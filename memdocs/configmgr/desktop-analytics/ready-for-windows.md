---
title: Připraveno pro Windows
titleSuffix: Configuration Manager
description: O vyřazení webu připraveného pro Windows
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 75dd74e3c1019c9819b44a0ffa8936eeb9eee366
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268347"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Nejčastější dotazy k vyřazení moderních desktopových prostředí

<!-- placeholder -->

## <a name="general"></a>Obecné

### <a name="what-happened-to-the-ready-for-windows-website"></a>Co se stalo s připraveným pro web Windows?

Mnohé zákazníky mají problémy s načtením a aktuálností v systému Windows 10 a Office 365 ProPlus. Primární výzvou testuje aplikace, protože tento proces je obvykle ruční. Pro správce IT a vlastníky aplikací je časově náročné, aby mohli průběžně analyzovat stávající aplikace a následně opravit problémy, které vznikají.

*Připravený pro moderní adresář desktopových* řešení, která jsou podporovaná a používána na komerčních zařízeních s Windows 10 a Office 365 ProPlus. Tento adresář pomáhá vedoucím IT, kteří berou v úvahy o nejnovějších verzích Windows 10 a Office 365 pro jejich nasazení.

Zpětná vazba od správců IT je, že chtějí tyto přehledy integrovat s nástroji, které už používají k naplánování plánů nasazení. Pomocí funkcí [Desktop Analytics](https://aka.ms/dadocs) a [připravenosti sady Office 365 proplus](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) v Configuration Manager můžete plánovat a spravovat projekty Windows 10 a Office 365 ProPlus upgrade. 

> [!Note]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

### <a name="what-is-desktop-analytics"></a>Co je Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) je cloudová služba, která se integruje s Configuration Manager. Služba poskytuje přehled a inteligentní informace, které vám pomůžou dělat podrobnější rozhodnutí o připravenosti na aktualizace koncových bodů Windows. Kombinuje data specifická pro vaši organizaci s agregovanými poznatky z milionů zařízení s Windows, která jsou připojená ke cloudovým službám Microsoftu.

-    V rámci správy ve vaší organizaci získáte komplexní zobrazení koncových bodů, aplikací a ovladačů.

-    Vyhodnoťte kompatibilitu aplikací a ovladačů s nejnovějšími aktualizacemi funkcí Windows. Získejte doporučení pro zmírnění známých problémů a rozšířené přehledy pro obchodní aplikace.

-    Využijte umělou Intelligence (AI) z cloudu Microsoftu k optimalizaci sady pilotních zařízení, která odpovídajícím způsobem reprezentují vaše celkové prostředí.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Proč mám použít desktopovou analýzu pro svoje plány nasazení Windows?

Desktop Analytics nabízí následující výhody:

-    **Inventář zařízení a softwaru**: inventarizace klíčových faktorů, jako jsou aplikace a verze Windows.

-    **Identifikace pilotního projektu**: identifikace nejmenší sady zařízení, která poskytují nejširší pokrytí faktorů. Zaměřuje se na faktory, které jsou nejdůležitější pro pilotní nasazení upgradů a aktualizací Windows. Zajištění úspěšnosti pilotního nasazení vám umožní rychleji a bez obav nasazovat rozsáhlá nasazení v produkčním prostředí.

-    **Identifikace problému**: pomocí agregovaných tržních dat spolu s daty z vašeho prostředí předpovídá možné problémy s tím, že se budou v systému Windows získávat a předávat aktuální údaje. Pak navrhuje možná omezení rizik.

-    **Configuration Manager Integration**: Cloud IT – umožňuje vaši stávající místní infrastrukturu. Tato data a analýza použijte k nasazení a správě Windows na svých zařízeních.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Co je ve službě Desktop Analytics to znamená *připraveno pro stav systému Windows* ?

**Stav přijetí** je založený na informacích z komerčních zařízení, která sdílejí data s Microsoftem. Stav je integrován s příkazy podpory od dodavatelů softwaru.

Desktop Analytics poskytuje stav přijetí pro každou verzi assetu, která se nachází v komerčních zařízeních. Tento stav nezahrnuje data ze zařízení uživatelů nebo zařízení, která nesdílejí data. Stav nemusí být zástupcem míry přijetí ve všech zařízeních s Windows 10.

Další informace najdete v tématu [posouzení kompatibility](compat-assessment.md).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Jaké prostředky získávají stav *připravenosti na Windows* v Desktop Analytics? 

V nástroji Desktop Analytics jsou prostředky připravené na stav *systému Windows* , pokud:

-    Poskytovatel softwaru deklaruje podporu pro řešení.
-    Zákazníci je nasadili na velký počet komerčních zařízení s Windows 10, která sdílí informace s Microsoftem.
-    Asset je relevantní pro komerční uživatele.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Jaké další přehledy se zobrazují v Desktop Analytics?

Desktop Analytics nabízí inventář [zařízení a jejich nainstalovaných aplikací](about-assets.md)a také [Pokročilé přehledy](compat-assessment.md#advanced-insights) pro obchodní aplikace. 

## <a name="software-providers"></a>Poskytovatelé softwaru

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>Můžu v nástroji Desktop Analytics dál uvést řešení softwaru?

Publikujte příkaz podpory, který váš produkt pracuje s 32-bit nebo 64 Windows 10 nebo Office 365 ProPlus. Pokud chcete prezentovat vaše řešení v Desktop Analytics, obraťte se na kontakt Microsoftu.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Jak mám v seznamu využít moje řešení?

Tisíc správců IT spravuje miliony zařízení s Configuration Manager a desktopovou analýzou. Používají tyto nástroje k bezproblémovému naplánování a upgradu svých organizací na nejnovější verzi Windows 10 a Office 365 ProPlus. Používají je také k rozhodování o nákupu pro softwarová řešení.

Společnost Microsoft integruje příkazy podpory od dodavatelů softwaru s informacemi o přijetí, které obdrží z komerčních zařízení. Organizace po celém světě pak používají tato data v Desktop Analytics a nástrojích připravenosti Office. 

Pokud vaše příkazy podpory nejsou správně přidruženy k assetům, obraťte se na kontakt společnosti Microsoft.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Můžu na svých aktivech zobrazit podrobné metriky výkonu?

Vyhodnoťte výkon svých řešení pomocí sestav stavů a metrik prostřednictvím centra pro vývojáře: 

- [Windows Store](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [Plocha](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Doplňky pro Office](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Jak můžu vyvíjet kompatibilní prostředky pro Windows 10 a Office 365 ProPlus?

Ujistěte se, že vaše desktopové aplikace jsou teď kompatibilní a jsou v budoucnu kompatibilní s Windows 10. Další informace najdete v tématu [Kompatibilita aplikací pro vývojáře](https://developer.microsoft.com/windows/desktop/app-compatibility).

Pokud vyvíjíte řešení pro Office 365 ProPlus, přečtěte si téma [osvědčené postupy vývoje pro Doplňky COM, VSTO a VBA v Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).
