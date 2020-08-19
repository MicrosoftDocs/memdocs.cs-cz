---
title: Optimalizace doručování aktualizací Windows 10
titleSuffix: Configuration Manager
description: Naučte se používat Configuration Manager ke správě obsahu aktualizace, aby zůstal aktuální s Windows 10.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e832feb6f5a56225cd63a0b0d6290fc0c70e53a
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591550"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Optimalizace doručování aktualizací Windows 10 pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

U mnoha zákazníků začíná mít úspěšná cesta k získání a aktuálnosti aktuální pomocí měsíčních aktualizací Windows 10 dobrou strategii distribuce obsahu pomocí Configuration Manager. Velikost měsíčních aktualizací kvality může být příčinou obav pro velké organizace. K dispozici je několik dostupných technologií, které mají za cíl snížit šířku pásma a zatížení sítě pro optimalizaci aktualizace. Tento článek vysvětluje tyto technologie, porovnává je a poskytuje doporučení, která vám pomůžou s rozhodováním, která z nich se mají použít.  
 
Windows 10 nabízí několik typů aktualizací. Další informace najdete v tématu [aktualizace typů v web Windows Update pro firmy](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Tento článek se zaměřuje na aktualizace *kvality* Windows 10 s Configuration Manager. 


## <a name="express-update-delivery"></a>Doručení Express Update

Soubory ke stažení aktualizací kvality Windows 10 můžou být velké. Každý balíček obsahuje všechny dřív vydané opravy, které zajišťují konzistenci a jednoduchost. Microsoft dokáže zmenšit velikost obsahu aktualizace Windows 10, který každý klient stáhne, pomocí funkce s názvem Express. Express se dnes používá miliony zařízení, která získávají aktualizace přímo z web Windows Update služby, a významně snižuje velikost stahovaných dat. Tato výhoda je dostupná i pro zákazníky, jejichž klienti nestahují přímo z web Windows Update služby. 

Configuration Manager přidat podporu [souborů Expresní instalace](manage-express-installation-files-for-windows-10-updates.md) aktualizací kvality Windows 10 ve verzi 1702. Pro nejlepší prostředí však doporučujeme použít Configuration Manager verze 1802 nebo novější. Pro dosažení nejlepšího výkonu při stahování je také vhodné použít Windows 10 verze 1703 nebo novější. 

> [!NOTE]  
> Obsah verze Express je podstatně větší než verze v plném formátu. Soubor rychlé instalace obsahuje všechny možné variace pro každý soubor, který je určen k aktualizaci. V důsledku toho se požadované množství místa na disku zvýší na aktualizace ve zdroji balíčku aktualizace a v distribučních bodech, pokud povolíte Express support v Configuration Manager. I když se zvyšuje požadavek na místo na disku v distribučních bodech, zmenší se velikost obsahu, který klienti stáhnou z těchto distribučních bodů. Klienti stáhnou jenom bity, které vyžadují (rozdílové), ale ne celou aktualizaci.


## <a name="peer-to-peer-content-distribution"></a>Distribuce obsahu peer-to-peer

I když klienti stáhnou jenom ty části obsahu, které vyžadují, urychlí aktualizace Windows ve vašem prostředí tím, že využívají distribuci obsahu peer-to-peer. Využití partnerských vztahů jako zdroje stahování pro aktualizace kvality může být výhodné pro prostředí, kde místní distribuční body nejsou přítomny ve vzdálených pobočkách. Toto chování brání nutnosti všem klientům stahovat obsah ze vzdáleného distribučního bodu přes pomalé připojení WAN. Použití partnerských vztahů může být užitečné i v případě, že se klienti můžou do služby web Windows Update zavázat. K stažení obsahu aktualizace z cloudu a jeho zpřístupnění ostatním zařízením je potřeba jenom jeden partner.

Configuration Manager podporuje mnoho technologií peer-to-peer, včetně následujících:
- Optimalizace doručení Windows
- Configuration Manager sdílené mezipaměti
- Služba BranchCache systému Windows  

Další části poskytují další informace o těchto technologiích.

### <a name="windows-delivery-optimization"></a>Optimalizace doručení Windows

[Optimalizace doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) je hlavní technologie ke stažení a metoda distribuce peer-to-peer, která je integrovaná do Windows 10. Klienti s Windows 10 můžou získat obsah z jiných zařízení v místní síti, které stáhnou stejné aktualizace. Pomocí [možností Windows dostupných pro optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)můžete nakonfigurovat klienty do skupin. Toto seskupení umožňuje vaší organizaci identifikovat zařízení, která jsou možná nejlepšími kandidáty na splnění požadavků peer-to-peer. Optimalizace doručení významně snižuje celkovou šířku pásma, která se používá k udržení aktuálního stavu zařízení a současně urychluje dobu stahování.

> [!NOTE]  
> Optimalizace doručení je řešení spravované v cloudu. Přístup k Internetu do cloudové služby optimalizace doručování je nutný k využití svých funkcí peer-to-peer. Informace o potřebných koncových bodech internetu najdete v tématu [Nejčastější dotazy k optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

Pro dosažení nejlepších výsledků možná budete muset nastavit [režim stažení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode) Optimalizace doručení na **skupiny (2)** a definovat *ID skupin*. V režimu skupiny může partnerský vztah mezi zařízeními, která patří do stejné skupiny, zahrnovat zařízení ve vzdálených kancelářích mezi interními podsítěmi. Pomocí [Možnosti ID skupiny](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) můžete vytvořit vlastní skupinu nezávisle na doménách a služba AD DS lokalitách. Režim stahování skupiny je doporučenou možností pro většinu organizací, které hledají nejlepší optimalizaci šířky pásma s optimalizací doručení.

Ruční konfigurace těchto ID skupin je náročná na to, že klienti přecházejí mezi různými sítěmi. Configuration Manager verze 1802 přidala novou funkci pro zjednodušení správy tohoto procesu [integrací skupin hranic s optimalizací doručení](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Když se klient probudí, mluví se svým bodem správy, aby získal zásady, a poskytuje informace o jeho síti a skupině hranic. Configuration Manager vytvoří jedinečné ID pro každou skupinu hranic. Lokalita používá informace o umístění klienta k automatické konfiguraci ID skupiny Optimalizace doručení klienta s ID hranice Configuration Manager. Když se klient přenese do jiné skupiny hranic, mluví ho s bodem správy a automaticky se překonfiguruje s novým ID hraniční skupiny. Díky této integraci může Optimalizace doručení využít Configuration Manager informace o skupině hranic k vyhledání partnerského zařízení, ze kterého se mají aktualizace stahovat.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> Optimalizace doručení od verze 1910
<!--4699118-->
Počínaje verzí 1910 Configuration Manager můžete použít optimalizaci doručování pro distribuci veškerého obsahu služby Windows Update pro klienty se systémem Windows 10 verze 1709 nebo novější, nikoli pouze soubory Expresní instalace.

Chcete-li použít optimalizaci doručování pro všechny instalační soubory služby Windows Update, povolte následující [nastavení klienta aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#software-updates):

- **Povolí klientům stahovat rozdílový obsah, pokud je k dispozici** možnost nastaveno na **Ano**.
- **Port, který klienti používají pro příjem požadavků na rozdílový obsah** nastavený na 8005 (výchozí) nebo vlastní číslo portu.
 
> [!IMPORTANT]
> - Optimalizace doručení musí být povolená (výchozí) a nepoužívá se. Další informace najdete v tématu [referenční informace k optimalizaci Windows Delivery](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference).
> - Při změně [nastavení klienta aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#software-updates) pro rozdílový obsah ověřte [nastavení klienta Optimalizace doručení](../../core/clients/deploy/about-client-settings.md#delivery-optimization) .
> - Optimalizace doručení se nedá použít pro Microsoft 365 aktualizace klienta, pokud je povolený Office COM. Sada Office COM je používána nástrojem Configuration Manager ke správě aktualizací pro klienty Microsoft 365ch aplikací. Můžete zrušit registraci Office COM, aby bylo možné používat optimalizaci doručování pro aktualizace aplikací Microsoft 365. Když je Office COM zakázaný, aktualizace softwaru pro Microsoft 365 aplikace se spravují pomocí výchozí naplánované úlohy pro Office Automatic Updates 2,0. To znamená, že Configuration Manager nediktování ani nesleduje proces instalace aktualizací Microsoft 365 aplikací. Configuration Manager bude pokračovat ve shromažďování informací z inventáře hardwaru a naplnit řídicí panel pro správu klientů Office 365 v konzole nástroje. Informace o tom, jak zrušit registraci Office COM, najdete v tématu [Povolení klientů office 365 přijímat aktualizace z Office CDN místo Configuration Manager](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - Při použití CMG pro úložiště obsahu se nebude obsah pro aktualizace třetích stran stahovat do klientů, pokud je povolený **rozdílový obsah ke stažení, pokud** je povolené [nastavení klienta](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) dostupné. <!--6598587-->

#### <a name="configuration-recommendations-for-clients-downloading-delta-content"></a>Doporučení konfigurace pro klienty, kteří stahují rozdílový obsah
<!--7913814-->
Pokud je v klientech pro obsah aktualizace softwaru povolena [možnost](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Povolit klientům stahování rozdílových obsahu** , jsou v rámci [nouzového chování distribučního bodu](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_site-fallback) k dispozici určitá omezení. Chcete-li zajistit, aby tito klienti mohli správně stáhnout obsah aktualizace softwaru, doporučujeme následující konfigurace:

- Zajistěte, aby se klienti nacházejí ve skupině hranic a aby existoval spolehlivý distribuční bod s potřebným obsahem přidruženým k této skupině hranic.
- Nasaďte aktualizace softwaru s využitím Fallback do Microsoft Update povolené pro klienty, kteří můžou stahovat přímo z Internetu.
   - Nastavení nasazení pro toto nouzové chování je v **případě, že aktualizace softwaru nejsou k dispozici v distribučním bodě v aktuálních, sousedních nebo hraničních skupinách lokality, stahují obsah z aktualizací společnosti Microsoft** a nacházejí se na stránce **Nastavení stahování** . Další informace najdete v tématu [nasazení aktualizací softwaru](manually-deploy-software-updates.md#process-to-manually-deploy-the-software-updates-in-a-software-update-group).

Pokud není jedna z výše uvedených možností životaschopná, **umožněte klientům stahovat rozdílový obsah, pokud** je možné ho v nastavení klienta zakázat, aby se povolily funkce Fallback. Partnerský vztah pro optimalizaci doručování se v tomto případě nebude využívat, protože klient nepoužije rozdílový kanál.

### <a name="configuration-manager-peer-cache"></a>Configuration Manager sdílené mezipaměti

Sdílená [mezipaměť](../../core/plan-design/hierarchy/client-peer-cache.md) je funkce Configuration Manager, která umožňuje klientům sdílet obsah s jinými klienty přímo z místní mezipaměti Configuration Manager. Sdílená mezipaměť nenahrazuje použití jiných řešení ukládání do sdílené mezipaměti, jako je Windows BranchCache. Společně s nimi spolupracuje s dalšími možnostmi rozšíření tradičních řešení pro nasazení obsahu, jako jsou třeba distribuční body. Sdílená mezipaměť nespoléhá na BranchCache. Pokud službu BranchCache nepovolíte nebo nepoužíváte, sdílená mezipaměť pořád funguje.

> [!NOTE]  
> Klienti můžou stahovat jenom obsah od klientů sdílené mezipaměti, kteří jsou v aktuální skupině hranic.  


### <a name="windows-branchcache"></a>Služba BranchCache systému Windows
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) je technologie optimalizace šířky pásma ve Windows. Každý klient má mezipaměť a funguje jako alternativní zdroj obsahu. Zařízení ve stejné síti si můžou tento obsah vyžádat. [Configuration Manager může používat službu BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) , aby umožnila partnerským uzlům zdrojový obsah navzájem, a vždy se musí spojit s distribučním bodem. Pomocí služby BranchCache se soubory ukládají do mezipaměti každého jednotlivého klienta a ostatní klienti je můžou podle potřeby načítat. Tento přístup distribuuje mezipaměť místo toho, aby bylo možné načíst jenom jeden bod. Toto chování šetří značnou šířku pásma a zároveň zkracuje dobu, po kterou klienti dostanou požadovaný obsah.



## <a name="selecting-the-right-peer-caching-technology"></a>Výběr správné technologie ukládání do mezipaměti pro sdílené počítače

Výběr správné technologie peere naukládání do mezipaměti pro soubory Expresní instalace závisí na vašem prostředí a požadavcích. I když Configuration Manager podporuje všechny výše uvedené technologie peer-to-peer, měli byste použít ty, které pro vaše prostředí mají smysl. Pro většinu zákazníků, předpokládá, že klienti můžou splňovat požadavky na Internet pro zajištění optimalizace doručování, takže by měla být integrovaná mezipaměť Windows 10 integrovaná do mezipaměti s optimalizací doručení dostačující. Pokud vaši klienti nemůžou tyto požadavky na Internet splnit, zvažte použití funkce Configuration Manager sdílené mezipaměti. Pokud v tuto chvíli používáte službu BranchCache s Configuration Manager a splňujete všechny vaše potřeby, můžou být pro vás správné možnosti souborů Express s BranchCache. 

### <a name="peer-cache-comparison-chart"></a>Graf porovnání sdílené mezipaměti


| Funkce  | Optimalizace doručení  | Sdílená mezipaměť  | Služba BranchCache  |
|---------|---------|---------|---------|
| Podporováno mezi podsítěmi | Yes | Ano | No |
| Omezení šířky pásma | Ano (nativní) | Ano (přes BITS) | Ano (přes BITS) |
| Podpora částečného obsahu | Ano, u všech podporovaných typů obsahu uvedených v tomto sloupci na dalším řádku. | Jenom pro aplikace Microsoft 365 a expresní aktualizace | Ano, u všech podporovaných typů obsahu uvedených v tomto sloupci na dalším řádku. |
| Podporované typy obsahu | **Prostřednictvím nástroje ConfigMgr:** </br> – Expresní aktualizace </br> – Všechny aktualizace Windows (počínaje verzí 1910). To nezahrnuje aktualizace Microsoft 365ch aplikací.</br> </br> **Přes Microsoft Cloud:**</br> – Windows a aktualizace zabezpečení</br> – Ovladače</br> – Aplikace pro Windows Store</br> – Aplikace pro Windows Store pro firmy | Všechny typy obsahu nástroje ConfigMgr, včetně obrázků stažených v [systému Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | Všechny typy obsahu nástroje ConfigMgr kromě imagí |
| Velikost mezipaměti na ovládacím prvku disku | Yes | Yes | Yes |
| Zjišťování zdroje partnerského vztahu | Automaticky | Ruční (nastavení agenta klienta) | Automaticky |
| Rovnocenné zjišťování | Přes cloudovou službu optimalizace doručování (vyžaduje přístup k Internetu) | Přes bod správy (na základě skupin hranic klientů) | Odesílání |
| Vytváření sestav | Ano (použití Desktop Analytics) | Řídicí panel zdrojů dat klienta nástroje ConfigMgr | Řídicí panel zdrojů dat klienta nástroje ConfigMgr |
| Řízení využití sítě WAN | Ano (nativní, lze ovládat pomocí nastavení zásad skupiny) | Skupiny hranic | Pouze podpora podsítí |
| Správa prostřednictvím nástroje ConfigMgr | Částečný (nastavení klientského agenta) | Ano (nastavení agenta klienta) | Ano (nastavení agenta klienta) |



## <a name="conclusion"></a>Závěr

Microsoft doporučuje, abyste v případě potřeby vyoptimalizovalte doručování aktualizací kvality Windows 10 pomocí Configuration Manager se soubory Expresní instalace a technologií pro ukládání do mezipaměti. Tento přístup by měl zmírnit výzvy spojené se zařízeními s Windows 10, které stahují velký obsah pro instalaci aktualizací kvality. Nasazením aktualizací kvality každý měsíc se také doporučuje udržovat zařízení s Windows 10 aktuální. Tento postup snižuje rozdíl mezi obsahem aktualizace kvality, který zařízení každý měsíc potřebuje. Snížení rozdílů v obsahu způsobí, že menší velikost se stáhne z distribučních bodů nebo z partnerských zdrojů. 

Vzhledem k povaze souborů Expresní instalace je jejich velikost obsahu podstatně větší než tradiční samostatné soubory. Tato velikost má za následek delší dobu stahování aktualizace od služby web Windows Update do Configuration Manager serveru lokality. Velikost místa na disku potřebného pro server lokality i pro distribuční body se také zvyšuje. Celková doba potřebná ke stažení a distribuci aktualizací kvality může být delší. Výhody na straně zařízení by se ale měly během stahování a instalace aktualizací kvality zařízení s Windows 10 všimnout. Další informace najdete v tématu [použití souborů Expresní instalace](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files).

Pokud jsou na straně serveru kompromisy aktualizací s větší velikostí blokování pro přijetí expresní podpory, ale výhody na straně zařízení jsou pro firmu a prostředí velmi důležité, společnost Microsoft doporučuje použít [web Windows Update pro firmy](integrate-windows-update-for-business-windows-10.md) s Configuration Manager. Web Windows Update pro firmy nabízí všechny výhody, které jsou v programu Express bez nutnosti stahovat, ukládat a distribuovat soubory Expresní instalace v celém prostředí. Klienti stahují obsah přímo ze služby web Windows Update, takže můžete i nadále používat optimalizaci doručování.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Nejčastější dotazy

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Jak Windows Express stahuje práci s Configuration Manager?

Agent webu Windows Update (WUA) nejprve požaduje expresní obsah. Pokud se instalace expresní aktualizace nezdařila, může se vrátit k úplné aktualizaci souborů.  

1. Klient Configuration Manager oznamuje službě WUA stažení obsahu aktualizace. Když Agent WUA spustí expresní stažení, nejprve stáhne zástupnou proceduru (například `Windows10.0-KB1234567-<platform>-express.cab` ), která je součástí balíčku Express.  

2. WUA předá tuto zástupnou proceduru instalačnímu programu služby Windows Update, který je součástí údržby (CBS). CBS používá zástupnou proceduru k provádění místního inventáře a porovnávání rozdílových souborů v zařízení s tím, co je potřeba k získání nejnovější verze nabízeného souboru.  

3. CBS pak vyzve agenta WUA, aby si stáhl požadované rozsahy z jednoho nebo více souborů Express. PSV.  

4. Pokud je povolená optimalizace doručování a zjištění partnerských uzlů, které mají požadované rozsahy, bude klient stahovat z partnerských uzlů nezávisle na klientovi nástroje ConfigMgr. Pokud je optimalizace doručování zakázána nebo žádné partnerské uzly nemají potřebné rozsahy, klient nástroje ConfigMgr tyto rozsahy stáhne z místního distribučního bodu (nebo z partnerského nebo Microsoft Update). Rozsahy jsou předány agentovi web Windows Update, který je zpřístupňuje, aby bylo možné použít rozsahy.


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Proč jsou expresní soubory (. PSV) tak velké, pokud jsou uložené v Configuration Manager partnerských zdrojů ve složce ccmcache?

Soubory Express (. PSV) jsou řídké soubory. Chcete-li určit skutečné místo na disku, které je používáno souborem, zkontrolujte vlastnost **Velikost na disku** souboru. Vlastnost Size na disku by měla být výrazně menší než hodnota Size.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Podporuje Configuration Manager soubory Expresní instalace s aktualizacemi funkcí Windows 10?

Ne, Configuration Manager v současné době podporuje pouze soubory Expresní instalace s aktualizacemi kvality Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Kolik místa na disku je potřeba na základě aktualizace kvality na serveru lokality a distribučních bodech?

To závisí na okolnostech. Pro každou aktualizaci kvality jsou na serverech uloženy úplné soubory a verze Express aktualizace. Aktualizace kvality Windows 10 jsou kumulativní, takže se velikost těchto souborů zvětšuje každý měsíc. Naplánujte minimálně 5 GB na aktualizaci na jednotlivé jazyky. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Mají Configuration Manager klienti stále výhodné soubory Expresní instalace, pokud se vrátí ke službě web Windows Update?

Ano. Pokud použijete následující možnost nasazení aktualizace softwaru, klienti pořád používají expresní aktualizace a optimalizaci doručování, když se budou vracet do cloudové služby:  

**Pokud aktualizace softwaru nejsou k dispozici v distribučním bodě v aktuálních, sousedních nebo skupinových lokalitách, Stáhněte obsah z aktualizací společnosti Microsoft.**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Proč se obsah expresního souboru nestáhl pro existující aktualizace po povolení podpory expresních souborů? 

Změny se projeví až po povolení podpory u všech nových aktualizací synchronizovaných a nasazených.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Existuje nějaký způsob, jak zjistit množství obsahu staženého z partnerských uzlů pomocí optimalizace doručování?
Windows 10 verze 1703 (a novější) obsahuje dvě nové rutiny PowerShellu **Get-DeliveryOptimizationPerfSnap** a **Get-DeliveryOptimizationStatus**. Tyto rutiny poskytují lepší přehled o službě Optimalizace doručení a využití mezipaměti. Další informace najdete v tématu věnovaném [optimalizaci doručování pro aktualizace Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network) .


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Jak klienti komunikují s optimalizací doručování přes síť?
Další informace o síťových portech, požadavcích na proxy serveru a názvůch hostitelů pro brány firewall najdete v tématu [Nejčastější dotazy k optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>Soubory protokolu

Ke sledování rozdílového stahování použijte následující soubory protokolu:

- WUAHandler.log
- DeltaDownload. log

## <a name="next-steps"></a>Další kroky

- [Nasazení aktualizací softwaru](deploy-software-updates.md)
- [Automatické nasazení aktualizací softwaru](automatically-deploy-software-updates.md)
