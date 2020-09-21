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
ms.openlocfilehash: 01231bc54372dcafb46c58af4ae3169875bed888
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815068"
---
# <a name="add-wi-fi-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Přidání nastavení Wi-Fi pro zařízení s iOS a iPadOS v Microsoft Intune

Můžete vytvořit profil s konkrétním nastavením Wi-Fi a potom tento profil nasadit do zařízení se systémem iOS/iPadOS. Microsoft Intune nabízí mnoho funkcí, včetně ověřování ve vaší síti, přidání certifikátu PKCS nebo SCEP a dalších.

Tato nastavení Wi-Fi jsou rozdělena do dvou kategorií: základní nastavení a nastavení Enterprise.

Těmito nastaveními se zabývá tento článek.

## <a name="before-you-begin"></a>Než začnete

Vytvoření [profilu konfigurace zařízení se systémem iOS/iPadOS](wi-fi-settings-configure.md)

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu Registrace zařízení se [systémem iOS/iPadOS](../enrollment/ios-enroll.md).
>
> Tato nastavení používají [datovou část Apple Wi-Fi](https://developer.apple.com/documentation/devicemanagement/wifi) (otevře web společnosti Apple).

## <a name="basic-profiles"></a>Základní profily

- **Typ Wi-Fi**: vyberte **základní**.
- **Název sítě**: Zadejte název pro toto připojení Wi-Fi. Tato hodnota představuje název, který uživatelé na svém zařízení uvidí při procházení seznamu dostupných připojení.
- **SSID**: Zkratka pro **Service Set Identifier**. Tato vlastnost je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Název sítě, který jste nakonfigurovali, ale uživatelé uvidí jen při zvolení připojení.
- **Připojit automaticky**: **Povolit** automatické připojení k této síti, pokud je zařízení v dosahu. **Disable** znemožní automatickému připojení zařízení.
- **Skrytá síť**: **Povolit** odpovídá nastavení zařízení s nastavením v konfiguraci Wi-Fi směrovače. Takže pokud je síť nastavená na skrytou, pak je v profilu sítě Wi-Fi taky skrytá. Vyberte možnost **Zakázat** , pokud je síťové SSID všesměrové a viditelné.
- **Typ zabezpečení**: Vyberte protokol zabezpečení, který se má použít k ověření sítě Wi-Fi. Možnosti:

  - **Otevřené (bez zabezpečení):** tuto možnost použijte jenom v případě, že síť není zabezpečená.
  - **WPA/WPA2-osobní**: Zadejte heslo do pole **Předsdílený klíč**. Po nastavení nebo konfiguraci firemní sítě se nakonfiguruje také heslo nebo síťový klíč. Toto heslo nebo síťový klíč zadejte jako hodnotu PSK.
  - **WEP**

- **Nastavení proxy**: Máte tyto možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Ručně**: Zadejte **adresu proxy serveru** ve formě IP adresy a její **číslo portu**.
  - **Automaticky**: Ke konfiguraci proxy serveru použijte soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které se nachází konfigurační soubor.

- **Zakázat náhodné přeskupování adres MAC**: od iOS/iPadOS 14 zařízení prezentuje v případě připojení k síti náhodný adresou MAC místo fyzické adresy Mac. Pro ochranu osobních údajů se doporučuje používat náhodné adresy MAC, protože je těžší sledovat zařízení podle adresy MAC. Náhodné adresy MAC však přeruší funkčnost, která spoléhá na statickou adresu MAC, včetně řízení přístupu k síti (NAC).

  Možnosti:

  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení se při připojování k síti místo fyzické adresy MAC při připojování k nové síti zobrazí v zařízeních náhodná adresa MAC.
  - **Ano**: vynutí, aby zařízení prezentují svoji skutečnou adresu MAC sítě Wi-Fi místo náhodné adresy Mac. **Ano** umožňuje sledování zařízení pomocí adresy Mac. V případě potřeby zakažte pouze náhodnost adresy MAC, například pro podporu řízení přístupu k síti (NAC).
  - **Ne**: povoluje NÁHODNOST adresy MAC na zařízeních. Uživatelé ji nemůžou vypnout. Při připojování k nové síti zařízení prezentují náhodnou adresu MAC místo fyzické adresy MAC.

  Toto nastavení platí pro:  
  - iOS 14,0 a novější
  - iPadOS 14,0 a novější

## <a name="enterprise-profiles"></a>Profily Enterprise

- **Typ Wi-Fi**: vyberte **Enterprise**.
- **SSID**: Zkratka pro **Service Set Identifier**. Tato vlastnost je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Název sítě, který jste nakonfigurovali, ale uživatelé uvidí jen při zvolení připojení.
- **Připojit automaticky**: **Povolit** automatické připojení k této síti, pokud je zařízení v dosahu. **Disable** znemožní automatickému připojení zařízení.
- **Skrytá síť**: **Povolit** odpovídá nastavení zařízení s nastavením v konfiguraci Wi-Fi směrovače. Takže pokud je síť nastavená na skrytou, pak je v profilu sítě Wi-Fi taky skrytá. Vyberte možnost **Zakázat** , pokud je síťové SSID všesměrové a viditelné.
- **Typ zabezpečení**: Vyberte protokol zabezpečení, který se má použít k ověření sítě Wi-Fi. Možnosti:
  - **WPA-podnikové**
  - **WPA/WPA2-podnikové**

- **Typ protokolu EAP**: Vyberte typ protokolu EAP (Extensible Authentication Protocol) používaný k ověřování zabezpečených bezdrátových připojení. Možnosti:

  - **EAP-FAST**: Zadejte **nastavení PAC (Protected Access Credential)**. Tato možnost používá přihlašovací údaje chráněného přístupu k vytvoření ověřeného tunelového propojení mezi klientem a serverem ověřování. Možnosti:
    - **Nepoužívat (PAC)**
    - **Používat (PAC)**: Pokud existuje soubor PAC, použijte ho.
    - **Používat a zřídit PAC**: Vytvoří a přidá soubor PAC do zařízení.
    - **Používat a zřídit PAC anonymně**: Vytvoří a přidá soubor PAC do zařízení bez ověřování na serveru.

  - **EAP-SIM**

  - **EAP-TLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů, které se používají v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA), na servery bezdrátové sítě pro přístup. Například přidejte `mywirelessserver.contoso.com` nebo `mywirelessserver` . Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Tento certifikát umožňuje klientovi, aby důvěřoval certifikátu serveru pro přístup k bezdrátové síti.

    - **Ověřování klienta** Vyberte **metodu ověřování**. Možnosti:

      - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

      - **Certifikáty**: vyberte profil klientského certifikátu SCEP nebo PKCS, který je taky nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

    - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **EAP-TTLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů, které se používají v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA), na servery bezdrátové sítě pro přístup. Například přidejte `mywirelessserver.contoso.com` nebo `mywirelessserver` . Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Tento certifikát umožňuje klientovi, aby důvěřoval certifikátu serveru pro přístup k bezdrátové síti.

    - **Ověřování klientů**: vyberte **metodu ověřování**. Možnosti:

      - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. Dále zadejte:
        - **Metoda bez protokolu EAP (vnitřní identita)**: Zvolte, jak chcete připojení ověřovat. Nezapomeňte vybrat stejný protokol, který je nakonfigurovaný u sítě Wi-Fi.

          Máte tyto možnosti: **Nešifrované heslo (PAP)**, **CHAP (Challenge Handshake Authentication Protocol)**, **Microsoft CHAP (MS-CHAP)** nebo **Microsoft CHAP verze 2 (MS-CHAP v2)**.

      - **Certifikáty**: vyberte profil klientského certifikátu SCEP nebo PKCS, který je taky nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **LEAP**

  - **PEAP**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů, které se používají v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA), na servery bezdrátové sítě pro přístup. Například přidejte `mywirelessserver.contoso.com` nebo `mywirelessserver` . Když tento údaj zadáte, můžete obejít okno dynamického vztahu důvěryhodnosti, které se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.
    - **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Tento certifikát umožňuje klientovi, aby důvěřoval certifikátu serveru pro přístup k bezdrátové síti.

    - **Ověřování klientů**: vyberte **metodu ověřování**. Možnosti:

      - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. 

      - **Certifikáty**: vyberte profil klientského certifikátu SCEP nebo PKCS, který je taky nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

- **Nastavení proxy**: Máte tyto možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Ručně**: Zadejte **adresu proxy serveru** ve formě IP adresy a její **číslo portu**.
  - **Automaticky**: Ke konfiguraci proxy serveru použijte soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které se nachází konfigurační soubor.

- **Zakázat náhodné přeskupování adres MAC**: od iOS/iPadOS 14 zařízení prezentuje v případě připojení k síti náhodný adresou MAC místo fyzické adresy Mac. Pro ochranu osobních údajů se doporučuje používat náhodné adresy MAC, protože je těžší sledovat zařízení podle adresy MAC. Náhodné adresy MAC také přeruší funkčnost, která spoléhá na statickou adresu MAC, včetně řízení přístupu k síti (NAC).

  Možnosti:

  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení se při připojování k síti můžou zařízení místo fyzické adresy MAC vyskytovat s náhodným adresou MAC.
  - **Ano**: vynutí, aby zařízení prezentují svoji skutečnou adresu MAC sítě Wi-Fi místo náhodné adresy Mac. **Ano** umožňuje sledování zařízení pomocí adresy Mac. V případě potřeby zakažte pouze náhodnost adresy MAC, například pro podporu řízení přístupu k síti (NAC).
  - **Ne**: povoluje NÁHODNOST adresy MAC na zařízeních. Uživatelé ji nemůžou vypnout. Při připojování k síti zařízení prezentují náhodnou adresu MAC místo fyzické adresy MAC.

  Toto nastavení platí pro:  
  - iOS 14,0 a novější
  - iPadOS 14,0 a novější

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Dále [přiřaďte tento profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Konfigurace nastavení Wi-Fi na zařízeních s [Androidem](wi-fi-settings-android.md), [Androidem Enterprise](wi-fi-settings-android-enterprise.md), [MacOS](wi-fi-settings-macos.md)a [Windows 10](wi-fi-settings-windows.md)
