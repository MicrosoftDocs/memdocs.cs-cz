---
title: Pokyny pro výkon a velikost webu
titleSuffix: Configuration Manager
description: Výsledky testování výkonu, metodologie a doprovodné materiály týkající se velikosti webu.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 9e5cc21e4fef60f64576a7b578b3616a7e37756d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073496"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Configuration Manager pokyny pro velikost a výkon lokality

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager vede ke zlepšení škálovatelnosti a výkonu v oboru. Další dokumentace obsahuje [Maximální podporované limity škálovatelnosti](size-and-scale-numbers.md) a [pokyny k hardwaru](recommended-hardware.md) pro spouštění webů v největších velikostech prostředí. Tento článek obsahuje doplňkové pokyny k výkonu pro prostředí všech velikostí. Tyto doprovodné materiály vám pomůžou přesně odhadnout hardware, který potřebujete k nasazení Configuration Manager.

Tento článek se zaměřuje na největšího přispěvatele při Configuration Manager problémech s výkonem: vstupně-výstupní subsystému disku nebo IOPS. Tento článek:

- Zobrazí podrobnosti a výsledky testů zaměřené na IOPS.
- Dokumenty, jak rekládat testy s vlastními prostředími a hardwarem
- Navrhuje požadavky na IOPS disku pro různá velikost prostředí. 

## <a name="performance-test-methodology"></a>Metodologie testu výkonu

Configuration Manager můžete nasadit mnoha jedinečnými způsoby, ale je důležité pochopit několik proměnných v každé diskuzi o velikosti. Jedna proměnná je *interval funkcí*, jako je například cyklus inventarizace. Další proměnnou je počet uživatelů, nasazení softwaru nebo jiné *objekty* , které systém odkazuje nebo nasazuje. Testování výkonu aplikuje tyto proměnné jako součást *zatížení*. Zatížení generuje objekty za typickou sazbou pro podnikové zákazníky, kteří využívají produkční nasazení v různých velikostních prostředích.

> [!NOTE] 
> Data telemetrie zákazníků umožňují testování aktuálních sestavení větví s nejběžnějšími scénáři, konfiguracemi a nastaveními pro většinu zákazníků. Doporučení v tomto článku jsou založená na těchto průměrech. Vaše prostředí se může lišit v závislosti na velikosti a konfiguraci prostředí. Obecně platí, že Configuration Manager vyžaduje běžný smysl, pokud to přichází do objektů a intervalů. Vzhledem k tomu, že můžete shromáždit všechny soubory v systému nebo nastavit interval pro cyklus na jednu minutu, neznamená to, že byste měli.

V následujících částech se zvýrazní některá nastavení a konfigurace, která se použijí při testování a zpracování modelování pro velké podniky. Tyto pokyny vám pomohou nastavit základní očekávání výkonu systému pro navrhované velikosti hardwaru.

### <a name="feature-intervals-settings"></a>Nastavení intervalů funkcí 
Většina testování by měla pro klíčové cykly v systému používat výchozí intervaly. Například testování inventáře hardwaru probíhá jednou za týden s větším než výchozím souborem *. mof* . Některé opakující se intervaly funkcí, zejména cykly inventáře hardwaru a softwaru, můžou mít výrazný vliv na výkonnostní charakteristiky prostředí. Prostředí, která umožňují agresivní výchozí intervaly pro shromažďování dat, potřebují v přímém poměru k navýšení v aktivitě výrazně naměnit velikost hardwaru. Řekněme například, že máte 25 000 klientů pro stolní počítače a chcete shromáždit inventář hardwaru dvakrát, než je výchozí interval. Měli byste začít změnou velikosti hardwaru webu, jako by byl 50 000 klientů.

### <a name="objects"></a>Objekty 
Testy by měly používat *horní průměr* objektů, které v systému obvykle používají velké podniky. Typické hodnoty jsou tisíce kolekcí a aplikací, které jsou nasazeny na stovky tisíc uživatelů nebo systémů. Testy by měly běžet souběžně na *všech* objektech v systému v těchto omezeních. Mnoho zákazníků využívá několik funkcí, ale obecně nepoužívá všechny funkce produktu v těchto horních limitech. Testování se všemi funkcemi produktu pomáhá zajistit nejlepší možný výkon v celém systému a umožňuje použití vyrovnávací paměti pro funkce, které můžou někteří zákazníci použít nad průměrem. 

### <a name="loads"></a>Zaveden 
Testy by měly být spuštěny na více než standardním *průměrném denním* zatížení, a to díky simulacím, které generují požadavky špičky využití systému. Jedním z příkladů je simulace aktualizace úterý uvádění, abyste měli jistotu, že systém může vracet data o kompatibilitě aktualizací během těchto dní aktivity špičky. Dalším příkladem je simulace aktivity webu během rozšíření šíření malwaru, aby bylo zajištěno včasné oznámení a reakce. I když se nasazené počítače o Doporučené velikosti můžou v kterémkoli dni použít jako nepoužitelné, pro extrémní situace je potřeba použít nějaké vyrovnávací paměti pro zpracování.

### <a name="configurations"></a>Konfigurace
Spusťte testování na řadě fyzického, Hyper-V a hardwaru Azure s kombinací podporovaných operačních systémů a SQL Server verzí. Vždy ověřte nejhorší případy pro podporovanou konfiguraci. Obecně platí, že technologie Hyper-V a Azure vrátí srovnatelné výsledky výkonu na ekvivalentní fyzický hardware, když se nakonfiguruje podobně. Novější serverové operační systémy mají za následek stejně nebo lepší i lepší, než starší podporované serverové operační systémy. I když všechny podporované platformy splňují minimální požadavky, obvykle nejnovější verze podpůrných produktů, jako je Windows a SQL, ještě lepší výkon. 

Největší variace pochází z používaných SQL Server verzí. Další informace o SQL Server verzích najdete v tématu [jakou verzi SQL mám spustit?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Klíčové determinanty výkonu

Můžete testovat a měřit Configuration Manager výkon pomocí různých nastavení, a to různými způsoby a v různých velikostech lokality. Následující nastavení a objekty můžou významně ovlivnit výkon. Nezapomeňte je zvážit při testování a modelování výkonu ve vašem prostředí.

> [!CAUTION]
> I když některé aspekty Configuration Manager mají oficiální maximum nebo omezení uživatelského rozhraní, které brání nadměrnému využití, může být překročení těchto pokynů pro výkon webu významné nepříznivé účinky. Překročení doporučené úrovně nebo ignorování pokynů pro změnu velikosti obvykle vyžaduje větší hardware a může způsobit, že vaše prostředí nebude možné udržovat, dokud neomezíte četnost nebo počet různých objektů.

### <a name="hardware-inventory"></a>Inventář hardwaru
Chcete-li otestovat výkon směrného plánu, nastavte kolekci inventáře hardwaru do jednoho týdne s výchozí velikostí souboru *. mof* a přibližně 20% dodatečných vlastností. Nepovolujte všechny vlastnosti a Shromážděte jenom vlastnosti, které skutečně potřebujete. Věnujte zvláštní pozornost při shromažďování vlastností, jako je dostupná virtuální paměť, která se *vždycky* mění se *všemi* cykly inventarizace. Shromažďování těchto vlastností může způsobit nadměrné změny všech cyklů inventarizace od každého klienta.

### <a name="software-inventory"></a>Inventář softwaru
Chcete-li otestovat výkon směrného plánu, nastavte shromažďování inventáře softwaru na jednou týdně a pouze informace o *produktu* . Shromažďování mnoha souborů může být významným kmenem systému inventáře. Vyhněte se zadávání filtrů, které by mohly ukončit shromažďování tisíců souborů napříč mnoha klienty, jako je * \*například. exe* nebo * \*. dll*.

### <a name="collections"></a>Kolekce
Základní testování výkonu může zahrnovat několik tisíc kolekcí s různými nastaveními rozsahu, velikosti, složitosti a aktualizací. Výkon webu není přímou funkcí Sheer počtu kolekcí v lokalitě. Výkon je zároveň meziproduktem složitá složitost dotazů, úplné a přírůstkové aktualizace a frekvence změn, závislosti mezi kolekcemi a počty klientů v kolekcích.

Pokud je to možné, minimalizujte kolekce, které mají nákladné nebo složité dotazy dynamického pravidla. Pro kolekce, které vyžadují tyto typy pravidel, nastavte příslušné intervaly aktualizací a časy aktualizace, aby se minimalizoval dopad opakovaného vyhodnocení kolekce v systému. Můžete například aktualizovat o půlnoci místo 8:00.

Povolení přírůstkových aktualizací v kolekcích zajišťuje rychlé a včasné aktualizace členství v kolekci. I když jsou přírůstkové aktualizace efektivní, jsou stále zatíženy systémem. Vyvážení frekvence změn, které předpokládáte, s potřebou pro aktualizace členství téměř v reálném čase. Řekněme například, že v členech kolekce očekáváte těžké změny, ale nevyžadujete aktualizace členství téměř v reálném čase. Je efektivnější a přináší méně zátěž v systému, aby se kolekce aktualizovala s plánovanou úplnou aktualizací v určitém intervalu, než když chcete povolit přírůstkové aktualizace. 

Pokud povolíte přírůstkové aktualizace, omezte všechny plánované úplné aktualizace na stejné kolekce. Jsou jenom metodou záložního vyhodnocování, protože přírůstkové aktualizace by měly udržovat členství v kolekci téměř v reálném čase. [Osvědčené postupy pro kolekce](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) nástroje doporučí maximální počet celkových kolekcí pro přírůstkové aktualizace, ale jak je uvedeno v článku, vaše prostředí se může lišit v závislosti na mnoha faktorech.

Kolekce s přímými pravidly členství a s omezenou kolekcí, která neprovádí přírůstkové aktualizace, nepotřebuje naplánované úplné aktualizace. Zakáže aktualizace plánů pro tyto typy kolekcí, aby nedocházelo k zbytečnému zatížení systému. Pokud omezující kolekce používá přírůstkové aktualizace, kolekce s přímým pravidlem členství nemusí aktualizace členství odrážet po dobu až 24 hodin nebo dokud nebude provedena plánovaná aktualizace.

I když se nejedná o osvědčený postup, některé organizace vytvářejí stovky nebo dokonce tisíce kolekcí jako součást různých obchodních procesů. Pokud k vytváření kolekcí používáte automatizaci, je důležité, abyste správně povolili všechny potřebné přírůstkové aktualizace. Minimalizujte a rozšíříte všechny plány plné aktualizace, abyste se vyhnuli aktivním skvrnám při vyhodnocování shromažďování během jednoho časového období. Navažte pravidelný proces výmazu dat, který odstraní nepoužívané kolekce, zejména pokud automaticky vytvoříte kolekce, které už po nějakou dobu nepotřebujete.

Pamatujte, že Configuration Manager vytvoří zásady pro všechny objekty ve vašich kolekcích, když cílíte na úlohy, jako jsou nasazení. Změny členství, ať už prostřednictvím plánované aktualizace nebo přírůstkové aktualizace, můžou vytvořit spoustu dalších prací pro celý systém. Nejnovější aktuální sestavení větve mají speciální optimalizace zásad pro kolekce všechny systémy a všichni uživatelé. Při cílení na celý podnik použijte předdefinované kolekce místo klonování těchto integrovaných kolekcí.

Chcete-li prozkoumat výkon kolekce ještě hlouběji, můžete použít nástroj CEViewer (Collection Evaluation Viewer) v sadě [Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012).

### <a name="discovery-methods"></a>Metody zjišťování
V případě testování výkonnosti směrného plánu spouštějte metody zjišťování založené na serveru jednou za týden a povolíte zjišťování rozdílů, aby data zůstala v průběhu týdne v čerstvém stavu. Testy by měly zjistit množství objektu úměrné simulované podnikové velikosti. Test standardních hodnot výkonu pro zjišťování prezenčního signálu by se měl spustit taky jednou týdně.

Data zjišťování jsou globální data. Běžný problém související s výkonem je nesprávně konfigurovat metody zjišťování na základě serveru v hierarchii, což způsobuje duplicitní zjišťování stejných prostředků z několika primárních lokalit. Pečlivě nakonfigurujte metody zjišťování pro optimalizaci komunikace s cílovou službou, jako jsou řadiče domény služby Active Directory, a zamezit tak duplicitě stejného rozsahu zjišťování na několika primárních lokalitách.

## <a name="general-sizing-guidelines"></a>Obecné pokyny pro změnu velikosti 

V závislosti na předchozí [metodologii testování výkonu](#performance-test-methodology)následující tabulka obsahuje obecné pokyny pro *minimální* požadavky na hardware pro konkrétní počty spravovaných klientů. Tyto hodnoty by měly všem zákazníkům, kteří mají zadaný počet klientů, zpracovávat objekty dostatečně rychle a spravovat tak určenou lokalitu. Výpočetní výkon se v každém roce stále snižuje a některé z následujících požadavků jsou malé z pohledu na hardwarové konfigurace moderních serverů. Hardware, který přesáhne následující pokyny, vylepší výkon pro weby, které vyžadují další výpočetní výkon, nebo speciální vzorce používání produktů. 

| Desktopové klienty  | Typ nebo role webu  | Jádra<sup>1</sup>   | Paměť (GB)   | Přidělení paměti SQL  | IOPS: Doručená pošta<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Požadované místo pro úložiště (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Role primárního serveru nebo certifikační autority s databází lokality na stejném serveru   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25k  | Primární nebo CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | Vzdálený SQL                                                  | 4   | 16  | 70 % |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50 tis  | Role primárního serveru nebo certifikační autority s databází lokality na stejném serveru   | 8   | 32  | 70 % | 1200 | 2800 | 600  |
| 50 tis  | Primární nebo CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | Vzdálený SQL                                                  | 8   | 24  | 70 % |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100 tisíc | Role primárního serveru nebo certifikační autority s databází lokality na stejném serveru   | 12  | 64  | 70 % | 1200 | 5000 | 1100 |
| 100 tisíc | Primární nebo CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | Vzdálený SQL                                                  | 12  | 48  | 80 % |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Role primárního serveru nebo certifikační autority s databází lokality na stejném serveru   | 16  | 96  | 70 % | 1800 | 7400 | 1600 |
| 150k | Primární nebo CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | Vzdálený SQL                                       | 16  | 72   | 90 % |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | Role CAS s databázovým serverem na stejném serveru   | 20+ | 128 + | 80 % | 1800 + | 9 000 +   | 5 000 + |
| 700k | CAS                                              | 8 +  | 16+  |     | 1800 + |         | 500 +  |
|      | Vzdálený SQL                                       | 16+ | 96 +  | 90 % |       | 9 000 +   | 4500 + |
|      |                                                             |     |     |     |      |      |      |
| 5k   | Sekundární lokalita                                   | 4   | 8    |     | 500   | -       | 200   |
| /min.  | Sekundární lokalita                                   | 8   | 16   |     | 500   | -       | 300   |

**Poznámky**

1. **Jádra**: Configuration Manager provádí mnoho souběžných procesů, takže potřebuje určitý minimální počet jader procesoru pro různé velikosti lokalit. I když jsou jádra rychlejší a každý rok je důležité zajistit, aby určitý minimální počet jader fungoval paralelně. Obecně platí, že každý procesor na úrovni serveru vyprodukovaný po 2015 splňuje základní požadavky na výkon pro jádra uvedená v tabulce. Configuration Manager využívá výhod dalších jader nad rámec těchto doporučení, ale obecně platí, že když máte minimální navrhovaná jádra, měli byste určit prioritu investic prostředků procesoru, abyste zvýšili rychlost stávajících jader, a ne přidávat více, pomalejších jader. Například Configuration Manager bude lépe provádět úlohy zpracování klíčů s 16 rychlými jádry než 24 pomalejšími jádry za předpokladu, že jsou k dispozici dostatečný počet dalších systémových prostředků, jako je například disk IOPS.
   
   Vztah mezi jádry a pamětí je také důležitý. Obecně platí, že méně než 3-4 GB paměti RAM na jádro snižuje celkovou schopnost zpracování na SQL serverech. Pokud je SQL společně umístěn v součástech webového serveru, budete potřebovat více paměti RAM na jádro.
   
   > [!NOTE]
   > Všechna testování nastaví schémata napájení počítače tak, aby umožňovala maximální nároky na výkon procesoru a výkon.
   
2. **IOPS: složky Doručená pošta a IOPS: SQL** odkazuje na IOPS nutné pro Configuration Manager a logické jednotky SQL. Sloupec **IOPS: inboxy** zobrazuje požadavky IOPS pro logickou jednotku, kde se nacházejí adresáře doručené pošty Configuration Manager. Sloupec **IOPS: SQL** zobrazuje celkový počet IOPS potřebných pro logické jednotky, které používají různé soubory SQL. Tyto sloupce se liší, protože tyto dvě jednotky by měly mít jiné formátování. Další informace a příklady navrhovaných konfigurací disků SQL a osvědčených postupů pro soubory, včetně podrobností o rozdělování souborů mezi více svazků, najdete v tématu [Nejčastější dotazy týkající se velikosti a výkonu lokality](../../understand/site-size-performance-faq.md).
   
   Oba tyto sloupce IOPS používají data z oboru standardní nástroj *DiskSpd*. Pokyny k duplikaci těchto měření najdete v tématu [Postup měření výkonu disku](#how-to-measure-disk-performance) . Obecně platí, že jakmile budete splňovat základní požadavky na procesor a paměť, bude mít podsystém úložiště největší dopad na výkon webu a vylepšení, která zde budou mít Payback investici.
   
3.  **Požadované místo pro úložiště:** Tyto hodnoty reálného světa se mohou lišit od dalších dokumentovaných doporučení. Tato čísla poskytujeme jenom jako obecný návod. jednotlivé požadavky se můžou výrazně lišit. Pečlivě Naplánujte volné místo na disku před instalací lokality. Předpokládejme, že některé množství tohoto úložiště zůstává ve většině případů volné místo na disku. Tento prostor vyrovnávací paměti můžete použít ve scénáři obnovení nebo pro scénáře upgradu, které potřebují volné místo na disku pro rozšíření instalačního balíčku. Vaše lokalita může vyžadovat další úložiště pro velké objemy sběru dat, delší dobu uchovávání dat a velké množství obsahu distribuce softwaru. Tyto položky můžete také ukládat na samostatné svazky s nižší propustností.

## <a name="how-to-measure-disk-performance"></a>Měření výkonu disku 

K poskytnutí standardních návrhů pro vstupně-výstupní operace, které vyžadují různá Configuration Manager prostředí, můžete použít standardní nástroj *DiskSpd* . I když není vyčerpávající, následující kroky testu a příkazový řádek poskytují jednoduchý a reprodukovatelný způsob, jak odhadnout propustnost subsystému disku na serveru. Výsledky můžete porovnat s minimálními doporučenými IOPS v tabulce [pokynů pro obecné změny velikosti](#general-sizing-guidelines) . 

V tématu [Příklady konfigurací disků](#example-disk-configurations) pro výsledky testů z nejrůznějších hardwarových konfigurací v testovacích prostředích. Data můžete použít pro přibližný počáteční bod při navrhování subsystému úložiště pro nové prostředí od začátku.

### <a name="to-test-disk-iops"></a>Testování IOPS disku  
1. Stáhněte si nástroj *DiskSpd* zde: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Ujistěte se, že máte k dispozici alespoň 100 GB volného místa na disku. Zakažte všechny aplikace, které by mohly narušovat nebo způsobit dodatečné zatížení disku, jako je například aktivní antivirová kontrola adresáře, SQL nebo SMSExec.
   
1. Spusťte *DiskSpd* z příkazového řádku se zvýšenými oprávněními. 
   
   Pro svazek, který chcete testovat, proveďte dvě spuštění nástroje v sekvenci. První test provádí pro jednu minutu operace náhodného zápisu o velikosti 64 KB. Tento test zajišťuje načítání mezipaměti řadiče a přidělení místa na disku pro případ, že se svazek dynamicky rozšiřuje. Zahodí výsledky prvního testu. Druhý test by měl *bezprostředně* následovat po prvním testu a provádět stejné zatížení po dobu pěti minut.
   
   K otestování svazku G:\\ použijte například následující konkrétní příkazové řádky.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Zkontrolujte výstup z druhého testu a vyhledejte celkový počet vstupně **-výstupních operací** na sloupci s. V následujícím příkladu jsou celkový počet vstupně-výstupních operací **3929,18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Příklady konfigurací disků

V následujících tabulkách jsou uvedeny výsledky spuštění testovacích kroků v tématu [Postup měření výkonu disku](#how-to-measure-disk-performance) pomocí různých konfigurací testovací laboratoře. Tato data použijte pro *hrubou* počáteční bod při navrhování subsystému úložiště pro nové prostředí od začátku. 

### <a name="physical-machines-and-hyper-v"></a>Fyzické počítače a technologie Hyper-V 
Hardware vždy vylepšuje. Očekává novější generace hardwaru a různých hardwarových kombinací, jako jsou SSD a San, aby překročily níže uvedený výkon. Tyto výsledky představují základní výchozí bod, který je potřeba vzít v úvahu při navrhování serveru nebo diskuze s dodavatelem hardwaru.

V následující tabulce jsou uvedeny výsledky testů napříč různými subsystémy disku, včetně diskových jednotek SSD a SSD, v různých konfiguracích testovacích laboratoří. Všechny konfigurace naformátují disky s 64 KB clusterů a připojují je k řadiči disků podnikové třídy. Kromě počtu disků RAID Array mají každý z nich aspoň jeden disk, který je k dispozici.

| Typ disku   | Počet disků, včetně náhradního disku + 1 | ČLEN     | Měřený počet IOPS  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15 000 SAS          | 2                                                  |           1   | 620           |
| 15 000 SAS          | 4                                                  |           10  | 1206          |
| 15 000 SAS          | 6                                                  |           10  | 1751          |
| 15 000 SAS          | 8                                                  |           10  | 2322          |
| 15 000 SAS          | 10                                                 |           10  | 2882          |
| 15 000 SAS          | 12                                                 |           10  | 3476          |
| 15 000 SAS          | 16                                                 |           10  | 4236          |
| 15 000 SAS          | 20                                                 |           10  | 5148          |
| 15 000 SAS          | 30                                                 |           10  | 7398          |
| 15 000 SAS          | 40                                                 |           10  | 9913          |
| SSD SATA         | 2                                                  |           1   | 3300          |
| SSD SATA         | 4                                                  |           10  | 5542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15607         |

Jedná se o zařízení, které se používá v příkladu. Tyto informace nejsou doporučením pro žádný konkrétní hardwarový model nebo výrobce. 

| Typ disku    | Model      | Řadič RAID | Paměť a konfigurace mezipaměti |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15 000 ot./min. SAS HD    | HP EH0300JDYTH  | P822 Smart Array     | 2 GB, 20% čtení/80% zápis           |
| SSD SATA          | MK0200GCTYV ATA | P420i Smart Array    | 1 GB, 20% čtení/80% zápisu           |
| SSD SAS           | HP MO0800 JEFPB | P420i Smart Array    | 1 GB, 20% čtení/80% zápisu           |

### <a name="azure-machine-and-disk-performance"></a>Výkon počítače a disku Azure 
Výkon disku Azure závisí na několika faktorech, třeba na velikosti virtuálního počítače Azure, na počtu a typu disků, které používá. Azure také neustále přidává nové typy počítačů a rychlosti disků, které se liší od následujícího grafu. Další informace o Configuration Manager spuštěné v Azure a další informace o porozumění vstupně-výstupních operacích disků v Azure najdete v článku [Configuration Manager na nejčastějších dotazech k Azure](../../understand/configuration-manager-on-azure.md).

Všechny disky jsou formátovány na velikost clusteru NTFS 64 a řádky s více než jedním diskem se nakonfigurují jako prokládané svazky pomocí nástroje Správa disků systému Windows.

| Virtuální počítač Azure| Disk Azure| Počet disků | Dostupné místo | Měřený počet IOPS   | Faktor omezení   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Velikost virtuálního počítače Azure   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Velikost virtuálního počítače Azure   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Velikost virtuálního počítače Azure   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Velikost virtuálního počítače Azure   |
| **DS3/DS12/F4S ÚROVNĚ**                          | P20                     | 1                   | 512 MB                    | 1994  | Velikost virtuálního počítače Azure   |
| **DS3/DS12/F4S ÚROVNĚ**                          | P20                     | 2                   | 1024 MB                   | 1992  | Velikost virtuálního počítače Azure   |
| **DS3/DS12/F4S ÚROVNĚ**                          | P30                     | 1                   | 1024 MB                   | 1993  | Velikost virtuálního počítače Azure   |
| **DS3/DS12/F4S ÚROVNĚ**                          | P30                     | 2                   | 2048 MB                   | 1992  | Velikost virtuálního počítače Azure   |
| **DS4/DS13/F8S ÚROVNĚ**                          | P20                     | 1                   | 512 MB                    | 2334  | P20 disk        |
| **DS4/DS13/F8S ÚROVNĚ**                          | P20                     | 2                   | 1024 MB                   | 3984  | Velikost virtuálního počítače Azure   |
| **DS4/DS13/F8S ÚROVNĚ**                          | P20                     | 3                   | 1536 MB                   | 3984  | Velikost virtuálního počítače Azure   |
| **DS4/DS13/F8S ÚROVNĚ**                          | P30                     | 1                   | 1024 MB                   | 3112  | P30 disk        |
| **DS4/DS13/F8S ÚROVNĚ**                          | P30                     | 2                   | 2048 MB                   | 3984  | Velikost virtuálního počítače Azure   |
| **DS4/DS13/F8S ÚROVNĚ**                          | P30                     | 3                   | 3072 MB                   | 3996  | Velikost virtuálního počítače Azure   |
| **DS5/DS14/F16S ÚROVNĚ**                         | P20                     | 1                   | 512 MB                    | 2335  | P20 disk        |
| **DS5/DS14/F16S ÚROVNĚ**                         | P20                     | 2                   | 1024 MB                   | 4639  | P20 disk        |
| **DS5/DS14/F16S ÚROVNĚ**                         | P20                     | 3                   | 1536 MB                   | 6913  | P20 disk        |
| **DS5/DS14/F16S ÚROVNĚ**                         | P20                     | 4                   | 2048 MB                   | 7966  | Velikost virtuálního počítače Azure   |
| **DS5/DS14/F16S ÚROVNĚ**                         | P30                     | 1                   | 1024 MB                   | 3112  | P30 disk        |
| **DS5/DS14/F16S ÚROVNĚ**                         | P30                     | 2                   | 2048 MB                   | 6182  | P30 disk        |
| **DS5/DS14/F16S ÚROVNĚ**                         | P30                     | 3                   | 3072 MB                   | 7963  | Velikost virtuálního počítače Azure   |
| **DS5/DS14/F16S ÚROVNĚ**                         | P30                     | 4                   | 4096 MB                   | 7968  | Velikost virtuálního počítače Azure   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | P30 disk        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | P30 disk        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | P30 disk        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Velikost virtuálního počítače Azure   |

## <a name="see-also"></a>Viz také

- [Nejčastější dotazy týkající se velikosti a výkonu webu](../../understand/site-size-performance-faq.md)
- [Nejčastější dotazy k Configuration Manager v Azure](../../understand/configuration-manager-on-azure.md)
- [Dimenzování a škálování](size-and-scale-numbers.md)
- [Doporučený hardware](recommended-hardware.md)

