---
title: Nastavení profilu připojení k doméně pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte konfigurační profil zařízení připojit k doméně pro zařízení připojená k hybridní službě Azure AD. Pomocí tohoto profilu můžete nasadit místní informace o doméně služby Active Directory do zařízení zřízených pomocí automatického pilotního nasazení systému Windows a Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2472354c4f1c6b704f1e681c3e839f9903d4d079
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912759"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Nastavení připojení k doméně konfigurace pro zařízení připojená k hybridní službě Azure AD v Microsoft Intune

Mnoho prostředí používá místní službu Active Directory (AD). Když jsou zařízení připojená k doméně připojená také k Azure AD, nazývají se zařízení připojená k hybridní službě Azure AD. Pomocí automatických pilotů Windows můžete [zaregistrovat zařízení připojená k hybridní službě Azure AD](../../autopilot/windows-autopilot-hybrid.md) v Intune. K registraci budete potřebovat taky konfigurační profil **připojení k doméně** .

Konfigurační profil **připojení k doméně** zahrnuje místní informace o doméně služby Active Directory. Při zřizování zařízení (a obvykle offline) Tento profil nasadí podrobnosti o doméně služby AD, aby zařízení věděli, která místní doména se mají připojit. Pokud nevytvoříte profil připojení k doméně, možná se tato zařízení nepodaří nasadit.

Tato funkce platí pro:

- Windows 10 a novější
- Hybridní zařízení připojená k Azure AD
- Hybridní nasazení pomocí autopilotu a Intune

V tomto článku se dozvíte, jak vytvořit profil připojení k doméně pro nasazení Hybrid autopilotu. Můžete si také prohlédnout dostupná nastavení.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **připojení k doméně (Preview)**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **Windows 10: Profil připojení k doméně, který obsahuje informace o místní doméně k registraci zařízení připojených k hybridní službě AD pomocí automatického pilotního projektu Windows**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**zadejte následující vlastnosti:

    - **Předpona názvu počítače**: Zadejte předponu názvu zařízení. Názvy počítačů mají délku 15 znaků. Po předponě se budou náhodně generovat zbylé 15 znaků.
    - **Název domény**: zadejte plně kvalifikovaný název domény (FQDN), ke které se mají zařízení připojit. Zadejte například `americas.corp.contoso.com.`
    - **Organizační jednotka** (volitelné): zadejte úplnou cestu ([rozlišující název](/windows/win32/ad/object-names-and-identities#distinguished-name)) k organizační jednotce (OU), které se mají vytvořit účty počítačů. Zadejte například `"CN=Users,DC=Contoso,DC=com"`. Pokud nezadáte hodnotu, použije se dobře známý kontejner objektů počítače.

      Další informace a Rady k tomuto nastavení najdete v tématu [nasazení hybridních zařízení připojených k Azure AD](../../autopilot/windows-autopilot-hybrid.md).

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupinu uživatelů, kteří obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Nyní je připraven k [nasazení hybridních zařízení připojených k Azure AD pomocí Intune a Windows autopilotu](../../autopilot/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Další kroky

Po [přiřazení](device-profile-assign.md)profilu [sledujte jeho stav](device-profile-monitor.md).

[Nasaďte hybridní zařízení připojená k Azure AD pomocí Intune a Windows autopilotu](../../autopilot/windows-autopilot-hybrid.md).