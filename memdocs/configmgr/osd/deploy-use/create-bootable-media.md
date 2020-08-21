---
title: Vytvoření spouštěcího média
titleSuffix: Configuration Manager
description: Pomocí spouštěcího média v Configuration Manager nainstalujte novou verzi Windows nebo počítač nahraďte.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3ec1476a9b5374eb91d147e2b22fd0f669d6251
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698040"
---
# <a name="create-bootable-media"></a>Vytvoření spouštěcího média

*Platí pro: Configuration Manager (Current Branch)*

Spouštěcí médium v Configuration Manager obsahuje spouštěcí image, volitelné příkazy před zahájením a přidružené soubory a soubory Configuration Manager. Použijte spouštěcí médium pro následující scénáře nasazení operačního systému:

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)

- [Nahrazení existujícího počítače a nastavení přenosu](replace-an-existing-computer-and-transfer-settings.md)

## <a name="usage"></a>Využití

K následujícímu procesu dochází při spuštění spouštěcího média:

1. Spustí se cílový počítač.

1. Připojuje se k síti.

1. Načte z webu následující obsah:

    - Zadané pořadí úkolů

    - Bitová kopie operačního systému

    - Libovolný další požadovaný obsah

Vzhledem k tomu, že pořadí úkolů není na médiu, můžete změnit pořadí úloh nebo obsah, aniž byste museli znovu vytvořit médium.

Balíčky na spouštěcím médiu nejsou šifrovány. Chcete-li zajistit, aby byl obsah balíčku zabezpečený před neautorizovanými uživateli, proveďte příslušná bezpečnostní opatření. Přidejte například heslo k médiu.

Počínaje verzí 2006 může spouštěcí médium stahovat cloudový obsah. Zařízení ještě potřebuje intranetové připojení k bodu správy. Může získat obsah z brány pro správu cloudu s povoleným obsahem (CMG) nebo cloudového distribučního bodu.<!--6209223--> Další informace najdete v tématu [Podpora cloudového obsahu](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="prerequisites"></a>Předpoklady

Než vytvoříte spouštěcí médium pomocí Průvodce vytvořením média pořadí úloh, ujistěte se, že jsou splněné všechny tyto podmínky.

### <a name="boot-image"></a>Spouštěcí image

Vezměte v úvahu následující body spouštěcí bitové kopie, které v pořadí úkolů použijete k nasazení operačního systému:

- Architektura spouštěcí bitové kopie musí být vhodná pro architekturu cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Ale cílový počítač x86 může bootovat a spustit pouze bootovací obrázek x86.
- Ujistěte se, že spouštěcí bitová kopie obsahuje síťové ovladače a ovladače úložiště, které jsou nutné k zřízení cílového počítače.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Vytvoření pořadí úkolů pro nasazení operačního systému

Jako součást spouštěcího média zadejte pořadí úkolů pro nasazení operačního systému. Další informace najdete v tématu [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuce veškerého obsahu souvisejícího s pořadím úkolů

Distribuujte veškerý obsah, který pořadí úkolů vyžaduje alespoň v jednom distribučním bodě. Tento obsah obsahuje spouštěcí image a další související soubory před zahájením. Průvodce shromáždí obsah z distribučního bodu při vytváření spouštěcího média.

Váš uživatelský účet potřebuje alespoň přístupová práva ke **čtení** knihovny obsahu v tomto distribučním bodě. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Příprava vyměnitelné jednotky USB

Pokud používáte vyměnitelnou jednotku USB, připojte ji k počítači, na kterém spouštíte Průvodce vytvořením média pořadí úloh. Jednotka USB musí být zjistitelná systémem Windows jako zařízení pro odebrání. Průvodce při vytváření média provádí zápis přímo na jednotku USB.

### <a name="create-an-output-folder"></a>Vytvoření výstupní složky

Před spuštěním Průvodce vytvořením média pořadí úloh pro vytvoření média pro sadu CD nebo DVD vytvořte složku pro výstupní soubory, které vytvoří. Médium, které vytvoří pro sadu disků CD nebo DVD, je zapsáno jako. Soubor ISO přímo ve složce.

## <a name="process"></a>Proces

> [!NOTE]
> V prostředích PKI, protože v primární lokalitě zadáte kořenovou certifikační autoritu (CA), nezapomeňte vytvořit spouštěcí médium v primární lokalitě. Lokalita centrální správy (CAS) neobsahuje informace o kořenové certifikační autoritě, aby bylo možné správně vytvořit spouštěcí médium.

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit médium pořadí úloh**. Tato akce spustí Průvodce vytvořením média pořadí úloh.

1. Na stránce **Výběr typu média** zadejte následující možnosti:

    - Vyberte položku **Spouštěcí médium**.

    - Případně, pokud chcete, aby byl operační systém nasazen pouze bez nutnosti zásahu uživatele, vyberte možnost **umožňuje bezobslužné nasazení operačního systému**.

        > [!IMPORTANT]
        > Když vyberete tuto možnost, uživateli se nezobrazí výzva k zadání informací o konfiguraci sítě nebo o volitelných sekvencích úloh. Pokud nakonfigurujete médium pro ochranu heslem, bude se uživateli stále zobrazovat výzva k zadání hesla.

1. Na stránce **Správa média** zadejte jednu z následujících možností:

    - **Dynamické médium**: umožňuje bodu správy přesměrování média do jiného bodu správy na základě umístění klienta v hranicích lokality.

    - **Médium založené na webu**: médium pouze kontaktuje zadaný bod správy.

1. Na stránce **typ média** určete, jestli je médium **vyměnitelná jednotka USB** nebo **Sada disků CD/DVD**. Pak nakonfigurujte následující možnosti:

    > [!IMPORTANT]
    > Médium používá souborový systém FAT32. Nemůžete vytvořit médium na jednotce USB, jejíž obsah obsahuje soubor větší než 4 GB.

    - Pokud vyberete **vyměnitelnou jednotku USB**, vyberte jednotku, na kterou chcete obsah uložit.

        - **Naformátujte vyměnitelnou jednotku USB (FAT32) a proveďte spouštěcí**zařízení: ve výchozím nastavení nechte jednotku USB Configuration Manager připravit. Mnoho novějších zařízení UEFI vyžaduje spouštěcí oddíl FAT32. Tento formát ale taky omezuje velikost souborů a celkovou kapacitu jednotky. Pokud jste již naformátovali a nakonfigurovali vyměnitelnou jednotku, zakažte tuto možnost.

    - Pokud vyberete možnost **sada CD/DVD**, určete kapacitu média (**velikost média**) a název a cestu k výstupnímu souboru (**soubor média**). Průvodce uloží výstupní soubory do tohoto umístění. Příklad: `\\servername\folder\outputfile.iso`

        Pokud je kapacita média příliš malá pro uložení celého obsahu, vytvoří se několik souborů. Pak je potřeba obsah uložit na víc disků CD nebo DVD. Pokud vyžaduje více mediálních souborů, Configuration Manager přidá číslo sekvence k názvu každého výstupního souboru, který vytvoří.

        > [!IMPORTANT]
        > Pokud vyberete stávající bitovou kopii .iso, průvodce média pořadí úlohy odstraní tuto bitovou kopii z disku nebo zruší její sdílení okamžitě po otevření další stránky průvodce. Existující bitová kopie je odstraněna, i když pak průvodce zrušíte.

    - **Pracovní složka**<!--1359388-->: Proces vytváření médií může vyžadovat mnohem dočasné místo na disku. Ve výchozím nastavení je toto umístění podobné následující cestě: `%UserProfile%\AppData\Local\Temp` . Pokud chcete zajistit větší flexibilitu při ukládání těchto dočasných souborů, můžete tuto hodnotu změnit na jinou jednotku a cestu.

    - **Popisek média**<!--1359388-->: Přidejte popisek k médiu pořadí úloh. Tento popisek vám pomůže lépe identifikovat médium po jeho vytvoření. Výchozí hodnota je `Configuration Manager`. Toto textové pole se zobrazí v následujících umístěních:

        - Pokud připojíte soubor ISO, systém Windows zobrazí tento popisek jako název připojené jednotky.

        - Pokud naformátujete jednotku USB, použije se jako název prvních 11 znaků popisku.

        - Configuration Manager zapíše textový soubor s názvem `MediaLabel.txt` do kořenového adresáře média. Ve výchozím nastavení soubor obsahuje jeden řádek textu: `label=Configuration Manager` . Pokud přizpůsobíte popisek pro médium, tento řádek používá vlastní popisek místo výchozí hodnoty.

    - **Zahrnout soubor Autorun. inf na médium**<!-- 4090666 -->: Počínaje verzí 1906 Configuration Manager ve výchozím nastavení nepřidá soubor Autorun. inf. Tento soubor je pro antimalwarové produkty často blokovaný. Další informace o funkci AutoRun systému Windows najdete v tématu [Vytvoření aplikace CD-ROM s podporou automatického spuštění](/windows/desktop/shell/autoplay). Pokud to pro váš scénář pořád potřebujete, vyberte tuto možnost, chcete-li soubor zahrnout.

1. Na stránce **zabezpečení** zadejte následující možnosti:

    - **Povolit podporu neznámých počítačů**: povolí médium nasadit operační systém na počítač, který není spravován nástrojem Configuration Manager. V databázi Configuration Manager neexistují žádné záznamy o těchto počítačích. Další informace najdete v tématu [Příprava pro nasazení do neznámých počítačů](../get-started/prepare-for-unknown-computer-deployments.md).

    - **Chránit médium heslem**: zadejte silné heslo, abyste mohli médium ochránit před neoprávněným přístupem. Pokud určíte heslo, musí uživatel k použití spouštěcího média zadat toto heslo.

        > [!IMPORTANT]
        > K zvýšení ochrany spouštěcího média doporučujeme vždy přiřadit heslo.

    - V případě komunikace HTTP vyberte možnost **vytvořit certifikát média podepsaný svým držitelem**. Pak zadejte datum zahájení a vypršení platnosti certifikátu.

        > [!NOTE]
        > Pokud vyberete tuto možnost, nemůžete na stránce **spouštěcí bitová kopie** tohoto průvodce vybrat žádný bod správy https.

    - V případě komunikace pomocí protokolu HTTPS vyberte možnost **importovat certifikát PKI**. Pak zadejte certifikát, který chcete importovat, a jeho heslo.

        Další informace o tomto klientském certifikátu, který používají spouštěcí image, najdete v tématu [požadavky na certifikát PKI](../../core/plan-design/network/pki-certificate-requirements.md).

    - **Spřažení zařízení a uživatele**: pro podporu správy zaměřené na uživatele v Configuration Manager určete, jak chcete, aby média spojila uživatele s cílovým počítačem. Další informace o tom, jak nasazení operačního systému podporuje spřažení uživatelských zařízení, najdete v tématu [přidružení uživatelů k cílovému počítači](../get-started/associate-users-with-a-destination-computer.md).

        - **Povolí spřažení uživatelských zařízení pomocí automatického schválení**: médium automaticky přidruží uživatele k cílovému počítači. Tato funkce je založena na akcích sekvence úloh, která nasazuje operační systém. V tomto scénáři pořadí úkolů vytvoří vztah mezi zadanými uživateli a cílovým počítačem při nasazování operačního systému do cílového počítače.

        - **Povolení spřažení uživatelských zařízení na schválení správcem**: po udělení schválení médium přidružuje uživatele k cílovému počítači. Tato funkce je založena na rozsahu pořadí úkolů, které nasazuje operační systém. V tomto scénáři pořadí úkolů vytvoří vztah mezi zadanými uživateli a cílovým počítačem. Poté čeká na schválení od správce před nasazením operačního systému.

        - **Nepovolit spřažení uživatelských zařízení**: médium nespojuje uživatele s cílovým počítačem. V tomto scénáři pořadí úkolů nepřidruží uživatele k cílovému počítači při nasazení operačního systému.

1. Na stránce **spouštěcí bitová kopie** určete následující možnosti:

    > [!IMPORTANT]
    > Architektura spouštěcí bitové kopie, kterou distribuujete, musí být vhodná pro architekturu cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Cílový počítač x86 však může spustit pouze spouštěcí bitovou kopii x86.

    - **Spouštěcí bitová kopie**: výběrem spouštěcí bitové kopie Spusťte cílový počítač.

    - **Distribuční bod**: Vyberte distribuční bod, který obsahuje spouštěcí bitovou kopii. Průvodce získá bootovací obrázek z distribučního místa a uloží jej do médií.

        > [!NOTE]
        > Váš uživatelský účet potřebuje alespoň oprávnění **ke čtení** knihovny obsahu v distribučním bodě.

    - **Bod správy**: pouze pro *médium založené na lokalitě*vyberte bod správy z primární lokality.

    - **Přidružené body správy**: jenom pro *Dynamické médium*, vyberte body správy primární lokality, které se mají použít, a pořadí priorit pro počáteční komunikaci.

        > [!NOTE]
        > Když na stránce **zabezpečení** v tomto průvodci určíte certifikát PKI, Tato stránka zobrazí jenom body správy s POVOLENým protokolem HTTPS.

1. Na stránce **vlastní nastavení** určete následující možnosti:

    - Přidejte jakékoli proměnné, které pořadí úkolů používá.

    - **Povolit příkaz před zahájením**: Zadejte všechny příkazy před zahájením, které chcete spustit před spuštěním pořadí úkolů. Předstartovní příkazy jsou skripty nebo spustitelné soubory, které mohou komunikovat s uživatelem v systému Windows PE před spuštěním pořadí úloh. Další informace najdete v tématu [příkazy před zahájením pro médium pořadí úloh](../understand/prestart-commands-for-task-sequence-media.md).

        > [!TIP]
        > Během vytváření média pořadí úkolů zapíše ID balíčku a Předstartovní příkazový řádek, včetně hodnoty všech proměnných pořadí úkolů, do souboru **CreateTSMedia. log** v počítači, ve kterém je spuštěna konzola Configuration Manager. Zkontrolováním tohoto protokolového souboru můžete ověřit hodnoty proměnných sekvence úlohy.

        Pokud příkaz před zahájením vyžaduje nějaký obsah, vyberte možnost **zahrnout soubory pro předspouštěcí příkaz**.

1. Dokončete průvodce.

## <a name="alternate-method"></a>Alternativní metoda

Spouštěcí médium můžete vytvořit na vyměnitelné jednotce USB, pokud jednotka není připojená k počítači, na kterém je spuštěná konzola Configuration Manager.

1. [Vytvořte spouštěcí médium pořadí úloh](#process). Na stránce **typ média** vyberte možnost **sada CD/DVD**. Průvodce zapíše výstupní soubory do umístění, které zadáte. Například: `\\servername\folder\outputfile.iso`.  

1. Připravte vyměnitelnou jednotku USB. Jednotka musí být naformátovaná, prázdná a spustitelná.

1. Připojte soubor ISO z umístění sdílené složky a přeneste soubory z ISO na jednotku USB.

## <a name="next-steps"></a>Další kroky

[Použití spouštěcího média k nasazení Windows přes síť](use-bootable-media-to-deploy-windows-over-the-network.md)