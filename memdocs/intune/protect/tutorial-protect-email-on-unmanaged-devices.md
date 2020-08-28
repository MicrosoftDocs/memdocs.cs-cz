---
title: Kurz – Ochrana e-mailů Exchange Online na nespravovaných zařízeních
titleSuffix: Microsoft Intune
description: Naučte se zabezpečit Microsoft 365 Exchange Online pomocí zásad ochrany aplikací Intune a podmíněného přístupu Azure AD.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/30/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12b776af250a9d4a9bf0fb6c8ba7eec98540f883
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993949"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>Kurz: Ochrana e-mailů Exchange Online na nespravovaných zařízeních

Přečtěte si, jak používat zásady ochrany aplikací s podmíněným přístupem k ochraně Exchange Online, i když nejsou zařízení zaregistrovaná v řešení pro správu zařízení, jako je Intune. V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvořte zásady ochrany aplikací Intune pro aplikaci Outlook. Můžete omezit, co může uživatel s daty aplikace dělat, a zabránit tak akcím Uložit jako a omezit operace vyjmutí, zkopírování a vložení.
> * Vytvoření zásad podmíněného přístupu Azure Active Directory (Azure AD), které umožní přístup k firemnímu e-mailu v Exchange Online jenom aplikaci Outlook. Pro moderní ověřování klientů budete také vyžadovat vícefaktorové ověřování (MFA), jako je Outlook pro iOS a Android.

## <a name="prerequisites"></a>Předpoklady

Pro účely tohoto kurzu budete potřebovat testovacího tenanta s následujícími předplatnými:

- Azure Active Directory Premium ([bezplatná zkušební verze](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Předplatné Intune ([bezplatná zkušební verze](../fundamentals/free-trial-sign-up.md))
- Předplatné Microsoft 365 aplikací pro firmy, které zahrnuje Exchange ([bezplatná zkušební verze](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

V tomto kurzu se po přihlášení k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)přihlaste jako [globální správce](../fundamentals/users-add.md#types-of-administrators) nebo jako [Správce služby](../fundamentals/users-add.md#types-of-administrators)Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, se kterým jste předplatné vytvořili, je globální správce.

## <a name="create-the-app-protection-policy"></a>Vytvoření zásad ochrany aplikací

V tomto kurzu nastavíme zásady ochrany aplikací Intune pro iOS, aby aplikace Outlook mohla umístit ochrany na úrovni aplikace. Pro otevření aplikace v pracovním kontextu budeme vyžadovat kód PIN. Také omezíme sdílení dat mezi aplikacemi a zabránění ukládání firemních dat do osobního umístění.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **aplikace**  >  **Zásady ochrany aplikací**  >  **vytvořit zásadu**a pro platformu vyberte **iOS/iPadOS** .

3. Na stránce **základy** nakonfigurujte následující nastavení:

   - **Název**: zadejte **test zásad**aplikace pro Outlook.
   - **Popis**: zadejte **test zásad**aplikace pro Outlook.

   Hodnota **platformy** je nastavená na předchozí volbu.

   Pokračujte kliknutím na **Next** (Další).

4. Stránka **aplikace** umožňuje zvolit, jak chcete tyto zásady použít pro aplikace na různých zařízeních. Nakonfigurujte tyhle možnosti:

   - Pro **cíl pro všechny typy aplikací**: vyberte **ne**a pak u **typů aplikací**zaškrtněte políčko pro **aplikace na nespravovaných zařízeních**.
   - Klikněte na **Vybrat veřejné aplikace**. V seznamu aplikace vyberte možnost **Outlook**a pak zvolte **možnost vybrat**.  Outlook se teď zobrazuje v části *veřejné aplikace*.

   Pokračujte kliknutím na **Next** (Další).

5. Stránka **Ochrana dat** poskytuje nastavení, která určují, jak uživatelé budou pracovat s daty v aplikacích, které tato zásada ochrany aplikací používá. Nakonfigurujte tyhle možnosti:

   Níže *přenos dat*nakonfigurujte následující nastavení a nechte všechna ostatní nastavení na jejich výchozích hodnotách:

   - Pro možnost **Odeslat organizační data do jiných aplikací**vyberte **None (žádné**).  
   - Pro **příjem dat z jiných aplikací**vyberte **None (žádné**).  
   - V **části uložit kopie organizačních dat**vyberte **blokovat**.  
   - Pokud chcete **Omezit vyjmutí, zkopírování a vložení mezi ostatními aplikacemi**, vyberte **blokované**. 

   ![Výběr nastavení přemístění dat v zásadách ochrany aplikací Outlook](./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png)

   Pokračujte výběrem tlačítka **Další**.

6. Stránka **požadavky na přístup** poskytuje nastavení, které vám umožní nakonfigurovat požadavky na PIN a přihlašovací údaje, které uživatelé musí splnit, aby měli přístup k aplikacím v pracovním kontextu. Nakonfigurujte následující nastavení a nechte všechna ostatní nastavení na jejich výchozích hodnotách:

   - V případě **kódu PIN pro přístup**vyberte **vyžadovat**.
   - V případě **přihlašovacích údajů pracovního nebo školního účtu pro přístup**vyberte **vyžadovat**.

   ![Vybrat akce přístupu k zásadám ochrany aplikací Outlook](./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png)

   Pokračujte výběrem tlačítka **Další**.

7. **Podmíněná spouštěcí** stránka poskytuje nastavení pro nastavení požadavků zabezpečení přihlášení pro zásady ochrany aplikací. Pro tento kurz nemusíte konfigurovat tato nastavení.

   Pokračujte kliknutím na **Next** (Další).

8. Na stránce **přiřazení** můžete přiřadit zásady ochrany aplikací skupinám uživatelů. Pro tento kurz nepřiřazujte tuto zásadu ke skupině.  

   Pokračujte kliknutím na **Next** (Další).

9. Na stránce **Další: zkontrolovat + vytvořit** zkontrolujte hodnoty a nastavení, které jste zadali pro tyto zásady ochrany aplikací. Kliknutím na **vytvořit** vytvořte zásadu ochrany aplikací v Intune.

Vytvoří se zásady ochrany aplikací pro Outlook. V dalším kroku nastavíte podmíněný přístup, který bude vyžadovat, aby zařízení používalo Outlookovou aplikaci.

## <a name="create-conditional-access-policies"></a>Vytvoření zásad podmíněného přístupu

Nyní vytvoříme dvě zásady podmíněného přístupu, které pokrývají všechny platformy zařízení.  

- První zásada bude vyžadovat, aby klienti moderního ověřování používali schválenou aplikaci Outlook a službu Multi-Factor Authentication (MFA). Mezi klienty moderního ověřování patří Outlook pro iOS a Outlook pro Android.  

- Druhá zásada bude vyžadovat, aby klienti Exchange ActiveSync používali schválenou aplikaci Outlook. (V současné době Exchange Active Sync nepodporuje jiné podmínky než platforma zařízení). Zásady podmíněného přístupu můžete nakonfigurovat buď na portálu Azure AD, nebo na portálu Intune. Vzhledem k tomu, že už jsme na portálu Intune, vytvoříme tady zásadu.  

### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>Vytvoření zásady MFA pro klienty moderních ověřování  

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte položku **Endpoint Security**  >   **podmíněný přístup**  >  **nové zásady**.  

3. Jako **název**zadejte **zásady testování pro klienty s moderním ověřováním**.  

4. V části **Přiřazení** vyberte **Uživatelé a skupiny**. Na kartě **Zahrnout** vyberte **Všichni uživatelé** a vyberte **Hotovo**.

5. V části **přiřazení**vyberte **cloudové aplikace nebo akce**. Vzhledem k tomu, že chceme chránit Microsoft 365 e-mailové zprávy Exchange Online, vybereme je pomocí následujících kroků:

   1. Na kartě **Zahrnout** zvolte **Vybrat aplikace**.
   2. Zvolte **Vybrat**.
   3. V seznamu aplikace vyberte možnost **Office 365 Exchange Online**a pak zvolte **možnost vybrat**.
   4. Vyberte **Hotovo** a vraťte se do podokna nové zásady.

   ![Výběr aplikace Office 365 se službou Exchange Online](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png)

6. V části **Přiřazení** vyberte **Podmínky** > **Platformy zařízení**.

   1. V části **Konfigurovat** vyberte **Ano**.
   2. Na kartě **Zahrnout** vyberte **libovolné zařízení**.
   3. Vyberte **Hotovo**.

7. V podokně **podmínky** vyberte **klientské aplikace**.

   1. V části **Konfigurovat** vyberte **Ano**.
   2. Vyberte **mobilní aplikace a klienti pro stolní počítače** a **moderní ověřování**.
   3. Zrušte zaškrtnutí těchto políček.
   4. Vyberte **Hotovo**  >  **Done** a vraťte se do podokna nové zásady.

   ![Vybrat mobilní aplikace a klienti](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

8. V části **Ovládací prvky přístupu** zvolte **Udělení**.

   1. V podokně **Udělení** vyberte **Udělit přístup**.
   2. Vyberte **vyžadovat službu Multi-Factor Authentication**.
   3. Vyberte **Vyžaduje se klientem schválená aplikace**.
   4. V části **Pro více ovládacích prvků** vyberte **Vyžadovat všechny vybrané ovládací prvky**. Toto nastavení zajistí, že se při přístupu zařízení k e-mailu oba vybrané požadavky vynutí.
   5. Zvolte **Vybrat**.

   ![Výběr řízení přístupu](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

9. V části **Povolit zásadu**vyberte **zapnuto**a pak vyberte **vytvořit**.

   ![Vytvoření zásad](./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)  

Vytvoří se zásada podmíněného přístupu pro klienty moderního ověřování. Nyní můžete vytvořit zásadu pro klienty Exchange Active Sync.

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Vytvoření zásady pro Exchange Active Sync klientů

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte položku **Endpoint Security**  >  **podmíněný přístup**  >  **nové zásady**.

3. Jako **název**zadejte **zásady testování pro klienty EAS**.

4. V části **Přiřazení** vyberte **Uživatelé a skupiny**. Na kartě *Zahrnout* vyberte **Všichni uživatelé** a vyberte **Hotovo**.

5. V části **přiřazení**vyberte **cloudové aplikace nebo akce**. Vyberte Microsoft 365 e-mailové zprávy Exchange Online s těmito kroky:

   1. Na kartě *Zahrnout* zvolte **Vybrat aplikace**.
   2. Zvolte **Vybrat**.
   3. V seznamu *aplikací*vyberte možnost **Office 365 Exchange Online**a pak klikněte na **Vybrat**a pak na **Hotovo**.
  
6. V části **Přiřazení** vyberte **Podmínky** > **Platformy zařízení**.

   1. V části **Konfigurovat** vyberte **Ano**.
   2. Na kartě **Zahrnout** vyberte **libovolné zařízení**a potom vyberte **Hotovo**.

7. V podokně **podmínky** vyberte **klientské aplikace**.

   1. V části **Konfigurovat** vyberte **Ano**.
   2. Vyberte **mobilní aplikace a klienti klasické pracovní plochy**.
   3. Vyberte **klienti Exchange ActiveSync** a **použijte zásady jenom pro podporované platformy**.  
   4. Zaškrtnutí všech ostatních políček zrušte.  
   5. Vyberte **Hotovo** a potom znovu vyberte **Hotovo**.  

   ![Platí pro podporované platformy](./media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png)  

8. V části **Ovládací prvky přístupu** zvolte **Udělení**.

   1. V podokně **Udělení** vyberte **Udělit přístup**.
   2. Vyberte **Vyžaduje se klientem schválená aplikace**. Zaškrtnutí všech ostatních políček zrušte.
   3. Zvolte **Vybrat**.

   ![Vyžadovat klientskou aplikaci schválenou](./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

9. V části **Povolit zásadu**vyberte **zapnuto**a pak vyberte **vytvořit**.

Vaše zásady ochrany aplikací a podmíněný přístup teď fungují a jsou připravené k testování.

## <a name="try-it-out"></a>Vyzkoušet

Pomocí zásad, které jste vytvořili, se zařízení musí zaregistrovat v Intune a používat mobilní aplikaci Outlook k přístupu k e-mailu Microsoft 365. Pokud chcete tento scénář otestovat na zařízení s iOSem, zkuste se přihlásit k Exchangi Online pomocí přihlašovacích údajů uživatele v testovacím tenantovi.

1. Chcete-li provést test na iPhonu, použijte **Nastavení**  >  **hesla & účty**  >  **Přidat účet**  >  **Exchange**.

2. Zadejte e-mailovou adresu uživatele v testovacím tenantovi a stiskněte **Další**.  
3. Stiskněte **Přihlásit se**.

4. Zadejte heslo testovacího uživatele a stiskněte **Přihlásit se**.

5. Zobrazí se **Další informace, které jsou požadovány** , což znamená, že se zobrazí výzva k nastavení vícefaktorového ověřování. Pokračujte a nastavte další metodu ověřování.

6. V dalším kroku se zobrazí zpráva s informacemi o tom, že se snažíte otevřít tento prostředek, pomocí aplikace, která není schválená vaším IT oddělením. Zpráva znamená, že jste zablokovali používání aplikace v nativním e-mailu. Zrušte přihlášení.

7. Otevřete Outlook App a vyberte **Nastavení**  >  **Přidat účet**přidat  >  **e-mailový účet**.

8. Zadejte e-mailovou adresu uživatele v testovacím tenantovi a stiskněte **Další**.

9. Stiskněte tlačítko **Přihlásit se sadou Office 365**. Zobrazí se výzva k dodatečnému ověření a registraci. Po přihlášení můžete testovat akce, jako je vyjmutí, kopírování, vložení a uložit jako.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud už testovací zásady nepotřebujete, můžete je odebrat.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices** **zásady dodržování předpisů**pro zařízení.

3. V seznamu **název zásady** vyberte kontextovou nabídku (**...**) pro vaši zásadu testování a pak vyberte **Odstranit**. Vyberte **OK**. Tím akci potvrdíte.

4. Vyberte možnost podmíněný přístup **zabezpečení koncového bodu**  >  **Conditional access**.

5. V seznamu **název zásady** vyberte kontextovou nabídku (**...**) pro každou ze svých zásad testování a pak vyberte **Odstranit**. Akci potvrďte výběrem **Ano**.

## <a name="next-steps"></a>Další kroky
V tomto kurzu jste vytvořili zásady ochrany aplikací, abyste omezili to, co může uživatel dělat s aplikací Outlook, a vytvořili jste zásady podmíněného přístupu, které vyžadují aplikaci Outlook a vyžadují MFA pro klienty moderních ověřování. Další informace o používání Intune s podmíněným přístupem k ochraně dalších aplikací a služeb najdete v tématu [nastavení podmíněného přístupu](conditional-access.md).
