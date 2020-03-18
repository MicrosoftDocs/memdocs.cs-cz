---
title: Rychlý start – vytvoření a přiřazení zásady ochrany aplikací
titleSuffix: Microsoft Intune
description: V tomto rychlém startu použijete Microsoft Intune k vytvoření a přiřazení zásady ochrany aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2586fce0-5dca-4686-b9c4-791778838401
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb8b5eae3c88664caff76da597fc3ab9111f989c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326791"
---
# <a name="quickstart-create-and-assign-an-app-protection-policy"></a>Rychlý start: Vytvoření a přiřazení zásady ochrany aplikací

V tomto rychlém startu použijete Intune k vytvoření a přiřazení zásady ochrany aplikací ke klientské aplikaci na zařízení koncového uživatele. Intune používá zásady ochrany aplikací k potvrzení, že vaše aplikace vyhovují požadavkům na ochranu dat vaší organizace.

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky

- Abyste dokončili tento rychlý start, musíte [vytvořit uživatele](../fundamentals/quickstart-create-user.md), [vytvořit skupinu](../fundamentals/quickstart-create-group.md), [zaregistrovat zařízení](../enrollment/quickstart-setup-auto-enrollment.md) a [přidat a přiřadit aplikaci](quickstart-add-assign-app.md).

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

Přihlaste se k [Intune](https://aka.ms/intuneportal) jako [globální správce nebo jako správce služby Intune](../fundamentals/users-add.md#types-of-administrators). Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="create-an-app-protection-policy"></a>Vytvoření zásady ochrany aplikací

Zásady ochrany aplikací vytvoříte pomocí následujících kroků:

1. V [Intune](https://aka.ms/intuneportal)vyberte **aplikace** > **Zásady ochrany aplikací** > **vytvořit zásadu**. 
2. Zadejte následující podrobnosti:

    - **Název:** *Ochrana obsahu pro Windows 10*
    - **Popis:** *Uživatelé přidružení k této zásadě nebudou moci vyjímat, kopírovat ani vkládat žádný obsah mezi přiřazenou aplikací a jinými nespravovanými aplikacemi v zařízení.*
    - **Platforma:** *Windows 10*
    - **Stav registrace:** *S registrací*

3. Vyberte **Chráněné aplikace** a zvolte aplikace, které musí tuto zásadu dodržovat.
4. Klikněte na **Přidat aplikace**.
5. V oblasti **Doporučené aplikace** vyberte **Word Mobile**.
5. Klikněte na **OK** > **OK**. 
6. Vyberte **Požadovaná nastavení** a nakonfigurujte tuto aplikaci.
7. Kliknutím na **Povolit potlačení** nastavte režim Windows Information Protection. Výběr této možnosti znemožní únik podnikových dat z chráněné aplikace.
8. Klikněte na **OK** > **Vytvořit**.

V Intune se teď zobrazí zásady ochrany aplikací.

### <a name="assign-the-app-protection-policy"></a>Přiřazení zásady ochrany aplikací

Po vytvoření zásady ochrany aplikací v Intune ji můžete přiřadit ke skupinám. 

K přiřazení zásady ochrany aplikací použijte následující postup:

1. V [Intune](https://aka.ms/intuneportal)vyberte **Intune** > **aplikace** > **Zásady ochrany aplikací**. 
2. Vyberte dříve vytvořenou zásadu ochrany aplikací. V tomto rychlém startu je to zásada **Ochrana obsahu pro Windows 10**.
3. Zvolte **Přiřazení**.
4. Na kartě **Zahrnout** klikněte na **Vybrat skupiny, které se zahrnou**.
5. Jako skupinu, která se zahrne, vyberte **Testeři Contoso**.
6. Klikněte na **vybrat** > **Uložit**. 

Právě jste přiřadili zásadu ochrany aplikací.

> [!NOTE]
> Zásady ochrany aplikací je možné použít jen u skupin, které obsahují uživatele, nikoli u skupin, které obsahují zařízení.

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste vytvořili a přiřadili zásadu ochrany aplikací. Uživatelé aplikace, ke které je přiřazená tato zásada, nebudou moci vyjímat, kopírovat ani vkládat žádný obsah mezi přiřazenou aplikací a jinými nespravovanými aplikacemi v zařízení. Tento typ ochrany bude pomáhat chránit data vaší organizace. Další informace o zásadách ochrany aplikací v Intune najdete v článku [Co jsou zásady ochrany aplikací?](app-protection-policy.md)

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Vytvoření a přiřazení vlastní role](../fundamentals/create-custom-role.md)
