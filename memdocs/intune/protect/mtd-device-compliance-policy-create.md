---
title: Vytvoření zásad dodržování předpisů pro ochranu zařízení před mobilními hrozbami (MTD) v Microsoft Intune
titleSuffix: Microsoft Intune
description: Vytvořte zásady dodržování předpisů zařízením v Intune, které využívají úrovně hrozby partnerů MTD k určení, jestli má mobilní zařízení přístup k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e05577967d874ea8e3cd5e4bdd5e20e204158921
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325442"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Vytvoření zásad dodržování předpisů pro ochranu zařízení před mobilními hrozbami (MTD) v Intune

Intune s MTD vám pomůže odhalit hrozby a posoudit rizika u mobilních zařízení. Můžete vytvořit pravidlo zásad dodržování předpisů zařízení služby Intune, které posuzuje rizika a zjišťuje, jestli zařízení předpisy dodržuje, nebo ne. Pak můžete pomocí [zásad podmíněného přístupu](create-conditional-access-intune.md) zablokovat přístup ke službám na základě dodržování předpisů zařízením.

> [!NOTE]
> Tyto informace se týkají všech partnerů ochrany před mobilními hrozbami.

## <a name="before-you-begin"></a>Před zahájením

V rámci nastavení ochrany před mobilními hrozbami (MTD) jste v konzole partnera MTD vytvořili zásadu, která klasifikuje různé hrozby jako vysoké, střední nebo nízké. V zásadách dodržování předpisů zařízením služby Intune je teď potřeba nastavit úroveň ochrany zařízení před mobilními hrozbami.

Předpoklady zásad dodržování předpisů zařízením pro MTD:

- Nastavení integrace MTD se službou Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>Vytvoření zásad dodržování předpisů zařízením pro MTD

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **zásady dodržování předpisů** > **vytvořit zásadu**.

3. Zadejte **název**zásady dodržování předpisů pro zařízení, **Popis**, vyberte **platformu**a potom v části **Nastavení** vyberte **Konfigurovat** .

4. V podokně **zásad dodržování předpisů** zvolte **Stav zařízení**.

5. V podokně **stav zařízení** v rozevíracím seznamu vyberte úroveň mobilní hrozby, **která vyžaduje, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod**ní.

   - **Zabezpečeno:** Tato úroveň poskytuje nejvyšší zabezpečení. Zařízení nemůže přistupovat k prostředkům společnosti, pokud je vystavené nějakým hrozbám. Pokud se najde jakákoli hrozba, zařízení se vyhodnotí jako nevyhovující.

   - **Nízká:** Zařízení se vyhodnotí jako vyhovující i v případě, že se v něm nachází jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.

   - **Střední:** Zařízení vyhovuje, pokud se v něm přítomné hrozby pohybují na střední nebo nízké úrovni. Pokud se v zařízení zjistí hrozby vysoké úrovně, vyhodnotí se jako nevyhovující.

   - **Vysoká:** Tato úroveň poskytuje nejnižší zabezpečení. Tato možnost povoluje všechny úrovně hrozeb, protože používá ochranu před mobilními hrozbami jenom ke generování sestav. Při tomto nastavení musejí mít zařízení aplikaci pro ochranu před mobilními hrozbami aktivovanou.

6. Dvakrát klikněte na **OK** a pak vyberte **vytvořit** a vytvořte zásadu.

> [!IMPORTANT]
> Pokud vytvoříte zásady podmíněného přístupu pro Office 365 nebo jiné služby, vyhodnotí se hodnocení dodržování předpisů zařízením a zařízení, která nedodržují předpisy, budou mít zablokovaný přístup k prostředkům společnosti, dokud se hrozby v zařízení nevyřeší.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Přiřazení zásad dodržování předpisů zařízením pro MTD

Postup přiřazení zásad dodržování předpisů zařízením uživatelům:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **zásady dodržování předpisů**.

3. Vyberte zásadu, kterou chcete přiřadit uživatelům, a pak vyberte **přiřazení**. Pomocí dostupných možností můžete *Zahrnout* a *vyloučit* skupiny pro příjem těchto zásad.  

4. Kliknutím na Uložit dokončete přiřazení. Při uložení přiřazení se zásada nasadí vybraným uživatelům a jejich zařízení se vyhodnotí jako dodržování předpisů.

## <a name="next-steps"></a>Další kroky

[Povolení MTD v Intune](mtd-connector-enable.md)
