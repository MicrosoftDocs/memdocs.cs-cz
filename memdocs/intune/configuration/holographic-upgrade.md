---
title: Upgrade na Windows Holografick pro firmy v Microsoft Intune – Azure | Microsoft Docs
description: Upgradujte na Windows 10 Holografick pro firmy pomocí profilu konfigurace zařízení v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65a45b13a91671c1de9bcf04f23156d75313285f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907765"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Upgrade zařízení se softwarem Windows Holographic na Windows Holographic for Business

Microsoft Intune obsahuje mnoho nastavení, které vám pomůžou se správou a ochranou vašich zařízení. Tento článek obsahuje seznam a popis nastavení pro upgrade zařízení se systémem Windows holografick pro firmy.

Jako součást řešení správy mobilních zařízení (MDM) použijte Tato nastavení k upgradu holografických zařízení s Windows. V případě Microsoft HoloLens si můžete koupit komerční sadu a získat tak požadovanou licenci pro upgrade. Další informace najdete v tématu [Odblokování funkcí Windows Holographic for Business](/hololens/hololens1-upgrade-enterprise).

Jako správce Intune můžete vytvořit a přiřadit tato nastavení k vašim zařízením.

Další informace o této funkci najdete v tématu [upgrade edice Windows 10 nebo povolení režimu S](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil konfigurace zařízení s přepínačem pro upgrade a režim Windows 10](edition-upgrade-configure-windows-10.md#create-the-profile).

Když vytvoříte konfigurační profil zařízení s přepínačem pro upgrade a režim systému Windows 10, je k dispozici více nastavení, než jaké je uvedeno v tomto článku. Nastavení v tomto článku jsou podporovaná na zařízeních s Windows holografickým pro firmy.

## <a name="edition-upgrade"></a>Upgrade edice

- **Edice, na kterou se má upgradovat**: vyberte **Windows 10 holografick pro firmy**.
- **Soubor s licencí**: vyhledejte a vyberte soubor s licencí XML, který vám byl poskytnut.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="V Intune zadejte název souboru XML, který obsahuje informace o licenci pro holografické firmy.":::

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily upgradu edice pro zařízení [s Windows 10 a novějším](edition-upgrade-windows-settings.md) .