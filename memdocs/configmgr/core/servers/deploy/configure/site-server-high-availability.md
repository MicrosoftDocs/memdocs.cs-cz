---
title: Vysoká dostupnost serveru lokality
titleSuffix: Configuration Manager
description: Postup konfigurace vysoké dostupnosti pro Configuration Manager serveru lokality přidáním serveru lokality v pasivním režimu.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718305"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Vysoká dostupnost serveru lokality v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1128774-->

Historicky jste mohli do většiny rolí v Configuration Manager přidat redundanci tím, že ve svém prostředí budete mít víc instancí těchto rolí. S výjimkou samotného serveru lokality. Vysoká dostupnost pro roli serveru lokality je řešení založené na Configuration Manager k instalaci dalšího serveru lokality v *pasivním* režimu. Lokalita centrální správy a podřízené primární lokality mohou mít další server lokality v pasivním režimu. Server lokality v pasivním režimu může být místní nebo cloudový v Azure.

Tato funkce přináší následující výhody:

- Redundance a vysoká dostupnost role serveru lokality  
- Snadnější změna hardwaru nebo operačního systému serveru lokality  
- Jednodušší přesunutí serveru lokality do Azure IaaS  

Server lokality v pasivním režimu je navíc k vašemu stávajícímu serveru lokality, který je v *aktivním* režimu. Server lokality v pasivním režimu je k dispozici pro okamžité použití v případě potřeby. Tento další server lokality uveďte jako součást celkového návrhu pro zajištění [vysoké dostupnosti](high-availability-options.md)služby Configuration Manager.  

Server lokality v pasivním režimu:

- Používá stejnou databázi lokality jako server lokality v aktivním režimu.
- Nepíše data do databáze lokality, pokud je v pasivním režimu.
- Používá stejnou knihovnu obsahu jako server lokality v aktivním režimu.

Aby se server lokality v pasivním režimu stal aktivní, ručně ho *povýšíte* . Tato akce přepne server lokality v aktivním režimu na server lokality v pasivním režimu. Role systému lokality, které jsou k dispozici na původním serveru aktivního režimu, zůstávají k dispozici, pokud je tento počítač přístupný. Mezi aktivním a pasivním režimem je přepnuta pouze role serveru lokality.

Technologie Microsoft Core Services a operace, které tuto funkci využívají k migraci lokality centrální správy na Microsoft Azure. Další informace najdete v [článku prezentující Microsoft](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Požadavky

- Knihovna obsahu webu musí být ve vzdálené sdílené síťové složce. Oba servery lokality potřebují oprávnění Úplné řízení ke sdílené složce a jejímu obsahu. Další informace najdete v tématu [Správa knihovny obsahu](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).<!--1357525-->  

  - Účet počítače serveru lokality potřebuje oprávnění **Úplné řízení** k síťové cestě, do které přesouváte knihovnu obsahu. Toto oprávnění platí jak pro sdílenou složku, tak pro systém souborů. Ve vzdáleném systému nejsou nainstalovány žádné součásti.

  - Webový server nemůže mít roli distribučního bodu. Distribuční bod také používá knihovnu obsahu a tato role nepodporuje vzdálenou knihovnu obsahu. Po přesunutí knihovny obsahu nelze přidat roli distribučního bodu do serveru lokality.  

- Server lokality v pasivním režimu může být místní nebo cloudový v Azure.  

    > [!NOTE]
    > Cloudový server lokality v pasivním režimu používá infrastrukturu Azure jako službu (IaaS). Další informace najdete v těchto článcích:
    >
    >   - [Virtuální počítače Azure (pro cloudovou infrastrukturu)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Nejčastější dotazy k Configuration Manager v Azure](../../../understand/configuration-manager-on-azure.md)  

- Oba servery lokality musí být připojeny ke stejné doméně služby Active Directory.  

- Configuration Manager podporuje servery lokality v pasivním režimu v hierarchii. Lokalita centrální správy a podřízené primární lokality mohou mít další server lokality v pasivním režimu.<!-- 3607755 -->  

- Oba servery lokality musí používat stejnou databázi lokality.  

  - Databázi lze z každého serveru lokality vzdáleně provést. Počínaje verzí 1810 nebude proces instalace Configuration Manager nadále blokovat instalaci role serveru lokality do počítače s rolí systému Windows pro clustering s podporou převzetí služeb při selhání. SQL Always On vyžaduje tuto roli, takže dříve se nepovedlo společně najít databázi lokality na serveru lokality. Díky této změně můžete vytvořit vysoce dostupnou lokalitu s menším počtem serverů pomocí SQL Always On a serveru lokality v pasivním režimu.<!-- SCCMDocs issue 1074 -->  

  - SQL Server, která je hostitelem databáze lokality, může používat výchozí instanci, pojmenovanou instanci, [SQL Server cluster](use-a-sql-server-cluster-for-the-site-database.md)nebo [SQL Server skupiny dostupnosti Always On](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Oba servery lokality potřebují roli zabezpečení **sysadmin** na instanci SQL Server, která je hostitelem databáze lokality. Původní server lokality by již měl mít tyto role, proto jej přidejte pro nový server lokality. Například následující skript SQL přidá tyto role pro nový server lokality **VM2** v doméně contoso:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Oba servery lokality potřebují přístup k databázi lokality na instanci SQL Server. Původní server lokality by již měl mít tento přístup, proto jej přidejte pro nový server lokality. Například následující skript SQL přidá přihlášení do databáze **CM_ABC** pro nový server lokality **VM2** v doméně contoso:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - Server lokality v pasivním režimu je nakonfigurován pro použití stejné databáze lokality jako serveru lokality v aktivním režimu. Server lokality v pasivním režimu čte pouze z databáze. Nezapisuje do databáze, dokud se nezvýší na aktivní režim.  

- Server lokality v pasivním režimu:  

  - Musí splňovat požadavky pro instalaci primární lokality. Například .NET Framework, Remote Differential Compression a Windows ADK. Úplný seznam najdete v tématu [požadavky na lokalitu a systém lokality](../../../plan-design/configs/site-and-site-system-prerequisites.md).<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Nezapomeňte nainstalovat SQL Server Native Client. Pokud ho nenainstalujete, Kontrola požadovaných součástí během Configuration Manager Setup nahlásí chybu týkající se chybějících oprávnění SQL Server.<!-- SCCMDocs#2290 -->

  - Musí mít účet počítače v místní skupině Administrators na serveru lokality v aktivním režimu.<!--516036-->

  - Je nutné nainstalovat pomocí zdrojových souborů, které odpovídají verzi serveru lokality v aktivním režimu.  

  - Před instalací serveru lokality do role pasivního režimu nemůže být v žádné nainstalované lokalitě role systému lokality.  

- Obě webové servery můžou spouštět různé verze operačního systému nebo aktualizace Service Pack, pokud [Configuration Manager podporuje](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)obě.  

- Nehostovat roli spojovacího bodu služby na jednom serveru lokality nakonfigurovaném pro vysokou dostupnost. Pokud je aktuálně na původním serveru lokality, odeberte ho a nainstalujte na jiný server systému lokality. Další informace najdete v tématu [o spojovacím bodu služby](about-the-service-connection-point.md).  

- Oprávnění pro [účet instalace systému lokality](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)  

  - Ve výchozím nastavení spousta zákazníků používá účet počítače serveru lokality k instalaci nových systémů lokality. Požadavek pak přidá účet počítače serveru lokality do místní skupiny **Administrators** ve vzdáleném systému lokality. Pokud vaše prostředí používá tuto konfiguraci, nezapomeňte přidat počítačový účet nového serveru lokality do této místní skupiny na všech systémech vzdálené lokality. Například všechny vzdálené distribuční body.  

  - Bezpečnější a doporučenou konfigurací je použití účtu služby pro instalaci systému lokality. Nejbezpečnější konfigurací je použití účtu místní služby. Pokud vaše prostředí používá tuto konfiguraci, není potřeba žádná změna.  

## <a name="limitations"></a>Omezení

- V každé lokalitě je podporován pouze jeden server lokality v pasivním režimu.  

- Server lokality v pasivním režimu není podporován v sekundární lokalitě.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Sekundární lokality jsou stále podporovány v primární lokalitě s vysoce dostupnými servery lokality.

- Propagační akce serveru lokality v pasivním režimu do aktivního režimu je ruční. Neexistuje žádné automatické převzetí služeb při selhání.  

- Role systému lokality nelze nainstalovat na nový server před přidáním serveru lokality v pasivním režimu.  

    > [!NOTE]
    > Po instalaci serveru lokality v pasivním režimu můžete podle potřeby přidat další role. Například bod správy v primární lokalitě.

- U rolí, jako je bod hlášení, který používá databázi, je třeba hostovat databázi na serveru, který je vzdálený od obou serverů lokality.  

- Konzola Configuration Manager není automaticky nainstalována na server lokality v pasivním režimu.  

## <a name="add-a-site-server-in-passive-mode"></a>Přidání serveru lokality v pasivním režimu

Další informace o obecném procesu přidávání rolí najdete v tématu [Instalace rolí systému lokality](install-site-system-roles.md).

1. V konzole Configuration Manager přejděte do pracovního prostoru **Správa** , rozbalte položku **Konfigurace lokality**, vyberte uzel **lokality** a klikněte na pásu karet na možnost **vytvořit server systému lokalit** .

2. Na stránce **Obecné** v Průvodci vytvořením serveru systému lokality zadejte server, který bude hostovat server lokality v pasivním režimu. Server, který zadáte, nemůže hostovat žádné role systému lokality před instalací serveru lokality v pasivním režimu.  

3. Na stránce **Výběr role systému** vyberte **v pasivním režimu možnost pouze server lokality**.  

    > [!NOTE]  
    > Průvodce provede na této stránce následující prvotní kontroly požadovaných součástí:
    >
    > - Vybraný server není sekundárním webovým serverem.
    > - Vybraný server již není serverem lokality v pasivním režimu.
    > - Knihovna obsahu webu je ve vzdáleném umístění.  
    >  
    > Pokud tyto prvotní kontroly požadavků selžou, nemůžete pokračovat po této stránce průvodce.  

4. Na stránce **Server lokality v pasivním režimu** zadejte následující informace, které se používají ke spuštění instalačního programu a instalaci role serveru lokality na zadaný server:

     - Zvolte jednu z následujících možností:  

         - **Kopírovat zdrojové instalační soubory přes síť ze serveru lokality v aktivním režimu**: Tato možnost vytvoří komprimovaný balíček a odešle ho na nový server lokality.  

         - **Použijte zdrojové soubory v následujícím umístění na serveru lokality v pasivním režimu**: například místní cesta, na kterou jste již zkopírovali zdrojové soubory. Ujistěte se, že tento obsah je stejná jako verze serveru lokality v aktivním režimu.  

         - (*Doporučeno*) **Použít zdrojové soubory v následujícím síťovém umístění**: zadejte cestu přímo k obsahu **disku CD-ROM. Poslední** složka ze serveru lokality v aktivním režimu. Například, `\\Server\SMS_ABC\CD.Latest` kde "*Server*" je název serveru lokality v aktivním režimu a "*ABC*" je kód lokality.  

     - Zadejte místní cestu, na které se má Configuration Manager nainstalovat na novém serveru lokality. Příklad: `C:\Program Files\Configuration Manager`  

5. Dokončete průvodce. Configuration Manager pak na určený server nainstaluje server lokality v pasivním režimu.

Podrobný stav instalace získáte tak, že v konzole přejdete do pracovního prostoru **monitorování** a vyberete uzel **stav serveru lokality** . Stav serveru lokality v pasivním režimu se zobrazí jako **instalace**. Podrobnější informace získáte tak, že vyberete server a kliknete na **Zobrazit stav**. Tato akce otevře okno stav instalace webového serveru. Po dokončení procesu se u obou serverů zobrazí stav **OK** .

Další informace o procesu instalace najdete v tématu [vývojový diagram – nastavení serveru lokality v pasivním režimu](passive-site-server-flowchart.md).

Po přidání serveru lokality v pasivním režimu si Projděte oba servery lokality na kartě **uzly** v uzlu **lokality** v konzole nástroje.

Všechny součásti Configuration Managerho serveru lokality jsou v pohotovostním režimu na serveru lokality v pasivním režimu. Služby systému Windows jsou pořád spuštěné.

## <a name="site-server-promotion"></a>Zvýšení úrovně webového serveru  

Podobně jako u zálohování a obnovování, plánování a cvičení procesu změny serverů lokality. V plánu povýšení zvažte následující body:  

- Procvičování plánovaného povýšení, kde jsou oba servery lokality online Procvičit také neplánované převzetí služeb při selhání vynuceným odpojením nebo vypnutím serveru lokality v aktivním režimu.  

- Určete provozní procesy během převzetí služeb při selhání a co komunikovat s ostatními správci Configuration Manager.  

- Před plánovaným zvýšením úrovně:  

  - Zkontroluje celkový stav lokalit a součástí lokality. Ujistěte se, že všechno je v pořádku jako normální pro vaše prostředí.  

  - Zkontroluje stav obsahu pro všechny balíčky, které aktivně replikují mezi lokalitami.  

  - Ověřte stav sekundární lokality a replikaci lokality.

  - Nespouštějte žádné nové úlohy distribuce obsahu ani Údržba na serverech podřízených nebo sekundárních lokalitách.

    > [!NOTE]
    > Pokud během převzetí služeb při selhání probíhá replikace souboru nebo databáze mezi lokalitami, nový server lokality nemusí získat replikovaný obsah. Pokud k tomu dojde, znovu distribuujte obsah softwaru poté, co je nový server lokality aktivní.<!--515436--> V případě replikace databáze možná budete muset po převzetí služeb při selhání znovu inicializovat sekundární lokalitu.<!-- SCCMDocs issue 808 -->

  - Snižte nebo odeberte jiné naplánované aktivity současně. Například neplánujete povýšit server lokality hned po aktualizaci lokality na novou verzi. Aktualizace webu zahrnuje další úlohy, které můžou být v konfliktu se zvýšením úrovně serveru lokality.

    > [!TIP]
    > Tady je příklad toho, jak můžou jiné aktivity kolidovat s povýšením serveru lokality:
    >
    > - Pondělí: Aktualizujte lokalitu na nejnovější verzi. Povolte automatický upgrade klienta s pilotním nasazením klienta.
    > - Úterý: Zvyšte úroveň serveru lokality v pasivním režimu na aktivní server lokality.
    >
    > Ve středu nebo ve čtvrtek může tato akce způsobit, že *Všichni* klienti budou upgradovat, ne pouze pilotní kolekce. Toto chování může způsobit významné využití sítě a neočekávané zatížení distribučních bodů.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Postup pro zvýšení úrovně serveru lokality v pasivním režimu na aktivní režim

Tato část popisuje, jak změnit server lokality v pasivním režimu na aktivní režim. Chcete-li získat přístup k webu a provést tuto změnu, je nutné mít přístup k instanci poskytovatele serveru SMS. Další informace najdete v tématu [použití více poskytovatelů serveru SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> Pokud jsou všechny instance poskytovatele služby SMS v režimu offline, nemůžete se připojit k webu, protože není k dispozici žádný zprostředkovatel. Při přidávání serveru lokality v pasivním režimu nainstaluje instalační program instanci poskytovatele služby SMS na tento server.<!-- SCCMDocs#1613 -->
>
> Konzola Configuration Manager vyžádá seznam dostupných poskytovatelů serveru SMS z rozhraní WMI na serveru lokality. Když nainstalujete více poskytovatelů serveru SMS v lokalitě, lokalita náhodně přiřadí každé nové žádosti o připojení použití nainstalovaného poskytovatele služby SMS. Nemůžete zadat umístění poskytovatele služby SMS pro použití s konkrétní relací připojení. Pokud se konzola nemůže připojit k lokalitě, protože aktuální server lokality je v režimu offline, Určete druhý server lokality v okně připojení k webu.  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte lokalitu a poté přepněte na kartu **uzly** . Vyberte server lokality v pasivním režimu a potom klikněte na pásu karet na možnost **povýšit na aktivní** . Kliknutím na **Ano** potvrďte a pokračujte.
  
2. Obnovte uzel konzoly. Sloupec **stav** pro server, který podporujete, se zobrazí na kartě **uzly** jako **propagace**.  

3. Po dokončení povýšení se ve sloupci **stav** zobrazí **OK** pro nový server lokality v aktivním režimu a pro nový server lokality v pasivním režimu. Sloupec **název serveru** pro lokalitu nyní zobrazuje název nového serveru lokality v aktivním režimu.

Podrobný stav získáte tak, že přejdete do pracovního prostoru **monitorování** a vyberete uzel **stav serveru lokality** . Sloupec **Mode (režim** ) určuje, který server je *aktivní* nebo *pasivní*. Při povýšení serveru z pasivního režimu na aktivní režim vyberte server lokality, který budete přizpůsobovat na aktivní, a pak na pásu karet zvolte **Zobrazit stav** . Tato akce otevře okno stav zvýšení úrovně serveru lokality, ve kterém se zobrazí další podrobnosti o procesu.

Když se server lokality v aktivním režimu přepne do pasivního režimu, stane se pasivní jenom role systému lokality. Všechny ostatní role systému lokality, které jsou nainstalované v tomto počítači, zůstávají aktivní a přístupné pro klienty.

Další informace o *plánovaném* procesu povýšení najdete v tématu [vývojový diagram – povýšení serveru lokality (plánované)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Neplánované převzetí služeb při selhání

Pokud je aktuální server lokality v aktivním režimu offline, server lokality pro povýšení se pokusí kontaktovat aktuální server lokality v aktivním režimu po dobu 30 minut. Pokud se server offline vrátí k této době, bude úspěšně upozorněn a změna pokračuje. V opačném případě server lokality pro zvýšení úrovně nuceně aktualizuje konfiguraci lokality, aby byla aktivní. Pokud se offline server vrátí po uplynutí této doby, nejprve zkontroluje aktuální stav v databázi lokality. Pak pokračuje tím, že se na server lokality v pasivním režimu převede.

Během této 30 minutové čekací doby nemá lokalita žádný server lokality v aktivním režimu. Klienti stále komunikují s rolemi orientovanými na klienta, jako jsou body správy, body aktualizace softwaru a distribuční body. Uživatelé můžou nainstalovat software, který je už nasazený. V tomto časovém období není možné spravovat žádnou správu lokality. Další informace najdete v tématu [vliv na selhání lokality](../../manage/site-failure-impacts.md).  

Pokud je offline server poškozený tak, že se nemůže vrátit, odstraňte tento server lokality z konzoly nástroje. Pak vytvořte nový server lokality v pasivním režimu pro obnovení služby s vysokou dostupností.

Další informace o procesu *neplánovaného* převzetí služeb při selhání najdete v tématu [vývojový diagram – povýšení serveru lokality (Neplánovaná)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Další úkoly po zvýšení úrovně webového serveru  

Po přepnutí serverů lokality není nutné provádět většinu dalších úloh, které jsou nezbytné při [obnovování lokality](../../manage/recover-sites.md#post-recovery-tasks). Například nemusíte resetovat hesla ani znovu připojit předplatné Microsoft Intune.

V případě potřeby můžete v prostředí vyžadovat následující kroky:  

- Pokud importujete certifikáty PKI pro distribuční body, znovu naimportujte certifikát pro ovlivněné servery. Další informace najdete v tématu [opětovné vygenerování certifikátů pro distribuční body](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Pokud integrujete Configuration Manager s Microsoft Store pro firmy, překonfigurujte toto připojení. Další informace najdete v tématu [Správa aplikací z Microsoft Store pro firmy](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

## <a name="daily-monitoring"></a>Denní monitorování

Pokud máte server lokality v pasivním režimu, sledujte ho denně. Ujistěte se, že stav zůstává v pořádku a je připravený k použití. V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **stav serveru lokality** . Zobrazit oba servery lokality a jejich aktuální stav. Můžete také zobrazit stav v pracovním prostoru **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **weby** . Vyberte lokalitu a pak přepněte na kartu **uzly** .

> [!NOTE]
> Když aktualizujete lokalitu na novou verzi Configuration Manager, aktualizuje se taky server lokality v pasivním režimu. <!-- SCCMDocs-pr#4293 -->