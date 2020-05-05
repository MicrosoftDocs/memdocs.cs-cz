---
title: Použití Centra softwaru k nasazení Windows přes síť
titleSuffix: Configuration Manager
description: Operační systém můžete nasadit do centra softwaru a aktualizovat existující počítač pomocí nové verze Windows nebo upgradovat Windows na nejnovější verzi.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724213"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití centra softwaru k nasazení Windows přes síť s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete vytvořit pořadí úkolů, které nainstaluje operační systém v Configuration Manager k dispozici v centru softwaru. Operační systém můžete nasadit do centra softwaru v následujících scénářích nasazení operačního systému:

-   [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Upgrade systému Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md)

Proveďte kroky v jednom ze scénářů nasazení operačního systému. Pak pomocí následujících částí připravte nasazení, která jsou k dispozici v centru softwaru.

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení  
Aby bylo nasazení operačního systému dostupné v centru softwaru, nakonfigurujte nasazení. Nasazení můžete nakonfigurovat na stránce **nastavení nasazení** v nástroji Průvodce nasazením softwaru nebo na kartě **nastavení nasazení** ve vlastnostech nasazení. U nastavení **Zpřístupnit pro následující** nakonfigurujte buď **Pouze klienti aplikace Configuration Manager** , nebo **Klienti aplikace Configuration Manager, média a technologie PXE**. Po nasazení operačního systému systémem se operační systém zobrazí v centru softwaru pro členy cílové kolekce.

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a>Nasazení pořadí úkolů na počítače  
Nasaďte operační systém do cílové kolekce. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md). Když nasazujete operační systémy pro Centrum softwaru, můžete nakonfigurovat, jestli je nasazení požadované, nebo dostupné.

-   **Požadované nasazení**: Požadovaná nasazení zpřístupní operační systém v Centru softwaru, ale spustí se automaticky podle nakonfigurovaného plánu přiřazení.

-   **Dostupné nasazení**: Operační systém bude dostupný v Centru softwaru a uživatel ho může na požádání nainstalovat.
