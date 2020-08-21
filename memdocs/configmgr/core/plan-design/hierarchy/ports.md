---
title: Porty používané pro připojení
titleSuffix: Configuration Manager
description: Přečtěte si o požadovaných a přizpůsobitelných síťových portech, které Configuration Manager používá pro připojení.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2495c0d7b5b19b5d6f7741d3b28b6a9a0e213fc3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700142"
---
# <a name="ports-used-in-configuration-manager"></a>Porty používané v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje seznam síťových portů, které Configuration Manager používá. Některá připojení používají porty, které nejsou konfigurovatelné, a některá podporují vlastní porty, které zadáte. Pokud používáte jakoukoli technologii filtrování portů, ověřte, že jsou k dispozici požadované porty. Mezi tyto technologie filtrování portů patří brány firewall, směrovače, proxy servery nebo protokol IPsec.

> [!NOTE]  
> Pokud podporujete internetové klienty pomocí přemostění SSL, může se kromě požadavků na porty taky u některých příkazů a hlaviček protokolu HTTP povolovat procházení branou firewall.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Porty, které můžete konfigurovat

Configuration Manager umožňuje konfigurovat porty pro následující typy komunikace:  

- Bod webu Katalog aplikací na bod služeb webu Katalog aplikací  

- Zprostředkující bod registrace s bodem registrace  

- Systémy klientů a lokalit, které spouštějí službu IIS  

- Klient s internetem (jako nastavení proxy server)  

- Bod aktualizace softwaru na Internet (jako nastavení proxy server)  

- Bod aktualizace softwaru se serverem WSUS  

- Server lokality se serverem databáze lokality  

- Server lokality k databázovému serveru WSUS

- Body služby Reporting services  

  > [!NOTE]  
  > Používané porty pro roli systému lokality bodu služby Reporting Services jsou konfigurovány v SQL Server Reporting Services. Tyto porty se pak při komunikaci s bodem služby Reporting Services používají Configuration Manager. Nezapomeňte si projít tyto porty definující informace filtru IP pro zásady protokolu IPsec nebo pro konfiguraci bran firewall.  

Ve výchozím nastavení je port HTTP, který se používá pro komunikaci mezi klientem a lokalitou, port 80 a výchozí port HTTPS je 443. Porty pro komunikaci klienta se systémem lokality přes protokol HTTP nebo HTTPS lze změnit během instalace nebo ve vlastnostech lokality pro váš Configuration Manager Web.  

Používané porty pro roli systému lokality bodu služby Reporting Services jsou konfigurovány v SQL Server Reporting Services. Tyto porty se pak při komunikaci s bodem služby Reporting Services používají Configuration Manager. Nezapomeňte tyto porty zkontrolovat, když definujete informace filtru IP pro zásady protokolu IPsec nebo pro konfiguraci bran firewall.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Nekonfigurovatelné porty  

Configuration Manager neumožňuje konfigurovat porty pro následující typy komunikace:  

- Site-to-Site  

- Server lokality se systémem lokality  

- Configuration Manager konzolu k poskytovateli serveru SMS  

- Configuration Manager konzolu k Internetu  

- Připojení ke cloudovým službám, jako jsou Microsoft Intune a distribuční body cloudu  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Porty používané klienty Configuration Manager a systémy lokality  

Následující části podrobně popisují porty používané pro komunikaci v Configuration Manager. Šipky v názvu oddílu zobrazují směr komunikace:  

- --> znamená, že jeden počítač spustí komunikaci a druhý počítač vždycky odpoví.  

- &lt;--> označuje, že počítač může zahájit komunikaci.  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Bod synchronizace funkce Asset Intelligence – > Microsoft  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Funkce Asset Intelligence bod synchronizace – > SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Bod webové služby Katalog aplikací--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Bod webu Katalog aplikací--> bod webové služby Katalog aplikací  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Klient--> bod webu Katalog aplikací  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Klient--> klient  

Proxy probuzení také používá zprávy s požadavkem na odezvu protokolu ICMP od jednoho klienta k jinému klientovi. Klienti používají tuto komunikaci k potvrzení, zda je jiný klient v síti zapnutý. ICMP se někdy označuje jako příkazy příkazu příkazového testu. Protokol ICMP nemá číslo protokolu UDP nebo TCP, takže není uveden v následující tabulce. Jakékoli brány firewall na těchto klientských počítačích nebo síťových zařízeních v rámci podsítě však musí povolit provoz protokolu ICMP, aby komunikace proxy probuzení mohla úspěšně probíhat.  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Funkce vzdáleného probuzení Wake On LAN|9 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|--|  
|Proxy probuzení|25536 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|--|  
|Všesměrové vysílání sdílené mezipaměti prostředí Windows PE|8004|--|  
|Stažení sdílené mezipaměti prostředí Windows PE|--|8003|  

Další informace najdete v tématu sdílená [mezipaměť prostředí Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> Klient--> Configuration Manager modul zásad služby zápisu síťových zařízení (NDES)

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Klient--> distribuční bod cloudu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Další informace najdete v tématu [porty a tok dat](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> Klient--> brána pro správu cloudu (CMG)  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Další informace najdete v tématu [CMG porty a tok dat](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> Klient--> distribuční bod, Standard i pull  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|
|Expresní aktualizace|--|8005 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Použijte nastavení klienta ke konfiguraci alternativního portu pro expresní aktualizace. Další informace najdete v tématu [port, který klienti používají pro příjem požadavků na rozdílový obsah](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content).

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> Klient-> distribuční bod konfigurovaný pro vícesměrové vysílání, Standard i pull  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Protokol vícesměrového vysílání|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> Klient-> distribuční bod konfigurovaný pro technologii PXE, Standard i pull  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 a 68|--|  
|NEJČASTĚJI|69 <sup> [Poznámka 4](#bkmk_note4)</sup> |--|  
|Protokol BINL (Boot Information Negotiation Layer)|4011|--|  

> [!Important]  
> Pokud povolíte bránu firewall založenou na hostiteli, ujistěte se, že pravidla umožňují serveru odesílat a přijímat na těchto portech. Pokud povolíte distribuční bod pro technologii PXE, Configuration Manager může povolit pravidla příchozího přenosu (Receive) v bráně Windows Firewall. Nekonfiguruje pravidla odchozího (Send).<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Klient--> bod stavu pro použití náhradní lokality  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Klient--> řadič domény globálního katalogu

Klient Configuration Manager nekontaktuje server globálního katalogu, pokud se jedná o počítač pracovní skupiny nebo pokud je nakonfigurovaný pro internetovou komunikaci.  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol LDAP globálního katalogu|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Klient--> bod správy  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Klientské oznámení (výchozí komunikace před návratem zpět k protokolu HTTP nebo HTTPS)|--|10123 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Klient--> bod aktualizace softwaru  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 nebo 8530 <sup> [Poznámka 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 nebo 8531 <sup> [Poznámka 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Klient--> bod migrace stavu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|SMB (Server Message Block)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> Bod připojení CMG--cloudová služba > CMG  

Configuration Manager pomocí těchto připojení sestaví kanál CMG. Další informace najdete v tématu [CMG porty a tok dat](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (upřednostňovaný)|--|10140-10155|  
|HTTPS (záloha s jedním virtuálním počítačem)|--|443|  
|HTTPS (záloha se dvěma nebo více virtuálními počítači)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> Bod připojení CMG – bod správy >  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Další informace najdete v tématu [CMG porty a tok dat](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> Bod připojení CMG--> bod aktualizace softwaru  

Konkrétní port závisí na konfiguraci bodu aktualizace softwaru.

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Další informace najdete v tématu [CMG porty a tok dat](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Konzola Configuration Manager – > klienta  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Vzdálené řízení (řízení)|--|2701|  
|Vzdálená pomoc (RDP a RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Konzola Configuration Manager – > Internet  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Konzola Configuration Manager používá přístup k Internetu pro následující akce:

- Stahování aktualizací softwaru z Microsoft Update pro balíčky pro nasazení.
- Položka zpětné vazby na pásu karet.
- Odkazy na dokumentaci v konzole nástroje.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Konzola Configuration Manager – bod > služby Reporting Services  

|Popis|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Konzola Configuration Manager – > serveru lokality  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (úvodní připojení k rozhraní WMI pro vyhledání systému poskytovatele)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Konzola Configuration Manager--> poskytovatele služby SMS  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager modul zásad služby zápisu síťových zařízení (NDES) – > bod registrace certifikátu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> Bod služby datového skladu – > SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> Distribuční bod, bod správy pro vyžádání obsahu Standard a >

Distribuční bod komunikuje s bodem správy v těchto scénářích:  

- Ohlášení stavu připraveného obsahu  

- K vytváření sestav o souhrnných datech o využití  

- K vytváření sestav o ověřování obsahu  

- Chcete-li ohlásit stav stahování balíčků (pouze distribuční bod pro vyžádání obsahu)

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection bod--> Internet  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection bod--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Zprostředkující bod registrace--> bod registrace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Bod registrace--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Konektor systému Exchange Server – > Exchange Online  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Vzdálená správa systému Windows v rámci protokolu HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Konektor systému Exchange Server--> místní Exchange Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Vzdálená správa systému Windows v rámci protokolu HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Počítač Mac – > zprostředkující bod registrace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Bod správy--> řadič domény  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol LDAP (Lightweight Directory Access Protocol)|389|389|  
|Protokol Secure LDAP (LDAPs, pro podepisování a vázání)|636|636|  
|Protokol LDAP globálního katalogu|--|3268|  
|Mapovač koncových bodů Endpoint Mapper RPC|--|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> Bod správy &lt; --> server lokality

<sup>[Poznámka 5](#bkmk_note5)</sup>

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Mapovač koncových bodů Endpoint Mapper RPC|--|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  
|SMB (Server Message Block)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Bod správy--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobilní zařízení--> zprostředkující bod registrace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Bod služby Reporting Services – > SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> Bod připojení služby – > Azure (CMG)  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol HTTPS pro nasazení služby CMG|--|443|

Další informace najdete v tématu [CMG porty a tok dat](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Server lokality &lt; -> bod webové služby Katalog aplikací  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Server lokality &lt; -> bod webu Katalog aplikací  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Server lokality &lt; --> funkce Asset Intelligence bod synchronizace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Server lokality--> klient  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Funkce vzdáleného probuzení Wake On LAN|9 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Server lokality--> distribuční bod cloudu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Další informace najdete v tématu [porty a tok dat](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> Server lokality – > distribuční bod, standardní i vyžádání

<sup>[Poznámka 5](#bkmk_note5)</sup>  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Server lokality--> řadič domény  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol LDAP (Lightweight Directory Access Protocol)|389|389|
|Protokol Secure LDAP (LDAPs, pro podepisování a vázání)|636|636|
|Protokol LDAP globálního katalogu|--|3268|  
|Mapovač koncových bodů Endpoint Mapper RPC|--|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Server lokality &lt; --> bod registrace certifikátu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> Server lokality &lt; --> bod připojení CMG

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Server lokality &lt; --> Endpoint Protection bod  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Server lokality &lt; --> bod registrace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Server lokality &lt; --> zprostředkující bod registrace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Server lokality &lt; --> bod stavu pro použití náhradní lokality

<sup>[Poznámka 5](#bkmk_note5)</sup>  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Server lokality--> Internet  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Server lokality &lt; --> vydávající certifikační autoritu (CA)

Tato komunikace se používá, pokud nasadíte profily certifikátů za použití bodu registrace certifikátu. Komunikace se nepoužívá pro všechny servery lokality v hierarchii. Místo toho se používá pouze pro server lokality v horní části hierarchie.  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC (DCOM)|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> Server lokality--> server hostující vzdálenou sdílenou knihovnu obsahu

Knihovnu obsahu můžete přesunout do jiného umístění úložiště a uvolnit tak místo na pevném disku na serverech centrální správy nebo primárních lokalit. Další informace najdete v tématu [Konfigurace vzdálené knihovny obsahu pro server lokality](the-content-library.md#bkmk_remote).

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> Server lokality &lt; – bod připojení služby >

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Server lokality &lt; --> bod služby Reporting Services

<sup>[Poznámka 5](#bkmk_note5)</sup>  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> Server lokality &lt; --> server lokality  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Server lokality--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

Během instalace lokality, která používá vzdálené SQL Server k hostování databáze lokality, otevřete následující porty mezi serverem lokality a SQL Server:  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> Server lokality--> SQL Server pro službu WSUS  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 3:](#bkmk_note3) alternativní port k dispozici</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Server lokality--> poskytovatel serveru SMS  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  
|RPC|--|Dynamická <sup> [Poznámka 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Server lokality &lt; --> bod aktualizace softwaru

<sup>[Poznámka 5](#bkmk_note5)</sup>  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|HTTP|--|80 nebo 8530 <sup> [Poznámka 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 nebo 8531 <sup> [Poznámka 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Server lokality &lt; – bod migrace stavu >

<sup>[Poznámka 5](#bkmk_note5)</sup>  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mapovač koncových bodů Endpoint Mapper RPC|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Poskytovatel služby SMS--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Bod aktualizace softwaru--> Internet  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Poznámka 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Bod aktualizace softwaru--> nadřazený server WSUS  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 nebo 8530 <sup> [Poznámka 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 nebo 8531 <sup> [Poznámka 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

Replikace databáze mezi lokalitami vyžaduje SQL Server v jedné lokalitě, aby komunikovala přímo s SQL Serverou v nadřazené nebo podřízené lokalitě.  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Služba SQL Server|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  
|Služba SQL Server Service Broker|--|4022 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

> [!TIP]  
> Configuration Manager nevyžaduje SQL Server Browser, který používá port UDP 1434.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Bod migrace stavu--> SQL Server  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 <sup> [Poznámka 2:](#bkmk_note2) alternativní port k dispozici</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Poznámky pro porty používané klienty nástroje Configuration Manager a systémy lokality  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> Poznámka 1: port proxy serveru

Tento port se nedá nakonfigurovat, ale dá se směrovat pomocí nakonfigurovaného proxy server.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> Poznámka 2: k dispozici je alternativní port

Pro tuto hodnotu můžete definovat alternativní port v Configuration Manager. Pokud definujete vlastní port, použijte tento vlastní port v informacích filtru IP pro zásady protokolu IPsec nebo nakonfigurujte brány firewall.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> Poznámka 3: Windows Server Update Services (WSUS)

Službu WSUS je možné nainstalovat pro použití portů 80/443 nebo 8530/8531 pro komunikaci klientů. Pokud spustíte službu WSUS v systému Windows Server 2012 nebo Windows Server 2016, služba WSUS je ve výchozím nastavení nakonfigurována tak, aby používala port 8530 pro protokol HTTP a port 8531 pro protokol HTTPS.  

Po instalaci můžete port změnit. V rámci hierarchie lokality nemusíte používat stejné číslo portu.  

- Jestliže port HTTP je 80, port HTTPS musí být 443.  

- Pokud je port HTTP cokoliv jiného, port HTTPS musí být 1 nebo vyšší, například 8530 a 8531.

    > [!NOTE]  
    >  Při konfiguraci bodu aktualizace softwaru pro použití protokolu HTTPS musí být port HTTP taky otevřený. Nešifrovaná data, například smlouva EULA pro konkrétní aktualizace, tento port HTTP používají.

- Webový server vytvoří připojení k SQL serveru, který je hostitelem služby SUSDB, pokud pro službu WSUS Cleanup povolíte následující možnosti:
  - Přidání neclusterovaných indexů do databáze WSUS za účelem zlepšení výkonu služby WSUS pro vyčištění
  - Odebrat zastaralé aktualizace z databáze WSUS
  
  Pokud se výchozí port SQL Server změní na alternativní port pomocí Configuration Manager SQL Server, ujistěte se, že se server lokality může připojit pomocí definovaného portu. Configuration Manager nepodporuje dynamické porty. Ve výchozím nastavení SQL Server pojmenované instance používají pro připojení k databázovému stroji dynamické porty. Pokud používáte pojmenovanou instanci, nakonfigurujte ručně statický port.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> Poznámka 4: démon protokolu TFTP (Trivial FTP)

Systémová služba démonu protokolu TFTP (Trivial FTP) nevyžaduje uživatelské jméno ani heslo a je nedílnou součástí služby WDS (Windows Deployment Services). Služba Trivial FTP démon implementuje podporu pro protokol TFTP definovaný následujícími specifikacemi RFC:  

- RFC 1350: TFTP  

- RFC 2347: rozšíření možnosti  

- RFC 2348: možnost velikosti bloku  

- RFC 2349: možnosti intervalu časového limitu a velikosti přenosu  

Protokol TFTP je navržený tak, aby podporoval prostředí pro spouštění bezdiskového prostředí. Démoni protokolu TFTP naslouchají na portu UDP 69, avšak odpovídají z dynamicky přiřazeného portu s vysokým číslem. Pokud povolíte tento port, může služba TFTP přijímat příchozí požadavky TFTP, ale vybraný server nemůže na tyto požadavky reagovat. Vybraný server nemůžete povolit, aby odpovídal na příchozí požadavky TFTP, pokud server TFTP nenastavíte tak, aby odpovídal z portu 69.  

Distribuční bod s povoleným PXE a klient v systému Windows PE vyberou dynamicky přidělené vysoké porty pro přenosy pomocí protokolu TFTP. Tyto porty definuje společnost Microsoft mezi 49152 a 65535. Další informace najdete v tématu [Přehled služeb a požadavky na síťové porty pro Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows) .

Během samotného spuštění PXE ale síťová karta na zařízení vybere dynamicky přidělený vysoký port, který používá během přenosu TFTP. Síťová karta v zařízení není vázaná na dynamicky přidělené vysoké porty definované Microsoftem. Je vázána pouze na porty definované v dokumentu RFC 1350. Tento port může být libovolný od 0 do 65535. Další informace o tom, co dynamicky přiděluje vysoké porty, používá síťová karta, získáte od výrobce hardwaru zařízení.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> Poznámka 5: komunikace mezi serverem lokality a systémy lokality

Ve výchozím nastavení je komunikace mezi serverem lokality nástroje a systémy lokality obousměrná. Server lokality spustí komunikaci s konfigurací systému lokality a pak se většina systémů lokalit připojí zpět k serveru lokality, aby odesílala informace o stavu. Body a distribuční body služby Reporting Services neodesílají informace o stavu. Pokud vyberete možnost **vyžadovat, aby server lokality inicializoval připojení k tomuto systému lokality** ve vlastnostech systému lokality po instalaci systému lokality, systém lokality nebude spouštět komunikaci se serverem lokality. Místo toho server lokality spustí komunikaci. Pro ověřování na server systému lokality používá účet instalace systému lokality.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> Poznámka 6: dynamické porty

Dynamické porty používají rozsah čísel portů, který je definovaný verzí operačního systému. Tyto porty se označují také jako dočasné porty. Další informace o výchozích rozsazích portů naleznete v části [Přehled služeb a požadavky na síťové porty pro systém Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Další seznamy portů  

Následující části poskytují další informace o portech, které Configuration Manager používá.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Sdílené složky klienta a serveru

Klienti používají protokol SMB (Server Message Block) kdykoli se připojí ke sdíleným složkám UNC. Příklad:

- Ruční instalace klienta, která určuje CCMSetup.exe **/Source:** vlastnost příkazového řádku  

- Endpoint Protection klienti, kteří stahují definiční soubory z cesty UNC

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Připojení k serveru Microsoft SQL Server

Pro komunikaci s databázovým strojem SQL Server a pro replikace mezi lokalitami můžete použít výchozí port serveru SQL Server nebo zadat vlastní porty:  

- Komunikace mezi lokalitami používá:  

  - Službu SQL Server Service Broker, kde je použit výchozí port TCP 4022.  

  - Služba SQL Server, která má výchozí port TCP 1433.  

- Komunikace mezi lokalitami mezi SQL Server databázovým strojem a různými Configuration Managermi rolemi systému lokality je standardně nastavená na port TCP 1433.  

- Configuration Manager používá stejné porty a protokoly ke komunikaci s každou replikou skupiny dostupnosti SQL, která je hostitelem databáze lokality, jako by byla replika samostatnou instancí SQL Server.

Pokud používáte Azure a databáze lokality je za interním nebo externím nástrojem pro vyrovnávání zatížení, nakonfigurujte následující komponenty:

- Výjimky brány firewall na každé replice
- Pravidla vyrovnávání zatížení

Nakonfigurujte následující porty:

- SQL přes TCP: TCP 1433
- SQL Server Service Broker: TCP 4022
- Protokol SMB (Server Message Block): TCP 445
- Mapovač koncových bodů RPC: TCP 135

> [!WARNING]  
> Configuration Manager nepodporuje dynamické porty. ve výchozím nastavení SQL Server pojmenované instance používají pro připojení k databázovému stroji dynamické porty. Při použití pojmenované instance ručně nakonfigurujte statický port pro komunikaci v rámci lokality.  

Následující role systému lokality komunikují přímo s databází SQL Server:  

- Bod služeb webu Katalog aplikací  

- Role bodu registrace certifikátu  

- Role bodu registrace  

- Bod správy  

- Server lokality  

- Bod služby Reporting services  

- poskytovatele serveru SMS  

- SQL Server--> SQL Server  

Pokud SQL Server hostuje databázi z více než jedné lokality, musí každá databáze používat samostatnou instanci SQL Server. Nakonfigurujte každou instanci s jedinečnou sadou portů.  

Pokud na SQL serveru povolíte bránu firewall založenou na hostiteli, nakonfigurujte ji tak, aby povolovala správné porty. Také Konfigurujte síťové brány firewall v mezi počítači, které komunikují s SQL serverem.  

Příklad konfigurace SQL Server pro použití konkrétního portu najdete v tématu [Konfigurace serveru pro naslouchání na specifickém portu TCP](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Zjišťování a publikování

Configuration Manager používá pro zjišťování a publikování informací o lokalitě následující porty:

- Protokol LDAP (Lightweight Directory Access Protocol): 389
- Protokol Secure LDAP (LDAPs, pro podepisování a vázání): 636
- LDAP globálního katalogu: 3268
- Mapovač koncových bodů RPC: 135
- RPC: dynamicky přidělené vysoké porty TCP
- TCP: 1024:5000
- TCP: 49152:65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Externí připojení vytvořená Configuration Manager

Místní Configuration Manager klienti nebo systémy lokality mohou provést následující externí připojení:  

- [Bod synchronizace funkce Asset Intelligence – &gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection Point-- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Klient – &gt; řadič domény globálního katalogu](#BKMK_PortsClient-GCDC)  

- [Konzola Configuration Manager – &gt; Internet](#BKMK_PortsConsole-Internet)  

- [Bod správy-- &gt; řadič domény](#BKMK_PortsMP-DC)  

- [Server lokality – &gt; řadič domény](#BKMK_PortsSite-DC)  

- [Server lokality &lt;  -- &gt; vydávající certifikační autoritu (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [Bod aktualizace softwaru-- &gt; Internet](#BKMK_PortsSUP-Internet)  

- [Bod aktualizace softwaru – &gt; nadřazený server WSUS](#BKMK_PortsSUP-WSUS)  

- [Bod připojení služby – > Azure](#bkmk_scp-cmg)  

- [Bod připojení CMG--cloudová služba > CMG](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Požadavky na instalaci pro systémy lokality, které podporují internetové klienty

> [!Note]  
> Tato část platí jenom pro internetovou správu klientů (IBCM). Neplatí to pro bránu pro správu cloudu. Další informace najdete v tématu [Správa klientů na internetu](../../clients/manage/manage-clients-internet.md).  

Internetové body správy, distribuční body, které podporují internetové klienty, bod aktualizace softwaru a bod záložního stavu, používají pro instalaci a opravu následující porty:  

- Server lokality--> systém lokality: Mapovač koncových bodů RPC pomocí protokolu UDP a TCP port 135.  

- Server lokality--> systém lokality: dynamické porty TCP protokolu RPC  

- Server lokality &lt; --> systém lokality: SMB (Server Message Blocks) pomocí portu TCP 445

Instalace aplikací a balíčků v distribučních bodech vyžadují následující porty RPC:  

- Server lokality--> distribuční bod: Mapovač koncových bodů RPC pomocí protokolu UDP a portu TCP 135

- Server lokality--> distribuční bod: dynamické porty TCP služby RPC  

K zajištění přenosu mezi serverem lokality a systémy lokality použijte protokol IPsec. Pokud musíte omezit dynamické porty, které se používají s RPC, můžete použít konfigurační nástroj Microsoft RPC (rpccfg.exe). Pomocí tohoto nástroje můžete nakonfigurovat omezený rozsah portů pro tyto pakety RPC. Další informace najdete v tématu [Postup konfigurace RPC pro použití určitých portů a postup při zabezpečení těchto portů pomocí protokolu IPSec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Před instalací těchto systémů lokality zajistěte, aby na serveru systému lokality byla spuštěna služba Remote Registry Service a zda jste zadali účet instalace systému lokality, pokud je systém lokality v jiné doménové struktuře služby Active Directory bez důvěryhodného vztahu. Například služba Remote Registry se používá na serverech, na kterých běží systémy lokality, jako jsou distribuční body (vyžádání a standardní), vzdálené servery SQL a katalog aplikací.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Porty používané při instalaci klienta Configuration Manager

Porty, které Configuration Manager používá během instalace klienta, závisí na metodě nasazení.

- Seznam portů pro jednotlivé metody nasazení klientů najdete v tématu [porty používané během Configuration Manager nasazení klienta](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment) .  

- Další informace o tom, jak nakonfigurovat bránu Windows Firewall na klientovi pro instalaci klienta a komunikaci po instalaci, najdete v tématu [nastavení brány Windows Firewall a portů pro klienty](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md) .  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Porty používané migrací

Server lokality, na kterém běží migrace, používá několik portů pro připojení k příslušným lokalitám ve zdrojové hierarchii. Další informace najdete v tématu [požadované konfigurace pro migraci](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Porty používané Windows serverem

Následující tabulka uvádí některé z klíčových portů používaných Windows serverem.

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 a 68|--|  
|Překlad adresy rozhraní NetBIOS|137|--|  
|Služba datagramu rozhraní NetBIOS|138|--|  
|Služba relace rozhraní NetBIOS|--|139|  
|Ověřování protokolu Kerberos|--|88|

Další informace najdete v následujících článcích:

- [Přehled služeb a požadavky na síťové porty pro systém Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Jak nakonfigurovat bránu firewall pro domény a vztahy důvěryhodnosti](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)