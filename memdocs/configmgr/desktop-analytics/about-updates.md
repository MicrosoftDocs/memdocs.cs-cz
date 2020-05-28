---
title: Aktualizace v Desktop Analytics
titleSuffix: Configuration Manager
description: Seznamte se s aktualizacemi zabezpečení a funkcí v Desktop Analytics.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 1c79db413f8e37424b84d98d51fb584d168e3819
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268925"
---
# <a name="updates-in-desktop-analytics"></a>Aktualizace v Desktop Analytics

Na portálu Desktop Analytics si prohlédněte stav aktualizací zabezpečení a funkcí. Vyberte tyto uzly ve skupině monitorování v hlavní nabídce nástroje Desktop Analytics. Tyto uzly vám poskytnou přehled o stavu těchto aktualizací ve vašem prostředí.


## <a name="security-updates"></a>Aktualizace zabezpečení

Chcete-li zkontrolovat aktuální stav aktualizací zabezpečení, vyberte možnost **aktualizace zabezpečení** v části **monitorování** v Desktop Analytics:

![Uzel aktualizace zabezpečení pro Desktop Analytics](media/security-updates.png)

Toto zobrazení shrnuje aktualizace *zabezpečení* pro zařízení s Windows 10. Zařízení v pruhovém grafu jsou rozdělená podle následujících popisků:

#### <a name="latest"></a>Latest (Nejnovější)

Na zařízeních je spuštěná nejnovější aktualizace zabezpečení pro tuto verzi a kanál.

#### <a name="latest-1"></a>Nejnovější – 1

Na zařízeních je spuštěná aktualizace zabezpečení jedna verze, která je starší než nejnovější dostupná aktualizace tohoto kanálu.

#### <a name="older"></a>Starší

Na zařízeních je spuštěná aktualizace zabezpečení starší než nejnovější verze-1.

#### <a name="not-measured"></a>Neměřené

Desktop Analytics nehodnotil zařízení. Tento stav zahrnuje zařízení se systémem Windows 7, Windows 8.1 nebo zařízení s Windows 10 zaregistrovanými pro program Windows Insider.  

Pokud chcete zobrazit trendy přijetí aktualizací zabezpečení, vyberte **Zobrazit další** pro konkrétní verzi Windows. Skládaný plošný graf rozděluje zařízení podle aktualizace zabezpečení, kterou nainstalují v průběhu času.

Pokud chcete zkontrolovat stav nasazení pro aktualizace zabezpečení, vyberte **Zobrazit vše**. V tomto zobrazení jsou uvedena zařízení v následujících kategoriích:

- Nezahájeno
- Rozpracované
- Dokončeno
- Potřebuje pozornost – zařízení (seřazené podle názvu zařízení)
- Vyžaduje problémy s pozorností (seřazené podle typu vydání)

Pokud chcete zobrazit zařízení s novými informacemi, které služba stále zpracovává, vyberte **Zobrazit poslední data**. Po příštím úplném obnovení dat se na Desktop Analytics zobrazí tyto informace.

  > [!IMPORTANT]
  > Možnost Analytics pro stolní počítače, která **zobrazuje poslední data** , je zastaralá. Tato akce bude odebrána v budoucí verzi služby Desktop Analytics. Další informace najdete v tématu [zastaralé funkce](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="feature-updates"></a>Aktualizace funkcí

Chcete-li zkontrolovat aktuální stav aktualizací funkcí, vyberte možnost **aktualizace funkcí** v části **monitorování** v Desktop Analytics:

![Uzel aktualizace funkcí v Desktop Analytics](media/feature-updates.png)

Toto zobrazení shrnuje aktualizace *funkcí* pro zařízení s Windows 10.

Další informace o obdobích služby najdete v tématu [Přehled životního cyklu Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Zařízení v pruhovém grafu jsou rozdělená podle následujících popisků:

#### <a name="in-service"></a>V provozu

Na zařízeních je spuštěná nejnovější aktualizace funkcí pro danou verzi a kanál.  

#### <a name="near-end-of-service"></a>Poblíž konce služby

Na zařízeních je spuštěná aktualizace funkcí, která je během 90 dnů od dosažení konce služby.

#### <a name="end-of-service"></a>Konec služby

Na zařízeních je spuštěná aktualizace funkcí, která je po datu ukončení služby. Tato data jsou specifická pro edice Windows Enterprise a školství. Nevztahují se na edice Home, pro, pro školství nebo pro pro pracovní stanice. Další informace najdete v tématu [seznam faktů pro životní cyklus systému Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>Neměřené

Desktop Analytics nehodnotil zařízení. Tento stav zahrnuje zařízení se systémem Windows 7, Windows 8.1 nebo zařízení s Windows 10 zaregistrovanými pro program Windows Insider.

Výběrem dlaždice zobrazíte trendy přijímání aktualizací funkcí. Skládaný plošný graf rozděluje zařízení podle aktualizace funkcí, kterou nainstalují v průběhu času.

## <a name="next-steps"></a>Další kroky

- [Další informace o prostředcích Desktop Analytics](about-assets.md): zařízení, ovladače a aplikace  

- [Další informace o plánech nasazení](about-deployment-plans.md)  
