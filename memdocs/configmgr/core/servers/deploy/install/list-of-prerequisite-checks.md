---
title: Kontroly požadovaných součástí
titleSuffix: Configuration Manager
description: Odkaz na konkrétní kontrolu předpokladů pro Configuration Manager aktualizace.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bdf2adbf4ba5f02869ba5058da84ee7738e0ce2
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608067"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Seznam kontrol požadovaných součástí pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek podrobně popisuje kontroly požadovaných součástí, které se spustí při instalaci nebo aktualizaci Configuration Manager. Další informace najdete v tématu [Kontrola požadovaných součástí](prerequisite-checker.md).  



## <a name="errors"></a>Chyby

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapování aktivních migrací na cílové primární lokalitě

*Platí pro: lokalita centrální správy*

Neexistují žádná mapování aktivních migrací k primárním lokalitám.

### <a name="active-replica-mp"></a>MP aktivní repliky

*Platí pro: primární lokalita*

Existuje aktivní replika bodu správy.

### <a name="administrative-rights-on-expand-primary-site"></a>Práva správce v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, uživatelský účet, který spouští instalační program, má práva **správce** na samostatném primárním serveru lokality.

### <a name="administrative-rights-on-site-system"></a>Práva správce v systému lokality

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Uživatelský účet, který spouští instalační program Configuration Manager, má práva **správce** na serveru lokality.

### <a name="administrator-rights-on-central-administration-site"></a>Práva správce na lokalitě centrální správy

*Platí pro: primární lokalita*

Uživatelský účet, který spouští instalační program Configuration Manager, má práva **správce** na serveru lokality centrální správy.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>funkce Asset Intelligence bod synchronizace v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, role bodu synchronizace funkce Asset Intelligence není nainstalovaná na samostatné primární lokalitě.

### <a name="bits-enabled"></a>Služba BITS povolena

*Platí pro: bod správy*

V bodu správy je nainstalována Background Intelligent Transfer Service (BITS). Tato kontroly může selhat z některého z následujících důvodů:

- BITY nejsou nainstalované.  

- Součást kompatibility WMI služby IIS 6,0 pro IIS 7,0 není nainstalovaná na serveru nebo na vzdáleném hostiteli služby IIS.  

- Instalačnímu programu se nepovedlo ověřit Vzdálená nastavení služby IIS. Společné součásti služby IIS nejsou nainstalovány na serveru lokality.  

### <a name="case-insensitive-collation-on-sql-server"></a>Kolace nerozlišující malá a velká písmena u SQL Server

*Platí pro: Server databáze lokality*

Instalace SQL Server používá kolaci nerozlišující malá a velká písmena, jako je například **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Práva správce serveru lokality centrální správy v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, účet počítače serveru lokality centrální správy má práva **správce** na samostatném primárním serveru lokality.

### <a name="client-version-on-management-point-computer"></a>Verze klienta v počítači bodu správy

*Platí pro: bod správy*

Instalujete bod správy na server, který nemá nainstalovanou jinou verzi klienta Configuration Manager.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Brána pro správu cloudu v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, role brány pro správu cloudu není nainstalovaná na samostatné primární lokalitě.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Připojení k SQL Server v lokalitě centrální správy

*Platí pro: primární lokalita*

Uživatelský účet, který spouští Configuration Manager instalaci v primární lokalitě pro připojení k existující hierarchii, má roli **sysadmin** v instanci SQL Server pro lokalitu centrální správy.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>Vlastní nastavení klientského agenta má povolenou architekturu NAP.

*Platí pro: lokalita centrální správy, primární lokalita*

Neexistují žádná vlastní nastavení klienta, která umožňují architekturu NAP (Network Access Protection).

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Bod služby datového skladu v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, role bodu služby datového skladu není nainstalovaná na samostatné primární lokalitě.

### <a name="dedicated-sql-server-instance"></a>Vyhrazená instance SQL Server

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Nakonfigurovali jste vyhrazenou instanci SQL Server pro hostování databáze Configuration Manager lokality.

Pokud instance používá jiný web, je nutné vybrat jinou instanci pro novou lokalitu. Můžete také odinstalovat druhou lokalitu nebo přesunout její databázi do jiné instance systému SQL Server.

### <a name="default-client-agent-settings-have-nap-enabled"></a>Výchozí nastavení klientského agenta má povolenou architekturu NAP.

*Platí pro: lokalita centrální správy, primární lokalita*

Výchozí nastavení klienta nepovoluje architekturu NAP (Network Access Protection).

### <a name="domain-membership-error"></a>Členství v doméně (chyba)

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita, poskytovatel serveru SMS, SQL Server*

Configuration Manager počítač je členem domény systému Windows.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Bod Endpoint Protection v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, role Endpoint Protectionho bodu není nainstalovaná na samostatné primární lokalitě.

### <a name="existing-configuration-manager-server-components-on-server"></a>Existující součásti Configuration Manager serveru na serveru

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Server lokality nebo role systému lokality nejsou již nainstalovány na serveru vybraném pro instalaci lokality.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Existující samostatná primární lokalita pro verzi a kód lokality

*Platí pro: lokalita centrální správy, primární lokalita*

Primární lokalita, kterou plánujete rozšířit, je samostatnou primární lokalitou. Má stejnou verzi Configuration Manager, ale jiný kód lokality než lokalita centrální správy, která se má nainstalovat.

### <a name="firewall-exception-for-sql-server"></a>Výjimka brány firewall pro SQL Server

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita, bod správy*

Brána Windows Firewall je zakázaná nebo pro SQL Server existuje příslušná výjimka brány Windows Firewall.

Povolte vzdálený přístup k Sqlservr.exe nebo k požadovaným portům TCP. Ve výchozím nastavení SQL Server naslouchá na portu TCP 1433 a SQL Server Service Broker (SSB) používá port TCP 4022.

### <a name="free-disk-space-on-site-server"></a>Volné místo na disku na serveru lokality

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Chcete-li nainstalovat webový server, musí mít alespoň 15 GB volného místa na disku. Pokud nainstalujete poskytovatele služby SMS na stejný server, budete potřebovat dalších 1 GB volného místa.

### <a name="iis-service-running"></a>Spuštěná služba IIS

*Platí pro: bod správy, distribuční bod*

Služba IIS je nainstalovaná a spuštěná na serveru pro bod správy nebo distribuční bod.

### <a name="incompatible-collection-references"></a>Nekompatibilní odkazy na kolekce

*Platí pro: lokalita centrální správy*

Během upgradu kolekce odkazují jenom na jiné kolekce stejného typu.

### <a name="match-collation-of-expand-primary-site"></a>Porovnat kolaci rozšířené primární lokality

*Platí pro: lokalita centrální správy*

Když rozšíříte primární lokalitu do hierarchie nástroje, databáze lokality pro samostatnou primární lokalitu má stejnou kolaci jako databáze lokality v lokalitě centrální správy.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Maximální velikost replikace textu pro skupiny dostupnosti Always On SQL Server

*Platí pro: Server databáze lokality*

Pokud používáte SQL Server Always On, nastavení **maximální velikosti textu REPL** musí být správně nakonfigurované. Další informace najdete v tématu [Příprava na používání skupin dostupnosti Always On SQL Server s Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Konektor Microsoft Intune v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozbalíte primární lokalitu do hierarchie, role konektoru Microsoft Intune není nainstalovaná na samostatné primární lokalitě.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Zaregistrovaná knihovna algoritmu RDC (Microsoft Remote Differential Compression)

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Knihovna RDC je zaregistrovaná na Configuration Manager serveru lokality.

### <a name="microsoft-windows-installer"></a>Instalační služba systému Microsoft Windows

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Ověří Instalační služba systému Windows verzi.

Pokud se tato kontrola nezdařila, instalační program nemohl ověřit verzi, nebo nainstalovaná verze nesplňuje minimální požadavek Instalační služba systému Windows 4,5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Minimální verze .NET Framework pro konzolu Configuration Manager

*Platí pro: Configuration Manager konzolu*

V počítači konzoly Configuration Manager je nainstalována aplikace Microsoft .NET Framework 4,0.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Minimální verze .NET Framework pro server lokality Configuration Manager

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Na Configuration Manager serveru lokality je nainstalována nebo povolena .NET Framework 3,5.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Minimální verze .NET Framework pro instalaci edice SQL Server Express pro Configuration Manager sekundární lokalitě

*Platí pro: sekundární lokalita*

.NET Framework 4,0 je nainstalován nebo povolen na Configuration Manager sekundárním serveru lokality. Tuto verzi vyžaduje SQL Server Express.

### <a name="parent-database-collation"></a>Kolace nadřazené databáze

*Platí pro: primární lokalita, sekundární lokalita*

Kolace databáze lokality odpovídá kolaci databáze nadřazené lokality. Všechny lokality v hierarchii musí používat stejnou kolaci databáze.

### <a name="parent-site-replication-status"></a>Stav replikace nadřazené lokality

*Platí pro: lokalita centrální správy, primární lokalita*

Stav replikace nadřazené lokality je **replikace aktivní** (stav **125**).

### <a name="pending-system-restart"></a>Čeká se na restart systému.

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Před spuštěním instalačního programu vyžaduje jiný program restartování serveru.

Od verze 1810 je tato kontrolu pružnější. Pokud chcete zjistit, jestli je počítač ve stavu čekání na restartování, zkontroluje následující umístění registru:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>Primární plně kvalifikovaný název domény

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita, Server databáze lokality*

Název NetBIOS počítače se shoduje s názvem místního hostitele v plně kvalifikovaném názvu domény (FQDN).

### <a name="read-only-domain-controller"></a>Řadič domény jen pro čtení

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Servery databáze lokality a servery sekundární lokality nejsou podporované na řadiči domény jen pro čtení (RODC).

Další informace najdete v podpora Microsoftu článku o [problémech při instalaci SQL Server na řadič domény](https://support.microsoft.com/help/2032911).

### <a name="required-sql-server-collation"></a>Požadovaná kolace SQL Server

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Instance pro SQL Server je nakonfigurovaná tak, aby používala **SQL_Latin1_General_CP1_CI_AS** kolaci.

Je-li již databáze lokality Configuration Manager nainstalována, tato tato tato zaškrtávací políčka platí také pro databázi. Informace o změně instance SQL Server a kolace databáze najdete v tématu [věnovaném řazení SQL a podpoře kódování Unicode](/sql/relational-databases/collations/collation-and-unicode-support).

Pokud používáte čínský operační systém a požadujete podporu GB18030, tato kontroler se nepoužije. Další informace o povolení podpory GB18030 najdete v tématu [mezinárodní podpora](../../../plan-design/hierarchy/international-support.md).

### <a name="server-service-is-running"></a>Služba serveru je spuštěná.

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Služba serveru je spuštěná a spuštěná.

### <a name="setup-source-folder"></a>Složka zdroje instalace

*Platí pro: sekundární lokalita*

Účet počítače pro sekundární lokalitu má následující oprávnění ke zdrojové složce nastavení a ke sdílení:

- **Číst** Oprávnění systému souborů NTFS  

- **Číst** oprávnění ke sdílení  

> [!Note]  
> Pokud používáte sdílené složky pro správu, například C $ a D $, účet počítače sekundární lokality musí být **správce** na serveru.  

### <a name="setup-source-version"></a>Verze zdroje instalace

*Platí pro: sekundární lokalita*

Verze Configuration Manager v zadané zdrojové složce pro instalaci sekundární lokality se shoduje s verzí Configuration Manager primární lokality.

### <a name="site-code-in-use"></a>Používaný kód lokality

*Platí pro: primární lokalita*

Zadaný kód lokality se už v hierarchii Configuration Manager nepoužívá. Zadejte jedinečný kód lokality pro tento web.

### <a name="site-server-computer-account-administrative-rights"></a>Práva správce účtu počítače serveru lokality

*Platí pro: primární lokalita, Server databáze lokality*

Účet počítače serveru lokality má práva **správce** na serveru SQL Server a bodu správy.

### <a name="site-server-fqdn-length"></a>Délka plně kvalifikovaného názvu domény serveru lokality

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Délka plně kvalifikovaného názvu domény serveru lokality.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Server lokality v pasivním režimu v rozšířené primární lokalitě

*Platí pro: lokalita centrální správy*

Když rozšíříte primární lokalitu na hierarchii, server lokality v pasivním režimu není nainstalován v samostatné primární lokalitě.

### <a name="sms-provider-in-same-domain-as-site-server"></a>Poskytovatel serveru SMS ve stejné doméně jako server lokality

*Platí pro: poskytovatel serveru SMS*

Libovolná instance poskytovatele služby SMS je ve stejné doméně jako server lokality.

### <a name="software-update-point-in-nlb-configuration"></a>Bod aktualizace softwaru v konfiguraci NLB

*Platí pro: bod aktualizace softwaru*

Web nepoužívá vyrovnávání zatížení sítě (NLB) se všemi virtuálními umístěními pro aktivní body aktualizace softwaru.

### <a name="software-update-point-using-a-load-balancer"></a>Bod aktualizace softwaru s použitím nástroje pro vyrovnávání zatížení

*Platí pro: bod aktualizace softwaru*

Configuration Manager nepodporuje body aktualizace softwaru v síti (NLB) nebo nástrojích pro vyrovnávání zatížení hardwaru (HLB).

### <a name="sql-server-always-on-availability-groups"></a>Skupiny dostupnosti AlwaysOn pro SQL Server

*Platí pro: Server databáze lokality*

Pokud používáte SQL Server Always On, musí splňovat minimální požadavky na hostování skupiny dostupnosti. Další informace najdete v tématu [Příprava na používání skupin dostupnosti Always On SQL Server s Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>Skupina dostupnosti SQL Server nakonfigurovaná pro čtení sekundárních souborů

*Platí pro: Server databáze lokality*

Pokud používáte SQL Server Always On, Projděte si sekundární stav čtení replik skupin dostupnosti.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>Skupina dostupnosti SQL Server nakonfigurovaná pro manuální převzetí služeb při selhání

*Platí pro: Server databáze lokality*

Při použití SQL Server Always On jsou repliky skupin dostupnosti nakonfigurované na ruční převzetí služeb při selhání.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>SQL Server replik skupin dostupnosti ve výchozí instanci

*Platí pro: Server databáze lokality*

Při použití SQL Server Always On jsou repliky skupin dostupnosti na výchozí instanci.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>Všechny repliky skupin dostupnosti SQL musejí mít stejný režim osazení.

<!-- SCCMDocs-pr#3899 -->
*Platí pro: Server databáze lokality*

Počínaje verzí 1906 je při používání SQL Server Always On potřeba nakonfigurovat repliky skupin dostupnosti se stejným [režimem osazení](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).

### <a name="sql-availability-group-replicas-must-be-healthy"></a>Repliky skupin dostupnosti SQL musí být v pořádku.

<!-- SCCMDocs-pr#3899 -->
*Platí pro: Server databáze lokality*

Počínaje verzí 1906 platí, že při použití SQL Server Always On jsou repliky skupin dostupnosti v dobrém stavu.

### <a name="sql-server-configuration-for-site-upgrade"></a>Konfigurace SQL Server pro upgrade webu

*Platí pro: Server databáze lokality*

SQL Server splňuje minimální požadavky pro upgrade lokality. Další informace najdete v tématu [podporované verze SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>Edice SQL Serveru

*Platí pro: Server databáze lokality*

SQL Server v lokalitě není SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express v sekundární lokalitě

*Platí pro: sekundární lokalita*

SQL Server Express lze úspěšně nainstalovat na server sekundární lokality.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server na serveru sekundární lokality

*Platí pro: sekundární lokalita*

SQL Server je nainstalován na sekundárním serveru lokality. Nemůžete nainstalovat SQL Server do vzdáleného systému lokality pro sekundární lokalitu.

> [!Warning]  
> Tato kontroler se použije jenom v případě, že se rozhodnete, že instalační program použije existující instanci SQL Server.  

### <a name="sql-server-service-running-account"></a>Účet běžící služby SQL Server

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Přihlašovací účet pro službu SQL Server není místní uživatelský účet nebo **místní služba**.

Nakonfigurujte službu SQL Server tak, aby používala platný účet domény, **síťovou službu**nebo **místní systém**.

### <a name="sql-server-site-database-consistency"></a>SQL Server konzistence databáze webu

*Platí pro: Server databáze lokality*

Ověřte konzistenci databáze.

### <a name="sql-server-sysadmin-rights"></a>SQL Server oprávnění sysadmin

*Platí pro: Server databáze lokality*

Uživatelský účet, který spouští instalační program Configuration Manager, má roli **sysadmin** na instanci SQL Server, kterou jste vybrali pro instalaci databáze lokality. Tato kontrola se také nezdařila, pokud instalační program nemůže získat přístup k instanci SQL Server k ověření oprávnění.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>SQL Server oprávnění sysadmin pro referenční lokalitu

*Platí pro: Server databáze lokality*

Uživatelský účet, který spouští instalační program Configuration Manager, má roli **sysadmin** na instanci role SQL Server, kterou jste vybrali jako databázi referenční lokality. Pro úpravu databáze lokality jsou vyžadována oprávnění SQL Server role **sysadmin** .

### <a name="sql-server-tcp-port"></a>Port SQL Server TCP

*Platí pro: Server databáze lokality*

Protokol TCP je povolen pro instanci SQL Server a je nastaven na použití statického portu.

### <a name="sql-server-version"></a>Verze SQL Serveru

*Platí pro: Server databáze lokality*

Na zadaném databázovém serveru lokality je nainstalovaná podporovaná verze SQL Server.

Další informace najdete v tématu [podpora verzí SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="unsupported-os-for-configuration-manager-console"></a>Nepodporovaný operační systém pro konzolu Configuration Manager

*Platí pro: Configuration Manager konzolu*

Nainstalujte konzolu Configuration Manager na počítačích, na kterých běží podporovaná verze operačního systému.

Další informace najdete v tématu [podporované verze operačních systémů pro konzolu Configuration Manager](../../../plan-design/configs/supported-operating-systems-consoles.md).

### <a name="unsupported-os-for-site-server"></a>Nepodporovaný operační systém pro server lokality

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita, Configuration Manager konzola, bod správy, distribuční bod*

Server používá podporovanou verzi operačního systému.

Další informace najdete v tématu [podporované verze operačních systémů pro servery systému lokality Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Nepodporovaná role systému lokality: bod obsluhy vzdálené správy

*Platí pro: primární lokalita*

Role systému lokality bodu služby mimo IP síť není nainstalovaná.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Nepodporovaná role systému lokality: bod ověření stavu systému

*Platí pro: primární lokalita*

Role systému lokality bodu ověření stavu systému není nainstalována.

### <a name="unsupported-upgrade-path"></a>Nepodporovaná cesta upgradu

*Platí pro: lokalita centrální správy, primární lokalita*

Všechny servery lokalit v hierarchii splňují Configuration Manager minimální verzi, která je nutná pro upgrade.

### <a name="usmt-installed"></a>Nástroj USMT nainstalován

*Platí pro: lokalita centrální správy, primární lokalita (jenom samostatně)*

Je nainstalována součást Nástroj pro migraci uživatelských souborů a nastavení (USMT) sady Windows Assessment and Deployment Kit (ADK) pro systém Windows.

### <a name="validate-fqdn-of-sql-server"></a>Ověřit plně kvalifikovaný název domény SQL Server

*Platí pro: Server databáze lokality*

Zadali jste platný plně kvalifikovaný název domény pro SQL Server počítač.

### <a name="verify-central-administration-site-version"></a>Ověření verze lokality centrální správy

*Platí pro: primární lokalita*

Lokalita centrální správy má stejnou verzi Configuration Manager.

### <a name="verify-database-consistency"></a>Ověření konzistence databáze

*Platí pro: lokalita centrální správy, primární lokalita*

Ověřuje konzistenci databáze lokality v SQL Server.  

### <a name="windows-deployment-tools-installed"></a>Nainstalované nástroje pro nasazení systému Windows

*Platí pro: poskytovatel serveru SMS*

Je nainstalovaná součást nástrojů pro nasazení systému Windows v systému Windows ADK.

### <a name="windows-failover-cluster"></a>Služba Windows Failover Cluster

*Platí pro: Server lokality, bod správy, distribuční bod*

Server se serverem lokality, bodem správy nebo rolemi distribučních bodů nejsou součástí clusteru Windows.

Počínaje verzí 1810 nebude proces instalace Configuration Manager nadále blokovat instalaci role serveru lokality do počítače s rolí systému Windows pro clustering s podporou převzetí služeb při selhání. SQL Always On vyžaduje tuto roli, takže dříve se nepovedlo společně najít databázi lokality na serveru lokality. Díky této změně můžete vytvořit vysoce dostupnou lokalitu s menším počtem serverů pomocí SQL Always On a serveru lokality v pasivním režimu. Další informace najdete v tématu [Možnosti vysoké dostupnosti](../configure/high-availability-options.md). <!--1359132-->  

### <a name="windows-pe-installed"></a>Prostředí Windows PE nainstalováno

*Platí pro: poskytovatel serveru SMS*

Je nainstalovaná komponenta Windows Preinstallation Environment (PE) systému Windows ADK.



## <a name="warnings"></a>Upozornění

### <a name="active-directory-domain-functional-level"></a>Funkční úroveň domény služby Active Directory

*Platí pro: lokalita centrální správy, primární lokalita*

Úroveň funkčnosti domény a doménové struktury služby Active Directory je minimálně Windows Server 2008 R2. Další informace najdete v tématu [Podpora domén služby Active Directory](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Práva správce na distribučním bodu

*Platí pro: distribuční bod*

Uživatelský účet, který spouští instalační program, má v distribučním bodě práva **správce** .

### <a name="administrative-rights-on-management-point"></a>Práva správce v bodu správy

*Platí pro: bod správy, distribuční bod*

Účet počítače serveru lokality má práva **správce** pro bod správy a distribuční bod.

### <a name="administrative-share-site-system"></a>Sdílená složka pro správu (systém lokality)

*Platí pro: bod správy*

Požadované sdílené složky pro správu jsou k dispozici na počítači systému lokality.

### <a name="application-compatibility"></a>Kompatibilita aplikací

*Platí pro: lokalita centrální správy, primární lokalita*

Aktuální aplikace jsou kompatibilní se schématem aplikace.

### <a name="backlogged-inboxes"></a>Nevyřízené složky Doručená pošta

*Platí pro: lokalita centrální správy, primární lokalita*

Server lokality včas zpracovává kritické složky Doručená pošta. Složky Doručená pošta neobsahují soubory starší než jeden den.

Zkontroluje následující složky doručené pošty:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Chcete-li toto upozornění vyřešit, ověřte, zda jsou spuštěny součásti systému lokality nástroje pro vyřazování a Plánovač.

### <a name="bits-installed"></a>Služba BITS nainstalována

*Platí pro: bod správy*

Ve službě IIS je nainstalovaná a povolená Background Intelligent Transfer Service (BITS).

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Ověřte, jestli lokalita používá Upgrade Readiness konektor cloudové služby.

*Platí pro: lokalita centrální správy, primární lokalita*

Služba Upgrade Readiness je vyřazena od 31. ledna 2020. Další informace najdete v [článku KB 4521815: vyřazení služby Windows Analytics na 31. ledna 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Desktop Analytics je vývoj Windows Analytics. Další informace najdete v tématu [co je Desktop Analytics](../../../../desktop-analytics/overview.md).

Pokud má váš Configuration Manager web připojení k Upgrade Readiness, je nutné jej odebrat a znovu nakonfigurovat klienty. Další informace najdete v tématu [odebrání upgrade Readinessho připojení](../../../clients/manage/upgrade-readiness.md#bkmk_remove).

Pokud toto upozornění na požadavky přeskočíte, Configuration Manager instalační program automaticky odebere konektor Upgrade Readiness.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Brána pro správu cloudu vyžaduje buď ověřování na základě tokenu, nebo bod správy HTTPS.

*Platí pro: Brána pro správu cloudu*

U některých verzí Configuration Manager nemůžete použít bod správy HTTP s bránou pro správu cloudu (CMG). Buď nakonfigurujte CMG pro protokol HTTPS, nebo nakonfigurujte lokalitu pro rozšířený protokol HTTP. Další informace najdete v tématu [Plánování brány pro správu cloudu](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>Konfigurace pro využití SQL Server paměti

*Platí pro: Server databáze lokality*

SQL Server je nakonfigurovaný pro neomezené využití paměti. Nakonfigurujte SQL Server paměti tak, aby měla maximální limit.

### <a name="distribution-point-package-version"></a>Verze balíčku distribučního bodu

*Platí pro: distribuční body*

Všechny distribuční body v lokalitě mají nejnovější verzi balíčků distribuce softwaru.

### <a name="domain-membership-warning"></a>Členství v doméně (upozornění)

*Platí pro: bod správy, distribuční bod*

Configuration Manager počítač je členem domény systému Windows.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Výjimka brány firewall pro SQL Server (samostatná primární lokalita)

*Platí pro: primární lokalita (jenom samostatně)*

Brána Windows Firewall je zakázaná nebo pro SQL Server existuje příslušná výjimka brány Windows Firewall.

Povolte vzdálený přístup k Sqlservr.exe nebo k požadovaným portům TCP. Ve výchozím nastavení SQL Server naslouchá na portu TCP 1433 a Server Service Broker (SSB) používá port TCP 4022.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Výjimka brány firewall pro SQL Server pro bod správy

*Platí pro: bod správy*

Brána Windows Firewall je zakázaná nebo pro SQL Server existuje příslušná výjimka brány Windows Firewall.

### <a name="iis-https-configuration"></a>Konfigurace protokolu HTTPS služby IIS

*Platí pro: bod správy, distribuční bod*

Web služby IIS obsahuje vazby pro komunikační protokol HTTPS.

Při instalaci rolí lokality, které vyžadují protokol HTTPS, nakonfigurujte vazby webu IIS na určeném serveru s platným certifikátem infrastruktury veřejných klíčů (PKI).

### <a name="invalid-discovery-records"></a>Neplatné záznamy zjišťování

*Platí pro: lokalita centrální správy*

Existují záznamy zjišťování, které již nejsou platné. Tyto záznamy budou označeny pro odstranění.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6,0 (MSXML60)

*Platí pro lokalitu centrální správy, primární lokalitu, sekundární lokalitu, Configuration Manager konzolu, bod správy, distribuční bod*

Ověřuje, že je nainstalovaná služba MSXML 6,0 nebo novější verze.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>Architektura NAP (Network Access Protection) už není podporovaná.

*Platí pro: primární lokalita*

Nejsou k dispozici žádné aktualizace softwaru pro architekturu NAP.

### <a name="ntfs-drive-on-site-server"></a>Jednotka NTFS na serveru lokality

*Platí pro: primární lokalita*

Disková jednotka je naformátovaná pomocí systému souborů NTFS. Pro lepší zabezpečení nainstalujte součásti serveru lokality na diskové jednotky naformátované pomocí systému souborů NTFS.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> Čeká se na aktualizace zásad položky konfigurace

<!--SCCMDocs-pr issue 2814-->

*Platí pro: primární lokalita*

Pokud při aktualizaci z verze 1706 nebo novější používáte verzi 1806, může se toto upozornění zobrazit v případě, že máte spoustu nasazení aplikací a nejméně jeden z nich vyžaduje schválení.

Máte dvě možnosti:  

- Ignorujte upozornění a pokračujte v aktualizaci. Tato akce způsobí, že při zpracovávání zásad dojde v průběhu aktualizace k rychlejšímu zpracování na serveru lokality. Po aktualizaci můžete zobrazit také další zatížení procesoru v bodu správy.  

- Revidujte jednu z aplikací, které nemají žádné požadavky, nebo konkrétní požadavek na operační systém. Předem zpracujte některá zatížení na serveru lokality v daném čase. Zkontrolujte **Objreplmgr. log**a pak monitorujte procesor v bodu správy. Po dokončení zpracování aktualizujte lokalitu. Po aktualizaci bude stále existovat další zpracování, ale menší než při ignorování upozornění s první možností.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Čeká se na restartování systému na vzdáleném SQL Server

*Platí pro: verze 1902 a novější, vzdálené SQL Server*

Před spuštěním instalačního programu vyžaduje jiný program restartování serveru.

Pokud chcete zjistit, jestli je počítač ve stavu čekání na restartování, zkontroluje následující umístění registru:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2,0 na serveru lokality

*Platí pro: primární lokalita s konektorem Exchange*

Na serveru lokality pro Configuration Manager Exchange Connector je nainstalovaná verze Windows PowerShell 2,0 nebo novější.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Vzdálené připojení k rozhraní WMI v sekundární lokalitě

*Platí pro: sekundární lokalita*

Instalační program může navázat vzdálené připojení ke službě WMI na serveru sekundární lokality.

### <a name="schema-extensions"></a>Rozšíření schématu

*Platí pro: lokalita centrální správy, primární lokalita*

Schéma služby Active Directory bylo rozšířeno. Pokud je rozšířená, verze rozšíření schématu, které se použily.

Configuration Manager nevyžaduje rozšíření schématu služby Active Directory pro instalaci serveru lokality. Společnost Microsoft je doporučuje, aby plně používala všechny funkce Configuration Manager. Další informace o výhodách rozšíření schématu najdete v tématu [Příprava služby Active Directory pro publikování lokality](../../../plan-design/network/extend-the-active-directory-schema.md).

### <a name="share-name-in-package"></a>Název sdílené složky v balíčku

*Platí pro: lokalita centrální správy, primární lokalita*

Balíčky nemají v názvu sdílené složky neplatné znaky, třeba `#` .

### <a name="site-system-to-sql-server-communication"></a>Komunikace mezi systémem lokality a SQL Server

*Platí pro: sekundární lokalita, bod správy*

Účet, který jste nakonfigurovali ke spuštění služby SQL Server pro instanci databáze lokality, má v Active Directory Domain Services platný hlavní název služby (SPN). Zaregistrujte platný hlavní název služby (SPN) ve službě Active Directory pro podporu ověřování Kerberos.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> Vyčištění sledování změn SQL Server

*Platí pro: Server databáze lokality*

Počínaje verzí 1810 ověřte, zda má databáze lokality nevyřízené položky dat sledování změn SQL.<!--SCCMDocs-pr issue 3023-->  

Tuto kontrolu ověřte ručně spuštěním diagnostické uložené procedury v databázi lokality. Nejdřív vytvořte [diagnostické připojení](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators) k vaší databázi lokality. Nejjednodušším způsobem je použít Editor dotazů databázového stroje SQL Server Management Studio a připojit se k `admin:<instance name>` .

V okně dotazu na vyhrazené připojení správce spusťte následující příkazy:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

V závislosti na velikosti databáze a velikosti backlogu může tato uložená procedura běžet za několik minut nebo několik hodin. Po dokončení dotazu se zobrazí dvě části dat, které souvisejí s nevyřízenými položkami. Nejprve se podíváte na **CT_Days_Old**. Tato hodnota oznamuje stáří (dny) nejstarší položky v tabulce syscommittab. Mělo by to být pět dnů, což je Configuration Manager výchozí hodnota. Tuto výchozí hodnotu neměňte. V době náročného zpracování dat nebo replikace může být nejstarší položka v syscommittab víc než pět dní. Pokud je tato hodnota nad sedm dní, spusťte ruční vyčištění dat sledování změn.  

Chcete-li vyčistit data sledování změn, spusťte v rámci vyhrazeného připojení pro správu následující příkaz:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Tento příkaz spustí vyčištění syscommittab a všech přidružených tabulek na straně. Může běžet během několika minut nebo několik hodin. Chcete-li monitorovat jeho průběh, dotazování **na zobrazení seznamu** . Chcete-li zobrazit aktuální průběh, spusťte následující dotaz:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>Nativní klient systému SQL Server

<!--SCCMDocs-pr issue 3094-->

Když nainstalujete novou lokalitu, Configuration Manager automaticky nainstaluje SQL Server Native Client jako Distribuovatelný komponentu. Po instalaci lokality Configuration Manager neupgraduje SQL Server Native Client. Aktualizace SQL Server Native Client může vyžadovat restart, což může mít vliv na proces instalace lokality.

Tato kontrolu zajistí, že webový server má podporovanou verzi SQL Native Client. Kontrola požadovaných součástí neověřuje verzi SQL Native Client ve vzdálených systémech lokality.

Minimální verze je SQL 2012 SP4 ( `11.*.7001.0` ). Tato SQL Native Client verze podporuje TLS 1,2. Další informace najdete v následujících článcích:

- [Podpora TLS 1,2 pro Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Jak povolit TLS 1,2 pro Configuration Manager](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager používá SQL Server Native Client na následujících rolích systému lokality:<!-- SCCMDocs issue 1150 -->

- Server databáze lokality
- Server lokality: lokalita centrální správy, primární lokalita nebo sekundární lokalita
- Bod správy
- Bod správy zařízení
- Bod migrace stavu
- poskytovatele serveru SMS
- Bod aktualizace softwaru
- Distribuční bod s povoleným vícesměrovým vysíláním
- Servisní bod aktualizace služby funkce Asset Intelligence
- Bod služby Reporting services
- Webová služba Application Catalog
- Bod registrace
- Bod ochrany koncového bodu Endpoint Protection
- Spojovací bod služby
- Bod registrace certifikátu
- Bod služby datového skladu

### <a name="sql-server-process-memory-allocation"></a>Přidělení paměti procesu SQL Server

*Platí pro: Server databáze lokality*

SQL Server rezervuje minimálně 8 GB paměti pro lokalitu centrální správy a primární lokalitu a minimálně 4 GB paměti pro sekundární lokalitu.

Další informace najdete v tématu [Konfigurace možností paměti pomocí SQL Server Management Studio](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Tato kontroly není platná pro SQL Server Express v sekundární lokalitě. Tato edice je omezená na 1 GB rezervované paměti.  

### <a name="sql-server-security-mode"></a>Režim zabezpečení SQL Server

*Platí pro: Server databáze lokality*

SQL Server je nakonfigurován pro zabezpečení ověřování systému Windows.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Nepodporovaná verze operačního systému serveru pro upgrade

*Platí pro: primární lokalita, sekundární lokalita*

Role systému lokality kromě distribučních bodů jsou nainstalovány na serverech se systémem Windows Server 2012 nebo novějším.

Další informace najdete v tématu [podporované operační systémy pro Configuration Manager servery systému lokality](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

> [!NOTE]  
> Tato kontrolu nedokáže vyřešit stav rolí systému lokality nainstalovaných v Azure nebo cloudového úložiště, které používá Microsoft Intune. Ignorovat upozornění pro tyto role jako falešně pozitivních hodnot.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Upgrade Assessment Toolkit není podporován.

*Platí pro: lokalita centrální správy, primární lokalita*

Sada nástrojů pro vyhodnocení upgradu není nainstalovaná. Další informace najdete v tématu [odebrané a zastaralé funkce](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Ověření oprávnění serveru lokality pro publikování ve službě Active Directory

*Platí pro: lokalita centrální správy, primární lokalita, sekundární lokalita*

Účet počítače pro server lokality má oprávnění **Úplné řízení** ke kontejneru **System Management** v doméně služby Active Directory.

Další informace najdete v tématu [Příprava služby Active Directory pro publikování lokality](../../../plan-design/network/extend-the-active-directory-schema.md).

> [!NOTE]  
> Pokud oprávnění ověříte ručně, můžete toto upozornění ignorovat.

### <a name="windows-remote-management-winrm-v11"></a>Vzdálená správa systému Windows (WinRM) v 1.1

*Platí pro: primární lokalita, Configuration Manager konzolu*

WinRM 1,1 je nainstalovaná na serveru primární lokality nebo na počítači konzoly Configuration Manager ke spuštění konzoly pro vzdálenou správu.

Služba WinRM je automaticky nainstalována se všemi aktuálně podporovanými verzemi systému Windows. Další informace najdete v tématu [instalace a konfigurace pro vzdálená správa systému Windows](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>Služba WSUS na serveru lokality

*Platí pro: lokalita centrální správy, primární lokalita*

Na serveru lokality je nainstalovaná podporovaná verze služby Windows Server Update Services (WSUS).

Použijete-li bod aktualizace softwaru na jiném serveru, než je server lokality, je nutné nainstalovat konzolu pro správu služby WSUS na server lokality. Další informace o službě WSUS najdete v tématu [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).