---
title: Skupiny Orchestration
titleSuffix: Configuration Manager
description: Vytvořte skupiny Orchestration a nasaďte do nich aktualizace.
ms.date: 04/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9a307df23900abb985535b2ab59a5ff172cafb7
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254907"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Skupiny orchestrace v Configuration Manager
<!--3098816-->
*Platí pro: Configuration Manager (Current Branch)*

Od verze Configuration Manager 2002 můžete vytvořit skupiny Orchestration. Vytvořte skupinu Orchestration, která vám umožní lépe řídit nasazení softwarových aktualizací do zařízení. Mnoho správců serveru musí pečlivě spravovat aktualizace pro konkrétní úlohy a automatizovat chování mezi.

Skupina Orchestration poskytuje flexibilitu při aktualizaci zařízení na základě procenta, konkrétního čísla nebo explicitního pořadí. Můžete také spustit skript prostředí PowerShell před a po spuštění nasazení aktualizace na zařízeních.

Členy skupiny orchestration může být jakýkoli Configuration Manager klient, nikoli jenom Server. Pravidla skupiny Orchestration se vztahují na zařízení pro všechna nasazení aktualizací softwaru na všechny kolekce, které obsahují člena skupiny Orchestration. Stále platí jiné chování nasazení. Například časová období údržby a plány nasazení.

> [!NOTE]
> V této verzi Configuration Manager skupiny Orchestration jsou funkcí předběžné verze. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../core/servers/manage/pre-release-features.md).  
>
> Funkce **skupin Orchestration** je vývojem funkce [skupiny serveru](service-a-server-group.md) . Skupina Orchestration je objekt v Configuration Manager.

## <a name="orchestration-group-usage-example"></a>Příklad použití skupiny Orchestration

- Jako správce aktualizací softwaru můžete spravovat všechny aktualizace vaší organizace.
- Máte jednu velkou kolekci pro všechny servery a jednu velkou kolekci pro všechny klienty. Všechny aktualizace se nasazují do těchto kolekcí.
- Správci SQL chtějí řídit veškerý software nainstalovaný na serverech SQL. Chtějí opravit pět serverů v určitém pořadí. Jejich aktuálním procesem je ruční zastavení určitých služeb před instalací aktualizací a následné restartování služeb.
- Vytvoříte skupinu Orchestration a přidáte všechny pět serverů SQL. Pomocí skriptů PowerShellu poskytovaných správci SQL můžete také přidat předem a post-Script.
- Během příštího aktualizačního cyklu vytvoříte a nasadíte aktualizace softwaru jako normální pro velkou kolekci serverů. Správci SQL spouštějí nasazení a skupina Orchestration automatizuje pořadí a služby.

## <a name="prerequisites"></a>Požadavky

### <a name="site-server-and-permission-prerequisites"></a>Požadavky na server lokality a oprávnění
- Pokud chcete zobrazit všechny skupiny Orchestrace a aktualizace pro tyto skupiny, musí být váš účet **úplný správce**.
   - Správa na základě rolí pro skupiny Orchestration aktuálně není dostupná.
- Povolte funkci **skupiny Orchestration** . Další informace najdete v tématu [Povolení volitelných funkcí](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - Pokud povolíte **skupiny Orchestration**, lokalita zakáže funkci **skupiny serverů** . Toto chování zabrání jakémukoli konfliktu mezi těmito dvěma funkcemi.

### <a name="client-prerequisites"></a>Požadavky klienta

- Upgradujte cílová zařízení na nejnovější verzi klienta Configuration Manager.
- Členové skupiny Orchestration by měli mít přiřazenou stejnou lokalitu.
- Zařízení nemůžou být ve více než jedné skupině Orchestration.
   - Zařízení, která jsou už ve skupině Orchestration, nebudou k dispozici pro výběr při přidávání nových členů.


## <a name="limitations"></a>Omezení

- Můžete mít až 1000 členů skupiny Orchestration.
- Skupiny Orchestration nefungují v režimu interoperability. Další informace najdete v tématu [vzájemná funkční spolupráce mezi různými verzemi Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Pokud se aktualizace iniciují uživateli z centra softwaru, orchestrace se vynechá. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Skupiny serverů se automaticky aktualizují na skupiny orchestrace.

Funkce **skupin Orchestration** je vývojem funkce [skupiny serveru](service-a-server-group.md) . Když nainstalujete Configuration Manager verze 2002 nebo novější a máte povolené skupiny serverů, skupiny serverů se automaticky přesunou do skupin Orchestration.

## <a name="create-an-orchestration-group"></a>Vytvořit skupinu Orchestration

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **Skupina Orchestration** .

1. Na pásu karet vyberte **vytvořit skupinu Orchestration** a otevřete tak **Průvodce vytvořením skupiny Orchestration**.

1. Na stránce **Obecné** dejte skupině Orchestration **název** a volitelně také **Popis**. Zadejte hodnoty pro následující položky:
   - **Časový limit skupiny Orchestration (v minutách)**: časový limit pro všechny členy skupiny, aby se instalace aktualizace dokončila.
   - **Časový limit člena skupiny Orchestration (v minutách)**: časový limit pro jedno zařízení ve skupině, aby se instalace aktualizace dokončila.

1. Na stránce **Výběr členů** nejprve zadejte **kód lokality**. Pak vyberte **Přidat** a přidejte prostředky zařízení jako členy této skupiny Orchestration. **Vyhledejte** zařízení podle názvu a pak je **přidejte** . Hledání můžete také filtrovat do jedné kolekce pomocí **hledání v kolekci**.  Po dokončení přidávání zařízení do seznamu vybraných prostředků vyberte **OK** .
   - Při výběru prostředků pro skupinu se zobrazí pouze platní klienti. Pro ověření kódu lokality jsou provedeny kontroly, že je klient nainstalován a že prostředky nejsou duplikovány.

1. Na stránce **Výběr pravidla** vyberte jednu z následujících možností:

   - **Nechte aktualizovat procento počítačů současně**a pak vybrat nebo zadat číslo pro toto procento. Toto nastavení použijte, pokud chcete, aby byla umožněna budoucí flexibilita velikosti skupiny orchestrace. Například skupina orchestrace obsahuje zařízení 50 a tuto hodnotu nastavíte na 10. Během nasazení aktualizace softwaru Configuration Manager umožňuje souběžné nasazení spustit pět zařízení. Pokud později zvětšíte velikost skupiny Orchestration na zařízení 100, po jednom se aktualizuje 10 zařízení najednou.

   - **Umožněte, aby se počet počítačů aktualizoval současně**, a pak vyberte nebo zadejte číslo tohoto konkrétního počtu. Toto nastavení použijte, pokud chcete vždycky omezit na určitý počet zařízení bez ohledu na celkovou velikost skupiny Orchestration.

   - **Zadejte sekvenci údržby**a pak seřaďte vybrané prostředky ve správném pořadí. Pomocí tohoto nastavení můžete explicitně definovat pořadí, ve kterém zařízení spouštějí nasazení aktualizace softwaru.

1. Na stránce **předzálohovací skript** zadejte powershellový skript, který se spustí na každém zařízení *před* spuštěním nasazení. Skript by měl vrátit hodnotu `0` pro úspěch nebo `3010` pro úspěch s restartem.

1. Na stránce **pozálohovací skript** zadejte powershellový skript, který se spustí na každém zařízení *po* spuštění nasazení. Chování je jinak stejné jako u skriptu.

1. Dokončete průvodce.

> [!WARNING]
> Před jejich použitím pro skupiny orchestrace zajistěte, aby byly testovány předběžné skripty a následné skripty. Předzálohovací a pozálohovací skripty nekončí časovým limitem a budou spuštěny, dokud nedosáhnete časového limitu členů skupiny Orchestration.

## <a name="view-orchestration-groups-and-members"></a>Zobrazení skupin Orchestration a členů

V pracovním prostoru **prostředky a kompatibilita** vyberte uzel **Skupina Orchestration** . Chcete-li zobrazit členy, vyberte skupinu Orchestration a na pásu karet vyberte možnost **Zobrazit členy** . Další informace o dostupných sloupcích pro uzly najdete v tématu věnovaném [monitorování skupin a členů orchestrace](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Upravit nebo odstranit skupinu Orchestration

Pokud chcete skupinu Orchestration odstranit, vyberte ji a pak na pásu karet nebo v místní nabídce klikněte na **Odstranit** . Chcete-li upravit skupinu Orchestration, vyberte ji a pak klikněte na tlačítko **vlastnosti** na pásu karet nebo v místní nabídce klikněte na tlačítko. Změňte nastavení z následujících karet:

   - **Obecné**: 
      - **Name**(název): název skupiny Orchestration
      - **Popis**: Popis skupiny Orchestration (volitelné)
      - **Časový limit skupiny Orchestration (v minutách)**: časový limit pro všechny členy skupiny, aby se instalace aktualizace dokončila.
      - **Časový limit člena skupiny Orchestration (v minutách)**: časový limit pro jedno zařízení ve skupině, aby se instalace aktualizace dokončila.

  - **Výběr členů**:
     - **Kód lokality**: kód lokality pro skupinu Orchestration.
     - **Členové**: kliknutím na tlačítko **Přidat** vyberte další zařízení pro skupinu Orchestration. Kliknutím na tlačítko **Odebrat** odeberete vybrané zařízení.

   - **Výběr pravidel**:
      - **Nechte aktualizovat procento počítačů současně**a pak vybrat nebo zadat číslo pro toto procento. Toto nastavení použijte, pokud chcete, aby byla umožněna budoucí flexibilita velikosti skupiny orchestrace. Například skupina orchestrace obsahuje zařízení 50 a tuto hodnotu nastavíte na 10. Během nasazení aktualizace softwaru Configuration Manager umožňuje souběžné nasazení spustit pět zařízení. Pokud později zvětšíte velikost skupiny Orchestration na zařízení 100, po jednom se aktualizuje 10 zařízení najednou.
      - **Umožněte, aby se počet počítačů aktualizoval současně**, a pak vyberte nebo zadejte číslo tohoto konkrétního počtu. Toto nastavení použijte, pokud chcete vždycky omezit na určitý počet zařízení bez ohledu na celkovou velikost skupiny Orchestration.
      - **Zadejte sekvenci údržby**: seřadit vybrané prostředky do správného pořadí. Pomocí tohoto nastavení můžete explicitně definovat pořadí, ve kterém zařízení spouštějí nasazení aktualizace softwaru.

   - **Předzálohovací skript**: 
       - *Před* spuštěním nasazení zadejte powershellový skript, který se spustí na každém zařízení. Skript by měl vrátit hodnotu `0` pro úspěch nebo `3010` pro úspěch s restartem.
       
   - **Po skriptu**:
      - *Po* spuštění nasazení zadejte powershellový skript, který se spustí na každém zařízení. Skript by měl vrátit hodnotu `0` pro úspěch nebo `3010` pro úspěch s restartem.
   > [!WARNING]
   > Před jejich použitím pro skupiny orchestrace zajistěte, aby byly testovány předběžné skripty a následné skripty. Předzálohovací a pozálohovací skripty nekončí časovým limitem a budou spuštěny, dokud nedosáhnete časového limitu členů skupiny Orchestration.


## <a name="start-orchestration"></a>Spustit orchestraci

1. [Nasaďte aktualizace softwaru](deploy-software-updates.md) do kolekce, která obsahuje členy skupiny Orchestration.

1. Orchestrace se spustí, když se kterýkoli klient ve skupině pokusí nainstalovat jakoukoli aktualizaci softwaru v konečném termínu nebo během časového intervalu pro správu a údržbu. Spustí se pro celou skupinu a zajistí, že se zařízení aktualizují podle pravidel skupiny Orchestration.
1. Orchestraci můžete spustit ručně tak, že ji vyberete v uzlu **Skupina Orchestration** a pak na pásu karet kliknete pravým tlačítkem myši na možnost **Spustit Orchestration** .
1. Pokud je skupina Orchestration ve stavu *selhání* :
   1. Určete, proč orchestrace selhala, a vyřešte případné problémy.
   1. [Obnovte stav orchestrace pro členy skupiny](#bkmk_reset).
   1. V uzlu **Skupina Orchestration** kliknutím na tlačítko **zahájit orchestraci** restartujte orchestraci.
   [![Spustit orchestraci](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Skupiny Orchestration se vztahují pouze na nasazení aktualizací softwaru. Nevztahují se na jiná nasazení.
> - Můžete kliknout pravým tlačítkem na člena skupiny Orchestration a vybrat **obnovit člena skupiny Orchestration**. To umožňuje znovu spustit orchestraci.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a>Monitorování skupin Orchestration

V pracovním prostoru **prostředky a kompatibilita** vyberte uzel **Skupina Orchestration** . Přidejte libovolné z následujících sloupců, abyste získali informace o skupinách:

- **Název orchestrace**: název vaší skupiny Orchestration.
- **Kód lokality**: kód lokality pro skupinu.
- **Typ orchestrace**: je jeden z následujících typů:
   - Číslo
   - Procento
   - Sequence

- **Hodnota orchestrace**: kolik členů nebo procento členů, kteří mohou najednou získat zámek. **Hodnota orchestrace** je naplněna pouze v případě, že je **typ orchestrace** buď *číslo* , nebo *procento*.  
- **Stav orchestrace**: probíhá během orchestrace. Nečinný, pokud neprobíhá.
- **Čas zahájení orchestrace**: datum a čas zahájení orchestrace.
- **Aktuální pořadové číslo**: Určuje, který člen orchestrace skupiny je aktivní. Toto číslo odpovídá **pořadovému číslu** člena.  
- **Časový limit orchestrace (v minutách)**: hodnota **časového limitu skupiny orchestrace (v minutách)** nastavená na stránce **Obecné** při vytváření skupiny nebo na kartě **Obecné** při úpravách skupiny.
- **Časový limit člena skupiny Orchestration (v minutách)**: hodnota **časového limitu člena skupiny Orchestration (v minutách)** , která se nastavuje na stránce **Obecné** při vytváření skupiny, nebo na kartě **Obecné** při úpravách skupiny.
- **ID skupiny Orchestration**: ID skupiny, ID se používá v protokolech a v databázi.
- **Jedinečné ID skupiny Orchestration**: jedinečné ID skupiny, jedinečné ID se používá v protokolech a v databázi.

## <a name="monitor-orchestration-group-members"></a>Monitorování členů skupiny Orchestration

V uzlu **Skupina Orchestration** vyberte skupinu Orchestration. Na pásu karet vyberte **Zobrazit členy**. Můžete zobrazit členy skupiny a jejich stav Orchestration. Přidejte libovolné z následujících sloupců, chcete-li získat informace o členech:

- **Název**: název zařízení člena skupiny Orchestration.
- **Aktuální stav**: poskytuje stav členského zařízení.
   - **Probíhá během** orchestrace.
   - **Čekání**: Určuje, že klient čeká na zámek pro jeho instalaci aktualizací.
   - **Nečinné** , pokud je orchestrace dokončena nebo není spuštěná.
- **Stavový kód**: můžete kliknout pravým tlačítkem na člen skupiny Orchestration a vybrat **obnovit člena skupiny Orchestration**. Tato možnost resetování umožňuje znovu spustit orchestraci. Stavy zahrnují: 
   - Období
   - Čeká se na zařízení, které čeká na zapnutí.
   - Probíhá instalace aktualizace.
   - Failed
   - Čeká na restartování
- **Čas pořízení zámku**: klient požaduje zámky na základě zásad. Jakmile klient získá zámek, aktivuje se orchestrace.  
-**Čas hlášený jako poslední stav**: čas, kdy člen naposledy ohlásil stav.
- **Pořadové číslo**: umístění klienta ve frontě pro instalaci aktualizací.
- **Kód lokality**: kód lokality pro člena.
- **Aktivita klienta**: oznamuje, zda je klient aktivní nebo neaktivní.
- **Primární uživatelé**: uživatelé, kteří jsou primární pro zařízení.
- **Typ klienta**: typ zařízení, které klient používá.
- **Aktuálně přihlášený uživatel**: aktuálně přihlášený uživatel k zařízení.
- **Og ID**: ID skupiny orchestrace, do které patří člen.
- **Og jedinečné ID**: jedinečné ID skupiny orchestrace, ke které patří daný člen.
- **ID prostředku**: ID prostředku zařízení.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a>Resetovat stav orchestrace člena skupiny

Pokud chcete znovu spustit orchestraci u člena skupiny, můžete jeho stav vymazat, jako je *dokončeno* nebo *Chyba*. Chcete-li vymazat stav, klikněte pravým tlačítkem na člena skupiny Orchestration a vyberte možnost **obnovit člena skupiny Orchestration**. Na pásu karet můžete také kliknout na **obnovit člena skupiny Orchestration** . Před resetováním stavu byste měli zjistit, proč se klient nezdařil, a opravit případné zjištěné problémy.
   [![Resetovat člena skupiny Orchestration](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Soubory protokolů

Pomocí následujících souborů protokolu na serveru lokality můžete monitorovat a řešit potíže:

### <a name="site-server"></a>Server lokality

- **Policypv. log**: ukazuje, že lokalita cílí na skupinu Orchestration na klienty.
- **SMS_OrchestrationGroup. log**: zobrazuje chování skupiny Orchestration.

### <a name="client"></a>Klient

- **MaintenanceCoordinator. log**: zobrazuje získání zámku, aktualizace instalace, předzálohovacích a pozálohovacích skriptů a proces uvolnění zámků.
- **UpdateDeployment. log**: zobrazuje proces instalace aktualizací.
- **Policyagent. log**: kontroluje, jestli je klient ve skupině Orchestration.

## <a name="next-steps"></a>Další kroky

[Nasazení aktualizací softwaru](deploy-software-updates.md)