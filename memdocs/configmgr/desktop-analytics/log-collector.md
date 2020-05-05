---
title: Kolektor protokolů
titleSuffix: Configuration Manager
description: Řešení potíží s desktopovou analýzou pomocí nástroje kolektor protokolů
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718879"
---
# <a name="desktop-analytics-log-collector"></a>Kolektor protokolů Desktop Analytics

Od verze Configuration Manager 1906 použijte nástroj **DesktopAnalyticsLogsCollector. ps1** z instalačního adresáře Configuration Manager, abyste pomohli řešit problémy s registrací zařízení v Desktop Analytics. Spustí se základní kroky pro řešení potíží a shromáždí příslušné protokoly do jednoho pracovního adresáře. Tento obsah můžete sdílet s podporou Microsoftu.


## <a name="prerequisites"></a>Požadavky

- Klient nástroje Desktop Analytics se systémem Windows 10, Windows 8.1 nebo Windows 7 s aktualizací Service Pack 1

- Spusťte skript na zařízení jako administrativní uživatel a **Spusťte jako správce**.

    > [!Tip]
    > Pomocí tohoto nástroje můžete použít funkci **skriptů** Configuration Manager. Další informace najdete v tématu [Příklad 5: nasazení skriptu prostřednictvím Configuration Manager **skriptů**](#bkmk_ex5).

- Pro Windows 7 s aktualizací Service Pack 1, PowerShell verze 4,0 nebo novější
    - [Rozhraní .NET Framework verze 4,6 nebo novější](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [verze 4,0](https://support.microsoft.com/help/2819745) (aka.MS/wmf4download) nebo [verze 5,1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.MS/wmf5download)

## <a name="usage"></a>Využití

Získání skriptu z Configuration Manager obsahu instalace:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parametry

### `-LogPath`

Určuje místní cestu nebo cestu UNC pro vložení protokolu a dalších výstupních souborů.

**Hodnoty**:

- Místní cesta (maximální délka = 130), například:`c:\myfolder`

- Cesta UNC (maximální délka = 130), například:`\\myserver\myfolder`

**Typ**: řetězec

**Pozice**: 1

**Výchozí hodnota**: `$Env:SystemDrive\M365AnalyticsLogs` (Pokud má tento parametr hodnotu null, prázdné nebo prázdné místo, skript vytvoří složku M365AnalyticsLogs pod systémovou jednotkou.)

### `-LogMode`

Určuje úroveň podrobností protokolů.

**Hodnoty**:

- `0`: Protokolovat zprávy skriptu do příkazového okna PowerShellu.

- `1`: Protokoluje zprávy skriptu do obou souborů protokolu v rámci výstupní složky a příkazového okna PowerShellu.

- `2`: Protokoluje zprávy skriptu do souboru protokolu pouze v rámci výstupní složky.

**Typ**: Int16

**Pozice**: 2

**Výchozí hodnota**: `1` (Protokolovat zprávy skriptu do souboru protokolu a příkazového okna prostředí PowerShell.)

### `-CollectNetTrace`

Určuje, zda skript shromažďuje síťové trasování.

**Hodnoty**:

- `0`: Nepovolujte trasování sítě.

- `1`(jakákoli nenulová celočíselná hodnota): Povolte trasování sítě a Shromážděte výsledky.

**Typ**: Int16

**Pozice**: 3

**Výchozí hodnota**: `0` (Nepovolit trasování sítě)

### `-CollectUTCTrace`

Určuje, jestli skript shromažďuje trasování UTC v systému Windows a spouští diagnostiku připojení.

**Hodnoty**:

- `0`: Nepovolujte trasování UTC nebo spusťte diagnostiku připojení.

- `1`(jakákoli nenulová celočíselná hodnota): povolí trasování UTC, spustí diagnostiku připojení a shromáždí výsledky.

**Typ**: Int16

**Pozice**: 4

**Výchozí hodnota**: `0` (Nepovolit trasování UTC nebo spustit diagnostiku připojení)


## <a name="output"></a>Výstup

Skript vytvoří *pracovní složku* v zadané cestě. Například **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Všechny své výstupní soubory vloží do této pracovní složky.

Pokud povolíte skriptu zápis do *souboru protokolu*, vygeneruje se ten v pracovní složce. Například **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss. txt**.

Skript také generuje další *diagnostické soubory* v pracovní složce. Příklad:

- `installedKBs.txt`: seznam aktualizací Windows nainstalovaných na zařízení
- `appcompat`: data kompatibility aplikací
- `Reg*.txt`: řada souborů s exportovanými daty z registru systému Windows


## <a name="examples"></a>Příklady

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a>Příklad 1: spuštění skriptu přes příkazové okno PowerShellu s výchozími hodnotami

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a>Příklad 2: spuštění skriptu pomocí příkazového okna PowerShellu se zadanými parametry

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a>Příklad 3: spuštění skriptu prostřednictvím příkazového okna PowerShellu se zadanými parametry na pozici

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a>Příklad 4: spuštění skriptu pomocí příkazového okna PowerShellu se zadaným parametrem a podrobnými zprávami

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a>Příklad 5: nasazení skriptu pomocí Configuration Manager **skriptů**

Další informace najdete v tématu [Vytvoření a spuštění skriptů PowerShellu z konzoly Configuration Manager](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector. ps1 je digitálně podepsán společností Microsoft. Je možné, že budete muset přidat svůj certifikát Microsoftu pro podpis kódu jako důvěryhodného vydavatele na cílovém zařízení.

1. Otevřete vlastnosti skriptu v Průzkumníkovi Windows. Přepněte na kartu **digitální podpisy** a vyberte **Podrobnosti**.

2. Na kartě **Obecné** vyberte **Zobrazit certifikát**.

    > [!Note]
    > K distribuci certifikátu přes jiné mechanismy nejdřív exportujte certifikát do souboru. Přejít na kartu **Podrobnosti** a vyberte **Kopírovat do souboru**.

3. Vyberte **nainstalovat certifikát**. Importujte certifikát a umístěte ho do úložiště **důvěryhodných vydavatelů** .


## <a name="see-also"></a>Viz také

- [Řešení potíží s Desktop Analytics](troubleshooting.md)

- [Vytvoření a spuštění PowerShellových skriptů z konzoly Configuration Manager](../apps/deploy-use/create-deploy-scripts.md)
