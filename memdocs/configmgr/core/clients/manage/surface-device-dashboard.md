---
title: Řídicí panel zařízení Surface
titleSuffix: Configuration Manager
description: Zkontrolujte informace o zařízeních Surface pomocí řídicího panelu.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 7e6a98c25fabff31d3eae688edf89540c1ab71a7
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84613943"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Řídicí panel zařízení Surface v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Počínaje verzí 1802 řídicí panel zařízení Surface nabízí informace o zařízeních s Surface, která se ve vašem prostředí nacházejí v jediném přehledu. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Otevřete řídicí panel zařízení Surface

Řídicí panel zařízení Surface otevřete pomocí následujících kroků: 

1. Otevřete konzolu nástroje Configuration Manager. 
2. Klikněte na uzel **monitorování** . 
3. Pokud chcete řídicí panel načíst, klikněte na **Surface zařízení**.

**Řídicí panel** 
 ![ zařízení Surface Řídicí panel zařízení Surface](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Kontrola informací na řídicím panelu zařízení Surface

Řídicí panel zařízení Surface zobrazuje tři grafy pro vaše prostředí. 

- **Procenta Surface zařízení** – poskytuje procento Surface zařízení v celém prostředí.

    ![Graf procent zařízení Surface](media/Percent-Surface-Devices.PNG)
- **Modely Surface** – zobrazuje počet zařízení na model Surface. 
  - Najetí myší nad oddíl grafu vám poskytne procento zařízení Surface, která jsou vybraná pro model. 

       ![Graf modelů Surface](media/Surface-Models-Hover.PNG)
  - Kliknutím na oddíl grafu přejdete do seznamu zařízení pro daný model. 
      ![Seznam zařízení s modelem Surface](media/Surface-Model-Device-List.PNG)

- **Pět hlavních verzí firmwaru**– zobrazuje graf s nejvyšším pěti modely firmwaru ve vašem prostředí. 
  - Najetí myší na část grafu vám poskytne počet zařízení Surface, která jsou vybrána ve verzi firmwaru. Od verze Configuration Manager 1806 se kliknutím na oddíl grafu zobrazí seznam relevantních zařízení. <!--1358654-->
     ![Seznam zařízení s modelem Surface](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Další informace

Další informace o zařízeních Surface najdete na webu [Surface](https://www.microsoft.com/surface) .

Další informace o nasazení aktualizací firmwaru Surface v Configuration Manager najdete v tématu [Správa aktualizací ovladačů Surface](../../../sum/deploy-use/surface-drivers.md).




