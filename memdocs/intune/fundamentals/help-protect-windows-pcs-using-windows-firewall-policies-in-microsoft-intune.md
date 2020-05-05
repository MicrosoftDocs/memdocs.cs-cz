---
title: Zásady brány firewall pro počítače s Windows
titleSuffix: Microsoft Intune
description: Intune vám pomůže zabezpečit počítače, které spravujete, mnoha různými způsoby, včetně pomoci při konfiguraci nastavení brány Windows Firewall.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 9549c072-ac3d-4d14-a931-a2eda8846217
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57210928bf92c5300db69dc68d5d5dd4d37795e7
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079429"
---
# <a name="help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune"></a>Pomoc při ochraně počítačů s Windows pomocí zásad brány Windows Firewall v Microsoft Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Informace v tomto tématu se vztahují jenom na desktopové systémy Windows, které spravujete jako počítače (PC) pomocí softwarového klienta Intune. Pokud chcete spravovat nastavení brány firewall pro počítače s Windows zaregistrované jako mobilní zařízení, přečtěte si téma [Přidání nastavení ochrany koncových bodů v Intune](../protect/endpoint-protection-configure.md).

Microsoft Intune vám pomůže mnoha různými způsoby zabezpečit počítače s Windows, které spravujete. Jedním z těchto způsobů je poskytnutí zásad, které vám umožní nakonfigurovat nastavení brány Windows Firewall na počítačích.

Pokud jste ještě na svých počítačích nenainstalovali klienta Intune pro počítače s Windows, přečtěte si téma [instalace klienta na počítači s Windows pomocí Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

Informace v následujících částech vám pomohou s konfigurací, nasazováním a monitorováním zásad brány Windows Firewall na počítačích s Windows.

## <a name="use-intune-policies-to-manage-windows-firewall"></a>Použití zásad Intune ke správě brány Windows Firewall
Zásady brány Windows Firewall umožňují vytvářet a nasazovat nastavení, která řídí bránu Windows Firewall na spravovaných počítačích. Není možné spravovat vlastní výjimky pro bránu Windows Firewall a tato nastavení neovlivní brány firewall třetích stran.

> [!NOTE]
> Pokud jsou zásady Microsoft Intune a zásady skupiny nakonfigurované pro správu stejných nastavení na počítači PC, pak má nastavení zásad skupiny přednost před zásadami Microsoft Intune. Informace o tom, jak zamezit konfliktům mezi zásadami Intune a zásadami skupiny, najdete v článku [Řešení konfliktů GPO a zásad Microsoft Intune](resolve-gpo-and-microsoft-intune-policy-conflicts.md).
>
> Pokud chcete nasadit nastavení brány Windows Firewall do počítačů se systémem Windows Vista, musíte na tyto počítače nejdřív nainstalovat [opravu Hotfix KB971800](https://support2.microsoft.com/kb/971800).

> [!IMPORTANT]
> Pokud chcete spravovat bránu Windows Firewall pomocí Intune, musí být na počítačích, které spravujete, povolené tyto dvě služby:
>
> - Brána Windows Firewall
> - Agent zásad protokolu IPsec

## <a name="configure-a-windows-firewall-policy"></a>Konfigurace zásad brány Windows Firewall

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)klikněte na **zásady** &gt; **Přidat zásadu**.

2. Konfigurujte a nasaďte zásady **nastavení brány Windows Firewall**. Můžete použít doporučená nastavení, nebo nastavení upravit. Pokud potřebujete další informace o tom, jak vytvořit a nasadit zásady, Projděte si článek [běžné úlohy správy počítačů s Windows pomocí počítačového klienta Microsoft Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md).

    V následující části jsou uvedené hodnoty, které můžete v zásadách konfigurovat, a také výchozí hodnoty, které se použijí, pokud zásady neupravíte.

Po nasazení zásad brány Windows Firewall můžete zobrazit stav těchto zásad na stránce **Všechny zásady** pracovního prostoru **Zásady**.

## <a name="specify-policy-settings-for-windows-firewall"></a>Zadání nastavení zásad brány Windows Firewall

### <a name="turn-on-windows-firewall"></a>Zapnout bránu Windows Firewall

Toto nastavení zásad povoluje bránu Windows Firewall na spravovaných počítačích, které jsou:
- Připojené k doméně (například na pracovišti)
- Připojené k privátní (důvěryhodné) síti (jako je třeba domácí síť)
- Připojené k nedůvěryhodné veřejné síti (například v kavárně)

Výchozí hodnota pro každé z těchto nastavení je **Ano**, což je nejbezpečnější hodnota.



### <a name="block-all-incoming-connections-including-those-in-the-list-of-allowed-programs"></a>Blokování všech příchozích připojení, včetně připojení uvedených na seznamu povolených programů

Tato nastavení zásad konfigurují bránu Windows Firewall, aby blokovala příchozí síťový provoz na počítačích, které jsou:
- Připojené k doméně (například na pracovišti)
- Připojené k privátní (důvěryhodné) síti (jako je třeba domácí síť)
- Připojené k nedůvěryhodné veřejné síti (například v kavárně)

Výchozí hodnota pro každé z těchto nastavení je **Ano**, což je nejbezpečnější hodnota.

> [!IMPORTANT]
> Pokud prostředí obsahuje spravované počítače, ve kterých je spuštěný systém Windows Vista bez nainstalovaných aktualizací Service Pack, musíte nainstalovat aktualizaci uvedenou ve znalostní bázi Microsoft Knowledge Base v [článku 971800](https://go.microsoft.com/fwlink/?LinkId=188405) nebo v zásadách nasazených v těchto počítačích vypnout nastavení zásady **Blokovat všechna příchozí připojení**.

### <a name="notify-the-user-when-windows-firewall-blocks-a-new-program"></a>Oznámit uživatelům blokování nového programu bránou Windows Firewall

Tato nastavení zásad určují, jestli brána Windows Firewall upozorní uživatele počítačů, když blokuje příchozí síťový provoz na počítačích, které jsou:
- Připojené k doméně (například na pracovišti)
- Připojené k privátní (důvěryhodné) síti (jako je třeba domácí síť)
- Připojené k nedůvěryhodné veřejné síti (například v kavárně)

Výchozí hodnota pro každé z těchto nastavení je **Ano**.


### <a name="configure-predefined-exceptions"></a>Konfigurace předdefinovaných výjimek

Můžete nakonfigurovat výjimky, které povolují konkrétní typy síťového přenosu přes bránu firewall bez ohledu na hodnoty, které jste nakonfigurovali dřív. Ve výchozím nastavení nejsou nakonfigurovaná žádná z těchto nastavení.

|Název nastavení|Podrobnosti|
|------------------|--------------------|
|**Služba BranchCache – načítání obsahu**<br>(Windows 7 nebo novější)|Umožňuje klientům služby BranchCache prostřednictvím protokolu HTTP načítat obsah z ostatních klientů služby BranchCache (v distribuovaném režimu) a z hostované mezipaměti (v režimu hostované mezipaměti). Toto nastavení využívá protokol HTTP.|
|**Služba BranchCache – klient hostované mezipaměti**<br>(Windows 7 nebo novější)|Umožňuje klientům služby BranchCache používat hostovanou mezipaměť. Toto nastavení využívá protokol HTTPS.|
|**Služba BranchCache – server hostované mezipaměti**|Umožňuje klientům služby BranchCache používat hostovanou mezipaměť ke komunikaci s ostatními klienty. Toto nastavení využívá protokol HTTPS.|
|**Služba BranchCache – zjišťování rovnocenných zařízení**<br>(Windows 7 nebo novější)|Umožňuje klientům služby BranchCache používat protokol WS-Discovery (Web Services Dynamic Discovery) k vyhledání dostupnosti obsahu v místní podsíti.|
|**Ukládání do sdílené mezipaměti BITS**|Umožňuje klientům používat službu inteligentního přenosu na pozadí (BITS) k vyhledání a sdílení souborů uložených v mezipaměti BITS na klientských počítačích ve stejné podsíti. Toto nastavení využívá službu WSDAPI (Web Services on Devices ) a vzdálené volání procedur (RPC).|
|**Připojení k síťovému projektoru**|Umožňuje uživatelům připojit se k projektorům prostřednictvím drátových nebo bezdrátových sítí a promítat prezentace. Toto nastavení využívá rozhraní WSDAPI.|
|**Základní síťové služby**|Umožňuje klientům používat protokoly IPv4 a IPv6 pro připojení k síťovým prostředkům.|
|**Koordinátor distribuovaných transakcí**|Umožňuje spravovaným počítačům koordinovat transakce, které aktualizují prostředky s ochranou transakcí, jako jsou databáze, fronty zpráv nebo souborové systémy.|
|**Sdílení souborů a tiskáren**|Umožňuje uživatelům sdílet místní soubory a tiskárny s dalšími uživateli v síti. Toto nastavení využívá NetBIOS, LLMNR (Link Local Multicast Name Resolution), protokol SMB (Server Message Block) a RPC.|
|**Domácí skupina**<br>(Windows 7 nebo novější)|Umožňuje spravovaným počítačům účast v síti domácí skupiny.|
|**Služba iSCSI**|Umožňuje spravovaným počítačům připojení k serverům a zařízením iSCSI.|
|**Služba správy klíčů**|Umožňuje spočítání počítačů kvůli shodě s licencí v podnikovém prostředí.|
|**Zařízení Media Center Extender**|Umožňuje zařízením Media Center Extender komunikovat s počítači se systémem Windows Media Center. Toto nastavení využívá protokol SSDP (Simple Service Discovery Protocol) a qWave.|
|**Služba Netlogon**|Konfiguruje zabezpečený kanál mezi klienty v doméně a řadičem domény za účelem ověřování totožnosti uživatelů a služeb. Toto nastavení využívá protokol RPC.|
|**Zjištění sítě**|Umožňuje počítačům zjišťovat jiná zařízení a být zjištěny jinými zařízeními v síti. Toto nastavení používá službu publikování a hostitele rozpoznávání funkcí a taky síťové protokoly SSDP, NetBIOS, LLMNR a UPnP.|
|**Výstrahy a protokolování výkonu**|Umožňuje vzdálenou správu služby Výstrahy a protokolování výkonu. Toto nastavení využívá protokol RPC.|
|**Vzdálená správa**|Umožňuje vzdálenou správu počítače.|
|**Vzdálená pomoc**|Umožňuje uživatelům spravovaných počítačů žádat o vzdálenou pomoc od jiných uživatelů v síti. Toto nastavení používá síťové protokoly SSDP, PNRP (Peer Name Resolution Protocol), Teredo a UPnP.|
|**Vzdálená plocha**|Umožňuje počítači přistupovat k jiným počítačům pomocí vzdálené plochy.|
|**Vzdálená správa protokolu událostí**|Umožňuje vzdálené zobrazení a správu protokolů událostí klienta. Toto nastavení využívá pojmenované kanály a rozhraní RPC.|
|**Vzdálená správa naplánovaných úloh**|Umožňuje vzdálenou správu služby plánování úloh. Toto nastavení využívá protokol RPC.|
|**Vzdálená správa služeb**|Umožňuje vzdálenou správu místních služeb na klientech. Toto nastavení využívá pojmenované kanály a rozhraní RPC.|
|**Vzdálená správa svazků**|Umožňuje vzdálenou softwarovou a hardwarovou správu svazku disku. Toto nastavení využívá protokol RPC.|
|**Směrování a vzdálený přístup**|Umožňuje příchozí připojení VPN a připojení se vzdáleným přístupem k počítačům.|
|**Protokol SSTP**|Umožňuje příchozí připojení VPN ke spravovaným počítačům pomocí protokolu SSTP (Secure Socket Tunneling Protocol). Toto nastavení využívá protokol HTTPS.|
|**Zachytávání pro službu SNMP**|Umožňuje spravovaným počítačům přijímat přenos služby depeší protokolu SNMP (Simple Network Management Protocol).|
|**Architektura UPnP**|Konfiguruje službu Architektura UPnP na počítačích, aby mohly zjišťovat a používat certifikovaná zařízení UPnP.|
|**Služba registrace názvu počítače pro Centrum spolupráce**|Umožňuje počítačům najít další počítače a komunikovat s nimi pomocí protokolů SSDP a PNRP.|
|**Windows Media Player**|Umožňuje uživatelům přijímat multimédia streamovaná přes UDP (User Datagram Protocol).|
|**Služba Windows Media Player Network Sharing**|Umožňuje uživatelům sdílet multimédia přes síť. Toto nastavení používá síťové protokoly SSDP, qWave a UPnP.|
|**Služba Windows Media Player Network Sharing (Internet)**<br>(Windows 7 nebo novější)|Umožňuje uživatelům sdílet domácí multimédia prostřednictvím internetu.|
|**Centrum spolupráce**|Umožňuje uživatelům spolupracovat přes síť a sdílet tak dokumenty, programy nebo plochy. Toto nastavení využívá službu Replikace distribuovaného systému souborů (DFSR) a P2P.|
|**Základ spolupráce rovnocenných počítačů**|Konfiguruje různé programy a technologie typu peer-to-peer, aby se mohly připojit. Toto nastavení využívá protokol SSDP a PNRP.|
|**Vzdálená správa Windows (režim kompatibility)**|Umožňuje vzdálenou správu spravovaných počítačů pomocí služby vzdálené správy systému Windows (WS-Management), což je protokol založený na webových službách pro vzdálenou správu operačních systémů a zařízení.|
|**Vzdálená správa systému Windows**<br>(Windows 8 nebo novější)|Umožňuje vzdálenou správu spravovaných počítačů pomocí služby vzdálené správy systému Windows (WS-Management), což je protokol založený na webových službách pro vzdálenou správu operačních systémů a zařízení.|
|**Windows Virtual PC**<br>(Windows 7 nebo novější)|Umožňuje virtuálním počítačům komunikovat s dalšími počítači.|
|**Bezdrátová přenosná zařízení**|Umožňuje přenos multimediálních souborů z fotoaparátu nebo multimediálního zařízení připojeného k síti do spravovaných počítačů pomocí protokolu MTP (Media Transfer Protocol). Toto nastavení používá síťové protokoly SSDP a UPnP.|

## <a name="see-also"></a>Viz také
[Zásady ochrany počítačů se systémem Windows](policies-to-protect-windows-pcs-in-microsoft-intune.md)
