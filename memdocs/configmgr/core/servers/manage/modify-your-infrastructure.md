---
title: Změna infrastruktury
titleSuffix: Configuration Manager
description: Proveďte změny nebo proveďte akce, které mají vliv na infrastrukturu Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713671"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Úprava infrastruktury Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po instalaci jedné nebo více lokalit může být nutné upravit konfigurace nebo provést akce, které mají vliv na vaši infrastrukturu.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a>Správa poskytovatele serveru SMS

Poskytovatel serveru SMS poskytuje bod administrativního kontaktu pro jednu nebo více Configuration Manager konzol. Když nainstalujete více poskytovatelů serveru SMS, můžete poskytnout redundanci pro kontaktní body pro správu lokality a hierarchie.

V každé Configuration Manager lokalitě můžete znovu spustit instalační program a:

- Přidejte další instanci poskytovatele serveru SMS. Každá další instance poskytovatele serveru SMS musí být v samostatném počítači.

- Odebrat instanci poskytovatele serveru SMS. Chcete-li odebrat posledního poskytovatele serveru SMS pro lokalitu, musíte lokalitu odinstalovat.

Instalaci nebo odebrání poskytovatele serveru SMS můžete monitorovat zobrazením souboru **ConfigMgrSetup. log** v kořenové složce serveru lokality, na které spouštíte instalační program.

Před úpravou poskytovatele služby SMS v lokalitě nástroje si přečtěte téma [plánování poskytovatele serveru SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Správa konfigurace poskytovatele služby SMS pro lokalitu  

1. Spusťte **instalační program Configuration Manager** z `\BIN\X64\setup.exe` nástroje v instalační složce Configuration Manager webu.

1. Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat tuto lokalitu**.

1. Na stránce **Údržba lokality** vyberte **Upravit konfiguraci poskytovatele služby SMS**.

1. Na stránce **Správa poskytovatelů serveru SMS** vyberte jednu z následujících možností:

    - **Přidat nového poskytovatele služby SMS**: zadejte plně kvalifikovaný název domény pro počítač, který bude hostitelem poskytovatele služby SMS, který aktuálně není hostitelem.

    - **Odinstalujte zadaného poskytovatele služby SMS**: vyberte název počítače, ze kterého chcete odebrat poskytovatele služby SMS.

    > [!TIP]  
    > Chcete-li přesunout poskytovatele služby SMS mezi dvěma počítači, nainstalujte jej nejprve do nového počítače. Pak ho odeberte z původního umístění. Není k dispozici možnost přesunout poskytovatele služby SMS mezi počítači.

Po dokončení Průvodce instalací se konfigurace poskytovatele služby SMS dokončí. Ve **vlastnostech**lokality na kartě **Obecné** ověřte počítače, které mají nainstalovaného poskytovatele služby SMS pro danou lokalitu.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a>Správa konzoly Configuration Manager

Následující úlohy vám pomůžou se správou konzoly Configuration Manager:

- Chcete-li upravit jazyk, který se zobrazí v konzole Configuration Manager, přečtěte si část [správa Configuration Manager jazyka konzoly](#BKMK_ManageConsoleLanguages) .

- Informace o instalaci dalších konzol najdete v tématu [install Configuration Manager Consoles](../deploy/install/install-consoles.md).

- Postup při konfiguraci oprávnění modelu DCOM pro povolení konzol, které jsou vzdálené od serveru lokality, naleznete v části [Konfigurace oprávnění modelu DCOM pro vzdálené Configuration Manager konzoly](#BKMK_ConfigDCOMforRemoteConsole) .

- Chcete-li upravit oprávnění pro správu a omezit tak, co mohou uživatelé zobrazit a dělat v konzole nástroje, přečtěte si téma [Úprava rozsahu správy administrativního uživatele](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a>Správa jazyka konzoly Configuration Manager

Během instalace serveru lokality se instalační soubory konzoly Configuration Manager a podporované jazykové sady pro lokalitu zkopírují do `\Tools\ConsoleSetup` podsložky v instalační cestě Configuration Manager na serveru lokality.

- Když spustíte instalaci konzoly Configuration Manager z této složky na serveru lokality, zkopíruje se do počítače konzola Configuration Manager a podporované soubory jazykových sad.

- Když je k dispozici jazyková sada pro aktuální nastavení jazyka v počítači, otevře se konzola Configuration Manager v tomto jazyce.

- Pokud přidružená jazyková sada není pro konzolu Configuration Manager k dispozici, otevře se konzola v angličtině (USA).

Například nainstalujete konzolu Configuration Manager ze serveru lokality, který podporuje angličtinu, němčinu a francouzštinu. Pokud otevřete konzolu Configuration Manager v počítači s nakonfigurovaným nastavením jazyka francouzštiny, otevře se konzola ve francouzštině. Pokud otevřete konzolu Configuration Manager v počítači s nakonfigurovaným jazykem japonštiny, otevře se konzola v angličtině, protože japonská jazyková sada není k dispozici.  

Pokaždé, když se otevře konzola Configuration Manager:

- TT určuje nakonfigurované nastavení jazyka pro počítač.
- Ověří, jestli je k dispozici přidružená jazyková sada pro konzolu Configuration Manager.
- Otevře konzolu pomocí příslušné jazykové sady.

Pokud chcete konzolu Configuration Manager otevřít v angličtině bez ohledu na nakonfigurované nastavení jazyka v počítači, odeberte nebo přejmenujte soubory jazykové sady v počítači.

Následující postupy použijte ke spuštění konzoly Configuration Manager v angličtině bez ohledu na Nastavení konfigurovaného národního prostředí v počítači.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Instalace verze Configuration Manager konzoly jenom v angličtině do počítačů  

1. V Průzkumníku Windows přejděte na `\Tools\ConsoleSetup\LanguagePack` adresu instalace Configuration Manager.

1. Přejmenujte soubory **.msp** a **.mst**. Můžete například změnit ** &lt;\>název souboru. MSP** na ** &lt;název\>souboru. MSP. disabled**.

1. Nainstalujte do počítače konzolu Configuration Manager.

    > [!IMPORTANT]
    > Pokud jsou pro server lokality nakonfigurovány nové jazyky serveru, jsou soubory. msp a. mst znovu zkopírovány do složky **LanguagePack** a tento postup je nutné zopakovat, chcete-li nainstalovat nové konzoly Configuration Manager pouze v angličtině.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Dočasné zakázání jazyku konzoly na existující instalaci konzoly Configuration Manager

1. V počítači se spuštěnou konzolou Configuration Manager zavřete konzolu Configuration Manager.

1. V Průzkumníku Windows přejděte do &lt; *ConsoleInstallationPath*> \Bin\ na počítači konzoly Configuration Manager.  

1. Přejmenujte příslušnou jazykovou složku pro jazyk, který je nakonfigurován na počítači. Pokud bylo například nastavení jazyka počítače nastaveno na němčinu, můžete přejmenovat složku **de** na **de.zakázáno**.  

1. Chcete-li otevřít konzolu Configuration Manager v jazyce, který je nakonfigurován pro počítač, přejmenujte složku na původní název. Například přejmenujte složku **de.zakázáno** na **de**.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a>Konfigurace oprávnění modelu DCOM pro vzdálené konzoly

Uživatelský účet, který spouští konzolu Configuration Manager, vyžaduje oprávnění pro přístup k databázi lokality pomocí poskytovatele služby SMS. Administrativní uživatel, který používá vzdálenou konzolu Configuration Manager, ale také vyžaduje oprávnění modelu DCOM pro **vzdálenou aktivaci** na těchto počítačích:

- Počítač severu lokality

- Každý počítač, který je hostitelem instance poskytovatele serveru SMS

Skupina zabezpečení nazvaná **Správci SMS** uděluje přístup k poskytovateli serveru SMS na počítači a lze jej také použít k udělení požadovaných oprávnění modelu DCOM. Tato skupina je místní k počítači, pokud poskytovatel serveru SMS běží na členském serveru. Jedná se o místní doménovou skupinu, pokud poskytovatel serveru SMS běží na řadiči domény.

> [!IMPORTANT]
> Konzola Configuration Manager používá rozhraní WMI pro připojení k poskytovateli serveru SMS a rozhraní WMI interně používá model DCOM. Pokud se konzola Configuration Manager spouští na jiném počítači, než je počítač poskytovatele serveru SMS, vyžaduje oprávnění k aktivaci serveru DCOM na počítači poskytovatele serveru SMS. Ve výchozím nastavení je Vzdálená aktivace udělena pouze členům předdefinované skupiny Administrators.
>
> Pokud skupině Admins služby SMS povolíte, aby měla oprávnění ke vzdálené aktivaci, člen této skupiny může pokusit o útoky modelu DCOM na počítač poskytovatele serveru SMS. Tato konfigurace též zvyšuje prostor pro útoky na počítač. Pro zmírnění této hrozby pozorně sledujte členství u skupiny SMS Admins.

Následující postup slouží ke konfiguraci jednotlivých lokalit centrální správy (CAS), serveru primární lokality a všech počítačů, ve kterých je nainstalován poskytovatel služby SMS pro udělení přístupu ke vzdálené Configuration Manager konzole pro správce.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Konfigurace oprávnění modelu DCOM pro vzdálená připojení konzoly Configuration Manager

1. Jako správce cílového počítače spusťte `Dcomcnfg.exe` příkaz a otevřete **službu komponent**.

1. Rozbalte položku **Služba komponent**, rozbalte položku **počítače**a potom vyberte možnost **Tento počítač**. V nabídce **Akce** vyberte možnost **vlastnosti**.

1. V okně **vlastnosti tohoto počítače** přepněte na kartu **zabezpečení com** . V části **spouštěcí a aktivační oprávnění** vyberte **Upravit omezení**.

1. V okně **spouštěcí a aktivační oprávnění** vyberte **Přidat**.

1. V okně **Vyberte uživatele, počítače, účty služby nebo skupiny** v poli **Zadejte názvy objektů k výběru** zadejte `SMS Admins`a pak vyberte **OK**.

   > [!TIP]
   > Pokud chcete najít skupinu Admins služby SMS, možná budete muset změnit nastavení: **z tohoto umístění**. Tato skupina je místní k počítači, pokud poskytovatel serveru SMS běží na členském serveru a jedná se o místní doménovou skupinu, pokud poskytovatel serveru SMS běží na řadiči domény.

1. V části **oprávnění pro správce služby SMS** pro povolení vzdálené aktivace vyberte sloupec **povoleno** pro řádek **vzdálené aktivace** .

1. Výběrem **OK** uložte změny a zavřete všechna okna.

Počítač je nyní nakonfigurován tak, aby povoloval vzdáleným Configuration Manager přístup ke členům skupiny Admins služby SMS.

Tento postup opakujte u každého počítače poskytovatele SMS, který podporuje vzdálené konzoly Configuration Manager.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a>Úprava konfigurace databáze lokality

Po instalaci lokality můžete změnit konfiguraci databáze lokality a serveru databáze lokality. Změny provedete spuštěním Configuration Manager instalace na serveru CAS nebo na serveru primární lokality. Databázi lokality můžete přesunout do nové instance systému SQL Server ve stejném počítači nebo do jiného počítače, ve kterém je spuštěna podporovaná verze systému SQL Server. Tyto změny nejsou podporovány pro konfiguraci databáze v sekundárních lokalitách.

Další informace o omezení podpory najdete v tématu [Zásady podpory pro ruční změny databáze v prostředí nástroje Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> Když upravíte konfiguraci databáze pro lokalitu nástroje, Configuration Manager restartuje nebo znovu nainstaluje Configuration Manager služby na server lokality a servery systému vzdálené lokality, které komunikují s databází nástroje.

### <a name="modify-the-database-configuration"></a>Úprava konfigurace databáze

Spusťte instalační program Configuration Manager na serveru lokality a vyberte možnost **provést údržbu lokality nebo resetovat tuto lokalitu**. Pak vyberte možnost **Upravit konfiguraci SQL Server** . Můžete změnit následující konfigurace databáze lokality:

- Server se systémem Windows, který je hostitelem databáze.

- Instance systému SQL Server používaná na serveru, který je hostitelem databáze systému SQL Server.

- název databáze,

- SQL Server Port používaný pomocí Configuration Manager.

- SQL Server Service Broker port používaný pomocí Configuration Manager.

### <a name="move-the-site-database"></a>Přesunutí databáze lokality

Pokud přesouváte databázi lokality, přečtěte si také následující konfigurace:

- Když přesunete databázi lokality do nového počítače, přidejte účet počítače serveru lokality do skupiny místní **Správci** v počítači, na kterém je spuštěný SQL Server. Pokud pro databázi lokality používáte cluster SQL Server, přidejte účet počítače do skupiny místní **Správci** každého počítače uzlu clusteru se systémem Windows Server.

- Když přesunete databázi do nové instance v SQL Server nebo do nového SQL Server počítače, povolte integraci modulu CLR (Common Language Runtime). Pomocí **SQL Server Management Studio** se připojte k instanci SQL Server, která je hostitelem databáze lokality. Pak spusťte následující uloženou proceduru jako dotaz:`sp_configure 'clr enabled',1; reconfigure`

- Ujistěte se, že nový SQL Server má přístup k umístění zálohy. Když použijete cestu UNC k uložení zálohy databáze lokality, po přesunutí databáze na nový server se ujistěte, že účet počítače nového SQL Server má oprávnění k **zápisu** do umístění UNC. Tato konfigurace zahrnuje přesun do skupiny dostupnosti SQL Server AlwaysOn nebo SQL Server clusteru.

> [!IMPORTANT]
> Před přesunutím databáze, která obsahuje jednu nebo více replik databáze pro body správy, nejprve odeberte repliky databáze. Po dokončení přesunu databáze můžete provést opětovnou konfiguraci replik databáze. Další informace najdete v tématu [repliky databáze pro body správy](../deploy/configure/database-replicas-for-management-points.md).

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a>Správa hlavního názvu služby (SPN) pro server databáze lokality

Můžete zvolit účet, který spouští služby SQL Services pro databázi lokality:

- Když se služby spustí s účtem počítače systému, automaticky registruje hlavní název služby (SPN).

- Pokud se služba spouští s místním uživatelským účtem domény, hlavní název služby ručně zaregistrujte. Hlavní název služby (SPN) umožňuje klientům SQL a jiným systémům lokality ověřování pomocí protokolu Kerberos. Bez ověřování Kerberos může selhat komunikace s databází.

Další informace o SPN a připojení Kerberos najdete v tématu [registrace hlavního názvu služby pro připojení Kerberos](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

Zaregistrujte hlavní název služby (SPN) pro účet služby SQL Server serveru databáze lokality pomocí nástroje **Setspn** . Spusťte příkaz Setspn jako správce domény v počítači ve stejné doméně jako SQL Server.

Následující postupy jsou příklady správy hlavního názvu služby (SPN) pro účet služby SQL Server. Další informace o Setspn naleznete v tématu [Setspn Overview](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Ručně vytvořit hlavní název služby (SPN) uživatele domény pro účet služby SQL Server

1. Otevřete příkazový řádek jako správce.

1. Zadejte platný příkaz pro vytvoření hlavního názvu služby (SPN) pro název rozhraní NetBIOS a plně kvalifikovaný název domény:

    > [!IMPORTANT]
    > Když vytváříte hlavní název služby (SPN) pro clusterované SQL Server, zadejte jako název SQL Server počítače virtuální název clusteru SQL Server.

    - Název pro rozhraní NetBIOS:`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Příklad: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - ZADÁNÍ`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Příklad: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > Příkaz k registraci hlavního názvu služby (SPN) pro SQL Server pojmenované instance je stejný jako při registraci hlavního názvu služby (SPN) pro výchozí instanci. Jedinou výjimkou je, že číslo portu musí odpovídat portu, který používá pojmenovaná instance.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Ověřte, jestli je hlavní název uživatele domény správně zaregistrován.

1. Otevřete příkazový řádek jako správce.

1. Zadejte následující příkaz:`setspn -L <domain\SQL service account>`

    Příklad: `setspn -L contoso\sqlservice`

1. Zkontrolujte zaregistrovanou hodnotu **servicePrincipalName**. Ujistěte se, že jste pro SQL Server vytvořili platný hlavní název služby (SPN).

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Změna účtu služby SQL Server z místního systému na uživatelský účet domény

1. Vytvořte nebo vyberte doménu nebo uživatelský účet místního systému, který chcete použít jako účet služby SQL Server.

1. Otevřete nástroj **SQL Server Configuration Manager**.

1. Vyberte **SQL Server Services**a pak otevřete **SQL Server&lt;\>název instance**.

1. Přepněte na kartu **přihlášení** . Vyberte **Tento účet**a pak zadejte uživatelské jméno a heslo pro účet uživatele domény z kroku 1.

1. Potvrďte změnu účtu služby a restartujte službu SQL Server.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a>Spuštění vynulování lokality

Pokud se resetování lokality spustí v certifikační autoritě nebo primární lokalitě, lokalita:

- Znovu použije výchozí oprávnění souboru Configuration Manager a registru.

- Přeinstaluje všechny součásti lokality a všechny role systému lokality.

Sekundární lokality nepodporují vynulování lokality.

Lokalitu můžete resetovat ručně. Můžou se také spouštět automaticky po úpravě konfigurace lokality. Příklad:

- Pokud došlo ke změně účtů používaných součástmi Configuration Manager, zvažte ruční resetování lokality. Tato akce zajistí, že součásti lokality se aktualizují, aby používaly nové podrobnosti účtu.

- Pokud v lokalitě upravíte jazyky klienta nebo serveru, Configuration Manager automaticky spustí Reset lokality. Lokalita vyžaduje resetování, aby používala nové jazyky.

> [!NOTE]
> Resetování lokality neobnoví přístupová oprávnění k objektům, které nejsou Configuration Manager.

### <a name="what-happens-during-a-site-reset"></a>Co se stane při resetování lokality

Proces vynulování lokality:

1. Instalační program zastaví a restartuje službu **SMS_SITE_COMPONENT_MANAGER** a součásti vlákna služby **SMS_Executive** .

1. Instalační program odebere a znovu vytvoří sdílenou složku systému lokality a komponentu **SMS Executive** v místním počítači a ve vzdálených počítačích systému lokality.

1. Instalační program restartuje službu **SMS_SITE_COMPONENT_MANAGER** , která nainstaluje **SMS_Executive** a **SMS_SQL_MONITOR** služby.

Resetování lokality obnoví následující objekty:

- Klíče registru **SMS** nebo **NAL** a jakékoliv výchozí podklíče pod těmito klíči.

- Configuration Manager strom adresářových souborů a všechny výchozí soubory nebo podadresáře v tomto adresářovém stromu souborů.

### <a name="prerequisites-for-site-reset"></a>Předpoklady pro resetování lokality

Účet, který použijete k resetování lokality, musí mít následující oprávnění:

- Resetování certifikačních autorit:

  - Místní **správce** na serveru CAS

  - Oprávnění, která jsou rovnocenná roli zabezpečení správy na základě rolí s **úplnými oprávněními správce**

- Resetování primární lokality:

  - Místní **správce** na serveru primární lokality

  - Oprávnění, která jsou rovnocenná roli zabezpečení správy na základě rolí s **úplnými oprávněními správce**
  
  - Pokud je primární lokalita v hierarchii s certifikační autoritou, musí být tento účet také místním **správcem** na serveru CAS.

### <a name="limitations-for-a-site-reset"></a>Omezení pro resetování lokality

Pokud je hierarchie nakonfigurovaná tak, aby podporovala [testování upgradů klientů v předprodukční kolekci](../../clients/manage/upgrade/test-client-upgrades.md), nemůžete pomocí resetování lokality změnit jazykové sady serveru nebo klienta v lokalitách.

### <a name="run-a-site-reset"></a>Vynulování lokality

1. Spusťte Configuration Manager instalační program na serveru lokality pomocí jedné z následujících metod:

    - V nabídce **Start** vyberte **Configuration Manager nastavení**.

    - V adresáři pro *instalační médium*Configuration Manager otevřete `\SMSSETUP\BIN\X64\setup.exe`. Ujistěte se, že je tato verze stejná jako verze lokality.

    - V adresáři, ve kterém je *nainstalováno*Configuration Manager `\BIN\X64\setup.exe`, otevřete.

1. Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat tuto lokalitu**.

1. Na stránce **Údržba webového serveru** vyberte možnost **resetovat lokalitu bez změn konfigurace**.

1. Výběrem **Ano** zahájíte resetování lokality.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a>Správa jazykových sad v lokalitě

Po instalaci lokality můžete změnit jazykové sady serveru a klienta, které se používají.

### <a name="server-language-packs"></a>Jazykové sady pro server

*Platí pro: instalace konzol Configuration Manager, nové instalace příslušných rolí systému lokality*

Po aktualizaci jazykových sad serveru v lokalitě můžete přidat podporu pro jazykové sady do konzoly Configuration Manager.

Chcete-li přidat podporu pro jazykovou sadu serveru do konzoly Configuration Manager, nainstalujte konzolu Configuration Manager ze složky **ConsoleSetup** na serveru lokality, která obsahuje jazykovou sadu, kterou chcete použít. Je-li již konzola Configuration Manager nainstalována, je nutné ji nejprve odinstalovat, aby mohla nová instalace identifikovat aktuální seznam podporovaných jazykových sad.

### <a name="client-language-packs"></a>Jazykové sady klienta

Změny jazykových sad klienta aktualizují zdrojové soubory instalace klienta. Nové instalace a upgrady klientů přidávají podporu pro aktualizovaný seznam jazyků klienta.

Po aktualizaci jazykových sad klienta v lokalitě nainstalujte každého klienta, který bude používat jazykové sady, pomocí zdrojových souborů, které zahrnují jazykové sady klienta.

Další informace o jazycích klienta a serveru, které Configuration Manager podporuje, najdete v tématu [jazykové sady](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Úprava podporovaných jazykových sad v lokalitě

1. Spusťte Configuration Manager instalační program na serveru lokality pomocí jedné z následujících metod:

    - V nabídce **Start** vyberte **Configuration Manager nastavení**.

    - V adresáři pro *instalační médium*Configuration Manager otevřete `\SMSSETUP\BIN\X64\setup.exe`. Ujistěte se, že je tato verze stejná jako verze lokality.

    - V adresáři, ve kterém je *nainstalováno*Configuration Manager `\BIN\X64\setup.exe`, otevřete.

1. Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat tuto lokalitu**.

1. Na stránce **Údržba lokality** vyberte **Upravit konfiguraci jazyka**.

1. Na stránce **stažení požadovaných součástí** vyberte jednu z následujících možností:

    - **Stáhnout požadované soubory**: získat aktualizace jazykových sad.

    - **Použít dříve stažené soubory**: použijte dříve stažené soubory, které zahrnují jazykové sady, které chcete přidat do lokality.

1. Na stránce **Výběr jazyka serveru** vyberte jazyky serveru, které tato lokalita podporuje.

1. Na stránce **Výběr jazyka klienta** vyberte jazyky klienta, které tato lokalita podporuje.

1. Dokončete průvodce úpravou jazykové podpory v lokalitě.

    > [!NOTE]
    > Configuration Manager inicializuje resetování lokality, které také přeinstaluje všechny role systému lokality v lokalitě.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a>Změnit prahovou hodnotu pro výstrahu databázového serveru

Ve výchozím nastavení Configuration Manager generuje výstrahy, pokud je volné místo na disku na serveru databáze lokality nízké:

- Vygenerovat upozornění, když je na disku 10 GB nebo méně volného místa
- Vygenerovat kritickou výstrahu, pokud je na disku 5 GB nebo méně volného místa

Můžete upravit tyto hodnoty nebo zakázat výstrahy pro jednotlivé lokality:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .

1. Vyberte lokalitu, kterou chcete konfigurovat. Na pásu karet vyberte možnost **vlastnosti**.

1. Přepněte na kartu **Výstraha** a pak upravte nastavení.

## <a name="uninstall-sites-and-hierarchies"></a>Odinstalace lokalit a hierarchií

Možná budete muset odinstalovat Configuration Manager role systému lokality, lokalita nebo hierarchie. Další informace najdete v tématu [odinstalace rolí, lokalit a hierarchií](../deploy/install/uninstall-sites-and-hierarchies.md).

Počínaje verzí 2002 můžete certifikační autority odebrat i z hierarchie, ale zachovat primární lokalitu. Další informace najdete v tématu [Odebrání certifikačních autorit](../deploy/install/remove-central-administration-site.md).
