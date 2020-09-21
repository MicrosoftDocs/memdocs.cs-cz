---
title: Referenční informace k protokolům
titleSuffix: Configuration Manager
description: Odkaz na všechny soubory protokolu pro Configuration Manager klienta, server a závislé součásti.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa473d15b5abfbab7049a1e822a890d76aee239b
ms.sourcegitcommit: 81f6b4cac6c991d34bc864f950c82e5b57e906c3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90779545"
---
# <a name="log-file-reference"></a>Referenční informace k protokolům

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager komponenty klienta a webového serveru zaznamenávají informace o procesu do jednotlivých souborů protokolu. Informace v těchto protokolových souborech vám můžou pomoct při řešení problémů, ke kterým může dojít. Ve výchozím nastavení Configuration Manager povolí protokolování pro klientské a serverové součásti.

Obecnější informace o souborech protokolu v Configuration Manager najdete v tématu [informace o souborech protokolu](about-log-files.md). Tento článek obsahuje informace o nástrojích, které se mají použít, jak nakonfigurovat protokoly a kde je najít.

Následující části obsahují podrobné informace o různých souborech protokolů, které máte k dispozici. Monitorování Configuration Manager protokolů klienta a serveru pro podrobnosti o operacích a zobrazení informací o chybách k řešení problémů.  

- [Soubory protokolů klienta](#BKMK_ClientLogs)  

  - [Klientské operace](#BKMK_ClientOpLogs)  

  - [Instalace klienta](#BKMK_ClientInstallLog)  

  - [Klient operačních systémů Linux a UNIX](#BKMK_LogFilesforLnU)  

  - [Klient pro počítače Mac](#BKMK_LogfilesforMac)  

- [Soubory protokolu serveru](#BKMK_ServerLogs)  

  - [Server lokality a systémy lokality](#BKMK_SiteSiteServerLog)  

  - [Instalace serveru lokality](#BKMK_SiteInstallLog)

  - [Bod služby datového skladu](#BKMK_DataWarehouse)

  - [Bod záložního stavu](#BKMK_FSPLog)  

  - [Bod správy](#BKMK_MPLog)  

  - [Bod připojení služby](#BKMK_WITLog)  

  - [Bod aktualizace softwaru](#BKMK_SUPLog)  

- [Soubory protokolu podle funkcí](#BKMK_FunctionLogs)  

  - [Správa aplikací](#BKMK_AppManageLog)  

  - [Funkce Asset Intelligence](#BKMK_AILog)  

  - [Backup a obnovení](#BKMK_BnRLog)  

  - [Zápis certifikátu](#BKMK_CertificateEnrollment)

  - [Klientské oznámení](#BKMK_BGB)

  - [Brána pro správu cloudu](#cloud-management-gateway)

  - [Nastavení dodržování předpisů a přístup k prostředkům společnosti](#BKMK_CompSettingsLog)  

  - [Konzola Configuration Manager](#BKMK_ConsoleLog)  

  - [Správa obsahu](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Rozpoznávání](#BKMK_DiscoveryLog)  

  - [Analýza koncového bodu](#bkmk_analytics)
  
  - [Endpoint Protection](#BKMK_EPLog)  

  - [Rozšíření](#BKMK_Extensions)  

  - [Inventář](#BKMK_InventoryLog)  

  - [Migrace](#BKMK_MigrationLog)  

  - [Mobilní zařízení](#BKMK_MDMLog)  

  - [Nasazení operačního systému](#BKMK_OSDLog)  

  - [Řízení spotřeby](#BKMK_PowerMgmtLog)  

  - [Vzdálené řízení](#BKMK_RCLog)  

  - [Generování sestav](#BKMK_ReportLog)  

  - [Správa na základě rolí](#BKMK_RBALog)  

  - [Monitorování míry využití softwaru](#BKMK_MeteringLog)  

  - [Aktualizace softwaru](#BKMK_SU_NAPLog)  

  - [Funkce vzdáleného probuzení Wake On LAN](#BKMK_WOLLog)  

  - [Údržba Windows 10](#BKMK_WindowsServicingLog)

  - [Windows Update Agent](#BKMK_WULog)  

  - [Server WSUS](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a> Soubory protokolů klienta

V následujících oddílech jsou uvedeny soubory protokolu týkající se operací klienta a instalace klienta.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a> Klientské operace

Následující tabulka uvádí soubory protokolů, které se nacházejí v klientovi Configuration Manager.  

|Název protokolu|Popis|  
|--------------|-----------------|  
|ADALOperationProvider. log|Informace o požadavcích tokenu ověřování klienta s Azure Active Directory (služba Azure AD) Authentication Library (ADAL).|
|BitLockerManagementHandler. log|Zaznamenává informace o zásadách správy BitLockeru.|
|CAS.log|Služba Content Access. Spravuje místní mezipaměť balíčků na klientovi.|  
|Ccm32BitLauncher.log|Zaznamenává akce spouštění aplikací na klientovi označené *jako bit Run as 32*.|  
|CcmEval.log|Zaznamenává aktivity hodnocení stavu klienta Configuration Manager a podrobnosti pro součásti, které jsou vyžadovány klientem Configuration Manager.|  
|CcmEvalTask.log|Zaznamenává Configuration Manager aktivity hodnocení stavu klienta, které jsou iniciovány naplánovanou úlohou vyhodnocení.|  
|CcmExec.log|Zaznamenává činnosti klienta a služby SMS Agent Host. Tento protokolový soubor zahrnuje taky informace o povolování a zakazování proxy probuzení.|  
|CcmMessaging.log|Zaznamenává činnosti související s komunikací mezi klientem a body správy.|  
|CCMNotificationAgent.log|Zaznamenává činnosti týkající se oznamovacích operací klienta.|  
|Ccmperf.log|Zaznamenává činnosti týkající se správy a sběru dat v závislosti na čítačích výkonu klienta.|  
|CcmRestart.log|Zaznamenává činnost restartování služby klienta.|  
|CCMSDKProvider.log|Zaznamenává činnosti rozhraní SDK klienta.|  
|ccmsqlce. log|Zaznamenává činnosti pro SQL Compact Edition, které klient používá. Tento protokol se obvykle používá pouze v případě, že povolíte protokolování ladění, nebo dojde k potížím s komponentou. Úloha stavu klienta (ccmeval) obvykle opravuje problémy s touto součástí.|
|CertificateMaintenance.log|Spravuje certifikáty služby Active Directory Domain Services a bodů správy.|  
|CIDownloader.log|Zaznamenává údaje o stahování definicí položek konfigurace.|  
|CITaskMgr.log|Zaznamenává úlohy pro jednotlivé typy aplikací a nasazení, jako je například stažení obsahu a akce instalace nebo odinstalace.|  
|ClientAuth.log|Zaznamenává aktivitu podepisování a ověřování pro klienta.|  
|ClientIDManagerStartup.log|Vytvoří a udržuje identifikátor GUID klienta a identifikuje úlohy během registrace a přiřazování klienta.|  
|ClientLocation.log|Zaznamenává úlohy, které se týkají přiřazení lokality klienta.|  
|CMHttpsReadiness.log|Zaznamenává výsledky spuštění nástroje pro vyhodnocení připravenosti HTTPS Configuration Manager. Tento nástroj kontroluje, jestli počítače mají certifikát ověřování klienta infrastruktury veřejných klíčů (PKI), který se dá použít s Configuration Manager.|  
|CmRcService.log|Zaznamenává informace pro službu vzdáleného řízení.|  
|CoManagementHandler. log|Použijte k řešení potíží spolusprávy na klientovi.|
|ContentTransferManager.log|Naplánuje Background Intelligent Transfer Service (BITS) nebo protokol SMB (Server Message Block) ke stažení nebo přístupu k balíčkům.|  
|DataTransferService.log|Zaznamenává veškerou komunikaci služby BITS pro přístup k zásadám nebo balíčkům.|  
|DeltaDownload. log|Zaznamenává informace o stažení expresních aktualizací a aktualizací stažených pomocí optimalizace doručování.|  
|Diagnostika. log|Zaznamenává stav akcí diagnostiky klienta.|
|EndpointProtectionAgent|Zaznamenává informace o instalaci klienta System Center Endpoint Protection a o použití antimalwarových zásad do tohoto klienta.|  
|execmgr.log|Zaznamenává údaje o balíčcích a sekvencích úloh, které se spouští na klientovi.|  
|ExpressionSolver.log|Zaznamenává údaje o rozšířených detekčních metodách, které se používají, když je zapnuté podrobné protokolování nebo protokolování ladění.|  
|ExternalEventAgent.log|Zaznamenává historii detekce malware ochrany koncového bodu Endpoint Protection a událostí týkajících se stavu klienta.|  
|FileBITS.log|Zaznamenává všechny úlohy zpřístupnění balíčků SMB.|  
|FileSystemFile.log|Zaznamenává činnost poskytovatele služby Windows Management Instrumentation (WMI) pro inventář softwaru a kolekci souborů.|  
|FSPStateMessage.log|Zaznamenává činnost pro stavové zprávy, které klient zasílá do záložního stavového bodu.|  
|InternetProxy.log|Zaznamenává konfiguraci a aktivitu použití sítě proxy serveru pro klienta.|  
|InventoryAgent.log|Zaznamenává činnosti inventáře hardwaru, inventáře softwaru a akce zjišťování prezenčního signálu na klientovi.|  
|LocationCache.log|Zaznamenává aktivitu pro použití a údržbu mezipaměti umístění pro klienta.|  
|LocationServices.log|Zaznamenává činnost klienta týkající se umísťování bodů správy, bodů aktualizací softwaru a distribučních bodů.|  
|M365AHandler. log|Informace o zásadách nastavení pro Desktop Analytics|
|MaintenanceCoordinator.log|Zaznamenává aktivitu pro úlohy obecné údržby pro klienta.|  
|Mifprovider.log|Zaznamenává činnost zprostředkovatele rozhraní WMI pro soubory MIF (Management Information Format).|  
|mtrmgr.log|Monitoruje všechny procesy kontroly softwaru.|  
|PolicyAgent.log|Zaznamenává požadavky na zásady vytvořené pomocí služby Přenos dat.|  
|PolicyAgentProvider.log|Zaznamenává změny zásad.|  
|PolicyEvaluator.log|Zaznamenává údaje o vyhodnocení zásad na klientských počítačích, včetně zásad z aktualizací softwaru.|  
|PolicyPlatformClient.log|Zaznamenává proces nápravy a dodržování předpisů pro všechny poskytovatele umístěné ve složce \Program Files\Microsoft Policy Platform s výjimkou poskytovatele souboru.|  
|PolicySdk.log|Zaznamenává činnosti rozhraní služby SDK systému zásad.|  
|Pwrmgmt.log|Zaznamenává informace o povolování nebo zakazování a konfigurování nastavení klienta pro proxy probuzení.|  
|PwrProvider.log|Zaznamenává činnosti poskytovatele řízení spotřeby (PWRInvProvider) hostovaného ve službě WMI. Na všech podporovaných verzích Windows poskytovatel uvádí aktuální nastavení na počítačích během inventáře hardwaru a používá nastavení plánu výkonu.|  
|SCClient_ &lt; *doména* \> @ &lt; *username* \> _1. log|Zaznamenává činnost centra softwaru pro určeného uživatele na klientském počítači.|  
|SCClient_ &lt; *doména* \> @ &lt; *username* \> _2. log|Zaznamenává historickou činnost centra softwaru pro určeného uživatele na klientském počítači.|  
|Scheduler.log|Zaznamenává činnosti plánovaných úloh pro všechny operace klienta.|  
|SCNotify_ &lt; *doména* \> @ &lt; *username* \> _1. log|Zaznamenává činnost oznamujících uživatelů o softwaru pro určeného uživatele.|  
|SCNotify_ &lt; *doména* \> @ &lt; *username* \> _1- &lt; *date_time*>. log|Zaznamenává historické informace oznamujících uživatelů o softwaru pro určeného uživatele.|
|SensorWmiProvider. log|Zaznamenává činnost zprostředkovatele rozhraní WMI pro senzor služby Endpoint Analytics.|
|SensorEndpoint. log|Zaznamenává spuštění zásad služby Endpoint Analytics a odeslání klientských dat na server lokality.|
|SensorManagedProvider. log|Zaznamenává shromažďování a zpracování událostí a informací pro službu Endpoint Analytics.|
|setuppolicyevaluator.log|Zaznamenává konfiguraci a vytváření zásad inventáře ve službě WMI.|  
|&lt;*Doména* SleepAgent_\>@SYSTEM_0.log|Hlavní protokolový soubor pro proxy probuzení.|  
|smscliui.log|Zaznamenává použití klienta Configuration Manager v Ovládacích panelech.|  
|SrcUpdateMgr.log|Zaznamenává činnost nainstalovaných aplikací instalační služby systému Windows, které jsou aktualizované pomocí aktuálních zdrojových umístění distribučních bodů.|  
|StatusAgent.log|Zaznamenává stavové zprávy, které vytváří součásti klienta.|  
|SWMTRReportGen.log|Vygeneruje sestavu použití dat, která je shromažďována agentem měření. Tato data se protokolují v souboru Mtrmgr.log.|  
|UserAffinity.log|Zaznamenává údaje o spřažení uživatelských zařízení.|  
|VirtualApp.log|Zaznamenává informace specifické pro vyhodnocení typů nasazení Application Virtualization (App-V).|  
|Wedmtrace.log|Zaznamenává operace týkající se filtrů zápisu na klientech operačního systému Windows Embedded.|  
|wakeprxy-install.log|Zaznamenává informace o instalaci, když klienti obdrží možnost nastavení klienta zapnout proxy probuzení.|  
|wakeprxy-uninstall.log|Zaznamenává informace o odinstalování proxy probuzení, když klienti obdrží možnost nastavení klienta pro vypnutí proxy probuzení, pokud byl proxy probuzení dříve zapnutý.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a> Instalace klienta

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se instalace klienta Configuration Manager.  

|Název protokolu|Popis|  
|--------------|-----------------|  
|ccmsetup.log|Zaznamenává úlohy ccmsetup.exe pro instalaci klienta, upgrade klienta a odebrání klienta. Dá se použít k odstraňování problémů instalace klienta.|  
|ccmsetup-ccmeval.log|Zaznamenává úlohy ccmsetup.exe pro stav a nápravu klienta.|  
|CcmRepair.log|Zaznamenává činnosti oprav agenta klienta.|  
|client.msi.log|Zaznamenává úlohy instalace, které provádí client.msi. Lze použít k odstraňování problémů instalace nebo odebrání klienta.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Klient pro systémy Linux a UNIX

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX.
>
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Klient Configuration Manager pro systémy Linux a UNIX zaznamenává informace v následujících protokolových souborech:  

> [!TIP]
> Použijte CMTrace k zobrazení souborů protokolu pro klienta nástroje pro Linux a UNIX.

|Název protokolu|Podrobnosti|
|-------------------|-----------------------------------------------------------------|
|Scxcm. log| Soubor protokolu pro základní službu klienta Configuration Manager pro systémy Linux a UNIX (Ccmexec. bin). Tento protokolový soubor obsahuje informace o instalaci a probíhajících operacích souboru ccmexec.bin. Ve výchozím nastavení se tento soubor protokolu nachází na adrese **/var/opt/Microsoft/scxcm.log**. Pokud chcete změnit umístění souboru protokolu, upravte **/opt/microsoft/configmgr/etc/scxcm.conf** a změňte pole **CESTA**. Aby se změna projevila, nemusíte restartovat klientský počítač ani službu. Úroveň protokolu můžete nastavit na jedno ze čtyř různých nastavení. |
| Scxcmprovider. log |Soubor protokolu pro službu CIM klienta Configuration Manager pro systémy Linux a UNIX (omiserver. bin). Tento protokolový soubor obsahuje informace o probíhajících operacích souboru nwserver.bin. Tento protokol je umístěný na adrese `/var/opt/microsoft/configmgr/scxcmprovider.log` . Pokud chcete změnit umístění souboru protokolu, upravte **/opt/microsoft/omi/etc/scxcmprovider.conf** a změňte pole **CESTA**. Aby se změna projevila, nemusíte restartovat klientský počítač ani službu. Úroveň protokolu můžete nastavit na jedno ze tří nastavení.|

Oba soubory protokolu podporují několik úrovní protokolování:  

- **scxcm. log**. Pokud chcete změnit úroveň protokolu, upravte **/opt/Microsoft/ConfigMgr/etc/scxcm.conf** a změňte každou instanci značky  **Module** na požadovanou úroveň protokolu:  

  - Chyba: označuje problémy, které vyžadují pozornost.  

  - Upozornění: označuje možné problémy pro klientské operace.  

  - INFORMACE: Podrobnější protokolování, které indikuje stav různých událostí na klientovi.  

  - TRACE: podrobné protokolování, které se obvykle používá k diagnostice problémů  

- **scxcmprovider. log**. Pokud chcete změnit úroveň protokolu, upravte **/opt/microsoft/omi/etc/scxcmprovider.conf** a změňte každou instanci značky **Module** na požadovanou úroveň protokolu:  

  - Chyba: označuje problémy, které vyžadují pozornost.  

  - Upozornění: označuje možné problémy pro klientské operace.

  - INFORMACE: Podrobnější protokolování, které indikuje stav různých událostí na klientovi.  

Za normálních provozních podmínek použijte úroveň protokolu chyb. Tato úroveň protokolu vytvoří nejmenší soubor protokolu. Protože se úroveň protokolu zvyšuje z chyby na upozornění, informace a následně trasování, je vytvořen větší soubor protokolu, protože do souboru se zapisují další data.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Správa souborů protokolu pro klienta se systémy Linux a UNIX

Klient pro systémy Linux a UNIX neomezuje maximální velikost souborů protokolu klienta. Také automaticky nekopíruje obsah svých souborů. log do jiného souboru, například do souboru. lo_. Pokud chcete řídit maximální velikost souborů protokolu, implementujte proces pro správu souborů protokolu nezávisle na klientovi Configuration Manager pro systémy Linux a UNIX.  

Například můžete použít standardní příkaz systému Linux a UNIX **logrotate** pro správu velikosti a rotace souborů protokolů klienta. Klient Configuration Manager pro systémy Linux a UNIX má rozhraní, které umožňuje **logrotate** klientovi signalizovat, kdy se rotace protokolu dokončí, aby klient mohl pokračovat v protokolování do souboru protokolu.  

Informace o příkazu **logrotate** najdete v dokumentaci pro distribuce operačních systémů Linux a UNIX, které používáte.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Klient pro počítače Mac

Klient Configuration Manager pro počítače Mac zaznamenává informace v následujících protokolových souborech v počítači Mac:  

|Název protokolu|Podrobnosti|Umístění|
|--------------|-------------|-------------|
|CCMClient- &lt; *date_time*>. log|Zaznamenává činnosti týkající se operací klienta Mac, včetně správy aplikací, inventáře a protokolování chyb.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent- &lt; *date_time*>. log|Zaznamenává informace týkající se operací klienta, včetně operací přihlášení a odhlášení uživatele a aktivity počítače Mac.| `~/Library/Logs`|  
|CCMNotifications- &lt; *date_time*>. log|Zaznamenává činnosti týkající se Configuration Manager oznámení zobrazených v počítači Mac.| `~/Library/Logs`|  
|CCMPrefPane- &lt; *date_time*>. log|Zaznamenává činnosti týkající se dialogového okna Předvolby Configuration Manager v počítači Mac, které zahrnují obecné protokolování stavu a chyb.| `~/Library/Logs`|  

Soubor protokolu **SMS_DM. log** na serveru systému lokality zaznamenává komunikaci mezi počítači Mac a bodem správy, který je nastaven pro mobilní zařízení a počítače se systémem Mac.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a> Soubory protokolu serveru

V následujících oddílech jsou uvedeny soubory protokolů, které jsou na serveru lokality nebo které souvisejí s konkrétními rolemi systému lokality.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a> Server lokality a systémy lokality

Následující tabulka uvádí soubory protokolů, které jsou na serveru Configuration Manager lokality a na serverech systému lokality.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Zaznamenává činnost zpracování zápisu.|Server lokality|  
|ADForestDisc.log|Zaznamenává akce funkce zjišťování doménové struktury služby Active Directory.|Server lokality|  
|AdminService. log|Zaznamenává akce pro službu správy poskytovatele serveru SMS REST API|Počítač obsahující poskytovatele serveru SMS|
|ADService.log|Zaznamenává vytváření účtů a údaje skupiny zabezpečení ve službě Active Directory.|Server lokality|  
|adsgdis.log|Zaznamenává akce funkce zjišťování skupiny služby Active Directory.|Server lokality|  
|adsysdis.log|Zaznamenává akce funkce zjišťování systému služby Active Directory.|Server lokality|  
|adusrdis.log|Zaznamenává akce funkce zjišťování uživatele služby Active Directory.|Server lokality|  
|BusinessAppProcessWorker. log|Zaznamenává zpracování pro Microsoft Store pro obchodní aplikace.|Server lokality|
|ccm.log|Zaznamenává činnosti pro nabízenou instalaci klienta.|Server lokality|  
|CertMgr.log|Zaznamenává aktivity certifikátů pro komunikaci v rámci lokality.|Server systému lokality|  
|chmgr.log|Zaznamenává činnosti správce stavů klienta.|Server lokality|  
|Cidm.log|Zaznamenává změny nastavení klienta prostřednictvím správce instalačních dat klienta (CIDM).|Server lokality|  
|CollectionAADGroupSyncWorker. log | Počínaje verzí 2002 se soubor protokolu pro synchronizaci výsledků členství kolekce Azure Active Directory. Ve verzi 1910 a starší se protokolování této funkce spojilo v SMS_AZUREAD_DISCOVERY_AGENT. log. | Server lokality|
|colleval.log|Podrobnosti záznamu týkající se vytvoření, změny a odstranění kolekcí nástrojem Collection Evaluator.|Server lokality|  
|compmon.log|Zaznamenává stav vláken součástí monitorovaných pro server lokality.|Server systému lokality|  
|compsumm.log|Zaznamenává úlohy sumarizovatele stavů součástí.|Server lokality|  
|ComRegSetup.log|Zaznamenává výsledky registrace COM počáteční instalace pro server lokality.|Server systému lokality|  
|dataldr.log|Zaznamenává informace o zpracování souborů MIF a inventáře hardwaru v databázi Configuration Manager.|Server lokality|  
|ddm.log|Činnosti záznamů nástroje Discovery Data Manager.|Server lokality|  
|despool.log|Zaznamenává přenosy příchozích komunikací mezi lokalitami.|Server lokality|  
|distmgr.log|Zaznamenává údaje vytváření, komprese, rozdílové replikace a aktualizací informací o balíčcích. Může taky zahrnovat další aktivity z komponenty správce distribuce. Například instalace distribučního bodu, pokusů o připojení a instalace součástí. Další informace o dalších funkcích, které používají tento protokol, najdete v tématu [připojení ke spojovacímu bodu služby](#BKMK_WITLog) a [nasazení operačního systému](#BKMK_OSDLog).|Server lokality|  
|EPCtrlMgr.log|Zaznamenává informace o synchronizaci informací o hrozbách malwaru ze serveru Endpoint Protection role systému lokality s databází Configuration Manager.|Server lokality|  
|EPMgr.log|Zaznamenává stav role systému lokality ochrany koncového bodu Endpoint Protection.|Server systému lokality|  
|EPSetup.log|Poskytuje informace o instalaci role systému lokality ochrany koncového bodu Endpoint Protection.|Server systému lokality|  
|EnrollSrv.log|Zaznamenává činnosti procesu služby zápisu.|Server systému lokality|  
|EnrollWeb.log|Zaznamenává činnosti procesu webové stránky zápisu.|Server systému lokality|  
|fspmgr.log|Zaznamenává činnosti role systému lokality záložního stavového bodu.|Server systému lokality|  
|hman.log|Zaznamenává informace o změnách konfigurace lokality a o publikování informací o lokalitě v Active Directory Domain Services.|Server lokality|  
|Inboxast.log|Zaznamenává soubory, které jsou přemístěné z bodu správy do příslušných složek DORUČENÁ POŠTA na serveru lokality.|Server lokality|  
|inboxmgr.log|Zaznamenává činnosti přenosu souborů mezi složkami doručené pošty.|Server lokality|  
|inboxmon.log|Zaznamenává zpracování souborů doručené pošty a aktualizace čítačů výkonu.|Server lokality|  
|invproc.log|Zaznamenává odesílání souborů MIF ze sekundární lokality do její nadřazené lokality.|Server lokality|  
|migmctrl.log|Zaznamenává informace pro akce migrace zahrnující úlohy migrace, sdílené distribuční body a upgrady distribučních bodů.|Lokalita nejvyšší úrovně v hierarchii Configuration Manager a každá podřízená primární lokalita. V hierarchii s více primárními lokalitami použijte protokolový soubor, který je vytvořen v lokalitě centrální správy.|  
|mpcontrol.log|Zaznamenává registraci bodu správy pomocí služby WINS (Windows Internet Name Service). Zaznamenává dostupnost bodu správy každých 10 minut.|Server systému lokality|  
|mpfdm.log|Zaznamenává akce součásti bodu správy, která přemísťuje soubory klienta do příslušných složek DORUČENÁ POŠTA na serveru lokality.|Server systému lokality|  
|mpMSI.log|Zaznamenává údaje o instalaci bodu správy.|Server lokality|  
|MPSetup.log|Zaznamenává proces obálky instalace bodu správy.|Server lokality|  
|netdisc.log|Zaznamenává akce funkce zjišťování sítě.|Server lokality|  
|NotiCtrl. log|Oznámení žádostí o aplikace|Server lokality|  
|ntsvrdis.log|Zaznamenává činnost funkce zjišťování na serverech systému lokality.|Server lokality|  
|Objreplmgr|Zaznamenává zpracování oznámení o změnách objektů pro replikaci.|Server lokality|  
|offermgr.log|Zaznamenává aktualizace inzerování.|Server lokality|  
|offersum.log|Zaznamenává shrnutí stavových zpráv nasazení.|Server lokality|  
|OfflineServicingMgr.log|Zaznamenává činnosti použití aktualizací pro soubory image operačního systému.|Server lokality|  
|outboxmon.log|Zaznamenává zpracování souborů odeslané pošty a aktualizace čítačů výkonu.|Server lokality|  
|PerfSetup.log|Zaznamenává výsledky instalace čítačů výkonu.|Server systému lokality|  
|PkgXferMgr.log|Zaznamenává akce součásti SMS_Executive zodpovědné za odeslání obsahu z primární lokality do vzdáleného distribučního bodu.|Server lokality|  
|policypv.log|Zaznamenává aktualizace zásad klienta k zohlednění změn v nastaveních nebo nasazeních klienta.|Server primární lokality|  
|rcmctrl.log|Zaznamenává činnosti replikace databáze mezi lokalitami v hierarchii.|Server lokality|  
|replmgr.log|Zaznamenává replikaci souborů mezi součástmi serveru lokality a součástí plánovače.|Server lokality|  
|ResourceExplorer.log|Zaznamenává chyby, upozornění a informace o spouštění Průzkumník prostředků.|Počítač se spuštěnou konzolou Configuration Manager|  
|RESTPROVIDERSetup. log|Instalace REST API služby pro správu poskytovatele služby SMS|Počítač obsahující poskytovatele serveru SMS|
|ruleengine.log|Zaznamenává údaje o pravidlech automatického nasazování pro identifikaci, stahování obsahu a skupině aktualizací softwaru a vytváření nasazení.|Server lokality|  
|schedule.log|Zaznamenává údaje o replikaci úloh mezi lokalitami a o replikaci souborů.|Server lokality|  
|sender.log|Zaznamenává soubory, které provádějí přenos replikací souborů mezi lokalitami.|Server lokality|  
|sinvproc.log|Zaznamenává informace o zpracování dat inventáře softwaru do databáze lokality.|Server lokality|  
|sitecomp.log|Zaznamenává údaje o správě nainstalovaných součástí lokality na všech serverech systému v lokalitě.|Server lokality|  
|sitectrl.log|Zaznamenává změny nastavení lokality provedené na objektech řízení lokality v databázi.|Server lokality|  
|sitestat.log|Zaznamenává proces monitorování dostupnosti a volného místa na disku pro všechny systémy lokality.|Server lokality|
|SMS_AZUREAD_DISCOVERY_AGENT. log| Soubor protokolu pro službu Azure Active Directory (Azure AD) pro zjišťování uživatelů a skupin uživatelů. Ve verzi 1910 a starší zahrnuje také synchronizaci výsledků členství kolekce do služby Azure AD.| Server lokality|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Soubor protokolu pro součást, která synchronizuje aplikace z Microsoft Store pro firmy.|Server lokality|
|SMS_DataEngine. log|Soubor protokolu pro přehledy správy.|Server lokality|
|SMS_ISVUPDATES_SYNCAGENT. log| Soubor protokolu pro synchronizaci aktualizací softwaru třetích stran.| Bod aktualizace softwaru nejvyšší úrovně v hierarchii Configuration Manager.|
|SMS_OrchestrationGroup. log| Soubor protokolu pro skupiny orchestrace|Server lokality|
|SMS_PhasedDeployment. log| Soubor protokolu pro dvoufázové nasazení|Lokalita nejvyšší úrovně v hierarchii Configuration Manager|
|SMS_REST_PROVIDER. log|Stav služby pro REST API služby pro správu poskytovatele služby SMS, včetně informací o certifikátu|Počítač obsahující poskytovatele serveru SMS|
|SmsAdminUI.log|Zaznamenává činnost konzoly Configuration Manager.|Počítač se spuštěnou konzolou Configuration Manager|  
|SMSAWEBSVCSetup.log|Zaznamenává instalační činnosti webové služby Application Catalog.|Server systému lokality|  
|smsbkup.log|Zaznamenává výsledek procesu zálohování lokality.|Server lokality|  
|smsdbmon.log|Zaznamenává změny databáze.|Server lokality|  
|SMSENROLLSRVSetup.log|Zaznamenává instalační činnosti webové služby zápisu.|Server systému lokality|  
|SMSENROLLWEBSetup.log|Zaznamenává instalační činnosti webové stránky zápisu.|Server systému lokality|  
|smsexec.log|Zaznamenává zpracování všech vláken součástí serveru lokality.|Server lokality nebo server systému lokality|  
|SMSFSPSetup.log|Zaznamenává zprávy vytvářené instalací záložního stavového bodu.|Server systému lokality|  
|SMSPORTALWEBSetup.log|Zaznamenává instalační činnosti webové stránky služby Application Catalog.|Server systému lokality|  
|SMSProv.log|Zaznamenává přístup poskytovatele služby WMI k databázi lokality.|Počítač obsahující poskytovatele serveru SMS|  
|srsrpMSI.log|Zaznamenává podrobné výsledky procesu instalace bodu generování sestav z výstupu MSI.|Server systému lokality|  
|srsrpsetup.log|Zaznamenává výsledky procesu instalace bodu generování sestav.|Server systému lokality|  
|statesys.log|Zaznamenává zpracování stavových zpráv systému.|Server lokality|  
|statmgr.log|Zaznamenává zápis všech stavových zpráv do databáze.|Server lokality|  
|swmproc.log|Zaznamenává zpracování souborů a nastavení měření.|Server lokality|
|UXAnalyticsUploadWorker. log|Zaznamenává nahrávání dat do služby pro službu Endpoint Analytics.|Server lokality|

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a> Instalace serveru lokality

Následující tabulka uvádí protokolové soubory, které obsahují informace týkající se instalace lokality.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Zaznamenává požadavky na vyhodnocení požadovaných součástí a instalační činnosti.|Server lokality|  
|ConfigMgrSetup.log|Zaznamenává podrobný výstup z nastavení serveru lokality.|Server lokality|  
|ConfigMgrSetupWizard.log|Zaznamenává informace související s aktivitou v Průvodci instalací nástroje.|Server lokality|  
|SMS_BOOTSTRAP.log|Zaznamenává informace o průběhu spuštění procesu instalace sekundární lokality. Informace o aktuálním procesu instalace jsou obsažené v souboru ConfigMgrSetup.log.|Server lokality|  
|smstsvc.log|Zaznamenává informace o instalaci, použití a odebrání služby systému Windows. Systém Windows používá tuto službu k testování připojení a oprávnění mezi servery. Používá počítačový účet serveru, který vytváří připojení.|Server lokality a server systému lokality|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a> Bod služby datového skladu

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se bodu služby datového skladu.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|DWSSMSI. log|Zaznamenává zprávy vygenerované instalací bodu služby datového skladu.|Server systému lokality|  
|DWSSSetup. log|Zaznamenává zprávy vygenerované instalací bodu služby datového skladu.|Server systému lokality|  
|Microsoft.ConfigMgrDataWarehouse. log|Zaznamenává informace o synchronizaci dat mezi databází lokality a databází datového skladu.|Server systému lokality|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a> Bod záložního stavu

Následující tabulka uvádí protokolové soubory, které obsahují informace týkající se záložního stavového bodu.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Zaznamenává údaje o komunikacích se záložním stavovým bodem ze starších klientů a počítačů klientů mobilních zařízení.|Server systému lokality|  
|fspMSI.log|Zaznamenává zprávy vytvářené instalací záložního stavového bodu.|Server systému lokality|  
|fspmgr.log|Zaznamenává činnosti role systému lokality záložního stavového bodu.|Server systému lokality|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a> Bod správy

Následující tabulka uvádí protokolové soubory, které obsahují informace týkající se bodu správy.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Zaznamenává činnost zpracování zpráv klienta na koncovém bodě.|Server systému lokality|
|CCM_STS. log|Zaznamenává činnosti pro tokeny ověřování, buď od Azure Active Directory nebo tokenů klientů vydaných serverem.|Server systému lokality|
|ClientAuth.log|Zaznamenává aktivitu podepisování a ověřování.|Server systému lokality|
|MP_CliReg.log|Zaznamenává činnost registrace klienta zpracovávané bodem správy.|Server systému lokality|  
|MP_Ddr.log|Zaznamenává převod záznamů XML. DDR z klientů a kopíruje je do serveru lokality.|Server systému lokality|  
|MP_Framework.log|Zaznamenává činnosti základního bodu správy a součástí architektury klienta.|Server systému lokality|  
|MP_GetAuth.log|Zaznamenává činnost autorizace klienta.|Server systému lokality|  
|MP_GetPolicy.log|Zaznamenává dotazovací činnost zásad z klientských počítačů.|Server systému lokality|  
|MP_Hinv.log|Zaznamenává údaje o převodu záznamů inventáře hardwaru XML od klientů a o kopírování těchto souborů do serveru lokality.|Server systému lokality|  
|MP_Location.log|Zaznamenává činnost dotazů a odpovědí na umístění od klientů.|Server systému lokality|  
|MP_OOBMgr.log|Zaznamenává činnosti bodu správy související s přijímáním jednorázového hesla od klienta.|Server systému lokality|  
|MP_Policy.log|Zaznamenává komunikaci zásad.|Server systému lokality|  
|MP_RegistrationManager. log|Zaznamenává činnosti týkající se registrace klienta, jako je například ověřování certifikátů, seznamů CRL a tokenů.|Server systému lokality|
|MP_Relay.log|Zaznamenává přenos shromažďovaných souborů od klienta.|Server systému lokality|  
|MP_Retry.log|Zaznamenává opakované procesy inventáře hardwaru.|Server systému lokality|  
|MP_Sinv.log|Zaznamenává údaje o převodu záznamů inventáře softwaru XML od klientů a o kopírování těchto souborů do serveru lokality.|Server systému lokality|  
|MP_SinvCollFile.log|Zaznamenává údaje o kolekci souborů.|Server systému lokality|  
|MP_Status.log|Zaznamenává údaje o převodu souborů stavových zpráv XML.svf od klientů a o kopírování těchto souborů do serveru lokality.|Server systému lokality|
|mpcontrol.log|Zaznamenává registraci bodu správy pomocí služby WINS. Zaznamenává dostupnost bodu správy každých 10 minut.|Server lokality|  
|mpfdm.log|Zaznamenává akce součásti bodu správy, která přemísťuje soubory klienta do příslušných složek DORUČENÁ POŠTA na serveru lokality.|Server systému lokality|  
|mpMSI.log|Zaznamenává údaje o instalaci bodu správy.|Server lokality|  
|MPSetup.log|Zaznamenává proces obálky instalace bodu správy.|Server lokality|  
|Userservice předefinovala smazání. log|Zaznamenává požadavky uživatelů z centra softwaru, načítá nebo instaluje aplikace dostupné pro uživatele ze serveru.|Server systému lokality|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a> Bod připojení služby

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se spojovacího bodu služby.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Zaznamenává informace o certifikátech a proxy účtu.|Server lokality|  
|CollEval.log|Podrobnosti záznamu týkající se vytvoření, změny a odstranění kolekcí nástrojem Collection Evaluator.|Primární lokalita a lokalita centrální správy|  
|Cloudusersync.log|Zaznamenává povolení licence pro uživatele.|Počítač se spojovacím bodem služby|  
|Dataldr.log|Zaznamenává údaje o zpracování souborů MIF.|Server lokality|  
|ddm.log|Činnosti záznamů nástroje Discovery Data Manager.|Server lokality|  
|Distmgr.log|Zaznamenává údaje o požadavcích na distribuci obsahu.|Server lokality vysoké úrovně|  
|Dmpdownloader.log|Zaznamenává údaje o stahování z Microsoft Intune.|Počítač se spojovacím bodem služby|  
|Dmpuploader.log|Zaznamenává podrobnosti týkající se nahrávání změn databáze Microsoft Intune.|Počítač se spojovacím bodem služby|  
|hman.log|Zaznamenává údaje o předávání zpráv.|Server lokality|  
|MSfBSyncWorker. log|Zaznamenává informace o komunikaci s Microsoft Store pro firmy.|Počítač se spojovacím bodem služby|
|objreplmgr.log|Zaznamenává zpracování zásad a přiřazení.|Server primární lokality|  
|PolicyPV.log|Zaznamenává generování zásad u všech zásad.|Server lokality|  
|outgoingcontentmanager.log|Zaznamenává obsah odeslaný do Microsoft Intune.|Počítač se spojovacím bodem služby|  
|ServiceConnectionTool. log|Zaznamenává údaje o použití nástroje pro [připojení služby](../../servers/manage/use-the-service-connection-tool.md) na základě parametru, který používáte. Pokaždé, když nástroj spustíte, nahradí se veškerý stávající soubor protokolu.|Stejné umístění jako nástroj|
|Sitecomp.log|Zaznamenává údaje o instalaci spojovacího bodu služby.|Server lokality|  
|SmsAdminUI.log|Zaznamenává činnost konzoly Configuration Manager.|Počítač se spuštěnou konzolou Configuration Manager|  
|SMS_CLOUDCONNECTION. log|Zaznamenává informace o cloudových službách.|Počítač se spojovacím bodem služby|
|Smsprov.log|Zaznamenává aktivity poskytovatele serveru SMS. Configuration Manager aktivity konzoly používají poskytovatele serveru SMS.|Počítač obsahující poskytovatele serveru SMS|  
|SrvBoot.log|Zaznamenává údaje o službě instalačního programu spojovacího bodu služby.|Počítač se spojovacím bodem služby|  
|Statesys.log|Zaznamenává zpracování zpráv správy mobilních zařízení.|Primární lokalita a lokalita centrální správy|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a> Bod aktualizace softwaru

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se bodu aktualizace softwaru.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Zaznamenává údaje o replikaci souborů oznámení o aktualizacích softwaru z nadřazené lokality do podřízených lokalit.|Server lokality|  
|PatchDownloader.log|Zaznamenává údaje o procesu stahování aktualizací softwaru ze zdroje aktualizací do cílového umístění stahování na serveru lokality.|Při ručním stažení aktualizací se tento soubor nachází ve vašem `%temp%` adresáři na počítači, kde používáte konzolu nástroje. V případě pravidel automatického nasazení je-li klient Configuration Manager nainstalován na serveru lokality, je tento soubor na serveru lokality v nástroji `%windir%\CCM\Logs` .|  
|ruleengine.log|Zaznamenává údaje o pravidlech automatického nasazování pro identifikaci, stahování obsahu a skupině aktualizací softwaru a vytváření nasazení.|Server lokality|
|SMS_ISVUPDATES_SYNCAGENT. log| Soubor protokolu pro synchronizaci aktualizací softwaru třetích stran.| Bod aktualizace softwaru nejvyšší úrovně v hierarchii Configuration Manager.|
|SUPSetup.log|Zaznamenává údaje o instalaci bodu aktualizací softwaru. Po dokončení instalace bodu aktualizací softwaru se do tohoto souboru protokolu zapíše text **Instalace byla úspěšná**.|Server systému lokality|  
|WCM.log|Zaznamenává údaje o konfiguraci bodu aktualizace softwaru a připojení k serveru WSUS pro odebírané kategorie, klasifikace a jazyky aktualizací.|Server lokality, který se připojuje k serveru WSUS|  
|WSUSCtrl.log|Zaznamenává údaje o konfiguraci, připojení databáze a stavu serveru služby WSUS pro lokalitu.|Server systému lokality|  
|wsyncmgr.log|Zaznamenává údaje o procesu synchronizace aktualizací softwaru.|Server systému lokality|  
|WUSSyncXML.log|Zaznamenává údaje týkající se nástroje inventáře pro proces synchronizace aktualizací od společnosti Microsoft.|Klientský počítač nakonfigurovaný jako hostitel synchronizace pro nástroj inventáře pro aktualizace od Microsoftu|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a> Soubory protokolu podle funkcí

V následujících oddílech jsou uvedeny soubory protokolu týkající se funkcí Configuration Manager.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a> Správa aplikací

Následující tabulka uvádí soubory protokolů, které obsahují informace související se správou aplikací.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Zaznamenává údaje týkající se aktuálního a zamýšleného stavu aplikací, jejich použitelnosti, splnění požadavků, typů nasazení a závislostí.|Klient|  
|AppDiscovery.log|Zaznamenává údaje týkající se zjišťování nebo detekce aplikací na klientských počítačích.|Klient|  
|AppEnforce.log|Zaznamenává údaje týkající se vynucených akcí (instalace a odinstalace) provedených pro aplikace v klientovi.|Klient|  
|AppGroupHandler. log|Počínaje verzí 1906, informace o detekci a vynucení pro skupiny aplikací|Klient|
|awebsctl.log|Zaznamenává aktivity sledování pro roli systému lokality bodu webové služby katalogu aplikací.|Server systému lokality|  
|awebsvcMSI.log|Zaznamenává podrobné informace o instalaci pro roli systému lokality bodu webové služby katalogu aplikací.|Server systému lokality|  
|BusinessAppProcessWorker. log|Zaznamenává zpracování pro Microsoft Store pro obchodní aplikace.|Server lokality|
|Ccmsdkprovider.log|Zaznamenává aktivity správy aplikací sady SDK.|Klient|  
|colleval.log|Podrobnosti záznamu týkající se vytvoření, změny a odstranění kolekcí nástrojem Collection Evaluator.|Server systému lokality|  
|ConfigMgrSoftwareCatalog.log|Zaznamenává aktivitu katalogu aplikací, což zahrnuje jeho použití programu Silverlight.|Klient|  
|MSfBSyncWorker. log|Zaznamenává informace o komunikaci s Microsoft Store pro firmy.|Počítač se spojovacím bodem služby|
|NotiCtrl. log|Oznámení žádostí o aplikace|Server lokality|  
|portlctl.log|Zaznamenává aktivity sledování pro roli systému lokality bodu webu katalogu aplikací.|Server systému lokality|  
|portlwebMSI.log|Zaznamenává aktivitu instalace MSI pro role webu katalogu aplikací.|Server systému lokality|  
|PrestageContent.log|Zaznamenává údaje o použití nástroje ExtractContent.exe ve vzdáleném, připraveném distribučním bodě. Tento nástroj rozbaluje obsah, který se exportoval do souboru.|Server systému lokality|  
|ServicePortalWebService.log|Zaznamenává aktivitu obsluhy webu katalogu aplikací.|Server systému lokality|  
|ServicePortalWebSite.log|Zaznamenává aktivitu webu katalogu aplikací.|Server systému lokality|  
|SettingsAgent. log|Vynucování konkrétních aplikací, zaznamená orchestraci vyhodnocení skupin aplikací a podrobnosti o zásadách spolusprávy.|Klient|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Soubor protokolu pro součást, která synchronizuje aplikace z Microsoft Store pro firmy.|Server lokality|
|SMS_CLOUDCONNECTION. log|Zaznamenává informace o cloudových službách.|Počítač se spojovacím bodem služby|
|SMSdpmon.log|Zaznamenává údaje týkající se naplánované úlohy sledování stavu distribučního bodu, která je nakonfigurovaná v distribučním bodě.|Server lokality|  
|SoftwareCatalogUpdateEndpoint.log|Zaznamenává aktivity pro správu adresy URL pro katalog aplikací zobrazené v centru softwaru.|Klient|  
|SoftwareCenterSystemTasks.log|Zaznamenává činnosti související s ověřením požadované součásti centra softwaru.|Klient|  
|TSDTHandler. log|Pro typ nasazení pořadí úloh. Protokoluje proces od vynucení aplikace (při instalaci nebo odinstalaci) při spuštění pořadí úkolů. Použijte ho s AppEnforce. log a souboru Smsts. log.|Klient|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>Balíčky a programy

Následující tabulka uvádí soubory protokolů, které obsahují informace související s nasazováním balíčků a programů.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|colleval.log|Podrobnosti záznamu týkající se vytvoření, změny a odstranění kolekcí nástrojem Collection Evaluator.|Server lokality|  
|execmgr.log|Zaznamenává údaje týkající se běžících balíčků a sekvencí úloh.|Klient|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a> funkce Asset Intelligence

Následující tabulka uvádí soubory protokolů, které obsahují informace související s funkcí Asset Intelligence.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Zaznamenává aktivity akcí inventáře Asset Intelligence.|Klient|  
|aikbmgr.log|Zaznamenává údaje týkající se zpracování souborů XML z doručené pošty pro aktualizaci katalogu Asset Intelligence.|Server lokality|  
|AIUpdateSvc.log|Zaznamenává interakce funkce Asset Intelligenceho bodu synchronizace s cloudovou službou.|Server systému lokality|  
|AIUSMSI.log|Zaznamenává údaje o instalaci role systému lokality bodu synchronizace funkce Asset Intelligence.|Server systému lokality|  
|AIUSSetup.log|Zaznamenává údaje o instalaci role systému lokality bodu synchronizace funkce Asset Intelligence.|Server systému lokality|  
|ManagedProvider.log|Zaznamenává údaje týkající se zjišťovacího softwaru s přidruženou identifikační softwarovou značkou. Zaznamenává také činnosti související s inventářem hardwaru.|Server systému lokality|  
|MVLSImport.log|Zaznamenává údaje týkající se zpracování importovaných licenčních souborů.|Server systému lokality|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a> Zálohování a obnovení

Následující tabulka uvádí soubory protokolů, které obsahují informace související s akcemi zálohování a obnovení, včetně resetování lokalit a změn u poskytovatele serveru SMS.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Zaznamenává informace týkající se úloh nastavení a obnovení, když Configuration Manager obnovuje lokalitu ze zálohy.|Server lokality|  
|Smsbkup.log|Zaznamenává údaje týkající se aktivity zálohování lokality.|Server lokality|  
|smssqlbkup.log|Zaznamenává výstup z procesu zálohování databáze lokality, když je SQL Server nainstalována na serveru, který není serverem lokality.|Server databáze lokality|  
|Smswriter.log|Zaznamenává informace o stavu Configuration Manager zapisovači VSS, který je používán procesem zálohování.|Server lokality|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> Zápis certifikátu

V následující tabulce jsou uvedeny soubory protokolu Configuration Manager, které obsahují informace související s zápisem certifikátu. Zápis certifikátu používá bod registrace certifikátu a modul zásad Configuration Manager na serveru, na kterém je spuštěná služba zápisu síťových zařízení (NDES).  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|Crp.log|Zaznamenává činnosti registrace.|Bod registrace certifikátu|  
|Crpctrl.log|Zaznamenává provozní stav bodu registrace certifikátu.|Bod registrace certifikátu|  
|Crpsetup.log|Zaznamenává údaje týkající se instalace a konfigurace bodu registrace certifikátu.|Bod registrace certifikátu|  
|Crpmsi.log|Zaznamenává údaje týkající se instalace a konfigurace bodu registrace certifikátu.|Bod registrace certifikátu|  
|NDESPlugin.log|Zaznamenává ověřování výzvou a aktivity Registrace certifikátů.|Modul zásad Configuration Manager a Služba zápisu síťových zařízení|  

Společně s Configuration Manager soubory protokolů Zkontrolujte protokoly aplikací Windows v Prohlížeč událostí na serveru, na kterém je spuštěná služba zápisu síťových zařízení, a na serveru, který je hostitelem bodu registrace certifikátu. Hledejte třeba zprávy ze zdroje **NetworkDeviceEnrollmentService**.

Můžete taky použít následující soubory protokolů:  

- Soubory protokolu služby IIS pro službu zápisu síťových zařízení: **%systemdrive%\inetpub\logs\LogFiles\W3SVC1**  

- Soubory protokolu služby IIS pro bod registrace certifikátu: **%systemdrive%\inetpub\logs\LogFiles\W3SVC1**  

- Soubor protokolu zásad zápisu síťových zařízení: **mscep.log**  

    > [!NOTE]  
    > Tento soubor se nachází ve složce pro profil účtu NDES, například v složce c:\users\scepsvc.. Další informace o tom, jak povolit protokolování NDES, najdete v části [Povolení protokolování](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) na wikiwebu NDES.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a> Klientské oznámení

Následující tabulka uvádí soubory protokolů, které obsahují informace související s klientským oznámením.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Zaznamenává údaje o aktivitách serveru lokality souvisejících s úlohami klientských oznámení a zpracování online a se soubory stavu úloh.|Server lokality|  
|BGBServer.log|Zaznamenává aktivity serveru oznámení, jako je komunikace mezi klientem a serverem a doručování úloh klientům. Také zaznamenává informace o generaci online a souborů stavu úloh, které se mají odeslat na server lokality.|Bod správy|  
|BgbSetup.log|Zaznamenává činnosti procesu obálky instalace serveru oznámení během instalace a odinstalace.|Bod správy|  
|bgbisapiMSI.log|Zaznamenává údaje o instalaci a odinstalaci serveru oznámení.|Bod správy|  
|BgbHttpProxy.log|Zaznamenává aktivity oznámení HTTP proxy jak předává zprávy klientů pomocí protokolu HTTP na server oznámení a z něho.|Klient|  
|CcmNotificationAgent.log|Zaznamenává aktivity agenta oznámení, jako je komunikace mezi klientem a serverem, a informace o přijatých a odeslaných úlohách jiným klientským agentům.|Klient|  

### <a name="cloud-management-gateway"></a>Brána pro správu cloudu

Následující tabulka uvádí soubory protokolů, které obsahují informace související s bránou pro správu cloudu.

|Název protokolu|Popis|Počítač obsahující soubor protokolu|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Zaznamenává údaje o nasazení služby brány pro správu cloudu, stavu průběžné služby a k používání dat přidružených k této službě. Pokud chcete nakonfigurovat úroveň protokolování, upravte hodnotu **úrovně protokolování** v následujícím klíči registru: `HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|Složka *INSTALLDIR* na serveru primární lokality nebo CAS.|
|CMGSetup. log – <sup> [Poznámka 1](#bkmk_note1)</sup>|Zaznamenává údaje o druhé fázi nasazení brány pro správu cloudu (místní nasazení v Azure). Pokud chcete nakonfigurovat úroveň protokolování, použijte nastavení **úroveň trasování** (**informace** (výchozí), **verbose**, **Chyba**) na kartě **Konfigurace služby Azure portal\Cloud** .|**%AppRoot%\Logs** na serveru Azure nebo ve složce SMS/protokolů na serveru systému lokality|
|CMGService. log – <sup> [Poznámka 1](#bkmk_note1)</sup>|Zaznamenává údaje o komponentě jádra služby brány pro správu cloudu v Azure. Pokud chcete nakonfigurovat úroveň protokolování, použijte nastavení **úroveň trasování** (**informace** (výchozí), **verbose**, **Chyba**) na kartě **Konfigurace služby Azure portal\Cloud** .|**%AppRoot%\Logs** na serveru Azure nebo ve složce SMS/protokolů na serveru systému lokality|
|SMS_Cloud_ProxyConnector. log|Zaznamenává údaje týkající se nastavení připojení mezi službou brány pro správu cloudu a bodem připojení brány pro správu cloudu.|Server systému lokality|
|CMGContentService. log – <sup> [Poznámka 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Když povolíte, aby CMG taky poskytoval obsah z Azure Storage, tento protokol zaznamenává podrobnosti o této službě.|**%AppRoot%\Logs** na serveru Azure nebo ve složce SMS/protokolů na serveru systému lokality|

- Pro řešení potíží s nasazeními použijte protokol **CloudMgr. log** a **CMGSetup. log.**
- Pro řešení potíží se stavem služby použijte **protokol CMGService. log** a **SMS_Cloud_ProxyConnector. log**.
- Pro řešení potíží s klientskými přenosy použijte **protokol CMGHttpHandler. log**, **CMGService. log**a **SMS_Cloud_ProxyConnector. log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a> Poznámka 1: protokoly synchronizované z Azure

Jedná se o místní soubory Configuration Manager protokolů, které Cloud Service Manager synchronizuje z Azure Storage každých pět minut. Brána pro správu cloudu každých pět minut připisuje protokoly do Azure Storage. Proto je maximální zpoždění 10 minut. Podrobné přepínače ovlivňují místní i vzdálené protokoly. Mezi skutečné názvy souborů patří název služby a identifikátor instance role. Například CMG-*ServiceName* - *RoleInstanceID*-CMGSetup. log. Tyto soubory protokolu se synchronizují, takže je nemusíte v bráně pro správu cloudu získat a tato možnost není podporovaná.

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> Nastavení dodržování předpisů a přístup k prostředkům společnosti

Následující tabulka uvádí soubory protokolů, které obsahují informace související s nastavením dodržování předpisů a přístupem k prostředkům společnosti.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Zaznamenává údaje týkající se procesu nápravy a souladu s nastavením dodržování předpisů, aktualizace softwaru a správy aplikací.|Klient|  
|CITaskManager.log|Zaznamenává informace týkající se plánování úloh položek konfigurace.|Klient|  
|DCMAgent.log|Zaznamenává informace vysoké úrovně o vyhodnocování, generování sestav o konfliktech a nápravě položek konfigurace a aplikací.|Klient|  
|DCMReporting.log|Zaznamenává informace o výsledcích platformy generování sestav služby Policy Platform do stavových zpráv pro položky konfigurace.|Klient|  
|DcmWmiProvider.log|Zaznamenává informace o čtení syncletů ze položky konfigurace z rozhraní WMI.|Klient|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Konzola Configuration Manager

Následující tabulka uvádí soubory protokolů, které obsahují informace související s konzolou Configuration Manager.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Zaznamenává instalaci konzoly Configuration Manager.|Počítač se spuštěnou konzolou Configuration Manager|  
|SmsAdminUI.log|Zaznamenává informace o operaci konzoly Configuration Manager.|Počítač se spuštěnou konzolou Configuration Manager|  
|Smsprov.log|Zaznamenává aktivity poskytovatele serveru SMS. Configuration Manager aktivity konzoly používají poskytovatele serveru SMS.|Server lokality nebo server systému lokality|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a> Správa obsahu

Následující tabulka uvádí soubory protokolů, které obsahují informace související se správou obsahu.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|Souboru CloudDP- &lt; GUID \> . log|Zaznamenává údaje pro konkrétní cloudový distribuční bod, včetně informací o skladování a přístupu k obsahu.|Server systému lokality|  
|CloudMgr.log|Zaznamenává údaje týkající se zřizování obsahu, shromažďování statistik úložiště a šířky pásma a akcí iniciované správcem pro zastavení nebo spuštění cloudové služby, která spouští cloudový distribuční bod.|Server systému lokality|  
|DataTransferService.log|Zaznamenává veškerou komunikaci služby BITS pro přístup k zásadám nebo balíčkům. Tento protokol se taky používá pro správu obsahu pomocí distribučních bodů pro vyžádání obsahu.|Počítač, který je nakonfigurován jako distribuční bod pro vyžádání obsahu|  
|PullDP.log|Zaznamenává údaje o obsahu, který převádí vyžadování distribučního bodu ze zdrojových distribučních bodů.|Počítač, který je nakonfigurován jako distribuční bod pro vyžádání obsahu|  
|PrestageContent.log|Zaznamenává údaje o použití nástroje ExtractContent.exe ve vzdáleném, připraveném distribučním bodě. Tento nástroj rozbaluje obsah, který se exportoval do souboru.|Role systému lokality|  
|SMSdpmon.log|Zaznamenává údaje o plánovaných úlohách sledování stavu distribučního bodu, které jsou konfigurovány v distribučním bodě.|Role systému lokality|  
|smsdpprov.log|Zaznamenává údaje o extrahování komprimovaných souborů přijatých z primární lokality. Tento protokol je generovaný zprostředkovatelem rozhraní WMI vzdáleného distribučního bodu.|Počítač distribučního bodu, který není společně umístěn na serveru lokality|  
|smsdpusage. log|Zaznamenává údaje o smsdpusage.exe, které běží, a shromažďuje data pro sestavu Souhrn využití distribučních bodů.|Role systému lokality|  

### <a name="desktop-analytics"></a>Desktop Analytics

Pomocí následujících souborů protokolu můžete pomoct řešit problémy s integrací Desktop Analytics s Configuration Manager.

Soubory protokolu ve spojovacím bodu služby jsou v následujícím adresáři: `%ProgramFiles%\Configuration Manager\Logs\M365A` .
Soubory protokolu v klientovi Configuration Manager jsou v následujícím adresáři: `%WinDir%\CCM\logs` .

| Protokol | Popis |Počítač obsahující soubor protokolu|
|---------|---------|---------|
| M365ADeploymentPlanWorker. log | Informace o plánu nasazení synchronizovaném s cloudovou službou Desktop Analytics do místních Configuration Manager |Spojovací bod služby|
| M365ADeviceHealthWorker. log | Informace o nahrání stavu zařízení z Configuration Manager do cloudu Microsoftu |Spojovací bod služby|
| M365AHandler. log | Informace o zásadách nastavení pro Desktop Analytics |Klient|
| M365AUploadWorker. log | Informace o shromažďování a nahrávání zařízení z Configuration Manager do cloudu Microsoftu |Spojovací bod služby|
| SmsAdminUI.log | Informace o aktivitě konzoly Configuration Manager, jako je konfigurace Azure Cloud Services  |Spojovací bod služby|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a> Rozpoznávání

Následující tabulka uvádí soubory protokolů, které obsahují informace související se zjišťováním.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Zaznamenává akce funkce zjišťování skupiny zabezpečení služby Active Directory.|Server lokality|  
|adsysdis.log|Zaznamenává akce funkce zjišťování systému služby Active Directory.|Server lokality|  
|adusrdis.log|Zaznamenává akce funkce zjišťování uživatele služby Active Directory.|Server lokality|  
|ADForestDisc.Log|Zaznamenává akce funkce zjišťování doménové struktury služby Active Directory.|Server lokality|  
|ddm.log|Činnosti záznamů nástroje Discovery Data Manager.|Server lokality|  
|InventoryAgent.log|Zaznamenává činnosti inventáře hardwaru, inventáře softwaru a akce zjišťování prezenčního signálu na klientovi.|Klient|  
|netdisc.log|Zaznamenává akce funkce zjišťování sítě.|Server lokality|  

### <a name="endpoint-analytics"></a><a name="bkmk_analytics"></a> Analýza koncových bodů

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|UXAnalyticsUploadWorker. log|Zaznamenává nahrávání dat do služby pro službu Endpoint Analytics.|Server lokality|  
|SensorWmiProvider. log|Zaznamenává činnost zprostředkovatele rozhraní WMI pro senzor služby Endpoint Analytics.|Klient|  
|SensorEndpoint. log|Zaznamenává spuštění zásad služby Endpoint Analytics a odeslání klientských dat na server lokality.|Klient|
|SensorManagedProvider. log|Zaznamenává shromažďování a zpracování událostí a informací pro službu Endpoint Analytics.|Klient|

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection

Následující tabulka uvádí soubory protokolů, které obsahují informace související s ochranou koncového bodu Endpoint Protection.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Zaznamenává údaje o instalaci klienta ochrany koncového bodu Endpoint Protection a o zásadách aplikace Antimalware pro tohoto klienta.|Klient|  
|EPCtrlMgr.log|Zaznamenává údaje o synchronizaci informací o hrozbách malwaru ze serveru Endpoint Protection role s databází Configuration Manager.|Server systému lokality|  
|EPMgr.log|Sleduje stav role systému lokality ochrany koncového bodu Endpoint Protection.|Server systému lokality|  
|EPSetup.log|Poskytuje informace o instalaci role systému lokality ochrany koncového bodu Endpoint Protection.|Server systému lokality|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a> SND

Následující tabulka uvádí soubory protokolů, které obsahují informace související s rozšířeními.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Zaznamenává informace o stažení rozšíření od Microsoftu a instalace a odinstalace všech rozšíření.|Počítač se spuštěnou konzolou Configuration Manager|  
|FeatureExtensionInstaller.log|Zaznamenává informace o instalaci a odebrání jednotlivých rozšíření, pokud jsou povolené nebo zakázané v konzole Configuration Manager.|Počítač se spuštěnou konzolou Configuration Manager|  
|SmsAdminUI.log|Zaznamenává činnost konzoly Configuration Manager.|Počítač se spuštěnou konzolou Configuration Manager|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a> Inventáře

Následující tabulka uvádí soubory protokolů, které obsahují informace související se zpracováním dat inventáře.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Zaznamenává informace o zpracování souborů MIF a inventáře hardwaru v databázi Configuration Manager.|Server lokality|  
|invproc.log|Zaznamenává odesílání souborů MIF ze sekundární lokality do její nadřazené lokality.|Server sekundární lokality|  
|sinvproc.log|Zaznamenává informace o zpracování dat inventáře softwaru do databáze lokality.|Server lokality|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a> Měření

Následující tabulka uvádí soubory protokolů, které obsahují informace související s měřením.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitoruje všechny procesy kontroly softwaru.|Klient|  
|SWMTRReportGen.log|Vygeneruje sestavu použití dat, která je shromažďována agentem měření. Tato data se protokolují v souboru Mtrmgr.log.|Klient|
|swmproc.log|Zaznamenává zpracování souborů a nastavení měření.|Server lokality|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a> Migrace

Následující tabulka uvádí soubory protokolů, které obsahují informace související s migrací.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Zaznamenává informace o akcích migrace zahrnujících úlohy migrace, sdílené distribuční body a upgradování distribučních bodů.|Lokalita nejvyšší úrovně v hierarchii Configuration Manager a každá podřízená primární lokalita. V hierarchii vícenásobných primárních lokalit použijte protokolový soubor vytvořený v lokalitě centrální správy.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a> Mobilní zařízení

V následujících oddílech jsou uvedeny soubory protokolů, které obsahují informace související se správou mobilních zařízení.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a> Registraci

Následující tabulka uvádí protokoly, které obsahují informace související s registrací mobilních zařízení.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Zaznamenává komunikaci mezi body správy, které jsou povolené pro mobilní zařízení, a koncovými body bodu správy.|Server systému lokality|  
|dmpmsi.log|Zaznamenává data Instalační služby systému Windows pro konfiguraci bodu správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DMPSetup.log|Zaznamenává konfiguraci bodu správy, pokud je povolený pro mobilní zařízení.|Server systému lokality|  
|enrollsrvMSI.log|Zaznamenává data Instalační služby systému Windows pro konfiguraci bodu registrace.|Server systému lokality|  
|enrollmentweb.log|Zaznamenává komunikaci mezi mobilními zařízeními a zprostředkujícím bodem registrace|Server systému lokality|  
|enrollwebMSI.log|Zaznamenává data Instalační služby systému Windows pro konfiguraci zprostředkujícího bodu registrace.|Server systému lokality|  
|enrollmentservice.log|Zaznamenává komunikaci mezi zprostředkujícím bodem registrace a bodem registrace.|Server systému lokality|  
|SMS_DM.log|Zaznamenává komunikaci mezi mobilními zařízeními, počítači Mac a bodem správy, který je povolený pro mobilní zařízení a počítače Mac.|Server systému lokality|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Konektor systému Exchange Server

Následující protokoly obsahují informace týkající se konektoru serveru Exchange Server.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Zaznamenává aktivity a stav konektoru Exchange Serveru.|Server lokality|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> Starší mobilní zařízení

Následující tabulka uvádí protokoly, které obsahují informace související se staršími mobilními zařízeními.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Zaznamenává údaje o datech zápisu certifikátu u starších verzí klientů mobilních zařízení.|Klient|  
|DMCertResp.htm|Zaznamenává odpověď protokolu HTML z certifikačního serveru, pokud program registrace klientů mobilních zařízení starších verzí vyžaduje certifikát PKI.|Klient|  
|DmClientHealth.log|Zaznamenává identifikátory GUID všech starších verzí klientů mobilních zařízení komunikujících s bodem správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DmClientRegistration.log|Zaznamenává žádosti o registraci a odpovědi do a ze starších verzí klientů mobilních zařízení.|Server systému lokality|  
|DmClientSetup.log|Zaznamenává data instalací klientů pro starší verze klientů mobilních zařízení.|Klient|  
|DmClientXfer.log|Zaznamenává data přenosu klientů pro starší verze klientů mobilních zařízení a pro nasazení ActiveSync.|Klient|  
|DmCommonInstaller.log|Zaznamenává instalaci souborů přenosu klientů pro konfiguraci přenosu souborů starších verzí klientů mobilních zařízení.|Klient|  
|DmInstaller.log|Zaznamenává, jestli DMInstaller správně volá DmClientSetup a jestli se DmClientSetup u starších verzí klientů mobilních zařízení ukončuje úspěšně či neúspěšně.|Klient|  
|DmpDatastore.log|Zaznamenává všechna připojení a dotazy databáze lokality provedené bodem správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DmpDiscovery.log|Zaznamenává všechna data zjišťování od starších verzí klientů mobilních zařízení v bodu správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DmpHardware.log|Zaznamenává data inventáře hardwaru od starších verzí klientů mobilních zařízení v bodu správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DmpIsapi.log|Zaznamenává komunikaci starších verzí klientů mobilních zařízení s bodem správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|dmpmsi.log|Zaznamenává data Instalační služby systému Windows pro konfiguraci bodu správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DMPSetup.log|Zaznamenává konfiguraci bodu správy, pokud je povolený pro mobilní zařízení.|Server systému lokality|  
|DmpSoftware.log|Zaznamenává data distribuce softwaru od starších verzí klientů mobilních zařízení v bodu správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DmpStatus.log|Zaznamenává data stavových zpráv od starších verzí klientů mobilních zařízení v bodu správy, který je povolený pro mobilní zařízení.|Server systému lokality|  
|DmSvc.log|Zaznamenává komunikaci klienta ze starších verzí klientů mobilních zařízení s bodem správy, který je povolený pro mobilní zařízení.|Klient|  
|FspIsapi.log|Zaznamenává údaje o komunikacích se záložním stavovým bodem ze starších klientů a počítačů klientů mobilních zařízení.|Server systému lokality|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a> Nasazení operačního systému

Následující tabulka uvádí soubory protokolů, které obsahují informace související s nasazením operačního systému.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|CAS.log|Zaznamenává údaje, pokud jsou nalezené distribuční body pro odkazovaný obsah.|Klient|  
|ccmsetup.log|Zaznamenává úlohy nástroje ccmsetup pro instalaci, upgrade a odebrání klienta. Dá se použít k odstraňování problémů instalace klienta.|Klient|  
|CreateTSMedia.log|Zaznamenává údaje pro vytváření médií sekvence úlohy.|Počítač se spuštěnou konzolou Configuration Manager|  
|Dism.log|Zaznamenává akce instalace ovladače nebo aktualizuje akce aplikace pro offline údržbu.|Server systému lokality|  
|Distmgr.log|Zaznamenává údaje o konfiguraci povolení distribučního bodu pro prostředí PXE (Preboot eXecution Environment).|Server systému lokality|  
|DriverCatalog.log|Zaznamenává údaje o ovladačích zařízení importovaných do katalogu ovladačů.|Server systému lokality|  
|mcsisapi.log|Zaznamenává informace pro vícesměrový přenos balíčků a odpovědi na požadavky klienta.|Server systému lokality|  
|mcsexec.log|Zaznamenává kontrolu stavu, obor názvů, vytvoření relace a akce kontroly certifikátu.|Server systému lokality|  
|mcsmgr.log|Zaznamenává změny konfigurace, režimu zabezpečení a dostupnosti.|Server systému lokality|  
|mcsprv.log|Zaznamenává interakci poskytovatele vícesměrového vysílání se službou Windows Deployment Services (WDS).|Server systému lokality|  
|MCSSetup.log|Zaznamenává údaje o instalaci role serveru vícesměrového vysílání.|Server systému lokality|  
|MCSMSI.log|Zaznamenává údaje o instalaci role serveru vícesměrového vysílání.|Server systému lokality|  
|Mcsperf.log|Zaznamenává údaje o aktualizace čítačů výkonu vícesměrového vysílání.|Server systému lokality|  
|MP_ClientIDManager.log|Zaznamenává odezvy bodu správy na ID klienta, které sekvence úloh začínají z prostředí PXE nebo ze spouštěcích médií.|Server systému lokality|  
|MP_DriverManager.log|Zaznamenává odezvy bodu správy na požadavky akce pořadí úloh pro automatické použití ovladačů.|Server systému lokality|  
|OfflineServicingMgr.log|Zaznamenává údaje o plánech offline údržby a akcích použití aktualizací pro soubory ve formátu WIM (Windows Imaging Format) operačního systému.|Server systému lokality|  
|Setupact.log|Podrobnosti záznamu týkající se nástroje Sysprep systému Windows a protokolů nastavení. Další informace najdete v tématu [soubory protokolu](/windows/deployment/upgrade/log-files).|Klient|  
|Setupapi.log|Podrobnosti záznamu týkající se nástroje Sysprep systému Windows a protokolů nastavení.|Klient|  
|Setuperr.log|Podrobnosti záznamu týkající se nástroje Sysprep systému Windows a protokolů nastavení.|Klient|  
|smpisapi.log|Zaznamenává údaje o akcích zachytávání a obnovy stavu klienta a o prahových informacích.|Klient|  
|Smpmgr.log|Zaznamenává údaje o výsledcích kontrol stavu bodu migrace stavu a o změnách konfigurace.|Server systému lokality|  
|smpmsi.log|Zaznamenává údaje o instalaci a konfiguraci bodu migrace stavu.|Server systému lokality|  
|smpperf.log|Zaznamenává aktualizace čítače výkonů bodu migrace stavu.|Server systému lokality|  
|smspxe.log|Zaznamenává údaje o odpovědích na klienty, kteří používají spouštění pomocí technologie PXE, a údaje o rozšíření spouštěcích imagí a spouštěcích souborů.|Server systému lokality|  
|smssmpsetup.log|Zaznamenává údaje o instalaci a konfiguraci bodu migrace stavu.|Server systému lokality|
| SMS_PhasedDeployment. log| Soubor protokolu pro dvoufázové nasazení|Lokalita nejvyšší úrovně v hierarchii Configuration Manager|
|Smsts.log|Zaznamenává aktivity pořadí úloh.|Klient|  
|TSAgent.log|Zaznamenává výsledek závislosti pořadí úloh před spuštěním pořadí úloh.|Klient|  
|TaskSequenceProvider.log|Zaznamenává údaje o pořadí úloh při jejich importu, exportu nebo úpravách.|Server systému lokality|  
|loadstate.log|Zaznamenává údaje o nástroji přenesení stavu uživatele (USMT) a obnově dat o stavu uživatele.|Klient|  
|scanstate.log|Zaznamenává údaje o nástroji přenesení stavu uživatele (USMT) a zaznamenávání dat o stavu uživatele.|Klient|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a> Řízení spotřeby

Následující tabulka uvádí soubory protokolů, které obsahují informace související s řízením spotřeby.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Zaznamenává údaje o aktivitách řízení spotřeby na klientském počítači, včetně monitorování a vynucení nastavení klientským agentem pro řízení spotřeby.|Klient|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a> Vzdálené řízení

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se vzdáleného řízení.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Zaznamenává údaje o aktivitě prohlížeče vzdáleného řízení.|V počítači, na kterém je spuštěný prohlížeč vzdáleného řízení, ve složce% Temp%.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a> Zpravodajský

V následující tabulce jsou uvedeny soubory protokolu Configuration Manager, které obsahují informace související s vytvářením sestav.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Zaznamenává údaje o aktivitě a stavu bodu služeb generování sestav.|Server systému lokality|  
|srsrpMSI.log|Zaznamenává podrobné výsledky procesu instalace bodu služeb generování sestav z výstupu MSI.|Server systému lokality|  
|srsrpsetup.log|Zaznamenává výsledky procesu instalace bodu služeb generování sestav.|Server systému lokality|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a> Správa na základě rolí

Následující tabulka uvádí soubory protokolů, které obsahují informace související s řízením správy na základě rolí.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|hman.log|Zaznamenává informace o změnách konfigurace lokality a o publikování informací o lokalitě pro Active Directory Domain Services.|Server lokality|  
|SMSProv.log|Zaznamenává přístup poskytovatele služby WMI k databázi lokality.|Počítač obsahující poskytovatele serveru SMS|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a> Monitorování míry využívání softwaru

Následující tabulka uvádí soubory protokolů, které obsahují informace související s měřením softwaru.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitoruje všechny procesy kontroly softwaru.|Server lokality|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a> Aktualizace softwaru

Následující tabulka uvádí soubory protokolu, které obsahují informace týkající se aktualizací softwaru.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|AlternateHandler. log|Zaznamenává údaje, když klient zavolá rozhraní COM Klikni a spusť ke stažení a instalaci aplikací Microsoft 365 pro aktualizace podnikového klienta. Je podobná použití WuaHandler při volání rozhraní API agenta web Windows Update ke stažení a instalaci aktualizací Windows.<!-- SCCMDocs#888 -->|Klient|
|ccmperf.log|Zaznamenává činnosti týkající se správy a sběru dat v závislosti na čítačích výkonu klienta.|Klient|
|DeltaDownload. log|Zaznamenává informace o stažení expresních aktualizací a aktualizací stažených pomocí optimalizace doručování.|Klient|  
|PatchDownloader.log|Zaznamenává údaje o procesu stahování aktualizací softwaru ze zdroje aktualizací do cílového umístění stahování na serveru lokality.|Když se aktualizace stahují ručně, tento soubor protokolu se nachází v adresáři% Temp% uživatele, který spouští konzolu na počítači, na kterém je spuštěná konzola nástroje. Pro pravidla automatického nasazení je tento soubor protokolu umístěn na serveru lokality v%windir%\CCM\Logs, pokud je klient nástroje ConfigMgr nainstalován na serveru lokality.|  
|PolicyEvaluator.log|Zaznamenává údaje o vyhodnocení zásad na klientských počítačích, včetně zásad z aktualizací softwaru.|Klient|  
|RebootCoordinator.log|Zaznamenává údaje o koordinaci restartování systému na klientských počítačích po dokončení instalací aktualizace softwaru.|Klient|  
|ScanAgent.log|Zaznamenává údaje o požadavcích na skenování pro aktualizace softwaru, umístění služby WSUS a souvisejících akcích.|Klient|  
|SdmAgent.log|Zaznamenává údaje o sledování nápravy a dodržování předpisů. Soubor protokolu aktualizací softwaru, Updateshandler. log, ale poskytuje podrobnější informace o instalaci aktualizací softwaru, které jsou požadovány pro dodržování předpisů. Tento protokol je sdílený s nastavením dodržování předpisů.|Klient|  
|ServiceWindowManager.log|Zaznamenává údaje o vyhodnocení oken údržby.|Klient|
|SMS_ISVUPDATES_SYNCAGENT. log| Soubor protokolu pro synchronizaci aktualizací softwaru třetích stran.| Bod aktualizace softwaru nejvyšší úrovně v hierarchii Configuration Manager.|
|SMS_OrchestrationGroup. log| Soubor protokolu pro skupiny orchestrace|Server lokality|
|SmsWusHandler.log|Zaznamenává údaje týkající se procesu skenování pro nástroj inventáře pro aktualizace od Microsoftu.|Klient|  
|StateMessage.log|Zaznamenává údaje o stavových zprávách aktualizace softwaru, které jsou vytvořeny a odesílány do bodu správy.|Klient|  
|SUPSetup.log|Zaznamenává údaje o instalaci bodu aktualizací softwaru. Po dokončení instalace bodu aktualizací softwaru se do tohoto souboru protokolu zapíše text **Instalace byla úspěšná**.|Server systému lokality|  
|UpdatesDeployment.log|Zaznamenává údaje o nasazení u klienta, včetně aktivace aktualizace softwaru, vyhodnocení a vynucení. Podrobné protokolování poskytuje další informace o interakci s uživatelským rozhraním klienta.|Klient|  
|UpdatesHandler.log|Zaznamenává údaje o dodržování shody aktualizací softwaru a o stažení a instalaci aktualizací softwaru u klienta.|Klient|  
|UpdatesStore.log|Zaznamenává údaje o dodržování shody aktualizací softwaru posouzené v průběhu cyklu prověřování shody.|Klient|  
|WCM.log|Zaznamenává údaje o konfiguracích bodu aktualizace softwaru a připojení k serveru WSUS pro odebírané kategorie, klasifikace a jazyky aktualizací.|Server lokality|  
|WSUSCtrl.log|Zaznamenává údaje o konfiguraci, připojení databáze a stavu serveru služby WSUS pro lokalitu.|Server systému lokality|  
|wsyncmgr.log|Zaznamenává údaje o procesu synchronizace aktualizací softwaru.|Server lokality|  
|WUAHandler.log|Zaznamenává údaje o agentovi služby Windows Update u klienta při vyhledávání aktualizací softwaru.|Klient|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a> Wake On LAN

Následující tabulka uvádí soubory protokolů, které obsahují informace související s používáním Wake On LAN.  

> [!NOTE]  
> Když doplníte Wake On LAN pomocí proxy probuzení, tato aktivita se zaprotokoluje na straně klienta. Příklad naleznete v části Ccmexec. log a SleepAgent_<*Domain* \> @SYSTEM_0.log v části [operace klienta](#BKMK_ClientOpLogs) tohoto článku.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Zaznamenává údaje o tom, kterým klientům se mají odeslat pakety pro buzení ze spánku, počet odeslaných paketů pro buzení a počet paketů pro buzení s opakovaným pokusem o odeslání.|Server lokality|  
|wolmgr.log|Zaznamenává údaje o postupech buzení, jako např. kdy budit nasazení, která jsou nakonfigurovaná pro funkci Wake On LAN.|Server lokality|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a> Údržba Windows 10

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se údržby Windows 10.  
Údržba používá stejnou infrastrukturu a proces jako aktualizace softwaru. Další protokoly použitelné pro scénář údržby najdete v tématu [aktualizace softwaru](#BKMK_SU_NAPLog).

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|CBS. log|Zaznamenává selhání obsluhy související se změnami pro aktualizace nebo role a funkce systému Windows.|Klient|
|DISM. log|Zaznamenává všechny akce pomocí nástroje DISM. V případě potřeby bude nástroj DISM. log odkazovat na protokol CBS. log, kde najdete další podrobnosti.|Klient|
|Setupact. log|Primární soubor protokolu pro většinu chyb, ke kterým došlo během procesu instalace systému Windows. Soubor protokolu je umístěný ve složce% Windir% \$ Windows. ~ BT\sources\panther.|Klient|

Další informace najdete v tématu [soubory protokolu týkající se údržby online](/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files).

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a> Agent web Windows Update

Následující tabulka uvádí soubory protokolu, které obsahují informace týkající se agenta služby Windows Update.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Zaznamenává údaje o tom, kdy se agent web Windows Update připojí k serveru WSUS a načítá aktualizace softwaru pro posouzení dodržování předpisů a zda jsou k dispozici aktualizace komponent agenta.|Klient|  

Další informace najdete v tématu [web Windows Update souborů protokolu](/windows/deployment/update/windows-update-logs).

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a> Server WSUS

Následující tabulka uvádí soubory protokolů, které obsahují informace týkající se serveru WSUS.  

|Název protokolu|Popis|Počítač obsahující soubor protokolu|  
|--------------|-----------------|----------------------------|  
|Change.log|Zaznamenává údaje o informacích o databázi serveru WSUS, které se změnily.|Server služby WSUS|  
|SoftwareDistribution.log|Zaznamenává údaje o aktualizacích softwaru synchronizovaných z nakonfigurovaného zdroje aktualizací s databází serveru WSUS.|Server služby WSUS|  

Tyto soubory protokolu jsou umístěné ve `%ProgramFiles%\Update Services\LogFiles` složce.

## <a name="see-also"></a>Viz také

- [Informace o souborech protokolu](about-log-files.md)

- [OneTrace Support Center](../../support/support-center-onetrace.md)

- [Prohlížeč souborů protokolu Support Center](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
