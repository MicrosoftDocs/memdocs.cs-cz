---
title: Konzola nástroje Configuration Manager
titleSuffix: Configuration Manager
description: Přečtěte si informace o navigaci prostřednictvím konzoly Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126490"
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

|Možnost|Popis|  
|------------|-----------------|  
|`/sms:debugview=1`|Nástroj DebugView je součástí všech ResultViews, které určují zobrazení. Nástroj DebugView zobrazí nezpracované vlastnosti (názvy a hodnoty).|  
|`/sms:NamespaceView=1`|Zobrazuje zobrazení oboru názvů v konzole nástroje.|  
|`/sms:ResetSettings`|Konzola ignoruje uživatelem uložené připojení a stavy zobrazení. Velikost okna není resetována.|  
|`/sms:IgnoreExtensions`|Zakáže všechna Configuration Manager rozšíření.|  
|`/sms:NoRestore`|Konzola ignoruje předchozí trvalý navigační uzel.|  


## <a name="next-steps"></a>Další kroky

- [Oznámení konzoly](admin-console-notifications.md)
- [Tipy pro konzolu](admin-console-tips.md)
- [Funkce pro usnadnění přístupu](../../understand/accessibility-features.md)
- [Editor pořadí úloh](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
