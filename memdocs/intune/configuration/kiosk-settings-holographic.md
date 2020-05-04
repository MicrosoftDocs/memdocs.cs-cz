---
title: Nastavení veřejného terminálu pro Windows Holografick pro firmy v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurovat zařízení s Windows holografickým pro firmy jako veřejné terminály s jednou aplikací a s více aplikacemi, přizpůsobit nabídku Start, přidat aplikace, zobrazit panel úloh a nakonfigurovat webový prohlížeč v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18de92792582d4c6753bc8657c56d73fa1509788
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359129"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Nastavení zařízení s Windows holografickým pro firmy, která se mají spustit jako veřejný terminál v Intune

Zařízení s Windows Holographic for Business můžete nakonfigurovat tak, aby se spouštěla v režimu veřejného terminálu s jednou aplikací, nebo v režimu veřejného terminálu s více aplikacemi. Některé funkce nejsou na zařízení s Windows Holographic for Business podporované.

Tento článek obsahuje seznam a popis různých nastavení, která můžete řídit na zařízeních s Windows holografickým pro firmy. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete nakonfigurovat, aby zařízení s Windows holografickým podnikem běžela v celoobrazovkovém režimu.

Jako správce Intune můžete vytvořit a přiřadit tato nastavení k vašim zařízením.

Další informace o funkci veřejného terminálu Windows v Intune najdete v tématu [Konfigurace nastavení veřejného terminálu](kiosk-settings.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil](kiosk-settings.md#create-the-profile).

## <a name="single-full-screen-app-kiosks"></a>Veřejné terminály s jednou aplikací v režimu na celou obrazovku

Když zvolíte beznabídkový režim s jednou aplikací, zadejte následující nastavení:

- **Typ přihlášení uživatele**: Vyberte **Účet místního uživatele** a zadejte účet místního uživatele (v zařízení) nebo účet Microsoft (MSA) přidružený k aplikaci veřejného terminálu. Typy uživatelských účtů **Automatické přihlášení** nejsou na zařízení s Windows Holographic for Business podporované.

- **Typ aplikace**: Vyberte **aplikaci pro Store**.

- **Aplikace, která se spustí v beznabídkovém režimu**: Zvolte **Přidat aplikaci pro Store** a vyberte aplikaci ze seznamu.

    Nejsou v seznamu žádné aplikace? Přidejte aplikace pomocí postupu v části [Klientské aplikace](../apps/apps-add.md).

    Výběrem **OK** uložte změny.

## <a name="multi-app-kiosks"></a>Veřejné terminály s více aplikacemi

Aplikace v tomto režimu jsou k dispozici v nabídce Start. Tyto aplikace jsou jedinými aplikacemi, které může uživatel spustit. Když zvolíte beznabídkový režim s více aplikacemi, zadejte následující nastavení:

- **Cílit na zařízení s Windows 10 v režimu S**: Zvolte **Ne**. Režim S není podporován na Windows Holografick pro firmy.

- **Typ přihlášení uživatele**: Přidejte jeden nebo více uživatelských účtů, které mohou přidané aplikace používat. Možnosti: 

  - **Automatické přihlášení**: Na zařízeních s Windows Holographic for Business se nepodporuje.
  - **Účet místního uživatele**: **Přidejte** účet místního uživatele (v zařízení). Zadaný účet se používá pro přihlášení k veřejnému terminálu.
  - **Uživatel nebo skupina Azure AD (Windows 10, verze 1803+)**: Vyžaduje zadání přihlašovacích údajů, aby se uživatel mohl k zařízení přihlásit. Vyberte **Přidat** a zvolte uživatele nebo skupiny Azure AD ze seznamu. Můžete vybrat více uživatelů a skupin. Zvolením možnosti **Vybrat** uložte změny.
  - **Návštěvník HoloLens**: Účet návštěvníka je účtem hosta, který nevyžaduje žádné přihlašovací údaje uživatele ani ověřování, viz článek o [konceptech režimu sdíleného počítače](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Aplikace**: Přidejte aplikace, které se budou spouštět zařízení s beznabídkovým režimem. Nezapomeňte, že můžete přidat několik aplikací.

  - **Přidat aplikace pro Store**: Vyberte existující aplikaci, kterou jste přidali nebo nasadili do Intune, jako [klientské aplikace](../apps/apps-add.md), včetně obchodních aplikací. Pokud nemáte uvedené žádné aplikace, podporuje Intune mnoho [typů aplikací](../apps/apps-add.md) , které [přidáte do Intune](../apps/store-apps-windows.md).
  - **Přidat aplikaci Win32**: Na zařízeních s Windows Holographic for Business se nepodporuje.
  - **Přidat podle AUMID**: Tuto možnost použijte pro přidání vnitřních aplikací pro Windows. Zadejte tyto vlastnosti: 

    - **Název aplikace**: Povinné. Zadejte název aplikace.
    - **ID modelu uživatele aplikace (AUMID)**: Povinné. Zadejte ID modelu uživatele aplikace (AUMID) aplikace pro Windows. Pokud chcete získat toto ID, přečtěte si článek o tom, [jak u nainstalované aplikace najít ID modelu uživatele aplikace](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).
    - **Velikost dlaždice**: Povinné. Zvolte velikost dlaždice aplikace – malá, střední, široká nebo velká.

- **Nastavení Kiosk Browseru**: Na zařízeních s Windows Holographic for Business se nepodporuje.

- **Použít alternativní rozložení nabídky Start**: Zvolte **Ano**, pokud chcete zadat soubor XML, který popisuje, jak se aplikace zobrazují v nabídce Start (včetně jejich pořadí). Tuto možnost použijte, pokud v nabídce Start potřebujete větší míru přizpůsobení. V článku o [přizpůsobení a exportu rozložení nabídky Start](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) najdete pokyny a ukázkový soubor XML pro zařízení s Windows Holographic for Business.

- **Hlavní panel Windows**: Na zařízeních s Windows Holographic for Business se nepodporuje.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily pro celoobrazovkový režim pro zařízení s [Androidem](device-restrictions-android.md#kiosk), [Androidem Enterprise](device-restrictions-android-for-work.md#dedicated-devices)a [Windows 10 a novějším](kiosk-settings-windows.md) .
