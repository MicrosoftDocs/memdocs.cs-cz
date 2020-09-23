---
title: Použití řešení Microsoft Tunnel VPN pro Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si o bráně Microsoft Tunnel Gateway, serveru VPN pro Intune, který běží na Linux. Cloudová zařízení od Microsoftu, která spravujete pomocí Intune, můžou mít přístup k místní infrastruktuře.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b77b9aea2fae8173389d3e660744fbb32424a89b
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017710"
---
# <a name="microsoft-tunnel-for-microsoft-intune"></a>Tunelové propojení Microsoft pro Microsoft Intune

Tunelové propojení Microsoft je řešení brány VPN pro Microsoft Intune. Tunelové propojení umožňuje přístup k místním prostředkům ze zařízení s iOS/iPadOS a Androidem Enterprise pomocí moderního ověřování a podmíněného přístupu. Tento článek vysvětluje, jak tunel funguje, včetně požadavků na jeho použití a jeho architektury.

*Tunelové propojení Microsoft je ve verzi Public Preview*.

Pokud máte nastavené požadované konfigurace a jste připraveni k instalaci tunelu, přečtěte si téma [Konfigurace tunelu Microsoft](../protect/microsoft-tunnel-configure.md).

## <a name="overview-of-microsoft-tunnel"></a>Přehled tunelového propojení Microsoft

Microsoft Tunnel Gateway se nainstaluje do kontejneru Docker, který běží na serveru Linux. Server Linux může být fyzické pole v místním prostředí nebo virtuální počítač, který běží místně nebo v cloudu. Po instalaci tunelu použijete profily sítě VPN v Intune pro iOS nebo Android a nasměrujete zařízení tak, aby používala tunel pro připojení k podnikové síti a prostředkům. Po hostování tunelu v cloudu budete muset použít řešení jako Azure ExpressRoute k rozšiřování vaší místní sítě do cloudu.

Prostřednictvím centra pro správu Microsoft Endpoint Manageru:

- Stáhněte si instalační skript Microsoft Tunneling, který budete spouštět na serverech se systémem Linux.
- Nakonfigurujte aspekty brány Microsoft Tunnel Gateway, jako jsou IP adresy, servery DNS a porty.
- Nasaďte profily sítě VPN do zařízení a nasměrujte je tak, aby používaly tunel.
- Nasaďte do svých zařízení aplikace Microsoft Tunneling.

Prostřednictvím aplikace Microsoft Tunneling, zařízení s iOS/iPadOS a Android Enterprise:

- K ověření tunelu použijte Azure Active Directory (Azure AD).
- Se vyhodnocují na základě zásad podmíněného přístupu. Pokud zařízení nedodržuje předpisy, nebude mít přístup k vašemu serveru VPN ani k vaší místní síti.

Pokud se chcete připojit k tunelu, zařízení používají aplikaci Microsoft Tunnel, která je dostupná v obchodech s iOS/iPadOS nebo Androidem.

Pro podporu tunelu Microsoft můžete nainstalovat více serverů Linux a kombinovat servery do logických skupin označovaných jako *weby*. Každý server se může připojit k jedné lokalitě. Když nakonfigurujete lokalitu, definujete bod připojení, který budou zařízení používat při přístupu k tomuto tunelu. Lokality vyžadují *konfiguraci serveru* , kterou definujete a přiřadíte k lokalitě. Konfigurace serveru se aplikuje na každý server, který přidáte do této lokality. tím se zjednoduší konfigurace dalších serverů.

Pokud chcete zařízení směrovat pomocí tunelového propojení, vytvoříte a nasadíte zásady sítě VPN pro tunelování Microsoft. Tato zásada je profilem sítě VPN konfigurace zařízení, který pro typ připojení používá tunel Microsoftu.

Mezi funkce profilů sítě VPN pro tunelové propojení patří:

- Popisný název připojení VPN, které koncoví uživatelé uvidí.
- Lokalita, ke které se klient VPN připojuje
- Konfigurace sítě VPN pro jednotlivé aplikace definující aplikace, pro které se profil sítě VPN používá, a pokud jsou vždycky zapnuté. Pokud je tato funkce vždycky zapnutá, připojení k síti VPN se automaticky připojí a použije se jenom pro aplikace, které definujete. Pokud nejsou definované žádné aplikace, připojení Always On zajišťuje přístup k tunelu pro veškerý síťový provoz ze zařízení.
- Ruční připojení k tunelu, když uživatel spustí síť VPN a vybere *připojit*.
- Podpora proxy (iOS/iPadOS, Android 10 +)

Mezi konfigurace serveru patří:

- Rozsah IP adres – IP adresy, které jsou přiřazené zařízením, která se připojují k tunelu Microsoftu.
- DNS servery – zařízení serveru DNS by se měla použít, když se připojí k serveru.
- Hledání přípon DNS.
- Rozdělit pravidla tunelování – až 500 pravidla sdílená mezi zahrnutím a vyloučením tras. Pokud například vytvoříte 300 pravidel zahrnutí, můžete mít až 200 pravidel pro vyloučení.
- Port – port, na kterém naslouchá brána Microsoft tunel.

Konfigurace lokality zahrnuje:

- Veřejná IP adresa nebo plně kvalifikovaný název domény, což je bod připojení pro zařízení, která používají tunel. Tato adresa může být pro jednotlivý Server nebo IP adresu nebo plně kvalifikovaný název domény serveru pro vyrovnávání zatížení.
- Konfigurace serveru, která se používá na každém serveru v lokalitě.

K lokalitě přiřadíte Server v době instalace softwaru pro tunelování na server Linux. Instalace používá skript, který můžete stáhnout v centru pro správu. Po spuštění skriptu se zobrazí výzva, abyste nakonfigurovali jeho operaci pro vaše prostředí, což zahrnuje určení lokality, ke které se bude server připojovat.

Aby bylo možné používat tunelové propojení od Microsoftu, zařízení bude muset nainstalovat aplikaci Microsoft Tunnel. Aplikaci získáte z App Storu pro iOS/iPadOS nebo Android a nasadíte ji uživatelům.

## <a name="configure-prerequisites-for-microsoft-tunnel"></a>Konfigurace požadavků pro tunelové propojení Microsoft

V následujících částech jsou popsány požadavky na server Linux, který je hostitelem softwaru pro tunelování a ve vaší síti.  

> [!NOTE]
> Tunelové propojení Microsoft se u Azure Government cloudových prostředí nepodporuje.

### <a name="linux-server"></a>Server Linux

Nastavte virtuální počítač založený na systému Linux nebo fyzický server, na který se bude instalovat brána Microsoft Tunnel Gateway.

- **Distribuce systému Linux** – jsou podporovány následující:

  - CentOS 7.4 + (CentOS 8 + se nepodporuje)
  - Red Hat (RHEL) 7.4 + (RHEL 8 + není podporováno)
  - Ubuntu 18.04
  - Ubuntu 20.04

- **Velikost serveru Linux**: pro splnění očekávaného použití použijte následující pokyny:

  |Počet zařízení | Počet procesorů | Paměť – GB | Počet serverů | Počet webů | Místo na disku GB |
  |----------|--------|-----------|-----------|---------|---------------|
  | 1 000    | 4      | 4         | 1         | 1       | 30            |
  | 2 000    | 4      | 4         | 1         | 1       | 30            |
  | 5 000    | 8      | 8         | 2         | 1       | 30            |
  | 10 000   | 8      | 8         | 3         | 1       | 30            |
  | 20 000   | 8      | 8         | 4         | 1       | 30            |
  | 40,000   | 8      | 8         | 8         | 1       | 30            |

  Podpora se škáluje lineárně. Zatímco každé tunelové propojení Microsoftu podporuje až 64 000 souběžných připojení, můžou jednotlivá zařízení otevřít víc připojení.

- **Procesor**: 64 procesor AMD/Intel.

- **Nainstalovat Docker**: Nainstalujte Docker verze 19,03 CE nebo novější.

  Aby bylo možné poskytovat podporu kontejnerů, Microsoft Tunnel vyžaduje Docker na serveru se systémem Linux. Kontejnery poskytují konzistentní spouštěcí prostředí, monitorování stavu a proaktivní nápravu a čisté prostředí pro upgrade.

  Informace o instalaci a konfiguraci Docker najdete v tématu:

  - [Nainstalovat modul Docker do CentOS]( https://docs.docker.com/engine/install/centos/)
  - [Používání Docker na Red Hat Enterprise Linux 7](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.0_release_notes/sect-red_hat_enterprise_linux-7.0_release_notes-linux_containers_with_docker_format-using_docker)
  - [Nainstalovat modul Docker do Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

- **Certifikát TLS (Transport Layer Security)**: Server Linux vyžaduje důvěryhodný certifikát TLS pro zabezpečení připojení mezi zařízeními a serverem brány tunelového propojení. Během instalace brány tunelového připojení přidáte do serveru certifikát TLS, včetně úplného důvěryhodného řetězu certifikátů.

  - Certifikát TLS použitý k zabezpečení koncového bodu brány tunelového připojení musí obsahovat IP adresu nebo plně kvalifikovaný název domény serveru brány tunelového připojení v síti SAN.

  - Certifikát TLS nemůže mít datum vypršení platnosti delší než dva roky. Pokud je datum delší než dva roky, nebude přijato na zařízeních s iOS.

  - Použití zástupných znaků má omezená podpora. Například ** \* . contoso.com** je podporováno. **pokračování \* . com** se nepodporuje.

  - Během instalace serveru brány tunelového připojení je nutné zkopírovat celý řetěz důvěryhodných certifikátů na server Linux. Instalační skript poskytuje umístění, kam se zkopírují soubory certifikátů, a vyzve vás k tomu.

  - Pokud používáte certifikát TLS, který není veřejně důvěryhodný, je nutné odeslat celý řetěz důvěryhodnosti do zařízení pomocí profilu *důvěryhodného certifikátu* Intune.

  - Certifikát TLS může být ve formátu **PEM** nebo **PFX** .

### <a name="network"></a>Síť

Pro zvýšení výkonu doporučujeme použít dva řadiče síťového rozhraní (nic) na server Linux, přestože použití dvou je volitelné.

- **Síťová karta 1** – Tato síťová karta zpracovává provoz ze spravovaných zařízení a měla by být ve veřejné síti s veřejnou IP adresou.Tato IP adresa je adresa, kterou nakonfigurujete v *konfiguraci lokality*. Tato adresa může představovat jediný server nebo nástroj pro vyrovnávání zatížení.

- **Síťová karta 2** – Tato síťová karta zpracovává provoz na vaše místní prostředky a měla by být ve vaší privátní interní síti bez segmentace sítě.

Pokud spustíte Linux jako virtuální počítač v cloudu, budete muset zajistit, aby server měl přístup k vaší místní síti. Například pokud váš virtuální počítač běží v Azure, můžete k poskytnutí přístupu použít [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) nebo něco podobného. Pokud server spouštíte na místním VIRTUÁLNÍm počítači, ExpressRoute není nutné.

Pokud se rozhodnete přidat nástroj pro vyrovnávání zatížení, Projděte si informace o konfiguraci v dokumentaci k dodavatelům. Vezměte v úvahu porty síťového provozu a brány firewall specifické pro Intune a tunelové propojení Microsoftu.

### <a name="firewall"></a>Brána firewall

Ve výchozím nastavení používá tunel a server Microsoft následující porty:

**Příchozí porty**:

- TCP 443 – vyžadované tunelovým propojením Microsoftu
- UDP 443 – vyžadováno tunelovým propojením Microsoftu.
- TCP 22 – volitelné. Používá se pro SSH/SCP pro server Linux.

**Odchozí porty**:

- TCP 443 – vyžadováno pro přístup ke službám Intune. Požadováno nástrojem Docker k vyžádání imagí.
- TCP – 80 – vyžadováno pro přístup ke službám Intune.

Když vytvoříte konfiguraci serveru pro tunelové propojení, můžete zadat jiný port, než je výchozí hodnota 443. Pokud zadáte jiný port, nezapomeňte nakonfigurovat brány firewall tak, aby podporovaly vaši konfiguraci.

**Další požadavky**:

- Tunel sdílí stejné požadavky jako [koncové body sítě pro Microsoft Intune](../fundamentals/intune-endpoints.md)s přidáním portu TCP 22, jak je uvedeno výše.

- Nakonfigurujte pravidla brány firewall tak, aby podporovala konfigurace popsané v části  [Konfigurace pravidel brány firewall klienta Microsoft Container Registry (MCR)](https://github.com/microsoft/containerregistry/blob/master/client-firewall-rules.md).

### <a name="proxy"></a>Proxy server

Můžete použít proxy server s tunelovým propojením Microsoftu. Následující požadavky vám pomůžou nakonfigurovat server Linux a vaše prostředí pro úspěch:

- Pokud používáte interní proxy server, bude pravděpodobně nutné nakonfigurovat hostitele se systémem Linux tak, aby používal vaši proxy server pomocí proměnných prostředí. Chcete-li použít proměnné, upravte soubor **/etc/Environment** na serveru Linux a přidejte následující řádky:

  `http_proxy=[address]`  
  `https_proxy=[address]`

- Ověřené proxy servery nejsou podporované.

- Proxy server nemůže provést přerušení a kontrolu. Je tomu tak proto, že server Linux používá při připojování k Intune vzájemné ověřování TLS.

- Nakonfigurujte Docker tak, aby používal proxy server k vyžádání imagí. Provedete to tak, že upravíte soubor **/etc/systemd/System/Docker.Service.d/HTTP-proxy.conf** na serveru Linux a přidáte následující řádky:

  ```
  [Service]
  Environment="HTTP_PROXY=http://your.proxy:8080/"
  Environment="HTTPS_PROXY=http://your.proxy:8080/"
  Environment="NO_PROXY=127.0.0.1,localhost
  ```

  > [!NOTE]  
  > Tunelové propojení Microsoft nepodporuje Aplikace Azure AD proxy server ani podobná řešení proxy.

### <a name="platforms"></a>Platformy

Tunelové propojení Microsoftu podporuje jenom zařízení, která jsou zaregistrovaná v Intune. Podporovány jsou následující platformy zařízení:

- Android Enterprise (plně spravovaný, podnikový pracovní profil, pracovní profil)
- iOS/iPadOS

Všechny platformy podporují následující funkce:

- Ověřování pomocí Azure Active Directory (Azure AD) pro tunelové připojení pomocí uživatelského jména a hesla nebo certifikátů.
- Podpora pro jednotlivé aplikace.
- Ruční tunelové propojení zařízení prostřednictvím tunelové aplikace, kde uživatel spouští VPN a vybere *připojit*.
- Dělené tunelové propojení. Pravidla tunelového propojení v iOS se ale při použití *sítě VPN pro jednotlivé aplikace*ignorují.

Podpora proxy serveru je omezená na tyto platformy:

- Android 10 a novější
- iOS/iPadOS

## <a name="run-the-readiness-tool"></a>Spuštění nástroje Readiness Tool

Než začnete s instalací serveru, doporučujeme si stáhnout a spustit nástroj **připravenosti na MST** . Tento nástroj je skript, který běží na serveru Linux a provádí následující akce:

- Potvrdí, že konfigurace sítě umožňuje Microsoft Tunneling přístup k požadovaným koncovým bodům Microsoftu.  
- Ověří, jestli účet Azure Active Directory (Azure AD), který budete používat k instalaci tunelu Microsoft, má požadované role pro dokončení registrace. 

Nástroj připravenosti na MST má závislost na **JQ**, což je procesor JSON pro příkaz. Před spuštěním nástroje Readiness Tool se ujistěte, že je nainstalovaná **JQ** . Informace o tom, jak získat a nainstalovat **JQ**, najdete v dokumentaci k verzi systému Linux, kterou používáte.

Použití nástroje Readiness Tool:

1. Získejte nástroj Readiness pomocí jedné z následujících metod:
   - Stáhněte si nástroj přímo pomocí webového prohlížeče.  Chcete https://aka.ms/microsofttunnelready -li stáhnout soubor s názvem **MST – připravenost**, klikněte na Přejít.
   - Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Správa tenanta**  >  **Microsoft Tunnel Gateway**, vyberte kartu **servery** , vyberte **vytvořit** a otevřete podokno *vytvořit server* a pak vyberte **stáhnout Nástroj připravenosti**.  
   - K získání nástroje Readiness použijte příkaz pro Linux přímo. Například můžete použít **wget** nebo **oblý** k otevření odkazu https://aka.ms/microsofttunnelready .

   Skript můžete spustit z libovolného serveru Linux, který je ve stejné síti jako server, který chcete nainstalovat, a umožnit tak správcům sítě spouštět ho a řešit problémy se sítí nezávisle.

2. Chcete-li ověřit konfiguraci sítě, spusťte skript jako **kořenový adresář** a použijte následující příkazový řádek: `./mst-readiness network`

   Skript spustí následující akce a ohlásí při úspěchu nebo chybě pro obojí:
   - Pokusí se připojit ke každému koncovému bodu Microsoftu, který bude tunel používat.
   - Kontroluje, zda jsou požadované porty otevřeny v bráně firewall.

3. Pokud chcete ověřit, že účet, který budete používat k instalaci tunelu Microsoft, má požadované role a oprávnění pro dokončení registrace, spusťte skript s následujícím příkazovým řádkem: `./mst-readiness account`

   Skript vás vyzve k použití jiného počítače s webovým prohlížečem, který používáte k ověření pro Azure AD a Intune. Nástroj bude hlásit úspěch nebo chybu.

Další informace o tomto nástroji najdete v článku referenční informace [k MST-CLI](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel-gateway) v referenčním článku pro Microsoft Tunnel.

## <a name="use-conditional-access-with-the-microsoft-tunnel"></a>Použití podmíněného přístupu s tunelem Microsoftu

Když použijete podmíněný přístup s Intune, můžete vytvořit zásady pro přístup zařízení k bráně Microsoft Tunnel.

### <a name="provision-your-tenant"></a>Zřízení tenanta

Než budete moct nakonfigurovat zásady podmíněného přístupu pro tunel, musíte vašemu klientovi povolit podporu tunelového propojení Microsoft pro podmíněný přístup. Pokud chcete svého tenanta povolit, spusťte skript PowerShellu, který upraví vašeho tenanta a přidá **Microsoft Tunnel Gateway** jako cloudovou aplikaci, kterou pak můžete vybrat jako součást zásad podmíněného přístupu.  Tento proces vyžaduje použití modulu Azure Active Directory PowerShellu.

1. [Stáhněte a nainstalujte](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0&preserve-view=true) **modul prostředí PowerShell pro AzureAD**.

2. Stáhněte si skript PowerShellu s názvem **mst-CA-provisioning.ps1** z **aka.MS/MST-CA-Provisioning**.

3. Pomocí přihlašovacích údajů, které mají oprávnění role Azure [stejné jako **správce aplikace**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#application-administrator-permissions), spusťte skript z libovolného umístění ve vašem prostředí a zřiďte svého tenanta. Skript upraví tenanta vytvořením principu služby s následujícími podrobnostmi:

   - ID aplikace: 3678c9e9-9681-447a-974d-d19f668fcd88
   - Název: Microsoft Tunnel Gateway

   Přidání tohoto principu služby je povinné, abyste mohli při konfiguraci zásad podmíněného přístupu vybrat cloudovou cloudovou aplikaci. Pomocí grafu je také možné do svého tenanta přidat informace o zásadách služby.  
4. Po dokončení skriptu můžete pomocí běžného procesu vytvořit zásady podmíněného přístupu.

Pokud chcete vytvořit zásady pro podmíněný přístup, přečtěte si téma [Vytvoření zásady podmíněného přístupu na základě zařízení](../protect/create-conditional-access-intune.md).

### <a name="create-conditional-access-policy-to-limit-access-to-microsoft-tunnel"></a>Vytvoření zásad podmíněného přístupu pro omezení přístupu k tunelu Microsoft

Pokud se rozhodnete nakonfigurovat zásadu podmíněného přístupu, abyste omezili přístup uživatelů, doporučujeme tyto zásady nakonfigurovat až po zřízení tenanta, aby podporoval cloudovou aplikaci Microsoft Tunnel Gateway, ale před instalací brány tunelového připojení.

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru centrum](https://go.microsoft.com/fwlink/?linkid=2109431)pro  >  **zabezpečení**  >  **podmíněný přístup zásady podmíněného přístupu**  >  **New policy**.
2. Zadejte název těchto zásad.
3. Pokud chcete nakonfigurovat přístup uživatelů a skupin, vyberte v části *přiřazení*možnost **Uživatelé a skupiny**.
   1. Vyberte možnost **Zahrnout**  >  **všechny uživatele**.  
   2. V dalším kroku vyberte **vyloučit** a nakonfigurujte skupiny, kterým chcete *udělit přístup*, a pak konfiguraci uživatele a skupiny uložte.
4. Pod *ovládacími prvky přístupu*vyberte **udělit**, vyberte **blokovat přístup**a pak konfiguraci uložte.  
5. Nastavte **Povolit zásadu** na **Zapnuté**.
6. Vyberte **Vytvořit**.

## <a name="architecture"></a>Architektura

Microsoft Tunnel Gateway běží v kontejnerech Docker, které běží na serverech se systémem Linux.  

![Vykreslení architektury brány Microsoft Tunnel Gateway](./media/microsoft-tunnel-overview/tunnel-architecture.png)
  
**Součásti**:  
- **A** – Microsoft Intune.
- **B**-Azure Active Directory (AD).
- **C** – Linux Server s Docker.
  - **CI** – Microsoft Tunnel Gateway.
  - **Cii** – Agent pro správu
  - **CIII** – modul plug-in ověřování – ověřovací modul plug-in, který se ověřuje ve službě Azure AD.
- **D** – veřejná IP adresa nebo plně kvalifikovaný název domény tunelového propojení Microsoftu. To může představovat Nástroj pro vyrovnávání zatížení.
- **E** – zařízení zaregistrovaná ve správě mobilních zařízení (MDM).
- **F** – brána firewall
- **G** – interní proxy server (volitelné).
- **H** – podniková síť.
- **I** – veřejný Internet.

**Akce**:  
- **1** – správce Intune nakonfiguruje *lokality*a *Konfigurace serveru* a konfigurace serveru jsou přidružené k lokalitám nástroje.
- **2** – správce Intune nainstaluje bránu Microsoft Tunnel Gateway a ověřovací modul plug-in ověřuje bránu Microsoft Tunnel Gateway pomocí Azure AD. Server Microsoft Tunnel Gateway je přiřazen k lokalitě.
- **3** – Agent pro správu komunikuje s Intune, aby načetl vaše zásady konfigurace serveru a odesílal do Intune protokoly telemetrie.  
- **4** – správce Intune vytváří a nasazuje profily sítě VPN a tunelové aplikace do zařízení.  
- **5** – zařízení se ověřuje ve službě Azure AD. Vyhodnotí se zásady podmíněného přístupu.  
- **6** – s rozděleným tunelem:  
  - **6a** – některý provoz směřuje přímo k veřejnému Internetu.  
  - **6b** – některý z provozu přechází do vaší veřejné IP adresy pro tunel.  
- **7** – tunel směruje provoz na váš interní proxy server (volitelné) a vaši podnikovou síť.

**Další podrobnosti**:

- Podmíněný přístup se provádí v klientovi VPN a v závislosti na cloudové aplikaci *Microsoft Tunnel Gateway*. Nevyhovující zařízení neobdrží přístupový token ze služby Azure AD a nemůže získat přístup k serveru VPN. Další informace o použití podmíněného přístupu s tunelovým propojením Microsoftu najdete v tématu [použití podmíněného přístupu s tunelovým propojením Microsoftu](#use-conditional-access-with-the-microsoft-tunnel).

- Agent pro správu je autorizovaný pro Azure AD pomocí Azure App ID/tajných klíčů.

- Server brány tunelového připojení používá překlad adres (NAT) k poskytování adres klientům VPN, kteří se připojují k podnikové síti.
  
## <a name="next-steps"></a>Další kroky

[Instalace a konfigurace tunelu Microsoft](microsoft-tunnel-configure.md)
