---
title: Přidání aplikací pro Windows Phone 8.1 ze Storu do Microsoft Intune
titleSuffix: ''
description: Toto téma popisuje, jak přidat aplikace Windows Phone 8,1 Storu do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4a95e575-2c63-4bfc-b9c4-f0a132eef618
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26baded3ebf12b770d8e1a70a3ab9251381afa03
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987866"
---
# <a name="add-windows-phone-81-store-apps-to-microsoft-intune"></a>Přidání aplikací pro Windows Phone 8.1 ze Storu do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Před přiřazením aplikace k zařízení nebo skupině uživatelů je nejprve potřeba danou aplikaci přidat do Microsoft Intune. 

## <a name="add-an-app-to-intune"></a>Přidání aplikace do Intune
Aplikaci pro Windows Phone 8.1. ze Storu můžete přidat do Intune z portálu Azure Portal následujícím postupem:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části dostupné typy **aplikací pro store** vyberte **Windows Phone 8,1 Store app**.
4. Klikněte na **Vybrat**.<br>
   Zobrazí se kroky **Přidání aplikace** .
5. Pokud chcete nakonfigurovat **informace o aplikaci** pro aplikace Windows Phone 8,1 Store, přejděte do [Microsoft Storu](https://www.microsoft.com/store/apps/windows-phone) a vyhledejte aplikaci, kterou chcete nasadit. Zobrazte stránku aplikace a poznamenejte si podrobnosti o aplikaci. 
6. Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci:
    - **Název**: Zadejte název aplikace, který se zobrazí na Portálu společnosti. Ujistěte se, že používaný název aplikace je jedinečný. Pokud je název aplikace duplicitní, zobrazí se uživatelům na Portálu společnosti pouze jeden název.
    - **Popis**: Zadejte popis aplikace. Tento popis se uživatelům zobrazí na Portálu společnosti.
    - **Vydavatel**: zadejte název vydavatele aplikace.
    - **Adresa URL v obchodu s aplikacemi**: Zadejte adresu URL v obchodu s aplikacemi pro aplikaci, kterou chcete vytvořit.
    - **Kategorie**: Volitelně můžete vybrat jednu nebo několik předdefinovaných kategorií aplikací nebo kategorii, kterou jste vytvořili. Uživatelé tak při procházení Portálu společnosti najdou aplikaci snadněji.
    - **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se sada aplikací zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Vývojář**: Volitelně zadejte jméno vývojáře aplikace.
    - **Vlastník**: Volitelně zadejte vlastníka aplikace, například *Personální oddělení*.
    - **Poznámky**: Volitelně zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
    - **Logo**: Volitelně nahrajte ikonu, která se přidruží k aplikaci. Tato ikona se u aplikace zobrazí, když uživatelé procházejí portál společnosti.
7. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .
8. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro aplikaci. Další informace najdete v tématu [použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci](../fundamentals/scope-tags.md).
9. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
10. Vyberte přiřazení skupin pro aplikaci. Další informace najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md). 
11. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** . Zkontrolujte hodnoty a nastavení, které jste zadali pro aplikaci.
12. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

Zobrazí se okno **Přehled** aplikace, kterou jste vytvořili.


Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřazovat vybraným skupinám.

## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací skupinám](apps-deploy.md)
