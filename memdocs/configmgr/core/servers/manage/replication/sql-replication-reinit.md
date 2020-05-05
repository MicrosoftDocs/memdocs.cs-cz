---
title: Reinit replikace SQL
titleSuffix: Configuration Manager
description: Pomocí tohoto diagramu můžete začít řešit potíže s opětovnou inicializací replikace SQL mezi Configuration Manager lokalitami.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078548"
---
# <a name="sql-replication-reinit"></a>Reinit replikace SQL

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pomocí následujícího diagramu můžete začít řešit potíže s opětovnou inicializací replikace SQL (znovu spustit):

![Diagram řešení potíží s reinicializací replikace SQL](media/sql-replication-reinit.svg)

## <a name="queries"></a>Dotazy

Tento diagram používá následující dotazy:

### <a name="check-if-site-is-in-maintenance-mode"></a>Zkontroluje, jestli je lokalita v režimu údržby.

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Ověřte, která replikační skupina nedokončila reinicializaci.

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Kontrolovat globální data

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Ověřit data lokality

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Další kroky

- [Opětovná inicializace globálních dat](global-data-reinit.md)
- [Opětovná inicializace dat webu](site-data-reinit.md)
- [Konfigurace SQL](sql-configuration.md)
