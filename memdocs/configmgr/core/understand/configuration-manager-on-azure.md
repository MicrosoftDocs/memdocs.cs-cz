---
title: Configuration Manager v Azure
titleSuffix: Configuration Manager
description: Informace o používání Configuration Manager v prostředí Azure.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9d398d7fddab61014547fc0f8f64cd180e58ab6
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438566"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager na Azure – Nejčastější dotazy

*Platí pro: Configuration Manager (Current Branch)*

Následující otázky a odpovědi vám pomohou pochopit, kdy použít a jak nakonfigurovat Configuration Manager v Microsoft Azure.

## <a name="general-questions"></a>Obecné dotazy
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Moje společnost se snaží přesunout co nejvíce fyzických serverů, aby bylo možné Microsoft Azure, můžu přesunout Configuration Manager servery do Azure?
To je jistě podporovaný scénář.  Podívejte se [na podporu virtualizačních prostředí pro Configuration Manager](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Výborně! Moje prostředí vyžaduje více webů. Měly by být všechny podřízené primární lokality v Azure v lokalitě centrální správy nebo v místním prostředí? Co jsou sekundární lokality?
Komunikace mezi lokalitami (replikace na základě souborů a databází) z okolí hostování v Azure. Veškerý provoz související s klientem však bude vzdálený od serverů lokality a systémů lokality. Pokud používáte rychlé a spolehlivé síťové připojení mezi Azure a intranetem s neomezeným datovým tarifem, je hostitelem veškeré infrastruktury v Azure možnost.

Pokud ale použijete měřený tarif dat a dostupnou šířku pásma nebo náklady, nebo není síťové připojení mezi Azure a intranetem rychlé nebo může být nespolehlivé, zvažte umístění konkrétních lokalit (a systémů lokality) místně a pak použijte ovládací prvky šířky pásma integrované v Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Má Configuration Manager v Azure scénář SaaS (software jako služba)?
Ne, jedná se o IaaS (infrastrukturu jako služba), protože Hostujte servery infrastruktury Configuration Manager na virtuálních počítačích Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Jaké oblasti mám věnovat pozornost při zvažování přesunu Configuration Manager infrastruktury do Azure?
Skvělý dotaz, tady jsou oblasti, které jsou při rozhodování v tomto rozhodnutí nejdůležitější. Každá z nich se prozkoumá v samostatné části tohoto tématu:
1. Sítě
2. Dostupnost
3. Výkon
4. Náklady
5. Zkušenosti uživatele

## <a name="networking"></a>Sítě
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Jak mám požadavky na síť použít ExpressRoute nebo Azure VPN Gateway?
Síť je velice důležité rozhodnutí. Síťové rychlosti a latence můžou ovlivnit funkčnost mezi serverem lokality a vzdálenými systémy lokality a všemi klientskými komunikacemi v systémech lokality. Naším doporučením je použití ExpressRoute. Ale neexistuje omezení Configuration Manager, které vám zabrání v používání Azure VPN Gateway. Z této infrastruktury byste měli pečlivě zkontrolovat požadavky (výkon, opravy, distribuce softwaru, nasazení operačního systému) a pak rozhodnout o svém rozhodnutí. Pro každé řešení je potřeba zvážit tyto věci:

- **ExpressRoute** (doporučeno)
  - Přirozené rozšíření vašeho datacentra (může spojovat více datových Center)
  - Privátní připojení mezi datacentry Azure a vaší infrastrukturou
  - Nepřekračuje veřejný Internet
  - Nabízí spolehlivost, rychlost a nižší latenci, vysoké zabezpečení
  - Nabízí až peering – rychlosti a možnosti neomezeného datového tarifu.
- **VPN Gateway**
  - Sítě VPN typu Site-to-site a Point-to-site
  - Provoz přechází přes veřejný Internet.
  - Používá protokol Internet Protocol Security (IPsec) a IKE (Internet Key Exchange) (IKE).

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute má mnoho různých možností, jako je neomezená škála vs. měření, různé možnosti rychlosti a doplněk Premium. Kterou možnost mám zvolit?
Možnosti, které vyberete, závisí na scénáři, který implementujete, a na množství dat, která plánujete distribuovat. Přenos Configuration Managerch dat lze ovládat mezi servery lokality a distribučními body, ale komunikace serveru typu Site-to-site nelze kontrolovat.   Když použijete měřený datový tarif, umístíte konkrétní lokality (a systémy lokality) místně a pomocí [předdefinovaných ovládacích prvků šířky pásma Configuration Manager](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) můžete řídit náklady na používání Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Jaké jsou požadavky na instalaci, jako jsou domény služby Active Directory? Musím stále připojovat servery lokality k doméně služby Active Directory?
Yes. Když přejdete na Azure, [podporované konfigurace](../plan-design/configs/supported-configurations.md) zůstanou stejné, včetně požadavků na službu Active Directory pro instalaci Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Beru na vyznámení s nutností připojit servery k webu k doméně služby Active Directory, ale můžu použít Azure Active Directory?
Ne, Azure Active Directory se v tuto chvíli nepodporuje. Servery lokality stále musí být členy [domény služby Windows Active Directory](../plan-design/configs/support-for-active-directory-domains.md).



## <a name="availability"></a>Dostupnost
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Jedním z důvodů, proč přesouváte infrastrukturu do Azure, je příslib vysoké dostupnosti. Můžu využít možnosti vysoké dostupnosti, jako jsou skupiny dostupnosti virtuálních počítačů Azure pro virtuální počítače, které využijete pro Configuration Manager?
Ano. Skupiny dostupnosti virtuálních počítačů Azure je možné použít k redundantním rolím systému lokality, jako jsou distribuční body nebo body správy.

Můžete je také použít pro Configuration Manager servery lokality. Například lokality centrální správy a primární lokality mohou být ve stejné skupině dostupnosti, které vám pomohou zajistit, že nebudou restartovány současně.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Jak můžu zajistit vysokou dostupnost databáze? Můžu použít Azure SQL Database? Nebo musím použít Microsoft SQL Server na virtuálním počítači?
Na virtuálním počítači je potřeba použít Microsoft SQL Server. Configuration Manager v tuto chvíli nepodporuje službu Azure SQL Server. Pro SQL Server ale můžete použít funkce, jako je Skupiny dostupnosti AlwaysOn. [Skupiny dostupnosti AlwaysOn](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) jsou doporučeny a jsou oficiálně podporovány od verze 1602 Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Můžu použít nástroje pro vyrovnávání zatížení Azure s rolemi systému lokality, jako jsou body správy nebo body aktualizace softwaru?
I když se Configuration Manager netestuje pomocí nástrojů pro vyrovnávání zatížení Azure, pokud jsou funkce pro aplikaci transparentní, nemělo by to mít žádný negativní vliv na běžné operace.


## <a name="performance"></a>Výkon
### <a name="what-factors-affect-performance-in-this-scenario"></a>Jaké faktory ovlivňují výkon v tomto scénáři?
[Velikost a typ virtuálního počítače Azure](/azure/virtual-machines/sizes), disky virtuálních počítačů Azure (doporučuje se Premium Storage, zejména u SQL Server), latence sítě a rychlost jsou nejdůležitějšími oblastmi.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Podrobnější informace o virtuálních počítačích Azure Jakou velikost virtuálních počítačů mám použít?
Obecně platí, že výpočetní výkon (procesor a paměť) musí splňovat [doporučený hardware pro Configuration Manager](../plan-design/configs/recommended-hardware.md). Existují však určité rozdíly mezi běžným hardwarem počítače a virtuálními počítači Azure, zejména pokud se nacházejí na discích, které tyto virtuální počítače používají.  Velikost používaných virtuálních počítačů závisí na velikosti vašeho prostředí, ale tady je několik doporučení:
- V produkčních nasazeních jakékoli významné velikosti doporučujeme, aby virtuální počítače Azure třídy "**S**". Důvodem je to, že můžou využívat Premium Storage disky.  Virtuální počítače třídy bez "S" používají úložiště objektů BLOB a obecně nesplňují požadavky na výkon nezbytné pro přijatelné provozní prostředí.
- K dispozici je třeba více Premium Storage disků pro vyšší škálování a v konzole pro správu disků systému Windows je možné použít maximálně IOPS.  
- Při počátečním nasazení lokality doporučujeme použít lepší nebo více prémiových disků (například P30 místo P20 a 2xP30 v prokládaném svazku namísto 1xP30). Pokud se pak váš web později potřebuje rozložit do velikosti virtuálního počítače kvůli dalšímu zatížení, můžete využít další procesor a paměť, které poskytuje větší velikost virtuálního počítače. Už budete mít ještě disky, které budou mít k dispozici i další propustnost IOPS, kterou větší velikost virtuálního počítače umožňuje.



V následujících tabulkách je seznam počátečních navrhovaných disků, které se mají využít v primárních a centrálních lokalitách pro správu s různými velikostmi instalací:

**Společně umístěná databáze lokality** – primární lokalita nebo lokalita centrální správy s databází lokality na serveru lokality:

| Desktopové klienty    |Doporučená velikost virtuálního počítače|Doporučené disky|
|--------------------|-------------------|-----------------|
|**Až 25k**       |   DS4_V2          |2xP30 (prokládané)  |
|**25k na 50 tis**      |   DS13_V2         |2xP30 (prokládané)  |
|**50 tis na 100 tisíc**     |   DS14_V2         |3xP30 (prokládané)  |


**Vzdálená databáze lokality** – primární lokalita nebo lokalita centrální správy s databází lokality na vzdáleném serveru:

| Desktopové klienty    |Doporučená velikost virtuálního počítače|Doporučené disky |
|--------------------|-------------------|------------------|
|**Až 25k**       | Webový server: F4S úrovně </br>Databázový server: DS12_V2 | Webový server: 1xP30 </br>Databázový server: 2xP30 (prokládaný)  |
|**25k na 50 tis**      | Webový server: F4S úrovně </br>Databázový server: DS13_V2 | Webový server: 1xP30 </br>Databázový server: 2xP30 (prokládaný)   |
|**50 tis na 100 tisíc**     | Webový server: F8S úrovně </br>Databázový server: DS14_V2 | Webový server: 2xP30 (prokládaný)   </br>Databázový server: 3xP30 (prokládaný)   |

V následující části najdete příklad konfigurace 50 tis pro 100 tisíc klientů na DS14_V2 s disky 3xP30 v prokládaném svazku se samostatnými logickými svazky pro Configuration Manager instalaci a soubory databáze: ![ VM).](media/vm_disks.png)  



## <a name="user-experience"></a>Zkušenosti uživatele
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Zmiňujete se, že uživatelské prostředí je jednou z hlavních oblastí důležitosti, proč je to?
Rozhodnutí týkající se sítě, dostupnosti, výkonu a místa, kde vaše Configuration Manager servery lokality mohou ovlivnit vaše uživatele přímo. Věříme, že přechod na Azure by měl být pro vaše uživatele transparentní, aby nedošlo ke změně svých každodenních interakcí s Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, zobrazí se. Mám v plánu nainstalovat jednu samostatnou primární lokalitu na virtuální počítač Azure a chci se ujistit, že jsou nízké náklady. Je vhodné umístit (vzdálené) systémy lokality (například body správy, distribuční body a body aktualizace softwaru) na virtuální počítače Azure i v místním prostředí?
S výjimkou komunikace ze serveru lokality do distribučního bodu může tato komunikace mezi servery v lokalitě nastat kdykoli a nevyužívá mechanismy k řízení používání šířky pásma sítě. Vzhledem k tomu, že nemůžete řídit komunikaci mezi systémy lokality, je třeba vzít v úvahu veškeré náklady spojené s touto komunikací.

Síťové rychlosti a latence jsou jiné faktory, které je potřeba zvážit. Pomalé nebo nespolehlivé sítě mohou ovlivnit funkčnost mezi serverem lokality a vzdálenými systémy lokality a všemi klientskými komunikacemi v systémech lokality. Také je nutné vzít v úvahu počet spravovaných klientů, kteří používají daný systém lokality, i funkce, které aktivně používáte.
Obecně platí, že je možné využít běžné pokyny, které se vztahují na propojení sítě WAN a systémy lokality jako výchozí bod. V ideálním případě bude propustnost sítě, kterou vyberete a přijímáte mezi Azure a intranetem, odpovídat síti WAN, která je dobře propojená s rychlou sítí.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>Co je distribuce obsahu a Správa obsahu? Pokud mají standardní distribuční body být v Azure nebo v místním prostředí a mám použít BranchCache nebo distribuční body pro vyžádání obsahu v místním prostředí? Nebo by se mělo používat pro cloudové distribuční body výhradně?
Přístup ke správě obsahu je stejný jako u serverů lokality a systémů lokality.
- Pokud používáte rychlé a spolehlivé síťové připojení mezi Azure a intranetem s neomezeným datovým tarifem, může být hostitelem standardních distribučních bodů v Azure možnost.
- Pokud používáte měření podle objemu dat a náklady na šířku pásma jsou obavy nebo síťové připojení mezi Azure a intranetem není rychlé nebo může být nespolehlivé, možná zvažte další přístupy. Mezi ně patří vyhledání standardu nebo distribučních bodů pro vyžádání obsahu v místním prostředí a používání služby BranchCache. Použití cloudových distribučních bodů je také možností, ale existují určitá omezení pro podporované typy obsahu (například bez podpory balíčků aktualizací softwaru).

> [!NOTE]
>  Pokud potřebujete podporu PXE nebo vícesměrového vysílání, musíte k reakci na požadavky na spuštění použít místní distribuční body (Standard nebo pull).


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>I když mám v pořádku omezení cloudových distribučních bodů, nechci do DMZ umístit svůj bod správy, i když to je potřeba pro podporu mých internetových klientů. Mám nějaké další možnosti?
Ano. V Configuration Manager verze 1610 jsme zavedli [Brána pro správu cloudu](../clients/manage/manage-clients-internet.md#cloud-management-gateway) jako funkci předběžného vydání. (Tato funkce se nejdřív objevila ve verzi Technical Preview 1606 jako [cloudová proxy služba](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)).

**Brána pro správu cloudu** poskytuje jednoduchý způsob, jak spravovat klienty Configuration Manager na internetu. Služba, která je nasazená do Microsoft Azure a vyžaduje předplatné Azure, se připojí k místní infrastruktuře Configuration Manager pomocí nové role, která se nazývá bod konektoru služby Cloud Management Gateway. Po nasazení a konfiguraci budou mít klienti přístup k místním Configuration Manager rolím systému lokality bez ohledu na to, jestli jsou připojené k interní privátní síti nebo k Internetu.

Ve svém prostředí můžete začít používat bránu pro správu cloudu a poskytnout nám svůj názor na to, abychom to mohli lépe. Informace o předběžných verzích funkcí najdete v tématu [použití předběžných verzí funkcí z aktualizací](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Také jsem slyšeli o tom, že máte další novou funkci nazvanou peer cache, která byla představena jako předběžná verze funkce verze 1610. Liší se od BranchCache? Který z nich mám zvolit?
Ano, zcela odlišně. Sdílená [mezipaměť](../plan-design/hierarchy/client-peer-cache.md) je 100% nativní Configuration Manager technologie, kde BranchCache je funkce systému Windows. Obě můžou být pro vás užitečné. Služba BranchCache využívá všesměrové vysílání k nalezení požadovaného obsahu, zatímco sdílená mezipaměť používá standardní pracovní postup distribuce a nastavení skupiny hranic pro Správce konfigurace.

Můžete nakonfigurovat libovolného klienta jako zdroj sdílené mezipaměti. Když body správy poskytují klientům informace o umístěních zdroje obsahu, poskytují podrobnosti o distribučních bodech a všech zdrojích sdílené mezipaměti s obsahem, který klient vyžaduje.


## <a name="cost"></a>Náklady
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>V části informace o nákladech se dozvíte něco. Bude toto řešení pro mě finančně výhodné?
Těžko se říká, protože každé prostředí je jiné. Nejlepší je, že se vám vaše prostředí používá Microsoft Azure cenové kalkulačky:https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Další materiály
**Základy:**https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Typy počítačů virtuálních počítačů Azure:**
- Velikosti počítačů Azure:https://docs.microsoft.com/azure/virtual-machines/sizes  
- Ceny za virtuální počítače:https://azure.microsoft.com/pricing/details/virtual-machines/  
- Ceny za Storage:https://azure.microsoft.com/pricing/details/storage/

**Požadavky na výkon disku:**    
- Úvodní disk na prémii:https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Hlubší informace o disku Premium:https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Praktická kolekce grafů pro maximální velikosti a cíle výkonu pro úložiště:https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Další Úvod + některá studená Uber data o tom, jak Premium Storage funguje za sebou:https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Dostupnosti**
- Smlouva SLA pro Azure IaaS-Time:https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Vysvětlené sady dostupnosti:https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability

**Komunikační**
- Expresní směrování vs. Azure VPN:https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Ceny expresních tras:https://azure.microsoft.com/pricing/details/expressroute/
- Další informace o expresní trase:https://azure.microsoft.com/documentation/articles/expressroute-introduction/
