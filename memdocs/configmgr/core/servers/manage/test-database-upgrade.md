---
title: Test aktualizace databáze
titleSuffix: Configuration Manager
description: Otestujte upgrade databáze lokality při instalaci aktualizací pro Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719978"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testování upgradu databáze při instalaci aktualizace

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto tématu vám pomůžou spustit test upgradu databáze před instalací konzolové aktualizace pro aktuální větev Configuration Manager. Upgrade upgradu již není povinný nebo doporučený krok, není-li databáze podezřelá nebo je upravena vlastními nastaveními, která nejsou explicitně podporována nástrojem Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Potřebuji spustit test upgrade?
Vyřazení tohoto testu upgradu bylo možné z důvodu změn zavedených s Configuration Manager aktuální větví. Tyto změny zjednodušují proces a rychlost, kterými se dá v produkčním prostředí aktualizovat novější verze. Tímto přepracováním jsme mohli pomáhat zákazníkům, kteří při instalaci každé nové aktualizace mají nižší riziko a méně provozní režie.

Tyto změny slouží k instalaci aktualizací, včetně logiky, která automaticky vrátí neúspěšnou aktualizaci bez nutnosti spustit obnovení lokality. Tyto změny umožňují použití konzoly nástroje ke správě instalací aktualizací a zahrnují možnost [opakovat instalaci aktualizace, která se nezdařila](install-in-console-updates.md#bkmk_retry).

> [!TIP]
> Když provedete upgrade na Configuration Manager aktuální větev ze staršího produktu, jako je například System Center 2012 Configuration Manager, [upgrade testů databáze zůstane Doporučeným krokem](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test).

Pokud ještě plánujete otestovat upgrade databáze lokality při instalaci konzolové aktualizace, doplňují následující informace [pokyny k instalaci konzolové aktualizace](install-in-console-updates.md#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Příprava na spuštění upgradu testovací databáze  
Než do své hierarchie nainstalujete novou aktualizaci, jako je třeba aktualizace 1702, můžete otestovat upgrade databáze lokality.

Chcete-li spustit test upgradu, použijte instalační program nástroje Configuration Manager ze zdrojových souborů z [disku CD-ROM. Nejnovější složku](the-cd.latest-folder.md) webu, na které běží verze Configuration Manager, na kterou aktualizujete. Tento požadavek znamená, že k otestování aktualizace databáze pro aktualizaci na 1702:
-   Musíte mít aspoň jednu lokalitu, na které běží verze 1702, ze které můžete tento disk CD získat. Poslední složka
-   Pokud nemáte lokalitu, na které běží požadovaná verze, zvažte možnost nainstalovat lokalitu v testovacím prostředí a následně aktualizovat tuto lokalitu na novou verzi. Tím se vytvoří disk CD. Poslední složka se správnou verzí zdrojových souborů.

Test upgradu se spustí proti zálohování databáze lokality, kterou jste obnovili do samostatné instance SQL Server.  Instalaci spustíte z **disku CD-ROM. Poslední** složka s přepínačem příkazového řádku **TESTDBUPGRADE** k otestování upgradu, který obnovil kopii databáze. Po dokončení testu se upgradovaná databáze zruší. Nemůže být použita Configuration Manager lokalitou.

Pokud se instalace aktualizace nezdařila, neměli byste lokalitu obnovovat. Místo toho můžete instalaci aktualizace opakovat v konzole nástroje.

##  <a name="run-the-test-upgrade"></a>Spustit test upgradu    
1. Použijte instalační program Configuration Manager a zdrojové soubory z **disku CD-ROM. Poslední** složka webu, na které je spuštěná verze, na kterou plánujete aktualizovat  

2. Zkopírujte **disk CD. Nejnovější** složku do umístění na instanci SQL Server, kterou použijete ke spuštění upgradu testovací databáze.

3. Vytvořte zálohu databáze lokality, kterou chcete otestovat upgrade. Dále obnovte kopii této databáze do instance SQL Server, která není hostitelem Configuration Manager lokality. Instance SQL Server musí jako databázi lokality používat stejnou edici SQL Server.  

4. Po obnovení kopie databáze spusťte **instalační program** z disku CD-ROM. Nejnovější složku, která obsahuje zdrojové soubory z verze, na kterou aktualizujete. Při spuštění instalačního programu použijte možnost příkazového řádku **/TESTDBUPGRADE**. Pokud instance SQL Server hostující kopii databáze není výchozí instancí, zadejte argumenty příkazového řádku, které identifikují instanci hostující kopii databáze lokality.   

   Například máte databázi lokality s názvem databáze *SMS_ABC*. Kopii této databáze lokality obnovíte do podporované instance SQL Server s názvem instance *dbtest*. K otestování upgradu této kopie databáze lokality použijte následující příkazový řádek: **Setup. exe/TESTDBUPGRADE DBtest \ CM_ABC**.  

   Soubor Setup. exe najdete na zdrojovém médiu Configuration Manager v následujícím umístění: **SMSSETUP\BIN\X64**.  

5. V instanci SQL Server, kde spustíte test upgradu, Sledujte v souboru *ConfigMgrSetup. log* , který se nachází v kořenovém adresáři systémového disku, průběh a úspěch.  

    Pokud test upgradu selže, opravte všechny problémy související s selháním upgradu databáze lokality. Pak vytvořte novou zálohu databáze lokality a otestujte upgrade nové kopie databáze.  



## <a name="next-steps"></a>Další kroky
Po úspěšném dokončení aktualizace testovací databáze zahodí aktualizovanou databázi. Nemůže být použita Configuration Manager lokalitou. Pak se můžete vrátit k aktivnímu webu a [zahájit instalaci aktualizace](install-in-console-updates.md).
