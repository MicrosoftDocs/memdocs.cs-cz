---
title: Novinky ve verzi 1902
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1902 Configuration Manager aktuální větve.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78150c497757c1a3f0b65a870c35516983711d9a
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193823"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Co je nového ve verzi 1902 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1902 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1802, 1806 nebo 1810. <!-- baseline only statement:-->Při instalaci nové lokality je také k dispozici jako základní verze. Tento článek shrnuje změny a nové funkce v Configuration Manager verze 1902.  

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 1902](../../servers/manage/checklist-for-installing-update-1902.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).

Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Zastaralé funkce a operační systémy

Přečtěte si o změnách podpory před jejich implementací v [odebraných a zastaralých položkách](deprecated/removed-and-deprecated.md).

- Implementace pro sdílení obsahu z Azure se změnila. Pomocí brány pro správu cloudu s povoleným obsahem povolte, aby služba **CMG mohla fungovat jako distribuční bod cloudu a poskytovala obsah z Azure Storage**. V budoucnu nebudete moci vytvořit tradiční distribuční bod cloudu.

Verze 1902 vyřazuje podporu pro následující produkty:  

- Systémy Linux a UNIX jako klient. Vyřazení bylo oznámeno [verzí 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruktura webu

### <a name="client-health-dashboard"></a>Řídicí panel stavu klienta

<!--3599209-->
Nasadíte aktualizace softwaru a další aplikace, které vám pomůžou zabezpečit vaše prostředí, ale tato nasazení dosáhnou jenom zdravých klientů. Bezstavové Configuration Manager klienti nepříznivě ovlivňují celkové dodržování předpisů. Určení stavu klienta může být náročné v závislosti na jmenovateli: kolik zařízení by mělo být v oboru správy? Pokud například zjistíte všechny systémy ze služby Active Directory, i když některé z těchto záznamů jsou pro vyřazené počítače, tento proces zvýší váš jmenovatel.

Teď si můžete zobrazit řídicí panel s informacemi o stavu klientů Configuration Manager ve vašem prostředí. Zobrazit stav klienta, stav scénáře a běžné chyby. Filtrovat zobrazení podle několika atributů, aby se zobrazily případné problémy podle verzí operačního systému a klienta.

V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Rozbalte položku **stav klienta**a vyberte uzel **řídicí panel stavu klienta** .

![Snímek obrazovky s řídicím panelem stavu klienta](media/3599209-client-health-dashboard.png)

Další informace najdete v tématu [monitorování klientů](../../clients/manage/monitor-clients.md#bkmk_health).

### <a name="new-management-insight-rules"></a>Nová pravidla přehledu správy

Funkce Management Insights má následující nová pravidla:

- Několik pravidel s doporučeními pro správu kolekcí. Pomocí těchto přehledů můžete zjednodušit správu a zvýšit výkon. Zkontrolujte Tato nová pravidla ve skupině **kolekce** .<!--3555752-->  

- **Aktualizujte klienty na podporované pravidlo verze Windows 10** ve **zjednodušené skupině pro správu** . Toto pravidlo sestavuje na klientech, na kterých běží verze Windows 10, která už není podporovaná. Zahrnuje taky klienty s verzí Windows 10, která se blíží konci služby (tři měsíce).<!--3897268-->  

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md).

### <a name="improvement-to-enhanced-http"></a>Vylepšení rozšířené protokolu HTTP

<!--3798957-->

Nyní můžete povolit rozšířený protokol HTTP na primární lokalitu nebo pro lokalitu centrální správy.

Ve vlastnostech lokality centrální správy vyberte možnost **použití Configuration Manager generovaných certifikátů pro systémy lokality http**. Toto nastavení platí pouze pro role systému lokality v lokalitě centrální správy. Nejedná se o globální nastavení hierarchie.

Další informace najdete v tématu [Rozšířená http](../hierarchy/enhanced-http.md).

### <a name="improvement-to-setup-prerequisites"></a>Vylepšení požadavků na instalaci

Když nainstalujete nebo aktualizujete verzi 1902, Configuration Manager instalační program nyní zahrnuje následující kontrolu požadovaných součástí:

- **Čeká se na restart systému na vzdáleném SQL Server**: Tato kontrola požadovaných součástí je podobná pravidlu **restartování systému** , ale kontroluje vzdálené SQL Server. Další informace najdete v tématu [seznam kontrol požadovaných součástí](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Správa připojená ke cloudu

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Zastavit cloudovou službu, pokud překročí prahovou hodnotu

<!--3735092-->
Configuration Manager teď může zastavit službu Brána pro správu cloudu (CMG), když celkový přenos dat dosáhne limitu. CMG má vždycky výstrahy, aby aktivovaly oznámení v případě, že využití dosáhlo varování nebo kritické úrovně. Tato nová možnost vypne cloudovou službu, aby vám pomohla snížit případné neočekávané náklady na Azure z důvodu špičky využití.

Další informace najdete v tématu [zastavení CMG, pokud překročí prahovou hodnotu](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop).

### <a name="use-azure-resource-manager-for-cloud-services"></a>Použití Azure Resource Manager pro cloudové služby

<!--3605704-->
Počínaje verzí 1810 se nasazení klasické služby v Azure už nepoužívá k použití v Configuration Manager. Tato verze je poslední, aby podporovala vytváření těchto nasazení Azure.

Existující nasazení budou fungovat i nadále. Od této aktuální verze větve je Azure Resource Manager jediným mechanismem nasazení pro nové instance brány pro správu cloudu a cloudového distribučního bodu.

Další informace najdete v tématu [Azure Resource Manager pro bránu pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Přidat bránu pro správu cloudu do skupin hranic

<!--3640932-->
Nyní můžete přidružit bránu pro správu cloudu (CMG) k hraniční skupině. Tato konfigurace umožňuje klientům výchozí nebo záložní CMG pro komunikaci klientů podle vztahů skupin hranic. Toto chování je užitečné hlavně v scénářích firemních poboček a VPN. Můžete směrovat klientský provoz z nákladných a pomalých připojení WAN, abyste místo toho používali rychlejší internetové odkazy na Microsoft Azure.

Další informace najdete v tématu [Návrh hierarchie CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) a [Nastavení CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Správa v reálném čase

### <a name="run-cmpivot-from-the-central-administration-site"></a>Spuštění CMPivot z lokality centrální správy

<!--3610960-->
Configuration Manager nyní podporuje spouštění CMPivot z lokality centrální správy v hierarchii. Primární lokalita stále zpracovává komunikaci s klientem. Při spuštění CMPivot z lokality centrální správy komunikuje s primární lokalitou prostřednictvím vysokorychlostního kanálu pro odběr zpráv. Tato komunikace nespoléhá na standardní replikaci SQL mezi lokalitami.

Další informace najdete v tématu [CMPivot for data v reálném čase](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1902).

### <a name="edit-or-copy-powershell-scripts"></a>Úpravy nebo kopírování skriptů PowerShellu

<!--3705507-->
Nyní můžete **Upravit** nebo **zkopírovat** existující skript prostředí PowerShell, který se používá s funkcí spustit skripty. Místo opětovného vytváření skriptu, který potřebujete změnit, ho teď můžete přímo upravit. Obě akce používají stejné možnosti průvodce jako při vytváření nového skriptu. Při úpravách nebo kopírování skriptu Configuration Manager neuchovává stav schválení.

Další informace najdete v tématu [spuštění skriptů](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit).


## <a name="content-management"></a><a name="bkmk_content"></a> Správa obsahu

### <a name="distribution-point-maintenance-mode"></a>Režim údržby distribučního bodu

<!--3555754-->

Distribuční bod teď můžete nastavit v režimu údržby. Povolit režim údržby při instalaci softwarových aktualizací nebo při změnách hardwaru serveru.

I když je distribuční bod v režimu údržby, má následující chování:

- Web do něj nedistribuuje žádný obsah.  

- Body správy nevracejí umístění tohoto distribučního bodu klientům.

- Při aktualizaci lokality se stále aktualizuje distribuční bod v režimu údržby.

- Vlastnosti distribučního bodu jsou jen pro čtení. Nemůžete například změnit certifikát ani přidat skupiny hranic.  

- Všechny naplánované úlohy, jako je ověření obsahu, se pořád spouštějí ve stejném plánu.

Další informace o této funkci najdete v tématu [režim údržby](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

Další informace o automatizaci tohoto procesu pomocí Configuration Manager SDK naleznete v tématu [Metoda SetDPMaintenanceMode ve třídě SMS_DistributionPointInfo](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Správa klientů

### <a name="client-provisioning-mode-timeout"></a>Časový limit režimu zřizování klientů

<!--3197824-->
Pořadí úkolů nastaví časové razítko, když klient umístí do režimu zřizování. Klient v režimu zřizování kontroluje každých 60 minut dobu od časového razítka. Pokud je v režimu zřizování více než 48 hodin, klient automaticky ukončí režim zřizování a restartuje jeho proces.

Další informace najdete v tématu [režim zřizování](../../../osd/understand/provisioning-mode.md).

### <a name="view-first-screen-only-during-remote-control"></a>Zobrazit první obrazovku pouze při vzdáleném řízení

<!--3231732-->
Když se připojujete ke klientovi se dvěma nebo více monitory, může být obtížné zobrazit všechny v prohlížeči vzdáleného řízení Configuration Manager. Operátor nástrojů pro vzdálenou spolupráci si teď může vybrat, jestli se mají zobrazovat **všechny obrazovky** nebo jenom **první obrazovka** .

Další informace najdete v tématu [Postup při vzdálené správě klientského počítače se systémem Windows](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Zadat vlastní port pro probuzení partnerského vztahu

<!--3605925-->
Nyní můžete zadat vlastní číslo portu pro proxy probuzení. V nastavení klienta ve skupině **řízení spotřeby** nakonfigurujte nastavení pro **Wake on LAN číslo portu (UDP)**.  

Další informace najdete v tématu [Postup konfigurace funkce Wake on LAN](../../clients/deploy/configure-wake-on-lan.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Správa aplikací

### <a name="improvements-to-application-approvals-via-email"></a>Vylepšení pro schvalování aplikací prostřednictvím e-mailu

<!--3594063-->
Tato verze obsahuje vylepšení funkce pro příjem e-mailových oznámení pro žádosti o aplikace. Uživatelé můžou do žádosti vždycky přidat komentář z centra softwaru. Tento komentář se zobrazuje na žádost aplikace v konzole Configuration Manager. Teď tento komentář zobrazuje i v e-mailu. Zahrnutím tohoto komentáře do e-mailu můžou schvalovatelé učinit lepší rozhodnutí o schválení nebo zamítnutí žádosti.

Další informace najdete v tématu [e-mailová oznámení](../../../apps/deploy-use/app-approval.md#bkmk_email-approve).

### <a name="improvements-to-package-conversion-manager"></a>Vylepšení správce převodu balíčků

<!-- SCCMDocs-pr issue #3357 -->
Tato verze zahrnuje následující vylepšení pro [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md):

- Plánovaná analýza balíčku se ve výchozím nastavení spouští každých 7 dnů.
- Rutiny PowerShellu pro analýzu a převod balíčků
- Obecné opravy chyb a vylepšení


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Nasazení operačního systému

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Stav průběhu během místního upgradu pořadí úkolů

<!--3747129-->
Nyní se zobrazí podrobnější indikátor průběhu během pořadí úkolů místního upgradu systému Windows 10. Tento panel zobrazuje průběh instalace systému Windows, což je v opačném případě v průběhu pořadí úkolů tiché. Uživatelé teď mají přehled o tom, jak je vidět. Pomáhá s tím, že proces upgradu je pozastaven z důvodu nedostatku indikace průběhu.  

![Příklad průběhu pořadí úkolů s průběhem upgradu Windows](media/3747129-installation-progress.png)

Tato funkce funguje s libovolnou podporovanou verzí systému Windows 10, a to pouze pomocí místního pořadí úkolů upgradu.

### <a name="improvements-to-task-sequence-media-creation"></a>Vylepšení vytváření médií pořadí úloh

<!--3556027, fka 1359388-->
Tato verze zahrnuje několik vylepšení, která vám pomůžou lépe vytvářet a spravovat média pořadí úloh. Další informace najdete v následujících článcích pro konkrétní typy médií:

- [Vytvoření samostatného média](../../../osd/deploy-use/create-stand-alone-media.md)
- [Vytvoření předzpracovaného média](../../../osd/deploy-use/create-prestaged-media.md)
- [Vytvoření spouštěcího média](../../../osd/deploy-use/create-bootable-media.md)
- [Vytvoření záznamového média](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Zadat dočasné úložiště

Když vytváříte médium pořadí úkolů, teď můžete přizpůsobit umístění, které lokalita používá k dočasnému ukládání dat. Tento proces může vyžadovat mnoho místa na dočasném disku. Tato změna poskytuje větší flexibilitu při výběru místa pro uložení těchto dočasných souborů.

V **Průvodci vytvořením média pořadí úloh**zadejte umístění **pracovní složky**. Ve výchozím nastavení je toto umístění podobné následující cestě: `%UserProfile%\AppData\Local\Temp` .

#### <a name="add-a-label-to-the-media"></a>Přidání popisku na médium

Nyní můžete přidat popisek k médiu pořadí úloh. Tento popisek vám pomůže lépe identifikovat médium po jeho vytvoření. V **Průvodci vytvořením média pořadí úloh**zadejte **jmenovku média**.

### <a name="import-a-single-index-of-an-os-image"></a>Importovat jeden index image operačního systému

<!--3719699-->
Při importu souboru bitové kopie systému Windows (WIM) do Configuration Manager můžete nyní zadat automatické importování jednoho indexu místo všech indexů obrázků v souboru. Tato možnost nabízí následující výhody:

- Menší soubor obrázku  
- Rychlejší online údržba  
- Optimalizace údržby imagí pro menší soubor bitové kopie po provedení offline údržby

Když importujete bitovou kopii operačního systému, vyberte možnost pro **extrakci konkrétního indexu bitové kopie ze zadaného souboru WIM**. Pak ze seznamu vyberte index bitové kopie.  

Další informace najdete v tématu [Přidání image operačního systému](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages).

### <a name="optimized-image-servicing"></a>Optimalizovaná údržba imagí

<!--3555951-->
Při použití aktualizací softwaru na bitovou kopii operačního systému je k dispozici nová možnost optimalizace výstupu odebráním všech nahrazených aktualizací. Optimalizace na offline údržbu platí jenom pro image s jedním indexem.

Když vytváříte plán pro aktualizaci image operačního systému, vyberte možnost **Odebrání nahrazených aktualizací po aktualizaci image**.

Další informace najdete v tématu [použití aktualizací softwaru pro obrázek](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase).

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Vylepšení spuštění skriptu prostředí PowerShell pro krok pořadí úkolů

<!--3556028, fka 1359389-->
Krok pořadí úkolů **Spustit skript prostředí PowerShell** nyní obsahuje následující vylepšení:  

- V tomto kroku teď můžete přímo zadat kód Windows PowerShellu. Tato změna umožňuje spustit příkazy prostředí PowerShell během pořadí úkolů bez předchozího vytvoření a distribuce balíčku pomocí skriptu.

- Když zvolíte možnost **zadat skript prostředí PowerShell** , vyberte **Upravit skript**. Nové okno skriptu PowerShellu nabízí tyto akce:  

    - Přímo upravit skript  

    - Otevřít existující skript ze souboru  

    - Přejít na existující schválený skript v Configuration Manager

- Uložte výstup skriptu do vlastní proměnné pořadí úkolů.  

- Chcete-li zahrnout parametry skriptu do protokolu pořadí úloh, nastavte proměnnou pořadí úloh **OSDLogPowerShellParameters** na **hodnotu true**. Ve výchozím nastavení nejsou parametry v protokolu.  

- Další vylepšení, která poskytují podobné funkce jako krok [Spustit příkazový řádek](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . Zadejte například alternativní přihlašovací údaje uživatele nebo zadejte časový limit.

> [!Important]  
> Pokud chcete tuto novou funkci Configuration Manager využít, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

Další informace najdete v tématu [spuštění skriptu PowerShellu](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

### <a name="other-improvements-to-os-deployment"></a>Další vylepšení nasazení operačního systému

<!--3633146,3641475,3654172,3734270-->
Tato verze zahrnuje následující vylepšení nasazení operačního systému:

- V pořadí úloh je nová akce **zobrazení** výchozí. <!--3633146-->  

- V dialogovém okně chyby pořadí úloh se nyní zobrazí další informace. Zobrazuje název kroku pořadí úloh, u kterého došlo k chybě. <!--3641475-->  

- Když nastavíte proměnnou pořadí úloh **OSDDoNotLogCommand** na hodnotu true, teď se z kroku Spustit příkazový řádek v souboru protokolu také skryje příkazový řádek. Dříve používali pouze název programu v kroku instalovat balíček v souboru Smsts. log.<!--3654172-->  

- Pokud povolíte respondér PXE v distribučním bodě bez služby pro nasazení systému Windows, může být nyní na stejném serveru jako služba DHCP. <!--3734270--> Další informace najdete v tématu [Konfigurace aspoň jednoho distribučního bodu pro příjem požadavků PXE](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


## <a name="software-center"></a><a name="bkmk_userxp"></a> Centrum softwaru

### <a name="replace-toast-notifications-with-dialog-window"></a>Nahradit informační zprávy pomocí dialogového okna

<!--3555947-->
Někdy se uživatelům nezobrazuje zpráva informující o systému Windows o restartování nebo požadovaném nasazení. Pak nevidí prostředí, které připomíná připomenutí k odložení. Toto chování může vést k nedostatečnému uživatelskému prostředí, když klient dosáhne konečného termínu.

Teď, když nasazení potřebuje restartování nebo změny softwaru, máte možnost použít více rušivých dialogových oken.

Další informace najdete v tématu [plánování centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact) .

### <a name="configure-user-device-affinity-in-software-center"></a>Konfigurace spřažení uživatelských zařízení v centru softwaru

<!--3485366-->
Díky [vylepšením infrastruktury centra softwaru](whats-new-in-version-1806.md#software-center-infrastructure-improvements) počínaje verzí 1806 se už role serveru webu Katalog aplikací ve většině scénářů nevyžadují. Někteří zákazníci se pořád spoléhali na katalog aplikací, aby uživatelům umožnili nastavit jejich primární zařízení pro spřažení uživatelských zařízení.

Uživatelé teď můžou nastavit svoje primární zařízení v centru softwaru. Tato akce vytvoří primárnímu uživateli zařízení v Configuration Manager.

Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="configure-default-views-in-software-center"></a>Konfigurace výchozích zobrazení v centru softwaru

<!--3612112-->
V této verzi Configuration Manager se dále vychází, jak můžete přizpůsobit Centrum softwaru:

- Nastavení výchozího rozložení aplikací, a to jako dlaždic nebo seznam  

    - Pokud uživatel tuto konfiguraci změní, Centrum softwaru bude v budoucnu nadále mít předvolbu uživatele.  

- Konfigurace výchozího filtru aplikace, buď všech nebo jenom požadovaných aplikací  

    - Centrum softwaru vždy používá vaše výchozí nastavení. Uživatelé můžou tento filtr změnit, ale Centrum softwaru neuchovává své preference.

Tato nastavení zadejte ve skupině **Centrum softwaru** nastavení klienta.

Další informace najdete v tématu [informace o nastavení klienta](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults).


## <a name="software-updates"></a><a name="bkmk_sum"></a> Aktualizace softwaru

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Zadejte prioritu pro aktualizace funkcí v rámci údržby Windows 10.

<!--3734525-->
Upravte prioritu tím, že klienti nainstalují aktualizaci funkcí prostřednictvím [údržby Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). Ve výchozím nastavení klienti nyní instalují aktualizace funkcí s vyšší prioritou zpracování.

Tuto možnost můžete nakonfigurovat pomocí nastavení klienta. Ve skupině **aktualizace softwaru** nakonfigurujte následující nastavení: **Zadejte prioritu vlákna pro aktualizace funkcí**.

Další informace najdete v tématu [informace o nastavení klienta](../../clients/deploy/about-client-settings.md#software-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a> Správa Office

### <a name="redirect-windows-known-folders-to-onedrive"></a>Přesměrovat známé složky Windows na OneDrive

<!--3556021-->
Pomocí Configuration Manager můžete přesunout známé složky Windows na OneDrive pro firmy. Mezi tyto složky patří plocha, dokumenty a obrázky. Chcete-li zjednodušit upgrady Windows 10, nasaďte tato nastavení do klientů se systémem Windows 7 před nasazením pořadí úkolů.

Další informace o této funkci OneDrivu pro firmy najdete v tématu [přesměrování a přesunutí známých složek Windows na OneDrive](/onedrive/redirect-known-folders).

Nejdřív [vyhledejte ID tenanta Microsoft 365](/onedrive/find-your-office-365-tenant-id). Pak nasaďte synchronizačního klienta OneDrivu verze 18.111.0603.0004 nebo novější. Další informace najdete v tématu [nasazení aplikací OneDrive pomocí Configuration Manager](/onedrive/deploy-on-windows).  

Profil OneDrivu pro firmy vytvoříte a nasadíte tak, že v konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Rozbalte **Nastavení dodržování předpisů**a vyberte uzel **profily OneDrivu pro firmy** .  

Další informace najdete v části přesměrování známých složek Windows na OneDrive v článku [profily OneDrivu pro firmy](../../../compliance/deploy-use/onedrive-profile.md) .

### <a name="integration-for-microsoft-365-apps-for-enterprise-readiness"></a>Integrace pro aplikace Microsoft 365 pro podnikovou připravenost

<!--3735402-->
Použijte Configuration Manager k identifikaci zařízení s vysokou jistotou, která je připravená k upgradu na Microsoft 365 aplikace pro podnik. Integrace poskytuje přehledy o potenciálních potížích s kompatibilitou s Doplňky Office a makry používanými ve vašem prostředí. Pak použijte Configuration Manager k nasazení Office do připravených zařízení.

Existující řídicí panel pro správu klientů Microsoft 365 nyní obsahuje novou dlaždici **upgrade Readiness Office 365 ProPlus**.

Další informace najdete v tématu [Microsoft 365 řídicího panelu pro správu klientů](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) .

### <a name="additional-languages-for-microsoft-365-updates"></a>Další jazyky pro aktualizace Microsoft 365

<!--3555955-->
Configuration Manager teď podporuje všechny podporované jazyky pro Microsoft 365 aktualizace klientů. Pracovní postup aktualizace teď odděluje jazyky 38 pro **web Windows Update** z mnoha jazyků pro **aktualizaci klienta Office 365**.

Další informace najdete v tématu [Správa aktualizací Microsoft 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang) .

### <a name="office-products-on-lifecycle-dashboard"></a>Produkty Office na řídicím panelu životní cyklus

<!--3556026-->
Řídicí panel životní cyklus produktu teď obsahuje informace o nainstalovaných verzích Office 2003 až do sady Office 2016. Data se zobrazí poté, co lokalita spustí úlohu Shrnutí životního cyklu, což je každých 24 hodin.

Další informace najdete v tématu [Použití řídicího panelu životní cyklus produktu](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> Postupná nasazení

### <a name="dedicated-monitoring-for-phased-deployments"></a>Vyhrazené monitorování pro dvoufázové nasazení

<!--3555949-->
Postupná nasazení nyní mají vlastní vyhrazený uzel monitorování. Tento uzel usnadňuje identifikaci fází nasazení, které jste vytvořili, a pak přejdete do zobrazení monitorování postupného nasazení. V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **dvoufázové nasazení** . Zobrazuje seznam fází nasazení.

Další informace najdete v tématu [zobrazení monitorování postupného nasazení](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor).

### <a name="improvement-to-phased-deployment-success-criteria"></a>Zlepšení úspěšných kritérií nasazení

<!--3555946-->
Zadejte další kritéria pro úspěch fáze v dvoufázovém nasazení. Místo jenom v procentech teď může být tato kritéria zároveň počet úspěšně nasazených zařízení. Tato možnost je užitečná v případě, že je velikost kolekce proměnná a máte určitý počet zařízení, aby bylo možné před přechodem do další fáze zobrazit úspěch.

Vytvoření postupného nasazení pro pořadí úkolů, aktualizaci softwaru nebo aplikaci. Pak na stránce nastavení v průvodci vyberte následující možnost jako kritéria úspěchu první fáze: **Počet úspěšně nasazených zařízení**.

Další informace najdete v tématu [Vytvoření dvoufázové nasazení](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Konzola Configuration Manager

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Vylepšení konzoly Configuration Manager

<!--3594151-->
Na základě zpětné vazby od zákazníků na konferenci Středozápadě Management summit (MMS) Desert edice 2018 obsahuje tato verze následující vylepšení Configuration Manager konzole:

- Maximalizuje okno procházení registru pro metody detekce aplikace.
- Přejít na kolekci z nasazení aplikace
- Odebrat obsah ze stavu monitorování
- Zobrazení řazení podle celočíselných hodnot v uzlu **nasazení** pracovního prostoru **monitorování**
- Přesunutí upozornění na velký počet výsledků

Další informace najdete v tématu [Configuration Manager tipů konzoly](../../servers/manage/admin-console-tips.md).

### <a name="configuration-manager-console-notifications"></a>Oznámení konzoly Configuration Manager

<!--3556016, fka 1318035-->
Abyste měli lepší informace, abyste mohli provádět příslušné akce, Configuration Manager konzola vás nyní upozorní na následující události:

- Když je k dispozici aktualizace pro Configuration Manager sebe sama
- V případě, že dojde k událostem životního cyklu a údržby v prostředí

Toto oznámení je pruhem v horní části okna konzoly pod pás karet. Nahrazuje předchozí prostředí, když Configuration Manager aktualizace k dispozici. Tato oznámení v konzole stále zobrazují důležité informace, ale nebrání v práci v konzole nástroje. Nemůžete zavřít kritická oznámení. Konzola zobrazí všechna oznámení v nové oblasti oznámení v záhlaví.

Další informace najdete v tématu [Configuration Manager oznámení konzoly](../../servers/manage/admin-console-notifications.md).

### <a name="confirmation-of-console-feedback"></a>Potvrzení zpětné vazby z konzoly

<!--3556010-->
Po odeslání [zpětné vazby](../../understand/find-help.md#product-feedback) v konzole Configuration Manager se nyní zobrazí potvrzovací zpráva. Tato zpráva obsahuje **ID zpětné vazby**, které můžete společnosti Microsoft poskytnout jako identifikátor sledování.

Další informace najdete v tématu o [zpětné vazbě produktu](../../understand/find-help.md#bkmk_feedbackid).

### <a name="view-recently-connected-consoles"></a>Zobrazit nedávno připojené konzoly

<!--3699367-->
Nyní si můžete zobrazit nejnovější připojení pro konzolu Configuration Manager. Zobrazení zahrnuje aktivní připojení a konzoly, které byly nedávno připojeny. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **zabezpečení**a vyberte uzel **připojení konzoly** .

Další informace najdete v tématu [použití konzoly Configuration Manager](../../servers/manage/admin-console.md#bkmk_viewconnected).

### <a name="in-console-documentation-dashboard"></a>Řídicí panel dokumentace konzoly

<!--3556019, fka 1357546-->
V novém pracovním prostoru **komunity** je nový uzel **dokumentace** . Tento uzel obsahuje aktuální informace o Configuration Manager dokumentaci a články o podpoře.

Další informace najdete v tématu [použití konzoly Configuration Manager](../../servers/manage/admin-console.md#bkmk_doc-dashboard).

### <a name="search-device-views-using-mac-address"></a>Prohledat zobrazení zařízení pomocí adresy MAC

<!--3600878-->
Adresu MAC teď můžete vyhledat v zobrazení zařízení konzoly Configuration Manager. Tato vlastnost je užitečná pro Správce nasazení operačního systému při řešení potíží s nasazeními založenými na technologii PXE. Když si zobrazíte seznam zařízení, přidejte do zobrazení sloupec **adresa MAC** . Pomocí vyhledávacího pole přidejte kritéria hledání **adresy MAC** .

Další informace najdete v tématu [Configuration Manager tipů konzoly](../../servers/manage/admin-console-tips.md).

### <a name="use-net-47-for-improved-console-accessibility"></a>Použití .NET 4,7 pro lepší přístupnost konzoly

<!-- SCCMDocs-pr issue #3228 -->
Chcete-li zlepšit funkce přístupnosti konzoly Configuration Manager, aktualizujte rozhraní .NET na verzi 4,7 nebo novější v počítači, na kterém je spuštěna konzola nástroje.

Další informace najdete v tématu [funkce usnadnění v Configuration Manager](../../understand/accessibility-features.md).

### <a name="changes-to-console-setup-process"></a>Změny procesu instalace konzoly

<!-- 3612513 -->
Při instalaci konzoly Configuration Manager jsou vyžadovány nové součásti. Pokud vytvoříte balíček pro instalaci konzoly nástroje do jiných počítačů, ujistěte se, že balíček obsahuje následující soubory:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Při instalaci nebo aktualizaci serveru lokality zkopírují tyto instalační soubory a podporované jazykové sady pro lokalitu do podsložky **Tools\ConsoleSetup** . Další informace najdete v tématu [Instalace konzoly Configuration Manager](../../servers/deploy/install/install-consoles.md).


## <a name="other-updates"></a>Další aktualizace

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1902](https://support.microsoft.com/help/4498910).

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell verze 1902](/powershell/sccm/1902-release-notes?view=sccm-ps).

Následující kumulativní aktualizace (4500571) je k dispozici v konzole od 17. června 2019: [kumulativní aktualizace pro Configuration Manager aktuální větev, verze 1902](https://support.microsoft.com/help/4500571).

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

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 1902](../../servers/manage/checklist-for-installing-update-1902.md).

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.  
>
> Přečtěte si další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)  

Známé a významné problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).