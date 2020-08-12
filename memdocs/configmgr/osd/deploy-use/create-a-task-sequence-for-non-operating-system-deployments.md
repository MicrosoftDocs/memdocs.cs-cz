---
title: Vytvoření pořadí úkolů pro nasazení jiného softwaru než operačního systému
titleSuffix: Configuration Manager
description: Vytváření pořadí úkolů, která nejsou pro nasazení operačního systému, jako je například distribuce softwaru nebo automatizace úloh
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fcae4d520b1e81d0ef3470cd12ee68488b4f589
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125522"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Vytvoření pořadí úkolů pro nasazení jiného softwaru než operačního systému

*Platí pro: Configuration Manager (Current Branch)*

Pořadí úloh v Configuration Manager slouží k automatizaci různých druhů úloh v rámci vašeho prostředí. Tyto úlohy jsou primárně určené a testované pro nasazení operačních systémů. Configuration Manager má mnoho dalších funkcí, které by měly být primární technologií, kterou použijete v následujících situacích:

- [Instalace aplikace](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > Počínaje verzí 2002 nainstalujte komplexní aplikace pomocí pořadí úkolů prostřednictvím aplikačního modelu. Přidejte typ nasazení do aplikace, která je pořadím úkolů, a to buď k instalaci nebo odinstalaci aplikace. Další informace najdete v tématu [vytváření aplikací pro Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Instalace aktualizací softwaru](../../sum/understand/software-updates-introduction.md)

- [Nastavení konfigurace](../../compliance/understand/ensure-device-compliance.md)

Zvažte také další technologie Microsoft System Center Automation, jako je například [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) a [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

Výkon pořadí úkolů spočívá v jejich flexibilitě a způsobu jejich použití. Můžou konfigurovat nastavení klienta, distribuovat software, aktualizovat ovladače, upravovat stavy uživatelů a provádět další úkoly nezávisle na nasazení operačního systému. Můžete vytvořit vlastní pořadí úkolů a přidat do něj libovolný počet úloh. V Configuration Manager se podporuje použití vlastních pořadí úkolů pro nasazení bez OS. Pokud ale v pořadí úkolů dojde k nežádoucím nebo nekonzistentním výsledkům, podívejte se na způsoby zjednodušení operace:

- Použití jednodušších kroků
- Rozdělení akcí mezi více pořadí úloh
- Vytvoření a otestování pořadí úloh pomocí postupného přístupu

## <a name="supported-steps"></a>Podporované kroky

Následující kroky se podporují pro použití ve vlastním pořadí úkolů nasazení bez OS:  

- [Zkontrolovat připravenost](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Připojit k síťové složce](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Stažení obsahu balíčku](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Instalovat aplikaci](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Instalovat balíček](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Instalovat aktualizace softwaru](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Restartovat počítač](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Spustit příkazový řádek](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Spustit skript prostředí PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Spustit pořadí úloh](../understand/task-sequence-steps.md#child-task-sequence)  

- [Nastavit dynamické proměnné](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Nastavit proměnnou pořadí úloh](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Další kroky

[Vytvoření vlastního pořadí úkolů](create-a-custom-task-sequence.md)