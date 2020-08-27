---
title: Použití hromadných akcí zařízení v Microsoft Intune zařízení.
titleSuffix: ''
description: Používejte hromadné akce vzdáleného zařízení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c00e124c9f2741c3b94b08b51a6d1d897086087
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914408"
---
# <a name="use-bulk-device-actions"></a>Použití hromadných akcí zařízení

Akce hromadných zařízení můžete použít pro následující vzdálené akce:
- [Resetování autopilotu](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Vlastní oznámení](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Odstranit](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Přejmenovat](device-rename.md)
- [Restartovat](device-restart.md)
- [Synchronizovat](device-sync.md)
- [Vymazání](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Použít hromadnou akci zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **všechna zařízení**  >  **hromadně akce zařízení**.
![Hromadně prováděné akce zařízení](./media/bulk-device-actions/bulk-device-actions.png)
3. Na stránce **Hromadná akce zařízení** vyberte akci s **operačním systémem** a **zařízením**. Některé akce zařízení mají další možnosti nebo pole k naplnění. Zvolte **Další**.
4. Na stránce **zařízení** vyberte od 1 do 100 zařízení > **Další**.
5. Na stránce **Revize + vytvořit** vyberte **vytvořit**.

## <a name="next-steps"></a>Další kroky
[Přehled správy zařízení.](device-management.md)