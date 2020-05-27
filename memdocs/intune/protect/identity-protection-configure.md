---
title: Použití PIN kódu pro přihlášení k zařízením s Windows 10 pomocí Microsoft Intune – Azure | Microsoft Docs
description: Pomocí Windows Hello pro firmy umožníte uživatelům přihlásit se k zařízením pomocí PIN kódu, otisku prstu a dalších údajů. Pomocí těchto nastavení vytvořte v Intune pro zařízení s Windows 10 konfigurační profil ochrany identit a přiřaďte tento profil skupinám uživatelů a skupinám zařízení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 896574f956353c526858356fea40c2248ce70dd3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990784"
---
# <a name="use-windows-hello-for-business-on-windows-10-devices-with-microsoft-intune"></a>Použití Windows Hello pro firmy na zařízeních s Windows 10 s Microsoft Intune

Windows Hello pro firmy je metoda pro přihlašování k zařízením s Windows tím, že nahrazujete hesla, čipové karty a virtuální čipové karty. Intune obsahuje vestavěná nastavení, která správcům umožní nakonfigurovat a používat Windows Hello pro firmy. Tato nastavení můžete například použít k těmto akcím:

- Povolit Windows Hello pro firmy pro zařízení a uživatele
- Nastavte požadavky na PIN kód zařízení, včetně minimální nebo maximální délky PIN kódu.
- Povolení gest, jako je otisk prstu, které uživatelé můžou (nebo nemůžou použít) pro přihlášení k zařízením

Tato funkce je dostupná pro zařízení s následujícími systémy:

- Windows 10 a novější
- Windows 10 Mobile
- Windows Holographic for Business

Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu můžete tato nastavení vložit nebo nasadit do skupin uživatelů a zařízení ve vaší organizaci.

V tomto článku se dozvíte, jak vytvořit profil konfigurace zařízení. Seznam všech nastavení a jejich toho, co dělají, najdete v tématu [nastavení zařízení s Windows 10 a povolení Windows Hello pro firmy](identity-protection-windows-settings.md).

## <a name="create-the-device-profile"></a>Vytvoření profilu zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Zadejte tyto vlastnosti:

   - **Název**: Zadejte popisný název nového profilu.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
   - **Platforma**: vyberte **Windows 10 a novější**. Windows Hello pro firmy se podporuje jen na zařízeních s Windows 10 a novějšími.
   - **Typ profilu**: vyberte **Identity Protection**.

4. V podokně *Windows Hello pro firmy* nakonfigurujte následující možnosti:

   - **Konfigurace Windows Hello pro firmy**: vyberte, jak chcete nakonfigurovat Windows Hello pro firmy:

     - **Nenakonfigurováno** (výchozí): zřídí na zařízení [Windows Hello pro firmy](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning) . Pokud profily ochrany identit přiřazujete jen uživatelům, kontext zařízení nastaví výchozí hodnotu **Nenakonfigurováno**.

     - **Zakázáno**: Pokud nechcete používat Windows Hello pro firmy, vyberte tuto možnost. Tato možnost zakáže Windows Hello pro firmy pro všechny uživatele.

     - **Povoleno**: tuto možnost vyberte, pokud chcete [zřídit](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning)a nakonfigurovat nastavení Windows Hello pro firmy v Intune. Zadejte nastavení, která chcete nakonfigurovat. Seznam všech nastavení a jejich možnosti najdete v tématu [nastavení zařízení s Windows 10 k povolení Windows Hello pro firmy](identity-protection-windows-settings.md).

   - **Použít bezpečnostní klíče pro přihlášení**: Povolte klíč zabezpečení Windows Hello jako přihlašovací údaje pro všechny počítače v tenantovi.

     - **Povolení**
     - **Nenakonfigurováno** (výchozí)

5. Až budete hotovi, vyberte **OK**  >  **Create** a uložte změny.

Profil se vytvoří a zobrazí se v seznamu profily. V dalším kroku [přiřaďte](../configuration/device-profile-assign.md) tento profil skupinám uživatelů a zařízení, aby vyhovovaly vašim potřebám.

> [!IMPORTANT]
> Pokud chcete, aby bylo možné zřídit více uživatelů na zařízení, určete, že se pro zařízení použijí zásady Windows Hello pro firmy. Pokud se zásada použije jenom pro uživatele, dá se zařízení zřídit jenom u jednoho uživatele.

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/identity-protection-configure/disable-android-camera.png)

-->

## <a name="next-steps"></a>Další kroky

- Podívejte se na seznam všech [nastavení a co dělají](identity-protection-windows-settings.md).
- [Přiřaďte profil](../configuration/device-profile-assign.md) a [monitorujte jeho stav](../configuration/device-profile-monitor.md).
