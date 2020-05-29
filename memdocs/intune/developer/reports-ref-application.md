---
title: Referenční informace o entitách aplikace
titleSuffix: Microsoft Intune
description: Téma referenčních informací ke kategorii Aplikace pro kolekce entit v rozhraní API datového skladu Intune
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: A92DEF30-5D01-4774-9917-E26F5F0E2E68
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 402285b871db6c3ff18e8f89ec0553a51dab9c13
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165545"
---
# <a name="reference-for-application-entities"></a>Referenční informace o entitách aplikací

Kategorie **aplikace** obsahuje entity pro zařízení, která sledují informace, jako například:

- Verze aplikace
- Zdroj instalace aplikace
- Typ vývojářů, kteří aplikaci vytvořili
- Typy spravovaného softwaru pro aplikaci, například **sidecar** nebo **desktop**
- Stav VPP (Volume Purchase Program) pro aplikaci

## <a name="apprevisions"></a>appRevisions

Entita **appRevision** obsahuje seznam všech verzí aplikací.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| appKey |Jedinečný identifikátor aplikace |123 |
| applicationId |Jedinečný identifikátor aplikace – podobá se AppKey, ale tento klíč je přirozený. |b66bc706-ffff-7437-0340-032819502773 |
| revision |Verze, kterou uvedl správce během nahrávání binárního souboru |2 |
| title |Název aplikace |Excel |
| vydavatel |Vydavatel aplikace |Microsoft |
| uploadState |Stav nahrávání aplikace |1 |
| appTypeKey |Odkaz na entitu AppType, která je popsaná v následujícím oddílu | |
| vppProgramTypeKey |Odkaz na entitu VppProgramType, která je popsaná níže | |
| creationTime |Čas vytvoření této revize |23.11.2016 12:00:00 |
| modifiedTime |Čas poslední změny nějakého prvku, který s touto revizí souvisí |23.11.2016 12:00:00 |
| velikost |Velikost binárního souboru | |
| startDateInclusiveUTC |Datum a čas ve standardu UTC, kdy se tato revize aplikace v datovém skladu vytvořila |23.11.2016 12:00:00 |
| endDateExclusiveUTC |Datum a čas ve standardu UTC, od kdy je tato revize aplikace zastaralá |23.11.2016 12:00:00 |
| Aktuální |Určuje, jestli tato verze aplikace v datovém skladu je nebo není aktuální |Pravda/nepravda |
| rowLastModifiedDateTimeUTC |Datum a čas ve standardu UTC, kdy se tato verze aplikace v datovém skladu naposledy změnila |23.11.2016 12:00:00 |

## <a name="apptypes"></a>appTypes

Entita **appType** obsahuje seznam zdrojů instalace aplikace.

| Vlastnost  | Popis |
|---------|------------|
| appTypeID |ID pro daný typ |
| appTypeKey |Náhradní klíč pro daný klíč |
| appTypeName |Typ aplikace |

### <a name="example"></a>Příklad

| AppTypeID  | Name | Popis |
|---------|------------|--------|
| 0 |Aplikace z obchodu pro Android | Aplikace z obchodu pro Android |
| 1 |Obchodní aplikace pro Android | Obchodní aplikace pro Android |
| 2 |Spravovaná aplikace z obchodu pro Android (MAM) | Aplikace z obchodu pro Android s povolenou správou |
| 3 |Aplikace z obchodu pro iOS | Aplikace z obchodu pro iOS |
| 4 |Obchodní aplikace pro iOS | Obchodní aplikace pro iOS |
| 5 |Spravovaná aplikace obchodu pro iOS (MAM) | Aplikace z obchodu pro iOS s povolenou správou |
| 6 |Sada O365 Pro Plus | Aplikace Microsoft 365 pro Windows 10 |
| 7 |Webová aplikace | Webová aplikace |
| 8 |Aplikace pro Windows Phone 8.1 Store | Aplikace pro Windows Phone 8.1 Store |
| 9 |Aplikace pro Windows Store | Aplikace pro Windows Store |
| 10 |Obchodní aplikace pro Windows | Obchodní aplikace Windows AppX |
| 11 |Windows Mobile MSI | Obchodní aplikace MSI |
| 12 |Obchodní aplikace pro Windows Phone | Obchodní aplikace pro Windows Phone |


## <a name="vppprogramtypes"></a>vppProgramTypes

Entita **vppProgramType** obsahuje seznam možných typů programu VPP pro aplikaci.

| Vlastnost  | Popis |
|---------|------------|
| vppProgramTypeID | ID pro daný typ |
| vppProgramTypeKey | Náhradní klíč pro daný klíč |
| vppProgramTypeName | Typ programu VPP |

### <a name="example"></a>Příklad

| VppProgramID  | Name | Popis |
|---------|------------|--------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Microsoft | Program VPP společnosti Microsoft |
| 00000000-0000-0000-0000-000000000000 | Ještě není k dispozici | Výchozí hodnota, žádný program VPP |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple | Program VPP společnosti Apple |



## <a name="applicationinventories"></a>applicationInventories

Entita **entita applicationinventory zobrazuje** obsahuje seznam aplikací, které se v zařízení našly v okamžiku shromažďování inventáře.

| Vlastnost  | Popis |
|---------|------------|
| deviceKey | Jedná se o odkaz na tabulku zařízení obsahující ID zařízení v Intune. |
| dateKey | Odkaz na tabulku kalendářních dat udávající den inventáře |
| applicationName | Název aplikace. |
| applicationVersion | Verze aplikace |
| bundleSize | Velikost aplikace v bajtech |

## <a name="mobileappinstallstates"></a>mobileAppInstallStates

Entita **entita mobileappinstallstate** představuje stav instalace mobilní aplikace poté, co byla přiřazena ke skupině obsahující zařízení, uživatele nebo obojímu.

| Vlastnost | Popis |
|---|---|
| appInstallStateKey | Jedinečné ID stavu instalace aplikace pro váš účet |
| appInstallState | Hodnota výčtu stavu instalace aplikace |
| appInstallStateName | Název stavu instalace aplikace |



