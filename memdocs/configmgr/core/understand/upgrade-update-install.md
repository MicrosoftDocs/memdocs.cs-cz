---
title: O upgradu, aktualizaci a instalaci
titleSuffix: Configuration Manager
description: Naučte se rozdíl mezi podmínkami instalace, aktualizace a upgradu při správě Configuration Manager infrastruktury.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722596"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Informace o upgradu, aktualizaci a instalaci infrastruktury lokality a hierarchie

*Platí pro: Configuration Manager (Current Branch)*

Při správě Configuration Manager lokalit a infrastruktury hierarchie se pomocí pojmů *upgrade*, *aktualizace*a *instalace* popíší tři samostatné koncepty.

## <a name="upgrade"></a>Upgrade

*Upgrade* nebo *místní upgrade*se používá při převodu lokality Configuration Manager 2012 nebo hierarchie na jednu, která spouští Configuration Manager aktuální větve.

Při upgradu nástroje System Center 2012 Configuration Manager na Configuration Manager aktuální větve budete nadále používat stejné servery pro hostování lokalit a serverů lokality a zachováte stávající data a konfigurace pro Configuration Manager.  To se liší od [migrace](../migration/migrate-data-between-hierarchies.md) , což je způsob, jak zachovat vaše konfigurace a data týkající se spravovaných zařízení při použití nových Configuration Managerch stávajících větví nainstalovaných na novém hardwaru.

Další podrobnosti najdete v tématu [upgrade na Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).



## <a name="update"></a>Aktualizace
*Aktualizace* se používá k instalaci konzolových aktualizací pro Configuration Manager a pro aktualizace mimo IP síť, které se nedají doručit v konzole Configuration Manager. Konzolové aktualizace mohou změnit verzi vaší Current Branch webu (nebo webu Technical Preview) tak, aby běžela vyšší verze. Například pokud vaše lokalita používá verzi 1806, můžete nainstalovat aktualizaci verze 1810. Aktualizace také mohou nainstalovat opravy pro známý problém bez změny verze lokality.      

Aktualizace standardně přidávají do stávajícího nasazení opravy zabezpečení, vylepšení kvality a nové funkce. Pokud používáte větev Technical Preview, může aktualizace nainstalovat novější verzi Technical Preview.
- Vyberte, kdy se má nainstalovat aktualizace v konzole, počínaje lokalitou nejvyšší úrovně ve vaší hierarchii.
- V konzole nástroje můžete nainstalovat jakoukoli aktualizaci, která je k dispozici. Pokud třeba vaše lokalita používá verzi 1802 a jsou nabízeny 1806 i 1810, měli byste zvážit instalaci verze 1810, protože každá verze obsahuje funkce, které byly poprvé k dispozici v předchozích vydaných verzích.
- Po dokončení instalace nové aktualizace v lokalitě nejvyšší úrovně automaticky spustí podřízené primární lokality proces, který se má aktualizovat. Můžete ale nastavit časové intervaly pro správu a [údržbu](../servers/manage/service-windows.md) .
- Sekundární lokality neinstalují automaticky aktualizace. Místo toho můžete aktualizaci ručně spustit v rámci konzoly Configuration Manager.

Další informace najdete v tématu [aktualizace pro Configuration Manager](../servers/manage/updates.md)a [Technical Preview pro Configuration Manager](../get-started/technical-preview.md).



## <a name="install"></a>Instalace
*Instalace* se používá při vytváření nové Configuration Manager hierarchie od začátku nebo přidání dalších lokalit do existující hierarchie.  

Když instalujete novou primární lokalitu nebo lokalitu centrální správy, umístění souboru Setup. exe a jeho souvisejících zdrojových souborů, které použijete, závisí na vašem scénáři instalace.

Další informace najdete v tématu [Příprava na instalaci lokalit](../servers/deploy/install/prepare-to-install-sites.md).
