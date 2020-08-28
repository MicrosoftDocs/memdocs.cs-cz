---
title: Vytvoření zásady dodržování předpisů pro zařízení MTD (Mobile Threat obrany) pomocí Microsoft Intune
titleSuffix: Microsoft Intune
description: Vytvořte zásady dodržování předpisů zařízením v Intune, které využívají úrovně hrozby partnerů MTD k určení, jestli má mobilní zařízení přístup k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
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
ms.openlocfilehash: 265b92229d687c7dafb2c6de196990c29ffc0cb8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996091"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Vytvoření zásad dodržování předpisů pro ochranu zařízení před mobilními hrozbami (MTD) v Intune

Intune s MTD vám pomůže odhalit hrozby a posoudit rizika u mobilních zařízení. Můžete vytvořit pravidlo zásad dodržování předpisů zařízení služby Intune, které posuzuje rizika a zjišťuje, jestli zařízení předpisy dodržuje, nebo ne. Pak můžete pomocí [zásad podmíněného přístupu](create-conditional-access-intune.md) zablokovat přístup ke službám na základě dodržování předpisů zařízením.

> [!NOTE]
> Tyto informace se týkají všech partnerů ochrany před mobilními hrozbami.

## <a name="before-you-begin"></a>Než začnete

V rámci nastavení ochrany před mobilními hrozbami (MTD) jste v konzole partnera MTD vytvořili zásadu, která klasifikuje různé hrozby jako vysoké, střední nebo nízké. Dále nastavíte úroveň ochrany před mobilními hrozbami v zásadách dodržování předpisů pro zařízení v Intune.

Předpoklady zásad dodržování předpisů zařízením pro MTD:

- Nastavení integrace MTD se službou Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>Vytvoření zásad dodržování předpisů zařízením pro MTD

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint Security**  >  **dodržování předpisů pro zařízení**  >  **zásady vytvořit zásadu**.

3. Vyberte **platformu**a pak **vytvořte**.

4. V **základních**informacích zadejte **název**zásad dodržování předpisů pro zařízení a **Popis** (volitelné). Pokračujte výběrem tlačítka **Další**.


5. V **Nastavení dodržování předpisů**rozbalte a nakonfigurujte **stav zařízení**. V rozevíracím seznamu vyberte úroveň mobilní hrozby, **která vyžaduje, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod**ní.

   - **Zabezpečeno:** Tato úroveň poskytuje nejvyšší zabezpečení. Zařízení nemůže mít k dispozici žádné hrozby a bude mít přístup k prostředkům společnosti. Pokud se najde jakákoli hrozba, zařízení se vyhodnotí jako nevyhovující.

   - **Nízká:** Zařízení se vyhodnotí jako vyhovující i v případě, že se v něm nachází jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.

   - **Střední:** Zařízení vyhovuje, pokud se v něm přítomné hrozby pohybují na střední nebo nízké úrovni. Pokud se v zařízení zjistí hrozby vysoké úrovně, vyhodnotí se jako nevyhovující.

   - **Vysoká**: Tato úroveň hrozeb je nejméně zabezpečená, protože umožňuje všechny úrovně hrozeb a používá ochranu před mobilními hrozbami jenom pro účely vytváření sestav. Při tomto nastavení musejí mít zařízení aplikaci pro ochranu před mobilními hrozbami aktivovanou.

6. Pokud chcete pokračovat v **přiřazení**, vyberte **Další** . Vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

   Vyberte **Další**.

7. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

> [!IMPORTANT]
> Pokud vytvoříte zásady podmíněného přístupu pro Microsoft 365 nebo jiné služby, vyhodnotí se hodnocení dodržování předpisů zařízením a zařízení, která nedodržují předpisy, budou mít zablokovaný přístup k podnikovým prostředkům, dokud se hrozby v zařízení nevyřeší.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Přiřazení zásad dodržování předpisů zařízením pro MTD

Chcete-li přiřadit nebo změnit přiřazení zásady dodržování předpisů zařízením pro uživatele:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint security**  >  **dodržování předpisů zařízením**v zabezpečení koncového bodu.

3. Vyberte zásadu, kterou chcete přiřadit uživatelům, a pak vyberte **vlastnosti**.

4. Vyberte **Upravit** pro přiřazení a pak použijte dostupné možnosti k *zahrnutí* a *vyloučení* skupin pro příjem těchto zásad.  

5. Kliknutím na tlačítko **Revize + Uložit** dokončete přiřazení. Při uložení přiřazení se zásada nasadí vybraným uživatelům a jejich zařízení se vyhodnotí jako dodržování předpisů.

## <a name="next-steps"></a>Další kroky

[Povolení MTD v Intune](mtd-connector-enable.md)
