---
title: 'Rychlý start: Vytvoření a přiřazení vlastní role v Intune'
description: 'Rychlý start: Vytvoření a přiřazení vlastní role pro správce vzdáleného zařízení'
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 03/26/2019
ms.author: erikje
ms.assetid: 0b3ac749-4a61-4717-bf08-e0e6a15c3b0a
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f1f381d0b9f48f26c84785bb7c50434971d6c89
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330875"
---
# <a name="quickstart-create-and-assign-a-custom-role"></a>Rychlý start: Vytvoření a přiřazení vlastní role

V tomto rychlém startu pro Intune vytvoříte vlastní roli se specifickými oprávněními pro oddělení operací zabezpečení. Potom tuto roli přiřadíte skupině příslušných operátorů. Existuje několik výchozích rolí, které se dají okamžitě použít. Vytvořením vlastních rolí, jako je tato, však můžete přesně řídit přístup ke všem částem systému pro správu mobilních zařízení.

Pokud nemáte předplatné Intune, [zaregistrujte si bezplatný zkušební účet](free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky

- Abyste mohli projít tento rychlý start, je nutné [vytvořit skupinu](quickstart-create-group.md).

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

Přihlaste se k [Intune](https://aka.ms/intuneportal) jako globální správce nebo správce služby Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="create-a-custom-role"></a>Vytvoření vlastní role

Když vytvoříte vlastní roli, můžete nastavit oprávnění pro širokou škálu akcí. Pro roli Operace zabezpečení nastavíme několik oprávnění ke čtení tak, aby příslušný operátor mohl kontrolovat konfigurace a zásady zařízení.

1. V Intune zvolte **Role** > **Všechny role** > **Přidat**.
![Prohlížeč](./media/quickstart-create-custom-role/add-custom-role.png)
2. V části **Přidat vlastní roli** do pole **Název** zadejte *Operace zabezpečení*.
3. Do pole **Popis** zadejte *Tato role umožňuje operátorovi zabezpečení monitorovat konfiguraci zařízení a informace o dodržování předpisů.*
4. Zvolte **Konfigurovat** > **Identifikátory podnikových zařízení** > **Ano** vedle možnosti **Číst** > **OK**.
![Prohlížeč](./media/quickstart-create-custom-role/corp-device-id-read.png)
5. Zvolte **Zásady dodržování předpisů zařízení** > **Ano** vedle možnosti **Číst** > **OK**.
6. Zvolte **Konfigurace zařízení** > **Ano** vedle možnosti **Číst** > **OK**.
7. Zvolte **Organizace** > **Ano** vedle možnosti **Číst** > **OK**.
8. Zvolte **OK** > **Vytvořit**.

## <a name="assign-the-role-to-a-group"></a>Přiřazení role skupině

Operátor zabezpečení může použít nová oprávnění až poté, co danou roli přiřadíte skupině obsahující uživatele zabezpečení.

1. V Intune zvolte **Role** > **Všechny role** > **Operace zabezpečení**.
2. V části **Role Intune** zvolte **Přiřazení** > **Přiřadit**.
3. Do pole **Název přiřazení** zadejte *Operace zabezpečení*.
4. Zvolte **Členové (Skupiny)**  > **Přidat**.
5. Zvolte skupinu **Testeři Contoso**.
6. Zvolte **Vybrat** > **OK**.
7. Zvolte **Rozsah (Skupiny)**  > **Vybrat skupiny, které se zahrnou** > **Testeři Contoso**.
8. Zvolte **Vybrat** > **OK** > **OK**.

Teď jsou všichni členové dané skupiny členy role *Operace zabezpečení* a můžou kontrolovat následující informace o zařízení: identifikátory podnikových zařízení, zásady dodržování předpisů zařízením, konfigurace zařízení a informace o organizaci.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud už nechcete novou vlastní roli dále používat, můžete ji odstranit. Zvolte **Role** > **Všechny role** > vyberte tři tečky vedle příslušné role > **Odstranit**.

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste vytvořili vlastní roli pro operace zabezpečení a přiřadili jste ji skupině. Další informace o rolích v Intune najdete v článku [Řízení správy na základě role (RBAC) v Microsoft Intune](role-based-access-control.md).

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý Start: vytvoření profilu e-mailového zařízení pro iOS/iPadOS](../configuration/quickstart-email-profile.md)
