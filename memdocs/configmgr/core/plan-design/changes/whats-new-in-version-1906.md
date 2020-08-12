---
title: Novinky ve verzi 1906
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1906 Configuration Manager aktuální větve.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 378a5de5633d7a526004d84ec5e6885e165eaadb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128980"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Co je nového ve verzi 1906 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1906 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1802 nebo novější. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Tento článek shrnuje změny a nové funkce v Configuration Manager verze 1906.  

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 1906](../../servers/manage/checklist-for-installing-update-1906.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

> [!Tip]  
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Změny požadavku

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Klient verze 1906 vyžaduje podporu podepisování kódu SHA-2.

<!--SCCMDocs-pr#3404-->
Z důvodu slabých míst v algoritmu SHA-1 a pro zajištění souladu s oborovou normou společnost Microsoft nyní pouze podepisuje Configuration Manager binárních souborů pomocí bezpečnějšího algoritmu SHA-2. Následující verze operačních systémů Windows vyžadují aktualizaci pro podporu podepisování kódu SHA-2:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Další informace najdete v tématu [předpoklady pro klienty se systémem Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infrastruktura webu

### <a name="site-server-maintenance-task-improvements"></a>Vylepšení úloh údržby serveru lokality

<!--3555894-->
Úlohy údržby webového serveru se teď dají zobrazit a upravit ze své vlastní karty v zobrazení podrobností serveru lokality. Na kartě nové **úlohy údržby** se zobrazí následující informace:

- Pokud je úkol povolený
- Plán úlohy
- Čas posledního spuštění
- Čas posledního dokončení
- Pokud byla úloha úspěšně dokončena

![Nová karta pro úlohy údržby v zobrazení podrobností serveru lokality](./media/3555894-maintenance-tasks.png)

Další informace najdete v tématu [úlohy údržby](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906).

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Monitorování upgradu databáze Configuration Manager Update

<!--4200581-->
Při použití aktualizace Configuration Manager se teď můžete podívat na stav úlohy **aktualizace databáze nástroje ConfigMgr** v okně stav instalace.

- Pokud je upgrade databáze zablokován, bude vám docházet k upozorněním, probíhá **, vyžaduje pozornost**.
   - Protokol CMUpdate. log zaznamená název programu a identifikátor SessionID z SQL, který blokuje upgrade databáze.
- Pokud upgrade databáze již není zablokován, bude stav **resetován na hodnotu probíhá nebo** **dokončeno**.
   - Pokud je upgrade databáze zablokován, je tato kontrolu provedena každých 5 minut, aby se zobrazila, zda je stále blokovaná.

   ![Monitorování upgradu databáze během instalace](./media/4200581-database-upgrade-monitoring.png)

Další informace najdete v tématu [instalace konzolových aktualizací](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>Pravidlo správy přehledů pro Fallback protokolu NTLM

<!--4572953-->
Přehledy správy zahrnují nové pravidlo, které zjistí, jestli jste u této lokality povolili metodu pro použití méně zabezpečeného ověřování NTLM: **záloha protokolu NTLM je povolená**.

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>Vylepšení podpory pro SQL Always On

- Přidat novou synchronní repliku z instalačního programu<!--3127336-->: Teď můžete přidat nový uzel sekundární repliky do existující skupiny dostupnosti Always On SQL serveru. Místo ručního procesu použijte Configuration Manager Setup k provedení této změny. Další informace najdete v tématu [Konfigurace skupin dostupnosti Always On SQL Server](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Převzetí služeb při selhání s více podsítěmi<!-- SCCMDocs-pr#3734 -->: Teď můžete povolit [klíčové slovo připojovacího řetězce MultiSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) v SQL Server. Také je nutné ručně nakonfigurovat server lokality. Další informace najdete v tématu věnovaném [převzetí služeb při selhání s více podsítěmi](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) .

- Podpora distribuovaných zobrazení<!-- SCCMDocs-pr#3792 -->: Databáze lokality může být hostována ve skupině dostupnosti Always On SQL Server a můžete povolit odkazy replikace databáze na používání [distribuovaných zobrazení](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep).

    > [!Note]  
    > Tato změna se nevztahuje na SQL Server clustery.

- Site Recovery může znovu vytvořit databázi na skupině SQL Always On. Tento proces funguje s ručním i automatickým osazením.<!-- SCCMDocs-pr#3846 -->

- Nové kontroly požadovaných součástí instalace:<!-- SCCMDocs-pr#3899 -->  

    - Všechny repliky skupin dostupnosti SQL musejí mít stejný režim osazení.
    - Repliky skupin dostupnosti SQL musí být v pořádku.

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Správa připojená ke cloudu

### <a name="azure-active-directory-user-group-discovery"></a>Azure Active Directory zjišťování skupiny uživatelů

<!--3611956-->

Nyní můžete zjišťovat skupiny uživatelů a členy těchto skupin z Azure Active Directory (Azure AD). Uživatelé nalezeni v rámci skupin Azure AD, které ještě nebyly zjištěny, jsou přidány jako prostředky uživatele v Configuration Manager. Záznam prostředku skupiny uživatelů se vytvoří, když je skupina skupinou zabezpečení. Tato funkce je součástí [předběžné verze](../../servers/manage/pre-release-features.md) a musí být povolená.

Další informace najdete v tématu [Konfigurace metod zjišťování](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco).

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Synchronizace výsledků členství kolekce do skupin Azure Active Directory

<!--3607475-->

Nyní můžete povolit synchronizaci členství kolekce do skupiny Azure Active Directory (Azure AD). Tato synchronizace je předběžnou verzí funkce. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../servers/manage/pre-release-features.md).

Synchronizace vám umožní využít vaše stávající místní pravidla seskupení v cloudu vytvořením členství ve skupině Azure AD na základě výsledků členství v kolekci. Ve skupině Azure AD se projeví pouze zařízení se záznamem Azure Active Directory. Podporovaná jsou i zařízení Azure Active Directory připojená k hybridní službě Azure AD.

Další informace najdete v tématu [Vytvoření kolekcí](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync).


## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

### <a name="readiness-insights-for-desktop-apps"></a>Přehledy připravenosti pro desktopové aplikace

<!-- 4021225 -->

Teď můžete získat podrobnější přehled o vašich desktopových aplikacích, včetně obchodních aplikací. Dřívější sada nástrojů pro kontrolu stavu aplikací je teď integrovaná s klientem Configuration Manager. Tato integrace zjednodušuje nasazení a správu přehledů připravenosti aplikací na portálu pro Desktop Analytics.

Další informace najdete v tématu [posouzení kompatibility v Desktop Analytics](../../../desktop-analytics/compat-assessment.md#advanced-insights).


### <a name="dalogscollector-tool"></a>Nástroj DALogsCollector

<!--4622989-->
K řešení potíží s nástrojem Desktop Analytics použijte nástroj DesktopAnalyticsLogsCollector.ps1 z Configuration Manager instalačního adresáře. Spustí se základní kroky pro řešení potíží a shromáždí příslušné protokoly do jednoho pracovního adresáře.

Další informace najdete v tématu [kolektor protokolů](../../../desktop-analytics/log-collector.md).


## <a name="real-time-management"></a><a name="bkmk_real"></a>Správa v reálném čase

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Přidání spojení, dalších operátorů a agregátorů v CMPivot

<!--4054074-->

Pro CMPivot nyní máte další aritmetické operátory, agregátory a možnost přidávat dotazová spojení, jako je například použití registru a souboru dohromady.

Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>CMPivot samostatná

<!--3555890, 4619340, 4692885 -->

CMPivot teď můžete používat jako samostatnou aplikaci. CMPivot Standalone je **funkce předběžného vydání** a je dostupná jenom v angličtině. Spusťte CMPivot mimo konzolu Configuration Manager, abyste zobrazili stav zařízení ve vašem prostředí v reálném čase. Tato změna umožňuje používat CMPivot na zařízení bez první instalace konzoly.

Výkon CMPivot můžete sdílet s ostatními osoby, jako jsou Helpdesk nebo správci zabezpečení, kteří nemají na svém počítači nainstalovanou konzolu. Tyto další osoby můžou použít CMPivot k dotazování Configuration Manager společně s jinými nástroji, které tradičně používají. Sdílením těchto dat s bohatou správou můžete společně proaktivně řešit obchodní problémy, které mezi rolemi pracují.

Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) a [předběžné verze funkcí](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Do role správce zabezpečení se přidala oprávnění.

<!--4683130-->

Do předdefinované role [**Správce zabezpečení**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) Configuration Manager byla přidána následující oprávnění:

- Číst ve skriptu SMS
- Spustit CMPivot pro kolekci
- Číst sestavu inventáře

Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a>Správa obsahu

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Stažení Optimalizace doručení data na řídicím panelu zdrojů dat klienta

<!--3555759-->
Řídicí panel zdroje dat klienta teď obsahuje data [Optimalizace doručení](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) . Tento řídicí panel vám pomůže pochopit, kde klienti získávají obsah ve vašem prostředí.

Další informace najdete v tématu [řídicí panel zdrojů dat klienta](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Použití distribučního bodu jako serveru mezipaměti v síti pro optimalizaci doručení

<!--3555764-->
Nyní můžete v distribučních bodech nainstalovat do serveru mezipaměti v síti možnost optimalizace doručování. Uložením tohoto obsahu do mezipaměti v místním prostředí můžou vaši klienti těžit z funkce Optimalizace doručení, ale můžete přispět k ochraně WAN Links.

Tento server mezipaměti funguje jako transparentní mezipaměť na vyžádání pro obsah stažený optimalizací doručení. Pomocí nastavení klienta se ujistěte, že je tento server nabízen pouze členům místní skupiny hranic Configuration Manager.

Další informace najdete v tématu [optimalizace doručování v síťové mezipaměti v Configuration Manager](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a>Správa klientů

### <a name="support-for-windows-virtual-desktop"></a>Podpora pro virtuální počítače s Windows

<!--3556025-->
[Virtuální plocha Windows](https://docs.microsoft.com/azure/virtual-desktop/) je funkce verze Preview Microsoft Azure a Microsoft 365. Teď můžete pomocí Configuration Manager spravovat tato virtuální zařízení s Windows v Azure.

Podobně jako u terminálového serveru tato virtuální zařízení umožňují více souběžných aktivních uživatelských relací. Kvůli lepšímu výkonu klienta Configuration Manager nyní zakáže zásady uživatele na jakémkoli zařízení, které umožňuje tyto více uživatelských relací. I když zásady uživatele povolíte, klient je ve výchozím nastavení standardně zakáže na těchto zařízeních, která zahrnují virtuální počítače s Windows a Terminálové servery.

Další informace najdete v tématu [podporované verze operačních systémů pro klienty a zařízení](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers).

### <a name="support-center-onetrace-preview"></a>Support Center OneTrace (Preview)

<!--3555962-->
OneTrace je nový prohlížeč protokolů s nástrojem Support Center. Funguje podobně jako CMTrace, s následujícími vylepšeními:

- Zobrazení s kartami
- Ukotvit okna
- Vylepšené možnosti vyhledávání
- Možnost Povolit filtry bez nutnosti opustit zobrazení protokolu
- Tipy pro rychlou identifikaci clusterů s chybami v ScrollBar
- Rychlé otevírání protokolů pro velké soubory

![Snímek obrazovky prohlížeče protokolu OneTrace](./media/3555962-onetrace.png)

Další informace najdete v tématu [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>Konfigurace doby minimálního uchování mezipaměti klienta

<!--4485509-->
Nyní můžete zadat minimální dobu, po kterou může klient Configuration Manager uchovávat obsah v mezipaměti. Toto nastavení klienta definuje minimální dobu Configuration Manager agenta čekat, než bude moci odebrat obsah z mezipaměti v případě, že je potřeba více místa. V části **nastavení mezipaměti klienta** v nastavení klienta nakonfigurujte následující nastavení: **Minimální doba trvání, než bude možné obsah uložený v mezipaměti odebrat (minuty)**.

> [!Note]  
> Ve stejné skupině nastavení klienta je stávající nastavení **povolit Configuration Manager klienta v úplném operačním systému pro sdílení obsahu** teď přejmenované na **Povolit jako zdroj sdílené mezipaměti**. Chování nastavení se nezmění.  

Další informace najdete v tématu [nastavení mezipaměti klienta](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a>Spoluspráva

### <a name="improvements-to-co-management-auto-enrollment"></a>Vylepšení automatického zápisu pro spolusprávu

- Nové spoluspravované zařízení teď automaticky zaregistruje službu Microsoft Intune na základě tokenu *zařízení* Azure Active Directory (Azure AD). Není nutné čekat, než se uživatel přihlásí k zařízení, aby se mohl spustit automatický zápis. Tato změna pomáhá snižovat počet zařízení se [stavem registrace](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *čeká na přihlášení uživatele*.<!-- 4454491 -->

- Pro zákazníky, kteří už mají zařízení zaregistrovaná v rámci společné správy, se teď nová zařízení registrují hned, jakmile splní požadavky. Například když je zařízení připojené ke službě Azure AD a nainstaluje se klient Configuration Manager.<!--4321130-->

Další informace najdete v tématu [Povolení spolusprávy](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Několik pilotních skupin pro úlohy spolusprávy

<!--3555750-->
Pro každou úlohu spolusprávy teď můžete nakonfigurovat různé pilotní kolekce. Používání různých pilotních kolekcí vám umožní podrobnější přístup při posunování zatížení.

- Na kartě **Zapnutí** teď můžete zadat kolekci **automatického zápisu do Intune** .
    - Kolekce **automatického zápisu do Intune** by měla obsahovat všechny klienty, které chcete integrovat do společné správy. Je v podstatě nadmnožinou všech dalších pracovních kolekcí.

- Na kartě **fázování** místo použití jedné pilotní kolekce pro všechny úlohy teď můžete zvolit jednotlivou kolekci pro každou úlohu.

    ![Karta fázování pro spolusprávu umožňuje zvolit kolekci pro každou úlohu.](./media/3555750-co-management-staging-tab.png)

Tyto možnosti jsou k dispozici také při prvním povolení spolusprávy.

Další informace najdete v tématu [Povolení spolusprávy](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Podpora spolusprávy pro státní správu v cloudu

<!--4075452-->
Zákazníci státní správy USA teď můžou používat spolusprávu s cloudem pro státní správu Azure USA (portal.azure.us). Další informace najdete v tématu [Povolení spolusprávy](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a>Správa aplikací

### <a name="filter-applications-deployed-to-devices"></a>Filtrovat aplikace nasazené do zařízení

<!--4451056-->
Kategorie uživatelů pro nasazení aplikací cílené na zařízení se teď zobrazují jako filtry v centru softwaru. Určete **kategorii uživatele** pro aplikaci na stránce **Centrum softwaru** vlastností. Pak otevřete aplikaci v centru softwaru a podívejte se na dostupné filtry.

Další informace najdete v tématu [Ruční zadání informací o aplikaci](../../../apps/deploy-use/create-applications.md#bkmk_manual-app).

### <a name="application-groups"></a>Skupiny aplikací

<!--3555907-->
Vytvořte skupinu aplikací, které můžete odeslat do kolekce uživatelů nebo zařízení jako jediné nasazení. Metadata, která zadáte o skupině aplikací, se zobrazují v centru softwaru jako jediná entita. Aplikace můžete seřadit ve skupině, aby je klient nainstalovaly v určitém pořadí.

Tato funkce je předběžnou verzí. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../servers/manage/pre-release-features.md).

Další informace najdete v tématu [Vytvoření skupin aplikací](../../../apps/deploy-use/create-app-groups.md).

### <a name="retry-the-install-of-pre-approved-applications"></a>Opakovat instalaci předběžně schválených aplikací

<!--4336307-->
Nyní můžete opakovat instalaci aplikace, kterou jste dříve schválili pro uživatele nebo zařízení. Možnost schválení je dostupná jenom pro dostupná nasazení. Pokud uživatel aplikaci odinstaluje nebo dojde k chybě počáteční instalace, Configuration Manager nevyhodnocují svůj stav a znovu ho přeinstalujte. Tato funkce umožňuje technikovi podpory rychle opakovat instalaci aplikace pro uživatele, který volá nápovědu.

Další informace najdete v tématu [schvalování aplikací](../../../apps/deploy-use/app-approval.md).

### <a name="install-an-application-for-a-device"></a>Instalace aplikace pro zařízení

<!--4402180-->
Z konzoly Configuration Manager nyní můžete instalovat aplikace do zařízení v reálném čase. Tato funkce může přispět k omezení nutnosti samostatné kolekce pro každou aplikaci.

Další informace najdete v tématu [instalace aplikací pro zařízení](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Vylepšení pro schválení aplikací

<!--4224910-->
Tato verze zahrnuje následující vylepšení pro schválení aplikací:

- Pokud žádost o aplikaci schválíte v konzole a pak ji odepřete, můžete ji teď schválit znovu. Aplikace se po schválení znovu nainstaluje na klienta.  

- V konzole Configuration Manager v pracovním prostoru **softwarová knihovna** v části **Správa aplikací**se uzel **žádosti o schválení** přejmenuje na **požadavky aplikace**.<!-- SCCMDocs-pr#4028 -->

- Existuje nová metoda WMI, kterou **DeleteInstance** odebrat žádost o schválení aplikace. Tato akce neodinstaluje aplikaci na zařízení. Pokud ještě není nainstalovaná, uživatel nemůže aplikaci nainstalovat z centra softwaru.

- Voláním rozhraní **CreateApprovedRequest** API vytvoříte předběžně schválenou žádost o aplikaci na zařízení. Chcete-li zabránit automatické instalaci aplikace na klienta, nastavte parametr **AutoInstall** na `FALSE` . Uživatel uvidí aplikaci v centru softwaru, ale není automaticky nainstalována.

Další informace najdete v tématu [schvalování aplikací](../../../apps/deploy-use/app-approval.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a>Nasazení operačního systému

### <a name="task-sequence-debugger"></a>Ladicí program pořadí úloh

<!--3612274-->
Ladicí program pořadí úkolů je nový nástroj pro řešení potíží. Pořadí úkolů nasadíte v režimu ladění do kolekce jednoho zařízení. Umožňuje procházet pořadí úkolů řízeným způsobem, který pomáhá řešit problémy a vyšetřování.

![Snímek obrazovky s ladicím programem pořadí úloh](./media/3612274-tsdebug.png)

Tato funkce je předběžnou verzí. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../servers/manage/pre-release-features.md).

Další informace najdete v tématu [ladění pořadí úkolů](../../../osd/deploy-use/debug-task-sequence.md).

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Vymazat obsah aplikace z mezipaměti klienta během pořadí úkolů

<!--4485675-->
V kroku pořadí úkolů **instalovat aplikaci** teď můžete obsah aplikace odstranit z mezipaměti klienta, až se krok spustí.

Další informace najdete v tématu [o krocích pořadí úkolů](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!Important]  
> Aktualizujte cílového klienta na nejnovější verzi, aby podporovala tuto novou funkci.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>Uvolnit SEDO zámek pro pořadí úloh

<!--3699337-->
Pokud konzola Configuration Manager přestane reagovat, můžete se při provádění dalších změn v pořadí úkolů zablokovat. Nyní když se pokusíte o přístup k uzamčenému pořadí úkolů, můžete nyní **zrušit změny**a pokračovat v úpravách objektu.

Další informace najdete v tématu [použití editoru pořadí úloh](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Balíčky ovladačů pro starší mezipaměť a image operačních systémů

<!--4224642-->
Předběžná mezipaměť pořadí úkolů nyní zahrnuje další typy obsahu. Obsah předběžné mezipaměti se dřív používal jenom pro balíčky s upgradem operačního systému. Nyní můžete použít předukládání do mezipaměti a snížit tak spotřebu šířky pásma pro:

- Image operačního systému
- Balíčky ovladačů
- Balíčky

Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>Vylepšení nasazení operačního systému

Tato verze zahrnuje následující vylepšení nasazení operačního systému:

- Pomocí následujících dvou rutin PowerShellu vytvořte a upravte krok [pořadí úkolů Spustit](../../../osd/understand/task-sequence-steps.md#child-task-sequence) :<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Při spuštění pořadí úkolů je teď snazší upravovat proměnné. Po výběru pořadí úkolů v okně Průvodce pořadím úloh obsahuje stránka pro úpravu proměnných pořadí úkolů tlačítko **Upravit** .<!-- 4668846 --> Další informace najdete v tématu [Použití proměnných pořadí úkolů](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz).

- Krok pořadí úkolů **Vypnout nástroj BitLocker** má nový čítač restartování. Tuto možnost použijte, pokud chcete zadat počet restartování, která mají být zakázána nástrojem BitLocker. Tato změna vám pomůže zjednodušit pořadí úloh. Místo přidávání více instancí tohoto kroku můžete použít jeden krok. <!--4512937--> Další informace naleznete v části [Disable BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Použijte novou proměnnou pořadí úloh **SMSTSRebootDelayNext** s existující proměnnou [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) . Pokud chcete, aby pozdější restartování probíhalo s jiným časovým limitem, než je první, nastavte tuto novou proměnnou na jinou hodnotu v sekundách. <!--4447680--> Další informace najdete v tématu [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- Pořadí úkolů nastaví novou **_SMSTSLastContentDownloadLocation**proměnnou jen pro čtení. Tato proměnná obsahuje poslední umístění, kde se pořadí úkolů stáhlo nebo se pokusilo stáhnout obsah. Zkontrolujte tuto proměnnou místo analýzy protokolů klienta.<!-- 2840337 -->

- Při vytváření média pořadí úloh Configuration Manager nepřidá soubor Autorun. inf. Tento soubor je pro antimalwarové produkty často blokovaný. V případě potřeby můžete soubor přesto zahrnout do svého scénáře.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Vylepšení technologie PXE

Možnost 82 během ověřování PXE DHCP se teď podporuje s respondérem PXE bez služby WDS. Možnost 82 není u služby WDS podporována.


## <a name="software-center"></a><a name="bkmk_userxp"></a>Centrum softwaru

### <a name="improvements-to-software-center-tab-customizations"></a>Vylepšení přizpůsobení karty centra softwaru

<!--4063773-->
V centru softwaru teď můžete přidat až pět vlastních karet. Můžete také upravit pořadí, ve kterém se tyto karty zobrazují v centru softwaru.

Další informace najdete v tématu [nastavení klienta centra softwaru](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Vylepšení infrastruktury centra softwaru

<!--3555950-->

Tato verze zahrnuje následující vylepšení infrastruktury pro software Center:

- Centrum softwaru nyní komunikuje s bodem správy pro aplikace cílené na uživatele jako dostupné. Katalog aplikací už nepoužívá. Tato změna usnadňuje odebrání katalogu aplikací z lokality nástroje.

- Dříve Centrum softwaru vybralo první bod správy ze seznamu dostupných serverů. Od této verze používá stejný bod správy, který klient používá. Tato změna umožňuje centru softwaru použít stejný bod správy z přiřazené primární lokality jako klienta.

> [!Important]  
> Tato iterativní vylepšení centra softwaru a bodu správy slouží k vyřazení rolí katalogu aplikací.
>
> - Uživatelské prostředí Silverlight není pro aktuální větev verze 1806 podporováno.
> - Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací.
> - Podpora končí pro role katalogu aplikací s verzí 1910.  

Další informace najdete v tématu [Odebrání katalogu aplikací](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) a [plánování centra softwaru](../../../apps/plan-design/plan-for-software-center.md).

### <a name="redesigned-notification-for-newly-available-software"></a>Nové navržené oznámení pro nově dostupný software

<!--3555904-->
**K dispozici je nový software** oznámení se zobrazí jenom jednou pro uživatele zadané aplikace a revize. Uživatel se už nebude zobrazovat oznámení pokaždé, když se přihlásí. Uvidí jenom další oznámení o aplikaci, pokud se změnila nebo byla znovu nasazena.

Další informace najdete v tématu [Vytvoření a nasazení aplikace](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Častější odpočítávání oznámení pro restartování

<!--3976435-->

Koncovým uživatelům se nyní bude v případě občasného odpočítávání oznámení zobrazovat častěji než na restartování. Můžete definovat interval pro přerušovaná oznámení v **nastavení klienta** na stránce **restart počítače** . Změňte hodnotu pro **zadání doby opakovaného přiložení pro odpočítávání pro restartování počítače (minuty)** , abyste nakonfigurovali, jak často bude uživatel upozorněn na nedokončené restartování, dokud neproběhne konečné oznámení o odpočítávání.

Maximální hodnota pro **zobrazení dočasného oznámení uživateli, které určuje interval před odhlášením uživatele nebo restartováním počítače (minuty)** se zvýšila z 1440 minut (24 hodin) až 20160 minut (dva týdny).

Další informace najdete v tématu [oznámení o restartování zařízení](../../clients/deploy/device-restart-notifications.md) a [o nastavení klienta](../../clients/deploy/about-client-settings.md#computer-restart).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Přímý odkaz na vlastní karty v centru softwaru

<!--4655176-->

Nyní můžete uživatelům poskytnout přímý odkaz na [vlastní kartu](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) v centru softwaru.

Pomocí následujícího formátu adresy URL otevřete Centrum softwaru na konkrétní kartu:

`softwarecenter:page=CustomTab1`

Řetězec `CustomTab1` je první vlastní karta v daném pořadí.

Zadejte například tuto adresu URL v okně **spuštění** systému Windows.

Tuto syntaxi můžete použít také k otevření výchozích karet v centru softwaru:

|Příkazový řádek  |Karta  |
|---------|---------|
|`AvailableSoftware`|Aplikace|
|`Updates`|Aktualizace|
|`OSD`|Operační systémy|
|`InstallationStatus`|Stav instalace|
|`Compliance`|Dodržování předpisů zařízení|
|`Options`|Možnosti|

Další informace najdete v tématu [viditelnost karty centra softwaru](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a>Aktualizace softwaru

### <a name="additional-options-for-wsus-maintenance"></a>Další možnosti údržby služby WSUS

<!--4110109-->
Nyní máte další úlohy údržby služby WSUS, které mohou Configuration Manager spustit za účelem zachování zdravých bodů aktualizace softwaru. Údržba služby WSUS probíhá po každé synchronizaci. Kromě odmítnutí aktualizací s vypršenou platností ve službě WSUS teď Configuration Manager možné:

- Odeberte zastaralé aktualizace z databáze WSUS.
- Přidáním neclusterovaných indexů do databáze WSUS můžete zlepšit výkon vyčištění služby WSUS.

Další informace najdete v tématu [Údržba aktualizací softwaru](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906).

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Konfigurovat výchozí maximální dobu běhu pro aktualizace softwaru

<!--3734426-->

Nyní můžete zadat maximální dobu, po kterou musí být instalace aktualizace softwaru dokončena. Na kartě **Maximální doba běhu** v bodě aktualizace softwaru můžete zadat následující položky:

- **Maximální doba běhu pro aktualizace funkcí Windows (minuty)**
- **Maximální doba běhu pro aktualizace Office 365 a aktualizace bez funkcí pro Windows (minuty)**

Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### <a name="configure-dynamic-update-during-feature-updates"></a>Konfigurace dynamické aktualizace během aktualizací funkcí

<!--4062619-->

Pomocí nového nastavení klienta nakonfigurujte [dynamickou aktualizaci](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) při instalaci aktualizací funkcí Windows 10. Dynamická aktualizace instaluje jazykové sady, funkce na vyžádání, ovladače a kumulativní aktualizace během instalace systému Windows nasměrováním klienta na stažení těchto aktualizací z Internetu.

Další informace najdete v tématu [nastavení klienta aktualizace softwaru](../../clients/deploy/about-client-settings.md#software-updates) a [Správa Windows jako služby](../../../osd/deploy-use/manage-windows-as-a-service.md).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Nová kategorie produktů Windows 10, verze 1903 a novější

<!--4682946-->

**Windows 10 verze 1903 a novější** se přidala do Microsoft Update jako vlastní produkt, a ne jako součást produktu **Windows 10** , jako je třeba předchozí verze. Tato změna způsobila, že provedete několik ručních kroků, abyste zajistili, že se tyto aktualizace zobrazí u klientů. Pomohl vám snížit počet ručních kroků, které je třeba provést pro nový produkt.

Když aktualizujete na Configuration Manager verze 1906 a produkt **Windows 10** je vybraný pro synchronizaci, automaticky se provedou následující akce:

- Pro synchronizaci se přidá **Windows 10 verze 1903 a novější** .
- Pravidla automatického nasazení obsahující produkt **Windows 10** se budou aktualizovat tak, aby zahrnovala **Windows 10, verze 1903 a novější**.
- Plány údržby se aktualizují tak, aby zahrnovaly **Windows 10, verze 1903 a novější** produkt.

Další informace najdete v tématu [Konfigurace klasifikací a produktů pro synchronizaci](../../../sum/get-started/configure-classifications-and-products.md), [plány údržby](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)a [pravidla automatického nasazení](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

### <a name="drill-through-required-updates"></a>Podrobné informace o požadovaných aktualizacích

<!--4224414-->
Nyní můžete procházet statistiky dodržování předpisů a zjistit, která zařízení vyžadují určitou aktualizaci softwaru. Chcete-li zobrazit seznam zařízení, potřebujete oprávnění k zobrazení aktualizací a kolekcí, do kterých zařízení patří. Chcete-li přejít k podrobnostem v seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu na kartě **Souhrn** aktualizace. Kliknutím na hypertextový odkaz přejdete na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci.

Hypertextový odkaz **požadovaný zobrazení** je k dispozici v následujících umístěních:

   - **Softwarová knihovna**  >  **Aktualizace softwaru**  >  **Všechny aktualizace softwaru**
   - **Softwarová knihovna**  >  **Údržba**  >  Windows 10 **Všechny aktualizace Windows 10**
   - **Softwarová knihovna**  >  Správa klientů Office **365**  >  **Aktualizace Office 365**

Další informace najdete v tématech [monitorování aktualizací softwaru](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates), [Správa Windows jako služby](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)a [Správa aktualizací Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


## <a name="office-management"></a><a name="bkmk_o365"></a>Správa Office

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Řídicí panel připravenosti na upgrade pro Office 365 ProPlus

<!--4021125-->

Abychom vám pomohli určit, která zařízení jsou připravená k upgradu na Office 365 ProPlus, je k dispozici nový řídicí panel připravenosti. Zahrnuje dlaždici **připravenosti na upgrade sady Office 365** , která byla vydaná ve Configuration Manager aktuální verze větve 1902. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **správa klientů Office 365**a vyberte uzel **Office 365 ProPlus upgrade Readiness** .

Další informace o řídicím panelu, požadavcích a používání těchto dat najdete v tématu [integrace pro Office 365 ProPlus Readiness](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a>Antivirový

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Kritéria vztahu důvěryhodnosti souborů ochrany Application Guard v programu Windows Defender

<!--3555858-->

K dispozici je nové nastavení zásad, které uživatelům umožňuje důvěřovat souborům, které jsou normálně otevřené v ochraně Application Guard v programu Windows Defender (WDAG). Po úspěšném dokončení se soubory otevřou na hostitelském zařízení, nikoli v WDAG.

Další informace najdete v tématu [Vytvoření a nasazení zásad ochrany Application Guard v programu Windows Defender](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Konzola Configuration Manager

### <a name="role-based-access-for-folders"></a>Přístup na základě rolí pro složky

<!--3600867-->

Pro složky teď můžete nastavit obory zabezpečení. Pokud máte přístup k objektu ve složce, ale nemáte přístup ke složce, nebudete moct objekt zobrazit. Podobně platí, že pokud máte přístup do složky, ale ne do objektu, neuvidíte tento objekt. Klikněte pravým tlačítkem myši na složku, zvolte možnost **nastavit rozsahy zabezpečení**a pak zvolte rozsahy zabezpečení, které chcete použít.

Další informace najdete v tématech [Configuration Manager tipů pro konzolu](../../servers/manage/admin-console-tips.md) a [Konfigurace správy na základě rolí](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder).

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Přidat sloupec SMBIOS GUID do uzlů kolekce zařízení a zařízení

<!--4526580-->
V uzlech kolekce **zařízení** a **zařízení** teď můžete přidat nový sloupec pro **identifikátor SMBIOS GUID**. Tato hodnota je stejná jako vlastnost **GUID systému BIOS** třídy systémového prostředku. Je to jedinečný identifikátor hardwaru zařízení.

### <a name="administration-service-support-for-security-nodes"></a>Podpora služeb správy pro uzly zabezpečení

<!--4223683-->
Nyní můžete povolit některé uzly konzoly Configuration Manager pro použití služby správy. Tato změna umožňuje konzole komunikovat s poskytovatelem serveru SMS přes protokol HTTPS místo přes rozhraní WMI.

Další informace najdete v tématu [Služba pro správu](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).

> [!Note]
> Počínaje verzí 1906 se nyní karta **komunikace s klientským počítačem** ve vlastnostech lokality nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Karta kolekce v uzlu zařízení

<!--4616810-->
V pracovním prostoru **prostředky a kompatibilita** , přejít na uzel **zařízení** a vyberte zařízení. V podokně podrobností přepněte na kartu nové **kolekce** . Tato karta obsahuje seznam kolekcí, které zahrnují toto zařízení.

> [!Note]  
> - Tato karta není momentálně k dispozici v poduzlu zařízení v uzlu **kolekce zařízení** . Například když vyberete možnost **zobrazení členů** v kolekci.
> - Tato karta se pro některé uživatele nemusí naplnit očekávaným způsobem. Úplný seznam kolekcí, do kterých zařízení patří, zobrazíte tak, že musíte mít roli zabezpečení **správce s úplnými oprávněními** . Jedná se o známý problém. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Karta pořadí úloh v uzlu aplikace

<!--4616810-->
V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**, pak přejít do uzlu **aplikace** a vyberte aplikaci. V podokně podrobností přepněte na kartu nové **pořadí úkolů** . Tato karta obsahuje pořadí úloh, která odkazují na tuto aplikaci.

### <a name="show-collection-name-for-scripts"></a>Zobrazit název kolekce pro skripty

<!--4616810-->
V pracovním prostoru **monitorování** vyberte uzel **stav skriptu** . Kromě ID teď obsahuje i **název kolekce** .

### <a name="real-time-actions-from-device-lists"></a>Akce ze seznamů zařízení v reálném čase

<!--4616810-->
Existují různé způsoby, jak zobrazit seznam zařízení v uzlu **zařízení** v pracovním prostoru **prostředky a kompatibilita** .

- V pracovním prostoru **prostředky a kompatibilita** vyberte uzel **kolekce zařízení** . Vyberte kolekci zařízení a zvolte akci pro **zobrazení členů**. Tato akce otevře dílčí uzel uzlu **zařízení** se seznamem zařízení pro tuto kolekci.  

  - Když vyberete dílčí uzel kolekce, můžete nyní začít **CMPivot** ze skupiny kolekcí na pásu karet.  

- V pracovním prostoru **monitorování** vyberte uzel **nasazení** . Vyberte nasazení a na pásu karet zvolte akci **Zobrazit stav** . V podokně Stav nasazení dvakrát klikněte na celkový počet assetů, aby bylo možné přejít k seznamu zařízení.  

  - Když v tomto seznamu vyberete zařízení, teď můžete začít **CMPivot** a **spouštět skripty** ze skupiny zařízení na pásu karet.  

### <a name="order-by-program-name-in-task-sequence"></a>Seřadit podle názvu programu v pořadí úkolů

<!--4616810-->
V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** . Upravte pořadí úkolů a vyberte nebo přidejte krok [instalovat balíček](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) . Pokud má balíček více než jeden program, rozevírací seznam nyní Seřadí programy abecedně.

### <a name="correct-names-for-client-operations"></a>Správné názvy pro klientské operace

<!--4616810-->
V pracovním prostoru **monitorování** vyberte **operace klientů**. Operace **Přepnutí na další bod aktualizace softwaru** je nyní správně pojmenována.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a>Zastaralé funkce a operační systémy

Přečtěte si o změnách podpory před jejich implementací v [odebraných a zastaralých položkách](deprecated/removed-and-deprecated.md).

Verze 1906 vyřazuje podporu pro následující funkce:  

- Nemůžete instalovat nové role katalogu aplikací. Aktualizovaní klienti automaticky používají bod správy pro nasazení aplikací, která jsou k dispozici pro uživatele. Další informace najdete v tématu [plánování centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

Verze 1906 zastaralá o podporu pro následující produkty:  

- Systém Windows CE 7,0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Další aktualizace

Od této verze již nejsou k dispozici následující funkce předběžného vydání:

- [Služba pro správu poskytovatele serveru SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Správa Řízení aplikací v programu Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1906](https://support.microsoft.com/help/4514258).

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell verze 1906](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps).

V konzole nástroje je k dispozici následující kumulativní aktualizace (4517869) od 1. října 2019: [kumulativní aktualizace pro Configuration Manager aktuální větev, verze 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Další kroky

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
Od 16. srpna 2019 je verze 1906 k dispozici pro všechny zákazníky, kteří chtějí instalovat.

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.  
>
> Přečtěte si další informace:
>
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)  

Známé a významné problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).
