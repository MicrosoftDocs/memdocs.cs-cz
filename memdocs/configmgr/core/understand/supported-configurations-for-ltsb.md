---
title: 'Podporované konfigurace pro LTSB '
titleSuffix: Configuration Manager
description: Pochopte, jaké operační systémy a závislé produkty pracují s System Center Configuration Managerou dlouhodobou obsluhu.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60d08d04e2b2cb37dc7751fee0673fa8703d1865
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994442"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Podporované konfigurace pro větev dlouhodobé údržby System Center Configuration Manager

*Platí pro: System Center Configuration Manager (větev dlouhodobé údržby)*

Informace v tomto tématu vám pomohou pochopit, jaké operační systémy a závislosti produktů jsou podporovány větví LTSB (Long-Term Servicing Branch) Configuration Manager.
Pokud není uvedeno jinak v tomto nebo LTSB konkrétní témata, vztahují se na LTSB stejné konfigurace a omezení, které platí pro Current Branch verze 1606.  Pokud dojde ke konfliktům, použijte informace, které se vztahují na edici, kterou používáte. LTSB je typicky omezené, než Current Branch.

## <a name="general-statement-of-support"></a>Obecné prohlášení o podpoře
Tato větev Configuration Manager podporuje následující produkty a technologie. Jejich zahrnutí do tohoto obsahu však nevyjadřuje rozšíření podpory pro žádné produkty ani verze, které přesahují jednotlivé životní cyklus podpory daného produktu. Produkty, které přesahují životní cyklus podpory, se nepodporují pro použití s Configuration Manager. Další informace najdete na webu [životního cyklu podpora Microsoftu](https://support.microsoft.com/lifecycle) a přečtěte si nejčastější dotazy k podpora Microsoftu zásad životního cyklu.

Produkty a verze produktů, které nejsou uvedené v následujících tématech, se navíc nepodporují, pokud nejsou ohlášeny na [blogu Enterprise mobility + Security](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).

**Omezení pro budoucí podporu:** LTSB má omezené podpory pro budoucí serverové a klientské operační systémy a závislosti produktů. Seznam platforem pro LTSB je vyřešen po dobu životnosti verze:

**Systému**
- Podporují se jenom aktualizace kvality a zabezpečení pro Windows.
- Nepřidala se žádná podpora pro aktuální větve (ta), aktuální pobočky pro firmy (CBB) nebo LTSB Windows 10.
- Pro nové hlavní verze Windows serveru není podporovaná žádná podpora.

**SQL Server:**
- Pro SQL Server je podporována pouze aktualizace kvality a zabezpečení nebo méně upgrady jako aktualizace Service Pack.
- Žádná podpora pro nové hlavní verze SQL Server.  

## <a name="site-systems-and-servers"></a>Systémy lokality a servery
LTSB podporuje používání následujících počítačových operačních systémů Windows jako systémů lokality.  Každý operační systém má stejné požadavky a omezení jako stejná položka v [podporovaných operačních systémech pro servery systému lokality](../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  Například instalace jádra serveru systému Windows 2012 R2 musí mít verzi x64, která je podporována pouze pro hostování distribučního bodu a nepodporuje technologii PXE ani vícesměrové vysílání.

**Podporované operační systémy:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Instalace jádra serveru systému Windows Server 2012
- Instalace jádra serveru systému Windows Server 2012 R2

## <a name="client-management"></a>Správa klientů
Následující části identifikují klientské operační systémy, které můžete spravovat pomocí nástroje LTSB. LTSB nepodporuje přidání nových operačních systémů jako podporovaných klientů.

### <a name="windows-computers"></a>Počítače s Windows
Pomocí nástroje LTSB můžete spravovat následující počítačové operační systémy Windows s klientským softwarem Configuration Manager, který je součástí Configuration Manager. Další informace najdete v tématu [nasazení klientů do počítačů se systémem Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

**Podporované operační systémy:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Poznámka 1)
- Windows Server 2012 (x64): Standard, Datacenter (Poznámka 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Instalace jádra serveru systému Windows Server 2012 R2 (x64) (Poznámka 2)
- Instalace jádra serveru systému Windows Server 2012 (x64) (Poznámka 2)

**(Poznámka 1)** Vydání Datacenter jsou podporovaná, ale nejsou certifikované pro Configuration Manager.  
**(Poznámka 2)** Aby bylo možné podporovat nabízenou instalaci klienta, musí počítač, který spouští tuto verzi operačního systému, spustit službu role souborový server pro roli serveru Souborová služba a služba úložiště. Informace o instalaci funkcí Windows na počítači s jádrem serveru najdete v tématu [Instalace rolí serveru a funkcí na server s jádrem serveru](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11)).

### <a name="windows-embedded"></a>Windows Embedded
Pomocí nástroje LTSB můžete spravovat následující zařízení se systémem Windows Embedded, a to tak, že na zařízení nainstalujete klientský software.  Další informace najdete v tématu [Plánování nasazení klientů na zařízení se systémem Windows Embedded](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

**Požadavky a omezení:**  

-   Všechny klientské funkce jsou podporovány v podporovaných systémech Windows Embedded, které nemají povolené filtry zápisu.  

-   Klienti, kteří používají jednu z následujících možností, jsou podporovány pro všechny funkce kromě řízení spotřeby:  

    -   Vylepšené filtry zápisu (EWF)    

    -   Filtry zápisu založené na souborech RAM (FBWF)    

    -   Sjednocené filtry zápisu (UWF)  

-   Pro žádné zařízení se systémem Windows Embedded není katalog aplikací podporován.  

-   Než budete moct monitorovat zjištěné malware na zařízeních se systémem Windows Embedded založených na systému Windows XP, je nutné na integrovaném zařízení nainstalovat balíček Microsoft Windows WMI pro skriptování. K instalaci tohoto balíčku použijte Windows Embedded Target Designer. *WBEMDISP.DLL* a *WBEMDISP. *Aby bylo možné zjistit, zda byl zjištěn malware, musí existovat soubory TLB a musí být registrovány ve složce%windir%\system32\wbem v integrovaném zařízení.  

**Podporované operační systémy:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8,1 – obor (x86, x64)    
-   Windows tenký počítač (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 s aktualizací SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Zařízení systém Windows CE můžete spravovat pomocí Configuration Manager starší verze klienta pro mobilní zařízení, která je součástí Configuration Manager.  

**Požadavky a omezení:**  

-   Klient mobilního zařízení vyžaduje 0,78 MB úložného prostoru pro instalaci klienta. Mobilní zařízení může vyžadovat až 256 KB dalšího úložného prostoru pro přihlášení.    

-   Funkce pro tato mobilní zařízení se liší podle typu platformy a klienta. Informace o druhu funkcí správy, které Configuration Manager podporuje pro starší verze klienta mobilních zařízení, najdete v tématu [Výběr řešení správy zařízení pro Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Podporované operační systémy:**  

-   Systém Windows CE 7,0 (procesory ARM a x86)  

**Mezi podporované jazyky patří:**  
-   Čínština (zjednodušená a tradiční)    
-   Angličtina (USA)    
-   francouzština (Francie)    
-   Němčina    
-   Italština    
-   Japonština  
-   Korejština  
-   Portugalština (Brazílie)  
-   Ruština  
-   Španělština (Španělsko)  

### <a name="mac-computers"></a>Počítače Mac  
 LTSB můžete použít ke správě počítačů s Mac OS X pomocí klienta Configuration Manager pro Mac.

Instalační balíček klienta pro systém Mac není dodáván s Configuration Managerm médiu. Můžete si ho stáhnout jako součást "klienti pro další operační systémy" na webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719).  

Podpora pro operační systémy Mac je omezená na ty, které jsou uvedené v této části. Podpora nezahrnuje další operační systémy, které by mohly být podporovány v budoucí aktualizaci instalačních balíčků klienta systému Mac pro Current Branch.

Další informace najdete v tématu [nasazení klientů na počítače Mac](../clients/deploy/deploy-clients-to-macs.md).

**Podporované verze:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servery se systémy Linux a UNIX
LTSB můžete použít ke správě serverů se systémy Linux a UNIX pomocí klienta Configuration Manager pro systémy Linux a UNIX.

Instalační balíčky klienta systému Linux a UNIX nejsou dodávány s Configuration Managerm médiem. Můžete si je stáhnout jako součást "klienti pro další operační systémy" stažení z [webu Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Vedle instalačních balíčků klienta zahrnuje stažení klienta také skript install , který spravuje instalaci klienta v jednotlivých počítačích.

Podpora pro operační systémy Linux a UNIX je omezená na ty, které jsou uvedené v této části. Podpora nezahrnuje další operační systémy, které by mohly být podporovány v budoucí aktualizaci balíčků klientů se systémy Linux a UNIX pro Current Branch.

**Požadavky a omezení:**  

-   Informace o závislostech souborů operačních systémů pro klienta nástroje pro Linux a UNIX najdete v tématu [předpoklady pro nasazení klientů na servery se systémy Linux a UNIX](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  
-   Přehled možností správy podporovaných pro počítače se systémem Linux nebo UNIX najdete v tématu [postup nasazení klientů na servery se systémy UNIX a Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  
-   V případě podporovaných verzí systémů Linux a UNIX uvedená verze obsahuje všechny následné dílčí verze. Například v případě, že je pro CentOS verze 6 uvedena podpora, zahrnuje také všechny následné podverze CentOS 6, jako je například CentOS 6,3. Podobně platí, že pokud je uvedena podpora pro operační systém, který používá aktualizace Service Pack, například SUSE Linux Enterprise Server 11 SP1, podpora zahrnuje i další aktualizace Service Pack pro danou verzi operačního systému.
-   Informace o instalačních balíčcích klienta a univerzálním agentovi najdete v tématu [postup nasazení klientů na servery se systémy UNIX a Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).


**Podporované verze:**   
Následující verze jsou podporovány pomocí uvedeného souboru. tar.  
### <a name="aix"></a>AIX  

|Verze|Soubor|  
|-|-|  
|Verze 5,3 (výkon)|ccm-Aix53ppc. &lt; Build \> . tar|  
|Verze 6,1 (výkon)|ccm-Aix61ppc. &lt; Build \> . tar|  
|Verze 7,1 (výkon)|ccm-Aix71ppc. &lt; Build \> . tar|  

### <a name="centos"></a>CentOS  

|Verze|Soubor|  
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  

### <a name="debian"></a>Debian  

|Verze|Soubor|    
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|6x86 verze|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 8 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 8 x64|ccm-Universalx64. &lt; Build \> . tar|  

### <a name="hp-ux"></a>HP-UX  

|Verze|Soubor|  
|-|-|  
|11iv2 verze IA64|ccm-HpuxB. 11.23 I64. &lt; Build \> . tar|  
|Verze 11iv2 PA – RISC|ccm-HpuxB. 11.23 PA. &lt; Build \> . tar|  
|11iv3 verze IA64|ccm-HpuxB. 11.31 I64. &lt; Build \> . tar|  
|Verze 11iv3 PA – RISC|ccm-HpuxB. 11.31 PA. &lt; Build \> . tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Verze|Soubor|    
|-|-|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Verze|Soubor|  
|-|-|  
|Verze 4 x86|ccm-RHEL4x86. &lt; Build \> . tar|  
|Verze 4 x64|ccm-RHEL4x64. &lt; Build \> . tar|  
|Verze 5 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 5 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 6 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 6 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 7 x64|ccm-Universalx64. &lt; Build \> . tar|  

### <a name="solaris"></a>Solaris  

|Verze|Soubor|   
|-|-|  
|SPARC verze 9|ccm-Sol9sparc. &lt; Build \> . tar|  
|Verze 10 x86|ccm-Sol10x86. &lt; Build \> . tar|  
|Verze 10 SPARC|ccm-Sol10sparc. &lt; Build \> . tar|  
|Verze 11 x86|ccm-Sol11x86. &lt; Build \> . tar|  
|SPARC verze 11|ccm-Sol11sparc. &lt; Build \> . tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Verze|Soubor|  
|-|-|  
|Verze 9 x86|ccm-SLES9x86. &lt; Build \> . tar|  
|Verze 10 SP1 x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 10 SP1 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 11 SP1 – x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 11 SP1 x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 12 x64|ccm-Universalx64. &lt; Build \> . tar|  

### <a name="ubuntu"></a>Ubuntu  

|Verze|Soubor|    
|-|-|  
|Verze 10,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 10,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 12,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 12,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  
|Verze 14,04 LTS x86|ccm-Universalx86. &lt; Build \> . tar|  
|Verze 14,04 LTS x64|ccm-Universalx64. &lt; Build \> . tar|  

### <a name="exchange-server-connector"></a>konektor systému Exchange Server
 LTSB podporuje omezené řízení zařízení, která se připojují k vaší instanci Exchange serveru bez instalace klientského softwaru. Další informace najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Požadavky a omezení:**  

-   Configuration Manager nabízí omezené řízení pro mobilní zařízení. Omezená Správa je dostupná, když použijete konektory systému Exchange Server pro Exchange Active Sync (EAS), které se připojují k serveru se systémem Exchange Server nebo Exchange Online.  

-   Další informace o funkcích správy, které Configuration Manager podporuje pro mobilní zařízení, která spravuje konektor systému Exchange Server, najdete v tématu [Výběr řešení správy zařízení pro Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Podporované verze systému Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB nepodporuje správu zařízení, která se připojují prostřednictvím online služby, jako je Exchange Online (Microsoft 365).


## <a name="configuration-manager-console"></a>Konzola nástroje Configuration Manager
LTSB podporuje následující operační systémy pro spuštění konzoly Configuration Manager. Každý počítač, který je hostitelem konzoly nástroje, musí mít minimálně .NET Framework verze 4.5.2 s výjimkou Windows 10, která vyžaduje minimálně .NET Framework 4,6.

**Podporované operační systémy:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Verze SQL Server podporované pro databázi lokality a bod hlášení
LTSB podporuje následující verze SQL Server pro hostování databáze lokality a bodu hlášení. Pro každou podporovanou verzi platí stejné požadavky na konfiguraci a omezení, které se zobrazí v části [Podpora pro SQL Server verze](../plan-design/configs/support-for-sql-server-versions.md) Current Branch pro LTSB.  To zahrnuje použití SQL Server clusteru nebo skupiny dostupnosti SQL Server AlwaysOn.  

**Podporované verze:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Podpora domén služby Active Directory
Všechny systémy lokality LTSB musí být členy podporované domény služby Windows Active Directory. Podpora domén služby Active Directory má stejné požadavky a omezení jako ty, které se zobrazují v [podpoře domén služby Active Directory](../plan-design/configs/support-for-active-directory-domains.md), ale jsou omezené na následující úrovně funkčnosti domény:

**Podporované úrovně:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Další témata podpory, která se vztahují na větev dlouhodobé údržby
Informace v následujících tématech Current Branch se vztahují na LTSB:
- [Dimenzování a škálování](../plan-design/configs/size-and-scale-numbers.md)
- [Požadavky na lokality a systémy lokalit](../plan-design/configs/site-and-site-system-prerequisites.md)
- [Možnosti vysoké dostupnosti](../servers/deploy/configure/high-availability-options.md)
- [Doporučený hardware](../plan-design/configs/recommended-hardware.md)
- [Podpora pro funkce Windows a sítě](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Podpora virtualizovaných prostředí](../plan-design/configs/support-for-virtualization-environments.md)