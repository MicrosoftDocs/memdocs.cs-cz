---
title: Nástroj Power View
titleSuffix: Configuration Manager
description: Pomocí nástroje Power Viewer můžete zobrazit stav funkce řízení spotřeby u klienta Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723191"
---
# <a name="power-viewer-tool"></a>Nástroj Power View

*Platí pro: Configuration Manager (Current Branch)*

Nástroj Power Viewer je jedním z [nástrojů Configuration Manager](tools.md). Použijte ho k zobrazení stavu funkce řízení spotřeby v klientovi Configuration Manager.

Spusťte **PowerVwr. exe** jako správce. Když se nástroj spustí, zobrazí možnosti napájení a nastavení napájení místního počítače na kartě **Konfigurace napájení** . 

Zobrazení dat řízení spotřeby vzdáleného počítače:  

1. Přejděte do nabídky **soubor** a klikněte na **připojit**. 

2. V případě potřeby zadejte název **počítače** a **uživatelské jméno** a **heslo**. 

Power Viewer obsahuje tři karty:  

- **Konfigurace napájení**: Zobrazte možnosti napájení a nastavení napájení cílového počítače.  

- **Denní aktivita**: zobrazení grafů každodenní aktivity klienta, které obsahují následující informace:  

    - **Počítač zapnutý**: stav napájení počítače za jeden den. Režim spánku se považuje za vypínání.  

    - **Monitorování**: stav monitorování je zapnuto nebo vypnuto za jeden den.  

    - **Aktivní uživatel**: informace o aktivitě uživatele za jeden den.  

- **Události napájení**: zobrazení všech každodenních událostí napájení. Klient shrnuje tyto události v 12:00. Tato sumarizace generuje data pro graf každodenní aktivity.  
