---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716170"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a>Sestavy inventáře hardwaru

<!--5468413-->
Pokud se pokusíte spustit sestavu, která spoléhá na inventář hardwaru, vrátí chybu. Například zpráva nástroje BitLocker vrátí chybu podobnou této zprávě:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

V souboru **Dataldr. log** se může zobrazit také následující chyba:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Může to mít vliv i na řídicí panely konzoly, které spoléhají na inventář hardwaru.

Příčinou tohoto problému je změna schématu databáze pro konkrétní tabulky inventáře hardwaru.

#### <a name="workaround"></a>Alternativní řešení

Alternativním řešením je vyřadit z databáze již existující atribut. Součást webu dataloader pak může vytvořit nový atribut. Spusťte následující skript SQL na serveru databáze lokality, abyste opravili schéma tabulky:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
