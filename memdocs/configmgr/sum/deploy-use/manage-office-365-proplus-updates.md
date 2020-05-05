---
title: Správa aktualizací Office 365 ProPlus
titleSuffix: Configuration Manager
description: Configuration Manager synchronizuje aktualizace klientů Office 365 z katalogu služby WSUS do serveru lokality, aby byly aktualizace k dispozici pro nasazení na klienty.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 4967b8b289d54a6355cb0a1e6454d5fac469a733
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110402"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Správa Office 365 ProPlus pomocí Configuration Manageru

*Platí pro: Configuration Manager (Current Branch)*

> [!Note]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

Configuration Manager vám umožní spravovat aplikace Office 365 ProPlus následujícími způsoby:

- [Nasazení aplikací office 365](#deploy-office-365-apps): Instalační program Office 365 můžete spustit z [řídicího panelu pro správu klientů sady Office 365](office-365-dashboard.md) a usnadnit tak počáteční prostředí pro instalaci aplikace Office 365. Průvodce umožňuje konfigurovat nastavení instalace Office 365, stahovat soubory ze sítě pro doručování obsahu (sítě CDN) pro Office a vytvářet a nasazovat aplikace skriptu s obsahem.

- [Nasazení aktualizací office 365](#deploy-office-365-updates): aktualizace klientů Office 365 můžete spravovat pomocí pracovního postupu správy softwarových aktualizací. Když Microsoft zveřejňuje v Office Content Delivery Network (CDN) nové aktualizace klienta Office 365, publikuje také balíček aktualizací ve službě WSUS (Windows Server Update Services). Jakmile Configuration Manager synchronizuje aktualizaci klienta Office 365 z katalogu služby WSUS na server lokality, bude aktualizace k dispozici pro nasazení na klienty.

   > [!NOTE]
   > Od verze Configuration Manager 2002 můžete importovat aktualizace sady Office 365 do odpojených prostředí. Další informace najdete v tématu [synchronizace aktualizací Office 365 z odpojeného bodu aktualizace softwaru](../get-started/synchronize-office-updates-disconnected.md).   

- [Přidat jazyky pro stažení aktualizací pro Office 365](#bkmk_o365_lang): můžete přidat podporu pro Configuration Manager ke stažení aktualizací pro všechny jazyky, které sada Office 365 podporuje. To znamená, že Configuration Manager nemusí podporovat jazyk, pokud je to sada Office 365. Před Configuration Manager verze 1610 musíte stáhnout a nasadit aktualizace ve stejných jazycích nakonfigurovaných na klientech Office 365.

- [Změna kanálu aktualizace](#bkmk_channel): k distribuci hodnoty klíče registru do klientů Office 365 můžete použít zásady skupiny a změnit tak kanál aktualizací.

Chcete-li zkontrolovat informace o klientech Office 365 a spustit některé z těchto akcí správy sady Office 365, použijte [řídicí panel Správa klientů nástroje office 365](office-365-dashboard.md).

## <a name="deploy-office-365-apps"></a>Nasazení aplikací Office 365  
Spusťte instalační program Office 365 z řídicího panelu pro správu klientů Office 365 pro úvodní instalaci aplikace Office 365. Průvodce umožňuje konfigurovat nastavení instalace Office 365, stahovat soubory ze sítě pro doručování obsahu (sítě CDN) pro Office a vytvářet a nasazovat aplikace skriptu pro soubory. Až do chvíle, kdy je Office 365 nainstalovaný na klientech a spustí se [úloha funkce Automatické aktualizace Office](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) , aktualizace Office 365 se nepoužijí. Pro účely testování můžete spustit úlohu aktualizace ručně.

Pro předchozí verze Configuration Manager musíte provést následující kroky a nainstalovat aplikace Office 365 poprvé na klienty:
- Stáhnout nástroj pro nasazení Office 365 (ODT)
- Stáhněte zdrojové instalační soubory sady Office 365, včetně všech jazykových sad, které potřebujete.
- Vygenerujte soubor Configuration. XML, který určuje správnou verzi a kanál Office.
- Vytvořte a nasaďte starší balíček nebo aplikaci skriptu pro klienty, kteří budou instalovat aplikace Office 365.

### <a name="requirements"></a>Požadavky
- Počítač, který spouští instalační program sady Office 365, musí mít přístup k Internetu.  
- Uživatel, který spouští instalační program sady Office 365, musí mít oprávnění **ke čtení** a **zápisu** pro sdílenou složku umístění obsahu, která je k dispozici v průvodci.
- Pokud se zobrazí chyba stahování 404, zkopírujte následující soubory do složky uživatele% Temp%:
  - [releasehistory. XML](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit. XML](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Nasaďte aplikace Office 365 pomocí Configuration Manager verze 1806 nebo vyšší: 
Od verze Configuration Manager 1806 se nástroj pro přizpůsobení sady Office integruje s instalačním programem sady Office 365 v konzole Configuration Manager. Při vytváření nasazení pro Office 365 můžete dynamicky konfigurovat nejnovější nastavení spravovatelnosti Office. <!--1358149-->

1. V konzole Configuration Manager přejděte do části > **Přehled** >  **knihovny softwaru****Office 365 Správa klientů**.
2. V pravém horním podokně klikněte na **instalační program Office 365** . Otevře se Průvodce instalací klienta sady Office 365.
3. Na stránce **nastavení aplikace** zadejte název a popis aplikace, zadejte umístění pro stažení souborů a potom klikněte na tlačítko **Další**. Umístění musí být zadané jako &#92;&#92;*server*&#92;*Shared*.
4. Na stránce **Nastavení Office** klikněte na **Přejít k nástroji pro přizpůsobení Office**. Otevře se [Nástroj pro přizpůsobení Office pro kliknutí na spuštění](https://config.office.com).
5. Nakonfigurujte požadovaná nastavení pro instalaci sady Office 365. Po dokončení konfigurace klikněte na **Odeslat** v pravém horním rohu stránky. 
6. Na stránce **nasazení** určete, zda chcete nasadit nyní nebo později. Pokud se rozhodnete k nasazení později, můžete aplikaci najít v**aplikacích** > **pro správu** > aplikací v **knihovně softwaru**.  
7. Potvrďte nastavení na stránce **Souhrn** . 
8. Klikněte na tlačítko **Další** a po dokončení Průvodce instalací klienta sady Office 365 klikněte na tlačítko **Zavřít** . 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Nasaďte aplikace Office 365 pomocí Configuration Manager verze 1802 a předchozí:

1. V konzole Configuration Manager přejděte do části > **Přehled** >  **knihovny softwaru****Office 365 Správa klientů**.
2. V pravém horním podokně klikněte na **instalační program Office 365** . Otevře se Průvodce instalací klienta sady Office 365.
3. Na stránce **nastavení aplikace** zadejte název a popis aplikace, zadejte umístění pro stažení souborů a potom klikněte na tlačítko **Další**. Umístění musí být zadané jako &#92;&#92;*server*&#92;*Shared*.
4. Na stránce **importovat nastavení klienta** vyberte, zda chcete importovat nastavení klienta sady Office 365 z existujícího konfiguračního souboru XML nebo ručně zadat nastavení. Až budete hotovi, klikněte na **Další** .  

    Pokud máte existující konfigurační soubor, zadejte umístění souboru a přejděte ke kroku 7. Je nutné zadat umístění ve formuláři &#92;&#92;*server*&#92;*sdílet*&#92;*filename*. XML.
    > [!IMPORTANT]    
    > Konfigurační soubor XML musí obsahovat jenom [jazyky, které podporuje klient Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Na stránce **klientské produkty** vyberte sadu Office 365, kterou používáte. Vyberte aplikace, které chcete zahrnout. Vyberte všechny další produkty Office, které by měly být zahrnuty, a potom klikněte na tlačítko **Další**.
6. Na stránce **nastavení klienta** vyberte nastavení, které chcete zahrnout, a potom klikněte na tlačítko **Další**.
7. Na stránce **nasazení** vyberte, zda chcete aplikaci nasadit, a poté klikněte na tlačítko **Další**. <br/>Pokud se rozhodnete nenasadit balíček v průvodci, přejděte ke kroku 9.
8. Nakonfigurujte zbývající stránky průvodce jako při typickém nasazení aplikace. Podrobnosti najdete v tématu [Vytvoření a nasazení aplikace](../../apps/get-started/create-and-deploy-an-application.md).
9. Dokončete průvodce.
10. Můžete nasadit nebo upravit aplikaci z **knihovny** > **Přehled** > **aplikací****pro správu** > aplikací.    

Po vytvoření a nasazení aplikací Office 365 pomocí instalačního programu sady Office 365 nebude Configuration Manager ve výchozím nastavení spravovat aktualizace sady Office. Pokud chcete, aby klienti Office 365 dostávali aktualizace z Configuration Manager, přečtěte si téma [nasazení aktualizací Office 365 pomocí Configuration Manager](#deploy-office-365-updates).

Po nasazení aplikací Office 365 můžete vytvořit pravidla automatického nasazení, která budou aplikace spravovat. Pokud chcete vytvořit pravidlo automatického nasazení pro aplikace Office 365, klikněte na **vytvořit** pravidlo automatického nasazení z [řídicího panelu pro správu klientů Office 365](office-365-dashboard.md). Když vyberete produkt, vyberte **klienta Office 365** . Další informace najdete v tématu [automatické nasazení aktualizací softwaru](automatically-deploy-software-updates.md).


## <a name="drill-through-required-office-365-updates"></a>Podrobné informace o požadovaných aktualizacích Office 365
<!--4224414-->
*(Představené ve verzi 1906)*

Můžete procházet statistiky dodržování předpisů a zjistit, která zařízení vyžadují konkrétní aktualizaci softwaru Office 365. Chcete-li zobrazit seznam zařízení, potřebujete oprávnění k zobrazení aktualizací a kolekcí, do kterých zařízení patří. Přechod k podrobnostem v seznamu zařízení:

1. Přejít na **Software Library** > **Office 365 Update Management** > **Office 365 Updates**.
1. Vyberte jakoukoli aktualizaci, kterou vyžaduje aspoň jedno zařízení.
1. Podívejte se na kartu **Souhrn** a v části **Statistika**Najděte výsečový graf.
1. Pokud chcete přejít k podrobnostem seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu.
1. Tato akce přejde na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci. Můžete také provést akce pro uzel, jako je například vytvoření nové kolekce ze seznamu.


## <a name="deploy-office-365-updates"></a>Nasazení aktualizací Office 365

Pomocí následujících kroků nasaďte aktualizace Office 365 s Configuration Manager:

1. [Ověřte požadavky](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) na použití Configuration Manager ke správě aktualizací klientů Office 365 v tématu **požadavky pro použití Configuration Manager ke správě aktualizací klienta sady Office 365** v článku.  

2. [Konfigurace bodů aktualizace softwaru](../get-started/configure-classifications-and-products.md) pro synchronizaci aktualizací klienta Office 365. Nastavte **aktualizace** pro klasifikaci a vyberte **klienta Office 365** pro daný produkt. Synchronizace aktualizací softwaru po nakonfigurování bodů aktualizace softwaru na používání klasifikace **aktualizací**
3. Povolit klientům Office 365 příjem aktualizací z Configuration Manager. K povolení klienta použijte Configuration Manager nastavení klienta nebo zásady skupiny.

    **Metoda 1**: od verze Configuration Manager 1606 můžete použít nastavení klienta Configuration Manager ke správě klientského agenta Office 365. Po nakonfigurování tohoto nastavení a nasazení aktualizací Office 365 komunikuje klientský Agent Configuration Manager s agentem klienta Office 365 ke stažení aktualizací z distribučního bodu a jejich instalaci. Configuration Manager využívá inventarizaci nastavení klienta Office 365 ProPlus.    

      1. V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **nastavení klienta**.  

      2. Otevřete příslušné nastavení zařízení a povolte agenta klienta. Další informace o výchozích a vlastních nastaveních klienta najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

      3. Klikněte na možnost **aktualizace softwaru** a u nastavení **Povolit správu klientského agenta systému Office 365** vyberte **Ano** .  

    **Metoda 2**: [povolení klientům Office 365 přijímat aktualizace](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) z Configuration Manager pomocí nástroje pro nasazení Office nebo zásady skupiny.  

4. [Nasaďte aktualizace Office 365](deploy-software-updates.md) na klienty.

> [!Important]
> - Configuration Manager počínaje verzí 1706 se aktualizace klienta sady Office 365 přesunuly do uzlu aktualizace sady Office 365 pro 365 **správu** >klientů**aktualizace** sady Office. Tento přesun nebude mít vliv na aktuální konfiguraci služby ADR. 
> - Před Configuration Manager verze 1610 musíte stáhnout a nasadit aktualizace ve stejných jazycích nakonfigurovaných na klientech Office 365. Řekněme například, že máte klienta Office 365 nakonfigurovaný s jazyky en-US a de-de. Na serveru lokality stahujete a nasadíte jenom obsah en-US pro příslušnou aktualizaci Office 365. Když uživatel spustí instalaci z centra softwaru pro tuto aktualizaci, aktualizace přestane při stahování obsahu pro de-de. 

> [!NOTE]  
>
> Pokud byla sada Office 365 ProPlus v poslední době nainstalována a v závislosti na tom, jak byla nainstalována, je možné, že kanál aktualizace ještě nebyl nastaven. V takovém případě budou nasazené aktualizace zjištěny jako nepoužitelné. Při instalaci Office 365 ProPlus se vytvoří [úloha naplánované automatické aktualizace](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) . V takovém případě je potřeba tuto úlohu aspoň jednou spustit, aby se nastavil kanál aktualizací a aktualizace se zjistily jako použitelné.
>
> Pokud jste nainstalovali sadu Office 365 ProPlus v poslední době a nasazené aktualizace se nezjistily, můžete pro účely testování spustit úlohu automatické aktualizace Office ručně a pak na klientovi spustit [cyklus hodnocení nasazení aktualizací softwaru](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) . Pokyny k tomu, jak to provést v pořadí úkolů, najdete v tématu [aktualizace sady Office 365 ProPlus v pořadí úkolů](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence).

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Chování při restartování a oznámení klientů pro aktualizace Office 365
Když nasadíte aktualizaci na klienta Office 365, chování při restartování a oznámení klienta se liší v závislosti na verzi Configuration Manager. Následující tabulka poskytuje informace o činnostech koncového uživatele, když klient obdrží aktualizaci Office 365:

|Verze Configuration Manager |Prostředí koncového uživatele|  
|----------------|---------------------|
|1706, 1710|Klient obdrží automaticky otevíraná okna a oznámení v aplikaci a také dialogové okno odpočítávání před instalací aktualizace.|
|1802| Klient obdrží automaticky otevíraná okna a oznámení v aplikaci a také dialogové okno odpočítávání před instalací aktualizace. </br>Pokud se během vynucení aktualizace klienta Office 365 spustí nějaké aplikace Office 365, aplikace Office se nenuceně zavřou. Místo toho se instalace aktualizace vrátí jako požadavek na restartování systému. <!--510006-->|


> [!Important]
>
>V Configuration Manager verze 1706 si všimněte následujících podrobností:
>
>- Ikona oznámení se zobrazí v oznamovací oblasti na hlavním panelu pro požadované aplikace, jejichž konečný termín je mezi 48 hodinami v budoucnosti a stažením obsahu aktualizace. 
>- Dialog pro odpočítávání se zobrazí u požadovaných aplikací, u kterých je konečný termín v budoucnosti 7,5 hodin a aktualizace se stáhla. Uživatel může odložit dialog odpočítávání po dobu až třikrát před konečným termínem. Po odložení se odpočítávání znovu zobrazí po dvou hodinách. Pokud nedošlo k odložení, dojde k odpočítávání na 30 minut a aktualizace se nainstaluje, až vyprší platnost odpočítávání.
>- Místní oznámení se nemusí zobrazit, dokud uživatel neklikne na ikonu v oznamovací oblasti. Kromě toho, pokud má oznamovací oblast minimální místo, nemusí být ikona oznámení viditelná, pokud uživatel neotevře nebo nerozšíří oznamovací oblast. 
>- Dialog oznámení a odpočítávání by se mohl spustit, když uživatel na zařízení aktivně nepracuje. Například když je zařízení uzamčené přes noc, může být vynucená instalace aplikací Office, které běží na zařízení, ukončit, aby se nainstalovala aktualizace. Před zavřením aplikace Office uloží data aplikace, aby nedošlo ke ztrátě dat. 
>- Pokud je konečný termín v minulosti nebo nakonfigurovaný tak, aby začal co nejdříve, můžou se spuštěné aplikace Office nuceně zavřít bez oznámení. 
>- Pokud uživatel před konečným termínem nainstaluje aktualizaci Office, Configuration Manager ověří, že je aktualizace nainstalovaná po dosažení konečného termínu. Pokud aktualizace není v zařízení zjištěna, je nainstalována aktualizace. 
>- Oznamovací panel v aplikaci se nezobrazí v aplikaci Office, která je spuštěná před stažením aktualizace. Po stažení aktualizace se v oznámení v aplikaci zobrazí jenom nově otevřené aplikace.
>- U aktualizací Office aktivovaných oknem služby nebo naplánovaným pro jiné než pracovní hodiny je možné, že běžící aplikace Office můžou být vynucené zavřít, aby se aktualizace nainstalovaly bez oznámení. 
>- Další informace najdete v tématu [oznámení o aktualizacích koncových uživatelů pro Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus) .


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a>Přidat jazyky pro stažení aktualizací pro Office 365
Můžete přidat podporu pro Configuration Manager ke stažení aktualizací pro všechny jazyky, které jsou podporovány sadou Office 365.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Stažení aktualizací pro další jazyky ve verzi 1902
<!--3555955-->

Počínaje verzí 1902 Configuration Manager pracovní postup aktualizace odděluje 38 jazyky pro **web Windows Update** z mnoha dalších jazyků pro **aktualizaci klienta Office 365**.

Chcete-li vybrat nezbytné jazyky, použijte stránku **Výběr jazyka** v následujících umístěních:
- Průvodce vytvořením pravidla automatického nasazení
- Průvodce nasazením aktualizací softwaru
- Průvodce stažením aktualizací softwaru
- Vlastnosti pravidla automatického nasazení

Na stránce **Výběr jazyka** vyberte **aktualizace klienta Office 365**a pak klikněte na **Upravit**. Přidejte potřebné jazyky pro Office 365 a pak klikněte na **OK**.

![Snímek obrazovky s přidáním dalších jazyků pro Office 365](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Přidání podpory pro stažení aktualizací pro další jazyky verze 1810 a starší

Následující postup použijte v bodě aktualizace softwaru v lokalitě centrální správy nebo v samostatné primární lokalitě.

> [!IMPORTANT]  
> Konfigurace dalších jazyků aktualizace Office 365 je nastavení pro celá lokalita. Po přidání jazyků pomocí následujícího postupu jsou všechny aktualizace sady Office 365 staženy v těchto jazycích a jazyky, které vyberete na stránce **Výběr jazyka** v průvodci stáhnout aktualizace softwaru nebo nasadit Průvodce aktualizacemi softwaru.

1. Na příkazovém řádku zadejte program *WBEMTest* jako administrativní uživatel a otevřete rozhraní WMI (Windows Management Instrumentation) Tester.
2. Klikněte na **připojit**a zadejte *root\sms\ site_&lt;siteCode&gt;*.
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
10. V konzole Configuration Manager klikněte na > **Přehled** >  **knihovny softwaru****Office 365 aktualizace pro správu** > klientů**sady Office 365**.
11. Když teď stáhnete aktualizace Office 365, stáhnou se aktualizace v jazycích, které jste vybrali v průvodci a nakonfigurovali v tomto postupu. Chcete-li ověřit, zda jsou aktualizace staženy ve správných jazycích, pro aktualizaci použijte zdroj balíčku a vyhledejte soubory s kódem jazyka v názvu souboru.  
    ![Názvy souborů s dalšími jazyky](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>Aktualizace Office 365 ProPlus v pořadí úkolů
Při instalaci aktualizací Office 365 pomocí kroku pořadí úkolů [instalovat aktualizace softwaru](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) je možné, že nasazené aktualizace budou zjištěny jako nedostupné.  K tomu může dojít v případě, že se naplánovaná úloha automatické aktualizace Office nespouštěla aspoň jednou (podívejte se na poznámku v tématu [nasazení aktualizací Office 365](manage-office-365-proplus-updates.md#deploy-office-365-updates)). K tomu může dojít například v případě, že sada Office 365 ProPlus byla nainstalována těsně před spuštěním tohoto kroku.

Chcete-li zajistit, aby byl kanál aktualizací nastaven tak, aby byly nasazené aktualizace správně zjištěny, použijte jednu z následujících metod:

**Metoda 1:**
1. V počítači se stejnou verzí Office 365 ProPlus otevřete Plánovač úloh (Taskschd. msc) a Identifikujte úlohu automatické aktualizace Office 365. Obvykle se nachází v části **Plánovač úloh Library** >**Microsoft**>**Office**.
2. Klikněte pravým tlačítkem na úlohu automatické aktualizace a vyberte **vlastnosti**.
3. Přejděte na kartu **Akce** a klikněte na **Upravit**. Zkopírujte příkaz a všechny argumenty. 
4. V konzole Configuration Manager upravte pořadí úkolů.
5. Přidejte nový krok **Spustit příkazový řádek** před krok **instalovat aktualizace softwaru** v pořadí úkolů. Pokud je sada Office 365 ProPlus nainstalována jako součást stejného pořadí úloh, zajistěte, aby tento krok běžel po instalaci sady Office.
6. Zkopírujte příkaz a argumenty, které jste shromáždili z naplánované úlohy automatických aktualizací pro Office. 
7. Klikněte na tlačítko **OK**. 

**Metoda 2:**
1. V počítači se stejnou verzí Office 365 ProPlus otevřete Plánovač úloh (Taskschd. msc) a Identifikujte úlohu automatické aktualizace Office 365. Obvykle se nachází v části **Plánovač úloh Library** >**Microsoft**>**Office**.
2. V konzole Configuration Manager upravte pořadí úkolů.
3. Přidejte nový krok **Spustit příkazový řádek** před krok **instalovat aktualizace softwaru** v pořadí úkolů. Pokud je sada Office 365 ProPlus nainstalována jako součást stejného pořadí úloh, zajistěte, aby tento krok běžel po instalaci sady Office.
4. Do pole Příkazový řádek zadejte příkazový řádek, který spustí naplánovanou úlohu. Níže uvedený příklad zajistí, že řetězec v uvozovkách odpovídá cestě a názvu úlohy identifikované v kroku 1.  

    Příklad: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Klikněte na tlačítko **OK**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a><a name="bkmk_channel"></a>Pokud chcete, aby klienti Office 365 dostávali aktualizace z Configuration Manager, změňte kanál pro aktualizaci.

Po nasazení Office 365 ProPlus můžete změnit kanál aktualizace pomocí Zásady skupiny nebo nástroje pro nasazení Office (ODT). Můžete například přesunout zařízení z pololetního kanálu na půlroční kanál (cílený). Při změně kanálu se Office aktualizuje automaticky bez nutnosti přeinstalovat nebo stáhnout plnou verzi. Další informace najdete v tématu [Změna kanálu aktualizace Office 365 ProPlus pro zařízení ve vaší organizaci](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Další kroky

Pomocí řídicího panelu pro správu klientů Office 365 v Configuration Manager zkontrolujte informace o klientovi Office 365 a nasaďte aplikace Office 365. Další informace najdete v tématu [řídicí panel pro správu klientů Office 365](office-365-dashboard.md).
