---
title: Přidružení zařízení uživatelů – Datový sklad Intune
titleSuffix: Microsoft Intune
description: Entita UserDeviceAssociation obsahuje přidružení zařízení uživatelů ve vaší organizaci.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6127b365a04ad48a9cbaa98bdef821c4d1334181
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79325571"
---
# <a name="reference-for-user-device-association-entity"></a>Referenční informace o entitě Přidružení zařízení uživatelů

Entita **userDeviceAssociation** obsahuje přidružení zařízení uživatelů ve vaší organizaci.

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Název        |                                           Popis                                            |        Příklad         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Jedinečný identifikátor uživatele v datovém skladu (náhradní klíč)               |          123           |
|     deviceKey      |                      Jedinečný identifikátor zařízení v datovém skladu                      |          123           |
| createdDateTimeUTC |           Datum a čas, kdy bylo přidružení zařízení uživatele vytvořeno. Používá formát UTC.           | 23.11.2016 12:00:00 |
|     IsDeleted      | Udává, že uživatel registraci zařízení zrušil a že přidružení už není aktuální. |       Pravda/nepravda       |
|  endedDateTimeUTC  |              Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu <strong>True</strong>               | 23.06.2017 12:00:00 |

## <a name="next-steps"></a>Další kroky

- Přečtěte si další informace o [datovém skladu Intune](reports-nav-create-intune-reports.md).
