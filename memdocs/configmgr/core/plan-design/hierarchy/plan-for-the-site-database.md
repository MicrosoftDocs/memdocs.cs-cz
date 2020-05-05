---
title: Plánování databáze lokality
titleSuffix: Configuration Manager
description: Při plánování Configuration Manager hierarchie Vezměte v úvahu databázi lokality a roli serveru databáze lokality.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a32f0a59a0b3ce3ad864fecf61fe7281b8ebbdd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720811"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>Plánování databáze lokality pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Server databáze lokality je počítač, na kterém běží podporovaná verze Microsoft SQL Server. SQL Server slouží k ukládání informací pro Configuration Manager weby. Každá lokalita v hierarchii Configuration Manager obsahuje databázi lokality a server, kterému je přiřazena role serveru databáze lokality.  

-   U lokalit centrální správy a primárních lokalit můžete nainstalovat SQL Server na server lokality, nebo můžete SQL Server nainstalovat na jiný počítač než server lokality.  

-   U sekundárních lokalit můžete místo úplné SQL Server instalace použít SQL Server Express. Databázový server je však třeba spustit na serveru sekundární lokality.  

-  Pro použití skupiny dostupnosti SQL musí být model obnovení databáze nastaven na hodnotu FULL.  

-  Pro použití skupiny dostupnosti bez SQL musí být model obnovení databáze nastaven na hodnotu jednoduché.  

Další informace o režimech obnovení SQL najdete v [modelech obnovení (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

K hostování databáze lokality můžou být použité následující konfigurace SQL Serveru:  

-   Výchozí instance SQL Serveru  

-   Pojmenovaná instance na jednom počítači se spuštěným SQL Serverem  

-   Pojmenovaná instance na clusterové instanci SQL Serveru  

-   Skupina dostupnosti SQL Server AlwaysOn (od verze 1602 Configuration Manager)


Aby bylo možné hostovat databázi lokality, SQL Server musí splňovat požadavky popsané v části [podpora verzí SQL Server pro Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Informace o umístění vzdáleného databázového serveru  

Pokud používáte počítač se vzdáleným databázovým serverem, ujistěte se, že použité síťové připojení je vysoce dostupné síťové připojení s vysokou šířkou pásma. Server lokality a některé role systému lokality musí nepřetržitě komunikovat se vzdáleným serverem, který je hostitelem databáze lokality.

-   Šířka pásma potřebná pro komunikaci s databázovým serverem závisí na kombinaci mnoha různých konfigurací lokality a klienta. Proto se skutečná požadovaná šířka pásma nedá vhodně odhadnout.  

-   Každý počítač, který používá poskytovatele SMS a který se připojuje k databázi lokality, zvyšuje požadavky na šířku pásma sítě.  

-   Počítač, ve kterém je spuštěný SQL Server, musí být umístěný v doméně, která má oboustranný vztah důvěryhodnosti se serverem lokality a všemi počítači, které používají poskytovatele služby SMS.  

-   Klastrovaný SQL Server nemůžete používat pro databázový server lokality, pokud se databáze lokality nachází na stejném místě jako server lokality.  


Server systému lokality obvykle podporuje role systému lokality pouze z jedné Configuration Manager lokality. K hostování databáze z různých Configuration Manager lokalit ale můžete použít různé instance SQL Server, na clusterovaných nebo neclusterovaných serverech, které používají SQL Server. K podpoře databází z různých lokalit musíte nakonfigurovat jednotlivé instance SQL Serveru tak, aby ke komunikaci používaly odlišné porty.  
