---
title: 'Rychlý start: Nastavení automatické registrace v Intune'
description: 'Rychlý start: Nastavení automatické registrace zařízení s Windows 10 v Intune.'
services: microsoft-intune
author: ErikjeMS
manager: dougeby
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 599a5f6e6e355a37e909182fc14a07d489f45558
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872031"
---
# <a name="quickstart-set-up-automatic-enrollment-for-windows-10-devices"></a>Rychlý start: Nastavení automatické registrace zařízení s Windows 10

V tomto rychlém startu nastavíte v Microsoft Intune automatickou registraci zařízení, když se konkrétní uživatelé přihlásí k zařízením s Windows 10.

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Předpoklady

- Předplatné Microsoft Intune – [zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).
- K dokončení tohoto rychlého startu potřebujete napřed [vytvořit uživatele](../fundamentals/quickstart-create-user.md) a [vytvořit skupinu](../fundamentals/quickstart-create-group.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Přihlášení k Intune ve službě Microsoft Endpoint Manager

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako globální správce nebo správce Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="set-up-windows-10-automatic-enrollment"></a>Nastavení automatické registrace pro Windows 10

V tomto příkladu použijete registraci MDM, aby byla možná automatická registrace firemních zařízení i vlastních zařízení uživatelů. Zaregistrujete si bezplatné předplatné Azure Active Directory verze Premium.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **všechny služby**  >  **M365 Azure Active Directory**  >  **Azure Active Directory**  >  **mobilita (MDM a mam)**.
2. Vyberte **Abyste mohli použít tuto funkci, pořiďte si bezplatnou zkušební verzi Premium**. Její výběr vám umožní automatickou registraci pomocí bezplatné zkušební verze Premium služby Azure Active Directory. 

    ![Výběr bezplatné zkušební verze Premium služby Azure Active Directory](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-01.png)

3. Zvolte možnost bezplatné zkušební verze **Enterprise Mobility + Security E5**. 
4. Kliknutím na **bezplatnou zkušební verzi**  >  **aktivujte** bezplatnou zkušební verzi.

    ![Volba bezplatné zkušební verze Enterprise Mobility + Security E5](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-02.png)

    > [!NOTE]
    > Aktivace může trvat několik minut. 

3. Vyberte **Microsoft Intune** pro konfiguraci Intune. 

    ![Volba Microsoft Intune v seznamu](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-03.png)

4. V seznamu **Obor uživatele MDM** vyberte **Někteří**. Automatická registrace MDM se tak použije ke správně podnikových dat na zaměstnaneckých zařízeních s Windows. Automatická registrace MDM se nakonfiguruje pro zařízení připojená ke službě AAD a vlastní zařízení uživatelů.

    ![Výběr možnosti Někteří v seznamu konfigurace](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-04.png)

5. Klikněte na **Vybrat skupiny**  >  **Contoso testery**  >  **Vybrat** jako přiřazenou skupinu.

    ![Výběr skupiny k registraci](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-05.png)

6. V seznamu **Obor uživatele MDM** vyberte **Někteří**. Data se tak budou spravovat na zařízeních vašich zaměstnanců.

    ![Výběr skupiny k registraci](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-06.png)

7. Zvolte **Vybrat skupiny**  >  **Contoso testery**  >  **Vybrat** jako přiřazenou skupinu. 
8. Pro zbývající konfigurační hodnoty použijte výchozí hodnoty.
9. Klikněte na tlačítko **Uložit**.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud chcete automatickou registraci v Intune změnit, zaškrtněte, že chcete [nastavit registraci zařízení s Windows](windows-enroll.md).

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste se naučili, jak nastavit automatickou registraci zařízení s Windows 10. Další informace o registraci zařízení najdete v článku [Co je registrace zařízení?](device-enrollment.md)

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Registrace zařízení s Windows 10](quickstart-enroll-windows-device.md)
