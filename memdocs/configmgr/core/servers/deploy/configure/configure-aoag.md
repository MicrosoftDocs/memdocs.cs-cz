---
title: Konfigurace skupin dostupnosti
titleSuffix: Configuration Manager
description: Nastavení a Správa skupin dostupnosti Always On SQL Server s Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e85b36d0caeb6ceb99f56220e271774dc0db0f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699241"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Konfigurace skupin dostupnosti Always On SQL Server pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku vám popoužívají ke konfiguraci a správě skupin dostupnosti, které používáte s Configuration Manager.

Než začnete, potřebujete:  

- Seznamte se s informacemi z části [Příprava na používání skupin dostupnosti Always On SQL Server s Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).
- Seznamte se s SQL Server dokumentaci, která se zabývá používáním skupin dostupnosti a souvisejících postupů. Tyto informace jsou nutné k provedení následujících scénářů.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Vytvoření a konfigurace skupiny dostupnosti

Pomocí následujícího postupu vytvořte skupinu dostupnosti a poté přesuňte kopii databáze lokality do této skupiny dostupnosti.

1. Pomocí následujícího příkazu zastavte Configuration Manager web:

    `preinst.exe /stopsite`

    Další informace najdete v tématu [Nástroj Údržba hierarchie](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Změňte model zálohování databáze lokality z **jednoduchého** na **úplný**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Skupiny dostupnosti podporují jenom model ÚPLNÉho zálohování. Další informace najdete v tématu [zobrazení nebo změna modelu obnovení databáze](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Pomocí SQL Server vytvořte úplnou zálohu databáze lokality. Zvolte jednu z následujících možností:

    - **Bude členem vaší skupiny dostupnosti**: Pokud použijete tento server jako počátečního člena primární repliky skupiny dostupnosti, nebudete muset obnovovat kopii databáze lokality na tomto serveru nebo jinou ve skupině. Databáze je již na primární replice k dismístě. SQL Server replikuje databázi do sekundárních replik v průběhu pozdějšího kroku.  

    - **Nebude členem skupiny dostupnosti**: Obnovte kopii databáze lokality na serveru, který bude hostitelem primární repliky skupiny.

    Další informace najdete v následujících článcích v dokumentaci k SQL Server:

    - [Vytvořit úplnou zálohu databáze](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Obnovení zálohy databáze pomocí SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Pokud plánujete přesunout ze skupiny dostupnosti na samostatnou ve stávající replice, nejdřív odeberte databázi ze skupiny dostupnosti.

4. Na serveru, který bude hostitelem počáteční primární repliky skupiny, vytvořte skupinu dostupnosti pomocí [Průvodce novou skupinou dostupnosti](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) . V průvodci:

    - Na stránce **Vybrat databázi** vyberte databázi pro Configuration Manager Web.  

    - Na stránce **Specify Replicas** (Zadat repliky) nakonfigurujte toto nastavení:

        - **Repliky:** Zadejte servery, které budou hostovat sekundární repliky.

        - **Naslouchací proces:** Zadejte **název DNS naslouchacího procesu** jako úplný název DNS, například `<listener_server>.fabrikam.com` . Když nakonfigurujete Configuration Manager, aby používal databázi ve skupině dostupnosti, tento název se používá.

    - Na stránce **Select Initial Data Synchronization** (Vybrat počáteční synchronizaci dat) vyberte možnost **Úplná**. Až Průvodce vytvoří skupinu dostupnosti, průvodce zálohuje primární databázi a protokol transakcí. Průvodce je pak obnoví na každém serveru, který je hostitelem sekundární repliky.

        > [!Note]  
        > Pokud tento krok nepoužijete, obnovte kopii databáze lokality na každém serveru, který je hostitelem sekundární repliky. Pak ručně Připojte tuto databázi ke skupině.

5. Ověřte konfiguraci na každé replice:

    1. Ujistěte se, že počítačový účet serveru lokality je členem místní skupiny **Administrators** na každém počítači, který je členem skupiny dostupnosti.  

    2. Spusťte [ověřovací skript](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) a potvrďte, že je databáze lokality v každé replice správně nakonfigurovaná.

    3. Pokud je potřeba nastavit konfigurace na sekundárních replikách, než budete pokračovat, ručně převezme služby primární repliky do sekundární repliky. Databázi můžete nakonfigurovat jenom pro primární repliku. Další informace najdete v tématu [provedení plánovaného ručního převzetí služeb při selhání skupiny dostupnosti](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) v dokumentaci k SQL Server.

6. Až budou všechny repliky splňovat požadavky, je skupina dostupnosti připravena k použití s Configuration Manager.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Konfigurace lokality pro použití skupiny dostupnosti

Po [Vytvoření a konfiguraci skupiny dostupnosti](#bkmk_create)použijte Configuration Manager Údržba lokality a nakonfigurujte lokalitu tak, aby používala databázi, kterou hostuje Skupina dostupnosti.

Instalace nové lokality se svou databází ve skupině dostupnosti není podporovaná. Pokud například používáte základní média, nainstalujte lokalitu pomocí jediné instance SQL Server. Po instalaci lokality přesuňte databázi lokality do skupiny dostupnosti.

1. Spusťte **instalační program Configuration Manager**: `\BIN\X64\setup.exe` z Configuration Manager instalační složky webu.

2. Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat**lokalitu a pak vyberte **Další**.

3. Vyberte **změnit konfiguraci SQL Server**a pak vyberte **Další**.

4. Pro databázi lokality znovu nakonfigurujte následující nastavení:

    - **SQL Server název**: zadejte virtuální název *naslouchacího procesu*skupiny dostupnosti. Naslouchací proces jste nakonfigurovali při vytváření skupiny dostupnosti. Virtuálním názvem by měl být úplný název DNS, třeba `<Listener_Server>.fabrikam.com` .  

    - **Instance:** Chcete-li určit výchozí instanci pro *naslouchací proces* skupiny dostupnosti, tato hodnota musí být prázdná. Pokud aktuální databáze lokality běží na pojmenované instanci, vymažte aktuální pojmenovanou instanci.

    - **Databáze:** Nechte název tak, jak je zobrazený. Toto je název aktuální databáze lokality.

5. Po zadání informací o novém umístění databáze dokončete instalační program s normálním procesem a konfigurací.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Synchronní členové repliky  

Pokud je databáze lokality hostována ve skupině dostupnosti, použijte následující postupy k přidání nebo odebrání členů synchronní repliky. Další informace o podporovaném typu a počtu replik najdete v tématu [Konfigurace skupin dostupnosti](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> Přidat nového člena synchronní repliky

<!--3127336-->
Počínaje verzí 1906 spusťte instalační program Configuration Manager a přidejte nového synchronního člena repliky.

1. Pomocí SQL Server postupů přidejte sekundární repliku.

    1. [Přidejte sekundární repliku do skupiny dostupnosti Always On](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Sledujte stav ve službě SQL Management Studio. Počkejte, až se skupina dostupnosti vrátí na úplný stav.

1. Spusťte instalační program Configuration Manager a vyberte možnost změny webu.

1. Jako název databáze zadejte název naslouchacího procesu skupiny dostupnosti. Pokud naslouchací proces používá nestandardní síťový port, určete také. Tato akce způsobí, že instalační program zajistí, aby byl každý uzel správně nakonfigurovaný. Také spustí proces obnovení databáze.

Configuration Manager instalační program používá operaci přesunu databáze SQL a zajišťuje, aby byly správně nakonfigurovány uzly.

Další informace o tom, jak tento proces provést ručně ve verzi 1902 nebo starší, najdete v tématu [ConfigMgr 1702: Přidání nového uzlu (sekundární replika) do existující služby SQL Ao AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### <a name="remove-a-replica-member"></a>Odebrání člena repliky

Počínaje verzí 1906 můžete k odebrání člena repliky použít Configuration Manager Setup. Pro [Přidání nového synchronního člena repliky](#bkmk_sync-add)použijte stejný postup.

Další informace o tom, jak tento proces provést ručně ve verzi 1902 nebo starší, najdete v tématu [odebrání sekundární repliky ze skupiny dostupnosti](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Asynchronní repliky

Můžete použít asynchronní repliku ve skupině dostupnosti, kterou používáte s Configuration Manager. Nemusíte spouštět konfigurační skripty potřebné ke konfiguraci synchronní repliky, protože asynchronní replika není pro databázi lokality podporována.

### <a name="configure-an-asynchronous-commit-replica"></a>Konfigurace repliky asynchronního potvrzování

Další informace najdete v tématu [Přidání sekundární repliky do skupiny dostupnosti](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Obnovení lokality pomocí asynchronní repliky

K obnovení databáze lokality použijte asynchronní repliku.

1. Zastavte aktivní primární lokalitu, aby se zabránilo dalším zápisům do databáze lokality. Chcete-li lokalitu zastavit, použijte [Nástroj Hierarchy Maintenance](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. Po zastavení webu použijte asynchronní repliku místo [ručně obnovené databáze](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> Ukončení používání skupiny dostupnosti

Následující postup použijte v případě, že už nechcete hostovat databázi lokality ve skupině dostupnosti. V tomto procesu přesunete databázi lokality zpátky do jediné instance SQL Server.

1. Zastavte Configuration Manager webu pomocí následujícího příkazu: `preinst.exe /stopsite` . Další informace najdete v tématu [Nástroj Údržba hierarchie](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Pomocí systému SQL Server vytvořte úplnou zálohu databáze lokality z primární repliky. Další informace najdete v tématu [vytvoření úplné zálohy databáze](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Pomocí systému SQL Server obnovte zálohu databáze lokality na serveru, který bude hostitelem databáze lokality. Další informace najdete v tématu [obnovení zálohy databáze pomocí SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Pokud bude server primární repliky pro skupinu dostupnosti hostovat jednu instanci databáze lokality, přeskočte tento krok.

4. Na serveru, který bude hostovat databázi lokality, změňte model zálohování databáze lokality z **úplného** na **jednoduché**. Další informace najdete v tématu [zobrazení nebo změna modelu obnovení databáze](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Spusťte **instalační program Configuration Manager**: `\BIN\X64\setup.exe` z Configuration Manager instalační složky webu.

6. Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat**lokalitu a pak vyberte **Další**.  

7. Vyberte **změnit konfiguraci SQL Server**a pak vyberte **Další**.  

8. Pro databázi lokality znovu nakonfigurujte následující nastavení:

    - **Název SQL Serveru:** Zadejte název serveru, který je teď hostitelem databáze lokality.

    - **Instance:** Zadejte pojmenovanou instanci, která je hostitelem databáze lokality. Pokud je databáze na výchozí instanci, ponechte toto pole prázdné.

    - **Databáze:** Nechte název tak, jak je zobrazený. Toto je název aktuální databáze lokality.

9. Po zadání informací o novém umístění databáze dokončete instalační program s normálním procesem a konfigurací. Po dokončení instalace se lokalita restartuje a začne používat nové umístění databáze.

10. Pokud chcete vyčistit servery, které byly členy skupiny dostupnosti, postupujte podle pokynů v části [Odebrání skupiny dostupnosti](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).