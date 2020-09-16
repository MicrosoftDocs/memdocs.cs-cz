---
title: Kroky pořadí úkolů
titleSuffix: Configuration Manager
description: Přečtěte si o krocích, které můžete přidat do Configuration Manager pořadí úkolů.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49792ea588f01cc57a1dbce9cc137b94a0e4d291
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574792"
---
# <a name="task-sequence-steps"></a>Kroky pořadí úkolů

*Platí pro: Configuration Manager (Current Branch)*

Do pořadí úkolů Configuration Manager lze přidat následující kroky pořadí úkolů. Další informace najdete v tématu [použití editoru pořadí úloh](task-sequence-editor.md).  

## <a name="common-settings"></a>Obecná nastavení

Následující nastavení jsou společná pro všechny kroky pořadí úloh:

### <a name="properties-for-all-steps"></a>Vlastnosti všech kroků

- **Název**: Editor pořadí úloh vyžaduje, abyste zadali krátký název, který popisuje tento krok. Když přidáte nový krok, Editor pořadí úkolů nastaví jako výchozí název typ. Délka **názvu** nesmí překročit 50 znaků.  

- **Popis**: Volitelně můžete zadat podrobnější informace o tomto kroku. Délka **popisu** nesmí překročit 256 znaků.  

Zbývající část tohoto článku popisuje další nastavení na kartě **vlastnosti** jednotlivých kroků pořadí úkolů.

### <a name="options-for-all-steps"></a>Možnosti pro všechny kroky

- **Zakázat tento krok**: pořadí úkolů tento krok přeskočí, když běží na počítači. Ikona tohoto kroku je šedá v editoru pořadí úloh.  

- **Pokračovat při chybě**: Pokud při spuštění kroku dojde k chybě, pořadí úkolů bude pokračovat. Další informace najdete v tématu [požadavky na plánování pro automatizaci úloh](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups).  

- **Přidat podmínku**: pořadí úkolů vyhodnotí tyto podmíněné příkazy a určí, zda spustí krok. Příklad použití proměnné pořadí úkolů jako podmínky najdete v tématu [Použití proměnných pořadí úkolů](using-task-sequence-variables.md#bkmk_access-condition). Další informace o podmínkách najdete v tématu [Editor pořadí úloh – podmínky](task-sequence-editor.md#bkmk_conditions).

Níže uvedené části pro konkrétní kroky pořadí úkolů popisují další možná nastavení na kartě **Možnosti** .



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> Použít data bitové kopie

Pomocí tohoto kroku můžete zkopírovat bitovou kopii dat do zadaného cílového oddílu.  

Tento krok běží jenom v prostředí Windows PE. Neběží v plném operačním systému.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové**kopie a zvolte možnost **použít bitovou kopii dat**.

### <a name="variables-for-apply-data-image"></a>Proměnné pro obrázek použití dat

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Rutiny pro bitovou kopii použití dat

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage)
- [New-CMTSStepApplyDataImage](/powershell/module/configurationmanager/New-CMTSStepApplyDataImage)
- [Remove-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage)
- [Set-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage)

### <a name="properties-for-apply-data-image"></a>Vlastnosti pro obrázek použití dat

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="image-package"></a>Balíček bitové kopie

Vyberte **Procházet** a zadejte **balíček bitové kopie** použitý tímto pořadím úkolů. V dialogovém okně **Vybrat balíček** vyberte balíček, který chcete nainstalovat. V dolní části dialogového okna se zobrazí informace o přidružené vlastnosti pro každý balíček bitové kopie. Pomocí rozevíracího seznamu vyberte **image**, kterou chcete z vybraného **balíčku imagí** nainstalovat.  

> [!NOTE]  
> Tato akce pořadí úkolů zpracovává bitovou kopii jako datový soubor. Tato akce neprovádí žádné nastavení pro spuštění bitové kopie jako operačního systému.  

#### <a name="destination"></a>Cíl

Nakonfigurujte jednu z následujících možností:

- **Další dostupný oddíl**: použijte další sekvenční oddíl, který krok **použít operační systém** nebo **použít data bitové kopie** v tomto pořadí úkolů ještě necílí.  

- **Konkrétní disk a oddíl**: vyberte číslo **disku** (počínaje 0) a číslo **oddílu** (počínaje 1).  

- **Specifické písmeno logické jednotky**: zadejte **písmeno jednotky** , které systém Windows PE přiřadí k oddílu. Toto písmeno jednotky se může lišit od písmene jednotky přiřazeného nově nasazeným operačním systémem.  

- **Písmeno logické jednotky uložené v proměnné**: zadejte proměnnou pořadí úkolů obsahující písmeno jednotky přiřazené oddílu prostředím Windows PE. Tato proměnná se obvykle nastavuje v části Upřesnit dialogového okna **Vlastnosti oddílu** pro krok pořadí úkolů **Formátovat a rozdělit disk na oddíly** .  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Před použitím bitové kopie odstranit veškerý obsah v oddílu  

Určuje, že před instalací bitové kopie pořadí úkolů odstraní všechny soubory v cílovém oddílu. Když neodstraníte obsah oddílu, dá se tato akce použít k použití dalšího obsahu na dříve cílový oddíl.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Použít balíček ovladače  

Pomocí tohoto kroku stáhnete všechny ovladače v balíčku ovladačů a nainstalujete je do operačního systému Windows.

Krok pořadí úkolů **Použít balíček ovladače** zpřístupní všechny ovladače zařízení v balíčku ovladačů pro použití v systému Windows. Přidejte tento krok mezi kroky **použít operační systém** a **nastavit systém Windows a nástroj ConfigMgr** , aby byly ovladače v balíčku k dispozici pro systém Windows. Krok pořadí úkolů **Použít balíček ovladače** je taky užitečný v případě nasazování ze samostatných médií.  

Podobné ovladače zařízení umístěte do balíčku ovladačů a distribuujte je do příslušných distribučních bodů. Například do balíčku ovladačů umístěte všechny ovladače od jednoho výrobce. Pak balíček distribuujte do distribučních bodů, kde k nim mají přidružené počítače přístup.

Krok **použít balíček ovladače** je vhodný pro samostatné médium. Tento krok je vhodný také pro instalaci konkrétní sady ovladačů. Mezi tyto typy ovladačů patří zařízení, která Windows Plug-and-Play nedetekuje, třeba síťové tiskárny.  

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **ovladače**a vyberte možnost **použít balíček ovladače**.

> [!TIP]
> Přehled ovladačů v Configuration Manager najdete v tématu [instalace ovladačů pomocí pořadí úloh](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Pokud chcete stáhnout příslušný balíček ovladačů před tím, než uživatel nainstaluje pořadí úkolů, použijte předběžné ukládání obsahu do mezipaměti. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).

### <a name="variables-for-apply-driver-package"></a>Proměnné pro použití balíčku ovladačů

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Rutiny pro použití balíčku ovladačů

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage)
- [New-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage)
- [Remove-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage)
- [Set-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage)

### <a name="properties-for-apply-driver-package"></a>Vlastnosti pro použití balíčku ovladačů

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="driver-package"></a>Balíček ovladačů

Zadejte balíček ovladačů, který obsahuje potřebné ovladače zařízení. Vyberte **Procházet** a otevřete dialogové okno **Vybrat balíček** . Vyberte existující balíček ovladačů, který chcete použít. V dolní části dialogového okna se zobrazí vlastnosti přidruženého balíčku.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Instalovat balíček ovladačů přes spuštění DISM s možností rekurze

Tuto možnost vyberte, pokud chcete přidat `/recurse` parametr do příkazového řádku DISM, když systém Windows použije balíček ovladačů.

Pokud povolíte tuto možnost, můžete také zadat další parametry příkazového řádku DISM. K zahrnutí dalších možností použijte proměnnou pořadí úloh [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) . Další informace najdete v tématu [Možnosti příkazového řádku Windows 10 DISM](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Vyberte ovladač velkokapacitního úložiště, který musí být nainstalovaný před tím, než Configuration Manager nainstaluje operační systém starší než Windows Vista

Zadejte všechny ovladače velkokapacitních paměťových zařízení potřebné k instalaci klasického operačního systému.  

##### <a name="driver"></a>Ovladač

Vyberte soubor ovladače velkokapacitního úložiště, který se má nainstalovat před instalací klasického operačního systému. Rozevírací seznam se naplní ze zadaného balíčku.  

##### <a name="model"></a>Modelování

Zadejte zařízení kritické pro spouštění, které je potřeba pro nasazení z operačního systému staršího než Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Provést bezobslužnou instalaci nepodepsaných ovladačů ve verzích systému Windows, kde je to povoleno 

Tato možnost umožňuje systému Windows instalovat ovladače bez digitálního podpisu.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> Použít nastavení sítě  

Pomocí tohoto kroku zadejte informace o konfiguraci sítě nebo pracovní skupiny pro cílový počítač. Pořadí úkolů ukládá tyto hodnoty do příslušného souboru odpovědí. Instalační program systému Windows používá tento soubor odpovědí během akce **nastavit systém Windows a nástroj ConfigMgr** .  

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte **Nastavení**a zvolte možnost **použít nastavení sítě**.

> [!NOTE]
> Pokud zahrnete více instancí tohoto kroku v pořadí úkolů, podmínky se nepoužijí. Nastavení z poslední instance tohoto kroku v pořadí úkolů se aplikují na zařízení. Pokud chcete toto chování obejít, zahrňte každý krok do samostatné skupiny s podmínkami pro skupinu.

### <a name="variables-for-apply-network-settings"></a>Proměnné pro použití nastavení sítě

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Rutiny pro použití nastavení sítě

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting)
- [New-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting)
- [Remove-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting)
- [Set-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting)

### <a name="properties-for-apply-network-settings"></a>Vlastnosti použití nastavení sítě

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="join-a-workgroup"></a>Připojit k pracovní skupině

Tuto možnost vyberte, pokud chcete mít cílový počítač připojený ke konkrétní pracovní skupině. Na řádku **Pracovní skupina** zadejte název pracovní skupiny. Hodnota, kterou zachytí krok pořadí úkolů zaznamenat **nastavení sítě** , může tuto hodnotu přepsat.

#### <a name="join-a-domain"></a>Připojení k doméně

Tuto možnost vyberte, pokud chcete mít cílový počítač připojený ke konkrétní doméně. Zadejte nebo přejděte k doméně, například `fabricam.com` . Zadejte nebo vyhledejte cestu protokolu LDAP (Lightweight Directory Access Protocol) pro organizační jednotku. Například: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

> [!NOTE]
> Když klient připojený k Azure Active Directory (Azure AD) spustí pořadí úloh nasazení operačního systému, klient v novém operačním systému se automaticky nepřipojí k Azure AD. I když není připojený k Azure AD, klient se pořád spravuje.

#### <a name="account"></a>Účet

Vyberte možnost **nastavit** a zadejte účet s potřebnými oprávněními pro připojení počítače k doméně. V dialogovém okně **uživatelský účet systému Windows** zadejte uživatelské jméno v následujícím formátu: `Domain\User` . Další informace najdete v tématu [účet pro připojení k doméně](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Nastavení adaptéru

Zadejte konfigurace sítě pro každý síťový adaptér v počítači. Výběrem možnosti **nové** otevřete dialogové okno **nastavení sítě** a pak zadejte nastavení sítě.

- Pokud použijete také krok **zaznamenat nastavení sítě** , použije pořadí úloh dříve zaznamenané nastavení na síťový adaptér.
- Pokud pořadí úkolů předtím nezachytí nastavení sítě, použije se nastavení, které zadáte v tomto kroku.
- Pořadí úkolů používá tato nastavení pro síťové adaptéry v pořadí výčtu zařízení Windows.  
- Pořadí úkolů okamžitě nepoužije nastavení, které zadáte v tomto kroku do počítače.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Použít bitovou kopii operačního systému  

Pomocí tohoto kroku nainstalujete operační systém na cílový počítač.

Po spuštění akce **použít operační systém** nastaví proměnnou **OSDTargetSystemDrive** na písmeno jednotky oddílu, který obsahuje soubory operačního systému.  

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové**kopie a zvolte možnost **použít bitovou kopii operačního systému**.

> [!TIP]
> Počínaje systémem Windows 10 verze 1709 obsahuje médium více edicí. Když nakonfigurujete pořadí úkolů tak, aby používalo balíček s upgradem operačního systému nebo bitovou kopii operačního systému, je nutné vybrat [podporovanou edici](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Pokud chcete stáhnout příslušný balíček s upgradem pro operační systém před tím, než uživatel nainstaluje pořadí úkolů, použijte předběžné ukládání obsahu do mezipaměti. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).
>
> Krok **nastavit systém Windows a nástroj ConfigMgr** spustí instalaci systému Windows.

### <a name="variables-for-apply-os-image"></a>Proměnné pro bitovou kopii použití operačního systému

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>Rutiny pro použití bitové kopie operačního systému

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem)
- [New-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem)
- [Remove-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem)
- [Set-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem)

### <a name="behaviors-for-apply-os-image"></a>Chování pro bitovou kopii použití operačního systému

Tento krok provádí různé akce v závislosti na tom, jestli používá bitovou kopii operačního systému nebo balíček s upgradem operačního systému.  

#### <a name="os-image-actions"></a>Akce s bitovou kopií operačního systému

Při použití bitové kopie operačního systému provede krok **použít bitovou kopii operačního systému** následující akce:  

1. Odstraňte veškerý obsah na cílovém svazku s výjimkou souborů ve složce určené proměnnou ** \_ SMSTSUserStatePath** .  

2. Extrahuje obsah zadaného souboru. wim do zadaného cílového oddílu.  

3. Připravte soubor odpovědí:  

    1. Vytvoří nový výchozí soubor odpovědí instalační program systému Windows (Sysprep. inf nebo unattend.xml) pro nasazený operační systém.  

    2. Sloučí všechny hodnoty ze souboru odpovědí zadaného uživatelem.  

4. Zkopírujte do aktivního oddílu zavaděče spouštění systému Windows.  

5. Nastavte boot.ini nebo konfigurační databázi BCD (Boot Configuration Database) tak, aby odkazovaly na nově nainstalovaný operační systém.  

#### <a name="os-upgrade-package-actions"></a>Akce balíčku pro upgrade operačního systému

Když použijete balíček s upgradem operačního systému, provede krok **použít bitovou kopii operačního systému** následující akce:  

1. Odstraňte veškerý obsah na cílovém svazku s výjimkou souborů ve složce určené proměnnou ** \_ SMSTSUserStatePath** .  

2. Připravte soubor odpovědí:  

    1. Vytvoří nový soubor odpovědí se standardními hodnotami vytvořenými nástrojem Configuration Manager.  

    2. Sloučí všechny hodnoty ze souboru odpovědí zadaného uživatelem.  

### <a name="properties-for-apply-os-image"></a>Vlastnosti pro bitovou kopii použití operačního systému

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Použít operační systém ze zaznamenané bitové kopie

Nainstaluje bitovou kopii operačního systému, kterou jste si poznamenali. Vyberte **Procházet** a otevřete dialogové okno **Vybrat balíček** . Pak vyberte existující balíček bitové kopie, který chcete nainstalovat. Pokud je k zadanému **balíčku bitové kopie**přidruženo více imagí, vyberte z rozevíracího seznamu přidružený obrázek, který chcete použít pro toto nasazení. Základní informace o každé existující imagi si můžete zobrazit tak, že ji vyberete.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Použít operační systém z originálního zdroje instalace

Nainstaluje operační systém pomocí balíčku s upgradem operačního systému, který je také původním zdrojem instalace. Vyberte **Procházet** a otevřete dialogové okno **Vybrat balíček s upgradem operačního systému** . Pak vyberte existující balíček s upgradem operačního systému, který chcete použít. Výběrem této možnosti zobrazíte základní informace o jednotlivých existujících zdrojích imagí. V podokně výsledků v dolní části dialogového okna se zobrazí vlastnosti přidruženého zdroje obrázku. Pokud je k zadanému balíčku přidruženo několik edicí, použijte rozevírací seznam a vyberte **edici** , kterou chcete použít.  

> [!NOTE]  
> **Balíčky s upgradem operačního systému** jsou primárně určeny pro použití s místními upgrady, nikoli pro nové instalace systému Windows. Při nasazování nových instalací systému Windows použijte možnost **použít operační systém ze zaznamenané bitové kopie** a ze zdrojových instalačních souborů **nainstalujte. wim** .
>
> Nasazení nových instalací Windows přes **balíčky s upgradem operačního systému** se pořád podporuje, ale závisí na ovladačích, které jsou s touto metodou kompatibilní. Při instalaci systému Windows z balíčku pro upgrade operačního systému jsou ovladače nainstalovány i v systému Windows PE, a to pouhým vložením v prostředí Windows PE. Některé ovladače nejsou kompatibilní s instalací v prostředí Windows PE.
>
> Pokud ovladače nejsou kompatibilní s instalací nástroje v prostředí Windows PE, pak z původních zdrojových souborů instalace vytvořte **bitovou kopii operačního systému** pomocí souboru **install. wim** . Místo toho proveďte nasazení prostřednictvím možnosti **použít operační systém z digitalizované bitové kopie** .

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Pro vlastní instalaci použít bezobslužný soubor odpovědi nebo soubor odpovědi Sysprep

Pomocí této možnosti můžete zadat soubor odpovědí instalačního programu systému Windows (**unattend.xml**, **unattend.txt**nebo **Sysprep. inf**) v závislosti na verzi operačního systému a metodě instalace. Soubor, který zadáte, může zahrnovat kteroukoliv ze standardních možností konfigurace podporovanou soubory odpovědí systému Windows. Například můžete pomocí něj určit výchozí domovskou stránku Internet Exploreru. Zadejte balíček, který obsahuje soubor odpovědí, a přidruženou cestu k souboru v balíčku.  

> [!NOTE]  
> Soubor odpovědí instalačního programu systému Windows, který zadáte, může obsahovat vložené proměnné pořadí úkolů ve formuláři `%varname%` , kde *název_proměnné* je název proměnné. Krok **nastavit systém Windows a nástroj ConfigMgr** nahradí proměnnou řetězcem pro skutečnou hodnotu proměnné. Tyto vložené proměnné pořadí úkolů nemůžete použít v souboru odpovědí unattend.xml jenom v číselném poli.  

Pokud soubor odpovědí instalace systému Windows nezadáte, pořadí úloh automaticky vygeneruje soubor odpovědí.  

#### <a name="destination"></a>Cíl

Nakonfigurujte jednu z následujících možností:  

- **Další dostupný oddíl**: použijte další sekvenční oddíl, který se už nezaměřuje na krok **použít operační systém** nebo **použít pro obrázek data** v tomto pořadí úkolů.  

- **Konkrétní disk a oddíl**: vyberte číslo **disku** (počínaje 0) a číslo **oddílu** (počínaje 1).  

- **Konkrétní písmeno logické jednotky**: zadejte **písmeno jednotky** přiřazené oddílu prostředím Windows PE. Toto písmeno jednotky se může lišit od písmene jednotky přiřazeného nově nasazeným operačním systémem.  

- **Písmeno logické jednotky uložené v proměnné**: zadejte proměnnou pořadí úkolů obsahující písmeno jednotky přiřazené oddílu prostředím Windows PE. Tato proměnná se obvykle nastavuje v části Upřesnit dialogového okna **Vlastnosti oddílu** pro krok pořadí úkolů **Formátovat a rozdělit disk na oddíly** .  

### <a name="options-for-apply-os-image"></a>Možnosti použití bitové kopie operačního systému

Kromě výchozích možností nakonfigurujte na kartě **Možnosti** tohoto kroku pořadí úkolů následující další nastavení:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Přístup k obsahu přímo z distribučního bodu

Nakonfigurujte pořadí úkolů pro přístup k bitové kopii operačního systému přímo z distribučního bodu. Tuto možnost můžete například použít při nasazování operačních systémů do integrovaných zařízení, která mají omezené kapacity úložiště. Když vyberete tuto možnost, nakonfigurujte také nastavení sdílení balíčku na kartě **přístup k datům** ve vlastnostech image operačního systému.  

> [!NOTE]  
> Toto nastavení potlačí možnost nasazení, kterou nakonfigurujete na stránce **distribuční body** v **Průvodci nasazením softwaru**. Toto přepsání je určeno pouze pro bitovou kopii operačního systému, kterou tento krok určuje, nikoli pro veškerý obsah pořadí úloh.  

> [!IMPORTANT]  
> Pro největší zabezpečení se důrazně doporučuje, abyste tuto možnost nevybrali. Tato možnost je navržená hlavně pro použití na zařízeních s omezeným množstvím úložiště. Tato možnost není určena k zvýšení rychlosti pořadí úkolů. Pokud je vybrána tato možnost, není pro balíček operačního systému ověřena hodnota hash balíčku. Proto nelze zajistit integritu balíčku, protože je možné, že uživatelé s právy správce mohou měnit nebo manipulovat s obsahem balíčku.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Použít nastavení systému Windows

Pomocí tohoto kroku můžete nakonfigurovat nastavení systému Windows pro cílový počítač. Pořadí úkolů ukládá tyto hodnoty do příslušného souboru odpovědí. Instalační program systému Windows používá tento soubor odpovědí během kroku **nastavit systém Windows a nástroj ConfigMgr** .  

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte **Nastavení**a zvolte možnost **použít nastavení systému Windows**.

### <a name="variables-for-apply-windows-settings"></a>Proměnné pro použití nastavení systému Windows

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Rutiny pro použití nastavení systému Windows

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [New-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [Remove-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting)
- [Set-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting)

### <a name="properties-for-apply-windows-settings"></a>Vlastnosti pro použití nastavení systému Windows

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="user-name"></a>Uživatelské jméno

Zadejte registrované uživatelské jméno, které chcete přidružit k cílovému počítači. Hodnota, kterou zachytí krok pořadí úloh **zaznamenat nastavení systému Windows** , může tuto hodnotu přepsat.  

#### <a name="organization-name"></a>Název organizace

Zadejte název registrované organizace, který se má přidružit k cílovému počítači. Hodnota, kterou zachytí krok pořadí úloh **zaznamenat nastavení systému Windows** , může tuto hodnotu přepsat.  

#### <a name="product-key"></a>Kód Product Key  

Zadejte kód Product Key, který se má použít pro instalaci Windows na cílovém počítači.  

#### <a name="server-licensing"></a>Licence serveru

Zadejte režim licencování serveru.

- Jako režim licencování vyberte na **jeden server** nebo **na uživatele** .  
- Pokud vyberete možnost **podle serveru**, zadejte také maximální počet připojení povolených na základě vaší licenční smlouvy.  
- Pokud cílový počítač není server nebo pokud nechcete **zadat režim**licencování, vyberte nezadávat.  

#### <a name="maximum-connections"></a>Maximální počet připojení

> [!NOTE]
> Toto nastavení platí pouze pro starší verze systému Windows, které již nejsou podporovány.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Náhodně generovat heslo místního správce a vypnout účet na všech podporovaných platformách (doporučeno)  

Tuto možnost vyberte, pokud chcete nastavit heslo místního správce na náhodně vygenerovaný řetězec. Tato možnost také zakáže účet místního správce na platformách, které tuto funkci podporují.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Zapnout účet a zadat heslo místního správce  

Tuto možnost vyberte, pokud chcete povolit účet místního správce pomocí zadaného hesla. Zadejte heslo na řádku **Heslo** a potvrďte ho na řádku **Potvrdit heslo**.  

#### <a name="time-zone"></a>Časové pásmo

Určete časové pásmo, které chcete nakonfigurovat na cílovém počítači. Hodnota, kterou zachytí krok pořadí úloh **zaznamenat nastavení systému Windows** , může tuto hodnotu přepsat.  

#### <a name="language-settings"></a>Nastavení jazyka

<!--5411057, 5138936-->

Počínaje verzí 1910 řídí konfiguraci jazyka během nasazování operačního systému. Pokud už tato nastavení jazyka aplikujete, může vám tato změna zjednodušit pořadí úkolů nasazení operačního systému. Místo použití více kroků v jednotlivých jazycích nebo samostatných skriptech použijte pro daný jazyk jednu instanci v rámci tohoto kroku s podmínkou.

Nakonfigurujte tahle nastavení:

- Vstupní národní prostředí (výchozí rozložení klávesnice)
- Národní prostředí systému
- Jazyk uživatelského rozhraní
- Záložní jazyk uživatelského rozhraní
- Národní prostředí uživatele

Další informace o těchto hodnotách souboru odpovědí instalačního programu systému Windows najdete v tématu [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> Pokud vytvoříte vlastní soubor odpovědí instalačního programu systému Windows (unattend.xml), přepíše tento krok všechny existující hodnoty. K automatizaci dynamického procesu pro tato nastavení použijte související proměnné pořadí úkolů. Například [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Automaticky použít ovladače

Tento krok použijte, pokud chcete vyhledat a nainstalovat ovladače jako součást nasazení operačního systému.  

> [!IMPORTANT]  
> Samostatné médium nemůže použít krok **automaticky použít ovladače** . Pořadí úkolů nemá v tomto scénáři žádné připojení k Configuration Manager lokalitě.  

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **ovladače**a vyberte možnost **automaticky použít ovladače**.

> [!TIP]
> Přehled ovladačů v Configuration Manager najdete v tématu [instalace ovladačů pomocí pořadí úloh](../get-started/manage-drivers.md#BKMK_TSDrivers).

### <a name="behaviors-for-auto-apply-drivers"></a>Chování pro automatické použití ovladačů

Krok pořadí úkolů **Automaticky použít ovladače** provede následující akce:  

1. Naskenujte hardware a vyhledejte ID Plug-and-Play pro všechna zařízení v systému.  

2. Odešle seznam zařízení a jejich ID Plug-and-Play do bodu správy. Bod správy vrátí seznam kompatibilních ovladačů z katalogu ovladačů pro každé hardwarové zařízení. Seznam obsahuje všechny povolené ovladače bez ohledu na to, v jakém balíčku ovladačů se nacházejí, a ovladače označené určenou kategorií ovladačů.  

3. Pro každé hardwarové zařízení pořadí úkolů vybere nejlepší ovladač. Tento ovladač je vhodný pro nasazený operační systém a je na přístupném distribučním bodu.  

4. Pořadí úkolů stáhne vybrané ovladače z distribučního bodu a fáze ovladačů v cílovém operačním systému.  

    1. Při použití image operačního systému pořadí úkolů umístí ovladače do úložiště ovladačů operačního systému.  

    2. Při použití balíčku s upgradem operačního systému jako původního zdroje instalace nakonfiguruje sekvence úloh instalační program systému Windows s umístěním ovladače.  

5. Během kroku **nastavit systém Windows a nástroj ConfigMgr** v pořadí úloh instalační program systému Windows najde ovladače připravené tímto krokem.  

### <a name="variables-for-auto-apply-drivers"></a>Proměnné pro automatické použití ovladačů

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Rutiny pro automatické použití ovladačů

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver)
- [New-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver)
- [Remove-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver)
- [Set-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver)

### <a name="properties-for-auto-apply-drivers"></a>Vlastnosti pro automatické použití ovladačů

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Instalovat pouze nejvhodnější kompatibilní ovladače 

Určuje, že má krok pořadí úkolů pro každé zjištěné hardwarové zařízení nainstalovat jenom ten nejvhodnější ovladač.  

#### <a name="install-all-compatible-drivers"></a>Instalovat všechny kompatibilní ovladače

Pořadí úkolů nainstaluje všechny ovladače kompatibilní pro každé zjištěné hardwarové zařízení. Instalační program systému Windows pak zvolí nejlepší ovladač. Tato možnost využívá větší šířku pásma sítě a místo na disku. Pořadí úkolů stáhne další ovladače, ale systém Windows může vybrat lepší ovladač.  

#### <a name="consider-drivers-from-all-categories"></a>Nabídnout ovladače ze všech kategorií

Pořadí úkolů vyhledá příslušné ovladače zařízení ve všech dostupných kategoriích ovladačů.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Omezit zobrazené ovladače pouze na nabídnuté ovladače z vybraných kategorií

Pořadí úkolů vyhledá příslušné ovladače zařízení v zadaných kategoriích ovladačů.  

Pokud vyberete více kategorií, vrátí všechny odpovídající ovladače, které jsou k dispozici v některé z kategorií. Je ekvivalentní `OR` operaci.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Provést bezobslužnou instalaci nepodepsaných ovladačů ve verzích systému Windows, kde je to povoleno

Tato možnost umožňuje systému Windows instalovat ovladače bez digitálního podpisu.  

> [!IMPORTANT]  
> Tato možnost se nevztahuje na operační systémy, ve kterých nelze nakonfigurovat zásady podepisování ovladačů.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Zaznamenat nastavení sítě

Tento krok použijte k zaznamenání nastavení sítě Microsoft z počítače, na kterém pořadí úkolů běží. Pořadí úkolů uloží tato nastavení do proměnných pořadí úkolů. Tato nastavení přepíší výchozí nastavení, které nakonfigurujete v kroku **použít nastavení sítě** .  

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.  

Pokud chcete přidat tento krok v editoru pořadí úloh, vyberte **Přidat**, vyberte **Nastavení**a vyberte **zaznamenat nastavení sítě**.

### <a name="variables-for-capture-network-settings"></a>Proměnné pro záznam nastavení sítě

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Rutiny pro zachycení nastavení sítě

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings)
- [New-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings)
- [Remove-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings)
- [Set-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings)

### <a name="properties-for-capture-network-settings"></a>Vlastnosti pro zaznamenání nastavení sítě

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrovat členství v doménách a pracovních skupinách

Zaznamená informace o členství v doméně a pracovní skupině cílového počítače.  

#### <a name="migrate-network-adapter-configuration"></a>Migrovat konfiguraci síťového adaptéru

Zaznamená konfiguraci síťového adaptéru cílového počítače. Zachycuje následující informace:

- Globální nastavení sítě  
- Počet adaptérů  
- Následující nastavení sítě přidružené ke každému adaptéru: DNS, WINS, IP a filtry portů



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Zachytit bitovou kopii operačního systému

Tento krok zachycuje jednu nebo více imagí z referenčního počítače. Pořadí úkolů vytvoří soubor bitové kopie systému Windows (. wim) v zadané síťové sdílené složce. Pak pomocí průvodce **přidáním balíčku bitových kopií operačního systému** naimportujte tento obrázek do Configuration Manager pro nasazení operačního systému na základě bitové kopie.  

Configuration Manager zachycuje jednotlivé svazky (jednotky) z referenčního počítače na samostatnou bitovou kopii v souboru. wim. Pokud má odkazovaný počítač více svazků, bude výsledný soubor. wim obsahovat samostatnou bitovou kopii pro každý svazek. V tomto kroku se zachytí jenom svazky, které jsou naformátované jako NTFS nebo FAT32. Přeskočí svazky s jinými formáty a svazky USB.  

Instalovaný operační systém v referenčním počítači musí být verze Windows, která Configuration Manager podporuje. Použijte nástroj SysPrep k přípravě operačního systému v referenčním počítači. Instalovaný svazek operačního systému a spouštěcí svazek musí být stejný svazek.  

Zadejte účet s oprávněním k zápisu do vybrané sdílené síťové složky. Další informace o účtu image operačního systému Capture najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové**kopie a vyberte možnost **zachytit bitovou kopii operačního systému**.

### <a name="variables-for-capture-os-image"></a>Proměnné pro image operačního systému pro zachycení

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>Rutiny pro zachycení image operačního systému

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage)
- [New-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage)
- [Remove-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage)
- [Set-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage)

### <a name="properties-for-capture-os-image"></a>Vlastnosti pro image operačního systému pro zachycení

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="target"></a>Cíl  

Cesta systému souborů k umístění, které Configuration Manager používá při ukládání zachycené image operačního systému.  

#### <a name="description"></a>Description  

Volitelný uživatelsky definovaný popis zachycené image operačního systému uložený v souboru bitové kopie.  

#### <a name="version"></a>Verze  

Volitelné uživatelsky definované číslo verze, které se má přiřadit k zaznamenané bitové kopii operačního systému. Tato hodnota může být libovolná kombinace písmen a číslic. Je uložen v souboru obrázku.  

#### <a name="created-by"></a>Vytvořil(a)  

Volitelné jméno uživatele, který vytvořil bitovou kopii operačního systému. Je uložen v souboru obrázku.  

#### <a name="capture-operating-system-image-account"></a>Zaznamenat účet bitové kopie operačního systému  

Zadejte účet systému Windows, který má oprávnění k zadané sdílené síťové složce. Vyberte **nastavit** a zadejte název účtu systému Windows.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Zaznamenat stav uživatele

Tento krok používá Nástroj pro migraci uživatelských souborů a nastavení (USMT) k zaznamenání stavu uživatele a nastavení z počítače, na kterém pořadí úkolů běží. Tento krok pořadí úkolů se používá ve spojení s krokem pořadí úkolů **Obnovit stav uživatele**. Tento krok vždycky zašifruje úložiště stavů USMT pomocí šifrovacího klíče, který Configuration Manager generuje a spravuje.  

Další informace o správě stavu uživatele při nasazování operačních systémů najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  

Pokud chcete nastavení stavu uživatele uložit a obnovit z bodu migrace stavu, použijte tento krok s kroky úložiště **stavu požadavku** a **úložiště stavu uvolnění** .  

Tento krok zajišťuje kontrolu nad určitou podmnožinou nejčastěji používaných možností nástroje USMT. Zadejte další možnosti příkazového řádku pomocí proměnné pořadí úkolů **proměnné OSDMigrateAdditionalCaptureOptions** .  

Tento krok pořadí úkolů běží jenom v prostředí Windows PE. Neběží v plném operačním systému.  

Pokud chcete přidat tento krok v editoru pořadí úloh, vyberte **Přidat**, vyberte **stav uživatele**a vyberte **zaznamenat stav uživatele**.

### <a name="variables-for-capture-user-state"></a>Proměnné pro záznam stavu uživatele

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Rutiny pro zachycení stavu uživatele

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState)
- [New-CMTSStepCaptureUserState](/powershell/module/configurationmanager/New-CMTSStepCaptureUserState)
- [Remove-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState)
- [Set-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState)

### <a name="properties-for-capture-user-state"></a>Vlastnosti pro zaznamenání stavu uživatele

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="user-state-migration-tool-package"></a>Balíček nástroje pro migraci stavu uživatele

Zadejte balíček, který obsahuje Nástroj pro migraci uživatelských souborů a nastavení (USMT). Pořadí úkolů používá tuto verzi nástroje USMT k zachycení stavu a nastavení uživatele. Tento balíček nevyžaduje program. Zadejte balíček obsahující 32 nebo 64 verzi nástroje USMT pro bitovou kopii. Architektura nástroje USMT závisí na architektuře operačního systému, ze které pořadí úkolů zachytí stav.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Zaznamenat všechny profily uživatelů pomocí standardních možností

Migrujte všechny informace o profilu uživatele. Tato možnost je výchozí.  

Pokud vyberete tuto možnost, ale nezaškrtnete políčko **Obnovit profily uživatelů místního počítače** v kroku **Obnovit stav uživatele** , pořadí úkolů se nezdařilo. Configuration Manager nemůže migrovat nové účty, aniž by jim přiřadil hesla.

Když použijete možnost **instalovat existující balíček bitových kopií** v průvodci **vytvořením nového pořadí úkolů** , ve výsledném pořadí úkolů se ve výchozím nastavení **zachytí všechny profily uživatelů se standardními možnostmi**. Toto výchozí pořadí úkolů neumožňuje vybrat možnost **obnovení profilů uživatelů místního počítače**ani uživatelských účtů, které nejsou v doméně.  

Vyberte **Obnovit profily uživatelů místního počítače** a zadejte heslo pro účet, který chcete migrovat. V ručně vytvořeném pořadí úkolů se toto nastavení nachází v kroku **Obnovit stav uživatele** . V pořadí úkolů, které vytvořil průvodce vytvořením **nového pořadí úkolů**, je toto nastavení v kroku na stránku průvodce **Obnovení uživatelských souborů a nastavení**.  

Pokud nemáte žádné místní uživatelské účty, toto nastavení se nepoužije.  

#### <a name="customize-how-user-profiles-are-captured"></a>Přizpůsobit způsob zaznamenání profilů

Tuto možnost vyberte, pokud chcete zadat soubor vlastního profilu pro migraci. Vyberte **soubory** a vyberte konfigurační soubory, které má nástroj USMT použít pro tento krok. Zadejte vlastní soubor. XML, který obsahuje pravidla definující soubory stavu uživatele k migraci.  

#### <a name="click-here-to-select-configuration-files"></a>Kliknutím sem vyberte konfigurační soubory.

Tuto možnost vyberte, abyste mohli vybrat konfigurační soubory v balíčku USMT, které chcete použít pro zaznamenání profilů uživatelů. Kliknutím na tlačítko **soubory** otevřete dialogové okno **konfigurační soubory** . Pokud chcete zadat konfigurační soubor, zadejte název souboru do řádku **filename** a vyberte tlačítko **Přidat** .  

#### <a name="enable-verbose-logging"></a>Zapnout podrobné protokolování

Tuto možnost povolte, pokud chcete v souboru protokolu vygenerovat podrobnější informace. Při zaznamenávání stavu se ve výchozím nastavení pořadí úkolů ve složce protokolu pořadí úkolů generuje příkaz **Scanstate. log** `%WinDir%\ccm\logs` .  

#### <a name="skip-files-using-encrypted-file-system"></a>Přeskočit soubory používající systém souborů EFS 

Tuto možnost povolte, pokud chcete přeskočit zachytávání souborů šifrovaných pomocí systému souborů EFS (Encrypted File System). Tyto soubory obsahují soubory profilu uživatele. V závislosti na verzi operačního systému a nástroje USMT nemusí být šifrované soubory po obnovení čitelné. Další informace najdete v dokumentaci k nástroji USMT.  

#### <a name="copy-by-using-file-system-access"></a>Kopírovat pomocí přístupu k systému souborů

Tuto možnost povolte, pokud chcete zadat některé z následujících nastavení:  

- **Pokračovat, i když některé soubory nelze zaznamenat**: Pokud povolíte toto nastavení, bude proces migrace pokračovat i v případě, že nemůže zachytit některé soubory. Pokud tuto možnost zakážete a nebudete moct zachytit soubor, tento krok se nezdařil. Tato možnost je ve výchozím nastavení povolená.  

- **Zaznamenat lokálně pomocí odkazů místo pomocí kopírování souborů**: Pokud povolíte toto nastavení, můžete k zaznamenávání souborů používat pevné odkazy systému souborů NTFS.  

    Další informace o migraci dat pomocí pevných odkazů najdete v tématu [úložiště migrace s pevným odkazem](/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Zaznamenat v režimu offline (pouze systém Windows PE)**: Toto nastavení povolte, pokud chcete zachytit stav uživatele v prostředí Windows PE, nikoli v plném operačním systému.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Zaznamenání pomocí služby Stínová kopie svazku (VSS)

Tato možnost umožňuje zachytávání souborů i v případě, že jsou zamčené pro úpravy jinou aplikací.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Zaznamenat nastavení systému Windows

Tento krok použijte k zaznamenání nastavení Windows z počítače, na kterém pořadí úkolů běží. Pořadí úkolů uloží tato nastavení do proměnných pořadí úkolů. Tato zachycená nastavení přepíší výchozí nastavení, které nakonfigurujete v kroku **použít nastavení systému Windows** .  

Tento krok pořadí úkolů běží buď v prostředí Windows PE, nebo v úplném operačním systému.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte **Nastavení**a vyberte možnost **zaznamenat nastavení systému Windows**.

### <a name="variables-for-capture-windows-settings"></a>Proměnné pro nastavení systému Windows pro zachycení

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Rutiny pro zachycení nastavení systému Windows

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings)
- [New-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings)
- [Remove-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings)
- [Set-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings)

### <a name="properties-for-capture-windows-settings"></a>Vlastnosti pro zachycení nastavení systému Windows

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="migrate-computer-name"></a>Migrovat název počítače

Zaznamenejte si název počítače pro rozhraní NetBIOS.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrovat názvy registrovaných uživatelů a organizací

Zachyťte názvy registrovaných uživatelů a organizací z počítače.  

#### <a name="migrate-time-zone"></a>Migrovat časová pásma

Zachyťte nastavení časového pásma v počítači.  


## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> Kontrolovat připravenost

Pomocí tohoto kroku ověříte, že cílový počítač splňuje zadané předpoklady pro nasazení.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **kontrolovat připravenost**.

Počínaje verzí 2002 tento krok zahrnuje osm nových kontrol. Žádná z těchto nových kontrol není ve výchozím nastavení v nových nebo existujících instancích tohoto kroku vybraná.<!--6005561--> Další informace o každé kontrole najdete v níže uvedených částech.

- **Architektura aktuálního operačního systému**
- **Minimální verze operačního systému**
- **Maximální verze operačního systému**
- **Minimální verze klienta**
- **Jazyk aktuálního operačního systému**
- **Napájení ze sítě AC**
- **Síťový adaptér připojen**
  - **Síťový adaptér není bezdrátový.**

Počínaje verzí 2006 tento krok zahrnuje kontrolu a určení, jestli zařízení používá rozhraní UEFI, **je počítač v režimu UEFI**.<!--6452769-->

> [!IMPORTANT]
> Pokud chcete tuto novou funkci Configuration Manager využít, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

**Souboru Smsts. log** zahrnuje výsledek všech kontrol. Pokud se jedna kontrola nezdařila, modul sekvence úloh bude nadále vyhodnocovat další kontroly. Krok se nezdařil, dokud nebudou dokončeny všechny kontroly. Pokud nejméně jedna kontrolní chyba není úspěšná, krok se nepovede a vrátí kód chyby **4316**. Tento kód chyby se překládá na prostředek vyžadovaný pro tuto operaci neexistuje.

### <a name="variables-for-check-readiness"></a>Proměnné pro kontrolu připravenosti

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH) (počínaje verzí 2002)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER) (počínaje verzí 2002)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER) (počínaje verzí 2002)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER) (počínaje verzí 2002)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE) (počínaje verzí 2002)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER) (počínaje verzí 2002)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK) (počínaje verzí 2002)
- [_TS_CRUEFI](task-sequence-variables.md#TSCRUEFI) (počínaje verzí 2006)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED) (počínaje verzí 2002)

### <a name="cmdlets-for-check-readiness"></a>Rutiny pro kontrolu připravenosti

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck)
- [New-CMTSStepPrestartCheck](/powershell/module/configurationmanager/New-CMTSStepPrestartCheck)
- [Remove-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck)
- [Set-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck)

### <a name="properties-for-check-readiness"></a>Vlastnosti pro kontrolu připravenosti

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="minimum-memory-mb"></a>Minimální paměť (MB)

Ověřte, zda velikost paměti v megabajtech (MB) splňuje nebo překračuje zadanou velikost. Krok toto nastavení povolí ve výchozím nastavení.  

#### <a name="minimum-processor-speed-mhz"></a>Minimální rychlost procesoru (MHz)  

Ověřte, že rychlost procesoru (v MHz) splňuje nebo překračuje zadanou velikost. Krok toto nastavení povolí ve výchozím nastavení.  

#### <a name="minimum-free-disk-space-mb"></a>Minimální volné místo na disku (MB)

Ověřte, zda velikost volného místa na disku v megabajtech (MB) splňuje nebo překračuje zadanou velikost.  

#### <a name="current-os-to-be-refreshed-is"></a>Aktuální operační systém, který se má aktualizovat, je

Ověřte, že operační systém nainstalovaný na cílovém počítači splňuje zadaný požadavek. Krok nastaví toto nastavení na **klient** ve výchozím nastavení.  

#### <a name="architecture-of-current-os"></a>Architektura aktuálního operačního systému

Počínaje verzí 2002 ověřte, zda je aktuální operační systém **32-** bit nebo **64-bit**.

#### <a name="minimum-os-version"></a>Minimální verze operačního systému

Od verze 2002 ověřte, zda aktuální operační systém používá verzi, která je novější než zadaná. Zadejte verzi s hlavní verzí, vedlejší verzí a číslem sestavení. Například, `10.0.16299`.

#### <a name="maximum-os-version"></a>Maximální verze operačního systému

Počínaje verzí 2002 ověřte, zda aktuální operační systém používá verzi starší než určenou. Zadejte verzi s hlavní verzí, vedlejší verzí a číslem sestavení. Například, `10.0.18356`.

#### <a name="minimum-client-version"></a>Minimální verze klienta

Od verze 2002 ověřte, zda je verze Configuration Manager klienta alespoň zadané verze. Zadejte verzi klienta v následujícím formátu: `5.00.8913.1005` .

#### <a name="language-of-current-os"></a>Jazyk aktuálního operačního systému

Počínaje verzí 2002 ověřte, zda aktuální jazyk operačního systému odpovídá zadaným hodnotám. Vyberte název jazyka a krok porovná kód přidruženého jazyka. Tato možnost porovná vybraný jazyk s vlastností **OSLanguage** třídy WMI **Win32_OperatingSystem** na klientovi.

#### <a name="ac-power-plugged-in"></a>Napájení ze sítě AC

Od verze 2002 ověřte, že je zařízení napájené ze sítě, a ne na baterii.

#### <a name="network-adapter-connected"></a>Síťový adaptér připojen

Od verze 2002 ověřte, že zařízení má síťový adaptér, který je připojený k síti. Můžete také vybrat závislou kontrolu a ověřit, že **síťový adaptér není bezdrátový**.

#### <a name="computer-is-in-uefi-mode"></a>Počítač je v režimu UEFI.

Od verze 2006 Zjistěte, jestli je zařízení nakonfigurované pro rozhraní UEFI nebo BIOS.

### <a name="options-for-check-readiness"></a>Možnosti kontroly připravenosti

> [!NOTE]  
> Pokud povolíte nastavení **pokračovat při chybě** na kartě **Možnosti** tohoto kroku, zapíše se pouze výsledky kontroly připravenosti. Pokud se ověření nepodaří, pořadí úkolů se nezastaví.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Připojit k síťové složce

Pomocí tohoto kroku můžete vytvořit připojení ke sdílené síťové složce.  

Tento krok pořadí úkolů běží v plném operačním systému nebo v prostředí Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **připojit k síťové složce**.

### <a name="variables-for-connect-to-network-folder"></a>Proměnné pro připojení k síťové složce

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Rutiny pro připojení k síťové složce

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder)
- [New-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder)
- [Remove-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder)
- [Set-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder)

### <a name="properties-for-connect-to-network-folder"></a>Vlastnosti pro připojení k síťové složce

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="path"></a>Cesta  

Vyberte **Procházet** a zadejte cestu ke složce v síti. Použijte formát `\\server\share`.

#### <a name="drive"></a>Disky  

Vyberte písmeno místní jednotky, které chcete přiřadit k tomuto připojení.

#### <a name="account"></a>Účet

Pokud chcete zadat uživatelský účet s oprávněními pro připojení k této síťové složce, vyberte **nastavit** . Další informace o účtu připojení síťové složky pořadí úkolů najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> Zakázat nástroj BitLocker

Pomocí tohoto kroku zakážete šifrování nástrojem BitLocker na aktuální jednotce operačního systému nebo na konkrétní jednotce. Tato akce ponechá ochraně klíčů v nešifrovaných textech na pevném disku. Nešifruje obsah jednotky. Tato akce se dokončí téměř okamžitě.  

> [!NOTE]  
> Nástroj BitLocker Drive Encryption poskytuje nižší úroveň šifrování obsahu svazku disku.  

Máte-li několik šifrovaných jednotek, zakažte nástroj BitLocker na všech datových jednotkách před zakázáním nástroje BitLocker na jednotce operačního systému.  

Tento krok se spouští jenom v plném operačním systému. Neběží v systému Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **disky**a vyberte možnost **Zakázat nástroj BitLocker**.

### <a name="variables-for-disable-bitlocker"></a>Proměnné pro zakázání nástroje BitLocker

Počínaje verzí 1906 použijte následující proměnné pořadí úkolů s tímto krokem:  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>Rutiny pro zakázání nástroje BitLocker

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker)
- [New-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker)
- [Remove-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker)
- [Set-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker)

### <a name="properties-for-disable-bitlocker"></a>Vlastnosti pro zakázání nástroje BitLocker

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="current-operating-system-drive"></a>Aktuální jednotka operačního systému

Zakáže nástroj BitLocker na aktuální jednotce operačního systému.  

#### <a name="specific-drive"></a>Konkrétní jednotka  

Zakáže nástroj BitLocker na konkrétní jednotce. Z rozevíracího seznamu vyberte jednotku, kde je nástroj BitLocker zakázaný.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Obnovit ochranu po restartování Windows zadaného počtu opakování

<!-- 4512937 -->
Počínaje verzí 1906 použijte tuto možnost k určení počtu restartování, která mají být zakázána nástrojem BitLocker. Místo přidání více instancí tohoto kroku nastavte hodnotu mezi 1 (výchozí) a 15.

Toto chování můžete nastavit a změnit pomocí proměnných pořadí úkolů [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) a [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride).


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Stáhnout obsah balíčku

Pomocí tohoto kroku si stáhněte kterýkoli z následujících typů balíčků:  

- Image operačního systému  
- Balíčky s upgradem operačního systému  
- Balíčky ovladačů  
- Balíčky  
- Spouštěcí image – <sup> [Poznámka 1](#bkmk_note1)</sup>  

Tento krok dobře funguje v pořadí úkolů pro upgrade operačního systému v následujících scénářích:  

- Používáte jedno pořadí úkolů upgradu, které může fungovat pro platformu x86 i x64. Do skupiny **Příprava pro upgrade** přidejte dva kroky **Stáhnout obsah balíčku** . Zadejte podmínky na kartě **Možnosti** pro detekci architektury klienta a stáhněte pouze příslušný balíček upgradu operačního systému. Nakonfigurujte všechny kroky **Stáhnout obsah balíčku** tak, aby používaly stejnou proměnnou. Proměnnou pro cestu k médiu použijte v kroku **upgrade operačního systému** .  

- Pokud chcete dynamicky stáhnout příslušný balíček ovladačů, použijte dva kroky **Stáhnout obsah balíčku** s podmínkami, které zjišťují odpovídající typ hardwaru pro každý balíček ovladače. Nakonfigurujte všechny kroky **Stáhnout obsah balíčku** tak, aby používaly stejnou proměnnou. Použijte proměnnou pro hodnotu **připraveného obsahu** v části ovladače v kroku **upgrade operačního systému** .  

> [!NOTE]  
> Když nasadíte pořadí úloh, které obsahuje tento krok, nevybírejte možnost **stáhnout veškerý obsah místně před spuštěním pořadí úloh** nebo **přístup k obsahu přímo z distribučního bodu** pro **Možnosti nasazení** na stránce **distribuční body** v Průvodci nasazením softwaru.  

Tento krok běží buď v úplném operačním systému, nebo v prostředí Windows PE. Možnost Uložit balíček v mezipaměti klienta Configuration Manager není podporována v systému Windows PE.

> [!NOTE]  
> Úloha **Stažení obsahu balíčku** se nepodporuje pro použití se samostatným médiem. Další informace najdete v tématu [nepodporované akce pro samostatné médium](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media).  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **software**a vyberte možnost **Stáhnout obsah balíčku**.

### <a name="cmdlets-for-download-package-content"></a>Rutiny pro stažení obsahu balíčku

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent)
- [New-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent)
- [Remove-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent)
- [Set-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent)

### <a name="properties-for-download-package-content"></a>Vlastnosti pro stažení obsahu balíčku

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="select-package"></a>Výběr balíčku  

Vyberte ikonu pro výběr balíčku, který chcete stáhnout. Po výběru jednoho balíčku vyberte ikonu znovu a zvolte jiný balíček.  

#### <a name="place-into-the-following-location"></a>Umístit na následující místo

Vyberte možnost Uložit balíček v jednom z následujících umístění:  

- **Pracovní adresář pořadí úkolů**: Toto umístění je také označováno jako mezipaměť pořadí úloh.  

- **Mezipaměť klienta Configuration Manager**: tuto možnost použijte, pokud chcete uložit obsah do mezipaměti klienta. Ve výchozím nastavení je tato cesta `%WinDir%\ccmcache` .  

- **Vlastní cesta**: modul pořadí úkolů nejprve stáhne balíček do pracovního adresáře pořadí úkolů. Pak přesune obsah do této cesty, kterou zadáte. Modul pořadí úloh připojuje cestu k ID balíčku.  

#### <a name="save-path-as-a-variable"></a>Uložit cestu jako proměnnou

Uložte cestu balíčku do vlastní proměnné pořadí úkolů. Pak tuto proměnnou použijte v jiném kroku pořadí úkolů.

Configuration Manager přidá k názvu proměnné číselnou příponu. Například zadáte proměnnou `%MyContent%` jako vlastní proměnná. Je to kořenový adresář, kde pořadí úkolů ukládá veškerý odkazovaný obsah pro tento krok. Tento obsah může obsahovat více balíčků. Když odkazujete na proměnnou, přidejte číselnou příponu. První balíček najdete v tématu `%MyContent01%` . Když v následujících krocích, jako je například **upgrade operačního systému**, provedete ukazatel na proměnnou, použijte `%MyContent02%` nebo `%MyContent03%` , kde číslo odpovídá pořadí, v jakém krok **Stáhnout obsah balíčku** vypíše balíčky.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Když stahování balíčku selže, pokračovat ve stahování dalších balíčků v seznamu

Pokud pořadí úloh nedokáže Stáhnout balíček, začne stahovat další balíček v seznamu.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> Poznámka 1: použití spouštěcích imagí v kroku stáhnout obsah balíčku

*Platí pro verzi 1910 a novější.*<!-- SCCMDocs-pr #4202 -->

Pokud nakonfigurujete [vlastnosti pořadí úkolů](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) , aby **používaly spouštěcí bitovou kopii**, pak je do tohoto kroku Přidání spouštěcí bitové kopie redundantní. Do tohoto kroku přidejte pouze spouštěcí bitovou kopii, pokud není zadána ve vlastnostech pořadí úkolů.

#### <a name="example-use-case"></a>Příklad případu použití

- Jedno pořadí úkolů pro předběžné stažení obsahu:
  - Žádná přidružená spouštěcí image
  - Spouští se jenom v plném operačním systému, který je nejspíš bez zásahu uživatele.
  - Používá více kroků **Stáhnout obsah balíčku** s podmínkami. V závislosti na konkrétním jazyku a architektuře stahuje obsah do mezipaměti klienta nástroje pro přípravu pro pořadí úkolů nasazení operačního systému.
  - K dispozici je pouze jedna instance tohoto pořadí úkolů se všemi možnými možnostmi obsahu.

- Pořadí úloh nasazení s více operačními systémy:
  - Normální pořadí úkolů nasazení operačního systému.
  - Obsahuje spouštěcí bitovou kopii, na kterou se odkazuje ve vlastnostech.
  - Existuje několik instancí tohoto pořadí úloh s různými spouštěcími bitovými kopiemi podle potřeby architektury a jazyka.

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> Zapnout nástroj BitLocker

Nástroj BitLocker Drive Encryption poskytuje nižší úroveň šifrování obsahu svazku disku. Tento krok použijte, pokud chcete povolit šifrování BitLockeru aspoň na dvou oddílech na pevném disku. První aktivní oddíl obsahuje kód pro spuštění systému Windows. Jiný oddíl obsahuje operační systém. Spouštěcí oddíl musí zůstat nezašifrovaný.  

Chcete-li povolit nástroj BitLocker na jednotce v prostředí Windows PE, použijte krok [před poskytnutím nástroje BitLocker](#BKMK_PreProvisionBitLocker) .

Tento krok se spouští jenom v plném operačním systému. Neběží v systému Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **disky**a vyberte možnost **Povolit nástroj BitLocker**.

Když zadáte **pouze TPM**, **TPM a spouštěcí klíč na sběrnici USB**nebo **TPM a PIN**, musí být čip TPM (Trusted Platform Module) v následujícím stavu, než bude možné spustit krok **zapnout nástroj BitLocker** :  

- Povoleno  
- Aktivováno  
- Vlastnictví povoleno  

Počínaje verzí 2006 můžete tento krok přeskočit pro počítače, které nemají TPM, nebo když není čip TPM povolený. Nové nastavení usnadňuje správu chování pořadí úkolů na zařízeních, která nemůžou plně podporovat nástroj BitLocker.<!--6995601-->

Tento krok dokončí veškerou zbývající inicializaci čipu TPM. Zbývající akce nevyžadují fyzickou přítomnost ani restartování. Krok **zapnout nástroj BitLocker** transparentně provede následující zbývající akce inicializace čipu TPM v případě potřeby:

- Vytvoření dvojice ověřovacích klíčů  
- Vytvoření hodnoty autorizace vlastníka a úschovy v adresáři služby Active Directory, která se musí rozšířit pro zajištění podpory této hodnoty  
- Přebírat vlastnictví  
- Vytvoření klíče SRK (Storage Root Key) nebo jeho resetování (pokud už existuje, ale není kompatibilní)  

Pokud chcete, aby pořadí úkolů čekalo na dokončení procesu šifrování jednotky **nástrojem BitLocker** , vyberte možnost **čekání** . Pokud nevyberete možnost **čekání** , dojde k procesu šifrování jednotky na pozadí. Pořadí úkolů okamžitě pokračuje k dalšímu kroku.  

BitLocker se dá použít k šifrování několika jednotek v systémovém systému, a to i v operačních systémech a datových jednotkách. Pokud chcete zašifrovat datovou jednotku, nejdřív Zašifrujte jednotku operačního systému a dokončete proces šifrování. Důvodem je, že jednotka operačního systému ukládá ochrany klíčů pro datové jednotky. Pokud zašifrujete operační systém a datové jednotky ve stejném pořadí úkolů, vyberte možnost **čekání** v kroku **zapnout nástroj BitLocker** pro jednotku operačního systému.  

Pokud je pevný disk už zašifrovaný, ale BitLocker je zakázaný, pak krok **zapnout nástroj BitLocker** znovu povolí ochranu pomocí klíče a rychle dokončí činnost. V tomto případě není nutné znovu šifrovat pevný disk.  

### <a name="variables-for-enable-bitlocker"></a>Proměnné pro zapnutí nástroje BitLocker

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDBitLockerPIN](task-sequence-variables.md#OSDBitLockerPIN)
- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)

### <a name="cmdlets-for-enable-bitlocker"></a>Rutiny pro zapnutí nástroje BitLocker

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker)
- [New-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker)
- [Remove-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker)
- [Set-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker)

### <a name="properties-for-enable-bitlocker"></a>Vlastnosti pro zapnutí nástroje BitLocker

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="choose-the-drive-to-encrypt"></a>Vybrat jednotku pro zašifrování

Určuje jednotku, která se má šifrovat. Pokud chcete zašifrovat aktuální jednotku operačního systému, vyberte **aktuální jednotka operačního systému**. Pak nakonfigurujte jednu z následujících možností pro správu klíčů:  

- **Pouze TPM**: Tuto možnost vyberte, pokud se má používat jenom čip TPM (Trusted Platform Module).  

- **Spouštěcí klíč pouze na sběrnici USB**: Tuto možnost vyberte, pokud chcete použít spouštěcí klíč uložený na USB flash disku. Když vyberete tuto možnost, BitLocker zamkne normální proces spouštění, dokud nebude k počítači připojené USB zařízení se spouštěcím klíčem nástroje BitLocker.  

- **TPM a spouštěcí klíč na sběrnici USB**: Tuto možnost vyberte, pokud chcete použít čip TPM a spouštěcí klíč uložený na USB flash disku. Když vyberete tuto možnost, BitLocker zamkne normální proces spouštění, dokud nebude k počítači připojené USB zařízení se spouštěcím klíčem nástroje BitLocker.  

- **TPM a PIN**: tuto možnost vyberte, pokud chcete použít čip TPM a osobní identifikační číslo (PIN). Když vyberete tuto možnost, BitLocker zamkne normální proces spouštění, dokud uživatel nezadá PIN kód.  

Pokud chcete zašifrovat určitou datovou jednotku bez operačního systému, vyberte **konkrétní jednotka**. Pak vyberte jednotku ze seznamu.  

#### <a name="disk-encryption-mode"></a>Režim šifrování disku

<!--6995601-->
Počínaje verzí 2006 vyberte jeden z následujících šifrovacích algoritmů:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Ve výchozím nastavení nebo pokud není zadaný, bude tento krok dál používat výchozí metodu šifrování pro verzi operačního systému. Pokud tento krok běží na verzi Windows, která nepodporuje zadaný algoritmus, vrátí se k výchozímu operačnímu systému. V této situaci modul pořadí úkolů odešle stavovou zprávu 11911.

#### <a name="use-full-disk-encryption"></a>Použít úplné šifrování disku

<!--SCCMDocs-pr issue 2671-->
Ve výchozím nastavení tento krok zašifruje jenom využité místo na jednotce. Toto výchozí chování se doporučuje, protože je rychlejší a efektivnější. Pokud vaše organizace vyžaduje šifrování celé jednotky během instalace, pak tuto možnost povolte. Instalační program systému Windows čeká na zašifrování celé jednotky, což trvá dlouhou dobu, zejména u velkých jednotek.

> [!TIP]
> Počínaje verzí 1910 můžete vytvářet a nasazovat zásady správy BitLockeru, které používají *Úplné šifrování disku* . Pokud chcete spravovat BitLocker na zařízeních poté, co pořadí úkolů nasadí operační systém, povolte tuto možnost. Další informace najdete v tématu [Plánování správy BitLockeru](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Zvolit místo pro vytvoření obnovovacího klíče

Pokud chcete určit, aby nástroj BitLocker vytvořil heslo pro obnovení a v úschově ho ve službě Active Directory, vyberte **ve službě Active Directory**. Tato možnost vyžaduje, abyste rozšířili službu Active Directory pro nástroj BitLocker Key v úschově. BitLocker pak může uložit přidružené informace pro obnovení ve službě Active Directory. Pokud nechcete vytvořit heslo, vyberte **Nevytvářet obnovovací klíč** . Doporučenou možností je vytvořit heslo.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Počkat, až nástroj BitLocker dokončí proces šifrování jednotky na všech jednotkách; poté bude nástroj Configuration Manager pokračovat v provádění pořadí úloh

Tuto možnost vyberte, pokud chcete, aby nástroj BitLocker Drive Encryption byl dokončen před spuštěním dalšího kroku v pořadí úkolů. Vyberete-li tuto možnost, nástroj BitLocker zašifruje celý svazek disku před tím, než se uživatel bude moci přihlásit k počítači.  

Proces šifrování může trvat hodiny na dokončení při šifrování velkého pevného disku. Pokud tuto možnost nevyberete, můžete pořadí úkolů okamžitě pokračovat.  

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Přeskočit tento krok pro počítače, které nemají TPM, nebo když není TPM povoleno

<!--6995601-->
Počínaje verzí 2006 vyberte tuto možnost, pokud chcete přeskočit šifrování jednotky v počítači, který neobsahuje podporovaný nebo povolený čip TPM. Tuto možnost můžete například použít při nasazování operačního systému do virtuálního počítače. Ve výchozím nastavení je toto nastavení zakázáno pro krok **zapnout nástroj BitLocker** . Pokud toto nastavení povolíte a zařízení nemá funkční čip TPM, modul pořadí úkolů zaznamená chybu do protokolu souboru Smsts. log a odešle stavovou zprávu 11912. Pořadí úkolů pokračuje v předchozím kroku.


## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Formátovat a rozdělit disk na oddíly

Pomocí tohoto kroku můžete naformátovat a rozdělit na oddíly zadaný disk v cílovém počítači.  

> [!IMPORTANT]  
> Každé nastavení, které pro tento krok zadáte, se vztahuje na jeden zadaný disk. Pokud chcete naformátovat a rozdělit na oddíly jiný disk v cílovém počítači, přidejte do pořadí úkolů další krok **Formátovat a rozdělit disk na oddíly** .  

Tento krok běží jenom v prostředí Windows PE. Neběží v plném operačním systému.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **disky**a možnost **Formátovat a rozdělit disk na oddíly**.

### <a name="variables-for-format-and-partition-disk"></a>Proměnné pro formát a diskový disk

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>Rutiny pro Format a partition disk

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](/powershell/module/configurationmanager/get-cmtssteppartitiondisk)
- [New-CMTSStepPartitionDisk](/powershell/module/configurationmanager/new-cmtssteppartitiondisk)
- [Remove-CMTSStepPartitionDisk](/powershell/module/configurationmanager/remove-cmtssteppartitiondisk)
- [Set-CMTSStepPartitionDisk](/powershell/module/configurationmanager/set-cmtssteppartitiondisk)

### <a name="properties-for-format-and-partition-disk"></a>Vlastnosti pro formátování a rozdělení disku na oddíly

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="disk-number"></a>Číslo disku

Číslo fyzického disku, který se má formátovat Počet je založený na řazení výčtu disků v systému Windows.  

#### <a name="variable-name-to-store-disk-number"></a>Název proměnné pro uložení čísla disku

<!--6610288-->

Počínaje verzí 2006 použijte proměnnou pořadí úkolů k určení cílového disku, který chcete formátovat. Možnost této proměnné podporuje složitější pořadí úkolů s dynamickým chováním. Vlastní skript například může disk rozpoznat a nastavit proměnnou na základě typu hardwaru. Pak můžete použít více instancí tohoto kroku ke konfiguraci různých typů hardwaru a oddílů.

Pokud vyberete tuto vlastnost, zadejte název vlastní proměnné. Přidejte v pořadí úkolů předchozí krok pro nastavení hodnoty této vlastní proměnné na celočíselnou hodnotu pro fyzický disk.

Následující vzorové kroky ukazují jeden příklad:

- **Spustit skript prostředí PowerShell**: vlastní skript pro shromažďování cílových disků
  - Nastaví `myOSDisk` na `1`
  - Nastaví `myDataDisk` na `2`

- **Formátovat a rozdělit disk na oddíly** pro disk s operačním systémem: Určuje `myOSDisk` proměnnou.
  - Nakonfiguruje disk 1 jako systémový disk.

- **Formátovat a rozdělit disk na oddíly** pro datový disk: Určuje `myDataDisk` proměnnou.
  - Nakonfiguruje disk 2 pro nezpracované úložiště.

Variace tohoto příkladu používá pro různé typy hardwaru čísla disků a plány dělení na oddíly.

> [!NOTE]
> Stávající proměnnou pořadí úloh můžete dál používat **OSDDiskIndex**. Každá instance kroku **Format a partition disk** ale používá stejnou hodnotu indexu. Chcete-li programově nastavit číslo disku pro více instancí tohoto kroku, použijte tuto vlastnost proměnné.

#### <a name="disk-type"></a>Typ disku

Typ disku, který se má formátovat Z rozevíracího seznamu můžete vybrat jednu ze dvou možností:

- **Standardní (MBR)**: hlavní spouštěcí záznam  
- **GPT**: tabulka oddílů GUID  

> [!NOTE]  
> Pokud změníte typ disku ze **standardního (MBR)** na **GPT**a rozložení oddílů obsahuje rozšířený oddíl, sekvence úloh odebere z rozložení všechny rozšířené a logické oddíly. Editor pořadí úkolů vyzve k potvrzení této akce před změnou typu disku.  

#### <a name="volume"></a>Svazek

Konkrétní informace o oddílu nebo svazku, které pořadí úkolů vytvoří, včetně následujících atributů:  

- Name  
- Zbývající místo na disku  

Pokud chcete vytvořit nový oddíl, vyberte **Nový** a otevřete tak dialogové okno **Vlastnosti oddílu** . Zadejte typ a velikost oddílu a v případě, že se jedná o spouštěcí oddíl. Pokud chcete upravit existující oddíl, vyberte oddíl, který se má upravit, a pak klikněte na tlačítko **vlastnosti** . Další informace o tom, jak nakonfigurovat oddíly pevných disků, najdete v jednom z následujících článků:  

- [Oddíly pevného disku se systémem UEFI/GPT](/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [Oddíly pevného disku se systémem BIOS/MBR](/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Pokud chcete odstranit oddíl, zvolte oddíl a pak vyberte **Odstranit**.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> Instalovat aplikaci

Tento krok nainstaluje zadané aplikace nebo sadu aplikací, které jsou definovány dynamickým seznamem proměnných pořadí úkolů. Když pořadí úkolů spustí tento krok, začne instalace aplikace okamžitě bez čekání na interval dotazování zásady.  

Aplikace musí splňovat následující kritéria:  

- Aplikace musí mít typ nasazení **Instalační služba systému Windows** nebo instalační program **skriptu** . Typy nasazení balíček aplikace systému Windows (soubor. appx) nejsou podporovány.  

- Musí běžet pod účtem Local System a nikoli s uživatelským účtem.  

- Nesmí komunikovat s plochou. Program musí běžet v tichém/bezobslužném režimu.  

- Nesmí iniciovat svoje vlastní restartování. Aplikace musí požádat o restartování pomocí standardního kódu pro restartování, 3010. Tím se zajistí, že tento krok správně zpracuje restart. Pokud aplikace vrátí ukončovací kód 3010, modul pořadí úkolů restartuje počítač. Po restartování bude pořadí úkolů automaticky pokračovat.  

> [!Note]
> Pokud aplikace [kontroluje spouštění spustitelných souborů](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check), pořadí úloh je nenainstaluje. Pokud tento krok nenastavíte tak, aby pokračoval při chybě, pak celé pořadí úkolů se nezdařilo.

Po spuštění tohoto kroku aplikace zkontroluje použitelnost pravidel požadavků a metody detekce na svých typech nasazení. Na základě výsledků této kontroly aplikace nainstaluje příslušný typ nasazení. Pokud typ nasazení obsahuje závislosti, vyhodnotí se závislý typ nasazení a nainstaluje se jako součást tohoto kroku. Závislosti aplikací nejsou podporované pro samostatná média.  

> [!NOTE]  
> Chcete-li nainstalovat aplikaci, která nahrazuje jinou aplikaci, musí být k dispozici soubory obsahu pro nahrazenou aplikaci. V opačném případě tento krok pořadí úkolů selže. Například Microsoft Visio 2010 se instaluje na klienta nebo do zaznamenané bitové kopie. Když krok **instalovat aplikaci** nainstaluje microsoft Visio 2013, soubory obsahu pro Microsoft Visio 2010 (nahrazené aplikace) musí být k dispozici v distribučním bodě. Pokud aplikace Microsoft Visio není v klientovi nebo v zaznamenané imagi nainstalována vůbec, pořadí úloh nainstaluje Microsoft Visio 2013 bez kontroly souborů obsahu Microsoft Visia 2010.  
>
> Pokud vyřadíte nahrazenou aplikaci a v pořadí úkolů je odkazováno na novou aplikaci, spuštění pořadí úloh se nezdařilo.
Toto chování je záměrné: pořadí úkolů vyžaduje všechny odkazy na aplikace.<!-- SCCMDocs 1711 -->  

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **software**a vyberte možnost **instalovat aplikaci**.

### <a name="variables-for-install-application"></a>Proměnné pro instalaci aplikace

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> Pokud klient nemůže načíst seznam bodů správy ze služeb zjišťování polohy, použijte proměnné pořadí úkolů **SMSTSMPListRequestTimeoutEnabled** a **SMSTSMPListRequestTimeout** . Tyto proměnné určují počet milisekund, po které pořadí úkolů počká, než se pokusí znovu nainstalovat aplikaci. Další informace najdete v tématu [proměnné pořadí úkolů](task-sequence-variables.md).

### <a name="cmdlets-for-install-application"></a>Rutiny pro instalaci aplikace

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](/powershell/module/configurationmanager/get-cmtsstepinstallapplication)
- [New-CMTSStepInstallApplication](/powershell/module/configurationmanager/new-cmtsstepinstallapplication)
- [Remove-CMTSStepInstallApplication](/powershell/module/configurationmanager/remove-cmtsstepinstallapplication)
- [Set-CMTSStepInstallApplication](/powershell/module/configurationmanager/set-cmtsstepinstallapplication)

### <a name="properties-for-install-application"></a>Vlastnosti pro instalaci aplikace

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení, která jsou popsaná v této části.  

#### <a name="install-the-following-applications"></a>Instalovat následující aplikace

Pořadí úkolů nainstaluje tyto aplikace v zadaném pořadí.  

Configuration Manager odfiltruje všechny zakázané aplikace nebo jakékoli aplikace s následujícím nastavením:  

- Pouze je-li přihlášen nějaký uživatel  
- Spustit s uživatelskými právy  

Tyto aplikace se nezobrazí v dialogovém okně **Vybrat aplikaci pro instalaci** .

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Instalovat aplikace podle seznamu dynamických proměnných

Pořadí úkolů nainstaluje aplikace s použitím tohoto názvu základní proměnné. Základní proměnná Název je určena pro sadu proměnných pořadí úkolů definovaných pro kolekci nebo počítač. Tyto proměnné určují aplikace, které pořadí úkolů nainstaluje pro tuto kolekci nebo počítač. Každý název proměnné se skládá z jeho běžného základního názvu plus číselná přípona začínající od 01. Hodnota pro každou proměnnou musí obsahovat název aplikace. Nic jiného.  

Pokud chcete, aby pořadí úkolů nainstalovalo aplikace pomocí seznamu dynamických proměnných, povolte na kartě **Obecné** ve **vlastnostech**aplikace následující nastavení: **Povolit instalaci této aplikace z pořadí úkolů instalace aplikace místo ručního nasazení**.  

> [!NOTE]  
> Aplikace nemůžete instalovat pomocí seznamu dynamických proměnných pro nasazení ze samostatného média.  

Pokud chcete například nainstalovat jednu aplikaci pomocí proměnné pořadí úkolů s názvem AA01, zadejte následující proměnnou:  

|Název proměnné|Hodnota proměnné|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Chcete-li nainstalovat dvě aplikace, zadejte následující proměnné:  

|Název proměnné|Hodnota proměnné|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Následující podmínky mají vliv na aplikace nainstalované pořadím úloh:  

- Pokud hodnota proměnné obsahuje jakékoliv jiné informace než název aplikace. Pořadí úkolů neinstaluje aplikaci a pořadí úkolů pokračuje.  

- Pokud pořadí úkolů nenalezne proměnnou se zadaným základním názvem a příponou 01, pořadí úkolů nenainstaluje žádné aplikace.  

> [!Important]  
> U těchto hodnot se rozlišují malá a velká písmena. Například "Install" se liší od "instalace". Pokud potřebujete změnit hodnotu, Editor pořadí úkolů nezjistí změnu velikosti písmen. Proveďte další úpravy ve stejnou dobu, například změňte popis kroku.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>V případě selhání instalace aplikace pokračujte instalováním dalších aplikací v seznamu

Toto nastavení určuje, že krok bude v případě neúspěchu instalace jednotlivých aplikací pokračovat. Pokud zadáte toto nastavení, pořadí úkolů bude pokračovat bez ohledu na chyby instalace. Pokud toto nastavení nezadáte a instalace se nezdařila, krok bude okamžitě ukončen.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Vymazat obsah aplikace z mezipaměti po instalaci

<!--4485675-->
Počínaje verzí 1906 odstraňte obsah aplikace z mezipaměti klienta po spuštění kroku. Toto chování je užitečné na zařízeních s malými pevnými disky nebo při úspěchu instalace velkého množství aplikací.


### <a name="options-for-install-application"></a>Možnosti instalace aplikace

> [!NOTE]  
> Když na kartě **Možnosti** v tomto kroku vyberete **pokračovat při chybě** , pořadí úkolů bude pokračovat i v případě, že se aplikace nebude moct nainstalovat. Pokud tuto možnost nepovolíte, pořadí úkolů se nespustí a nenainstaluje zbývající aplikace.  

Kromě výchozích možností nakonfigurujte na kartě **Možnosti** tohoto kroku pořadí úkolů následující další nastavení:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Opakovat tento krok, pokud se počítač neočekávaně restartuje

Pokud jedna z instalací aplikace neočekávaně restartuje počítač, opakujte tento krok. Tento krok umožňuje ve výchozím nastavení toto nastavení se dvěma opakováními. Můžete zadat jeden až pět opakovaných pokusů.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> Instalovat balíček

Pomocí tohoto kroku nainstalujete softwarový balíček jako součást pořadí úkolů. Po spuštění tohoto kroku se instalace začne okamžitě bez čekání na interval dotazování zásady.  

Balíček musí splňovat následující kritéria:  

- Musí běžet pod účtem Local System a nikoli s uživatelským účtem.  

- Neměl by spolupracovat s plochou. Program musí běžet v tichém/bezobslužném režimu.  

- Nesmí iniciovat svoje vlastní restartování. Software musí požádat o restart pomocí standardního kódu pro restartování, 3010. Tím se zajistí, že pořadí úkolů správně zpracuje restart. Pokud software vrátí ukončovací kód 3010, modul pořadí úkolů restartuje počítač. Po restartování bude pořadí úkolů automaticky pokračovat.  

Programy, které používají **první možnost spustit jiný program** k instalaci závislého programu, nejsou podporovány při nasazení operačního systému. Pokud povolíte možnost balíček **nejprve spustit jiný program**a závislý program již v cílovém počítači běžel, bude závislý program spuštěn a pořadí úkolů bude pokračovat. Pokud se ale závislý program v cílovém počítači ještě nespustil, krok pořadí úkolů se nezdařil.  

> [!NOTE]  
> Lokalita centrální správy nemá potřebné zásady konfigurace klienta nutné k povolení agenta distribuce softwaru během pořadí úkolů. Když vytvoříte samostatné médium pro pořadí úkolů v lokalitě centrální správy a pořadí úkolů obsahuje krok **Instalovat balíček**, v souboru CreateTsMedia.log se může objevit následující chyba:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> U samostatného média, které obsahuje krok **instalovat balíček** , vytvořte samostatné médium v primární lokalitě s povoleným agentem distribuce softwaru. Alternativně přidejte krok **Spustit příkazový řádek** za krok **nastavit systém Windows a nástroj ConfigMgr** a před první krok **instalovat balíček** . Krok **Spustit příkazový řádek** SPUSTÍ příkaz WMIC, který povolí agenta distribuce softwaru před prvním krokem **instalace balíčku** . V kroku **Spustit příkazový řádek** použijte následující příkaz:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Další informace o vytváření samostatných médií najdete v tématu [vytvoření samostatného média](../deploy-use/create-stand-alone-media.md).  

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **software**a vyberte možnost **instalovat balíček**.

### <a name="variables-for-install-package"></a>Proměnné pro instalační balíček

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Rutiny pro instalaci balíčku

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](/powershell/module/configurationmanager/get-cmtsstepinstallsoftware)
- [New-CMTSStepInstallSoftware](/powershell/module/configurationmanager/new-cmtsstepinstallsoftware)
- [Remove-CMTSStepInstallSoftware](/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware)
- [Set-CMTSStepInstallSoftware](/powershell/module/configurationmanager/set-cmtsstepinstallsoftware)

> [!TIP]
> Pokud chcete stáhnout příslušný balíček s upgradem pro operační systém před tím, než uživatel nainstaluje pořadí úkolů, použijte předběžné ukládání obsahu do mezipaměti. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).

### <a name="properties-for-install-package"></a>Vlastnosti balíčku pro instalaci

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="install-a-single-software-package"></a>Instalovat jeden balíček softwaru

Toto nastavení určuje Configuration Manager softwarový balíček. Krok počká, až se instalace dokončí.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Instalovat balíčky softwaru podle seznamu dynamických proměnných

Pořadí úkolů nainstaluje balíčky pomocí tohoto názvu základní proměnné. Základní proměnná Název je určena pro sadu proměnných pořadí úkolů definovaných pro kolekci nebo počítač. Tyto proměnné určují balíčky, které pořadí úkolů nainstaluje pro tuto kolekci nebo počítač. Každý název proměnné se skládá z jeho běžného základního názvu plus číselná přípona začínající od 001. Hodnota pro každou proměnnou musí obsahovat ID a název softwaru oddělené dvojtečkou.  

Chcete-li pořadí úkolů nainstalovat software pomocí dynamického seznamu proměnných, povolte následující nastavení na kartě **Upřesnit** ve **vlastnostech**balíčku: **Povolit instalaci tohoto programu z pořadí úloh instalace balíčku bez nasazení**.  

> [!NOTE]  
> Softwarové balíčky nemůžete instalovat pomocí seznamu dynamických proměnných pro nasazení ze samostatného média.  

Pokud chcete například nainstalovat jeden softwarový balíček pomocí proměnné pořadí úkolů s názvem AA001, zadejte následující proměnnou:  

|Název proměnné|Hodnota proměnné|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Pokud byste chtěli nainstalovat tři softwarové balíčky, zadali byste následující proměnné:  

|Název proměnné|Hodnota proměnné|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

Následující podmínky ovlivňují balíčky nainstalované pořadím úloh:  

- Pokud nevytvoříte hodnotu proměnné ve správném formátu nebo neurčíte platné ID a název balíčku, instalace softwaru se nezdařila.  

- Pokud ID balíčku obsahuje malá písmena, instalace softwaru se nezdařila.  

- Pokud pořadí úkolů nenalezne proměnnou se zadaným základním názvem a příponou "001", pořadí úkolů neinstaluje žádné balíčky. Pořadí úkolů pokračuje.  

> [!Important]  
> U těchto hodnot se rozlišují malá a velká písmena. Například "Install" se liší od "instalace". Pokud potřebujete změnit hodnotu, Editor pořadí úkolů nezjistí změnu velikosti písmen. Proveďte další úpravy ve stejnou dobu, například změňte popis kroku.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>V případě selhání instalace balíčku softwaru pokračovat v instalaci dalších balíčků v seznamu

Toto nastavení určuje, že krok bude v případě selhání instalace jednotlivých softwarových balíčků vždycky pokračovat dál. Pokud zadáte toto nastavení, pořadí úkolů bude pokračovat bez ohledu na chyby instalace. Pokud toto nastavení nezadáte a instalace se nezdařila, krok bude okamžitě ukončen.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Instalovat aktualizace softwaru

Pomocí tohoto kroku nainstalujete do cílového počítače aktualizace softwaru. V cílovém počítači se nevyhodnocují příslušné aktualizace softwaru, dokud se tento krok pořadí úkolů nespustí. V tuto chvíli se v cílovém počítači vyhodnotí aktualizace softwaru jako u jakéhokoli jiného klienta Configuration Manager. Chcete-li tento krok nainstalovat aktualizace softwaru, nasaďte aktualizace nejprve do kolekce, do které je cílový počítač členem.  

> [!IMPORTANT]  
> Nejlepšího výkonu dosáhnete, když nainstalujete nejnovější verzi agenta web Windows Update.  

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **software**a vyberte možnost **instalovat aktualizace softwaru**.

### <a name="variables-for-install-software-updates"></a>Proměnné pro instalaci aktualizací softwaru

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Pokud klient nemůže načíst seznam bodů správy ze služeb zjišťování polohy, použijte proměnné **SMSTSMPListRequestTimeoutEnabled** a **SMSTSMPListRequestTimeout** . Tyto proměnné určují počet milisekund, po které pořadí úkolů počká, než se znovu pokusí o instalaci aplikace nebo aktualizace softwaru. Další informace najdete v tématu [proměnné pořadí úkolů](task-sequence-variables.md).  

### <a name="cmdlets-for-install-software-updates"></a>Rutiny pro instalaci aktualizací softwaru

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](/powershell/module/configurationmanager/get-cmtsstepinstallupdate)
- [New-CMTSStepInstallUpdate](/powershell/module/configurationmanager/new-cmtsstepinstallupdate)
- [Remove-CMTSStepInstallUpdate](/powershell/module/configurationmanager/remove-cmtsstepinstallupdate)
- [Set-CMTSStepInstallUpdate](/powershell/module/configurationmanager/set-cmtsstepinstallupdate)

Další doporučení a diagram technického toku pro tento krok najdete v tématu [instalace aktualizací softwaru](install-software-updates.md).

### <a name="properties-for-install-software-updates"></a>Vlastnosti pro instalaci aktualizací softwaru

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Instalace nutná – jenom povinné aktualizace softwaru

Tuto možnost vyberte, pokud chcete nainstalovat všechny povinné aktualizace softwaru s konečným termínem instalace definovaným správcem.  

#### <a name="available-for-installation---all-software-updates"></a>K dispozici pro instalaci – všechny aktualizace softwaru

Tuto možnost vyberte, pokud chcete nainstalovat všechny dostupné aktualizace softwaru. Nejprve tyto aktualizace nasaďte do kolekce, do které je počítač členem. Pořadí úkolů nainstaluje všechny dostupné aktualizace softwaru na cílové počítače.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Vyhodnotit aktualizace softwaru z výsledků kontroly v mezipaměti

Ve výchozím nastavení používá tento krok výsledky kontroly uložené v mezipaměti od agenta web Windows Update. Vypnutím této možnosti dáte pokyn agentovi web Windows Update stáhnout nejnovější katalog z bodu aktualizace softwaru. Tuto možnost povolte, pokud chcete [zachytit a sestavit image operačního systému](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)pomocí pořadí úkolů. V tomto scénáři je pravděpodobný velký počet aktualizací softwaru.

Mnohé z těchto aktualizací mají závislosti. Například nainstalujte aktualizaci ABC, aby se zdá, že se aktualizuje XYZ. Když toto nastavení zakážete a nasadíte pořadí úkolů na mnoho klientů, připojí se k bodu aktualizace softwaru ve stejnou dobu. Výsledkem tohoto chování je problémy s výkonem během procesu a stahování katalogu aktualizací.

Ve většině případů použijte výchozí nastavení pro použití výsledků kontroly uložené v mezipaměti.

Proměnná **SMSTSSoftwareUpdateScanTimeout** řídí časový limit kontroly aktualizací softwaru v průběhu tohoto kroku. Výchozí hodnota je 60 minut. Další informace najdete v tématu [proměnné pořadí úkolů](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### <a name="options-for-install-software-updates"></a>Možnosti instalace aktualizací softwaru

Kromě výchozích možností nakonfigurujte na kartě **Možnosti** tohoto kroku pořadí úkolů následující další nastavení:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Opakovat tento krok, pokud se počítač neočekávaně restartuje

Pokud jedna z aktualizací neočekávaně restartuje počítač, opakujte tento krok. Tento krok umožňuje ve výchozím nastavení toto nastavení se dvěma opakováními. Můžete zadat jeden až pět opakovaných pokusů.  

> [!NOTE]  
> Nakonfigurujte proměnnou **SMSTSWaitForSecondReboot** a určete, kolik sekund se pořadí úkolů po restartování počítače v tomto scénáři pozastaví. Další informace najdete v tématu [proměnné pořadí úkolů](task-sequence-variables.md#SMSTSWaitForSecondReboot).  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Připojit k doméně nebo pracovní skupině

Pomocí tohoto kroku přidáte cílový počítač do pracovní skupiny nebo domény.  

> [!NOTE]
> Když klient připojený k Azure Active Directory (Azure AD) spustí pořadí úloh nasazení operačního systému, klient v novém operačním systému se automaticky nepřipojí k Azure AD. I když není připojený k Azure AD, klient se pořád spravuje.

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **připojit k doméně nebo pracovní skupině**.

### <a name="variables-for-join-domain-or-workgroup"></a>Proměnné pro připojení k doméně nebo pracovní skupině

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Rutiny pro připojení k doméně nebo pracovní skupině

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup)
- [New-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup)
- [Remove-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup)
- [Set-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup)

### <a name="properties-for-join-domain-or-workgroup"></a>Vlastnosti pro připojení k doméně nebo pracovní skupině

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="join-a-workgroup"></a>Připojit k pracovní skupině

Tuto možnost vyberte, pokud chcete mít cílový počítač připojený ke konkrétní pracovní skupině. Pokud je počítač aktuálně členem domény, výběr této možnosti způsobí, že se počítač restartuje.  

#### <a name="join-a-domain"></a>Připojení k doméně

Tuto možnost vyberte, pokud chcete mít cílový počítač připojený ke konkrétní doméně.  

V případě potřeby zadejte nebo vyhledejte organizační jednotku (OU) v zadané doméně, ke které se má počítač připojit. Pokud je počítač aktuálně členem některé jiné domény nebo pracovní skupiny, tato možnost způsobí, že se počítač restartuje. Pokud je počítač již členem jiné organizační jednotky, protože Active Directory Domain Services nepovoluje změnu organizační jednotky prostřednictvím této metody, instalační program systému Windows toto nastavení ignoruje.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Zadejte účet, který má oprávnění pro připojení do domény

Vyberte **nastavit** a zadejte uživatelské jméno a heslo pro účet s oprávněním pro připojení k doméně. Zadejte účet ve formátu:  `Domain\account` . Další informace o účtu připojení k doméně pořadí úkolů najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> Připravit klienta nástroje ConfigMgr pro zaznamenání

Tento krok použijte k odebrání nebo konfiguraci klienta Configuration Manager v referenčním počítači. Tato akce připraví počítač k zaznamenání jako součást procesu vytváření imagí.

Tento krok úplně odebere klienta Configuration Manager, místo aby se odebraly jenom informace o klíči. Když pořadí úkolů nasadí zachycenou image operačního systému, nainstaluje se vždy nový Configuration Manager klienta.  

> [!TIP]
> Ve výchozím nastavení modul pořadí úloh odebere klienta pouze během **sestavování a zaznamenání referenčního pořadí úloh operačního systému** . Modul pořadí úloh neodebere klienta během jiných metod zachycení, například záznamového média nebo vlastního pořadí úkolů. Toto chování můžete overide pro pořadí úkolů nasazení operačního systému. Před krok **připravit klienta nástroje ConfigMgr pro zaznamenání** nastavte proměnnou pořadí úloh **SMSTSUninstallCCMClient** na **hodnotu true** . Tato proměnná a chování se vztahuje jenom na pořadí úkolů nasazení operačního systému. Po příštím restartování zařízení odebere klienta.

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové kopie**a vyberte možnost **připravit klienta nástroje ConfigMgr pro zaznamenání**.


### <a name="variables-for-prepare-configmgr-client-for-capture"></a>Proměnné pro přípravu klienta nástroje ConfigMgr pro zaznamenání

V tomto kroku použijte následující proměnné pořadí úkolů:  

- SMSTSUninstallCCMClient


### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>Rutiny pro přípravu klienta nástroje ConfigMgr pro zaznamenání

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient)
- [New-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient)
- [Remove-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient)
- [Set-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Příprava Windows pro zachytávání

Pomocí tohoto kroku můžete zadat možnosti nástroje Sysprep při zaznamenávání image operačního systému v referenčním počítači. Tento krok spustí nástroj Sysprep a potom restartuje počítač do spouštěcí image prostředí Windows PE zadané pro pořadí úkolů. Tato akce se nezdařila, pokud je referenční počítač připojen k doméně.  

Tento krok se spouští jenom v plném operačním systému. Neběží v systému Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové kopie**a vyberte možnost **připravit systém Windows pro zaznamenání**.

### <a name="variables-for-prepare-windows-for-capture"></a>Proměnné pro přípravu systému Windows pro zachytávání

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Rutiny pro přípravu Windows pro zachytávání

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows)
- [New-CMTSStepPrepareWindows](/powershell/module/configurationmanager/New-CMTSStepPrepareWindows)
- [Remove-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows)
- [Set-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows)

### <a name="properties-for-prepare-windows-for-capture"></a>Vlastnosti pro přípravný systém Windows pro zaznamenání

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Automaticky sestavit seznam ovladačů velkokapacitního úložiště

Tuto možnost vyberte, pokud chcete, aby nástroj Sysprep automaticky sestavil seznam ovladačů velkokapacitních paměťových zařízení z referenčního počítače. Tato možnost umožňuje použít v referenčním počítači v souboru sysprep.inf možnost pro sestavení ovladačů velkokapacitních paměťových zařízení. Další informace o tomto nastavení najdete v dokumentaci k nástroji Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>Neresetovat příznak aktivace

Tuto možnost vyberte, pokud chcete nástroji Sysprep zabránit v resetování příznaku aktivace produktu.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Po spuštění této akce vypnout počítač

<!--SCCMDocs-pr issue 2695-->
Tato možnost instruuje nástroj Sysprep, aby vypnul počítač namísto výchozího chování při restartování.

Pořadí úloh [Windows autopilot pro stávající zařízení](../../../autopilot/existing-devices.md) používá tento krok s touto možností.

- Pokud chcete, aby pořadí úkolů aktualizovalo zařízení a pak hned spouštělo počáteční nastavení pro autopilot, nechte tuto možnost Vypnuto.  

- Tuto možnost povolte, pokud chcete zařízení po vytvoření bitové kopie vypnout. Potom můžete zařízení doručovat uživateli, který spustí OOBE s autopilotem při prvním zapnutí.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> Předem zřídit nástroj BitLocker

Tento krok použijte, pokud chcete zapnout BitLocker na jednotce v prostředí Windows PE. Ve výchozím nastavení je zašifrováno pouze použité místo na disku, takže doba šifrování je mnohem rychlejší. Možnosti správy klíčů aplikujete pomocí kroku [zapnout nástroj BitLocker](#BKMK_EnableBitLocker) po instalaci operačního systému.

> [!IMPORTANT]
> Předběžné poskytování BitLockeru vyžaduje, aby počítač měl podporovaný a povolený čip TPM (Trusted Platform Module).

Tento krok běží jenom v prostředí Windows PE. Neběží v plném operačním systému.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **disky**a vyberte možnost **předem zřídit nástroj BitLocker**.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>Rutiny pro předběžné poskytování nástroje BitLocker

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker)
- [New-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker)
- [Remove-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker)
- [Set-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker)

### <a name="properties-for-pre-provision-bitlocker"></a>Vlastnosti pro předběžné poskytnutí nástroje BitLocker

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Použít na vybranou jednotku nástroj BitLocker

Zadejte jednotku, pro kterou chcete nástroj BitLocker povolit. BitLocker zašifruje jenom využité místo na jednotce.  

#### <a name="disk-encryption-mode"></a>Režim šifrování disku

<!--6995601-->
Počínaje verzí 2006 vyberte jeden z následujících šifrovacích algoritmů:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Ve výchozím nastavení nebo pokud není zadaný, bude tento krok dál používat výchozí metodu šifrování pro verzi operačního systému. Pokud tento krok běží na verzi Windows, která nepodporuje zadaný algoritmus, vrátí se k výchozímu operačnímu systému. V této situaci modul pořadí úkolů odešle stavovou zprávu 11911.

#### <a name="use-full-disk-encryption"></a>Použít úplné šifrování disku

<!--SCCMDocs-pr issue 2671-->
Ve výchozím nastavení tento krok zašifruje jenom využité místo na jednotce. Toto výchozí chování se doporučuje, protože je rychlejší a efektivnější. Pokud vaše organizace vyžaduje šifrování celé jednotky během instalace, pak tuto možnost povolte. Instalační program systému Windows čeká na zašifrování celé jednotky, což trvá dlouhou dobu, zejména u velkých jednotek.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Přeskočit tento krok pro počítače, které nemají TPM, nebo když není TPM povoleno

Tuto možnost vyberte, pokud chcete přeskočit šifrování jednotky v počítači, který neobsahuje podporovaný nebo povolený čip TPM. Tuto možnost můžete například použít při nasazování operačního systému do virtuálního počítače. Ve výchozím nastavení je toto nastavení povoleno pro krok **předem zřídit nástroj BitLocker** . Tento krok se nezdařil v zařízení bez čipu TPM nebo čipu TPM, který neinicializuje. Pokud zařízení nemá funkční čip TPM, počínaje verzí 2006, modul pořadí úkolů zaznamená upozornění do protokolu souboru Smsts. log a odešle stavovou zprávu 11912.



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Úložiště stavu uvolnění

Pomocí tohoto kroku můžete bodu migrace stavu sdělit, že se dokončila akce zachycení nebo obnovení. Tento krok použijte ve spojení s kroky **úložiště stavu požadavku**, **zaznamenat stav uživatele**a **Obnovit stav uživatele** . Tento postup slouží k migraci dat stavu uživatele pomocí bodu migrace stavu a Nástroj pro migraci uživatelských souborů a nastavení (USMT).  

Další informace o správě stavu uživatele při nasazování operačních systémů najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  

Použijete-li krok **úložiště stavu požadavku** k vyžádání přístupu k bodu migrace stavu za účelem *zachycení* stavu uživatele, tento krok upozorní bod migrace stavu, že proces zachycení je dokončen. Bod migrace stavu pak označí data o stavu uživatele jako dostupná pro obnovení. Bod migrace stavu nastaví oprávnění řízení přístupu pro data stavu uživatele tak, že pouze obnovující počítač má přístup jen pro čtení.  

Použijete-li krok **úložiště stavu požadavku** k vyžádání přístupu k bodu migrace stavu za účelem *obnovení* stavu uživatele, tento krok upozorní bod migrace stavu, že proces obnovení byl dokončen. Bod migrace stavu pak aktivuje jeho nakonfigurovaná nastavení uchovávání dat.  

> [!IMPORTANT]  
> U všech kroků mezi kroky **úložiště stavu požadavku** a **úložiště stavu uvolnění** nastavte možnost **pokračovat při chybě** . Každý krok **úložiště stavu požadavku** musí mít porovnávací krok **úložiště stavu uvolnění** .  

Tento krok se spouští jenom v plném operačním systému. Neběží v systému Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **stav uživatele**a vyberte položku **úložiště stavu uvolnění**.

### <a name="variables-for-release-state-store"></a>Proměnné pro úložiště stavu uvolnění

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Rutiny pro úložiště stavu uvolnění

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore)
- [New-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore)
- [Remove-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore)
- [Set-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore)

### <a name="properties-for-release-state-store"></a>Vlastnosti pro úložiště stavu uvolnění

Tento krok nevyžaduje žádné nastavení na kartě **vlastnosti** .



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> Úložiště stavu požadavku

Tento krok použijte k vyžádání přístupu k bodu migrace stavu při zachytávání nebo obnovování stavu.  

Další informace o správě stavu uživatele při nasazování operačních systémů najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  

Tento krok použijte ve spojení s kroky **úložiště stavu uvolnění**, **zaznamenat stav uživatele**a **Obnovit stav uživatele** . Pomocí těchto kroků migrujete stav počítače pomocí bodu migrace stavu a Nástroj pro migraci uživatelských souborů a nastavení (USMT).  

> [!NOTE]  
> Když vytváříte nový bod migrace stavu, úložiště stavů uživatele není k dispozici po dobu až jedné hodiny. Chcete-li zrychlit dostupnost, upravte nastavení vlastností bodu migrace stavu tak, aby se aktivovala aktualizace souboru ovládacího prvku lokality.  

Tento krok běží v úplném operačním systému a v prostředí Windows PE pro offline USMT.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **stav uživatele**a vyberte položku **úložiště stavu požadavku**.

### <a name="variables-for-request-state-store"></a>Proměnné pro úložiště stavu požadavku

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Rutiny pro úložiště stavu požadavku

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore)
- [New-CMTSStepRequestStateStore](/powershell/module/configurationmanager/New-CMTSStepRequestStateStore)
- [Remove-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore)
- [Set-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore)

### <a name="properties-for-request-state-store"></a>Vlastnosti úložiště stavu požadavku

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="capture-state-from-the-computer"></a>Zaznamenat stav z počítače

Vyhledejte bod migrace stavu, který splňuje minimální požadavky nakonfigurované v nastavení bodu migrace stavu. Například **maximální počet klientů** a **minimální velikost volného místa na disku**. Tato možnost nezaručuje dostatek místa v době migrace stavu. Tato možnost vyžaduje přístup k bodu migrace stavu za účelem zachycení stavu uživatele a nastavení z počítače.  

Pokud má lokalita Configuration Manager více aktivních bodů migrace stavu, tento krok najde bod migrace stavu s dostupným místem na disku. Pořadí úloh provede dotaz na bod správy pro seznam bodů migrace stavu a pak je vyhodnotí, dokud nenalezne ten, který splňuje minimální požadavky.  

#### <a name="restore-state-from-another-computer"></a>Obnovit stav z jiného počítače

Požádat o přístup k bodu migrace stavu, aby obnovil dříve zaznamenaný stav a nastavení uživatele do cílového počítače.  

Pokud existuje více bodů migrace stavu, tento krok najde bod migrace stavu, který má stav pro cílový počítač.  

#### <a name="number-of-retries"></a>Počet opakovaných pokusů

Počet, kolikrát se tento krok pokusí najít odpovídající bod migrace stavu, než selže.  

#### <a name="retry-delay-in-seconds"></a>Zpoždění při opakování (v sekundách)

Doba v sekundách, kterou krok pořadí úkolů čeká mezi pokusy o opakování.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Pokud se účtu počítače nepovede připojit k úložišti stavů, použijte účet pro přístup k síti.

Pokud pořadí úloh nemá přístup k bodu migrace stavu pomocí účtu počítače, připojte se k němu přihlašovací údaje účtu pro přístup k síti. Tato možnost je méně bezpečná, protože jiné počítače by mohly použít účet přístupu k síti pro přístup k uloženému stavu. Tato možnost může být nutná v případě, že cílový počítač není připojený k doméně.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> Restartovat počítač

Tento krok použijte k restartování počítače, na kterém pořadí úkolů běží. Po restartování bude počítač automaticky pokračovat dalším krokem v pořadí úkolů.  

Tento krok lze spustit v úplném operačním systému nebo prostředí Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **restartovat počítač**.

### <a name="variables-for-restart-computer"></a>Proměnné pro restartování počítače

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Rutiny pro restartování počítače

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](/powershell/module/configurationmanager/get-cmtsstepreboot)
- [New-CMTSStepReboot](/powershell/module/configurationmanager/new-cmtsstepreboot)
- [Remove-CMTSStepReboot](/powershell/module/configurationmanager/remove-cmtsstepreboot)
- [Set-CMTSStepReboot](/powershell/module/configurationmanager/set-cmtsstepreboot)

### <a name="properties-for-restart-computer"></a>Vlastnosti pro restartování počítače

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>Bitová spouštěcí kopie přiřazená tomuto pořadí úloh

Tuto možnost vyberte, pokud má cílový počítač používat spouštěcí bitovou kopii, která je přiřazená k pořadí úkolů. Pořadí úkolů používá spouštěcí bitovou kopii ke spouštění dalších kroků v systému Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>Aktuálně nainstalovaný výchozí operační systém

Tuto možnost vyberte, pokud chcete cílový počítač restartovat do nainstalovaného operačního systému.  

#### <a name="notify-the-user-before-restarting"></a>Před restartováním upozornit uživatele

Tuto možnost vyberte, pokud chcete uživateli zobrazit oznámení před tím, než se cílový počítač restartuje. Tento krok ve výchozím nastavení vybere tuto možnost.  

#### <a name="notification-message"></a>Oznámení

Zadejte zprávu oznámení, která se zobrazí uživateli před restartováním cílového počítače.  

#### <a name="message-display-time-out"></a>Časový limit zobrazení zprávy

Zadejte dobu v sekundách, po jejímž uplynutí bude restartován cílový počítač. Výchozí hodnota je 60 sekund.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Obnovit stav uživatele

Pomocí tohoto kroku spustíte Nástroj pro migraci uživatelských souborů a nastavení (USMT) pro obnovení stavu a nastavení uživatele do cílového počítače. Tento krok se používá ve spojení s krokem **zaznamenat stav uživatele** .  

Další informace o správě stavu uživatele při nasazování operačních systémů najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  

Tento krok použijte s kroky úložiště **stavu požadavku** a **úložiště stavu uvolnění** k uložení nebo obnovení nastavení stavu s bodem migrace stavu. Tato možnost vždycky dešifruje úložiště stavů USMT pomocí šifrovacího klíče, který Configuration Manager generuje a spravuje.  

Krok **Obnovit stav uživatele** poskytuje kontrolu nad určitou podmnožinou nejčastěji používaných možností nástroje USMT. Zadejte další možnosti příkazového řádku s proměnnou **proměnné OSDMigrateAdditionalRestoreOptions** .  

> [!IMPORTANT]  
> Pokud tento krok používáte pro účel, který nesouvisí se scénářem nasazení operačního systému, přidejte ihned krok [restartovat počítač](#BKMK_RestartComputer) hned za krok **Obnovit stav uživatele** .  

Tento krok se spouští jenom v plném operačním systému. Neběží v systému Windows PE.

Pokud chcete přidat tento krok v editoru pořadí úloh, vyberte **Přidat**, vyberte **stav uživatele**a vyberte **Obnovit stav uživatele**.

### <a name="variables-for-restore-user-state"></a>Proměnné pro obnovení stavu uživatele

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Rutiny pro obnovení stavu uživatele

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState)
- [New-CMTSStepRestoreUserState](/powershell/module/configurationmanager/New-CMTSStepRestoreUserState)
- [Remove-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState)
- [Set-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState)

### <a name="properties-for-restore-user-state"></a>Vlastnosti pro obnovení stavu uživatele

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="user-state-migration-tool-package"></a>Balíček nástroje pro migraci stavu uživatele

Zadejte balíček, který obsahuje verzi nástroje USMT pro tento krok, který se má použít. Tento balíček nevyžaduje program. Při spuštění kroku pořadí úkolů použije verzi nástroje USMT v zadaném balíčku. Zadejte balíček obsahující 32 nebo 64 verzi nástroje USMT pro bitovou kopii. Architektura nástroje USMT závisí na architektuře operačního systému, na kterou pořadí úkolů obnovuje stav.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Obnovit všechny zaznamenané profily uživatelů pomocí standardních možností

Obnoví zaznamenané profily uživatelů se standardními možnostmi. Chcete-li přizpůsobit možnosti, které nástroj USMT obnoví, vyberte možnost **přizpůsobit zachytávání profilů uživatelů**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Přizpůsobit způsob obnovení profilů

Umožňuje upravit soubory, které chcete obnovit do cílového počítače. Vyberte **soubory** a určete konfigurační soubory v balíčku USMT, které chcete použít pro obnovení profilů uživatelů. Pokud chcete přidat konfigurační soubor, zadejte název souboru do pole **název** souboru a pak vyberte **Přidat**. V podokně soubory jsou uvedené konfigurační soubory, které nástroj USMT používá. Soubor. XML, který určíte, definuje, který uživatel bude nástroj USMT obnovovat.  

#### <a name="restore-local-computer-user-profiles"></a>Obnovit profily uživatelů místního počítače

Obnoví profily uživatelů místního počítače. Tyto profily nejsou pro uživatele domény. Pro obnovené místní uživatelské účty přiřaďte nová hesla. Nástroj USMT nemůže migrovat původní hesla. Zadejte nové heslo do pole **Heslo** a potvrzení hesla do pole **Potvrdit heslo**.  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Pokračovat, i když některé soubory nelze obnovit

Pokračuje v obnovování stavu a nastavení uživatele i v případě, že nástroj USMT nemůže obnovit některé soubory. Tento krok ve výchozím nastavení povolí tuto možnost. Pokud tuto možnost zakážete a nástroj USMT při obnovování souborů zjistí chyby, tento krok se okamžitě nezdařil. Nástroj USMT neobnoví všechny soubory.

#### <a name="enable-verbose-logging"></a>Zapnout podrobné protokolování

Tuto možnost povolte, pokud chcete v souboru protokolu vygenerovat podrobnější informace. Při obnovování stavu se ve výchozím nastavení pořadí úkolů ve složce protokolu pořadí úkolů generuje **LoadState. log** `%WinDir%\ccm\logs` .  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> Spustit příkazový řádek

Pomocí tohoto kroku spustíte zadaný příkazový řádek.  

Spuštěný příkaz musí splňovat následující kritéria:  

- Neměl by spolupracovat s plochou. Příkaz musí běžet v tichém režimu nebo v bezobslužném režimu.  

- Nesmí iniciovat svoje vlastní restartování. Příkaz musí požádat o restart pomocí standardního kódu pro restartování, 3010. Tím se zajistí, že pořadí úkolů správně zpracuje restart. Pokud příkaz vrátí ukončovací kód 3010, modul pořadí úkolů restartuje počítač. Po restartování bude pořadí úkolů automaticky pokračovat.

Tento krok lze spustit v úplném operačním systému nebo prostředí Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **Spustit příkazový řádek**.

### <a name="variables-for-run-command-line"></a>Proměnné pro příkazový řádek spuštění

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (počínaje verzí 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (počínaje verzí 2002)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Rutiny pro příkazový řádek pro spuštění

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](/powershell/module/configurationmanager/get-cmtsstepruncommandline)
- [New-CMTSStepRunCommandLine](/powershell/module/configurationmanager/new-cmtsstepruncommandline)
- [Remove-CMTSStepRunCommandLine](/powershell/module/configurationmanager/remove-cmtsstepruncommandline)
- [Set-CMTSStepRunCommandLine](/powershell/module/configurationmanager/set-cmtsstepruncommandline)

### <a name="properties-for-run-command-line"></a>Vlastnosti příkazového řádku pro spuštění

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="command-line"></a>Příkazový řádek

Určuje příkazový řádek, který pořadí úkolů spouští. Toto pole je vyžadováno. Zadejte přípony názvů souborů, například. vbs a. exe. Zahrňte všechny požadované soubory nastavení a možnosti příkazového řádku.  

Pokud nezadáte příponu názvu souboru, Configuration Manager pokusy. com,. exe a. bat. Pokud má název souboru příponu, která není typu spustitelného souboru, Configuration Manager se pokusí použít místní přidružení. Například pokud je příkazový řádek readme.gif, Configuration Manager spustí aplikaci určenou v cílovém počítači pro otevírání souborů. gif.  

Příklady:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Chcete-li úspěšně spustit, před akcemi příkazového řádku pomocí příkazu **cmd.exe/c** . Mezi tyto akce patří například přesměrování výstupu, potrubí a příkazy kopírování.  

#### <a name="output-to-task-sequence-variable"></a>Výstup do proměnné pořadí úkolů

<!--user story 4977616/bug 4798352-->

Počínaje verzí 1910 uložte výstup příkazu do vlastní proměnné pořadí úkolů.

> [!Note]  
> Configuration Manager omezuje tento výstup na posledních 1000 znaků.

#### <a name="disable-64-bit-file-system-redirection"></a>Vypnout přesměrování 64bitového systému souborů

Ve výchozím nastavení používají 64 operační systémy přesměrovač systému souborů WOW64 ke spouštění příkazových řádků. Toto chování je správně najít 32 bitů a knihoven spustitelných souborů operačního systému. Tuto možnost vyberte, pokud chcete zakázat používání přesměrovače systému souborů WOW64. Systém Windows spustí příkaz pomocí nativních 64 verzí spustitelných souborů a knihoven operačního systému. Tato možnost nemá žádný vliv, pokud je spuštěná v 32 operačním systému.  

#### <a name="start-in"></a>Spustit v:

Určuje složku spustitelného souboru programu (maximálně 127 znaků). Tato složka může představovat absolutní cestu k cílovému počítači nebo relativní cestu ke složce distribučního bodu obsahující balíček. Toto pole je volitelné.  

Příklady:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> Tlačítko **Procházet** prochází místní počítač se soubory a složkami. Cokoli, co vyberete, musí existovat také v cílovém počítači. Musí existovat ve stejném umístění a se stejnými názvy souborů a složek.  

#### <a name="package"></a>Balíček

Když na příkazovém řádku zadáte soubory nebo programy, které ještě nejsou v cílovém počítači, vyberte tuto možnost, pokud chcete zadat balíček Configuration Manager, který obsahuje potřebné soubory. Balíček nevyžaduje program. Pokud zadané soubory existují v cílovém počítači, tato možnost není povinná.  

#### <a name="time-out"></a>Časový limit

Určuje hodnotu, která představuje, jak dlouho Configuration Manager povolit spuštění příkazového řádku. Tato hodnota může být od 1 minuty do 999 minut. Výchozí hodnota je 15 minut. Tato možnost je ve výchozím nastavení zakázána.  

> [!IMPORTANT]  
> Pokud zadáte hodnotu, která nepovolí dostatek času pro úspěšné dokončení zadaného příkazu, tento krok se nezdaří. V závislosti na podmínkách kroku nebo skupiny by mohlo dojít k selhání celého pořadí úkolů. Pokud časový limit vyprší, Configuration Manager ukončí proces příkazového řádku.  

#### <a name="run-this-step-as-the-following-account"></a>Spustit tento krok jako následující účet

Určuje, že se má příkazový řádek spustit jako jiný uživatelský účet systému Windows než účet místního systému.  

> [!NOTE]  
> Chcete-li spustit jednoduché skripty nebo příkazy s jiným účtem po instalaci operačního systému, přidejte nejprve účet do počítače. Kromě toho může být nutné obnovit uživatelské profily Windows pro spouštění složitějších programů, jako je například Instalační služba systému Windows.  

#### <a name="account"></a>Účet

Určuje uživatelský účet systému Windows, který tento krok používá ke spuštění příkazového řádku. Příkazový řádek se spustí s oprávněními zadaného účtu. Vyberte možnost **nastavit** a zadejte účet místního uživatele nebo domény. Další informace o účtu Spustit jako pro pořadí úloh najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Pokud tento krok Určuje uživatelský účet a spustí se v prostředí Windows PE, akce se nezdařila. K doméně se nedá připojit prostředí Windows PE. V souboru **souboru Smsts. log** se zaznamená toto selhání.  

### <a name="options-for-run-command-line"></a>Možnosti příkazového řádku pro spuštění

Kromě výchozích možností nakonfigurujte na kartě **Možnosti** tohoto kroku pořadí úkolů následující další nastavení:  

#### <a name="success-codes"></a>Kódy úspěchu

Do skriptu zahrňte další ukončovací kódy, které by měl krok vyhodnotit jako úspěšný.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> Spustit skript prostředí PowerShell

Pomocí tohoto kroku spustíte zadaný skript prostředí Windows PowerShell.  

Skript musí splňovat následující kritéria:  

- Neměl by spolupracovat s plochou. Skript musí běžet v tichém nebo v bezobslužném režimu.  

- Nesmí iniciovat svoje vlastní restartování. Sscript musí požádat o restart pomocí standardního kódu pro restartování, 3010. Tím se zajistí, že pořadí úkolů správně zpracuje restart. Pokud skript vrátí ukončovací kód 3010, modul pořadí úkolů restartuje počítač. Po restartování bude pořadí úkolů automaticky pokračovat.

Tento krok lze spustit v úplném operačním systému nebo prostředí Windows PE. Pokud chcete tento krok spustit v prostředí Windows PE, povolte ve spouštěcí imagi PowerShell. Na kartě **volitelné součásti** ve vlastnostech pro spouštěcí bitovou kopii povolte komponentu WinPE-PowerShell. Další informace o tom, jak změnit spouštěcí image, najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

> [!NOTE]  
> V operačních systémech Windows Embedded není PowerShell ve výchozím nastavení povolen.  

> [!WARNING]
> Určitý antimalwarový software může nechtěně aktivovat události proti Configuration Manager kroku pořadí úkolů Spustit skript prostředí PowerShell. Doporučuje se vyloučit%windir%\temp\smstspowershellscripts, aby antimalwarový software mohl spouštět tyto skripty bez rušivých zásahů.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **Spustit skript prostředí PowerShell**.

### <a name="variables-for-run-powershell-script"></a>Proměnné pro spuštění skriptu PowerShellu

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (počínaje verzí 1902)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (počínaje verzí 2002)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>Rutiny pro spuštění skriptu PowerShellu

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/get-cmtssteprunpowershellscript)
- [New-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/new-cmtssteprunpowershellscript)
- [Remove-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript)
- [Set-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/set-cmtssteprunpowershellscript)

> [!Note]  
> Používejte podepsané skripty PowerShellu ve formátu Unicode. Formát ANSI, který je výchozí, nefunguje s tímto krokem.

### <a name="properties-for-run-powershell-script"></a>Vlastnosti pro spuštění skriptu PowerShellu

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="package"></a>Balíček

Zadejte balíček Configuration Manager, který obsahuje skript prostředí PowerShell. Jeden balíček může obsahovat několik skriptů prostředí PowerShell.  

#### <a name="script-name"></a>Název skriptu

Určuje název skriptu prostředí PowerShell, který se má spustit. Toto pole je vyžadováno.  

#### <a name="enter-a-powershell-script"></a>Zadejte PowerShellový skript.

<!-- 3556028 -->
Počínaje verzí 1902 zadejte do tohoto kroku přímo kód Windows PowerShellu. Tato funkce umožňuje spustit příkazy prostředí PowerShell během pořadí úkolů bez předchozího vytvoření a distribuce balíčku pomocí skriptu.

Když přidáte nebo upravíte skript, okno skriptu PowerShellu poskytuje následující akce:  

- Přímo upravit skript  

- Otevřít existující skript ze souboru  

- Přejít na existující schválený [skript](../../apps/deploy-use/create-deploy-scripts.md) v Configuration Manager

> [!Important]  
> Pokud chcete tuto novou funkci Configuration Manager využít, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

#### <a name="parameters"></a>Parametry

Určuje parametry předané do skriptu PowerShellu. Tyto parametry jsou stejné jako parametry skriptu PowerShellu na příkazovém řádku.  

Zadejte parametry používané ve skriptu, ne pro příkazový řádek prostředí Windows PowerShell.  
Následující příklad obsahuje platné parametry:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

Následující příklad obsahuje neplatné parametry. První dvě položky jsou parametry příkazového řádku Windows PowerShellu (**-bez loga** a **-ExecutionPolicy bez omezení**). Skript tyto parametry nespotřebovává.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Pokud hodnota parametru obsahuje speciální znak, použijte kolem hodnoty jednoduché uvozovky ( `'` ). Použití dvojitých uvozovek ( `"` ) může způsobit, že krok pořadí úkolů nesprávně zpracuje parametr.

Příklad: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

Počínaje verzí 2002 nastavte tuto vlastnost na proměnnou.<!-- 5690481 --> Pokud například zadáte `%MyScriptVariable%` , když pořadí úkolů spustí skript, přidá hodnotu této vlastní proměnné do příkazového řádku PowerShellu.

#### <a name="powershell-execution-policy"></a>Zásady spouštění skriptu PowerShell

Určete, které skripty prostředí PowerShell (pokud nějaké máte) povolíte spuštění na počítači. Zvolte jednu z následujících zásad spouštění:  

- **AllSigned**: spouštějte jenom skripty podepsané důvěryhodným vydavatelem.  

- **Nedefinováno**: nedefinovat žádné zásady spouštění  

- **Bypass**: načte všechny konfigurační soubory a spustí všechny skripty. Pokud si stáhnete nepodepsaný skript z Internetu, Windows PowerShell před spuštěním skriptu nezobrazí výzvu k zadání oprávnění.  

> [!IMPORTANT]  
> PowerShell 1,0 nepodporuje zásady spouštění undefined a bypass.  

#### <a name="output-to-task-sequence-variable"></a>Výstup do proměnné pořadí úkolů

<!-- 3556028 -->
Počínaje verzí 1902 uložte výstup skriptu do vlastní proměnné pořadí úkolů.

> [!Note]  
> Počínaje verzí 1910 Configuration Manager tento výstup omezuje na posledních 1000 znaků.

Příklad použití této vlastnosti kroku naleznete v tématu [jak nastavit proměnné](using-task-sequence-variables.md#bkmk_run-ps).

#### <a name="start-in"></a>Spustit v:

<!-- 3556028 -->
Počínaje verzí 1902 zadejte spouštěcí složku pro skript, maximálně 127 znaků. Tato složka může představovat absolutní cestu k cílovému počítači nebo relativní cestu ke složce distribučního bodu obsahující balíček. Toto pole je volitelné.  

> [!NOTE]  
> Tlačítko **Procházet** prochází místní počítač se soubory a složkami. Cokoli, co vyberete, musí existovat také v cílovém počítači. Musí existovat ve stejném umístění a se stejnými názvy souborů a složek.  

#### <a name="time-out"></a>Časový limit

<!-- 3556028 -->
Počínaje verzí 1902 zadejte hodnotu, která představuje, jak dlouho Configuration Manager povolit spuštění skriptu prostředí PowerShell. Tato hodnota může být od 1 minuty do 999 minut. Výchozí hodnota je 15 minut. Tato možnost je ve výchozím nastavení zakázána.  

> [!IMPORTANT]  
> Pokud zadáte hodnotu, která nedovolí dostatek času na úspěšné dokončení zadaného skriptu, tento krok se nezdaří. V závislosti na podmínkách kroku nebo skupiny by mohlo dojít k selhání celého pořadí úkolů. Pokud časový limit vyprší, Configuration Manager ukončí proces PowerShellu.  

#### <a name="run-this-step-as-the-following-account"></a>Spustit tento krok jako následující účet

<!-- 3556028 -->
Počínaje verzí 1902 určete, že se skript prostředí PowerShell spouští jako jiný uživatelský účet systému Windows než účet místního systému.  

> [!NOTE]  
> Chcete-li spustit jednoduché skripty nebo příkazy s jiným účtem po instalaci operačního systému, přidejte nejprve účet do počítače. Kromě toho může být nutné obnovit uživatelské profily systému Windows, aby bylo možné provádět složitější akce.  

#### <a name="account"></a>Účet

<!-- 3556028 -->
Počínaje verzí 1902 zadejte uživatelský účet systému Windows, který tento krok používá ke spuštění skriptu prostředí PowerShell. Zadaný účet musí být místní správce v systému a skript se spustí s oprávněními tohoto účtu. Vyberte možnost **nastavit** a zadejte účet místního uživatele nebo domény. Další informace o účtu Spustit jako pro pořadí úloh najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Pokud tento krok Určuje uživatelský účet a spustí se v prostředí Windows PE, akce se nezdařila. K doméně se nedá připojit prostředí Windows PE. V souboru **souboru Smsts. log** se zaznamená toto selhání.  

### <a name="options-for-run-powershell-script"></a>Možnosti spuštění skriptu PowerShellu

Kromě výchozích možností nakonfigurujte na kartě **Možnosti** tohoto kroku pořadí úkolů následující další nastavení:  

#### <a name="success-codes"></a>Kódy úspěchu

<!-- 3556028 -->
Počínaje verzí 1902 zahrňte do skriptu další ukončovací kódy, které by měl krok vyhodnotit jako úspěšný.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> Spustit pořadí úloh

> [!Note]  
> Ve výchozím nastavení ve verzi 1910 Configuration Manager tuto funkci povolí. Verze 1906 nebo starší Configuration Manager ve výchozím nastavení tuto volitelnou funkci nepovoluje. Před použitím této funkce tuto funkci povolte. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).

Tento krok spustí jiné pořadí úkolů. Vytvoří vztah nadřazenosti-podřízenosti mezi pořadím úkolů. U podřízených sekvencí úloh můžete vytvořit více modulárních a opakovaně použitelných pořadí úloh.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **Spustit pořadí úloh**.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Specifikace a omezení pro pořadí úkolů spuštění

Při přidávání podřízeného pořadí úloh do pořadí úloh Vezměte v úvahu následující body:  

- Sekvence nadřazených a podřízených úloh jsou efektivně zkombinovány do jediné zásady, kterou klient spustí.  

- Prostředí je globální. Pokud nadřazené pořadí úkolů nastaví proměnnou a pak pořadí podřízených úkolů změní tuto proměnnou, zachová nejnovější hodnotu. Pokud podřízené pořadí úkolů vytvoří novou proměnnou, je k dispozici pro zbytek nadřazeného pořadí úkolů.  

- Stavové zprávy jsou posílány na normální pro jednu operaci pořadí úkolů.  

- Pořadí úkolů zapisuje položky do souboru **souboru Smsts. log** s novými položkami protokolu, které se při spuštění podřízeného pořadí úkolů vymažou.  

<!--the following points are from SCCMdocs issue #1079-->

- Nemůžete vybrat pořadí úloh s odkazem na spouštěcí bitovou kopii. Pro jakékoli nasazení, které vyžaduje spouštěcí bitovou kopii, ji určete v nadřazeném pořadí úkolů.  

- Pokud je podřízené pořadí úkolů zakázané, nasazení se nezdařilo. Pro řešení tohoto omezení nemůžete použít možnost **pokračovat při chybě** .  

- Pokud podřízené pořadí úkolů obsahuje kroky považované za *vysoký dopad*, Centrum softwaru je nedetekuje a zobrazuje oznámení s vysokým dopadem. Upravte vlastnosti nadřazeného pořadí úloh na kartě oznámení uživateli, abyste určili, že **se jedná o velmi působivé pořadí úkolů**.  

- Pokud v podřízeném pořadí úkolů chybí odkaz na balíček, zobrazení nadřazeného pořadí úkolů tento stav nerozpozná. Pokud upravíte nadřazené pořadí úkolů, zjistí všechny chybějící odkazy v podřízených pořadích úloh při provádění změn nadřazeného objektu.  

### <a name="cmdlets-for-run-task-sequence"></a>Rutiny pro pořadí úloh spuštění

Od verze 1906 spravujte tento krok pomocí následujících rutin PowerShellu:<!-- 2839943, SCCMDocs#1118 -->

- [Get-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/get-cmtsstepruntasksequence)
- [New-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/new-cmtsstepruntasksequence)
- [Remove-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/remove-cmtsstepruntasksequence)
- [Set-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/set-cmtsstepruntasksequence)

Další informace najdete v [poznámkách k verzi 1906 – nové rutiny](/powershell/sccm/1906-release-notes#new-cmdlets).

### <a name="properties-for-run-task-sequence"></a>Vlastnosti pořadí úloh spuštění

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="select-task-sequence-to-run"></a>Vyberte pořadí úloh, které se má spustit.

Vyberte **Procházet** a vyberte podřízené pořadí úkolů. V dialogovém okně **Vybrat pořadí úloh** se nezobrazí nadřazené pořadí úkolů.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Nastavit dynamické proměnné

Tento krok použijte k provedení následujících akcí:  

1. Shromažďování informací z počítače a jeho prostředí. Pak nastavte zadané proměnné pořadí úkolů s informacemi.  

2. Vyhodnotit definovaná pravidla Nastavte proměnné pořadí úkolů na základě pravidel, která se vyhodnotí jako true.  

Tento krok lze spustit v úplném operačním systému nebo prostředí Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **nastavit dynamické proměnné**.

### <a name="variables-for-set-dynamic-variables"></a>Proměnné pro nastavení dynamických proměnných

Pořadí úkolů automaticky nastaví následující proměnné pořadí úkolů jen pro čtení:  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Rutiny pro nastavení dynamických proměnných

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable)
- [New-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable)
- [Remove-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable)
- [Set-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable)

### <a name="properties-for-set-dynamic-variables"></a>Vlastnosti pro nastavení dynamických proměnných

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="dynamic-rules-and-variables"></a>Dynamická pravidla a proměnné

Chcete-li nastavit dynamickou proměnnou pro použití v pořadí úkolů, přidejte pravidlo. Pak nastavte hodnotu pro každou proměnnou zadanou v pravidle. Kromě toho přidejte jednu nebo více proměnných bez přidání pravidla. Když přidáte pravidlo, vyberte z následujících kategorií:  

- **Počítač**: vyhodnotí hodnoty pro štítek hardwarových prostředků, UUID, sériové číslo nebo adresu MAC. Podle potřeby nastavte více hodnot. Pokud je libovolná hodnota true, pravidlo se vyhodnotí jako true. Následující pravidlo se například vyhodnotí jako true, pokud je sériové číslo zařízení 5892087 a adresa MAC je 22-a4-5A-13-78-26:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Umístění**: vyhodnotit hodnoty pro výchozí síťovou bránu  

- **Značka a model**: vyhodnotit hodnoty pro model a model počítače. Aby se pravidlo vyhodnotilo jako true, musí se jako true vyhodnotit jak hodnota značky, tak hodnota modelu.

    Zadejte hvězdičku ( `*` ) a otazník ( `?` ) jako zástupné znaky zástupných karet. Hvězdička odpovídá více znakům a otazník odpovídá jednomu znaku. Například řetězec `DELL*900?` odpovídá `DELL-ABC-9001` a `DELL9009` .  

- **Proměnná pořadí úloh**: Přidání proměnné, podmínky a hodnoty pořadí úkolů k vyhodnocení. Pravidlo se vyhodnotí jako true, pokud sada hodnot pro proměnnou splňuje zadanou podmínku.  

    Zadejte jednu nebo více proměnných pro nastavení pravidla, které se vyhodnotí jako true, nebo nastavte proměnné bez použití pravidla. Vyberte existující proměnnou nebo vytvořte vlastní proměnnou.  

  - **Existující proměnné pořadí úkolů**: vyberte jednu nebo více proměnných ze seznamu existujících proměnných pořadí úkolů. Proměnné pole nejsou k dispozici pro výběr.  

  - **Vlastní proměnné pořadí úkolů**: Definujte vlastní proměnnou pořadí úkolů. Můžete taky určit existující proměnnou pořadí úkolů. Toto nastavení je užitečné při určení existujícího pole proměnných, jako je například **OSDAdapter**, protože pole proměnných nejsou v seznamu existujících proměnných pořadí úkolů.  

Po výběru proměnných pro pravidlo zadejte hodnotu pro každou proměnnou. Proměnná se nastaví na zadanou hodnotu, pokud se pravidlo vyhodnotí jako true. Pro každou proměnnou můžete vybrat možnost **Nezobrazovat tuto hodnotu** pro skrytí hodnoty proměnné. Ve výchozím nastavení některé existující proměnné skrývají hodnoty, jako je například proměnná **Proměnná OSDCaptureAccountPassword** .  

> [!IMPORTANT]  
> Když naimportujete pořadí úkolů s krokem **nastavit dynamické proměnné** , Configuration Manager odebere všechny hodnoty proměnných označené jako **Nezobrazovat tuto hodnotu**. Po importu pořadí úkolů znovu zadejte hodnotu pro dynamickou proměnnou.

Když použijete možnost **tuto hodnotu nezobrazovat**, hodnota proměnné se nezobrazí v editoru pořadí úloh. Soubor protokolu pořadí úkolů (**souboru Smsts. log**) nebo ladicí program sekvence úloh nezobrazuje hodnotu proměnné buď. Proměnnou lze v pořadí úkolů používat i v případě, že je spuštěna. Pokud již nechcete tyto proměnné skrývat, nejprve je odstraňte. Pak předefinujte proměnné bez výběru možnosti jejich skrytí.  

> [!WARNING]  
> Pokud zahrnete proměnné do příkazového řádku kroku **Spustit příkazový řádek** , zobrazí se v souboru protokolu pořadí úloh úplný příkazový řádek, včetně hodnot proměnných. Chcete-li zabránit tomu, aby se potenciálně citlivá data zobrazovala v souboru protokolu, nastavte proměnnou pořadí úloh **OSDDoNotLogCommand** na `TRUE` .


## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Nastavit proměnnou pořadí úloh

Pomocí tohoto kroku nastavíte hodnotu proměnné, která se používá s pořadím úkolů.  

Tento krok lze spustit v úplném operačním systému nebo prostředí Windows PE.

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **Obecné**a vyberte možnost **nastavit proměnnou pořadí úloh**.

### <a name="variables-for-set-task-sequence-variable"></a>Proměnné pro nastavení proměnné pořadí úloh

Proměnné pořadí úkolů se čtou akcemi pořadí úkolů a určují chování těchto akcí. Další informace o konkrétních proměnných pořadí úkolů a jejich použití naleznete v následujících článcích:  

- [Jak používat proměnné pořadí úkolů](using-task-sequence-variables.md)  
- [Proměnné pořadí úkolů](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Rutiny pro nastavení proměnné pořadí úkolů

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](/powershell/module/configurationmanager/get-cmtsstepsetvariable)
- [New-CMTSStepSetVariable](/powershell/module/configurationmanager/new-cmtsstepsetvariable)
- [Remove-CMTSStepSetVariable](/powershell/module/configurationmanager/remove-cmtsstepsetvariable)
- [Set-CMTSStepSetVariable](/powershell/module/configurationmanager/set-cmtsstepsetvariable)

### <a name="properties-for-set-task-sequence-variable"></a>Vlastnosti pro nastavení proměnné pořadí úkolů

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="task-sequence-variable"></a>Proměnné pořadí úloh

Zadejte název předdefinované nebo proměnné akce pořadí úkolů nebo zadejte vlastní název proměnné definované uživatelem.  

#### <a name="do-not-display-this-value"></a>Nezobrazovat tuto hodnotu

<!--1358330-->
Tuto možnost povolte, pokud chcete maskovat citlivá data uložená v proměnných pořadí úkolů. Například při zadávání hesla.

> [!NOTE]
> Tuto možnost povolte a pak nastavte hodnotu proměnné pořadí úkolů. V opačném případě se hodnota proměnné nenastaví podle vašich záměrů, což může způsobit neočekávané chování při spuštění pořadí úkolů.<!--SCCMdocs issue #800-->

Když použijete možnost **tuto hodnotu nezobrazovat**, hodnota proměnné se nezobrazí v editoru pořadí úloh. Soubor protokolu pořadí úkolů (**souboru Smsts. log**) nebo ladicí program sekvence úloh nezobrazuje hodnotu proměnné buď. Proměnnou lze v pořadí úkolů používat i v případě, že je spuštěna. Pokud už nechcete, aby tato proměnná byla skrytá, odstraňte ji jako první. Pak proměnnou znovu definujte bez výběru možnosti k jejímu skrytí.

> [!WARNING]
> Pokud zahrnete proměnné do příkazového řádku kroku **Spustit příkazový řádek** , zobrazí se v souboru protokolu pořadí úloh úplný příkazový řádek, včetně hodnot proměnných. Chcete-li zabránit tomu, aby se potenciálně citlivá data zobrazovala v souboru protokolu, nastavte proměnnou pořadí úloh **OSDDoNotLogCommand** na `TRUE` .<!-- 6963278 -->

#### <a name="value"></a>Hodnota  

Pořadí úkolů nastaví proměnnou na tuto hodnotu. Nastavte tuto proměnnou pořadí úloh na hodnotu jiné proměnné pořadí úkolů s syntaxí `%varname%` .  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Nastavit systém Windows a nástroj ConfigMgr

Pomocí tohoto kroku můžete provést přechod z prostředí Windows PE do nového operačního systému. Tento krok pořadí úkolů je požadovaná součást nasazení operačního systému. Nainstaluje klienta Configuration Manager do nového operačního systému a připraví pořadí úkolů pro pokračování v provádění v novém operačním systému.  

Tento krok zodpovídá za přechod pořadí úloh z Windows PE do úplného operačního systému. Tento krok v systému Windows PE a v plném operačním systému spouští z důvodu tohoto přechodu. Protože se ale přechod spustí v prostředí Windows PE, dá se přidat jenom během části pořadí úkolů v prostředí Windows PE.  

Tento krok nahrazuje soubor Sysprep. inf nebo unattend.xml proměnných adresáře, například `%WINDIR%` a `%ProgramFiles%` , v instalačním adresáři systému Windows PE `X:\Windows` . Pořadí úkolů ignoruje proměnné určené pomocí těchto proměnných prostředí.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové kopie**a vyberte možnost **nastavit systém Windows a nástroj ConfigMgr**.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Chování pro instalační systém Windows a nástroj ConfigMgr

Tento krok provádí následující akce:  

#### <a name="preliminaries-windows-pe"></a>Nezbytné úkony: prostředí Windows PE  

1. Nahraďte proměnné pořadí úkolů v souboru unattend.xml.  

2. Stáhněte balíček, který obsahuje klienta Configuration Manager. Přidejte balíček do nasazené bitové kopie.  

#### <a name="set-up-windows"></a>Instalace Windows  

- Instalace na základě bitové kopie  

    1. Zakáže klienta Configuration Manager v imagi, pokud existuje. Jinými slovy, zakažte autostart pro Configuration Manager klientskou službu.  

    2. Aktualizujte registr v nasazené bitové kopii tak, aby se spustil nasazený operační systém se stejným písmenem jednotky jako referenční počítač.  

    3. Restartujte počítač s nasazeným operačním systémem.  

    4. Zkrácená instalace Windows se spustí s dříve zadaným souborem Sysprep. inf nebo unattend.xml odpovědí, který má potlačenou veškerou interakci s koncovým uživatelem. Pokud použijete krok **použít nastavení sítě** pro připojení k doméně, pak jsou tyto informace v souboru odpovědí. Zkrácená instalace Windows připojí počítač k doméně.  

- Instalace ze souboru Setup.exe. Spustí soubor Setup.exe, který se drží typického procesu instalace systému Windows:  

    1. Zkopírujte balíček s upgradem operačního systému, který je zadaný v kroku **použít operační systém** , na jednotku pevného disku.  

    2. Restartujte nově nasazený operační systém.  

    3. Zkrácená instalace Windows se spustí s dříve zadaným souborem Sysprep. inf nebo unattend.xml odpovědí, který má potlačené veškeré nastavení uživatelského rozhraní. Pokud použijete krok  **použít nastavení sítě** pro připojení k doméně, pak jsou tyto informace v souboru odpovědí. Zkrácená instalace Windows připojí počítač k doméně.  

#### <a name="set-up-the-configuration-manager-client"></a>Nastavení klienta Configuration Manager  

1. Po dokončení zkrácené instalace systému Windows pořadí úkolů pokračuje s použitím souboru setupcomplete.cmd. Další informace najdete v tématu [spuštění skriptu po dokončení instalace (SetupComplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).  

2. Povolte nebo zakažte účet místního správce na základě možnosti vybrané v kroku **použít nastavení systému Windows** .  

3. Nainstalujte klienta Configuration Manager pomocí dříve staženého balíčku a vlastností instalace zadaných v tomto kroku. Klient se nainstaluje v režimu zřizování. Tento režim brání klientovi ve zpracování nových požadavků na zásady, dokud se pořadí úkolů nedokončí. Další informace najdete v tématu [režim zřizování](provisioning-mode.md).  

4. Počkejte, až bude klient plně funkční.  

#### <a name="the-step-completes"></a>Krok se dokončí.

Pořadí úkolů pokračuje v provádění dalšího kroku.  

> [!Note]  
> Zásady skupiny systému Windows obvykle nezpracovávají až po dokončení pořadí úloh. Toto chování je konzistentní v různých verzích Windows. Další vlastní akce v průběhu pořadí úkolů mohou aktivovat vyhodnocení zásad skupiny. Další informace o pořadí operací najdete v tématu [spuštění skriptu po dokončení instalace (SetupComplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd). <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Proměnné pro instalační systém Windows a nástroj ConfigMgr

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Rutiny pro instalační systém Windows a nástroj ConfigMgr

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr)
- [New-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr)
- [Set-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr)

### <a name="properties-for-setup-windows-and-configmgr"></a>Vlastnosti pro nastavení systému Windows a nástroje ConfigMgr

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="client-package"></a>Klientský balíček

Vyberte **Procházet**a pak vyberte instalační balíček klienta Configuration Manager, který chcete s tímto krokem použít.  

#### <a name="use-pre-production-client-package-when-available"></a>Použít předprodukční klientský balíček, pokud je dostupný

Pokud je k dispozici předprodukční klientský balíček a počítač je členem pilotní kolekce, pořadí úkolů použije tento balíček místo produkčního klientského balíčku. Předprodukční klient je novější verze pro testování v produkčním prostředí. Vyberte **Procházet**a vyberte instalační balíček předprodukčního klienta, který chcete s tímto krokem použít.  

#### <a name="installation-properties"></a>Vlastnosti instalace

Krok pořadí úkolů automaticky určuje přiřazení lokality a výchozí konfiguraci. Pomocí tohoto pole můžete určit jakékoli další vlastnosti instalace, které se mají použít při instalaci klienta. Pokud chcete zadat víc vlastností instalace, oddělte je mezerami.  

Zadejte parametry příkazového řádku, které se mají použít při instalaci klienta. Zadejte například, `/skipprereq: silverlight.exe` abyste informovali CCMSetup.exe, že nechcete instalovat požadované součásti Microsoft Silverlightu. Další informace o dostupných možnostech příkazového řádku pro CCMSetup.exe najdete v tématu [informace o vlastnostech instalace klienta](../../core/clients/deploy/about-client-installation-properties.md).  

Při spuštění pořadí úloh nasazení operačního systému v internetovém klientovi, který je připojen k Azure AD nebo používá ověřování založené na tokenech, je nutné zadat vlastnost [CCMHOSTNAME](../../core/clients/deploy/about-client-installation-properties.md#ccmhostname) v kroku **nastavit systém Windows a nástroj ConfigMgr** . Například, `CCMHOSTNAME=OTTERFALLS.CLOUDAPP.NET/CCM_Proxy_MutualAuth/12345678907927939`.

### <a name="options-for-setup-windows-and-configmgr"></a>Možnosti pro nastavení systému Windows a nástroje ConfigMgr

> [!NOTE]  
> Na kartě **Možnosti** nepovolujte možnost **pokračovat při chybě** . Pokud během tohoto kroku dojde k chybě, pořadí úkolů se nezdařilo, bez ohledu na to, jestli toto nastavení povolíte.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Upgradovat operační systém

Tento krok použijte k upgradu starší verze Windows na novější verzi Windows 10.  

Tento krok pořadí úkolů se spouští jenom v plném operačním systému. Neběží v systému Windows PE.  

Chcete-li přidat tento krok v editoru pořadí úloh, vyberte možnost **Přidat**, vyberte možnost **bitové kopie**a vyberte možnost **upgradovat operační systém**.

> [!TIP]
> Počínaje systémem Windows 10 verze 1709 obsahuje médium více edicí. Když nakonfigurujete pořadí úkolů tak, aby používalo balíček s upgradem operačního systému nebo bitovou kopii operačního systému, je nutné vybrat [podporovanou edici](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Pokud chcete stáhnout příslušný balíček s upgradem pro operační systém před tím, než uživatel nainstaluje pořadí úkolů, použijte předběžné ukládání obsahu do mezipaměti. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../deploy-use/configure-precache-content.md).

### <a name="variables-for-upgrade-os"></a>Proměnné pro upgrade operačního systému

V tomto kroku použijte následující proměnné pořadí úkolů:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>Rutiny pro upgrade operačního systému

Tento krok spravujte pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem)
- [New-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem)
- [Remove-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem)
- [Set-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem)

### <a name="properties-for-upgrade-os"></a>Vlastnosti pro upgrade operačního systému

Na kartě **vlastnosti** tohoto kroku nakonfigurujte nastavení popsaná v této části.  

#### <a name="upgrade-package"></a>Upgradovat balíček

Tuto možnost vyberte, pokud chcete zadat balíček s upgradem operačního systému Windows 10, který se má pro upgrade použít.  

#### <a name="source-path"></a>Zdrojová cesta

Určuje místní nebo síťovou cestu k médiu Windows 10, které instalační program systému Windows používá. Toto nastavení odpovídá možnosti příkazového řádku instalační program systému Windows `/InstallFrom` .

Můžete také zadat proměnnou, například `%MyContentPath%` nebo `%DPC01%` . Pokud pro zdrojovou cestu použijete proměnnou, nastavte její hodnotu dříve v pořadí úkolů. Můžete například použít krok [Stáhnout obsah balíčku](#BKMK_DownloadPackageContent) a zadat proměnnou pro umístění balíčku upgradu operačního systému. Pak použijte tuto proměnnou pro zdrojovou cestu pro tento krok.  

#### <a name="edition"></a>Edice

Zadejte edici v médiu s operačním systémem, která se má pro upgrade použít.  

#### <a name="product-key"></a>Kód Product Key

Zadejte kód Product Key, který se má použít pro proces upgradu.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Při upgradu zadejte do instalačního programu systému Windows následující obsah ovladače

Během procesu upgradu přidejte do cílového počítače ovladače. Ovladače musí být kompatibilní s Windows 10. Toto nastavení odpovídá možnosti příkazového řádku instalační program systému Windows `/InstallDriver` . Další informace najdete v tématu [instalační program systému Windows možnosti příkazového řádku](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers).

Zadejte jednu z následujících možností:  

- **Balíček ovladače**: vyberte **Procházet** a vyberte ze seznamu existující balíček ovladačů.

- **Připravený obsah**: tuto možnost vyberte, pokud chcete zadat umístění obsahu ovladače. Můžete určit místní složku, síťovou cestu nebo proměnnou pořadí úkolů. Pokud pro zdrojovou cestu použijete proměnnou, nastavte její hodnotu dříve v pořadí úkolů. Například pomocí kroku [Stáhnout obsah balíčku](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

> [!TIP]
> Pokud chcete mít dynamický obsah pro více typů hardwaru:
>
> - Použijte více instancí tohoto kroku s podmínkami pro typy hardwaru a samostatný obsah ovladače.
>
> - Použijte více instancí kroku [Stáhnout obsah balíčku](task-sequence-steps.md#BKMK_DownloadPackageContent) . Umístěte obsah do společného umístění a pak použijte možnost **připraveného obsahu** . Výhodou této metody je, že pořadí úloh má jeden krok **upgradu operačního systému** .

#### <a name="time-out-minutes"></a>Časový limit (minuty)

Zadejte počet minut, po kterém Configuration Manager tento krok neprojde. Tato možnost je užitečná, když instalační program systému Windows zastaví zpracování, ale neukončí se.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Provést kontrolu kompatibility instalačního programu systému Windows bez spuštění upgradu

Proveďte kontrolu kompatibility instalační program systému Windows bez spuštění procesu upgradu. Toto nastavení odpovídá možnosti příkazového řádku instalační program systému Windows `/Compat ScanOnly` . Pomocí této možnosti nasaďte celý balíček s upgradem operačního systému.

<!--SCCMDocs-pr issue 2812-->
Když tuto možnost povolíte, tento krok nepřepne klienta Configuration Manager do režimu zřizování. Instalační program systému Windows běží tiše na pozadí a klient bude i nadále fungovat jako normální. Další informace najdete v tématu [režim zřizování](provisioning-mode.md).

Instalační program vrátí jako výsledek kontroly ukončovací kód. Následující tabulka uvádí některé z nejběžnějších ukončovacích kódů:  

|Ukončovací kód|Podrobnosti|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Žádné problémy s kompatibilitou („úspěch“).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problémy s kompatibilitou.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Vybraná volba migrace není dostupná. Může jít třeba o upgrade z edice Enterprise na edici Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Pro systém Windows 10 se nedá použít.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Není dostatek volného místa na disku.|  

Další informace o tomto parametru najdete v tématu [instalační program systému Windows možnosti příkazového řádku](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignorovat všechny zprávy o kompatibilitě, které jde přeskočit

Určuje, že instalační program dokončí instalaci a ignoruje všechny zprávy o kompatibilitě přeskočit. Toto nastavení odpovídá možnosti příkazového řádku instalační program systému Windows `/Compat IgnoreWarning` .  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Dynamicky aktualizovat instalační program Windows přes Windows Update

Povolit instalačnímu programu provádět dynamické operace aktualizace, jako je hledání, stahování a instalace aktualizací. Toto nastavení odpovídá možnosti příkazového řádku instalační program systému Windows `/DynamicUpdate` . Toto nastavení není kompatibilní s Configuration Managermi aktualizacemi softwaru. Tuto možnost povolte, když spravujete aktualizace se samostatnými Windows Server Update Services (WSUS) nebo web Windows Update pro firmy.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Přepsat zásady a použít výchozí Microsoft Update

Dočasné přepsání místních zásad v reálném čase, aby se spouštěly operace dynamické aktualizace. Počítač získá aktualizace z web Windows Update.
