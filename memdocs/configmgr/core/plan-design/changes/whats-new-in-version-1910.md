---
title: Novinky ve verzi 1910
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1910 Configuration Manager aktuální větve.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c99716070bf32ae27a7bd8b7a114d8b920814e2
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993467"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Co je nového ve verzi 1910 Configuration Manager Current Branch

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1910 pro Configuration Manager aktuální větev je k dispozici jako aktualizace v konzole. Tuto aktualizaci použijte na webech, na kterých běží verze 1806 nebo novější. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Tento článek shrnuje změny a nové funkce v Configuration Manager verze 1910.

Vždy si přečtěte nejnovější kontrolní seznam pro instalaci této aktualizace. Další informace najdete v tématu [Kontrolní seznam pro instalaci aktualizace 1910](../../servers/manage/checklist-for-installing-update-1910.md). Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

> [!TIP]
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Configuration Manager koncového bodu Microsoftu

<!--4960084-->

Configuration Manager je teď součástí Microsoft Endpoint Manageru.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spolupracuje Configuration Manager a Intune s zjednodušeným licencováním. Nadále Využijte své stávající investice do Configuration Manager, abyste využili sílu cloudu Microsoftu podle vlastního tempa.

Následující řešení pro správu Microsoft jsou teď součástí značky Microsoft Endpoint Manageru:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Další funkce v [konzole správce správy zařízení](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Další informace najdete v následujících příspěvcích od Brada Anderson, což je Microsoft Corporate viceprezident pro Microsoft 365:

- [Příspěvek na blogu v oznámení](https://aka.ms/cmannounce)
- [Visionový papír](https://aka.ms/MEMVisionPaper)
- [Video souhrn oznámení](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Co se mění v Configuration Manager pomocí Microsoft Endpoint Manageru?

V rámci verze 1910, Configuration Manager nadále funguje stejně jako v případě změny názvu. Některé změny názvů můžou mít vliv na používání následujících součástí:

- **Konzola Configuration Manager**: vyhledejte zástupce konzoly a **prohlížeče vzdáleného řízení** v nabídce Start systému Windows ve složce **Microsoft Endpoint Manager** .

- **Centrum softwaru**: v nabídce Windows Start ve složce **Microsoft Endpoint Manageru** Najděte zástupce centra softwaru.

![Ikony nabídky Start pro Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

Nezapomeňte aktualizovat jakoukoli interní dokumentaci, kterou udržujete, aby zahrnovala Tato nová umístění.

> [!TIP]
> V systému Windows 10 když otevřete nabídku Start, zadejte název pro vyhledání ikony. Zadejte například `Configuration Manager` nebo `Software Center`.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infrastruktura webu

### <a name="reclaim-sedo-lock"></a>Uvolnit SEDO zámek

<!--4786915-->

Od [aktuální větve verze 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)můžete zrušit zámek pro pořadí úkolů. Nyní můžete zrušit zámek pro libovolný objekt v konzole Configuration Manager.

Další informace najdete v tématu [použití konzoly Configuration Manager](../../servers/manage/admin-console.md#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Rozšiřování a migrace místního serveru na Microsoft Azure
<!--3556022-->

Tento nový nástroj vám pomůže programově vytvořit virtuální počítače Azure pro Configuration Manager. Může se nainstalovat s výchozími nastaveními role lokality, jako je pasivní server lokality, body správy a distribuční body. Po ověření nových rolí je používejte jako další systémy lokality pro zajištění vysoké dostupnosti. Můžete také odebrat roli místního systému lokality a zachovat jenom roli virtuálních počítačů Azure.

Další informace najdete v tématu věnovaném [rozšiřování a migraci místního webu na Microsoft Azure](../../support/azure-migration-tool.md).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Další informace o měsíčních změnách v cloudové službě Desktop Analytics najdete v tématu [co je nového v Desktop Analytics](../../../desktop-analytics/whats-new.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Správa v reálném čase

### <a name="optimizations-to-the-cmpivot-engine"></a>Optimalizace modulu CMPivot
<!--3197353-->
Do modulu CMPivot jsme přidali nějaké významné optimalizace. Nyní můžete do klienta nástroje ConfigMgr vložit další zpracování. Optimalizace výrazně snižují zatížení procesoru sítě a serveru potřebné ke spouštění dotazů CMPivot. S těmito optimalizacemi teď můžete v reálném čase prosift až gigabajty dat klientů. 

Další informace najdete v tématu [optimalizace pro modul CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Další entity a vylepšení CMPivot
<!--5410930-->
Přidali jsme řadu nových entit CMPivot a vylepšení entit, která pomáhají při řešení potíží a lovu. Do dotazu jsme zahrnuli následující entity:

- Protokoly událostí systému Windows ([WinEvent](../../servers/manage/cmpivot-changes.md#bkmk_WinEvent))
- Obsah souboru ([obsah](../../servers/manage/cmpivot-changes.md#bkmk_File)souboru)
- Knihovny DLL načtené procesy ([ProcessModule](../../servers/manage/cmpivot-changes.md#bkmk_ProcessModule))
- Informace o Azure Active Directory ([AADStatus](../../servers/manage/cmpivot-changes.md#bkmk_AadStatus))
- Stav služby Endpoint Protection ([EPStatus](../../servers/manage/cmpivot-changes.md#bkmk_EPStatus))

Tato verze také obsahuje několik [dalších vylepšení](../../servers/manage/cmpivot-changes.md#bkmk_Other) CMPivot. Další informace najdete v tématu [CMPivot počínaje verzí 1910](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a> Správa obsahu

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Podpora mezipaměti s připojením Microsoftu pro aplikace Intune Win32

<!--5032900-->

Když v Configuration Manager distribučních bodech povolíte propojenou mezipaměť Microsoftu, můžou teď Microsoft Intune aplikace Win32 sloužit spoluspravovaným klientům.

Další informace najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> Configuration Manager aktuální větve verze 1906 zahrnovala [optimalizaci doručování do síťové mezipaměti](../hierarchy/microsoft-connected-cache.md), aplikace nainstalovaná v systému Windows Server, která je stále ve vývoji. Od aktuální větve verze 1910 je tato funkce nyní označována jako propojená s mezipamětí Microsoft.
>
> Když nainstalujete připojenou mezipaměť do distribučního bodu Configuration Manager, přesměruje provoz služby optimalizace doručení do místních zdrojů. Propojená mezipaměť dělá toto chování efektivně při ukládání obsahu do mezipaměti na úrovni bajtového rozsahu.

## <a name="client-management"></a><a name="bkmk_client"></a> Správa klientů

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Zahrnout vlastní standardní hodnoty konfigurace jako součást posouzení zásad dodržování předpisů
<!--3608345-->

Nyní můžete přidat hodnocení vlastních standardních hodnot konfigurace jako pravidla pro vyhodnocení zásad dodržování předpisů. Když vytváříte nebo upravujete standardní hodnoty konfigurace, můžete nyní použít možnost **vyhodnotit tuto standardní hodnotu jako součást hodnocení zásad dodržování předpisů** . Když přidáte nebo upravíte pravidlo zásad dodržování předpisů, budete mít v vyhodnocení zásad dodržování předpisů k dispozici podmínky s názvem **Zahrnout nakonfigurované směrné plány**.

Pro spoluspravovaná zařízení a když nakonfigurujete Intune tak, aby byly výsledky vyhodnocení dodržování předpisů Configuration Manager v rámci celkového stavu dodržování předpisů, odesílají se tyto informace na Azure Active Directory. Pak ji můžete použít pro podmíněný přístup k prostředkům Microsoft 365.

Další informace najdete v tématu [Zahrnutí vlastních standardních hodnot konfigurace jako součásti posouzení zásad dodržování předpisů](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Povolit zásady uživatele pro více relací Windows 10 Enterprise

<!--4737447-->

Configuration Manager aktuální větev verze 1906 představila podporu pro [virtuální počítače s Windows](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop). Toto prostředí Microsoft Azure podporuje několik verzí operačního systému, z nichž některé umožňují více souběžných aktivních uživatelských relací. Například Windows 10 Enterprise Multi-Session je jedna z těchto verzí operačního systému.

Pokud na těchto zařízeních s více relacemi požadujete zásady uživatele a akceptujete případný dopad na výkon, můžete teď nakonfigurovat nastavení klienta, aby se povolilo zásady uživatele. Ve skupině **zásad klienta** nakonfigurujte nastavení **Povolit zásady uživatele pro více uživatelských relací** .

Další informace najdete v tématu [Konfigurace nastavení klienta](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> Správa aplikací

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Nasazení Microsoft Edge verze 77 a novější
<!--4561024-->
Microsoft Edge pro všechny nové je připravený pro firmy. Pro uživatele teď můžete nasadit Microsoft Edge, verze 77 a novější. Správci si můžou vybrat beta verzi, vývoj nebo stabilní kanál spolu s verzí klienta Microsoft Edge, která se má nasadit.

Další informace najdete v tématu [nasazení Microsoft Edge verze 77 a novější](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Vylepšení skupin aplikací

<!--4760058-->

Od aktuální větve verze 1906 můžete vytvořit skupinu aplikací, které budou odeslány do kolekce zařízení jako jediné nasazení. Tato verze se vylepšuje na této funkci:

- Uživatelé můžou vybrat **odinstalovat** pro skupinu aplikací v centru softwaru.
- Skupinu aplikací můžete nasadit do **kolekce uživatelů**.

Obecnější informace najdete v tématu [Vytvoření skupin aplikací](../../../apps/deploy-use/create-app-groups.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Nasazení operačního systému

### <a name="improvements-to-the-task-sequence-editor"></a>Vylepšení editoru pořadí úloh

 Editor pořadí úkolů obsahuje následující vylepšení:

- **Hledání v editoru pořadí úloh:**<!--4621085--> Pokud máte velké pořadí úkolů s mnoha skupinami a kroky, může být obtížné najít konkrétní kroky. Nyní můžete hledat v editoru pořadí úloh. Tato akce vám umožní rychleji vyhledat kroky v pořadí úkolů.
- **Podmínky pořadí úloh kopírovat a vložit:**<!--4621098--> Pokud chcete znovu použít podmínky z jednoho kroku pořadí úkolů na jiný, můžete nyní zkopírovat a vložit podmínky v editoru pořadí úloh.

Další informace najdete v novém článku o [použití editoru pořadí úloh](../../../osd/understand/task-sequence-editor.md).

### <a name="task-sequence-performance-improvements-power-plans"></a>Vylepšení výkonu pořadí úloh: schémata napájení

<!--3555926-->

Nyní můžete spustit pořadí úkolů s vysokým výkonem schématu napájení. Tato možnost vylepšuje celkovou rychlost pořadí úkolů. Nakonfiguruje Windows tak, aby používal integrované schéma napájení s vysokým výkonem, které poskytuje maximální výkon na úkor vyšší spotřeby energie.

Další informace najdete v tématu [vylepšení výkonu pro schémata napájení](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Stažení pořadí úkolů na vyžádání přes Internet

<!--3601238-->

Pořadí úkolů můžete použít k nasazení místního upgradu Windows 10 přes bránu pro správu cloudu (CMG). Nicméně vyžaduje, aby nasazení stáhlo veškerý obsah místně před spuštěním pořadí úkolů.

Od této verze může modul pořadí úkolů stahovat balíčky na vyžádání z CMG nebo cloudového distribučního bodu. Tato změna poskytuje větší flexibilitu pro nasazení místního upgradu Windows 10 na Internetová zařízení.

Další informace najdete v tématu [nasazení místního upgradu Windows 10 přes CMG](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Vylepšení nasazení operačního systému

Tato verze zahrnuje následující vylepšení nasazení operačního systému.

#### <a name="boot-image-keyboard-layout"></a>Rozložení klávesnice spouštěcí bitové kopie

<!--4910348-->

Nakonfigurujte výchozí rozložení klávesnice pro spouštěcí bitovou kopii. Na kartě **vlastní nastavení** spouštěcí image použijte novou možnost **nastavit výchozí rozložení klávesnice v prostředí WinPE** . Pokud vyberete jiný jazyk než en-US, Configuration Manager dál obsahuje en-US v dostupných vstupních národních prostředích. V zařízení je počáteční rozložení klávesnice vybraným národním prostředím, ale pokud to bude potřeba, může uživatel zařízení v případě potřeby přepnout na en-US.

Další informace najdete v tématu [Správa spouštěcích imagí](../../../osd/get-started/manage-boot-images.md#customization).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importovat jeden index balíčku s upgradem operačního systému

<!--4931110-->

Když importujete balíček s upgradem operačního systému, můžete použít možnost **extrahovat konkrétní index bitové kopie ze souboru Install. wim vybraného balíčku upgrade** . Toto chování je podobné jako u [bitových kopií operačního systému](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages), s tím rozdílem, že přepíše existující soubor Install. wim v balíčku s UPGRADEM operačního systému. Extrahuje index bitové kopie do dočasného umístění a poté je přesune do původního zdrojového adresáře.

Další informace najdete v tématu [Správa balíčků s upgradem operačního systému](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Výstup výsledků kroku Spustit příkazový řádek do proměnné během pořadí úkolů

<!--user story 4977616/bug 4798352-->

Krok **Spustit příkazový řádek** teď obsahuje možnost **výstup do proměnné pořadí úkolů** . Když tuto možnost povolíte, pořadí úkolů uloží výstup z příkazu do vlastní proměnné pořadí úkolů, kterou určíte.

Další informace najdete v tématu [spuštění příkazového řádku](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Vylepšení ladicího programu pořadí úloh

Tato verze zahrnuje následující vylepšení ladicího programu pořadí úloh:

- Použijte novou proměnnou pořadí úloh **TSDebugOnError** k automatickému spuštění ladicího programu, když pořadí úkolů vrátí chybu.<!-- 5012536 -->
- Pokud vytvoříte zarážku v ladicím programu a poté pořadí úkolů restartuje počítač, ladicí program po restartování udržuje zarážky.<!-- 5012509 -->

Další informace najdete v tématu [ladicí program sekvence úloh](../../../osd/deploy-use/debug-task-sequence.md) a [proměnné pořadí úkolů – TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Vylepšená podpora jazyků v pořadí úkolů

<!--5411057, 5138936-->

Tato verze přidává během nasazování operačního systému kontrolu před konfigurací jazyka. Pokud už tato nastavení jazyka aplikujete, může vám tato změna zjednodušit pořadí úkolů nasazení operačního systému. Místo použití více kroků pro jednotlivé jazyky nebo samostatné skripty použijte jednu instanci v rámci předdefinovaného kroku **použít nastavení systému Windows** s podmínkou pro daný jazyk.

Pomocí kroku pořadí úkolů **použít nastavení systému Windows** můžete nakonfigurovat následující nová nastavení:

- Vstupní národní prostředí (výchozí rozložení klávesnice)
- Národní prostředí systému
- Jazyk uživatelského rozhraní
- Záložní jazyk uživatelského rozhraní
- Národní prostředí uživatele

Další informace naleznete v části [Apply Windows Settings](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Nová proměnná pro místní upgrade Windows 10

<!--4680263-->

Chcete-li vyřešit problémy s časováním v rámci pořadí úkolů pro zařízení s vysokým výkonem na zařízeních s vysokým výkonem po dokončení instalace systému Windows, můžete nyní nastavit novou proměnnou pořadí úloh **SetupCompletePause**. Když přiřadíte hodnotu v sekundách k této proměnné, proces instalace systému Windows zpozdí prodlevu před spuštěním pořadí úloh. Tento časový limit poskytuje Configuration Manager klientovi další čas k inicializaci.

Další informace najdete v tématu [proměnné pořadí úkolů – SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Aktualizace softwaru

### <a name="additional-options-for-third-party-update-catalogs"></a>Další možnosti pro katalogy aktualizací třetích stran
<!--4469002-->
Nyní máte podrobnější ovládací prvky pro synchronizaci katalogů aktualizací třetích stran. Od verze Configuration Manager 1910 můžete naplánovat synchronizaci pro každý katalog nezávisle na sobě. Pokud používáte katalogy, které zahrnují aktualizace kategorií, můžete synchronizaci nakonfigurovat tak, aby zahrnovala pouze konkrétní kategorie aktualizací, aby se předešlo synchronizaci celého katalogu. V případě, že máte jistotu, že nasazujete kategorii, můžete ji nakonfigurovat tak, aby se automaticky stáhla a publikovala do Windows Server Update Services (WSUS).

Další informace najdete v tématu [Povolení aktualizací třetích stran](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Použít optimalizaci doručování pro všechny aktualizace systému Windows
<!--4699118-->
Dříve jste mohli použít optimalizaci doručování pouze pro expresní aktualizace. S Configuration Manager verze 1910 je teď možné použít optimalizaci doručování pro distribuci veškerého web Windows Update obsahu pro klienty se systémem Windows 10 verze 1709 nebo novější.

Další informace naleznete v tématu:
- [Optimalizace doručování aktualizací Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Nastavení klienta pro aktualizace softwaru](../../clients/deploy/about-client-settings.md#software-updates)
- [Nastavení klienta pro optimalizaci doručení](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Další filtr aktualizace softwaru pro pravidla automatického nasazení
<!--4852033-->
Nyní můžete použít **nasazení** jako filtr aktualizace pro pravidla automatického nasazení (pravidla automatického nasazení). Tento filtr pomáhá identifikovat nové aktualizace, které může být nutné nasadit do pilotních nebo testovacích kolekcí.

Další informace najdete v tématu [automatické nasazení aktualizací softwaru](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

## <a name="office-management"></a><a name="bkmk_o365"></a> Správa Office


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Pilotní a řídicí panel pro Office 365-plus
<!--4488272, 4488301-->

Pilotní a řídicí panel stavů Office 365 vám pomůže plánovat, pilotovat a nasazovat Office 365 ProPlus. Řídicí panel poskytuje přehledy stavu pro zařízení s Office 365 ProPlus, které vám pomůžou identifikovat možné problémy, které můžou mít vliv na vaše plány nasazení. Pilotní a řídicí panel pro sadu Office 365 poskytuje doporučení pro pilotní zařízení založená na inventáři doplňku.

Další informace najdete v tématu [pilotní a řídicí panel pro Office 365-plus](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a> Antivirový

### <a name="bitlocker-management"></a>Správa nástroje BitLocker

<!--3601034-->

Configuration Manager nyní poskytuje následující možnosti správy pro nástroj BitLocker Drive Encryption:

- Nasaďte klienta nástroje BitLocker do spravovaných zařízení s Windows.
- Spravujte zásady šifrování zařízení.
- Generování sestav dodržování předpisů.
- Pro obnovení klíče použijte web pro správu a monitorování.
- Přístup k samoobslužnému portálu uživatele

Další informace najdete v tématu [Plánování správy BitLockeru](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Konzola Configuration Manager

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Zobrazení aktivních konzol a správců zpráv prostřednictvím připojení konzoly
<!--4923997-->
Provedli jsme následující vylepšení **připojení konzole**:

- Možnost zprávy ostatním správcům Configuration Manager prostřednictvím Microsoft Teams.
- **Poslední sloupec prezenčního signálu konzoly** nahradil sloupec **naposledy připojeného času** .
  - Otevřená konzola v popředí pošle prezenční signál každých 10 minut, aby bylo možné zjistit, která připojení konzoly jsou aktuálně aktivní.

Další informace najdete v tématu [zobrazení nedávno připojených konzol](../../servers/manage/admin-console.md#bkmk_viewconnected) a [správců zpráv](../../servers/manage/admin-console.md#bkmk_message).

### <a name="client-diagnostics-actions"></a>Akce diagnostiky klienta

<!--4433455-->

Existují nové akce zařízení pro **diagnostiku klienta** v konzole Configuration Manager:

- **Povolit podrobné protokolování:** Změňte úroveň globálního protokolu pro komponentu CCM na *verbose*a povolte protokolování ladění.
- **Zakázat podrobné protokolování:** Změňte globální úroveň protokolu na *výchozí*a zakažte protokolování ladění.

Další informace najdete v tématu [Diagnostika klientů](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="improvements-to-console-search"></a>Vylepšení hledání konzoly
<!--4640570-->

Tato verze zahrnuje následující vylepšení vyhledávání v konzole Configuration Manager:

- Nyní můžete použít možnost hledání **všech podsložek** z **balíčků ovladačů** a uzlů **dotazů** .<!--2841181,5424892-->
- Když hledání vrátí více než 1 000 výsledků, vyberte na panelu oznámení možnost **OK** , aby se zobrazily další výsledky.<!--4640570-->

## <a name="other-updates"></a>Další aktualizace

Další informace o změnách rutin prostředí Windows PowerShell pro Configuration Manager najdete v [poznámkách k verzi PowerShell verze 1910](/powershell/sccm/1910-release-notes?view=sccm-ps).

Další informace o změnách REST API služby správy najdete v tématu poznámky k [verzi služby správy](../../../develop/adminservice/release-notes.md#bkmk_1910).

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
V konzole nástroje je k dispozici následující kumulativní aktualizace (4537079) od 18. února 2020: [kumulativní aktualizace pro Microsoft Endpoint Configuration Manager Current Branch, verze 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Další kroky

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
Od 20. prosince 2019 je verze 1910 k dispozici pro všechny zákazníky, kteří chtějí instalovat.

Až budete připraveni k instalaci této verze, přečtěte si téma [instalace aktualizací pro Configuration Manager](../../servers/manage/updates.md) a [Kontrolní seznam pro instalaci aktualizace 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Chcete-li nainstalovat novou lokalitu, použijte základní verzi Configuration Manager.
>
> Přečtěte si další informace:
>
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md) 
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines) 

Známé důležité problémy najdete v [poznámkách k verzi](../../servers/deploy/install/release-notes.md).

Po aktualizaci lokality si také Projděte [Kontrolní seznam po aktualizaci](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).