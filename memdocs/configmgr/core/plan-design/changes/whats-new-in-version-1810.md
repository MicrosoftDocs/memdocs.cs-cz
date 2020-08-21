---
title: Novinky ve verzi 1810
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1810 Configuration Manager aktuální větve.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 04630815b3d10a232d7fc0eea50296062c823194
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699836"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Co je nového ve verzi 1810 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1810 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1710, 1802 nebo 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> Tento článek shrnuje změny a nové funkce v Configuration Manager verze 1810.  

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 1810](../../servers/manage/checklist-for-installing-update-1810.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).

Pokud chcete využívat nové funkce Configuration Manager, nejdřív aktualizujte klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Zastaralé funkce a operační systémy

Přečtěte si o změnách podpory před jejich implementací v [odebraných a zastaralých položkách](deprecated/removed-and-deprecated.md).

Od 14. srpna 2018 je funkce hybridní správy mobilních zařízení zastaralá. Další informace najdete v tématu [co se stalo s hybridní MDM](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

Podpora pro System Center Endpoint Protection (SCEP) pro Mac a Linux (všechny verze) končí 31. prosince 2018. Dostupnost nových definic virů pro SCEP pro Mac a SCEP pro Linux se může po skončení podpory přestat používat. Další informace najdete v [příspěvku blogu konec podpory](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).

Nasazení klasických služeb v Azure je teď v Configuration Manager zastaralá. Začněte používat Azure Resource Manager nasazení pro bránu pro správu cloudu a distribuční bod cloudu. Další informace najdete v tématu [plánování pro CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruktura webu

### <a name="support-for-windows-server-2019"></a>Podpora pro Windows Server 2019

<!--1359195-->
Configuration Manager teď podporuje Windows Server 2019 a Windows Server, verze 1809, jako systémy lokality.

Další informace najdete v tématu [podporované operační systémy pro servery systému lokality](../configs/supported-operating-systems-for-site-system-servers.md).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Podpora hierarchie pro vysokou dostupnost serveru lokality

<!--3607755, fka 1358224-->
Lokality centrální správy a podřízené primární lokality teď mohou mít další server lokality v pasivním režimu.

Další informace najdete v tématu [Vysoká dostupnost serveru lokality](../../servers/deploy/configure/site-server-high-availability.md).


### <a name="improvements-to-setup-prerequisites"></a>Vylepšení požadavků na instalaci

Když nainstalujete nebo aktualizujete verzi 1810, Configuration Manager instalační program nyní zahrnuje nebo vylepšuje následující kontroly požadovaných součástí:

- **Čeká se na restartování systému**: Tato kontrola požadavků je teď pružnější. Kontroluje další klíče registru pro funkce Windows. Další informace najdete v tématu [čekání na restart systému](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Vyčištění sledování změn SQL**: novou kontrolu, jestli má databáze lokality nevyřízené položky dat sledování změn SQL. Další informace, včetně postupu pro ověření a vymazání těchto nevyřízených položek, najdete v tématu [Vyčištění sledování změn SQL](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client verze**: Tato kontrola požadavků je aktualizovaná pro verze SQL Native Client, které podporují protokol TLS 1,2. Minimální verze je [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Další informace najdete v tématu [SQL Native Client verze](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Systém lokality na uzlu clusteru Windows**: proces instalace Configuration Manager již neblokuje instalaci role serveru lokality do počítače s rolí Windows pro clusteringu s podporou převzetí služeb při selhání. SQL Always On vyžaduje tuto roli, takže dříve se nepovedlo společně najít databázi lokality na serveru lokality. Díky této změně můžete vytvořit vysoce dostupnou lokalitu s menším počtem serverů pomocí SQL Always On a serveru lokality v pasivním režimu. Další informace najdete v tématu [cluster Windows s podporou převzetí služeb při selhání](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster). <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>Nové oprávnění pro akce klientských oznámení

<!--SCCMDocs-pr issue #2972-->
Akce oznámení klienta nyní vyžadují oprávnění **oznámit prostředek** pro třídu SMS_Collection. Následující předdefinované role mají toto oprávnění ve výchozím nastavení:

- Správce s úplnými oprávněními  
- Správce infrastruktury  

Toto oprávnění přidejte do všech vlastních rolí, které potřebují používat akce klientských oznámení.

Další informace najdete v tématu [oznámení klienta](../../clients/manage/client-notification.md).



## <a name="content-management"></a><a name="bkmk_content"></a> Správa obsahu

### <a name="new-boundary-group-options"></a>Nové možnosti skupiny hranic

<!--1358749-->
Skupiny hranic teď obsahují následující dodatečná nastavení, která vám poskytnou větší kontrolu nad distribucí obsahu ve vašem prostředí:

- **Preferovat distribuční body přes partnerské uzly se stejnou podsítí**: ve výchozím nastavení určuje bod správy prioritu zdrojů sdílené mezipaměti v horní části seznamu umístění obsahu. Toto nastavení obrátí prioritu u klientů, kteří jsou ve stejné podsíti jako zdroj sdílené mezipaměti.  

- **Preferovat cloudové distribuční body prostřednictvím distribučních bodů**: Pokud máte pobočku s rychlejším internetovým propojením, můžete nyní nastavit prioritu cloudového obsahu.  

Další informace najdete v tématu [Možnosti hraniční skupiny pro rovnocenné soubory ke stažení](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Pravidlo služby Management Insights pro verzi klienta sdílené mezipaměti

<!-- 1358008 -->
Uzel **Management Insights** má nové pravidlo pro identifikaci klientů, kteří slouží jako zdroj sdílené mezipaměti, ale nebyl upgradován z verze klienta starší než 1806. Nové pravidlo provádí **upgrade zdrojů sdílené mezipaměti na nejnovější verzi klienta Configuration Manager**a je součástí nové skupiny pravidel **proaktivní údržby** . Klienty starších než 1806 nelze použít jako zdroj sdílené mezipaměti pro klienty, kteří používají verzi 1806 nebo novější. Výběrem možnosti **provést akci** otevřete zobrazení zařízení, které zobrazí seznam klientů.

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md).



## <a name="client-management"></a><a name="bkmk_client"></a> Správa klientů

### <a name="new-client-notification-action-to-wake-up-device"></a>Nová akce oznámení klienta pro probuzení zařízení

<!--1317364-->
Nyní můžete probudit klienty z konzoly Configuration Manager, i když klient není ve stejné podsíti jako server lokality. Pokud potřebujete provést údržbu nebo dotazování na zařízení, nebudete omezeni vzdálenými klienty, kteří jsou v režimu spánku. Webový server používá kanál oznámení klienta k identifikaci jiného klienta, který běží ve stejné vzdálené podsíti. Klient v režimu spánku pak pošle požadavek Wake on LAN (Magic Packet).

Další informace najdete v tématu [Konfigurace funkce Wake on LAN](../../clients/deploy/configure-wake-on-lan.md) a [postup probuzení klientů](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nová možnost pro provádění klientských oznámení z uzlu zařízení

<!--1317364-->
Až do 1810, možnost **oznámení klienta** byla dostupná jenom z uzlu kolekce zařízení nebo když jste zobrazili členství v kolekci zařízení. Nyní je možné provést **klientské oznámení** přímo z uzlu **zařízení** . Už nemusíte mít v zobrazení členství v kolekci žádné požadavky.

Další informace najdete v tématu [oznámení klienta](../../clients/manage/client-notification.md).


### <a name="improvements-to-collection-evaluation"></a>Vylepšení vyhodnocování kolekcí

<!--3607726, fka 1358981-->
Následující změny v chování při vyhodnocování kolekce můžou zlepšit výkon webu:  

- Pokud jste dřív nakonfigurovali plán pro kolekci založenou na dotazech, bude lokalita i nadále vyhodnocovat dotaz bez ohledu na to, jestli jste povolili nastavení kolekce **naplánovat úplnou aktualizaci této kolekce**. K úplnému zakázání plánu jste museli změnit plán na **žádný**. Když teď toto nastavení zakážete, tento web zruší plán. Chcete-li zadat plán pro vyhodnocení kolekce, povolte možnost **naplánovat úplnou aktualizaci v této kolekci**.  

- Nemůžete zakázat vyhodnocení předdefinovaných kolekcí, jako jsou **všechny systémy**, ale teď můžete plán nakonfigurovat. Toto chování umožňuje přizpůsobit tuto akci v době, kdy vyhovuje vašim obchodním požadavkům.

Další informace najdete v tématu [vytváření kolekcí](../../clients/manage/collections/create-collections.md#bkmk_create).


### <a name="improvement-to-client-installation"></a>Vylepšení klientské instalace

<!--1358840-->
Při instalaci klienta Configuration Manager se proces CCMSetup spojí s bodem správy, aby vyhledal potřebný obsah. Bod správy dříve v tomto procesu vrátí pouze distribuční body v aktuální skupině hranic klienta. Pokud není k dispozici žádný obsah, proces instalace přejde zpět na stažení obsahu z bodu správy. Neexistuje žádný způsob, jak vrátit zpět do distribučních bodů v jiných skupinách hranic, které by mohly mít potřebný obsah. Bod správy nyní vrací distribuční body na základě konfigurace hraniční skupiny.

Další informace najdete v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup).



## <a name="co-management"></a><a name="bkmk_comgmt"></a> Spoluspráva

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Požadované zásady dodržování předpisů aplikací pro společně spravovaná zařízení

<!--1358196-->
Definujte pravidla zásad dodržování předpisů v Configuration Manager pro požadované aplikace. Toto posouzení aplikace je součástí celkového stavu dodržování předpisů odesílaného Microsoft Intune pro spoluspravovaná zařízení.

Další informace najdete v tématu [úlohy spolusprávy](../../../comanage/workloads.md).


### <a name="improvement-to-co-management-dashboard"></a>Vylepšení řídicího panelu spolusprávy

<!--1358980-->
Řídicí panel spolusprávy je vylepšený pomocí následujících podrobnějších informací:  

- Dlaždice **stavu registrace spolusprávy** zahrnuje další stavy.

- Nová dlaždice **stavu spolusprávy** s trychtýřovým grafem zobrazuje stavy procesu registrace.

- Nová dlaždice s počty **chyb registrace**

![Snímek obrazovky s řídicím panelem pro spolusprávu zobrazující horní čtyři dlaždice](media/1358980-comgmt-dashboard.png)

Další informace najdete v tématu [řídicí panel pro spolusprávu](../../../comanage/how-to-monitor.md#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Vylepšení internetového nastavení klientů

<!--3607731, fka 1359181-->
Tato verze dále zjednodušuje proces instalace klienta Configuration Manager klientů na internetu. Lokalita publikuje Další informace Azure Active Directory (Azure AD) do brány pro správu cloudu (CMG). Klient připojený ke službě Azure AD získá tyto informace z CMG během procesu CCMSetup pomocí stejného tenanta, ke kterému je připojený. Toto chování dále zjednodušuje registraci zařízení do spolusprávy v prostředí s více než jedním klientem služby Azure AD. Nyní jsou pouze dvě požadované vlastnosti CCMSetup **CCMHOSTNAME** a **SMSSiteCode**.

Další informace najdete v tématu [Příprava internetových zařízení pro spolusprávu](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).



## <a name="application-management"></a><a name="bkmk_app"></a> Správa aplikací

### <a name="convert-applications-to-msix"></a>Převést aplikace na MSIX

<!--3607729, fka 1359029-->
Počínaje verzí 1806 podporuje Configuration Manager nasazení nového formátu balíčku aplikace pro Windows 10 (. msix). Nyní můžete převést stávající aplikace Instalační služba systému Windows (. msi) na formát MSIX.

Další informace najdete v tématu [vytváření aplikací pro Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).  


### <a name="repair-applications"></a>Opravit aplikace

<!--1357866-->
Zadejte příkazový řádek opravy pro Instalační služba systému Windows a typy nasazení instalačního programu skriptů. Pokud povolíte možnost nasazení, je v centru softwaru k dispozici nové tlačítko k **opravě** aplikace. Když nakonfigurujete aplikaci pomocí opravného programu, uživatelé mohou spustit příkaz z centra softwaru.

Další informace najdete v tématu [vytváření aplikací](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) a [nasazení aplikací](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Schvalování žádostí o aplikace přes e-mail

<!--1321550-->
Nakonfigurujte e-mailová oznámení pro žádosti o schválení aplikace. Když uživatel požádá o aplikaci, obdržíte e-mail. Kliknutím na odkazy v e-mailu schválíte nebo odepřete žádost, aniž byste museli konzolu Configuration Manager.

Další informace najdete v tématu [schvalování aplikací](../../../apps/deploy-use/app-approval.md).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Metody detekce nenačte profily Windows PowerShellu.

<!--3607762, fka 1359239-->
Pro metody detekce aplikací a nastavení v položkách konfigurace můžete použít skripty prostředí Windows PowerShell. Když tyto skripty běží na klientech, Configuration Manager klient nyní volá PowerShell s `-NoProfile` parametrem. Tato možnost spustí PowerShell bez profilů.

Profil PowerShellu je skript, který se spustí při spuštění PowerShellu. Můžete vytvořit profil PowerShellu pro přizpůsobení prostředí a přidání prvků specifických pro relaci do každé relace prostředí PowerShell, kterou spustíte.

> [!Note]  
> Tato změna chování se nevztahuje na [skripty](../../../apps/deploy-use/create-deploy-scripts.md) nebo [CMPivot](../../servers/manage/cmpivot.md). Obě tyto funkce už tento parametr PowerShellu používají.  

Další informace najdete v tématech o [vytváření aplikací](../../../apps/deploy-use/create-applications.md) a [vytváření vlastních položek konfigurace](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).



## <a name="os-deployment"></a><a name="bkmk_osd"></a> Nasazení operačního systému

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Podpora pořadí úkolů pro existující zařízení ve Windows autopilotu

<!--3607717, fka 1358333-->
[Windows autopilot pro stávající zařízení](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) je teď k dispozici ve Windows 10 verze 1809 nebo novější. Tato nová funkce umožňuje obnovení image a zřízení zařízení se systémem Windows 7 pro [uživatele se systémem Windows autopilot na základě](/windows/deployment/windows-autopilot/user-driven) jednoho nativního Configuration Managerho pořadí úloh.

Další informace najdete v tématu [Windows Autopilot pro existující zařízení](../../../../autopilot/existing-devices.md).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Zadejte jednotku pro obsluhu bitové kopie operačního systému offline

<!--1358924-->
Nyní zadejte jednotku, kterou Configuration Manager používá při přidávání aktualizací softwaru do imagí operačních systémů a balíčků s upgradem operačního systému. Tento proces může využívat velké množství místa na disku s dočasnými soubory, takže tato možnost nabízí flexibilitu pro výběr jednotky, která se má použít.

Další informace najdete v tématech [Správa imagí operačního systému](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) nebo [Správa balíčků s upgradem operačního systému](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Podpora pořadí úkolů pro skupiny hranic

<!--1359025-->
Když zařízení spustí pořadí úkolů a potřebuje získat obsah, použije se chování skupiny hranic podobné jako u klienta Configuration Manager.

Další informace najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Vylepšení údržby ovladačů

<!--3607716, fka 1358270-->
Balíčky ovladačů teď mají další pole metadat pro **výrobce** a **model**. Pomocí těchto polí můžete označit balíčky ovladačů informacemi, které vám pomůžou všeobecně údržbu, nebo identifikovat staré a duplicitní ovladače, které můžete odstranit.

Další informace najdete v tématu [Správa ovladačů](../../../osd/get-started/manage-drivers.md).

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Vylepšení filtrů plánů údržby Windows 10

<!--3098809, 3113836, 3204570 -->
Do plánů údržby Windows 10 se přidaly další filtry. Nyní můžete filtrovat podle **architektury**, **kategorie produktu**a v případě, že je upgrade **nahrazen**.

Další informace najdete v tématu [plán údržby Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan).

### <a name="new-task-sequence-variable-for-last-action-name"></a>Nová proměnná pořadí úloh pro název poslední akce

<!--SCCMDocs-pr issue #2964-->
Spolu s proměnnou pořadí úloh _SMSTSLastActionRetCode také pořadí úkolů nastaví novou proměnnou **_SMSTSLastActionName**. Tato hodnota se také zaznamená do souboru souboru Smsts. log. Tato nová proměnná je při odstraňování potíží s pořadím úkolů prospěšná. V případě neúspěchu kroku může vlastní skript zahrnovat název kroku spolu s návratovým kódem.

Další informace najdete v tématu [proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName).



## <a name="software-updates"></a><a name="bkmk_sum"></a> Aktualizace softwaru

### <a name="phased-deployment-of-software-updates"></a>Dvoufázové nasazení aktualizací softwaru

<!--1358146-->
Vytvoření postupného nasazení pro aktualizace softwaru. Postupné nasazení vám umožní orchestrovat koordinované, sekvenční zavedení softwaru na základě přizpůsobitelných kritérií a skupin.

Další informace najdete v tématu [Vytvoření dvoufázové nasazení](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Zlepšení oken údržby pro aktualizace softwaru

<!--vso2839307-->
Následující nastavení klienta se nachází ve skupině **aktualizace softwaru** , která řídí chování při instalaci aktualizací softwaru v oknech údržby: **Povolit instalaci aktualizací v časovém intervalu pro správu všech nasazení, když je k dispozici okno Údržba aktualizace softwaru** .

Ve výchozím nastavení je tato možnost **ne** , aby zůstala v souladu s existujícím chováním. Změňte na **Ano** , pokud chcete, aby klienti mohli k instalaci aktualizací softwaru používat jiné dostupné časové intervaly pro správu a údržbu.

Další informace najdete v tématu [nastavení klienta pro aktualizace softwaru](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint).


### <a name="improvement-to-software-updates-maintenance"></a>Zlepšení údržby aktualizací softwaru

<!--2839349-->
Úlohy čištění služby WSUS se nyní spouštějí v sekundárních lokalitách. Aktualizace služby WSUS pro aktualizace s vypršenou platností se spouští a nahrazené aktualizace jsou ve službě WSUS pro sekundární lokality odmítnuty.

Další informace najdete v tématu [chování služby WSUS Cleanup počínaje verzí 1810](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810) .

### <a name="improvement-to-software-update-supersedence-rules"></a>Vylepšení pravidel nahrazení aktualizací softwaru

<!--3098809, 2977644-->
Pro aktualizace funkcí teď můžete zadat pravidla nahrazení odděleně od aktualizací bez funkcí. To znamená, že před dokončením údržby klientů s Windows 10 nebudou upgrady z Configuration Manager odebrány.

Další informace najdete v části [Pravidla nahrazení](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules).

## <a name="reporting"></a><a name="bkmk_report"></a> Zpravodajský

### <a name="improvement-to-lifecycle-dashboard"></a>Vylepšení řídicího panelu životní cyklus

<!--1358702-->
Řídicí panel životní cyklus produktu teď obsahuje informace pro **System Center 2012 Configuration Manager a novější**.

K dispozici je také Nová sestava **05A životní cyklus – pracovní cyklus životního cyklu produktu**. Obsahuje podobné informace jako na řídicím panelu v konzole.

Další informace o tomto řídicím panelu najdete v tématu [Použití řídicího panelu životního cyklu produktu](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="improvement-to-data-warehouse"></a>Zlepšení datového skladu

<!--1358870-->
Nyní můžete synchronizovat více tabulek z databáze lokality do datového skladu. Tato změna vám umožní vytvořit další sestavy založené na vašich obchodních požadavcích.

Další informace najdete v tématu [datový sklad](../../servers/manage/data-warehouse.md).



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Konzola Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Ověřování správce Configuration Manager

<!--1357013-->
Nyní můžete zadat minimální úroveň ověřování pro správce pro přístup k Configuration Manager lokalit. Tato funkce vynutila správcům přihlášení k systému Windows s požadovanou úrovní. Pokud chcete nakonfigurovat toto nastavení, najděte kartu **ověřování** v **Nastavení hierarchie**.

Další informace najdete v tématu [plánování poskytovatele serveru SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).


### <a name="support-center"></a>Support Center

<!--1357489-->
Použijte Support Center pro řešení potíží s klientem, zobrazení protokolu v reálném čase nebo zachycení stavu Configuration Manager klientského počítače pro pozdější analýzu. Support Center je jediným nástrojem ke zkombinování mnoha nástrojů pro odstraňování potíží správců. Vyhledejte instalační program centra pro podporu na serveru lokality ve složce **CD. latest\SMSSETUP\Tools\SupportCenter** .

Další informace najdete v tématu [Support Center](../../support/support-center.md).


### <a name="management-insights-dashboard"></a>Řídicí panel Management Insights

<!--1357979-->
Uzel **Management Insights** teď obsahuje grafický řídicí panel. Tento řídicí panel zobrazuje přehled stavů pravidel, což usnadňuje zobrazení průběhu. Řídicí panel obsahuje tyto dlaždice:

- **Index Insights pro správu**: sleduje celkový pokrok v pravidlech přehledů správy. Index je vážený průměr. Jsou to nejvíce nejdůležitější pravidla. Tento index poskytuje nejmenší váhu volitelným pravidlům.  

- **Skupiny Insights pro správu**: zobrazí procento pravidel v každé skupině.  

- **Priorita Management Insights**: zobrazuje procento pravidel podle priority.  

- **Všechny přehledy**: tabulka přehledů, včetně priority a stavu.  

![Snímek obrazovky s řídicím panelem Management Insights](media/1357979-management-insights-dashboard.png)

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md).


### <a name="improvements-to-cmpivot"></a>Vylepšení CMPivot

<!--1359068-->
CMPivot obsahuje následující vylepšení:

- Uložení **oblíbených** dotazů  

- Na kartě Souhrn dotazu vyberte počet neúspěšných nebo offline zařízení a pak vyberte možnost **Vytvoření kolekce**.

Další informace o dalších vylepšeních výkonu a řešení problémů s CMPivot najdete v tématu [vylepšení skriptů](#bkmk_scripts).

Další informace o CMPivot najdete v tématu [CMPivot](../../servers/manage/cmpivot.md).


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> Vylepšení skriptů

<!--1358239-->
Teď si můžete zobrazit podrobný výstup skriptu v nezpracovaném nebo strukturovaném formátu JSON. Toto formátování usnadňuje čtení a analýzu výstupu.

Následující vylepšení výkonu a řešení potíží se vztahují na CMPivot i skripty:

- Aktualizovaní klienti vrátí výstup na lokalitu menší než 80 KB přes rychlý komunikační kanál. Tato změna zvyšuje výkon zobrazení výstupu skriptu nebo dotazu.  

- Další protokoly pro řešení potíží  

Další informace najdete v následujících článcích:  

- [Vytvoření a spuštění PowerShellových skriptů z konzoly Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md)  

- [Odstraňování potíží s CMPivotem](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>Rozhraní API poskytovatele služby SMS

<!--3607711, fka 1321523-->
Poskytovatel serveru SMS nyní poskytuje přístup k rozhraní WMI přes protokol HTTPS, který se nazývá **Služba pro správu**. Tento REST API lze použít místo vlastní webové služby pro přístup k informacím z webu.

**Poskytovatel serveru SMS** se zobrazí jako role s možností povolení komunikace přes bránu pro správu cloudu. Aktuální použití tohoto nastavení slouží k povolení schválení aplikací prostřednictvím e-mailu ze vzdáleného zařízení.

Další informace najdete v tématu [plánování poskytovatele serveru SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Místní MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Připojení Intune už není potřeba pro nová místní nasazení MDM.

<!--1359124-->
Pro nové nasazení už není potřeba místní požadavek na správu mobilních zařízení (MDM) pro konfiguraci Microsoft Intune předplatného. Vaše organizace pořád vyžaduje licence Intune, aby mohli tuto funkci používat. Nemůžete aktuálně odebrat připojení Intune z existujících místních nasazení MDM. Další informace najdete v příspěvku na [blogu podpory Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Další aktualizace

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1810](https://support.microsoft.com/help/4482169).

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell verze 1810](/powershell/sccm/1810-release-notes?view=sccm-ps).

V konzole nástroje je k dispozici následující kumulativní aktualizace (4488598) od 25. března 2019: [kumulativní aktualizace 2 pro Configuration Manager aktuální větev, verze 1810](https://support.microsoft.com/help/4488598). Tato náhrada nahrazuje předchozí kumulativní aktualizaci KB 4486457.


### <a name="hotfixes"></a>Opravy hotfix

K vyřešení konkrétních problémů jsou k dispozici následující další opravy hotfix:

| ID | Nadpis | Datum | V konzole |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Certifikát konektoru Microsoft Intune se neobnovuje v Configuration Manager | 18. ledna 2019 | Ano |
| [4490434](https://support.microsoft.com/help/4490434) | Duplicitní sloupce zjišťování uživatelů jsou vytvořeny v Configuration Manager | 22. února 2019 | Ano |
| [4490575](https://support.microsoft.com/help/4490575) | Instalace aktualizací přestanou reagovat nebo nikdy nezobrazuje doplňování v Configuration Manager verze 1810 | 22. února 2019 | Ano |


## <a name="next-steps"></a>Další kroky

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 1810](../../servers/manage/checklist-for-installing-update-1810.md).

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.  
>
> Přečtěte si další informace:
>
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)  

Známé a významné problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).