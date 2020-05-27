---
title: Vyhledání ztracených zařízení s iOS/iPadOS pomocí Microsoft Intune – Azure | Microsoft Docs
description: Pomocí funkce najít zařízení v Microsoft Intune Najděte ztracená nebo odcizená zařízení s iOS/iPadOS. Získejte podrobnosti o zabezpečení a ochraně osobních údajů při používání akce Najít zařízení.
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
ms.assetid: 3e544286-12ad-4a3a-86f8-d2cf16940b1f
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 825105fb11c37293285638e8d86514aae4ba8303
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989879"
---
# <a name="locate-lost-or-stolen-iosipados-devices-with-intune"></a>Vyhledání ztracených nebo odcizených zařízení s iOS/iPadOS pomocí Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Pokud chcete zjistit umístění ztraceného nebo odcizeného zařízení s iOS/iPadOS na mapě, použijte akci **Najít zařízení** . Zařízení musí být v režimu dohledu. Než použijete tuto akci, zkontrolujte, že je zařízení v [režimu ztráty](device-lost-mode.md).

## <a name="supported-platforms"></a>Podporované platformy

- iOS/iPadOS 9,3 a novější

Tato funkce není podporovaná pro tyto systémy: 
- Windows
- telefon se systémem Windows
- macOS
- Android

## <a name="locate-a-lost-or-stolen-device"></a>Vyhledání ztraceného nebo odcizeného zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **Zařízení** a potom **Všechna zařízení**.
4. V seznamu zařízení, která spravujete, vyberte zařízení s iOS/iPadOS a vyberte **... Další**. Pak zvolte vzdálenou akci **Najít zařízení**.
5. Po nalezení zařízení se jeho poloha zobrazí v části **Najít zařízení**.
    ![Snímek obrazovky z funkcí Najít zařízení pomocí Intune v Azure](./media/device-locate/locate-device.png)


## <a name="activate-lost-mode-sound-alert-on-an-ios-device"></a>Aktivace zvukového upozornění v režimu ztráty na zařízení s iOSem

Pokud někdo ztratil zařízení se systémem iOS/iPadOS 9,3 nebo novějším, můžete zařízení vzdáleně aktivovat a přehrát zvuk, aby ho uživatel mohl najít. Zařízení musí být v [režimu ztráty](device-lost-mode.md).

V [Intune v Azure Portal](https://aka.ms/intuneportal)zvolte **zařízení**  >  **všechna zařízení** > vybrat zařízení se systémem iOS/iPadOS > **Přehled**  >  **dalšího**  >  **přehrání zvuku režimu ztráty (jenom pod dohledem)**.

Zvuk se bude přehrávat, dokud ho uživatel na zařízení nedeaktivuje nebo se zařízení neodebere z režimu ztráty.


## <a name="security-and-privacy-information-for-lost-mode-and-locate-device-actions"></a>Informace o zabezpečení a ochraně osobních údajů pro akce Režim ztráty a Najít zařízení
- Dokud tuto akci nezapnete, neodesílají se do Intune žádné informace o poloze zařízení.
- Když použijete akci Najít zařízení, můžete pomocí Graph API získat údaje o poloze zařízení (zeměpisné šířce a délce).
- Tady tyto údaje zůstanou uložené 24 hodin a pak se odeberou. Údaje o poloze se nedají ručně odebrat.
- Údaje o poloze jsou při uložení i při přenosu zašifrované.
- Při konfiguraci režimu ztráty můžete přizpůsobit zprávu, která se zobrazí na zamykací obrazovce. V této zprávě určené osobě, která ztracené zařízení najde, nezapomeňte uvést konkrétní podrobnosti o vrácení ztraceného zařízení.

## <a name="next-steps"></a>Další kroky

Pokud se chcete podívat na stav povolení funkce Najít zařízení, otevřete **Zařízení** a vyberte **Akce zařízení**.
