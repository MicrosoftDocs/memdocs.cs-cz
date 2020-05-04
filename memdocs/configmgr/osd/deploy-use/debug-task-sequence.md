---
title: Ladění pořadí úkolů
titleSuffix: Configuration Manager
description: K řešení potíží s pořadím úloh použijte nástroj pro ladění pořadí úloh.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66f460b7ba5c870a9ee81d10835ceb9f660cba89
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711032"
---
# <a name="debug-a-task-sequence"></a>Ladění pořadí úkolů

*Platí pro: Configuration Manager (Current Branch)*

<!--3612274-->

Počínaje verzí 1906 je ladicí program sekvence úloh novým nástrojem pro řešení potíží. Pořadí úkolů nasadíte v režimu ladění do malé kolekce. Umožňuje procházet pořadí úkolů řízeným způsobem, který pomáhá řešit problémy a vyšetřování. Ladicí program aktuálně běží na stejném zařízení jako modul pořadí úkolů, není to vzdálený ladicí program.

> [!Note]  
> V této verzi Configuration Manager je ladicí program sekvence úloh předběžnou verzí funkce. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Požadavky

- Aktualizace klienta Configuration Manager na cílovém zařízení

- Přihlaste se k cílovému zařízení jako uživatel v místní skupině **Administrators** . Ladicí program je spuštěn pouze pro správce.

- Aktualizujte spouštěcí image přidruženou k pořadí úkolů, abyste se ujistili, že má nejnovější verzi klienta.


## <a name="start-the-tool"></a>Spusťte nástroj.

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.

1. Vyberte pořadí úkolů. Ve skupině nasazení na pásu karet vyberte možnost **ladit**.

    > [!Tip]  
    > Alternativně nastavte proměnnou **TSDebugMode** na objekt `TRUE` na kolekci nebo počítači, do kterého je pořadí úkolů nasazeno. Jakékoli zařízení, které má tuto sadu proměnných, vloží do režimu ladění jakékoli nasazené pořadí úkolů.

1. Vytvoření ladicího nasazení. Nastavení nasazení jsou shodná s normálním nasazením pořadí úloh. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md#process).

    > [!Note]  
    > Pro nasazení ladění můžete vybrat jenom malou kolekci. Zobrazuje jenom kolekce zařízení s maximálně 10 členy.

Počínaje verzí 1910 použijte novou proměnnou pořadí úloh **TSDebugOnError** k automatickému spuštění ladicího programu, když pořadí úkolů vrátí chybu.<!-- 5012536 --> Další informace najdete v tématu [proměnné pořadí úkolů – TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError).

## <a name="use-the-tool"></a>Použití nástroje

Když je pořadí úkolů spuštěné na zařízení, otevře se okno ladicího programu pořadí úkolů podobné jako na následujícím snímku obrazovky:

![Snímek obrazovky s ladicím programem pořadí úloh](media/3612274-tsdebug.png)

Ladicí program obsahuje následující ovládací prvky:

- **Krok**: z *aktuální* pozice spouštějte pouze další krok v pořadí úkolů.  

    > [!Note]  
    > Pokud je pořadí úkolů v režimu ladění, pokud krok vrátí závažnou chybu, pořadí úloh nebude v normálním případě úspěšné. Toto chování vám dává možnost opakovat krok po provedení externí změny.

- **Spustit**: z *aktuální* pozice, spustit pořadí úloh normálně na konec, další bod *přerušení* nebo v případě, že se krok nezdařil. Než použijete tuto akci, nezapomeňte nastavit body přerušení pomocí akce **nastavit přerušení** .

- **Nastavit aktuální**: Vyberte krok v ladicím programu a pak vyberte **nastavit aktuální**. Tato akce přesune *aktuální* ukazatel na tento krok. Tato akce umožňuje přeskočit kroky nebo přesunout zpět.  

    > [!Warning]  
    > Ladicí program nebere v úvahu typ kroku při změně aktuální pozice v sekvenci. Některé kroky můžou nastavovat proměnné pořadí úkolů, které se vyžadují pro vyhodnocení podmínky v pozdějších krocích. Pokud je příkaz mimo pořadí, některé kroky můžou selhat nebo způsobit významné poškození zařízení. Tuto možnost použijte na vlastní riziko.  

- **Nastavit přerušení**: Vyberte krok v ladicím programu a pak vyberte **nastavit přerušení**. Tato akce přidá bod *přerušení* v ladicím programu. Při **spuštění** pořadí úkolů se zastaví na *konci.*  

    - Před použitím akce **Spustit** nastavte body přerušení.

    - Počínaje verzí 1910, pokud v ladicím programu vytvoříte bod přerušení a pak pořadí úkolů restartuje počítač, ladicí program po restartování udržuje body přerušení.<!-- 5012509 -->

    - Ve verzi 1906 se po restartování počítače neukládají body přerušení, například krok [restartovat počítač](../understand/task-sequence-steps.md#BKMK_RestartComputer) . Pokud například spustíte ladicí program z centra softwaru pro pořadí úloh pro vytvoření bitové kopie, nenastavte v fázi Windows PE přerušení. Když se počítač restartuje do prostředí Windows PE, ladicí program pořadí úkolů pozastaví, aby bylo možné nastavit přerušení.

- **Vymazat všechny konce**: odebrat všechny body přerušení.

- **Soubor protokolu**: otevře aktuální soubor protokolu pořadí úloh **souboru Smsts. log**s [CMTrace](../../core/support/cmtrace.md). V případě, že je modul pořadí úkolů "čeká na ladicí program", můžete zobrazit položky protokolu.

- Příkazového **řádku**: v systému Windows PE otevře příkazový řádek.

- **Zrušit**: Ukončete ladicí program a selhání pořadí úkolů.

- **Konec**: odpojte a zavřete ladicí program, ale pořadí úkolů bude i nadále normálně fungovat.

V okně **proměnné pořadí úkolů** se zobrazují aktuální hodnoty všech proměnných v prostředí pořadí úloh. Další informace najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md). Použijete-li krok [nastavit proměnnou pořadí úloh](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) s možností pro **nezobrazení této hodnoty**, ladicí program nezobrazí hodnotu proměnné. V ladicím programu nelze upravovat hodnoty proměnných.

> [!Note]
> Některé proměnné pořadí úkolů jsou pouze pro interní použití a nejsou uvedeny v referenční dokumentaci.

Ladicí program pořadí úkolů se i nadále spouští po kroku [restartování počítače](../understand/task-sequence-steps.md#BKMK_RestartComputer) , ale je nutné znovu vytvořit všechny body přerušení. I když je pořadí úkolů nemusí vyžadovat, protože ladicí program vyžaduje zásah uživatele, musíte se přihlásit k systému Windows, abyste mohli pokračovat. Pokud se po jednu hodinu nebudete moci pokračovat v ladění, pořadí úkolů se nezdařilo.

Také se postupuje na podřízené pořadí úkolů pomocí kroku [pořadí úkolů Spustit](../understand/task-sequence-steps.md#child-task-sequence) . Okno ladicího programu zobrazuje kroky podřízeného pořadí úloh spolu s hlavním pořadím úkolů.


## <a name="known-issues"></a>Známé problémy

Pokud cílíte na normální nasazení a nasazení ladění na stejné zařízení prostřednictvím více nasazení, nemůžete spustit ladicí program pořadí úkolů.


## <a name="see-also"></a>Viz také

- [O krocích pořadí úkolů](../understand/task-sequence-steps.md)
- [Proměnné pořadí úkolů](../understand/task-sequence-variables.md)
- [Jak používat proměnné pořadí úkolů](../understand/using-task-sequence-variables.md)
- [Nasazení pořadí úkolů](deploy-a-task-sequence.md)
