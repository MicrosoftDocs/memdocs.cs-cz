---
title: Používané účty
titleSuffix: Configuration Manager
description: Identifikujte a spravujte skupiny systému Windows, účty a objekty SQL používané v Configuration Manager.
ms.date: 10/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6808fed9fa9aaf894e3975066eb7707880b7948
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073411"
---
# <a name="accounts-used-in-configuration-manager"></a>Účty používané v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí následujících informací Identifikujte skupiny systému Windows, účty a objekty SQL používané v Configuration Manager, způsob jejich použití a jakékoli požadavky.  

- [Skupiny systému Windows, které vytváří a používá nástroj Configuration Manager](#bkmk_groups)  
  - [ConfigMgr_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [ConfigMgr_DViewAccess](#configmgr_dviewaccess)  
  - [Uživatelé vzdáleného ovládání nástroje ConfigMgr](#configmgr-remote-control-users)  
  - [Správci SMS](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_&lt;SiteCode\>](#bkmk_filerepl)  

- [Účty, které používá nástroj Configuration Manager](#bkmk_accounts)
  - [Účet zjišťování skupiny služby Active Directory](#active-directory-group-discovery-account)  
  - [Účet zjišťování systému služby Active Directory](#active-directory-system-discovery-account)  
  - [Účet zjišťování uživatelů služby Active Directory](#active-directory-user-discovery-account)  
  - [Účet doménové struktury služby Active Directory](#active-directory-forest-account)  
  - [Účet bodu registrace certifikátu](#certificate-registration-point-account)  
  - [Zachytit účet bitové kopie operačního systému](#capture-os-image-account)  
  - [Účet klientské nabízené instalace](#client-push-installation-account)  
  - [Účet pro připojení k bodu registrace](#enrollment-point-connection-account)  
  - [Účet pro připojení k serveru Exchange](#exchange-server-connection-account)  
  - [Účet pro připojení k bodu správy](#management-point-connection-account)  
  - [Účet pro připojení vícesměrového vysílání](#multicast-connection-account)  
  - [Účet přístupu k síti](#network-access-account)  
  - [Účet pro přístup k balíčku](#package-access-account)  
  - [Účet bodu služby Reporting Services](#reporting-services-point-account)  
  - [Účty povolených prohlížečů vzdálených nástrojů](#remote-tools-permitted-viewer-accounts)  
  - [Účet instalace lokality](#site-installation-account)
  - [Účet instalace systému lokality](#site-system-installation-account)  
  - [Účet proxy server systému lokality](#site-system-proxy-server-account)  
  - [Účet pro připojení k serveru SMTP](#smtp-server-connection-account)  
  - [Účet pro připojení k bodu aktualizace softwaru](#software-update-point-connection-account)  
  - [Účet zdrojové lokality](#source-site-account)  
  - [Účet databáze zdrojové lokality](#source-site-database-account)  
  - [Účet připojení k doméně pořadí úloh](#task-sequence-domain-join-account)  
  - [Účet připojení síťové složky pořadí úloh](#task-sequence-network-folder-connection-account)  
  - [Účet Spustit jako pořadí úloh](#task-sequence-run-as-account)  

- [Uživatelské objekty, které Configuration Manager používá v SQL](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Databázové role, které Configuration Manager používá v SQL](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a>Skupiny systému Windows, které Configuration Manager vytvářejí a používají  

Configuration Manager automaticky vytvoří a v mnoha případech automaticky udržuje následující skupiny systému Windows:  

> [!NOTE]  
> Když Configuration Manager vytvoří skupinu v počítači, který je členem domény, bude skupina místní skupinou zabezpečení. Pokud je počítač řadičem domény, skupina je místní doménovou skupinou. Tento typ skupiny je sdílen mezi všemi řadiči domény v doméně.  


### <a name="configmgr_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess

Configuration Manager tuto skupinu používá k udělení přístupu k zobrazení souborů shromážděných inventářem softwaru.  

Další informace najdete v tématu [Úvod do inventáře softwaru](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení vytvořená na serveru primární lokality.

Když odinstalujete lokalitu, tato skupina se automaticky neodebere. Po odinstalaci lokality ji ručně odstraní.

#### <a name="membership"></a>Členství
Configuration Manager automaticky spravuje členství ve skupině. Členství zahrnuje uživatele s právy pro správu, kterým je uděleno oprávnění **Zobrazit shromážděné soubory** pro zabezpečitelný objekt **Kolekce** z přiřazené role zabezpečení.

#### <a name="permissions"></a>Oprávnění
Ve výchozím nastavení má tato skupina oprávnění **číst** k následující složce na serveru lokality:`C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configmgr_dviewaccess"></a><a name="configmgr_dviewaccess"></a>ConfigMgr_DViewAccess  

Tato skupina je místní skupina zabezpečení, která Configuration Manager vytvořena na serveru databáze lokality nebo serveru repliky databáze pro podřízenou primární lokalitu. Lokalita ji vytvoří, když použijete distribuovaná zobrazení pro replikaci databáze mezi lokalitami v hierarchii. Obsahuje server lokality a účty počítačů SQL Server lokality centrální správy.

Další informace najdete v tématu [přenos dat mezi lokalitami](data-transfers-between-sites.md).


### <a name="configmgr-remote-control-users"></a>Uživatelé vzdáleného ovládání nástroje ConfigMgr  

Configuration Manager nástroje Remote Tools tuto skupinu používají k ukládání účtů a skupin, které jste nastavili v seznamu **povolených prohlížečů** . Lokalita přiřadí tento seznam každému klientovi.  

Další informace najdete v tématu [Úvod do vzdáleného řízení](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení vytvořená v klientovi Configuration Manager, když klient obdrží zásadu, která povoluje vzdálené nástroje.

Po zakázání nástrojů Remote Tools pro klienta nebude tato skupina automaticky odebrána. Po zakázání nástrojů Remote Tools ji ručně odstraňte.

#### <a name="membership"></a>Členství
Ve výchozím nastavení nejsou v této skupině žádní členové. Když přidáte uživatele do seznamu **povolených prohlížečů** , přidají se do této skupiny automaticky.

Pomocí seznamu **povolených prohlížečů** spravujte členství této skupiny místo přidání uživatelů nebo skupin přímo do této skupiny.

Kromě povoleného prohlížeče musí mít administrativní uživatel oprávnění ke **vzdálenému řízení** pro objekt **kolekce** . Přiřaďte toto oprávnění pomocí role zabezpečení **operátor nástrojů pro vzdálenou** práci.  

#### <a name="permissions"></a>Oprávnění
Ve výchozím nastavení tato skupina nemá oprávnění pro žádná umístění v počítači. Používá se pouze k uložení seznamu **povolených prohlížečů** .  


### <a name="sms-admins"></a>Správci SMS  

Configuration Manager tuto skupinu používá k udělení přístupu k poskytovateli serveru SMS prostřednictvím služby WMI. Přístup k poskytovateli serveru SMS je nutný k zobrazení a změně objektů v konzole Configuration Manager.  

> [!NOTE]  
> Konfigurace správy na základě rolí uživatele s právy pro správu Určuje, které objekty mohou zobrazovat a spravovat při použití konzoly Configuration Manager.  

Další informace najdete v tématu [plánování poskytovatele serveru SMS](plan-for-the-sms-provider.md).

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení vytvořená na všech počítačích, které mají poskytovatele serveru SMS. 

Když odinstalujete lokalitu, tato skupina se automaticky neodebere. Po odinstalaci lokality ji ručně odstraní.

#### <a name="membership"></a>Členství
Configuration Manager automaticky spravuje členství ve skupině. Ve výchozím nastavení je každý správce v hierarchii a účet počítače serveru lokality členy skupiny **Admins služby SMS** na jednotlivých počítačích poskytovatele SMS v lokalitě.

#### <a name="permissions"></a>Oprávnění
Práva a oprávnění pro skupinu SMS Admins můžete zobrazit v modulu snap-in konzoly MMC **řízení služby WMI** . Ve výchozím nastavení má tato skupina povolenou **možnost povolit účet** a povolit **Vzdálené povolení** v oboru názvů `Root\SMS` rozhraní WMI. Ověření uživatelé mají oprávnění **spouštět metody**, **zapisovat zprostředkovatele**a **Povolit účet**.

Používáte-li vzdálenou konzolu Configuration Manager, nakonfigurujte oprávnění modelu DCOM pro **vzdálenou aktivaci** na počítači serveru lokality i u poskytovatele serveru SMS. Udělte tato práva skupině **Admins služby SMS** . Tato akce zjednodušuje správu namísto udělení těchto oprávnění přímo uživatelům nebo skupinám. Další informace najdete v tématu [Konfigurace oprávnění modelu DCOM pro vzdálené Configuration Manager konzoly](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>  
 
Body správy, které jsou vzdálené od serveru lokality, používají tuto skupinu pro připojení k databázi lokality. Tato skupina nabízí bodu správy přístup ke složkám příchozí pošty na serveru lokality a v databázi lokality.  

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení vytvořená na všech počítačích, které mají poskytovatele serveru SMS.

Když odinstalujete lokalitu, tato skupina se automaticky neodebere. Po odinstalaci lokality ji ručně odstraní.

#### <a name="membership"></a>Členství
Configuration Manager automaticky spravuje členství ve skupině. Ve výchozím nastavení členství zahrnuje počítačové účty vzdálených počítačů, které mají pro lokalitu bod správy.

#### <a name="permissions"></a>Oprávnění
Ve výchozím nastavení má tato skupina oprávnění **číst**, **číst & spouštět**a **Zobrazovat obsah složky** pro následující složku na serveru lokality: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Tato skupina má další oprávnění **zapisovat** do podsložek pod složkou **Doručená pošta**, do kterých bod správy zapisuje data klientů.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>  
 
Vzdálené počítače poskytovatele služby SMS tuto skupinu používají pro připojení k serveru lokality.  

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení na serveru lokality.

Když odinstalujete lokalitu, tato skupina se automaticky neodebere. Po odinstalaci lokality ji ručně odstraní.

#### <a name="membership"></a>Členství
Configuration Manager automaticky spravuje členství ve skupině. Ve výchozím nastavení členství zahrnuje počítačový účet nebo uživatelský účet domény. Tento účet používá pro připojení k serveru lokality od každého vzdáleného poskytovatele služby SMS.

#### <a name="permissions"></a>Oprávnění
Ve výchozím nastavení má tato skupina oprávnění **číst**, **číst & spouštět**a **Zobrazovat obsah složky** pro následující složku na serveru lokality: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Tato skupina má další oprávnění pro **zápis** a **Úpravy** podsložek pod složkou Doručená pošta. Poskytovatel serveru SMS vyžaduje přístup k těmto složkám.

Tato skupina má také oprávnění **ke čtení** pro podsložky na serveru lokality níže `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

Má také následující oprávnění pro podsložky níže `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Čtení**  
- **Čtení & provedení**  
- **Výpis obsahu složky**  
- **Zápis**  
- **Úprava**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>  

Součást Správce odesílání souborů na Configuration Manager počítače se vzdáleným systémem lokality používá tuto skupinu pro připojení k serveru lokality.  

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení na serveru lokality.

Když odinstalujete lokalitu, tato skupina se automaticky neodebere. Po odinstalaci lokality ji ručně odstraní.

#### <a name="membership"></a>Členství
Configuration Manager automaticky spravuje členství ve skupině. Ve výchozím nastavení členství zahrnuje počítačový účet nebo uživatelský účet domény. Tento účet používá pro připojení k serveru lokality z každého vzdáleného systému lokality, ve kterém je spuštěný správce odesílání souborů.

#### <a name="permissions"></a>Oprávnění
Ve výchozím nastavení má tato skupina oprávnění **číst**, **číst & spouštět**a **Zobrazovat obsah složky** v následující složce a jejích podsložkách na serveru lokality: `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

Tato skupina má další oprávnění **zápisu** a **úprav** do následující složky na serveru lokality: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a>SMS_SiteToSiteConnection_&lt;SiteCode\>  
Configuration Manager tuto skupinu používá k povolení replikace na základě souborů mezi lokalitami v hierarchii. Pro každou vzdálenou lokalitu, která přímo přenáší soubory do této lokality, má tato skupina účty nastavené jako **účet replikace souborů**.  

#### <a name="type-and-location"></a>Typ a umístění
Tato skupina je místní skupina zabezpečení na serveru lokality.

#### <a name="membership"></a>Členství
Když instalujete novou lokalitu jako podřízenou jiné lokalitě, Configuration Manager automaticky přidá počítačový účet nového serveru lokality do této skupiny na nadřazeném serveru lokality. Configuration Manager také přidá účet počítače nadřazené lokality do skupiny na novém serveru lokality. Pokud zadáte jiný účet pro přenosy založené na souborech, přidejte tento účet do této skupiny na cílovém serveru lokality.

Když odinstalujete lokalitu, tato skupina se automaticky neodebere. Po odinstalaci lokality ji ručně odstraní.

#### <a name="permissions"></a>Oprávnění
Ve výchozím nastavení má tato skupina **Úplné řízení** pro následující složku: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a>Účty, které Configuration Manager používá  

Pro Configuration Manager můžete nastavit následující účty.  


### <a name="active-directory-group-discovery-account"></a>Účet zjišťování skupiny služby Active Directory  

Lokalita používá **účet zjišťování skupiny služby Active Directory** ke zjištění následujících objektů z umístění v Active Directory Domain Services, které zadáte:
- Místní, globální a univerzální skupiny zabezpečení
- Členství v rámci těchto skupin
- Členství v rámci distribučních skupin
  - Distribuční skupiny se neobjevují jako prostředky skupiny.

Tento účet může být účet počítače serveru lokality, který spouští zjišťování nebo je to účet uživatele systému Windows. Musí mít oprávnění ke **čtení** pro umístění služby Active Directory, která zadáte pro zjišťování.  

Další informace najdete v tématu [zjišťování skupin služby Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Účet zjišťování systému služby Active Directory  

Lokalita používá **účet zjišťování systému služby Active Directory** ke zjišťování počítačů z umístění v Active Directory Domain Services, které zadáte.  

Tento účet může být účet počítače serveru lokality, který spouští zjišťování nebo je to účet uživatele systému Windows. Musí mít oprávnění ke **čtení** pro umístění služby Active Directory, která zadáte pro zjišťování.  

Další informace najdete v tématu [zjišťování systémových informací služby Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Účet zjišťování uživatelů služby Active Directory  
 
Lokalita používá **účet zjišťování uživatelů služby Active Directory** ke zjištění uživatelských účtů z umístění v Active Directory Domain Services, které zadáte.  

Tento účet může být účet počítače serveru lokality, který spouští zjišťování nebo je to účet uživatele systému Windows. Musí mít oprávnění ke **čtení** pro umístění služby Active Directory, která zadáte pro zjišťování.  

Další informace najdete v tématu [zjišťování uživatelů služby Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Účet doménové struktury služby Active Directory  

Lokalita používá **účet doménové struktury služby Active Directory** ke zjišťování síťové infrastruktury z doménových struktur služby Active Directory. Lokality centrální správy a primární lokality ji používají také k publikování dat lokality pro Active Directory Domain Services pro doménovou strukturu.  

> [!NOTE]  
> Sekundární lokality vždy používají k publikování pro službu Active Directory účet počítače serveru sekundární lokality.  

Pro zjišťování a publikování v nedůvěryhodných doménových strukturách musí být účet doménové struktury služby Active Directory globálním účtem. Pokud nepoužíváte účet počítače serveru lokality, můžete vybrat pouze globální účet.  

Tento účet musí mít oprávnění **Číst** ke každé doménové struktuře služby Active Directory, ve které chcete zjišťovat síťovou infrastrukturu.  

Tento účet musí mít oprávnění **Úplné řízení** ke kontejneru **System Management** a všem jeho podřízeným objektům v každé doménové struktuře služby Active Directory, do které chcete publikovat data lokality. Další informace najdete v tématu [Příprava služby Active Directory pro publikování lokality](../network/extend-the-active-directory-schema.md).  

Další informace najdete v tématu [zjišťování doménové struktury služby Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Účet bodu registrace certifikátu  

Bod registrace certifikátu používá **účet bodu registrace certifikátu** pro připojení k databázi Configuration Manager. Ve výchozím nastavení používá svůj počítačový účet, ale můžete místo něj nakonfigurovat uživatelský účet. Pokud je bod registrace certifikátu v nedůvěryhodné doméně ze serveru lokality, musíte zadat uživatelský účet. Tento účet vyžaduje pouze **oprávnění ke čtení** databáze lokality, protože systém zpráv o stavu zpracovává úkoly zápisu.  

Další informace najdete v tématu [Úvod do profilů certifikátů](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>Zachytit účet bitové kopie operačního systému  

Když zachytíte image operačního systému, Configuration Manager používá **účet pro zachycení bitové kopie operačního systému** pro přístup ke složce, do které ukládáte zachycené image. Pokud přidáte do pořadí úkolů krok **zaznamenat bitovou kopii operačního systému** , tento účet je povinný.  

Účet musí mít oprávnění **ke čtení** a **zápisu** v síťové sdílené složce, kam ukládáte zachycené image.  

Pokud změníte heslo pro účet ve Windows, aktualizujte pořadí úkolů pomocí nového hesla. Klient Configuration Manager obdrží nové heslo při příštím stažení zásad klienta.  

Pokud potřebujete použít tento účet, vytvořte jeden uživatelský účet domény. Udělte IT minimální oprávnění pro přístup k požadovaným síťovým prostředkům a použijte je pro všechna pořadí úloh zachycení.  

> [!IMPORTANT]  
> Nepřiřazujte k tomuto účtu oprávnění k interaktivnímu přihlašování.  
>   
> Pro tento účet nepoužívejte účet pro přístup k síti.  

Další informace najdete v tématu [Vytvoření pořadí úkolů pro zachycení operačního systému](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Účet klientské nabízené instalace  

Když nasazujete klienty pomocí metody nabízené instalace klienta, lokalita používá **účet klientské nabízené instalace** pro připojení k počítačům a instalaci klientského softwaru Configuration Manager. Pokud tento účet nezadáte, server lokality se pokusí použít svůj účet počítače.  

Tento účet musí být členem místní skupiny **Administrators** na cílových klientských počítačích. Tento účet nevyžaduje oprávnění **správce domény** .  

Můžete zadat více než jeden účet klientské nabízené instalace. Configuration Manager se každý z nich pokusí, dokud jeden neuspěje.  

> [!TIP]  
> Pokud máte velké prostředí Active Directory a potřebujete tento účet změnit, pomocí následujícího postupu efektivněji zajistěte koordinaci tohoto účtu aktualizace: 
> 1. Vytvoří nový účet s jiným názvem.   
> 2. Přidejte nový účet do seznamu účtů klientské nabízené instalace v Configuration Manager  
> 3. Umožněte, aby Active Directory Domain Services pro replikaci nového účtu dost času.  
> 4. Pak odeberte starý účet z Configuration Manager a Active Directory Domain Services  

> [!IMPORTANT]  
> Neudělujte tomuto účtu oprávnění k místnímu přihlášení.  

Další informace najdete v tématu [klientská nabízená instalace](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Účet pro připojení k bodu registrace  

Bod registrace používá pro připojení k databázi lokality Configuration Manager **účet pro připojení k bodu registrace** . Ve výchozím nastavení používá svůj počítačový účet, ale můžete místo něj nakonfigurovat uživatelský účet. Pokud je bod registrace v nedůvěryhodné doméně ze serveru lokality, je nutné zadat uživatelský účet. Tento účet vyžaduje oprávnění **ke čtení** a **zápisu** do databáze lokality.  

Další informace najdete v tématu [Instalace rolí systému lokality pro místní](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)správu mobilních zařízení (MDM).


### <a name="exchange-server-connection-account"></a>Účet pro připojení k serveru Exchange  

Webový server používá pro připojení k zadanému serveru Exchange **účet pro připojení** k serveru Exchange. Toto připojení používá k vyhledání a správě mobilních zařízení, která se připojují k systému Exchange Server. Tento účet vyžaduje rutiny Exchange PowerShell, které poskytují nezbytné oprávnění pro počítač serveru Exchange. Další informace o rutinách najdete v tématu [instalace a konfigurace konektoru Exchange](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Účet pro připojení k bodu správy  

Bod správy používá k připojení k databázi lokality Configuration Manager **účet pro připojení k bodu správy** . Pomocí tohoto připojení odesílají a načítají informace pro klienty. Bod správy ve výchozím nastavení používá svůj počítačový účet, ale můžete místo něj nakonfigurovat uživatelský účet. Pokud je bod správy v nedůvěryhodné doméně ze serveru lokality, je nutné zadat uživatelský účet.  

Vytvořte účet jako místní účet s omezenými právy v počítači, na kterém je spuštěný Microsoft SQL Server.  

> [!IMPORTANT]  
> Neudělujete k tomuto účtu interaktivní přihlašovací práva.  


### <a name="multicast-connection-account"></a>Účet pro připojení vícesměrového vysílání  

Distribuční body s povoleným vícesměrovým vysíláním používají **účet pro připojení vícesměrového** vysílání ke čtení informací z databáze lokality. Server ve výchozím nastavení používá svůj počítačový účet, ale můžete místo něj nakonfigurovat uživatelský účet. Pokud se databáze lokality nachází v nedůvěryhodné doménové struktuře, musíte zadat uživatelský účet. Pokud například datové centrum obsahuje hraniční síť v jiné doménové struktuře než server lokality a databáze lokality, použijte tento účet ke čtení informací vícesměrového vysílání z databáze lokality.  

Pokud potřebujete tento účet, vytvořte ho jako místní účet s omezenými právy v počítači, na kterém běží Microsoft SQL Server.  

> [!IMPORTANT]  
> Neudělujete k tomuto účtu interaktivní přihlašovací práva.  

Další informace najdete v tématu [použití vícesměrového vysílání k nasazení Windows přes síť](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Účet přístupu k síti  

Klientské počítače používají **účet přístupu k síti** , když nemohou použít svůj místní počítač k přístupu k obsahu v distribučních bodech. Většinou platí pro klienty pracovní skupiny a počítače z nedůvěryhodných domén. Tento účet se používá také během nasazování operačního systému, když počítač, který instaluje operační systém, ještě nemá účet počítače v doméně.  

> [!Important]  
> Účet přístupu k síti se nikdy nepoužívá jako kontext zabezpečení pro spouštění programů, instalaci softwarových aktualizací nebo spouštění pořadí úloh. Používá se pouze pro přístup k prostředkům v síti.  

Klient Configuration Manager se nejprve pokusí použít svůj počítačový účet ke stažení obsahu. Pokud dojde k chybě, bude automaticky proveden pokus o účet přístupu k síti.  

Od verze 1806 může klient připojený k pracovní skupině nebo klientovi připojenému k Azure AD bezpečně přistupovat k obsahu z distribučních bodů bez nutnosti účtu přístupu k síti. Toto chování zahrnuje scénáře nasazení operačního systému s pořadím úkolů spuštěným ze spouštěcího média, PXE nebo centra softwaru. Další informace najdete v tématu [Rozšířená http](enhanced-http.md).<!--1358228,1358278-->

> [!Note]  
> Pokud povolíte **Rozšířený protokol HTTP** tak, aby nevyžadoval účet přístupu k síti, musí mít distribuční bod spuštěný systém Windows Server 2012 nebo novější. <!--SCCMDocs-pr issue #2696-->
>  
> Než povolíte tuto funkci, upgradujte klienty alespoň na verzi 1806. Pokud povolíte jenom **Rozšířená připojení HTTP** , starší klienti se pomocí této metody nemůžou ověřit, takže balíček aktualizace klienta nepůjde stáhnout z distribučního bodu. <!--vso2841213-->   

#### <a name="permissions"></a>Oprávnění

Udělte tomuto účtu minimální vhodná oprávnění k přístupu k obsahu, který klient vyžaduje pro přístup k softwaru. Účet musí mít **přístup k tomuto počítači ze sítě** přímo v distribučním bodě. Pro každý web můžete nakonfigurovat až 10 účtů přístupu k síti.  

Vytvořte účet v libovolné doméně, která poskytuje nezbytný přístup k prostředkům. Účet přístupu k síti musí vždy zahrnovat název domény. Předávací zabezpečení není u tohoto účtu podporováno. Pokud máte distribuční body ve více doménách, vytvořte účet v důvěryhodné doméně.  

> [!TIP]  
> Aby nedošlo k uzamknutí účtu, neměňte heslo stávajícího účtu přístupu k síti. Místo toho vytvořte nový účet a nastavte nový účet v Configuration Manager. Po uplynutí dostatečné doby, aby všichni klienti obdrželi nové podrobnosti účtu, odstraňte starý účet ze sdílených síťových složek a účet odstraňte.  

> [!IMPORTANT]  
> Neudělujete k tomuto účtu interaktivní přihlašovací práva.  
>   
> Neudělujte tomuto účtu oprávnění k připojování počítačů k doméně. Pokud je nutné během sekvence úlohy připojit počítače k doméně, použijte [účet pro připojení k doméně pořadí úkolů](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Konfigurace účtu přístupu k síti  

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Pak vyberte lokalitu.  

2.  Ve skupině **Nastavení** na pásu karet vyberte možnost **Konfigurovat součásti webu**a zvolte možnost **distribuce softwaru**.  

3.  Zvolte kartu **účet přístupu k síti** . Nastavte jeden nebo víc účtů a pak zvolte **OK**.  


### <a name="package-access-account"></a>Účet pro přístup k balíčku  

**Účet pro přístup k balíčku** umožňuje nastavit oprávnění systému souborů NTFS a zadat uživatele a skupiny uživatelů, kteří mají přístup k obsahu balíčku v distribučních bodech. Ve výchozím nastavení Configuration Manager uděluje přístup jenom **uživatelům** a **správcům**účtů obecného přístupu. Přístup pro klientské počítače můžete řídit pomocí dalších účtů nebo skupin systému Windows. Mobilní zařízení vždy načítají obsah balíčku anonymně, takže nepoužívají účet pro přístup k balíčku.  

Ve výchozím nastavení, když Configuration Manager kopíruje soubory obsahu do distribučního bodu, udělí oprávnění ke **čtení** místní skupině **uživatelů** a **Úplné řízení** místní skupině **Administrators** . Skutečná požadovaná oprávnění závisí na balíčku. Pokud máte klienty v pracovních skupinách nebo v nedůvěryhodných doménových strukturách, budou tyto klienti používat účet přístupu k síti pro přístup k obsahu balíčku. Přesvědčte se, zda má účet přístupu k síti oprávnění k balíčku pomocí definovaných účtů pro přístup k balíčkům.  

Použijte účty v doméně s přístupem k distribučním bodům. Pokud vytvoříte nebo upravíte účet po vytvoření balíčku, je třeba balíček znovu distribuovat. Aktualizace balíčku nezmění oprávnění NTFS v balíčku.  

Nemusíte přidávat účet pro přístup k síti jako účet pro přístup k balíčku, protože členství ve skupině **uživatelů** ho přidá automaticky. Omezení účtu pro přístup k balíčku jenom na účet přístupu k síti nezabrání klientům v přístupu k balíčku.  

#### <a name="manage-package-access-accounts"></a>Správa účtů pro přístup k balíčkům  

1.  V konzole Configuration Manager vyberte možnost **softwarová knihovna**.  

2.  V pracovním prostoru **softwarová knihovna** určete typ obsahu, pro který chcete spravovat účty pro přístup, a postupujte podle uvedených kroků:  

    - **Aplikace**: rozbalte možnost **Správa aplikací**, zvolte **aplikace**a pak vyberte aplikaci, pro kterou chcete spravovat účty pro přístup.  

    - **Balíček**: rozbalte možnost **Správa aplikací**, zvolte **balíčky**a pak vyberte balíček, pro který chcete spravovat účty pro přístup.  

    - **Balíček pro nasazení aktualizace softwaru**: rozbalte položku **aktualizace softwaru**, zvolte **balíčky pro nasazení**a potom vyberte balíček pro nasazení, pro který chcete spravovat účty pro přístup.  

    - **Balíček ovladače**: rozbalte možnost **operační systémy**, zvolte **balíčky ovladačů**a pak vyberte balíček ovladačů, pro který chcete spravovat účty pro přístup.  

    - **Bitová kopie operačního**systému: rozbalte možnost **operační systémy**, zvolte **bitové kopie operačního systému**a pak vyberte bitovou kopii operačního systému, pro kterou chcete spravovat účty pro přístup.  

    - **Balíček s upgradem operačního**systému: rozbalte možnost **operační systémy**, zvolte **balíčky s upgradem operačního systému**a pak vyberte balíček s upgradem operačního systému, pro který chcete spravovat účty pro přístup.  

    - **Spouštěcí bitová kopie**: rozbalte možnost **operační systémy**, zvolte **spouštěcí bitové kopie**a pak vyberte spouštěcí bitovou kopii, pro kterou chcete spravovat účty pro přístup.  

3.  Klikněte pravým tlačítkem myši na vybraný objekt a zvolte možnost **Spravovat účty pro přístup**.  

4.  V dialogovém okně **Přidat účet** zadejte typ účtu, kterému bude udělen přístup k obsahu, a pak zadejte přístupová práva spojená s tímto účtem.  

    > [!NOTE]  
    > Když přidáte uživatelské jméno pro účet a Configuration Manager najde jak místní uživatelský účet, tak účet uživatele domény s tímto názvem, Configuration Manager nastaví přístupová práva pro účet uživatele domény.  


### <a name="reporting-services-point-account"></a>Účet bodu služby Reporting Services  
 
SQL Server Reporting Services používá **účet bodu služby Reporting Services** k načtení dat pro sestavy Configuration Manager z databáze lokality. Zadaný uživatelský účet systému Windows a jeho heslo jsou zašifrovány a uloženy v databázi služby SQL Server Reporting Services.  

> [!NOTE]  
> Účet, který zadáte, musí mít oprávnění k **místnímu přihlášení** v počítači, který je hostitelem databáze služby SQL Reporting Services.

> [!NOTE]  
> Účtu se automaticky přiřadí všechna potřebná práva, a to přidáním do role smsschm_users SQL Database v databázi nástroje ConfigMgr.

Další informace najdete v tématu [Úvod do vytváření sestav](../../servers/manage/introduction-to-reporting.md).


### <a name="remote-tools-permitted-viewer-accounts"></a>Účty povolených prohlížečů vzdálených nástrojů  

Účty, které zadáte jako **Povolené prohlížeče** pro vzdálené řízení, představují seznam uživatelů, kterým je povoleno používání funkcí vzdálených nástrojů v klientech.  

Další informace najdete v tématu [Úvod do vzdáleného řízení](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Účet instalace lokality
<!--SCCMDocs issue #572-->
Pomocí doménového uživatelského účtu se přihlaste k serveru, na kterém spouštíte Configuration Manager instalační program a nainstalujete novou lokalitu.

Tento účet vyžaduje následující práva:  

- **Správce** na následujících serverech:
    - Server lokality  
    - Každý server, který je hostitelem databáze lokality  
    - Každá instance poskytovatele služby SMS pro danou lokalitu  

- **Správce** systému v instanci SQL Server, která je hostitelem databáze lokality  

Configuration Manager instalační program automaticky přidá tento účet do skupiny [Admins služby SMS](#sms-admins) .

Po instalaci je tento účet jediným uživatelem s právy ke konzole Configuration Manager. Pokud potřebujete tento účet odebrat, nezapomeňte nejdřív přidat jeho práva k jinému uživateli.

Když rozšíříte samostatnou lokalitu tak, aby zahrnovala lokalitu centrální správy, tento účet vyžaduje oprávnění správce s **úplnými oprávněními** nebo **správcem infrastruktury** v samostatné primární lokalitě.


### <a name="site-system-installation-account"></a>Účet instalace systému lokality  

Webový server používá **účet instalace systému lokality** k instalaci, přeinstalaci, odinstalaci a nastavení systémů lokality. Pokud nastavíte systém lokality tak, aby vyžadoval, aby server lokality inicializoval připojení k tomuto systému lokality, Configuration Manager používá tento účet také k vyžádání dat ze systému lokality po instalaci systému lokality a všech rolí. Každý systém lokality může mít jiný instalační účet, ale můžete nastavit jenom jeden účet instalace pro správu všech rolí v daném systému lokality.  

Tento účet vyžaduje místní oprávnění pro správu v systémech cílových webů. Tento účet navíc musí mít **přístup k tomuto počítači ze sítě** v zásadách zabezpečení v systémech cílové lokality.  

> [!TIP]  
> Máte-li mnoho řadičů domény a tyto účty jsou používány napříč doménami, před nastavením systému lokality ověřte, zda služba Active Directory replikuje tyto účty.  
>   
> Když zadáte místní účet v každém spravovaném systému lokality, bude tato konfigurace bezpečnější než použití doménových účtů. Omezuje škodu, kterou útočníci můžou dělat, pokud dojde k ohrožení bezpečnosti účtu. Účty domény se ale snáze spravují. Zvažte kompromis mezi zabezpečením a efektivní správou.  


### <a name="site-system-proxy-server-account"></a>Účet proxy server systému lokality
<!--SCCMDocs issue #648-->
Následující role systému lokality používají **účet proxy server systému lokality** pro přístup k internetu prostřednictvím proxy server nebo brány firewall, která vyžaduje ověřený přístup:

- Bod synchronizace katalogu Asset Intelligence
- konektor systému Exchange Server
- Spojovací bod služby
- Bod aktualizace softwaru

> [!IMPORTANT]  
> Určete účet, který má nejmenší možná oprávnění pro požadovaný proxy server nebo bránu firewall.  

Další informace najdete v tématu [Podpora proxy serveru](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>Účet pro připojení k serveru SMTP  

Webový server používá účet pro **připojení k serveru SMTP** k odesílání e-mailových upozornění, pokud server SMTP vyžaduje ověřený přístup.  

> [!IMPORTANT]  
> Určete účet s nejmenšími možnými oprávněními k odesílání e-mailů.  

Další informace najdete v tématu [použití výstrah a stavového systému](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Účet pro připojení k bodu aktualizace softwaru  

Webový server používá **účet připojení bodu aktualizace softwaru** pro tyto dvě služby aktualizace softwaru:  

- Windows Server Update Services (WSUS), který nastavuje nastavení, jako jsou definice produktů, klasifikace a nastavení pro odesílání dat.  

- Nástroj WSUS Synchronization Manager, který vyžaduje synchronizaci s nadřazeným serverem WSUS nebo službou Microsoft Update.  

[Účet instalace systému lokality](#site-system-installation-account) může instalovat součásti pro aktualizace softwaru, ale nemůže provádět funkce specifické pro aktualizaci softwaru v bodě aktualizace softwaru. Pokud pro tuto funkci nemůžete použít účet počítače serveru lokality, protože bod aktualizace softwaru je v nedůvěryhodné doménové struktuře, je nutné zadat tento účet kromě účtu instalace systému lokality.  

Tento účet musí být místní správce na počítači, na kterém instalujete službu WSUS. Také musí být součástí místní skupiny **správců služby WSUS** .  

Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).


### <a name="source-site-account"></a>Účet zdrojové lokality  

Proces migrace používá **Účet zdrojové lokality** pro přístup k poskytovateli serveru SMS zdrojové lokality. Tento účet vyžaduje oprávnění **Číst** k objektům lokality ve zdrojové lokalitě ke shromažďování dat pro úlohy migrace.  

Pokud máte Configuration Manager 2007 distribučních bodů nebo sekundárních lokalit se společně umístěnými distribučními body, pak při upgradu na Configuration Manager (aktuální větev) distribučních bodů musí mít tento účet také oprávnění **Odstranit** pro třídu **lokalita** . Toto oprávnění má úspěšně odebrat distribuční bod z webu Configuration Manager 2007 během upgradu.  

> [!NOTE]  
> Účet zdrojové lokality i [účet databáze zdrojové lokality](#source-site-database-account) jsou označeny jako **Správce migrace** v uzlu **účty** pracovního prostoru **Správa** v konzole nástroje Configuration Manager.  

Další informace najdete v tématu [migrace dat mezi hierarchiemi](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Účet databáze zdrojové lokality  

Proces migrace používá **účet databáze zdrojové lokality** pro přístup k databázi SQL Server pro zdrojovou lokalitu. Chcete-li shromáždit data z databáze SQL Server zdrojové lokality, musí mít účet databáze zdrojové lokality oprávnění **číst** a **spustit** pro databázi SQL Server zdrojové lokality.  

Pokud používáte účet počítače Configuration Manager (aktuální větev), ujistěte se, že pro tento účet platí všechny následující podmínky:  
  
- Je členem skupiny zabezpečení **Distributed COM Users** ve stejné doméně jako lokalita Configuration Manager 2007.  
- Je členem skupiny zabezpečení **SMS Admins** .  
- Má oprávnění **číst** ke všem objektům Configuration Manager 2007.  

> [!NOTE]  
> Účet zdrojové lokality i [účet databáze zdrojové lokality](#source-site-database-account) jsou označeny jako **Správce migrace** v uzlu **účty** pracovního prostoru **Správa** v konzole nástroje Configuration Manager.  

Další informace najdete v tématu [migrace dat mezi hierarchiemi](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Účet připojení k doméně pořadí úloh 

Instalační program systému Windows používá k připojení nově připojeného počítače k doméně **účet pro připojení k doméně pořadí úkolů** . Tento účet vyžaduje krok pořadí úkolů [připojit k doméně nebo pracovní skupině](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) s možností **připojit k doméně** . Tento účet je také možné nastavit pomocí kroku [použít nastavení sítě](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings) , není ale vyžadován.  

Tento účet vyžaduje právo **k připojení k doméně** v cílové doméně.  

> [!TIP]  
> Vytvořte jeden uživatelský účet domény s minimálními oprávněními pro připojení k doméně a použijte ho pro všechna pořadí úkolů.  

> [!IMPORTANT]  
> Nepřiřazujte k tomuto účtu oprávnění k interaktivnímu přihlašování.  
>   
> Pro tento účet nepoužívejte účet pro přístup k síti.  


### <a name="task-sequence-network-folder-connection-account"></a>Účet připojení síťové složky pořadí úloh  

Modul pořadí úloh používá **účet připojení síťové složky pořadí úkolů** pro připojení ke sdílené složce v síti. Tento účet vyžaduje krok pořadí úkolů [připojit k síťové složce](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .  

Tento účet vyžaduje oprávnění pro přístup k zadané sdílené složce. Musí se jednat o účet uživatele domény.  

> [!TIP]  
> Vytvořte jeden uživatelský účet domény s minimálními oprávněními pro přístup k požadovaným síťovým prostředkům a použijte ho pro všechna pořadí úloh.  

> [!IMPORTANT]  
> Nepřiřazujte k tomuto účtu oprávnění k interaktivnímu přihlašování.  
>   
> Pro tento účet nepoužívejte účet pro přístup k síti.  


### <a name="task-sequence-run-as-account"></a>Účet Spustit jako pořadí úloh  

Modul pořadí úloh používá **účet Spustit jako pořadí úloh** ke spouštění příkazových řádků nebo skriptů PowerShellu s jinými přihlašovacími údaji, než je účet místního systému. Tento účet je vyžadován pomocí [příkazového řádku spustit](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) a [Spustit skript prostředí PowerShell](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) s možností **Spustit tento krok jako následující účet** .  

Nastavte účet tak, aby měl minimální oprávnění potřebná pro spuštění příkazového řádku, který zadáte v pořadí úkolů. Účet vyžaduje interaktivní přihlašovací práva. Obvykle vyžaduje možnost instalovat software a přistupovat k síťovým prostředkům. Pro úlohu spustit skript prostředí PowerShell vyžaduje tento účet oprávnění místního správce. 

> [!IMPORTANT]  
> Pro tento účet nepoužívejte účet pro přístup k síti.  
>   
> Nikdy neprovádějte účet správci domény.  
>   
> Pro tento účet nikdy nenastavte cestovní profily. Když je pořadí úkolů spuštěné, stáhne profil roamingu pro tento účet. Tím se profil pro přístup k místnímu počítači ponechá zranitelně.  
>   
> Omezte rozsah účtu. Vytvořte například různé účty spuštění pořadí úloh jako pro každé pořadí úloh. Pokud dojde k ohrožení bezpečnosti jednoho účtu, budou ohroženy pouze klientské počítače, ke kterým má tento účet přístup.  
>   
> Pokud příkazový řádek vyžaduje v počítači přístup správce, zvažte vytvoření místního účtu správce výhradně pro tento účet na všech počítačích, které spouští pořadí úkolů. Odstraňte účet, jakmile ho už nebudete potřebovat.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a>Uživatelské objekty, které Configuration Manager používá v SQL 
<!--SCCMDocs issue #1160-->
Configuration Manager automaticky vytvoří a zachová následující objekty uživatele v SQL.  Tyto objekty jsou umístěné v rámci databáze Configuration Manager v části zabezpečení/uživatelé.  

> [!IMPORTANT]  
>  Úprava nebo odebrání těchto objektů může způsobit drastické problémy v prostředí Configuration Manager.  Pro tyto objekty nedoporučujeme provádět žádné změny.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Tento objekt se používá ke spouštění dotazů v kontextu, který je jen pro čtení.  Tento objekt se využívá s několika uloženými procedurami.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Tento objekt slouží k poskytování oprávnění pro dynamické příkazy SQL.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Tento objekt se používá ke spouštění SQL Reporting provádění.  S touto funkcí se používá následující uložená procedura: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Databázové role, které Configuration Manager používá v SQL
<!--SCCMDocs issue #1160-->
Configuration Manager automaticky vytvoří a zachová následující objekty role v SQL. Tyto role poskytují přístup ke konkrétním uloženým procedurám, tabulkám, zobrazením a funkcím, aby bylo možné provádět potřebné akce jednotlivých rolí buď k načtení dat, nebo k vložení dat do a z databáze nástroje ConfigMgr. Tyto objekty jsou umístěné v rámci databáze Configuration Manager v části zabezpečení/role/databázové role.

> [!IMPORTANT]  
> Úprava nebo odebrání těchto objektů může způsobit drastické problémy v prostředí Configuration Manager.  Pro tyto objekty nedoporučujeme provádět žádné změny.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Import multilicencí funkce Asset Intelligence. Nástroj ConfigMgr udělí toto oprávnění účtům uživatelů na základě přístupu RBA, aby mohl importovat multilicence pro použití s funkce Asset Intelligence.  Tento účet může být přidán pomocí role úplného správce nebo role správce prostředků.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Synchronizace aktualizace funkce Asset Intelligence. ConfigMgr uděluje účet počítače, který je hostitelem účtu bodu synchronizace funkce Asset Intelligence, aby získal přístup k datům proxy serveru funkce Asset Intelligence a zobrazila nevyřízená data AI pro nahrání.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Vzdálená správa. Tuto roli používá Configuration Manager role AMT k načtení dat na zařízeních, která podporují technologii Intel AMT.

> [!NOTE]  
> Tato role je v novějších verzích nástroje ConfigMgr zastaralá.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Podpora služby System Center Endpoint Protection pro body registrace certifikátu (SCEP). Nástroj ConfigMgr uděluje oprávnění k účtu počítače v systému lokality, který podporuje bod registrace certifikátu pro podporu SCEP pro podepsání a obnovení certifikátu.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

Podpora pro bod registrace certifikátu: PFX. Nástroj ConfigMgr uděluje oprávnění k účtu počítače systému lokality, který podporuje bod registrace certifikátu nakonfigurovaný pro podporu PFX pro podepisování a obnovování.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Bod správy zařízení. Nástroj ConfigMgr udělí toto oprávnění k účtu počítače pro bod správy, který má možnost "Povolit mobilním zařízením a počítačům Mac používat tento bod správy", schopnost poskytovat podporu pro zařízení zaregistrovaná v MDM.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Spojovací bod služby. ConfigMgr udělí toto oprávnění k účtu počítače, který je hostitelem spojovacího bodu služby, aby načetl a poskytoval data telemetrie, spravovala cloudové služby a načetla aktualizace služby.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Distribuovaná zobrazení. Pokud je vybrána možnost SQL Server distribuovaná zobrazení ve vlastnostech odkazu replikace, Configuration Manager udělí toto oprávnění účtu počítače primárních serverů lokality na certifikačních autoritách.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Datový sklad. Nástroj ConfigMgr udělí toto oprávnění k účtu počítače, který je hostitelem role datového skladu.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Bod registrace. ConfigMgr udělí toto oprávnění k účtu počítače, který je hostitelem bodu registrace a povoluje registraci zařízení přes MDM.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Poskytuje přístup ke všem zobrazením rozšířených schémat.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Služba Hierarchy Manager. ConfigMgr uděluje oprávnění k tomuto účtu pro správu zpráv o stavu převzetí služeb při selhání a transakce SQL Server Broker mezi lokalitami v rámci hierarchie.

> [!NOTE]  
> Role smdbrole_WebPortal je ve výchozím nastavení členem této role.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Služba vícesměrového vysílání. Nástroj ConfigMgr udělí toto oprávnění k účtu počítače distribučního bodu, který podporuje vícesměrové vysílání.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Bod správy. Nástroj ConfigMgr udělí toto oprávnění k účtu počítače, který je hostitelem role bodu správy, aby poskytoval podporu pro klienty nástroje ConfigMgr.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Správa a monitorování nástrojem Microsoft BitLocker v bodu správy. Nástroj ConfigMgr udělí toto oprávnění účtu počítače, který je hostitelem bodu správy, který spravuje MBAM pro prostředí.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Žádost o aplikaci bodu správy Nástroj ConfigMgr udělí toto oprávnění k účtu počítače, který je hostitelem bodu správy, aby podporoval požadavky na aplikace založené na uživatelích.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

Poskytovatel serveru SMS. Configuration Manager udělí toto oprávnění účtu počítače, který je hostitelem role poskytovatele služby SMS.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Server lokality. ConfigMgr udělí toto oprávnění účtu počítače, který je hostitelem primární lokality nebo lokality CAS.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Bod aktualizace softwaru. ConfigMgr udělí toto oprávnění účtu počítače, který je hostitelem bodu aktualizace softwaru pro práci s aktualizacemi třetích stran.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Bod webu Katalog aplikací. Nástroj ConfigMgr uděluje oprávnění k účtu počítače, který je hostitelem bodu webu Application Catalog, aby poskytoval nasazení aplikace založené na uživateli.

### <a name="smsschm_users"></a>smsschm_users

Přístup k vytváření sestav uživatelů Nástroj ConfigMgr uděluje přístup k účtu, který se používá pro účet bodu služby Reporting Services, aby povoloval přístup k zobrazením sestav SMS, aby mohl zobrazovat data Configuration Manager sestav.  Data jsou dále omezená pomocí RBA.
