---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14b571c069fd2484e7e3fd5f2841f6e5884ecc80
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502676"
---
# <a name="in-development-for-microsoft-intune"></a>Ve vývoji pro Microsoft Intune

Tato stránka vám umožní v rámci připravenosti a plánování vypsat aktualizace uživatelského rozhraní Intune a funkce, které jsou ve vývoji, ale ještě nejsou vydané. Kromě informací na této stránce: 

- Pokud předpokládáme, že před změnou budete muset provést nějakou akci, zveřejníme doplňkový příspěvek v centru zpráv Office.
- Pokud funkce vstoupí do produkčního prostředí, ať už je verze Preview, nebo je všeobecně dostupná, popis funkce se přesune z této stránky na [co je nového](whats-new.md).
- Tato stránka a stránka [co je nového](whats-new.md) se pravidelně aktualizují. Přijďte se tedy znovu podívat, jestli nejsou k dispozici nové informace.
- Strategické dodávky a časová osa najdete v tématu [Microsoft 365 plán](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) .

> [!NOTE]
> Tato stránka odráží naše aktuální očekávání funkcí Intune v nadcházející verzi. Data a jednotlivé funkce se můžou změnit. Tato stránka nepopisuje všechny funkce vývoje.

**Informační kanál RSS**: Zjistěte, kdy se tato stránka aktualizuje zkopírováním a vložením následující adresy URL do čtečky informačních kanálů:`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Tento článek byl naposledy aktualizován na datum uvedené pod nadpisem výše.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Správa aplikací

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Aktualizace ikon zařízení v Portál společnosti a aplikacích Intune v Androidu<!-- 6057023  -->
Aktualizujeme ikony zařízení v aplikacích Portál společnosti a Intune na zařízeních s Androidem, abyste vytvořili pokročilejší vzhled a atmosféru a mohli se přizpůsobit k systému Microsoft Fluent design. Související informace najdete v tématu [aktualizace ikon v aplikaci Portál společnosti App pro iOS/iPadOS a MacOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>S/MIME pro Outlook na zařízeních s iOS a Androidem Enterprise spravovaná bez registrace<!-- 6517155  -->
Pomocí zásad konfigurace aplikací pro zařízení spravovaná bez registrace budete moct povolit S/MIME v aplikaci Outlook v zařízeních S iOS a Androidem Enterprise. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**  >  **spravované aplikace**. Kromě toho můžete zvolit, jestli chcete uživatelům dovolit, aby toto nastavení v Outlooku změnili. Další informace o nastavení konfigurace aplikace Outlook najdete v tématu [nastavení konfigurace aplikace Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Portál společnosti bude podporovat automatické registrace zařízení společnosti Apple bez přidružení uživatele.<!-- 7282707  --> 
v zařízeních zaregistrovaných pomocí automatizované registrace zařízení společnosti Apple se bude podporovat iOS Portál společnosti, aniž by museli přiřazeného uživatele. Koncový uživatel se může přihlásit k Portál společnosti iOS, aby se sám navázal jako primární uživatel na zařízení se systémem iOS/iPadOS, které je zaregistrované bez spřažení zařízení. Další informace o automatizované registraci zařízení najdete v tématu [Automatická registrace zařízení s iOS/iPadOS pomocí automatizované registrace zařízení společnosti Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Oznámení o instalaci aplikace Win32 a Portál společnosti<!-- 7485945  -->
Koncoví uživatelé budou moci rozhodnout, zda aplikace, které jsou uvedeny ve [Microsoft Intune Web portál společnosti](https://portal.manage.microsoft.com/) by měly být otevřeny aplikací portál společnosti nebo webovým portál společnosti. Tato možnost je dostupná jenom v případě, že má koncový uživatel nainstalovanou aplikaci Portál společnosti a spustí webovou aplikaci Portál společnosti mimo prohlížeč.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Portál společnosti přidává podporu aplikací Configuration Manager<!-- 4297660 -->
Portál společnosti teď podporuje Configuration Manager aplikace. Tato funkce umožňuje koncovým uživatelům zobrazit Configuration Manager i aplikace nasazené v Intune v Portál společnosti pro spoluspravované zákazníky. Tato podpora pomůže správcům konsolidovat různé prostředí portálu pro koncové uživatele. Další informace najdete v tématu [použití portál společnosti aplikace na spoluspravovaných zařízeních](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Nastavit stav dodržování předpisů zařízením od partnerů MDM třetích stran<!-- 6361689   -->
Microsoft 365 zákazníci, kteří vlastní řešení MDM třetí strany, budou moci vyhovět zásadám podmíněného přístupu pro aplikace Microsoft 365 v iOS a Androidu prostřednictvím integrace se službou Microsoft Intune dodržování předpisů zařízením. Dodavatel MDM třetí strany bude využívat službu Intune pro dodržování předpisů zařízením k odesílání dat o dodržování předpisů zařízením do Intune. Intune se pak vyhodnotí a určí, jestli je zařízení důvěryhodné, a nastavte atributy podmíněného přístupu ve službě Azure AD.  Zákazníci budou muset nastavit zásady podmíněného přístupu Azure AD z centra pro správu Microsoft Endpoint Manageru nebo z portálu Azure AD.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nové nastavení sítě VPN pro zařízení s Windows 10 a novějšími systémy<!-- 6602122  -->
Když vytváříte profil sítě VPN pomocí typu připojení IKEv2, můžete nakonfigurovat nová nastavení. (**Devices**  >  **konfigurační profily**zařízení  >  **vytvořit profil**  >  **Windows 10 a novější** pro platformu > **VPN** pro > **základní síť VPN**):

- **Tunelové zařízení**: umožňuje zařízení automaticky se připojovat k síti VPN bez nutnosti zásahu uživatele, včetně přihlášení uživatele. Tato funkce vyžaduje, abyste povolili funkci **Always On**a jako metodu ověřování používali **certifikáty počítače** .
- Nastavení kryptografie: umožňuje nakonfigurovat algoritmy používané k zabezpečení IKE a podřízená přidružení zabezpečení, která vám umožní odpovídat nastavení klienta a serveru.

Pokud chcete zobrazit nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Windows a přidejte připojení k síti VPN pomocí Intune](../configuration/vpn-settings-windows-10.md).

Platí pro:
- Windows 10 a novější

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Nové funkce pro spravovanou domovskou obrazovku na vyhrazených zařízeních vlastníka zařízení s Androidem Enterprise (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
Na zařízeních s Androidem Enterprise budou správci moct pomocí profilů konfigurace zařízení přizpůsobit spravovanou domovskou obrazovku na vyhrazených zařízeních pomocí beznabídkového režimu s více aplikacemi **(**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**pro zařízení pro  >  **Android Enterprise** **vlastní**nastavení  >  **Device Restrictions** **cloudu**> jenom pro možnost profilace zařízení >).

Konkrétně můžete:

- Přizpůsobení ikon, změna orientace obrazovky a zobrazení oznámení aplikací pro ikony BADGE <!--7414175-->
- Skrýt vstupní bod spravovaného nastavení <!--7133328-->
- Snadnější přístup k nabídce ladění <!--7133720-->
- Vytvoření seznamu povolených sítí Wi-Fi <!-- 7134873-->
- Snazší přístup k informacím o zařízení <!-- 7135184-->

Další informace najdete v tématu [nastavení zařízení s Androidem Enterprise pro povolení nebo omezení funkcí](../configuration/device-restrictions-android-for-work.md).

Platí pro:

- Vlastníci zařízení s Androidem Enterprise, vyhrazená zařízení (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrace zařízení

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Zařízení ve vlastnictví firmy (Preview)<!--4442275 -->
Intune bude podporovat zařízení s Androidem Enterprise ve vlastnictví firmy s pracovním profilem pro verze operačního systému Android 8 a vyšší. Zařízení vlastněná společností s pracovním profilem jsou jedním z scénářů podnikové správy v sadě Android Enterprise Solution. Tento scénář je určený pro samostatná uživatelská zařízení určená pro podnikové a osobní použití. Tento scénář, který je ve vlastnictví firmy, nabízí:

- pracovní a osobní profilové kontejnery
- řízení na úrovni zařízení pro správce
- záruka pro koncové uživatele, že jejich osobní data a aplikace zůstanou v soukromí

První verze Public Preview bude obsahovat podmnožinu funkcí, které budou zahrnuty do všeobecně dostupné verze. Další funkce budou přidány do provozu. Mezi funkce, které budou dostupné v první verzi Preview, patří:

- Registrace: Správci můžou vytvořit několik profilů zápisu s jedinečnými tokeny, jejichž platnost nevyprší. Registrace zařízení se dá dělat prostřednictvím NFC, záznamu tokenu, kódu QR, nulového dotyku nebo registrace pro telefonickou instalaci v Knox.
- Konfigurace zařízení: podmnožina existujících plně spravovaných a vyhrazených nastavení zařízení.
- Dodržování předpisů zařízením: zásady dodržování předpisů, které jsou aktuálně k dispozici pro plně spravovaná zařízení.
- Akce zařízení: odstranit zařízení (resetování továrního nastavení), restartovat zařízení a uzamknout zařízení.  
- Správa aplikací: přiřazení aplikací, konfigurace aplikací a přidružené možnosti vytváření sestav 
- Podmíněný přístup



<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Protokoly dodržování předpisů pro zařízení teď v angličtině<!--6014904 -->
Protokoly IntuneDeviceComplianceOrg mají pouze výčty pro ComplianceState, OwnerType a DeviceHealthThreatLevel. V budoucí aktualizaci budou tyto protokoly obsahovat anglické informace ve sloupcích.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
V **sestavách**  >  **Log Analytics**budou k dispozici protokoly podrobností o zařízeních v Intune. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Připojení tenanta: časová osa zařízení v centru pro správu<!--7220536, CM7141381 -->
Když Configuration Manager synchronizuje zařízení s Microsoft Endpoint Managerem prostřednictvím připojení tenanta, budete moct zobrazit časovou osu událostí. Tato časová osa zobrazuje minulou aktivitu v zařízení, která vám může pomoct při řešení problémů. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Připojení tenanta: instalace aplikace z centra pro správu<!-- 7220536, CM6024389 -->
Instalaci aplikace můžete zahájit v reálném čase pro zařízení připojené k tenantovi z centra pro správu služby Microsoft Endpoint Management. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Připojení tenanta: CMPivot z centra pro správu<!--7220536, CM6024392 -->
Budete moct využít sílu [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) do centra pro správu Microsoft Endpoint Manageru. Umožněte dalším osoby, jako je helpdesk, aby bylo možné iniciovat dotazy v reálném čase z cloudu proti jednotlivým zařízením spravovaným nástrojem ConfigMgr a vracet výsledky zpátky do centra pro správu. To poskytuje všechny tradiční výhody CMPivot, které správcům IT a dalším určeným osoby schopnost rychle vyhodnotit stav zařízení ve svém prostředí a provést akci. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Připojení tenanta: spuštění skriptů z centra pro správu<!--7220536, CM6234688 -->
Do centra pro správu služby Microsoft Endpoint Manager budete moct využít sílu Configuration Manager funkce místního [spouštění skriptů](../../configmgr/apps/deploy-use/create-deploy-scripts.md) . Povolí další osoby, jako je helpdesk, aby se spouštěly skripty PowerShellu z cloudu proti jednotlivým Configuration Manager spravovaným zařízením. To poskytuje všechny tradiční výhody skriptů PowerShellu, které již byly definovány a schváleny správcem Configuration Manager k tomuto novému prostředí. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nová logika sloučení pro zařízení s Windows 10<!--179048-->
Pokud se dnes zákazník znovu pokusí vytvořit kopii zařízení a pak ho znovu zaregistruje, zobrazí se v konzole pro správu Microsoft Endpoint Manageru víc záznamů pro toto zařízení. Nová logika sloučení je ve vývoji ke sloučení takových duplicitních záznamů pro zařízení s Windows 10.

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>Aktualizace akce vzdáleného uzamčení pro zařízení macOS<!--7032805 -->
Aktualizace akce vzdálené uzamčení pro zařízení macOS budou zahrnovat:
- PIN kód pro obnovení se zobrazí po dobu 30 dní před odstraněním (ne sedm dní).
- Pokud má správce druhý otevřený prohlížeč a pokusí se znovu aktivovat příkaz z jiné karty nebo prohlížeče, Intune umožní příkazu projít. Stav vytváření sestav se ale nastaví jako neúspěšný, nikoli generování nového PIN kódu.
- Správce nebude moci vydat další příkaz pro vzdálené uzamčení, pokud je předchozí příkaz stále čeká nebo pokud se zařízení nevrátilo zpět.
Tyto změny jsou navržené tak, aby se zabránilo přepsání správného kódu PIN po několika příkazech vzdáleného zamykání.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Nasazení aktualizací softwaru do zařízení macOS <!-- 3194876 -->
Aktualizace softwaru budete moct nasadit do skupin zařízení macOS. Tato funkce zahrnuje kritické, firmware, konfigurační soubor a další aktualizace. V příští registraci zařízení budete moct odesílat aktualizace, nebo můžete vybrat týdenní plán pro nasazení aktualizací do nebo z časového intervalu, který jste nastavili. To pomáhá při aktualizaci zařízení mimo standardní pracovní dobu nebo v případě, že je vaše Helpdesk plně přiřazená. Zobrazí se vám také podrobná sestava všech zařízení macOS s nasazenými aktualizacemi. Pokud chcete zobrazit stav konkrétních aktualizací, můžete přejít k sestavě podle jednotlivých zařízení.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Další vlastnosti datového skladu v 1.0<!-- 6125732   -->
Další vlastnosti jsou k dispozici pomocí datového skladu Intune v 1.0. Následující vlastnosti jsou nyní zpřístupněny prostřednictvím entity [zařízení](../developer/reports-ref-devices.md#devices) :
- `ethernetMacAddress`– Jedinečný identifikátor sítě tohoto zařízení.
- `office365Version`– Verze Office 365, která je na zařízení nainstalovaná.

Následující vlastnosti jsou nyní zpřístupněny prostřednictvím entity [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) :
- `physicalMemoryInBytes`– Fyzická paměť v bajtech.
- `totalStorageSpaceInBytes`-Celková kapacita úložiště v bajtech.

Další informace najdete v tématu [Microsoft Intune rozhraní API datového skladu](../developer/reports-nav-intune-data-warehouse.md).

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Šablona sestavy dodržování předpisů Power BI V 2.0<!-- 636958  -->
Správci budou moct aktualizovat verzi šablony zprávy o kompatibilitě Power BI z verze 1.0 až verze 2.0. Verze 2.0 bude obsahovat vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Související informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Řízení přístupu na základě role

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Podpora značek oboru pro zásady přizpůsobení<!--6182440 -->
Budete moct přiřadit značky oboru k zásadám přizpůsobení. Provedete to tak, že přejdete do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Tenant administration** >  **přizpůsobení** , kde se zobrazí možnosti konfigurace **značky oboru** .

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Přiřadit změny oprávnění profilování a aktualizace profilu<!--7177586 -->
Oprávnění k řízení přístupu na základě rolí se mění pro přiřazení profilu a profilu aktualizace:
- Přiřadit profil: Správci s tímto oprávněním budou moci přiřadit profily k tokenům a přiřadit k tokenu výchozí profil.
- Aktualizovat profil: Správci s tímto oprávněním budou moci aktualizovat pouze existující profily.

<!-- ***********************************************-->
## <a name="security"></a>Zabezpečení

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Podpora zásad ochrany aplikací pro Symantec Endpoint Security a Check Point Sandblast<!--  4452423, 4731168 -->

V říjnu 2019 zásady ochrany aplikací Intune přidaly možnost používat data z některých našich partnerů ochrany před internetovými útoky (MTD partneři Microsoftu). Přidáváme podporu pro následující partnery, aby bylo možné použít zásady ochrany aplikací k blokování nebo selektivnímu vymazání podnikových dat uživatele na základě stavu zařízení:

- **Check Point Sandblast** v Androidu, iOS a iPadOS
- **Symantec Endpoint Security** na Androidu, iOS a iPadOS

Informace o používání zásad ochrany aplikací s partnery MTD najdete v tématu [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami v Intune](../protect/mtd-app-protection-policy.md).

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Před registrací v Intune uložte obnovovací klíč pro zařízení macOS, které se zašifroval pomocí trezoru.<!--5239424   -->
Brzy budou koncoví uživatelé zařízení macOS, kteří se před registrací do Intune zašifroval, nebo zašifrované předtím, než je zaregistrované v Intune, nebudou muset dešifrovat zařízení, aby je bylo možné znovu šifrovat pomocí Intune. Místo toho může aktuální šifrování zůstat na svém místě a uživatel může přejít na web Portál společnosti, kde si můžou vybrat možnost *Uložit obnovovací klíč* a odeslat svůj osobní obnovovací klíč pro šifrované zařízení MacOS. Po odeslání platného klíče Intune otočí osobní klíč, aby vygeneroval nový klíč, který bude k dispozici pro uživatele prostřednictvím Portál společnosti webu, iOS/Portál společnosti, Android Portál společnosti nebo aplikace Intune. Uživatelé pak budou mít přístup k těmto umístěním z libovolného zařízení, aby si mohli klíč zobrazit v zařízení macOS.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>Skrýt osobní obnovovací klíč od uživatele zařízení během šifrování disku macOS trezoru<!--  5475632  -->
Přidáváme nové nastavení s názvem *Skrýt obnovovací klíč* pro zásady šifrování disku Endpoint Security pro trezor (**koncový bod zabezpečení**  >  **disku**  >  **Create Profile**  >  **MacOS**  >  **FileVault**). Když zapnete nové nastavení, Intune během šifrování skryje osobní obnovovací klíč od uživatele zařízení macOS. Skrytím klíče v tuto chvíli můžete zajistit, aby byla zabezpečená, protože uživatelé nebudou moct zapisovat mimo jiné při čekání na šifrování zařízení. Místo toho může uživatel při obnovení vždy použít jakékoli zařízení k zobrazení svého osobního obnovovacího klíče prostřednictvím webu Portál společnosti Intune.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Vylepšené zobrazení podrobností o standardních hodnotách zabezpečení pro zařízení<!-- 5536846   -->
Pracujeme na vylepšení zobrazení podrobností pro nastavení standardních hodnot zabezpečení, když přejdete k podrobnostem o zařízení (zařízení**zabezpečení koncového bodu**  >  **Devices**).  U každého přiřazeného směrného plánu zabezpečení budete moct zobrazit nestrukturovaný seznam podrobností pro každé nastavení, které zahrnuje kategorie nastavení, nastavení názvů a stav každého nastavení v tomto zařízení.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Správa zdrojových umístění pro aktualizace definic pomocí zásad služby Endpoint Security AntiVir pro zařízení s Windows 10<!-- 6347801  -->  
Přidáváme dvě nová nastavení do kategorie *aktualizace* zásad ochrany koncových bodů Endpoint Security pro zařízení s Windows 10, která vám pomůžou spravovat, jak zařízení získávají definice aktualizací (**Endpoint Security** > * * Antivirus * * > **vytvořit zásadu**  >  **Windows 10 a novější**  >  **antivirovou ochranu v programu Microsoft Defender**).

S novým nastavením budete moct přidat sdílené složky UNC jako umístění zdrojů pro aktualizace definic a definovat pořadí, ve kterém se budou kontaktovat různá zdrojová umístění. Nové nastavení bude spravovat následující zprostředkovatele CSP v programu Defender:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>Zjišťování koncových bodů a zásady odezvy pro zařízení připojená k klientovi do MDATP se přesouvá mimo verzi Preview.<!-- 7303816   -->
Jako součást zabezpečení koncového bodu v Intune podporuje zásady detekce a odezvy koncových bodů (EDR) pro použití se zařízeními, která spravuje Configuration Manager, brzy přestanou být ve verzi Preview**Endpoint security**a bude všeobecně dostupná (  >  **zásada zjišťování koncových bodů**zabezpečení koncového bodu a odpověď na Windows  >  **Create Policy**  >  **10 a Windows Server**). Když nakonfigurujete [připojení tenanta pro Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md), můžete pomocí zásad EDR připojit zařízení spravovaná pomocí Configuration Manager k Rozšířené ochraně před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP). 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Vylepšení uzlu základní hodnoty zabezpečení<!-- 7433136   -->
Pro zlepšení použitelnosti uzlu základní hodnoty zabezpečení v centru pro správu Microsoft Endpoint Manageru odebíráme kartu *Přehled* pro každý směrný plán a místo toho se otevře karta **profil** směrného plánu (směrný plán zabezpečení**koncového bodu zabezpečení služby Endpoint Security**  >  **Security baselines**  >  *baseline*).

Na stránce *Přehled* jednotlivých standardních hodnot se zobrazí grafy a dlaždice, které agreguje výsledky z poslední nasazené verze, kterou jste nasadili. Tyto informace jsou duplikovány z toho, co vidíte, pokud chcete získat další podrobnosti o verzi. Po odebrání stránky s *přehledem* budou tyto grafy a agregované podrobnosti zůstat dostupné, i když přejdete přímo k verzi.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Nástroj pro migraci pravidel brány firewall Preview<!-- 6423187  -->
Ve verzi Public Preview pracujeme na nástroji založeném na prostředí PowerShell, který bude migrovat pravidla firewallu v programu Windows Defender. Když nainstalujete a spustíte nástroj, automaticky se vytvoří zásady pravidla firewallu zabezpečení koncového bodu pro Intune, které jsou založené na aktuální konfiguraci klienta s Windows 10.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Nová nastavení pro profil ovládacího prvku zařízení v zásadách redukce pro útok na službu Endpoint Security<!--7032084 -->
Přidáváme několik nastavení pro zařízení s Windows 10 do profilu řízení zařízení pro zásady omezení pro útoky na zabezpečení koncového bodu. (omezení**zabezpečení koncového bodu**:  >  **omezení**  >  **Vytvoření zásady**pro  >  **zařízení s Windows 10 a novější**  >  ).**Device control** 

Nová nastavení budou stejná jako ta nastavení, která jsou dnes k dispozici v [profilech omezení zařízení](../configuration/device-restrictions-windows-10.md) pro *konfiguraci zařízení*. Nastavení, která se přidávají do profilu *řízení zařízení* , by měla obsahovat různá nastavení Bluetooth.  


<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
