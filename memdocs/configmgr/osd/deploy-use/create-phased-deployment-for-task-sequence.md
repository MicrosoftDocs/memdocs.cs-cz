---
title: Vytvořit dvoufázové nasazení
titleSuffix: Configuration Manager
description: Pomocí dvoufázové nasazení můžete automatizovat zavedení softwaru do několika kolekcí.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1845b381d8b37fed3a785475e961cd39c54cf42d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125266"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Vytvoření postupného nasazení pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Postupná nasazení automatizují koordinované, sekvenční zavedení softwaru napříč více kolekcemi. Například nasaďte software do pilotní kolekce a potom automaticky pokračujte v zavedení na základě kritérií úspěchů. Vytvořte dvoufázové nasazení s výchozími dvěma fázemi nebo ručně nakonfigurujte několik fází. 

Vytvořit dvoufázové nasazení pro následující objekty:
- **Pořadí úkolů**  
    - Postupné nasazení pořadí úloh nepodporuje instalaci pomocí technologie PXE nebo médií.   
- **Aplikace** (počínaje verzí 1806) <!--1358147-->  
- **Aktualizace softwaru** (počínaje verzí 1810) <!--1358146-->  
    - Nemůžete použít pravidlo automatického nasazení se dvoufázovém nasazením.

> [!Tip]  
> Funkce postupného nasazení byla poprvé představena ve verzi 1802 jako [funkce předběžné verze](../../core/servers/manage/pre-release-features.md). Od verze 1806 už není k dispozici funkce předběžného vydání.<!--1356837-->  



## <a name="prerequisites"></a>Požadavky

#### <a name="security-scope"></a>Obor zabezpečení
Nasazení vytvořená pomocí dvoufázové nasazení nejsou viditelná pro žádného administrativního uživatele, který nemá rozsah zabezpečení **vše** . Další informace najdete v tématu [Obory zabezpečení](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

#### <a name="distribute-content"></a>Distribuovat obsah
Před vytvořením postupného nasazení distribuujte přidružený obsah do distribučního bodu.<!--518293-->  

- **Aplikace**: v konzole vyberte cílovou aplikaci a na pásu karet použijte akci **distribuovat obsah** . Další informace najdete v tématu [nasazení a Správa obsahu](../../core/servers/deploy/configure/deploy-and-manage-content.md).   

- **Pořadí úkolů**: před vytvořením pořadí úkolů je nutné vytvořit odkazované objekty, jako je balíček s UPGRADEM operačního systému. Před vytvořením nasazení tyto objekty distribuujte. Použijte akci **distribuovat obsah** u každého objektu nebo pořadí úkolů. Chcete-li zobrazit stav veškerého odkazovaného obsahu, vyberte pořadí úloh a v podokně podrobností přepněte na kartu **odkazy** . Další informace najdete v části konkrétní typ objektu v tématu [Příprava na nasazení operačního systému](../get-started/prepare-for-operating-system-deployment.md).   

- **Aktualizace softwaru**: Vytvořte balíček pro nasazení a distribuujte ho. Použijte Průvodce stažením aktualizací softwaru. Další informace najdete v tématu [Stažení aktualizací softwaru](../../sum/deploy-use/download-software-updates.md).  



## <a name="phase-settings"></a><a name="bkmk_settings"></a>Nastavení fáze

Tato nastavení jsou jedinečná pro dvoufázové nasazení. Tato nastavení konfigurujte při vytváření nebo úpravách fází pro řízení plánování a chování procesu dvoufázového nasazení. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Kritéria úspěchu první fáze  

- **Procento úspěšnosti nasazení**: zadejte procento zařízení, která musí úspěšně dokončit nasazení, aby se první fáze úspěšně dokončila. Ve výchozím nastavení je tato hodnota 95%. Jinými slovy lokalita posuzuje první fázi úspěšně, když je stav kompatibility 95% zařízení pro toto nasazení **úspěšné** . Lokalita pak pokračuje ve druhé fázi a vytvoří nasazení softwaru do další kolekce.  
- **Počet úspěšně nasazených zařízení**: přidáno v Configuration Manager verze 1902. Zadejte počet zařízení, která musí úspěšně dokončit nasazení, aby byla první fáze úspěšná. Tato možnost je užitečná v případě, že je velikost kolekce proměnná a máte určitý počet zařízení, aby bylo možné před přechodem do další fáze zobrazit úspěch. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Podmínky pro zahájení druhé fáze nasazení po úspěchu první fáze  

- **Automaticky zahájit tuto fázi po odložení (ve dnech)**: Vyberte počet dní, po který se má čekat před začátkem druhé fáze po úspěchu prvního. Ve výchozím nastavení je tato hodnota jeden den.  

- **Ruční zahájení druhé fáze nasazení**: lokalita po úspěšném dokončení první fáze automaticky nespustí druhou fázi. Tato možnost vyžaduje ruční spuštění druhé fáze. Další informace najdete v tématu [Přesun do další fáze](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Tato možnost není k dispozici pro dvoufázové nasazení aplikací.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Postupně zpřístupnit tento software v tomto časovém intervalu (ve dnech)
<!--1358578-->
Pokud začínáte ve verzi 1806, nakonfigurujte toto nastavení tak, aby se v každé fázi postupně prováděly změny. Toto chování pomáhá zmírnit riziko problémů s nasazením a snižuje zatížení sítě, které je způsobeno distribucí obsahu klientům. Tato lokalita postupně zpřístupňuje software v závislosti na konfiguraci pro každou fázi. Každý klient ve fázi má konečný termín relativně k době, kdy byl software zpřístupněn. Časový interval mezi dostupným časem a konečným termínem je stejný pro všechny klienty ve fázi. Výchozí hodnota tohoto nastavení je nula, takže ve výchozím nastavení není nasazení omezené. Nenastavujte hodnotu vyšší než 30.<!--SCCMDocs-pr issue 2767--> 

![Kritéria postupného nasazení pro nastavení úspěchu](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Konfigurace chování konečného termínu vzhledem k zpřístupnění softwaru  

- **Instalace je nutná co nejdříve**: nastavte konečný termín instalace na zařízení, jakmile bude zařízení cíleno.  

- **Po uplynutí této doby se vyžaduje instalace**: nastavte konečný termín pro instalaci určitého počtu dní od cílení na zařízení. Ve výchozím nastavení je tato hodnota sedm dní.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a>Automatické vytvoření výchozího dvoufázové nasazení

1. Spusťte Průvodce vytvořením postupného nasazení v konzole Configuration Manager. Tato akce se liší v závislosti na typu softwaru, který nasazujete:  

    - **Aplikace** (pouze ve verzi 1806 nebo novější): Otevřete **knihovnu softwaru**, rozbalte položku **Správa aplikací**a vyberte možnost **aplikace**. Vyberte existující aplikaci a pak na pásu karet vyberte **vytvořit dvoufázové nasazení** .  

    - **Aktualizace softwaru** (jenom ve verzi 1810 nebo novější): Otevřete **knihovnu softwaru**, rozbalte možnost **aktualizace softwaru**a vyberte **všechny aktualizace softwaru**. Vyberte jednu nebo víc aktualizací a pak na pásu karet vyberte **vytvořit dvoufázové nasazení** .  

        Tato akce je k dispozici pro aktualizace softwaru z následujících uzlů:  
        - Aktualizace softwaru  
            - **Všechny aktualizace softwaru**  
            - **Skupiny aktualizací softwaru**   
        - Údržba Windows 10, **všechny aktualizace Windows 10**  
        - Správa klientů Office 365, **aktualizace sady office 365**  

    - **Pořadí úloh**: přejít do pracovního prostoru **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**. Vyberte existující pořadí úloh a pak na pásu karet vyberte **vytvořit dvoufázové nasazení** .  

2. Na stránce **Obecné** udělte postupné nasazení **název**, **Popis** (volitelné) a vyberte **automaticky vytvořit výchozí dvoufázové nasazení**.  

3. Vyberte **Procházet** a zvolte cílovou kolekci pro pole **první kolekce** i **druhá kolekce** . V pořadí úkolů a aktualizacích softwaru vyberte z kolekcí zařízení. V případě aplikace vyberte možnost z kolekce uživatelů nebo zařízení. Vyberte **Další**.  

    > [!Important]  
    > Průvodce vytvořením postupného nasazení vás upozorní, pokud je nasazení potenciálně vysoce rizikové. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) a na poznámku při [nasazení pořadí úkolů](deploy-a-task-sequence.md).  

4. Na stránce **Nastavení** vyberte jednu možnost pro každé nastavení plánování. Další informace najdete v tématu [nastavení fáze](#bkmk_settings). Po dokončení vyberte **Další** .  

5. Na stránce **fáze** se podívejte na dvě fáze, které průvodce vytvoří pro zadané kolekce. Vyberte **Další**. Tyto pokyny pokrývají postup pro automatické vytvoření výchozího dvoufázové nasazení. Průvodce umožňuje přidávat, odebírat, měnit pořadí, upravovat a zobrazovat fáze pro postupné nasazení. Další informace o těchto dalších akcích najdete v tématu [vytvoření postupného nasazení s ručně nakonfigurovanými fázemi](#bkmk_manual).  

6. Potvrďte svoje výběry na kartě **Souhrn** a potom kliknutím na tlačítko **Další** dokončete průvodce.  

> [!NOTE]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). I když se konzola aktualizuje, můžete si i nadále zobrazovat starý název v Configuration Manager produktu a dokumentaci.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a>Vytvoření postupného nasazení s ručně nakonfigurovanými fázemi
<!--1358148--> 

Počínaje verzí 1806 vytvořte dvoufázové nasazení s ručně nakonfigurovanými fázemi pro pořadí úkolů. Na kartě **fáze** v Průvodci vytvořením fáze nasazení přidejte až 10 dalších fází. 

> [!Note]  
> V tuto chvíli nemůžete ručně vytvářet fáze pro aplikaci. Průvodce automaticky vytvoří dvě fáze pro nasazení aplikací.


1. Spusťte Průvodce vytvořením postupného nasazení pro pořadí úkolů nebo aktualizace softwaru.  

2. Na stránce **Obecné** v Průvodci vytvořením fáze nasazení udělte postupné nasazení **název**, **Popis** (volitelné) a vyberte možnost **ručně konfigurovat všechny fáze**.  

3. Na stránce **fáze** v Průvodci vytvořením fáze nasazení jsou k dispozici tyto akce:  

    - **Vyfiltrujte** seznam fází nasazení. Zadejte řetězec znaků pro shodu sloupce Order, Name nebo Collection bez rozlišení velkých a malých písmen. 

    - **Přidat** novou fázi:  

        1. Na stránce **Obecné** v Průvodci přidáním fáze zadejte **název** fáze a potom přejděte do cílové **kolekce fází**. Další nastavení na této stránce jsou stejná jako při normálním nasazení pořadí úloh nebo aktualizací softwaru.  

        2. Na stránce **nastavení fáze** Průvodce přidáním fáze nakonfigurujte nastavení plánování a po dokončení vyberte **Další** . Další informace najdete v tématu [Nastavení](#bkmk_settings).   

            > [!Note]  
            > V první fázi nemůžete upravit nastavení fáze, **Procento úspěšnosti nasazení** nebo **Počet úspěšně nasazených zařízení** (verze 1902 nebo novější). Toto nastavení platí jenom pro fáze, které mají předchozí fázi.  

        3. Nastavení na stránkách **uživatelské prostředí** a **distribuční body** Průvodce přidáním fáze jsou stejná jako při normálním nasazení pořadí úloh nebo aktualizací softwaru.  

        4. Zkontrolujte nastavení na stránce **Souhrn** a pak dokončete Průvodce přidáním fáze.  

    - **Upravit**: Tato akce otevře okno vlastnosti vybrané fáze, která má karty stejné jako stránky Průvodce přidáním fáze.  

    - **Odebrat**: Tato akce odstraní vybranou fázi.  

       > [!Warning]  
       > Neexistuje žádné potvrzení a způsob, jak tuto akci zrušit.  

    - **Přesunout nahoru** nebo **Přesunout dolů**: Průvodce seřadí fáze podle způsobu jejich přidání. Naposledy přidaná fáze je v seznamu poslední. Chcete-li změnit pořadí, vyberte fázi a pak pomocí těchto tlačítek přesuňte umístění fáze v seznamu.  

       > [!Important]  
       > Po změně pořadí zkontrolujte nastavení fáze. Ujistěte se, že následující nastavení jsou stále v souladu s vašimi požadavky na toto dvoufázové nasazení:  
       > 
       > - Kritéria úspěchu předchozí fáze  
       > - Podmínky zahájení této fáze nasazení po úspěšném provedení předchozí fáze   

5. Vyberte **Další**. Zkontrolujte nastavení na stránce **Souhrn** a pak dokončete Průvodce vytvořením postupného nasazení.  


Po vytvoření postupného nasazení otevřete jeho vlastnosti, abyste provedli změny:  

- **Přidejte** další fáze do stávajícího dvoufázové nasazení.  

- Pokud fáze není aktivní, můžete ji **Upravit**, **Odebrat**nebo **přesunout** nahoru nebo dolů. Nemůžete ho přesunout před aktivní fází.  

- Když je fáze aktivní, je jen pro čtení. Nemůžete ho upravit, odebrat nebo přesunout jeho umístění do seznamu. Jedinou možností je **Zobrazit** vlastnosti fáze.  

- Dvoufázové nasazení aplikace je vždy jen pro čtení.  



## <a name="next-steps"></a>Další kroky

Správa a monitorování postupného nasazení:
- [Aplikace](manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)
- [Aktualizace softwaru](manage-monitor-phased-deployments.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Pořadí úkolů](manage-monitor-phased-deployments.md)  

