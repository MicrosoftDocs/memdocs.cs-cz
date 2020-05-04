---
title: Příprava na správu aktualizací softwaru
titleSuffix: Configuration Manager
description: Chcete-li provést přípravu na správu aktualizací, dokončete tyto úlohy, abyste zobrazili data vyhodnocení dodržování předpisů v konzole Configuration Manager.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717269"
---
# <a name="prepare-for-software-updates-management"></a>Příprava na správu aktualizací softwaru

*Platí pro: Configuration Manager (Current Branch)*

Před tím, než se data vyhodnocení shody aktualizace softwaru zobrazí v konzole Configuration Manager a před nasazením aktualizací softwaru do klientských počítačů je nutné provést kroky v následujících částech.

## <a name="step-1-install-a-software-update-point"></a>Krok 1: instalace bodu aktualizace softwaru  
Bod aktualizace softwaru je vyžadován v lokalitě centrální správy nebo v samostatné primární lokalitě a v primárních lokalitách, aby bylo možné povolit posuzování shody aktualizací softwaru a nasazovat aktualizace softwaru na klienty nástroje. Bod aktualizace softwaru je volitelně v sekundárních lokalitách. Podrobnosti najdete v tématu [instalace bodu aktualizace softwaru](install-a-software-update-point.md) .  

## <a name="step-2-synchronize-software-updates"></a>Krok 2: Synchronizace aktualizací softwaru
Synchronizace aktualizací softwaru je proces načítání metadat aktualizací softwaru, která splňují kritéria, která nakonfigurujete. Aktualizace softwaru se v konzole Configuration Manager nezobrazí, dokud nesynchronizujete aktualizace softwaru. Podrobnosti najdete v tématu [synchronizace aktualizací softwaru](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Krok 3: Konfigurace klasifikací a produktů k synchronizaci
Tuto konfiguraci proveďte v lokalitě centrální správy nebo v samostatné primární lokalitě. Po prvním dokončení synchronizace aktualizací softwaru Configuration Manager načte aktualizovaný seznam klasifikací a produktů. Nyní můžete vybrat z nových možností ve vlastnostech komponenty bodu aktualizace softwaru. Po nakonfigurování nových klasifikací a produktů opakujte krok 2 a spusťte synchronizaci aktualizací softwaru pro načtení metadat aktualizace softwaru pro nová kritéria. Podrobnosti najdete v tématu [Konfigurace klasifikací a produktů k synchronizaci](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Krok 4: Správa nastavení pro aktualizace softwaru
Po synchronizaci aktualizací softwaru ověřte Configuration Manager nastavení klienta, konfigurace zásad skupiny a nastavení aktualizací softwaru před nasazením aktualizací softwaru. Podrobnosti najdete v tématu [Správa nastavení pro aktualizace softwaru](manage-settings-for-software-updates.md).
