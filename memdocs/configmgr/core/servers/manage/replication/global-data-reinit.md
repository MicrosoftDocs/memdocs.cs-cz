---
title: Opětovná inicializace globálních dat
titleSuffix: Configuration Manager
description: Pomocí tohoto diagramu můžete začít řešit potíže s reinicializací replikace SQL pro globální data v hierarchii Configuration Manager.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713629"
---
# <a name="troubleshoot-global-data-reinit"></a>Řešení potíží s globálním inicializací dat

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pomocí následujícího diagramu můžete začít řešit potíže s opětovnou inicializací replikace SQL (reinit) pro globální data v Configuration Manager hierarchii:

![Diagram řešení potíží s globálním reinicializací dat](media/global-data-reinit.svg)

## <a name="queries"></a>Dotazy

Tento diagram používá následující dotazy:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Ověřte, jestli se replikace lokality nedokončila znovu.

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Získat stav TrackingGuid & z primární lokality

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Získat stav TrackingGuid & z CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Zkontroluje stav žádosti pro ID sledování.

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Další kroky

- [Chybějící zpráva k opětovné inicializaci](reinit-missing-message.md)
