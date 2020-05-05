---
title: Spuštění nástroje pro souhrn měřiče
titleSuffix: Configuration Manager
description: Pomocí nástroje pro Shrnutí měřiče spuštění můžete aktivovat úkoly sumarizace měření softwaru v Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723170"
---
# <a name="run-meter-summarization-tool"></a>Spuštění nástroje pro souhrn měřiče

*Platí pro: Configuration Manager (Current Branch)*

Nástroj pro Shrnutí měřičů spuštění je jedním z [Configuration Manager nástrojů](tools.md). Použijte ji k okamžitému spuštění úloh údržby pro Shrnutí monitorování míry využívání softwaru v primárních lokalitách. Ve výchozím nastavení se tyto úlohy spouštějí jako naplánované v úlohách **údržby lokality** , které začínají po 12:00 ráno každý den. 

Tyto úlohy shrnují data v tabulce SQL **MeterData** a zapisují souhrnné výsledky do tabulek **FileUsageSummary** a **MonthlyUsageSummary** . Pak se zobrazí souhrnný výsledek sestav měření softwaru. Každý Configuration Manager administrativní uživatel, který se může připojit k databázi primární lokality, může tento nástroj použít ke spuštění Shrnutí. 

Tento nástroj spustí souhrnný úkol Shrnutí **využití souborů** a **měsíční Souhrn využití** dat měření softwaru. Shrnuje všechna existující data měřičů bez běžné 12 hodin čekací doby. Spusťte ji na SQL serveru, který je hostitelem databáze lokality. Je-li Shrnutí úspěšné, je ukončovací kód nastaven na `0`. Pokud došlo k chybě, kód ukončení je `1`.



## <a name="usage"></a>Využití

### <a name="command-line"></a>Příkazový řádek

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Možnosti

#### <a name="database-name"></a>Název databáze
Název databáze lokality na serveru SQL Server.

#### <a name="delay-in-hours-for-summarization"></a>Zpoždění v hodinách pro Shrnutí
Nástroj shrnuje využití měření softwaru vygenerované před zpožděním. Ve výchozím nastavení je tato prodleva nula.


### <a name="example"></a>Příklad

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Shrnutí využití softwarového měření vygenerovaného před 12 hodinami

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Viz také

- [Úlohy údržby](../servers/manage/maintenance-tasks.md)
- [Sledování využití aplikací pomocí monitorování míry využívání softwaru](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
