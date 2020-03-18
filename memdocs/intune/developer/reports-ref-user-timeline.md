---
title: Časová osa entity uživatele datového skladu
titleSuffix: Microsoft Intune
description: Přečtěte si, jak Microsoft Intune datový sklad představuje uživatele na časové ose.
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
ms.assetid: 363D148E-688F-4830-B6DE-AB4FE3648817
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b339941da247cf6bc5efd9f3fa9c598415ed0e9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325575"
---
# <a name="user-lifetime-representation-in-the-microsoft-intune-data-warehouse"></a>Znázornění životnosti uživatele v datovém skladu Microsoft Intune

Odpovědi na otázky o časových trendech získáte ze snímků dat uložených po jeden měsíc v Datovém skladu Intune. Můžete například zobrazit počet uživatelů přidaných za měsíc. Můžete také chtít zjistit počet uživatelů odebraných ze systému.

Datový sklad poskytuje tento typový přehled díky uloženým historickým informacím. Datový sklad může sledovat životnost entity. Sklad zaznamenává informace o času vytvoření entity, času změny stavu entity a času odstranění entity. Díky historii zachycené kvantitativním měřením denních snímků můžete zpětně porovnávat jednotlivé dny mezi sebou.

Práce s dobou života entit může být matoucí, protože entity mění stav. To znamená, že když se podíváte na snímek v třicátý den, nemusí v datech existovat uživatelský záznam v aktivním stavu. Ve dnech 29–28 může existovat záznam entity v aktivním stavu. A před dnem 28 uživatel nemusel vůbec neexistovat.

Tento scénář bude jasnější, když si projdete životnost entity.

Představte si uživatele **Jan Macek**, který získá licenci na 1.6.2017. V tabulce **Uživatel** bude následující položka: 
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| Jan Macek | CHYBNÉ | 1\.6.2017 | 31.12.9999 | PRAVDA
 
Jan Macek vrací licenci 25.7.2017. Tabulka **Uživatel** obsahuje následující položky. Změny v existujících záznamech jsou `marked`. 

| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| Jan Macek | CHYBNÉ | 1\.6.2017 | `07/26/2017` | `FALSE` 
| Jan Macek | PRAVDA | 26.7.2017 | 31.12.9999 | PRAVDA 

První řádek označuje, že Jan Macek existoval v Intune od 1.6.2017 do 25.7.2017. Druhý záznam označuje, že uživatel byl 25.7.2017 odstraněn a již není v Intune k dispozici.

Nyní si představte, že uživatel Jan Macek získá novou licenci dne 31.8.2017. V tabulce Uživatel budou následující položky:
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| Jan Macek | CHYBNÉ | 1\.6.2017 | 26.7.2017 | CHYBNÉ 
| Jan Macek | PRAVDA | 26.7.2017 | `08/31/2017` | `FALSE` 
| Jan Macek | CHYBNÉ | 08/31/2017 | 31.12.9999 | PRAVDA 
 
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
