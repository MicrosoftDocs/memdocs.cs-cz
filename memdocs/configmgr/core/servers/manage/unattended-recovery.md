---
title: Bezobslužné obnovení
titleSuffix: Configuration Manager
description: Pomocí skriptu obnovte své weby v Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720797"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Bezobslužné obnovení lokality pro Configuration Manager   

*Platí pro: Configuration Manager (Current Branch)*

 Chcete-li provést [bezobslužné obnovení](recover-sites.md#site-recovery-procedures) Configuration Manager lokality centrální správy nebo primární lokality, můžete vytvořit skript bezobslužné instalace a pak použít instalační program s možností **/Script** . Skript poskytuje stejný typ informací, k jejichž zadání vyzve Průvodce instalací nástroje, s tím rozdílem, že neexistuje žádné výchozí nastavení. Všechny hodnoty musí být zadány pro klíče instalace, jež platí pro typ obnovení, který používáte.

 Chcete-li použít možnost příkazového řádku instalace/Script, je nutné vytvořit inicializační soubor. Poté zadejte název souboru za možností/Script. Název souboru je neimportovaná, pokud má příponu názvu souboru **. ini** . Když odkazujete inicializační soubor instalace z příkazového řádku, musíte zadat úplnou cestu k souboru. Například pokud se inicializační soubor instalace nazývá *Setup. ini*a je uložen ve *složce C:\setup*, bude příkazový řádek:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Ke spuštění instalace musíte mít oprávnění správce. Když spouštíte instalaci pomocí bezobslužného skriptu, spusťte příkazový řádek v kontextu správce pomocí příkazu **Spustit jako správce**.

 Skript obsahuje názvy částí, názvy klíčů a hodnoty. Povinné názvy klíčů částí se liší v závislosti na typu obnovení, pro který vytváříte skript. Pořadí klíčů v částech a pořadí částí v souboru není důležité. U klíčů se nerozlišují velká a malá písmena. Když poskytujete hodnoty pro klíče, musí za názvem klíče následovat znak rovná se (=) a hodnota klíče.

 Následující části vám pomohou vytvořit váš skript pro bezobslužné obnovení lokality. V tabulkách jsou uvedeny dostupné klíče skriptů instalace, jejich příslušné hodnoty, zda jsou povinné, pro jaký typ instalace se používají a jejich popis.

## <a name="recover-a-central-administration-site-unattended"></a>Bezobslužné obnovení lokality centrální správy
 Následující informace slouží ke konfiguraci souboru skriptu bezobslužné instalace pro obnovení lokality centrální správy.

 **Identifikace**

-   **Název klíče:** Action

    -   **Požadováno:** Ano
    -   **Hodnoty:** RecoverCCAR
    -   **Podrobnosti:** Obnoví lokalitu centrální správy.


-   **Název klíče:** CDLatest

    -   **Požadováno:** Ano – jenom při použití média z CD Poslední složka
    -   **Hodnoty:** 1 jakákoli jiná hodnota než 1 se považuje za nepoužitou CD. Nejnovější.
    -   **Podrobnosti:** Když spustíte instalační program z média na disku CD, váš skript musí zahrnovat tento klíč a hodnotu. Poslední složka pro účely instalace primární lokality nebo lokality centrální správy nebo obnovování primární lokality nebo lokality centrální správy. Tato hodnota informuje o nastavení disku CD média. Je používán nejnovější.

**MožnostiObnovení**   
-   **Název klíče:** ServerRecoveryOptions   

    -   **Požadováno:** Ano
    -   **Hodnoty:** 1, 2 nebo 4  
         1 = Obnovit server lokality a server SQL.   
         2 = Obnovit pouze server lokality.  
         4 = Obnovit pouze server SQL.
    -   **Podrobnosti:** Určuje, jestli instalační program obnoví server lokality, SQL Server, nebo obojí. Přidružené klíče jsou požadovány při nastavení následující hodnoty pro MožnostiObnoveníServeru:  
        -   **Hodnota = 1** : Máte možnost zadat hodnotu klíče **SiteServerBackupLocation** pro obnovení lokality pomocí zálohy lokality. Pokud hodnotu nezadáte, bude lokalita přeinstalována bez obnovení ze zálohovacího skladu.

             Klíč **BackupLocation** se vyžaduje při nastavení hodnoty **10** pro klíč **DatabaseRecoveryOptions** , který má obnovit databázi lokality ze zálohy.

        -   **Hodnota = 2** : Máte možnost zadat hodnotu klíče **SiteServerBackupLocation** pro obnovení lokality pomocí zálohy lokality. Pokud hodnotu nezadáte, bude lokalita přeinstalována bez obnovení ze zálohovacího skladu.

        -   **Hodnota = 4** : Klíč **BackupLocation** se vyžaduje při nastavení hodnoty **10** pro klíč **DatabaseRecoveryOptions** , který má obnovit databázi lokality ze zálohy.

-   **Název klíče:** DatabaseRecoveryOptions

    -   **Požadováno:** Možná
    -   **Hodnota**   
         - **10** = obnovit databázi lokality ze zálohy.  
         - **20** = použít databázi lokality, která byla ručně obnovena pomocí jiné metody.   
         - **40** = vytvořte novou databázi pro tento web. Tuto možnost použijte, pokud není k dispozici žádná záloha databáze lokality. Globální data a data lokality jsou obnovena prostřednictvím replikace z ostatních lokalit.  
         - **80** = přeskočit obnovení databáze.
    -   **Podrobnosti:** Určuje způsob, jakým Instalační program obnovuje databázi lokality v SQL Server. Tento klíč se požaduje při nastavení **ServerRecoveryOptions** na hodnotu **1** nebo **4**.


-   **Název klíče:** ReferenceSite  

    -   **Požadováno:** Možná
    -   **Hodnoty:** &lt;ReferenceSiteFQDN\>
    -   **Podrobnosti:** Určuje referenční primární lokalitu. Pokud je záloha databáze starší než doba uchování dat sledování změn nebo obnovujete lokalitu bez zálohy, lokalita centrální správy použije referenční lokalitu k obnovení globálních dat.

         Pokud neurčíte referenční lokalitu a záloha je starší než doba uchování dat sledování změn, všechny primární lokality budou znovu inicializovány obnovenými daty z lokality centrální správy.

         Když neurčíte referenční lokalitu a záloha spadá do doby uchování dat sledování změn, replikují se z primárních lokalit jenom změny od zálohy. Když dojde ke konfliktu změn z různých primárních lokalit, lokalita centrální správy použije první, kterou přijme.

         Tento klíč se požaduje při nastavení **DatabaseRecoveryOptions** na hodnotu **40**.

-   **Název klíče:** SiteServerBackupLocation

    -   **Požadováno:** Ne
    -   **Hodnoty:** &lt;PathToSiteServerBackupSet\>
    -   **Podrobnosti:** Udává cestu k zálohovacímu skladu serveru lokality. Tento klíč je volitelný při nastavení **ServerRecoveryOptions** na hodnotu **1** nebo **2**. K obnovení lokality pomocí zálohy lokality zadejte hodnotu klíče **SiteServerBackupLocation** . Pokud hodnotu nezadáte, bude lokalita přeinstalována bez obnovení ze zálohovacího skladu.


-   **Název klíče:** BackupLocation

    -   **Požadováno:** Možná
    -   **Hodnoty:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Podrobnosti:** Udává cestu k zálohovacímu skladu databáze lokality. Klíč **BackupLocation** se požaduje při nastavení hodnoty **1** nebo **4** pro klíč **ServerRecoveryOptions** a hodnoty **10** pro klíč **DatabaseRecoveryOptions** .


**Možnosti**

- **Název klíče:** ProductID
  -   **Požadováno:** Ano
  -   **Hodnota**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Podrobnosti:** Kód Product Key instalace Configuration Manager, včetně pomlček. Zadejte **Eval** může nainstalovat zkušební verzi Configuration Manager.  


- **Název klíče:** SiteCode

  -   **Požadováno:** Ano
  -   **Hodnoty:** &lt;kód lokality\>
  -   **Podrobnosti:** Tři alfanumerické znaky, které jedinečně identifikují lokalitu ve vaší hierarchii. Zadejte kód lokality, který byl použit lokalitou před chybou.


- **Název klíče:** SiteName

  -   **Požadováno:** Ano
  -   **Hodnoty:** název_lokality
  -   **Podrobnosti:** Popis této lokality.


- **Název klíče:** SMSInstallDir

  - **Požadováno:** Ano
  - **Hodnoty:** &lt; *ConfigMgrInstallationPath*>
  - **Podrobnosti:** Určuje instalační složku pro soubory Configuration Manager programu.
    > [!NOTE]   
    >  Můžete zadat původní cestu nebo novou cestu, kterou chcete použít pro instalaci Configuration Manager.

- **Název klíče:** SDKServer

  -   **Požadováno:** Ano
  -   **Hodnoty:** &lt;*plně_kvalifikovaný_název_domény_poskytovatele_serveru_SMS*>
  -   **Podrobnosti:** Určuje plně kvalifikovaný název domény pro server, který je hostitelem poskytovatele služby SMS. Zadejte server, který hostuje poskytovatele služby SMS, před selháním.

       Po počáteční instalaci lze nastavit další poskytovatele služeb SMS pro lokalitu.

- **Název klíče:** PrerequisiteComp

  -   **Požadováno:** Ano
  -   **Hodnoty:** 0 nebo 1  
       0 = stáhnout   
       1 = již staženo
  -   **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu 0, instalační program soubory stáhne.  


- **Název klíče:** PrerequisitePath

  -   **Požadováno:** Ano
  -   **Hodnoty:** &lt;*cesta_k_požadovaným_souborům_instalace*>
  -   **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.

- **Název klíče:** AdminConsole

  -   **Požadováno:** Možná
  -   **Hodnoty:** 0 nebo 1 0 = neinstalovat   
       1 = instalovat
  -   **Podrobnosti:** Určuje, jestli se má nainstalovat konzola Configuration Manager. Tento klíč se požaduje vždy, když jako **ServerRecoveryOptions** není nastavená hodnota **4**.


- **Název klíče:** JoinCEIP   
  > [!Note]  
  > Počínaje verzí Configuration Manager 1802 je funkce CEIP z produktu odebrána.

  -   **Požadováno:** Ano
  -   **Hodnoty:** 0 nebo 1  
       0 = zapojit se  
       1 = nezapojovat se
  -   **Podrobnosti:** Udává, jestli se chcete zapojit do programu Zlepšování softwaru a služeb na základě zkušeností uživatelů (CEIP).

**MožnostiKonfSQL**

-   **Název klíče:** SQLServerName

    -   **Požadováno:** Ano
    -   **Hodnoty:** * &lt;SQLServer\>*
    -   **Podrobnosti:** Název serveru nebo název skupiny prostředků clusteru, na kterém běží SQL Server, který hostuje databázi lokality. Zadejte stejný server, který hostuje databázi lokality před selháním.


-   **Název klíče:** DatabaseName

    -   **Požadováno:** Ano
    -   **Hodnoty:** * &lt;SiteDatabaseName\> * \\nebo * &lt;InstanceName\>**SiteDatabaseName&lt;\> *
    -   **Podrobnosti:** Název databáze SQL Serveru k vytvoření nebo instalaci databáze lokality centrální správy. Zadejte stejný název databáze, který byl použit před selháním.

        > [!IMPORTANT]  
        >  Pokud nepoužíváte výchozí instanci, je nutné zadat název instance a název databáze lokality.

-   **Název klíče:** SQLSSBPort

    -   **Požadováno:** Ne
    -   **Hodnoty:** &lt;*číslo_portu_SSB*>
    -   **Podrobnosti:** Udává port služby SQL Server Service Broker (SSB) používaný SQL Serverem. SSB obvykle využívá port TCP 4022, ale podporovány jsou i další porty. Zadejte stejný port SSB, který byl použit před selháním.

## <a name="recover-a-primary-site-unattended"></a>Bezobslužné obnovení primární lokality
 Následující informace slouží ke konfiguraci souboru skriptu bezobslužné instalace pro obnovení lokality centrální správy.

 **Identifikace**

-   **Název klíče:** Action

    -   **Požadováno:** Ano
    -   **Hodnoty:** RecoverPrimarySite
    -   **Podrobnosti:** Obnoví primární lokalitu.


-   **Název klíče:** CDLatest

    -   **Požadováno:** Ano – jenom při použití média z CD Poslední složka
    -   **Hodnoty:** 1 jakákoli jiná hodnota než 1 se považuje za nepoužitou CD. Nejnovější.
    -   **Podrobnosti:** Když spustíte instalační program z média na disku CD, váš skript musí zahrnovat tento klíč a hodnotu. Poslední složka pro účely instalace primární lokality nebo lokality centrální správy nebo obnovování primární lokality nebo lokality centrální správy. Tato hodnota informuje o nastavení disku CD média. Je používán nejnovější.

**MožnostiObnovení**

-   **Název klíče:** ServerRecoveryOptions

    -   **Požadováno:** Ano
    -   **Hodnoty:** 1, 2 nebo 4    
         1 = Obnovit server lokality a server SQL.   
         2 = Obnovit pouze server lokality.  
         4 = Obnovit pouze server SQL.
    -   **Podrobnosti:** Určuje, jestli instalační program obnoví server lokality, SQL Server, nebo obojí. Přidružené klíče jsou požadovány při nastavení následující hodnoty pro MožnostiObnoveníServeru:

        -   **Hodnota = 1** : Máte možnost zadat hodnotu klíče **SiteServerBackupLocation** pro obnovení lokality pomocí zálohy lokality. Pokud hodnotu nezadáte, bude lokalita přeinstalována bez obnovení ze zálohovacího skladu.

             Klíč **BackupLocation** se vyžaduje při nastavení hodnoty **10** pro klíč **DatabaseRecoveryOptions** , který má obnovit databázi lokality ze zálohy.

        -   **Hodnota = 2** : Máte možnost zadat hodnotu klíče **SiteServerBackupLocation** pro obnovení lokality pomocí zálohy lokality. Pokud hodnotu nezadáte, bude lokalita přeinstalována bez obnovení ze zálohovacího skladu.

        -   **Hodnota = 4** : Klíč **BackupLocation** se vyžaduje při nastavení hodnoty **10** pro klíč **DatabaseRecoveryOptions** , který má obnovit databázi lokality ze zálohy.

-   **Název klíče:** DatabaseRecoveryOptions

    -   **Požadováno:** Možná
    -   **Hodnota**   
         - **10** = obnovit databázi lokality ze zálohy.  
         - **20** = použít databázi lokality, která byla ručně obnovena pomocí jiné metody.     
         - **40** = vytvořte novou databázi pro tento web. Tuto možnost použijte, pokud není k dispozici žádná záloha databáze lokality. Globální data a data lokality jsou obnovena prostřednictvím replikace z ostatních lokalit.  
         - **80** = přeskočit obnovení databáze.
    -   **Podrobnosti:** Určuje způsob, jakým Instalační program obnovuje databázi lokality v SQL Server. Tento klíč se požaduje při nastavení **ServerRecoveryOptions** na hodnotu **1** nebo **4**.


-   **Název klíče:** SiteServerBackupLocation

    -   **Požadováno:** Ne
    -   **Hodnoty:** &lt;PathToSiteServerBackupSet\>
    -   **Podrobnosti:** Udává cestu k zálohovacímu skladu serveru lokality. Tento klíč je volitelný při nastavení **ServerRecoveryOptions** na hodnotu **1** nebo **2**. K obnovení lokality pomocí zálohy lokality zadejte hodnotu klíče **SiteServerBackupLocation** . Pokud hodnotu nezadáte, bude lokalita přeinstalována bez obnovení ze zálohovacího skladu.     


-   **Název klíče:** BackupLocation

    -   **Požadováno:** Možná
    -   **Hodnoty:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Podrobnosti:** Udává cestu k zálohovacímu skladu databáze lokality. Klíč **BackupLocation** se požaduje při nastavení hodnoty **1** nebo **4** pro klíč **ServerRecoveryOptions** a hodnoty **10** pro klíč **DatabaseRecoveryOptions** .

**Možnosti**

-   **Název klíče:** ProductID

    -   **Požadováno:** Ano
    -   **Hodnota**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Podrobnosti:** Kód Product Key instalace Configuration Manager, včetně pomlček. Zadejte **Eval** může nainstalovat zkušební verzi Configuration Manager.  


-   **Název klíče:** SiteCode

    -   **Požadováno:** Ano
    -   **Hodnoty:** &lt;kód lokality\>
    -   **Podrobnosti:** Tři alfanumerické znaky, které jedinečně identifikují lokalitu ve vaší hierarchii. Zadejte kód lokality, který byl použit lokalitou před chybou.


-   **Název klíče:** SiteName

    -   **Požadováno:** Ano
    -   **Hodnoty:** název_lokality
    -   **Podrobnosti:** Popis této lokality.


-   **Název klíče:** SMSInstallDir

    -   **Požadováno:** Ano
    -   **Hodnoty:** &lt; *ConfigMgrInstallationPath*>
    -   **Podrobnosti:** Určuje instalační složku pro soubory Configuration Manager programu.

        > [!NOTE]   
        >  Můžete zadat původní cestu nebo novou cestu, kterou chcete použít pro instalaci Configuration Manager.

-   **Název klíče:** SDKServer

    -   **Požadováno:** Ano
    -   **Hodnoty:** &lt;*plně_kvalifikovaný_název_domény_poskytovatele_serveru_SMS*>
    -   **Podrobnosti:** Určuje plně kvalifikovaný název domény pro server, který je hostitelem poskytovatele služby SMS. Zadejte server, který hostuje poskytovatele služby SMS, před selháním.

         Po počáteční instalaci lze nastavit další poskytovatele služeb SMS pro lokalitu.

-   **Název klíče:** PrerequisiteComp

    -   **Požadováno:** Ano
    -   **Hodnoty:** 0 nebo 1    
         0 = stáhnout   
         1 = již staženo   
    -   **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu 0, instalační program soubory stáhne.


-   **Název klíče:** PrerequisitePath

    -   **Požadováno:** Ano
    -   **Hodnoty:** &lt;*cesta_k_požadovaným_souborům_instalace*>
    -   **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.


-   **Název klíče:** AdminConsole

    -   **Požadováno:** Možná
    -   **Hodnoty:** 0 nebo 1  
         0 = neinstalovat   
         1 = instalovat  
    -   **Podrobnosti:** Určuje, jestli se má nainstalovat konzola Configuration Manager. Tento klíč se požaduje vždy, když jako **ServerRecoveryOptions** není nastavená hodnota **4**.

-   **Název klíče:** JoinCEIP  
    > [!Note]  
    > Počínaje verzí Configuration Manager 1802 je funkce CEIP z produktu odebrána.

    -   **Požadováno:** Ano
    -   **Hodnoty:** 0 nebo 1    
         0 = zapojit se  
         1 = nezapojovat se
    -   **Podrobnosti:** Udává, jestli se chcete zapojit do programu Zlepšování softwaru a služeb na základě zkušeností uživatelů (CEIP).


**MožnostiKonfSQL**

-   **Název klíče:** SQLServerName

    -   **Požadováno:** Ano
    -   **Hodnoty:** * &lt;SQLServer\>*
    -   **Podrobnosti:** Název serveru nebo název skupiny prostředků clusteru, na kterém běží SQL Server, který hostuje databázi lokality. Zadejte stejný server, který hostuje databázi lokality před selháním.


-   **Název klíče:** DatabaseName

    -   **Požadováno:** Ano
    -   **Hodnoty:** * &lt;SiteDatabaseName\> * \\nebo * &lt;InstanceName\>**SiteDatabaseName&lt;\> *
    -   **Podrobnosti:** Název databáze SQL Serveru k vytvoření nebo instalaci databáze lokality centrální správy. Zadejte stejný název databáze, který byl použit před selháním.

        > [!IMPORTANT]    
        >  Pokud nepoužíváte výchozí instanci, je nutné zadat název instance a název databáze lokality.

-   **Název klíče:** SQLSSBPort

    -   **Požadováno:** Ne
    -   **Hodnoty:** &lt;*číslo_portu_SSB*>
    -   **Podrobnosti:** Udává port služby SQL Server Service Broker (SSB) používaný SQL Serverem. SSB obvykle využívá port TCP 4022, ale podporovány jsou i další porty. Zadejte stejný port SSB, který byl použit před selháním.

**Hierarchie ExpansionOption**

-   **Název klíče:** CCARSiteServer

    -   **Požadováno:** Možná
    -   **Hodnoty:** &lt; *SiteCodeForCentralAdministrationSite*>
    -   **Podrobnosti:** Určuje lokalitu centrální správy, ke které se primární lokalita připojí, když se připojí k hierarchii Configuration Manager. Toto nastavení je povinné, pokud byla před chybou primární lokalita připojena k lokalitě centrální správy. Zadejte kód lokality, který se používal pro lokalitu centrální správy před chybou.

-   **Název klíče:** CASRetryInterval

    -   **Požadováno:** Ne
    -   **Hodnoty:** &lt; *interval*>
    -   **Podrobnosti:** Udává interval opakování pokusu o připojení k lokalitě centrální správy (CAS) v případě, že selhalo spojení (v minutách). Pokud se například připojení k lokalitě centrální správy nezdaří, primární lokalita počká na počet minut, který zadáte pro CASRetryInterval, a pak se znovu pokusí o připojení.


-   **Název klíče:** WaitForCASTimeout

    -   **Požadováno:** Ne
    -   **Hodnoty:** &lt;*časový_limit*>
    -   **Podrobnosti:** Určuje maximální hodnotu časového limitu (v minutách), který má primární lokalita na připojení k lokalitě centrální správy. Pokud se například primární lokalitě nepodaří připojit k lokalitě centrální správy, opakuje primární správa připojení k lokalitě centrální správy, na základě hodnoty parametru CASRetryInterval, až dokud nebude dosaženo časového limitu určeného v parametru WaitForCASTimeout. Zadávat lze hodnoty od 0 do 100.
