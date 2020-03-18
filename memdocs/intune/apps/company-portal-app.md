---
title: Konfigurace aplikace Portál společnosti
titleSuffix: Microsoft Intune
description: Přečtěte si, jak můžete v aplikaci Portál společnosti Intune použít branding pro konkrétní společnosti.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36d26eb7f644731082407e816358b74c515333cb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325655"
---
# <a name="how-to-configure-the-microsoft-intune-company-portal-app"></a>Konfigurace aplikace Portál společnosti služby Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Portál společnosti v Microsoft Intune je místo, odkud mají uživatelé přístup k firemním datům a kde můžou dělat běžné úkoly, jako je registrace zařízení, instalace aplikací nebo vyhledání informací pro oddělení IT v případě žádosti o podporu. Kromě toho aplikace Portál společnosti umožňuje uživateli zabezpečený přístup k prostředkům společnosti. Aplikace Portál společnosti poskytuje několik různých stránek, například domů, aplikace, podrobnosti o aplikaci, zařízení a podrobnosti o zařízení. K rychlému vyhledání aplikací v rámci Portál společnosti můžete aplikace filtrovat na stránce aplikace.

> [!IMPORTANT]
> Aby bylo možné podporovat Firebase Cloud Messaging (FCM) Google, musíte aplikaci pro Android Portál společnosti aktualizovat na nejnovější verzi.  

> [!Tip]
> Když si portál společnosti přizpůsobíte, bude se vaše konfigurace vztahovat na web portálu společnosti i na aplikace Portál společnosti. Všimněte si, že uživatelé musí mít přiřazenou licenci Intune pro přístup k webu Portál společnosti.

Přizpůsobením Portál společnosti umožníte vašim koncovým uživatelům známé a užitečné možnosti. Provedete to tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberete **Správa tenanta** > **branding a přizpůsobení**a pak nakonfigurujete požadovaná nastavení.

Když uživatel instaluje aplikaci pro iOS/iPadOS z Portál společnosti, zobrazí se výzva. K tomu dochází, když je aplikace pro iOS/iPadOS propojená s obchodem s aplikacemi, která je propojená s programem Volume purchase program (VPP), nebo propojená s obchodní aplikací (LOB). Tato výzva umožní uživatelům přijmout akci nebo povolit správu aplikace. Výzva zobrazí název vaší společnosti, nebo pokud název vaší společnosti není k dispozici, zobrazí se **portál společnosti** . 

> [!Note]
> Pokud používáte Azure Government, nabízí se protokoly aplikace koncovým uživatelům, aby se rozhodli o způsobu sdílení po inicializaci procesu získání pomoci s problémem. Pokud ale Azure Government nepoužíváte, Portál společnosti pro Windows 10 bude odesílat protokoly aplikace přímo Microsoftu, když uživatel iniciuje proces pro získání pomoci s problémem. Odesílání protokolů aplikace do Microsoftu usnadní řešení problémů. 

## <a name="company-information-and-privacy-statement"></a>Informace o společnosti a prohlášení o zásadách ochrany osobních údajů
Název společnosti je zobrazen v záhlaví okna Portálu společnosti. Prohlášení o ochraně osobních údajů se zobrazí po kliknutí na odkaz na zásady ochrany osobních údajů.

| Název pole | Maximální délka | Další informace |
|---|---|---|
|**Název společnosti**| 40 | Tento název se zobrazí v záhlaví okna Portálu společnosti a bude se zobrazovat jako text během činnosti koncového uživatele Intune. |
| **Adresa URL prohlášení o zásadách ochrany osobních údajů** |     79     | Můžete přidat vlastní prohlášení o zásadách ochrany osobních údajů společnosti, které se uživatelům zobrazí po kliknutí na příslušné odkazy v Portálu společnosti. Musíte zadat platnou adresu URL ve formátu `<https://www.contoso.com>`. |

> [!NOTE]
> V souladu se zásadami Microsoftu a Apple nebudeme z jakéhokoli důvodu prodávat žádná data shromážděná naší službou žádným třetím stranám.

## <a name="support-information"></a>Informace o podpoře
Zadejte informace o podpoře vaší společnosti a poskytněte tak vašemu zaměstnanci kontakt na otázky související s Intune.

|Název pole|Maximální délka|Další informace|
|---|---|---|
|**Jméno kontaktu** | 40 | Tento název se zobrazí na stránce **pomoc a podpora** . |
|**Telefonní číslo** | 20 | Toto kontaktní číslo se zobrazí na stránce **pomoc a podpora** , aby se zaměstnanci mohli obrátit na podporu. |
|**E-mailová adresa**| 40 | Tato kontaktní adresa se zobrazí na stránce **pomoc a podpora** . Je potřeba zadat platnou e-mailovou adresu ve formátu `alias@domainname.com`. |
|**Název webu**| 40 | Toto je popisný název, který se zobrazí pro adresu URL webu podpory. Pokud zadáte adresu URL webu podpory bez popisného názvu, zobrazí se na stránce **pomoc a podpora** v portál společnosti adresa přejít na web IT. |
|**Adresa URL webu**| 150 | Pokud máte web podpory, který chcete, aby uživatelé používali, zadejte jeho adresu URL sem. Adresa URL musí být ve formátu `https://www.contoso.com`. Pokud adresu URL nezadáte, nezobrazí se na stránce pomoc **a podpora** v portál společnosti žádné informace o webu podpory. |
| **Další informace**| 120 | Zobrazí se na stránce **pomoc a podpora** . |


## <a name="company-identity-branding-customization"></a>Přizpůsobení brandingu firemní identity
Portál své společnosti si můžete přizpůsobit – můžete na něj umístit logo své společnosti, uvést na něm název své společnosti a použít na něm barevný motiv a pozadí podle svých představ.

### <a name="theme-color-and-logo-in-the-company-portal"></a>Barva motivu a logo na Portálu společnosti
Přiřaďte barvu motivu pro Portál společnosti. Vyberte standardní barvu nebo zadejte šestimístný šestnáctkový kód pro vlastní barvu.

|Název pole|Další informace|
|---|---|
|**Vyberte standardní barvu, nebo zadejte šestičíselný šestnáctkový kód**| Zvolte možnost **Standard** pro vizuální výběr barvy. Zvolte **Vlastní**, pokud chcete vybrat konkrétní barvu podle hodnoty šestnáctkového kódu.|
|**Zvolit barvu motivu**| Vyberte barvu motivu, kterou chcete použít pro Portál společnosti. Můžete ji vybrat ze standardní barvy nebo zadat konkrétní šestnáctkový kód. |
|**Zobrazení**| Vyberte, zda chcete zobrazit **Logo a název firmy**, **Jen logo firmy** nebo **Jen název firmy**. |
|**Nahrát firemní logo**|Tato možnost vám umožní nahrát vlastní firemní logo, které se bude zobrazovat na Portálu společnosti. Všimněte si, že barva textu se automaticky zvolí tak, aby byl zajištěn nejvyšší kontrast. Pokud chcete dosáhnout nejlepšího vzhledu, nahrajte logo s transparentním pozadím.<p><ul><li>Maximální velikost obrázku: 400 px × 400 px</li><li>Maximální velikost souboru: 750 kB</li><li>Typ souboru: PNG, JPG nebo JPEG</li></ul>|

Po nahrání loga se v oblasti náhledu zobrazí logo s barvou motivu. Pokud jste si zvolili zobrazení názvu firmy, zobrazí se název na Portálu společnosti v černé nebo bílé barvě. Barva se zvolí automaticky tak, aby byl zajištěn nejvyšší kontrast s ohledem na barvu motivu. V oblasti náhledu na obrazovce se nezobrazuje název vaší společnosti. 

### <a name="logo-to-use-on-white-or-light-backgrounds"></a>Logo, které se použije na bílých nebo světlých pozadích
Zvolte logo, které bude nejlépe vypadat na bílých nebo světlých pozadích.

|Název pole|Další informace|
|---|---|
|**Nahrát logo**| Tato možnost je dostupná, pokud jste zvolili zobrazení loga společnosti. Pokud chcete dosáhnout nejlepšího vzhledu, nahrajte logo s transparentním pozadím.<p><ul><li>Maximální velikost obrázku: 400 px × 400 px</li><li>Maximální velikost souboru: 750 kB</li><li>Typ souboru: PNG, JPG nebo JPEG</li></ul>|

### <a name="brand-image-for-company-portal"></a>Firemní logo pro Portál společnosti

Zobrazte si firemní logo, které odráží značku vaší společnosti. Po uložení změn můžete zvolit možnost **Zobrazit náhled nastavení** na webovém portálu Intune v horní části podokna a zjistit, jak budou vaše konfigurace vypadat. Všimněte si, že budete moct zobrazit náhled obrázku značky jenom na zařízení s iOS/iPadOS, ne na webovém portálu Intune. 

|Název pole|Další informace|
|---|---|
|**Nahrát firemní logo**| Tato možnost umožňuje zobrazit obrázek značky. V Portál společnosti pro iOS/iPadOS se na stránce profilu uživatele zobrazuje jako obrázek na pozadí.<p><ul><li>Doporučená šířka obrázku: větší než 1125px (musí být aspoň 650 px)</li><li>Maximální velikost obrázku: 1,3 MB</li><li>Typ souboru: PNG, JPG nebo JPEG</li></ul>|

Správný obrázek značky může vylepšit důvěryhodnost uživatele v Portál společnosti tím, že prezentuje silný smysl firemních značek. Nabízíme vám několik tipů, nad kterými byste se mohli zamyslet při pořizování, výběru a optimalizaci loga pro Portál společnosti. 

- Obraťte se na marketingové nebo kreativní oddělení. Můžou už mít schválenou sadu imagí značky. Mohli by vám také pomoci při optimalizaci obrázků. 

- Zvažte kompozici v orientaci jak na šířku, tak i na výšku. Ústřední bod obrázku by mělo obklopovat dostatečně velké pozadí. Obrázek může být oříznutý odlišně na základě velikosti zařízení, orientace a platformy. 

- Nepoužívejte obecné obrázky převzaté z fotobanky. Image by měla odrážet značku vaší společnosti a znát uživatele. Pokud ho ještě nemáte, je lepší nepoužívat ho, než použijte obecný, který nemá žádný význam pro uživatele. 

- Odeberte nepotřebná metadata. Soubor obrázku může obsahovat metadata, jako jsou profil fotoaparátu, zeměpisná poloha, název, popisek a další. Pomocí nástroje pro optimalizaci obrázků tyto informace odstraňte, abyste zachovali kvalitu, ale vešli se do velikostního limitu souboru. 

Po přidání nebo změně obrázku značky v Intune nemusí koncový uživatel na zařízení se systémem iOS nebo iPadOS vidět změnu, dokud Portál společnosti nerozpoznali změnu při spuštění, a pak se restartoval, aby zobrazila obrázek značky. 

### <a name="brand-image-examples"></a>Příklady obrázků značky

Následující obrázek ukazuje příklad obrázku na základě značky pro iPad:

![Snímek obrazovky s ukázkovým obrázkem o značce iPhone](./media/company-portal-app/company-portal-app-03.png)

Následující obrázek ukazuje příklad obrázku iPhone s brandingem:

![Snímek obrazovky s ukázkovým obrázkem značky pro iPad](./media/company-portal-app/company-portal-app-02.png)

## <a name="privacy-statement-customization"></a>Přizpůsobení prohlášení o zásadách ochrany osobních údajů

Prohlášení o zásadách ochrany osobních údajů, které se zobrazí pro vaši organizaci, můžete přizpůsobit na spravovaných zařízeních se systémem iOS/iPadOS. Tato zpráva obsahuje seznam položek, které vaše organizace nemůže zobrazit nebo dělat na spravovaných zařízeních se systémem iOS/iPadOS.

V části **portál společnosti přizpůsobení** > **Správa zařízení a zpráva o ochraně osobních údajů**můžete:

- Přijměte **výchozí hodnotu** pro použití seznamu, jak je uvedeno níže.
- Zvolením možnosti **vlastní** upravíte seznam položek, které vaše organizace nemůže zobrazit nebo dělat na spravovaných zařízeních se systémem iOS/iPadOS. Pomocí [Markdownu](https://daringfireball.net/projects/markdown/) můžete přidat odrážky, tučné písmo, kurzívu a odkazy.

## <a name="company-portal-derived-credentials-for-ios-devices"></a>Portál společnosti odvozené přihlašovací údaje pro zařízení s iOS

Intune podporuje ověřování osobních identit (PIV) a služby Common Access Card (CAC) odvozené přihlašovací údaje v partnerství s poskytovateli přihlašovacích údajů DISA purebred, Entrust Datacard a Intercede. Koncoví uživatelé procházejí dalšími kroky po registraci zařízení s iOS/iPadOS a ověřují jejich identitu v aplikaci Portál společnosti. Odvozená pověření budou pro uživatele povolena tím, že nejprve nastaví poskytovatele pověření pro vašeho tenanta a pak zacílíte na profil, který používá odvozená pověření pro uživatele nebo zařízení.

> [!NOTE]
> Uživateli se zobrazí pokyny k odvozeným přihlašovacím údajům na základě odkazu, který jste zadali přes Intune.

Další informace o odvozených přihlašovacích údajích pro zařízení s iOS/iPadOS najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-ios-company-portal"></a>Tmavý režim pro iOS Portál společnosti

Pro iOS Portál společnosti je k dispozici tmavý režim. Uživatelé můžou stahovat firemní aplikace, spravovat jejich zařízení a získávat v nich podporu v barevném schématu podle nastavení zařízení. Portál společnosti pro iOS bude automaticky odpovídat nastavení zařízení koncového uživatele pro tmavý nebo lehký režim.

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

![Snímek obrazovky s dostupnými zástupci ve Windows Portál společnosti](./media/company-portal-app/company-portal-app-01.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Akce zařízení Samoobslužná služba uživatele z Portál společnosti

Uživatelé můžou na svých místních nebo vzdálených zařízeních provádět akce pomocí Portál společnosti aplikace nebo webu. Akce, které může uživatel provádět, se liší v závislosti na platformě a konfiguraci zařízení. Ve všech případech můžou akce se vzdáleným zařízením provádět jenom primární uživatel zařízení.
- **Vyřadit** – odebere zařízení ze správy Intune. V aplikaci Portál společnosti a na webu se zobrazuje jako **Remove (odebrat**).
- **Vymazat** – Tato akce zahájí resetování zařízení. Na webu portál společnosti se zobrazuje jako **resetování**nebo **obnovení továrního nastavení** v aplikaci Portál společnosti pro iOS.
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
<sup>(5)</sup> **vymazání** není k dispozici na uživatelem zaregistrovaných zařízeních iOS.<br>
<sup>(6)</sup> **resetování hesla** není podporované u některých konfigurací pro Android a Android Enterprise. Další informace najdete v tématu [resetování nebo odebrání hesla zařízení v Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> **vyřazení** a **vymazání** nejsou k dispozici ve scénářích pro vlastníky zařízení s Androidem Enterprise (odolat, Cobo, COSU).<br> 
<sup>(8)</sup> **resetování hesla** není u zaregistrovaných zařízení se systémem iOS podporované uživatelem.

## <a name="next-steps"></a>Další kroky

- [Ruční přidání aplikace Portál společnosti pro Windows 10 pomocí Microsoft Intune](company-portal-app.md)
