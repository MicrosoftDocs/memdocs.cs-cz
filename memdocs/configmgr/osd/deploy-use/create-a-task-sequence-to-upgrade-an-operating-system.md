---
title: Vytvoření pořadí úkolů při upgradu operačního systému
titleSuffix: Configuration Manager
description: Použití pořadí úkolů k automatickému upgradu ze systému Windows 7 nebo novějšího na Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ad36978f3f3dc5207068a65d76bf8f5c7c3078c
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383236"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Vytvoření pořadí úkolů pro upgrade operačního systému v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí pořadí úkolů v Configuration Manager automaticky upgradovat operační systém v cílovém počítači. Tento upgrade může být z Windows 7 nebo novějšího na Windows 10 nebo z Windows Serveru 2012 nebo novějšího na Windows Server 2016. Vytvořte pořadí úkolů, které odkazuje na balíček s upgradem operačního systému a jakýkoli další obsah, který se má nainstalovat, například aplikace nebo aktualizace softwaru. Pořadí úkolů pro upgrade operačního systému je součástí scénáře [upgradu na nejnovější verzi](upgrade-windows-to-the-latest-version.md) .  


## <a name="prerequisites"></a>Požadavky

Před vytvořením pořadí úkolů je nutné, aby byly provedeny následující požadavky:

### <a name="required"></a>Vyžadováno

- [Balíček s upgradem operačního systému](../get-started/manage-operating-system-upgrade-packages.md) musí být dostupný v konzole Configuration Manager.  

- Při upgradu na systém Windows Server 2016 vyberte nastavení **ignorovat zprávy o kompatibilitě** v kroku pořadí úkolů upgradovat operační systém. V opačném případě se upgrade nezdařil.  

### <a name="required-if-used"></a>Požaduje se (pokud se používá)  

- [Aktualizace softwaru](../../sum/get-started/synchronize-software-updates.md) musí být synchronizované v konzole Configuration Manager.  

- [Aplikace](../../apps/deploy-use/create-applications.md) musí být přidány do konzoly Configuration Manager.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a>Vytvoření pořadí úkolů pro upgrade operačního systému  

Chcete-li upgradovat operační systém na klientských počítačích, vytvořte pořadí úkolů a v Průvodci vytvořením pořadí úloh vyberte možnost **upgradovat operační systém z balíčku pro upgrade** . Průvodce přidá kroky pořadí úkolů pro upgrade operačního systému, použití aktualizací softwaru a instalaci aplikací.

1. V konzole Configuration Manager klikněte na pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a pak vyberte **pořadí úloh**.  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pořadí úloh**.  

3. Na stránce **vytvořit novou sekvenci úloh** v Průvodci vytvořením pořadí úloh vyberte možnost **upgradovat operační systém z balíčku pro upgrade**a pak vyberte možnost **Další**.  

4. Na stránce **informace o pořadí úloh** zadejte následující nastavení:  

    - **Název pořadí úkolů**: Zadejte název, který identifikuje pořadí úkolů.  

    - **Popis**: Volitelně zadejte popis.  

5. Na stránce **upgrade operačního systému Windows** zadejte následující nastavení:  

    - **Balíček s upgradem**: Zadejte balíček pro upgrade, který obsahuje zdrojové soubory upgradu operačního systému. Ověřte, že jste vybrali správný balíček pro upgrade, a Prohlédněte si informace v podokně **vlastnosti** . Další informace najdete v tématu [Správa balíčků s upgradem operačního systému](../get-started/manage-operating-system-upgrade-packages.md).  

    - **Index edice**: Pokud je v balíčku k dispozici více indexů OS Edition, vyberte požadovaný index edice. Ve výchozím nastavení Průvodce vybere první index.  

    - **Kód Product Key**: zadejte kód Product Key systému Windows pro operační systém, který chcete nainstalovat. Zadejte kódované klíče multilicencí nebo standardní kódy Product Key. Použijete-li standardní kód Product Key, oddělte každou skupinu pěti znaky pomlčkou ( `-` ). Příklad: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Pokud je upgrade pro multilicenční edici, nemusí se kód Product Key vyžadovat.  

        > [!Note]  
        > Tento kód Product Key může být klíč k vícenásobné aktivaci (MAK) nebo obecný multilicenční klíč (GVLK). GVLK se také označuje jako klíč pro nastavení klienta služby správy klíčů (KMS). Další informace najdete v tématu [plánování aktivace multilicence](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Seznam klíčů pro instalaci klienta služby správy klíčů najdete v [příloze a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) v příručce k aktivaci Windows serveru.

    - **Ignorovat všechny zprávy o kompatibilitě**: Toto nastavení vyberte, pokud provádíte upgrade na systém Windows Server 2016. Pokud toto nastavení nevyberete, pořadí úkolů se neúspěšně dokončí, protože instalační program systému Windows čeká, až uživatel v dialogovém okně kompatibility aplikací pro Windows vybere možnost **Potvrdit** .  

6. Na stránce **Zahrnout aktualizace** určete, zda se mají nainstalovat požadované, všechny nebo žádné aktualizace softwaru. Pak vyberte **Další**. Pokud určíte, že se mají instalovat aktualizace softwaru, Configuration Manager nainstaluje jenom ty aktualizace, které jsou cílené na kolekce, kterých je cílový počítač členem.  

7. Na stránce **instalovat aplikace** určete aplikace, které chcete do cílového počítače nainstalovat, a pak vyberte **Další**. Pokud vyberete více než jednu aplikaci, určete také, zda má pořadí úkolů pokračovat, pokud se instalace určité aplikace nepovede.  

8. Dokončete průvodce.  

> [!Important]  
> Když je pořadí úloh spuštěno na zařízení, klient Configuration Manager vytvoří několik skriptů pro řízení chování pořadí úkolů v různých scénářích. Po dokončení pořadí úkolů klient tyto skripty neodebere, dokud se počítač nerestartuje. Tyto soubory skriptu neobsahují citlivé informace.  

Výchozí šablona pořadí úkolů pro místní upgrade systému Windows 10 zahrnuje další skupiny s doporučenými akcemi, které je třeba přidat před a po procesu upgradu. Tyto akce jsou společné mezi mnoha zákazníky, kteří úspěšně upgradují zařízení na Windows 10. Další informace najdete v tématu Doporučené kroky pořadí úloh pro [přípravu na upgrade](#recommended-task-sequence-steps-to-prepare-for-upgrade) a [pro následné zpracování](#recommended-task-sequence-steps-for-post-processing).

Počínaje verzí 1806 Tato šablona pořadí úkolů zahrnuje také skupinu s doporučenými akcemi, které se mají přidat pro případ, že proces upgradu neproběhne úspěšně. Tyto akce usnadňují řešení potíží. Další informace najdete v tématu [Doporučené kroky pořadí úkolů při selhání](#recommended-task-sequence-steps-on-failure).<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Konfigurace obsahu předběžné mezipaměti

<!--1021244-->
Funkce pre-cache pro dostupná nasazení pořadí úkolů umožňuje klientům stáhnout relevantní obsah balíčku upgradu operačního systému před tím, než uživatel nainstaluje pořadí úkolů.  

Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Doporučené kroky pořadí úloh k přípravě na upgrade

Výchozí šablona pořadí úkolů pro místní upgrade Windows 10 zahrnuje další skupiny s doporučenými akcemi, které se mají přidat před proces upgradu. Tyto akce ve skupině **Příprava pro upgrade** jsou společné mezi mnoha zákazníky, kteří úspěšně upgradují zařízení na Windows 10. Máte-li existující pořadí úloh, které již tyto akce nemá, přidejte je do pořadí úkolů ručně ve skupině **Příprava pro upgrade** .  

### <a name="battery-checks"></a>Kontroly baterie

Do této skupiny přidejte kroky, pokud chcete ověřit, jestli počítač používá baterii, nebo kabelové napájení. Tato akce vyžaduje provedení této kontroly pomocí vlastního skriptu nebo nástroje.

#### <a name="battery-check-example"></a>Příklad kontroly baterie

Použijte program WbemTest a připojte se k `root\cimv2` oboru názvů. Pak spusťte následující dotaz:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Pokud vrátí všechny výsledky, zařízení se spustí na baterii. V opačném případě je zařízení připojené k kabelovému napájení.  

### <a name="networkwired-connection-checks"></a>Kontroly připojení k síti nebo kabelové připojení

Do této skupiny přidejte kroky, pokud chcete ověřit, jestli je počítač připojený k síti a nepoužívá bezdrátové připojení. Tato akce vyžaduje provedení této kontroly pomocí vlastního skriptu nebo nástroje.

#### <a name="network-check-example"></a>Příklad kontroly sítě

Použijte program WbemTest a připojte se k `root\cimv2` oboru názvů. Pak spusťte následující dotaz:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Pokud vrátí všechny výsledky, zařízení běží na Wi-Fi. V opačném případě je zařízení připojené k kabelovému připojení k síti.

### <a name="remove-incompatible-applications"></a>Odebrání nekompatibilních aplikací

Do této skupiny přidejte kroky, pokud chcete odebrat všechny aplikace, které nejsou kompatibilní s touto verzí Windows 10. Způsob odinstalace aplikace se liší.  

Pokud aplikace používá Instalační služba systému Windows, zkopírujte příkazový řádek **odinstalačního programu** na kartě **programy** v části vlastnosti typu nasazení Instalační služba systému Windows aplikace. Pak v této skupině přidejte krok **Spustit příkazový** řádek pomocí příkazového řádku Uninstall program. Například:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Odebrat nekompatibilní ovladače

Do této skupiny přidejte kroky, pokud chcete odebrat všechny ovladače, které nejsou kompatibilní s touto verzí Windows 10.  

### <a name="removesuspend-third-party-security"></a>Odebrání nebo pozastavení zabezpečení třetích stran

Do této skupiny přidejte kroky, pokud chcete odebrat nebo pozastavit zabezpečovací programy třetích stran, jako je třeba antivirová ochrana.  

Pokud používáte program pro šifrování disků od jiného výrobce, poskytněte jeho ovladač šifrování pro instalační program systému Windows s `/ReflectDrivers` [možností příkazového řádku](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Přidejte krok [nastavit proměnnou pořadí úloh](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) do pořadí úkolů v této skupině. Nastavte proměnnou pořadí úloh na **OSDSetupAdditionalUpgradeOptions**. Nastavte hodnotu na `/ReflectDrivers` cestu k ovladači. Tato [proměnná pořadí úloh](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) připojuje instalační program systému Windows příkazového řádku, který používá pořadí úkolů. Další pokyny k tomuto procesu získáte od dodavatele softwaru.  

### <a name="download-package-content-task-sequence-step"></a>Krok pořadí úkolů stáhnout obsah balíčku  

Použijte krok [Stáhnout obsah balíčku](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) před krok **upgrade operačního systému** v následujících scénářích:  

- Pro platformy x86 i x64 používáte jedno pořadí úkolů upgradu. Do skupiny **Příprava pro upgrade** přidejte dva kroky **Stáhnout obsah balíčku** . Nastavte podmínky pro jednotlivé kroky ke zjištění architektury klienta. Tento stav způsobí, že krok stáhne pouze příslušný balíček upgradu operačního systému. Nakonfigurujte všechny kroky **Stáhnout obsah balíčku** tak, aby používaly stejnou proměnnou, a proměnnou pro cestu k médiu použijte v kroku **Upgrade operačního systému**.  

- Pokud chcete dynamicky stáhnout příslušný balíček ovladačů, použijte dva kroky **Stáhnout obsah balíčku** s podmínkami, které zjišťují odpovídající typ hardwaru pro každý balíček ovladače. Nakonfigurujte všechny kroky **Stáhnout obsah balíčku** tak, aby používaly stejnou proměnnou. Pak použijte tuto proměnnou pro hodnotu **připraveného obsahu** v části ovladače v kroku **upgrade operačního systému** .  

    > [!NOTE]  
    > Configuration Manager přidá k názvu proměnné číselnou příponu. Pokud například zadáte `%mycontent%` jako vlastní proměnnou, klient uloží do tohoto umístění veškerý odkazovaný obsah. Pokud v následujícím kroku odkazujete na proměnnou, jako je například **upgrade operačního systému**, použijte proměnnou s číselnou příponou. V tomto příkladu `%mycontent01%` nebo `%mycontent02%` , kde číslo odpovídá pořadí, ve kterém krok **Stáhnout obsah balíčku** uvádí tento konkrétní obsah.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Doporučené kroky pořadí úloh pro následné zpracování

Po vytvoření pořadí úloh přidejte další kroky do skupiny **po zpracování** pořadí úkolů.  

> [!NOTE]  
> Toto pořadí úkolů není lineární. Existují podmínky pro kroky, které mohou ovlivnit výsledky pořadí úkolů. Toto chování závisí na tom, jestli úspěšně Upgradoval klientský počítač, nebo jestli má vrátit zpátky klientský počítač do původního operačního systému.  

Výchozí šablona pořadí úkolů pro místní upgrade systému Windows 10 zahrnuje další skupiny s doporučenými akcemi, které se mají přidat po dokončení procesu upgradu. Tyto akce ve skupině **po zpracování** jsou společné mezi mnoha zákazníky, kteří úspěšně upgradují zařízení na Windows 10. Máte-li existující sekvenci úloh, která ještě tyto akce nemá, přidejte je do pořadí úkolů ručně ve skupině **po zpracování** .  

### <a name="apply-setup-based-drivers"></a>Použít ovladače založené na nastavení

Do této skupiny přidejte kroky, pokud chcete nainstalovat ovladače založené na instalaci (. exe) z balíčků.  

### <a name="installenable-third-party-security"></a>Instalace nebo povolení zabezpečení třetích stran

Do této skupiny přidejte kroky, pokud chcete nainstalovat nebo povolit zabezpečovací programy třetích stran, jako je třeba antivirová ochrana.  

### <a name="set-windows-default-apps-and-associations"></a>Nastavení výchozích aplikací a přidružení pro Windows

Do této skupiny přidejte kroky, pokud chcete nastavit výchozí aplikace Windows a přidružení souborů.

1. Připravte referenční počítač s požadovanými přidruženími aplikace.
1. K exportu spusťte následující příkazový řádek:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Přidejte soubor XML do balíčku.
1. Přidejte krok [Spustit příkazový řádek](../understand/task-sequence-steps.md#BKMK_RunCommandLine) v této skupině. Zadejte balíček, který obsahuje soubor XML, a pak zadejte následující příkazový řádek:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Další informace najdete v tématu [Export nebo import výchozích přidružení aplikace](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).

### <a name="apply-customizations-and-personalization"></a>Použití přizpůsobení a přizpůsobení

Do této skupiny přidejte kroky, pokud chcete použít přizpůsobení nabídky Start, jako je například organizace skupin programů. Další informace najdete v tématu [přizpůsobení úvodní obrazovky](/windows-hardware/manufacture/desktop/customize-the-start-screen).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Volitelné kroky pořadí úloh pro vrácení zpět  

Když se po restartování počítače dojde k nějaké chybě v procesu upgradu, instalační program systému Windows vrátí systém do předchozího operačního systému. Pořadí úkolů pak pokračuje všemi kroky ve skupině **vrácení** . Po vytvoření pořadí úloh přidejte v této skupině volitelné kroky podle potřeby. Můžete například vrátit všechny změny provedené v systému ve skupině příprava pro upgrade, například odinstalování nekompatibilního softwaru.


## <a name="recommended-task-sequence-steps-on-failure"></a>Doporučené kroky pořadí úkolů při selhání

<!--1358500-->
Počínaje verzí 1806 je výchozí šablona pořadí úkolů pro místní upgrade Windows 10 skupina, která **spouští akce při selhání**. Tato skupina zahrnuje doporučené akce, které je potřeba přidat pro případ, že proces upgradu neproběhne úspěšně. Tyto akce usnadňují řešení potíží.

### <a name="collect-logs"></a>Shromažďování protokolů

Chcete-li shromáždit protokoly z klienta, přidejte do této skupiny kroky.  

- Běžný postup je zkopírovat soubory protokolu do sdílené síťové složky. Chcete-li vytvořit toto připojení, použijte krok [připojit k síťové složce](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .  

- K provedení operace kopírování použijte vlastní skript nebo nástroj buď pomocí [příkazového řádku spustit](../understand/task-sequence-steps.md#BKMK_RunCommandLine) , nebo kroku [Spustit skript prostředí PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) .  

- Soubory, které se mají shromažďovat, můžou zahrnovat tyto protokoly:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Další informace o setupaccích. log a dalších protokolech instalační program systému Windows najdete v tématu [instalační program systému Windows soubory protokolu](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

- Další informace o Configuration Manager klientských protokolech najdete v tématu [Configuration Manager protokolech klienta](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).  

- Další informace o **_SMSTSLogPath** a dalších užitečných proměnných najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md).  

### <a name="run-diagnostic-tools"></a>Spustit diagnostické nástroje

Chcete-li spustit další diagnostické nástroje, přidejte do této skupiny kroky. Automatizujte tyto nástroje pro shromažďování dalších informací ze systému hned po selhání.  

Jedním z těchto nástrojů je Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). K získání podrobných informací o tom, proč upgrade Windows 10 neproběhl úspěšně, se jedná o samostatný diagnostický nástroj.  

- V Configuration Manager [vytvořte balíček](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) pro nástroj.  

- Přidejte krok [Spustit příkazový řádek](../understand/task-sequence-steps.md#BKMK_RunCommandLine) do této skupiny pořadí úkolů. K odkazování na nástroj použijte možnost **balíček** . Následující řetězec je příkladem **příkazového řádku**:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> Pro nejnovější funkce a opravy známých problémů vždy používejte nejnovější verzi SetupDiag. Další informace najdete v tématu [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag).

## <a name="additional-recommendations"></a>Další doporučení

### <a name="windows-documentation"></a>Dokumentace k Windows

Přečtěte si dokumentaci k Windows a [vyřešte chyby upgradu Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Tento článek obsahuje taky podrobné informace o procesu upgradu.  

### <a name="check-minimum-disk-space"></a>Kontrolovat minimální místo na disku

V kroku výchozí **Kontrola připravenosti zkontrolujte** , že **zajistěte minimální volné místo na disku (MB)**. Nastavte hodnotu na minimálně **16384** (16 GB) pro 32 balíček s UPGRADEM operačního systému nebo **20480** (20 GB) pro 64 bitů.  

### <a name="retry-downloading-policy"></a>Zkusit znovu stáhnout zásady

Pro opakované stažení zásad použijte [proměnnou pořadí úloh](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount** . Ve výchozím nastavení se klient opakuje dvakrát; Tato proměnná je nastavená na dvě (2). Pokud klienti nejsou připojeni k kabelové síti intranet, pomohou vám další pokusy o získání zásad klienta. Pokud se tato proměnná nedá stáhnout, nejedná se o negativní vedlejší účinek, jiné než opožděné selhání.<!--501016--> Také navýšit proměnnou **SMSTSDownloadRetryDelay** z výchozí hodnoty 15 sekund.  

### <a name="perform-an-inline-compatibility-assessment"></a>Provedení vloženého posouzení kompatibility

1. Přidejte druhý krok **upgrade operačního systému** na úvodní fázi ve skupině **Příprava pro upgrade** .  

    1. Pojmenujte si *posouzení upgradu*.
    1. Zadejte stejný balíček pro upgrade a pak povolte možnost **provádět kontrolu kompatibility instalační program systému Windows bez spuštění upgradu**.
    1. Povolte možnost **pokračovat při chybě** na kartě Možnosti.  

1. Hned za tento krok *posouzení upgradu* přidejte krok **příkazového řádku pro spuštění** . Zadejte následující příkazový řádek:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. Na kartě **Možnosti** přidejte následující podmínku:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

Tento návratový kód je desítkovým ekvivalentem MOSETUP_E_COMPAT_SCANONLY (0xC1900210), což je úspěšná kontrola kompatibility bez problémů. Pokud krok *posouzení upgradu* uspěje a vrátí tento kód, pořadí úkolů tento krok přeskočí. V opačném případě, pokud krok vyhodnocení vrátí jiný návratový kód, tento krok pořadí úkolů neprojde návratovým kódem z kontroly kompatibility instalační program systému Windows. Další informace o **_SMSTSOSUpgradeActionReturnCode**najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

Další informace najdete v tématu [upgrade operačního systému](../understand/task-sequence-steps.md#BKMK_UpgradeOS).  

### <a name="convert-from-bios-to-uefi"></a>Převod ze systému BIOS na rozhraní UEFI

Pokud chcete změnit zařízení ze systému BIOS na rozhraní UEFI během tohoto pořadí úloh, přečtěte si téma [převod ze systému BIOS na rozhraní UEFI během místního upgradu](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).  

### <a name="manage-bitlocker"></a>Správa nástroje BitLocker

<!--SCCMDocs issue #494-->
Pokud používáte šifrování disku BitLockerem, instalační program systému Windows ho ve výchozím nastavení automaticky pozastavit během upgradu. Počínaje verzí 1803 Windows 10 instalační program systému Windows zahrnuje `/BitLocker` parametr příkazového řádku pro řízení tohoto chování. Pokud požadavky na zabezpečení vyžadují, aby bylo šifrování aktivních disků vždy aktivní, použijte k zahrnutí **OSDSetupAdditionalUpgradeOptions** [proměnnou pořadí úloh](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) OSDSetupAdditionalUpgradeOptions ve skupině **Příprava pro upgrade** `/BitLocker TryKeepActive` . Další informace najdete v tématu [instalační program systému Windows možnosti příkazového řádku](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Odebrat výchozí aplikace

<!--SCCMDocs issue #526-->
Někteří zákazníci odstraňují ve Windows 10 výchozí zřízené aplikace. Například aplikace pro počasí v programu Bing nebo kolekce Microsoft Solitaire. V některých situacích tyto aplikace po aktualizaci Windows 10 vrátí. Další informace najdete v tématu [Jak zachovat aplikace odebrané ze systému Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

Přidejte krok **Spustit příkazový řádek** do pořadí úkolů ve skupině **Příprava pro upgrade** . Zadejte příkazový řádek podobný následujícímu příkladu:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
