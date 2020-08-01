---
title: CMPivot – přehled připojených klientů
titleSuffix: Configuration Manager
description: CMPivot přehled pro zařízení připojená ke klientovi Microsoft Endpoint Manager.
ms.date: 07/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07bb8cd913c945198d181e6191c540eeb8b2dffc
ms.sourcegitcommit: 5a58af4f7d40bbde88a273fba859bf69eeff6107
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473664"
---
# <a name="tenant-attach-cmpivot-overview"></a>Připojení tenanta: Přehled CMPivot

*Platí pro: Configuration Manager (větev Technical Preview)*

> [!Important]
> Tento článek se týká větve Technical Preview pro Configuration Manager. Další informace najdete v tématu [Configuration Manager Technical Preview verze 2005](../core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot).

CMPivot vám umožňuje rychle vyhodnotit stav zařízení ve vašem prostředí a provést akci. Když zadáte dotaz, CMPivot spustí dotaz v reálném čase v aktuálně připojeném zařízení. Vrácená data je pak možné filtrovat, seskupovat a zdokonalovat, aby odpovídala obchodním otázkám, řešení problémů ve vašem prostředí nebo reagovat na bezpečnostní hrozby. Další informace o použití CMPivot najdete v tématu [použití CMPivot](../core/servers/manage/cmpivot.md).

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a>Upřesnění dotazů CMPivot

Pokud používáte CMPivot z konzoly pro správu Microsoft Endpoint Manageru, ujistěte se, že jsou dotazy optimalizované pro výkon. Pokud si vyžádáte dotaz s datovou sadou, která je příliš velká, může se zobrazit `Error: The query result is too large, retry with additional filters` . Pokud se zobrazí tato chyba, upřesněte dotaz tak, aby byl konkrétnější. K upřesnění dotazů se běžně používají následující operátory:

- Použijte, `count` Pokud potřebujete jenom počet vrácených položek.
- Použijte `project` , pokud potřebujete pouze konkrétní sloupce.
- Slouží `take` k návratu až k zadanému počtu řádků.
- Slouží `top` k vrácení prvních N záznamů seřazených podle zadaných sloupců.

> [!Important]
> Při použití CMPivot k dotazování na zařízení, pokud odpověď není během 10 minut, bude časový limit dotazu. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]

## <a name="next-steps"></a>Další kroky

Další ukázkové skripty najdete v článku [připojení tenanta Microsoft Endpoint Manageru: Ukázky skriptů CMPivot](cmpivot-samples-attached.md).
