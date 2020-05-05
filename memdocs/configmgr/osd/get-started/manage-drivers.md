---
title: Správa ovladačů
titleSuffix: Configuration Manager
description: Pomocí katalogu ovladačů Configuration Manager importujte ovladače zařízení, ovladače skupiny v balíčcích a distribuujte tyto balíčky do distribučních bodů.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724122"
---
# <a name="manage-drivers-in-configuration-manager"></a>Správa ovladačů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager poskytuje katalog ovladačů, který můžete použít ke správě ovladačů zařízení systému Windows ve vašem prostředí Configuration Manager. Pomocí katalogu ovladačů můžete importovat ovladače zařízení do Configuration Manager, seskupovat je do balíčků a distribuovat tyto balíčky do distribučních bodů. Ovladače zařízení lze použít při instalaci úplného operačního systému do cílového počítače a při použití prostředí Windows PE ve spouštěcí imagi. Ovladače zařízení systému Windows se skládají z souboru INF (Setup Information) a všech dalších souborů, které jsou nutné k podpoře zařízení. Když nasadíte operační systém, Configuration Manager získá informace o hardwaru a platformě zařízení z jeho souboru INF. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a>Kategorie ovladačů

Když importujete ovladače zařízení, můžete je zařadit do kategorií. Kategorie ovladačů zařízení pomáhají seskupit podobně používané ovladače v katalogu. Nastavte například všechny ovladače zařízení síťového adaptéru na konkrétní kategorii. Když potom vytvoříte pořadí úkolů, které zahrnuje krok [automaticky použít ovladače](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) , určete kategorii ovladačů zařízení. Configuration Manager pak vyhledá hardware a vybere z této kategorie příslušné ovladače, které se mají instalační program systému Windows použít.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a>Balíčky ovladačů

Seskupení podobných ovladačů zařízení v balíčcích vám umožní zjednodušit nasazení operačního systému. Můžete například vytvořit balíček ovladačů pro každého výrobce počítačů ve vaší síti. Balíček ovladačů můžete vytvořit při importu ovladačů do katalogu ovladačů přímo v uzlu **balíčky ovladačů** . Po vytvoření balíčku ovladačů ho distribuujte do distribučních bodů. Pak Configuration Manager klientské počítače mohou ovladače instalovat podle potřeby. 

Vezměte v úvahu následující body:  

- Když vytváříte balíček ovladačů, zdrojové umístění balíčku musí ukazovat na prázdnou sdílenou síťovou složku, kterou nepoužívá jiný balíček ovladačů. Poskytovatel serveru SMS musí mít oprávnění k **úplnému řízení** pro toto umístění.  

- Když přidáte ovladače zařízení do balíčku ovladačů, Configuration Manager ho zkopírovat do zdrojového umístění balíčku. Můžete přidat do balíčku ovladačů pouze ovladače zařízení, které jste naimportovali a které jsou povoleny v katalogu ovladačů.  

- Můžete zkopírovat podmnožinu ovladačů zařízení z existujícího balíčku ovladačů. Nejprve vytvořte nový balíček ovladačů. Pak přidejte podmnožinu ovladačů zařízení do nového balíčku a potom distribuujte nový balíček do distribučního bodu.  

- Pokud instalujete ovladače pomocí pořadí úkolů, vytvářejte balíčky ovladačů, které obsahují míň než 500 ovladačů zařízení.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a>Vytvoření balíčku ovladačů  

> [!IMPORTANT]  
> Chcete-li vytvořit balíček ovladačů, je nutné mít prázdnou síťovou složku, kterou nepoužívá jiný balíček ovladačů. Ve většině případů vytvořte novou složku před zahájením tohoto postupu.  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **operační systémy**a potom vyberte uzel **balíčky ovladačů** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit balíček ovladačů**.  

3. Zadejte popisný **název** balíčku ovladačů.  

4. Zadejte volitelný **Komentář** k balíčku ovladačů. Tento popis slouží k zadání informací o obsahu nebo účelu balíčku ovladačů.  

5. V poli **Cesta** zadejte prázdnou zdrojovou složku pro umístění balíčku ovladačů. Každý balíček ovladačů musí používat unikátní složku. Tato cesta je povinná jako síťové umístění.  

   > [!IMPORTANT]  
   > Účet serveru lokality musí mít oprávnění k **úplnému řízení** pro zadanou zdrojovou složku.  

Nový balíček ovladačů neobsahuje žádné ovladače. Dalším krokem je přidání ovladačů do balíčku.  

Pokud uzel **Balíčky ovladačů** obsahuje více balíčků, můžete do uzlu přidat složky a rozčlenit balíčky do logických skupin.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Další akce s balíčky ovladačů  

Když vyberete jeden nebo více balíčků ovladačů z uzlu **balíčky ovladačů** , můžete provádět další akce, které vám umožní spravovat balíčky ovladačů. 


#### <a name="create-prestage-content-file"></a>Vytvořit soubor připraveného obsahu
Vytvoří soubory, které můžete použít k ručnímu importu obsahu a přidružených metadat. Připravený obsah používejte v případech, kdy máte malou šířku pásma sítě mezi serverem lokality a distribučními body, v nichž je uložen balíček ovladačů.

#### <a name="delete"></a>Odstranit
Odebere balíček ovladačů z uzlu **Balíček ovladačů**.

#### <a name="distribute-content"></a>Distribuovat obsah
Distribuuje balíček ovladačů do distribučních bodů, skupin distribučních bodů a skupin distribučních bodů přidružených ke kolekcím.

#### <a name="manage-access-accounts"></a>Správa účtů pro přístup
Umožňuje přidat, upravit nebo odebrat přístupové účty pro balíček ovladačů.

Další informace o účtech pro přístup k balíčkům najdete [v tématu účty používané v Configuration Manager](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Přesunout
Přesune balíček ovladačů do jiné složky v uzlu **Balíčky ovladačů** .

#### <a name="update-distribution-points"></a>Aktualizovat distribuční body
Aktualizuje balíček ovladačů zařízení ve všech distribučních bodech, v nichž je uložen. Tato akce zkopíruje pouze obsah, který byl od poslední distribuce změněn.

#### <a name="properties"></a>Vlastnosti
Otevře dialogové okno **vlastnosti** . Zkontrolujte a změňte obsah a vlastnosti ovladače. Můžete například změnit název a popis ovladače, povolit nebo zakázat a určit, na kterých platformách lze spustit. 

<!--3607716, fka 1358270-->
Počínaje verzí 1810 mají balíčky ovladačů pole metadat pro **výrobce** a **model**. Pomocí těchto polí můžete označit balíčky ovladačů informacemi, které vám pomůžou všeobecně údržbu, nebo identifikovat staré a duplicitní ovladače, které můžete odstranit. Na kartě **Obecné** vyberte v rozevíracích seznamech existující hodnotu nebo zadejte řetězec pro vytvoření nové položky.

V uzlu **balíčky ovladačů** se tato pole zobrazují v seznamu jako **výrobce ovladače** a sloupce **modelu ovladače** . Lze je také použít jako kritérium hledání.

Od verze 1906 použijte tyto atributy k předběžné mezipaměti obsahu v klientovi. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Ovladače zařízení

Do cílových počítačů můžete nainstalovat ovladače, aniž byste je museli zahrnout do nasazené image operačního systému. Configuration Manager poskytuje katalog ovladačů, který obsahuje odkazy na všechny ovladače, které naimportujete do Configuration Manager. Katalog ovladačů se nachází v pracovním prostoru **Softwarová knihovna** a tvoří ho dva uzly: **Ovladače** a **Balíčky ovladačů**. Uzel **ovladače** obsahuje seznam všech ovladačů, které jste do katalogu ovladačů naimportovali.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Import ovladačů zařízení do katalogu ovladačů  

Než budete moct použít ovladač při nasazení operačního systému, naimportujte ho do katalogu ovladačů. Pokud je chcete lépe spravovat, importujte jenom ovladače, které plánujete nainstalovat, jako součást nasazení operačního systému. V katalogu si můžete uložit více verzí ovladačů, abyste měli snadný způsob, jak upgradovat existující ovladače při změně požadavků na hardwarové zařízení ve vaší síti.  

V rámci procesu importu ovladače zařízení Configuration Manager přečte následující vlastnosti ovladače:
- Poskytovatel
- Třída
- Verze
- Podpis
- Podporovaný hardware
- Podporované informace o platformě

Ve výchozím nastavení se ovladač jmenuje po prvním hardwarovém zařízení, které podporuje. Ovladač zařízení můžete přejmenovat později. Seznam podporovaných platforem vychází z informací v souboru INF ovladače. Vzhledem k tomu, že přesnost těchto informací se může lišit, ručně ověřte, zda je ovladač podporován po importu do katalogu.  

Po importu ovladačů zařízení do katalogu je přidejte do balíčků ovladačů nebo spouštěcích bitových kopií.  

> [!IMPORTANT]  
> Ovladače zařízení není možné importovat přímo do podsložky uzlu **ovladače** . Pokud chcete importovat ovladač zařízení do podsložky, importujte ho nejprve do uzlu **Ovladač** a potom ho přesuňte do požadované podsložky.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Postup importu ovladačů zařízení systému Windows do katalogu ovladačů  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **operační systémy**a vyberte uzel **ovladače** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **importovat ovladač** a spusťte **Průvodce importem nového ovladače**.  

3. Na stránce **najít ovladač** určete následující možnosti:  

    - **Importovat všechny ovladače v následující cestě sítě (UNC)**: Pokud chcete importovat všechny ovladače zařízení do určité složky, zadejte její síťovou cestu. Například: `\\servername\share\folder`.  

        > [!NOTE]  
        > Pokud je k dispozici hodně podsložek a mnoho souborů INF ovladačů, tento proces může trvat dlouho.  

    - **Importovat konkrétní ovladač**: Pokud chcete ze složky importovat konkrétní ovladač, zadejte síťovou cestu k souboru INF ovladače zařízení systému Windows.  

    - **Zadejte možnost pro duplicitní ovladače**: Vyberte způsob, jakým má Configuration Manager spravovat kategorie ovladačů při importu duplicitního ovladače zařízení.  
        - **Importovat ovladač a připojit novou kategorii k existujícím kategoriím**  
        - **Importovat ovladač a zachovat existující kategorie**  
        - **Importovat ovladač a přepsat existující kategorie**  
        - **Neimportovat ovladač**  

    > [!IMPORTANT]  
    > Při importu ovladačů musí mít server lokality ke složce oprávnění ke **čtení** , jinak nebude import úspěšný.  

4. Na stránce **Podrobnosti o ovladači** určete následující možnosti:  

    - **Skrýt ovladače, které nejsou v třídě úložiště nebo sítě (pro spouštěcí image)**: pomocí tohoto nastavení můžete zobrazit jenom ovladače úložiště a sítě. Tato možnost skryje další ovladače, které nejsou obvykle potřeba pro spouštěcí image, jako je ovladač videa nebo modemu.  

    - **Skrýt ovladače, které nejsou digitálně podepsané**: Microsoft doporučuje používat jenom ovladače, které jsou digitálně podepsané.  

    - V seznamu ovladačů vyberte ovladače, které chcete importovat do katalogu ovladačů.  

    - **Povolit tyto ovladače a dovolit počítačům jejich instalaci**: Tímto nastavením povolíte instalaci ovladačů zařízení do počítače. Tato možnost je ve výchozím nastavení povolená.  

        > [!IMPORTANT]  
        > Pokud ovladač zařízení způsobuje problémy nebo pokud chcete instalaci ovladače zařízení pozastavit, zakažte ho během importu. Ovladače můžete zakázat i po jejich importu.  

    - Chcete-li přiřadit ovladače zařízení k administrativní kategorii pro účely filtrování, jako jsou například "stolní počítače" nebo "notebooky", vyberte **kategorie**. Pak zvolte existující kategorii nebo vytvořte novou. Pomocí kategorií můžete řídit, které ovladače zařízení se použijí pro krok pořadí úkolů [automaticky použít ovladače](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) .  

5. Na stránce **Přidat ovladač k balíčkům** vyberte, jestli se mají ovladače přidat do balíčku.  

    - Vyberte balíčky ovladačů použité k distribuci ovladačů zařízení.  

        V případě potřeby vyberte **nový balíček** a vytvořte nový balíček ovladačů. Když vytváříte nový balíček ovladačů, zajistěte sdílenou síťovou složku, kterou nepoužívají jiné balíčky ovladačů.  

    - Pokud balíček již byl distribuován do distribučních bodů, v dialogovém okně vyberte možnost **Ano** , pokud chcete aktualizovat spouštěcí bitové kopie v distribučních bodech. Ovladače zařízení nelze používat, dokud nejsou distribuovány do distribučních bodů. Pokud vyberete **ne**, spusťte před použitím spouštěcí image akci **Aktualizovat distribuční bod** . Pokud balíček ovladače nikdy nebyl distribuován, je nutné použít akci **distribuovat obsah** v uzlu **balíčky ovladačů** .  

6. Na stránce **Přidat ovladač k bitovým spouštěcím kopiím** vyberte, jestli chcete ovladače zařízení přidat do existujících spouštěcích imagí.  

    > [!NOTE]  
    > Do spouštěcích imagí přidejte pouze ovladače úložiště a sítě.  

    - V dialogovém okně vyberte **Ano** , pokud chcete aktualizovat spouštěcí bitové kopie v distribučních bodech. Ovladače zařízení nelze používat, dokud nejsou distribuovány do distribučních bodů. Pokud vyberete **ne**, spusťte před použitím spouštěcí image akci **Aktualizovat distribuční bod** . Pokud balíček ovladače nikdy nebyl distribuován, je nutné použít akci **distribuovat obsah** v uzlu **balíčky ovladačů** .  

    - Configuration Manager vás upozorní, pokud architektura jednoho nebo více ovladačů neodpovídá architektuře spouštěcích imagí, které jste vybrali. Pokud se neshodují, vyberte **OK**. Vraťte se na stránku **Podrobnosti o ovladači** a zrušte označení ovladačů, které neodpovídají architektuře vybrané spouštěcí image. Pokud jste třeba vybrali spouštěcí image x64 a x86, všechny ovladače musí podporovat obě tyto architektury. Pokud jste vybrali spouštěcí image x64, všechny ovladače musí architekturu x64.  

        > [!NOTE]  
        > - Architektura je založená na architektuře, která je uvedena v souboru INF od výrobce.  
        > - Pokud ovladač hlásí, že podporuje obě architektury, můžete ho naimportovat do obou spouštěcích imagí.  

    - Configuration Manager vás upozorní, když přidáváte ovladače zařízení, které nejsou ovladači sítě nebo úložiště, do spouštěcí bitové kopie. Ve většině případů nejsou pro spouštěcí image nutné. Vyberte **Ano** , pokud chcete přidat ovladače do spouštěcí image, nebo **ne** , chcete-li se vrátit a změnit výběr ovladače.  

    - Configuration Manager vás upozorní, pokud některé z vybraných ovladačů nejsou správně digitálně podepsány. Pokračujte výběrem možnosti **Ano** a kliknutím na tlačítko **ne** se vraťte zpět a proveďte změny v výběru ovladače.  

7. Dokončete průvodce.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Správa ovladačů zařízení v balíčku ovladačů  

Podle následujících postupů lze upravovat balíčky ovladačů a bitové spouštěcí kopie. Pokud chcete přidat nebo odebrat ovladač, nejdřív ho vyhledejte v uzlu **ovladače** . Pak upravte balíčky nebo spouštěcí bitové kopie, ke kterým je vybraný ovladač přidružen.  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **operační systémy**a potom vyberte uzel **ovladače** .  

2. Vyberte ovladače zařízení, které chcete přidat do balíčku ovladačů.  

3. Na kartě **Domů** na pásu karet ve skupině **ovladač** vyberte **Upravit**a pak zvolte **balíčky ovladačů**.  

4. Chcete-li přidat ovladač zařízení, zaškrtněte políčka u balíčků ovladačů, do nichž chcete ovladače zařízení přidat. Chcete-li odebrat ovladač zařízení, zrušte zaškrtnutí políček u balíčků ovladačů, z nichž chcete ovladače zařízení odebrat.  

    Pokud přidáváte ovladače zařízení, které jsou přidružené k balíčkům ovladačů, můžete volitelně vytvořit nový balíček. Vyberte **nový balíček**. otevře se dialogové okno **nový balíček ovladačů** .  

5. Pokud balíček již byl distribuován do distribučních bodů, v dialogovém okně vyberte možnost **Ano** , pokud chcete aktualizovat spouštěcí bitové kopie v distribučních bodech. Ovladače zařízení nelze používat, dokud nejsou distribuovány do distribučních bodů. Pokud vyberete **ne**, spusťte před použitím spouštěcí image akci **Aktualizovat distribuční bod** . Pokud balíček ovladače nikdy nebyl distribuován, je nutné použít akci **distribuovat obsah** v uzlu **balíčky ovladačů** . Předtím, než budou ovladače dostupné, musíte aktualizovat balíček ovladačů na distribučních bodech.  

    Po dokončení vyberte **OK** .  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Správa ovladačů zařízení ve spouštěcí imagi  

Můžete přidat ke spouštěcím bitovým kopiím ovladačů zařízení systému Windows, které byly naimportovány do katalogu. Při přidávání ovladačů zařízení do spouštěcí bitové kopie postupujte podle následujících pokynů:  

- Do spouštěcích imagí přidejte pouze ovladače úložiště a sítě. Jiné typy ovladačů nejsou většinou potřeba v prostředí Windows PE. Ovladače, které nejsou vyžadovány zbytečně, zvyšují velikost spouštěcí bitové kopie.  

- Do spouštěcí image přidávejte jenom ovladače zařízení pro Windows 10. Požadovaná verze prostředí Windows PE vychází z Windows 10.  

- Ujistěte se, že používáte správný ovladač zařízení pro architekturu spouštěcí bitové kopie. Nepřidávejte do spouštěcí bitové kopie x64 ovladač zařízení x86.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Postup úpravy ovladačů zařízení přidružených ke spouštěcí imagi  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **operační systémy**a potom vyberte uzel **ovladače** .  

2. Vyberte ovladače zařízení, které chcete přidat do balíčku ovladačů.  

3. Na kartě **Domů** na pásu karet ve skupině **ovladač** vyberte **Upravit**a pak zvolte **spouštěcí bitové kopie**.  

4. Chcete-li přidat ovladač zařízení, zaškrtněte políčka u spouštěcích bitových kopií, do nichž chcete ovladače zařízení přidat. Chcete-li odebrat ovladač zařízení, zrušte zaškrtnutí políček u spouštěcích bitových kopií, z nichž chcete ovladače zařízení odebrat.  

5. Pokud nechcete aktualizovat distribuční body, ve kterých je spouštěcí bitová kopie uložená, zrušte zaškrtnutí políčka po **dokončení aktualizovat distribuční body** . Ve výchozím nastavení se distribuční body aktualizují po dokončení aktualizace spouštěcí bitové kopie.  

    - V dialogovém okně vyberte **Ano** , pokud chcete aktualizovat spouštěcí bitové kopie v distribučních bodech. Ovladače zařízení nelze používat, dokud nejsou distribuovány do distribučních bodů. Pokud vyberete **ne**, spusťte před použitím spouštěcí image akci **Aktualizovat distribuční bod** . Pokud balíček ovladače nikdy nebyl distribuován, je nutné použít akci **distribuovat obsah** v uzlu **balíčky ovladačů** .  

    - Configuration Manager vás upozorní, pokud architektura jednoho nebo více ovladačů neodpovídá architektuře spouštěcích imagí, které jste vybrali. Pokud se neshodují, vyberte **OK**. Vraťte se na stránku **Podrobnosti o ovladači** a zrušte označení ovladačů, které neodpovídají architektuře vybrané spouštěcí image. Pokud jste třeba vybrali spouštěcí image x64 a x86, všechny ovladače musí podporovat obě tyto architektury. Pokud jste vybrali spouštěcí image x64, všechny ovladače musí architekturu x64.  

        > [!NOTE]
        > - Architektura je založená na architektuře, která je uvedena v souboru INF od výrobce.  
        > - Pokud ovladač hlásí, že podporuje obě architektury, můžete ho importovat do obou spouštěcích imagí.  

    - Configuration Manager vás upozorní, když přidáváte ovladače zařízení, které nejsou ovladači sítě nebo úložiště, do spouštěcí bitové kopie. Ve většině případů nejsou pro spouštěcí image nutné. Vyberte **Ano** , pokud chcete ovladače přidat do spouštěcí image, nebo **ne** , chcete-li se vrátit a změnit výběr ovladače.  

    - Configuration Manager vás upozorní, pokud některé z vybraných ovladačů nejsou správně digitálně podepsány. Pokračujte výběrem možnosti **Ano** nebo kliknutím na tlačítko **ne** vraťte zpět a proveďte změny v výběru ovladače.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a>Další akce pro ovladače zařízení  

V případě, že je vyberete v uzlu **ovladače** , můžete provádět další akce správy ovladačů.  

#### <a name="categorize"></a>Zařadit do kategorií
Zruší, spravuje nebo nastavuje administrativní kategorii pro vybrané ovladače.

#### <a name="delete"></a>Odstranit
Odebere ovladač z uzlu **ovladače** a také odebere ovladač z přidružených distribučních bodů.

#### <a name="disable"></a>Zakázat
Zakáže instalaci ovladače. Tato akce dočasně zakáže ovladač. Pořadí úkolů nemůže nainstalovat zakázaný ovladač při nasazení operačního systému. 

> [!Note]  
> Tato akce zabrání pouze instalaci ovladačů pomocí kroku pořadí úkolů **automaticky použít ovladač** .

#### <a name="enable"></a>Povolení
Umožňuje Configuration Manager klientským počítačům a sekvencím úloh instalovat ovladač zařízení při nasazení operačního systému.

#### <a name="move"></a>Přesunout
Přesune ovladač zařízení do jiné složky v uzlu **Ovladače**.

#### <a name="properties"></a>Vlastnosti
Otevře dialogové okno **vlastnosti** . Zkontrolujte a změňte vlastnosti ovladače. Můžete například změnit název a popis, povolit nebo zakázat a určit, na kterých platformách může běžet.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a>Použití pořadí úkolů k instalaci ovladačů  

Pomocí pořadí úkolů můžete automatizovat způsob nasazení operačního systému. Každý krok v pořadí úkolů může provádět určitou akci, jako je například instalace ovladače. K instalaci ovladačů zařízení při nasazení operačního systému můžete použít následující dva kroky pořadí úloh:  

- [Automaticky použít ovladače](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Tento krok umožňuje automaticky vyhledat a nainstalovat ovladače zařízení při nasazování operačního systému. Krok pořadí úkolů můžete nakonfigurovat tak, aby pro každé zjištěné hardwarové zařízení nainstaloval pouze nejlépe vyhovující ovladač. Případně můžete určit, že krok nainstaluje všechny kompatibilní ovladače pro každé zjištěné hardwarové zařízení a pak instalační program systému Windows zvolit nejlepší ovladač. Můžete také zadat kategorii ovladačů pro omezení ovladačů, které jsou k dispozici pro tento krok.  

- [Použít balíček ovladače](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Tento krok umožňuje zpřístupnit instalačnímu programu systému Windows všechny ovladače zařízení z určitého balíčku. Instalační program systému Windows pak hledá požadované ovladač zařízení v zadaných balíčcích. Pokud vytvoříte samostatné médium, musíte ovladače zařízení nainstalovat pomocí tohoto kroku.  

Při použití těchto kroků pořadí úloh můžete také určit, jak mají být ovladače nainstalovány v počítači, do kterého nasazujete operační systém. Další informace najdete v tématu [Správa pořadí úkolů pro automatizaci úloh](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a>Sestavy ovladačů  

Kategorie sestav **Správa ovladačů** nabízí několik sestav, které podávají obecné informace o ovladačích zařízení v katalogu ovladačů. Další informace o sestavách najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).

