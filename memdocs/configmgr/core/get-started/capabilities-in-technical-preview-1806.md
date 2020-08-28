---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Seznamte se s novými funkcemi dostupnými v Configuration Manager Technical Preview verze 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 01c482700b56a1835e46cf5d48da75710f380496
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995394"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1806 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1806. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Technical Preview. 

Před instalací této aktualizace si přečtěte článek [Technical Preview](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Známé problémy v této verzi Technical Preview

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> Lokalita se nezdařila při upgradu se vzdálenou knihovnou obsahu
<!--514642-->
Lokalita se nemůže upgradovat s následujícími chybami v **CMUpdate. log**:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

K tomuto problému dochází v této verzi, pokud je knihovna obsahu ve vzdáleném umístění.

#### <a name="workaround"></a>Alternativní řešení
Přesuňte knihovnu obsahu na jednotku, která je místní, do serveru lokality. Další informace najdete v tématu [Konfigurace vzdálené knihovny obsahu pro server lokality](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> Aktualizace softwaru třetích stran
<!--1352101-->
Tato verze dále prochází podporu aktualizací softwaru třetích stran v důsledku vaší [zpětné vazby](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)na webu UserVoice. Pro některé běžné scénáře už nevyžadujete použití System Center Updates Publisher (SCUP). Nový uzel **katalogy aktualizací softwaru třetích stran** v konzole Configuration Manager umožňuje přihlásit se k odběru katalogů třetích stran, publikovat aktualizace do bodu aktualizace softwaru a pak je nasadit do klientů. 

V této verzi jsou k dispozici následující katalogy aktualizací softwaru třetích stran:

 | Publisher | Název katalogu |
 |--------|---------------------|
 | EMULEX | Katalog aktualizací klientů HP |

SCUP nadále podporuje i další katalogy a scénáře. Seznam katalogů v uzlu katalogy aktualizací softwaru třetích stran konzoly Configuration Manager je dynamický a bude aktualizován, protože jsou k dispozici a podporovány další katalogy.


### <a name="prerequisites"></a>Předpoklady
- Nastavte správu aktualizací softwaru s bodem aktualizace softwaru s povoleným protokolem HTTPS. Další informace najdete v tématu [Příprava na správu aktualizací softwaru](../../sum/get-started/prepare-for-software-updates-management.md).  
  - Bod aktualizace softwaru musí být na serveru lokality pro tuto funkci v této verzi. <!--515810--> 

    > [!Tip]  
    > Bod aktualizace softwaru vyžaduje protokol HTTPS, protože se jedná o požadavek na rozhraní API služby WSUS použitá ke zpracování podpisových certifikátů. Klienti nemusí být povoleni také pomocí protokolu HTTPS. Další informace o povolení HTTPS na serveru WSUS najdete v následujících článcích o pomoc:  
    > - [Zabezpečení služby WSUS pomocí protokolu SSL](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [Příspěvek na blog podpory služby WSUS](/archive/blogs/sus/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names)

- V bodu aktualizace softwaru je dostatek místa na disku pro uložení zdrojového binárního obsahu pro aktualizace softwaru třetích stran. Velikost požadovaného úložiště se liší v závislosti na dodavateli, typech aktualizací a konkrétních aktualizacích, které publikujete pro nasazení. Pokud potřebujete přesunout složku WSUSContent na jinou jednotku s větším množstvím volného místa, přečtěte si blog týmu podpory služby WSUS, [kde můžete změnit umístění, kam služba WSUS ukládá aktualizace místně](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).  

- Povolte a nasaďte nastavení klienta [Povolit aktualizace softwaru třetích stran](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) ve skupině **aktualizace softwaru** .  

- Webový server vyžaduje internetový přístup k download.microsoft.com přes port HTTPS 443. Služba synchronizace aktualizací softwaru třetí strany se aktuálně spouští na serveru lokality. Tato služba aktualizuje seznam dostupných katalogů třetích stran, stáhne katalogy při přihlášení k odběru a stáhne aktualizace, když jsou publikovány. V případě potřeby nakonfigurujte nastavení internetového proxy serveru na kartě **proxy** ve vlastnostech role systému lokality v počítači serveru lokality.  


### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fáze 1: povolení a nastavení funkce
Následující kroky proveďte *jednou pro každou hierarchii* a povolte a nastavte funkci pro použití:  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **weby** .  

2. Vyberte lokalitu nejvyšší úrovně v hierarchii. Na pásu karet klikněte na položku **Konfigurovat součásti webu**a vyberte možnost **bod aktualizace softwaru**.  

3. Přepněte na kartu **aktualizace třetích stran** . Vyberte možnost **Povolení aktualizací softwaru třetích stran**. Další informace o možnostech certifikátu najdete v tématu [vylepšení pro povolení podpory aktualizací softwaru třetích stran](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Pokud pro správu tohoto certifikátu použijete výchozí možnost Configuration Manager, vytvoří se v uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** nový certifikát typu **Služba WSUS pro zápis jiného výrobce** .  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fáze 2: přihlášení k odběru katalogu a synchronizovaných aktualizací třetích stran
U *každého katalogu třetích stran* , ke kterému se chcete přihlásit, proveďte následující kroky:  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **aktualizace softwaru** a vyberte uzel **katalogy aktualizací softwaru třetích stran** .  

2. Vyberte katalog k přihlášení k odběru a klikněte na pásu karet na **přihlásit k odběru katalogu** .   

3. Zkontrolujte a schvalte certifikát katalogu.  

   > [!Note]  
   > Když se přihlásíte k odběru katalogu aktualizací softwaru třetí strany, certifikát, který zkontrolujete a schválíte v průvodci, se přidá do lokality. Tento certifikát je typu **katalog aktualizací softwaru třetích stran**. Můžete ji spravovat v uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** .  

4. Dokončete průvodce.  

   > [!Tip]  
   > Po počátečním předplatném by se měl katalog začít stahovat hned. Pak se znovu synchronizuje každých 24 hodin v této verzi. Pokud nechcete čekat na automatické stahování katalogu, klikněte na tlačítko **synchronizovat nyní** na pásu karet.  
   > 
   > Po stažení katalogu se metadata produktu musí synchronizovat s bodem aktualizace softwaru. Další informace o tomto procesu a o tom, jak ručně spustit, najdete v tématu [synchronizace aktualizací softwaru](../../sum/get-started/synchronize-software-updates.md). V tomto okamžiku vidíte aktualizace třetích stran v uzlu **všechny aktualizace** . 

5. Dále nakonfigurujte **produkty** bodu aktualizace softwaru pro katalog třetích stran, ke kterému jste se přihlásili. Další informace najdete v tématu [Konfigurace klasifikací a produktů k synchronizaci](../../sum/get-started/configure-classifications-and-products.md). Po změně kritérií produktu se musí znovu objevit synchronizace aktualizací softwaru.

Než budete moct zobrazit výsledky dodržování předpisů od klientů, potřebují kontrolovat a vyhodnocovat aktualizace. Tento cyklus lze aktivovat ručně z ovládacích panelů Configuration Manager v klientovi spuštěním akce **cyklus prověřování aktualizací softwaru** . Další informace o tomto procesu najdete v tématu [Úvod do aktualizací softwaru](../../sum/understand/software-updates-introduction.md).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fáze 3: nasazení aktualizací softwaru třetích stran
Proveďte následující kroky pro *jakékoli aktualizace softwaru třetích stran* , které chcete nasadit do klientů nástroje:  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **aktualizace softwaru** a vyberte uzel **všechny aktualizace softwaru** .  

   > [!Tip]  
   > Pokud chcete filtrovat seznam aktualizací, klikněte na **Přidat kritéria** . Přidejte například **dodavatele** pro **společnosti Adobe Systems, Inc.** , aby se zobrazily všechny aktualizace od společnosti Adobe.  

2. Vyberte aktualizace, které jsou vyžadovány klienty. Klikněte na **publikovat obsah aktualizace softwaru třetí strany** a zkontrolujte průběh v SMS_ISVUPDATES_SYNCAGENT. log. Tato akce stáhne binární soubory aktualizace od dodavatele a uloží je do složky WSUSContent v bodu aktualizace softwaru. Také mění stav aktualizace z metadat – pouze pro obsah a nasazení.  

   > [!Note]  
   > Při publikování obsahu aktualizace softwaru třetí strany se do lokality přidají všechny certifikáty, které se používají k podepsání obsahu. Tyto certifikáty jsou typu **obsahu aktualizací softwaru třetích stran**. Můžete je spravovat v uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** .  

3. Nasaďte aktualizace pomocí stávajícího procesu správy aktualizací softwaru. Další informace najdete v tématu [nasazení aktualizací softwaru](../../sum/deploy-use/deploy-software-updates.md). Na stránce **umístění pro stahování** v Průvodci nasazením aktualizace softwaru vyberte výchozí možnost pro **Stažení aktualizací softwaru z Internetu**. V tomto scénáři je obsah již publikován do bodu aktualizace softwaru, který slouží ke stažení obsahu pro balíček pro nasazení.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorování průběhu aktualizací softwaru třetích stran
Synchronizace aktualizací softwaru třetích stran je zpracována komponentou SMS_ISVUPDATES_SYNCAGENT na serveru lokality. Můžete zobrazit stavové zprávy z této součásti nebo zobrazit podrobnější stav v SMS_ISVUPDATES_SYNCAGENT. log. Tento protokol se nachází na serveru lokality v podsložce **log (protokoly** ) instalačního adresáře webového serveru. Ve výchozím nastavení je tato cesta `C:\Program Files\Microsoft Configuration Manager\Logs` . Další informace o monitorování obecného procesu správy aktualizací softwaru najdete v tématu [monitorování aktualizací softwaru](../../sum/deploy-use/monitor-software-updates.md).


### <a name="known-issues"></a>Známé problémy
- Synchronizační služba aktualizace softwaru třetí strany nepodporuje bod aktualizace softwaru nakonfigurovaný pro použití **účtu připojení serveru WSUS**. Pokud je tento účet nakonfigurovaný na kartě **nastavení serveru proxy a účtu** na stránce vlastností bodu aktualizace softwaru, zobrazí se v SMS_ISVUPDATES_SYNCAGENT. log následující chyba:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Další informace o tomto účtu najdete v tématu [účet připojení bodu aktualizace softwaru](../plan-design/hierarchy/accounts.md#software-update-point-connection-account).<!--515492-->  

- Nepoužívejte kombinaci dalších nástrojů, jako je SCUP, s touto novou integrovanou funkcí aktualizace softwaru třetí strany. Služba synchronizace aktualizací softwaru třetí strany nemůže publikovat obsah do aktualizací, které byly přidány do služby WSUS, pomocí jiné aplikace, nástroje nebo skriptu, například SCUP. Akce **publikovat obsah aktualizace softwaru třetí strany** se u těchto aktualizací nezdařila. Pokud potřebujete nasadit aktualizace třetích stran, které tato funkce zatím nepodporuje, použijte k nasazení těchto aktualizací svůj stávající proces v plném rozsahu.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurace nastavení filtru SmartScreen v programu Windows Defender pro Microsoft Edge
<!--1353701-->
Tato verze přidává do [zásad nastavení dodržování předpisů prohlížeče Microsoft Edge](../../compliance/deploy-use/browser-profiles.md)tři nastavení [filtru SmartScreen v programu Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) . Zásady teď na stránce **nastavení filtru SmartScreen** obsahují následující dodatečná nastavení:
- **Povolit SmartScreen**: Určuje, zda je povolen filtr SmartScreen v programu Windows Defender. Další informace najdete v tématu [zásady prohlížeče AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Uživatelé můžou přepsat výzvu filtru SmartScreen pro weby**: Určuje, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Windows Defender týkající se potenciálně škodlivých webů. Další informace najdete v tématu [zásady prohlížeče PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Uživatelé můžou přepsat výzvu filtru SmartScreen pro soubory**: Určuje, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Windows Defender týkající se stahování neověřených souborů. Další informace najdete v tématu [zásady prohlížeče PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synchronizace zásad MDM z Microsoft Intune pro spoluspravované zařízení
<!--1357377-->
Když v této verzi [přepnete úlohu spolusprávy](../../comanage/how-to-switch-workloads.md), spoluspravovaná zařízení automaticky synchronizují zásady MDM z Microsoft Intune. K této synchronizaci dojde také v případě, že spustíte akci pro **stažení zásad počítače** z oznámení klienta v konzole Configuration Manager. Další informace najdete v tématu [spuštění načtení zásad klienta pomocí klientského oznámení](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-microsoft-365-workload-to-intune-using-co-management"></a>Přechod úloh Microsoft 365 do Intune pomocí spolusprávy
<!--1357841-->
Nyní můžete převést úlohu Microsoft 365 z Configuration Manager na Microsoft Intune poté, co povolíte spolusprávu. Chcete-li převést tuto úlohu, přejděte na stránku vlastností spolusprávy a přesuňte posuvník z Configuration Manager na pilotní nebo všechny. Další informace najdete v tématu [společná správa zařízení s Windows 10](../../comanage/overview.md).

K dispozici je také nová globální podmínka, jedná **se o aplikace Office 365 spravované přes Intune na zařízení**. Tato podmínka se ve výchozím nastavení přidá jako požadavek na nové aplikace Microsoft 365. Když provedete přechod na tuto úlohu, spoluspravované klienty nesplňují požadavky na aplikaci, proto Neinstalujte Microsoft 365 nasazené prostřednictvím Configuration Manager.

### <a name="known-issue"></a>Známý problém

- Tento přechod úlohy se v současné době týká jenom nasazení Microsoft 365. Configuration Manager nadále spravuje aktualizace Microsoft 365.<!--510876--> Další informace, včetně možného alternativního řešení, najdete v poznámce k verzi Configuration Manager verze 1802 [Microsoft 365 nastavení klienta neplatí](../servers/deploy/install/release-notes.md).



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager je teď integrovaný nástroj, který umožňuje převést starší verze balíčků Configuration Manager 2007 na Configuration Manager aktuální aplikace větví. Potom můžete používat funkce aplikací, jako jsou závislosti, pravidla požadavků a spřažení uživatelských zařízení.

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

> [!Important]  
> Pokud jste dříve nainstalovali starší verzi nástroje Package Conversion Manager, před upgradem lokality ji nejprve odinstalujte. Nová integrovaná verze nevyžaduje instalaci, ale může být v konfliktu se stávajícími verzemi.  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte položku **Správa aplikací** a vyberte **balíčky**.  
2. Vyberte balíček. Ve skupině pro **Převod balíčku** na pásu karet jsou k dispozici následující tři možnosti:  
     - **Analyzovat balíček**: Spusťte proces převodu analýzou balíčku.
     - **Převést balíček**: některé balíčky je možné snadno převést na aplikace s touto akcí.
     - **Opravit a převést**: některé balíčky vyžadují před převodem na aplikace problémy, které se mají opravit.  


3. V pracovním prostoru **monitorování** vyberte **stav konverze balíčku**. Tento nový řídicí panel zobrazuje celkový stav analýzy a převodu balíčků v lokalitě. Nová úloha na pozadí automaticky shrnuje data analýzy.  

   > [!Tip]  
   > Package Conversion Manager nevyžaduje, abyste naplánovali analýzu balíčků. Tuto akci teď zpracovává integrovaná úloha Shrnutí.  

![Snímek obrazovky řídicího panelu stavu převodu balíčku](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Nasadit aktualizace softwaru bez obsahu
<!--1357933-->
Nyní můžete aktualizace softwaru nasadit do zařízení bez předchozího stažení a distribuce obsahu aktualizace softwaru do distribučních bodů. Tato funkce je prospěšná při práci s extrémně velkým obsahem aktualizace, nebo když chcete, aby klienti měli vždycky možnost získávat obsah z cloudové služby Microsoft Update. Klienti v tomto scénáři si také můžou stáhnout obsah od partnerských uzlů, které už mají potřebný obsah. Klient Configuration Manager nadále spravuje stahování obsahu, proto může využít funkci Configuration Manager sdílené mezipaměti nebo jiné technologie, jako je Optimalizace doručení. Tato funkce podporuje libovolný typ aktualizace, který podporuje Configuration Manager Správa aktualizací softwaru, včetně aktualizací Windows a Office. 

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. Spustí nasazení aktualizace softwaru na normální. Další informace najdete v tématu [nasazení aktualizací softwaru](../../sum/deploy-use/deploy-software-updates.md).
2. V Průvodci nasazením aktualizace softwaru na stránce **balíček pro nasazení** vyberte možnost Nový pro **žádný balíček pro nasazení**.

### <a name="known-issues"></a>Známé problémy
- Ikona aktualizace nasazená s tímto nastavením se nesprávně zobrazuje s červeným symbolem X, jako by byla aktualizace neplatná. Další informace najdete v tématu [ikony používané pro aktualizace softwaru](../../sum/understand/software-updates-icons.md). <!--515556-->  
- Toto nastavení je integrováno pouze v Průvodci nasazením aktualizace softwaru. Momentálně není k dispozici u pravidel automatického nasazení. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integrace nástrojů pro přizpůsobení Office s instalačním programem Office 365
<!--1358149-->
Nástroj pro přizpůsobení sady Office je nyní integrovaný s instalačním programem sady Office 365 v konzole Configuration Manager. Při vytváření nasazení pro Office 365 teď můžete dynamicky konfigurovat nejnovější nastavení spravovatelnosti Office. Nástroj pro přizpůsobení sady Office je aktualizován ve stejnou dobu jako vydání nových sestavení sady Office 365. Teď můžete využít nové nastavení spravovatelnosti v Office 365, jakmile budou k dispozici. 

### <a name="prerequisites"></a>Předpoklady
- Počítač se spuštěnou konzolou Configuration Manager potřebuje přístup přes Internet přes port HTTPS 443. Průvodce instalací klienta Office 365 používá rozhraní API standardního webového prohlížeče Windows pro otevření https://config.office.com . Pokud se použije internetový proxy server, musí být uživatel schopný získat přístup k této adrese URL.

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** a vyberte uzel **správa klientů Office 365** .
2. Kliknutím na dlaždici **instalační program office 365** na řídicím panelu spusťte Průvodce instalací klienta sady Office 365. Další informace najdete v tématu [nasazení aplikací Microsoft 365](../../sum/deploy-use/manage-office-365-proplus-updates.md).
3. Na stránce **Nastavení Office** klikněte na **Přejít na webovou stránku Office**. Pomocí online nástroje pro přizpůsobení Office určete nastavení pro toto nasazení. 
4. Až se dokončí, klikněte na **Odeslat** v pravém horním rohu. Dokončete Průvodce instalací klienta Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Vylepšení brány pro správu cloudu
Tato verze zahrnuje následující vylepšení brány pro správu cloudu (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Zjednodušený příkazový řádek pro zavedení klienta
<!--1358215-->
Při instalaci klienta Configuration Manager na Internet prostřednictvím CMG se teď vyžadují méně vlastností příkazového řádku. Další informace o jednom z příkladů tohoto scénáře najdete v [příkazovém řádku, který se má nainstalovat Configuration Manager klienta](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) při přípravě spolusprávy. 

Ve všech scénářích jsou vyžadovány následující vlastnosti příkazového řádku:
- CCMHOSTNAME  
- SMSSITECODE  

Při použití služby Azure AD pro ověřování klientů místo certifikátů ověřování klientů založených na infrastruktuře PKI se vyžadují následující vlastnosti:
- AADCLIENTAPPID  
- AADRESOURCEURI  

Následující vlastnost je povinná, pokud se klient bude přenášet zpátky na intranet:
- SMSMP  

Následující příklad obsahuje všechny výše uvedené vlastnosti:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Další informace najdete v tématu [vlastnosti instalace klienta](../clients/deploy/about-client-installation-properties.md).

### <a name="download-content-from-a-cmg"></a>Stažení obsahu z CMG
<!--1358651-->
Dříve jste museli nasadit distribuční bod cloudu a CMG jako samostatné role. Nyní v této verzi může CMG také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure. Pokud chcete tuto funkci povolit, zapněte možnost povolit, aby služba **CMG fungovala jako distribuční bod cloudu a poskytovala obsah z Azure Storage** na kartě **Nastavení** vlastností CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Pro Azure AD není vyžadován důvěryhodný kořenový certifikát.
<!--503899-->
Při vytváření CMG už nebudete muset poskytovat [důvěryhodný kořenový certifikát](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) na stránce nastavení. Tento certifikát se nevyžaduje při použití Azure Active Directory (Azure AD) pro ověřování klientů, ale používá se v průvodci.

> [!Important]  
> Pokud používáte certifikáty pro ověřování klientů PKI, musíte do CMG Přidat důvěryhodný kořenový certifikát.



## <a name="improvements-to-secure-client-communications"></a>Vylepšení zabezpečení komunikace s klientem
<!--1358278,1358279-->
Tato verze pokračuje v iteraci na [vylepšenou zabezpečenou komunikaci klientů](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) odebráním dalších závislostí na účtu přístupu k síti. Pokud povolíte možnost nové lokality pro **použití Configuration Manager generovaných certifikátů pro systémy lokality http**, následující scénáře nevyžadují účet pro přístup k síti ke stažení obsahu z distribučního bodu:  

- Pořadí úloh spuštěná ze spouštěcího média nebo technologie PXE
- Pořadí úkolů spuštěné z centra softwaru  

Tato pořadí úloh mohou být pro nasazení operačního systému nebo vlastní. Podporuje se taky pro počítače pracovní skupiny.



## <a name="software-center-infrastructure-improvements"></a>Vylepšení infrastruktury centra softwaru
<!--1358309-->
Role katalogu aplikací se už nevyžadují k zobrazení aplikací, které jsou dostupné pro uživatele v centru softwaru. Tato změna vám pomůže snižovat serverovou infrastrukturu potřebnou k doručování aplikací uživatelům. Centrum softwaru teď spoléhá na bod správy, aby získal tyto informace, což pomáhá lépe škálovat větší prostředí tím, že je přiřadí ke [skupinám hranic](../servers/deploy/configure/boundary-groups.md#management-points).

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. Odeberte všechny role katalogu aplikací z lokality. Mezi tyto role patří bod služeb webu Katalog aplikací a bod webu Katalog aplikací.
2. Nasaďte aplikaci jako dostupnou pro kolekci uživatelů.
3. Pro vyhledání, vyžádání a instalaci aplikace použijte centrum softwaru jako cílového uživatele.

### <a name="known-issue"></a>Známý problém
- Pokud k této funkci použijete klienta připojeného Azure Active Directory, nekonfigurujte lokalitu tak, aby **používala certifikáty vygenerované Configuration Manager pro systémy lokality http**. V tuto chvíli je v konfliktu s touto funkcí.<!--515846--> Další informace o tomto nastavení najdete v tématu [Vylepšená zabezpečená komunikace klientů](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Zřídit balíčky aplikací pro Windows pro všechny uživatele na zařízení
<!--1358310-->
Nyní můžete zřídit aplikaci s balíčkem aplikace systému Windows pro všechny uživatele v zařízení. Jedním z běžných příkladů tohoto scénáře je zřízení aplikace od Microsoft Store pro firmy a vzdělávání, jako je Minecraftu: školství Edition, pro všechna zařízení používaná studenty ve škole. Dřív Configuration Manager podporuje jenom instalaci těchto aplikací na uživatele. Po přihlášení k novému zařízení musí student čekat na přístup k aplikaci. Když teď aplikaci zřídíte pro všechny uživatele, můžou se rychleji zvýšit.

> [!Important]  
> Buďte opatrní při instalaci, zřizování a aktualizaci různých verzí stejného balíčku aplikace pro Windows na zařízení, což může vést k neočekávaným výsledkům. K tomuto chování může dojít při použití Configuration Manager k zřízení aplikace, ale pak uživatelům umožnit aktualizaci aplikace z Microsoft Store. Další informace najdete v pokynech k dalšímu kroku při [správě aplikací z Microsoft Store pro firmy](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Při zřizování offline licencované aplikace Configuration Manager Nedovolí, aby ho Windows automaticky aktualizoval z Microsoft Store.  

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. Vytvořte novou aplikaci. Tato aplikace musí být z balíčku aplikace pro Windows nebo z offline aplikace, kterou jste synchronizoval od Microsoft Store pro firmy a vzdělávání.  

2. Na stránce **Obecné informace** v nástroji Průvodce vytvořením aplikace povolte možnost **zřízení této aplikace pro všechny uživatele v zařízení**.  

   > [!Tip]  
   > Pokud upravujete existující aplikaci, toto nastavení je na kartě **činnost koncového uživatele** ve vlastnostech aplikace.  

3. Nasaďte aplikaci do kolekce zařízení.  

4. Přihlaste se k cílovému zařízení s různými uživatelskými účty a spusťte aplikaci.  

> [!Note]  
> Pokud potřebujete odinstalovat zřízenou aplikaci ze zařízení, ke kterým se uživatelé už přihlásili, musíte vytvořit dvě odinstalační nasazení. Zaměřte se na první nasazení odinstalace do kolekce zařízení, která obsahuje zařízení. Zajistěte druhé odinstalaci nasazení na kolekci uživatelů, která obsahuje uživatele, kteří se už přihlásili k zařízením s zřízenou aplikací. Při odinstalaci zřízené aplikace na zařízení Windows v tuto chvíli neprovádí odinstalaci této aplikace pro uživatele. 



## <a name="improvements-to-the-surface-dashboard"></a>Vylepšení řídicího panelu Surface
<!--1358654-->
Tato verze obsahuje následující vylepšení [řídicího panelu Surface](../clients/manage/surface-device-dashboard.md):
- Řídicí panel Surface teď po výběru oddílů grafů zobrazuje seznam relevantních zařízení.
   - Kliknutím na dlaždici **procento zařízení Surface** otevřete seznam zařízení Surface.
   - Kliknutím na pruh v dlaždici **5 nejoblíbenější verze firmwaru** otevřete seznam zařízení Surface s touto konkrétní verzí firmwaru.
- Při prohlížení těchto seznamů zařízení na řídicím panelu Surface můžete kliknout pravým tlačítkem na zařízení a provádět běžné akce.



## <a name="hardware-inventory-default-unit-revision"></a>Výchozí revize jednotky inventáře hardwaru
<!--514442-->
Ve [Configuration Manager verze 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure)se výchozí jednotka použitá v mnoha zobrazeních sestav změnila z megabajtů (MB) na gigabajty (GB). Z důvodu [vylepšení inventáře hardwaru pro velké celočíselné hodnoty](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)a na základě zpětné vazby od zákazníků je tato výchozí jednotka nyní MB.



## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).