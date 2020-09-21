---
title: Konfigurace nastavení Wi-Fi pro zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Vytvořte nebo přidejte konfigurační profil zařízení s připojením Wi-Fi pro zařízení s macOS. Podívejte se na různá nastavení, přidejte certifikáty, zvolte typ protokolu EAP a vyberte metodu ověřování v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34bd57d1ca7d5c8a892903380347afa9f402de99
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815302"
---
# <a name="add-wi-fi-settings-for-macos-devices-in-microsoft-intune"></a>Přidání nastavení Wi-Fi pro zařízení s macOS v Microsoft Intune

Můžete vytvořit profil s konkrétním nastavením Wi-Fi a potom tento profil nasadit do zařízení macOS. Microsoft Intune nabízí mnoho funkcí, včetně ověřování ve vaší síti, přidání certifikátu PKCS nebo SCEP a dalších.

Tato nastavení sítě Wi-Fi jsou rozdělená do dvou kategorií: základní nastavení a podniková nastavení.

Těmito nastaveními se zabývá tento článek.

## <a name="before-you-begin"></a>Než začnete

Vytvořte [MacOS konfigurační profil zařízení Wi-Fi](wi-fi-settings-configure.md).

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="basic-profiles"></a>Základní profily

Základní nebo osobní profily používají WPA/WPA2 k zabezpečení připojení Wi-Fi na zařízeních. Standard WPA/WPA2 se obvykle používá v domácích sítích nebo v osobních sítích. K ověření připojení můžete také přidat předsdílený klíč.

- **Typ Wi-Fi**: Zvolte **Základní**.
- **Název sítě**: Zadejte název pro toto připojení Wi-Fi. Tato hodnota představuje název, který uživatelé na svém zařízení uvidí při procházení seznamu dostupných připojení.
- **SSID**: Zkratka pro **Service Set Identifier**. Tato vlastnost je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Název sítě, který jste nakonfigurovali, ale uživatelé uvidí jen při zvolení připojení.
- **Připojovat automaticky**: Zvolte **Povolit**, pokud se chcete automaticky připojovat k této síti, když je zařízení v rozsahu. Zvolte **Zakázat**, pokud chcete zařízením zabránit v automatickém připojování.
- **Skrytá síť**: Zvolte **Povolit**, pokud chcete tuto síť skrýt v seznamu dostupných sítí na zařízení. Identifikátor SSID se všesměrově nevysílá. Zvolte **Zakázat**, pokud tuto síť chcete v seznamu dostupných sítí na zařízení zobrazit.
- **Typ zabezpečení**: Vyberte protokol zabezpečení, který se má použít k ověření sítě Wi-Fi. Možnosti:

  - **Otevřené (bez zabezpečení):** tuto možnost použijte jenom v případě, že síť není zabezpečená.
  - **WPA/WPA2-osobní**: Zadejte heslo do pole **Předsdílený klíč**. Po nastavení nebo konfiguraci firemní sítě se nakonfiguruje také heslo nebo síťový klíč. Toto heslo nebo síťový klíč zadejte jako hodnotu PSK.
  - **WEP**

- **Nastavení proxy**: Máte tyto možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Ručně**: Zadejte **adresu proxy serveru** ve formě IP adresy a její **číslo portu**.
  - **Automaticky**: Ke konfiguraci proxy serveru použijte soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které se nachází konfigurační soubor.

## <a name="enterprise-profiles"></a>Profily Enterprise

Podnikové profily používají k ověřování připojení Wi-Fi protokol EAP (Extensible Authentication Protocol). Společnost často používá protokol EAP, protože k ověřování a zabezpečení připojení a konfiguraci dalších možností zabezpečení slouží certifikáty.

- **Typ Wi-Fi**: Zvolte **Enterprise**.
- **SSID**: Zkratka pro **Service Set Identifier**. Tato vlastnost je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Název sítě, který jste nakonfigurovali, ale uživatelé uvidí jen při zvolení připojení.
- **Připojovat automaticky**: Zvolte **Povolit**, pokud se chcete automaticky připojovat k této síti, když je zařízení v rozsahu. Zvolte **Zakázat**, pokud chcete zařízením zabránit v automatickém připojování.
- **Skrytá síť**: Zvolte **Povolit**, pokud chcete tuto síť skrýt v seznamu dostupných sítí na zařízení. Identifikátor SSID se všesměrově nevysílá. Zvolte **Zakázat**, pokud tuto síť chcete v seznamu dostupných sítí na zařízení zobrazit.

- **Typ EAP**: Zvolte typ protokolu EAP (Extensible Authentication Protocol) pro ověřování zabezpečených bezdrátových připojení. Možnosti:

  - **EAP-FAST**: Zadejte **nastavení PAC (Protected Access Credential)**. Tato možnost používá přihlašovací údaje chráněného přístupu k vytvoření ověřeného tunelového propojení mezi klientem a serverem ověřování. Možnosti:
    - **Nepoužívat (PAC)**
    - **Používat (PAC)**: Pokud existuje soubor PAC, použijte ho.
    - **Používat a zřídit PAC**: Vytvoří a přidá soubor PAC do zařízení.
    - **Používat a zřídit PAC anonymně**: Vytvoří a přidá soubor PAC do zařízení bez ověřování na serveru.

  - **EAP-SIM**

  - **EAP-TLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů používaných v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA). Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověření serveru**: vyberte jeden nebo více existujících profilů důvěryhodných kořenových certifikátů. Když se klient připojí k síti, tyto certifikáty se zobrazí na serveru. Ověřují připojení.

    - **Ověřování klienta**  -  **Klientský certifikát pro ověření klienta (certifikát identity)**: vyberte profil certifikátu klienta SCEP nebo PKCS, který je také nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

  - **EAP-TTLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů používaných v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA). Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověření serveru**: vyberte jeden nebo více existujících profilů důvěryhodných kořenových certifikátů. Když se klient připojí k síti, tyto certifikáty se zobrazí na serveru. Ověřují připojení.

    - **Ověřování klientů**: Zvolte **metodu ověřování**. Možnosti:

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. Dále zadejte:
        - **Metoda bez protokolu EAP (vnitřní identita)**: Zvolte, jak chcete připojení ověřovat. Nezapomeňte vybrat stejný protokol, který je nakonfigurovaný u sítě Wi-Fi.

          Máte tyto možnosti: **Nešifrované heslo (PAP)**, **CHAP (Challenge Handshake Authentication Protocol)**, **Microsoft CHAP (MS-CHAP)** nebo **Microsoft CHAP verze 2 (MS-CHAP v2)**.

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **LEAP**

  - **PEAP**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů používaných v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA). Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověření serveru**: vyberte jeden nebo více existujících profilů důvěryhodných kořenových certifikátů. Když se klient připojí k síti, tyto certifikáty se zobrazí na serveru. Ověřují připojení.

    - **Ověřování klientů**: Zvolte **metodu ověřování**. Možnosti:

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. 

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

- **Nastavení proxy**: Máte tyto možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Ručně**: Zadejte **adresu proxy serveru** ve formě IP adresy a její **číslo portu**.
  - **Automaticky**: Ke konfiguraci proxy serveru použijte soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které se nachází konfigurační soubor.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Dále [přiřaďte tento profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Konfigurace nastavení Wi-Fi na zařízeních se systémem [Android](wi-fi-settings-android.md), [Android Enterprise](wi-fi-settings-android-enterprise.md), [iOS/iPadOS](wi-fi-settings-ios.md)a [Windows 10](wi-fi-settings-windows.md)
