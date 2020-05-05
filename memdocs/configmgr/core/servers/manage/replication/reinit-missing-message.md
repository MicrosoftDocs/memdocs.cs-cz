---
title: Chybějící zpráva k opětovné inicializaci
titleSuffix: Configuration Manager
description: Pomocí tohoto diagramu můžete začít řešit potíže s chybějící zprávou s reinicializací replikace SQL v Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720461"
---
# <a name="reinit-missing-message"></a>Chybějící zpráva k opětovné inicializaci

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pomocí následujícího diagramu můžete začít řešit potíže s chybějící zprávou s opětovnou inicializací replikace SQL (znovu spustit):

![Diagram pro řešení potíží s chybějící zprávou o reinicializaci](media/reinit-missing-message.svg)

## <a name="queries"></a>Dotazy

Tento diagram používá následující dotazy:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Ověřte, jestli se replikace lokality nedokončila znovu.

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>Získat stav TrackingGuid & z webu odběratele

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>Získat stav TrackingGuid & z webu publikování

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Nápravné akce

### <a name="version-1902-and-later"></a>Verze 1902 a novější

K detekci problému a jeho inicializaci spusťte [analyzátor propojení replikace](../monitor-replication.md#BKMK_RLA).

### <a name="version-1810-and-earlier"></a>Verze 1810 a starší

Spusťte následující dotaz SQL a získejte `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Pak použijte `InitializeData` metodu třídy `SMS_ReplicationGroup` WMI s následujícími hodnotami:

- ReplicationGroupID: z dotazu SQL výše
- SiteCode1: nadřazený web
- SiteCode2: podřízená lokalita

Další informace naleznete v tématu [Metoda InitializeData ve třídě SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Příklad

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Další kroky

- [Opětovná inicializace replikace SQL](sql-replication-reinit.md)
