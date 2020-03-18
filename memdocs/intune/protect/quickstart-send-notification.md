---
title: Rychlý start – odeslání oznámení zařízením nedodržujícím předpisy
titleSuffix: Microsoft Intune
description: V tomto rychlém startu použijete Microsoft Intune k posílání e-mailových oznámení na zařízení nedodržující předpisy.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1b89f2d-7937-46bb-926b-b05f6fa9c749
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe62fa8082923b960773ce3ca45654a541132ca6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325283"
---
# <a name="quickstart-send-notifications-to-noncompliant-devices"></a>Rychlý start: Odeslání oznámení zařízením nedodržujícím předpisy

V tomto rychlém startu použijete Microsoft Intune k odeslání e-mailových oznámení členům pracovníků, kteří mají zařízení nedodržující předpisy.

Když Intune ve výchozím nastavení detekuje zařízení, které nedodržuje předpisy, okamžitě ho označí jako nedodržující předpisy. Služba Azure Active Directory (Azure AD) [podmíněný přístup](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) pak zařízení zablokuje. Pokud zařízení nedodržuje předpisy, Intune vám umožní přidat akce při nedodržení předpisů, což vám poskytne flexibilitu při rozhodování o tom, co dělat. Uživatelům můžete dát například určitou dobu odkladu, během které musí zajistit dodržování předpisů, než tato zařízení zablokujete.

Jedna akce, která se má provést, když zařízení nevyhovuje předpisům, je odeslání e-mailu uživateli zařízení. Před odesláním e-mailového oznámení můžete také upravit. Konkrétně můžete přizpůsobit příjemce, předmět a text zprávy včetně firemního loga a kontaktních údajů. Intune obsahuje taky podrobnosti o zařízení nesplňujících požadavky v e-mailovém oznámení.

Pokud nemáte předplatné Intune, [zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky

Pokud používáte zásady dodržování předpisů zařízením k blokování zařízení z firemních prostředků, musíte nastavit podmíněný přístup Azure AD. Pokud jste dokončili rychlý Start pro [vytváření zásad dodržování předpisů pro zařízení](quickstart-set-password-length-android.md) , používáte Azure Active Directory. Další informace o Azure AD najdete v tématu [podmíněný přístup v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) a [běžné způsoby použití podmíněného přístupu s Intune](../protect/conditional-access-intune-common-ways-use.md).

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako [globální správce](../fundamentals/users-add.md#types-of-administrators) nebo [Správce služby](../fundamentals/users-add.md#types-of-administrators)Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, se kterým jste předplatné vytvořili, je globální správce.

## <a name="create-a-notification-message-template"></a>Vytvoření šablony zprávy s oznámením

Pokud chcete svým uživatelům odeslat e-mail, vytvořte šablonu zprávy s oznámením. Pokud zařízení nedodržuje předpisy, musíte do šablony zadat podrobnosti, které se zobrazují v e-mailu odeslaném vašim uživatelům.

1. V Intune vyberte **zařízení** > **zásady dodržování předpisů** > **oznámení** > **vytvořit oznámení**.
2. Zadejte následující informace:

   - **Jméno:** *Správce Contoso*
   - **Předmět:** *Dodržování předpisů zařízením*
   - **Zpráva**: *vaše zařízení aktuálně nesplňuje požadavky naší organizace na dodržování předpisů.*
   - **Záhlaví e-mailu – Připojte logo společnosti:** Pokud chcete zobrazit logo organizace, nastavte na **Povoleno**.
   - **Zápatí e-mailu – Uveďte název společnosti:** Pokud chcete zobrazit název organizace, nastavte na **Povoleno**.
   - **Zápatí e-mailu – Uveďte kontaktní údaje:** Pokud chcete zobrazit kontaktní údaje organizace, nastavte na **Povoleno**.

   ![Příklad oznámení o dodržování předpisů v Intune](./media/quickstart-send-notification/quickstart-send-notification-01.png)

3. Vyberte **Další** a zkontrolujte své oznámení. Vyberte **vytvořit** a Šablona zprávy s oznámením je připravena k použití.

   > [!NOTE]
   > Můžete také upravit některou dříve vytvořenou šablonu oznámení.

Podrobnosti o nastavení názvu společnosti, kontaktní informace společnosti a loga společnosti najdete v následujících článcích:

- [Informace o společnosti a prohlášení o zásadách ochrany osobních údajů](../apps/company-portal-app.md#company-information-and-privacy-statement)
- [Informace o podpoře](../apps/company-portal-app.md#support-information)
- [Přizpůsobení značky identity společnosti](../apps/company-portal-app.md#company-identity-branding-customization).

## <a name="add-a-noncompliance-policy"></a>Přidání zásady při nedodržování předpisů

Když vytvoříte zásady dodržování předpisů pro zařízení, Intune automaticky vytvoří akci pro případ nedodržování těchto předpisů. Intune pak označí zařízení jako nedodržující předpisy, když nevyhovují zásadám dodržování předpisů. Můžete přizpůsobit, jak dlouho bude zařízení takto označené. Při vytváření zásady dodržování předpisů nebo aktualizaci existující zásady dodržování předpisů můžete také přidat další akci.

Následující postup vytvoří zásadu dodržování předpisů pro zařízení s Windows 10.

1. V Intune vyberte **zařízení** > **zásady dodržování předpisů** > **vytvořit zásadu**.

2. Zadejte následující informace:

   - **Název:** *Dodržování předpisů pro Windows 10*
   - **Popis:** *Zásada dodržování předpisů pro Windows 10*
   - **Platforma:** Windows 10 a novější

3. Výběrem možnosti **Nastavení** > **Zabezpečení systému** zobrazte nastavení související se zabezpečením zařízení.

4. Nakonfigurujte tyhle možnosti:

   - Možnost **Vyžadovat heslo k odemknutí mobilních zařízení** nastavte na **Vyžadovat**. Toto nastavení určuje, jestli se má po uživatelích vyžadovat zadání hesla, než bude udělen přístup k informacím uloženým v jejich mobilních zařízeních.

   - Volbu **Minimální délka hesla** nastavte na **6**. Toto nastavení určuje minimální počet číslic nebo znaků v hesle.

   ![Nastavení Zabezpečení systému pro novou zásadu dodržování předpisů](./media/quickstart-send-notification/system-security-settings-01.png)

5. Vyberte **ok** > **OK** > **vytvořit** a vytvořte tak zásady dodržování předpisů.

6. Vyberte **Vlastnosti** > **Akce při nedodržení předpisů** > **Přidat**.

7. V rozevíracím seznamu **Akce** potvrďte, že je vybraná možnost **Odeslat e-mail koncovému uživateli**.

8. Vyberte **šablonu zprávy**, šablonu, kterou jste vytvořili dříve v tomto článku, a poté **Vyberte** šablonu zprávy.

9. Pokud chcete změny uložit, vyberte **přidat** > **OK** > **Uložit** .

## <a name="assign-the-policy"></a>Přiřazení zásady

Zásadu dodržování předpisů můžete přiřadit určité skupině uživatelů nebo všem uživatelům. Když Intune rozpozná, že zařízení nedodržuje předpisy, upozorní uživatele, že musí aktualizovat svoje zařízení, aby splňoval zásady dodržování předpisů. Zásadu přiřadíte pomocí následujícího postupu.

1. V Intune přejdete na **zařízení** > **zásady dodržování předpisů** a vyberte zásady **dodržování předpisů pro Windows 10** , které jste vytvořili dříve.

2. Zvolte **Přiřazení**.

3. V rozevíracím seznamu **Přiřadit k** vyberte **Všichni uživatelé**. Tím vyberete všechny uživatele. Každý uživatel se zařízením s **Windows 10 a novější verzí**, které nesplňuje tuto zásadu dodržování předpisů, dostane oznámení.

    > [!NOTE]
    > Při přiřazování zásad dodržování předpisů můžete zahrnout a vyloučit skupiny.

4. Klikněte na **Uložit**.

Po úspěšném vytvoření a uložení zásady se zobrazí v seznamu **zásad dodržování předpisů – zásady**. V tomto seznamu si můžete všimnout, že **Přiřazeno** je nastavené na **Ano**.

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste Intune použili k vytvoření a přiřazení zásady dodržování předpisů pro firemní zařízení s Windows 10, která vyžaduje zadání hesla o minimální délce šesti znaků. Další informace o vytváření zásad dodržování předpisů pro zařízení s Windows najdete v článku [Přidání zásad dodržování předpisů pro zařízení s Windows v Intune](compliance-policy-create-windows.md).

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Přidání a přiřazení klientské aplikace](../apps/quickstart-add-assign-app.md)
