---
title: Konfigurace nastavení sítě VPN pro zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte konfigurační profil virtuální privátní sítě (VPN), včetně podrobností o připojení, děleného tunelového propojení, vlastního nastavení sítě VPN s identifikátorem, páry klíč-hodnota, nastavení serveru proxy pomocí konfiguračního skriptu, IP adresy nebo adresy plně kvalifikovaného názvu domény a portu TCP v Microsoft Intune na zařízeních s macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0db4187540c671bf985de9c6c52524280ad2d06
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331895"
---
# <a name="add-vpn-settings-on-macos-devices-in-microsoft-intune"></a>Přidat nastavení sítě VPN na zařízení macOS v Microsoft Intune



Tento článek popisuje, jaká nastavení můžete v Intune použít ke konfiguraci připojení VPN na zařízeních s macOS.

V závislosti na tom, jaká nastavení zvolíte, nebudou v následujícím seznamu konfigurovatelné všechny hodnoty.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](vpn-settings-configure.md).

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="base-vpn-settings"></a>Základní nastavení sítě VPN

**Název připojení**: zadejte název tohoto připojení. Tento název uživatelé vidí, když na svém zařízení procházejí seznamem dostupných připojení VPN.
- **IP adresa nebo plně kvalifikovaný**název domény: zadejte IP adresu nebo plně kvalifikovaný název domény serveru VPN, ke kterému se zařízení připojují. Příklady: **192.168.1.1**, **vpn.contoso.com**.
- **Metoda ověřování**: zvolte způsob, kterým se zařízení ověřují vůči serveru VPN:
  - **Certifikáty**: v části **ověřovací certifikát**vyberte profil certifikátu SCEP nebo PKCS, který jste dříve vytvořili za účelem ověřování připojení. Další informace o profilech certifikátů najdete v článku [Konfigurace certifikátů](../protect/certificates-configure.md).
  - **Uživatelské jméno a heslo**: koncoví uživatelé musí pro přihlášení k serveru VPN uvést uživatelské jméno a heslo.
- **Typ připojení**: z následujícího seznamu dodavatelů vyberte typ připojení VPN:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**
  - **Vlastní VPN**
- **Dělené tunelové propojení**: **povolí** nebo **zakáže** tuto možnost, která umožňuje zařízením rozhodnout, které připojení se má použít v závislosti na provozu. Uživatel v hotelu například pro přístup k pracovním souborům použije připojení VPN, ale pro běžné procházení webu bude používat standardní síť hotelu.

<!--- **Per-app VPN** - Select this option if you want to associate this VPN connection with an iOS/iPadOS or macOS app so that the connection will be opened when the app is run. You can associate the VPN profile with an app when you assign the software. For more information, see [How to assign and monitor apps](../apps/apps-deploy.md). --->

## <a name="custom-vpn-settings"></a>Vlastní nastavení sítě VPN

Pokud jste vybrali **Vlastní VPN**, nakonfigurujte tato další nastavení:

- **Identifikátor sítě VPN**: zadejte identifikátor aplikace VPN, kterou používáte. Tento identifikátor poskytuje poskytovatel sítě VPN.
- **Zadejte páry klíč-hodnota pro vlastní atributy VPN**: přidejte nebo naimportujte **klíče** a **hodnoty**, pomocí nichž si přizpůsobíte připojení VPN. Tyto hodnoty obvykle poskytuje poskytovatel sítě VPN.

## <a name="proxy-settings"></a>Nastavení proxy serveru

- **Skript automatické konfigurace**: ke konfiguraci proxy serveru použijte konfigurační soubor. Zadejte **adresu URL proxy serveru** , který obsahuje konfigurační soubor. Zadejte například `http://proxy.contoso.com`.
- **Adresa**: zadejte adresu proxy server (jako IP adresu).
- **Číslo portu**: Zadejte číslo portu přidruženého k proxy serveru.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Nakonfigurujte nastavení sítě VPN na zařízeních se systémem [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md)a [Windows 10](vpn-settings-windows-10.md) .
