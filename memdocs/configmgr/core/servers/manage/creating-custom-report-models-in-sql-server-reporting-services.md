---
title: Vytváření vlastních sestav
titleSuffix: Configuration Manager
description: Definujte modely sestav tak, aby splňovaly vaše podnikové požadavky, a potom modely sestav nasaďte do Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: fe570eeedc2c050bdaf27903d30ddffff63109d9
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879151"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>Vytváření vlastních modelů sestav pro Configuration Manager v SQL Server Reporting Services

*Platí pro: Configuration Manager (Current Branch)*

Modely vzorových sestav jsou součástí Configuration Manager, ale můžete také definovat modely sestav pro splnění vlastních podnikových požadavků a pak nasadit model sestavy, který se Configuration Manager, aby se použil při vytváření nových sestav založených na modelu. Následující tabulka obsahuje postup pro vytvoření a nasazení základního modelu sestavy.  

> [!NOTE]  
>  Postup pro vytvoření pokročilejšího modelu sestavy naleznete v části [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) tohoto tématu.  

|Krok|Description|Další informace|  
|----------|-----------------|----------------------|  
|Ověřte, zda je nainstalován nástroj SQL Server Business Intelligence Development Studio|Modely sestav jsou navrženy a sestaveny pomocí tohoto nástroje SQL Server Business Intelligence Development Studio. Ověřte, zda na počítači, na kterém vytváříte vlastní model sestavy, je nainstalován nástroj SQL Server Business Intelligence Development Studio.|Další informace o nástroji SQL Server Business Intelligence Development Studio naleznete v dokumentaci k systému SQL Server 2008.|  
|Vytvoření projektu modelu sestavy|Projekt modelu sestavy obsahuje definici zdroje dat (soubor DS), definici zobrazení zdroje dat (soubor DSV) a model sestavy (soubor SMDL).|Další informace najdete v části [To create the report model project](#BKMK_CreateReportModelProject) v tomto tématu.|  
|Definujte zdroj dat pro model sestavy|Po vytvoření projektu modelu sestavy musíte definovat jeden zdroj dat, ze kterého budete extrahovat obchodní data. Obvykle se jedná o databázi lokality Configuration Manager.|Další informace najdete v části [To define the data source for the report model](#BKMK_DefineReportModelDataSource) v tomto tématu.|  
|Definujte zobrazení zdroje dat pro model sestavy|Po definování zdrojů dat, které používáte ve vašem projektu modelu sestavy, následuje další krok, což je definování zobrazení zdroje dat pro projekt. Zobrazení zdroje dat je logický datový model vytvořený na základě jednoho nebo více datových zdrojů. Zobrazení zdrojů dat zjednodušují přístup k fyzickým objektům, jako např. tabulkám a zobrazením, které jsou součástí podkladových zdrojů dat. Služba SQL Server Reporting Services vytváří model sestavy ze zobrazení zdroje dat.<br /><br /> Zobrazení zdrojů dat usnadňují proces návrhu modelu tím, že vám poskytnou užitečné znázornění dat, která jste si definovali. Aniž byste pozměnili podkladové zdroje dat, v zobrazení zdrojů dat můžete přejmenovávat tabulky a pole a přidávat agregační pole a odvozené tabulky. Aby byl model efektivní, k zobrazení zdroje dat přidávejte pouze ty tabulky, které máte v úmyslu použít.|Další informace najdete v části [To define the data source view for the report model](#BKMK_DefineReportModelDataSourceView) v tomto tématu.|  
|Vytvoření modelu sestavy|Model sestavy je horní vrstva databáze, která identifikuje obchodní entity, pole a role. Při publikování pomocí těchto modelů uživatelé Tvůrce sestav mohou vyvinout sestavy, aniž by museli být obeznámeni s databázovými strukturami, nebo pochopit a psát dotazy. Modely sestávají ze souborů souvisejících položek sestavy, které se seskupují pod popisným názvem s předdefinovanými vztahy mezi těmito obchodními položkami a s předdefinovanými výpočty. Modely jsou definovány pomocí jazyka XML nazývaného Semantic Model Definition Language (SMDL). Přípona názvu souboru pro soubory modelu sestavy je SMDL.|Další informace najdete v části [To create the report model](#BKMK_CreateReportModel) v tomto tématu.|  
|Publikování modelu sestavy|Pro vytvoření sestavy pomocí modelu, který jste právě vytvořili, ho musíte publikovat do serveru sestav. Zdroj dat a zobrazení zdroje dat jsou při publikování součástí modelu.|Další informace najdete v části [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) v tomto tématu.|  
|Nasazení modelu sestavy do Configuration Manager|Před použitím vlastního modelu sestavy v **Průvodci vytvořením sestavy** pro vytvoření sestavy založené na modelu je nutné nasadit model sestavy, aby bylo možné Configuration Manager.|Další informace najdete v části [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) v tomto tématu.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Postup vytvoření základního modelu sestavy ve službě SQL Server Reporting Services  
 Následující postupy můžete použít k vytvoření základního modelu sestavy, který mohou uživatelé na webu použít k sestavení konkrétních sestav založených na modelu na základě dat v jednom zobrazení databáze Configuration Manager. Můžete vytvořit model sestavy, který autorovi sestavy prezentuje informace o počítačích klienta ve vaší lokalitě. Tyto informace jsou pořízeny ze zobrazení **v_R_System** v databázi Configuration Manager.  

 Na počítači, kde provádíte tyto postupy, zajistěte, aby byl nainstalován nástroj SQL Server Business Intelligence Development Studio a aby počítač byl připojen k síti serveru bodu služby Reporting Services. Podrobné informace o nástroji SQL Server Business Intelligence Development Studio naleznete v dokumentaci k systému SQL Server 2008.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a>Vytvoření projektu modelu sestavy  

1.  Na ploše klikněte na tlačítko **Start**, klikněte na **Microsoft SQL Server 2008**a pak klikněte na nástroj **SQL Server Business Intelligence Development Studio**.  

2.  Poté, co se **SQL Server Business Intelligence Development Studio** v nástroji Microsoft Visual Studio otevře, klikněte na tlačítko **Soubor**, klikněte na **Nový**a pak klikněte na **Projekt**.  

3.  V dialogovém okně **Nový projekt** vyberte v seznamu **Šablony****Projekt modelu sestavy** .  

4.  V okně **Název** zadejte název tohoto modelu sestavy. V tomto příkladu zadejte hodnotu **Jednoduchý_Model**.  

5.  Pro vytvoření projektu modelu sestavy klikněte na tlačítko **OK**.  

6.  V **Průzkumníku řešení** se zobrazí řešení **Simple_Model**.  

    > [!NOTE]  
    >  Pokud podokno **Průzkumník řešení** nevidíte, klikněte na tlačítko **Zobrazení**a pak klikněte na **Průzkumník řešení**.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a>Definování zdroje dat pro model sestavy  

1.  V podokně **Průzkumník řešení** nástroje **SQL Server Business Intelligence Development Studio**klikněte pravým tlačítkem na položku **Zdroje dat** , kde vyberete **Přidat nový zdroj dat**.  

2.  Na stránce **Vítejte v Průvodci zdroje dat** klikněte na tlačítko **Další**.  

3.  Na stránce **Vyberte, jak definovat připojení** ověřte, zda je vybrána položka **Vytvořit zdroj dat na základě stávajícího nebo nového připojení** a pak klikněte na tlačítko **Nový**.  

4.  V dialogovém okně **Správce připojení** zadejte následující vlastnosti připojení pro zdroj dat:  

    -   **Název serveru**: zadejte název serveru databáze lokality Configuration Manager nebo ho vyberte v seznamu. Pokud místo výchozí instance pracujete s pojmenovanou instancí, zadejte &lt; název instance *databázového serveru* > \\ &lt; *instance name*>.  

    -   Vyberte **Ověřování systému Windows**.  

    -   V seznamu **Vyberte nebo zadejte název databáze** vyberte název vaší databáze lokality Configuration Manager.  

5.  Pro ověření připojení databáze klikněte na položku **Testování připojení**.  

6.  Jestliže je připojení úspěšné, klikněte na tlačítko **OK** , čímž zavřete dialogové okno **Správce připojení** . Pokud připojení úspěšné není, ověřte, zda informace jsou zadány správně a pak znovu klikněte na položku **Testování připojení** .  

7.  Na stránce **Vyberte, jak definovat připojení** ověřte, zda je vybráno **Vytvořit zdroj dat na základě stávajícího nebo nového připojení** , ověřte, zda zdroj dat, který jste právě zadali, je vybrán v okně **Datová připojení**, a pak klikněte na tlačítko **Další**.  

8.  Do pole **název zdroje dat**zadejte název zdroje dat a potom klikněte na tlačítko **Dokončit**. V tomto příkladu zadejte hodnotu **Jednoduchý_Model**.  

9. V **Průzkumníku řešení** pod uzlem **Zdroj dat** se nyní zobrazí zdroj dat **Simple_Model.ds** .  

    > [!NOTE]  
    >  Chcete-li upravit vlastnosti stávajícího zdroje dat, dvakrát klikněte na zdroj dat ve složce **Zdroj dat** v podokně **Průzkumník řešení** , čímž se zobrazí vlastnosti zdroje dat v nástroji Návrhář zdroje dat.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a>Definování zobrazení zdroje dat pro model sestavy  

1.  V **Průzkumníku řešení**klikněte pravým tlačítkem na položku **Zobrazení zdrojů dat** , kde vyberete **Přidat nový zdroj dat**.  

2.  Na stránce **Vítejte v Průvodci zobrazení zdroje dat** klikněte na tlačítko **Další**. Zobrazí se stránka **Vyberte zdroj dat** .  

3.  V okně **Zdroje relačních dat** ověřte, zda je vybrán zdroj dat **Simple_Model** , a pak klikněte na tlačítko **Další**.  

4.  Na kartě **Výběr tabulek a zobrazení** v seznamu **Dostupné objekty** vyberte následující zobrazení, které se má použít v modelu sestavy: **v_R_System (dbo)**.  

    > [!TIP]  
    >  Pro usnadnění vyhledání zobrazení v seznamu **Dostupné objekty** klikněte v horní části seznamu na záhlaví **Název** , čímž se objekty abecedně seřadí.  

5.  Po výběru zobrazení klikněte na tlačítko **>** pro přenos objektu do seznamu **zahrnuté objekty** .  

6.  Jestliže se zobrazí stránka **Shoda názvu** , přijměte výchozí nastavení a klikněte na tlačítko **Další**.  

7.  Pokud jste vybrali objekty, které potřebujete, klikněte na tlačítko **Další**a zadejte název zobrazení zdroje dat. V tomto příkladu zadejte hodnotu **Jednoduchý_Model**.  

8.  Klikněte na **Finish** (Dokončit). Zobrazení zdroje dat **Simple_Model.dsv** se zobrazí ve složce **Zobrazení zdrojů dat** v **Průzkumníku řešení**.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a>Vytvoření modelu sestavy  

1.  V **Průzkumníku řešení**klikněte pravým tlačítkem na položku **Modely sestav** , kde vyberete **Přidat nový model sestavy**.  

2.  Na stránce **Vítejte v Průvodci modelů sestav** klikněte na tlačítko **Další**.  

3.  Na stránce **Výběr zobrazení zdrojů dat** v seznamu **Dostupná zobrazení zdrojů dat** vyberte zobrazení zdroje dat a pak klikněte na tlačítko **Další**. V tomto příkladu vyberte **Simple_Model.dsv**.  

4.  Na stránce **Výběr pravidel pro vytvoření modelu sestavy** přijměte výchozí hodnoty a pak klikněte na tlačítko **Další**.  

5.  Na stránce **Statistika modelu** ověřte, že je vybráno **Aktualizovat statistiku modelu před vytvořením** , a pak klikněte na tlačítko **Další**.  

6.  Na stránce **Dokončení průvodce** zadejte název pro model sestavy. V tomto příkladu ověřte, že se zobrazí **Simple_Model** .  

7.  Pro dokončení průvodce a vytvoření modelu sestavy klikněte na tlačítko **Spustit**.  

8.  Průvodce opustíte kliknutím na tlačítko **Dokončit**. Model sestavy se zobrazí v okně Návrh.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> To publish the report model for use in SQL Server Reporting Services  

1.  V **Průzkumníku řešení**klikněte pravým tlačítkem na model sestavy a vyberte **Nasadit**. V tomto příkladu je model sestavy **Simple_Model.smdl**.  

2.  V levém dolním rohu okna **SQL Server Business Intelligence Development Studio** projděte stav nasazení. Pokud nasazení úspěšně proběhlo, zobrazí se **Nasazení dokončeno** . Pokud se nasazení nezdaří, příčina selhání se zobrazí v okně **Výstup** . Nový model sestavy je nyní k dispozici na vašem webu služby SQL Server Reporting Services.  

3.  Klikněte na tlačítko **Soubor**, dále klikněte na **Uložit vše**a pak okno **SQL Server Business Intelligence Development Studio**zavřete.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1. Vyhledejte složku, ve které jste vytvořili projekt modelu sestavy. Například název projektu%*USERPROFILE*% \ Documents\Visual Studio 2008 \ \\ * &lt; Projects \> .*  

2. Ze složky projektu modelu sestavy zkopírujte následující soubory do dočasné složky ve vašem počítači:  

   -   * &lt; Název \> modelu* **. DSV**  

   -   * &lt; Název \> modelu* **. smdl**  

3. Pomocí textového editoru, např. Poznámkového bloku, otevřete předchozí soubory.  

4. V souboru _ &lt; model název \> _**. DSV**vyhledejte první řádek souboru, který bude načten následujícím způsobem:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Teto řádek upravte do následující podoby:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Celý obsah souboru zkopírujte do schránky systému Windows.  

6. Zavřete soubor _ &lt; model název \> _**. DSV**.  

7. V souboru File _ &lt; name \> _**. smdl**vyhledejte poslední tři řádky souboru, které se zobrazí takto:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Vložte obsah souborového _ &lt; modelu název \> _**. DSV** přímo před poslední řádek souboru (** &lt; SemanticModel \> **).  

9. Uložte a zavřete soubor _ &lt; model název \> _**. smdl**.  

10. Zkopírujte _ &lt; \> soubor_**. smdl** do složky *% ProgramFiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other na serveru lokality Configuration Manager.  

    > [!IMPORTANT]  
    >  Po zkopírování souboru modelu sestavy do serveru Configuration Manager lokality je nutné ukončit a znovu spustit konzolu Configuration Manager předtím, než budete moci použít model sestavy v **Průvodci vytvořením sestavy**.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Steps for Creating an Advanced Report Model in SQL Server Reporting Services  
 Následující postupy můžete použít k vytvoření pokročilého modelu sestavy, který mohou uživatelé na webu použít k sestavení konkrétních sestav založených na modelu na základě dat ve více zobrazeních databáze Configuration Manager. Vytvoříte model sestavy, který autorovi sestavy prezentuje informace o počítačích klienta a operačním systému na těchto počítačích nainstalovaném. Tyto informace jsou pořízeny z následujících zobrazení v databázi Configuration Manager:  

- **V_R_System**: obsahuje informace o zjištěných počítačích a klientovi Configuration Manager.  

- **V_GS_OPERATING_SYSTEM**: Obsahuje informace o operačním systému nainstalovaném v klientském počítači.  

  Vybrané položky z předchozích zobrazení jsou konsolidovány do jediného seznamu, jsou jim přiděleny popisné názvy a poté jsou předloženy autorovi sestavy v Tvůrci sestav k zahrnutí do konkrétních sestav.  

  Na počítači, kde provádíte tyto postupy, zajistěte, aby byl nainstalován nástroj SQL Server Business Intelligence Development Studio a aby počítač byl připojen k síti serveru bodu služby Reporting Services. Podrobné informace o nástroji SQL Server Business Intelligence Development Studio naleznete v dokumentaci k systému SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Na ploše klikněte na tlačítko **Start**, klikněte na **Microsoft SQL Server 2008**a pak klikněte na nástroj **SQL Server Business Intelligence Development Studio**.  

2.  Poté, co se **SQL Server Business Intelligence Development Studio** v nástroji Microsoft Visual Studio otevře, klikněte na tlačítko **Soubor**, klikněte na **Nový**a pak klikněte na **Projekt**.  

3.  V dialogovém okně **Nový projekt** vyberte v seznamu **Šablony****Projekt modelu sestavy** .  

4.  V okně **Název** zadejte název tohoto modelu sestavy. V tomto příkladu zadejte hodnotu **Rozšířený_Model**.  

5.  Pro vytvoření projektu modelu sestavy klikněte na tlačítko **OK**.  

6.  V **Průzkumníku řešení** se zobrazí řešení **Rozšířený_Model**.  

    > [!NOTE]  
    >  Pokud podokno **Průzkumník řešení** nevidíte, klikněte na tlačítko **Zobrazení**a pak klikněte na **Průzkumník řešení**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>To define the data source for the report model  

1.  V podokně **Průzkumník řešení** nástroje **SQL Server Business Intelligence Development Studio**klikněte pravým tlačítkem na položku **Zdroje dat** , kde vyberete **Přidat nový zdroj dat**.  

2.  Na stránce **Vítejte v Průvodci zdroje dat** klikněte na tlačítko **Další**.  

3.  Na stránce **Vyberte, jak definovat připojení** ověřte, zda je vybrána položka **Vytvořit zdroj dat na základě stávajícího nebo nového připojení** a pak klikněte na tlačítko **Nový**.  

4.  V dialogovém okně **Správce připojení** zadejte následující vlastnosti připojení pro zdroj dat:  

    -   **Název serveru**: zadejte název serveru databáze lokality Configuration Manager nebo ho vyberte v seznamu. Pokud místo výchozí instance pracujete s pojmenovanou instancí, zadejte &lt; název instance *databázového serveru* > \\ &lt; *instance name*>.  

    -   Vyberte **Ověřování systému Windows**.  

    -   V seznamu **Vyberte nebo zadejte název databáze** vyberte název vaší databáze lokality Configuration Manager.  

5.  Pro ověření připojení databáze klikněte na položku **Testování připojení**.  

6.  Jestliže je připojení úspěšné, klikněte na tlačítko **OK** , čímž zavřete dialogové okno **Správce připojení** . Pokud připojení úspěšné není, ověřte, zda informace jsou zadány správně a pak znovu klikněte na položku **Testování připojení** .  

7.  Na stránce **Vyberte, jak definovat připojení** ověřte, zda je zvolena možnost **Vytvořit zdroj dat na základě stávajícího nebo nového připojení** , ověřte, zda je zdroj dat, který jste právě zadali, vybrán v seznamu **Datová připojení** a pak klikněte na tlačítko **Další**.  

8.  V poli **Název zdroje dat**zadejte název datového zdroje a pak klikněte na tlačítko **Dokončit**. V tomto příkladu zadejte hodnotu **Rozšířený_Model**.  

9. V **Průzkumníku řešení** pod uzlem **Zdroje dat** se nyní zobrazí zdroj dat **Rozšířený_Model.ds** .  

    > [!NOTE]  
    >  Chcete-li upravit vlastnosti stávajícího zdroje dat, dvakrát klikněte na zdroj dat ve složce **Zdroj dat** v podokně **Průzkumník řešení** , čímž se zobrazí vlastnosti zdroje dat v nástroji Návrhář zdroje dat.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>To define the data source view for the report model  

1. V **Průzkumníku řešení**klikněte pravým tlačítkem na položku **Zobrazení zdrojů dat** , kde vyberete **Přidat nový zdroj dat**.  

2. Na stránce **Vítejte v Průvodci zobrazení zdroje dat** klikněte na tlačítko **Další**. Zobrazí se stránka **Vyberte zdroj dat** .  

3. V okně **Zdroje relačních dat** ověřte, zda je vybrán zdroj dat **Rozšířený_Model** a pak klikněte na tlačítko **Další**.  

4. Na stránce **Výběr tabulek a zobrazení** v seznamu **Dostupné objekty** vyberte následující zobrazení, která se mají použít v modelu sestavy:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Po výběru každého zobrazení klikněte na tlačítko **>** pro přenos objektu do seznamu **zahrnuté objekty** .  

   > [!TIP]  
   >  Pro usnadnění vyhledání zobrazení v seznamu **Dostupné objekty** klikněte v horní části seznamu na záhlaví **Název** , čímž se objekty abecedně seřadí.  

5. Jestliže se zobrazí dialogové okno **Shoda názvu** , přijměte výchozí nastavení a klikněte na tlačítko **Další**.  

6. Pokud jste již vybrali požadované objekty, klikněte na tlačítko **Další**a zadejte název zobrazení zdroje dat. V tomto příkladu zadejte hodnotu **Rozšířený_Model**.  

7. Klikněte na **Finish** (Dokončit). Zobrazení zdroje dat **Rozšířený_Model.dsv** se zobrazí v **Průzkumníku řešení** ve složce **Zobrazení zdrojů dat**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Definování vztahů v zobrazení zdroje dat  

1.  V **Průzkumníku řešení**dvakrát klikněte na zdroj dat **Rozšířený_Model.dsv** a otevřete okno Návrh.  

2.  Klikněte pravým tlačítkem na záhlaví okna **v_R_System** , zvolte možnost **Nahradit tabulku**a poté klikněte na položku **S novým pojmenovaným dotazem**.  

3.  V dialogovém okně **Vytvořit pojmenovaný dotaz** klikněte na ikonu **Přidat tabulku** (obvykle poslední ikona na pásu karet).  

4.  V dialogovém okně **Přidat tabulku** klikněte na kartu **Zobrazení** , v seznamu vyberte zobrazení **V_GS_OPERATING_SYSTEM** a klikněte na tlačítko **Přidat**.  

5.  Kliknutím na tlačítko **Zavřít** zavřete dialogové okno **Přidat tabulku** .  

6.  V dialogovém okně **Vytvořit pojmenovaný dotaz** zadejte následující údaje:  

    -   **Název:** Zadejte název dotazu. V tomto příkladu zadejte hodnotu **Rozšířený_Model**.  

    -   **Popis:** Zadejte popis dotazu. V tomto příkladu zadejte **Vzorový model sestavy služby Reporting Services**.  

7.  V okně **v_R_System** vyberte v seznamu objektů následující položky, které se mají zobrazit v modelu sestavy:  

    -   **Prostředku**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  V okně **v_GS_OPERATING_SYSTEM** vyberte v seznamu objektů následující položky, které se mají zobrazit v modelu sestavy:  

    -   **Prostředku**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Aby bylo možné objekty v těchto zobrazeních předložit autorovi sestavy v jediném seznamu, je nutné určit vztah mezi oběma tabulkami nebo zobrazeními pomocí propojení. Obě zobrazení lze propojit pomocí objektu **ResourceID**, který se objevuje v obou zobrazeních.  

10. V okně **v_R_System** klikněte na objekt **ResourceID** , podržte tlačítko a přetáhněte objekt k objektu **ResourceID** v okně **v_GS_OPERATING_SYSTEM** .  

11. Klikněte na tlačítko **OK.**  

12. Okno **Rozšířený_Model** nahradí okno **v_R_System** a obsahuje všechny objekty požadované pro model sestavy ze zobrazení **v_R_System** a **v_GS_OPERATING_SYSTEM** . Nyní lze z Návrháře zobrazení zdroje dat odstranit okno **v_GS_OPERATING_SYSTEM** . Klikněte pravým tlačítkem na záhlaví okna **v_GS_OPERATING_SYSTEM** a zvolte možnost **Odstranit tabulku z DSV**. V dialogovém okně **Odstranit objekty** potvrďte odstranění kliknutím na tlačítko **OK** .  

13. Klikněte na **soubor**a potom klikněte na **Uložit vše**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  V **Průzkumníku řešení**klikněte pravým tlačítkem na položku **Modely sestav** , kde vyberete **Přidat nový model sestavy**.  

2.  Na stránce **Vítejte v Průvodci modelů sestav** klikněte na tlačítko **Další**.  

3.  Na stránce **Výběr zobrazení zdroje dat** v seznamu **Dostupná zobrazení zdrojů dat** vyberte zobrazení zdroje dat a pak klikněte na tlačítko **Další**. V tomto příkladu vyberte **Simple_Model.dsv**.  

4.  Na stránce **Výběr pravidel pro vytvoření modelu sestavy** neměňte výchozí hodnoty a klikněte na tlačítko **Další**.  

5.  Na stránce **Statistika modelu** ověřte, že je vybráno **Aktualizovat statistiku modelu před vytvořením** , a pak klikněte na tlačítko **Další**.  

6.  Na stránce **Dokončení průvodce** zadejte název pro model sestavy. V tomto příkladu ověřte, že se zobrazí **Rozšířený_Model** .  

7.  Pro dokončení průvodce a vytvoření modelu sestavy klikněte na tlačítko **Spustit**.  

8.  Průvodce opustíte kliknutím na tlačítko **Dokončit**.  

9. Model sestavy se zobrazí v okně Návrh.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Úprava názvů objektů v modelu sestavy  

1.  V **Průzkumníku řešení**klikněte pravým tlačítkem na model sestavy a vyberte položku **Návrhář zobrazení**. V tomto příkladu vyberte **Rozšířený_Model.smdl**.  

2.  V okně návrhu modelu sestavy klikněte pravým tlačítkem na libovolný název objektu a zvolte možnost **Přejmenovat**.  

3.  Zadejte nový název pro vybraný objekt a stiskněte klávesu Enter. Můžete například přejmenovat objekt **CSD_Version_0** na **Verze Windows Service Pack**.  

4.  Po dokončení přejmenování objektů klikněte na nabídku **Soubor**a zvolte položku **Uložit vše**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>To publish the report model for use in SQL Server Reporting Services  

1.  V **Průzkumníku řešení**klikněte pravým tlačítkem na model sestavy **Rozšířený_Model.smdl** a zvolte položku **Nasadit**.  

2.  V levém dolním rohu okna **SQL Server Business Intelligence Development Studio** projděte stav nasazení. Pokud nasazení úspěšně proběhlo, zobrazí se **Nasazení dokončeno** . Pokud se nasazení nezdaří, příčina selhání se zobrazí v okně **Výstup** . Nový model sestavy je nyní k dispozici na vašem webu služby SQL Server Reporting Services.  

3.  Klikněte na tlačítko **Soubor**, dále klikněte na **Uložit vše**a pak okno **SQL Server Business Intelligence Development Studio**zavřete.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Vyhledejte složku, ve které jste vytvořili projekt modelu sestavy. Například název projektu%*USERPROFILE*% \ Documents\Visual Studio 2008 \ \\ * &lt; Projects \> .*  

2. Ze složky projektu modelu sestavy zkopírujte následující soubory do dočasné složky ve vašem počítači:  

   -   * &lt; Název \> modelu* **. DSV**  

   -   * &lt; Název \> modelu* **. smdl**  

3. Pomocí textového editoru, např. Poznámkového bloku, otevřete předchozí soubory.  

4. V souboru _ &lt; model název \> _**. DSV**vyhledejte první řádek souboru, který bude načten následujícím způsobem:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Teto řádek upravte do následující podoby:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Celý obsah souboru zkopírujte do schránky systému Windows.  

6. Zavřete soubor _ &lt; model název \> _**. DSV**.  

7. V souboru File _ &lt; name \> _**. smdl**vyhledejte poslední tři řádky souboru, které se zobrazí takto:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Vložte obsah souborového _ &lt; modelu název \> _**. DSV** přímo před poslední řádek souboru (** &lt; SemanticModel \> **).  

9. Uložte a zavřete soubor _ &lt; model název \> _**. smdl**.  

10. Zkopírujte _ &lt; \> soubor_**. smdl** do složky *% ProgramFiles%* \Microsoft Endpoint Manager\AdminConsole\XmlStorage\Other na serveru lokality Configuration Manager.  

    > [!IMPORTANT]  
    >  Po zkopírování souboru modelu sestavy do serveru Configuration Manager lokality je nutné ukončit a znovu spustit konzolu Configuration Manager předtím, než budete moci použít model sestavy v **Průvodci vytvořením sestavy**.  
