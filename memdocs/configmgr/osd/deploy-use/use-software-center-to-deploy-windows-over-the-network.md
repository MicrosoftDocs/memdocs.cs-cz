---
title: Použití Centra softwaru k nasazení Windows přes síť
titleSuffix: Configuration Manager
description: Nasazení operačního systému z centra softwaru pro aktualizaci existujícího počítače s novou verzí Windows nebo upgrade Windows na nejnovější verzi.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124597"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití centra softwaru k nasazení Windows přes síť s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete vytvořit pořadí úkolů, které nainstaluje operační systém, který je k dispozici v centru softwaru. Uživatel může spustit pořadí úkolů z centra softwaru pro následující scénáře nasazení operačního systému:

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Upgrade systému Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md)

- [Vytvoření pořadí úkolů pro nasazení jiného softwaru než operačního systému](create-a-task-sequence-for-non-operating-system-deployments.md)

Proveďte kroky v jednom z těchto scénářů nasazení operačního systému. Pak pomocí následujících částí připravte nasazení, která jsou k dispozici v centru softwaru.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Nasazení pořadí úkolů

Nasaďte pořadí úkolů do cílové kolekce. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

Na stránce **nastavení nasazení** v nasazení vyberte u položky **zpřístupnit pro následující** nastavení jednu z následujících možností:

- Pouze klienti Configuration Manager

- Klienti aplikace Configuration Manager, média a technologie PXE

Také nakonfigurujte, zda je nasazení požadováno nebo k dispozici:

- Požadované nasazení: požadovaná nasazení zpřístupňují pořadí úkolů v centru softwaru. Automaticky se spustí s nakonfigurovaným konečným termínem.

- Dostupné nasazení: pořadí úkolů je dostupné v centru softwaru a uživatel ho může nainstalovat na vyžádání.

Po vytvoření nasazení budou klienti v cílové kolekci zobrazovat pořadí úkolů v centru softwaru.

## <a name="next-steps"></a>Další kroky

[Uživatelská prostředí pro nasazení operačního systému](../understand/user-experience.md#software-center)
