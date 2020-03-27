---
title: Aktivace režimu ztráty zařízení s iOS/iPadOS pomocí Microsoft Intune – Azure | Microsoft Docs
description: Zapněte nebo spusťte režim ztráty a upravte zprávu, která se zobrazí na zamykací obrazovce ztraceného nebo odcizeného zařízení s iOS/iPadOS, pomocí Microsoft Intune. Při použití akce Režim ztráty získáte také podrobnosti o zabezpečení a ochraně osobních údajů.
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
ms.assetid: 126a7489-fe3e-43fd-a681-defb2fe0bb66
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cf638ba82d1b6e91e3c4c24d5cfd3433df3b010
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326530"
---
# <a name="enable-lost-mode-on-iosipados-devices-with-intune"></a>Povolení režimu ztráty na zařízeních s iOS/iPadOS pomocí Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Akce zařízení v **režimu ztráty** vám pomůže zapnout režim ztráty u ztracených nebo odcizených zařízení s iOS/iPadOS. Tento režim vám umožňuje zadat zprávu a telefonní číslo, které se zobrazuje na zamykací obrazovce zařízení. Pokud chcete použít režim ztráty, musí být zařízení ve vlastnictví firmy iOS/iPadOS, které je v režimu pod dohledem.

## <a name="supported-platforms"></a>Podporované platformy

- iOS 9.3 nebo novější
- iPadOS 13,0 nebo novější

Tato funkce není podporovaná pro: 
- Windows
- Windows Phone
- macOS
- Android

## <a name="enable-lost-mode"></a>Zapnutí režimu ztráty

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **Zařízení** a potom **Všechna zařízení**.
4. V seznamu zařízení, která spravujete, zvolte zařízení s iOS/iPadOS a pak zvolte **režim ztráty (jenom pod dohledem)** .
5. V části **režim ztráty**vyberte **Povolit**.
6. Ve **zprávě, která se má zobrazit na zamykací obrazovce**zadejte zprávu, která se zobrazí na zamykací obrazovce zařízení.
7. Volitelně můžete zadat telefonní číslo do pole **telefonní číslo, které se má zobrazit** .
6. Výběrem **OK** uložte změny.

Když zapnete režim ztráty, zablokujete veškeré možnosti použití zařízení. Koncový uživatel nebude mít k zařízení přístup, dokud režim ztráty nevypnete. Když je režim ztráty zapnutý, můžete pomocí akce [Najít zařízení](device-locate.md) zjistit, kde se zařízení nachází.

## <a name="security-and-privacy-information-for-the-lost-mode-and-locate-device-actions"></a>Informace o zabezpečení a ochraně osobních údajů pro akce Režim ztráty a Najít zařízení
- Dokud tuto akci nezapnete, neodesílají se do Intune žádné informace o poloze zařízení.
- Když použijete akci Najít zařízení, údaje o poloze zařízení – zeměpisná šířka a délka – se odešlou do Intune a zobrazí se na portálu Azure Portal.
- Tady tyto údaje zůstanou uložené 24 hodin a pak se odeberou. Údaje o poloze se nedají ručně odebrat.
- Údaje o poloze jsou při uložení i při přenosu zašifrované.
- Ve zprávě, která se zobrazí na zamykací obrazovce, nezapomeňte uvést konkrétní podrobnosti o vrácení ztraceného zařízení.

## <a name="next-steps"></a>Další kroky

Pokud se chcete podívat na stav zapnutí režimu ztráty, otevřete **Zařízení** a vyberte **Akce zařízení**.
