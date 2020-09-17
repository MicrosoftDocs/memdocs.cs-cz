---
title: Konfigurace nastavení Wi-Fi pro zařízení s iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Vytvořte nebo přidejte profil konfigurace zařízení Wi-Fi pro zařízení s iOS/iPadOS. Podívejte se na různá nastavení, včetně přidání certifikátů, volby typu protokolu EAP a výběru metody ověřování v Microsoft Intune.
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
ms.openlocfilehash: e3206bf7092218eaa1cf05f77cf310be54ac5336
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718752"
---
# <a name="add-wi-fi-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Přidání nastavení Wi-Fi pro zařízení s iOS a iPadOS v Microsoft Intune

Můžete vytvořit profil s konkrétním nastavením Wi-Fi a potom tento profil nasadit do zařízení se systémem iOS/iPadOS. Microsoft Intune nabízí mnoho funkcí, včetně ověřování ve vaší síti, přidání certifikátu PKCS nebo SCEP a dalších.

Tato nastavení Wi-Fi jsou rozdělena do dvou kategorií: základní nastavení a nastavení Enterprise.

Těmito nastaveními se zabývá tento článek.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil zařízení](wi-fi-settings-configure.md).

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu Registrace zařízení se [systémem iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="basic-profiles"></a>Základní profily

- **Typ Wi-Fi**: Zvolte **Základní**.
- **Název sítě**: Zadejte název pro toto připojení Wi-Fi. Tato hodnota představuje název, který uživatelé na svém zařízení uvidí při procházení seznamu dostupných připojení.
- **SSID**: Zkratka pro **Service Set Identifier**. Tato vlastnost je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Název sítě, který jste nakonfigurovali, ale uživatelé uvidí jen při zvolení připojení.
- **Připojovat automaticky**: Zvolte **Povolit**, pokud se chcete automaticky připojovat k této síti, když je zařízení v rozsahu. Zvolte **Zakázat**, pokud chcete zařízením zabránit v automatickém připojování.
- **Skrytá síť**: **Povolit** odpovídá nastavení zařízení s nastavením v konfiguraci Wi-Fi směrovače. Takže pokud je síť nastavená na skrytou, pak je v profilu sítě Wi-Fi taky skrytá. Vyberte možnost **Zakázat** , pokud je síťové SSID všesměrové a viditelné.
- **Typ zabezpečení**: Vyberte protokol zabezpečení, který se má použít k ověření sítě Wi-Fi. Možnosti:

  - **Otevřené (bez zabezpečení):** tuto možnost použijte jenom v případě, že síť není zabezpečená.
  - **WPA/WPA2-osobní**: Zadejte heslo do pole **Předsdílený klíč**. Po nastavení nebo konfiguraci firemní sítě se nakonfiguruje také heslo nebo síťový klíč. Toto heslo nebo síťový klíč zadejte jako hodnotu PSK.
  - **WEP**

- **Nastavení proxy**: Máte tyto možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Ručně**: Zadejte **adresu proxy serveru** ve formě IP adresy a její **číslo portu**.
  - **Automaticky**: Ke konfiguraci proxy serveru použijte soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které se nachází konfigurační soubor.

## <a name="enterprise-profiles"></a>Profily Enterprise

- **Typ Wi-Fi**: Zvolte **Enterprise**.
- **SSID**: Zkratka pro **Service Set Identifier**. Tato vlastnost je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Název sítě, který jste nakonfigurovali, ale uživatelé uvidí jen při zvolení připojení.
- **Připojovat automaticky**: Zvolte **Povolit**, pokud se chcete automaticky připojovat k této síti, když je zařízení v rozsahu. Zvolte **Zakázat**, pokud chcete zařízením zabránit v automatickém připojování.
- **Skrytá síť**: **Povolit** odpovídá nastavení zařízení s nastavením v konfiguraci Wi-Fi směrovače. Takže pokud je síť nastavená na skrytou, pak je v profilu sítě Wi-Fi taky skrytá. Vyberte možnost **Zakázat** , pokud je síťové SSID všesměrové a viditelné.
- **Typ zabezpečení**: Vyberte protokol zabezpečení, který se má použít k ověření sítě Wi-Fi. Možnosti:
  - **WPA-podnikové**
  - **WPA/WPA2-podnikové**

- **Typ EAP**: Zvolte typ protokolu EAP (Extensible Authentication Protocol) pro ověřování zabezpečených bezdrátových připojení. Možnosti:

  - **EAP-FAST**: Zadejte **nastavení PAC (Protected Access Credential)**. Tato možnost používá přihlašovací údaje chráněného přístupu k vytvoření ověřeného tunelového propojení mezi klientem a serverem ověřování. Možnosti:
    - **Nepoužívat (PAC)**
    - **Používat (PAC)**: Pokud existuje soubor PAC, použijte ho.
    - **Používat a zřídit PAC**: Vytvoří a přidá soubor PAC do zařízení.
    - **Používat a zřídit PAC anonymně**: Vytvoří a přidá soubor PAC do zařízení bez ověřování na serveru.

  - **EAP-SIM**

  - **EAP-TLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů, které se používají v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA), na servery bezdrátové sítě pro přístup. Například přidejte `mywirelessserver.contoso.com` nebo `mywirelessserver` . Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověřování serveru**: Zvolte existující profil důvěryhodného kořenového certifikátu. Tento certifikát umožňuje klientovi, aby důvěřoval certifikátu serveru pro přístup k bezdrátové síti.

    - **Ověřování klienta** Vyberte **metodu ověřování**. Možnosti:

      - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

    - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **EAP-TTLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů, které se používají v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA), na servery bezdrátové sítě pro přístup. Například přidejte `mywirelessserver.contoso.com` nebo `mywirelessserver` . Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověřování serveru**: Zvolte existující profil důvěryhodného kořenového certifikátu. Tento certifikát umožňuje klientovi, aby důvěřoval certifikátu serveru pro přístup k bezdrátové síti.

    - **Ověřování klientů**: Zvolte **metodu ověřování**. Možnosti:

      - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. Dále zadejte:
        - **Metoda bez protokolu EAP (vnitřní identita)**: Zvolte, jak chcete připojení ověřovat. Nezapomeňte vybrat stejný protokol, který je nakonfigurovaný u sítě Wi-Fi.

          Máte tyto možnosti: **Nešifrované heslo (PAP)**, **CHAP (Challenge Handshake Authentication Protocol)**, **Microsoft CHAP (MS-CHAP)** nebo **Microsoft CHAP verze 2 (MS-CHAP v2)**.

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **LEAP**

  - **PEAP**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů, které se používají v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA), na servery bezdrátové sítě pro přístup. Například přidejte `mywirelessserver.contoso.com` nebo `mywirelessserver` . Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověřování serveru**: Zvolte existující profil důvěryhodného kořenového certifikátu. Tento certifikát umožňuje klientovi, aby důvěřoval certifikátu serveru pro přístup k bezdrátové síti.

    - **Ověřování klientů**: Zvolte **metodu ověřování**. Možnosti:

      - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. 

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

- **Nastavení proxy**: Máte tyto možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Ručně**: Zadejte **adresu proxy serveru** ve formě IP adresy a její **číslo portu**.
  - **Automaticky**: Ke konfiguraci proxy serveru použijte soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které se nachází konfigurační soubor.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Dále [přiřaďte tento profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Konfigurace nastavení Wi-Fi na zařízeních s [Androidem](wi-fi-settings-android.md), [Androidem Enterprise](wi-fi-settings-android-enterprise.md), [MacOS](wi-fi-settings-macos.md)a [Windows 10](wi-fi-settings-windows.md)
