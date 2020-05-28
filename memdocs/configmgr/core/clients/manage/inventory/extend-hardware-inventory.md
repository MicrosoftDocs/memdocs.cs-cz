---
title: Rozšíří inventář hardwaru
titleSuffix: Configuration Manager
description: Naučte se, jak rozšíří inventář hardwaru v Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427753"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Postup rozšiřování inventáře hardwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Inventář hardwaru čte informace z počítačů s Windows pomocí rozhraní WMI (Windows Management Instrumentation) (WMI). Rozhraní WMI je implementací standardu WBEM (Web-Based Enterprise Management), což je oborový standard pro přístup k informacím správy v podniku. V předchozích verzích Configuration Manager jste rozšířili inventář hardwaru úpravou souboru sms_def. mof na serveru lokality. Tento soubor obsahoval seznam tříd WMI, které by mohly být čteny inventářem hardwaru. Úpravou tohoto souboru můžete povolit a zakázat existující třídy a také vytvořit nové třídy pro inventarizaci.  

Soubor Configuration. mof se používá k definování datových tříd, které se mají v inventáři hardwaru na klientovi a které se nezměnily Configuration Manager 2012. Můžete vytvořit datové třídy k inventarizaci existujících nebo vlastních datových tříd úložiště WMI nebo klíčů registru přítomných v systémech klientů.  

 Soubor Configuration.mof také definuje a registruje zprostředkovatele WMI, kteří přistupují k informacím zařízení během inventáře hardwaru. Registrace zprostředkovatele definuje typ zprostředkovatele, který se má použít, a třídy, které zprostředkovatel podporuje.  

 Když klienti vyžadují zásady Configuration Manager, soubor Configuration. mof se připojí k tělu zásady. Tento soubor pak klienti stáhnou a zkompilují. Když přidáte, upravíte nebo odstraníte datové třídy v souboru Configuration.mof, klienti automaticky tyto změny provedené u datových tříd týkajících se inventáře zkompilují. K inventarizaci nových nebo upravených datových tříd na Configuration Manager klientech není nutná žádná další akce. Tento soubor je umístěný v adresáři **<umístění_instalace_CM\>\Inboxes\clifiles.src\hinv\\** na serverech primární lokality.  

 V Configuration Manager už soubor sms_def. mof neupravujte stejně jako v Configuration Manager 2007. Místo toho můžete povolit a zakázat třídy WMI a přidat nové třídy shromažďované inventářem hardwaru pomocí nastavení klienta. Configuration Manager poskytuje následující metody pro rozšiřování inventáře hardwaru.  

> [!NOTE]  
>  Pokud jste ručně změnili soubor Configuration. MOF, aby bylo možné přidat vlastní třídy inventáře, tyto změny budou při aktualizaci na verzi 1602 přepsány. Chcete-li po aktualizaci dál používat vlastní třídy, je nutné je po aktualizaci na 1602 přidat do oddílu "přidané přípony" v souboru Configuration. mof.  
> Nesmíte však upravovat cokoli nad touto sekcí, protože tyto oddíly jsou rezervovány pro úpravy Configuration Manager. Zálohu vlastního souboru Configuration.mof najdete v umístění:  
> **<adresář_instalace_CM\>\data\hinvarchive\\**.  

## <a name="methods"></a>Metody

### <a name="enable-or-disable"></a>Povolit nebo zakázat

Povolí nebo zakáže některé z atributů třídy, které již existují v klientovi. Tato akce vydá agentovi pro inventář hardwaru, aby ho mohl shromažďovat na klientech. Tuto akci můžete provést ve výchozím nastavení klienta nebo vlastním nastavení klienta zařízení. Další informace najdete v tématu [Povolení nebo zakázání existujících tříd inventáře](#BKMK_Enable).

### <a name="add"></a>Přidat

Pokud třída WMI existuje v klientovi a je známou lokalitou, bude tato akce zahrnovat tuto akci do možné sady tříd inventáře hardwaru. Můžete přidat novou třídu inventáře z oboru názvů WMI jiného zařízení. Tato akce je určena pouze pro výchozí nastavení klienta. Další informace najdete v tématu [Přidání nové třídy inventáře](#BKMK_Add).

### <a name="extend"></a>Rozšíření

Přidejte k klientovi novou třídu služby WMI. Chcete-li ručně rozšíří inventář hardwaru, upravte soubor Configuration. mof v lokalitě nejvyšší úrovně.<!-- SCCMDocs#1073 -->

Pokud již třída WMI na klientovi neexistuje, je nutné roztáhnout schéma WMI:

1. Upravte soubor Configuration. mof v lokalitě nejvyšší úrovně. Podívejte se na **Dataldr. log** , aby se web přidal.

1. Aktualizujte zásady na klientovi a počkejte, než se nová třída zkompiluje.

1. K [Přidání](#add) nové třídy do inventáře hardwaru použijte výchozí nastavení klienta. Ve výchozím nastavení klienta nemusíte tuto třídu povolit. Pak ho můžete povolit ve vlastním nastavení klienta zařízení.

### <a name="import-and-export"></a>Import a export

Použijte konzolu Configuration Manager k importu a exportu souborů formát MOF (Managed Object Format) (MOF), které obsahují třídy inventáře. Další informace najdete v tématech [Import tříd inventáře hardwaru](#BKMK_Import) a [Export tříd inventáře hardwaru](#BKMK_Export).

### <a name="create-noidmif-files"></a>Vytvoření souborů NOIDMIF

Soubory NOIDMIF můžete použít ke shromažďování informací o klientských zařízeních, která Configuration Manager nemůžou inventář. Například Shromážděte informace o inventárním čísle zařízení, které existuje jenom jako štítek na zařízení. Soubor NOIDMIF se automaticky přidruží klientskému zařízení, ze kterého byl shromážděný. Další informace najdete v tématu [vytvoření souborů NOIDMIF](#BKMK_NOIDMIF).

### <a name="create-idmif-files"></a>Vytvoření souborů IDMIF

Soubory IDMIF můžete použít ke shromažďování informací o prostředcích ve vaší organizaci, které nejsou přidružené k Configuration Manager klientovi. Například projektory, kopírky a síťové tiskárny. Další informace najdete v tématu [vytvoření souborů IDMIF](#BKMK_IDMIF).

## <a name="procedures-to-extend-hardware-inventory"></a>Postupy rozšíření inventáře hardwaru

Tyto postupy vám pomůžou nakonfigurovat výchozí nastavení klienta pro inventář hardwaru a vztahují se na všechny klienty v hierarchii. Pokud chcete toto nastavení použít jenom pro některé klienty, vytvořte vlastní nastavení klientského zařízení a přiřaďte ho ke kolekci konkrétních klientů. Další informace najdete v tématu [Konfigurace nastavení klienta](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Umožňuje povolit nebo zakázat existující třídy inventáře.  

1. V konzole Configuration Manager vyberte možnost **Správa**  >  **nastavení klienta**  >  **výchozí nastavení klienta**.  

1. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

1. V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

1. V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

1. V dialogovém okně **Třídy inventáře hardwaru** zaškrtněte vlastnosti tříd, které má inventář hardwaru shromažďovat, nebo jejich zaškrtnutí zrušte. Můžete třídy rozbalit a zaškrtnout jednotlivé vlastnosti v rámci třídy, nebo jejich zaškrtnutí zrušit. Pomocí pole **Vyhledat třídy inventáře** vyhledejte jednotlivé třídy.  

    > [!IMPORTANT]  
    >  Při přidání nových tříd do Configuration Manager inventáře hardwaru se zvýší velikost souboru inventáře, který se shromažďuje a odesílá na server lokality. To může negativně ovlivnit výkon sítě a Configuration Manager lokality. Povolte jenom ty třídy inventáře, které chcete shromažďovat.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Přidat novou třídu inventáře  

Třídy inventáře můžete přidat jenom ze serveru nejvyšší úrovně v hierarchii tím, že upravíte výchozí nastavení klienta. Tato možnost není dostupná, když vytvoříte vlastní nastavení zařízení.

1. V konzole Configuration Manager vyberte možnost **Správa**  >  **nastavení klienta**  >  **výchozí nastavení klienta**.  

1. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

1. V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

1. V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

1. V dialogovém okně **třídy inventáře hardwaru** klikněte na **Přidat**.  

1. V dialogovém okně **Přidat třídu inventáře hardwaru** vyberte **připojit**.  

1. V dialogovém okně **připojit k rozhraní WMI (Windows Management Instrumentation) (WMI)** zadejte název počítače, ze kterého budete načítat třídy WMI, a obor názvů WMI, který bude použit pro načtení tříd. Pokud chcete načíst všechny třídy pod oborem názvů WMI, který jste zadali, vyberte **rekurzivní**. Pokud není počítač, ke kterému se připojujete, místním počítačem, zadejte přihlašovací údaje pro účet, který má oprávnění pro přístup k rozhraní WMI na vzdáleném počítači.

1. Zvolte **Připojit**.  

1. V dialogovém okně **Přidat třídu inventáře hardwaru** vyberte v seznamu **třídy inventáře** třídy WMI, které chcete přidat do Configuration Manager inventáře hardwaru.  

1. Pokud chcete upravit informace o vybrané třídě WMI, klikněte na **Upravit**a v dialogovém okně **kvalifikátory třídy** zadejte následující informace:  

    - **Zobrazovaný název**: Tento název se zobrazí v Průzkumník prostředků.  

    - **Vlastnosti**: Zadejte jednotky, ve kterých se budou zobrazovat jednotlivé vlastnosti třídy WMI.  

      Můžete také nastavit vlastnosti jako klíčové vlastnosti, které vám pomohou jednoznačně identifikovat každou instanci třídy. Pokud není pro třídu definovaný žádný klíč a z klienta se hlásí víc instancí třídy, v databázi se uloží jenom poslední nalezená instance.  

      Po dokončení konfigurace vlastností vyberte **OK** a zavřete tak dialogové okno **kvalifikátory třídy** a další otevřená dialogová okna.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Importovat třídy inventáře hardwaru

Třídy inventáře můžete importovat, jenom když upravíte výchozí nastavení klienta. Můžete však použít vlastní nastavení klienta pro import informací, které neobsahují změnu schématu, jako je například změna vlastnosti existující třídy z **hodnoty true** na **false**.  

1. V konzole Configuration Manager vyberte možnost **Správa**  >   **nastavení klienta**  >  **výchozí nastavení klienta**.

1. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

1. V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

1. V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

1. V dialogovém okně **třídy inventáře hardwaru** vyberte **importovat**.  

1. V dialogovém okně **importovat** vyberte soubor formát MOF (MANAGED Object Format) (MOF), který chcete importovat, a klikněte na **tlačítko OK**. Zkontrolujte položky, které se naimportují, a pak vyberte **importovat**.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Exportovat třídy inventáře hardwaru  

1. V konzole Configuration Manager vyberte možnost **Správa**  >  **nastavení klienta**  >  **výchozí nastavení klienta**.  

1. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

1. V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

1. V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

1. V dialogovém okně **třídy inventáře hardwaru** klikněte na tlačítko **exportovat**.  

    > [!NOTE]  
    > Při exportu tříd se exportují všechny aktuálně vybrané třídy.  

1. V dialogovém okně **exportovat** zadejte soubor formát MOF (MANAGED Object Format) (MOF), do kterého chcete třídy exportovat, a pak zvolte možnost **Uložit**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Konfigurace inventáře hardwaru pro shromažďování řetězců větších než 255 znaků

Pro vlastnosti inventáře hardwaru můžete zadat délku řetězce, který bude větší než 255 znaků. Tato akce se vztahuje pouze na nově přidané třídy a vlastnosti inventáře hardwaru, které nejsou klíče. <!-- 1357389 -->

1. V pracovním prostoru **Správa** vyberte **nastavení klienta**. Zvolte nastavení klientského zařízení, které chcete upravit, a pak vyberte **vlastnosti**.

1. Vyberte **inventář hardwaru**a pak **nastavte třídy**a **Přidat**.

1. Vyberte **Připojit**.

1. Do pole **název počítače**zadejte **obor názvů rozhraní WMI**a v případě potřeby vyberte možnost **rekurzivní** . V případě potřeby zadejte přihlašovací údaje pro připojení. Vyberte **připojit** a zobrazte třídy oboru názvů.

1. Vyberte novou třídu a pak vyberte **Upravit**.

1. Změňte **délku** vlastnosti, která je řetězcem, jiné než klíč, aby byla větší než 255. Vyberte **OK**.

1. Zajistěte, aby byla upravená vlastnost vybraná pro možnost **Přidat třídu inventáře hardwaru**, a vyberte **OK**.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>Použití souborů MIF k rozšiřování inventáře hardwaru

Soubory MIF (Management Information Format) můžete použít k rozšiřování informací o inventáři hardwaru shromážděných z klientů pomocí Configuration Manager. Informace uložené v souborech MIF se během inventáře hardwaru přidají do sestavy inventáře klienta a uloží v databázi lokality, kde můžete data použít stejným způsobem, jakým používáte výchozí data inventáře klienta. Existují dva typy souborů MIF: NOIDMIF a IDMIF.

> [!IMPORTANT]  
> Než budete moct přidat informace ze souborů MIF do databáze Configuration Manager, musíte pro ně vytvořit nebo importovat informace o třídě. Další informace najdete v částech [pro přidání nové třídy inventáře](#BKMK_Add) a [importu tříd inventáře hardwaru](#BKMK_Import) v tomto článku.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>Vytvoření souborů NOIDMIF

Soubory NOIDMIF se dají použít k přidání informací do inventáře hardwaru klienta, které nemůžou normálně shromažďovat Configuration Manager a jsou přidružené ke konkrétnímu klientskému zařízení. Mnoho společností například označí každý počítač v organizaci číslem assetu a potom ručně zaregistruje tato čísla do katalogu. Když vytvoříte soubor NOIDMIF, dají se tyto informace přidat do databáze Configuration Manager a budou se používat pro dotazy a vytváření sestav. Informace o vytváření souborů NOIDMIF najdete v dokumentaci k sadě SDK pro Configuration Manager.  

> [!IMPORTANT]  
> Když vytvoříte soubor NOIDMIF, musíte ho uložit ve formátu kódování ANSI. Soubory NOIDMIF uložené ve formátu UTF-8 nelze číst pomocí Configuration Manager.  

Po vytvoření souboru NOIDMIF ho uložte do `%Windir%\CCM\Inventory\Noidmifs` složky v každém klientovi. Configuration Manager bude shromažďovat informace ze souborů NODMIF v této složce během příštího naplánovaného cyklu inventáře hardwaru.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a>Vytvoření souborů IDMIF

Soubory IDMIF se dají použít k přidání informací o prostředcích, které se normálně nedaří v inventáři, pomocí Configuration Manager a nejsou přidružené ke konkrétnímu klientskému zařízení, do databáze Configuration Manager. Můžete například použít soubory IDMIF ke shromažďování informací o projektorech, přehrávačích DVD, fotokopírkách nebo jiných zařízeních, která nemají klienta Configuration Manager. Informace o vytváření souborů IDMIF najdete v dokumentaci k sadě SDK pro Configuration Manager.  

Po vytvoření souboru IDMIF ho uložte do `%Windir%\CCM\Inventory\Idmifs` složky na klientských počítačích. Configuration Manager bude shromažďovat informace z tohoto souboru během příštího naplánovaného cyklu inventáře hardwaru. Deklarovat nové třídy pro informace obsažené v souboru přidáním nebo importováním.  

> [!NOTE]
> Soubory MIF můžou obsahovat velká množství dat a shromažďování těchto dat může mít negativní vliv na výkon lokality. Povolte shromažďování souborů MIF pouze v případě potřeby a nakonfigurujte možnost **maximální velikost vlastního souboru MIF (KB)** v nastavení inventáře hardwaru. Další informace najdete v tématu [Úvod do inventáře hardwaru](introduction-to-hardware-inventory.md).
