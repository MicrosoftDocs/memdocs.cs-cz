---
title: Možnosti ve verzi Technical Preview 1605
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: c38230b44f7f18e3f60cb4c88b31a03e10a37d30
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721637"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1605 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1605. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

 **Známé problémy v této verzi Technical Preview:**  

- Pokud v nástroji Technical Preview 1605 aktualizujete vlastnosti bodu správy po jeho instalaci, může se zobrazit chyba konzoly, která vynutí zavření konzoly.  Pokud k tomu dojde, můžete bod správy odinstalovat a potom znovu nainstalovat bod správy pomocí požadovaných nastavení. Alternativně můžete upravit bod správy před instalací Technical Preview 1605.  

- Když použijete funkci Windows Storu pro firmy s Technical Preview 1604 a potom upgradujte na Technical Preview 1605, nebudete už moct zobrazit data připojování. Všechny ostatní funkce i nadále fungují. Pokud jste se připojili k verzi Technical Preview 1604, zůstane při instalaci Technical Preview 1605 k dispozici připojení a není nutné provádět žádné další akce.  

  **V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a>SÍŤ VPN pro jednotlivé aplikace pro zařízení s Windows 10  
 Pro zařízení s Windows 10 spravovaná pomocí služby Configuration Manager s Intune můžete přidat seznam aplikací, které automaticky otevřou připojení VPN, které jste nakonfigurovali prostřednictvím konzoly pro správu Configuration Manager. Máte možnost omezit provoz sítě VPN na tyto aplikace nebo můžete nadále povolit veškerý provoz prostřednictvím připojení VPN.  

 **Požadavky**:  

-   Configuration Manager s Intune  

-   Profil sítě VPN s Windows 10, který se nasadil aspoň na jedno zařízení  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a>Vylepšení pořadí úkolů instalovat aktualizace softwaru  
 V pořadí úkolů instalovat aktualizace softwaru byla provedena následující vylepšení:  

-   K dispozici je nová proměnná pořadí úloh SMSTSSoftwareUpdateScanTimeout, která vám dává možnost řídit časový limit kontroly aktualizací softwaru během kroku pořadí úkolů instalovat aktualizace softwaru. Výchozí hodnota je 30 minut.  

-   Bylo vylepšeno protokolování. Soubor protokolu souboru Smsts. log bude obsahovat nové položky protokolu, které odkazují na další soubory protokolů, které vám pomůžou při řešení potíží během procesu instalace aktualizací softwaru.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a>Vylepšení kroku pořadí úkolů připravit klienta nástroje ConfigMgr pro zaznamenání  
 Krok připravit klienta nástroje ConfigMgr teď zcela odebere klienta Configuration Manager, místo aby se odebraly jenom informace o klíči. Když pořadí úkolů nasadí zaznamenanou bitovou kopii operačního systému, nainstaluje se pokaždé Configuration Manager klienta.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a>Období odkladu pro požadovaná nasazení aplikace  
 V některých případech můžete chtít dát uživatelům více času na instalaci požadovaných nasazení aplikací nad rámec všech nakonfigurovaných termínů. Například pokud se koncový uživatel vrátil jenom z dovolené, může se stát, že budou muset počkat delší dobu, než se nainstalují opožděná nasazení aplikací. Nicméně můžou aplikaci hned nainstalovat kdykoli, kdykoli chtějí.  

 Chcete-li tento problém vyřešit, můžete nyní definovat **dobu odkladu** nasazením Configuration Manager nastavení klienta do kolekce.  

 Pokud chcete nastavit dobu odkladu, proveďte následující akce:  

1. Na stránce **Počítačový agent** v nastavení klienta nakonfigurujte **po konečném termínu nasazení (hodiny) novou dobu odkladu** vlastnosti na hodnotu **1** až **120** hodin.  

2. V novém nasazení aplikace nebo ve vlastnostech stávajícího nasazení na stránce **plánování** zaškrtněte políčko **zpoždění vynucení tohoto nasazení podle uživatelských předvoleb**, až do období odkladu definovaného v nastavení klienta.  

    Všechna nasazení, která mají vybrané políčko a které jsou cílena na zařízení, na která jste nasadili nastavení klienta, bude používat dobu odkladu.  

   V této verzi se v klientských zařízeních nepoužívají období odkladu, které nakonfigurujete. Pokud nakonfigurujete období odkladu a zaškrtnete políčko, aplikace se nainstaluje do prvního nefiremního okna, které uživatel nakonfigurovali po uplynutí konečného termínu.  

   Podobné možnosti byly přidány do Průvodce nasazením aktualizací softwaru, Průvodce pravidly automatického nasazení a stránky vlastností. V této verzi Technical Preview se ale v tuto chvíli neimplementují.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a>Nové prostředí pro akce se vzdáleným zařízením  
 Bylo vylepšeno prostředí pro provádění akcí se vzdáleným zařízením z konzoly Configuration Manager.  
Běžné akce, jako je **vyřazení/vymazání**, **resetování hesla**, **vzdálené uzamčení**a **obejití zámek aktivace** , se teď dají najít v nabídce **Akce vzdáleného zařízení** , ke které přistupovali z pracovního prostoru **prostředky a kompatibilita** .  

 ![Snímek obrazovky s novými akcemi vzdáleného zařízení](media/New-Remote-Device-Actions.png)  

 Stav každé z těchto operací najdete na následujících místech:  

- V podokně podrobností vyberte zařízení z uzlu **zařízení** .  

- Na stránce **vlastnosti** zařízení.  

- Na hlavní stránce uzlu **zařízení** (ve výchozím nastavení se nemusí zobrazit všechny sloupce).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a>Aplikace pro Windows Store pro firmy  
 [Windows Store pro firmy](https://www.microsoft.com/business-store) je místo, kde můžete najít a zakoupit aplikace pro svou organizaci, a to jednotlivě i na svazku. Když obchod připojíte k Configuration Manager, můžete spravovat hromadně zakoupené aplikace z konzoly Configuration Manager, například:  

- Seznam zakoupených aplikací můžete synchronizovat s Configuration Manager  

- Aplikace, které jsou synchronizované, se zobrazí v konzole Configuration Manager a můžete je nasadit stejně jako všechny ostatní aplikace.  

- Každých 24 hodin Configuration Manager stáhne informace o licencování aplikací ze Storu a můžete si je prohlédnout v konzole Configuration Manager  

  Ve verzi 1604 Technical Preview byste mohli synchronizovat a zobrazit aplikace z Windows Storu pro firmy v konzole Configuration Manager. V této verzi jsme přidali možnost vytvářet a nasazovat aplikace Configuration Manager z synchronizovaných aplikací ze Storu.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Nastavit synchronizaci s Windows Storem pro firmy  

1.  V Azure Active Directory Zaregistrujte Configuration Manager pomocí nástroje pro správu "webová aplikace nebo webové rozhraní API". Tím získáte ID klienta, které budete potřebovat později.  

    1.  V uzlu [https://manage.windowsazure.com](https://manage.windowsazure.com)služby Active Directory vyberte svou Azure Active Directory a pak klikněte na **aplikace** > **Přidat**.  

    2.  Klikněte na **Přidat aplikaci, kterou vyvíjí moje organizace**.  

    3.  Zadejte název aplikace, vyberte **Webová aplikace** nebo **webové rozhraní API**a potom klikněte na šipku **Další** .  

    4.  Zadejte stejnou adresu URL pro **přihlašovací adresu URL** i **identifikátor URI ID aplikace**. Adresa URL může být libovolná a nemusí se překládat na skutečnou adresu. Můžete například zadat **https://&lt;yourdomain>/SCCM**.  

    5.  Dokončete průvodce.  

2.  V Azure Active Directory vytvořte klíč klienta pro registrovaný Nástroj pro správu.  

    1.  Zvýrazněte aplikaci, kterou jste právě vytvořili, a klikněte na **Konfigurovat**.  

    2.  V části **klíče**vyberte v seznamu dobu trvání a klikněte na **Uložit**. Tím se vytvoří nový klíč klienta. Nevybírejte z této stránky, dokud jste neúspěšně připojili Windows Store pro firmy k Configuration Manager.  

3.  Ve Windows Storu pro firmy nakonfigurujte Configuration Manager jako nástroj pro správu úložiště.  

    1.  Otevřete [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) a přihlaste se, pokud se zobrazí výzva.  

    2.  V případě potřeby přijměte podmínky použití.  

    3.  V části **Nástroje pro správu**klikněte na **Přidat Nástroj pro správu**.  

    4.  V **části Hledat nástroj podle názvu**zadejte název aplikace, kterou jste předtím vytvořili v AAD, a pak klikněte na **Přidat**.  

    5.  Klikněte na tlačítko **aktivovat** vedle aplikace, kterou jste právě naimportovali.  

    6.  V průvodci **Zobrazit offline licencované aplikace** klikněte na **Ano** , pokud chcete umožnit nákup aplikací licencovaných offline.  

4.  Zakupte si aspoň jednu aplikaci z Windows Storu pro firmy.  

5.  V pracovním prostoru **Správa** konzoly Configuration Manager rozbalte položku **Cloud Services**a pak klikněte na možnost **Windows Store pro firmy.**  

6.  Na kartě **Domů** ve skupině **vytvořit** klikněte na **Přidat účet Windows Store pro firmy**.  

7.  Z Azure Active Directory přidejte ID tenanta, ID klienta a klíč klienta a potom průvodce dokončete.  

8.  Až budete hotovi, zobrazí se účet, který jste nakonfigurovali v seznamu **účty Windows Storu pro firmy** v konzole Configuration Manager.  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste dokončit následující úkol a pak nám dejte vědět, jak to fungovalo, pomocí našeho formuláře pro odeslání názoru na stránce [programu Configuration Manager Feedback](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) na webu Microsoft Connect:  

 Vytvoření a nasazení aplikace Configuration Manager z licencované aplikace Windows Store pro firmy offline  

1. V pracovním prostoru **softwarová knihovna** konzoly Configuration Manager rozbalte položku **Správa aplikací**a pak klikněte na **informace o licencích pro aplikace ze Storu**.  

2. Zvolte aplikaci, kterou chcete nasadit, a potom na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit aplikaci**.  

   Vytvoří se Configuration Manager aplikace obsahující aplikaci Windows Store pro firmy. Tuto aplikaci pak můžete nasadit a monitorovat stejně jako jakoukoli jinou aplikaci Configuration Manager.  

> [!IMPORTANT]  
>  Když vytvoříte aplikaci Configuration Manager s jedním typem nasazení z offline licencované aplikace, můžete ji nasadit do zařízení, která jsou spravovaná pomocí MDM, a také spravovat s klientem Configuration Manager. Pokud se pokusíte nasadit aplikaci s více typy nasazení, instalace se nezdaří.  
>   
>  V tuto chvíli nemůžete nasazovat online licencované aplikace pomocí Configuration Manager.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a>Obecná vylepšení pro hromadně zakoupené aplikace  

-   V této verzi se hromadně zakoupené aplikace z Windows Storu pro firmy a obchodu s aplikacemi pro iOS nakupovaly do stejného zobrazení – **informace o licencích pro aplikace pro Store**.  

-   V případě hromadně zakoupených aplikací pro iOS se karta Apple Volume Purchase Program v Průvodci vytvořením aplikace odebrala v dialogovém okně **balíček aplikace pro prohlížeč iOS** . Chcete-li vytvořit hromadně zakoupenou aplikaci pro iOS, použijte následující postup:  

    1.  1.  V pracovním prostoru **softwarová knihovna** konzoly Configuration Manager rozbalte položku **Správa aplikací**a pak klikněte na **informace o licencích pro aplikace ze Storu**.  

    2.  2.  Zvolte aplikaci, kterou chcete nasadit, a potom na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit aplikaci**.  

-   Umístění, které použijete k získání a nahrání tokenu Apple VPP pro hromadně zakoupené aplikace v konzole Configuration Manager, se změnilo. Nyní to můžete provést v pracovním prostoru **správce** pod uzlem **Cloud Services** > **Apple Volume purchase program tokeny** .  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a>Ochrana podnikových dat (EDP)  
 Můžete vytvořit položky konfigurace, které umožňují nasadit zásady ochrany podnikových dat (EDP), včetně toho, abyste si vybrali chráněné aplikace, úroveň ochrany EDP a našli podniková data v síti. Další informace o EDP najdete v následujících tématech:  

- [Ochrana podnikových dat pomocí Information Protection Windows (NV)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Vytvoření a nasazení zásady Information Protection Windows (nedokončené výroby) pomocí Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a>Koncoví uživatelé mohou instalovat aplikace z Portál společnosti  
 Místní MDM se zavedla ve verzi Configuration Manager 1511. V předchozích verzích jste mohli nasadit aplikace na zařízení s Windows 10 spravovaná pomocí MDM s účelem nasazení **požadovaná** instalace pro místní zařízení spravovaná pomocí MDM.  

 V této verzi teď můžete nasazovat aplikace s účelem nasazení **dostupným** pro uživatele místních počítačů s Windows 10, které jsou spravované v MDM, a uživatelé teď můžou tyto aplikace nainstalovat sami z portál společnosti.
V této verzi Technical Preview se uživateli zobrazí chybová zpráva, pokud je Portál společnosti otevřená déle než 15 minut. Pokud chcete tento problém obejít, restartujte Portál společnosti.  

### <a name="before-you-start"></a>Než začnete  

#### <a name="server-prerequisites"></a>Požadavky na server  

-   .NET 4,5 nebo vyšší (vyžaduje restart)  

-   PowerShell 3,0 pro konfigurační skript (vyžaduje restart)  

#### <a name="client-prerequisites"></a>Požadavky klienta  

-   Windows 10 Desktop 1511 (OS build 10586,218) nebo novější  

#### <a name="general-prerequisites"></a>Obecné požadavky  

-   Ujistěte se, že jste dokončili [přípravné kroky pro místní správu mobilních zařízení](https://technet.microsoft.com/library/mt613153.aspx) a [zaregistrovali vaše zařízení](https://technet.microsoft.com/library/mt627870.aspx).  

-   Pro zajištění nejlepšího prostředí pro instalaci aplikace při použití Portál společnosti se ujistěte, že Configuration Manager aktivní připojení k Microsoft Intune.  

-   Pokud zvolíte možnost hromadného zápisu, před provedením tohoto scénáře nakonfigurujte spřažení uživatelských zařízení pro zaregistrované zařízení.  

### <a name="configuration-steps"></a>Postup konfigurace  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instalace rolí katalogu aplikací a povolení podpory správy mobilních zařízení  

1.  Přidat webové služby katalogu aplikací a role webu  

    1.  Vyberte **režim https** a **Povolte mobilní zařízení, aby používala tuto možnost bodu webové služby katalogu aplikací** .  

    2.  Omezení v této verzi Technical Preview:  

        -   Než vyberete možnost pro připojení mobilních zařízení, musíte odinstalovat všechny existující role katalogu aplikací.  

        -   Zajistěte, aby byla k dispozici pouze jedna sada rolí katalogu aplikací a role jsou umístěny společně na stejném systému lokality s rolemi bodu registrace a zprostředkujícího bodu registrace.  

2.  Ověřte, zda jsou následující komponenty v uzlu Stav součásti v konzole Configuration Manager funkční:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Konfigurovat hranice  
 Nakonfigurujte požadované hranice pro jenom intranetové distribuční body.  

> [!NOTE]  
>  Pro správu mobilních zařízení je v tuto chvíli podporovaná jenom hranice rozsahu IPv4.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Nasazení aplikace Portál společnosti a konfigurace  

1. Příprava Portál společnostiho nasazení a konfigurace pomocí konfiguračního skriptu, který je součástí Technical Preview:  

   1. Otevřete okno příkazového řádku PowerShellu se zvýšenými oprávněními.  

   2. Spustit rutinu **Set-ExecutionPolicy RemoteSigned**  

   3. V ** &lt;instalačním adresáři\>složky SCCM \CD.latest\SMSSETUP\TOOLS\MDM** spustit **.\ConfigurationScript.ps1**  

      Konfigurační skript provede následující akce:  

   4. Vytvoří aplikaci Configuration Manager s typem nasazení balíčku aplikace systému Windows s použitím **CompanyPortalOnPremisesMDM. appx** ve stejné složce.  

   5. Vytvoří položku konfigurace a standardní hodnoty konfigurace, které nakonfigurují Portál společnosti.  

   6. Nasadí standardní hodnoty konfigurace i aplikaci a přidá aplikaci do všech distribučních bodů.  

   > [!NOTE]
   >  Pokud role katalogu aplikací nejsou umístěny společně s primární lokalitou, proveďte následující akce:  
   > 
   > - V pracovním prostoru **prostředky a kompatibilita** Najděte položku konfigurace **portálu OnPremMDM Configuration CI – adresa URL serveru** konfigurace.  
   >   -   Změňte hodnotu **pravidla dodržování předpisů** na plně kvalifikovaný název domény systému lokality, ve kterém se nacházejí Role katalogu aplikací.  

2. Jakmile se aplikace Portál společnosti a její konfigurace nasadí, ověřte, že je **v části Configuration Manager** konzole pro dané zařízení kompatibilní standardní hodnoty konfigurace. V nabídce Start na zařízení se zobrazí Portál společnosti jako **portál společnosti (Technical Preview)** .  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste dokončit následující úlohy a potom nám dejte vědět, jak pracovali pomocí formuláře pro odeslání názoru na stránce [Configuration Manager Feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) na webu Microsoft Connect:  

1.  Nasaďte několik aplikací s podporovanými typy nasazení do uživatelské kolekce s účelem nasazení **k dispozici**. Pro tuto verzi Technical Preview se nepodporují aplikace, které vyžadují schválení správcem, a nebudou se zobrazovat v Portál společnosti.  

2.  Uživatelé pak můžou vyhledat a nainstalovat aplikace z Portál společnosti.  

     Po otevření Portál společnosti se zobrazí dialogové okno ověřování s názvem **Configuration Manager** zadání přihlašovacích údajů uživatele Active Directory (ve formě user@domain nebo doména \ Uživatel) pro přihlášení.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a>Nové karty pro aktualizace a operační systémy v centru softwaru  
 V této verzi byly provedeny následující změny pro zlepšení rozložení aplikace Software Center:  

-   Karta **aplikace** byla rozdělena na tři samostatné karty pro **aktualizace**, **operační systémy** (které byly v seznamu **filtrů** dříve nalezeny) a **aplikace**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a>Obsluha skupiny serverů  
 Technical Preview pro Configuration Manager, verze 1511, zahrnoval možnost vytvořit kolekci, kde všechna zařízení v kolekci tvoří skupinu serverů. Pak můžete nakonfigurovat nastavení skupiny serveru tak, aby se používalo při nasazení aktualizací softwaru do skupiny serverů, řídit procento počítačů, které se v daném čase aktualizují, a nakonfigurovat skripty PowerShellu pro předběžné nasazení a následné nasazení, které budou spouštět vlastní akce.  

 Technical Preview pro Configuration Manager, verze 1605, přidává možnost aktualizovat počítače ve skupině serverů v zadaném pořadí, které definujete, přidá rozšířené monitorování pro zobrazení stavu počítačů ve skupině serverů a poskytuje možnost Vymazat zámky nasazení, které jsou užitečné, když se klienti neúspěšně nainstalovali aktualizace softwaru a brání ostatním klientům v instalaci aktualizací softwaru.  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste dokončit následující úlohy a potom nám dejte vědět, jak pracovali pomocí formuláře pro odeslání názoru na stránce [Configuration Manager Feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) na webu Microsoft Connect:  

-   Můžu vytvořit kolekci, která představuje skupinu serverů. Pro tento test můžete nakonfigurovat, aby vaše pravidla shromažďování členství měla 2 počítače v této kolekci.   

-   Můžu určit, že počítače v serverové skupině budou instalovat aktualizace softwaru v určitém pořadí na základě nastavení skupiny serverů pro tuto kolekci. Pomocí ukázkových skriptů v postupu určete skripty před nasazením a po nasazení.  

-   Můžu do této kolekce nasadit aktualizaci softwaru. Zkontrolujte soubory Start. txt a end. txt (vytvořené z ukázkových skriptů) v C:\Temp a ověřte počáteční a koncový časy nasazení v počítačích ve skupině serverů. Další informace najdete v souboru UpdatesDeployment. log.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Vytvoření kolekce pro skupinu serverů  

1.  [Vytvořte kolekci zařízení](https://technet.microsoft.com/library/gg712295.aspx) , která obsahuje počítače ve skupině serverů.  

2.  V pracovním prostoru **prostředky a kompatibilita** klikněte na **kolekce zařízení**, klikněte pravým tlačítkem na kolekci, která obsahuje počítače ve skupině serverů, a pak klikněte na **vlastnosti**.  

3.  Na kartě **Obecné** vyberte **všechna zařízení jsou součástí stejné skupiny serverů**a pak klikněte na **Nastavení**.  

4.  Na stránce **Nastavení skupiny serverů** zadejte jedno z následujících nastavení:  

    -   **Povolí aktualizaci procenta počítačů současně**: Určuje, že v jednom okamžiku se aktualizují jenom určité procento klientů. Pokud má například kolekce 10 klientů a kolekce je nakonfigurována tak, aby aktualizovala více než 30% klientů současně, nainstaluje aktualizace softwaru v jednom okamžiku pouze 3 klienty.  

    -   **Umožnění aktualizace několika počítačů současně**: Určuje, že v jednom okamžiku se aktualizuje jenom určitý počet klientů.  

    -   **Zadejte sekvenci údržby**: Určuje, že se klienti v kolekci budou aktualizovat po jednom v sekvenci, kterou nakonfigurujete. Po dokončení instalace aktualizací softwaru bude klient instalovat aktualizace softwaru pouze poté, co je klient, který je před ním v seznamu.  

5.  Určete, jestli se má použít skript před nasazením (vyprazdňování uzlu) nebo po nasazení (obnovení uzlu).  

    > [!TIP]  
    >  Následují příklady, které můžete použít v části testování pro skripty před nasazením a po nasazení, které zapisují aktuální čas do textového souboru:  
    >   
    >  **Před nasazením**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Po nasazení**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Nasazení aktualizací softwaru do skupiny serverů a stavu monitorování  

1.  [Nasaďte aktualizace softwaru](https://technet.microsoft.com/library/gg712304.aspx) do kolekce skupin serverů.  

2.  [Monitorujte nasazení aktualizace softwaru](https://technet.microsoft.com/library/gg712304.aspx). Kromě standardních zobrazení monitorování pro nasazení aktualizací softwaru se zobrazí nový popis stavu, když klient čeká na instalaci aktualizací softwaru. Pro tento nový stav se zobrazí **čekání na zámek** .  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Vymazání zámků nasazení pro počítače ve skupině serverů  

1.  V pracovním prostoru **prostředky a kompatibilita** klikněte na **kolekce zařízení**a kliknutím na kolekci vymažte zámky nasazení.  

2.  Na kartě **Domů** ve skupině **nasazení** klikněte na **Vymazat zámky nasazení skupiny serverů**. Pokud se klientům nepodařilo nainstalovat aktualizace softwaru a zabráníte ostatním klientům v instalaci aktualizací softwaru, je možné zámky nasazení ručně vymazat.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a>Podpora služby Microsoft Defender Advanced Threat Protection  
 Microsoft Defender Advanced Threat Protection (ATP) je služba, která podnikům pomůže odhalit, prozkoumat a reagovat na pokročilé útoky v jejich sítích. Microsoft Defender ATP se dřív jmenovala jako ochrana ATP v programu Windows Defender. Přečtěte si další informace o [ATP Microsoft Defenderu](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager vám může pomáhat s připojováním a monitorováním spravovaných klientských zařízení s Windows 10 a Home Edition.  

### <a name="try-it-now"></a>Vyzkoušejte si ji hned teď!  
 Zkuste dokončit následující úlohy a potom nám dejte vědět, jak pracovali pomocí formuláře pro odeslání názoru na stránce [Configuration Manager Feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) na webu Microsoft Connect:  

- Připojení zařízení k online službě Microsoft Defender Advanced Threat Protection (ATP)  

- Monitorování nasazení ATP v Microsoft Defenderu na spravovaná zařízení  

  **Požadavky**  

- Předplatné služby Microsoft Defender Advanced Threat Protection online  

- Klienti se systémem Windows 10, výročí Edition (Build 14328 a vyšší)  

- Vytvoření konfiguračního souboru klienta pro registraci  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Jak vytvořit konfigurační soubor připojování  

  1.  Přihlášení k online službě Microsoft Defender ATP  

  2.  Klikněte na položku nabídky **klienta při připojování** .  

  3.  Vyberte **Configuration Manager** a klikněte na **Stáhnout balíček**.  

  4.  Stáhněte komprimovaný soubor archivu (. zip) a extrahujte obsah.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Připojení zařízení pro ATP v programu Microsoft Defender  

1. V konzole Configuration Manager přejděte na**Přehled** >  **prostředků a dodržování předpisů** > **Endpoint Protection** > **Zásady ochrany ATP v programu Windows Defender** a klikněte na **vytvořit zásadu ochrany ATP v programu Windows Defender**. Otevře se Průvodce zásadami ochrany ATP v programu Microsoft Defender.  

2. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender a vyberte **připojování**. Klikněte na Další.  

3. **Přejděte** ke konfiguračnímu souboru, který poskytl tenant cloudové služby Microsoft Defender ATP pro vaši organizaci. Klikněte na **Další**.  

4. Zadejte ukázky souborů, které se shromažďují a sdílejí ze spravovaných zařízení pro účely analýzy.  

   - **Žádné** – nejsou shromažďovány žádné ukázkové soubory pro analýzu.  

   - **Přenositelné spustitelné soubory** – soubory jako Program Files (. exe), soubory dynamické knihovny (. dll), soubory písem a podobné soubory, které lze zneužít v kyberútokům, jsou shromažďovány a sdíleny pro účely analýzy.  

     Klikněte na **Další**.  

5. Projděte si souhrn a dokončete průvodce.  

6. Do spravovaných klientských počítačů teď můžete nasadit zásadu ochrany ATP v programu Microsoft Defender kliknutím na **nasadit**.  

##### <a name="monitor-microsoft-defender-atp"></a>Monitorovat ATP v programu Microsoft Defender  

1.  V konzole Configuration Manager přejděte na **monitorování** > **Přehled** > **zabezpečení** a pak klikněte na ochrana **ATP v programu Windows Defender**.  

2.  Projděte si řídicí panel rozšířené ochrany před internetovými útoky v programu Microsoft Defender.  

    -   **Stav nasazení agenta v programu Windows Defender** – počet a procento oprávněných spravovaných klientských počítačů s aktivním pořízenou zásadou Microsoft Defender ATP  

    -   **Agent Health ATP v programu Windows Defender** – procento klientských počítačů hlásících stav pro svého agenta ATP v programu Microsoft Defender  

        -   **V pořádku** – funguje správně  

        -   **Neaktivní** – během časového období se neodesílají žádná data do služby.  

        -   **Stav agenta** – systémová služba pro agenta ve Windows není spuštěná.  

        -   Nepoužily se **žádné** připojené zásady, ale agent neohlásil připojení zásad.  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a>Místní Ověření stavu zařízení  
 Ověření stavu pro zařízení s Windows 10 se teď dá nakonfigurovat tak, aby komunikovala s místní infrastrukturou. Správci můžou určit, jestli se vytváření sestav provádí prostřednictvím cloudu nebo místních prostředků. Pokud je pro vytváření sestav Health Attestation vybraná možnost místní, dá se pro službu zadat adresa URL. To umožňuje klientským počítačům bez přístupu k Internetu povolit a spravovat zařízení pomocí ověření stavu.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Povolit ověření stavu pro místní zařízení  
 V 1605 jsme vyřešili několik chyb zjištěných v 1604 Technical Preview.  Pokud to chcete vyzkoušet, nakonfigurujte místní službu ověření stavu pomocí nastavení klientského agenta.  

1.  V konzole Configuration Manager přejděte na **Správa** > **Přehled** > **nastavení klienta**a pak nastavte použít místní **službu ověření stavu** na **Ano**.  

2.  Zadejte **Adresu URL místní služby Ověření stavu** a poté klikněte na **OK**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a>Nové možnosti restartování klientů s Windows 10 po instalaci aktualizací softwaru  
 Když je aktualizace softwaru, která vyžaduje restart, nasazená pomocí Configuration Manager a nainstalovaná na počítači, zobrazí se dialogové okno čeká na restartování a zobrazí se dialogové okno restartování. Pokud jste v současnosti v systému Windows 8 nebo novějším počítač vypnuli nebo restartujete pomocí možností napájení systému Windows (místo z dialogového okna restartování), dialogové okno restartovat zůstane po restartování počítače a počítač bude muset restartovat v nakonfigurovaném termínu. V této verzi Technical Preview bude možnost **aktualizovat a restartovat** a **aktualizovat a vypnout** bude k dispozici v počítačích s Windows 10 v možnostech napájení systému Windows vždy, když dojde k restartování Configuration Manager aktualizace softwaru. Po použití jedné z těchto možností se po restartování počítače nezobrazí dialogové okno restartování.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a>Předem deklarovat zařízení vlastněná společností pomocí sériového čísla IMEI nebo iOS  
 Teď můžete identifikovat zařízení vlastněná firmou tím, že importujete jejich mezinárodní čísla identity mobilních zařízení (IMEI). Můžete nahrát textový soubor s oddělovači (. csv), který obsahuje čísla zařízení IMEI, nebo můžete ručně zadat informace o zařízení.  Můžete také naimportovat sériová čísla pro zařízení s iOS.  Importované informace nastaví vlastnictví zařízení, která se registrují jako "podnik".  Pro každého uživatele, který přistupuje ke službě, se stále vyžaduje licence Intune.  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste dokončit následující úlohy a potom nám dejte vědět, jak pracovali pomocí formuláře pro odeslání názoru na stránce [Configuration Manager Feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) na webu Microsoft Connect:  

-   Importujte sadu čísel IMEI do souboru. csv. Každý řádek může obsahovat číslo IMEI následovaný polem podrobností.  

-   Ručně importujte čísla IMEI z konzoly Configuration Manager.  

-   Importujte sadu sériových čísel iOS do souboru. csv. Každý řádek znovu obsahuje číslo, po kterém následují podrobnosti pro zařízení.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Předběžné deklarování zařízení vlastněných společností na základě čísla IMEI nebo sériového čísla systému iOS  

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita** > **Přehled** >  > **všechna zařízení vlastněná společností****předem deklarovaná zařízení**a potom klikněte na **vytvořit předem deklarovaná zařízení**. Spustí se Průvodce předem deklarovanými zařízeními.  

2. Zadejte, jak chcete přidat informace o zařízení:  

   -   **Nahrajte soubor. csv obsahující čísla IMEI a podrobnosti** – Pokud chcete nahrát seznam čísel, přečtěte si téma #3.  

   -   **Ručním přidáním čísel IMEI a podrobností** – Chcete-li zadat informace ručně, zadejte číslo IMEI nebo sériové číslo iOS a podrobnosti pro zařízení a potom přejděte ke kroku #4.  

3. U nahraných souborů přejděte k souboru. csv obsahujícímu informace, které předem deklaruje zařízení vlastněná společností. Soubor musí mít následující formát, kromě horního řádku (jenom pro doprovodné materiály):  

   |**IMEI #**|**Sériové číslo iOS**|**OS**|**Zobrazí**|
   |---|---|---|---|
   |123456789012345||SYSTÉMU|Zařízení s Windows vlastněné společností|
   |123456789012|A0BCD0EFGH0J|iOS|Zařízení s iOSem patřící společnosti|
   |123456789012346||SVÉM|Zařízení s Androidem vlastněné společností|

    **Sloupcích**  

   - Sloupec 1: číslo IMEI – pro každý řádek se vyžaduje buď číslo IMEI, nebo sériové číslo iOS.  

   - Sloupec 2: sériové číslo iOS – je možné předem deklarovat pouze sériová čísla iOS. Použít číslo IMEI pro jiné platformy zařízení  

   - Sloupec 3: operační systém zařízení (požadováno velkými písmeny):  

     -   IOS – všechna zařízení s iOS  

     -   WINDOWS – zahrnuje Windows Phone, okno 10 mobilních zařízení a počítače s Windows.  

     -   ANDROID – všechna zařízení s Androidem  

   - Sloupec 4: podrobnosti – Další informace o zařízení, které se zobrazí v konzole Configuration Manager  

     Klikněte na **Další**.  

4. Zkontrolujte výsledky importu souboru. Dříve importovaná čísla IMEI nebo sériová čísla se budou aktualizovat o nové podrobnosti.  Pokračujte kliknutím na tlačítko **Další** nebo **zpět** , abyste zachovali aktualizované podrobnosti, a pak dokončete průvodce.  
