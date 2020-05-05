---
title: Úrovně diagnostických dat o využití
titleSuffix: Configuration Manager
description: Seznamte se s úrovněmi diagnostiky a dat o využití, která Configuration Manager shromažďuje.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720335"
---
# <a name="levels-of-diagnostic-usage-data"></a>Úrovně diagnostických dat o využití

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager shromažďuje tři úrovně diagnostiky a dat o využití: **základní**, **Rozšířená**a **plná**. Ve výchozím nastavení má tato funkce nastavenou úroveň Rozšířená.

> [!IMPORTANT]
> Configuration Manager neshromažďuje kódy lokalit, názvy lokalit, IP adresy, uživatelská jména, názvy počítačů, fyzické adresy ani e-mailové adresy na úrovních Basic a Enhanced. Žádná kolekce těchto informací na úrovni Úplná není záměrné. Je potenciálně součástí pokročilých diagnostických informací, jako jsou soubory protokolu nebo snímky paměti. Společnost Microsoft tyto informace nepoužívá k tomu, aby vás identifikovala, kontaktovala vás nebo vyvinula reklamu.

## <a name="levels"></a>Úrovně

### <a name="basic"></a>Základní

Základní úroveň zahrnuje data o vaší hierarchii. Je potřeba, abyste vylepšili možnosti instalace nebo upgradu. Tato data také pomáhají určit Configuration Manager aktualizací, které se vztahují k vaší hierarchii.

### <a name="enhanced"></a>Rozšířené

Rozšířená úroveň je výchozí po dokončení instalace. Tato úroveň zahrnuje data shromážděná na úrovni Basic a v datech specifických pro jednotlivé funkce. Zobrazuje četnost a dobu používání různých funkcí. Zahrnuje taky Configuration Manager data nastavení klienta: název komponenty, stav a určitá nastavení jako intervaly cyklického dotazování. Informace o aktualizacích softwaru jsou základní při použití funkcí a nezahrnují data o dodržování předpisů aktualizací na této úrovni.

Společnost Microsoft tuto úroveň doporučuje, protože poskytuje minimální data pro zajištění vylepšení produktů a služeb.

Mezi příklady dat, která tato úroveň neshromažďuje, patří:

- Názvy webů, uživatelů, počítačů nebo jiných objektů

- Podrobnosti o objektech souvisejících se zabezpečením

- Ohrožení zabezpečení jako počty systémů, které vyžadují aktualizace softwaru

### <a name="full"></a>Do bloku

Úplná úroveň zahrnuje všechna data na úrovni Basic a Enhanced. Obsahuje také další informace o řešení funkci Endpoint Protection, procenta dodržování předpisů pro aktualizace a informace o aktualizacích softwaru. Tato úroveň může zahrnovat taky rozšířené diagnostické informace, jako jsou systémové soubory a snímky paměti. Tato pokročilá data můžou zahrnovat osobní údaje v paměti nebo souborech protokolu v době zachycení.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Postup pro změnu úrovně

Chcete-li změnit úroveň shromažďování dat, potřebujete oprávnění **změnit** u třídy objektů **lokalita** .

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .
1. Na pásu karet vyberte **Nastavení hierarchie** .
1. Přepněte na kartu **Diagnostika a data o využití** a pak zvolte úroveň dat.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a>Podrobnosti specifické pro verzi

Následující články podrobně popisují konkrétní data, která Configuration Manager shromažďuje na jednotlivých úrovních s každou podporovanou verzí:

- [Diagnostická data a data o využití pro 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Diagnostická data a data o využití pro 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Diagnostická data a data o využití pro 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Diagnostická data a data o využití pro 1902](levels-of-diagnostic-usage-data-collection-1902.md)
- [Diagnostická data a data o využití pro 1810](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Nejčastější dotazy](frequently-asked-questions.md)
