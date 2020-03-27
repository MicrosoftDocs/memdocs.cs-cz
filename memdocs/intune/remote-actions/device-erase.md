---
title: Vymazání zařízení s macOS
titleSuffix: Microsoft Intune
description: Přečtěte si, jak ze zařízení s macOS vymažete všechna data, včetně operačního systému.
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
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3812dc710c28105436327c4049bfcd61611eeeaf
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80322578"
---
# <a name="erase-all-data-from-a-macos-device"></a>Vymazání všech dat ze zařízení s macOS

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Ze zařízení s macOS můžete vymazat veškerá data, včetně operačního systému. Zařízení se také odebere ze správy v Intune. Koncoví uživatelé nedostanou žádné upozornění.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **všechna zařízení** > vyberte zařízení, které chcete vymazat.
2. Klikněte na **Další** > **Vymazat** a zadejte 6 číslic pro **PIN kód pro obnovení**. Je to PIN kód, který je potřeba předat uživateli, aby si mohl na zařízení znovu nainstalovat operační systém. Nezapomeňte si tento PIN kód poznamenat, protože po dokončení akce vymazání se už nezobrazí.
![Snímek obrazovky](./media/device-erase/providepin.png)
3. Kliknutím na **OK** vymažte zařízení.
