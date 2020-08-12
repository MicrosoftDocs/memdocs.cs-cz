---
title: Vytvoření předzpracovaného média
titleSuffix: Configuration Manager
description: Pomocí předzpracovaného média v Configuration Manager můžete zjednodušit nasazení Windows v několika scénářích.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82bb02d8154939b4b0e0ee89bcc6637e9393acff
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125215"
---
# <a name="create-prestaged-media"></a>Vytvoření předzpracovaného média

*Platí pro: Configuration Manager (Current Branch)*

Předzpracované médium v Configuration Manager je soubor bitové kopie systému Windows (WIM). Dá se nainstalovat na holé počítač od výrobce nebo v přípravném centru, které není připojené k produkčnímu Configuration Manager prostředí. Předzpracované médium obsahuje spouštěcí bitovou kopii, která se používá ke spuštění cílového počítače a image operačního systému, která se použije pro cílový počítač. Můžete taky v rámci předzpracovaného média určit aplikace, balíčky a ovladače, které mají být součástí. Pořadí úkolů, které nasazuje operační systém, není součástí média. Předzpracované médium se přenese na pevný disk nového počítače před jeho odesláním koncovému uživateli.

Použít Předzpracované médium pro následující scénáře nasazení operačního systému:  

- [Vytvoření image pro výrobce OEM v továrně nebo místním úložišti](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

- [Nasazení funkce Windows to Go](deploy-windows-to-go.md)  


## <a name="usage"></a>Využití

Když se počítač poprvé spustí po použití předzpracovaného média, počítač se spustí v systému Windows PE. Připojí se k bodu správy a vyhledá pořadí úkolů, které dokončí proces nasazení operačního systému. Když nasadíte pořadí úloh používající Předzpracované médium, klient nejprve zkontroluje platný obsah v místní mezipaměti pořadí úloh. Pokud obsah nebyl nalezen nebo byl revidován, klient stáhne obsah z distribučního bodu nebo partnera.  


## <a name="prerequisites"></a>Požadavky

Než vytvoříte Předzpracované médium pomocí Průvodce vytvořením média pořadí úloh, ujistěte se, že jsou splněné všechny podmínky.

### <a name="boot-image"></a>Spouštěcí image

Vezměte v úvahu následující body spouštěcí bitové kopie, které v pořadí úkolů použijete k nasazení operačního systému:

- Architektura spouštěcí bitové kopie musí být vhodná pro architekturu cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Ale cílový počítač x86 může bootovat a spustit pouze bootovací obrázek x86.
- Ujistěte se, že spouštěcí bitová kopie obsahuje síťové ovladače a ovladače úložiště, které jsou nutné k zřízení cílového počítače.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Vytvoření pořadí úkolů pro nasazení operačního systému

Jako součást předzpracovaného média zadejte pořadí úkolů pro nasazení operačního systému. Další informace najdete v tématu [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuce veškerého obsahu souvisejícího s pořadím úkolů

Distribuujte veškerý obsah, který pořadí úkolů vyžaduje alespoň v jednom distribučním bodě. Tento obsah obsahuje spouštěcí bitovou kopii, bitovou kopii operačního systému a další související soubory. Průvodce shromáždí obsah z distribučního bodu při vytváření předzpracovaného média.

Váš uživatelský účet potřebuje alespoň přístupová práva ke **čtení** knihovny obsahu v tomto distribučním bodě. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Pevný disk v cílovém počítači

Před použitím předzpracovaného média musí být pevný disk cílového počítače naformátován. Pokud není pevný disk naformátován, když je médium použito, pořadí úkolů, které nasadí operační systém, se při pokusu o spuštění cílového počítače nezdařilo.

> [!NOTE]  
> Průvodce vytvořením média pořadí úloh nastavuje na médiu následující podmínku proměnné pořadí úkolů: **_SMSTSMediaType = OEMMedia**. Stejnou podmínku můžete použít ve vašem pořadí úkolů.  


## <a name="process"></a>Proces

 > [!NOTE]  
 > V případě prostředí PKI, vzhledem k tomu, že je kořenová certifikační autorita určena v primární lokalitě, se ujistěte, že jsou předzpracovaná média vytvořena v primární lokalitě. Lokalita CAS neobsahuje informace o kořenové certifikační autoritě pro správné vytvoření předzpracovaného média.

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit médium pořadí úloh**. Tato akce spustí Průvodce vytvořením média pořadí úloh.  

3. Na stránce **Výběr typu média** zadejte následující možnosti:  

    - Vyberte položku **Předzpracované médium**.  

    - Případně, pokud chcete, aby byl operační systém nasazen pouze bez nutnosti zásahu uživatele, vyberte možnost **umožňuje bezobslužné nasazení operačního systému**.  

        > [!IMPORTANT]  
        > Když vyberete tuto možnost, uživateli se nezobrazí výzva k zadání informací o konfiguraci sítě nebo o volitelných sekvencích úloh. Pokud nakonfigurujete médium pro ochranu heslem, bude se uživateli stále zobrazovat výzva k zadání hesla.  

4. Na stránce **Správa média** zadejte jednu z následujících možností:  

    - **Dynamické médium**: umožňuje bodu správy přesměrování média do jiného bodu správy na základě umístění klienta v hranicích lokality.  

    - **Médium založené na webu**: médium pouze kontaktuje zadaný bod správy.  

5. Na stránce **vlastnosti média** zadejte následující informace:  

    - **Vytvořil**: Zadejte, kdo médium vytvořil.  

    - **Verze**: Zadejte číslo verze média.  

    - **Komentář**: Zadejte unikátní popis, k čemu médium slouží.  

    - **Mediální soubor**: Zadejte název výstupních souborů a cestu ke složce, ve které se uloží. Průvodce uloží výstupní soubory do tohoto umístění. Příklad: `\\servername\folder\outputfile.wim`  

    - **Pracovní složka**<!--1359388-->: Proces vytváření médií může vyžadovat mnoho místa na dočasném disku. Ve výchozím nastavení je toto umístění podobné následující cestě: `%UserProfile%\AppData\Local\Temp` . Od verze 1902 získáte větší flexibilitu, kam chcete ukládat tyto dočasné soubory, změňte tuto hodnotu na jinou jednotku a cestu.  

6. Na stránce **zabezpečení** zadejte následující možnosti:  

    - **Povolit podporu neznámých počítačů**: povolí médium nasadit operační systém na počítač, který není spravován nástrojem Configuration Manager. V databázi Configuration Manager neexistují žádné záznamy o těchto počítačích. Další informace najdete v tématu [Příprava pro nasazení do neznámých počítačů](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Chránit médium heslem**: zadejte silné heslo, abyste mohli médium ochránit před neoprávněným přístupem. Pokud zadáte heslo, musí uživatel k použití předzpracovaného média zadat toto heslo.  

        > [!IMPORTANT]  
        > Ke zvýšení ochrany předzpracovaného média doporučujeme vždy nastavit heslo.  
 
    - V případě komunikace HTTP vyberte možnost **vytvořit certifikát média podepsaný svým držitelem**. Pak zadejte datum zahájení a vypršení platnosti certifikátu.  
    
        > [!NOTE] 
        > Vyberete-li tuto možnost, body správy protokolu HTTPS nebudou k dispozici pro výběr na stránce **spouštěcí bitová kopie** tohoto průvodce.

    - V případě komunikace pomocí protokolu HTTPS vyberte možnost **importovat certifikát PKI**. Pak zadejte certifikát, který chcete importovat, a jeho heslo.  

        Další informace o tomto klientském certifikátu, který používají spouštěcí image, najdete v tématu [požadavky na certifikát PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Spřažení zařízení a uživatele**: pro podporu správy zaměřené na uživatele v Configuration Manager určete, jak chcete, aby média spojila uživatele s cílovým počítačem. Další informace o tom, jak nasazení operačního systému podporuje spřažení uživatelských zařízení, najdete v tématu [přidružení uživatelů k cílovému počítači](../get-started/associate-users-with-a-destination-computer.md).  

        - **Povolí spřažení uživatelských zařízení pomocí automatického schválení**: médium automaticky přidruží uživatele k cílovému počítači. Tato funkce je založena na akcích sekvence úloh, která nasazuje operační systém. V tomto scénáři pořadí úkolů vytvoří vztah mezi zadanými uživateli a cílovým počítačem při nasazování operačního systému do cílového počítače.  

        - **Povolení spřažení uživatelských zařízení na schválení správcem**: po udělení schválení médium přidružuje uživatele k cílovému počítači. Tato funkce je založena na rozsahu pořadí úkolů, které nasazuje operační systém. V tomto scénáři pořadí úkolů vytvoří vztah mezi zadanými uživateli a cílovým počítačem, ale před nasazením operačního systému čeká na schválení administrativního uživatele.  

        - **Nepovolit spřažení uživatelských zařízení**: médium nespojuje uživatele s cílovým počítačem. V tomto scénáři pořadí úkolů nepřidruží uživatele k cílovému počítači při nasazení operačního systému.  

7. Na stránce **pořadí úloh** vyberte pořadí úloh, které se spustí na cílovém počítači. Ověřte seznam obsahu, na který odkazuje pořadí úkolů.  

    - **Zjistit přidružené závislosti aplikací a přidat je na toto médium**: přidejte také obsah na médium pro závislosti aplikací.  

        > [!TIP]  
        > Pokud nevidíte očekávané závislosti aplikací, zrušte výběr a pak znovu vyberte tuto možnost, aby se seznam aktualizoval.  

8. Na stránce **spouštěcí bitová kopie** určete následující možnosti:  

    > [!IMPORTANT]  
    > Architektura spouštěcí bitové kopie, kterou distribuujete, musí být vhodná pro architekturu cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Ale cílový počítač x86 může bootovat a spustit pouze bootovací obrázek x86.  

    - **Spouštěcí bitová kopie**: výběrem spouštěcí bitové kopie Spusťte cílový počítač.  

    - **Distribuční bod**: Vyberte distribuční bod, který obsahuje spouštěcí bitovou kopii. Průvodce získá bootovací obrázek z distribučního místa a uloží jej do médií.  

        > [!NOTE]  
        > Váš uživatelský účet potřebuje alespoň oprávnění **ke čtení** knihovny obsahu v distribučním bodě.  

    - **Bod správy**: pouze pro *médium založené na lokalitě*vyberte bod správy z primární lokality.  

    - **Přidružené body správy**: jenom pro *Dynamické médium*, vyberte body správy primární lokality, které se mají použít, a pořadí priorit pro počáteční komunikaci.  

        > [!NOTE]  
        > Body správy s povoleným protokolem HTTPS budou zobrazeny pouze v případě, že je na stránce **zabezpečení** tohoto průvodce uveden certifikát PKI.  

9. Na stránce **bitové kopie** zadejte následující možnosti:  

    - **Balíček bitové kopie**: Určete image operačního systému, která se má použít. Další informace najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).  

    - **Index bitové kopie**: Pokud balíček obsahuje více bitových kopií operačního systému, zadejte index bitové kopie, která se má nasadit.  

    - **Distribuční bod**: zadejte distribuční bod, který má balíček bitové kopie operačního systému. Průvodce získá bitovou kopii operačního systému z distribučního bodu a zapíše ji na médium.  

10. Na stránce **Vybrat aplikaci** vyberte další aplikace, které chcete přidat do souboru předzpracovaného média.  

11. Na stránce **Vybrat balíček** vyberte další balíčky, které chcete přidat do souboru předzpracovaného média.  

12. Na stránce **Vybrat balíček ovladače** vyberte další balíčky ovladačů, které chcete přidat do souboru předzpracovaného média.  

13. Na stránce **distribuční body** vyberte jeden nebo více distribučních bodů, ze kterých se má získat obsah.  

    Configuration Manager zobrazí pouze distribuční body s obsahem. Než budete pokračovat, distribuujte veškerý obsah přidružený k pořadí úkolů alespoň k jednomu distribučnímu bodu. Po distribuci obsahu aktualizujte seznam distribučních bodů. Odeberte všechny distribuční body, které jste už na této stránce vybrali, přejít na předchozí stránku a pak zpátky na stránku **distribuční body** . Případně můžete také restartovat průvodce. Další informace najdete v tématech [distribuce obsahu, na který odkazuje pořadí úkolů](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) , a [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. Na stránce **vlastní nastavení** určete následující možnosti:  

    - Přidejte jakékoli proměnné, které pořadí úkolů používá.  

    - **Povolit příkaz před zahájením**: Zadejte všechny příkazy před zahájením, které chcete spustit před spuštěním pořadí úkolů. Předstartovní příkazy jsou skripty nebo spustitelné soubory, které mohou komunikovat s uživatelem v systému Windows PE před spuštěním pořadí úloh. Další informace najdete v tématu [příkazy před zahájením pro médium pořadí úloh](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Během vytváření média pořadí úkolů zapíše ID balíčku a Předstartovní příkazový řádek, včetně hodnoty všech proměnných pořadí úkolů, do souboru **CreateTSMedia. log** v počítači, ve kterém je spuštěna konzola Configuration Manager. Zkontrolováním tohoto protokolového souboru můžete ověřit hodnoty proměnných sekvence úlohy.  

        Pokud příkaz před zahájením vyžaduje nějaký obsah, vyberte možnost **zahrnout soubory pro předspouštěcí příkaz**.  

15. Dokončete průvodce.  


## <a name="next-steps"></a>Další kroky

[Vytvoření image pro výrobce OEM v továrně nebo místním úložišti](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
