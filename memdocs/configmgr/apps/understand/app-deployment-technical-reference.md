---
title: Řešení potíží s technickými referencemi k nasazení aplikace
titleSuffix: Configuration Manager
description: Technické informace o řešení potíží s nasazením aplikací v Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709814"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Technické informace o nasazení aplikace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto článku se dozvíte, jak funguje nasazení aplikace.

## <a name="before-you-begin"></a>Než začnete

Při řešení potíží s nasazením aplikací existuje několik položek, které mohou být užitečné při kontrole protokolů klienta. Mezi tyto položky patří:

- ID položky konfigurace aplikace
- Jedinečné ID aplikace
- Jedinečné ID typu nasazení
- Jedinečné ID nasazení aplikace (označuje se také jako jedinečné ID přiřazení)
- Účel nasazení aplikace
- Jedinečné ID obsahu
- ID a název kolekce
- Typ kolekce

Chcete-li zjednodušit řešení potíží, můžete spustit dotaz SQL podobný tomuto: v databázi Configuration Manager, abyste získali výše uvedené informace.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Při spuštění tohoto dotazu je **nutné** použít název aplikace uvedený na kartě Obecné informace v části vlastnosti aplikace namísto použití lokalizovaného názvu aplikace, který je uveden v části vlastnosti aplikace na kartě Centrum softwaru.

## <a name="next-steps"></a>Další kroky

- [Zásada nasazení aplikace](deployment-policy-technical-reference.md)
