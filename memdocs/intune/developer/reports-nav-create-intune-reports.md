---
title: Použití datového skladu Intune
titleSuffix: Microsoft Intune
description: Datový sklad Intune můžete používat k vytváření sestav poskytujících přehled o podnikovém mobilním prostředí.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/28/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 57019B11-DF9B-4D8A-95FE-254C75398DDE
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84fe1afcf04c6b3771d1541ad0488a95b9313dca
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908832"
---
# <a name="use-the-microsoft-intune-data-warehouse"></a>Použití datového skladu Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Datový sklad Intune můžete používat k vytváření sestav poskytujících přehled o podnikovém mobilním prostředí. Některé z těchto sestav například obsahují:
- Trend uživatelů registrujících se v Intune, který vám umožní optimalizovat nákupy licencí
- Rozpis verzí aplikací a operačních systémů, abyste mohli kontrolovat stav mobilních zařízení
- Trendy registrace a dodržování předpisů zařízeními, abyste mohli plynule zavést aktualizace zásad

## <a name="data-warehouse-benefits"></a>Výhody datového skladu

Datový sklad poskytuje přístup k více informacím týkajícím se vašeho mobilního prostředí než web Azure Portal. Datový sklad Intune vám umožňuje přistupovat k:

- Historickým datům Intune
- Datům aktualizovaným na denní bázi
- Datovému modelu používajícímu standard OData

> [!Note]
> Pokud používáte spoluspravovanou správu mobilních zařízení (MDM) se službou Microsoft Endpoint Configuration Manager a Microsoft Intune, je nutné načíst data z Configuration Manager. Datový sklad Intune obsahuje jenom data Intune. Pro vlastní sestavy můžete použít řídicí panel Configuration Manager Power BI. Další informace najdete v tématu o[oznámení Power BI šablony řešení pro Configuration Manager](https://powerbi.microsoft.com/blog/sccm-solution-template)a[Power BI obsahu pro Dynamics 365](/dynamics365/unified-operations/dev-itpro/analytics/power-bi-home-page).

> [!Important]  
> Nastavením parametru dotazu  `api-version=v1.0` můžete teď používat verzi datového skladu Intune v1.0. Aktualizace kolekcí v datovém skladu mají aditivní povahu a nijak nenarušují existující scénáře.<br><br>
> Nejnovější funkce datového skladu můžete vyzkoušet pomocí beta verze. Pokud chcete použít beta verzi, musí adresa URL obsahovat parametr dotazu  `api-version=beta`. Beta verze nabízí funkce dřív, než budou všeobecně dostupné jako podporované služby. S tím, jak Intune přidává nové funkce, se může měnit chování a kontrakty dat beta verze. Jakýkoli vlastní kód nebo nástroje pro vytváření sestav závislé na beta verzi můžou přestat v probíhajících aktualizacích fungovat.

## <a name="next-steps"></a>Další kroky

- Získejte odkaz a použijte Power BI k získání přehledu. Pokyny najdete v tématu [Připojení k datovému skladu Intune pomocí Power BI](reports-proc-get-a-link-powerbi.md).
- S odkazem vytvořte vlastní sestavu pomocí Power BI. Pokyny najdete v článku [Vytvoření sestavy z datového kanálu OData pomocí Power BI](reports-proc-create-with-odata.md).
- Získejte další informace o rozhraní API datového skladu Intune, datovém modelu a relacích mezi entitami.<!-- , and an example of creating a custom client to retrieve data,--> viz [rozhraní API datového skladu Intune](reports-nav-intune-data-warehouse.md).