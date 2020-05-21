---
title: Surface Hub omezení pro zařízení s Windows 10 Team v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Pomocí Intune můžete přidat nebo nakonfigurovat nastavení Surface Hub zařízení s Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429691"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Nastavení Windows 10 Team pro povolení nebo omezení funkcí v zařízeních Surface Hub s využitím Intune

V tomto článku se dozvíte, jak Microsoft Intune nastavení omezení zařízení, která můžete nakonfigurovat pro zařízení s Windows 10 Team, včetně zařízení Surface Hub.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil zařízení](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>Aplikace a prostředí

Tato nastavení používají [zprostředkovatele CSP pro SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Probuzení obrazovky, když je někdo v místnosti**: **blok** brání automatickému probuzení obrazovky, když senzor detekuje někoho v místnosti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Informace o schůzce zobrazené na úvodní obrazovce**: vyberte informace, které se zobrazí na dlaždici schůzky na úvodní obrazovce. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Jenom organizátor a čas**
  - **Organizátor, čas a předmět (u privátních schůzek je předmět skrytý)**
- **Adresa URL obrázku pozadí úvodní obrazovky**: zadejte adresu URL obrázku. png, který chcete mít na **úvodní** obrazovce na zařízeních s Windows 10 Team, jako vlastní pozadí. Obrázek musí být ve formátu PNG a adresa URL musí začínat na `https://` .
- **Automaticky spustit připojení**: **blok** zabraňuje automatickému otevírání aplikace Connect při spuštění projekce. Pokud je blokované, uživatelé můžou ručně spustit aplikaci připojit z nastavení centra. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Návrhy přihlašování**: **blok** zakáže automatické vyplňování přihlašovacího dialogu pomocí pozvánek z plánovaných schůzek. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Moje schůzky a soubory**: **blok** zakáže funkci **Moje schůzky a soubory** v nabídce Start. Tato funkce zobrazuje schůzky a soubory přihlášeného uživatele z Office 365. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights**: **umožňuje** shromažďovat, ukládat a analyzovat data protokolů ze zařízení s Windows 10 Team pomocí Azure Operational Insights. Azure Operational Insights je součástí sady Microsoft Operations Manager Suite. Zadejte **ID pracovního prostoru** a **klíč pracovního prostoru** pro připojení k Azure Operational Insights.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí tato data shromažďovat.

## <a name="maintenance"></a>Údržba

Tato nastavení používají [zprostředkovatele CSP pro SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- Časové **období údržby pro aktualizace**: **možnost Povolit** vytvoří okno údržby, když se můžou aktualizace nainstalovat. Zadejte **čas spuštění časového**období údržby a **dobu v hodinách**od 1-5 hodin.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="session"></a>Relace

Tato nastavení používají [zprostředkovatele CSP pro SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Svazek**: zadejte výchozí hodnotu svazku pro novou relaci, od 0-100. Pokud je ponecháno prázdné, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení může operační systém nastavit svazek na 45.
- **Časový limit obrazovky**: zadejte počet minut, než se vypne obrazovka centra.
- **Časový limit relace**: zadejte počet minut, než vyprší časový limit relace.
- **Časový limit režimu spánku**: zadejte počet minut, než centrum přejde do režimu spánku.
- **Session Resume**: **Block** zabraňuje uživatelům v pokračování relace, když vyprší časový limit relace. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="wireless-projection"></a>Bezdrátová projekce

Tato nastavení používají [zprostředkovatele CSP pro SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **PIN pro bezdrátovou projekci**: **vyžaduje** , aby uživatelé před použitím funkcí bezdrátové projekce na zařízení zadali PIN kód. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Bezdrátová projekce Miracast**: **blok** zabraňuje použití zařízení s podporou Miracast k projektu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Kanál bezdrátové projekce Miracast**: vyberte kanál Miracast pro navázání připojení.

## <a name="next-steps"></a>Další kroky

Další informace najdete v tématu [Konfigurace nastavení omezení zařízení](device-restrictions-configure.md).

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).
