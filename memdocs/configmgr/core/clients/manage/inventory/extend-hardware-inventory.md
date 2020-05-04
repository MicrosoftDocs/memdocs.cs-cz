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
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714413"
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

|Metoda|Další informace|  
|------------|----------------------|  
|Povolení nebo zákaz existujících tříd inventáře|Povolte nebo zakažte výchozí třídy inventáře nebo vytvořte vlastní nastavení klienta, které umožňuje shromažďovat různé třídy inventáře hardwaru ze zadaných kolekcí klientů. Viz postup [Povolení nebo zakázání existujících tříd inventáře](#BKMK_Enable) v tomto článku.|  
|Přidání nové třídy inventáře|Přidejte novou třídu inventáře z oboru názvů WMI jiného zařízení. Postup [Přidání nové třídy inventáře](#BKMK_Add) v tomto článku najdete v tématu.|  
|Import a export tříd inventáře hardwaru|Importujte a exportujte soubory formát MOF (Managed Object Format) (MOF), které obsahují třídy inventáře, z konzoly Configuration Manager. Postup [importu tříd](#BKMK_Import) inventáře hardwaru a [exportu tříd inventáře hardwaru](#BKMK_Export) v tomto článku najdete v tématu.|  
|Vytvoření souborů NOIDMIF|Soubory NOIDMIF můžete použít ke shromažďování informací o klientských zařízeních, která nemůžou být v inventáři Configuration Manager. Můžete například chtít shromažďovat pro zařízení informace o evidenčním čísle, které existuje jenom jako štítek na zařízení. Soubor NOIDMIF se automaticky přidruží klientskému zařízení, ze kterého byl shromážděný. Další informace najdete v tématu [vytvoření souborů NOIDMIF](#BKMK_NOIDMIF) v tomto článku.|  
|Vytvoření souborů IDMIF|Soubory IDMIF můžete použít ke shromažďování informací o prostředcích ve vaší organizaci, které nejsou přidružené k Configuration Manager klientovi, například projektory, kopírky a síťové tiskárny. Další informace najdete v tématu [vytvoření souborů IDMIF](#BKMK_IDMIF) v tomto článku.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Postupy rozšíření inventáře hardwaru  
Tyto postupy vám pomůžou nakonfigurovat výchozí nastavení klienta pro inventář hardwaru a vztahují se na všechny klienty v hierarchii. Pokud chcete toto nastavení použít jenom pro některé klienty, vytvořte vlastní nastavení klientského zařízení a přiřaďte ho ke kolekci konkrétních klientů. Viz [Jak konfigurovat nastavení klienta](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Postup povolení nebo zákazu existujících tříd inventáře  

1.  V konzole Configuration Manager vyberte možnost **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  

4.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

5.  V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

6.  V seznamu **Nastavení zařízení** klikněte na **Nastavit třídy**.  

7.  V dialogovém okně **Třídy inventáře hardwaru** zaškrtněte vlastnosti tříd, které má inventář hardwaru shromažďovat, nebo jejich zaškrtnutí zrušte. Můžete třídy rozbalit a zaškrtnout jednotlivé vlastnosti v rámci třídy, nebo jejich zaškrtnutí zrušit. Pomocí pole **Vyhledat třídy inventáře** vyhledejte jednotlivé třídy.  

    > [!IMPORTANT]  
    >  Při přidání nových tříd do Configuration Manager inventáře hardwaru se zvýší velikost souboru inventáře, který se shromažďuje a odesílá na server lokality. To může negativně ovlivnit výkon sítě a Configuration Manager lokality. Povolte jenom ty třídy inventáře, které chcete shromažďovat.  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Přidání nové třídy inventáře  

Třídy inventáře můžete přidat jenom ze serveru nejvyšší úrovně v hierarchii tím, že upravíte výchozí nastavení klienta. Tato možnost není dostupná, když vytvoříte vlastní nastavení zařízení.

1. V konzole Configuration Manager vyberte možnost **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  

2. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

3. V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

4. V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

5. V dialogovém okně **třídy inventáře hardwaru** klikněte na **Přidat**.  

6. V dialogovém okně **Přidat třídu inventáře hardwaru** klikněte na **Připojit**.  

7. V dialogovém okně **Připojit ke službě Windows Management Instrumentation (WMI)** zadejte název počítače, ze kterého se budou načítat třídy WMI, a oboru názvů WMI použitý pro získání tříd. Pokud chcete načíst všechny třídy pod zadaným oborem názvů WMI, klikněte na **Rekurzivní**. Pokud není počítač, ke kterému se připojujete, místním počítačem, zadejte přihlašovací údaje pro účet, který má oprávnění k přístupu ke službě WMI na vzdáleném počítači.  

8. Zvolte **Připojit**.  

9. V dialogovém okně **Přidat třídu inventáře hardwaru** vyberte v seznamu **třídy inventáře** třídy WMI, které chcete přidat do Configuration Manager inventáře hardwaru.  

10. Pokud chcete upravit informace o vybrané třídě WMI, klikněte na **Upravit**a v dialogovém okně **kvalifikátory třídy** zadejte následující informace:  

    - **Zobrazované jméno** – tento název se zobrazí v Průzkumník prostředků.  

    - **Vlastnosti** – zadejte jednotky, ve kterých se budou zobrazovat jednotlivé vlastnosti třídy WMI.  

      Můžete také určit vlastnosti jako vlastnosti klíče, aby bylo možné jednoznačně identifikovat každou instanci třídy. Pokud není pro třídu definovaný žádný klíč a z klienta se hlásí víc instancí třídy, v databázi se uloží jenom poslední nalezená instance.  

      Po dokončení konfigurace vlastností kliknutím na tlačítko **OK** zavřete dialogové okno **kvalifikátory třídy** a další otevřená dialogová okna. 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Import tříd inventáře hardwaru  

Třídy inventáře můžete importovat, jenom když upravíte výchozí nastavení klienta. Můžete však použít vlastní nastavení klienta pro import informací, které neobsahují změnu schématu, jako je například změna vlastnosti existující třídy z **hodnoty true** na **false**.  

1.  V konzole Configuration Manager vyberte možnost **Správa** >  **Nastavení** > klienta**výchozí nastavení klienta**.  

4.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

5.  V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

6.  V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

7.  V dialogovém okně **třídy inventáře hardwaru** vyberte **importovat**.  

8.  V dialogovém okně **importovat** vyberte soubor formát MOF (MANAGED Object Format) (MOF), který chcete importovat, a klikněte na **tlačítko OK**. Zkontrolujte položky, které se naimportují, a pak klikněte na **importovat**.  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Export tříd inventáře hardwaru  

1.  V konzole Configuration Manager vyberte možnost **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  

4.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

5.  V dialogovém okně **výchozí nastavení klienta** vyberte **inventář hardwaru**.  

6.  V seznamu **nastavení zařízení** vyberte možnost **nastavit třídy**.  

7.  V dialogovém okně **třídy inventáře hardwaru** klikněte na tlačítko **exportovat**.  

    > [!NOTE]  
    >  Při exportu tříd se exportují všechny aktuálně vybrané třídy.  

8.  V dialogovém okně **exportovat** zadejte soubor formát MOF (MANAGED Object Format) (MOF), do kterého chcete třídy exportovat, a pak zvolte možnost **Uložit**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Konfigurace inventáře hardwaru pro shromažďování řetězců větších než 255 znaků
Počínaje Configuration Manager 1802 můžete zadat délku řetězců, které mají být delší než 255 znaků pro vlastnosti inventáře hardwaru. Tato změna se vztahuje pouze na nově přidané třídy a vlastnosti inventáře hardwaru, které nejsou klíče. <!-- 1357389 -->

1. V pracovním prostoru **Správa** klikněte na **nastavení klienta** zvýraznit nastavení klientského zařízení, které chcete upravit, klikněte pravým tlačítkem myši a vyberte možnost **vlastnosti**.

2. Vyberte **inventář hardwaru**a pak **nastavte třídy**a **Přidat**.

3. Klikněte na tlačítko **připojit** .

4. Do pole **název počítače**zadejte **obor názvů rozhraní WMI**a v případě potřeby vyberte možnost **rekurzivní** . V případě potřeby zadejte přihlašovací údaje pro připojení. Kliknutím na **připojit** Zobrazte třídy oboru názvů.

5. Vyberte novou třídu a pak klikněte na **Upravit**.

6. Změňte **délku** vlastnosti, která je řetězec, jiný než klíč, tak, aby byla větší než 255. Klikněte na tlačítko **OK**. 

7. Zajistěte, aby byla upravená vlastnost pro **Přidat třídu inventáře hardwaru** vybrána, a klikněte na tlačítko **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Postup použití souborů MIF (Management Information Format) k rozšíření inventáře hardwaru  
 Soubory MIF (Management Information Format) můžete použít k rozšiřování informací o inventáři hardwaru shromážděných z klientů pomocí Configuration Manager. Informace uložené v souborech MIF se během inventáře hardwaru přidají do sestavy inventáře klienta a uloží v databázi lokality, kde můžete data použít stejným způsobem, jakým používáte výchozí data inventáře klienta. Existují dva typy souborů MIF, NOIDMIF a IDMIF.

> [!IMPORTANT]  
>  Než budete moct přidat informace ze souborů MIF do databáze Configuration Manager, musíte pro ně vytvořit nebo importovat informace o třídě. Další informace najdete v částech [pro přidání nové třídy inventáře](#BKMK_Add) a [importu tříd inventáře hardwaru](#BKMK_Import) v tomto článku.  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>Vytvoření souborů NOIDMIF  
 Soubory NOIDMIF se dají použít k přidání informací do inventáře hardwaru klienta, které nemůžou normálně shromažďovat Configuration Manager a jsou přidružené ke konkrétnímu klientskému zařízení. Mnoho společností například označí každý počítač v organizaci číslem assetu a potom ručně zaregistruje tato čísla do katalogu. Když vytvoříte soubor NOIDMIF, dají se tyto informace přidat do databáze Configuration Manager a budou se používat pro dotazy a vytváření sestav. Informace o vytváření souborů NOIDMIF najdete v dokumentaci k sadě SDK pro Configuration Manager.  

> [!IMPORTANT]  
>  Když vytvoříte soubor NOIDMIF, musíte ho uložit ve formátu kódování ANSI. Soubory NOIDMIF uložené ve formátu UTF-8 nelze číst pomocí Configuration Manager.  

 Po vytvoření souboru NOIDMIF ho uložte do složky _% windir%_**\CCM\Inventory\Noidmifs** v každém klientovi. Configuration Manager bude shromažďovat informace ze souborů NODMIF v této složce během příštího naplánovaného cyklu inventáře hardwaru.  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a>Vytvoření souborů IDMIF  
 Soubory IDMIF se dají použít k přidání informací o prostředcích, které se normálně nedaří v inventáři, pomocí Configuration Manager a nejsou přidružené ke konkrétnímu klientskému zařízení, do databáze Configuration Manager. Můžete například použít soubory IDMIF ke shromažďování informací o projektorech, přehrávačích DVD, fotokopírkách nebo jiných zařízeních, která nemají klienta Configuration Manager. Informace o vytváření souborů IDMIF najdete v dokumentaci k sadě SDK pro Configuration Manager.  

 Po vytvoření souboru IDMIF ho uložte do složky _% windir%_**\CCM\Inventory\Idmifs** v klientských počítačích. Configuration Manager bude shromažďovat informace z tohoto souboru během příštího naplánovaného cyklu inventáře hardwaru. Je potřeba deklarovat nové třídy pro informace obsažené v souboru jejich přidáním nebo importováním.  

> [!NOTE]
> Soubory MIF můžou obsahovat velká množství dat a shromažďování těchto dat může mít negativní vliv na výkon lokality. Povolte shromažďování souborů MIF pouze v případě potřeby a nakonfigurujte možnost **maximální velikost vlastního souboru MIF (KB)** v nastavení inventáře hardwaru. Další informace najdete v tématu [Úvod do inventáře hardwaru](introduction-to-hardware-inventory.md).
