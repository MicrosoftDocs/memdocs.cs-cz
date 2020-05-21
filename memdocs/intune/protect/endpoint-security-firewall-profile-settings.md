---
title: Nastavení firewallu zabezpečení koncového bodu Intune | Microsoft Docs
description: Nastavení zásad brány firewall zabezpečení koncového bodu pro Windows a macOS v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431289"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad brány firewall pro zabezpečení koncového bodu v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro zásady *brány firewall* v uzlu zabezpečení koncového bodu služby Intune jako součást [zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Podporované platformy a profily:

- **MacOS**:
  - Profil: **MacOS firewall**

- **Windows 10 a novější**:
  - Profil: **firewall v programu Microsoft Defender**

## <a name="macos-firewall-profile"></a>Profil brány firewall macOS

### <a name="firewall"></a>Brána firewall

Následující nastavení jsou nakonfigurovaná jako [zásady zabezpečení koncového bodu pro MacOS brány firewall](../protect/endpoint-security-firewall-policy.md) .

- **Povolit bránu firewall**

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – povolit bránu firewall.
  
  Pokud nastavíte *Ano*, můžete nakonfigurovat následující nastavení.  

  - **Blokovat všechna příchozí připojení**

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zablokuje všechna příchozí připojení s výjimkou připojení, která jsou nutná pro základní internetové služby, jako jsou DHCP, Bonjour a IPSec. Tím se zablokuje všechny služby sdílení.

  - **Povolit režim utajení**

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zabrání počítači v reakci na požadavky na zjišťování. Počítač bude nadále odpovídat na požadavky oprávněných aplikací.

  - **Aplikace brány firewall** Rozbalte rozevírací seznam a pak vyberte **Přidat** a zadejte aplikace a pravidla pro příchozí připojení pro aplikaci.
    - **Povolení příchozích připojení**
      - Nenakonfigurováno
      - Blok
      - Povolit

    - **ID sady** – ID identifikuje aplikaci. Příklad: *com. Apple. app*

## <a name="microsoft-defender-firewall-profile"></a>Profil firewallu v programu Microsoft Defender

### <a name="microsoft-defender-firewall"></a>Firewall v programu Microsoft Defender

Následující nastavení jsou nakonfigurovaná jako [zásady zabezpečení koncového bodu pro brány firewall systému Windows 10](../protect/endpoint-security-firewall-policy.md).

- **Zakázat stavovou protokol FTP (File Transfer Protocol) (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Nenakonfigurováno** (*výchozí*) – brána firewall používá ke kontrole a filtrování sekundárních síťových připojení protokol FTP, což by mohlo způsobit ignorování pravidel brány firewall.
  - **Ano**
  
- **Počet sekund, po které může být přidružení zabezpečení nečinné, než se odstraní**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Zadejte čas v sekundách mezi 300 a 3600, jak dlouho se přidružení zabezpečení uchovávají po tom, co se nezobrazuje síťový provoz.
  
  Pokud nezadáte žádnou hodnotu, systém odstraní přidružení zabezpečení po nečinnosti po 300 sekundách.
  
- **Kódování předsdíleného klíče**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Pokud nepotřebujete *UTF-8*, předsdílené klíče se zpočátku zakódují pomocí kódování UTF-8. Pak uživatelé zařízení můžou zvolit jinou metodu kódování.

  - **Nenakonfigurováno** (*výchozí*)
  - **Žádné**
  - **UTF**

- **Výjimky brány firewall s povoleným PROTOKOLem Neighbor Discovery**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – výjimky protokolu IPSec brány firewall umožňují sousední zjišťování.

- **Výjimka brány firewall protokolu IP s povoleným protokolem ICMP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – výjimky protokolu IPSec brány firewall umožňují protokol ICMP.

- **Výjimky brány firewall protokolu IP s umožňují zjišťování směrovačů**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – výjimky protokolu IPSec brány firewall umožňují zjišťování směrovačů.

- **Výjimka brány firewall protokolu IP s povoleným protokolem DHCP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – výjimky brány firewall s protokolem IP s umožňují protokol DHCP

- **Ověření seznamu odvolaných certifikátů (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Určete, jak se vynutilo ověřování seznamu odvolaných certifikátů (CRL).
  - **Nenakonfigurováno** (*výchozí*) – výchozí nastavení klienta je zakázat ověření seznamu CRL.
  - **Žádné**
  - **Byl**
  - **Vyžadovat**

- **Vyžadovat, aby se moduly klíčů ignorovaly jenom pro ověřovací sady, které nepodporují**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – moduly pro tvorbu klíčů ignorují nepodporované sady ověřování.

- **Řízení front paketů**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Určete, jak povolit škálování softwaru na straně příjmu pro šifrované přijímání a prostý text před scénářem brány IPsec pro tunelové připojení. Tím se zajistí zachování pořadí paketů.
  - **Nenakonfigurováno** (*výchozí*) – služba Řízení front paketů se vrátí zpátky do výchozího nastavení klienta, což je zakázané.
  - **Disabled** (Zakázáno)
  - **Příchozí fronta**
  - **Odchozí fronta**
  - **Zařadit do fronty**

- **Zapnout firewall v programu Microsoft Defender pro doménové sítě**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nenakonfigurováno** (*výchozí*) – klient se vrátí k výchozímu, což znamená povolení brány firewall.
  - **Ano** – firewall **v programu Microsoft** Defender pro typ sítě je zapnutý a vynucované.
  - **Ne** – zakázat bránu firewall.

- **Zapnout firewall v programu Microsoft Defender pro privátní sítě**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nenakonfigurováno** (*výchozí*) – klient se vrátí k výchozímu, což znamená povolení brány firewall.
  - **Ano** – firewall v programu Microsoft Defender pro typ sítě **Private** je zapnutý a vynucované.
  - **Ne** – zakázat bránu firewall.

- **Zapnout firewall v programu Microsoft Defender pro veřejné sítě**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nenakonfigurováno** (*výchozí*) – klient se vrátí k výchozímu, což znamená povolení brány firewall.
  - **Ano** – firewall **v programu Microsoft** Defender pro typ sítě je zapnutý a vynucované.
  - **Ne** – zakázat bránu firewall.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Pravidla firewallu v programu Microsoft Defender

*Tento profil je ve verzi Preview*.

Následující nastavení jsou nakonfigurovaná jako [zásady zabezpečení koncového bodu pro brány firewall systému Windows 10](../protect/endpoint-security-firewall-policy.md).

#### <a name="windows-firewall-rule"></a>Pravidlo brány Windows Firewall

- **Název**  
  Zadejte popisný název pravidla. Tento název se zobrazí v seznamu pravidel, který vám pomůže ho identifikovat.

- **Popis**  
  Zadejte popis pravidla.

- **Směr**  
  - **Nenakonfigurováno** (*výchozí*) – Toto pravidlo je výchozím nastavením odchozího provozu.
  - **Out** – toto pravidlo se vztahuje na odchozí přenosy.
  - Toto pravidlo se **vztahuje na příchozí** přenosy.

- **Akce**  
  - **Nenakonfigurováno** (*výchozí*) – pravidlo standardně povoluje provoz.
  - **Blokované** – provoz se zablokuje ve *směru* , který jste nakonfigurovali.
  - **Povoleno** – provoz je povolen ve *směru* , který jste nakonfigurovali.

- **Typ sítě**  
  Zadejte typ sítě, ke kterému pravidlo patří. Můžete vybrat jednu nebo více z následujících možností. Pokud nevyberete možnost, bude pravidlo platit pro všechny typy sítí.
  - **Domain**
  - **Hlášen**
  - **Republik**
  - **Není nakonfigurováno**

- **Název rodiny balíčků**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  Názvy rodin balíčků můžete načíst spuštěním příkazu Get-AppxPackage z PowerShellu.

- **Cesta k souboru**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  Pokud chcete zadat cestu k souboru aplikace, zadejte umístění aplikací v klientském zařízení. Například: `C:\Windows\System\Notepad.exe` nebo`%WINDIR%\Notepad.exe`

- **Název služby**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Pokud služba, ne aplikace, odesílá nebo přijímá provoz, používejte krátký název služby Windows. Krátké názvy služby se načítají spuštěním `Get-Service` příkazu z PowerShellu.

- **Protocol (Protokol)**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Zadejte protokol pro toto pravidlo portu.
  - Protokoly přenosové vrstvy, jako jsou *TCP (6)* a *UDP (17)* , umožňují zadat porty nebo rozsahy portů.
  - Pro vlastní protokoly zadejte číslo mezi *0* a *255* , které představuje protokol IP.
  - Pokud není nic zadáno, **použije se výchozí pravidlo.**

- **Typy rozhraní**  
  Zadejte typy rozhraní, do kterých pravidlo patří. Můžete vybrat jednu nebo více z následujících možností. Pokud nevyberete možnost, pravidlo se vztahuje na všechny typy rozhraní:
  - **Vzdálený přístup**
  - **Bezdrátová síť**
  - **Místní síť**
  - **Není nakonfigurováno**

- **Autorizovaní uživatelé**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Zadejte seznam autorizovaných místních uživatelů pro toto pravidlo. Seznam autorizovaných uživatelů nelze zadat, je-li *název služby* v této zásadě nastaven jako služba systému Windows. Pokud není zadán žádný autorizovaný uživatel, výchozí hodnota je *Všichni uživatelé*.

- **Libovolná místní adresa**  
  **Nenakonfigurováno** (*výchozí*) – pro konfiguraci rozsahu adres pro podporu použijte následující nastavení, *rozsahy místních adres**.
  - **Ano** – podporuje jakoukoli místní adresu a nekonfigurujte rozsah adres.

- **Rozsahy místních adres**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Přidejte jednu nebo více adres jako čárkami oddělený seznam místních adres, na které se vztahuje pravidlo. Platné položky (tokeny) obsahují následující možnosti:
  - **Hvězdička** – hvězdička ( \* ) označuje libovolnou místní adresu. Pokud je k dispozici, hvězdička musí být jediným tokenem, který je součástí.
  - **Podsíť** – zadejte podsítě pomocí masky podsítě nebo zápisu předpony sítě. Pokud není Zadaná maska podsítě nebo předpona sítě, použije se výchozí maska podsítě 255.255.255.255.
  - **Platná IPv6 adresa**
  - **Rozsah adres IPv4** – rozsahy IPv4 adres musí být ve formátu *adresy počáteční adresy – koncová adresa* bez zahrnutých mezer, přičemž počáteční adresa je menší, než koncová adresa.
  - **Rozsah adres IPv6** – rozsahy IPv6 adres musí být ve formátu *adresy počáteční adresy* , bez zahrnutých mezer, přičemž počáteční adresa je menší než koncová adresa.

  Pokud není zadána žádná hodnota, toto nastavení nastaví jako výchozí hodnotu použít *libovolnou adresu*.

- **Jakákoli Vzdálená adresa**  
  **Nenakonfigurováno** (*výchozí*) – ke konfiguraci rozsahu adres pro podporu použijte následující nastavení, *vzdálené rozsahy adres**.
  - **Ano** – podporuje všechny vzdálené adresy a nekonfigurujte rozsah adres.

- **Vzdálené rozsahy adres**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Přidejte jednu nebo více adres jako čárkami oddělený seznam vzdálených adres, na které se vztahuje pravidlo. Platné položky (tokeny) zahrnují následující a bez rozlišení velkých a malých písmen:
  - **Hvězdička** – hvězdička ( \* ) označuje jakoukoli vzdálenou adresu. Pokud je k dispozici, hvězdička musí být jediným tokenem, který je součástí.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** podporovaný na zařízeních se systémem Windows 1809 nebo novějším.
  - **RmtIntranet** – podporováno na zařízeních, na kterých běží Windows 1809 nebo novější.
  - **Ply2Renders** – podporováno na zařízeních, na kterých běží Windows 1809 nebo novější.
  - **LocalSubnet** – označuje libovolnou místní adresu v místní podsíti.
  - **Podsíť** – zadejte podsítě pomocí masky podsítě nebo zápisu předpony sítě. Pokud není Zadaná maska podsítě nebo předpona sítě, je maska podsítě standardně 255.255.255.255.
  - **Platná IPv6 adresa**
  - **Rozsah adres IPv4** – rozsahy IPv4 adres musí být ve formátu *adresy počáteční adresy – koncová adresa* bez zahrnutých mezer, přičemž počáteční adresa je menší, než koncová adresa.
  - **Rozsah adres IPv6** – rozsahy IPv6 adres musí být ve formátu *adresy počáteční adresy* , bez zahrnutých mezer, přičemž počáteční adresa je menší než koncová adresa.

  Pokud není zadána žádná hodnota, toto nastavení nastaví jako výchozí hodnotu použít *libovolnou adresu*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Další kroky

[Zásady zabezpečení koncového bodu pro brány firewall](../protect/endpoint-security-firewall-policy.md)
