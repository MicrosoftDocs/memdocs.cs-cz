---
title: Monitorování nastavení dodržování předpisů
titleSuffix: Configuration Manager
description: Pomocí jednoho nebo více postupů v tomto tématu zobrazíte stav dodržování předpisů u standardních hodnot konfigurace.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 839c08c8782a815703a19999bf1315fd65980ed8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712292"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Monitorování nastavení dodržování předpisů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po nasazení Configuration Manager standardních hodnot konfigurace do zařízení ve vaší hierarchii můžete použít jeden nebo více postupů v tomto tématu a zobrazit tak stav dodržování předpisů pro standardní hodnoty konfigurace:

> [!NOTE]  
>  Pole ověřovacích kritérií v sestavách nastavení dodržování předpisů (ekvivalent v sestavě na straně klienta je **Omezení**) zobrazí základní jazyk SML (Service Modeling Language). To může ztížit správcům, kteří vytvořili položku konfigurace v konzole Configuration Manager, aby porozuměli tomu, co kritéria ověření jsou, pokud nemají znalosti SML. V takovém případě pomocí pracovního prostoru **monitorování** v konzole Configuration Manager zobrazíte vlastnosti položky konfigurace a její ověřovací kritéria.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Zobrazení výsledků kontroly kompatibility v konzole nástroje Configuration Manager  
 Tento postup slouží k zobrazení podrobností o kompatibilitě nasazených standardních hodnot konfigurace v konzole Configuration Manager.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Zobrazení výsledků kontroly kompatibility v konzole nástroje Configuration Manager  

1.  V konzole Configuration Manager klikněte na **monitorování** > **nasazení**.  

3.  V seznamu **Nasazení** vyberte nasazení standardních hodnot konfigurace, u kterých chcete zkontrolovat informace o dodržování předpisů.  

4.  Na hlavní stránce můžete zkontrolovat souhrnné informace o dodržování předpisů nasazení standardních hodnot konfigurace. Pokud chcete zobrazit podrobnější informace, vyberte nasazení standardních hodnot konfigurace a potom na kartě **Domů** klikněte ve skupině **Nasazení** na **Zobrazit stav** a otevřete stránku **Stav nasazení** .  

     Na stránce **Stav nasazení** naleznete následující karty:  

    -   **Kompatibilní:** Zobrazuje dodržování předpisů standardních hodnot konfigurace podle počtu ovlivněných prostředků. Kliknutím na pravidlo můžete vytvořit dočasný uzel v uzlu **Uživatelé** nebo **Zařízení** v pracovním prostoru **Prostředky a kompatibilita**, který bude obsahovat všechny uživatele nebo zařízení kompatibilní s tímto pravidlem. V podokně **Podrobnosti o aktivech** jsou zobrazení uživatelé nebo zařízení kompatibilní se standardními hodnotami konfigurace. Dvojím kliknutím na uživatele nebo zařízení v seznamu zobrazíte další informace.  

        > [!IMPORTANT]  
        >  Pravidlo položky konfigurace není vyhodnoceno, pokud nebylo zjištěno nebo není použitelné na klientském zařízení. pravidlo se ale vrátí jako vyhovující.  

    -   **Chyba**: Zobrazuje seznam všech chyb pro vybrané nasazení standardních hodnot konfigurace podle počtu ovlivněných prostředků. Kliknutím na pravidlo můžete vytvořit dočasný uzel v uzlu **Uživatelé** nebo **Zařízení** v pracovním prostoru **Prostředky a kompatibilita**, který bude obsahovat všechny uživatele nebo zařízení, kteří vytvořili chyby s tímto pravidlem. Po výběru uživatele nebo zařízení se v podokně **Podrobnosti o aktivech** zobrazí uživatelé nebo zařízení, na které se vztahuje vybraný problém. Dvojím kliknutím na uživatele nebo zařízení v seznamu zobrazíte další informace o problému.  

    -   **Nekompatibilní:** Zobrazuje seznam všech pravidel nesplňujících požadavky ve standardních hodnotách konfigurace podle počtu ovlivněných prostředků. Kliknutím na pravidlo můžete vytvořit dočasný uzel v uzlu **Uživatelé** nebo **Zařízení** pracovního prostoru **Prostředky a kompatibilita**, který bude obsahovat všechny uživatele nebo zařízení nekompatibilní s tímto pravidlem. Po výběru uživatele nebo zařízení se v podokně **Podrobnosti o aktivech** zobrazí uživatelé nebo zařízení, na které se vztahuje vybraný problém. Dvakrát klikněte na uživatele nebo zařízení v seznamu a zobrazte další informace o problému.  

    -   **Neznámé:** Zobrazuje seznam všech uživatelů a zařízení, u kterých není nahlášená kompatibilita pro vybrané nasazení standardních hodnot konfigurace, spolu s aktuálním stavem klienta zařízení.  

5.  Na stránce **Stav nasazení** lze zobrazit podrobné informace o kompatibilitě nasazených standardních hodnot konfigurace. V uzlu **Nasazení** se vytvoří dočasný uzel, který vám znovu pomůže rychle najít tyto informace.  

##  <a name="view-compliance-results-by-using-reports"></a>Zobrazení výsledků dodržování předpisů pomocí sestav  
 Nastavení dodržování předpisů v Configuration Manager zahrnuje řadu předdefinovaných sestav, které umožňují monitorovat informace o položkách konfigurace, standardních hodnotách konfigurace a nasazeních. Tyto sestavy obsahují kategorii sestav **Správa nastavení a kompatibility**.  

> [!IMPORTANT]  
>  Při použití parametrů **Filtr zařízení** a**%** filtr uživatelů v sestavách nastavení dodržování předpisů je nutné použít zástupný znak ().  

 Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Zobrazení výsledků dodržování předpisů na Configuration Manager klientském počítači s Windows

> [!NOTE]  
>  Pokud jste přihlášeni pomocí účtu hosta domény, nemůžete zobrazit informace o Configuration Manager klientovi Windows.    

1.  Na ovládacím panelu klientského počítače přejděte ke **Configuration Manageru** a pak dvojím kliknutím otevřete jeho vlastnosti.  

2.  Klikněte na kartu **Konfigurace** a zobrazte seznam nasazených standardních hodnot konfigurace.  

3.  Zobrazte **Stavu dodržování předpisů** pro každé standardní hodnoty konfigurace:  

    > [!IMPORTANT]  
    >  Výsledky hodnocení jsou uložené v mezipaměti klienta na 15 minut. Pokud spustíte nové hodnocení během 15 minut, výsledky dodržování předpisů se vrátí z mezipaměti a nedělá se hodnocení znova. Proto pokud uděláte na klientovi změnu, která může ovlivnit výsledky hodnocení dodržování předpisů, počkejte před zahájením nového hodnocení na uplynutí 15 minut.  

    -   **Kompatibilní**: Klientský počítač je kompatibilní s hodnocenými standardními hodnotami konfigurace.  

    -   **Nekompatibilní**: Klientský počítač není kompatibilní s hodnocenými standardními hodnotami konfigurace.  

    -   **Neznámý**: Pro klientský počítač se zatím nevyhodnocovaly standardní hodnoty konfigurace. Pokud chcete zahájit hodnocení mimo plán vyhodnocení shody, vyberte standardní hodnoty konfigurace, které chcete vyhodnotit, a pak klikněte na **Vyhodnotit**.  

        > [!NOTE]  
        >  Pokud máte na klientském počítači přihlašovací údaje místního správce, můžete zobrazit podrobnosti pro každé standardní hodnoty konfigurace a určit, která položka konfigurace hlásí nekompatibilní stav. Pokud chcete to provést, vyberte standardní hodnoty konfigurace a pak klikněte na **Zobrazit sestavu**.  

4.  Klikněte na tlačítko **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Vytvoření kolekcí na základě dodržování předpisů standardních hodnot konfigurace  
 Pomocí následujícího postupu můžete vytvořit kolekci Configuration Manager založenou na zařízeních se zadaným dodržováním předpisů. Můžete vytvořit kolekce založené na následujících stavech dodržováním předpisů:  

-   **Odpovídající**  

-   **Chyba**  

-   **Nedodržující předpisy**  

-   **Není známo**  

1.  V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů** > **Nastavení** > dodržování předpisů**standardní hodnoty konfigurace**.  

3.  V seznamu **Standardní hodnoty konfigurace** vyberte standardní hodnoty konfigurace, ze kterých chcete vytvořit kolekci.  

4.  Na kartě **Nasazení** v části **Skupina nasazení**klikněte na **Vytvořit novou kolekci** a pak v rozevíracím seznamu vyberte úroveň dodržování předpisů, pro kterou chcete kolekci vytvořit.  

5.  Otevře se **Průvodce vytvořením uživatelské kolekce** nebo **Průvodce vytvořením kolekce zařízení** , v závislosti na tom, jestli je položka konfigurace nasazená na uživatele, nebo na zařízení. V průvodci se automaticky vyplní správné hodnoty pro vytvoření kolekce, ale můžete je ještě upravit.  

6.  Po dokončení průvodce se kolekce zobrazí v uzlu **Kolekce uživatelů** nebo **Kolekce zařízení** v pracovním prostoru **Prostředky a kompatibilita** .  
