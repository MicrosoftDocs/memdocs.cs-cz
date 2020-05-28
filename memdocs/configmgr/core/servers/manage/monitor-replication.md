---
title: Monitorování replikace databáze
titleSuffix: Configuration Manager
description: Naučte se monitorovat replikaci SQL Server v hierarchii Configuration Manager.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4a9ae791582911f91e5f76b841248ad5085d8170
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879822"
---
# <a name="monitor-database-replication"></a>Monitorování replikace databáze

*Platí pro: Configuration Manager (Current Branch)*

Sledujte podrobnosti o replikaci databáze pomocí uzlu **replikace databáze** v pracovním prostoru **monitorování** konzoly Configuration Manager. Můžete monitorovat stav replikačních propojení mezi lokalitami. Zobrazuje taky inicializaci a replikaci replikačních skupin pro lokalitu, ke které se připojujete.  

> [!TIP]  
> I když se uzel **replikace databáze** zobrazuje taky pod uzlem **Konfigurace hierarchie** v pracovním prostoru **Správa** , nemůžete zobrazit stav replikace pro odkazy replikace databáze z tohoto umístění.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Stav odkazů replikace  

Replikace databáze mezi lokalitami zahrnuje replikaci několika sad informací nazývaných *replikační skupiny*. Každá replikační skupina odesílá a přijímá data s různými prioritami. Ve výchozím nastavení nemůžete upravovat data obsažená v replikační skupině a četnost replikace.  

Když je odkaz replikace aktivní a jeho stav není neúspěšný nebo snížený, všechny skupiny se rychle replikují. Pokud se jedné nebo více skupinám nepodaří dokončit replikaci během očekávaného časového období, odkaz se zobrazí jako *snížený*. Degradované odkazy mohou i nadále fungovat, ale měli byste je monitorovat, abyste se ujistili, že se vrátí k aktivnímu stavu. Prozkoumejte je, abyste se ujistili, že nedochází k dalšímu snížení nebo selhání replikace.  

Pro každý odkaz replikace zadejte, kolikrát se neúspěšně replikovaná skupina opakuje. Po tomto počtu opakovaných pokusů lokalita nastaví stav propojení na hodnotu Degradováno nebo selhalo. I v případě, že je úspěšně replikována všechny kromě jedné skupiny, lokalita nastaví stav propojení na hodnotu Degradováno nebo selhání. Nastaví tento stav, protože jedna replikační skupina nedokáže dokončit replikaci v zadaném počtu pokusů. Další informace najdete v tématu [prahové hodnoty replikace databáze](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

Následující informace vám pomohou pochopit stav replikačních odkazů, které mohou vyžadovat další šetření:  

### <a name="link-is-active"></a>Odkaz je aktivní

Nebyly zjištěny žádné problémy a komunikace přes odkaz je aktuální.

I když je nadřazená lokalita aktualizována na novou verzi a zobrazí se stav propojení z podřízené lokality, stav odkazu se zobrazí jako aktivní. Až do té doby, než bude podřízená lokalita ve stejné verzi jako nadřazená lokalita, se po zobrazení stav odkazu zobrazí jako aktivní, pokud je zobrazený z nadřazené lokality. Při prohlížení z podřízené lokality se zobrazuje jako konfigurovaná.  

### <a name="link-is-degraded"></a>Odkaz je degradovaný

Replikace je funkční, avšak minimálně jeden objekt replikace nebo replikační skupina jsou zpožděny. Sledujte odkazy, které jsou v tomto stavu. Zkontrolujte informace z obou lokalit na odkazu pro indikaci, že odkaz může selhat.

Odkaz může též zobrazovat degradovaný stav, pokud lokalita, která přijímá replikovaná data, není schopna rychle data zapsat do databáze. K tomuto chování dochází při replikaci velkého objemu dat. Například nasadíte aktualizaci softwaru na velký počet počítačů. Nadřazený web na tomto odkazu může chvíli trvat, než se tento svazek replikovaných dat zpracuje. Výsledkem prodlevy při zpracování na nadřazeném webu je nastavení stavu propojení tak, aby se snížilo, dokud nebude možné úspěšně zpracovat nevyřízené položky dat.

### <a name="link-has-failed"></a>Odkaz se nezdařil

Replikace není funkční. Je možné, že odkaz replikace se může obnovit bez další akce. K prozkoumání a usnadnění nápravy replikace na tomto odkazu použijte Analyzátor propojení replikace (RLA).

Tento stav může také indikovat problém s fyzickou sítí mezi nadřazenou a podřízenou lokalitou na odkazu replikace.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a>Stav monitorování replikace

Pomocí uzlu **replikace databáze** v pracovním prostoru **monitorování** zobrazte stav odkazu replikace. Zobrazit podrobnosti o databázi v každé lokalitě na odkazu replikace. Jde taky zobrazit informace o replikačních skupinách. Chcete-li zobrazit tyto podrobnosti, vyberte odkaz replikace a pak vyberte příslušnou kartu pro stav replikace, který chcete zobrazit.

Následující části obsahují podrobné informace o různých kartách pro stav replikace:

### <a name="summary"></a>Souhrn

Zobrazení informací na nejvyšší úrovni o replikaci dat lokality a globálních dat mezi dvěma lokalitami na odkazu.  

Vyberte **Zobrazit sestavy pro historická data o provozu** a zobrazte sestavu s podrobnostmi o šířce pásma sítě, kterou používá replikace napříč odkazem.  

### <a name="parent-site"></a>Nadřazená lokalita

Pro nadřazenou lokalitu na odkazu replikace můžete zobrazit informace o databázi, které zahrnují:  

- Porty brány Firewall pro systém SQL Server  

- Volné místo na disku  

- Umístění souboru databáze  

- Certifikáty  

### <a name="child-site"></a>Podřízená lokalita

Pro podřízenou lokalitu na odkazu replikace můžete zobrazit informace o databázi, které zahrnují:  

- Porty brány Firewall pro systém SQL Server  

- Volné místo na disku  

- Umístění souboru databáze  

- Certifikáty  

### <a name="initialization-detail"></a>Informace o inicializaci

Zobrazí stav inicializace pro skupiny, které se replikují přes propojení. Tyto informace vám mohou pomoci zjistit, zda inicializace replikačních dat probíhá nebo se nezdařila.  

Tyto informace slouží k identifikaci, kdy se lokalita může nacházet v *režimu interoperability*. Režim interoperability je v případě, že na podřízené lokalitě není spuštěna stejná verze Configuration Manager jako nadřazená lokalita.  

### <a name="replication-detail"></a>Informace o replikaci

Zobrazte stav replikace pro každou skupinu, která se replikuje přes propojení. Tyto informace vám pomůžou identifikovat problémy nebo prodlevy při replikaci konkrétních dat. Může vám to usnadnit určení vhodných prahových hodnot replikace databáze pro tento odkaz. Další informace najdete v tématu [prahové hodnoty replikace databáze](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

> [!TIP]  
> Skupiny replikací dat lokality lze zaslat pouze z podřízené lokality do nadřazené lokality. Skupiny replikací globálních dat replikují v obou směrech.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a>Analyzátor propojení replikace

Configuration Manager zahrnuje **analyzátor propojení replikace** (RLA), které slouží k analýze a opravám potíží s replikací. Pokud dojde k selhání replikace, použijte RLA k nápravě chyb propojení. Je to také užitečné, když replikace přestane fungovat, ale web ji ještě neohlásil jako neúspěšnou.

K nápravě potíží s replikací mezi následujícími počítači v hierarchii použijte RLA:  

- Mezi serverem lokality a serverem databáze lokality  

- Mezi databázovým serverem lokality a databázovým serverem jiné lokality, jinak označované jako replikace mezi lokalitami  

> [!Note]  
> Směr nezáleží na selhání replikace.

Spusťte RLA buď v konzole Configuration Manager, nebo na příkazovém řádku:  

- Spuštění v konzole Configuration Manager: přejdete do pracovního prostoru **monitorování** a vyberete uzel **replikace databáze** . Vyberte odkaz replikace, který chcete analyzovat, a potom na pásu karet vyberte **analyzátor propojení replikace**.  

- Pro spuštění na příkazovém řádku zadejte následující příkaz:`%ProgramFiles(x86)%\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

    > [!IMPORTANT]
    > Počínaje verzí 1910 se tato cesta změnila na použití `Microsoft Endpoint Manager` složky. Ujistěte se, že nepoužíváte starší verzi souboru, která může existovat v jiné složce.

Když spustíte RLA, detekuje problémy pomocí řady diagnostických pravidel a kontrol. Zobrazíte problémy, které nástroj identifikuje. Pokud obsahuje pokyny k vyřešení problému, zobrazí se. Pokud RLA může problém automaticky vyřešit, zobrazí se vám tato možnost.

Po dokončení RLA uloží výsledky do následující sestavy založené na XML a souboru protokolu na ploše uživatele, který nástroj spouští:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA zastaví následující služby, zatímco vyřeší některé problémy. Po dokončení nápravy tyto služby restartuje:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Pokud se RLA nepovede dokončit nápravu, restartujte v případě potřeby tyto služby na serveru lokality.  

RLA zaznamená všechny akce šetření a nápravy, které poskytují další podrobnosti, které se v průvodci nezobrazí.  

### <a name="rla-prerequisites"></a>Požadavky na RLA

Účet, který použijete ke spuštění RLA, musí mít následující oprávnění:

- Oprávnění místního správce na každém počítači, který je součástí replikačního odkazu.

- Oprávnění správce systému pro každou databázi SQL Server, která je zahrnuta v odkazu replikace.  

> [!Note]  
> Účet nevyžaduje konkrétní Configuration Manager roli zabezpečení správy na základě rolí. Administrativní uživatel s přístupem k uzlu **replikace databáze** může spustit nástroj v konzole Configuration Manager. Správce systému, který má ke každému počítači dostatečná práva, může spustit nástroj z příkazového řádku.  

### <a name="rla-known-issue"></a>Známý problém s RLA

RLA vygeneruje chyby certifikátů SQL Server Service Broker (SSB) pro primární lokality, které se upgradovali z verze System Center 2012 Configuration Manager. Důvodem těchto potíží je změny v názvech certifikátů v Configuration Manager aktuální větev. Tyto chyby můžete bezpečně ignorovat.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a>Monitorování replikace databáze  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Monitorování stavu replikace databáze mezi lokalitami vysoké úrovně

1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** .  

2. Vyberte uzel **hierarchie lokality** a otevřete zobrazení **diagramu hierarchie** .  

3. Najeďte ukazatelem myši na čáru mezi dvěma lokalitami. Zobrazení stavu replikace globálních dat a dat lokality pro tyto lokality.  

### <a name="monitor-the-status-of-a-replication-link"></a>Monitoruje stav odkazu replikace.

1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** .  

2. Vyberte uzel **replikace databáze** a poté vyberte odkaz replikace, který chcete monitorovat. Pak vyberte příslušnou kartu pro zobrazení různých podrobností o stavu replikace pro tento odkaz.  
