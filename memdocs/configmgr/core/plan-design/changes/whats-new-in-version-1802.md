---
title: Nová verze 1802
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1802 Configuration Manager.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 11066470347db0f3ffbfadda9897aed92baa645b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073598"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Co je nového ve verzi 1802 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1802 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1702, 1706 nebo 1710. <!-- baseline only statement: -->Při instalaci nové lokality je také k dispozici jako základní verze.

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1802](https://support.microsoft.com/help/4101375).

Nyní jsou k dispozici i následující další aktualizace této verze:
- [Kumulativní aktualizace pro Configuration Manager aktuální větev verze 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, je nutné použít základní verzi Configuration Manager.  
>
> Další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Následující části obsahují podrobné informace o změnách a nových funkcích verze 1802 Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruktura webu

### <a name="reassign-distribution-point"></a>Změna přiřazení distribučního bodu
<!-- 1306937 -->
Mnoho zákazníků má velké Configuration Manager infrastruktury a snižuje primární nebo sekundární lokalitu, aby se zjednodušilo jejich prostředí. Pořád potřebují uchovávat distribuční body v pobočkách, aby poskytovaly obsah spravovaným klientům. Tyto distribuční body často obsahují více terabajtů nebo více obsahu. Tento obsah je nákladný v čase a šířka pásma sítě pro distribuci na tyto vzdálené servery. Tato funkce umožňuje změnit přiřazení distribučního bodu k jiné primární lokalitě bez nutnosti opětovné distribuce obsahu. Tato akce aktualizuje přiřazení systému lokality a uchovává veškerý obsah na serveru. Další informace najdete v tématu [Změna přiřazení distribučního bodu](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Konfigurace optimalizace doručování Windows pro použití Configuration Manager skupin hranic
<!-- 1324696 -->
Skupiny hranic Configuration Manager slouží k definování a regulaci distribuce obsahu napříč podnikovou sítí a vzdálenými pobočkami. [Optimalizace doručení Windows](/windows/deployment/update/waas-delivery-optimization) je cloudová technologie peer-to-peer pro sdílení obsahu mezi zařízeními s Windows 10. Od této verze můžete nakonfigurovat optimalizaci doručování, aby při sdílení obsahu mezi partnerskými uzly používala vaše skupiny hranic. Nové nastavení klienta použije identifikátor skupiny hranic jako identifikátor skupiny Optimalizace doručení na klientovi. Když klient komunikuje s cloudovou službou Optimalizace doručení, používá tento identifikátor k vyhledání partnerských uzlů s požadovaným obsahem. Další informace najdete v tématu [základní koncepty správy obsahu](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Podpora pro zařízení s Windows 10 ARM64
<!-- 1353704 -->
Od této verze je klient Configuration Manager podporovaný na zařízeních s Windows 10 ARM64. Stávající funkce správy klientů by měly spolupracovat s těmito novými zařízeními. Například inventář hardwaru a softwaru, aktualizace softwaru a správu aplikací. Nasazení operačního systému se v tuto chvíli nepodporuje. 

### <a name="improved-support-for-cng-certificates"></a>Vylepšená podpora pro certifikáty CNG
<!-- 1357314 -->
Configuration Manager (Current Branch) verze 1710 podporuje [certifikáty kryptografie: Next Generation (CNG)](../network/cng-certificates-overview.md). Verze 1710 omezuje podporu klientských certifikátů v několika scénářích. 

Od této verze použijte certifikáty CNG pro následující role serveru s podporou protokolu HTTPS:
- Bod správy
- Distribuční bod
- Bod aktualizace softwaru
- Bod migrace stavu  


### <a name="boundary-group-fallback-for-management-points"></a>Záložní skupina hranic pro body správy
<!-- 1324594 -->
Konfigurace záložních vztahů pro body správy mezi [hraničními skupinami](../../servers/deploy/configure/boundary-groups.md). Toto chování nabízí větší kontrolu nad body správy, které klienti používají. Další informace najdete v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Spřažení lokalit distribučních bodů cloudu
<!--503719-->
Tato funkce přináší zákazníkům s více lokalitami geograficky rozptýlenou hierarchii pomocí distribučních bodů cloudu. Když internetový klient vyhledává obsah, dříve existovala žádná objednávka na seznam distribučních bodů cloudu přijatých klientem. Toto chování může vést k tomu, že internetoví klienti obdrží obsah od geograficky vzdálených cloudových distribučních bodů. Stahování obsahu z takového vzdáleného serveru je obvykle pomalejší než server blíže.
 
Díky spřažení lokalit distribučních bodů cloudu obdrží internetový klient uspořádaný seznam. Tento seznam určuje prioritu distribučních bodů cloudu z přiřazené lokality klienta. Díky tomuto chování může správce zachovat vlastní záměr pro stahování obsahu z prostředků webu.
 

## <a name="management-insights"></a>Přehledy správy
<!-- 1353967 -->
Přehledy správy v Configuration Manager poskytují informace o aktuálním stavu vašeho prostředí. Informace jsou založeny na analýze dat z databáze lokality. Přehledy vám pomůžou lépe pochopit vaše prostředí a provádět akce na základě přehledu. Podrobnosti najdete v tématu [přehledy správy](../../servers/manage/management-insights.md)

V Configuration Manager 1802 jsou k dispozici následující přehledy:
- Aplikace:
    - Aplikace bez nasazení
- Cloud Services: <!--1356412-->
    - Posouzení připravenosti spolusprávy 
    - Povolení, aby vaše zařízení byla připojená k hybridnímu Azure Active Directory
    - Modernizovat vaší infrastruktury identit a přístupu
    -  Upgradujte klienty na Windows 10 verze 1709 nebo vyšší. 
- Sbírk
    - Prázdné kolekce
- Zjednodušená správa:  <!--1355148-->
    - Zastaralé verze klienta  
- Centrum softwaru: 
    - Směrování uživatelů do centra softwaru namísto katalogu aplikací  
    - Používat novou verzi centra softwaru 
- Windows 10: <!--1357421-->
    - Konfigurace telemetrie Windows a klíče komerčního ID 
    - Připojit Configuration Manager k Upgrade Readiness 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Správa klientů

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Podpora brány pro správu cloudu pro Azure Resource Manager
<!-- 1324735 -->
Při vytváření instance [brány pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) Průvodce teď nabízí možnost vytvořit **nasazení Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) je moderní platforma pro správu všech prostředků řešení jako jedné entity, která se označuje jako [Skupina prostředků](/azure/azure-resource-manager/resource-group-overview#resource-groups). Když nasazujete CMG s Azure Resource Manager, lokalita používá Azure Active Directory (Azure AD) k ověření a vytvoření potřebných cloudových prostředků. Toto moderní nasazení nevyžaduje klasický certifikát pro správu Azure. Další informace najdete v tématu [návrh topologie CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

> [!IMPORTANT]
> Tato funkce nepovoluje podporu pro poskytovatele cloudových služeb Azure (CSP). Nasazení CMG s Azure Resource Manager nadále používá klasickou cloudovou službu, kterou CSP nepodporuje. Další informace najdete v tématu [dostupné služby Azure v CSP Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Vylepšení brány pro správu cloudu  

- Od této verze už **Brána pro správu cloudu** není součástí předběžné verze.  

- Dokumentace k funkcím je revidována a vylepšena. Další informace najdete v těchto článcích:
    - [Plánování brány pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Velikost brány pro správu cloudu a čísla škálování](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Zabezpečení a ochrana brány pro správu cloudu](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Nejčastější dotazy týkající se brány pro správu cloudu](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Certifikáty brány pro správu cloudu](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Instalace brány pro správu cloudu](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Konfigurace inventáře hardwaru pro shromažďování řetězců větších než 255 znaků
<!-- 1357389 -->
Pro vlastnosti inventáře hardwaru můžete nakonfigurovat délku řetězců, aby byla větší než 255 znaků. Tato změna se vztahuje pouze na nově přidané třídy a vlastnosti inventáře hardwaru, které nejsou klíče. Podrobnosti najdete v článku o [rozšířeném inventáři hardwaru](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255) . 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Oznámení o zastarání pro podporu klientů se systémy Linux a UNIX
 <!--510139-->
Společnost Microsoft má v úmyslu ukončit podporu klientů se systémy Linux a UNIX v Configuration Manager zhruba jeden rok, takže klienti nebudou součástí verze 1902 v předčasném kalendáři 2019. Verze Configuration Manager 1810, ve zpožděném kalendářním 2018, bude poslední verzí pro zahrnutí klientů se systémy Linux a UNIX a bude podporováno pro úplný životní cyklus Configuration Manager 1810. Po Configuration Manager 1810 by zákazníci měli zvážit Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

### <a name="surface-device-dashboard"></a>Řídicí panel zařízení Surface
<!--1355788-->
Řídicí panel zařízení Surface poskytuje informace o zařízeních Surface, která se nacházejí ve vašem prostředí. V konzole nástroje přejdete na **monitorování** > **Surface zařízení**. Můžete zobrazit položky:
- Procento povrchů
- Procento modelů Surface
- Pět hlavních verzí firmwaru

Podrobnosti najdete v článku [Surface řídicího panelu](../../clients/manage/surface-device-dashboard.md) .

### <a name="change-in-the-configuration-manager-client-install"></a>Změna v instalaci klienta Configuration Manager
<!--1356195-->
V této verzi se Silverlight už neinstaluje na klientská zařízení automaticky. Další informace najdete v tématu [předpoklady pro nasazení klientů do počítačů se systémem Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies) .

## <a name="co-management"></a>Spoluspráva

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Přechod úloh Endpoint Protection do Intune pomocí spolusprávy
<!-- 1357365 -->
 Endpoint Protection úlohy je možné po povolení spolusprávy převést na Intune. Chcete-li převést úlohu Endpoint Protection, přejděte na stránku vlastností spolusprávy a přesuňte posuvník z Configuration Manager na **pilot** nebo **vše**. Podrobnosti o úlohách najdete v tématu [úlohy spolusprávy](../../../comanage/workloads.md). Další informace o spolusprávě najdete v tématu [společná správa pro zařízení s Windows 10](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Řídicí panel spolusprávy v Configuration Manager
<!--1356648-->
Od této verze můžete zobrazit řídicí panel s informacemi o spolusprávě. Řídicí panel vám pomůže zkontrolovat počítače, které jsou ve vašem prostředí spoluspravované. Grafy můžou identifikovat zařízení, která by mohla vyžadovat pozornost. Podrobnosti najdete v článku o [společném řídicím panelu pro spolusprávu](../../../comanage/how-to-monitor.md#co-management-dashboard) . 


## <a name="compliance-settings"></a>Nastavení dodržování předpisů

### <a name="microsoft-edge-browser-policies"></a>Zásady prohlížeče Microsoft Edge
<!-- 1357310 -->
Pro zákazníky, kteří používají webový prohlížeč [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) na klientech Windows 10, vytvořte zásady nastavení dodržování předpisů Configuration Manager ke konfiguraci několika nastavení Microsoft Edge. Další informace najdete v tématu [Vytvoření profilu prohlížeče Microsoft Edge](../../../compliance/deploy-use/browser-profiles.md). 



## <a name="application-management"></a>Správa aplikací

### <a name="allow-user-interaction-when-installing-an-application"></a>Při instalaci aplikace povolte interakci s uživatelem.
<!-- 1356976 -->
Povolí koncovému uživateli interakci s instalací aplikace při spuštění pořadí úkolů. Například spusťte proces instalace, který vyzve koncového uživatele k zadání různých možností. Některé instalační programy aplikace nemůžou potiché výzvy k uživateli, nebo proces instalace může vyžadovat konkrétní hodnoty konfigurace, které uživatel zná. Tato funkce umožňuje zvládnout tyto scénáře instalace. Další informace najdete v tématu [Určení možností uživatelského prostředí pro typ nasazení](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Neupgradovat automaticky nahrazené aplikace
<!-- 1351266 -->
Nakonfigurujte nasazení aplikace tak, aby nedošlo k automatickému upgradu žádné nahrazené verze. Nyní při vytváření nasazení můžete na stránce **nastavení nasazení** v **Průvodci nasazením softwaru**pro **dostupný** účel instalace povolit nebo zakázat možnost **automaticky upgradovat jakékoli nahrazené verze této aplikace**. Další informace najdete v tématu [Určení nastavení nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Schvalovat žádosti o aplikace pro uživatele na zařízení
<!-- 1357015 -->
Od této verze se když uživatel požádá o aplikaci, která vyžaduje schválení, konkrétní název zařízení je teď součástí žádosti. Pokud správce žádost schválí, uživatel může aplikaci nainstalovat jenom na toto zařízení. Uživatel musí odeslat další žádost o instalaci aplikace na jiné zařízení. Další informace najdete v tématu [Určení nastavení nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

 > [!Note]  
 > Tato funkce je volitelná. Další informace naleznete v části [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).  


### <a name="run-scripts-improvements"></a>Spustit vylepšení skriptů 
<!-- 1236459 -->
 Od verze v této verzi už nemusíte **spouštět skripty** . Výstup skriptu nyní vrátí použití formátování JSON. Další informace najdete v tématu [Vytvoření a spuštění skriptů PowerShellu z konzoly Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md).


## <a name="operating-system-deployment"></a>Nasazení operačního systému

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Pořadí úkolů místního upgradu Windows 10 přes bránu pro správu cloudu
<!-- 1357149 -->
[Pořadí úkolů místního upgradu](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) Windows 10 teď podporuje nasazení do internetových klientů spravovaných prostřednictvím [brány pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md). Tato možnost umožňuje vzdáleným uživatelům snadněji upgradovat na Windows 10, aniž by se museli připojit k podnikové síti. Další informace naleznete v části [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Vylepšení pořadí úkolů místního upgradu Windows 10
<!-- 1357425 -->
Výchozí šablona pořadí úkolů pro místní upgrade systému Windows 10 nyní zahrnuje další skupiny s doporučenými akcemi pro přidání před a po dokončení procesu upgradu. Tyto akce jsou společné mezi mnoha zákazníky, kteří úspěšně upgradují zařízení na Windows 10. Další informace najdete v tématu [Vytvoření pořadí úkolů pro upgrade operačního systému](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Vylepšení nasazení operačního systému
Tato verze zahrnuje následující vylepšení nasazení operačního systému:
- Při spuštění CMTrace. exe v systému Windows PE již nebudete vyzváni k výběru, zda má být program nastaven jako výchozí prohlížeč pro soubory protokolu. <!-- SMS 500897 -->
- Přidejte spouštěcí bitové kopie do kroku [Stáhnout obsah balíčku](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent) pořadí úkolů.
- Vylepšení kroku [pořadí úkolů spuštění](../../../osd/understand/task-sequence-steps.md#child-task-sequence) : <!-- 1261338 -->   
  - Podpora všech scénářů nasazení operačního systému z centra softwaru, technologie PXE a médií.
  - Vylepšení akcí konzoly, jako je kopírování, import, export a upozornění při odstraňování objektu.
  - Podpora pro průvodce [vytvořením souboru připraveného obsahu](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) .
  - Integrace s ověřováním nasazení. Další informace najdete v tématu [vysoce rizikové nasazení pořadí úkolů](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - Krok pořadí úkolů spustit se teď dá použít na více úrovních pořadí úkolů, nikoli jenom na jeden vztah nadřazený-podřízený. Vztahy na více úrovních zvyšují složitost, proto používejte s opatrností. U těchto vztahů se pořád kontroluje cyklické odkazy.

### <a name="deployment-templates-for-task-sequences"></a>Šablony nasazení pro pořadí úkolů
<!-- 1357391 -->
[Průvodce nasazením pro pořadí úkolů](../../../osd/deploy-use/deploy-a-task-sequence.md) teď může vytvořit šablonu nasazení. Šablonu nasazení lze uložit a použít pro existující nebo nové pořadí úkolů a vytvořit tak nasazení. 

### <a name="phased-deployments-for-task-sequences"></a>Postupná nasazení pro pořadí úloh
<!--1356837-->
 Postupná nasazení jsou [součástí předběžné verze](../../servers/manage/pre-release-features.md). Postupná nasazení automatizují koordinované, sekvenční zavedení pořadí úkolů napříč více kolekcemi. Můžete [vytvořit dvoufázové nasazení](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) s výchozími dvěma fázemi nebo ručně nakonfigurovat několik fází. Postupné nasazení pořadí úloh nepodporuje instalaci pomocí technologie PXE nebo médií.




## <a name="software-center"></a>Centrum softwaru

### <a name="install-multiple-applications-in-software-center"></a>Instalace více aplikací v centru softwaru
<!-- 1357126 -->
Pokud chce koncový uživatel nebo stolní počítač nainstalovat na zařízení více aplikací, Centrum softwaru teď podporuje instalaci více vybraných aplikací. Díky tomuto chování může být uživatel efektivnější, i když nečeká na dokončení jedné instalace před spuštěním dalšího. Další informace najdete v tématu [Instalace více aplikací](../../understand/software-center.md#install-multiple-applications) v nové uživatelské příručce centra softwaru.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Použití centra softwaru k procházení a instalaci aplikací dostupných uživatelům na zařízeních připojených k Azure AD
<!-- 1322613 -->
Pokud nasadíte aplikace jako dostupné pro uživatele, mohou je nyní procházet a instalovat prostřednictvím centra softwaru v Azure Active Directory (Azure AD). Další informace najdete v tématu [nasazení aplikací dostupných pro uživatele na zařízeních připojených k Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Skrýt nainstalované aplikace v centru softwaru
<!--1357592-->
Nainstalované aplikace teď můžou být v centru softwaru skryté. Pokud je tato možnost povolena v nastavení klienta, aplikace, které jsou již nainstalovány, již nebudou zobrazeny na kartě aplikace. Tato možnost je nastavená jako výchozí při instalaci nebo upgradu na Configuration Manager 1802.  Nainstalované aplikace jsou stále k dispozici pro kontrolu na kartě stav instalace. Další podrobnosti najdete [v části skrýt nainstalované aplikace v centru softwaru](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled) .   

### <a name="hide-unapproved-applications-in-software-center"></a>Skrýt neschválené aplikace v centru softwaru
 <!--1355146-->
Pokud je tato možnost nastavení klienta povolena, jsou aplikace dostupné pro uživatele, které vyžadují schválení, skryté v centru softwaru.  [Skrýt neschválené aplikace v centru softwaru](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved) obsahuje další podrobnosti.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Centrum softwaru zobrazuje informace o dalších dodržování předpisů uživateli
<!-- 1235616 -->
 Když použijete Ověření stavu zařízení stav jako pravidlo zásad dodržování předpisů pro podmíněný přístup k firemním prostředkům, Centrum softwaru teď zobrazí uživateli nastavení Ověření stavu zařízení, které nedodržuje předpisy.


 ## <a name="software-updates"></a>Aktualizace softwaru 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Naplánovat, aby vyhodnocení pravidla automatického nasazení bylo posunuto od základního dne. 
<!--1357133-->
Pravidla automatického nasazení je možné naplánovat tak, aby vyhodnotila posun od základního dne. To znamená, že pokud se ve středu provede oprava úterý za vás, plán vyhodnocení se dá nastavit pro druhé úterý v měsíci posun na jeden den. Podrobnosti najdete v tématu [automatické nasazení aktualizací softwaru](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Generování sestav

### <a name="report-for-default-browser-counts"></a>Sestava pro výchozí počty prohlížečů
<!-- 1357830 -->
Nyní je k dispozici nová sestava pro zobrazení počtu klientů s určitým webovým prohlížečem jako výchozí nastavení systému Windows. Podívejte se na **výchozí sestavu počty prohlížečů** ve skupině **software-společnosti a sestavy produktů** . Další informace najdete v [seznamu sestav](../../servers/manage/list-of-reports.md#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Sestava informací o zařízení s Windows autopilotem
<!-- 1351442 -->
Windows autopilot pro Windows je řešení pro připojování a konfiguraci nových zařízení s Windows 10 moderním způsobem. Další informace najdete v tématu [Přehled Windows autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Jednou z metod registrace existujících zařízení pomocí Windows autopilotu je odeslání informací o zařízení do Microsoft Store pro firmy a vzdělávání. Tyto informace zahrnují sériové číslo zařízení, identifikátor produktu Windows a identifikátor hardwaru. Použijte Configuration Manager ke shromáždění a hlášení informací o zařízení s novou sestavou **informace o zařízení Windows autopilot**v uzlu sestavy **Hardware-obecné** . Další informace najdete v tématu Příprava pro [spolusprávu](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) v rámci přípravy na spolupráci v Internetu.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Sestava podrobností údržby Windows 10 pro konkrétní kolekci
<!--1357653-->
Sestava **Podrobnosti údržby Windows 10 pro konkrétní** kolekci obsahuje obecné informace o údržbě Windows 10 pro konkrétní kolekci. Tato sestava ukazuje ID prostředku, název rozhraní NetBIOS, název operačního systému, název verze operačního systému, větev sestavení, větev operačního systému a stav údržby pro zařízení s Windows 10. Další informace najdete v [seznamu sestav](../../servers/manage/list-of-reports.md#operating-system) .



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Ochrana zařízení

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Vylepšení zásad Configuration Manager pro ochranu před zneužitím v programu Windows Defender
<!-- 1356220 -->
Do Configuration Manager pro [ochranu před zneužitím v programu Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction)se přidala další nastavení zásad pro [omezení ploch útoku](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) a [řízené součásti přístupu ke složkám](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) .

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Nastavení interakce nového hostitele pro ochranu Application Guard v programu Windows Defender
<!-- 1356256 -->
Pro zařízení s Windows 10 verze 1709 a novější jsou k dispozici dvě nová nastavení interakce hostitelů pro [ochranu Application Guard v programu Windows Defender](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS): 
- Webům lze udělit přístup k virtuálnímu grafickému procesoru hostitele. 
- Soubory stažené v kontejneru lze zachovat na hostiteli. 




## <a name="configuration-manager-console"></a>Konzola nástroje Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Vylepšení konzoly Configuration Manager 
Tato verze zahrnuje následující vylepšení konzoly Configuration Manager.
- Seznam zařízení v části prostředky a kompatibilita: zařízení teď ve výchozím nastavení zobrazuje primárního uživatele. Tento sloupec se zobrazí pouze v uzlu zařízení. Poslední přihlášený uživatel může být také přidán jako volitelný sloupec.<!-- 1357280 --> Povolit nastavení klienta [spřažení uživatele a zařízení](../../clients/deploy/about-client-settings.md#user-and-device-affinity) pro lokalitu k přidružení primárního uživatele k zařízení.
- Pokud je kolekce členem jiné kolekce a dojde k jejímu přejmenování, nový název se aktualizuje v souladu s pravidly členství.<!--1357282--> 
- Při použití vzdáleného řízení na klientovi s více monitory s různou škálou DPI se ukazatel myši teď mezi nimi mapuje správně. <!--433170-->
- [Řídicí panel pro správu klientů Office 365](../../../sum/deploy-use/office-365-dashboard.md) zobrazuje seznam relevantních zařízení, když jsou vybrány oddíly grafu. <!--1357281 --> 



## <a name="next-steps"></a>Další kroky
Až budete připraveni k instalaci této verze, přečtěte si téma [aktualizace pro Configuration Manager](../../servers/manage/updates.md).
