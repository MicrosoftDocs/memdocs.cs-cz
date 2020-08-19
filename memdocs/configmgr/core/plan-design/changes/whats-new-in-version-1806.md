---
title: Novinky ve verzi 1806
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1806 Configuration Manager aktuální větve.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d6703f0889590b3d37d05b7c9b283a16c0150649
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591628"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Co je nového ve verzi 1806 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1806 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1706, 1710 nebo 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 1806](../../servers/manage/checklist-for-installing-update-1806.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

Následující části obsahují podrobné informace o změnách a nových funkcích verze 1806 Configuration Manager aktuální větve.  



## <a name="deprecated-features-and-operating-systems"></a>Zastaralé funkce a operační systémy

Přečtěte si o změnách podpory před jejich implementací v [odebraných a zastaralých položkách](deprecated/removed-and-deprecated.md).

Od 14. srpna 2018 je funkce hybridní správy mobilních zařízení zastaralá. Další informace najdete v tématu [co se stalo s hybridní MDM](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infrastruktura webu

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager vždy poskytoval velké centralizované úložiště dat zařízení, které zákazníci používají pro účely vytváření sestav. Lokalita obvykle shromažďuje tato data každý týden. CMPivot je nový nástroj v konzole, který teď poskytuje přístup ke stavu zařízení ve vašem prostředí v reálném čase. Okamžitě spustí dotaz na všech aktuálně připojených zařízeních v cílové kolekci a vrátí výsledky. Tato data pak můžete filtrovat a seskupovat v nástroji. Díky poskytování dat z online klientů v reálném čase můžete rychleji odpovídat na obchodní otázky, řešit problémy a reagovat na incidenty zabezpečení. 

Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot.md).  


### <a name="site-server-high-availability"></a>Vysoká dostupnost serveru lokality
<!--1128774-->
Vysoká dostupnost samostatné role serveru primární lokality je řešení založené na Configuration Manager k instalaci dalšího serveru lokality v pasivním režimu. Server lokality v pasivním režimu je navíc k vašemu stávajícímu serveru lokality, který je v aktivním režimu. Server lokality v pasivním režimu je k dispozici pro okamžité použití v případě potřeby. 

Další informace najdete v následujících článcích: 
- [Vysoká dostupnost serveru lokality](../../servers/deploy/configure/site-server-high-availability.md) 
- [Vývojový diagram – nastavení serveru lokality v pasivním režimu](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Vývojový diagram – zvýšení úrovně serveru lokality (plánované)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Vývojový diagram – zvýšení úrovně serveru lokality (neplánované)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Vylepšení přehledů správy
Tato verze zahrnuje následující vylepšení pro správu:  

- Některé přehledy správy teď mají možnost provést akci. Tato akce buď naviguje k přidruženému uzlu v konzole, nebo zobrazuje filtrované zobrazení založené na dotazech.<!--1357930-->  

- Nová skupina pro proaktivní údržbu je k dispozici pro šest nových pravidel, což umožňuje zvýraznit potenciální problémy s konfigurací a vyhnout se tak pravidelnému udržování.<!--1352184-->  

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md).


### <a name="configuration-manager-tools"></a>Configuration Manager – nástroje
<!--1357145-->
Server a nástroje pro Configuration Manager klienta jsou teď součástí serveru. Vyhledejte je ve `CD.Latest\SMSSETUP\Tools` složce na serveru lokality. Není nutná žádná další instalace. 

Další informace najdete v tématu [Configuration Manager Tools](../../support/tools.md).


### <a name="exclude-active-directory-containers-from-discovery"></a>Vyloučení kontejnerů služby Active Directory ze zjišťování
<!--1358143-->
Chcete-li snížit počet zjištěných objektů, vylučte konkrétní kontejnery ze zjišťování systému služby Active Directory. 

Další informace najdete v tématu [Konfigurace zjišťování systémových souborů služby Active Directory](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## <a name="content-management"></a>Správa obsahu

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Konfigurace vzdálené knihovny obsahu pro server lokality
<!--1357525-->
Chcete-li konfigurovat vysokou dostupnost serveru lokality nebo uvolnit místo na pevném disku v centrální správě nebo serverech primární lokality, přemístěte knihovnu obsahu do jiného umístění úložiště. Přesuňte knihovnu obsahu na jinou jednotku na serveru lokality, na samostatný server nebo disky odolné vůči chybám v síti SAN (Storage Area Network). 

Další informace najdete v následujících článcích: 
- [Knihovna obsahu](../hierarchy/the-content-library.md)
- [Vývojový diagram – správa knihovny obsahu](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Podpora distribučního bodu cloudu pro Azure Resource Manager
<!--1322209-->
Průvodce teď při vytváření cloudového distribučního bodu nabízí možnost vytvořit **nasazení Azure Resource Manager**. Azure Resource Manager je moderní platforma pro správu všech prostředků řešení jako jedné entity, která se označuje jako skupina prostředků. Při nasazování distribučního bodu cloudu s Azure Resource Manager lokalita používá Azure Active Directory k ověření a vytvoření nezbytných cloudových prostředků. Toto moderní nasazení nevyžaduje klasický certifikát pro správu Azure. 

Dokumentace k funkcím distribučního bodu cloudu je také revidována a vylepšena. Další informace najdete v následujících článcích:
- [Použití distribučního bodu cloudu](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Instalace distribučního bodu cloudu](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Distribuční body pro vyžádání obsahu podporují distribuční body cloudu jako zdroj  
<!--1321554-->
Mnoho zákazníků používá distribuční body pro vyžádání obsahu ve vzdálených nebo firemních pobočkách, které stahují obsah ze zdrojového distribučního bodu v síti WAN. Pokud vaše vzdálené pobočky mají lepší připojení k Internetu nebo chcete snížit zatížení připojení WAN, teď můžete jako zdroj použít distribuční bod cloudu v Microsoft Azure. Když přidáte zdroj na kartě **distribuční bod pro vyžádání** obsahu vlastností distribučního bodu, všechny distribuční body cloudu v lokalitě jsou nyní uvedeny jako dostupné distribuční body. Chování obou rolí systému lokality zůstane stejné jako v opačném případě. 

Další informace najdete v tématu [Použití distribučních bodů pro vyžádání](../hierarchy/use-a-pull-distribution-point.md)obsahu.


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Povolit distribučním bodům použití řízení zahlcení sítě
<!--1358112-->
Přenos na pozadí s nízkou prodlevou pro Windows (LEDBAT) je funkce systému Windows Server, která usnadňuje správu přenosů v síti na pozadí. U distribučních bodů běžících na podporovaných verzích Windows serveru povolte možnost upravit síťový provoz. Klienti používají šířku pásma sítě jenom v případě, že jsou k dispozici. 

Další informace najdete v tématu [Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Částečná podpora stahování ve sdílené mezipaměti klienta pro omezení využití sítě WAN
<!--1357346-->
Zdroje sdílené mezipaměti klienta teď můžou rozdělit obsah na části. Tyto části minimalizují přenos v síti, aby se snížilo využití sítě WAN. Bod správy poskytuje podrobnější sledování částí obsahu. Pokusí se odstranit více než jedno stažení stejného obsahu pro jednu skupinu hranic. 

Další informace najdete v tématu [podpora částečného stahování](../hierarchy/client-peer-cache.md#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Možnosti skupiny hranic pro rovnocenné soubory ke stažení
<!--1356193-->
Skupiny hranic teď obsahují další nastavení, která vám poskytnou větší kontrolu nad distribucí obsahu ve vašem prostředí. Tato verze přidává následující možnosti:  

- **Povolí stahování ze strany partnerů v této skupině hranic**: bod správy poskytuje klientům seznam umístění obsahu, která obsahují partnerské zdroje. Toto nastavení má vliv také na použití ID skupin pro optimalizaci doručení.  

- **Během stahování peere se používají jenom partnerské uzly ve stejné podsíti**: bod správy obsahuje jenom v seznamu umístění obsahu partnerské zdroje, které jsou ve stejné podsíti jako klient.  

Další informace najdete v tématu [Možnosti hraniční skupiny pro rovnocenné soubory ke stažení](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Zlepšení stavu umístění zdroje sdílené mezipaměti
<!--SCCMDocs issue 850-->
Configuration Manager je efektivnější při určování, zda byl zdroj sdílené mezipaměti připojen do jiného umístění. Tím se zajistí, že bod správy nabízí jako zdroj obsahu pro klienty v novém umístění a ne na starém místě. Pokud používáte funkci sdílené mezipaměti s cestovními zdroji sdílené mezipaměti, po aktualizaci lokality na verzi 1806 aktualizujte také všechny zdroje sdílené mezipaměti na nejnovější verzi klienta. Bod správy nezahrnuje tyto zdroje sdílené mezipaměti v seznamu umístění obsahu, dokud nebudou aktualizovány alespoň na verzi 1806.

Další informace najdete v tématu [požadavky pro](../hierarchy/client-peer-cache.md#requirements)sdílenou mezipaměť.



<!-- ## Migration  -->



## <a name="client-management"></a>Správa klientů

### <a name="improvement-to-client-push-security"></a>Zlepšení zabezpečení nabízených oznámení klientů
<!--1358204-->
Při použití metody push klienta pro instalaci klienta Configuration Manager může lokalita nyní vyžadovat vzájemné ověřování pomocí protokolu Kerberos. Toto vylepšení pomáhá zabezpečit komunikaci mezi serverem a klientem. 

Další informace najdete v tématu [instalace klientů pomocí klientské nabízené instalace](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a> Vylepšený systém lokality HTTP
<!--1356889,1358228-->
Pro všechny Configuration Manager komunikačních cest se doporučuje používat komunikaci pomocí protokolu HTTPS, ale můžou být pro některé zákazníky náročné kvůli režii při správě certifikátů PKI.

Tato verze obsahuje vylepšení způsobu, jakým klienti komunikují se systémy lokality. Na kartě Vlastnosti lokality, **komunikace s klientským počítačem** vyberte možnost **https nebo http**a pak povolte novou možnost **použití Configuration Manager generovaných certifikátů pro systémy lokality http**. Tato funkce je předběžnou [verzí funkce](../../servers/manage/pre-release-features.md).

Další informace najdete v tématu [Rozšířená http](../hierarchy/enhanced-http.md).


### <a name="azure-ad-device-identity"></a>Identita zařízení Azure AD 
<!--1358460-->
Zařízení Azure AD, které je [připojené k Azure AD](/azure/active-directory/devices/concept-azure-ad-join) nebo [hybridní](/azure/active-directory/devices/concept-azure-ad-join-hybrid) , bez přihlášení uživatele Azure AD, může bezpečně komunikovat s přiřazenou lokalitou. Cloudová identita zařízení je nyní dostačující k ověřování pomocí CMG a bodu správy.  

Další informace najdete v tématu [Rozšířená http](../hierarchy/enhanced-http.md).


### <a name="cmtrace-installed-with-client"></a>CMTrace nainstalované s klientem
<!--1357971-->
Nástroj pro zobrazení protokolu CMTrace se teď automaticky nainstaluje společně s klientem Configuration Manager. Přidá se do instalačního adresáře klienta, který je ve výchozím nastavení `%WinDir%\ccm\cmtrace.exe` . 

Další informace najdete v tématu [CMTrace](../../support/cmtrace.md).


### <a name="cloud-management-dashboard"></a>Řídicí panel pro správu cloudu
<!--1358461-->
Nový řídicí panel pro správu cloudu poskytuje centralizované zobrazení použití brány pro správu cloudu (CMG). Pokud je lokalita připojená pomocí Azure AD, zobrazuje také data o cloudových uživatelích a zařízeních.   

Tato funkce zahrnuje také **analyzátor připojení CMG** pro ověřování v reálném čase, který pomáhá řešit potíže. Nástroj v konzole kontroluje aktuální stav služby a komunikační kanál prostřednictvím spojovacího bodu CMG k jakýmkoli bodům správy, které povolují přenos CMG. 

Další informace najdete v následujících částech článku [monitorování CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md) :  
- [Řídicí panel pro správu cloudu](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Analyzátor připojení](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Vylepšení brány pro správu cloudu

Verze 1806 obsahuje následující vylepšení brány pro správu cloudu (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Zjednodušený příkazový řádek pro zavedení klienta
<!--1358215-->
Při instalaci klienta Configuration Manager na Internet prostřednictvím CMG je v příkazovém řádku nyní vyžadováno méně vlastností. Toto vylepšení snižuje velikost příkazového řádku používaného v Microsoft Intune při přípravě spolusprávy. 

Další informace najdete v tématu [Příprava internetových zařízení pro spolusprávu](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

#### <a name="download-content-from-a-cmg"></a>Stažení obsahu z CMG
<!--1358651-->
Dříve jste museli nasadit distribuční bod cloudu a CMG jako samostatné role. CMG teď může také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure. 

Další informace najdete v tématu [Úprava CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Pro Azure AD není vyžadován důvěryhodný kořenový certifikát.
<!--503899-->
Při vytváření CMG už nebudete muset poskytovat [důvěryhodný kořenový certifikát](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) na stránce nastavení. Tento certifikát se nevyžaduje při použití Azure Active Directory (Azure AD) pro ověřování klientů, ale používá se v průvodci. Pokud používáte certifikáty pro ověřování klientů PKI, musíte do CMG Přidat důvěryhodný kořenový certifikát.



## <a name="co-management"></a>Spoluspráva

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synchronizace zásad MDM z Microsoft Intune pro spoluspravované zařízení
<!--1357377-->
Když přepnete úlohu spolusprávy, spoluspravovaná zařízení automaticky synchronizují zásady MDM z Microsoft Intune. K této synchronizaci dojde také v případě, že spustíte akci pro **stažení zásad počítače** z oznámení klienta v konzole Configuration Manager. 

Další informace najdete v tématu [Postup přepnutí úloh Configuration Manager do Intune](../../../comanage/how-to-switch-workloads.md).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Přechod nových úloh do Intune pomocí spolusprávy
Následující úlohy teď můžou po povolení spolusprávy přejít z Configuration Manager do Intune:  

- **Konfigurace zařízení**<!--1357903-->: Pomocí služby Intune můžete nasadit zásady MDM a přitom dál používat Configuration Manager pro nasazení aplikací.  

- **Office 365**<!--1357841-->: Zařízení neinstalují nasazení Office 365 z Configuration Manager.  

- **Mobilní aplikace**<!--1357892-->: Všechny dostupné aplikace nasazené z Intune jsou k dispozici v Portál společnosti. Aplikace, které nasazujete z Configuration Manager, jsou k dispozici v centru softwaru. Tato funkce je předběžnou [verzí funkce](../../servers/manage/pre-release-features.md).  

Pokud chcete tyto úlohy převést, přejděte na stránku vlastností spolusprávy a přesuňte posuvník úlohy z Configuration Manager na **pilotní** nebo **všechny**. 

Další informace najdete v tématu [společná správa zařízení s Windows 10](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Podpora více hierarchií do jednoho tenanta Intune
<!--1357944-->
Někteří zákazníci mají několik hierarchií Configuration Manager a chtějí v budoucnu konsolidovat do jednoho tenanta pro Azure Active Directory a Microsoft Intune. Spoluspráva teď podporuje připojení více než jednoho Configuration Managerho prostředí ke stejnému tenantovi Intune.

Další informace najdete v tématu [požadavky pro spolusprávu](../../../comanage/overview.md#prerequisites).
 


## <a name="compliance-settings"></a>Nastavení dodržování předpisů

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurace nastavení filtru SmartScreen v programu Windows Defender pro Microsoft Edge
<!--1353701-->
Zásady nastavení dodržování předpisů prohlížeče Microsoft Edge přidávají následující tři nastavení filtru SmartScreen v programu Windows Defender: 
- Povolení filtru SmartScreen
- Uživatelé můžou přepsat výzvu filtru SmartScreen pro weby
- Uživatelé můžou přepsat výzvu filtru SmartScreen pro soubory

Další informace najdete v tématu [Konfigurace nastavení Microsoft Edge](../../../compliance/deploy-use/browser-profiles.md).


### <a name="scap-extensions"></a>Rozšíření SCAP
<!--1357552-->
Převede obsah protokolu SCAP (Security Content Automation Protocol) na směrné plány nastavení dodržování předpisů a generuje sestavy SCAP pomocí rozšíření konzoly. Tato funkce také obsahuje nový řídicí panel, který vizualizuje dodržování předpisů klienta a také dodržování pravidel XCCDF. 





## <a name="application-management"></a>Správa aplikací

### <a name="phased-deployment-of-applications"></a>Dvoufázové nasazení aplikací
<!--1358147-->
Vytvoření postupného nasazení pro aplikaci. Postupné nasazení vám umožní orchestrovat koordinované, sekvenční zavedení softwaru na základě přizpůsobitelných kritérií a skupin. Například Nasaďte aplikaci do pilotní kolekce a potom automaticky pokračuje v zavedení na základě kritérií úspěchů. 

Další informace najdete v následujících článcích:  

- [Vytvoření postupného nasazení](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [Správa a sledování postupných nasazení](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Zřídit balíčky aplikací pro Windows pro všechny uživatele na zařízení
<!--1358310-->
Zřídit aplikaci s balíčkem aplikace pro Windows pro všechny uživatele v zařízení. Jedním z běžných příkladů tohoto scénáře je zřízení aplikace od Microsoft Store pro firmy a vzdělávání, jako je Minecraftu: školství Edition, pro všechna zařízení používaná studenty ve škole. Dřív Configuration Manager podporuje jenom instalaci těchto aplikací na uživatele. Po přihlášení k novému zařízení musí student čekat na přístup k aplikaci. Když teď aplikaci zřídíte pro všechny uživatele, můžou se rychleji zvýšit. 

Další informace najdete v tématu [vytváření aplikací pro Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integrace nástrojů pro přizpůsobení Office s instalačním programem Office 365
<!--1358149-->
Nástroj pro přizpůsobení sady Office je nyní integrovaný s instalačním programem sady Office 365 v konzole Configuration Manager. Při vytváření nasazení pro Office 365 je možné dynamicky konfigurovat nejnovější nastavení spravovatelnosti Office. Společnost Microsoft aktualizuje Nástroj pro přizpůsobení Office při vydání nových sestavení sady Office 365. Tato integrace vám umožní využít nové nastavení spravovatelnosti v Office 365, jakmile budou k dispozici. 

Další informace najdete v tématu [nasazení aplikací Office 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


### <a name="support-for-new-windows-app-package-formats"></a>Podpora pro nové formáty balíčků aplikací pro Windows
<!--1357427-->
Configuration Manager teď podporuje nasazení nového balíčku aplikace pro Windows 10 (. msix) a formátů sady prostředků aplikace (. msixbundle). 

Další informace najdete v tématu [vytváření aplikací pro Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### <a name="uninstall-application-on-approval-revocation"></a>Odinstalace aplikace při odvolání schválení
<!--1357891-->
Chování se změnilo při odvolání schválení pro aplikaci. Když teď žádost o aplikaci odepřete, klient aplikace odinstaluje aplikaci ze zařízení uživatele. Toto chování vyžaduje, abyste povolili [volitelnou funkci](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **schvalovat žádosti o aplikace pro uživatele na zařízení**. 

Další informace najdete v tématu [nasazení aplikací](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager je teď integrovaný nástroj, který umožňuje převést starší balíčky na Configuration Manager aktuální aplikace větví. Potom můžete používat funkce aplikací, jako jsou závislosti, pravidla požadavků a spřažení uživatelských zařízení.

Další informace najdete v tématu [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md).



## <a name="os-deployment"></a>Nasazení operačního systému

### <a name="improvements-to-phased-deployments"></a>Vylepšení postupného nasazení

Tato verze zahrnuje následující vylepšení postupného nasazení:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Vytvoření postupného nasazení s ručně nakonfigurovanými fázemi
<!--1358148-->
V pořadí úkolů teď při vytváření dvoufázového nasazení ručně nakonfigurujete fáze. Na kartě **fáze** v Průvodci vytvořením fáze nasazení přidejte až 10 dalších fází. Můžete přesto automaticky vytvořit výchozí dvoufázové nasazení. 

Další informace najdete v tématu [vytvoření postupného nasazení s ručně nakonfigurovanými fázemi](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### <a name="phased-deployment-status"></a>Stav postupného nasazení
<!--1358577-->
Postupná nasazení nyní mají nativní prostředí monitorování. V uzlu **nasazení** v pracovním prostoru **monitorování** vyberte postupné nasazení a pak na pásu karet klikněte na **Stav postupného nasazení** . 

Další informace najdete v tématu [Správa a monitorování postupného nasazení](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Postupné zavedení při dvoufázovém nasazení
<!--1358578-->
Během dvoufázového nasazení teď může probíhat v každé fázi postupně. Toto chování pomáhá zmírnit riziko problémů s nasazením a snižuje zatížení sítě způsobené distribucí obsahu na klienty. V lokalitě může být software postupně dostupný v závislosti na konfiguraci pro každou fázi. Každý klient ve fázi má konečný termín relativně k době, kdy byl software zpřístupněn. Časový interval mezi dostupným časem a konečným termínem je stejný pro všechny klienty ve fázi. 

Další informace najdete v tématu [nastavení fáze](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Vylepšení pořadí úkolů místního upgradu Windows 10
<!--1358500-->
Výchozí šablona pořadí úkolů pro místní upgrade systému Windows 10 nyní zahrnuje další novou skupinu s doporučenými akcemi, které je třeba přidat pro případ, že proces upgradu nebude úspěšný. Tyto akce usnadňují řešení potíží. Jedním z těchto nástrojů je Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). K získání podrobných informací o tom, proč upgrade Windows 10 neproběhl úspěšně, se jedná o samostatný diagnostický nástroj. 

Další informace najdete v tématu [Vytvoření pořadí úkolů pro upgrade operačního systému](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Vylepšení distribučních bodů s povoleným PXE
<!--1357580-->
Na kartě **PXE** vlastností distribučního bodu zaškrtněte **možnost Povolit respondér technologie PXE bez služby pro nasazení systému Windows**. Tato nová možnost povolí v distribučním bodě respondér technologie PXE, který nevyžaduje službu pro nasazení systému Windows (WDS). Protože služba WDS není povinná, může být distribuční bod s povoleným PXE klientským nebo serverovým operačním systémem, včetně jádra Windows serveru. Tato nová služba respondérů PXE podporuje protokol IPv6 a vylepšuje také flexibilitu distribučních bodů s podporou technologie PXE ve vzdálených pobočkách. 

Další informace najdete v tématu [Povolení technologie PXE v distribučním bodě](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Účet přístupu k síti není v některých scénářích vyžadován.
<!--1358278,1358279-->
[Vylepšená funkce systému lokality http](#bkmk_ehttp) také odebere některé závislosti na účtu přístupu k síti. Pokud povolíte možnost nové lokality pro **použití Configuration Manager generovaných certifikátů pro systémy lokality http**, následující scénáře nevyžadují účet pro přístup k síti ke stažení obsahu z distribučního bodu:  

- Pořadí úloh spuštěná ze spouštěcího média nebo technologie PXE
- Pořadí úkolů spuštěné z centra softwaru  

Tato pořadí úloh mohou být pro nasazení operačního systému nebo vlastní. Podporuje se taky pro počítače pracovní skupiny.

Další informace najdete v tématu [sekvence úloh a účet přístupu k síti](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>Další vylepšení nasazení operačního systému

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Maskovat citlivá data uložená v proměnných pořadí úkolů
 <!--1358330-->
 V kroku **nastavit proměnnou pořadí úloh** vyberte novou možnost a **tuto hodnotu nezobrazovat**. 

 Další informace najdete v tématu [nastavení proměnné pořadí úkolů](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Maskování názvu programu během příkazu Spustit pořadí úkolů
 <!--1358493-->
 Chcete-li zabránit zobrazení nebo protokolování potenciálně citlivých dat, nakonfigurujte proměnnou pořadí úloh **OSDDoNotLogCommand**.  

 Další informace najdete v tématu [proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Proměnná pořadí úkolů pro parametry DISM při instalaci ovladačů
 <!--516679/2840016-->
 Chcete-li zadat další parametry příkazového řádku pro nástroj DISM, použijte novou proměnnou pořadí úloh **OSDInstallDriversAdditionalOptions**. 

 Další informace najdete v tématu [proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Možnost použití úplného šifrování disku
 <!--SCCMDocs-pr issue 2671-->
 Jak **Nástroj BitLocker** , tak **předběžné zřízení kroků BitLockeru** nyní zahrnuje možnost **použít úplné šifrování disku**. Ve výchozím nastavení tyto kroky šifrují využité místo na jednotce. Toto výchozí chování se doporučuje, protože je rychlejší a efektivnější. 

 Další informace najdete v tématu [povolení nástroje BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) a [předběžného poskytování nástroje BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker). 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>Režim zřizování klientů není povolený s kontrolou kompatibility upgradu Windows 10.
 <!--SCCMDocs-pr issue 2812-->
 Když teď povolíte možnost **provádět kontrolu kompatibility instalační program systému Windows bez spuštění upgradu**, krok pořadí úkolů **upgradovat operační systém** nepřepne klienta Configuration Manager do režimu zřizování.

 Další informace najdete v tématu [upgrade operačního systému](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Revidovaná dokumentace pro proměnné pořadí úkolů
K dispozici jsou teď dva nové články, které vám pomohou pochopit proměnné pořadí úkolů:  

- [Použití proměnných pořadí úkolů](../../../osd/understand/using-task-sequence-variables.md) je nový článek, který popisuje různé typy proměnných, metody pro nastavení proměnných a přístup k nim.  

- [Proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md) jsou odkazy na všechny dostupné proměnné pořadí úkolů. Tento článek spojuje předchozí články, které oddělují předdefinované proměnné z proměnných akcí. 



## <a name="software-center"></a>Centrum softwaru

> [!Important]  
> Pokud chcete využívat nové funkce Configuration Manager, nejdřív aktualizujte klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.


### <a name="software-center-infrastructure-improvements"></a>Vylepšení infrastruktury centra softwaru
<!--1358309-->
Role katalogu aplikací se už nevyžadují k zobrazení aplikací, které jsou dostupné pro uživatele v centru softwaru. Tato změna vám pomůže snižovat serverovou infrastrukturu potřebnou k doručování aplikací uživatelům. Centrum softwaru teď spoléhá na bod správy, aby získal tyto informace, což pomáhá lépe škálovat větší prostředí tím, že je přiřadí ke [skupinám hranic](../../servers/deploy/configure/boundary-groups.md#management-points).

Další informace najdete v tématu [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) .  

> [!Note]  
> Role bodu webu katalogu aplikací a bodu webové služby se už *nevyžadují* v 1806, ale pořád *podporované* role. 
> 
> **Uživatelské prostředí Silverlight** pro bod webu Katalog aplikací už není podporované. Další informace najdete v tématu [odebrané a zastaralé funkce](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Zadání viditelnosti odkazu na web katalogu aplikací v centru softwaru
<!--1358214-->
Pomocí nastavení klienta můžete řídit, jestli se má odkaz pro **otevření webu katalogu aplikací** zobrazit v uzlu **stav instalace** v centru softwaru.  

Další informace najdete v tématu [nastavení klienta centra softwaru](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> **Uživatelské prostředí Silverlight** pro bod webu Katalog aplikací už není podporované. Další informace najdete v tématu [odebrané a zastaralé funkce](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Vlastní karta pro webovou stránku v centru softwaru
<!--1358132-->
Pomocí nastavení klienta můžete vytvořit přizpůsobenou kartu pro otevření webové stránky v centru softwaru. Tato funkce umožňuje zobrazit obsah koncovým uživatelům konzistentním a spolehlivým způsobem. Následující seznam obsahuje několik příkladů:  

- Kontaktujte IT: informace o tom, jak kontaktovat oddělení IT ve vaší organizaci  

- IT Support Center: samoobslužné akce, jako je hledání ve znalostní bázi nebo otevření lístku podpory.  

- Dokumentace pro koncové uživatele: články pro uživatele ve vaší organizaci na různých tématech, jako je například použití aplikací nebo upgrade na systém Windows 10.  

Další informace najdete v tématu [nastavení klienta centra softwaru](../../clients/deploy/about-client-settings.md#software-center) a [uživatelská příručka k centru softwaru](../../understand/software-center.md).


### <a name="maintenance-windows-in-software-center"></a>Okna údržby v centru softwaru
<!--1358131-->
Centrum softwaru teď zobrazí další naplánované časové období údržby. Na kartě stav instalace přepněte zobrazení ze všech na nadcházející. Zobrazuje časový rozsah a seznam naplánovaných nasazení. Pokud nejsou k dispozici žádná budoucí časová období údržby, seznam je prázdný. 

Další informace najdete v tématu [použití časových období údržby](../../clients/manage/collections/use-maintenance-windows.md) a [uživatelské příručky centra softwaru](../../understand/software-center.md).



## <a name="software-updates"></a>Aktualizace softwaru

### <a name="third-party-software-updates"></a>Aktualizace softwaru třetích stran
<!--1357605, 1352101, 1358714-->
Aktualizace softwaru třetích stran umožňují přihlášení k odběru katalogů partnerů v konzole Configuration Manager a publikování aktualizací do služby WSUS. Tyto aktualizace pak můžete nasadit pomocí stávajícího procesu správy aktualizací softwaru. 

Další informace najdete v tématu [Povolení aktualizací třetích stran](../../../sum/deploy-use/third-party-software-updates.md).


### <a name="deploy-software-updates-without-content"></a>Nasadit aktualizace softwaru bez obsahu
<!--1357933-->
Nasaďte aktualizace softwaru do zařízení bez předchozího stažení a distribuce obsahu do distribučních bodů. Tato funkce je prospěšná při práci s extrémně velkým obsahem aktualizace, nebo když chcete, aby klienti měli vždycky možnost získávat obsah z cloudové služby Microsoft Update. Klienti v tomto scénáři si také můžou stáhnout obsah od partnerských uzlů, které už mají potřebný obsah. Klient Configuration Manager nadále spravuje stahování obsahu, proto může využít funkci Configuration Manager sdílené mezipaměti nebo jiné technologie, jako je Optimalizace doručení. Tato funkce podporuje libovolný typ aktualizace, který podporuje Configuration Manager Správa aktualizací softwaru, včetně aktualizací Windows a Office. 

Další informace naleznete v možnosti **balíček bez nasazení** , když [ručně nasazujete aktualizace softwaru](../../../sum/deploy-use/manually-deploy-software-updates.md) nebo [automaticky nasazujete aktualizace softwaru](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrování pravidel automatického nasazení podle architektury aktualizace softwaru
 <!--1322266-->
Teď můžete vyfiltrovat pravidla automatického nasazení (ADR), abyste vyloučili architektury, jako je například Itanium a ARM64. Na stránce **aktualizace softwaru** v Průvodci vytvořením pravidla automatického nasazení je nyní k dispozici filtr vlastností **architektury** . 

Další informace najdete v tématu [automatické nasazení aktualizací softwaru](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="improved-wsus-maintenance"></a>Vylepšená údržba služby WSUS 
<!--1357898-->
Průvodce vyčištěním služby WSUS teď odmítne aktualizace, jejichž platnost vypršela podle pravidel nahrazení definovaných ve vlastnostech komponenty bodu aktualizace softwaru. 

Další informace najdete v tématu [Údržba aktualizací softwaru](../../../sum/deploy-use/software-updates-maintenance.md).



## <a name="reporting"></a>Vytváření sestav

### <a name="new-software-updates-compliance-report"></a>Nová sestava dodržování předpisů pro aktualizace softwaru
<!--1357775-->
Zobrazení sestav pro dodržování předpisů aktualizací softwaru obvykle zahrnuje data z klientů, kteří se nedávno nepřipojili k lokalitě. Nová sestava, **dodržování předpisů 9 – celkový stav a dodržování předpisů**, umožňuje filtrovat výsledky dodržování předpisů pro konkrétní skupinu aktualizací softwaru podle "zdravých" klientů. Tato sestava obsahuje realističtější stav dodržování předpisů aktivních klientů ve vašem prostředí. 

Další informace najdete v tématu [sestavy aktualizací softwaru](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports).



## <a name="inventory"></a>inventář

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a> Zlepšení inventáře hardwaru pro velké celočíselné hodnoty
<!--1357880-->
Inventář hardwaru dřív měl omezení pro celá čísla větší než 4 294 967 296 (2 ^ 32). Tento limit se dá dosáhnout u atributů, jako jsou velikosti pevného disku v bajtech. Bod správy nezpracovává celočíselné hodnoty nad tímto limitem, takže v databázi nebyla uložena žádná hodnota. V této verzi se tento limit zvýšil na 18446744073709551616 (2 ^ 64). 

Další informace najdete v tématu [použití velkých celočíselných hodnot](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Výchozí revize jednotky inventáře hardwaru
<!--514442-->
Ve [Configuration Manager verze 1710](whats-new-in-version-1710.md#site-infrastructure)se výchozí jednotka použitá v mnoha zobrazeních sestav změnila z megabajtů (MB) na gigabajty (GB). Z důvodu [vylepšení inventáře hardwaru pro velké celočíselné hodnoty](#bkmk_bigint)a na základě zpětné vazby od zákazníků je tato výchozí jednotka nyní MB.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Konzola nástroje Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Řídicí panel životního cyklu produktu
<!--1319632-->
Řídicí panel životní cyklus produktu zobrazuje stav zásad životního cyklu Microsoftu pro produkty společnosti Microsoft nainstalované na zařízeních spravovaných pomocí Configuration Manager. Poskytuje vám taky informace o produktech Microsoftu ve vašem prostředí, stavu podpory a koncových datech podpory. Pomocí řídicího panelu můžete pochopit dostupnost podpory jednotlivých produktů. Tyto informace vám pomohou při plánování, kdy aktualizovat produkty od společnosti Microsoft, které používáte, před dosažením jejich aktuálního konce podpory.   

Další informace najdete v tématu [řídicí panel životní cyklus produktu](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="copy-asset-details-from-monitoring-views"></a>Kopírovat podrobnosti prostředků ze zobrazení monitorování
<!--1357856-->
Následující oblasti pracovního prostoru **monitorování** teď podporují kopírování textu:  

- V uzlu **nasazení** vyberte nasazení a klikněte na **Zobrazit stav**. V podokně **Podrobnosti o aktivech** v zobrazení stav nasazení vyberte jedno nebo více zařízení.  

- Rozbalte uzel **stav distribuce** a vyberte možnost **stav obsahu**. Vyberte část softwaru a klikněte na **Zobrazit stav**. V podokně **Podrobnosti o aktivech** v zobrazení stav obsahu vyberte jeden nebo více distribučních bodů. 

Klikněte pravým tlačítkem na Asset a vyberte **Kopírovat**. Tato akce zkopíruje vybrané prostředky jako seznam s oddělovači, který obsahuje úplné podrobnosti. Klávesová zkratka **CTRL +**  +  **C** funguje také v těchto zobrazeních. 

Další informace najdete v tématu [vylepšení konzoly ve verzi 1806](../../servers/manage/admin-console-tips.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Vylepšení řídicího panelu Surface
<!--1358654-->
Tato verze obsahuje následující vylepšení řídicího panelu Surface:  

- Řídicí panel Surface nyní zobrazuje seznam relevantních zařízení, když vyberete konkrétní oddíly grafu:  

   - Kliknutím na dlaždici **procento zařízení Surface** otevřete seznam zařízení Surface.  

   - Kliknutím na pruh v dlaždici **5 nejoblíbenější verze firmwaru** otevřete seznam zařízení Surface s touto konkrétní verzí firmwaru.  

- Při prohlížení těchto seznamů zařízení na řídicím panelu Surface klikněte pravým tlačítkem myši na zařízení a proveďte běžné akce.  

Další informace najdete na [řídicím panelu Surface](../../clients/manage/surface-device-dashboard.md).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Zobrazit aktuálně přihlášeného uživatele pro zařízení
<!--1358202-->
Teď uzel **zařízení** v pracovním prostoru **prostředky a kompatibilita** zobrazuje sloupec pro **aktuálně přihlášeného uživatele**. Zobrazí se také pro všechny seznamy zařízení specifických pro kolekci. Tato hodnota je jako [stav klienta](../../clients/manage/monitor-clients.md#bkmk_indStatus)jako aktuální. Když se uživatel odhlásí, klient tuto hodnotu vymaže. Pokud není přihlášen žádný uživatel, hodnota je prázdná. 

Další informace najdete v tématu [vylepšení konzoly ve verzi 1806](../../servers/manage/admin-console-tips.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Odeslat názor z konzoly Configuration Manager  
<!--1357542-->

Poslat smajlíka! Configuration Manager tým teď můžete přímo informovat o svých prostředích. Zasílání názorů je snadné z konzoly Configuration Manager. Chceme slyšet váš názor: Praise, problémy a návrhy. V konzole Configuration Manager klikněte na tlačítko smajlíka v pravém horním rohu nad pásem karet. Tato zpětná vazba směřuje přímo k produktu Microsoft Product Team pro Configuration Manager. I když se používá centrum Feedback pro Windows 10, doporučujeme použít mechanismus zpětné vazby v konzole.  

Další informace najdete v tématu [vylepšení konzoly ve verzi 1806](../../servers/manage/admin-console-tips.md#send-feedback) a [názory na produkt](../../understand/find-help.md#BKMK_1806Feedback).



## <a name="other-updates"></a>Další aktualizace

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1806](https://support.microsoft.com/help/4459701).

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell 1806](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps).

V konzole nástroje je k dispozici následující kumulativní aktualizace (4462978) od 24. října 2018: [kumulativní aktualizace pro Configuration Manager aktuální větev, verze 1806](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Opravy hotfix

K vyřešení konkrétních problémů jsou k dispozici následující další opravy hotfix:

| ID | Title | Datum | V konzole |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Aktualizace pro Configuration Manager verze 1806, první vlna | 31. srpna 2018 | Yes |
| [4465865](https://support.microsoft.com/help/4465865) | Pokud je služba WSUS odpojená, aktualizace softwaru se nestahují v prostředí Configuration Manager.<br><br>Tato aktualizace je také v kumulativní aktualizaci (4462978). | 01. října 2018 | Yes |
| [4471892](https://support.microsoft.com/help/4471892) | Respondér technologie PXE nefunguje napříč podsítěmi v Configuration Manager 1806 | 23. listopadu 2018 | No |
| [4487960](https://support.microsoft.com/help/4487960) | Certifikát konektoru Microsoft Intune se neobnovuje v Configuration Manager | 18. ledna 2019 | Ano |


## <a name="next-steps"></a>Další kroky

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 1806](../../servers/manage/checklist-for-installing-update-1806.md).

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.  
>
> Přečtěte si další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Známé a významné problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).
