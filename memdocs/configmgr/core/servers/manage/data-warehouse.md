---
title: Datový sklad
titleSuffix: Configuration Manager
description: Bod služby a databáze datového skladu pro Configuration Manager
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d5ff011c0d25e601ff6605edb49383e58f949203
ms.sourcegitcommit: 1edcfb3ce4350ba1a6f36a6150e86301d35c631b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/15/2020
ms.locfileid: "86390887"
---
# <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Bod služby datového skladu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1277922-->
Pomocí bodu služby datového skladu můžete ukládat a vykazovat dlouhodobá historická data pro nasazení Configuration Manager.

> [!NOTE]
> Ve výchozím nastavení ve verzi 1910 Configuration Manager tuto funkci povolí. Verze 1906 nebo starší Configuration Manager ve výchozím nastavení tuto volitelnou funkci nepovoluje. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](install-in-console-updates.md#bkmk_options).<!--505213-->

Datový sklad podporuje až 2 TB dat s časovými razítky pro sledování změn. Datový sklad ukládá data automaticky synchronizací dat z databáze lokality Configuration Manager do databáze datového skladu. Tyto informace jsou pak přístupné z bodu služby generování sestav. Data synchronizovaná s databází datového skladu se uchovávají po dobu tří let. Předdefinovaná úloha pravidelně odstraňuje data, která jsou starší než tři roky.

Synchronizovaná data zahrnují z globálních dat a skupin dat webu následující:

- Stav infrastruktury
- Zabezpečení
- Dodržování předpisů
- Malware
- Nasazení softwaru
- Podrobnosti inventáře (ale historie inventáře není synchronizovaná)

Při instalaci role systému lokality nainstaluje a nakonfiguruje databázi datového skladu. Také nainstaluje několik sestav, abyste mohli snadno vyhledat a ohlásit tato data.

## <a name="prerequisites"></a>Požadavky

- Role systému lokality datového skladu je podporována pouze v lokalitě nejvyšší úrovně ve vaší hierarchii. Například lokalita centrální správy (CAS) nebo samostatná primární lokalita.

- Počítač, na který instalujete roli systému lokality, vyžaduje .NET Framework 4.5.2 nebo novější.

- Udělte **účtu bodu služby Reporting Services** **db_datareader** oprávnění k databázi datového skladu.

- K synchronizaci dat s databází datového skladu Configuration Manager používá počítačový účet role systému lokality. Tento účet vyžaduje následující oprávnění:

  - **Správce** počítače, který je hostitelem databáze datového skladu.

  - **DB_Creator** oprávnění k databázi datového skladu.

  - Buď **DB_owner** , nebo **DB_reader** s oprávněním **Execute** pro databázi lokality nejvyšší úrovně.

- Databáze datového skladu vyžaduje použití SQL Server 2012 nebo vyšší. Edice může být standard, Enterprise nebo Datacenter. Verze SQL Server pro datový sklad nemusí být stejná jako server databáze lokality.<!--SCCMDocs issue 662-->

- Databáze datového skladu podporuje následující konfigurace SQL Server:

  - Výchozí nebo pojmenovaná instance

  - Skupina dostupnosti Always On SQL Server

  - SQL Server clusteru převzetí služeb při selhání

- Pokud používáte [distribuovaná zobrazení](../../plan-design/hierarchy/database-replication.md#bkmk_distviews), nainstalujte bod služby datový sklad na stejný server, který je hostitelem databáze CAS.

Další informace o SQL Server licencování najdete v tématu [Nejčastější dotazy k produktu a licencování](../../understand/product-and-licensing-faq.md).<!-- sms500967 -->

Velikost databáze datového skladu je stejná jako databáze lokality. I když je datový sklad v prvním místě, bude růst v průběhu času. <!--SCCMDocs issue 756-->

## <a name="install"></a>Instalace

Každá hierarchie podporuje jednu instanci této role v libovolném systému lokality lokality nejvyšší úrovně. SQL Server, která je hostitelem databáze pro daný datový sklad, může být místní pro roli systému lokality nebo vzdálené. Datový sklad funguje s bodem služby Reporting Services nainstalovaným ve stejné lokalitě. Nemusíte instalovat dvě role systému lokality na stejný server.

Chcete-li nainstalovat roli, použijte **Průvodce přidáním rolí systému lokality** nebo **Průvodce vytvořením serveru systému lokality**. Další informace najdete v tématu [Instalace rolí systému lokality](../deploy/configure/install-site-system-roles.md). Na stránce **Výběr role systému** v průvodci vyberte roli **bodu služby datového skladu** .

Při instalaci role Configuration Manager vytvoří databázi datového skladu pro vás na instanci SQL Server, kterou zadáte. Pokud zadáte název existující databáze, Configuration Manager nevytvoří novou databázi. Místo toho používá ten, který zadáte. Tento proces je stejný jako při [přesunu databáze datového skladu do nové SQL Server](#move-the-database).

### <a name="configure-properties"></a>Konfigurovat vlastnosti

#### <a name="general-page"></a>Stránka Obecné

- **SQL Server plně kvalifikovaný název domény**: zadejte plně kvalifikovaný název domény (FQDN) serveru, který je hostitelem databáze bodu služby datového skladu.

- **Název instance SQL Server, pokud je k dispozici**: Pokud nepoužíváte výchozí instanci SQL Server, zadejte pojmenovanou instanci.

- **Název databáze**: zadejte název databáze datového skladu. Configuration Manager vytvoří databázi datového skladu s tímto názvem. Pokud zadáte název databáze, který již v instanci systému SQL Server existuje, Configuration Manager používá tuto databázi.

- **Port SQL Server používaný pro připojení**: zadejte číslo portu TCP/IP, které používá SQL Server, který hostuje databázi datového skladu. Služba synchronizace datového skladu používá tento port pro připojení k databázi datového skladu. Ve výchozím nastavení používá SQL Server port **1433** pro komunikaci.

- **Účet bodu služby datového skladu**: nastavte **uživatelské jméno** , které SQL Server Reporting Services používá při připojení k databázi datového skladu.

#### <a name="synchronization-settings-page"></a>Stránka nastavení synchronizace

- **Vlastní nastavení synchronizace dat**: zvolte možnost **výběru tabulek**. V okně tabulky databáze vyberte názvy tabulek pro synchronizaci s databází datového skladu. Použijte filtr k hledání podle názvu nebo vyberte rozevírací seznam a zvolte konkrétní skupiny. Po dokončení ukládání vyberte **OK** .

    > [!NOTE]
    > Nemůžete odebrat tabulky, které tato role vybere ve výchozím nastavení.

- **Čas spuštění**: zadejte čas, kdy se má spustit synchronizace datového skladu.

- **Způsob opakování**

  - **Denně**: Určete, že se synchronizace spouští každý den.

  - **Týdně**: Zadejte každý týden jeden den a týdenní opakování synchronizace.

## <a name="reporting"></a>Přehledy

Po instalaci bodu služby datového skladu bude v bodu služby Reporting Services pro danou lokalitu k dispozici několik sestav. Pokud před instalací bodu služby Reporting Services nainstalujete bod služby datového skladu, budou tyto sestavy automaticky přidány při pozdější instalaci bodu služby Reporting Services.

> [!NOTE]
> Bod datového skladu podporuje alternativní přihlašovací údaje.<!--507334--> Zadejte přihlašovací údaje, které SQL Server Reporting Services používá pro připojení k databázi datového skladu. Sestavy datového skladu se otevřou, dokud nepřidáte přihlašovací údaje.
>
> Chcete-li zadat účet, nastavte **uživatelské jméno** pro účet bodu služby datového skladu ve vlastnostech role. Další informace najdete v tématu [Konfigurace vlastností](#configure-properties).

Role systému lokality datového skladu zahrnuje následující sestavy v kategorii **datový sklad** :

- **Nasazení aplikace – historická**: zobrazení podrobností nasazení aplikace pro konkrétní aplikaci a počítač.

- **Endpoint Protection a Software Update Compliance – historická**: zobrazení počítačů, ve kterých chybí aktualizace softwaru.

- **Obecný inventář hardwaru – historická**: zobrazení veškerého inventáře hardwaru pro určitý počítač.

- **Obecný inventář softwaru – historická**: zobrazení veškerého inventáře softwaru pro určitý počítač.

- **Přehled stavu infrastruktury – historická**: zobrazuje přehled stavu infrastruktury Configuration Manager.

- **Seznam zjištěného malwaru – historická**: zobrazení malwaru zjištěného v organizaci.

- **Shrnutí distribuce softwaru – historická**: Shrnutí distribuce softwaru pro konkrétní reklamu a počítač.

## <a name="site-expansion"></a>Rozšíření lokality

Než budete moci nainstalovat certifikační autority pro rozšíření existující samostatné primární lokality, nejprve odinstalujte roli bodu služby datového skladu. Po instalaci certifikační autority pak můžete nainstalovat roli systému lokality na CAS.

Na rozdíl od přesunutí databáze datového skladu Tato změna vede ke ztrátě historických dat, která jste předtím synchronizovali v primární lokalitě. Není podporována pro zálohování databáze z primární lokality a její obnovení v certifikačních autoritách.

## <a name="move-the-database"></a>Přesunutí databáze

K přesunutí databáze datového skladu do nové SQL Server použijte následující postup:

1. K zálohování databáze datového skladu použijte SQL Server Management Studio. Pak tuto databázi obnovte do SQL Server v novém počítači, který je hostitelem datového skladu.

    > [!NOTE]
    > Po obnovení databáze na nový server se ujistěte, že jsou přístupová oprávnění k databázi stejná na nové databázi datového skladu, stejně jako v původní databázi datového skladu.

2. Pomocí konzoly Configuration Manager odeberte roli bodu služby datového skladu z aktuálního serveru.

3. Přeinstalujte bod služby datového skladu. Zadejte název nové SQL Server a instance, která hostuje obnovenou databázi datového skladu.

4. Po instalaci role systému lokality se přesun dokončí.

## <a name="troubleshoot"></a>Řešení potíží

### <a name="log-files"></a>Soubory protokolu

Pomocí následujících protokolů můžete prozkoumat problémy s instalací bodu služby datového skladu nebo synchronizace dat:

- **DWSSMSI. log** a **DWSSSetup. log**: pomocí těchto protokolů můžete prozkoumat chyby při instalaci bodu služby datového skladu.

- **Microsoft.ConfigMgrDataWarehouse. log**: pomocí tohoto protokolu můžete prozkoumat synchronizaci dat mezi databází lokality a databází datového skladu.

### <a name="set-up-failure"></a>Nastavení selhání

Pokud je role bodu služby datového skladu první, kterou nainstalujete na vzdálený server, instalace datového skladu se nezdařila.  

Pokud chcete tento problém obejít, ujistěte se, že počítač, na který jste nainstalovali bod služby datového skladu, již hostuje alespoň jednu další roli.

### <a name="synchronization-failed-to-populate-schema-objects"></a>Synchronizaci se nepodařilo naplnit objekty schématu.

Synchronizace se nezdařila s následující zprávou v **Microsoft.ConfigMgrDataWarehouse. log**:`failed to populate schema objects`

Pokud chcete tento problém obejít, ujistěte se, že počítačový účet role systému lokality je **db_owner** v databázi datového skladu.

### <a name="reports-fail-to-open"></a>Otevření sestav se nezdařilo.

V případě, že se databáze datového skladu a bod služby Reporting Services nacházejí v různých systémech lokality, nelze otevřít sestavy datového skladu.

Chcete-li tento problém obejít, udělte **účtu bodu služby Reporting Services** **db_datareader** oprávnění k databázi datového skladu.

### <a name="error-opening-reports"></a>Chyba při otevírání sestav

Když otevřete sestavu datového skladu, vrátí se následující chyba:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

Pokud chcete tento problém obejít, nakonfigurujte certifikáty pomocí následujících kroků:

1. Na serveru, který je hostitelem databáze datového skladu:

    1. Vytvořte certifikát podepsaný svým držitelem. Otevřete IIS, vyberte **certifikáty serveru**a pak vyberte akci **vytvořit certifikát podepsaný držitelem** . Zadejte popisný název názvu certifikátu jako **SQL Serverho identifikačního certifikátu datového skladu**. Vyberte úložiště certifikátů jako **osobní**.

      > [!TIP]
      > Pokud tento server ještě nemá službu IIS, nainstalujte ho jako první.

    1. Spravujte certifikát. Otevřete konzolu Microsoft Management Console (MMC) a přidejte modul snap-in **certifikáty** . Vyberte **počítačový účet** místního počítače. Rozbalte položku **osobní** složka a vyberte položku **certifikáty**.

        1. Udělte účtu služby SQL Server oprávnění ke čtení certifikátu. Vyberte **datový sklad SQL Server certifikát pro identifikaci certifikátu** , pak přejděte do nabídky **Akce** , vyberte **všechny úlohy**a vyberte **Spravovat privátní klíče**. Přidejte účet služby SQL Server a povolte oprávnění **ke čtení** .<!-- SCCMDocs#1805 -->

        1. Exportujte **datový sklad SQL Server identifikační certifikát** jako **binární soubor kódování der X. 509 (. CER)** soubor.

    1. Překonfigurujte SQL. Otevřete nástroj **SQL Server Configuration Manager**.

        1. V části **SQL Server konfigurace sítě**klikněte pravým tlačítkem na možnost **vlastnosti** v části **protokoly pro MSSQLSERVER**. Přepněte na kartu **certifikát** , jako certifikát vyberte **datový sklad SQL Server identifikační certifikát** a změny uložte.

        1. V části **SQL Server služby**restartujte **službu SQL Server**. Pokud je na serveru, který je hostitelem databáze datového skladu, nainstalován také SQL Reporting služby, restartujte služby **Reporting Service** .

1. Na serveru, který je hostitelem nástroje SQL Server Reporting Services otevřete konzolu MMC a přidejte modul snap-in **certifikáty** . Vyberte možnost **účet počítače**. Do složky **důvěryhodných kořenových certifikačních autorit** importujte **datový sklad SQL Server identifikační certifikát**.

## <a name="data-flow"></a>Tok dat

:::image type="content" source="media/datawarehouse.png" alt-text="Diagram znázorňující tok logických dat mezi součástmi webu pro datový sklad" lightbox="media/datawarehouse.png":::

### <a name="data-storage-and-synchronization"></a>Ukládání a synchronizace dat

| Krok   | Podrobnosti  |
|--------|----------|
| **1**  | Server lokality přenáší a ukládá data v databázi lokality. |
| **2**  | V závislosti na plánu a konfiguraci získá bod služby datového skladu data z databáze lokality. |
| **3**  | Bod služeb datového skladu přenáší a ukládá kopii synchronizovaných dat v databázi datového skladu. |

### <a name="reporting-flow"></a>Tok generování sestav

| Krok   | Podrobnosti  |
|--------|----------|
| **A**  | Pomocí předdefinovaných sestav uživatel požaduje data. Tento požadavek je předán bodu služby Reporting Service pomocí SQL Server Reporting Services. |
| **B**  | Většina sestav je pro aktuální informace a tyto požadavky se spouštějí v databázi lokality. |
| **R**  | Když sestava vyžádá historická data pomocí jedné ze sestav s *kategorií* **datového skladu**, spustí se požadavek na databázi datového skladu. |
