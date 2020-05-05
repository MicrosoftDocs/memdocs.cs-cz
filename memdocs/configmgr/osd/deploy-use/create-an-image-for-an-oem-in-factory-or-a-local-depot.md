---
title: Vytvoření image pro výrobce OEM v továrně nebo místním úložišti
titleSuffix: Configuration Manager
description: Nasazení předzpracovaného média můžete použít ke snížení síťového provozu při nasazení operačního systému do počítače, který není úplně zřízený.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722995"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Vytvoření image pro výrobce OEM v továrně nebo místním skladu pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení předzpracovaného média v Configuration Manager umožňuje nasadit operační systém na počítač, který není úplně zřízený. Předzpracované médium je soubor ve formátu WIM (Windows Imaging Format), který se dá nainstalovat na holý počítač výrobcem OEM nebo v přípravném centru podniku, které není připojené k Configuration Managermu prostředí. Později v prostředí Configuration Manager se počítač spustí pomocí spouštěcí bitové kopie, která je k dispozici na médiu, na předzpracovaném médiu se spustí kontrolní hodnota hash, aby se zajistilo, že je platný, a pak se počítač připojí k bodu správy lokality, aby mohla být dostupná pořadí úkolů, která dokončí proces stahování.


Tato metoda nasazení snižuje objem síťového přenosu, protože bitová kopie a spouštěcí bitová kopie operačního systému jsou již uloženy v cílovém počítači. Můžete určit aplikace, balíčky a balíčky ovladačů, které mají být součástí předzpracovaného média. Po instalaci operačního systému na počítači se nejdřív zkontroluje místní mezipaměť pořadí úkolů, jestli neobsahuje aplikace, balíčky nebo balíčky ovladačů, a pokud se obsah nenajde nebo byl revidován, stáhne se obsah z distribučního bodu nakonfigurovaného na předzpracovaném médiu a nainstaluje se.  

 Předzpracovaná média můžete použít v následujících scénářích nasazení operačního systému:  

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

- [Nahrazení existujícího počítače a nastavení přenosu](replace-an-existing-computer-and-transfer-settings.md)  

  Proveďte kroky v jednom ze scénářů nasazení operačního systému, potom se podle následujících částí připravte na vytvoření předzpracovaného média a nakonec ho vytvořte.  

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení  
 Když používáte předzpracované médium k zahájení procesu nasazení operačního systému, musíte nakonfigurovat nasazení, aby byl operační systém v médiu dostupný. To můžete nakonfigurovat na stránce **Nastavení nasazení** Průvodce nasazením softwaru nebo na kartě **Nastavení nasazení** ve vlastnostech nasazení.  U nastavení **Zpřístupnit pro následující** nakonfigurujte jednu z následujících možností:  

-   **Klienti aplikace Configuration Manager, média a technologie PXE**  

-   **Pouze média a technologie PXE**  

-   **Pouze média a technologie PXE (skryté)**  

## <a name="create-the-prestaged-media"></a>Vytvoření předzpracovaného média  
 Vytvořte soubor předzpracovaného média, který chcete odeslat výrobci OEM nebo do místního skladu. Další informace najdete v tématu [Vytvoření předzpracovaného média pomocí Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Odeslání souboru předzpracovaného média výrobci OEM nebo do místního skladu  
 Odešlete médium, které bude sloužit k přípravě počítačů, výrobci OEM nebo do místního skladu. Soubor předzpracovaného média se umístí na naformátovaný pevný disk počítače.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Spuštění počítače za účelem instalace operačního systému  
 Soubor předzpracovaného média se použije na počítačích. Při prvním spuštění počítače se spustí proces instalace operačního systému.  
