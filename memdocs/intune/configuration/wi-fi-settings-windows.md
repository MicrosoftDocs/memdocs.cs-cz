---
title: Nastavení Wi-Fi pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte konfigurační profil pomocí nastavení Wi-Fi pro zařízení s Windows 10 nebo novější verzí v Microsoft Intune. Můžete nakonfigurovat základní nastavení nebo nastavení na podnikové úrovni.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.reviewer: tycast
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ffa0fd0bc1c3b1ed1fe7f5d79ae009aaf9fc713
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815119"
---
# <a name="add-wi-fi-settings-for-windows-10-and-later-devices-in-intune"></a>Přidání nastavení Wi-Fi pro zařízení s Windows 10 a novější verzí v Intune

Můžete vytvořit profil s konkrétními nastaveními Wi-Fi. Pak tento profil nasaďte do zařízení s Windows 10 a novějším. Microsoft Intune nabízí mnoho funkcí, například ověřování v síti, použití předsdíleného klíče a další.

Těmito nastaveními se zabývá tento článek.

## <a name="before-you-begin"></a>Než začnete

Vytvořte [konfigurační profil zařízení s Windows 10 Wi-Fi](wi-fi-settings-configure.md).

## <a name="basic-profile"></a>Základní profil

Základní nebo osobní profily používají WPA/WPA2 k zabezpečení připojení Wi-Fi na zařízeních. Standard WPA/WPA2 se obvykle používá v domácích sítích nebo v osobních sítích. K ověření připojení můžete také přidat předsdílený klíč.

- **Typ Wi-Fi**: Zvolte **Základní**. 

- **Název Wi-Fi (SSID):** zkratka pro Service Set Identifier. Tato hodnota je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Nakonfigurovaný **Název připojení** ale uživatelé uvidí jen při volbě připojení.

- **Název připojení:** Zadejte popisný název připojení Wi-Fi. Zadaný text uživatelé uvidí na svém zařízení při procházení dostupných připojení.

- **Připojit se automaticky, pokud je v dosahu:** Když nastavíte **Ano**, zařízení se budou k této síti připojovat automaticky, když budou v dosahu. Když nastavíte **Ne**, zařízení se automaticky připojovat nebudou.

  - **Připojit k upřednostňovanější síti, pokud je k dispozici:** Pokud jsou zařízení v dosahu upřednostňovanější sítě, zvolte **Ano**, aby se k ní připojila. Pokud chcete použít síť Wi-Fi v tomto konfiguračním profilu, zvolte **Ne**.

    Například můžete vytvořit síť Wi-Fi **ContosoCorp** a v rámci tohoto konfiguračního profilu **ContosoCorp** použít. V dosahu máte i Wi-Fi **ContosoGuest**. Když jsou v dosahu vaše podniková zařízení, budete chtít, aby se automaticky připojovala k síti **ContosoCorp**. V takové situaci vlastnost **Připojit k upřednostňovanější síti, pokud je k dispozici** nastavte na **Ne**.

  - **Připojit se k této síti i v případě, že nevysílá svůj identifikátor SSID:** Pokud chcete, aby se konfigurační profil připojoval k vaší síti automaticky, i když je síť skrytá (její SSID se nevysílá veřejně), zvolte **Ano**. Pokud nechcete, aby se tento konfigurační profil připojoval ke skryté síti, zvolte **Ne**.

- **Limit připojení účtovaného podle objemu dat**: Správce může zvolit způsob měření provozu v síti. Aplikace pak mohou na základě tohoto nastavení upravit svůj provoz v síti. Možnosti:

  - **Neomezené**: Toto je výchozí možnost. Toto připojení se neměří a provoz není nijak omezen.
  - **Pevné**: Tuto možnost použijte, pokud je síť nakonfigurovaná s pevně stanoveným limitem síťového provozu. Po dosažení limitu se přístup k síti zakáže.
  - **Proměnná**: Tuto možnost použijte, pokud se síťový provoz účtuje po bajtech (cena za bajt).

- **Typ zabezpečení bezdrátové sítě**: Zadejte protokol zabezpečení, který bude ověřovat zařízení v síti. Máte tyto možnosti:
  - **Otevřené (bez zabezpečení):** tuto možnost použijte jenom v případě, že síť není zabezpečená.
  - **WPA/WPA2-osobní**: Jedná se o možnost s vyšším zabezpečením, která se obvykle používá pro připojení Wi-Fi. Z důvodu dalšího zvýšení zabezpečení můžete zadat také heslo předsdíleného klíče nebo síťový klíč.

    - **Předsdílený klíč** (PSK): Volitelné. Tato možnost se zobrazí, pokud jako typ zabezpečení vyberete **WPA/WPA2-osobní**. Po nastavení nebo konfiguraci firemní sítě se nakonfiguruje také heslo nebo síťový klíč. Toto heslo nebo síťový klíč zadejte jako hodnotu PSK. Zadejte řetězec, jehož délka je 8 až 64 znaků. Pokud mají vaše heslo nebo síťový klíč 64 znaků, zadejte šestnáctkové znaky.

      > [!IMPORTANT]
      > PSK je stejný pro všechna zařízení, na která tento profil cílíte. Pokud dojde k ohrožení bezpečnosti klíče, může ho použít jakékoli zařízení pro připojení k síti Wi-Fi. Zajistěte, aby byl PSKs zabezpečený, aby nedocházelo k neoprávněn

- **Nastavení firemního proxy:** Zvolte nastavení proxy v organizaci. Možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Nakonfigurovat ručně:** Zadejte **IP adresu proxy serveru** a **Číslo portu**.
  - **Automaticky nakonfigurovat**: Zadejte adresu URL, která odkazuje na skript PAC (automatická konfigurace proxy). Zadejte například `http://proxy.contoso.com/proxy.pac`.

## <a name="enterprise-profile"></a>Profil Enterprise

Podnikové profily používají k ověřování připojení Wi-Fi protokol EAP (Extensible Authentication Protocol). Společnost často používá protokol EAP, protože k ověřování a zabezpečení připojení a konfiguraci dalších možností zabezpečení slouží certifikáty.

- **Typ Wi-Fi**: Zvolte **Enterprise**.

- **Název Wi-Fi (SSID):** zkratka pro Service Set Identifier. Tato hodnota je reálným názvem bezdrátové sítě, ke které se zařízení připojí. Nakonfigurovaný **Název připojení** ale uživatelé uvidí jen při volbě připojení.

- **Název připojení:** Zadejte popisný název připojení Wi-Fi. Zadaný text uživatelé uvidí na svém zařízení při procházení dostupných připojení.

- **Připojit se automaticky, pokud je v dosahu:** Když nastavíte **Ano**, zařízení se budou k této síti připojovat automaticky, když budou v dosahu. Když nastavíte **Ne**, zařízení se automaticky připojovat nebudou.
  - **Připojit k upřednostňovanější síti, pokud je k dispozici:** Pokud jsou zařízení v dosahu upřednostňovanější sítě, zvolte **Ano**, aby se k ní připojila. Pokud chcete použít síť Wi-Fi v tomto konfiguračním profilu, zvolte **Ne**.

    Například můžete vytvořit síť Wi-Fi **ContosoCorp** a v rámci tohoto konfiguračního profilu **ContosoCorp** použít. V dosahu máte i Wi-Fi **ContosoGuest**. Když jsou v dosahu vaše podniková zařízení, budete chtít, aby se automaticky připojovala k síti **ContosoCorp**. V takové situaci vlastnost **Připojit k upřednostňovanější síti, pokud je k dispozici** nastavte na **Ne**.

- **Připojit se k této síti i v případě, že nevysílá svůj identifikátor SSID:** Pokud chcete, aby se konfigurační profil připojoval k vaší síti automaticky, i když je síť skrytá (její SSID se nevysílá veřejně), zvolte **Ano**. Pokud nechcete, aby se tento konfigurační profil připojoval ke skryté síti, zvolte **Ne**.

- **Limit připojení účtovaného podle objemu dat**: Správce může zvolit způsob měření provozu v síti. Aplikace pak mohou na základě tohoto nastavení upravit svůj provoz v síti. Možnosti:

  - **Neomezené**: Toto je výchozí možnost. Toto připojení se neměří a provoz není nijak omezen.
  - **Pevné**: Tuto možnost použijte, pokud je síť nakonfigurovaná s pevně stanoveným limitem síťového provozu. Po dosažení limitu se přístup k síti zakáže.
  - **Proměnná**: Tuto možnost použijte, pokud se síťový provoz účtuje po bajtech.

- **Jednotné přihlašování:** Umožňuje vám nakonfigurovat jednotné přihlašování (SSO), u kterého se přihlašovací údaje k počítači i síti Wi-Fi sdílejí. Máte tyto možnosti:
  - **Zakázat:** Jednotné přihlašování se zakáže. Uživatel se musí v síti ověřit zvlášť.
  - **Povolit dříve, než se uživatel přihlásí k zařízení:** Použití jednotného přihlašování k síti těsně předtím, než se uživatel přihlásí
  - **Povolit, až se uživatel přihlásí k zařízení:** Použití jednotného přihlašování k síti hned poté, co se uživatel přihlásil
  - **Maximální časový limit na ověření:** Zadejte maximální dobu, v rozmezí od 1 do 120 sekund, po kterou se bude čekat, než se provede ověření k síti.
  - **Povolit systému Windows zobrazit uživateli výzvu, aby zadal další přihlašovací údaje pro ověření:** Když zvolíte **Ano**, umožníte systému Windows vyzvat uživatele k zadání dalších přihlašovacích údajů, pokud to metoda ověřování vyžaduje. Pokud chcete tyto výzvy skrýt, zvolte **Ne**.

- **Povolit ukládání klíče PMK (Pairwise Master Key) do mezipaměti:** Pokud chcete klíč PMK používaný při ověřování ukládat do mezipaměti, zvolte **Ano**. Toto ukládání do mezipaměti obvykle ověřování k síti urychluje. Pokud chcete ověřovací signalizaci vynutit pokaždé, když se připojujete k síti Wi-Fi, zvolte **Ne**. Chcete-li použít nastavení **Povolit předběžné ověřování** , vyberte možnost **Ano**.

  - **Maximální doba, po kterou je klíč PMK uložený v mezipaměti:** Zadejte dobu, v rozmezí od 5 do 1440 minut, po kterou bude klíč PMK uložený v mezipaměti.
  - **Maximální počet klíčů PMK uložených v mezipaměti:** Zadejte počet klíčů, v rozmezí od 1 do 255, který se může uložit do mezipaměti.

- **Povolit předběžné ověření:** Předběžné ověření umožňuje profilu, který chcete ověřit, získat před připojením přístup ke všem přístupovým bodům sítě v profilu. Při přesouvání mezi přístupovými body, proběhne opětovné připojení uživatele nebo zařízení díky předběžnému ověření rychleji. Pokud chcete, aby profil provedl ověření u všech přístupových bodů, které jsou v dané síti v dosahu, zvolte **Ano**. Pokud vyžadujete, aby se uživatel nebo zařízení ověřovalo u každého přístupového bodu zvlášť, zvolte **Ne**.

  Chcete-li použít toto nastavení, nastavte **možnost Povolit ukládání klíče PMK (Pairwise Master Key) do mezipaměti** **Ano**.

  - **Maximální počet pokusů o předběžné ověření:** Zadejte počet pokusů, v rozmezí od 1 do 16, k předběžnému ověření.

- **Typ protokolu EAP:** Zvolte typ protokolu EAP pro ověřování zabezpečených bezdrátových připojení. Možnosti:

  - **EAP-SIM**
  - **EAP-TLS**
  - **EAP-TTLS**
  - **Protokol PEAP** (Protected EAP)

    **Další nastavení EAP-TLS, EAP-TTLS a PEAP**:

    > [!NOTE]
    > Profily certifikátů SCEP a PKCS se podporují při použití typu protokolu EAP.

    **VZTAH DŮVĚRYHODNOSTI SERVERU**  

    - **Názvy certifikačních serverů**: Použijte s protokoly typu **EAP-TLS**, **EAP-TTLS** a **PEAP**. Zadejte jeden nebo více běžných názvů použitých v certifikátech, které vystavuje vaše důvěryhodná certifikační autorita. Když tento údaj zadáte, můžete obejít dialog dynamického vztahu důvěryhodnosti, který se zobrazí na zařízeních uživatelů při připojování k Wi-Fi síti.  

    - **Kořenový certifikát pro ověřování serveru**: Použijte s protokoly typu **EAP-TLS**, **EAP-TTLS** a **PEAP**. Zvolte profil důvěryhodného kořenového certifikátu pro ověření připojení.  

    - **Ochrana identity (vnější identita)**: Použijte s typem **PEAP**. Zadejte text odeslaný v odpovědi na požadavek identity EAP. Tento text může být libovolná hodnota. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.  

    - **Provést ověření serveru ve fázi protokolu PEAP 1**: Pokud je nastaveno na **Ano**, ve fázi vyjednávání protokolu PEAP 1, zařízení ověřují certifikát a ověřují server. Vyberte **ne** , pokud chcete toto ověření zablokovat nebo zakázat. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

      Pokud vyberete **Ano**, nakonfiguruje se také:

      **Zakázat výzvy uživatelů k ověření serveru ve fázi protokolu PEAP fáze 1**: Pokud je hodnota nastavena na **Ano**, ve fázi vyjednávání protokolu PEAP 1 se nezobrazí výzvy uživatele s výzvou k autorizaci nových serverů protokolu PEAP pro důvěryhodné certifikační autority. Pokud chcete zobrazit výzvy, vyberte **ne** . Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

    - **Vyžadovat kryptografickou vazbu**: **Ano** zabraňuje připojením k serverům PEAP, které během vyjednávání protokolu PEAP nepoužívají kryptografických. **Ne** , nevyžaduje kryptografických. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

    **OVĚŘOVÁNÍ KLIENTA**

    - **Klientský certifikát pro ověření klienta (certifikát identity)**: Použijte s typem **EAP-TLS**. Vyberte profil certifikátu použitý k ověření připojení.

    - **Metoda ověřování**: Použijte s typem **EAP-TTLS**. Vyberte metodu ověřování připojení:  

      - **Certifikáty**: Vyberte klientský certifikát, který je certifikátem identity předloženým serveru.
      - **Uživatelské jméno a heslo**: Zadejte metodu ověřování **Metoda bez protokolu EAP (vnitřní identita)**. Možnosti:

        - **Nezašifrované heslo (PAP)**
        - **Protokol CHAP (Challenge Handshake)**
        - **Protokol Microsoft CHAP (MS-CHAP)**
        - **Protokol Microsoft CHAP verze 2 (MS-CHAP v2)**

    - **Ochrana identity (vnější identita)**: Použijte s typem **EAP-TTLS**. Zadejte text odeslaný v odpovědi na požadavek identity EAP. Tento text může být libovolná hodnota. Při ověřování se nejdřív pošle tato anonymní identita a po ní následuje skutečná identifikace poslaná přes zabezpečené tunelové propojení.

- **Nastavení firemního proxy:** Zvolte nastavení proxy v organizaci. Možnosti:
  - **Žádné:** nenakonfiguruje se žádné nastavení proxy.
  - **Nakonfigurovat ručně:** Zadejte **IP adresu proxy serveru** a **Číslo portu**.
  - **Automaticky konfigurovat**: zadejte adresu URL odkazující na skript automatické konfigurace proxy serveru (PAC). Zadejte například `http://proxy.contoso.com/proxy.pac`.

- **Vynutit, aby profil Wi-Fi dodržoval standard FIPS**: Pokud chcete používat vyhodnocování proti standardu FIPS 140-2, vyberte možnost **Ano**. Tento standard se vyžaduje od všech agentur federální vlády USA, které chrání citlivé, ale ne tajné digitálně ukládané informace pomocí bezpečnostních systémů založených na kryptografii. Pokud se nemá standard FIPS dodržovat, zvolte **Ne**.

## <a name="use-an-imported-settings-file"></a>Importování souboru nastavení

Pro libovolné nastavení, které není v Intune k dispozici, můžete exportovat nastavení Wi-Fi z jiného zařízení s Windows. Tento export vytvoří soubor XML se všemi nastaveními. Potom tento soubor importujte do Intune a použijte ho jako profil Wi-Fi. Viz [Import nastavení Wi-Fi pro zařízení s Windows 8.1 a novější verzí v Microsoft Intune](wi-fi-settings-import-windows-8-1.md).

## <a name="next-steps"></a>Další kroky

Profil je vytvořen, ale nemusí provádět žádné akce. Nezapomeňte [profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).

## <a name="more-resources"></a>Další zdroje informací

- [Nastavení Windows 8.1 Wi-Fi](wi-fi-settings-import-windows-8-1.md)
- [Přehled nastavení Wi-Fi](wi-fi-settings-configure.md), včetně dalších platforem
