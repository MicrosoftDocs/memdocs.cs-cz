---
title: Omezení funkcí zařízení pomocí zásad v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte profil zařízení, který omezí funkce pro správce zařízení s Androidem, Android Enterprise, macOS, iOS, iPadOS, Windows Phone a zařízení s Windows 10 v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 716925f077b7433eab06a6ea2f557c7653d0b03d
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551425"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Konfigurace nastavení omezení zařízení v Microsoft Intune

Intune zahrnuje zásady omezení zařízení, které správcům pomůžou řídit zařízení se systémem Android, iOS/iPadOS, macOS a Windows. Tato omezení umožňují řídit široké spektrum nastavení a funkcí pro ochranu prostředků vaší organizace. Správci můžou například:

- Povolí nebo blokuje fotoaparát zařízení.
- Řízení přístupu k Google Play, obchodům s aplikacemi, zobrazování dokumentů a hraní her.
- Zablokuje integrované aplikace nebo vytvoří seznam aplikací, které jsou povolené nebo zakázané.
- Povolí nebo zakáže zálohování souborů do účtů cloudu a úložiště.
- Nastavte minimální délku hesla a zablokujte jednoduchá hesla.

Tyto funkce jsou dostupné v Intune a správce je může nakonfigurovat. Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu můžete profil nainstalovat nebo nasadit do zařízení ve vaší organizaci.

V tomto článku se dozvíte, jak vytvořit profil omezení pro zařízení. Můžete si také prohlédnout všechna dostupná nastavení pro různé platformy.

> [!NOTE]
> Uživatelské rozhraní (UI) Intune se aktualizuje na celé obrazovce a může trvat několik týdnů. Až do chvíle, kdy váš tenant obdrží tuto aktualizaci, budete mít při vytváření nebo úpravách nastavení popsaných v tomto článku mírně odlišný pracovní postup.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Platforma**: vyberte platformu zařízení. Možnosti:  

        - **Správce zařízení s Androidem**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 a novější**
        - **Windows 8.1 a novější**
        - **Windows Phone 8.1**

    - **Profil**: vyberte **omezení zařízení**.

        Pokud chcete vytvořit profil omezení zařízení pro zařízení s Windows 10 Team, jako je například Surface Hub, zvolte **omezení zařízení (Windows 10 Team)** .

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **iOS/iPadOS: zablokovat kameru na zařízeních**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte platformu:

    - [Správce zařízení s Androidem](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 a novější](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu na konkrétní skupiny IT, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil je po vytvoření připravený k přiřazení. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
