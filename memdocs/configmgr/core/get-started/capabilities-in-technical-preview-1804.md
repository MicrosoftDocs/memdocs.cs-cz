---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Seznamte se s novými funkcemi dostupnými v Configuration Manager Technical Preview verze 1804.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b30386745244900e7f525f8f45b25a598628bf43
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078732"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1804 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1804. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Technical Preview. 

Před instalací této aktualizace si přečtěte článek [Technical Preview](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Známé problémy v této verzi Technical Preview

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a>Odkaz na nastavení pro stažení aktualizací, které nefungují
<!--514334-->
Pokud spustíte instalaci z média, úvodní stránka obsahuje odkaz s názvem **získat nejnovější Configuration Manager aktualizace**, které v této verzi nefungují. Tento odkaz slouží ke stažení požadovaných souborů pro instalaci.

#### <a name="workaround"></a>Alternativní řešení
Chcete-li stáhnout požadované soubory pro instalační program, spusťte Průvodce instalací nástroje. Na stránce stažení požadovaných součástí použijte možnost ke **stažení požadovaných souborů**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a>Bod webové služby katalogu aplikací nemůže být povolen pomocí protokolu HTTPS.
<!--512637-->
Pokud je bod služeb webu Katalog aplikací povolený pomocí protokolu HTTPS:

- Aplikace nasazené jako dostupné uživatelům se nezobrazují v centru softwaru  

- V protokolu awebsctl. log se zobrazí následující chyba:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Alternativní řešení
Překonfigurujte bod webové služby Katalog aplikací tak, aby komunikoval pomocí připojení HTTP.  




</br>

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Konfigurace vzdálené knihovny obsahu pro server lokality  
<!--1357525-->
Chcete-li uvolnit místo na pevném disku na primárním serveru lokality, přemístěte příslušnou [knihovnu obsahu](../plan-design/hierarchy/the-content-library.md) do jiného umístění úložiště. Knihovnu obsahu můžete přesunout na jinou jednotku na serveru lokality, na samostatném serveru nebo na disky odolné proti chybám v síti SAN (Storage Area Network). Doporučujeme síť SAN, protože poskytuje elastické úložiště, které se v průběhu času zvětšuje nebo zmenšuje, aby splňovalo vaše změny požadavků obsahu. 

Tato vzdálená knihovna obsahu je novou podmínkou pro [vysokou dostupnost role serveru lokality](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Tato akce přesune obsah knihovny obsahu na serveru lokality. Nemá vliv na umístění knihovny obsahu v distribučních bodech. 

### <a name="prerequisites"></a>Požadavky  
- Účet počítače serveru lokality potřebuje oprávnění **ke čtení** a **zápisu** pro síťovou cestu, do které přesouváte knihovnu obsahu. Ve vzdáleném systému nejsou nainstalovány žádné součásti. 

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager přepněte do pracovního prostoru **Správa** . Rozbalte položku **Konfigurace lokality** a vyberte možnost **lokality**. Na kartě **Souhrn** v dolní části podokna podrobností si všimněte nového sloupce pro **knihovnu obsahu**.  

2. Na pásu karet klikněte na **Spravovat knihovnu obsahu** .  

3. Vyberte **sdílenou síťovou složku** a zadejte platnou cestu k síti. Tato cesta je umístění, do kterého lokalita přesouvá knihovnu obsahu. Klikněte na tlačítko **OK**.  

4. Poznamenejte si vlastnost **stav** ve sloupci knihovna obsahu v podokně podrobností. Aktualizuje a zobrazí průběh přesunutí knihovny obsahu. V průběhu zobrazení se zobrazí procento dokončení. Pokud dojde k chybovém stavu, zobrazí se chyba. Mezi běžné chyby `access denied` patří `disk full`nebo. Po dokončení se zobrazí `OK`. Podrobnosti najdete v **protokolu Distmgr. log** . Další informace najdete v tématu [protokoly serveru lokality a serveru systému lokality](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

Pokud potřebujete přesunout knihovnu obsahu zpět na server lokality, opakujte tento postup, ale vyberte možnost **místní pro server lokality**.  

> [!Tip]  
> Chcete-li přesunout obsah na jinou jednotku na serveru lokality, použijte nástroj pro **přenos knihovny obsahu** . Další informace najdete v tématu [Configuration Manager Toolkit](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a>Odeslat názor z konzoly Configuration Manager  
<!--1357542-->

Poslat smajlíka! Configuration Manager tým teď můžete přímo informovat o svých prostředích. Zasílání názorů je snadné z konzoly Configuration Manager. Chceme slyšet váš názor: Praise, problémy a návrhy.  

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme **názor** , abychom věděli, jak pracovali.  

1. V konzole Configuration Manager klikněte na tlačítko smajlíka v pravém horním rohu nad pásem karet.  

2. V rozevíracím seznamu vyberte jednu z dostupných možností:  

   - **Poslat smajlíka**: opravdu se vám něco líbí! Pro tuto možnost zadejte podrobnosti o zpětné vazbě. Volitelně můžete zahrnout snímek obrazovky a vaši e-mailovou adresu.  

   - **Odeslání zamračení**: došlo k potížím v konzole nástroje nebo něco nefungovalo podle očekávání. Pro tuto možnost zadejte podrobnosti o potenciálním problému s produktem. Volitelně můžete zahrnout snímek obrazovky, e-mailovou adresu a diagnostická data.  

   - **Odeslání návrhu**: máte nápad, jak můžete změnit a vylepšit Configuration Manager. Tato možnost otevře náš web [UserVoice](https://configurationmanager.uservoice.com) ve webovém prohlížeči.  

Tato zpětná vazba směřuje přímo k produktu Microsoft Product Team pro Configuration Manager. I když se používá centrum Feedback pro Windows 10, doporučujeme použít mechanismus zpětné vazby v konzole.  

Následující anonymní informace jsou vždy součástí zpětné vazby pro kontext:  

- Verze a jazyk konzoly Configuration Manager  

- Verze Configuration Manager lokality  

- ID podpory, označované také jako ID hierarchie  

- Verze a jazyk operačního systému pro systém, na kterém je spuštěná konzola  

- Přesné umístění v konzole, ze které jste klikli na smajlíka  

Tato data jsou konzistentní s kolekcí naší diagnostiky a dat o využití. Další informace najdete v tématu [Diagnostika a data o využití](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Známé problémy

Pokud se pokusíte odeslat zpětnou vazbu ze zařízení, které není schopné získat přístup k Internetu, aplikace se může nečekaně zavřít. Pokud chcete poslat smajlíka nebo zamračení, ujistěte se, že je zařízení schopné získat přístup k petrol.office.microsoft.com.



## <a name="support-center"></a>Support Center
<!--1357489-->

Použijte Support Center pro řešení potíží s klientem, zobrazení protokolu v reálném čase nebo zachycení stavu Configuration Manager klientského počítače pro pozdější analýzu. Support Center je jedním z nástrojů pro konsolidaci mnoha nástrojů pro odstraňování potíží správců. Verze Preview pro nejnovější verzi nástroje Support Center s opravami chyb, vylepšeními a verzí Preview našeho nového prohlížeče protokolu je k dispozici v Technical Preview. Vyhledejte instalační program centra pro podporu na serveru lokality ve složce **CD. latest\SMSSETUP\Tools\SupportCenter** .

 > [!Tip]  
 > Starší verze dokumentace pro stávající funkce v nástroji Support Center je k dispozici na [webu TechNet](https://technet.microsoft.com/library/dn688621.aspx). V průběhu migrace do knihovny docs.microsoft.com probíhá zpracování relevantních informací.  

### <a name="new-support-center-features"></a>Nové funkce nástroje Support Center  

- Nový prohlížeč protokolů OneTrace. Funguje podobně jako CMTrace a obsahuje vylepšení, jako jsou například zobrazení s kartami a ukotvit okna.  

- Nová funkce kolekce dat shromažďuje diagnostické protokoly z místního nebo vzdáleného klienta Configuration Manager. Poskytuje diagnostiku inventáře v reálném čase (nahrazuje klienta Spy), zásady (nahrazuje zásadu Spy) a mezipaměť klienta.  



## <a name="configuration-manager-toolkit"></a>Sada Configuration Manager Toolkit
<!--1357145-->

Nástroj Configuration Manager Server a klientské nástroje jsou teď součástí Technical Preview. Najdete je ve složce **CD. latest\SMSSETUP\Tools** na serveru lokality. Není nutná žádná další instalace.

#### <a name="server-tools"></a>Nástroje serveru  

- **DP Správce úloh**: řeší úlohy distribuce obsahu do distribučních bodů  

- **Prohlížeč vyhodnocení kolekce**: zobrazení podrobností o vyhodnocení kolekce  

- **Průzkumník knihovny obsahu**: zobrazit obsah úložiště jediné instance knihovny obsahu  

- **Přenos knihovny obsahu**: přenáší knihovnu obsahu mezi jednotkami  

- **Nástroj pro vlastnictví obsahu**: změní vlastnictví osamocených balíčků. Tyto balíčky existují v lokalitě bez vlastnícího serveru lokality.  

- **Nástroj pro správu a auditování na základě rolí**: pomáhá správcům auditovat konfiguraci rolí.  

#### <a name="client-tools"></a>Nástroje klienta

- **CMTrace**: Zobrazit protokoly  

- **Nástroj pro monitorování nasazení**: řešení problémů s nasazením aplikací, aktualizací a směrného plánu  

- **Zásady Spy**: zobrazení přiřazení zásad  

- **Nástroj Power Viewer**: zobrazení stavu funkce řízení spotřeby  

- **Nástroj pro odeslání plánu**: Aktivace plánů a vyhodnocení standardních hodnot DCM  

> [!Important]  
> [Support Center](#support-center) se doporučuje pro většinu případů použití, protože obsahuje stejné nebo vylepšené funkce pro následující nástroje:  
> - Klientský Spy
> - CMTrace<sup>1</sup> 
> - Nástroj pro monitorování nasazení
> - Spy pro zásady
> - Nástroj pro odeslání plánu
> 
> <sup>1</sup> CMTrace není závislá na rozhraní .net nebo Windows Presentation Foundation (WPF), takže se pořád používá ve spouštěcích bitových kopiích Windows PE.

### <a name="known-issues"></a>Známé problémy
Některé nástroje klienta a serveru se při spuštění neočekávaně ukončí. K tomuto problému dochází z důvodu chybějícího souboru na médiu. Jako alternativní řešení zkopírujte soubor **Microsoft. Diagnostics. Tracing. EventSource. dll** z adresáře AdminConsole\bin do adresáře SMSSETUP\Tools\ClientTools a ServerTools. Tento soubor musí mít stejnou verzi, jakou používá konzola Configuration Manager. Jiné verze nemusí fungovat. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Odinstalace aplikace při odvolání schválení
<!--1357891-->

Chování se změnilo při odvolání schválení pro aplikaci. Když teď žádost o aplikaci odepřete, klient aplikace odinstaluje aplikaci ze zařízení uživatele. 

### <a name="prerequisites"></a>Požadavky
- Povolte funkci **schvalovat žádosti o aplikace pro uživatele na zařízení**.

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager nasaďte do uživatele aplikaci, která vyžaduje schválení. Na kartě **nastavení nasazení** v nasazení povolte možnost, že **Správce musí na zařízení schválit žádost o tuto aplikaci**.  

2. V klientovi Configuration Manager v centru softwaru si uživatel vyžádá schválení instalace aplikace.  

3. V konzole Configuration Manager schvalte žádost pro tohoto uživatele a nainstalujte aplikaci na zařízení. Žádosti o schválení aplikace se zobrazují v pracovním prostoru **softwarová knihovna** v části **Správa aplikací**v uzlu **žádosti o schválení** .  

4. V klientovi v centru softwaru uživatel aplikaci nainstaluje.  

5. V konzole Configuration Manager zakažte žádost uživatele o aplikaci na zařízení.  

### <a name="known-issues"></a>Známé problémy
- Jakmile uživatel aplikaci nainstaluje na klienta, aktualizujte zásady uživatele. V centru softwaru přepněte na kartu **Možnosti** , rozbalte položku **Údržba počítače** a klikněte na **zásady synchronizace**.<!--480609-->  

- Bod webové služby katalogu aplikací musí být HTTP. Další informace najdete v části [známé problémy v této verzi Technical Preview](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Vyloučení kontejnerů služby Active Directory ze zjišťování
<!--1358143-->
Chcete-li snížit počet zjištěných objektů, můžete nyní vyloučit konkrétní kontejnery ze zjišťování systému služby Active Directory. Tato funkce je výsledkem vaší [zpětné vazby](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery)ve službě UserVoice.

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace hierarchie** a vyberte možnost **metody zjišťování**. Vyberte možnost **zjišťování systému služby Active Directory** a na pásu karet klikněte na tlačítko **vlastnosti** .  

2. Klikněte na ikonu Nový a zadejte nový kontejner služby Active Directory.   

3. V dialogovém okně kontejner služby Active Directory vyhledejte nebo zadejte **cestu** do části umístění a spusťte zjišťování.  

4. V části Možnosti hledání povolte možnost **rekurzivní vyhledávání podřízených kontejnerů služby Active Directory**. Pak klikněte na **Přidat** a vyberte subkontejnery, které se mají vyloučit z tohoto zjišťování.  

5. V dialogovém okně vybrat nový kontejner vyberte podřízený kontejner, který se má vyloučit. Kliknutím na tlačítko **OK** zavřete dialogové okno vybrat nový kontejner.  

6. Kliknutím na tlačítko **OK** zavřete dialogové okno kontejner služby Active Directory.  

7. V okno Vlastnosti zjišťování systémových součástí služby Active Directory, přečtěte si cestu k adresáři služby Active Directory, ve kterém je zjišťování spuštěno. **Rekurzivní** sloupec zobrazuje **Ano**a ve sloupci nový **má vyloučení** se zobrazí také hodnota **Ano**. Kliknutím na tlačítko **OK** zavřete okno Vlastnosti zjišťování systémových souborů služby Active Directory.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Zadání viditelnosti odkazu na web katalogu aplikací v centru softwaru
<!--1358214-->

Nyní můžete určit, zda se odkaz na **otevření webu katalogu aplikací** zobrazí v uzlu **stav instalace** v centru softwaru.  

> [!Note]  
> Podpora uživatelského prostředí webu Katalog aplikací skončí s první aktualizací vydanou od 1. června 2018. Další informace najdete v tématu [odebrané a zastaralé funkce](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager v části pracovní prostor **Správa** , uzel **nastavení klienta** vytvořte vlastní zásadu nastavení klientského zařízení.  

2. Vyberte skupinu **Centrum softwaru** .  

3. V **Nastavení centra softwaru**klikněte na **přizpůsobit**.  

4. Povolte možnost **skrýt odkaz Web Application Catalog v centru softwaru**.   

Další informace o nastavení klienta najdete v tématu [Konfigurace nastavení klienta](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrování pravidel automatického nasazení podle architektury aktualizace softwaru
 <!--1322266-->
Teď můžete filtrovat pravidla automatického nasazení tak, aby se vyloučily architektury, jako je například Itanium a ARM64.

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager přepněte do pracovního prostoru **softwarová knihovna** . Rozbalte položku **aktualizace softwaru** a vyberte možnost **pravidla automatického nasazení**. Na pásu karet vyberte **vytvořit pravidlo automatického nasazení**.  

2. Vyplňte příslušné nastavení na kartě **Obecné** a na kartě **nastavení nasazení** .  

3. Na kartě **aktualizace softwaru** vyberte možnost **Architektura** a v **kritériích hledání**klikněte na **položky, které chcete najít** .  

4. Vyberte architektury, které chcete zahrnout do pravidla automatického nasazení.  

5. Klikněte na tlačítko **Další** a pokračujte v vytváření pravidla automatického nasazení.  

> [!IMPORTANT]  
> Mějte na paměti, že v systémech s procesorem 64 (x64) jsou spuštěny 32bitové aplikace a komponenty v 32. Pokud si nejste jistí, že nepotřebujete x86, povolte ji i v případě, že zvolíte x64.  

### <a name="known-issues"></a>Známé problémy
Po přidání kritérií architektury se na stránce Vlastnosti pravidla automatického nasazení zobrazí **Nadpis** v kritériích hledání. Pravidlo automatického nasazení stále funguje podle očekávání a vybere správné aktualizace softwaru. V tuto chvíli ale nemůžete zahrnout kritéria **architektury** i **názvu** . <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Vylepšení nasazení operačního systému
Provedli jsme následující vylepšení nasazení operačního systému, přičemž některé z nich byly výsledkem zpětné vazby vašeho uživatele na hlas.  

- [Maskovat citlivá data uložená v proměnných pořadí úkolů](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): v kroku [nastavit proměnnou pořadí úkolů](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) vyberte novou možnost, aby se **Tato hodnota nezobrazila**. Například při zadávání hesla.<!--1358330--> Pokud povolíte tuto možnost, platí následující chování:
  - Hodnota proměnné se nezobrazuje v souboru Smsts. log.
  - Konzola Configuration Manager a poskytovatel serveru SMS zpracují tuto hodnotu stejně jako jiné tajné klíče, jako jsou hesla.
  - Hodnota není obsažena při exportu pořadí úloh.
  - Když upravíte krok, Editor pořadí úkolů tuto hodnotu nepřečetl. Přepište celou hodnotu, aby se změny provedly.

  > [!Important]  
  > Proměnné a jejich hodnoty jsou uloženy v pořadí úkolů jako XML a v databázi jsou zakódovány. Když klient požádá o zásadu pořadí úloh z bodu správy, zašifruje se při přenosu a při uložení na klienta. Všechny proměnné hodnoty jsou však v prostředí pořadí úloh v paměti během běhu v klientovi prostý text. Pokud pořadí úkolů obsahuje krok pro výstup hodnoty proměnné, je tento výstup v prostém textu. Toto chování vyžaduje explicitní akci správce k zahrnutí takového kroku v pořadí úkolů. 


- [Maskovat název programu během příkazu Spustit pořadí úkolů](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Pokud chcete zabránit zobrazení nebo protokolování potenciálně citlivých dat, nastavte proměnnou pořadí úkolů **OSDDoNotLogCommand** na `TRUE`. Tato proměnná maskuje název programu v souboru Smsts. log během kroku pořadí úkolů [Spustit příkazový řádek](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Vylepšení konzoly Configuration Manager
- Při zobrazení členů kolekce v části **prostředky a kompatibilita**, **kolekce zařízení**se teď zobrazují informace o primárním uživateli.<!--510252-->  



## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
