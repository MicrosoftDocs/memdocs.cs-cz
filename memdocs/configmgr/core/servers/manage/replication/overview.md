---
title: Řešení potíží s replikací SQL
titleSuffix: Configuration Manager
description: Tyto diagramy vám pomůžou pochopit a řešit potíže s replikací SQL mezi Configuration Manager lokalitami.
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720468"
---
# <a name="troubleshoot-sql-replication"></a>Řešení potíží s replikací SQL

V hierarchii s více lokalitami používá Configuration Manager k přenosu dat mezi lokalitami replikaci SQL. Další informace najdete v tématu [replikace databáze](../../../plan-design/hierarchy/database-replication.md).

Pro lepší pochopení a usnadnění řešení potíží s replikací SQL použijte tyto diagramy.

- [Replikace SQL](sql-replication.md)
- [Konfigurace SQL](sql-configuration.md)
- [Výkon SQL](sql-performance.md)
- [Opětovná inicializace replikace SQL](sql-replication-reinit.md)
- [Opětovná inicializace globálních dat](global-data-reinit.md)
- [Opětovná inicializace dat webu](site-data-reinit.md)
- [Chybějící zpráva k opětovné inicializaci](reinit-missing-message.md)

Tyto diagramy řešení potíží jsou propojeny. Pro pochopení jejich vztahů použijte následující diagram:

![Diagram s přehledem procesu pro řešení potíží s replikací SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Další informace najdete v následujících řadách blogů z podpora Microsoftu:

- [Interní DRS synchronizace nástroje ConfigMgr](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [Služba DRS (data Replication Service) nástroje ConfigMgr 2012 nebyla zablokována.](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – Nejčastější dotazy týkající se řešení potíží](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [Interní DRS inicializace nástroje ConfigMgr 2012](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: problémy s certifikátem služby DRS a SQL Service Broker](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
