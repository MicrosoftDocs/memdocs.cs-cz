---
title: Zastaralé pro servery lokality
titleSuffix: Configuration Manager
description: Seznamte se s produkty a operačními systémy, které Configuration Manager již nejsou podporovány pro servery lokality.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719474"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Odebrané a zastaralé pro Configuration Manager servery lokality

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje produkty a operační systémy, které se odebraly z podpory pro Configuration Manager servery lokality, nebo se v budoucí aktualizaci odeberou (zastaralé). Poskytuje úvodní oznámení o budoucích změnách, které můžou ovlivnit použití Configuration Manager.  

Tyto informace se mohou v budoucnu změnit. Nemusí zahrnovat všechny zastaralé funkce, produkty nebo operační systémy.  

## <a name="server-os"></a>Operační systém serveru  

|Operační systémy|Zastarání poprvé oznámeno|Podpora odebrána|
|-|-|-|
|Windows Server 2008 R2 s aktualizací SP1|10. července 2015| Verze 1702|
|Windows Server 2008 s aktualizací SP2|10. července 2015|Verze 1511|

## <a name="sql-server"></a>SQL Server

|Verze SQL Serveru|Zastarání poprvé oznámeno|Podpora odebrána|
|-|-|-|
|SQL Server 2008 R2|10. července 2015|Verze 1702|
|SQL Server 2008|10. července 2015|Verze 1511|

Pokud potřebujete upgradovat svou verzi SQL Server, doporučujeme od snadno složitějších následujících metod:

1. [Upgradovat SQL Server místně](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (doporučeno)  

2. Nainstalujte novou verzi SQL Server do nového počítače. Pak pokud chcete server lokality Ukázat na novém SQL Server, [použijte možnost přesunutí databáze](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) Configuration Manager nastavení.  

3. Použijte [zálohování a obnovení](../../../servers/manage/backup-and-recovery.md).  

## <a name="next-steps"></a>Další kroky

Další informace najdete v těchto článcích:

- [Odebrané a zastaralé](removed-and-deprecated.md)  

- [Životní cyklus podpora Microsoftu](https://support.microsoft.com/lifecycle)  

- [Podpora pro aktuální verze větví Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)  
