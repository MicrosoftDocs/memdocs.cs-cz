---
title: Správa & monitorování fází nasazení
titleSuffix: Configuration Manager
description: Pochopte, jak spravovat a monitorovat dvoufázové nasazení softwaru v Configuration Manager.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efc43258e65752e7371c9baadf61598aac820062
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697989"
---
# <a name="manage-and-monitor-phased-deployments"></a>Správa a sledování postupných nasazení

Tento článek popisuje, jak spravovat a monitorovat dvoufázové nasazení. Úlohy správy zahrnují ruční zahájení další fáze a pozastavení nebo obnovení fáze. 

Nejdřív je potřeba vytvořit postupné nasazení: 
- [Aplikace](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Aktualizace softwaru](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Pořadí úkolů](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Přejít na další fázi

Když vyberete toto nastavení, **ručně zahájíte druhou fázi nasazení**, lokalita automaticky nespustí další fázi na základě kritérií úspěchů. Je nutné přesunout dvoufázové nasazení do další fáze.  

1. Postup, jak spustit tuto akci, se liší podle typu nasazeného softwaru:  

    - **Aplikace** (pouze ve verzi 1806 nebo novější): v pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte možnost **aplikace**.   

    - **Aktualizace softwaru** (pouze ve verzi 1810 nebo novější): vyhledejte v pracovním prostoru **softwarová knihovna** a vyberte jeden z následujících uzlů:    
        - Aktualizace softwaru  
            - **Všechny aktualizace softwaru**  
            - **Skupiny aktualizací softwaru**   
        - Údržba Windows 10, **všechny aktualizace Windows 10**  
        - Správa klientů Office 365, **aktualizace sady office 365**  

    - **Pořadí úloh**: přejít do pracovního prostoru **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.   

2. Vyberte software se dvoufázovém nasazením.  

3. V podokně podrobností přepněte na kartu **dvoufázové nasazení** .  

4. Vyberte dvoufázové nasazení a klikněte na tlačítko **přesunout do další fáze** na pásu karet.  

    ![Nabídka kliknutí pravým tlačítkem myši zobrazující akce při dvoufázovém nasazení](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Fáze pozastavení a obnovení 

Postupné nasazení můžete ručně pozastavit nebo obnovit. Můžete například vytvořit postupné nasazení pořadí úkolů. Při monitorování fáze do pilotní skupiny si všimnete velkého počtu selhání. Pozastavíte postupné nasazení, aby se zastavilo další zařízení pro spuštění pořadí úkolů. Po vyřešení problému obnovíte postupné nasazení, abyste mohli pokračovat v zavádění. 

1. Postup, jak spustit tuto akci, se liší podle typu nasazeného softwaru:  

    - **Aplikace** (pouze ve verzi 1806 nebo novější): v pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte možnost **aplikace**.   

    - **Aktualizace softwaru** (pouze ve verzi 1810 nebo novější): vyhledejte v pracovním prostoru **softwarová knihovna** a vyberte jeden z následujících uzlů:    
        - Aktualizace softwaru  
            - **Všechny aktualizace softwaru**  
            - **Skupiny aktualizací softwaru**   
        - Údržba Windows 10, **všechny aktualizace Windows 10**  
        - Správa klientů Office 365, **aktualizace sady office 365**  

    - **Pořadí úloh**: přejít do pracovního prostoru **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**. Vyberte existující pořadí úloh a pak klikněte na **vytvořit dvoufázové nasazení** na pásu karet.  

2. Vyberte software se dvoufázovém nasazením.  

3. V podokně podrobností přepněte na kartu **dvoufázové nasazení** .  

4. Vyberte dvoufázové nasazení a klikněte na tlačítko **pozastavit** nebo **obnovit** na pásu karet. 

> [!NOTE]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](/deployoffice/name-change). I když se konzola aktualizuje, můžete si i nadále zobrazovat starý název v Configuration Manager produktu a dokumentaci. 

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a> Sledován
<!--1358577-->
Počínaje verzí 1902 mají dvoufázové nasazení svůj vlastní vyhrazený monitorovací uzel, což usnadňuje identifikaci dvoufázové nasazení, které jste vytvořili, a přejdete do zobrazení monitorování postupného nasazení. V pracovním prostoru **monitorování** vyberte **dvoufázové nasazení**a pak dvakrát klikněte na jedno ze postupných nasazení, abyste zobrazili stav. <!--3555949-->

V Configuration Manager 1806 a 1810 můžete zobrazit nativní prostředí monitorování pro dvoufázové nasazení. V uzlu **nasazení** v pracovním prostoru **monitorování** vyberte postupné nasazení a pak na pásu karet klikněte na **Stav postupného nasazení** .

![Řídicí panel stavu postupného nasazení zobrazující stav dvou fází](media/1358577-phased-deployment-status.png)

Tento řídicí panel zobrazuje pro každou fázi nasazení následující informace:  

- **Celkem zařízení** nebo **Celkový počet prostředků**: kolik zařízení cílí touto fází.  

- **Status (stav**): aktuální stav této fáze. Každá fáze může být v jednom z následujících stavů:  

    - **Nasazení vytvořeno**: dvoufázové nasazení vytvořilo nasazení softwaru do kolekce pro tuto fázi. Klienti jsou aktivně zacíleni na tento software.  

    - **Čekání**: předchozí fáze ještě nedosáhla kritérií úspěchu, aby nasazení pokračovalo v této fázi.  

    - **Pozastaveno**: Správce pozastavil nasazení.  

- **Průběh**: barevně kódované stavy nasazení od klientů. Například: úspěch, probíhá, chyba, požadavky nejsou splněny a neznámé. 

#### <a name="success-criteria-tile"></a>Dlaždice kritérií úspěchu

Pomocí rozevíracího seznamu **Výběr fáze** můžete změnit zobrazení dlaždice **kritéria úspěchu** . Tato dlaždice porovnává **cíl fáze** s aktuálním dodržováním předpisů nasazení. Ve výchozím nastavení je cíl fáze 95%. Tato hodnota znamená, že nasazení potřebuje 95% dodržování předpisů, aby bylo možné přejít k další fázi.

V tomto příkladu je cílem fáze 65% a aktuální kompatibilita je 66,7%. Dvoufázové nasazení se automaticky přesune do druhé fáze, protože první fáze splnila kritéria úspěchu.  

   ![Ukázková kritéria úspěšné dlaždice ze stavu postupného nasazení, kde cíl je 65%](media/pod-status-success-criteria-tile.png)

Cíl fáze je stejný jako **Procento úspěšnosti nasazení** v nastavení fáze pro *Další* fázi. V případě postupného nasazení na začátek další fáze definuje druhá fáze kritéria úspěchu první fáze. Chcete-li zobrazit toto nastavení: 

1. V tomto softwaru přejdete na objekt postupného nasazení a otevřete vlastnosti postupného nasazení.  

2. Přepněte na kartu **fáze** . Vyberte **fáze 2** a klikněte na **Zobrazit**.  

3. Ve fázi okno Vlastnosti přepněte na kartu **nastavení fáze** .  

4. V *kritériích pro úspěch předchozí skupiny fází* zobrazte hodnotu **Procento úspěšnosti nasazení** .  

Například následující vlastnosti jsou pro stejnou fázi jako dlaždice kritéria úspěšnosti zobrazené výše, kde kritéria jsou 65%:  
![Karta nastavení fáze ve vlastnostech fáze](media/phase-properties-phase-settings.png)