---
title: Replikace SQL
titleSuffix: Configuration Manager
description: Pomocí tohoto diagramu můžete začít řešit potíže s replikací SQL mezi Configuration Manager lokalitami.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717521"
---
# <a name="sql-replication"></a>Replikace SQL

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pomocí následujícího diagramu můžete začít řešit potíže s replikací SQL, když se odkaz nezdařil:

![Diagram řešení potíží s replikací SQL](media/sql-replication.svg)

## <a name="queries"></a>Dotazy

Tento diagram používá následující dotazy:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Ověřte, jestli je odkaz replikační skupiny v neomezeném stavu nebo se nezdařil.

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Zjistit, jestli se nedávno vypočítal odkaz na replikační skupinu

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>Kontrolovat režim údržby SQL

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Další kroky

- [Opětovná inicializace replikace SQL](sql-replication-reinit.md)
- [Výkon SQL](sql-performance.md)
- [Konfigurace SQL](sql-configuration.md)
