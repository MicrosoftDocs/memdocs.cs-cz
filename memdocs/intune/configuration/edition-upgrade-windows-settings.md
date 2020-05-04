---
title: Nastavení upgradu a režimu S Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení a co dělají při upgradování edice Windows 10 na zařízení nebo povolit režim S v zařízení pomocí profilu konfigurace zařízení v Microsoft Intune.
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
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ab94c3cc8bb9009d49a6b301d9a67fa6ffc5f1a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333083"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Nastavení zařízení s Windows 10 (a novější) pro upgrade edice nebo povolení režimu S v Intune

Microsoft Intune obsahuje mnoho nastavení, které vám pomůžou se správou a ochranou vašich zařízení. Tento článek obsahuje seznam a popis nastavení pro upgrade edice nebo povolení režimu S v zařízeních S Windows 10. Tato nastavení se vytvoří v profilu konfigurace upgradu v Intune, který se předává nebo nasazuje do zařízení.

V rámci řešení pro správu mobilních zařízení (MDM) použijte Tato nastavení k řízení možností v režimu edice a S pro zařízení S Windows 10.

Další informace o této funkci najdete v tématu [upgrade edice Windows 10 nebo povolení režimu S](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Upgrade edice

- **Edice, na kterou se má upgradovat:** Vyberte edici Windows 10, na kterou upgradujete. Zařízení, pro která zásada platí, se upgradují na vámi vybranou edici.
- **Kód Product Key:** Zadejte kód Product Key, který jste dostali od Microsoftu. Po vytvoření zásady s kódem Product Key nepůjde kód aktualizovat. Kód je také z bezpečnostních důvodů skrytý. Pokud chcete kód Product Key změnit, zadejte ho celý znovu.
- **Soubor s licencí**: U edice **Windows 10 Holographic for Business** nebo **Windows 10 Mobile** zvolte **Procházet** a vyberte licenční soubor, který jste dostali od Microsoftu. Tento soubor s licencí obsahuje informace o licencích pro edice, na které zařízení upgradujete.

## <a name="mode-switch"></a>Přepínač režimu

- **Žádná konfigurace**: zařízení v režimu s zůstane v režimu s. Koncový uživatel může zařízení přepnout z režimu S.
- **Zůstat v režimu S:** Zakáže koncovému uživateli přepnutí zařízení z režimu S.
- **Přepínač:** Přepne zařízení z režimu S.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nemusí ještě nic dělat. Nezapomeňte [profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily upgradu edice pro zařízení s [Windows holografickým pro firmy](holographic-upgrade.md) .
