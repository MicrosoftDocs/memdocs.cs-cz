---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1706 pro Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 79258786b56cc3e7fe4971391903772700768a89
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126752"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1706 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1706. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Známé problémy v této verzi Technical Preview:**

- **Přesunout distribuční bod** – možnosti v konzole pro přesun distribučního bodu mezi lokalitami nelze v této verzi použít z důvodu limitu Technical Preview pro jednu primární lokalitu.

- **Nastavení dodržování předpisů pro zařízení** – při použití dvou z nových nastavení dodržování předpisů pro zařízení se můžete setkat s opačným chováním:
  - **Blokovat na zařízení ladění USB**
  - **Blokovat aplikace z neznámých zdrojů**

    Pokud například správci nastavili možnost **blokovat ladění USB na zařízení** na **hodnotu true**, všechna zařízení, která nemají povolené ladění USB, se označí jako nedodržující předpisy.

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Vylepšené skupiny hranic pro body aktualizace softwaru
<!-- 1324591 -->
Tato verze zahrnuje vylepšení způsobu práce bodů aktualizace softwaru se skupinami hranic. Následující shrnuje nové nouzové chování:
- Záloha pro body aktualizace softwaru teď používá konfigurovatelný čas pro přechod do sousedních skupin hranic s minimální dobou 120 minut.

- Nezávisle na záložní konfiguraci se klient pokusí spojit s posledním bodem aktualizace softwaru, který se použil po dobu 120 minut. Po neúspěšném pokusu o dosažení tohoto serveru na 120 minut klient zkontroluje svůj fond dostupných bodů aktualizace softwaru, aby mohl najít nový.

  - Všechny body aktualizace softwaru v aktuální skupině hranic klienta se okamžitě přidají do fondu klientů.

  - Vzhledem k tomu, že se klient pokusí použít původní server po dobu 120 minut, než si vyzkouší nový, nekontaktují se žádné další servery až po uplynutí dvou hodin.

  - Pokud je záloha pro sousední skupinu nakonfigurovaná na minimum 120 minut, body aktualizace softwaru z této sousední skupiny hranic budou součástí fondu dostupných serverů klienta.

- Po neúspěšném přístupu k původnímu serveru po dobu dvou hodin se klient přepne na kratší cyklus, aby se obrátil na nový bod aktualizace softwaru.

  To znamená, že pokud se klient nemůže připojit k novému serveru, rychle vybere další server z fondu dostupných serverů a pokusí se ho kontaktovat.

  - Tento cyklus pokračuje, dokud se klient nepřipojí k bodu aktualizace softwaru, který může použít.
  - Dokud klient nenajde bod aktualizace softwaru, přidají se další servery do fondu dostupných serverů, když se splní záložní čas každé sousední skupiny hranic.

Další informace najdete v tématu [body aktualizace softwaru](../servers/deploy/configure/boundary-groups.md#bkmk_sup) v tématu skupiny hranic pro Current Branch.


## <a name="site-server-role-high-availability"></a>Vysoká dostupnost role serveru lokality
<!-- 1128774 -->
Vysoká dostupnost pro roli serveru lokality je Configuration Manager řešení založené na instalaci dalšího serveru primární lokality v *pasivním* režimu. Server lokality pasivního režimu je kromě stávajícího serveru primární lokality, který je v *aktivním* režimu. Server lokality v pasivním režimu je k dispozici pro okamžité použití v případě potřeby.

Server primární lokality v pasivním režimu:
- Používá stejnou databázi lokality jako aktivní server lokality.
- Přijme kopii knihovny obsahu aktivní servery webu, která je pak udržována v synchronizaci.
- Nepíše data do databáze lokality, pokud je v pasivním režimu.
- Nepodporuje instalaci ani odebrání nepovinných rolí systému lokality, pokud je v pasivním režimu.

Chcete-li nastavit webový server pasivního režimu jako server lokality aktivního režimu, ručně ho povýšíte. Tím se server aktivního serveru přepne na pasivní server lokality. Role systému lokality, které jsou k dispozici na původním serveru aktivního režimu, zůstávají k dispozici, pokud je tento počítač přístupný. Mezi aktivním a pasivním režimem je přepnuta pouze role serveru lokality.

Chcete-li nainstalovat server lokality pasivního režimu, použijte **Průvodce vytvořením serveru systému lokality** ke konfiguraci nového serveru lokality s typem **primárního serveru lokality** a **pasivním**režimem. Průvodce pak spustí Configuration Manager instalaci na zadaném serveru pro instalaci nového serveru lokality v pasivním režimu. Po dokončení instalace Server lokality aktivního režimu udržuje server lokality v pasivním režimu a jeho knihovnu obsahu synchronizované se změnami nebo konfiguracemi, které provedete na aktivním serveru lokality.

### <a name="prerequisites-and-limitations"></a>Požadavky a omezení
- Jeden server lokality v pasivním režimu je podporován v každé primární lokalitě.

- Server lokality v pasivním režimu může být místní nebo cloudový v Azure.

- Servery lokality aktivního režimu i pasivního režimu musí být ve stejné doméně.

- Servery lokality aktivního režimu i pasivního režimu musí používat stejnou databázi lokality, která musí být vzdálená z počítačů na každém serveru lokality.

    - SQL Server, která je hostitelem databáze, může používat výchozí instanci, pojmenovanou instanci, SQL Server cluster nebo skupinu dostupnosti Always On.

    - Server lokality v pasivním režimu je nakonfigurován tak, aby používal stejnou databázi lokality jako server lokality aktivního režimu. Server lokality pasivního režimu však tuto databázi nepoužívá, dokud nebude povýšen na aktivní režim.

- Počítač, ve kterém bude spuštěný server lokality pasivního režimu:

    - Musí splňovat [požadavky pro instalaci primární lokality](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    - Instaluje se pomocí zdrojových souborů, které odpovídají verzi serveru lokality aktivního režimu.

    - Před instalací lokality pasivního režimu nelze z žádné lokality role systému lokality.

- Počítač serveru lokality aktivního a pasivního režimu může spouštět různé operační systémy nebo verze aktualizace Service Pack, pokud oba zůstanou podporované vaší verzí Configuration Manager.

- Povýšení serveru lokality pasivního režimu na server aktivního režimu je ruční. Neexistuje žádné automatické převzetí služeb při selhání.

- Role systému lokality lze nainstalovat pouze na server lokality, který je v aktivním režimu.

    - Server lokality v aktivním režimu podporuje všechny role systému lokality. Role systému lokality nelze instalovat na server, pokud je v pasivním režimu.

    - Role systému lokality, které používají databázi (například bod hlášení), musí mít tuto databázi na serveru, který je vzdálený od serverů lokality aktivního režimu i pasivního režimu.

    - SMS_Provider se neinstaluje na server lokality v pasivním režimu. Vzhledem k tomu, že je nutné se připojit k SMS_Provider pro lokalitu a ručně zvýšit úroveň serveru lokality pasivního režimu na aktivní režim, doporučujeme [nainstalovat alespoň jednu další instanci poskytovatele](../plan-design/hierarchy/plan-for-the-sms-provider.md) na další počítač.

**Známý problém**:   
V této verzi se v konzole zobrazí **stav** z následujících podmínek jako číselné hodnoty namísto čitelného textu:
- 131071 – instalace webového serveru se nezdařila
- 720895 – nepovedlo se odinstalace role serveru lokality
- 851967 – neúspěšné převzetí služeb při selhání

### <a name="add-a-site-server-in-passive-mode"></a>Přidání serveru lokality v pasivním režimu
1. V konzole nástroje klikněte na **Správa**  >  **Konfigurace lokality**  >  **lokality** a spusťte [Průvodce Přidat role systému lokality](../servers/deploy/configure/install-site-system-roles.md). Můžete také použít **Průvodce vytvořením serveru systému lokality**.

2. Na stránce **Obecné** zadejte server, který bude hostitelem serveru lokality pasivního režimu. Server, který zadáte, nemůže hostovat žádné role systému lokality před instalací serveru lokality v pasivním režimu.

3. Na stránce **Výběr role systému** vyberte **v pasivním režimu pouze server primární lokality**.

4. K dokončení průvodce musíte zadat následující informace, které se použijí ke spuštění instalačního programu a instalaci role serveru lokality na zadaný server:
    - Zvolte možnost zkopírovat instalační soubory ze serveru aktivní lokality do nového serveru lokality pasivního režimu, nebo zadejte cestu k umístění, které obsahuje obsah disku CD serveru aktivní lokality **. Poslední** složka

    - Zadejte stejný server databáze lokality a název databáze, jak je používáno serverem lokality aktivního režimu.

5. Configuration Manager pak na určený server nainstaluje server lokality v pasivním režimu.

Podrobný stav instalace naleznete v umístění **Správa**  >  **Konfigurace lokality**  >  **lokality**.
- Stav serveru lokality v pasivním režimu se zobrazí jako **instalace**.

- Vyberte server a potom kliknutím na **Zobrazit stav** otevřete **stav instalace serveru lokality** , kde najdete podrobnější informace.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Zvýšit úroveň serveru lokality pasivního režimu na aktivní režim
Pokud chcete změnit server lokality pasivního režimu na aktivní režim, provedete to v podokně **uzly** v části **Správa**  >  **Konfigurace lokality**  >  **lokality**. Pokud budete mít přístup k instanci SMS_Provider, můžete k webu přejít, abyste tuto změnu provedli.
1. V podokně **uzly** konzoly Configuration Manager vyberte server lokality v pasivním režimu a pak na pásu karet zvolte možnost **povýšit na aktivní**.

2. Jednoduchý **stav** serveru, který podporujete, se zobrazí v podokně **uzly** při **zvyšování úrovně**.

3. Po dokončení povýšení se ve sloupci **stav** zobrazí **OK** pro nový server lokality *aktivního* režimu i pro nový server lokality v *pasivním* režimu.

4. V části **Správa**  >  **Konfigurace lokality**  >  **lokality**se v názvu serveru primární lokality nyní zobrazuje název nového serveru lokality *aktivního* režimu.
Podrobný stav najdete na stránce **monitorování**  >  **stav serveru lokality**.
    - Sloupec **Mode (režim** ) určuje, který server je *aktivní* nebo *pasivní*.

    - Při povýšení serveru z pasivního režimu na aktivní režim vyberte server lokality, který chcete zvýšit na aktivní, a pak na pásu karet zvolte **Zobrazit stav** . Otevře se okno **stav zvýšení úrovně serveru lokality** , ve kterém se zobrazí další podrobnosti o procesu.

Když se server lokality v aktivním režimu přepne do pasivního režimu, stane se pasivní jenom role systému lokality. Všechny ostatní role systému lokality, které jsou nainstalované v tomto počítači, zůstávají aktivní a přístupné pro klienty.


### <a name="daily-monitoring"></a>Denní monitorování
Pokud máte primární lokalitu v pasivním režimu, Sledujte ji denně, abyste zajistili, že zůstane synchronizovaná se serverem lokality aktivního režimu a je připraveno k použití. Provedete to tak, že přejdete na **monitorování**  >  **stav serveru lokality**. Tady můžete zobrazit servery lokality aktivního režimu i pasivního režimu.

Karta **Souhrn** :
- Sloupec **Mode (režim** ) určuje, který server je aktivní nebo pasivní.
- Seznam **stavů** je v **pořádku** , když je server pasivního režimu synchronizovaný se serverem aktivního režimu.
- Pokud chcete zobrazit další podrobnosti o stavu synchronizace obsahu, klikněte na **Zobrazit stav** ze stavu synchronizace obsahu. Tím se otevře karta knihovna obsahu, kde se můžete pokusit opravit problémy s synchronizací obsahu.

Karta **Knihovna obsahu** :
- Zobrazení **stavu** obsahu, který se synchronizuje z aktivního serveru lokality do serveru lokality pasivního režimu.
- Můžete vybrat obsah se stavem **selhání**a pak vybrat **synchronizovat vybrané položky** na pásu karet. Tato akce se pokusí znovu synchronizovat daný obsah ze zdroje obsahu do serveru lokality pasivního režimu. Během obnovení se stav **zobrazuje jako probíhající a když**se synchronizuje, zobrazí se jako **úspěšný**.

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste provést následující úkoly a pak nám poslat **zpětnou vazbu** z karty **Domů** na pásu karet a sdělte nám, jak se pracovalo:
- Můžu nainstalovat primární lokalitu v pasivním režimu.
- Můžu použít konzolu k povýšení serveru lokality pasivního režimu, aby mohl být serverem lokality aktivního režimu, a Potvrdit změnu stavu pro oba servery lokality.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Zahrnout vztah důvěryhodnosti pro konkrétní soubory a složky v zásadách Device Guard
<!-- 1324676 -->
V této verzi jsme přidali další možnosti správy zásad [Device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md) .

Nyní můžete volitelně přidat vztah důvěryhodnosti pro konkrétní soubory pro složky v zásadách ochrany zařízení. To vám umožní:

1. Překonání problémů s chováním spravované instalační služby
2. Důvěřovat obchodním aplikacím, které se nedají nasadit pomocí Configuration Manager
3. Důvěřujte aplikacím, které jsou součástí bitové kopie nasazení operačního systému.

### <a name="try-it-out"></a>Určitě to udělejte!

1. Když vytváříte zásadu ochrany zařízení, na kartě zahrnutí v Průvodci vytvořením zásady ochrany zařízení klikněte na **Přidat**.
2. V dialogovém okně **Přidat důvěryhodný soubor nebo složku** zadejte informace o souboru nebo složce, které chcete důvěřovat. Můžete buď zadat místní cestu k souboru nebo složce, nebo se připojit ke vzdálenému zařízení, ke kterému máte oprávnění k připojení, a určit cestu k souboru nebo složce na zařízení.
3. Dokončete průvodce.


## <a name="hide-task-sequence-progress"></a>Skrýt průběh pořadí úloh
<!-- 1354291 -->
V této verzi můžete určit, kdy se má koncovým uživatelům zobrazit průběh pořadí úloh pomocí nové proměnné. V pořadí úkolů pomocí kroku **nastavit proměnnou pořadí úkolů** nastavte hodnotu proměnné **TSDisableProgressUI** pro skrytí nebo zobrazení průběhu pořadí úkolů. V pořadí úkolů můžete použít krok nastavit proměnnou pořadí úkolů několikrát a změnit hodnotu proměnné. To umožňuje skrýt nebo zobrazit průběh pořadí úloh v různých částech pořadí úkolů.

#### <a name="to-hide-task-sequence-progress"></a>Skrytí průběhu pořadí úkolů
V editoru pořadí úloh použijte krok [nastavit proměnnou pořadí úkolů](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) a nastavte hodnotu proměnné **TSDisableProgressUI** na hodnotu **true** , aby se skryl průběh pořadí úkolů.

#### <a name="to-display-task-sequence-progress"></a>Zobrazení průběhu pořadí úkolů
V editoru pořadí úloh použijte krok [nastavit proměnnou pořadí úkolů](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) a nastavte hodnotu proměnné **TSDisableProgressUI** na **false** , aby se zobrazil průběh pořadí úkolů.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Zadejte jiné umístění obsahu pro instalaci obsahu a odinstalaci obsahu.
<!-- 1097546 -->
V Configuration Manager dnes zadáte umístění instalace, které obsahuje instalační soubory pro aplikaci. Když zadáte umístění instalace, použije se také jako umístění pro odinstalaci obsahu aplikace.
Na základě vaší zpětné vazby, pokud chcete odinstalovat nasazenou aplikaci a obsah aplikace není v klientském počítači, klient stáhne všechny instalační soubory aplikace znovu před odinstalací aplikace.
Chcete-li tento problém vyřešit, můžete nyní zadat umístění obsahu instalace i volitelné umístění obsahu pro odinstalaci. Kromě toho se můžete rozhodnout neurčit umístění obsahu pro odinstalaci.

### <a name="try-it-out"></a>Vyzkoušejte si to!

1. Ve vlastnostech typu nasazení aplikace klikněte na kartu **obsah** .
2. Nakonfigurujte **umístění obsahu instalace** jako normální.
3. V části **Nastavení obsahu pro odinstalaci**vyberte jednu z následujících možností:
   - **Stejné jako obsah instalace** – stejné umístění obsahu se bude používat bez ohledu na to, jestli provádíte instalaci nebo odinstalaci aplikace.
   - **Bez obsahu pro odinstalování** – tuto možnost vyberte, pokud nechcete, aby aplikace poskytovala umístění obsahu pro odinstalaci.
   - **Odlišné od obsahu instalace** – tuto možnost vyberte, pokud chcete zadat umístění obsahu pro odinstalaci, které se liší od umístění obsahu instalace.
5. Pokud jste vybrali možnost **jiný než obsah instalace**, vyhledejte nebo zadejte umístění obsahu aplikace, které bude použito k odinstalaci aplikace.
6. Kliknutím na tlačítko **OK** zavřete dialogové okno Vlastnosti typu nasazení.


## <a name="accessibility-improvements"></a>Vylepšení přístupnosti  
<!--1253000 -->
Tato verze Preview přináší několik vylepšení [funkcí usnadnění](../understand/accessibility-features.md) v konzole Configuration Manager. Tady jsou některé z nich:     

**Nové klávesové zkratky pro pohyb v konzole:**
- CTRL + M – nastaví fokus do hlavního (centrálního) podokna.
- CTRL + T – nastaví fokus na nejvyšší uzel v navigačním podokně. Pokud byl fokus již v tomto podokně, je fokus nastaven na poslední uzel, který jste navštívili.
- CTRL + I – nastaví fokus na panel s popisem cesty pod pás karet.
- CTRL + L – nastaví fokus na **vyhledávací** pole, pokud je k dispozici.
- CTRL + D – nastaví fokus na podokno podrobností, pokud je k dispozici.
- ALT – změní fokus na pás karet a ven z něj.

**Obecná vylepšení:**
- Vylepšená navigace v navigačním podokně při psaní písmen názvu uzlu.
- Navigace pomocí klávesnice v hlavním zobrazení a na pásu karet je teď cyklická.
- Navigace na klávesnici v podokně podrobností je teď cyklická. Chcete-li se vrátit k předchozímu objektu nebo podoknu, použijte kombinaci kláves CTRL + D a klávesy SHIFT + TAB.
- Po aktualizaci zobrazení pracovního prostoru se fokus nastaví na hlavní podokno daného pracovního prostoru.
- Opravili jsme problém, aby čtenáři obrazovky mohli oznamovat názvy položek seznamu.
- Na stránce byly přidány přístupné názvy pro více ovládacích prvků, které umožňují čtenářům obrazovky oznamovat důležité informace.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Změny v Průvodci službami Azure pro podporu Upgrade Readiness
<!-- 1353331 -->
Od této verze použijte Průvodce službami Azure ke konfiguraci připojení z Configuration Manager k Upgrade Readiness. Použití Průvodce zjednodušuje konfiguraci konektoru pomocí společného průvodce pro související služby Azure.   

I když se změnila metoda konfigurace připojení, požadavky pro připojení a způsob použití Upgrade Readiness zůstanou beze změny.   

### <a name="prerequisites-for-upgrade-readiness"></a>Předpoklady pro Upgrade Readiness
Požadavky na připojení k Upgrade Readiness se nezměnily od těch, které jsou podrobné pro Current Branch Configuration Manager. Tady jsou pro pohodlí opakované:  

**Požadavky**
- Aby bylo možné přidat připojení, musí vaše prostředí Configuration Manager nejprve nakonfigurovat [spojovací bod služby](../servers/deploy/configure/about-the-service-connection-point.md) v [online režimu](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes). Když přidáte připojení do prostředí, nainstaluje se taky Microsoft Monitoring Agent na počítač, na kterém je spuštěná tato role systému lokality.
- Zaregistrujte se Configuration Manager jako nástroj pro správu webové aplikace nebo webového rozhraní API a [z této registrace Získejte ID klienta](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Vytvořte klíč klienta pro registrovaný Nástroj pro správu v Azure Active Directory.
- V Azure Portal zadejte registrovanou webovou aplikaci s oprávněním pro přístup k OMS.

> [!IMPORTANT]       
> Při konfiguraci oprávnění pro přístup k OMS si nezapomeňte zvolit roli **Přispěvatel** a přiřadit jí oprávnění pro skupinu prostředků registrované aplikace.

Po dokončení konfigurace požadavků budete připraveni k vytvoření připojení použít průvodce.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Pomocí Průvodce službami Azure nakonfigurujte Upgrade Readiness
1. V konzole nástroje v části Přehled **správy**  >  **Overview**  >  **Cloud Services**  >  **služby Azure**a pak zvolte **Konfigurovat služby Azure** na kartě **Domů** na pásu karet a spusťte **Průvodce službami Azure**.

2. Na stránce **služby Azure** vyberte **konektor upgrade Readiness**a pak klikněte na **Další**.

3. Na stránce **aplikace** určete své **prostředí Azure** (Technical Preview podporuje jenom veřejný cloud). Pak kliknutím na **importovat** otevřete okno **importovat aplikace** .

4. V okně **importovat aplikace** zadejte podrobnosti pro webovou aplikaci, která už ve službě Azure AD existuje.
    - Zadejte popisný název pro název tenanta Azure AD. Pak zadejte ID tenanta, název aplikace, ID klienta, tajný klíč pro webovou aplikaci Azure a identifikátor URI ID aplikace.
    - Klikněte na tlačítko **ověřit**a v případě úspěchu kliknutím na tlačítko **OK** pokračujte.

5.  Na stránce **Konfigurace** určete předplatné, skupinu prostředků a pracovní prostor Windows Analytics, které chcete používat s tímto připojením k upgrade Readiness.  

6. Kliknutím na **Další** přejděte na stránku **Souhrn** a pak dokončete průvodce, aby se vytvořilo připojení.


## <a name="new-client-settings-for-cloud-services"></a>Nová nastavení klienta pro cloudové služby
<!-- 1319883 -->

V této verzi jsme do Configuration Manager přidali dvě nová nastavení klienta. Najdete je v části **Cloud Services** .  Tato nastavení poskytují následující možnosti:

- Řídí, kteří Configuration Manager klienti mají přístup k nakonfigurované bráně pro správu cloudu.
- Automaticky registrovat klienty Správce konfigurace připojené k doméně Windows 10 pomocí Azure Active Directory.

Tato nová nastavení vám pomůžou s provedením možností popsaných v [Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Než začnete

Musíte mít nainstalovanou a nakonfigurovanou Azure AD Connect mezi vaší místní službou Active Directory a vaším klientem služby Azure AD.

Pokud připojení odeberete, zařízení se nezaregistrují, ale nebudou se registrovat žádná nová zařízení.

### <a name="try-it-out"></a>Určitě to udělejte!

1. Nakonfigurujte následující nastavení klienta (najdete v části Cloud Services) s použitím informací v tématu [Konfigurace nastavení klienta](../clients/deploy/configure-client-settings.md).
   - **Automaticky registrovat nová zařízení s Windows 10 připojená k doméně pomocí Azure Active Directory** – nastavte na **Ano** (výchozí) nebo **ne**.
   - **Povolit klientům používat bránu pro správu cloudu** – nastavte na **Ano** (výchozí) nebo **ne**.
2. Nasaďte nastavení klienta do požadované kolekce zařízení.

Pokud chcete potvrdit, že je zařízení připojené k Azure AD, spusťte příkaz **dsregcmd.exe/status** v okně příkazového řádku. Pokud je zařízení připojené k Azure AD, zobrazí se v poli **AzureAdjoined** ve výsledcích hodnota **Ano** .

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Vytvoření a spuštění PowerShellových skriptů z konzoly Configuration Manager
<!-- 1236459 -->

V Configuration Manager můžete do klientských zařízení nasadit skripty pomocí balíčků a programů. V této verzi Technical Preview jsme přidali nové funkce, které vám umožní provést následující akce:

- Import skriptů PowerShellu pro Configuration Manager
- Úprava skriptů z konzoly Configuration Manager (jenom pro nepodepsané skripty)
- Označení skriptů jako schválených nebo odepřených pro zlepšení zabezpečení
- Spouštějte skripty na kolekcích klientských počítačů s Windows a na místních spravovaných počítačích s Windows. Skripty nesadíte místo toho, aby byly spouštěny téměř v reálném čase na klientských zařízeních.
- Projděte si výsledky vracené skriptem v konzole Configuration Manager.


### <a name="prerequisites"></a>Požadavky

Chcete-li použít skripty, musíte být členem příslušné role zabezpečení Configuration Manager.

- **Import a vytváření skriptů** – váš účet musí mít oprávnění **Create** pro **skripty SMS** v roli zabezpečení **správce s úplnými oprávněními** .
- **Chcete-li schválit nebo zamítnout skripty** – váš účet musí mít oprávnění **schvalovat** pro **skripty SMS** v roli zabezpečení **správce s úplnými oprávněními** .
- **Chcete-li spustit skripty** – váš účet musí mít oprávnění **Run Script** pro **kolekce** v roli zabezpečení **Správce nastavení dodržování předpisů** .

Další informace o Configuration Manager rolí zabezpečení najdete v tématu [základy správy na základě rolí](../understand/fundamentals-of-role-based-administration.md).

Ve výchozím nastavení uživatelé nemůžou schvalovat skript, který vytvořil. Vzhledem k tomu, že jsou skripty výkonné, všestranné a můžou být nasazené na mnoho zařízení, zavedli jsme nový koncept poskytování možnosti oddělení rolí mezi osobou, která tento skript vytvoří, a osobou, která tento skript schválí. Tím se dá zvýšit úroveň zabezpečení před spuštěním skriptu bez dohledu. Toto sekundární schválení můžete vypnout, abyste usnadnili testování, zejména v rámci verze Technical Preview.

Umožnění uživatelům schvalovat své vlastní skripty:

1. V konzole Configuration Manager klikněte na možnost **Správa**.
2. V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace webu**a klikněte na položku **Weby**.
3. V seznamu lokality vyberte lokalitu a pak na kartě **Domů** ve skupině **lokality** klikněte na **Nastavení hierarchie**.
4. Na kartě **Obecné** v dialogovém okně **Vlastnosti nastavení hierarchie** zrušte zaškrtnutí políčka **Nepovolit autorům skriptů schvalovat své vlastní skripty**.


### <a name="try-it-out"></a>Určitě to udělejte!

#### <a name="import-and-edit-a-script"></a>Import a úprava skriptu

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.
2. V pracovním prostoru **softwarová knihovna** klikněte na **skripty**.
3. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit skript**.
4. Na stránce **skript** v průvodci **vytvořením skriptu** nakonfigurujte následující nastavení:
   - **Název skriptu** – zadejte název skriptu. I když můžete vytvořit více skriptů se stejným názvem, to vám usnadní vyhledání skriptu, který potřebujete v konzole Configuration Manager.
   - **Skriptovací jazyk** – v současné době se podporují jenom skripty **PowerShellu** .
   - **Import** – importujte powershellový skript do konzoly nástroje. Skript se zobrazí v poli **skript** .
   - **Vymazat** – Odebere aktuální skript z pole **skriptu** .
   - **Skript** – zobrazí aktuálně importovaný skript. Skript v tomto poli můžete podle potřeby upravit.
5. Dokončete průvodce. Nový skript se zobrazí v seznamu **skriptů** se stavem **čekání na schválení**. Než budete moct spustit tento skript na klientských zařízeních, musíte ho schválit.


#### <a name="approve-or-deny-a-script"></a>Schválení nebo zamítnutí skriptu



Než budete moct skript spustit, musí se schválit. Postup schválení skriptu:

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.
2. V pracovním prostoru **softwarová knihovna** klikněte na **skripty**.
3. V seznamu **skript** vyberte skript, který chcete schválit nebo odepřít, a potom na kartě **Domů** ve skupině **skript** klikněte na **schválit/odepřít**.
4. V dialogovém okně pro **schválení nebo odmítnutí** skriptu **schvalte**nebo **odepřete** skript a volitelně zadejte komentář k vašemu rozhodnutí. Pokud skript odepřete, nejde ho spustit na klientských zařízeních.
5. Dokončete průvodce. V seznamu **skriptů** uvidíte, že se změní sloupec **stav schválení** v závislosti na akci, kterou jste udělali.

#### <a name="run-a-script"></a>Spuštění skriptu

Po schválení skriptu je možné ho spustit pro kolekci, kterou zvolíte.

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.
2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na možnost **Kolekce zařízení**.
3. V seznamu **kolekce zařízení** klikněte na kolekci zařízení, na kterých chcete skript spustit.
3. Na kartě **Domů** ve skupině **všechny systémy** klikněte na možnost **Spustit skript**.
4. Na stránce **skript** v průvodci **spuštěním skriptu** vyberte ze seznamu skript. Zobrazují se jenom schválené skripty. Klikněte na **Další**a pak dokončete průvodce.

#### <a name="monitor-a-script"></a>Monitorování skriptu

Po spuštění skriptu na klientská zařízení pomocí tohoto postupu můžete monitorovat úspěch operace.

1. V konzole Configuration Manager klikněte na **monitorování**.
2. V pracovním prostoru **monitorování** klikněte na možnost **výsledky skriptu**.
3. V seznamu **výsledků skriptu** zobrazíte výsledky pro každý skript, který jste spustili v klientských zařízeních. Kód ukončení skriptu **0**, obecně znamená, že skript byl úspěšně spuštěn.

## <a name="pxe-network-boot-support-for-ipv6"></a>Podpora spouštění sítě PXE pro protokol IPv6
<!-- 1269793 -->
Nyní můžete povolit podporu spouštění sítě PXE pro protokol IPv6 pro spuštění nasazení operačního systému pořadí úkolů. Když použijete toto nastavení, distribuční body s podporou technologie PXE budou podporovat protokol IPv4 i IPv6. Tato možnost nevyžaduje program WDS a zastaví službu WDS, pokud je k dispozici.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Povolení podpory spouštění PXE pro protokol IPv6
Pomocí následujícího postupu povolte možnost podpory protokolu IPv6 pro technologii PXE.

1. V konzole Configuration Manager přejděte na **Správa**  >  **Přehled**  >  **distribučních bodů**a klikněte na **vlastnosti** distribučních bodů s podporou technologie PXE.
2. Na kartě **PXE** vyberte **podporovat IPv6** , aby se povolila podpora IPv6 pro PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Spravovat aktualizace ovladačů Microsoft Surface
<!-- 1098490 -->
Teď můžete pomocí Configuration Manager spravovat aktualizace ovladačů Microsoft Surface.

### <a name="prerequisites"></a>Požadavky
Všechny body aktualizace softwaru musí používat systém Windows Server 2016.

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste provést následující úkoly a pak nám poslat **zpětnou vazbu** z karty **Domů** na pásu karet a sdělte nám, jak se pracovalo:
1. Povolte synchronizaci pro ovladače Microsoft Surface. Pomocí postupu v části [Konfigurace klasifikace a produktů](../../sum/get-started/configure-classifications-and-products.md) vyberte možnost **zahrnout ovladače Microsoft Surface a aktualizace firmwaru** na kartě **klasifikace** a povolte ovladače Surface.
2. [Synchronizovat ovladače Microsoft Surface](../../sum/get-started/synchronize-software-updates.md).
3. [Nasazení synchronizovaných ovladačů Microsoft Surface](../../sum/deploy-use/deploy-software-updates.md)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurace zásad odložení web Windows Update pro firmy
<!-- 1290890 -->
Teď můžete nakonfigurovat zásady odložení pro aktualizace funkcí Windows 10 nebo aktualizace kvality pro zařízení s Windows 10 spravovaná přímo pomocí web Windows Update pro firmy. Zásady odložení můžete spravovat v uzlu nové **zásady web Windows Update pro firmy** v části **softwarová knihovna**  >  **Windows 10 – Údržba**.

### <a name="prerequisites"></a>Požadavky
Zařízení s Windows 10 spravovaná pomocí web Windows Update pro firmy musí mít připojení k Internetu.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Vytvoření zásady pro odložení web Windows Update pro firmy
1. V **knihovně softwaru**  >  **Windows 10 Údržba**  >  **web Windows Update pro podnikové zásady**
2. Na kartě **Domů** ve skupině **vytvořit** vyberte **vytvořit web Windows Update pro firmy** a otevřete tak Průvodce vytvořením zásad web Windows Update pro firmy.
3. Na stránce **Obecné** zadejte název a popis zásady.
4. Na stránce **zásady odložení** nakonfigurujte, jestli se mají odložit nebo pozastavit aktualizace funkcí.    
    Aktualizace funkcí jsou obecně nové funkce pro Windows. Po konfiguraci nastavení **úrovně připravenosti větve** můžete definovat, jestli a jak dlouho chcete odložit příjem aktualizací funkcí po jejich dostupnosti od Microsoftu.
    - **Úroveň připravenosti větve**: nastavte větev, pro kterou bude zařízení přijímat aktualizace Windows (Current Branch nebo Current Branch for Business).
    - Doba odkladu **(dny)**: zadejte počet dní, po které budou aktualizace funkcí odloženy. Příjem těchto aktualizací funkcí můžete odložit až o 180 dní od jejich vydání.
    - **Pozastavení funkcí aktualizace od**: Určete, jestli se mají zařízení pozastavit po dobu až 60 dnů od doby, kdy jste aktualizace pozastavili. Po uplynutí maximálního počtu dní funkce pozastavení automaticky vyprší a zařízení zkontroluje dostupné aktualizace ve Windows Update. Po této kontrole můžete aktualizace znovu pozastavit. Zaškrtnutím políčka můžete zrušit pozastavení aktualizací funkcí.   
5. Vyberte, jestli se mají odložit nebo pozastavit aktualizace kvality.     
    Aktualizace kvality jsou obecně opravy a vylepšení stávajících funkcí Windows a jsou obvykle vydávané první úterý v každém měsíci. Microsoft je ale může vydávat i kdykoli jindy. Můžete definovat, jestli a jak dlouho chcete přijímání aktualizací kvality po jejich vydání odkládat.
    - Doba odkladu **(dny)**: zadejte počet dní, po které budou aktualizace funkcí odloženy. Příjem těchto aktualizací funkcí můžete odložit až o 180 dní od jejich vydání.
    - **Pozastavení aktualizací kvality od**: Určete, jestli se mají zařízení pozastavit, aby se aktualizace kvality zobrazovaly po dobu až 35 dní od času, kdy jste aktualizace pozastavili. Po uplynutí maximálního počtu dní funkce pozastavení automaticky vyprší a zařízení zkontroluje dostupné aktualizace ve Windows Update. Po této kontrole můžete aktualizace znovu pozastavit. Zaškrtnutím políčka můžete zrušit pozastavení aktualizací kvality.
6. Výběrem možnosti **instalovat aktualizace z dalších produktů společnosti Microsoft** povolte nastavení zásad skupiny, které umožňuje nastavení odložení na Microsoft Update a také aktualizace systému Windows.
7. Chcete-li automaticky aktualizovat ovladače z aktualizací systému Windows, vyberte možnost **zahrnout ovladače s web Windows Update** . Pokud toto nastavení zrušíte, aktualizace ovladačů se z aktualizací Windows nestáhnou.
8. Dokončete průvodce a vytvořte novou zásadu odložení.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Nasazení zásad pro odložení web Windows Update pro firmy
1. V **knihovně softwaru**  >  **Windows 10 Údržba**  >  **web Windows Update pro podnikové zásady**
2. Na kartě **Domů** ve skupině **nasazení** vyberte **nasadit web Windows Update pro podnikové zásady**.
3. Nakonfigurujte tahle nastavení:
    - **Zásady konfigurace, které se mají nasadit**: vyberte zásady web Windows Update pro firmy, které chcete nasadit.
    - **Kolekce**: kliknutím na **Procházet** vyberte kolekci, do které chcete zásady nasadit.
    - **Napravit pravidla nesplňující požadavky**, je-li to podporováno: tuto možnost vyberte, pokud chcete automaticky opravit všechna pravidla, která nedodržují předpisy pro rozhraní WMI (Windows Management Instrumentation) (WMI), registr, skripty a všechna nastavení pro mobilní zařízení zaregistrovaná pomocí Configuration Manager.
    - **Povolit nápravu mimo okno údržby**: Pokud je pro kolekci, do které zásadu nasazujete, nakonfigurované časové období údržby, povolte tuto možnost, aby nastavení dodržování předpisů napravila hodnotu mimo časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../clients/manage/collections/use-maintenance-windows.md)údržby.
    - **Vygenerovat výstrahu**: nakonfiguruje výstrahu, která se vygeneruje, pokud kompatibilita standardních hodnot konfigurace je nižší než zadané procento podle zadaného data a času. Také můžete zvolit, zda chcete zasílat výstrahu do nástroje System Center Operations Manager.
    - **Náhodné zpoždění (v hodinách)**: Určuje okno zpoždění, aby se zabránilo nadměrnému zpracování služby zápisu síťových zařízení. Výchozí hodnota je 64 dnů.
    - **Plán**: Určete plán vyhodnocení dodržování předpisů, podle kterého je nasazený profil vyhodnocený na klientských počítačích. Plán může být jednoduchý nebo vlastní. Profil je vyhodnocován klientskými počítači, když se uživatel přihlašuje.
4.  Dokončením Průvodce nasaďte profil.



## <a name="support-for-entrust-certification-authorities"></a>Podpora pro svěřené certifikační autority
<!-- 1350740 -->
Configuration Manager teď podporuje svěřené certifikační autority; To umožňuje doručování certifikátů PFX do zařízení zaregistrovaných do Microsoft Intune.

Při přidávání role bodu registrace certifikátu do Configuration Manager můžete jako certifikační autoritu nakonfigurovat oprávnění svěřit. Při přidávání nového profilu certifikátu, který vydává certifikáty PFX, můžete vybrat certifikační autoritu od Microsoftu nebo pověřit.

**Známý problém**: ve verzi 1706 Technical Preview se certifikáty PFX nevydávají pro certifikační autority Microsoftu. To nemá vliv na importované certifikáty PFX ani profily SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Podpora Cisco (IPsec) pro profily VPN iOS
<!-- 1321367 -->

Jako typ připojení můžete vytvořit profil VPN iOS s Cisco (IPsec). Další informace najdete v tématu [Vytvoření profilů sítě VPN](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Nová nastavení položky konfigurace Windows
<!-- 1354715 -->

V této verzi jsme přidali následující nová nastavení, která můžete použít v položkách konfigurace Windows:

### <a name="password"></a>Heslo

- **Šifrování zařízení**

### <a name="device"></a>Zařízení

- **Změny nastavení oblasti (jenom desktopové)**
- **Úprava nastavení napájení a režimu spánku**
- **Změny nastavení jazyka**
- **Změna systémového času**
- **Úprava názvu zařízení**

### <a name="store"></a>Uložení

- **Automaticky aktualizovat aplikace ze Storu**
- **Použít pouze privátní úložiště**
- **Spuštění aplikace pocházející ze Storu**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Zablokovat přístup k about: Flags**
- **Přepsání výzvy SmartScreen**
- **Přepsání výzvy SmartScreen pro soubory**
- **IP adresa WebRTC localhost**
- **Výchozí vyhledávací modul**
- **Adresa URL XML pro OpenSearch**
- **Domovské stránky (jenom desktopové)**

Další informace o nastavení dodržování předpisů najdete v tématu [zajištění dodržování předpisů zařízením](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Nová pravidla zásad dodržování předpisů pro zařízení

* **Požadovaný typ hesla**. Určete, zda musí uživatel vytvořit alfanumerické nebo číselné heslo. U alfanumerických hesel je také možné zadat minimální počet znakových sad, které musí heslo obsahovat. Jedná se o čtyři znakové sady: malá písmena, Velká písmena, symboly a čísla.

  **Podporované platformy:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
<br></br>
* **Blokuje na zařízení ladění USB**. Toto nastavení nemusíte konfigurovat, protože ladění USB je už na zařízeních s Androidem for Work zakázané.

  **Podporované platformy:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Blokuje aplikace z neznámých zdrojů**. Vyžadovat, aby zařízení bránila instalaci aplikací z neznámých zdrojů. Toto nastavení nemusíte konfigurovat, protože zařízení s Androidem for Work vždycky omezují instalaci z neznámých zdrojů.

  **Podporované platformy:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Vyžadovat kontrolu hrozeb u aplikací** Toto nastavení určuje, že je na zařízení povolená funkce ověřovat aplikace.

  **Podporované platformy:**
  * Android 4,2 až 4,4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Nová nastavení zásad správy mobilních aplikací
Od této verze můžete použít tři nová nastavení zásad správy mobilních aplikací (MAM):

- **Blokovat snímek obrazovky (jenom zařízení s Androidem):** Určuje, že při použití této aplikace jsou při používání této aplikace zablokované možnosti zachycení obrazovky zařízení.

- **Zakázat synchronizaci kontaktů:** Zabraňuje aplikaci ukládat data do nativní aplikace kontakty na zařízení.

- **Zakázat tisk:** Zabraňuje aplikaci v tisku pracovních nebo školních dat.

## <a name="android-and-ios-enrollment-restrictions"></a>Omezení registrace pro Android a iOS
<!-- 1290826 -->
Od této verze můžou správci teď určit, že uživatelé nebudou moct do svého hybridního prostředí registrovat osobní zařízení s Androidem nebo iOS. To vám umožní omezit registrovaná zařízení na předem deklarovaná zařízení, která patří společnosti nebo zařízení s iOS registrovaná jenom pomocí Program registrace zařízení.

### <a name="try-it-out"></a>Vyzkoušet
1. V konzole nástroje Configuration Manager přejděte v pracovním prostoru **Správa** do části **Cloudové služby** > **Předplatné Microsoft Intune**.
2. Na kartě **Domů** ve skupině **předplatné** zvolte **Konfigurovat platformy** a pak vyberte **Android** nebo **iOS**.
3. Vyberte možnost **blokovat zařízení v osobním vlastnictví**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Zásady správy aplikací pro Android for Work pro kopírování a vkládání
Aktualizovali jsme popisy nastavení pro položky konfigurace Androidu for Work pro možnost **Povolení sdílení dat mezi pracovním a osobním profilem**.

|Před 1706 Technical Preview | Nový název možnosti | Chování|
|-|-|-|
|Zakázat sdílení přes hranice| Výchozí omezení sdílení| Work-to-Personal: výchozí (očekává se, že bude blokováno u všech verzí) <br>Osobní práce: výchozí (povolená na 6. x +, blokované na 5. x)|
|Žádná omezení| Aplikace v osobním profilu můžou zpracovat žádosti o sdílení z pracovního profilu.| Work-to-osobní: povoleno  <br>Osobní práce: povoleno|
|Aplikace v pracovním profilu můžou zpracovat žádosti o sdílení z osobního profilu. |Aplikace v pracovním profilu můžou zpracovat žádosti o sdílení z osobního profilu. |Pracovní – osobní: výchozí<br>Osobní práce: povoleno<br>(Hodí se jenom na 5. x, kde se zablokuje osobní práce)|

Žádná z těchto možností přímo nebrání chování při kopírování a vkládání. Do 1704 jsme přidali vlastní nastavení služby a Portál společnosti aplikaci, která se dá nakonfigurovat tak, aby se zabránilo kopírování a vkládání. Dá se nastavit pomocí vlastního identifikátoru URI.

- OMA-URI:./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Typ hodnoty: logická hodnota

Nastavení DisallowCrossProfileCopyPaste na hodnotu true brání chování funkce kopírování a vkládání mezi osobními a pracovními profily Androidu for Work.

### <a name="try-it-out"></a>Vyzkoušet
1. V konzole Configuration Manager vyberte **prostředky a kompatibilita**  >  **Přehled**  >  **Nastavení dodržování předpisů**  >  **položky konfigurace**.
2. Zvolte **vytvořit** a vytvořte novou položku konfigurace a zadejte **název** a **Android for Work**.
3. Ve skupinách nastavení zařízení ke konfiguraci vyberte **pracovní profil**a klikněte na tlačítko **Další**.
4. Vyberte hodnotu pro **Povolení sdílení dat mezi pracovními a osobními profily**a pak dokončete průvodce.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Ověření stavu zařízení posouzení zásad dodržování předpisů pro podmíněný přístup
<!-- 1097546 -->
Od této verze můžete použít Ověření stavu zařízení stav jako pravidlo zásad dodržování předpisů pro podmíněný přístup k prostředkům společnosti.

### <a name="try-it-out"></a>Vyzkoušet
Vyberte pravidlo Ověření stavu zařízení jako součást hodnocení zásad dodržování předpisů.
