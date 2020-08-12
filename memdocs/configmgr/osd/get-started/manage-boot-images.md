---
title: Správa spouštěcích imagí
titleSuffix: Configuration Manager
description: V Configuration Manager se naučíte spravovat spouštěcí bitové kopie prostředí Windows PE používané při nasazení operačního systému.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e68a3274a32d28ac0b4ad2a611c59870ee338472
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124537"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Správa spouštěcích imagí pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Spouštěcí bitová kopie v Configuration Manager je image prostředí [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE), která se používá při nasazení operačního systému. Spouštěcí image slouží ke spuštění počítače v prostředí WinPE. Tento minimální operační systém obsahuje omezené součásti a služby. Configuration Manager pomocí prostředí WinPE připravit cílový počítač pro instalaci Windows.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a>Výchozí spouštěcí image

Configuration Manager poskytuje dvě výchozí spouštěcí image: jednu pro podporu platforem x86 a druhou pro podporu platforem x64. Tyto image jsou uložené ve složkách *x64* nebo *i386* v následující sdílené složce na serveru lokality: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\` . Výchozí spouštěcí image se aktualizují nebo znovu vygenerují v závislosti na tom, jakou akci chcete provést.

Pro kteroukoli z akcí popsaných u výchozích spouštěcích imagí zvažte následující chování:

- Zdrojové objekty ovladače musí být platné. Mezi tyto objekty patří zdrojové soubory ovladače. Pokud tyto objekty nejsou platné, lokalita ovladače nepřidá do spouštěcích imagí.  

- Spouštěcí bitové kopie, které nejsou založené na výchozích spouštěcích bitových kopiích, i když používají stejnou verzi prostředí Windows PE, se nezmění.  

- Znovu distribuovat upravené spouštěcí bitové kopie do distribučních bodů.  

- Znovu vytvořte jakékoli médium, které používá upravené spouštěcí bitové kopie.  

- Pokud nechcete, aby se automaticky aktualizovaly vlastní nebo výchozí spouštěcí image, neukládejte je do výchozího umístění.  

> [!NOTE]
> Nástroj protokol Configuration Manager (**CMTrace**) se přidá do všech spouštěcích imagí v **knihovně softwaru**. Když jste v prostředí Windows PE, spusťte nástroj zadáním `cmtrace` z příkazového řádku.
>
> CMTrace je výchozí prohlížeč pro soubory protokolů v systému Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>K instalaci nejnovější verze Configuration Manager použijte aktualizace a údržbu.

Při upgradu verze Windows Assessment and Deployment Kit (ADK) a následné instalaci nejnovější verze Configuration Manager pomocí aktualizace a údržby vygeneruje lokalita znovu výchozí spouštěcí image. Tato aktualizace zahrnuje novou verzi prostředí WinPE z aktualizovaného Windows ADK, nové verze klienta Configuration Manager, ovladačů a přizpůsobení. Web neupravuje vlastní spouštěcí image.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Upgradovat z Configuration Manager 2012 na aktuální větev

Když upgradujete Configuration Manager 2012 na aktuální větev, lokalita znovu vygeneruje výchozí spouštěcí image. Tato aktualizace zahrnuje novou verzi prostředí WinPE z aktualizovaného systému Windows ADK a novou verzi klienta Configuration Manager. Všechna Přizpůsobení spouštěcích bitových kopií zůstanou beze změny. Web neupravuje vlastní spouštěcí image.

### <a name="update-distribution-points-with-the-boot-image"></a>Aktualizace distribučních bodů pomocí spouštěcí bitové kopie

Použijete-li akci **Aktualizovat distribuční body** z uzlu **spouštěcí bitové kopie** v konzole nástroje, lokalita aktualizuje cílovou spouštěcí kopii pomocí komponent klienta, ovladačů a přizpůsobení.

Spouštěcí bitovou kopii můžete znovu načíst pomocí nejnovější verze prostředí WinPE z instalačního adresáře Windows ADK. Na stránce **Obecné** v Průvodci aktualizací distribučních bodů jsou k dispozici následující informace:

- Aktuální verze systému Windows ADK nainstalovaná na serveru lokality
- Aktuální verze produkčního klienta
- Verze prostředí WinPE pro Windows ADK ve spouštěcí imagi
- Verze klienta Configuration Manager ve spouštěcí imagi

Pokud jsou verze v spouštěcí imagi zastaralé, použijte možnost pro **opětovné načtení této spouštěcí image s aktuální verzí Windows PE ze sady Windows ADK**.

> [!Important]  
> Tato akce je k dispozici pro výchozí i vlastní spouštěcí image. Během tohoto procesu pro opětovné načtení spouštěcí image nezůstane na webu žádná ruční přizpůsobení vytvořená mimo Configuration Manager. Mezi tato přizpůsobení patří rozšíření třetích stran. Tato možnost znovu sestaví spouštěcí image pomocí nejnovější verze prostředí WinPE a nejnovější verze klienta. Znovu se aplikují jenom konfigurace, které jste zadali ve vlastnostech spouštěcí image. <!--SCCMDocs issue #1283-->

Uzel **spouštěcí bitové kopie** obsahuje také nový sloupec pro (**verze klienta**). Tento sloupec slouží k rychlému zobrazení Configuration Manager verze klienta v každé spouštěcí imagi.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a>Přizpůsobení spouštěcí image  

Pokud je spouštěcí bitová kopie založená na verzi prostředí WinPE z podporované verze sady Windows ADK, můžete upravit nebo [Upravit spouštěcí bitovou kopii](#BKMK_ModifyBootImages) z konzoly nástroje. Když upgradujete lokalitu a nainstalujete novou verzi sady Windows ADK, vlastní spouštěcí image se neaktualizují s novou verzí Windows ADK. Pokud k tomu dojde, nemůžete přizpůsobit spouštěcí bitové kopie v konzole Configuration Manager. Budou však i nadále fungovat stejně jako před upgradem.  

Je-li spouštěcí image založena na jiné verzi sady Windows ADK nainstalované v lokalitě, je nutné přizpůsobit spouštěcí bitové kopie. K přizpůsobení těchto spouštěcích imagí použijte jinou metodu, například pomocí nástroje příkazového řádku Obsluha a správa bitových kopií (DISM) nasazení. DISM je součástí sady Windows ADK. Další informace najdete v tématu [Přizpůsobení spouštěcích bitových kopií](customize-boot-images.md).  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a>Přidat spouštěcí bitovou kopii  

Během instalace lokality Configuration Manager automaticky přidávají spouštěcí bitové kopie, které jsou založené na verzi prostředí WinPE z podporované verze sady Windows ADK. V závislosti na verzi Configuration Manager můžete přidat spouštěcí bitové kopie založené na jiné verzi prostředí WinPE z podporované verze sady Windows ADK. Pokud se pokusíte přidat spouštěcí bitovou kopii, která obsahuje nepodporovanou verzi prostředí WinPE, dojde k chybě. V následujícím seznamu jsou aktuálně podporované verze Windows ADK a WinPE:

- Windows ADK verze: Windows ADK pro Windows 10

- Verze prostředí Windows PE pro spouštěcí bitové kopie přizpůsobitelné z konzoly Configuration Manager: Windows PE 10

- Podporované verze prostředí Windows PE pro spouštěcí bitové kopie, *které nelze přizpůsobit* z konzoly Configuration Manager

  - Windows PE 3,1<sup>[Poznámka 1](#bkmk_note1)</sup>

  - Windows PE 5

Použijte například konzolu Configuration Manager k přizpůsobení spouštěcích imagí založených na Windows PE 10 od Windows ADK pro Windows 10. Spouštěcí bitovou kopii založenou na Windows PE 5 si můžete přizpůsobit z jiného počítače pomocí verze nástroje DISM z Windows ADK pro Windows 8. Pak přidejte vlastní spouštěcí bitovou kopii do konzoly Configuration Manager. Další informace najdete v následujících článcích:

- [Přizpůsobení spouštěcích imagí](customize-boot-images.md)
- [Podpora pro Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [Podporované platformy DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Poznámka 1: podpora pro Windows PE 3,1**
>
> Přidejte pouze spouštěcí bitovou kopii, která je Configuration Manager založená na systému Windows PE *verze 3,1*. Upgradujte Windows AIK pro Windows 7 (na platformě Windows PE 3,0) pomocí doplňku Windows AIK pro Windows 7 SP1 (na platformě Windows PE 3,1). Doplněk Windows AIK pro Windows 7 SP1 si můžete stáhnout z webu [Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=5188).  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a pak vyberte uzel **spouštěcí bitové kopie** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **přidat spouštěcí bitovou kopii**. Tato akce spustí Průvodce přidáním bitové spouštěcí kopie.  

3. Na stránce **zdroj dat** zadejte následující možnosti:  

    - V poli **Cesta** určete cestu k souboru WIM spouštěcí bitové kopie. Zadaná cesta musí být platná síťová cesta ve formátu UNC. Příklad: `\\ServerName\ShareName\BootImageName.wim`

    - Vyberte spouštěcí bitovou kopii z rozevíracího seznamu **Spouštěcí bitová kopie**. Pokud soubor WIM obsahuje více spouštěcích bitových kopií, vyberte příslušnou bitovou kopii.  

4. Na stránce **Obecné** zadejte následující možnosti:  

    - V poli **Název** zadejte unikátní název spouštěcí bitové kopie.  

    - V poli **Verze** zadejte číslo verze spouštěcí bitové kopie.  

    - V poli **Komentář** zadejte stručný popis způsobu použití spouštěcí bitové kopie.  

5. Dokončete průvodce.  

Spouštěcí bitová kopie je nyní uvedena v uzlu **spouštěcí bitová kopie** . Před použitím spouštěcí image k nasazení operačního systému Distribuujte spouštěcí bitovou kopii do distribučních bodů.

> [!Tip]  
> V uzlu **spouštěcí bitové kopie** v konzole se ve sloupci **Velikost (KB)** zobrazuje dekomprimovaná velikost každé spouštěcí bitové kopie. Když lokalita odešle spouštěcí image přes síť, pošle komprimovanou kopii. Tato kopie je obvykle menší než velikost uvedená ve sloupci **Velikost (KB)** .  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a>Distribuce spouštěcích bitových kopií  

Spouštěcí bitové kopie jsou distribuovány do distribučních bodů stejným způsobem, jak distribuujete jiný obsah. Před nasazením operačního systému nebo vytvoření média Distribuujte spouštěcí bitovou kopii do alespoň jednoho distribučního bodu.

Další informace o tom, jak distribuovat spouštěcí bitovou kopii, najdete v tématu [distribuce obsahu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Chcete-li použít technologii PXE k nasazení operačního systému, před distribucí spouštěcí image zvažte následující body:  

- Nakonfigurujte distribuční bod, aby přijímal požadavky PXE.  
- Distribuujte spouštěcí image x86 i x64 s povoleným PXE aspoň na jeden distribuční bod s povoleným PXE.  
- Configuration Manager distribuuje spouštěcí bitové kopie do složky **RemoteInstall** v distribučním bodě s povoleným PXE.  
  
Další informace o použití technologie PXE k nasazení operačních systémů najdete v tématu [použití technologie PXE k nasazení systému Windows přes síť](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a>Úprava spouštěcí bitové kopie  

Přidejte nebo odeberte ovladače zařízení v imagi nebo upravte vlastnosti spouštěcí bitové kopie. Ovladače, které přidáváte nebo odebíráte, můžou zahrnovat ovladače sítě nebo úložiště. Při úpravě spouštěcích imagí zohledněte tyto faktory:  

- Před přidáním ovladačů do spouštěcí image je importujte a povolte v katalogu ovladačů zařízení.  

- Když upravíte spouštěcí image, spouštěcí image nezmění žádný z přidružených balíčků, na které odkazuje spouštěcí image.  

- Až provedete změny spouštěcí image, **aktualizujte** spouštěcí image v distribučních bodech, které ji již mají. Tento proces zpřístupňuje nejnovější verzi spouštěcí bitové kopie pro klienty. Další informace najdete v tématu [Správa distribuovaného obsahu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Úprava vlastností spouštěcí bitové kopie  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a pak vyberte uzel **spouštěcí bitové kopie** .  

2. Vyberte spouštěcí bitovou kopii, kterou chcete upravit.  

3. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.  

4. Úpravou kteréhokoli z následujících nastavení můžete změnit chování spouštěcí bitové kopie.  

#### <a name="images"></a>Obrázky

Pokud změníte vlastnosti spouštěcí bitové kopie pomocí externího nástroje, na kartě **bitové kopie** vyberte možnost **znovu načíst**.  

#### <a name="drivers"></a>Ovladače

Na kartě **ovladače** přidejte ovladače zařízení systému Windows, které prostředí WinPE vyžaduje ke spuštění. Když přidáváte ovladače zařízení, vezměte v úvahu následující body:  

- Zajistěte, aby ovladače, které přidáváte do spouštěcí image, odpovídaly architektuře spouštěcí image.  

- Chcete-li zobrazit pouze ovladače pro architekturu spouštěcí bitové kopie, vyberte možnost **Skrýt ovladače, které neodpovídají architektuře spouštěcí bitové kopie**. Architektura ovladače je založena na architektuře, která je uvedena v souboru INF od výrobce.  

- Prostředí WinPE již obsahuje mnoho integrovaných ovladačů. Přidejte pouze ovladače sítě a úložiště, které nejsou součástí prostředí WinPE.  

- Do spouštěcí bitové kopie přidejte pouze ovladače sítě a úložiště, pokud neexistují požadavky na jiné ovladače v prostředí WinPE.  

- Pokud chcete zobrazit jenom ovladače úložiště a sítě, vyberte **Skrýt ovladače, které nejsou v třídě úložiště nebo sítě (u spouštěcích imagí)**. Tato možnost také skryje další ovladače, které nejsou obvykle potřeba pro spouštěcí image, jako jsou ovladače videa nebo modemu.  

- Chcete-li skrýt ovladače, které nemají platný digitální podpis, vyberte možnost **Skrýt ovladače, které nejsou digitálně podepsány**.  

> [!NOTE]  
> Importujte ovladače zařízení do katalogu ovladačů, než je přidáte do spouštěcí bitové kopie. Informace o importu ovladačů zařízení najdete v tématu [Správa ovladačů](manage-drivers.md).  

#### <a name="customization"></a>Přizpůsobení

Na kartě **Vlastní nastavení** vyberte některé z následujících nastavení:  

- Vyberte možnost **Povolit předspouštěcí příkazy** k určení příkazu, který se má spustit před spuštěním pořadí úloh. Pokud tuto možnost povolíte, zadejte také příkazový řádek, který se má spustit, a všechny podpůrné soubory vyžadované příkazem.  

    > [!WARNING]  
    > Přidejte `cmd /c` na začátek příkazového řádku. Pokud nezadáte `cmd /c` , příkaz se po spuštění nezavře. Nasazení bude i nadále čekat na dokončení příkazu a nespustí žádné další nakonfigurované příkazy nebo akce.  

    > [!TIP]  
    > Během vytváření média pořadí úloh průvodce zapíše ID balíčku a Předstartovní příkazový řádek do souboru **CreateTSMedia. log** . Tyto informace zahrnují hodnotu všech proměnných pořadí úkolů. Tento protokol je v počítači, na kterém je spuštěna konzola Configuration Manager. Zkontrolujte tento soubor protokolu a ověřte hodnoty proměnných pořadí úkolů.  

- Pomocí nastavení **Pozadí systému Windows PE** určete, jestli chcete používat výchozí pozadí systému WinPE, nebo vlastní pozadí.  

- Nakonfigurujte **pomocné místo systému Windows PE (MB)**, což je dočasné úložiště (jednotka RAM) používané prostředím WinPE. Když třeba v systému WinPE běží určitá aplikace a potřebuje zapisovat dočasné soubory, systém WinPE přesměruje tyto soubory na pomocné místo v paměti, aby simuloval přítomnost pevného disku. Ve výchozím nastavení je tato hodnota 512 MB pro zařízení s více než 1 GB paměti RAM, v opačném případě výchozí hodnota je 32 MB.  

- Vyberte možnost **Povolit podporu příkazů (pouze zkušební režim)**, aby se při nasazení spouštěcí image dal pomocí klávesy **F8** otevřít příkazový řádek. Tato možnost je užitečná při řešení potíží při testování nasazení. Použití tohoto nastavení v produkčním nasazení není doporučeno z důvodu zabezpečení.  

- **Nastavení výchozího rozložení klávesnice v prostředí WinPE**: <!--4910348-->Počínaje verzí 1910 nakonfigurujte výchozí rozložení klávesnice pro spouštěcí bitovou kopii. Pokud vyberete jiný jazyk než en-US, Configuration Manager dál obsahuje en-US v dostupných vstupních národních prostředích. V zařízení je počáteční rozložení klávesnice vybraným národním prostředím, ale pokud to bude potřeba, může uživatel zařízení v případě potřeby přepnout na en-US.

> [!Tip]
> Pomocí rutiny PowerShellu [set-CMBootImage](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) můžete nakonfigurovat tato nastavení ze skriptu.

#### <a name="optional-components"></a>Volitelné součásti

Na kartě **volitelné součásti** určete součásti, které jsou přidány do systému Windows PE pro použití s Configuration Manager. Další informace o dostupných volitelných komponentách najdete v tématu [WinPE: Přidání balíčků (informace o volitelných komponentách)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Následující komponenty jsou vyžadovány Configuration Manager a vždy přidané do spouštěcích bitových kopií:

- Skriptování (WinPE-Scripting)
- Po spuštění (WinPE-SecureStartup)
- Síť (WinPE-WDS-Tools)
- Skriptování (WinPE-WMI)

Seznam **součástí** obsahuje další položky, které jsou přidány do této spouštěcí bitové kopie. Pokud chcete přidat další součásti, vyberte hvězdičku Gold. Chcete-li odebrat součást, vyberte ji ze seznamu a pak vyberte červený symbol X.

Zákazníci obvykle používají následující komponenty:

- Microsoft .NET (WinPE-NetFX): Tato součást je předpokladem pro PowerShell. Je to jedna z větších volitelných komponent.  
- Prostředí Windows PowerShell (WinPE-PowerShell): Tato komponenta vyžaduje rozhraní .NET a přidává omezené podpory prostředí PowerShell. Pokud spouštíte vlastní skripty PowerShellu během fáze prostředí WinPE v pořadí úkolů, přidejte tuto součást. Existují i další komponenty, které mohou být vyžadovány pro jiné rutiny prostředí PowerShell.
- HTML (WinPE-HTA): Pokud spouštíte vlastní aplikace HTML během fáze WinPE pořadí úkolů, přidejte tuto součást.

Další informace o přidávání jazyků najdete v tématu [Konfigurace více jazyků](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>Zdroj dat

Na kartě **Zdroj dat** aktualizujte některé z následujících nastavení:  

- Chcete-li změnit zdrojový soubor spouštěcí bitové kopie, nastavte **cestu k bitové kopii** a **index bitové kopie**.  

- Chcete-li vytvořit plán, kdy lokalita aktualizuje spouštěcí bitovou kopii, vyberte možnost **Aktualizovat distribuční body podle plánu**.  

- Pokud nechcete, aby obsah tohoto balíčku byl stáří mezipaměti klienta, aby uvolnil prostor pro další obsah, vyberte **zachovat obsah v mezipaměti klienta**.  

- Chcete-li určit, že lokalita distribuuje změněné soubory pouze při aktualizaci balíčku spouštěcí bitové kopie v distribučním bodě, vyberte možnost **Povolit binární rozdílovou replikaci** (binární rozdílová replikace). Toto nastavení minimalizuje síťový provoz mezi lokalitami. BINÁRNÍ ROZDÍLOVÁ replikace je zvláště užitečné, pokud je balíček spouštěcí bitové kopie velký a změny jsou relativně malé.  

- Pokud používáte spouštěcí image v nasazení s povoleným PXE, vyberte **nasadit tuto bitovou spouštěcí kopii z distribučního bodu s povoleným PXE**. Další informace najdete v tématu [použití technologie PXE k nasazení Windows přes síť](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### <a name="data-access"></a>Přístup k datům

Na kartě **přístup k datům** můžete nakonfigurovat nastavení sdílení balíčků. V případě potřeby v prostředí nastavte možnost **kopírování obsahu tohoto balíčku do sdílené složky balíčků v distribučních bodech**. Pak budete mít další možnost **použít pro sdílenou složku balíčku vlastní název** a zadat vlastní **název sdílené složky**. Pokud tuto možnost povolíte, v distribučních bodech se vyžaduje další místo na disku. Vztahuje se na všechny distribuční body, které obdrží tuto spouštěcí bitovou kopii.

#### <a name="distribution-settings"></a>Nastavení distribuce

Na kartě **Nastavení pro distribuci** vyberte některé z následujících nastavení:  

- V seznamu **Priorita distribuce** určete úroveň priority. Configuration Manager používá tento seznam priorit, pokud lokalita distribuuje více balíčků do stejného distribučního bodu.  

- Pokud chcete povolit distribuci obsahu na vyžádání do upřednostňovaných distribučních bodů, vyberte **Povolit pro distribuci na vyžádání**. Pokud povolíte toto nastavení, pokud klient požaduje obsah balíčku a obsah není dostupný v žádných distribučních bodech, bod správy distribuuje obsah. Další informace najdete v tématu [distribuce obsahu na vyžádání](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- Chcete-li určit, jak má lokalita distribuovat spouštěcí bitovou kopii do distribučních bodů, které jsou povoleny pro připravený obsah, nastavte **Nastavení připraveného distribučního bodu**. Další informace o připraveném obsahu najdete v tématu [Příprava obsahu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### <a name="content-locations"></a>Umístění obsahu

Na kartě **umístění obsahu** vyberte distribuční bod nebo skupinu distribučních bodů a použijte následující akce:  

- **Ověřit**: Zkontrolujte integritu balíčku spouštěcích bitových kopií ve vybraném distribučním bodě nebo skupině distribučních bodů.  

- Znovu **distribuovat**: Spusťte znovu distribuci spouštěcí bitové kopie do vybraného distribučního bodu nebo skupiny distribučních bodů.  

- **Odebrat**: Odstraňte spouštěcí bitovou kopii z vybraného distribučního bodu nebo skupiny distribučních bodů.  

#### <a name="security"></a>Zabezpečení

Na kartě **zabezpečení** si prohlédněte administrativní uživatele, kteří mají oprávnění k tomuto objektu.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a>Konfigurace spouštěcí bitové kopie pro PXE  

Než budete moci použít spouštěcí bitovou kopii pro nasazení založené na technologii PXE, nakonfigurujte spouštěcí bitovou kopii pro nasazení z distribučního bodu s povoleným PXE.  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a pak vyberte uzel **spouštěcí bitové kopie** .  

2. Vyberte spouštěcí bitovou kopii, kterou chcete upravit.  

3. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.  

4. Na kartě **Zdroj dat** vyberte **Nasadit tuto spouštěcí image z distribučního bodu s povoleným PXE**. Další informace najdete v tématu [použití technologie PXE k nasazení Windows přes síť](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a>Konfigurace více jazyků

> [!TIP]
> Počínaje verzí 1910 nakonfigurujte výchozí rozložení klávesnice ve vlastnostech spouštěcí bitové kopie. Další informace najdete v tématu věnovaném [přizpůsobení](#customization).<!--4910348-->

Spouštěcí image jsou jazykově neutrální. Tato funkce umožňuje použít jednu spouštěcí bitovou kopii k zobrazení textu pořadí úkolů v několika jazycích v prostředí WinPE. Přidejte příslušnou jazykovou podporu z karty **volitelné součásti** spouštěcí bitové kopie. Pak nastavte příslušnou proměnnou pořadí úkolů tak, aby označovala, který jazyk chcete zobrazit. Jazyk nasazeného operačního systému je nezávislý na jazyce v prostředí WinPE. Jazyk, který WinPE zobrazuje uživateli, je určen následujícím způsobem:  

- Když uživatel spustí pořadí úloh z existujícího operačního systému, Configuration Manager automaticky použije jazyk nakonfigurovaný pro tohoto uživatele. Když se pořadí úkolů spustí automaticky jako výsledek povinného termínu nasazení, Configuration Manager používá jazyk operačního systému.  

- Pro nasazení operačního systému, která používají technologii PXE nebo médium, nastavte hodnotu ID jazyka v proměnné **SMSTSLanguageFolder** jako součást předstartovního příkazu. Když se počítač spustí do prostředí Windows PE, zprávy se zobrazují v jazyce určeném v proměnné. Pokud při přístupu k souboru prostředků jazyka v zadané složce dojde k chybě nebo pokud tuto proměnnou nenastavíte, WinPE zobrazí zprávy ve výchozím jazyce.  

    > [!NOTE]  
    > Když chráníte médium heslem, text, který vyzývá uživatele k zadání hesla, se vždy zobrazuje v jazyce WinPE.  

Pomocí následujícího postupu můžete nastavit jazyk WinPE pro nasazení operačních systémů iniciovaná pomocí technologie PXE nebo médií.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Nastavení jazyka Windows PE pro nasazení operačního systému inicializovaného technologií PXE nebo médií  

1. Před aktualizací spouštěcí image ověřte, zda je příslušný soubor prostředků pořadí úkolů (tsres.dll) v odpovídající složce jazyka na serveru lokality. Například soubor prostředků English je v následujícím umístění:`<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Jako součást předstartovního příkazu nastavte proměnnou prostředí **SMSTSLanguageFolder** na příslušné ID jazyka. ID jazyka musí být zadáno pomocí desítkového a nešestnáctkového formátu. Chcete-li například nastavit ID jazyka na angličtinu, zadejte desítkovou hodnotu **1033**, nikoli hexadecimální hodnotu 00000409 názvu složky.  
