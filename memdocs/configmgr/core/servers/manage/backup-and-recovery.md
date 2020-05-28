---
title: Zálohovat lokality
titleSuffix: Configuration Manager
description: Naučte se zálohovat své weby před tím, než dojde k selhání nebo ztrátě dat v Configuration Manager.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 46d2af2d89e41e931add0f77931b442b68835235
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906478"
---
# <a name="back-up-a-configuration-manager-site"></a>Zálohování lokality Configuration Manageru

*Platí pro: Configuration Manager (Current Branch)*

Připravte přístup k zálohování a obnovení, abyste se vyhnuli ztrátě dat. U Configuration Managerch webů vám přístup k zálohování a obnovení pomůže rychleji obnovit lokality a hierarchie a s minimální ztrátou dat.  

Oddíly v tomto článku vám můžou pomáhat při zálohování vašich webů. Chcete-li obnovit lokalitu, přečtěte si téma [obnovení pro Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> K dispozici jsou dvě metody zálohování Configuration Manager Site Recovery:
>
> - Úspěšná záloha z úlohy údržby **Zálohovat server webu**
> - Ručně obnovená záloha databáze lokality


## <a name="considerations-before-creating-a-backup"></a>Předpoklady před vytvořením zálohy  

-   Pokud pro hostování databáze lokality používáte skupinu dostupnosti Always On SQL Server, upravte své plány zálohování a obnovení, jak je popsáno v části [Příprava na použití SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

-   Configuration Manager může obnovit databázi lokality z úlohy zálohování Configuration Manager. Může také použít zálohu databáze lokality, kterou vytvoříte pomocí jiného procesu.   

     Databázi lokality můžete například obnovit ze zálohy, která byla vytvořena jako součást plánu údržby Microsoft SQL Server. K zálohování databáze lokality můžete použít taky zálohu, která je vytvořená pomocí Data Protection Manager.  

-   Počínaje verzí 1806 nainstalujte další server lokality v *pasivním* režimu. Server lokality v pasivním režimu je kromě stávajícího serveru lokality v *aktivním* režimu. Server lokality v pasivním režimu je k dispozici pro okamžité použití v případě potřeby. Další informace najdete v tématu [Vysoká dostupnost serveru lokality](../deploy/configure/site-server-high-availability.md). I když tato role neodebírá nutnost plánování a cvičení operací zálohování a obnovení, významně snižuje úsilí při obnovení lokality v případě potřeby.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Využití aplikace Data Protection Manager k zálohování lokality
K zálohování databáze Configuration Manager lokality můžete použít System Center Data Protection Manager (DPM).

Vytvořte novou skupinu ochrany v aplikaci DPM pro počítač databáze lokality. Na stránce **Vybrat členy skupiny** v Průvodce vytvořením nové skupiny ochrany vytvoření vyberte službu SMS Writer ze seznamu zdroj dat. Pak vyberte databázi lokality jako příslušného člena. Další informace o použití aplikace DPM najdete v knihovně dokumentace [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) .  

> [!IMPORTANT]  
>  Configuration Manager nepodporuje zálohování aplikace DPM pro cluster SQL Server, který používá pojmenovanou instanci. Podporuje zálohování DPM na SQL Serverm clusteru, který používá výchozí instanci SQL Server.  

Po obnovení databáze lokality postupujte podle kroků v části instalace pro obnovení lokality. Chcete-li použít databázi lokality, kterou jste zazálohovali s Data Protection Manager, vyberte možnost obnovení pro **použití databáze lokality, která byla ručně obnovena**.  



## <a name="backup-maintenance-task"></a>Úloha zálohovací údržby
Zálohování Configuration Managerch lokalit můžete automatizovat naplánováním předdefinované úlohy údržby Zálohovat server webu. Tato úloha má následující funkce:

-   Spouští se podle plánu.
-   Zálohuje databázi lokality.
-   Zálohuje určité klíče registru.
-   Zálohuje určité složky a soubory.
-   Zálohuje [disk CD. Poslední složka](the-cd.latest-folder.md)   

Naplánujte spuštění výchozí úlohy zálohování lokality minimálně každých pět dní. Důvodem je to, že Configuration Manager používá *dobu uchovávání dat SQL Serverho sledování změn* pět dnů. Další informace najdete v tématu [SQL Server dobu uchovávání dat sledování změn](recover-sites.md#sql-server-change-tracking-retention-period).

Chcete-li zjednodušit proces zálohování, můžete vytvořit soubor **soubor AfterBackup. bat** . Tento skript po úspěšném dokončení úlohy zálohování automaticky spustí akce po zálohování. K archivaci snímku zálohy do zabezpečeného umístění použijte soubor soubor AfterBackup. bat. Můžete také použít soubor soubor AfterBackup. bat ke zkopírování souborů do složky zálohy nebo ke spuštění jiných úloh zálohování.  

Můžete zálohovat lokalitu centrální správy a primární lokalitu. Sekundární lokality nebo servery systému lokality nemají úlohy zálohování.

Po spuštění služby Configuration Manager Backup se postupuje podle pokynů definovaných v řídicím souboru zálohování: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl` . Pokud chcete chování zálohovací služby změnit, můžete upravit řídicí soubor zálohování.  
> [!NOTE]
> Změny **Smsbkup. CTL** budou platit po restartování SMS_SITE_VSS_WRITER služby na serveru lokality.

Do souboru **Smsbkup.log** se zapisují stavové informace o zálohování lokality. Tento soubor se vytvoří v cílové složce, kterou určíte ve vlastnostech úlohy údržby Zálohovat server webu.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Zapnutí úlohy zálohovací údržby pro lokalitu  
1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2.  Vyberte lokalitu, pro kterou chcete povolit úlohu údržby zálohování lokality.  

3.  Na pásu karet klikněte na **úlohy údržby lokality** .  

4.  Vyberte úlohu **Zálohovat server webu** a klikněte na **Upravit**.  

5.  Vyberte možnost pro **Povolení této úlohy**. Klikněte na **nastavit cesty** a zadejte cílovou složku zálohy. Máte tyto možnosti:  

    > [!IMPORTANT]  
    >  Aby nemohlo být se soubory zálohy manipulováno, uložte je do zabezpečeného umístění. Nejbezpečnější cestou k zálohování je místní disk, takže můžete nastavit oprávnění pro soubory NTFS ve složce. Configuration Manager nešifruje zálohovaná data uložená v cestě k záloze.  

    -   **Místní jednotka na serveru lokality pro data lokality a databázi**: Určuje, že úloha ukládá záložní soubory pro lokalitu a databázi lokality do zadané cesty na místní diskové jednotce serveru lokality. Vytvořte místní složku před spuštěním úlohy zálohování. Místní systémový účet na serveru lokality musí mít oprávnění k **zápisu** souborů NTFS do místní složky pro zálohování serveru lokality. Místní systémový účet počítače, na kterém běží SQL Server, musí mít ke složce pro zálohování databáze lokality oprávnění pro **zápis** systému souborů NTFS.  

    -   **Síťová cesta (název UNC) pro data lokality a databázi**: Určuje, že úloha ukládá záložní soubory pro lokalitu a databázi lokality v zadané síťové cestě. Před spuštěním úlohy zálohování vytvořte sdílenou složku. Účet počítače serveru lokality musí mít ke sdílené síťové složce oprávnění pro **zápis** systému souborů NTFS a oprávnění ke sdílení. Pokud je SQL Server nainstalován na jiném počítači, účet počítače SQL Server musí mít stejná oprávnění.  

    -   **Místní jednotky na serveru lokality a SQL Server**: Určuje, jestli má úloha ukládat záložní soubory pro lokalitu do zadané cesty na místním disku serveru lokality. Úloha ukládá záložní soubory pro databázi lokality do zadané cesty na místním disku serveru databáze lokality. Vytvořte místní složky před spuštěním úlohy zálohování. Účet počítače serveru lokality musí mít ke složce, kterou vytvoříte na serveru lokality, oprávnění pro **zápis** systému souborů NTFS. Účet počítače SQL Serveru musí mít ke složce, kterou vytvoříte na serveru databáze lokality, oprávnění pro **zápis** systému souborů NTFS. Tato možnost je k dispozici pouze v případě, že databáze lokality není nainstalována na serveru lokality.  

    > [!NOTE]  
    > Možnost procházení k cíli zálohování je k dispozici pouze v případě, že zadáte síťovou cestu cíle zálohování.  
    >  
    > Název složky nebo sdílené složky, který se používá pro cílové umístění zálohy, nepodporuje použití znaků Unicode.  

6.  Nakonfigurujte plán pro úlohu zálohování lokality. Vezměte v úvahu plán zálohování, který je mimo aktivní pracovní dobu. Pokud máte hierarchii, zvažte plán, který se spouští alespoň dvakrát týdně. Pokud lokalita nebude úspěšná, tento plán zajistí maximální uchovávání dat.  

    Když spustíte konzolu Configuration Manager na stejném serveru lokality, který konfigurujete pro zálohování, úloha zálohování použije pro plán místní čas. Když spouštíte konzolu Configuration Manager z jiného počítače, úloha zálohování používá pro plán koordinovaný světový čas (UTC).  

7.  Vyberte, zda chcete vytvořit výstrahu v případě, že úloha zálohování lokality neproběhne úspěšně. Když se tato možnost vybere, Configuration Manager vytvoří kritickou výstrahu pro selhání zálohování. Tyto výstrahy můžete zkontrolovat v uzlu **výstrahy** v pracovním prostoru **monitorování** .  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Ověřte, zda je spuštěna úloha údržby Zálohovat server webu.  

-   Ověřte časové razítko v souborech v cílové složce zálohování, kterou byl úkol vytvořen. Ověřte, zda se časové razítko aktualizuje na čas, kdy bylo naposledy naplánováno spuštění úlohy.  

-   V pracovním prostoru **monitorování** přejdete do uzlu **Stav součásti** . Zkontrolujte stavové zprávy pro **SMS_SITE_BACKUP**. Až se zálohování lokality úspěšně dokončí, zobrazí se zpráva s ID **5035**. Tato zpráva znamená, že bylo zálohování lokality dokončeno bez chyb.  

-   Když nakonfigurujete úlohu zálohování tak, aby při selhání vytvořila výstrahu, vyhledejte výstrahy selhání zálohování v uzlu **výstrahy** v pracovním prostoru **monitorování** .  

-   Na serveru lokality otevřete Průzkumníka Windows a přejděte na adresu `<ConfigMgrInstallationFolder>\Logs` . Upozornění a chyby najdete v **protokolu Smsbkup. log** . Po úspěšném dokončení zálohování lokality se v protokolu zobrazí `Backup completed` Zpráva s ID `STATMSG: ID=5035` .  

    > [!TIP]  
    >  Pokud se úloha zálohovací údržby nezdařila, restartujte úlohu zálohování zastavením a restartováním **SMS_SITE_BACKUP** služby systému Windows.  



## <a name="archive-the-backup-snapshot"></a>Archivace snímku zálohy  
Úloha zálohování vytvoří snímek zálohy při prvním spuštění. Tento snímek můžete použít k obnovení serveru lokality, pokud se nedaří. Když se úloha zálohování znovu spustí podle plánu, vytvoří nový snímek zálohy, který přepíše předchozí snímek. V důsledku toho má web pouze jeden snímek zálohy a neexistuje žádný způsob, jak načíst starší snímek zálohy.  

Ponechte více archivů záložního snímku z následujících důvodů:  

-   Je běžné, že záložní média selžou, přestanou být vložená nebo obsahují pouze částečnou zálohu. Obnovení poškozené samostatné primární lokality ze starší zálohy je lepší, než obnovení bez jakékoli zálohy. Pro server lokality v hierarchii se záloha musí nacházet v době uchování dat sledování změn SQL Server, nebo není zálohování nutné.  

-   Poškození v lokalitě může pokračovat nezjištěné po několik cyklů zálohy. Je možné, že budete muset použít záložní snímek z doby, kdy se lokalita stala poškozená. Tento důvod platí pro samostatnou primární lokalitu a lokality v hierarchii, kde se záloha nachází v SQL Server dobu uchovávání dat sledování změn.  

-   Lokalita nemusí mít žádný záložní snímek. Například pokud úloha údržby Zálohovat server webu neproběhne úspěšně. Vzhledem k tomu, že úloha zálohování odebere předchozí snímek zálohy před tím, než začne zálohovat aktuální data, nebude k dispozici platný snímek zálohy.  



## <a name="using-the-afterbackupbat-file"></a>Použití souboru AfterBackup.bat  
Po úspěšném zálohování lokality se úloha zálohování automaticky pokusí spustit skript s názvem **soubor AfterBackup. bat**. Ručně vytvořte soubor soubor AfterBackup. bat na serveru lokality v nástroji `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box` . Pokud soubor soubor AfterBackup. bat existuje ve správné složce, spustí se automaticky po dokončení úlohy zálohování.

Soubor soubor AfterBackup. bat umožňuje archivaci záložního snímku na konci každé operace zálohování. Může automaticky provádět další úlohy po zálohování, které nejsou součástí úlohy údržby Zálohovat server webu. Soubor AfterBackup.bat integruje archiv a činnosti zálohování a zajistí tak, že každý nový snímek zálohy bude archivován.

Pokud soubor soubor AfterBackup. bat není k dispozici, úloha zálohování ho přeskočí, aniž by to mělo vliv na operaci zálohování. Chcete-li ověřit, zda úloha zálohování úspěšně spustila tento skript, v pracovním prostoru **monitorování** vyberte uzel **Stav součásti** a zkontrolujte stavové zprávy pro **SMS_SITE_BACKUP**. Když úloha úspěšně spustí soubor příkazu soubor AfterBackup. bat, zobrazí se zpráva s ID **5040**.  

> [!TIP]  
>  K archivaci záložních souborů serveru lokality pomocí nástroje soubor AfterBackup. bat musíte použít příkaz pro kopírování v dávkovém souboru. Jeden z těchto nástrojů je [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) ve Windows serveru. Například vytvořte soubor soubor AfterBackup. bat pomocí následujícího příkazu:`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

I když zamýšlené použití souboru soubor AfterBackup. bat slouží k archivaci záložních snímků, můžete vytvořit soubor soubor AfterBackup. bat pro spuštění dalších úloh na konci každé operace zálohování.  



##  <a name="supplemental-backup-tasks"></a>Další úlohy zálohování  
Úloha údržby Zálohovat server webu poskytuje záložní snímek pro soubory serveru lokality a databázi lokality. Při vytváření strategie zálohování se nezálohují žádné další položky, které je potřeba vzít v úvahu. Tyto části vám pomůžou dokončit strategii Configuration Manager zálohování.  

### <a name="back-up-custom-reports"></a>Zálohování vlastních sestav   
Pokud v SQL Server Reporting Services upravíte předdefinované nebo vytvořené vlastní sestavy, vytvořte zálohu pro soubory databáze serveru sestav. Záloha serveru sestav musí zahrnovat následující součásti:
- Zdrojové soubory pro sestavy a modely
- Šifrovací klíče
- Vlastní sestavení nebo rozšíření
- Konfigurační soubory
- Vlastní zobrazení SQL Server používaná ve vlastních sestavách
- Vlastní uložené procedury  

> [!IMPORTANT]  
>  Když Configuration Manager aktualizuje na novější verzi, předdefinované sestavy se můžou přepsat novými sestavami. Pokud upravíte předdefinovanou sestavu, ujistěte se, že jste sestavu zazálohovali a pak ji obnovíte ve službě Reporting Services.  

Další informace o zálohování vlastních sestav ve službě Reporting Services najdete v tématu [operace zálohování a obnovení pro služby Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Zálohování souborů obsahu  
Knihovna obsahu v Configuration Manager je umístění, kam se ukládají všechny soubory obsahu pro všechna nasazení softwaru. Knihovna obsahu se nachází na serveru lokality a v každém distribučním bodě. Úloha údržby Zálohovat server webu nezálohuje knihovnu obsahu nebo zdrojové soubory balíčku. Pokud dojde k chybě serveru lokality, informace o knihovně obsahu budou obnoveny do databáze lokality, ale je nutné obnovit knihovnu obsahu a zdrojové soubory balíčku.  

-   Aby bylo možné znovu distribuovat obsah do distribučních bodů, je nutné obnovit knihovnu obsahu. Po spuštění Redistribuce obsahu Configuration Manager zkopíruje soubory z knihovny obsahu serveru lokality do distribučních bodů. Další informace najdete v [knihovně obsahu](../../plan-design/hierarchy/the-content-library.md).  

-   Než budete moct aktualizovat obsah v distribučních bodech, je potřeba obnovit zdrojové soubory balíčku. Když začnete s aktualizací obsahu, Configuration Manager zkopíruje nové nebo změněné soubory ze zdroje balíčku do knihovny obsahu. Pak zkopíruje soubory do přidružených distribučních bodů. Spusťte následující SQL Server dotaz na databázi lokality, abyste našli zdrojové umístění balíčku pro všechny balíčky a aplikace: `SELECT * FROM v_Package` . Zdrojové umístění balíčku lze určit podle prvních tří znaků ID balíčku. Pokud je třeba ID balíčku CEN00001, kód lokality pro zdrojovou lokalitu je CEN. Když obnovíte zdrojové soubory balíčku, musí být obnoveny do stejného umístění, ve kterém se nacházely před selháním.  

Ověřte, zda jste do zálohy systému souborů pro server lokality zahrnuli knihovnu obsahu a zdrojové soubory balíčku.  

### <a name="back-up-custom-software-updates"></a>Zálohování aktualizací uživatelského softwaru  
System Center Updates Publisher je samostatný nástroj, který umožňuje spravovat vlastní aktualizace softwaru. Nástroj Updates Publisher používá pro své úložiště softwarových aktualizací místní databázi. Pokud používáte nástroje Updates Publisher ke správě vlastních aktualizací softwaru, určete, zda byste měli do plánu zálohování zahrnout databázi Updates Publisher. Další informace najdete v tématu [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

K zálohování databáze nástroje Updates Publisher použijte následující postup.  

#### <a name="back-up-the-updates-publisher-database"></a>Zálohování databáze nástroje Updates Publisher  

1.  V počítači, který spouští nástroje Updates Publisher, vyhledejte soubor databáze nástroje Updates Publisher **Scupdb. sdf** v `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` . Pro každého uživatele, který spouští Updates Publisher, je k dispozici jiný databázový soubor.  

2.  Zkopírujte databázový soubor do umístění zálohy. Pokud je například cílem zálohování `E:\ConfigMgr_Backup` , můžete zkopírovat soubor databáze nástroje Updates Publisher do `E:\ConfigMgr_Backup\SCUP` .  

    > [!TIP]  
    >  Pokud je v počítači více než jeden databázový soubor, zvažte uložení souboru do podsložky, která označuje profil uživatele přidružený k databázovému souboru. Například můžete mít jeden databázový soubor v `E:\ConfigMgr_Backup\SCUP\User1` a další databázový soubor v `E:\ConfigMgr_Backup\SCUP\User2` .  



## <a name="user-state-migration-data"></a>Data migrace stavu uživatele  
K zachycení a obnovení dat o stavu uživatele ve scénářích nasazení operačního systému můžete použít Configuration Manager sekvence úloh. Vlastnosti bodu migrace stavu seznam složek, v nichž jsou uložena data o stavu uživatele. Tato data nejsou zálohována jako součást úlohy údržby zálohování serveru lokality. Jako součást plánu zálohování musíte ručně zálohovat složky, které určíte k uložení údajů migrace stavu uživatele.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Určení složek používaných k ukládání dat migrace stavu uživatele  

1.  V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** .  

2.  Vyberte systém lokality, který je hostitelem role migrace stavu. Pak vyberte možnost **bod migrace stavu** v podokně **role systému lokality** .  

3.  Na pásu karet klikněte na **vlastnosti** .  

4.  Složky, které obsahují údaje migrace stavu uživatele, jsou uvedené v části **Podrobnosti složky** na kartě **Obecné**.  



## <a name="about-the-sms-writer-service"></a>Služba zapisovače SMS  
SMS Writer je služba, která během procesu zálohování komunikuje s Windows služba Stínová kopie svazku (VSS). Služba zapisovače SMS musí být spuštěná, aby se lokalita Configuration Manager úspěšně dokončila.  

### <a name="process"></a>Proces  
1. Služba SMS Writer je zaregistrována spolu se službou VSS a váže se k jejím rozhraním a událostem. 
2. Když služba VSS vysílá události nebo odešle upozornění do služby SMS Writer, služba SMS Writer na upozornění odpoví a provede příslušnou akci. 
3. Zapisovač SMS přečte řídicí soubor zálohování **Smsbkup. CTL** umístěný v a `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` určí soubory a data, která mají být zálohována. 
4. Zapisovač SMS vytváří metadata, která se skládají z různých součástí, včetně konkrétních dat z klíče a podklíčů registru serveru SMS. 
    a. Po vyžádání pošle metadata do služby VSS. 
    b. Služba VSS pak pošle metadata do žádosti o Configuration Manager správce zálohování. 
5. Správce zálohování vybere data, která se mají zálohovat, a pošle tato data do zapisovače SMS prostřednictvím služby VSS. 
6. Služba SMS Writer učiní potřebné kroky, aby se připravila na proces zálohování. 
7. Později, až bude služba VSS připravena k pořízení snímku: a. Pošle událost b. Služba SMS Writer zastaví všechny Configuration Manager služby v jazyce c. Zajišťuje, aby byly během vytváření snímku zamrazené aktivity Configuration Manager. 
8. Jakmile je snímek vytvořen, služba SMS Writer opět spustí zastavené služby a činnosti.

Služba SMS Writer se instaluje automaticky. V okamžiku, kdy si aplikace VSS vyžádá zálohování nebo obnovu, musí být služba SMS Writer spuštěna.  

### <a name="writer-id"></a>ID zapisovače  
ID zapisovače zapisovače SMS je **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Oprávnění  
Služba SMS Writer musí být spuštěna pod účtem místního systému.  

### <a name="volume-shadow-copy-service"></a>Služba Stínová kopie svazku  
VSS (Volume Shadow Copy Service) je sada rozhraní API modelu COM, umožňující zálohování svazku, zatímco aplikace v systému mohou do svazků stále zapisovat. Služba VSS nabízí jednotné rozhraní, pomocí kterého je možné koordinovat uživatelské aplikace, aktualizující data na disku (služba SMS Writer), a aplikace provádějící zálohování (služba Správce zálohování). Další informace najdete v [Služba Stínová kopie svazku](https://docs.microsoft.com/windows-server/storage/file-server/volume-shadow-copy-service).  



## <a name="next-steps"></a>Další kroky
Po vytvoření zálohy se v této záloze doporučuje [Site Recovery](recover-sites.md) . Tento postup vám může přispět k tomu, abyste se seznámili s procesem obnovení, než ho budete muset spoléhat. Může také pomáhat s potvrzením, že zálohování proběhlo podle svého zamýšleného účelu.  
