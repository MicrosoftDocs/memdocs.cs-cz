---
title: Konfigurace nastavení sítě VPN pro zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
description: Přidat nebo vytvořit konfigurační profil virtuální privátní sítě (VPN) v Microsoft Intune. Přidejte podrobnosti o připojení, dělené tunelové propojení, vlastní nastavení sítě VPN s identifikátorem, páry klíč-hodnota, nastavení proxy serveru s konfiguračním skriptem, adresou IP nebo plně kvalifikovaným názvem domény a portem TCP v Microsoft Intune na zařízeních s macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 581e39ddbd50d4c2aeb4001b73c1492a3a799f90
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814752"
---
# <a name="add-vpn-settings-on-macos-devices-in-microsoft-intune"></a>Přidat nastavení sítě VPN na zařízení macOS v Microsoft Intune

Tento článek popisuje, jaká nastavení můžete v Intune použít ke konfiguraci připojení VPN na zařízeních s macOS.

V závislosti na tom, jaká nastavení zvolíte, nebudou v následujícím seznamu konfigurovatelné všechny hodnoty.

## <a name="before-you-begin"></a>Než začnete

Vytvořte [MacOS konfigurační profil zařízení VPN](vpn-settings-configure.md).

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="base-vpn-settings"></a>Základní nastavení sítě VPN

**Název připojení**: zadejte název tohoto připojení. Tento název uživatelé vidí, když na svém zařízení procházejí seznamem dostupných připojení VPN.

- **IP adresa nebo plně kvalifikovaný**název domény: zadejte IP adresu nebo plně kvalifikovaný název domény serveru VPN, ke kterému se zařízení připojují. Zadejte například `192.168.1.1` nebo `vpn.contoso.com`.
- **Metoda ověřování**: Zvolte způsob, kterým se zařízení ověřují vůči serveru VPN. Možnosti:
  - **Certifikáty**: v části **ověřovací certifikát**vyberte profil certifikátu SCEP nebo PKCS, který jste dříve vytvořili za účelem ověřování připojení. Další informace o profilech certifikátů najdete v článku [Konfigurace certifikátů](../protect/certificates-configure.md).
  - **Uživatelské jméno a heslo**: koncoví uživatelé musí pro přihlášení k serveru VPN uvést uživatelské jméno a heslo.
- **Typ připojení**: z následujícího seznamu dodavatelů vyberte typ připojení VPN:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Mobilita NetMotion**
  - **Pulse Secure**
  - **Vlastní síť VPN**: tuto možnost vyberte, pokud váš dodavatel VPN není uveden. Také konfigurovat:

    - **Identifikátor sítě VPN**: zadejte identifikátor aplikace VPN, kterou používáte. Tento identifikátor poskytuje poskytovatel sítě VPN.
    - **Zadejte páry klíč-hodnota pro vlastní atributy sítě VPN**: přidejte nebo importujte **klíče** a **hodnoty** , které přizpůsobují připojení k síti VPN. Tyto hodnoty obvykle poskytuje poskytovatel sítě VPN.

- **Dělené tunelové propojení**: **povolí** nebo **zakáže** tuto možnost, která umožňuje zařízením rozhodnout, které připojení se má použít v závislosti na provozu. Uživatel v hotelu například pro přístup k pracovním souborům použije připojení VPN, ale pro běžné procházení webu bude používat standardní síť hotelu.

## <a name="automatic-vpn"></a>Automatické připojení VPN

- **Síť VPN na vyžádání**: síť VPN na vyžádání používá pravidla k automatickému připojení nebo odpojení připojení k síti VPN. Když se vaše zařízení pokusí připojit k síti VPN, vyhledá shody v parametrech a pravidlech, které vytvoříte, jako je například odpovídající IP adresa nebo název domény. Pokud se zobrazí shoda, akce, kterou zvolíte, se spustí.

  Můžete třeba vytvořit podmínku, že se připojení VPN použije, jen pokud zařízení není připojené k firemní síti Wi-Fi. Nebo pokud zařízení nemá přístup k zadané doméně hledání DNS, připojení VPN se nespustí.

  - **Přidat**: tuto možnost vyberte, pokud chcete přidat pravidlo.

  - **Chci udělat následující**: Pokud existuje shoda mezi hodnotou zařízení a vaším pravidlem na vyžádání, vyberte akci. Možnosti:

    - Zřízení sítě VPN
    - Odpojení sítě VPN
    - Vyhodnotit jednotlivé pokusy o připojení
    - Ignorovat

  - **Chci omezit na**: vyberte podmínku, kterou musí pravidlo splňovat. Možnosti:

    - **Konkrétní identifikátory SSID**: Zadejte alespoň jeden název bezdrátové sítě, který bude pravidlo platit. Tento název sítě je identifikátor SSID (Service Set Identifier). Zadejte například `Contoso VPN`.
    - **Konkrétní domény DNS**: zadejte jednu nebo víc domén DNS, na které se bude pravidlo vztahovat. Zadejte například `contoso.com`.
    - **Všechny domény**: tuto možnost vyberte, pokud chcete pravidlo použít pro všechny domény ve vaší organizaci.

  - **Ale jenom v případě, že je tato funkce URL test úspěšná**: volitelné. Zadejte adresu URL, kterou pravidlo použije pro účely testování. Pokud zařízení přistupuje k této adrese URL bez přesměrování, spustí se připojení VPN. A zařízení se připojí k cílové adrese URL. Uživatel neuvidí testovací web řetězce adresy URL.

    Například test řetězce adresy URL je audit URL webového serveru, který kontroluje dodržování předpisů zařízením před připojením k síti VPN. Adresa URL taky testuje možnost připojení VPN k lokalitě, než se zařízení připojí k cílové adrese URL prostřednictvím sítě VPN.

- **Zabránit uživatelům v zakázání automatické sítě VPN**: vaše možnosti:

  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
  - **Ano**: zabraňuje uživatelům vypnout automatickou síť VPN. Vynutí uživatele, aby povolili automatické povolení a používání sítě VPN.
  - **Ne**: umožňuje uživatelům vypnout automatické připojení VPN.

  Toto nastavení platí pro:  
  - macOS 11 a novější (velký sur)

- **Síť VPN pro jednotlivé aplikace**: povolí VPN pro jednotlivé aplikace přidružením tohoto připojení k síti VPN k aplikaci MacOS. Po spuštění aplikace se připojení VPN spustí. Profil sítě VPN můžete přidružit k aplikaci, když software přiřadíte. Další informace najdete v tématu [jak přiřadit a monitorovat aplikace](../apps/apps-deploy.md).

  - **Adresy URL Safari, které aktivují tuto síť VPN:** Můžete přidat jednu nebo více adres URL webu. Při návštěvě těchto adres URL pomocí prohlížeče Safari na zařízení se automaticky naváže připojení k VPN.

  - **Přidružené domény**: zadejte přidružené domény v profilu sítě VPN, který automaticky SPUSTÍ připojení VPN. Zadejte například `contoso.com`. Zařízení v `contoso.com` doméně automaticky spustí připojení k síti VPN.

    Další informace najdete v tématu [přidružené domény](device-features-configure.md#associated-domains).

  - **Vyloučené domény**: zadejte domény, které můžou obejít připojení VPN, když je připojené k síti VPN pro jednotlivé aplikace. Zadejte například `contoso.com`. Zařízení v `contoso.com` doméně nebudou spouštět ani používat připojení VPN pro jednotlivé aplikace. Zařízení v `contoso.com` doméně budou používat veřejný Internet.

  - **Zabránit uživatelům v zakázání automatické sítě VPN**: vaše možnosti:

    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Ano**: zabraňuje uživatelům vypnout automatickou síť VPN. Vynutí uživatele, aby povolili automatické povolení a používání sítě VPN.
    - **Ne**: umožňuje uživatelům vypnout automatické připojení VPN.

    Toto nastavení platí pro:  
    - macOS 11 a novější (velký sur)

## <a name="proxy-settings"></a>Nastavení proxy serveru

- **Skript automatické konfigurace**: ke konfiguraci proxy serveru použijte konfigurační soubor. Zadejte **adresu URL proxy serveru** , který obsahuje konfigurační soubor. Zadejte například `http://proxy.contoso.com`.
- **Adresa**: zadejte adresu proxy server (jako IP adresu).
- **Číslo portu**: zadejte číslo portu přidruženého k proxy server.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nemusí ještě nic dělat. Nezapomeňte [profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).

Nakonfigurujte nastavení sítě VPN na zařízeních se systémem [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md)a [Windows 10](vpn-settings-windows-10.md) .
