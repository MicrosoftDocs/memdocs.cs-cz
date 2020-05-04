---
title: Nastavení testovacího prostředí
titleSuffix: Configuration Manager
description: Nastavte testovací prostředí pro vyhodnocení Configuration Manager se simulovanými reálnými aktivitami.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a23f6106a8c922b3ff4e8306fb76aec4fd26b148
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711606"
---
# <a name="set-up-a-configuration-manager-lab"></a>Nastavení testovacího prostředí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Podle pokynů v tomto tématu vám umožní nastavit testovací prostředí pro vyhodnocení Configuration Manager se simulovanými reálnými aktivitami.  

> [!NOTE]
> Microsoft nabízí předem konfigurovanou verzi tohoto testovacího prostředí s využitím zkušební verze Configuration Manager. Další informace najdete v tématu [Sada Windows a sada Office Deployment and Management Lab Kit](https://docs.microsoft.com/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab). 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Základní součásti  
 Nastavení prostředí pro Configuration Manager vyžaduje, aby některé základní součásti podporovaly instalaci Configuration Manager.    

-   **Testovací prostředí používá Windows Server 2012 R2**, do kterého budeme instalovat Configuration Manager.  

     Zkušební verzi Windows Serveru 2012 R2 si můžete stáhnout z [webu TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Zvažte úpravu nebo zakázání konfigurace rozšířeného zabezpečení aplikace Internet Explorer, aby bylo snazší získat přístup k některým souborům ke stažení, na které se odkazuje v průběhu těchto cvičení. Další aspekty technologie WCF najdete v tématu [Internet Explorer: Konfigurace rozšířeného zabezpečení](https://technet.microsoft.com/library/dd883248\(v=ws.10\).aspx) .  

-   **Testovací prostředí používá SQL Server 2012 SP2** pro databázi lokality.  

     Zkušební verzi SQL Server 2012 si můžete stáhnout z webu [Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=43340).  

     SQL Server má [podporované verze SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) , které musí být splněné pro použití s Configuration Manager.  

    -   Configuration Manager vyžaduje pro hostování databáze lokality 64 verze SQL Server.  

    -   **SQL_Latin1_General_CP1_CI_AS** jako třída **řazení SQL** .  

    -   **ověřování systému Windows**[namísto ověřování SQL](https://technet.microsoft.com/library/ms144284.aspx) is required.  

    -   Je požadována vyhrazená **instance SQL Server** .  

    -   Neomezovat **systémovou adresovatelnou paměť** pro SQL Server.  

    -   Nakonfigurujte **účet služby SQL Server** pro spuštění pomocí účtu uživatele domény s nízkými právy.  

    -   Je nutné nainstalovat **službu SQL Server Reporting Services**.  

    -   **Komunikace mezi lokalitami** používá nástroj SQL Server Service Broker na výchozím portu TCP 4022.  

    -   **Komunikace** v lokalitě mezi databázovým strojem SQL Server a výběr Configuration Manager role systému lokality používají výchozí port TCP 1433.  

-   **Řadič domény používá Windows Server 2008 R2** s nainstalovaným Active Directory Domain Services. Řadič domény taky funguje jako hostitel pro servery DHCP a DNS k použití s plně kvalifikovaným názvem domény.  

     Další informace najdete v tomto [přehledu Active Directory Domain Services](https://technet.microsoft.com/library/hh831484).  

-   **Technologie Hyper-V se používá s několika virtuálními počítači** , aby se ověřilo, že kroky správy prováděné v těchto cvičeních fungují podle očekávání. Doporučuje se mít minimálně tři virtuální počítače s nainstalovaným Windows 10.  

     Další informace najdete v tomto [přehledu technologie Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).  

-   **Oprávnění správce** bude potřebné pro všechny tyto součásti.  

    -   Configuration Manager vyžaduje správce s místními oprávněními v prostředí Windows serveru.  

    -   Služby Active Directory vyžaduje správce s oprávněním k úpravě schématu.  

    -   Virtuální počítače vyžadují místní oprávnění na příslušných počítačích.  

I když to pro toto testovací prostředí není nutné, můžete si projít [podporované konfigurace pro Configuration Manager](../../core/plan-design/configs/supported-configurations.md) , kde najdete další informace o požadavcích na implementaci Configuration Manager. Další informace najdete v dokumentaci k jiným verzím softwaru, než je zde odkazováno.  

Po instalaci všech těchto součástí je potřeba provést další kroky, abyste mohli nakonfigurovat prostředí Windows pro Configuration Manager:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Příprava obsahu služby Active Directory pro testovací prostředí  
 Pro toto testovací prostředí vytvoříte skupinu zabezpečení a pak do ní přidáte uživatele domény.  

-   Skupiny zabezpečení: **Evaluation**  

    -   Obor skupiny: **Universal**  

    -   Typ skupiny: **zabezpečení**  

-   Uživatel domény: **ConfigUser**  

     Za normálních okolností byste v rámci vašeho prostředí neudělovali univerzální přístup všem uživatelům. S tímto uživatelem to děláte, aby se zjednodušilo uvedení testovacího prostředí online.  

Další kroky potřebné k tomu, aby Configuration Manager klienti mohli zadat dotaz Active Directory Domain Services vyhledání prostředků lokality, najdete v následujících postupech.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Vytvoření kontejneru System Management  
 Pokud je schéma rozšířeno, Configuration Manager nevytvoří automaticky požadovaný kontejner System Management v Active Directory Domain Services. Proto ho pro testovací prostředí vytvoříte vy. Tento krok bude vyžadovat [instalaci nástroje ADSI Edit](https://technet.microsoft.com/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit).  

 Zkontrolujte, že jste přihlášení jako účet, který má oprávnění **Vytvořit všechny podřízené objekty** na kontejneru **Systém** ve službě Active Directory Domain Services.  

#### <a name="to-create-the-system-management-container"></a>Vytvoření kontejneru System Management:  

1.  Spusťte nástroj **ADSI Edit**a připojte k doméně, ve které se nachází server lokality.  

2.  Rozbalte **plně&lt;kvalifikovaný název\>domény počítače domény**, rozbalte **<rozlišující název\>**, klikněte pravým tlačítkem na **CN = System**, klikněte na **Nový**a pak klikněte na **objekt**.  

3.  V dialogovém okně **Vytvořit objekt** zvolte položku **Kontejner**a pak klikněte na tlačítko **Další**.  

4.  Do pole **Hodnota** zadejte **System Management**, a poté klikněte na **Další**.  

5.  Proceduru dokončete kliknutím na tlačítko **Dokončit** .  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Nastavení oprávnění zabezpečení pro kontejner System Management  
 Účtu počítače serveru lokality udělte oprávnění, která se požadují k publikování informací o lokalitě do kontejneru. Pro tuto úlohu také použijete nástroj ADSI Edit.  

> [!IMPORTANT]  
>  Před zahájením následujícího postupu potvrďte, že jste připojení k doméně serveru lokality.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Nastavení oprávnění zabezpečení pro kontejner System Management:  

1.  V podokně konzoly rozbalte **doménu serveru lokality**, rozbalte **&lt;DC = Server rozlišující název\>** a potom rozbalte **CN = System**. Klikněte pravým tlačítkem na **CN = System Management**a pak klikněte na **vlastnosti**.  

2.  V dialogovém okně **Vlastnosti CN=System Management** klikněte na kartu **Zabezpečení** a pak kliknutím na **Přidat** přidejte účet počítače serveru lokality. Udělte účtu oprávnění **Úplné řízení** .  

3.  Klikněte na tlačítko **Upřesnit**, vyberte účet počítače serveru lokality a pak klikněte na tlačítko **Upravit**.  

4.  V seznamu **Použít na** zvolte **Tento objekt a všechny následné objekty**.  

5.  Kliknutím na **OK** zavřete konzolu **ADSI Edit** a dokončete postup.  

     Další přehled tohoto postupu najdete v [části rozšiřování schématu služby Active Directory pro Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Rozšíření schématu služby Active Directory pomocí souboru extadsch.exe  
 Rozšíříte schéma služby Active Directory pro toto testovací prostředí, protože vám to umožní používat všechny Configuration Manager funkce a funkce s minimálním množstvím režijních nákladů na správu. Rozšíření schématu služby Active Directory je konfigurace ovlivňující celou doménovou strukturu, která se v doménové struktuře provádí jenom jednou. Rozšíření schématu trvale upravuje sadu tříd a atributů v základní konfiguraci služby Active Directory. Tato akce je nevratná. Rozšíření schématu umožňuje Configuration Manager získat přístup k součástem, které jim umožní efektivně fungovat v testovacím prostředí.  

> [!IMPORTANT]  
>  Zkontrolujte, že jste přihlášení k řadiči domény originálu schématu pomocí účtu, který je členem skupiny zabezpečení **Schema Admins** . Pokus o použití alternativních přihlašovacích údajů se nepovede.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Rozšíření schématu služby Active Directory pomocí souboru extadsch.exe:  

1.  Vytvořte zálohu stavu systému řadiče domény hlavního serveru schémat. Další informace o zálohování řadiče domény originálu najdete v tématu [Zálohování Windows Serveru](https://technet.microsoft.com/library/cc770757.aspx)  

2.  Na instalačním médiu přejděte do složky **\SMSSETUP\BIN\X64** :  

3.  Spusťte **extadsch.exe**.  

4.  Kontrolou souboru **extadsch.log** umístěného v kořenovém adresáři diskové jednotky systému ověřte, že rozšíření schématu bylo úspěšné.  

     Další přehled tohoto postupu najdete v [části rozšiřování schématu služby Active Directory pro Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Další požadované úlohy  
 Před instalací budete taky muset provést následující úlohy.  

 **Vytvoření složky pro uložení všech souborů ke stažení**  

 Během tohoto cvičení bude potřeba provést víc stažení kvůli součástem na instalačním médiu. Před zahájením jakéhokoli postupu instalace určete umístění, které nebude vyžadovat přesunutí těchto souborů až do vyřazení testovacího prostředí z provozu. K ukládání těchto souborů ke stažení se doporučuje jedna složka se samostatnými podsložkami.  

 **Instalace rozhraní .NET a aktivace technologie Windows Communication Foundation**  

 Budete muset nainstalovat dvě rozhraní .NET Framework: jako první rozhraní .NET 3.5.1, a potom .NET 4.5.2+. Musíte taky aktivovat technologii Windows Communication Foundation (WCF). Technologie WCF je určená k poskytování spravovaného přístupu k distribuovanému zpracování dat, široké interoperability a přímé podpory pro orientaci na služby a usnadňuje vývoj propojených aplikací prostřednictvím programovacího modelu orientovaného na služby. Další aspekty technologie WCF najdete v tématu [Co je Windows Communication Foundation?](https://technet.microsoft.com/subscriptions/ms731082\(v=vs.90\).aspx) .  

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Instalace rozhraní .NET a aktivace technologie Windows Communication Foundation:  

1.  Otevřete **Server Manager**a potom přejděte na **Spravovat**. Kliknutím na **Přidat role a funkce** otevřete **Průvodce přidáním rolí a funkcí.**  

2.  Přečtěte si informace uvedené na panelu **Než začnete** a pak klikněte na **Další**.  

3.  Vyberte **Instalace na základě rolí nebo na základě funkcí**a pak klikněte na **Další**.  

4.  Vyberte server z **Fondu serverů**a pak klikněte na **Další**.  

5.  Zkontrolujte panel **Role serveru** a pak klikněte na **Další**.  

6.  Přidejte následující **Funkce** jejich výběrem ze seznamu:  

    -   **Funkce .NET Framework 3.5**  

        -   **.NET Framework 3.5 (zahrnuje rozhraní .NET 2.0 a 3.0)**  

    -   **Funkce rozhraní .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **Služby WCF**  

            -   **Aktivace protokolem HTTP**  

            -   **Sdílení portů TCP**  

7.  Zkontrolujte obrazovky **Role webového serveru (IIS)** a **Služby rolí** a pak klikněte na **Další**.  

8.  Zkontrolujte obrazovku **Potvrzení** a pak klikněte na **Další**.  

9. Klikněte na **Instalovat** a v podokně **Oznámení****Správce serveru**ověřte, že se instalace dokončila správně .  

10. Po dokončení základní instalace rozhraní .NET přejděte do služby [Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=42643) a získejte webovou instalační službu pro rozhraní .NET Framework 4.5.2. Klikněte na tlačítko **Stáhnout** a pak na **Spustit** , aby se spustil instalační program. Automaticky se rozpoznají a nainstalují požadované součásti ve vybraném jazyce.  

Další informace o tom, proč jsou tato rozhraní .NET Framework potřeba, najdete v následujících článcích:  

-   [Verze a závislosti rozhraní .NET Framework](https://technet.microsoft.com/library/bb822049.aspx)  

-   [Návod ke kompatibilitě aplikací rozhraní .NET Framework 4 RTM](https://technet.microsoft.com/library/dd889541.aspx)  

-   [Postupy: Upgrade webové aplikace ASP.NET na ASP.NET 4](https://technet.microsoft.com/library/dd483478\(VS.100\).aspx)  

-   [Nejčastější dotazy k zásadám životního cyklu podpory rozhraní Microsoft .NET Framework](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [CLR uvnitř souběžného procesu](https://msdn.microsoft.com/magazine/ee819091.aspx)  

**Povolení služby BITS, IIS a RDC**  

[Služba BITS (Background Intelligent Transfer Service)](https://technet.microsoft.com/library/dn282296.aspx) se používá pro aplikace, které potřebují asynchronně přenášet soubory mezi klientem a serverem. Podle měření toku přenosů na popředí a na pozadí zachovává služba BITS odezvy ostatních síťových aplikací. Taky automaticky pokračuje v přenosech souborů, když dojde k přerušení relace přenosu.  

Službu BITS nainstalujete pro toto testovací prostředí, protože server lokality se bude taky používat jako bod správy.  

Internetové informační služby (IIS) je flexibilní, škálovatelný webový server, který jde použít k hostování čehokoli na webu. Používá ho Configuration Manager pro několik rolí systému lokality. Další informace o službě IIS najdete na [webech pro servery systému lokality](../../core/plan-design/network/websites-for-site-system-servers.md).  

[Remote Differential Compression (RDC)](https://technet.microsoft.com/library/cc754372.aspx) je sada rozhraní API, které můžou aplikace použít k určení, jestli nebyly v sadách souborů provedené nějaké změny. RDC umožňuje aplikaci replikovat jenom změněné části souboru, čímž udržuje síťový provoz na minimu.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Povolení rolí serveru lokality BITS, IIS a RDC:  

1.  Na serveru lokality otevřete **Server Manager**. Přejděte do části **Správa**. Kliknutím na **Přidat role a funkce** otevřete **Průvodce přidání rolí a funkcí**.  

2.  Přečtěte si informace uvedené na panelu **Než začnete** a pak klikněte na **Další**.  

3.  Vyberte **Instalace na základě rolí nebo na základě funkcí**a pak klikněte na **Další**.  

4.  Vyberte server z **Fondu serverů**a pak klikněte na **Další**.  

5.  Přidejte následující **Role serveru** jejich výběrem ze seznamu:  

    -   **Webový server (IIS)**  

        -   **Společné funkce protokolu HTTP**  

            -   **Výchozí dokument**  

            -   **Procházení adresářů**  

            -   **Chyby protokolu HTTP**  

            -   **Statický obsah**  

            -   **Přesměrování protokolu HTTP**  

        -   **Stav a diagnostika**  

            -   **Protokolování HTTP**  

            -   **Nástroje protokolování**  

            -   **Sledování požadavků**  

            -   **Trasování**  

    -   **Výkon**  

        -   **Komprese statického obsahu**  

        -   **Komprese dynamického obsahu**  

    -   **Zabezpečení**  

        -   **Filtrování požadavků**  

        -   **Základní ověření**  

        -   **Ověřování mapování klientských certifikátů**  

        -   **Omezení podle IP adresy a domény**  

        -   **Autorizace adres URL**  

        -   **Ověřování systému Windows**  

    -   **Vývoj aplikací**  

        -   **Rozšiřitelnost rozhraní .NET 3.5**  

        -   **Rozšiřitelnost rozhraní .NET 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **Rozšíření ISAPI**  

        -   **Filtry ISAPI**  

        -   **Začlenění na straně serveru**  

    -   **Server FTP**  

        -   **Služba FTP**  

    -   **Nástroje pro správu**  

        -   **Konzola pro správu služby IIS**  

        -   **Kompatibilita správy služby IIS 6**  

            -   **Kompatibilita metabáze služby IIS 6**  

            -   **Konzola pro správu služby IIS 6**  

            -   **Nástroje pro skriptování služby IIS 6**  

            -   **Kompatibilita rozhraní WMI služby IIS 6**  

        -   **Skripty a nástroje správy služby IIS 6**  

        -   **Služba správy**  

6.  Přidejte následující **Funkce** jejich výběrem ze seznamu:  

    -   **Služba inteligentního přenosu na pozadí (BITS)**  

          -   **Rozšíření serveru IIS**  

    -   **Nástroje pro vzdálenou správu serveru**  

          -   **Nástroje pro správu funkcí**  

          -   **Nástroje rozšíření serveru BITS**  

7.  Klikněte na **Instalovat** a v podokně **Oznámení****Správce serveru**ověřte, že se instalace dokončila správně .  

Služba IIS standardně blokuje přístup protokolu HTTP nebo HTTPS k některým typům přípon názvu souborů a umístění. Pokud chcete, aby se tyto soubory distribuovaly na klientské systémy, budete muset nakonfigurovat filtrování žádostí služby IIS v distribučním bodě. Další informace najdete v tématu [IIS Request Filtering for distribution points](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Konfigurace filtrování služby IIS v distribučních bodech:  

1.  Otevřete **IIS Manager** a na bočním panelu vyberte název serveru. Tím přejdete na obrazovku **Domů** .  

2.  Ověřte, že je v dolní části obrazovky **Domů** vybrané **Zobrazení funkcí** . Přejděte k **IIS** a otevřete **Filtrování žádostí**.  

3.  V podokně **Akce** klikněte na **Povolit příponu názvu souboru**.  

4.  Do dialogového okna zadejte **.msi** a klikněte na **OK**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Instalace Configuration Manageru  
[Určíte, kdy se má primární lokalita používat](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) ke správě klientů přímo. Tím umožníte, aby vaše testovací prostředí podporovalo správu pro škálování možných zařízení v [systému lokality](../plan-design/configs/size-and-scale-numbers.md) .  
Během tohoto procesu nainstalujete také konzolu Configuration Manager, která se bude používat ke správě zkušebních zařízení před tím, než se dokončí.  

Před zahájením instalace spusťte  [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) na serveru s Windows Server 2012, abyste potvrdili, že všechna nastavení byla správně povolená.  

#### <a name="to-download-and-install-configuration-manager"></a>Stažení a instalace nástroje Configuration Manager:  

1.  Přejděte na stránku [vyhodnocení produktu System Center](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) a stáhněte nejnovější zkušební verzi Configuration Manager.  

2.  Rozbalte stažené médium do předdefinovaného místa.  

3.  Postupujte podle pokynů k instalaci uvedených v části [instalace lokality pomocí Průvodce instalací nástroje Configuration Manager](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md). V rámci tohoto postupu budete zadávat následující položky:  

    |Krok v postupu instalace lokality|Výběr|  
    |-----------------------------------------|---------------|  
    |Krok 4: Stránka **Kód Product Key**|Vyberte **Vyhodnocení**.|  
    |Krok 7:  **Požadované soubory ke stažení**|Vyberte **Stáhnout požadované soubory** a zadejte předdefinované umístění.|  
    |Krok 10: **Nastavení lokality a instalace**|-   **Kód lokality:LAB**<br />-   **Název lokality:Evaluation**<br />-   **Instalační složka:** Zadejte předdefinované umístění.|  
    |Krok 11: **Instalace primární lokality**|Vyberte **Nainstalovat primární lokalitu jako samostatnou lokalitu**a pak klikněte na **Další**.|  
    |Krok 12: **Instalace databáze**|-   **Název SQL Serveru (FQDN):** Zadejte sem plně kvalifikovaný název domény.<br />-   **Název instance:** Nechte prázdné, protože budete používat výchozí instanci SQL, kterou jste nainstalovali dřív.<br />-   **Port služby Service Broker:** Ponechte jako výchozí port 4022.|  
    |Krok 13: **Instalace databáze**|Tato nastavení ponechte jako výchozí.|  
    |Krok 14: **poskytovatel serveru SMS**|Tato nastavení ponechte jako výchozí.|  
    |Krok 15: **Nastavení komunikace s klientem**|Zkontrolujte, že není vybrané **Všechny role systémů serverů lokality přijímají od klientů pouze komunikaci pomocí protokolu HTTPS** .|  
    |Krok 16: **Role systému lokality**|Zadejte plně kvalifikovaný název domény a zkontrolujte, že stále není vybraná možnost **Všechny role systémů serverů lokality přijímají od klientů pouze komunikaci pomocí protokolu HTTPS** .|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a>Povolit publikování pro Configuration Manager Web  
Každá lokalita Configuration Manager zveřejňuje do kontejneru System Management své vlastní informace v rámci svého oddílu domény ve schématu služby Active Directory. Pro zpracování tohoto provozu musí být otevřené obousměrné kanály pro komunikaci mezi službou Active Directory a Configuration Manager. Dál taky povolíte metodu zjišťování lokalit a podsítí v doménových strukturách pro určení konkrétních komponent infrastruktury sítě a služby Active Directory.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Konfigurace doménových struktur služby Active Directory pro publikování:  

1.  V levém dolním rohu konzoly Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte možnost **Konfigurace hierarchie**a pak klikněte na položku **Metody zjišťování**.  

3.  Vyberte **Zjišťování lokalit a podsítí v doménových strukturách služby Active Directory** a klikněte na **Vlastnosti**.  

4.  V dialogovém okně **Vlastnosti** vyberte **Povolit zjišťování doménové struktury služby Active Directory**. Po aktivaci vyberte **Automaticky vytvářet meze lokality služby Active Directory při jejich zjištění**. Zobrazí se dialogové okno s oznámením **Chcete co nejdříve spustit plné zjišťování?** Klikněte na tlačítko **Ano**.  

5.  Ve skupině **Metoda zjišťování** v horní části obrazovky klikněte na tlačítko **Spustit zjišťování lokalit a podsítí v doménových strukturách ihned**a pak na bočním panelu přejděte na **Doménové struktury služby Active Directory** . Doménové struktury služby Active Directory by se měly zobrazit v seznamu zjištěných doménových struktur.  

6.  Přejděte do horní části obrazovky na kartu **Obecné** .  

7.  V pracovním prostoru **Správa** rozbalte možnost **Konfigurace hierarchie**a pak klikněte na položku **Doménové struktury služby Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Povolení publikování informací o lokalitě Configuration Manager v doménové struktuře služby Active Directory:  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  Nakonfigurujete novou doménovou strukturu, která ještě nebyla zjištěná.  

3.  V pracovním prostoru **Správa** klikněte na možnost **Doménové struktury služby Active Directory**.  

4.  Na kartě **Publikování** vlastností lokality vyberte připojenou doménovou strukturu a pak kliknutím na **OK** konfiguraci uložte.
