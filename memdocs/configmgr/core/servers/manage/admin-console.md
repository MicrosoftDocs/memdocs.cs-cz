---
title: Konzola nástroje Configuration Manager
titleSuffix: Configuration Manager
description: Přečtěte si informace o navigaci prostřednictvím konzoly Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ac5b3ca8e8e2231bb421838fa56b20253ddfcb74
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878375"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Jak používat konzolu Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Správci používají konzolu Configuration Manager ke správě prostředí Configuration Manager. Tento článek se zabývá základy navigace v konzole nástroje.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Otevřete konzolu

Konzola Configuration Manager je vždy nainstalována na každém serveru lokality. Můžete ho také nainstalovat na jiné počítače. Další informace najdete v tématu [Instalace konzoly Configuration Manager](../deploy/install/install-consoles.md).

Nejjednodušší způsob, jak otevřít konzolu na počítači s Windows 10, můžete stisknout **Start** a začít psát `Configuration Manager console` . Možná nebudete muset zadávat celý řetězec pro Windows, abyste našli nejlepší shodu.

Pokud procházíte v nabídce Start, vyhledejte ikonu **konzoly Configuration Manager** ve skupině **Microsoft Endpoint Manager** .

![Ikony nabídky Start pro Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Cesta v nabídce Start se změnila ve verzi 1910. Ve verzi 1906 a starší se jedná o název složky **System Center**. Když aktualizujete Configuration Manager na verzi 1910 nebo novější, nezapomeňte aktualizovat jakoukoli interní dokumentaci, kterou udržujete, aby zahrnovala toto nové umístění.

## <a name="connect-to-a-site-server"></a>Připojit k serveru lokality

Konzola se připojí k serveru lokality centrální správy nebo k serverům primární lokality. Nemůžete připojit konzolu Configuration Manager k sekundární lokalitě. Během instalace jste zadali plně kvalifikovaný název domény (FQDN) serveru lokality, ke které se konzola připojuje.

Pokud se chcete připojit k jinému serveru lokality, použijte následující postup:

1. Vyberte šipku v horní části [pásu karet](#ribbon)a zvolte **připojit k novému webu**.  

    ![Připojit konzolu k nové lokalitě](media/connect-to-a-new-site.png)  

2. Zadejte plně kvalifikovaný název domény serveru lokality. Pokud jste se dříve připojili k serveru lokality, vyberte server z rozevíracího seznamu.  

    ![Okno připojení k webu zadejte plně kvalifikovaný název domény serveru lokality.](media/site-server-fqdn.png)  

3. Vyberte **Připojit**.  

Počínaje verzí 1810 můžete určit minimální úroveň ověřování pro správce pro přístup k Configuration Manager lokalit. Tato funkce vynutila správcům přihlášení k systému Windows s požadovanou úrovní. Další informace najdete v tématu [plánování poskytovatele serveru SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Navigace

Některé oblasti konzoly nemusí být viditelné v závislosti na přiřazené roli zabezpečení. Další informace o rolích najdete v tématu [základy správy na základě rolí](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Pracovní prostory

Konzola Configuration Manager má čtyři **pracovní prostory**:  

- **Prostředky a kompatibilita**  

- **Softwarová knihovna**  

- **Monitorování**  

- **Správa**  

![Configuration Manager pracovní prostory s místní nabídkou](media/configuration-manager-workspaces.png)  

Změnou pořadí tlačítek pracovního prostoru vyberte šipku dolů a zvolte **Možnosti navigačního podokna**. Vyberte položku, kterou chcete **Přesunout nahoru** nebo **dolů**. Vyberte **obnovit** , pokud chcete obnovit výchozí pořadí tlačítek.  

![Okno možností navigačního podokna k uspořádání pracovních prostorů](media/navigation-pane-options.png)  

Minimalizujte tlačítko pracovní prostor výběrem **Zobrazit méně tlačítek**. Poslední pracovní prostor v seznamu je minimalizován jako první. Vyberte minimalizované tlačítko a kliknutím na tlačítko **Zobrazit další tlačítka** obnovte jeho původní velikost.

![Minimalizované pracovní prostory v konzole Configuration Manager](media/workspace-buttons.png)  

### <a name="nodes"></a>Uzly

Pracovní prostory jsou kolekce **uzlů**. Jedním z příkladů uzlů je uzel **skupiny aktualizací softwaru** v pracovním prostoru **softwarová knihovna** .

Až budete v uzlu, můžete vybrat šipku pro minimalizaci navigačního podokna.  

![Příklad uzlu a zvýraznění – minimalizace šipky](media/software-update-groups-node.png)  

Pomocí **navigačního panelu** se můžete pohybovat v konzole nástroje, když minimalizujete navigační podokno.  

![Configuration Manager minimalizované navigační podokno](media/minimized-navigation-pane.png)  

V konzole nástroje jsou uzly někdy uspořádány do složek. Když vyberete složku, obvykle se zobrazí **navigační index** nebo **řídicí panel**.  

![Navigační index pro Configuration Manager aktualizace softwaru](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Pásem

Pás karet je v horní části konzoly Configuration Manager. Pás karet může mít více než jednu kartu a může být minimalizován pomocí šipky vpravo. Tlačítka na pásu karet se mění v závislosti na uzlu. Většina tlačítek na pásu karet je také k dispozici v místních nabídkách.  

![Ukázkový pás karet, zvýraznění více karet a minimalizace šipky](media/ribbon.png)

### <a name="details-pane"></a>Podokno podrobností

Další informace o položkách najdete v podokně podrobností. Podokno podrobností může mít jednu nebo více karet. Karty se liší v závislosti na uzlu.  

![Configuration Manager příklad podokna podrobností](media/details-pane.png)

### <a name="columns"></a>Sloupce

Můžete přidat, odstranit, změnit pořadí a změnit velikost sloupců. Tyto akce umožňují zobrazit data, která dáváte přednost. Dostupné sloupce se liší v závislosti na uzlu. Chcete-li přidat nebo odebrat sloupec ze zobrazení, klikněte pravým tlačítkem myši na záhlaví existujícího sloupce a vyberte položku. Přeuspořádat sloupce přetažením záhlaví sloupce, kde byste chtěli být.  

![Správci konfigurace přidat sloupec](media/add-columns.png)  

V dolní části kontextové nabídky sloupce můžete řadit nebo seskupovat podle sloupce. Můžete také řadit podle sloupce tak, že vyberete jeho záhlaví.  

![Configuration Manager seskupit podle sloupce](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a>Uvolnění zámku pro úpravy objektů

<!--4786915-->

Pokud konzola Configuration Manager přestane reagovat, můžete se před 30 Minuti zablokovat a provést další změny, dokud zámek nevyprší. Tento zámek je součástí Configuration Manager SEDO (serializovaná úprava distribuovaných objektů). Další informace najdete v tématu [Configuration Manager SEDO](../../../develop/core/understand/sedo.md).

Od [aktuální větve verze 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)můžete zrušit zámek pro pořadí úkolů. Počínaje verzí 1910 můžete zrušit zámek pro libovolný objekt v konzole Configuration Manager.

Tato akce se vztahuje jenom na váš uživatelský účet, který má zámek, a na stejném zařízení, ze kterého web udělil zámek. Když se pokusíte o přístup k uzamčenému objektu, můžete nyní **zrušit změny**a pokračovat v úpravách objektu. Tyto změny by se ztratily i po vypršení platnosti zámku.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a>Zobrazit nedávno připojené konzoly

<!--3699367-->
Počínaje verzí 1902 můžete zobrazit nejnovější připojení pro konzolu Configuration Manager. Zobrazení zahrnuje aktivní připojení a připojení, která se nedávno připojila. V seznamu se vždycky zobrazí aktuální připojení konzoly a zobrazí se jenom připojení z konzoly Configuration Manager. K poskytovateli serveru SMS se nezobrazuje prostředí PowerShell nebo jiná připojení založená na sadě SDK. Lokalita odebere instance ze seznamu, které jsou starší než 30 dní.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a>Předpoklady pro zobrazení připojených konzol

- Váš účet potřebuje oprávnění **číst** pro objekt **SMS_Site** .

- Nakonfigurujte REST API služby správy. Další informace najdete v tématu [co je služba pro správu?](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>Zobrazit připojené konzoly

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** .  

2. Rozbalte položku **zabezpečení** a vyberte uzel **připojení konzoly** .  

3. Podívejte se na poslední připojení s následujícími vlastnostmi:  

    - Uživatelské jméno
    - Název počítače
    - Kód připojené lokality
    - Verze konzoly
    - Čas posledního připojení: když uživatel naposledy *otevřel* konzolu
    - Počínaje verzí 1910 se poslední sloupec **prezenčního signálu konzoly** nahradil sloupcem **naposledy připojeného času** . <!--4923997-->
       - Otevřená konzola v popředí odesílá prezenční signál každých 10 minut.

![Zobrazit Configuration Manager připojení konzoly](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a>Spustit chat Microsoft Teams z připojení konzoly
<!--4923997-->
*(Představené ve verzi 1910)*

Počínaje verzí 1910 můžete ostatním správcům Configuration Manager zpráv z uzlu **připojení konzoly** pomocí Microsoft Teams. Pokud se rozhodnete **Spustit Microsoft Teams chat** s správcem, spustí se Microsoft teams a otevře se s ním chat.

### <a name="prerequisites"></a>Požadavky

- Aby bylo možné spustit chat se správcem, účet, se kterým chcete chatovat, musí být zjištěn pomocí [Azure AD nebo zjišťování uživatelů služby AD](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Microsoft Teams je nainstalovaný na zařízení, ze kterého spouštíte konzolu.
značte
- Všechny [požadavky pro zobrazení připojených konzol](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Spustit chat Microsoft Teams

1. Přejít do **Administration**  >  konzoly**zabezpečení**Správa  >  **připojení**.
1. Klikněte pravým tlačítkem na připojení ke konzole uživatele a vyberte **Spustit chat Microsoft Teams**.
    - Pokud se hlavní název uživatele pro vybraného správce nenajde, **Spusťte chat Microsoft Teams chat** šedě.
    - Pokud na zařízení, ze kterého spouštíte konzolu, není nainstalovaný Microsoft teams, zobrazí se chybová zpráva, včetně odkazu ke stažení.
    - Pokud jsou na zařízení, ze kterého konzolu spouštíte, nainstalované Microsoft teams, otevře se s uživatelem chat.

### <a name="known-issues"></a>Známé problémy

Chybová zpráva oznamující, že Microsoft Teams není nainstalovaný, se nezobrazí, pokud následující klíč registru neexistuje:

Počítač \ HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Pokud chcete tento problém obejít, vytvořte ručně klíč registru.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a>Oznámení konzoly Configuration Manager

<!--3556016, fka 1318035-->
Od verze Configuration Manager 1902 vás konzola upozorní na následující události:

- Když je k dispozici aktualizace pro Configuration Manager sebe sama
- V případě, že dojde k událostem životního cyklu a údržby v prostředí

Toto oznámení je pruhem v horní části okna konzoly pod pás karet. Nahrazuje předchozí prostředí, když Configuration Manager aktualizace k dispozici. Tato oznámení v konzole stále zobrazují důležité informace, ale nebrání v práci v konzole nástroje. Nemůžete zavřít kritická oznámení. Konzola zobrazí všechna oznámení v nové oblasti oznámení v záhlaví.

![Oznamovací pruh a příznak v konzole](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Nakonfigurovat lokalitu, aby zobrazovala Nekritická oznámení

Každou lokalitu můžete nakonfigurovat tak, aby zobrazovala Nekritická oznámení ve vlastnostech lokality.

1. V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**a pak vyberte uzel **lokality** .
1. Vyberte lokalitu, kterou chcete nakonfigurovat pro Nekritická oznámení.
1. Na pásu karet vyberte možnost **vlastnosti**.
1. Na kartě **výstrahy** vyberte možnost **Povolení oznámení konzoly pro nekritické změny stavu lokality**.
   - Pokud povolíte toto nastavení, všichni uživatelé konzoly uvidí upozornění na kritická, varovná a informační oznámení. Toto nastavení je standardně zapnuté.  
   - Pokud toto nastavení zakážete, budou se uživatelům konzoly zobrazovat jenom kritická oznámení.  

Většina oznámení konzoly je vázaná na jednu relaci. Konzola vyhodnocuje dotazy, když je uživatel spustí. Chcete-li zobrazit změny v oznámeních, restartujte konzolu. Pokud uživatel zahodí nekritické oznámení, znovu se upozorní, jakmile se konzola restartuje, pokud je stále k dispozici.

Následující oznámení se znovu vyhodnotí každých pět minut:

- Lokalita je v režimu údržby.  
- Lokalita je v režimu obnovení.  
- Lokalita je v režimu upgradu.  

Oznámení se řídí oprávněními pro správu na základě rolí. Pokud například uživatel nemá oprávnění k zobrazení Configuration Manager aktualizace, neuvidí tato oznámení.

Některá oznámení mají související akci. Pokud se například verze konzoly neshoduje s verzí lokality, vyberte **nainstalovat novou verzi konzoly**. Tato akce spustí instalační program konzoly.

Pro větev Technical Preview platí následující oznámení:  

- Zkušební verze spadá do 30 dnů od vypršení platnosti (upozornění): aktuální datum spadá do 30 dnů od data vypršení platnosti zkušební verze.  
- Platnost zkušební verze vypršela (kritická): aktuální datum následuje po datu vypršení platnosti zkušební verze.  
- Neshoda verzí konzoly (kritická): verze konzoly neodpovídá verzi lokality.  
- Je k dispozici upgrade lokality (upozornění): je k dispozici nový balíček aktualizace.  

Další informace a pomoc při řešení potíží najdete v souboru **SmsAdminUI. log** v počítači konzoly. Ve výchozím nastavení se tento soubor protokolu nachází v následující cestě: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log` .


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a>Řídicí panel dokumentace konzoly

<!--3556019 FKA 1357546-->
Od verze Configuration Manager 1902 je v novém pracovním prostoru **komunity** k dispozici uzel **dokumentace** . Tento uzel obsahuje aktuální informace o Configuration Manager dokumentaci a články o podpoře. Obsahuje následující oddíly:  

### <a name="product-documentation-library"></a>Knihovna dokumentace k produktu

- **Doporučené**: ručně seznam důležitých článků.
- **Trendy**: nejoblíbenější články za poslední měsíc.
- **Nedávno aktualizované**: články byly v posledním měsíci revidovány.

### <a name="support-articles"></a>Články o podpoře

- **Články týkající se řešení potíží**s postupy, které vám pomůžou při řešení potíží s Configuration Manager komponentami a funkcemi.
- **Nové a aktualizované články podpory**: články, které jsou v posledních dvou měsících nové nebo aktualizované.

### <a name="troubleshooting-connection-errors"></a>Řešení chyb připojení
Uzel **dokumentace** nemá žádnou explicitní konfiguraci proxy serveru. Používá všechny proxy definované v operačním systému v apletu ovládacího panelu **Možnosti Internetu** . Pokud to chcete zkusit znovu po chybě připojení, aktualizujte uzel **dokumentace** .


## <a name="command-line-options"></a>Možnosti příkazového řádku

Konzola Configuration Manager má následující možnosti příkazového řádku:

|Možnost|Description|  
|------------|-----------------|  
|`/sms:debugview=1`|Nástroj DebugView je součástí všech ResultViews, které určují zobrazení. Nástroj DebugView zobrazí nezpracované vlastnosti (názvy a hodnoty).|  
|`/sms:NamespaceView=1`|Zobrazuje zobrazení oboru názvů v konzole nástroje.|  
|`/sms:ResetSettings`|Konzola ignoruje uživatelem uložené připojení a stavy zobrazení. Velikost okna není resetována.|  
|`/sms:IgnoreExtensions`|Zakáže všechna Configuration Manager rozšíření.|  
|`/sms:NoRestore`|Konzola ignoruje předchozí trvalý navigační uzel.|  


## <a name="tips"></a>Tipy

### <a name="general"></a>Obecné

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Vylepšení hledání konzoly
<!--4640570-->
*(Představené ve verzi 1910)*

- V uzlech **balíčky ovladačů** a **dotazy** můžete použít možnost Hledat **všechny podsložky** .<!--2841181,5424892--> Počínaje verzí 2002 Tato možnost slouží také v uzlech **položky konfigurace** a **standardní hodnoty konfigurace** .<!--5891241-->

- Když hledání vrátí více než 1 000 výsledků, kliknutím na tlačítko **OK** na panelu oznámení zobrazíte další výsledky.<!--4640570-->

    ![Snímek obrazovky s panelem upozornění pro příliš mnoho výsledků hledání](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Výchozí omezení výsledků hledání je 1 000. Tuto výchozí hodnotu můžete změnit. V konzole Configuration Manager otevřete na pásu karet kartu **Hledat** . Ve skupině **Možnosti** vyberte **Nastavení hledání**. Změňte hodnotu **výsledků hledání** . Zobrazení většího počtu výsledků hledání může trvat delší dobu.
    >
    > Ve výchozím nastavení je maximální horní limit 100 000. Pokud chcete tento limit změnit, nastavte hodnotu DWORD **QueryResultCountMaximum** v následujícím klíči registru:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > Nastavení in-Console odpovídá hodnotě **QueryResultCountLimit** ve stejném klíči. Správce může tyto hodnoty nakonfigurovat v podregistru HKLM pro všechny uživatele zařízení. Hodnota HKCU přepisuje nastavení HKLM.

#### <a name="role-based-administration-for-folders"></a>Správa na základě rolí pro složky
<!--3600867-->
*(Představené ve verzi 1906)*

Pro složky můžete nastavit rozsahy zabezpečení. Pokud máte přístup k objektu ve složce, ale nemáte přístup ke složce, nebudete moct objekt zobrazit. Podobně platí, že pokud máte přístup do složky, ale ne do objektu, neuvidíte tento objekt. Klikněte pravým tlačítkem myši na složku, zvolte možnost **nastavit rozsahy zabezpečení**a pak zvolte rozsahy zabezpečení, které chcete použít.

#### <a name="views-sort-by-integer-values"></a>Zobrazení – seřadit podle celočíselných hodnot

*(Představené ve verzi 1902)*

Provedli jsme vylepšení způsobu řazení dat v různých zobrazeních. Například v uzlu **nasazení** pracovního prostoru **monitorování** nyní následující sloupce seřadí jako čísla namísto řetězcových hodnot:  

- Počet chyb
- Počet probíhajících
- Jiné číslo
- Počet úspěchů
- Neznámé číslo  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Přesunutí upozornění na velký počet výsledků

*(Představené ve verzi 1902)*

Když v konzole vyberete uzel, který vrátí více než 1 000 výsledků, Configuration Manager zobrazí následující upozornění:

> Configuration Manager vrátil velký počet výsledků. Výsledky můžete zúžit pomocí vyhledávání. Případně můžete kliknutím sem zobrazit maximálně 100000 výsledků.

Mezi tímto upozorněním a polem hledání je teď další prázdné místo. Tento přesun pomáhá zabránit nechtěnému výběru upozornění pro zobrazení dalších výsledků.

#### <a name="send-feedback"></a>Odeslat názor

*(Představené ve verzi 1806)*
<!--1357542-->

Odešlete zpětnou vazbu produktu z konzoly.  

- **Poslat smajlíka**: pošlete nám svůj názor na to, co se vám líbí.  

- **Odeslání zamračení**: pošlete nám svůj názor na to, co jste nechtěli.  

- **Odeslání návrhu**: přejdete na UserVoice, abyste mohli sdílet svůj nápad.  

Další informace najdete v tématu o [zpětné vazbě produktu](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Pracovní prostor prostředky a kompatibilita

#### <a name="real-time-actions-from-device-lists"></a>Akce ze seznamů zařízení v reálném čase
<!--4616810-->
*(Představené ve verzi 1906)*

Existují různé způsoby, jak zobrazit seznam zařízení v uzlu **zařízení** v pracovním prostoru **prostředky a kompatibilita** .

- V pracovním prostoru **prostředky a kompatibilita** vyberte uzel **kolekce zařízení** . Vyberte kolekci zařízení a zvolte akci pro **zobrazení členů**. Tato akce otevře dílčí uzel uzlu **zařízení** se seznamem zařízení pro tuto kolekci.  

  - Když vyberete dílčí uzel kolekce, můžete nyní začít **CMPivot** ze skupiny kolekcí na pásu karet.  

- V pracovním prostoru **monitorování** vyberte uzel **nasazení** . Vyberte nasazení a na pásu karet zvolte akci **Zobrazit stav** . V podokně Stav nasazení dvakrát klikněte na celkový počet assetů, aby bylo možné přejít k seznamu zařízení.  

  - Když v tomto seznamu vyberete zařízení, teď můžete začít **CMPivot** a **spouštět skripty** ze skupiny zařízení na pásu karet.  


#### <a name="collections-tab-in-devices-node"></a>Karta kolekce v uzlu zařízení
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **prostředky a kompatibilita** , přejít na uzel **zařízení** a vyberte zařízení. V podokně podrobností přepněte na kartu nové **kolekce** . Tato karta obsahuje seznam kolekcí, které zahrnují toto zařízení. 

> [!Note]  
> - Tato karta není momentálně k dispozici v poduzlu zařízení v uzlu **kolekce zařízení** . Například když vyberete možnost **zobrazení členů** v kolekci.
> - Tato karta se pro některé uživatele nemusí naplnit očekávaným způsobem. Úplný seznam kolekcí, do kterých zařízení patří, zobrazíte tak, že musíte mít roli zabezpečení **správce s úplnými oprávněními** . Jde o známý problém. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Přidat sloupec SMBIOS GUID do uzlů kolekce zařízení a zařízení

*(Představené ve verzi 1906)*

<!--4526580-->
V uzlech kolekce **zařízení** a **zařízení** teď můžete přidat nový sloupec pro **identifikátor SMBIOS GUID**. Tato hodnota je stejná jako vlastnost **GUID systému BIOS** třídy systémového prostředku. Je to jedinečný identifikátor hardwaru zařízení.

#### <a name="search-device-views-using-mac-address"></a>Prohledat zobrazení zařízení pomocí adresy MAC

<!--3600878-->
*(Představené ve verzi 1902)*

Adresu MAC můžete vyhledat v zobrazení zařízení konzoly Configuration Manager. Tato vlastnost je užitečná pro Správce nasazení operačního systému při řešení potíží s nasazeními založenými na technologii PXE. Když si zobrazíte seznam zařízení, přidejte do zobrazení sloupec **adresa MAC** . Pomocí vyhledávacího pole přidejte kritéria hledání **adresy MAC** .

#### <a name="view-users-for-a-device"></a>Zobrazit uživatele pro zařízení

Počínaje verzí 1806 jsou v uzlu **zařízení** k dispozici následující sloupce:  

- **Počet primárních uživatelů:** <!--1357280-->  

- **Aktuálně přihlášený uživatel** <!--1358202-->  

    > [!NOTE]  
    > Zobrazení aktuálně přihlášeného uživatele vyžaduje [zjišťování uživatelů](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) a [spřažení uživatelských zařízení](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Další informace o tom, jak zobrazit sloupec, který není výchozí, najdete v tématu [sloupce](#columns).

#### <a name="improvement-to-device-search-performance"></a>Zlepšení výkonu hledání zařízení

<!-- 3614690 -->
Počínaje verzí 1806 při hledání v kolekci zařízení nehledá klíčové slovo u všech vlastností objektu. Pokud nejste konkrétní informace o tom, co hledat, vyhledává se v následujících čtyřech vlastnostech:

- Name
- Počet primárních uživatelů:
- Aktuálně přihlášený uživatel
- Jméno posledního přihlášeného uživatele

Toto chování významně zlepšuje čas potřebný k hledání podle názvu, zejména ve velkém prostředí. Tato změna neovlivní vlastní vyhledávání podle konkrétních kritérií.


### <a name="software-library-workspace"></a>Pracovní prostor knihovny softwaru

#### <a name="order-by-program-name-in-task-sequence"></a>Seřadit podle názvu programu v pořadí úkolů
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** . Upravte pořadí úkolů a vyberte nebo přidejte krok [instalovat balíček](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) . Pokud má balíček více než jeden program, rozevírací seznam nyní Seřadí programy abecedně.

#### <a name="task-sequences-tab-in-applications-node"></a>Karta pořadí úloh v uzlu aplikace
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**, pak přejít do uzlu **aplikace** a vyberte aplikaci. V podokně podrobností přepněte na kartu nové **pořadí úkolů** . Tato karta obsahuje pořadí úloh, která odkazují na tuto aplikaci.

#### <a name="drill-through-required-updates"></a>Podrobné informace o požadovaných aktualizacích
<!--4224414-->
*(Představené ve verzi 1906)*

1. V konzole Configuration Manager klikněte na jedno z následujících míst:

   - **Softwarová knihovna**  >  **Aktualizace softwaru**  >  **Všechny aktualizace softwaru**
   - **Softwarová knihovna**  >  **Údržba**  >  Windows 10 **Všechny aktualizace Windows 10**
   - **Softwarová knihovna**  >  Správa klientů Office **365**  >  **Aktualizace Office 365**

1. Vyberte jakoukoli aktualizaci, kterou vyžaduje aspoň jedno zařízení.
1. Podívejte se na kartu **Souhrn** a v části **Statistika**Najděte výsečový graf.
1. Pokud chcete přejít k podrobnostem seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu.
1. Tato akce přejde na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci. Můžete také provést akce pro uzel, jako je například vytvoření nové kolekce ze seznamu.

> [!NOTE]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

#### <a name="maximize-the-browse-registry-window"></a>Maximalizace okna Procházet Registry

<!--3594151 includes all MMS 1902 console changes-->
*(Představené ve verzi 1902)*

1. V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .
1. Vyberte aplikaci, která má typ nasazení s metodou detekce. Například metoda zjišťování Instalační služba systému Windows.
1. V podokně podrobností přepněte na kartu **typy nasazení** .
1. Otevřete vlastnosti typu nasazení a přepněte na kartu **Metoda zjišťování** . Vyberte možnost **Přidat klauzuli**.
1. Změňte **Typ nastavení** na **registr** a kliknutím na **Procházet** otevřete okno **Procházet registr** . Nyní můžete toto okno maximalizovat.  

#### <a name="edit-a-task-sequence-by-default"></a>Upravit pořadí úkolů ve výchozím nastavení

*(Představené ve verzi 1902)*

V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** . **Upravit** je nyní výchozí akce při otevírání pořadí úkolů. Předchozí akce byla dříve nastavena na **vlastnosti**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Přejít na kolekci z nasazení aplikace

*(Představené ve verzi 1902)*

1. V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .
1. Vyberte aplikaci. V podokně podrobností přepněte na kartu **nasazení** .
1. Vyberte nasazení a pak na pásu karet na kartě nasazení zvolte možnost Nová **kolekce** . Tato akce přepne zobrazení do kolekce, která je cílem nasazení.
   - Tato akce je k dispozici také v místní nabídce na nasazení v tomto zobrazení.


### <a name="monitoring-workspace"></a>Pracovní prostor monitorování

#### <a name="correct-names-for-client-operations"></a>Správné názvy pro klientské operace
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **monitorování** vyberte **operace klientů**. Operace **Přepnutí na další bod aktualizace softwaru** je nyní správně pojmenována.

#### <a name="show-collection-name-for-scripts"></a>Zobrazit název kolekce pro skripty
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **monitorování** vyberte uzel **stav skriptu** . Kromě ID teď obsahuje i **název kolekce** .

#### <a name="remove-content-from-monitoring-status"></a>Odebrat obsah ze stavu monitorování

*(Představené ve verzi 1902)*

1. V pracovním prostoru **monitorování** rozbalte možnost **stav distribuce**a vyberte **stav obsahu**.
1. Vyberte položku v seznamu a na pásu karet zvolte možnost **Zobrazit stav** .
1. V podokně Podrobnosti o aktivech klikněte pravým tlačítkem myši na distribuční bod a vyberte novou možnost **Odebrat**. Tato akce odebere obsah z vybraného distribučního bodu.

#### <a name="copy-details-in-monitoring-views"></a>Kopírovat podrobnosti v zobrazeních monitorování

*(Představené ve verzi 1806)*
<!--1357856-->
Informace o kopírování najdete v podokně **Podrobnosti o aktivech** v následujících uzlech monitorování:  

- **Stav distribuce obsahu**  

- **Stav nasazení**  

![Zobrazení stavu nasazení, kopírování podrobností prostředků](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Pracovní prostor pro správu

<!--4223683-->
Počínaje verzí 1906 můžete povolit některé uzly pod uzlem **zabezpečení** , aby používaly službu pro správu. Tato změna umožňuje konzole komunikovat s poskytovatelem serveru SMS přes protokol HTTPS místo přes rozhraní WMI. Další informace najdete v tématu [nastavení služby správy](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Další kroky

[Funkce pro usnadnění přístupu](../../understand/accessibility-features.md)

[Editor pořadí úloh](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
