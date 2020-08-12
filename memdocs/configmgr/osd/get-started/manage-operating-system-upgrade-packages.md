---
title: Správa balíčků s upgradem operačního systému
titleSuffix: Configuration Manager
description: Naučte se spravovat balíčky s upgradem operačního systému v Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a50592815ed4581c01489f90b6c3701e53bb4981
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124410"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Správa balíčků s upgradem operačního systému pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Balíček s upgradem operačního systému v Configuration Manager obsahuje zdrojové soubory instalace systému Windows k upgradu stávajícího operačního systému v počítači. Tento článek popisuje, jak přidat, distribuovat a obsluhovat balíček s upgradem operačního systému.

> [!NOTE]
> Balíčky s upgradem operačního systému se dají použít i pro nové instalace systému Windows. Je však závislý na ovladačích, které jsou kompatibilní s touto metodou. Při provádění nových instalací systému Windows z balíčku s upgradem operačního systému jsou ovladače nainstalovány i v systému Windows PE, a to pouhým vložením v prostředí Windows PE. Některé ovladače nejsou kompatibilní s instalací v prostředí Windows PE. Pokud nejsou ovladače kompatibilní s instalací v prostředí Windows PE, použijte místo toho [bitovou kopii operačního systému](manage-operating-system-images.md), jako je například **install. wim**.

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a>Přidat balíček s upgradem operačního systému  

Než budete moct použít balíček s upgradem operačního systému, přidejte ho nejdřív do Configuration Manager lokality.

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **balíčky s upgradem operačního systému** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **Přidat balíček s upgradem operačního systému**. Tato akce spustí Průvodce přidáním upgradu operačního systému.  

3. Na stránce **zdroj dat** zadejte následující nastavení:

    - Síťová **cesta** k instalačním zdrojovým souborům balíčku s UPGRADEM operačního systému. Například, `\\server\share\path`.  

        > [!NOTE]  
        >  Zdrojové instalační soubory obsahují setup.exe a další soubory a složky pro instalaci operačního systému.  

        > [!IMPORTANT]  
        >  Omezte přístup k těmto zdrojovým souborům instalace, abyste zabránili nežádoucí manipulaci.  

    - **Rozbalte konkrétní index bitové kopie ze souboru Install. wim vybraného balíčku s upgradem** a potom v seznamu vyberte index bitové kopie.<!--4931110--> Počínaje verzí 1910 Tato možnost automaticky importuje jeden index a nikoli všechny indexy obrázků v souboru. Použití této možnosti má za následek menší soubor obrázku a rychlejší online údržbu. Také podporuje proces [optimalizace údržby imagí](#bkmk_resetbase)pro menší soubor bitové kopie po použití aktualizací softwaru.  

        > [!IMPORTANT]  
        > Configuration Manager přepíše existující soubor Install. wim v balíčku s upgradem operačního systému. Extrahuje index bitové kopie do dočasného umístění a poté je přesune do původního zdrojového adresáře. Před importem balíčku s upgradem operačního systému a povolením této možnosti nezapomeňte zálohovat původní zdrojové soubory.

    - Pokud chcete obsah předběžně ukládat do mezipaměti klienta, zadejte **architekturu** a **jazyk** obrázku. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).  

4. Na stránce **Obecné** zadejte následující informace. Tyto informace jsou užitečné pro účely identifikace, pokud máte více než jeden balíček s upgradem operačního systému.  

    - **Název**: jedinečný název balíčku upgradu operačního systému.  

    - **Verze**: volitelný identifikátor verze. Tato vlastnost nemusí být verzí operačního systému balíčku pro upgrade. Pro balíček je často verze vaší organizace.  

    - **Komentář**: volitelný stručný popis.  

5. Dokončete průvodce.  

Dále distribuujte balíček s upgradem operačního systému do distribučních bodů.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a>Distribuce obsahu do distribučního bodu  

Distribuujte balíčky s upgradem operačního systému do distribučních bodů stejně jako jiný obsah. Před nasazením pořadí úkolů distribuujte balíček s upgradem operačního systému do alespoň jednoho distribučního bodu. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Další kroky

[Vytvoření pořadí úkolů pro upgrade operačního systému](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
