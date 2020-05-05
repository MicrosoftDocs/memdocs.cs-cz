---
title: Opětovná inicializace dat webu
titleSuffix: Configuration Manager
description: Pomocí tohoto diagramu můžete začít řešit potíže s reinicializací replikace SQL pro data lokality v hierarchii Configuration Manager.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078582"
---
# <a name="troubleshoot-site-data-reinit"></a>Řešení potíží s opakovaným inicializací dat lokality

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pomocí následujícího diagramu můžete začít řešit potíže s opětovnou inicializací replikace SQL (znovu spustit) pro data lokality ve Configuration Manager hierarchii:

![Diagram řešení potíží s reinicializací dat lokality](media/site-data-reinit.svg)

## <a name="queries"></a>Dotazy

Tento diagram používá následující dotazy:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Ověřte, jestli se replikace lokality nedokončila znovu.

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Získat stav TrackingGuid & z CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Získat stav TrackingGuid & z primární lokality

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Ověřte, že primární lokalita není v režimu údržby.

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Zkontroluje stav žádosti pro ID sledování.

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Další kroky

- [Chybějící zpráva k opětovné inicializaci](reinit-missing-message.md)
- [Opětovná inicializace globálních dat](global-data-reinit.md)
