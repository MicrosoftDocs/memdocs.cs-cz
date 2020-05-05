---
title: Konfigurace SQL
titleSuffix: Configuration Manager
description: Pomocí tohoto diagramu můžete začít řešit potíže s konfigurací SQL pro Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723226"
---
# <a name="sql-configuration"></a>Konfigurace SQL

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pomocí následujícího diagramu můžete začít řešit potíže s konfigurací SQL souvisejících se službou SQL Service Broker:

![Diagram řešení potíží s konfigurací SQL](media/sql-configuration.svg)

## <a name="queries"></a>Dotazy

Tento diagram obsahuje následující dotazy a akce:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Zkontroluje, jestli SQL může doručovat zprávy SSB.

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Nápravné akce

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Náprava problémů hlášených z transmission_status

Běžné problémy:

- Konfigurace brány firewall
- Konfigurace sítě
- Nesprávně nakonfigurované certifikáty SSB

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Spuštění profileru SQL pro trasování událostí SSB

Spusťte profiler SQL v databázi certifikačních autorit a primární lokality a sledujte události týkající se Service Broker SQL:

- **Auditovat přihlášení zprostředkovatele**
- **Konverzace zprostředkovatele auditu**
- Události v kategorii **zprostředkovatele**
