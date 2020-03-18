---
title: Kurz – Ochrana e-mailů Exchange Online na spravovaných zařízeních
titleSuffix: Microsoft Intune
description: Naučte se zabezpečit Exchange Online pomocí zásad dodržování předpisů Intune pro iOS a podmíněného přístupu Azure AD, abyste mohli vyžadovat spravovaná zařízení a aplikaci Outlook.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/21/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9921fb9e22b17a47c588dfcbfbf502e00ef2aadd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328643"
---
# <a name="tutorial-protect-exchange-online-email-on-managed-devices"></a>Kurz: Ochrana e-mailu Exchange Online na spravovaných zařízeních

Přečtěte si, jak používat zásady dodržování předpisů pro zařízení s podmíněným přístupem, abyste se ujistili, že zařízení se systémem iOS mají přístup k e-mailu Exchange Online jenom v případě, že jsou spravovaná pomocí Intune

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvořit zásadu dodržování předpisů zařízením s iOSem v Intune. Tato zásada nastaví podmínky, které zařízení musí splnit, než bude považováno za vyhovující.
> * Vytvořte zásadu podmíněného přístupu Azure Active Directory (Azure AD), která vyžaduje, aby se zařízení s iOS zaregistrovala do Intune, dodržovala zásady Intune a používala schválenou mobilní aplikaci Outlooku k přístupu k e-mailu Exchange Online.

Pokud nemáte předplatné Intune, [zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky

Pro účely tohoto kurzu budete potřebovat testovacího tenanta s následujícími předplatnými:

- Azure Active Directory Premium ([bezplatná zkušební verze](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))

- Předplatné Office 365 Business, které zahrnuje Exchange ([bezplatná zkušební verze](https://go.microsoft.com/fwlink/p/?LinkID=510938))

Než začnete, vytvořte profil testovacího zařízení pro zařízení s iOS podle kroků v části [rychlý Start: vytvoření profilu e-mailového zařízení pro iOS/iPadOS](../configuration/quickstart-email-profile.md).

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako [globální správce](../fundamentals/users-add.md#types-of-administrators) nebo [Správce služby](../fundamentals/users-add.md#types-of-administrators)Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="create-the-ios-device-compliance-policy"></a>Vytvoření zásady dodržování předpisů zařízením s iOSem

Nastavte zásadu dodržování předpisů zařízením s iOSem v Intune a nastavte podmínky, které zařízení musí splnit, než bude považováno za vyhovující. Pro účely tohoto kurzu vytvoříme zásadu dodržování předpisů pro zařízení s iOSem. Zásady dodržování předpisů jsou pro jednotlivé platformy specifické, a proto potřebujete samostatnou zásadu dodržování předpisů pro každou platformu zařízení, kterou chcete vyhodnotit.

1. V Intune vyberte **zařízení** > **zásady dodržování předpisů** > **vytvořit zásadu**.

2. Jako **název**zadejte **test zásad dodržování předpisů pro iOS**.

3. Jako **Popis**zadejte **test zásad dodržování předpisů pro iOS**.

4. V případě **platformy**vyberte **iOS/iPadOS**.

5. Vyberte **Nastavení** > **E-mail**.

   1. Vedle možnosti **Vyžadovat, aby mobilní zařízení měla spravovaný e-mailový profil** vyberte **Vyžadovat**.

   2. Vyberte **OK**.

   ![Nastavení zásad dodržování předpisů e-mailem, které vyžadují spravovaný e-mailový profil](./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-email.png)

6. Vyberte **Stav zařízení**. Vedle možnosti **Zařízení s jailbreakem** vyberte **Blokovat** a potom vyberte **OK**.

7. Vyberte **Zabezpečení systému** a zadejte nastavení **hesla**. Pro účely tohoto kurzu vyberte následující doporučená nastavení:

   - U možnosti **Vyžadovat heslo k odemknutí mobilních zařízení** vyberte **Vyžadovat**.

   - U možnosti **Jednoduchá hesla** vyberte **Blokovat**.

   - U možnosti **Minimální délka hesla** zadejte **4**.

     > [!TIP]
     > Výchozí hodnoty, které jsou šedé a kurzívou, jsou pouze doporučení. Je nutné nahradit hodnoty, které jsou doporučeními ke konfiguraci nastavení.

   - Jako **Požadovaný typ hesla** zvolte **Alfanumerické**.

   - U možnosti **Maximální počet minut po uzamčení obrazovky, po kterém bude nutné zadat heslo**, zvolte **Okamžitě**.

   - U možnosti **Konec platnosti hesla (dny)** zadejte **41**.

   - U možnosti **Počet předchozích hesel, která se nesmí použít znovu** zadejte **5**.
 
   ![Nastavení hesla pro zásady dodržování předpisů e-mailem](./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-system-security.png)

8. Vyberte **OK** a potom znovu vyberte **OK**.

9. Vyberte **Vytvořit**.

## <a name="create-the-conditional-access-policy"></a>Vytvoření zásady podmíněného přístupu

Nyní vytvoříme zásadu podmíněného přístupu, která vyžaduje, aby všechny platformy zařízení registrovaly do Intune a dodržovaly zásady dodržování předpisů Intune předtím, než budou mít přístup k Exchangi Online. Pro přístup k e-mailu budeme také vyžadovat aplikaci Outlook. Zásady podmíněného přístupu se dají nakonfigurovat buď na portálu Azure AD, nebo na portálu Intune. Vzhledem k tomu, že se už nacházíme na portálu Intune, vytvoříme zásadu zde.

1. V Intune vyberte **Endpoint security** > **podmíněný přístup** > **nové zásady**.

2. Jako **název**zadejte **zásady testu pro e-maily Office 365**.

3. V části **Přiřazení** vyberte **Uživatelé a skupiny**. Na kartě **Zahrnout** vyberte **Všichni uživatelé** a vyberte **Hotovo**.

4. V části **přiřazení**vyberte **cloudové aplikace nebo akce**. Protože chceme chránit e-mail Office 365 se službou Exchange Online, vybereme ho následujícím postupem:

   1. Na kartě **Zahrnout** zvolte **Vybrat aplikace**.

   2. Zvolte **Vybrat**. 

   3. V seznamu aplikací vyberte **Office 365 se službou Exchange Online** a potom zvolte **Vybrat**. 

   4. Vyberte **Hotovo**.
  
   ![Výběr aplikace Office 365 se službou Exchange Online](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-apps.png)

5. V části **Přiřazení** vyberte **Podmínky** > **Platformy zařízení**.

   1. V části **Konfigurovat** vyberte **Ano**.

   2. Na kartě **Zahrnout** vyberte **libovolné zařízení**a potom vyberte **Hotovo**. 

   3. Znovu vyberte **Hotovo**.

   ![Zahrnout všechna zařízení](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-device-platforms.png)

6. V části **Přiřazení** vyberte **Podmínky** > **Klientské aplikace**.

   1. V části **Konfigurovat** vyberte **Ano**.

   2. Pro účely tohoto kurzu vyberte **Mobilní aplikace a desktopoví klienti** a **Klienti moderního ověřování** (týká se aplikací, jako jsou Outlook pro iOS a Outlook pro Android). Zaškrtnutí všech ostatních políček zrušte.

   3. Vyberte **Hotovo** a potom znovu vyberte **Hotovo**.

   ![Výběr aplikací a klientů](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-client-apps.png)

7. V části **Ovládací prvky přístupu** zvolte **Udělení**.

   1. V podokně **Udělení** vyberte **Udělit přístup**.

   2. Vyberte **Vyžadovat, aby zařízení bylo označené jako vyhovující**.

   3. Vyberte **Vyžaduje se klientem schválená aplikace**.

   4. V části **Pro více ovládacích prvků** vyberte **Vyžadovat všechny vybrané ovládací prvky**. Toto nastavení zajistí, že se při přístupu zařízení k e-mailu oba vybrané požadavky vynutí.

   5. Zvolte **Vybrat**.

   ![Vybrat ovládací prvky](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-grant-access.png)

8. V části **Povolit zásadu** vyberte **Zapnuto**.

   ![Povolení zásady](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-enable-policy.png)

9. Vyberte **Vytvořit**.

## <a name="try-it-out"></a>Vyzkoušejte si to

V případě zásad, které jste vytvořili, se musí všechna zařízení se systémem iOS, která se pokusí přihlásit k Office 365 e-mail, zaregistrovat v Intune a používat mobilní aplikaci Outlook pro iOS/iPadOS. Pokud chcete tento scénář otestovat na zařízení s iOSem, zkuste se přihlásit k Exchangi Online pomocí přihlašovacích údajů uživatele v testovacím tenantovi. Zobrazí se výzva k registraci zařízení a k instalaci mobilní aplikace Outlook.

1. Pokud si chcete zásady otestovat na iPhonu, přejděte na **Nastavení** > **Hesla a účty** > **Přidat účet** > **Exchange**.

2. Zadejte e-mailovou adresu uživatele v testovacím tenantovi a stiskněte **Další**.

3. Stiskněte **Přihlásit se**.

4. Zadejte heslo testovacího uživatele a stiskněte **Přihlásit se**.

5. Zobrazí se zpráva, že zařízení musí být spravováno, aby mohlo prostředek použít, spolu s možností registrace.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud už testovací zásady nepotřebujete, můžete je odebrat.
1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako globální správce nebo správce služby Intune.

2. Vyberte **zařízení** > **zásady dodržování předpisů**.

3. V seznamu **Název zásady** vyberte u testovací zásady místní nabídku ( **...** ) a potom vyberte **Odstranit**. Vyberte **OK**. Tím akci potvrdíte.

4. Vyberte možnost **zabezpečení koncového bodu** > **podmíněný přístup**.

5. V seznamu **Název zásady** vyberte u testovací zásady místní nabídku ( **...** ) a potom vyberte **Odstranit**. Vyberte **Ano**. Tím akci potvrdíte.

## <a name="next-steps"></a>Další kroky

V tomto kurzu jste vytvořili zásady, které vyžadují, aby se zařízení s iOSem zaregistrovala v Intune a používala aplikaci Outlook pro přístupu k e-mailu Exchange Online. Další informace o použití Intune s podmíněným přístupem k ochraně dalších aplikací a služeb, včetně klientů Exchange ActiveSync pro Office 365 Exchange Online, najdete v tématu [nastavení podmíněného přístupu](conditional-access.md).
