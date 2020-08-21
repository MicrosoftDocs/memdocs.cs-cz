---
title: Požadavky vytváření sestav
titleSuffix: Configuration Manager
description: Pochopení různých závislostí, které mají vliv na používání sestav v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b082ae578052a92c0afacd3d1f62fdb2e21bd6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699530"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Předpoklady pro vytváření sestav v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vytváření sestav v Configuration Manager má následující závislosti:

- SQL Server Reporting Services
- Bod služby Reporting services
- Server sestav Power BI (volitelné, počínaje verzí 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Než budete moct použít vytváření sestav v Configuration Manager, nainstalujte a nakonfigurujte SQL Server Reporting Services.

Další informace o plánování a nasazení služeb generování sestav najdete v tématu [Install SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services).

Nainstalujte databázi služby Reporting Services buď na výchozí instanci, nebo na pojmenovanou instanci instalace 64 SQL Server. Společně vyhledejte instanci SQL Server se serverem systému lokality nebo ji nakonfigurujte na vzdáleném počítači.

Configuration Manager podporuje stejné verze SQL Server pro vytváření sestav, protože jsou pro databázi lokality. Další informace najdete v tématu [podporované verze SQL Server](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Bod služby Reporting services

Než budete moci použít vytváření sestav v nástroji Configuration Manager, nakonfigurujte roli systému lokality bodu služby Reporting Services.

Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Server sestav Power BI

Počínaje verzí 2002 můžete integrovat vytváření sestav pomocí Server sestav Power BI. Další informace, včetně požadavků, najdete v tématu věnovaném [integraci s server sestav Power BI](powerbi-report-server.md).

## <a name="next-steps"></a>Další kroky

[Konfigurace vytváření sestav](configuring-reporting.md)