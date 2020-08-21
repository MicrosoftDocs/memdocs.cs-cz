---
title: Konzolové aktualizace
titleSuffix: Configuration Manager
description: Instalace aktualizací pro Configuration Manager z Microsoft cloudu
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f22a28c173c980bdf598a5afc8a969a86ec96cc2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699768"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Instalace konzolových aktualizací pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager se synchronizuje s cloudovou službou Microsoftu, aby získala aktualizace. Pak tyto aktualizace nainstalujte v konzole Configuration Manager.

## <a name="get-available-updates"></a>Získání dostupných aktualizací

Lokalita stáhne pouze aktualizace, které se vztahují k vaší infrastruktuře a verzi. Tato synchronizace může být automatická nebo ruční, podle toho, jak nakonfigurujete spojovací bod služby pro vaši hierarchii:

- V **online režimu**se spojovací bod služby automaticky připojuje ke cloudové službě Microsoftu a stahuje použitelné aktualizace.  

    Ve výchozím nastavení Configuration Manager kontroluje nové aktualizace každých 24 hodin. Ručně vyhledat aktualizace v konzole Configuration Manager. V pracovním prostoru **Správa** vyberte uzel **aktualizace a údržba** a na pásu karet zvolte **Vyhledat aktualizace** .  

- V **offline režimu**se spojovací bod služby nepřipojuje ke cloudové službě Microsoftu. Chcete-li stáhnout a následně importovat dostupné aktualizace, [použijte nástroj pro připojení služby](use-the-service-connection-tool.md).  

> [!NOTE]  
> V případě potřeby naimportujte do konzoly vzdálené opravy. K tomu použijte [Nástroj pro registraci aktualizací](use-the-update-registration-tool-to-import-hotfixes.md). Tyto opravy mimo pásmo doplňují aktualizace, které získáte při synchronizaci s cloudovou službou Microsoftu.  

Po dokončení aktualizace je zobrazte v konzole Configuration Manager. Otevřete pracovní prostor **Správa** a vyberte uzel **aktualizace a údržba** .  

- Aktualizace, které jste nenainstalovali, se zobrazí jako **dostupné**.  

- Aktualizace, které jste nainstalovali, se zobrazí jako **nainstalované**. Zobrazuje se jenom poslední nainstalovaná aktualizace. Chcete-li zobrazit dříve nainstalované aktualizace, vyberte na pásu karet možnost **Historie** .  

Před konfigurací spojovacího bodu služby je třeba pochopit a naplánovat jeho další použití. Následující použití může mít vliv na konfiguraci této role systému lokality:  

- Lokalita používá spojovací bod služby k odesílání informací o využití vašeho webu. Tyto informace pomáhají cloudové službě Microsoftu určit aktualizace, které jsou dostupné pro aktuální verzi vaší infrastruktury. Další informace najdete v tématu [Diagnostika a data o využití](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Chcete-li lépe pochopit, co se stane, když se stáhnou aktualizace, přečtěte si následující vývojové diagramy:  

- [Vývojový diagram – stahování aktualizací](download-updates-flowchart.md)  

- [Vývojový diagram – replikace aktualizací](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Přiřazení oprávnění k zobrazení a správě aktualizací a funkcí

Chcete-li zobrazit aktualizace v konzole nástroje, musí mít uživatel roli zabezpečení správy na základě rolí, která zahrnuje **balíčky aktualizací**třídy zabezpečení. Tato třída uděluje přístup pro zobrazení a správu aktualizací v konzole Configuration Manager.

### <a name="about-the-update-packages-class"></a>O třídě balíčky aktualizací

Ve výchozím nastavení je třída **balíčky aktualizací** (SMS_CM_Updatepackages) součástí následujících předdefinovaných rolí zabezpečení s uvedenými oprávněními:  

- **Správce s úplnými oprávněními** s oprávněními **Upravit** a **Číst** :  

  - Uživatel s touto rolí zabezpečení a přístupem k oboru zabezpečení **All** může zobrazit a nainstalovat aktualizace. Uživatel může v průběhu instalace povolit i funkce a po aktualizaci lokality povolit jednotlivé funkce.  

  - Uživatel s touto rolí zabezpečení a přístupem k **výchozímu** oboru zabezpečení může zobrazit a nainstalovat aktualizace. Uživatel může v průběhu instalace povolit i funkce a zobrazit funkce po aktualizaci lokality. Tento uživatel ale nebude moct po aktualizaci lokality tyto funkce povolit.  

- **Analytik jen pro čtení** s oprávněním **Číst** :  

  - Uživatel s touto rolí zabezpečení a přístupem k **výchozímu** oboru může zobrazit aktualizace, ale nebude je instalovat. Tento uživatel může také zobrazit funkce po aktualizaci lokality, ale nemůže je povolit.  

### <a name="permissions-required-for-updates-and-servicing"></a>Oprávnění požadovaná pro aktualizace a údržbu

- Použijte účet, ke kterému přiřadíte roli zabezpečení zahrnující třídu **balíčky aktualizací** s oprávněním **Upravit** i **číst** .  

- Přiřaďte účet k **výchozímu** oboru.  

### <a name="permissions-to-only-view-updates"></a>Oprávnění pouze k zobrazení aktualizací

- Použijte účet, ke kterému přiřadíte roli zabezpečení zahrnující třídu **balíčky aktualizací** pouze s oprávněním **číst** .  

- Přiřaďte účet k **výchozímu** oboru.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Oprávnění vyžadovaná k povolení funkcí po aktualizacích webu

- Použijte účet, ke kterému přiřadíte roli zabezpečení zahrnující třídu **balíčky aktualizací** s oprávněním **Upravit** i **číst** .  

- Přiřaďte účet k oboru **vše** .  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Před instalací konzolové aktualizace  

Než nainstalujete aktualizaci z konzoly Configuration Manager, přečtěte si následující kroky.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Krok 1: Kontrola kontrolního seznamu aktualizací  

Před zahájením aktualizace si přečtěte příslušný kontrolní seznam aktualizací, který bude trvat:

- [Kontrolní seznam pro instalaci aktualizace 2006](checklist-for-installing-update-2006.md)

- [Kontrolní seznam pro instalaci aktualizace 2002](checklist-for-installing-update-2002.md)

- [Kontrolní seznam pro instalaci aktualizace 1910](checklist-for-installing-update-1910.md)  

- [Kontrolní seznam pro instalaci aktualizace 1906](checklist-for-installing-update-1906.md)  

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a> Krok 2: spuštění kontroly požadovaných součástí před instalací aktualizace  

Než nainstalujete aktualizaci, zvažte, jestli by nebylo dobré spustit pro ni kontrolu požadovaných součástí. Pokud před instalací aktualizace spustíte kontrolu požadovaných součástí:  

- Lokalita před instalací aktualizace replikuje soubory aktualizace na jiné lokality.  

- Pokud zvolíte instalaci aktualizace, Kontrola požadovaných součástí se automaticky spustí znovu.  

> [!NOTE]  
> Když zahájíte kontrolu požadavků a pak zobrazíte stav, bude **instalační** fáze pravděpodobně aktivní. Lokalita ale ve skutečnosti nenainstaluje aktualizaci. Chcete-li spustit kontrolu požadovaných součástí, proces aktualizace extrahuje balíček z knihovny obsahu. Pak balíček vloží do pracovní složky, kde má přístup k aktuálním kontrolám předpokladů. Při instalaci aktualizace se spustí stejný proces. Toto chování je **důvod, proč**se instalační fáze zobrazuje jako probíhající. V kategorii instalace se zobrazí pouze krok *extrahovat balíček aktualizace* .  

Později při instalaci aktualizace můžete nakonfigurovat aktualizaci tak, aby ignorovala upozornění kontroly požadavků.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Postup spuštění kontroly požadovaných součástí před instalací aktualizace  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **aktualizace a údržba** .  

2. Vyberte balíček aktualizace, pro který chcete spustit kontrolu požadovaných součástí.  

3. Na pásu karet vyberte **Spustit kontrolu požadovaných součástí** .  

    Když spustíte kontrolu požadovaných součástí, obsah aktualizace se replikuje do podřízených lokalit. Zobrazte **Distmgr. log** na serveru lokality a potvrďte tak, že se obsah úspěšně replikuje.  

4. Zobrazení výsledků kontroly požadovaných součástí:  

    1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** .  

    2. Vyberte uzel **aktualizace a stav údržby** a vyhledejte stav předpokladů.  

    3. Další informace najdete v tématu **souboru ConfigMgrPrereq. log** na serveru lokality.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> Instalace konzolových aktualizací  

Až budete připraveni k instalaci aktualizací z konzoly Configuration Manager, začněte s lokalitou nejvyšší úrovně ve vaší hierarchii. Tato lokalita je buď lokalita centrální správy, nebo samostatná primární lokalita.  

Nainstalujte aktualizaci mimo běžnou pracovní dobu pro každou lokalitu, abyste minimalizovali dopad na obchodní operace. Instalace aktualizace může zahrnovat akce, jako je přeinstalace součástí lokality a rolí systému lokality.  

- Podřízené primární lokality automaticky spustí aktualizaci poté, co lokalita centrální správy dokončí instalaci aktualizace. Tento proces je ve výchozím nastavení a doporučený. Chcete-li určit, kdy má primární lokalita instalovat aktualizace, použijte [pro servery lokality servisní systémy](service-windows.md).  

- Po dokončení aktualizace primární nadřazené lokality ručně aktualizujte sekundární lokality v konzole Configuration Manager. Automatické aktualizace serverů sekundárních lokalit se nepodporují.  

- Když po aktualizaci lokality použijete konzolu Configuration Manager, budete vyzváni k aktualizaci konzoly.  

- Po úspěšném dokončení instalace aktualizace serverem lokality se automaticky aktualizují všechny příslušné role systému lokality. Všechny distribuční body se ale neinstalují znovu a nejdou přejít do režimu offline, aby se aktualizovaly současně. Místo toho server lokality používá nastavení distribuce obsahu lokality k distribuci aktualizace do podmnožiny distribučních bodů najednou. Výsledkem je, že pouze některé distribuční body jsou offline, aby se aktualizace nainstalovala. Distribuční body, které nezačaly aktualizovat nebo které dokončily aktualizaci, zůstávají online a můžou klientům poskytovat obsah.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Přehled instalace konzolových aktualizací  

#### <a name="1-when-the-update-installation-starts"></a>1. Při spuštění instalace aktualizace

Zobrazí se Průvodce aktualizacemi, který zobrazuje seznam oblastí produktu, na které se aktualizace vztahuje.  

- Na stránce **Obecné** v průvodci nakonfigurujte **Upozornění na předpoklady** podle potřeby:  

  - Chyby požadovaných součástí vždycky zastaví instalaci aktualizace. Opravte chyby, abyste mohli úspěšně opakovat instalaci aktualizace. Další informace najdete v tématu [opakování instalace aktualizace, která se nezdařila](#bkmk_retry).  

  - Instalaci aktualizací můžou zastavit i upozornění kontroly požadavků. Před opakováním instalace aktualizace opravte upozornění. Další informace najdete v tématu [opakování instalace aktualizace, která se nezdařila](#bkmk_retry).  

  - **Ignorovat upozornění kontroly požadavků a nainstalovat tuto aktualizaci bez ohledu na chybějící požadavky**: nastavte podmínku pro instalaci aktualizace tak, aby ignorovala upozornění na předpoklady. Tato možnost umožní pokračování instalace aktualizace. Pokud tuto možnost nevyberete, instalace aktualizace se zastaví, když proces narazí na upozornění. Tuto možnost nepoužívejte, pokud jste předtím nespustili kontrolu požadovaných součástí a opravili upozornění na požadované součásti lokality.  

    V pracovních prostorech **pro správu** a **monitorování** obsahuje uzel aktualizace a údržba na pásu karet tlačítko s názvem **Ignorovat upozornění na předpoklady**. Toto tlačítko je k dispozici, když se nepovede dokončit instalaci balíčku aktualizací kvůli upozorněním na kontrolu požadavků. Například nainstalujete aktualizaci bez použití možnosti ignorovat upozornění na předpoklady (v rámci průvodce aktualizacemi). Instalace aktualizace se zastaví se stavem upozornění na předpoklady, ale žádné chyby. Později v pásu karet vyberete **Ignorovat upozornění na předpoklady** . Tato akce aktivuje automatické pokračování instalace aktualizace, která ignoruje upozornění na předpoklady. Když použijete tuto možnost, instalace aktualizace automaticky pokračuje po několika minutách.  

- Pokud se aktualizace vztahuje na klienta Configuration Manager, vyberte možnost otestovat aktualizaci klienta s omezeným počtem klientů. Další informace najdete v tématu [testování upgradu klienta v předprodukční kolekci](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Při instalaci aktualizace

V rámci instalace aktualizace Configuration Manager provádí následující akce:  

- Přeinstaluje všechny ovlivněné komponenty, jako jsou role systému lokality nebo konzola Configuration Manager.  

- Spravuje aktualizace klientů na základě výběrů, které jste provedli pro pilotní nasazení klientů, a pro [automatické upgrady klientů](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Servery systému lokality zpravidla není nutné restartovat v rámci aktualizace. Pokud role používá .NET a balíček aktualizuje tuto požadovanou součást, může dojít k restartování systému lokality.  

> [!TIP]  
> Když instalujete aktualizace Configuration Manager, lokalita také aktualizuje disk CD. Poslední složka Další informace najdete [na disku CD. Poslední složka](the-cd.latest-folder.md)  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Monitorování průběhu aktualizací během instalace

Průběh můžete sledovat pomocí následujících kroků:  

- V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **aktualizace a údržba** . V tomto uzlu se zobrazuje stav instalace všech balíčků aktualizace.  

- V konzole Configuration Manager klikněte na pracovní prostor **monitorování** a vyberte uzel **stav aktualizace a údržba** . V tomto uzlu se zobrazuje stav instalace jenom pro aktuální balíček aktualizace, který lokalita instaluje.  

    Instalace aktualizace je rozdělená do několika fází pro snazší monitorování. Pro každou z následujících fází se zobrazí další podrobnosti o stavu instalace, který obsahuje soubor protokolu, který se má zobrazit, kde najdete další informace:  

  - **Stažení**: Tato fáze se vztahuje pouze na lokalitu nejvyšší úrovně se spojovacím bodem služby.

  - **Replikace**

  - **Kontrola předpokladů**

  - **Instalace**

  - **Po instalaci**: Další informace najdete v tématu [úlohy po instalaci](#post-installation-tasks).  

- Zobrazení souboru **CMUpdate. log** v nástroji `<ConfigMgr_Installation_Directory>\Logs` na serveru lokality.  

>[!NOTE]
> Počínaje verzí 1906 můžete zobrazit stav úlohy **aktualizace databáze nástroje ConfigMgr** během fáze **instalace** .
>
> - Pokud je upgrade databáze zablokován, bude vám docházet k zadanému upozornění **, bude nutné věnovat pozornost**.
>   - Protokol CMUpdate. log zaznamená název programu a identifikátor SessionID z SQL, který blokuje upgrade databáze.
> - Pokud upgrade databáze již není zablokován, bude stav **resetován na hodnotu probíhá nebo** **dokončeno**.
>   - Pokud je upgrade databáze zablokován, je tato kontrolu provedena každých 5 minut, aby se zobrazila, zda je stále blokovaná.

#### <a name="4-when-the-update-installation-completes"></a>4. Po dokončení instalace aktualizace

Po dokončení instalace aktualizace první lokality:  

- Podřízené primární lokality instalují aktualizaci automaticky. Nevyžaduje se žádná další akce.  

- V konzole Configuration Manager ručně aktualizujte sekundární lokality. Další informace najdete v tématu [spuštění instalace aktualizace v sekundární lokalitě](#bkmk_secondary).  

- Dokud se všechny lokality v hierarchii neaktualizují na novou verzi, hierarchie funguje v režimu smíšených verzí. Další informace najdete v tématu [vzájemná funkční spolupráce mezi různými verzemi](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. aktualizace Configuration Managerch konzol

Po aktualizaci lokality centrální správy nebo primární lokality je potřeba aktualizovat také každou konzolu Configuration Manager, která se připojuje k lokalitě nástroje. Zobrazuje se výzva k aktualizaci konzoly:  

- Když otevřete konzolu.  

- Když přejdete na nový uzel v otevřené konzole  

Aktualizujte konzolu hned po aktualizaci lokality.  

Po dokončení aktualizace konzoly ověřte, že je verze konzoly a lokality správná. V levém horním rohu konzoly najdete **informace o Configuration Manager** .  

> [!Note]  
> Verze konzoly se mírně liší od verze lokality. Podverze konzoly odpovídá verzi Configuration Manager vydané verze. Například v Configuration Manager verze 1802 je počáteční verze lokality 5.0.8634.1000 a počáteční verze konzoly je 5. **1802**. 1082,1700. Čísla Build (1082) a revize (1700) se můžou v budoucích opravách hotfix změnit.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a> Postup spuštění instalace aktualizace v lokalitě nejvyšší úrovně  

V lokalitě nejvyšší úrovně ve vaší hierarchii v konzole Configuration Manager klikněte na pracovní prostor **Správa** a vyberte uzel **aktualizace a údržba** . Vyberte aktualizaci se stavem **k dispozici**a pak na pásu karet zvolte **instalovat balíček aktualizací** .  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Postup spuštění instalace aktualizace v sekundární lokalitě  

Po aktualizaci nadřazené primární lokality sekundární lokality aktualizujte sekundární lokalitu v konzole Configuration Manager. K tomu slouží **Průvodce upgradem sekundární lokality**.  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte sekundární lokalitu, kterou chcete aktualizovat, a pak na pásu karet zvolte **upgradovat** .  

2. Vyberte **Ano** , pokud chcete spustit aktualizaci sekundární lokality.  

Chcete-li monitorovat instalaci aktualizací v sekundární lokalitě, vyberte sekundární lokalitu a na pásu karet zvolte možnost **Zobrazit stav instalace** . Přidejte také sloupec **verze** do uzlu lokality, abyste mohli zobrazit verzi jednotlivých sekundárních lokalit.  

V některých případech se stav v konzole neaktualizuje nebo naznačuje, že se aktualizace nezdařila. Po úspěšném dokončení aktualizace sekundární lokality použijte možnost **opakovat instalaci** . Tato možnost neprovádí přeinstalaci aktualizace sekundární lokality, která úspěšně nainstalovala aktualizaci, ale vynutí, aby konzola aktualizovala stav.

### <a name="post-installation-tasks"></a>Úlohy po instalaci

Když lokalita nainstaluje aktualizaci, existuje několik úloh, které nelze spustit až po dokončení instalace aktualizace na serveru lokality. Tento seznam obsahuje úlohy po instalaci, které jsou klíčové pro operace lokality a hierarchie. Protože jsou kritické, jsou aktivně monitorovány. Další úkoly, které nejsou přímo monitorovány, zahrnují přeinstalaci rolí systému lokality. Chcete-li zobrazit stav nejdůležitějších úloh po instalaci, vyberte úlohu **po instalaci** během monitorování instalace aktualizace lokality.

Ne všechny úlohy se dokončí okamžitě. Některé úlohy se nespustí, dokud každá lokalita nedokončí instalaci aktualizace. Nové funkce, které byste mohli očekávat, je možné zpozdit až do dokončení těchto úloh. Zapnutí nových funkcí se nespustí, dokud všechny lokality nedokončí instalaci aktualizace, takže nové funkce nemusí být pro určitou dobu viditelné.

Úlohy po instalaci zahrnují:

- **Instalace služby SMS_EXECUTIVE**

  - Kritická služba, která běží na serveru lokality.
  - Přeinstalace této služby by měla být dokončena rychle.

- **Instalace součásti SMS_DATABASE_NOTIFICATION_MONITOR**

  - Vlákno součásti důležitého webového serveru služby SMS_EXECUTIVE.
  - Přeinstalace této služby by měla být dokončena rychle.

- **Instalace součásti SMS_HIERARCHY_MANAGER**

  - Kritická součást lokality, která je spuštěna na serveru lokality.
  - Zodpovídá za přeinstalaci rolí na serverech systému lokality. Stav pro individuální přeinstalaci role systému lokality se nezobrazuje.
  - Přeinstalace této služby by měla být dokončena rychle.

    > [!Note]
    > Některé Configuration Manager role lokality sdílejí rozhraní klienta. Například bod správy a distribuční bod pro vyžádání obsahu. Když se tyto role aktualizují, verze klienta na těchto serverech se aktualizuje ve stejnou dobu. Další informace najdete v tématu [Postup upgradu klientů](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Instalace součásti SMS_REPLICATION_CONFIGURATION_MONITOR**

  - Kritická součást lokality, která je spuštěna na serveru lokality.
  - Přeinstalace této služby by měla být dokončena rychle.

- **Instalace součásti SMS_POLICY_PROVIDER**

  - Kritická součást lokality, která se spouští pouze v primárních lokalitách.
  - Přeinstalace této služby by měla být dokončena rychle.

- **Monitorování inicializace replikace**

  - Tato úloha se zobrazí pouze v lokalitě centrální správy a v podřízených primárních lokalitách.
  - Závisí na SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Mělo by se rychle dokončit.

- **Aktualizace předprodukčního balíčku klienta Configuration Manager**

  - Tato úloha se zobrazí i v případě, že není povoleno použití předprodukčního klienta (označuje se také jako pilotní nasazení klienta).
  - Nespustí se, dokud všechny lokality v hierarchii nedokončí instalaci aktualizace.

- **Aktualizace složky Client na serveru lokality**

  - Tato úloha se nezobrazí, pokud používáte klienta v předprodukčním prostředí.  
  - Mělo by se rychle dokončit.

- **Aktualizuje se balíček klienta Configuration Manager.**

  - Tato úloha se nezobrazí, pokud používáte klienta v předprodukčním prostředí.  
  - Dokončí až po instalaci aktualizace všemi lokalitami.  

- **Zapnutí funkcí**

  - Tato úloha se zobrazí pouze v lokalitě nejvyšší úrovně v hierarchii.
  - Nespustí se, dokud všechny lokality v hierarchii nedokončí instalaci aktualizace.
  - Jednotlivé funkce se nezobrazují.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Opakování instalace aktualizace, která se nezdařila  

Když se nějakou aktualizaci nepodaří nainstalovat, přečtěte si zpětnou vazbu v konzole, abyste zjistili, jak vyřešit upozornění a chyby. Další podrobnosti najdete v **protokolu souboru ConfigMgrPrereq. log** na serveru lokality. Než zopakujete instalaci aktualizace, je nutné opravit chyby a opravit upozornění.  

> [!TIP]  
> Pokud má aktualizace potíže při stahování nebo replikaci, použijte nástroj pro [Obnovení aktualizací](update-reset-tool.md).  

Až budete připraveni zopakovat instalaci aktualizace, vyberte neúspěšnou aktualizaci a pak zvolte příslušnou možnost. Chování při opakování instalace aktualizace závisí na uzlu, ve kterém se spouští opakování, a na používané možnosti opakování.  

### <a name="retry-installation-for-the-hierarchy"></a>Opakovaný pokus o instalaci pro hierarchii

Opakujte instalaci aktualizace pro celou hierarchii, pokud je tato aktualizace v některém z následujících stavů:  

- Kontrola požadovaných součástí byla dokončena s jedním nebo více upozorněními a možnost Ignorovat upozornění kontroly požadavků nebyla nastavena v Průvodci aktualizací. (Hodnota aktualizace pro **Ignorovat požadavků ohlásila upozornění** v uzlu **aktualizace a údržba** je **ne**.)

- Kontrola požadovaných součástí se nezdařila.

- Instalace se nezdařila.  

- Replikace obsahu na lokalitu se nezdařila.

Otevřete pracovní prostor **Správa** a vyberte uzel **aktualizace a údržba** . Vyberte aktualizaci a pak zvolte jednu z následujících možností:  

- **Opakovat**: když se znovu **pokusíte** z **aktualizace a obsluhy**, znovu se spustí instalace aktualizace a automaticky se ignorují upozornění na předpoklady. Pokud se dřív nezdařila replikace obsahu, obsah pro aktualizaci se znovu replikuje.  

- **Ignorovat upozornění na předpoklady**: Pokud se instalace aktualizace zastaví z důvodu upozornění, můžete zvolit **Ignorovat upozornění na předpoklady**. Tato akce umožní, aby instalace aktualizace pokračovala po několika minutách a použila možnost Ignorovat upozornění na předpoklady.

### <a name="retry-installation-for-the-site"></a>Opakovaný pokus o instalaci pro lokalitu

Opakujte instalaci aktualizace v konkrétní lokalitě, pokud je tato aktualizace v některém z následujících stavů:  

- Kontrola požadovaných součástí byla dokončena s jedním nebo více upozorněními a možnost Ignorovat upozornění kontroly požadavků nebyla nastavena v Průvodci aktualizací. (Hodnota aktualizace pro **Ignorovat požadavků ohlásila upozornění** v uzlu aktualizace a údržba je **ne**.)  

- Kontrola požadovaných součástí se nezdařila.

- Instalace se nezdařila.

V pracovním prostoru **monitorování** vyberte uzel **stav údržby lokality** . Vyberte aktualizaci a pak zvolte jednu z následujících možností:  

- **Opakovat**: **když se** pokusíte o **stav údržby lokality**, restartujete instalaci aktualizace jenom v této lokalitě. Na rozdíl od spuštění **opakování** z uzlu **aktualizace a údržba** tento pokus Neignoruje upozornění na předpoklady.  

- **Ignorovat upozornění na předpoklady**: Pokud se instalace aktualizace zastaví z důvodu upozornění, můžete vybrat **Ignorovat upozornění na předpoklady**. Tato akce umožní, aby instalace aktualizace pokračovala po několika minutách a použila možnost Ignorovat upozornění na předpoklady.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Po instalaci aktualizace lokality  

Po aktualizaci lokality si projděte kontrolní seznam po aktualizaci pro příslušnou verzi:  

- [Kontrolní seznam po aktualizaci pro verzi 2006](checklist-for-installing-update-2006.md#post-update-checklist)

- [Kontrolní seznam po aktualizaci pro verzi 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Kontrolní seznam po aktualizaci pro verzi 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Kontrolní seznam po aktualizaci pro verzi 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Povolit volitelné funkce z aktualizací  

Pokud aktualizace obsahuje jednu nebo více volitelných funkcí, máte možnost povolit tyto funkce ve vaší hierarchii. Povolte funkce při instalaci aktualizace nebo se vraťte do konzoly později, aby se povolily volitelné funkce.

Chcete-li zobrazit dostupné funkce a jejich stav, v konzole nástroje přejdete do pracovního prostoru **Správa** , rozbalte položku **aktualizace a údržba**a vyberte uzel **funkce** .

Pokud funkce není volitelná, nainstaluje se automaticky. Nezobrazuje se v uzlu **funkce** .  

> [!IMPORTANT]
> V hierarchii s více lokalitami povolte volitelné nebo předběžné verze funkcí pouze z centrální lokality pro správu. Toto chování zajistí, že v hierarchii nejsou žádné konflikty. <!--507197-->  

Pokud povolíte novou funkci nebo předběžnou verzi funkce, Správce hierarchie Configuration Manager (HMAN) musí před tím, než bude tato funkce dostupná, zpracovat změnu. Zpracování změny je často okamžité. V závislosti na cyklu zpracování HMAN může trvat až 30 minut, než se dokončí. Po zpracování změny restartujte konzolu, než budete moci funkci použít.

Počínaje verzí 2002,<!--5834830--> Když jsou v centru pro správu Microsoft Endpoint Manageru k dispozici nové cloudové funkce nebo jiné připojené cloudové služby pro místní instalaci Configuration Manager, můžete se teď v konzole Configuration Manager přihlásit k těmto novým funkcím.

### <a name="list-of-optional-features"></a>Seznam volitelných funkcí

Následující funkce jsou volitelné v nejnovější verzi Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Centrum komunity](community-hub.md)<!--3555935, C098DA03-C33C-4E15-B337-6C0FEEB3CB8A-->
- [Skupiny orchestrace](../../../sum/deploy-use/orchestration-groups.md)<!--3098816, 290B66D8-C735-4895-B59A-DD732D84A697-->
- [Typ nasazení pořadí úloh](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!-- 3555953, CB0CDFFB-9C6F-4B18-8954-A43A387302A2-->
- [Správa nástroje BitLocker](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Synchronizovat výsledky členství kolekce s Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Azure Active Directory zjišťování skupiny uživatelů](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Skupiny aplikací](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Ladicí program pořadí úloh](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Aktualizace softwaru třetích stran](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Schvalovat žádosti o aplikace pro uživatele na zařízení](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Vytváření a spouštění skriptů](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Aktualizace ovladačů Surface](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Brána pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [Vytvoření PFX](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Konektor Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Zásady ochrany před zneužitím v programu Windows Defender](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [SÍŤ VPN pro Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Údržba kolekce podporující clustery (skupiny serverů)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello pro firmy](../../../protect/deploy-use/windows-hello-for-business-settings.md) (dříve označované jako *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!TIP]
> Další informace o funkcích, které vyžadují souhlas s povolením, najdete v tématu [předběžné verze funkcí](pre-release-features.md).  
>
> Další informace o funkcích, které jsou k dispozici pouze ve větvi Technical Preview, najdete v tématu [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Použití předběžných verzí funkcí z aktualizací

Aktuální větev obsahuje předběžné verze funkcí pro prvotní testování v produkčním prostředí. Další informace najdete v tématu [předběžné verze funkcí](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Nejčastější dotazy

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Proč v konzole nevidím některé aktualizace?

Pokud v konzole nemůžete po úspěšné synchronizaci s cloudovou službou Microsoftu najít konkrétní aktualizaci, může to být způsobeno jedním z následujících důvodů:  

- Tato aktualizace vyžaduje konfiguraci, kterou vaše infrastruktura nepoužívá, nebo vaše aktuální verze produktu nesplňuje požadavky pro příjem aktualizace.  

    Pokud si myslíte, že máte požadované konfigurace a předpoklady pro chybějící aktualizaci, zkontrolujte, jestli je spojovací bod služby v online režimu. Pak pomocí možnosti **Vyhledat aktualizace** v uzlu **aktualizace a údržba** vynuťte kontrolu. Pokud je spojovací bod služby v režimu offline, použijte nástroj pro připojení služby k ruční synchronizaci s cloudovou službou.  

- Váš účet nemá správná oprávnění pro správu na základě rolí pro zobrazení aktualizací v konzole Configuration Manager. Další informace najdete v tématu [oprávnění ke správě aktualizací](#assign-permissions-to-view-and-manage-updates-and-features).