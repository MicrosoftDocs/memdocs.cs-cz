---
title: Replikace databáze
titleSuffix: Configuration Manager
description: Přečtěte si, jak Configuration Manager replikace databáze používá SQL Server k přenosu dat v hierarchii.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720195"
---
# <a name="database-replication"></a>Replikace databáze

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager replikace databáze používá SQL Server k přenosu dat. Tuto metodu používá ke sloučení změn v databázi lokality s informacemi z databáze v jiných lokalitách v hierarchii.

Všimněte si, že replikace databáze má následující body:

- Všechny weby sdílejí stejné informace.  

- Když nainstalujete lokalitu v hierarchii nástroje, Configuration Manager automaticky zahájí replikaci databáze mezi novou lokalitou a její nadřazenou lokalitou.  

- Po dokončení instalace lokality se automaticky spustí replikace databáze.  

Když přidáte novou lokalitu do hierarchie, Configuration Manager v nové lokalitě vytvoří obecnou databázi. Nadřazená lokalita vytvoří snímek relevantních dat ve své databázi. Poté přenese snímek do nové lokality pomocí [replikace na základě souborů](file-based-replication.md). Nová lokalita pak pomocí programu SQL Server hromadného kopírování (BCP) načte informace do místní kopie databáze Configuration Manager. Po načtení snímku každá lokalita provede replikaci databáze s ostatními lokalitami.  

Pokud chcete replikovat data mezi lokalitami, Configuration Manager používá vlastní replikační službu databáze. Replikační služba databáze používá SQL Server sledování změn k monitorování změn databáze místní lokality. Pak replikuje změny do jiných lokalit pomocí SQL Server Service Broker (SSB). Ve výchozím nastavení tento proces používá port TCP 4022.  


## <a name="replication-groups"></a>Replikační skupiny

Configuration Manager seskupuje data, která se replikují pomocí replikace databáze do různých replikačních skupin. Každá replikační skupina má samostatný, pevný plán replikace. Lokalita používá tento plán k určení, jak často replikuje změny v jiných lokalitách.  

Například změna konfigurace správy na základě rolí se rychle replikuje do ostatních lokalit. Tím se zajistí, že druhý web může tyto změny rychle vykonat. Změna konfigurace s nižší prioritou, například požadavek na instalaci nové sekundární lokality, je replikována s menší naléhavostí. Může trvat několik minut, než se nová žádost lokality dostane do cílové primární lokality.  


## <a name="settings"></a>Nastavení

Pro replikaci databáze můžete upravit následující nastavení:  

- **Odkazy replikace databáze**: Určuje, kdy konkrétní přenosy procházejí sítí.  

- **Distribuovaná zobrazení**: Pokud se webový server Centrální správy (CAS) žádá o vybraná data lokality, může získat přístup k datům přímo z databáze v podřízené primární lokalitě.  

- **Plány**: Určete, kdy se má odkaz replikace používat, a když se různé typy dat lokality replikují.  

- **Shrnutí**: Změna nastavení shrnutí dat o síťovém provozu, který projde odkazy replikace. Ve výchozím nastavení se sumarizace provádí každých 15 minut. Používá se v sestavách pro replikaci databáze.  

- **Prahové hodnoty replikace databáze**: definuje, kdy lokalita ohlásí negradované nebo neúspěšné. Můžete taky nakonfigurovat, kdy Configuration Manager vyvolává výstrahy týkající se replikačních odkazů, které mají stav snížené nebo neúspěšné.  


## <a name="types-of-data"></a>Typy dat

Configuration Manager primárně klasifikuje data, která replikuje, jako *globální data* nebo *data lokality*. Když dojde k replikaci databáze, lokalita přenáší změny globálních dat a dat lokality přes odkaz replikace databáze. Globální data se replikují do nadřazené nebo podřízené lokality. Data lokality se replikují pouze do nadřazené lokality. Třetí datový typ, *místní data*, se nereplikují do ostatních lokalit. Místní data jsou informace, které ostatní lokality nevyžadují.  

### <a name="global-data"></a>Globální data

Globální data jsou objekty vytvořené správci, které se replikují do všech lokalit v celé hierarchii. Sekundární lokality přijímají pouze podmnožinu globálních dat, jako jsou globální proxy data. Globální data se vytvářejí v primárních certifikačních autoritách a v primárních lokalitách. Tento typ zahrnuje následující data:

- Nasazení softwaru
- Aktualizace softwaru
- Definice kolekce
- Obory zabezpečení správy na základě rolí

### <a name="site-data"></a>Data lokality

Data lokality jsou provozní informace vytvořené Configuration Manager primárními lokalitami a jejich přiřazenými klienty. Data lokality se replikují do certifikačních autorit, ale ne do jiných primárních lokalit. Data lokality jsou viditelná pouze v certifikačních autoritách a v primární lokalitě, kde data pocházejí. Data lokality můžete upravovat jenom v primární lokalitě, na které jste ji vytvořili. Tento typ zahrnuje následující data:

- Inventář hardwaru
- Stavové zprávy
- Výstrahy
- Výsledky kolekcí založených na dotazech

Všechna data lokality se replikují do certifikačních autorit. CAS provádí správu a vytváření sestav pro celou hierarchii lokality.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a>Odkazy replikace databáze

Když nainstalujete novou lokalitu v hierarchii, Configuration Manager automaticky vytvoří propojení replikace databáze mezi nadřazenou a novou lokalitou. Vytvoří se jediné propojení pro propojení těchto dvou lokalit.  

Chcete-li řídit přenos dat napříč replikačním propojením, změňte nastavení pro jednotlivé odkazy. Každé replikační připojení podporuje samostatné konfigurace. Každý odkaz replikace databáze zahrnuje následující ovládací prvky:  

- Zastavte replikaci vybraných dat lokality z primární lokality do certifikačních autorit. Tato akce způsobí, že CAS budou přistupovat k těmto datům přímo z databáze primární lokality.  

- Naplánujte vybraná data lokality pro přenos z podřízené primární lokality do certifikačních autorit.

- Definujte nastavení, které určuje, kdy má připojení replikace databáze stav snížené nebo neúspěšné.

- Určete, kdy se mají vyvolat výstrahy pro odkaz na nezdařenou replikaci.

- Určete, jak často Configuration Manager shrnuje data týkající se provozu replikace, který používá odkaz replikace. Tato data se používají v sestavách.

Chcete-li nakonfigurovat odkaz replikace databáze, v konzole nástroje Configuration Manager přejít do pracovního prostoru **monitorování** . Vyberte uzel **replikace databáze** a upravte vlastnosti odkazu. Tento uzel je také v pracovním prostoru **Správa** v uzlu **Konfigurace hierarchie** . Upravte odkaz replikace buď z nadřazené lokality, nebo z podřízené lokality odkazu replikace.  

> [!TIP]  
> Propojení replikace databáze můžete upravit v uzlu **Replikace databáze** v libovolném pracovním prostoru. Pokud ale použijete uzel **replikace databáze** v pracovním prostoru **sledování** , můžete také zobrazit stav replikace databáze. Poskytuje také přístup k nástroji [analyzátor propojení replikace](../../servers/manage/monitor-replication.md#BKMK_RLA) . Pomocí tohoto nástroje můžete prozkoumat problémy s replikací databáze.  

Další informace o tom, jak nakonfigurovat replikační propojení, najdete v tématu [ovládací prvky replikace databáze lokality](#BKMK_DBRepControls). Další informace o tom, jak monitorovat replikaci, najdete v tématu [monitorování replikace databáze](../../servers/manage/monitor-replication.md).  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a>Distribuovaná zobrazení  

Když v distribuovaných zobrazeních vydáte požadavek na CAS pro vybraná data lokality, přímý přístup k databázi v podřízené primární lokalitě. Tento přímý přístup nahrazuje nutnost replikovat data lokality z primární lokality do certifikačních autorit. Vzhledem k tomu, že je každé připojení replikace nezávislé na dalších replikačních odkazech, můžete použít distribuovaná zobrazení na odkazech replikace, které vyberete. Nemůžete použít distribuovaná zobrazení mezi primární lokalitou a sekundární lokalitou.  

Distribuovaná zobrazení poskytují následující výhody:  

- Snižte zatížení procesoru při zpracování změn databáze v certifikačních autoritách a primárních lokalitách.

- Snížení množství dat, která se přenášejí přes síť do certifikačních autorit

- Zlepšení výkonu SQL Server, který je hostitelem databáze CAS

- Snižte místo na disku, které používá databáze CAS.

Zvažte použití distribuovaných zobrazení, když je primární lokalita úzce umístěna na certifikačních autoritách v síti, tyto dvě lokality jsou vždy zapnuté a vždy připojené. Distribuovaná zobrazení nahrazují replikaci vybraných dat mezi lokalitami přímými připojeními mezi servery SQL Server v každé lokalitě. CAS vytvoří přímé připojení pokaždé, když si vyžádáte tato data.

Lokalita požaduje data distribuovaného zobrazení v následujících ukázkových scénářích:

- Při spuštění sestav nebo dotazů
- Při zobrazení informací v Průzkumník prostředků
- Vyhodnocení kolekce pro kolekce, které obsahují pravidla založená na datech webu

Ve výchozím nastavení jsou distribuovaná zobrazení pro každý odkaz replikace vypnutá. Když zapnete distribuovaná zobrazení, vyberte data lokality, která se nebudou replikovat do certifikačních autorit v rámci tohoto propojení. CAS přistupuje k těmto datům přímo z databáze podřízené primární lokality, která odkaz sdílí. Můžete provést konfiguraci následujících typů dat lokality pro distribuovaná zobrazení:  

- Data **inventáře hardwaru** od klientů
- **Inventář softwaru a data monitorování míry využívání softwaru** od klientů
- **Stavové zprávy** od klientů, primární lokalita a všechny sekundární lokality

Při zobrazení dat v konzole Configuration Manager nebo v sestavách jsou distribuovaná zobrazení neviditelná pro vás. Když vyžádáte data, která jsou povolená pro distribuovaná zobrazení, Server databáze lokality CAS přímo přistupuje k databázi podřízené primární lokality, aby načetla informace.

Například použijete konzolu Configuration Manager připojenou k certifikační autoritě. Vyžádáte informace o inventáři hardwaru ze dvou primárních lokalit: ABC a XYZ. Byl povolen pouze inventář hardwaru pro distribuovaná zobrazení v lokalitě ABC. CAS načte informace o inventáři pro klienty XYZ z vlastní databáze. CAS načte informace o inventáři pro klienty ABC přímo z databáze v lokalitě ABC. Tyto informace se zobrazí v konzole Configuration Manager nebo v sestavě bez identifikace zdroje.  

Pokud má odkaz replikace typ dat povolených pro distribuovaná zobrazení, podřízená primární lokalita tato data nereplikuje do certifikačních autorit. Pokud vypnete distribuovaná zobrazení pro určitý typ dat, podřízená primární lokalita obnoví normální replikaci dat do certifikačních autorit. Než budou tato data k dispozici na certifikačních autoritách, musí se replikační skupiny pro tato data znovu inicializovat mezi primární lokalitou a certifikační autoritou. Po odinstalaci primární lokality, která má zapnutá distribuovaná zobrazení, musí certifikační autorita dokončit opětovnou inicializaci svých dat, aby bylo možné získat přístup k datům, která jste povolili pro distribuovaná zobrazení na certifikačních autoritách.  

> [!IMPORTANT]  
> Pokud používáte distribuovaná zobrazení na jakémkoli propojení replikace v hierarchii lokality nástroje, před odinstalováním libovolné primární lokality vypněte distribuovaná zobrazení pro všechny odkazy replikace. Další informace najdete v tématu [odinstalace primární lokality, která používá distribuovaná zobrazení](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Předpoklady a omezení distribuovaných zobrazení  

- Pro propojení replikace mezi certifikačními autoritami a primární lokalitou používejte jenom distribuovaná zobrazení.

- Certifikační autority musí používat edici SQL Server Enterprise. Primární lokalita nemá tento požadavek.

- Certifikační autority můžou mít jenom jednu instanci poskytovatele serveru SMS. Nainstalujte tuto jednu instanci na server databáze lokality. Tato konfigurace podporuje ověřování pomocí protokolu Kerberos. SQL Server v CAS vyžaduje pro přístup k SQL serveru v podřízené primární lokalitě protokol Kerberos. Pro poskytovatele serveru SMS v podřízené primární lokalitě nejsou žádná omezení.

- V certifikačních autoritách můžete nainstalovat pouze jeden bod služby Reporting Services. Nainstalujte SQL Server Reporting Services na serveru databáze lokality. Tato konfigurace podporuje ověřování pomocí protokolu Kerberos. SQL Server v CAS vyžaduje pro přístup k SQL serveru v podřízené primární lokalitě protokol Kerberos.

- Databázi lokality nelze hostovat na [SQL serverm clusteru](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- Ve verzi 1902 a starší nemůžete hostovat databázi lokality ve [skupině dostupnosti Always on SQL Server](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md). Pro podporu této konfigurace aktualizujte na verzi 1906 nebo novější.<!-- SCCMDocs-pr#3792 -->

- Počítačový účet serveru databáze CAS vyžaduje oprávnění **ke čtení** databáze primární lokality.

> [!IMPORTANT]  
> Distribuovaná zobrazení a [plány](#BKMK_schedules) , kdy se můžou data replikovat, se vzájemně vylučují pro odkaz replikace databáze.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a>Plánování přenosů dat lokality

Aby bylo možné řídit šířku pásma sítě, která se používá k replikaci dat lokality z podřízené primární lokality do certifikačních autorit, naplánujte, kdy se používá odkaz replikace. Pak určete, kdy se různé typy dat lokality mají replikovat. Můžete ovládat, kdy má primární lokalita replikovat stavové zprávy, inventář a data měření. Odkazy replikace databáze ze sekundárních lokalit nepodporují plány pro data lokality. Nemůžete naplánovat přenos globálních dat.  

Při konfiguraci plánu odkazu replikace databáze můžete omezit přenos vybraných dat lokality z primární lokality do certifikačních autorit. Můžete také nakonfigurovat různé časy pro replikaci různých typů dat lokality.  

> [!IMPORTANT]  
> [Distribuovaná zobrazení](#bkmk_distviews) a plány, kdy se můžou data replikovat, jsou vzájemně exkluzivní konfigurace pro replikační připojení databáze.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a>Shrnutí provozu  

Každá lokalita pravidelně sumarizuje data o síťovém provozu, který prochází odkazy replikace databáze pro danou lokalitu. Lokalita používá sumarizovaná data v sestavách pro replikaci databáze. Obě lokality odkazu replikace sumarizují síťový provoz, který překračuje odkaz replikace. Server databáze lokality shrnuje data. Po sumarizaci dat se informace replikují do jiných lokalit jako globální data.  

Ve výchozím nastavení se sumarizace provádí každých 15 minut. Chcete-li upravit Četnost sumarizace síťového provozu, ve vlastnostech odkazu replikace databáze upravte **interval sumarizace**. Frekvence sumarizace ovlivňuje informace, které zobrazíte v sestavách o replikaci databáze. Můžete zvolit interval od 5 do 60 minut. Pokud četnost sumarizace zvýšíte, zvýšíte tím i zatížení SQL Serveru na každé lokalitě odkazu replikace.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a>Prahové hodnoty replikace databáze

Prahové hodnoty replikace databáze definují, když Configuration Manager hlásí stav odkazu replikace databáze buď Degradováno, nebo selhal. Ve výchozím nastavení nastaví propojení jako *omezené* , pokud se některé skupině replikací nepovede dokončit replikaci po dobu 12 po sobě jdoucích pokusů. Nastaví odkaz jako *neúspěšný* , pokud se některá replikační skupina nepovede replikovat během 24 po sobě jdoucích pokusů.  

Můžete zadat vlastní hodnoty pro snížený nebo neúspěšný stav. Pokud tyto hodnoty upravíte, můžete přesněji sledovat stav replikace databáze napříč odkazy.  

Nepovedlo se replikovat jednu nebo víc replikačních skupin, zatímco jiné replikační skupiny se budou dál replikovat. Naplánujte, abyste zkontrolovali stav replikace propojení při prvním generování sestav jako omezeného.

V následujících situacích zvažte úpravu hodnot opakování pro stav snížené nebo neúspěšného připojení:

- Existují opakované prodlevy pro určité replikační skupiny a jejich zpoždění nepředstavuje problém.

- Síťové propojení mezi lokalitami má nízkou dostupnou šířku pásma.

Pokud zvýšíte počet opakování, než lokalita nastaví odkaz na zhoršený nebo neúspěšný, můžete eliminovat falešná upozornění u známých problémů. Tato akce vám umožní přesněji sledovat stav odkazu.  

Pokud chcete zjistit, jak často k replikaci této skupiny dojde, zvažte interval synchronizace replikace pro každou skupinu replikace. **Interval synchronizace** pro replikační skupiny zobrazíte tak, že přejdete do pracovního prostoru **monitorování** v konzole Configuration Manager. V uzlu **replikace databáze** vyberte na kartě **Podrobnosti replikace** odkaz replikace.  

Další informace o sledování replikace databáze, včetně postupu zobrazení stavu replikace, najdete v tématu [monitorování replikace databáze](../../servers/manage/monitor-replication.md).  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a>Ovládací prvky replikace databáze lokality  

Chcete-li vám pořídit šířku pásma sítě použitou pro replikaci databáze, změňte nastavení pro každou databázi lokality. Nastavení platí pouze pro databázi lokality, ve které konfigurujete nastavení. Nastavení se vždycky použijí, když lokalita replikuje jakákoli data replikací databáze do jakékoli jiné lokality.  

Pro každou databázi lokality můžete upravit následující ovládací prvky replikace:  

- Port SSB  

- Doba, po kterou se má čekat, než selhání replikace aktivuje, aby se znovu inicializoval kopie databáze lokality  

- Komprimuje data, která lokalita replikuje. Pouze komprimuje data pro přenos mezi lokalitami a nikoli pro úložiště v databázi lokality v obou lokalitách.  

Chcete-li změnit nastavení pro ovládací prvky replikace databáze lokality, v konzole Configuration Manager v uzlu **replikace databáze** upravte vlastnosti databáze lokality. Tento uzel se zobrazí pod uzlem **Konfigurace hierarchie** v pracovním prostoru **Správa** a zobrazí se také v pracovním prostoru **monitorování** . Chcete-li upravit vlastnosti databáze lokality, vyberte odkaz replikace mezi lokalitami a pak otevřete vlastnosti **nadřazené databáze** nebo **vlastnosti podřízené databáze**.  

> [!TIP]  
> Konfiguraci ovládacích prvků replikace databáze můžete provést z uzlu **Replikace databáze** v libovolném pracovním prostoru. Pokud ale použijete uzel **replikace databáze** v pracovním prostoru **monitorování** , můžete si také zobrazit stav replikace databáze pro odkaz replikace a získat přístup k nástroji analyzátor propojení replikace, který vám umožní prozkoumat problémy s replikací.  


## <a name="see-also"></a>Viz také

[Monitorování replikace](../../servers/manage/monitor-replication.md)

[Řešení potíží s replikací SQL](../../servers/manage/replication/overview.md)
