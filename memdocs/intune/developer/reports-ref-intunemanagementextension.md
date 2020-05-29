---
title: Entita IntuneManagementExtension
titleSuffix: Microsoft Intune
description: Téma referenčních informací ke kategorii Entita IntuneManagementExtension pro kolekce entit v rozhraní API datového skladu Intune
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: aac78143e2b1e15f7b718c70d2dc7168c00f8fd4
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165290"
---
# <a name="reference-for-intune-management-extensions"></a>Referenční informace o rozšířeních pro správu Intune

Kategorie **intuneManagementExtensions** obsahuje entity pro mobilní zařízení, které sledují informace, jako například:

- Verze IntuneManagementExtension
- Stav instalace IntuneManagementExtension

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

Entita **intuneManagementExtensionVersion** obsahuje všechny verze, které používá intuneManagementExtensions.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| extensionVersionKey |Jedinečný identifikátor verze intuneManagementExtensions | 1 |
| extensionVersion |Číslo verze tvořené 4 číslicemi |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

**IntuneManagementExtensionHealthState** obsahuje seznam všech možných stavů intuneManagementExtensions.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| extensionStateKey |Jedinečný identifikátor stavu | 2 |
| extensionState |Stav IntuneManagementExtension | V pořádku |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

**IntuneManagementExtension** uvádí stav IntuneManagementExtensions na každém zařízení s Windows 10 za den.
Uchovávají se data za posledních 60 dní. 


|      Vlastnost       |                         Popis                         | Příklad |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Jedinečný identifikátor data                |   123   |
|      tenantKey      |              Jedinečný identifikátor tenanta               |   456   |
|      deviceKey      |              Jedinečný identifikátor zařízení               |   789   |
| extensionVersionKey | Jedinečný identifikátor verze intuneManagementExtension |    1    |
|  extensionStateKey  |             Jedinečný identifikátor stavu              |    2    |

