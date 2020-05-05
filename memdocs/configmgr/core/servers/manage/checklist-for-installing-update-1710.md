---
title: Kontrolní seznam pro 1710 | Configuration Manager
titleSuffix: Configuration Manager
description: Přečtěte si o akcích, které je potřeba provést před aktualizací na verzi Configuration Manager 1710.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e8ab8ca-41ef-467a-943b-a115d88cafe0
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fd3e067577a7f89c02727ccd490ef6d1eb26ca98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723317"
---
# <a name="checklist-for-installing-update-1710-for-configuration-manager"></a>Kontrolní seznam pro instalaci aktualizace 1710 pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když použijete aktuální větev Configuration Manager, můžete nainstalovat konzolovou aktualizaci pro verzi 1710, která aktualizuje vaši hierarchii z předchozí verze.

Chcete-li získat aktualizaci verze 1710, je nutné použít roli systému lokality spojovacího bodu služby v lokalitě nejvyšší úrovně ve vaší hierarchii. Tato možnost může být v režimu online nebo offline. Jakmile vaše hierarchie stáhne balíček aktualizace od Microsoftu, najdete ho v konzole v části **Správa &gt; přehled &gt; Cloud Services &gt; aktualizace a údržba**.

-   Je-li aktualizace uvedena jako **dostupná**, je aktualizace připravena k instalaci. Před instalací verze 1710 si přečtěte následující informace [o instalaci aktualizace 1710](#about-installing-update-1710) a [Kontrolní seznam](#checklist) pro konfigurace, které se mají provést před zahájením aktualizace.

-   Pokud se aktualizace zobrazí jako **stahování** a nemění se, zkontrolujte chyby v protokolu **hman. log** a **dmpdownloader. log** .

    -   Pokud dmpdownloader. log indikuje, že je proces dmpdownloader v režimu spánku a čeká se na něj před kontrolou aktualizací, můžete restartovat službu **SMS_Executive** na serveru lokality, aby se restartovala stahování souborů opětovné distribuce aktualizace.

    -   K dalšímu problému se stahování dochází, když proxy server nastavení brání `silverlight.dlservice.microsoft.com` stažení `download.microsoft.com`z a.

Další informace o instalaci aktualizací najdete v tématu [aktualizace a údržba v konzole](updates.md#bkmk_inconsole).

Informace o verzích Current Branch najdete v tématu [základní a aktualizační verze](updates.md#bkmk_Baselines) v článku [aktualizace pro Configuration Manager](updates.md).

## <a name="about-installing-update-1710"></a>O instalaci aktualizace 1710

**Místa**  
Aktualizaci 1710 nainstalujete v lokalitě nejvyšší úrovně ve vaší hierarchii. To znamená, že instalaci zahájíte z lokality centrální správy, pokud ji máte, nebo ze samostatné primární lokality. Po instalaci aktualizace v lokalitě nejvyšší úrovně mají podřízené lokality následující chování aktualizace:

-   Podřízené primární lokality instalují aktualizaci automaticky, jakmile lokalita centrální správy dokončí instalaci aktualizace. Můžete použít okna služby k řízení, kdy lokalita nainstaluje aktualizaci. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).

-   Pokud má primární Nadřazená lokalita dokončí instalaci aktualizace, je potřeba ručně aktualizovat každou sekundární lokalitu z konzoly Configuration Manager. Automatická aktualizace serverů sekundárních lokalit se nepodporuje.

**Role systému lokality:**  
Když server lokality nainstaluje aktualizaci, role systému lokality, které jsou nainstalované na počítači serveru lokality, a ty, které jsou nainstalované na vzdálených počítačích, se automaticky aktualizují. Před instalací aktualizace se ujistěte, že všechny systémové servery lokality splňují požadavky na provoz s novou verzí aktualizace.

**Konzoly Configuration Manager:**   
Při prvním použití konzoly Configuration Manager po dokončení aktualizace se zobrazí výzva k aktualizaci této konzoly. Pokud to chcete udělat, musíte spustit instalační program Configuration Manager v počítači, který je hostitelem konzoly, a pak zvolit možnost aktualizace konzoly. Instalaci aktualizace konzoly doporučujeme neodkládat.

> [!IMPORTANT]  
> Při instalaci aktualizace v lokalitě centrální správy mějte na paměti následující omezení a prodlevy, které existují, dokud všechny podřízené primární lokality instalaci aktualizace nedokončí:    
> - **Upgrade klienta** se nespustí. To zahrnuje automatické aktualizace klientů a předprodukčních klientů. Kromě toho nemůžete zvýšit úroveň předprodukčních klientů na produkční, dokud poslední lokalita nedokončí instalaci aktualizace. Po dokončení instalace aktualizace od poslední lokality začnou upgrady klientů na základě možností konfigurace.   
> - **Nové funkce** , které povolíte v rámci této aktualizace, nejsou k dispozici. Účelem je zabránit tomu, aby se replikace dat souvisejících s touto funkcí odesílala na lokalitu, která ještě nenainstalovala podporu pro tuto funkci. Po instalaci aktualizace všemi primárními lokalitami bude tato funkce k dispozici pro použití.   
> - **Odkazy replikace** mezi lokalitou centrální správy a podřízenými primárními lokalitami se zobrazují jako Neupgradované. Tato operace se zobrazí ve stavu instalace balíčku aktualizace jako stav dokončeno s upozorněním pro monitorování inicializace replikace. V uzlu monitorování konzoly se zobrazí jako *Konfigurace odkazu*.


## <a name="checklist"></a>Kontrolní seznam

**Ujistěte se, že všechny lokality používají verzi Configuration Manager, která podporuje aktualizaci na 1710:**   
Aby bylo možné spustit instalaci aktualizace 1710, musí každý server lokality v hierarchii používat stejnou verzi Configuration Manager. K aktualizaci na 1710 je nutné použít verzi 1610, 1702 nebo 1706.

**Zkontrolujte stav svého softwaru Software Assurance nebo ekvivalentního práva k předplatnému:**   
K instalaci aktualizace 1710 musíte mít aktivní smlouvu o programu Software Assurance (SA). Po instalaci této aktualizace karta **licencování** nabídne možnost potvrdit **Datum vypršení platnosti Software Assurance**.

Toto je volitelná hodnota, kterou můžete zadat jako pohodlné připomenutí data vypršení platnosti licence. Toto datum se zobrazí, když instalujete budoucí aktualizace. Tuto hodnotu jste mohli dřív zadat během instalace nebo instalace aktualizace nebo pomocí karty **licencování** v **Nastavení hierarchie**v rámci konzoly Configuration Manager.

Další informace najdete v tématu [licencování a větve pro Configuration Manager](../../understand/learn-more-editions.md).

**Přečtěte si nainstalované verze Microsoft .NET na serverech systému lokality:** Když lokalita nainstaluje tuto aktualizaci, Configuration Manager automaticky nainstaluje .NET Framework 4.5.2 do každého počítače, který je hostitelem jedné z následujících rolí systému lokality, pokud není již .NET Framework 4,5 nebo novější nainstalována:

-   Zprostředkující bod registrace
-   Bod registrace
-   Bod správy
-   Spojovací bod služby

Tato instalace může server systému lokality uvést do stavu čekání na restartování a ohlásit chyby do Configuration Manager Viewer stavu komponent. Kromě toho můžou aplikace .NET na serveru docházet k náhodným chybám, dokud se server nerestartuje.

Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../plan-design/configs/site-and-site-system-prerequisites.md).

**Přečtěte si verzi sady Windows Assessment and Deployment Kit (ADK) pro Windows 10** . Systém Windows 10 ADK by měl být verze 1703 nebo novější. (Další informace o podporovaných verzích Windows ADK najdete v tématu [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk).) Pokud musíte aktualizovat sadu Windows ADK, udělejte to předtím, než začnete s aktualizací Configuration Manager. Tím se zajistí, že výchozí spouštěcí image se automaticky aktualizují na nejnovější verzi Windows PE. (Vlastní spouštěcí image se musí aktualizovat ručně.)

Pokud aktualizujete lokalitu před aktualizací sady Windows ADK, přečtěte si téma [aktualizace distribučních bodů pomocí spouštěcí image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image) pro vylepšení tohoto procesu v Configuration Manager verze 1710.

**Zkontrolujte stav lokality a hierarchie a ověřte, že nejsou přítomné žádné nevyřešené problémy:** Před aktualizací lokality vyřešte všechny provozní problémy serveru lokality, serveru databáze lokality a rolí systému lokality, které jsou nainstalované na vzdálených počítačích. Aktualizace lokality může kvůli existujícím provozním problémům selhat.

Další informace najdete v tématu [použití výstrah a stavového systému pro Configuration Manager](use-alerts-and-the-status-system.md).

**Zkontrolujte replikaci souborů a dat mezi lokalitami:**   
Ujistěte se, že je replikace souborů a databáze mezi lokalitami v provozu a aktuální. Zpoždění nebo nevyřízené položky můžou bránit hladké úspěšné aktualizaci.
U replikace databáze můžete k řešení problémů před spuštěním aktualizace použít Analyzátor propojení replikace.

Další informace najdete v tématu [analyzátor propojení replikace](monitor-replication.md#BKMK_RLA) v tématu [monitorování replikace](monitor-replication.md#BKMK_RLA) databáze.

**Nainstalujte všechny použitelné kritické aktualizace operačních systémů na počítače, které jsou hostitelem lokality, serveru databáze lokality a rolí vzdáleného systému lokality:** Před instalací aktualizace pro Configuration Manager nainstalujte všechny důležité aktualizace pro každý příslušný systém lokality. Jestliže aktualizace, kterou instalujete, vyžaduje restart, před spuštěním upgradu restartujte příslušné počítače.

**Zakažte repliky databáze pro body správy v primárních lokalitách:**   
Configuration Manager nemůže úspěšně aktualizovat primární lokalitu, která má povolenou repliku databáze pro body správy. Před instalací aktualizace pro Configuration Manager zakažte replikaci databáze.

Další informace najdete v tématu [repliky databáze pro body správy pro Configuration Manager](../deploy/configure/database-replicas-for-management-points.md).

**Nastavit SQL Server skupiny dostupnosti AlwaysOn na ruční převzetí služeb při selhání:**   
Pokud používáte skupinu dostupnosti, před zahájením instalace aktualizace se ujistěte, že je skupina dostupnosti nastavená na ruční převzetí služeb při selhání. Po aktualizaci lokality můžete obnovit převzetí služeb při selhání automaticky. Další informace najdete v tématu [SQL Server AlwaysOn pro databázi lokality](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Znovu nakonfigurujte body aktualizace softwaru, které používají služby NLB:**   
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
Configuration Manager nemůže aktualizovat lokalitu, která pro hostování bodů aktualizace softwaru používá cluster služby Vyrovnávání zatížení sítě (NLB).

Pokud pro body aktualizace softwaru používáte clustery služby Vyrovnávání zatížení sítě, odeberte cluster programu NLB pomocí prostředí Windows PowerShell.
Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).

**Zakažte všechny úlohy údržby lokality v každé lokalitě po dobu trvání instalace aktualizace na této lokalitě:**   
Před instalací aktualizace zakažte všechny úlohy údržby lokality, které by mohly běžet v době, kdy je proces aktualizace aktivní. To zahrnuje, avšak není omezeno jen na:

-   Zálohovat server lokality
-   Vymazat staré operace klientů
-   Vymazat stará data zjišťování

Pokud se během instalace aktualizace spustí některá úloha údržby databáze lokality, při instalaci aktualizace může dojít k chybě. Než úlohu zakážete, zaznamenejte plán úlohy, abyste po instalaci aktualizace mohli obnovit její konfiguraci.

Další informace najdete v tématu [úlohy údržby pro Configuration Manager](maintenance-tasks.md) a [Referenční dokumentace k úlohám údržby pro Configuration Manager](reference-for-maintenance-tasks.md).

**Dočasně zastavit veškerý antivirový software na Configuration Managerch serverech:** Než aktualizujete lokalitu, ujistěte se, že jste zastavili antivirový software na serverech Configuration Manager. <!--SMS.503481--> 

**Vytvořte zálohu databáze lokality v lokalitě centrální správy a primárních lokalitách:** Před aktualizací lokality proveďte zálohu databáze lokality, abyste měli jistotu, že máte použitelnou úspěšnou zálohu pro případ zotavení po havárii.

Další informace najdete v tématu [zálohování a obnovení pro Configuration Manager](backup-and-recovery.md).

**Naplánujte pilotní nasazení klienta:**   
Když nainstalujete aktualizaci, která aktualizuje klienta, můžete novou aktualizaci klienta otestovat v předprodukčním prostředí ještě před tím, než se nasadí a upgraduje všechny aktivní klienty.

Pokud chcete tuto možnost využít, musíte nakonfigurovat lokalitu tak, aby podporovala automatické upgrady pro předprodukční prostředí před zahájením instalace aktualizace.

Další informace najdete v tématu [upgrade klientů](../../clients/manage/upgrade/upgrade-clients.md) a [testování upgradu klienta v předprodukční kolekci](../../clients/manage/upgrade/test-client-upgrades.md).

**Naplánování použití oken služby k řízení, kdy servery lokality instalují aktualizace:**   
Pomocí oken služby můžete definovat dobu, během které je možné nainstalovat aktualizace serveru lokality.

Můžete tak stanovit čas instalace aktualizací v lokalitách v rámci vaší hierarchie. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).

**Spusťte kontrolu požadovaných součástí instalace:**   
Když je aktualizace uvedená v konzole jako **k dispozici,** můžete před instalací aktualizace nezávisle spustit kontrolu požadovaných součástí. (Při instalaci aktualizace na lokalitu se Kontrola požadovaných součástí spouští znovu.)

Chcete-li spustit kontrolu požadovaných součástí z konzoly, vyhledejte **> přehled > Cloud Services > aktualizace a údržba.** Potom klikněte pravým tlačítkem na **balíček aktualizace Configuration Manager 1710**a pak zvolte **Spustit kontrolu požadovaných součástí**.

Další informace o spuštění a následné kontrole kontroly požadovaných součástí najdete v části **Krok 3: spuštění kontroly požadovaných součástí před instalací aktualizace** v tématu [instalace aktualizací v konzole pro Configuration Manager](install-in-console-updates.md).

> [!IMPORTANT]  
> Pokud se Kontrola požadovaných součástí spouští nezávisle nebo v rámci instalace aktualizace, proces aktualizuje některé zdrojové soubory produktu, které se používají pro úlohy údržby lokality. Proto po spuštění kontroly požadovaných součástí, ale před instalací aktualizace, potřebujete-li provést úlohu údržby lokality, spusťte **Setupwpf. exe** (Configuration Manager instalační program) z disku CD-ROM. Poslední složka na serveru lokality.

**Aktualizovat lokality:**   
Nyní jste připraveni zahájit instalaci aktualizace pro vaši hierarchii. Další informace o instalaci aktualizace najdete [v tématu Instalace konzolových aktualizací.](install-in-console-updates.md#bkmk_install)

Doporučujeme, abyste instalaci aktualizace naplánovali pro každou lokalitu mimo běžnou pracovní dobu, kdy bude mít proces instalace aktualizace a jejích akcí pro přeinstalaci součástí lokality a rolí systému lokality nejmenší dopad na vaše obchodní operace.

Další informace najdete v tématu [aktualizace pro Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Kontrolní seznam po aktualizaci
Projděte si následující akce, které se mají provést po dokončení instalace aktualizace.
1. Ujistěte se, že je replikace mezi lokalitami aktivní. V konzole nástroje zobrazte **monitorování** > **hierarchie lokality**a **monitorování** > **replikace databáze** pro indikaci problémů nebo potvrzení, že jsou odkazy replikace aktivní.
2. Ujistěte se, že každý server lokality a role systému lokality byly aktualizovány na verzi 1710. V konzole nástroje můžete přidat volitelnou **verzi** sloupce do zobrazení některých uzlů včetně **lokalit** a **distribučních bodů**.

   V případě potřeby se role systému lokality automaticky přeinstaluje, aby se aktualizovala na novou verzi. Zvažte restartování systémů vzdáleného webového serveru, které se neaktualizují úspěšně.
3. Před zahájením aktualizace znovu nakonfigurujte repliky databáze pro body správy v primárních lokalitách, které jste zakázali.
4. Před zahájením aktualizace znovu nakonfigurujte úlohy údržby databáze, které jste zakázali.
5. Pokud jste nakonfigurovali pilotní nasazení klienta před instalací aktualizace, upgradujte klienty podle plánu, který jste vytvořili.
