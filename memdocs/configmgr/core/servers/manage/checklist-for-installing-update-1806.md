---
title: Kontrolní seznam pro 1806
titleSuffix: Configuration Manager
description: Přečtěte si o akcích, které je potřeba provést před aktualizací na verzi Configuration Manager 1806.
ms.date: 08/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb0a87a6-fd65-440b-90a5-2fef35622c9d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f5323360e8c64e1ea0e1c2eb7152d16d2525f85e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723233"
---
# <a name="checklist-for-installing-update-1806-for-configuration-manager"></a>Kontrolní seznam pro instalaci aktualizace 1806 pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když použijete aktuální větev Configuration Manager, můžete nainstalovat konzolovou aktualizaci pro verzi 1806, která aktualizuje vaši hierarchii z předchozí verze. <!-- baseline only statement: (Because version 1802 is also available as [baseline media](updates.md#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

Chcete-li získat aktualizaci verze 1806, je nutné použít spojovací bod služby v lokalitě nejvyšší úrovně ve vaší hierarchii. Tato role systému lokality může být v režimu online nebo offline. Jakmile vaše hierarchie stáhne balíček aktualizace od Microsoftu, najděte ho v konzole. V pracovním prostoru **Správa** vyberte uzel **aktualizace a údržba** .

-   Je-li aktualizace uvedena jako **dostupná**, je aktualizace připravena k instalaci. Před instalací verze 1806 si přečtěte následující informace [o instalaci aktualizace 1806](#about-installing-update-1806) a [Kontrolní seznam](#checklist) pro konfigurace, které se mají provést před zahájením aktualizace.

-   Pokud se aktualizace zobrazí jako **stahování** a nedojde ke změně, zkontrolujte chyby v protokolu **hman. log** a **dmpdownloader. log** .

    -   Dmpdownloader. log může znamenat, že proces dmpdownloader čeká na interval před vyhledáním aktualizací. Chcete-li znovu spustit stahování souborů opětovné distribuce aktualizace, restartujte službu **SMS_Executive** na serveru lokality.

    -   K dalšímu problému se stahování dochází, když proxy server nastavení brání `silverlight.dlservice.microsoft.com` stažení `download.microsoft.com`z a.

Další informace o instalaci aktualizací najdete v tématu [aktualizace a údržba v konzole](updates.md#bkmk_inconsole).

Další informace o aktuálních verzích větví najdete v tématu [základní a aktualizační verze](updates.md#bkmk_Baselines).



## <a name="about-installing-update-1806"></a>O instalaci aktualizace 1806

#### <a name="sites"></a>Lokality
Aktualizaci 1806 nainstalujete v lokalitě nejvyšší úrovně ve vaší hierarchii. Spusťte instalaci z lokality centrální správy nebo z samostatné primární lokality. Po instalaci aktualizace v lokalitě nejvyšší úrovně mají podřízené lokality následující chování aktualizace:

-   Podřízené primární lokality instalují aktualizaci automaticky, jakmile lokalita centrální správy dokončí instalaci aktualizace. Můžete použít okna služby k řízení, kdy lokalita nainstaluje aktualizaci. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).

-   Ručně aktualizovat každou sekundární lokalitu z konzoly Configuration Manager poté, co dokončí primární Nadřazená lokalita instalace aktualizace. Automatické aktualizace serverů sekundárních lokalit se nepodporují.

#### <a name="site-system-roles"></a>Role systému lokality
Když server lokality nainstaluje aktualizaci, automaticky aktualizuje všechny role systému lokality. Tyto role jsou na serveru lokality nebo nainstalované na vzdálených serverech. Před instalací aktualizace se ujistěte, že všechny systémové servery lokality splňují aktuální požadavky na novou verzi aktualizace.

#### <a name="configuration-manager-consoles"></a>Konzoly Configuration Manager   
Při prvním použití konzoly Configuration Manager po dokončení aktualizace budete vyzváni k aktualizaci této konzoly. Můžete také spustit instalaci Configuration Manager v počítači, který je hostitelem konzoly nástroje, a vybrat možnost aktualizovat konzolu. Nainstalujte aktualizaci do konzoly, jakmile to bude možné. Další informace najdete v tématu [Instalace konzoly Configuration Manager](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> Při instalaci aktualizace v lokalitě centrální správy mějte na paměti následující omezení a prodlevy, které existují, dokud všechny podřízené primární lokality instalaci aktualizace nedokončí:    
> - **Upgrade klienta** se nespustí. To zahrnuje automatické aktualizace klientů a předprodukčních klientů. Kromě toho nemůžete zvýšit úroveň předprodukčních klientů na produkční, dokud poslední lokalita nedokončí instalaci aktualizace. Po dokončení instalace aktualizace od poslední lokality začnou upgrady klientů na základě možností konfigurace.   
> - **Nové funkce** , které povolíte v rámci této aktualizace, nejsou k dispozici. Účelem je zabránit tomu, aby se replikace dat souvisejících s touto funkcí odesílala na lokalitu, která ještě nenainstalovala podporu pro tuto funkci. Po instalaci aktualizace všemi primárními lokalitami bude tato funkce k dispozici pro použití.   
> - **Odkazy replikace** mezi lokalitou centrální správy a podřízenými primárními lokalitami se zobrazují jako Neupgradované. Tato operace se zobrazí ve stavu instalace balíčku aktualizace jako stav dokončeno s upozorněním pro monitorování inicializace replikace. V uzlu monitorování konzoly se zobrazí jako *Konfigurace odkazu*.


## <a name="checklist"></a>Kontrolní seznam

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Všechny lokality používají podporovanou verzi Configuration Manager  
Aby bylo možné spustit instalaci aktualizace 1806, musí každý server lokality v hierarchii používat stejnou verzi Configuration Manager. K aktualizaci na 1806 je nutné použít verzi 1706, 1710 nebo 1802.

#### <a name="review-the-status-of-your-product-licensing"></a>Kontrola stavu licencování produktu 
K instalaci této aktualizace musíte mít aktivní smlouvu programu Software Assurance (SA) nebo odpovídající práva k předplatnému. Po aktualizaci lokality se na stránce **licencování** zobrazí možnost potvrdit **Datum vypršení platnosti Software Assurance**.

Tato hodnota je volitelná. Můžete zadat jako pohodlné připomenutí data vypršení platnosti licence. Toto datum se zobrazí, když instalujete budoucí aktualizace. Tuto hodnotu jste mohli dřív zadat během instalace nebo instalace aktualizace. Tuto hodnotu můžete zadat také v konzole Configuration Manager. V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**a vyberte možnost **lokality**. Na pásu karet klikněte na **Nastavení hierarchie** a přepněte na kartu **licencování** .

Další informace najdete v tématu [licencování a větve](../../understand/learn-more-editions.md).

#### <a name="review-microsoft-net-versions"></a>Kontrola verzí rozhraní Microsoft .NET 
Když lokalita nainstaluje tuto aktualizaci, Configuration Manager automaticky nainstaluje .NET Framework 4.5.2. Pokud tato součást ještě není nainstalovaná, lokalita ji nainstaluje na každý server, který je hostitelem jedné z následujících rolí systému lokality:

-   Bod správy
-   Spojovací bod služby
-   Zprostředkující bod registrace
-   Bod registrace

Tato instalace může server systému lokality uvést do stavu čekání na restartování a ohlásit chyby do Configuration Manager Viewer stavu komponent. Kromě toho můžou aplikace .NET na serveru docházet k náhodným chybám, dokud se server nerestartuje.

Další informace najdete v tématu [požadavky na lokalitu a systém lokality](../../plan-design/configs/site-and-site-system-prerequisites.md).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Kontrola verze sady Windows ADK pro Windows 10
Verze sady Windows 10 Assessment and Deployment Kit (ADK) by měla být podporovaná pro Configuration Manager verze 1806. Další informace o podporovaných verzích Windows ADK najdete v článku [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Pokud potřebujete aktualizovat sadu Windows ADK, udělejte to předtím, než začnete s aktualizací Configuration Manager. Tato objednávka zajistí, že výchozí spouštěcí image se automaticky aktualizují na nejnovější verzi Windows PE. Po aktualizaci lokality ručně aktualizujte všechny vlastní spouštěcí image.

Pokud aktualizujete lokalitu před aktualizací sady Windows ADK, přečtěte si téma [aktualizace distribučních bodů pomocí spouštěcí bitové kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Zkontrolovat stav lokality a hierarchie pro nevyřešené problémy 
Než aktualizujete lokalitu, vyřešte všechny provozní problémy serveru lokality, serveru databáze lokality a rolí systému lokality, které jsou nainstalované na vzdálených počítačích. Aktualizace lokality může kvůli existujícím provozním problémům selhat.

Další informace najdete v tématu [použití výstrah a stavového systému](use-alerts-and-the-status-system.md).

#### <a name="review-file-and-data-replication-between-sites"></a>Kontrola replikace souborů a dat mezi lokalitami   
Ujistěte se, že je replikace souborů a databáze mezi lokalitami v provozu a aktuální. Zpoždění nebo nevyřízené položky můžou bránit hladké úspěšné aktualizaci. U replikace databáze můžete k řešení problémů před spuštěním aktualizace použít Analyzátor propojení replikace.

Další informace najdete v tématu [o analyzátor propojení replikace](monitor-replication.md#BKMK_RLA).

#### <a name="install-all-applicable-critical-windows-updates"></a>Nainstalovat všechny použitelné kritické aktualizace Windows
Před instalací aktualizace pro Configuration Manager nainstalujte všechny důležité aktualizace operačního systému pro každý příslušný systém lokality. Mezi tyto servery patří server lokality, Server databáze lokality a role vzdáleného systému lokality. Pokud aktualizace, kterou instalujete, vyžaduje restart, před zahájením upgradu restartujte příslušné servery.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Zakažte repliky databáze pro body správy v primárních lokalitách.   
Configuration Manager nemůže úspěšně aktualizovat primární lokalitu, která má povolenou repliku databáze pro body správy. Než nainstalujete aktualizaci pro Configuration Manager, zakažte replikaci databáze.

Další informace najdete v tématu [repliky databáze pro body správy](../deploy/configure/database-replicas-for-management-points.md).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Nastavit SQL Server skupiny dostupnosti AlwaysOn na ruční převzetí služeb při selhání   
Pokud používáte skupinu dostupnosti, před zahájením instalace aktualizace se ujistěte, že je skupina dostupnosti nastavená na ruční převzetí služeb při selhání. Po aktualizaci lokality můžete obnovit převzetí služeb při selhání automaticky. Další informace najdete v tématu [SQL Server AlwaysOn pro databázi lokality](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Zakažte úlohy údržby lokality v každé lokalitě.
Před instalací aktualizace zakažte všechny úlohy údržby lokality, které by mohly běžet v době, kdy je proces aktualizace aktivní. Například neomezeno na:

-   Zálohovat server lokality
-   Vymazat staré operace klientů
-   Vymazat stará data zjišťování

Pokud se během instalace aktualizace spustí některá úloha údržby databáze lokality, při instalaci aktualizace může dojít k chybě. Než úlohu zakážete, zaznamenejte plán úlohy, abyste po instalaci aktualizace mohli obnovit její konfiguraci.

Další informace najdete v tématech [úlohy](maintenance-tasks.md) údržby a [referenční informace pro úlohy údržby](reference-for-maintenance-tasks.md).

#### <a name="temporarily-stop-any-antivirus-software"></a>Dočasné zastavení veškerého antivirového softwaru 
Před aktualizací lokality zastavte antivirový software na serverech Configuration Manager. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Vytvoření zálohy databáze lokality 
Před aktualizací lokality zálohujte databázi lokality v lokalitě centrální správy a primárních lokalitách. Tato záloha zajišťuje, že máte úspěšnou zálohu, která se má použít pro zotavení po havárii.

Další informace najdete v tématu [zálohování a obnovení](backup-and-recovery.md).

#### <a name="plan-for-client-piloting"></a>Plánování pilotního nasazení klientů   
Když nainstalujete aktualizaci, která aktualizuje klienta, můžete novou aktualizaci klienta otestovat v předprodukčním prostředí ještě před tím, než se nasadí a upgraduje všechny aktivní klienty. Pokud chcete tuto možnost využít, musíte nakonfigurovat lokalitu tak, aby podporovala automatické upgrady pro předprodukční prostředí před zahájením instalace aktualizace.

Další informace najdete v tématu [upgrade klientů](../../clients/manage/upgrade/upgrade-clients.md) a [testování upgradu klienta v předprodukční kolekci](../../clients/manage/upgrade/test-client-upgrades.md).

#### <a name="plan-to-use-service-windows"></a>Plánování použití oken služby   
Chcete-li definovat dobu, během které lze nainstalovat aktualizace serveru lokality, použijte systémovou službu. Můžou vám pomůžou řídit, kdy weby v hierarchii tuto aktualizaci instalují. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).

#### <a name="review-supported-extensions"></a>Zkontrolovat podporovaná rozšíření
<!--SCCMdocs#587-->
Pokud rozšíříte Configuration Manager s jinými produkty od partnerů Microsoftu nebo Microsoftu, ujistěte se, že tyto produkty podporují verzi 1806. Tyto informace vám poskytne dodavatel produktu. Příklad najdete v [poznámkách k verzi](../../../mdt/release-notes.md)Microsoft Deployment Toolkit.

#### <a name="run-the-setup-prerequisite-checker"></a>Spusťte kontrolu požadovaných součástí instalace.   
Když je aktualizace uvedená v konzole jako **k dispozici,** můžete před instalací aktualizace nezávisle spustit kontrolu požadovaných součástí. (Při instalaci aktualizace na lokalitu se Kontrola požadovaných součástí spouští znovu.)

Chcete-li spustit kontrolu požadovaných součástí z konzoly, otevřete ovládací prostor pro **správu** a vyberte možnost **aktualizace a údržba**. Vyberte balíček aktualizace **Configuration Manager 1806** a na pásu karet klikněte na tlačítko **Spustit kontrolu požadovaných součástí** .

Další informace najdete v části **spuštění kontroly požadovaných součástí před instalací aktualizace v nástroji** [předtím, než nainstalujete konzolovou aktualizaci](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Po spuštění kontroly požadovaných součástí proces aktualizuje některé zdrojové soubory produktu, které se používají pro úlohy údržby lokality. Proto po spuštění kontroly požadovaných součástí, ale před instalací aktualizace, potřebujete-li provést úlohu údržby lokality, spusťte **Setupwpf. exe** (Configuration Manager instalační program) z disku CD-ROM. Poslední složka na serveru lokality.

#### <a name="update-sites"></a>Aktualizovat weby   
Nyní jste připraveni zahájit instalaci aktualizace pro vaši hierarchii. Další informace o instalaci aktualizace najdete [v tématu Instalace konzolových aktualizací](install-in-console-updates.md#bkmk_install).

Instalaci aktualizace můžete naplánovat mimo běžnou pracovní dobu. Určete, kdy bude mít proces nejmenší vliv na vaše obchodní operace. Instalace aktualizace a jejích akcí znovu nainstaluje součásti lokality a role systému lokality.

Další informace najdete v tématu [aktualizace pro Configuration Manager](updates.md).



## <a name="post-update-checklist"></a>Kontrolní seznam po aktualizaci

Po aktualizaci lokality použijte následující kontrolní seznam k dokončení běžných úloh a konfigurací.


#### <a name="confirm-version-and-restart-if-necessary"></a>Potvrdit verzi a restartovat (v případě potřeby)
Ujistěte se, že každý server lokality a role systému lokality byly aktualizovány na verzi 1806. V konzole nástroje přidejte sloupec **verze** do uzlů **lokality** a **distribučních bodů** v pracovním prostoru **Správa** . V případě potřeby se role systému lokality automaticky přeinstaluje, aby se aktualizovala na novou verzi. 

Zvažte restartování vzdálených systémů lokality, které se neúspěšně aktualizují. Zkontrolujte infrastrukturu lokality a ujistěte se, že příslušné servery lokality a vzdálené servery systému lokality byly úspěšně restartovány. Servery lokality se obvykle restartují, jenom když Configuration Manager nainstaluje .NET jako předpoklad pro roli systému lokality.


#### <a name="confirm-site-to-site-replication-is-active"></a>Potvrdit aktivní replikaci mezi lokalitami
V konzole Configuration Manager pro zobrazení stavu použijte následující umístění a ujistěte se, že je replikace aktivní:  

-   Pracovní prostor **monitorování** , uzel **hierarchie lokality**  

-   Pracovní prostor **monitorování** , uzel **replikace databáze**  

Další informace najdete v těchto článcích:  

- [Monitorování hierarchie](monitor-hierarchy.md)
- [Monitorování replikace](monitor-replication.md)
- [Nástroj Replication Link Analyzer](monitor-replication.md#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Aktualizace konzol nástroje Configuration Manager
Aktualizujte všechny konzoly pro vzdálenou Configuration Manager na stejnou verzi. Výzva k aktualizaci konzoly se zobrazí v těchto případech:  

-   Otevřete konzolu nástroje.  

-   V konzole přejdete na nový uzel.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Překonfigurujte repliky databáze pro body správy.
Po aktualizaci primární lokality znovu nakonfigurujte repliku databáze pro body správy, které jste odinstalovali před aktualizací lokality. Další informace najdete v tématu [repliky databáze pro body správy](../deploy/configure/database-replicas-for-management-points.md).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Překonfigurujte všechny zakázané úlohy údržby.
Pokud jste v lokalitě před instalací aktualizace zakázali [úlohy údržby](maintenance-tasks.md) databáze, překonfigurujte tyto úlohy. Použijte stejné nastavení, které bylo provedeno před aktualizací.  


#### <a name="update-clients"></a>Aktualizace klientů
Aktualizujte klienty podle plánu, který jste vytvořili, zejména v případě, že jste nakonfigurovali pilotní nasazení klienta před instalací aktualizace. Další informace najdete v tématu [Postup upgradu klientů pro počítače se systémem Windows](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  


#### <a name="third-party-extensions"></a>Rozšíření jiných výrobců
Pokud používáte jakákoli rozšíření Configuration Manager, aktualizujte je na nejnovější verzi, aby podporovala Configuration Manager verze 1806. 


#### <a name="update-custom-boot-images-and-media"></a>Aktualizace vlastních spouštěcích imagí a médií
<!--SCCMDocs issue 775-->

Použijte akci **Aktualizovat distribuční body** pro libovolnou spouštěcí bitovou kopii, kterou používáte, ať už se jedná o výchozí nebo vlastní spouštěcí bitovou kopii. Tato akce zajistí, že klienti můžou používat nejnovější verzi. I v případě, že není k dispozici nová verze sady Windows ADK, mohou se součásti klienta Configuration Manager u aktualizace změnit. Pokud neaktualizujete spouštěcí image a média, můžou se na zařízeních zdařit nasazení pořadí úkolů. 

Když aktualizujete lokalitu, Configuration Manager automaticky aktualizuje *výchozí* spouštěcí image. Nedistribuuje automaticky aktualizovaný obsah do distribučních bodů. Použijte akci **Aktualizovat distribuční body** u konkrétních spouštěcích imagí, až budete připraveni k distribuci tohoto obsahu napříč vaší sítí. 

Po aktualizaci lokality ručně aktualizujte všechny *vlastní* spouštěcí image. Tato akce aktualizuje spouštěcí bitovou kopii s nejnovějšími součástmi klienta, pokud je to nutné, případně ji znovu načte pomocí aktuální verze prostředí Windows PE a znovu distribuuje obsah do distribučních bodů. 

Další informace najdete v tématu [aktualizace distribučních bodů pomocí spouštěcí bitové kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image). 
