---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268775"
---
K odlišení pilotního nasazení a výroby použijte následující definice:  

- **Pilotní**nasazení: podmnožina zařízení, která chcete ověřit před nasazením do větší sady. Použijte Desktop Analytics k označení zařízení jako jedinečných pro pilotní sadu. Zařízení v pilotním projektu jsou připravená k upgradu, když žádné prostředky neblokují. Blokující prostředek je označený jako *kritický* a *nemůže* provést upgrade.  

- **Produkce**: všechna ostatní zařízení zaregistrovaná v Desktop Analytics, která nejsou v pilotním prostředí. Produkční zařízení jsou připravená k upgradu při odhlášení všech prostředků. Desktop Analytics automaticky odhlásí všechny nedůležité prostředky.  
