---
title: Mezipaměť sdílené klienta
titleSuffix: Configuration Manager
description: Při nasazování obsahu pomocí Configuration Manager použít sdílenou mezipaměť klienta pro zdrojová umístění.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d0bd136278053ded38d0d6ed4cfe4059ffe3037
ms.sourcegitcommit: 0ec6d8dabb14f20b1d84f7b503f1b03aac2a30d4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2020
ms.locfileid: "89479310"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Sdílená mezipaměť pro klienty Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1101436-->
Použití sdílené mezipaměti vám umožní spravovat nasazení obsahu na klienty ve vzdálených umístěních. Peer cache je integrované Configuration Manager řešení, které umožňuje klientům sdílet obsah s jinými klienty přímo z místní mezipaměti.   

> [!Note]  
> Ve výchozím nastavení ve verzi 1906 Configuration Manager tuto funkci povolí. Verze 1902 nebo starší Configuration Manager ve výchozím nastavení tuto volitelnou funkci nepovoluje. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Přehled

Definici  

- **Klient sdílené mezipaměti**: libovolný klient Configuration Manager, který stahuje obsah z partnerského zařízení.  

- **Zdroj sdílené mezipaměti**: klient Configuration Manager, který povolíte pro sdílenou mezipaměť, a který má obsah ke sdílení s ostatními klienty.  

Pomocí nastavení klienta můžete klientům povolit ukládání zdrojů sdílené mezipaměti. Nemusíte umožňovat klienty sdílené mezipaměti. Když klientům povolíte, aby byli zdroji sdílené mezipaměti, bod správy je zahrne do seznamu zdrojů umístění obsahu.<!--510397--> Další informace o tomto procesu najdete v tématu [operace](#operations).  

Zdroj sdílené mezipaměti musí být členem aktuální skupiny hranic klienta sdílené mezipaměti. Bod správy nezahrnuje zdroje sdílené mezipaměti ze sousední skupiny hranic v seznamu zdrojů obsahu, které poskytuje klientovi. Zahrnuje pouze distribuční body ze sousedních hraničních skupin. Další informace o aktuálních a sousedních skupinách hranic najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

Klient Configuration Manager používá sdílenou mezipaměť pro obsluhu dalších klientů, které mají každý typ obsahu v mezipaměti. Tento obsah zahrnuje Microsoft 365 aplikace pro podnikové soubory a soubory Expresní instalace.<!--SMS.500850-->  

Sdílená mezipaměť nenahrazuje použití jiných řešení, jako je Windows BranchCache nebo Optimalizace doručení. Sdílená mezipaměť spolupracuje spolu s dalšími řešeními. Tyto technologie poskytují více možností pro rozšíření tradičních řešení pro nasazení obsahu, jako jsou třeba distribuční body. Sdílená mezipaměť je vlastní řešení bez spoléhání na BranchCache. Pokud službu BranchCache nepovolíte nebo nepoužíváte, sdílená mezipaměť pořád funguje.  

> [!Note]  
> Počínaje verzí 1802 je služba Windows BranchCache vždy povolena při nasazení. Nastavení, které **povolí klientům sdílet obsah s ostatními klienty ve stejné podsíti** , se odebere.<!--SCCMDocs issue 539--> Pokud distribuční bod tuto funkci podporuje a je povolen v nastavení klienta, klienti používají službu BranchCache. Další informace najdete v tématu [Konfigurace služby BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Operace

Pro povolení sdílené mezipaměti nasaďte [nastavení klienta](#bkmk_settings) do kolekce. Pak členové této kolekce fungují jako zdroj sdílené mezipaměti pro ostatní klienty ve stejné skupině hranic.  

- Klient, který pracuje jako zdroj obsahu rovnocenného obsahu, odesílá do svého bodu správy seznam dostupného obsahu uložený v mezipaměti pomocí stavových zpráv. Klient zdroje obsahu s partnerským obsahem také pošle stavovou zprávu do bodu správy, když odebírá obsah z místní mezipaměti.

   > [!NOTE]
   > V [Configuration Manager se v seznamu stavových zpráv](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) zobrazí seznam platných zpráv o stavu partnerského obsahu s ID 7200, 7201, 7202 a 7203.

- Jiný klient ve stejné skupině hranic vytvoří požadavek na umístění obsahu do bodu správy. Server vrátí seznam potenciálních zdrojů obsahu. Tento seznam obsahuje všechny zdroje sdílené mezipaměti s obsahem a je online. Zahrnuje taky distribuční body a další umístění zdrojů obsahu v této skupině hranic. Další informace najdete v tématu [Priorita zdroje obsahu](fundamental-concepts-for-content-management.md#content-source-priority).  

- V obvyklých případech klient, který hledá obsah, vybere jeden zdroj ze zadaného seznamu. Klient se pak pokusí získat obsah.  

Od verze 1806 obsahují skupiny hranic další nastavení, která vám poskytnou větší kontrolu nad distribucí obsahu ve vašem prostředí. Další informace najdete v tématu [Možnosti hraniční skupiny pro rovnocenné soubory ke stažení](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Pokud se klient vrátí do sousední hraniční skupiny pro obsah, bod správy nepřidá zdroje sdílené mezipaměti ze sousední hraniční skupiny do seznamu potenciálních zdrojových umístění obsahu.  

Vyberte pouze klienti, kteří jsou nejvhodnější jako zdroje sdílené mezipaměti. Vyhodnocení vhodnosti klienta na základě atributů, jako je typ skříně, místo na disku a připojení k síti. Další informace, které vám pomůžou vybrat nejlepší klienty pro použití pro sdílenou mezipaměť, najdete v [tomto blogu od Microsoft konzultanta](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801).


### <a name="limited-access-to-a-peer-cache-source"></a>Omezený přístup ke zdroji sdílené mezipaměti  

Zdroj sdílené mezipaměti odmítne požadavky na obsah, pokud splňuje některou z následujících podmínek v době, kdy partner požaduje obsah:  

- Režim nízké baterie  

- Zatížení procesoru překračuje 80%  

- Vstup/výstup disku má *AvgDiskQueueLength* , který překračuje 10.  

- K počítači nejsou k dispozici žádná další připojení.  

> [!Tip]  
> Tato nastavení nakonfigurujte pomocí serverové třídy služby WMI pro konfiguraci klienta pro funkci zdroje peer (*SMS_WinPEPeerCacheConfig*) v sadě Configuration Manager SDK.  

Když zdroj sdílené mezipaměti odmítne požadavek na obsah, klient sdílené mezipaměti pokračuje v hledání obsahu ze svého seznamu zdrojových umístění obsahu.   



## <a name="requirements"></a>Požadavky

- Sdílená mezipaměť podporuje všechny verze systému Windows uvedené jako podporované v [podporovaných operačních systémech pro klienty a zařízení](../configs/supported-operating-systems-for-clients-and-devices.md). Operační systémy jiné než Windows nejsou podporované jako zdroje sdílené mezipaměti nebo klienti sdílené mezipaměti.  

- Zdroj sdílené mezipaměti musí být klient Configuration Manager připojený k doméně. Klient, který není připojený k doméně, ale může získat obsah ze zdroje sdílené mezipaměti připojené k doméně.  

- Klienti mohou stahovat obsah pouze ze zdrojů sdílené mezipaměti v aktuální hraniční skupině.  

- [Účet přístupu k síti](accounts.md#network-access-account) není vyžadován s následující výjimkou:  

  - Nakonfigurujte účet přístupu k síti v lokalitě, když klient s povolenou sdílenou mezipamětí spustí pořadí úkolů z centra softwaru a restartuje se na spouštěcí bitovou kopii. Když je zařízení v systému Windows PE, používá účet pro přístup k síti k získání obsahu ze zdroje sdílené mezipaměti.  

  - V případě potřeby použije zdroj sdílené mezipaměti účet přístupu k síti k ověření požadavků na stažení od partnerských uzlů. Tento účet vyžaduje pro tento účel pouze oprávnění uživatele domény.  

- V případě verze 1802 a dřívější odeslání posledního zjišťování prezenčního signálu klienta Určuje aktuální hranici zdroje sdílené mezipaměti. Klient, který se při roamingu do jiné skupiny hranic, může i nadále být členem své bývalé hraniční skupiny pro účely sdílené mezipaměti. Výsledkem tohoto chování je, že klient nabízí zdroj sdílené mezipaměti, který není v bezprostředním umístění v síti. Nepovolujte cestovní klienty jako zdroj sdílené mezipaměti.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > Počínaje verzí 1806 je Configuration Manager efektivnější při určování, zda byl zdroj sdílené mezipaměti připojen do jiného umístění. Tím se zajistí, že bod správy nabízí jako zdroj obsahu pro klienty v novém umístění a ne na starém místě. Pokud používáte funkci sdílené mezipaměti s cestovními zdroji sdílené mezipaměti, po aktualizaci lokality na verzi 1806 aktualizujte také všechny zdroje sdílené mezipaměti na nejnovější verzi klienta. Bod správy nezahrnuje tyto zdroje sdílené mezipaměti v seznamu umístění obsahu, dokud nebudou aktualizovány alespoň na verzi 1806.<!--SCCMDocs issue 850-->  

- Před pokusem o stažení obsahu bod správy nejprve ověří, zda je zdroj sdílené mezipaměti online.<!--sms.498675--> K ověření dojde prostřednictvím "rychlého kanálu" pro klientské oznámení, které používá port TCP 10123.<!--511673-->  

> [!Note]  
> Pokud chcete využívat nové funkce Configuration Manager, nejdřív aktualizujte klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a> Nastavení klienta sdílené mezipaměti

Další informace o nastavení klienta sdílené mezipaměti najdete v tématu [nastavení mezipaměti klienta](../../clients/deploy/about-client-settings.md#client-cache-settings). 

Další informace o konfiguraci těchto nastavení najdete v tématu [Konfigurace nastavení klienta](../../clients/deploy/configure-client-settings.md).

U klientů s povolenými partnerskými mezipaměť, kteří používají bránu Windows Firewall, Configuration Manager konfiguruje porty brány firewall, které zadáte v nastavení klienta.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a> Částečná podpora stahování
<!--1357346-->
Od verze 1806 mohou zdroje sdílené mezipaměti klienta dělit obsah do částí. Tyto části minimalizují přenos v síti, aby se snížilo využití sítě WAN. Bod správy poskytuje podrobnější sledování částí obsahu. Pokusí se odstranit více než jedno stažení stejného obsahu pro jednu skupinu hranic. 


### <a name="example-scenario"></a>Ukázkový scénář

Contoso má jednu primární lokalitu se dvěma skupinami hranic: ústředí (sídel) a firemní pobočky. Mezi skupinami hranic existuje záložní vztah mezi 30 minutami. Bod správy a distribuční bod pro lokalitu nástroje jsou pouze na hranici sídel. Umístění pobočky nemá žádný místní distribuční bod. Dva ze čtyř klientů na pobočce jsou nakonfigurováni jako zdroje sdílené mezipaměti. 

![Diagram konfigurace sítě, jak je popsáno v ukázkovém scénáři](media/1357346-peer-cache-source-parts.png)

1. Cílíte na nasazení s využitím obsahu na všechny čtyři klienty na pobočce. Obsah jste rozšíříte pouze do distribučního bodu.  

2. Client3 a Client4 nemají pro nasazení místní zdroj. Bod správy instruuje klienty, aby čekali 30 minut, než se vrátí do skupiny vzdálených hranic.  

3. KLIENT1 (PCS1) je prvním zdrojem sdílené mezipaměti, který aktualizuje zásady pomocí bodu správy. Vzhledem k tomu, že je tento klient povolen jako zdroj sdílené mezipaměti, bod správy ho instruuje, aby ihned zahájil stahování části A z distribučního bodu.  

4. Když počítač KLIENT2 (PCS2) kontaktuje bod správy, protože součást A již ještě není dokončena, bod správy ji vydá pokyn, aby hned zahájil stahování části B z distribučního bodu.  

5. PCS1 dokončí stahování části a a okamžitě se upozorní na bod správy. V případě, že část B již probíhá, ale ještě není dokončena, bod správy ji instruuje, aby zahájil stahování části C z distribučního bodu.  

6. PCS2 dokončí stahování části B a okamžitě se upozorní na bod správy. Bod správy dá pokyn ke spuštění stahování části D z distribučního bodu.  

7. PCS1 dokončí stahování části C a okamžitě se upozorní na bod správy. Bod správy je informuje o tom, že ze vzdáleného distribučního bodu nejsou k dispozici žádné další části. Bod správy dá pokyn ke stažení části B od svého místního partnera PCS2.  

8. Tento proces pokračuje, dokud oba zdroje sdílené mezipaměti klienta všechny části navzájem navzájem. Bod správy určuje prioritu částí ze vzdáleného distribučního bodu před tím, než dáte pokyn pro zdroje sdílené mezipaměti, aby stahoval součásti z místních partnerských uzlů.  

9. Client3 je první k aktualizaci zásad po vypršení platnosti záložního období 30 minut. Nyní se vrátí s bodem správy, který informuje klienta o nových místních zdrojích. Místo stažení obsahu z distribučního bodu v síti WAN stáhne obsah v plném rozsahu z jednoho ze zdrojů sdílené mezipaměti klienta. Klienti mají prioritu místních partnerských zdrojů. 

> [!Note]  
> Pokud je počet zdrojů sdílené mezipaměti klienta větší než počet částí obsahu, pak bod správy vydá další zdroje sdílené mezipaměti, aby čekal na záložní použití jako normálního klienta. 


### <a name="configure-partial-download"></a>Konfigurace částečného stahování

1. Nastavte [skupiny hranic](../../servers/deploy/configure/boundary-groups.md) a zdroje sdílené mezipaměti na normální.  

2. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte možnost **lokality**. Na pásu karet klikněte na **Nastavení hierarchie** .  

3. Na kartě **Obecné** povolte možnost **Konfigurace zdrojů sdílené mezipaměti klienta pro rozdělení obsahu na části**.  

4. Vytvořte požadované nasazení s obsahem.  

   > [!Note]  
   > Tato funkce funguje pouze v případě, že klient stáhne obsah na pozadí, například s požadovaným nasazením. Stahování na vyžádání, například když uživatel nainstaluje dostupné nasazení v centru softwaru, se chová jako obvykle.  

Pokud se chcete podívat, jak se stahují obsah v částech, Prohlédněte si soubor **ContentTransferManager. log** ve zdroji sdílené mezipaměti klienta a **MP_Location. log** v bodu správy.  



## <a name="guidance-for-cache-management"></a>Doprovodné materiály ke správě mezipaměti
<!--510645-->
Sdílená mezipaměť spoléhá na sdílení obsahu v mezipaměti klienta Configuration Manager. Při správě mezipaměti klienta ve vašem prostředí Vezměte v úvahu následující body:  

- Mezipaměť klienta Configuration Manager není podobná knihovně obsahu v distribučním bodě. Když spravujete obsah, který distribuujete do distribučního bodu, klient Configuration Manager automaticky spravuje obsah v mezipaměti. Existují nastavení a metody, které vám pomůžou určit, jaký obsah je v mezipaměti zdroje sdílené mezipaměti. Další informace najdete v tématu [Konfigurace mezipaměti klienta pro klienty Configuration Manager](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- Normální velikost mezipaměti a údržba se vztahují na zdroje sdílené mezipaměti. Další informace najdete v tématu [Konfigurace velikosti mezipaměti klienta](../../clients/deploy/about-client-settings.md#configure-client-cache-size). Vezměte v úvahu velikost většího obsahu, jako jsou balíčky pro upgrade operačního systému nebo soubory aktualizací Windows 10 Express. Porovnejte potřebu tohoto obsahu s dostupným místem na disku u zdrojů sdílené mezipaměti.  

- Klient zdroje sdílené mezipaměti aktualizuje poslední odkaz na obsah v mezipaměti, když ho partner stáhne. Klient používá toto časové razítko, když automaticky udržuje svou mezipaměť a nejprve odebírá starší obsah. Proto by měl čekat na odebrání obsahu, který klienti sdílené mezipaměti častěji stahují.  

- V případě potřeby můžete během pořadí úloh nasazení operačního systému zachovat obsah v mezipaměti klienta pomocí proměnné **SMSTSPreserveContent** . Další informace najdete v tématu [proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent).  

- Pokud je to nutné, při vytváření následujícího softwaru použijte možnost **zachovat obsah v mezipaměti klienta**:  
  - Aplikace
  - Balíčky
  - Image operačního systému
  - Balíčky s upgradem operačního systému
  - Spouštěcí image



## <a name="monitoring"></a>Monitorování   

Abyste porozuměli použití sdílené mezipaměti, zobrazte si řídicí panel **zdroje dat klienta** . Další informace najdete v tématu [řídicí panel zdrojů dat klienta](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

Pomocí sestav můžete také zobrazit použití sdílené mezipaměti. V konzole nástroje přejdete do pracovního prostoru **monitorování** , rozbalíte **vytváření sestav**a vyberete uzel **sestavy** . Všechny následující sestavy mají typ **obsahu distribuce softwaru**:  

1.  **Odmítnutí obsahu zdroje sdílené mezipaměti**: jak často zdroje sdílené mezipaměti v hraniční skupině odmítnou požadavek na obsah.  

    > [!Note]  
    > **Známý problém**<!--486652-->: Při přechodu k podrobnostem o výsledcích, jako je *MaxCPULoad* nebo *MaxDiskIO*, se může zobrazit chyba, která navrhuje sestavu nebo podrobnosti nejde najít. Pokud chcete tento problém obejít, použijte další dvě sestavy, které přímo zobrazují výsledky.  

2. Požadavek **na odmítnutí obsahu zdroje sdílené mezipaměti**: zobrazuje podrobnosti odmítnutí pro zadanou skupinu hranic nebo typ zamítnutí. 

    > [!Note]  
    > **Známý problém**<!--486652-->: Nemůžete vybrat z dostupných parametrů a místo toho je musí zadat ručně. Zadejte hodnoty pro *název skupiny hranic* a *typ zamítnutí* , jak je vidět v sestavě **odmítnutí obsahu zdroje sdílené mezipaměti** . Například pro *typ odmítnutí* můžete zadat *MaxCPULoad* nebo *MaxDiskIO*.  

3. **Podrobnosti odmítnutí obsahu zdroje sdílené mezipaměti**: zobrazit obsah, který klient požadoval při zamítnutí.  

    > [!Note]  
    > **Známý problém**<!--486652-->: Nemůžete vybrat z dostupných parametrů a místo toho je musí zadat ručně. Zadejte hodnotu pro *typ odmítnutí* , jak se zobrazuje ve zprávě o **odmítnutí obsahu zdroje sdílené mezipaměti** . Pak zadejte *ID prostředku* pro zdroj obsahu, o kterém chcete získat další informace. 
    > 
    > Vyhledání ID zdroje obsahu:  
    > 
    > 1. Ve výsledcích sestavy **odmítnutí obsahu zdroje sdílené mezipaměti** vyhledejte název počítače, který se zobrazí jako *zdroj sdílené mezipaměti* .  
    > 
    > 2. V pracovním prostoru **prostředky a kompatibilita** vyberte uzel **zařízení** a vyhledejte název tohoto počítače. Použijte hodnotu ze sloupce ID prostředku.  

