---
title: Nasazení klientů se systémem UNIX/Linux
titleSuffix: Configuration Manager
description: Přečtěte si, jak nasadit klienta nástroje na server se systémem UNIX nebo Linux v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906318"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Postup nasazení klientů na servery se systémy UNIX a Linux v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.


Než budete moct spravovat server se systémem Linux nebo UNIX pomocí Configuration Manager, musíte na každý server se systémem Linux nebo UNIX nainstalovat klienta Configuration Manager pro systémy Linux a UNIX. Instalaci můžete na každém počítači provést ručně nebo můžete použít skript prostředí, který klienta nainstaluje vzdáleně. Configuration Manager nepodporuje použití klientské nabízené instalace pro servery se systémem Linux nebo UNIX. Volitelně můžete nakonfigurovat sadu Runbook pro nástroj System Center Orchestrator, která umožní automatizaci instalace klienta na server se systémem Linux nebo UNIX.  

 Nehledě na to, jakou metodu instalace použijete, musíte během procesu instalace použít skript s názvem **install** , který slouží ke správě procesu instalace. Tento skript je součástí staženého klienta pro Linux a UNIX.  

 Instalační skript pro klienta Configuration Manager pro systémy Linux a UNIX podporuje vlastnosti příkazového řádku. Některé vlastnosti příkazového řádku jsou povinné, zatímco jiné jsou nepovinné. Při instalaci klienta musíte třeba zadat bod správy z lokality, který má server se systémem Linux nebo UNIX použít při prvním kontaktu s lokalitou. Úplný seznam vlastností příkazového řádku najdete v tématu [Vlastnosti příkazového řádku pro instalaci klienta na servery se systémy Linux a UNIX](#BKMK_CmdLineInstallLnUClient).  

 Po instalaci klienta zadáte nastavení klienta v konzole Configuration Manager ke konfiguraci klientského agenta stejným způsobem jako klienti se systémem Windows. Další informace najdete v oddílu  [Nastavení klienta pro servery se systémy Linux a UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>O instalačních balíčcích klienta a univerzálním agentovi  
 Pokud chcete klienta pro Linux a UNIX nainstalovat na konkrétní platformu, musíte na počítači, ve kterém klienta instalujete, použít příslušný instalační balíček klienta. Příslušné instalační balíčky klienta jsou součástí každého stažení klienta z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Vedle instalačních balíčků klienta zahrnuje stažení klienta také skript **install** , který spravuje instalaci klienta v jednotlivých počítačích.  

 Při instalaci klienta můžete použít stejný postup a vlastnosti příkazového řádku bez ohledu na to, který instalační balíček klienta použijete.  

 Informace o operačních systémech, platformách a instalačních balíčcích klienta podporovaných jednotlivými verzemi klienta Configuration Manager pro systémy Linux a UNIX najdete v tématu [servery se systémy Linux a UNIX](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers).  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a>Instalace klienta na servery se systémy Linux a UNIX  
 Pokud chcete nainstalovat klienta pro Linux a UNIX, spusťte na každém počítači se systémem Linux nebo UNIX skript. Tento skript má název **install** a podporuje vlastnosti příkazového řádku, které upravují chování při instalaci a odkazují na instalační balíček klienta. Skript install a instalační balíček klienta se musí nacházet v klientovi. Instalační balíček klienta obsahuje soubory klienta Configuration Manager pro konkrétní operační systém Linux nebo UNIX a platformu.
Každý instalační balíček klienta obsahuje všechny soubory potřebné k dokončení instalace klienta a na rozdíl od počítačů se systémem Windows nestahují další soubory z bodu správy ani jiného zdrojového umístění.  

 Po instalaci klienta Configuration Manager pro systémy Linux a UNIX nemusíte restartovat počítač. Po dokončení instalace softwaru bude klient hned v provozu. Pokud restartujete počítač, klient Configuration Manager se automaticky restartuje.  

 Nainstalovaný klient se spustí s přihlašovacími údaji uživatele root. Pověření ke kořenu jsou nutná ke shromáždění inventáře hardwaru a nasazení softwaru.  

 Použijte následující formát příkazu:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install`je název souboru skriptu, který nainstaluje klienta pro Linux a UNIX. Tento soubor je součástí softwaru klienta.  

-   `-mp <computer>`Určuje počáteční bod správy používaný klientem. Příklad: `smsmp.contoso.com`  

-   `-sitecode <site code>`Určuje kód lokality, ke které je klient přiřazen. Příklad: `S01`  

-   `<property #1> <property #2>`Určuje vlastnosti příkazového řádku, které se mají použít spolu s instalačním skriptem.  

    > [!NOTE]  
    >  Další informace najdete v tématu [Vlastnosti příkazového řádku pro instalaci klienta na servery se systémy Linux a UNIX](#BKMK_CmdLineInstallLnUClient).  

-   **instalační balíček klienta** je název instalačního balíčku .tar klienta pro operační systém, verzi a architekturu procesoru daného počítače. Instalační soubor .tar klienta musí být uvedený jako poslední. Příklad: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a>Instalace klienta Configuration Manager na servery se systémy Linux a UNIX  

1.  Na počítači s Windows [stáhněte příslušný soubor klienta pro server se systémem Linux nebo UNIX](https://www.microsoft.com/download/details.aspx?id=47719), který chcete spravovat.  

2.  Na počítači s Windows spusťte samorozbalovací soubor .exe, který extrahuje instalační skript a instalační soubor klienta .tar.  

3.  Zkopírujte skript **install** a soubor .tar do složky na serveru, který chcete spravovat.  

4.  Na serveru se systémem UNIX nebo Linux spusťte následující příkaz, který umožní spuštění skriptu jako programu:`chmod +x install`  

    > [!IMPORTANT]  
    >  K instalaci klienta potřebujete přihlašovací údaje uživatele root.  

5.  Dále spusťte následující příkaz pro instalaci klienta Configuration Manager:`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Při zadávání tohoto příkazu použijte další vlastnosti příkazového řádku podle svých požadavků. Seznam vlastností příkazového řádku najdete v tématu [Vlastnosti příkazového řádku pro instalaci klienta na servery se systémy Linux a UNIX](#BKMK_CmdLineInstallLnUClient) .  

6.  Po spuštění skriptu ověřte instalaci tak, že zkontrolujete soubor **/var/opt/microsoft/scxcm.log** . Kromě toho si můžete ověřit, že je klient nainstalován a komunikuje s lokalitou, zobrazením podrobností o klientovi v uzlu **zařízení** v pracovním prostoru prostředky **a kompatibilita** v konzole nástroje Configuration Manager.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a>Vlastnosti příkazového řádku pro instalaci klienta na servery se systémy Linux a UNIX  
 Pro úpravu chování instalačního skriptu jsou k dispozici následující vlastnosti:  

> [!NOTE]  
>  `-h`Tento seznam podporovaných vlastností zobrazíte pomocí vlastnosti.  

-   `-mp <server FQDN>`  

     Povinná hodnota. Určuje server bodu správy, který klient používá jako počáteční kontaktní bod, pomocí plně kvalifikovaného názvu domény.  

    > [!IMPORTANT]  
    >  Tato vlastnost neurčuje bod správy, ke kterému je klient přiřazen po instalaci.  

    > [!NOTE]  
    >  Pokud použijete `-mp` vlastnost k určení bodu správy, který je nakonfigurován tak, aby přijímal pouze připojení klientů přes protokol HTTPS, musíte také použít `-UsePKICert` vlastnost.  

-   `-sitecode <sitecode>`  

     Povinná hodnota. Určuje Configuration Manager primární lokalitu, ke které se má klient Configuration Manager přiřadit. Příklad: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Nepovinný parametr. Určuje server bodu stavu pro použití náhradní lokality, který má klient používat k odesílání stavových zpráv. Další informace najdete v tématu [určení, zda potřebujete bod stavu pro použití náhradní lokality](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     Nepovinný parametr. Určuje alternativní umístění pro instalaci Configuration Manager klientských souborů. Ve výchozím nastavení se klient nainstaluje do následujícího umístění:`/opt/microsoft`  

-   `-nostart`  

     Nepovinný parametr. Zabrání automatickému spuštění služby klienta Configuration Manager **Ccmexec. bin**po dokončení instalace klienta.  

     Po instalaci klienta musíte službu klienta spustit ručně.  

     Ve výchozím nastavení se tato služba klienta spustí po dokončení instalace klienta a po každém restartování počítače.  

-   `-clean`  

     Nepovinný parametr. Určuje odebrání všech souborů klienta a dat z dřív nainstalovaného klienta pro Linux a UNIX před zahájením nové instalace. Tato akce odebere databázi a úložiště certifikátů klienta.  

-   `-keepdb`  

     Nepovinný parametr. Určuje, že se má místní databáze klienta zachovat a znovu použít při přeinstalaci klienta. Ve výchozím nastavení se databáze při nové instalaci klienta odstraní.  

-   `-UsePKICert <parameter>`  

     Nepovinný parametr. Určuje úplnou cestu a název souboru certifikátu PKI X.509 PKI ve formátu PKCS#12 (Public Key Certificate Standard). Tento certifikát se používá k ověřování klienta. Pokud během instalace certifikát nezadáte a potřebujete ho později přidat nebo změnit, použijte nástroj **certutil** . Další informace najdete v tématu [Správa certifikátů v klientovi pro systémy Linux a UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Když použijete `-UsePKICert` , musíte také zadat heslo přidružené k souboru PKCS # 12 pomocí `-certpw` parametru příkazového řádku.  

     Pokud pomocí této vlastnosti neurčíte certifikát PKI, klient použije certifikát podepsaný svým držitelem a veškerá komunikace se systémy lokality bude využívat protokol HTTP.  

     Pokud na příkazový řádek pro instalaci klienta zadáte neplatný certifikát, nevrátí se žádné chyby. Ověření certifikátu probíhá po instalaci klienta. Po spuštění klienta se certifikáty ověřují s bodem správy. Pokud se certifikát nezdařil, zobrazí se v **scxcm. log**následující zpráva: **nepodařilo se ověřit certifikát pro bod správy**. Výchozí umístění souboru protokolu je:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Tuto vlastnost je nutné zadat při instalaci klienta a `-mp` vlastnost použijte k určení bodu správy, který je nakonfigurován tak, aby přijímal pouze připojení klientů pomocí protokolu HTTPS.  

     Příklad: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Nepovinný parametr. Určuje heslo přidružené k souboru PKCS # 12, který jste zadali pomocí `-UsePKICert` Vlastnosti.  

     Příklad: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Nepovinný parametr. Určuje, že klient by neměl kontrolovat seznam odvolaných certifikátů (CRL) při komunikaci přes protokol HTTPS pomocí certifikátu PKI. Pokud není tato možnost zadána, klient před vytvořením připojení HTTPS pomocí certifikátů PKI zkontroluje seznam CRL. Další informace o kontrole seznamu CRL klienta najdete v tématu Plánování zrušení certifikátů PKI.  

     Příklad: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Nepovinný parametr. Určuje úplnou cestu a název souboru Configuration Manager důvěryhodného kořenového klíče. Configuration Manager důvěryhodný kořenový klíč poskytuje mechanismus, pomocí kterého klienti se systémy Linux a UNIX ověřují, zda jsou připojeni k systému lokality, který patří do správné hierarchie.  

     Pokud v příkazovém řádku nezadáte důvěryhodný kořenový klíč, klient bude důvěřovat prvnímu bodu správy, se kterým bude komunikovat, a automaticky z tohoto bodu správy získá důvěryhodný kořenový klíč.  

     Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Příklad: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Nepovinný parametr. Určuje port nakonfigurovaný v bodech správy, který má klient použít při komunikaci s body správy přes protokol HTTP. Pokud port není zadaný, použije se výchozí hodnota 80.  

     Příklad: `-httpport 80`  

-   `-httpsport <port>`  

     Nepovinný parametr. Určuje port nakonfigurovaný v bodech správy, který má klient použít při komunikaci s body správy přes protokol HTTPS. Pokud port není zadaný, použije se výchozí hodnota 443.  

     Příklad: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Nepovinný parametr. Určuje, že má instalační skript klienta přeskočit ověřování SHA-256. Tuto možnost použijte při instalaci klienta nástroje v operačních systémech, které neobsahovaly verzi OpenSSL, která podporuje SHA-256. Další informace najdete v tématu [informace o operačních systémech Linux a UNIX, které nepodporují algoritmus SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Nepovinný parametr. Určuje úplnou cestu a název souboru **. cer** exportovaného certifikátu podepsaného svým držitelem na serveru lokality. Pokud nejsou certifikáty PKI dostupné, server lokality Configuration Manager automaticky vygeneruje certifikáty podepsané svým držitelem.  

     Tyto certifikáty se používají k ověření toho, jestli zásady klienta stažené z bodu správy odeslala zamýšlená lokalita. Pokud během instalace nezadáte certifikát podepsaný svým držitelem nebo pokud ho potřebujete změnit, použijte nástroj **certutil** . Další informace najdete v tématu [Správa certifikátů v klientovi pro systémy Linux a UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Tento certifikát lze načíst z úložiště certifikátů **SMS** a má název subjektu **Server lokality** a popisný název **Podpisový certifikát serveru lokality**.  

     Pokud tato možnost není určena během instalace, klienti se systémy Linux a UNIX považují za první bod správy, se kterým komunikuje. Z tohoto bodu správy automaticky načtou podpisový certifikát.  

     Příklad: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Nepovinný parametr. Určuje další certifikáty PKI k importu, které nejsou součástí hierarchie certifikační autority (CA) bodu správy. Pokud na příkazový řádek zadáte několik certifikátů, měly by být oddělené čárkami.  

     Tuto možnost použijte, pokud používáte certifikáty PKI klienta, které se nezřetězeny na certifikát kořenové certifikační autority, který je důvěryhodný pro body správy vašich lokalit. Body správy odmítnou klienta, pokud certifikát klienta neřetězí k důvěryhodnému kořenovému certifikátu v seznamu vystavitelů certifikátů lokality.  

     Pokud tuto možnost nepoužijete, klient se systémem Linux a UNIX ověří hierarchii důvěryhodnosti pouze pomocí certifikátu v této `-UsePKICert` Možnosti.  

     Příklad: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a>Odinstalování klienta ze serverů se systémy Linux a UNIX  
 Chcete-li odinstalovat klienta Configuration Manager pro systémy Linux a UNIX, použijte nástroj pro odinstalaci, **odinstalujte**. Ve výchozím nastavení je tento soubor uložený v klientském počítači ve složce **/opt/microsoft/configmgr/bin/** . Tento příkaz k odinstalaci nepodporuje žádné parametry příkazového řádku a odebere ze serveru všechny soubory související se softwarem klienta.  

 Chcete-li odinstalovat klienta, použijte tento příkazový řádek: **/opt/microsoft/configmgr/bin/uninstall**  

 Po odinstalaci klienta Configuration Manager pro systémy Linux a UNIX není nutné restartovat počítač.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a>Konfigurace portů žádostí pro klienta pro Linux a UNIX  
 Podobně jako klienti se systémem Windows klient Configuration Manager pro systémy Linux a UNIX používá ke komunikaci se systémy lokality Configuration Manager protokol HTTP a HTTPS. Porty, které klient Configuration Manager používá ke komunikaci, se označují jako porty požadavků.  

 Při instalaci klienta Configuration Manager pro systémy Linux a UNIX můžete změnit výchozí porty požadavků klientů zadáním vlastností instalace **-HttpPort** a **-HttpsPort** . Pokud nezadáte vlastnost instalace a vlastní hodnotu, klient použije výchozí hodnoty. Výchozí hodnoty jsou **80** pro přenosy přes protokol HTTP a **443** pro přenosy přes protokol HTTPS.  

 Po instalaci klienta nemůžete změnit jeho konfiguraci portu požadavků. Pokud potřebujete jinou konfiguraci portů, musíte klienta znovu nainstalovat a zadat při tom novou konfiguraci portů. Pokud přeinstalujete klienta, aby změnil čísla portů požadavku, spusťte příkaz **install** podobný instalaci nového klienta, ale použijte další vlastnost příkazového řádku **keepdb**. Tento přepínač dá instalaci pokyn, aby se zachovala databáze a soubory klienta, včetně identifikátoru GUID klientů a úložiště certifikátů.  

 Další informace o číslech portů pro komunikaci s klienty najdete v tématu [Postup konfigurace portů pro komunikaci klientů](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a>Konfigurace klienta pro Linux a UNIX, aby vyhledal body správy  
 Když instalujete klienta Configuration Manager pro systémy Linux a UNIX, musíte zadat bod správy, který se použije jako počáteční kontaktní bod.  

 Klient Configuration Manager pro systémy Linux a UNIX kontaktuje tento bod správy v době instalace klienta. Pokud se klientovi nepodaří kontaktovat tento bod správy, software klienta bude pokusy opakovat, dokud nebude úspěšný.  

 Další informace o tom, jak klienti vyhledávají body správy, najdete v tématu [Hledání bodů správy](assign-clients-to-a-site.md#locating-management-points).
