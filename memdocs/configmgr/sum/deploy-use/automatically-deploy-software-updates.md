---
title: Automatické nasazení aktualizací softwaru
titleSuffix: Configuration Manager
description: Automaticky nasazovat aktualizace softwaru pomocí pravidel automatického nasazení (ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: bf172c4cb34a17ac793ea5568b0505505baf97a0
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709430"
---
#  <a name="automatically-deploy-software-updates"></a>Automatické nasazení aktualizací softwaru  

*Platí pro: Configuration Manager (Current Branch)*

Místo přidávání nových aktualizací do existující skupiny aktualizací softwaru použijte pravidlo automatického nasazení (ADR). Obvykle používáte pravidla automatického nasazení k nasazení měsíčních aktualizací softwaru (označovaných také jako aktualizace úterý) a ke správě Endpoint Protection aktualizací definicí. Pokud potřebujete, abyste zjistili, která metoda nasazení je pro vás nejvhodnější, přečtěte si téma [nasazení aktualizací softwaru](deploy-software-updates.md).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Vytvoření pravidla automatického nasazení  
Automatické schvalování a nasazování aktualizací softwaru pomocí pravidla automatického nasazení. Pravidlo může přidat aktualizace softwaru do nové skupiny aktualizací softwaru pokaždé, když se pravidlo spustí, nebo přidat aktualizace softwaru do existující skupiny. Když se pravidlo spustí a přidá aktualizace softwaru do existující skupiny, pravidlo odebere všechny aktualizace ze skupiny. Pak přidá do skupiny aktualizace, které splňují definovaná kritéria. 

> [!WARNING]  
>  Před prvním vytvořením pravidla automatického nasazení ověřte, že lokalita dokončila synchronizaci aktualizací softwaru. Tento krok je důležitý, když spouštíte Configuration Manager s jiným než anglickým jazykem. Klasifikace aktualizace softwaru se zobrazují v angličtině před první synchronizací a po dokončení synchronizace aktualizací softwaru se pak zobrazí v lokalizovaných jazycích. Pravidla, která vytvoříte před synchronizací aktualizací softwaru, nemusí po synchronizaci správně fungovat, protože textový řetězec se nemusí shodovat.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a>Postup vytvoření pravidla automatického nasazení  

1.  V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **aktualizace softwaru**a vyberte uzel **pravidla automatického nasazení** .  

2.  Na pásu karet klikněte na **vytvořit pravidlo automatického nasazení**.  

3.  Na stránce **Obecné** v Průvodci vytvořením pravidla automatického nasazení nakonfigurujte následující nastavení:  

    -   **Název:** Zadejte název pravidla automatického nasazení. Název musí být jedinečný, může pomáhat s popisem účelu pravidla a identifikovat ho od ostatních v Configuration Manager lokalitě.  

    -   **Popis:** Zadejte popis pravidla automatického nasazení. Popis by měl poskytovat přehled o pravidle nasazení a další relevantní informace, které vám pomůžou pravidlo odlišit od ostatních. Pole popisu je volitelné, je omezeno na 256 znaků a výchozí hodnota je prázdná.  

    -   **Šablona**: vyberte šablonu nasazení a určete, jestli se mají použít dřív uložené konfigurace ADR. Nakonfigurujte šablonu nasazení obsahující více vlastností nasazení společné aktualizace, které můžete použít při vytváření dalších pravidla automatického nasazení. Tyto šablony šetří čas a umožňují zajistit konzistenci napříč podobnými nasazeními. Vyberte jednu z následujících předdefinovaných šablon nasazení aktualizací softwaru:  

         - Šablona rozboru aktualizací **Patch Tuesday** poskytuje obecná nastavení, když zavádíte aktualizace softwaru v měsíčním cyklu.  

         - Šablona **aktualizací klientů Office 365** poskytuje běžná nastavení, která se použijí při nasazení aktualizací pro klienty Office 365 pro plus.
             > [!Note]
             > Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Pokud vaše pravidla automatického nasazení spoléhá na vlastnost "title", budete ji muset upravit od 9. června 2020. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)`je příkladem nového názvu. Další informace o tom, jak upravit pravidla automatického nasazení pro změnu názvu, najdete v tématu [aktualizace kanálů pro aplikace Microsoft 365](manage-office-365-proplus-updates.md#bkmk_channel). Další informace o změně názvu najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change).

         - Šablona **SCEP a aktualizace antivirové ochrany v programu Windows Defender** poskytuje běžná nastavení, která se použijí při nasazení Endpoint Protection aktualizace definic.  

    -   **Kolekce:** Určuje cílovou kolekci, která se pro nasazení použije. Členové kolekce přijímají aktualizace softwaru, jež jsou definovány v nasazení.  

    -   Rozhodněte se, zda chcete přidat aktualizace softwaru do nové nebo existující skupiny aktualizací softwaru. Ve většině případů se při spuštění pravidla automatického nasazení rozhodne vytvořit novou skupinu aktualizací softwaru. Pokud se pravidlo spouští s výkonnějším plánem, můžete použít existující skupinu. Pokud například spouštíte pravidlo pro aktualizace definic každý den, můžete přidat aktualizace softwaru do existující skupiny aktualizací softwaru.  

    -   **Povolit nasazení po spuštění tohoto pravidla:** Určete, jestli se má povolit nasazení aktualizace softwaru po spuštění pravidla automatického nasazení. Pro toto nastavení zvažte následující možnosti:  

        -   Když nasazení povolíte, přidají se aktualizace, které splňují kritéria definovaná v pravidle, do skupiny aktualizací softwaru. Obsah aktualizace softwaru se stáhne podle potřeby. Obsah je zkopírován do zadaných distribučních bodů a aktualizace budou nasazeny do klientů v cílové kolekci.  

        -   Pokud nasazení nepovolíte, přidají se aktualizace, které splňují kritéria definovaná v pravidle, do skupiny aktualizací softwaru. Obsah nasazení aktualizace softwaru je v případě potřeby stažen a distribuován do určených distribučních bodů. Lokalita vytvoří zakázané nasazení ve skupině aktualizace softwaru, aby nedošlo k nasazení aktualizací do klientů. Tato možnost poskytuje čas k přípravě nasazení aktualizací, ověření odpovídajících aktualizací, které splňují kritéria, a pak povolte nasazení.  

4.  Na stránce **nastavení nasazení** nakonfigurujte následující nastavení:  

    -   **Použít funkci Wake on LAN k probuzení klientů pro požadovaná nasazení**: Určuje, jestli se má v konečném termínu povolit Wake on LAN. Wake On LAN odesílá pakety buzení ze spánku na počítače, které v nasazení vyžadují jednu nebo více aktualizací softwaru. Lokalita probudí všechny počítače, které jsou v režimu spánku v konečném termínu instalace, aby bylo možné zahájit instalaci. Klienti, kteří jsou v režimu spánku, který nevyžaduje žádné aktualizace softwaru v nasazení, se nespustí. Ve výchozím nastavení není toto nastavení povolené. Než použijete tuto možnost, nakonfigurujte počítače a sítě pro Wake On LAN. Další informace najdete v tématu [konfigurace Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Úroveň podrobností**: Určuje úroveň podrobností pro zprávy o stavu vynucení aktualizace, které jsou hlášeny klienty.  

        > [!IMPORTANT]  
        >  Pokud nasazujete aktualizace definic, nastavte úroveň podrobností na hodnotu **pouze chyba** , aby klient nahlásil stavovou zprávu pouze v případě, že se aktualizace definice nezdařila. V opačném případě klient hlásí velký počet stavových zpráv, které mohou mít vliv na výkon serveru lokality.  
        
        > [!NOTE]  
        > Úroveň podrobností o **chybě pouze** neodesílá stavové zprávy vynucení, které jsou požadovány pro sledování nevyřízených restartování.

    -   **Nastavení licenčních podmínek:** Určete, jestli se mají automaticky nasazovat aktualizace softwaru s přiřazenými licenčními podmínkami. Některé aktualizace softwaru zahrnují licenční smlouvu. Když automaticky nasadíte aktualizace softwaru, licenční podmínky se nezobrazí a není k dispozici možnost přijmout licenční podmínky. Zvolit automatické nasazení všech aktualizací softwaru bez ohledu na související licenční podmínky nebo nasazení pouze aktualizací, které nemají přidružené licenční podmínky.  

         - Pokud si chcete přečíst licenční smlouvu k aktualizaci softwaru, vyberte aktualizaci softwaru v uzlu **všechny aktualizace softwaru** v pracovním prostoru **softwarová knihovna** . Na pásu karet klikněte na tlačítko **zkontrolovat licenci**.    

         - Chcete-li najít aktualizace softwaru s přiřazenými licenčními podmínkami, přidejte sloupec **licenčních podmínek** do podokna výsledků v uzlu **všechny aktualizace softwaru** . Kliknutím na záhlaví sloupce seřadíte podle aktualizací softwaru s licenčními podmínkami.  

5.  Na stránce **aktualizace softwaru** nakonfigurujte kritéria pro aktualizace softwaru, které se ADR načítá a přidává do skupiny aktualizací softwaru.  

     - Limit pro aktualizace softwaru v pravidle automatického nasazení je 1000 aktualizací softwaru.  

     - V případě potřeby vyfiltrujte velikost obsahu pro aktualizace softwaru v pravidlech automatického nasazení. Další informace najdete v tématu [Configuration Manager a zjednodušená Údržba Windows v operačních systémech nižší úrovně](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056).  

     - Počínaje verzí 1910 můžete použít **nasazení** jako filtr aktualizace pro pravidla automatického nasazení. Tento filtr pomáhá identifikovat nové aktualizace, které může být nutné nasadit do pilotních nebo testovacích kolekcí. Filtr aktualizace softwaru můžete také využít k tomu, abyste se vyhnuli opětovnému nasazení starších aktualizací. 
         - Při použití **nasazení** jako filtru nezapomeňte, že je možné, že jste už aktualizaci nasadili do jiné kolekce, jako je například pilotní nebo testovací kolekce. <!--4852033-->
     - Počínaje verzí 1806 je teď k dispozici filtr vlastností pro **architekturu** . Tento filtr použijte k vyloučení architektury, jako je Itanium a ARM64, které jsou méně běžné. Mějte na paměti, že v systémech s procesorem 64 (x64) jsou spuštěny 32bitové aplikace a komponenty v 32. Pokud si nejste jistí, že nepotřebujete x86, povolte ji i v případě, že zvolíte x64.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10 verze 1903 a novější** se přidala do Microsoft Update jako vlastní produkt, a ne jako součást produktu **Windows 10** , jako je třeba předchozí verze. Tato změna způsobila, že provedete několik ručních kroků, abyste zajistili, že se tyto aktualizace zobrazí u klientů. Pomohli jsme snížit počet ručních kroků, které je třeba provést pro nový produkt ve verzi Configuration Manager 1906. Další informace najdete v tématu [Konfigurace produktů pro verze Windows 10](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later) . <!--4682946-->


6. Na stránce **Plán vyhodnocení** určete, jestli se má povolit, aby se pravidla automatického nasazení spouštěla podle plánu. Když je položka povolena, kliknutím na **Přizpůsobit** nastavte opakovaný plán.  

    - Konfigurace času zahájení pro plán je založena na místním času počítače, na kterém je spuštěna konzola Configuration Manager.  

    - Vyhodnocení pravidla automatického nasazení se může spouštět až třikrát denně.  

    - Nikdy nenastavte plán vyhodnocení s frekvencí, která přesahuje plán synchronizace aktualizací softwaru. Tato stránka zobrazuje plán synchronizace bodu aktualizace softwaru, který vám pomůže určit frekvenci plánu vyhodnocení.  

    - Chcete-li ručně spustit pravidla automatického nasazení, vyberte pravidlo v uzlu **pravidlo automatického nasazení** konzoly a pak klikněte na tlačítko **Spustit** na pásu karet.  

    - Od verze 1802 může být pravidla automatického nasazení naplánováno vyhodnotit posun od základního dne. Například pokud oprava úterý ve středu spadá do středu za vás, nastavte plán hodnocení druhého úterý v měsíci posune o jeden den.<!--1357133-->  
        - Pokud při plánování vyhodnocení s posunem během posledního týdne v měsíci zvolíte posun, který pokračuje v příštím měsíci, vyhodnocuje tato lokalita hodnocení posledního dne v měsíci.<!--506731-->  
        ![Posun plánu vlastního vyhodnocení pro ADR ze základního dne](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Na stránce **plán nasazení** nakonfigurujte následující nastavení:  

    -   **Vyhodnocení plánu**: Určete čas, který Configuration Manager vyhodnotí dostupný čas a konečné termíny instalace. Vyberte, jestli se má používat koordinovaný světový čas (UTC), nebo místní čas počítače, na kterém je spuštěná konzola Configuration Manager.  

          - Když zde vyberete **místní čas klienta** a pak pro **Čas dostupnosti softwaru**vyberete **co nejdříve** , k vyhodnocení, že jsou dostupné aktualizace, se použije aktuální čas v počítači, na kterém je spuštěná konzola Configuration Manager. Toto chování je stejné jako **konečný termín instalace** a čas instalace aktualizací na klienta. Pokud je klient v jiném časovém pásmu, k těmto akcím dochází, když čas klienta dosáhne doby hodnocení.  

    -   **Čas dostupnosti softwaru**: Pomocí jednoho z následujících nastavení určete, kdy mají být aktualizace softwaru dostupné klientům:  

        -   **Co nejdříve**: zpřístupní aktualizace softwaru v nasazení pro klienty, jakmile to bude možné. Když vytvoříte nasazení s vybraným tímto nastavením, Configuration Manager aktualizuje zásady klienta. V dalším intervalu cyklického dotazování zásad klienta se klienti budou vědomi nasazení a aktualizace softwaru jsou k dispozici pro instalaci.  

        -   **Určitý čas**: zpřístupní aktualizace softwaru, které jsou součástí nasazení, pro klienty v určité datum a čas. Když vytvoříte nasazení s povoleným tímto nastavením, Configuration Manager aktualizuje zásady klienta. V dalším cyklu cyklického dotazování zásad klienta se klienti budou vědomi nasazení. Aktualizace softwaru v nasazení však nejsou k dispozici pro instalaci až po nakonfigurované datum a čas.  

    -   **Konečný termín instalace**: výběrem jednoho z následujících nastavení určete konečný termín instalace pro aktualizace softwaru v nasazení:  

        -   **Co nejdříve:** Pomocí tohoto nastavení můžete automaticky nainstalovat aktualizace softwaru v nasazení, jakmile to bude možné.  

        -   **Určený čas:** Pomocí tohoto nastavení můžete aktualizace softwaru v nasazení automaticky nainstalovat v určité datum a čas. Configuration Manager Určuje konečný termín pro instalaci aktualizací softwaru přidáním nakonfigurovaného **zadaného časového** intervalu k **času dostupnosti softwaru**.  

             - Skutečný konečný termín instalace je zobrazený konečný termín a náhodné množství času až dvou hodin. Náhodnost omezuje potenciální dopad klientů v kolekci, kteří instalují aktualizace v nasazení ve stejnou dobu.  

             - Pokud chcete zakázat prodlevu náhodného přeskupování instalace pro požadované aktualizace softwaru, nakonfigurujte nastavení klienta tak, aby ve skupině **Počítačový agent** **zakázal náhodné přeskupování termínu** . Další informace najdete v tématu [nastavení klienta Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    -  **Odložit vynucení tohoto nasazení podle uživatelských preferencí, až do období odkladu definovaného v nastavení klienta**: Toto nastavení povolte, pokud chcete, aby uživatelé měli více času na instalaci požadovaných aktualizací softwaru po uplynutí konečného termínu.  

        - Toto chování se většinou vyžaduje v případě, že je počítač vypnutý po dlouhou dobu a potřebuje nainstalovat mnoho aktualizací softwaru nebo aplikací. Například pokud se uživatel vrátí z dovolené, musí počkat dlouhou dobu, než klient nainstaluje zpožděná nasazení.  

        - **Po uplynutí konečného termínu nasazení (hodiny)** v nastavení klienta nastavte tuto dobu odkladu s dobou odkladu pro vynucení. Další informace najdete v části [Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent) . Poskytnutá lhůta vynucení platí pro všechna nasazení s povolenou možností a cílí na zařízení, na která jste nasadili také nastavení klienta.  

        - Po uplynutí konečného termínu klient nainstaluje aktualizace softwaru v prvním nefiremním okně, které uživatel nakonfigurovali, až do této lhůty odkladu. Uživatel ale přesto může otevřít Centrum softwaru a kdykoli nainstalovat aktualizace softwaru. Jakmile vyprší lhůta odkladu, vynucení se vrátí do normálního chování pro zpožděná nasazení.  

8. Na stránce **činnost koncového uživatele** nakonfigurujte následující nastavení:  

    -   **Oznámení uživateli**: Určuje, jestli se má v centru softwaru zobrazovat oznámení v nakonfigurovaném **čase dostupnosti softwaru**. Toto nastavení také určuje, zda mají být uživatelé upozorněni na klienty.  

    -   **Chování konečného termínu**: Určete chování, když nasazení aktualizace softwaru dosáhne konečného termínu mimo jakákoli definovaná časová období údržby. Mezi možnosti patří to, jestli se mají nainstalovat aktualizace softwaru a jestli se má po instalaci provést restart systému. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.  
        
        > [!Note]
        > To platí jenom v případě, že je pro klientské zařízení nakonfigurované časové období údržby. Není-li v zařízení definováno žádné časové období údržby, bude aktualizace instalace a restartu vždy provedena po uplynutí konečného termínu.

    -   **Chování při restartování zařízení**: Určete, jestli se má potlačit restart systému na serverech a pracovních stanicích, pokud se k dokončení instalace aktualizace vyžaduje restartování.  

        > [!WARNING]  
        >  Potlačení restartu systému se může hodit v serverových prostředích nebo v případě, že nechcete, aby se cílové počítače ve výchozím nastavení restartovaly. Nicméně to může způsobit, že počítače budou v nezabezpečeném stavu. Umožnění vynuceného restartování pomáhá zajistit okamžité dokončení instalace aktualizace softwaru.  

    -   **Zpracování filtru zápisu pro zařízení se systémem Windows Embedded**: Toto nastavení řídí chování při instalaci na zařízeních se systémem Windows Embedded, která jsou povolena pomocí filtru zápisu. Vyberte možnost potvrdit změny při dokončení instalace nebo během časového období údržby. Když vyberete tuto možnost, vyžaduje se restartování a změny se na zařízení zachovají. V opačném případě se aktualizace nainstaluje, použije se na dočasné překrytí a potvrdí se později.  

           -  Když nasadíte aktualizaci softwaru do zařízení se systémem Windows Embedded, ujistěte se, že je zařízení členem kolekce, která má nakonfigurované časové období údržby.  

    - **Chování při opakovaném vyhodnocení nasazení aktualizací softwaru po restartu**: pomocí tohoto nastavení můžete nakonfigurovat nasazení aktualizací softwaru tak, aby klienti spouštěli kontrolu kompatibility aktualizací softwaru ihned po instalaci aktualizací softwaru a restartování z klienta. Toto nastavení umožňuje klientovi vyhledat další aktualizace, které se použijí po restartování klienta, a pak je nainstaluje do stejného časového období údržby.  

9. Na stránce **výstrahy** nakonfigurujte, jak Configuration Manager generuje výstrahy pro toto nasazení. Zkontrolujte nedávné výstrahy aktualizací softwaru z Configuration Manager v uzlu **aktualizace softwaru** v pracovním prostoru **softwarová knihovna** . Pokud používáte i System Center Operations Manager, nakonfigurujte také jeho výstrahy.  

10. Na stránce **Nastavení stahování** nakonfigurujte následující nastavení:  

    - Určete, zda mají klienti stahovat a instalovat aktualizace při použití distribučního bodu od souseda nebo výchozí skupiny hranic lokality.  

    - Určete, jestli by klienti měli stahovat a instalovat aktualizace z distribučního bodu ve výchozí skupině hranic lokality, když obsah pro aktualizace softwaru není dostupný z distribučního bodu v aktuální nebo sousední skupině hranic.  

    - **Povolit klientům sdílet obsah s ostatními klienty ve stejné podsíti:** Určete, jestli se má povolit použití funkce BranchCache pro stahování obsahu. Další informace najdete v tématu [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Počínaje verzí 1802 je služba BranchCache na klientech vždy povolena. Toto nastavení se odebere, protože klienti používají BranchCache, pokud ho distribuční bod podporuje.  

    - **Pokud nejsou aktualizace softwaru k dispozici na distribučním bodu v aktuální, sousední skupině nebo skupinách hranic lokality, Stáhněte obsah z aktualizací společnosti Microsoft**: Toto nastavení vyberte, pokud chcete, aby klienti připojení k intranetu stáhli aktualizace softwaru z Microsoft Update, pokud nejsou v distribučních bodech k dispozici aktualizace. Internetoví klienti vždycky přejdou na Microsoft Update obsahu aktualizací softwaru.  

    - Určete, jestli se klientům povolí stahování po konečném termínu instalace, pokud používají měřené připojení k Internetu. Poskytovatelé internetu někdy účtují podle množství dat, která odesíláte a přijímáte, když používáte připojení účtované podle objemu dat.  

    > [!NOTE]  
    >  Klienti požadují umístění obsahu od bodu správy pro aktualizace softwaru v nasazení. Chování při stahování závisí na tom, jak jste nakonfigurovali distribuční bod, balíček pro nasazení a nastavení na této stránce.   

11. Na stránce **balíček pro nasazení** vyberte jednu z následujících možností:  

    - **Vybrat balíček pro nasazení**: tyto aktualizace přidejte do existujícího balíčku pro nasazení.  

    - **Vytvořit nový balíček pro nasazení**: přidejte tyto aktualizace do nového balíčku pro nasazení. Nakonfigurujte následující další nastavení:  

        -  **Název**: Určuje název balíčku pro nasazení. Použijte jedinečný název, který popisuje obsah balíčku. Je omezena na 50 znaků.  

        -  **Popis**: Zadejte popis, který poskytuje informace o balíčku pro nasazení. Nepovinný popis je omezený na 127 znaků.  

        -  **Zdroj balíčku:** Určuje umístění zdrojových souborů aktualizace softwaru. Zadejte síťovou cestu k umístění zdroje, například `\\server\sharename\path` , nebo klikněte na tlačítko **Procházet** a vyhledejte umístění v síti. Než přejdete na další stránku, vytvořte sdílenou složku pro zdrojové soubory balíčku pro nasazení.  

            - Zadané umístění nemůžete použít jako zdroj jiného balíčku pro nasazení softwaru.  

            - Umístění zdroje balíčku můžete změnit ve vlastnostech balíčku nasazení po Configuration Manager vytvoří balíček pro nasazení. V takovém případě zkopírujte obsah z původního zdroje balíčku do nového umístění zdroje balíčku.  

            -  Počítačový účet poskytovatele služby SMS a uživatel, který spouští Průvodce pro stažení aktualizací softwaru, musí mít oprávnění k **zápisu** do umístění pro stahování. Omezte přístup k umístění pro stahování. Toto omezení snižuje riziko manipulace se zdrojovými soubory aktualizací softwaru.  

        -  **Priorita odeslání**: Zadejte prioritu odeslání balíčku pro nasazení. Configuration Manager používá tuto prioritu při posílání balíčku do distribučních bodů. Balíčky pro nasazení se odesílají v pořadí podle priority: vysoká, střední nebo nízká. Balíčky se stejnou prioritou jsou zasílány v pořadí podle data vytvoření. Pokud neexistují žádné nevyřízené položky, balíček okamžitě zpracuje bez ohledu na jeho prioritu.  

        - **Povolit binární rozdílovou replikaci**: Toto nastavení povolte, pokud chcete minimalizovat síťový provoz mezi lokalitami. Binární rozdílová replikace (binární ROZDÍLOVÁ replikace) aktualizuje jenom obsah, který se v balíčku změnil, místo aktualizace obsahu celého balíčku. Další informace najdete v tématu [binární rozdílová replikace](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Žádný balíček pro nasazení**: od verze 1806 nasaďte aktualizace softwaru do zařízení bez předchozího stažení a distribuce obsahu do distribučních bodů. Toto nastavení je užitečné při práci s extrémně velkým obsahem aktualizace. Můžete ho také použít, když chcete, aby klienti získali obsah z cloudové služby Microsoft Update. Klienti v tomto scénáři si také můžou stáhnout obsah od partnerských uzlů, které už mají potřebný obsah. Klient Configuration Manager nadále spravuje stahování obsahu, proto může využít funkci Configuration Manager sdílené mezipaměti nebo jiné technologie, jako je Optimalizace doručení. Tato funkce podporuje libovolný typ aktualizace, který podporuje Configuration Manager Správa aktualizací softwaru, včetně aktualizací Windows a Office.<!--1357933-->  

        > [!Note]  
        > Jakmile vyberete tuto možnost a použijete nastavení, nebude již možné ji změnit. Ostatní možnosti jsou šedé.<!--SCCMDocs-pr issue 3003-->  

12. Na stránce **distribuční body** určete distribuční body nebo skupiny distribučních bodů, které budou hostovat soubory aktualizace softwaru. Další informace o distribučních bodech najdete v tématu [Konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Tato stránka je dostupná pouze tehdy, když vytvoříte nový balíček pro nasazení aktualizací softwaru.  
  

13. Na stránce **umístění pro stahování** určete, jestli se mají stáhnout soubory aktualizace softwaru z Internetu, nebo z místní sítě. Nakonfigurujte tahle nastavení:  

    -   **Stáhnout softwarové aktualizace z Internetu**: Toto nastavení vyberte, pokud chcete stáhnout aktualizace softwaru ze zadaného umístění na internetu. Toto nastavení je standardně zapnuté.  

    -   **Stáhnout softwarové aktualizace z místa v mé síti:** Pomocí tohoto nastavení můžete stáhnout aktualizace softwaru z místního adresáře nebo sdílené složky. Toto nastavení je užitečné, když počítač, na kterém spouštíte Průvodce, nemá přístup k Internetu. Každý počítač s přístupem k Internetu může předběžně stáhnout aktualizace softwaru. Pak je uložte do umístění v místní síti, které je přístupné z počítače, na kterém běží průvodce. Při stahování obsahu, který je publikovaný prostřednictvím System Center Updates Publisher nebo řešení pro opravy jiného výrobce, by se mohlo jednat o jiný scénář. Sdílenou složku obsahu služby WSUS v bodě aktualizace softwaru nejvyšší úrovně lze zadat jako síťové umístění, ze kterého se má stáhnout `\\server\WsusContent` . <!--memdocs-issue-211-->

14. Na stránce **Výběr jazyka** vyberte jazyky, ve kterých bude lokalita stahovat vybrané aktualizace softwaru. Lokalita stáhne pouze ty aktualizace, pokud jsou k dispozici ve vybraných jazycích. Aktualizace softwaru, které nejsou specifické pro konkrétní jazyk, budou staženy vždy. Ve výchozím nastavení Průvodce vybírá jazyky, které jste nakonfigurovali ve vlastnostech bodu aktualizace softwaru. Před přechodem na další stránku je třeba vybrat alespoň jeden jazyk. Když vyberete jenom jazyky, které aktualizace softwaru nepodporuje, stahování se pro aktualizaci nepovede.  

15. Na stránce **Souhrn** zkontrolujte nastavení. Chcete-li uložit nastavení do šablony nasazení, klikněte na tlačítko **Uložit jako šablonu**. Zadejte název a vyberte nastavení, které chcete do šablony zahrnout, a pak klikněte na **Uložit**. Chcete-li změnit nakonfigurované nastavení, klikněte na stránku přiřazeného průvodce a změňte nastavení.  

    -  Název šablony se může skládat z alfanumerických znaků ASCII i `\` (zpětné lomítko) nebo `'` (jednoduché uvozovky).  

16. Pravidlo automatického nasazení vytvoříte kliknutím na **Další** .  

Po dokončení průvodce se ADR spustí. Přidá aktualizace softwaru, které odpovídají zadaným kritériím, do skupiny aktualizací softwaru. Potom ADR stáhne aktualizace do knihovny obsahu na serveru lokality a distribuuje je do nakonfigurovaných distribučních bodů. ADR pak nasadí skupinu aktualizace softwaru na klienty v cílové kolekci.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Přidání nového nasazení do existujícího pravidla automatického nasazení  

Po vytvoření pravidla automatického nasazení přidejte do pravidla další nasazení. Tato akce vám pomůže spravovat složitost nasazení různých aktualizací do různých kolekcí. Každé nové nasazení má plný rozsah funkcí a možností monitorování.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Postup přidání nového nasazení do existujícího pravidla automatického nasazení  

1.  V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **aktualizace softwaru**, vyberte uzel **pravidla automatického nasazení** a pak vyberte požadované pravidlo.  

2.  Na pásu karet klikněte na **Přidat nasazení**.   

3.  Na stránce **kolekce** v Průvodci přidáním nasazení nakonfigurujte dostupná nastavení podobně jako stránku **Obecné** v Průvodci vytvořením pravidla automatického nasazení. Další informace najdete v předchozí části [procesu vytvoření pravidla automatického](#bkmk_adr-process)nasazení. Zbytek Průvodce přidáním nasazení zahrnuje následující stránky, které se také shodují s podrobnými popisci:  

     - Nastavení nasazení
     - Plán nasazení
     - Zkušenosti uživatele
     - Výstrahy
     - Download Settings  

Nasazení je také možné přidat programově pomocí rutin prostředí Windows PowerShell. Úplný popis použití této metody najdete v části [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Další informace o procesu nasazení najdete v tématu [Proces nasazení aktualizací softwaru](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Další kroky
[Monitorování aktualizací softwaru](monitor-software-updates.md)
