---
title: Přesunutí zařízení s Androidem ze Správce zařízení do správy pracovního profilu
titleSuffix: Microsoft Intune
description: Přesuňte zařízení s Androidem ze Správce zařízení do správy pracovních profilů v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 685f2a51c7a2bfacbc95fb2a7615f0e459b97245
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126511"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Přesunutí zařízení s Androidem ze Správce zařízení do správy pracovního profilu

Uživatelům můžete pomoci přesunout zařízení s Androidem ze Správce zařízení do správy pracovních profilů pomocí nastavení dodržování předpisů pro **blokování zařízení spravovaných správcem zařízení**. Toto nastavení umožňuje nastavit nekompatibilní zařízení, pokud jsou spravovaná pomocí Správce zařízení. 

Když uživatelé uvidí, že z tohoto důvodu nejsou v souladu s předpisy, můžou klepnout na **vyřešit**. Budou provedeny v kontrolním seznamu, který je provede:
1. Rušení registrace správy správců zařízení
2. Registrace do správy pracovního profilu
3. Řešení problémů s dodržováním předpisů. 

## <a name="prerequisites"></a>Požadavky

- Uživatelé musí mít [zařízení zaregistrovaná správcem zařízení](android-enroll-device-administrator.md) s androidem portál společnosti verze 5.0.4720.0 nebo novější.
- Nastavte správu pracovního profilu Androidu [připojením účtu tenanta Intune k vašemu účtu Android Enterprise](connect-intune-android-enterprise.md).
- [Nastavte registraci pracovního profilu Android Enterprise](android-work-profile-enroll.md) pro skupinu uživatelů, kteří přesunou na pracovní profil Android.
- Zvažte zvýšení omezení vašich uživatelských zařízení. Při rušení registrace zařízení ze správy správců zařízení nemusí být záznamy zařízení okamžitě odebrány. Aby bylo možné během této doby poskytnout polštář, možná budete muset zvýšit kapacitu omezení počtu zařízení, aby se uživatelé mohli zaregistrovat do správy pracovního profilu.
  - [Nakonfigurujte Azure Active Directory nastavení zařízení](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) pro maximální počet zařízení na uživatele.
  - Nastavením limitu zařízení nastavte [omezení počtu zařízení v Intune](enrollment-restrictions-set.md#create-a-device-limit-restriction) . 

## <a name="create-device-compliance-policy"></a>Vytvoření zásad dodržování předpisů pro zařízení

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**zásady  >  **zásad dodržování předpisů**  >  **Policies**  >  **vytvořit zásadu**.

    ![Vytvoření zásad](./media/android-move-device-admin-work-profile/create-policy.png)

2. Na stránce **vytvořit zásadu** nastavte nastavení **platforma** na **Správce zařízení s Androidem**  >  **vytvořit**.
3. Na stránce **základy** zadejte **název** a **Popis**  >  **Další**.

    ![Stránka základy](./media/android-move-device-admin-work-profile/basics.png)
    
4. Na stránce **Nastavení dodržování předpisů** v části **stav zařízení** nastavte možnost **blokovat zařízení spravovaná pomocí Správce zařízení** na **Ano**  >  **Další**.

    ![Blokovat zařízení](./media/android-move-device-admin-work-profile/block-devices.png)

5. Na stránce **umístění** můžete přidat umístění, pokud chcete > **Další**.

6. Na kartě **Akce při nedodržení předpisů** můžete nakonfigurovat [Dostupné akce při nedodržení předpisů](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) pro přizpůsobení prostředí koncových uživatelů pro tento tok.

    ![Akce při nedodržení předpisů](media/android-move-device-admin-work-profile/noncompliance-actions.png)

    Jedná se o některé akce, které je potřeba vzít v úvahu:

    - **Označit zařízení jako nevyhovující**: ve výchozím nastavení je tato akce nastavená na nula (0) dnů a okamžitě se zařízení označí jako nedodržující předpisy. Změna tohoto počtu na více dní poskytuje uživatelům dobu odkladu, ve které můžou sledovat tok, který se přesune ke správě pracovních profilů, aniž by se ještě označil jako nedodržující předpisy. Například nastavení na hodnotu 14 dní uživateli poskytne dva týdny, aby se přesunuli od správce zařízení do správy pracovních profilů bez rizika ztráty přístupu k prostředkům.
    - **Odeslat nabízená oznámení koncovému uživateli**: tuto konfiguraci nakonfigurujte pro odesílání nabízených oznámení do zařízení Správce zařízení. Když uživatel vybere oznámení, spustí Portál společnosti pro Android na stránce **aktualizovat nastavení zařízení** , kde může spustit tok pro přesun do správy pracovního profilu.
    - **Odeslat e-mail koncovému uživateli**: tuto možnost nakonfigurujte, pokud chcete uživatelům odeslat e-maily o přesunutí ze Správce zařízení do správy pracovního profilu. Do e-mailu můžete zahrnout níže uvedenou adresu URL, která je v případě, že ji vyberete, spustí Portál společnosti pro Android na stránce aktualizovat nastavení zařízení, kde může spustit tok pro přesun do správy pracovního profilu.
      - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
      - Pro státní správu USA můžete místo toho použít tento odkaz: `https://portal.manage.microsoft.us/UpdateSettings.aspx` .
  
      > [!NOTE]
      > - Samozřejmě můžete použít uživatelsky přívětivý text Hyper-v propojeních ve vaší komunikaci s uživateli. Nepoužívejte však zkrácení adres URL, protože odkazy nemusí fungovat, pokud se tímto způsobem změní.
      > - Pokud je Android Portál společnosti otevřený a na pozadí, když uživatel klepne na odkaz, může místo toho přejít na poslední stránku, kterou otevřeli.
      > - Uživatelé musí klepnout na odkaz na zařízení s Androidem. Pokud je místo toho vložíte do prohlížeče, nespustí se Portál společnosti pro Android. 

    Zvolte **Další**.

7. Na stránce **značky oboru** vyberte libovolné značky oboru, které chcete zahrnout.
8. Na stránce **přiřazení** přiřaďte zásadu ke skupině, která má zařízení zaregistrovaná pomocí správy správce zařízení > **Další**.
9. Na stránce **Revize + vytvořit** potvrďte všechna nastavení a potom vyberte **vytvořit**.

## <a name="troubleshooting"></a>Řešení potíží

[Tok koncového uživatele, který se má přesunout do nového nastavení správy zařízení](../user-help/move-to-new-device-management-setup.md) , provede uživatele tím, že zruší registraci ze správy Správce zařízení a nastavuje se pomocí správy pracovního profilu. Uživatelé musí mít [zařízení zaregistrovaná správcem zařízení](android-enroll-device-administrator.md) s androidem portál společnosti verze 5.0.4720.0 nebo novější.

### <a name="user-sees-an-error-after-tapping-resolve"></a>Uživatel uvidí chybu po klepnutí na vyřešit.
Pokud se uživatelům po klepnutí na tlačítko **vyřešit** zobrazí chyba, je pravděpodobně příčinou jednoho z následujících důvodů:
- Registrace pracovního profilu není správně nastavená (účet Androidu Enterprise není připojený nebo omezení registrace se nastaví tak, aby se zablokoval zápis pracovního profilu).
- Na zařízení běží Android 4,4 nebo starší, což nepodporuje registraci pracovního profilu. 
- Výrobce zařízení nepodporuje registraci pracovního profilu v modelu zařízení.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>Tlačítko vyřešit se nezobrazuje na zařízení uživatele
Tlačítko **vyřešit** se nezobrazí na zařízení uživatele, pokud se uživatel zaregistruje do správy správců zařízení po jejich zaměření na zásady dodržování předpisů zařízením popsané výše.

Aby se zobrazilo tlačítko **vyřešit** , musí uživatel odložit instalaci a restartovat proces z oznámení.

Abyste se vyhnuli této situaci, pomocí omezení registrace zablokujte registraci do správy správců zařízení.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>Po klepnutí na adresu URL, která aktualizuje stránku nastavení zařízení, se uživateli zobrazí chyba
Uživatelům se v prohlížeči může zobrazit chybová stránka, když klepnou na **stránce aktualizovat nastavení zařízení** portál společnosti pro Android. Tato chyba může být způsobena jedním z následujících způsobů:
- Zařízení není Android.
- Zařízení s Androidem nemá aplikaci Portál společnosti.
- Verze Portál společnosti pro Android je starší než 5.0.4720.0.
- Zařízení s Androidem používá Android 6 nebo starší. 

## <a name="next-steps"></a>Další kroky
[Zobrazit tok](../user-help/move-to-new-device-management-setup.md) 
 koncového uživatele [Správa zařízení s pracovním profilem Androidu pomocí Intune](android-enterprise-overview.md)
