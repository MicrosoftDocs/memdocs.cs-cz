---
title: Konfigurace nastavení drátové sítě pro zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Vytvořte nebo přidejte konfigurační profil zařízení s drátovou sítí pro zařízení macOS. Podívejte se na různá nastavení, přidejte certifikáty, zvolte typ protokolu EAP a vyberte metodu ověřování v Microsoft Intune.
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
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 23878b08e783240d53ec8a205ba79b73b6d9faf2
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815455"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Přidat nastavení pevné sítě pro zařízení macOS v Microsoft Intune

Můžete vytvořit profil s konkrétními nastaveními drátové sítě a potom tento profil nasadit do zařízení macOS. Microsoft Intune nabízí mnoho funkcí, včetně ověřování ve vaší síti, přidání certifikátu SCEP a dalších.

Tento článek popisuje nastavení, která můžete konfigurovat.

## <a name="before-you-begin"></a>Než začnete

Vytvořte [MacOS konfigurační profil zařízení s drátovou sítí](wired-networks-configure.md).

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="wired-network"></a>Drátová síť

- **Síťové rozhraní**: vyberte Síťová rozhraní na zařízení, na které se profil vztahuje, podle priority služby – pořadí. Možnosti:
  
  - **První aktivní síť Ethernet** (výchozí)
  - **Druhá aktivní síť Ethernet**
  - **Třetí aktivní síť Ethernet**
  - **První síť Ethernet**
  - **Druhá síť Ethernet**
  - **Třetí Ethernet**
  - **Libovolný Ethernet**

  Možnosti, které mají v nadpisu "aktivní", používají rozhraní, která aktivně pracují na zařízení. Pokud žádná aktivní rozhraní neexistují, nakonfigurují se další rozhraní v prioritě pořadí služeb. Ve výchozím nastavení je vybrána **první aktivní síť Ethernet** , což je také výchozí nastavení nakonfigurované nástrojem MacOS.

- **Typ protokolu EAP**: Vyberte typ protokolu EAP (Extensible Authentication Protocol) pro ověřování zabezpečených drátových připojení. Možnosti:

  - **EAP-FAST**: Zadejte **nastavení PAC (Protected Access Credential)**. Tato možnost používá přihlašovací údaje chráněného přístupu k vytvoření ověřeného tunelového propojení mezi klientem a serverem ověřování. Možnosti:
    - **Nepoužívat (PAC)**
    - **Používat (PAC)**: Pokud existuje soubor PAC, použijte ho.
    - **Používat a zřídit PAC**: Vytvoří a přidá soubor PAC do zařízení.
    - **Používat a zřídit PAC anonymně**: Vytvoří a přidá soubor PAC do zařízení bez ověřování na serveru.

  - **EAP-TLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů používaných v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA). Když zadáte tyto informace, můžete obejít okno dynamického vztahu důvěryhodnosti zobrazené na zařízeních uživatelů při připojování k této síti.
    - **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Když se klient připojí k síti, zobrazí se tento certifikát serveru. Slouží k ověření připojení.
    - **Ověřování klienta**  -  **Certifikáty**: vyberte profil klientského certifikátu SCEP, který je taky nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení. Certifikáty PKCS se nepodporují.
    - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **EAP-TTLS**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů používaných v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA). Když zadáte tyto informace, můžete obejít okno dynamického vztahu důvěryhodnosti zobrazené na zařízeních uživatelů při připojování k této síti.
    - **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Když se klient připojí k síti, zobrazí se tento certifikát serveru. Slouží k ověření připojení.
    - **Ověřování klientů**: vyberte **metodu ověřování**. Možnosti:
      - **Uživatelské jméno a heslo**: vyzve uživatele k ověření připojení a zadáním uživatelského jména a hesla. Dále zadejte:
        - **Metoda bez protokolu EAP (vnitřní identita)**: Vyberte způsob ověřování připojení. Ujistěte se, že jste zvolili stejný protokol, který je nakonfigurovaný ve vaší síti. Možnosti:
          - **Nezašifrované heslo (PAP)**
          - **Protokol CHAP (Challenge Handshake Authentication Protocol)**
          - **Protokol Microsoft CHAP (MS-CHAP)**
          - **Protokol Microsoft CHAP verze 2 (MS-CHAP v2)**
      - **Certifikáty**: vyberte profil klientského certifikátu SCEP, který je taky nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení. Certifikáty PKCS se nepodporují.
      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

  - **LEAP**

  - **PEAP**: Dále zadejte:

    - **Vztah důvěryhodnosti serveru**  -  **Názvy certifikačních serverů**: **přidejte** jeden nebo více běžných názvů používaných v certifikátech vydaných vaší důvěryhodnou certifikační autoritou (CA). Když zadáte tyto informace, můžete obejít okno dynamického vztahu důvěryhodnosti zobrazené na zařízeních uživatelů při připojování k této síti.
    - **Kořenový certifikát pro ověření serveru**: Vyberte existující profil důvěryhodného kořenového certifikátu. Když se klient připojí k síti, zobrazí se tento certifikát serveru. Slouží k ověření připojení.
    - **Ověřování klientů**: vyberte **metodu ověřování**. Možnosti:
      - **Uživatelské jméno a heslo**: vyzve uživatele k ověření připojení a zadáním uživatelského jména a hesla.
      - **Certifikáty**: vyberte profil klientského certifikátu SCEP, který je taky nasazený do zařízení. Tento certifikát představuje identitu, kterou zařízení předloží serveru pro ověření připojení. Certifikáty PKCS se nepodporují.
      - **Ochrana identity (vnější identita)**: Zadejte text odeslaný v odpovědi na žádost o identitu EAP. Tento text může být libovolná hodnota, například `anonymous`. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

## <a name="next-steps"></a>Další kroky

Profil je vytvořen, ale nemusí provádět žádné akce. Nezapomeňte [Tento profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).
