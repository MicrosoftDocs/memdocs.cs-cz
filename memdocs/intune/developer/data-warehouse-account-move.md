---
title: Přesunutí vašich dat účtu datového skladu Intune
titleSuffix: Microsoft Intune
description: Vysvětlení, jak při přesouvání účtu zálohovat data v datovém skladu Intune
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ee3ccbf9-82fc-4fbf-9d3d-8f05e431d090
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 95c7104f949216a6a9f7704ac9bec6a7c2dfa7aa
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078086"
---
# <a name="move-your-intune-data-warehouse-account-data"></a>Přesunutí vašich dat účtu datového skladu Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Když požádáte o přesunutí účtu, považuje se to současně za žádost o změnu umístění vašeho datového centra. Po přesunutí dat se datový sklad resetuje a od stanoveného dne zahájení přesunutí bude data zaznamenávat v novém umístění. Pokud chcete zálohovat data z předchozího datového skladu, proveďte ještě **před** přesunutím účtu následující kroky. Většina tabulek datových skladů uchovává data 30 dní. Jakmile tedy uplyne 30 dní od přesunutí účtu, žádný prostor pro data v těchto tabulkách už nebude k dispozici. Další informace o dobách uchování pro zadané tabulky najdete v článku [Datový model datového skladu](reports-ref-data-model.md). 

## <a name="back-up-your-data-warehouse-data"></a>Zálohování dat datového skladu 

Pokud chcete zálohovat data datového skladu, musíte je uložit jako soubor *.csv* pomocí rozhraní API datového skladu:  

1. Pokud jste s rozhraním API datového skladu ještě nikdy nepracovali, postupujte podle jednorázového procesu uvedeného v článku [Získání dat z rozhraní API datového skladu Intune pomocí klienta REST](reports-proc-data-rest.md).
2. Pomocí ukázky PowerShellu s názvem [Přístup k datovému skladu Intune pomocí PowerShellu](https://github.com/Microsoft/Intune-Data-Warehouse/tree/master/Samples/PowerShell) stáhněte všechna data do souborů CSV. 

## <a name="back-up-your-trend-charts-from-the-azure-portal"></a>Záloha grafů trendů z portálu Azure Portal

Některé grafy trendů ve vašem zobrazení portálu Azure Portal se resetují. Spuštěním následujícího skriptu v části **Graf** můžete tyto grafy zálohovat:   

### <a name="terms--conditions-acceptance-reports"></a>Sestavy přijetí podmínek a ujednání
1. V Azure Portal přejděte na **Microsoft Intune** -> podmínky**registrace** -> zařízení **& podmínky**.
2. Pro každou položku **podmínek a ujednání** zvolte **Generování sestav o přijetí** a potom **Exportovat**.
3. Uložte si sestavu místně.
 
### <a name="app-protection-reports"></a>Sestavy o ochraně aplikace  
1. V Azure Portal přejděte na **Microsoft Intune** -> **klientské aplikace** -> **stav ochrany aplikace**.
2. Klikněte na ikonu stažení (⤓) pro sestavy, které si chcete uložit.

### <a name="device-configuration-charts"></a>Grafy konfigurace zařízení 
1. V Azure Portal přejděte na **Microsoft Intune** -> **DeviceConfiguration**.
2. Pomocí [Graph exploreru](https://developer.microsoft.com/graph/graph-explorer) stáhněte podkladová data grafů. 
    - Stav nasazení u všech konfiguračních profilů zařízení pro všechna zařízení viz [Stav nasazení zařízení](https://graph.microsoft.com/beta/reports/deviceConfigurationDeviceActivity/content).

    - Stav nasazení u všech konfiguračních profilů zařízení pro všechny uživatele viz [Stav nasazení uživatelů](https://graph.microsoft.com/beta/reports/deviceConfigurationUserActivity/content).

    - Stav nasazení profilu viz [Stav poskytnutí nasazení](https://graph.microsoft.com/beta/deviceManagement/deviceConfigurations?$select=id,displayName,lastModifiedDateTime,deviceStatusOverview&$expand=deviceStatusOverview).
  
    > [!NOTE]
    > Pro přístup ke konfiguraci zařízení a informacím o stavu nasazení musíte mít platný ověřovací token.

## <a name="device-enrollment-charts"></a>Grafy registrace zařízení
1. V Azure Portal přejděte na **Microsoft Intune** -> **DeviceEnrollment**.
2. Pomocí [Graph exploreru](https://developer.microsoft.com/graph/graph-explorer) stáhněte podkladová data grafů.
    - Pro stav registrace zkopírujte tento [dotaz na stav registrace](https://graph.microsoft.com/beta/reports/managedDeviceEnrollmentFailureTrends()/content) a vložte ho do [Graf exploreru](https://developer.microsoft.com/graph/graph-explorer).
    - Pro nejzávažnější chyby registrace zkopírujte tento [dotaz na chyby registrace](https://graph.microsoft.com/beta/reports/managedDeviceEnrollmentTopFailures(period=null)/content) a vložte ho do [Graf exploreru](https://developer.microsoft.com/graph/graph-explorer).

    > [!NOTE]
    > Pro přístup k datům registrace zařízení musíte mít platný ověřovací token. 

## <a name="after-a-data-warehouse-account-move"></a>Po přesunutí účtu datového skladu

Po přesunutí účtu datového skladu uvidíte v Intune, že datový sklad byl resetován a vaše data jsou teď uložená v novém umístění. Obnoví se grafy a možnosti exportu a zobrazí se oznámení, které vás po kliknutí nasměruje na článek s vysvětlením, proč byly grafy resetovány.  

## <a name="data-warehouse-move-example"></a>Příklad přesunutí datového skladu 

Zákazník X požaduje, aby bylo přesunutí účtu zahájeno 1. 6. 2018. V odpovědi na tento požadavek obdrží zákazník odkaz na dokumentaci s podrobnými kroky, které má podniknout, pokud si chce zazálohovat předchozí datový sklad. 1. 6. 2018 se datový sklad a grafy, které podporuje, resetují a data se začnou ukládat v novém datovém centru. 

## <a name="next-steps"></a>Další kroky

- Podívejte [se, co je nového v Intune každý týden](../fundamentals/whats-new.md). Můžete také získat informace o nadcházejících změnách, důležitá oznámení o službě a informace o minulých vydaných verzích.
- Přečtěte si [Blog Microsoft Intune](https://go.microsoft.com/fwlink/?LinkID=273882).
