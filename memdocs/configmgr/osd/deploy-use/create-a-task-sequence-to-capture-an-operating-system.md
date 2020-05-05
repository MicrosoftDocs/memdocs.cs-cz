---
title: Vytvoření pořadí úkolů pro zachycení image operačního systému
titleSuffix: Configuration Manager
description: Pořadí úloh sestavení a zachycení vytvoří referenční počítač, který může obsahovat konkrétní ovladače a aktualizace softwaru společně s operačním systémem.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723065"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Vytvoření pořadí úkolů pro zachycení image operačního systému

*Platí pro: Configuration Manager (Current Branch)*

Když použijete pořadí úkolů k nasazení operačního systému do počítače v Configuration Manager, počítač nainstaluje image operačního systému, kterou zadáte v pořadí úkolů. Bitovou kopii operačního systému můžete přizpůsobit tak, aby zahrnovala konkrétní ovladače, aplikace a aktualizace softwaru. Nejprve použijte pořadí úkolů sestavení a zachycení k sestavení referenčního počítače. Pak Zachyťte image operačního systému z tohoto referenčního počítače. Pokud již máte k dispozici referenční počítač pro zachycení, vytvořte vlastní pořadí úloh pro zachycení operačního systému.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a>Pořadí úloh sestavení a zachycení

Pořadí úkolů sestavení a zachycení:

- Rozdělí a zformátuje referenční počítač.
- Nainstaluje operační systém
- Nainstaluje klienta Configuration Manager.
- Nainstaluje aplikace
- Použije aktualizace softwaru
- Zachytí operační systém z referenčního počítače.

Balíčky přidružené k tomuto pořadí úkolů, jako jsou aplikace, musí být k dispozici v distribučních bodech před nasazením pořadí úloh sestavení a zachycení.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a>Požadavků

Než vytvoříte pořadí úkolů pro instalaci operačního systému, zajistěte, aby byly zavedeny následující komponenty:  

### <a name="required"></a>Požaduje se

- [Spouštěcí image](../get-started/manage-boot-images.md)

- [Bitová kopie operačního systému](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Požaduje se (pokud se používá)

- [Balíčky ovladačů](../get-started/manage-drivers.md) , které obsahují nezbytné ovladače Windows pro podporu hardwaru v referenčním počítači. Další informace o krocích pořadí úkolů pro správu ovladačů najdete v tématu [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Aktualizace softwaru](../../sum/get-started/synchronize-software-updates.md)

- [Aplikace](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Vytvoření pořadí úkolů sestavení a zachycení

Pomocí následujícího postupu můžete použít pořadí úloh k sestavení referenčního počítače a zachycení operačního systému.

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pořadí úloh** a spusťte tak Průvodce vytvořením pořadí úloh.  

1. Na stránce **Vytvoření nového pořadí úloh** vyberte možnost **Sestavení a zaznamenání referenční bitové kopie operačního systému**.  

1. Na stránce **informace o pořadí úloh** zadejte následující nastavení:  

    - **Název pořadí úkolů**: Zadejte název, který identifikuje pořadí úkolů.  

    - **Popis**: Zadejte volitelný popis pořadí úkolů. Popište například operační systém, který pořadí úkolů vytvoří.

    - **Spouštěcí bitová kopie**: zadejte spouštěcí image, která se má použít pro toto pořadí úloh.  

        > [!IMPORTANT]  
        > Architektura spouštěcí bitové kopie musí být kompatibilní s hardwarovou architekturou cílového počítače.  

1. Na stránce **instalovat systém Windows** zadejte následující nastavení:  

    - **Balíček bitové kopie**: Zadejte balíček bitové kopie operačního systému, který obsahuje soubory potřebné k instalaci operačního systému.  

    - **Index bitové kopie**: zadejte index operačního systému, který se má v imagi nainstalovat. Pokud image operačního systému obsahuje víc verzí, vyberte verzi, kterou chcete nainstalovat.  

    - **Kód Product Key**: v případě potřeby zadejte kód Product Key pro operační systém Windows, který chcete nainstalovat. Zadávat lze šifrované aktivační kódy VLK a standardní kódy Product Key. Pokud používáte kód Product Key, který není kódovaný, oddělte každou skupinu pěti znaky pomlčkou (`-`). Příklad: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Režim licencování serveru**: Pokud je to nutné, zadejte, že licence serveru je **vázaná na stanici**, **na server**nebo že není zadána žádná licence. Pokud je licence serveru **Na server**, zadejte také maximální počet připojení serverů.  

    - Určete, jak nakonfigurovat účet správce pro nasazený operační systém:  

        - **Náhodně generovat heslo místního správce a vypnout účet na všech podporovaných platformách**: Vytvořte náhodné heslo pro účet místního správce. Zakáže účet při nastavení systému Windows.

        - **Povolit účet a zadat heslo místního správce**: použijte stejné heslo pro účet místního správce na všech počítačích, na které tento operační systém nasadíte.

1. Na stránce **Konfigurovat síť** určete následující nastavení:

    - **Připojit k pracovní skupině**: Určete, jestli se má cílový počítač přidat do pracovní skupiny, když se NASADÍ operační systém.  

    - **Připojit k doméně**: Určete, jestli se při nasazení operačního systému má cílový počítač přidat do domény. Do pole **Doména** zadejte název domény.  

        > [!IMPORTANT]  
        > Můžete vyhledat domény v místní doménové struktuře. Zadejte název domény pro vzdálenou doménovou strukturu.

        Zadat lze rovněž organizační jednotku (OU). Toto nastavení je volitelné a určuje rozlišující název LDAP X. 500 pro organizační jednotku, ve které se má účet počítače vytvořit, pokud ještě neexistuje.  

    - **Účet**: Zadejte uživatelské jméno a heslo k účtu, který má oprávnění připojit se k zadané doméně. Například: `domain\user` nebo `%variable%`.  

        > [!IMPORTANT]  
        > Pokud plánujete migrovat nastavení domény nebo pracovní skupiny během nasazení, nezapomeňte sem zadat příslušné přihlašovací údaje do domény.  

1. Na stránce **Configuration Manager instalace** zadejte balíček klienta Configuration Manager. Tento balíček obsahuje zdrojové soubory pro instalaci klienta Configuration Manager. Zadejte také další vlastnosti, které jsou potřeba k instalaci klienta.  

    Další informace najdete v tématu [o vlastnostech instalace klienta](../../core/clients/deploy/about-client-installation-properties.md).

1. Na stránce **Zahrnout aktualizace** určete, zda se mají nainstalovat požadované aktualizace softwaru, všechny aktualizace softwaru nebo žádné aktualizace softwaru. Pokud určíte, že se mají instalovat aktualizace softwaru, Configuration Manager nainstaluje jenom aktualizace softwaru, které jsou cílené na kolekce, kterých je cílový počítač členem.  

1. Na stránce **instalovat aplikace** určete aplikace, které chcete do cílového počítače nainstalovat. Pokud zvolíte více aplikací, můžete také určit, aby pořadí úloh pokračovalo i v případě, že bude instalace některé z aplikací neúspěšná.  

    > [!NOTE]
    > V průvodci se zobrazí stránka **Příprava systému** , ale už se nepoužívá. Pokračujte výběrem tlačítka **Next** (Další).

1. Na stránce **vlastnosti imagí** zadejte následující nastavení pro bitovou kopii operačního systému:

    - **Vytvořil**: Zadejte jméno uživatele, které se má poznamenat jako tvůrce image operačního systému.  

    - **Verze**: zadejte číslo verze, které je přidružené k imagi operačního systému. Tento atribut nemusí být verzí operačního systému, protože lokalita tuto hodnotu ukládá samostatně.

    - **Popis**: zadejte popis image operačního systému.  

1. Na stránce **zachytit bitovou kopii** určete následující nastavení:

    - **Cesta**: Určete sdílenou síťovou složku, kam má Configuration Manager uložit výstupní soubor bitové kopie (. wim). Tento soubor obsahuje bitovou kopii operačního systému, která je založena na nastavení, které zadáte v tomto průvodci. Pokud zadáte složku, která obsahuje existující. Soubor WIM je přepsán.  

    - **Účet**: Určete účet systému Windows, který má oprávnění ke sdílené síťové složce, ve které je image uložená.  

1. Dokončete průvodce.  

Chcete-li do pořadí úkolů přidat další kroky, vyberte jej a zvolte možnost **Upravit**. Další informace o úpravách pořadí úkolů najdete v tématu [použití editoru pořadí úloh](../understand/task-sequence-editor.md).  

Jedním z následujících způsobů nasaďte pořadí úkolů do referenčního počítače:  

- Pokud je již referenční počítač Configuration Manager klientem, nasaďte pořadí úkolů sestavení a zachycení do kolekce, která obsahuje referenční počítač. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

- Pokud referenční počítač není klientem Configuration Manager, nebo pokud chcete pořadí úkolů spustit ručně na referenčním počítači, použijte **Průvodce vytvořením média pořadí úloh** a vytvořte spouštěcí médium. Další informace najdete v tématu [Vytvoření spouštěcího média](create-bootable-media.md).  

Po zaznamenání bitové kopie ji můžete nasadit do jiných počítačů. Další informace o tom, jak nasadit zachycenou image operačního systému, najdete v tématu [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a>Zachytit z existujícího referenčního počítače

Pokud již máte referenční počítač připravený k zachycení, vytvořte pořadí úkolů, které zachytí pouze operační systém z referenčního počítače. Pomocí kroku **zaznamenat bitovou kopii operačního systému** pořadí úkolů můžete zachytit jednu nebo víc imagí z referenčního počítače a uložit je do souboru image (. wim) v zadané síťové sdílené složce. Spusťte referenční počítač v systému Windows PE pomocí spouštěcí bitové kopie. Sekvence úloh zachycuje každý pevný disk v referenčním počítači jako samostatnou bitovou kopii v souboru. wim. Pokud má odkazovaný počítač více jednotek, bude výsledný soubor. wim obsahovat samostatnou bitovou kopii pro každý svazek. Zachycuje jenom svazky, které jsou naformátované jako NTFS nebo FAT32. Přeskočí svazky s jinými formáty nebo svazky USB.  

K zachycení image operačního systému z existujícího referenčního počítače použijte následující postup:

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pořadí úloh**. Tato akce spustí Průvodce vytvořením pořadí úloh.  

1. Na stránce **Vytvoření nového pořadí úloh** vyberte možnost **Vytvořit nové vlastní pořadí úloh**.  

1. Na stránce **informace o pořadí úloh** zadejte název pořadí úkolů. Volitelně můžete přidat popis pořadí úkolů.  

1. Zadejte spouštěcí image pro pořadí úkolů. Configuration Manager používá tuto spouštěcí image ke spuštění referenčního počítače s Windows PE. Další informace najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

1. Dokončete průvodce.  

1. V uzlu **pořadí úloh** vyberte nové pořadí úloh. Pak na kartě **Domů** na pásu karet ve skupině **pořadí úloh** vyberte **Upravit**. Tato akce otevře Editor pořadí úloh.  

1. Pokud je klient Configuration Manager nainstalován v referenčním počítači:

    Přejděte do nabídky **Přidat** , vyberte možnost **bitové kopie**a pak zvolte možnost [připravit klienta nástroje ConfigMgr pro zachytávání](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Tento krok generalizuje Configuration Manager klienta v referenčním počítači.

    > [!Note]  
    > Pořadí úkolů nepodporuje odinstalaci klienta Configuration Manager.

1. Přejděte do nabídky **Přidat** , vyberte možnost **obrázky**a zvolte možnost [připravit systém Windows pro zaznamenání](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Tento krok spustí nástroj Sysprep a potom restartuje počítač do spouštěcí image prostředí Windows PE zadané pro pořadí úkolů. Aby se tato akce úspěšně dokončila, nepřipojujte referenční počítač k doméně.

1. Přejděte do nabídky **Přidat** , vyberte možnost **bitové**kopie a zvolte možnost [zachytit bitovou kopii operačního systému](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage). Tento krok se spouští jenom z Windows PE pro zachycení pevných disků v referenčním počítači. Nakonfigurujte tahle nastavení:

    - **Název** a **Popis**: Volitelně můžete změnit název kroku pořadí úkolů a zadat pro něj popis.  

    - **Cíl**: Určete sdílenou síťovou složku, ve které je uložený výstupní soubor .wim. Tento soubor obsahuje bitovou kopii operačního systému na základě nastavení, které zadáte pomocí tohoto průvodce. Pokud zadáte složku, která obsahuje existující. Soubor WIM je přepsán.  

    - **Popis**, **verze**a **vytvořil**: Volitelně můžete zadat podrobnosti o imagi, kterou chcete zachytit.  

    - **Účet zaznamenání bitové kopie operačního systému**: Určete účet systému Windows, který má oprávnění k zadané sdílené síťové složce. Vyberte **nastavit** a zadejte název tohoto účtu systému Windows.  

Výběrem **OK** uložte změny a zavřete Editor pořadí úloh.  

Jedním z následujících způsobů nasaďte pořadí úkolů do referenčního počítače:  

- Pokud je již referenční počítač Configuration Manager klienta, nasaďte pořadí úkolů zachycení do kolekce, která obsahuje referenční počítač. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

- Pokud referenční počítač není klientem Configuration Manager, nebo pokud chcete pořadí úkolů spustit ručně na referenčním počítači, pomocí **Průvodce vytvořením média pořadí úloh** vytvořte záznamová média. Další informace najdete v tématu [Vytvoření záznamového média](create-capture-media.md).  

Po zaznamenání bitové kopie ji můžete nasadit do jiných počítačů. Další informace o tom, jak nasadit zachycenou image operačního systému, najdete v tématu [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a>Příklad pořadí úkolů

Při vytváření pořadí úkolů, které sestaví a zachytí bitovou kopii operačního systému, použijte jako vodítko následující tabulku. Tabulka vám pomůže určit obecné pořadí kroků pořadí úkolů a postup uspořádání a strukturování těchto kroků do logických skupin. Pořadí úloh, které vytvoříte, se může od této ukázky lišit. Může obsahovat více nebo méně kroků a skupin.

> [!NOTE]  
> K vytváření tohoto typu pořadí úkolů vždycky používejte Průvodce vytvořením pořadí úloh.
>
> Průvodce přidá do pořadí úloh kroky s mírně odlišnými názvy, které se zobrazí, pokud ručně přidáte stejný postup.

### <a name="group-build-the-reference-machine"></a>Skupina: Sestavte referenční počítač

Tato skupina obsahuje akce potřebné k sestavení referenčního počítače.

|Krok pořadí úloh|Popis|  
|-------------------------------|---------------|  
|**Restartování v prostředí Windows PE**|Restartujte cílový počítač do spouštěcí bitové kopie přiřazené k pořadí úkolů. Tento krok zobrazí uživateli zprávu, že se počítač bude restartovat, aby mohla pokračovat instalace.<br /><br />Tento krok používá proměnnou pořadí úkolů jen `_SMSTSInWinPE` pro čtení. Pokud se přidružená hodnota rovná `false`, bude krok pořadí úkolů pokračovat.|
|**Rozdělit disk 0 – BIOS**|Rozdělit a naformátovat pevný disk v cílovém počítači v režimu BIOS. Výchozí číslo disku je `0`.<br /><br />Tento krok používá několik proměnných pořadí úkolů jen pro čtení. Například se spustí jenom v případě, že mezipaměť klienta Configuration Manager neexistuje a nespustí se, pokud je počítač nakonfigurovaný pro rozhraní UEFI.|
|**Rozdělit disk 0 – UEFI**|Vytvořte oddíly a naformátujte pevný disk v cílovém počítači v režimu UEFI. Výchozí číslo disku je `0`.<br /><br />Tento krok používá několik proměnných pořadí úkolů jen pro čtení. Například se spustí jenom v případě, že mezipaměť klienta Configuration Manager neexistuje a spustí se jenom v případě, že je počítač nakonfigurovaný pro rozhraní UEFI.|
|**Použít operační systém**|Nainstalujte zadanou bitovou kopii operačního systému do cílového počítače. Tento krok nejprve odstraní všechny soubory na svazku, kromě souborů ovládacích prvků specifických pro Configuration Manager. Pak použije všechny image svazků obsažené v souboru. WIM na odpovídající sekvenční diskový svazek v cílovém počítači.|
|**Použít nastavení systému Windows**|Nakonfigurujte nastavení systému Windows pro cílový počítač.|
|**Použít nastavení sítě**|Zadejte informace o konfiguraci sítě nebo pracovní skupiny pro cílový počítač.|
|**Použít ovladače zařízení**|Odpovídat a instalovat ovladače jako součást nasazení operačního systému. Další informace najdete v části [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />Tento krok používá proměnnou pořadí úkolů jen `_SMSTSMediaType` pro čtení. Pokud se přidružená hodnota nerovná, tento krok se `FullMedia`nespustí.|
|**Nastavit systém Windows a Configuration Manager**|Nainstalujte klientský software Configuration Manager. Configuration Manager nainstaluje a zaregistruje identifikátor GUID Configuration Manager klienta. Zahrňte všechny nezbytné **vlastnosti instalace**.|
|**Instalovat aktualizace**|Určete, jak jsou aktualizace softwaru nainstalovány v cílovém počítači. V cílovém počítači se nevyhodnocují příslušné aktualizace softwaru, dokud se tento krok nespustí. V tomto okamžiku je hodnocení podobné jako u jakéhokoli jiného klienta spravovaného Configuration Manager. Další informace najdete v tématu [instalace aktualizací softwaru](../understand/install-software-updates.md).<br /><br />Tento krok používá proměnnou pořadí úkolů jen `_SMSTSMediaType` pro čtení. Pokud se přidružená hodnota nerovná, tento krok se `FullMedia`nespustí.|
|**Nainstalovat aplikace**|Určuje všechny aplikace, které se mají nainstalovat do referenčního počítače.|

### <a name="group-capture-the-reference-machine"></a>Skupina: Zachyťte referenční počítač.

Tato skupina obsahuje kroky nezbytné pro přípravu a zachycení referenčního počítače.

|Krok pořadí úloh|Popis|  
|-------------------------------|---------------|  
|**Příprava klienta Configuration Manager**|Generalize Configuration Manager klienta v referenčním počítači.|
|**Příprava operačního systému**|Spustí nástroj Sysprep pro generalizaci oken. Následně restartuje počítač do spouštěcí image prostředí Windows PE zadané pro pořadí úkolů.|
|**Zachytit v referenčním počítači**|Zachytí bitovou kopii do zadané síťové sdílené složky a. Soubor WIM.|

> [!IMPORTANT]
> Po zachycení image z referenčního počítače nezachytíte jinou image operačního systému z referenčního počítače. Položky registru se vytvoří během počáteční konfigurace. Při každém zaznamenání bitové kopie operačního systému vytvořte nový referenční počítač. Pokud plánujete použít stejný referenční počítač k vytvoření budoucích bitových kopií operačních systémů, nejprve odinstalujte a znovu nainstalujte klienta Configuration Manager.

## <a name="next-steps"></a>Další kroky

[Metody nasazení podnikových operačních systémů](methods-to-deploy-enterprise-operating-systems.md)
