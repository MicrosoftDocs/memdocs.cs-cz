---
title: Použití časových období údržby
titleSuffix: Configuration Manager
description: Pomocí oken kolekce a údržby můžete efektivně spravovat klienty v Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 06bb88368c6c958adc8fdefd336307d9b2924d31
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693093"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Použití časových období údržby v systému Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Časová období údržby použijte k definování, kdy Configuration Manager můžou spouštět úlohy, které mají vliv na zařízení. Časová období údržby vám pomůžou zajistit, aby změny konfigurace klientů probíhaly v časech, které neovlivňují produktivitu. Pomocí centra softwaru můžou uživatelé na kartě **stav instalace** zobrazit další okno údržby zařízení. <!--1358131-->

Následující úlohy podporují časové intervaly pro správu a údržbu:

- Nasazení aplikací a balíčků

- Nasazení aktualizací softwaru

- Nasazení a vyhodnocení nastavení dodržování předpisů

- Nasazení operačního systému a vlastního pořadí úkolů

Nakonfigurujte časové intervaly pro správu a údržbu pomocí data účinnosti, počátečního a koncového času a způsobu opakování. Maximální doba trvání okna musí být kratší než 24 hodin. Konzola nepovoluje jedno časové období údržby delší než 24 hodin. Například pokud chcete, aby byla údržba pokaždé sobota a neděle, pak pro každý den vytvoříme časová období údržby 2 24 hodin.<!-- MEMDocs#310 -->

Ve výchozím nastavení se restart počítače způsobený nasazením nepovoluje mimo časové období údržby, ale můžete přepsat výchozí. Časová období údržby mají vliv jenom na čas, kdy se nasazení spouští. Nasazení, která konfigurujete pro stahování a spouštění místně, můžou stahovat obsah mimo okno.

Když je klient členem kolekce zařízení, která má okno údržby, nasazení se spustí pouze v případě, že maximální povolená doba běhu nepřesáhne dobu trvání okna. Pokud se nasazení nepovede spustit, klient vygeneruje výstrahu. Pak znovu spustí nasazení během příštího plánovaného časového období údržby, které má dostupný čas.

## <a name="multiple-maintenance-windows"></a>Více oken údržby

Když je klientský počítač členem více kolekcí zařízení s časovými intervaly pro správu a údržbu, platí tato pravidla:  

- Pokud se okna údržby nepřekrývají, klient je považuje za dva nezávislé časové intervaly pro správu a údržbu.

- Pokud se časové intervaly pro správu a údržbu překrývají, klient je považuje za jedno okno pro celou dobu obou oken. V kolekci můžete například vytvořit dvě časová období údržby. První je platný od 6:00 do 7:00 a druhá je platná z 6:30 až 7:30. Vzhledem k tomu, že se překrývají po dobu 30 minut, je efektivní doba trvání kombinovaného časového období údržby 90 minut od 6:00 do 7:30.

Když uživatel nainstaluje aplikaci z centra softwaru, klient ji okamžitě spustí. Určuje prioritu záměru uživatele v rámci správce.

Pokud nasazení aplikace s účelem **požadované** dosáhne konečného termínu instalace v době mimo pracovní dobu, kterou uživatel nakonfiguruje v centru softwaru, klient nainstaluje aplikaci. Přinese prioritu záměr správce přes uživatele.

Ve výchozím nastavení s více časovými intervaly pro správu a údržbu klient nainstaluje jenom aktualizace softwaru v oknech typu **aktualizace softwaru** . Ignoruje všechna okna údržby **nasazení** , pokud se nejedná o jediný typ. Toto chování můžete nakonfigurovat pomocí následujícího nastavení klienta ve skupině **aktualizace softwaru** : **Povolit instalaci aktualizací softwaru v okně údržby všechna nasazení, když je k dispozici okno Údržba aktualizace softwaru**. Další informace najdete v tématu [informace o nastavení klienta](../../deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs#1317 -->

> [!NOTE]
> Toto nastavení platí i pro časové intervaly pro správu a údržbu, které nakonfigurujete pro **pořadí úkolů**.<!-- SCCMDocs-pr #4596 -->
>
> Pokud má klient k dispozici pouze okno **všechna nasazení** , bude nadále instalovat aktualizace softwaru nebo sekvence úloh v tomto okně.

## <a name="configure-maintenance-windows"></a>Konfigurace oken údržby

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** .

1. Vyberte uzel **kolekce zařízení** a pak vyberte kolekci.

    > [!NOTE]
    > Pro kolekci **všechny systémy** nelze vytvořit časová období údržby.

1. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.

1. Přepněte na kartu časové intervaly pro **správu a údržbu** a vyberte ikonu **Nová** .

    1. Zadejte **název** pro jedinečné identifikaci tohoto časového období údržby pro kolekci.

    1. Nakonfigurujte nastavení **času** :

        - **Datum účinnosti**: datum, kdy se spouští časová období údržby. Výchozí hodnota je aktuální datum.

        - **Začátek** a **konec**: začátek a konec časového intervalu pro správu a údržbu. Vypočítá **dobu trvání** okna. Minimální doba trvání je pět minut a maximální hodnota je 24 hodin. Výchozí doba trvání je tři hodiny, od 01:00 do 04:00.

        - **Koordinovaný světový čas (UTC)**: tuto možnost povolte, aby klient mohl interpretovat čas zahájení a ukončení v časovém pásmu UTC. V případě regionálních nebo globálně distribuovaných zařízení ve stejné kolekci Tato možnost nastaví časové období údržby, které se má provádět současně na všech zařízeních v kolekci. Tuto možnost zakažte, aby klient používal místní časové pásmo zařízení. Tato možnost je ve výchozím nastavení zakázána.

    1. Nakonfigurujte způsob opakování. Výchozí hodnota je jednou týdně v aktuálním dni v týdnu.

    1. **Použít tento plán na**: ve výchozím nastavení se okno vztahuje na **všechna nasazení**. Můžete vybrat buď **aktualizace softwaru** , nebo **pořadí úkolů** , abyste mohli dále řídit, jaká nasazení budou během tohoto okna spuštěna.

        > [!TIP]
        > Pokud nakonfigurujete více oken údržby různých typů ve stejné kolekci, ujistěte se, že rozumíte chování klienta. Další informace najdete v tématu [více oken údržby](#multiple-maintenance-windows).

1. Kliknutím na **tlačítko OK** uložte a zavřete okno.

Na kartě časové intervaly pro **správu a údržbu** vlastností kolekce se zobrazí všechna nakonfigurovaná okna.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a> Použití PowerShellu

PowerShell se dá použít ke konfiguraci časových období údržby. Další informace najdete v následujících článcích:

- [Get-CMMaintenanceWindow](/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)