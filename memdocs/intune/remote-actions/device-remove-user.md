---
title: Odebrání uživatele ze zařízení s iOS/iPadOS pomocí Microsoft Intune
titleSuffix: ''
description: Naučte se, jak odebrat uživatele ze sdíleného zařízení s iOS nebo iPadOS v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed91d31a7085d023ef012e1dd30d86c833819ecc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983082"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>Odebrání uživatele ze sdíleného zařízení s iOS/iPadOS


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Akce **Odebrat uživatele** odstraní vybraného uživatele z místní mezipaměti sdíleného zařízení iPad. Zařízení iPad musí být nastavené pro správu aplikace pro iOS/iPadOS pomocí [vzdělávacího profilu iOS/iPadOS](../fundamentals/education-settings-configure-ios.md). 

## <a name="supported-platforms"></a>Podporované platformy

- Windows – nepodporováno
- Windows Phone – nepodporováno
- iOS/iPadOS – podporováno v systémech iOS/iPadOS 9,3 a novějších (pouze sdílená zařízení iPad)
- macOS – nepodporováno
- Android – nepodporováno

## <a name="remove-a-user"></a>Odebrání uživatele

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **všechna zařízení**.
3. V seznamu zařízení, která spravujete, vyberte zařízení s iOS/iPadOS.
4. V podokně pro zařízení vyberte **Uživatelé**.
5. V seznamu klikněte pravým tlačítkem na uživatele, kterého chcete odebrat, a pak zvolte **Odebrat uživatele**.

## <a name="next-steps"></a>Další kroky

- Pokud chcete zobrazit stav akce **Odebrat uživatele**, vyberte **Zařízení** > **Akce zařízení**.
