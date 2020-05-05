---
title: Průvodce migrací správy mobilních zařízení do Intune
titleSuffix: Microsoft Intune
description: Tato příručka vás seznámí s různými detaily migrace od jiného poskytovatele MDM do Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dcfc21f9-1bcd-4371-a46d-f2e18154ec50
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b09240c2bd1d562985ce69c35f07181dc5c9489
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079905"
---
# <a name="intune-migration-guide"></a>Příručka k migraci do Intune

![Příručka k migraci MDM do Microsoft Intune – schéma](./media/migration-guide/MDM-migration-guide-art.PNG)

Úspěšná migrace do Microsoft Intune začíná vypracováním promyšleného plánu, který bere v úvahu nejen vaše aktuální prostředí pro správu mobilních zařízení (MDM), ale i obchodní cíle a technické požadavky. Kromě toho je potřeba zahrnout klíčové účastníky, kteří vám pomůžou plán migrace zrealizovat.

Tato příručka vás seznámí s různými detaily migrace od jiného poskytovatele MDM do Intune.

## <a name="whats-included-in-this-guide"></a>Co je součástí tohoto průvodce?

Tato příručka rozděluje migraci na dvě fáze zahrnující úkoly, strategie a taktické pokyny, které vám pomůžou projít celým procesem migrace do Intune MDM.

- [Fáze 1: Příprava Intune na správu mobilních zařízení](migration-guide-prepare.md)

  - [Vyhodnocení požadavků na migraci MDM](migration-guide-prepare.md#assess-mdm-requirements)

  - [Základní nastavení](migration-guide-setup.md)

  - [Konfigurace zásad pro správu zařízení a aplikací](migration-guide-configure-policies.md)

  - [Konfigurace zásad pro ochranu aplikací](../apps/app-protection-policies.md)

  - [Zvláštní stránky migrace](migration-guide-considerations.md)

- [Fáze 2: Kampaň migrace](migration-guide-campaign.md)

  - [Plán komunikace](migration-guide-communication-plan.md)

  - [Podpora přijetí koncovými uživateli pomocí podmíněného přístupu](migration-guide-drive-adoption.md)

  - [Typický cyklus migrace](migration-guide-cycle.md)
    - [Monitorování migrace](migration-guide-cycle.md#monitoring-migration)
    - [Po dokončení migrace](migration-guide-cycle.md#post-migration)

## <a name="assumptions"></a>Předpoklady

- Službu Intune jste už vyhodnotili v prostředí testování konceptu a rozhodli jste se použít ji jako řešení MDM ve vaší organizaci.

- Intune a její funkce už znáte.

## <a name="before-you-begin"></a>Před zahájením

Je důležité uvědomit si, že nové nasazení Intune se může lišit od předchozího nasazení MDM. Na rozdíl od tradičních služeb MDM používá Intune řízení přístupu na základě identity, takže řízení přístupu k firemním datům z mobilních zařízení nacházejících se mimo síť organizace nevyžaduje síťová proxy zařízení. Microsoft nabízí řešení pro zabezpečení dat přímo v cloudu prostřednictvím úzce integrovaných cloudových služeb, které se souhrnně označují jako Enterprise Client + Security.

- Projděte si [běžné způsoby použití Intune](common-scenarios.md).

## <a name="next-steps"></a>Další kroky

[Fáze 1: Příprava Intune na správu mobilních zařízení](migration-guide-prepare.md)
