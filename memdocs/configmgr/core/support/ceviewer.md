---
title: Prohlížeč hodnocení kolekce
titleSuffix: Configuration Manager
description: Pomocí prohlížeče hodnocení kolekce můžete zobrazit a vyřešit potíže s procesem vyhodnocení kolekce v Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723415"
---
# <a name="collection-evaluation-viewer"></a>Prohlížeč hodnocení kolekce

*Platí pro: Configuration Manager (Current Branch)*

Prohlížeč hodnocení kolekce je jedním z [Configuration Manager nástrojů](tools.md). Použijte ho k zobrazení a řešení potíží s procesem vyhodnocování kolekce na primárním serveru lokality.

Nástroj zobrazí následující informace:  

- Historické i živé informace pro vyhodnocení úplných a přírůstkových kolekcí  

- Stav fronty vyhodnocení  

- Čas, kdy se vyhodnocení kolekce dokončí  

- Které kolekce se aktuálně vyhodnocují  

- Odhadovaný čas, kdy se vyhodnocení kolekce spustí a dokončí  



## <a name="about-collection-evaluation"></a>O vyhodnocování kolekce

Proces vyhodnocení kolekce se spouští vyhodnocením pravidel členství kolekce za účelem aktualizace členů. Lokalita umístí kolekci, která je vyhodnocena v jedné ze čtyř různých front:  

- **Ruční fronta**: pro kolekce, které správce ručně vybral pro vyhodnocení z konzoly  

- **Nová fronta**: u nově vytvořených kolekcí  

- **Úplná fronta**: kolekce z důvodu úplného vyhodnocení  

- **Přírůstková fronta**: kolekce s přírůstkovým vyhodnocením  

Existují čtyři vlákna, která se spouštějí k vyhodnocení kolekcí ve výše uvedených frontách. Každá fronta zahrnuje řadu polí a každé pole zahrnuje kolekce, které se mají vyhodnotit. Vlákno, které je spuštěno pro frontu, vybere kolekci z pole a spustí vyhodnocení. Délka fronty označuje počet polí ve frontě.



## <a name="requirements"></a>Požadavky

- Spuštění nástroje na serveru lokality  

- Spusťte nástroj správcem s alespoň rolí **analytika jen pro čtení** .  

- Uživatel také vyžaduje oprávnění **ke čtení** pro databázi lokality v SQL.



## <a name="usage"></a>Využití

Spusťte **CEViewer. exe**. Hlavní nabídka nástroje obsahuje následující karty: 

- [Connect](#bkmk_connect): vytvoření počátečního připojení k serveru primární lokality a SQL Server  

- [Úplné vyhodnocení](#bkmk_full-eval): uvádí podrobné informace o všech minulých kompletních hodnoceních.   

- [Přírůstkové hodnocení](#bkmk_incremental-eval): zobrazuje podrobné informace o všech předchozích přírůstkových hodnoceních.  

- [Všechny fronty](#bkmk_all-q): shrnuje aktuální hodnocení shromažďování pro všechny čtyři fronty.  

- [Ruční fronta](#bkmk_manual-q): uvádí podrobné informace o aktuálním vyhodnocení kolekce v ruční frontě.  

- [Nová fronta](#bkmk_new-q): zobrazí podrobné informace o aktuálním vyhodnocení kolekce v nové frontě.  

- [Úplná fronta](#bkmk_full-q): uvádí podrobné informace o aktuálním vyhodnocení kolekce v úplné frontě.  

- [Přírůstková fronta](#bkmk_incremental-q): uvádí podrobné informace o aktuálním vyhodnocení kolekce v přírůstkové frontě.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Karta připojit

Tato karta vám umožní vytvořit počáteční připojení k serveru primární lokality. Nástroj také naváže připojení k SQL serveru, který je hostitelem databáze lokality.

Připojení k serveru primární lokality i k serverům SQL používají aktuální přihlášené přihlašovací údaje uživatele. Připojení k lokalitě centrální správy nebo k sekundární lokalitě nejsou podporována. V těchto lokalitách není spuštěn žádný proces vyhodnocení kolekce.

Jakmile nástroj úspěšně naváže připojení, přečtěte si oznámení v dolní části prohlížeče hodnocení kolekce, která potvrdí připojení nástroje k SQL serveru. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a>Karta úplná zkušební verze

Zobrazuje podrobné informace o předchozích hodnoceních pro celou kolekci. Existuje osm sloupců:  

- **Název kolekce**: název kolekce  

- **ID lokality**: ID lokality kolekce   

- **Doba běhu**: jak dlouho proběhlo poslední vyhodnocení kolekce, v sekundách  

- **Čas posledního dokončení vyhodnocení**: po dokončení posledního vyhodnocení kolekce  

- **Čas dalšího vyhodnocení**: po zahájení dalšího úplného vyhodnocení  

- **Změny členů**: člen se změní při poslední vyhodnocení kolekce. Tyto změny jsou buď plus (přidané členy), nebo mínus (členové odebrání).  

- **Čas poslední změny člena**: poslední čas, kdy došlo ke změně členství v vyhodnocení kolekce  

- **Procento**: procento doby vyhodnocování pro tuto kolekci v čase vyhodnocování celkových (všech kolekcí)  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a>Karta přírůstkové vyhodnocení

Zobrazuje podrobné informace o předchozích hodnoceních přírůstkových kolekcí. Existuje sedm sloupců:  

- **Název kolekce**: název kolekce  

- **ID lokality**: ID lokality kolekce   

- **Doba běhu**: jak dlouho proběhlo poslední vyhodnocení kolekce, v sekundách  

- **Čas posledního dokončení vyhodnocení**: po dokončení posledního vyhodnocení kolekce  

- **Změny členů**: člen se změní při poslední vyhodnocení kolekce. Tyto změny jsou buď plus (přidané členy), nebo mínus (členové odebrání).  

- **Čas poslední změny člena**: poslední čas, kdy došlo ke změně členství v vyhodnocení kolekce  

- **Procento**: procento doby vyhodnocování pro tuto kolekci v čase vyhodnocování celkových (všech kolekcí)  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a>Karta všechny fronty

Shrnuje vyhodnocení živých kolekcí pro všechny čtyři fronty. Existuje šest částí:  

- **Shrnutí**: zobrazuje celkový počet kolekcí a délku fronty pro všechny kolekce ve všech čtyřech frontách.  

- **Probíhá vyhodnocení**: zobrazuje kolekci, která je aktuálně vyhodnocována v každé frontě, a dobu, po kterou byla spuštěna  

- **Ruční aktualizace**: zobrazuje stručný souhrn vyhodnocených kolekcí, odhadovaný čas dokončení a pořadí vyhodnocování v ruční frontě.  

- **Nová kolekce**: zobrazuje stručný souhrn vyhodnocených kolekcí, odhadovaný čas dokončení a pořadí vyhodnocování v nové frontě kolekce.  

- **Úplné vyhodnocení**: zobrazuje stručný souhrn vyhodnocených kolekcí, odhadovaný čas dokončení a pořadí vyhodnocování v plné frontě hodnocení.  

- **Přírůstkové hodnocení**: zobrazuje stručný souhrn vyhodnocených kolekcí, odhadovaný čas dokončení a pořadí vyhodnocování v rámci fronty přírůstkového vyhodnocení.  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a>Karta Ruční fronta

Zobrazuje informace o aktuálně vyhodnocování ručního vyhodnocení kolekce. Pořadí v seznamu je pořadí, ve kterém bude kolekce vyhodnocena. Existují čtyři sloupce:  

- **Název kolekce**: název kolekce  

- **ID lokality**: ID lokality kolekce   

- **Odhadovaný čas dokončení**: po dokončení odhadu vyhodnocení  

- **Odhadovaná doba běhu**: jak dlouho je vyhodnocení odhadované, za den: hodina: minuta: druhý formát  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a>Karta nová fronta

Zobrazuje živé informace o vyhodnocování nového vyhodnocení kolekce. Pořadí v seznamu je pořadí, ve kterém bude kolekce vyhodnocena. Existují čtyři sloupce:  

- **Název kolekce**: název kolekce  

- **ID lokality**: ID lokality kolekce   

- **Odhadovaný čas dokončení**: po dokončení odhadu vyhodnocení  

- **Odhadovaná doba běhu**: jak dlouho je vyhodnocení odhadované, za den: hodina: minuta: druhý formát  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a>Karta plná fronta

Zobrazí informace o aktuálně vyhodnocování úplného vyhodnocení kolekce. Pořadí v seznamu je pořadí, ve kterém bude kolekce vyhodnocena. Existují čtyři sloupce:  

- **Název kolekce**: název kolekce  

- **ID lokality**: ID lokality kolekce   

- **Odhadovaný čas dokončení**: po dokončení odhadu vyhodnocení  

- **Odhadovaná doba běhu**: jak dlouho je vyhodnocení odhadované, za den: hodina: minuta: druhý formát  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a>Karta přírůstkové fronty

Zobrazuje informace o hodnocení přírůstkové kolekce, které se právě vyhodnocuje. Pořadí v seznamu je pořadí, ve kterém bude kolekce vyhodnocena. Existují čtyři sloupce:  

- **Název kolekce**: název kolekce  

- **ID lokality**: ID lokality kolekce   

- **Odhadovaný čas dokončení**: po dokončení odhadu vyhodnocení  

- **Odhadovaná doba běhu**: jak dlouho je vyhodnocení odhadované, za den: hodina: minuta: druhý formát  



