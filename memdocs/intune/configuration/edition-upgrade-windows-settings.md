---
title: Nastavení upgradu a režimu S Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení a co dělají při upgradování edice Windows 10 na zařízení nebo povolit režim S v zařízení pomocí profilu konfigurace zařízení v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d050139ae017f5800670518a41d75fba469ceac
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146469"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Nastavení zařízení s Windows 10 (a novější) pro upgrade edice nebo povolení režimu S v Intune

Microsoft Intune obsahuje mnoho nastavení, které vám pomůžou se správou a ochranou vašich zařízení. Tento článek obsahuje seznam a popis nastavení pro upgrade edice nebo povolení režimu S v zařízeních S Windows 10. Tato nastavení se vytvoří v profilu konfigurace upgradu v Intune, který se předává nebo nasazuje do zařízení.

V rámci řešení pro správu mobilních zařízení (MDM) použijte Tato nastavení k řízení možností v režimu edice a S pro zařízení S Windows 10.

Další informace o této funkci najdete v tématu [upgrade edice Windows 10 nebo povolení režimu S](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Upgrade edice

- **Edice, na kterou se má upgradovat:** Vyberte edici Windows 10, na kterou upgradujete. Zařízení, pro která zásada platí, se upgradují na vámi vybranou edici.
- **Kód Product Key:** Zadejte kód Product Key, který jste dostali od Microsoftu. Po vytvoření zásady s kódem Product Key nepůjde kód aktualizovat. Kód je také z bezpečnostních důvodů skrytý. Pokud chcete kód Product Key změnit, zadejte ho celý znovu.
- **Soubor s licencí**: pro **Windows 10 holografick pro firmy**zvolte **Procházet** a vyberte soubor s licencí, který jste dostali od Microsoftu. Tento soubor s licencí obsahuje informace o licencích pro edice, na které zařízení upgradujete.

## <a name="mode-switch"></a>Přepínač režimu

- **Přepnutí z režimu s**: přepne zařízení z režimu s. Možnosti:

  - **Žádná konfigurace**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může být zařízení v režimu S v režimu S. Uživatel může přepnout zařízení z režimu S.
  - **Ponechat v režimu s**: zabrání uživatelům v přepnutí zařízení z režimu s.
  - **Přepínač**: umožňuje uživatelům přepnout zařízení mimo režim s.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily upgradu edice pro zařízení s [Windows holografickým pro firmy](holographic-upgrade.md) .
