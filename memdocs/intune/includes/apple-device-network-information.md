---
title: zahrnout soubor
description: zahrnout soubor
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347240"
---
## <a name="apple-device-network-information"></a>Informace o síti pro zařízení Apple

|**Použití**|**Název hostitele (IP adresa/podsíť)**|**Protocol (Protokol)**|**Přístavní**|
|------------|-----------|------------|-----------|
|Načítání a zobrazování obsahu ze serverů Apple|itunes.apple.com<br>\*. itunes.apple.com<br>\*. mzstatic.com<br>\*. phobos.apple.com<br>\*. phobos.itunes-apple.com.akadns.net|HTTP|80|
|Komunikace se servery APNS|# – courier.push.apple.com<br>' # ' je náhodné číslo od 0 do 50.|TCP|5223 a 443|
|Různé funkce, včetně přístupu k Internetu, obchodu iTunes, macOS App Storu, iCloud, zasílání zpráv atd.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 nebo 443|

Další informace naleznete v tématu:

- [Porty TCP a UDP používané softwarovými produkty společnosti Apple](https://support.apple.com/HT202944)
- [O připojeních hostitele serveru macOS, iOS/iPadOS a iTunes a procesech na pozadí iTunes](https://support.apple.com/HT201999)
- [Pokud klienti macOS a iOS/iPadOS nezískávají nabízená oznámení Apple](https://support.apple.com/HT203609)