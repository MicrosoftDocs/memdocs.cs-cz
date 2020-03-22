---
title: Přizpůsobení aplikací Portál společnosti Intune, Portál společnosti webu a Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak můžete použít branding pro konkrétní společnosti pro aplikace Portál společnosti Intune, Portál společnosti web a Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/16/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1ec6d4ebe860a1c20ad1a11bd7e63086858a82c
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084211"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Přizpůsobení aplikací Portál společnosti Intune, Portál společnosti webu a Intune

Aplikace Portál společnosti, Portál společnosti web a Intune v Androidu jsou místo, kde uživatelé přistupují k podnikovým datům a můžou provádět běžné úkoly. Běžný úkol může zahrnovat registraci zařízení, instalaci aplikací a hledání informací (například pomoc z vašeho oddělení IT). Kromě toho umožňují uživatelům zabezpečený přístup k prostředkům společnosti. Činnost koncového uživatele poskytuje několik různých stránek, jako jsou domů, aplikace, podrobnosti o aplikaci, zařízení a podrobnosti o zařízení. K rychlému vyhledání aplikací v rámci Portál společnosti můžete aplikace filtrovat na stránce aplikace.

## <a name="customizing-the-user-experience"></a>Přizpůsobení uživatelského prostředí

Přizpůsobením prostředí pro koncové uživatele umožníte vašim koncovým uživatelům získat známé a užitečné možnosti. Provedete to tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberete **Správa tenanta** > **přizpůsobení**a pak nakonfigurujete požadovaná nastavení. Tato nastavení se použijí pro aplikace Portál společnosti, Portál společnosti webu a Intune v Androidu.

## <a name="branding"></a>Branding

Následující tabulka uvádí podrobnosti přizpůsobení značky pro činnost koncového uživatele:

| Název pole | Další informace |
|---|---|---|
| **Název organizace** | Tento název se zobrazí v rámci zasílání zpráv v prostředí koncového uživatele. Můžete ji nastavit tak, aby se zobrazila v hlavičkách i v nastavení **Zobrazit v hlavičce** . Maximální délka je 40 znaků. |
| **Barevných** | Vyberte možnost **Standard** pro výběr z pěti standardních barev. Zvolte **vlastní** pro výběr konkrétní barvy na základě hexadecimální hodnoty kódu. |
| **Barva motivu** | Nastavením barvy motivu zobrazíte činnost koncového uživatele. Barva textu automaticky nastavíme na černou nebo bílou, aby se zobrazila nad vybranou barvou motivu. |
| **Zobrazit v záhlaví** | Vyberte, jestli má záhlaví v prostředí koncových uživatelů zobrazovat **logo a název společnosti**, **jenom logo společnosti**, nebo **jenom název společnosti**. Níže uvedená pole pro náhled budou zobrazovat pouze loga, nikoli název.  |
| **Nahrát logo pro barvu motivu na pozadí** | Nahrajte logo, které chcete zobrazit, nad vybranou barvou motivu. Pro nejlepší vzhled nahrajte logo s průhledným pozadím. Uvidíte, jak se bude zobrazovat v poli Náhled pod nastavením.<p>Maximální velikost obrázku: 400 × 400 px<br>Maximální velikost souboru: 750 KB<br>Typ souboru: PNG, JPG nebo JPEG |
| **Nahrát logo pro bílé nebo světlé pozadí** | Nahrajte logo, které chcete zobrazit na bílých nebo lehkých pozadích. Pro nejlepší vzhled nahrajte logo s průhledným pozadím. Můžete vidět, jak se bude zobrazovat na bílém pozadí v poli Náhled pod nastavením.<p>Maximální velikost obrázku: 400 × 400 px<br>Maximální velikost souboru: 750 kB<br>Typ souboru: PNG, JPG nebo JPEG |
| **Nahrát obrázek značky** | Nahrajte obrázek, který odráží značku vaší organizace.<p><ul><li>Doporučená šířka obrázku: větší než 1125 px (musí být aspoň 650 px)</li><li>Maximální velikost obrázku: 1,3 MB</li><li>Typ souboru: PNG, JPG nebo JPEG</li><li>Zobrazuje se v těchto umístěních:</li><ul><li>iOS/iPadOS Portál společnosti: obrázek na pozadí na stránce profilu uživatele.</li><li>Portál společnosti web: obrázek na pozadí na stránce profilu uživatele.</li><li>Aplikace Intune pro Android: v zásuvce a jako obrázek na pozadí na stránce profilu uživatele.</li></ul></ul> |

> [!NOTE]
> Když uživatel instaluje aplikaci pro iOS/iPadOS z Portál společnosti, zobrazí se výzva. K tomu dochází, když je aplikace pro iOS/iPadOS propojená s obchodem s aplikacemi, která je propojená s programem Volume purchase program (VPP), nebo propojená s obchodní aplikací (LOB). Tato výzva umožní uživatelům přijmout akci nebo povolit správu aplikace. Výzva zobrazí název vaší společnosti, nebo pokud název vaší společnosti není k dispozici, zobrazí se **portál společnosti** .

### <a name="brand-image-best-practices"></a>Osvědčené postupy pro obrázky značky

Správný obrázek značky může vylepšit důvěryhodnost uživatele tím, že prezentuje silný smysl značky vaší organizace. Tady je několik tipů, které můžete zvážit pro získání, výběr a optimalizaci obrázku pro zobrazovaná místa.

- Obraťte se na marketingové nebo kreativní oddělení. Můžou už mít schválenou sadu imagí značky. Mohli by vám také pomoci při optimalizaci obrázků.
- Zvažte kompozici v orientaci jak na šířku, tak i na výšku. Ústřední bod obrázku by mělo obklopovat dostatečně velké pozadí. Obrázek může být oříznutý odlišně na základě velikosti zařízení, orientace a platformy.
- Nepoužívejte obecné obrázky převzaté z fotobanky. Image by měla odrážet značku vaší organizace a znát uživatele. Pokud žádný obrázek nemáte, je lepší nepoužívat žádný, než použít obecný, který pro uživatele nemá žádný význam.
- Odeberte nepotřebná metadata. Soubor obrázku může obsahovat metadata, jako jsou profil fotoaparátu, zeměpisná poloha, název, popisek a další. Pomocí nástroje pro optimalizaci obrázků tyto informace odstraňte, abyste zachovali kvalitu, ale vešli se do velikostního limitu souboru.

### <a name="brand-image-examples"></a>Příklady obrázků značky

Následující obrázek ukazuje příklad obrázku značky na iPhonu:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

Níže vidíte příklad obrázku značky v aplikaci Intune pro Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Informace o podpoře

Zadejte informace o podpoře vaší organizace, aby se zaměstnanci mohli obrátit na otázky. Tyto informace o podpoře se budou zobrazovat na **podporu**, **pomáhat & podpoře**a stránkách **helpdesku** v rámci prostředí koncových uživatelů.

| Název pole | Maximální délka | Další informace |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Jméno kontaktu | 40 | Tento název se bude uživatelům přistihnout při kontaktování podpory. |
| Telefonní číslo | 20 | Toto číslo umožňuje uživatelům zavolat na podporu. |
| E-mailová adresa | 40 | Tato e-mailová adresa umožňuje uživatelům odesílat e-maily pro podporu. Je potřeba zadat platnou e-mailovou adresu ve formátu `alias@domainname.com`. |
| Název webu | 40 | Toto je popisný název, který se zobrazí v některých umístěních pro adresu URL webu podpory. Pokud zadáte adresu URL webu podpory bez popisného názvu, zobrazí se tato adresa URL v prostředí koncového uživatele.  |
| Adresa URL webu | 150 | Web podpory, který uživatelé mají použít. Adresa URL musí být ve formátu `https://www.contoso.com`.  |
| Další informace | 120 | Sem Zahrňte všechny další zprávy týkající se podpory pro uživatele. |

## <a name="configuration"></a>Konfigurace

Následující tabulka poskytuje další podrobnosti o konfiguraci:

| Název pole | Maximální délka | Další informace |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Adresa URL prohlášení o zásadách ochrany osobních údajů | 79 | Nastavte prohlášení o zásadách ochrany osobních údajů ve vaší organizaci, které se zobrazí, když uživatel klikne na odkazy na soukromí Musíte zadat platnou adresu URL ve formátu `https://www.contoso.com`. |
| Zpráva o ochraně osobních údajů v Portál společnosti pro iOS/iPadOS | 520 | Ponechte výchozí nebo nastavte vlastní zprávu tak, aby vynechala seznam položek, které vaše organizace může nebo nemůže zobrazit na spravovaných zařízeních se systémem iOS/iPadOS. Pomocí Markdownu můžete přidat odrážky, tučné písmo, kurzívu a odkazy. |
| Registrace zařízení | NEUŽÍVÁ SE. | Určete, jestli a jak se má uživatelům zobrazit výzva k registraci do správy mobilních zařízení. Podrobnosti níže. |

### <a name="device-enrollment-setting-options"></a>Možnosti nastavení registrace zařízení

> [!NOTE]
> Podpora nastavení registrace zařízení vyžaduje, aby koncoví uživatelé měli tyto Portál společnosti verze:
> - Portál společnosti v systému iOS/iPadOS: verze 4,4 nebo novější
> - Portál společnosti na Androidu: verze 5.0.4715.0 nebo novější 

|    Možnosti registrace zařízení    |    Popis    |    Výzvy kontrolního seznamu    |    Oznámení    |    Stav podrobnosti o zařízení    |    Podrobnosti o stavu aplikace (aplikace, která vyžaduje registraci)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    K dispozici, s výzvami    |    Výchozí prostředí s výzvou k registraci ve všech možných umístěních.    |    Ano    |    Ano    |    Ano    |    Ano    |
|    K dispozici, žádné výzvy    |    Uživatel se může zaregistrovat přes stav v podrobnostech o zařízení pro svoje aktuální zařízení nebo aplikace, které vyžadují registraci.    |    Ne    |    Ne    |    Ano    |    Ano    |
|    Nedostupný    |    Pro uživatele neexistuje žádný způsob, jak ho zaregistrovat.    |    Ne    |    Ne    |    Ne    |    Ne<sup>(1)</sup>    |

<sup>(1)</sup> **známý problém:** Pokud nakonfigurujete aplikace, aby vyžadovaly registraci pro instalaci, a také nastavení registrace zařízení na "nedostupné", aplikace Portál společnosti v Androidu pořád budou uživatele registrovat. Tato akce bude brzy odebrána.

> [!NOTE]
> Pokud používáte Azure Government, nabízí se protokoly aplikace koncovým uživatelům, aby se rozhodli o způsobu sdílení po inicializaci procesu získání pomoci s problémem. Pokud však Azure Government nepoužíváte, Portál společnosti pošle protokoly aplikací přímo společnosti Microsoft, když uživatel zahájí proces, aby získal pomoc s problémem. Odesílání protokolů aplikace do Microsoftu usnadní řešení problémů.

> [!NOTE]
> V souladu se zásadami Microsoftu a Apple nebudeme z jakéhokoli důvodu prodávat žádná data shromážděná naší službou žádným třetím stranám.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Portál společnosti odvozené přihlašovací údaje pro zařízení s iOS/iPadOS

Intune podporuje ověřování osobních identit (PIV) a služby Common Access Card (CAC) odvozené přihlašovací údaje v partnerství s poskytovateli přihlašovacích údajů DISA purebred, Entrust Datacard a Intercede. Koncoví uživatelé procházejí dalšími kroky po registraci zařízení s iOS/iPadOS a ověřují jejich identitu v aplikaci Portál společnosti. Odvozená pověření budou pro uživatele povolena tím, že nejprve nastaví poskytovatele pověření pro vašeho tenanta a pak zacílíte na profil, který používá odvozená pověření pro uživatele nebo zařízení.

> [!NOTE]
> Uživateli se zobrazí pokyny k odvozeným přihlašovacím údajům na základě odkazu, který jste zadali přes Intune.

Další informace o odvozených přihlašovacích údajích pro zařízení s iOS/iPadOS najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-iosipados-company-portal"></a>Tmavý režim pro iOS/iPadOS Portál společnosti

Pro iOS/iPadOS Portál společnosti je k dispozici tmavý režim. Uživatelé můžou stahovat aplikace, spravovat jejich zařízení a získávat v nich podporu v barevném schématu podle nastavení zařízení. Portál společnosti iOS/iPadOS bude automaticky odpovídat nastavení zařízení koncového uživatele pro tmavý nebo lehký režim.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Klávesové zkratky v Portálu společnosti pro Windows

Koncoví uživatelé mohou aktivovat akce navigace, aplikace a zařízení ve Windows Portál společnosti pomocí klávesových zkratek (akcelerátory).

V aplikaci Portál společnosti pro Windows jsou k dispozici následující klávesové zkratky.

| Plošný | Popis | Klávesová zkratka |
|:------------------:|:--------------:|:-----------------:|
| Navigační nabídka | Navigace | ALT + M |
|  | Domů | ALT + H |
|  | Všechny aplikace | ALT + A |
|  | Nainstalované aplikace | Alt+I |
|  | Váš názor | ALT + F |
|  | Můj profil | ALT + U |
|  | Nastavení | Alt + T |
| Úvodní stránka – dlaždice Zařízení | Přejmenovat | F2 |
|  | Odebrat | Ctrl+D nebo Delete |
|  | Zkontrolovat přístup | Ctrl+M nebo F9 |
| Podrobnosti zařízení | Přejmenovat | F2 |
|  | Odebrat | Ctrl+D nebo Delete |
|  | Zkontrolovat přístup | Ctrl+M nebo F9 |
| Podrobnosti aplikace | Nainstalovat | Ctrl+I |
| Zařízení | K dispozici | CTRL+D |

Koncoví uživatelé budou také moci zobrazit dostupné zkratky v aplikaci pro Windows Portál společnosti.

![Snímek obrazovky s dostupnými zástupci ve Windows Portál společnosti](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Akce zařízení Samoobslužná služba uživatele z Portál společnosti

Uživatelé můžou na svých místních nebo vzdálených zařízeních provádět akce pomocí Portál společnosti aplikace nebo webu nebo aplikace Intune v Androidu. Akce, které může uživatel provádět, se liší v závislosti na platformě a konfiguraci zařízení. Ve všech případech můžou akce se vzdáleným zařízením provádět jenom primární uživatel zařízení.

- **Vyřadit** – odebere zařízení ze správy Intune. V aplikaci Portál společnosti a na webu se zobrazuje jako **Remove (odebrat**).
- **Vymazat** – Tato akce zahájí resetování zařízení. Na webu portál společnosti se zobrazuje jako **resetování**nebo **obnovení továrního nastavení** v aplikaci pro iOS/iPadOS portál společnosti.
- **Přejmenovat** – Tato akce změní název zařízení, které může uživatel vidět v portál společnosti. Nemění název místního zařízení, pouze výpis v Portál společnosti.
- **Synchronizovat** – Tato akce zahájí vrácení se změnami zařízení se službou Intune. Zobrazí se jako **stav kontroly** v portál společnosti.
- **Remote Lock** – zablokuje zařízení a vyžaduje ho k odemknutí.
- **Resetování hesla** – Tato akce se používá k resetování hesla zařízení. V zařízeních se systémem iOS/iPadOS bude heslo odebráno a koncový uživatel bude muset zadat nový kód v nastavení. V podporovaných zařízeních s Androidem Intune vygeneruje nové heslo a dočasně se zobrazí v Portál společnosti.
- **Obnovení klíčů** – Tato akce se používá k obnovení osobního obnovovacího klíče pro šifrovaná zařízení MacOS z webu portál společnosti. 

### <a name="self-service-actions"></a>Akce samoobslužných služeb

Některé platformy a konfigurace neumožňují akce zařízení samoobslužné služby. V této tabulce najdete další podrobnosti o akcích samoobslužných služeb:

|  | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Vyřadit | K dispozici<sup>(1)</sup> | K dispozici | K dispozici | K dispozici<sup>(7)</sup> |
| Vymazání | K dispozici | K dispozici<sup>(5)</sup> | Není k dispozici | K dispozici<sup>(7)</sup> |
| Přejmenovat<sup>(4)</sup> | K dispozici | K dispozici | K dispozici | K dispozici |
| Synchronizovat | K dispozici | K dispozici | K dispozici | K dispozici |
| Vzdálené uzamčení | Pouze Windows Phone | K dispozici | K dispozici | K dispozici |
| Resetovat heslo | Pouze Windows Phone | K dispozici<sup>(8)</sup> | Není k dispozici | K dispozici<sup>(6)</sup> |
| Obnovení klíče | Není k dispozici | Není k dispozici | K dispozici<sup>(2)</sup> | Není k dispozici |

<sup>(1)</sup> **vyřazení** je vždycky blokované na zařízeních s Windows připojená k Azure AD.<br>
<sup>(2)</sup> **obnovení klíče** pro MacOS je dostupné jenom přes webový portál.<br>
<sup>(3)</sup> Pokud používáte registraci správce registrace zařízení, jsou všechny vzdálené akce zakázané.<br>
<sup>(4)</sup> **přejmenování** změní pouze název zařízení v portál společnosti aplikaci nebo webovém portálu, nikoli na zařízení.<br>
<sup>(5)</sup> **vymazání** není k dispozici pro uživatele zaregistrovaná zařízení se systémem iOS/iPadOS.<br>
<sup>(6)</sup> **resetování hesla** není podporované u některých konfigurací pro Android a Android Enterprise. Další informace najdete v tématu [resetování nebo odebrání hesla zařízení v Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> **vyřazení** a **vymazání** nejsou k dispozici ve scénářích pro vlastníky zařízení s Androidem Enterprise (odolat, Cobo, COSU).<br> 
<sup>(8)</sup> **resetování hesla** není podporované uživatelem zaregistrovanými zařízeními iOS/iPadOS.

## <a name="next-steps"></a>Další kroky

- [Ruční přidání aplikace Portál společnosti pro Windows 10 pomocí Microsoft Intune](company-portal-app.md)