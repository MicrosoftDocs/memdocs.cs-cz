---
title: Synchronizace zařízení s Microsoft Intune – Azure | Microsoft Docs
description: Můžete synchronizovat zařízení zaregistrovaná nebo spravovaná v Microsoft Intune, abyste získali nejnovější zásady a akce. Postup zahrnuje synchronizaci pomocí portálu Azure Portal a zobrazení kódů chyb, které umožňují opakovaný pokus.
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
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650a91d17223c31e02d660e47874a42731de572a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983019"
---
# <a name="sync-devices-to-get-the-latest-policies-and-actions-with-intune"></a>Synchronizace zařízení s cílem načíst nejnovější zásady a akce pomocí Intune


Akce zařízení **Synchronizovat** vybrané zařízení donutí se okamžitě ohlásit ve službě Intune. Jakmile se zařízení ohlásí, začne okamžitě přijímat veškeré čekající akce nebo zásady, které mu byly přiřazeny. Tato funkce vám může pomoct okamžitě ověřit a řešit potíže se zásadami, které jste přiřadili, aniž byste čekali na další plánované vrácení se změnami.

## <a name="supported-platforms"></a>Podporované platformy

- Windows
- telefon se systémem Windows
- iOS
- macOS
- Android

## <a name="sync-a-device"></a>Synchronizace zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). 
3. Vyberte **zařízení**  >  **všechna zařízení**.
4. V seznamu zařízení, která spravujete, vyberte zařízení a otevřete jeho podokno *přehledu* a pak vyberte **synchronizovat**.
5. Potvrďte zvolením **Ano**.

Pokud chcete zobrazit stav akce synchronizace, vyberte **zařízení**  >  **monitorovat**  >  **Akce zařízení**.

Standardní frekvence vrácení se změnami zásad služby Intune najdete v [časech obnovy cyklů](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="retryable-error-codes"></a>Kódy chyb umožňujících opakovaný pokus

Když správce spustí akci zařízení **synchronizovat** , aplikace pro iOS/IPadOS a Android, které selhaly a zvýšily kód chyby umožňující Opakovaný pokus, jsou pořád k dispozici pro zařízení. Aplikace, které vyvolaly kód chyby neumožňující opakovaný pokus, ale musí počkat sedm dní, než budou pro zařízení znovu dostupné.


| Kód chyby  | Navrhovaný popis | Možnost opakovaného pokusu |
|---|---|---|
| 2016330898 | Došlo k neznámé chybě. | Ne |
| 2016330897 | Vypršel časový limit vašeho připojení k Intune. Obnovte připojení. | Ano |
| 2016330896 | Ztratili jste připojení k internetu. Resetujte připojení. | Ano |
| 2016330895 | Ztratili jste připojení k internetu. Resetujte připojení. | Ano |
| 2016330894 | Ztratili jste připojení k internetu. Resetujte připojení. | Ano |
| 2016330893 | Ztratili jste připojení k internetu. Resetujte připojení. | Ano|
| 2016330892 | Mezinárodní roaming je zakázaný. | Ne|
| 2016330891 | K mobilnímu datovému připojení pro toto zařízení nelze připomenout během telefonního hovoru. Počkejte na dokončení telefonního hovoru. | Ano|
| 2016330890 | Pro tato zařízení nešlo v tuto chvíli  V tuto chvíli se tato zařízení nedala použít. | Ne|
| 2016330889 | Nepovedlo se navázat zabezpečené připojení. Resetujte připojení. | Ano|
| 2016330888 | Nepovedlo se vyhodnotit důvěryhodnost serveru. | No|

## <a name="next-steps"></a>Další kroky

Můžete [zkontrolovat podrobnosti](device-inventory.md) zařízení.
 
