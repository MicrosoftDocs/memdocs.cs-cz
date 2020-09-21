---
title: Nastavení firewallu zabezpečení koncového bodu Intune | Microsoft Docs
description: Nastavení zásad brány firewall zabezpečení koncového bodu pro Windows a macOS v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
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
ms.openlocfilehash: 9b6af399d0f3fbd721932b47e8f1bc388711ca58
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814708"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad brány firewall pro zabezpečení koncového bodu v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro zásady *brány firewall* v uzlu zabezpečení koncového bodu služby Intune jako součást [zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Podporované platformy a profily:

- **macOS**:
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

- **Stavová protokol FTP (File Transfer Protocol) (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Nenakonfigurováno** (*výchozí*)
  - **Povoleno** – brána firewall provádí filtrování stavových protokol FTP (File Transfer Protocol) (FTP) pro povolení sekundárních připojení. 
  - **Zakázaný** stav FTP je zakázaný.

- **Počet sekund, po které může být přidružení zabezpečení nečinné, než se odstraní**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Zadejte čas v sekundách mezi 300 a 3600, jak dlouho se přidružení zabezpečení uchovávají po tom, co se nezobrazuje síťový provoz.
  
  Pokud nezadáte žádnou hodnotu, systém odstraní přidružení zabezpečení po nečinnosti po 300 sekundách.
  
- **Kódování předsdíleného klíče**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Pokud nepotřebujete *UTF-8*, předsdílené klíče se zpočátku zakódují pomocí kódování UTF-8. Pak uživatelé zařízení můžou zvolit jinou metodu kódování.

  - **Nenakonfigurováno** (*výchozí*)
  - **Žádný**
  - **UTF**

- **Žádné výjimky pro IP adresu brány firewall sec**  
  - **Nenakonfigurováno** (*výchozí*) – Pokud není nakonfigurovaný, budete mít přístup k následujícím nastavením pro výjimku protokolu IP, která můžete nakonfigurovat individuálně.
  - **Ano** – vypne výjimky brány firewall s protokolem IPSec. Následující nastavení není možné konfigurovat.

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
  - **Nenakonfigurováno** (*výchozí*) – použijte výchozí nastavení klienta, které umožňuje zakázat ověření seznamu CRL.
  - **Žádný**
  - **Byl**
  - **Vyžadovat**

- **Vyžadovat, aby se moduly klíčů ignorovaly jenom pro ověřovací sady, které nepodporují**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Nenakonfigurováno** (*výchozí*)
  - **Zakázáno**
  - **Povoleno** – moduly pro tvorbu klíčů ignorují nepodporované sady ověřování.

- **Řízení front paketů**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Určete, jak povolit škálování softwaru na straně příjmu pro šifrované přijímání a prostý text před scénářem brány IPsec pro tunelové připojení. Tím se zajistí zachování pořadí paketů.
  - **Nenakonfigurováno** (*výchozí*) – služba Řízení front paketů se vrátí do výchozího stavu klienta, který je zakázaný.
  - **Zakázáno**
  - **Příchozí fronta**
  - **Odchozí fronta**
  - **Zařadit do fronty**

- **Zapnout firewall v programu Microsoft Defender pro doménové sítě**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nenakonfigurováno** (*výchozí*) – klient se vrátí k výchozímu, což znamená povolení brány firewall.
  - **Ano** – firewall **v programu Microsoft** Defender pro typ sítě je zapnutý a vynucované. Získáte také přístup k dalším nastavením této sítě.
  - **Ne** – zakázat bránu firewall.

  Další nastavení pro tuto síť, pokud je nastaveno na *Ano*:

  - **Blokovat neviditelný režim**  
    CSP: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    Ve výchozím nastavení je v zařízeních povolený neviditelný režim. Pomáhá zabránit uživatelům se zlými úmysly v zjišťování informací o síťových zařízeních a službách, které spouštějí. Zakázáním režimu utajení můžou být zařízení zranitelná vůči útokům.
    - **Nenakonfigurováno** *(výchozí)*
    - **Ano**
    - **Ne**

  - **Povolit stíněný režim**  
    CSP: [stíněný](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Nenakonfigurováno** *(výchozí)* – použijte výchozí nastavení klienta, které slouží k zakázání stíněného režimu.
    - **Ano** – počítač je přepnut do *chráněného režimu*, který ho izoluje od sítě. Veškerý provoz je zablokovaný.
    - **Ne**

  - **Blokovat odezvy jednosměrového vysílání na vysílání vícesměrového vysílání**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, kterým se povolí jednosměrové odpovědi.
    - **Yes** Odpovědi na jednosměrové vysílání v případě odesílání na vícesměrové vysílání jsou zablokované.
    - **Ne** – vynutilo výchozí nastavení klienta, což umožňuje používat jednosměrové odpovědi.

  - **Zakázat příchozí oznámení**  
    [DISABLEINBOUNDNOTIFICATIONS](https://go.microsoft.com/fwlink/?linkid=872563) CSP
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které umožní oznámení uživateli.
    - **Ano** – oznámení uživateli je potlačeno, pokud je aplikace blokována příchozím pravidlem.
    - **Žádná** oznámení o uživateli nejsou povolena.

  - **Blokovat odchozí připojení**  

    *Toto nastavení platí pro Windows verze 1809 a novější*.
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    Toto pravidlo je vyhodnoceno na konci seznamu pravidel.
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, což umožňuje připojení.
    - **Ano** – všechna odchozí připojení, která neodpovídají odchozímu pravidlu, jsou blokovaná.
    - **Ne** – všechna připojení, která neodpovídají odchozímu pravidlu, jsou povolená.

  - **Blokovat příchozí připojení**  
    CSP: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    Toto pravidlo je vyhodnoceno na konci seznamu pravidel.
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, kterým se zablokuje připojení.
    - **Ano** – všechna příchozí připojení, která neodpovídají příchozímu pravidlu, jsou blokovaná.
    - **Ne** – všechna připojení, která neodpovídají příchozímu pravidlu, jsou povolená.

  - **Ignorovat pravidla brány firewall autorizovaných aplikací**  
    CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – pravidla brány firewall aplikací ověřená v místním úložišti se ignorují.
    - Nejsou dodržena **žádná** pravidla brány firewall pro aplikace, která nejsou autorizována.

  - **Ignorovat pravidla brány firewall globálního portu**  
    CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – globální pravidla brány firewall portu v místním úložišti se ignorují.
    - **Ne** – budou dodržena globální pravidla brány firewall portů.

  - **Ignorovat všechna místní pravidla brány firewall**  
    CSP: [IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – všechna pravidla brány firewall v místním úložišti se ignorují.
    - **Ne** – respektují se pravidla brány firewall v místním úložišti.

  - **Ignorovat pravidla zabezpečení připojení** CSP: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – pravidla brány firewall IPsec v místním úložišti se ignorují.
    - V místním úložišti se neuplatňují pravidla brány **firewall pro IPsec** .

- **Zapnout firewall v programu Microsoft Defender pro privátní sítě**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nenakonfigurováno** (*výchozí*) – klient se vrátí k výchozímu, což znamená povolení brány firewall.
  - **Ano** – firewall v programu Microsoft Defender pro typ sítě **Private** je zapnutý a vynucované. Získáte také přístup k dalším nastavením této sítě.
  - **Ne** – zakázat bránu firewall.

  Další nastavení pro tuto síť, pokud je nastaveno na *Ano*:

  - **Blokovat neviditelný režim**  
    CSP: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    Ve výchozím nastavení je v zařízeních povolený neviditelný režim. Pomáhá zabránit uživatelům se zlými úmysly v zjišťování informací o síťových zařízeních a službách, které spouštějí. Zakázáním režimu utajení můžou být zařízení zranitelná vůči útokům.
    - **Nenakonfigurováno** *(výchozí)*
    - **Ano**
    - **Ne**

  - **Povolit stíněný režim**  
    CSP: [stíněný](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Nenakonfigurováno** *(výchozí)* – použijte výchozí nastavení klienta, které slouží k zakázání stíněného režimu.
    - **Ano** – počítač je přepnut do *chráněného režimu*, který ho izoluje od sítě. Veškerý provoz je zablokovaný.
    - **Ne**

  - **Blokovat odezvy jednosměrového vysílání na vysílání vícesměrového vysílání**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, kterým se povolí jednosměrové odpovědi.
    - **Yes** Odpovědi na jednosměrové vysílání v případě odesílání na vícesměrové vysílání jsou zablokované.
    - **Ne** – vynutilo výchozí nastavení klienta, což umožňuje používat jednosměrové odpovědi.

  - **Zakázat příchozí oznámení**  
    [DISABLEINBOUNDNOTIFICATIONS](https://go.microsoft.com/fwlink/?linkid=872563) CSP
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které umožní oznámení uživateli.
    - **Ano** – oznámení uživateli je potlačeno, pokud je aplikace blokována příchozím pravidlem.
    - **Žádná** oznámení o uživateli nejsou povolena.

  - **Blokovat odchozí připojení**  

    *Toto nastavení platí pro Windows verze 1809 a novější*.
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    Toto pravidlo je vyhodnoceno na konci seznamu pravidel.
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, což umožňuje připojení.
    - **Ano** – všechna odchozí připojení, která neodpovídají odchozímu pravidlu, jsou blokovaná.
    - **Ne** – všechna připojení, která neodpovídají odchozímu pravidlu, jsou povolená.

  - **Blokovat příchozí připojení**  
    CSP: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    Toto pravidlo je vyhodnoceno na konci seznamu pravidel.
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, kterým se zablokuje připojení.
    - **Ano** – všechna příchozí připojení, která neodpovídají příchozímu pravidlu, jsou blokovaná.
    - **Ne** – všechna připojení, která neodpovídají příchozímu pravidlu, jsou povolená.

  - **Ignorovat pravidla brány firewall autorizovaných aplikací**  
    CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – pravidla brány firewall aplikací ověřená v místním úložišti se ignorují.
    - Nejsou dodržena **žádná** pravidla brány firewall pro aplikace, která nejsou autorizována.

  - **Ignorovat pravidla brány firewall globálního portu**  
    CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – globální pravidla brány firewall portu v místním úložišti se ignorují.
    - **Ne** – budou dodržena globální pravidla brány firewall portů.

  - **Ignorovat všechna místní pravidla brány firewall**  
    CSP: [IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – všechna pravidla brány firewall v místním úložišti se ignorují.
    - **Ne** – respektují se pravidla brány firewall v místním úložišti.

  - **Ignorovat pravidla zabezpečení připojení** CSP: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – pravidla brány firewall IPsec v místním úložišti se ignorují.
    - V místním úložišti se neuplatňují pravidla brány **firewall pro IPsec** .

- **Zapnout firewall v programu Microsoft Defender pro veřejné sítě**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nenakonfigurováno** (*výchozí*) – klient se vrátí k výchozímu, což znamená povolení brány firewall.
  - **Ano** – firewall **v programu Microsoft** Defender pro typ sítě je zapnutý a vynucované. Získáte také přístup k dalším nastavením této sítě.
  - **Ne** – zakázat bránu firewall.

  Další nastavení pro tuto síť, pokud je nastaveno na *Ano*:

  - **Blokovat neviditelný režim**  
    CSP: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    Ve výchozím nastavení je v zařízeních povolený neviditelný režim. Pomáhá zabránit uživatelům se zlými úmysly v zjišťování informací o síťových zařízeních a službách, které spouštějí. Zakázáním režimu utajení můžou být zařízení zranitelná vůči útokům.
    - **Nenakonfigurováno** *(výchozí)*
    - **Ano**
    - **Ne**

  - **Povolit stíněný režim**  
    CSP: [stíněný](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Nenakonfigurováno** *(výchozí)* – použijte výchozí nastavení klienta, které slouží k zakázání stíněného režimu.
    - **Ano** – počítač je přepnut do *chráněného režimu*, který ho izoluje od sítě. Veškerý provoz je zablokovaný.
    - **Ne**

  - **Blokovat odezvy jednosměrového vysílání na vysílání vícesměrového vysílání**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, kterým se povolí jednosměrové odpovědi.
    - **Yes** Odpovědi na jednosměrové vysílání v případě odesílání na vícesměrové vysílání jsou zablokované.
    - **Ne** – vynutilo výchozí nastavení klienta, což umožňuje používat jednosměrové odpovědi.

  - **Zakázat příchozí oznámení**  
    [DISABLEINBOUNDNOTIFICATIONS](https://go.microsoft.com/fwlink/?linkid=872563) CSP
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které umožní oznámení uživateli.
    - **Ano** – oznámení uživateli je potlačeno, pokud je aplikace blokována příchozím pravidlem.
    - **Žádná** oznámení o uživateli nejsou povolena.

  - **Blokovat odchozí připojení**  

    *Toto nastavení platí pro Windows verze 1809 a novější*.
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    Toto pravidlo je vyhodnoceno na konci seznamu pravidel.
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, což umožňuje připojení.
    - **Ano** – všechna odchozí připojení, která neodpovídají odchozímu pravidlu, jsou blokovaná.
    - **Ne** – všechna připojení, která neodpovídají odchozímu pravidlu, jsou povolená.

  - **Blokovat příchozí připojení**  
    CSP: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    Toto pravidlo je vyhodnoceno na konci seznamu pravidel.
    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, kterým se zablokuje připojení.
    - **Ano** – všechna příchozí připojení, která neodpovídají příchozímu pravidlu, jsou blokovaná.
    - **Ne** – všechna připojení, která neodpovídají příchozímu pravidlu, jsou povolená.

  - **Ignorovat pravidla brány firewall autorizovaných aplikací**  
    CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – pravidla brány firewall aplikací ověřená v místním úložišti se ignorují.
    - Nejsou dodržena **žádná** pravidla brány firewall pro aplikace, která nejsou autorizována.

  - **Ignorovat pravidla brány firewall globálního portu**  
    CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – globální pravidla brány firewall portu v místním úložišti se ignorují.
    - **Ne** – budou dodržena globální pravidla brány firewall portů.

  - **Ignorovat všechna místní pravidla brány firewall**  
    CSP: [IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – všechna pravidla brány firewall v místním úložišti se ignorují.
    - **Ne** – respektují se pravidla brány firewall v místním úložišti.

  - **Ignorovat pravidla zabezpečení připojení** CSP: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Nenakonfigurováno** *(výchozí)* – nastavení se vrátí do výchozího nastavení klienta, které má respektovat místní pravidla.
    - **Ano** – pravidla brány firewall IPsec v místním úložišti se ignorují.
    - V místním úložišti se neuplatňují pravidla brány **firewall pro IPsec** .

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
  - **Doména**
  - **Hlášen**
  - **Republik**
  - **Není nakonfigurováno**

- **Název rodiny balíčků**  
  [Get-AppxPackage](/previous-versions//hh856044(v=technet.10))

  Názvy rodin balíčků můžete načíst spuštěním příkazu Get-AppxPackage z PowerShellu.

- **Cesta k souboru**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](/windows/client-management/mdm/firewall-csp#filepath)

  Pokud chcete zadat cestu k souboru aplikace, zadejte umístění aplikací v klientském zařízení. Například: `C:\Windows\System\Notepad.exe` nebo `%WINDIR%\Notepad.exe`

- **Název služby**  
  [FirewallRules/FirewallRuleName/App/ServiceName](/windows/client-management/mdm/firewall-csp#servicename)

  Pokud služba, ne aplikace, odesílá nebo přijímá provoz, používejte krátký název služby Windows. Krátké názvy služby se načítají spuštěním `Get-Service` příkazu z PowerShellu.

- **Protokol**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](/windows/client-management/mdm/firewall-csp#protocol)

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
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Zadejte seznam autorizovaných místních uživatelů pro toto pravidlo. Seznam autorizovaných uživatelů nelze zadat, je-li *název služby* v této zásadě nastaven jako služba systému Windows. Pokud není zadán žádný autorizovaný uživatel, výchozí hodnota je *Všichni uživatelé*.

- **Libovolná místní adresa**  
  **Nenakonfigurováno** (*výchozí*) – pro konfiguraci rozsahu adres pro podporu použijte následující nastavení, *rozsahy místních adres**.
  - **Ano** – podporuje jakoukoli místní adresu a nekonfigurujte rozsah adres.

- **Rozsahy místních adres**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Umožňuje spravovat místní rozsah adres pro toto pravidlo. Další možnosti:
  - **Přidejte** jednu nebo více adres jako čárkami oddělený seznam místních adres, na které se vztahuje pravidlo.
  - **Importujte** soubor. csv, který obsahuje seznam adres, které se mají použít jako rozsahy místních adres.
  - **Exportujte** aktuální seznam místních rozsahů adres jako soubor. csv.

  Platné položky (tokeny) obsahují následující možnosti:
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
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Umožňuje spravovat vzdálené rozsahy adres pro toto pravidlo. Další možnosti:
  - **Přidejte** jednu nebo více adres jako čárkami oddělený seznam vzdálených adres, na které se vztahuje pravidlo.
  - **Importujte** soubor. csv, který obsahuje seznam adres, které se mají použít jako rozsahy vzdálených adres.
  - **Exportujte** aktuální seznam rozsahů vzdálených adres jako soubor. csv.

  Platné položky (tokeny) zahrnují následující a bez rozlišení velkých a malých písmen:
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