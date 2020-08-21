---
title: Požadavky na infrastrukturu OSD
titleSuffix: Configuration Manager
description: Seznamte se s externími závislostmi a požadavky na produkty a požadavky na nasazení operačního systému v Configuration Manager
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9bb07bd2b82a9411bc527d04a9a64a0bb6e12f8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697666"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Požadavky na infrastrukturu pro nasazení operačního systému v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení operačního systému v Configuration Manager má vnější závislosti a závislosti v rámci produktu. Tento článek vám může přispět k přípravě infrastruktury pro nasazení operačního systému.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Vnější závislosti Configuration Manager  

V této části najdete informace o externích nástrojích, instalačních sadách a verzích operačních systémů, které jsou nutné k nasazení operačních systémů v Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Sada Windows ADK pro Windows 10  

Sada Windows Assessment and Deployment Kit (ADK) je sada nástrojů a dokumentace, která podporuje konfiguraci a nasazení systému Windows. Configuration Manager používá ADK Windows k automatizaci akcí, jako je instalace Windows, zachytávání imagí a migrace profilů a dat uživatelů.  

Další informace najdete v následujících článcích:  

- [Scénáře sady Windows ADK pro Windows 10 pro IT specialisty](/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Stažení sady Windows ADK pro Windows 10](/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Nezapomeňte si stáhnout balíček **Windows ADK pro Windows 10** a **doplněk Windows PE pro ADK**.

- [Podpora pro Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Systémy lokality
Systém Windows ADK je předpokladem pro následující servery systémů lokality:

- Server lokality lokality nejvyšší úrovně v hierarchii  

- Server lokality každé primární lokality v hierarchii  

- Každá instance poskytovatele serveru SMS  


> [!NOTE]  
> Než nainstalujete lokalitu Configuration Manager, nainstalujte na každý server lokality ručně Windows ADK.  

#### <a name="windows-adk-features"></a>Funkce ADK systému Windows
Nainstalujte následující funkce sady Windows ADK:  

-   Nástroj pro migraci stavu uživatele (USMT)  

    > [!Note]  
    > Na poskytovateli služby SMS není nástroj USMT vyžadován.

-   Nástroje nasazení systému Windows  

-   Prostředí předinstalace systému Windows (Windows PE)  

    > [!Important]  
    > Počínaje systémem Windows 10 verze 1809 je systém Windows PE samostatným instalačním programem. Jinak neexistuje žádný funkční rozdíl.<!--SCCMDocs-pr issue 2908-->  

Seznam verzí Windows 10 ADK, které můžete použít s různými verzemi Configuration Manager, najdete v tématu [Podpora pro Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>Nástroj pro migraci stavu uživatele (USMT)  

Configuration Manager používá balíček nástroje USMT, který obsahuje zdrojové soubory nástroje USMT 10 pro zachycení a obnovení stavu uživatele v rámci nasazení operačního systému. Instalace Configuration Manager v lokalitě nejvyšší úrovně automaticky vytvoří balíček nástroje USMT. Nástroj USMT 10 zachytí stav uživatele ze systémů Windows 7, Windows 8, Windows 8.1 a Windows 10.  

Další informace najdete v následujících článcích:  

- [Běžné scénáře migrace pro nástroj USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Správa stavu uživatele](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Prostředí Windows PE se používá ke spuštění počítače pomocí spouštěcích imagí. Jedná se o verzi systému Windows s omezenými službami, které se používají při předinstalaci a nasazení systému Windows. Následující seznam obsahuje podporované verze sady Windows ADK for Configuration Manager aktuální větev:  

#### <a name="windows-adk-version"></a>Verze sady Windows ADK  
Windows ADK pro Windows 10 Další informace najdete v tématu [Podpora pro Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Verze prostředí Windows PE pro spouštěcí bitové kopie přizpůsobitelné z konzoly Configuration Manager  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Podporované verze prostředí Windows PE pro spouštěcí bitové kopie, které nelze přizpůsobit z konzoly Configuration Manager  
Windows PE 3.1<sup>1</sup> a Windows PE 5  

<sup>1</sup> do Configuration Manager můžete přidat pouze spouštěcí bitovou kopii, která je založená na prostředí Windows PE 3,1. Instalováním doplňku Windows AIK Supplement pro Windows 7 SP1 upgradujte sadu Windows AIK pro Windows 7 (na platformě Windows PE 3) s doplňkem Windows AIK Supplement pro Windows 7 SP1 (na platformě Windows PE 3.1). Doplněk Windows AIK pro Windows 7 SP1 si můžete stáhnout z webu [Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=5188).  

Pokud máte například Configuration Manager, můžete v konzole Configuration Manager přizpůsobit spouštěcí bitové kopie ze sady Windows ADK pro Windows 10 (na platformě Windows PE 10). Ale přestože se podporují spouštěcí image založené na Windows PE 5, je potřeba je přizpůsobit z jiného počítače a používat verzi DISM, která je nainstalovaná s Windows ADK pro Windows 8. Pak přidejte spouštěcí bitovou kopii do konzoly Configuration Manager. Další informace o postupu přizpůsobení spouštěcí bitové kopie (Přidání volitelných komponent a ovladačů), povolení podpory příkazů pro spouštěcí image, Přidání spouštěcí bitové kopie do konzoly Configuration Manager a aktualizace distribučních bodů pomocí spouštěcí image najdete v tématu [Přizpůsobení spouštěcích bitových kopií](../get-started/customize-boot-images.md). Další informace o spouštěcích imagích najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Služba WSUS (Windows Server Update Services)  

Pro bod aktualizace softwaru se vyžaduje služba WSUS, která je nutná k instalaci aktualizací softwaru během nasazování operačního systému. Další informace najdete v tématu [instalace konfigurace bodu aktualizace softwaru](../../sum/get-started/install-a-software-update-point.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internetová informační služba (IIS) na serverech systémů lokalit  

Služba IIS je vyžadována pro distribuční bod, bod migrace stavu a bod správy. Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### <a name="windows-deployment-services-wds"></a>Služba pro nasazení systému Windows (WDS)  

Ve verzi 1802 a starší se služba WDS potřebuje pro nasazení PXE. Počínaje verzí 1806 můžete povolit technologii PXE v distribučním bodě bez služby WDS. Další informace najdete v části [Služba pro nasazení systému Windows](#BKMK_WDS) v tomto článku. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protokol DHCP  

Pro nasazení PXE je vyžadován protokol DHCP. Chcete-li nasadit operační systémy pomocí PXE, je nutné mít funkční server DHCP s aktivním hostitelem. Další informace o nasazení PXE najdete v tématu [použití technologie PXE pro nasazení Windows přes síť](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Podporované operační systémy a konfigurace pevného disku  

Další informace o verzích operačních systémů a konfiguracích pevného disku, které nástroj Configuration Manager podporuje při nasazení operačních systémů, najdete v tématu [podporované operační systémy](#BKMK_SupportedOS) a [podporované konfigurace disků](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Ovladače zařízení systému Windows  

Ovladače zařízení systému Windows lze použít při instalaci operačního systému do cílového počítače. Používají se také při spuštění prostředí Windows PE ve spouštěcí imagi. Další informace najdete v tématu [Správa ovladačů](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Configuration Manager závislosti  

V této části najdete informace o požadavcích na nasazení Configuration Manager OS.  


### <a name="os-image"></a>Bitová kopie operačního systému  

Image operačního systému v Configuration Manager jsou uložené ve formátu WIM (Windows Imaging). Představují komprimovanou kolekci referenčních souborů a složek. Tyto image jsou potřebné k úspěšné instalaci a konfiguraci operačního systému v počítači. Další informace najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Katalog ovladačů  

Chcete-li nasadit ovladač zařízení, importujte ho a zpřístupněte ho v distribučním bodě, ke kterému má klient Configuration Manager přístup. Další informace o katalogu ovladačů najdete v tématu [Správa ovladačů](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Bod správy  

Body správy přenášejí informace mezi klienty a Configuration Manager lokality. Klient používá bod správy ke spuštění pořadí úkolů k dokončení nasazení operačního systému. Další informace o pořadí úkolů najdete v tématu [požadavky na plánování pro automatizaci úloh](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Distribuční bod  

Distribuční body se ve většině nasazení používají k ukládání dat, která se používají k nasazení operačního systému, jako jsou Image nebo balíčky ovladačů. Pořadí úloh obvykle načítají data z distribučního bodu pro nasazení operačního systému. Další informace o instalaci distribučních bodů a správě obsahu najdete v tématu [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>Distribuční bod s povoleným PXE  

Nasazení iniciovaná pomocí technologie PXE nasadíte tak, že nakonfigurujete distribuční bod, aby přijímal požadavky PXE od klientů. Další informace najdete v tématu [Konfigurace distribučního bodu](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Distribuční bod s povoleným vícesměrovým vysíláním  

Chcete-li optimalizovat nasazení operačního systému pomocí vícesměrového vysílání, nakonfigurujte distribuční bod tak, aby podporoval vícesměrové vysílání. Další informace najdete v tématu [Konfigurace distribučního bodu](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Bod migrace stavu  

Když zachytíte a obnovíte data o stavu uživatele pro souběžná a aktualizační nasazení, nakonfigurujte bod migrace stavu k uložení dat o stavu uživatele v jiném počítači.  

Další informace o konfiguraci bodu migrace stavu najdete v tématu [Bod migrace stavu](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

Další informace o zaznamenání a obnovení stavu uživatele najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Bod služby Reporting services  

Chcete-li použít sestavy Configuration Manager pro nasazení operačního systému, nainstalujte a nakonfigurujte bod hlášení. Další informace najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Oprávnění zabezpečení pro nasazení operačních systémů  

Role zabezpečení **Deployment Manager operačního systému** je předdefinovaná role, kterou nemůžete změnit. Roli však můžete zkopírovat, můžete provést změny a poté je uložit jako novou vlastní roli zabezpečení. Tady jsou některá oprávnění, která se vztahují přímo na nasazení operačního systému:  

- **Balíček spouštěcí image:** Vytvořit, Odstranit, Upravit, Upravit složku, Přesunout objekt, Načíst, Nastavit obor zabezpečení  

- **Ovladače zařízení:** Vytvořit, Odstranit, Upravit, Upravit složku, Upravit sestavu, Přesunout objekt, Číst, Spustit sestavu  

- **Balíček ovladače:** Vytvořit, Odstranit, Upravit, Upravit složku, Přesunout objekt, Číst, Nastavit obor zabezpečení  

- **Balíček operačního systému:** Vytvořit, Odstranit, Upravit, Upravit složku, Přesunout objekt, Číst, Nastavit obor zabezpečení  

- **Balíček s upgradem operačního systému**: vytvořit, odstranit, upravit, upravit složku, přesunout objekt, číst, nastavit obor zabezpečení  

- **Balíček pořadí úkolů:** Vytvořit, Vytvořit médium pořadí úloh, Odstranit, Upravit, Upravit složku, Upravit sestavu, Přesunout objekt, Číst, Spustit sestavu, Nastavit obor zabezpečení  

Další informace najdete v tématu [Vytvoření vlastních rolí zabezpečení](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Obory zabezpečení pro nasazení operačních systémů  

Pomocí oborů zabezpečení poskytněte správcům přístup k zabezpečitelné objekty používané v nasazeních operačních systémů, jako jsou operační systémy a spouštěcí bitové kopie, balíčky ovladačů a balíčky pořadí úloh. Další informace najdete v tématu [Obory zabezpečení](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Služba pro nasazení systému Windows  

Ve verzi 1802 a dřívější musí být služba WDS (Windows Deployment Services) nainstalovaná na stejném serveru jako distribuční body, které nakonfigurujete pro podporu technologie PXE nebo vícesměrového vysílání. Služba WDS je součástí operačního systému serveru. V případě nasazení PXE je WDS službou, která provede spuštění PXE. Když je distribuční bod nainstalován a povolen pro technologii PXE, Configuration Manager nainstaluje poskytovatele do služby WDS, který používá spouštěcí funkce služby WDS PXE.  

Počínaje verzí 1806 můžete povolit technologii PXE v distribučním bodě bez služby WDS. Další informace najdete v možnosti **Povolit respondér technologie PXE bez služby pro nasazení systému Windows** v tématu [instalace a konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


> [!NOTE]  
>  Pokud server vyžaduje restart, instalace služby WDS se nemusí zdařit. 


### <a name="wds-requirements"></a>Požadavky služby WDS  

-   Instalace služby WDS na serveru vyžaduje, aby byl správce členem místní skupiny Administrators.  

-   Server služby WDS musí být členem domény služby Active Directory nebo řadičem domény pro doménu služby Active Directory. Všechny konfigurace domény a doménové struktury systému Windows podporují službu WDS.  

-   Pokud je poskytovatel nainstalovaný na vzdáleném serveru, nainstalujte službu WDS na server lokality a na vzdáleného poskytovatele.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> Předpoklady, pokud máte na stejném serveru služby WDS a DHCP  

Pokud máte v úmyslu hostovat distribuční bod na serveru, na kterém je spuštěný protokol DHCP, vezměte v úvahu následující problémy s konfigurací:  

-   Musíte mít funkční server DHCP v aktivním oboru. Služba WDS používá technologii PXE, která vyžaduje server DHCP.  

-   Ke spuštění služby WDS je nutný server DNS.  

-   Na serveru služby WDS musí být otevřeny následující porty UDP:  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  Pokud je na serveru vyžadována autorizace DHCP, potřebujete na serveru otevřít port 68 klienta DHCP.  

-   Protokoly DHCP a WDS vyžadují port číslo 67. Pokud jste současně hostitelem služby WDS a DHCP, můžete přesunout službu DHCP nebo distribuční bod, který je nakonfigurován pro technologii PXE, na samostatný server. Případně můžete pomocí následujícího postupu nakonfigurovat server WDS tak, aby naslouchal na jiném portu.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Postup konfigurace serveru WDS pro naslouchání na jiném portu  

1.  Upravte následující klíč registru:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Nastavte hodnotu registru **UseDHCPPorts** na **0**.  

3.  Aby se nová konfigurace projevila, spusťte na serveru následující příkaz:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> Ve verzi 1810 a starší se nepodporuje použití respondérů PXE bez služby WDS na serverech, na kterých běží taky server DHCP.
>
> Pokud v rámci verze 1902 povolíte respondér PXE v distribučním bodě bez služby pro nasazení systému Windows, může být nyní na stejném serveru jako služba DHCP. Další informace najdete v tématu [Konfigurace aspoň jednoho distribučního bodu pro příjem požadavků PXE](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> Podporované operační systémy  

Všechny operační systémy Windows uvedené jako Podporovaní klienti v [podporovaných operačních systémech pro klienty a zařízení](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) se podporují pro nasazení operačního systému.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> Podporované konfigurace disků  

V následující tabulce jsou uvedeny kombinace konfigurací pevného disku na referenčním a cílovém počítači, které jsou podporované pro Configuration Manager nasazení operačního systému:  

|Konfigurace pevného disku referenčního počítače|Konfigurace pevného disku cílového počítače|  
|------------------------------------------------|--------------------------------------------------|  
|Základní disk|Základní disk|  
|Jednoduchý svazek na dynamickém disku|Jednoduchý svazek na dynamickém disku|  

Configuration Manager podporuje zachycení bitové kopie operačního systému pouze z počítačů, které jsou nakonfigurovány s jednoduchými svazky. Pro následující konfigurace pevného disku neexistuje žádná podpora:  

-   Rozložené svazky  

-   Prokládané svazky (RAID 0)  

-   Zrcadlové svazky (RAID 1)  

-   Svazky s paritou (RAID 5)  

Následující tabulka uvádí další konfiguraci pevného disku na referenčním a cílovém počítači, které nejsou podporované při nasazení Configuration Manager OS.  

|Konfigurace pevného disku referenčního počítače|Konfigurace pevného disku cílového počítače|  
|------------------------------------------------|--------------------------------------------------|  
|Základní disk|Dynamický disk|  



## <a name="next-steps"></a>Další kroky

- [Příprava rolí systému webového serveru pro nasazení operačního systému](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Příprava nasazení operačního systému](../get-started/prepare-for-operating-system-deployment.md)