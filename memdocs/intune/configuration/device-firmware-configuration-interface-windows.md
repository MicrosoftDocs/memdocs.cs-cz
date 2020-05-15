---
title: Aktualizace funkcí systému Windows BIOS pomocí zásad MDM v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte profil rozhraní DFCI (Device firmware Configuration Interface) pro správu nastavení UEFI, jako je CPU, integrovaný hardware a možnosti spouštění na zařízeních s Windows 10 v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: dce3c269686c6928e495796dedbadc6a1ba51a99
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401633"
---
# <a name="use-device-firmware-configuration-interface-profiles-on-windows-devices-in-microsoft-intune-public-preview"></a>Použití profilů rozhraní pro konfiguraci firmwaru zařízení na zařízeních s Windows v Microsoft Intune (Public Preview)

Pokud ke správě zařízení autopilot používáte Intune, můžete po registraci spravovat nastavení rozhraní UEFI (DFCI) pomocí rozhraní pro konfiguraci firmwaru zařízení. Přehled výhod, scénářů a požadavků najdete v tématu [Přehled DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/).

DFCI [umožňuje systému Windows](https://docs.microsoft.com/windows/client-management/mdm/uefi-csp) předat příkazy správy z Intune do rozhraní UEFI (rozhraní UEFI (Unified Extensible Firmware Interface)).

Pomocí této funkce můžete v Intune ovládat nastavení systému BIOS. Firmware je typicky odolný vůči škodlivým útokům. Omezuje koncovým uživatelům kontrolu nad systémem BIOS, což je v napadené situaci dobré.

Například používáte zařízení s Windows 10 v zabezpečeném prostředí a chcete kameru zakázat. Fotoaparát můžete zakázat ve vrstvě firmwaru, takže nezáleží na tom, co dělá koncový uživatel. Po přeinstalaci operačního systému nebo vymazání počítače se fotoaparát znovu nezapne. V jiném příkladu můžete uzamknout možnosti spouštění, aby uživatelé nemohli spustit jiný operační systém nebo starší verzi Windows, která nemá stejné funkce zabezpečení.

Pokud přeinstalujete starší verzi Windows, nainstalujete samostatný operační systém nebo naformátujete pevný disk, nebudete moct DFCI správu přepsat. Tato funkce může zabránit malwaru v komunikaci s procesy operačního systému, včetně zvýšených procesů operačního systému. Řetěz certifikátů DFCI používá kryptografii s veřejným klíčem a není závislý na zabezpečení hesla místního rozhraní UEFI (BIOS). Tato vrstva zabezpečení blokuje místním uživatelům přístup ke spravovaným nastavením z nabídek systému UEFI (BIOS) zařízení.

Tato funkce platí pro:

- Windows 10 RS5 (1809) a novější v podporovaném rozhraní UEFI

## <a name="before-you-begin"></a>Před zahájením

- Výrobce zařízení musí mít v výrobním procesu přidaný DFCI do firmwaru rozhraní UEFI nebo jako aktualizaci firmwaru, kterou nainstalujete. Spolupracujte se svými dodavateli zařízení a určete [výrobce, kteří podporují DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/#oems-that-support-dfci), nebo verzi firmwaru, která je potřebná k použití DFCI.

- Zařízení musí být zaregistrované pro Windows autopiloter pomocí [partnera poskytovatele řešení Microsoft Cloud (CSP)](https://partner.microsoft.com/cloud-solution-provider)nebo zaregistrovaného přímo výrobcem OEM. 

  Zařízení, která se registrují ručně pro autopilot, jako je [Import ze souboru CSV](../enrollment/enrollment-autopilot.md#add-devices), nemůžou používat DFCI. V rámci návrhu DFCI Management vyžaduje externí ověření komerčního akvizice zařízení prostřednictvím výrobce OEM nebo registrace partnera Microsoft CSP pro Windows autopilot.

  Po registraci zařízení se v seznamu zařízení s Windows autopilotem zobrazí jeho sériové číslo.

  Další informace o autopilotu, včetně všech požadavků, najdete v tématu [registrace zařízení s Windows v Intune pomocí automatických pilotů Windows](../enrollment/enrollment-autopilot.md).

## <a name="create-your-azure-ad-security-groups"></a>Vytvoření skupin zabezpečení služby Azure AD

Profily nasazení autopilotu jsou přiřazené ke skupinám zabezpečení Azure AD. Nezapomeňte vytvořit skupiny, které zahrnují vaše zařízení s podporou DFCI. U zařízení DFCI může většina organizací vytvářet skupiny zařízení místo skupin uživatelů. Zvažte následující scénáře:

- Lidské zdroje (HR) mají různá zařízení s Windows. Z bezpečnostních důvodů nechcete, aby se na zařízeních používala žádná z uživatelů v této skupině. V tomto scénáři můžete vytvořit skupinu uživatelů zabezpečení lidských zdrojů, aby se zásady platily pro uživatele ve skupině HR bez ohledu na typ zařízení.
- Na výrobním patře máte 10 zařízení. Na všech zařízeních chcete zabránit spouštění zařízení ze zařízení USB. V tomto scénáři můžete vytvořit skupinu zařízení zabezpečení a přidat do ní Tato 10 zařízení.

Další informace o vytváření skupin v Intune najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).

## <a name="create-the-profiles"></a>Vytvoření profilů

Pokud chcete používat DFCI, vytvořte následující profily a přiřaďte je ke skupině.

### <a name="create-an-autopilot-deployment-profile"></a>Vytvoření profilu nasazení Autopilotu

Tento profil nastaví a předem nakonfiguruje nová zařízení. [Profil nasazení autopilotu](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile) obsahuje seznam kroků pro vytvoření profilu.

### <a name="create-an-enrollment-state-page-profile"></a>Vytvořit profil stránky stavu registrace

Tento profil zajišťuje, aby byla zařízení ověřená a povolená pro DFCI během instalace Windows. Tento profil se doporučuje používat k blokování používání zařízení, dokud se nenainstalují všechny aplikace a profily. [Profil stránky stavu registrace](../enrollment/windows-enrollment-status.md) uvádí postup vytvoření profilu.

### <a name="create-the-dfci-profile"></a>Vytvoření profilu DFCI

Tento profil obsahuje nastavení DFCI, která nakonfigurujete.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: Zvolte **Windows 10 a novější**.
    - **Profil**: vyberte **rozhraní pro konfiguraci firmwaru zařízení**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **Windows: Konfigurace nastavení DFCI na zařízeních s Windows**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**nakonfigurujte následující nastavení:

    - **Umožňuje místnímu uživateli změnit nastavení rozhraní UEFI (BIOS)**: vaše možnosti:
      - **Jenom nenakonfigurovaná nastavení**: místní uživatel může změnit jakékoli nastavení, *s výjimkou* toho, že nastavení je explicitně nastavené na **Povolit** nebo **Zakázat** v Intune.
      - **Žádné**: místní uživatel nesmí měnit nastavení rozhraní UEFI (BIOS), včetně nastavení nezobrazených v profilu DFCI.

    - **Virtualizace CPU a v/** v: vaše možnosti:
        - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
        - **Povoleno**: systém BIOS povoluje možnosti virtualizace procesoru a vstupně-výstupních operací platformy pro použití v operačním systému. Zapne technologie Windows Virtualization Security a Device Guard.
    - **Kamery**: vaše možnosti:
        - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
        - **Povoleno**: jsou povoleny všechny integrované kamery přímo spravované pomocí rozhraní UEFI (BIOS). Periferní zařízení, jako jsou kamery USB, nejsou ovlivněná.
        - **Zakázáno**: všechny integrované kamery přímo spravované pomocí rozhraní UEFI (BIOS) jsou zakázané. Periferní zařízení, jako jsou kamery USB, nejsou ovlivněná.
    - Mikrofony **a reproduktory**: vaše možnosti:
        - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
        - **Povoleno**: jsou povoleny všechny integrované mikrofony a reproduktory přímo spravované rozhraním UEFI (BIOS). Periferní zařízení, jako jsou zařízení USB, ovlivněná nejsou.
        - **Zakázáno**: všechny integrované mikrofony a reproduktory přímo spravované pomocí rozhraní UEFI (BIOS) jsou zakázané. Periferní zařízení, jako jsou zařízení USB, ovlivněná nejsou.
    - **Radiostanice (Bluetooth, Wi-Fi, NFC atd.)**: vaše možnosti:
        - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
        - **Povoleno**: jsou povoleny všechny vestavěné radiostanice přímo spravované pomocí rozhraní UEFI (BIOS). Periferní zařízení, jako jsou zařízení USB, ovlivněná nejsou.
        - **Zakázáno**: jsou zakázaná všechna integrovaná radiostanice přímo spravovaná rozhraním UEFI (BIOS). Periferní zařízení, jako jsou zařízení USB, ovlivněná nejsou.

        > [!WARNING]
        > Pokud zakážete nastavení **přepínačů** , bude zařízení vyžadovat kabelové připojení k síti. V opačném případě může být zařízení nemožné spravovat.

    - **Spustit z externího média (USB, SD)**: vaše možnosti:
        - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
        - **Enabled**: rozhraní UEFI (BIOS) umožňuje spuštění z úložiště bez pevného disku.
        - **Disabled**: rozhraní UEFI (BIOS) neumožňuje spouštění z úložiště bez pevného disku.
    - **Spouštění ze síťových adaptérů**: vaše možnosti:
        - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
        - **Enabled**: rozhraní UEFI (BIOS) umožňuje spuštění z vestavěných síťových rozhraní.
        - **Disabled**: rozhraní UEFI (BIOS) neumožňuje spouštění vestavěných síťových rozhraní.

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupinu uživatelů, kteří obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Při příštím ověření každého zařízení se zásada použije.

## <a name="assign-the-profiles-and-reboot"></a>Přiřaďte profily a restartujte počítač.

Nezapomeňte [přiřadit](../configuration/device-profile-assign.md) profily ke skupinám zabezpečení Azure AD, které zahrnují vaše zařízení DFCI. Profil může být přiřazený, když je vytvořený, nebo později.

Když zařízení spustí automatický pilotní program Windows, během stránky stav registrace může DFCI Vynutit restartování. Tímto prvním restartováním zaregistrujete rozhraní UEFI do Intune. 

Pokud chcete potvrdit, že je zařízení zaregistrované, můžete znovu restartovat zařízení, ale není to nutné. Použijte pokyny výrobce zařízení k otevření nabídky UEFI a potvrďte, že je rozhraní UEFI teď spravované.

Když se zařízení příště synchronizuje s Intune, Windows přijme nastavení DFCI. Restartujte zařízení. Tento třetí restart vyžaduje, aby rozhraní UEFI přijímalo nastavení DFCI ze systému Windows.

## <a name="update-existing-dfci-settings"></a>Aktualizovat existující nastavení DFCI

Pokud chcete změnit stávající nastavení DFCI na zařízeních, která se používají, můžete. V existujícím profilu DFCI změňte nastavení a uložte provedené změny. Vzhledem k tomu, že profil je již přiřazen, nové nastavení DFCI se projeví v těchto případech:

1. Zařízení se ve službě Intune zarezervuje, aby zkontrolovala aktualizace profilu. Vrácení se změnami proběhne v různou dobu. Další informace najdete v tématu [Pokud zařízení získávají aktualizace zásad, profilů nebo aplikací](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

2. Chcete-li nové nastavení vynutilo, restartujte zařízení [vzdáleně](../remote-actions/device-restart.md) nebo místně.

Můžete také [signalizovat zařízení, která se mají vrátit](../remote-actions/device-sync.md). Po úspěšné synchronizaci se [signál dorestartuje](../remote-actions/device-restart.md).

>[!NOTE]
> Když odstraníte profil DFCI nebo odeberete zařízení ze skupiny přiřazené k profilu, neodeberete nastavení DFCI nebo znovu povolíte nabídky UEFI (BIOS). Pokud chcete přestat používat DFCI, aktualizujte stávající profil DFCI. Další informace o postupu najdete v tématu [vyřazení zařízení](#retire) v tomto článku.

## <a name="reuse-retire-or-recover-the-device"></a>Opětovné použití, vyřazení nebo obnovení zařízení

### <a name="reuse"></a>Opakované použití

Pokud se chystáte resetovat Windows, aby se zařízení obnovilo, pak [zařízení vymažte](../remote-actions/devices-wipe.md). **Neodstraňujte** záznam zařízení autopilot.

Po vymazání zařízení přesuňte zařízení do skupiny přiřazené nové profily DFCI a autopilotu. Nezapomeňte restartovat zařízení a znovu spusťte instalační program systému Windows.

### <a name="retire"></a>Vyřazení

Až budete připraveni zařízení vyřadit z provozu a uvolnit ho ze správy, aktualizujte profil DFCI na nastavení rozhraní UEFI (BIOS), které chcete ve stavu ukončení. Obvykle chcete povolit všechna nastavení. Příklad:

1. Otevřete profil DFCI (**Devices**  >  **profily konfigurace**zařízení).
2. Změňte **nastavení nastavit místnímu uživateli, aby se změnila nastavení rozhraní UEFI (BIOS)** na **nenakonfigurovaná nastavení**.
3. Nastavte všechna ostatní nastavení na **nenakonfigurovaná**.
4. Uložte nastavení.

Tyto kroky odemknou nabídky systému UEFI (BIOS) zařízení. Hodnoty zůstanou stejné jako profil (**povolený** nebo **zakázaný**) a nejsou nastavené zpátky na výchozí hodnoty operačního systému.

Teď jste připraveni zařízení vymazat. Jakmile bude zařízení vymazáno, odstraňte záznam autopilotu. Odstraněním záznamu zabráníte, aby se zařízení při restartování automaticky znovu zaregistrovalo.

### <a name="recover"></a>Zotavit

Pokud zařízení vymažete a odstraníte záznam autopilotu před tím, než se odzamkne nabídky rozhraní UEFI (BIOS), zůstanou nabídky uzamčené. Intune nemůže odeslat aktualizace profilu, aby ho odemkl.

Pokud chcete zařízení odemknout, otevřete nabídku rozhraní UEFI (BIOS) a aktualizujte správu ze sítě. Obnovení odemyká nabídky, ale ponechá nastavení rozhraní UEFI (BIOS) nastavená na hodnoty v předchozím profilu Intune DFCI.

## <a name="end-user-impact"></a>Dopad na koncového uživatele

Když se použije zásada DFCI, místní uživatelé nemůžou měnit nastavení nakonfigurovaná pomocí DFCI, a to i v případě, že je nabídka UEFI (BIOS) chráněná heslem. V závislosti na nastaveních, která nakonfigurujete, mohou koncoví uživatelé obdržet chyby, že hardwarové komponenty se nenašly nebo se nedají diagnostikovat. Nezapomeňte poskytnout koncovým uživatelům dokumentaci, která vysvětluje možnosti, které jste zakázali.  

## <a name="next-steps"></a>Další kroky

Po [přiřazení profilu](device-profile-assign.md) [sledujte jeho stav](device-profile-monitor.md).
