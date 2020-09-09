---
title: CMPivot využití připojené k tenantovi
titleSuffix: Configuration Manager
description: Přehled využití CMPivot pro zařízení připojená ke klientovi Microsoft Endpoint Manager.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8967957883a1c8d397377c30409cb94139014214
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564069"
---
# <a name="tenant-attach-cmpivot-preview-usage-overview"></a>Připojení tenanta: Přehled využití CMPivot (Preview)

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

CMPivot vám umožňuje rychle vyhodnotit stav zařízení ve vašem prostředí a provést akci. Když zadáte dotaz, CMPivot spustí dotaz v reálném čase v aktuálně připojeném zařízení. Vrácená data je pak možné filtrovat, seskupovat a zdokonalovat, aby odpovídala obchodním otázkám, řešení problémů ve vašem prostředí nebo reagovat na bezpečnostní hrozby. Další informace o použití CMPivot najdete v tématu [použití CMPivot](../core/servers/manage/cmpivot.md).

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a> Upřesnění dotazů CMPivot

Pokud používáte CMPivot z konzoly pro správu Microsoft Endpoint Manageru, ujistěte se, že jsou dotazy optimalizované pro výkon. Pokud si vyžádáte dotaz s datovou sadou, která je příliš velká, může se zobrazit `Error: The query result is too large, retry with additional filters` . Pokud se zobrazí tato chyba, upřesněte dotaz tak, aby byl konkrétnější. K upřesnění dotazů se běžně používají následující operátory:

- Použijte, `count` Pokud potřebujete jenom počet vrácených položek.
- Použijte `project` , pokud potřebujete pouze konkrétní sloupce.
- Slouží `take` k návratu až k zadanému počtu řádků.
- Slouží `top` k vrácení prvních N záznamů seřazených podle zadaných sloupců.

> [!Important]
> Při použití CMPivot k dotazování na zařízení, pokud odpověď není během 10 minut, bude časový limit dotazu. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]


## <a name="next-steps"></a>Další kroky

Další informace najdete v tématu [spuštění CMPivot (Preview) v centru pro správu](cmpivot-start.md) . Další ukázkové skripty najdete v článku [připojení tenanta Microsoft Endpoint Manageru: Ukázky skriptů CMPivot](cmpivot-samples-attached.md).
