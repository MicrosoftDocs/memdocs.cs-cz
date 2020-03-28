---
title: Používání vlastního nastavení zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte profil pro použití vlastního nastavení pro Windows Phone, Windows 8.1, Windows 10 a novější, Správce zařízení s Androidem, Android Enterprise, macOS a zařízení s iOS/iPadOS pomocí Microsoft Intune.
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
ms.openlocfilehash: c96de75557a4817f4e5f034689faecf7374cfe3f
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359429"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Vytvoření profilu s vlastním nastavením v Intune

Microsoft Intune obsahuje řadu integrovaných nastavení, které umožňují ovládat různé funkce zařízení. Můžete také vytvořit vlastní profily, které jsou vytvořeny podobně jako integrované profily. Vlastní profily jsou praktické, když chcete použít nastavení a funkce zařízení, která nejsou integrovaná do Intune. Tyto profily obsahují funkce a nastavení, která chcete ovládat na zařízeních v organizaci. Můžete například vytvořit vlastní profil, který nastaví stejnou funkci pro každé zařízení s iOS/iPadOS.

Vlastní nastavení se konfigurují pro každou platformu jinak. Třeba k ovládání funkcí na zařízeních s Androidem a Windows můžete zadat hodnoty OMA-URI (Open Mobile Alliance Uniform Resource Identifier). Do zařízení Apple můžete importovat soubor vytvořený v [Apple Configuratoru](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) nebo v [Apple Profile Manageru](https://support.apple.com/profile-manager).

Další informace o konfiguračních profilech najdete v tématu [Co jsou profily zařízení v Microsoft Intune?](device-profiles.md)

V tomto článku se dozvíte, jak vytvořit vlastní profil pro správce zařízení s Androidem, Android Enterprise, iOS/iPadOS, macOS a Windows. Můžete si také prohlédnout všechna dostupná nastavení pro různé platformy.

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
        - **Windows Phone 8.1**

    - **Profil**: vyberte **vlastní**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **Windows 10: vlastní profil, který umožňuje AllowVPNOverCellular vlastní OMA-URI**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte platformu:

    - [Správce zařízení s Androidem](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu na konkrétní skupiny IT, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="example"></a>Příklad

V následujícím příkladu je zapnuté nastavení **Connectivity/AllowVPNOverCellular**. Toto nastavení umožňuje zařízení s Windows 10, které je připojené k mobilní síti, otevřít připojení k síti VPN.

> [!div class="mx-imgBorder"]
> ![příklad vlastní zásady obsahující nastavení sítě VPN v Intune a ve Správci koncového bodu](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nemusí ještě nic dělat. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).
