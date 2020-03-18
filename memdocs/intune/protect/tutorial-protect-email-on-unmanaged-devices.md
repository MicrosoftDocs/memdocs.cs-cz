---
title: Kurz – Ochrana e-mailů Exchange Online na nespravovaných zařízeních
titleSuffix: Microsoft Intune
description: Naučte se zabezpečit Office 365 Exchange Online pomocí zásad ochrany aplikací Intune a podmíněného přístupu Azure AD.
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
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1e6731e41ccc7c687cf6fa68dc06b8c6ee4e1e2
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328583"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>Kurz: Ochrana e-mailů Exchange Online na nespravovaných zařízeních

Přečtěte si, jak používat zásady ochrany aplikací s podmíněným přístupem k ochraně Exchange Online, i když nejsou zařízení zaregistrovaná v řešení pro správu zařízení, jako je Intune. V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvořte zásady ochrany aplikací Intune pro aplikaci Outlook. Můžete omezit, co může uživatel s daty aplikace dělat, a zabránit tak akcím Uložit jako a omezit operace vyjmutí, zkopírování a vložení.
> * Vytvoření zásad podmíněného přístupu Azure Active Directory (Azure AD), které umožní přístup k firemnímu e-mailu v Exchange Online jenom aplikaci Outlook. Pro moderní ověřování klientů budete také vyžadovat vícefaktorové ověřování (MFA), jako je Outlook pro iOS a Android.

## <a name="prerequisites"></a>Požadavky

Pro účely tohoto kurzu budete potřebovat testovacího tenanta s následujícími předplatnými:

- Azure Active Directory Premium ([bezplatná zkušební verze](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Předplatné Intune ([bezplatná zkušební verze](../fundamentals/free-trial-sign-up.md))
- Předplatné Office 365 Business, které zahrnuje Exchange ([bezplatná zkušební verze](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

V tomto kurzu se po přihlášení k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)přihlaste jako [globální správce](../fundamentals/users-add.md#types-of-administrators) nebo jako [Správce služby](../fundamentals/users-add.md#types-of-administrators)Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, se kterým jste předplatné vytvořili, je globální správce.

## <a name="create-the-app-protection-policy"></a>Vytvoření zásad ochrany aplikací

V tomto kurzu nastavíme zásady ochrany aplikací Intune pro iOS, aby aplikace Outlook mohla umístit ochrany na úrovni aplikace. Pro otevření aplikace v pracovním kontextu budeme vyžadovat kód PIN. Také omezíme sdílení dat mezi aplikacemi a zabránění ukládání firemních dat do osobního umístění.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **aplikace** > **zásady ochrany aplikací** > **vytvořit zásadu**a pro platformu vyberte **iOS/iPadOS** .

3. Na stránce **základy** nakonfigurujte následující nastavení:

   - **Název**: zadejte **test zásad**aplikace pro Outlook.
   - **Popis**: zadejte **test zásad**aplikace pro Outlook.

   Hodnota **platformy** je nastavená na předchozí volbu.

   Pokračujte kliknutím na **Další**.

4. Stránka **aplikace** umožňuje zvolit, jak chcete tyto zásady použít pro aplikace na různých zařízeních. Nakonfigurujte tyhle možnosti:

   - Pro **cíl pro všechny typy aplikací**: vyberte **ne**a pak u **typů aplikací**zaškrtněte políčko pro **aplikace na nespravovaných zařízeních**.
   - Klikněte na **Vybrat veřejné aplikace**. V seznamu aplikace vyberte možnost **Outlook**a pak zvolte **možnost vybrat**.  Outlook se teď zobrazuje v části *veřejné aplikace*.

   Pokračujte kliknutím na **Další**.

5. Stránka **Ochrana dat** poskytuje nastavení, která určují, jak uživatelé budou pracovat s daty v aplikacích, které tato zásada ochrany aplikací používá. Nakonfigurujte tyhle možnosti:

   Níže *přenos dat*nakonfigurujte následující nastavení a nechte všechna ostatní nastavení na jejich výchozích hodnotách:

   - Pro možnost **Odeslat organizační data do jiných aplikací**vyberte **None (žádné**).  
   - Pro **příjem dat z jiných aplikací**vyberte **None (žádné**).  
   - V **části uložit kopie organizačních dat**vyberte **blokovat**.  
   - Pokud chcete **Omezit vyjmutí, zkopírování a vložení mezi ostatními aplikacemi**, vyberte **blokované**. 

   ![Výběr nastavení přemístění dat v zásadách ochrany aplikací Outlook](./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png)

   Pokračujte výběrem **Další** .

6. Stránka **požadavky na přístup** poskytuje nastavení, které vám umožní nakonfigurovat požadavky na PIN a přihlašovací údaje, které uživatelé musí splnit, aby měli přístup k aplikacím v pracovním kontextu. Nakonfigurujte následující nastavení a nechte všechna ostatní nastavení na jejich výchozích hodnotách:

   - V případě **kódu PIN pro přístup**vyberte **vyžadovat**.
   - V případě **přihlašovacích údajů pracovního nebo školního účtu pro přístup**vyberte **vyžadovat**.

   ![Vybrat akce přístupu k zásadám ochrany aplikací Outlook](./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png)

   Pokračujte výběrem **Další** .

7. **Podmíněná spouštěcí** stránka poskytuje nastavení pro nastavení požadavků zabezpečení přihlášení pro zásady ochrany aplikací. Pro tento kurz nemusíte konfigurovat tato nastavení.

   Pokračujte kliknutím na **Další**.

8. Na stránce **přiřazení** můžete přiřadit zásady ochrany aplikací skupinám uživatelů. Pro tento kurz nepřiřazujte tuto zásadu ke skupině.  
 Toto nastavení nemusíte konfigurovat.

   Pokračujte kliknutím na **Další**.

9. Na stránce **Další: zkontrolovat + vytvořit** zkontrolujte hodnoty a nastavení, které jste zadali pro tyto zásady ochrany aplikací. Kliknutím na **vytvořit** vytvořte zásadu ochrany aplikací v Intune.

Vytvoří se zásady ochrany aplikací pro Outlook. V dalším kroku nastavíte podmíněný přístup, který bude vyžadovat, aby zařízení používalo Outlookovou aplikaci.

## <a name="create-conditional-access-policies"></a>Vytvoření zásad podmíněného přístupu

Nyní vytvoříme dvě zásady podmíněného přístupu, které pokrývají všechny platformy zařízení.  

- První zásada bude vyžadovat, aby klienti moderního ověřování používali schválenou aplikaci Outlook a službu Multi-Factor Authentication (MFA). Mezi klienty moderního ověřování patří Outlook pro iOS a Outlook pro Android.  

- Druhá zásada bude vyžadovat, aby klienti Exchange ActiveSync používali schválenou aplikaci Outlook. (V současné době Exchange Active Sync nepodporuje jiné podmínky než platforma zařízení). Zásady podmíněného přístupu můžete nakonfigurovat buď na portálu Azure AD, nebo na portálu Intune. Vzhledem k tomu, že se už nacházíme na portálu Intune, vytvoříme zásadu zde.  

### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>Vytvoření zásady MFA pro klienty moderních ověřování  

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost **zabezpečení koncového bodu** >  **podmíněný přístup** > **nové zásady**.  

3. Jako **název**zadejte **zásady testování pro klienty s moderním ověřováním**.  

4. V části **Přiřazení** vyberte **Uživatelé a skupiny**. Na kartě **Zahrnout** vyberte **Všichni uživatelé** a vyberte **Hotovo**.

5. V části **přiřazení**vyberte **cloudové aplikace nebo akce**. Protože chceme chránit e-mail Office 365 se službou Exchange Online, vybereme ho následujícím postupem:

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
   4. Vyberte **hotovo** > **Hotovo** a vraťte se do podokna nové zásady.

   ![Vybrat mobilní aplikace a klienti](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

8. V části **Ovládací prvky přístupu** zvolte **Udělení**.

   1. V podokně **Udělení** vyberte **Udělit přístup**.
   2. Vyberte **vyžadovat službu Multi-Factor Authentication**.
   3. Vyberte **Vyžaduje se klientem schválená aplikace**.
   4. V části **Pro více ovládacích prvků** vyberte **Vyžadovat všechny vybrané ovládací prvky**. Toto nastavení zajistí, že se při přístupu zařízení k e-mailu oba vybrané požadavky vynutí.
   5. Zvolte **Vybrat**.

   ![Výběr řízení přístupu](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

9. V části **Povolit zásadu**vyberte **zapnuto**a pak vyberte **vytvořit**.

   ![Vytvořit zásadu](./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)  

Vytvoří se zásada podmíněného přístupu pro klienty moderního ověřování. Nyní můžete vytvořit zásadu pro klienty Exchange Active Sync.

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Vytvoření zásady pro Exchange Active Sync klientů

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost **zabezpečení koncového bodu** > **podmíněný přístup** > **nové zásady**.

3. Jako **název**zadejte **zásady testování pro klienty EAS**.

4. V části **Přiřazení** vyberte **Uživatelé a skupiny**. Na kartě *Zahrnout* vyberte **Všichni uživatelé** a vyberte **Hotovo**.

5. V části **přiřazení**vyberte **cloudové aplikace nebo akce**. Vyberte e-mailovou zprávu Office 365 Exchange Online s těmito kroky:

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

   ![Vyžaduje se klientem schválená aplikace.](./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

9. V části **Povolit zásadu**vyberte **zapnuto**a pak vyberte **vytvořit**.

Vaše zásady ochrany aplikací a podmíněný přístup teď fungují a jsou připravené k testování.

## <a name="try-it-out"></a>Vyzkoušejte si to

Pomocí zásad, které jste vytvořili, se zařízení musí zaregistrovat v Intune a používat mobilní aplikaci Outlook k přístupu k e-mailu Office 365. Pokud chcete tento scénář otestovat na zařízení s iOSem, zkuste se přihlásit k Exchangi Online pomocí přihlašovacích údajů uživatele v testovacím tenantovi.

1. Pokud si chcete zásady otestovat na iPhonu, přejděte na **Nastavení** > **Hesla a účty** > **Přidat účet** > **Exchange**.

2. Zadejte e-mailovou adresu uživatele v testovacím tenantovi a stiskněte **Další**.  
3. Stiskněte **Přihlásit se**.

4. Zadejte heslo testovacího uživatele a stiskněte **Přihlásit se**.

5. Zobrazí se **Další informace, které jsou požadovány** , což znamená, že se zobrazí výzva k nastavení vícefaktorového ověřování. Pokračujte a nastavte další metodu ověřování.

6. V dalším kroku se zobrazí zpráva s informacemi o tom, že se snažíte otevřít tento prostředek, pomocí aplikace, která není schválená vaším IT oddělením. Zpráva znamená, že jste zablokovali používání aplikace v nativním e-mailu. Zrušte přihlášení.

7. Otevřete aplikaci Outlook a vyberte **nastavení** > **Přidat účet** > **Přidat e-mailový účet**.

8. Zadejte e-mailovou adresu uživatele v testovacím tenantovi a stiskněte **Další**.

9. Stiskněte tlačítko **Přihlásit se sadou Office 365**. Zobrazí se výzva k dodatečnému ověření a registraci. Po přihlášení můžete testovat akce, jako je vyjmutí, kopírování, vložení a uložit jako.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud už testovací zásady nepotřebujete, můžete je odebrat.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices** **zásady dodržování předpisů**pro zařízení.

3. V seznamu **Název zásady** vyberte u testovací zásady místní nabídku ( **...** ) a potom vyberte **Odstranit**. Vyberte **OK**. Tím akci potvrdíte.

4. Vyberte možnost **zabezpečení koncového bodu** > **podmíněný přístup**.

5. V seznamu **název zásady** vyberte kontextovou nabídku ( **...** ) pro každou ze svých zásad testování a pak vyberte **Odstranit**. Vyberte **Ano**. Tím akci potvrdíte.

## <a name="next-steps"></a>Další kroky
V tomto kurzu jste vytvořili zásady ochrany aplikací, abyste omezili to, co může uživatel dělat s aplikací Outlook, a vytvořili jste zásady podmíněného přístupu, které vyžadují aplikaci Outlook a vyžadují MFA pro klienty moderních ověřování. Další informace o používání Intune s podmíněným přístupem k ochraně dalších aplikací a služeb najdete v tématu [nastavení podmíněného přístupu](conditional-access.md).
