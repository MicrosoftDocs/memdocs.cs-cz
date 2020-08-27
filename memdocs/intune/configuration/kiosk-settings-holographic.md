---
title: Nastavení veřejného terminálu pro Windows Holografick pro firmy v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurovat zařízení s Windows holografickým pro firmy jako veřejné terminály s jednou aplikací a s více aplikacemi, přizpůsobit nabídku Start, přidat aplikace, zobrazit panel úloh a nakonfigurovat webový prohlížeč v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8127281069ce4209adfc2aec82a93f5a60669307
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911858"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Nastavení zařízení s Windows holografickým pro firmy, která se mají spustit jako veřejný terminál v Intune

Zařízení s Windows Holographic for Business můžete nakonfigurovat tak, aby se spouštěla v režimu veřejného terminálu s jednou aplikací, nebo v režimu veřejného terminálu s více aplikacemi. Některé funkce nejsou na zařízení s Windows Holographic for Business podporované.

Tento článek obsahuje seznam a popis různých nastavení, která můžete řídit na zařízeních s Windows holografickým pro firmy. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete nakonfigurovat, aby zařízení s Windows holografickým podnikem běžela v celoobrazovkovém režimu.

Jako správce Intune můžete vytvořit a přiřadit tato nastavení k vašim zařízením.

Další informace o funkci veřejného terminálu Windows v Intune najdete v tématu [Konfigurace nastavení veřejného terminálu](kiosk-settings.md).

## <a name="before-you-begin"></a>Než začnete

- [Vytvoří konfigurační profil zařízení s Windows 10 v celoobrazovkovém](kiosk-settings.md#create-the-profile)režimu.

  Když vytvoříte konfigurační profil zařízení s Windows 10, budete mít víc nastavení, než jaké je uvedené v tomto článku. Nastavení v tomto článku jsou podporovaná na zařízeních s Windows holografickým pro firmy.

- Tento profil veřejného terminálu přímo souvisí s profilem omezení zařízení, které vytvoříte pomocí [nastavení Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser)na veřejném terminálu. Shrnutí:

  1. Vytvořte tento profil veřejného terminálu pro spuštění zařízení v celoobrazovkovém režimu.
  2. Umožňuje vytvořit [profil omezení zařízení](device-restrictions-windows-holographic.md#microsoft-edge-browser)a nakonfigurovat konkrétní funkce a nastavení povolená v Microsoft Edge.

> [!IMPORTANT]
> Ujistěte se, že tento profil pro terminál přiřadíte ke stejným zařízením jako váš [profil Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Jedna aplikace, celoobrazovkový terminál na celé obrazovce

Spustí na zařízení jenom jednu aplikaci. Jakmile se uživatel přihlásí, spustí se daná aplikace. Tento režim zároveň brání uživateli v otevírání nových aplikací nebo změně spuštěné aplikace.

- **Typ přihlášení uživatele**: Vyberte typ účtu, ve kterém se aplikace spouští. Možnosti:

  - **Automatické přihlašování (Windows 10 verze 1803 a novější)**: Nepodporováno ve Windows holografickém pro firmy.
  - **Účet místního uživatele**: Zadejte účet místního uživatele (v zařízení). Případně zadejte účet Microsoft (MSA), který je přidružený k aplikaci veřejného terminálu. Účet, který zadáte, se přihlaste k veřejnému terminálu.

    Pro veřejné terminály ve veřejných prostředích byste měli použít typ uživatele s nejnižším oprávněním.

- **Typ aplikace**: vyberte **Přidat aplikaci ze Storu**.

  - **Aplikace, která se má spustit v celoobrazovkovém režimu**: ze seznamu vyberte aplikaci.

    Nejsou v seznamu žádné aplikace? Přidejte aplikace pomocí postupu v části [Klientské aplikace](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Veřejný terminál s více aplikacemi

Aplikace v tomto režimu jsou k dispozici v nabídce Start. Tyto aplikace jsou jedinými aplikacemi, které může uživatel spustit. Pokud má aplikace závislost na jiné aplikaci, musí být v seznamu povolené aplikace zahrnutá obě.

- **Cílová zařízení s Windows 10 v režimu S**: vyberte **ne**. Režim S není podporován na Windows Holografick pro firmy.

- **Typ přihlášení uživatele**: Přidejte jeden nebo více uživatelských účtů, které mohou přidané aplikace používat. Možnosti:

  - **Automatické přihlašování (Windows 10 verze 1803 a novější)**: Nepodporováno ve Windows holografickém pro firmy.
  - **Účet místního uživatele**: **Přidejte** účet místního uživatele (v zařízení). Účet, který zadáte, se přihlaste k veřejnému terminálu.
  - **Uživatel nebo skupina Azure AD (Windows 10, verze 1803+)**: Vyžaduje zadání přihlašovacích údajů, aby se uživatel mohl k zařízení přihlásit. Vyberte **Přidat** a zvolte uživatele nebo skupiny Azure AD ze seznamu. Můžete vybrat více uživatelů a skupin. Zvolením možnosti **Vybrat** uložte změny.
  - **Návštěvník HoloLens**: Účet návštěvníka je účtem hosta, který nevyžaduje žádné přihlašovací údaje uživatele ani ověřování, viz článek o [konceptech režimu sdíleného počítače](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Prohlížeč a aplikace**: Přidejte aplikace, které se mají spustit v celoobrazovkovém zařízení. Nezapomeňte, že můžete přidat několik aplikací.

  - **Browsers**
    - **Přidat Microsoft Edge**: Microsoft Edge se přidá do mřížky aplikace a všechny aplikace můžou běžet na tomto terminálu. Vyberte typ beznabídkového režimu Microsoft Edge:

      - **Normální režim (plná verze Microsoft Edge)**: spustí plnou verzi Microsoft Edge se všemi funkcemi pro procházení. Data a stav uživatele jsou ukládána mezi relacemi.
      - **Veřejné procházení (InPrivate)**: spouští vícevrstvou verzi Microsoft Edge InPrivate s přizpůsobeným prostředím pro veřejné terminály, které běží v režimu celé obrazovky.

      Další informace o těchto možnostech najdete v tématu [nasazení celoobrazovkového režimu Microsoft Edge](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Toto nastavení povolí prohlížeči Microsoft Edge na zařízení. Pokud chcete nakonfigurovat nastavení specifické pro Microsoft Edge, vytvořte profil omezení zařízení (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Windows 10** pro platformu > **omezení zařízení**  >  **prohlížeč Microsoft Edge**). [Prohlížeč Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser) uvádí a popisuje dostupná nastavení pro holografické firmy.

    - **Přidat webový prohlížeč**na veřejném počítači: Nepodporováno ve Windows holografické pro firmy.

  - **Aplikace**
    - **Přidat aplikaci pro Store**: Vyberte existující aplikaci, kterou jste přidali nebo nasadili do Intune, jako [klientské aplikace](../apps/apps-add.md), včetně obchodních aplikací. Pokud nemáte uvedené žádné aplikace, podporuje Intune mnoho [typů aplikací](../apps/apps-add.md) , které [přidáte do Intune](../apps/store-apps-windows.md).
    - **Přidat aplikaci Win32**: Na zařízeních s Windows Holographic for Business se nepodporuje.
    - **Přidat podle AUMID**: Tuto možnost použijte pro přidání aplikací pro Windows, například Poznámkového bloku nebo Kalkulačky. Zadejte tyto vlastnosti:

      - **Název aplikace**: Povinné. Zadejte název aplikace.
      - **ID modelu uživatele aplikace (AUMID)**: Povinné. Zadejte ID modelu uživatele aplikace (AUMID) aplikace pro Windows. Pokud chcete získat toto ID, přečtěte si článek o tom, [jak u nainstalované aplikace najít ID modelu uživatele aplikace](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **AUTOLAUNCH**: volitelné. Po přidání aplikací a prohlížeče vyberte jednu aplikaci nebo prohlížeč, které se automaticky otevřou, když se uživatel přihlásí. Spustit se dá jenom jedna aplikace nebo prohlížeč.
    - **Velikost dlaždice**: Povinné. Po přidání aplikací vyberte malou, střední, širokou nebo velkou velikost dlaždice aplikace.

- **Použít alternativní počáteční rozložení**: vyberte **Ano** , pokud chcete zadat soubor XML, který popisuje, jak se aplikace objeví v nabídce Start, včetně pořadí aplikací. Tuto možnost použijte, pokud v nabídce Start potřebujete větší míru přizpůsobení. V článku o [přizpůsobení a exportu rozložení nabídky Start](/hololens/hololens-kiosk#start-layout-for-hololens) najdete pokyny a ukázkový soubor XML pro zařízení s Windows Holographic for Business.

- **Hlavní panel Windows**: Na zařízeních s Windows Holographic for Business se nepodporuje.
- **Povolení přístupu ke složce stažené soubory**: Nepodporováno ve Windows Holografick pro firmy.
- **Zadejte časové období údržby pro restartování aplikací**: nepodporuje se ve Windows holografickém pro firmy.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily pro celoobrazovkový režim pro zařízení s [Androidem](device-restrictions-android.md#kiosk), [Androidem Enterprise](device-restrictions-android-for-work.md#device-experience)a [Windows 10 a novějším](kiosk-settings-windows.md) .