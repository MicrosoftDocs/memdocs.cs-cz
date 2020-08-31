---
title: Vytvoření samostatného média
titleSuffix: Configuration Manager
description: Použití samostatného média k nasazení operačního systému na počítači bez připojení k síti.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c8710c50dc2feabebd7e8f0f84ac49b3b0dd35c
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068017"
---
# <a name="create-stand-alone-media"></a>Vytvoření samostatného média

*Platí pro: Configuration Manager (Current Branch)*

Samostatné médium v Configuration Manager obsahuje vše potřebné k nasazení operačního systému na počítač bez připojení k síti.

Používejte samostatné médium s následujícími scénáři nasazení operačního systému:  

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

- [Upgrade systému Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Využití

Samostatné médium obsahuje pořadí úkolů, které automatizuje kroky pro instalaci operačního systému a veškerý další požadovaný obsah. Tento obsah obsahuje spouštěcí bitovou kopii, bitovou kopii operačního systému a ovladače zařízení. Protože samostatné médium ukládá všechno pro nasazení operačního systému, vyžaduje více místa na disku, než je vyžadováno pro jiné typy médií.

Když vytvoříte samostatné médium v lokalitě centrální správy, klient načte svůj přiřazený kód lokality ze služby Active Directory. Samostatné médium vytvořené v podřízených lokalitách automaticky přiřadí klientovi kód lokality pro danou lokalitu.  


## <a name="prerequisites"></a>Požadavky

Před vytvořením samostatného média pomocí Průvodce vytvořením média pořadí úloh se ujistěte, že jsou splněné všechny tyto podmínky.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Vytvoření pořadí úkolů pro nasazení operačního systému

Jako součást samostatného média zadejte pořadí úkolů pro nasazení operačního systému. Další informace najdete v tématu [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Nepodporované akce pro samostatné médium

Následující akce nejsou podporovány pro samostatná média:

- Krok [automaticky použít ovladače](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) v pořadí úkolů. Samostatné médium nepodporuje automatické použití ovladačů zařízení z katalogu ovladačů. Pomocí kroku [použít balíček ovladače](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) zpřístupníte určenou sadu ovladačů k instalační program systému Windows.  

- Krok [Stáhnout obsah balíčku](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) v pořadí úkolů. Informace o bodu správy nejsou k dispozici na samostatném médiu, takže se krok nepovede pokoušet o zobrazení výčtu umístění obsahu.  

- Instalování aktualizací softwaru.  

- Instalace softwaru před nasazením operačního systému.  

- Vlastní pořadí úkolů pro nasazení bez OS.  

- Spojování uživatelů s cílovým počítačem pro podporu spřažení uživatelských zařízení.  

- Dynamický balíček se nainstaluje přes krok [instalovat balíčky](../understand/task-sequence-steps.md#BKMK_InstallPackage) .  

- Dynamická aplikace se instaluje prostřednictvím kroku [instalovat aplikaci](../understand/task-sequence-steps.md#BKMK_InstallApplication) .

- Možnost **použít předprodukční klientský balíček, pokud je k dispozici** nastavení v kroku pořadí úkolů **nastavit systém Windows a nástroj ConfigMgr** . Další informace o tomto nastavení najdete v tématu [nastavení systému Windows a nástroje ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> K chybě může dojít v případě, že pořadí úkolů zahrnuje krok [instalovat balíček](../understand/task-sequence-steps.md#BKMK_InstallPackage) a Vy vytvoříte samostatné médium v lokalitě centrální správy. Lokalita centrální správy nemá potřebné zásady konfigurace klienta. Tyto zásady jsou nutné k povolení agenta distribuce softwaru při spuštění pořadí úkolů. V souboru **CreateTSMedia. log** se může zobrazit následující chyba:  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> U samostatného média, které obsahuje krok **instalovat balíček** , vytvořte samostatné médium v primární lokalitě s povoleným agentem distribuce softwaru.
>
> Případně můžete použít vlastní krok [příkazového řádku pro spuštění](../understand/task-sequence-steps.md#BKMK_RunCommandLine) . Přidejte ho za krok [nastavit systém Windows a nástroj ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) a před první krok **instalovat balíček** . Krok **Spustit příkazový řádek** spustí následující příkaz WMIC, který povolí agenta distribuce softwaru před prvním krokem instalace balíčku:  
>
> `WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuce veškerého obsahu souvisejícího s pořadím úkolů

Distribuujte veškerý obsah, který pořadí úkolů vyžaduje alespoň v jednom distribučním bodě. Tento obsah obsahuje spouštěcí bitovou kopii, bitovou kopii operačního systému a další související soubory. Průvodce shromáždí obsah z distribučního bodu při vytváření média.

Váš uživatelský účet potřebuje alespoň přístupová práva ke **čtení** knihovny obsahu v tomto distribučním bodě. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Příprava vyměnitelné jednotky USB

Pokud používáte vyměnitelnou jednotku USB, připojte ji k počítači, na kterém spouštíte Průvodce vytvořením média pořadí úloh. Jednotka USB musí být zjistitelná systémem Windows jako zařízení pro odebrání. Průvodce při vytváření média provádí zápis přímo na jednotku USB.

Samostatné médium používá souborový systém FAT32. Samostatné médium nemůžete vytvořit na vyměnitelném disku USB, jehož obsah obsahuje soubor větší než 4 GB.

### <a name="create-an-output-folder"></a>Vytvoření výstupní složky

Před spuštěním Průvodce vytvořením média pořadí úloh pro vytvoření média pro sadu CD nebo DVD vytvořte složku pro výstupní soubory, které vytvoří. Médium, které vytvoří pro sadu disků CD nebo DVD, je zapsáno jako. Soubor ISO přímo ve složce.


## <a name="process"></a>Proces

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit médium pořadí úloh**. Tato akce spustí Průvodce vytvořením média pořadí úloh.  

3. Na stránce **Výběr typu média** zadejte následující možnosti:  

    - Vyberte **samostatné médium**.  

    - Případně, pokud chcete, aby byl operační systém nasazen pouze bez nutnosti zásahu uživatele, vyberte možnost **umožňuje bezobslužné nasazení operačního systému**.  

        > [!IMPORTANT]  
        > Když vyberete tuto možnost, uživateli se nezobrazí výzva k zadání informací o konfiguraci sítě nebo o volitelných sekvencích úloh. Pokud nakonfigurujete médium pro ochranu heslem, bude se uživateli stále zobrazovat výzva k zadání hesla.  

4. Na stránce **typ média** určete, jestli je médium **vyměnitelná jednotka USB** nebo **Sada disků CD/DVD**. Pak nakonfigurujte následující možnosti:  

    > [!IMPORTANT]  
    > Médium používá souborový systém FAT32. Nemůžete vytvořit médium na jednotce USB, jejíž obsah obsahuje soubor větší než 4 GB.  

    - Pokud vyberete **vyměnitelnou jednotku USB**, vyberte jednotku, na kterou chcete obsah uložit.  

        - **Naformátujte vyměnitelnou jednotku USB (FAT32) a proveďte spouštěcí**zařízení: ve výchozím nastavení nechte jednotku USB Configuration Manager připravit. Mnoho novějších zařízení UEFI vyžaduje spouštěcí oddíl FAT32. Tento formát ale taky omezuje velikost souborů a celkovou kapacitu jednotky. Pokud jste již naformátovali a nakonfigurovali vyměnitelnou jednotku, zakažte tuto možnost.

    - Pokud vyberete možnost **sada CD/DVD**, určete kapacitu média (**velikost média**) a název a cestu k výstupnímu souboru (**soubor média**). Průvodce uloží výstupní soubory do tohoto umístění. Příklad: `\\servername\folder\outputfile.iso`  

        Pokud je kapacita média příliš malá pro uložení celého obsahu, vytvoří se několik souborů. Pak je potřeba obsah uložit na víc disků CD nebo DVD. Pokud vyžaduje více mediálních souborů, Configuration Manager přidá číslo sekvence k názvu každého výstupního souboru, který vytvoří.  

        Pokud nasadíte aplikaci společně s operačním systémem a aplikace se nemůže vejít na jedno médium, aplikace Configuration Manager ukládá aplikaci na více médií. Při spuštění samostatného média Configuration Manager vyzve uživatele k zadání dalšího média, kde je aplikace uložena.  

        > [!IMPORTANT]  
        > Pokud vyberete stávající bitovou kopii .iso, průvodce média pořadí úlohy odstraní tuto bitovou kopii z disku nebo zruší její sdílení okamžitě po otevření další stránky průvodce. Existující bitová kopie je odstraněna, i když pak průvodce zrušíte.  

    - **Pracovní složka**<!--1359388-->: Proces vytváření médií může vyžadovat mnoho místa na dočasném disku. Ve výchozím nastavení je toto umístění podobné následující cestě: `%UserProfile%\AppData\Local\Temp` . Od verze 1902 získáte větší flexibilitu, kam chcete ukládat tyto dočasné soubory, změňte tuto hodnotu na jinou jednotku a cestu.  

    - **Popisek média**<!--1359388-->: Od verze 1902 přidejte popisek k médiu pořadí úloh. Tento popisek vám pomůže lépe identifikovat médium po jeho vytvoření. Výchozí hodnota je `Configuration Manager`. Toto textové pole se zobrazí v následujících umístěních:  

        - Pokud připojíte soubor ISO, Windows zobrazí tento popisek jako název připojené jednotky.  

        - Pokud naformátujete jednotku USB, použije se jako název prvních 11 znaků popisku.  

        - Configuration Manager zapíše textový soubor s názvem `MediaLabel.txt` do kořenového adresáře média. Ve výchozím nastavení soubor obsahuje jeden řádek textu: `label=Configuration Manager` . Pokud přizpůsobíte popisek pro médium, tento řádek používá vlastní popisek místo výchozí hodnoty.  

    - **Zahrnout soubor Autorun. inf na médium**<!-- 4090666 -->: Počínaje verzí 1906 Configuration Manager ve výchozím nastavení nepřidá soubor Autorun. inf. Tento soubor je pro antimalwarové produkty často blokovaný. Další informace o funkci AutoRun systému Windows najdete v tématu [Vytvoření aplikace CD-ROM s podporou automatického spuštění](/windows/desktop/shell/autoplay). Pokud to pro váš scénář pořád potřebujete, vyberte tuto možnost, chcete-li soubor zahrnout.  

5. Na stránce **zabezpečení** zadejte následující možnosti:

    - **Chránit médium heslem**: zadejte silné heslo, abyste mohli médium ochránit před neoprávněným přístupem. Když zadáte heslo, musí uživatel zadat toto heslo pro použití média.  

        > [!IMPORTANT]  
        > Z hlediska zabezpečení je nejvhodnější při ochraně média vždy přiřadit heslo.  
        >
        > Na samostatném médiu zašifruje pouze kroky pořadí úloh a jejich proměnné. Nešifruje zbývající obsah média. Do skriptů pořadí úloh nezahrnujte žádné citlivé informace. Ukládání a implementace všech citlivých informací pomocí proměnných pořadí úkolů.  

    - **Vyberte platný rozsah kalendářních dat pro toto samostatné médium**: nastavte volitelná data začátku a konce platnosti média. Standardně je toto nastavení zakázané. Data jsou porovnána se systémovým časem v počítači před spuštěním samostatného média. Pokud je systémový čas dřívější než čas spuštění nebo pozdější než čas vypršení platnosti, nespustí se samostatné médium. Tyto možnosti jsou dostupné taky pomocí rutiny [New-CMStandaloneMedia](/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) prostředí PowerShell.  

6. Na stránce **samostatný disk CD/DVD** vyberte pořadí úloh, které NASADÍ operační systém. Můžete vybrat jenom ta pořadí úloh, která jsou přidružená ke spouštěcí imagi. Ověřte seznam obsahu, na který odkazuje pořadí úkolů.  

    - **Zjistit přidružené závislosti aplikací a přidat je na toto médium**: přidejte také obsah na médium pro závislosti aplikací.  

        > [!TIP]  
        > Pokud nevidíte očekávané závislosti aplikací, zrušte výběr a pak znovu vyberte tuto možnost, aby se seznam aktualizoval.  

7. Na stránce **Vybrat aplikaci** zadejte další aplikační obsah, který chcete zahrnout jako součást souboru média.  

8. Na stránce **Vybrat balíček** zadejte další obsah balíčku, který se má zahrnout jako součást souboru média.  

9. Na stránce **Vybrat balíček ovladače** zadejte další obsah balíčku ovladačů, který chcete zahrnout jako součást souboru média.  

10. Na stránce **distribuční body** určete distribuční body, které obsahují požadovaný obsah.  

    Configuration Manager zobrazí pouze distribuční body s obsahem. Než budete pokračovat, distribuujte veškerý obsah přidružený k pořadí úkolů alespoň k jednomu distribučnímu bodu. Po distribuci obsahu aktualizujte seznam distribučních bodů. Odeberte všechny distribuční body, které jste už na této stránce vybrali, přejít na předchozí stránku a pak zpátky na stránku **distribuční body** . Případně můžete také restartovat průvodce. Další informace najdete v tématech [distribuce obsahu, na který odkazuje pořadí úkolů](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) , a [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. Na stránce **vlastní nastavení** určete následující možnosti:  

    - Přidejte jakékoli proměnné, které pořadí úkolů používá.  

    - **Povolit příkaz před zahájením**: Zadejte všechny příkazy před zahájením, které chcete spustit před spuštěním pořadí úkolů. Předstartovní příkazy jsou skripty nebo spustitelné soubory, které mohou komunikovat s uživatelem v systému Windows PE před spuštěním pořadí úloh. Další informace najdete v tématu [příkazy před zahájením pro médium pořadí úloh](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Během vytváření média pořadí úkolů zapíše ID balíčku a Předstartovní příkazový řádek, včetně hodnoty všech proměnných pořadí úkolů, do souboru **CreateTSMedia. log** v počítači, ve kterém je spuštěna konzola Configuration Manager. Zkontrolováním tohoto protokolového souboru můžete ověřit hodnoty proměnných sekvence úlohy.  

        Pokud příkaz před zahájením vyžaduje nějaký obsah, vyberte možnost **zahrnout soubory pro předspouštěcí příkaz**.  

12. Dokončete průvodce.  

Soubory samostatného média (. ISO) se vytvoří v cílové složce. Pokud jste vybrali možnost **sada CD/DVD**, zkopírujte výstupní soubory na sadu disků CD nebo DVD.


## <a name="next-steps"></a>Další kroky

[Nasazení Windows pomocí samostatného média bez použití sítě](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
