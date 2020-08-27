---
title: Nastavení sítě VPN pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si a přečtěte si o všech dostupných nastaveních sítě VPN v Microsoft Intune, k čemu se používají, a o tom, co dělají. Podívejte se na pravidla přenosů, podmíněný přístup a DNS a proxy serveru pro zařízení s Windows 10 a Windows holografickým pro firmy.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: tycast
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 25bb413aefa7d91ea825bbe96e057994b1375413
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915496"
---
# <a name="windows-10-and-windows-holographic-device-settings-to-add-vpn-connections-using-intune"></a>Nastavení zařízení s Windows 10 a Windows holografické pro přidání připojení k síti VPN pomocí Intune

Pomocí Microsoft Intune můžete přidat a nakonfigurovat připojení k síti VPN pro zařízení. Tento článek obsahuje seznam a popisuje běžná nastavení a funkce při vytváření virtuálních privátních sítí (VPN). Tato nastavení a funkce sítě VPN se používají v profilech konfigurace zařízení v Intune, která jsou vložená nebo nasazená do zařízení.

V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, včetně použití dodavatele sítě VPN, povolení funkcí Always On, DNS, přidání proxy serveru a dalších.

Tato nastavení platí pro zařízení se systémem:

- Windows 10
- Windows Holographic for Business

V závislosti na tom, jaká nastavení zvolíte, nemusí být všechny uvedené hodnoty konfigurovatelné.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil konfigurace zařízení VPN](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Základní nastavení sítě VPN

- **Název připojení**: zadejte název tohoto připojení. Tento název uživatelé vidí, když na svém zařízení procházejí seznamem dostupných připojení VPN.
- **Servery**: přidejte minimálně jeden VPN server, ke kterému se budou zařízení připojovat. Při přidání serveru zadáváte tyto informace:
  - **Popis**: zadejte popisný název serveru, jako je **Contoso VPN server**.
  - **IP adresa nebo plně kvalifikovaný**název domény: zadejte IP adresu nebo plně kvalifikovaný název domény (FQDN) serveru VPN, ke kterému se zařízení připojují, například **192.168.1.1** nebo **VPN.contoso.com**.
  - **Výchozí server**: povolí tento server jako výchozí server, který budou zařízení používat k navázání připojení. Jako výchozí server nastavte jenom jeden server.
  - **Importovat**: vyhledejte soubor, který obsahuje seznam serverů oddělených čárkami ve formátu popis, IP adresa nebo plně kvalifikovaný název domény, výchozí server. Pomocí **OK** servery naimportujte do seznamu **Servery**.
  - **Export**: exportuje seznam serverů do souboru s hodnotami oddělenými čárkami (CSV).

- **Zaregistrovat IP adresy v interní službě DNS**: výběrem možnosti **Povolit** nakonfigurujete profil sítě VPN s Windows 10 tak, aby dynamicky registroval IP adresy přiřazené k rozhraní sítě VPN pomocí interní služby DNS. Pokud vyberete možnost **Zakázat**, IP adresy se nebudou dynamicky registrovat.

- **Typ připojení**: z následujícího seznamu dodavatelů vyberte typ připojení VPN:

  - **Pulse Secure**
  - **F5 Edge Client**
  - **SonicWALL Mobile Connect**
  - **Check Point Capsule VPN**
  - **Citrix**
  - **Palo Alto Networks GlobalProtect**
  - **Automaticky**
  - **IKEv2**
  - **L2TP**
  - **PPTP**

  Když zvolíte typ připojení VPN, můžete být také vyzváni k zadání těchto nastavení:

  - **Always On**: **Povolit** automatické připojení k připojení VPN, když dojde k následujícím událostem:
    - Při přihlášení uživatelů do zařízení
    - Při změně sítě na zařízení
    - Při opětovném zapnutí obrazovky na zařízení po vypnutí

    Pokud chcete použít připojení zařízení, jako je IKEv2, **Povolte** toto nastavení.

  - **Metoda ověřování**: vyberte, jak chcete, aby se uživatelé vůči serveru VPN ověřovali. Možnosti:
    - **Uživatelské jméno a heslo**: vyžaduje, aby uživatelé zadali své uživatelské jméno a heslo domény k ověření, například `user@contoso.com` nebo `contoso\user` .
    - **Certifikáty**: Vyberte existující profil certifikátu klienta uživatele pro ověření uživatele. Tato možnost poskytuje vylepšené funkce, jako je například nulové prostředí, síť VPN na vyžádání a síť VPN pro jednotlivé aplikace.

      Informace o vytváření profilů certifikátů v Intune najdete v tématu [použití certifikátů k ověřování](../protect/certificates-configure.md).

    - **Certifikáty počítače** (jenom IKEv2): Vyberte existující profil certifikátu klienta zařízení pro ověření zařízení.

      Pokud používáte [připojení zařízení pomocí tunelového propojení](/windows-server/remote/remote-access/vpn/vpn-device-tunnel-config), musíte tuto možnost vybrat.

      Informace o vytváření profilů certifikátů v Intune najdete v tématu [použití certifikátů k ověřování](../protect/certificates-configure.md).

    - **EAP** (jenom IKEv2): Vyberte existující profil certifikátu klienta EAP (Extensible Authentication Protocol), který se má ověřit. V nastavení **protokolu EAP XML** zadejte parametry ověřování.
  - **Zapamatovat si přihlašovací údaje při každém přihlášení**: při zvolení této možnosti se přihlašovací údaje uloží do mezipaměti.
  - **Vlastní XML**: zadejte vlastní příkazy XML pro konfiguraci připojení VPN.
  - **XML protokolu EAP**: Zadejte libovolné příkazy protokolu EAP XML, které KONFIGURUJÍ připojení VPN. Další informace najdete v tématu [Konfigurace protokolu EAP](/windows/client-management/mdm/eap-configuration).

  - **Tunelové zařízení** (pouze IKEv2): **povolí možnost** připojit zařízení k síti VPN automaticky bez zásahu uživatele nebo přihlášení. Toto nastavení platí pro počítače, které jsou připojené k Azure Active Directory (AD).

    Pro použití této funkce jsou potřeba následující:

    - Nastavení **Typ připojení** je nastaveno na **IKEv2**.
    - Nastavení **Always On** je nastaveno na **Povolit**.
    - Nastavení **metody ověřování** je nastaveno na **certifikáty počítače**.

    Přiřaďte pouze jeden profil na zařízení s povoleným **tunelovým propojením zařízení** .

  **Parametry přidružení zabezpečení IKE** (jenom IKEv2): Tato nastavení kryptografie se používají během vyjednávání přidružení zabezpečení IKE (označuje se taky jako `main mode` nebo `phase 1` ) pro připojení IKEv2. Tato nastavení se musí shodovat s nastavením serveru VPN. Pokud se nastavení neshodují, profil VPN se nepřipojí.

  - **Šifrovací algoritmus**: Vyberte šifrovací algoritmus, který se používá na serveru VPN. Pokud například server VPN používá algoritmus AES 128, vyberte v seznamu možnost **AES-128** .

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  - **Algoritmus kontroly integrity**: vyberte algoritmus integrity, který se používá na serveru VPN. Pokud například server VPN používá SHA1-96, vyberte ze seznamu možnost **SHA1-96** .

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  - **Skupina Diffie-Hellman**: vyberte výpočetní skupinu Diffie-Hellman použitou na serveru VPN. Pokud například server VPN používá skupina2 (1024 bitů), pak v seznamu vyberte **2** .

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  **Parametry přidružení podřízeného zabezpečení** (jenom IKEv2): Tato nastavení kryptografie se používají během vyjednávání podřízených přidružení zabezpečení (označuje se také jako `quick mode` nebo `phase 2` ) pro připojení IKEv2. Tato nastavení se musí shodovat s nastavením serveru VPN. Pokud se nastavení neshodují, profil VPN se nepřipojí.

  - **Algoritmus transformace šifry**: vyberte algoritmus, který se používá na serveru VPN. Pokud například server VPN používá algoritmus AES-CBC 128, vyberte ze seznamu možnost **CBC-AES-128** .

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  - **Algoritmus transformace ověřování**: vyberte algoritmus, který se používá na serveru VPN. Pokud například server VPN používá algoritmus AES-GCM 128, vyberte ze seznamu možnost **GCM-AES-128** .

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  - **Skupina PFS (Perfect Forward Secrecy)**: vyberte výpočetní skupinu Diffie-Hellman, která se používá pro PFS (Perfect Forward Secrecy) na serveru VPN. Pokud například server VPN používá skupina2 (1024 bitů), pak v seznamu vyberte **2** .

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

### <a name="pulse-secure-example"></a>Příklad pro Pulse Secure

```
<pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
```

### <a name="f5-edge-client-example"></a>Příklad pro F5 Edge Client

```
<f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
```

### <a name="sonicwall-mobile-connect-example"></a>Příklad pro SonicWALL Mobile Connect
**Doména nebo skupina přihlášení**: tuto vlastnost v profilu sítě VPN nastavit nejde. Místo toho Mobile Connect tuto hodnotu analyzuje, když se zadá uživatelské jméno a doména ve formátu `username@domain` nebo `DOMAIN\username`.

Příklad:

```
<MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
```

### <a name="checkpoint-mobile-vpn-example"></a>Příklad pro CheckPoint Mobile VPN

```
<CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
```

### <a name="writing-custom-xml"></a>Psaní vlastních příkazů XML
Další informace o tom, jak psát vlastní příkazy XML, najdete v dokumentaci k síti VPN jednotlivých výrobců.

Další informace o vytváření vlastních dat XML protokolu EAP najdete v tématu [Konfigurace protokolu EAP](/windows/client-management/mdm/eap-configuration).

## <a name="apps-and-traffic-rules"></a>Pravidla pro aplikace a síťové přenosy

- **Přidružit WIP nebo aplikace k této síti VPN**: tuto možnost povolte, pokud chcete, aby toto připojení VPN používaly jenom některé aplikace. Možnosti:

  - **Přidružit WIP k tomuto připojení**: zadejte **Doménu WIP pro toto připojení**.
  - **Přidružit aplikace k tomuto připojení**: můžete **Omezit připojení ze sítě VPN k těmto aplikacím** a pak přidat **Přidružené aplikace**. Aplikace, které zadáte, automaticky použijí připojení VPN. Typ aplikace určuje identifikátor aplikace. Pro univerzální aplikace zadejte identitu aplikace (PFN). Pro desktopové aplikace zadejte cestu k souboru aplikace.

  > [!IMPORTANT]
  > Doporučujeme všechny seznamy aplikací vytvořené pro sítě VPN pro jednotlivé aplikace zabezpečit. Pokud seznam změní neoprávněný uživatel a vy seznam naimportujete do seznamu aplikací sítě VPN pro jednotlivé aplikace, potenciálně tím autorizujete přístup k síti VPN pro aplikace, které by přístup mít neměly. Jedním ze způsobů, jak zabezpečit seznamy aplikací, je použít seznam řízení přístupu (ACL).

- **Pravidla síťových přenosů pro toto připojení**k síti VPN: Vyberte protokoly a místní & vzdálený port a rozsahy adres, které jsou povolené pro připojení VPN. Když nevytvoříte pravidlo pro provoz sítě, budou povolené všechny protokoly, porty a rozsahy adres. Po vytvoření pravidla se pro připojení VPN použijí jenom protokoly, porty a rozsahy adres, které určíte v tomto pravidle.

## <a name="conditional-access"></a>Podmíněný přístup

- **Podmíněný přístup pro toto připojení k síti VPN**: umožňuje tok dodržování předpisů zařízením od klienta. Když je tato funkce povolená, komunikuje klient sítě VPN se službou Azure Active Directory (AD), aby získal certifikát pro účely ověření. U sítě VPN by mělo být nastavené ověřování certifikátem a server VPN musí důvěřovat serveru, který mu vrátí služba Azure AD.

- **Jednotné přihlašování s alternativním certifikátem**: pro dodržování předpisů zařízením použijte pro ověřování protokolem Kerberos certifikát, který je odlišný od ověřovacího certifikátu sítě VPN. Tento certifikát zadejte pomocí těchto nastavení:

  - **Název**: název rozšířeného použití klíče (EKU)
  - **Identifikátor objektu**: identifikátor objektu pro EKU
  - **Hodnota hash vystavitele**: kryptografický otisk certifikátu pro jednotné přihlašování

## <a name="dns-settings"></a>Nastavení DNS

- **Seznam hledání přípon DNS**: do pole **Přípony DNS** zadejte příponu DNS a vyberte **Přidat**. Můžete přidat mnoho přípon.

  Pokud použijete přípony DNS, můžete k vyhledání síťového prostředku použít jeho krátký název místo plně kvalifikovaného názvu domény (FQDN). Při hledání s použitím krátkého názvu se přípona automaticky určí serverem DNS. Například `utah.contoso.com` je v seznamu přípon DNS. Na `DEV-comp` použijte příkaz ping. V tomto scénáři se přeloží na `DEV-comp.utah.contoso.com`.

  Přípony DNS se překládají v uvedeném pořadí a toto pořadí lze měnit. Například `colorado.contoso.com` a `utah.contoso.com` jsou v seznamu přípon DNS a obě mají prostředek s názvem `DEV-comp`. Vzhledem k tomu, že `colorado.contoso.com` je v seznamu první, přeloží se jako `DEV-comp.colorado.contoso.com`.
  
  Pokud chcete pořadí změnit, klikněte na tečky vlevo od přípony DNS a pak přetáhněte příponu nahoru:

  ![Výběr tří teček a kliknutí a přetažení za účelem přesunutí přípony DNS](./media/vpn-settings-windows-10/vpn-settings-windows10-move-dns-suffix.png)

- **Pravidla pro tabulku zásad překladu IP adres (NRPT)**: pravidla pro překlad adres IP (NRPT) definují, jak DNS překládá názvy při připojení k síti VPN. Po navázání připojení VPN zvolíte, které servery DNS připojení VPN používá.

  Do tabulky můžete přidat pravidla, která zahrnují doménu, server DNS, proxy a další podrobnosti pro překlad domény, kterou zadáte. Připojení VPN používá tato pravidla, když se uživatelé připojí k doménám, které zadáte.

  Vyberte **Přidat** a přidejte nové pravidlo. Pro každý server zadejte:

  - **Doména**: zadejte plně kvalifikovaný název domény (FQDN) nebo příponu DNS pro použití pravidla. Můžete také zadat tečku (.) na začátku pro příponu DNS. Zadejte například `contoso.com` nebo `.allcontososubdomains.com`.
  - **Servery DNS**: zadejte IP adresu nebo server DNS, který tuto doménu vyřeší. Zadejte například `10.0.0.3` nebo `vpn.contoso.com`.
  - **Proxy**: zadejte web proxy server, který řeší doménu. Zadejte například `http://proxy.com`.
  - **Automaticky připojit**: Pokud je tato možnost **povolena**, zařízení se automaticky připojí k síti VPN, když se zařízení připojí k doméně, kterou zadáte, jako je například `contoso.com` . Pokud **není nakonfigurovaná** (výchozí), zařízení se k síti VPN automaticky nepřipojí.
  - **Persistent**: Pokud je tato možnost nastavená na **povolenou**, pravidlo zůstane v tabulce zásad překladu IP adres (NRPT), dokud se ze zařízení ručně neodebere pravidlo, a to ani po odpojení sítě VPN. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), pravidla NRPT v profilu sítě VPN se ze zařízení odeberou, když se síť VPN odpojí.

## <a name="proxy-settings"></a>Nastavení proxy serveru

- **Skript automatické konfigurace**: ke konfiguraci proxy serveru použijte konfigurační soubor. Zadejte **Adresu URL proxy serveru**, například `http://proxy.contoso.com`, která obsahuje konfigurační soubor.
- **Adresa**: zadejte adresu proxy serveru, třeba IP adresu nebo `vpn.contoso.com`.
- **Číslo portu**: zadejte číslo portu TCP vašeho proxy serveru.
- **Obejít proxy server pro místní adresy**: pokud nechcete používat proxy server pro místní adresy, pak zvolte Povolit. Toto nastavení platí, pokud server VPN vyžaduje pro připojení proxy server.

## <a name="split-tunneling"></a>Dělené tunelové propojení

- **Dělené tunelové propojení**: **Povolit** nebo **Zakázat** , aby se zařízení mohla rozhodnout, které připojení se má použít v závislosti na provozu. Uživatel v hotelu například pro přístup k pracovním souborům použije připojení VPN, ale pro běžné procházení webu bude používat standardní síť hotelu.
- **Rozdělit tunelové trasy pro toto připojení k síti VPN**: přidejte volitelné trasy pro externí poskytovatele připojení VPN. Pro každé připojení zadejte předponu cíle a velikost předpony.

## <a name="trusted-network-detection"></a>Zjištění důvěryhodné sítě

**Přípony DNS důvěryhodné sítě**: Pokud jsou uživatelé už připojení k důvěryhodné síti, můžete zařízením zabránit v automatickém připojení k jiným připojením VPN.

V případě **přípon DNS**zadejte příponu DNS, kterou chcete důvěřovat, například contoso.com, a vyberte **Přidat**. Můžete přidat tolik přípon, kolik chcete.

Pokud je uživatel připojen k příponě DNS v seznamu, uživatel se nebude automaticky připojovat k jinému připojení VPN. Uživatel pokračuje v používání důvěryhodného seznamu přípon DNS, které zadáte. Důvěryhodná síť se pořád používá i v případě, že jsou nastavené automatické triggery.

Pokud je například uživatel již připojen k důvěryhodné příponě DNS, následující automatické triggery se ignorují. Konkrétně přípony DNS v seznamu zruší všechny ostatní automatické triggery připojení, včetně:

- Vždy zapnuto
- Aktivační událost na základě aplikace
- Automatické triggery DNS

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Nakonfigurujte nastavení sítě VPN pro zařízení s [Androidem](vpn-settings-android.md), [iOS/iPadOS](vpn-settings-ios.md)a [MacOS](vpn-settings-macos.md) .