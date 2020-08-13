---
title: Přizpůsobení aplikací Portál společnosti Intune, Portál společnosti webu a Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak můžete použít branding pro konkrétní společnosti pro aplikace Portál společnosti Intune, Portál společnosti web a Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
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
ms.openlocfilehash: a82fbfa9e494828450729e29467580c29a590282
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179549"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Přizpůsobení aplikací Portál společnosti Intune, Portál společnosti webu a Intune

Aplikace Portál společnosti, Portál společnosti web a Intune v Androidu jsou místo, kde uživatelé přistupují k podnikovým datům a můžou provádět běžné úkoly. Běžný úkol může zahrnovat registraci zařízení, instalaci aplikací a hledání informací (například pomoc z vašeho oddělení IT). Kromě toho umožňují uživatelům zabezpečený přístup k prostředkům společnosti. Činnost koncového uživatele poskytuje několik různých stránek, jako jsou domů, aplikace, podrobnosti o aplikaci, zařízení a podrobnosti o zařízení. K rychlému vyhledání aplikací v rámci Portál společnosti můžete aplikace filtrovat na stránce aplikace.

## <a name="customizing-the-user-experience"></a>Přizpůsobení uživatelského prostředí

Přizpůsobením prostředí pro koncové uživatele umožníte vašim koncovým uživatelům získat známé a užitečné možnosti. Provedete to tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberete přizpůsobení **správy tenanta**  >  **Customization**, kde můžete buď upravit výchozí zásadu, nebo vytvořit až 10 cílových zásad skupiny. Tato nastavení se použijí pro aplikace Portál společnosti, Portál společnosti webu a Intune v Androidu.

## <a name="branding"></a>Značka

Následující tabulka uvádí podrobnosti přizpůsobení značky pro činnost koncového uživatele:

| Název pole | Další informace |
|---|---|---|
| **Název organizace** | Tento název se zobrazí v rámci zasílání zpráv v prostředí koncového uživatele. Můžete ji nastavit tak, aby se zobrazila v hlavičkách i v nastavení **Zobrazit v hlavičce** . Maximální délka je 40 znaků. |
| **Color** | Vyberte možnost **Standard** pro výběr z pěti standardních barev. Zvolte **vlastní** pro výběr konkrétní barvy na základě hexadecimální hodnoty kódu. |
| **Barva motivu** | Nastavením barvy motivu zobrazíte činnost koncového uživatele. Barva textu automaticky nastavíme na černou nebo bílou, aby se zobrazila nad vybranou barvou motivu. |
| **Zobrazit v záhlaví** | Vyberte, jestli má záhlaví v prostředí koncových uživatelů zobrazovat **logo a název organizace**, **jenom logo organizace**nebo **název organizace**. Níže uvedená pole pro náhled budou zobrazovat pouze loga, nikoli název.  |
| **Nahrát logo pro barvu motivu na pozadí** | Nahrajte logo, které chcete zobrazit, nad vybranou barvou motivu. Pro nejlepší vzhled nahrajte logo s průhledným pozadím. Uvidíte, jak se bude zobrazovat v poli Náhled pod nastavením.<p>Maximální velikost obrázku: 400 × 400 px<br>Maximální velikost souboru: 750 KB<br>Typ souboru: PNG, JPG nebo JPEG |
| **Nahrát logo pro bílé nebo světlé pozadí** | Nahrajte logo, které chcete zobrazit na bílých nebo lehkých pozadích. Pro nejlepší vzhled nahrajte logo s průhledným pozadím. Můžete vidět, jak se bude zobrazovat na bílém pozadí v poli Náhled pod nastavením.<p>Maximální velikost obrázku: 400 × 400 px<br>Maximální velikost souboru: 750 kB<br>Typ souboru: PNG, JPG nebo JPEG |
| **Nahrát obrázek značky** | Nahrajte obrázek, který odráží značku vaší organizace.<p><ul><li>Doporučená šířka obrázku: větší než 1125 px (musí být aspoň 650 px)</li><li>Maximální velikost obrázku: 1,3 MB</li><li>Typ souboru: PNG, JPG nebo JPEG</li><li>Zobrazuje se v těchto umístěních:</li><ul><li>iOS/iPadOS Portál společnosti: obrázek na pozadí na stránce profilu uživatele.</li><li>Portál společnosti web: obrázek na pozadí na stránce profilu uživatele.</li><li>Aplikace Intune pro Android: v zásuvce a jako obrázek na pozadí na stránce profilu uživatele.</li></ul></ul> |

> [!NOTE]
> Když uživatel instaluje aplikaci pro iOS/iPadOS z Portál společnosti, zobrazí se výzva. K tomu dochází, když je aplikace pro iOS/iPadOS propojená s obchodem s aplikacemi, která je propojená s programem Volume purchase program (VPP), nebo propojená s obchodní aplikací (LOB). Tato výzva umožní uživatelům přijmout akci nebo povolit správu aplikace. Výzva zobrazí název vaší společnosti, nebo pokud název vaší společnosti není k dispozici, zobrazí se **portál společnosti** .

### <a name="brand-image-best-practices"></a>Osvědčené postupy pro obrázky značky

Správný obrázek značky může vylepšit důvěryhodnost uživatele tím, že prezentuje silný smysl značky vaší organizace. Tady je několik tipů, které můžete zvážit pro získání, výběr a optimalizaci obrázku pro zobrazovaná místa.

- Obraťte se na marketingové nebo kreativní oddělení. Můžou už mít schválenou sadu imagí značky. Mohli by vám také pomoci při optimalizaci obrázků.
- Zvažte kompozici v orientaci jak na šířku, tak i na výšku. Ústřední bod obrázku by mělo obklopovat dostatečně velké pozadí. Obrázek může být oříznutý odlišně na základě velikosti zařízení, orientace a platformy.
- Nepoužívejte obecné obrázky převzaté z fotobanky. Image by měla odrážet značku vaší organizace a znát uživatele. Pokud ho ještě nemáte, je lepší nepoužívat ho, než použijte obecný, který nemá žádný význam pro uživatele.
- Odeberte nepotřebná metadata. Soubor obrázku může obsahovat metadata, jako jsou profil fotoaparátu, zeměpisná poloha, název, popisek a další. Pomocí nástroje pro optimalizaci obrázků tyto informace odstraňte, abyste zachovali kvalitu, ale vešli se do velikostního limitu souboru.

### <a name="brand-image-examples"></a>Příklady obrázků značky

Následující obrázek ukazuje příklad obrázku značky na iPhonu:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

Níže vidíte příklad obrázku značky v aplikaci Intune pro Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Informace pro získání podpory

Zadejte informace o podpoře vaší organizace, aby se zaměstnanci mohli obrátit na otázky. Tyto informace o podpoře se budou zobrazovat na **podporu**, **pomáhat & podpoře**a stránkách **helpdesku** v rámci prostředí koncových uživatelů.

| Název pole | Maximální délka | Další informace |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Jméno kontaktu | 40 | Tento název se bude uživatelům přistihnout při kontaktování podpory. |
| Telefonní číslo | 20 | Toto číslo umožňuje uživatelům zavolat na podporu. |
| E-mailová adresa | 40 | Tato e-mailová adresa umožňuje uživatelům odesílat e-maily pro podporu. Je potřeba zadat platnou e-mailovou adresu ve formátu `alias@domainname.com`. |
| Název webu | 40 | Toto je popisný název, který se zobrazí v některých umístěních pro adresu URL webu podpory. Pokud zadáte adresu URL webu podpory bez popisného názvu, zobrazí se tato adresa URL v prostředí koncového uživatele.  |
| Adresa URL webu | 150 | Web podpory, který uživatelé mají použít. Adresa URL musí být ve formátu `https://www.contoso.com` .  |
| Další informace | 120 | Sem Zahrňte všechny další zprávy týkající se podpory pro uživatele. |

## <a name="configuration"></a>Konfigurace

Můžete nakonfigurovat prostředí Portál společnosti specificky pro registraci, ochranu osobních údajů, oznámení, zdroje aplikací a akce samoobslužných služeb.

### <a name="enrollment"></a>Registrace

Následující tabulka uvádí podrobnosti konfigurace specifické pro registraci:

| Název pole | Maximální délka | Další informace |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Registrace zařízení | – | Určete, jestli a jak se má uživatelům zobrazit výzva k registraci do správy mobilních zařízení. Další informace najdete v tématu [Možnosti nastavení registrace zařízení](../apps/company-portal-app.md#device-enrollment-setting-options). |

#### <a name="device-enrollment-setting-options"></a>Možnosti nastavení registrace zařízení

> [!NOTE]
> Podpora nastavení registrace zařízení vyžaduje, aby koncoví uživatelé měli tyto Portál společnosti verze:
> - Portál společnosti v systému iOS/iPadOS: verze 4,4 nebo novější
> - Portál společnosti na Androidu: verze 5.0.4715.0 nebo novější 

> [!IMPORTANT]
> Následující nastavení se nevztahují na zařízení s iOS/iPadOS konfigurovaná pro registraci pomocí [automatizované registrace zařízení](../enrollment/device-enrollment-program-enroll-ios.md). Bez ohledu na to, jak jsou tato nastavení nakonfigurovaná, se zařízení se systémem iOS/iPadOS nakonfigurovaná k registraci pomocí automatizované registrace zařízení zaregistrují během natékání toku a uživatelé budou vyzváni k přihlášení při spuštění Portál společnosti.
> 
> Následující nastavení platí pro zařízení s Androidem nakonfigurovaná pomocí [zápisu na mobilních zařízeních Samsung KNOX](../enrollment/android-samsung-knox-mobile-enroll.md) (KME). Pokud je zařízení nakonfigurované pro KME a registrace zařízení je nastavená na nedostupné, zařízení se nebude moct zaregistrovat během toku mimo box.

|    Možnosti registrace zařízení    |    Description    |    Výzvy kontrolního seznamu    |    Notification (Oznámení)    |    Stav podrobnosti o zařízení    |    Podrobnosti o stavu aplikace (aplikace, která vyžaduje registraci)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    K dispozici, s výzvami    |    Výchozí prostředí s výzvou k registraci ve všech možných umístěních.    |    Ano    |    Ano    |    Ano    |    Ano    |
|    K dispozici, žádné výzvy    |    Uživatel se může zaregistrovat přes stav v podrobnostech o zařízení pro svoje aktuální zařízení nebo aplikace, které vyžadují registraci.    |    Ne    |    Ne    |    Ano    |    Ano    |
|    Neaktivní    |    Pro uživatele neexistuje žádný způsob, jak ho zaregistrovat.    |    Ne    |    Ne    |    Ne    |    Ne    |

### <a name="privacy"></a>Ochrana osobních údajů

V následující tabulce jsou uvedeny podrobnosti o konfiguraci specifické pro ochranu osobních údajů:

| Název pole | Maximální délka | Další informace |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Adresa URL prohlášení o zásadách ochrany osobních údajů | 79 | Nastavte prohlášení o zásadách ochrany osobních údajů ve vaší organizaci, které se zobrazí, když uživatel klikne na odkazy na soukromí Musíte zadat platnou adresu URL ve formátu `https://www.contoso.com`. |
| Zpráva o ochraně osobních údajů v Portál společnosti pro iOS/iPadOS | 520 | Ponechte **výchozí** nebo nastavte **vlastní** zprávu a seznam položek, které vaše organizace nemůže zobrazit na spravovaných zařízeních se systémem iOS/iPadOS. Pomocí Markdownu můžete přidat odrážky, tučné písmo, kurzívu a odkazy. Uživatelům se zobrazí také seznam věcí, které vaše organizace může zobrazit a dělat, ale tento seznam se automaticky vygeneruje pomocí Intune a nedá se přizpůsobit. |

### <a name="device-ownership-notification"></a>Oznámení o vlastnictví zařízení

Následující tabulka uvádí podrobnosti konfigurace konkrétního oznámení:

| Název pole | Maximální délka | Další informace |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Odeslání nabízených oznámení uživatelům, když se jejich typ vlastnictví zařízení změní z osobní na firemní (jenom Android a iOS/iPadOS) | – | Odeslání nabízeného oznámení do uživatelů pro Android i iOS Portál společnosti, když se jejich typ vlastnictví zařízení změnil z osobních na firemní. Ve výchozím nastavení je toto nabízené oznámení nastaveno na vypnuto. Když je vlastnictví zařízení nastavené na vlastnictví firmy, má Intune větší přístup k zařízení, které zahrnuje plný inventář aplikací, rotaci klíčů trezoru souborů, načtení telefonního čísla a několik vzdálených akcí. Další informace najdete v tématu [Změna vlastnictví zařízení](../enrollment/corporate-identifiers-add.md#change-device-ownership).  |

### <a name="app-sources"></a>Zdroje aplikací

Můžete zvolit, které další zdroje aplikací se budou zobrazovat v Portál společnosti. Následující tabulka uvádí podrobnosti konfigurace specifické pro zdroj aplikace:

| Název pole | Maximální délka | Další informace |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Podnikové aplikace Azure AD | – | Vyberte **Skrýt** nebo **Zobrazit** pro zobrazení **podnikových aplikací Azure AD** v portál společnosti pro každého koncového uživatele. Další informace najdete v tématu [Možnosti nastavení zdroje aplikace](../apps/company-portal-app.md#app-source-setting-options). |
| Aplikace Office Online | – | Vyberte možnost **Skrýt** nebo **Zobrazit** pro zobrazení **online aplikací Office** v portál společnosti pro každého koncového uživatele. Další informace najdete v tématu [Možnosti nastavení zdroje aplikace](../apps/company-portal-app.md#app-source-setting-options). |

#### <a name="app-source-setting-options"></a>Možnosti nastavení zdroje aplikace

> [!NOTE]
> Web Portál společnosti začne na začátku podporovat zobrazování aplikací z jiných služeb Microsoftu.

Pro každého koncového uživatele můžete skrýt nebo zobrazit **aplikace Azure AD Enterprise** a **aplikace Office Online** v portál společnosti. Možnost **Zobrazit** způsobí, že portál společnosti zobrazí celý katalog aplikací od vybraných služeb společnosti Microsoft přiřazených uživateli. **Podnikové aplikace Azure AD** se registrují a přiřazují prostřednictvím [Azure Portal](https://portal.azure.com). **Aplikace Office Online** se přiřazují pomocí řídicích mechanismů licencování dostupných v [centru pro správu M365](https://admin.microsoft.com). V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **přizpůsobení správy tenanta**  >  **Customization** a najděte toto nastavení konfigurace. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. 

### <a name="customizing-user-self-service-actions-for-the-company-portal"></a>Přizpůsobení samoobslužných akcí uživatele pro Portál společnosti

Můžete přizpůsobit dostupné akce samoobslužného zařízení, které se zobrazí koncovým uživatelům v aplikaci Portál společnosti a na webu. Aby se zabránilo nezamýšleným akcím zařízení, můžete nakonfigurovat nastavení pro aplikaci Portál společnosti tak, že vyberete možnost přizpůsobení **správy tenanta**  >  **Customization**. 

K dispozici jsou následující akce:
- Skrýt tlačítko **Odebrat** na podnikových zařízeních s Windows
- Skrýt tlačítko pro **obnovení** na podnikových zařízeních s Windows
- Skrýt tlačítko **Odebrat** na podnikových zařízeních s iOS/iPadOS
- Skrýt tlačítko pro **obnovení** na podnikových zařízeních s iOS/iPadOS

> [!NOTE]
> Tyto akce se dají použít k omezení akcí zařízení v Portál společnosti aplikaci a na webu a neimplementují žádné zásady omezení zařízení. Pokud chcete omezit, aby uživatelé prováděli obnovení továrního nastavení nebo odebrání MDM z nastavení, musíte nakonfigurovat zásady omezení zařízení. 

## <a name="opening-web-company-portal-applications"></a>Otevírání webových Portál společnostich aplikací
Pro webové Portál společnosti aplikace, pokud má koncový uživatel nainstalovanou aplikaci Portál společnosti, koncovým uživatelům se zobrazí dialogové okno s dotazem, jak chce aplikaci otevřít, když se otevírá mimo prohlížeč. Pokud aplikace není v cestě Portál společnosti, otevře Portál společnosti domovskou stránku. Pokud se aplikace nachází v cestě, Portál společnosti otevře konkrétní aplikaci. 

Po výběru Portál společnosti bude uživatel přesměrován na odpovídající stránku aplikace v případě, že cesta k identifikátoru URI je jedna z následujících:

- `/apps`– Web Portál společnosti otevře stránku aplikace se seznamem všech aplikací.
- `/apps/[appID]`– Web Portál společnosti otevře stránku podrobností příslušné aplikace.
- *Cesta k identifikátoru URI je jiná nebo neočekávaná* – zobrazí se Domovská stránka web portál společnosti.

Pokud uživatel nemá nainstalovanou aplikaci Portál společnosti, uživatel přejde k webovému Portál společnosti.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Portál společnosti odvozené přihlašovací údaje pro zařízení s iOS/iPadOS

Intune podporuje ověřování osobních identit (PIV) a služby Common Access Card (CAC) odvozené přihlašovací údaje v partnerství s poskytovateli přihlašovacích údajů DISA purebred, Entrust Datacard a Intercede. Koncoví uživatelé procházejí dalšími kroky po registraci zařízení s iOS/iPadOS a ověřují jejich identitu v aplikaci Portál společnosti. Odvozená pověření budou pro uživatele povolena tím, že nejprve nastaví poskytovatele pověření pro vašeho tenanta a pak zacílíte na profil, který používá odvozená pověření pro uživatele nebo zařízení.

> [!NOTE]
> Uživateli se zobrazí pokyny k odvozeným přihlašovacím údajům na základě odkazu, který jste zadali přes Intune.

Další informace o odvozených přihlašovacích údajích pro zařízení s iOS/iPadOS najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-the-company-portal"></a>Tmavý režim pro Portál společnosti

Pro iOS/iPadOS, macOS a Windows Portál společnosti je k dispozici tmavý režim. Uživatelé můžou stahovat aplikace, spravovat jejich zařízení a získávat v nich podporu v barevném schématu podle nastavení zařízení. Portál společnosti pro iOS/iPadOS, macOS a Windows budou automaticky odpovídat nastavení zařízení koncového uživatele pro tmavý nebo lehký režim.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Klávesové zkratky v Portálu společnosti pro Windows

Koncoví uživatelé mohou aktivovat akce navigace, aplikace a zařízení ve Windows Portál společnosti pomocí klávesových zkratek (akcelerátory).

V aplikaci Portál společnosti pro Windows jsou k dispozici následující klávesové zkratky.

| Oblast | Description | Klávesová zkratka |
|--------------------|----------------|-------------------|
| Navigační nabídka | Navigace | Alt+M |
|  | Domů | Alt+H |
|  | Všechny aplikace | Alt+A |
|  | Nainstalované aplikace | Alt+I |
|  | Odeslat názor | Alt+F |
|  | Můj profil | Alt+U |
|  | Nastavení | Alt+T |
| Úvodní stránka – dlaždice Zařízení | přejmenování | F2 |
|  | Odebrat | Ctrl+D nebo Delete |
|  | Kontrola přístupu | Ctrl+M nebo F9 |
| Podrobnosti o zařízení | přejmenování | F2 |
|  | Odebrat | Ctrl+D nebo Delete |
|  | Kontrola přístupu | Ctrl+M nebo F9 |
| Podrobnosti aplikace | Instalace | Ctrl+I |
| Zařízení | K dispozici. | Ctrl+D |

Koncoví uživatelé budou také moci zobrazit dostupné zkratky v aplikaci pro Windows Portál společnosti.

![Snímek obrazovky s dostupnými zástupci ve Windows Portál společnosti](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Akce zařízení Samoobslužná služba uživatele z Portál společnosti

Uživatelé můžou na svých místních nebo vzdálených zařízeních provádět akce prostřednictvím aplikace Portál společnosti, Portál společnosti webu nebo aplikace Intune v Androidu. Akce, které může uživatel provádět, se liší v závislosti na platformě a konfiguraci zařízení. Ve všech případech můžou akce se vzdáleným zařízením provádět jenom primární uživatel zařízení.  

K dispozici jsou i následující akce samoobslužných zařízení:

- **Vyřadit** – odebere zařízení ze správy Intune. V aplikaci Portál společnosti a na webu se zobrazuje jako **Remove (odebrat**).
- **Vymazat** – Tato akce zahájí resetování zařízení. Na webu portál společnosti se zobrazuje jako **resetování**nebo **obnovení továrního nastavení** v aplikaci pro iOS/iPadOS portál společnosti.
- **Přejmenovat** – Tato akce změní název zařízení, které může uživatel vidět v portál společnosti. Nemění název místního zařízení, pouze výpis v Portál společnosti.
- **Synchronizovat** – Tato akce zahájí vrácení se změnami zařízení se službou Intune. Zobrazí se jako **stav kontroly** v portál společnosti.
- **Remote Lock** – zablokuje zařízení a vyžaduje ho k odemknutí.
- **Resetování hesla** – Tato akce se používá k resetování hesla zařízení. V zařízeních se systémem iOS/iPadOS bude heslo odebráno a koncový uživatel bude muset zadat nový kód v nastavení. V podporovaných zařízeních s Androidem Intune vygeneruje nové heslo a dočasně se zobrazí v Portál společnosti.
- **Obnovení klíčů** – Tato akce se používá k obnovení osobního obnovovacího klíče pro šifrovaná zařízení MacOS z webu portál společnosti. 

Chcete-li přizpůsobit dostupné akce samoobslužných uživatelů, přečtěte si téma [přizpůsobení akcí Samoobslužná služba uživatele pro portál společnosti](../apps/company-portal-app.md#customizing-user-self-service-actions-for-the-company-portal).

### <a name="self-service-actions"></a>Akce samoobslužných služeb

Některé platformy a konfigurace neumožňují akce zařízení samoobslužné služby. V této tabulce najdete další podrobnosti o akcích samoobslužných služeb:

| Akce | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | macOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Vyřazení | K dispozici<sup>(1)</sup> | K dispozici<sup>(9)</sup> | K dispozici. | K dispozici<sup>(7)</sup> |
| Vymazání | K dispozici. | K dispozici<sup>(5)</sup><sup>(9)</sup> | Není k dispozici | K dispozici<sup>(7)</sup> |
| Přejmenovat<sup>(4)</sup> | K dispozici | K dispozici | K dispozici | K dispozici |
| Sync | K dispozici | K dispozici | K dispozici | K dispozici |
| Key Recovery | Není k dispozici | Není k dispozici | K dispozici<sup>(2)</sup> | Není k dispozici |

<sup>(1)</sup> **vyřazení** je vždycky blokované na zařízeních s Windows připojená k Azure AD.<br>
<sup>(2)</sup> **obnovení klíče** pro MacOS je dostupné jenom přes webový portál.<br>
<sup>(3)</sup> Pokud používáte registraci správce registrace zařízení, jsou všechny vzdálené akce zakázané.<br>
<sup>(4)</sup> **přejmenování** změní pouze název zařízení v portál společnosti aplikaci nebo webovém portálu, nikoli na zařízení.<br>
<sup>(5)</sup> **vymazání** není k dispozici pro uživatele zaregistrovaná zařízení se systémem iOS/iPadOS.<br>
<sup>(6)</sup> **resetování hesla** není podporované u některých konfigurací pro Android a Android Enterprise. Další informace najdete v tématu [resetování nebo odebrání hesla zařízení v Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> **vyřazení** a **vymazání** nejsou k dispozici ve scénářích pro vlastníky zařízení s Androidem Enterprise (odolat, Cobo, COSU).<br>
<sup>(8)</sup> **resetování hesla** není podporované uživatelem zaregistrovanými zařízeními iOS/iPadOS.<br>
<sup>(9)</sup> Všechna zařízení s automatickým zápisem zařízení s iOS nebo iPadOS (dříve označovaná jako DEP) mají zakázané možnosti **vyřazení** a **vymazání** .

### <a name="app-logs"></a>Protokoly aplikací

Pokud používáte Azure Government, nabízí se protokoly aplikace koncovým uživatelům, aby se rozhodli o způsobu sdílení po inicializaci procesu získání pomoci s problémem. Pokud však Azure Government nepoužíváte, Portál společnosti pošle protokoly aplikací přímo společnosti Microsoft, když uživatel zahájí proces, aby získal pomoc s problémem. Odesílání protokolů aplikace do Microsoftu usnadní řešení problémů.

> [!NOTE]
> V souladu se zásadami Microsoftu a Apple nebudeme z jakéhokoli důvodu prodávat žádná data shromážděná naší službou žádným třetím stranám.

## <a name="next-steps"></a>Další kroky

- [Nakonfigurujte logo vaší organizace a barvu značky pro nové stránky karet v Microsoft Edge pro iOS a Android.](manage-microsoft-edge.md#organization-logo-and-brand-color)
- [Přidání aplikací](apps-add.md)
