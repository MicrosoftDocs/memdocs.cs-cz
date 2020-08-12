---
title: Novinky ve verzi 2002
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 2002 Configuration Manager aktuální větve.
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fcd9b7d4d25decb3aeef7cf38b469363eeb1fa
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128895"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Co je nového ve verzi 2002 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 2002 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1810 nebo novější. <!-- baseline only statement:-->Při instalaci nové lokality je také k dispozici jako základní verze. Tento článek shrnuje změny a nové funkce v Configuration Manager verze 2002.

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 2002](../../servers/manage/checklist-for-installing-update-2002.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

> [!TIP]
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Připojení tenanta Microsoft Endpoint Manageru

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Akce zařízení a synchronizace zařízení
<!--3555758-->
Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. Od této verze můžete zařízení Configuration Manager nahrát do cloudové služby a provádět akce z okna **zařízení** v centru pro správu.

Další informace najdete v tématu věnovaném [připojení tenanta Microsoft Endpoint Manageru](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Infrastruktura webu

### <a name="remove-a-central-administration-site"></a>Odebrat lokalitu centrální správy
<!-- 3607277 -->

Pokud se vaše hierarchie skládá z lokality centrální správy (CAS) a jedné podřízené primární lokality, můžete nyní odebrat certifikační autority. Tato akce zjednodušuje infrastrukturu Configuration Manager pro jednu samostatnou primární lokalitu. Odstraňuje složitosti replikace mezi lokalitami a zaměřuje se na úlohy správy na jednu primární lokalitu.

Další informace najdete v tématu [Odebrání certifikačních autorit](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Nová pravidla přehledu správy

Tato verze zahrnuje následující pravidla přehledu správy:

- Devět pravidel ve skupině pro **posouzení Configuration Manager** v rámci Microsoft Premier Field Engineering. Tato pravidla jsou ukázkou mnoha dalších kontrol, které Microsoft Premier nabízí v centru služeb.<!-- 3607758 -->

  - Zjišťování skupiny zabezpečení služby Active Directory je nakonfigurováno tak, aby běželo příliš často.
  - Zjišťování systémových souborů služby Active Directory je nakonfigurováno tak, aby běželo příliš často.
  - Zjišťování uživatelů služby Active Directory je nakonfigurováno tak, aby běželo příliš často.
  - Kolekce omezené na všechny systémy nebo všechny uživatele
  - Zjišťování prezenčního signálu je zakázané.
  - Dlouho běžící dotazy kolekce jsou povoleny pro přírůstkové aktualizace.
  - Snížení počtu aplikací a balíčků v distribučních bodech
  - Problémy při instalaci sekundárního webového serveru
  - Aktualizovat všechny lokality na stejnou verzi

- Dvě další pravidla ve skupině **Cloud Services** , která vám pomůžou nakonfigurovat web pro přidání zabezpečené komunikace protokolu https:<!-- 6268489 -->

  - Lokality, které nemají správnou konfiguraci HTTPS
  - Zařízení neodeslaná do Azure AD

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Vylepšení služby pro správu

<!-- 5728365 -->

Služba správy je REST API pro poskytovatele služby SMS. Dřív jste museli implementovat jednu z následujících závislostí:

- Povolit rozšířený protokol HTTP pro celou lokalitu
- Ruční vytvoření vazby certifikátu založeného na infrastruktuře veřejných klíčů ke službě IIS na serveru, který je hostitelem role poskytovatele služby SMS

Od této verze služba pro správu automaticky používá certifikát podepsaný držitelem webu. Tato změna pomáhá snižovat tření za účelem snazšího používání služby pro správu. Lokalita vždy generuje tento certifikát. Rozšířené nastavení serveru HTTP, které **používá Configuration Manager certifikáty pro systémy lokality http** , řídí pouze to, zda systémy lokality používají nebo ne. Teď služba pro správu ignoruje toto nastavení lokality, protože vždycky používá certifikát lokality i v případě, že rozšířené HTTP nepoužívá žádný jiný systém lokality. Stále můžete použít certifikát ověřování serveru založený na infrastruktuře PKI.

Další informace najdete v následujících článcích:

- [Co je služba pro správu?](../../../develop/adminservice/overview.md)
- [Postup nastavení služby správy](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Podpora proxy serveru pro zjišťování Azure Active Directory a synchronizaci skupin

<!-- 5913817 -->

Nastavení proxy serveru systému lokality, včetně ověřování, teď používá:

- Zjišťování uživatelů Azure Active Directory (Azure AD)
- Zjišťování skupin uživatelů Azure AD
- Synchronizace výsledků členství kolekce do skupin Azure Active Directory

Další informace najdete v tématu [Podpora proxy serveru](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Správa připojená ke cloudu

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Kritická Stavová zpráva zobrazuje chyby připojení serveru k požadovaným koncovým bodům.

<!-- 5566763 -->

Pokud se serveru lokality Configuration Manager nepovede připojit k požadovaným koncovým bodům pro cloudovou službu, vyvolá kritickou stavovou zprávu s ID 11488. Pokud se server lokality nemůže připojit ke službě, stav součásti SMS_SERVICE_CONNECTOR se změní na kritický. Zobrazit podrobný stav v uzlu Stav součásti konzoly Configuration Manager.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Ověřování založené na tokenech pro bránu pro správu cloudu

<!-- 5686290 -->

Brána pro správu cloudu (CMG) podporuje mnoho typů klientů, ale i s rozšířenými HTTP, tito klienti vyžadují certifikát pro ověřování klientů. Tento požadavek na certifikát může být náročný na zřízení internetových klientů, kteří se často nepřipojují k interní síti, nelze se připojit Azure Active Directory (Azure AD) a nemusíte mít k dispozici metodu pro instalaci certifikátu vystaveného infrastrukturou veřejných klíčů.

Configuration Manager rozšiřuje svou podporu zařízení následujícími metodami:

- Registrace k interní síti pro jedinečný token
- Vytvoření hromadné registračního tokenu pro Internetová zařízení

Další informace najdete v tématu [ověřování založené na tokenech pro CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Cloudové funkce Microsoft Endpoint Configuration Manager

<!--5834830-->

Když jsou v centru pro správu Microsoft Endpoint Manageru k dispozici nové cloudové funkce nebo jiné připojené cloudové služby pro místní instalaci Configuration Manager, můžete se teď v konzole Configuration Manager přihlásit k těmto novým funkcím. Další informace o povolení funkcí v konzole Configuration Manager najdete v tématu [Povolení volitelných funkcí z aktualizací](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

Další informace o měsíčních změnách v cloudové službě Desktop Analytics najdete v tématu [co je nového v Desktop Analytics](../../../desktop-analytics/whats-new.md).

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Řídicí panel stavu připojení zobrazuje problémy s připojením klienta.

Pomocí řídicího panelu stavu připojení Desktop Analytics v Configuration Manager můžete monitorovat stav připojení klientů. Teď vám pomůže snadněji identifikovat problémy s konfigurací klientského proxy serveru ve dvou oblastech:

- **Kontroly připojení koncových bodů**: Pokud klienti nemůžou kontaktovat požadovaný koncový bod, zobrazí se na řídicím panelu upozornění na konfiguraci. Přechodem k podrobnostem zobrazíte koncové body, ke kterým se klienti nemůžou připojit kvůli problémům s konfigurací proxy serveru.<!-- 4963230 -->

- **Stav připojení**: Pokud vaši klienti k přístupu ke cloudové službě Desktop Analytics používají proxy server, Configuration Manager teď v klientech zobrazuje problémy s ověřováním proxy serveru. Přechodem k podrobnostem zobrazíte klienty, kteří se nemohou zaregistrovat kvůli ověřování proxy.<!-- 4963383 -->

Další informace najdete v tématu [monitorování stavu připojení](../../../desktop-analytics/monitor-connection-health.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a>Správa v reálném čase

### <a name="improvements-to-cmpivot"></a>Vylepšení CMPivot

<!-- 5870934 -->

Usnadnili jsme navigaci CMPivot entit. Nyní můžete hledat entity CMPivot. Přidaly se také nové ikony, které usnadňují odlišení entit a typů objektů entit.

Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a>Správa obsahu

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Vyloučení určitých podsítí pro stažení obsahu peer

<!-- 3555777 -->

Skupiny hranic obsahují následující možnost pro rovnocenné stahování: **během stahování peer-to se používají jenom partneři v rámci stejné podsítě**. Pokud tuto možnost povolíte, bude seznam umístění obsahu z bodu správy obsahovat jenom partnerské zdroje, které jsou ve stejné podsíti a skupině hranic jako klient. V závislosti na konfiguraci sítě teď můžete vyloučit určité podsítě pro porovnání. Například chcete zahrnout hranici, ale vyloučit konkrétní podsíť VPN.

Další informace najdete v tématu [Možnosti skupiny hranic](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Podpora proxy serveru pro propojenou mezipaměť Microsoft

<!-- 5856396 -->

Pokud vaše prostředí používá neověřené proxy server pro přístup k Internetu, teď může při povolení Configuration Manager distribučního bodu pro připojenou mezipaměť Microsoft komunikovat prostřednictvím proxy serveru. Další informace najdete v tématu [mezipaměť Microsoft připojené k síti](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a>Správa klientů

### <a name="client-log-collection"></a>Shromažďování protokolů klienta

<!-- 4226618 -->

Nyní můžete aktivovat klientské zařízení pro nahrání protokolů klienta na server lokality odesláním akce oznámení klienta z konzoly Configuration Manager.

Další informace najdete v tématu [klientské oznámení](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Probuzení zařízení z lokality centrální správy

<!-- 6030715 -->

Z lokality centrální správy (CAS) v uzlu zařízení nebo kolekce zařízení můžete nyní použít akci oznamování klienta k probuzení zařízení. Tato akce byla dřív dostupná jenom z primární lokality.

Další informace najdete v tématu [Postup konfigurace funkce Wake on LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>Vylepšení podpory pro zařízení ARM64

<!--5954175-->

Platforma **All Windows 10 (ARM64)** je dostupná v seznamu podporovaných verzí operačního systému u objektů s pravidly požadavků nebo seznamy použitelnosti.

> [!NOTE]
> Pokud jste dříve vybrali platformu **Windows 10** na nejvyšší úrovni, tato akce automaticky vybrala **všechny systémy windows 10 (64 bitů)** i **všechny systémy Windows 10 (32-bit)**. Tato nová platforma není automaticky vybraná. Pokud chcete přidat **všechny systémy Windows 10 (ARM64)**, ručně je vyberte v seznamu.

Další informace o podpoře Configuration Manager pro zařízení ARM64 najdete v tématu [Windows 10 v ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Sledování oprav položek konfigurace
<!--4261411-->
Teď můžete **sledovat historii náprav, pokud** se ve vašich pravidlech dodržování předpisů vašich položek konfigurace podporuje. Pokud je tato možnost povolena, jakákoli náprava, ke které dojde v klientovi pro položku konfigurace, vygeneruje stavovou zprávu. Historie je uložena v databázi Configuration Manager.

Další informace o tomto nastavení najdete v tématu [vytváření vlastních položek konfigurace pro stolní počítače s Windows a serverové počítače spravované pomocí klienta Configuration Manager](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a>Správa aplikací

### <a name="microsoft-edge-management-dashboard"></a>Řídicí panel pro správu Microsoft Edge

<!-- 3871913 -->

Řídicí panel pro správu Microsoft Edge vám poskytne přehled o používání Microsoft Edge a dalších prohlížečů. V tomto řídicím panelu můžete:

- Podívejte se, kolik vašich zařízení má nainstalované Microsoft Edge.
- Podívejte se, kolik klientů má nainstalované různé verze Microsoft Edge.
- Zobrazení nainstalovaných prohlížečů v různých zařízeních
- Zobrazit preferovaný prohlížeč podle zařízení

V pracovním prostoru Softwarová knihovna klikněte na Správa Microsoft Edge a zobrazte řídicí panel. Změňte kolekci dat grafu kliknutím na Procházet a výběrem jiné kolekce. Ve výchozím nastavení se v rozevíracím seznamu nacházejí pět největších kolekcí. Když vyberete kolekci, která není v seznamu, nově vybraná kolekce vezme v rozevíracím seznamu na spodní místo.

Další informace najdete v tématu [Správa Microsoft Edge](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### <a name="improvements-to-microsoft-edge-management"></a>Vylepšení správy Microsoft Edge

<!-- 4561024 -->

Teď můžete vytvořit aplikaci Microsoft Edge, která je nastavená tak, aby přijímala automatické aktualizace místo automatických aktualizací. Tato změna vám umožní spravovat aktualizace pro Microsoft Edge pomocí Configuration Manager nebo povolit automatické aktualizace Microsoft Edge. Když vytváříte aplikaci, vyberte možnost dovolit, aby Microsoft Edge automaticky aktualizoval verzi klienta na zařízení koncového uživatele na stránce nastavení Microsoft Edge.

Další informace najdete v tématu [Správa Microsoft Edge](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Pořadí úkolů jako typ nasazení modelu aplikace

<!-- 3555953 -->

Pomocí pořadí úkolů teď můžete pomocí aplikačního modelu nainstalovat složitá aplikace. Přidejte typ nasazení do aplikace, která je pořadím úkolů, a to buď k instalaci nebo odinstalaci aplikace. Tato funkce poskytuje následující chování:

- Zobrazí pořadí úkolů aplikace s ikonou v centru softwaru. Ikona usnadňuje uživatelům hledání a identifikaci pořadí úkolů aplikace.

- Definujte další metadata pro pořadí úkolů aplikace, včetně lokalizovaných informací.

Další informace najdete v tématu [vytváření aplikací pro Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a>Nasazení operačního systému

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Spustit pořadí úloh hned po registraci klienta

<!-- 5526972 -->

Když nainstalujete a zaregistrujete nového klienta Configuration Manager a také nasadíte pořadí úkolů, je obtížné zjistit, jak brzy po registraci spustí pořadí úkolů. Tato verze zavádí novou vlastnost instalace klienta, kterou můžete použít ke spuštění pořadí úkolů na klientovi po úspěšné registraci v lokalitě.

Další informace najdete v tématu [o vlastnostech instalace klienta – PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Vylepšení kontroly připravenosti kroku pořadí úkolů

<!-- 6005561 -->

V kroku pořadí úkolů **Zkontrolovat připravenost** teď můžete ověřit více vlastností zařízení. Tento krok použijte v pořadí úkolů k ověření, jestli cílový počítač splňuje vaše požadavky.

- Architektura aktuálního operačního systému
- Minimální verze operačního systému
- Maximální verze operačního systému
- Minimální verze klienta
- Jazyk aktuálního operačního systému
- Napájení ze sítě AC
- Síťový adaptér je připojený a není bezdrátový.

Další informace najdete v tématu [kroky pořadí úkolů – zkontrolujte připravenost](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Vylepšení průběhu pořadí úkolů

<!-- 5932692 -->

Okno průběh pořadí úkolů teď obsahuje následující vylepšení:

- Můžete povolit, aby zobrazil aktuální číslo kroku, celkový počet kroků a procento dokončení.
- Zvětšením šířky okna získáte více místa, aby bylo možné lépe zobrazit název organizace na jednom řádku.

Další informace najdete v tématu [uživatelské prostředí pro nasazení operačního systému](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>Vylepšení nasazení operačního systému

Tato verze zahrnuje následující vylepšení nasazení operačního systému:

- Prostředí pořadí úkolů zahrnuje novou proměnnou určenou jen pro čtení `_TSSecureBoot` .<!--5842295--> Pomocí této proměnné můžete určit stav zabezpečeného spouštění na zařízení s podporou rozhraní UEFI. Další informace najdete v tématu [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Nastavte proměnné pořadí úkolů pro konfiguraci kontextu uživatele pro **spuštění příkazového řádku** a **spuštění kroků skriptu PowerShellu** .<!-- 5573175 --> Další informace najdete v tématu [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) a [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- V kroku **Spustit skript PowerShellu** teď můžete nastavit vlastnost **Parameters** na proměnnou.<!-- 5690481 --> Další informace najdete v tématu [spuštění skriptu PowerShellu](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Configuration Manager respondér PXE nyní odesílá stavové zprávy serveru lokality. Tato změna usnadňuje řešení potíží s nasazeními OS, která tuto službu používají.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Aktualizace softwaru

### <a name="orchestration-groups"></a>Skupiny orchestrace

<!-- 3098816 -->

Vytvořte skupinu Orchestration, která vám umožní lépe řídit nasazení softwarových aktualizací do zařízení. Mnoho správců serveru musí pečlivě spravovat aktualizace pro konkrétní úlohy a automatizovat chování mezi.

Skupina Orchestration poskytuje flexibilitu při aktualizaci zařízení na základě procenta, konkrétního čísla nebo explicitního pořadí. Můžete také spustit skript prostředí PowerShell před a po spuštění nasazení aktualizace na zařízeních.

Členy skupiny orchestration může být jakýkoli Configuration Manager klient, nikoli jenom Server. Pravidla skupiny Orchestration se vztahují na zařízení pro všechna nasazení aktualizací softwaru na všechny kolekce, které obsahují člena skupiny Orchestration. Stále platí jiné chování nasazení. Například časová období údržby a plány nasazení.

Další informace najdete v tématu [skupiny Orchestration](../../../sum/deploy-use/orchestration-groups.md).

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Vyhodnotit aktualizace softwaru po aktualizaci servisního zásobníku

<!-- 4639943 -->

Configuration Manager nyní zjistí, zda je aktualizace cestou nadřazené (Servicing Stack) součástí instalace více aktualizací. Po zjištění cestou nadřazené se nainstalují jako první. Po instalaci cestou nadřazené se spustí cyklus vyhodnocení aktualizace softwaru, který nainstaluje zbývající aktualizace. Tato změna umožňuje instalaci závislé kumulativní aktualizace po aktualizaci zásobníku pro údržbu. Zařízení není nutné restartovat mezi instalacemi a nemusíte vytvářet další časové období údržby. SSUs se instalují jenom pro instalace, které neinicioval uživatel. Například pokud uživatel zahájí instalaci pro více aktualizací z centra softwaru, cestou nadřazené nemusí být nainstalován jako první.

Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Aktualizace Office 365 pro odpojené body aktualizace softwaru

<!-- 4065163 -->

Pomocí nového nástroje můžete importovat aktualizace Office 365 ze serveru WSUS připojeného k Internetu do odpojeného Configuration Managerho prostředí. Dříve, když jste exportovali a importovali metadata pro software aktualizovaný v odpojených prostředích, nemůžete nasadit aktualizace Office 365. Aktualizace Office 365 vyžadují další metadata stažená z rozhraní Office API a CDN Office, což není u odpojených prostředí možné.

Další informace najdete v tématu [synchronizace aktualizací Office 365 z odpojeného bodu aktualizace softwaru](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a>Antivirový

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Rozbalit registraci v programu Microsoft Defender Advanced Threat Protection (ATP)
 
<!-- 5229962 -->
Configuration Manager rozšířila podporu pro zařízení s připojováním do ochrany ATP v programu Microsoft Defender. Další informace najdete v tématu [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a>Připojení klientů Configuration Manager k ochraně ATP v programu Microsoft Defender prostřednictvím centra pro správu Microsoft Endpoint Manageru
<!--5691658-->
Teď můžete nasadit zásady registrace a odezvy EDR (Microsoft Defender ATP) pro Configuration Manager spravované klienty. Tito klienti nevyžadují registraci v Azure AD ani MDM a zásady jsou zaměřené na kolekce nástroje ConfigMgr místo skupin Azure AD.

Tato možnost umožňuje zákazníkům spravovat jak Intune MDM, tak Configuration Manager klienta EDR/ATP v rámci jediného prostředí pro správu – centra pro správu Microsoft Endpoint Manageru. Další informace najdete v tématu [zjišťování koncových bodů a zásady odezvy pro zabezpečení koncového bodu v Intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> Pro tuto funkci budete potřebovat kumulativní opravu hotfix [KB4563473](https://support.microsoft.com/help/4563473), která je nainstalovaná ve vašem prostředí.

### <a name="improvements-to-bitlocker-management"></a>Vylepšení správy BitLockeru

- Zásady správy BitLockeru teď obsahují další nastavení, včetně zásad pro pevné a vyměnitelné jednotky.<!-- 5925683 --> Další informace najdete v tématu [Reference k nastavením BitLockeru](../../../protect/tech-ref/bitlocker/settings.md).

- V Configuration Manager aktuální větve verze 1910 pro integraci služby obnovení nástroje BitLocker, kterou jste měli v rámci protokolu HTTPS – povolte bod správy. Připojení HTTPS je nezbytné k šifrování obnovovacích klíčů v síti od klienta Configuration Manager do bodu správy. Konfigurace bodu správy a všech klientů pro protokol HTTPS může být pro mnoho zákazníků náročné.

    Od této verze je požadavek HTTPS určen pro web IIS, který je hostitelem služby obnovení, nikoli celou roli bodu správy. Tato změna zmírnit požadavky na certifikát a stále zašifruje obnovovací klíče při přenosu.<!-- 5925660 --> Další informace najdete v tématu [šifrování dat pro obnovení](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a>Zpravodajský

### <a name="integrate-with-power-bi-report-server"></a>Integrace se Serverem sestav Power BI

<!-- 3721603 -->

Nyní můžete integrovat Server sestav Power BI s vytvářením sestav Configuration Manager. Tato integrace poskytuje moderní vizualizaci a lepší výkon. Přidává konzolovou podporu pro Power BI sestavy podobné tomu, co už existují s SQL Server Reporting Services.

Další informace najdete v tématu věnovaném [integraci s server sestav Power BI](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Konzola Configuration Manager

### <a name="show-boundary-groups-for-devices"></a>Zobrazit skupiny hranic pro zařízení

<!--6521835-->

Aby vám pomohl lépe řešit problémy zařízení pomocí skupin hranic, můžete si teď zobrazit skupiny hranic pro konkrétní zařízení. V uzlu **zařízení** nebo při zobrazení členů **kolekce zařízení**přidejte do zobrazení seznamu nové sloupce **hraničních skupin** .

Další informace najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Poslat vylepšení smajlíka

<!-- 5891852 -->

Když odešlete smajlíka nebo odešlete zamračení, vytvoří se při odeslání zpětné vazby stavová zpráva. Toto vylepšení poskytuje záznam o:

- Při odeslání zpětné vazby
- Kdo odeslal zpětnou vazbu
- ID zpětné vazby
- Pokud bylo odeslání zpětné vazby úspěšné nebo ne

Stavová zpráva s ID 53900 je úspěšná odeslání a 53901 je odeslání neúspěšné.

Další informace najdete v tématu o [zpětné vazbě produktu](../../understand/find-help.md#BKMK_1806Feedback).

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Prohledat všechny podsložky pro položky konfigurace a standardní hodnoty konfigurace

<!--5891241-->

Podobně jako u vylepšení v předchozích verzích teď můžete použít možnost vyhledávání **všech podsložek** v uzlech **položky konfigurace** a **standardní hodnoty konfigurace** .

### <a name="community-hub"></a>Centrum komunity

<!--3555935, 3555936-->

*(Poprvé představeno v červnu 2020)*

Komunita správce IT vyvinula spoustu znalostí během let. Místo rezásobování položek, jako jsou skripty a sestavy od začátku, jsme sestavili Configuration Manager **Centrum komunity** , kde můžete navzájem sdílet. Využitím práce ostatních můžete ušetřit hodiny práce. Centrum komunity podporuje kreativitu tím, že sestaví na práci ostatních a má na vás jiné uživatele. GitHub již obsahuje procesy a nástroje pro sdílení v celém oboru. Centrum komunity teď bude tyto nástroje využívat přímo v konzole Configuration Manager jako základní části pro řízení této nové komunity. V případě počáteční verze se obsah, který je dostupný v centru komunity, nahraje jenom Microsoftem.

Další informace najdete v tématu [komunitní centrum a GitHub](../../servers/manage/community-hub.md).

## <a name="tools"></a><a name="bkmk_tools"></a>Nástroje

### <a name="onetrace-log-groups"></a>Skupiny protokolů OneTrace

<!-- 5559993 -->

OneTrace nyní podporuje přizpůsobitelné skupiny protokolů, podobně jako funkce v nástroji Support Center. Skupiny protokolů umožňují otevřít všechny soubory protokolu pro jeden scénář. OneTrace v současné době zahrnuje skupiny pro následující scénáře:

- Správa aplikací
- Nastavení dodržování předpisů (také označované jako správa požadované konfigurace)
- Aktualizace softwaru

Další informace najdete v tématu [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>Vylepšení rozšiřování a migrace místních lokalit na Microsoft Azure
<!--5665775, 6307931-->
Nástroj pro rozšiřování a migraci místního webu na Microsoft Azure nyní podporuje zřizování více rolí systému lokality na jednom virtuálním počítači Azure. Po dokončení počátečního nasazení virtuálního počítače Azure můžete přidat role systému lokality.

Další informace najdete v tématu věnovaném [rozšiřování a migraci místního webu na Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role).

## <a name="other-updates"></a>Další aktualizace

Od této verze již nejsou k dispozici následující [funkce:](../../servers/manage/pre-release-features.md)

- [Azure Active Directory zjišťování skupiny uživatelů](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Synchronizovat výsledky členství kolekce s Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot samostatná](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Klientské aplikace pro spoluspravovaná zařízení](../../../comanage/workloads.md#client-apps) (dříve označovaná jako *mobilní aplikace pro spoluspravovaná zařízení*)<!-- 1357892/3600959 -->

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell verze 2002](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

Další informace o změnách REST API služby správy najdete v tématu poznámky k [verzi služby správy](../../../develop/adminservice/release-notes.md#bkmk_2002).

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 2002](https://support.microsoft.com/help/4556203).

V konzole nástroje je k dispozici následující kumulativní aktualizace (4560496) od 15. července 2020: [kumulativní aktualizace pro Microsoft Endpoint Configuration Manager verze 2002](https://support.microsoft.com/help/4560496).

### <a name="hotfixes"></a>Opravy hotfix

K vyřešení konkrétních problémů jsou k dispozici následující další opravy hotfix:

| ID | Nadpis | Datum | V konzole |
|---------|---------|---------|---------|
| [4575339](https://support.microsoft.com/help/4575339) | Zařízení se v centru pro správu Microsoft Endpoint Configuration Manager dvakrát zobrazují. | 23. července 2020 | Ne |
| [4575774](https://support.microsoft.com/help/4575774) | Rutina New-CMTSStepPrestartCheck se nezdařila v Configuration Manager verze 2002 | 24. července 2020 | Ne |
| [4576782](https://support.microsoft.com/help/4576782) | Časový limit pro okno aplikace v centru pro správu Microsoft Endpoint Manageru | 11. srpna 2020 | No |

<!--
> [!NOTE]
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Další kroky

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

Od 11. května 2020 je verze 2002 k dispozici pro všechny zákazníky, kteří chtějí instalovat.

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.
>
> Přečtěte si další informace:
>
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Známé důležité problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
