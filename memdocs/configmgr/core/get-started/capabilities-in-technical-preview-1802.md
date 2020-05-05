---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1802 pro Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 50e05d07ec3e2612c170157c45f5e64abe3766de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718606"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1802 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1802. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. 

Před instalací této verze Technical Preview si přečtěte [Technical Preview for Configuration Manager](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Známé problémy v této verzi Technical Preview
- **Aktualizace na novou verzi Preview se nezdařila, pokud máte server lokality v pasivním režimu**. Pokud máte [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné před aktualizací na tuto novou verzi Preview odinstalovat server lokality pasivního režimu. Server lokality v pasivním režimu můžete po dokončení aktualizace znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **Konfigurace** > **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
  2. V podokně **role systému lokality** klikněte pravým tlačítkem na roli **serveru lokality** a pak zvolte **Odebrat roli**.
  3. Klikněte pravým tlačítkem na server lokality pasivního režimu a zvolte **Odstranit**.
  4. Po odinstalaci serveru lokality na aktivním serveru primární lokality restartujte službu **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


</br>

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Přechod úloh Endpoint Protection do Intune pomocí spolusprávy    
<!-- 1357365 -->
V této verzi teď můžete po povolení spolusprávy převést úlohu Endpoint Protection z Configuration Manager na Intune. Chcete-li převést úlohu Endpoint Protection, přejděte na stránku vlastností spolusprávy a přesuňte posuvník z Configuration Manager na **pilot** nebo **vše**. Podrobnosti najdete v tématu [společná správa pro zařízení s Windows 10](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Konfigurace optimalizace doručování Windows pro použití Configuration Manager skupin hranic
<!-- 1324696 -->
Skupiny hranic Configuration Manager slouží k definování a regulaci distribuce obsahu napříč podnikovou sítí a vzdálenými pobočkami. [Optimalizace doručení Windows](/windows/deployment/update/waas-delivery-optimization) je cloudová technologie peer-to-peer pro sdílení obsahu mezi zařízeními s Windows 10. Od této verze můžete nakonfigurovat optimalizaci doručování, aby při sdílení obsahu mezi partnerskými uzly používala vaše skupiny hranic. Nové nastavení klienta použije identifikátor skupiny hranic jako identifikátor skupiny Optimalizace doručení na klientovi. Když klient komunikuje s cloudovou službou Optimalizace doručení, používá tento identifikátor k vyhledání partnerských uzlů s požadovaným obsahem. 

### <a name="prerequisites"></a>Požadavky
- Optimalizace doručení je dostupná jenom na klientech s Windows 10.

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. V konzole Configuration Manager v části pracovní prostor **Správa** , uzel **nastavení klienta** vytvořte vlastní zásadu nastavení klientského zařízení.
2. Vyberte novou skupinu **Optimalizace doručení** .
3. Povolte nastavení **použít Configuration Manager skupiny hranic pro ID skupiny Optimalizace doručení**.

Další informace najdete v možnosti režim doručení **skupiny** v tématu [Možnosti optimalizace doručení](/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Pořadí úkolů místního upgradu Windows 10 přes bránu pro správu cloudu
<!-- 1357149 -->

[Pořadí úkolů místního upgradu](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) Windows 10 teď podporuje nasazení do internetových klientů spravovaných prostřednictvím [brány pro správu cloudu](../clients/manage/cmg/plan-cloud-management-gateway.md). Tato možnost umožňuje vzdáleným uživatelům snadněji upgradovat na Windows 10, aniž by se museli připojit k podnikové síti. 

Zajistěte, aby veškerý obsah odkazovaný pořadím úkolů místního upgradu byl distribuován do [distribučního bodu cloudu](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Jinak zařízení nemůžou pořadí úkolů Spustit.

Když nasadíte pořadí úkolů upgradu, použijte následující nastavení:
- **Povolí spuštění pořadí úkolů pro klienta na internetu**na kartě činnost koncového uživatele v nasazení.
- **Před spuštěním pořadí úloh stáhnout veškerý obsah místně**, na kartě distribuční body v nasazení. Další možnosti, jako je například **Stažení obsahu místně, pokud to vyžaduje běžící pořadí úloh** , v tomto scénáři nefungují. Modul pořadí úloh v současné době nemůže získat obsah z distribučního bodu cloudu. Klient Configuration Manager musí před spuštěním pořadí úloh stáhnout obsah z distribučního bodu cloudu.
- (*Volitelné*) **Předem stáhnout obsah pro toto pořadí úloh**na kartě Obecné v nasazení. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Vylepšení pořadí úkolů místního upgradu Windows 10
<!-- 1357425 -->
Výchozí šablona pořadí úkolů pro místní upgrade systému Windows 10 nyní zahrnuje další skupiny s doporučenými akcemi pro přidání před a po dokončení procesu upgradu. Tyto akce jsou společné mezi mnoha zákazníky, kteří úspěšně upgradují zařízení na Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Nové skupiny v rámci **Příprava na upgrade**
- **Kontroly baterie**: do této skupiny přidejte kroky, pokud chcete zkontrolovat, jestli počítač používá baterii, nebo kabelové napájení. Tato akce vyžaduje provedení této kontroly pomocí vlastního skriptu nebo nástroje.
- **Kontroly připojení k síti nebo kabelové připojení**: do této skupiny přidejte kroky, pokud chcete zkontrolovat, jestli je počítač připojený k síti a nepoužívá bezdrátové připojení. Tato akce vyžaduje provedení této kontroly pomocí vlastního skriptu nebo nástroje.
- **Odebrat nekompatibilní aplikace**: do této skupiny přidejte kroky, pokud chcete odebrat všechny aplikace, které nejsou kompatibilní s touto verzí Windows 10. Způsob odinstalace aplikace se liší. Pokud aplikace používá Instalační služba systému Windows, zkopírujte příkazový řádek **odinstalačního programu** na kartě **programy** v části vlastnosti typu nasazení Instalační služba systému Windows aplikace. Pak v této skupině přidejte krok **Spustit příkazový** řádek pomocí příkazového řádku Uninstall program. Příklad: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Odebrat nekompatibilní ovladače**: do této skupiny přidejte kroky, pokud chcete odebrat všechny ovladače, které nejsou kompatibilní s touto verzí Windows 10.
- **Odebrat nebo pozastavit zabezpečení třetí strany**: do této skupiny přidejte kroky, pokud chcete odebrat nebo pozastavit zabezpečovací programy třetích stran, jako je třeba antivirová ochrana.
   - Pokud používáte program pro šifrování disků od jiného výrobce, poskytněte jeho ovladač šifrování pro instalační program systému Windows s [možností příkazového řádku](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers** . Přidejte krok [nastavit proměnnou pořadí úloh](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) do pořadí úkolů v této skupině. Nastavte proměnnou pořadí úloh na **OSDSetupAdditionalUpgradeOptions**. Nastavte hodnotu na **/ReflectDriver** s cestou k ovladači. Tato [Proměnná akce pořadí úkolů](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) připojuje instalační program systému Windows příkazového řádku, který používá pořadí úkolů. Další pokyny k tomuto procesu získáte od dodavatele softwaru.

### <a name="new-groups-under-post-processing"></a>Nové skupiny v rámci **následného zpracování**
- **Použít ovladače založené na instalaci**: do této skupiny přidejte kroky, pokud chcete nainstalovat ovladače založené na instalaci (. exe) z balíčků.
- **Instalace nebo povolení zabezpečení třetích stran**: do této skupiny přidejte kroky, pokud chcete nainstalovat nebo povolit zabezpečovací programy třetích stran, jako je třeba antivirová ochrana. 
- **Nastavení výchozích aplikací a přidružení pro Windows**: přidejte do této skupiny kroky, abyste nastavili výchozí aplikace Windows a přidružení souborů. Nejprve Připravte referenční počítač s požadovanými přidruženími aplikace. Pak spusťte následující příkazový řádek pro export: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Přidejte soubor XML do balíčku. Pak v této skupině přidejte krok [Spustit příkazový řádek](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . Zadejte balíček, který obsahuje soubor XML, a pak zadejte následující příkazový řádek: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Další informace najdete v tématu [Export nebo import výchozích přidružení aplikace](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Použít přizpůsobení a přizpůsobení**: do této skupiny přidejte kroky, pokud chcete použít přizpůsobení nabídky Start, jako je například organizace skupin programů. Další informace najdete v tématu [přizpůsobení úvodní obrazovky](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Další doporučení
- Přečtěte si dokumentaci k Windows a [vyřešte chyby upgradu Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Tento článek obsahuje taky podrobné informace o procesu upgradu.
- V kroku výchozí **Kontrola připravenosti zkontrolujte** , že **zajistěte minimální volné místo na disku (MB)**. Nastavte hodnotu na minimálně **16384** (16 GB) pro 32 balíček s UPGRADEM operačního systému nebo **20480** (20 GB) pro 64 bitů. 
- K opakovanému stažení zásad použijte [vestavěnou proměnnou pořadí úloh](../../osd/understand/task-sequence-variables.md) **SMSTSDownloadRetryCount** . Ve výchozím nastavení se klient opakuje dvakrát; Tato proměnná je nastavená na dvě (2). Pokud klienti nejsou připojení k pevné podnikové síti, pomohou vám další pokusy o získání zásad klienta. Pokud se tato proměnná nedá stáhnout, nejedná se o negativní vedlejší účinek, jiné než opožděné selhání.<!-- 501016 --> Také navýšit proměnnou **SMSTSDownloadRetryDelay** z výchozí hodnoty 15 sekund.
- Proveďte vložené posouzení kompatibility. 
   - Přidejte druhý krok **upgrade operačního systému** na úvodní fázi ve skupině **Příprava pro upgrade** . Pojmenujte si *posouzení upgradu*. Zadejte stejný balíček pro upgrade a pak povolte možnost **provádět kontrolu kompatibility instalační program systému Windows bez spuštění upgradu**. Povolte možnost **pokračovat při chybě** na kartě Možnosti. 
   - Hned za tento krok *posouzení upgradu* přidejte krok **příkazového řádku pro spuštění** . Zadejte následující příkazový řádek:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Na kartě **Možnosti** přidejte následující podmínku: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Tento návratový kód je desítkovým ekvivalentem MOSETUP_E_COMPAT_SCANONLY (0xC1900210), což je úspěšná kontrola kompatibility bez problémů. Pokud krok *posouzení upgradu* uspěje a vrátí tento kód, tento krok se přeskočí. V opačném případě, pokud krok vyhodnocení vrátí jiný návratový kód, tento krok pořadí úkolů neprojde návratovým kódem z kontroly kompatibility instalační program systému Windows.
   - Další informace najdete v tématu [upgrade operačního systému](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Pokud chcete změnit zařízení ze systému BIOS na rozhraní UEFI během tohoto pořadí úloh, přečtěte si téma [převod ze systému BIOS na rozhraní UEFI během místního upgradu](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Pokud máte další doporučení nebo návrhy, pošlete **nám svůj názor** na kartě **Domů** na pásu karet.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Vylepšení distribučních bodů s povoleným PXE
<!-- 1357580 -->
Pro objasnění chování [nových funkcí PXE](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) napoprvé zavedených ve verzi Technical Preview 1706 jsme přejmenovali možnost **IPv6 pro podporu** . Na kartě **PXE** vlastností distribučního bodu zaškrtněte **možnost Povolit respondér technologie PXE bez služby pro nasazení systému Windows**. 

Tato možnost povolí respondér PXE v distribučním bodě, který nevyžaduje službu pro nasazení systému Windows (WDS). Pokud tuto novou možnost povolíte v distribučním bodě, který je už povolený pomocí technologie PXE, Configuration Manager pozastaví službu WDS. Pokud tuto novou možnost zakážete, ale přesto **povolíte podporu PXE pro klienty**, pak distribuční bod POVOLÍ službu WDS znovu.

Protože služba WDS není povinná, může být distribuční bod s povoleným PXE klientským nebo serverovým operačním systémem, včetně jádra Windows serveru. Tato nová služba respondérů PXE nadále podporuje protokol IPv6 a vylepšuje také flexibilitu distribučních bodů s podporou technologie PXE ve vzdálených pobočkách.

> [!NOTE]
> Tato služba využívá stejnou základní technologii jako [Služba PXE na bázi klienta](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) v Technical Preview verze 1712. Tato funkce nevyžaduje režii role distribučního bodu.

### <a name="multicast"></a>Odesílání
Chcete-li povolit a nakonfigurovat vícesměrové vysílání na kartě **vícesměrové vysílání** vlastností distribučního bodu, musí distribuční bod používat službu WDS. 
- Pokud **povolíte podporu PXE pro klienty** a **povolíte vícesměrové vysílání pro souběžné odesílání dat na více klientů**, nemůžete **Povolit respondér technologie PXE bez služby pro nasazení systému Windows**.
- Pokud **povolíte podporu PXE pro klienty** a **povolíte respondér PXE bez služby pro nasazení systému Windows**, nemůžete **Povolit vícesměrové vysílání pro souběžné odesílání dat na více klientů** .



## <a name="deployment-templates-for-task-sequences"></a>Šablony nasazení pro pořadí úkolů
<!-- 1357391 -->
Průvodce nasazením pro pořadí úkolů teď může vytvořit šablonu nasazení. Šablonu nasazení lze uložit a použít pro existující nebo nové pořadí úkolů a vytvořit tak nasazení. 

### <a name="try-it-out"></a>Určitě to udělejte!  
Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali. 

 **Vytvoření šablony nasazení pro nové nasazení pořadí úloh** <br/> 
1. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.
2. Klikněte pravým tlačítkem na pořadí úkolů a vyberte **nasadit**. 
3. Na kartě **Obecné** si všimněte, že teď máte možnost **Vybrat šablonu nasazení**. 
4. Pokračujte v **Průvodci nasazením softwaru** a vyberte nastavení nasazení pro pořadí úkolů. 
5. Až se dostanete na kartu **Souhrn** v nástroji **Průvodce nasazením softwaru**, klikněte na **Uložit jako šablonu**.
6. Zadejte název šablony a vyberte nastavení, které chcete uložit do šablony. 
7. Klikněte na **Uložit**. Šablona je nyní k dispozici pro použití v možnosti **Vybrat šablonu nasazení** .



## <a name="product-lifecycle-dashboard"></a>Řídicí panel životního cyklu produktu
<!--1319632-->
Nový [řídicí panel životní cyklus produktu](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) zobrazuje stav zásad životního cyklu produktů Microsoft pro produkty, které jsou nainstalované na zařízeních spravovaných pomocí Configuration Manager. Řídicí panel poskytuje informace o produktech Microsoftu ve vašem prostředí, stavu podpory a koncových datech podpory. Řídicí panel můžete použít k pochopení dostupnosti podpory každého produktu. 

Přístup k řídicímu panelu životní cyklus získáte tak, že v konzole Configuration Manager přejdete na **prostředky a kompatibilita** >**funkce Asset Intelligence** >**životní cyklus produktu** .



## <a name="improvements-to-reporting"></a>Vylepšení vytváření sestav
<!--1357653-->
V důsledku [vašeho názoru](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) jsme přidali novou sestavu, **Podrobnosti údržby Windows 10 pro konkrétní kolekci**. Tato sestava ukazuje ID prostředku, název rozhraní NetBIOS, název operačního systému, název verze operačního systému, větev sestavení, větev operačního systému a stav údržby pro zařízení s Windows 10. Chcete-li získat přístup k sestavě, přejděte na **sledování** >**sestav** >**sestavy** >**operační systémy** >**Podrobnosti údržby Windows 10 pro konkrétní kolekci**.



## <a name="improvements-to-software-center"></a>Vylepšení centra softwaru
<!--1357592-->
V důsledku [vaší zpětné vazby](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) teď můžou být aplikace v centru softwaru skryté. Pokud je tato možnost povolena, aplikace, které jsou již nainstalovány, již nebudou zobrazeny na kartě aplikace. 

### <a name="try-it-out"></a>Určitě to udělejte!
V nastavení klienta centra softwaru povolte možnost **Skrýt nainstalované aplikace v centru softwaru** . Pokud koncový uživatel nainstaluje aplikaci, Sledujte chování centra softwaru.



## <a name="improvements-to-run-scripts"></a>Vylepšení spouštění skriptů
<!--1236459-->
Funkce [spustit skripty](../../apps/deploy-use/create-deploy-scripts.md) nyní vrátí výstup skriptu pomocí formátování JSON. Tento formát konzistentně vrátí čitelný výstup skriptu. Skripty, které se nepodařilo spustit, nemusí vrátit výstup. 



## <a name="boundary-group-fallback-for-management-points"></a>Záložní skupina hranic pro body správy
<!-- 1324594 -->
Od této verze můžete nakonfigurovat záložní relace pro body správy mezi [skupinami hranic](../servers/deploy/configure/boundary-groups.md). Toto chování nabízí větší kontrolu nad body správy, které klienti používají. Na kartě **relace** ve vlastnostech skupiny hranic je pro bod správy k dispozici nový sloupec. Když přidáte novou skupinu záložních hranic, doba použití pro bod správy je aktuálně vždycky nulová (0). Toto chování je stejné jako **výchozí chování** ve výchozí skupině hranic lokality.

V minulosti se k běžnému problému dochází, když máte chráněný bod správy v zabezpečené síti. Klienti v hlavní podnikové síti obdrží zásady, které obsahují tento chráněný bod správy, i když s ním nemohou komunikovat přes bránu firewall. Chcete-li vyřešit tento problém, použijte možnost **nikdy nefallback** , aby bylo zajištěno, že klienti budou moci komunikovat pouze s body správy, se kterými můžou komunikovat.

Při upgradu lokality na tuto verzi Configuration Manager přidá všechny body správy, které nejsou přístupné z Internetu, do výchozí skupiny hranic lokality. Toto chování upgradu zajišťuje, aby starší verze klienta pokračovaly v komunikaci s body správy. Aby bylo možné plně využít tuto funkci, přesuňte body správy do požadovaných skupin hranic.

Náhradní skupina hranic bodu správy nemění chování při instalaci klienta (CCMSetup). Pokud příkazový řádek neurčí počáteční bod správy pomocí parametru/MP, nový klient obdrží úplný seznam dostupných bodů správy. Pro svůj úvodní proces zavedení používá klient první bod správy, ke kterému má přístup. Po registraci klienta s lokalitou obdrží seznam bodů správy správně seřazený s tímto novým chováním. 

### <a name="prerequisites"></a>Požadavky
- Povolte [preferované body správy](../servers/deploy/configure/boundary-groups.md#bkmk_preferred). V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality** a vyberte možnost **lokality**. Na pásu karet klikněte na **Nastavení hierarchie** . Na kartě **Obecné** povolte klientům, **aby používaly body správy zadané ve skupinách hranic**. 

### <a name="known-issues"></a>Známé problémy
- Procesy nasazení operačního systému nevědí o hraničních skupinách.

### <a name="troubleshooting"></a>Řešení potíží
Nové položky se zobrazí v **LocationServices. log**. Atribut **Local** identifikuje jeden z následujících stavů:
- 0: neznámý
- 1: zadaný bod správy je pouze ve výchozí skupině hranic lokality pro záložní
- 2: zadaný bod správy je ve vzdálené nebo sousední skupině hranic. Když je bod správy v sousedu i ve výchozích skupinách hranic lokality, je to 2.
- 3: zadaný bod správy je v místní nebo aktuální skupině hranic. Pokud je bod správy v aktuální skupině hranic a zároveň buď sousedem, nebo výchozí skupinou hranic lokality, bude lokalita 3. Pokud nepovolíte nastavení preferované body správy v nastavení hierarchie, je vždy 3 bez ohledu na to, ve které skupině hranic se bod správy nachází.

Klienti používají jako první místní body správy (místní 3), vzdálenou sekundu (u 2) a pak záložní (místní 1). 

Když klient obdrží pět chyb během deseti minut a nebude komunikovat s bodem správy v aktuální skupině hranic, pokusí se kontaktovat bod správy v sousedovi nebo výchozí skupině hranic lokality. Pokud se bod správy v aktuální skupině hranic později vrátí zpět do online režimu, klient se vrátí do místního bodu správy v dalším cyklu aktualizace. Aktualizační cyklus je 24 hodin nebo když se služba agenta Configuration Manager restartuje.



## <a name="improved-support-for-cng-certificates"></a>Vylepšená podpora pro certifikáty CNG
<!-- 1357314 -->
Configuration Manager (Current Branch) verze 1710 podporuje [certifikáty kryptografie: Next Generation (CNG)](../plan-design/network/cng-certificates-overview.md). Verze 1710 omezuje podporu klientských certifikátů v několika scénářích. 

Od této verze Technical Preview použijte certifikáty CNG pro následující role serveru s podporou protokolu HTTPS:
- Bod správy
- Distribuční bod
- Bod aktualizace softwaru

Seznam [nepodporovaných scénářů](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) zůstává stejný.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Podpora brány pro správu cloudu pro Azure Resource Manager
<!-- 1324735 -->
Při vytváření instance [brány pro správu cloudu](../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) Průvodce teď nabízí možnost vytvořit **nasazení Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) je moderní platforma pro správu všech prostředků řešení jako jedné entity, která se označuje jako [Skupina prostředků](/azure/azure-resource-manager/resource-group-overview#resource-groups). Když nasazujete CMG s Azure Resource Manager, lokalita používá Azure Active Directory (Azure AD) k ověření a vytvoření potřebných cloudových prostředků. Toto moderní nasazení nevyžaduje klasický certifikát pro správu Azure.  

Průvodce CMG stále nabízí možnost **nasazení klasické služby** pomocí certifikátu pro správu Azure. Pro zjednodušení nasazení a správy prostředků doporučujeme pro všechny nové instance CMG použít model nasazení Azure Resource Manager. Pokud je to možné, znovu nasaďte existující instance CMG prostřednictvím Správce prostředků.

Configuration Manager nemigrují existující klasické instance CMG do modelu nasazení Azure Resource Manager. Pomocí Azure Resource Manager nasazení vytvořte nové instance CMG a pak odeberte klasické instance CMG. 

> [!IMPORTANT]
> Tato funkce nepovoluje podporu pro poskytovatele cloudových služeb Azure (CSP). Nasazení CMG s Azure Resource Manager nadále používá klasickou cloudovou službu, kterou CSP nepodporuje. Další informace najdete v tématu [dostupné služby Azure v CSP Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Požadavky
- Integrace se službou [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Zjišťování uživatelů služby Azure AD není vyžadováno.
- Stejné [požadavky pro bránu pro správu cloudu](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements), s výjimkou certifikátu pro správu Azure.

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. V konzole Configuration Manager v pracovním prostoru **Správa** rozbalte položku **Cloud Services**a vyberte možnost **Brána pro správu cloudu**. Na pásu karet klikněte na **vytvořit brána pro správu cloudu** . 
2. Na stránce **Obecné** vyberte **Azure Resource Manager nasazení**. Klikněte na **Přihlásit** se a proveďte ověření pomocí účtu správce předplatného Azure. Průvodce automaticky vyplní zbývající pole z informací o předplatném služby Azure AD uložených během integrace. Pokud vlastníte více předplatných, vyberte požadované předplatné, které chcete použít. Klikněte na **Další**.  
3. Na stránce **Nastavení** zadejte jako obvykle soubor certifikátu PKI serveru. Tento certifikát definuje název služby CMG v Azure. Vyberte **oblast**a pak vyberte možnost skupiny prostředků pro **Vytvoření nové** nebo **použití existující**. Zadejte nový název skupiny prostředků nebo v rozevíracím seznamu vyberte existující skupinu prostředků. 
4. Dokončete průvodce.

> [!NOTE] 
> U vybrané aplikace serveru Azure AD přiřadí Azure oprávnění **Přispěvatel** pro předplatné. 

Monitorujte průběh nasazení služby pomocí **CloudMgr. log** ve spojovacím bodu služby.



## <a name="approve-application-requests-for-users-per-device"></a>Schvalovat žádosti o aplikace pro uživatele na zařízení
<!-- 1357015 -->
Od této verze se když uživatel požádá o aplikaci, která vyžaduje schválení, konkrétní název zařízení je teď součástí žádosti. Pokud správce žádost schválí, uživatel může aplikaci nainstalovat jenom na toto zařízení. Uživatel musí odeslat další žádost o instalaci aplikace na jiné zařízení. 

> [!NOTE]
> Tato funkce je volitelná. Při aktualizaci na tuto verzi Povolte tuto funkci v Průvodci aktualizací. Případně můžete funkci v konzole zapnout později. Další informace naleznete v části [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Požadavky
- Upgrade klienta Configuration Manager na nejnovější verzi
- Povolit nastavení klienta **použít nové centrum softwaru** ve skupině [Počítačový agent](../clients/deploy/about-client-settings.md#computer-agent)

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. Nasaďte aplikaci jako dostupnou pro kolekci uživatelů.
2. Na stránce **nastavení nasazení** povolte možnost: **Správce musí na zařízení schválit žádost o tuto aplikaci**.
3. Jako cílový uživatel použijte centrum softwaru k odeslání žádosti o aplikaci. 
4. V části **Správa aplikací** v pracovním prostoru **softwarová knihovna** konzoly Configuration Manager zobrazte **žádosti o schválení** . V seznamu teď existuje sloupec **zařízení** pro každý požadavek. Pokud v žádosti provedete akci, dialogové okno žádosti o aplikaci také obsahuje název zařízení, ze kterého uživatel žádost odeslal.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Použití centra softwaru k procházení a instalaci aplikací dostupných uživatelům na zařízeních připojených k Azure AD
<!-- 1322613 -->
Pokud nasadíte aplikace jako dostupné pro uživatele, mohou je nyní procházet a instalovat prostřednictvím centra softwaru v Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Požadavky
- Povolit HTTPS v bodu správy
- Integrace webu s [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)
- Nasazení aplikace jako k dispozici pro kolekci uživatelů
- Distribuce libovolného obsahu aplikace do [distribučního bodu cloudu](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- Povolit nastavení klienta **použít nové centrum softwaru** ve skupině [Počítačový agent](../clients/deploy/about-client-settings.md#computer-agent)
- Klient musí být: 
   - Windows 10
   - Služba Azure AD – připojeno, označovanou také jako cloudová doména – připojeno
- Podpora internetových klientů:
    - [Brána pro správu cloudu](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Povolit nastavení klienta: **Povolit žádosti o zásady uživatele od internetových klientů** ve skupině [zásad klienta](../clients/deploy/about-client-settings.md#client-policy)
- Pro podporu klientů v podnikové síti:
    - Přidat distribuční bod cloudu do hraniční skupiny používané klienty
    - Klienti musí být schopni přeložit plně kvalifikovaný název domény (FQDN) bodu správy s povoleným protokolem HTTPS.



## <a name="report-on-windows-autopilot-device-information"></a>Sestava informací o zařízení s Windows autopilotem
<!-- 1351442 -->
Windows autopilot pro Windows je řešení pro připojování a konfiguraci nových zařízení s Windows 10 moderním způsobem. Další informace najdete v tématu [Přehled Windows Autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Jednou z metod registrace existujících zařízení pomocí Windows autopilotu je odeslání informací o zařízení do Microsoft Store pro firmy a vzdělávání. Tyto informace zahrnují sériové číslo zařízení, identifikátor produktu Windows a identifikátor hardwaru. K shromáždění a hlášení informací o zařízení použijte Configuration Manager. 

### <a name="prerequisites"></a>Požadavky
- Informace o tomto zařízení se týkají jenom klientů ve Windows 10, verze 1703 a novějších.

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. V konzole Configuration Manager v pracovním prostoru **monitorování** rozbalte uzel **vytváření sestav** , rozbalte položku **sestavy**a vyberte uzel **Hardware – obecné** .
2. Spusťte novou sestavu, **informace o zařízení Windows autopilot** a podívejte se na výsledky. 
3. V prohlížeči sestav klikněte na ikonu **exportovat** a vyberte možnost **CSV (oddělený čárkami)** .
4. Po uložení souboru nahrajte data do Microsoft Store pro firmy a vzdělávání. Další informace najdete v tématu [Přidání zařízení v Microsoft Store pro firmy a vzdělávání](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Vylepšení zásad Configuration Manager pro ochranu před zneužitím v programu Windows Defender
<!-- 1356220 -->
Do Configuration Manager pro [ochranu před zneužitím v programu Windows Defender](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)se přidala další nastavení zásad pro omezení ploch útoku a řízené součásti přístupu ke složkám.

**Nové nastavení pro řízený přístup ke složkám**<br/>
Při konfiguraci řízeného přístupu ke složkám jsou k dispozici dvě další možnosti: **Blokovat pouze sektory disků** a **Auditovat pouze sektory disku**. Tato dvě nastavení umožňují řízenému přístupu ke složkám povolit jenom pro spouštěcí sektory a neumožňují ochranu určitých složek ani výchozích chráněných složek. 

**Nové nastavení pro omezení možností útoku**
- Použijte pokročilou ochranu před ransomwarem.
- Blokuje odcizení přihlašovacích údajů ze subsystému místního úřadu zabezpečení systému Windows. 
- Umožňuje zablokovat spuštění spustitelných souborů, dokud nesplní kritéria prevalence, stáří nebo seznamu důvěryhodných položek. 
- Umožňuje zablokovat nedůvěryhodné a nepodepsané procesy, které se spouští z USB.



## <a name="microsoft-edge-browser-policies"></a>Zásady prohlížeče Microsoft Edge
<!-- 1357310 -->
Pro zákazníky, kteří používají webový prohlížeč [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) na klientech s Windows 10, teď můžete vytvořit zásady nastavení dodržování předpisů Configuration Manager ke konfiguraci několika nastavení Microsoft Edge. Tato zásada aktuálně obsahuje následující nastavení:
- **Nastavit prohlížeč Microsoft Edge jako výchozí**: konfiguruje nastavení výchozí aplikace Windows 10 pro webový prohlížeč na Microsoft Edge.
- **Zakázat rozevírací seznam panelu Adresa**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Povolí synchronizaci oblíbených položek mezi prohlížeči Microsoftu**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Povolení vymazání dat procházení při ukončení**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Povolit hlavičky do Not Track**: Další informace najdete v tématu [zásady prohlížeče AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Povolení automatického vyplňování**: Další informace najdete v tématu [zásady prohlížeče AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Povolení souborů cookie**: Další informace najdete v tématu [zásady prohlížeče AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Povolení blokování automaticky otevíraných oken**: Další informace najdete v tématu [zásady prohlížeče AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Povolení návrhů hledání na adresním řádku**: Další informace najdete v tématu [zásady prohlížeče AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Povolení odesílání intranetového provozu do Internet Exploreru**: Další informace najdete v tématu [zásady prohlížeče SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Povolení správce hesel**: Další informace najdete v tématu [zásady prohlížeče AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Povolení vývojářské nástroje**: Další informace najdete v tématu [zásady prohlížeče AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Povolení rozšíření**: Další informace najdete v tématu [zásady prohlížeče AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Požadavky
- Klient Windows 10, který je připojen Azure Active Directory. 

### <a name="known-issues"></a>Známé problémy
- Místní zařízení připojená k doméně nemůžou v této verzi použít tuto zásadu. Tento problém se týká také hybridních zařízení připojených k doméně.

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

**Vytvoření zásady**
1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Rozbalte **Nastavení dodržování předpisů** a vyberte nový uzel **profily prohlížeče Microsoft Edge** . Kliknutím na pás karet **vytvoříte zásadu prohlížeče Microsoft Edge**.
2. Zadejte **název** zásady, volitelně zadejte **Popis**a klikněte na **Další**.
3. Na stránce **Nastavení** změňte hodnotu na **nakonfigurovanou** pro nastavení, která chcete zahrnout do této zásady, a klikněte na **Další**.
4. Na stránce **podporované platformy** vyberte verze a architektury operačního systému, na které se tato zásada vztahuje, a klikněte na **Další**. 
5. Dokončete průvodce.

**Nasadit zásadu**
1. Vyberte zásadu a klikněte na možnost pásu karet k **nasazení**.
2. Klikněte na **Procházet** a vyberte kolekci uživatelů nebo zařízení, do které chcete zásady nasadit. 
3. Podle potřeby vyberte další možnosti. Vygenerovat výstrahy, pokud zásady nedodržují předpisy. Nastavte plán, podle kterého klient vyhodnotí kompatibilitu zařízení s touto zásadou.
4. Kliknutím na tlačítko **OK** vytvořte nasazení.

Stejně jako u zásad nastavení dodržování předpisů klient opraví nastavení podle zadaného plánu. [Monitorujte a ohlaste dodržování předpisů zařízením](../../compliance/deploy-use/monitor-compliance-settings.md) v konzole Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Sestava pro výchozí počty prohlížečů
<!-- 1357830 -->
Nyní je k dispozici nová sestava pro zobrazení počtu klientů s určitým webovým prohlížečem jako výchozí nastavení systému Windows. 

### <a name="known-issues"></a>Známé problémy
- Při prvním otevření sestavy se zobrazí pouze počet a nikoli BrowserProgID. Pokud chcete tento problém obejít, upravte dotaz sestavy na následující syntaxi:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.
1. V konzole **Configuration Manager** v pracovním prostoru **sledování** rozbalte možnost **vytváření sestav**, rozbalte položku **sestavy**a vyberte možnost **software-společnosti a produkty**.
2. Spustí sestavu **počet výchozích prohlížečů** .

Pro Common BrowserProgIDs použijte následující referenci:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE. HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Operaský software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Podpora pro zařízení s Windows 10 ARM64
<!-- 1353704 -->
Od této verze je klient Configuration Manager podporovaný na zařízeních s Windows 10 ARM64. Stávající funkce správy klientů by měly spolupracovat s těmito novými zařízeními. Například inventář hardwaru a softwaru, aktualizace softwaru a správu aplikací. Nasazení operačního systému se v tuto chvíli nepodporuje. 

## <a name="changes-to-phased-deployments"></a>Změny v postupného nasazení
<!-- 1357405 -->
Postupná nasazení automatizují koordinované, sekvenční zavedení softwaru napříč více kolekcemi. V této verzi Technical Preview se Průvodce vytvořením fáze nasazení dá dokončit pro pořadí úkolů v konzole pro správu a vytvoří se nasazení. Druhá fáze se ale nespustí automaticky po splnění kritéria úspěchu první fáze. Druhou fázi lze ručně spustit příkazem SQL.   

### <a name="try-it-out"></a>Určitě to udělejte!  
  Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.
 
**Vytvoření postupného nasazení pro pořadí úkolů** </br>
1. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.
2. Klikněte pravým tlačítkem na existující pořadí úloh a vyberte **vytvořit dvoufázové nasazení**. 
3. Na kartě **Obecné** udělte postupné nasazení název, popis (volitelné) a vyberte **automaticky vytvořit výchozí dvoufázové nasazení**. 
4. Naplňte pole **první kolekce** a **druhá kolekce** . Vyberte **Další**.
5. Na kartě **Nastavení** vyberte jednu možnost pro každé nastavení plánování a po dokončení vyberte **Další** . 
6. Na kartě **fáze** v případě potřeby upravte jakoukoli fázi a potom klikněte na tlačítko **Další**.
7. Potvrďte svoje výběry na kartě **Souhrn** a pokračujte kliknutím na tlačítko **Další** .
8. Pokud byla dosažena kritéria úspěchu pro první fázi, postupujte podle pokynů a spusťte druhou fázi s příkazem SQL.
 
**Spuštění druhé fáze s příkazem SQL**
1. Identifikujte PhasedDeploymentID pro vytvořené nasazení pomocí následujícího dotazu SQL:<br/> `Select * from PhasedDeployment`
2. Spuštěním následujícího příkazu zahajte produkční fázi:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
