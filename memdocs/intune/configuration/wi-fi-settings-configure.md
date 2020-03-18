---
title: Vytvoření profilu Wi-Fi pro zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Projděte si postup vytvoření konfiguračního profilu zařízení v Microsoft Intune. Vytvářejte profily pro Android, Android Enterprise, Android webceloobrazovkový, iOS, iPadOS, macOS, Windows 10 a novější a Windows Holografick pro firmy. Pomocí těchto profilů můžete vytvořit připojení Wi-Fi pro použití certifikátů, volbu typu protokolu EAP, výběr metody ověřování, povolení proxy a další.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5297f87dd3aad6b88281b491ccb7c1f0878ffc1e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326567"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Přidání a použití nastavení Wi-Fi na zařízeních v Microsoft Intune

Wi-Fi je bezdrátová síť, kterou používá mnoho mobilních zařízení k získání přístupu k síti. Microsoft Intune obsahuje vestavěná nastavení Wi-Fi, která se dají nasadit pro uživatele a zařízení ve vaší organizaci. Tato skupina nastavení se nazývá "profil" a je možné ji přiřadit různým uživatelům a skupinám. Po přiřazení získají vaši uživatelé přístup k síti Wi-Fi vaší organizace bez toho, aby ji nakonfigurovali sami.

Můžete třeba nainstalovat novou Wi-Fi síť nazvanou Contoso Wi-Fi. Pak budete chtít nastavit všechna zařízení se systémem iOS/iPadOS pro připojení k této síti. Postup je následující:

1. Vytvořte profil sítě Wi-Fi, který obsahuje nastavení, která se připojují k bezdrátové síti Contoso Wi-Fi.
2. Přiřaďte profil ke skupině, která obsahuje všechny uživatele zařízení se systémem iOS/iPadOS.
3. Uživatelé najdou novou síť Contoso Wi-Fi v seznamu bezdrátových sítí na svém zařízení. Potom se mohou k této síti připojit s využitím metody ověřování, kterou zvolíte.

Tento článek obsahuje seznam kroků pro vytvoření profilu sítě Wi-Fi. Obsahuje také odkazy, které popisují různá nastavení pro jednotlivé platformy.

## <a name="supported-device-platforms"></a>Podporované platformy zařízení

Profily Wi-Fi podporují zařízení s následujícími platformami:

- Android 4 a novější
- Android Enterprise a beznabídkový režim
- iOS 8,0 a novější
- iPadOS 13,0 a novější
- macOS X 10,11 a novější
- Windows 10 a novější, Windows 10 Mobile a Windows Holografick pro firmy

> [!NOTE]
> Pro zařízení s Windows 8.1 můžete importovat konfiguraci Wi-Fi, kterou předtím vyexportujete z jiného zařízení.

## <a name="create-a-device-profile"></a>Vytvoření profilu zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil WiFi pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte platformu zařízení. Možnosti:

      - **Androidemem**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 8.1 a novější**
      - **Windows 10 a novější**

    - **Typ profilu**: vyberte **Wi-Fi**.

      > [!TIP]
      >
      > - Pro zařízení s **Androidem Enterprise** spuštěná jako vyhrazené zařízení (beznabídkový režim) vyberte **pouze vlastník zařízení** > **Wi-Fi**.
      > - U **Windows 8.1 a novějších verzí** můžete zvolit **Import Wi-Fi**. Tato možnost umožňuje importovat nastavení Wi-Fi jako soubor XML, který jste předtím vyexportovali z jiného zařízení.

4. Některá nastavení Wi-Fi se u jednotlivých platforem liší. Pokud chcete zobrazit nastavení pro konkrétní platformu, vyberte svou platformu:

    - [Androidemem](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), včetně vyhrazených zařízení
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 a novější](wi-fi-settings-windows.md)
    - [Windows 8.1 a novější](wi-fi-settings-import-windows-8-1.md) (včetně Windows Holographic for Business)

5. Až budete hotovi, vyberte **vytvořit profil** > **vytvořit**.

Profil se vytvoří a zobrazí se v seznamu profilů (**Konfigurace zařízení** > **profily**).

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Pak [přiřaďte tento profil](device-profile-assign.md) a [sledujte jeho stav.](device-profile-monitor.md)..

[Problémy s profily sítě Wi-Fi v Intune](troubleshoot-wi-fi-profiles.md).
