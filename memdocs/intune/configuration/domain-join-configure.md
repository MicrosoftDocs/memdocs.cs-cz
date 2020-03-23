---
title: Nastavení profilu připojení k doméně pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte konfigurační profil zařízení připojit k doméně pro zařízení připojená k hybridní službě Azure AD. Pomocí tohoto profilu můžete nasadit místní informace o doméně služby Active Directory do zařízení zřízených pomocí automatického pilotního nasazení systému Windows a Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333111"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Nastavení připojení k doméně konfigurace pro zařízení připojená k hybridní službě Azure AD v Microsoft Intune

Mnoho prostředí používá místní službu Active Directory (AD). Když jsou zařízení připojená k doméně připojená také k Azure AD, nazývají se zařízení připojená k hybridní službě Azure AD. Pomocí automatických pilotů Windows můžete [zaregistrovat zařízení připojená k hybridní službě Azure AD](../enrollment/windows-autopilot-hybrid.md) v Intune. K registraci budete potřebovat taky konfigurační profil **připojení k doméně** .

Konfigurační profil **připojení k doméně** zahrnuje místní informace o doméně služby Active Directory. Při zřizování zařízení (a obvykle offline) Tento profil nasadí podrobnosti o doméně služby AD, aby zařízení věděli, která místní doména se mají připojit. Pokud nevytvoříte profil připojení k doméně, možná se tato zařízení nepodaří nasadit.

Tato funkce platí pro:

- Windows 10 a novější
- Zařízení připojená k hybridní službě Azure AD
- Hybridní nasazení pomocí autopilotu a Intune

V tomto článku se dozvíte, jak vytvořit profil připojení k doméně pro nasazení Hybrid autopilotu. Můžete si také prohlédnout dostupná nastavení.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **Windows 10: Profil připojení k doméně, který obsahuje informace o místní doméně k registraci zařízení připojených k hybridní službě AD pomocí automatického pilotního projektu Windows**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Typ profilu**: vyberte **připojení k doméně (Preview)** .

4. Vyberte **Nastavení**. Zadejte následující vlastnosti:

    - **Předpona názvu počítače**: Zadejte předponu názvu zařízení. Názvy počítačů mají délku 15 znaků. Po předponě se budou náhodně generovat zbylé 15 znaků.
    - **Název domény**: zadejte plně kvalifikovaný název domény (FQDN), ke které se mají zařízení připojit. Zadejte například `americas.corp.contoso.com.`
    - **Organizační jednotka** (volitelné): zadejte úplnou cestu ([rozlišující název](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) k organizační jednotce (OU), které se mají vytvořit účty počítačů. Zadejte například `"CN=Users,DC=Contoso,DC=com"`. Pokud nezadáte hodnotu, použije se dobře známý kontejner objektů počítače.

      Další informace a Rady k tomuto nastavení najdete v tématu [nasazení hybridních zařízení připojených k Azure AD](../enrollment/windows-autopilot-hybrid.md).

5. Až to budete mít, vyberte **OK** > **Vytvořit** a změny uložte.

Profil se vytvoří a zobrazí se v seznamu profily. Nyní je připraven k [nasazení hybridních zařízení připojených k Azure AD pomocí Intune a Windows autopilotu](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Další kroky

Profil je po vytvoření připravený k přiřazení. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

[Nasaďte hybridní zařízení připojená k Azure AD pomocí Intune a Windows autopilotu](../enrollment/windows-autopilot-hybrid.md).