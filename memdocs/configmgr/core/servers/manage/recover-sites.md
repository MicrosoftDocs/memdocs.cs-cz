---
title: Site Recovery
titleSuffix: Configuration Manager
description: Naučte se obnovovat své weby v Configuration Manager.
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37e4db2ad801c5923ba3db54554af0bb13968048
ms.sourcegitcommit: 64727a4b025a589e270842da39516c4c42563a34
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84301431"
---
# <a name="recover-a-configuration-manager-site"></a>Obnovení lokality nástroje Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Spusťte Configuration Manager Site Recovery po chybě lokality nebo dojde ke ztrátě dat v databázi lokality. Oprava a opětovná synchronizace data představují klíčové úlohy obnovení lokality a jsou nezbytné, chcete-li zabránit přerušování činností.

Části v tomto článku vám pomůžou obnovit Configuration Manager Web. Pokud chcete vytvořit zálohu, přečtěte si téma [zálohování pro Configuration Manager](backup-and-recovery.md).

## <a name="considerations-before-recovering-a-site"></a>Předpoklady před obnovou lokality

> [!Important]  
> Tyto informace se vztahují jenom na scénáře Site Recovery. Při upgradu místní infrastruktury a při neaktivním obnovování lokality se systémem si přečtěte informace v následujících článcích:
>
> - [Upgrade místní infrastruktury](upgrade-on-premises-infrastructure.md)
> - [Změna infrastruktury](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Příprava serverového hardwaru

<!-- 2841893 -->

Ujistěte se, že na serveru lokality nejsou přítomny existující konfigurace. Všechny předchozí konfigurace můžou způsobit konflikty během procesu Site Recovery. Pro serverový hardware použijte jednu z následujících možností:

- Použijte nový server, který splňuje požadavky na obecné a obnovení.

- Naformátujte disky a znovu nainstalujte operační systém na stávajícím serveru. Ujistěte se, že splňuje požadavky na obecné a obnovení.

- Opětovné použití existujícího serveru, který jste vyčistili

K vyčištění stávajícího serveru použijte jeden z následujících postupů:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Vyčistit stávající server pouze pro obnovení webového serveru

1. Odstranit klíče registru serveru SMS:`HKLM\Software\Microsoft\SMS`
2. Odstraňte všechny položky registru počínaje `SMS` od `HKLM\System\CurrentControlSet\Services` . Příklad:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Odinstalace konzoly Configuration Manager
4. Restartování serveru
5. Potvrďte, že jsou odstraněny všechny výše uvedené klíče registru.

Server je teď připravený na Configuration Manager postup obnovení.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Vyčistit stávající server jenom pro obnovení databáze lokality

1. Zálohujte databázi lokality. Zálohujte taky všechny další podpůrné databáze, jako je WSUS.
2. Nezapomeňte si uvědomit název a název instance SQL serveru.
3. Ručně odstraňte databázi lokality z SQL Server
4. Restartujte SQL Server

Server je teď připravený na Configuration Manager postup obnovení.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Vyčištění stávajícího serveru pro úplné obnovení

1. Zálohujte databázi lokality. Zálohujte taky všechny další podpůrné databáze, jako je WSUS.
2. Vytvoření kopie knihovny obsahu
3. Ručně odstraňte databázi lokality z SQL Server
4. Odinstalace Configuration Managerového webu
5. Ručně odstraňte instalační složku Configuration Manager a všechny další složky Configuration Manager
6. Restartování serveru
7. Obnovení knihovny obsahu a dalších databází, jako je WSUS

Server je teď připravený na Configuration Manager postup obnovení.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Použijte podporovanou verzi a stejnou edici SQL Server

<!-- SCCMDocs#751 -->

Pokud je to možné, použijte stejnou verzi SQL Server. Podporuje ale obnovení databáze na novější verzi.

Neměňte edici SQL Server. Obnovení databáze lokality z edice Standard Edition na verzi Enterprise se nepodporuje.

Další požadavky na konfiguraci SQL Server:

- SQL Server nelze nastavit do **režimu jednoho uživatele**.
- Ujistěte se, že jsou soubory MDF a LDF platné. Při obnovení lokality se nekontrolují stav souborů.  

### <a name="sql-server-always-on-availability-groups"></a>Skupiny dostupnosti AlwaysOn pro SQL Server

Pokud pro hostování databáze lokality používáte skupiny dostupnosti Always On SQL Server, upravte své plány obnovení, jak je popsáno v části [Příprava na použití SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Repliky databáze

Po obnovení databáze lokality, kterou jste nakonfigurovali pro repliky databáze, překonfigurujte každou repliku. Než budete moci použít repliky databáze, vytvořte znovu publikace i odběry.

## <a name="determine-your-recovery-options"></a>Nastavení možností obnovy

Existují dvě hlavní oblasti, které je třeba zvážit pro Configuration Manager obnovení primárního serveru lokality a lokality centrální správy (CAS): **Server lokality** a **databáze lokality**.
Následující části vám pomůžou vybrat nejlepší možnosti pro váš scénář obnovení.

> [!NOTE]  
> Configuration Manager když instalační program zjistí existující lokalitu na serveru, můžete spustit obnovení lokality, ale možnosti obnovení pro server lokality jsou omezené. Pokud například spustíte instalační program v existujícím serveru lokality, pak když zvolíte obnovení, budete moci obnovit databázový server lokality, ale možnost obnovení serveru lokality zůstane zakázána.

### <a name="site-server-recovery-options"></a>Možnosti obnovení serveru lokality

Spusťte instalační program Configuration Manager z kopie **disku CD-ROM. Poslední** složka, kterou jste vytvořili mimo instalační složku Configuration Manager.  

- Pokud spustíte instalaci z nabídky **Start** na serveru lokality, možnost **obnovit lokalitu** není dostupná.  

- Pokud jste před provedením zálohování nainstalovali do konzoly Configuration Manager nějaké aktualizace, nemůžete lokalitu přeinstalovat pomocí instalačního programu z následujících umístění:

  - Instalační médium
  - Configuration Manager cesta instalace

Pak vyberte možnost **obnovit lokalitu** . U vadného serveru lokality máte následující možnosti obnovení:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Obnovení serveru lokality pomocí existující zálohy

Tuto možnost použijte, pokud máte Configuration Manager zálohu serveru lokality před selháním lokality. Lokalita vytvoří tuto zálohu jako součást úlohy údržby **Zálohovat server webu** . Lokalita bude přeinstalována a nastavení lokality je konfigurováno na základě zálohovaného webu.  

#### <a name="reinstall-the-site-server"></a>Přeinstalování serveru lokality

Tuto možnost použijte, pokud nemáte zálohu serveru lokality. Server lokality bude znovu nainstalován a při počáteční instalaci je nutné zadat nastavení lokality.  

- Použijte stejný kód lokality a název databáze lokality, který jste použili při první instalaci vadné lokality.  

- Lokalitu můžete znovu nainstalovat na nový počítač, na kterém je spuštěná nová verze operačního systému.  

- Server musí používat stejný název hostitele a plně kvalifikovaný název domény (FQDN) původního serveru lokality.

### <a name="site-database-recovery-options"></a>Možnosti obnovení databázového serveru

Při spuštění instalačního programu Configuration Manager máte k dispozici následující možnosti obnovení pro databázi lokality:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Obnovení databáze lokality pomocí zálohovacího skladu

Tuto možnost použijte, pokud máte Configuration Manager zálohu databáze lokality před tím, než dojde k selhání databáze. Lokalita vytvoří tuto zálohu jako součást úlohy údržby **Zálohovat server webu** . V hierarchii při obnovení primární lokality proces obnovení načítá z CAS všechny změny provedené v databázi lokality po poslední záloze. Při obnovení CAS proces obnovení načte tyto změny z referenční primární lokality. Při obnovení databáze lokality pro samostatnou primární lokalitu ztratíte změny lokality po poslední záloze.  

Při obnovování databáze lokality v hierarchii se chování obnovení liší pro certifikační autority a primární lokalitu. Chování se liší i v případě, že se poslední záloha nachází uvnitř nebo mimo SQL Server dobu uchovávání dat sledování změn. Další informace najdete v části [scénáře obnovení databáze lokality](#site-database-recovery-scenarios) v tomto článku.  

> [!NOTE]  
> Pokud zvolíte obnovení databáze lokality pomocí zálohovacího skladu, ale databáze lokality již existuje, obnovení nebude úspěšné.  

#### <a name="create-a-new-database-for-this-site"></a>Vytvořit novou databázi pro tento web

Tuto možnost použijte, pokud nemáte zálohu databáze lokality. V hierarchii vytvoří proces obnovení novou databázi lokality. Při obnovování podřízené primární lokality se data obnoví replikací z certifikačních autorit. Při obnovení CAS replikuje data z referenční primární lokality. Tato možnost není dostupná, pokud obnovujete samostatnou primární lokalitu nebo certifikační autority, které nemají primární lokality.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Použít databázi lokality, která byla ručně obnovena

Tuto možnost použijte, pokud jste již obnovili Configuration Manager databázi lokality, ale musíte dokončit proces obnovení.  

- Configuration Manager může obnovit databázi lokality z některého z následujících procesů:  

  - Úloha údržby zálohování Configuration Manager  
  - Zálohování databáze lokality pomocí Data Protection Manager (DPM)  
  - Jiný proces zálohování  

    Po obnovení databáze lokality pomocí metody mimo Configuration Manager spusťte instalační program a výběrem této možnosti dokončete obnovení databáze lokality.  

    > [!NOTE]  
    > Použijete-li aplikaci DPM k zálohování databáze lokality, použijte postupy DPM k obnovení databáze lokality do zadaného umístění předtím, než budete pokračovat v procesu obnovení v Configuration Manager. Další informace o aplikaci DPM najdete v knihovně dokumentace [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) .  

- Když v hierarchii obnovíte databázi primární lokality, proces obnovení načte z CAS všechny změny provedené v databázi lokality po poslední záloze. Při obnovení CAS proces obnovení načte tyto změny z referenční primární lokality. Při obnovení databáze lokality pro samostatnou primární lokalitu ztratíte změny lokality po poslední záloze.  

#### <a name="skip-database-recovery"></a>Přeskočit obnovení databáze

Tuto možnost použijte, pokud nedošlo ke ztrátě dat na serveru databáze Configuration Manager lokality. Tato možnost je platná pouze v případě, že je databáze lokality na jiném počítači, než je server lokality, který obnovujete.  

### <a name="sql-server-change-tracking-retention-period"></a>Doba uchování dat sledování změn systému SQL Server

Configuration Manager povoluje sledování změn pro databázi lokality v SQL Server. Sledování změn umožňuje Configuration Manager dotaz na informace o změnách provedených v tabulkách databáze po předchozím bodě v čase. Doba uchování určuje, jak dlouho budou informace sledování změn uchovány. Ve výchozím nastavení je databáze lokality nakonfigurovaná tak, aby měla dobu uchování pět dnů. Po obnovení databáze lokality pokračuje proces obnovení odlišně, pokud se záloha nachází v rámci doby uložení nebo mimo dobu uchování. Například pokud váš SQL Server nebude úspěšný a vaše poslední záloha je sedm dní, bude mimo dobu uchování.

Další informace o SQL Server sledování změn v interních verzích najdete v následujících blogových příspěvcích z týmu SQL Server: [Change Tracking Cleanup – část 1](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) a [Change Tracking Cleanup – část 2](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Opětovná inicializace lokality nebo globálních dat

Proces opětovné inicializace lokality nebo globálních dat nahrazuje stávající data v databázi lokality daty z jiné databáze lokality. Například, pokud lokalita ABC znovu inicializuje data z lokality XYZ, dojde k následujícím krokům:

- Data budou zkopírována z lokality XYZ do lokality ABC.
- Stávající data lokality XYZ budou odstraněna z databáze lokality ABC.
- Zkopírovaná data z lokality XYZ budou vložena do databáze lokality ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Příklad scénáře 1: primární lokalita znovu inicializuje globální data z certifikačních autorit.

Proces obnovení odebere stávající globální data z primární lokality v databázi primární lokality a nahradí data globálními daty zkopírovanými z certifikačních autorit.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Příklad scénáře 2: certifikační autorita znovu inicializuje data lokality z primární lokality.

Proces obnovení odebere stávající data lokality pro danou primární lokalitu v databázi CAS. Nahrazuje data lokality zkopírovaná z primární lokality. Data lokality pro ostatní primární lokality to neovlivní.

### <a name="site-database-recovery-scenarios"></a>Scénáře obnovení databáze lokality

Po obnovení databáze lokality ze zálohy se Configuration Manager pokusí obnovit změny v lokalitě a globální data po poslední záloze databáze. Configuration Manager spustí následující akce po obnovení databáze lokality ze zálohy:  

#### <a name="recovered-site-is-a-cas"></a>Obnovená lokalita je certifikační autorita.

- Záloha databáze v rámci doby uchování sledování změn  

  - **Globální data**: změny v globálních datech po zálohování se replikují ze všech primárních lokalit.  

  - **Data lokality**: změny v datech lokality po zálohování se replikují ze všech primárních lokalit.  

- Záloha databáze starší než doba uchování sledování změn  

  - **Globální data**: certifikační autorita znovu inicializuje globální data z referenční primární lokality, pokud ji zadáte. Pak všechny ostatní primární lokality znovu inicializují globální data z certifikačních autorit. Pokud neurčíte referenční lokalitu, všechny primární lokality znovu inicializují globální data z certifikačních autorit. Tato data se obnovila ze zálohy.  

  - **Data lokality**: certifikační autorita znovu inicializuje data lokality z každé primární lokality.  

#### <a name="recovered-site-is-a-primary-site"></a>Obnovená lokalita je primární lokalita

- Záloha databáze v rámci doby uchování sledování změn  

  - **Globální data**: změny v globálních datech po zálohování se replikují z certifikačních autorit.  

  - **Data lokality**: certifikační autorita znovu inicializuje data lokality z primární lokality. Změny po zálohování se ztratí. Klienti znovu generují většinu dat, když odesílají informace do primární lokality.  

- Záloha databáze starší než doba uchování sledování změn  

  - **Globální data**: primární lokalita znovu inicializuje globální data z certifikačních autorit.  

  - **Data lokality**: certifikační autorita znovu inicializuje data lokality z primární lokality. Změny po zálohování se ztratí. Klienti znovu generují většinu dat, když odesílají informace do primární lokality.  

## <a name="site-recovery-procedures"></a>Postupy obnovení lokality

Pro obnovení serveru lokality a databáze lokality použijte jeden z následujících postupů:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Spuštění obnovení lokality v Průvodci instalací

1. Zkopírujte [disk CD. Nejnovější složku](the-cd.latest-folder.md) do umístění mimo instalační složku Configuration Manager. Z kopie disku CD-ROM. Nejnovější složku, spusťte Průvodce instalací Configuration Manager.  

2. Na stránce **Začínáme** vyberte **obnovit lokalitu**a pak vyberte **Další**.  

3. Dokončete průvodce pomocí možnosti, které jsou vhodné pro obnovení lokality.  

     - Během obnovení instalační program identifikuje port SQL Server Service Broker (SSB), který používá SQL Server. Toto nastavení portu během obnovování neměňte, nebo nebude replikace dat po dokončení obnovení správně fungovat.  

     - V Průvodci instalací můžete určit původní nebo novou cestu, kterou chcete použít pro instalaci Configuration Manager.  

### <a name="start-an-unattended-site-recovery"></a>Spuštění bezobslužného obnovení lokality

1. Připravte skript bezobslužné instalace na možnost, že bude nutné obnovit lokalitu. Další informace najdete v tématu [bezobslužné obnovení lokality](unattended-recovery.md).  

2. Spusťte instalační program Configuration Manager pomocí `/script` Možnosti příkazového řádku. Například vytvoříte inicializační soubor instalace **ConfigMgrUnattend. ini**. Uložte ho do `C:\Temp` adresáře počítače, na kterém spouštíte instalační program. Použijte následující příkaz:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> Po obnovení certifikačních autorit se může zdařit replikace některých dat lokality z podřízených lokalit. Tato data můžou zahrnovat inventář hardwaru, inventář softwaru a stavové zprávy.
>
> Pokud k tomuto problému dojde, inicializujte znovu **ConfigMgrDRSSiteQueue** pro replikaci databáze. Pomocí **správce SQL Server** spusťte následující dotaz na databázi lokality pro certifikační autority:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Úlohy po obnově

Po obnovení lokality je nutné zvážit několik úloh po obnovení, než bude obnovení lokality dokončeno. Následující části vám pomohou dokončit proces obnovení lokality.

### <a name="reenter-user-account-passwords"></a>Zadejte znovu hesla uživatelského účtu.

Po obnovení serveru lokality znovu zadejte hesla pro všechny uživatelské účty v lokalitě. Tato hesla se resetují během obnovování lokality. Účty se zobrazí na stránce **dokončeno** v Průvodci instalací po dokončení obnovení lokality. Seznam je také uložen do `C:\ConfigMgrPostRecoveryActions.html` obnoveného serveru lokality.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Opětovné zadání hesel uživatelského účtu po obnovení lokality

1. Otevřete konzolu Configuration Manager a připojte se k obnovenému webu.  

2. V pracovním prostoru **Správa** rozbalte nabídku **zabezpečení**a pak vyberte **účty**.  

3. Pro každý účet proveďte následující kroky a znovu zadejte heslo:  

     1. Vyberte účet ze seznamu zjištěného po obnovení lokality.  

     2. Na pásu karet vyberte **vlastnosti** .  

     3. Na kartě **Obecné** vyberte možnost **nastavit**a znovu zadejte heslo pro tento účet.  

     4. Vyberte **ověřit**, zvolte odpovídající zdroj dat pro vybraný uživatelský účet a pak vyberte **Test připojení**. Tento krok testuje, jestli se uživatelský účet může připojit ke zdroji dat, a ověří přihlašovací údaje.  

     5. Výběrem **OK** uložte změny hesla a pak kliknutím na **OK** zavřete stránku vlastností účtu.  

#### <a name="reenter-pxe-passwords"></a>Znovu zadat hesla PXE

<!-- SCCMDocs#1683 -->

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** . Každý místní distribuční bod s **hodnotou Ano** ve sloupci **PXE** je povolen pro technologii PXE a může mít heslo pro opětovné zadání.

1. Vyberte distribuční bod s povoleným PXE a na pásu karet vyberte **vlastnosti** .

1. Přepněte na kartu **PXE** .

1. Pokud je povolená možnost **vyžadovat heslo, když počítače používají PXE** , zadejte a potvrďte heslo.

1. Výběrem **OK** uložte a zavřete vlastnosti.

Tento postup opakujte pro všechny ostatní místní distribuční body s povoleným PXE.

#### <a name="reenter-task-sequence-passwords"></a>Znovu zadat hesla pořadí úkolů

<!-- SCCMDocs#1683 -->

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .

1. Vyberte pořadí úkolů a potom na pásu karet vyberte **Upravit**.

1. Přečtěte si následující postup, který vám umožní zadat hesla:

    - **Použít nastavení systému Windows**: Pokud povolíte a zadáte heslo místního správce, znovu zadejte a potvrďte heslo.

    - **Použít nastavení sítě**: pro účet, který má oprávnění pro připojení k doméně, vyberte možnost **nastavit**. Zadejte a potvrďte heslo a pak vyberte **ověřit**.

    - **Zachytit bitovou kopii operačního systému**: pro účet, který se používá pro přístup k cíli, vyberte možnost **nastavit**. Zadejte a potvrďte heslo a pak vyberte **ověřit**.

    - **Připojit k síťové složce**: pro účet, který se používá pro připojení k síťové složce, vyberte **nastavit**. Zadejte a potvrďte heslo a pak vyberte **ověřit**.

    - **Zapnout nástroj BitLocker**: Pokud použijete možnost správy klíčů **TPM a PIN kód**, znovu zadejte kód PIN.

    - **Připojit k doméně nebo pracovní skupině**: pro účet, který má oprávnění pro připojení k doméně, vyberte možnost **nastavit**. Zadejte a potvrďte heslo a pak vyberte **ověřit**.

    - **Spustit příkazový řádek**: Pokud použijete možnost pro **spuštění tohoto kroku jako u následujícího účtu**, vyberte **nastavit**. Zadejte a potvrďte heslo a pak vyberte **ověřit**.

    - **Spustit powershellový skript**: Pokud použijete možnost pro **spuštění tohoto kroku jako u následujícího účtu**, vyberte **nastavit**. Zadejte a potvrďte heslo a pak vyberte **ověřit**.

Tento postup opakujte pro všechna pořadí úloh.

### <a name="recreate-bootable-media-and-prestaged-media-in-non-pki-environments"></a>Opětovné vytvoření spouštěcího média a předzpracovaného média v prostředích bez infrastruktury veřejných klíčů

V prostředích bez infrastruktury veřejných klíčů jsou certifikáty podepsané svým držitelem ve spouštěcím médiu a předzpracovaném médiu založené na klíčích počítačů serveru, na kterém se médium vytvořilo. Z tohoto důvodu je potřeba znovu vytvořit jakékoli spouštěcí médium a Předzpracované médium vytvořené na tomto serveru, pokud se změní hardware nebo se operační systém přeinstaluje jako součást obnovení. Další informace o tom, jak vytvořit spouštěcí média a předzpracovaná média, najdete v tématu [Vytvoření spouštěcího média](../../../osd/deploy-use/create-bootable-media.md) a [Vytvoření předzpracovaného média](../../../osd/deploy-use/create-prestaged-media.md).

### <a name="reenter-sideloading-keys"></a>Znovu zadat klíče pro zkušební načtení

Po obnovení serveru lokality znovu zadejte klíče pro zkušební načtení systému Windows určené pro danou lokalitu. Při obnovení lokality se tyto klíče resetují. Po opětovném zadání klíče pro zkušební načtení lokalita obnoví počet ve sloupci **použité aktivace** pro klíče pro zkušební načtení systému Windows.

Například před selháním lokality se celkový počet **aktivací** zobrazí jako **100**. Počet klíčů, které zařízení používaly, nebo **používané aktivace**, jsou **90**. Po obnovení lokality se hodnota **Celkový počet aktivací** stále zobrazuje **100**, ale ve sloupci počet **používaných aktivací** se nesprávně zobrazuje hodnota **0**. Až 10 nových zařízení použije klíč pro zkušební načtení, neexistují žádné další klíče pro zkušební načtení a v jedenáctém zařízení se nepovede použít klíč pro zkušební načtení.

### <a name="recreate-azure-services"></a>Opětovné vytvoření služeb Azure

<!-- SCCMDocs#1022 -->

V Configuration Manager verze 1806 se po obnovení lokality v CloudMgr. log zobrazí následující chyba:

`Index (zero-based) must be greater than or equal to zero`

Chcete-li tento problém vyřešit, [obnovte tajný klíč](../deploy/configure/azure-services-wizard.md#bkmk_renew) pro každé připojení klienta Azure.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Konfigurace protokolu SSL pro role systému lokality používající službu IIS

Při obnovení systémů lokality, které spouštějí službu IIS a jste nakonfigurovali pro protokol HTTPS, překonfigurujte službu IIS tak, aby používala certifikát webového serveru.

### <a name="reinstall-hotfixes"></a>Opětovná instalace oprav hotfix

Po obnovení lokality je nutné znovu nainstalovat všechny [opravy hotfix vzdálené správy](updates.md#bkmk_outofband) , které byly aplikovány na server lokality. Po obnovení lokality si prohlédněte seznam dříve nainstalovaných oprav hotfix na stránce **dokončeno** v Průvodci instalací nástroje. Tento seznam je také uložen do `C:\ConfigMgrPostRecoveryActions.html` obnoveného serveru lokality.

### <a name="recover-custom-reports"></a>Obnovení vlastních sestav

Někteří zákazníci vytvářejí v SQL Server Reporting Services vlastní sestavy. V případě, že se tato součást nezdařila, obnovte sestavy ze zálohy serveru sestav. Další informace o obnovení vlastních sestav ve službě Reporting Services najdete v tématu [operace zálohování a obnovení pro služby Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Obnovení souborů obsahu

Databáze lokality sleduje, kde webový server ukládá soubory obsahu. Samotné soubory obsahu nejsou zálohovány ani obnoveny v rámci procesu zálohování a obnovení. Chcete-li plně obnovit soubory obsahu, obnovte knihovnu obsahu a zdrojové soubory balíčku do původního umístění. Existuje několik způsobů, jak obnovit soubory obsahu. Nejjednodušším způsobem je obnovit soubory ze zálohy systému souborů serveru lokality.

Pokud zálohu systému souborů pro zdrojové soubory balíčku nemáte, ručně je zkopírujte nebo stáhněte. Tento postup je podobný jako při původním vytvoření balíčku. Spuštěním následujícího dotazu v SQL Server Najděte zdrojové umístění balíčku pro všechny balíčky a aplikace: `SELECT * FROM v_Package` . Identifikujte zdrojovou lokalitu balíčku tak, že prohlížíte první tři znaky ID balíčku. Pokud je třeba ID balíčku CEN00001, kód lokality pro zdrojovou lokalitu je CEN. Pokud obnovujte zdrojové soubory balíčku, musíte je obnovit do stejného umístění, ve kterém se nacházely před selháním.

Pokud nemáte zálohu systému souborů, která zahrnuje knihovnu obsahu, máte následující možnosti obnovení:  

- **Importovat soubor připraveného obsahu**: v hierarchii Configuration Manager můžete vytvořit soubor připraveného obsahu se všemi balíčky a aplikacemi z jiného umístění. Pak importujte soubor připraveného obsahu a obnovte knihovnu obsahu na serveru lokality.  

- **Aktualizace obsahu**: Configuration Manager zkopíruje obsah ze zdroje balíčku do knihovny obsahu. Aby se tato akce úspěšně dokončila, musí být zdrojové soubory balíčku dostupné v původním umístění. Proveďte tuto akci u každého balíčku a aplikace.

### <a name="recover-custom-software-updates"></a>Obnovení vlastních aktualizací softwaru

Pokud jste zahrnuli System Center Updates Publisher databázových souborů do plánu zálohování, můžete obnovit databáze, pokud dojde k chybě počítače nástroje Updates Publisher. Další informace o nástroji Updates Publisher najdete v tématu [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Obnovení databáze nástroje Updates Publisher

1. Přeinstalujte Publisher Updates Publisher na obnovený počítač.  

2. Zkopírujte soubor databáze **Scupdb. sdf** z cílového umístění zálohy do `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` v počítači, který spouští nástroje Updates Publisher.  

3. Pokud je v počítači spuštěno více než jeden uživatel, zkopírujte každý soubor databáze do příslušného umístění profilu uživatele.  

### <a name="user-state-migration-data"></a>Data migrace stavu uživatele

Jako součást vlastností bodu migrace stavu určíte složky, do kterých se ukládají data o stavu uživatele. Po obnovení bodu migrace stavu ručně obnovte data stavu uživatele na serveru. Obnovte je do stejných složek, v nichž byla data uložena před selháním.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Opakované vygenerování certifikátů pro distribuční body

Po obnovení lokality může **Distmgr. log** vypsat následující položku pro jeden nebo více distribučních bodů: `Failed to decrypt cert PFX data` . Tato položka označuje, že lokalita nemůže dešifrovat data certifikátu distribučního bodu. Tento problém vyřešíte tak, že znovu vygenerujete nebo znovu naimportujete certifikát pro ovlivněné distribuční body. Použijte rutinu [set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) prostředí PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aktualizace certifikátů používaných pro cloudové distribuční body

Configuration Manager vyžaduje certifikát pro správu Azure pro server lokality ke komunikaci s cloudovým distribučním bodem. Po obnovení lokality aktualizujte certifikáty pro cloudové distribuční body.

## <a name="recover-a-secondary-site"></a>Obnovení sekundární lokality

Configuration Manager nepodporuje zálohu databáze v sekundární lokalitě, ale podporuje obnovení prostřednictvím přeinstalace sekundární lokality. Obnovení sekundární lokality je nutné, když dojde k chybě sekundárního Configuration Manager lokality.

### <a name="requirements"></a>Požadavky

- Server musí splňovat všechny požadavky na sekundární lokalitu a musí mít nakonfigurovaná příslušná zabezpečovací práva.  

- Použijte stejnou instalační cestu, která byla použita pro lokalitu, která selhala.  

- Použijte server se stejnou konfigurací, jako má server, který selhal. Tato konfigurace zahrnuje plně kvalifikovaný název domény (FQDN).  

- Server musí mít stejnou konfiguraci SQL Server jako lokalita, která selhala.  

  - Při obnovení sekundární lokality Configuration Manager nenainstaluje SQL Server Express, pokud ještě není v počítači nainstalovaná.  

  - Použijte stejnou verzi SQL Server a stejnou instanci SQL Server, kterou jste použili pro databázi sekundární lokality před selháním.  

### <a name="procedure"></a>Postup

Použijte akci **obnovit sekundární lokalitu** z uzlu **lokality** v konzole Configuration Manager. Na rozdíl od jiných typů webů nepoužívá obnovení sekundární lokality záložní soubor. Tento proces přeinstaluje soubory sekundární lokality na server, který selhal. Po opětovné instalaci lokality budou data sekundární lokality znovu inicializována z nadřazené primární lokality.

Během procesu obnovení Configuration Manager ověří, zda na serveru sekundární lokality existuje knihovna obsahu. Také kontroluje, zda je k dispozici příslušný obsah. Sekundární lokalita používá existující knihovnu obsahu, pokud obsahuje odpovídající obsah. V opačném případě můžete obnovit knihovnu obsahu sekundární lokality, znovu distribuovat nebo připravit obsah na server.

Máte-li distribuční bod, který není na serveru sekundární lokality, není nutné při obnovení sekundární lokality přeinstalovat distribuční bod. Po obnovení sekundární lokality se tato lokalita automaticky synchronizuje s distribučním bodem.

Stav obnovení sekundární lokality můžete ověřit pomocí akce **Zobrazit stav instalace** z uzlu **lokality** v konzole nástroje Configuration Manager.
