---
title: Podporované verze SQL Server
titleSuffix: Configuration Manager
description: Získat SQL Server požadavky na verzi a konfiguraci pro hostování databáze Configuration Manager lokality.
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bda64f11d5d2ee9498ce69224ec9a52efc0df902
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700329"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Podporované verze SQL Server pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Každá Configuration Manager lokalita vyžaduje podporovanou SQL Server verzi a konfiguraci pro hostování databáze lokality.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server instance a umístění

### <a name="central-administration-site-and-primary-sites"></a>Lokalita centrální správy a primární lokality

Databáze lokality musí používat úplnou instalaci SQL Server.  

SQL Server může být umístěn na:  

- Počítač serveru lokality.  
- Počítač, který je vzdálený od serveru lokality.  

Jsou podporovány následující instance:  

- Výchozí nebo pojmenovaná instance SQL Server.  
- Konfigurace s více instancemi.  
- Cluster SQL Server. Viz [použití clusteru SQL Server k hostování databáze lokality](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- Skupina dostupnosti SQL Server AlwaysOn. Další informace najdete v tématu [SQL Server AlwaysOn pro databázi lokality s vysokou dostupností](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="secondary-sites"></a>Sekundární lokality

Databáze lokality může používat výchozí instanci úplné instalace SQL Server nebo SQL Server Express.  

SQL Server se musí nacházet na počítači serveru lokality.  

### <a name="limitations-to-support"></a>Omezení podpory

Následující konfigurace nejsou podporovány:

- Cluster SQL Server v konfiguraci clusteru služby Vyrovnávání zatížení sítě (NLB)
- Cluster SQL Server v sdílený svazek clusteru (CSV)
- SQL Server technologie zrcadlení databáze a replikace peer-to-peer

SQL Server transakční replikace je podporovaná jenom pro replikaci objektů na body správy, které jsou nakonfigurované pro použití [replik databáze](../../servers/deploy/configure/database-replicas-for-management-points.md).  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Podporované verze SQL Server

V hierarchii s více lokalitami můžou různé lokality používat k hostování databáze lokality různé verze SQL Server. Pokud jsou splněné následující položky:

- Configuration Manager podporuje verze SQL Server, které používáte.
- Používané verze SQL Server zůstávají v podpoře Microsoftu.
- SQL Server podporuje replikaci mezi dvěma verzemi SQL Server. Další informace najdete v tématu [zpětné kompatibility replikace SQL Server](/sql/relational-databases/replication/replication-backward-compatibility).

Pro SQL Server 2016 a předchozí se podpora každé verze SQL a aktualizace Service Pack řídí [zásadami životního cyklu Microsoftu](https://aka.ms/sqllifecycle). Podpora pro konkrétní aktualizaci Service Pack SQL Server zahrnuje kumulativní aktualizace, pokud nepřeruší zpětnou kompatibilitu se základní verzí aktualizace Service Pack. Počínaje SQL Server 2017 se aktualizace Service Pack neuvolní, protože se řídí [moderním modelem údržby](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server). Tým SQL Server doporučuje průběžnou a [aktivní instalaci kumulativních aktualizací](/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) , jakmile budou k dispozici.

Pokud není uvedeno jinak, jsou podporovány následující verze SQL Server se všemi aktivními verzemi Configuration Manager. Pokud se přidá podpora pro novou verzi SQL Server, poznamenala se Configuration Manager verze, která tuto podporu přidává. Podobně, pokud je podpora zastaralá, vyhledejte podrobnosti o ovlivněných verzích Configuration Manager.

> [!IMPORTANT]  
> Když použijete SQL Server Standard pro databázi v lokalitě centrální správy, omezíte celkový počet klientů, které může hierarchie podporovat. Viz [Dimenzování a škálování](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standard, Enterprise

Počínaje verzí 1910 Configuration Manager můžete použít tuto verzi s kumulativní aktualizací 5 (CU5) nebo novější, pokud je vaše kumulativní aktualizace podporována životním cyklem SQL. CU5 je minimální požadavek na SQL Server 2019, protože řeší problém s [obložením skalárního systému souborů UDF](/sql/relational-databases/user-defined-functions/scalar-udf-inlining).

Tuto verzi SQL lze použít pro následující lokality:

- Lokalita centrální správy
- Primární lokalita
- Sekundární lokalita

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise

Tuto verzi můžete použít s [kumulativní aktualizací Update 2](https://support.microsoft.com/help/4052574) nebo vyšší, pokud je vaše kumulativní aktualizace podporována životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
<!--514985-->
Tuto verzi můžete použít s minimální aktualizací Service Pack a kumulativní aktualizací podporovanou životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard, Enterprise

Tuto verzi můžete použít s minimální aktualizací Service Pack a kumulativní aktualizací podporovanou životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard, Enterprise

Tuto verzi můžete použít s minimální aktualizací Service Pack a kumulativní aktualizací podporovanou životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

Tuto verzi můžete použít s [kumulativní aktualizací Update 2](https://support.microsoft.com/help/4052574) nebo vyšší, pokud je vaše kumulativní aktualizace podporována životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Sekundární lokalita
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

Tuto verzi můžete použít s minimální aktualizací Service Pack a kumulativní aktualizací podporovanou životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Sekundární lokalita

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

Tuto verzi můžete použít s minimální aktualizací Service Pack a kumulativní aktualizací podporovanou životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Sekundární lokalita  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

Tuto verzi můžete použít s minimální aktualizací Service Pack a kumulativní aktualizací podporovanou životním cyklem SQL. Tuto verzi SQL lze použít pro následující lokality:

- Sekundární lokalita  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Požadované konfigurace pro SQL Server

Následující konfigurace jsou vyžadovány všemi instalacemi SQL Server, které používáte pro databázi lokality, včetně SQL Server Express. Když Configuration Manager nainstaluje SQL Server Express jako součást instalace sekundární lokality, vytvoří tyto konfigurace automaticky.  

### <a name="sql-server-architecture-version"></a>Verze architektury SQL Server

Configuration Manager vyžaduje pro hostování databáze lokality 64 verze SQL Server.  

### <a name="database-collation"></a>Kolace databáze

V každé lokalitě musí obě instance SQL Server používané pro lokalitu a databázi lokality používat následující kolaci: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager podporuje dvě výjimky této kolace pro standard Čína GB18030. Další informace najdete v tématu [mezinárodní podpora](../hierarchy/international-support.md).  

### <a name="database-compatibility-level"></a>Úroveň kompatibility databáze

Configuration Manager vyžaduje, aby úroveň kompatibility databáze lokality nebyla nižší než nejnižší podporovaná verze SQL Server pro Configuration Manager verzi. Například počínaje verzí 1702 potřebujete [úroveň kompatibility databáze](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) větší nebo rovnou 110. <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server funkce

Každý server lokality vyžaduje pouze funkci **Služby databázového stroje**.  

Configuration Manager replikace databáze nevyžaduje funkci **replikace SQL Server** . Tato konfigurace SQL Server se ale vyžaduje v případě, že [pro body správy používáte repliky databáze](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="windows-authentication"></a>Ověřování systému Windows

Configuration Manager vyžaduje **ověřování systému Windows** k ověření připojení k databázi.  

### <a name="sql-server-instance"></a>Instance SQL Server

Pro každou lokalitu použijte vyhrazenou instanci SQL Server. Instancí může být **pojmenovaná instance** nebo **výchozí instance**.  

### <a name="sql-server-memory"></a>SQL Server paměti

Vyhradit paměť pro SQL Server pomocí SQL Server Management Studio. V části **možnosti paměti serveru**nastavte nastavení **Minimální paměti serveru** . Další informace o konfiguraci tohoto nastavení najdete v tématu [SQL Server možnosti konfigurace paměťového serveru](/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Pro databázový server, který nainstalujete na stejný počítač jako server lokality**, omezte paměť pro SQL Server na 50 až 80 procent dostupné adresovatelné systémové paměti.  

- **U vyhrazeného databázového serveru, který je vzdálený od serveru lokality**: omezte velikost paměti SQL Server na 80 až 90 procent dostupné adresovatelné systémové paměti.  

- **V případě rezervy paměti pro fond vyrovnávacích pamětí každé používané instance SQL Server**:  

  - Pro lokalitu centrální správy: nastavte minimálně 8 GB.  
  - Pro primární lokalitu: nastavte minimálně 8 GB.  
  - Pro sekundární lokalitu: nastavte minimálně 4 GB.  

### <a name="sql-nested-triggers"></a>Vnořené aktivační události SQL

Vnořené aktivační události SQL. musí být povolené. Další informace najdete v tématu [Konfigurace možnosti konfigurace serveru s vnořenými triggery](/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option) .

### <a name="sql-server-clr-integration"></a>Integrace modulu CLR SQL Serveru

Databáze lokality vyžaduje, aby byl povolen modul CLR (Common Language Runtime) SQL Serveru. Tato možnost je povolena automaticky při instalaci Configuration Manager. Další informace o modulu CLR naleznete v tématu [Úvod do SQL Server Integration CLR](/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

SQL Server Service Broker se vyžaduje pro replikaci mezi lokalitami i pro jednu primární lokalitu.

### <a name="trustworthy-setting"></a>DŮVĚRYHODNÉ nastavení

Configuration Manager automaticky povolí [vlastnost důvěryhodné databáze](/sql/relational-databases/security/trustworthy-database-property)SQL. Tato vlastnost je požadována Configuration Manager, aby byla **zapnuta**.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Volitelné konfigurace pro SQL Server

Následující konfigurace jsou volitelné pro každou databázi, která používá úplnou instalaci SQL Serveru.  

### <a name="sql-server-service"></a>Služba SQL Server

Můžete nakonfigurovat, že služba SQL Serveru běží s účtem:  

- Účet *uživatele domény s nízkými právy* :  

  - Tato konfigurace je osvědčeným postupem a může vyžadovat ruční registraci hlavního názvu služby (SPN) pro tento účet.  

- **Místní systémový** účet počítače, na kterém běží SQL Server:  

  - Proces konfigurace zjednodušíte použitím místního systémového účtu.  
  - Když použijete místní systémový účet, Configuration Manager automaticky registruje hlavní název služby pro SQL Server službu.  
  - Použití místního systémového účtu pro službu SQL Server není osvědčeným postupem SQL Server.  

Pokud počítač se systémem SQL Server nepoužívá ke spuštění služby SQL Server svůj místní systémový účet, nakonfigurujte hlavní název služby (SPN) účtu, který spouští službu SQL Server v Active Directory Domain Services. (Při použití systémového účtu se hlavní název služby (SPN) automaticky zaregistruje za vás.)

Informace o SPN pro databázi lokality najdete v tématu [Správa hlavního názvu služby (SPN) pro server databáze lokality](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

Informace o tom, jak změnit účet, který používá služba SQL Server, najdete v tématu [SCM Services – změna spouštěcího účtu služby](/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services se vyžaduje pro instalaci bodu služby Reporting Services, který umožňuje spouštět sestavy. Configuration Manager podporuje stejné verze SQL Server pro vytváření sestav, protože jsou pro databázi lokality.

Další informace najdete v tématu [předpoklady pro vytváření sestav v Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> Po upgradu SQL Server z předchozí verze se může zobrazit následující chyba: *Tvůrce sestav neexistuje*.  
> Chcete-li tuto chybu vyřešit, je nutné znovu nainstalovat roli systému lokality bodu služby Reporting Services.  

### <a name="data-warehouse-service-point"></a>Bod služby datového skladu

Datový sklad používá samostatnou databázi. Můžete ho hostovat na serveru databáze lokality nebo na samostatném SQL Server. Další informace najdete v [bodu služby datového skladu pro Configuration Manager](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>Porty SQL Server

Pro komunikaci s databázovým strojem SQL Server a pro replikaci mezi lokalitami můžete použít výchozí konfiguraci SQL Server portů nebo zadat vlastní porty:  

- **Komunikace mezi lokalitami** používá SQL Server Service Broker, která ve výchozím nastavení používá port TCP 4022.  
- **Komunikace** mezi lokalitami mezi SQL Server databázovým strojem a různými Configuration Manager role systému lokality ve výchozím nastavení používá port TCP 1433. Následující role systému lokality komunikují přímo s databází SQL Server:  

  - Bod správy  
  - Počítač poskytovatele serveru SMS  
  - Bod služby Reporting services  
  - Server lokality  

Když počítač se systémem SQL Server hostuje databázi z více než jedné lokality, musí každá databáze používat samostatnou instanci SQL Server. Každá instance musí být taky nakonfigurovaná tak, aby používala jedinečnou sadu portů.  

> [!WARNING]  
> Configuration Manager nepodporuje dynamické porty. Vzhledem k tomu, že pojmenované instance systému SQL Server ve výchozím nastavení používají pro připojení k databázovému stroji dynamické porty, musíte při použití pojmenované instance ručně nakonfigurovat statický port, který chcete používat pro komunikaci v lokalitě.  

Pokud máte v počítači se systémem SQL Server povolenou bránu firewall, ujistěte se, že je nakonfigurována tak, aby povolovala porty používané vaším nasazením a v jakémkoli umístění v síti mezi počítači, které komunikují s SQL Server.  

Příklad konfigurace SQL Server pro použití konkrétního portu najdete v tématu [Konfigurace serveru pro naslouchání na specifickém portu TCP](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>Možnosti upgradu pro SQL Server

Pokud potřebujete upgradovat svou verzi SQL Server, použijte jednu z následujících metod od snadno složitějších:  

- [Upgradovat SQL Server místně](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (doporučeno)  

- Nainstalujte novou verzi SQL Server do nového počítače a pak [použijte možnost přesunutí databáze](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) Configuration Manager nastavení, aby se server lokality odkazoval na novou SQL Server  

- Použijte [zálohování a obnovení](../../servers/manage/backup-and-recovery.md). Podpora zálohování a obnovení pro scénář upgradu SQL je podporovaná. Požadavek na správu verzí SQL můžete ignorovat při kontrole [důležitých informací před obnovování lokality](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site).