---
title: Konfigurace nastavení sítě VPN na zařízeních Windows Phone 8,1 v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte konfigurační profil sítě VPN pomocí nastavení konfigurace virtuální privátní sítě (VPN), včetně podrobností o připojení, a nastavení proxy serveru pro zahrnutí IP adresy nebo adresy FQDN a portu TCP v Microsoft Intune na zařízeních s Windows Phone 8,1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea08456fd55e03e86dfcec36411825d03652a47d
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146435"
---
# <a name="add-vpn-settings-on-windows-phone-81-devices-in-microsoft-intune"></a>Přidat nastavení sítě VPN v zařízeních Windows Phone 8,1 v Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Tento článek popisuje, jaká nastavení můžete v Intune použít ke konfiguraci připojení VPN na zařízeních s Windows Phone 8.1. 

V závislosti na tom, jaká nastavení zvolíte, nebudou v následujícím seznamu konfigurovatelné všechny hodnoty.

>[!IMPORTANT]
>Pro zařízení s Windows 10 se taky používají profily sítě VPN Windows Phone 8,1.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil konfigurace zařízení VPN](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Základní nastavení sítě VPN

- **Použít všechna nastavení jenom na Windows Phone 8,1**: nakonfigurujte toto nastavení na klasickém portálu Intune. V centru pro správu Microsoft Endpoint Manageru toto nastavení nejde změnit. Při nastavení **Konfigurace**se všechna nastavení aplikují jenom na zařízení Windows Phone 8,1. Pokud je nastavené na **Nenakonfigurováno**, tato nastavení se vztahují také na zařízení s Windows 10 Mobile.
- **Název připojení**: zadejte název tohoto připojení. Tento název uživatelé vidí, když na svém zařízení procházejí seznamem dostupných připojení VPN.
- **Metoda ověřování**: zvolte způsob, kterým se zařízení ověřují vůči serveru VPN:
  - **Certifikáty**: v části **ověřovací certifikát**vyberte profil certifikátu SCEP nebo PKCS, který jste dříve vytvořili za účelem ověřování připojení. Další informace o profilech certifikátů najdete v článku [Konfigurace certifikátů](../protect/certificates-configure.md).
  - **Uživatelské jméno a heslo**: koncoví uživatelé musí pro přihlášení k serveru VPN uvést uživatelské jméno a heslo.
- **Servery**: přidejte minimálně jeden VPN server, ke kterému se budou zařízení připojovat.
  - **Přidat**: otevře okno **Přidat řádek** , kde můžete zadat následující informace:
    - **Popis**: zadejte popisný název serveru, jako je **Contoso VPN server**.
    - **IP adresa nebo plně kvalifikovaný**název domény: zadejte IP adresu nebo plně kvalifikovaný název domény serveru VPN, ke kterému se zařízení připojují. Příklady: **192.168.1.1**, **VPN.contoso.com**.
    - **Výchozí server**: povolí tento server jako výchozí server, který budou zařízení používat k navázání připojení. Jako výchozí server musí být nastavený jenom jeden server.
  - **Importovat**: vyhledejte soubor s oddělovači se seznamem serverů ve formátu popis, IP adresa nebo plně kvalifikovaný název domény, výchozí server. Pomocí **OK** servery naimportujte do seznamu **Servery**.
  - **Export**: exportuje seznam serverů do souboru s hodnotami oddělenými čárkami (CSV).

- **Obejít síť VPN v podnikové síti Wi-Fi**: tuto možnost povolte, pokud chcete zadat, že se připojení VPN nepoužijí, když je zařízení připojené k podnikové síti Wi-Fi.
- **Obejít síť VPN v domácí síti Wi-Fi**: tuto možnost povolte, pokud chcete zadat, že se připojení VPN nebude používat při připojení zařízení k domácí síti Wi-Fi.

- **Typ připojení**: Vyberte typ připojení VPN. Možnosti:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

- **Doména nebo skupina přihlášení** (jenom SonicWALL Mobile Connect): zadejte název přihlašovací skupiny nebo domény, ke které se chcete připojit.
- **Role** (jenom Pulse Secure): zadejte název role uživatele, která má přístup k tomuto připojení. Role uživatele definuje osobní nastavení a možnosti a povolí nebo zakáže určité funkce přístupu.
- **Sféra** (pouze Pulse Secure): zadejte název sféry ověření, kterou chcete použít. Sféra ověření je seskupení prostředků ověření používaných typem připojení Pulse Secure.

- **Seznam hledání přípon DNS**: **přidejte** alespoň jeden server DNS. Každá zadaná přípona DNS se vyhledá při připojení k webu pomocí krátkého názvu. Pokud zadáte například přípony DNS **domain1.contoso.com** a **domain2.contoso.com** a navštívíte adresu URL `http://mywebsite`, vyhledají se adresy URL `http://mywebsite.domain1.contoso.com` a `http://mywebsite.domain2.contoso.com`.

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
- **Skript automatické konfigurace**: ke konfiguraci proxy serveru použijte konfigurační soubor. Zadejte **adresu URL proxy serveru** (třeba `http://proxy.contoso.com`), na které je konfigurační soubor.
- **Použít proxy server**: tuto možnost povolte, pokud chcete ručně zadat nastavení proxy server.
  - **Adresa**: zadejte adresu proxy server (jako IP adresu).
  - **Číslo portu**: zadejte číslo portu přidruženého k proxy server.
- **Obejít proxy server pro místní adresy**: Pokud server VPN vyžaduje pro připojení proxy server, nechcete použít proxy server pro místní adresy, které zadáte, a pak tuto možnost vyberte.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Nakonfigurujte nastavení sítě VPN na zařízeních se systémem [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [MacOS](vpn-settings-macos.md)a [Windows 10](vpn-settings-windows-10.md) .
