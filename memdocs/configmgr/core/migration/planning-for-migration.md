---
title: Plánování migrace
titleSuffix: Configuration Manager
description: Přečtěte si o lokalitách a hierarchiích předtím, než migrujete data do cílové hierarchie Configuration Manager aktuální větve.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719656"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Plánování migrace na Configuration Manager aktuální větev

*Platí pro: Configuration Manager (Current Branch)*

Před migrací dat do cílové hierarchie Configuration Manager aktuální větve se ujistěte, že máte zkušenosti s lokalitami a hierarchiemi v Configuration Manager. Další informace o lokalitách a hierarchiích najdete v tématu [základy Configuration Manager](../../core/understand/fundamentals.md).  

Než migrujete data z podporované zdrojové hierarchie, nainstalujte Configuration Manager aktuální hierarchie větví do cílové hierarchie.  

Po instalaci cílové hierarchie nastavte funkce a funkce správy, které chcete použít v cílové hierarchii, než začnete migrovat data.  

Kromě toho může být nutné naplánovat překrytí mezi zdrojovou hierarchií a cílovou hierarchií. Můžete například nastavit zdrojovou hierarchii tak, aby používala stejné síťové umístění nebo hranice jako cílová hierarchie, a pak nainstalujete nové klienty do cílové hierarchie a použijete automatické přiřazení lokality. Vzhledem k tomu, že nově nainstalovaný Configuration Manager klient může v tomto scénáři vybrat lokalitu, která se má připojit z jedné hierarchie, může se stát, že se klient nesprávně přiřadí ke zdrojové hierarchii. Proto Naplánujte přiřazení každého nového klienta v cílové hierarchii ke konkrétní lokalitě v této hierarchii namísto použití automatického přiřazení lokality.  

Další informace o přiřazeních lokality najdete v tématu věnovaném [hlediskům přiřazování lokalit klienta](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) při [vzájemné spolupráci mezi různými verzemi Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Následující články vám pomůžou naplánovat migraci podporované zdrojové hierarchie do cílové hierarchie Configuration Manager:

-   [Požadavky pro migraci](../../core/migration/prerequisites-for-migration.md)  

-   [Kontrolní seznamy správce pro plánování migrace](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Určení, zda se mají migrovat data do Configuration Manager aktuální větve](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Plánování strategie zdrojové hierarchie](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Kontrolní seznamy správce pro plánování migrace](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Plánování strategie migrace klientů](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Plánování strategie migrace nasazení obsahu](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Plánování migrace Configuration Managerch objektů do Configuration Manager aktuální větev](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Plánování monitorování migrační aktivity](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Plánování dokončení migrace](../../core/migration/planning-to-complete-migration.md)  
