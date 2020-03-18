---
title: Koncový bod rozhraní API datového skladu Intune
titleSuffix: Microsoft Intune
description: Toto referenční téma popisuje Microsoft Intune strukturu adres URL rozhraní API datového skladu. Jsou k dispozici příklady filtru.
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
ms.assetid: A7A174EC-109D-4BB8-B460-F53AA2D033E6
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 04521681ee6e262f4634cfc96560a5922ce1b8c0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331831"
---
# <a name="intune-data-warehouse-api-endpoint"></a>Koncový bod rozhraní API datového skladu Intune

Rozhraní API datového skladu Intune můžete použít s účtem s řízením přístupu na základě konkrétních rolí a přihlašovacími údaji služby Azure AD. Následně pak provedete autorizaci klienta REST s Azure AD pomocí standardu OAuth 2.0. Nakonec vytvoříte smysluplnou adresu URL pro volání prostředku datového skladu.

[!INCLUDE [reports-credential-reqs](../includes/reports-credential-reqs.md)]

## <a name="authorization"></a>Autorizace

Azure Active Directory (Azure AD) používá standard OAuth 2.0 za účelem umožnění autorizace přístupu k webovým aplikacím a webovým rozhraním API v tenantovi Azure AD. Tato příručka je nezávislá na jazyce a popisuje, jak posílat a přijímat zprávy HTTP bez použití knihoven open-source. Tok autorizačního kódu OAuth 2.0 je popsán v [části 4.1](https://tools.ietf.org/html/rfc6749#section-4.1) specifikace standardu OAuth 2.0.

Další informace najdete v tématu [Autorizace přístupu k webovým aplikacím pomocí OAuth 2.0 a Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code).

## <a name="api-url-structure"></a>Struktura adresy URL rozhraní API

Koncové body rozhraní API datového skladu čtou entity jednotlivých sad. Rozhraní API podporuje příkaz HTTP **GET** a podmnožinu možností dotazu.

Adresa URL pro Intune používá následující formát:  
`https://fef.{location}.manage.microsoft.com/ReportingService/DataWarehouseFEService/{entity-collection}?api-version={api-version}`

> [!NOTE]
> Ve výše uvedené adrese URL nahraďte `{location}`, `{entity-collection}` a `{api-version}` podle informací v tabulce níže.

Adresa URL obsahuje následující prvky:

| Prvek | Příklad | Popis |
|-------------------|------------|--------------------------------------------------------------------------------------------------------------------|
| umístění | msua06 | Základní adresu URL můžete najít zobrazením okna rozhraní API datového skladu na webu Azure Portal. |
| kolekce-entit | devicePropertyHistories | Název kolekce entit OData Další informace o kolekcích a entitách v datovém modelu najdete v tématu [Datový model](reports-ref-data-model.md). |
| verze-api | beta | Verze je verzí rozhraní API, ke kterému přistupujete. Další informace najdete v tématu [Verze](reports-api-url.md#api-version-information). |
| maxhistorydays | 7 | (Volitelné) Maximální počet dní, pro které se načte historie. Tento parametr lze zadat pro jakoukoli kolekci, ale bude mít účinek jenom u kolekcí, jejichž klíčová vlastnost zahrnuje `dateKey`. Další informace najdete v části [Filtry rozsahu DateKey](reports-api-url.md#datekey-range-filters). |

## <a name="api-version-information"></a>Informace o verzi rozhraní API

Nastavením parametru dotazu  `api-version=v1.0` můžete teď používat verzi datového skladu Intune v1.0. Aktualizace kolekcí v datovém skladu mají aditivní povahu a nijak nenarušují existující scénáře.

Nejnovější funkce datového skladu můžete vyzkoušet pomocí beta verze. Pokud chcete použít beta verzi, musí adresa URL obsahovat parametr dotazu  `api-version=beta`. Beta verze nabízí funkce dřív, než budou všeobecně dostupné jako podporované služby. S tím, jak Intune přidává nové funkce, se může měnit chování a kontrakty dat beta verze. Jakýkoli vlastní kód nebo nástroje pro vytváření sestav závislé na beta verzi můžou přestat v probíhajících aktualizacích fungovat.

## <a name="odata-query-options"></a>Možnosti dotazu OData

Aktuální verze podporuje tyto parametry dotazu OData: `$filter`, `$select`, `$skip,` a `$top`. V `$filter`může být podporován pouze `DateKey` nebo `RowLastModifiedDateTimeUTC`, pokud jsou sloupce použity a další vlastnosti budou aktivovat chybný požadavek.

## <a name="datekey-range-filters"></a>Filtry rozsahu DateKey

Filtry rozsahu `DateKey` se dají použít k omezení množství dat ke stažení u některých kolekcí s klíčovou vlastností `dateKey`. Filtr `DateKey` lze použít k optimalizaci výkonu služby tak, že se zadá následující parametr dotazu `$filter`:

1. Samotný prvek `DateKey` v dotazu `$filter`, který podporuje operátory `lt/le/eq/ge/gt` a ke kterému se dá přidat logický operátor `and`, který umožňuje mapování na počáteční nebo koncové datum.
2. `maxhistorydays` se zadá jako vlastní parametr dotazu.<br>

## <a name="filter-examples"></a>Příklady filtrů

> [!NOTE]
> Příklady filtru předpokládají, že dnes je 2/21/2019.

|                             Filtr                             |           Optimalizace výkonu           |                                          Popis                                          |
|:--------------------------------------------------------------:|:--------------------------------------------:|:---------------------------------------------------------------------------------------------:|
|    `maxhistorydays=7`                                            |    Úplný                                      |    Vrátí data s hodnotou `DateKey` mezi 20180214 a 20180221.                                     |
|    `$filter=DateKey eq 20180214`                                 |    Úplný                                      |    Vrátí data s hodnotou `DateKey` rovnající se 20180214.                                                    |
|    `$filter=DateKey ge 20180214 and DateKey lt 20180221`         |    Úplný                                      |    Vrátí data s hodnotou `DateKey` mezi 20180214 a 20180220.                                     |
|    `maxhistorydays=7&$filter=DateKey eq 20180214`                |    Úplný                                      |    Vrátí data s hodnotou `DateKey` rovnající se 20180214. `maxhistorydays` se ignoruje.                            |
|    `$filter=RowLastModifiedDateTimeUTC ge 2018-02-21T23:18:51.3277273Z`                                |    Úplný                                       |    Vrácení dat pomocí `RowLastModifiedDateTimeUTC` je větší nebo rovno `2018-02-21T23:18:51.3277273Z`                             |
