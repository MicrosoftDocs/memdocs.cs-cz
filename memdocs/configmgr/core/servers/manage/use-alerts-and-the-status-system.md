---
title: Výstrahy a stavový systém
titleSuffix: Configuration Manager
description: Nakonfigurujte výstrahy a používejte stavový systém, abyste měli nadále informace o stavu nasazení Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720713"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Použití výstrah a stavového systému pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nakonfigurujte výstrahy a pomocí integrovaného stavového systému Udržujte informace o stavu nasazení Configuration Manager.  


##  <a name="status-system"></a><a name="bkmk_Status"></a>Stavový systém  
 Všechny hlavní komponenty lokality generují stavové zprávy, které poskytují informace o operacích v lokalitě a hierarchii.    Díky těmto informacím si můžete udržovat přehled o stavu různých procesů v lokalitě. Systém výstrah můžete vyladit tak, aby ignoroval hlášení známých potíží a zároveň včas upozorňoval na jiné problémy, kterým byste měli věnovat pozornost.  

 Ve výchozím nastavení funguje stavový systém Configuration Manager bez konfigurace pomocí nastavení, která jsou vhodná pro většinu prostředí. Nicméně lze nakonfigurovat následující položky:  

-   **Shrnutí stavu:** Úpravou shrnutí stavu v jednotlivých lokalitách můžete určit četnost stavových zpráv, které vyvolávají změny indikátorů stavu. To se týká těchto čtyř shrnutí stavu:  

    -   Shrnutí nasazení aplikace  

    -   Shrnutí statistiky aplikace  

    -   Shrnutí stavu součástí  

    -   Shrnutí stavu serveru  

-   **Pravidla filtru zpráv:** U jednotlivých lokalit můžete vytvořit nová pravidla filtru zpráv, upravit prioritu pravidel, zakázat nebo povolit pravidla a odstranit nepoužívaná pravidla.  

    > [!NOTE]  
    >  Pravidla filtru zpráv nepodporují použití proměnných prostředí ke spuštění externích příkazů.  

-   **Vytváření stavových zpráv:** Můžete nakonfigurovat vytváření sestav serveru i klienta, abyste mohli upravit způsob hlášení stavových zpráv do stavového systému Configuration Manager a určit, kam se mají odesílat zprávy o stavu.  

    > [!WARNING]  
    >  Vzhledem k tomu, že výchozí nastavení hlášení jsou vhodná pro většinu prostředí, při jejich změně postupujte opatrně. Když zvýšíte úroveň vytváření stavových zpráv tím, že zvolíte, že budete hlásit všechny podrobnosti o stavu, můžete zvýšit množství zpracovávaných stavových zpráv, což zvyšuje zatížení Configuration Manager lokality. Pokud úroveň hlášení stavu snížíte, můžete tím omezit užitečnost shrnutí stavu.  

Stavový systém uchovává samostatné konfigurace pro jednotlivé lokality, takže musíte každou lokalitu upravit zvlášť.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Postupy konfigurace stavového systému  

##### <a name="to-configure-status-summarizers"></a>Postup při konfiguraci shrnutí stavu  

1.  V konzole Configuration Manager přejděte na **Správa** > **Konfigurace** >lokality**lokality**a pak vyberte lokalitu, pro kterou chcete konfigurovat stavový systém.  

2.  Na kartě **Domů** ve skupině **Nastavení** klikněte na položku **Shrnutí stavu**.  

3.  V dialogovém okně **Shrnutí stavu** vyberte shrnutí stavu, které chcete konfigurovat, a kliknutím na tlačítko **Upravit** otevřete vlastnosti tohoto shrnutí. Pokud upravujete Shrnutí nasazení aplikace nebo Shrnutí statistiky aplikace, pokračujte krokem 5. Pokud upravujete Shrnutí stavu součásti, přejděte ke kroku 6. Pokud upravujete Shrnutí stavu serveru, přejděte ke kroku 7.  

4.  Po otevření stránky vlastností buďto pro Shrnutí nasazení aplikace nebo pro Shrnutí statistiky aplikace použijte následující postup:  

    1.  Na kartě **Obecné** stránky vlastností shrnutí proveďte konfiguraci intervalů sumarizace a následným kliknutím na tlačítko **OK** stránku vlastností zavřete.  

    2.  Kliknutím na tlačítko **OK** zavřete dialogové okno **Shrnutí stavu** a dokončíte tuto proceduru.  

5.  Po otevření stránek vlastností Shrnutí stavu součásti použijte následující postup:  

    1.  Na kartě **Obecné** stránky vlastností Shrnutí proveďte konfiguraci hodnot replikace a prahového období.  

    2.  Na kartě **Prahové hodnoty** vyberte **Typ zprávy** , který chcete konfigurovat, a poté v seznamu **Prahové hodnoty** klikněte na název součásti.  

    3.  V dialogovém okně **Vlastnosti prahové hodnoty stavu** upravte hodnotu upozornění a kritickou prahovou hodnotu a poté klikněte na tlačítko **OK**.  

    4.  Opakujte kroky 6.b a 6.c podle potřeby a po skončení zavřete vlastnosti shrnutí kliknutím na tlačítko **OK** .  

    5.  Kliknutím na tlačítko **OK** zavřete dialogové okno **Shrnutí stavu** a dokončíte tuto proceduru.  

6.  Po otevření stránek vlastností Shrnutí stavu serveru použijte následující postup:  

    1.  Na kartě **Obecné** stránky vlastností Shrnutí proveďte konfiguraci hodnot replikace a plánu.  

    2.  Na kartě **Prahové hodnoty** nastavte **Výchozí prahové hodnoty** , které určí výchozí prahové hodnoty pro zobrazení kritického stavu a stavu upozornění.  

    3.  Chcete-li upravit hodnoty pro určité **Objekty úložiště**, vyberte objekt v seznamu **Specifické prahové hodnoty** a poté klikněte na tlačítko **Vlastnosti** , abyste získali přístup k upozorněním a kritickým prahovým hodnotám objektů úložiště a mohli je upravit. Kliknutím na tlačítko **OK** zavřete vlastnosti objektů úložiště.  

    4.  Pokud chcete vytvořit nový objekt úložiště, klikněte na tlačítko **Vytvořit objekt** a zadejte hodnoty objektu úložiště. Kliknutím na tlačítko **OK** zavřete vlastnosti objektu.  

    5.  Jestliže chcete objekt úložiště odstranit, vyberte objekt a poté klikněte na tlačítko **Odstranit** .  

    6.  Opakujte kroky 7. b až 7. e podle potřeby. Po skončení zavřete vlastnosti shrnutí kliknutím na tlačítko **OK** .  

    7.  Kliknutím na tlačítko **OK** zavřete dialogové okno **Shrnutí stavu** a dokončíte tuto proceduru.  

##### <a name="to-create-a-status-filter-rule"></a>Vytvoření pravidla filtru zpráv  

1.  V konzole Configuration Manager přejděte na **Správa** > **Konfigurace** >lokality**lokality**a pak vyberte lokalitu, u které chcete konfigurovat stavový systém.  

2.  Na kartě **Domů** ve skupině **Nastavení** klikněte na položku **Pravidla filtru zpráv**. Otevře se dialogové okno **Pravidla filtru zpráv** .  

3.  Klikněte na **Vytvořit**.  

4.  V nástroji **Průvodce vytvořením pravidla filtru zpráv**na stránce **Obecné** zadejte název nového pravidla filtru zpráv a kritéria přiřazování zpráv pro toto pravidlo a poté klikněte na tlačítko **Další**.  

5.  Na stránce **Akce** určete akce, jež mají být provedeny, když bude stavová zpráva odpovídat tomuto pravidlu filtru, a poté klikněte na tlačítko **Další**.  

6.  Na stránce **Souhrn** zkontrolujte podrobnosti nového pravidla a poté dokončete průvodce.  

    > [!NOTE]  
    >  Configuration Manager vyžaduje pouze, aby nové pravidlo filtru zpráv mělo název. Bude-li pravidlo vytvořeno, ale nebudou zadána žádná kritéria zpracování stavových zpráv, nebude mít pravidlo filtru zpráv žádný účinek. Díky tomuto chování lze vytvořit a uspořádat pravidla před konfigurací kritérií filtrů zpráv u jednotlivých pravidel.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Úprava nebo odstranění pravidla filtru zpráv  

1.  V konzole Configuration Manager přejděte na **Správa** > **Konfigurace** >lokality**lokality**a pak vyberte lokalitu, u které chcete konfigurovat stavový systém.  

2.  Na kartě **Domů** ve skupině **Nastavení** klikněte na položku **Pravidla filtru zpráv**.  

3.  V dialogovém okně **Pravidla filtru zpráv** vyberte pravidlo, které chcete upravit, a proveďte jednu z následujících akcí:  

    -   Kliknutím na možnost **Zvýšit prioritu** nebo **Snížit prioritu** změňte pořadí zpracování pravidla filtru zpráv. Potom zvolte další akci, nebo přejděte ke kroku 8 tohoto postupu a dokončete tuto úlohu.  

    -   Kliknutím na tlačítko **Zakázat** nebo **Povolit** změňte stav pravidla. Po provedení změny stavu pravidla zvolte další akci, nebo přejděte ke kroku 8 tohoto postupu a dokončete tuto úlohu.  

    -   Chcete-li pravidlo filtru stavu z této lokality odstranit, klikněte na tlačítko **Odstranit** a poté kliknutím na tlačítko **Ano** tuto akci potvrďte. Po odstranění pravidla zvolte další akci, nebo přejděte ke kroku 8 tohoto postupu a dokončete tuto úlohu.  

    -   Pokud chcete změnit kritéria pravidla stavových zpráv, klikněte na tlačítko **Upravit** a přejděte ke kroku 5 tohoto postupu.  

4.  Na záložce **Obecné** v dialogovém okně vlastností pravidla filtru zpráv upravte pravidlo a kritéria přiřazování zpráv.  

5.  Na kartě **Akce** upravte akce, jež mají být provedeny, když bude stavová zpráva odpovídat tomuto pravidlu filtru.  

6.  Klikněte na tlačítko **OK** a uložte změny.  

7.  Kliknutím na tlačítko **OK** zavřete dialogové okno **Pravidla filtru zpráv** .  

##### <a name="to-configure-status-reporting"></a>Postup při konfiguraci hlášení stavu  

1.  V konzole Configuration Manager přejděte na **Správa** > **Konfigurace** > lokality**lokality**a pak vyberte lokalitu, u které chcete konfigurovat stavový systém.  

2.  Na kartě **Domů** ve skupině **Nastavení** klikněte na položku **Konfigurovat součásti webu**a zvolte možnost **Vytváření stavových zpráv**.  

3.  V dialogovém okně **Vlastnosti komponenty vytváření stavových zpráv** zadejte stavové zprávy komponenty serveru a klienta, jež chcete hlásit nebo protokolovat:  

    1.  Nakonfigurujte **sestavu** pro posílání stavových zpráv do systému Configuration Manager stavové zprávy.  

    2.  Jestliže nakonfigurujete možnost **Protokol** , zaznamená se typ a závažnost stavových zpráv do protokolu událostí systému Windows.  

4.  Klikněte na tlačítko **OK**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a>Monitorování stavového systému Configuration Manager  
 **Stav systému** v Configuration Manager poskytuje přehled o obecných operacích lokalit a operací webového serveru ve vaší hierarchii. Může odhalit provozní problémy serverů nebo součástí systému lokality a můžete použít stav systému ke kontrole konkrétních podrobností pro různé operace Configuration Manager. Stav systému můžete monitorovat z uzlu **stav systému** v pracovním prostoru **monitorování** v konzole Configuration Manager.  

 Většina Configuration Manager role systému lokality a součásti generují stavové zprávy. Údaje stavových zpráv jsou protokolovány v provozních protokolech jednotlivých součástí, ale jsou také odeslány do databáze lokality, kde jsou sumarizovány a prezentovány v celkovém souhrnu stavů každé součásti nebo systému lokality. Tyto souhrny stavových zpráv poskytují podrobné informace o pravidelných operacích a o upozorněních a chybách. Můžete nakonfigurovat prahové hodnoty, při kterých se aktivují upozornění nebo chyby, a naladit systém tak, aby informace souhrnu ignorovaly známé problémy, které nejsou pro vás důležité a aby věnovaly pozornost aktuálním problémům na serverech nebo operacím součástí, které chcete prozkoumat.  

 Stav systému je replikován do jiných lokalit v hierarchii jako data lokalit, nikoli jako globální data. To znamená, že můžete zobrazit pouze stav lokality, ke které se připojuje konzola Configuration Manager, a všechny podřízené lokality pod touto lokalitou. Proto zvažte připojení konzoly Configuration Manager k lokalitě nejvyšší úrovně ve vaší hierarchii při zobrazení stavu systému.  

 Následující tabulku použijte k určení různých zobrazení stavu systému a kdy které zobrazení použít.  

|Node|Další informace|  
|----------|----------------------|  
|Stav lokality|Tento uzel použijte k zobrazení souhrnu stavu každého systému lokality za účelem kontroly dobrého stavu každého serveru systému lokality. Dobrý stav systému lokality je určen prahovými hodnotami, které nakonfigurujete pro každou lokalitu v nástroji **Sumarizovatel stavů systému lokality**.<br /><br /> Můžete zobrazit stavové zprávy pro každý systém lokality, můžete nastavit prahové hodnoty pro stavové zprávy a můžete spravovat činnost součástí systémů lokality pomocí nástroje **Configuration Manager Service Manager**.|  
|Stav součásti|Tento uzel použijte k zobrazení souhrnu stavu každé součásti Configuration Manager pro kontrolu provozního stavu součásti. Dobrý stav součásti je určen prahovými hodnotami, které nakonfigurujete pro každou lokalitu v nástroji **Sumarizovatel stavů součásti**.<br /><br /> Můžete zobrazit stavové zprávy pro každé součásti, můžete nastavit prahové hodnoty pro stavové zprávy a můžete spravovat činnost součástí pomocí nástroje **Configuration Manager Service Manager**.|  
|Konfliktní záznamy|Tento uzel použijte k zobrazení stavových zpráv o klientech, kteří mohou mít konfliktní záznamy.<br /><br /> Configuration Manager používá ID hardwaru k pokusu o identifikaci klientů, kteří mohou být duplicitní a upozorňuje vás na konfliktní záznamy. Například pokud je třeba přeinstalovat počítač, ID hardwaru bude stejné, ale identifikátor GUID, který Configuration Manager používá, může být změněn.|  
|Dotazy na stavové zprávy|Tento uzel použijte k dotazování na stavové zprávy konkrétních událostí a souvisejících detailů. Dotazy na stavové zprávy můžete použít k vyhledání stavových zpráv týkajících se konkrétních událostí.<br /><br /> Dotazy na stavové zprávy můžete často použít k identifikaci, kdy byla upravena konkrétní součást, operace nebo objekt Configuration Manager, a účet, který byl použit k provedení úprav. Například můžete spuštěním integrovaného dotazu na **Kolekce vytvořené, upravené nebo odstraněné** identifikovat, kdy byla konkrétní kolekce vytvořena a kdy byl uživatelský účet použit k vytvoření této kolekce.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Správa stavu lokality a stavu komponenty  
 Pro správu stavu lokality a stavu součásti použijte následující informace:  

-   Konfigurování prahových hodnot stavového systému naleznete v tématu [Postupy konfigurace stavového systému](#bkmk_configstatus).  

-   Chcete-li spravovat jednotlivé komponenty v Configuration Manager, použijte **Service Manager Configuration Manager**.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a>Zobrazit stavové zprávy  
 Stavové zprávy můžete zobrazit pro jednotlivé servery a součásti systému lokality.  

 Chcete-li zobrazit stavové zprávy v konzole Configuration Manager, vyberte konkrétní server nebo součást systému lokality a pak klikněte na tlačítko **Zobrazit zprávy**. Když zobrazujete zprávy, můžete vybrat zobrazení konkrétních typů zpráv nebo zprávy v určené době a dále můžete filtrovat výsledky podle údajů stavových zpráv.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a>Generoval  
 Výstrahy Configuration Manager jsou generovány pomocí některých operací, když dojde k určité podmínce.  

- Obvykle se výstrahy vytváří, když se vyskytne chyba, kterou musíte řešit.  

- Výstrahy se můžou generovat proto, aby vás upozornily na výskyt určitého stavu a vy mohli situaci dál monitorovat.  

- Některé výstrahy můžete nakonfigurovat, jako třeba výstrahy funkce Endpoint Protection a stavu klienta, kdežto jiné se konfigurují automaticky.  

- Můžete nakonfigurovat odběry výstrah a odesílat podrobné informace e-mailem. Tím se zvýší informovanost o klíčových problémech.  

  V následující tabulce najdete informace o konfiguraci výstrah a odběrů výstrah v Configuration Manager:  


|Akce|Další informace|  
|------------|----------------------|  
|Konfigurace výstrah Endpoint Protection pro kolekci|Přečtěte si téma **Konfigurace výstrah pro Endpoint Protection v Configuration Manager** při [konfiguraci Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Konfigurace výstrah stavu klienta pro kolekci|Viz [Postup konfigurace stavu klienta](../../../core/clients/deploy/configure-client-status.md).|  
|Správa výstrah Configuration Manager|Další informace najdete v části [úlohy správy pro výstrahy](#BKMK_Manage) v tomto tématu.|  
|Konfigurace e-mailových odběrů výstrah|Přečtěte si část [Management tasks for alerts](#BKMK_Manage) v tomto tématu.|  
|Sledování výstrah|Přečtěte si část [Monitorování výstrah](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Postup při správě obecných výstrah  

1. V konzole Configuration Manager přejděte na **monitorování** > **výstrahy**a potom vyberte úlohu správy.  

   Následující tabulka obsahuje podrobnosti o úlohách správy, které mohou před výběrem vyžadovat určité informace.  

|Úloha správy|Podrobnosti|  
    |---------------------|-------------|  
    |**Konfigurace**|Otevře dialogové okno\>**vlastnosti** * &lt;názvu výstrahy*, kde můžete upravit název, závažnost a prahovou hodnotu vybrané výstrahy. Pokud změníte Závažnost výstrahy, tato konfigurace ovlivní způsob zobrazení výstrah v konzole Configuration Manager.|  
    |**Upravit komentář**|Zadejte komentář k vybraným výstrahám. Tyto komentáře se zobrazí s výstrahou v konzole Configuration Manager.|  
    |**Odložit**|Pozastaví monitorování výstrahy až do zadaného data. Potom se stav výstrahy aktualizuje.<br /><br /> Výstrahu můžete odložit jenom v případě, že je povolená.|  
    |**Vytvoření odběru**|Otevře se dialog **Nový odběr** , ve kterém můžete vytvořit e-mailový odběr vybrané výstrahy.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Postup při konfiguraci výstrah týkajících se stavu klienta pro kolekci  

1.  V konzole Configuration Manager klikněte na **prostředky a kompatibilita** >   **kolekce zařízení**.  

2.  V seznamu **Kolekce zařízení** vyberte kolekci, pro kterou chcete nakonfigurovat výstrahy, a poté na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

    > [!NOTE]  
    >  Výstrahy nelze nakonfigurovat pro kolekce uživatelů.  

3.  Na kartě **výstrahy** v dialogovém okně\>**vlastnosti** * &lt;názvu kolekce*klikněte na tlačítko **Přidat**.  

    > [!NOTE]  
    >  Karta **Výstrahy** je viditelná jen v případě, že role zabezpečení, k níž jste přidruženi, má oprávnění pro výstrahy.  

4.  V dialogovém okně **Přidat nové výstrahy kolekce** vyberte výstrahy, jež mají být vygenerovány, když prahové hodnoty stavu klienta klesnou pod zadanou hodnotu, a poté klikněte na tlačítko **OK**.  

5.  V seznamu **Podmínky** na kartě **Výstrahy** vyberte jednotlivé výstrahy stavu klienta a zadejte následující informace.  

    -   **Název výstrahy** – přijměte výchozí název nebo zadejte nový název výstrahy.  

    -   **Závažnost výstrahy** – v rozevíracím seznamu vyberte úroveň výstrahy, která se zobrazí v konzole Configuration Manager.  

    -   **Vyvolat výstrahu** – zadejte procento prahové hodnoty pro výstrahu.  

6.  Kliknutím na tlačítko **OK** zavřete dialogové okno**vlastnosti** * &lt;názvu*\>kolekce.  

##### <a name="to-configure-email-notification-for-alerts"></a>Postup při konfiguraci e-mailových oznámení o výstrahách  

1.  V konzole Configuration Manager přejděte na **monitorování** > **Alerts** > **odběry**výstrahy.  

2.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na možnost **Konfigurovat e-mailová oznámení**.  

3.  V dialogu **Vlastnosti komponenty oznamování e-mailů** zadejte tyto informace:  

    -   **Povolit e-mailové oznámení pro výstrahy**: zaškrtněte toto políčko, pokud chcete Configuration Manager povolit použití serveru SMTP k odesílání e-mailových upozornění.  

    -   **Plně kvalifikovaný název domény nebo adresa IP serveru SMTP pro odeslání výstrah emailů**: Zadejte plně kvalifikovaný název domény (FQDN) nebo IP adresu a port SMTP pro e-mailový server, který chcete pro tyto výstrahy použít.  

    -   **Účet pro připojení k serveru SMTP**: Zadejte metodu ověřování pro Configuration Manager, která se má použít pro připojení e-mailového serveru.  

    -   **Adresa odesílatele pro e-mailové výstrahy**: Zadejte e-mailovou adresu, ze které se mají odesílat e-mailové výstrahy.  

    -   **Otestovat server SMTP**: Odešle zkušební e-mail na e-mailovou adresu zadanou v poli **Adresa odesílatele pro e-mailové výstrahy**.  

4.  Kliknutím na **OK** uložte nastavení a zavřete dialog **Vlastnosti komponenty oznamování e-mailů** .  

##### <a name="to-subscribe-to-email-alerts"></a>Postup nastavení odběru e-mailových výstrah  

1.  V konzole Configuration Manager přejděte na **monitorování** > **výstrah**.  

2.  Vyberte výstrahu a potom na kartě **Domů** ve skupině **Odběr** klikněte na **Vytvořit odběr**.  

3.  V dialogu **Nový odběr** zadejte tyto informace:  

    -   **Název**: Zadejte název, který bude sloužit k identifikaci e-mailového odběru. Může mít délku až 255 znaků.  

    -   **E-mailová adresa**: Zadejte e-mailové adresy, na které chcete výstrahu odesílat. Víc e-mailových adres můžete oddělit středníkem.  

    -   **Jazyk e-mailů**: V seznamu vyberte jazyk e-mailů.  

4.  Kliknutím na **OK** zavřete dialog **Nový odběr** a vytvořte e-mailový odběr.  

    > [!NOTE]  
    >  Odběry můžete odstranit a upravit v pracovním prostoru **Sledování** . Stačí rozbalit uzel **Výstrahy** a potom kliknout na uzel **Odběry** .  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a>Monitorování výstrah  
 Výstrahy můžete zobrazit v uzlu **Výstrahy** v pracovním prostoru **Monitorování** . Výstrahy mají jeden z následujících stavů:  

- **Neaktivní**: Podmínka výstrahy nebyla splněná.  

- **Aktivní**: Je splněná podmínka výstrahy.  

- **Zrušeno**: Podmínka aktivní výstrahy už není splněná. Tento stav udává, že podmínka, která způsobila výstrahu je nyní vyřešena.  

- **Odloženo**: administrativní uživatel nakonfiguroval Configuration Manager k vyhodnocení stavu výstrahy později.  

- **Zakázáno**: Správce výstrahu zakázal. Když je výstraha v tomto stavu, Configuration Manager neaktualizuje výstrahu, i když se stav výstrahy změní.  

  Když Configuration Manager vygeneruje výstrahu, můžete provést jednu z následujících akcí:  

- Vyřešit podmínku, která způsobila výstrahu, například můžete vyřešit problém sítě nebo problém konfigurace, který výstrahu vytvořil. Jakmile Configuration Manager zjistí, že problém již neexistuje, stav výstrahy se změní na **Canceled (zrušit**).  

- Pokud je výstraha známým problémem, můžete ji o určitou dobu odložit. V tuto chvíli Configuration Manager aktualizuje výstrahu na její aktuální stav.  

   Výstrahu můžete odložit, pouze když je aktivní.  

- **Komentář** výstrahy můžete upravit, aby další správci viděli, že o této výstraze víte. V komentáři můžete například uvést způsob řešení příčiny výstrahy, poskytnout informace o aktuálním stavu příčiny výstrahy nebo vysvětlit, proč jste výstrahu odložili.  
