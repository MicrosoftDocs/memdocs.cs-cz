---
title: Nastavení podmínek a ujednání v Microsoft Intune
titleSuffix: ''
description: Nastavte si podmínky a ujednání, které uvidí uživatelé na Portálu společnosti pro Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/20/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4a3a11a8-9c0c-4334-8c6b-6fea4d0a2efb
ms.reviewer: amyro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26c30c947c6db1d44d8438aa63972fd5a3f663cd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332815"
---
# <a name="terms-and-conditions-for-user-access"></a>Podmínky a ujednání pro přístup uživatelů

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Správce Intune může uživatele požádat, aby před použitím Portálu společnosti přijali podmínky a ujednání společnosti, aby mohli:
- registrovat zařízení,
- přistupovat k prostředkům, jako jsou aplikace a e-mail společnosti.

Konfigurace podmínek a ujednání je volitelná.

Můžete vytvořit více sad podmínek a přiřadit je různým skupinám, abyste například zajistili podporu různých jazyků.

Existují dva způsoby, jak vytvořit podmínky a ujednání společnosti:
- Můžete použít Intune spolu s postupem, který je popsaný v tomto článku.
- pomocí [funkce Azure Active Directory podmínek použití](https://docs.microsoft.com/azure/active-directory/governance/active-directory-tou)

Pokud chcete zjistit, která metoda je pro vás nejvhodnější, přečtěte si [Výběr správného pojmu řešení pro váš Blogový příspěvek vaší organizace](https://go.microsoft.com/fwlink/?linkid=2010506&clcid=0x409). 

## <a name="create-terms-and-conditions"></a>Vytvoření podmínek a ujednání
Pokud chcete vytvořit podmínky a ujednání, dokončete tento postup. Zobrazovaný název a popis jsou určené pro správu, zatímco vlastnosti podmínek se zobrazují uživatelům na Portálu společnosti.

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte možnost **Správa tenanta** > **podmínky a ujednání**.
2. Zvolte **Vytvořit**.
3. Na stránce **základy** zadejte následující informace:

   - **Name**(název): název podmínek v Azure Portal. Tento název se uživatelům nezobrazuje.
   - **Popis**: Volitelné podrobnosti, které vám pomůžou identifikovat tuto sadu podmínek na Azure Portalu.

    ![Snímek obrazovky Azure Portal zobrazující stránku základy pro podmínky a ujednání](./media/terms-and-conditions-create/terms-basics-page.png)

4. Kliknutím na tlačítko **Další** přejdete na stránku **podmínek** a zadáte následující informace:

   - **Nadpis**: Název vašich podmínek, který uživatelé uvidí na Portálu společnosti nad **Souhrnem**.
   - **Podmínky**: Podmínky, které se zobrazí uživatelům a které musí uživatelé přijmout nebo odmítnout.
   - **Souhrn podmínek**: Text, který vysvětluje, jaký význam má pro uživatele přijetí podmínek. Příklad: „Registrací svého zařízení souhlasíte s podmínkami použití stanovenými společností Contoso. Než budete pokračovat, pečlivě si podmínky prostudujte.“

5. Kliknutím na tlačítko **Další** přejdete na stránku **značky oboru** .

6. Zvolte **možnost vybrat značky oboru**, vyberte značky oboru, které chcete přiřadit těmto podmínkám a podmínkám, a pak zvolte **Vybrat**. 

7. Kliknutím na tlačítko **Další** přejdete na stránku **přiřazení** a vyberte jednu z následujících možností pro **přiřazení k**:
    - **Všichni uživatelé**: tuto možnost vyberte, pokud chcete přiřadit podmínky a ujednání všem uživatelům.
    - **Vybrat skupiny**: tuto možnost vyberte, pokud chcete, aby se tyto podmínky a ujednání přiřadily všem uživatelům ve skupinách, které identifikujete výběrem možnosti **Vybrat skupiny, které se mají zahrnout**.

8. Klikněte na tlačítko **další** > **vytvořit**.

## <a name="see-how-terms-are-displayed-to-your-users"></a>Prohlížení podmínek, jak se zobrazují uživatelům
V následujícím příkladu je vidět **Nadpis** a **Souhrn podmínek** v konzole pro správu a na Portálu společnosti.

![Snímek obrazovky s nadpisem a souhrnem podmínek v konzole pro správu a na Portálu společnosti](./media/terms-and-conditions-create/terms-summary-terms.png)

V následujícím příkladu jsou vidět podmínky a ujednání v konzole pro správu a na Portálu společnosti.

![Snímek obrazovky s podmínkami a ujednáními v konzole pro správu a na Portálu společnosti](./media/terms-and-conditions-create/terms-properties-terms.png)


## <a name="monitor-terms-and-conditions"></a>Monitorování podmínek a ujednání

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte možnost **Správa tenanta** > **podmínky a ujednání**.
2. V seznamu podmínek a ujednání zvolte podmínky, u kterých chcete zobrazit jejich přijetí > **Generování sestav o přijetí**.

## <a name="work-with-multiple-versions-of-terms-and-conditions"></a>Práce s více verzemi podmínek a ujednání
Podmínky a ujednání můžete upravit a spravovat jejich verze. Po každé významnější změně podmínek a ujednání byste měli:
- Zvýšit číslo verze.
- vyžadovat, aby uživatelé přijali nové podmínky a ujednání

Aktuální číslo verze nechejte, pokud například opravujete překlepy nebo měníte formátování.

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte možnost **Správa tenanta** > **podmínky a ujednání** > vyberte podmínky a ujednání, které chcete upravit > **vlastnosti**.

2. V podokně **Vlastnosti** zvolte **Podmínky** a podle potřeby změňte **Nadpis**, **Souhrn podmínek** a **Podmínky**. Pokud je potřeba, aby provedené změny uživatelé znovu přijali jako nové podmínky, zvolte **Požaduje opětovné přijetí od uživatelů a zvýší číslo verze na**.

3. Zvolte **OK** > **Uložit**.

Uživatelé musí přijmout aktualizované podmínky a ujednání jenom jednou. Uživatelé, kteří mají několik zařízení, je nemusejí přijímat na každém z nich.
