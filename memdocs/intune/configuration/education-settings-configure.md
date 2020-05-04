---
title: Přidání nebo konfigurace nastavení vzdělávání v Microsoft Intune – Azure | Microsoft Docs
description: Použijte aplikaci pořizovat test v profilu konfigurace zařízení v zařízení s Windows 10 a novějším v Microsoft Intune. Vytvořte konfigurační profil pomocí nastavení vzdělávání a zadejte adresu URL testovací aplikace, vyberte způsob, jakým se uživatelé přihlásí, monitorovat obrazovku během testu a při testování povolí nebo zakáže návrhy textu.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12d04869834691167c2f31be853029c9a939a338
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79333091"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Použití aplikace nabrat na zařízeních s Windows 10 v Microsoft Intune



Vzdělávací profily v Intune jsou navržené pro studenty, kteří můžou na zařízeních pořizovat test nebo zkoušku. Tato funkce **zahrnuje testovací URL aplikaci a** nastavení, které umožňují přidat testovací adresu URL, zvolit způsob, jakým se koncoví uživatelé přihlásí k testu, a další. Tato funkce podporuje následující platformu:

- Windows 10 a novější

Když se uživatel přihlásí, automaticky se otevře testovací aplikace se zadaným testem. V zařízení nemůžou běžet žádné jiné aplikace, zatímco probíhá test. [Pořizovat testy ve Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) poskytují další podrobnosti o aplikaci převzít test.

V tomto článku jsou uvedené kroky pro vytvoření profilu konfigurace zařízení v Microsoft Intune. Obsahuje také informace o dostupných nastaveních vzdělávání pro vaše zařízení s Windows 10.

## <a name="create-a-device-profile"></a>Vytvoření profilu zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Konfigurace zařízení** > **profily** > konfigurace**vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Název**: Zadejte popisný název nového profilu.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: Zvolte **Windows 10 a novější**.
    - **Profil**: vyberte **vzdělávací profil**.

4. Zadejte nastavení, která chcete nakonfigurovat:

    - [Windows 10 a novější](education-settings-windows.md)

5. Kliknutím na **tlačítko OK** > **vytvořit** uložte změny.

Po zadání nastavení a vytvoření profilu se tento profil zobrazí v seznamu profilů. Dále [tento profil přiřaďte některým skupinám](device-profile-assign.md).

## <a name="next-steps"></a>Další kroky

Podívejte se na seznam [Nastavení vzdělávání pro Windows 10](education-settings-windows.md) a jejich popis.

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
