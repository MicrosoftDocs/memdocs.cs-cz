---
title: Shromažďování diagnostických dat
titleSuffix: Configuration Manager
description: Přečtěte si, jak Configuration Manager shromažďuje data o využití a diagnostiku.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709534"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Jak Configuration Manager shromažďuje data o využití a diagnostiku

*Platí pro: Configuration Manager (Current Branch)*

Aby bylo možné shromažďovat data o využití a diagnostiku pro Configuration Manager, každá primární lokalita používá každý týden SQL Server dotazů. V hierarchii více lokalit se data replikují do lokality centrální správy.  

V lokalitě nejvyšší úrovně hierarchie spojovací bod služby odesílá tyto informace při kontrole aktualizací. Režim spojovacího bodu služby určuje způsob přenosu dat:

- **Online**: po týdnu spojovací bod služby automaticky odesílá data o diagnostice a využití do cloudové služby.

- **Offline**: pomocí [Nástroje pro připojení služby](../../servers/manage/use-the-service-connection-tool.md)ručně přeneste data o využití a diagnostiku.

Další informace najdete v tématu [o spojovacím bodu služby](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Jak zobrazit data o využití a diagnostiku](view-diagnostics-and-usage-data.md)
