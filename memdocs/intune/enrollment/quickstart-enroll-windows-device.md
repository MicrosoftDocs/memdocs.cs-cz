---
title: Rychlý start – registrace zařízení s desktopovou verzí Windows 10 v Microsoft Intune
description: Rychlý start – použití Portálu společnosti k registraci zařízení s desktopovou verzí Windows 10 v Microsoft Intune
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67de7db6587c1f80d849808c139bf1ae94f4bbd5
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643645"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>Rychlý start: Registrace zařízení s Windows 10

V tomto rychlém startu nejprve převezmete roli uživatele Intune a zaregistrujete své zařízení s Windows 10 v Microsoft Intune. Pak se vrátíte do Intune a ověřte, jestli je zařízení zaregistrované.

Registrace zařízení do Microsoft Intune umožňuje zařízením s Windows 10 získat přístup k zabezpečeným datům vaší organizace, včetně e-mailů, souborů a dalších prostředků. Platí to pro zařízení s desktopovou verzí Windows 10 i zařízení s Windows 10 Mobile. Registrace zařízení pomáhá zabezpečit přístup pro vás i vaši organizaci a udržovat pracovní data odděleně od osobních dat.

> [!TIP]
> Zjistěte, co se stane, když [zařízení zaregistrujete v Intune](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md), a co to znamená pro [informace v zařízení](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky

- Předplatné Microsoft Intune – [registrace bezplatného zkušebního účtu](../fundamentals/free-trial-sign-up.md)
- Abyste mohli absolvovat tento rychlý start, musíte dokončit postup [nastavení automatické registrace v Intune](quickstart-setup-auto-enrollment.md).

## <a name="confirm-your-windows-10-desktop-version"></a>Potvrzení desktopové verze Windows 10

Před registrací počítače s desktopovou verzí Windows 10 musíte potvrdit verzi Windows, kterou máte nainstalovanou.

1. Klikněte pravým tlačítkem na ikonu **Start** ve Windows a výběrem příkazu **Nastavení** zobrazte možnosti Nastavení Windows.

   ![Snímek obrazovky Nastavení Windows – Systém](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. Vyberte **systém**  >  **o produktu**. 

   ![Snímek obrazovky s nastavením systému](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > Můžete také zadat frázi „informace o počítači“ do **panelu vyhledávání** a pak zvolit **Informace o počítači**.

3. V okně **Nastavení** uvidíte seznam **Specifikace Windows** vašeho počítače. V tomto seznamu najděte **verzi**.

4. Potvrďte, že **Verze** Windows 10 je **1607 nebo vyšší**.

    > [!IMPORTANT]
    > Postup uvedený v tomto rychlém startu platí pro Windows 10 verze **1607 nebo vyšší**. Pokud máte verzi **1511 nebo nižší**, pokračujte [tímto postupem](../user-help/enroll-windows-10-device.md).  

## <a name="enroll-windows-10-desktop"></a>Registrace desktopové verze Windows 10

1. Vraťte se k Nastavení Windows a vyberte **Účty**.

   ![Snímek obrazovky Nastavení systému – Účty](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. Vyberte **přístup do práce nebo do školy**  >  **připojit**.

    ![Vyberte možnost Nastavit pracovní nebo školní účet.](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. Přihlaste se k Intune pomocí svého pracovního nebo školního účtu a vyberte **Další**. Pokud jste postupovali v rychlém startu [vytvořit uživatele a přiřadit licenci](../fundamentals/quickstart-create-user.md) , můžete se přihlásit pomocí uživatelského účtu, který jste vytvořili.

    > [!NOTE]
    > Pokud nastavujete „.onmicrosoft.com“, bude se jako součást adresy uživatelského účtu používat **.onmicrosoft.com**. 

   ![Zadání pracovního nebo školního účtu](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    Zobrazí se zpráva oznamující, že vaše společnost nebo škola vaše zařízení registruje.

4. Až uvidíte, že **jste všechno nastavili!** vyberte **Hotovo**. Už jste hotovi.

5. Přidaný účet teď uvidíte jako součást nastavení **Přístup do práce nebo do školy** desktopové verze Windows.

   ![Snímek obrazovky nově přidaného účtu](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    Pokud jste postupovali podle předchozích kroků, ale pořád nemáte přístup k pracovnímu nebo školnímu e-mailovému účtu a souborům, postupujte podle kroků v tématu [řešení potíží s přístupem k zařízení s Windows 10](../user-help/troubleshoot-your-windows-10-device-windows.md).  

## <a name="confirm-your-device-enrollment-in-intune"></a>Potvrzení registrace zařízení v Intune

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako globální správce nebo správce služby Intune.
2. Vyberte **zařízení**  >  **všechna zařízení** a podívejte se na zaregistrovaná zařízení v Intune.
3. Ověřte, že máte v Intune zaregistrované další zařízení.

   ![Snímek obrazovky zařízení zaregistrovaných v Intune](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud chcete registraci zařízení s Windows zrušit, přečtěte si článek [Odebrání zařízení s Windows ze systému správy](../user-help/unenroll-your-device-from-intune-windows.md).

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste se naučili zaregistrovat zařízení s Windows 10 v Intune. Teď se naučíte další způsoby registrace zařízení na všech platformách. Další informace o používání zařízení s Intune najdete v článku [Práce pomocí spravovaných zařízení](../user-help/use-managed-devices-to-get-work-done.md).

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Nastavení požadované délky hesla pro zařízení s Androidem](../protect/quickstart-set-password-length-android.md)
