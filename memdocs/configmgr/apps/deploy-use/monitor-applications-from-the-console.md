---
title: Monitorování aplikací z konzoly
titleSuffix: Configuration Manager
description: Monitorujte nasazení softwaru včetně aktualizací, nastavení dodržování předpisů a aplikací pomocí pracovního prostoru Monitorování v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710052"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Monitorování aplikací z konzoly Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


V Configuration Manager můžete monitorovat nasazení veškerého softwaru, včetně aktualizací softwaru, nastavení dodržování předpisů, aplikací, pořadí úloh a balíčků a programů. Nasazení můžete monitorovat pomocí pracovního prostoru **monitorování** v konzole Configuration Manager nebo pomocí sestav.  

 Aplikace v Configuration Manager podporují monitorování na základě stavu, které umožňuje sledovat poslední stav nasazení aplikací pro uživatele a zařízení. Tyto stavové zprávy obsahují informace o jednotlivých zařízeních. Například pokud je aplikace nasazena do kolekce uživatelů, můžete zobrazit stav dodržování předpisů nasazení a účel nasazení v konzole Configuration Manager.  

## <a name="learn-about-compliance-states"></a>Informace o stavech dodržování předpisů
 Stav nasazení aplikace může mít některý z následujících stavů shody:  

-   **Úspěch** – Nasazení aplikace bylo úspěšné nebo bylo zjištěno, že instalace proběhla již dříve.  

-   **Probíhá** – Nasazení aplikace probíhá.  

-   **Neznámé** – Stav nasazení aplikace nelze určit. Tento stav se netýká nasazení s účelem **K dispozici**. Tento stav obvykle bývá zobrazen, pokud od klienta dosud nebyly přijaty stavové zprávy.  

-   **Požadavky nesplněny** – Aplikace nebyla nasazena, protože neodpovídá některé závislosti nebo požadavku pravidla, případně proto, že cílový operační systém nasazení není použitelný.  

-   **Chyba** – Nasazení aplikace se nezdařilo z důvodu chyby.  

Můžete si Zobrazit další informace o jednotlivých stavech dodržování předpisů, včetně podkategorií v rámci stavu dodržování předpisů a počtu uživatelů a zařízení v této kategorii. Například stav shody **Chyba** obsahuje následující podkategorie:  

- Chyby při vyhodnocování požadavků  

- Chyby související s obsahem  

- Chyby při instalaci  

  Pokud nasazení aplikace odpovídá více stavů shody, můžete vidět celkový stav, který představuje nejnižší úroveň shody. Příklad:  

  -   Pokud se uživatel přihlásí ke dvěma zařízením a aplikace se úspěšně nainstaluje na jedno zařízení, ale instalace na druhé zařízení se nezdaří, zobrazí se jako **Chyba**agregovaný stav nasazení aplikace pro tohoto uživatele.  

  -   Pokud je aplikace nasazena pro všechny uživatele, kteří se přihlásí k počítači, obdržíte pro tento počítač více výsledků nasazení. Pokud se jedno z nasazení nezdaří, celkový stav nasazení pro tento počítač bude **Chyba**.  

Stavy nasazení balíčku a programu nejsou agregovány.  

 Pomocí těchto podkategorií můžete rychle zjistit jakékoli závažné potíže s nasazením aplikace. Můžete si také zobrazit další informace o zařízeních spadajících do určité podkategorie stavu shody.  

 Správa aplikací v Configuration Manager zahrnuje řadu předdefinovaných sestav, které umožňují monitorovat informace o aplikacích a nasazeních. Tyto sestavy mají kategorii sestav **Distribuce softwaru – monitorování aplikací**.  

 Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorování stavu aplikace v konzole Configuration Manager  

1.  V konzole Configuration Manager vyberte možnost **monitorování** > **nasazení**.  

3.  Chcete-li zkontrolovat podrobnosti nasazení pro každý stav dodržování předpisů a zařízení v tomto stavu, vyberte nasazení a pak na kartě **Domů** ve skupině **nasazení** zvolte možnost **Zobrazit stav** a otevřete podokno **stav nasazení** . V tomto podokně si můžete zobrazit položky s jednotlivými stavy shody. Pokud chcete zobrazit podrobnější informace o stavu nasazení tohoto prostředku, vyberte jakýkoli Asset.  

    > [!NOTE]  
    >  Počet položek, které se dají zobrazit v podokně **Stav nasazení** , je omezený na 20 000. Pokud potřebujete zobrazit víc položek, použijte k zobrazení dat o stavu aplikace Configuration Manager sestavy.  
    >   
    >  Stav typů nasazení je agregován v podokně **Stav nasazení** . Chcete-li si zobrazit podrobnější informace o typech nasazení, použijte sestavu **Chyby infrastruktury aplikace** v kategorii sestav **Distribuce softwaru – monitorování aplikací**.  

4.  Chcete-li zkontrolovat obecné informace o stavu nasazení aplikace, vyberte nasazení a pak zvolte kartu **Souhrn** v okně **vybrané nasazení** .  

5.  Chcete-li zkontrolovat informace o typu nasazení aplikací, vyberte nasazení a pak zvolte kartu **typy nasazení** v okně **vybrané nasazení** .  

Informace zobrazené v podokně **stav nasazení** po výběru možnosti **Zobrazit stav** jsou živá data z databáze Configuration Manager. Informace zobrazené na kartě **Souhrn** a **typy nasazení** jsou shrnutá data.

Pokud se data zobrazená na kartě **Souhrn** a na kartě **typy nasazení** neshodují s daty zobrazenými v podokně **stav nasazení** , aktualizujte data na těchto kartách výběrem **možnosti Spustit souhrn** . Výchozí interval shrnutí nasazení aplikací můžete nastavit následovně:  

1. V konzole Configuration Manager klikněte na **Správa** > **Konfigurace** > lokality**lokality**.

2. V seznamu **lokality** vyberte lokalitu, pro kterou chcete nakonfigurovat interval shrnutí, a poté na kartě **Domů** ve skupině **Nastavení** zvolte možnost **Shrnutí stavu**.

3. V dialogovém okně **Shrnutí stavu** zvolte možnost **Shrnutí nasazení aplikace**a pak zvolte možnost **Upravit**.  

4. V dialogovém okně **Shrnutí nasazení aplikace – vlastnosti** nastavte požadované intervaly Shrnutí a klikněte na **tlačítko OK**.  
