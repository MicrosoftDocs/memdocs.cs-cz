---
title: Úvod do vytváření sestav
titleSuffix: Configuration Manager
description: Přečtěte si o sadě nástrojů a prostředcích, které jsou k dispozici pro správu vytváření sestav v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607525"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Úvod do vytváření sestav v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vytváření sestav v Configuration Manager poskytuje sadu nástrojů a prostředků, které vám pomůžou používat pokročilé možnosti vytváření sestav služby SQL Server Reporting Services (SSRS) a Server sestav Power BI. Obě platformy pro vytváření sestav poskytují bohatá prostředí pro vytváření vlastních sestav. Vytváření sestav pomáhá shromažďovat, organizovat a prezentovat informace o množství Configuration Managerch dat ve vaší organizaci. Configuration Manager poskytuje ve službě Reporting Services mnoho předdefinovaných sestav, které můžete použít beze změn. Výchozí sestavy můžete duplikovat a upravit tak, aby splňovaly vaše požadavky, nebo můžete vytvořit vlastní sestavy.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services poskytuje celou škálu nástrojů a služeb připravených k použití, které vám pomůžou vytvářet, nasazovat a spravovat sestavy pro vaši organizaci. Obsahuje také funkce programování, které umožňují rozšiřování a přizpůsobení funkcí vytváření sestav. Služba Reporting Services je platforma pro generování sestav založená na serveru, která poskytuje komplexní funkci generování sestav pro různé druhy zdrojů dat.

Configuration Manager používá SQL Server Reporting Services jako své primární řešení pro vytváření sestav. Integrace se službou Reporting Services nabízí následující výhody:  

- K dotazování databáze Configuration Manager používá standardní systém generování sestav.  

- Zobrazí sestavy pomocí nástroje Configuration Manager Report Viewer nebo pomocí Správce sestav, což je webové připojení k sestavě.  

- Nabízí vysoký výkon, dostupnost a škálovatelnost.  

- Poskytuje odběr sestav, ke kterým se uživatelé můžou přihlásit k odběru. Správce například přihlásí k odběru e-mailem sestavu každý den, který podrobně popisuje stav zavedení aktualizace softwaru.

- Exportuje sestavy do různých druhů oblíbených formátů.  

Další informace najdete v tématu [co je SQL Server Reporting Services (SSRS)?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports)

## <a name="power-bi-report-server"></a>Server sestav Power BI

<!-- 3721603 -->

Počínaje verzí 2002 Integrujte Server sestav Power BI s vytvářením sestav Configuration Manager. Tato integrace poskytuje moderní vizualizaci a lepší výkon. Přidává konzolovou podporu pro Power BI sestavy podobné tomu, co už existují s SQL Server Reporting Services. Další informace najdete v tématu věnovaném [integraci s server sestav Power BI](powerbi-report-server.md).

Server sestav Power BI je místní server sestav s webovým portálem, ve kterém můžete zobrazovat a spravovat sestavy. Obsahuje nástroje pro vytváření sestav Power BI, stránkované sestavy, mobilní sestavy a klíčové ukazatele výkonu. Další informace najdete v tématu [co je server sestav Power BI?](/power-bi/report-server/get-started).

## <a name="reporting-services-point"></a>Bod služby Reporting services

Bod služby Reporting Services je role systému lokality, kterou přidáte na server, na kterém běží Microsoft SQL Server Reporting Services. Bod služby Reporting Services provádí následující funkce:

- Zkopíruje definice sestavy Configuration Manager do služby Reporting Services.
- Vytvoří složky sestav založené na kategoriích sestav.
- Nastaví zásady zabezpečení pro složky sestavy a sestavy. Tyto zásady vycházejí z oprávnění na základě rolí pro Configuration Manager administrativních uživatelů. V intervalu 10 minut se bod služby Reporting Services připojí ke službě Reporting Services a znovu použije zásadu zabezpečení, pokud jste ji změnili.

Další informace o plánování a instalaci bodu služby Reporting Services najdete v následujících článcích:

- [Plánování vytváření sestav](planning-for-reporting.md)

- [Konfigurace vytváření sestav](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Sestavy nástroje Configuration Manager

Configuration Manager poskytuje definice sestav pro více než 400 sestav ve více než 50 složkách sestav. Během procesu instalace bodu služby Reporting Services je zkopíruje do kořenové složky sestavy v SQL Server Reporting Services. Konzola Configuration Manager zobrazuje sestavy a uspořádá je v podsložkách na základě kategorie sestavy.

Sestavy nešíří směrem nahoru ani dolů Configuration Manager hierarchii. Spouští se pouze s databází lokality, ve které je vytvoříte. Vzhledem k tomu, že Configuration Manager replikuje globální data v hierarchii, máte přístup k informacím v celé hierarchii v sestavách. Když sestava získá data z databáze lokality, má přístup k datům lokality pro aktuální lokalitu a podřízené lokality a ke globálním datům pro každou lokalitu v hierarchii.

Stejně jako jiné Configuration Manager objekty musí mít administrativní uživatel příslušná oprávnění ke spuštění nebo úpravě sestav. Aby bylo možné sestavu spustit, musí mít administrativní uživatel oprávnění **Spustit sestavu** pro objekt. Aby bylo možné sestavu vytvořit nebo upravit, musí mít administrativní uživatel oprávnění **Upravit sestavu** pro objekt.

### <a name="create-and-modify-reports"></a>Vytváření a úpravy sestav

Pro sestavy založené na službě Reporting Services Configuration Manager používá Microsoft SQL Server Tvůrce sestav jako výhradní Nástroj pro vytváření obsahu a úpravy pro sestavy založené na modelu a SQL. Při vytváření nebo úpravě sestavy v konzole Configuration Manager se Tvůrce sestav otevře. Další informace najdete v tématu [operace a údržba pro vytváření sestav](operations-and-maintenance-for-reporting.md).

Od verze 2002 se konzola integruje s Power BI Desktop a vytvoří nebo upraví sestavy Power BI. Další informace najdete v tématu [Vytvoření sestav Power BI](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Spouštění sestav

Při spuštění sestavy založené na službě Reporting Services v konzole Configuration Manager se otevře prohlížeč sestav a připojí se ke službě Reporting Services. Po zadání požadovaných parametrů sestavy pak služba Reporting Services vyvolá data a v prohlížeči zobrazí výsledky. Také je možné se připojit ke službě SQL Services Reporting Services, poté ke zdroji dat pro lokalitu a spustit sestavy.

Počínaje verzí 2002 se při spuštění sestavy založené na Power BI otevře ve webovém prohlížeči.

### <a name="report-prompts"></a>Výzvy sestav

Při vytváření nebo úpravě sestavy můžete nakonfigurovat výzvu nebo parametr sestavy. Při vytváření sestavy se zobrazí výzva k omezení nebo cílení dat, která sestava načítá. Sestava může obsahovat více než jednu výzvu. Ujistěte se, že jsou názvy výzev jedinečné a obsahují pouze alfanumerické znaky, které odpovídají pravidlům SQL Server pro identifikátory.

Při spuštění sestavy výzva vyžádá hodnotu požadovaného parametru. Na základě hodnoty parametru načte data sestavy. Například zpráva informace o **počítači pro určitý počítač** zobrazí výzvu k zadání názvu počítače. Služba Reporting Services předá zadanou hodnotu do proměnné definované v příkazu SQL sestavy.

### <a name="report-links"></a>Odkazy na sestavy

Odkazy na sestavy v Configuration Manager se používají ve zdrojové sestavě pro zajištění snadného přístupu k dalším datům. Například může odkazovat na podrobnější informace o jednotlivých položkách ve zdrojové sestavě. Pokud cílová sestava vyžaduje spuštění jedné nebo více výzev, zdrojová sestava musí obsahovat sloupec s příslušnými hodnotami pro jednotlivé výzvy.

Odkaz musí zadat číslo sloupce s hodnotou pro příkazový řádek. Například:

- K dispozici je jedna sestava obsahující seznam počítačů, které lokalita nedávno zjistila.
- Propojíte je s jinou sestavou, která obsahuje poslední zprávy, které lokalita obdrží pro určitý počítač.
- Vytvoříte odkaz a určíte, že sloupec `2` ve zdrojové sestavě obsahuje název počítače. Tato hodnota je pro cílovou sestavu požadovaná výzva.
- Spustíte sestavu zdrojového kódu a zobrazí se ikona odkaz vlevo od každého řádku dat.
- Vyberete ikonu na řádku a Prohlížeč sestav předá hodnotu v zadaném sloupci pro daný řádek jako hodnotu výzvy pro cílovou sestavu.

Pro sestavu můžete nakonfigurovat pouze jeden odkaz a tento odkaz se může připojit pouze k jedné cílové sestavě.

> [!WARNING]  
> Pokud přesunete cílovou sestavu do jiné složky sestavy, umístění cílové sestavy se změní. Configuration Manager neaktualizuje automaticky odkaz na sestavu ve zdrojové sestavě s novým umístěním a odkaz nebude ve zdrojové sestavě fungovat.

## <a name="report-folders"></a>Složky sestav

Složky sestav poskytují metodu pro řazení a filtrování sestav, které Configuration Manager ukládají ve službě Reporting Services. Složky sestav jsou užitečné, když máte spoustu sestav ke správě. Když nainstalujete bod služby Reporting Services, zkopíruje sestavy do služby Reporting Services a uspořádá je do více než 50 složek sestav. Složky sestav jsou pouze ke čtení. Nemůžete je upravovat v konzole Configuration Manager.

## <a name="report-subscriptions"></a>Přihlášení k odběru sestav

Přihlášení k odběru sestavy ve službě Reporting Services je opakovaný požadavek na doručení sestavy v určitou dobu nebo v reakci na událost. Zadáte v předplatném formát souboru aplikace. Přihlášení k odběru nabízí alternativu ke spuštění sestavy na vyžádání. Generování sestav na vyžádání od vás vyžaduje aktivní výběr sestavy vždy, když chcete sestavu zobrazit. Přihlášení k odběru lze tedy využít k plánování a poté automatizaci dodání sestavy.

Odběry sestav můžete spravovat v konzole Configuration Manager. Server sestav zpracuje odběry. Distribuuje je pomocí rozšíření doručování, která jsou nasazena na serveru. Ve výchozím nastavení je možné vytvářet přihlášení k odběru, která odesílají sestavy do sdílené složky nebo na e-mailovou adresu.

Další informace najdete v tématu [Správa odběrů sestav](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Tvůrce sestav

Pro sestavy založené na službě Reporting Services Configuration Manager používá Microsoft SQL Server Tvůrce sestav jako výhradní Nástroj pro vytváření obsahu a úpravy pro sestavy založené na modelu i SQL. Pokud vytvoříte nebo upravíte sestavu v konzole Configuration Manager, Tvůrce sestav otevře. Při prvním vytvoření nebo úpravě sestavy se Tvůrce sestav nainstaluje automaticky. Při spuštění nebo editaci sestav se otevře verze Tvůrce sestav přidružená nainstalované verzi SQL Serveru.  

 Instalace Tvůrce sestav přidává podporu pro více než 20 jazyků. Když spustíte Tvůrce sestav, zobrazí data v jazyce operačního systému místního počítače. Pokud Tvůrce sestav jazyk nepodporuje, zobrazí data v angličtině. Tvůrce sestav podporuje plné možnosti SQL Server Reporting Services, které zahrnují následující funkce:

- Poskytuje intuitivní prostředí pro vytváření sestav s podobným vzhledem jako aplikace Microsoft 365.  

- Nabízí flexibilní rozložení sestavy SQL Server RDL (Report Definition Language).  

- Poskytuje různé formy vizualizace dat včetně grafů a ukazatelů.  

- Nabízí bohatě formátovaná textová pole.  

- Umožňuje export do formátu aplikace Microsoft Word.  

Tvůrce sestav lze také otevřít přímo z SQL Server Reporting Services.

## <a name="report-models-in-sql-server-reporting-services"></a>Modely sestav ve službě SQL Server Reporting Services

Služba SQL Reporting Services používá modely sestav, které vám pomůžou vybrat položky z databáze Configuration Manager, které se mají zahrnout do sestav založených na modelu. Při sestavování sestavy se v modelech sestav zveřejňují pouze zadaná zobrazení a položky, ze kterých lze vybírat. Aby bylo možné sestavy založené na modelu vytvořit, musí být k dispozici alespoň jeden model sestavy.

Modely sestav mají následující funkce:

- Poskytněte logickým obchodním názvům databázová pole a zobrazení. Pro vytváření sestav nemusíte znát Configuration Manager struktury databáze.

- Logické položky skupin  

- Definujte vztahy mezi položkami.  

- Prvky zabezpečeného modelu tak, aby uživatelé s právy pro správu viděli pouze data, k jejichž zobrazení mají oprávnění.

I když Configuration Manager poskytuje ukázkové modely sestav, můžete také definovat modely sestav tak, aby splňovaly vaše podnikové požadavky. Další informace o vytváření modelů sestav najdete v tématu [vytváření vlastních modelů sestav](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Další kroky

[Plánování vytváření sestav](planning-for-reporting.md)