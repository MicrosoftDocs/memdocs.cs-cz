---
title: 'Přizpůsobení imagí operačního systému '
titleSuffix: Configuration Manager
description: K přizpůsobení image operačního systému použijte pořadí úloh zachycení a sestavení, ruční konfiguraci nebo kombinaci obou.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 652a0c5e36ce7c4bacf40531a82fdf4e16197d95
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906918"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Přizpůsobení imagí operačního systému pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Bitové kopie operačního systému v Configuration Manager jsou soubory WIM a představují zkomprimovanou kolekci referenčních souborů a složek, které jsou nezbytné k úspěšné instalaci a konfiguraci operačního systému v počítači. Přizpůsobená image operačního systému se vytváří a zaznamenává z referenčního počítače, nakonfigurovaného se všemi požadovanými soubory operačního systému, pomocnými soubory, aktualizacemi softwaru, nástroji a dalšími softwarovými aplikacemi. Rozsah ruční konfigurace referenčního počítače závisí na vás. Pomocí pořadí úkolů sestavení a zaznamenání můžete zcela automatizovat konfiguraci referenčního počítače, pomocí pořadí úkolů můžete ručně nakonfigurovat některé aspekty referenčního počítače a potom automatizovat zbývající akce nebo můžete referenční počítač nakonfigurovat ručně bez pomoci pořadí úkolů. K přizpůsobení operačního systému použijte následující části.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a>Příprava referenčního počítače  
 Než zaznamenáte image operačního systému z referenčního počítače, je potřeba zvážit několik věcí.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a>Rozhodnutí mezi automatizovanou nebo ruční konfigurací  
 Následující informace popisují výhody a nevýhody automatizované a ruční konfigurace referenčního počítače.  

#### <a name="automated-configuration"></a>Automatizovaná konfigurace  
 **Výhody**  

- Konfiguraci lze provést zcela bez obsluhy, takže není vyžadována přítomnost správce nebo uživatele.  

- Opětovným použitím pořadí úloh lze s vysokou úrovní spolehlivosti opakovat konfiguraci dalších referenčních počítačů.  

- Pořadí úloh lze změnit, aby se přizpůsobilo rozdílům v referenčních počítačích, aniž by bylo nutné opětovně vytvářet celé pořadí úloh.  

  **Nevýhody**  

- Vytvoření a testování úvodní akce sestavení pořadí úloh může trvat dlouhou dobu.  

- Pokud se významně změní požadavky na referenční počítač, opětovné sestavení a testování pořadí úloh může trvat dlouhou dobu.  

#### <a name="manual-configuration"></a>Ruční konfigurace  
 **Výhody**  

- Není nutné vytvářet pořadí úloh nebo čekat na testování pořadí úloh a odstraňování potíží s pořadím úloh.  

- Instalaci můžete provést přímo z disků CD, aniž byste museli do balíčku Configuration Manager umístit všechny softwarové balíčky (včetně samotného systému Windows).  

  **Nevýhody**  

- Přesnost konfigurace referenčního počítače závisí na správci nebo uživateli, který počítač konfiguruje.  

- V každém případě je nutné ověřit a otestovat, zda je referenční počítač nakonfigurován správně.  

- Metodu konfigurace nelze opětovně použít.  

- Je třeba osoba, která bude aktivně zapojena do procesu.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a>Požadavky na referenční počítač  
 Následující informace uvádí základní položky, které je třeba zvážit v případě konfigurace referenčního počítače.  

-   **Nasazovaný operační systém**  

     Do referenčního počítače je nutné nainstalovat operační systém, který máte v úmyslu nasadit do cílových počítačů. Další informace o operačních systémech, které lze nasadit, najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Vhodná aktualizace Service Pack**  

     Do referenčního počítače je nutné nainstalovat operační systém, který máte v úmyslu nasadit do cílových počítačů.  

-   **Vhodné aktualizace softwaru**  

     Nainstalujte všechny softwarové aplikace, které chcete zahrnout do bitové kopie operačního systému, který zaznamenáte z referenčního počítače. Softwarové aplikace lze také nainstalovat při nasazení zaznamenané bitové kopie operačního systému do cílových počítačů.  

-   **Členství v pracovní skupině**  

     Referenční počítač musí být nakonfigurován jako člen pracovní skupiny.  

-   **Příkazu**  

     Nástroj pro přípravu systému (Sysprep) je technologie, kterou lze použít s dalšími nástroji nasazení za účelem instalace operačních systémů Windows na nový hardware. Nástroj Sysprep připraví počítač na vytvoření bitové kopie disku nebo doručení disku zákazníkovi nakonfigurováním počítače takovým způsobem, aby při restartování vytvořil nový identifikátor zabezpečení počítače (SID). Nástroj Sysprep dále vyčistí nastavení a data specifická pro uživatele a počítač, která nesmí být zkopírována do cílového počítače.  

     Spuštěním následujícího příkazu můžete ručně připravit referenční počítač pomocí nástroje Sysprep:  

     `Sysprep /quiet /generalize /reboot`  

     Možnost /generalize dává pokyn nástroji Sysprep k odebrání určitých systémových dat z instalace Windows. K systémovým datům patří protokoly událostí, jedinečné ID zabezpečení (SID) a další jedinečné informace. Po odebrání jedinečných systémových informací se počítač restartuje.  

     Pomocí kroku pořadí úkolů [Připravit systém Windows pro zaznamenání](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) nebo záznamového média můžete nástroj Sysprep automatizovat.  

    > [!IMPORTANT]  
    >  Krok pořadí úkolů [Připravit systém Windows pro zaznamenání](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) se před spuštěním nástroje Sysprep pokusí resetovat heslo místního správce v referenčním počítači na prázdnou hodnotu. Pokud je povolena místní zásada zabezpečení **Heslo musí splňovat požadavky na složitost**, resetování hesla správce tímto krokem pořadí úkolů se nezdaří. V případě tohoto scénáře zakažte tuto zásadu před spuštěním pořadí úloh.  

     Další informace o nástroji Sysprep najdete v tématu [Přehled nástroje Sysprep (Příprava systému)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).  

-   **Vhodné nástroje a skripty potřebné k usnadnění scénářů instalací**  

     Vhodné nástroje a skripty potřebné k usnadnění scénářů instalací  

-   **Vhodné vlastní nastavení pracovní plochy, například tapeta, značka organizace a výchozí uživatelský profil**  

     Referenční počítač lze nakonfigurovat vlastnostmi vlastního nastavení pracovní plochy, které chcete zahrnout při zaznamenání bitové kopie operačního systému z referenčního počítače. Vlastnosti pracovní plochy zahrnují tapetu, značku organizace a standardní výchozí uživatelský profil.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a>Ruční sestavení referenčního počítače  
 Referenční počítač jde ručně vytvořit pomocí následujícího postupu.  

> [!NOTE]  
>  Pokud vytvoříte referenční počítač ručně, můžete zachytit image operačního systému pomocí záznamového média. Další informace najdete v tématu [Vytvoření záznamového média](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Ruční vytvoření referenčního počítače  

1. Určete počítač, který chcete použít jako referenční počítač.  

2. Nakonfigurujte referenční počítač s odpovídajícím operačním systémem a dalším softwarem, který je nezbytný k vytvoření bitové kopie operačního systému, který chcete nasazovat.  

   > [!WARNING]  
   >  Minimálně nainstalujte odpovídající operační systém a aktualizaci Service Pack, podpůrné ovladače a nezbytné aktualizace softwaru.  

3. Nakonfigurujte referenční počítač jako člena pracovní skupiny.  

4. Resetujte heslo místního správce na referenčním počítači tak, aby hodnota hesla byla prázdná.  

5. Spusťte Sysprep pomocí příkazu: **sysprep /quiet /generalize /reboot**. Možnost /generalize dává pokyn nástroji Sysprep k odebrání určitých systémových dat z instalace Windows. K systémovým datům patří protokoly událostí, jedinečné ID zabezpečení (SID) a další jedinečné informace. Po odebrání jedinečných systémových informací se počítač restartuje.  

   Až bude referenční počítač připravený, pomocí pořadí úkolů z něj zaznamenejte image operačního systému.  Podrobný návod najdete v tématu [Zachycení image operačního systému z už existujícího referenčního počítače](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a>Použití pořadí úkolů k sestavení referenčního počítače  
 Proces vytvoření referenčního počítače můžete automatizovat pomocí pořadí úkolů pro nasazení operačního systému, ovladačů, aplikací a podobně.  Pomocí následujících kroků sestavte referenční počítač a potom z něj pomocí pořadí úkolů zaznamenejte image operačního systému.  

-   Pomocí pořadí úkolů sestavte referenční počítač a zaznamenejte z něj image operačního systému.  Podrobné pokyny najdete v části [Použití pořadí úkolů k sestavení a zachycení referenčního počítače](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  
