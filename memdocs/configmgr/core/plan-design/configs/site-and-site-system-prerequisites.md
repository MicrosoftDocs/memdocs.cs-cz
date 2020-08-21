---
title: Požadavky na lokalitu
titleSuffix: Configuration Manager
description: Naučte se konfigurovat počítač s Windows jako server systému lokality Configuration Manager.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce3420a6e229b5987616c5c0c1c41d50cdc499c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700346"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Požadavky lokality a systému lokality pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Počítače se systémem Windows vyžadují konkrétní konfiguraci pro podporu jejich použití jako Configuration Manager serverů systému lokality.

U některých produktů, jako je například Windows Server Update Services (WSUS) pro bod aktualizace softwaru, je třeba si v dokumentaci k produktu najít další požadavky a omezení pro použití. Zde jsou uvedeny pouze konfigurace, které přímo platí pro použití s Configuration Manager.

Další informace o .NET Framework najdete v tématu [věnovaném životnímu cyklu nejčastějších dotazů – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Obecné požadavky a omezení

Pro všechny systémové servery lokality platí následující požadavky:

- Každý server systému lokality musí používat 64 operační systém. Jedinou výjimkou je role systému lokality distribučního bodu, kterou můžete nainstalovat na některé 32. bitové operační systémy.  

- Systémy lokality nejsou podporovány v instalacích jádra serveru v jakémkoli operačním systému. Výjimkou je, že instalace jádra serveru jsou podporovány pro roli systému lokality distribučního bodu. Další informace najdete v tématu [podporované operační systémy pro Configuration Manager servery systému lokality](supported-operating-systems-for-site-system-servers.md).  

- Po instalaci serveru systému lokality se změna nepodporuje:  

    - Název domény, ve které se počítač systému lokality nachází (označuje se také jako **přejmenování domény**).  

    - Členství počítače v doméně.  

    - Název počítače.  

    Pokud je nutné změnit některou z těchto položek, odeberte nejprve roli systému lokality z počítače. Po dokončení změny Přeinstalujte roli. V případě změn, které mají vliv na server lokality, nejprve odinstalujte lokalitu. Po dokončení změny přeinstalujte lokalitu.  

- Role systému lokality nejsou podporované v instanci clusteru Windows serveru. Jedinou výjimkou je server databáze lokality. Další informace najdete v tématu [použití SQL Serverho clusteru pro databázi Configuration Manager lokality](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    Počínaje verzí 1810 nebude proces instalace Configuration Manager nadále blokovat instalaci role serveru lokality do počítače s rolí systému Windows pro clustering s podporou převzetí služeb při selhání. SQL Always On vyžaduje tuto roli, takže dříve se nepovedlo společně najít databázi lokality na serveru lokality. Díky této změně můžete vytvořit vysoce dostupnou lokalitu s menším počtem serverů pomocí SQL Always On a serveru lokality v pasivním režimu. Další informace najdete v tématu [Možnosti vysoké dostupnosti](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- Pro žádnou Configuration Manager službu není možné změnit typ spouštění ani nastavení přihlásit se jako. Pokud to uděláte, můžete zabránit správnému fungování služby Key Services.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Předpoklady pro operační systémy Windows Server 2012 a novější  

V hlavních částech tohoto článku najdete konkrétní požadavky na servery a role systému lokality ve Windows Serveru 2012 a novějších verzích:

- [Lokalita centrální správy a servery primární lokality](#bkmk_2012sspreq)
- [Server sekundární lokality](#bkmk_2012secpreq)
- [Databázový server](#bkmk_2012dbpreq)
- [Server poskytovatele služby SMS](#bkmk_2012smsprovpreq)
- [Bod webu Katalog aplikací](#bkmk_2012acwspreq)
- [Bod služeb webu Katalog aplikací](#bkmk_2012ACwsitepreq)
- [funkce Asset Intelligence bod synchronizace](#bkmk_2012AIpreq)
- [Bod registrace certifikátu](#bkmk_2012crppreq)
- [Distribuční bod](#bkmk_2012dppreq)
- [Bod ochrany koncového bodu Endpoint Protection](#bkmk_2012EPPpreq)
- [Bod registrace](#bkmk_2012Enrollpreq)
- [Zprostředkující bod registrace](#bkmk_2012EnrollProxpreq)
- [Bod záložního stavu](#bkmk_2012FSPpreq)
- [Bod správy](#bkmk_2012MPpreq)
- [Bod služby Reporting Services](#bkmk_2012RSpoint)
- [Bod připojení služby](#bkmk_SCPpreq)
- [Bod aktualizace softwaru](#bkmk_2012SUPpreq)
- [Bod migrace stavu](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> Lokalita centrální správy a servery primární lokality

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

- Algoritmus RDC (Remote Differential Compression)  

- Použijete-li bod aktualizace softwaru na jiném serveru, než je server lokality, nainstalujte konzolu pro správu služby WSUS na server lokality.

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Než nainstalujete nebo upgradujete lokalitu centrální správy nebo primární lokalitu, nainstalujte verzi sady Windows Assessment and Deployment Kit (ADK), která je nutná pro verzi Configuration Manager instalujete nebo upgradujete na. Další informace najdete v tématu [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Další informace o tomto požadavku najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Visual C++ distribuovatelné  

- Configuration Manager nainstaluje Distribuovatelný balíček Microsoft Visual C++ 2013 do každého počítače, který instaluje server lokality.  

- Lokality centrální správy a primární lokality vyžadují verze platformy x86 i x64 příslušného redistribuovatelného souboru.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> Server sekundární lokality

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

- Algoritmus RDC (Remote Differential Compression)  

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ distribuovatelné

- Configuration Manager nainstaluje Distribuovatelný balíček Microsoft Visual C++ 2013 do každého počítače, který instaluje server lokality.  

- Sekundární lokality vyžadují pouze verzi x64.  

### <a name="default-site-system-roles"></a>Výchozí role systému lokality  

- Ve výchozím nastavení sekundární lokalita nainstaluje **bod správy** a **distribuční bod**.  

- Ujistěte se, že server sekundární lokality splňuje požadavky pro tyto role systému lokality.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> Databázový server  

### <a name="remote-registry-service"></a>Remote Registry Service  

- Během instalace Configuration Manager lokality povolte službu **Remote Registry** v počítači, který je hostitelem databáze lokality.  

### <a name="sql-server"></a>SQL Server  

- Než nainstalujete lokalitu centrální správy nebo primární lokalitu, nainstalujte podporovanou verzi SQL Server pro hostování databáze lokality. Další informace najdete v tématu [podporované verze SQL Server](support-for-sql-server-versions.md).  

- Před instalací sekundární lokality můžete nainstalovat podporovanou verzi SQL Server.  

- Pokud se rozhodnete, že má Configuration Manager instalovat SQL Server Express jako součást instalace sekundární lokality, ujistěte se, že počítač splňuje požadavky na spuštění SQL Server Express.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> Server poskytovatele služby SMS  

### <a name="windows-adk"></a>Windows ADK

- Počítač, na který nainstalujete instanci poskytovatele serveru SMS, musí mít požadovanou verzi sady Windows ADK, kterou vyžaduje verze Configuration Manager, kterou instalujete nebo na kterou upgradujete. Další informace najdete v tématu [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Další informace o tomto požadavku najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- Pokud používáte [službu pro správu](../../../develop/adminservice/overview.md), server, který je hostitelem role poskytovatele služby SMS, vyžaduje rozhraní .NET 4,5 nebo novější.  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager verze 1810 vyžaduje rozhraní .NET 4.5.2 nebo novější.

- Webový server (IIS): každý zprostředkovatel se pokusí nainstalovat [službu správy](../../../develop/adminservice/overview.md). Tato služba má závislost na službě IIS, která umožňuje navazovat certifikát na port HTTPS 443. Configuration Manager používá rozhraní API služby IIS ke kontrole konfigurace tohoto certifikátu. Pokud nakonfigurujete lokalitu pro [Rozšířené protokol HTTP](../hierarchy/enhanced-http.md), Configuration Manager používá rozhraní API služby IIS k vytvoření vazby certifikátu vygenerovaného webem. Počínaje verzí 2002 lokalita automaticky používá certifikát podepsaný držitelem webu.

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Bod webu Katalog aplikací  

> [!Important]  
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS  

- Společné funkce protokolu HTTP:  

    - Výchozí dokument  

    - Statický obsah  

- Vývoj aplikací:  

    - ASP.NET 3,5 (a automaticky vybrané možnosti)  

    - ASP.NET 4,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 3.5  

    - Rozšiřitelnost rozhraní .NET 4.5  

- Zabezpečení:  

    - Ověřování systému Windows  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Bod webové služby Katalog aplikací  

> [!Important]  
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

- ASP.NET 4,5:  

    - Aktivace protokolem HTTP (a automaticky vybrané možnosti)  

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS

- Společné funkce protokolu HTTP:  

    - Výchozí dokument  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

- Vývoj aplikací:  

    - ASP.NET 3,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 3.5  

    - ASP.NET 4,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 4.5  

### <a name="computer-memory"></a>Paměť počítače  

- Počítač, který je hostitelem této role systému lokality, musí mít k dispozici minimálně 5% volné paměti počítače, aby mohla role systému lokality zpracovávat požadavky.  

- Pokud je tato role systému lokality společně umístěná s jinou rolí systému lokality, která má stejný požadavek, tento požadavek na paměť pro počítač se nezvýší, ale zůstane minimálně 5%.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> funkce Asset Intelligence bod synchronizace  

### <a name="net-framework"></a>.NET Framework

Nainstalujte podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Bod registrace certifikátu  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework

    - Aktivace protokolem HTTP  

### <a name="net-framework"></a>.NET Framework

Nainstalujte podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS

- Vývoj aplikací:  

    - ASP.NET 3,5 (a automaticky vybrané možnosti)  

    - ASP.NET 4,5 (a automaticky vybrané možnosti)  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

    - Kompatibilita rozhraní WMI služby IIS 6  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> Distribuční bod  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- Algoritmus RDC (Remote Differential Compression)  

#### <a name="iis-configuration"></a>Konfigurace služby IIS

- Vývoj aplikací:  

    - Rozšíření ISAPI  

- Zabezpečení:  

    - Ověřování systému Windows  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

    - Kompatibilita rozhraní WMI služby IIS 6  

### <a name="powershell"></a>PowerShell  

- V systému Windows Server 2012 nebo novější je před instalací distribučního bodu vyžadováno prostředí PowerShell 3,0 nebo 4,0.  

### <a name="visual-c-redistributable"></a>Visual C++ distribuovatelné

- Configuration Manager nainstaluje Distribuovatelný balíček Microsoft Visual C++ 2013 do každého počítače, který je hostitelem distribučního bodu.  

- Nainstalovaná verze závisí na platformě počítače (x86 nebo x64).  

### <a name="microsoft-azure"></a>Microsoft Azure  

- K hostování distribučního bodu můžete použít cloudovou službu v Microsoft Azure.  

### <a name="to-support-pxe-or-multicast"></a>Podpora technologie PXE nebo vícesměrového vysílání  

- Povolte respondér technologie PXE v distribučním bodě bez služby pro nasazení systému Windows.  

- Nainstalujte a nakonfigurujte roli Windows serveru služby pro nasazení systému Windows (WDS).  

    > [!NOTE]  
    > Služba WDS se nainstaluje a nakonfiguruje automaticky při konfiguraci distribučního bodu pro podporu technologie PXE nebo vícesměrového vysílání na serveru, na kterém běží Windows Server 2012 nebo novější.  

- V případě distribučního bodu s povoleným vícesměrovým vysíláním se ujistěte, že je tato SQL Server Native Client nainstalovaná a aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Když distribuční bod přenáší obsah, přenáší ho pomocí **Background Intelligent Transfer Service** (BITS) integrovaných do Windows. Role distribučního bodu nevyžaduje instalaci volitelné funkce rozšíření serveru služby BITS, protože klient do něj neodesílá informace.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection bod  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server  

- .NET Framework 3.5

- Funkce Windows Defenderu (Windows Server 2016 nebo novější)  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Bod registrace  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

    - Aktivace protokolem HTTP (a automaticky vybrané možnosti)  

    - ASP.NET 4.5  

    - Služby Windows Communication Foundation (WCF)<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

> [!Note]
> Při instalaci této role systému lokality Configuration Manager automaticky nainstaluje .NET Framework 4.5.2. Tato instalace může server umístit do stavu čekání na restartování. Pokud .NET Framework čeká na restartování, aplikace .NET může selhat až po restartování serveru a dokončení instalace.  

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS

- Společné funkce protokolu HTTP:  

    - Výchozí dokument  

- Vývoj aplikací:  

    - ASP.NET 3,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 3.5  

    - ASP.NET 4,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 4.5  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

### <a name="computer-memory"></a>Paměť počítače

- Počítač, který je hostitelem této role systému lokality, musí mít k dispozici minimálně 5% volné paměti počítače, aby mohla role systému lokality zpracovávat požadavky.  

- Pokud je tato role systému lokality společně umístěná s jinou rolí systému lokality, která má stejný požadavek, tento požadavek na paměť pro počítač se nezvýší, ale zůstane minimálně 5%.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Zprostředkující bod registrace  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

> [!Note]
> Při instalaci této role systému lokality Configuration Manager automaticky nainstaluje .NET Framework 4.5.2. Tato instalace může server umístit do stavu čekání na restartování. Pokud .NET Framework čeká na restartování, aplikace .NET může selhat až po restartování serveru a dokončení instalace.  

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS

- Společné funkce protokolu HTTP:  

    - Výchozí dokument  

    - Statický obsah  

- Vývoj aplikací:  

    - ASP.NET 3,5 (a automaticky vybrané možnosti)  

    - ASP.NET 4,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 3.5  

    - Rozšiřitelnost rozhraní .NET 4.5  

- Zabezpečení:  

    - Ověřování systému Windows  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

### <a name="computer-memory"></a>Paměť počítače

- Počítač, který je hostitelem této role systému lokality, musí mít k dispozici minimálně 5% volné paměti počítače, aby mohla role systému lokality zpracovávat požadavky.  

- Pokud je tato role systému lokality společně umístěná s jinou rolí systému lokality, která má stejný požadavek, tento požadavek na paměť pro počítač se nezvýší, ale zůstane minimálně 5%.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Bod záložního stavu

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- Rozšíření serveru BITS (a automaticky vybrané možnosti) nebo služby inteligentního přenosu na pozadí (BITS) (a automaticky vybrané možnosti)

#### <a name="iis-configuration"></a>Konfigurace služby IIS

Výchozí konfigurace služby IIS je povinná s následujícími přídavky:  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> Bod správy  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- Rozšíření serveru BITS (a automaticky vybrané možnosti) nebo služby inteligentního přenosu na pozadí (BITS) (a automaticky vybrané možnosti)  

### <a name="net-framework"></a>.NET Framework

Nainstalujte podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS

- Vývoj aplikací:  

    - Rozšíření ISAPI  

- Zabezpečení:  

    - Ověřování systému Windows  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

    - Kompatibilita rozhraní WMI služby IIS 6  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Bod služby Reporting Services  

### <a name="net-framework"></a>.NET Framework

Nainstalujte podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Před instalací bodu hlášení nainstalujte a nakonfigurujte alespoň jednu instanci SQL Server pro podporu SQL Server Reporting Services.  

- Instance, kterou použijete pro SQL Server Reporting Services, může být stejná jako instance, kterou používáte pro databázi lokality.  

- Kromě toho může být instance, kterou použijete, sdílená s jinými produkty System Center, pokud tyto další produkty System Center nemají omezení pro sdílení instance SQL Server.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> Bod připojení služby  

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

> [!Note]
> Při instalaci této role systému lokality Configuration Manager automaticky nainstaluje .NET Framework 4.5.2. Tato instalace může server umístit do stavu čekání na restartování. Pokud .NET Framework čeká na restartování, aplikace .NET může selhat až po restartování serveru a dokončení instalace.  

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ distribuovatelné

- Configuration Manager nainstaluje Distribuovatelný balíček Microsoft Visual C++ 2013 do každého počítače, který je hostitelem distribučního bodu.  

- Role systému lokality vyžaduje verzi x64.  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Bod aktualizace softwaru  

### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

Výchozí konfigurace služby IIS je povinná.

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Než nainstalujete bod aktualizace softwaru, nainstalujte na počítač Windows Server Update Services role Windows serveru.  

- Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> Použijete-li bod aktualizace softwaru na jiném serveru, než je server lokality, je nutné nainstalovat konzolu pro správu služby WSUS na server lokality.

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> Bod migrace stavu

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Role a funkce systému Windows Server

- .NET Framework 3.5

    - Aktivace protokolem HTTP (a automaticky vybrané možnosti)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Povolte funkci Windows pro .NET Framework 3,5.

Nainstalujte také podporovanou verzi .NET Framework verze 4,5 nebo novější. Počínaje verzí 1906 Configuration Manager podporuje .NET Framework 4,8.

> [!Note]
> Při instalaci této role systému lokality Configuration Manager automaticky nainstaluje .NET Framework 4.5.2. Tato instalace může server umístit do stavu čekání na restartování. Pokud .NET Framework čeká na restartování, aplikace .NET může selhat až po restartování serveru a dokončení instalace.  

Další informace o .NET Framework verzích najdete v následujících článcích:

- [.NET Framework verze a závislosti](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Nejčastější dotazy k životnímu cyklu – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Konfigurace služby IIS

- Společné funkce protokolu HTTP:  

    - Výchozí dokument  

- Vývoj aplikací:  

    - ASP.NET 3,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 3.5  

    - ASP.NET 4,5 (a automaticky vybrané možnosti)  

    - Rozšiřitelnost rozhraní .NET 4.5  

- Kompatibilita správy služby IIS 6:  

    - Kompatibilita metabáze služby IIS 6  

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Ujistěte se, že je tato součást aktuální. Další informace najdete v tématu [kontroly požadovaných součástí – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).