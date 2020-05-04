---
title: Vytvoření záznamového média
titleSuffix: Configuration Manager
description: K zachycení image operačního systému z referenčního počítače použijte záznamová média v Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbbec355356a74d61f263fe2b16d44c0cd15ba80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711144"
---
# <a name="create-capture-media"></a>Vytvoření záznamového média

*Platí pro: Configuration Manager (Current Branch)*

Záznamová média v Configuration Manager umožňují zaznamenat image operačního systému z referenčního počítače. Záznamové médium obsahuje spouštěcí bitovou kopii, která spouští referenční počítač, a pořadí úkolů, které zachytí image operačního systému. Pomocí záznamového média pro scénář [Vytvořte pořadí úkolů pro zachycení operačního systému](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Požadavky

Než vytvoříte záznamové médium pomocí Průvodce vytvořením média pořadí úloh, ujistěte se, že jsou splněné všechny tyto podmínky.

### <a name="boot-image"></a>Spouštěcí image

Vezměte v úvahu následující body spouštěcí bitové kopie, které v pořadí úkolů použijete k nasazení operačního systému:

- Architektura spouštěcí bitové kopie musí být vhodná pro architekturu cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Ale cílový počítač x86 může bootovat a spustit pouze bootovací obrázek x86.
- Ujistěte se, že spouštěcí bitová kopie obsahuje síťové ovladače a ovladače úložiště, které jsou nutné k zřízení cílového počítače.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuce veškerého obsahu souvisejícího s pořadím úkolů

Distribuujte veškerý obsah, který pořadí úkolů vyžaduje alespoň v jednom distribučním bodě. Tento obsah obsahuje spouštěcí bitovou kopii, bitovou kopii operačního systému a další související soubory. Průvodce shromáždí obsah z distribučního bodu, když vytváří záznamová média.

Váš uživatelský účet potřebuje alespoň přístupová práva ke **čtení** knihovny obsahu v tomto distribučním bodě. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Příprava vyměnitelné jednotky USB

Pokud používáte vyměnitelnou jednotku USB, připojte ji k počítači, na kterém spouštíte Průvodce vytvořením média pořadí úloh. Jednotka USB musí být zjistitelná systémem Windows jako zařízení pro odebrání. Průvodce při vytváření média provádí zápis přímo na jednotku USB.

### <a name="create-an-output-folder"></a>Vytvoření výstupní složky

Před spuštěním Průvodce vytvořením média pořadí úloh pro vytvoření média pro sadu CD nebo DVD vytvořte složku pro výstupní soubory, které vytvoří. Médium, které vytvoří pro sadu disků CD nebo DVD, je zapsáno jako. Soubor ISO přímo ve složce.


## <a name="process"></a>Proces

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit médium pořadí úloh**. Tato akce spustí Průvodce vytvořením média pořadí úloh.  

3. Na stránce **Vybrat typ média** vyberte možnost **zaznamenat médium**.  

4. Na stránce **typ média** určete, jestli je médium **vyměnitelná jednotka USB** nebo **Sada disků CD/DVD**. Pak nakonfigurujte následující možnosti:  

    > [!IMPORTANT]  
    > Médium používá souborový systém FAT32. Nemůžete vytvořit médium na jednotce USB, jejíž obsah obsahuje soubor větší než 4 GB.  

    - Pokud vyberete **vyměnitelnou jednotku USB**, vyberte jednotku, na kterou chcete obsah uložit.  

        - **Naformátujte vyměnitelnou jednotku USB (FAT32) a proveďte spouštěcí**zařízení: ve výchozím nastavení nechte jednotku USB Configuration Manager připravit. Mnoho novějších zařízení UEFI vyžaduje spouštěcí oddíl FAT32. Tento formát ale taky omezuje velikost souborů a celkovou kapacitu jednotky. Pokud jste již naformátovali a nakonfigurovali vyměnitelnou jednotku, zakažte tuto možnost.

    - Pokud vyberete možnost **sada CD/DVD**, určete kapacitu média (**velikost média**) a název a cestu k výstupnímu souboru (**soubor média**). Průvodce uloží výstupní soubory do tohoto umístění. Příklad: `\\servername\folder\outputfile.iso`  

        Pokud je kapacita média příliš malá pro uložení celého obsahu, vytvoří se několik souborů. Pak je potřeba obsah uložit na víc disků CD nebo DVD. Pokud vyžaduje více mediálních souborů, Configuration Manager přidá číslo sekvence k názvu každého výstupního souboru, který vytvoří.  

        > [!IMPORTANT]  
        > Pokud vyberete stávající bitovou kopii .iso, průvodce média pořadí úlohy odstraní tuto bitovou kopii z disku nebo zruší její sdílení okamžitě po otevření další stránky průvodce. Existující bitová kopie je odstraněna, i když pak průvodce zrušíte.  

    - **Pracovní složka**<!--1359388-->: Proces vytváření médií může vyžadovat mnoho místa na dočasném disku. Ve výchozím nastavení je toto umístění podobné následující cestě: `%UserProfile%\AppData\Local\Temp`. Od verze 1902 získáte větší flexibilitu, kam chcete ukládat tyto dočasné soubory, změňte tuto hodnotu na jinou jednotku a cestu.  

    - **Popisek média**<!--1359388-->: Od verze 1902 přidejte popisek k médiu pořadí úloh. Tento popisek vám pomůže lépe identifikovat médium po jeho vytvoření. Výchozí hodnota je `Configuration Manager`. Toto textové pole se zobrazí v následujících umístěních:  

        - Pokud připojíte soubor ISO, Windows zobrazí tento popisek jako název připojené jednotky.  

        - Pokud naformátujete jednotku USB, použije se jako název prvních 11 znaků popisku.  

        - Configuration Manager zapíše textový soubor s `MediaLabel.txt` názvem do kořenového adresáře média. Ve výchozím nastavení soubor obsahuje jeden řádek textu: `label=Configuration Manager`. Pokud přizpůsobíte popisek pro médium, tento řádek používá vlastní popisek místo výchozí hodnoty.  

    - **Zahrnout soubor Autorun. inf na médium**<!-- 4090666 -->: Počínaje verzí 1906 Configuration Manager ve výchozím nastavení nepřidá soubor Autorun. inf. Tento soubor je pro antimalwarové produkty často blokovaný. Další informace o funkci AutoRun systému Windows najdete v tématu [Vytvoření aplikace CD-ROM s podporou automatického spuštění](https://docs.microsoft.com/windows/desktop/shell/autoplay). Pokud to pro váš scénář pořád potřebujete, vyberte tuto možnost, chcete-li soubor zahrnout.  

5. Na stránce **spouštěcí bitová kopie** určete následující možnosti:  

    > [!IMPORTANT]  
    > Architektura spouštěcí bitové kopie, kterou distribuujete, musí být vhodná pro architekturu cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Ale cílový počítač x86 může bootovat a spustit pouze bootovací obrázek x86.  

    - **Spouštěcí bitová kopie**: výběrem spouštěcí bitové kopie Spusťte cílový počítač.  

    - **Distribuční bod**: Vyberte distribuční bod, který obsahuje spouštěcí bitovou kopii. Průvodce získá bootovací obrázek z distribučního místa a uloží jej do médií.  

        > [!NOTE]  
        > Váš uživatelský účet potřebuje alespoň oprávnění **ke čtení** knihovny obsahu v distribučním bodě.  

6. Dokončete průvodce.  


## <a name="next-steps"></a>Další kroky

[Vytvoření pořadí úkolů pro zachycení image operačního systému](create-a-task-sequence-to-capture-an-operating-system.md)
