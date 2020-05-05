---
title: Nasazení aplikací
titleSuffix: Configuration Manager
description: Vytvoření nebo simulace nasazení aplikace na kolekci zařízení nebo uživatelů
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7bbf395a5de98459043609986e51647362e7a0b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075332"
---
# <a name="deploy-applications-with-configuration-manager"></a>Nasazení aplikací pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vytvoření nebo simulace nasazení aplikace do kolekce zařízení nebo uživatele v Configuration Manager. Toto nasazení poskytuje pokyny pro klienta Configuration Manager o tom, jak a kdy se má software nainstalovat.

Předtím, než budete moci nasadit aplikaci, vytvořte alespoň jeden typ nasazení pro aplikaci. Další informace najdete v tématu věnovaném [vytváření aplikací](create-applications.md).

Počínaje verzí 1906 můžete vytvořit skupinu aplikací, které můžete odeslat do kolekce uživatelů nebo zařízení jako jediné nasazení. Další informace najdete v tématu [Vytvoření skupin aplikací](create-app-groups.md).

Můžete také simulovat nasazení aplikace. Tato simulace testuje použitelnost nasazení bez instalování nebo odinstalování aplikace. Simulované nasazení vyhodnocuje detekční metodu, požadavky a závislosti pro typ nasazení a hlásí výsledky v uzlu **nasazení** pracovního prostoru **monitorování** . Další informace najdete v tématu [Simulace nasazení aplikace](simulate-application-deployments.md).

> [!Note]
> Můžete simulovat jenom nasazení požadovaných aplikací, ale ne balíčky nebo aktualizace softwaru.
>
> Zařízení zaregistrovaná v MDM nepodporují simulovaná nasazení, uživatelské prostředí ani nastavení plánování.



## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a>Nasazení aplikace

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** nebo **skupiny aplikací** .

2. Vyberte aplikaci nebo skupinu aplikací ze seznamu, který chcete nasadit. Na pásu karet klikněte na **nasadit**.  

> [!Note]  
> Po zobrazení vlastností stávajícího nasazení budou v následujících oddílech odpovídat kartám okna Vlastnosti nasazení:  
>
> - [Obecné](#bkmk_deploy-general)
> - [Obsah](#bkmk_deploy-content)
> - [Nastavení nasazení](#bkmk_deploy-settings)
> - [Plánování](#bkmk_deploy-sched)
> - [Zkušenosti uživatele](#bkmk_deploy-ux)
> - [Výstrahy](#bkmk_deploy-alerts)


### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a>**Obecné** informace o nasazení

Na stránce **Obecné** v nástroji Průvodce nasazením softwaru zadejte následující informace:  

- **Software**: Tato hodnota zobrazí aplikaci, která se má nasadit. Klikněte na tlačítko **Procházet** a vyberte jinou aplikaci.  

- **Kolekce**: kliknutím na tlačítko **Procházet** vyberte kolekci, do které chcete aplikaci nasadit.  

- **Použít výchozí skupiny distribučních bodů přidružené k této kolekci**: Uložte obsah aplikace ve výchozí skupině distribučních bodů kolekce. Pokud jste vybranou kolekci nepřidali se skupinou distribučních bodů, je tato možnost zobrazena šedě.  

- **Automaticky distribuovat obsah pro závislosti**: Pokud některý z typů nasazení v aplikaci obsahuje závislosti, pak lokalita také pošle závislý obsah aplikace do distribučních bodů.  

    >[!Note]  
    > Pokud aktualizujete závislou aplikaci po nasazení primární aplikace, lokalita nebude automaticky distribuovat žádný nový obsah pro závislost.  

- **Komentáře (volitelné)**: Volitelně můžete zadat popis tohoto nasazení.  


### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a>Možnosti **obsahu** nasazení

Na stránce **obsah** klikněte na tlačítko **Přidat** a distribuujte obsah této aplikace do distribučního bodu nebo skupiny distribučních bodů.

Pokud jste na stránce Obecné vybrali možnost **použít výchozí distribuční body přidružené k této kolekci** , pak se tato možnost vyplní automaticky. Pouze člen role zabezpečení **Správce aplikací** ho může upravit.

Pokud je obsah aplikace již distribuován, zobrazí se zde.


### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a>**Nastavení nasazení**

Na stránce **nastavení nasazení** zadejte následující informace:  

- **Akce**: v rozevíracím seznamu vyberte, zda toto nasazení má být aplikace **nainstalována** nebo **odinstalována** .  

    > [!NOTE]  
    > Pokud vytvoříte nasazení pro **instalaci** aplikace a jiné nasazení pro **Odinstalování** stejné aplikace na stejném zařízení, má nasazení **instalace** přednost.  

    Akci nasazení po jeho vytvoření nemůžete změnit.  

- **Účel**: V rozevíracím seznamu vyberte jednu z těchto možností:  

  - **K dispozici**: uživatel uvidí aplikaci v centru softwaru. Můžou ho instalovat na vyžádání.  

  - **Požadováno**: klient automaticky nainstaluje aplikaci podle plánu, který jste nastavili. Pokud aplikace není skrytá, může uživatel sledovat jeho stav nasazení. Můžou také pomocí centra softwaru instalovat aplikaci před konečným termínem.  

    > [!NOTE]  
    > Když nastavíte akci nasazení na **odinstalace**, bude účel nasazení automaticky nastaven na **požadováno**. Toto chování nemůžete změnit.  

- **Povolit koncovým uživatelům pokusit se opravit tuto aplikaci**: od verze 1810, pokud jste aplikaci vytvořili pomocí příkazového řádku opravit, povolte tuto možnost. Uživatelé uvidí možnost v centru softwaru k **opravě** aplikace.<!--1357866-->  

- **Předem nasadit software na primární zařízení uživatele**: Pokud je nasazení pro uživatele, vyberte tuto možnost, pokud chcete aplikaci nasadit na primární zařízení uživatele. Toto nastavení nevyžaduje, aby se uživatel přihlásil před spuštěním nasazení. Pokud uživatel musí s instalací pracovat, tuto možnost nevybírejte. Tato možnost je k dispozici pouze v případě, že je nasazení **požadováno**.  

- **Odeslat pakety pro probuzení**: Pokud je nasazení **požadováno**, Configuration Manager odešle paket buzení ze spánku do počítačů předtím, než klient spustí nasazení. Tento paket probudit počítače v konečném termínu instalace. Než použijete tuto možnost, musí být počítače a sítě nakonfigurované pro Wake On LAN. Další informace najdete v tématu [plánování probuzení klientů](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Umožňuje klientům v měřeném připojení k internetu stahovat obsah po uplynutí konečného termínu instalace, což může způsobit další náklady**: Tato možnost je dostupná jenom pro nasazení s účelem **požadované**.  

- **Automaticky upgradovat všechny nahrazené verze této aplikace**: klient upgraduje všechny nahrazené verze aplikace pomocí nahrazující aplikace.

    > [!Note]  
    > Tato možnost funguje bez ohledu na schválení správce. Pokud správce již schválil nahrazenou verzi, nemusí také schvalovat nahrazující verzi. Schválení je pouze pro nové požadavky, nikoli pro nahrazující upgrady.<!--515824-->  
    >
    > V případě **dostupného** účelu instalace můžete tuto možnost povolit nebo zakázat. <!--1351266-->


#### <a name="approval-settings"></a><a name="bkmk_approval"></a>Nastavení schválení

Chování při schvalování aplikací závisí na tom, jestli povolíte doporučenou volitelnou funkci a **schválíte požadavky aplikací pro uživatele na zařízení**.

- **Správce musí na zařízení schválit žádost o tuto aplikaci**: Pokud povolíte volitelnou funkci, správce schválí všechny požadavky uživatelů na aplikaci, aby ji uživatel mohl nainstalovat na požadované zařízení. Pokud správce žádost schválí, uživatel může aplikaci nainstalovat jenom na toto zařízení. Uživatel musí odeslat další žádost o instalaci aplikace na jiné zařízení. Tato možnost je zobrazena šedě, pokud je **požadován**účel nasazení nebo když nasadíte aplikaci do kolekce zařízení.

- **Vyžadovat schválení správce, pokud uživatelé požadují tuto aplikaci**: Pokud nepovolíte volitelnou funkci, správce schválí všechny požadavky uživatelů na aplikaci, aby ji uživatel mohl nainstalovat. Tato možnost je zobrazena šedě, pokud je **požadován**účel nasazení nebo když nasadíte aplikaci do kolekce zařízení.  

Další informace najdete v tématu [schvalování aplikací](app-approval.md).


#### <a name="deployment-properties-deployment-settings"></a>Vlastnosti nasazení – **nastavení nasazení**

Pokud zobrazíte vlastnosti nasazení, je-li podporováno technologií typu nasazení, na kartě **nastavení nasazení** se zobrazí následující možnost:

**Automaticky zavřete všechny spuštěné spustitelné soubory, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení**. Další informace najdete v tématu [kontroly spouštění spustitelných souborů před instalací aplikace](#bkmk_exe-check).



### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a>Nastavení **plánování** nasazení

Na stránce **plánování** nastavte čas, kdy se tato aplikace nasadí nebo zpřístupní klientským zařízením.

Ve výchozím nastavení Configuration Manager zásady nasazení zpřístupnit klientům hned. Pokud chcete vytvořit nasazení, ale nikoli zpřístupnit klientům do pozdějšího data, nakonfigurujte možnost **plánování dostupnosti aplikace**. Pak vyberte datum a čas, včetně toho, jestli je založené na standardu UTC nebo místního času klienta.

Pokud je nasazení **požadováno**, zadejte také **konečný termín instalace**. Ve výchozím nastavení je tento konečný termín co nejrychleji.

Například je třeba nasadit novou obchodní aplikaci. Všichni uživatelé ji potřebují nainstalovat v určitou dobu, ale chcete jim dát možnost se k brzkému přihlášení přihlásit. Také je nutné zajistit, aby lokalita rozšíří obsah do všech distribučních bodů. Naplánujete, aby byla aplikace k dispozici po dobu 5 dní od dnešního dne. Tento plán vám poskytne čas k distribuci obsahu a potvrzení jeho stavu. Potom nastavíte konečný termín instalace na jeden měsíc od dnešního dne. Uživatelé uvidí aplikaci v centru softwaru, když jsou k dispozici během pěti dnů. Pokud to neudělá, klient v konečném termínu instalace automaticky nainstaluje aplikaci.

Pokud aplikace, kterou nasazujete, nahrazuje jinou aplikaci, nastavte konečný termín instalace, kdy uživatelé obdrží novou aplikaci. Nastavte **konečný termín instalace** pro upgrade uživatelů pomocí nahrazené aplikace.


#### <a name="delay-enforcement-with-a-grace-period"></a>Zpoždění vynucení s obdobím odkladu

Může být vhodné dát uživatelům větší čas na instalaci požadovaných aplikací *nad rámec* všech stanovených termínů. Toto chování se většinou vyžaduje v případě, že je počítač vypnutý dlouhou dobu a potřebuje nainstalovat spoustu aplikací. Například pokud se uživatel vrátí z dovolené, musí počkat dlouhou dobu, než klient nainstaluje zpožděná nasazení. Chcete-li tento problém vyřešit, definujte období odkladu vynucení.

- Nejdřív nakonfigurujte tuto poskytnutou dobu odkladu s **časovým obdobím pro vynucení po termínu nasazení (hodiny)** v nastavení klienta. Další informace najdete v tématu skupina [Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent) . Zadejte hodnotu v rozmezí **1** až **120** hodin.  

- Na stránce **plánování** požadovaného nasazení aplikace povolte možnost **odložit vynucení tohoto nasazení podle uživatelských preferencí, až do období odkladu definovaného v nastavení klienta**. Poskytnutá lhůta vynucení platí pro všechna nasazení s povolenou možností a cílí na zařízení, na která jste nasadili také nastavení klienta.

Po uplynutí konečného termínu klient nainstaluje aplikaci v prvním nefiremním okně, které uživatel nakonfigurovali, až do této lhůty odkladu. Uživatel ale přesto může spustit Centrum softwaru a nainstalovat aplikaci kdykoli. Jakmile vyprší lhůta odkladu, vynucení se vrátí do normálního chování pro zpožděná nasazení.

![Diagram časové osy období odkladu](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> Ve většině případů tato funkce řeší situaci, kdy je zařízení vypnuté, když je uživatel mimo kancelář. Technicky, období odkladu začíná, když klient získá zásady po konečném termínu nasazení. Ke stejnému chování dojde, pokud zastavíte službu Configuration Manager klienta (CcmExec) a pak ji znovu spustíte později po konečném termínu nasazení.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a>Nastavení **uživatelského prostředí** nasazení

Na stránce **činnost koncového uživatele** zadejte informace o tom, jak můžou uživatelé s instalací aplikace pracovat.

- **Oznámení uživateli**: Určuje, jestli se má v centru softwaru v nakonfigurovaném čase zobrazovat oznámení. Toto nastavení také určuje, zda mají být uživatelé upozorněni na klientské počítače. U dostupných nasazení nemůžete vybrat možnost, která se má **Skrýt v nástroji Software Center a všech oznámeních**.  

    - **Když se vyžadují změny softwaru, zobrazí se uživateli dialogové okno namísto informačního oznámení.**<!--3555947-->: Od verze 1902 vyberte tuto možnost, chcete-li změnit činnost uživatele, aby byla více rušivá. Platí jenom pro požadovaná nasazení. Další informace najdete v tématu [plánování centra softwaru](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Instalace softwaru** a **restart systému**: Nakonfigurujte tato nastavení jenom pro požadovaná nasazení. Určují chování, když nasazení dosáhne konečného termínu mimo jakákoli definovaná časová období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.  

- **Zpracování filtru zápisu pro zařízení se systémem Windows Embedded**: Toto nastavení řídí chování při instalaci na zařízeních se systémem Windows Embedded, která jsou povolena pomocí filtru zápisu. Vyberte možnost potvrdit změny při dokončení instalace nebo během časového období údržby. Když vyberete tuto možnost, vyžaduje se restartování a změny se na zařízení zachovají. V opačném případě se aplikace nainstaluje do dočasného překrytí a potvrdí se později.  

    - Když nasadíte aktualizaci softwaru do zařízení se systémem Windows Embedded, ujistěte se, že je zařízení členem kolekce, která má nakonfigurované časové období údržby. Další informace o oknech údržby a zařízeních se systémem Windows Embedded najdete v tématu [vytváření aplikací pro Windows Embedded](../get-started/creating-windows-embedded-applications.md).  


### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>**Výstrahy** nasazení

Na stránce **výstrahy** nakonfigurujte, jak Configuration Manager generuje výstrahy pro toto nasazení. Pokud používáte i System Center Operations Manager, nakonfigurujte také jeho výstrahy. Pro požadovaná nasazení můžete nakonfigurovat pouze některé výstrahy. 


## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a>Vytvoření postupného nasazení

<!--1358147-->
Počínaje verzí 1806 vytvořte dvoufázové nasazení pro aplikaci. Postupné nasazení vám umožní orchestrovat koordinované, sekvenční zavedení softwaru na základě přizpůsobitelných kritérií a skupin. Například Nasaďte aplikaci do pilotní kolekce a potom automaticky pokračuje v zavedení na základě kritérií úspěchů.

Další informace najdete v těchto článcích:  

- [Vytvoření postupného nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Správa a sledování postupných nasazení](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a>Odstranění nasazení

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** nebo **skupiny aplikací** .  

2. Vyberte aplikaci nebo skupinu aplikací, které obsahují nasazení, které chcete odstranit.  

3. Přepněte na kartu **nasazení** v podokně podrobností a vyberte nasazení.  

4. Na pásu karet na kartě **nasazení** a ve skupině **nasazení** klikněte na **Odstranit**.  

Při odstranění nasazení aplikace nebudou odebrány všechny instance aplikace, které již klienti nainstalovali. Chcete-li odebrat tyto aplikace, nasaďte aplikaci na počítače, které chcete **odinstalovat**. Pokud odstraníte nasazení aplikace nebo odeberete prostředek z kolekce, do které nasazujete, aplikace se už nebude zobrazovat v centru softwaru.



## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a>Oznámení uživatelů pro požadovaná nasazení

Když uživatelé dostanou požadovaný software, vyberte nastavení připomenout **a připomenout** , které si můžou vybrat z následujících možností:  

- **Později**: Určuje, zda jsou oznámení naplánována na základě nastavení oznámení nakonfigurovaného v nastavení klienta.  

- **Pevná doba**: Určuje, zda má být u oznámení naplánováno zobrazení po zvoleném čase. Pokud například vyberete 30 minut, oznámení se znovu zobrazí za 30 minut.  

![Skupina Počítačový agent ve výchozím nastavení klienta](media/ComputerAgentSettings.png)

Maximální doba odložení je vždy založena na hodnotách oznámení nakonfigurovaných v nastavení klienta při každé časové ose nasazení. Příklad:  

- **Konečný termín nasazení je delší než 24 hodin a nastavení připomenout uživatele po dobu (hodiny)** na stránce **Počítačový agent** po dobu 10 hodin.  

- Klient zobrazí dialog oznámení delší než 24 hodin před konečným termínem nasazení.  

- Dialog zobrazuje možnosti odložení až do 10 hodin, ale ne nikdy více.  

- V případě, že se blíží konečný termín nasazení, zobrazuje dialogové okno méně možností. Tyto možnosti jsou v souladu s příslušnými nastaveními klienta pro každou součást časové osy nasazení.  

V případě nasazení s vysokým rizikem, jako je pořadí úkolů, které nasazuje operační systém, je uživatelské prostředí upozorňovánější. Místo dočasného oznámení na hlavním panelu se zobrazí dialogové okno podobné následujícímu: pokaždé, když se vám zobrazí upozornění, že je nutná údržba nejdůležitějšího softwaru:

![Požadovaný softwarový Dialog upozorňuje na údržbu kritického softwaru.](media/client-toast-notification.png)



## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a>Kontrolovat spouštění spustitelných souborů

Nakonfigurujte nasazení, aby kontrolovalo, jestli jsou na klientovi spuštěné některé spustitelné soubory. Tato možnost slouží ke kontrole procesů, které mohou narušit instalaci aplikace. Pokud je některý z těchto spustitelných souborů spuštěný, klient zablokuje instalaci typu nasazení. Aby mohl uživatel nainstalovat typ nasazení, musí zavřít spuštěný spustitelný soubor. Pro nasazení s účelem požadováno může klient automaticky zavřít běžící spustitelný soubor.

1. Otevřete dialogové okno **vlastnosti** pro typ nasazení.  

2. Přepněte na kartu **chování instalace** a klikněte na **Přidat**.  

3. V dialogovém okně **Přidat spustitelný soubor** zadejte název cílového spustitelného souboru. Volitelně můžete zadat popisný název aplikace, který vám usnadní jeho identifikaci v seznamu.  

4. Klikněte na tlačítko **OK**a potom kliknutím na tlačítko **OK** zavřete okno Vlastnosti typu nasazení.  

5. Když nasadíte aplikaci, vyberte možnost **automaticky zavřít všechny spuštěné spustitelné soubory, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení**. Tato možnost je na kartě **nastavení nasazení** ve vlastnostech nasazení.  

> [!Note]
> Pokud nakonfigurujete aplikaci pro kontrolu spouštění spustitelných souborů a zahrnete ji do kroku pořadí úloh [instalovat aplikaci](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) , pořadí úkolů ji nepůjde nainstalovat. Pokud tento krok pořadí úkolů nenastavíte tak, aby pokračoval při chybě, pak celé pořadí úkolů se nezdařilo.

### <a name="client-behaviors-and-user-notifications"></a>Chování klienta a oznámení uživateli

Jakmile klienti dostanou nasazení, platí následující chování:  

- Pokud jste aplikaci nasadili jako **dostupnou**a uživatel se pokusí ji nainstalovat, klient vyzve uživatele, aby před pokračováním v instalaci zavřel zadané spuštěné spustitelné soubory.  

- Pokud jste aplikaci nasadili podle **potřeby**a zadali **jste k automatickému zavření všech spuštěných spustitelných souborů, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení**, klient zobrazí oznámení. Informuje uživatele o tom, že zadané spustitelné soubory se automaticky zavřou, když je dosaženo konečného termínu instalace aplikace.  

    - Naplánujte Tato dialogová okna ve skupině **Počítačový agent** v nastavení klienta. Další informace najdete v tématu [Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    - Pokud nechcete, aby uživatel tyto zprávy zobrazil, vyberte možnost **Skrýt v nástroji Software Center a všech oznámeních** na kartě **činnost koncového uživatele** ve vlastnostech nasazení. Další informace najdete v tématu [nasazení nastavení uživatelského prostředí](#bkmk_deploy-ux).  

- Pokud jste aplikaci nasadili podle **potřeby**a neurčili jste **automaticky zavřít všechny spuštěné spustitelné soubory zadané na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení**, pak se instalace aplikace nezdařila, pokud je spuštěna jedna nebo více zadaných aplikací.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Nasazení aplikací dostupných pro uživatele na zařízeních připojených k Azure AD

<!-- 1322613 -->
Pokud nasadíte aplikace jako dostupné pro uživatele, mohou je Procházet a instalovat prostřednictvím centra softwaru v Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Požadavky

- Povolit HTTPS v bodu správy  

- Integrace lokality se službou [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) pro **správu cloudu**  

    - Konfigurace [zjišťování uživatelů Azure AD](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Nasazení aplikace jako dostupné pro kolekci uživatelů ze služby Azure AD  

- Distribuce libovolného obsahu aplikace do [distribučního bodu cloudu](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- Povolit nastavení klienta **použít nové centrum softwaru** ve skupině [Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent)  

- Operační systém klienta musí být Windows 10 a připojený ke službě Azure AD. Buď jako čistě cloudová doména připojená, nebo do služby Azure AD připojené k hybridní službě Azure AD.  

- Podpora internetových klientů:  

    - [Brána pro správu cloudu](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

    - Povolit nastavení klienta: **Povolit žádosti o zásady uživatele od internetových klientů** ve skupině [zásad klienta](../../core/clients/deploy/about-client-settings.md#client-policy)  

- Pro podporu klientů na intranetu:  

    - Přidat distribuční bod cloudu do hraniční skupiny používané klienty  

    - Klienti musí přeložit plně kvalifikovaný název domény (FQDN) bodu správy s povoleným protokolem HTTPS.  



## <a name="next-steps"></a>Další kroky

- [Monitorování aplikací](monitor-applications-from-the-console.md)
- [Řešení problémů s nasazováním aplikací](troubleshoot-application-deployment.md)
- [Úlohy správy pro aplikace](management-tasks-applications.md)
- [Uživatelská příručka Centra softwaru](../../core/understand/software-center.md)
