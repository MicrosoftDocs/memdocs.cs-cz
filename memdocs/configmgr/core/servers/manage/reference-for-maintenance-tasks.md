---
title: Referenční informace k úlohám údržby
titleSuffix: Configuration Manager
description: Podrobnosti o jednotlivých úlohách údržby Configuration Manager lokality
ms.date: 06/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f686547e4698f1941a64f5b0346ba2d723248c31
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912520"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Referenční informace pro úlohy údržby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto článku jsou uvedeny podrobnosti o jednotlivých úlohách údržby Configuration Manager lokality. Každá položka určuje typy lokalit, kde je úloha k dispozici, a zda je ve výchozím nastavení povolená.

Další informace najdete v tématu [nastavení úloh údržby](maintenance-tasks.md#set-up-maintenance-tasks).  

## <a name="tasks"></a>Úlohy

### <a name="backup-site-server"></a>Zálohovat server lokality

Pomocí této úlohy můžete vytvořit zálohu důležitých informací k obnovení lokality a databáze Configuration Manager. Další informace najdete v tématu [zálohování Configuration Manager lokality](backup-and-recovery.md).  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Není povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="check-application-title-with-inventory-information"></a>Podívejte se na název aplikace s informacemi o inventáři.

Pomocí této úlohy můžete zachovat konzistenci softwarových titulů mezi inventářem softwaru a katalogem funkce Asset Intelligence. Další informace najdete v tématu [Úvod do funkce Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|Primární lokalita|Není k dispozici|
|Sekundární lokalita|Není k dispozici|

### <a name="clear-undiscovered-clients"></a>Vymazat nezjištěné klienty

> [!Tip]
> Tato úloha se může zobrazit také v konzole s názvem **Označit jako vymazat instalaci**.

Pomocí této úlohy můžete odebrat nainstalovaný příznak pro klienty, kteří neodesílají záznam zjišťování prezenčního signálu během období opakovaného **vyhledávání klienta** . Instalovaný příznak zabraňuje automatickému nabízené instalaci klienta do počítače, který může mít klienta služby Active Configuration Manager.  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Není povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-application-request-data"></a>Odstranit stará data aplikačních požadavků

Pomocí této úlohy můžete z databáze odstranit zastaralá aplikační požadavky. Další informace najdete v tématu [Vytvoření a nasazení aplikace](../../../apps/get-started/create-and-deploy-an-application.md).  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-application-revisions"></a>Odstranit staré revize aplikací

Pomocí této úlohy můžete odstranit revize aplikací, na které se již neodkazuje. Další informace najdete v tématu [postup revize a nahrazování aplikací](../../../apps/deploy-use/revise-and-supersede-applications.md).

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-client-download-history"></a>Odstranit zastaralou historii stahování klientů

Pomocí této úlohy můžete odstranit historická data o zdroji stahování používanému klienty. Lokalita nástroje používá zdrojové informace ke stažení k naplnění [řídicího panelu zdrojů dat klienta](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-client-operations"></a>Vymazat staré operace klientů

Pomocí této úlohy můžete z databáze lokality odstranit všechna zastaralá data pro klientské operace. Například tato data zahrnují následující operace:

- Stará nebo prošlá oznámení klienta, například požadavky na stažení pro počítač nebo zásady uživatele
- Endpoint Protection, jako jsou žádosti správce pro klienty, aby mohli spouštět kontrolu nebo stahovat aktualizované definice
- Spustit výsledky stavu skriptů

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-client-presence-history"></a>Odstranit zastaralou historii přítomnosti klientů
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Pomocí této úlohy můžete odstranit informace o historii týkající se online stavu klientů zaznamenaných klientským oznámením. Odstraní informace pro klienty se stavem, který je starší než určený čas. Další informace najdete v tématu [monitorování klientů](../../clients/manage/monitor-clients.md).

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Odstranit stará data o Brána pro správu cloudu provozu

Pomocí této úlohy můžete z databáze lokality odstranit všechna zastaralá data o provozu, který projde [bránou pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md). Mezi tato data patří:

- Počet požadavků
- Celkový počet bajtů požadavku
- Bajty odpovědí celkem
- Počet neúspěšných žádostí
- Maximální počet souběžných požadavků

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-cmpivot-results"></a>Odstranit zastaralá CMPivot výsledky

Pomocí této úlohy můžete odstranit z databáze lokality staré informace od klientů v dotazech CMPivot. Další informace najdete v tématu [CMPivot for data v reálném čase](cmpivot.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-collected-files"></a>Odstranit staré shromážděné soubory

Pomocí této úlohy můžete z databáze odstranit zastaralé informace o shromážděných souborech. Tato úloha rovněž odstraňuje shromážděné soubory ze struktury složky serveru lokality ve vybrané lokalitě. Ve výchozím nastavení se pět nejnovějších kopií shromážděných souborů ukládá na server lokality v adresáři **Inboxes\sinv.box\Filecol** . Další informace najdete v tématu [Úvod do inventáře softwaru](../../clients/manage/inventory/introduction-to-software-inventory.md).  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-computer-association-data"></a>Odstranit zastaralá data týkající se přidružení počítačů

Pomocí této úlohy můžete z databáze odstranit zastaralá data o přidružení počítačů s nasazením operačního systému. Tyto informace se použijí při obnovení stavu uživatele během pořadí úkolů. Další informace najdete v tématu [Správa stavu uživatele](../../../osd/get-started/manage-user-state.md).  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-console-connection-data"></a>Odstranit zastaralá data o připojení konzoly

Tento úkol vymaže z databáze lokality data o připojeních konzoly k lokalitě nástroje.<!-- SCCMDocs#528 -->

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-delete-detection-data"></a>Odstranit stará data o detekci odstranění

Pomocí této úlohy můžete odstranit zastaralá data z databáze, která byla vytvořena pomocí zobrazení extrakce. Odstraní staré informace o změnách dat používané externími systémy extrakce dat z databáze.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-device-wipe-record"></a>Odstranit zastaralá záznam o vymazání zařízení

Pomocí této úlohy můžete z databáze odstranit zastaralá data o akcích vymazání mobilního zařízení. Další informace najdete v tématu [Ochrana dat pomocí vzdáleného vymazání, zámku nebo resetování hesla](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-discovery-data"></a>Vymazat stará data zjišťování

Pomocí této úlohy můžete z databáze odstranit zastaralá data zjišťování. Tato data můžou zahrnovat záznamy z:

- Zjišťování prezenčního signálu
- Zjišťování sítě
- Metody zjišťování služby Active Directory: systém, uživatel a skupina

Tato úloha také odebere zastaralá zařízení označená jako vyřazená z provozu. Při spuštění této úlohy v určité lokalitě se odstraní data přidružená k dané lokalitě a tyto změny se replikují do ostatních lokalit. Další informace najdete v tématu [spuštění zjišťování](../deploy/configure/run-discovery.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-distribution-point-usage-stats"></a>Odstranit zastaralá statistiku využití distribučních bodů

Pomocí této úlohy můžete z databáze odstranit zastaralá data pro distribuční body, které jsou uložené déle než určitou dobu.  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-enrolled-devices"></a>Odstranit zastaralá zaregistrovaná zařízení

Pomocí této úlohy můžete z databáze lokality Odstranit zastaralá data o mobilních zařízeních, která po určitou dobu neohlásila žádné informace v lokalitě.

Tato úloha se týká zařízení, která jsou zaregistrovaná ve službě Configuration Manager [místní MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md). Další informace o těchto zařízeních najdete v tématu [podporované operační systémy pro klienty a zařízení](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Není povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-ep-health-status-history-data"></a>Odstranit stará data o historii stavu EP

Pomocí této úlohy můžete z databáze odstranit zastaralé informace o stavu pro Endpoint Protection (EP). Další informace najdete v tématu [monitorování Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-exchange-partnership"></a>Odstranit zastaralá partnerství Exchange

> [!Tip]
> > Tato úloha se může zobrazit také v konzole s názvem **Odstranit stará zařízení spravovaná konektorem systému Exchange Server**.

Pomocí této úlohy můžete odstranit zastaralá data o mobilních zařízeních, která spravuje konektor systému Exchange Server. Lokalita tato data odstraní v závislosti na nastavení **Ignorovat mobilní zařízení, která jsou neaktivní po dobu více než (dnů)** na kartě **zjišťování** vlastností konektoru serveru Exchange Server. Další informace najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-inventory-history"></a>Odstranit starou historii inventáře

Pomocí této úlohy můžete odstranit data inventáře databáze, která jsou uložená déle než zadanou dobu. Další informace najdete v tématu [použití Průzkumník prostředků k zobrazení inventáře hardwaru](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-log-data"></a>Odstranit stará data protokolu

Pomocí této úlohy můžete z databáze odstranit stará data protokolu používaná k řešení potíží. Tato data nesouvisí s Configuration Manager operace součástí.  

> [!IMPORTANT]  
> Tato úloha je standardně spouštěna každý den na každé lokalitě. V lokalitě centrální správy a primárních lokalitách Tato úloha odstraňuje data, která jsou starší než 30 dní. Při použití SQL Server Express v sekundární lokalitě se ujistěte, že je tato úloha spouštěna denně, a odstraní data, která jsou neaktivní po dobu sedmi dnů.  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|**Sekundární lokalita**|Povoleno|

### <a name="delete-aged-metering-data"></a>Odstranit stará data o měření

Pomocí této úlohy můžete z databáze odstranit zastaralá data pro měření softwaru, která jsou uložená déle než určitou dobu. Další informace najdete v tématu [monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-metering-summary-data"></a>Odstranit zastaralá souhrnná data měření

Pomocí této úlohy můžete z databáze odstranit zastaralá souhrnná data pro měření softwaru, která jsou uložená déle než určitou dobu. Další informace najdete v tématu [monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-notification-server-history"></a>Odstranit zastaralou historii serveru oznámení

Tato úloha odstraňuje zastaralou historii přítomnosti klientů.

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-notification-task-history"></a>Odstranit zastaralou historii úloh oznámení

Pomocí této úlohy můžete odstranit informace o úlohách klientských oznámení z databáze lokality. Tato úloha se vztahuje na data, která se po určitou dobu neaktualizovala. Další informace najdete v tématu [oznámení klienta](../../clients/manage/client-notification.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-passcode-records"></a>Odstranit zastaralé záznamy hesla

Pomocí této úlohy v lokalitě nejvyšší úrovně ve vaší hierarchii odstraňte zastaralá data o resetování hesla pro zařízení Windows Phone. Data pro resetování hesla jsou šifrovaná, ale zahrnují kód PIN pro zařízení. Ve výchozím nastavení je tato úloha povolená a odstraňuje data, která jsou starší než jeden den.  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-replication-data"></a>Odstranit stará data o replikaci

Pomocí této úlohy můžete z databáze odstranit zastaralá data o replikaci databáze mezi lokalitami Configuration Manager. Když změníte konfiguraci této úlohy údržby, bude konfigurace platit pro každou příslušnou lokalitu v hierarchii. Další informace najdete v tématu [monitorování replikace databáze](monitor-replication.md).  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|**Sekundární lokalita**|Povoleno|

### <a name="delete-aged-replication-summary-data"></a>Odstranit stará data Shrnutí replikace

Pomocí této úlohy můžete z databáze lokality Odstranit zastaralá souhrnná data replikace, když se po určitou dobu neaktualizovala. Další informace najdete v tématu [monitorování replikace databáze](monitor-replication.md).  

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|**Sekundární lokalita**|Povoleno|

### <a name="delete-aged-status-messages"></a>Odstranit staré zprávy o stavu

Pomocí této úlohy můžete z databáze odstranit zastaralá data stavových zpráv, jak jsou nakonfigurovaná v pravidlech filtru zpráv. Další informace najdete v tématu [monitorování stavového systému Configuration Manager](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-threat-data"></a>Odstranit stará data o hrozbách

Pomocí této úlohy můžete z databáze odstranit zastaralá Endpoint Protectioná data o ohroženích, která jsou uložená déle než určitou dobu. Další informace najdete v tématu [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-unknown-computers"></a>Odstranit zastaralé neznámé počítače

Pomocí této úlohy můžete odstranit informace o neznámých počítačích z databáze lokality, když se po určitou dobu neaktualizovala. Další informace najdete v tématu [Příprava pro nasazení do neznámých počítačů](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-aged-user-device-affinity-data"></a>Odstranit stará data o spřažení uživatelských zařízení

Pomocí této úlohy můžete z databáze odstranit zastaralá data o spřažení uživatelských zařízení. Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-duplicate-system-discovery-data"></a>Odstranit duplicitní data zjišťování systému

Tato úloha slouží k odstranění duplicitních záznamů generovaných zjišťováním systému z databáze lokality.<!-- SCCMDocs#1339 -->

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|Primární lokalita|Není k dispozici|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Odstranit prošlé záznamy balíčku hromadné registrace MDM

Pomocí této úlohy můžete odstranit staré certifikáty hromadných zápisů a odpovídající profily po vypršení platnosti certifikátu zápisu. Další informace najdete v tématu [Vytvoření profilů certifikátů](../../../protect/deploy-use/create-certificate-profiles.md).

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-inactive-client-discovery-data"></a>Odstranit neaktivní data zjišťování klientů

Pomocí této úlohy můžete z dat zjišťování databáze pro neaktivní klienty odstranit. Lokalita označuje klienty jako neaktivní, když je klient označen příznakem jako zastaralý a konfigurací, které jsou vytvořeny pro stav klienta.

Tato úloha funguje pouze na prostředcích, které jsou Configuration Manager klienty. Liší se od úlohy **Odstranit zastaralá data zjišťování** , která odstraňuje všechny zastaralé záznamy dat zjišťování. Když je tato úloha spuštěna na jedné lokalitě, odebírá data z databáze ve všech lokalitách hierarchie. Další informace najdete v tématu [Postup konfigurace stavu klienta](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> Pokud je povolená, nakonfigurujte tuto úlohu tak, aby běžela v intervalu větším, než je plán **zjišťování prezenčního signálu** . Tato konfigurace umožňuje aktivním klientům odeslat záznam zjišťování prezenčního signálu, aby označil svůj záznam klienta jako aktivní, aby ho tato úloha neodstranila.  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Není povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-obsolete-alerts"></a>Odstranit zastaralá upozornění

Pomocí této úlohy můžete z databáze odstranit výstrahy s vypršenou platností, které jsou uložené déle než určitou dobu. Další informace najdete v tématu [použití výstrah a stavového systému](use-alerts-and-the-status-system.md).

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-obsolete-client-discovery-data"></a>Odstranit zastaralá data zjišťování klientů

Pomocí této úlohy můžete z databáze odstranit zastaralé záznamy klientů. Záznam označený jako zastaralý byl obvykle nahrazen novějším záznamem pro stejného klienta. Novější záznam se stal aktuálním záznamem klienta. Informace o zjišťování najdete v tématu [spuštění zjišťování](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> Pokud je povolená, nakonfigurujte tuto úlohu tak, aby běžela v intervalu větším, než je plán zjišťování prezenčního signálu. Tato konfigurace umožňuje klientovi odeslat záznam zjišťování prezenčního signálu, který správně nastaví zastaralý stav.  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Není povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Odstranit zastaralé lokality a podsítě prohledávání doménové struktury

Pomocí této úlohy můžete odstranit data o lokalitách, podsítích a doménách služby Active Directory. V posledních 30 dnech dojde k odebrání dat, která lokalita nezjistila metodou zjišťování doménové struktury služby Active Directory. Tato úloha odebere data zjišťování, ale neovlivní hranice, které vytvoříte z těchto dat zjišťování. Další informace najdete v tématu [spuštění zjišťování](../deploy/configure/run-discovery.md).

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="delete-orphaned-client-deployment-state-records"></a>Odstranit záznamy stavu nasazení osamoceného klienta

Pomocí této úlohy můžete pravidelně vyprázdnit tabulku, která obsahuje informace o stavu nasazení klienta. Tento úkol vyčistí záznamy přidružené k zastaralým nebo vyřazeným zařízením.  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="evaluate-collection-members"></a>Vyhodnotit členy kolekce

Vyhodnocování členství kolekce nakonfigurujete jako součást lokality. Další informace najdete v tématu [součásti lokality](../deploy/configure/site-components.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="monitor-keys"></a>Monitorování klíčů

Pomocí této úlohy můžete monitorovat integritu primárních klíčů databáze Configuration Manager. Primární klíč je sloupec nebo kombinace sloupců, které jedinečně identifikují jeden řádek. Klíč rozlišuje řádek od jakéhokoli jiného řádku v Microsoft SQL Server tabulce databáze.

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Povoleno|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="rebuild-indexes"></a>Opětovné sestavení indexů

Pomocí této úlohy můžete znovu sestavit indexy Configuration Manager databáze. Index je databázová struktura, která je vytvořena v tabulce databáze pro urychlení načítání dat. Například vyhledávání indexovaného sloupce je často mnohem rychlejší než prohledávání sloupce, který není indexován.

Pro zvýšení výkonu se indexy Configuration Managerch databází často aktualizují, aby zůstaly synchronizované s neustále se měnícími se daty uloženými v databázi. Tato úloha:

- Vytvoří indexy na sloupcích databáze, které mají alespoň 50% jedinečných hodnot.
- Zruší indexy sloupců, které jsou menší než 50 procent.
- Znovu sestaví všechny stávající indexy, které splňují kritéria jedinečnosti dat.

| Typ lokality | Status |
| --------- | ------ |
|**Lokalita centrální správy**|Není povoleno|
|**Primární lokalita**|Není povoleno|
|**Sekundární lokalita**|Není povoleno|

### <a name="summarize-file-usage-metering-data"></a>Shrnutí dat měření využití souborů

Pomocí této úlohy můžete shrnout data z několika záznamů pro použití souboru měření softwaru do jednoho souhrnného záznamu. Souhrn dat může komprimovat množství dat uložených v databázi Configuration Manager.

Pokud chcete shrnout data měření softwaru a šetřit místo na disku v databázi, použijte tuto úlohu s úlohou **shrnout měsíční data o využití softwaru pro měření softwaru** . Další informace najdete v tématu [monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="summarize-installed-software-data"></a>Shrnout nainstalovaná data softwaru

Pomocí této úlohy můžete shrnout data ze shromážděných informací o softwaru katalogu Asset Intelligence prostřednictvím inventáře hardwaru a sloučit více záznamů do jednoho celkového záznamu. Souhrn dat může komprimovat množství dat uložených v databázi Configuration Manager. Další informace najdete v tématu [Konfigurace úloh údržby funkce Asset Intelligence](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="summarize-monthly-usage-metering-data"></a>Sumarizace měsíčních dat měření využití

Pomocí této úlohy můžete shrnout data z několika záznamů pro měsíční použití měření softwaru do jednoho souhrnného záznamu. Souhrn dat může komprimovat množství dat uložených v databázi Configuration Manager.

Chcete-li shrnout data softwarového měření a šetřit místo v databázi, použijte tuto úlohu s daty o **využití souborů měření softwaru na Shrnutí** . Další informace najdete v tématu [monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="update-application-available-targeting"></a>Aktualizovat dostupné cílení aplikace

Tato úloha slouží k tomu, aby Configuration Manager přepočítala mapování nasazení zásad a aplikací na prostředky v kolekcích. Když nasadíte zásady nebo aplikace do kolekce, Configuration Manager vytvoří počáteční mapování mezi objekty, které nasazujete, a členy kolekce.

Tato mapování jsou pro rychlý přístup uložená v tabulce. Když se členství v kolekci změní, lokalita tyto uložené mapování aktualizuje, aby odrážela tyto změny. Je ale možné, že tato mapování přestanou být synchronizovaná. Například pokud lokalita nedokáže správně zpracovat soubor oznámení, tato změna se nemusí projevit při změně mapování. Tato úloha aktualizuje mapování na základě aktuálního členství v kolekci.  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|

### <a name="update-application-catalog-tables"></a>Aktualizovat tabulky katalogu aplikací

Pomocí této úlohy můžete synchronizovat mezipaměť databáze webu Katalog aplikací s nejnovějšími informacemi o aplikaci. Když změníte konfiguraci této úlohy údržby, bude platit pro všechny primární lokality v hierarchii.  

| Typ lokality | Status |
| --------- | ------ |
|Lokalita centrální správy|Není k dispozici|
|**Primární lokalita**|Povoleno|
|Sekundární lokalita|Není k dispozici|


## <a name="see-also"></a>Viz také

[Úlohy údržby](maintenance-tasks.md)
