---
title: Nastavení dodržování předpisů pro zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení, která můžete použít při nastavení dodržování předpisů pro zařízení s Androidem v Microsoft Intune. Nastavte pravidla pro hesla, vyberte minimální nebo maximální verzi operačního systému, omezte konkrétní aplikace, Zabraňte použití hesla a další.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58369ee2130ac296c9768812cf51b3fcbfed0d95
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329707"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Nastavení pro Android označení zařízení jako kompatibilních nebo nekompatibilních s Intune

Tento článek obsahuje seznam a popis různých nastavení dodržování předpisů, která můžete nakonfigurovat na zařízeních s Androidem v Intune. V rámci řešení pro správu mobilních zařízení (MDM) použijte Tato nastavení k označení rootem (jailbreak) zařízení jako nevyhovující předpisům, nastavte povolenou úroveň hrozby, povolte Google Play chránit a další.

Tato funkce platí pro:

- Správce zařízení s Androidem

Jako správce Intune můžete pomocí těchto nastavení dodržování předpisů ochránit prostředky vaší organizace. Další informace o zásadách dodržování předpisů a o tom, co dělají, najdete v tématu [Začínáme s dodržováním předpisů pro zařízení](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte zásadu dodržování předpisů](create-compliance-policy.md#create-the-policy). Pro možnost **platforma**vyberte **Správce zařízení s Androidem**.

## <a name="device-health"></a>Stav zařízení

- **Zařízení s rootem**:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Block** Zařízení s označením root (jailbreak) jako nevyhovující předpisům.

- **Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod**ní:

  Pomocí tohoto nastavení můžete v rámci podmínky dodržování předpisů převzít vyhodnocení rizik od připojené služby ochrany před mobilními hrozbami.
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů. 
  - **Zabezpečené** – Tato možnost je nejbezpečnější, protože zařízení nemůže mít žádné hrozby. Pokud jsou na zařízení zjištěny hrozby jakékoli úrovně, vyhodnotí se jako nevyhovující.
  - **Nízká** – zařízení se vyhodnotí jako vyhovující, pokud jsou přítomny jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.
  - **Střední** – zařízení se vyhodnotí jako vyhovující, pokud jsou stávající hrozby v zařízení na nízké nebo střední úrovni. Pokud se u zařízení zjistí vysoká míra ohrožení, vyhodnotí se jako nevyhovující.
  - **Vysoká** – Tato možnost je nejméně bezpečná a umožňuje všechny úrovně hrozeb. Může být užitečná, pokud toto řešení používáte jen ke generování sestav.

### <a name="google-play-protect"></a>Google Play chránit

- **Služby Google Play je nakonfigurované**:

  Aplikace Služby Google Play umožňuje instalaci aktualizací zabezpečení a je základní závislostí pro mnoho funkcí zabezpečení na zařízeních s certifikací Google.

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.  
  - **Vyžadovat** – vyžaduje, aby byla aplikace Google Play Services nainstalovaná a povolená.  

- **Aktuální poskytovatel zabezpečení**:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyžaduje, aby aktuální poskytovatel zabezpečení chránil zařízení před známými chybami zabezpečení.

- **Kontrola hrozeb v aplikacích**:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyžaduje, aby byla povolená funkce Androidu **ověřovat aplikace** .

  > [!NOTE]
  > Na starších verzích platformy Android tato funkce představuje nastavení dodržování předpisů. Intune může jenom zkontrolovat, jestli je toto nastavení povolené na úrovni zařízení.

- **Ověření zařízení SafetyNet**:

  Zadejte úroveň [ověření identity SafetyNet](https://developer.android.com/training/safetynet/attestation.html) , která musí být splněna. Možnosti:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Zkontrolovat základní integritu**
  - **Zkontrolovat základní integritu a certifikovaná zařízení**

> [!NOTE]
> Konfigurace nastavení Google Play chránit pomocí zásad ochrany aplikací najdete v tématu [nastavení zásad ochrany aplikací Intune](../apps/app-protection-policy-settings-android.md#conditional-launch) na Androidu.

## <a name="device-properties"></a>Vlastnosti zařízení

### <a name="operating-system-version"></a>Verze operačního systému 

- **Minimální verze operačního systému**:

  Pokud zařízení nesplňuje požadavek na minimální verzi operačního systému, nahlásí se jako nedodržující předpisy. Zobrazí se odkaz s informacemi, jak upgradovat. Koncový uživatel si může zařízení upgradovat. Potom získá přístup k prostředkům společnosti.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

- **Maximální verze OS**:

  Pokud zařízení používá verzi operačního systému, která je novější než verze zadaná v pravidle, bude přístup k prostředkům společnosti blokovaný. Uživateli se zobrazí výzva, aby kontaktoval správce IT. Dokud se pravidlo nezmění a nepovolí verzi operačního systému, nebude mít toto zařízení přístup k prostředkům společnosti.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

## <a name="system-security"></a>Zabezpečení systému

### <a name="password"></a>Heslo

<!-- Removed
- **Minimum password length**: Enter the minimum number of digits or characters that the user's password must have.   


- **Maximum minutes of inactivity before password is required**: Enter the idle time before the user must reenter their password. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

- **Password expiration (days)**: Select the number of days before the password expires and the user must create a new password.

- **Number of previous passwords to prevent reuse**: Enter the number of recent passwords that can't be reused. Use this setting to restrict the user from creating previously used passwords.

-->

- **Vyžadovat heslo k odemknutí mobilních zařízení**:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – uživatelé musí zadat heslo, aby mohli získat přístup ke svému zařízení.

- **Požadovaný typ hesla**:

  Vyberte, jestli má heslo obsahovat jenom číselné znaky, nebo kombinaci číslic a dalších znaků. Možnosti:

  - **Výchozí nastavení zařízení** – vyhodnotit dodržování předpisů heslem, nezapomeňte vybrat jinou sílu hesla než **výchozí zařízení**.
  - **Biometrika s nízkým zabezpečením**
  - **Aspoň číslice**
  - **Číselné komplexní** – opakované nebo po sobě jdoucí číslice, například `1111` nebo `1234`, nejsou povoleny.
  - **Aspoň abecední znaky**
  - **Aspoň alfanumerické znaky**
  - **Aspoň alfanumerické se symboly**

### <a name="encryption"></a>Šifrování

- **Šifrování datového úložiště na zařízení**:  
  *Podporováno v systému Android 4,0 a novějším nebo KNOX 4,0 a novějším.*

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – šifrovat úložiště dat v zařízeních. Zařízení se šifrují, pokud vyberete nastavení **Vyžadovat heslo k odemknutí mobilních zařízení**.

### <a name="device-security"></a>Zabezpečení zařízení

- **Blokovat aplikace z neznámých zdrojů**:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Blokové** zařízení s povoleným **zabezpečením > neznámými** zdroji (*podporované v Androidu 4,0 až Android 7. x. Nepodporováno v Androidu 8,0 a novějším.* )

  Pokud chcete instalovat aplikace bokem, musí být povoleny neznámé zdroje. Pokud aplikace pro Android neinstalujete bokem, nastavte tuto funkci na **Blokovat**, abyste tuto zásadu dodržování předpisů povolili.

  > [!IMPORTANT]
  > Aplikace instalované bokem vyžadují, aby bylo povolené nastavení **Blokovat aplikace z neznámých zdrojů**. Na dodržení této zásady trvejte jenom v případě, že na zařízeních neprovádíte instalaci aplikací pro Android bokem.

- **Integrita modulu runtime aplikace Portál společnosti**:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyberte *vyžadovat* a potvrďte, že aplikace Portál společnosti splňuje všechny následující požadavky:

    - Má nainstalované výchozí prostředí modulu runtime.
    - Je řádně podepsaná.
    - Není v režimu ladění.
    - Je nainstalovaná ze známého zdroje.

- **Blokovat na zařízení ladění USB** *(Android 4,2 nebo novější)* :

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Blok** – zabraňuje zařízením používat funkci ladění USB.

- **Minimální úroveň opravy zabezpečení** *(Android 6,0 nebo novější)* :

  Vyberte nejstarší úroveň opravy zabezpečení, kterou může zařízení mít. Zařízení, která nemají aspoň tuto úroveň opravy, nevyhovují. Datum musí být zadáno ve formátu `YYYY-MM-DD`.

  *Ve výchozím nastavení není nakonfigurované žádné datum*.

- **Aplikace s omezeným přístupem**:

  Zadejte **název aplikace** a **ID sady prostředků aplikace** pro aplikace, které by měly být omezené, a pak vyberte **Přidat**. Pokud je na zařízení nainstalovaná aspoň jedna zakázaná aplikace, označí se zařízení jako nevyhovující.

## <a name="next-steps"></a>Další kroky

- [Přidejte akce pro zařízení nedodržující předpisy](actions-for-noncompliance.md) a [použijte značky oboru k filtrování zásad](../fundamentals/scope-tags.md).
- [Monitorujte zásady dodržování předpisů](compliance-policy-monitor.md).
- Podívejte se na [nastavení zásad dodržování předpisů pro zařízení s Androidem Enterprise](compliance-policy-create-android-for-work.md) .
