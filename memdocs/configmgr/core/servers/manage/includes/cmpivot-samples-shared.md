---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
ms.openlocfilehash: c450cff20df5dd45daa8097b8132f00d51bf713d
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226689"
---
<!--This file is shared by the CMPivot script samples articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->


## <a name="operating-system"></a>Operační systém

Načte informace o operačním systému.

```kusto
// Sample query for OS information
OperatingSystem
```

## <a name="recently-used-applications"></a>Nedávno použité aplikace

Následující dotaz se stane nedávno použitými aplikacemi (poslední 2 hodiny):

```kusto
CCMRecentlyUsedApplications
| where (LastUsedTime > ago(2h))
| project CompanyName, ProductName, ProductVersion, LastUsedTime
```

## <a name="device-start-times"></a>Časy spuštění zařízení

Následující dotaz ukazuje, kdy zařízení začala za posledních sedm dní:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
```

## <a name="free-disk-space"></a>Volné místo na disku

Následující dotaz ukazuje volné místo na disku:

```kusto
LogicalDisk
| project Device, DeviceID, Name, Description, FileSystem, Size, FreeSpace
| order by DeviceID asc
```

## <a name="device-information"></a>Informace o zařízení

Zobrazit zařízení, výrobce, model a OSVersion:

```kusto 
ComputerSystem
| project Device, Manufacturer, Model
| join (OperatingSystem | project Device, OSVersion=Caption)
```

## <a name="boot-times-for-a-device"></a>Časy spouštění pro zařízení

Zobrazit časy spouštění pro zařízení:

```kusto
SystemBootData
| project Device, SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
| order by SystemStartTime desc
```

## <a name="authentication-failures"></a>Selhání ověření

Vyhledejte v protokolech událostí chyby ověřování.

```kusto
EventLog('Security')
| where  EventID == 4673
```

## <a name="processmoduleprocessname"></a>ProcessModule ( \<processname> )  

Vytvoří výčet všech modulů (DLL) zavedených daným procesem. ProcessModule je užitečné při lovu malwaru, který se skrývá v legitimních procesech.  

```kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

## <a name="antimalware-software-status"></a>Stav antimalwarového softwaru

Načte stav antimalwarového softwaru nainstalovaného v počítači.

```kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
```

## <a name="find-bios-manufacturer-that-contains-any-word-like-micro"></a>Najít výrobce systému BIOS, který obsahuje nějaké slovo jako Micro

```kusto
Bios
// Find BIOS Manufacturer that contains any word like Micro, such as Microsoft
| where Manufacturer like '%Micro%'
```

## <a name="find-file-by-its-hash"></a>Najít soubor podle hodnoty hash

Vyhledá soubor pomocí algoritmu hash.

```kusto
Device
| join kind=leftouter ( File('%windir%\\system32\\*.exe')
| where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
| project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
```

## <a name="find-scripts-in-the-ccm-logs-in-the-last-hour"></a>Hledání skriptů v protokolech CCM za poslední hodinu

Následující dotaz se bude pohlížet na události za poslední 1 hodinu:

```kusto
CcmLog('Scripts',1h)
```

