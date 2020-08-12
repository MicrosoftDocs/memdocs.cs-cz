---
title: Správa imagí operačního systému
titleSuffix: Configuration Manager
description: Seznamte se s metodami správy imagí operačního systému uložených v souborech WIM (Windows Image).
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa574cd3db2e7a3d3277912ed4a383f71d33e59c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124283"
---
# <a name="manage-os-images-with-configuration-manager"></a>Správa imagí operačního systému pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Bitové kopie operačního systému v Configuration Manager jsou uloženy ve formátu souboru WIM (Windows Image). Tyto image jsou komprimovanou kolekcí referenčních souborů a složek, které slouží k instalaci a konfiguraci nového operačního systému v počítači. Mnoho scénářů nasazení operačního systému vyžaduje bitovou kopii operačního systému.


## <a name="os-image-types"></a>Typy bitových kopií operačního systému

Můžete použít [výchozí image operačního systému](#default-image)nebo sestavit image operačního systému z [referenčního počítače](#bkmk_capture) , který nakonfigurujete. Při sestavování referenčního počítače můžete do operačního systému přidat soubory operačního systému, ovladače, podpůrné soubory, aktualizace softwaru, nástroje a aplikace. Potom ho zachytíte pro vytvoření souboru bitové kopie.

### <a name="default-image"></a>Výchozí image

Instalační soubory systému Windows obsahují výchozí bitovou kopii operačního systému. Tato Image je základní image operačního systému, která obsahuje standardní sadu ovladačů. Když použijete výchozí image operačního systému, pomocí kroků pořadí úkolů nainstalujete aplikace a po instalaci operačního systému do zařízení můžete provést další konfigurace. Vyhledejte výchozí bitovou kopii operačního systému ve zdrojových souborech systému Windows: `\Sources\install.wim` .  

#### <a name="default-image-advantages"></a>Výchozí výhody imagí

- Velikost image je menší než u zaznamenané image.  

- Instalace aplikací a konfigurací pomocí kroků pořadí úkolů je dynamičtější. Můžete například změnit konfigurace a aplikace, které jsou v pořadí úkolů nainstalovány, bez nutnosti obnovení bitové kopie zařízení.  

#### <a name="default-image-disadvantages"></a>Výchozí nevýhody imagí

- Instalace operačního systému může trvat delší dobu. Instalace aplikace a další konfigurace se projeví po dokončení instalace operačního systému.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a>Zachycená bitová kopie z referenčního počítače

Pokud chcete vytvořit vlastní image operačního systému, Sestavte referenční počítač s požadovaným operačním systémem. Pak nainstalujte aplikace a nakonfigurujte nastavení. Zaznamenejte image operačního systému z referenčního počítače a vytvořte soubor WIM. Manuálně Sestavte referenční počítač nebo použijte pořadí úkolů pro automatizaci některých nebo všech kroků sestavení. Další informace najdete v tématu [přizpůsobení imagí operačního systému](customize-operating-system-images.md).  

#### <a name="captured-image-advantages"></a>Výhody zachycených imagí

- Instalace může být rychlejší než při použití výchozí image. Například aplikace lze předinstalovat pomocí zachycené image operačního systému. Pak tyto aplikace nemusíte instalovat později pomocí kroků pořadí úkolů.  

#### <a name="captured-image-disadvantages"></a>Nevýhody zaznamenané bitové kopie

- Velikost obrázku může být větší než výchozí obrázek.  

- Když budete potřebovat aktualizace pro aplikace a nástroje, je potřeba vytvořit novou bitovou kopii.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a>Přidání image operačního systému  

Než budete moci použít bitovou kopii operačního systému, přidejte ji do Configuration Manager lokality.

1. V konzole Configuration Manager klikněte na pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a pak vyberte uzel **bitové kopie operačního systému** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **Přidat bitovou kopii operačního systému**. Tato akce spustí Průvodce přidáním bitové kopie operačního systému.  

3. Na stránce **zdroj dat** zadejte následující informace:

    - Síťová **cesta** k souboru bitové kopie operačního systému. Například, `\\server\share\path\image.wim`.

    - **Extrahujte konkrétní index bitové kopie ze zadaného souboru WIM** a pak ze seznamu vyberte index bitové kopie.<!--3719699--> Počínaje verzí 1902 Tato možnost automaticky importuje jeden index a nikoli všechny indexy obrázků v souboru. Použití této možnosti má za následek menší soubor obrázku a rychlejší online údržbu. Také podporuje proces [optimalizace údržby imagí](#bkmk_resetbase)pro menší soubor bitové kopie po použití aktualizací softwaru.  

        > [!Note]  
        > Configuration Manager neupraví zdrojový soubor bitové kopie. Vytvoří nový soubor obrázku ve stejném zdrojovém adresáři.
        >
        > Tento proces extrakce může u extrémně velkých souborů obrázků selhat, například přes 60 GB. Chyba nástroje DISM je `Not enough storage is available to process this command.` příkazový řádek, který Configuration Manager používá, v protokolu Smsprov. log a DISM. log. Spusťte ručně stejný příkaz a pak naimportujte bitovou kopii.<!-- SCCMDocs-pr issue 3502 -->  

    - Pokud chcete v klientovi předem ukládat obsah do mezipaměti, začněte ve verzi 1906 a určete **architekturu** a **jazyk** obrázku. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. Na stránce **Obecné** zadejte následující informace. Tyto informace jsou užitečné pro účely identifikace, pokud máte více než jednu Image operačního systému.  

    - **Název**: jedinečný název obrázku. Ve výchozím nastavení název pochází z názvu souboru WIM.  

    - **Verze**: volitelný identifikátor verze. Tato vlastnost nemusí být verzí operačního systému image. Pro balíček je často verze vaší organizace.  

    - **Komentář**: volitelný stručný popis.  

5. Dokončete průvodce.  

Ekvivalent rutiny prostředí PowerShell pro tento Průvodce konzolou najdete v části [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Dále distribuujte bitovou kopii operačního systému do distribučních bodů.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a>Distribuce obsahu do distribučních bodů  

Distribuci imagí operačního systému do distribučních bodů, které jsou stejné jako u jiného obsahu. Před nasazením pořadí úkolů distribuujte image operačního systému do aspoň jednoho distribučního bodu. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a>Příprava image operačního systému pro nasazení vícesměrového vysílání  

Nasazení pomocí vícesměrového vysílání umožňuje, aby více než jeden počítač mohl současně stahovat bitovou kopii operačního systému. Bitová kopie je vícesměrového vysílání klientům prostřednictvím distribučního bodu, nikoli každému klientovi, který stahuje kopii image z distribučního bodu přes samostatné připojení. Když zvolíte metodu nasazení operačního systému pro [použití vícesměrového vysílání k nasazení Windows přes síť](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), nakonfigurujte image operačního systému tak, aby podporovala vícesměrové vysílání. Pak distribuujte bitovou kopii do distribučního bodu s povoleným vícesměrovým vysíláním.

1. V konzole Configuration Manager klikněte na pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a pak vyberte uzel **bitové kopie operačního systému** .  

2. Vyberte bitovou kopii operačního systému, kterou chcete distribuovat do distribučního bodu s povoleným vícesměrovým vysíláním.  

3. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.  

4. Přepněte na kartu **Nastavení distribuce** a nakonfigurujte následující možnosti:  

    - **Povolí přenos tohoto balíčku prostřednictvím vícesměrového vysílání (pouze WinPE)**: tuto možnost vyberte, pokud chcete Configuration Manager souběžně nasadit image operačního systému pomocí vícesměrového vysílání.  

    - **Šifrovat balíčky vícesměrového vysílání**: Určete, jestli lokalita zašifruje image, než se pošle do distribučního bodu. Pokud obrázek obsahuje citlivé informace, použijte tuto možnost. Pokud obrázek není zašifrovaný, jeho obsah se v síti zobrazí jako nešifrovaný text. Pak by neoprávněný uživatel mohl zachytit a zobrazit obsah obrázku.  

    - **Přenášet tento balíček pouze vícesměrovým vysíláním**: Určete, jestli má distribuční bod nasazovat image jenom během relace vícesměrového vysílání.  

         Pokud vyberete možnost **přenést tento balíček pouze pomocí vícesměrového vysílání**, je třeba zadat také možnost nasazení pořadí úloh pro **Stažení obsahu místně, pokud to vyžaduje běžící pořadí úloh**. Další informace naleznete v části [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md).  

5. Výběrem **OK** uložte nastavení a zavřete vlastnosti obrázku.  
