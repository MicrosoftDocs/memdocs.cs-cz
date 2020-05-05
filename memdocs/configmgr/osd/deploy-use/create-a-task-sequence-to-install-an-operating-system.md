---
title: Vytvoření pořadí úkolů pro instalaci operačního systému
titleSuffix: Configuration Manager
description: Pomocí pořadí úkolů v Configuration Manager automaticky nainstalovat image operačního systému a další obsah do cílového počítače.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e1b298856edea3f81cab2e9cd5ab75af49dff51
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723009"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Vytvoření pořadí úkolů pro instalaci operačního systému

*Platí pro: Configuration Manager (Current Branch)*

Pomocí pořadí úkolů v Configuration Manager automaticky nainstalovat image operačního systému do cílového počítače. Vytvoříte pořadí úkolů, které odkazuje na spouštěcí image sloužící ke spuštění cílového počítače, image operačního systému, kterou chcete nainstalovat na cílový počítač, a jakýkoli další obsah, jako jsou například jiné aplikace nebo aktualizace softwaru, které chcete nainstalovat. Potom nasadíte pořadí úkolů do kolekce, která obsahuje cílový počítač.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a>Vytvoření pořadí úkolů pro instalaci operačního systému

Existuje několik scénářů nasazení operačního systému do počítačů ve vašem prostředí. Ve většině případů vytvoříte pořadí úkolů a v Průvodci vytvořením pořadí úloh vyberete **instalovat existující balíček bitové kopie** . Tato možnost vytvoří pořadí úloh, které nainstaluje operační systém, migruje nastavení uživatele, nainstaluje aktualizace softwaru a nainstaluje aplikace.

### <a name="prerequisites"></a>Požadavky

Než vytvoříte pořadí úkolů pro instalaci operačního systému, musí být zavedeny tyto požadavky:

#### <a name="required"></a>Požaduje se

- [Spouštěcí bitová kopie](../get-started/manage-boot-images.md)  

- [Bitová kopie operačního systému](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Požaduje se (pokud se používá)

- Synchronizovat [aktualizace softwaru](../../sum/get-started/synchronize-software-updates.md)  

- Přidat [aplikace](../../apps/deploy-use/create-applications.md)  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Postup vytvoření pořadí úloh, které nainstaluje operační systém  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pořadí úloh**. Tato akce spustí Průvodce vytvořením pořadí úloh.  

3. Na stránce **vytvořit nové pořadí úloh** vyberte **instalovat existující balíček bitových kopií**a pak vyberte **Další**.  

4. Na stránce **informace o pořadí úloh** zadejte následující nastavení:  

    - **Název pořadí úkolů**: Zadejte název, který identifikuje pořadí úkolů.  

    - **Popis**: zadejte popis toho, co má pořadí úkolů dělat.  

    - **Spouštěcí bitová kopie**: Určete spouštěcí bitovou kopii, kterou pořadí úkolů používá k instalaci operačního systému do cílového počítače. Spouštěcí bitová kopie obsahuje verzi systému Windows PE a všechny další požadované ovladače zařízení. Další informace najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        > Architektura spouštěcí bitové kopie musí být kompatibilní s hardwarovou architekturou cílového počítače.  

5. Na stránce **instalovat systém Windows** zadejte následující nastavení:  

    - **Balíček bitové kopie**: Zadejte balíček obsahující bitovou kopii operačního systému, která se má nainstalovat. Další informace najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).  

    - **Image**: Pokud balíček image operačního systému obsahuje více imagí, určete index image operačního systému, který chcete nainstalovat.  

    - **Rozdělení a naformátování cílového počítače**, na který se instaluje operační systém: Určete, jestli má pořadí úkolů před instalací operačního systému vytvořit oddíly a naformátovat cílový počítač.  

    - **Kód Product Key**: v případě potřeby zadejte kód Product Key systému Windows. Zadávat lze šifrované aktivační kódy VLK a standardní kódy Product Key. Pokud používáte nekódovaný kód Product Key, musí být každá skupina pěti znaků oddělená pomlčkou (`-`). Příklad: *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*  

    - **Režim licence serveru**: Zadejte, jestli serverová licence je **Na stanici**, **Na server**nebo není zadaná žádná licence. Pokud je licence serveru **Na server**, zadejte také maximální počet připojení serverů.  

    - Určete, jak se má zpracovat účet správce pro nový operační systém:  

        - **Náhodně generovat heslo účtu místního správce a vypnout účet na všech podporovaných platformách (doporučeno)**: systém Windows zakáže účet místního správce poté, co pořadí úkolů nasadí bitovou kopii operačního systému.  

        - **Povolit účet a zadat heslo místního správce**: systém Windows používá stejné heslo pro účet místního správce na všech počítačích, kde pořadí úkolů nasadí bitovou kopii operačního systému.  

6. Na stránce **Konfigurovat síť** určete následující nastavení:  

    - **Připojit k pracovní skupině**: přidejte cílový počítač do pracovní skupiny.  

    - **Připojit k doméně**: přidejte cílový počítač k doméně. Do pole **Doména** zadejte název domény.  

        > [!IMPORTANT]  
        > Doménu v místní doménové struktuře lze vyhledat, ale název domény ve vzdálené doménové struktuře je nutné zadat.  

        V poli **OJ domény** můžete také zadat organizační jednotku (OU). Toto nastavení je volitelné a určuje rozlišující název protokolu LDAP X. 500 pro organizační jednotku. Pokud ještě neexistuje, vytvoří Windows účet počítače v této organizační jednotce.  

    - **Účet**: uživatelské jméno a heslo účtu, který má oprávnění připojit se k zadané doméně. Například: *doména\uživatel* nebo *%proměnná%*.  

        > [!IMPORTANT]  
        > Pokud plánujete migrovat nastavení domény nebo nastavení pracovní skupiny, zadejte příslušné přihlašovací údaje do domény.  

7. Na stránce **Configuration Manager instalace** Určete balíček klienta Configuration Manager, který chcete nainstalovat na cílový počítač. Můžete také zahrnout všechny vlastnosti instalace.  

8. Na stránce **migrace stavu** zadejte následující informace:  

    - **Zaznamenat uživatelská nastavení**: pořadí úkolů zachytí stav uživatele. Další informace o tom, jak zachytit a obnovit stav uživatele, najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  

    - **Zaznamenat nastavení sítě**: pořadí úkolů zachycuje nastavení sítě z cílového počítače. Zachycuje členství v doméně nebo pracovní skupině, a to i nastavení síťového adaptéru.  

    - **Zaznamenat nastavení systému Microsoft Windows**: pořadí úkolů zachycuje nastavení systému Windows z cílového počítače před tím, než nainstaluje bitovou kopii operačního systému. Zachycuje název počítače, jméno registrovaného uživatele a organizace a nastavení časového pásma.  

9. Na stránce **Zahrnout aktualizace** určete, zda se mají nainstalovat požadované aktualizace softwaru, všechny aktualizace softwaru nebo žádné aktualizace softwaru. Pokud určíte, že se mají instalovat aktualizace softwaru, Configuration Manager nainstaluje jenom aktualizace softwaru, které jsou cílené na kolekce, kterých je cílový počítač členem.  

10. Na stránce **instalovat aplikace** určete aplikace, které chcete do cílového počítače nainstalovat. Pokud zvolíte více aplikací, můžete také určit, aby pořadí úloh pokračovalo i v případě, že bude instalace některé z aplikací neúspěšná.  

11. Dokončete průvodce.  

Teď můžete pořadí úkolů nasadit do kolekce počítačů. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Obsah předběžné mezipaměti

<!--4224642-->
Počínaje verzí 1906 můžete tento typ pořadí úloh povolit pro předběžné ukládání obsahu do mezipaměti. Funkce pre-cache pro dostupná nasazení pořadí úkolů umožňuje klientům stáhnout relevantní obsah předtím, než uživatel nainstaluje pořadí úkolů.  

Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a>Příklad pořadí úkolů

Při vytváření pořadí úkolů, které nasadí operační systém pomocí existující image, použijte jako vodítko následující tabulku. Tabulka vám pomůže určit obecné pořadí kroků pořadí úkolů a postup uspořádání a strukturování těchto kroků pořadí úkolů do logických skupin. Pořadí úkolů, které vytvoříte, se může od této ukázky lišit a může obsahovat víc nebo míň skupin a kroků pořadí úkolů.  

> [!NOTE]  
> Pomocí Průvodce vytvořením pořadí úloh vytvořte toto pořadí úloh.  
>
> Když pro vytvoření tohoto nového pořadí úkolů použijete Průvodce vytvořením pořadí úloh, některé z názvů kroků se liší od toho, jak by se použily v případě, že jste tyto kroky pořadí úkolů přidali do existujícího pořadí úkolů ručně.

|Skupina nebo krok pořadí úloh|Popis|  
|---------------------------------|-----------------|  
|Zachytávací soubor a nastavení – **(nová skupina pořadí úkolů)**|Vytvořte skupinu pořadí úkolů. Skupina pořadí úkolů udržuje podobné kroky pořadí úkolů pohromadě. Zajistí se tak lepší uspořádání a řízení chyb.<br /><br /> Tato skupina obsahuje kroky potřebné pro zaznamenání souborů a nastavení z operačního systému v referenčním počítači.|  
|Zaznamenat nastavení systému Windows|Tento krok pořadí úkolů můžete použít k určení nastavení systému Microsoft Windows, které se má zaznamenat z referenčního počítače. Můžete zaznamenat název počítače, jméno uživatele a organizace a nastavení časového pásma.|  
|Zaznamenat nastavení sítě|Tento krok pořadí úkolů umožňuje zaznamenat nastavení sítě z referenčního počítače. Můžete zaznamenat členství referenčního počítače v doméně nebo pracovní skupině a informace o nastavení síťového adaptéru.|  
|Zaznamenání uživatelských souborů a nastavení – **(nová podskupina pořadí úkolů)**|Umožňuje vytvořit skupinu pořadí úkolů v rámci jiné skupiny pořadí úkolů. Tato podskupina obsahuje kroky potřebné k zaznamenání dat stavu uživatele. Podobně jako u počáteční skupiny, kterou jste přidali, tato podskupina udržuje podobné kroky pořadí úkolů společně pro lepší uspořádání a řízení chyb.|  
|Vyžádání úložiště stavů uživatele|Tento krok pořadí úkolů umožňuje požádat o přístup k bodu migrace stavu, ve kterém jsou uložená data stavu uživatele. Tento krok pořadí úkolů můžete nakonfigurovat tak, aby zaznamenával nebo obnovoval informace o stavu uživatele.|  
|Zaznamenání uživatelských souborů a nastavení|Pomocí tohoto kroku pořadí úkolů můžete pomocí Nástroj pro migraci uživatelských souborů a nastavení (USMT) zachytit stav uživatele a nastavení z referenčního počítače, který obdrží pořadí úkolů přidružené k tomuto kroku úlohy. Můžete zachytit standardní možnosti nebo nakonfigurovat, které možnosti chcete zachytit.|  
|Uvolnění úložiště stavů uživatele|Pomocí tohoto kroku pořadí úkolů můžete bodu migrace stavu oznámit, že se dokončila akce zaznamenávání nebo obnovení.|  
|Nainstalovat operační systém – **(nová skupina pořadí úkolů)**|Vytvořte další podskupinu pořadí úkolů. Tato podskupina obsahuje kroky potřebné k instalaci a konfiguraci prostředí Windows PE.|  
|Restartování v prostředí Windows PE|Pomocí tohoto kroku pořadí úkolů můžete určit možnosti restartování pro cílový počítač, který bude příjemcem pořadí úkolů. Tento krok zobrazí uživateli zprávu, že se počítač bude restartovat, aby mohla pokračovat instalace.<br /><br /> Tento krok používá proměnnou pořadí úkolů **_SMSTSInWinPE** , která je jen pro čtení. Pokud je přidružená hodnota **false**, bude tento krok pořadí úkolů pokračovat.|  
|Rozdělení disku na oddíly 0|Tento krok pořadí úkolů umožňuje zadat akce potřebné k formátování pevného disku v cílovém počítači. Výchozí číslo disku je **0**.<br /><br /> Tento krok používá proměnnou pořadí úkolů **_SMSTSClientCache** , která je jenom pro čtení. Tento krok se spustí, pokud Configuration Manager mezipaměť klienta neexistuje.|  
|Použít operační systém|Pomocí tohoto kroku pořadí úkolů nainstalujete image operačního systému na cílový počítač. Tento krok nejprve odstraní všechny soubory na svazku s výjimkou jakýchkoli souborů ovládacích prvků specifických pro Configuration Manager. Pak použije všechny image svazků obsažené v souboru. WIM na odpovídající sekvenční diskový svazek v cílovém počítači. Můžete určit soubor odpovědí **sysprep** a také nastavit diskový oddíl, který se má použít k instalaci.|  
|Použít nastavení systému Windows|Pomocí tohoto kroku pořadí úkolů nakonfigurujte konfigurační informace pro nastavení Windows pro cílový počítač. Mezi nastavení systému Windows, která můžete použít, patří informace o uživateli a organizaci, informace o produktu nebo licenčním kódu, časové pásmo a heslo místního správce.|  
|Použít nastavení sítě|Pomocí tohoto kroku pořadí úkolů můžete určit informace o konfiguraci sítě nebo pracovní skupiny pro cílový počítač. Můžete také zadat, jestli počítač používá server DHCP, nebo přiřadit informace o IP adrese staticky.|  
|Použít ovladače zařízení|Tento krok pořadí úkolů umožňuje instalovat ovladače v rámci nasazení operačního systému. Výběrem **Nabídnout ovladače ze všech kategorií** Instalačnímu programu systému Windows povolíte, aby prohledal všechny existující kategorie ovladačů. Pokud chcete kategorie ovladačů prohledávané Instalačním programem systému Windows omezit, vyberte **Omezit zobrazené ovladače pouze na nabídnuté ovladače z vybraných kategorií**.<br /><br /> Tento krok používá proměnnou pořadí úkolů **_SMSTSMediaType** , která je jen pro čtení. Tento krok pořadí úkolů se spustí jenom v případě, že hodnota proměnné se nerovná **FullMedia**.|  
|Použít balíček ovladače|Tento krok pořadí úkolů umožňuje zpřístupnit všechny ovladače zařízení v určitém balíčku ovladačů pro použití instalačním programem systému Windows.|  
|Nastavení operačního systému – **(nová skupina pořadí úkolů)**|Vytvořte další podskupinu pořadí úkolů. Tato podskupina obsahuje kroky potřebné k nastavení nainstalovaného operačního systému.|  
|Nastavit systém Windows a nástroj ConfigMgr|Pomocí tohoto kroku pořadí úkolů nainstalujete Configuration Manager klientský software. Configuration Manager nainstaluje a zaregistruje identifikátor GUID Configuration Manager klienta. Všechny nezbytné instalační parametry můžete přiřadit v okně **Vlastnosti instalace** .|  
|Instalovat aktualizace|Tento krok pořadí úkolů umožňuje určit, jak se mají aktualizace softwaru instalovat do cílového počítače. V cílovém počítači se nevyhodnocují příslušné aktualizace softwaru, dokud se tento krok pořadí úkolů nespustí. V tomto okamžiku se v cílovém počítači vyhodnotí aktualizace softwaru podobně jako u kteréhokoli jiného klienta spravovaného Configuration Manager.<br /><br /> Tento krok používá proměnnou pořadí úkolů **_SMSTSMediaType** , která je jen pro čtení. Tento krok pořadí úkolů se spustí jenom v případě, že hodnota proměnné se nerovná **FullMedia**.|  
|Obnovení uživatelských souborů a nastavení – **(nová podskupina pořadí úkolů)**|Vytvořte další podskupinu pořadí úkolů. Tato podskupina obsahuje kroky potřebné k obnovení uživatelských souborů a nastavení.|  
|Vyžádání úložiště stavů uživatele|Tento krok pořadí úkolů umožňuje požádat o přístup k bodu migrace stavu, ve kterém jsou uložená data stavu uživatele.|  
|Obnovení uživatelských souborů a nastavení|Pomocí tohoto kroku pořadí úkolů můžete spustit Nástroj pro migraci uživatelských souborů a nastavení (USMT), chcete-li obnovit stav a nastavení uživatele do cílového počítače.|  
|Uvolnění úložiště stavů uživatele|Pomocí tohoto kroku pořadí úkolů můžete bodu migrace stavu oznámit, že data o stavu uživatele už nejsou potřebná.|  
