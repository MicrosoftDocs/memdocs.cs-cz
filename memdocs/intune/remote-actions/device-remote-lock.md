---
title: Uzamčení zařízení pomocí Microsoft Intune – Azure | Microsoft Docs
description: Můžete použít akci Vzdáleného uzamčení v Microsoft Intun k uzamčení zařízení chráněného kódem PIN nebo heslem.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ac6a5d848a0d02b72a4f7275a6b6df47b2cd834
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107332"
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
> Pro zařízení s macOS nastavíte šestimístní číselný kód PIN pro obnovení. Když se zařízení zamkne, **přehled zařízení** bude zobrazovat kód PIN, dokud se nepošle jiná akce zařízení. Nezapomeňte si kód PIN zapsat, protože bude k dispozici až 30 dní od odeslání příkazu vzdáleného zámku. Po uplynutí 30 dnů Intune už nebude mít PIN kód. Tento příkaz také nespouštějte pro stejné zařízení, dokud se nepoužije původní PIN kód k úspěšnému odemknutí zařízení. Tento příkaz byste měli odeslat, zapište si PIN kód a dokud ho nepoužijete k úspěšnému přihlášení do zařízení macOS, neodešlete znovu tento příkaz do stejného zařízení.  


## <a name="remote-lock-a-device"></a>Vzdáleně uzamknout zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **zařízení**  >  **všechna zařízení**.
4. V seznamu zařízení vyberte zařízení a pak vyberte akci **Vzdálené uzamčení**.

## <a name="next-steps"></a>Další kroky

- Chcete-li zobrazit stav této akce, vyberte možnost **Microsoft Intune**  >  **zařízení**  >  **Akce zařízení**. 
- Další akce, které vám můžou pomoct se správou zařízení, najdete v tématu [Dostupné akce](device-management.md).
