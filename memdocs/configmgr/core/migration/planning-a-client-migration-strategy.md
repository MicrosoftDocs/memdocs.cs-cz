---
title: Plánování migrace klientů
titleSuffix: Configuration Manager
description: Přečtěte si o úlohách, které migrují klienty ze zdrojové hierarchie do cílové hierarchie Configuration Manager aktuální větve.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720909"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Plánování strategie migrace klientů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li migrovat klienty ze zdrojové hierarchie do cílové hierarchie Configuration Manager aktuální větve, je třeba provést dvě úlohy. Nejprve je nutné migrovat objekty, které jsou přidruženy ke klientovi, a poté přeinstalovat nebo přeřadit klienty ze zdrojové do cílové hierarchie. Nejprve proveďte migraci objektů, aby byly při migraci klientů k dispozici. Objekty přidružené ke klientovi se migrují pomocí úloh migrace. Informace o tom, jak migrovat objekty, které jsou přidružené ke klientovi, najdete v tématu [Plánování strategie úloh migrace](../../core/migration/planning-a-migration-job-strategy.md).  

 Následující části vám pomohou naplánovat migraci klientů do cílové hierarchie.  

-   [Plánování migrace klientů do cílové hierarchie](#Planning_for_Client_Agent_Migration)  

-   [Plánování zpracování dat spravovaných klienty při migraci](#Planning_for_Client_Data_Migration)  

-   [Plánování inventáře a dat o dodržování předpisů během migrace](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Plánování migrace klientů do cílové hierarchie  
 Když migrujete klienty ze zdrojové hierarchie nástroje, klientský software v klientském počítači se upgraduje tak, aby odpovídal verzi produktu cílové hierarchie.  

-   **Zdrojová hierarchie Configuration Manager 2007:** Při migraci klientů ze zdrojové hierarchie s podporovanou verzí nástroje Configuration Manager klientský software provede upgrade na verzi klienta cílové hierarchie.  

-   **Zdrojová hierarchie služby System Center 2012 Configuration Manager nebo novější:** Při migraci klientů mezi hierarchiemi se stejnou verzí produktu se klientský software nemění ani neupgraduje. Klient je pouze přeřazen ze zdrojové hierarchie do lokality v cílové hierarchii.  

    > [!NOTE]  
    >  Není-li verze produktu hierarchie podporována pro migraci do cílové hierarchie, proveďte upgrade všech lokalit a klientů ve zdrojové hierarchii na kompatibilní verzi produktu. Jakmile bude zdrojová hierarchie upgradována na podporovanou verzi produktu, můžete provést migraci mezi hierarchiemi. Další informace najdete v tématu [verze Configuration Manager podporované pro migraci](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) v článku [požadavky pro migraci](../../core/migration/prerequisites-for-migration.md).  

Následující informace vám pomohou při plánování migrace klientů:  

-   Chcete-li upgradovat nebo přeřadit klienty ze zdrojové do cílové lokality, můžete použít libovolnou metodu nasazení klienta podporovanou pro nasazování klientů v cílové hierarchii. Mezi typické metody nasazování klientů patří klientská nabízená instalace, distribuce softwaru, zásady skupiny a klientská instalace na základě aktualizace softwaru. Další informace najdete v tématu [metody instalace klientů](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Zkontrolujte, zda zařízení, které spouští software klienta ve zdrojové hierarchii, splňuje minimální hardwarové požadavky a používá operační systém podporovaný verzí Configuration Manager v cílové hierarchii.  

-   Před migrací klienta spusťte úlohu migrace za účelem migrace informací, které bude klient používat v cílové hierarchii.  

-   Klienti, kteří upgradují, si zachovají historii spuštění pro nasazení. To zabrání v tom, aby se nasazení v cílové hierarchii zbytečně nepoužívalo.  

    -   U klientů Configuration Manager 2007 se uchovává historie spuštění reklam.  

    -   Pro klienty ze System Center 2012 Configuration Manager nebo Configuration Manager aktuální větve se zachová historie spuštění nasazení.  

-   Klienty z lokalit ve zdrojové hierarchii lze migrovat v libovolném pořadí. Zvažte však možnost migrace omezeného počtu klientů v několika fázích místo migrace velkého počtu klientů najednou. Rozfázovaná migrace snižuje nároky na šířku pásma sítě a zpracování serverem, když každý nově upgradovaný klient odesílá do přiřazené lokality celý svůj počáteční inventář a data o shodě.  

-   Při migraci klientů Configuration Manager 2007 se z klientského počítače odinstaluje existující software klienta a nainstaluje se nový software klienta.  

-   Configuration Manager nemůže migrovat klienta Configuration Manager 2007, který má nainstalovaného klienta sady App-V, pokud verze klienta sady App-V není 4,6 SP1 nebo novější.  

Proces migrace klienta můžete sledovat v uzlu **migrace** v pracovním prostoru **Správa** v konzole nástroje Configuration Manager.  

Po dokončení migrace klienta do cílové hierarchie již nebude možné spravovat toto zařízení pomocí zdrojové hierarchie. měli byste zvážit odebrání klienta ze zdrojové hierarchie. Ačkoli to není při migraci hierarchií bezpodmínečně nutné, předejdete tím identifikací migrovaného klienta v sestavě zdrojové hierarchie nebo nesprávnému počtu prostředků mezi dvěma hierarchiemi během migrace. Pokud necháte migrovaného klienta v databázi zdrojové lokality, může dojít například k tomu, že po spuštění sestavy aktualizací softwaru bude počítač nesprávně identifikován jako nespravovaný prostředek, ačkoli je nyní spravován cílovou hierarchií.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a>Plánování zpracování dat spravovaných klienty při migraci  
Pokud migrujete klienta ze zdrojové do cílové hierarchie, zůstanou některé informace v zařízení zachovány, zatímco jiné informace přestanou být po migraci zařízení dostupné.  

V klientském zařízení zůstanou zachovány tyto informace:  

-   Jedinečný identifikátor (GUID), který přidruží klienta k informacím v databázi Configuration Manager.  

-   Historie reklam nebo nasazení, která zamezuje zbytečnému opětovnému spouštění reklam nebo nasazení v cílové hierarchii.  

V klientském zařízení nezůstanou zachovány tyto informace:  

-   Soubory v mezipaměti klienta. Pokud klient potřebuje tyto soubory k instalaci softwaru, znovu si je stáhne z cílové hierarchie.  

-   Informace ze zdrojové hierarchie o veškerých reklamách nebo nasazeních, které dosud nebyly spuštěny. Pokud chcete, aby klient spustil reklamy nebo nasazení po dokončení migrace, musíte je do klienta v cílové hierarchii znovu nasadit.  

-   Informace o inventáři. Klient znovu odešle tyto informace do přiřazené lokality v cílové hierarchii poté, co klient provede migraci a vytvoří se nová data klienta.  

-   Data o shodě. Klient znovu odešle tyto informace do přiřazené lokality v cílové hierarchii poté, co klient provede migraci a vytvoří se nová data klienta.  

Při migraci klienta se neuchovávají informace uložené v registru klienta Configuration Manager a v cestě k souboru. Po dokončení migrace znovu nakonfigurujte tato nastavení. Mezi typická nastavení patří:  

-   Schémata nastavení napájení  

-   Nastavení protokolování  

-   Nastavení místních zásad  

Kromě toho může být nutné přeinstalovat některé aplikace.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Plán pro inventář a data dodržování předpisů při migraci  
Inventář klienta a data o shodě nebudou při migraci klienta do cílové hierarchie uložena. Tyto informace jsou v cílové hierarchii nově vytvořeny poté, co je klient poprvé odešle do přiřazené lokality. Chcete-li snížit výsledné nároky na šířku pásma sítě a zpracování serverem, zvažte, zda nebude výhodnější migrovat menší počty klientů v několika fázích než migrovat velký počet klientů najednou.  

 Kromě toho nelze ze zdrojové hierarchie migrovat vlastní nastavení inventáře hardwaru. To je třeba přenést do cílové hierarchie nezávisle na migraci. Informace o tom, jak rozšíříte inventář hardwaru, najdete v tématu [Konfigurace inventáře hardwaru](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
