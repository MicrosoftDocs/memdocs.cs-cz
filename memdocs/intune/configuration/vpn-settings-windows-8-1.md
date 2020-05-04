---
title: Konfigurace nastavení sítě VPN na zařízeních Windows 8.1 v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte konfigurační profil sítě VPN pomocí nastavení konfigurace virtuální privátní sítě (VPN), včetně podrobností o připojení, a nastavení proxy serveru pro zahrnutí IP adresy nebo adresy FQDN a portu TCP v Microsoft Intune na zařízeních s Windows 8.1.
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
ms.openlocfilehash: 2c80bf57b195d7e97308ba423c9e5b53f7e29c74
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086473"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Přidat nastavení sítě VPN na zařízeních Windows 8.1 v Microsoft Intune

Tento článek popisuje, jaká nastavení můžete v Intune použít ke konfiguraci připojení VPN na zařízeních s Windows 8.1.

V závislosti na tom, jaká nastavení zvolíte, nebudou v následujícím seznamu konfigurovatelné všechny hodnoty.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Základní nastavení sítě VPN

- **Použít všechna nastavení jenom na Windows 8.1**: nakonfigurujte toto nastavení na klasickém portálu Intune. V centru pro správu Microsoft Endpoint Manageru toto nastavení nejde změnit. Při nastavení **Konfigurace**se všechna nastavení aplikují jenom na zařízení Windows 8.1. Pokud je nastavené na **Nenakonfigurováno**, tato nastavení se vztahují také na zařízení s Windows 10.
- **Název připojení**: zadejte název tohoto připojení. Tento název uživatelé vidí, když na svém zařízení procházejí seznamem dostupných připojení VPN.
- **Servery**: přidejte minimálně jeden VPN server, ke kterému se budou zařízení připojovat.
  - **Přidat**: otevře stránku **Přidat řádek** , kde můžete zadat následující informace:
    - **Popis**: zadejte popisný název serveru, jako je **Contoso VPN server**.
    - **IP adresa nebo plně kvalifikovaný**název domény: zadejte IP adresu nebo plně kvalifikovaný název domény serveru VPN, ke kterému se zařízení připojují. Příklady: **192.168.1.1**, **VPN.contoso.com**.
    - **Výchozí server**: povolí tento server jako výchozí server, který budou zařízení používat k navázání připojení. Jako výchozí server musí být nastavený jenom jeden server.
  - **Importovat**: vyhledejte soubor s oddělovači se seznamem serverů ve formátu popis, IP adresa nebo plně kvalifikovaný název domény, výchozí server. Pomocí **OK** servery naimportujte do seznamu **Servery**.
  - **Export**: exportuje seznam serverů do textového souboru s oddělovači (CSV).

- **Typ připojení**: z následujícího seznamu dodavatelů vyberte typ připojení VPN:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Doména nebo skupina přihlášení** (jenom SonicWALL Mobile Connect): zadejte název přihlašovací skupiny nebo domény, ke které se chcete připojit.

- **Role** (jenom Pulse Secure): zadejte název role uživatele, která má přístup k tomuto připojení. Role uživatele definuje osobní nastavení a možnosti a povolí nebo zakáže určité funkce přístupu.

- **Sféra** (pouze Pulse Secure): zadejte název sféry ověření, kterou chcete použít. Sféra ověření je seskupení prostředků ověření používaných typem připojení Pulse Secure.

- **Vlastní XML**: Zadejte libovolné vlastní příkazy XML, které KONFIGURUJÍ připojení VPN.

  **Příklad zabezpečení Pulse**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **Příklad kontrolního bodu mobilní sítě VPN**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **Příklad mobilního připojení SonicWALL**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client příklad**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Další informace o tom, jak psát vlastní příkazy XML, najdete v dokumentaci k síti VPN od výrobce.

- **Dělené tunelové propojení**: **Povolit** umožňuje zařízením rozhodnout, které připojení se má použít v závislosti na provozu. Uživatel v hotelu například pro přístup k pracovním souborům použije připojení VPN, ale pro běžné procházení webu bude používat standardní síť hotelu. Pokud chcete, aby všechny přenosy používaly tunel VPN v případě, že je připojení VPN aktivní, nastavte ho jako **zakázaný**.

## <a name="proxy-settings"></a>Nastavení proxy serveru

- **Automaticky zjišťovat nastavení proxy**serveru: Pokud server VPN vyžaduje pro připojení proxy server, určete, jestli chcete, aby zařízení automaticky zjišťoval nastavení připojení.
- **Skript automatické konfigurace**: ke konfiguraci proxy serveru použijte konfigurační soubor. Zadejte **adresu URL proxy serveru** , který obsahuje konfigurační soubor. Zadejte například `http://proxy.contoso.com`.
- **Použít proxy server**: tuto možnost povolte, pokud chcete ručně zadat nastavení proxy server.
  - **Adresa**: zadejte adresu proxy server (jako IP adresu).
  - **Číslo portu**: zadejte číslo portu přidruženého k proxy server.
- **Obejít proxy server pro místní adresy**: Pokud server VPN vyžaduje pro připojení proxy server, nechcete použít proxy server pro místní adresy, které zadáte, a pak tuto možnost vyberte.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Nakonfigurujte nastavení sítě VPN na zařízeních se systémem [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [MacOS](vpn-settings-macos.md)a [Windows 10](vpn-settings-windows-10.md) .
