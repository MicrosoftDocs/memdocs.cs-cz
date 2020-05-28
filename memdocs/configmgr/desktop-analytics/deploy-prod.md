---
title: Jak nasadit do produkčního prostředí
titleSuffix: Configuration Manager
description: Návod pro nasazení do produkční skupiny Desktop Analytics
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0a7ffe8eea1048e696ce7dd254d58364226efc58
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268776"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Nasazení do produkčního prostředí s využitím Desktop Analytics

Po [nasazení na pilotní nasazení](deploy-pilot.md) a kontrole stavu vašich assetů jste připraveni aktualizovat zbývající část produkčního prostředí.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Nasazení aktualizací do produkčních zařízení se dá provést třemi hlavními částmi:

1. [Projděte si materiály, které potřebují rozhodnutí o upgradu](#bkmk_review): Pokud chcete, aby byla zařízení připravená pro produkční nasazení, musí jejich prostředky mít rozhodnutí o upgradu nastavené na **připravené** nebo **připravené, požadované opravy**.  

2. [Nasadit do zařízení, která jsou připravená](#bkmk_deploy): pomocí Configuration Manager aktualizujte zařízení, která jsou připravená. Desktop Analytics nabízí seznam zařízení připravených pro produkční nasazení a sestavy pro monitorování úspěchu nasazení.  

3. [Monitorovat stav aktualizovaných zařízení](#bkmk_monitor): v průběhu nasazení aktualizace Sledujte stav důležitých prostředků. Pokud je potřeba věnovat pozornost, vyřešte potíže a opravte je. Pokud se rozhodnete potíže vyřešit, zastavte nasazení ovlivněným zařízením nastavením rozhodnutí o upgradu na **nemožné**.  

> [!NOTE]  
> Když jste si jistí úspěch pilotního nasazení, spusťte nasazení v produkčním prostředí kdykoli. Neexistuje žádný požadavek, aby všechna pilotní zařízení nejdřív dosáhla stavu "dokončeno".  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a>Kontrola prostředků, které potřebují rozhodnutí o upgradu

Pomocí nástroje Desktop Analytics Vás provedeme procesem kontroly vašich prostředků pro produkční nasazení. V Azure Portal přejděte na **plány nasazení**, vyberte plán nasazení a v nabídce vlevo vyberte **připravit produkci** .

![Snímek obrazovky Příprava výrobního zobrazení v Desktop Analytics](media/prepare-production.png)

Zkontrolujte stav svých aplikací. Tyto informace slouží k nastavení rozhodnutí o upgradu pro každý z těchto prostředků.

Jednotlivé karty můžete použít ke kontrole stavu aplikací. V každém zobrazení s kartami můžete filtrovat výsledky a zobrazit zařízení, která jsou sledována pro upgrade, vyžadovat vaši pozornost, zařízení se smíšenými výsledky a tato zařízení v neurčitém stavu.

Vyberte **cíle schůzky** , abyste mohli filtrovat zobrazení na prostředky, které jsou pro produkční nasazení nejspíš připravené na provozní nasazení, a to na základě následujících kritérií:

- Riziko: posouzení známých rizik před upgradem pro aktualizace zařízení, která mají tento prostředek nainstalovaný  

- Stav: posouzení po upgradu zařízení v jiných nasazeních a to, jestli při instalaci aktualizace došlo k potížím. Další informace o stavu najdete v tématu [monitorování stavu aktualizovaných zařízení](#bkmk_monitor).  

Chcete-li schválit prostředek pro upgrade, vyberte název v seznamu a vyberte jednu z následujících možností v seznamu **rozhodnutí o upgradu** :

- Probíhá kontrola
- Připraveno
- Připraveno (s nápravou)
- Možné
- Nerevidováno

Chcete-li nastavit tuto hodnotu pro více aplikací najednou, **Vyberte tuto položku**pomocí prvního sloupce a pak zvolte možnost **nastavit rozhodnutí o upgradu**.

![Nastavení možnosti rozhodování o upgradu ve více aplikacích](media/prep-prod-set-upgrade-decision.png)

Vyberte **žádná data** pro zobrazení prostředků, které nemohly být klasifikovány. Obecně se jedná o prostředky, které nemají dostatečné pokrytí pro desktopovou analýzu, aby bylo možné provést analýzu rizika nebo stavu. Pro zlepšení pokrytí přidejte další zařízení s těmito prostředky do pilotního projektu, nebo požádejte uživatele pilotního nasazení, aby vyzkoušeli tyto prostředky.

V případě **potřeby pozornosti** nebo **smíšeného výsledků** můžou být také prostředky. Tyto prostředky mohou vyžadovat další kontrolu před provedením rozhodnutí o upgradu.

Zkontrolujte všechny aplikace. Jakmile má dané zařízení kladné rozhodnutí o upgradu pro všechny prostředky, změní se jeho stav na připravené pro produkční prostředí. Seznamte se s aktuálním počtem na hlavní stránce pro plán nasazení tak, že vyberete třetí krok nasazení, **nasadíte**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a>Nasadit do zařízení, která jsou připravená

Configuration Manager používá data z Desktop Analytics k vytvoření kolekce pro produkční nasazení. Nesaďte pořadí úkolů s použitím tradičního nasazení. Pomocí následujícího postupu vytvoříte nasazení integrované na Desktop Analytics:

Pokud jste postupovali podle doporučeného postupu [nasazení do pilotních zařízení](deploy-pilot.md#deploy-to-pilot-devices), je Configuration Manager dvoufázové nasazení připravené. Když označíte prostředky jako *připravené*, analýza plochy tato zařízení automaticky synchronizuje s Configuration Manager. Tato zařízení se pak přidají do produkční kolekce. Když se dvoufázové nasazení přesune do druhé fáze, tato produkční zařízení dostanou nasazení upgradu.

Pokud jste nakonfigurovali postupné nasazení na **Ruční zahájení druhé fáze nasazení**, musíte ho ručně přesunout do další fáze. Další informace najdete v tématu [Správa a monitorování postupného nasazení](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Pokud jste v pilotní kolekci vytvořili jedno nasazení integrované na Desktop Analytics, musíte tento postup opakovat pro nasazení do produkční kolekce.


### <a name="address-deployment-alerts"></a>Výstrahy nasazení adres

V rámci pilotního nasazení vás Analytics desktopu radí s případnými problémy, které vyžadují vaši pozornost během produkčního nasazení. V části Desktop Analytics přejděte na plán nasazení a v nabídce vlevo vyberte **stav nasazení** . V zobrazení stav nasazení jsou uvedena zařízení v následujících kategoriích:  

- Nezahájeno
- Rozpracované
- Dokončeno
- Potřebuje pozornost – zařízení (seřazené podle názvu zařízení)
- Vyžaduje problémy s pozorností (seřazené podle typu vydání)

![Snímek obrazovky se stavem nasazení produkčního prostředí Desktop Analytics](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a>Monitorování stavu aktualizovaných zařízení

Stránka **připravit produkci** se zaměřuje na to, aby vám usnadnila rozhodování o upgradu vašich assetů. Tato stránka ve výchozím nastavení zobrazuje pouze prostředky, které ještě nejsou ve stavu **připraveno** . Na stránce **monitorovat stav** se zobrazují problémy se stavem u všech prostředků zajímavosti, a to i u prostředků, které jsou označené jako **připravené**. Pokud zjistí problémy, můžete problém vyřešit a opravit nebo změnit rozhodnutí o upgradu na **nemožné**. Když změníte rozhodnutí o upgradu, tato akce zabrání budoucím inovacím na zařízeních s tímto prostředkem.

Filtrovat tuto stránku podle assetů s následujícími stavy:

| Filtr stavu | Description |
|----------------------|-------------|
| **Nutná pozornost** | (Výchozí filtr) Desktop Analytics detekuje statisticky významnou regresi pro určitou metriku stavu tohoto prostředku.
| **Cíle schůzky** | Desktop Analytics nedetekuje žádné regrese v chování |
| **Nedostatečné údaje** | Desktop Analytics nemá k dispozici dostatek dat o tomto prostředku, aby mohla dělat doporučení. |
| **Žádná data** | Pro tento prostředek ještě nejsou k dispozici žádná data o využití. |

Chcete-li zobrazit nefiltrované zobrazení všech prostředků, vyberte aktuální filtr. Tato akce odebere filtr.

> [!NOTE]  
> Aby se snížil počet prostředků s nedostatečnými daty, Analytics Desktop monitoruje prostředky na všech vašich zařízeních, která se upgradují na cílovou verzi Windows zadanou v plánu nasazení. Mezi tato zařízení patří ty, které nejsou zahrnuté do konkrétního plánu nasazení.  

Výchozím pořadím řazení je počet zařízení, u kterých došlo k incidentu tohoto konkrétního prostředku, takže můžete rychle zjistit, které z nich způsobují nejvíce problémů. Například při zobrazení **aplikací**se seřadí podle **zařízení s chybami aplikace za poslední dva týdny**.

Pokud chcete zkontrolovat stav pro všechny prostředky, i ty, které s nedostatečnými daty pro desktopovou analýzu slouží k zajištění statistických odvození, použijte následující postup:

1. Vyberte rozevírací seznam u **zařízení s incidenty ve sloupci poslední dva týdny** . Přidejte filtr jenom na ty prostředky, které mají incidenty na některém minimálním počtu zařízení, která jsou zajímavá. Můžete například zobrazit položky s hodnotami **vyššími než** 100.  

2. Vyberte rozevírací seznam v části **% zařízení s incidenty ve sloupci poslední dva týdny** a vyberte možnost řazení **sestupně**.  

    Výsledné zobrazení ukazuje prostředky s nejvyšší mírou incidentu s minimálním počtem incidentů.  

3. Vyberte Asset, pro který chcete získat další podrobnosti, nebo změňte jeho rozhodnutí o upgradu.  

Další informace najdete v tématu [monitorování stavu](health-status-monitoring.md)stavu.
