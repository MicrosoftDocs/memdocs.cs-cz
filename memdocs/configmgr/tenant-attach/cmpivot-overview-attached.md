---
title: CMPivot – přehled připojených klientů
titleSuffix: Configuration Manager
description: CMPivot přehled pro zařízení připojená ke klientovi Microsoft Endpoint Manager.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 93460b08b7ba47951656e1107aae56e687acf4e8
ms.sourcegitcommit: f6b14e6fe694a2a05c6ed92e67089e80a00a0908
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/17/2020
ms.locfileid: "88501194"
---
# <a name="tenant-attach-cmpivot-overview"></a>Připojení tenanta: Přehled CMPivot

*Platí pro: Configuration Manager (větev Technical Preview)*

> [!Important]
> Tento článek se týká větve Technical Preview pro Configuration Manager. Další informace najdete v tématu [Configuration Manager Technical Preview verze 2005](../core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot).

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

## <a name="known-issues"></a>Známé problémy

### <a name="inconsistent-results-for-some-operators-with-configuration-manager-version-2002"></a>Nekonzistentní výsledky pro některé operátory s Configuration Manager verze 2002
<!--7784718, 7884272-->
Pokud používáte CMPivot z centra pro správu Microsoft Endpoint Manageru s Configuration Manager verze 2002, můžete získat nekonzistentní výsledky pro následující operátory:

- Vytvořit souhrn podle
- Take
- Řadit podle
- Nahoře
- Count
- Distinct

## <a name="next-steps"></a>Další kroky

Další ukázkové skripty najdete v článku [připojení tenanta Microsoft Endpoint Manageru: Ukázky skriptů CMPivot](cmpivot-samples-attached.md).
