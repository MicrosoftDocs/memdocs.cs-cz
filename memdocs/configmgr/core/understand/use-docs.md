---
title: Jak používat dokumentaci
titleSuffix: Configuration Manager
description: Přečtěte si tipy k používání knihovny dokumentace Configuration Manager technickou dokumentaci.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31f9b1cb083400abd36858a177e87804a916362c
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746507"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Jak používat Configuration Manager docs

*Platí pro: Configuration Manager (Current Branch)*

Tento článek poskytuje zdroje informací a tipy pro používání knihovny dokumentace Configuration Manager.

- Hledání
- Odesílání chyb dokumentů, vylepšení, otázek a nových nápadů
- Jak dostávat upozornění na změny
- Jak přispívat do dokumentů

Obecnou nápovědu k produktu najdete v tématu věnovaném [hledání nápovědě](find-help.md).

## <a name="search"></a><a name="bkmk_searchtips"></a>Nápovědě

Následující tipy vám můžou pomoct při hledání požadovaných informací:

- Pokud používáte preferovaný vyhledávací web k vyhledání obsahu pro Configuration Manager, zahrňte `ConfigMgr` společně s klíčovými slovy hledání.

  - Vyhledejte výsledky z `docs.microsoft.com/mem/configmgr` pro Configuration Manager aktuální větev. Výsledky `docs.microsoft.com/previous-versions` jsou pro starší verze produktu.

  - Chcete-li se zaměřit na výsledky hledání do aktuální knihovny obsahu, zahrňte `site:docs.microsoft.com` do oboru vyhledávacího modulu.

- Použijte hledané výrazy, které odpovídají terminologii v uživatelském rozhraní a online dokumentaci. Vyhněte se neoficiálním podmínkám nebo zkratkám, které by se vám mohly zobrazit v obsahu komunity. Vyhledejte například:

  - "bod správy" místo "MP"
  - "typ nasazení" místo "DT"
  - "aktualizace softwaru" místo "SUM"

- Pokud chcete hledat v aktuálním článku, použijte funkci **Najít** v prohlížeči. V případě většiny moderních webových prohlížečů stiskněte **kombinaci kláves CTRL** + **F** a zadejte hledané výrazy.

- Každý článek v systému `docs.microsoft.com` obsahuje následující pole, která vám pomůžou při hledání obsahu:

  - **Vyhledejte** v pravém horním rohu. Pokud chcete vyhledat všechny články, zadejte do tohoto pole výrazy. Články v knihovně Configuration Manager automaticky obsahují `ConfigMgr` obor pro hledání v této knihovně dokumentace.

  - **Filtrovat podle názvu** nad levou tabulku obsahu Pokud chcete vyhledat aktuální obsah, zadejte do tohoto pole výrazy. Toto pole odpovídá pouze podmínkám, které se zobrazí v nadpisech článků pro aktuální uzel. Například **základní infrastruktura** ( `docs.microsoft.com/configmgr/core` ) nebo **Správa aplikací** ( `docs.microsoft.com/configmgr/apps` ).

- Máte problémy s jejich hledáním? [Váš názor na soubor](#bkmk_docfeedback) Při nastavování problému poskytněte vyhledávací web, který používáte, klíčová slova, která jste zkusili, a cílový článek. Tato zpětná vazba pomáhá Microsoftu optimalizovat obsah pro lepší vyhledávání.

> [!TIP]
> Configuration Manager počínaje verzí 1902 se v novém pracovním prostoru **komunity** konzoly Configuration Manager nachází uzel **dokumentace** . Tento uzel obsahuje aktuální informace o Configuration Manager dokumentaci a články o podpoře. Další informace najdete v tématu [použití konzoly Configuration Manager](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="feedback"></a><a name="bkmk_docfeedback"></a>Od

V pravém horním rohu libovolného článku **vyberte odkaz pro zpětnou vazbu a** v dolní části jděte do části zpětné vazby. Tato část se integruje s problémy GitHubu. Další informace o integraci s problémy GitHubu najdete v [příspěvku na blogu platformy docs](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Pokud chcete sdílet svůj názor na Configuration Manager samotný produkt, vyberte **svůj názor na produkt**. Další informace najdete v tématu o [zpětné vazbě produktu](find-help.md#product-feedback).

Pro poskytování názoru na dokumentaci je nezbytný [účet GitHubu](https://github.com/join) . Po přihlášení bude pro organizaci MicrosoftDocs jednorázová autorizace. Poté, co vyberete **svůj názor na obsah**, zadejte název a komentář a **Odešlete zpětnou vazbu**. Tato akce vytvoří nový problém pro cílový článek v [úložišti SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Tato integrace také zobrazí všechny existující otevřené nebo uzavřené problémy pro cílový článek. Pokud existuje, přečtěte si je ještě před odesláním nového problému. Pokud najdete související problém, vyberte ikonu obličeje a přidejte reakci, nebo ji můžete rozbalit a přidat komentář.

#### <a name="types-of-feedback"></a>Typy zpětné vazby

K odeslání následujících typů zpětné vazby použijte problémy GitHubu:

- Chyba dokumentu: obsah je neaktuální, nejasný, matoucí nebo porušený.
- Vylepšení dokumentu: návrh na vylepšení článku.
- Otázka k dokumentu: potřebujete pomáhat s hledáním stávající dokumentace.
- Nápad dokumentu: návrh nového článku. Tuto metodu použijte místo UserVoice k poskytnutí názoru na dokumentaci.
- Pochvalné hodnocení: kladná zpětná vazba k užitečnému nebo informativnímu článku!
- Lokalizace: zpětná vazba k překladu obsahu.
- Optimalizace vyhledávače (SEO): zpětná vazba k potížím při hledání obsahu. Do komentářů zahrňte vyhledávací web, klíčová slova a cílový článek.

Pokud vytvoříte problém s tématy, která nesouvisí s dokumentem, společnost Microsoft tyto problémy ukončí. Příklad:

- [Váš názor na produkt](find-help.md#product-feedback)
- [Otázky k produktu](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Žádosti o podporu](https://aka.ms/cmcbsupport)

Pokud chcete sdílet názory na základní platformu docs.microsoft.com, přečtěte si [názory na dokumentaci](https://aka.ms/sitefeedback). Platforma zahrnuje všechny komponenty obálky, například záhlaví, obsah a pravou nabídku. Také způsob vykreslování článků v prohlížeči, například písmo, pole výstrah a kotvy stránky.

## <a name="notifications"></a><a name="bkmk_notifications"></a>Připomenutí

Chcete-li dostávat oznámení, když se změní obsah v knihovně dokumentace, použijte následující postup:

1. K vyhledání článku nebo sady článků použijte hledání na webu [docs](https://docs.microsoft.com/search/index?scope=ConfigMgr) . Příklad:

    - Hledání jednoho článku podle názvu, ["soubory protokolu pro řešení potíží – Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - Vyhledat libovolný článek o [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)

2. V pravém horním rohu vyberte odkaz **RSS** .

3. Pomocí tohoto informačního kanálu v libovolné aplikaci RSS můžete dostávat oznámení, když dojde ke změně výsledků hledání.

> [!TIP]
> Můžete také **sledovat** [úložiště SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) na GitHubu. Tato metoda generuje mnoho oznámení. Nezahrnuje taky změny z privátního úložiště, které Microsoft používá.

## <a name="contribute"></a><a name="bkmk_contribute"></a>Programu

Knihovna dokumentace Configuration Manager, podobně jako většina obsahu v docs.microsoft.com, je otevřená na GitHubu. Tato knihovna přijímá a podporuje komunitní příspěvky. Další informace o tom, jak začít, najdete v [příručce pro přispěvatele](https://docs.microsoft.com/contribute). Jediným předpokladem je vytvoření [účtu GitHub](https://github.com/join).

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Základní kroky pro přispívání do SCCMdocs

1. Z cílového článku vyberte **Upravit**. Tato akce otevře zdrojový soubor v GitHubu.

2. Chcete-li upravit zdrojový soubor, vyberte ikonu tužky.

3. Proveďte změny ve zdroji Markdownu. Další informace najdete v tématu [použití Markdownu pro psaní dokumentů](https://docs.microsoft.com/contribute/markdown-reference).

4. V části navrhnout změnu souboru zadejte komentář veřejné potvrzení popisující, *co* jste změnili. Pak vyberte **navrhnout změnu souboru**.

5. Posuňte se dolů a ověřte změny, které jste provedli. Vyberte **vytvořit žádost o získání dat** a otevřete formulář. Popište, *Proč* jste tuto změnu provedli. Označte autora článku a požádejte ho o revizi. Vyberte **vytvořit žádost o získání dat**.

### <a name="what-to-contribute"></a>Co je potřeba přispívat

Pokud chcete přispívat, ale nevíte, kde začít, podívejte se na následující návrhy:

- V seznamu problémů vyhledejte štítky cílené na komunitu:

  - [dobrý první problém](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [Help – žádoucí](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Autoři Microsoftu tyto štítky přiřadí k problémům, které jsou vhodnými kandidáty na komunitní příspěvek.

- Projděte si článek s přesností. Pak aktualizujte metadata **MS. Date** pomocí `mm/dd/yyyy` formátu. Tento příspěvek pomáhá udržet obsah v čerstvém stavu.

- Na základě vašeho prostředí přidejte vysvětlení, příklady nebo pokyny. Tento příspěvek využívá sílu komunity ke sdílení znalostí.

- Správné překlady v jiné než anglické jazykové verzi. Tento příspěvek zlepšuje použitelnost lokalizovaného obsahu.

> [!NOTE]
> Pokud nejste zaměstnancem Microsoftu, vyžadují velké příspěvky podepisování licenční smlouvy s příspěvkem (CLA). GitHub je automaticky nutný k podepsání této smlouvy, pokud příspěvek splňuje prahovou hodnotu.

### <a name="tips"></a>Tipy

Při přispívání do Configuration Manager dokumentů postupujte podle těchto obecných pokynů:

- Nedělejte si u velkých žádostí o přijetí změn. Místo toho zapište [problém](#bkmk_docfeedback) a spusťte diskuzi. Pak můžeme souhlasit s směrem a teprve potom investovat velké množství času.

- Přečtěte si [příručku ke stylům Microsoftu](https://aka.ms/MicrosoftStyle). Poznejte [10 nejoblíbenějších tipů pro Microsoft Style a Voice](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).

- [Šablonu žádosti o získání dat](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) použijte jako výchozí bod práce.

- Postupujte podle [pracovního postupu Flow GitHub](https://guides.github.com/introduction/flow/).

- Na blogu (nebo cokoli) o vašich příspěvcích, často!

(Tento seznam byl vypůjčen z [Průvodce přispívajícím pro .NET](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Konsolidace dokumentace pro Microsoft Endpoint Manager

Pro lepší podporu kombinovaných scénářů Intune a Configuration Manager jsou jejich knihovny dokumentace konsolidovány na [webu Microsoft Endpoint Manager](https://docs.microsoft.com/mem). Dokumentace k Intune je teď na [docs.Microsoft.com/mem/Intune](https://docs.microsoft.com/mem/intune)a dokumentace k Configuration Manager je teď na [docs.Microsoft.com/mem/ConfigMgr](https://docs.microsoft.com/mem/configmgr). Pokud pořád používáte starou adresu URL, přesměruje se automaticky, takže nemusíte dělat žádné změny pro čtení tohoto obsahu.

Pokud zadáte zpětnou vazbu nebo přispějete k článkům, bude nutné provést některé změny:

- Stávající problémy GitHubu zůstanou v původním úložišti, [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) nebo [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - Tyto problémy se nebudou zobrazovat jako otevřené nebo uzavřené problémy v části věnované zpětné vazbě v odkazovaném článku.

  - Budeme pokračovat v práci na řešení těchto problémů.

  - V některých případech můžeme učinit obtížné uzavřít problém, který se domníváme, že můžeme řešit.

  - Pokud máte problém ve stávajícím úložišti a zapálených se o něm, zaslat svůj názor na migrovaný článek v [úložišti MEMDocs](https://github.com/MicrosoftDocs/MEMDocs).

- Když teď zadáte zpětnou vazbu nebo upravíte článek, problém nebo žádost o přijetí změn přejde do úložiště MEMDocs.
