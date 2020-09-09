---
title: Správa & monitorování fází nasazení
titleSuffix: Configuration Manager
description: Pochopte, jak spravovat a monitorovat dvoufázové nasazení softwaru v Configuration Manager.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 631a2fc3cb7df01eed1a5a6af80dd87f84455bdc
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606332"
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

    - **Aplikace**: přejít do pracovního prostoru **softwarová knihovna** , rozbalte položku **Správa aplikací**a vyberte možnost **aplikace**.

    - **Aktualizace softwaru**: přejdete do pracovního prostoru **softwarová knihovna** a pak vyberete jeden z následujících uzlů:
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

Od verze 2002 použijte následující rutinu prostředí Windows PowerShell pro tuto úlohu: [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext).

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Fáze pozastavení a obnovení

Postupné nasazení můžete ručně pozastavit nebo obnovit. Můžete například vytvořit postupné nasazení pořadí úkolů. Při monitorování fáze do pilotní skupiny si všimnete velkého počtu selhání. Pozastavíte postupné nasazení, aby se zastavilo další zařízení pro spuštění pořadí úkolů. Po vyřešení problému obnovíte postupné nasazení, abyste mohli pokračovat v zavádění.

1. Postup, jak spustit tuto akci, se liší podle typu nasazeného softwaru:  

    - **Aplikace**: přejít do pracovního prostoru **softwarová knihovna** , rozbalte položku **Správa aplikací**a vyberte možnost **aplikace**.

    - **Aktualizace softwaru**: přejdete do pracovního prostoru **softwarová knihovna** a pak vyberete jeden z následujících uzlů:
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

Počínaje verzí 2002 použijte pro tuto úlohu tyto rutiny Windows PowerShellu:

- [Pozastavit – CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)
- [Pokračovat – CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)

## <a name="monitor"></a><a name="bkmk_monitor"></a> Sledován
<!--1358577-->

Postupná nasazení mají svůj vlastní vyhrazený monitorovací uzel, což usnadňuje identifikaci dvoufázového nasazení, které jste vytvořili, a přejdete do zobrazení monitorování postupného nasazení. V pracovním prostoru **monitorování** vyberte **dvoufázové nasazení**a pak dvakrát klikněte na jedno ze postupných nasazení, abyste zobrazili stav. <!--3555949-->

![Řídicí panel stavu postupného nasazení zobrazující stav dvou fází](media/1358577-phased-deployment-status.png)

Tento řídicí panel zobrazuje pro každou fázi nasazení následující informace:  

- **Celkem zařízení** nebo **Celkový počet prostředků**: kolik zařízení cílí touto fází.  

- **Status (stav**): aktuální stav této fáze. Každá fáze může být v jednom z následujících stavů:  

  - **Nasazení vytvořeno**: dvoufázové nasazení vytvořilo nasazení softwaru do kolekce pro tuto fázi. Klienti jsou aktivně zacíleni na tento software.  

  - **Čekání**: předchozí fáze ještě nedosáhla kritérií úspěchu, aby nasazení pokračovalo v této fázi.  

  - **Pozastaveno**: Správce pozastavil nasazení.  

- **Průběh**: barevně kódované stavy nasazení od klientů. Například: úspěch, probíhá, chyba, požadavky nejsou splněny a neznámé.

### <a name="success-criteria-tile"></a>Dlaždice kritérií úspěchu

Pomocí rozevíracího seznamu **Výběr fáze** můžete změnit zobrazení dlaždice **kritéria úspěchu** . Tato dlaždice porovnává **cíl fáze** s aktuálním dodržováním předpisů nasazení. Ve výchozím nastavení je cíl fáze 95%. Tato hodnota znamená, že nasazení potřebuje 95% dodržování předpisů, aby bylo možné přejít k další fázi.

V tomto příkladu je cílem fáze 65% a aktuální kompatibilita je 66,7%. Dvoufázové nasazení se automaticky přesune do druhé fáze, protože první fáze splnila kritéria úspěchu.  

   ![Ukázková kritéria úspěšné dlaždice ze stavu postupného nasazení, kde cíl je 65%](media/pod-status-success-criteria-tile.png)

Cíl fáze je stejný jako **Procento úspěšnosti nasazení** v nastavení fáze pro *Další* fázi. V případě postupného nasazení na začátek další fáze definuje druhá fáze kritéria úspěchu první fáze. Chcete-li zobrazit toto nastavení:

1. V tomto softwaru přejdete na objekt postupného nasazení a otevřete vlastnosti postupného nasazení.  

2. Přepněte na kartu **fáze** . Vyberte **fáze 2** a klikněte na tlačítko **Zobrazit**.  

3. Ve fázi okno Vlastnosti přepněte na kartu **nastavení fáze** .  

4. V *kritériích pro úspěch předchozí skupiny fází* zobrazte hodnotu **Procento úspěšnosti nasazení** .  

Například následující vlastnosti jsou pro stejnou fázi jako dlaždice kritéria úspěšnosti zobrazené výše, kde kritéria jsou 65%:  

![Karta nastavení fáze ve vlastnostech fáze](media/phase-properties-phase-settings.png)

## <a name="powershell"></a>PowerShell

Ke správě postupného nasazení použijte následující rutiny Windows PowerShellu:

### <a name="automatically-create-phased-deployments"></a>Automaticky vytvářet dvoufázové nasazení

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment)

### <a name="manually-create-phased-deployments"></a>Ruční vytváření fází nasazení

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment)

### <a name="get-existing-phased-deployment-objects"></a>Získat existující objekty postupného nasazení

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment)
- [Get-CMPhase](/powershell/module/configurationmanager/get-cmphase)

### <a name="monitor-phased-deployment-status"></a>Monitorování stavu postupného nasazení

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus)

### <a name="manage-existing-phased-deployments"></a>Spravovat existující dvoufázové nasazení

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext)
- [Pokračovat – CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)
- [Pozastavit – CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)

### <a name="modify-existing-phased-deployments"></a>Upravit existující dvoufázové nasazení

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment)
