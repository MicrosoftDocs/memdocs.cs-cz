---
title: Nejčastější dotazy týkající se velikosti a výkonu webu
titleSuffix: Configuration Manager
description: Odpovědi na běžné otázky Configuration Manager o velikosti a výkonu lokality.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073258"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Nejčastější dotazy k nastavení velikosti a výkonu webu Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento dokument popisuje Nejčastější dotazy týkající se Configuration Manager pokynů pro změnu velikosti lokality a běžné problémy s výkonem.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Nejčastější dotazy a příklady konfigurace počítačů a disků

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Jak mám naformátovat disky na serveru lokality a SQL Server?

Oddělte Configuration Manager složky Doručená pošta a soubory SQL na alespoň dvou různých svazcích. Toto oddělení vám umožní optimalizovat velikosti přidělených clusterů pro různé druhy vstupně-výstupních operací. 

U svazku hostujícího servery vašich webů použijte systém souborů NTFS s alokačními jednotkami 4K nebo 8K. ReFS zapisuje 64 KB i pro malé soubory. Configuration Manager má mnoho malých souborů, takže ReFS můžou vydávat zbytečné nároky na disk.

Pro disky obsahující soubory databáze SQL použijte formátování NTFS nebo ReFS, přičemž alokační jednotky jsou 64 KB.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Jak a kde mám rozvrhnout soubory databáze SQL?

Moderní pole jednotek SSD (Solid-State Drive) a Azure Premium Storage můžou poskytovat vysoký počet vstupně-výstupních operací na jednom svazku s několika disky. Obvykle přidáte více jednotek do pole pro další úložiště, nikoli pro další propustnost. Pokud používáte fyzické disky na discích, možná budete potřebovat více IOPS, než můžete vygenerovat na jednom svazku. Měli byste přidělit 60% celkového počtu doporučených vstupně-výstupních operací za sekundu a místo na disku pro soubor *. mdf* , 20% pro soubor *. ldf* a 20% pro dočasné soubory protokolů a dat. Všechny soubory *. ldf* a tempo se můžou nacházet na jednom svazku s 40% (20% + 20%). přiděleného IOPS.

Servery SQL starší než SQL Server 2016 byly vytvořeny ve výchozím nastavení pouze pro jeden dočasný datový soubor. Měli byste vytvořit více, abyste se vyhnuli zámkům SQL a čekali na přístup k jedinému souboru. Názory komunity se liší podle nejlepšího počtu souborů s dočasnou daty, které se mají vytvořit, od čtyř až osmi. Testování odhalí malý rozdíl mezi čtyřmi a osmi, takže můžete vytvořit čtyři soubory s dočasnoumi daty *stejné velikosti* . Vaše datové soubory databáze tempdb by měly mít až 20-25% velikost plné databáze.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Existují nějaká další doporučení pro instalaci disku?

Při konfiguraci nastavte v paměti řadiče RAID na 70% přidělení pro operace zápisu a 30% pro operace čtení. Obecně platí, že pro databázi lokality použijte konfiguraci pole RAID 10. RAID 1 je taky přijatelné pro malé lokality s požadavky na vstupně-výstupní operace nebo při použití rychlého SSD. Když máte větší disková pole, nakonfigurujte náhradní disky tak, aby automaticky nahradily neúspěšné disky.

**Příklad: fyzický počítač s fyzickými disky** 

[Pokyny](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pro určení velikosti pro společně umístěný server lokality a SQL server s **100 000** klienty jsou 1200 IOPS pro server lokality a 5000 IOPS pro SQL Server soubory.

Vaše výsledná konfigurace disku může vypadat takto:

| Jednotky<sup>1</sup> | ČLEN | Formát | Obsah svazku | Minimální počet IOPS nutných| Přibližně dodaných IOPS<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | 8k NTFS     | Složky Doručená pošta nástroje ConfigMgr    |     1700            | 1751             |
| 12x15k         | 10        | 64 KB – odkazy    | SQL. mdf             | 60% * 5 000 = 3000     | 3476             |
| 8x15k          | 10        | 64 KB – odkazy    | SQL. ldf, dočasné soubory | 40% * 5 000 = 2000     | 2322             |

1. Neobsahuje Doporučené náhradní disky. 
2. Tato hodnota je z [ukázkových konfigurací disků](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Používám technologii Hyper-V v systému Windows Server. Jak mám nakonfigurovat disky pro moje Configuration Manager virtuálních počítačů, aby se co nejlépe vyzpůsobilo?

Technologie Hyper-V přináší podobný výkon fyzickému serveru, pokud jsou hardwarové prostředky (jádra procesoru a předávací úložiště) 100% vyhrazené pro virtuální počítač (VM). Použití souborů disků s pevnou velikostí *. VHD* nebo *. vhdx* způsobuje minimální dopad na výkon v/v 1-5%. Použití dynamicky se zvětšující soubory *. VHD* nebo *. vhdx* souborů způsobuje až 25% vlivu na výkon vstupně-výstupních operací pro Configuration Manager úlohy. Pokud potřebujete dynamicky se zvětšující disky, můžete kompenzovat přidáním dalších 25% výkonu vstupně-výstupních operací do pole.

Když ve VIRTUÁLNÍm počítači spouštíte Configuration Manager Server lokality nebo SQL, izolujte jednotky operačního systému hostitele Hyper-V z virtuálního počítače a datových jednotek.

Další informace o optimalizaci virtuálních počítačů najdete v tématu [optimalizace výkonu servery Hyper-V](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Příklad: Server lokality Hyper-V na virtuálním počítači** 

[Pokyny](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pro určení velikosti pro společně umístěný server lokality a SQL server s **150 000** klienty jsou 1800 IOPS pro server lokality a 7400 IOPS pro SQL Server soubory.

Vaše výsledná konfigurace disku může vypadat takto:

| Jednotky<sup>1</sup> | ČLEN | Formát<sup>2</sup> | Obsah svazku | Minimální počet IOPS nutných| Přibližně dodaných IOPS<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Operační systém hostitele technologie Hyper-V           | -                    | -                |
| 2x10k          | 1         | -              | (Virtuální počítač) operační systém serveru lokality       | -                    | -                |
| 2xSSD SAS      | 1         | 8k NTFS        | (Virtuální počítač) složky Doručená pošta nástroje ConfigMgr    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64 KB – odkazy       | (Virtuální počítač) hostitel SQL (všechny soubory) | 7400                 | 14346            |

1. Neobsahuje Doporučené náhradní disky. 
2. Pevná velikost, Pass-through *. vhdx* pro jednotku virtuálního počítače vyhrazenou pro základní svazek. 
3. Tato hodnota je z [ukázkových konfigurací disků](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Existují nějaké návrhy Configuration Managerch prostředí v Microsoft Azure?

Začněte tím, že si přečtete [Configuration Manager v Azure – Nejčastější dotazy](configuration-manager-on-azure.md).

Virtuální počítače infrastruktury Azure jako služby (IaaS), které využívají Premium Storage disky, můžou mít vysoké IOPS. Na těchto virtuálních počítačích nakonfigurujte další disky pro očekávané potřeby místa na disku, nikoli pro další IOPS.

Služba Azure Storage je ze své podstaty redundantní a nevyžaduje pro dostupnost více disků. Disky můžete vydělit ve Správci disků nebo prostorech úložiště a zajistit tak další místo a výkon.

Další informace a doporučení, jak maximalizovat Premium Storage výkon a spustit SQL servery ve virtuálních počítačích Azure s IaaS, najdete v tématech:

- [Optimalizace výkonu aplikace](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Doprovodné materiály pro disky](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Příklad: Server lokality založený na Azure** 

[Pokyny](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pro určení velikosti pro společně umístěný server lokality a SQL server s **50 000** klienty mají osm jader, 32 GB a 1200 IOPS pro složky serveru lokality a 2800 IOPS pro SQL Server soubory.

Výsledný počítač Azure může být DS13v2 (osm jader, 56 GB) s následující konfigurací disku:

| Drives | Formát | Contains | Minimální počet IOPS nutných| Přibližně zadaný IOPS<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standardní&gt; | -             | Operační systém serveru lokality     | -                    | -                |
| 1xP20 (512 GB)    | 8k NTFS       | Složky Doručená pošta nástroje ConfigMgr  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64 KB – odkazy      | SQL (všechny soubory<sup>2</sup>) | 2800                 | 3112             |

1. Tato hodnota je z [ukázkových konfigurací disků](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. [Doprovodné](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) materiály k Azure umožňují umístění databáze tempdb na *místní jednotce jednotky SSD založené na disku* SSD, protože by nepřesáhla dostupný prostor a umožňují další distribuci v/v disku.

**Příklad: Server lokality založený na Azure (pro zvýšení výkonu okamžitě)** 

Propustnost disku Azure je omezená na velikost virtuálního počítače. Konfigurace v předchozím příkladu Azure může omezit budoucí rozšíření nebo zvýšit výkon. Pokud přidáte další disky během počátečního nasazování virtuálního počítače Azure, můžete virtuální počítač Azure navýšit na vyšší výkon zpracování v budoucnu, s minimálními investicemi do začátku. Je mnohem jednodušší naplánovat zvýšení výkonu lokality jako změny požadavků místo toho, abyste museli později dělat složitější migrace.

Změnou disků v předchozím příkladu Azure zjistíte, jak se IOPS mění.

**DS13v2** 

| Jednotky<sup>1</sup> | Formát | Contains | Minimální počet IOPS nutných| Přibližně dodaných IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standardní&gt; | -             | Operační systém serveru lokality     | -                    | -                |
| 2xP20 (1024 GB)   | 8k NTFS       | Složky Doručená pošta nástroje ConfigMgr  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64 KB – odkazy      | SQL (všechny soubory<sup>3</sup>) | 2800                 | 3984             |

1. Disky jsou vykládané pomocí prostorů úložiště.
2. Tato hodnota je z [ukázkových konfigurací disků](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Velikost virtuálního počítače omezuje výkon.
3. [Doprovodné](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) materiály k Azure umožňují umístění databáze tempdb na *místní jednotce jednotky SSD založené na disku* SSD, protože by nepřesáhla dostupný prostor a umožňují další distribuci v/v disku.

Pokud budete v budoucnu potřebovat vyšší výkon, můžete virtuální počítač naformátovat na DS14v2, což bude mít za následek zdvojnásobení procesoru a paměti. Další šířka pásma, kterou tato velikost virtuálního počítače povoluje, taky okamžitě zvýší počet dostupných diskových IOPS na dříve nakonfigurovaných discích.

**DS14v2**

| Jednotky<sup>1</sup> | ČLEN | Formát | Contains | Minimální počet IOPS nutných| Přibližně dodaných IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standardní&gt; | -             | Operační systém serveru lokality     | -                    | -                |
| 2xP20 (1024 GB)   | 8k NTFS       | Složky Doručená pošta nástroje ConfigMgr  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64 KB – odkazy      | SQL (všechny soubory<sup>3</sup>) | 2800                 | 6182             |

1. Disky jsou vykládané pomocí prostorů úložiště.
2. Tato hodnota je z [ukázkových konfigurací disků](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Velikost virtuálního počítače omezuje výkon.
3. [Doprovodné](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) materiály k Azure umožňují umístění databáze tempdb na *místní jednotce jednotky SSD založené na disku* SSD, protože by nepřesáhla dostupný prostor a umožňují další distribuci v/v disku.

## <a name="other-common-sql-server-related-performance-questions"></a>Další běžné otázky týkající se výkonu související s SQL Server 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>Je lepší pracovat s SQL společně umístěným na serveru lokality nebo ho spustit na vzdáleném serveru?

Oba můžou provádět odpovídající možnosti, za předpokladu, že jeden server má patřičnou velikost, nebo je síťové připojení dostatečné mezi těmito dvěma servery.

Remote SQL vyžaduje předem a provozní náklady na další server, ale je typický mezi většinou velkých zákazníků. Mezi výhody této konfigurace patří:

- Zvýšení možností dostupnosti lokality, například SQL Always On
- Možnost spouštění silného generování sestav s méně předaným zpracováním webu
- Jednodušší zotavení po havárii v některých situacích
- Jednodušší Správa zabezpečení
- Oddělení rolí pro správu SQL, například pomocí samostatného týmu DBA

Společně umístěný SQL vyžaduje jeden server a je typický pro většinu malých zákazníků. Mezi výhody této konfigurace patří:

- Nižší náklady na počítače, licence a údržbu
- Méně bodů selhání v lokalitě
- Lepší řízení pro plánování výpadků

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Kolik paměti RAM mám přidělit pro SQL?

Ve výchozím nastavení SQL používá veškerou dostupnou paměť na vašem serveru, může omezují operační systém a další procesy v počítači. Aby nedocházelo k potenciálním problémům s výkonem, je důležité přidělit paměť SQL explicitně. Na serverech lokality společně se serverem SQL Server se ujistěte, že operační systém má dostatek paměti RAM pro ukládání souborů do mezipaměti a jiné operace. Ujistěte se, že zbývá dostatek paměti RAM pro SMSExec a jiné procesy Configuration Manager. Při spuštění SQL na vzdáleném serveru můžete přidělit *většinu* paměti SQL, ale ne všechny. Přečtěte si [pokyny pro změnu velikosti](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pro úvodní doprovodné materiály. 

Přidělení SQL Server paměti by se mělo zaokrouhlit na celé GB. I když se velikost paměti RAM zvyšuje na velká množství, můžete nechat SQL vyšší procento. Pokud je například k dispozici 256 GB nebo více paměti RAM, můžete SQL nakonfigurovat až na 95%, protože stále zachovává dostatek paměti pro operační systém. Monitorování stránkovacího souboru je dobrým způsobem, jak zajistit dostatek paměti pro operační systém a všechny Configuration Manager procesy.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Tato data jsou v jádrech levné. Můžu do svého SQL serveru přidat spoustu těchto svazků?

Pokud je na SQL serveru více než 16 fyzických jader a není dostatek paměti RAM, může dojít k problémům s kolize paměti. Configuration Manager úlohy vylepší, pokud je k dispozici alespoň 3-4 GB paměti RAM na jádro pro SQL. Při přidávání jader do SQL serveru nezapomeňte zvýšit velikost paměti RAM v proporcionálních částkách.

### <a name="will-sql-always-on-impact-my-performance"></a>Bude mít SQL vždycky vliv na svůj výkon?

Obecně platí, že SQL Always On má zanedbatelný vliv na výkon systému, pokud je k dispozici dostatečná síť mezi servery repliky SQL. V případě zaneprázdněného prostředí SQL Always On můžete mít nárůst souborů *. ldf* rychlého protokolu databáze. Místo pro soubor protokolu se ale automaticky uvolní po úspěšném zálohování databáze. Přidejte úlohu SQL pro databázi Configuration Manager k provedení zálohování, například každých 24 hodin a zálohování *. ldf* každých 6 hodin. Další informace o službě SQL Always On a Configuration Manager, včetně dalších informací o strategiích zálohování SQL, najdete v článku [SQL Server Always On pro databázi lokality s vysokou dostupností](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="should-i-enable-sql-compression-on-my-database"></a>Mám povolit kompresi SQL v databázi?

Pro Configuration Manager databázi se komprese SQL nedoporučuje. I když neexistují žádné funkční problémy s povolením komprese na Configuration Manager databázi, výsledky testů neukazují množství úspory velikosti v porovnání s možným dopadem na výkon systému.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Mám povolit šifrování SQL v naší databázi?

Jakékoli tajné kódy v databázi Configuration Manager jsou již bezpečně uloženy, ale přidání šifrování SQL může ještě přidat jinou vrstvu zabezpečení. Neexistují žádné funkční problémy s povolením šifrování v databázi, ale může to být až 25% snížení výkonu v závislosti na tabulkách, které jste si zvolili k šifrování, a na verzi SQL, kterou používáte. Proto Zašifrujte opatrně, zejména v rozsáhlých prostředích. Nezapomeňte také aktualizovat vaše plány zálohování a obnovení, abyste měli jistotu, že můžete šifrovaná data úspěšně obnovit.

### <a name="what-version-of-sql-should-i-run"></a>Jakou verzi SQL mám spustit?

Podporované verze SQL najdete v tématu [podpora verzí SQL Server](../plan-design/configs/support-for-sql-server-versions.md). Z hlediska výkonu musí všechny podporované verze SQL splňovat požadovaná kritéria výkonu. SQL 2012 a SQL 2016 nebo novější je ale překoná SQL 2014 v některých aspektech Configuration Manager úlohy. Také spuštění SQL 2014 na úrovni kompatibility SQL 2012 (110) zvyšuje výkon obecně. V době instalace Configuration Manager databáze běžící na SQL 2012 a SQL 2014 nastavené na úroveň kompatibility 110. SQL 2016 nebo novější je nastavená na úroveň kompatibility výchozí verze SQL, jako je například 130 pro SQL 2016. Upgrade SQL na místě neaktualizuje úrovně kompatibility, dokud nenainstalujete další hlavní Configuration Manager verzi aktuální větve. 

Pokud vidíte nezvyklé časové limity nebo zpomalení u určitých dotazů SQL na SQL 2016 nebo novějším, například při použití RBAC v konzole pro správu, zkuste změnit úroveň kompatibility SQL databáze Configuration Manager na 110. Spuštění na úrovni kompatibility SQL 110 na SQL 2014 a novějších verzích SQL je plně podporované. Další informace najdete v tématu vypršení [časového limitu dotazu SQL nebo pomalé konzoly na určitých databázových dotazech Configuration Manager](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

Od ledna 2018 byste *se měli vyhnout* následujícím verzím SQL kvůli různým známým nebo jiným potenciálním problémům souvisejícím s výkonem:

- SQL 2012 SP3 CU1 na CU5
- SQL 2014 SP1 CU6 na SP2 CU2
- SQL 2016 RTM až CU3, SP1 CU3 na CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Mám implementovat další úlohy indexování SQL?

Ano, aktualizovat indexy tak často jako týden a statistiku, a to často jako jeden den pro zlepšení výkonu SQL. Skripty třetích stran a další informace, které jsou k dispozici z Configuration Manager a komunity SQL, mohou přispět k optimalizaci těchto úkolů.

Ve velkých lokalitách můžou být některé tabulky SQL, například\_CI CurrentComplianceStatusDetails, HinvChangeLog, velké v závislosti na vašich způsobech používání. Je možné, že budete muset svůj přístup k údržbě snížit nebo upravit o jeden.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>Kdy mám použít úplné SQL Server místo SQL Express na mých sekundárních lokalitách?

SQL Express nemá žádné významné dopady na výkon u sekundárních lokalit a je vhodný pro většinu zákazníků. Je také snadné ho nasadit a spravovat a jedná se o doporučenou konfiguraci pro téměř všechny zákazníky v libovolné velikosti.

Existuje jedna situace, kdy může být potřeba úplná instalace SQL Server. Pokud máte ve svém prostředí velký počet distribučních bodů a balíčků nebo zdrojů, je možné překročit limit velikosti 10 GB SQL Express. Pokud počet balíčků vyprší, kolik distribučních bodů je více než 4 000 000, například 2 000 DPs s 2 000mi obsahu, zvažte použití úplné SQL Server v sekundárních lokalitách. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Mám v databázi změnit nastavení MaxDOP?

Nastavení na 0 (použít všechny dostupné procesory) je optimální pro celkový výkon zpracování ve většině případů.

Mnoho správců Configuration Manager podle pokynů [a pokynů pro možnost konfigurace "maximální stupeň paralelismu" v SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Na většině moderních velkých hardwarových zařízení tento návod vede k navrženému maximálnímu nastavení osm. Pokud ale ve srovnání s počtem procesorů spustíte spoustu menších dotazů, může vám to usnadnit jeho nastavení na vyšší číslo. Pokud je k dispozici více jader, nebudete nutně omezovat na osm webů, pokud to není vhodné. 

Na SQL serverech s více než osmi jádry začněte s nastavením 0 a udělejte změny jenom v případě, že dojde k problémům s výkonem nebo nadměrnému zamykání. Pokud potřebujete změnit MaxDOP, protože na 0 dochází k problémům s výkonem, začněte novou hodnotou alespoň s minimálním doporučeným počtem jader pro velikost SQL serveru této lokality. Méně než tato hodnota bude téměř vždy mít negativní dopad na výkon. Například vzdálený SQL Server pro klientské servery 100 000 potřebuje aspoň 12 jader. Pokud má SQL Server 16 jader, spusťte testování nastavení MaxDOP s hodnotou 12.

## <a name="other-common-performance-related-questions"></a>Další běžné otázky související s výkonem

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Které složky na serveru lokality (nebo jiných rolích) by se měly vyloučit z antivirového softwaru?

Při zakazování antivirové ochrany v jakémkoli systému se ujistěte. V prostředích s vysokým objemem a zabezpečením doporučujeme zakázat *aktivní monitorování* pro optimální výkon.

Další informace o doporučených výjimkách antivirové ochrany najdete v tématu [doporučená vyloučení antivirového programu pro Configuration Manager 2012 a Current Branch servery lokality, systémy lokality a klienty](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Jak se dá služba WSUS zlepšit, když se používá s Configuration Manager?

Změna několika klíčových nastavení služby IIS, jako je délka fronty nastavení WsusPool a limit soukromé paměti nastavení WsusPool, může zlepšit výkon služby WSUS i na menších instalacích. Další informace najdete v tématu [doporučený hardware](../plan-design/configs/recommended-hardware.md).

Také se ujistěte, že máte nainstalované nejnovější aktualizace pro operační systém, na kterém běží služba WSUS:

- Windows Server 2012: všechny kumulativní aktualizace, které nejsou jenom pro zabezpečení, se vydávaly na 15. října 2017 nebo novější. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: všechny kumulativní aktualizace, které nejsou jenom "zabezpečení", byly vydány 2017 nebo novější. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016: všechny kumulativní aktualizace, které nejsou jenom "zabezpečení", byly vydány 2017 nebo novější. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Jaký typ údržby mám spustit na serverech WSUS?

Přečtěte si [kompletní příručku k údržbě Microsoft WSUS a Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Chci nastavit základní monitorování výkonu pro svůj web. Co mám sledovat?

Tradiční monitorování výkonu serveru efektivně funguje pro obecné Configuration Manager. Můžete také využít různé sady Management Pack System Center Operations Manager pro Configuration Manager, SQL Server a Windows Server a monitorovat základní stav serverů. Čítače Windows Performance Monitor (PerfMon) Configuration Manager také můžete přímo monitorovat. Monitorování nevyřízených položek v různých doručených oknech pro včasné varování potenciálních problémů s výkonem webu nebo nevyřízených položek.

## <a name="see-also"></a>Viz také

- [Pokyny pro velikost a výkon lokality](../plan-design/configs/site-size-performance-guidelines.md)
- [Nejčastější dotazy k Configuration Manager v Azure](configuration-manager-on-azure.md)
