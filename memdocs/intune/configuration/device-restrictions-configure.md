---
title: Omezení funkcí zařízení pomocí zásad v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte profil zařízení, který omezí funkce pro správce zařízení s Androidem, Android Enterprise, macOS, iOS, iPadOS, Windows Phone a zařízení s Windows 10 v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f1e421a344122dbd4cf59a49ea56ef0ba2bb125
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087084"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Konfigurace nastavení omezení zařízení v Microsoft Intune

Intune zahrnuje zásady omezení zařízení, které správcům pomůžou řídit zařízení se systémem Android, iOS/iPadOS, macOS a Windows. Tato omezení umožňují řídit široké spektrum nastavení a funkcí pro ochranu prostředků vaší organizace. Správci můžou například:

- Povolí nebo zablokuje fotoaparát zařízení.
- Řízení přístupu k Google Play, obchodům s aplikacemi, zobrazování dokumentů a hraní her
- Zablokovat integrované aplikace nebo vytvořit seznam aplikací, které jsou povolené nebo zakázané
- Povolení nebo prevence zálohování souborů do účtů cloudu a úložiště
- Nastavit minimální délku hesla a zablokovat jednoduchá hesla

Tyto funkce jsou dostupné v Intune a správce je může nakonfigurovat. Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu můžete profil nainstalovat nebo nasadit do zařízení ve vaší organizaci.

V tomto článku se dozvíte, jak vytvořit profil omezení pro zařízení. Můžete si také prohlédnout všechna dostupná nastavení pro různé platformy.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **iOS/iPadOS: zablokovat kameru na zařízeních**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte platformu zařízení. Možnosti:  

        - **Správce zařízení s Androidem**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows Phone 8.1**
        - **Windows 8.1 a novější**
        - **Windows 10 a novější**

    - **Typ profilu**: vyberte **omezení zařízení**.

        Pokud chcete vytvořit profil omezení zařízení pro zařízení s Windows 10 Team, jako je například Surface Hub, zvolte **omezení zařízení (Windows 10 Team)** .

4. Nastavení, která můžete konfigurovat, se liší podle zvolené platformy. Pro podrobnější nastavení vyberte platformu:

    - [Nastavení správce zařízení s Androidem](device-restrictions-android.md)
    - [Nastavení Androidu Enterprise](device-restrictions-android-for-work.md)
    - [nastavení pro iOS/iPadOS](device-restrictions-ios.md)
    - [Nastavení macOS](device-restrictions-macos.md)
    - [Nastavení Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Nastavení Windows 10](device-restrictions-windows-10.md)
    - [Nastavení Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Nastavení Windows Holographic for Business](device-restrictions-windows-holographic.md)

5. Až to budete mít, vyberte **OK** > **Vytvořit** a změny uložte.

Profil se vytvoří a zobrazí se v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil je po vytvoření připravený k přiřazení. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
