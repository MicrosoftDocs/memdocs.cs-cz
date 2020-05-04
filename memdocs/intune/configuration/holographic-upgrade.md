---
title: Upgrade na Windows Holografick pro firmy
titleSuffix: Microsoft Intune
description: Přečtěte si, jak upgradovat v zařízení software Windows Holographic na Windows Holographic for Business.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332083"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Upgrade zařízení se softwarem Windows Holographic na Windows Holographic for Business

Microsoft Intune obsahuje mnoho nastavení, které vám pomůžou se správou a ochranou vašich zařízení. Tento článek obsahuje seznam a popis nastavení pro upgrade zařízení se systémem Windows holografick pro firmy. Tato nastavení se vytvoří v profilu konfigurace upgradu v Intune, který se předává nebo nasazuje do zařízení.

Jako součást řešení správy mobilních zařízení (MDM) použijte Tato nastavení k upgradu holografických zařízení s Windows. V případě Microsoft HoloLens si můžete koupit komerční sadu a získat tak požadovanou licenci pro upgrade. Další informace najdete v tématu [Odblokování funkcí Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Další informace o této funkci najdete v tématu [upgrade edice Windows 10 nebo povolení režimu S](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Upgrade edice

- **Edice, na kterou se má upgradovat**: vyberte **Windows 10 holografick pro firmy**.
- **Soubor s licencí**: vyhledejte a vyberte soubor s licencí XML, který vám byl poskytnut.

  ![Zadejte název souboru XML, který obsahuje informace o licenci pro holografické firmy.](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nemusí ještě nic dělat. Nezapomeňte [profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily upgradu edice pro zařízení [s Windows 10 a novějším](edition-upgrade-windows-settings.md) .
