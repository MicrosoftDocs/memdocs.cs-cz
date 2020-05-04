---
title: Správce fronty úloh DP
titleSuffix: Configuration Manager
description: K odstraňování potíží a správě úloh distribuce obsahu pro Configuration Manager distribučních bodů použijte Správce fronty úlohy DP.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713657"
---
# <a name="dp-job-queue-manager"></a>Správce fronty úloh DP

*Platí pro: Configuration Manager (Current Branch)*

Správce fronty úloh distribučního bodu (DP) je jedním z [Configuration Manager nástrojů](tools.md). Použijte ji k řešení potíží a správě probíhajících úloh distribuce obsahu pro Configuration Manager distribučních bodů. 

Nástroj zobrazí seznam úloh, které má součást správce přenosu balíčků ve frontě. Zobrazuje taky stav úloh: připraveno ke spuštění, spuštění nebo opakování. Umožňuje manipulovat s úlohami ve frontě, přesouvat úlohy v seznamu výše, zrušit úlohu nebo ručně spustit úlohu.

Také získává informace ze serveru lokality, na kterém distribuční bod spouští úlohu. Nástroj se připojí přes poskytovatele k serveru lokality. Nepřipojuje se ke každému vzdálenému distribučnímu bodu pro shromáždění těchto informací. Vzhledem k tomu, že aktivuje akce a získává informace prostřednictvím poskytovatele, dochází ke zpoždění při odrážející změny ze vzdálených distribučních bodů.



## <a name="usage"></a>Využití

Spusťte **DPJobMgr. exe**. Hlavní nabídka nástroje obsahuje následující karty: 

- [Connect](#bkmk_connect): vytvoření počátečního připojení k serveru primární lokality  

- [Přehled](#bkmk_overview): Shrnutí v jednom zobrazení všech úloh, které jsou spuštěny ve všech distribučních bodech  

- [Informace o distribučním bodu](#bkmk_dp-info): vícenásobný výběr distribučních bodů pro jejich sledování a Správa jedné úlohy zájmu  

- [Spravovat úlohy](#bkmk_manage-jobs): zobrazuje v jednom nestrukturovaném zobrazení seznam všech úloh a jejich stavů. Manipulace s úlohami, jejich přesun, zrušení nebo ruční spuštění.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Karta připojit

Tato karta slouží k vytvoření počátečního připojení k serveru primární lokality. Používá přihlašovací údaje aktuálně přihlášeného uživatele. Nemůžete se připojit k lokalitě centrální správy nebo k sekundárním webům. Připojení vyžaduje roli zabezpečení **správce s úplnými oprávněními** .

Jakmile nástroj úspěšně naváže spojení, oznámení v dolní části nástroje potvrdí, že je připojeno k serveru lokality. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a>Karta Přehled

Zobrazí souhrn všech úloh ve všech distribučních bodech. Podívejte se na následující sloupce:  

- **Distribuční bod**: seznam názvů distribučních bodů  

- **Běžící úlohy**: zobrazuje počet souběžných úloh, které jsou spuštěny v určitém distribučním bodě.  

    > [!Tip]  
    > Počet souběžných distribucí softwaru je nastavení lokality. Toto nastavení bylo upraveno ve vlastnostech součásti distribuce softwaru.  

- **Celkový počet úloh**: zobrazuje počet všech úloh cílených na konkrétní distribuční bod. Toto číslo zahrnuje úlohy, které běží, opakují nebo čekají na provedení.  

- **Celkem opakování**: zobrazuje počet opakovaných pokusů o provedení úloh v určitém distribučním bodě. Vyšší číslo může představovat obecný problém s konkrétním distribučním bodem.  


> [!Tip]  
> - Chcete-li seřadit jednotlivé sloupce na této kartě, klikněte na název sloupce.  
> 
> - Ručně aktualizovat informace na této kartě kliknutím na **aktualizovat**  
> 
> - Automaticky aktualizovat informace na této kartě kliknutím na **Spustit automatickou aktualizaci** a nastavením intervalu automatické aktualizace. Výchozí interval aktualizace je dvě minuty.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a>Karta informace o distribučním bodu

Zobrazuje seznam všech distribučních bodů v připojené lokalitě. V podokně na levé straně je seznam všech distribučních bodů. Klikněte na **Vybrat vše** nebo zrušte **Výběr vše** v případě potřeby nebo vyberte v seznamu konkrétní distribuční body. Podokno na pravé straně znázorňuje úlohy pro vybrané distribuční body.

Existuje osm sloupců:  

- **Ikona stavu**: Existují tři možné ikony stavu:  

    - **Připraveno**: označuje, že konkrétní úloha dokončila všechny kroky ověření. Je připravený k přidání do běžících souběžných úloh. Úlohy v tomto stavu jsou obvykle ve fázi čekání. Čekají na dokončení probíhajících procesů, aby bylo možné otevřít prostor pro tyto spuštěné prostory.  

    - **Running**: označuje, že v distribučním bodě je aktuálně spuštěna určitá úloha. Pro dlouhotrvající úlohy (velké balíčky) obvykle je čas získat průběh (%) směrem k dokončení. Zobrazuje toto procento ve sloupci **průběh** v tomto zobrazení. Pro malé balíčky může sloupec **průběh** zůstat prázdný. Úlohu již může být dokončena v době, kdy obdrží stav ze vzdáleného distribučního bodu.  

    - **Opakování**: označuje, že konkrétní úloha se nezdařila a je nyní ve stavu opakování. Tato úloha se zopakuje po intervalu opakování. Tento interval se dá nakonfigurovat a ve výchozím nastavení se nastaví na 30 minut.  

- **Software**: název balíčku, který je zaměřený na konkrétní distribuční bod  

- **ID balíčku**: ID balíčku, který je zaměřený na konkrétní distribuční bod.  

- **Velikost**: velikost balíčku v KB  

- **Průběh**: procento dokončení úlohy. Další informace najdete v popisu ikony stavu **spuštění** .  

- **Čas spuštění/restartování**: u spuštěné úlohy je tato hodnota počáteční čas (zelený). Pro úlohu opakování se jedná o čas, kdy se úloha zopakuje.  

- **Opakování**: počet pokusů o opětovné vyzkoušení tohoto balíčku.  

- **Název distribučního bodu**: plně kvalifikovaný název domény (FQDN) distribučního bodu  

> [!Tip]  
> - Chcete-li seřadit jednotlivé sloupce na této kartě, klikněte na název sloupce.  
> 
> - Ručně aktualizovat informace na této kartě kliknutím na **aktualizovat**  
> 
> - Automaticky aktualizovat informace na této kartě kliknutím na **Spustit automatickou aktualizaci** a nastavením intervalu automatické aktualizace. Výchozí interval aktualizace je dvě minuty.  
> 
> - Pokud potřebujete upravit konkrétní úlohu, klikněte pravým tlačítkem myši na úlohu v tomto zobrazení a vyberte **Spravovat úlohu**. Tato akce otevře [kartu spravovat úlohy](#bkmk_manage-jobs).  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a>Karta spravovat úlohy

Zobrazuje v jednom nestrukturovaném zobrazení seznam všech úloh a jejich stavů. Obsahuje stejné osm sloupců jako [Karta informace o distribučním bodu](#bkmk_dp-info). V tomto zobrazení klikněte pravým tlačítkem na úlohy pro následující akce:  

- **Spustit**: spustí úlohu, která je v jiném stavu než je spuštěná.  

- **Přesunout na začátek**: přesune jednu nebo více úloh na začátek fronty. Tato akce může vést k okamžitému spuštění úloh. Úloha s nižší prioritou se může kvůli této akci pozastavit.  

- **Přesunout nahoru**: přesune konkrétní úlohu na jeden řádek výše. Úloha s nižší prioritou může pozastavit spuštění z důvodu této akce.  

- **Přesunout dolů**: přesune konkrétní úlohu na jeden řádek níže.  

- **Přesunout na konec**: přesune jednu nebo více úloh do dolní části fronty.  

    > [!Tip]  
    > Přetahováním úloh v seznamu je přesuňte.  

- **Zrušit**: pokusí se zrušit jednu nebo více úloh.  

    > [!Note]  
    > Nemůžete zrušit úlohy v blízkosti jejich konečného času dokončení. Pokud je server lokality také distribučním bodem, nemůžete zrušit úlohy na serveru lokality.  



## <a name="see-also"></a>Viz také

- [Základní koncepty správy obsahu](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Správce přenosu balíčků](../plan-design/hierarchy/package-transfer-manager.md)
