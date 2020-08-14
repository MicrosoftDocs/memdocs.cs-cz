---
title: Přidání aplikací pro App Store (iOS) do Microsoft Intune
titleSuffix: ''
description: Zjistěte, jak do Microsoft Intune přidat aplikace z obchodu pro iOS. Pomocí této metody můžete přiřadit aplikace, pokud jsou aplikace zdarma v App Storu.
keywords: Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c59514d7-1256-4576-9380-e7a0b85a0378
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe19721210b4221e4e86394be0a4e3663a9f0b77
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217280"
---
# <a name="add-ios-store-apps-to-microsoft-intune"></a>Přidání aplikací pro App Store (iOS) do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Informace v tomto článku vám pomůžou přidat do Intune aplikace z obchodu pro iOS. Aplikace z App Storu (iOS) jsou aplikace, které Intune instaluje na zařízení uživatelů. Uživatel je jeden ze zaměstnanců společnosti. Aplikace z obchodu pro iOS se automaticky aktualizují.

>[!NOTE]
>I když uživatelé zařízení se systémem iOS/iPadOS můžou odebrat některé integrované aplikace pro iOS/iPadOS, jako jsou například akcie a mapy, nemůžete tyto aplikace znovu nasadit pomocí Intune. Pokud uživatel tyto aplikace odstraní, musí si je znovu ručně nainstalovat z App Storu.

## <a name="before-you-start"></a>Než začnete

Pomocí této metody můžete aplikace přiřazovat jen v případě, že jsou v App Storu bezplatné. Pokud chcete přiřadit placené aplikace pomocí Intune, zvažte použití [programu Volume purchase pro iOS/iPadOS](vpp-apps-ios.md).

>[!NOTE]
>Při práci s Microsoft Intune doporučujeme používat prohlížeč Microsoft Edge nebo Google Chrome.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části dostupné typy **aplikací pro Store** vyberte aplikace pro **iOS Store**.
4. Klikněte na **Vybrat**.<br>
   Zobrazí se kroky **Přidání aplikace** .
5. Vyberte **Hledat v App Storu**.
6. V podokně **Hledat v App Storu** vyberte národní prostředí pro zemi nebo oblast obchodu App Store.
7. Do **vyhledávacího** pole zadejte název (nebo část názvu) aplikace.  
    Intune prohledá Store a vrátí seznam relevantních výsledků.
8. V seznamu výsledků vyberte požadovanou aplikaci a pak vyberte **Vybrat**.<br>

   Stránka **informace o aplikaci** se zobrazí v podokně **Přidat aplikaci** . Pokud je to možné, budou informace o aplikaci přidány na základě aplikace, kterou jste vybrali ze Storu.

9. Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci. V závislosti na zvolené aplikaci můžou být některé hodnoty v tomto podokně vyplněné automaticky:
    - **Název**: Zadejte název aplikace, který se zobrazí na Portálu společnosti. Ujistěte se, že používaný název aplikace je jedinečný. Pokud je název aplikace duplicitní, zobrazí se uživatelům na Portálu společnosti pouze jeden název.
    - **Popis**: Zadejte popis aplikace. Tento popis se uživatelům zobrazí na Portálu společnosti.
    - **Vydavatel**: zadejte název vydavatele aplikace.
    - **Adresa URL v obchodu s aplikacemi**: Zadejte adresu URL v obchodu s aplikacemi pro aplikaci, kterou chcete vytvořit.
    - **Minimální operační systém**: V seznamu vyberte nejstarší verzi operačního systému, na kterou je možné aplikaci nainstalovat. Pokud aplikaci přiřadíte k zařízení se starším operačním systémem, nenainstaluje se.
    - **Použitelný typ zařízení**: V seznamu vyberte zařízení, která aplikace používá.
    - **Kategorie**: Volitelně můžete vybrat jednu nebo několik předdefinovaných kategorií aplikací nebo kategorii, kterou jste vytvořili. Uživatelé tak při procházení Portálu společnosti najdou aplikaci snadněji.
    - **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se sada aplikací zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Vývojář**: Volitelně zadejte jméno vývojáře aplikace. Toto pole je viditelné jen pro správce, uživatelé ho nevidí.
    - **Vlastník**: Volitelně zadejte vlastníka aplikace, například *Personální oddělení*. Toto pole je viditelné jen pro správce, uživatelé ho nevidí.
    - **Poznámky**: Volitelně zadejte jakékoli poznámky, které chcete k aplikaci přidružit. Toto pole vidí jenom správce a koncoví uživatelé je neuvidí.
    - **Logo**: Volitelně nahrajte ikonu, která se přidruží k aplikaci. Tato ikona se u aplikace zobrazí, když uživatelé procházejí portál společnosti.
10. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .
11. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro aplikaci. Další informace najdete v tématu [použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci](../fundamentals/scope-tags.md).
12. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
13. Vyberte přiřazení skupin pro aplikaci. Další informace najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md). 
14. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** . Zkontrolujte hodnoty a nastavení, které jste zadali pro aplikaci.
15. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

Zobrazí se okno **Přehled** aplikace, kterou jste vytvořili.

## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací skupinám](apps-deploy.md)
