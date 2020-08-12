---
title: Vytvoření vlastního pořadí úkolů
titleSuffix: Configuration Manager
description: Úpravou vlastního pořadí úkolů v Configuration Manager přidejte do pořadí úkolů kroky.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f390c3857ad5a277002839c4c14ab1307d9ab281
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125572"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Vytvoření vlastního pořadí úloh pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když vytvoříte vlastní pořadí úloh v Configuration Manager, nezahrnuje žádné kroky pořadí úkolů. Po vytvoření pořadí úloh ho upravte a přidejte potřebné kroky pořadí úkolů.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a>Vytvoření vlastního pořadí úloh

K vytvoření vlastního pořadí úkolů použijte následující postup:

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pořadí úloh**. Tato akce spustí Průvodce vytvořením pořadí úloh.  

1. Na stránce **Vytvoření nového pořadí úloh** vyberte možnost **Vytvořit nové vlastní pořadí úloh**.  

1. Na stránce **informace o pořadí úloh** zadejte:

    - Název pořadí úloh
    - Popis pořadí úkolů
    - Volitelná spouštěcí image pro pořadí úkolů, které se má použít

Po dokončení Průvodce vytvořením pořadí úloh Configuration Manager přidá vlastní pořadí úloh do uzlu **pořadí úloh** . Nyní je možné toto pořadí úloh upravit a přidat do něj kroky pořadí úloh.  

## <a name="see-also"></a>Viz také

Seznam dostupných kroků pořadí úkolů najdete v tématu [kroky pořadí úkolů](../understand/task-sequence-steps.md).  

Další informace o úpravách pořadí úkolů najdete v tématu [použití editoru pořadí úloh](../understand/task-sequence-editor.md).  

Nejčastěji budete používat pořadí úkolů k automatizaci úloh pro nasazení operačního systému, ale můžete vytvořit vlastní pořadí úkolů pro automatizaci různých druhů úkolů. Další informace najdete v tématu [Vytvoření pořadí úkolů pro nasazení bez OS](create-a-task-sequence-for-non-operating-system-deployments.md).

Počínaje verzí 2002 nainstalujte komplexní aplikace pomocí pořadí úkolů prostřednictvím aplikačního modelu. Přidejte typ nasazení do aplikace, která je pořadím úkolů, a to buď k instalaci nebo odinstalaci aplikace. Další informace najdete v tématu [vytváření aplikací pro Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Další kroky

[Nasazení pořadí úloh](deploy-a-task-sequence.md)
