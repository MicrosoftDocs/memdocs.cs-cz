---
title: Úvod do aktualizací softwaru
titleSuffix: Configuration Manager
description: Seznamte se se základy aktualizací softwaru v Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: bd384edafd6464073b33a593a56bc88ba2fb0b87
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906768"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Seznámení s aktualizacemi softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace softwaru v Configuration Manager poskytují sadu nástrojů a prostředků, které vám pomůžou spravovat složitý úkol sledování a použití aktualizací softwaru na klientských počítačích v podniku. Účinný proces správy aktualizací softwaru je nutný k udržení provozní účinnosti, řešení problémů zabezpečení a udržení stability síťové infrastruktury. Ale kvůli měnící se povaze technologie a neustálému výskytu nových hrozeb zabezpečení vyžaduje účinná správa aktualizací softwaru důslednou a nepřetržitou pozornost.  

Ukázkový scénář, který ukazuje, jak můžete nasadit aktualizace softwaru ve vašem prostředí, najdete v tématu [vzorový scénář nasazení aktualizací zabezpečení softwaru](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a>Synchronizace aktualizací softwaru  
 Synchronizace aktualizací softwaru v nástroji Configuration Manager se připojuje k Microsoft Update a načítá metadata aktualizací softwaru. Lokalita nejvyšší úrovně (lokalita centrální správy nebo samostatná primární lokalita) se synchronizuje s Microsoft Update podle plánu nebo když ručně spustíte synchronizaci z konzoly Configuration Manager. Když Configuration Manager dokončí synchronizaci aktualizací softwaru v lokalitě nejvyšší úrovně, spustí se synchronizace aktualizací softwaru v podřízených lokalitách, pokud existují. Když se synchronizace dokončí ve všech primárních nebo sekundárních lokalitách, vytvoří se zásady v rámci lokalit, které poskytují body aktualizací softwaru pro klientské počítače.  

> [!NOTE]  
>  Ve výchozím klientském nastavení jsou aktualizace softwaru povolené. Ale pokud nastavíte klientské nastavení **Povolit aktualizace softwaru na klientech** na hodnotu **Ne** k zakázání aktualizací softwaru v kolekci nebo ve výchozím nastavení, přidruženým klientům se nebude posílat umístění pro body aktualizací softwaru. Podrobnosti najdete v tématu [nastavení klienta aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#software-updates).  

 Když klient obdrží zásady, spustí kontrolu kompatibility aktualizací softwaru a zapisuje informace do služby Windows Management Instrumentation (WMI). Informace o kompatibilitě se pak posílají do bodu správy, který je pak zasílá do serveru lokality. Další informace o vyhodnocování kompatibility najdete v části [Software updates compliance assessment](#BKMK_SUMCompliance) v tomto tématu.  

 V primární lokalitě můžete nainstalovat několik bodů aktualizace softwaru. První bod aktualizací softwaru, který nainstalujete, se nakonfiguruje jako zdroj synchronizace. Tím se synchronizuje z Microsoft Update nebo serveru WSUS, který není ve vaší Configuration Manager hierarchii. Ostatní body aktualizací softwaru v lokalitě používají tento první bod aktualizací softwaru jako zdroj synchronizace.  

> [!NOTE]  
>  Když je proces synchronizace aktualizací softwaru v lokalitě nejvyšší úrovně dokončený, replikují se metadata aktualizací softwaru do podřízených lokalit pomocí replikace databáze. Když připojíte konzolu Configuration Manager k podřízené lokalitě, Configuration Manager zobrazí metadata aktualizace softwaru. Nicméně dokud nenainstalujete a nenakonfigurujete bod aktualizace softwaru v lokalitě, klienti nebudou kontrolovat kompatibilitu aktualizací softwaru, nebudou nahlásit informace o kompatibilitě Configuration Manager a nebudete moct úspěšně nasadit aktualizace softwaru.  

### <a name="synchronization-on-the-top-level-site"></a>Synchronizace v lokalitě nejvyšší úrovně  
 Proces synchronizace aktualizací softwaru v lokalitě nejvyšší úrovně získává ze služby Microsoft Update metadata aktualizací softwaru, která splňují kritéria určená ve vlastnostech možnosti Součást bodu aktualizací softwaru. Kritéria můžete nakonfigurovat jenom v lokalitě nejvyšší úrovně.  

> [!NOTE]  
>  Jako zdroj synchronizace můžete zadat existující server WSUS, který není v hierarchii Configuration Manager, nikoli Microsoft.  

 Následující seznam popisuje základní kroky procesu synchronizace v lokalitě nejvyšší úrovně:  

1.  Spouštění synchronizace aktualizací softwaru.  

2.  Správce synchronizace služby WSUS zasílá požadavek do služby WSUS spuštěné v bodě aktualizací softwaru k spuštění synchronizace pomocí služby Microsoft Update.  

3.  Metadata aktualizací softwaru se synchronizují ze služby Microsoft Update a veškeré změny se přidají nebo aktualizují v databázi služby WSUS.  

4.  Až služba WSUS dokončí synchronizaci, Správce synchronizace služby WSUS synchronizuje metadata aktualizací softwaru z databáze WSUS do databáze Configuration Manager a všechny změny po poslední synchronizaci budou vloženy nebo aktualizovány v databázi lokality. Metadata aktualizací softwaru jsou uložená v databázi lokality jako položka konfigurace.  

5.  Položky konfigurace aktualizací softwaru se posílají do podřízených lokalit pomocí replikace databáze.  

6.  Po úspěšném dokončení synchronizace vytvoří nástroj správce synchronizace WSUS stavovou zprávu 6702.  

7.  Správce synchronizace služby WSUS posílá požadavek na synchronizaci do všech podřízených lokalit.  

8.  Správce synchronizace služby WSUS posílá požadavky po jednom do služby WSUS spuštěné v dalších bodech aktualizací softwaru v lokalitě. Servery služby WSUS v ostatních bodech aktualizací softwaru jsou nakonfigurované jako repliky služby WSUS spuštěné ve výchozím bodě aktualizací softwaru v lokalitě.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Synchronizace v podřízených primárních a sekundárních lokalitách  
 Během procesu synchronizace aktualizací softwaru v lokalitě nejvyšší úrovně se položky konfigurace aktualizací softwaru replikují do podřízených lokalit pomocí replikace databáze. Na konci procesu posílá lokalita nejvyšší úrovně požadavek na synchronizaci do podřízené lokality a podřízená lokalita spouští synchronizaci služby WSUS. Následující seznam uvádí základní kroky procesu synchronizace v podřízené primární lokalitě nebo v sekundární lokalitě:  

1.  Správce synchronizace služby WSUS přijímá požadavek na synchronizaci z lokality nejvyšší úrovně.  

2.  Spouštění synchronizace aktualizací softwaru.  

3.  Správce synchronizace služby WSUS vytváří požadavek na službu WSUS spuštěnou v bodě aktualizací softwaru k spuštění synchronizace.  

4.  Služba WSUS spuštěná v bodě aktualizací softwaru v podřízené lokalitě synchronizuje metadata aktualizací softwaru ze služby WSUS spuštěné v bodě aktualizací softwaru v nadřazené lokalitě.  

5.  Po úspěšném dokončení synchronizace vytvoří nástroj správce synchronizace WSUS stavovou zprávu 6702.  

6.  Z primární lokality posílá správce synchronizace služby WSUS požadavek na synchronizaci do všech podřízených sekundárních lokalit. Sekundární lokalita spouští synchronizaci aktualizací softwaru s nadřazenou primární lokalitou. Sekundární lokalita je nakonfigurovaná jako replika služby WSUS spuštěné v nadřazené lokalitě.  

7.  Správce synchronizace služby WSUS posílá požadavky po jednom do služby WSUS spuštěné v dalších bodech aktualizací softwaru v lokalitě. Servery služby WSUS v ostatních bodech aktualizací softwaru jsou nakonfigurované jako repliky služby WSUS spuštěné ve výchozím bodě aktualizací softwaru v lokalitě.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a>Vyhodnocení kompatibility aktualizací softwaru  
 Před nasazením aktualizací softwaru do klientských počítačů v nástroji Configuration Manager spusťte hledání shody aktualizací softwaru v klientských počítačích. Pro každou aktualizaci softwaru se vytvoří stavová zpráva, která obsahuje stav kompatibility pro danou aktualizaci. Stavové zprávy se hromadně posílají do bodu správy a pak do serveru lokality, kde se stav kompatibility přidá do databáze lokality. Stav dodržování předpisů pro aktualizace softwaru se zobrazí v konzole Configuration Manager. Aktualizace softwaru můžete nasazovat a instalovat na počítačích, které vyžadují aktualizace. Následující části poskytují informace o stavech kompatibility a popisují proces kontroly kompatibility aktualizací softwaru.  

### <a name="software-updates-compliance-states"></a>Stavy kompatibility aktualizací softwaru  
 Následující seznam popisuje všechny stavy dodržování předpisů, které se zobrazují v konzole Configuration Manager pro aktualizace softwaru.  

-   **Požadováno**  

     Určuje, že aktualizace softwaru je aplikovatelná a požaduje se na klientském počítači. Jakákoli z následujících podmínek může být pravdivá, když má stav aktualizací softwaru hodnotu **Požadována**:  

    -   Aktualizace softwaru se na klientský počítač nenasadila.  

    -   Aktualizace softwaru se nainstalovala na klientský počítač. Nejnovější stavová zpráva se zatím nepřidala do databáze na serveru lokality. Klientský počítač znovu kontroluje aktualizaci po dokončení instalace. Zpoždění až dvě minuty se může vyskytovat předtím, než klient zašle aktualizovaný stav do bodu správy, který pak odesílá aktualizovaný stav do serveru lokality.  

    -   Aktualizace softwaru se nainstalovala na klientský počítač. Instalace aktualizací softwaru požaduje restart počítače předtím, než se aktualizace dokončí.  

    -   Aktualizace softwaru se nasadila na klientský počítač, ale ještě se nenainstalovala.  

-   **Nepožadováno**  

     Určuje, že aktualizace softwaru na klientském počítači není aplikovatelná. Proto se aktualizace softwaru nevyžaduje.  

-   **Nainstalovaný**  

     Určuje, že aktualizace softwaru na klientském počítači je aplikovatelná a že klientský počítač už má aktualizaci softwaru nainstalovanou.  

-   **Není známo**  

     Určuje, že server lokality neobdržel stavovou zprávu z klientského počítače, obvykle v důsledku následujících situací:  

    -   Klientský počítač provedl neúspěšnou kontrolu kompatibility aktualizací softwaru.  

    -   Kontrola na klientském počítači se dokončila úspěšně. Ale stavová zpráva se zatím nezpracovala na serveru lokality, pravděpodobně kvůli nevyřízené úloze stavové zprávy.  

    -   Kontrola na klientském počítači se úspěšně dokončila, ale nedošlo k přijetí stavové zprávy z podřízené lokality.  

    -   Kontrola na klientském počítači se úspěšně dokončila, ale soubor stavové zprávy se nějakým způsobem poškodil a nedal se zpracovat.  

### <a name="scan-for-software-updates-compliance-process"></a>Kontrola procesu kompatibility aktualizací softwaru  
 Když je bod aktualizace softwaru nainstalovaný a synchronizovaný, vytvoří se zásady počítače na úrovni lokality, které informují klientské počítače, které Configuration Manager aktualizace softwaru pro lokalitu povolené. Když klient obdrží zásady počítačů, naplánuje se náhodné spouštění kontroly vyhodnocení kompatibility v příštích dvou hodinách. Když se kontrola spustí, proces agenta klienta aktualizací softwaru vymaže historii kontrol, předloží požadavek k vyhledání serveru služby WSUS, který se použije pro kontrolu, a aktualizuje místní zásady skupiny pro umístění serveru služby WSUS.  

> [!NOTE]  
>  Internetoví klienti se musí připojit k serveru služby WSUS přes protokol SSL.  

 Agentovi webu Windows Update (WUA) se předá žádost o vyhledávání. Agent WUA se pak připojí k umístění serveru WSUS, který je uvedený v místní zásadě, získá metadata aktualizace softwaru, která se synchronizovala na serveru WSUS, a vyhledá v klientském počítači aktualizace. Proces Klientského agenta aktualizace softwaru zjistí, že se vyhledávání shody dokončilo, a vytvoří stavové zprávy pro jednotlivé aktualizace softwaru se změněným stavem shody od posledního vyhledávání. Stavové zprávy se hromadně posílají do bodu správy každých 15 minut. Bod správy je pak předá serveru lokality, kde se vloží do databáze serveru lokality.  

 Po úvodním vyhledávání shody aktualizací softwaru se vyhledávání spouští podle nastaveného plánu vyhledávání. Pokud ale klient vyhledával shodu aktualizací softwaru v časovém intervalu zadaném v hodnotě Time to Live (TTL), použije klient metadata aktualizace softwaru uložená v místním počítači. Pokud poslední vyhledávání proběhlo mimo interval TTL, musí se klient připojit ke službě WSUS spuštěné v bodě aktualizace softwaru a metadata aktualizace softwaru uložená v klientovi aktualizovat.  

 Vyhledávání shody aktualizací softwaru (včetně plánu vyhledávání) se dá spustit takto:  

-   **Plán vyhledávání aktualizací softwaru**: Vyhledávání dodržování předpisů u aktualizací softwaru se spustí podle plánu vyhledávání nakonfigurovaného v nastavení Klientský agent aktualizace softwaru. Další informace o konfiguraci nastavení klienta aktualizace softwaru najdete v tématu [nastavení klienta aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Akce Vlastnosti nástroje Configuration Manager**: Na kartě **Akce** v dialogovém okně **Vlastnosti nástroje Configuration Manager** může uživatel v klientském počítači spustit akci **Cyklus prověřování aktualizací softwaru** nebo **Cyklus hodnocení nasazení aktualizací softwaru** .  

-   **Plán nového vyhodnocení nasazení**: Vyhodnocení nasazení a vyhledávání dodržování předpisů u aktualizací softwaru se spouští podle plánu nového vyhodnocení nasazení, nakonfigurovaného v nastavení Klientský agent aktualizace softwaru. Další informace o nastavení klienta aktualizace softwaru najdete v tématu [nastavení klienta aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Před stažením souborů aktualizace**: Když klientský počítač obdrží zásadu přiřazování k nově požadovanému nasazení, Klientský agent aktualizace softwaru stáhne soubory aktualizace softwaru do místní mezipaměti klienta. Než se spustí stahování souborů aktualizace softwaru, spustí klientský agent vyhledávání s cílem ověřit, že se aktualizace softwaru ještě vyžaduje.  

-   **Před nainstalováním aktualizace softwaru**: Než se nainstaluje aktualizace softwaru, spustí Klientský agent aktualizace softwaru vyhledávání s cílem ověřit, že se aktualizace softwaru ještě vyžadují.  

-   **Po nainstalování aktualizace softwaru**: Hned po dokončení instalace aktualizace softwaru Klientský agent aktualizace softwaru spustí vyhledávání s cílem ověřit, že se už nevyžadují aktualizace softwaru, a vytvoří novou stavovou zprávu s informací, že se nainstalovala aktualizace softwaru. Pokud se instalace dokončila, ale vyžaduje se restartování, stavová zpráva obsahuje informaci, že se čeká na restartování klientského počítače.  

-   **Po restartování systému**: Pokud se k dokončení instalace aktualizace softwaru vyžaduje restartování systému klientského počítače, spustí Klientský agent aktualizace softwaru po restartu vyhledávání s cílem ověřit, že se už nevyžadují aktualizace softwaru, a vytvoří stavovou zprávu s informací, že se nainstalovala aktualizace softwaru.  

#### <a name="time-to-live-value"></a>Hodnota Time to Live (TTL)  
 Metadata aktualizace softwaru vyžadovaná k vyhledávání shody aktualizací softwaru se ukládají v místním klientském počítači a ve výchozím nastavení zůstávají platná po dobu maximálně 24 hodin. Tato hodnota se nazývá Time to Live (TTL).  

#### <a name="scan-for-software-updates-compliance-types"></a>Vyhledávání typů shody aktualizací softwaru  
 Klient vyhledává shodu aktualizací softwaru pomocí online nebo offline vyhledávání a vynuceného nebo nevynuceného vyhledávání, a to podle způsobu spuštění vyhledávání shody aktualizací softwaru. Následující popis popisuje, které metody spuštění kontroly jsou online nebo offline a zda je kontrola vynucená nebo Nevynucená.  

-   **Plán vyhledávání aktualizací softwaru** (Nevynucená online kontrola)  

     V případě nastaveného plánu vyhledávání se klient připojí ke službě WSUS spuštěné v bodě aktualizace softwaru, a pokud poslední vyhledávání proběhlo mimo interval TTL, získá metadata aktualizace softwaru.  

-   Cyklus **prověřování aktualizací softwaru** nebo **cyklus hodnocení nasazení aktualizací softwaru** (vynucená online kontrola)  

     Klientský počítač se vždycky připojuje ke službě WSUS spuštěné v bodě aktualizace softwaru a získává metadata aktualizace softwaru, než klientský počítač vyhledá shodu aktualizací softwaru. Po dokončení vyhledávání se počítadlo TTL vynuluje. Příklad: Pokud je TTL 24 hodin a uživatel spustí vyhledávání shody aktualizací softwaru, resetuje se limit TTL na odpočítávání 24 hodin.  

-   **Plán nového vyhodnocení nasazení** (Nevynucená online kontrola)  

     V případě nastaveného plánu nového vyhodnocení nasazení se klient připojí ke službě WSUS spuštěné v bodě aktualizace softwaru, a pokud poslední vyhledávání proběhlo mimo interval TTL, získá metadata aktualizace softwaru.  

-   **Před stažením souborů aktualizací** (není vynucená online kontrola)  

     Než klient může stáhnout soubory aktualizace v požadovaných nasazeních, připojí se ke službě WSUS spuštěné v bodě aktualizace softwaru, a pokud poslední vyhledávání proběhlo mimo interval TTL, získá metadata aktualizace softwaru.  

-   **Před instalací aktualizace softwaru** (není vynucená online kontrola)  

     Než klient nainstaluje aktualizace softwaru v požadovaných nasazeních, připojí se ke službě WSUS spuštěné v bodě aktualizace softwaru, a pokud poslední vyhledávání proběhlo mimo interval TTL, získá metadata aktualizace softwaru.  

-   **Po instalaci aktualizace softwaru** (vynucená offline kontrola)  

     Po nainstalování aktualizace softwaru spustí Klientský agent aktualizace softwaru vyhledávání na základě místních metadat. Klient se nikdy nepřipojuje ke službě WSUS spuštěné v bodě aktualizace softwaru za účelem získání metadat aktualizace softwaru.  

-   **Po restartování systému** (vynucená offline kontrola)  

     Po nainstalování aktualizace softwaru a restartování počítače spustí Klientský agent aktualizace softwaru vyhledávání na základě místních metadat. Klient se nikdy nepřipojuje ke službě WSUS spuštěné v bodě aktualizace softwaru za účelem získání metadat aktualizace softwaru.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Balíčky pro nasazení aktualizace softwaru  
 Balíček pro nasazení aktualizací softwaru je nástroj sloužící ke stažení aktualizací softwaru do sdílené síťové složky a zkopírování zdrojových souborů aktualizace softwaru do knihovny obsahů na serverech lokality a v distribučních bodech, které jsou definované v nasazení. Pomocí Průvodce stažením aktualizací můžete stáhnout aktualizace softwaru a přidat je do balíčků pro nasazení ještě před samotným nasazením. Pomocí tohoto průvodce můžete zřídit aktualizace softwaru v distribučních bodech a ověřit, že tato část nasazení proběhla úspěšně, než nasadíte aktualizace softwaru do klientů.  

 Pokud nasazujete stažené aktualizace softwaru pomocí Průvodce nasazením aktualizace softwaru, nasazení automaticky využije balíček pro nasazení obsahující aktualizace softwaru. Pokud se nasazují aktualizace softwaru, které se nestáhly, je potřeba v Průvodci nasazením aktualizace softwaru zadat nový nebo existující balíček pro nasazení a aktualizace softwaru se stáhnou po dokončení průvodce.  

> [!IMPORTANT]  
>  Než v průvodci vyberete sdílenou síťovou složku pro zdrojové soubory balíčku pro nasazení, musíte tuto složku ručně vytvořit. Každý balíček pro nasazení musí používat vlastní sdílenou síťovou složku.  

> [!IMPORTANT]  
>  Účet počítače poskytovatele serveru SMS i správce, který stahuje aktualizace softwaru, musí mít ke zdroji balíčku oprávnění **Číst** . Pokud chcete snížit riziko manipulace se zdrojovými soubory aktualizací softwaru ve zdroji balíčku, omezte přístup ke zdroji balíčku.  

 Při vytvoření nového balíčku pro nasazení se nastaví verze obsahu na hodnotu 1, která se změní až se stažením aktualizací softwaru. Při stažení souborů aktualizace softwaru pomocí balíčku se verze obsahu zvýší na 2. Proto všechny nové balíčky pro nasazení začínají s verzí obsahu 2. Pokaždé, když se v balíčku pro nasazení změní obsah, verze obsahu se zvýší o 1. Další informace najdete v tématu [základní koncepty správy obsahu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 Klienti instalují aktualizace softwaru v nasazení prostřednictvím distribučního bodu, ve kterém jsou dostupné aktualizace softwaru, bez ohledu na balíček pro nasazení. I když dojde ke smazání balíčku pro nasazení pro aktivní nasazení, klienti můžou nainstalovat aktualizace softwaru v nasazení za podmínky, že se jednotlivé aktualizace stáhly aspoň do jednoho balíčku nasazení a jsou dostupné v distribučním bodě, ke kterému má klient přístup. Až když se smaže poslední balíček nasazení obsahující aktualizaci softwaru, nebudou klientské počítače moct získat aktualizaci softwaru, dokud se aktualizace znovu nestáhne do balíčku pro nasazení. Pokud nejsou soubory aktualizace v balíčcích pro nasazení, zobrazují se aktualizace softwaru v konzole Configuration Manager červenou šipkou. Pokud nasazení obsahuje aktualizace s tímto stavem, je označené dvěma červenými šipkami.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Pracovní postupy nasazení aktualizací softwaru  
 Ve vašem prostředí existují dva základní scénáře nasazení aktualizací softwaru: ruční a automatické nasazení. Běžně se aktualizace softwaru nasazují ručně, aby se vytvořila základna pro klientské počítače, a pak se aktualizace softwaru v klientech spravují pomocí automatických nasazení. Následující části podávají přehled o postupech ručního a automatického nasazení aktualizací softwaru.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Ruční nasazení aktualizací softwaru  
 Ruční nasazení aktualizací softwaru je proces výběru aktualizací softwaru v konzole Configuration Manager a ruční spuštění procesu nasazení. Tato metoda nasazení se běžně využívá v případě, že chcete do klientských počítačů distribuovat požadované aktualizace softwaru, než vytvoříte pravidla automatického nasazení, která budou řídit průběžné měsíční nasazování aktualizací softwaru, nebo že nasazujete vzdálené požadavky aktualizací softwaru. Následující seznam shrnuje obecný postup ručního nasazení aktualizací softwaru:  

1.  Vyfiltrování aktualizací softwaru využívajících konkrétní požadavky. Můžete třeba zadat kritéria, na základě kterých se získají všechny bezpečnostní nebo kritické aktualizace softwaru vyžadované na víc než 50 klientských počítačích.  

2.  Vytvoření skupiny aktualizací softwaru, která obsahuje aktualizace softwaru.  

3.  Stažení obsahu aktualizací softwaru ve skupině aktualizací softwaru.  

4.  Ruční nasazení skupiny aktualizací softwaru.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Automatické nasazení aktualizací softwaru  
 Automatické nasazení aktualizací softwaru se konfiguruje pomocí pravidel automatického nasazení (ADR). Tato metoda nasazení se běžně využívá k pravidelným měsíčním aktualizacím softwaru (tzv. Patch Tuesday) a ke správě aktualizací definic. Při spuštění pravidla se aktualizace softwaru odeberou ze skupiny aktualizací softwaru (v případě použití existující skupiny), aktualizace softwaru splňující zadané kritérium (třeba všechny aktualizace softwaru zabezpečení vydané minulý týden) se přidají do skupiny aktualizací softwaru, soubory obsahu pro aktualizace softwaru se stáhnou a zkopírují do distribučních bodů a aktualizace softwaru se nasadí do klientských počítačů v cílové kolekci. Následující seznam shrnuje obecný postup automatického nasazení aktualizací softwaru:  

1. Vytvoření pravidla automatického nasazení, které definuje nastavení nasazení, třeba:  

   -   Cílová kolekce  

   -   Určete, jestli se má povolit nasazení nebo oznámení o shodě aktualizací softwaru pro klientské počítače v cílové kolekci  

   -   Kritéria aktualizací softwaru  

   -   Plány vyhodnocení a nasazení  

   -   Uživatelské prostředí  

   -   Vlastnosti stahování  

2. Aktualizace softwaru se přidají do skupiny aktualizací softwaru.  

3. Skupina aktualizací softwaru se nasadí do klientských počítačů v cílové kolekci (pokud je kolekce určená).  

   Určete, jaká strategie nasazení se má ve vašem prostředí použít. Můžete třeba vytvořit pravidlo automatického nasazení a cílit na kolekci testovacích klientů. Až ověříte, že se aktualizace softwaru nainstalovaly v testovací skupině, můžete do pravidla přidat nové nasazení nebo změnit stávající pravidlo nasazení tak, aby cílilo na kolekci s větším počtem klientů. Objekty aktualizace softwaru, které vytvářejí pravidla automatického nasazení, jsou interaktivní.  

- Aktualizace softwaru, které se nasadily pomocí pravidla automatického nasazení, se automaticky nasadí do nových klientů přidaných do cílové kolekce.  

- Nové aktualizace softwaru, přidané do skupiny aktualizací softwaru, se automaticky nasadí do klientů v cílové kolekci.  

- U pravidla automatického nasazení se dá nasazení kdykoli zapnout nebo vypnout.  

  Do pravidla automatického nasazení, které jste už vytvořili, se taky můžou přidávat další nasazení. To vám může pomoct zvládnout složité nasazení různých aktualizací do různých kolekcí. Každé nové nasazení má plný rozsah funkcí a možností monitorování. Každé nové nasazení, které přidáte:  

- Používá stejnou skupinu aktualizací a balíček, který se vytvoří při prvním spuštění ADR.  

- Může určovat jinou kolekci.  

- Podporuje jedinečné vlastnosti nasazení včetně vlastností:  

  -   Čas aktivace  

  -   Termín  

  -   Zobrazení nebo skrytí činnosti koncového uživatele  

  -   Samostatné výstrahy pro toto nasazení  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a>Proces nasazení aktualizace softwaru  
 Po nasazení aktualizace softwaru nebo po spuštění pravidla automatického nasazení, které nasadí aktualizace softwaru, se do zásady počítače pro lokalitu přidá zásada přiřazení nasazení. Aktualizace softwaru se stáhnou z umístění stahování, z internetu nebo ze sdílené síťové složky do zdroje balíčku. Aktualizace softwaru se zkopírují ze zdroje balíčku do knihovny obsahu na serveru lokality a pak do knihovny obsahu v distribučním bodě.  

 Když klientský počítač v cílové kolekci pro nasazení obdrží zásadu počítače, dojde ke spuštění skenování hodnocení agenta klienta aktualizace softwaru. Agent klienta stáhne obsah pro požadované aktualizace softwaru z distribučního bodu do místní mezipaměti klienta v nastavení **Čas dostupnosti softwaru** pro nasazení a potom jsou k dispozici aktualizace softwaru pro instalaci. Softwarové aktualizace ve volitelných nasazeních (nasazení, která neobsahují termín instalace), se nestáhnou, dokud uživatel ručně instalaci nespustí.  

 Když uplyne konfigurovaný termín, agent klienta softwarových aktualizací provede vyhledávání a ověří, jestli jsou softwarové aktualizace stále potřeba. Pak zkontroluje místní mezipaměť v klientském počítači a ověří, jestli jsou zdrojové soubory aktualizovaného softwaru stále k dispozici. Nakonec klient nainstaluje softwarové aktualizace. Pokud se obsah odstranil z mezipaměti klienta, aby uvolnil prostor pro další nasazení, klient softwarové aktualizace znovu stáhne z distribučního bodu do mezipaměti klienta. Softwarové aktualizace se vždycky stahují do mezipaměti klienta nezávisle na maximální nakonfigurované velikosti mezipaměti klienta. Po dokončení instalace agent klienta ověří, jestli už nejsou softwarové aktualizace potřeba a pak odešle stavovou zprávu do bodu správy, aby oznámil, že jsou softwarové aktualizace nainstalované v klientovi.  

### <a name="required-system-restart"></a>Požadované restartování systému  
 Ve výchozím nastavení, když jdou softwarové aktualizace z požadovaného nasazení nainstalovány v klientském počítači a restart systému je nutný k dokončení instalace, dojde k zahájení restartu systému. Pro softwarové aktualizace, které byly nainstalovány před termínem, je automatický restart systému posunut až do konečného termínu, není-li počítač z nějakého důvodu restartován dříve. Restart systému lze potlačit u serverů a pracovních stanic. Tato nastavení jsou konfigurována na stránce **Zkušenosti uživatele** průvodce aktualizací nasazením softwaru nebo průvodce pravidly vytváření automatických aktualizací.  

### <a name="deployment-reevaluation-cycle"></a>Cyklus nového vyhodnocení nasazení  
 Ve výchozím nastavení spustí klientské počítače cyklus opětovného hodnocení nasazení každých 7 dní. Během tohoto cyklu hodnocení klientský počítač hledá softwarové aktualizace, které byly dříve nasazeny a nainstalovány. Pokud jakékoliv softwarové aktualizace chybí, jsou softwarové aktualizace přeinstalovány z místní mezipaměti. Pokud již není softwarová aktualizace dostupná v místní mezipaměti, bude stažena z distribučního bodu a pak nainstalována. Plán opětovného hodnocení můžete konfigurovat na stránce **Softwarové aktualizace** v nastavení klienta lokality.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a>Podpora zařízení se systémem Windows Embedded, která používají filtry zápisu  
 Pokud nasadíte softwarové aktualizace do zařízení se systémem Windows, která mají povolený filtr zápisu, můžete určit, zda chcete v zařízení deaktivovat filtr zápisu během nasazení a po nasazení pak zařízení restartovat. Pokud není filtr zápisu zakázán, bude software nasazen do dočasného překrytí a po restartu zařízení již nebude software nainstalován, pokud další nasazení nevynutí změny natrvalo.  

> [!NOTE]  
>  Pokud zavádíte aktualizaci softwaru na vložené zařízení Windows, zkontrolujte, že zařízení je součástí kolekce, která má nakonfigurované okno údržby. Tato funkce umožňuje řídit, kdy je filtr zápisu zakázán a povolen a kdy se zařízení restartuje.  

 Nastavení zkušeností uživatele, které ovládá chování filtru zápisu, představuje zaškrtávací políčko s názvem **Použít změny v konečném termínu nebo během okna údržby (vyžaduje restart)**.  

 Další informace o tom, jak Configuration Manager spravuje vložená zařízení, která používají filtry zápisu, najdete v tématu [Plánování nasazení klientů na zařízení se systémem Windows Embedded](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a>Rozšiřování aktualizací softwaru v Configuration Manager  
 Pomocí System Center Updates Publisher můžete spravovat aktualizace softwaru, které nejsou k dispozici Microsoft Update. Po publikování aktualizací softwaru na server aktualizací a synchronizaci aktualizací softwaru v Configuration Manager můžete nasadit aktualizace softwaru pro klienty Configuration Manager. Další informace o nástroji Updates Publisher najdete v tématu [Updates publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

## <a name="next-steps"></a>Další kroky
[Plánování aktualizací softwaru](../plan-design/plan-for-software-updates.md)
