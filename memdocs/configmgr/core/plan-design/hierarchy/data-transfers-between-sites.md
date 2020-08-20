---
title: Přenos dat mezi lokalitami
titleSuffix: Configuration Manager
description: Přečtěte si, jak Configuration Manager přesouvá data mezi lokalitami a jak můžete spravovat přenos dat napříč vaší sítí.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c3b74ceab892c67abbd56e8cb2a5c123374a92be
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663307"
---
# <a name="data-transfers-between-sites"></a>Přenos dat mezi lokalitami

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager používá k přenosu různých typů informací mezi lokalitami *replikaci na základě souborů* a *replikaci databáze* . Přečtěte si, jak Configuration Manager přesouvá data mezi lokalitami a jak můžete spravovat přenos dat napříč vaší sítí.  

## <a name="types-of-replication"></a>Typy replikace

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /></a> File-based replication

Configuration Manager používá replikaci na základě souborů k přenosu dat založených na souborech mezi lokalitami v hierarchii. Tato data zahrnují aplikace a balíčky, které chcete nasadit do distribučních bodů v podřízených lokalitách. Zpracovává také nezpracované záznamy dat zjišťování, které lokalita přenáší do své nadřazené lokality a následně zpracuje.  

Další informace najdete v tématu [replikace na základě souborů](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /></a> Database replication

Configuration Manager replikace databáze používá SQL Server k přenosu dat. Tuto metodu používá ke sloučení změn v databázi lokality s informacemi z databáze v jiných lokalitách v hierarchii.

Další informace najdete v tématu [replikace databáze](database-replication.md).

Nápovědu k řešení potíží s replikací SQL najdete v tématu [řešení potíží s REPLIKACÍ SQL](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Viz také:

[Monitorování replikace](../../servers/manage/monitor-replication.md)
