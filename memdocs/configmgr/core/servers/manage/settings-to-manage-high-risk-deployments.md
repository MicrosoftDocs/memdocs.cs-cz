---
title: Správa nasazení s vysokým rizikem
titleSuffix: Configuration Manager
description: Nakonfigurujte nastavení lokality ověřování nasazení v Configuration Manager tak, aby byli správci upozorněni na to, že vytvoří nasazení s vysokým rizikem.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719985"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Nastavení pro správu nasazení s vysokým rizikem pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager můžete nakonfigurovat nastavení lokality *ověřování nasazení* . Tato nastavení upozorňují správce na to, že vytvoří nasazení pořadí úkolů s vysokým rizikem. Nasazení s vysokou rizikovostí je:  

- Nasazení, které je automaticky nainstalováno  

- Nasazení, které má potenciál způsobovat nežádoucí výsledky  

Například pořadí úkolů s účelem **požadováno** , které nasazuje operační systém, je považováno za vysoce rizikové.  

> [!WARNING]
> Pokud používáte nasazení PXE a nakonfigurujete hardware zařízení se síťovým adaptérem jako prvním spouštěcím zařízením, můžou tato zařízení automaticky spustit pořadí úloh nasazení operačního systému bez zásahu uživatele. Ověřování nasazení nespravuje tuto konfiguraci. I když tato konfigurace může zjednodušit proces a omezit interakci s uživatelem, umístí zařízení s větším rizikem na nechtěné obnovení obrazu.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a>Nastavení ověřování nasazení

Abyste snížili riziko nežádoucího nasazení s vysokým rizikem, můžete nakonfigurovat omezení velikosti v těchto nastaveních ověřování nasazení:  

- **Omezení velikosti kolekce**: Když vytvoříte nasazení, skryjte kolekce, které obsahují víc klientů, než je limit.  

  - **Výchozí velikost**: Když vytvoříte nasazení, skryje toto nastavení kolekce ve výchozím nastavení, které zahrnují víc klientů, než je toto omezení. Tyto kolekce se pořád zobrazují při vytváření nasazení, ale ve výchozím nastavení jsou skryté. Výchozí hodnota je **100**. Pokud chcete toto nastavení ignorovat, zadejte hodnotu **0**.  

  - **Maximální velikost**: Když vytvoříte nasazení, toto nastavení vždy skryje kolekce s víc klienty, než je toto omezení. Výchozí hodnota je **0**, která toto nastavení ignoruje. Hodnota **Maximální velikost** musí být větší než hodnota **Výchozí velikost** .  

    Například nastavíte **výchozí velikost** na 100 a **maximální velikost** na 1000. Když vytvoříte vysoce rizikové nasazení, okno **Vybrat kolekci** zobrazí jenom kolekce, které zahrnují méně než 100 klientů. Pokud zrušíte nastavení pro **skrytí kolekcí s počtem členů větším, než je konfigurace minimální velikosti webu**, zobrazí se v okně kolekce, které zahrnují méně než 1000 klientů.  

- **Kolekce se servery systému lokality**: Pokud cílová kolekce obsahuje počítač s rolí systému lokality, zablokujte nasazení nebo vyžadovat ověření před vytvořením nasazení. Pokud je nasazení blokované, vyberte jinou kolekci, která splňuje kritéria pro ověření nasazení, aby bylo možné pokračovat v vytváření nasazení.  

> [!NOTE]
> Vysoce riziková nasazení se vždy omezují na vlastní kolekce, kolekce, které vytvoříte, a na vestavěnou kolekci **Neznámé počítače**. Když vytvoříte vysoce rizikové nasazení, nemůžete vybrat vestavěnou kolekci, například **všechny systémy**.  

## <a name="configure-deployment-verification"></a>Konfigurovat ověřování nasazení

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**, vyberte možnost **lokality**a pak vyberte primární lokalitu, kterou chcete nakonfigurovat.

2. Na pásu karet vyberte **vlastnosti**a pak přepněte na kartu **Ověření nasazení** .

3. Nakonfigurujte [Nastavení](#bkmk_settings) , která chcete použít, a potom výběrem **OK** uložte konfiguraci a zavřete vlastnosti.

## <a name="next-steps"></a>Další kroky

[Správa pořadí úkolů – nastavení vysokého dopadu](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Konfigurace lokalit a hierarchií](../deploy/configure/configure-sites-and-hierarchies.md)
