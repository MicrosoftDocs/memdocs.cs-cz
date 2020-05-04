---
title: Správa mobilních aplikací (MAM)
titleSuffix: Microsoft Intune
description: Téma referenčních informací ke kategorii Správa mobilních aplikací pro kolekce entit v rozhraní API datového skladu Intune
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 084F11AD-F7BA-45A4-8424-45E6E4564930
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 428ee1ce93b4f6fe21c4b0180a9df222f3e23e09
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331683"
---
# <a name="reference-for-mobile-app-management-mam-entities"></a>Referenční informace o entitách správy mobilních aplikací (MAM)

Kategorie **Správa mobilních aplikací** obsahuje entity pro mobilní aplikace, například:

- Aplikace
- Instance
- Stav přihlášení
- Stav
- Stav zásad
- Stav registrace
- Typy platformy

## <a name="mamapplications"></a>mamApplications

Entita **mamApplication** obsahuje seznam obchodních aplikací (LOB), které jsou spravované prostřednictvím správy mobilních aplikací (MAM) bez registrace ve vašem podniku.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| mamApplicationKey |Jedinečný identifikátor aplikace MAM | 432 |
| mamApplicationName |Název aplikace MAM |Příklad názvu aplikace MAM |
| mamApplicationId |ID aplikace MAM | 123 |
| IsDeleted |Určuje, jestli je tento záznam aplikace MAM aktualizovaný. <br>True – aplikace MAM má v této tabulce nový záznam s aktualizovanými poli. <br>False – jedná se o nejnovější záznam pro tuto aplikaci MAM. |Pravda/nepravda |
| startDateInclusiveUTC |Datum a čas ve standardu UTC, kdy se tato aplikace MAM v datovém skladu vytvořila |23.11.2016 12:00:00 |
| deletedDateUTC |Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True |23.11.2016 12:00:00 |
| rowLastModifiedDateTimeUTC |Datum a čas ve standardu UTC, kdy se tato aplikace MAM v datovém skladu naposledy změnila |23.11.2016 12:00:00 |


## <a name="mamapplicationinstances"></a>mamApplicationInstances

Entita **mamApplicationInstance** obsahuje seznam spravovaných aplikací pro správu mobilních aplikací (MAM) jako jednotné instance na uživatele a zařízení. Všichni uživatelé a zařízení, kteří jsou v této entitě uvedení, jsou chránění, protože mají přiřazenou aspoň jednu zásadu MAM.


|          Vlastnost          |                                                                                                  Popis                                                                                                  |               Příklad                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   Vlastnosti applicationinstancekey   |                                                               Jedinečný identifikátor instance aplikace MAM v datovém skladu – náhradní klíč                                                                |                 123                  |
|           userId           |                                                                              ID uživatele, který má tuto aplikaci MAM nainstalovanou.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              Jedinečný identifikátor instance aplikace MAM – podobá se vlastnosti ApplicationInstanceKey, ale tento identifikátor představuje přirozený klíč.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | ID aplikace mam, pro kterou se vytvořila tato instance aplikace mam   | 23.11.2016 12:00:00   |
|     applicationVersion     |                                                                                     Verze aplikace pro danou aplikaci MAM                                                                                      |                  2                   |
|        createdDate         |                                                                 Datum vytvoření daného záznamu instance aplikace MAM Hodnota může být null.                                                                 |        23.11.2016 12:00:00        |
|          platforma          |                                                                          Platforma zařízení, na kterém je daná aplikace MAM nainstalovaná                                                                           |                  2                   |
|      platformVersion       |                                                                      Verze platformy zařízení, na kterém je daná aplikace MAM nainstalovaná                                                                       |                 2,2                  |
|         sdkVersion         |                                                                            Verze sady SDK MAM, pomocí které byla daná aplikace MAM zabalena                                                                            |                 3,2                  |
| mamDeviceId | ID zařízení, ke kterému je přidružená instance aplikace MAM   | 23.11.2016 12:00:00   |
| mamDeviceType | Typ zařízení, ke kterému je přidružená instance aplikace MAM   | 23.11.2016 12:00:00   |
| mamDeviceName | Název zařízení, ke kterému je přidružená instance aplikace MAM   | 23.11.2016 12:00:00   |
|         IsDeleted          | Určuje, jestli je tento záznam instance aplikace MAM aktualizovaný. <br>True – tato instance aplikace MAM má v této tabulce nový záznam s aktualizovanými poli. <br>False – jedná se o nejnovější záznam pro tuto instanci aplikace MAM. |              Pravda/nepravda              |
|   startDateInclusiveUtc    |                                                              Datum a čas ve standardu UTC, kdy se tato instance aplikace MAM v datovém skladu vytvořila                                                               |        23.11.2016 12:00:00        |
|       deletedDateUtc       |                                                                             Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True                                                                              |        23.11.2016 12:00:00        |
| rowLastModifiedDateTimeUtc |                                                           Datum a čas ve standardu UTC, kdy se tato instance aplikace MAM v datovém skladu naposledy změnila                                                            |        23.11.2016 12:00:00        |


## <a name="mamcheckins"></a>mamCheckins

Entita **mamCheckin** představuje data shromážděná při vrácení instance aplikace správy mobilních aplikací (MAM) ve službě Intune. 

> [!Note]  
> Pokud se instance aplikace přihlásí několikrát denně, uloží se to v datovém skladu jako jediné přihlášení.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| dateKey |Klíč data, kdy se přihlášení aplikace MAM v datovém skladu zaznamenalo | 20160703 |
| Vlastnosti applicationinstancekey |Klíč instance aplikace, který je k tomuto přihlášení aplikace MAM přidružený | 123 |
| userKey |Klíč uživatele, který je k tomuto přihlášení aplikace MAM přidružený | 4323 |
| mamApplicationKey |Aplikační klíč aplikace přidružený k vrácení aplikace MAM se změnami | 432 |
| Vlastnosti devicehealthkey |Klíč pro stav, který je k tomuto přihlášení aplikace MAM přidružený | 321 |
| Vlastnosti platformkey |Představuje platformu zařízení, které je k tomuto přihlášení aplikace MAM přidružené |123 |
| effectiveAppliedPolicyKey |Představuje platné použité zásady, které jsou k tomuto přihlášení aplikace MAM přidružené. Platné použité zásady jsou výsledkem sloučení všech zásad, které jsou pro konkrétní aplikaci a uživatele relevantní. | 322 |
| pastCheckInDate |Datum a čas posledního přihlášení dané aplikace MAM Hodnota může být null. |23.11.2016 12:00:00 |


## <a name="mamdevicehealth"></a>mamDeviceHealth

Entita **mamDeviceHealth** představuje zařízení, která mají nasazené zásady správy mobilních aplikací (MAM), i když mají jailbreak.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| Vlastnosti devicehealthkey |Jedinečný identifikátor zařízení a jeho přidruženého stavu v datovém skladu – náhradní klíč |123 |
| Přidružený |Jedinečný identifikátor zařízení a jeho přidruženého stavu – podobá se vlastnosti DeviceHealthKey, ale tento identifikátor představuje přirozený klíč. |b66bc706-FFFF-7777-0340-032819502773 |
| deviceHealthName |Představuje stav zařízení. <br>Není k dispozici – žádné informace o tomto zařízení nejsou dostupné. <br>V pořádku – nejedná se o zařízení s jailbreakem. <br>Není v pořádku – jedná se o zařízení s jailbreakem. |Není k dispozici, V pořádku, Není v pořádku |
| rowLastModifiedDateTimeUtc |Datum a čas ve standardu UTC, kdy se tento konkrétní stav zařízení MAM v datovém skladu naposledy změnil |23.11.2016 12:00:00 |

## <a name="mameffectivepolicies"></a>mamEffectivePolicies

Entita **mamEffectivePolicy** obsahuje seznam všech efektivních zásad správy mobilních aplikací (MAM) používaných ve vaší organizaci. Platné použité zásady jsou výsledkem sloučení všech zásad, které jsou pro konkrétní aplikaci a uživatele relevantní.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| effectivePolicyKey |Jedinečný identifikátor platných zásad MAM v datovém skladu |2 |
| realPolicyKey |Jedinečný identifikátor zásad MAM, které vytvořil pracovník oddělení IT |1 |
| rowCreatedDateTimeUtc |Datum a čas ve standardu UTC, kdy se tyto platné zásady MAM v datovém skladu vytvořily |23.11.2016 12:00:00 |

## <a name="mamplatforms"></a>mamPlatforms

Entita **mamPlatform** obsahuje seznam názvů a typů platforem, na kterých se nainstalovala aplikace pro správu mobilních aplikací (MAM).


|          Vlastnost          |                                    Popis                                    |                         Příklad                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        Vlastnosti platformkey         |     Jedinečný identifikátor platformy v datovém skladu – náhradní klíč      |                           123                           |
|          platforma          | Jedinečný identifikátor platformy – podobá se vlastnosti PlatformKey, jedná se ale o přirozený klíč. |                           123                           |
|        platformName        |                                   Název platformy                                   | Není k dispozici <br>Žádná <br>Windows <br>iOS <br>Android. |
| rowLastModifiedDateTimeUtc | Datum a čas ve standardu UTC, kdy se tato platforma v datovém skladu naposledy změnila  |                 23.11.2016 12:00:00                  |

