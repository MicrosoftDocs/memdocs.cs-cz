---
title: Přehled životního cyklu aplikace pro Microsoft Intune
description: Přečtěte si o životním cyklu spravovaných aplikací v Microsoft Intune. Životní cyklus aplikace zahrnuje přidání, nasazení, konfiguraci, ochranu a vyřazení aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60347012-bc3f-4b9a-a4f4-6d3c5021a6e6
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: apps; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33f59cc2ecd2662e2d5d09fb06a9f1c7a33f0fca
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326331"
---
# <a name="overview-of-the-app-lifecycle-in-microsoft-intune"></a>Přehled životního cyklu aplikace v Microsoft Intune

Životní cyklus aplikace Microsoft Intune začíná, když je aplikace přidána, a postupuje dalšími fázemi, dokud ji neodeberete. Když pochopíte tyto fáze, budete mít k dispozici podrobné informace, které vám pomohou začít se správou aplikací v Intune.

![Životní cyklus aplikace – přidání, nasazení, konfigurace, ochrana a vyřazení z provozu.](./media/app-lifecycle/app-lifecycle.png "životní cyklus aplikace Intune")

## <a name="add"></a>Přidat

Prvním krokem při nasazení aplikací je přidání aplikací, které chcete spravovat a přiřazovat, do Intune. Můžete pracovat s mnoha různými typy aplikací, ale základní postupy jsou stejné. Pomocí Intune můžete přidat různé typy aplikací, včetně aplikací, které jsou zapsané interně (obchodní), aplikací ze Storu, aplikací, které jsou integrované, a aplikací na webu. Další informace o těchto typech aplikací najdete v článku [Přidání aplikací do Microsoft Intune](apps-add.md).

## <a name="deploy"></a>Nasadit

Po přidání aplikace do Intune ji pak můžete [přiřadit uživatelům a zařízením, která spravujete](apps-deploy.md). Intune tento proces usnadňuje a po nasazení aplikace můžete [monitorovat úspěšnost](apps-monitor.md) nasazení z Intune v rámci Azure Portal. Kromě toho některé obchody s aplikacemi, jako jsou obchody pro [Apple](vpp-apps-ios.md) a [Windows](windows-store-for-business.md), umožňují vaší společnosti nákup hromadných licencí k aplikaci. Intune může synchronizovat data s těmito obchody, abyste mohli nasazovat a sledovat využití licencí pro tyto typy aplikací přímo z konzoly pro správu Intune.

## <a name="configure"></a>Konfigurace

Jako součást životního cyklu aplikace jsou pravidelně vydávány nové verze aplikace. Intune poskytuje nástroje ke snadné [aktualizaci aplikací](apps-add.md), které jste nasadili, na novější verzi. Kromě toho můžete pro některé aplikace konfigurovat další funkce, například:

- [zásady konfigurace aplikací pro iOS/iPadOS](app-configuration-policies-use-ios.md) poskytují nastavení pro kompatibilní aplikace pro iOS/iPadOS, které se používají při spuštění aplikace. Aplikace může například vyžadovat konkrétní nastavení brandingu nebo název serveru, ke kterému se musí připojit.
- [Zásady spravovaného prohlížeče](app-configuration-managed-browser.md) vám pomůžou nakonfigurovat nastavení pro [Microsoft Edge](apps-supported-intune-apps.md#microsoft-apps), které nahradí výchozí prohlížeč zařízení a umožní vám omezit weby, které můžou uživatelé navštěvovat.

## <a name="protect"></a>Chránit

Intune poskytuje mnoho způsobů, jak pomoci chránit data ve vašich aplikacích. Hlavní metody jsou následující:

- [Podmíněný přístup](../protect/conditional-access.md), který řídí přístup k e-mailu a dalším službám na základě podmínek, které zadáte. Příkladem podmínek může být typ zařízení nebo shoda se [zásadami dodržování předpisů zařízení](../protect/device-compliance-get-started.md), které jste nasadili.
- [Zásady ochrany aplikací](app-protection-policy.md) spolupracují s jednotlivými aplikacemi a pomáhají chránit firemní data, která používají. Například můžete omezit kopírování dat mezi nespravovanými a spravovanými aplikacemi, nebo můžete zabránit aplikacím ve spuštění v zařízeních s jailbreakem nebo rootem.

## <a name="retire"></a>Vyřadit

Nakonec pravděpodobně dojde k tomu, že nasazené aplikace začnou být zastaralé a bude třeba je odebrat. Intune umožňuje snadno [vyřazovat aplikace z provozu](../remote-actions/device-management.md).

## <a name="next-steps"></a>Další kroky

- Přečtěte si další informace o [správě aplikací v Microsoft Intune](app-management.md).