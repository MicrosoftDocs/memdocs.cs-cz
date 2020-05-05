---
title: Strategie zdrojové hierarchie
titleSuffix: Configuration Manager
description: Před konfigurací Configuration Manager úlohy migrace nakonfigurujte zdrojovou hierarchii a Shromážděte data ze zdrojové lokality.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719677"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Plánování strategie zdrojové hierarchie v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Před nastavením úlohy migrace v prostředí Configuration Manager musíte nakonfigurovat zdrojovou hierarchii a shromažďovat data z nejméně jedné zdrojové lokality v této hierarchii. Následující části vám pomůžou naplánovat konfiguraci zdrojových hierarchií, konfiguraci zdrojových lokalit a určení způsobu, jakým Configuration Manager shromažďuje informace ze zdrojových lokalit ve zdrojové hierarchii. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a> Zdrojové hierarchie  
Zdrojová hierarchie je Configuration Manager hierarchie, která obsahuje data, která chcete migrovat. Když nastavíte migraci a určíte zdrojovou hierarchii, určíte lokalitu nejvyšší úrovně ve zdrojové hierarchii. Tato lokalita se rovněž nazývá zdrojová lokalita. Další lokality, ze kterých můžete migrovat data ze zdrojové hierarchie, se nazývají taky zdrojové lokality.  

-   Když nastavíte úlohu migrace pro migraci dat ze zdrojové hierarchie Configuration Manager 2007, konfigurujete ji pro migraci dat z jedné nebo více konkrétních zdrojových lokalit ve zdrojové hierarchii.  

-   Když nastavíte úlohu migrace pro migraci dat ze zdrojové hierarchie, na které běží System Center 2012 Configuration Manager nebo novější, stačí zadat jenom lokalitu nejvyšší úrovně.  

V jednom okamžiku můžete nastavit jenom jednu zdrojovou hierarchii.  

-   Pokud nastavíte novou zdrojovou hierarchii, bude se tato hierarchie automaticky nacházet aktuální zdrojovou hierarchií, která nahradí předchozí zdrojovou hierarchii.  

-   Při nastavování zdrojové hierarchie je nutné určit lokalitu nejvyšší úrovně ve zdrojové hierarchii a zadat přihlašovací údaje, které Configuration Manager použít pro připojení k poskytovateli služby SMS a k databázi lokality této zdrojové lokality.  

-   Configuration Manager používá tato pověření ke spuštění shromažďování dat za účelem načtení informací o objektech a distribučních bodech ze zdrojové lokality.  

-   V rámci procesu shromažďování dat jsou ve zdrojové hierarchii identifikovány podřízené lokality.  

-   Pokud je zdrojová hierarchie hierarchií Configuration Manager 2007, můžete nastavit tyto další lokality jako zdrojové lokality s oddělenými přihlašovacími údaji pro každou zdrojovou lokalitu.  

I když můžete nastavit více zdrojových hierarchií po sobě, migrace je aktivní jenom pro jednu zdrojovou hierarchii.  

-   Pokud jste nastavili další zdrojovou hierarchii před dokončením migrace z aktuální zdrojové hierarchie, Configuration Manager zruší všechny aktivní úlohy migrace a odloží všechny plánované úlohy migrace pro aktuální zdrojovou hierarchii.  

-   Nově nakonfigurovaná zdrojová hierarchie se pak bude nacházet v aktuální zdrojové hierarchii a původní zdrojová hierarchie je teď neaktivní.  

-   Pak můžete nastavit přihlašovací údaje pro připojení, další zdrojové lokality a úlohy migrace pro novou zdrojovou hierarchii.  

Pokud obnovíte neaktivní zdrojovou hierarchii a zatím jste nepoužívali **data migrace čištění**, můžete zobrazit dříve nakonfigurované úlohy migrace pro tuto zdrojovou hierarchii. Než však budete moci pokračovat v migraci z této hierarchie, je třeba znovu nakonfigurovat přihlašovací údaje pro připojení k příslušným zdrojovým lokalitám v této hierarchii a následně přeplánovat všechny úlohy migrace, které nebyly dokončeny.  

> [!CAUTION]  
>  Jestliže provádíte migraci dat z více než jedné zdrojové hierarchie, musí každá další zdrojová hierarchie obsahovat jedinečný soubor kódů lokalit.  
> Zdrojové a cílové hierarchie také vyžadují různé sady kódů lokalit.

Další informace o konfiguraci zdrojové hierarchie najdete v tématu [Konfigurace zdrojových hierarchií a zdrojových lokalit pro migraci na Configuration Manager aktuální větev](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md) .  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a>Zdrojové lokality  
 Zdrojové lokality jsou lokality ve zdrojové hierarchii, v nichž jsou obsažena data, která chcete migrovat. Lokalita nejvyšší úrovně ve zdrojové hierarchii je vždy první zdrojová lokalita. Když migrace shromažďuje data z první zdrojové lokality nové zdrojové hierarchie, zjišťuje informace o dalších lokalitách v této hierarchii.  

 Po skončení shromažďování dat u počáteční zdrojové lokality závisí další kroky na verzi produktu zdrojové hierarchie.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Zdrojové lokality, které používají Configuration Manager 2007 SP2  
 Po shromáždění dat z počáteční zdrojové lokality hierarchie Configuration Manager 2007 SP2 není nutné před vytvořením úloh migrace nastavovat další zdrojové lokality. Než však budete moci migrovat data z dalších lokalit, je třeba nastavit další lokality jako zdrojové lokality a Configuration Manager musí z těchto lokalit úspěšně shromažďovat data.  

 Chcete-li shromáždit data z dalších lokalit, nastavte každou lokalitu jako zdrojovou lokalitu zvlášť. K tomu je potřeba zadat přihlašovací údaje pro Configuration Manager pro připojení k poskytovateli služby SMS a k databázi lokality každé zdrojové lokality. Po nastavení přihlašovacích údajů pro zdrojovou lokalitu začne proces shromažďování dat pro tuto lokalitu.  

 Když nastavíte další zdrojové lokality ve zdrojové hierarchii Configuration Manager 2007 SP2, je nutné nastavit zdrojové lokality shora dolů, což znamená, že se lokality na nejnižší úrovni nastavují jako poslední. Zdrojové lokality ve větvi hierarchie lze konfigurovat kdykoli, ale musíte nastavit lokalitu jako zdrojovou lokalitu, aby bylo možné nastavit některou z jejích podřízených lokalit jako zdrojové lokality.  

> [!NOTE]  
>  Pro migraci se podporují jenom primární lokality v hierarchii Configuration Manager 2007 SP2.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Zdrojové lokality, na kterých je spuštěný System Center 2012 Configuration Manager nebo novější  
 Po shromáždění dat z počáteční zdrojové lokality v hierarchii nástroje System Center 2012 Configuration Manager nebo novější není nutné v této zdrojové hierarchii nastavovat další zdrojové lokality. Důvodem je to, že na rozdíl od Configuration Manager 2007 používají tyto verze Configuration Manager sdílenou databázi a sdílená databáze umožňuje identifikovat a následně migrovat všechny dostupné objekty z počáteční zdrojové lokality.  

 Když nastavíte přístupové účty pro shromažďování dat, může být nutné udělit **účtu poskytovatele služby SMS zdrojového webového serveru** přístup k více počítačům ve zdrojové hierarchii. To může být nutné, když zdrojová lokalita podporuje víc instancí poskytovatele služby SMS, každou v jiném počítači. Po zahájení shromažďování dat kontaktuje lokalita nejvyšší úrovně v cílové hierarchii lokalitu nejvyšší úrovně ve zdrojové hierarchii, aby určila umístění poskytovatele služby SMS pro tuto lokalitu. Je určena pouze první instance poskytovatele služby SMS. Nemůže-li proces shromažďování dat získat přístup k poskytovateli služby SMS v určeném umístění, proces selže a nepokusí se připojit k dalším počítačům, ve kterých je spuštěna instance poskytovatele služby SMS pro tuto lokalitu.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a>Shromažďování dat  
 Ihned po určení zdrojové hierarchie, nastavení přihlašovacích údajů pro každou další zdrojovou lokalitu ve zdrojové hierarchii nebo nasdílení distribučních bodů pro zdrojovou lokalitu Configuration Manager začne shromažďovat data ze zdrojové lokality.  

 Proces shromažďování dat se pak opakuje podle jednoduchého plánu kvůli zachování synchronizace s případnými změnami dat ve zdrojové lokalitě. Ve výchozím nastavení se tento proces opakuje každé čtyři hodiny. Plán pro tento cyklus můžete změnit úpravou **vlastností** zdrojové lokality. Proces prvotního shromažďování dat musí zkontrolovat všechny objekty v databázi Configuration Manager a dokončit může trvat dlouhou dobu. Následné procesy shromažďování dat zjišťují pouze změny v datech a jejich dokončení vyžaduje méně času.  

 Při shromažďování dat se lokalita nejvyšší úrovně v cílové hierarchii připojí k poskytovateli služby SMS a k databázi webu zdrojové lokality, z níž načte seznam objektů a distribučních bodů. Tato připojení používají účty pro přístup ke zdrojové lokalitě. Informace o požadovaných konfiguracích pro shromažďování dat najdete v tématu [předpoklady pro migraci](../../core/migration/prerequisites-for-migration.md).  

 Proces shromažďování dat můžete spustit a zastavit pomocí shromažďování **dat** a **Zastavit shromažďování dat** v konzole Configuration Manager.  

 Po použití nástroje **Zastavit shromažďování dat** ze zdrojové lokality z nějakého důvodu je třeba znovu nakonfigurovat přihlašovací údaje pro lokalitu, aby bylo možné data z této lokality znovu shromáždit. Dokud neprovedete konfiguraci zdrojové lokality, Configuration Manager nemůže identifikovat nové objekty nebo změny v dříve migrovaných objektech v dané lokalitě.  

> [!NOTE]  
>  Předtím, než rozšíříte samostatnou primární lokalitu do hierarchie s lokalitou centrální správy, je nutné zastavit veškeré shromažďování dat. Po dokončení rozšíření lokality můžete shromažďování dat znovu nakonfigurovat.  

### <a name="gather-data-now"></a>Shromáždit data nyní  
 Po provedení počátečního procesu shromažďování dat u dané lokality se pak tento proces opakuje za účelem identifikace objektů, jež byly aktualizovány od posledního cyklu shromažďování dat. Můžete také použít akci **shromáždit data nyní** v konzole Configuration Manager pro okamžité spuštění procesu a resetování času zahájení dalšího cyklu.  

 Po úspěšném dokončení procesu shromažďování dat pro zdrojovou lokalitu lze sdílet distribuční body ze zdrojové lokality a konfigurovat úlohy migrace pro migraci dat z této lokality. Shromažďování dat je opakovaný proces pro migraci a pokračuje, dokud nezměníte zdrojovou hierarchii nebo nepoužijete příkaz **Zastavit shromažďování dat** k ukončení procesu shromažďování dat pro tuto lokalitu.  

### <a name="stop-gathering-data"></a>Zastavit shromažďování dat  
 Chcete-li ukončit proces shromažďování dat pro zdrojovou lokalitu, pokud již nechcete, Configuration Manager identifikovat nové nebo změněné objekty z této lokality, můžete použít možnost **Zastavit shromažďování dat** . Tato akce také brání Configuration Manager z nabídky klientů v cílové hierarchii všechny sdílené distribuční body ze zdroje jako umístění obsahu pro obsah, který jste migrovali.  

 Chcete-li zastavit shromažďování dat z jednotlivých zdrojových lokalit, je nutné spustit příkaz **Zastavit shromažďování dat** ve zdrojových lokalitách nejnižší úrovně a poté tento postup opakovat v každé nadřazené lokalitě. Lokalita nejvyšší úrovně ve zdrojové hierarchii musí být poslední lokalitou, u níž shromažďování dat zastavíte. Shromažďování dat je nutné zastavit u každé podřízené lokality před provedením stejné akce u nadřazené lokality. Obvykle se shromažďování dat zastavuje pouze tehdy, když jste připraveni dokončit proces migrace.  

 Jakmile zastavíte shromažďování dat pro zdrojovou lokalitu, informace o objektech a kolekcích z této lokality, které byly dříve shromážděny, zůstávají k dispozici pro použití při nastavování nových úloh migrace. Neuvidíte však žádné nové objekty ani kolekce, ani neuvidíte změny provedené u stávajících objektů. Jestliže zdrojovou lokalitu znovu nakonfigurujete a začnete data znovu shromažďovat, uvidíte informace o dříve migrovaných objektech i jejich stav.  
