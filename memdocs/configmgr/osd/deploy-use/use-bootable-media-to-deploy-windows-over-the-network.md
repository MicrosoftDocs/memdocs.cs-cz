---
title: Použití spouštěcího média k nasazení Windows přes síť
titleSuffix: Configuration Manager
description: Pomocí nasazení spouštěcího média v nástroji Configuration Manager nasaďte operační systém při spuštění cílového počítače.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724360"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití spouštěcího média k nasazení Windows přes síť pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Operační systém můžete nasadit, když se cílový počítač spustí pomocí nasazení ze spouštěcího média. Médium obsahuje ukazatel na pořadí úkolů, bitovou kopii operačního systému a další požadovaný obsah ze sítě. Po spuštění cílového počítače načte počítač položky, na které se odkazuje v ukazateli. Pomocí spouštěcího média bez obsahu můžete cíl aktualizovat, aniž byste ho museli nahrazovat na médiu.

Operační systémy můžete nasadit přes síť pomocí vícesměrového vysílání v následujících scénářích nasazení operačního systému:

-   [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Nahrazení existujícího počítače a nastavení přenosu](replace-an-existing-computer-and-transfer-settings.md)  

Proveďte kroky v jednom ze scénářů nasazení operačního systému a potom podle následujících částí použijte spouštěcí médium k nasazení operačního systému.  

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení  
Když použijete spouštěcí médium k zahájení procesu nasazení operačního systému, nakonfigurujte nasazení tak, aby byl operační systém pro médium k dispozici. Tuto možnost lze nastavit na stránce **nastavení nasazení** v nástroji Průvodce nasazením softwaru nebo na kartě **nastavení nasazení** ve vlastnostech nasazení. U nastavení **Zpřístupnit pro následující** nakonfigurujte jednu z následujících možností:

-   Configuration Manager klienty, média a technologie PXE

-   Pouze média a technologie PXE

-   Pouze média a technologie PXE (skryté)

## <a name="create-the-bootable-media"></a>Vytvoření spouštěcího média
Můžete určit, jestli spouštěcí médium je USB flash disk nebo sada disků CD/DVD. Počítač, který spouští médium, musí podporovat možnost, kterou zvolíte jako spouštěcí jednotku. Další informace najdete v tématu [Vytvoření spouštěcího média](create-bootable-media.md).  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Instalace operačního systému ze spouštěcího média  
Vložte spouštěcí médium do spouštěcí jednotky v počítači a pak ho zapněte, aby se nainstaloval operační systém.
