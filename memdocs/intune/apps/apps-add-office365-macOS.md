---
title: Instalace Office 365 na zařízení s macOS pomocí Microsoft Intune
titleSuffix: ''
description: Zjistěte, jak můžete využít Microsoft Intune k instalaci aplikací Office 365 na zařízení s macOS.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2372332a-7e3a-4a9c-91a9-86654e0fabe2
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1633900e77eedce0bcca477173e647f5d35b1ee8
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326027"
---
# <a name="assign-office-365-to-macos-devices-with-microsoft-intune"></a>Přiřazení Office 365 zařízením s macOS v Microsoft Intune

Tento typ aplikace usnadňuje přiřazení aplikací Office 365 2016 zařízením s macOS. Pomocí tohoto typu aplikace nainstalujete Word, Excel, PowerPoint, Outlook a OneNote. Tyto aplikace jsou dodávané prostřednictvím funkce Microsoft AutoUpdate (MAU). Je to kvůli jejich zabezpečení a aktuálnosti. Požadované aplikace se v seznamu aplikací v konzole Intune zobrazí jako jedna aplikace.


## <a name="before-you-start"></a>Než začnete

Než začnete přidávat Office 365 do zařízení s macOS, seznamte se s těmito podrobnostmi:

- Zařízení, na která tyto aplikace budete nasazovat, musí mít macOS 10.10 nebo novější.
- Intune umožňuje přidat jenom aplikace Office, které jsou součástí sady Office 2016 pro Mac.
- Pokud jsou při instalaci sady aplikací službou Intune spuštěné nějaké aplikace Office, můžou uživatelé přijít o data z neuložených souborů.

## <a name="select-the-office-365-suite-app-type"></a>Vyberte typ aplikace Office 365 Suite.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V části sada **Office 365** v podokně **Vybrat typ aplikace** vyberte **MacOS** .
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidat sadu Office 365** .

## <a name="step-1---app-suite-information"></a>Krok 1 – informace o sadě aplikací

V tomto kroku zadáte informace o sadě aplikací. Tyto informace vám pomůžou sadu aplikací identifikovat v Intune a uživatelům ji pomůžou najít na portálu společnosti.

1. Na stránce **informace o sadě aplikací** můžete potvrdit nebo upravit výchozí hodnoty:
    - **Název sady**: Zadejte název sady aplikací, který se zobrazí na portálu společnosti. Názvy všech používaných sad musí být jedinečné. Pokud stejný název sady aplikací existuje dvakrát, zobrazí se na portálu společnosti uživatelům jenom jedna z aplikací.
    - **Popis sady**: Zadejte popis sady aplikací. Můžete například uvést aplikace, které jste vybrali pro zahrnutí.
    - **Vydavatel**: Jako vydavatel se zobrazí Microsoft.
    - **Kategorie**: Můžete vybrat jednu nebo několik předdefinovaných kategorií nebo kategorii, kterou jste vytvořili. Díky tomuto nastavení uživatelé dokážou sadu aplikací při procházení portálu společnosti jednodušeji najít.
    - **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se sada aplikací zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Vývojář**: Jako vývojář se zobrazí Microsoft.
    - **Vlastník**: Jako vlastník se zobrazí Microsoft.
    - **Poznámky**: Zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
    - **Logo**: Logo Office 365 se zobrazí u aplikace, když uživatelé procházejí Portál společnosti.
2. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .

## <a name="step-2---select-scope-tags-optional"></a>Krok 2 – výběr značek oboru (volitelné)
Pomocí značek Scope můžete určit, kdo může v Intune zobrazit informace o klientské aplikaci. Úplné podrobnosti o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).

1. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro sadu aplikací. 
2. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .

## <a name="step-3---assignments"></a>Krok 3 – přiřazení

1. Vyberte **požadované** nebo dostupné přiřazení skupin **zaregistrovaných zařízení** pro sadu aplikací. Další informace najdete v tématech [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md) a [přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).

    >[!Note]
    > Sadu Office 365 pro sadu aplikací macOS nemůžete odinstalovat přes Intune.

2. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** . 

## <a name="step-4---review--create"></a>Krok 4 – přezkoumání a vytvoření

1. Zkontrolujte hodnoty a nastavení, které jste zadali pro sadu aplikací.
2. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

    Zobrazí se okno s **přehledem** sady aplikací Office 365 Window 10, kterou jste vytvořili. Sada se zobrazí v seznamu aplikací jako jedna položka.

## <a name="next-steps"></a>Další kroky

- Další informace o přidání aplikací Office 365 do zařízení s Windows 10 najdete v článku [Přiřazení aplikací Office 365 ProPlus 2016 k zařízením s Windows 10 pomocí Microsoft Intune](apps-add-office365.md).
- Informace o zahrnutí a vyloučení přiřazení aplikací ze skupin uživatelů najdete v článku [Zahrnutí a vyloučení přiřazení aplikací](apps-inc-exl-assignments.md).
