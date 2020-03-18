---
title: Referenční informace pro entity zásad
titleSuffix: Microsoft Intune
description: Téma referenčních informací ke kategorii Zásady pro kolekce entit v rozhraní API datového skladu Intune
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
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a2f13bddb852b46459c9c79df39dda49ef9549d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325579"
---
# <a name="reference-for-policy-entities"></a>Referenční informace pro entity zásad

Kategorie **zásady** obsahuje entity pro mobilní zařízení, které sledují informace, jako například:

- Inventář konfiguračních profilů zařízení, konfiguračních profilů aplikací a zásad dodržování předpisů  
- Počet zařízení v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den  
- Počet uživatelů v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den  
- Kumulativní počet zařízení v úspěšném, čekajícím, neúspěšném nebo chybovém stavu  

## <a name="policies"></a>policies

Entita **zásady** uvádí profily konfigurace zařízení, konfigurační profily aplikací a zásady dodržování předpisů. Zásady se správou mobilních zařízení (MDM) můžete přiřadit skupině ve vašem podniku.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| PolicyKey |Jedinečný klíč reprezentující zásady v datovém skladu |123 |
| PolicyId |Jedinečný identifikátor zásad v datovém skladu |b66bc706-ffff-7437-0340-032819502773 |
| policyName |Název zásad |„Směrný plán Windows 10“ |
| policyVersion |Verze zásad Když dojde k úpravě nebo změně zásad, vytvoří se novější verze. |1, 2, 3 |
| IsDeleted |Určuje, jestli je záznam zásad aktualizovaný.  <br>True – zásada má nový záznam s aktualizovanými poli. <br>False – jedná se o nejnovější záznam pro zásady. |True nebo False |
| startDateInclusiveUTC |Datum a čas ve standardu UTC, kdy se tyto zásady v datovém skladu vytvořily |23.11.2016 12:00:00 |
| DeletedDateUTC |Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True |23.11.2016 12:00:00 |
| rowLastModifiedDateTimeUTC |Datum a čas ve standardu UTC, kdy se tyto zásady v datovém skladu naposledy změnily |23.11.2016 12:00:00 |

## <a name="policytypes"></a>policyTypes

Entita **policyType** obsahuje seznam typů profilů konfigurace zařízení, konfiguračních profilů aplikací a zásad dodržování předpisů. Zásady se správou mobilních zařízení (MDM) můžete přiřadit skupině ve vašem podniku.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| PolicyTypeId |Jedinečný identifikátor zásad ve zdrojovém systému |123 |
| PolicyTypeKey |Jedinečný identifikátor zásad v datovém skladu |1 |
| PolicyTypeName |Název typu zásad |Zásady dodržování předpisů Windows 10 |

## <a name="device-configuration"></a>Konfigurace zařízení

Entita **deviceConfigurationProfileDeviceActivity** uvádí počet **zařízení** v úspěšném, nevyřízeném, neúspěšném nebo chybovém stavu za den. Číslo odráží konfigurační profily Zařízení přiřazené entitě. Pokud je například **zařízení** v úspěšném stavu pro všechny přiřazené zásady, zvýší se v tomto dni čítač úspěšného dokončení. Pokud má zařízení přiřazené dva profily, jeden je v úspěšném stavu a druhý v chybovém stavu, entita zvýší čítač úspěšných zařízení o jedno a umístí zařízení do chybového stavu. Entita uvádí, kolik zařízení je v jakém stavu v daném dni za posledních 30 dní.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| dateKey |Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo |20160703 |
| Čeká se na zadání |Počet jedinečných zařízení v čekajícím stavu |123 |
| Úspěšné |Počet jedinečných zařízení v úspěšném stavu |12 |
| chyba |Počet jedinečných zařízení v chybovém stavu |10 |
| selhalo |Počet jedinečných zařízení v neúspěšném stavu |2 |

Entita **entita deviceconfigurationprofileuseractivity** uvádí počet **uživatelů** v úspěšném, nevyřízeném, neúspěšném nebo chybovém stavu za den. Číslo odráží konfigurační profily Zařízení přiřazené entitě. Například pokud je **uživatel** v úspěšném stavu pro všechny přiřazené zásady, posune čítač úspěšného počítadla o jeden den. Pokud má uživatel přiřazené dva profily, jeden je v úspěšném stavu a druhý je v chybovém stavu, započítá se uživatel v chybovém stavu.  Entita **entita deviceconfigurationprofileuseractivity** uvádí, kolik uživatelů se v daném dni během posledních 30 dnů zobrazuje.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| dateKey |Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo |20160703 |
| Čeká se na zadání |Počet jedinečných uživatelů v čekajícím stavu |123 |
| Úspěšné |Počet jedinečných uživatelů v úspěšném stavu |12 |
| chyba |Počet jedinečných uživatelů v chybovém stavu |10 |
| selhalo |Počet jedinečných uživatelů v neúspěšném stavu |2 |

## <a name="policytypeactivities"></a>policyTypeActivities

Entita **policyTypeActivity** obsahuje kumulativní počet zařízení v úspěšném, nevyřízeném, neúspěšném nebo chybovém stavu. Zobrazí tyto stavy s ohledem na konfigurační profil zařízení, konfigurační profil aplikace nebo zásady dodržování předpisů na den.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| dateKey |dateKey, když se v datovém skladu zaznamenalo vrácení se změnami konfiguračního profilu zařízení. |20160703 |
| PolicyKey |policyKey se dá připojit k zásadám a získat tak zásadu. |Směrný plán Windows 10 |
| PolicyTypeKey |Typ klíče zásad, který jde připojit k typu zásad a získat tak název typu zásad |Zásady dodržování předpisů Windows 10 |
| Čeká se na zadání |Počet jedinečných zařízení v čekajícím stavu |123 |
| Úspěšné |Počet jedinečných zařízení v úspěšném stavu |12 |
| chyba |Počet jedinečných zařízení v chybovém stavu |10 |
| selhalo |Počet jedinečných zařízení v neúspěšném stavu |2 |

## <a name="compliance-policy"></a>Zásady dodržování předpisů

Referenční dokumentace rozhraní Compliance Policy API obsahuje entity, které poskytují stavové informace týkající se zásad dodržování předpisů přiřazených k zařízením.

### <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities

Následující tabulka shrnuje stav přiřazení zásad dodržování předpisů k zařízením. Uvádí počet zařízení nacházejících se v jednotlivých stavech shody.


|Vlastnost     |Popis  |Příklad  |
|---------|---------|---------|
|dateKey  |Klíč data, kdy se vytvořil souhrn pro zásady dodržování předpisů|20161204 |
|neznámý  |Počet zařízení, která jsou offline nebo kterým se nepodařilo komunikovat s Intune nebo Azure AD z jiných důvodů |5|
|NotApplicable      |Počet zařízení, ve kterých nejsou použitelné zásady dodržování předpisů, na které zacílil správce|201 |
|Kompatibilní      |Počet zařízení, ve kterých se úspěšně použily jedny nebo více zásad dodržování předpisů, na které zacílil správce |4083 |
|V období odkladu      |Počet zařízení, která nevyhovují předpisům, ale jsou v období odkladu definovaném správcem |57|
|Nekompatibilních      |Počet zařízení, u kterých se nepodařilo použít jedny nebo více zásad dodržování předpisů, na které zacílil správce nebo u kterých uživatel nedodržel zásady, na které zacílil správce|43 |
|chyba      |Počet zařízení, kterým se nepodařilo komunikovat s Intune nebo Azure AD a která vrátila chybovou zprávu |3|

### <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities 

Následující tabulka shrnuje stav přiřazení zásad dodržování předpisů k zařízením pro jednotlivé zásady a pro jednotlivé typy zásad. Uvádí počet zařízení nacházejících se v jednotlivých stavech shody pro všechny přiřazené zásady dodržování předpisů.



|Vlastnost  |Popis  |Příklad  |
|---------|---------|---------|
|dateKey  |Klíč data, kdy se vytvořil souhrn pro zásady dodržování předpisů|20161219|
|PolicyKey     |Klíč pro zásady dodržování předpisů, pro který se vytvořil souhrn |10178 |
|PolicyPlatformKey      |Klíč pro typ platformy zásad dodržování předpisů, pro který se vytvořil souhrn|5|
|neznámý     |Počet zařízení, která jsou offline nebo kterým se nepodařilo komunikovat s Intune nebo Azure AD z jiných důvodů|13|
|NotApplicable     |Počet zařízení, ve kterých nejsou použitelné zásady dodržování předpisů, na které zacílil správce|3|
|Kompatibilní      |Počet zařízení, ve kterých se úspěšně použily jedny nebo více zásad dodržování předpisů, na které zacílil správce |45|
|V období odkladu      |Počet zařízení, která nevyhovují předpisům, ale jsou v období odkladu definovaném správcem |3|
|Nekompatibilních      |Počet zařízení, u kterých se nepodařilo použít jedny nebo více zásad dodržování předpisů, na které zacílil správce nebo u kterých uživatel nedodržel zásady, na které zacílil správce|7|
|chyba      |Počet zařízení, kterým se nepodařilo komunikovat s Intune nebo Azure AD a která vrátila chybovou zprávu |3|

### <a name="policyplatformtypes"></a>policyPlatformTypes

Následující tabulka obsahuje typy platforem všech přiřazených zásad. Typy platforem zásad, které se k žádným zařízením nikdy nepřiřadily, se v této tabulce nenacházejí.


|Vlastnost  |Popis  |Příklad  |
|---------|---------|---------|
|PolicyPlatformTypeKey      |Jedinečný klíč pro typ platformy zásad |20170519 |
|PolicyPlatformTypeId      |Jedinečný identifikátor pro typ platformy zásad|1|
|PolicyPlatformTypeName      |Název typu platformy zásad|AndroidForWork |

### <a name="policydeviceactivities"></a>policyDeviceActivities

Následující tabulka uvádí počet zařízení v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den. Číslo odráží data pro jednotlivé profily typu zásad. Pokud se například zařízení nachází v úspěšném stavu pro všechny své přiřazené zásady, zvýší čítač úspěšných zařízení pro daný den o jedno. Pokud má zařízení přiřazené dva profily, jeden je v úspěšném stavu a druhý v chybovém stavu, entita zvýší čítač úspěšných zařízení o jedno a umístí zařízení do chybového stavu. V entitě policyDeviceActivity se uvádí počet zařízení, ve kterých se v daném dni během posledních 30 dnů zobrazuje stav.

|Vlastnost  |Popis  |Příklad  |
|---------|---------|---------|
|dateKey|Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo|20160703|
|Čeká se na zadání|Počet jedinečných zařízení v čekajícím stavu|123|
|Úspěšné|Počet jedinečných zařízení v úspěšném stavu|12|
|PolicyKey|policyKey se dá připojit k zásadám a získat tak zásadu.|Směrný plán Windows 10|
|chyba|Počet jedinečných zařízení v chybovém stavu|10|
|selhalo|Počet jedinečných zařízení v neúspěšném stavu|2|

### <a name="policyuseractivities"></a>policyUserActivities

Následující tabulka uvádí počet uživatelů v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den. Číslo odráží data pro jednotlivé profily typu zásad. Pokud se například uživatel nachází v úspěšném stavu pro všechny své přiřazené zásady, posune čítač úspěšných uživatelů pro daný den o jedna nahoru. Pokud má uživatel přiřazené dva profily, jeden je v úspěšném stavu a druhý je v chybovém stavu, započítá se uživatel v chybovém stavu. Entita PolicyUserActivity uvádí, kolik uživatelů je v jakém stavu v daném dni za posledních 30 dní.


| Vlastnost  |                                         Popis                                         |       Příklad       |
|-----------|---------------------------------------------------------------------------------------------|---------------------|
|  dateKey  | Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo |      20160703       |
|  Čeká se na zadání  |                         Počet jedinečných zařízení v čekajícím stavu                          |         123         |
| Úspěšné |                         Počet jedinečných zařízení v úspěšném stavu                          |         12          |
| PolicyKey |                 policyKey se dá připojit k zásadám a získat tak zásadu.                 | Směrný plán Windows 10 |
|   chyba   |                          Počet jedinečných zařízení v chybovém stavu                           |         10          |

