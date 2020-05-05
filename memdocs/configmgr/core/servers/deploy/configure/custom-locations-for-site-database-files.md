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
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721007"
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

-   Pomocí dokumentace pro vaši verzi SQL Server se naučíte, jak přesunout uživatelskou databázi. Pokud například používáte SQL Server 2014, přečtěte si téma [přesunutí uživatelských databází](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) na webu TechNet.  

-   Po dokončení přesunutí souboru databáze restartujte službu **SMS_Executive** na serveru Configuration Manager lokality.  
