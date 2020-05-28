---
title: Ruční nasazení aktualizací softwaru
titleSuffix: Configuration Manager
description: Ručně vytvořte nasazení softwaru, abyste klientům mohli aktualizovat požadované aktualizace softwaru nebo nasazovat vzdálené aktualizace.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717087"
---
# <a name="manually-deploy-software-updates"></a>Ruční nasazení aktualizací softwaru  

*Platí pro: Configuration Manager (Current Branch)*

Ruční nasazení aktualizace softwaru je proces výběru aktualizací softwaru z konzoly Configuration Manager a ruční spuštění procesu nasazení. Nebo přidejte vybrané aktualizace softwaru do skupiny aktualizací a pak ručně nasaďte skupinu aktualizací. Ruční nasazení se obvykle používá k aktuálnosti klientů pomocí požadovaných aktualizací softwaru. Pak použijete pravidla automatického nasazení (ADR) k řízení průběžného měsíčního nasazení aktualizací softwaru. Tuto ruční metodu použijte také k nasazení vzdálené aktualizace softwaru. Další informace o tom, která metoda nasazení je pro vás nejvhodnější, najdete v tématu [nasazení aktualizací softwaru](deploy-software-updates.md).



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a>Krok 1: určení kritérií hledání pro aktualizace softwaru  

V závislosti na kombinacích produktů a klasifikací, které vaše lokalita synchronizuje, se v konzole Configuration Manager zobrazí potenciálně tisíce aktualizací softwaru. Prvním krokem pracovního postupu ručního nasazení aktualizací softwaru je identifikace aktualizací softwaru, které chcete nasadit. Můžete například zobrazit všechny aktualizace softwaru požadované na více než 50 klientských zařízeních s klasifikací **zabezpečení** nebo **kritická** .  

> [!IMPORTANT]  
>  Jedno nasazení aktualizace softwaru má omezení 1000 aktualizací softwaru.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Proces zadání kritérií hledání pro aktualizace softwaru  

1.  V konzole Configuration Manager přejděte do pracovního prostoru **softwarová knihovna** , rozbalte možnost **aktualizace softwaru**a klikněte na **všechny aktualizace softwaru**. V tomto uzlu se zobrazují všechny synchronizované aktualizace softwaru.  

    > [!NOTE]  
    >  Uzel **všechny aktualizace softwaru** zobrazí pouze aktualizace softwaru s klasifikací **kritická** a **zabezpečení** , které byly vydány v posledních 30 dnech.  

2.  V podokně hledání vyfiltrujte požadované aktualizace softwaru. Použijte jednu nebo obě následující možnosti:  

    -   Do textového pole Hledat zadejte hledaný řetězec, který filtruje aktualizace softwaru. Zadejte například číslo článku nebo ID bulletinu pro určitou aktualizaci softwaru. Nebo zadejte řetězec, který se zobrazí v názvu několika aktualizací softwaru.  

    -   Klikněte na **Přidat kritéria**a vyberte kritéria pro filtrování aktualizací softwaru. Klikněte na tlačítko **Přidat**a poté zadejte hodnoty kritérií.  

3.  Kliknutím na tlačítko **Vyhledat** můžete aktualizace softwaru filtrovat.  

    > [!TIP]  
    >  Ukládat často používaná kritéria filtru. Na pásu karet klikněte na možnost a **uložte aktuální hledání**. Kliknutím na **uložená hledání**načtěte předchozí hledání.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a>Krok 2: Vytvoření skupiny aktualizací softwaru, která obsahuje aktualizace softwaru   

Skupiny aktualizací softwaru umožňují organizovat aktualizace softwaru v přípravě na nasazení. Pomocí následujícího postupu můžete ručně přidat aktualizace softwaru do nové skupiny aktualizací softwaru.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Postup ručního přidání aktualizací softwaru do nové skupiny aktualizací softwaru  

1.  V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** a vyberte možnost **aktualizace softwaru**. Vyberte požadované aktualizace softwaru.  

2.  Na pásu karet klikněte na **vytvořit skupinu aktualizací softwaru** .  

3.  Zadejte název skupiny aktualizací softwaru a případně doplňte také popis. Použijte název a popis, který vám poskytne dostatek informací, abyste mohli určit, jaký typ aktualizací je ve skupině aktualizace softwaru. Klikněte na **Vytvořit**.  

4.  Vyberte uzel **skupiny aktualizací softwaru** a vyberte novou skupinu aktualizace softwaru. Chcete-li zobrazit seznam aktualizací ve skupině, klikněte na tlačítko **Zobrazit členy** na pásu karet.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a> Krok 3: Stažení obsahu skupiny aktualizací softwaru  

Před nasazením aktualizací softwaru si stáhněte obsah aktualizací softwaru ve skupině aktualizace softwaru. Tento krok umožňuje ověřit, zda je obsah v distribučních bodech k dispozici před nasazením aktualizací softwaru. Pomůže vám taky se vyhnout jakýmkoli neočekávaným problémům s distribucí obsahu. Pokud tento krok přeskočíte, v rámci procesu nasazení lokalita stáhne obsah a distribuuje je do distribučních bodů. Pomocí následujícího postupu lze stáhnout obsah aktualizací softwaru ve skupině aktualizací softwaru.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Postup pro stažení obsahu pro skupinu aktualizací softwaru
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Postup sledování stavu obsahu
1. Chcete-li monitorovat stav obsahu pro aktualizace softwaru, v konzole Configuration Manager klikněte na pracovní prostor **monitorování** . Rozbalte položku **stav distribuce**a potom vyberte uzel **stav obsahu** .  

2. Vyberte balíček aktualizace softwaru, který jste dříve identifikovali ke stažení aktualizací softwaru ve skupině aktualizace softwaru.  

3. Na pásu karet klikněte na **Zobrazit stav** .  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a>Krok 4: nasazení skupiny aktualizací softwaru  

Jakmile určíte aktualizace, které chcete nasadit, a přidejte je do skupiny aktualizací softwaru, ručně nasaďte skupinu aktualizace softwaru.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Postup ručního nasazení aktualizací softwaru ve skupině aktualizací softwaru  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **aktualizace softwaru**a vyberte uzel **skupiny aktualizací softwaru** .  

2. Vyberte skupinu aktualizací softwaru, kterou chcete nasadit. Na pásu karet klikněte na **nasadit** .   

3. Na stránce **Obecné** v Průvodci nasazením aktualizace softwaru nakonfigurujte následující nastavení:  

   -   **Název:** Zadejte název nasazení. Nasazení musí mít jedinečný název, který popisuje jeho účel a odlišuje jej od ostatních nasazení v lokalitě. Pole s názvem má limit 256 znaků. Ve výchozím nastavení Configuration Manager automaticky poskytuje název pro nasazení v následujícím formátu:`Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Popis:** Zadejte popis nasazení. Popis je nepovinný, ale poskytuje přehled o nasazení. Zahrnutí jakýchkoli dalších relevantních informací, které pomáhají identifikovat a odlišit je mezi ostatními v lokalitě. Pole s popisem má limit 256 znaků a ve výchozím nastavení má prázdnou hodnotu.  

   -   **Aktualizace softwaru/skupina aktualizace softwaru**: Ověřte, zda je zobrazená skupina aktualizace softwaru nebo aktualizace softwaru správná.  

   -   **Vybrat šablonu nasazení:** Určuje, jestli se má použít dřív uložená šablona nasazení. Nakonfigurujte šablonu nasazení tak, aby ukládala společné vlastnosti nasazení aktualizace softwaru. Pak šablonu použijte při nasazování aktualizací softwaru v budoucnu. Tyto šablony šetří čas a umožňují zajistit konzistenci napříč podobnými nasazeními.  

   -   **Kolekce**: zadejte kolekci pro nasazení. Zařízení v kolekci obdrží aktualizace softwaru v tomto nasazení.  

4. Na stránce **nastavení nasazení** nakonfigurujte následující nastavení:  

   -   **Typ nasazení:** Určuje typ nasazení pro nasazení aktualizace softwaru.  

       > [!IMPORTANT]  
       >  Po vytvoření nasazení aktualizace softwaru nemůžete změnit typ nasazení.  

        - Vyberte možnost **požadováno** pro vytvoření povinného nasazení aktualizace softwaru. Aktualizace softwaru se automaticky nainstalují na klienty před vámi nakonfigurovaným konečným termínem instalace.  

        - Vyberte možnost **k dispozici** pro vytvoření volitelného nasazení aktualizace softwaru. Toto nasazení je dostupné uživatelům k instalaci z centra softwaru.  

       > [!NOTE]  
       >  Když nasadíte skupinu aktualizací softwaru podle **potřeby**, klienti stáhnou obsah na pozadí a dodrží nastavení BITS, pokud je nakonfigurované.  
       > 
       > Pro skupiny aktualizací softwaru nasazené jako **dostupné**klienti stahují obsah z popředí a ignorují nastavení BITS.  

   -   **Použít funkci Wake-on-LAN k probuzení klientů pro požadovaná nasazení**: Určuje, jestli se má v konečném termínu povolit Wake on LAN. Wake On LAN odesílá pakety buzení ze spánku na počítače, které v nasazení vyžadují jednu nebo více aktualizací softwaru. Lokalita probudí všechny počítače, které jsou v režimu spánku v konečném termínu instalace, aby bylo možné zahájit instalaci. Klienti, kteří jsou v režimu spánku, který nevyžaduje žádné aktualizace softwaru v nasazení, se nespustí. Ve výchozím nastavení není toto nastavení povolené. Je dostupná jenom pro **požadovaná** nasazení. Než použijete tuto možnost, nakonfigurujte počítače a sítě pro Wake On LAN. Další informace najdete v tématu [konfigurace Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Úroveň podrobností**: Určuje úroveň podrobností pro stavové zprávy, které klienti hlásí k lokalitě.  

5. Na stránce **plánování** nakonfigurujte následující nastavení:  

   -   **Vyhodnocení plánu**: Určete čas, který Configuration Manager vyhodnotí dostupný čas a konečné termíny instalace. Vyberte, jestli se má používat koordinovaný světový čas (UTC), nebo místní čas počítače, na kterém je spuštěná konzola Configuration Manager.  

       - Když zde vyberete **místní čas klienta** a pak pro **Čas dostupnosti softwaru**vyberete **co nejdříve** , k vyhodnocení, že jsou dostupné aktualizace, se použije aktuální čas v počítači, na kterém je spuštěná konzola Configuration Manager. Toto chování je stejné jako **konečný termín instalace** a čas instalace aktualizací na klienta. Pokud je klient v jiném časovém pásmu, k těmto akcím dochází, když čas klienta dosáhne doby hodnocení.  

   -   **Čas dostupnosti softwaru**: Pomocí jednoho z následujících nastavení určete, kdy mají být aktualizace softwaru dostupné klientům:  

       -   **Co nejdříve**: zpřístupní aktualizace softwaru v nasazení pro klienty, jakmile to bude možné. Když vytvoříte nasazení s vybraným tímto nastavením, Configuration Manager aktualizuje zásady klienta. V dalším intervalu cyklického dotazování zásad klienta se klienti budou vědomi nasazení a aktualizace softwaru jsou k dispozici pro instalaci.  

       -   **Určitý čas**: zpřístupní aktualizace softwaru, které jsou součástí nasazení, pro klienty v určité datum a čas. Když vytvoříte nasazení s povoleným tímto nastavením, Configuration Manager aktualizuje zásady klienta. V dalším cyklu cyklického dotazování zásad klienta se klienti budou vědomi nasazení. Aktualizace softwaru v nasazení však nejsou k dispozici pro instalaci až po nakonfigurované datum a čas.  

   -   **Konečný termín instalace**: tyto možnosti jsou k dispozici pouze pro **požadovaná** nasazení. Výběrem jednoho z následujících nastavení určete konečný termín instalace pro aktualizace softwaru v nasazení.  

       -   **Co nejdříve:** Pomocí tohoto nastavení můžete automaticky nainstalovat aktualizace softwaru v nasazení, jakmile to bude možné.  

       -   **Určený čas:** Pomocí tohoto nastavení můžete aktualizace softwaru v nasazení automaticky nainstalovat v určité datum a čas.  

           - Skutečný konečný termín instalace je zobrazený konečný termín a náhodné množství času až dvou hodin. Náhodnost omezuje potenciální dopad klientů v kolekci, kteří instalují aktualizace v nasazení ve stejnou dobu.   

           - Pokud chcete zakázat prodlevu náhodného přeskupování instalace pro požadované aktualizace softwaru, nakonfigurujte nastavení klienta tak, aby ve skupině **Počítačový agent** **zakázal náhodné přeskupování termínu** . Další informace najdete v tématu [nastavení klienta Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **Odložit vynucení tohoto nasazení podle uživatelských preferencí, až do období odkladu definovaného v nastavení klienta**: Toto nastavení povolte, pokud chcete, aby uživatelé měli více času na instalaci požadovaných aktualizací softwaru po uplynutí konečného termínu.  

       - Toto chování se většinou vyžaduje v případě, že je počítač vypnutý po dlouhou dobu a potřebuje nainstalovat mnoho aktualizací softwaru nebo aplikací. Například pokud se uživatel vrátí z dovolené, musí počkat dlouhou dobu, než klient nainstaluje zpožděná nasazení.  

       - **Po uplynutí konečného termínu nasazení (hodiny)** v nastavení klienta nastavte tuto dobu odkladu s dobou odkladu pro vynucení. Další informace najdete v části [Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent) . Poskytnutá lhůta vynucení platí pro všechna nasazení s povolenou možností a cílí na zařízení, na která jste nasadili také nastavení klienta.  

       - Po uplynutí konečného termínu klient nainstaluje aktualizace softwaru v prvním nefiremním okně, které uživatel nakonfigurovali, až do této lhůty odkladu. Uživatel ale přesto může otevřít Centrum softwaru a kdykoli nainstalovat aktualizace softwaru. Jakmile vyprší lhůta odkladu, vynucení se vrátí do normálního chování pro zpožděná nasazení.  

6. Na stránce **činnost koncového uživatele** nakonfigurujte následující nastavení:  

   -   **Oznámení uživateli**: Určuje, jestli se má v centru softwaru zobrazovat oznámení v nakonfigurovaném **čase dostupnosti softwaru**. Toto nastavení také určuje, zda mají být uživatelé upozorněni na klientské počítače. U **dostupných** nasazení nemůžete vybrat možnost, která se má **Skrýt v nástroji Software Center a všech oznámeních**.  

   -   **Chování konečného termínu**: Toto nastavení se dá nakonfigurovat jenom pro **požadovaná** nasazení. Určete chování, když nasazení aktualizace softwaru dosáhne konečného termínu mimo jakákoli definovaná časová období údržby. Mezi možnosti patří to, jestli se mají nainstalovat aktualizace softwaru a jestli se má po instalaci provést restart systému. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby. 
  
       > [!Note]
       > To platí jenom v případě, že je pro klientské zařízení nakonfigurované časové období údržby. Není-li v zařízení definováno žádné časové období údržby, bude aktualizace instalace a restartu vždy provedena po uplynutí konečného termínu.

   -   **Chování při restartování zařízení**: Toto nastavení se dá nakonfigurovat jenom pro **požadovaná** nasazení. Určete, jestli se má potlačit restart systému na serverech a pracovních stanicích, pokud se k dokončení instalace aktualizace vyžaduje restartování.  

       > [!WARNING]  
       >  Potlačení restartu systému se může hodit v serverových prostředích nebo v případě, že nechcete, aby se cílové počítače ve výchozím nastavení restartovaly. Nicméně to může způsobit, že počítače budou v nezabezpečeném stavu. Umožnění vynuceného restartování pomáhá zajistit okamžité dokončení instalace aktualizace softwaru.  

   -   **Zpracování filtru zápisu pro zařízení se systémem Windows Embedded**: Toto nastavení řídí chování při instalaci na zařízeních se systémem Windows Embedded, která jsou povolena pomocí filtru zápisu. Vyberte možnost potvrdit změny při dokončení instalace nebo během časového období údržby. Když vyberete tuto možnost, vyžaduje se restartování a změny se na zařízení zachovají. V opačném případě se aktualizace nainstaluje, použije se na dočasné překrytí a potvrdí se později.  

       -  Když nasadíte aktualizaci softwaru do zařízení se systémem Windows Embedded, ujistěte se, že je zařízení členem kolekce, která má nakonfigurované časové období údržby.  

   - **Chování při opakovaném vyhodnocení nasazení aktualizací softwaru po restartu**: pomocí tohoto nastavení můžete nakonfigurovat nasazení aktualizací softwaru tak, aby klienti spouštěli kontrolu kompatibility aktualizací softwaru ihned po instalaci aktualizací softwaru a restartování z klienta. Toto nastavení umožňuje klientovi vyhledat další aktualizace, které se použijí po restartování klienta, a pak je nainstaluje do stejného časového období údržby.  

7. Na stránce **výstrahy** nakonfigurujte, jak Configuration Manager generuje výstrahy pro toto nasazení. Zkontrolujte nedávné výstrahy aktualizací softwaru z Configuration Manager v uzlu **aktualizace softwaru** v pracovním prostoru **softwarová knihovna** . Pokud používáte i System Center Operations Manager, nakonfigurujte také jeho výstrahy. Nakonfigurujte jenom výstrahy pro **požadovaná** nasazení.  

8. Na stránce **Nastavení stahování** nakonfigurujte následující nastavení:  

    > [!NOTE]  
    >  Klienti požadují umístění obsahu od bodu správy pro aktualizace softwaru v nasazení. Chování při stahování závisí na tom, jak jste nakonfigurovali distribuční bod, balíček pro nasazení a nastavení na této stránce.  

    - Určete, zda mají klienti stahovat a instalovat aktualizace při použití distribučního bodu od souseda nebo výchozí skupiny hranic lokality.  

    - Určete, jestli by klienti měli stahovat a instalovat aktualizace z distribučního bodu ve výchozí skupině hranic lokality, když obsah pro aktualizace softwaru není dostupný z distribučního bodu v aktuální nebo sousední skupině hranic.  

    - **Povolit klientům sdílet obsah s ostatními klienty ve stejné podsíti:** Určete, jestli se má povolit použití funkce BranchCache pro stahování obsahu. Další informace najdete v tématu [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Počínaje verzí 1802 je služba BranchCache na klientech vždy povolena. Toto nastavení se odebere, protože klienti používají BranchCache, pokud ho distribuční bod podporuje.  

    - **Pokud nejsou aktualizace softwaru k dispozici na distribučním bodu v aktuální, sousední skupině nebo skupinách hranic lokality, Stáhněte obsah z aktualizací společnosti Microsoft**: Toto nastavení vyberte, pokud chcete, aby klienti připojení k intranetu stáhli aktualizace softwaru z Microsoft Update, pokud nejsou v distribučních bodech k dispozici aktualizace. Internetoví klienti vždycky přejdou na Microsoft Update obsahu aktualizací softwaru.

    - Určete, jestli se klientům povolí stahování po konečném termínu instalace, pokud používají měřené připojení k Internetu. Poskytovatelé internetu někdy účtují podle množství dat, která odesíláte a přijímáte, když používáte připojení účtované podle objemu dat.  

9. Na stránce **balíček pro nasazení** vyberte jednu z následujících možností:  

    > [!Note]  
    > Pokud jste již provedli [Krok 3: stažení obsahu pro skupinu aktualizací softwaru](#BKMK_3DownloadContent), Průvodce nezobrazí stránky **balíček pro nasazení**, **distribuční body**a **Výběr jazyka** . Přejděte na stránku [Souhrn](#bkmk_summary) v průvodci.  
    > 
    >  Aktualizace softwaru, které byly dříve staženy do knihovny obsahu na serveru lokality, se znovu nestahují. Toto chování je pravdivé i v případě, že vytvoříte nový balíček pro nasazení pro aktualizace softwaru. Pokud již byly všechny aktualizace softwaru staženy, průvodce přeskočí na stránku [Souhrn](#bkmk_summary) .  

    - **Vybrat balíček pro nasazení**: tyto aktualizace přidejte do existujícího balíčku pro nasazení.  

    - **Vytvořit nový balíček pro nasazení**: přidejte tyto aktualizace do nového balíčku pro nasazení. Nakonfigurujte následující další nastavení:  

        -  **Název**: Určuje název balíčku pro nasazení. Použijte jedinečný název, který popisuje obsah balíčku. Je omezena na 50 znaků.  

        -  **Popis**: Zadejte popis, který poskytuje informace o balíčku pro nasazení. Nepovinný popis je omezený na 127 znaků.  

        -  **Zdroj balíčku:** Určete umístění zdrojových souborů aktualizace softwaru. Zadejte síťovou cestu k umístění zdroje, například `\\server\sharename\path` , nebo klikněte na tlačítko **Procházet** a vyhledejte umístění v síti. Než přejdete na další stránku, vytvořte sdílenou složku pro zdrojové soubory balíčku pro nasazení.  

            - Zadané umístění nemůžete použít jako zdroj jiného balíčku pro nasazení softwaru.  

            - Umístění zdroje balíčku můžete změnit ve vlastnostech balíčku nasazení po Configuration Manager vytvoří balíček pro nasazení. V takovém případě zkopírujte obsah z původního zdroje balíčku do nového umístění zdroje balíčku.  

            -  Počítačový účet poskytovatele služby SMS a uživatel, který spouští Průvodce pro stažení aktualizací softwaru, musí mít oprávnění k **zápisu** do umístění pro stahování. Omezte přístup k umístění pro stahování. Toto omezení snižuje riziko manipulace se zdrojovými soubory aktualizací softwaru.  

        -  **Priorita odeslání**: Zadejte prioritu odeslání balíčku pro nasazení. Configuration Manager používá tuto prioritu při posílání balíčku do distribučních bodů. Balíčky pro nasazení se odesílají v pořadí podle priority: vysoká, střední nebo nízká. Balíčky se stejnou prioritou jsou zasílány v pořadí podle data vytvoření. Pokud neexistují žádné nevyřízené položky, balíček okamžitě zpracuje bez ohledu na jeho prioritu.  

        - **Povolit binární rozdílovou replikaci**: Toto nastavení povolte, pokud chcete minimalizovat síťový provoz mezi lokalitami. Binární rozdílová replikace (binární ROZDÍLOVÁ replikace) aktualizuje jenom obsah, který se v balíčku změnil, místo aktualizace obsahu celého balíčku. Další informace najdete v tématu [binární rozdílová replikace](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Žádný balíček pro nasazení**: od verze 1806 nasaďte aktualizace softwaru do zařízení bez předchozího stažení a distribuce obsahu do distribučních bodů. Toto nastavení je užitečné při práci s extrémně velkým obsahem aktualizace. Můžete ho také použít, když chcete, aby klienti získali obsah z cloudové služby Microsoft Update. Klienti v tomto scénáři si také můžou stáhnout obsah od partnerských uzlů, které už mají potřebný obsah. Klient Configuration Manager nadále spravuje stahování obsahu, proto může využít funkci Configuration Manager sdílené mezipaměti nebo jiné technologie, jako je Optimalizace doručení. Tato funkce podporuje libovolný typ aktualizace, který podporuje Configuration Manager Správa aktualizací softwaru, včetně aktualizací Windows a Office.<!--1357933-->  

10. Na stránce **distribuční body** určete distribuční body nebo skupiny distribučních bodů, které budou hostovat soubory aktualizace softwaru. Další informace o distribučních bodech najdete v tématu [Konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Pokud jste již provedli [Krok 3: stažení obsahu pro skupinu aktualizací softwaru](#BKMK_3DownloadContent), Průvodce nezobrazí stránky **balíček pro nasazení**, **distribuční body**a **Výběr jazyka** . Přejděte na stránku [Souhrn](#bkmk_summary) v průvodci.  

11. Na stránce **umístění pro stahování** určete, jestli se mají stáhnout soubory aktualizace softwaru z Internetu, nebo z místní sítě. Nakonfigurujte tahle nastavení:  

    -   **Stáhnout softwarové aktualizace z Internetu**: Toto nastavení vyberte, pokud chcete stáhnout aktualizace softwaru ze zadaného umístění na internetu. Toto nastavení je standardně zapnuté.  

    -   **Stáhnout softwarové aktualizace z místa v mé síti:** Pomocí tohoto nastavení můžete stáhnout aktualizace softwaru z místního adresáře nebo sdílené složky. Toto nastavení je užitečné, když počítač, na kterém spouštíte Průvodce, nemá přístup k Internetu. Každý počítač s přístupem k Internetu může předběžně stáhnout aktualizace softwaru. Pak je uložte do umístění v místní síti, které je přístupné z počítače, na kterém běží průvodce.  

12. Na stránce **Výběr jazyka** vyberte jazyky, ve kterých bude lokalita stahovat vybrané aktualizace softwaru. Lokalita stáhne pouze ty aktualizace, pokud jsou k dispozici ve vybraných jazycích. Aktualizace softwaru, které nejsou specifické pro konkrétní jazyk, budou staženy vždy. Ve výchozím nastavení Průvodce vybírá jazyky, které jste nakonfigurovali ve vlastnostech bodu aktualizace softwaru. Před přechodem na další stránku je třeba vybrat alespoň jeden jazyk. Když vyberete jenom jazyky, které aktualizace softwaru nepodporuje, stahování se pro aktualizaci nepovede.  

    > [!Note]  
    > Pokud jste již provedli [Krok 3: stažení obsahu pro skupinu aktualizací softwaru](#BKMK_3DownloadContent), Průvodce nezobrazí stránky **balíček pro nasazení**, **distribuční body**a **Výběr jazyka** . Přejděte na stránku [Souhrn](#bkmk_summary) v průvodci.  

13. <a name="bkmk_summary"></a>Na stránce **Souhrn** zkontrolujte nastavení. Chcete-li uložit nastavení do šablony nasazení, klikněte na tlačítko **Uložit jako šablonu**. Zadejte název a vyberte nastavení, které chcete do šablony zahrnout, a pak klikněte na **Uložit**. Chcete-li změnit nakonfigurované nastavení, klikněte na stránku přiřazeného průvodce a změňte nastavení.  

    -  Název šablony se může skládat z alfanumerických znaků ASCII i `\` (zpětné lomítko) nebo `'` (jednoduché uvozovky).  

14. Kliknutím na **Další** nasadíte aktualizaci softwaru.  

    Po dokončení průvodce Configuration Manager stáhne aktualizace softwaru do knihovny obsahu na serveru lokality. Pak distribuuje obsah do nakonfigurovaných distribučních bodů a nasadí skupinu aktualizace softwaru na klienty v cílové kolekci. Další informace o procesu nasazení najdete v tématu [Proces nasazení aktualizací softwaru](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Další kroky
[Monitorování aktualizací softwaru](monitor-software-updates.md)
