---
title: Vytvoření vlastní role v Intune
description: Naučte se, jak vytvořit vlastní roli v Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 07c29f45c2d9356bda78e021d3baf9647aa03397
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326796"
---
# <a name="create-a-custom-role-in-intune"></a>Vytvoření vlastní role v Intune

Můžete vytvořit vlastní roli Intune, která bude obsahovat všechna oprávnění požadovaná pro konkrétní pracovní funkci. Pokud například skupina oddělení IT spravuje aplikace, zásady a profily konfigurace, můžete všechna tato oprávnění přidat společně v jedné vlastní roli. Po vytvoření vlastní role ji můžete [přiřadit](assign-role.md) všem uživatelům, kteří tato oprávnění potřebují.

Abyste mohli vytvářet, upravovat nebo přiřazovat role, váš účet musí mít ve službě Azure AD jedno z těchto oprávnění:
- **Globální správce**
- **Správce služby Intune**

## <a name="to-create-a-custom-role"></a>Jak vytvořit vlastní roli

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte možnost **Správa tenanta** > **role** > **všechny role** > **vytvořit**.

2. Na stránce **základy** zadejte název a popis nové role a pak zvolte **Další**.

3. Na stránce **oprávnění** vyberte oprávnění, která chcete u této role použít.

4. Na stránce **obor (značky)** vyberte značky pro tuto roli. Tato role má přístup k prostředkům, které mají také tyto značky. Vyberte **Další**.

5. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nová role se zobrazí v seznamu v okně **role Intune – všechny role** .

## <a name="copy-a-role"></a>Kopírovat roli

Můžete také zkopírovat existující roli.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)zvolte **Správa tenanta** > **role** > **všechny role** > zaškrtněte políčko u role v seznamu > **duplikujte**.

2. Na stránce **základy** zadejte název. Ujistěte se, že používáte jedinečný název.

3. Všechna oprávnění a značky oboru z původní role budou již vybrány. Následně můžete změnit **název**, **Popis**, **oprávnění**a obor duplicitní role **(značky)** .

4. Až provedete všechny požadované změny, klikněte na tlačítko **Další** a dostanete se na stránku **Kontrola a vytvoření** . Vyberte **Vytvořit**. 

## <a name="next-steps"></a>Další kroky
- [Přiřazení role uživateli](assign-role.md)
- [Další informace o řízení přístupu na základě role v Intune](role-based-access-control.md)


