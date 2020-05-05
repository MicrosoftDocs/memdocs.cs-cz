---
title: Mezinárodní podpora
titleSuffix: Configuration Manager
description: Nakonfigurujte Configuration Manager tak, aby splňovaly konkrétní mezinárodní požadavky.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720937"
---
# <a name="international-support-in-configuration-manager"></a>Mezinárodní podpora v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Následující části obsahují technické informace, které vám pomůžou zajistit Configuration Manager kompatibilní s konkrétními mezinárodními požadavky.  

## <a name="gb18030-requirements"></a>Požadavky normy GB18030  
 Configuration Manager splňuje standardy definované v GB18030, aby bylo možné používat Configuration Manager v Číně. Nasazení Configuration Manager musí mít následující konfigurace, aby splňovala požadavky GB18030:  

-   Každý počítač serveru lokality a SQL Server počítač, který používáte s Configuration Manager, musí používat čínský operační systém.  

-   Všechny databáze lokalit a všechny instance systému SQL Server v hierarchii musí používat stejnou kolaci, a to jednu z následujících:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Tyto kolace databáze představují výjimku z požadavků uvedených v části [podpora SQL serverch verzí pro Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Do kořenové složky systémového svazku každého počítače serveru lokality v hierarchii musíte umístit soubor s názvem **GB18030.SMS** . Tento soubor neobsahuje žádná data, může jít o prázdný textový soubor s názvem odpovídajícím tomuto požadavku.  
