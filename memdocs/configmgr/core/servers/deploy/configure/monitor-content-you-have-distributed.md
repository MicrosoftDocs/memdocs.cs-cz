---
title: Monitorování obsahu
titleSuffix: Configuration Manager
description: Zjistěte, jak monitorovat distribuovaný obsah pomocí konzoly Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110011"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Monitorování obsahu, který distribuujete pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí konzoly Configuration Manager můžete monitorovat distribuovaný obsah, včetně:  

- Stav všech typů balíčků přidružených distribučních bodů.  
- Stav ověření obsahu pro obsah v balíčku.  
- Stav obsahu přiřazeného ke konkrétní skupině distribučních bodů.  
- Stav obsahu přiřazeného k distribučnímu bodu.  
- Stav volitelných funkcí pro jednotlivé distribuční body (ověření obsahu, technologie PXE a vícesměrové vysílání).  

> [!NOTE]  
> Configuration Manager pouze monitoruje obsah v distribučním bodě, který je v knihovně obsahu. Nemonitoruje obsah uložený v distribučním bodě v balíčku nebo vlastní sdílené složky.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitorování stavu obsahu

Uzel **Stav obsahu** v pracovním prostoru **Monitorování** poskytuje informace o balíčcích obsahu. V konzole Configuration Manager zkontrolujte informace jako:  

- Název balíčku, typ a ID
- Počet distribučních bodů, na které byl balíček odeslán
- Míra dodržování předpisů
- Po vytvoření balíčku
- Verze zdroje

Najdete zde také podrobné informace o stavu pro každý balíček, včetně těchto:  

- Stav distribuce
- Počet selhání
- Probíhající distribuce  
- Počet instalací

Můžete také spravovat distribuce, které zůstávají v průběhu, do distribučního bodu nebo které selhaly při úspěšné distribuci obsahu do distribučního bodu:  

- Možnost buď zrušit nebo znovu distribuovat obsah je k dispozici při zobrazení stavové zprávy o nasazení distribuční úlohy do distribučního bodu v podokně Podrobnosti o **aktivech** . Toto podokno lze najít buď na kartě **probíhá** , nebo na kartě **Chyba** uzlu **stav obsahu** .  
- Kromě toho se v podrobnostech úlohy zobrazí procento úlohy, která se dokončila při zobrazení podrobností úlohy na kartě **probíhá** . V podrobnostech úlohy se zobrazí také počet opakovaných pokusů, které pro úlohu zůstanou. Když si zobrazíte podrobnosti o úloze na kartě **chyby** , zobrazí se doba, po jejímž uplynutí dojde k dalšímu opakování.  

Pokud zrušíte nasazení, které ještě není dokončené, bude distribuční úloha přenos tohoto obsahu zastavena:  

- Stav nasazení se pak aktualizuje, aby označoval, že se distribuce nezdařila a že byla zrušena akcí uživatele.  
- Tento nový stav se zobrazí na kartě **Chyba** .  

> [!NOTE]  
> Je-li nasazení téměř dokončené, je možné akci zrušit, pokud se distribuce nebude zpracovávat před dokončením distribuce do distribučního bodu. V takovém případě se akce pro zrušení nasazení ignoruje a stav nasazení se zobrazí jako úspěšný.  
>
> I když můžete vybrat možnost zrušení distribuce do distribučního bodu, který je umístěn na serveru lokality, nemá to žádný vliv. Důvodem je to, že server lokality a distribuční bod na serveru lokality sdílí stejné úložiště obsahu s jedinou instancí. Neexistuje žádná skutečná distribuční úloha, kterou by bylo možné zrušit.  

Když znovu distribuujete obsah, který se dřív nepodařilo přenést do distribučního bodu, Configuration Manager okamžitě zahájí opětovné nasazení tohoto obsahu do distribučního bodu. Configuration Manager aktualizuje stav nasazení tak, aby odráželo nepřetržitý stav tohoto opětovného nasazení.  

### <a name="tasks-to-monitor-content"></a>Úlohy pro monitorování obsahu

1. V konzole Configuration Manager klikněte na pracovní prostor **monitorování** , rozbalte položku **stav distribuce**a potom vyberte uzel **stav obsahu** . V tomto uzlu se zobrazují balíčky.  

2. Vyberte balíček, který chcete spravovat.  

3. Na kartě **Domů** na pásu karet ve skupině **obsah** vyberte **Zobrazit stav**. Konzola zobrazuje podrobné informace o stavu balíčku.

Pro další akce pokračujte v jedné z následujících částí:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Zrušení distribuce, která stále probíhá  

1. Přepněte na kartu **probíhá** .

2. V podokně **Podrobnosti o aktivech** klikněte pravým tlačítkem myši na položku distribuce, kterou chcete zrušit, a vyberte možnost **Zrušit**.  

3. Vyberte **Ano** , pokud chcete akci potvrdit a zrušit úlohu distribuce do tohoto distribučního bodu.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Znovu distribuovat obsah, který se nepodařilo distribuovat  

1. Přepněte na kartu **chyby** .

2. V podokně **Podrobnosti o aktivech** klikněte pravým tlačítkem myši na položku distribuce, kterou chcete znovu distribuovat, a vyberte možnost znovu **distribuovat**.  

3. Výběrem možnosti **Ano** potvrďte akci a spusťte proces Redistribuce do tohoto distribučního bodu.  


## <a name="distribution-point-group-status"></a>Stav skupiny distribučních bodů

Uzel **Stav skupiny distribučních bodů** v pracovním prostoru **Sledování** poskytuje informace o skupinách distribučních bodů. Můžete zkontrolovat podobné informace:  

- Název skupiny distribučních bodů, popis a stav
- Počet distribučních bodů, které jsou členy skupiny distribučních bodů
- Kolik balíčků bylo přiřazeno ke skupině
- Míra dodržování předpisů

Zobrazí se také následující podrobné informace o stavu:  

- Chyby pro skupinu distribučních bodů  
- Kolik distribucí probíhá
- Počet úspěšně distribuovaných  

### <a name="monitor-distribution-point-group-status"></a>Monitorovat stav skupiny distribučních bodů  

1. V konzole Configuration Manager přejděte do pracovního prostoru **monitorování** , rozbalte položku **stav distribuce**a potom vyberte uzel **stav skupiny distribučních bodů** . Zobrazí se skupiny distribučních bodů.  

2. Vyberte skupinu distribučních bodů, pro kterou chcete získat podrobné informace o stavu.  

3. Na kartě **Domů** na pásu karet vyberte **Zobrazit stav**. Zobrazí podrobné informace o stavu skupiny distribučních bodů.  


## <a name="distribution-point-configuration-status"></a>Stav konfigurace distribučního bodu

Uzel **Stav konfigurace distribučního bodu** v pracovním prostoru **Sledování** poskytuje informace o distribučním bodu. Můžete zkontrolovat, které atributy jsou povoleny pro distribuční bod, jako je například technologie PXE, vícesměrové vysílání a ověření obsahu. Zkontrolujte také stav distribuce distribučního bodu.

> [!WARNING]  
> Stav konfigurace distribučního bodu je relativní vzhledem k uplynulým 24 hodinám. Pokud distribuční bod obsahuje chybu a obnovuje se, může se stav chyby zobrazit po dobu až 24 hodin po obnovování distribučního bodu.  

### <a name="monitor-distribution-point-configuration-status"></a>Monitorování stavu konfigurace distribučního bodu  

1. V konzole Configuration Manager přejděte do pracovního prostoru **monitorování** , rozbalte položku **stav distribuce**a potom vyberte uzel **stav konfigurace distribučního bodu** .  

2. Vyberte distribuční bod.  

3. V podokně výsledků přepněte na kartu **Podrobnosti** . Zobrazí informace o stavu distribučního bodu.  


## <a name="client-data-sources-dashboard"></a>Řídicí panel zdrojů dat klienta

Pomocí řídicího panelu **zdroje dat klientů** můžete lépe pochopit, odkud Klienti získávají obsah ve vašem prostředí. Řídicí panel začne zobrazovat data poté, co klienti stáhnou obsah a oznamují tyto informace zpět do lokality. Tento proces může trvat až 24 hodin.

> [!Note]  
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Než použijete funkci **sdílené mezipaměti klienta** , je nutné ji povolit. Další informace naleznete v části [Enable optional features from updates](../../manage/install-in-console-updates.md#bkmk_options).  

V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **stav distribuce**a vyberte uzel **klientské zdroje dat** . Vyberte časové období, které se má použít na řídicí panel. Pak vyberte skupinu hranic, pro kterou chcete zobrazit informace. Najetím myší na dlaždice můžete zobrazit další podrobnosti o různých zdrojích obsahu nebo zásad.

K zobrazení souhrnu zdrojů dat klientů pro každou skupinu hranic můžete také použít sestavu **klientské zdroje dat – souhrn**.

### <a name="dashboard-tiles"></a>Dlaždice řídicího panelu

Řídicí panel obsahuje tyto dlaždice:  

#### <a name="client-content-sources"></a>Zdroje obsahu klienta

Zobrazuje zdroje, ze kterých klienti získali obsah:

- Distribuční bod
- [Distribuční bod cloudu](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [Služba BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Sdílená mezipaměť](../../../plan-design/hierarchy/client-peer-cache.md)
- [Optimalizace doručení](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (počínaje verzí 1906)<sup>[Poznámka 1](#bkmk_note1)</sup>
- Microsoft Update: zařízení hlásí tento zdroj, když Configuration Manager klient stáhne aktualizace softwaru z cloudových služeb Microsoftu. Mezi tyto služby patří Microsoft Update a Microsoft 365 aplikace pro podniky.

![Dlaždice zdroje obsahu klienta na řídicím panelu](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Počínaje verzí 1906<!--3555759-->Pokud chcete na tomto řídicím panelu zahrnout optimalizaci doručování, proveďte následující akce:
>
> - Nakonfigurujte nastavení klienta a **Povolte instalaci expresních aktualizací na klientech** ve skupině aktualizace softwaru.
>
> - Nasazení aktualizací Windows 10 Express
>
> Další informace najdete v tématu [Správa souborů Expresní instalace pro aktualizace Windows 10](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Distribuční body

Zobrazí počet distribučních bodů, které jsou součástí vybrané skupiny hranic.

#### <a name="clients-that-used-a-distribution-point"></a>Klienti, kteří použili distribuční bod

Z počtu klientů, kteří jsou ve vybrané skupině hranic, tato dlaždice ukazuje, kolik z distribučního bodu se k získání obsahu používalo.

#### <a name="peer-cache-sources"></a>Zdroje sdílené mezipaměti

V případě vybrané skupiny hranic tato dlaždice ukazuje, kolik zdrojů sdílené mezipaměti oznámilo stažení Historie.

#### <a name="clients-that-used-a-peer"></a>Klienti, kteří používali partnera

Z počtu klientů, kteří jsou ve vybrané skupině hranic, tato dlaždice zobrazuje, kolik z nich použil zdroj sdílené mezipaměti k získání obsahu.

#### <a name="top-distributed-content"></a>Horní distribuovaný obsah

Nejvíce distribuované balíčky podle typu zdroje
