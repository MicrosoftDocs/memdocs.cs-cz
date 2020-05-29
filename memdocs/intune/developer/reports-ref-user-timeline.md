---
title: Časová osa entity uživatele datového skladu
titleSuffix: Microsoft Intune
description: Přečtěte si, jak Microsoft Intune datový sklad představuje uživatele na časové ose.
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
ms.assetid: 363D148E-688F-4830-B6DE-AB4FE3648817
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c5fb086e36bfc16ddc2123227887d3d8bf61211
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165154"
---
# <a name="user-lifetime-representation-in-the-microsoft-intune-data-warehouse"></a>Znázornění životnosti uživatele v datovém skladu Microsoft Intune

Odpovědi na otázky o časových trendech získáte ze snímků dat uložených po jeden měsíc v Datovém skladu Intune. Můžete například zobrazit počet uživatelů přidaných za měsíc. Můžete také chtít zjistit počet uživatelů odebraných ze systému.

Datový sklad poskytuje tento typový přehled díky uloženým historickým informacím. Datový sklad může sledovat životnost entity. Sklad zaznamenává informace o času vytvoření entity, času změny stavu entity a času odstranění entity. Díky historii zachycené kvantitativním měřením denních snímků můžete zpětně porovnávat jednotlivé dny mezi sebou.

Práce s dobou života entit může být matoucí, protože entity mění stav. To znamená, že když se podíváte na snímek v třicátý den, nemusí v datech existovat uživatelský záznam v aktivním stavu. Ve dnech 29–28 může existovat záznam entity v aktivním stavu. A před dnem 28 uživatel nemusel vůbec neexistovat.

Tento scénář bude jasnější, když si projdete životnost entity.

Představte si uživatele **Jan Macek**, který získá licenci na 1.6.2017. V tabulce **Uživatel** bude následující položka: 
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| Jan Macek | FALSE | 1.6.2017 | 31.12.9999 | TRUE
 
Jan Macek vrací licenci 25.7.2017. Tabulka **Uživatel** obsahuje následující položky. Změny v existujících záznamech jsou `marked`. 

| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| Jan Macek | FALSE | 1.6.2017 | `07/26/2017` | `FALSE` 
| Jan Macek | TRUE | 26.7.2017 | 31.12.9999 | TRUE 

První řádek označuje, že Jan Macek existoval v Intune od 1.6.2017 do 25.7.2017. Druhý záznam označuje, že uživatel byl 25.7.2017 odstraněn a již není v Intune k dispozici.

Nyní si představte, že uživatel Jan Macek získá novou licenci dne 31.8.2017. V tabulce Uživatel budou následující položky:
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| Jan Macek | FALSE | 1.6.2017 | 26.7.2017 | FALSE 
| Jan Macek | TRUE | 26.7.2017 | `08/31/2017` | `FALSE` 
| Jan Macek | FALSE | 08/31/2017 | 31.12.9999 | TRUE 
 
Osoba, která chce zobrazit aktuální stav všech uživatelů, musí použít filtr `IsCurrent = TRUE`. 
 
Osoba, která chce zobrazit pouze existující uživatele, musí použít filtr `IsCurrent = TRUE AND IsDeleted = FALSE`.

## <a name="dimension-tables-in-the-entity-lifetime"></a>Tabulky dimenzí v době života entity

Aby bylo možné zachovat historii změn stavu entit, neodstraňuje Intune záznamy. Místo toho označí záznamy jako odstraněné. Tomu se říká obnovitelné odstranění. Tabulky dimenzí využívají ke sledování doby života záznamů různé sloupce metadat. 

Nejčastěji používané sloupce metadat: 

| Název vlastnosti metadat  | Interpretace hodnot |
|--|--|
| IsDeleted | Určuje, zda byla entita odstraněna v Intune. |
| StartDateInclusiveUTC  | Datum podle standardu UTC, kdy se entita načetla do Datového skladu Intune. Entita byla pravděpodobně vytvořena před jejím importem do Datového skladu Intune. |
| DeletedDateUTC  | Datum podle standardu UTC, kdy byla entita odstraněna v Intune. |  

Každý sloupec metadat začínající předponou **Row**, jako například **RowLastModifiedDateTimeUTC**, označuje, kdy se záznam vytvořil nebo změnil v Datovém skladu Intune. Sklad je podřízený datům v Intune. Tato hodnota nemá žádný vztah k době života entity v Intune.  
 
Každý, kdo chce zobrazit pouze aktuálně existující entity dimenze, musí použít filtr **IsDeleted = FALSE**.

## <a name="next-steps"></a>Další kroky

- Další informace o entitě **Aktuální uživatel** najdete v tématu [Referenční informace o entitě aktuálního uživatele](reports-ref-data-model.md).
- Další informace o entitě **Uživatel** najdete v tématu [Referenční informace pro entitu uživatele](reports-ref-user.md).
