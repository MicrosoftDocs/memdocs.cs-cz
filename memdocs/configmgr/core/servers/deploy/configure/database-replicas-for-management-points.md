---
title: Repliky databáze bodu správy
titleSuffix: Configuration Manager
description: Pomocí repliky databáze snižte zatížení procesoru na serveru databáze lokality body správy.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db1e0d78263d264c66eed7258db800397baad735
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607585"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Repliky databáze pro body správy pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager primárních lokalitách může pomocí repliky databáze snížit zatížení procesoru na serveru databáze lokality podle bodů správy v případě požadavků na služby od klientů.  

-   Když bod správy používá repliku databáze, tento bod správy vyžaduje data z počítače SQL Serveru, který je hostitelem repliky databáze, místo ze serveru databáze lokality.  

-   To může pomoct snížit požadavky na výpočetní výkon procesoru na serveru databáze lokality přesměrováním častých úloh zpracování spojených s klienty.  Mezi příklady častých úloh zpracování pro klienty patří lokality, kde je velké množství klientů s častými požadavky na zásady klientů.  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> Příprava na použití replik databáze  
**O replikách databáze pro body správy:**  

-   Repliky jsou částečné kopie databáze lokality, která se replikuje do samostatné instance SQL Serveru:  

    -   Primární lokality podporují vyhrazenou repliku databáze pro každý bod správy v lokalitě (sekundární lokality repliky databáze nepodporují).  

    -   Jednu repliku databáze může využívat víc než jeden bod správy ze stejné lokality.  

    -   SQL Server může být hostitelem víc replik databáze používaných různými body správy, pokud každá běží v samostatné instanci SQL Serveru.  

-   Repliky synchronizují kopii databáze lokality podle pevného plánu z dat, která pro tento účel publikuje server databáze lokality.  

-   Body správy se můžou k používání repliky nakonfigurovat při instalaci bodu správy nebo později změnou konfigurace dřív nainstalovaného bodu správy na používání repliky databáze.  

-   Pravidelně sledujte server databáze lokality a všechny servery repliky databáze, abyste zajistili, že mezi nimi probíhá replikace a že výkon serveru repliky databáze je pro danou lokalitu a pro požadovaný výkon klientů dostatečný.  

**Předpoklady pro repliky databáze:**  

-   **SQL Server požadavky:**  

    -   SQL Server, který je hostitelem repliky databáze, musí splňovat stejné požadavky jako server databáze lokality. Server repliky ale nemusí používat stejnou verzi nebo edici SQL Serveru jako server databáze lokality, pokud používá podporovanou verzi a edici SQL Serveru. Informace najdete v článku [podpora SQL Server verzí pro Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   Služba SQL Server Service na počítači, který je hostitelem replikované databáze, musí běžet jako **systémový** účet.  

    -   SQL Server, který je hostitelem databáze lokality, i ten, který je hostitelem repliky databáze, musí mít nainstalovanou **replikaci SQL Serveru** .  

    -   Databáze lokality musí repliku databáze **publikovat** a každý vzdálený server repliky databáze musí publikovaná data **odebírat** .  

    -   SQL Server, který je hostitelem databáze lokality, i ten, který je hostitelem repliky databáze, musí být nakonfigurované, aby podporovaly velikost **Max Text Repl Size** 2 GB. Ukázkové konfigurování pro systém SQL Server 2012 je uvedeno v části [Konfigurování možnosti Max Text Repl Size konfigurace serveru](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option).  

-   **Certifikát podepsaný svým držitelem:** Chcete-li nakonfigurovat repliku databáze, je nutné na serveru repliky databáze vytvořit certifikát podepsaný svým držitelem a tento certifikát zpřístupnit všem bodům správy, které budou používat server repliky databáze.  

    -   Certifikát je automaticky dostupný pro bod správy, který je instalován na serveru repliky databáze.  

    -   Pro zpřístupnění tohoto certifikátu pro vzdálené body správy musíte certifikát exportovat a pak ho přidat do úložiště certifikátů **Důvěryhodných osob** ve vzdáleném bodu správy.  

-   **Klientské oznámení:** Pokud u repliky databáze v bodu správy chcete podporovat klientské oznámení, musíte nakonfigurovat komunikaci mezi serverem databáze lokality a serverem repliky databáze pro službu **SQL Server Service Broker**. To vyžaduje:  

    -   Nakonfigurovat každou databázi pomocí informací o druhé databázi  

    -   Vyměnit certifikáty mezi oběma databázemi kvůli bezpečné komunikaci  

**Omezení při použití replik databáze:**  

-   Když je vaše lokalita nakonfigurovaná pro publikování replik databáze, místo normálních pokynů byste měli použít následující postupy:  

    -   [Odinstalace serveru lokality, který publikuje repliku databáze](#BKMK_DBReplicaOps_Uninstall)  

    -   [Přesunutí databáze serveru lokality, která publikuje repliku databáze](#BKMK_DBReplicaOps_Move)  

-   **Upgrady na Configuration Manager aktuální větev**: před upgradem lokality, buď z nástroje System Center 2012 Configuration Manager na Configuration Manager aktuální větve nebo aktualizace Configuration Manager aktuální větve na nejnovější verzi, je nutné zakázat repliky databáze pro body správy.  Po upgradu lokality můžete repliky databáze pro body správy znovu nakonfigurovat.  

-   **Více replik na jednom SQL Server:**  Pokud nakonfigurujete server repliky databáze pro hostování více replik databáze pro body správy (každá replika musí být v samostatné instanci), musíte použít upravený konfigurační skript (z kroku 4 v následující části), abyste zabránili přepsání používaného certifikátu podepsaného svým držitelem dřív nakonfigurovanými replikami databáze na tomto serveru.  

- Uživatelská nasazení v centru softwaru nebudou fungovat s bodem správy pomocí repliky SQL. <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> Konfigurace replik databáze  
Konfigurace repliky databáze vyžaduje tyto kroky:  

-   [Krok 1 – Konfigurování serveru databáze lokality pro publikování repliky databáze](#BKMK_DBReplica_ConfigSiteDB)  

-   [Krok 2 – konfigurování serveru repliky databáze](#BKMK_DBReplica_ConfigSrv)  

-   [Krok 3 – Konfigurování bodů správy pro používání repliky databáze](#BKMK_DBReplica_ConfigMP)  

-   [Krok 4 – Konfigurování certifikátu podepsaného svým držitelem pro server repliky databáze](#BKMK_DBReplica_Cert)  

-   [Krok 5 – konfigurace SQL Server Service Broker serveru repliky databáze](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a> Krok 1 – konfigurace serveru databáze lokality pro publikování repliky databáze  
 Pro publikování repliky databáze použijte následující postup s ukázkovým konfigurováním serveru databáze lokality na počítači se systémem Windows Server 2008 R2. Máte-li jinou verzi operačního systému, vyhledejte obdobný postup v dokumentaci k operačnímu systému a podle potřeby kroky tohoto postupu upravte.  

##### <a name="to-configure-the-site-database-server"></a>Nakonfigurování serveru databáze lokality  

1.  Na serveru databáze lokality nastavte agenta serveru SQL Server na automatické spuštění.  

2.  Na serveru databáze lokality vytvořte místní skupinu uživatelů s názvem **ConfigMgr_MPReplicaAccess**. Pro každý server repliky databáze, který v této lokalitě používáte, musíte k této skupině přidat účet počítače, aby se servery repliky databáze mohly synchronizovat s publikovanou replikou databáze.  

3.  Na serveru databáze lokality nakonfigurujte sdílený soubor s názvem **ConfigMgr_MPReplica**.  

4.  Do sdílené složky **ConfigMgr_MPReplica** přidejte následující oprávnění:  

    > [!NOTE]  
    >  Jestliže agent serveru SQL Server používá jiný než místní systémový účet, nahraďte SYSTEM názvem účtu z následujícího seznamu.  

    -   **Oprávnění ke sdílení:**  

        -   SYSTEM: **Zapisovat**  

        -   ConfigMgr_MPReplicaAccess: **čtení**  

    -   **Oprávnění NTFS:**  

        -   SYSTEM: **Úplné řízení**  

        -   ConfigMgr_MPReplicaAccess: **čtení**, **čtení & provádění**, **Výpis obsahu složky**  

5.  Pro připojení k databázi lokality a spuštění následující uložené procedury jako dotazu použijte aplikaci **SQL Server Management Studio** : **spCreateMPReplicaPublication**  

Po dokončení uložené procedury je server databáze lokality nakonfigurován pro publikování repliky databáze.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Krok 2 – Konfigurování serveru repliky databáze  
Server repliky databáze je počítač, který spouští SQL Server a je hostitelem repliky databáze lokality pro body správy, které se mají používat. Podle pevného plánu server repliky databáze synchronizuje svou kopii databáze s replikou databáze, které je publikovaná serverem databáze lokality.  

Server repliky databáze musí splňovat stejné požadavky jako server databáze lokality. Server repliky databáze však může spustit jinou edici nebo verzi SQL Serveru než server databáze lokality používá. Informace o podporovaných verzích SQL Server najdete v tématu [podpora SQL Server verzí pro Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) tématu.  

> [!IMPORTANT]  
>  Služba SQL Server Service na počítači, který je hostitelem replikované databáze, musí běžet jako systémový účet.  

Použijte následující postup s ukázkovým konfigurováním serveru repliky databáze na počítači se systémem Windows Server 2008 R2. Máte-li jinou verzi operačního systému, vyhledejte obdobný postup v dokumentaci k operačnímu systému a podle potřeby kroky tohoto postupu upravte.  

##### <a name="to-configure-the-database-replica-server"></a>Nakonfigurování serveru repliky databáze  

1. Na serveru repliky databáze nastavte agenta serveru SQL Server Agent na automatické spuštění.  

2. Na serveru repliky databáze použijte aplikaci **SQL Server Management Studio** , kterou se připojíte k místnímu serveru, vyhledejte složku **Replikace** , klikněte na Místní odběry a vyberte **Nové odběry** , čímž se spustí **Průvodce novým odběrem**:  

   1. Na stránce **Publikace** v seznamu **Vydavatel** vyberte **Najít vydavatele typu SQL Server**, zadejte název serveru databáze lokality a pak klikněte na tlačítko **Připojit**.  

   2. Vyberte **ConfigMgr_MPReplica**a potom klikněte na **Další**.  

   3. Na stránce **umístění agenta distribuce** vyberte **Spustit každého agenta ve svém předplatiteli (vyžádané odběry)** a klikněte na **Další**.  

   4. Na stránce **Odběratelé** proveďte jednu z následujících akcí:  

      -   Ze serveru repliky databáze vyberte stávající databázi, která se má použít pro repliku databáze, a pak klikněte na tlačítko **OK**.  

      -   Vyberte položku **Nová databáze** , aby se vytvořila nová databáze pro repliku databáze. Na stránce **Nová databáze** zadejte název databáze a pak klikněte na tlačítko **OK**.  

   5. Pokračujte kliknutím na **Next** (Další).  

   6. Na stránce **zabezpečení agenta distribuce** klikněte na tlačítko vlastnosti **(....)** v řádku připojení odběratele dialogového okna a pak nakonfigurujte nastavení zabezpečení pro připojení.  

      > [!TIP]  
      >  Tlačítko vlastnosti **(....)** je ve čtvrtém sloupci zobrazovaného pole.  

      **Nastavení zabezpečení:**  

      - Nakonfigurujte účet, který spouští proces agenta distribuce (účet procesu):  

        -   Pokud Agent SQL Server běží jako místní systém, vyberte **Spustit pod účtem služby SQL Server agenta (nejedná se o doporučený postup zabezpečení.)**  

        -   Jestliže agent SQL Server běží za použití jiného účtu, vyberte **Spustit pod následujícím účtem systému Windows** a pak tento účet nakonfigurujte. Můžete zadat účet systému Windows nebo účet SQL Serveru.  

        > [!IMPORTANT]  
        >  Účtu, který spouští agenta distribuce, musíte přidělit oprávnění vůči vydavateli jako vyžádané odběry. Informace o konfiguraci těchto oprávnění najdete v tématu [zabezpečení agenta distribuce](/sql/relational-databases/replication/distribution-agent-security).  

      - Pro položku **Připojit k distributorovi**vyberte **Zosobněním účtu procesu**.  

      - Pro položku **Připojit k odběrateli**vyberte **Zosobněním účtu procesu**.  

        Po nakonfigurování nastavení zabezpečení pro připojení klikněte na tlačítko **OK** , čímž se nastavení uloží, a pak klikněte na tlačítko **Další**.  

   7. Na stránce **Plán synchronizace** v seznamu **Plán agenta** vyberte **Definovat plán** a pak nakonfigurujte **Plán nové úlohy**. Nastavte četnost výskytu **denně**, opakovat každých **5 minut**a dobu trvání **bez koncového data**. Klikněte na tlačítko **Další**, čímž plán uložíte, a pak znovu klikněte na tlačítko **Další**.  

   8. Na stránce **Akce průvodce** zaškrtněte políčko **vytvořit odběry**a potom klikněte na tlačítko **Další**.  

   9. Na stránce **Dokončit průvodce** klikněte na tlačítko **Dokončit** a pak klikněte na tlačítko **Zavřít**, čímž se průvodce dokončí.  

3. Okamžitě po dokončení Průvodce novým odběrem se pomocí aplikace **SQL Server Management Studio** připojte k databázi serveru repliky databáze a spusťte následující dotaz, který povolí vlastnost databáze TRUSTWORTHY:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Zkontrolujte stav synchronizace, abyste ověřili, že odběr je úspěšný:  

   -   Na počítači odběratele:  

       -   V aplikaci **SQL Server Management Studio** se připojte k serveru repliky databáze a rozbalte nabídku **Replikace**.  

       -   Rozbalte **místní odběry**, klikněte pravým tlačítkem na odběr publikace databáze lokality a pak vyberte **Zobrazit stav synchronizace**.  

   -   Na počítači vydavatele:  

       -   V **SQL Server Management Studio**se připojte k počítači databáze lokality, klikněte pravým tlačítkem na složku **replikace** a pak vyberte **Spustit monitorování replikace**.  

5. Chcete-li povolit integraci modulu CLR (Common Language Runtime) pro repliku databáze, použijte **SQL Server Management Studio** pro připojení k replice databáze na serveru repliky databáze a spusťte následující uloženou proceduru jako dotaz: **EXEC sp_configure ' CLR Enabled ', 1; překonfigurovat pomocí přepsání**  

6. Pro každý bod správy, který používá server repliky databáze, přidejte příslušný účet počítače bodů správy ke skupině **Správci** příslušného serveru repliky databáze.  

   > [!TIP]  
   >  Tento krok není nutný pro bod správy, který běží na serveru repliky databáze.  

   Replika databáze je nyní připravena, aby ji bod správy mohl používat.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a> Krok 3 – konfigurace bodů správy pro použití repliky databáze  
 Bod správy v primární lokalitě můžete při instalaci role bodu správy nakonfigurovat na používání repliky databáze nebo můžete stávající bod správy znovu nakonfigurovat na používání repliky databáze.  

 Pro nakonfigurování bodu správy na používání repliky databáze použijte následující informace:  

-   **Konfigurace nového bodu správy:** Na stránce **Databáze bodu správy** průvodce používaného pro instalaci bodu správy vyberte **Použít repliku databáze**a zadejte úplný název domény počítače, který je hostitelem repliky databáze. Dále pro **Název databáze lokality nástroje ConfigMgr** zadejte název repliky databáze na tomto počítači.  

-   **Konfigurace dřív nainstalovaného bodu správy:** Otevřete stránku vlastnosti bodu správy, vyberte kartu **Databáze bodu správy** , vyberte **Použít repliku databáze**a pak zadejte úplný název domény počítače, který je hostitelem repliky databáze. Dále pro **Název databáze lokality nástroje ConfigMgr** zadejte název repliky databáze na tomto počítači.  

-   **Pro každý bod správy, který používá repliku databáze**, musíte ručně přidat počítačový účet serveru bodu správy do role **db_datareader** pro repliku databáze.  

Kromě konfigurace bodu správy pro používání serveru repliky databáze musíte povolit **Ověřování systému Windows** ve službě **IIS** v bodu správy:  

1.  Otevřete **správce Internetová informační služba (IIS)**.  

2.  Vyberte web používaný bodem správy a otevřete **Ověřování**.  

3.  Nastavte **ověřování systému Windows** na **povoleno**a pak zavřete **správce Internetová informační služba (IIS)**.  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> Krok 4 – konfigurování certifikátu podepsaného svým držitelem pro server repliky databáze  
 Na serveru repliky databáze musíte vytvořit certifikát podepsaný svým držitelem a tento certifikát zpřístupnit všem bodům správy, které budou server repliky databáze používat.  

 Certifikát je automaticky dostupný pro bod správy, který je instalován na serveru repliky databáze. Pro zpřístupnění tohoto certifikátu pro vzdálené body správy však musíte certifikát exportovat a pak ho přidat do úložiště certifikátů důvěryhodných osob ve vzdáleném bodu správy.  

 Následující postupy použijte jako příklad konfigurace certifikátu podepsaného svým držitelem na serveru repliky databáze pro počítač se systémem Windows Server 2008 R2. Máte-li jinou verzi operačního systému, vyhledejte obdobný postup v dokumentaci k operačnímu systému a podle potřeby kroky těchto postupů upravte.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Konfigurace certifikátu podepsaného svým držitelem pro server repliky databáze  

1.  Na serveru repliky databáze otevřete příkazový řádek prostředí PowerShell s oprávněními správce a pak spusťte následující příkaz: **Set-ExecutionPolicy Restricted** .  

2.  Zkopírujte následující skript Windows PowerShell a uložte ho jako soubor s názvem **CreateMPReplicaCert.ps1**. Umístěte kopii tohoto souboru do kořenové složky systémového oddílu serveru repliky databáze.  

    > [!IMPORTANT]  
    >  Pokud konfigurujete víc než jednu repliku databáze na jednom SQL Serveru, pro každou další repliku, kterou konfigurujete, musíte použít upravenou verzi skriptu pro tento postup. Viz  [Doplňkový skript pro další databáze repliky na jednom SQL Serveru](#bkmk_supscript)  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  Na serveru repliky databáze spusťte následující příkaz, který se týká konfigurace vašeho SQL Serveru:  

    -   Pro výchozí instanci SQL Server: klikněte pravým tlačítkem na soubor **CreateMPReplicaCert.ps1** a vyberte **Spustit s prostředím PowerShell**. Po spuštění skriptu se vytvoří certifikát podepsaný svým držitelem a nakonfiguruje SQL Server k použití certifikátu.  

    -   Pro pojmenovanou instanci SQL Server: pomocí PowerShellu spusťte příkaz **% path% \CreateMPReplicaCert.ps1 xxxxxx** , kde **xxxxxx** je název instance SQL Server.  

    -   Po dokončení skriptu ověřte, zda je spuštěn agent SQL Serveru. Pokud není, znovu ho spusťte.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Konfigurace bodů vzdálené správy pro použití certifikátu podepsaného svým držitelem serveru repliky databáze  

1.  Proveďte následující kroky na serveru repliky databáze a exportujte certifikát podepsaný svým držitelem serveru:  

    1.  V nabídce **Start**klikněte na **Spustit**a zadejte **mmc.exe**. V prázdné konzole klikněte na položku **Soubor**a vyberte možnost **Přidat nebo odebrat modul snap-in**.  

    2.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** vyberte ze seznamu **Moduly snap-in k dispozici** položku **Certifikáty**a pak klikněte na **Přidat**.  

    3.  V dialogovém okně **Snap-in Certifikáty** zvolte položku **Účet počítače** a klikněte na tlačítko **Další**.  

    4.  V dialogovém okně **Vybrat počítač** ověřte výběr **Místní počítač: (počítač, na kterém je spuštěna tato konzola)** a poté klikněte na **Dokončit**.  

    5.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** klikněte na tlačítko **OK**.  

    6.  V konzole rozbalte položku **Certifikáty (místní počítač)**, rozbalte položku **Osobní** a vyberte složku **Certifikáty**.  

    7.  Klikněte pravým tlačítkem na certifikát s popisným názvem **SQL Server pro identifikaci certifikátu nástroje ConfigMgr**, klikněte na položku **všechny úlohy**a poté vyberte možnost **exportovat**.  

    8.  Dokončete **Průvodce exportem certifikátu** za použití výchozích možností a uložte certifikát s příponou názvu souboru **.cer** .  

2.  V počítači bodu správy proveďte následující kroky k přidání certifikátu podepsaného svým držitelem pro server repliky databáze do úložiště certifikátů Důvěryhodné osoby v bodu správy:  

    1.  Podle předchozích kroků 1.a až 1.e Konfigurace modulu snap-in **certifikáty** konzoly MMC v počítači bodu správy.  

    2.  V konzole rozbalte položku **Certifikáty (místní počítač)**, rozbalte položku **Důvěryhodné osoby**, klikněte pravým tlačítkem myši na položku **Certifikáty**, vyberte položku **Všechny úlohy** a poté zvolením možnosti **Importovat** spusťte **Průvodce importem certifikátu**.  

    3.  Na stránce **Importovat soubor** vyberte certifikát uložený v kroku 1.h a klikněte na tlačítko **Další**.  

    4.  Na stránce **Úložiště certifikátů** zvolte možnost **Všechny certifikáty umístit v následujícím úložišti**, s parametrem **Úložiště certifikátů** nastaveným na hodnotu **Důvěryhodné osoby**, a poté klikněte na tlačítko **Další**.  

    5.  Kliknutím na **Dokončit** zavřete průvodce a dokončete konfiguraci certifikátu v bodu správy.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> Krok 5 – Konfigurování služby SQL Server Service Broker pro server repliky databáze  
Chcete-li u repliky databáze v bodu správy podporovat klientské oznámení, je nutné nakonfigurovat komunikaci mezi serverem databáze lokality a serverem repliky databáze pro službu SQL Server Service Broker. K tomu je zapotřebí nakonfigurovat každou databázi pomocí informací o jiné databázi a provést výměnu certifikátů mezi těmito dvěma databázemi k zabezpečení komunikace.  

> [!NOTE]  
>  Než bude možné použít následující postup, musí server repliky databáze úspěšně dokončit počáteční synchronizaci se serverem databáze lokality.  

 Následující postup neupravuje port služby Service Broker, který je v SQL Serveru nakonfigurovaný pro server databáze lokality nebo server repliky databáze. Místo toho tento postup konfiguruje každou databázi, aby komunikovala s druhou databází prostřednictvím správného portu služby Service Broker.  

 Následující postup slouží ke konfiguraci služby Service Broker pro server databáze lokality a server repliky databáze.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Nakonfigurování služby Service Broker pro repliku databáze  

1. Pomocí **SQL Server Management Studio** se připojte k databázi serveru repliky databáze a pak spusťte následující dotaz, který povolí Service Broker na serveru repliky databáze: **změnit &lt; název databáze repliky databáze na \> hodnotu ENABLE_BROKER, HONOR_BROKER_PRIORITY s vrácením zpět okamžitě** .  

2. Následně na serveru repliky databáze nakonfigurujte službu Service Broker na klientské oznámení a exportujte certifikát služby Service Broker. Abyste tak mohli učinit, spusťte uložený postup SQL Serveru, který nakonfiguruje službu Service Broker a exportuje certifikát v rámci jediné akce. Při spuštění uloženého postupu je nutné zadat úplný název domény (FQDN) pro server repliky databáze, název databáze replik databází a umístění pro export souboru certifikátu.  

    Spuštěním následujícího dotazu nakonfigurujte požadované podrobnosti na serveru repliky databáze a exportujte certifikát pro server repliky databáze: **EXEC sp_BgbConfigSSBForReplicaDB ' &lt; replika SQL Server FQDN \> ', ' &lt; název databáze repliky ' \> , ' &lt; cesta k souboru zálohy certifikátu \> '**  

   > [!NOTE]  
   >  Pokud server repliky databáze není ve výchozí instanci SQL Serveru, je nutné v tomto kroku zadat kromě názvu repliky databáze také název instance. Provedete to tak, že nahradíte ** &lt; název \> databáze repliky** názvem ** &lt; \\ \> instance název databáze repliky**.  

    Po exportu certifikátu ze serveru repliky databáze umístěte kopii certifikátu na server databáze primárních lokalit.  

3. Pomocí aplikace **SQL Server Management Studio** se připojte k databázi primárních lokalit. Po připojení k databázi primárních lokalit spusťte dotaz, kterým importujete certifikát a určíte port služby Service Broker používaný na serveru repliky databáze, FQDN serveru repliky databáze a název databáze replik databází. Tím se konfiguruje databáze primárních lokalit na použití služby Service Broker ke komunikaci s databází serveru repliky databáze.  

    Spuštěním následujícího dotazu importujte certifikát ze serveru repliky databáze a určete požadované podrobnosti: **EXEC sp_BgbConfigSSBForRemoteService ' replika ', ' &lt; SQL Service Broker port \> ', ' &lt; cesta souboru certifikátu \> ', ' &lt; REPLIKa SQL Server plně kvalifikovaný název domény ' \> , ' &lt; název databáze repliky \> '**  

   > [!NOTE]  
   >  Pokud server repliky databáze není ve výchozí instanci SQL Serveru, je nutné v tomto kroku zadat kromě názvu repliky databáze také název instance. Provedete to tak, že nahradíte ** &lt; \> název databáze repliky** názvem **\Instance název \\ databáze \> repliky**.  

4. Potom na serveru databáze lokality spuštěním následujícího příkazu exportujte certifikát pro server databáze lokality: **EXEC sp_BgbCreateAndBackupSQLCert ' &lt; cesta k souboru zálohy certifikátu \> '**  

    Po exportu certifikátu ze serveru databáze lokality umístěte kopii certifikátu na server repliky databáze.  

5. Pomocí aplikace **SQL Server Management Studio** se připojte k databázi serveru repliky databáze. Po připojení k databázi serveru repliky databáze spusťte dotaz pro import certifikátu a zadejte kód primární lokality a port služby Service Broker používaný na serveru databáze lokality. Tím se nakonfiguruje server repliky databáze na použití služby Service Broker ke komunikaci s databází primární lokality.  

    Spuštěním následujícího dotazu importujte certifikát ze serveru databáze lokality: **EXEC sp_BgbConfigSSBForRemoteService ' &lt; kód lokality \> ', ' &lt; SQL Service Broker port \> ', ' &lt; cesta souboru certifikátu \> '**  

   Několik minut poté, co dokončíte konfiguraci databáze lokality a databáze replik databází, nastaví správce oznámení v primární lokalitě konverzaci služby Service Broker pro klientské oznámení z databáze primární lokality do repliky databáze.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> Doplňkový skript pro další repliky databáze na jednom SQL Server  
 Když použijete skript z kroku 4 ke konfiguraci certifikátu podepsaného svým držitelem pro server repliky databáze na SQL Server, která už má repliku databáze, kterou plánujete dál používat, musíte použít upravenou verzi původního skriptu. Následující úpravy zabrání skriptu v odstranění existujícího certifikátu na serveru a vytvoří další certifikáty s jedinečnými popisnými názvy.  Původní skript upravte takto:  

-   Odkomentovat (zabránit spuštění) každý řádek mezi položkami skriptu **# Odstranit existující certifikát, pokud existuje** , a **# vytvořit nový certifikát**. Chcete-li to provést, přidejte  **#**  jako první znak každého relevantního řádku.  

-   U každé další repliky databáze, kterou pomocí tohohle skriptu nakonfigurujete, aktualizujte popisný název certifikátu.  Provedete to tak, že upravíte řádek **$Enrollment. CertificateFriendlyName = "certifikát pro identifikaci nástroje ConfigMgr SQL Server** a nahraďte **SQL Server identifikační certifikát nástroje ConfigMgr** novým názvem, například  **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a> Správa konfigurací repliky databáze  
 Při použití repliky databáze v lokalitě použijte informace v následujících částech k doplnění procesu odinstalace repliky databáze, odinstalace lokality používající repliku databáze nebo přesunu databáze lokality do nové instalace SQL Serveru. Pokud použijete informace z následujících částí k odstranění publikací, použijte návod na odstranění transakční replikace pro verzi serveru SQL Server používanou pro repliku databáze. Další informace najdete v tématu [Odstranění publikace](/sql/relational-databases/replication/publish/delete-a-publication).  

> [!NOTE]  
>  Než bude po obnovení databáze lokality nakonfigurované pro repliky databází možné použít repliky databáze, je nutné překonfigurovat jednotlivé repliky databáze a znovu vytvořit publikace i odběry.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Odinstalování repliky databáze  
 Při použití repliky databáze pro bod správy může být zapotřebí repliku databáze na nějakou dobu odinstalovat a poté ji znovu nakonfigurovat k opětovnému použití. Například je třeba odebrat repliky databáze před upgradem Configuration Manager lokality na novou aktualizaci Service Pack. Po dokončení upgradu lokality je možné repliku databáze obnovit a znovu používat.  

 Pomocí následujícího postupu odinstalujete repliku databáze.  

1.  V pracovním prostoru **Správa** konzoly Configuration Manager rozbalte položku **Konfigurace lokality**, vyberte možnost **servery a role systému lokality**a potom v podokně podrobností vyberte server systému lokality, který je hostitelem bodu správy používajícího repliku databáze, kterou budete odinstalovat.  

2.  V podokně **Role systému lokality** klikněte pravým tlačítkem myši na **Bod správy** a zvolte položku **Vlastnosti**.  

3.  Na kartě **Databáze bodu správy** zvolte možnost **Použít databázi lokality** , která nakonfiguruje bod správy k použití databáze lokality místo repliky databáze. Potom kliknutím na **OK** tuto konfiguraci uložte.  

4.  Následně pomocí aplikace **SQL Server Management Studio** proveďte následující úlohy:  

    -   Odstraňte publikaci repliky databáze z databáze serveru lokality.  

    -   Odstraňte odběr repliky databáze ze serveru repliky databáze.  

    -   Odstraňte repliku databáze ze serveru repliky databáze.  

    -   Zakažte publikování a distribuci na serveru databáze lokality. Publikování a distribuci zakážete tak, že kliknete pravým tlačítkem na složku replikace a pak kliknete na **Zakázat publikování a distribuci**.  

5.  Jakmile odstraníte publikaci, odběr, repliku databáze a zakážete publikování na serveru databáze lokality, replika databáze bude odinstalována.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Odinstalování serveru lokality, který publikuje repliku databáze  
 Před odinstalací lokality, jež publikuje repliku databáze, proveďte následující postup za účelem vyčištění publikace a případných odběrů.  

1.  Pomocí aplikace **SQL Server Management Studio** odstraňte publikaci repliky databáze z databáze serveru lokality.  

2.  Pomocí aplikace **SQL Server Management Studio** odstraňte odběr repliky databáze z každého vzdáleného SQL Serveru, který je hostitelem repliky databáze pro tuto lokalitu.  

3.  Odinstalujte lokalitu.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> Přesunutí databáze serveru lokality, který publikuje repliku databáze  
 Při přesunování databáze lokality do nového počítače použijte následující kroky:  

1.  Pomocí aplikace **SQL Server Management Studio** odstraňte publikaci repliky databáze z databáze serveru lokality.  

2.  Pomocí aplikace **SQL Server Management Studio** odstraňte odběr repliky databáze z každého serveru repliky databáze pro tuto lokalitu.  

3.  Přesuňte databázi do nového počítače s SQL Serverem. Další informace najdete v části [Úprava konfigurace databáze lokality](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) v tématu [Úprava infrastruktury Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md) .  

4.  Vytvořte znovu publikaci repliky databáze na serveru databáze lokality. Další informace najdete v části [Krok 1 – Konfigurování serveru databáze lokality pro publikování repliky databáze](#BKMK_DBReplica_ConfigSiteDB) v tomto tématu.  

5.  Vytvořte znovu odběry repliky databáze na každém serveru repliky databáze. Další informace najdete v části [Krok 2 – Konfigurování serveru repliky databáze](#BKMK_DBReplica_ConfigSrv) v tomto tématu.