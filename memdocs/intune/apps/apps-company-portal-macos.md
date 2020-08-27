---
title: Přidání Portál společnosti pro aplikaci macOS
titleSuffix: Microsoft Intune
description: Přidejte aplikaci macOS Portál společnosti.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1eb64f8ed2bc67b4800a4583010dea150ade421d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914153"
---
# <a name="add-the-macos-company-portal-app"></a>Přidání aplikace Portál společnosti macOS

Aby bylo možné spravovat zařízení, instalovat volitelné aplikace a získat přístup k prostředkům chráněným pomocí podmíněného přístupu na zařízeních macOS s přidružením uživatele, musí si uživatelé nainstalovat aplikaci Portál společnosti a přihlásit se k ní. Uživatelům můžete poskytnout pokyny k instalaci Portál společnosti pro macOS nebo jejich instalaci do zařízení, která jsou už zaregistrovaná přímo v Intune.

K instalaci Portál společnosti pro aplikaci macOS můžete použít kteroukoli z následujících možností:
- [Vyzvat uživatele ke stažení a instalaci Portál společnosti](#instruct-users-to-download-and-install-company-portal)
- [Instalace Portál společnosti pro macOS jako aplikace macOS LOB](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Instalace Portál společnosti pro macOS pomocí skriptu prostředí macOS](#install-company-portal-for-macos-by-using-a-macos-shell-script)

Pro lepší zabezpečení a aktuálnost aplikací po instalaci aplikace Portál společnosti dodávána s Microsoft AutoUpdate (MAU).

> [!NOTE]
> Aplikaci Portál společnosti lze nainstalovat do zařízení pomocí služby Intune, které jsou již zaregistrovány pomocí přímého registrace nebo automatizovaného registrace zařízení. Pro osobní zařízení nebo ruční registrace se musí stáhnout a nainstalovat aplikace Portál společnosti pro zahájení registrace. Viz [pokyn pro uživatele ke stažení a instalaci portál společnosti](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Vyzvat uživatele ke stažení a instalaci Portál společnosti

Můžete uživatelům dát pokyn ke stažení, instalaci a přihlášení Portál společnosti pro macOS. Pokyny ke stažení, instalaci a přihlášení do Portál společnosti najdete v tématu [registrace zařízení MacOS pomocí portál společnosti aplikace](../user-help/enroll-your-device-in-intune-macos-cp.md).

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>Instalace Portál společnosti pro macOS jako aplikace macOS LOB

Portál společnosti pro macOS se dají stáhnout a nainstalovat pomocí funkce [MACOS LOB pro aplikace](lob-apps-macos.md) . Stažená verze je verze, která bude vždy nainstalována a může být nutné ji pravidelně aktualizovat, aby se uživatelé mohli při prvotní registraci lépe doskytnout.

1. Stáhnout Portál společnosti pro macOS z https://go.microsoft.com/fwlink/?linkid=853070 . 

2. Podle pokynů vytvořte v [aplikacích pro MACOS LOB](lob-apps-macos.md)obchodní aplikaci MacOS.

> [!NOTE]
> Po nainstalování se aplikace Portál společnosti for macOS automaticky aktualizuje pomocí služby Microsoft AutoUpdate (MAU).
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>Instalace Portál společnosti pro macOS pomocí skriptu prostředí macOS

Portál společnosti pro macOS se dají stáhnout a nainstalovat pomocí funkce [skriptů prostředí MacOS](macos-shell-scripts.md) . Tato možnost vždy nainstaluje aktuální verzi Portál společnosti pro macOS, ale neposkytne vám vytváření sestav instalace aplikací, které můžete použít k nasazení aplikací pomocí [MacOS obchodních aplikací](lob-apps-macos.md).

1. Stáhněte si ukázkový skript pro instalaci Portál společnosti pro macOS z ukázkových [skriptů prostředí Intune-portál společnosti](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal).

2. Postupujte podle pokynů pro nasazení skriptu prostředí macOS pomocí [skriptů prostředí MacOS](macos-shell-scripts.md). 
    - Nastavte **Spustit skript jako přihlášeného uživatele** na **ne** (pro spuštění v kontextu systému).
    - Nastaví **maximální počet opakovaných pokusů, pokud se skript** nepovede na **3**.

> [!NOTE]
> Skript bude vyžadovat přístup k Internetu, pokud je spuštěn pro stažení aktuální verze Portál společnosti pro macOS. 
## <a name="next-steps"></a>Další kroky
- Další informace o přiřazování aplikací najdete v tématu [přiřazení aplikací do skupin](apps-deploy.md).
- Další informace o konfiguraci automatizované registrace zařízení najdete v tématu [program registrace zařízení – MacOS registrace](../enrollment/device-enrollment-program-enroll-macos.md).
- Další informace o konfiguraci nastavení Microsoft AutoUpdate na macOS najdete v tématu [aktualizace pro Mac](/windows/security/threat-protection/microsoft-defender-atp/mac-updates).