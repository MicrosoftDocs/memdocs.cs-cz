---
title: 'Rychlý start: Vytvoření uživatele v Intune'
description: 'Rychlý start: Vytvoření uživatele v Intune'
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.manager: dougeby
ms.assetid: 820fcb18-0927-4ebd-be79-dce92b51c261
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf5c76e276722fb9bab2b5d6fac511f0b22ae1f2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330747"
---
# <a name="quickstart-create-a-user-in-intune-and-assign-the-user-a-license"></a>Rychlý Start: vytvoření uživatele v Intune a přiřazení licence uživateli

V tomto rychlém startu vytvoříte uživatele a pak tomuto uživateli přiřadíte licenci Intune. Pokud používáte Intune, musí mít všichni uživatelé, kteří mají přístup k firemním datům, svůj vlastní uživatelský účet. Správci Intune můžou nakonfigurovat uživatele později, aby mohli spravovat řízení přístupu.

## <a name="prerequisites"></a>Požadavky

- Předplatné služby Microsoft Intune. [Zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune-in-microsoft-endpoint-manager"></a>Přihlášení k Intune ve službě Microsoft Endpoint Manager

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako [globální správce nebo správce služby Intune](users-add.md#types-of-administrators). Pokud jste vytvořili zkušební předplatné Intune, účet, se kterým jste předplatné vytvořili, je globální správce.

## <a name="create-a-user"></a>Vytvoření uživatele

Uživatel musí mít uživatelský účet k registraci do správy zařízení v Intune. Vytvoření nového uživatele:

1. V Microsoft Endpoint Manageru vyberte **Uživatelé** > **Všichni uživatelé** > **Nový uživatel**: ![ve Správci Microsoft Endpoint Manager vyberte nový uživatel.](./media/quickstart-create-user/create-user.png)
2. Do pole **název** zadejte název, například *Dewey Kellum*: Přidat podrobnosti o uživateli ![.](./media/quickstart-create-user/create-user-02.png)
3. Do pole **uživatelské jméno** zadejte identifikátor uživatele, například Dewey@contoso.onmicrosoft.com.

    > [!NOTE]
    > Pokud jste nenakonfigurovali název domény zákazníka, použijte ověřený název domény, který jste použili k vytvoření předplatného Intune (nebo [bezplatné zkušební verze](free-trial-sign-up.md#sign-up-for-a-microsoft-intune-free-trial)). 

4. Vyberte možnost **Zobrazit heslo** a nezapomeňte si pamatovat automaticky vygenerované heslo, abyste se mohli přihlásit k testovacímu zařízení.
5. Vyberte **Vytvořit**.

## <a name="assign-a-license-to-the-user"></a>Přiřazení licence uživateli

Po vytvoření uživatele musíte použít [Centrum pro správu Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) k přiřazení licence Intune uživateli. Pokud uživateli nepřiřazujete licenci, nebude se moct zaregistrovat do Intune.

Přiřazení licence Intune uživateli:

1. Přihlaste se k [centru pro správu Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) pomocí stejných přihlašovacích údajů, které jste použili pro přihlášení k Intune.
2. Vyberte **Uživatelé** > **aktivní uživatelé**a pak vyberte právě vytvořeného uživatele.
3. Vyberte kartu **licence a aplikace** .
4. V části **Vybrat umístění**vyberte umístění pro uživatele, pokud ještě není nastavené.
2. V části **licence** zaškrtněte políčko **Intune** . Pokud jiná licence zahrnuje Intune, můžete tuto licenci vybrat. Zobrazený [název produktu](https://docs.microsoft.com/azure/active-directory/users-groups-roles/licensing-service-plan-reference) se používá jako plán služby ve správě Azure.

    ![Vyberte umístění a licenci Intune.](./media/quickstart-create-user/create-user-03.png)

   > [!NOTE]
   > Toto nastavení využívá jednu z vašich licencí pro uživatele. Pokud používáte zkušební prostředí, později tuto licenci znovu přiřadíte skutečnému uživateli v živém prostředí.

6. Vyberte **Uložit změny**.

Nový aktivní uživatel Intune teď zobrazí, že používá licenci **Intune** .

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud tento uživatel už nepotřebujete, můžete uživatele odstranit tak, že v centru pro [správu Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) **a vyberete** > uživatele.*uživatel* > *odstraní ikonu* > **Delete user** > odstranit uživatele**Zavřít**.

   ![Vyberte ikonu Odstranit](./media/quickstart-create-user/create-user-04.png)

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste pro tohoto uživatele vytvořili uživatele a přiřadili mu licenci Intune. Další informace o přidání uživatelů do Intune najdete v článku [Přidání uživatelů a udělení oprávnění pro správu v Intune](users-add.md).

Pokud chcete pokračovat v této sérii rychlých startů Intune, přejděte k dalšímu rychlému startu:

> [!div class="nextstepaction"]
> [Rychlý start: Vytvoření skupiny pro správu uživatelů](quickstart-create-group.md)
