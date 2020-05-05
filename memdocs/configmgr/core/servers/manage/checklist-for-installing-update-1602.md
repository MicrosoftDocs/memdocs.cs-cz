---
title: Kontrolní seznam pro 1602
titleSuffix: Configuration Manager
description: Přečtěte si o akcích, které je potřeba provést před aktualizací z verze Configuration Manager 1511 na verzi 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717857"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Kontrolní seznam pro instalaci aktualizace 1602 pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Před aktualizací z verze Configuration Manager 1511 na verzi 1602 si Projděte následující informace a kontrolní seznam pro akce, které je nutné před zahájením aktualizace provést.  

 **O instalaci aktualizace 1602:**  

 Aktualizace 1602 se dá instalovat jenom v lokalitě nejvyšší úrovně v hierarchii. To znamená, že instalaci zahájíte z lokality centrální správy, pokud ji máte, nebo ze samostatné primární lokality.  

-   Podřízené primární lokality instalují aktualizaci automaticky po dokončení instalace aktualizace lokalitou centrální správy. Časová období údržby můžete použít k určení, kdy lokalita nainstaluje aktualizace. Od vydání aktualizace 1602 byly časové intervaly pro správu a údržbu přejmenovány na *Windows*. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).  

-   Sekundární lokality je nutné ručně aktualizovat v konzole Configuration Manager po dokončení instalace aktualizace primárním serverem nadřazené lokality. Automatické aktualizace serverů sekundárních lokalit nejsou podporovány.  

Když server lokality nainstaluje aktualizaci, role systému lokality nainstalované na serveru lokality a ty, které jsou nainstalované na vzdálených počítačích, se automaticky aktualizují. Proto se před instalací aktualizace ujistěte, že všechny systémové servery lokality splňují nové požadavky na operace s novou verzí aktualizace.  

Při prvním použití konzoly Configuration Manager po dokončení aktualizace se zobrazí výzva k aktualizaci této konzoly. Pokud to chcete udělat, musíte spustit instalační program Configuration Manager v počítači, který je hostitelem konzoly, a vybrat možnost aktualizovat konzolu. Instalaci aktualizace konzoly doporučujeme neodkládat.  

 **Téma**  

 **Ujistěte se, že všechny lokality používají podporovanou verzi Configuration Manager:**  Aby bylo možné spustit instalaci aktualizace Update 1602, musí každý server lokality v hierarchii běžet Configuration Manager verze 1511.  

 **Přečtěte si nainstalované verze Microsoft .NET na serverech systému lokality:** Když lokalita nainstaluje aktualizaci 1602, Configuration Manager automaticky nainstaluje .NET Framework 4.5.2 do každého počítače, který je hostitelem jedné z následujících rolí systému lokality (Pokud ještě není nainstalovaná .NET Framework 4,5 nebo novější):  

-   Zprostředkující bod registrace  

-   Bod registrace  

-   Bod správy  

-   Spojovací bod služby  

Tato instalace může umístit server systému lokality do stavu čekání na restartování a ohlásit chyby do Configuration Manager prohlížeč stavu komponent. Kromě toho můžou aplikace .NET na serveru docházet k náhodným chybám, dokud se server nerestartuje.  

 Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Zkontrolujte stav lokality a hierarchie a ověřte, že nejsou přítomné žádné nevyřešené problémy:** Před aktualizací lokality vyřešte všechny provozní problémy serveru lokality, serveru databáze lokality a rolí systému lokality, které jsou nainstalované na vzdálených počítačích. Aktualizace lokality může kvůli existujícím provozním problémům selhat.  

Další informace najdete v tématu [použití výstrah a stavového systému pro Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Zkontrolujte replikaci souborů a dat mezi lokalitami:**  Ujistěte se, že je replikace souborů a databáze mezi lokalitami v provozu a aktuální. Zpoždění nebo nevyřízené položky můžou bránit hladké úspěšné aktualizaci.    

U replikace databáze můžete k řešení problémů před spuštěním aktualizace použít Analyzátor propojení replikace.    

 Další informace najdete v tématu [o analyzátor propojení replikace](monitor-replication.md#BKMK_RLA).  

 **Nainstalujte všechny použitelné kritické aktualizace operačních systémů na počítače, které jsou hostitelem lokality, serveru databáze lokality a rolí vzdáleného systému lokality:** Před instalací aktualizace pro Configuration Manager nainstalujte všechny důležité aktualizace pro každý příslušný systém lokality. Jestliže aktualizace, kterou instalujete, vyžaduje restart, před spuštěním upgradu restartujte příslušné počítače.  

 **Zakažte repliky databáze pro body správy v primárních lokalitách:** Configuration Manager nemůže úspěšně aktualizovat primární lokalitu, která má povolenou repliku databáze pro body správy. Repliky databáze zakažte dříve než:  

-   Vytvořte zálohu databáze lokality pro otestování upgradu databáze.  

-   Nainstalujte aktualizaci pro Configuration Manager.  

Další informace najdete v tématu [repliky databáze pro body správy pro Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Znovu nakonfigurujte body aktualizace softwaru, které používají služby NLB:** Configuration Manager nemůže aktualizovat lokalitu, která pro hostování bodů aktualizace softwaru používá cluster služby Vyrovnávání zatížení sítě (NLB).  Pokud pro body aktualizace softwaru používáte clustery služby Vyrovnávání zatížení sítě, odeberte cluster programu NLB pomocí prostředí Windows PowerShell.    

 Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).  

 **Zakažte všechny úlohy údržby lokality v každé lokalitě po dobu trvání instalace aktualizace na této lokalitě:** Před instalací aktualizací zakažte všechny úlohy údržby lokality, které by mohly běžet v době, kdy je proces aktualizace aktivní. Mezi tyto úlohy patří (ale nejsou omezené) k následujícím akcím:  

-   Zálohovat server lokality  

-   Vymazat staré operace klientů  

-   Vymazat stará data zjišťování  

Pokud se během instalace aktualizace spustí některá úloha údržby databáze lokality, při instalaci aktualizace může dojít k chybě. Než úlohu zakážete, zaznamenejte plán úlohy, abyste po instalaci aktualizace mohli obnovit její konfiguraci.  

 Další informace najdete v tématu [úlohy údržby pro Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) a [Referenční dokumentace k úlohám údržby pro Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Dočasně zastavit veškerý antivirový software na Configuration Managerch serverech:** Než aktualizujete lokalitu, ujistěte se, že jste zastavili antivirový software na serverech Configuration Manager. <!--SMS.503481--> 

 **Vytvořte zálohu databáze lokality v lokalitě centrální správy a primárních lokalitách:** Než aktualizujete lokalitu, zálohujte databázi lokality, abyste měli jistotu, že máte úspěšnou zálohu pro použití při zotavení po havárii.   

Další informace najdete v tématu [zálohování a obnovení pro Configuration Manager](backup-and-recovery.md).  

 **Zálohujte přizpůsobený soubor Configuration. mof:** Použijete-li přizpůsobený soubor Configuration. mof k definování datových tříd, které používáte s inventářem hardwaru, vytvořte před aktualizací lokality zálohu tohoto souboru. Po aktualizaci obnovte tento soubor na webu verze 1602. Při aktualizaci lokality se aktuální soubor přepíše původní (výchozí) verzí souboru. Další informace o používání tohoto souboru najdete v tématu [postup rozšiřování inventáře hardwaru](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testování upgradu databáze na kopii nejnovější zálohy databáze lokality:** Než aktualizujete Configuration Manager lokalitu centrální správy nebo primární lokalitu, otestujte proces upgradu databáze lokality na kopii databáze lokality.  

-   Měli byste otestovat proces upgradu databáze lokality, protože při upgradu lokality se může změnit databáze lokality.  

-   I když test testovací databáze není vyžadován, může identifikovat problémy s upgradem před tím, než bude ovlivněna vaše provozní databáze.  

-   Selhání upgradu databáze lokality může mít za následek, že vaše databáze lokality nebude funkční a může vyžadovat obnovení lokality.  

-   I když je databáze lokality sdílena mezi lokalitami v hierarchii nástroje, naplánujte otestování databáze v každé příslušné lokalitě před upgradem lokality.  

-   Pokud pro body správy v primární lokalitě používáte repliky databáze, před vytvořením zálohy databáze lokality zakažte replikaci.  

Configuration Manager nepodporuje zálohování sekundárních lokalit ani nepodporuje test upgradu databáze sekundární lokality.   
Nespouštějte upgrade testovací databáze na provozní databázi lokality. Tato činnost aktualizuje databázi lokality a může mít za následek nefunkčnost vaší lokality. Další informace najdete v části [Krok 2: testování upgradu databáze před instalací aktualizace](install-in-console-updates.md#bkmk_step2) **před instalací konzolové aktualizace**.  

 **Naplánujte pilotní nasazení klienta:** Když nainstalujete aktualizaci, která aktualizuje klienta, můžete novou aktualizaci klienta otestovat v předprodukčním prostředí ještě před tím, než se nasadí a upgraduje všechny aktivní klienty.   

 Pokud chcete tuto možnost využít, musíte nakonfigurovat lokalitu tak, aby podporovala automatické upgrady pro předprodukční prostředí před zahájením instalace aktualizace. Další informace najdete v tématu [upgrade klientů](../../../core/clients/manage/upgrade/upgrade-clients.md) .   
[Testování upgradu klienta v předprodukční kolekci](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Naplánujte použití časových období údržby k řízení, kdy servery lokality instalují aktualizace:** Časové intervaly pro správu a údržbu můžete použít k definování časového období, během kterého lze nainstalovat aktualizace serveru lokality. Můžete tak stanovit čas instalace aktualizací v lokalitách v rámci vaší hierarchie.   

Od vydání aktualizace 1602 byly časové intervaly pro správu a údržbu přejmenovány na *Windows*. Další informace najdete v tématu [Služba pro servery lokality](service-windows.md).  

 **Spusťte kontrolu požadovaných součástí instalace:**  Před instalací aktualizace 1602 můžete spustit kontrolu požadovaných součástí nezávisle na instalaci aktualizace. Po instalaci aktualizace na lokalitu se Kontrola požadovaných součástí spustí znovu.  

Další informace najdete v části **Krok 3: spuštění kontroly požadovaných součástí před instalací aktualizace** v tématu [aktualizace pro Configuration Manager](../../../core/servers/manage/updates.md) .  

> [!IMPORTANT]  
>  Pokud se Kontrola požadovaných součástí spouští nezávisle nebo v rámci instalace aktualizace, proces aktualizuje některé zdrojové soubory produktu, které se používají pro úlohy údržby lokality. Proto po spuštění kontroly požadovaných součástí, ale před instalací aktualizace 1602, potřebujete-li provést úlohu údržby lokality, spusťte **program setupwfe. exe** (Configuration Manager instalační program) z disku CD-ROM. Poslední složka na serveru lokality.  

 **Aktualizujte lokality:** Teď jste připraveni spustit instalaci aktualizací ve své hierarchii. Doporučujeme, abyste instalaci aktualizace naplánovali pro každou lokalitu mimo běžnou pracovní dobu, kdy bude mít proces instalace aktualizace a jejích akcí pro přeinstalaci součástí lokality a rolí systému lokality nejmenší dopad na vaše obchodní operace.

Další informace najdete v tématu [aktualizace pro Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Viz také  
 [Aktualizace pro Configuration Manager](../../../core/servers/manage/updates.md)
