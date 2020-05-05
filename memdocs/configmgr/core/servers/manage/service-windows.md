---
title: Okna služby
titleSuffix: Configuration Manager
description: Pomocí oken služby můžete řídit, kdy Configuration Manager lokality instalují aktualizace.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719110"
---
#  <a name="service-windows-for-site-servers"></a>Časové intervaly pro správu a údržbu serverů lokality

*Platí pro: Configuration Manager (Current Branch)*

Můžete nakonfigurovat okna služby v lokalitách centrální správy a primárních lokalitách, aby bylo možné řídit, kdy se můžou instalovat aktualizace v konzole.  Můžete nakonfigurovat několik oken s povoleným oknem pro instalaci aktualizací určených kombinací všech oken služby pro daný server lokality.

Když není nakonfigurované žádné okno služby:
- **V lokalitě nejvyšší úrovně** (lokalita centrální správy nebo samostatná primární lokalita) vyberte, kdy se má spustit instalace aktualizace.
- **V případě podřízených primárních lokalit**se aktualizace automaticky nainstaluje po dokončení instalace aktualizace v lokalitě centrální správy.
- **V sekundární lokalitě**se aktualizace nikdy nespustí automaticky. Místo toho je nutné ručně spustit instalaci aktualizace z konzoly nástroje po instalaci aktualizace nadřazenou primární lokalitou.

Když je nakonfigurované okno služby:
- **V lokalitě nejvyšší úrovně**nebudete moci spustit instalaci jakékoli nové aktualizace v konzole Configuration Manager. I v případě, že je nakonfigurováno okno služby, stáhne web automaticky aktualizace, aby byly připraveny k instalaci.  
- **V podřízených primárních lokalitách**se aktualizace, které jsou nainstalované v lokalitě centrální správy, stáhnou do primární lokality, ale nespustí se automaticky. Instalaci aktualizace nelze ručně spustit v čase, který je zablokován pomocí okna služby. V době, kdy systém Windows již neblokuje instalaci aktualizace, se spustí instalace aktualizace automaticky.
- **Sekundární lokality** nepodporují okna služby a neinstalují automaticky aktualizace. Poté, co primární Nadřazená lokalita sekundární lokality nainstaluje aktualizaci, můžete v konzole nástroje spustit aktualizaci sekundární lokality.

## <a name="to-configure-a-service-window"></a>Konfigurace okna služby

1.  V konzole Configuration Manager otevřete konzolu **Správa** > **Konfigurace** > lokality**lokality**a potom vyberte server lokality, na kterém chcete nakonfigurovat okno služby.  

2.  Potom upravte **Vlastnosti** serveru lokality a vyberte kartu **Časový interval** pro správu a údržbu, kde můžete pro tento server lokality nastavit jeden nebo několik časových intervalů pro správu a údržbu.  
