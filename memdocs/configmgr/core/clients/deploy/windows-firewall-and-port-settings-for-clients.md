---
title: Nastavení portů a brány firewall klienta Windows
titleSuffix: Configuration Manager
description: Vyberte možnost Brána Windows Firewall a nastavení portů pro klienty v nástroji Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713965"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Nastavení brány Windows Firewall a portů pro klienty v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Klientské počítače v Configuration Manager, které používají bránu Windows Firewall, často vyžadují, abyste nakonfigurovali výjimky, které umožňují komunikaci s jejich lokalitou. Výjimky, které je nutné nakonfigurovat, závisí na funkcích správy, které používáte s klientem Configuration Manager.  

 Následující části vám umožní zjistit tyto funkce správy a získat další informace o konfiguraci těchto výjimek v bráně Windows Firewall.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Změna nastavení portů a programů povolených bránou Windows Firewall  
 K úpravě portů a programů v bráně Windows Firewall pro Configuration Manager klienta použijte následující postup.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Změna nastavení portů a programů povolených bránou Windows Firewall  

1.  V počítači používajícím bránu Windows Firewall otevřete část Ovládací panely.  

2.  Klikněte pravým tlačítkem na položku **Brána Windows Firewall**a poté klikněte na tlačítko **Otevřít**.  

3.  Nakonfigurujte jakékoli vyžadované výjimky a vlastní programy a porty.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programy a porty vyžadované nástrojem Configuration Manager  
 Následující funkce Configuration Manager vyžadují výjimky v bráně Windows Firewall:  

### <a name="queries"></a>Dotazy  
 Spouštíte-li konzolu Configuration Manager v počítači se systémem Windows Firewall, dotazy selžou při prvním spuštění a operační systém zobrazí dialogové okno s dotazem, zda chcete odblokovat soubor statview. exe. Pokud odblokujete soubor statview.exe, budoucí dotazy se spustí bez chyb. Před spuštěním dotazu lze na kartě **Výjimky** brány Windows Firewall také přidat soubor Statview.exe do seznamu programů a služeb ručně.  

### <a name="client-push-installation"></a>Klientská nabízená instalace  
 Chcete-li použít klientskou nabízenou instalaci k instalaci klienta Configuration Manager, přidejte následující jako výjimky do brány Windows Firewall:  

-   Odchozí a příchozí: **Sdílení souborů a tiskáren**  

-   Příchozí: **Služba WMI (Windows Management Instrumentation)**  

### <a name="client-installation-by-using-group-policy"></a>Instalace klienta pomocí zásad skupiny  
 Chcete-li použít Zásady skupiny k instalaci klienta Configuration Manager, přidejte jako výjimku do brány Windows Firewall **sdílení souborů a tiskáren** .  

### <a name="client-requests"></a>Požadavky klientů  
 Aby klientské počítače komunikovaly se systémy Configuration Manager lokality, přidejte následující jako výjimky do brány Windows Firewall:  

 Odchozí: Port TCP **80** (pro komunikaci protokolem HTTP)  

 Odchozí: Port TCP **443** (pro komunikaci protokolem HTTPS)  

> [!IMPORTANT]  
>  Toto jsou výchozí čísla portů, která lze změnit v Configuration Manager. Další informace najdete v tématu Postup [Konfigurace portů pro komunikaci klientů](../../../core/clients/deploy/configure-client-communication-ports.md). Pokud jsou změněny výchozí hodnoty těchto portů, je nutné také nakonfigurovat odpovídající výjimky v bráně Windows Firewall.  

### <a name="client-notification"></a>Klientské oznámení  
 Aby bod správy informoval klientské počítače o akci, kterou musí provést v případě, že uživatel vybere akci klienta v konzole Configuration Manager, jako je například stažení zásady počítače nebo zahájení prohledávání malwaru, přidejte následující příkaz jako výjimku do brány Windows Firewall:  

 Odchozí: Port TCP **10123**  

 Pokud tato komunikace není úspěšná, Configuration Manager se automaticky vrátí k používání existujícího portu pro komunikaci klienta s bodem správy protokolu HTTP nebo HTTPS:  

 Odchozí: Port TCP **80** (pro komunikaci protokolem HTTP)  

 Odchozí: Port TCP **443** (pro komunikaci protokolem HTTPS)  

> [!IMPORTANT]  
>  Toto jsou výchozí čísla portů, která lze změnit v Configuration Manager. Další informace najdete v tématu [Konfigurace portů pro komunikaci klientů](../../../core/clients/deploy/configure-client-communication-ports.md). Pokud jsou změněny výchozí hodnoty těchto portů, je nutné také nakonfigurovat odpovídající výjimky v bráně Windows Firewall.  

### <a name="remote-control"></a>Vzdálené řízení  
 Pokud chcete použít Configuration Manager vzdálené řízení, povolte následující port:  

-   Příchozí: port TCP **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Funkce Vzdálená pomoc a Vzdálená plocha  
 Chcete-li spustit vzdálenou pomoc z konzoly Configuration Manager, přidejte vlastní program **Helpsvc. exe** a příchozí vlastní port TCP **135** do seznamu povolených programů a služeb v bráně Windows Firewall v klientském počítači. Je také nutné povolit funkci **Vzdálená pomoc** a **Vzdálená plocha**. Pokud spustíte funkci Vzdálená pomoc z klientského počítače, brána Windows Firewall automaticky nakonfiguruje a povolí funkci **Vzdálená pomoc** a **Vzdálená plocha**.  

### <a name="wake-up-proxy"></a>Proxy probuzení  
 Pokud povolíte nastavení proxy probuzení v klientovi, použije nová služba s názvem Proxy probuzení nástroje ConfigMgr protokol peer-to-peer, aby zkontrolovala, zda běží ostatní počítače v podsíti, a aby je v případě potřeby probudila. Tato komunikace používá následující porty:  

 Odchozí: Port UDP **25536**  

 Odchozí: Port UDP **9**  

 Toto jsou výchozí čísla portů, která lze změnit v Configuration Manager pomocí nastavení klientů **řízení spotřeby** pro **číslo portu proxy probuzení (UDP)** a **číslo portu Wake on LAN (UDP)**. Pokud zadáte nastavení klienta **Řízení spotřeby**: **Výjimka brány Windows Firewall pro proxy probuzení** , tyto porty se automaticky nakonfigurují v bráně Windows Firewall pro klienty. Pokud však klienti používají jinou bránu firewall, je nutné nakonfigurovat výjimky pro tato čísla portů ručně.  

 Proxy probuzení používá kromě těchto portů také žádosti o odezvu protokolu ICMP (Internet Control Message Protocol) od jednoho klientského počítače do jiného klientského počítače. Tato komunikace se používá pro potvrzení, zda počítač jiného klienta běží na síti. ICMP se někdy označuje příkazy ping TCP/IP.  

 Další informace o proxy probuzení najdete v tématu [plánování probuzení klientů](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Nástroj Prohlížeč událostí systému Windows, Monitor výkonu systému Windows a Diagnostika systému Windows  
 Chcete-li získat přístup k Windows Prohlížeč událostí, sledování výkonu systému Windows a Diagnostika systému Windows z konzoly Configuration Manager, povolte **sdílení souborů a tiskáren** jako výjimku v bráně Windows Firewall.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Porty používané během nasazení klienta nástroje Configuration Manager  
 Následující tabulky uvádí porty, které se používají během instalace klienta.  

> [!IMPORTANT]  
>  Pokud je mezi servery systému lokality a klientským počítačem brána firewall, potvrďte, zda brána firewall povolí provoz pro porty, které jsou vyžadovány pro vybranou metodu instalace klienta. Brány firewall například často zamezí úspěšné klientské nabízené instalaci, protože blokují protokol SMB (Server Message Block) a RPC (Remote Procedure Calls). V případě tohoto scénáře použijte odlišnou metodu instalace klienta, například ruční instalaci (spuštěním souboru CCMSetup.exe) nebo instalaci klienta na základě zásad skupiny. Tyto alternativní metody instalace klienta nevyžadují protokol SMB ani RPC.  

 Informace o konfiguraci brány Windows Firewall v klientském počítači naleznete v části [Změna nastavení portů a programů povolených bránou Windows Firewall](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Porty používané pro všechny metody instalace  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol HTTP (Hypertext Transfer Protocol) od klientského počítače do bodu záložního stavu, pokud je ke klientovi přiřazen bod záložního stavu.|--|80 (viz poznámku 1, **Alternativní port dostupný**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Porty používané při klientské nabízené instalaci  
 Kromě portů uvedených v následující tabulce používá klientská nabízená instalace také žádosti o odezvu protokolu ICMP (Internet Control Message Protocol) od serveru lokality do klientského počítače pro potvrzení, zda je klientský počítač dostupný na síti. ICMP se někdy označuje příkazy ping TCP/IP. ICMP nemá číslo protokolu UDP nebo TCP, proto není v následující tabulce uveden. Jakákoli síťová zařízení, například brány firewall, však musí povolit provoz protokolu ICMP, aby klientská nabízená instalace mohla úspěšně probíhat.  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol SMB (Server Message Block) mezi serverem lokality a klientským počítačem|--|445|  
|Mapovač koncových bodů protokolu RPC mezi serverem lokality a klientským počítačem|135|135|  
|Dynamické porty RPC mezi serverem lokality a klientským počítačem|--|DYNAMIC|  
|Protokol HTTP (Hypertext Transfer Protocol) od klientského počítače do bodu správy v případě připojení prostřednictvím protokolu HTTP|--|80 (viz poznámku 1, **Alternativní port dostupný**)|  
|Protokol HTTPS (Secure Hypertext Transfer Protocol) od klientského počítače do bodu správy v případě připojení prostřednictvím protokolu HTTPS|--|443 (viz poznámku 1, **Alternativní port dostupný**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Porty používané při instalaci aktualizace softwaru z bodu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol HTTP (Hypertext Transfer Protocol) od klientského počítače do bodu aktualizace softwaru|--|80 nebo 8530 (viz poznámku 2, **Služba Windows Server Update Services**)|  
|Protokol HTTPS (Secure Hypertext Transfer Protocol) od klientského počítače do bodu aktualizace softwaru|--|443 nebo 8531 (viz poznámku 2, **Služba Windows Server Update Services**)|  
|Protokol SMB (Server Message Block) mezi zdrojovým serverem a klientským počítačem při zadání vlastnosti příkazového řádku CCMSetup **/Source:&lt;Path\>**.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Porty používané při instalaci na základě zásad skupiny  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol HTTP (Hypertext Transfer Protocol) od klientského počítače do bodu správy v případě připojení prostřednictvím protokolu HTTP|--|80 (viz poznámku 1, **Alternativní port dostupný**)|  
|Protokol HTTPS (Secure Hypertext Transfer Protocol) od klientského počítače do bodu správy v případě připojení prostřednictvím protokolu HTTPS|--|443 (viz poznámku 1, **Alternativní port dostupný**)|  
|Protokol SMB (Server Message Block) mezi zdrojovým serverem a klientským počítačem při zadání vlastnosti příkazového řádku CCMSetup **/Source:&lt;Path\>**.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Porty používané při ruční instalaci a instalaci na základě přihlašovacího skriptu  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol SMB (Server Message Block) mezi klientským počítačem a sdílenou síťovou složkou, ze které lze spustit soubor CCMSetup.exe.<br /><br /> Při instalaci Configuration Manager se zdrojové soubory instalace klienta zkopírují a automaticky sdílejí ze složky * &lt;InstallationPath\>* \Client v bodech správy. Tyto soubory však můžete zkopírovat a můžete vytvořit novou sdílenou složku v jakémkoli počítači v síti. Případně můžete omezit tento síťový provoz místním spuštěním souboru CCMSetup.exe, například pomocí vyměnitelného média.|--|445|  
|Protokol HTTP (Hypertext Transfer Protocol) od klientského počítače do bodu správy v případě připojení prostřednictvím protokolu HTTP a nezadáte vlastnost příkazového řádku služby CCMSetup **/Source:&lt;Path\>**.|--|80 (viz poznámku 1, **Alternativní port dostupný**)|  
|Protokol HTTPS (Secure Hypertext Transfer Protocol) od klientského počítače do bodu správy v případě připojení prostřednictvím protokolu HTTPS, a pokud nezadáte vlastnost příkazového řádku služby CCMSetup **/Source:&lt;Path\>**.|--|443 (viz poznámku 1, **Alternativní port dostupný**)|  
|Protokol SMB (Server Message Block) mezi zdrojovým serverem a klientským počítačem při zadání vlastnosti příkazového řádku CCMSetup **/Source:&lt;Path\>**.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Porty používané při instalaci na základě distribuce softwaru  

|Popis|UDP|TCP|  
|-----------------|---------|---------|  
|Protokol SMB (Server Message Block) mezi distribučním bodem a klientským počítačem|--|445|  
|Protokol HTTP (Hypertext Transfer Protocol) od klienta do distribučního bodu v případě připojení prostřednictvím protokolu HTTP|--|80 (viz poznámku 1, **Alternativní port dostupný**)|  
|Protokol HTTPS (Secure Hypertext Transfer Protocol) od klienta do distribučního bodu v případě připojení prostřednictvím protokolu HTTPS|--|443 (viz poznámku 1, **Alternativní port dostupný**)|  

## <a name="notes"></a>Poznámky  
 **k dispozici je 1 alternativní port** . V Configuration Manager můžete pro tuto hodnotu definovat alternativní port. Jestliže byl nadefinován vlastní port, dosaďte tento vlastní port při definování informací IP filtru pro zásady protokolu IPsec nebo pro konfigurování bran firewall.  

 **2 Služba Windows Server Update Services** Službu WSUS (Windows Server Update Service) lze instalovat buď na výchozí web (port 80), nebo na vlastní web (port 8530).  

 Po instalaci můžete port změnit. Nemusíte používat stejné číslo portu v celé hierarchii webu.  

 Jestliže port HTTP je 80, port HTTPS musí být 443.  

 Pokud je port HTTP něco jiného, port HTTPS musí být o 1 vyšší. Například 8530 a 8531.
