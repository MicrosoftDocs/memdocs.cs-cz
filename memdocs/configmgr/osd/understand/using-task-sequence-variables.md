---
title: Jak používat proměnné pořadí úkolů
titleSuffix: Configuration Manager
description: Přečtěte si, jak používat proměnné v Configuration Manager pořadí úkolů.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c043cfabc411dbd5ae4984110fc2904d37669300
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717822"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Použití proměnných pořadí úkolů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

 Modul pořadí úloh v nástroji pro nasazení operačního systému Configuration Manager používá k řízení jeho chování mnoho proměnných. Tyto proměnné použijte k následujícím akcím:

- Nastavit podmínky kroků  
- Změnit chování pro konkrétní kroky  
- Použití ve skriptech pro složitější akce  

Odkaz na všechny dostupné proměnné pořadí úkolů najdete v tématu [proměnné pořadí úkolů](task-sequence-variables.md).

## <a name="types-of-variables"></a><a name="bkmk_types"></a>Typy proměnných

Existuje několik typů proměnných:  

- [Integrované](#bkmk_built-in)  
- [Akce](#bkmk_action)  
- [Vlastní](#bkmk_custom)  
- [Jen pro čtení](#bkmk_read-only)  
- [Pole](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a>Předdefinované proměnné

Předdefinované proměnné poskytují informace o prostředí, ve kterém je spuštěno pořadí úloh. Jejich hodnoty jsou k dispozici v celém celé sekvenci úloh. Modul pořadí úkolů obvykle inicializuje předdefinované proměnné předtím, než spustí všechny kroky.

Například `_SMSTSLogPath` je proměnná prostředí, která určuje cestu, do které Configuration Manager komponenty zapisují soubory protokolů. K této proměnné prostředí má přístup libovolný krok pořadí úloh.

Pořadí úkolů vyhodnotí některé proměnné před každým krokem. Například `_SMSTSCurrentActionName` vypíše název aktuálního kroku.

### <a name="action-variables"></a><a name="bkmk_action"></a>Proměnné akcí

Proměnné akcí pořadí úkolů určují nastavení konfigurace, které používá jeden krok pořadí úkolů. Ve výchozím nastavení krok inicializuje jeho nastavení před spuštěním. Tato nastavení jsou dostupná jenom v případě, že se spustí přidružený krok pořadí úkolů. Pořadí úkolů přidá hodnotu proměnné akce do prostředí před tím, než spustí krok. Po spuštění tohoto kroku pak odstraní hodnotu z prostředí.

Například můžete přidat krok **Spustit příkazový řádek** do pořadí úkolů. Tento krok zahrnuje vlastnost **Spustit v** . Pořadí úkolů ukládá jako `WorkingDirectory` proměnnou výchozí hodnotu této vlastnosti. Pořadí úkolů Inicializuje tuto hodnotu před spuštěním kroku **Spustit příkazový řádek** . I když je tento krok spuštěný, přejděte k hodnotě vlastnosti **Spustit v** z `WorkingDirectory` hodnoty. Po dokončení kroku pořadí úloh odebere hodnotu `WorkingDirectory` proměnné z prostředí. Pokud pořadí úkolů obsahuje jiný krok **Spustit příkazový řádek** , Inicializuje novou `WorkingDirectory` proměnnou. V tuto chvíli pořadí úkolů nastaví proměnnou na počáteční hodnotu pro aktuální krok. Další informace najdete v tématu [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

*Výchozí* hodnota pro proměnnou akce je přítomna při spuštění kroku. Pokud nastavíte *novou* hodnotu, je k dispozici pro několik kroků v pořadí úkolů. Pokud přepíšete výchozí hodnotu, nová hodnota zůstane v prostředí. Tato nová hodnota přepisuje výchozí hodnotu pro další kroky v pořadí úkolů. Například přidáte jako první krok pořadí úloh nastavit krok s **proměnným pořadí úloh** . Tento krok nastaví `WorkingDirectory` proměnnou na `C:\`. Libovolný krok **příkazového řádku pro spuštění** v pořadí úkolů používá novou hodnotu počátečního adresáře.  

Některé kroky pořadí úkolů označují určité proměnné akcí jako *výstup*. Kroky níže v pořadí úkolů čtou tyto výstupní proměnné.

> [!Note]  
> Ne všechny kroky pořadí úloh mají proměnné akcí. Například i když jsou k akci **zapnout nástroj BitLocker** přidružené proměnné, k akci **Vypnout nástroj BitLocker** nejsou přidružené žádné proměnné.  

### <a name="custom-variables"></a><a name="bkmk_custom"></a>Vlastní proměnné

Tyto proměnné jsou všechny, které Configuration Manager nevytváří. Inicializujte vlastní proměnné, které se použijí jako podmínky, na příkazových řádcích nebo ve skriptech.

Když zadáte název nové proměnné pořadí úkolů, postupujte podle těchto pokynů:  

- Název proměnné pořadí úloh může obsahovat písmena, číslice, podtržítko (`_`) a spojovník (`-`).  

- Názvy proměnných pořadí úloh mají minimální délku jednoho znaku a maximální délku 256 znaků.  

- Uživatelem definované proměnné musí začínat písmenem (`A-Z` nebo `a-z`).  

- Uživatelsky definované názvy proměnných nemůžou začínat znakem podtržítka. Znakem podtržítka předchází pouze proměnné pořadí úkolů jen pro čtení.  

- Názvy proměnných pořadí úloh nerozlišují velká a malá písmena. Například `OSDVAR` a `osdvar` jsou stejnou proměnnou pořadí úkolů.  

- Názvy proměnných pořadí úloh nemůžou začínat ani končit mezerou. Nemůžou mít taky vložené mezery. Pořadí úkolů ignoruje všechny mezery na začátku nebo konci názvu proměnné.  

Pro počet proměnných pořadí úkolů, které můžete vytvořit, není nastavené žádné omezení. Počet proměnných je však limitován velikostí prostředí pořadí úloh. Limit celkové velikosti prostředí pořadí úkolů je 32 MB.  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a>Proměnné jen pro čtení

Nemůžete změnit hodnotu některých proměnných, které jsou jen pro čtení. Název obvykle začíná znakem podtržítka (`_`). Pořadí úkolů je používá pro své operace. Proměnné jen pro čtení jsou viditelné v prostředí pořadí úloh.

Tyto proměnné jsou užitečné ve skriptech nebo příkazových řádcích. Například spuštění příkazového řádku a zřetězení výstupu do souboru protokolu v `_SMSTSLogPath` nástroji pomocí dalších souborů protokolu.

> [!NOTE]  
> Proměnné pořadí úkolů jen pro čtení lze číst podle kroků v pořadí úloh, ale nelze je nastavit. Například použijte proměnnou jen pro čtení jako součást příkazového řádku pro krok **Spustit příkazový řádek** . Proměnnou určenou jen pro čtení nelze nastavit pomocí kroku **nastavit proměnnou pořadí úloh** .  

### <a name="array-variables"></a><a name="bkmk_array"></a>Proměnné pole

Pořadí úkolů ukládá některé proměnné jako pole. Každý prvek v poli představuje nastavení pro jeden objekt. Tyto proměnné použijte, pokud má zařízení více než jeden objekt ke konfiguraci. Následující kroky pořadí úkolů používají proměnné pole:

- [Použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Formátovat a rozdělit disk na oddíly](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a>Postup nastavení proměnných

U vlastních proměnných nebo proměnných, které nejsou jen pro čtení, existuje několik metod, jak inicializovat a nastavit hodnotu proměnné:  

- [Nastavit krok pro proměnnou pořadí úloh](#bkmk_set-ts-step)
- Krok [Nastavení dynamických proměnných](#bkmk_set-dyn-step)
- [Spustit krok skriptu PowerShellu](#bkmk_run-ps)
- [Kolekce a proměnné zařízení](#bkmk_set-coll-var)  
- [Objekt COM TSEnvironment](#bkmk_set-com)  
- [Příkaz před zahájením](#bkmk_set-prestart)  
- [Průvodce pořadím úloh](#bkmk_set-tswiz)
- [Průvodce médii pořadí úloh](#bkmk_set-media)  

Odstraňte proměnnou z prostředí pomocí stejných metod jako při vytváření proměnné. Chcete-li odstranit proměnnou, nastavte hodnotu proměnné na prázdný řetězec.  

Můžete zkombinovat metody a nastavit proměnnou pořadí úloh na různé hodnoty pro stejnou sekvenci. Nastavte například výchozí hodnoty pomocí editoru pořadí úloh a pak nastavte vlastní hodnoty pomocí skriptu.

Pokud jste stejnou proměnnou nastavili pomocí různých metod, modul pořadí úkolů používá následující pořadí:  

1. Nejprve vyhodnotí proměnné kolekce.  

2. Proměnné specifické pro zařízení přepíšou stejnou sadu proměnných u kolekce.  

3. Proměnné nastavené jakoukoliv metodou v pořadí úkolů mají přednost před proměnnými kolekce nebo zařízení.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Obecná omezení pro hodnoty proměnných pořadí úkolů

- Hodnoty proměnných pořadí úloh nemůžou být delší než 4 000 znaků.  

- Proměnnou pořadí úkolů jen pro čtení nemůžete změnit. Proměnné jen pro čtení mají názvy, které začínají znakem podtržítka (`_`).  

- Hodnoty proměnných pořadí úloh mohou rozlišovat velká a malá písmena v závislosti na použití hodnoty. Ve většině případů hodnoty proměnných pořadí úkolů nerozlišují velká a malá písmena. Proměnná, která obsahuje heslo, rozlišuje velká a malá písmena.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a>Nastavit proměnnou pořadí úloh

Pomocí tohoto kroku v pořadí úkolů můžete nastavit jednu proměnnou na jedinou hodnotu.

Další informace najdete v tématu [nastavení proměnné pořadí úkolů](task-sequence-steps.md#BKMK_SetTaskSequenceVariable).

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a>Nastavit dynamické proměnné

Tento krok pořadí úkolů použijte k nastavení jedné nebo více proměnných pořadí úkolů. V tomto kroku definujete pravidla, která určují proměnné a hodnoty, které se mají použít.

Další informace najdete v tématu [Nastavení dynamických proměnných](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a>Spustit skript prostředí PowerShell

<!-- 6315548 -->

Tento krok pořadí úkolů použijte k nastavení proměnné pořadí úkolů pomocí skriptu prostředí PowerShell.

Můžete zadat název skriptu z balíčku nebo přímo do kroku zadat skript prostředí PowerShell. Pak pomocí vlastnosti krok v poli **výstup do proměnné pořadí úkolů** uložte výstup skriptu do vlastní proměnné pořadí úkolů.

Další informace o tomto kroku najdete v tématu [spuštění skriptu PowerShellu](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> Můžete také použít skript prostředí PowerShell k nastavení jedné nebo více proměnných s objektem **TSEnvironment** . Další informace najdete v tématu [Použití proměnných v běžícím pořadí úkolů](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) v sadě Configuration Manager SDK.

#### <a name="example-scenario-with-run-powershell-script-step"></a>Ukázkový scénář s krokem spuštění skriptu PowerShellu

Vaše prostředí obsahuje uživatele ve více zemích, takže chcete zadat dotaz na jazyk operačního systému, který se má nastavit jako podmínka pro použití v rámci více kroků **operačního systému** pro konkrétní jazyk.

1. Přidejte instanci **skriptu Run PowerShell** do pořadí úkolů před kroky **použít operační systém** .

1. Pomocí možnosti **zadejte skript prostředí PowerShell** pro zadání následujícího příkazu:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Další informace o této rutině naleznete v tématu [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture). Další informace o názvech jazyka ISO se dvěma písmeny najdete v [seznamu kódů iso 639-1](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. Pro možnost **výstup do proměnné pořadí úkolů**zadejte `CurrentOSLanguage`.

    ![Snímek obrazovky s příkladem, jak spustit krok skriptu PowerShellu](media/run-powershell-script-example-language.png)

1. V kroku **použít operační systém** pro obrázek v anglické jazykové verzi vytvořte tuto podmínku:`Task Sequence Variable CurrentOSLanguage equals "en"`

    ![Snímek obrazovky s příkladem podmínky pro krok použití operačního systému](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Další informace o tom, jak vytvořit podmínku pro krok, najdete v tématu [Jak získat přístup k proměnným – krok kroku](#bkmk_access-condition).

1. Uložte a nasaďte pořadí úkolů.

Když se krok **Spustit skript PowerShellu** spustí na zařízení s anglickou jazykovou verzí Windows, příkaz vrátí hodnotu `en`. Pak tuto hodnotu uloží do vlastní proměnné. Když se na stejném zařízení spustí krok **použít operační systém** pro bitovou kopii v anglickém jazyce, podmínka se vyhodnotí jako true. Pokud máte více instancí kroku **použít operační systém** pro různé jazyky, pořadí úkolů dynamicky spustí krok, který odpovídá jazyku operačního systému.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a>Kolekce a proměnné zařízení

Pro zařízení a kolekce můžete definovat vlastní proměnné pořadí úkolů. Proměnné, které definujete pro zařízení, se označují jako proměnné pořadí úkolů pro zařízení. Proměnné definované pro kolekci jsou odkazovány jako proměnné pořadí úkolů pro kolekci. Pokud dojde ke konfliktu, proměnné pro zařízení mají přednost před proměnnými pro kolekci. Toto chování znamená, že proměnné pořadí úkolů, které jsou přiřazeny konkrétnímu zařízení, mají automaticky vyšší prioritu než proměnné, které jsou přiřazeny ke kolekci, která obsahuje zařízení.  

Například zařízení XYZ je členem kolekce ABC. Přiřadíte MojePromenna ke kolekci ABC s hodnotou 1. Přiřadíte také MojePromenna k zařízení XYZ s hodnotou 2. Proměnná přiřazená k XYZ má vyšší prioritu než proměnná přiřazená kolekci ABC. Když pořadí úkolů s touto proměnnou běží na XYZ, MojePromenna má hodnotu 2.

Proměnné pro zařízení a pro kolekci můžete skrýt, aby nebyly viditelné v konzole Configuration Manager. Když použijete možnost **nezobrazit tuto hodnotu v konzole Configuration Manager**, hodnota proměnné se nezobrazí v konzole nástroje. Proměnnou lze v pořadí úkolů používat i v případě, že je spuštěna. Pokud již nechcete tyto proměnné skrývat, nejprve je odstraňte. Pak předefinujte proměnné bez výběru možnosti jejich skrytí.  

> [!WARNING]  
> Nastavení pro **zobrazení této hodnoty v konzole Configuration Manager** se vztahuje pouze na konzolu Configuration Manager. Hodnoty proměnných jsou stále zobrazeny v souboru protokolu pořadí úkolů (**souboru Smsts. log**).

Proměnné pro zařízení můžete spravovat v primární lokalitě nebo v lokalitě centrální správy. Configuration Manager nepodporuje pro zařízení více než 1 000 přiřazených proměnných.  

> [!IMPORTANT]  
> Když použijete proměnné pro kolekci pro pořadí úkolů, zvažte následující chování:  
>
> - Změny kolekcí jsou vždy replikovány v celé hierarchii. Všechny změny, které provedete v proměnných kolekce, platí nejen pro členy aktuální lokality, ale pro všechny členy kolekce v celé hierarchii.  
>  
> - Když kolekci odstraníte, tato akce odstraní také proměnné pořadí úkolů, které jste pro kolekci nakonfigurovali.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Vytvoření proměnných pořadí úkolů pro *zařízení*

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** .  

2. Vyberte cílové zařízení a vyberte **vlastnosti**.  

3. V dialogovém okně **vlastnosti** přepněte na kartu **proměnné** .  

4. Pro každou proměnnou, kterou chcete vytvořit, vyberte **novou** ikonu. Zadejte **název** a **hodnotu** proměnné pořadí úkolů. Chcete-li skrýt proměnnou tak, aby nebyla viditelná v konzole Configuration Manager, vyberte možnost **Nezobrazovat tuto hodnotu v konzole Configuration Manager**.  

5. Po přidání všech proměnných do vlastností zařízení vyberte **OK**.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Vytváření proměnných pořadí úkolů pro *kolekci*

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **kolekce zařízení** . Vyberte cílovou kolekci a zvolte **vlastnosti**.  

2. V dialogovém okně **vlastnosti** přepněte na kartu **proměnné kolekce** .  

3. Pro každou proměnnou, kterou chcete vytvořit, vyberte **novou** ikonu. Zadejte **název** a **hodnotu** proměnné pořadí úkolů. Chcete-li skrýt proměnnou tak, aby nebyla viditelná v konzole Configuration Manager, vyberte možnost **Nezobrazovat tuto hodnotu v konzole Configuration Manager**.  

4. Volitelně můžete zadat prioritu Configuration Manager, která se má použít při vyhodnocení proměnných pořadí úkolů.  

5. Po přidání všech proměnných do vlastností kolekce vyberte **OK**.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a>Objekt COM TSEnvironment

Chcete-li pracovat s proměnnými ze skriptu, použijte objekt **TSEnvironment** .

Další informace najdete v tématu [Použití proměnných v běžícím pořadí úkolů](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) v sadě Configuration Manager SDK.

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a>Příkaz před zahájením

Předspouštěcí příkaz je skript nebo spustitelný soubor, který běží v systému Windows PE před tím, než uživatel vybere pořadí úkolů. Předspouštěcí příkaz může zadat dotaz na proměnnou nebo zobrazit uživateli výzvu k zadání informací a pak ho uložit v prostředí. Použijte objekt COM [TSEnvironment](#bkmk_set-com) ke čtení a zápisu proměnných z předspouštěcího příkazu.

Další informace najdete v tématu [příkazy před zahájením pro médium pořadí úloh](prestart-commands-for-task-sequence-media.md).

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a>Průvodce pořadím úloh

Počínaje verzí 1906 platí, že po výběru pořadí úkolů v okně Průvodce pořadím úloh bude stránka pro úpravu proměnných pořadí úkolů obsahovat tlačítko pro **Úpravy** . K úpravě proměnných můžete použít klávesové zkratky k dispozici. Tato změna pomáhá v případech, kdy myš není k dispozici.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a>Průvodce médii pořadí úloh

Zadejte proměnné pro pořadí úloh spouštěné z média. Při použití média k nasazení operačního systému přidáte proměnné pořadí úkolů a určíte jejich hodnoty při vytváření média. Proměnné a jejich hodnoty jsou uloženy na médiu.  

> [!NOTE]  
> Pořadí úkolů se ukládají na samostatné médium. Všechny ostatní typy médií, jako jsou předzpracovaná média, načítají pořadí úloh z bodu správy.  

Když spouštíte pořadí úkolů z média, můžete přidat proměnnou na stránce **vlastní nastavení** v průvodci.

Místo proměnných pro kolekci nebo pro počítač použijte proměnné pro médium. Pokud je pořadí úkolů spuštěné z média, proměnné pro počítač a pro kolekci se nepoužijí a nepoužívají se.  

> [!TIP]  
> Pořadí úkolů zapíše ID balíčku a Předstartovní příkazový řádek do souboru **CreateTSMedia. log** v počítači, ve kterém je spuštěna konzola Configuration Manager. Tento soubor protokolu obsahuje hodnotu pro všechny proměnné pořadí úkolů. Zkontrolujte tento soubor protokolu a ověřte hodnotu pro proměnné pořadí úkolů.  

Další informace najdete v tématu [Vytvoření média pořadí úkolů](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a>Jak přistupovat k proměnným

Po zadání proměnné a její hodnoty pomocí jedné z metod z předchozí části ji použijte v pořadí úkolů. Například nastavte přístup k výchozím hodnotám pro předdefinované proměnné pořadí úkolů nebo proveďte krok s hodnotou proměnné.  

Pro přístup k proměnným hodnotám v prostředí pořadí úloh použijte následující metody:

- [Použití v kroku](#bkmk_access-step)  
- [Podmínka kroku](#bkmk_access-condition)  
- [Vlastní skript](#bkmk_access-script)  
- [Soubor odpovědí instalačního programu systému Windows](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a>Použití v kroku

Zadejte hodnotu proměnné pro nastavení v kroku pořadí úloh. V editoru pořadí úloh upravte krok a jako hodnotu pole zadejte název proměnné. V části znaky procenta (`%`) vložte název proměnné.

Například použijte název proměnné jako součást pole **příkazový řádek** v kroku **Spustit příkazový řádek** . Následující příkazový řádek zapíše název počítače do textového souboru.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a>Podmínka kroku

Použijte předdefinované nebo vlastní proměnné pořadí úkolů jako součást podmínky pro krok nebo skupinu. Pořadí úkolů vyhodnotí proměnnou hodnoty před spuštěním kroku nebo skupiny.

Chcete-li přidat podmínku, která vyhodnotí hodnotu proměnné, proveďte následující kroky:  

1. V editoru pořadí úloh vyberte krok nebo skupinu, do které chcete podmínku přidat.  

2. Přepněte na kartu **Možnosti** pro krok nebo skupinu. Klikněte na **Přidat podmínku**a vyberte **proměnná pořadí úloh**.  

3. V dialogovém okně **proměnná pořadí úloh** zadejte následující nastavení:  

    - **Proměnná**: název proměnné. Například, `_SMSTSInWinPE`.  

    - **Podmínka**: podmínka pro vyhodnocení hodnoty proměnné. Například je **rovno**.  

    - **Value**(hodnota): hodnota proměnné, která se má ověřit. Například, `false`.  

Tři předchozí příklady tvoří běžnou podmínku pro otestování, jestli je pořadí úkolů spuštěné ze spouštěcí bitové kopie v systému Windows PE:

> **Proměnná pořadí úloh**`_SMSTSInWinPE equals "false"`

Chcete-li nainstalovat existující bitovou kopii operačního systému, přečtěte si tento stav ve skupině **zachycení souborů a nastavení** výchozí šablony pořadí úkolů.

Další informace o podmínkách najdete v tématu [Editor pořadí úloh – podmínky](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a>Vlastní skript

Čtení a zápis proměnných pomocí objektu COM **Microsoft. SMS. TSEnvironment** , když je spuštěno pořadí úloh.

Následující příklad Windows PowerShellu se dotazuje na **_SMSTSLogPath** proměnnou pro získání aktuálního umístění protokolu. Skript zároveň nastaví vlastní proměnnou.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a>Soubor odpovědí instalačního programu systému Windows

Soubor odpovědí instalačního programu systému Windows, který zadáte, může obsahovat vložené proměnné pořadí úkolů. Použijte formulář `%varname%`, kde *název_proměnné* je název proměnné. Krok **nastavit systém Windows a nástroj ConfigMgr** nahrazuje řetězec názvu proměnné pro skutečnou hodnotu proměnné. Tyto vložené proměnné pořadí úkolů se nedají používat v souboru odpovědí Unattend. XML jenom v číselném poli.

Další informace najdete v části [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Viz také

- [Kroky pořadí úkolů](task-sequence-steps.md)

- [Proměnné pořadí úkolů](task-sequence-variables.md)

- [Aspekty plánování pro automatizaci úloh](../plan-design/planning-considerations-for-automating-tasks.md)

- [Editor pořadí úloh](task-sequence-editor.md)
