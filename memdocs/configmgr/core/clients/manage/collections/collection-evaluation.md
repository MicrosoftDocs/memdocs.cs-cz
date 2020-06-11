---
title: Vyhodnocení kolekce
titleSuffix: Configuration Manager
description: Přečtěte si o procesu vyhodnocení kolekce, typech a triggerech. Pochopení grafu vyhodnocení kolekce a hierarchie.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af90154b848ddcd7cbff21917ef122ab10585098
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663910"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Vyhodnocení kolekce v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager používá *vyhodnocení kolekce* k aktualizaci členství kolekce na základě pravidel kolekce, které definujete. Rozsah vyhodnocení kolekce a časování se liší v závislosti na konfiguraci lokality a kolekce a typu vyhodnocení. 

Je důležité pochopit chování při vyhodnocování kolekce, abyste mohli vytvářet vhodná rozhodnutí o návrhu kolekce. Pokyny a doporučení k vyhodnocení kolekce najdete v tématu [osvědčené postupy pro kolekce](best-practices-for-collections.md).

## <a name="evaluation-process"></a>Proces vyhodnocení

Záznam [Colleval. log](https://docs.microsoft.com/mem/configmgr/core/plan-design/hierarchy/log-files#BKMK_ServerLogs) , když vyhodnocení kolekce vytvoří, změní a odstraní kolekce.

Na vysoké úrovni se každé vyhodnocení každé kolekce a aktualizace aktualizuje podle těchto kroků:

![Proces aktualizace kolekce na vysoké úrovni](media/high-level-collection-update-process.png)

1. Spusťte dotaz na kolekci.
1. Přidejte všechny systémy, které jsou přímými členy.
1. Vyhodnoťte všechny *zahrnuté* kolekce.
   
   Pokud mají kolekce zahrnutí taky pravidla dotazování nebo zahrnutí nebo vyloučení kolekcí, vyhodnoťte je také. Pokud samotné kolekce include omezují omezení kolekcí, vyhodnoťte z nich všechny kolekce. Po úplném vyhodnocení stromu vrátí výsledky do kolekce volání.
   
1. Provede logickou hodnotu `AND` mezi vrácenými výsledky a omezením kolekce.
1. Vyhodnoťte *vyloučené* kolekce.
   
   Pokud mají kolekce vyloučení taky pravidla dotazování nebo zahrnutí nebo vyloučení kolekcí, vyhodnoťte je také. Pokud tyto kolekce samy omezují kolekce, vyhodnoťte z nich všechny kolekce. Po úplném vyhodnocení stromu vrátí výsledky do kolekce volání.
   
1. Porovnejte sadu výsledků dotazu z vyhodnocování přímých členů a zahrnutím kolekcí s výsledky vyhodnocení vyloučených kolekcí.
1. Zapište změny do databáze a proveďte aktualizace.
1. Aktivovat taky všechny závislé kolekce, které se mají aktualizovat Závislé kolekce jsou kolekce, které aktuální kolekce omezuje nebo které odkazují na aktuální kolekci pomocí pravidel include nebo Exclude.

## <a name="collection-evaluation-types-and-triggers"></a>Typy a triggery vyhodnocení kolekce

Tyto typy vláken zpracovávají vyhodnocení kolekce v závislosti na typu vyhodnocení:

- **Primární** pro plánované aktualizace kolekcí
- **Pomocná** osoba pro ruční aktualizaci kolekcí se závislými kolekcemi
- **Jednoduchá** ruční aktualizace kolekcí bez závislých kolekcí
- **Expresní** aktualizace pro přírůstkové shromažďování

Následující tabulka popisuje triggery vyhodnocování kolekce a jejich odpovídající typy vyhodnocení. 

| Trigger | Typ vyhodnocení | Popis |
|---------|-----------------|-------------|
|Ruční|Jedna nebo pomocná|Ruční je vyhodnocování kolekce s nejvyšší prioritou. Když správce požádá o ruční vyhodnocení kolekce, vyhodnocení kolekce přiřadí k vyhodnocení další dostupné vlákno vyhodnocení.|
|Naplánované|Primární|Proces plánovaného vyhodnocení je stejný jako ruční vyhodnocení, s výjimkou toho, že je vyhodnocování založené na čase, nikoli na základě událostí.|
|Příprava|Jedna nebo pomocná|Všechny kolekce přímo nebo nepřímo závisí na **všech systémech** nebo **všech uživatelích a skupinách uživatelů**. Obě tyto kolekce provádí úplné hodnocení shromažďování dat v 4:00. den. Změna některé z těchto kolekcí aktivuje aktualizace závislých kolekcí na základě [celého grafu shromažďování](#collection-evaluation-graph).
|Přírůstkový|Express|Přírůstkové hodnocení používá graf vyhodnocení kolekce k vyhodnocení a aktualizaci závislých kolekcí v případě, že se změní aktualizace pro přírůstkové členství kolekce. Configuration Manager monitoruje a aktualizuje objekty prostředků ve všech kolekcích, které jsou nakonfigurované pro přírůstkové aktualizace.<br /><br />Pokud je dotaz na kolekci založený na informacích, které se později aktualizují, jako je inventář hardwaru, Configuration Manager během plánované aktualizace kolekce přidat nebo odebrat prostředek z kolekce.|

## <a name="collection-evaluation-graph"></a>Graf vyhodnocení kolekce

*Graf vyhodnocení kolekce* mapuje všechny kolekce, které se vztahují k kolekci určené pro vyhodnocení. Vyhodnocení kolekce zahrnuje cílovou kolekci a všechny související kolekce v grafu vyhodnocení kolekce.

Při spuštění vyhodnocení kolekce Configuration Manager sestaví graf, který zahrnuje všechny kolekce, které by mohly být možná nutné vyhodnotit v důsledku změn v cílové kolekci, od nejvyšší úrovně v cyklu. Vyhodnocení kolekce pak projde grafem v daném pořadí a vyhodnocuje každé členství v kolekci. Po úplném vyhodnocení kolekce vyhodnocovací filtr kolekce odebere kolekce nižší úrovně, které nejsou ovlivněny tímto cyklem z grafu vyhodnocení kolekce.

Pokud jedna nebo více vyhodnocených kolekcí obsahuje pravidlo zahrnutí nebo vyloučení, vyhodnocení kolekce přidá do grafu zahrnutou nebo vyloučenou kolekci spolu se všemi kolekcemi, které mají omezení kolekce. Pokud během hodnocení zahrnutí a vyloučení kolekce dojde ke změnám, bude graf v této větvi pokračovat, než se vrátí do hlavní větve.

Configuration Manager vytvoří dva typy grafů hodnocení, *přírůstkové* nebo *úplné*.

### <a name="incremental-collection-evaluation"></a>Přírůstkové vyhodnocování shromažďování

Když se data tabulky změní, Trigger SQL vloží řádek do tabulky **CollectionNotifications** . Při příštím spuštění plánu vyhodnocování kolekce se jedná `AND` o ID prostředku s existujícím dotazem kolekce a spustí aktualizace pro kolekce, které jsou povoleny pro *přírůstkové* kolekce.

Přírůstkové vyhodnocování kolekce spouští jeden dotaz na počítač. Výchozí konfigurace lokality pro přírůstkové vyhodnocování shromažďování je každých pět minut.

Graf hodnocení přírůstkové kolekce mapuje odkazované kolekce pouze v případě, že jsou povoleny pro přírůstkové vyhodnocení. Pokud je přírůstkové vyhodnocení omezeno na kolekci, která není povolena pro přírůstkové vyhodnocení, graf vyhodnotí kolekci na základě stávajícího členství v omezující kolekci. 

Například následující diagram znázorňuje nově zjištěné prostředky, které se vztahují na všechny kolekce. Vyhodnocení kolekce ale aktualizuje jenom kolekce **všechny servery** a **všechny řadiče domény** . Vyhodnocení kolekce nevyhodnocuje jiné kolekce, protože kolekce **všechny členské servery** není povolena pro přírůstkové vyhodnocení.

![Příklad grafu vyhodnocení přírůstkové kolekce](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Úplné vyhodnocení kolekce

Vyhodnocení ruční nebo plánované kolekce vytvoří *kompletní* graf vyhodnocení kolekce všech závislých kolekcí. Graf obsahuje všechny kolekce, které odkazují na kolekci, která aktualizuje a následné kolekce. Configuration Manager nadále vyhodnocuje graf, pokud dojde k aktualizacím pro zpracovávané kolekce.

Následující diagram znázorňuje, jak naplánovaná nebo ruční žádost o aktualizaci kolekce pro kolekci **všechny servery** vytváří úplný graf, který obsahuje všechny použitelné kolekce. Nové prostředky serveru DNS a řadiče domény jsou v oboru dotazů na členství všech kolekcí, takže se všechny kolekce aktualizují.

![Graf vyhodnocení úplné kolekce – příklad 1](media/full-collection-evaluation-graph-1.png)

Úplné hodnocení neprovádí vždy vyhodnocení všech kolekcí. Graf vyhodnocení kolekce pokračuje pouze v vyhodnocení závislých kolekcí, pokud dojde k aktualizaci aktuální odkazované kolekce. Pokud se přírůstkově aktualizované kolekce aktualizuje během plánovaných přírůstkových hodnocení, nemusí se aktualizovat odkazy na kolekce, které nejsou povolené pro přírůstkové aktualizace. Úplné vyhodnocení neaktualizuje kolekci, ukončí graf vyhodnocení kolekce a všechny referenční hodnocení kolekce pro tento cyklus. 

V následujícím příkladu se server DNS na stávajícím serveru stane členem kolekce **serverů DNS** , ale vzhledem k tomu, že není k dispozici žádná aktualizace pro kolekci **všechny členské servery** , úplné vyhodnocení nevyhodnotí kolekci **serverů DNS** . Další cyklus přírůstkového hodnocení vyhodnotí kolekci **serverů DNS** , protože se jedná o přírůstkovou kolekci.

![Graf vyhodnocení úplné kolekce – příklad 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Další kroky
- [Vytváření kolekcí](create-collections.md)
- [Osvědčené postupy pro kolekce](best-practices-for-collections.md)
- [Prohlížeč hodnocení kolekce](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer)
- [ConfigMgrDogs řešení potíží s relací ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) na konferenci TechEd Austrálie
