---
title: Konfigurace nastavení sítě VPN pro zařízení s iOS nebo iPadOS v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte profil konfigurace sítě VPN na zařízeních s iOS/iPadOS pomocí nastavení konfigurace virtuální privátní sítě (VPN). Nakonfigurujte podrobnosti připojení, metody ověřování, dělené tunelové propojení, vlastní nastavení sítě VPN s páry identifikátor, klíč-hodnota, nastavení sítě VPN pro jednotlivé aplikace, které zahrnují adresy URL Safari, a sítě VPN na vyžádání, které budou zahrnovat nastavení proxy serveru. konfigurační skript, adresa IP nebo plně kvalifikovaný název domény a port TCP v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74e889419dcaaa75c2a31fe16931dddd84d1a967
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086539"
---
# <a name="add-vpn-settings-on-ios-and-ipados-devices-in-microsoft-intune"></a>Přidání nastavení sítě VPN v zařízeních s iOS a iPadOS v Microsoft Intune

Microsoft Intune zahrnuje mnoho nastavení sítě VPN, která se dají nasadit do zařízení s iOS/iPadOS. Tato nastavení se používají k vytvoření a konfiguraci připojení sítě VPN k síti vaší organizace. Těmito nastaveními se zabývá tento článek. Některá nastavení jsou dostupná jen pro určité klienty VPN, jako je Citrix, Zscaler a další.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](vpn-settings-configure.md).

> [!NOTE]
> Tato nastavení jsou k dispozici pro všechny typy registrace. Další informace o typech registrace najdete v tématu Registrace zařízení se [systémem iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="connection-type"></a>Typ připojení

Z následujícího seznamu dodavatelů vyberte typ připojení VPN:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**: Určeno pro aplikaci [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924) verze 4.0.5x a starší.
- **Cisco AnyConnect**: Určeno pro aplikaci [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690) verze 4.0.7x a novější.
- **SonicWall Mobile Connect**
- **Starší verze F5 Access**: Určeno pro aplikaci F5 Access verze 2.1 a starší.
- **F5 Access**: Určeno pro aplikaci F5 Access verze 3.0 a novější.
- **Palo Alto Networks GlobalProtect (starší verze)** : Určeno pro aplikaci Palo Alto Networks GlobalProtect verze 4.1 a starší.
- **Palo Alto Networks GlobalProtect**: Určeno pro aplikaci Palo Alto Networks GlobalProtect verze 5.0 a novější.
- **Pulse Secure**
- **Cisco (IPSec)**
- **Citrix VPN**
- **Citrix SSO**
- **Zscaler**: Pokud chcete použít podmíněný přístup, nebo pokud chcete uživatelům dovolit obejít přihlašovací obrazovku Zscaler, musíte do svého účtu Azure AD integrovat Zscaler Private Access (ZPA). Podrobné pokyny najdete v [dokumentaci k aplikaci Zscaler](https://help.zscaler.com/zpa/configuration-example-microsoft-azure-ad). 
- **IKEv2**: [Nastavení IKEv2](#ikev2-settings) (v tomto článku) popisuje vlastnosti.
- **Vlastní VPN**

> [!NOTE]
> Společnosti Cisco, Citrix, F5 a Palo Alto oznámily, že v iOSu 12 nebudou starší klienti fungovat. Co nejdříve byste tak měli provést migraci do nových aplikací. Další informace najdete na [blogu technické podpory pro Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## <a name="base-vpn-settings"></a>Základní nastavení sítě VPN

Nastavení, která jsou v následujícím seznamu, jsou ovlivněná zvoleným typem připojení k síti VPN.  

- **Název připojení**: Tento název koncoví uživatelé vidí, když na svém zařízení procházejí seznamem dostupných připojení VPN.
- **Vlastní název domény** (jenom Zscaler): předvyplňte přihlašovací pole aplikace Zscaler s doménou, do které uživatelé patří. Například pokud je uživatelské jméno `Joe@contoso.net`, zobrazí se při otevření aplikace v poli statická doména `contoso.net`. Pokud nezadáte název domény, použije se v Azure Active Directory (AD) doménová část hlavního názvu uživatele (UPN).
- **IP adresa nebo plně kvalifikovaný název domény**: IP adresa nebo plně kvalifikovaný název domény serveru VPN, ke kterému se zařízení připojí Zadejte například `192.168.1.1` nebo `vpn.contoso.com`.
- **Název cloudu organizace** (pouze Zscaler): Zadejte název cloudu, ve kterém je organizace zřízena. Název je v adrese URL, kterou používáte k přihlášení do aplikace Zscaler.  
- **Metoda ověřování**: Zvolte způsob, kterým se zařízení ověřují vůči serveru VPN. 
  - **Certifikáty**: V části **Ověřovací certifikát** vyberte existující profil certifikátu SCEP nebo PKCS pro ověřování připojení. V článku [Konfigurace certifikátů](../protect/certificates-configure.md) najdete pokyny k profilům certifikátů.
  - **Uživatelé jméno a heslo**: koncoví uživatelé musí zadat uživatelské jméno a heslo, aby se mohli přihlásit k serveru VPN.  

    > [!NOTE]
    > Pokud se jako metoda ověřování pro Cicso IPsec VPN používá uživatelské jméno a heslo, musí prostřednictvím vlastního profilu Apple Configuratoru poskytovat tajný kód SharedSecret.

  - **Odvozené přihlašovací údaje**: použijte certifikát, který je odvozený od čipové karty uživatele. Pokud není nakonfigurovaný žádný odvozený Vydavatel přihlašovacích údajů, Intune vás vyzve, abyste ho přidali. Další informace najdete v tématu [použití odvozených přihlašovacích údajů v Microsoft Intune](../protect/derived-credentials.md).

- **Vyloučené adresy URL** (jen Zscaler): Pokud jsou uvedené adresy URL připojené k síti VPN Zscaleru, jsou k dispozici i mimo cloud Zscaler. 

- **Rozdělit tunel**: tuto možnost můžete **povolit** nebo **zakázat**, aby se zařízení mohla rozhodnout, které připojení se má v závislosti na typech přenosů používat. Uživatel v hotelu například pro přístup k pracovním souborům použije připojení VPN, ale pro běžné procházení webu bude používat standardní síť hotelu.

- **Identifikátor VPN** (vlastní VPN, Zscaler a Citrix): identifikátor aplikace VPN, kterou používáte, a který poskytuje poskytovatel sítě VPN.
- **Zadejte páry klíč/hodnota pro vlastní atributy sítě VPN vaší organizace** (vlastní VPN, Zscaler a Citrix): přidejte nebo importujte **klíče** a **hodnoty** , které přizpůsobují připojení k síti VPN. Nezapomeňte, že tyto hodnoty obvykle dodá poskytovatel připojení VPN.

- **Povolit řízení přístupu k síti (NAC)** (Cisco AnyConnect, Citrix SSO, F5 Access): když zvolíte **Souhlasím, ID**zařízení je zahrnuté v profilu sítě VPN. Toto ID se dá použít k ověřování sítě VPN pro povolení nebo zákaz přístupu k síti.

  **Při použití Cisco AnyConnect s ISE**nezapomeňte:

  - Pokud jste to ještě neudělali, Integrujte ISE do Intune pro NAC, jak je popsáno v tématu **konfigurace Microsoft Intune jako MDM Server** v [příručce pro správce služby Cisco identity Services Engine](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html).
  - Povolí NAC v profilu sítě VPN.

  **Při použití jednotného přihlašování pro Citrix s bránou**nezapomeňte:

  - Potvrďte, že používáte 12.0.59 nebo novější bránu Citrix Gateway.
  - Potvrďte, že uživatelé mají na svých zařízeních nainstalovaný Citrix SSO 1.1.6 nebo novější.
  - Integrujte bránu Citrix s Intune pro NAC. Podívejte se na téma [integration Microsoft Intune/Enterprise Mobility Suite with NetScaler (scénář LDAP + heslem)](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf) příručka pro nasazení Citrix.
  - Povolí NAC v profilu sítě VPN.

  **Při použití přístupu F5**nezapomeňte:

  - Potvrďte, že používáte F5 BIG-IP 13.1.1.5 nebo novější. 
  - Integrujte BIG-IP s Intune for NAC. Další informace najdete v tématu [Přehled: Konfigurace APM pro stav kontrol zařízení pomocí Průvodce pro správu koncových bodů](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) F5.
  - Povolí NAC v profilu sítě VPN.

  Pro partnery VPN, kteří podporují ID zařízení, může získat ID klient VPN, jako je Citrix SSO. Pak se může dotazovat Intune, aby zkontroloval, jestli je zařízení zaregistrované, a jestli profil VPN vyhovuje nebo nedodržuje předpisy.

  - Pokud chcete toto nastavení odebrat, znovu profil vytvořte, ale nevybírejte při tom **Souhlasím**. Pak profil znovu přiřaďte.

## <a name="ikev2-settings"></a>Nastavení IKEv2

Tato nastavení se použijí, když zvolíte **Typ připojení** > **IKEv2**.

- **Vždycky zapnutá síť VPN**: **Povolit** nastaví klienta VPN tak, aby se automaticky připojoval a znovu připojil k síti VPN. Neustále aktivní připojení VPN zůstávají ve spojení nebo se ihned připojí, jakmile uživatel zamkne zařízení, zařízení se restartuje nebo se změní bezdrátová síť. Pokud je nastavené na **Zakázat** (výchozí), je vždycky zapnutá síť VPN pro všechny klienty VPN. Pokud je tato možnost povolená, nakonfigurujte taky:

  - **Síťové rozhraní**: všechna nastavení IKEv2 se vztahují jenom na síťové rozhraní, které zvolíte. Možnosti:
    - **Wi-Fi a mobilní síť** (výchozí): nastavení IKEv2 se vztahuje na rozhraní Wi-Fi a mobilní rozhraní v zařízení.
    - **Mobilní**: nastavení IKEv2 se vztahuje jenom na mobilní rozhraní na zařízení. Tuto možnost vyberte, pokud nasazujete do zařízení s vypnutým nebo odebraným rozhraním Wi-Fi.
    - **Wi-Fi**: nastavení IKEv2 se vztahuje jenom na rozhraní Wi-Fi na zařízení.
  - **Uživatel, který zakáže konfiguraci sítě VPN**: **možnost Povolit** umožňuje uživatelům vypnout funkci Always On VPN. **Disable** (výchozí) zabrání uživatelům v jeho vypnutí. Výchozí hodnota tohoto nastavení je nejbezpečnější možnost.
  - **Hlasová pošta**: vyberte, co se stane s přenosem pomocí hlasové pošty, pokud je povolená možnost vždycky zapnuto Možnosti:
    - **Vynutit síťový provoz prostřednictvím sítě VPN** (výchozí nastavení): Toto nastavení představuje nejbezpečnější možnost.
    - **Povolení předávání síťového provozu mimo VPN**
    - **Odpojit síťový provoz**
  - Postup **tisku**: vyberte, co se stane s přenosem v provozu, pokud je povolená možnost vždycky zapnutá síť VPN. Možnosti:
    - **Vynutit síťový provoz prostřednictvím sítě VPN** (výchozí nastavení): Toto nastavení představuje nejbezpečnější možnost.
    - **Povolení předávání síťového provozu mimo VPN**
    - **Odpojit síťový provoz**
  - **Mobilní služby**: v iOS 13.0 + vyberte, co se stane s mobilními přenosy, pokud je povolená možnost vždycky zapnutá síť VPN. Možnosti:
    - **Vynutit síťový provoz prostřednictvím sítě VPN** (výchozí nastavení): Toto nastavení představuje nejbezpečnější možnost.
    - **Povolení předávání síťového provozu mimo VPN**
    - **Odpojit síťový provoz**
  - **Povolení provozu z nenativních bezplatných síťových aplikací k předávání mimo síť VPN: v neintegrované**síti se obvykle nachází v restauracích a hotelových sítích Wi-Fi. Možnosti:
    - **Ne**: vynucuje provoz všech nedobrovolných síťových přenosů (CN) prostřednictvím tunelového připojení VPN.
    - **Ano, všechny aplikace**: umožňuje, aby všechny přenosy aplikace propojené sítě VPN nepoužívaly.
    - **Ano, konkrétní aplikace**: **přidá** seznam aplikací propojené sítě, jejichž provoz může obejít síť VPN. Zadejte identifikátory sady prostředků aplikace CN. Zadejte například `com.contoso.app.id.package`.

  - **Provoz z neobsluhované aplikace weblist, který se má předat mimo VPN**: vestavěný weblist je integrovaný webový prohlížeč, který zpracovává přihlašovacího přihlášení. Při použití této **možnost povolíte** , aby aplikace prohlížeče mohla obejít síť VPN. **Disable** (výchozí) vynutí provoz na weblist, aby používal síť VPN Always On. Výchozí hodnota je nejbezpečnější možnost.
  - **Interval kontroly udržení adres (NAT)** (v sekundách): Pokud chcete zůstat připojení k síti VPN, zařízení zachová aktivní síťové pakety. Zadejte hodnotu v sekundách, jak často se tyto pakety odesílají, od 20-1440. Zadejte například hodnotu `60` pro odeslání síťových paketů do sítě VPN každých 60 sekund. Ve výchozím nastavení je tato hodnota nastavená na `110` sekund.
  - Přesměrovat nastavení protokolu **NAT na hardware, když je zařízení v režimu spánku**: když je zařízení v režimu spánku, **Povolit** (výchozí) NAT nepřetržitě odesílá pakety Keep-Alive, takže zařízení zůstane připojené k síti VPN. **Disable** tuto funkci vypne.

- **Vzdálený identifikátor**: zadejte síťovou IP adresu, plně kvalifikovaný název domény, USERFQDN nebo ASN1DN serveru IKEv2. Zadejte například `10.0.0.3` nebo `vpn.contoso.com`. Obvykle zadáváte stejnou hodnotu jako [**název připojení**](#base-vpn-settings) (v tomto článku). Ale závisí na nastavení serveru IKEv2.

- **Typ ověřování klienta**: Vyberte způsob, jakým se klient VPN ověřuje pro síť VPN. Možnosti:
  - **Ověření uživatele** (výchozí): ověření přihlašovacích údajů uživatele u sítě VPN.
  - **Ověřování počítače**: ověření přihlašovacích údajů zařízení k síti VPN.

- **Metoda ověřování**: Vyberte typ přihlašovacích údajů klienta, které chcete odeslat na server. Možnosti:
  - **Certifikáty**: k ověření připojení k síti VPN používá existující profil certifikátu. Ujistěte se, že tento profil certifikátu je už přiřazený uživateli nebo zařízení. V opačném případě se připojení VPN nezdařilo.
    - **Typ certifikátu**: Vyberte typ šifrování používaný certifikátem. Ujistěte se, že je server VPN nakonfigurován tak, aby přijímal tento typ certifikátu. Možnosti:
      - **RSA** (výchozí)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Uživatelské jméno a heslo** (jenom ověřování uživatelů): když se uživatelé připojí k síti VPN, zobrazí se jim výzva k zadání uživatelského jména a hesla.
  - **Sdílený tajný klíč** (pouze ověřování počítače): umožňuje zadat sdílený tajný klíč, který se odešle na server VPN.
    - **Sdílený tajný klíč**: Zadejte sdílený tajný klíč, který se označuje také jako předsdílený klíč (PSK). Ujistěte se, že hodnota odpovídá sdílenému tajnému kódu nakonfigurovanému na serveru VPN.

- **Běžný název vystavitele certifikátu serveru**: umožňuje serveru VPN ověřování pro klienta VPN. Zadejte běžný název vystavitele certifikátu (CN) certifikátu serveru VPN, který je odeslán klientovi VPN na zařízení. Ujistěte se, že hodnota CN odpovídá konfiguraci na serveru VPN. V opačném případě se připojení VPN nezdařilo.
- **Běžný název certifikátu serveru**: zadejte cn pro samotný certifikát. Pokud je ponecháno prázdné, použije se hodnota vzdáleného identifikátoru.

- **Rychlost detekce nedoručených partnerů**: vyberte, jak často klient sítě VPN kontroluje, jestli je tunel VPN aktivní. Možnosti:
  - **Nenakonfigurováno**: používá výchozí systém iOS/iPadOS, který se může shodovat s volbou **střední**.
  - **None**: zakáže detekci mrtvého partnera.
  - **Nízká**: pošle zprávu kontroly kontroly a každých 30 minut.
  - **Střední** (výchozí): odešle zprávu kontroly stavu kontroly každých 10 minut.
  - **Vysoká**: pošle zprávu o prohození každých 60 sekund.

- **Minimální rozsah verze TLS**: zadejte minimální verzi TLS, kterou chcete použít. Zadejte `1.0`, `1.1`nebo `1.2`. Pokud necháte pole prázdné, použije se výchozí hodnota `1.0`.
- **Maximální hodnota rozsahu verze TLS**: zadejte maximální verzi TLS, která se má použít. Zadejte `1.0`, `1.1`nebo `1.2`. Pokud necháte pole prázdné, použije se výchozí hodnota `1.2`.

> [!NOTE]
> Při použití ověřování uživatelů a certifikátů je potřeba nastavit minimální a maximální rozsah verze TLS.

- **Perfect Forward Secrecy**: výběrem **Povolit** zapněte metodu PFS (Perfect Forward Secrecy). PFS je funkce zabezpečení protokolu IP, která snižuje dopad v případě ohrožení zabezpečení klíče relace. **Disable** (default) nepoužívá metodu PFS.
- **Ověření odvolání certifikátu**: výběrem možnosti **Povolit** zajistěte, aby se certifikáty odvolaly, než povolíte úspěšné připojení k síti VPN. Tato kontroler je nejlepší úsilí. Pokud vyprší časový limit serveru VPN před zjištěním, jestli je certifikát odvolaný, udělí se přístup. **Disable** (výchozí) nekontroluje odvolané certifikáty.

- **Konfigurovat parametry přidružení zabezpečení**: **Nenakonfigurováno** (výchozí) používá výchozí systém iOS/iPadOS. Pokud chcete zadat parametry používané při vytváření přidružení zabezpečení se serverem VPN, vyberte **Povolit** .
  - **Šifrovací algoritmus**: vyberte algoritmus, který chcete:
    - DES
    - ŠIFROVÁNÍ
    - AES-128
    - AES-256 (výchozí)
    - AES-128 – GCM
    - AES-256-GCM
  - **Algoritmus integrity**: vyberte algoritmus, který chcete:
    - SHA1-96
    - SHA1 – 160
    - SHA2-256 (výchozí)
    - SHA2 – 384
    - SHA2 – 512
  - **Skupina Diffie-Hellman**: vyberte skupinu, kterou chcete. Výchozí hodnota je skupina `2`.
  - **Doba života** (minuty): vyberte, jak dlouho zůstane přidružení zabezpečení aktivní, dokud se klíče neotáčí. Zadejte celou hodnotu mezi `10` a `1440` (1440 minut je 24 hodin). Výchozí hodnota je `1440`.

- **Konfigurace samostatné sady parametrů pro podřízená přidružení zabezpečení**: iOS/iPadOS umožňuje konfigurovat samostatné parametry pro připojení IKE a všechna podřízená připojení. 

  **Nenakonfigurováno** (výchozí) používá hodnoty, které zadáte v nastavení dříve **Konfigurovat parametry přidružení zabezpečení** . Pokud chcete zadat parametry používané při vytváření *podřízených* přidružení zabezpečení se serverem VPN, vyberte **Povolit** .
  - **Šifrovací algoritmus**: vyberte algoritmus, který chcete:
    - DES
    - ŠIFROVÁNÍ
    - AES-128
    - AES-256 (výchozí)
    - AES-128 – GCM
    - AES-256-GCM
  - **Algoritmus integrity**: vyberte algoritmus, který chcete:
    - SHA1-96
    - SHA1 – 160
    - SHA2-256 (výchozí)
    - SHA2 – 384
    - SHA2 – 512
  - **Skupina Diffie-Hellman**: vyberte skupinu, kterou chcete. Výchozí hodnota je skupina `2`.
  - **Doba života** (minuty): vyberte, jak dlouho zůstane přidružení zabezpečení aktivní, dokud se klíče neotáčí. Zadejte celou hodnotu mezi `10` a `1440` (1440 minut je 24 hodin). Výchozí hodnota je `1440`.

## <a name="automatic-vpn-settings"></a>Automatické nastavení sítě VPN

- **VPN pro jednotlivé aplikace:** Umožňuje používat síť VPN pro jednotlivé aplikace. Při otevření určitých aplikací automaticky aktivuje připojení VPN. Aplikace také můžete přidružit k danému profilu sítě VPN. SÍŤ VPN pro jednotlivé aplikace není v IKEv2 podporována. Další informace najdete v tématu [pokyny pro nastavení sítě VPN pro jednotlivé aplikace pro iOS/iPadOS](vpn-setting-configure-per-app.md). 
  - **Typ zprostředkovatele:** Je k dispozici jen pro Pulse Secure a Vlastní VPN.
  - Pokud používáte profily **sítě VPN pro** iOS/IPadOS s Pulse Secure nebo vlastní sítí VPN, vyberte tunelové propojení vrstev (App-proxy) nebo tunelové propojení na úrovni paketů (Packet-Tunnel). U tunelování v aplikační vrstvě nastavte hodnotu **ProviderType** na **app-proxy**, u tunelování na úrovni paketů na **packet-tunnel**. Pokud si nejste jistí, jakou hodnotu použít, podívejte se do dokumentace poskytovatele připojení VPN.
  - **Adresy URL Safari, které aktivují tuto síť VPN:** Můžete přidat jednu nebo více adres URL webu. Při návštěvě těchto adres URL pomocí prohlížeče Safari na zařízení se automaticky naváže připojení k VPN.

- **Síť VPN na vyžádání:** Nakonfigurujte podmíněná pravidla, která řídí, kdy se má připojení VPN spustit. Můžete třeba vytvořit podmínku, že se připojení VPN použije, jen pokud zařízení není připojené k firemní síti Wi-Fi. Nebo vytvořte podmínku. Pokud například zařízení nemá přístup k zadané doméně hledání DNS, pak se připojení VPN nespustí.

  - **Identifikátory SSID nebo domény hledání DNS**: Vyberte, jestli se v této podmínce používají identifikátory **SSID** bezdrátové sítě nebo **domény hledání DNS**. Zvolte **Přidat** a nakonfigurujte minimálně jeden identifikátor SSID nebo doménu hledání.
  - **Test řetězce adresy URL**: Toto nastavení je volitelné. Zadejte adresu URL, kterou pravidlo použije pro účely testování. Pokud zařízení přistupuje k této adrese URL bez přesměrování, spustí se připojení VPN. A zařízení se připojí k cílové adrese URL. Uživatel neuvidí testovací web řetězce adresy URL.

    Například test řetězce adresy URL je audit URL webového serveru, který kontroluje dodržování předpisů zařízením před připojením k síti VPN. Adresa URL taky testuje schopnost sítě VPN připojit se k lokalitě předtím, než se zařízení připojí k cílové adrese URL prostřednictvím sítě VPN.

  - **Akce domény**: Zvolte jednu z následujících možností:
    - Připojit v případě potřeby
    - Nepřipojovat
  - **Akce**: Zvolte jednu z následujících možností:
    - Připojit
    - Vyhodnotit připojení
    - Ignorovat
    - Odpojit

## <a name="proxy-settings"></a>Nastavení proxy serveru

Pokud používáte proxy server, nakonfigurujte následující nastavení. Nastavení proxy serveru nejsou k dispozici pro připojení VPN typu Zscaler.  

- **Skript automatické konfigurace**: ke konfiguraci proxy serveru použijte konfigurační soubor. Zadejte **adresu URL proxy serveru** (například `http://proxy.contoso.com`), na které je konfigurační soubor.
- **Adresa**: Zadejte IP adresu plně kvalifikovaného názvu hostitele proxy serveru.
- **Číslo portu**: Zadejte číslo portu přidruženého k proxy serveru.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Nakonfigurujte nastavení sítě VPN na zařízeních se systémem [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [MacOS](vpn-settings-macos.md)a [Windows 10](vpn-settings-windows-10.md) .
