---
title: Migrace dat
titleSuffix: Configuration Manager
description: Přečtěte si, jak přenést data ze zdrojové hierarchie do cílové hierarchie Configuration Manager.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718900"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrace dat mezi hierarchiemi v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí migrace přeneste data z podporované zdrojové hierarchie do cílové hierarchie Configuration Manager (Current Branch). Při migraci dat ze zdrojové hierarchie:  

- Přistupujete k datům z databází lokality ve zdrojové infrastruktuře a potom tato data přeneste do svého aktuálního prostředí.  

- Migrace nemění data ve zdrojové hierarchii. Místo toho zjistí data a uloží kopii do databáze cílové hierarchie.  

Při plánování strategie migrace Vezměte v úvahu následující body:  

- Stávající infrastrukturu Configuration Manager 2007 SP2 můžete migrovat do Configuration Manager (Current Branch).  

- Ze zdrojové lokality můžete migrovat buď všechna podporovaná data, nebo jejich část.  

- Data z jedné zdrojové lokality můžete migrovat do několika různých lokalit v cílové hierarchii.  

- Data z víc zdrojových lokalit můžete přesunout do jedné lokality v cílové hierarchii.  


Následující video popisuje a ukazuje dva běžné [scénáře migrace](#BKMK_MigrationScenarios). Obsahuje taky možnosti, které zahrnují Microsoft Azure v plánech migrace.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a>Charakteristiky  

 Configuration Manager v průběhu migrace používá následující pojmy a pojmy.  

#### <a name="source-hierarchy"></a>Zdrojová hierarchie
Hierarchie, která používá podporovanou verzi Configuration Manager a obsahuje data, která chcete migrovat. Při nastavování migrace identifikujete zdrojovou hierarchii, když určíte lokalitu nejvyšší úrovně ve zdrojové hierarchii. Po určení zdrojové hierarchie lokalita nejvyšší úrovně v cílové hierarchii shromáždí data z databáze příslušné zdrojové lokality a zjistí, která data chcete migrovat. 

Další informace najdete v tématu [zdrojové hierarchie](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Zdrojové lokality
Lokality ve zdrojové hierarchii obsahující data, která můžete migrovat do cílové hierarchie. 

Další informace najdete v tématu [zdrojové lokality](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Cílová hierarchie
Hierarchie Configuration Manager (Current Branch), ve které se při migraci spouští import dat ze zdrojové hierarchie.

#### <a name="data-gathering"></a>Shromažďování dat
Probíhající proces identifikace informací ve zdrojové hierarchii, které můžete migrovat do cílové hierarchie. Configuration Manager kontroluje zdrojovou hierarchii podle plánu. Tento proces identifikuje všechny změny informací ve zdrojové hierarchii, které jste předtím migrovali a které můžete chtít aktualizovat v cílové hierarchii.

Další informace najdete v tématu [shromažďování dat](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Úlohy migrace
Proces konfigurace určitých objektů pro migraci a následná správa migrace těchto objektů do cílové hierarchie.

Další informace najdete v tématu [Plánování strategie úloh migrace](planning-a-migration-job-strategy.md).

#### <a name="client-migration"></a>Migrace klientů
Proces přenosu informací používaných klienty z databáze zdrojové lokality do databáze cílové hierarchie. Tato migrace dat pak následuje upgrade klientského softwaru v zařízeních na verzi klientského softwaru z cílové hierarchie.

Další informace najdete v tématu [Plánování strategie migrace klientů](planning-a-client-migration-strategy.md).

#### <a name="shared-distribution-points"></a>Sdílené distribuční body
Distribuční body ze zdrojové hierarchie, které Configuration Manager sdílet s cílovou hierarchií během období migrace.

Během období migrace mohou klienti přiřazení k lokalitám v cílové hierarchii získat obsah ze sdílených distribučních bodů.

Další informace najdete v tématu [Sdílení distribučních bodů mezi zdrojovou a cílovou hierarchií](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Monitorování migrace
Proces monitorování aktivit migrace. Průběh a úspěšnost migrace můžete monitorovat z uzlu **migrace** v pracovním prostoru **Správa** .

Další informace najdete v tématu [Plánování monitorování aktivity migrace](planning-to-monitor-migration-activity.md).

#### <a name="stop-gathering-data"></a>Zastavit shromažďování dat
Proces zastavení shromažďování dat ze zdrojových lokalit. Když už data nebudete moct migrovat ze zdrojové hierarchie nebo pokud chcete pozastavit aktivity související s migrací, můžete nakonfigurovat cílovou hierarchii tak, aby se zastavilo shromažďování dat ze zdrojové hierarchie.

Další informace najdete v tématu [shromažďování dat](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Vyčištění dat migrace
Proces dokončení migrace ze zdrojové hierarchie odebráním informací o migraci z databáze cílové hierarchie.

Další informace najdete v tématu [plánování dokončení migrace](planning-to-complete-migration.md).



## <a name="typical-workflow"></a>Typický pracovní postup  

Postup nastavení pracovního postupu pro migraci:

1.  Určete podporovanou zdrojovou hierarchii.  

2.  Nastavte shromažďování dat. Shromažďování dat umožňuje Configuration Manager shromažďovat informace o datech, která lze migrovat ze zdrojové hierarchie.  

     Configuration Manager automaticky opakuje proces shromažďování dat podle jednoduchého plánu, dokud proces shromažďování dat nezastavíte. Ve výchozím nastavení se proces shromažďování dat opakuje každé čtyři hodiny, aby Configuration Manager mohl identifikovat změny dat ve zdrojové hierarchii. Shromažďování dat je rovněž nezbytné pro sdílení distribučních bodů.  

3.  Vytvořte úlohy migrace pro migraci dat mezi zdrojovou a cílovou hierarchií.  

4.  Proces shromažďování dat můžete kdykoli zastavit pomocí akce **Zastavit shromažďování dat** . Když zastavíte shromažďování dat, Configuration Manager již neidentifikuje změny dat ve zdrojové hierarchii a nemůže již nadále sdílet distribuční body. Tato akce se obvykle používá, pokud již neplánujete migraci dat nebo sdílení distribučních bodů ze zdrojové hierarchie.  

5.  Po zastavení shromažďování dat ve všech lokalitách zdrojové hierarchie můžete volitelně vyčistit data migrace pomocí akce **Vyčištění dat migrace** . Tato akce odstraní historická data o migraci ze zdrojové hierarchie z databáze cílové hierarchie.  

Po migraci dat a již nepotřebujete zdrojovou hierarchii pro správu zařízení ve vašem prostředí, můžete vyřadit z provozu zdrojovou hierarchii a infrastrukturu.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a>Řešení  

 Configuration Manager podporuje následující scénáře migrace:
- [Migrace z hierarchií nástroje Configuration Manager 2007](#bkmk_2007)  
- [Migrace z Configuration Manager 2012 nebo jiné hierarchie Configuration Manager](#bkmk_2012)

> [!NOTE]  
>  Rozšíření hierarchie, která má samostatnou lokalitu do hierarchie s lokalitou centrální správy, není zařazeno do kategorie migrace. Informace o rozšíření hierarchie naleznete v tématu [expand a samostatná primární lokalita](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a>Migrace z hierarchií Configuration Manager 2007  

 Když použijete migraci k migraci dat z Configuration Manager 2007, můžete udržet svou investici do stávající infrastruktury lokality a získat následující výhody:  

#### <a name="site-database-improvements"></a>Zdokonalení databáze lokality
Databáze Configuration Manager (Current Branch) podporuje úplné kódování Unicode.

#### <a name="database-replication-between-sites"></a>Replikace dat mezi lokalitami
Replikace v Configuration Manager (Current Branch) je založená na Microsoft SQL Server. Toto chování zvyšuje výkon přenosu dat mezi lokalitami.

#### <a name="user-centric-management"></a>Správa zaměřená na uživatele
Úlohy správy v Configuration Manager (aktuální větev) jsou zaměřeny na uživatele. Můžete například distribuovat software uživateli, i když neznáte název zařízení pro daného uživatele. Kromě toho Configuration Manager poskytuje uživatelům mnohem větší kontrolu nad tím, jaký software je nainstalovaný na svých zařízeních a kdy se tento software nainstaluje.

#### <a name="hierarchy-simplification"></a>Zjednodušení hierarchie
Configuration Manager (Current Branch) vám umožní vytvořit jednodušší hierarchii webu. Důvodem tohoto vylepšení je zavedení typu lokality centrální správy a změny v chování primárních a sekundárních lokalit. Configuration Manager (Current Branch) využívá menší šířku pásma sítě a vyžaduje menší počet serverů než předchozí verze.

#### <a name="role-based-administration"></a>Správa na základě rolí
Tento model centrálního zabezpečení v Configuration Manager (Current Branch) nabízí zabezpečení a správu na úrovni hierarchie, které odpovídají vašim požadavkům na správu a podnikání.

> [!NOTE]  
>  Z důvodu změn v návrhu, které byly poprvé představeny v System Center 2012 Configuration Manager, nemůžete upgradovat Configuration Manager 2007 na Configuration Manager (aktuální větev). Místní upgrade je podporovaný z Configuration Manager System Center 2012 na Configuration Manager (Current Branch).  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a>Migrace z Configuration Manager 2012 nebo jiné hierarchie Configuration Manager  
 Proces migrace dat z hierarchie nástroje System Center 2012 Configuration Manager nebo Configuration Manager je stejný. Tento proces zahrnuje migraci dat z více zdrojových hierarchií do jedné cílové hierarchie. Tento postup můžete použít, když vaše společnost získá další prostředky, které jsou již spravovány nástrojem Configuration Manager. Kromě toho můžete migrovat data z testovacího prostředí do produkčního prostředí Configuration Manager. Tento proces vám umožní udržovat investici do Configuration Manager testovacího prostředí.  



## <a name="see-also"></a>Viz také  

-   [Plánování migrace na Configuration Manager](planning-for-migration.md)  

-   [Konfigurace zdrojových hierarchií a zdrojových lokalit pro migraci](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operace migrace](operations-for-migration.md)  

-   [Zabezpečení a ochrana osobních údajů při migraci](security-and-privacy-for-migration.md)  

-   [Začínáme používat Configuration Manager](../servers/deploy/start-using.md)
