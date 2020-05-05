---
title: Správa pořadí úkolů
titleSuffix: Configuration Manager
description: Vytváření, úpravy, nasazování, importování a exportování pořadí úloh pro jejich správu a automatizaci úloh ve vašem prostředí.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b38b0c8f28645fa0aae66058b0c93bd8beffc470
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078477"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Správa pořadí úkolů pro automatizaci úloh

*Platí pro: Configuration Manager (Current Branch)*

Pomocí pořadí úkolů můžete automatizovat kroky v prostředí Configuration Manager. Tyto kroky můžou nasadit image operačního systému do cílového počítače, sestavit a zachytit image operačního systému ze sady instalačních souborů operačního systému a zachytit a obnovit informace o stavu uživatele. Pořadí úkolů se nachází v konzole Configuration Manager. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte **pořadí úloh**. Uzel **pořadí úloh** , včetně podsložek, které vytvoříte, se replikuje v rámci hierarchie Configuration Manager. Informace o plánování najdete v tématu [předpoklady plánování pro automatizaci úloh](../plan-design/planning-considerations-for-automating-tasks.md).  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a>Vytvořeny

Pořadí úloh lze vytvořit pomocí průvodce vytvořením pořadí úloh. Pomocí tohoto průvodce lze vytvořit následující typy pořadí úloh:  

- [Pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md): Vytvořte kroky pro instalaci operačního systému. Zahrnuje taky možnosti migrace uživatelských dat, zahrnutí aktualizací softwaru a instalaci aplikací.

- [Pořadí úkolů pro upgrade operačního systému](create-a-task-sequence-to-upgrade-an-operating-system.md): Vytvořte kroky pro upgrade operačního systému. Zahrnuje také možnosti pro zahrnutí aktualizací softwaru a instalaci aplikací.

- [Pořadí úkolů pro zachycení operačního systému](create-a-task-sequence-to-capture-an-operating-system.md): Vytvořte kroky pro sestavení a zachycení operačního systému z referenčního počítače. Před zachycením image můžete zahrnout aktualizace softwaru a instalovat aplikace do referenčního počítače.

- [Pořadí úkolů pro zachycení a obnovení stavu uživatele](create-a-task-sequence-to-capture-and-restore-user-state.md): Přidání kroků do existujícího pořadí úkolů pro zaznamenání a obnovení dat o stavu uživatele.

- [Vlastní pořadí úloh](create-a-custom-task-sequence.md): Tento typ do pořadí úkolů nepřidá žádné kroky. Po vytvoření tohoto pořadí úloh ho upravte a přidejte kroky.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a>Úpravě  

Upravte pořadí úkolů přidáním nebo odebráním kroků, přidáním nebo odebráním skupin nebo změnou pořadí kroků. Další informace najdete v tématu [použití editoru pořadí úloh](../understand/task-sequence-editor.md).

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a>Vlastnosti centra softwaru

Pomocí následujícího postupu můžete nakonfigurovat podrobnosti o pořadí úloh zobrazeném v centru softwaru. Tyto podrobnosti jsou pouze pro informace.  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.  

2. Vyberte pořadí úkolů, které chcete upravit, a vyberte **vlastnosti**.  

3. Na kartě **Obecné** jsou k dispozici následující nastavení pro Centrum softwaru:  

    - **Vyžadováno restartování**: umožňuje uživateli zjistit, zda je během instalace vyžadováno restartování.  

    - **Velikost ke stažení (MB)**: Určuje, kolik megabajtů se zobrazuje v nástroji Software Center pro pořadí úkolů.  

    - **Odhadovaná doba běhu (v minutách)**: Určuje odhadovanou dobu běhu (v minutách), která se zobrazí v centru softwaru pro pořadí úkolů.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a>Rozšířená nastavení

Pomocí následujícího postupu můžete nakonfigurovat chování pořadí úkolů v klientovi Configuration Manager.  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.  

2. Vyberte pořadí úkolů, které chcete upravit, a vyberte **vlastnosti**.  

3. Na kartě **Upřesnit** jsou k dispozici následující nastavení:  

    - **Nejprve spustit jiný program**: tuto možnost vyberte, pokud chcete spustit program v jiném balíčku před spuštěním pořadí úloh. Ve výchozím nastavení je toto políčko zaškrtnuto. Nemusíte samostatně nasazovat program, který zadáte, aby se spouštěl jako první.  

        > [!IMPORTANT]
        > Toto nastavení platí jenom pro pořadí úloh, která běží v plném operačním systému. Pokud pořadí úkolů spustíte pomocí technologie PXE nebo spouštěcího média, Configuration Manager toto nastavení ignoruje.  

        - **Balíček**: vyhledejte balíček, který obsahuje program, který se má spustit před tímto pořadím úloh.  

        - **Program**: Vyberte program, který se má spustit před tímto pořadím úkolů.  

        > [!NOTE]  
        > Pokud se vybraný program v klientovi nepodaří spustit, pořadí úkolů se nespustí. Pokud se vybraný program úspěšně spustí, nespustí se znovu, i když je pořadí úkolů znovu spuštěno na stejném klientovi.  

    - **Potlačit oznámení pořadí úloh**: tuto možnost vyberte, pokud chcete skrýt **nový software je k dispozici** informační zpráva oznámení. V oznamovací oblasti se pořád zobrazuje **Nová ikona softwaru** z centra softwaru. Ve výchozím nastavení je tato možnost zakázána.  

    - **Zakázat toto pořadí úloh v počítačích, kde je nasazena**: Pokud vyberete tuto možnost, Configuration Manager dočasně zakáže všechna nasazení, která obsahují toto pořadí úloh. Odebere také pořadí úloh ze seznamu nasazení, která jsou k dispozici pro spuštění. Pořadí úkolů se nespustí, dokud ho nepovolíte. Ve výchozím nastavení je tato možnost zakázána.  

    - **Maximální povolená doba spuštění**: Určuje maximální dobu v minutách, po kterou se očekává, že se pořadí úkolů v cílovém počítači spustí. Použijte celé číslo, které je větší nebo rovno nule. Ve výchozím nastavení je tato hodnota 120 minut.  

        > [!IMPORTANT]  
        > Pokud používáte časová období údržby pro kolekci, do které nasazujete toto pořadí úloh, může dojít ke konfliktu, pokud je **maximální povolená doba běhu** delší než plánované časové období údržby. Pokud nastavíte maximální dobu běhu na **0**, pořadí úkolů se spustí během časového intervalu pro správu a údržbu. Pokračuje v běhu, dokud se nedokončí nebo neuspěje po zavření okna údržby. V důsledku toho mohou být pořadí úkolů s maximální dobou běhu nastavenou na **hodnotu 0** spouštěny po skončení oken údržby. Pokud nastavíte maximální dobu běhu na určitou dobu (nenulovou), která překračuje délku dostupného časového období údržby, pak se toto pořadí úkolů nespustí. Další informace najdete v tématu [použití časových období údržby](../../core/clients/manage/collections/use-maintenance-windows.md).  

        Pokud nastavíte hodnotu **0**, Configuration Manager vyhodnotí maximální povolenou dobu běhu na **12** hodin (720 minut) pro sledování průběhu. Pořadí úkolů se ale spustí, dokud doba odpočítávání nepřekračuje hodnotu časového intervalu pro správu a údržbu.  

        > [!NOTE]
        > Pokud nepovolíte uživatelům interakci s požadovaným nasazením, při dosažení maximální doby běhu aplikace Configuration Manager zastaví pořadí úkolů. Pokud se samotné pořadí úkolů nezastaví, Configuration Manager zastaví monitorování pořadí úkolů poté, co dosáhne maximální povolené doby běhu.

    - **Použít spouštěcí bitovou kopii**: při spuštění pořadí úkolů použijte vybranou spouštěcí bitovou kopii. Vyberte **Procházet** a vyberte jinou bitovou spouštěcí kopii. Zaškrtnutím této možnosti zakážete použití vybrané spouštěcí image při spuštění pořadí úkolů.  

    - **Toto pořadí úkolů lze spustit na libovolné platformě**: Pokud vyberete tuto možnost, Configuration Manager nekontrolují typ platformy cílového počítače, když je spuštěno pořadí úloh. Tato možnost je ve výchozím nastavení zaškrtnutá.  

    - **Toto pořadí úloh lze spustit pouze na zadaných klientských platformách**: Tato možnost určuje procesory, verze operačního systému a aktualizace Service Pack, na kterých lze pořadí úkolů Spustit. Když vyberete tuto možnost, vyberte ze seznamu alespoň jednu platformu. Ve výchozím nastavení nejsou vybrány žádné platformy. Configuration Manager tyto informace používá, když se vyhodnotí, které cílové počítače v kolekci obdrží nasazené pořadí úkolů.  

        > [!NOTE]  
        > Když spouštíte pořadí úkolů ze spouštěcího média nebo PXE, tato možnost ignoruje Configuration Manager. Pořadí úkolů se spustí, jako kdyby byla vybrána možnost **Tento program může běžet na libovolné platformě** .  

## <a name="high-impact-settings"></a>Nastavení s vysokým dopadem

Nakonfigurujte pořadí úkolů s vysokým dopadem a přizpůsobte zprávy, které uživatelé obdrží při spuštění pořadí úkolů.

> [!WARNING]
> Pokud používáte nasazení PXE a nakonfigurujete hardware zařízení se síťovým adaptérem jako prvním spouštěcím zařízením, můžou tato zařízení automaticky spustit pořadí úloh nasazení operačního systému bez zásahu uživatele. Ověřování nasazení nespravuje tuto konfiguraci. I když tato konfigurace může zjednodušit proces a omezit interakci s uživatelem, umístí zařízení s větším rizikem na nechtěné obnovení obrazu.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Nastavení pořadí úkolů jako vysoce ovlivněné pořadí úkolů

Následující postup slouží k nastavení pořadí úkolů jako vysokého dopadu.

> [!NOTE]  
> Pořadí úkolů, které splňuje určité podmínky, je automaticky definováno jako vysoce ovlivněno. Další informace najdete v tématu [Správa nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.  

2. Vyberte pořadí úkolů, které chcete upravit, a vyberte **vlastnosti**.  

3. Na kartě **oznámení uživateli** vyberte **Toto pořadí úkolů s vysokým dopadem**.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Vytvoření vlastního oznámení pro nasazení s vysokým rizikem

Pomocí následujícího postupu můžete vytvořit vlastní oznámení pro vysoce ovlivněná nasazení.

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.  

2. Vyberte pořadí úkolů, které chcete upravit, a vyberte **vlastnosti**.  

3. Na kartě **oznámení uživateli** vyberte **použít vlastní text**.  

    > [!NOTE]
    > Text oznámení uživateli lze nastavit pouze tehdy, když vyberete možnost, jedná **se o vysoce ovlivněné pořadí úkolů**.  

4. Nakonfigurujte tahle nastavení:  

    > [!Note]  
    > Každé textové pole má maximální povolený limit 255 znaků.  

    - **Text titulku oznámení uživateli**: Určuje modrý text, který se zobrazí v oznámení o uživateli centra softwaru. Například ve výchozím oznámení uživateli obsahuje tato část "potvrzení, že chcete upgradovat operační systém v tomto počítači."  

    - **Text zprávy oznámení uživateli**: Existují tři textová pole, která poskytují text vlastního oznámení. Všechna textová pole vyžadují, abyste přidali text.  

        - First text box: Určuje hlavní text textu, který obvykle obsahuje pokyny pro uživatele. Například ve výchozím oznámení uživateli obsahuje tato část "upgrade operačního systému na určitou dobu a počítač se může několikrát restartovat."  

        - Druhé textové pole: Určuje tučný text v hlavním těle textu. Například ve výchozím oznámení uživateli Tato část obsahuje "tento místní upgrade nainstaluje nový operační systém a automaticky migruje vaše aplikace, data a nastavení."  

        - Třetí textové pole: Určuje poslední řádek textu pod tučným textem. Například ve výchozím oznámení uživateli Tato část obsahuje "kliknutím na Instalovat zahájíte. V opačném případě klikněte na tlačítko Storno. "  

#### <a name="example"></a>Příklad

Řekněme, že ve vlastnostech nakonfigurujete následující vlastní oznámení.

![Přizpůsobená karta oznámení uživateli vlastností pořadí úloh](../media/user-notification.png)

Následující zpráva oznámení se zobrazí, když koncový uživatel otevře instalaci z centra softwaru.

![Přizpůsobené oznámení pořadí úkolů koncovému uživateli z centra softwaru](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a>Vylepšení výkonu pro schémata napájení

<!--3555926-->

Počínaje verzí 1910 můžete nyní spustit pořadí úkolů s vysokým výkonem schématu napájení. Tato možnost vylepšuje celkovou rychlost pořadí úkolů. Nakonfiguruje Windows tak, aby používal integrované schéma napájení s vysokým výkonem, které zajišťuje maximální výkon na úkor vyšší spotřeby energie. Tato možnost je ve výchozím nastavení zapnutá pro nové pořadí úkolů.

Když se pořadí úkolů spustí, ve většině případů zaznamenává aktuálně povolené schéma napájení. Pak přepne aktivní schéma napájení do výchozího **vysoce výkonného** plánu Windows. Pokud pořadí úkolů restartuje počítač, tento postup se opakuje. Na konci pořadí úkolů obnoví schéma napájení uloženou hodnotu. Tato funkce funguje v systémech Windows i Windows PE, ale nemá žádný vliv na virtuální počítače.

- Pokud se pořadí úkolů spustí v systému Windows PE, pořadí úkolů nebude nahrávat aktuálně povolené schéma napájení pro pozdější opakované použití.

- Pořadí úloh nasazení operačního systému, které obnovuje počítač (vymazání a zatížení), nezachovává nastavení schématu napájení starého operačního systému. Na konci pořadí úkolů se obnoví výchozí schéma **vyváženého** napájení.

> [!Important]
> Pokud chcete tuto novou funkci Configuration Manager využít, po aktualizaci lokality aktualizujte klienty na nejnovější verzi. Aktualizujte také spouštěcí image tak, aby obsahovaly nejnovější součásti klienta. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .

1. Vytvořte nebo zvolte existující pořadí úloh a pak vyberte **vlastnosti**.

1. Přepněte na kartu **výkon** .

1. Povolte možnost **Spustit jako schéma napájení s vysokým výkonem**.

> [!Warning]
> Buďte opatrní s tímto nastavením na hardwaru s nízkým výkonem. Provoz intenzivních systémových operací po delší dobu může být náročné na hardware nižší úrovně. Konkrétní pokyny vám poskytne výrobce hardwaru.

### <a name="known-issue"></a>Známý problém

<!-- 5554928 -->

Pro zajištění vysokého výkonu je potřeba vytvořit nové nasazení pořadí úloh a povolit nebo zakázat toto nastavení. Nové nastavení se zobrazí ve stávajících nasazeních, ale nevztahuje se na něj.<!-- SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a>Distribuovat odkazovaný obsah  

Předtím, než klienti spustí pořadí úloh, které odkazuje na obsah, distribuujte tento obsah do distribučních bodů. Kdykoli můžete vybrat pořadí úloh a distribuovat jeho obsah za účelem sestavení nového seznamu referenčních balíčků pro distribuci. Pokud provedete změny v pořadí úkolů s aktualizovaným obsahem, znovu distribuujte obsah před tím, než bude dostupný pro klienty. Obsah, který je odkazován pořadím úloh, můžete distribuovat pomocí následujícího postupu.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Proces distribuce odkazovaného obsahu do distribučních bodů  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

2. V seznamu **Pořadí úloh** vyberte pořadí úloh, které chcete distribuovat.  

3. Na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte možnost **distribuovat obsah**. Tato akce spustí Průvodce distribucí obsahu.  

4. Na stránce **Obecné** ověřte, že je pro distribuci vybráno správné pořadí úloh.  

5. Na stránce **obsah** ověřte obsah, který chcete distribuovat, jako je například spouštěcí bitová kopie, na kterou odkazuje pořadí úkolů.  

6. Na stránce **cílové umístění obsahu** určete kolekce, distribuční bod nebo skupinu distribučních bodů, ve kterých chcete distribuovat obsah pořadí úloh.  

    > [!IMPORTANT]  
    > Pokud pořadí úloh, které jste vybrali, odkazuje na obsah, který je již distribuován do konkrétního distribučního bodu, průvodce tento distribuční bod neuvádí.  

7. Dokončete průvodce.  

Můžete také připravit obsah, na který se odkazuje v pořadí úkolů. Configuration Manager vytvoří komprimovaný soubor připraveného obsahu, který obsahuje soubory, přidružené závislosti a přidružená metadata pro vybraný obsah. Pak ručně naimportujete obsah ze serveru lokality, sekundární lokality nebo distribučního bodu. Další informace o tom, jak předem připravit soubory obsahu, najdete v tématu [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a>Nasazení  

Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a>Export a import  

Exportovat a importovat pořadí úloh s jejich souvisejícími objekty nebo bez nich. Tento odkazovaný obsah obsahuje následující objekty:  

- Image operačního systému  
- Spouštěcí image  
- Balíčky, jako je například klientský instalační balíček  
- Balíčky ovladačů  
- Aplikace se závislostmi  

Při exportu a importu pořadí úloh Vezměte v úvahu následující body:  

- Configuration Manager neexportují hesla v pořadí úkolů. Pokud exportujete a importujete pořadí úloh, které obsahuje hesla, upravte importované pořadí úkolů tak, aby znovu zadala hesla. Projděte si následující kroky, které mohou zahrnovat heslo:  

  - [Připojit k doméně nebo pracovní skupině](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Připojit k síťové složce](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Spustit příkazový řádek](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- Když exportujete pořadí úkolů s krokem **nastavit dynamické proměnné** , Configuration Manager neexportují hodnoty pro proměnné, které nakonfigurujete s nastavením **tajné hodnoty** . Po importu pořadí úkolů znovu zadejte hodnoty těchto proměnných.  

- Pokud máte více primárních lokalit, importujte pořadí úloh v lokalitě centrální správy.  

### <a name="process-to-export-task-sequences"></a>Proces exportu pořadí úloh  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

2. V seznamu **Pořadí úloh** vyberte pořadí úloh, která chcete exportovat. Pokud vyberete více než jedno pořadí úloh, budou všechny uloženy v jednom souboru exportu.  

3. Na kartě **Domů** na pásu karet ve skupině **pořadí úloh** vyberte **exportovat**. Tato akce spustí Průvodce exportem pořadí úloh.  

4. Na stránce **Obecné** určete následující nastavení:  

    - **Soubor**: zadejte umístění a název souboru exportu. Pokud zadáte přímo název souboru, nezapomeňte k němu zahrnout rovněž příponu .zip. Pokud k souboru exportu procházíte, tuto příponu automaticky přidá průvodce.  

    - Pokud nechcete exportovat závislosti pořadí úloh, zrušte výběr možnosti **exportu všech závislostí pořadí úloh**. Standardně průvodce hledá všechny související objekty a exportuje je s pořadím úloh. Tyto závislosti zahrnují všechny pro aplikace.  

    - Pokud nechcete kopírovat obsah ze zdroje balíčku do umístění exportu, zrušte výběr možnosti **exportovat veškerý obsah pro vybraná pořadí úloh a závislosti**. Pokud vyberete tuto možnost, Průvodce importem pořadí úloh použije jako nové zdrojové umístění balíčku cestu pro import.  

    - **Komentáře správce**: přidejte popis pořadí úloh k exportu.  

5. Dokončete průvodce.  

Průvodce vytváří následující výstupní soubory:  

- Pokud neexportujete obsah: soubor. zip.  

- Pokud exportujete obsah: soubor .zip a složka s názvem *export*_files, kde *export* je název souboru .zip, který obsahuje exportovaný obsah.  

Pokud při exportu pořadí úloh zahrnete obsah, Nezapomeňte zkopírovat soubor. zip a složku *export*_files, jinak se import nezdařil.  

### <a name="process-to-import-task-sequences"></a>Proces importu pořadí úloh  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **importovat pořadí úloh**. Tato akce spustí Průvodce importem pořadí úloh.  

3. Na stránce **Obecné** na pásu karet zadejte exportovaný soubor. zip.  

4. Na stránce **Obsah souboru** vyberte akci, kterou pro každý importovaný objekt požadujete. Tato stránka zobrazuje všechny objekty, které Configuration Manager nalezeny pro import.  

    - Pokud objekt nikdy nebyl importován, vyberte možnost **Vytvořit nový**.  

    - Pokud objekt již dříve importován byl, vyberte jednu z následujících akcí:  

        - **Ignorovat duplicity** (výchozí): Tato akce neimportuje objekt. Místo toho průvodce spojí stávající objekty se pořadím úkolů.  

        - **Přepsat**: Tato akce přepíše stávající objekt importovaným objektem. Pro aplikace můžete přidat revizi pro aktualizování stávající aplikace nebo vytvoření nové.  

5. Dokončete průvodce.  

Po importování pořadí úkolů toto pořadí upravte a zadejte všechna hesla, která byla zahrnuta do původního pořadí úkolů. Z bezpečnostních důvodů se hesla exportují.  

## <a name="return-to-previous-page-on-failure"></a>Vrátit se na předchozí stránku při selhání

Když spustíte pořadí úloh a dojde k selhání, můžete se vrátit na předchozí stránku průvodce pořadím úloh. V předchozích verzích Configuration Manager bylo nutné restartovat pořadí úkolů, pokud došlo k selhání. Použijte tlačítko **Předchozí** v následujících scénářích:

- Když se počítač spustí v prostředí Windows PE, může se dialogové okno spuštění pořadí úkolů zobrazit předtím, než bude pořadí úkolů k dispozici. Když v tomto scénáři vyberete další, zobrazí se poslední stránka v pořadí úkolů se zprávou, že nejsou k dispozici žádná pořadí úkolů. Teď můžete vybrat **Předchozí** a znovu vyhledávat dostupná pořadí úkolů. Tento postup můžete opakovat až do chvíle, kdy je pořadí úkolů k dispozici.  

- Když spustíte pořadí úloh, ale v distribučních bodech ještě nejsou k dispozici závislé balíčky obsahu, pořadí úkolů se nezdařilo. Pokud se zatím chybějící obsah nedistribuuje, distribuujte ho hned teď. Nebo počkejte, až bude obsah k dispozici v distribučních bodech. Pak vyberte možnost **Předchozí** , pokud chcete, aby pořadí úkolů znovu vyhledalo obsah.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a>Kolekce a proměnné zařízení

Pro počítače a kolekce můžete definovat vlastní proměnné pořadí úkolů. Proměnné definované pro počítač jsou označovány jako proměnné pořadí úkolů pro počítač. Proměnné definované pro kolekci jsou odkazovány jako proměnné pořadí úkolů pro kolekci. Další informace najdete v tématu [kolekce a proměnné zařízení](../understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a>Další akce  

Pořadí úkolů můžete spravovat pomocí dalších akcí, když vyberete pořadí úkolů.  

### <a name="edit"></a>Upravit

Další informace najdete v tématu [použití editoru pořadí úloh](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Povolení

Povolí pořadí úkolů, aby je klienti mohli spustit. Pořadí úkolů nemusíte po jeho povolení znovu nasazovat.  

### <a name="disable"></a>Zakázat

Zakáže pořadí úkolů, aby se nemohlo spustit na počítačích. Můžete nasadit zakázané pořadí úloh, ale počítače nespustí pořadí úkolů, dokud je nepovolíte.  

### <a name="export"></a>Export

Další informace najdete v tématu [Export a import pořadí úkolů](#BKMK_ExportImport).

### <a name="copy"></a>Kopírovat

Zhotoví kopii vybraného pořadí úloh. Tato akce je užitečná pro vytvoření nového pořadí úloh, které je založené na stávajícím pořadí úkolů.

Když zhotovíte kopii pořadí úkolů ve složce, kopie je uvedena v této složce do doby, než aktualizujete uzel pořadí úkolů. Po aktualizování se kopie objeví v kořenové složce.  

### <a name="refresh"></a>Obnovení

Aktualizuje podrobnosti pro vybrané pořadí úkolů.

### <a name="delete"></a>Odstranit

Odstraní vybrané pořadí úkolů.

### <a name="create-phased-deployment"></a>Vytvořit dvoufázové nasazení

Další informace najdete v tématu [Vytvoření dvoufázové nasazení](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Nasazení

Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>Distribuovat obsah

Spustí Průvodce distribucí obsahu, který odešle odkazovaný obsah do distribučních bodů.

### <a name="create-prestaged-content-file"></a>Vytvořit soubor připraveného obsahu

Spouští nástroj Vytvořit Průvodce souborem připraveného obsahu, který slouží k přípravě obsahu pořadí úkolů. Informace o vytváření souboru připraveného obsahu naleznete v části [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### <a name="move"></a>Přesunout

Přesune vybrané pořadí úkolů do jiné složky v uzlu **pořadí úloh** .

### <a name="set-security-scopes"></a>Nastavit rozsahy zabezpečení

Vyberte obory zabezpečení pro vybrané pořadí úkolů. Další informace najdete v tématu [Obory zabezpečení](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Vlastnosti

Další informace najdete v tématech [Konfigurace vlastností centra softwaru](#bkmk_prop-general) a [Konfigurace pokročilých nastavení pořadí úloh](#bkmk_prop-advanced).

### <a name="view"></a>Zobrazit

<!--3633146-->
Počínaje verzí 1902 je výchozí akce **zobrazení** v pořadí úkolů výchozí. Tato akce vám umožní zobrazit kroky pořadí úloh bez uzamčení pro úpravy. Další informace najdete v tématu [použití editoru pořadí úloh](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Viz také

- [Scénáře nasazení podnikových operačních systémů](scenarios-to-deploy-enterprise-operating-systems.md)

- [Použití editoru pořadí úloh](../understand/task-sequence-editor.md)

- [Nasazení pořadí úkolů](deploy-a-task-sequence.md)

- [Kroky pořadí úkolů](../understand/task-sequence-steps.md)

- [Kolekce a proměnné zařízení](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Vytvořit dvoufázové nasazení](create-phased-deployment-for-task-sequence.md)
