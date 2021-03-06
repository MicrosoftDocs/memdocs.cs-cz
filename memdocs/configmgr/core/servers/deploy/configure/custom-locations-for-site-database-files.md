---
title: Umístění souborů vlastního souboru databáze
titleSuffix: Configuration Manager
description: Přečtěte si, jak zadat vlastní umístění souborů databáze SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8e4bf4eb11502d798ffa97500436494bc639aae
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607591"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Vlastní umístění pro soubory databáze lokality Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

 Configuration Manager podporuje pro soubory databáze SQL Server vlastní umístění.  

> [!NOTE]  
>  Možnost určení jiných než výchozích umístění souborů není dostupná, když používáte cluster SQL Server.  

 **Během instalace** nové primární lokality nebo lokality centrální správy můžete:  

-   **Zadejte jiné než výchozí umístění souborů pro databázi lokality**: Configuration Manager instalační program potom vytvoří databázi lokality pomocí těchto umístění.  

-   **Zadejte použití předem vytvořené databáze SQL Server, která používá vlastní umístění souborů**: Configuration Manager instalační program potom použije tuto předem vytvořenou databázi a její předem nakonfigurovaná umístění souborů.  

**Po dokončení instalace**můžete změnit umístění souborů databáze lokality. To vyžaduje, abyste zastavili lokalitu a upravili umístění souboru v SQL Server:  

-   Na Configuration Manager serveru lokality zastavte službu **SMS_Executive** .  

-   Další informace o tom, jak přesunout uživatelskou databázi, najdete v tématu [Přesun uživatelských databází](/sql/relational-databases/databases/move-user-databases).  

-   Po dokončení přesunutí souboru databáze restartujte službu **SMS_Executive** na serveru Configuration Manager lokality.