---
title: Správa obsahu – základy
titleSuffix: Configuration Manager
description: Pro správu obsahu, který nasazujete, použijte nástroje a možnosti v Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8f29ed1e3201da139daeaa1fadca739ff44dc8e
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384940"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Základní koncepty správy obsahu v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje robustní systém nástrojů a možností správy obsahu softwaru. Nasazení softwaru, jako jsou aplikace, balíčky, aktualizace softwaru a nasazení operačního systému, mají veškerý obsah. Configuration Manager ukládá obsah na serverech lokality i v distribučních bodech. Tento obsah vyžaduje při přenosu mezi umístěními velký objem šířky pásma sítě. Pro efektivní plánování a používání infrastruktury správy obsahu si nejdřív Pochopte dostupné možnosti a konfigurace. Pak zvažte, jak je používat, aby nejlépe vyhovovaly potřebám vašeho síťového prostředí a nasazení obsahu.  

> [!TIP]  
> Další informace o procesu distribuce obsahu a o tom, jak najít nápovědu při diagnostice a řešení obecných problémů s distribucí obsahu, najdete v tématu [porozumění a řešení potíží s distribucí obsahu v Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

V následujících částech najdete základní koncepty správy obsahu. Pokud koncept vyžaduje další nebo komplexní informace, jsou k dispozici odkazy, které vás k nim přivedou.


## <a name="accounts-used-for-content-management"></a>Účty používané pro správu obsahu

Pro správu obsahu se dají používat následující účty:  

### <a name="network-access-account"></a>Účet přístupu k síti

Používané klienty pro připojení k distribučnímu bodu a přístup k obsahu. Ve výchozím nastavení se účet počítače zkouší jako první.  

Tento účet je používán také distribučními body pro vyžádání obsahu ke stažení obsahu ze zdrojového distribučního bodu ve vzdálené doménové struktuře.  

Počínaje verzí 1806 některé scénáře již nevyžadují účet pro přístup k síti. Můžete povolit, aby lokalita používala rozšířené protokol HTTP s ověřováním Azure Active Directory.<!--1358228-->

Další informace najdete v tématu [účet pro přístup k síti](accounts.md#network-access-account).

### <a name="package-access-account"></a>Účet pro přístup k balíčku

Ve výchozím nastavení Configuration Manager uděluje přístup k obsahu v distribučním bodě uživatelům a správcům účtů obecného přístupu. Můžete ale nakonfigurovat další oprávnění k omezení přístupu.

Další informace najdete v tématu [účet pro přístup k balíčku](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Omezení a plánování šířky pásma

Omezení i plánování jsou možnosti, pomocí kterých můžete určovat, kdy se má obsah distribuovat ze serveru lokality do distribučních bodů. Tyto možnosti jsou podobné, ale nepřímo se nevztahují na řízení šířky pásma pro replikaci na základě souborů mezi lokalitami.  

Další informace najdete v tématu [Správa šířky pásma sítě](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>Binární rozdílová replikace

Configuration Manager používá binární rozdílovou replikaci (binární ROZDÍLOVÁ replikace) k aktualizaci obsahu, který jste předtím distribuováni do jiných lokalit nebo do vzdálených distribučních bodů. Chcete-li podpořit omezení využití šířky pásma binární ROZDÍLOVÁ replikace, nainstalujte funkci **Remote Differential Compression** do distribučních bodů. Další informace najdete v tématu [požadavky na distribuční body](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq).

BINÁRNÍ ROZDÍLOVÁ replikace minimalizuje šířku pásma sítě používanou k odesílání aktualizací distribuovaného obsahu. Znovu pošle pouze nový nebo změněný obsah místo odeslání celé sady zdrojových souborů obsahu pokaždé, když tyto soubory změníte.  

Když se použije binární ROZDÍLOVÁ replikace, Configuration Manager identifikuje změny, ke kterým došlo ve zdrojových souborech pro každou sadu obsahu, kterou jste předtím rozšíříte.  

- Když se soubory ve zdrojovém obsahu změní, lokalita vytvoří novou přírůstkovou verzi obsahu. Pak replikuje pouze změněné soubory do cílových lokalit a distribučních bodů. Soubor se považuje za změněný, pokud jste ho přejmenovali nebo přesunuli, nebo pokud jste změnili obsah souboru. Pokud například nahradíte jeden soubor ovladače pro balíček ovladačů, který jste předtím rozšíříte do několika lokalit, bude replikován pouze změněný soubor ovladače.  

- Configuration Manager podporuje až pět přírůstkových verzí sady obsahu předtím, než znovu odešle celou sadu obsahu. Po páté aktualizaci dojde při další změně sady obsahu k tomu, že lokalita vytvoří novou verzi sady obsahu. Configuration Manager pak distribuuje novou verzi sady obsahu, aby nahradila předchozí sadu a všechny její přírůstkové verze. Po distribuci nové sady obsahu jsou později přírůstkové změny zdrojových souborů replikovány pomocí binární ROZDÍLOVÁ replikace.  

Binární rozdílová replikace je podporovaná mezi každou nadřazenou a podřízenou lokalitou v hierarchii. BINÁRNÍ ROZDÍLOVÁ replikace se podporuje v rámci lokality mezi serverem lokality a jeho pravidelnými distribučními body. Distribuční body pro vyžádání obsahu a distribuční body cloudu však nepodporují binární ROZDÍLOVÁ replikace k přenosu obsahu. Distribuční body pro vyžádání obsahu podporují rozdíl na úrovni souborů, převádějí nové soubory, ale ne bloky v rámci souboru.

Aplikace vždy použijí binární rozdílovou replikaci. BINÁRNÍ ROZDÍLOVÁ replikace je pro balíčky nepovinná a není ve výchozím nastavení povolená. Pokud chcete pro balíčky použít binární ROZDÍLOVÁ replikace, povolte tuto funkci pro každý balíček. Vyberte možnost **Povolit binární rozdílovou replikaci** při vytváření nebo úpravách balíčku.


### <a name="bdr-or-delta-replication"></a>BINÁRNÍ ROZDÍLOVÁ replikace nebo rozdílová replikace

<!-- SCCMDocs#1209 -->
Následující seznam shrnuje rozdíly mezi *binární rozdílovou replikací* (binární rozdílová replikace) a *rozdílovou replikací*.

#### <a name="summary-of-binary-differential-replication"></a>Shrnutí binární rozdílové replikace

- Termín Configuration Manager pro Microsoft **Remote Differential Compression**
- Rozdíly na úrovni *bloku*
- Vždy povoleno pro aplikace
- Volitelné na starších verzích balíčků
- Pokud soubor již v distribučním bodě existuje a dojde ke změně, lokalita používá binární ROZDÍLOVÁ replikace k replikaci změn na úrovni bloku místo celého souboru. Toto chování platí pouze v případě, že povolíte objektu použití binární ROZDÍLOVÁ replikace.<!-- SCCMDocs#2026 -->

#### <a name="summary-of-delta-replication"></a>Shrnutí rozdílové replikace

- Rozdíly na úrovni *souborů*
- Ve výchozím nastavení není možné konfigurovat.
- Když se balíček změní, lokalita místo celého balíčku vyhledá změny v jednotlivých souborech.
    - Pokud se soubor změní, proveďte práci pomocí binární ROZDÍLOVÁ replikace.
    - Pokud je k dispozici nový soubor, zkopírujte nový soubor.


## <a name="peer-caching-technologies"></a>Technologie pro ukládání do sdílené mezipaměti

<!-- SCCMDocs#1044 -->

Configuration Manager podporuje několik možností správy obsahu mezi partnerskými zařízeními ve stejné síti:

- [Služba BranchCache](#branchcache)
- [Optimalizace doručení](#delivery-optimization)
- [Configuration Manager sdílené mezipaměti](#peer-cache)

K porovnání hlavních funkcí těchto technologií použijte následující tabulku:

| Funkce  | Sdílená &nbsp; mezipaměť  | &nbsp;Optimalizace doručení  | Služba BranchCache  |
|---------|---------|---------|---------|
| V různých podsítích | Ano | Ano | No |
| Omezení šířky pásma | Ano (bity) | Ano (nativní) | Ano (bity) |
| Částečný obsah | Ano | Ano | Ano |
| Velikost mezipaměti ovládacího prvku na disku | Ano | Ano | Ano |
| Zjišťování zdrojů partnerského vztahu | Ruční (nastavení klienta) | Automaticky | Automaticky |
| Rovnocenné zjišťování | Přes bod správy používající skupiny hranic | DO cloudové služby | To |
| Přehledy | Řídicí panel zdrojů dat klienta | Řídicí panel zdrojů dat klienta | Řídicí panel zdrojů dat klienta |
| Řízení využití sítě WAN | Skupiny hranic | DO GroupID | Pouze podsíť |
| Podporovaný obsah | Veškerý obsah nástroje ConfigMgr | Aktualizace Windows, ovladače, aplikace pro Store | Veškerý obsah nástroje ConfigMgr |
| Řízení pomocí zásad | Nastavení agenta klienta | Nastavení agenta klienta (částečně) | Nastavení agenta klienta |

### <a name="recommendations"></a>Doporučení

- Moderní správa: Pokud už používáte moderní nástroje, jako je Intune, implementujte optimalizaci doručení

- Configuration Manager a spoluspráva: použijte kombinaci sdílené mezipaměti a Optimalizace doručení. Používejte sdílenou mezipaměť s místními distribučními body a využijte možnost optimalizace doručování pro cloudové scénáře.

- Stávající služba BranchCache byla implementována: Používejte paralelní všechny tři technologie. Pro scénáře, které služba BranchCache nepodporuje, použijte funkci sdílené mezipaměti a optimalizaci doručení.


## <a name="branchcache"></a>Služba BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) je technologie Windows. Klienti, kteří podporují službu BranchCache, stáhli nasazení, které nakonfigurujete pro BranchCache, a pak slouží jako zdroj obsahu pro jiné klienty s povolenou službou BranchCache.  

Máte například distribuční bod se systémem Windows Server 2012 nebo novějším a je nakonfigurován jako server BranchCache. Když první klient s povolenou službou BranchCache požaduje obsah z tohoto serveru, klient stáhne tento obsah a uloží ho do mezipaměti.  

- Tento klient pak zpřístupní obsah pro další klienty s povolenou službou BranchCache ve stejné podsíti, která také obsah ukládá do mezipaměti.  
- Ostatní klienti ve stejné podsíti nemusí stahovat obsah z distribučního bodu.  
- Obsah je distribuován mezi několik klientů pro budoucí přenosy.  

Další informace najdete v tématu [Podpora služby Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Optimalizace doručení

<!-- 1324696 -->
Skupiny hranic Configuration Manager slouží k definování a regulaci distribuce obsahu napříč podnikovou sítí a vzdálenými pobočkami. [Optimalizace doručení Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) je cloudová technologie peer-to-peer pro sdílení obsahu mezi zařízeními s Windows 10. Nakonfigurujte optimalizaci doručení pro použití skupin hranic při sdílení obsahu mezi partnerskými uzly. Nastavení klienta použije identifikátor skupiny hranic jako identifikátor skupiny Optimalizace doručení na klientovi. Když klient komunikuje s cloudovou službou Optimalizace doručení, používá tento identifikátor k vyhledání partnerských uzlů s obsahem. Další informace najdete v tématu Nastavení klienta [Optimalizace doručení](../../clients/deploy/about-client-settings.md#delivery-optimization) .

Optimalizace doručování je doporučená technologie pro optimalizaci doručování aktualizací Windows 10 souborů Expresní instalace pro aktualizace kvality Windows 10. Počínaje verzí 1910 je internetový přístup k cloudové službě Optimalizace doručení k disConfiguration Manager požadavek na využití funkce peer-to-peer. Informace o potřebných koncových bodech internetu najdete v tématu [Nejčastější dotazy k optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). Optimalizaci lze použít pro všechny aktualizace systému Windows. Další informace najdete v tématu [optimalizace doručování aktualizací Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).


## <a name="microsoft-connected-cache"></a>Microsoft Connected Cache

<!--3555764-->
Počínaje verzí 1906 můžete nainstalovat server Microsoft Connected cache do distribučních bodů. Uložením tohoto obsahu do mezipaměti v místním prostředí můžou vaši klienti těžit z funkce Optimalizace doručení, ale můžete přispět k ochraně WAN Links.

> [!NOTE]
> Počínaje verzí 1910 je tato funkce nyní označována jako **propojená s mezipamětí Microsoft**. Dříve byla známá jako Optimalizace doručení v síťové mezipaměti.

Tento server mezipaměti funguje jako transparentní mezipaměť na vyžádání pro obsah stažený optimalizací doručení. Pomocí nastavení klienta se ujistěte, že je tento server nabízen pouze členům místní skupiny hranic Configuration Manager.

Tato mezipaměť je oddělená od obsahu distribučního bodu Configuration Manager. Pokud zvolíte stejnou jednotku jako role distribučního bodu, uloží se obsah samostatně.

Další informace najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Sdílená mezipaměť

Sdílená mezipaměť klienta vám pomůže spravovat nasazení obsahu do klientů ve vzdálených umístěních. Peer cache je integrované Configuration Manager řešení, které umožňuje klientům sdílet obsah s jinými klienty přímo z místní mezipaměti.

Napřed nasaďte nastavení klienta, které povoluje sdílenou mezipaměť pro kolekci. Potom můžou členové této kolekce fungovat jako zdroj obsahu rovnocenného pro ostatní klienty ve stejné skupině hranic.

Od verze 1806 mohou zdroje sdílené mezipaměti klienta rozdělit obsah na části. Tyto části minimalizují přenos v síti, aby se snížilo využití sítě WAN. Bod správy poskytuje podrobnější sledování částí obsahu. Pokusí se odstranit více než jedno stažení stejného obsahu pro jednu skupinu hranic.<!--1357346-->

Další informace najdete v tématu sdílená [mezipaměť pro klienty Configuration Manager](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Sdílená mezipaměť prostředí Windows PE

Když nasadíte nový operační systém s Configuration Manager, můžou počítače, které spouštějí pořadí úkolů, používat sdílenou mezipaměť prostředí Windows PE. Stahují obsah ze zdroje sdílené mezipaměti místo z distribučního bodu. Toto chování pomáhá minimalizovat provoz v síti WAN ve scénářích firemní pobočky, kde není k dispozici žádný místní distribuční bod.

Další informace najdete v tématu sdílená [mezipaměť prostředí Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>LEDBAT Windows

<!--1358112-->
LEDBAT (prodloužení prodlevy na pozadí systému Windows) je funkce řízení zahlcení sítě systému Windows Server, která usnadňuje správu přenosů v síti na pozadí. U distribučních bodů běžících na podporovaných verzích Windows serveru povolte možnost upravit síťový provoz. Pak budou klienti používat šířku pásma sítě jenom v případě, že jsou k dispozici.

Další informace o LEDBAT Windows najdete v příspěvku na novém blogu o [přenosech](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) .

Další informace o tom, jak používat Windows LEDBAT Configuration Manager s distribučními body, najdete v nastavení pro **úpravu rychlosti stahování pro použití nevyužité šířky pásma sítě (Windows LEDBAT)** při [konfiguraci obecných nastavení distribučního bodu](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Umístění obsahu

Klienti přistupují k obsahu z těchto umístění:  

- **Intranet** (místní):  

    - Distribuční body můžou používat protokol HTTP nebo HTTPs.  

    - Pro zálohu použít jenom distribuční bod cloudu, pokud nejsou místní distribuční body k dispozici.  

- **Internet**:  

    - Vyžaduje internetové distribuční body pro příjem HTTPS.  

    - Může používat distribuční bod cloudu nebo bránu pro správu cloudu (CMG).  

        Od verze 1806 může CMG také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure. Další informace najdete v tématu [Úprava CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md).

- **Pracovní skupina**:  

    - Vyžaduje, aby distribuční body přijímaly protokol HTTPS.  

    - Může používat cloudový distribuční bod nebo CMG.  


## <a name="content-source-priority"></a>Priorita zdroje obsahu

Když klient potřebuje obsah, provede požadavek na umístění obsahu do bodu správy. Bod správy vrátí seznam zdrojových umístění, která jsou platná pro požadovaný obsah. Tento seznam se liší v závislosti na konkrétním scénáři, používaných technologiích, návrhu lokality, skupinách hranic a nastavení nasazení. Například když je spuštěno pořadí úloh, kompletní klient Configuration Manager vždy neběží, takže chování se může lišit.<!-- SCCMDocs#1960 -->

Následující seznam obsahuje všechna možná umístění zdroje obsahu, která může klient Configuration Manager použít, v pořadí, ve kterém je bude upřednostňovat:  

1. Distribuční bod ve stejném počítači jako klient nástroje
2. Partnerský zdroj ve stejné podsíti sítě
3. Distribuční bod ve stejné podsíti sítě
4. Partnerský zdroj ve stejné skupině hranic
5. Distribuční bod v aktuální skupině hranic
6. Distribuční bod v sousední skupině hranic nakonfigurovaný pro nouzové
7. Distribuční bod ve výchozí skupině hranic lokality
8. Cloudová služba web Windows Update
9. Internetový distribuční bod
10. Cloudový distribuční bod v Azure

> [!Note]  
> <!-- SCCMDocs#1607 -->Pro toto stanovení priorit zdroje není Optimalizace doručení platná. Tento seznam ukazuje, jak Configuration Manager klient najde obsah. Agent web Windows Update stahuje obsah pro optimalizaci doručení. Pokud agent web Windows Update nenalezne obsah, použije ho tento seznam k vyhledání v Configuration Manager klient.

## <a name="content-library"></a>Knihovna obsahu

Knihovna obsahu je úložiště obsahu s jednou instancí v Configuration Manager. V této knihovně se zmenší celková velikost obsahu, který distribuujete.  

- Přečtěte si další informace o [knihovně obsahu](the-content-library.md).
- Pomocí [Nástroje pro vyčištění knihovny obsahu](content-library-cleanup-tool.md) můžete odebrat obsah, který už není přidružený k aplikaci.  


## <a name="distribution-points"></a>Distribuční body

Configuration Manager používá distribuční body k ukládání souborů, které jsou požadovány pro spuštění softwaru na klientských počítačích. Klienti musí mít přístup aspoň k jednomu distribučnímu bodu, ze kterého můžou stahovat soubory pro obsah, který nasazujete.  

Základní (Nespecializovaný) distribuční bod se obvykle označuje jako standardní distribuční bod. Existují dvě varianty standardního distribučního bodu, které vyžadují zvláštní pozornost:  

- **Distribuční bod pro vyžádání**obsahu: variace distribučního bodu, kde distribuční bod získává obsah z jiného distribučního bodu (zdrojového distribučního bodu). Tento proces se podobá tomu, jak klienti stahují obsah z distribučních bodů. Distribuční body pro vyžádání obsahu vám pomohou vyhnout se kritickým bodům šířky pásma sítě, ke kterým dochází, když server lokality musí přímo distribuovat obsah do každého distribučního bodu. [Použijte distribuční bod pro vyžádání](use-a-pull-distribution-point.md)obsahu.

- **Distribuční bod cloudu**: variace distribučního bodu, který je nainstalován v Microsoft Azure. [Naučte se používat cloudový distribuční bod](use-a-cloud-based-distribution-point.md).  

Standardní distribuční body podporují řadu konfigurací a funkcí:  

- K řízení tohoto přenosu použijte ovládací prvky, jako jsou **plány** nebo **omezení šířky pásma** .  

- K minimalizaci a řízení spotřeby sítě použijte další možnosti, včetně **připraveného obsahu**a **distribučních bodů pro vyžádání** obsahu.  

- Služba **BranchCache**, **mezipaměť sdílené mezipaměti**a **Optimalizace doručení** jsou technologie peer-to-peer, které snižují šířku pásma sítě, která se používá při nasazování obsahu.  

- Existují různé konfigurace pro nasazení operačního systému, například **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** a **[vícesměrové vysílání](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** .  

- Možnosti pro **mobilní zařízení**  
  
Cloudové a distribuční body pro vyžádání obsahu podporují mnohé z těchto konfigurací, ale mají omezení, která jsou specifická pro jednotlivé varianty distribučních bodů.  


## <a name="distribution-point-groups"></a>Skupiny distribučních bodů

Skupiny distribučních bodů jsou logické skupiny distribučních bodů, které mohou zjednodušit distribuci obsahu.  

Další informace najdete v tématu [Správa skupin distribučních bodů](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## <a name="distribution-point-priority"></a>Priorita distribučního bodu

Hodnota priority distribučního bodu je založená na tom, jak dlouho trval přenos předchozích nasazení do tohoto distribučního bodu.  

- Tato hodnota je samoobslužné vyladění. Je nastavená na všech distribučních bodech, které vám pomůžou Configuration Manager rychleji přenášet obsah do více distribučních bodů.  

- Když distribuujete obsah do několika distribučních bodů současně nebo do skupiny distribučních bodů, lokalita nejprve pošle obsah serveru s nejvyšší prioritou. Pak tento stejný obsah odešle do distribučního bodu s nižší prioritou.  

- Priorita distribučního bodu nenahrazuje prioritu distribuce pro balíčky. Priorita balíčku zůstává rozhodujícím faktorem, kdy lokalita odesílá jiný obsah.  

Máte například balíček s vysokou prioritou balíčku. Distribuujete ji na server s nízkou prioritou distribučního bodu. Tento balíček s vysokou prioritou vždy přenáší před balíček s nižší prioritou. Priorita balíčku platí i v případě, že lokalita distribuuje balíčky s nižší prioritou na servery s vyššími prioritami distribučních bodů.

Vysoká priorita balíčku zajišťuje, že Configuration Manager distribuuje daný obsah do distribučních bodů předtím, než pošle všechny balíčky s nižší prioritou.  

> [!NOTE]  
> Distribuční body pro vyžádání obsahu taky používají koncept priority za účelem uspořádání pořadí zdrojových distribučních bodů.  
>
> - Priorita distribučního bodu pro přenosy obsahu na server se liší od priority, kterou používají distribuční body pro vyžádání obsahu. Distribuční body pro vyžádání obsahu používají prioritu při hledání obsahu ze zdrojového distribučního bodu.  
> - Další informace najdete v tématu [použití distribučního bodu pro vyžádání](use-a-pull-distribution-point.md)obsahu.  


## <a name="fallback"></a>Záložní volba

U Configuration Manager aktuální větve se změnily několik věcí tak, jak klienti hledají distribuční bod s obsahem, včetně záložního.

Klienti, kteří nemůžou najít obsah z distribučního bodu, který je přidružený ke své aktuální skupině hranic, se vrátí k použití zdrojových umístění obsahu přidružených ke skupinám sousedních hranic. Aby bylo možné použít záložní skupinu, musí mít sousední hraniční skupina definovanou relaci s aktuální skupinou hranic daného klienta. Tento vztah zahrnuje nakonfigurovaný čas, který musí uplynout před tím, než klient, který nemůže najít obsah místně, zahrnuje zdroje obsahu ze sousední skupiny hranic jako součást svého hledání.

Koncepty upřednostňovaných distribučních bodů již nejsou používány a nastavení pro možnost **Povolení záložních zdrojových umístění obsahu** již nejsou k dispozici ani k vykonání.

Další informace najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Šířka pásma sítě

Pro lepší správu šířky pásma sítě, která se používá při distribuci obsahu, můžete použít následující možnosti:  

- **Připravený obsah**: přenos obsahu do distribučního bodu bez distribuce obsahu napříč sítí.  

- **Plánování a omezování**: konfigurace, které vám pomůžou řídit, kdy a jak se obsah distribuuje do distribučních bodů.  

Další informace najdete v tématu [Správa šířky pásma sítě](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>Rychlost síťového připojení ke zdroji obsahu

U Configuration Manager aktuální větve se změnily několik věcí tak, jak klienti hledají distribuční bod s obsahem. Tyto změny zahrnují rychlost sítě pro zdroj obsahu.

Rychlosti síťového připojení, které definují distribuční bod jako **rychlé** nebo **pomalé** , se už nepoužívají. Místo toho se každý systém lokality, který je přidružený ke skupině hranic, považuje za stejný.

Další informace najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>Distribuce obsahu na vyžádání

Distribuce obsahu na vyžádání je možnost pro jednotlivá nasazení aplikací a balíčků. Tato možnost povolí distribuci obsahu na vyžádání na upřednostňované servery.  

- Pokud chcete toto nastavení Povolit pro nasazení, povolte: **distribuovat obsah pro tento balíček do preferovaných distribučních bodů**.  

- Pokud povolíte tuto možnost pro nasazení a klient požaduje obsah, ale obsah není dostupný na žádném z upřednostňovaných distribučních bodů klienta, Configuration Manager automaticky distribuuje tento obsah do upřednostňovaných distribučních bodů klienta.  

- I když se tato událost aktivuje Configuration Manager k automatické distribuci obsahu do upřednostňovaných distribučních bodů daného klienta, klient může obsah získat z jiných distribučních bodů předtím, než preferované distribuční body klienta nasazení obdrží. Když k tomuto chování dojde, obsah bude v tomto distribučním bodě k dispozici pro použití dalším klientem, který bude toto nasazení Hledat.  

Další informace najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Správce přenosu balíčků

Správce přenosu balíčků je součást serveru lokality, která přenáší obsah do distribučních bodů v jiných počítačích.  

Další informace najdete v tématu [správce přenosu balíčků](package-transfer-manager.md).  


## <a name="prestage-content"></a>Příprava obsahu

Příprava obsahu je proces přenosu obsahu do distribučního bodu bez distribuce obsahu napříč sítí.  

Další informace najdete v tématu [Správa šířky pásma sítě](manage-network-bandwidth.md).
