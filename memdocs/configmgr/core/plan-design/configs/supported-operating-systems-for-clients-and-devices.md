---
title: Podporovaní klienti a zařízení
titleSuffix: Configuration Manager
description: Zjistěte, které verze operačního systému Configuration Manager podporuje pro klienty a zařízení.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 497a43fe6647f1dc2787f16a76f45ddd26d24796
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128844"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Podporované verze operačních systémů pro klienty a zařízení pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje instalaci klientského softwaru do počítačů s Windows a macOS.  

## <a name="general-requirements-and-limitations"></a>Obecné požadavky a omezení

Zkontrolujte následující požadavky a omezení pro všechny klienty:

- Změna typu spuštění nebo **přihlášení jako** nastavení pro jakoukoli službu Configuration Manager není podporovaná. Tato změna může zabránit správnému fungování služby Key Services.

## <a name="windows-computers"></a>Počítače s Windows  

Ke správě následujících verzí operačních systémů Windows použijte klienta, který je součástí nástroje Configuration Manager. Další informace najdete v tématu [nasazení klientů do počítačů se systémem Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Podporované verze operačního systému klienta

- **Windows 10**  

    Podrobnější informace najdete v tématu [Podpora pro Windows 10](support-for-windows-10.md).  

- **Windows 8.1** (x86, x64): Professional, Enterprise

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Virtuální plocha Windows](https://docs.microsoft.com/azure/virtual-desktop/) je služba virtualizace plochy a aplikací, která běží na Microsoft Azure. Počínaje verzí 1906 použijte Configuration Manager ke správě těchto virtuálních zařízení s Windows v Azure.

Podobně jako terminálový server, některá z těchto virtuálních zařízení umožňují více souběžných aktivních uživatelských relací. Kvůli lepšímu výkonu klienta Configuration Manager nyní zakáže zásady uživatele na jakémkoli zařízení, které umožňuje tyto více uživatelských relací. I když zásady uživatele povolíte, klient je ve výchozím nastavení standardně zakáže na těchto zařízeních, která zahrnují víc relací a terminálových serverů s Windows 10 Enterprise.

Klient zakáže zásady uživatele pouze v případě, že během nové instalace detekuje tento typ zařízení. Pro existujícího klienta tohoto typu, který aktualizujete na tuto verzi, bude předchozí chování trvat dál. V existujícím zařízení nakonfiguruje nastavení zásad uživatele i v případě, že zjistí, že zařízení umožňuje více uživatelských relací.

Pokud v tomto scénáři požadujete zásady uživatele a souhlasíte s případným dopadem na výkon, použijte k povolení zásad uživatele jednu z následujících metod:

- Ve verzi 1910 a novější použijte [nastavení klienta](../../clients/deploy/configure-client-settings.md). Ve skupině **zásad klienta** nakonfigurujte následující nastavení: **Povolit zásady uživatele pro více uživatelských relací**.<!-- 4737447 -->

- Ve verzi 1906 použijte sadu Configuration Manager SDK se [třídou WMI serveru SMS_PolicyAgentConfig](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Nastavte novou `PolicyEnableUserPolicyOnTS` vlastnost na `true` .

> [!Note]  
> Spolusprávu nemůžete použít u klienta s Windows 10 Enterprise více relacemi. <!-- SCCMDocs-pr#3950 -->

Počínaje verzí 2006 je platforma pro **více relací Windows 10 Enterprise** dostupná v seznamu podporovaných verzí operačního systému u objektů s pravidly požadavků nebo seznamy použitelnosti.<!--6527576-->

> [!NOTE]
> Pokud jste dříve vybrali platformu **Windows 10** na nejvyšší úrovni, tato akce automaticky vybere všechny podřízené platformy. Tato nová platforma není automaticky vybraná. Pokud chcete přidat **víc relací Windows 10 Enterprise**, vyberte ji v seznamu ručně.

Další informace najdete v následujících článcích:

- [Podpora virtualizovaných prostředí](support-for-virtualization-environments.md)
- [Správa klientů Configuration Manager v infrastruktuře virtuálních klientských počítačů (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### <a name="supported-server-os-versions"></a>Podporované verze operačního systému serveru

- **Windows Server 2019**: Standard, Datacenter – <sup> [Poznámka 1](#bkmk_note1)</sup>  
    (Počínaje verzí 1806 Configuration Manager.)

- **Windows Server 2016**: Standard, Datacenter – <sup> [Poznámka 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: pracovní skupina, Standard  

- **Windows Server 2012 R2** (x64): Standard, Datacenter – <sup> [Poznámka 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter – <sup> [Poznámka 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Jádro serveru

Následující verze konkrétně odkazují na instalaci jádra serveru operačního systému. <sup>[Poznámka 3](#bkmk_note3)</sup>  

Pololetní verze kanálů Windows serveru jsou instalace jádra serveru, jako je Windows Server verze 1809. Jako klient Configuration Manager se podporují stejně jako související verze Windows 10 s poloviční roční verzí. Další informace najdete v tématu [Podpora pro Windows 10](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup> [Poznámka 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup> [Poznámka 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup> [Poznámka 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup> [Poznámka 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a>Poznámka 1

Configuration Manager testuje a podporuje edice Windows serveru Datacenter, ale není oficiálně certifikováno pro Windows Server. Podpora Configuration Manager hotfix není nabízena pro problémy, které jsou specifické pro Windows Server Datacenter Edition. Další informace o certifikaci Windows serveru najdete v tématu [katalog Windows serveru](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a>Poznámka 2

Chcete-li podporovat [nabízenou instalaci klienta](../../clients/deploy/plan/client-installation-methods.md#client-push-installation), přidejte službu souborového serveru role serveru souborové služby a služby úložiště. Další informace o instalaci funkcí Windows na jádro serveru najdete v tématu [Instalace rolí, služeb rolí a funkcí pomocí rutin prostředí Windows PowerShell](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="note-3"></a><a name="bkmk_note3"></a>Poznámka 3

Nová aplikace centra softwaru se nepodporuje v žádné verzi jádra Windows serveru.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Počítače se systémem Windows Embedded  

Spravovat zařízení se systémem Windows Embedded instalací klienta Configuration Manager do zařízení. Další informace najdete v tématu [Plánování nasazení klientů na zařízení se systémem Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Požadavky a omezení

- Všechny klientské funkce jsou podporovány v systémech Windows Embedded, které nemají povolené filtry zápisu.  

- Klienti, kteří používají jednu z následujících možností, jsou podporovány pro všechny funkce kromě řízení spotřeby:  

  - Vylepšené filtry zápisu (EWF)

  - Filtry zápisu založené na souborech RAM (FBWF)

  - Sjednocené filtry zápisu (UWF)  

- Pro žádné zařízení se systémem Windows Embedded není katalog aplikací podporován.  

### <a name="supported-os-versions"></a>Podporované verze operačního systému  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Tato verze zahrnuje kanál pro dlouhodobé obsluhy (LTSC). Další informace najdete v tématu [Přehled Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8,1 – obor** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows tenký počítač** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 s aktualizací SP1** (x86, x64)

## <a name="windows-ce-computers"></a>systém Windows CE počítače

Správa zařízení systém Windows CE pomocí Configuration Manager starší verze klienta mobilních zařízení, která je součástí Configuration Manager.  

### <a name="requirements-and-limitations"></a>Požadavky a omezení

- Klient mobilního zařízení vyžaduje 0,78 MB úložného prostoru pro instalaci. Přihlášení může vyžadovat až 256 KB dalšího úložného prostoru.

- Funkce pro tato mobilní zařízení se liší podle typu platformy a klienta. Informace o podporovaných funkcích správy najdete v tématu [Volba řešení pro správu zařízení](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>Podporované verze operačního systému

- Systém Windows CE 7,0 (procesory ARM a x86)  

    > [!IMPORTANT]
    > Configuration Manager verze 2006 vyřazuje podporu systém Windows CE 7,0 jako klienta. Vyřazení bylo oznámeno [verzí 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

#### <a name="supported-languages-include"></a>Mezi podporované jazyky patří

- Čínština (zjednodušená a tradiční)

- Angličtina (USA)

- francouzština (Francie)

- Němčina

- Italština

- Japonština  

- Korejština  

- Portugalština (Brazílie)  

- Ruština  

- Španělština (Španělsko)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Rozšířené aktualizace zabezpečení a Configuration Manager

Program [Extended Security Updates (EVJ)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) je poslední možností pro zákazníky, kteří potřebují spouštět některé starší verze produktů Microsoftu po skončení podpory. Například Windows 7. Zahrnuje kritické a/nebo důležité aktualizace zabezpečení (definované [centrem MSRC (Microsoft Security Response Center)](https://www.microsoft.com/msrc)po dobu delší než tři roky po ukončení rozšířené podpory produktu.

Produkty, které přesahují životní cyklus podpory, se nepodporují pro použití s Configuration Manager. To zahrnuje všechny produkty, které jsou pokryté v programu EVJ. Aktualizace zabezpečení vydané v rámci programu EVJ budou publikovány ve službě Windows Server Update Services (WSUS). Tyto aktualizace se zobrazí v konzole Configuration Manager. I když produkty, které jsou pokryté programem EVJ, už nejsou podporované pro použití s Configuration Manager, [nejnovější vydanou verzi Configuration Manager aktuální větev](../../servers/manage/updates.md#version-details) můžete použít k nasazení a instalaci aktualizací zabezpečení systému Windows vydaných v rámci programu. Nejnovější vydanou verzi je taky možné použít k nasazení Windows 10 na zařízení s Windows 7.

Funkce správy klientů, které nesouvisejí se správou aktualizací softwaru systému Windows nebo nasazení operačního systému, již nebudou testovány v operačních systémech, které jsou zahrnuty v rámci programu EVJ, a nezaručujeme, že budou nadále fungovat. Pro příjem podpory správy klientů doporučujeme, abyste v nejbližší době provedli upgrade nebo migraci na aktuální verzi operačních systémů.

## <a name="mac-computers"></a>Počítače Mac  

Správa počítačů se systémem Mac Apple pomocí klienta Configuration Manager pro macOS.  

Instalační balíček klienta macOS se nedodává s médii Configuration Manager. Stáhněte si ho z webu Microsoft Download Center, [klienta Microsoft Endpoint Configuration Manager-MacOS (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850).  

Další informace najdete v tématu [nasazení klientů na počítače Mac](../../clients/deploy/deploy-clients-to-macs.md).  

### <a name="requirements-and-limitations"></a>Požadavky a omezení

- Instalace nebo spuštění klienta Configuration Manager pro macOS v počítačích pod jiným účtem než rootem se nepodporuje. V takovém případě může služba Key Services zabránit správnému fungování.  

### <a name="supported-versions"></a>Podporované verze

- **MacOS Catalina (10,15)** (vyžaduje Configuration Manager lokality verze 1910 nebo novější a Configuration Manager klient pro MacOS verze 5.0.8742.1000 nebo novější)

- **macOS Mojave (10,14)**

- **macOS High Sierra (10,13)**

## <a name="linux-and-unix-servers"></a>Servery se systémy Linux a UNIX  

> [!Important]  
> Configuration Manager verze 1902 vyřazuje podporu pro systémy Linux a UNIX jako klienta. Vyřazení bylo oznámeno [verzí 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Instalační balíčky klienta systému Linux a UNIX nejsou dodávány s Configuration Managerm médiem. Stáhněte si **klienty pro další operační systémy** z [webu Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Kromě instalačních balíčků klienta zahrnuje stažení klienta také skript, který spravuje instalaci klienta v každém počítači.  

### <a name="requirements-and-limitations"></a>Požadavky a omezení

- Informace o tom, jak zkontrolovat závislosti souborů operačního systému pro klienta pro Linux a UNIX, najdete v tématu [předpoklady pro nasazení klientů na servery se systémy Linux a UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Přehled podporovaných možností správy pro systémy Linux a UNIX najdete v tématu [postup nasazení klientů na servery se systémy UNIX a Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- V případě podporovaných verzí systémů Linux a UNIX uvedená verze obsahuje všechny následné dílčí verze. Například CentOS verze 6 zahrnuje CentOS 6,3. Podobně podpora operačního systému, který používá aktualizace Service Pack (například SUSE Linux Enterprise Server 11 SP1), zahrnuje další aktualizace Service Pack pro danou verzi operačního systému.  

- Informace o instalačních balíčcích klienta a univerzálním agentovi najdete v tématu [postup nasazení klientů na servery se systémy UNIX a Linux](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Podporované verze

Následující verze jsou podporovány pomocí uvedeného souboru. tar.  

#### <a name="aix"></a>AIX  

|Verze|Soubor TAR|  
|-|-|  
|Verze 6,1 (výkon)|ccm-Aix61ppc. &lt; Build \> . tar|  
|Verze 7,1 (výkon)|ccm-Aix71ppc. &lt; Build \> . tar|  

#### <a name="centos"></a>CentOS  

|Verze|Soubor TAR|  
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  

#### <a name="debian"></a>Debian  

|Verze|Soubor TAR|  
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 8 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 8 x64|ccm-Universalx64. &lt; Build \> . tar|  

#### <a name="hp-ux"></a>HP-UX  

|Verze|Soubor TAR|  
|-|-|  
|11iv3 verze IA64|ccm-HpuxB. 11.31 I64. &lt; Build \> . tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Verze|Soubor TAR|  
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Verze|Soubor TAR|  
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  

#### <a name="solaris"></a>Solaris  

|Verze|Soubor TAR|  
|-|-|  
|Verze 10 x86|ccm-Sol10x86. &lt; Build \> . tar|  
|Verze 10 SPARC|ccm-Sol10sparc. &lt; Build \> . tar|  
|Verze 11 x86|ccm-Sol11x86. &lt; Build \> . tar|  
|SPARC verze 11|ccm-Sol11sparc. &lt; Build \> . tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Verze|Soubor TAR|  
|-|-|  
|Verze 10 SP1 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 10 SP1 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 11 SP1 – x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 11 SP1 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 12 x64|ccm-Universalx64. &lt; Build \> . tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Verze|Soubor TAR|  
|-|-|  
|Verze 10,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 10,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 12,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 12,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 14,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 14,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 16,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 16,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a>Místní MDM

Configuration Manager obsahuje integrované funkce pro správu mobilních zařízení, která jsou místně bez instalace klientského softwaru. Další informace najdete v tématu [Správa mobilních zařízení s místní infrastrukturou](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Podporované operační systémy

- **Windows 10 pro** (x86, x64)  

- **Windows 10 pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Tato verze zahrnuje kanál pro dlouhodobé obsluhy (LTSC). Další informace najdete v tématu [Přehled Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team pro Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!IMPORTANT]
    > Configuration Manager verze 2006 vyřazuje podporu pro Windows 10 Mobile a Windows 10 Mobile Enterprise jako klienta. Vyřazení bylo oznámeno [verzí 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a>Konektor systému Exchange Server  

Configuration Manager podporuje omezené řízení zařízení, která se připojují k serveru Exchange bez instalace klienta Configuration Manager. Další informace najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Podporované verze systému Exchange Server

- **Exchange Online (Office 365)**: Tato verze zahrnuje sadu Online Standard pro produktivitu firmy.  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange server 2010 SP1** nebo **Exchange Server 2010 SP2**
