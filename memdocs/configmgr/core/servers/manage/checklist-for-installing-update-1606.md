---
title: Kontrolní seznam pro 1606
titleSuffix: Configuration Manager
description: Přečtěte si o akcích, které je potřeba provést před aktualizací z verze Configuration Manager 1511 nebo 1602 na verzi 1606.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723079"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>Kontrolní seznam pro instalaci aktualizace 1606 pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Verze 1606 pro Configuration Manager aktuální větev je aktualizace, kterou můžete použít k aktualizaci z verze 1511 nebo 1602.

Před instalací verze 1606 jako aktualizace si Projděte následující informace a kontrolní seznam pro akce, které je třeba provést před zahájením aktualizace.

Informace o základních verzích najdete v tématu [základní a aktualizační verze](../../../core/servers/manage/updates.md#bkmk_Baselines) v článku [aktualizace pro Configuration Manager](../../../core/servers/manage/updates.md).

## <a name="about-installing-update-1606"></a>O instalaci aktualizace 1606

*Aktualizace*1606 se dá nainstalovat jenom v lokalitě nejvyšší úrovně ve vaší hierarchii. To znamená, že instalaci zahájíte z lokality centrální správy, pokud ji máte, nebo ze samostatné primární lokality.  

- Podřízené primární lokality instalují aktualizaci automaticky po dokončení instalace aktualizace lokalitou centrální správy. Pomocí oken služby můžete řídit, kdy lokalita instaluje aktualizace. Před verzí 1606 se v oknech služby nazývala okna údržby. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).  

- Sekundární lokality je nutné ručně aktualizovat v konzole Configuration Manager po dokončení instalace aktualizace primárním serverem nadřazené lokality. Automatická aktualizace serverů sekundárních lokalit se nepodporuje.  

Když server lokality nainstaluje aktualizaci, role systému lokality nainstalované na serveru lokality a ty, které jsou nainstalované na vzdálených počítačích, se automaticky aktualizují. Proto se před instalací aktualizace ujistěte, že všechny systémové servery lokality splňují nové požadavky na operace s novou verzí aktualizace.  

Při prvním použití konzoly Configuration Manager po instalaci aktualizace se zobrazí výzva k aktualizaci této konzoly.  Pokud to chcete udělat, musíte spustit instalační program Configuration Manager v počítači, který je hostitelem konzoly, a pak zvolit možnost aktualizace konzoly. Instalaci aktualizace konzoly doporučujeme neodkládat.

**Známé problémy pro tuto aktualizaci**   
Po zobrazení stavu instalace balíčku aktualizace platí následující problémy:
- Při aktualizaci z verze 1602 na 1606 zobrazuje krok **extrakce datové části balíčku aktualizace** stav **Nezahájeno**, a to i v případě, že stahování bylo dokončeno.
- Při aktualizaci z verze 1511 na 1606 se v některých krocích zobrazí stav **dokončeno** , ale nezobrazí se hodnota **čas poslední aktualizace**.


## <a name="checklist"></a>Kontrolní seznam  

**Ujistěte se, že všechny lokality používají podporovanou verzi Configuration Manager:**  Než začnete s instalací aktualizace 1606, musí mít každý server lokality v hierarchii spuštěnou stejnou verzi Configuration Manager: buď verze 1511, nebo 1602.

**Zkontrolujte nainstalované verze Microsoft.NET na serverech systému lokality:** Když lokalita nainstaluje aktualizaci 1606, Configuration Manager automaticky nainstaluje .NET Framework 4.5.2 do každého počítače, který je hostitelem jedné z následujících rolí systému lokality (Pokud ještě není nainstalovaná .NET Framework 4,5 nebo novější):  

- Zprostředkující bod registrace  

- Bod registrace  

- Bod správy  

- Spojovací bod služby  

Tato instalace může server systému lokality uvést do stavu čekání na restartování a ohlásit chyby do Configuration Manager Viewer stavu komponent. Kromě toho může v aplikacích .NET na serveru docházet k náhodným chybám, dokud se server nerestartuje.  

Další informace najdete v tématu [požadavky na lokalitu a systém lokality](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

**Zkontrolujte stav lokality a hierarchie a ověřte, že nejsou přítomné žádné nevyřešené problémy:** Před aktualizací lokality vyřešte všechny provozní problémy serveru lokality, serveru databáze lokality a rolí systému lokality, které jsou nainstalované na vzdálených počítačích. Aktualizace lokality může kvůli existujícím provozním problémům selhat.

Další informace najdete v tématu [použití výstrah a stavového systému pro Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

**Zkontrolujte replikaci souborů a dat mezi lokalitami:**  Ujistěte se, že je replikace souborů a databáze mezi lokalitami v provozu a aktuální. Zpoždění nebo nevyřízené položky můžou bránit hladké úspěšné aktualizaci.    

U replikace databáze můžete k řešení problémů před spuštěním aktualizace použít Analyzátor propojení replikace. Další informace najdete v tématu [o analyzátor propojení replikace](monitor-replication.md#BKMK_RLA).  


**Nainstalujte všechny použitelné kritické aktualizace operačních systémů na počítače, které jsou hostitelem lokality, serveru databáze lokality a rolí vzdáleného systému lokality:** Před instalací aktualizace pro Configuration Manager nainstalujte všechny důležité aktualizace pro každý příslušný systém lokality. Jestliže aktualizace, kterou instalujete, vyžaduje restart, před spuštěním upgradu restartujte příslušné počítače.  

**Zakažte repliky databáze pro body správy v primárních lokalitách:** Configuration Manager nemůže úspěšně aktualizovat primární lokalitu, která má povolenou repliku databáze pro body správy. Před instalací aktualizace pro Configuration Manager zakažte replikaci databáze.  

Další informace najdete v tématu [repliky databáze pro body správy pro Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Nastavit SQL Server skupiny dostupnosti AlwaysOn na ruční převzetí služeb při selhání:**  
Před instalací aktualizací, jako je verze 1606, se ujistěte, že je skupina dostupnosti nastavená na ruční převzetí služeb při selhání. Po aktualizaci lokality můžete obnovit převzetí služeb při selhání automaticky. Další informace najdete v tématu [SQL Server AlwaysOn pro databázi lokality](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Znovu nakonfigurujte body aktualizace softwaru, které používají služby NLB:** Configuration Manager nemůže aktualizovat lokalitu, která pro hostování bodů aktualizace softwaru používá cluster služby Vyrovnávání zatížení sítě (NLB).  

Pokud pro body aktualizace softwaru používáte clustery služby Vyrovnávání zatížení sítě, odeberte cluster programu NLB pomocí prostředí Windows PowerShell.    

Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).  

**Zakažte všechny úlohy údržby lokality v každé lokalitě po dobu trvání instalace aktualizace na této lokalitě:** Před instalací aktualizace zakažte všechny úlohy údržby lokality, které by mohly běžet během doby, kdy je proces aktualizace aktivní. To zahrnuje, avšak není omezeno jen na:  

- Zálohovat server lokality  

- Vymazat staré operace klientů  

- Vymazat stará data zjišťování  

Pokud se během instalace aktualizace spustí některá úloha údržby databáze lokality, při instalaci aktualizace může dojít k chybě. Než úlohu zakážete, zaznamenejte plán úlohy, abyste po instalaci aktualizace mohli obnovit její konfiguraci.  

Další informace najdete v tématu [úlohy údržby pro Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) a [Referenční dokumentace k úlohám údržby pro Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Dočasně zastavit veškerý antivirový software na Configuration Managerch serverech:** Než aktualizujete lokalitu, ujistěte se, že jste zastavili antivirový software na serverech Configuration Manager. <!--SMS.503481--> 

**Vytvořte zálohu databáze lokality v lokalitě centrální správy a primárních lokalitách:** Před aktualizací lokality proveďte zálohu databáze lokality, abyste měli jistotu, že máte použitelnou úspěšnou zálohu pro případ zotavení po havárii.   

Další informace najdete v tématu [zálohování a obnovení pro Configuration Manager](backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Naplánujte pilotní nasazení klienta:** Když nainstalujete aktualizaci, která aktualizuje klienta, můžete novou aktualizaci klienta otestovat v předprodukčním prostředí ještě před tím, než se nasadí a upgraduje všechny aktivní klienty.   

Pokud chcete tuto možnost využít, musíte před zahájením instalace aktualizace nakonfigurovat lokalitu tak, aby podporovala automatické upgrady pro předprodukční prostředí. Další informace najdete v tématu [upgrade klientů](../../../core/clients/manage/upgrade/upgrade-clients.md) .   
[Testování upgradu klienta v předprodukční kolekci](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**Naplánování použití oken služby k řízení, kdy servery lokality instalují aktualizace:** Pomocí oken služby můžete definovat dobu, během které je možné nainstalovat aktualizace serveru lokality.

Můžete tak stanovit čas instalace aktualizací v lokalitách v rámci vaší hierarchie.
Před verzí 1606 se v oknech služby nazývala okna údržby. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).  

**Spusťte kontrolu požadovaných součástí instalace:**  Před instalací aktualizace 1606 můžete spustit kontrolu požadovaných součástí nezávisle na instalaci aktualizace. Po instalaci aktualizace na lokalitu se Kontrola požadovaných součástí spustí znovu.  

Další informace najdete v části **Krok 3: spuštění kontroly požadovaných součástí před instalací aktualizace** v tématu [aktualizace pro Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) .  

> [!IMPORTANT]  
> Pokud se Kontrola požadovaných součástí spouští nezávisle nebo v rámci instalace aktualizace, proces aktualizuje některé zdrojové soubory produktu, které se používají pro úlohy údržby lokality. Proto po spuštění kontroly požadovaných součástí, ale před instalací aktualizace 1606, potřebujete-li provést úlohu údržby lokality, spusťte **Setupwpf. exe** (Configuration Manager instalační program) z disku CD-ROM. Poslední složka na serveru lokality.  

**Aktualizujte lokality:** Teď jste připraveni spustit instalaci aktualizací ve své hierarchii.  
Doporučujeme, abyste instalaci aktualizace naplánovali pro každou lokalitu mimo běžnou pracovní dobu, kdy bude mít proces instalace aktualizace a jejích akcí pro přeinstalaci součástí lokality a rolí systému lokality nejmenší dopad na vaše obchodní operace.

Další informace najdete v tématu [aktualizace pro Configuration Manager](../../../core/servers/manage/updates.md).  
