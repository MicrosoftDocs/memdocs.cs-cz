---
title: Nastavení ochrany pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Na zařízeních s Windows 10 můžete použít nebo nakonfigurovat nastavení ochrany koncových bodů, abyste povolili funkce programu Microsoft Defender, včetně ochrany Application Guard, brány firewall, filtru SmartScreen, šifrování a BitLockeru, zneužití ochrany, řízení aplikací, Security Center a zabezpečení na místních zařízeních v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3af7c91b-8292-4c7e-8d25-8834fcf3517a
ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08a9656328c6de29441a0d8b0b5e2526836cdb9b
ms.sourcegitcommit: 441d0958721b6f9b6694dfffbec77c9a49929dd3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/08/2020
ms.locfileid: "80863192"
---
# <a name="windows-10-and-later-settings-to-protect-devices-using-intune"></a>Nastavení Windows 10 (a novější) pro ochranu zařízení pomocí Intune

Microsoft Intune obsahuje řadu nastavení, která vám pomůžou chránit vaše zařízení. Tento článek popisuje všechna nastavení, která můžete povolit a konfigurovat v zařízeních s Windows 10 a novějších. Tato nastavení se v Intune vytvoří v konfiguračním profilu Endpoint Protection pro řízení zabezpečení, včetně BitLockeru a Microsoft Defenderu.  

Pokud chcete nakonfigurovat antivirovou ochranu v programu Microsoft Defender, přečtěte si téma [omezení zařízení s Windows](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)  

## <a name="before-you-begin"></a>Před zahájením  

[Vytvoření profilu konfigurace zařízení Endpoint Protection](endpoint-protection-configure.md).  

Další informace o poskytovatelích konfiguračních služeb (CSP) najdete v tématu [Reference k poskytovateli služby konfigurace](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).  

## <a name="microsoft-defender-application-guard"></a>Ochrana Application Guard v programu Microsoft Defender  

Při používání Microsoft Edge Aplikace Microsoft Defender Application Guard chrání vaše prostředí od webů, které nedůvěřují vaší organizaci. Když uživatelé navštíví weby, které nejsou uvedené ve vaší izolované síti, lokality se otevřou v rámci virtuální relace procházení technologie Hyper-V. Důvěryhodné lokality jsou definované pomocí hranice sítě, která je nakonfigurovaná v konfiguraci zařízení.  

Ochrana Application Guard je dostupná jenom pro zařízení s Windows 10 (64bitovou verzí). Tento profil nainstaluje součást Win32, pomocí které se aktivuje ochrana Application Guard.  

- **Ochrana Application Guard**  
  **Výchozí**: Nenakonfigurováno  
   Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/AllowWindowsDefenderApplicationGuard](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)  

  - **Povoleno pro Edge** – zapne tuto funkci, která otevírá nedůvěryhodné weby v kontejneru procházení virtualizovaného na Hyper-V.  
  - **Nenakonfigurováno** – na zařízení může být otevřena žádná lokalita (důvěryhodná a nedůvěryhodná).  

- **Chování schránky**  
  **Výchozí**: Nenakonfigurováno  
   Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)  

  Vyberte, které akce kopírování a vkládání jsou povolené mezi místním počítačem a virtuálním prohlížečem Application Guard.  
  - **Nenakonfigurované**  
  - **Povolí kopírování a vkládání jenom z počítačů do prohlížeče.**  
  - **Povoluje kopírování a vkládání jenom z prohlížeče na počítač.**  
  - **Povolí kopírování a vkládání mezi počítačem a prohlížečem.**  
  - **Blokovat kopírování a vkládání mezi počítačem a prohlížečem**  

- **Obsah schránky**  
  Toto nastavení je k dispozici pouze v případě, že je *chování schránky* nastaveno na jedno z nastavení *povoleno* .  
  **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/ClipboardFileType](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardfiletype)  

  Vyberte povolený obsah schránky.  
  - **Nenakonfigurované**  
  - **Textové**  
  - **Fotografií**  
  - **Text a obrázky**  

- **Externí obsah na podnikových webech**  
  **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)  

  - **Blok** – zablokuje načítání obsahu z neschválených webů.  
  - **Nenakonfigurováno** – na zařízení můžou být otevřené nepodnikové weby.  
 
- **Tisk z virtuálního prohlížeče**  
  **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/PrintingSettings](https://go.microsoft.com/fwlink/?linkid=872354)  

  - **Povolit** – povolí tisk vybraného obsahu z virtuálního prohlížeče.  
  - **Není nakonfigurováno** Zakáže všechny funkce tisku.  

  Když *povolíte* tisk, můžete nakonfigurovat následující nastavení:
  - **Typ (typy) tisku** Vyberte jednu nebo více z následujících možností:  
    - PDF  
    - XPS  
    - Místní tiskárny
    - Síťové tiskárny  

- **Shromažďovat protokoly**  
  **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [audit/AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)  

  - **Povoluje** -shromažďovat protokoly pro události, ke kterým dojde v relaci procházení ochrany Application Guard.  
  - **Nenakonfigurováno** – v rámci relace procházení nebudou shromažďovány žádné protokoly.  

- **Zachovat uživatelem generovaná data prohlížeče**  
  **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)  

  - **Povolení** Ukládat data uživatelů (například hesla, oblíbené položky a soubory cookie), která se vytvoří během relace pro virtuální procházení ochrany Application Guard.  
  - **Není nakonfigurováno** Zahodit uživatelem stažené soubory a data, když se zařízení restartuje, nebo když se uživatel odhlásí.  

- **Akcelerace grafiky**  
 **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)  
      
  - **Umožněte** rychlejší načítání webů náročných na grafiku a videa rychleji díky získání přístupu k virtuálnímu grafickému procesoru.  
  - **Není nakonfigurováno** Použijte procesor zařízení pro grafiku. Nepoužívejte virtuální grafický procesor.  

- **Stáhnout soubory do systému souborů hostitele**  
  **Výchozí**: Nenakonfigurováno  
  Zprostředkovatel kryptografických služeb Application Guard: [Nastavení/SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)  

  - **Povolit** – uživatelé můžou stahovat soubory z virtualizovaného prohlížeče do hostitelského operačního systému.  
  - **Nenakonfigurováno** – zachová místní soubory v zařízení a nestahují soubory do hostitelského souborového systému.  

## <a name="microsoft-defender-firewall"></a>Firewall v programu Microsoft Defender  
 
### <a name="global-settings"></a>Globální nastavení  

Tato nastavení platí pro všechny typy sítě.  

- **protokol FTP (File Transfer Protocol)**  
  **Výchozí**: Nenakonfigurováno  
   CSP brány firewall: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Blokování** – zakažte stavový FTP.  
  - **Nenakonfigurováno** – brána firewall má stavové filtrování FTP, které umožňuje sekundární připojení.  

- **Doba nečinnosti přidružení zabezpečení před odstraněním**  
  **Výchozí**: *Nenakonfigurováno*  
   CSP brány firewall: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)  

   Zadejte dobu nečinnosti v sekundách, po které se přidružení zabezpečení odstraní.   

- **Kódování předsdíleného klíče**  
  **Výchozí**: Nenakonfigurováno  
   CSP brány firewall: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)  

   - **Povolit** – zakódovat předem přeformátované klíče pomocí UTF-8.  
   - **Nenakonfigurováno – kódování předdefinovaných** klíčů pomocí hodnoty místního úložiště.  

- **Výjimky protokolu IPsec**  
  **Výchozí**: *Vybraná hodnota 0*  
   CSP brány firewall: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

   Vyberte jeden nebo více z následujících typů provozu, které mají být vyloučeny z protokolu IPsec:  
   - **Zjišťování kódů typu ICMP IPv6 sousedem**  
   - **Protokol ICMP**  
   - **Zjišťování kódů typu ICMP IPv6 směrovačem**  
   - **Přenosy DHCP IPv4 i IPv6**  

- **Ověření seznamu odvolaných certifikátů**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)  

  Vyberte, jak zařízení ověřuje seznam odvolaných certifikátů. Vaše možnosti jsou:  
  - **Zakázat ověření seznamu CRL**  
  - **Neúspěšné ověření seznamu CRL jenom u odvolaného certifikátu**  
  - Při **ověřování seznamu CRL došlo k chybě**.  
 

- **Oportunisticky odpovídá sadě ověřování na modul klíčů.**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)  
  
  - **Povolit** Moduly klíčů musí ignorovat pouze ověřovací sady, které nepodporují.  
  - **Není nakonfigurováno**, moduly klíčů musí ignorovat celou sadu ověřování, pokud nepodporují všechny ověřovací sady zadané v sadě.  


- **Řízení front paketů**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)  

  Určete, jak je povolené škálování softwaru na straně příjmu pro šifrované přijímání a prostý text před scénářem brány IPsec pro tunelové připojení. Toto nastavení potvrdí, že se zachová pořadí paketů. Vaše možnosti jsou:  
  - **Nenakonfigurované**  
  - **Zakázat všechny služby Řízení front paketů**  
  - **Zařadit pouze příchozí šifrované pakety do fronty**  
  - **Queue Packets po dešifrování se provede jenom pro předávání.**  
  - **Konfigurace příchozích i odchozích paketů**  

### <a name="network-settings"></a>Nastavení sítě  

Následující nastavení jsou uvedena v tomto článku v jednom okamžiku, ale všechny se vztahují na tři konkrétní typy sítě:  
- **Síť v doméně (pracovní)**  
- **Soukromá (zjistitelná) síť**  
- **Veřejná (nezjistitelná) síť**  

#### <a name="general-settings"></a>Obecná nastavení  

- **Firewall v programu Microsoft Defender**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)  
  
  - **Povolit** – Zapněte bránu firewall a rozšířené zabezpečení. 
  - **Není nakonfigurováno** Povolí veškerý provoz v síti bez ohledu na nastavení dalších zásad.  

- **Neviditelný režim**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)  
  - **Nenakonfigurované**  
  - **Blokování** – brána firewall je zablokovaná pro provoz v režimu utajení. Blokování neviditelného režimu vám umožňuje zablokovat také **výjimku zabezpečených paketů protokolu IPsec**.  
  - **Povolení** – brána firewall funguje v režimu utajení, což pomáhá zabránit odpovědím na požadavky na zjišťování.  

- **Výjimka zabezpečeného paketu protokolu IPsec s neviditelným režimem**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [DisableStealthModeIpsecSecuredPacketExemption](https://go.microsoft.com/fwlink/?linkid=872560)  

  Tato možnost je ignorována, pokud je *režim utajení* nastaven na možnost *blokovat*.  

  - **Nenakonfigurované**  
  - **Block** Zabezpečené pakety protokolu IPSec nezískají výjimky.  
  - **Povolit** – povolit výjimky. Režim utajení brány firewall nesmí bránit hostitelskému počítači v reakci na nevyžádaný síťový provoz zabezpečený protokolem IPsec.  

- **Stíněné**  
  **Výchozí**: Nenakonfigurováno  
  Firewall CSP: [stíněný](https://go.microsoft.com/fwlink/?linkid=872561)  
    - **Nenakonfigurované**  
    - **Blokovat** – když je zapnutá brána firewall v programu Microsoft Defender a toto nastavení je nastavené na *blokovat*, veškerý příchozí provoz se zablokuje bez ohledu na nastavení dalších zásad. 
    - **Povolit** – Pokud je nastavené na *Povolit*, toto nastavení je vypnuté – a na základě dalších nastavení zásad je povolený příchozí provoz.

- **Jednosměrové odpovědi na vysílání vícesměrového vysílání**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)  
  
  Jednosměrové odpovědi na zprávy vícesměrového nebo všesměrového vysílání obvykle nebudete chtít přijímat. Tyto odpovědi mohou označovat útok na útok DoS (Denial of Service) nebo útočník, který se pokouší zjistit známý živý počítač.  
  - **Nenakonfigurované**  
  - **Blokování** – zakažte odezvy jednosměrového vysílání na vysílání vícesměrového vysílání.  
  - **Povolení** – povolí jednosměrové odpovědi na vysílání vícesměrového vysílání.  

- **Příchozí oznámení**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=8725630)  

  - **Nenakonfigurované**  
  - **Blok** – skryje oznámení, která se použijí, když je aplikace blokovaná pro naslouchání na portu.  
  - **Povolit** – povolí toto nastavení a může uživatelům zobrazovat oznámení, když je aplikace blokovaná na portu blokována.  

- **Výchozí akce pro odchozí připojení**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)  
  
  Nakonfigurujte výchozí akci, kterou firewall provede u odchozích připojení. Toto nastavení se použije pro Windows verze 1809 a vyšší.  

  - **Nenakonfigurované**  
  - **Block** – výchozí akce brány firewall neběží na odchozím provozu, pokud není explicitně zadáte blokování.  
  - **Povoleno** – výchozí akce brány firewall jsou spouštěny u odchozích připojení.  

- **Výchozí akce pro příchozí připojení**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)  
 
  - **Nenakonfigurované**  
  - **Blokovat** – výchozí akce brány firewall se nespouští u příchozích připojení.  
  - **Povolit** – výchozí akce brány firewall se spouštějí u příchozích připojení.  

#### <a name="rule-merging"></a>Sloučení pravidel  

- **Oprávnění brány firewall v programu Microsoft Defender pro autorizované aplikace z místního úložiště**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)  

  - **Nenakonfigurované**  
  - **Blokovat** – pravidla brány firewall autorizovaných aplikací v místním úložišti se ignorují a neuplatňují.  
  - **Povolit** -
   zvolit **Povolit** použije pravidla brány firewall v místním úložišti, aby byla rozpoznaná a vynutila.  

- **Globální port pravidla firewallu v programu Microsoft Defender z místního úložiště**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)  

  - **Nenakonfigurované**  
  - **Blok** – globální pravidla brány firewall portu v místním úložišti se ignorují a neuplatňují.  
  - **Povolení** – použít a vyhovět pravidla firewallu globálního portu v místním úložišti  

- **Pravidla firewallu v programu Microsoft Defender z místního úložiště**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)  

  - **Nenakonfigurované**  
  - **Blokování** – pravidla firewallu z místního úložiště se ignorují a neuplatňují.
  - **Povolí** rozpoznání a vykonání pravidel brány firewall v místním úložišti.  

- **Pravidla IPsec z místního úložiště**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)  

  - **Nenakonfigurované**  
  - **Blokovat** – pravidla zabezpečení připojení z místního úložiště se ignorují a neuplatňují bez ohledu na verzi schématu a verzi pravidla zabezpečení připojení.  
  - **Povolí** – použije pravidla zabezpečení připojení z místního úložiště bez ohledu na verze schématu nebo pravidla zabezpečení připojení.  

### <a name="firewall-rules"></a>Pravidla brány firewall  

Můžete **Přidat** jedno nebo více vlastních pravidel brány firewall. Další informace najdete v tématu [Přidání vlastních pravidel brány firewall pro zařízení s Windows 10](endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices).  

Vlastní pravidla brány firewall podporují tyto možnosti:  

#### <a name="general-settings"></a>Obecná nastavení:  

- **Název**  
  **Výchozí**: *žádný název*  

  Zadejte popisný název pravidla. Tento název se zobrazí v seznamu pravidel, který vám pomůže ho identifikovat.  

- **Popis**  
  **Výchozí**: *bez popisu*  

  Zadejte popis pravidla.  

-   **směru**  
  **Výchozí**: Nenakonfigurováno  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/Direction](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#direction)  
  
  Určete, jestli se toto pravidlo vztahuje na **příchozí**nebo **odchozí** provoz. Pokud je nastavená jako **nenakonfigurovaná**, pravidlo se automaticky použije pro odchozí přenosy.  

- **Akce**  
  **Výchozí**: Nenakonfigurováno  
  Firewall CSP: [FirewallRules/*FirewallRuleName*za akci](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#action)a [FirewallRules/*FirewallRuleName*/Action/Type](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#type)  

  Vyberte z **povolených** nebo **blokovaných**. Pokud je nastavená jako **nenakonfigurovaná**, pravidlo povolí provoz.  

- **Typ sítě**  
  **Výchozí**: vybraná hodnota 0  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/Profiles](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#profiles)  

  Vyberte až tři typy sítí, do kterých toto pravidlo patří. Mezi možnosti patří **doména**, **privátní**a **Veřejná**.  Pokud nejsou vybrané žádné typy sítí, pravidlo se použije na všechny tři typy sítě.  

#### <a name="application-settings"></a>Nastavení aplikací  

- **Aplikace (y)**  
  **Výchozí**: vše  

  Řízení připojení aplikace nebo programu. Vyberte jednu z následujících možností a dokončete další konfiguraci:  
  - **Název rodiny balíčků** – zadejte název rodiny balíčků. Pokud chcete najít název řady balíčků, použijte příkaz PowerShellu **Get-AppxPackage**.   
    CSP brány firewall: [FirewallRules/*FirewallRuleName*/App/PackageFamilyName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#packagefamilyname)  
 
  - **Cesta k souboru** – je nutné zadat cestu k souboru aplikace v klientském zařízení, což může být absolutní cesta nebo relativní cesta. Příklad: C:\Windows\System\Notepad.exe nebo%WINDIR%\Notepad.exe.  
    CSP brány firewall: [FirewallRules/*FirewallRuleName*/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)  

  - **Služba systému Windows** – zadejte krátký název služby systému Windows, pokud se jedná o službu, nikoli o aplikaci, která odesílá nebo přijímá provoz. Chcete-li najít krátký název služby, použijte příkaz prostředí PowerShell **Get-Service**.  
    CSP brány firewall: [FirewallRules/*FirewallRuleName*/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)  

  - **Vše**– *k dispozici není žádná další konfigurace*.  

#### <a name="ip-address-settings"></a>Nastavení IP adresy  

Zadejte místní a vzdálené adresy, na které se toto pravidlo vztahuje.  

-    **místních adres**  
  **Výchozí**: Libovolná adresa  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  

  Vyberte **libovolnou adresu** nebo **zadanou adresu**.  

  Když použijete *zadanou adresu*, přidáte jednu nebo více adres jako čárkami oddělený seznam místních adres, na které se vztahuje pravidlo. Mezi platné tokeny patří:  
  - Pro *libovolnou* místní adresu použijte hvězdičku (*). Pokud použijete hvězdičku, musí se jednat o jediný token, který používáte.  
  - Chcete-li určit podsíť, použijte buď masku podsítě, nebo zápis předpony sítě. Pokud není Zadaná maska podsítě ani předpona sítě, je maska podsítě standardně 255.255.255.255.  
  - Platná adresa IPv6.  
  - Rozsah IPv4 adres ve formátu "počáteční adresa-koncová adresa", včetně nezahrnutých mezer.  
  - Rozsah adres IPv6 ve formátu "počáteční adresa-koncová adresa" bez zahrnutých mezer.  

- **Vzdálené adresy**  
  **Výchozí**: Libovolná adresa  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  
 
  Vyberte **libovolnou adresu** nebo **zadanou adresu**.  

  Když použijete *zadanou adresu*, přidáte jednu nebo více adres jako čárkami oddělený seznam vzdálených adres, na které se vztahuje pravidlo. U tokenů se nerozlišují velká a malá písmena. Mezi platné tokeny patří:  
  - Pro *libovolnou* vzdálenou adresu použijte hvězdičku "*". Pokud použijete hvězdičku, musí se jednat o jediný token, který používáte.  
  - "Defaultgateway"  
  - DANÉ  
  - NÁZV  
  - UDÁVANÁ  
  - Intranet (podporuje se ve verzích Windows 1809 a novějších)  
  - "RmtIntranet" (podporováno ve verzích Windows 1809 a novějších)  
  - Internet (podporuje se ve verzích Windows 1809 a novějších)  
  - "Ply2Renders" (podporováno ve verzích Windows 1809 a novějších)  
  - "LocalSubnet" označuje jakoukoli místní adresu v místní podsíti.  
  - Chcete-li určit podsíť, použijte buď masku podsítě, nebo zápis předpony sítě. Pokud není Zadaná maska podsítě ani předpona sítě, je maska podsítě standardně 255.255.255.255.  
  - Platná adresa IPv6.  
  - Rozsah IPv4 adres ve formátu "počáteční adresa-koncová adresa", včetně nezahrnutých mezer.  
  - Rozsah adres IPv6 ve formátu "počáteční adresa-koncová adresa" bez zahrnutých mezer.  

#### <a name="port-and-protocol-settings"></a>Nastavení portu a protokolu  
Zadejte místní a vzdálené porty, na které se toto pravidlo vztahuje.  

- **Protokol**  
  **Výchozí**: Any  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)  
  Vyberte některou z následujících možností a dokončete všechny požadované konfigurace:  
  - **Vše** – k dispozici není žádná další konfigurace.  
  - **TCP** – konfigurace místních a vzdálených portů. Obě možnosti podporují všechny porty nebo zadané porty. Zadejte zadané porty pomocí čárkami odděleného seznamu.  
    - **Místní porty** – zprostředkovatel brány firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Vzdálené porty** – zprostředkovatel brány firewall: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **UDP** – konfigurace místních a vzdálených portů. Obě možnosti podporují všechny porty nebo zadané porty. Zadejte zadané porty pomocí čárkami odděleného seznamu.  
    - **Místní porty** – zprostředkovatel brány firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Vzdálené porty** – zprostředkovatel brány firewall: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **Vlastní** – zadejte číslo vlastního **protokolu** od 0 do 255.  

#### <a name="advanced-configuration"></a>Pokročilá konfigurace  
- **Typy rozhraní**  
  **Výchozí**: vybraná hodnota 0  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/InterfaceTypes](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#interfacetypes)  

  Vyberte z následujících možností:  
  - **Vzdálený přístup**  
  - **Síti**  
  - **Místní síť**  

- **Povolujte jenom připojení od těchto uživatelů.**  
  **Výchozí**: všichni uživatelé *(výchozí pro všechna použití, pokud není zadaný žádný seznam)*  
  CSP brány firewall: [FirewallRules/*FirewallRuleName*/LocalUserAuthorizationList](https://aka.ms/intunefirewallauthorizedusers)  

  Zadejte seznam autorizovaných místních uživatelů pro toto pravidlo. Pokud se toto pravidlo vztahuje na službu systému Windows, nelze zadat seznam autorizovaných uživatelů.  


## <a name="microsoft-defender-smartscreen-settings"></a>Nastavení filtru SmartScreen v programu Microsoft Defender  
 
V zařízení musí být nainstalovaný Microsoft Edge.  

- **Filtr SmartScreen pro aplikace a soubory**  
  **Výchozí**: Nenakonfigurováno  
   Zprostředkovatel SmartScreen: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)  

  - **Nenakonfigurováno** – zakáže použití filtru SmartScreen.  
  - **Povolit** – povolit Windows SmartScreen pro provádění souborů a spouštění aplikací. SmartScreen je cloudová antiphisingová a antimalwarová vrstva ochrany.  

- **Provádění neověřených souborů**  
  **Výchozí**: Nenakonfigurováno  
   Zprostředkovatel SmartScreen: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Nenakonfigurováno** – zakáže tuto funkci a koncovým uživatelům umožní spouštět soubory, které nebyly ověřeny.  
  - **Blokovat** – zabrání koncovým uživatelům spouštět soubory, které nebyly ověřeny filtrem SmartScreen systému Windows.  

## <a name="windows-encryption"></a>Šifrování Windows  
 
### <a name="windows-settings"></a>Nastavení systému Windows  

- **Šifrovat zařízení**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)  

  - **Vyžadovat** – vyzvat uživatele k povolení šifrování zařízení V závislosti na edici Windows a konfiguraci systému se může od uživatelů vyžadovat:  
    - Potvrďte, že šifrování od jiného zprostředkovatele není povolené.  
    - Je nutné vypnout nástroj BitLocker Drive Encryption a pak znovu zapnout nástroj BitLocker.  
  - **Nenakonfigurované**  
  
  Pokud je zapnuto šifrování Windows a současně je aktivní jiná metoda šifrování, mohlo by to narušit stabilitu zařízení.  

- **Šifrování paměťové karty (jenom mobilní zařízení)**  
  *Toto nastavení platí jenom pro Windows 10 Mobile.*  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)  

  - **Vyžaduje** zašifrování jakýchkoli vyměnitelných paměťových karet používaných zařízením.  
  - **Nenakonfigurováno** – Nevyžadovat šifrování paměťové karty a nedotazovat uživatele na jeho zapnutí.  

### <a name="bitlocker-base-settings"></a>Základní nastavení BitLockeru  

Základní nastavení jsou univerzální nastavení BitLockeru pro všechny typy datových jednotek. Tato nastavení určují, které úkoly šifrování jednotek nebo možnosti konfigurace může koncový uživatel upravit na všech typech datových jednotek.  

- **Upozornění pro jiné šifrování disku**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)  

  - **Blokovat** – zakáže upozornění, pokud je na zařízení jiná služba šifrování disku.  
  - **Nenakonfigurováno** – povolí zobrazení upozornění pro další šifrování disku.  

  > [!TIP]  
  > Chcete-li nainstalovat nástroj BitLocker automaticky a tiše na zařízení, které je připojené k Azure AD, a spustí systém Windows 1809 nebo novější, musí být toto nastavení nastaveno na *blokovat*. Další informace najdete v tématu [tiché zapnutí nástroje BitLocker na zařízeních](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  Když se nastaví *blokování*, můžete nakonfigurovat následující nastavení:  

  - **Povolit Standard uživatelům povolit šifrování během připojení ke službě Azure AD**  
    *Toto nastavení platí jenom pro zařízení s Azure Active Directory připojená (Azure ADJ) a závisí na předchozím nastavení `Warning for other disk encryption`.*  
    **Výchozí**: Nenakonfigurováno  
    CSP nástroje BitLocker: [AllowStandardUserEncryption](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowstandarduserencryption)

     - **Povolit** – standardní uživatelé (bez správců) můžou povolit šifrování BitLockeru, když se přihlásí.  
     - **Nenakonfigurovaní** jenom správci můžou na zařízení povolit šifrování BitLockeru.  

  > [!TIP]  
  > K automatickému a tiché instalaci nástroje BitLocker na zařízení, které je připojené k Azure AD, se používá systém Windows 1809 nebo novější, musí být toto nastavení nastavené na *Povolit*. Další informace najdete v tématu [tiché zapnutí nástroje BitLocker na zařízeních](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Konfigurace metod šifrování**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Povolit** – nakonfigurujte algoritmy šifrování pro operační systém, data a vyměnitelné jednotky.  
  - **Nenakonfigurováno** – BitLocker používá jako výchozí metodu šifrování XTS-AES 128 nebo používá metodu šifrování určenou jakýmkoli skriptem instalace.  

  Když nastavíte možnost *Povolit*, můžete nakonfigurovat následující nastavení:  

  - **Šifrování pro jednotky operačního systému**  
    **Výchozí**: XTS-AES 128-bit  
   
    Vyberte metodu šifrování pro jednotky operačního systému. Doporučujeme použít algoritmus XTS-AES.  
    - **AES-CBC 128-bit**  
    - **AES-CBC 256-bit**  
    - **XTS-AES 128-bit**  
    - **XTS-AES 256-bit**  

  - **Šifrování pevných datových jednotek**  
    **Výchozí**: AES-CBC 128-bit  
   
    Vyberte metodu šifrování pro pevné (integrované) datové jednotky. Doporučujeme použít algoritmus XTS-AES.  
    - **AES-CBC 128-bit**  
    - **AES-CBC 256-bit**  
    - **XTS-AES 128-bit**  
    - **XTS-AES 256-bit**  

  - **Šifrování vyměnitelných datových jednotek**  
    **Výchozí**: AES-CBC 128-bit  

    Vyberte metodu šifrování pro vyměnitelné datové jednotky. Pokud se vyměnitelná jednotka používá se zařízeními s jiným systémem než Windows 10, doporučujeme použít algoritmus AES-CBC.  
    - **AES-CBC 128-bit**  
    - **AES-CBC 256-bit**  
    - **XTS-AES 128-bit**  
    - **XTS-AES 256-bit**  

### <a name="bitlocker-os-drive-settings"></a>Nastavení BitLockeru pro jednotky s operačním systémem  

Tato nastavení platí konkrétně pro datové jednotky s operačním systémem.  

- **Další ověřování při spuštění**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)  

  - **Vyžadovat** – nakonfigurujte požadavky na ověření pro spuštění počítače, včetně použití čipu TPM (Trusted Platform Module).  
  - **Nenakonfigurováno – umožňuje** konfigurovat jenom základní možnosti na zařízeních s čipem TPM.  

  Pokud nastavíte hodnotu *vyžadovat*, můžete nakonfigurovat následující nastavení:  

  - **BitLocker s nekompatibilním čipem TPM**  
    **Výchozí**: Nenakonfigurováno  

    - **Blokovat** – zakázat použití BitLockeru v případě, že zařízení nemá kompatibilní čip TPM.  
    - **Nenakonfigurováno** – uživatelé můžou používat BitLocker bez kompatibilního čipu TPM. BitLocker může vyžadovat heslo nebo spouštěcí klíč.  

  - **Kompatibilní spuštění čipu TPM**  
    **Výchozí**: povolení čipu TPM  

    Nakonfigurujte, jestli je čip TPM povolený, povinný, nebo není povolený.  

    - **Povolení čipu TPM**  
    - **Nepovolit čip TPM**  
    - **Vyžadovat čip TPM**  

  - **Kompatibilní spouštěcí PIN kód TPM**  
    **Výchozí**: povolení spouštěcího PIN kódu s čipem TPM  

    Vyberte možnost povolení, nepovolení nebo vyžadování použití spouštěcího PIN kódu s čipem TPM. Povolení spouštěcího PIN kódu vyžaduje interakci koncového uživatele.  

    - **Povolení spouštěcího PIN kódu s čipem TPM**  
    - **Nepovolit spouštěcí PIN kód s čipem TPM**  
    - **Vyžadovat spouštěcí PIN kód s čipem TPM**

    > [!TIP]
    > K automatickému a tiché instalaci nástroje BitLocker na zařízení, které je připojené k Azure AD, se používá systém Windows 1809 nebo novější, ale toto nastavení nesmí být nastavené tak, aby *vyžadovalo spouštěcí PIN kód s čipem TPM*. Další informace najdete v tématu [tiché zapnutí nástroje BitLocker na zařízeních](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Kompatibilní spouštěcí klíč TPM**  
    **Výchozí**: povolení spouštěcího klíče s čipem TPM  

    Vyberte možnost povolení, nepovolení nebo vyžadování použití spouštěcího klíče s čipem TPM. Povolení spouštěcího klíče vyžaduje interakci koncového uživatele.  

    - **Povolení spouštěcího klíče s čipem TPM**  
    - **Nepovolit spouštěcí klíč s čipem TPM**  
    - **Vyžadovat spouštěcí klíč s čipem TPM**  

    > [!TIP]
    > K automatickému a tiché instalaci nástroje BitLocker na zařízení, které je připojené k Azure AD, se používá systém Windows 1809 nebo novější, ale toto nastavení nesmí být nastavené tak, aby *vyžadovalo spouštěcí klíč s čipem TPM*. Další informace najdete v tématu [tiché zapnutí nástroje BitLocker na zařízeních](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Kompatibilní spouštěcí klíč a PIN kód TPM**  
    **Výchozí**: povolení spouštěcího klíče a PIN kódu pomocí TPM  

    Vyberte možnost povolení, nepovolení nebo vyžadování spouštěcího klíče a kódu PIN pomocí čipu TPM. Povolení spouštěcího klíče a PIN kódu vyžaduje interakci koncového uživatele.  
    - **Povolení spouštěcího klíče a kódu PIN pomocí TPM**  
    - **Nepovolit spouštěcí klíč a PIN kód s čipem TPM**  
    - **Vyžadovat spouštěcí klíč a PIN kód s čipem TPM**   

    > [!TIP]  
    > K automatickému a tiché instalaci nástroje BitLocker na zařízení, které je připojené k Azure AD, se používá systém Windows 1809 nebo novější, ale toto nastavení nesmí být nastavené tak, aby *vyžadovalo spouštěcí klíč a PIN kód s čipem TPM*. Další informace najdete v tématu [tiché zapnutí nástroje BitLocker na zařízeních](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Minimální délka PIN kódu**  
    **Výchozí**: Nenakonfigurováno  
    CSP nástroje BitLocker: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)   

    - **Povolit** Nakonfigurujte minimální délku spouštěcího PIN kódu TPM.  
    - **Nenakonfigurováno** – uživatelé můžou nakonfigurovat spouštěcí PIN kód libovolné délky mezi 6 a 20 číslicemi.  

  Když nastavíte možnost *Povolit*, můžete nakonfigurovat následující nastavení:  

  - **Minimální znaky**  
    **Výchozí**: *nenakonfigurovaný* CSP nástroje BitLocker: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)  

    Zadejte počet znaků vyžadovaných spouštěcím PIN kódem ze **4**-**20**.  

- **Obnovení jednotky operačního systému**  
  **Výchozí**: Nenakonfigurováno   
  CSP nástroje BitLocker: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)  

  - **Povolit** – určuje, jak se mají obnovit jednotky operačního systému chráněné bitlockerem, když nejsou k dispozici požadované informace pro spuštění.  
  - **Nenakonfigurováno** – výchozí možnosti obnovení jsou podporovány pro obnovení nástroje BitLocker. Ve výchozím nastavení je povolený DRA, možnosti obnovení volí uživatel, včetně hesla pro obnovení a obnovovacího klíče, a informace o obnovení nejsou zálohovány služba AD DS.  

  Když nastavíte možnost *Povolit*, můžete nakonfigurovat následující nastavení:  

  - **Agent obnovení dat založený na certifikátech**  
    **Výchozí**: Nenakonfigurováno  
     
    - **Blok** – zabraňuje použití agenta obnovování dat s disky s operačním systémem chráněnými bitlockerem.  
    - **Nenakonfigurováno** – povolí použití agentů obnovení dat s jednotkami operačního systému chráněnými nástrojem BitLocker.  

  - **Vytváření hesla pro obnovení uživatelem**  
    **Výchozí**: Allow 48 – heslo pro obnovení číslic  

    Vyberte, jestli mají uživatelé povoleno, musí nebo nemá povoleno generovat heslo pro obnovení číslice 48.  
    - **Allow 48 – heslo pro obnovení číslic**  
    - **Nepovolit 48 heslo pro obnovení číslic**  
    - **Vyžadovat heslo pro obnovení číslic 48**  

  - **Vytvoření obnovovacího klíče uživatelem**  
    **Výchozí**: Allow 256-bit Recovery Key  

    Vyberte, jestli mají uživatelé povolené, povinné nebo Nepovolit generování 256 klíče pro obnovení.  
    - **Povolení 256 klíče pro obnovení**  
    - **Nepovolit 256 obnovovací klíč**  
    - **Vyžadovat 32bitový obnovovací klíč (256)**  

  - **Možnosti obnovení v Průvodci nastavením BitLockeru**  
    **Výchozí**: Nenakonfigurováno  

    - **Blokovat** – uživatelé nemůžou zobrazovat a měnit možnosti obnovení. Při nastavení na 
    - **Nenakonfigurováno** – uživatelé můžou při zapnutí BitLockeru zobrazit a změnit možnosti obnovení. 
 
  - **Uložit informace pro obnovení BitLockeru do Azure Active Directory**  
    **Výchozí**: Nenakonfigurováno  

    - **Povolit** – ukládat informace pro obnovení BitLockeru do Azure Active Directory (Azure AD).  
    - **Nenakonfigurováno** – informace pro obnovení nástroje BitLocker nejsou uloženy v AAD.  

  - **Informace o obnovení BitLockeru uložené do Azure Active Directory**  
    **Výchozí**: hesla pro obnovení zálohování a balíčky klíčů  

    Nakonfiguruje, které části informací pro obnovení BitLockeru se ukládají do služby Azure AD. Vybírejte z těchto možností:  
    - **Zálohovat hesla pro obnovení a sady klíčů**  
    - **Zálohovat jenom hesla pro obnovení**  

  - **Otočení hesla pro obnovení na základě klienta**  
    **Výchozí**: pro zařízení připojená k Azure AD je zapnuté střídání klíčů.  
    CSP nástroje BitLocker: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Toto nastavení inicializuje otočení hesla pro obnovení na základě klienta po obnovení jednotky operačního systému (buď pomocí programu Bootmgr nebo WinRE).  

    - Není nakonfigurováno  
    - Zakázané střídání klíčů  
    - Rotace klíčů povolená pro dedivizi připojenou ke službě Azure AD  
    - Zapnuté střídání klíčů pro Azure AD a zařízení připojená k hybridnímu připojení  

  - **Před povolením nástroje BitLocker ukládat informace pro obnovení do Azure Active Directory**  
    **Výchozí**: Nenakonfigurováno  
 
     Zabrání uživatelům povolit nástroj BitLocker, pokud počítač úspěšně nezálohoval informace pro obnovení BitLockeru na Azure Active Directory.  

    - **Vyžadovat** – zabrání uživatelům zapnout BitLocker, pokud se informace pro obnovení BitLockeru úspěšně neuloží v Azure AD.  
    - **Nenakonfigurováno** – uživatelé můžou zapnout BitLocker, i když se informace o obnovení úspěšně neuložily do Azure AD.  

- **Zpráva o obnovení před spuštěním a adresa URL**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)  

  - **Povolit** – nakonfigurujte zprávu a adresu URL, které se zobrazí na obrazovce pro obnovení klíče před spuštěním.  
  - **Nenakonfigurováno** – zakažte tuto funkci.  
  
  Když nastavíte možnost *Povolit*, můžete nakonfigurovat následující nastavení:  
  - **Zpráva o obnovení před spuštěním**  
    **Výchozí**: použít výchozí zprávu a adresu URL pro obnovení   
 
    Nakonfigurujte způsob zobrazení zprávy pro obnovení před spuštěním pro uživatele. Vybírejte z těchto možností:  
    - **Použít výchozí zprávu a adresu URL pro obnovení**  
    - **Použít prázdnou zprávu a adresu URL pro obnovení**  
    - **Použít vlastní zprávu o obnovení**  
    - **Použít vlastní adresu URL pro obnovení**  

### <a name="bitlocker-fixed-data-drive-settings"></a>Nastavení nástroje BitLocker pro pevné datové jednotky  

Tato nastavení platí konkrétně pro pevné datové jednotky.  

- **Přístup pro zápis na pevné datové jednotky, které nechrání BitLocker**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  

  - **Block** – udělte přístup jen pro čtení k datovým jednotkám, které nejsou chráněné bitlockerem.  
  - **Nenakonfigurováno** – ve výchozím nastavení se jedná o přístup pro čtení a zápis k datovým jednotkám, které nejsou šifrované.  

- **Obnovení pevného disku**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)  

  - **Povolit** – určuje, jak se obnovují pevné jednotky chráněné bitlockerem, když nejsou k dispozici požadované informace pro spuštění.  
  - **Nenakonfigurováno** – zakažte tuto funkci.  

  Když nastavíte možnost *Povolit*, můžete nakonfigurovat následující nastavení:  

  - **Agent obnovování dat**  
    **Výchozí**: Nenakonfigurováno  
 
    - **Blok** – zabraňuje použití agenta obnovování dat s pevnými jednotkami chráněnými nástrojem BitLocker. 
    - **Nenakonfigurováno** – povolí použití agentů obnovení dat s pevnými jednotkami chráněnými bitlockerem.  

  - **Vytváření hesla pro obnovení uživatelem**  
    **Výchozí**: Allow 48 – heslo pro obnovení číslic  

    Vyberte, jestli mají uživatelé povoleno, musí nebo nemá povoleno generovat heslo pro obnovení číslice 48.  
    - **Allow 48 – heslo pro obnovení číslic**  
    - **Nepovolit 48 heslo pro obnovení číslic**  
    - **Vyžadovat heslo pro obnovení číslic 48**  

  - **Vytvoření obnovovacího klíče uživatelem**  
    **Výchozí**: Allow 256-bit Recovery Key

    Vyberte, jestli mají uživatelé povolené, povinné nebo Nepovolit generování 256 klíče pro obnovení.
    - **Povolení 256 klíče pro obnovení**  
    - **Nepovolit 256 obnovovací klíč**  
    - **Vyžadovat 32bitový obnovovací klíč (256)**  

  - **Možnosti obnovení v Průvodci nastavením BitLockeru**  
    **Výchozí**: Nenakonfigurováno  

    - **Blokovat** – uživatelé nemůžou zobrazovat a měnit možnosti obnovení. Při nastavení na 
    - **Nenakonfigurováno** – uživatelé můžou při zapnutí BitLockeru zobrazit a změnit možnosti obnovení.
 
  - **Uložit informace pro obnovení BitLockeru do Azure Active Directory**  
    **Výchozí**: Nenakonfigurováno  

    - **Povolit** – ukládat informace pro obnovení BitLockeru do Azure Active Directory (Azure AD).  
    - **Nenakonfigurováno** – informace pro obnovení nástroje BitLocker nejsou uloženy v AAD.

  - **Informace o obnovení BitLockeru uložené do Azure Active Directory**  
    **Výchozí**: hesla pro obnovení zálohování a balíčky klíčů  

    Nakonfiguruje, které části informací pro obnovení BitLockeru se ukládají do služby Azure AD. Vybírejte z těchto možností:  
    - **Zálohovat hesla pro obnovení a sady klíčů**  
    - **Zálohovat jenom hesla pro obnovení**  

  - **Otočení hesla pro obnovení na základě klienta**  
    **Výchozí**: pro zařízení připojená k Azure AD je zapnuté střídání klíčů.  
    CSP nástroje BitLocker: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Toto nastavení inicializuje otočení hesla pro obnovení na základě klienta po obnovení jednotky operačního systému (buď pomocí programu Bootmgr nebo WinRE).  

    - Není nakonfigurováno  
    - Zakázané střídání klíčů  
    - Rotace klíčů povolená pro dedivizi připojenou ke službě Azure AD  
    - Zapnuté střídání klíčů pro Azure AD a zařízení připojená k hybridnímu připojení  

  - **Před povolením nástroje BitLocker ukládat informace pro obnovení do Azure Active Directory**  
    **Výchozí**: Nenakonfigurováno  
 
    Zabrání uživatelům povolit nástroj BitLocker, pokud počítač úspěšně nezálohoval informace pro obnovení BitLockeru na Azure Active Directory.  

    - **Vyžadovat** – zabrání uživatelům zapnout BitLocker, pokud se informace pro obnovení BitLockeru úspěšně neuloží v Azure AD.  
    - **Nenakonfigurováno** – uživatelé můžou zapnout BitLocker, i když se informace o obnovení úspěšně neuložily do Azure AD.  

### <a name="bitlocker-removable-data-drive-settings"></a>Nastavení nástroje BitLocker pro vyměnitelné datové jednotky  

Tato nastavení platí konkrétně pro vyměnitelné datové jednotky.  

- **Přístup pro zápis na vyměnitelné datové jednotky, které nechrání BitLocker**  
  **Výchozí**: Nenakonfigurováno  
  CSP nástroje BitLocker: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  

  - **Block** – udělte přístup jen pro čtení k datovým jednotkám, které nejsou chráněné bitlockerem.  
  - **Nenakonfigurováno** – ve výchozím nastavení se jedná o přístup pro čtení a zápis k datovým jednotkám, které nejsou šifrované.  

  Když nastavíte možnost *Povolit*, můžete nakonfigurovat následující nastavení:  

  - **Přístup pro zápis do zařízení nakonfigurovaných v jiné organizaci**  
    **Výchozí**: Nenakonfigurováno  

    - **Blok** – zablokuje přístup k zápisu do zařízení nakonfigurovaných v jiné organizaci.  
    - **Nenakonfigurováno** – zamítnout přístup pro zápis.  
 
## <a name="microsoft-defender-exploit-guard"></a>Ochrana před zneužitím programu Microsoft Defender  

Pomocí [ochrany před zneužitím](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/exploit-protection) můžete spravovat a snižovat plochu útoků aplikací používaných vašimi zaměstnanci.  

### <a name="attack-surface-reduction"></a>Omezení možností útoku  

Pravidla pro omezení možností útoku zabraňují malwaru chování často používá k nainfikování počítačů se škodlivým kódem.  

#### <a name="attack-surface-reduction-rules"></a>Pravidla pro omezení možností útoku  

- **Označit zcizování přihlašovacích údajů ze subsystému místního úřadu zabezpečení Windows**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokovat odcizení přihlašovacích údajů ze subsystému místního úřadu zabezpečení systému Windows (Lsass. exe)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-credential-stealing-from-the-windows-local-security-authority-subsystem)

  Ochrana před akcemi a aplikacemi, které se obvykle používají k navýšení malwaru pro napadení malwarem.  

  - **Nenakonfigurované**  
  - **Povolit** – příznak pro krádeže přihlašovacích údajů ze subsystému místního úřadu zabezpečení systému Windows (Lsass. exe).  
  - **Jenom audit**  

- **Vytváření procesů z aplikace Adobe Reader (beta verze)**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [zablokuje Adobe Reader z vytváření podřízených procesů](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-adobe-reader-from-creating-child-processes) .  

  - **Nenakonfigurované**  
  - **Enable** – zablokuje podřízené procesy vytvořené z aplikace Adobe Reader.  
  - **Jenom audit**  

#### <a name="rules-to-prevent-office-macro-threats"></a>Pravidla pro ochranu před hrozbami od maker Office  

Aplikacím Office zablokujte provádění následujících akcí:  

- **Injektáž aplikací Office do jiných procesů (bez výjimek)**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokovat aplikacím Office vkládání kódu do jiných procesů](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-injecting-code-into-other-processes)  

  - **Nenakonfigurované**  
  - **Blok** – zablokuje aplikacím Office vkládání do jiných procesů.  
  - **Jenom audit**  

- **Aplikace a makra Office vytvářející spustitelný obsah**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokovat aplikacím Office vytváření spustitelného obsahu](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-creating-executable-content)  

  - **Nenakonfigurované**  
  - **Blok** – zablokuje aplikacím Office a makrům vytváření spustitelného obsahu.  
  - **Jenom audit**  

- **Aplikace Office spouštějící podřízené procesy**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokovat všechny aplikace Office z vytváření podřízených procesů](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-all-office-applications-from-creating-child-processes)  

  - **Nenakonfigurované**  
  - **Blok** – zablokuje aplikacím Office spouštění podřízených procesů.  
  - **Jenom audit**  
  
- **Importy Win32 z kódu maker v Office**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokování volání Win32 API v makrech Office](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-win32-api-calls-from-office-macros)  

  - **Nenakonfigurované**  
  - **Blok** – zablokuje importy Win32 z kódu makra v Office.  
  - **Jenom audit**  
  
- **Vytváření procesů z komunikačních produktů Office**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [Blokovat aplikaci Office Communications z vytváření podřízených procesů](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-communication-application-from-creating-child-processes)  

  - **Nenakonfigurované**  
  - **Enable** – zablokuje vytváření podřízeného procesu z aplikací Office Communications.  
  - **Jenom audit**  

#### <a name="rules-to-prevent-script-threats"></a>Pravidla pro ochranu před hrozbami od skriptů  

Z důvodu ochrany před hrozbami od skriptů zablokujte tyto akce:  

- **Obfuskovaný kód js, vbs, ps nebo makra**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [zablokuje spuštění potenciálně zablokovaných skriptů](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-execution-of-potentially-obfuscated-scripts) .    

  - **Nenakonfigurované**  
  - **Blok** – zablokuje všechny zakódovaná kód JS, VBS, PS nebo makra.  
  - **Jenom audit**  

- **Skripty js a vbs spouštějící datovou část staženou z internetu (bez výjimek)**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [zablokovat jazyk JavaScript nebo VBScript pro spuštění staženého spustitelného obsahu](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-javascript-or-vbscript-from-launching-downloaded-executable-content)  

  - **Nenakonfigurované**  
  - **Blok** -Block js/vbs ze spouštění datové části stažené z Internetu  
  - **Jenom audit**  

- **Vytváření procesů z příkazů PSExec a WMI**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokování vytváření procesů, které pocházejí z příkazů PsExec a WMI](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-process-creations-originating-from-psexec-and-wmi-commands)  

  - **Nenakonfigurované**  
  - **Blokové** vytváření procesů, které pocházejí z příkazů PsExec a WMI.  
  
  - **Jenom audit**  

- **Nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokuje nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-untrusted-and-unsigned-processes-that-run-from-usb) .    

  - **Nenakonfigurované**  
  - **Blokuje** nedůvěryhodné a nepodepsané procesy, které se SPOUŠTĚJÍ z USB.  
  - **Jenom audit**  
  
- **Spustitelné soubory, které nesplňují kritéria prevalence, stáří nebo seznamu důvěryhodných souborů**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [zablokovat spouštění spustitelných souborů, pokud nesplňují kritéria prevalence, stáří nebo seznamu důvěryhodných](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion)    

  - **Nenakonfigurované**  
  - **Blok** – zablokuje spouštění spustitelných souborů, pokud nesplňují kritéria prevalence, stáří nebo seznamu důvěryhodných souborů.  
  - **Jenom audit**  

#### <a name="rules-to-prevent-email-threats"></a>Pravidla pro ochranu před e-mailovými hrozbami  

Z důvodu ochrany před e-mailovými hrozbami zablokujte tuto akci:  

- **Spuštění spustitelného obsahu (exe, dll, ps, js, vbs atd.) doručeného v e-mailu (webová pošta/poštovní klient) (bez výjimek)**  
  **Výchozí**: Nenakonfigurováno  
  Pravidlo: [blokovat spustitelný obsah z e-mailového klienta a webové pošty](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-content-from-email-client-and-webmail)  

  - **Nenakonfigurované**  
  - **Blok** -blokovat spuštění spustitelného obsahu (exe, DLL, PS, js, VBS atd.) vyřazeného z e-mailu (webová pošta/pošta – klient).  
  - **Jenom audit**  

#### <a name="rules-to-protect-against-ransomware"></a>Pravidla, která chrání před ransomwarem  

- **Rozšířená ochrana před ransomwarem**  
  Výchozí: Nenakonfigurováno  
  Pravidlo: [použití rozšířené ochrany proti ransomwarem](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#use-advanced-protection-against-ransomware)  

  - **Nenakonfigurované**  
  - **Povolit** – používejte agresivní ransomwarem ochranu.  
  - **Jenom audit**  

#### <a name="attack-surface-reduction-exceptions"></a>Výjimky pro omezení možností útoku

- **Soubory a složky, které se mají vyloučit z pravidel pro omezení možností útoku**  
  CSP pro Defender: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)  

  - **Importujte** soubor. csv, který obsahuje soubory a složky, které se mají vyloučit z pravidel pro omezení možností útoku.  
  - **Přidejte** místní soubory nebo složky ručně.  

> [!IMPORTANT]  
> Aby bylo možné správně nainstalovat a spustit aplikace pro obchodní prostředí Win32, nastavení antimalwarového programu by mělo vyloučit následující adresáře, aby byly prohledávány:  
> **Na klientských počítačích x64**:  
> *C:\Program Files (x86) \Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>  
> **Na klientských počítačích x86**:  
> *C:\Program Files\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>
> Další informace najdete v tématu [doporučení pro kontrolu virů pro podnikové počítače, na kterých běží aktuálně podporované verze Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).


### <a name="controlled-folder-access"></a>Řízený přístup ke složkám  

[Chraňte cenná data](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/controlled-folders) před škodlivými aplikacemi a hrozbami, jako je například ransomwarem.  

- **Ochrana složky**  
  **Výchozí**: Nenakonfigurováno  
  CSP pro Defender: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)  

  Umožňuje chránit soubory a složky před neautorizovanými změnami od neznámých aplikací.  

  - **Nenakonfigurované**  
  - **Povolení**  
  - **Jenom audit**  
  - **Zablokovat úpravu disku**  
  - **Auditovat úpravu disku**  

  Když vyberete jinou konfiguraci než *nenakonfigurovanou*, můžete nakonfigurovat:  
  - **Seznam aplikací, které mají přístup k chráněným složkám**  
    CSP pro Defender: [ControlledFolderAccessAllowedApplications](https://go.microsoft.com/fwlink/?linkid=872616)  

    - **Importujte** soubor. csv, který obsahuje seznam aplikací.  
    - Do tohoto seznamu **přidejte** aplikace ručně.  

  - **Seznam dalších složek, které je třeba chránit**  
    CSP pro Defender: [ControlledFolderAccessProtectedFolders](https://go.microsoft.com/fwlink/?linkid=872617)  

    - **Importujte** soubor. csv, který obsahuje seznam složek.  
    - Do tohoto seznamu **přidejte** složky ručně.  

### <a name="network-filtering"></a>Filtrování sítě  

Blokuje odchozí připojení z libovolné aplikace na IP adresy nebo domény s nízkými Reputacemi. Filtrování sítě je podporováno v režimu auditu i blokování.  

- **Ochrana sítě**  
  **Výchozí**: Nenakonfigurováno  
  CSP pro Defender: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)  

  Záměrem tohoto nastavení je chránit koncové uživatele před aplikacemi s přístupem k podvodným podvodům, webům pro zneužití a škodlivým obsahem na internetu. Zabraňuje také prohlížečům třetích stran v připojení k nebezpečným webům.  

  - **Nenakonfigurováno** – zakažte tuto funkci. Uživatelům a aplikacím není zablokováno připojení k nebezpečným doménám. Správci nevidí tuto aktivitu v programu Microsoft Defender Security Center.  
  - **Povolit** – zapnout ochranu sítě a zablokovat uživatelům a aplikacím připojení k nebezpečným doménám. Správci mohou tuto aktivitu zobrazit v programu Microsoft Defender Security Center.  
  - **Jenom audit**: – uživatelé a aplikace nejsou zablokovaným připojením k nebezpečným doménám. Správci mohou tuto aktivitu zobrazit v programu Microsoft Defender Security Center.  

### <a name="exploit-protection"></a>Ochrana Exploit Protection  

- **Nahrát XML**  
  **Výchozí**: *Nenakonfigurováno*  

  Pokud chcete ochranu [zařízení před zneužitím chránit](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)pomocí ochrany před zneužitím, vytvořte soubor XML, který bude obsahovat nastavení pro omezení rizik systému a aplikací. Existují dvě metody vytvoření souboru XML:  

  - *PowerShell* – použijte jednu nebo více rutin PowerShellu *Get-ProcessMitigation*, *set-ProcessMitigation*a *ConvertTo-powershellových processmitigationpolicy* . Tyto rutiny nakonfigurují nastavení zmírňování a exportují jejich reprezentaci v jazyce XML.  

  - *Microsoft defender Security Center uživatelské rozhraní* : v Security Center Microsoft Defenderu klikněte na aplikace & řízení prohlížeče a potom se posuňte k dolnímu okraji výsledné obrazovky a najděte ochranu před zneužitím. Nejprve nakonfigurujte nastavení zmírňování na kartách Nastavení systému a Nastavení programů. Pak ve spodní části obrazovky najděte odkaz Exportovat nastavení a exportujte reprezentaci daného nastavení v jazyce XML.  

- **Uživatel upravující rozhraní ochrany před zneužitím**  
  **Výchozí**: Nenakonfigurováno  
  ExploitGuard CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=872887)  


  - **Blokovat** – nahrání souboru XML, který umožňuje konfiguraci omezení paměti, toku řízení a zásad. Nastavení v souboru XML se dají použít k ochraně aplikace před zneužitím.  
  - **Nenakonfigurováno** – nepoužívá se žádná vlastní konfigurace.  

## <a name="microsoft-defender-application-control"></a>Řízení aplikací v programu Microsoft Defender  

Vyberte další aplikace, které musí být buď auditovány, nebo mohou být důvěryhodné pro spuštění pomocí řízení aplikací v programu Microsoft Defender. Součásti systému Windows a všechny aplikace z obchodu Windows Store se za důvěryhodné považují automaticky.  


- **Zásady integrity kódu pro řízení aplikací**  
  **Výchozí**: Nenakonfigurováno  
   CSP: [CSP pro AppLocker](https://go.microsoft.com/fwlink/?linkid=874543)  

  - **Vynutilo** – vyberte zásady integrity kódu pro řízení aplikací pro vaše uživatelská zařízení.  
  
    Po povolení na zařízení je možné řízení aplikací zakázat jenom změnou režimu z *vyhovět* na *jenom audit*. Změna režimu z *Vynutit* na *Nenakonfigurováno* způsobí, že řízení aplikací se na přiřazených zařízeních bude dále vynucovat.  

  - **Nenakonfigurováno** – řízení aplikací není přidáno do zařízení. Nastavení, která byla dříve přidána, se však budou na přiřazených zařízeních nadále vymáhat. 
 
  - **Jenom audit** – aplikace nejsou blokované. Všechny události se zaznamenávají do protokolů místního klienta.  

## <a name="microsoft-defender-credential-guard"></a>Ochrana Credential Guard v programu Microsoft Defender  

Ochrana Credential Guard v programu Microsoft Defender chrání před útoky krádeže přihlašovacích údajů. Izoluje tajné kódy, aby k nim měl přístup jenom privilegovaný software systému.  

- **Credential Guard**  
  **Výchozí**: zakázat  
  [DeviceGuard CSP](https://go.microsoft.com/fwlink/?linkid=872424)  

  - **Disable** – vypněte ochranu Credential Guard vzdáleně, pokud byla dříve zapnutá s možností **Povolit bez zámku UEFI** .  

  - **Povolit s rozhraním UEFI Lock** – ochranu přihlašovacích údajů nelze vzdáleně zakázat pomocí klíče registru nebo zásad skupiny.  

    > [!NOTE]
    > Pokud toto nastavení použijete a chcete ochranu Credential Guard později zakázat, musíte nastavit zásady skupiny na **Zakázáno**. Musíte také fyzicky vymazat informace o konfiguraci UEFI z jednotlivých počítačů. Dokud je uložená konfigurace UEFI, je povolená i ochrana přihlašovacích údajů Credential Guard.  

  - **Povolit bez zámku UEFI** – umožní vzdálené vypnutí ochrany přihlašovacích údajů pomocí Zásady skupiny. Na zařízeních s tímto nastavením musí běžet Windows 10 verze 1511 a novější.  

  Pokud *povolíte* ochranu Credential Guard, jsou povolené taky tyto povinné funkce:  
  
  - **Zabezpečení založené na virtualizaci** (VBS)  
    Zapne při příštím restartování. Zabezpečení na základě virtualizace nabízí podporu služeb zabezpečení pomocí hypervisoru Windows.  
  - **Zabezpečené spouštění s přístupem ke službě Directory Memory**  
    Zapne VBS s zabezpečeným spouštěním a chráněným přímým přístupem do paměti (DMA). Ochrany DMA vyžadují hardwarovou podporu a povolí se jenom na správně nakonfigurovaných zařízeních.  

## <a name="microsoft-defender-security-center"></a>Security Center programu Microsoft Defender  

Microsoft Defender Security Center v každé z jednotlivých funkcí funguje jako samostatná aplikace nebo proces. Zobrazuje oznámení prostřednictvím Centra akcí. Slouží jako kolekce nebo jedno místo pro zobrazení stavu a spuštění některé konfigurace pro každou z těchto funkcí. Další informace najdete v dokumentaci k [Microsoft Defenderu](https://docs.microsoft.com/windows/threat-protection/windows-defender-security-center/windows-defender-security-center) .  

### <a name="microsoft-defender-security-center-app-and-notifications"></a>Aplikace a oznámení v programu Microsoft Defender Security Center  

Zablokujte přístup koncových uživatelů k různým oblastem aplikace Security Center v programu Microsoft Defender. Když se skryje nějaká část, zablokují se i související oznámení.  

- **Ochrana před viry a hrozbami**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)  

  Nakonfigurujte, jestli koncoví uživatelé můžou zobrazit oblast ochrany před viry a hrozbami v Security Center programu Microsoft Defender. Skrytím této části se taky zablokuje všechna oznámení týkající se ochrany před viry a hrozbami.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Ochrana ransomwarem**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)  

  Nakonfigurujte, jestli koncoví uživatelé můžou zobrazit oblast ransomwarem Protection v programu Microsoft Defender Security Center. Skrytím této části se taky zablokuje všechna oznámení týkající se ransomwarem Protection.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Ochrana účtu**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)  

  Nakonfigurujte, jestli koncoví uživatelé můžou zobrazit oblast ochrany účtu v Security Center programu Microsoft Defender. Skrytím této části se taky zablokuje všechna oznámení týkající se ochrany účtů.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Firewall a ochrana sítě**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)  

  Nakonfigurujte, jestli koncoví uživatelé můžou zobrazit oblast brána firewall a ochrana sítě v centru zabezpečení v programu Microsoft Defender. Skrytím této části dojde také k blokování všech oznámení souvisejících s bránou firewall a ochranou sítě.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Řízení aplikací a prohlížečů**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)  

  Nakonfigurujte, jestli koncoví uživatelé můžou v centru zabezpečení v programu Microsoft Defender zobrazit oblast ovládacího prvku aplikace a prohlížeče. Skrytím této části dojde také k blokování všech oznámení souvisejících s ovládacím prvkem aplikace a prohlížeče.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Hardwarová ochrana**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)  

  Nakonfigurujte, jestli koncoví uživatelé mohou zobrazit oblast hardwarového zabezpečení v Security Center programu Microsoft Defender. Skrytím této části dojde také k blokování všech oznámení týkajících se hardwarové ochrany.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Výkon a stav zařízení**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)  

  Nakonfigurujte, jestli koncoví uživatelé můžou zobrazit oblast výkon a stav zařízení v centru zabezpečení v programu Microsoft Defender. Skrytím této části dojde také k blokování všech oznámení týkajících se výkonu a stavu zařízení.  
  
  - **Nenakonfigurované**  
  - **Skryl**  

- **Možnosti pro rodinu**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)  

  Nakonfigurujte, jestli koncoví uživatelé mohou zobrazit oblast možností rodiny v centru zabezpečení v programu Microsoft Defender. Skrytím této části budou také zablokována všechna oznámení týkající se rodinných možností.  
  
  - **Nenakonfigurované**  
  - **Skryl**  

- **Oznámení ze zobrazených oblastí aplikace**  
  **Výchozí**: Nenakonfigurováno  
  WindowsDefenderSecurityCenter CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)  

  Vyberte, která oznámení se mají zobrazit koncovým uživatelům. Nekritická oznámení zahrnují Shrnutí aktivity antivirové ochrany v programu Microsoft Defender, včetně oznámení po dokončení kontroly. Všechna další oznámení se považují za závažná.  

  - **Nenakonfigurované**  
  - **Blokovat Nekritická oznámení**  
  - **Blokovat všechna oznámení**  

- **Ikona Security Center systému Windows na hlavním panelu systému**  
  **Výchozí**: Nenakonfigurováno  

  Nakonfigurujte zobrazení ovládacího prvku oznamovací oblasti. Aby se toto nastavení projevilo, musí se uživatel odhlásit a přihlásit nebo restartovat počítač.  
  
  - **Nenakonfigurované**  
  - **Skryl**  

- **Tlačítko vymazat čip TPM**  
  **Výchozí**: Nenakonfigurováno  

  Nakonfigurujte zobrazení tlačítka vymazat čip TPM.  
  
  - **Nenakonfigurované**  
  - **Zakázat**  

- **Upozornění na aktualizaci firmwaru TPM**  
  **Výchozí**: Nenakonfigurováno  
  
  Konfigurace zobrazení firmwaru čipu TPM při zjištění ohroženého firmwaru.  

  - **Nenakonfigurované**  
  - **Skryl**  

- **Ochrana před zneužitím**  
  **Výchozí**: Nenakonfigurováno

  Zapněte nebo vypněte ochranu proti falšování na zařízeních. Pokud chcete používat ochranu před zneužitím, je potřeba [integrovat rozšířenou ochranu před internetovými útoky v programu Microsoft Defender s Intune](advanced-threat-protection.md)a mít [licence Enterprise mobility + Security E5](../fundamentals/licenses.md).  
  - **Nenakonfigurováno** – není provedena žádná změna v nastavení zařízení.
  - **Povoleno** – ochrana proti falšování je zapnutá a na zařízeních se vynutila omezení.
  - **Zakázáno** – ochrana proti falšování je vypnuta a omezení nejsou vynutila.

### <a name="it-contact-information"></a>Informace o kontaktu IT  

Poskytněte kontaktní informace, které se zobrazí v aplikaci Security Center Microsoft Defenderu a v oznámeních aplikací.  

Můžete zvolit možnost **Zobrazovat v aplikacích a v oznámeních**, **Zobrazovat jen v aplikaci**, **Zobrazovat jen v oznámeních** nebo **Nezobrazovat**. Zadejte **Název organizace IT** a aspoň jednu z následujících možností kontaktu:  


- **Kontaktní údaje IT**  
  **Výchozí**: Nezobrazovat  
  WindowsDefenderSecurityCenter CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)  
  
  Nakonfigurujte, kde se mají koncovým uživatelům zobrazovat kontaktní informace pro IT oddělení.  
  
  - **Zobrazit v aplikaci a v oznámeních**  
  - **Zobrazit jenom v aplikaci**  
  - **Zobrazit jenom v oznámeních**  
  - **Nezobrazovat**  

  Pokud je nakonfigurováno pro zobrazení, můžete nakonfigurovat následující nastavení:  

  - **Název organizace IT**  
    **Výchozí**: *Nenakonfigurováno*  
    WindowsDefenderSecurityCenter CSP: [CompanyName](https://go.microsoft.com/fwlink/?linkid=873677)  

  - **Telefonní číslo nebo skypové jméno oddělení IT**  
    **Výchozí**: *Nenakonfigurováno*  
    WindowsDefenderSecurityCenter CSP: [telefon](https://go.microsoft.com/fwlink/?linkid=873678) 

  - **E-mailová adresa IT oddělení**  
    **Výchozí**: *Nenakonfigurováno*  
    WindowsDefenderSecurityCenter CSP: [e-mail](https://go.microsoft.com/fwlink/?linkid=873679)  

  - **Adresa URL webu podpory IT**  
    **Výchozí**: *Nenakonfigurováno*  
    WindowsDefenderSecurityCenter CSP: [URL](https://go.microsoft.com/fwlink/?linkid=873680)  
 
## <a name="local-device-security-options"></a>Možnosti místního zabezpečení zařízení  

Pomocí těchto možností můžete konfigurovat nastavení místního zabezpečení na zařízeních s Windows 10.  

### <a name="accounts"></a>Účty  

- **Přidat nové účty Microsoft**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [Accounts_BlockMicrosoftAccounts](https://go.microsoft.com/fwlink/?linkid=867916)  


  - **Blok** Zabránit uživatelům v přidávání nových účtů Microsoft do zařízení.  
  - **Nenakonfigurováno** – uživatelé můžou na zařízení používat účty Microsoft.  

- **Vzdálené přihlášení bez hesla**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867890)  


   - **Blok** – povolí pouze místní účty s prázdnými hesly pro přihlášení pomocí klávesnice zařízení.  
   - **Nenakonfigurováno** – umožňuje místním účtům s prázdnými hesly přihlašovat se z jiných umístění, než je fyzické zařízení.  

#### <a name="admin"></a>Správce  

- **Účet místního správce**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867850)  


  - **Blok** Zabraňte použití místního účtu správce.  
  - **Nenakonfigurované**  

- **Přejmenovat účet správce**  
  **Výchozí**: *Nenakonfigurováno*  
  LocalPoliciesSecurityOptions CSP: [Accounts_RenameAdministratorAccount](https://go.microsoft.com/fwlink/?linkid=867917)  
 

  Definujte jiný název účtu, který se má přidružit k identifikátoru zabezpečení (SID) pro účet Administrator.  

 #### <a name="guest"></a>Guest  

- **Účet Guest**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [LocalPoliciesSecurityOptions](https://go.microsoft.com/fwlink/?linkid=867853)  

  - **Blok** – zabraňuje použití účtu Guest.  
  - **Nenakonfigurované**  

- **Přejmenovat účet hosta**  
  **Výchozí**: *Nenakonfigurováno*  
  LocalPoliciesSecurityOptions CSP: [Accounts_RenameGuestAccount](https://go.microsoft.com/fwlink/?linkid=867918)  
  
  Definujte jiný název účtu, který se má přidružit k identifikátoru zabezpečení (SID) pro účet Guest.  

### <a name="devices"></a>Zařízení  

- **Uvolnit zařízení bez přihlášení**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [Devices_AllowUndockWithoutHavingToLogon](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-devices-allowundockwithouthavingtologon)  

  
  - **Blok** – uživatelé můžou k bezpečnému odložení zařízení stisknout tlačítko fyzického vysunutí přenosného zařízení.  
  - **Nenakonfigurováno** – uživatel se musí přihlásit k zařízení a získat oprávnění k odložení zařízení.  

- **Nainstalovat ovladače tiskáren pro sdílené tiskárny**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [Devices_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters](https://go.microsoft.com/fwlink/?linkid=867921)  


  - **Povoleno** – libovolný uživatel může nainstalovat ovladač tiskárny jako součást připojení ke sdílené tiskárně.  
  - **Nenakonfigurovaní** – ovladač tiskárny může nainstalovat jenom správce, který je součástí připojení ke sdílené tiskárně.  

- **Omezit přístup k jednotce CD-ROM na místního aktivního uživatele**  
  **Výchozí**: Nenakonfigurováno  
  CSP: [Devices_RestrictCDROMAccessToLocallyLoggedOnUserOnly](https://go.microsoft.com/fwlink/?linkid=867922)  


  - **Povoleno** – jenom interaktivně přihlášený uživatel může používat médium CD-ROM. Pokud je tato zásada povolená a nikdo není interaktivně přihlášený, je možné získat k jednotce CD-ROM přístup přes síť.  
  - **Nenakonfigurováno** – kdokoli má přístup k jednotce CD-ROM.  

- **Formátování a vysunutí vyměnitelného média**  
  **Výchozí**: Správci  
  CSP: [Devices_AllowedToFormatAndEjectRemovableMedia](https://go.microsoft.com/fwlink/?linkid=867920)  
 

  Definujte, kdo má povolené formátování a vysunutí vyměnitelných médií NTFS:  
  - **Nenakonfigurované**  
  - **Správci**  
  - **Správci a členové skupiny Power Users**  
  - **Správci a interaktivní uživatelé**  

### <a name="interactive-logon"></a>Interaktivní přihlášení  

- **Počet minut nečinnosti uzamčené obrazovky, než se aktivuje spořič obrazovky**  
  **Výchozí**: *Nenakonfigurováno*  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=867891)  


  Zadejte maximální počet minut nečinnosti na přihlašovací obrazovce interaktivní plochy, dokud se nespustí spořič obrazovky. (**0** - **99999**)  

- **Pro přihlášení vyžadovat kombinaci kláves CTRL + ALT + DEL**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DoNotRequireCTRLALTDEL](https://go.microsoft.com/fwlink/?linkid=867951)  


  - **Povolit** – stisknutím kombinace kláves CTRL + ALT + DEL se uživatelé nebudou muset přihlašovat.  
  - **Není nakonfigurováno** Před přihlášením k systému Windows vyžadovat, aby uživatelé stiskli kombinaci kláves CTRL + ALT + DEL.  

- **Chování při odebrání čipové karty**  
  **Výchozí**: zamknout pracovní stanici   
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=868437)  
    
  Určuje, co se stane, když se čipová karta přihlášeného uživatele odebere z čtecího zařízení s čipovou kartou. Možnosti:  

  - **Zamknout pracovní stanici** – pracovní stanice je při odebrání čipové karty uzamčená. Tato možnost umožňuje uživatelům opustit danou oblast, vzít si svoji čipovou kartu s sebou a přesto udržovat chráněnou relaci.  
  - **Žádná akce**  
  - **Vynutit odhlášení** – při odebrání čipové karty se uživatel automaticky odhlásí.  
  - **Odpojit, pokud relace vzdálené plochy** – odebrání čipové karty odpojí relaci bez odhlášení uživatele. Tato možnost umožňuje uživateli později vložením čipové karty obnovit danou relaci na tomto počítači nebo na jiném počítači se čtečkou čipových karet, aniž by se musel znovu přihlašovat. Pokud je relace místní, funguje tato zásada stejně jako možnost Zamknout pracovní stanici.  

#### <a name="display"></a>Zobrazit  

- **Informace o uživateli na zamykací obrazovce**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DisplayUserInformationWhenTheSessionIsLocked](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-displayuserinformationwhenthesessionislocked)  

  Nakonfigurujte informace o uživateli, které se zobrazí, když je relace uzamčena. Pokud tato možnost není nakonfigurovaná, zobrazí se zobrazované jméno uživatele, doména a uživatelské jméno.  

  - **Nenakonfigurované**  
  - **Zobrazované jméno uživatele, doména a uživatelské jméno**  
  - **Jen zobrazované jméno uživatel**  
  - **Nezobrazovat informace o uživateli**  

- **Skrýt posledního přihlášeného uživatele**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DoNotDisplayLastSignedIn](https://go.microsoft.com/fwlink/?linkid=868437)  
  
  
  - **Povolit** – skryje uživatelské jméno.  
  - **Nenakonfigurováno** – zobrazí poslední uživatelské jméno.  

- **Skrýt uživatelské jméno při přihlašování**
  **výchozí**: není nakonfigurované  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_DoNotDisplayUsernameAtSignIn](https://go.microsoft.com/fwlink/?linkid=867959)  

  
  - **Povolit** – skryje uživatelské jméno.  
  - **Nenakonfigurováno** – zobrazí poslední uživatelské jméno.  

- **Název přihlašovací zprávy**  
  **Výchozí**: *Nenakonfigurováno*  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_MessageTitleForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867964)  

  Nastavte název zprávy pro uživatele, kteří se přihlásí.  

- **Text zprávy pro přihlášení**  
  **Výchozí**: *Nenakonfigurováno*  
  LocalPoliciesSecurityOptions CSP: [InteractiveLogon_MessageTextForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867962)  

  Nastavte text zprávy pro přihlášení uživatelů.  
  
### <a name="network-access-and-security"></a>Přístup k síti a zabezpečení

- **Anonymní přístup k pojmenovaným kanálům a sdíleným složkám**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=868432)  

  - **Nenakonfigurováno** – zakáže anonymní přístup ke sdílení a nastavení pojmenovaného kanálu. Platí pro nastavení, ke kterým se dá přistupovat anonymně.  
  - **Blokování** – zakáže tuto zásadu a zpřístupní se anonymní přístup.  

- **Anonymní výčet účtů SAM**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=868434)  
  
  - **Nenakonfigurováno** – anonymní uživatelé mohou vytvořit výčet účtů SAM.  
  - **Blok** – zabraňuje anonymnímu výčtu účtů SAM.  

- **Anonymní výčet účtů SAM a sdílených složek**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=868435)  

  - **Nenakonfigurováno** – anonymní uživatelé mohou vytvořit výčet názvů doménových účtů a síťových sdílených složek.  
  - **Blok** – zabraňuje anonymnímu výčtu účtů SAM a sdílených složek. 

- **Hodnota hash správce sítě LAN uložená při změně hesla**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=868431)  
   
  Určete, jestli se při příštím změně hesla uloží hodnota hash pro hesla. 
  - **Nenakonfigurováno** – hodnota hash není uložena.  
  - **Blokovat** – správce LAN (LM) ukládá hodnotu hash nového hesla.  

- **Žádosti o ověření PKU2U**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_AllowPKU2UAuthenticationRequests](https://go.microsoft.com/fwlink/?linkid=867892)  

  - **Nenakonfigurováno**– povoluje PU2U požadavky.  
  - **Blok** – zablokuje žádosti o ověření PKU2U na zařízení.  

- **Omezit vzdálená připojení RPC k SAM**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=867893)  
  
  - **Nenakonfigurováno** – použijte výchozí popisovač zabezpečení, který umožňuje uživatelům a skupinám vzdálené volání RPC do Sam.
  - **Povolit** – odepřít uživatelům a skupinám v poskytování vzdálených volání RPC do Správce zabezpečení účtů (SAM), který ukládá uživatelské účty a hesla. Možnost **Povolit** také umožňuje změnit výchozí řetězec jazyka SDDL (Security Descriptor Definition Language) tak, aby explicitně povoloval nebo odepřel uživatelům a skupinám, aby tato vzdálená volání mohla provádět.  

    - **Popisovač zabezpečení**  
      **Výchozí**: *Nenakonfigurováno*  
    
- **Minimální zabezpečení relace pro klienty založené na NTLM SSP**  
  **Výchozí**: žádné  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)  
  
  Toto nastavení zabezpečení umožňuje serveru vyžadovat vyjednávání 128ho šifrování nebo zabezpečení relace NTLMv2.  

  - **Žádné**  
  - **Vyžadovat zabezpečení relace NTLMv2**  
  - **Vyžadovat 64bitové šifrování 128**  
  - **Šifrování NTLMv2 a 128 bitů**  
 
- **Minimální zabezpečení relace pro server založený na NTLM SSP**  
  **Výchozí**: žádné  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)  

  Toto nastavení zabezpečení určuje, který ověřovací protokol pro ověření výzvou a odpovědí se používá pro přihlášení k síti.  

  - **Žádné**  
  - **Vyžadovat zabezpečení relace NTLMv2**  
  - **Vyžadovat 64bitové šifrování 128**  
  - **Šifrování NTLMv2 a 128 bitů**  

- **Úroveň ověřování nástroje LAN Manager**  
  **Výchozí**: LM a NTLM  
  LocalPoliciesSecurityOptions CSP: [NetworkSecurity_LANManagerAuthenticationLevel](https://aka.ms/policy-csp-localpoliciessecurityoptions-lanmanagerauthenticationlevel)  


  - **LM a NTLM**  
  - **LM, NTLM a NTLMv2**  
  - **NTLM**  
  - **Protokolu**  
  - **NTLMv2 a ne LM**  
  - **NTLMv2 a ne LM nebo NTLM**  
  
- **Nezabezpečené přihlášení hosta**  
  **Výchozí**: Nenakonfigurováno  
  LanmanWorkstation CSP: [LanmanWorkstation](https://aka.ms/policy-csp-lanmanworkstation-enableinsecureguestlogons)  

  Pokud toto nastavení povolíte, bude klient SMB odmítat nezabezpečená přihlášení hostů.  

  - **Nenakonfigurované**  
  - **Blok** – klient SMB odmítne nezabezpečená přihlášení hostů.  

### <a name="recovery-console-and-shutdown"></a>Konzola pro zotavení a vypnutí  

- **Při vypínání vymazat stránkovací soubor virtuální paměti**  
  **Výchozí**: Nenakonfigurováno  
   LocalPoliciesSecurityOptions CSP: [Shutdown_ClearVirtualMemoryPageFile](https://go.microsoft.com/fwlink/?linkid=867914)  


  - **Povolit** – vymažte stránkovací soubor virtuální paměti, když je zařízení vypnuté.  
  - **Nenakonfigurováno** – vymaže virtuální paměť.  

- **Vypnout bez přihlášení**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [Shutdown_AllowSystemToBeShutDownWithoutHavingToLogOn](https://go.microsoft.com/fwlink/?linkid=867912)  

  
  - **Blokovat** – skryje možnost vypnutí na přihlašovací obrazovce Windows. Uživatelé se musí k zařízení přihlásit, aby ho mohli vypnout.  
  - **Nenakonfigurováno** – povolí uživatelům vypnout zařízení z přihlašovací obrazovky Windows.  

### <a name="user-account-control"></a>Řízení uživatelských účtů  

- **UIA integrita bez zabezpečeného umístění**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867897)  
  
  - **Blok** – aplikace, které jsou v zabezpečeném umístění v systému souborů, budou spouštěny pouze s integritou UIAccess.  
  - **Nenakonfigurováno** – povolí spouštění aplikací s integritou UIAccess, i když nejsou aplikace v zabezpečeném umístění v systému souborů.  

- **Virtualizovat selhání zápisu souborů a registrů do umístění jednotlivých uživatelů**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=867900)  

  - **Povoleno** – aplikace, které zapisují data do chráněných umístění, selžou.  
  - **Nenakonfigurováno** – chyby zápisu aplikace se přesměrují za běhu do definovaných uživatelských umístění pro systém souborů a registr.  

- **Zvýšit jenom spustitelné soubory, které jsou podepsané a ověřené**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867965)  

  - **Povoleno** – vynutilo ověření cesty certifikace PKI pro spustitelný soubor, než bude možné ho spustit.  
  - **Nenakonfigurováno** – před spuštěním spustitelného souboru vynutili ověření cesty certifikace PKI.  

#### <a name="uia-elevation-prompt-behavior"></a>Chování výzvy ke zvýšení oprávnění UIA  

- **Výzva ke zvýšení úrovně oprávnění pro správce**  
  **Výchozí**: vyzvat k vyjádření souhlasu s binárními soubory jiného typu než Windows  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=867895)  

  Definujte chování výzvy ke zvýšení oprávnění pro správce v režimu schválení správcem.  

  - **Nenakonfigurované**  
  - **Zvýšit oprávnění bez dotaz**  
  - **Požádat o přihlašovací údajů na zabezpečené ploše**  
  - **Vyzvat k zadání pověření**  
  - **Požádat o souhlas**  
  - **Vyzvat k vyjádření souhlasu s binárními soubory jiného typu než Windows**  


- **Výzva ke zvýšení úrovně oprávnění pro standardní uživatele**  
  **Výchozí**: vyzvat k zadání přihlašovacích údajů  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=867896)  

  Definujte chování výzvy ke zvýšení oprávnění pro standardní uživatele.  

  - **Nenakonfigurované**  
  - **Automaticky zamítat žádosti o zvýšení oprávnění**  
  - **Požádat o přihlašovací údajů na zabezpečené ploše**  
  - **Vyzvat k zadání pověření**  

- **Výzvy ke zvýšení oprávnění tras k interaktivní ploše uživatele**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation](https://go.microsoft.com/fwlink/?linkid=867899)  


  - **Povoleno** – všechny požadavky na zvýšení oprávnění jdou přejít na plochu interaktivního uživatele, nikoli na zabezpečenou plochu. Použijí se všechna nastavení zásad chování výzev pro správce a standardní uživatele.  
  - **Nenakonfigurováno** – vynutí všechny žádosti o zvýšení oprávnění přejít na zabezpečenou plochu bez ohledu na nastavení zásad chování výzvy pro správce a standardní uživatele.

- **Výzva se zvýšenými oprávněními pro instalace aplikací**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867901)  

   - **Povoleno** – instalační balíčky aplikací nejsou zjištěny nebo se zobrazí výzva ke zvýšení oprávnění.
   - **Nenakonfigurováno** – uživatelům se zobrazí výzva k zadání uživatelského jména a hesla, když instalační balíček aplikace vyžaduje zvýšená oprávnění.

- **UIA výzvy ke zvýšení oprávnění bez zabezpečené plochy**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_AllowUIAccessApplicationsToPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867894)  

- **Enable** – povolí aplikacím UIAccess dotaz na zvýšení oprávnění bez použití zabezpečené plochy.  
- **Nenakonfigurované** – výzvy zvýšení úrovně oprávnění používají zabezpečenou plochu.  

#### <a name="admin-approval-mode"></a>Režim schválení správcem  

- **Režim schválení správcem pro předdefinovaný správce**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867902)  

  - **Povoleno** – povolí použití režimu schválení správce pro předdefinovaný účet správce. Všechny operace vyžadující zvýšení oprávnění zobrazí uživateli výzvu ke schválení operace.  
  - **Nenakonfigurováno** – spustí všechny aplikace s oprávněními úplný správce.  

- **Spustit všechny správce v režimu schválení správce**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867898)  


  - **Povoleno**– povolit režim schválení správcem.  
  - **Nenakonfigurováno** – zakažte režim schválení správce a všechna související nastavení zásad nástroje řízení uživatelských účtů.  

### <a name="microsoft-network-client"></a>Microsoft Network Client  

- **Digitálně podepsat komunikaci (Pokud server souhlasí)**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsIfServerAgrees](https://go.microsoft.com/fwlink/?linkid=868423)  

  Určuje, zda klient SMB vyjednává podepisování paketů SMB.  
  - **Block** – klient SMB nikdy nedohaduje podepisování paketů SMB.
  - **Nenakonfigurováno** – klient sítě Microsoft žádá server, aby po nastavení relace spouštěl podepisování paketů SMB. Pokud je na serveru podepisování paketů povolené, podepisování paketů se vyjedná.  

- **Poslat nešifrované heslo serverům SMB třetích stran**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=868426)  


  - **Blokovat** – přesměrovač SMB (Server Message Block) může posílat hesla ve formátu prostého textu na servery SMB jiné než Microsoft, které při ověřování nepodporují šifrování hesla.  
  - **Nenakonfigurováno** – zablokuje odesílání hesel ve formátu prostého textu. Hesla jsou zašifrovaná.  

- **Digitálně podepsat komunikaci (vždy)**  
  **Výchozí**: Nenakonfigurováno  
  LocalPoliciesSecurityOptions CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868425)  


  - **Povolit** – klient sítě Microsoftu nekomunikuje se serverem sítě Microsoft, pokud tento server nesouhlasí s podepisováním paketů SMB.  
  - **Nenakonfigurováno** – vyjednávat se podepisování paketů SMB mezi klientem a serverem.  

### <a name="microsoft-network-server"></a>Server sítě Microsoft  
  
- **Digitálně podepsat komunikaci (Pokud klient souhlasí)**  
  **Výchozí**: Nenakonfigurováno  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsIfClientAgrees](https://go.microsoft.com/fwlink/?linkid=868429)  

  - **Povolit** – síťový server Microsoftu vyjednává podepisování paketů SMB podle požadavků klienta. To znamená, že pokud je v klientovi podepisování paketů povolené, podepisování paketů se vyjedná.  
  - **Nenakonfigurováno** – klient SMB nikdy nedohaduje podepisování paketů SMB.  

- **Digitálně podepsat komunikaci (vždy)**  
  **Výchozí**: Nenakonfigurováno  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868428)  

  - **Povolit** – síťový server společnosti Microsoft nekomunikuje s klientem sítě Microsoft, pokud tento klient nesouhlasí s podepisováním paketů SMB.  
  - **Nenakonfigurováno** – vyjednávat se podepisování paketů SMB mezi klientem a serverem.  

## <a name="xbox-services"></a>Služby Xbox

- **Úloha uložení hry Xbox**  
  **Výchozí**: Nenakonfigurováno  
  CSP: [TaskScheduler/EnableXboxGameSaveTask](https://go.microsoft.com/fwlink/?linkid=875480)  
   
  Toto nastavení určuje, zda je úloha uložení hry Xbox povolená nebo zakázaná.  
  - **Umožněn**
  - **Nenakonfigurované**

- **Služba správy příslušenství pro Xbox**  
  **Výchozí**: ruční  
  CSP: [SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875481)  

  Toto nastavení určuje typ spuštění služby pro správu doplňku.  
  - **Zásah**
  - **Automaticky**
  - **Zabezpečen**

- **Služba Xbox Live auth Manager**  
  **Výchozí**: ruční  
  CSP: [SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875482)  
 
  Toto nastavení určuje typ spuštění služby Live auth Manager.  
  - **Zásah**
  - **Automaticky**
  - **Zabezpečen**
 
- **Služba Xbox Live pro uložení her**  
  **Výchozí**: ruční  
  CSP: [SystemServices/ConfigureXboxLiveGameSaveServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875483)  

  Toto nastavení určuje typ spuštění služby Live Game Save.  
  - **Zásah**
  - **Automaticky**
  - **Zabezpečen**

- **Síťová služba Xbox Live**  
  **Výchozí**: ruční  
  CSP: [SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875484)  

  Toto nastavení určuje typ spuštění síťové služby.  
  - **Zásah**
  - **Automaticky**
  - **Zabezpečen**

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](../configuration/device-profile-assign.md)a [sledujte jeho stav](../configuration/device-profile-monitor.md).  

Nakonfigurujte nastavení ochrany koncových bodů na zařízeních [MacOS](endpoint-protection-macos.md) .  
