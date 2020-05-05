---
title: Upgradovat na aktuální větev
titleSuffix: Configuration Manager
description: Přečtěte si postup pro spuštění úspěšného místního upgradu z lokality a hierarchie, na které běží System Center 2012 Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717962"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Upgradovat na Configuration Manager aktuální větev

*Platí pro: Configuration Manager (Current Branch)*

Proveďte místní upgrade a Configuration Manager aktuální větev z lokality a hierarchie, na které běží System Center 2012 Configuration Manager. Před upgradem z nástroje System Center 2012 Configuration Manager musíte lokality připravit. Tato příprava vyžaduje odebrání konkrétních konfigurací, které mohou bránit úspěšnému upgradu. Pak postupujte podle pořadí upgradu, pokud je zapojená víc než jedna lokalita.  

> [!TIP]  
> Při správě Configuration Manager infrastruktury lokalit a hierarchie se používají výrazy *upgradu*, *aktualizace*a *instalace* , které popisují tři samostatné koncepty. Informace o tom, jak se jednotlivé podmínky používají, najdete v tématu věnovaném [upgradu, aktualizaci a instalaci](../../../understand/upgrade-update-install.md).

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a>Cesty k místnímu upgradu  

K dispozici jsou následující možnosti, které jsou aktuálně podporované v místních cestách upgradu:

### <a name="upgrade-to-version-2002"></a>Upgradovat na verzi 2002

Následující produkty můžete upgradovat na *plně licencovanou* verzi Configuration Manager aktuální větev verze 2002:

- *Zkušební* instalace Configuration Manager, aktuální větev verze 2002
- System Center 2012 Configuration Manager s aktualizací Service Pack 1
- System Center 2012 Configuration Manager s aktualizací Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager s aktualizací Service Pack 1

Další informace najdete v tématu [Nejčastější dotazy k Configuration Manager větví a licencování](../../../understand/product-and-licensing-faq.md).

> [!TIP]  
> Při upgradu z verze System Center 2012 Configuration Manager na aktuální větev budete možná moci zjednodušit proces upgradu. Další informace najdete v následujících článcích:  
>
> - [Základní a aktualizační verze](../../manage/updates.md#bkmk_Baselines)  
> - [Složka CD.Latest](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Nepodporované cesty

Následující cesty nejsou podporovány:

- Upgrade větve Technical Preview na plně licencovanou instalaci se nepodporuje. Verze Technical Preview se dá upgradovat jenom na novější verzi Technical Preview.  

- Migrace z verze Technical Preview na plně licencovanou verzi se nepodporuje.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a>Kontrolní seznamy upgradu  

Následující kontrolní seznamy vám pomůžou naplánovat úspěšný upgrade na Configuration Manager.  

### <a name="before-you-upgrade"></a>Před upgradem  

Před upgradem na Configuration Manager si Projděte tyto kroky.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Kontrola prostředí System Center 2012 Configuration Manager

Vyřešte problémy tak, jak je podrobně popsáno v následujícím podpora Microsoftu článku: [Configuration Manager klienty přeinstalujte každých pět hodin kvůli opakovanému pokusu o úlohu a můžou způsobit neúmyslný upgrade klienta](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Ujistěte se, že vaše prostředí splňuje podporované konfigurace

- Kontrola verze operačního systému serveru používaného k hostování rolí systému lokality:  

  - Některé starší operační systémy podporované Configuration Manager System Center 2012 nejsou podporované Configuration Manager aktuální větví. Před upgradem nástroje odeberte role systému lokality na těchto verzích operačního systému. Další informace najdete v tématu [podporované operační systémy pro servery systému lokality](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - Kontrola požadovaných součástí pro Configuration Manager neověřuje požadavky na role systému lokality na serveru lokality nebo ve vzdálených systémech lokality.  

- Zkontrolujte požadované součásti pro každý počítač, který je hostitelem role systému lokality. Například pro nasazení operačního systému Configuration Manager používá sadu Windows 10 Assessment and Deployment Kit (Windows ADK). Před zahájením instalace musíte stáhnout sadu Windows ADK a nainstalovat ji na server lokality a na každý počítač s instancí služby Poskytovatel serveru SMS.  

Další informace o podporovaných platformách a požadovaných konfiguracích najdete v části [podporované konfigurace](../../../plan-design/configs/supported-configurations.md).  

Další informace o použití sady Windows ADK s Configuration Manager najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Zkontrolujte stav lokality a hierarchie a ověřte, že nejsou k dispozici žádné nevyřešené problémy.

Před upgradem webu vyřešte všechny provozní problémy serveru lokality, serveru databáze lokality a rolí systému lokality, které jsou nainstalovány na vzdálených počítačích. Upgrade webu může selhat kvůli existujícím provozním problémům.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Nainstalujte všechny použitelné kritické aktualizace operačních systémů na počítače, které jsou hostitelem lokality, serveru databáze lokality a rolí vzdáleného systému lokality.

Před upgradem webu nainstalujte všechny kritické aktualizace pro všechny použitelné systémy lokality. Jestliže aktualizace, kterou instalujete, vyžaduje restart, před spuštěním aktualizace service packu restartujte příslušné počítače.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Odinstalace rolí systému lokality není podporována nástrojem Configuration Manager

Následující role systému lokality se už v Configuration Manager nepoužívají. Odinstalujte je před upgradem ze služby System Center 2012 Configuration Manager:  

- Bod vzdálené správy  

- Bod validátoru stavu systému  

- Bod webu Katalog aplikací a bod webové služby

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Zakažte repliky databáze pro body správy v primárních lokalitách.

Configuration Manager nemůže upgradovat primární lokalitu, která má repliku databáze pro body správy. Repliky databáze zakažte dříve než:  

- Vytvoříte zálohu databáze lokality pro otestování upgradu databáze.  

- Upgrade produkční lokality na Configuration Manager aktuální větev  

Další informace najdete v těchto článcích:  

- System Center 2012 Configuration Manager: [Konfigurace replik databáze pro body správy](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager aktuální větev: [repliky databáze pro body správy](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Změna konfigurace bodů aktualizace softwaru, které používají službu Vyrovnávání zatížení sítě

Configuration Manager nemůže upgradovat lokalitu, která pro hostování bodů aktualizace softwaru používá cluster služby Vyrovnávání zatížení sítě (NLB).  

Pokud používáte klastry NLB pro body softwarových aktualizací, použijte skript PowerShell k odstranění klastru NLB. (Od verze System Center 2012 Configuration Manager SP1 v konzole Configuration Manager nebyla žádná možnost konfigurace clusteru programu NLB.)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Zakažte všechny úlohy údržby lokality v každé lokalitě po dobu trvání upgradu tohoto webu.

Před upgradem na Configuration Manager zakažte všechny úlohy údržby lokality, které by mohly běžet v době, kdy je proces upgradu aktivní. Tento seznam obsahuje mimo jiné následující úlohy:  

- Zálohovat server lokality  
- Vymazat staré operace klientů  
- Vymazat stará data zjišťování  

Pokud je během procesu upgradu spuštěna úloha údržby databáze lokality, upgrade webu může selhat.  

Než úlohu zakážete, zaznamenejte plán úlohy, abyste po provedení upgradu webu mohli obnovit její konfiguraci.

Další informace o úlohách údržby lokality najdete v následujících článcích:  

- System Center 2012 Configuration Manager: [plánování operací na pracovišti](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, Current Branch: [Reference pro úlohy údržby](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Spustit kontrolu požadovaných součástí instalace

Před upgradem lokality spusťte **kontrolu požadovaných součástí** nezávisle na instalaci, abyste ověřili, že vaše lokalita splňuje požadavky. Později při upgradu lokality se Kontrola požadovaných součástí spustí znovu.  

Kontrola nezávislého požadavku vyhodnocuje web pro upgrade na aktuální větev i na LTSB (Long-Term Servicing Branch) Configuration Manager. Protože LTSB některé funkce nepodporují, mohou se v **protokolu souboru ConfigMgrPrereq. log** zobrazit položky, které jsou podobné následujícím příkladům:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Pokud plánujete upgrade na aktuální větev, můžou se chyby LTSB edice bezpečně ignorovat. Použijí se jenom v případě, že plánujete upgradovat na LTSB.

Když později spustíte Configuration Manager instalaci pro upgrade, Kontrola požadovaných součástí se znovu spustí. Vyhodnocuje váš web na základě větve Configuration Manager, kterou si zvolíte k instalaci (aktuální větev nebo LTSB). Pokud se rozhodnete upgradovat na aktuální větev, nespustí kontrolu funkcí, které LTSB nepodporuje.

Další informace najdete v části [Kontrola požadovaných součástí](prerequisite-checker.md) a [seznam kontrol požadovaných](list-of-prerequisite-checks.md)součástí.  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Stáhnout požadované soubory a distribuovatelné soubory pro Configuration Manager

Pro stažení požadovaných redistribuovatelných souborů, jazykových sad a nejnovějších aktualizací produktu použijte nástroj Configuration Manager pro stažení **instalačního programu** .  

Informace najdete v tématu Nástroj pro [stažení instalačního programu](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Plánování správy jazyků serveru a klienta

Při upgradu lokality se instalují pouze ty jazykové sady, které jste pro upgrade vybrali.  

- Instalační program zkontroluje aktuální konfiguraci jazyka vaší lokality. Pak identifikuje jazykové sady, které jsou k dispozici ve složce, kam ukládáte dříve stažené požadované soubory.  

- Můžete potvrdit výběr aktuální jazykové sady serveru a klienta nebo změnit výběry a přidat nebo odebrat podporu pro jazyky.  

- Mohou být vybrány pouze jazykové sady, které jsou k dispozici při spuštění instalačního programu.  

> [!NOTE]  
> Jazykové sady z nástroje System Center 2012 Configuration Manager nelze použít, pokud chcete povolit jazyky pro Configuration Manager aktuální větve.  

Další informace o jazykových sadách najdete v tématu [jazykové sady](language-packs.md).  

#### <a name="review-considerations-for-site-upgrades"></a>Revidovat požadavky na upgrady lokality

Při upgradu webu se některé vlastnosti a konfigurace resetují na výchozí nastavení. Nápovědu k přípravě na tyto a související změny najdete v tématu věnovaném [důležitým aspektům upgradu](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Vytvoření zálohy databáze lokality v lokalitě centrální správy a primárních lokalitách

Před upgradem lokality nástroje zálohujte databázi lokality, abyste měli jistotu, že máte úspěšnou zálohu pro použití při zotavení po havárii.  

Další informace najdete v tématu [zálohování a obnovení](../../manage/backup-and-recovery.md).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Zálohování přizpůsobeného souboru Configuration. mof

Pokud použijete přizpůsobený soubor Configuration. mof k definování datových tříd, které používáte s inventářem hardwaru, vytvořte zálohu tohoto souboru. Po upgradu obnovte tento soubor na svůj web. Další informace najdete v tématu [postup rozšiřování inventáře hardwaru](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Otestujte proces upgradu databáze na kopii nejnovější zálohy databáze lokality.

Před upgradem lokality centrální správy nebo primární lokality Configuration Manageru otestujte proces upgradu databáze lokality na kopii této databáze.  

- Otestujte proces upgradu databáze lokality. Při upgradu lokality se může změnit databáze lokality.  

- I když test upgradu databáze není vyžadován, může identifikovat problémy s upgradem před tím, než bude ovlivněna vaše provozní databáze.  

- Selhání upgradu databáze lokality může mít za následek, že vaše databáze lokality nebude funkční a pro obnovu funkčnosti může být zapotřebí obnovit lokalitu.  

- Přestože databáze lokality je mezi lokalitami sdílena v hierarchii, ještě před upgradem lokality si na všech zasažených lokalitách naplánujte otestování databáze.  

- Jestliže pro body správy v primární lokalitě používáte repliky databáze, před vytvořením zálohy databáze lokality zakažte replikaci.  

Configuration Manager nepodporuje zálohování sekundárních lokalit nebo testování upgradu databáze sekundární lokality.  

Není podporováno spuštění testu upgradu databáze na provozní databázi lokality. Tato činnost upgraduje databázi lokality a může mít za následek nefunkčnost vaší lokality.  

Další informace najdete v tématu [Testování upgradu databáze lokality](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Restartujte server lokality a každý počítač, který je hostitelem role systému lokality.

Tuto akci proveďte, chcete-li zajistit, aby nedocházelo k nevyřízeným akcím z poslední instalace aktualizací nebo z požadovaných součástí.  

#### <a name="upgrade-sites"></a>Upgradujte lokality.

Začněte u lokality nejvyšší úrovně v hierarchii a spusťte soubor Setup. exe ze zdrojového média Configuration Manager.  

Po upgradu lokality nejvyšší úrovně můžete zahájit upgrade všech podřízených lokalit. Než začnete s upgradem další lokality, dokončete upgrade každé lokality.  

Dokud se všechny lokality v hierarchii neupgradují na Configuration Manager, vaše hierarchie funguje v režimu smíšených verzí.  

Informace o tom, jak spustit upgrade, najdete v tématu [upgrade webů](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Po upgradu  

Po upgradu na Configuration Manager si Projděte tyto kroky.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Upgradovat samostatné konzoly Configuration Manager

Ve výchozím nastavení při upgradu lokality centrální správy nebo primární lokality se při instalaci upgraduje i konzola Configuration Manager, která je nainstalovaná na serveru lokality. Ručně upgradujte každou konzolu, která je nainstalovaná na jiném počítači, než je server lokality.  

> [!TIP]  
> Před zahájením upgradu vždy příslušnou konzoli zavřete.  

Další informace najdete v tématu [instalace konzol Configuration Manager](install-consoles.md).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Znovu nakonfigurujte repliky databáze pro body správy v primárních lokalitách.

Pokud pro body správy v primárních lokalitách používáte repliky databáze, před upgradem lokality odinstalujte repliky databáze. Po provedení upgradu primární lokality znovu nakonfigurujte repliky databáze pro body správy.

Další informace najdete v tématu [repliky databáze pro body správy](../configure/database-replicas-for-management-points.md).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Překonfigurujte všechny úlohy údržby databáze, které jste před upgradem zakázali.

Pokud jste v lokalitě před upgradem zakázali [úlohy údržby](../../manage/reference-for-maintenance-tasks.md) databáze, překonfigurujte tyto úlohy v lokalitě pomocí stejných nastavení, která byla provedena před upgradem.  

#### <a name="upgrade-clients"></a>Upgradujte klienty.

Až budou všechny vaše weby upgradované na Configuration Manager, naplánujte upgrade klientů.  

Při upgradu klienta se odinstaluje aktuální klientský software a nainstaluje se nová verze klientského softwaru. K upgradu klientů můžete použít libovolnou metodu, kterou Configuration Manager podporuje.  

> [!TIP]  
> Při upgradu lokality nejvyšší úrovně v hierarchii se aktualizuje také instalační balíček klienta v každém distribučním bodu hierarchie. Při upgradu primární lokality se aktualizuje balíček aktualizace klienta, který je dostupný z této primární lokality.  

Další informace najdete v tématu [Postup upgradu klientů pro počítače se systémem Windows](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a>Pokyny pro upgrade  

### <a name="automatic-actions"></a>Automatické akce

Při upgradu na Configuration Manager dojde k následujícím akcím automaticky:  

- Resetování lokality. Tato akce zahrnuje přeinstalaci všech rolí systému lokality.  

- Pokud je lokalita lokalitou na nejvyšší úrovni v hierarchii, aktualizuje instalační balíček klienta v každém distribučním bodu hierarchie. Lokalita taky aktualizuje výchozí spouštěcí image tak, aby používala novou verzi prostředí Windows PE, která je součástí sady Windows Assessment and Deployment Kit 10. Upgrade ale neupgraduje existující média pro použití s nasazením image.  

- Je-li lokalita primární lokalitou, aktualizuje balíček aktualizace klienta pro tuto lokalitu.  

### <a name="manual-actions-after-an-upgrade"></a>Ruční akce po upgradu

Po upgradu lokality se ujistěte, že provedete následující akce:  

- Ujistěte se, že se klienti přiřazení k jednotlivým primárním lokalitám upgradují a instalují novou verzi klienta.  

- Upgradujte každou Configuration Manager konzolu, která se připojuje k lokalitě nástroje a která běží na počítači, který je vzdálený od serveru lokality.  

- V primárních lokalitách, kde pro body správy používáte repliky databáze, překonfigurujte repliky databáze.  

- Po upgradu lokality ručně upgradovat fyzická média, jako jsou soubory ISO pro disky CD, DVD nebo USB flash disky. Zahrnuje také předzpracovaná média poskytovaná dodavatelům hardwaru. Upgrade lokality aktualizuje výchozí spouštěcí image, nemůže upgradovat tyto mediální soubory nebo zařízení, která se používají externě, Configuration Manager.  

- Pokud nepotřebujete starší verzi Windows PE, naplánujte aktualizaci vlastních spouštěcích imagí.  

### <a name="actions-that-affect-configurations-and-settings"></a>Akce ovlivňující konfigurace a nastavení

Když se lokalita upgraduje na Configuration Manager, některé konfigurace a nastavení se po upgradu neuchovávají. Některé konfigurace jsou nastaveny na nové výchozí hodnoty. Následující seznam obsahuje některá nastavení, která nezůstanou zachována nebo se mění:  

- **Centrum softwaru**  
    Následující položky Centra softwaru se resetují na výchozí hodnoty:  

  - **Pracovní informace** se resetují na pracovní dobu od **5:10:00** až **10:13:00** pondělí až pátek.  

  - Parametr **Údržba počítače** je nastaven na hodnotu **Pozastavit aktivity Centra softwaru, pokud je počítač v prezentačním režimu**.  

  - Parametr **Vzdálené řízení** je nastaven na hodnotu v nastaveních klienta, která jsou přiřazena k tomuto počítači.  

- **Plány Shrnutí aktualizací softwaru**: vlastní plány Shrnutí pro aktualizace softwaru nebo skupiny aktualizací softwaru se resetují na výchozí hodnotu 1 hodina. Po dokončení upgradu přenastavte hodnoty vlastních shrnutí na požadovanou četnost.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a>Testování upgradu databáze lokality  

Následující informace platí pouze v případě, že upgradujete předchozí verzi, například System Center 2012 Configuration Manager, na Configuration Manager aktuální větev.

Před upgradem lokality otestujte kopii této databáze lokality pro upgrade.  

Chcete-li otestovat databázi pro upgrade, nejprve obnovíte kopii databáze lokality do instance SQL Server, která není hostitelem Configuration Manager lokality. Verze SQL Server používaného k hostování kopie databáze musí být verze SQL Server, kterou Configuration Manager podporuje.  

Po obnovení databáze lokality na SQL Server počítači spusťte Configuration Manager instalaci ze složky zdrojového média pro Configuration Manager. Použijte možnost `/TESTDBUPGRADE` příkazového řádku.  

Další informace najdete v těchto článcích:

- [Zálohování lokality Configuration Manageru](../../manage/backup-and-recovery.md)  

- [Možnosti příkazového řádku pro instalační program](command-line-options-for-setup.md#bkmk_setup)  

- [Podpora verzí SQL Serveru](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Pokud integrujete Microsoft Intune s Configuration Manager:  
>
> Při spuštění testu upgradu databáze na kopii databáze lokality, která je starší než 5 dnů, se může zobrazit jedna z následujících zpráv:  
>
> - VAROVÁNÍ: Upgrade vynutí úplnou synchronizaci s cloudem.  
> - CHYBA: Upgrade databáze vynutí úplnou synchronizaci s cloudem.  
>
> Obě můžou být během testování upgradu databáze bezpečně ignorované. Nesignalizují selhání nebo problém s testovacím upgradem. Místo toho označují, že během vlastního upgradu se můžou data z replikační skupiny **cloudových** databází synchronizovat s Microsoft Intune.  

### <a name="test-a-site-database-for-upgrade"></a>Testování databáze lokality pro upgrade  

Pro každou lokalitu centrální správy a primární lokalitu, kterou plánujete upgradovat, použijte následující postup:  

1. Vytvořte kopii databáze lokality. Pak tuto kopii obnovte do instance SQL Server, která používá stejnou edici jako databáze lokality a která nehostuje Configuration Manager lokality. Pokud se například databáze lokality používá v instanci edice Enterprise systému SQL Server, je nezbytné obnovit databázi do instance systému SQL Server, která rovněž používá edici Enterprise systému SQL Server.  

2. Po obnovení kopie databáze spusťte instalační program ze zdrojového média pro Configuration Manager aktuální větev. Při spuštění instalačního programu použijte možnost `/TESTDBUPGRADE` příkazového řádku. Pokud instance SQL Server hostující kopii databáze není výchozí instancí, zadejte také argumenty příkazového řádku, které identifikují instanci hostující kopii databáze lokality.  

    Plánujete například upgrade databáze lokality s názvem databáze SMS_ABC. Kopii této databáze lokality obnovíte do podporované instance systému SQL Server s názvem instance DBTest. K otestování upgradu této kopie databáze lokality použijte následující příkazový řádek:`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Soubor Setup. exe je v následujícím umístění na zdrojovém médiu Configuration Manager:`SMSSETUP\BIN\X64`  

3. V instanci systému SQL Server, kde spouštíte test upgradu databáze, sledujte v souboru ConfigMgrSetup.log, který se nachází v kořenovém adresáři systémového disku, průběh a úspěšné dokončení testu:  

    - Pokud test upgradu selže, vyřešte všechny problémy související s chybou upgradu databáze lokality. Pak vytvořte novou zálohu databáze lokality a otestujte upgrade nové kopie databáze lokality.  

    - Po úspěšném dokončení procesu můžete kopii databáze odstranit.  

        > [!NOTE]  
        > Obnovení kopie databáze lokality, kterou používáte pro testovací upgrade pro použití jako databáze lokality v libovolné lokalitě, není podporováno.  

Po úspěšném upgradu kopie databáze lokality pokračujte v upgradu lokality Configuration Manager a její databáze lokality.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a>Upgradovat weby  

Po dokončení následujících úkolů jste připraveni upgradovat Configuration Manager web:

- Konfigurace před upgradem pro vaši lokalitu
- Testování upgradu databáze lokality na kopii databáze
- Stáhnout požadované soubory a jazykové sady pro verzi, kterou plánujete nainstalovat

Při upgradu lokality v hierarchii nejprve upgradujete lokalitu nejvyšší úrovně v hierarchii. Tato lokalita nejvyšší úrovně je buďto lokalita centrální správy nebo samostatná primární lokalita. Po dokončení upgradu lokality centrální správy můžete upgradovat podřízené primární lokality v libovolném pořadí. Po provedení upgradu primární lokality můžete upgradovat podřízené sekundární lokality této lokality nebo upgradovat další primární lokality před upgradem sekundárních lokalit.  

Chcete-li upgradovat lokalitu centrální správy nebo primární lokalitu, spusťte instalační program nástroje ze zdrojového média Configuration Manager. Nespouštějte instalaci pro upgrade sekundárních lokalit. Místo toho použijete konzolu Configuration Manager k upgradu sekundární lokality po dokončení upgradu její primární nadřazené lokality.  

Před upgradem lokality zavřete konzolu Configuration Manager na serveru lokality až do dokončení upgradu lokality. Také zavřete každou konzolu Configuration Manager spuštěnou v jiných počítačích, než je server lokality. Po dokončení upgradu lokality můžete konzolu znovu připojit. Nicméně dokud neprovedete upgrade konzoly Configuration Manager na novou verzi Configuration Manager, tato konzola nemůže zobrazit některé objekty a informace, které jsou k dispozici v nové verzi Configuration Manager.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Upgrade lokality centrální správy nebo primární lokality  

1. Ověřte, zda má uživatel, který spouští instalační program, následující bezpečnostní oprávnění:  

    - Práva místního **správce** na serveru lokality  

    - Pokud je server databáze lokality vzdálený od serveru lokality, oprávnění místního **správce** .  

2. Na serveru lokality otevřete následující program: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Tato akce otevře Průvodce instalací Configuration Manager.  

3. Přečtěte si informace na stránce **než začnete** a pak vyberte **Další**.  

4. Na stránce **Začínáme** vyberte možnost **upgradovat tuto Configuration Manager lokalitu**a pak vyberte **Další**.  

5. Na stránce **kód Product Key** :  

    Pokud jste dříve nainstalovali vyhodnocení Configuration Manager, můžete vybrat **nainstalovat licencovanou verzi produktu**. Pak zadejte kód Product Key pro úplnou instalaci Configuration Manager. Tato akce převede lokalitu na plnou verzi.  

    Můžete také zadat **Datum vypršení platnosti licenční smlouvy Software Assurance** jako pohodlný připomenutí k tomuto datu. Pokud tuto hodnotu nezadáte během instalace, můžete ji později zadat v konzole Configuration Manager.  

    > [!NOTE]  
    > Microsoft neověřuje datum vypršení platnosti, které jste zadali, a nepoužije toto datum pro ověření licence. Můžete ji použít jako připomenutí data vypršení platnosti. Configuration Manager pravidelně kontrolují nové aktualizace softwaru nabízené online a stav licence Software Assurance by měl být aktuální, aby měl nárok na použití těchto dalších aktualizací.

    Další informace najdete v tématu [licencování a větve](../../../understand/learn-more-editions.md).

6. Na stránce **licenční podmínky pro software společnosti Microsoft** si přečtěte a přijměte licenční podmínky a pak vyberte **Další**.  

7. Na stránce požadované **licence** si přečtěte a přijměte licenční podmínky pro požadovaný software a pak vyberte **Další**. Instalační program stáhne a automaticky nainstaluje software na systémy lokality nebo klienty, pokud je to nutné. Než budete moci pokračovat na další stránku, souhlasíte se všemi podmínkami.  

8. Na stránce **stažení požadovaných součástí** určete, jestli instalační program stáhne nejnovější obsah z Internetu, nebo použije dříve stažené soubory. Tento obsah zahrnuje redistribuovatelné soubory požadovaných součástí, jazykové sady a nejnovější aktualizace produktu. Pokud jste dříve stáhli soubory pomocí nástroje pro stažení instalačního programu, vyberte možnost **Použít dříve stažené soubory** a určete složku pro stahování. Další informace najdete v tématu Nástroj pro [stažení instalačního programu](setup-downloader.md).  

    > [!NOTE]  
    > Pokud použijete dříve stažené soubory, ověřte, zda cesta ke složce pro stahování obsahuje poslední verzi souborů.  

9. Na stránce **Výběr jazyka serveru** si prohlédněte seznam jazyků aktuálně nainstalovaných pro danou lokalitu. Vyberte další jazyky, které jsou k dispozici v této lokalitě pro konzolu Configuration Manager a pro sestavy. Můžete také vymazat jazyky, které již nechcete v této lokalitě podporovat. Ve výchozím nastavení je zvolena angličtina a nelze ji odebrat.  

    > [!IMPORTANT]  
    > Každá verze Configuration Manager nemůže používat jazykové sady z předchozí verze Configuration Manager. Pokud chcete povolit podporu pro jazyk na Configuration Manager lokalitě, kterou upgradujete, musíte použít verzi jazykové sady pro tuto novou verzi. Například během upgradu z nástroje System Center 2012 Configuration Manager na Configuration Manager aktuální větve, pokud není aktuální verze větve jazykové sady k dispozici ve stažených souborech požadovaných součástí, nemůžete pro tento jazyk nainstalovat podporu.  

10. Na stránce **Výběr jazyka klienta** si prohlédněte seznam jazyků aktuálně nainstalovaných pro danou lokalitu. Vyberte další jazyky, které jsou v této lokalitě k dispozici pro klientské počítače, nebo zrušte zaškrtnutí u jazyků, které již nechcete v této lokalitě podporovat. Určete, zda mají být povoleny všechny jazyky klientů pro klienty mobilních zařízení, a poté klikněte na tlačítko **Další**. Ve výchozím nastavení je zvolena angličtina a nelze ji odebrat.  

11. Na stránce **Souhrn nastavení** Zkontrolujte konfiguraci. Až budete připraveni, kliknutím na tlačítko **Další** spustíte kontrolu požadovaných součástí a ověříte připravenost serveru na upgrade lokality.  

12. Pokud na stránce **Kontrola požadovaných součástí instalace** nejsou uvedené žádné problémy, vyberte **Další** a upgradujte lokalitu a role systému lokality.

    Pokud nástroj pro kontrolu požadovaných součástí najde nějaký problém, vyberte položku v seznamu, kde najdete podrobnosti o tom, jak tento problém vyřešit. Než budete pokračovat v instalaci, vyřešte všechny položky se stavem **Chyba** . Po vyřešení problému klikněte na tlačítko **Spustit kontrolu** a restartujte kontrolu požadovaných součástí. V kořenovém adresáři systémové jednotky můžete také otevřít soubor ConfigMgrPrereq.log a zkontrolovat výsledky kontroly požadovaných součástí. Soubor protokolu může obsahovat další informace, které se nezobrazí v uživatelském rozhraní. Seznam požadovaných pravidel a popisů instalace najdete v části [Kontrola požadovaných součástí](list-of-prerequisite-checks.md).

Na stránce **Upgrade** zobrazí instalační program celkový průběh instalace. Po ukončení instalace základního serveru lokality a systému lokality pomocí instalačního programu můžete průvodce zavřít. Konfigurace lokality bude pokračovat na pozadí.  

### <a name="upgrade-a-secondary-site"></a>Upgrade sekundární lokality  

1. Ověřte, zda má administrativní uživatel, který spouští instalační program, následující bezpečnostní oprávnění:  

    - Práva místního **správce** na serveru sekundární lokality  

    - Role zabezpečení **správce infrastruktury** nebo správce s **úplnými oprávněními** pro nadřazenou primární lokalitu  

    - Práva správce systému (**SA**) v databázi lokality sekundární lokality  

2. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte uzel **lokality** .  

3. Vyberte sekundární lokalitu, kterou chcete upgradovat. Na kartě **Domů** na pásu karet ve skupině **lokalita** vyberte možnost **upgradovat**.  

4. Výběrem **Ano** potvrďte rozhodnutí a spusťte upgrade sekundární lokality.  

Upgrade sekundární lokality běží na pozadí. Po dokončení upgradu zkontrolujte stav v konzole Configuration Manager. Vyberte server sekundární lokality a potom na kartě **Domů** na pásu karet ve skupině **lokalita** vyberte možnost **Zobrazit stav instalace**.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a>Úkoly po upgradu  

Po upgradu lokality může být nutné provést další úlohy k dokončení upgradu nebo překonfigurování lokality. Tyto úlohy mohou zahrnovat následující položky:

- Upgrade Configuration Manager klientů
- Upgrade Configuration Managerch konzol
- Opětovné povolení replik databáze pro body správy
- Obnovení nastavení pro Configuration Manager funkce, které používáte a které po upgradu nezůstanou zachovány  
