---
title: Správa aktualizací aplikací Microsoft 365
titleSuffix: Configuration Manager
description: Configuration Manager synchronizuje aktualizace klienta Microsoft 365 Apps z katalogu služby WSUS do serveru lokality, aby byly aktualizace k dispozici pro nasazení na klienty.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 907c8d63d68ee4f34b9d22be24f32ffb1878b715
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696170"
---
# <a name="manage-microsoft-365-apps-with-configuration-manager"></a>Správa aplikací Microsoft 365 s využitím Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Note]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

Configuration Manager vám umožní spravovat aplikace Microsoft 365 těmito způsoby:

- [Nasazení Microsoft 365Ch aplikací](#bkmk_deploy): pomocí [řídicího panelu pro správu klientů Office 365](office-365-dashboard.md) můžete spustit instalační program Microsoft 365ch aplikací a usnadnit tak počáteční instalaci Microsoft 365 aplikací. Průvodce umožňuje konfigurovat nastavení instalace Microsoft 365 Apps, stahovat soubory ze sítí pro doručování obsahu (sítě CDN) pro Office a vytvářet a nasazovat aplikace skriptu s obsahem.

- [Nasazení aktualizací Microsoft 365Ch aplikací](#bkmk_update): aktualizace klienta Microsoft 365 Apps můžete spravovat pomocí pracovního postupu správy softwarových aktualizací. Když Microsoft publikuje v Office Content Delivery Network (CDN) novou aktualizaci Microsoft 365 Apps, publikuje také balíček aktualizací pro Windows Server Update Services (WSUS). Jakmile Configuration Manager synchronizuje aktualizace Microsoft 365ch aplikací z katalogu služby WSUS na server lokality, bude aktualizace k dispozici pro nasazení na klienty.

   > [!NOTE]
   > Od verze Configuration Manager 2002 můžete importovat Microsoft 365 aplikace do odpojených prostředí. Další informace najdete v tématu [synchronizace aktualizací Microsoft 365Ch aplikací z odpojeného bodu aktualizace softwaru](../get-started/synchronize-office-updates-disconnected.md).   

- [Přidat jazyky pro stažení aktualizací Microsoft 365 Apps](#bkmk_o365_lang): můžete přidat podporu pro Configuration Manager ke stažení aktualizací pro všechny jazyky, které aplikace Microsoft 365 Apps podporuje. To znamená, že Configuration Manager nemusí podporovat jazyk, dokud Microsoft 365 aplikace. Před Configuration Manager verze 1610 musíte stáhnout a nasadit aktualizace ve stejných jazycích nakonfigurovaných na klientech Microsoft 365 aplikací.

- [Změna kanálu pro aktualizace](#bkmk_channel): pomocí zásad skupiny můžete distribuovat změnu hodnoty klíče registru, aby se klienti Microsoft 365 aplikací změnili kanál aktualizace.

Chcete-li zkontrolovat informace o klientovi Microsoft 365 Apps a spustit některé z těchto akcí správy aplikace Microsoft 365, použijte [řídicí panel pro správu klientů Office 365](office-365-dashboard.md).

## <a name="deploy-microsoft-365-apps"></a><a name="bkmk_deploy"></a> Nasazení Microsoft 365ch aplikací
Spusťte instalační program Microsoft 365 Apps z řídicího panelu pro správu klientů Office 365 pro úvodní instalaci Microsoft 365ch aplikací. Průvodce vám umožní nakonfigurovat nastavení instalace Microsoft 365 Apps, stahovat soubory ze sítě pro doručování obsahu (sítě CDN) pro Office a vytvářet a nasazovat skriptovací aplikace pro soubory. Dokud se na klientech nenainstalovaly aplikace Microsoft 365 a spouští se [úloha automatické aktualizace Microsoft 365 aplikací](/deployoffice/overview-update-process-microsoft-365-apps) , Microsoft 365 aktualizace aplikací se nedají použít. Pro účely testování můžete spustit úlohu aktualizace ručně.

Pro předchozí verze Configuration Manager musíte provést následující kroky a nainstalovat Microsoft 365 aplikace poprvé na klientech:
- Stáhnout nástroj pro nasazení Office (ODT)
- Stáhněte zdrojové instalační soubory aplikace Microsoft 365, včetně všech jazykových sad, které potřebujete.
- Vygenerujte Configuration.xml, které určují správnou verzi Microsoft 365 aplikací a kanál.
- Vytvořte a nasaďte starší balíček nebo aplikaci skriptu pro klienty, kteří budou instalovat aplikace Microsoft 365.

### <a name="requirements"></a>Požadavky
- Počítač, který spouští instalační program, musí mít přístup k Internetu.  
- Uživatel, který spouští instalační program, musí mít oprávnění **ke čtení** a **zápisu** pro sdílenou složku umístění obsahu, která je k dispozici v průvodci.
- Pokud se zobrazí chyba stahování 404, zkopírujte následující soubory do složky uživatele% Temp%:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1806-or-higher"></a>Nasazení Microsoft 365 aplikací pomocí Configuration Manager verze 1806 nebo vyšší: 
Počínaje Configuration Manager 1806 Nástroj pro přizpůsobení sady Office je integrovaný do instalačního programu v konzole Configuration Manager. Při vytváření nasazení pro aplikace Microsoft 365 můžete dynamicky konfigurovat nejnovější nastavení spravovatelnosti. <!--1358149-->

1. V konzole Configuration Manager přejděte do části Přehled **knihovny softwaru**  >  **Overview**  >  **Office 365 Správa klientů**.
2. V pravém horním podokně klikněte na **instalační program Office 365** . Otevře se Průvodce instalací nástroje.
3. Na stránce **nastavení aplikace** zadejte název a popis aplikace, zadejte umístění pro stažení souborů a potom klikněte na tlačítko **Další**. Umístění musí být zadané jako &#92;&#92;*server*&#92;*Shared*.
4. Na stránce **Nastavení Office** klikněte na **Přejít k nástroji pro přizpůsobení Office**. Otevře se [Nástroj pro přizpůsobení Office pro kliknutí na spuštění](https://config.office.com).
5. Nakonfigurujte požadovaná nastavení pro instalaci aplikací Microsoft 365. Po dokončení konfigurace klikněte na **Odeslat** v pravém horním rohu stránky. 
6. Na stránce **nasazení** určete, zda chcete nasadit nyní nebo později. Pokud se rozhodnete k nasazení později, můžete aplikaci najít v **Software Library**  >  **aplikacích pro správu aplikací**v knihovně softwaru  >  **Applications**.  
7. Potvrďte nastavení na stránce **Souhrn** . 
8. Klikněte na tlačítko **Další** a po dokončení průvodce klikněte na tlačítko **Zavřít** . 

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1802-and-prior"></a>Nasaďte Microsoft 365 aplikace pomocí Configuration Manager verze 1802 a předchozí:

1. V konzole Configuration Manager přejděte do části Přehled **knihovny softwaru**  >  **Overview**  >  **Office 365 Správa klientů**.
2. V pravém horním podokně klikněte na **instalační program Office 365** . Otevře se Průvodce instalací nástroje.
3. Na stránce **nastavení aplikace** zadejte název a popis aplikace, zadejte umístění pro stažení souborů a potom klikněte na tlačítko **Další**. Umístění musí být zadané jako &#92;&#92;*server*&#92;*Shared*.
4. Na stránce **importovat nastavení klienta** vyberte, zda chcete importovat nastavení klienta aplikace Microsoft 365 Apps z existujícího konfiguračního souboru XML nebo ručně zadat nastavení. Až budete hotovi, klikněte na **Další** .  

    Pokud máte existující konfigurační soubor, zadejte umístění souboru a přejděte ke kroku 7. Je nutné zadat umístění ve formuláři &#92;&#92;*server*&#92;*sdílet*&#92;*filename*. XML.
    > [!IMPORTANT]    
    > Konfigurační soubor XML musí obsahovat jenom [jazyky, které podporuje Office 2016](/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Na stránce **klientské produkty** vyberte sadu Microsoft 365 Apps, kterou používáte. Vyberte aplikace, které chcete zahrnout. Vyberte všechny další produkty, které by měly být zahrnuty, a poté klikněte na tlačítko **Další**.
6. Na stránce **nastavení klienta** vyberte nastavení, které chcete zahrnout, a potom klikněte na tlačítko **Další**.
7. Na stránce **nasazení** vyberte, zda chcete aplikaci nasadit, a poté klikněte na tlačítko **Další**. <br/>Pokud se rozhodnete nenasadit balíček v průvodci, přejděte ke kroku 9.
8. Nakonfigurujte zbývající stránky průvodce jako při typickém nasazení aplikace. Podrobnosti najdete v tématu [Vytvoření a nasazení aplikace](../../apps/get-started/create-and-deploy-an-application.md).
9. Dokončete průvodce.
10. Můžete nasadit nebo upravit aplikaci z **knihovny softwaru**  >  **Přehled**  >  **aplikací pro správu aplikací**  >  **Applications**.

Když pomocí instalačního programu vytvoříte a nasadíte aplikace Microsoft 365, Configuration Manager ve výchozím nastavení nespravují aktualizace aplikací Microsoft 365. Pokud chcete klientům Microsoft 365ch aplikací povolit příjem aktualizací z Configuration Manager, přečtěte si téma [nasazení aktualizací Microsoft 365 aplikací pomocí Configuration Manager](#bkmk_update).

Po nasazení aplikací Microsoft 365 můžete vytvořit pravidla automatického nasazení, která budou aplikace spravovat. Pokud chcete vytvořit pravidlo automatického nasazení pro Microsoft 365 aplikace, klikněte na **vytvořit** pravidlo automatického nasazení z [řídicího panelu pro správu klientů Office 365](office-365-dashboard.md). Když vyberete produkt, vyberte **klienta Office 365** . Další informace najdete v tématu [automatické nasazení aktualizací softwaru](automatically-deploy-software-updates.md).


## <a name="drill-through-required-microsoft-365-apps-updates"></a>Podrobné informace o požadovaných aktualizacích Microsoft 365 aplikací
<!--4224414-->
*(Představené ve verzi 1906)*

Můžete procházet statistiky dodržování předpisů a zjistit, která zařízení vyžadují konkrétní aktualizaci softwaru Microsoft 365 Apps. Chcete-li zobrazit seznam zařízení, potřebujete oprávnění k zobrazení aktualizací a kolekcí, do kterých zařízení patří. Přechod k podrobnostem v seznamu zařízení:

1. Přejít na **Software Library**  >  **Office 365**  >  **Update Management Office 365 Updates**.
1. Vyberte jakoukoli aktualizaci, kterou vyžaduje aspoň jedno zařízení.
1. Podívejte se na kartu **Souhrn** a v části  **Statistika**Najděte výsečový graf.
1. Pokud chcete přejít k podrobnostem seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu.
1. Tato akce přejde na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci. Můžete také provést akce pro uzel, jako je například vytvoření nové kolekce ze seznamu.


## <a name="deploy-microsoft-365-apps-updates"></a><a name="bkmk_update"></a> Nasazení aktualizací Microsoft 365 Apps

Pomocí následujících kroků nasaďte Microsoft 365 aktualizace aplikací pomocí Configuration Manager:

1. [Ověřte požadavky](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) na použití Configuration Manager ke správě aktualizací Microsoft 365 aplikací klienta v tématu **požadavky na používání Configuration Manager pro správu aktualizací klienta Microsoft 365 aplikace** v článku.  

2. [Nakonfigurujte body aktualizace softwaru](../get-started/configure-classifications-and-products.md) pro synchronizaci aktualizací klienta aplikace Microsoft 365. Nastavte **aktualizace** pro klasifikaci a vyberte **klienta Office 365** pro daný produkt. Synchronizace aktualizací softwaru po nakonfigurování bodů aktualizace softwaru na používání klasifikace **aktualizací**
3. Umožňuje klientům Microsoft 365 aplikací přijímat aktualizace od Configuration Manager. K povolení klienta použijte Configuration Manager nastavení klienta nebo zásady skupiny.

    **Metoda 1**: od verze Configuration Manager 1606 můžete použít nastavení klienta Configuration Manager ke správě agenta Microsoft 365 aplikací klienta. Když nakonfigurujete toto nastavení a nasadíte aktualizace Microsoft 365ch aplikací, klientský Agent Configuration Manager komunikuje s klientským agentem Microsoft 365 Apps ke stažení aktualizací z distribučního bodu a jejich instalaci. Configuration Manager převezme inventář nastavení klienta Microsoft 365 aplikace.    

      1. V konzole Configuration Manager klikněte na **Správa**  >  **Přehled**  >  **nastavení klienta**.  

      2. Otevřete příslušné nastavení zařízení a povolte agenta klienta. Další informace o výchozích a vlastních nastaveních klienta najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

      3. Klikněte na možnost **aktualizace softwaru** a u nastavení **Povolit správu klientského agenta systému Office 365** vyberte **Ano** .  

    **Metoda 2**:  [Povolení klientům Microsoft 365ch aplikací přijímat aktualizace](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) z Configuration Manager pomocí nástroje pro nasazení Office nebo zásady skupiny.  

4. [Nasaďte aktualizace aplikací Microsoft 365](deploy-software-updates.md) do klientů.

> [!NOTE]  
>
> Pokud byly aplikace Microsoft 365 nainstalovány v poslední době a v závislosti na tom, jak byla nainstalována, je možné, že kanál aktualizace ještě nebyl nastaven. V takovém případě budou nasazené aktualizace zjištěny jako nepoužitelné. Při instalaci Microsoft 365 aplikací se vytvořila [úloha naplánované automatické aktualizace](/deployoffice/overview-of-the-update-process-for-office-365-proplus) . V takovém případě je potřeba tuto úlohu aspoň jednou spustit, aby se nastavil kanál aktualizací a aktualizace se zjistily jako použitelné.
>
> Pokud se v poslední době nainstalovaly aplikace Microsoft 365 a nezjistily se nasazené aktualizace, můžete pro účely testování spustit úlohu automatické aktualizace Office ručně a pak na klientovi spustit [cyklus hodnocení nasazení aktualizací softwaru](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) . Pokyny k tomu, jak to provést v pořadí úkolů, najdete v tématu [aktualizace Microsoft 365Ch aplikací v pořadí úkolů](manage-office-365-proplus-updates.md#bkmk_ts).

## <a name="restart-behavior-and-client-notifications-for-microsoft-365-apps-updates"></a>Chování při restartování a oznámení klientů pro aktualizace aplikací Microsoft 365
Když nasadíte aktualizaci klienta Microsoft 365 Apps, chování při restartování a oznámení klienta se liší v závislosti na verzi Configuration Manager. Následující tabulka poskytuje informace o činnostech koncového uživatele, když klient obdrží aktualizaci Microsoft 365 Apps:

|Verze Configuration Manager |Prostředí koncového uživatele|  
|----------------|---------------------|
|1706, 1710|Klient obdrží automaticky otevíraná okna a oznámení v aplikaci a také dialogové okno odpočítávání před instalací aktualizace.|
|1802| Klient obdrží automaticky otevíraná okna a oznámení v aplikaci a také dialogové okno odpočítávání před instalací aktualizace. </br>Pokud během vynucení aktualizace klienta běží nějaké aplikace Microsoft 365, Microsoft 365 aplikace nebudou nuceně ukončeny. Místo toho se instalace aktualizace vrátí jako požadavek na restartování systému. <!--510006-->|


> [!Important]
>
>V Configuration Manager verze 1706 si všimněte následujících podrobností:
>
>- Ikona oznámení se zobrazí v oznamovací oblasti na hlavním panelu pro požadované aplikace, jejichž konečný termín je mezi 48 hodinami v budoucnosti a stažením obsahu aktualizace. 
>- Dialog pro odpočítávání se zobrazí u požadovaných aplikací, u kterých je konečný termín v budoucnosti 7,5 hodin a aktualizace se stáhla. Uživatel může odložit dialog odpočítávání po dobu až třikrát před konečným termínem. Po odložení se odpočítávání znovu zobrazí po dvou hodinách. Pokud nedošlo k odložení, dojde k odpočítávání na 30 minut a aktualizace se nainstaluje, až vyprší platnost odpočítávání.
>- Místní oznámení se nemusí zobrazit, dokud uživatel neklikne na ikonu v oznamovací oblasti. Kromě toho, pokud má oznamovací oblast minimální místo, nemusí být ikona oznámení viditelná, pokud uživatel neotevře nebo nerozšíří oznamovací oblast. 
>- Dialog oznámení a odpočítávání by se mohl spustit, když uživatel na zařízení aktivně nepracuje. Například když je zařízení zamknuté přes noc, Microsoft 365 můžou být aplikace běžící na zařízení nuceně ukončené, aby se nainstalovala aktualizace. Před zavřením aplikace Office uloží data aplikace, aby nedošlo ke ztrátě dat. 
>- Pokud je konečný termín v minulosti nebo nakonfigurovaný tak, aby začal co nejdříve, spuštění Microsoft 365ch aplikací může být vynucené zavřít bez oznámení. 
>- Pokud uživatel nainstaluje aktualizaci Microsoft 365 Apps před konečný termín, Configuration Manager ověří, zda je aktualizace nainstalována po dosažení konečného termínu. Pokud aktualizace není v zařízení zjištěna, je nainstalována aktualizace. 
>- Na aplikaci, která je spuštěná před stažením aktualizace, se nezobrazí panel oznámení v aplikaci. Po stažení aktualizace se v oznámení v aplikaci zobrazí jenom nově otevřené aplikace.
>- V případě aktualizací Microsoft 365 aplikací aktivovaných oknem služby nebo v době nepracovních hodin je možné, že běžící aplikace Office mohou být nuceně ukončeny, aby se aktualizace nainstalovaly bez oznámení. 
>- Další informace najdete v tématu [oznámení o aktualizacích koncových uživatelů pro aplikace Microsoft 365](/deployoffice/end-user-update-notifications-microsoft-365-apps) .


## <a name="add-languages-for-microsoft-365-apps-update-downloads"></a><a name="bkmk_o365_lang"></a> Přidat jazyky pro stažení aktualizací Microsoft 365 Apps
Můžete přidat podporu pro Configuration Manager ke stažení aktualizací pro všechny jazyky, které aplikace Microsoft 365 podporuje.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Stažení aktualizací pro další jazyky ve verzi 1902
<!--3555955-->

Počínaje verzí 1902 Configuration Manager pracovní postup aktualizace odděluje 38 jazyky pro **web Windows Update** z mnoha dalších jazyků pro **aktualizaci klienta Office 365**.

Chcete-li vybrat nezbytné jazyky, použijte stránku **Výběr jazyka** v následujících umístěních:
- Průvodce vytvořením pravidla automatického nasazení
- Průvodce nasazením aktualizací softwaru
- Průvodce stažením aktualizací softwaru
- Vlastnosti pravidla automatického nasazení

Na stránce **Výběr jazyka** vyberte **aktualizace klienta Office 365**a pak klikněte na **Upravit**. Přidejte potřebné jazyky pro aplikace Microsoft 365 a pak klikněte na tlačítko **OK**.

![Snímek obrazovky s přidáním dalších jazyků pro aplikace Microsoft 365](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Přidání podpory pro stažení aktualizací pro další jazyky verze 1810 a starší

Následující postup použijte v bodě aktualizace softwaru v lokalitě centrální správy nebo v samostatné primární lokalitě.

> [!IMPORTANT]  
> Konfigurace dalších jazyků aktualizace Microsoft 365 Apps je nastavení pro celá lokalita. Po přidání jazyků pomocí následujícího postupu se všechny aktualizace Microsoft 365 Apps stáhnou v těchto jazycích a jazyky, které vyberete na stránce **Výběr jazyka** v průvodci stáhnout aktualizace softwaru nebo nasadit Průvodce aktualizacemi softwaru.

1. Na příkazovém řádku zadejte program *WBEMTest* jako administrativní uživatel a otevřete rozhraní WMI (Windows Management Instrumentation) Tester.
2. Klikněte na **připojit**a zadejte *root\sms\ site_ &lt; siteCode &gt; *.
3. Klikněte na možnost **dotaz**a poté spusťte následující dotaz: *vyberte &#42; z SMS_SCI_Component, kde "Component" = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Dotaz rozhraní WMI](../media/1-wmiquery.png)
4. V podokně výsledků dvakrát klikněte na objekt s kódem lokality pro lokalitu centrální správy nebo samostatnou primární lokalitu.
5. Vyberte vlastnost **props** , klikněte na **Upravit vlastnost**a pak klikněte na **Zobrazit vložené**.
   ![Editor vlastností](../media/2-propeditor.png)
6. Počínaje prvním výsledkem dotazu otevřete všechny objekty, dokud nenajdete objekt s **AdditionalUpdateLanguagesForO365** pro vlastnost **PropertyName** .
7. Vyberte **hodnota2** a klikněte na **Upravit vlastnost**.  
   ![Úprava vlastnosti hodnota2](../media/3-queryresult.png)
8. Přidejte další jazyky do vlastnosti **hodnota2** a klikněte na **Uložit vlastnost**. <br/> Například pt-PT (pro portugalštinu-Portugalsko), AF-za (pro Afrikánština-Jižní Afrika), NN-No (pro norštinu (nynorsk) – Norsko) atd. Měli byste zadat `pt-pt,af-za,nn-no` ukázkové jazyky. Nepoužívejte mezery mezi jazyky.
 
   ![Přidat jazyky v editoru vlastností](../media/4-props.png)  
9. Klikněte na tlačítko **Zavřít**, klikněte na tlačítko **Zavřít**, klikněte na tlačítko **Uložit vlastnost**a klikněte na **Uložit objekt** (Pokud kliknete na tlačítko **Zavřít** , hodnoty se zahodí). Klikněte na **Zavřít**a pak kliknutím na **konec** ukončete rozhraní WMI (Windows Management Instrumentation) Tester.
10. V konzole Configuration Manager klikněte na přehled **knihovny softwaru**  >  **Overview**  >  **Office 365 aktualizace pro správu klientů**  >  **sady Office 365**.
11. Když teď stáhnete aktualizace aplikací Microsoft 365, aktualizace se stáhnou v jazycích, které jste vybrali v průvodci a nakonfigurovali v tomto postupu. Chcete-li ověřit, zda jsou aktualizace staženy ve správných jazycích, pro aktualizaci použijte zdroj balíčku a vyhledejte soubory s kódem jazyka v názvu souboru.  
    ![Názvy souborů s dalšími jazyky](../media/5-verification.png)

## <a name="updating-microsoft-365-apps-in-a-task-sequence"></a><a name="bkmk_ts"></a> Aktualizace aplikací Microsoft 365 v pořadí úkolů
Při instalaci aktualizací Microsoft 365 aplikací pomocí kroku pořadí úkolů [instalovat aktualizace softwaru](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) je možné, že nasazené aktualizace budou zjištěny jako nedostupné.  K tomu může dojít v případě, že se naplánovaná úloha automatických aktualizací Office nespouštěla aspoň jednou (podívejte se na poznámku v tématu [nasazení aktualizací Microsoft 365 Apps](manage-office-365-proplus-updates.md#bkmk_update)). K tomu může dojít například v případě, že Microsoft 365 aplikace byly nainstalovány těsně před spuštěním tohoto kroku.

Chcete-li zajistit, aby byl kanál aktualizací nastaven tak, aby byly nasazené aktualizace správně zjištěny, použijte jednu z následujících metod:

**Metoda 1:**
1. V počítači se stejnou verzí aplikace Microsoft 365 otevřete Plánovač úloh (Taskschd. msc) a Identifikujte úlohu automatické aktualizace Microsoft 365 aplikací. Obvykle se nachází v části **Plánovač úloh Library**  > **Microsoft** > **Office**.
2. Klikněte pravým tlačítkem na úlohu automatické aktualizace a vyberte **vlastnosti**.
3. Přejděte na kartu **Akce** a klikněte na **Upravit**. Zkopírujte příkaz a všechny argumenty. 
4. V konzole Configuration Manager upravte pořadí úkolů.
5. Přidejte nový krok **Spustit příkazový řádek** před krok **instalovat aktualizace softwaru** v pořadí úkolů. Pokud jsou aplikace Microsoft 365 nainstalovány jako součást stejného pořadí úloh, zajistěte, aby tento krok běžel po instalaci Office.
6. Zkopírujte příkaz a argumenty, které jste shromáždili z naplánované úlohy automatických aktualizací pro Office. 
7. Klikněte na **OK**. 

**Metoda 2:**
1. V počítači se stejnou verzí aplikace Microsoft 365 otevřete Plánovač úloh (Taskschd. msc) a Identifikujte úlohu automatické aktualizace Microsoft 365 aplikací. Obvykle se nachází v části **Plánovač úloh Library**  > **Microsoft** > **Office**.
2. V konzole Configuration Manager upravte pořadí úkolů.
3. Přidejte nový krok **Spustit příkazový řádek** před krok **instalovat aktualizace softwaru** v pořadí úkolů. Pokud jsou aplikace Microsoft 365 nainstalovány jako součást stejného pořadí úloh, zajistěte, aby tento krok běžel po instalaci Office.
4. Do pole Příkazový řádek zadejte příkazový řádek, který spustí naplánovanou úlohu. Níže uvedený příklad zajistí, že řetězec v uvozovkách odpovídá cestě a názvu úlohy identifikované v kroku 1.  

    Příklad: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Klikněte na **OK**. 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a> Aktualizace kanálů pro aplikace Microsoft 365
<!--6298093-->
Až se sada Office 365 ProPlus přejmenovala na **Microsoft 365 aplikace pro podniky**, přejmenují se i kanály aktualizací. Pokud k nasazení aktualizací použijete pravidlo automatického nasazení (ADR), budete muset provést změny v pravidla automatického nasazení, pokud se spoléhají na vlastnost **title** . Důvodem je, že se mění název balíčků aktualizací v katalogu Microsoft Update.

V současné době název balíčku aktualizací pro Office 365 ProPlus začíná "aktualizace klienta Office 365", jak je vidět v následujícím příkladu:

&nbsp;&nbsp;Aktualizace klienta Office 365 – půlroční kanál verze 1908 pro edici x64 (Build 11929,20648)

V případě balíčků aktualizací vydaných v systémech a po 9. června začíná nadpisem "Microsoft 365 Apps Update", jak je vidět v následujícím příkladu:

&nbsp;&nbsp;Aktualizace Microsoft 365 Apps – půlroční kanál verze 1908 pro edici x64 (Build 11929,50000)
</br>
</br>

|Název nového kanálu|Název předchozího kanálu|
|--|--|
|Půlroční podnikový kanál|Půlroční kanál|
|Půlroční podnikový kanál (Preview)|Půlroční kanál (vybraní uživatelé)|
|Měsíční podnikový kanál|Není k dispozici|
|Aktuální kanál|Měsíční kanál|
|Aktuální kanál (Preview)|Měsíční kanál (cílený)|
|Beta kanál|Obchodování|

Další informace o tom, jak upravit pravidla automatického nasazení, najdete v tématu věnovaném [automatickému nasazování aktualizací softwaru](automatically-deploy-software-updates.md). Další informace o změně názvu najdete v tématu [Změna názvu pro Office 365 ProPlus](/deployoffice/name-change).


## <a name="change-the-update-channel-after-you-enable-microsoft-365-apps-clients-to-receive-updates-from-configuration-manager"></a>Pokud povolíte klientům Microsoft 365 aplikací příjem aktualizací z Configuration Manager, změňte kanál pro aktualizaci.

Po nasazení Microsoft 365 aplikací můžete změnit kanál aktualizace pomocí Zásady skupiny nebo nástroje pro nasazení Office (ODT). Můžete například přesunout zařízení z pololetního kanálu na půlroční kanál (cílený). Při změně kanálu se Office aktualizuje automaticky bez nutnosti přeinstalovat nebo stáhnout plnou verzi. Další informace najdete v tématu [Změna kanálu aktualizace Microsoft 365 Apps pro zařízení ve vaší organizaci](//deployoffice/change-update-channels).


## <a name="next-steps"></a>Další kroky

Pomocí řídicího panelu pro správu klientů Office 365 v Configuration Manager zkontrolujte informace o klientovi Microsoft 365 aplikace a nasaďte Microsoft 365 aplikace. Další informace najdete v tématu [řídicí panel pro správu klientů Office 365](office-365-dashboard.md).