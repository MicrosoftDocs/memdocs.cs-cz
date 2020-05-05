---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723646"
---
K odlišení pilotního nasazení a výroby použijte následující definice:  

- **Pilotní**nasazení: podmnožina zařízení, která chcete ověřit před nasazením do větší sady. Použijte Desktop Analytics k označení zařízení jako jedinečných pro pilotní sadu. Zařízení v pilotním projektu jsou připravená k upgradu, když žádné prostředky neblokují. Blokující prostředek je označený jako *kritický* a *nemůže* provést upgrade.  

- **Produkce**: všechna ostatní zařízení zaregistrovaná v Desktop Analytics, která nejsou v pilotním prostředí. Produkční zařízení jsou připravená k upgradu při odhlášení všech prostředků. Desktop Analytics automaticky odhlásí všechny nedůležité prostředky.  

