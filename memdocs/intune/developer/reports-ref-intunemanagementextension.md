---
title: Entita IntuneManagementExtension
titleSuffix: Microsoft Intune
description: Téma referenčních informací ke kategorii Entita IntuneManagementExtension pro kolekce entit v rozhraní API datového skladu Intune
keywords: Datový sklad Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
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
ms.openlocfilehash: f8152eb12779376e1885d0a2b2898cd602aa825d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331687"
---
# <a name="reference-for-intune-management-extensions"></a>Referenční informace o rozšířeních pro správu Intune

Kategorie **intuneManagementExtensions** obsahuje entity pro mobilní zařízení, které sledují informace, jako například:

- Verze IntuneManagementExtension
- Stav instalace IntuneManagementExtension

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

Entita **intuneManagementExtensionVersion** obsahuje všechny verze, které používá intuneManagementExtensions.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| ExtensionVersionKey |Jedinečný identifikátor verze intuneManagementExtensions | 1 |
| ExtensionVersion |Číslo verze tvořené 4 číslicemi |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

**IntuneManagementExtensionHealthState** obsahuje seznam všech možných stavů intuneManagementExtensions.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| ExtensionStateKey |Jedinečný identifikátor stavu | 2 |
| ExtensionState |Stav IntuneManagementExtension | V pořádku |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

**IntuneManagementExtension** uvádí stav IntuneManagementExtensions na každém zařízení s Windows 10 za den.
Uchovávají se data za posledních 60 dní. 


|      Vlastnost       |                         Popis                         | Příklad |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Jedinečný identifikátor data                |   123   |
|      TenantKey      |              Jedinečný identifikátor tenanta               |   456   |
|      deviceKey      |              Jedinečný identifikátor zařízení               |   789   |
| ExtensionVersionKey | Jedinečný identifikátor verze intuneManagementExtension |    1    |
|  ExtensionStateKey  |             Jedinečný identifikátor stavu              |    2    |

