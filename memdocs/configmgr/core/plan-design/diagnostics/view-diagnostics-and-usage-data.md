---
title: Zobrazit diagnostická data
titleSuffix: Configuration Manager
description: Zobrazte diagnostická data a data o využití, abyste se ujistili, že vaše Configuration Manager hierarchie neobsahuje žádné citlivé informace.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a11b5779eca41ed25a8e53e555f91b596452e51b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128565"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Jak zobrazit data o využití a diagnostiku pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Data o diagnostice a využití můžete zobrazit z hierarchie Configuration Manager, abyste se ujistili, že nezahrnují žádné citlivé nebo identifikovatelné informace. Lokalita shrnuje a ukládá diagnostická data v tabulce **TEL_TelemetryResults** databáze lokality. Formátuje data, aby je bylo možné programově použít a efektivně.

Informace v tomto článku vám poskytnou přehled o konkrétních datech odesílaných společnosti Microsoft. Není určeno k použití pro jiné účely, jako je třeba analýza dat.  

## <a name="view-data-in-database"></a>Zobrazit data v databázi

Pomocí následujícího příkazu SQL můžete zobrazit obsah této tabulky a zobrazit přesná data, která jsou odeslána:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Export dat

Pokud je spojovací bod služby v režimu offline, pomocí nástroje pro připojení služby exportujte aktuální data do souboru hodnot oddělených čárkami (CSV). Spusťte nástroj pro připojení služby v spojovacím bodě služby s parametrem **-Export** .

Další informace najdete v tématu [použití nástroje pro připojení služby](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a>Jednosměrné hodnoty hash

Některá data se skládají z řetězců náhodných alfanumerických znaků. Configuration Manager používá algoritmus SHA-256 k vytvoření jednosměrných algoritmů hash. Tento proces zajistí, že společnost Microsoft neshromažďuje potenciálně citlivá data. Data s algoritmem hash je možné používat i pro účely korelace a porovnání.

Například místo shromažďování názvů tabulek v databázi lokality zachycuje jednosměrná hodnota hash pro každý název tabulky. Tím se zajistí, že všechny vlastní názvy tabulek nejsou viditelné. Microsoft pak provede stejný jednosměrný proces hash názvů výchozích tabulek SQL. Porovnání výsledků těchto dvou dotazů určuje odchylku schématu databáze od výchozího produktu. Tyto informace se pak použijí ke zlepšení aktualizací, které vyžadují změny schématu SQL.  

Při zobrazení nezpracovaných dat se v každém řádku dat zobrazí společná hodnota hash. Tato hodnota hash je ID hierarchie. Slouží ke korelaci dat se stejnou hierarchií bez identifikace zákazníka nebo zdroje.

### <a name="how-the-one-way-hash-works"></a>Jak funguje jednosměrná hodnota hash

1. Získejte ID vaší hierarchie spuštěním následujícího dotazu SQL ve službě SQL Management Studio proti databázi Configuration Manager:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Pomocí následujícího skriptu prostředí Windows PowerShell proveďte jednosměrnou hodnotu hash ID vaší hierarchie.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Porovnejte výstup skriptu s identifikátorem GUID v nezpracovaných datech. Tento proces ukazuje, jak jsou data zakryta.

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Úrovně diagnostických dat o využití](levels-overview.md)
