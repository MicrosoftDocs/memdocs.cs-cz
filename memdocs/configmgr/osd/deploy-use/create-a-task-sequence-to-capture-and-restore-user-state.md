---
title: Zaznamenání a obnovení stavu uživatele
titleSuffix: Configuration Manager
description: Pomocí Configuration Manager sekvencí úloh můžete zachytit a obnovit data o stavu uživatele ve scénářích nasazení operačního systému.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a1f11c46689b213b795c0d71221728f916a68bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125487"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Vytvoření pořadí úkolů pro zachycení a obnovení stavu uživatele v Configuration Manager

 *Platí pro: Configuration Manager (Current Branch)*

 Pomocí Configuration Manager sekvencí úloh můžete zachytit a obnovit data o stavu uživatele ve scénářích nasazení operačního systému. V těchto scénářích chcete zachovat stav uživatele v aktuálním operačním systému. Podle typu pořadí úkolů, které vytvoříte, můžou být kroky zaznamenání a obnovení automaticky přidané jako součást tohoto pořadí úkolů. V jiných scénářích může být potřeba přidat kroky zaznamenání a obnovení do pořadí úkolů ručně. Tento článek popisuje kroky, které musíte přidat do existujícího pořadí úkolů, abyste mohli zachytit a obnovit data stavu uživatele.  



## <a name="task-sequence-steps"></a>Kroky pořadí úkolů  

Chcete-li zachytit a obnovit stav uživatele, přidejte do pořadí úloh následující kroky:  

- [Úložiště stavu požadavku](../understand/task-sequence-steps.md#BKMK_RequestStateStore): Pokud ukládáte stav uživatele do bodu migrace stavu, budete potřebovat tento krok.  

- [Zaznamenat stav uživatele](../understand/task-sequence-steps.md#BKMK_CaptureUserState): Tento krok zaznamená data o stavu uživatele. Pak data uloží buď na bod migrace stavu, nebo na místní disk pomocí hardlinks.  

- [Obnovit stav uživatele](../understand/task-sequence-steps.md#BKMK_RestoreUserState): Tento krok obnoví data o stavu uživatele v cílovém počítači. Může načíst data z bodu migrace stavu, nebo pokud hardlinked na místním disku.  

- [Úložiště stavu uvolnění](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): Pokud ukládáte stav uživatele do bodu migrace stavu, budete potřebovat tento krok. Tento krok odebere data z bodu migrace stavu.  


 Následující postupy použijte k přidání kroků pořadí úkolů potřebných k zaznamenání a obnovení stavu uživatele. Další informace o vytváření pořadí úkolů najdete v tématu [Správa pořadí úkolů pro automatizaci úloh](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Zaznamenat stav uživatele  

 Chcete-li přidat kroky pořadí úkolů pro zaznamenání stavu uživatele, použijte následující postup:

1.  V seznamu **Pořadí úloh** zvolte požadované pořadí úloh a klikněte na tlačítko **Upravit**.  

2.  Pokud k uložení stavu uživatele používáte bod migrace stavu, přidejte do pořadí úkolů krok **úložiště stavu požadavku** . V **editoru pořadí úloh**klikněte na tlačítko **Přidat**. Ukažte na možnost **stav uživatele**a klikněte na položku **úložiště stavu požadavku**. Nakonfigurujte vlastnosti a možnosti pro tento krok a pak klikněte na **použít**. Další informace o dostupných nastaveních najdete v tématu [úložiště stavu požadavku](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Přidejte do pořadí úloh krok **Zaznamenat stav uživatele** . V **editoru pořadí úloh**klikněte na tlačítko **Přidat**. Ukažte na **stav uživatele**a pak klikněte na **zaznamenat stav uživatele**. Nakonfigurujte vlastnosti a možnosti pro tento krok a pak klikněte na **použít**. Další informace o dostupných nastaveních najdete v tématu [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Když tento krok přidáte do pořadí úkolů, nastavte proměnnou pořadí úloh **proměnnou OSDStateStorePath** a určete, kam se mají ukládat data o stavu uživatele. Pokud ukládáte stav uživatele v místním počítači, nezadávejte kořenovou složku, protože by mohlo dojít k selhání pořadí úloh. Pokud ukládáte uživatelská data v místním počítači, vždy použijte složku nebo podsložku. Další informace o této proměnné naleznete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md#OSDStateStorePath).  

4.  Pokud používáte bod migrace stavu, přidejte do pořadí úkolů krok **úložiště stavu uvolnění** . V **editoru pořadí úloh**klikněte na tlačítko **Přidat**. Ukažte na **stav uživatele**a potom klikněte na položku **úložiště stavu uvolnění**. Nakonfigurujte vlastnosti a možnosti pro tento krok a pak klikněte na **použít**. Další informace o dostupných nastaveních najdete v části [úložiště stavu uvolnění](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  Akce pořadí úkolů spuštěná před krokem **úložiště stavu uvolnění** musí být úspěšná, než se spustí krok **úložiště stavu uvolnění** .  


 Nasaďte toto pořadí úloh k zaznamenání stavu uživatele v cílovém počítači. Informace o nasazení pořadí úkolů najdete v tématu [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Obnovit stav uživatele  

 Chcete-li přidat kroky pořadí úloh k obnovení stavu uživatele, použijte následující postup:

1. V seznamu **Pořadí úloh** zvolte požadované pořadí úloh a klikněte na tlačítko **Upravit**.  

2. Přidejte do pořadí úkolů krok **Restore User State** . V **editoru pořadí úloh**klikněte na tlačítko **Přidat**. Ukažte na **stav uživatele**a pak klikněte na **Obnovit stav uživatele**. Tento krok naváže připojení k bodu migrace stavu, pokud je to nutné. Nakonfigurujte vlastnosti a možnosti pro tento krok a pak klikněte na **použít**. Další informace o dostupných nastaveních najdete v tématu [obnovení stavu uživatele](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  Když použijete krok [zaznamenat stav uživatele](../understand/task-sequence-steps.md#BKMK_CaptureUserState) s možností **zaznamenání všech profilů uživatelů se standardními možnostmi**, musíte v kroku **Obnovit stav uživatele** vybrat nastavení **Obnovit profily uživatelů místního počítače** . V opačném případě se pořadí úkolů nezdaří.  

   > [!Note]  
   > Pokud ukládáte stav uživatele pomocí místní hardlinks a obnovení není úspěšné, můžete ručně odstranit hardlinks, které byly vytvořeny pro uložení dat. Pořadí úloh může spustit nástroj USMTUtils k automatizaci této akce pomocí kroku [Spustit příkazový řádek](../understand/task-sequence-steps.md#BKMK_RunCommandLine) . Pokud používáte USMTUtils k odstranění hardlink create, přidejte po spuštění USMTUtils krok [restartovat počítač](../understand/task-sequence-steps.md#BKMK_RestartComputer) .  

3. Pokud k uložení stavu uživatele používáte bod migrace stavu, přidejte do pořadí úkolů krok **úložiště stavu uvolnění** . V **editoru pořadí úloh**klikněte na tlačítko **Přidat**. Ukažte na **stav uživatele**a potom klikněte na položku **úložiště stavu uvolnění**. Nakonfigurujte vlastnosti a možnosti pro tento krok a pak klikněte na **použít**. Další informace o dostupných nastaveních najdete v části [úložiště stavu uvolnění](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  Akce pořadí úkolů spuštěná před krokem **úložiště stavu uvolnění** musí být úspěšná, než se spustí krok **úložiště stavu uvolnění** .  


 Nasaďte toto pořadí úloh k obnovení stavu uživatele v cílovém počítači. Další informace o nasazení pořadí úkolů najdete v tématu [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Další kroky

[Monitorování nasazení pořadí úkolů](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
