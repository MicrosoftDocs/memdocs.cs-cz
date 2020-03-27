---
title: Kurz – konfigurace časové rezervy pro používání služby Intune pro modul EMM a konfiguraci aplikací
titleSuffix: Microsoft Intune
description: V tomto kurzu nakonfigurujete časovou rezervu, která bude používat Intune pro modul EMM a konfiguraci aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 55db37c5-0da7-4d9c-8027-525afb1c6349
Customer intent: As an Intune admin, I want to learn how to configure Slack to use Intune for EMM and app configuration..
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 556381337b225640f25d2e3adf86dde5ed428273
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325683"
---
# <a name="tutorial-configure-slack-to-use-intune-for-emm-and-app-configuration"></a>Kurz: Konfigurace časové rezervy pro používání služby Intune pro modul EMM a konfiguraci aplikací

Časová rezerva je aplikace pro spolupráci, kterou můžete použít s Microsoft Intune.   

V tomto kurzu se naučíte:
> [!div class="checklist"]
> - Nastavte Intune jako poskytovatele podnikové mobility (EMM) v podnikové mřížce s časovou rezervou. V zařízeních spravovaných přes Intune budete moct omezit přístup k pracovním prostorům plánu vaší mřížky.
> - Vytvořte zásady konfigurace aplikací pro správu časové rezervy aplikace EMM na zařízeních iOS/iPadOS a aplikaci časové rezervy pro zařízení s pracovním profilem Androidu.
> - Vytvoření zásad dodržování předpisů pro zařízení v Intune pro nastavení podmínek, které musí zařízení s Androidem a iOS/iPadOS splňovat, aby se dalo považovat za vyhovující.

Pokud nemáte předplatné Intune, [zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky
Pro účely tohoto kurzu budete potřebovat testovacího tenanta s následujícími předplatnými:
- Azure Active Directory Premium ([bezplatná zkušební verze](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Předplatné Intune ([bezplatná zkušební verze](../fundamentals/free-trial-sign-up.md))

Budete také potřebovat plán [podnikové mřížky s časovou rezervou](https://get.slack.help/hc/articles/360004150931-What-is-Slack-Enterprise-Grid-) .

## <a name="configure-your-slack-enterprise-grid-plan"></a>Konfigurace plánu podnikové mřížky pro časové rezervy
Pomocí [pokynů pro časovou rezervu](https://get.slack.help/hc/articles/115002579426-Enable-Enterprise-Mobility-Management-for-your-org#step-2:-turn-on-emm) zapněte modul EMM pro plán podnikové mřížky s časovou rezervou a [Připojte Azure Active Directory](https://docs.microsoft.com/azure/active-directory/saas-apps/slack-tutorial) jako zprostředkovatele identity (IDP) vašeho plánu.

## <a name="sign-in-to-intune"></a>Přihlášení k Intune
Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako globální správce nebo správce služby Intune. Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="set-up-slack-for-emm-on-ios-devices"></a>Nastavení časové rezervy pro modul EMM na zařízeních s iOS
Přidejte pro modul EMM do svého tenanta Intune časovou rezervu aplikace pro iOS/iPadOS a vytvořte zásadu konfigurace aplikace, která umožní vašim organizacím uživatelům iOS/iPadOS povolit přístup k časové rezervě v Intune jako poskytovatel EMM.

### <a name="add-slack-for-emm-to-intune"></a>Přidání časové rezervy pro modul EMM do Intune
Přidejte do Intune časovou rezervu pro modul EMM jako spravovanou aplikaci pro iOS/iPadOS a přiřaďte uživatele časové rezervy. Aplikace jsou specifické pro platformu, takže potřebujete přidat samostatnou aplikaci Intune pro uživatele časové rezervy na zařízeních s Androidem.
1. V centru pro správu vyberte **aplikace** > **všechny aplikace** > **Přidat**.
2. V části **Typ aplikace**vyberte aplikace pro **iOS** Store.
3. Vyberte **Hledat v App Storu**. Zadejte hledaný termín "časová rezerva pro modul EMM" a vyberte aplikaci. V podokně Hledat v **App Storu** klikněte na **Vybrat** .
4. Vyberte **informace o aplikaci** a podle potřeby nakonfigurujte libovolné změny. Vyberte **OK** a nastavte informace o aplikaci.
5. Klikněte na **Přidat**.
6. Zvolte **Přiřazení**.
7. Klikněte na **Přidat skupinu**. V závislosti na tom, na koho jste se zapnuli, když zapnete modul EMM pro časovou rezervu, vyberte v části **Typ přiřazení** , který chcete vybrat:
    - **K dispozici pro zaregistrovaná zařízení** , pokud jste zvolili "Všichni členové (včetně hostů)" nebo
    - **K dispozici s registrací nebo bez registrace** , pokud jste vybrali "Všichni členové (kromě hostů)" nebo "volitelné".
8. Vyberte **zahrnuté skupiny** a v části **zpřístupnit tuto aplikaci všem uživatelům** vyberte **Ano**.
9. Klikněte na **OK**a potom znovu klikněte na **OK** a přidejte skupinu.
10. Klikněte na **Uložit**.

### <a name="add-an-app-configuration-policy-for-slack-for-emm"></a>Přidání zásad konfigurace aplikace pro časovou rezervu pro modul EMM
Přidejte zásady konfigurace aplikace pro tuto časovou rezervu pro modul EMM iOS/iPadOS. Zásady konfigurace aplikací pro spravovaná zařízení jsou specifické pro konkrétní platformu, takže musíte přidat samostatnou zásadu pro uživatele časové rezervy na zařízeních s Androidem.
1. V centru pro správu vyberte **aplikace** > **zásady konfigurace aplikací** > **Přidat** > **spravovaná zařízení**.
2. Do název zadejte ' test zásad konfigurace aplikace pro časovou rezervu '.
3. V části typ registrace zařízení potvrďte, že je nastavená **spravovaná zařízení** .
4. V části platforma vyberte **iOS**.
5. Vyberte **přidružená aplikace**.
6. Na panelu hledání zadejte "časová rezerva pro modul EMM" a vyberte aplikaci.
7. Klikněte na **OK**a pak vyberte **nastavení konfigurace**. 
8. Vyberte **OK**a pak vyberte **Přidat**.
9. Na panelu hledání zadejte "test zásad konfigurace aplikace pro časovou rezervu" a vyberte zásadu, kterou jste právě přidali.
10. V možnosti Spravovat vyberte **přiřazení**.
11. V části přiřadit k vyberte **Všichni uživatelé a všechna zařízení**.
12. Klikněte na **Uložit**.

### <a name="optional-create-an-ios-device-compliance-policy"></a>Volitelné Vytvoření zásady dodržování předpisů pro zařízení s iOS
Nastavte zásadu dodržování předpisů zařízením s iOSem v Intune a nastavte podmínky, které zařízení musí splnit, než bude považováno za vyhovující. Pro tento kurz vytvoříme zásadu dodržování předpisů pro zařízení s iOS/iPadOS. Zásady dodržování předpisů jsou specifické pro konkrétní platformu, takže musíte vytvořit samostatnou zásadu pro uživatele časové rezervy na zařízeních s Androidem.
1. V centru pro správu vyberte **zásady** > **dodržování předpisů zařízením** > **vytvořit zásadu**.
2. Do název zadejte "test zásad dodržování předpisů pro iOS".
3. V části Popis zadejte "test zásad dodržování předpisů pro iOS".
4. V části platforma vyberte **iOS**.
5. Vyberte **Stav zařízení**. V poli zařízení s jailbreakem vyberte **blokovat**a pak vyberte **OK**.
6. Vyberte **zabezpečení systému** a zadejte nastavení hesla. Pro účely tohoto kurzu vyberte následující doporučená nastavení:
    - Pro možnost vyžadovat heslo k odemknutí mobilních zařízení vyberte **vyžadovat**.
    - V případě jednoduchých hesel vyberte **blokovat**.
    - Pro minimální délku hesla zadejte 4.
    - V případě požadovaného typu hesla vyberte možnost **alfanumerické**.
    - Po maximálním počtu minut po uzamknutí obrazovky před zadáním hesla vyberte možnost **okamžitě**.
    - Do vypršení platnosti hesla (dny) zadejte 41.
    - Pokud chcete zabránit opakovanému použití, zadejte pro počet předchozích hesel 5.
7. Klikněte na **OK**a pak znovu vyberte **OK** .
8. Klikněte na **Vytvořit**.

## <a name="set-up-slack-on-android-work-profile-devices"></a>Nastavení časové rezervy pro zařízení s pracovním profilem Androidu
Přidejte do svého tenanta Intune spravovanou aplikaci Google Playovou časovou rezervu a vytvořte zásadu konfigurace aplikace, která uživatelům s Androidem umožní přístup k časové rezervě v Intune jako poskytovatel EMM.

### <a name="add-slack-to-intune"></a>Přidání časové rezervy do Intune
Přidejte časovou rezervu jako spravovanou aplikaci Google Play do Intune a přiřaďte uživatele časové rezervy. Aplikace jsou specifické pro platformu, takže potřebujete přidat samostatnou aplikaci Intune pro uživatele časové rezervy na zařízeních s iOS/iPadOS.
1. V Intune vyberte **aplikace** > **všechny aplikace** > **Přidat**.
2. V části Typ aplikace vyberte **Store app – spravovaná Google Play**.
3. Vyberte **spravované Google Play-schvalovat**. Zadejte hledaný termín "časová rezerva pro modul EMM" a vyberte aplikaci.
4. Vyberte **schválit**.
5. Na panelu hledání zadejte "časová rezerva" a vyberte aplikaci, kterou jste právě přidali.
6. V možnosti Spravovat vyberte **přiřazení**.
7. Vyberte **Přidat skupinu**. V závislosti na tom, na koho jste se zapnuli, když zapnete modul EMM pro časovou rezervu, vyberte v části **Typ přiřazení** , který chcete vybrat:
    - **K dispozici pro zaregistrovaná zařízení** , pokud jste zvolili "Všichni členové (včetně hostů)" nebo
    - **K dispozici s registrací nebo bez registrace** , pokud jste vybrali "Všichni členové (kromě hostů)" nebo "volitelné".
8. Vyberte zahrnuté skupiny a v části zpřístupnit tuto aplikaci všem uživatelům vyberte **Ano**.
9. Klikněte na **OK**a pak znovu na **OK** .
10. Klikněte na **Uložit**.

### <a name="add-an-app-configuration-policy-for-slack"></a>Přidání zásad konfigurace aplikace pro časovou rezervu
Přidejte zásady konfigurace aplikace pro časovou rezervu. Zásady konfigurace aplikací pro spravovaná zařízení jsou specifické pro konkrétní platformu, takže musíte přidat samostatnou zásadu pro uživatele časové rezervy na zařízeních s iOS/iPadOS.
1. V Intune vyberte **aplikace** > **zásady konfigurace aplikací** > **Přidat**.
2. Do název zadejte Test zásad konfigurace aplikace pro časovou rezervu.
3. V části typ registrace zařízení vyberte **spravovaná zařízení**.
4. V části platforma vyberte **Android**.
5. Vyberte **přidružená aplikace**.
6. Na panelu hledání zadejte "časová rezerva" a vyberte aplikaci.
7. Vyberte **OK**a pak vyberte **nastavení konfigurace**.
    - Informace o konfiguračních klíčích a jejich hodnotách najdete v dokumentaci na [webové stránce appconfig časové rezervy](https://www.appconfig.org/company/slack/)na kartě Technical.
8. Klikněte na **OK**a pak vyberte **Přidat**.
9. Na panelu hledání zadejte "test zásad konfigurace aplikace pro časovou rezervu" a vyberte zásadu, kterou jste právě přidali.
10. V možnosti Spravovat vyberte **přiřazení**.
11. V části přiřadit k vyberte **Všichni uživatelé a všechna zařízení**.
12. Klikněte na **Uložit**.

### <a name="optional-create-an-android-device-compliance-policy"></a>Volitelné Vytvoření zásad dodržování předpisů pro zařízení s Androidem
Nastavte zásadu dodržování předpisů zařízením s iOSem v Intune a nastavte podmínky, které zařízení musí splnit, než bude považováno za vyhovující. Pro tento kurz vytvoříme zásady dodržování předpisů pro zařízení s Androidem. Zásady dodržování předpisů jsou specifické pro konkrétní platformu, takže potřebujete vytvořit samostatnou zásadu pro uživatele časové rezervy na zařízeních s iOS/iPadOS.
1. V Intune vyberte **Dodržování předpisů zařízením** > **Zásady** > **Vytvořit zásadu**.
2. Do název zadejte "test zásad dodržování předpisů pro Android".
3. V části Popis zadejte "test zásad dodržování předpisů pro Android".
4. V části platforma vyberte **Android Enterprise**.
5. V části Typ profilu vyberte **pracovní profil**.
6. Vyberte **Stav zařízení**. U zařízení s rootem vyberte **blokovat**a pak vyberte **OK**.
7. Vyberte **zabezpečení systému** a zadejte **Nastavení hesla**. Pro účely tohoto kurzu vyberte následující doporučená nastavení:
    - Pro možnost vyžadovat heslo k odemknutí mobilních zařízení vyberte **vyžadovat**.
    - Pro požadovaný typ hesla vyberte **aspoň alfanumerické znaky**.
    - Pro minimální délku hesla zadejte 4.
    - Po maximálním počtu minut po uzamčení obrazovky, než se vyžaduje heslo, vyberte **15 minut**.
    - Do vypršení platnosti hesla (dny) zadejte 41.
    - Pokud chcete zabránit opakovanému použití, zadejte pro počet předchozích hesel 5.
8. Klikněte na **OK**a pak znovu na **OK** .
9. Klikněte na **Vytvořit**.

## <a name="launch-slack"></a>Časová rezerva spuštění

Díky zásadám, které jste právě vytvořili, se všechna zařízení pracovních profilů s iOS/iPadOS nebo Androidem, která se pokusí přihlásit k některému z vašich pracovních prostorů, musí být zaregistrovaná v Intune. K otestování tohoto scénáře zkuste spustit časovou rezervu pro modul EMM na zařízení se systémem iOS/iPadOS zaregistrovaným v Intune nebo na základě časové rezervy na zaregistrovaném zařízení pracovního profilu Androidu Intune. 

## <a name="next-steps"></a>Další kroky

V tomto kurzu:
- Intune nastavíte jako poskytovatele služby Enterprise mobility (EMM) v podnikové mřížce s časovou rezervou. 
- Zásady konfigurace aplikací jste vytvořili pro správu časové rezervy aplikace EMM na zařízeních iOS/iPadOS a v aplikaci časové rezervy pro zařízení s pracovním profilem Androidu.
- Vytvořili jste zásady dodržování předpisů pro zařízení v Intune, abyste mohli nastavit podmínky, které musí zařízení s Androidem a iOS/iPadOS splňovat.

Další informace o zásadách konfigurace aplikací najdete v tématu [zásady konfigurace aplikací pro Microsoft Intune](app-configuration-policies-overview.md). Další informace o zásadách dodržování předpisů pro zařízení najdete v tématu [Nastavení pravidel na zařízeních pro povolení přístupu k prostředkům ve vaší organizaci pomocí Intune](../protect/device-compliance-get-started.md).
