---
title: Nastavení dodržování předpisů pro Android Enterprise v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení, která můžete použít při nastavování dodržování předpisů pro zařízení s Androidem Enterprise v Microsoft Intune. Nastavte pravidla pro hesla, vyberte minimální nebo maximální verzi operačního systému, omezte konkrétní aplikace, Zabraňte použití hesla a další.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 9da89713-6306-4468-b211-57cfb4b51cc6
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9897f824bb1bd13c1d12ff0c705b42cea275b9d4
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462078"
---
# <a name="android-enterprise-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Nastavení Androidu Enterprise k označení zařízení jako kompatibilních nebo nekompatibilních s Intune

Tento článek obsahuje seznam a popis různých nastavení dodržování předpisů, která můžete nakonfigurovat na zařízeních s Androidem Enterprise v Intune. V rámci řešení pro správu mobilních zařízení (MDM) použijte Tato nastavení k označení rootem (jailbreak) zařízení jako nevyhovující předpisům, nastavte povolenou úroveň hrozby, povolte Google Play chránit a další.

Tato funkce platí pro:

- Android Enterprise

Jako správce Intune můžete pomocí těchto nastavení dodržování předpisů ochránit prostředky vaší organizace. Další informace o zásadách dodržování předpisů a o tom, co dělají, najdete v tématu [Začínáme s dodržováním předpisů pro zařízení](device-compliance-get-started.md).

> [!IMPORTANT]
> Zásady dodržování předpisů také používají vyhrazená zařízení s Androidem Enterprise. Pokud je zásada dodržování předpisů přiřazená vyhrazenému zařízení, může se zařízení zobrazovat jako **nevyhovující předpisům**. Podmíněný přístup a vynucování dodržování předpisů není na vyhrazených zařízeních k dispozici. Ujistěte se, že jste dokončili všechny úkoly nebo akce, abyste získali vyhrazená zařízení, která vyhovují vašim přiřazeným zásadám.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte zásady dodržování předpisů](create-compliance-policy.md#create-the-policy). Jako **platformu**vyberte **Android Enterprise**.


## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Plně spravovaný, vyhrazený a podnikový pracovní profil

### <a name="microsoft-defender-atp"></a>Ochrana ATP v programu Microsoft Defender

- **Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače**  

  Vyberte maximální povolené skóre rizika počítače pro zařízení vyhodnocená ATP programu Microsoft Defender. Zařízení, která překračují toto skóre, se označí jako nedodržující předpisy.
  - **Nenakonfigurováno** (*výchozí*)
  - **Vymazat**
  - **Nízké**
  - **Medium**
  - **Vysoké**

### <a name="device-health"></a>Stav zařízení

- **Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod ní**  
  Vyberte maximální povolenou úroveň hrozby pro zařízení vyhodnocenou [službou ochrany před mobilními hrozbami](mobile-threat-defense.md). Zařízení, která přesahují tuto úroveň hrozby, se označí jako nedodržující předpisy. Pokud chcete nastavení použít, zvolte povolenou úroveň ohrožení:

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Zabezpečené** – Tato možnost je nejbezpečnější a to znamená, že zařízení nemůže mít žádné hrozby. Pokud jsou na zařízení zjištěny hrozby jakékoli úrovně, vyhodnotí se jako nevyhovující.
  - **Nízká**: zařízení se vyhodnotí jako vyhovující, pokud jsou přítomny jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.
  - **Střední** – zařízení se vyhodnotí jako vyhovující, pokud se v něm přítomné hrozby pohybují na střední nebo nízké úrovni. Pokud se u zařízení zjistí vysoká míra ohrožení, vyhodnotí se jako nevyhovující.
  - **Vysoká** – Tato možnost je nejméně bezpečná, protože umožňuje všechny úrovně hrozeb. Může být užitečná, pokud toto řešení používáte jen ke generování sestav.
  
> [!NOTE]
> Všichni poskytovatelé ochrany před mobilními hrozbami (MTD) se podporují pomocí konfigurace aplikací v rámci plně spravovaných, vyhrazených a podnikových nasazení v pracovních profilech v Androidu. U svého poskytovatele MTD se obraťte na přesnou konfiguraci, která je nutná pro podporu plně spravovaných, vyhrazených a podnikových profilů pracovních profilů pro Android v Intune.

#### <a name="google-play-protect"></a>Google Play chránit

- **Ověření zařízení SafetyNet**  
  Zadejte úroveň [ověření identity SafetyNet](https://developer.android.com/training/safetynet/attestation.html) , která musí být splněna. Možnosti:
  - **Nenakonfigurováno** (*výchozí*) – nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržení předpisů.
  - **Zkontrolovat základní integritu**
  - **Zkontrolovat základní integritu a certifikovaná zařízení**

### <a name="device-properties"></a>Vlastnosti zařízení

#### <a name="operating-system-version"></a>Verze operačního systému

- **Minimální verze operačního systému**  
  Pokud zařízení nesplňuje požadavek na minimální verzi operačního systému, nahlásí se jako nevyhovující. Zobrazí se odkaz s informacemi, jak upgradovat. Koncový uživatel může upgradovat svoje zařízení a pak získat přístup k prostředkům organizace.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

- **Maximální verze operačního systému**  
  Pokud zařízení používá verzi operačního systému, která je novější než verze v pravidle, bude přístup k prostředkům organizace blokovaný. Uživateli se zobrazí výzva, aby kontaktoval správce IT. Dokud se pravidlo nezmění, aby nedošlo k této verzi operačního systému, nebude mít toto zařízení přístup k prostředkům organizace.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

- **Minimální úroveň opravy zabezpečení**  
  Vyberte nejstarší úroveň opravy zabezpečení, kterou může zařízení mít. Zařízení, která nemají aspoň tuto úroveň opravy, nevyhovují. Datum musí být zadáno ve formátu RRRR-MM-DD.

  *Ve výchozím nastavení není nakonfigurované žádné datum*.

### <a name="system-security"></a>Zabezpečení systému

- **Vyžadovat heslo k odemknutí mobilních zařízení**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – uživatelé musí zadat heslo, aby mohli získat přístup ke svému zařízení.

- **Vyžadovaný typ hesla**  
  Vyberte, jestli má heslo obsahovat jenom číselné znaky, nebo kombinaci číslic a dalších znaků. Možnosti:
  - **Výchozí nastavení zařízení** – vyhodnotit dodržování předpisů heslem, nezapomeňte vybrat jinou sílu hesla než *výchozí zařízení*.
  - **Vyžaduje se heslo, žádná omezení.**
  - **Slabý biometrika**  -  [Silný vs. slabý biometrika](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (otevře web v Androidu)
  - **Numeric** (*výchozí*): heslo musí obsahovat jenom čísla, třeba `123456789` . Zadejte **minimální délku hesla** , kterou musí uživatel zadat, a to v rozmezí 4 až 16 znaků.
  - **Číselná komplexní** – opakující se nebo po sobě jdoucí čísla, například "1111" nebo "1234", nejsou povolena. Zadejte **minimální délku hesla** , kterou musí uživatel zadat, a to v rozmezí 4 až 16 znaků.
  - **Abecední** písmena v abecedě jsou povinná. Čísla a symboly nejsou požadovány. Zadejte **minimální délku hesla** , kterou musí uživatel zadat, a to v rozmezí 4 až 16 znaků.
  - **Alfanumerické** – obsahuje velká písmena, malá písmena a číselné znaky. Zadejte **minimální délku hesla** , kterou musí uživatel zadat, a to v rozmezí 4 až 16 znaků.
  - **Alfanumerické znaky se symboly** – obsahuje velká písmena, malá písmena, číslice, interpunkční znaménka a symboly.

  V závislosti na zvoleném *typu hesla* jsou k dispozici následující nastavení:
  - **Minimální délka hesla**  
    Zadejte minimální délku hesla, které musí mít 4 až 16 znaků.  

  - **Požadovaný počet znaků**  
    Zadejte počet znaků, které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.

  - **Počet požadovaných malých písmen**  
    Zadejte počet malých písmen, které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.

  - **Počet požadovaných velkých znaků**  
    Zadejte počet velkých písmen, které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.

  - **Počet požadovaných znaků bez písmen**  
    Zadejte počet nepísmenových znaků (cokoli kromě písmen v abecedě), které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.

  - **Počet požadovaných číselných znaků**  
    Zadejte počet číselných znaků ( `1` , `2` , `3` atd.), které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.

  - **Počet požadovaných znaků symbolů**  
    Zadejte počet znaků symbolu (,, `&` `#` `%` atd.), které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.

  - **Maximální počet minut nečinnosti před vyžadováním hesla**  
    Zadejte dobu nečinnosti, než uživatel musí znovu zadat heslo. Mezi možnosti patří výchozí hodnota *není nakonfigurovaná*a *1 minuta* až *8 hodin*.

  - **Počet dní do vypršení platnosti hesla**  
    Zadejte počet dnů od 1-365, po jehož uplynutí se musí změnit heslo zařízení. Pokud například chcete změnit heslo po 60 dnech, zadejte `60` . Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla.

    *Ve výchozím nastavení není nakonfigurována žádná hodnota*.

  - **Počet hesel vyžadovaných před opětovným použitím hesla uživatelem**  
    Zadejte počet nedávných hesel, která se nedají znovu použít, mezi 1-24. Toto nastavení použijte, pokud chcete uživateli zabránit ve vytváření hesel, která používal dříve.  

    *Ve výchozím nastavení není nakonfigurována žádná verze*.

#### <a name="encryption"></a>Šifrování

- **Šifrování datového úložiště na zařízení**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – šifrovat úložiště dat v zařízeních.

  Toto nastavení nemusíte konfigurovat, protože zařízení s Androidem Enterprise vynutila šifrování.

## <a name="work-profile"></a>Pracovní profil

### <a name="microsoft-defender-atp---for-work-profile"></a>Microsoft Defender ATP – *pro pracovní profil*

- **Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače**  
  Vyberte maximální povolené skóre rizika počítače pro zařízení vyhodnocená ATP programu Microsoft Defender. Zařízení, která překračují toto skóre, se označí jako nedodržující předpisy.
  - **Nenakonfigurováno** (*výchozí*)
  - **Vymazat**
  - **Nízké**
  - **Medium**
  - **Vysoké**

### <a name="device-health---for-work-profile"></a>Profil Stav zařízení- *for Work*

- **Zařízení s rootem**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Block** Zařízení s označením root (jailbreak) jako nevyhovující předpisům.

- **Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod ní**  
  Vyberte maximální povolenou úroveň hrozby pro zařízení vyhodnocenou [službou ochrany před mobilními hrozbami](mobile-threat-defense.md). Zařízení, která přesahují tuto úroveň hrozby, se označí jako nedodržující předpisy. Pokud chcete nastavení použít, zvolte povolenou úroveň ohrožení:
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Zabezpečené** – Tato možnost je nejbezpečnější a to znamená, že zařízení nemůže mít žádné hrozby. Pokud jsou na zařízení zjištěny hrozby jakékoli úrovně, vyhodnotí se jako nevyhovující.
  - **Nízká** – zařízení se vyhodnotí jako vyhovující, pokud jsou přítomny jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.
  - **Střední** – zařízení se vyhodnotí jako vyhovující, pokud se v něm přítomné hrozby pohybují na střední nebo nízké úrovni. Pokud se u zařízení zjistí vysoká míra ohrožení, vyhodnotí se jako nevyhovující.
  - **Vysoká** – Tato možnost je nejméně bezpečná, protože umožňuje všechny úrovně hrozeb. Může být užitečná, pokud toto řešení používáte jen ke generování sestav.

#### <a name="google-play-protect---for-work-profile"></a>Profil Google Play Protected- *for Work*

- **Aplikace Služby Google Play je nakonfigurovaná**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyžaduje, aby byla aplikace Google Play Services nainstalovaná a povolená. Aplikace Služby Google Play umožňuje instalaci aktualizací zabezpečení a je základní závislostí pro mnoho funkcí zabezpečení na zařízeních s certifikací Google.
  
- **Aktualizovaný poskytovatel zabezpečení**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyžaduje, aby aktuální poskytovatel zabezpečení chránil zařízení před známými chybami zabezpečení.
  
- **Ověření zařízení SafetyNet**  
  Zadejte úroveň [ověření identity SafetyNet](https://developer.android.com/training/safetynet/attestation.html) , která musí být splněna. Možnosti:
  - **Nenakonfigurováno** (*výchozí*) – nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržení předpisů.
  - **Zkontrolovat základní integritu**
  - **Zkontrolovat základní integritu a certifikovaná zařízení**

> [!NOTE]
> V zařízeních s Androidem Enterprise je **Kontrola hrozeb u aplikací** zásada konfigurace zařízení. Pomocí zásad konfigurace můžou správci povolit nastavení na zařízení. Další informace viz [Nastavení omezení pro zařízení s Androidem](../configuration/device-restrictions-android-for-work.md).

### <a name="device-properties---for-work-profile"></a>Vlastnosti zařízení – *profil pro práci*

#### <a name="operating-system-version---for-work-profile"></a>Verze operačního systému – *profil práce*

- **Minimální verze operačního systému**  
Pokud zařízení nesplňuje požadavek na minimální verzi operačního systému, nahlásí se jako nevyhovující. Zobrazí se odkaz s informacemi, jak upgradovat. Koncový uživatel může upgradovat svoje zařízení a pak získat přístup k prostředkům organizace.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

- **Maximální verze operačního systému**  
Pokud zařízení používá verzi operačního systému, která je novější než verze v pravidle, bude přístup k prostředkům organizace blokovaný. Uživateli se zobrazí výzva, aby kontaktoval správce IT. Dokud se pravidlo nezmění, aby nedošlo k této verzi operačního systému, nebude mít toto zařízení přístup k prostředkům organizace.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

### <a name="system-security---for-work-profile"></a>Zabezpečení systému – *pracovní profil*

- **Vyžadovat heslo k odemknutí mobilních zařízení**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – uživatelé musí zadat heslo, aby mohli získat přístup ke svému zařízení.  

  Toto nastavení platí na úrovni zařízení. Pokud potřebujete vyžadovat heslo na úrovni pracovního profilu, použijte zásady konfigurace. Viz [nastavení konfigurace zařízení s Androidem Enterprise](../configuration/device-restrictions-android-for-work.md).

- **Vyžadovaný typ hesla**  
  Vyberte, jestli má heslo obsahovat jenom číselné znaky, nebo kombinaci číslic a dalších znaků. Možnosti:
  - **Výchozí nastavení zařízení**
  - **Biometrika s nízkým zabezpečením**
  - **Aspoň číslice** (*výchozí*): zadejte **minimální délku hesla** , kterou musí uživatel zadat, o délce 4 až 16 znaků.
  - **Číselná složitá**: zadejte **minimální délku hesla** , kterou musí uživatel zadat, a to v rozmezí 4 až 16 znaků.
  - **Aspoň abecední**: zadejte **minimální délku hesla** , kterou musí uživatel zadat, a to v rozmezí 4 až 16 znaků.
  - **Aspoň alfanumerické**: zadejte **minimální délku hesla** , kterou musí uživatel zadat, o délce 4 až 16 znaků.
  - **Aspoň alfanumerické se symboly**: zadejte **minimální délku hesla** , kterou musí uživatel zadat, o délce 4 až 16 znaků.

  V závislosti na zvoleném *typu hesla* jsou k dispozici následující nastavení:

  - **Maximální počet minut nečinnosti před vyžadováním hesla**  
    Zadejte dobu nečinnosti, než uživatel musí znovu zadat heslo. Mezi možnosti patří výchozí hodnota *není nakonfigurovaná*a *1 minuta* až *8 hodin*.

  - **Počet dní do vypršení platnosti hesla**  
    Zadejte počet dnů od 1-365, po jehož uplynutí se musí změnit heslo zařízení. Pokud například chcete změnit heslo po 60 dnech, zadejte `60` . Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla.

  - **Minimální délka hesla**  
    Zadejte minimální délku hesla, které musí mít 4 až 16 znaků.

  - **Počet předchozích hesel, která zabrání opakovanému použití**  
    Zadejte počet nedávných hesel, která se nedají znovu použít. Toto nastavení použijte, pokud chcete uživateli zabránit ve vytváření hesel, která používal dříve.

#### <a name="encryption---for-work-profile"></a>Šifrování – *profil pro práci*

- **Šifrování datového úložiště na zařízení**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – šifrovat úložiště dat v zařízeních.  

  Toto nastavení nemusíte konfigurovat, protože zařízení s Androidem Enterprise vynutila šifrování.

#### <a name="device-security---for-work-profile"></a>Zabezpečení zařízení – *profil pro práci*

- **Blokovat aplikace z neznámých zdrojů**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Blokové** zařízení s **Security**  >  povolenými zdroji zabezpečení**neznámými zdroji** (*podporované v Androidu 4,0 až Android 7. x. Nepodporováno Androidem 8,0 a novějším*.  

  Pokud chcete instalovat aplikace bokem, musí být povoleny neznámé zdroje. Pokud aplikace pro Android neinstalujete bokem, nastavte tuto funkci na **Blokovat**, abyste tuto zásadu dodržování předpisů povolili.

  > [!IMPORTANT]
  > Aplikace instalované bokem vyžadují, aby bylo povolené nastavení **Blokovat aplikace z neznámých zdrojů**. Na dodržení této zásady trvejte jenom v případě, že na zařízeních neprovádíte instalaci aplikací pro Android bokem.

  Toto nastavení nemusíte konfigurovat, protože zařízení se systémem Android Enterprise vždy omezují instalaci z neznámých zdrojů.

- **Integrita modulu runtime aplikace Portál společnosti**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyberte *vyžadovat* a potvrďte, že aplikace Portál společnosti splňuje všechny následující požadavky:
    - Má nainstalované výchozí prostředí modulu runtime.
    - Je řádně podepsaná.
    - Není v režimu ladění.
    - Je nainstalovaná ze známého zdroje.

- **Blokovat na zařízení ladění USB**  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Blok** – zabraňuje zařízením používat funkci ladění USB.  

  Toto nastavení nemusíte konfigurovat, protože ladění USB je už na zařízeních s Androidem Enterprise zakázané.

- **Minimální úroveň opravy zabezpečení**  
  Vyberte nejstarší úroveň opravy zabezpečení, kterou může zařízení mít. Zařízení, která nemají aspoň tuto úroveň opravy, nevyhovují. Datum musí být zadáno ve formátu RRRR-MM-DD.

  *Ve výchozím nastavení není nakonfigurované žádné datum*.

## <a name="next-steps"></a>Další kroky

- [Přidejte akce pro zařízení nedodržující předpisy](actions-for-noncompliance.md) a [použijte značky oboru k filtrování zásad](../fundamentals/scope-tags.md).
- [Monitorujte zásady dodržování předpisů](compliance-policy-monitor.md).
- Podívejte se na [nastavení zásad dodržování předpisů pro zařízení s Androidem](compliance-policy-create-android.md) .
