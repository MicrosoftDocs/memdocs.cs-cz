---
title: Protokoly událostí nástroje BitLocker
titleSuffix: Configuration Manager
description: Informace o tom, jak pracovat s nástrojem BitLocker v protokolu událostí systému Windows k řešení problémů
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722099"
---
# <a name="bitlocker-event-logs"></a>Protokoly událostí nástroje BitLocker

*Platí pro: Configuration Manager (Current Branch)*

Agent správy BitLockeru a webové služby používají protokoly událostí systému Windows k zaznamenávání zpráv. V Prohlížeč událostí přejdete do části **protokoly aplikací a služeb**, **Microsoft**, **Windows**. Kanál protokolu (uzel) se liší v závislosti na počítači a součásti:

- **MBAM**: Agent pro správu BitLockeru na klientském počítači
- **MBAM-web**:
  - Služba obnovení v bodu správy
  - Samoobslužný portál
  - Web pro správu a monitorování

Další informace o konkrétních zprávách v těchto protokolech najdete v následujících článcích:

- [Protokoly klientských událostí](client-event-logs.md)
- [Protokoly serverových událostí](server-event-logs.md)

V každém uzlu se ve výchozím nastavení zobrazí dva kanály protokolu: **správce** a **funkční**. Podrobnější informace o řešení potíží můžete zobrazit také v [protokolech analýzy a ladění](#bkmk_debug).

## <a name="log-properties"></a>Vlastnosti protokolu

Ve Windows Prohlížeč událostí vyberte konkrétní protokol. Například **admin**. Přejděte do nabídky **Akce** a vyberte **vlastnosti**. Nakonfigurujte tahle nastavení:

- **Maximální velikost protokolu (KB)**: ve výchozím nastavení je `1028` toto nastavení (1 MB) pro všechny protokoly.
- **Pokud je dosaženo maximální velikosti protokolu událostí**: ve výchozím nastavení se protokoly pro **správu** a **provoz** nastaví na hodnotu **Přepsat události podle potřeby (nejstarší události jako první)**.

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a>Protokoly o analýze a ladění

Pro účely řešení potíží můžete povolit podrobnější protokoly. V Prohlížeč událostí přejděte do nabídky **zobrazení** a vyberte možnost **Zobrazit protokoly pro ladění a analýzu**. Když teď přejdete na kanál protokolu, zobrazí se dva další protokoly: **analytické** a **ladicí**.

> [!TIP]
> Ve výchozím nastavení mají tyto protokoly následující vlastnosti:
>
> - **Maximální velikost protokolu (KB)**: `1028` (1 MB)
> - **Nepřepisovat události (Ruční vymazání protokolů)**

## <a name="export-logs-to-text"></a>Exportovat protokoly do textu

Zvláště u [protokolů pro analýzu a ladění](#bkmk_debug)může být snazší zkontrolovat položky protokolů v jednom textovém souboru. K exportu položek protokolu událostí do textových souborů použijte následující příkazy PowerShellu:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
