---
title: AlwaysOn SQL Serveru
titleSuffix: Configuration Manager
description: Plánování použití skupiny dostupnosti Always On SQL Server s Configuration Manager
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce8c10d9d59d97caa53ece12dd43d90c78546bb
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384838"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Příprava na používání skupin dostupnosti Always On SQL Server s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek slouží k přípravě Configuration Manager k používání skupin dostupnosti Always On SQL Server. Tato funkce poskytuje řešení pro zajištění vysoké dostupnosti a zotavení po havárii pro databázi lokality.  

Configuration Manager podporuje používání skupin dostupnosti:

- V primárních lokalitách a lokalitě centrální správy.
- Místně nebo v Microsoft Azure.

Když v Microsoft Azure použijete skupiny dostupnosti, můžete dál zvýšit dostupnost vaší databáze lokality pomocí skupin *dostupnosti Azure*. Další informace o skupinách dostupnosti služby Azure najdete v tématu [Správa dostupnosti virtuálních počítačů](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
> Než budete pokračovat, je vhodné nakonfigurovat skupiny dostupnosti SQL Server a SQL Server. Níže uvedené informace odkazují na knihovnu a postupy dokumentace k SQL Server.


## <a name="supported-scenarios"></a>Podporované scénáře

Následující scénáře jsou podporovány pro používání skupin dostupnosti s Configuration Manager. Další informace a postupy pro jednotlivé scénáře najdete v tématu [Konfigurace skupin dostupnosti pro Configuration Manager](configure-aoag.md).

- [Vytvoření skupiny dostupnosti pro použití s Configuration Manager](configure-aoag.md#bkmk_create)  
- [Konfigurace lokality pro použití skupiny dostupnosti](configure-aoag.md#bkmk_configure)  
- [Přidání nebo odebrání členů synchronní repliky ze skupiny dostupnosti, která je hostitelem databáze lokality](configure-aoag.md#bkmk_sync)  
- [Konfigurace nebo obnovení lokality z asynchronních replik potvrzení](configure-aoag.md#bkmk_async)  
- [Přesun databáze lokality ze skupiny dostupnosti do výchozí nebo pojmenované instance samostatného SQL Server](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Požadavky

Následující požadavky platí pro všechny scénáře. Pokud se další předpoklady vztahují na konkrétní scénář, jsou v tomto scénáři podrobně popsané.

### <a name="configuration-manager-accounts-and-permissions"></a>Účty Configuration Manager a oprávnění

#### <a name="installation-account"></a>Účet instalace

Účet, který použijete ke spuštění instalačního programu Configuration Manager, musí být:

- Člen místní skupiny **Administrators** na každém počítači, který je členem skupiny dostupnosti.
- **Správce sysadmin** na každé instanci SQL Server, která je hostitelem databáze lokality.

#### <a name="site-server-to-replica-member-access"></a>Webový server pro přístup ke členům repliky

Účet počítače serveru lokality musí být členem místní skupiny **Administrators** na každém počítači, který je členem skupiny dostupnosti.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Verze

Každá replika ve skupině dostupnosti musí používat verzi SQL Server, kterou podporuje vaše verze Configuration Manager. Když je aplikace SQL Server podporovaná, můžou různé uzly skupiny dostupnosti spouštět různé verze SQL Server. Další informace najdete v tématu [podporované verze SQL Server pro Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edice

Použijte SQL Server edice *Enterprise* .

#### <a name="account"></a>Účet

Každá instance SQL Server může běžet pod účtem uživatele domény (**účet služby**) nebo účtem mimo doménu. Každá replika ve skupině může mít jinou konfiguraci.

- Použijte účet s nejnižšími možnými oprávněními. Další informace najdete v tématu [požadavky na zabezpečení pro instalaci SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Další informace o konfiguraci účtů služeb a oprávnění pro SQL Server najdete v tématu [Konfigurace účtů a oprávnění služby systému Windows](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Chcete-li použít účet, který není doménovým účtem, je nutné použít certifikáty. Další informace najdete v tématu [použití certifikátů pro koncový bod zrcadlení databáze (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Další informace najdete v tématu [Vytvoření koncového bodu zrcadlení databáze pro skupiny dostupnosti Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>databáze

#### <a name="configure-the-database-on-a-new-replica"></a>Konfigurace databáze na nové replice

Nakonfigurujte databázi každé repliky s následujícím nastavením:  

- Povolit **integraci CLR**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Další informace naleznete v tématu [Integrace modulu CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Nastavte **repl velikost textu** na `2147483647` :  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Nastavte vlastníka databáze na *účet sa*. Tento účet není potřeba povolit.

- Zapnout **ON** **důvěryhodné** nastavení:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Další informace najdete v tématu [důvěryhodná vlastnost databáze](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).

- Povolit **Service Broker**:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Možnost Service Broker nemůžete povolit u databáze, která už je součástí skupiny dostupnosti. Tuto možnost musíte povolit, než ji přidáte do skupiny dostupnosti.<!-- SCCMDocs#1432 -->

- Nakonfigurujte prioritu Service Broker:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Tyto konfigurace proveďte pouze v primární replice. Chcete-li nakonfigurovat sekundární repliku, nejprve převezme primární objekt k sekundárnímu. Tato akce provede sekundární novou primární repliku.

#### <a name="database-verification-script"></a>Skript pro ověření databáze

Spuštěním následujícího skriptu SQL Ověřte konfiguraci databáze pro primární i sekundární repliky. Než budete moci vyřešit problém u sekundární repliky, změňte tuto sekundární repliku jako primární repliku.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Konfigurace skupiny dostupnosti

#### <a name="replica-members"></a>Členové repliky

- Skupina dostupnosti musí mít jednu primární repliku.  

- V rámci skupiny dostupnosti použijte stejný počet a typ replik, jakou vaše verze SQL Server podporuje.

- Můžete použít repliku asynchronního potvrzení k obnovení synchronní repliky. Další informace najdete v tématu [Možnosti obnovení databáze lokality](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager nepodporuje *převzetí služeb při selhání* pro použití repliky asynchronního potvrzení jako databáze lokality. Další informace najdete v tématu [režimy převzetí služeb při selhání a převzetí služeb při selhání (skupiny dostupnosti Always On)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager neověřuje stav repliky asynchronního potvrzování, aby bylo možné potvrdit, že je aktuální. Použití repliky asynchronního potvrzení jako databáze lokality může ohrozit integritu vašeho webu a ohrožení dat. Tato replika nemůže být synchronizovaná podle návrhu. Další informace najdete v tématu [Přehled skupin dostupnosti Always On SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Každý člen repliky musí mít následující konfiguraci:

- Použití *výchozí instance* nebo *pojmenované instance*  

- Nastavení **připojení v primární roli** **umožňují všechna připojení** .  

- **Načtení sekundárního** nastavení je **Ano** .  

- Povolení **ručního převzetí služeb při selhání**

    > [!Note]
    > Ve verzi 1902 a starší musíte nakonfigurovat všechny skupiny dostupnosti na SQL Server pro ruční převzetí služeb při selhání. Tato konfigurace je nutná i v případě, že není hostitelem databáze lokality.
    >
    > Počínaje verzí 1906 podporuje Configuration Manager při nastavení **automatického převzetí služeb při selhání**používat synchronní repliky skupiny dostupnosti. Nastavit **ruční převzetí služeb při selhání** v těchto případech:
    >
    > - Spuštěním instalačního programu Configuration Manager určíte použití databáze lokality ve skupině dostupnosti.  
    > - Nainstalujete jakoukoli aktualizaci Configuration Manager. (Ne jen aktualizace, které se vztahují k databázi lokality).  

- Všichni členové potřebují stejný [režim osazení](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).<!-- SCCMDocs-pr#3899 --> Instalační program Configuration Manager obsahuje kontrolu předpokladů pro ověření této konfigurace při vytváření databáze prostřednictvím instalace nebo obnovení.

    > [!Note]  
    > Když instalační program vytvoří databázi a nakonfigurujete **Automatické** osazení, Skupina dostupnosti musí mít oprávnění k vytvoření databáze. Tento požadavek platí pro novou databázi i obnovení. Další informace najdete v tématu [Automatické osazení pro sekundární repliku](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Umístění člena repliky

Buď můžete hostovat všechny repliky ve skupině dostupnosti místně, nebo je hostovat na Microsoft Azure. Skupina, která obsahuje místního člena a člena v Azure, se nepodporuje.

> [!NOTE]
> Pokud pro SQL Server používáte virtuální počítač Azure, povolte **plovoucí IP adresu**. Další informace najdete v tématu [Konfigurace nástroje pro vyrovnávání zatížení pro skupinu dostupnosti Always On SQL Server ve virtuálních počítačích Azure](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure).<!-- SCCMDocs#1928 -->

Configuration Manager instalační program se musí připojit ke každé replice. Když nastavíte skupinu dostupnosti v Azure a skupina je za interním nebo externím nástrojem pro vyrovnávání zatížení, otevřete následující výchozí porty:

- Mapovač koncových bodů RPC: **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL přes TCP: **tcp 1433**

Po dokončení instalace musí tyto porty zůstat otevřené pro Configuration Manager a analyzátor propojení replikace.<!-- MEMDocs#375 -->

Pro tyto konfigurace můžete použít vlastní porty. Použijte stejné vlastní porty pro koncový bod a na všechny repliky ve skupině dostupnosti.

Aby SQL mohl replikovat data mezi lokalitami, vytvořte pravidlo vyrovnávání zatížení pro každý port v nástroji pro vyrovnávání zatížení Azure. Další informace najdete v tématu [Konfigurace portů s vysokou dostupností pro interní nástroj pro vyrovnávání zatížení](https://docs.microsoft.com/azure/load-balancer/load-balancer-configure-ha-ports).<!-- MEMDocs#252 -->

#### <a name="listener"></a>Naslouchací proces

Skupina dostupnosti musí mít aspoň jeden *naslouchací proces skupiny dostupnosti*. Když nakonfigurujete Configuration Manager k použití databáze lokality ve skupině dostupnosti, použije se virtuální název tohoto naslouchacího procesu. Skupina dostupnosti sice může obsahovat několik posluchačů, Configuration Manager je ale může používat jenom jednou. Další informace najdete v tématu [Vytvoření nebo konfigurace naslouchacího procesu skupiny dostupnosti SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Cesty k souborům

Když spustíte Configuration Manager instalační program a nakonfigurujete lokalitu tak, aby používala databázi ve skupině dostupnosti, musí mít každý sekundární server repliky cestu k souboru SQL Server, která je shodná s cestou k souboru pro soubory databáze lokality v aktuální primární replice. Pokud totožná cesta neexistuje, instalace se nepodaří přidat instanci pro skupinu dostupnosti jako nové umístění databáze lokality.  

Účet místní SQL Server služby musí mít oprávnění **Úplné řízení** k této složce.

Servery sekundární repliky tuto cestu k souboru vyžadují jenom v době, kdy používáte instalační program Configuration Manager k určení instance databáze ve skupině dostupnosti. Po dokončení konfigurace databáze lokality ve skupině dostupnosti můžete odstranit nepoužitou cestu ze serverů sekundární repliky.

Představte si třeba následující scénář:

- Vytvoříte skupinu dostupnosti, která používá tři SQL servery.  

- Server primární repliky je nová instalace systému SQL Server 2014. Ve výchozím nastavení ukládá databázi. MDF a. Soubory LDF v `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` .  

- Upgradovali jste oba servery sekundární repliky na SQL Server 2014 z předchozích verzí. S upgradem tyto servery uchovávají původní cestu k ukládání souborů databáze: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA` .  

- Než přesunete databázi lokality do této skupiny dostupnosti, vytvořte na každém sekundárním serveru repliky tuto cestu k souboru: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` . Tato cesta je duplikátem používané cesty na primární replice, a to i v případě, že sekundární repliky nepoužijí toto umístění souboru.  

- Pak udělíte účtu služby SQL Server v každé sekundární replice přístup k nově vytvořenému umístění souboru na tomto serveru.  

- Teď můžete úspěšně spustit Configuration Manager Setup a nakonfigurovat lokalitu tak, aby používala databázi lokality ve skupině dostupnosti.  

#### <a name="multi-subnet-failover"></a>Převzetí služeb při selhání s více podsítěmi

<!-- SCCMDocs-pr#3734 -->
Počínaje verzí 1906 můžete povolit [klíčové slovo připojovacího řetězce MultiSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) v SQL Server. Také je nutné ručně přidat následující hodnoty do registru systému Windows na serveru lokality:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> Použití [vysoké dostupnosti serveru lokality](site-server-high-availability.md) a SQL Server Always On s převzetím služeb při selhání s více podsítěmi neposkytuje úplné možnosti automatického převzetí služeb při selhání pro scénáře zotavení po havárii.

Pokud potřebujete vytvořit skupinu dostupnosti s členem ve vzdáleném umístění, nastavte prioritu podle nejnižší latence sítě. Vysoká latence sítě může způsobit selhání replikace.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Omezení a známé problémy

Následující omezení platí pro všechny scénáře.

### <a name="unsupported-sql-server-options-and-configurations"></a>Nepodporované možnosti a konfigurace SQL Server

- **Základní skupiny dostupnosti**: představené se systémem SQL Server 2016 Standard Edition. základní skupiny dostupnosti nepodporují přístup pro čtení sekundárních replik. Konfigurace vyžaduje tento přístup. Další informace najdete v tématu [základní skupiny dostupnosti SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Instance clusteru s podporou převzetí služeb při**selhání: instance clusteru s podporou převzetí služeb při selhání Configuration Manager se nepodporují pro repliku Další informace najdete v tématu [SQL Server vždy na instancích clusteru s podporou převzetí služeb při selhání](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: ve verzi 1902 a starší není podporována použití skupiny dostupnosti s Configuration Manager v konfiguraci s více podsítěmi. Nemůžete také použít připojovací řetězec pro klíčové slovo [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) .

    Pro podporu této konfigurace Configuration Manager aktualizujte na verzi 1906 nebo novější. Další informace najdete v tématu věnovaném [převzetí služeb při selhání s více podsítěmi](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) .

### <a name="sql-servers-that-host-additional-availability-groups"></a>SQL servery, které hostují další skupiny dostupnosti

<!--SCCMDocs issue 649-->
Pokud SQL Server hostuje jednu nebo více skupin dostupnosti kromě skupiny, kterou používáte pro Configuration Manager, potřebuje konkrétní nastavení v době, kdy spustíte Configuration Manager instalaci. Tato nastavení jsou také nutná k instalaci aktualizace pro Configuration Manager. Každá replika v každé skupině dostupnosti musí mít následující konfigurace:

- Ruční převzetí služeb při selhání  
- Povolení všech připojení jen pro čtení  

> [!Note]
> Ve verzi 1902 a starší musíte nakonfigurovat všechny skupiny dostupnosti na SQL Server pro ruční převzetí služeb při selhání. Tato konfigurace je nutná i v případě, že není hostitelem databáze lokality.
>
> Počínaje verzí 1906 podporuje Configuration Manager při nastavení **automatického převzetí služeb při selhání**používat synchronní repliky skupiny dostupnosti. Nastavit **ruční převzetí služeb při selhání** v těchto případech:
>
> - Spuštěním instalačního programu Configuration Manager určíte použití databáze lokality ve skupině dostupnosti.  
> - Nainstalujete jakoukoli aktualizaci Configuration Manager. (Ne jen aktualizace, které se vztahují k databázi lokality).  

### <a name="unsupported-database-use"></a>Nepodporované použití databáze

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager podporuje jenom databázi lokality ve skupině dostupnosti.

Následující databáze nejsou podporovány nástrojem Configuration Manager ve skupině dostupnosti Always On SQL Server:  

- Databáze vytváření sestav  
- Databáze WSUS  

#### <a name="pre-existing-database"></a>Již existující databáze

Nemůžete použít novou databázi vytvořenou v replice. Pokud konfigurujete skupinu dostupnosti, obnovte kopii existující databáze Configuration Manager do primární repliky.  

#### <a name="distributed-views"></a>Distribuovaná zobrazení

<!-- SCCMDocs-pr#3792 -->
Pokud ve verzi 1902 nebo starší zadáte hostitelskou databázi lokality ve skupině dostupnosti Always On SQL Server, nemůžete povolit [distribuovaná zobrazení](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) pro replikaci databáze. Pro podporu této konfigurace aktualizujte na verzi 1906 nebo novější.


### <a name="setup-errors-in-configmgrsetuplog"></a>Chyby instalačního programu v souboru ConfigMgrSetup. log

Když spustíte Configuration Manager instalační program a přesunete databázi lokality do skupiny dostupnosti, pokusí se zpracovat databázové role na sekundárních replikách skupiny dostupnosti. V souboru **ConfigMgrSetup. log** se zobrazuje následující chyba:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Tyto chyby je bezpečné ignorovat.

### <a name="site-expansion"></a>Rozšíření lokality

<!--SCCMDocs issue 568-->
Pokud nakonfigurujete databázi lokality pro samostatnou primární lokalitu, aby používala SQL Always On, nemůžete lokalitu rozšířit, aby zahrnovala lokalitu centrální správy. Pokud tento postup vyzkoušíte, dojde k chybě. Chcete-li lokalitu rozšířit, dočasně odeberte databázi primární lokality ze skupiny dostupnosti.

Při přidávání sekundární lokality není nutné provádět žádné změny v konfiguraci.


## <a name="changes-for-site-backup"></a>Změny pro zálohování lokality

### <a name="backup-database-files"></a>Zálohování souborů databáze
  
Pokud databáze lokality používá skupinu dostupnosti, spusťte úlohu údržby **Zálohovat server webu** , která slouží k zálohování běžných nastavení Configuration Manager a souborů. Nepoužívejte. MDF nebo. Soubory LDF vytvořené touto zálohou Místo toho proveďte přímé zálohování těchto souborů databáze pomocí SQL Server.

### <a name="transaction-log"></a>Transakční protokol  

Nastavte model obnovení databáze lokality na hodnotu **Full**. Tato konfigurace je požadavkem pro Configuration Manager použití ve skupině dostupnosti. Naplánujte monitorování a udržování velikosti protokolu transakcí databáze lokality. V úplném modelu obnovení nejsou transakce zpřísněny, dokud nevytvoří úplnou zálohu databáze nebo protokolu transakcí. Další informace najdete v tématu [zálohování a obnovení databází SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Změny pro Site Recovery

Pokud je alespoň jeden uzel skupiny dostupnosti stále funkční, přeskočte pomocí možnosti Site Recovery **obnovení databáze (tuto možnost použijte v případě, že databáze webového serveru nebyla nijak ovlivněna)**.

Počínaje verzí 1906 může Site Recovery znovu vytvořit databázi na skupině SQL Always On. Tento proces funguje s ručním i automatickým osazením.<!-- SCCMDocs-pr#3846 -->

Pokud ve verzi 1902 nebo starší dojde ke ztrátě všech uzlů skupiny dostupnosti, před obnovením lokality nejprve vytvořte skupinu dostupnosti. Configuration Manager nemůže znovu sestavit nebo obnovit uzel dostupnosti. Znovu vytvořte skupinu, obnovte zálohu a znovu nakonfigurujte SQL. Pak pomocí možnosti Site Recovery **přeskočíte obnovení databáze (tuto možnost použijte, pokud databáze lokality nebyla nijak ovlivněna)**.

Další informace najdete v tématu [zálohování a obnovení](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Změny pro vytváření sestav

### <a name="install-the-reporting-service-point"></a>Instalace bodu služby Reporting Services

Bod služby Reporting Services nepodporuje použití virtuálního názvu naslouchacího procesu skupiny dostupnosti. Nepodporuje také hostování své databáze ve skupině dostupnosti Always On SQL Server.  

- Ve výchozím nastavení instalace bodu služby Reporting Services nastaví **název serveru databáze lokality** na virtuální název, který je zadaný jako naslouchací proces. Změnou tohoto nastavení určíte název počítače a instanci repliky ve skupině dostupnosti.  

- Aby bylo možné přesměrovat generování sestav a zvýšit dostupnost v případě, že je uzel repliky offline, zvažte instalaci dalších bodů služby Reporting Services na každý uzel repliky. Pak nakonfigurujte jednotlivé body služby Reporting Services tak, aby používaly vlastní název počítače. Když nainstalujete bod služby Reporting Service do každé repliky skupiny dostupnosti, může se vytváření sestav vždy připojit k serveru aktivního bodu generování sestav.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Přepínání bodu služby Reporting Services používaného konzolou

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte uzel **sestavy** .

1. Na pásu karet vyberte **Možnosti sestavy**.  

1. V dialogovém okně Možnosti sestavy vyberte bod služby Reporting Services, který chcete použít.  


## <a name="next-steps"></a>Další kroky

Tento článek popisuje požadavky, omezení a změny v běžných úlohách, které Configuration Manager vyžadují při použití skupin dostupnosti. Postupy nastavení a Konfigurace lokality tak, aby používaly skupiny dostupnosti, najdete v tématu [Konfigurace skupin dostupnosti](configure-aoag.md).
