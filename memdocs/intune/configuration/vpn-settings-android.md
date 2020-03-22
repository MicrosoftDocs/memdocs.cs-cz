---
title: Použití nastavení sítě VPN pro zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na všechna nastavení a vytvořte připojení VPN na zařízeních s Androidem v Microsoft Intune. Zadejte název připojení, IP adresu nebo plně kvalifikovaný název domény serveru VPN, vyberte, jak se uživatelé ověřují, a vyberte Citrix, SonicWall, Check Point kapsle a typy připojení Pulse Secure.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b43b9671767a2d67bb98db6150799d266fe9fa6
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086554"
---
# <a name="android-device-settings-to-configure-vpn-in-intune"></a>Nastavení zařízení s Androidem pro konfiguraci sítě VPN v Intune

Tento článek obsahuje seznam a popis různých nastavení připojení VPN, která můžete řídit na zařízeních s Androidem. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení můžete vytvořit připojení k síti VPN, zvolit způsob ověřování sítě VPN, vybrat typ serveru sítě VPN a další.

Jako správce Intune můžete vytvořit a přiřadit nastavení sítě VPN pro zařízení s Androidem. 

Další informace o profilech sítě VPN v Intune najdete v tématu [Profily sítě VPN](vpn-settings-configure.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte konfigurační profil zařízení](vpn-settings-configure.md)a vyberte **Správce zařízení s Androidem**.

## <a name="base-vpn"></a>Základní síť VPN

- **Název připojení**: zadejte název tohoto připojení. Tento název uživatelé vidí, když na svém zařízení procházejí dostupná připojení VPN. Zadejte například `Contoso VPN`.
- **IP adresa nebo plně kvalifikovaný název domény**: zadejte IP adresu nebo plně kvalifikovaný název domény serveru VPN, ke kterému se zařízení připojí. Zadejte například **192.168.1.1** nebo **vpn.contoso.com**.

  - **Metoda ověřování**: Zvolte způsob, kterým se zařízení ověřují vůči serveru VPN. Možnosti:

    - **Certifikáty**: Vyberte existující profil certifikátu SCEP nebo PKCS pro ověřování připojení. [Konfigurace certifikátů](../protect/certificates-configure.md) obsahuje kroky pro vytvoření profilu certifikátu.
    - **Uživatelské jméno a heslo**: když se přihlásíte k serveru VPN, koncovým uživatelům se zobrazí výzva k zadání uživatelského jména a hesla.

- **Typ připojení**: Vyberte typ připojení VPN. Možnosti:

  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **Přístup F5**
  - **Pulse Secure**
  - **Citrix SSO**

- **Otisk prstu** (pouze Check Point Capsule VPN): Zadejte řetězec, například **Kód otisku prstu Contoso**, který se použije k ověření, že serveru VPN je možné důvěřovat. Do klienta se pošle otisk prstu, aby klient věděl, že bude důvěřovat jakémukoli serveru, který má stejný otisk prstu. Pokud zařízení otisk prstu nemá, vyzve uživatele, aby při zobrazování otisku prstu důvěřoval serveru VPN. Uživatel ručně ověří otisk prstu a rozhodne se důvěřovat pro připojení.
- **Zadejte páry klíč-hodnota pro atributy Citrix VPN** (pouze Citrix): Zadejte páry klíče a hodnoty, které poskytl Citrix. Tyto hodnoty nakonfigurují vlastnosti připojení VPN. 

  Soubor hodnot oddělených čárkami (. csv) můžete také **importovat** s páry klíče a hodnoty. Nezapomeňte zkontrolovat, že **data obsahují záhlaví** a vlastnosti **klíče** .

  Po přidání párů klíč a hodnoty použijte **Export** k zálohování dat do souboru. csv.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily sítě VPN pro zařízení s [Androidem Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md), [MacOS](vpn-settings-macos.md), [Windows 10 a novějším](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md)a [Windows Phone 8,1](vpn-settings-windows-phone-8-1.md) .
