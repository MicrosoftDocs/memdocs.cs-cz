---
title: Konfigurace nastavení Wi-Fi pro zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Vytvořte nebo přidejte konfigurační profil zařízení s připojením Wi-Fi pro Android. Podívejte se na různá nastavení, včetně přidání certifikátů, volby typu protokolu EAP a výběru metody ověřování v Microsoft Intune.
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
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d892142b22c76bae25ff1754dde7cd56a22960d0
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815017"
---
# <a name="add-wi-fi-settings-for-devices-running-android-in-microsoft-intune"></a>Přidání nastavení Wi-Fi pro zařízení s Androidem v Microsoft Intune

Můžete vytvořit profil s konkrétním nastavením Wi-Fi a potom ho nasadit na zařízení s Androidem. Microsoft Intune nabízí mnoho funkcí, například ověřování v síti, přidání certifikátu PKS nebo SCEP a další.

Tato nastavení Wi-Fi jsou rozdělena do dvou kategorií: základní nastavení a nastavení Enterprise.

Těmito nastaveními se zabývá tento článek.

## <a name="before-you-begin"></a>Než začnete

Vytvořte [profil konfigurace zařízení Wi-Fi Správce zařízení s Androidem](wi-fi-settings-configure.md).

## <a name="basic"></a>Základní

- **Typ Wi-Fi**: Zvolte **Základní**.
- **SSID**: zadejte **identifikátor sady služeb**, což je skutečný název bezdrátové sítě, ke které se zařízení připojují. Uživatelé ale uvidí jenom **název sítě** , který jste nakonfigurovali, když zvolí připojení.
- **Skrytá síť**: Zvolte **Povolit**, pokud chcete tuto síť skrýt v seznamu dostupných sítí na zařízení. Identifikátor SSID se všesměrově nevysílá. Zvolte **Zakázat**, pokud tuto síť chcete v seznamu dostupných sítí na zařízení zobrazit.

## <a name="enterprise"></a>Enterprise

- **Typ Wi-Fi**: Zvolte **Enterprise**.
- **SSID**: zadejte **identifikátor sady služeb**, což je skutečný název bezdrátové sítě, ke které se zařízení připojují. Uživatelé ale uvidí jenom **název sítě** , který jste nakonfigurovali, když zvolí připojení.
- **Skrytá síť**: Zvolte **Povolit**, pokud chcete tuto síť skrýt v seznamu dostupných sítí na zařízení. Identifikátor SSID se všesměrově nevysílá. Zvolte **Zakázat**, pokud tuto síť chcete v seznamu dostupných sítí na zařízení zobrazit.
- **Typ EAP**: Zvolte typ protokolu EAP (Extensible Authentication Protocol) pro ověřování zabezpečených bezdrátových připojení. Možnosti:

  - **EAP-TLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Tento certifikát je prezentován serveru, když se klient připojí k síti. Ověřuje připojení.

    - **Ověřování klienta**  -  **Klientský certifikát pro ověření klienta (certifikát identity)**: vyberte profil certifikátu klienta SCEP nebo PKCS, který je také nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

    - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **EAP-TTLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Tento certifikát je prezentován serveru, když se klient připojí k síti. Ověřuje připojení.

    - **Ověřování klientů**: vyberte **metodu ověřování**. Možnosti:

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. Dále zadejte:
        - **Metoda bez protokolu EAP (vnitřní identita)**: Zvolte, jak chcete připojení ověřovat. Nezapomeňte vybrat stejný protokol, který je nakonfigurovaný u sítě Wi-Fi. Možnosti:

          - **Nezašifrované heslo (PAP)**
          - **Protokol CHAP (Challenge Handshake Authentication Protocol)**
          - **Protokol Microsoft CHAP (MS-CHAP)**
          - **Protokol Microsoft CHAP verze 2 (MS-CHAP v2)**

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **PEAP**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Tento certifikát je prezentován serveru, když se klient připojí k síti. Ověřuje připojení.

    - **Ověřování klientů**: vyberte **metodu ověřování**. Možnosti:

      - **Uživatelské jméno a heslo**: Zobrazí uživateli výzvu k zadání uživatelského jména a hesla pro ověření připojení. Dále zadejte:
        - **Ověřování metodou bez protokolu EAP (vnitřní identita)**: Zvolte, jak chcete připojení ověřovat. Nezapomeňte vybrat stejný protokol, který je nakonfigurovaný u sítě Wi-Fi. Možnosti:

          - **Žádný**
          - **Protokol Microsoft CHAP verze 2 (MS-CHAP v2)**

      - **Certifikáty**: Zvolte profil klientského certifikátu SCEP nebo PKCS, který je také nasazený na zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení.

      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Dále [tento profil přiřaďte](device-profile-assign.md).

## <a name="more-resources"></a>Další zdroje informací

- [Přehled nastavení sítě Wi-Fi](wi-fi-settings-configure.md), včetně dalších platforem.

- Používáte zařízení s Androidem Enterprise nebo beznabídkovým režimem Androidu? Pokud ano, podívejte se na [nastavení Wi-Fi pro zařízení s Androidem Enterprise a vyhrazenými zařízeními](wi-fi-settings-android-enterprise.md).
