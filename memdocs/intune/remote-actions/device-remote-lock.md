---
title: Uzamčení zařízení pomocí Microsoft Intune – Azure | Microsoft Docs
description: Můžete použít akci Vzdáleného uzamčení v Microsoft Intun k uzamčení zařízení chráněného kódem PIN nebo heslem.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3a94b71bb479fcb84e998a4e4b7c3ad91e2e3043
ms.sourcegitcommit: d8dc05476ecd5db7ecb36dc649b566b349ba263d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2020
ms.locfileid: "83732903"
---
# <a name="remotely-lock-devices-with-intune"></a>Vzdálené uzamčení zařízení přes Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Akce zařízení **Vzdálené uzamčení** uzamkne zařízení. Vlastník zařízení musí k jeho odemčení zadat heslo. Vzdáleně uzamknout můžete zařízení, která mají nastavený kód PIN nebo heslo. Zařízení bez kódu PIN nebo hesla nejdou vzdáleně zamknout.

## <a name="supported-platforms"></a>Podporované platformy

**Vzdálené uzamčení** je podporované u těchto platforem:

- Android
- Zařízení s beznabídkovým režimem Androidu Enterprise
- Zařízení Android Enterprise s pracovním profilem
- iOS
- macOS
- Windows 10 Mobile
- Windows Phone 8.1 nebo novější

**Vzdálené uzamčení** není podporované pro:
- Stolní počítač s Windows 10

> [!NOTE]
> Pro zařízení s macOS nastavíte šestimístní číselný kód PIN pro obnovení. Když se zařízení zamkne, **přehled zařízení** bude zobrazovat kód PIN, dokud se nepošle jiná akce zařízení. Nezapomeňte si kód PIN zapsat, protože bude k dispozici až 7 dní po odeslání příkazu Remote Lock. Po 7 dnech už Intune nebude mít PIN kód. Tento příkaz také nespouštějte pro stejné zařízení, dokud se nepoužije původní PIN kód k úspěšnému odemknutí zařízení. Tento příkaz byste měli odeslat, zapište si PIN kód a dokud ho nepoužijete k úspěšnému přihlášení do zařízení macOS, neodešlete znovu tento příkaz do stejného zařízení.  


## <a name="remote-lock-a-device"></a>Vzdáleně uzamknout zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **zařízení**  >  **všechna zařízení**.
4. V seznamu zařízení vyberte zařízení a pak vyberte akci **Vzdálené uzamčení**.

## <a name="next-steps"></a>Další kroky

- Chcete-li zobrazit stav této akce, vyberte možnost **Microsoft Intune**  >  **zařízení**  >  **Akce zařízení**. 
- Další akce, které vám můžou pomoct se správou zařízení, najdete v tématu [Dostupné akce](device-management.md).
