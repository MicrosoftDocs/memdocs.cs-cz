---
title: Rychlý Start – vytvoření profilu e-mailového zařízení pro zařízení s iOS/iPadOS
titleSuffix: Microsoft Intune
description: Naučte se, jak pomocí Microsoft Intune vytvořit profil e-mailového zařízení, aby se zařízení s iOS/iPadOS mohla bezpečně připojit k firemnímu e-mailu.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/18/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a6345afe4258ff7141228a7284932f083791c70
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332215"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Rychlý Start: vytvoření profilu e-mailového zařízení pro iOS/iPadOS

V tomto rychlém startu se dozvíte, jak vytvořit profil e-mailového zařízení pro zařízení s iOS/iPadOS. Tento profil určuje nastavení, které je nutné pro integrovanou e-mailovou aplikaci na zařízení se systémem iOS/iPadOS pro připojení k firemnímu e-mailu. E-mailové profily zařízení pomáhají standardizovat nastavení pro různá zařízení a umožňují koncovým uživatelům přístup k firemnímu e-mailu na jejich osobních zařízeních bez toho, aby museli něco nastavovat. K dalšímu zabezpečení e-mailu můžete použít e-mailový profil k určení, jestli jsou zařízení kompatibilní, a pak nastavit podmíněný přístup tak, aby přístup k e-mailu umožňoval jenom vyhovující zařízení. Podrobnosti o e-mailových profilech najdete v tématu [Jak nakonfigurovat nastavení e-mailu v Microsoft Intune](email-settings-configure.md).

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako globální správce nebo správce služby Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="create-an-iosipados-email-profile"></a>Vytvoření e-mailového profilu pro iOS/iPadOS

1. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

   ![Vytvoření e-mailového profilu pro iOS/iPadOS v Intune](./media/quickstart-email-profile/ios-create-profile.png)

2. Do pole **Název** zadejte popisný název nového profilu. Pro účely tohoto příkladu zadejte **Vyžadovat pracovní e-mail pro iOS**.
3. Zadejte následující informace o profilu:
    - Jako **Popis**zadejte **vyžadovat, aby zařízení s iOS/iPadOS používala pracovní e-mail**.
    - V případě **platformy**vyberte **iOS/iPadOS**.
    - U možnosti **Typ profilu** vyberte **E-mail**.

        ![Vytvoření e-mailového profilu pro použití se zařízeními s iOS/iPadOS v Intune](./media/quickstart-email-profile/ios-email-profile-name.png)

4. Vyberte **Nastavení** a zadejte následující nastavení (u dalších nastavení ponechejte výchozí hodnoty):
   - **E-mailový server**: Pro účely tohoto rychlého startu zadejte **outlook.office365.com**. Toto nastavení určuje umístění Exchange (URL) e-mailového serveru, který bude aplikace pro iOS/iPadOS mail používat pro připojení k e-mailu.
   - **Název účtu**: Zadejte **Firemní e-mail**.
   - **Atribut uživatelského jména z AAD**: Toto jméno je atribut, který Intune získá z Azure Active Directory (Azure AD). Pomocí tohoto jména Intune dynamicky vygeneruje uživatelské jméno pro tento profil. Pro účely tohoto rychlého startu předpokládáme, že chceme použít **hlavní název uživatele (UPN** ), který se použije jako uživatelské jméno pro profil (například user1@contoso.com).
   - **Atribut e-mailové adresy z AAD**: Toto nastavení je e-mailová adresa z Azure AD, která se použije pro přihlášení k serveru Exchange. Pro účely tohoto rychlého startu vyberte **Hlavní název uživatele (UPN)** .
   - **Metoda ověřování**: Pro účely tohoto rychlého startu vyberte možnost **Uživatelské jméno a heslo**. ( **Certifikát** můžete zvolit i v případě, že jste už nastavili certifikát pro Intune.)

        ![Vytvoření e-mailového profilu pro iOS/iPadOS use](./media/quickstart-email-profile/ios-email-profile.png)

5. Vyberte **OK** > **vytvořit**. Nový profil se zobrazí v seznamu profily se zobrazeným řídicím panelem, abyste mohli sledovat, jak byl profil přiřazený zařízením se systémem iOS/iPadOS a uživatelům iOS/iPadOS.
6. Zvolte **Přiřazení**.
7. Vyberte kartu **Zahrnout** a pak vyberte **Všichni uživatelé a všechna zařízení**. 
8. Vyberte **Uložit**.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud nechcete používat profil, který jste vytvořili pro další kurzy nebo testování, můžete ho teď odstranit.

1. V Intune vyberte **Konfigurace zařízení** a pak **Profily**.
2. Vyberte profil testu, který jste vytvořili, **iOS/iPadOS vyžaduje pracovní e-mail**.
3. Vyberte tři tečky ( **...** ) vedle tohoto profilu a pak vyberte **Odstranit**.

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste vytvořili e-mailový profil pro zařízení s iOS/iPadOS. Tento profil teď můžete použít k určení, jestli zařízení s iOS/iPadOS dodržuje předpisy, vytvořením zásad dodržování předpisů, které se označí jako nekompatibilní všechna zařízení s iOS nebo iPadOS, která se neshodují s profilem. Pro další ochranu můžete vytvořit zásadu podmíněného přístupu, která blokuje přístup k e-mailu pro zařízení s iOS a iPadOS, která nedodržují předpisy. Další informace o zásadách dodržování předpisů pro zařízení najdete v článku o tom, [jak začít používat zásady dodržování předpisů pro zařízení v Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Kurz: Ochrana e-mailu Exchange Online na spravovaných zařízeních](../protect/tutorial-protect-email-on-enrolled-devices.md)
