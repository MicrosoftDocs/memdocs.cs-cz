---
title: Použití hromadných akcí zařízení v Microsoft Intune zařízení.
titleSuffix: ''
description: Používejte hromadné akce vzdáleného zařízení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f33198e71fd4250ee93207e571bc535abd1c95f
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325371"
---
# <a name="use-bulk-device-actions"></a>Použití hromadných akcí zařízení

Akce hromadných zařízení můžete použít pro následující vzdálené akce:
- [Resetování autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Vlastní oznámení](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Odstranit](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Přejmenovat](device-rename.md)
- [Restartovat](device-restart.md)
- [Synchronizovat](device-sync.md)
- [Vymazání](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Použít hromadnou akci zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **všechna zařízení** > **hromadných akcí zařízení**.
![hromadných akcí zařízení](./media/bulk-device-actions/bulk-device-actions.png)
3. Na stránce **Hromadná akce zařízení** vyberte akci s **operačním systémem** a **zařízením**. Některé akce zařízení mají další možnosti nebo pole k naplnění. Vyberte **Další**.
4. Na stránce **zařízení** vyberte od 1 do 100 zařízení > **Další**.
5. Na stránce **Revize + vytvořit** vyberte **vytvořit**.

## <a name="next-steps"></a>Další kroky
[Přehled správy zařízení.](device-management.md)
