---
title: Nastavení veřejného terminálu pro Windows a holografická zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurujte zařízení s Windows 10 (a novější) a zařízení s Windows holografickým pro firmy jako veřejné terminály s jednou aplikací a s více aplikacemi, přizpůsobte nabídku Start, přidejte aplikace, zobrazte panel úloh a nakonfigurujte webový prohlížeč v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9be644a47a361cf29e7b7132b2c87a4921553ea
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989428"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Nastavení zařízení s Windows 10 a Windows holografickým pro firmy, která se mají používat jako vyhrazené veřejné terminály pomocí Intune

V zařízeních s Windows 10 můžete pomocí Intune spouštět zařízení jako veřejný terminál, někdy označovaný jako vyhrazené zařízení. Zařízení v celoobrazovkovém režimu může spouštět jednu aplikaci nebo spouštět mnoho aplikací. Můžete zobrazit a přizpůsobit nabídku Start, přidat různé aplikace, včetně aplikací Win32, přidat konkrétní domovskou stránku do webového prohlížeče a další. 

Tato funkce platí pro:

- Windows 10 a novější
- Windows Holographic for Business

Pokud chcete vytvořit profily na veřejném terminálu pro jiné platformy, přečtěte si téma [Správce zařízení s Androidem](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)a [iOS/iPadOS](device-restrictions-ios.md#kiosk).

Intune podporuje jeden profil beznabídkového režimu v jednom zařízení. Pokud potřebujete více profilů beznabídkového režimu, můžete použít [vlastní OMA-URI](custom-settings-windows-10.md).

Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu můžete tato nastavení nasdílet nebo nasadit do skupin ve vaší organizaci.

V tomto článku se dozvíte, jak vytvořit profil konfigurace zařízení. Seznam všech nastavení a jejich toho, co dělají, najdete v tématu Nastavení veřejného [terminálu Windows 10](kiosk-settings-windows.md) a [Nastavení veřejného terminálu pro Windows holografick pro firmy](kiosk-settings-holographic.md).

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

   - **Platforma**: vyberte **Windows 10 a novější**.
   - **Profil**: vyberte možnost **celoobrazovkový**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

   - **Název**: Zadejte popisný název nového profilu.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**  >  **Vyberte celoobrazovkový režim**a zvolte typ celoobrazovkového režimu, který zásady podporuje. Mezi možnosti patří:

    - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Zásada nepovoluje celoobrazovkový režim.
    - **Beznabídkový režim na celou obrazovku s jednou aplikací**: Zařízení se spustí jako účet jednoho uživatele a uzamkne ho pro jednu aplikaci pro Store. Když se uživatel přihlásí, spustí se daná aplikace. Tento režim zároveň brání uživateli v otevírání nových aplikací nebo změně spuštěné aplikace.
    - **Veřejný terminál s více aplikacemi**: Zařízení spustí více aplikací pro Store, aplikací Win32 nebo vnitřních aplikací pro Windows pomocí ID uživatele aplikace (AUMID). Na zařízení jsou dostupné pouze aplikace, které přidáte.

        Veřejný terminál s více aplikacemi, neboli zařízení s pevně stanoveným účelem, umožňuje poskytovat přehledné prostředí uživatelům, protože jim povoluje přístup pouze k aplikacím, které potřebují. A také z jejich zobrazení z pohledu aplikací, které nepotřebují.

    Seznam všech nastavení a o tom, co dělají, najdete v těchto tématech:

      - [Nastavení beznabídkového režimu Windows 10](kiosk-settings-windows.md)
      - [Nastavení veřejného terminálu pro Windows Holografick pro firmy](kiosk-settings-holographic.md)

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupinu uživatelů, kteří obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Při příštím ověření každého zařízení se zásada použije.

## <a name="next-steps"></a>Další kroky

Po [přiřazení profilu](device-profile-assign.md) [sledujte jeho stav](device-profile-monitor.md).

Pro zařízení s následujícími platformami můžete vytvořit profily na veřejném terminálu:

- [Správce zařízení s Androidem](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 a novější](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
