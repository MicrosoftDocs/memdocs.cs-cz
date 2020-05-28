---
title: Konfigurace vytváření sestav
titleSuffix: Configuration Manager
description: Jak nastavit vytváření sestav v hierarchii Configuration Manager, včetně informací o SQL Server Reporting Services.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b7ada6f54a7642817a321937a4d7128994d5538
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823975"
---
# <a name="configure-reporting-in-configuration-manager"></a>Konfigurace vytváření sestav v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než budete moci vytvořit, upravit a spustit sestavy v konzole Configuration Manager, je třeba provést několik úloh konfigurace. Tento článek vám umožní nakonfigurovat vytváření sestav v hierarchii Configuration Manager.  

Než nainstalujete a nakonfigurujete SQL Server Reporting Services ve vaší hierarchii, přečtěte si následující články o Configuration Manager vytváření sestav:  

- [Úvod do vytváření sestav](introduction-to-reporting.md)  

- [Plánování vytváření sestav](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services je platforma pro generování sestav založená na serveru, která poskytuje komplexní funkci generování sestav pro různé druhy zdrojů dat. Bod služby Reporting Services v Configuration Manager komunikuje s SQL Server Reporting Services a:

- Kopírování sestav Configuration Manager do zadané složky sestav
- Konfigurace nastavení služby Reporting Services
- Konfigurace nastavení zabezpečení služby Reporting Services

Při spuštění sestavy se komponenta služby Reporting Services připojí k databázi lokality Configuration Manager a načte data.  

Předtím, než budete moci nainstalovat bod služby Reporting Services do Configuration Manager lokality, nainstalujte a nakonfigurujte SQL Server Reporting Services v cílovém systému lokality. Další informace najdete v tématu [instalace SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).  

### <a name="verify-sql-server-reporting-services-installation"></a>Ověření instalace SQL Server Reporting Services

Pro ověření, zda je služba SQL Server Reporting Services nainstalovaná a je spuštěná správně, použijte následující postup.

1. Přejděte do nabídky **Start** v systému lokality a otevřete **službu Reporting Services Configuration Manager**. Můžete ji najít v části **Konfigurační nástroje** **Microsoft SQL Server** skupině.

2. V okně **připojení konfigurace služby Reporting Services** zadejte název serveru, který je hostitelem SQL Server Reporting Services. Vyberte instanci SQL Server, na které jste nainstalovali SQL Reporting Services. Pak vyberte **připojit** k otevření služby Reporting Services Configuration Manager.  

3. Na stránce **stav serveru sestav** ověřte, zda je **spuštěn** **stav služby hlášení** . Pokud není v tomto stavu, vyberte **Spustit**.  

4. Na stránce **Adresa URL webové služby** vyberte adresu URL v **adresách URL webové služby Report Service**. Tato akce testuje připojení ke složce sestav. Prohlížeč vás může vyzvat k zadání přihlašovacích údajů. Ověřte, zda se webová stránka úspěšně otevřela.

5. Na stránce **databáze** ověřte, zda je **režim serveru sestav** nastaven na hodnotu **nativní**.  

6. Na stránce **Adresa URL správce sestav** vyberte adresu URL v **identifikaci webu Správce sestav**. Tato akce testuje připojení k virtuálnímu adresáři pro správce sestav. Prohlížeč vás může vyzvat k zadání přihlašovacích údajů. Ověřte, zda se webová stránka úspěšně otevřela.

    > [!NOTE]  
    > Vytváření sestav v Configuration Manager nevyžaduje správce sestav služby Reporting Services. Budete ji potřebovat jenom v případě, že chcete spouštět sestavy v prohlížeči nebo spravovat sestavy pomocí Správce sestav.  

7. Kliknutím na tlačítko **ukončit** zavřete službu Reporting Services Configuration Manager.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Konfigurace vytváření sestav pro použití Tvůrce sestav 3,0

1. V počítači se spuštěnou konzolou Configuration Manager otevřete Editor registru systému Windows.  

2. Přejděte na `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Otevřete klíč **klávesu ReportBuilderApplicationManifestName** a upravte data hodnoty.  

4. Změňte hodnotu na `ReportBuilder_3_0_0_0.application` a pak kliknutím na **OK** uložte.

5. Zavřete editor registru systému Windows.  

## <a name="install-a-reporting-services-point"></a>Instalace bodu služby Reporting Services

Chcete-li spravovat sestavy v lokalitě, nainstalujte bod služby Reporting Services. Bod služby Reporting Services:

- Kopíruje složky sestav a sestavy do SQL Server Reporting Services
- Použije zásady zabezpečení pro sestavy a složky.
- Nastaví nastavení konfigurace ve službě Reporting Services.

### <a name="requirements-and-limitations"></a>Požadavky a omezení

Než budete moci zobrazit nebo spravovat sestavy v konzole Configuration Manager, budete potřebovat bod služby Reporting Services. Nakonfigurujte tuto roli systému lokality na serveru s Microsoft SQL Server Reporting Services. Další informace najdete v tématu [předpoklady pro vytváření sestav](prerequisites-for-reporting.md).  

- Když vyberete lokalitu pro instalaci bodu služby Reporting Services, uživatelé, kteří budou mít přístup k sestavám, musí být ve stejném oboru zabezpečení jako lokalita, do které roli nainstalujete.  

- Po instalaci bodu služby Reporting Services do systému lokality neměňte adresu URL pro server sestav.

    Například vytvoříte bod služby Reporting Services. Pak změníte adresu URL pro server sestav ve službě Reporting Services Configuration Manager. Konzola Configuration Manager nadále používá starou adresu URL. Z konzoly nástroje nemůžete spouštět, upravovat ani vytvářet sestavy.

    Pokud potřebujete změnit adresu URL serveru sestav, nejprve odeberte stávající bod služby Reporting Services. Změňte adresu URL a pak bod služby Reporting Services znovu nainstalujte.  

- Při instalaci bodu služby Reporting Services zadejte [účet bodu služby Reporting Services](../../plan-design/hierarchy/accounts.md#reporting-services-point-account). Pro uživatele z jiné domény pro spuštění sestavy vytvořte obousměrný vztah důvěryhodnosti mezi doménami. V opačném případě se spuštění sestavy nezdařilo.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" />Instalace bodu služby Reporting Services do systému lokality  

Další informace o konfiguraci systémů lokality najdete v tématu [Instalace rolí systému lokality](../deploy/configure/install-site-system-roles.md).  

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte uzel **servery a role systému lokality** .  

1. Přidejte bod služby Reporting Services na nový nebo existující server systému lokality:  

    - *Nový systém lokality*: na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit server systému lokalit**. Otevře se **Průvodce vytvořením serveru systému lokality** .  

    - *Existující systém lokality*: Vyberte cílový server. Na kartě **Domů** na pásu karet ve skupině **Server** vyberte **Přidat roli systému lokality**. Otevře se **Průvodce Přidat role systému lokality** .  

1. Na stránce **Obecné** definujte obecná nastavení serveru systému lokalit. Když přidáte bod služby Reporting Services na existující server, ověřte hodnoty, které jste předtím nakonfigurovali.  

1. Na stránce **Výběr role systému** vyberte možnost **bod služby Reporting Services** v seznamu dostupných rolí a pak vyberte možnost **Další**.  

1. Na stránce **bod služby Reporting Services** nakonfigurujte následující nastavení:  

    - **Název serveru databáze lokality**: zadejte název serveru, který je hostitelem databáze lokality Configuration Manager. Průvodce obvykle načte plně kvalifikovaný název domény (FQDN) pro server. Chcete-li určit instanci databáze, použijte formát &lt; *název* > \& lt;* název instance*>. Například, `sqlserver\named1`.

    - **Název databáze**: zadejte název databáze lokality Configuration Manager. Vyberte **ověřit** a potvrďte, že Průvodce má přístup k databázi lokality.  

        > [!IMPORTANT]  
        > Uživatelský účet, který použijete k vytvoření bodu služby Reporting Services, musí mít oprávnění **ke čtení** databáze lokality. V případě selhání testu připojení se objeví červená varovná ikona. Kontextový text přechodu na ikoně obsahuje podrobnosti o selhání. Opravte chybu a pak znovu vyberte **test** .  

    - **Název složky**: zadejte název složky, která se má vytvořit a použít pro sestavy Configuration Manager ve službě Reporting Services.  

    - **Instance serveru služby Reporting Services**: vyberte instanci SQL Server služby Reporting Services. Pokud tato stránka neobsahuje žádné instance, ověřte, že je nainstalovaná, nakonfigurovaná a spuštěná SQL Server Reporting Services.  

        > [!IMPORTANT]  
        > Configuration Manager vytvoří připojení v kontextu aktuálního uživatele k rozhraní WMI ve vybraném systému lokality. Toto připojení používá k načtení instance SQL Server služby Reporting Services. Aktuální uživatel musí mít přístup **pro čtení** ke službě WMI v systému lokality nebo Průvodce nemůže získat instance služby Reporting Services.  

    - **Účet bodu služby Reporting Services**: vyberte možnost **nastavit**a pak vyberte účet, který chcete použít. SQL Server Reporting Services v bodu služby Reporting Services používá tento účet pro připojení k databázi lokality Configuration Manager. Toto připojení má načíst data pro sestavu. Vyberte možnost **existující účet** a zadejte uživatelský účet systému Windows, který jste dříve nakonfigurovali jako účet Configuration Manager. Vyberte možnost **nový účet** a zadejte uživatelský účet systému Windows, který není aktuálně nakonfigurován pro použití. Configuration Manager automaticky udělí zadanému uživateli přístup k databázi lokality.  

        Účet, který spouští službu Reporting Services, musí patřit do skupiny místních zabezpečení skupiny zabezpečení **Windows Authorization Access**. Tento účet udělí účtu oprávnění **ke čtení** u atributu **tokenGroupsGlobalAndUniversal** pro všechny uživatelské objekty v doméně. Uživatelé v jiné doméně než účet bodu služby Reporting Services potřebují oboustranný vztah důvěryhodnosti mezi doménami, aby bylo možné sestavy úspěšně spouštět.

        Zadaný uživatelský účet systému Windows a jeho heslo jsou zašifrovány a uloženy v databázi služby Reporting Services. Služba Reporting Services načítá pomocí tohoto účtu a hesla data pro sestavy z databáze lokality.  

        > [!IMPORTANT]  
        > Účet, který zadáte, musí mít oprávnění **Přihlásit se místně** na serveru, který je hostitelem databáze služby Reporting Services.  

1. Dokončete průvodce.

Po dokončení Průvodce vytvoří Configuration Manager složky sestav ve službě Reporting Services. Pak zkopíruje své sestavy do zadaných složek sestav.  

> [!TIP]  
> Chcete-li zobrazit seznam pouze systémů lokalit, které jsou hostiteli role lokality bodu služby Reporting Services, klikněte pravým tlačítkem myši na **servery a role systému lokality**a vyberte **bod služby Reporting Services**.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" />Jazyky pro sestavy

<!-- SCCMDocs#1067 -->

Když Configuration Manager vytváří složky sestav a kopíruje sestavy na server sestav, určí příslušný jazyk pro objekty.

- Vytváření složek sestav, kopírování sestav

  - Vytváření objektů pomocí národního prostředí operačního systému serveru lokality

  - Pokud konkrétní jazyková sada není dostupná, je výchozí pro angličtinu (CSY).

- Zobrazení sestav ve webovém prohlížeči

  - Název složky a sestavy: stejné národní prostředí jako server lokality
  
  - Obsah sestavy: dynamický na základě národního prostředí prohlížeče

- Zobrazení sestav v konzole Configuration Manager

  - Název složky a sestavy: dynamické na základě národního prostředí konzoly
  
  - Obsah sestavy: dynamické na základě národního prostředí konzoly

Po nainstalování bodu služby Reporting Services na lokalitu bez jazykových sad jsou sestavy instalovány v angličtině. Pokud instalujete jazykovou sadu poté, co jste nainstalovali bod služby Reporting Services, musíte bod služby Reporting Services odinstalovat a znovu nainstalovat, aby byl pro sestavy dostupný v jazyce příslušné jazykové sady.  

Další informace najdete v tématu [jazykové sady](../deploy/install/language-packs.md).

### <a name="file-installation-and-report-folder-security-rights"></a>Instalace souboru a zabezpečovací práva složky sestav

Configuration Manager provádí následující akce pro instalaci bodu služby Reporting Services a pro konfiguraci služby Reporting Services:  

> [!IMPORTANT]  
> Lokalita provede tyto akce v kontextu účtu, který je nakonfigurován pro službu SMS_Executive. Obvykle se jedná o účet místního systému serveru lokality.  

- Nainstalujte roli lokality bodu služby Reporting Services.  

- Vytvořte zdroj dat ve službě Reporting Services s uloženými přihlašovacími údaji, které jste zadali v průvodci. Tento účet je uživatelský účet systému Windows a heslo, které služba Reporting Services používá pro připojení k databázi lokality při spouštění sestav.  

- Vytvořte kořenovou složku Configuration Manager ve službě Reporting Services.  

- Přidejte role zabezpečení **Uživatelé sestav nástroje ConfigMgr** a **Správci sestav nástroje ConfigMgr** ve službě Reporting Services.  

- Vytvořte podsložky a potom nasaďte Configuration Manager sestavy ze `%ProgramFiles%\SMS_SRSRP` serveru lokality do služby Reporting Services.  

- Přidejte roli **Uživatelé sestav nástroje ConfigMgr** ve službě Reporting Services do kořenových složek pro všechny uživatelské účty v Configuration Manager, které mají oprávnění **ke čtení z lokality** .  

- Přidejte roli **Správci sestav nástroje ConfigMgr** ve službě Reporting Services do kořenových složek pro všechny uživatelské účty v Configuration Manager s právy pro **úpravu lokality** .  

- Načtěte mapování mezi složkami sestav a Configuration Manager typy zabezpečených objektů. Configuration Manager tuto mapu udržuje v databázi lokality.  

- Nakonfigurujte následující práva pro administrativní uživatele v Configuration Manager na konkrétní složky sestav ve službě Reporting Services:  

  - Přidejte uživatele a přiřaďte roli **Uživatelé sestav nástroje ConfigMgr** k přidružené složce sestav pro uživatele s právy pro správu, kteří mají oprávnění **Spustit sestavu** pro objekt Configuration Manager.  

  - Přidejte uživatele a přiřaďte roli **Správci sestav nástroje ConfigMgr** k přidružené složce sestav pro správce, kteří mají oprávnění **Upravit sestavu** pro objekt Configuration Manager.  

Configuration Manager se připojí ke službě Reporting Services a nastaví oprávnění pro uživatele v kořenových složkách služby Configuration Manager a Reporting Services a na konkrétní složky sestav. Po počáteční instalaci bodu služby Reporting Services se Configuration Manager připojí ke službě Reporting Services každých 10 minut, aby se ověřilo, že uživatelská práva konfigurovaná ve složkách sestav jsou přidružená práva, která jsou nastavena pro uživatele Configuration Manager. Když se přidají uživatelé nebo se upraví uživatelská práva ve složce sestav pomocí Správce sestav služby Reporting Services, Configuration Manager přepíše tyto změny pomocí přiřazení na základě rolí uložených v databázi lokality. Configuration Manager také odebere uživatele, kteří nemají práva k vytváření sestav v Configuration Manager.  

### <a name="reporting-services-security-roles"></a>Role zabezpečení služby Reporting Services

Když Configuration Manager nainstaluje bod služby Reporting Services, přidá do služby Reporting Services tyto role zabezpečení:  

- **Uživatelé sestav nástroje ConfigMgr**: Uživatelé přiřazení k této roli zabezpečení mohou spouštět pouze sestavy Configuration Manager.  

- **Správci sestav nástroje ConfigMgr**: Uživatelé přiřazení k této roli zabezpečení mohou provádět všechny úlohy související s vytvářením sestav v Configuration Manager.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a>Ověřit instalaci

Ověřte instalaci bodu služby Reporting Services tak, že prohlížíte konkrétní stavové zprávy a položky souboru protokolu. Úspěšnost instalace bodu služby Reporting Services ověříte pomocí následujícího postupu.  

> [!Note]  
> Pokud vidíte sestavy v podsložce **sestavy** uzlu **vytváření sestav** v pracovním prostoru **monitorování** v konzole Configuration Manager, můžete tento postup přeskočit.

### <a name="verify-installation-by-status-message"></a>Ověřit instalaci podle stavové zprávy

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **stav systému**a vyberte uzel **Stav součásti** .  

1. Vyberte součást **SMS_SRS_REPORTING_POINT** .  

1. Na kartě **Domů** na pásu karet ve skupině **součást** vyberte možnost **Zobrazit zprávy**a pak zvolte možnost **vše**.  

1. Zadejte datum a čas pro období před instalací bodu služby Reporting Services a pak vyberte **OK**.  

1. Ověřte ID stavové zprávy **1015**. Tato stavová zpráva znamená, že bod služby Reporting Services byl úspěšně nainstalován.

### <a name="verify-installation-by-log-file"></a>Ověřit instalaci podle souboru protokolu

Otevřete soubor **soubor Srsrp. log** , který se nachází v adresáři **Logs** instalační cesty Configuration Manager. Vyhledejte řetězec `Installation was successful` .

Projděte si tento soubor protokolu od okamžiku, kdy byl úspěšně nainstalován bod služby Reporting Services. Ověřte, že byly vytvořeny složky sestav, že byly nasazeny sestavy a že u každé složky byly potvrzeny zásady zabezpečení. Po posledním řádku potvrzení zásad zabezpečení vyhledejte řetězec `Successfully checked that the SRS web service is healthy on server` .  

## <a name="configure-a-certificate-to-author-reports"></a>Konfigurace certifikátu pro vytváření sestav

K dispozici je mnoho možností, jak můžete vytvářet sestavy v SQL Server Reporting Services. Když vytváříte nebo upravujete sestavy v konzole Configuration Manager, Configuration Manager otevře Tvůrce sestav k použití jako prostředí pro vytváření obsahu. Bez ohledu na to, jakým způsobem vytváříte sestavy Configuration Manager, potřebujete certifikát podepsaný svým držitelem pro ověřování serveru databáze serveru lokality.

> [!NOTE]  
> Další informace o vytváření sestav pomocí SQL Server Reporting Services najdete v tématu [prostředí pro vytváření Tvůrce sestav](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Configuration Manager automaticky nainstaluje certifikát na server lokality a všechny role poskytovatele služby SMS. Můžete vytvářet nebo upravovat sestavy z konzoly Configuration Manager, když je spustíte z některého z těchto serverů.

Když vytváříte nebo upravujete sestavy z konzoly Configuration Manager v jiném počítači, exportujte certifikát ze serveru lokality. Popisný název konkrétního certifikátu je plně kvalifikovaný název domény serveru lokality v úložišti certifikátů **Důvěryhodné osoby** pro místní počítač. Tento certifikát přidejte do úložiště certifikátů **Důvěryhodné osoby** v počítači, na kterém je spuštěna konzola Configuration Manager.  

## <a name="modify-reporting-services-point-settings"></a>Úprava nastavení bodu služby Reporting Services

Po instalaci této role můžete upravit připojení k databázi lokality a nastavení ověřování ve vlastnostech bodu služby Reporting Services.

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte uzel **servery a role systému lokality** .  

    > [!TIP]  
    > Chcete-li zobrazit seznam pouze systémů lokalit, které jsou hostiteli bodu služby Reporting Services, klikněte pravým tlačítkem myši na uzel **servery a role systému lokality** a vyberte **bod služby Reporting Services**.  

1. Vyberte systém lokality, který je hostitelem bodu služby Reporting Services. Pak v podokně podrobností vyberte role systému lokality **bodu služby Reporting Services** .

1. Na kartě **role lokality** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.  

1. Ve **vlastnostech bodu služby Reporting Services**lze upravit následující nastavení:  

    - **Název serveru databáze lokality**

    - **Název databáze**

    - **Uživatelský účet**

1. Výběrem **OK** uložte změny a zavřete vlastnosti.  

Další informace o těchto nastaveních naleznete v popisech v části [instalace bodu služby Reporting Services do systému lokality](#bkmk_install).

## <a name="power-bi-report-server"></a>Server sestav Power BI

Počínaje verzí 2002 můžete integrovat vytváření sestav pomocí Server sestav Power BI. Další informace o konfiguraci najdete v tématu věnovaném [integraci s server sestav Power BI](powerbi-report-server.md).

## <a name="upgrade-sql-server"></a>SQL Server upgradu

Chcete-li upgradovat SQL Server a SQL Server Reporting Services nejprve, odeberte bod služby Reporting Services z lokality. Po upgradu SQL Server znovu nainstalujte bod služby Reporting Services v Configuration Manager.

Pokud tento proces nesledujete, zobrazí se při spuštění nebo úpravě sestav z konzoly Configuration Manager chyby. Sestavy můžete ve webovém prohlížeči úspěšně spouštět a upravovat.  

## <a name="configure-report-options"></a> Konfigurace možností sestav

Můžete vybrat výchozí bod služby Reporting Services, který používáte ke správě sestav. Lokalita může mít více než jeden bod služby Reporting Services, ale používá pouze výchozí server pro správu sestav. K nastavení možností sestav pro svoji lokalitu použijte následující postup.  

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a potom vyberte uzel **sestavy** .  

1. Na kartě **Domů** na pásu karet ve skupině **Nastavení** vyberte **Možnosti sestavy**.  

1. V seznamu vyberte výchozí server sestav a pak vyberte **OK**.

Pokud se nezobrazí žádné servery, ověřte, že jste v lokalitě nainstalovali a nakonfigurovali bod služby Reporting Services. Další informace najdete v tématu [ověření instalace](#bkmk_verify).

Ujistěte se, že počítač používá verzi SQL Server Tvůrce sestav, která odpovídá verzi SQL Server, kterou používáte pro server sestav. V opačném případě se zobrazí chyba, výchozí server sestav nebude uložen a nemůžete vytvářet ani upravovat sestavy.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Další kroky

[Operace a údržba pro vytváření sestav](operations-and-maintenance-for-reporting.md)
