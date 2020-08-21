---
title: Upgrade místní infrastruktury
titleSuffix: Configuration Manager
description: Naučte se, jak upgradovat infrastrukturu, jako je SQL Server a operační systém systémů lokality.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7efc775199a34a66a8cd4a83b85baccd4a3ab5cb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699479"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Upgrade místní infrastruktury, která podporuje Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku vám pomůžou při upgradu infrastruktury serveru, která běží Configuration Manager.  

- Pokud chcete *upgradovat* ze starší verze nástroje na Configuration Manager aktuální větev, přečtěte si téma [upgrade na Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Pokud chcete *aktualizovat* Configuration Manager, aktuální větev, infrastrukturu na novou verzi, přečtěte si téma [aktualizace pro Configuration Manager](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Upgrade operačního systému systémů lokality  

Configuration Manager podporuje místní upgrade serverového operačního systému, který je hostitelem serveru lokality a jakékoli role systému lokality, v následujících situacích:  

- Pokud Configuration Manager nadále podporuje výslednou úroveň aktualizace Service Pack systému Windows, podporuje místní upgrade na novější aktualizaci Service Pack systému Windows Server.  

- Místní upgrade z:  

    - Windows Server 2016 na Windows Server 2019  

    - Windows Server 2012 R2 na Windows Server 2019  

    - Windows Server 2012 R2 na Windows Server 2016  

    - Windows Server 2012 na Windows Server 2016  

    - Windows Server 2012 na Windows Server 2012 R2  

    - Windows Server 2008 R2 na Windows Server 2012 R2  

K upgradu serveru použijte postupy upgradu poskytované operačním systémem, na který provádíte upgrade. Viz následující články:  

- [Centrum upgradu Windows serveru](https://aka.ms/upgradecenter)  

- [Upgrade a možnosti převodu pro Windows Server 2016](/windows-server/get-started/supported-upgrade-paths)  

- [Možnosti upgradu pro Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Upgrade na Windows Server 2016 nebo 2019

Kroky v této části použijte pro některý z následujících scénářů upgradu:  

- Upgrade systému Windows Server 2012 R2 nebo Windows Server 2016 na Windows Server 2019  

- Upgrade systému Windows Server 2012 nebo Windows Server 2012 R2 na Windows Server 2016  

#### <a name="before-upgrade"></a>Před upgradem

- (Windows Server 2012 nebo Windows Server 2012 R2): Odeberte klienta System Center Endpoint Protection (SCEP). Windows Server má teď integrovaný program Windows Defender, který nahrazuje klienta SCEP. Přítomnost klienta SCEP může znemožnit upgrade na Windows Server.  

- Odeberte roli WSUS ze serveru, pokud je nainstalována. Po přeinstalování služby WSUS můžete SUSDB zachovat a znovu připojit.  

- Provádíte-li upgrade operačního systému serveru lokality, zajistěte, aby byla [replikace na základě souborů](../../plan-design/hierarchy/file-based-replication.md) v dobrém stavu pro danou lokalitu. Zaškrtněte všechna Doručená místa u nevyřízených položek při odesílání i přijímání lokalit. Pokud je k dispozici hodně zablokovaných nebo čekajících úloh replikace, počkejte, než vymažete.<!-- SCCMDocs#1792 -->
    - V odesílajícím webu zkontrolujte **odesílatel. log**.
    - Na přijímajícím webu zkontrolujte protokol vyřazení z **fronty**.

#### <a name="after-upgrade"></a>Po upgradu

- Ujistěte se, že je program Windows Defender povolený, nastavený pro automatické spouštění a spouštění.  

- Ujistěte se, že jsou spuštěné tyto služby Configuration Manager:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Ujistěte se, že je povolená **Aktivační služba procesů systému Windows** a služba **www/W3SVC** a zda jsou nastaveny pro automatické spouštění. Proces upgradu tyto služby zakáže, takže se ujistěte, že jsou spuštěné pro následující role systému lokality:  

    - Server lokality  

    - Bod správy  

    - Bod služeb webu Katalog aplikací  

    - Bod webu Katalog aplikací  

- Ujistěte se, že každý server, který je hostitelem role systému lokality, nadále splňuje všechny [požadavky](../../plan-design/configs/site-and-site-system-prerequisites.md). Například může být nutné přeinstalovat službu BITS, WSUS nebo nakonfigurovat konkrétní nastavení služby IIS.  

- Po obnovení chybějících nezbytných součástí restartujte server ještě jednou, abyste se ujistili, že jsou služby spuštěné a funkční.  

- Pokud upgradujete server primární lokality, potom [Spusťte resetování lokality](modify-your-infrastructure.md#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Známý problém pro konzoly pro vzdálenou Configuration Manager

Po upgradu serveru lokality nebo instance poskytovatele serveru SMS se nemůžete připojit pomocí konzoly Configuration Manager. Pokud chcete tento problém obejít, ručně obnovte oprávnění skupiny **Admins služby SMS** ve službě WMI. Na serveru lokality musí být nastavena oprávnění a na každém vzdáleném serveru, který je hostitelem instance poskytovatele serveru SMS:

1. Na příslušných serverech otevřete konzolu Microsoft Management Console (MMC) a přidejte modul snap-in pro  **řízení služby WMI**a pak vyberte možnost **místní počítač**.  

2. V konzole MMC otevřete **vlastnosti** **řízení služby WMI (místní)** a vyberte kartu **zabezpečení** .  

3. Rozbalte stromovou strukturu pod kořenem, vyberte uzel **SMS** a pak zvolte **zabezpečení**.  Ujistěte se, že má skupina **Admins služby SMS** následující oprávnění:  

    - Povolit účet  

    - Vzdálené povolení  

4. Na **kartě zabezpečení** pod uzlem **SMS** vyberte uzel **site_ &lt; SiteCode**> a pak zvolte **zabezpečení**. Ujistěte se, že má skupina **Admins služby SMS** následující oprávnění:  

    - Spustit metody  

    - Zápis zprostředkovatele  

    - Povolit účet  

    - Vzdálené povolení  

5. Uložte oprávnění k obnovení přístupu pro konzolu Configuration Manager.  

#### <a name="known-issue-for-remote-site-systems"></a>Známý problém pro systémy vzdálené lokality

Po upgradu serveru, který je hostitelem role systému lokality, může tato hodnota `Software\Microsoft\SMS` chybět v následujícím klíči registru: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Pokud tato hodnota chybí po upgradu Windows na serveru, přidejte ji ručně. V opačném případě role systému lokality mohou mít problémy při nahrávání souborů do složky Doručená pošta na serveru lokality.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Upgrade na Windows Server 2012 R2

Při upgradu z Windows serveru 2008 R2 nebo Windows Serveru 2012 na Windows Server 2012 R2 platí následující podmínky:

#### <a name="before-upgrade"></a>Před upgradem

- V systému Windows Server 2012: Odeberte roli WSUS ze serveru, pokud je nainstalována. Po přeinstalování služby WSUS můžete SUSDB zachovat a znovu připojit.  

- V systému Windows Server 2008 R2: před provedením upgradu na systém Windows Server 2012 R2 je třeba odinstalovat službu WSUS 3,2 ze serveru aplikace. Po přeinstalování služby WSUS můžete SUSDB zachovat a znovu připojit. Další informace najdete v tématu [přehled Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- Provádíte-li upgrade operačního systému serveru lokality, zajistěte, aby byla [replikace na základě souborů](../../plan-design/hierarchy/file-based-replication.md) v dobrém stavu pro danou lokalitu. Zaškrtněte všechna Doručená místa u nevyřízených položek při odesílání i přijímání lokalit. Pokud je k dispozici hodně zablokovaných nebo čekajících úloh replikace, počkejte, než vymažete.<!-- SCCMDocs#1792 -->
    - V odesílajícím webu zkontrolujte **odesílatel. log**.
    - Na přijímajícím webu zkontrolujte protokol vyřazení z **fronty**.

#### <a name="after-upgrade"></a>Po upgradu

- Proces upgradu zakáže službu pro nasazení systému Windows. Zajistěte, aby byla tato služba spuštěná a spuštěná v následujících rolích systému lokality:  

    - Server lokality  

    - Bod správy  

    - Bod služeb webu Katalog aplikací  

    - Bod webu Katalog aplikací  

- Ujistěte se, že je povolená **Aktivační služba procesů systému Windows** a služba **www/W3SVC** a zda jsou nastaveny pro automatické spouštění. Proces upgradu tyto služby zakáže, takže se ujistěte, že jsou spuštěné pro následující role systému lokality:  

    - Server lokality  

    - Bod správy  

    - Bod služeb webu Katalog aplikací  

    - Bod webu Katalog aplikací  

- Ujistěte se, že každý server, který je hostitelem role systému lokality, nadále splňuje všechny [požadavky](../../plan-design/configs/site-and-site-system-prerequisites.md). Například může být nutné přeinstalovat službu BITS, WSUS nebo nakonfigurovat konkrétní nastavení služby IIS.  

    Po obnovení chybějících nezbytných součástí restartujte server ještě jednou, abyste se ujistili, že jsou služby spuštěné a funkční.  

### <a name="unsupported-upgrade-scenarios"></a>Nepodporované scénáře upgradu

Následující scénáře upgradu systému Windows Server se často týkají, ale nepodporují je Configuration Manager:  

- Windows Server 2008 na Windows Server 2012 nebo novější  

- Windows Server 2008 R2 na Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Upgrade operačního systému klientů  

Configuration Manager podporuje místní upgrade operačního systému pro klienty Configuration Manager v následujících situacích:  

- Pokud Configuration Manager podporuje výslednou úroveň aktualizace Service Pack, podporuje místní upgrade na novější aktualizaci Service Pack systému Windows.  

- Místní upgrade systému Windows z podporované verze na Windows 10. Další informace najdete v tématu [upgrade Windows na nejnovější verzi](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Upgrady údržby Windows 10 z buildu na sestavení. Další informace najdete v tématu [Správa systému Windows jako služby](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> SQL Server upgradu  

Configuration Manager podporuje místní upgrade SQL Server na serveru databáze lokality.

Informace o verzích SQL Server, které Configuration Manager podporuje, najdete v tématu [podpora verzí SQL Server](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Upgrade verze aktualizace Service Pack SQL Serveru

Pokud Configuration Manager stále podporuje výslednou úroveň SQL Server aktualizace Service Pack, podporuje místní upgrade SQL Server na novější aktualizaci Service Pack.

Pokud máte v hierarchii více než jednu Configuration Manager lokalitu, každá lokalita nástroje může spustit jinou verzi aktualizace Service Pack SQL Server. Neexistuje žádné omezení pořadí, ve kterém lokality upgradují verzi aktualizace Service Pack SQL Server.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Upgrade na novou verzi SQL Server

Configuration Manager podporuje místní upgrade SQL Server na tyto verze:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

To zahrnuje upgrade SQL Server Express na novější verzi SQL Server Express v sekundárních lokalitách.

Pokud upgradujete verzi SQL Server, která je hostitelem databáze lokality, je nutné upgradovat SQL Server verzi, která se používá v lokalitách v tomto pořadí:

1. Nejdříve upgradovat SQL Server v lokalitě centrální správy  

2. Upgrade sekundárních lokalit před upgradem nadřazené primární lokality sekundární lokality  

3. Nakonec upgradujte nadřazené primární lokality. Tyto lokality zahrnují podřízené primární lokality, které jsou součástí centrální lokality pro správu, a samostatné primární lokality, které jsou lokalitou nejvyšší úrovně v hierarchii.  

### <a name="sql-server-cardinality-estimation-level"></a>SQL Server úroveň odhadu mohutnosti

Při upgradu databáze lokality ze starší verze SQL Server databáze udržuje existující úroveň odhadu mohutnosti SQL, pokud je minimální povolená pro tuto instanci SQL Server. Upgrade SQL Server s databází na úrovni kompatibility nižší než povolená úroveň automaticky nastaví databázi na nejnižší úroveň kompatibility povolenou SQL Server.

Následující tabulka uvádí doporučené úrovně kompatibility pro databáze Configuration Manager lokality:

|Verze SQL Serveru | Podporované úrovně kompatibility | Doporučená úroveň |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Pro identifikaci úrovně kompatibility odhadu SQL Server mohutnosti, která se používá pro vaši databázi lokality, spusťte následující dotaz SQL na serveru databáze lokality:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Další informace o úrovních kompatibility SQL CE a o tom, jak je nastavit, najdete v tématu [ALTER DATABASE Compatibility Level (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

Další informace o upgradu SQL Server najdete v následujících článcích SQL Server:  

- [Upgradovat na SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Upgradovat na SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Upgrade na SQL Server 2014](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Upgrade SQL Serveru na serveru databáze lokality  

1. Zastavit všechny služby Configuration Manager Services v lokalitě  

2. Upgradovat SQL Server na podporovanou verzi  

3. Restartování služby Configuration Manager Services  

> [!NOTE]  
> Když změníte edici SQL Server používané v lokalitě centrální správy z úrovně Standard na Datacenter nebo Enterprise, oddíl databáze se nemění. Tento oddíl databáze omezuje počet klientů, které hierarchie podporuje.