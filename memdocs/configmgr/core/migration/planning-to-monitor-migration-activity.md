---
title: Monitorování migrace
titleSuffix: Configuration Manager
description: Naučte se používat konzolu Configuration Manager ke sledování průběhu a úspěchu úloh migrace.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712999"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Plánování monitorování aktivity migrace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager můžete monitorovat migraci v konzole Configuration Manager, která se připojuje k cílové hierarchii. V konzole Configuration Manager v pracovním prostoru **Správa** můžete pomocí uzlu **migrace** monitorovat průběh a úspěšnost úloh migrace. Můžete zobrazit souhrnné informace o každé úloze migrace, které identifikují migrované objekty, objekty, které ještě nebyly migrovány, a počet objektů, které jsou vyloučeny z úlohy migrace. Zobrazí se také podrobnosti o problémech s migrací.  

## <a name="view-migration-progress"></a>Zobrazit průběh migrace  
 Chcete-li zobrazit průběh úlohy migrace, použijte některou z následujících akcí:  

-   V pracovním prostoru **Správa** konzoly Configuration Manager rozbalte uzel **úlohy migrace** , vyberte úlohu migrace a poté vyberte kartu **objekty v úloze** .  

-   Pomocí souborů protokolu Configuration Manager můžete zkontrolovat průběh migrace nebo identifikovat případné problémy. Správce migrace je Configuration Manager proces, který sleduje akce migrace a zaznamenává je do souboru souboru migmctrl. log ve složce ** \&lt; InstallationPath\>\\logs** na serveru lokality.  

    > [!NOTE]  
    >  Pokud se úloha migrace nezdařila, Projděte si podrobnosti v souboru souboru migmctrl. log co nejrychleji. Položky protokolu migrace se do souboru průběžně přidávají a přepisují staré podrobnosti. Pokud jsou položky přepsány, možná nebudete schopni zjistit, zda se problémy, které se mohou u migrovaných objektů setkat, vztahují k problémům s migrací. Aktivita migrace se protokoluje v lokalitě\-nejvyšší úrovně v hierarchii bez ohledu na lokalitu, ke které se konzola Configuration Manager připojuje při konfiguraci migrace.  

-   Použijte vytváření sestav Configuration Manager. Configuration Manager poskytuje několik integrovaných\-sestav pro migraci nebo tyto sestavy můžete upravit tak, aby vyhovovaly vašim požadavkům. Další informace o Configuration Managerch sestavách najdete v tématu [Úvod do vytváření sestav](../servers/manage/introduction-to-reporting.md).  
