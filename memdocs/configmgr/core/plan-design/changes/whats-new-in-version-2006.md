---
title: Novinky ve verzi 2006
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 2006 Configuration Manager aktuální větve.
ms.date: 09/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c061236202e685a6b59eeca3254a80cc1ddabf9
ms.sourcegitcommit: 9d5c7a5e6ec430dc02d6d345028f6b29f6579b20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385358"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Co je nového ve verzi 2006 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 2006 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1810 nebo novější. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->Tento článek shrnuje změny a nové funkce v Configuration Manager verze 2006.

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 2006](../../servers/manage/checklist-for-installing-update-2006.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

> [!TIP]
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Připojení tenanta Microsoft Endpoint Manageru

### <a name="tenant-attach-microsoft-defender-antivirus-policies-in-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Připojení tenanta: zásady antivirové ochrany v Microsoft Defenderu v centru pro správu Microsoft Endpoint Manageru
<!--4812909-->
Nyní můžete vytvořit zásady ochrany před viry v programu Microsoft Defender v konzole Microsoft Endpoint Manager a nasadit je do kolekcí Configuration Manager. Další informace, včetně podrobných pokynů a dostupných nastavení, najdete v následujících článcích:
- [Připojení tenanta: zprovoznění klientů Configuration Manager do služby Microsoft Defender ATP z centra pro správu (Preview)](../../../tenant-attach/atp-onboard.md)
- [Připojení tenanta: nasazení zásad ochrany koncového bodu Endpoint Security z centra pro správu (Preview)](../../../tenant-attach/deploy-antivirus-policy.md)
- [Nastavení pro zásady antivirové ochrany v programu Microsoft Defender pro zařízení připojená klientovi v Microsoft Intune](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json). 

### <a name="install-applications-from-the-admin-center"></a>Instalace aplikací z centra pro správu
<!--7518897, 6024389-->
Instalaci aplikace můžete iniciovat v reálném čase pro zařízení připojené k tenantovi z centra pro správu Microsoft Endpoint Manageru. Počínaje verzí 2006 Configuration Manager seznam aplikací dostupných pro zařízení zahrnuje i aplikace nasazené do aktuálně přihlášeného uživatele zařízení. Další informace najdete v tématu věnovaném [připojení tenanta: instalace aplikace z centra pro správu](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a>Importovat dřív vytvořenou aplikaci Azure AD během připojování klienta
<!--6479246-->
Během nového zprovoznění může správce během připojování k tenantovi zadat dříve vytvořenou aplikaci. Další informace najdete v tématu [připojení tenanta Microsoft Endpoint Manager: synchronizace zařízení a akce zařízení](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Analýza koncových bodů

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>Ve výchozím nastavení je povolené shromažďování dat služby Endpoint Analytics.
<!--7065447, 7741111-->
Ve výchozím nastavení je teď povolené nastavení klienta **Povolit shromažďování dat pro službu analýza koncových bodů** . Toto nastavení umožňuje spravovaným koncovým bodům odesílat data, jako jsou například přehledy o výkonu při spuštění, na váš Configuration Manager Server lokality. Tato změna má vliv pouze na místní shromažďování dat. Data služby Endpoint Analytics se neodesílají do centra pro správu Microsoft Endpoint Manageru, dokud [nepovolíte nahrávání dat v Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). Nová výchozí hodnota se vztahuje na výchozí nastavení klienta a všechna vlastní nastavení klienta vytvořená po upgradu na verzi 2006.

- Pokud upgradujete z verze 2002 na verzi 2006, jsou zachovány existující hodnoty vlastního nastavení klienta. Výchozí hodnota pro **možnost Povolit shromažďování dat služby Endpoint Analytics** ve verzi Configuration Manager 2002 je **ne**.
- Pokud upgradujete na verzi 2006 z verze Configuration Manager 1910 nebo předchozí, všechna předplatná vlastní nastavení klienta, která obsahují skupinu **Počítačový agent** nastavení, zdědí nové výchozí nastavení **Ano** pro **shromažďování dat služby Endpoint Analytics**.

Další informace najdete v tématu [Konfigurace shromažďování dat služby Endpoint Analytics v Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruktura webu

### <a name="vpn-boundary-type"></a>Typ hranice sítě VPN

<!--7020519-->

Chcete-li zjednodušit správu vzdálených klientů, můžete nově vytvořit nový typ hranice pro sítě VPN. Dřív jste museli vytvořit hranice pro klienty VPN na základě IP adresy nebo podsítě. Tato konfigurace může být náročná nebo není možná, protože se jedná o konfiguraci podsítě nebo návrh sítě VPN.

Když teď klient pošle požadavek na umístění, bude obsahovat další informace o jeho konfiguraci sítě. Na základě těchto informací server určí, jestli je klient na síti VPN.

Další informace najdete v tématu [definice hranic](../../servers/deploy/configure/boundaries.md).

### <a name="management-insights-to-optimize-for-remote-workers"></a>Přehledy správy pro optimalizaci pro vzdálené pracovníky

<!--6982226-->

Tato verze přidává novou skupinu přehledů správy, **optimalizaci pro vzdálené pracovníky**. Tyto přehledy vám pomůžou vytvořit lepší prostředí pro vzdálené pracovníky a snížit zatížení vaší infrastruktury. Přehledy v této verzi se primárně zaměřují na síť VPN:

- **Definování skupin hranic sítě VPN**
- **Konfigurace klientů VPN připojených k preferovat cloudovým zdrojům obsahu**
- **Zakázat sdílení obsahu peer-to-peer pro klienty připojené k síti VPN**

Další informace najdete v tématu [přehledy správy](../../servers/manage/management-insights.md).

### <a name="improved-support-for-windows-virtual-desktop"></a>Vylepšená podpora pro virtuální počítače s Windows

<!--6527576-->

Platforma pro **více relací Windows 10 Enterprise** je dostupná v seznamu podporovaných verzí operačního systému u objektů s pravidly požadavků nebo seznamy použitelnosti.

Další informace o podpoře Configuration Manager pro virtuální počítače s Windows najdete v tématu [podporované verze operačních systémů pro klienty a zařízení](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Intranetové klienty můžou používat CMG bod aktualizace softwaru.
<!--7102873-->
Intranetové klienty mají nyní přístup k bodu aktualizace softwaru CMG při jeho přiřazení ke skupině hranic. Další informace najdete v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Správa připojená ke cloudu

### <a name="use-the-company-portal-app-on-co-managed-devices"></a>Použití aplikace Portál společnosti na spoluspravovaných zařízeních

<!--CMADO-3601237,INADO-4297660-->

Portál společnosti je teď prostředí portálu pro aplikace pro různé platformy pro Microsoft Endpoint Manager. Když nakonfigurujete spoluspravovaná zařízení, aby se taky používala Portál společnosti, můžete na všech zařízeních zajistit konzistentní uživatelské prostředí.

Další informace najdete v tématu [použití portál společnosti aplikace na spoluspravovaných zařízeních](../../../comanage/company-portal.md).

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Použití Microsoft Azure Čína 21Vianet pro spolusprávu
<!--7133238-->
Při povolování spolusprávy teď můžete jako prostředí Azure vybrat cloud Azure Čína. Další informace najdete v tématu [Jak povolit spolusprávu](../../../comanage/how-to-enable.md).

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Oznámení o vypršení platnosti tajného klíče aplikace Azure AD

<!--6386392-->

Pokud nakonfigurujete služby Azure pro cloudové připojení lokality, konzola Configuration Manager nyní zobrazuje oznámení v následujících situacích:

- Brzo vyprší platnost jednoho nebo více tajných klíčů aplikací Azure AD.
- Platnost jednoho nebo více tajných klíčů aplikace Azure AD vypršela.

Další informace najdete v tématu [obnovení tajného klíče](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="desktop-analytics"></a>Desktop Analytics

Další informace o měsíčních změnách v cloudové službě Desktop Analytics najdete v tématu [co je nového v Desktop Analytics](../../../desktop-analytics/whats-new.md).

#### <a name="change-to-diagnostic-data-labels"></a>Změnit na popisky diagnostických dat

<!-- 7363467 -->

Chcete-li lépe zarovnávat požadavky na analýzu plochy pro diagnostická data Windows, tato nastavení mají nové popisky:

| Verze 2006 a novější | Verze 2002 a starší |
|---------|---------|
| Vyžadováno | Základní |
| Volitelné (omezené) | Rozšířené (omezené) |
| – | Rozšířené |
| Volitelné | Do bloku |

Pokud jste dříve nakonfigurovali všechna zařízení na **vyšší** úrovni při upgradu na verzi 2006, vrátí se k **volitelnému (omezenému)**. Pak budou do Microsoftu posílat méně dat. Tato změna by neměla mít vliv na to, co vidíte v Desktop Analytics.

Další informace najdete v tématu [Povolení sdílení dat pro desktopovou analýzu](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Správa v reálném čase

### <a name="improvements-to-cmpivot"></a>Vylepšení CMPivot
<!--6518631-->
V CMPivot se provedla následující vylepšení:

- CMPivot z konzoly a samostatně CMPivot byly sblíženy
- Spuštění CMPivot z jednotlivého zařízení nebo více zařízení bez nutnosti vybrat nebo vytvořit kolekci
- Z výsledků dotazu CMPivot můžete vybrat jednotlivá zařízení nebo více zařízení a pak spustit samostatnou instanci CMPivot s rozsahem pro váš výběr.

Další informace najdete v tématu [CMPivot počínaje verzí 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="client-management"></a><a name="bkmk_client"></a> Správa klientů

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a>Instalace a upgrade klienta na připojení účtované podle objemu dat

<!--6976145-->

Pokud jste dřív připojili zařízení k měřené síti, nenainstaluje se noví klienti. Stávající klienti se upgradovali jenom v případě, že jste povolili veškerou komunikaci s klienty. U zařízení, která jsou často roamingovaná v síti s měřením, by byla nespravována nebo starší verze klienta. Od této verze můžete nainstalovat a upgradovat klienta, pokud nastavíte klientské nastavení **komunikace klienta u měřených internetových připojení** na **povolené** nebo **omezené**. S tímto nastavením můžete klientovi dovolit, aby zůstal aktuální, ale pořád spravovat komunikaci klienta v účtované síti.

Chcete-li definovat chování pro novou instalaci klienta, je k dispozici nový parametr CCMSetup **/AllowMetered**. Když povolíte komunikaci klienta v monitorovaných sítích pro CCMSetup, stáhne se obsah, zaregistruje se v lokalitě a stáhne počáteční zásady. Veškerá další komunikace klienta se řídí konfigurací nastavení klienta z těchto zásad.

Další informace najdete v následujících článcích:

- [O nastavení klientů](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [O parametrech a vlastnostech instalace klienta](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Vylepšení správy restartování zařízení

<!--3601213-->

Configuration Manager poskytuje mnoho možností správy restartování zařízení a oznámení o restartování. Teď můžete nakonfigurovat nastavení klienta, aby se zabránilo automatickému restartování zařízení, když to nasazení vyžaduje. Toto nastavení poskytuje větší kontrolu v jedinečných situacích. Ve výchozím nastavení **může Configuration Manager nastavení klienta vynutit** , aby bylo zařízení restartování povoleno, takže Configuration Manager může i nadále Vynutit restartování zařízení. Toto nastavení platí jenom pro aplikace, aktualizace softwaru a nasazení balíčků, které vyžadují restart.

Další informace najdete v tématu [oznámení o restartování zařízení](../../clients/deploy/device-restart-notifications.md).

## <a name="application-management"></a><a name="bkmk_app"></a> Správa aplikací

### <a name="improvements-to-available-apps-via-cmg"></a>Vylepšení dostupných aplikací prostřednictvím CMG

<!--6935376-->
Tato verze opravuje problém s ověřováním pomocí centra softwaru a Azure Active Directory (Azure AD). Pro klienta, který se zjistil jako na intranetu, ale komunikuje přes bránu pro správu cloudu (CMG), by dřív používalo ověřování systému Windows v centru softwaru. Když se pokusí získat seznam aplikací dostupných uživateli, selže. Teď používá pro zařízení připojená k Azure AD identitu Azure Active Directory (Azure AD). Tato zařízení můžou být připojená ke cloudu nebo se připojila k hybridnímu připojení.

Další informace najdete v tématu [nasazení aplikací dostupných pro uživatele](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Aplikace Microsoft 365 pro podniky
<!--6298093-->
Sada Office 365 ProPlus byla přejmenována na Microsoft 365 aplikace pro společnost 21. dubna 2020. Počínaje verzí 2006 byly provedeny následující změny:

- Konzola Configuration Manager byla aktualizována tak, aby používala nový název.
  - Tato změna zahrnuje taky aktualizace názvů kanálů pro Microsoft 365 aplikace.
- Do konzoly se přidalo oznámení banneru, které vás upozorní, pokud jedno nebo víc pravidel automatického nasazení odkazuje na zastaralé názvy kanálů **v kritériích** pro Microsoft 365 aktualizace aplikací.

Další informace najdete v tématu [Microsoft 365 aplikace názvy kanálů](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) a [řídicí panel připravenosti pro Microsoft 365 aplikace](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Nasazení operačního systému

### <a name="task-sequence-media-support-for-cloud-based-content"></a>Podpora médií pořadí úloh pro cloudový obsah

<!--6209223-->

Médium pořadí úloh teď může stahovat cloudový obsah. Například odešlete klíč USB uživateli ve vzdálené kanceláři, který obnoví image zařízení. Nebo Office, který má místní server PXE, ale chcete, aby zařízení mohla upřednostňovat Cloud Services co nejvíce. Místo dalšího zdanění sítě WAN ke stažení velkého obsahu nasazení operačního systému, spouštěcí média a nasazení PXE teď můžou získávat obsah z cloudových zdrojů. Například brána pro správu cloudu (CMG), kterou povolíte pro sdílení obsahu.

> [!NOTE]
> Zařízení ještě potřebuje intranetové připojení k bodu správy.

Další informace najdete v tématu [použití spouštěcího média k nasazení Windows přes síť](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

### <a name="improvements-to-task-sequences-via-cmg"></a>Vylepšení pořadí úloh prostřednictvím CMG

Tato verze zahrnuje následující vylepšení pro nasazení pořadí úloh do zařízení, která komunikují přes bránu pro správu cloudu (CMG):

- Podpora pro nasazení operačního systému<!--6997525-->: S pořadím úloh, které používá spouštěcí bitovou kopii k nasazení operačního systému, ho můžete nasadit do zařízení, které komunikuje přes CMG. Uživatel musí spustit pořadí úloh z centra softwaru. Další informace najdete v tématu [Plan for CMG – specifikace](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications).

- Tato verze opravuje dva [známé problémy](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) z Configuration Manager aktuální větev verze 2002.<!-- 6983320 --> Nyní můžete spustit pořadí úkolů v zařízení, které komunikuje prostřednictvím CMG v následujících případech:

  - Zařízení pracovní skupiny, které zaregistrujete s [registračním tokenem pro hromadnou registraci](../../clients/deploy/deploy-clients-cmg-token.md)

  - Nakonfigurujete lokalitu pro [Rozšířený protokol HTTP](../hierarchy/enhanced-http.md) a bod správy je http.

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>Vylepšení kroků pořadí úloh nástroje BitLocker

<!--6995601-->

V krocích pořadí úloh **Povolit nástroj BitLocker** a **předem zřídit nástroj BitLocker** můžete teď zadat režim šifrování disku. Ve výchozím nastavení postup pokračuje v používání výchozí metody šifrování pro verzi operačního systému.

Krok **zapnout nástroj BitLocker** teď obsahuje nastavení pro **přeskočení tohoto kroku pro počítače, které nemají čip TPM, nebo když není čip TPM povolený**. Pokud povolíte toto nastavení, krok zaznamená chybu v zařízení bez čipu TPM nebo čipu TPM, který se neinicializuje, a pořadí úkolů bude pokračovat. Toto nastavení usnadňuje správu chování pořadí úkolů na zařízeních, která nemůžou plně podporovat nástroj BitLocker.

Další informace najdete v tématu [kroky pořadí úkolů](../../../osd/understand/task-sequence-steps.md).

### <a name="management-insight-rules-for-os-deployment"></a>Pravidla přehledu správy pro nasazení operačního systému

<!--6982275-->

Když velikost zásad pořadí úkolů překročí 32 MB, klient nedokáže zpracovat velkou zásadu. Klient pak nemůže spustit nasazení pořadí úloh. Tato verze obsahuje následující přehledy správy, které vám pomůžou spravovat velikost zásad pořadí úkolů.

- **Velká pořadí úkolů můžou přispět k překročení maximální velikosti zásad.**

- **Celková velikost zásad pro pořadí úloh překračuje limit zásad.**

> [!TIP]
> Tato pravidla jsou v nové skupině pro **nasazení operačního systému**. Stávající pravidlo pro **nepoužívané spouštěcí image** je nyní v této skupině.

Další informace najdete v tématu [Přehled správy](../../servers/manage/management-insights.md#operating-system-deployment).

### <a name="improvements-to-os-deployment"></a>Vylepšení nasazení operačního systému

Tato verze zahrnuje následující dodatečná vylepšení nasazení operačního systému:

- Pomocí proměnné pořadí úkolů určete cíl kroku [Formátovat a rozdělit disk na oddíly](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) . Tato nová proměnná možnost podporuje složitější pořadí úkolů s dynamickým chováním. Vlastní skript například může disk rozpoznat a nastavit proměnnou na základě typu hardwaru. Pak můžete použít více instancí tohoto kroku ke konfiguraci různých typů hardwaru a oddílů.<!--6610288-->

- Krok [Zkontrolovat připravenost](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) teď obsahuje kontrolu, abyste zjistili, jestli zařízení používá rozhraní UEFI. Obsahuje taky novou proměnnou pořadí úkolů jen pro čtení **_TS_CRUEFI**.<!--6452769-->

- Pokud zapnete [okno průběh pořadí úloh](../../../osd/understand/user-experience.md#task-sequence-progress) , aby se zobrazily podrobnější informace o průběhu, nepočítá se teď v zakázané skupině žádné povolené kroky. Tato změna pomáhá zajistit přesnější odhad průběhu.<!--6448412-->

- Dříve během sekvence úkolů při upgradu zařízení na Windows 10 se okno příkazového řádku, které se otevřelo během jedné z konečných fází konfigurace Windows. Okno se nacházelo nad systémem Windows počátečního prostředí (OOBE) a uživatelé by s ním mohli narušit proces upgradu. Nyní skripty SetupCompleteTemplate. cmd a SetupRollbackTemplate. cmd z Configuration Manager obsahují změnu pro skrytí tohoto okna příkazového řádku.<!--2837795-->

- Někteří zákazníci sestavují vlastní rozhraní pořadí úkolů pomocí metody **IProgressUI:: ShowMessage** , ale nevrací hodnotu pro odpověď uživatele. Tato verze přidává metodu [IProgressUI:: ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) . Tato nová metoda je podobná existující metodě, ale také obsahuje novou celočíselnou proměnnou s hodnotou **pResult**.<!--6448458-->

## <a name="protection"></a>Ochrana

### <a name="cmg-support-for-endpoint-protection-policies"></a>Podpora CMG pro zásady ochrany koncových bodů

<!--4773948-->

I když brána pro správu cloudu (CMG) podporuje zásady ochrany koncových bodů, zařízení vyžadovala přístup k místním řadičům domény. Od této verze můžou klienti, kteří komunikují prostřednictvím CMG, okamžitě použít zásady ochrany koncových bodů bez aktivního připojení ke službě Active Directory.

Další informace najdete v tématu [Podpora CMG pro funkce Configuration Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### <a name="bitlocker-management-support-for-hierarchies"></a>Podpora správy BitLockeru pro hierarchie

<!-- 5925693 -->

Nyní můžete nainstalovat Samoobslužný portál BitLocker a web pro správu a monitorování v lokalitě centrální správy.

Další informace najdete v tématu [Nastavení portálů BitLockeru](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Konzola Configuration Manager

### <a name="community-hub-and-github"></a>Komunitní centrum a GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(Poprvé představeno v červnu 2020)*

Komunita správce IT vyvinula spoustu znalostí během let. Místo rezásobování položek, jako jsou skripty a sestavy od začátku, jsme sestavili Configuration Manager **Centrum komunity** , kde můžete navzájem sdílet. Využitím práce ostatních můžete ušetřit hodiny práce. Centrum komunity podporuje kreativitu tím, že sestaví na práci ostatních a má na vás jiné uživatele. GitHub již obsahuje procesy a nástroje pro sdílení v celém oboru. Centrum komunity teď bude tyto nástroje využívat přímo v konzole Configuration Manager jako základní části pro řízení této nové komunity. V případě počáteční verze se obsah, který je dostupný v centru komunity, nahraje jenom Microsoftem. 

Další informace najdete v tématu [komunitní centrum a GitHub](../../servers/manage/community-hub.md).

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Přímé odkazy na položky centra komunity
<!--4224406-->
Můžete snadno přejít na položky v uzlu centra komunity konzoly Configuration Manager a odkazovat na ně s přímým odkazem. Další informace najdete v tématu [přímé odkazy na položky centra komunity](../../servers/manage/community-hub.md#bkmk_deeplink).

### <a name="notifications-from-microsoft"></a>Oznámení od Microsoftu
<!--3953121-->
Nyní se můžete rozhodnout, že chcete dostávat oznámení od Microsoftu v konzole Configuration Manager. Tato oznámení vám pomůžou udržovat informace o nových nebo aktualizovaných funkcích, změnách Configuration Manager a připojených službách a problémech, které vyžadují nápravu.

Další informace najdete v tématu [Konfigurace lokality pro příjem zpráv od Microsoftu](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### <a name="power-bi-sample-reports"></a>Ukázkové sestavy Power BI
<!--5679791-->

*(Poprvé představeno v červnu 2020)*

Při integraci Server sestav Power BI s vytvářením sestav Configuration Manager jsou nyní k dispozici ukázkové Power BI sestavy. Stáhněte a nainstalujte následující ukázkové sestavy:

- Stav Update Compliance softwaru
- Stav nasazení aktualizace softwaru

Další informace najdete v tématu [Instalace ukázkových sestav Power BI](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Zastaralé operační systémy

Přečtěte si o změnách podpory před jejich implementací v [odebraných a zastaralých položkách](deprecated/removed-and-deprecated.md).

Jak bylo poprvé oznámeno ve verzi 1906, verze 2006 zanechá podporu pro následující verze operačního systému klienta:  

- Systém Windows CE 7,0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Další aktualizace

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell verze 2006](/powershell/sccm/2006-release-notes?view=sccm-ps).

Další informace o změnách REST API služby správy najdete v tématu poznámky k [verzi služby správy](../../../develop/adminservice/release-notes.md#bkmk_2006).

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 2006](https://support.microsoft.com/help/4578830).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Další kroky

<!-- At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring). -->

Od 31. srpna 2020 je verze 2006 k dispozici pro všechny zákazníky, kteří chtějí instalovat.

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.
>
> Přečtěte si další informace:
>
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Známé důležité problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).
