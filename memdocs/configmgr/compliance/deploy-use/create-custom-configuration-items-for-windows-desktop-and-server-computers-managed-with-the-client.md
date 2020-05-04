---
title: Vytváření vlastních položek konfigurace
titleSuffix: Configuration Manager
description: Správa nastavení pro počítače a servery s Windows s vlastní položkou konfigurace pro stolní počítače a servery s Windows
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f11066918854d72af0f1160d7d7569a93d7ebe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712383"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Vytváření vlastních položek konfigurace pro desktopové a serverové počítače s Windows spravované pomocí klienta Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


Pomocí položky Configuration Manager **vlastní stolní počítače a servery s Windows** můžete spravovat nastavení počítačů a serverů s Windows, které jsou spravované klientem Configuration Manager.  



## <a name="start-the-wizard"></a>Spustit Průvodce

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**a vyberte uzel **položky konfigurace** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit položku konfigurace**.  

3. Na stránce **Obecné** v **průvodci vytvořením položky konfigurace**zadejte název a volitelný popis položky konfigurace.  

4. V části **Zadejte typ položky konfigurace, který chcete vytvořit** vyberte **Stolní počítače a servery Windows (vlastní)**.  

    > [!TIP]  
    > Chcete-li zadat nastavení metody detekce, pomocí které se bude kontrolovat přítomnost určité aplikace, vyberte **Tato položka konfigurace obsahuje nastavení aplikace**.  

5. Chcete-li při hledání a filtrování položek konfigurace v konzole Configuration Manager, vyberte **kategorie** pro vytvoření a přiřazení kategorií.  



## <a name="detection-methods"></a>Metody detekce  

Pomocí tohoto postupu můžete zadat informace o metodě detekce pro danou položku konfigurace.  

> [!NOTE]  
> Tyto informace platí pouze v případě, že jste vybrali možnost **Tato položka konfigurace obsahuje nastavení aplikace** na stránce **Obecné** v průvodci.  

Metoda detekce v Configuration Manager obsahuje pravidla, která se používají k detekci, jestli je aplikace nainstalovaná na počítači. K tomuto zjištění dojde předtím, než klient vyhodnotí dodržování předpisů pro položku konfigurace. Chcete-li zjistit, zda je nainstalovaná určitá aplikace, můžete zjistit přítomnost souboru Instalační služby systému Windows pro danou aplikaci, použít vlastní skript, nebo vybrat možnost **Vždy předpokládat, že je aplikace nainstalovaná**, která vyhodnotí dodržování předpisů položkou konfigurace bez ohledu na to, jestli je aplikace nainstalovaná, nebo ne.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Zjištění instalace aplikace pomocí souboru Instalační služba systému Windows  

1. Na stránce **metody detekce** v **Průvodci vytvořením položky konfigurace**vyberte možnost **použití zjišťování instalační služba systému Windows**.  

2. Vyberte **otevřít**, vyhledejte soubor Instalační služba systému Windows (. msi), který chcete zjistit, a pak vyberte **otevřít**.  

3. Pole **verze** se automaticky naplní číslem verze Instalační služba systému Windows souboru. Pokud je zobrazená hodnota nesprávná, zadejte nové číslo verze sem.  

4. Chcete-li zjistit každý uživatelský profil v počítači, vyberte možnost **Tato aplikace je nainstalována pro jednoho nebo více uživatelů**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Detekce konkrétního typu aplikace a nasazení  

1. Na stránce **metody detekce** v **Průvodci vytvořením položky konfigurace**vyberte možnost **zjistit konkrétní typ aplikace a nasazení**. Zvolte **Vybrat**.   

2. V dialogovém okně **Určit aplikaci** vyberte aplikaci a přidružený typ nasazení, které chcete zjistit.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Detekce instalace aplikace pomocí vlastního skriptu  

1. Na stránce **metody detekce** v **Průvodci vytvořením položky konfigurace**vyberte možnost k **detekci této aplikace použít vlastní skript**.  

2. V seznamu vyberte jazyk skriptu. Vyberte z těchto formátů:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Počínaje verzí 1810 se při spuštění skriptu Windows PowerShellu jako metody detekce volá klient Configuration Manager PowerShell s `-NoProfile` parametrem. Tato možnost spustí PowerShell bez profilů. Profil PowerShellu je skript, který se spustí při spuštění PowerShellu. <!--3607762-->  

3. Vyberte **otevřít**, přejděte ke skriptu, který chcete použít, a pak vyberte **otevřít**.  



## <a name="specify-supported-platforms"></a>Určení podporovaných platforem  

Na stránce **podporované platformy** v **Průvodci vytvořením položky konfigurace**vyberte verze systému Windows, u kterých chcete vyhodnotit dodržování předpisů u položky konfigurace, nebo zvolte **možnost Vybrat vše**.

**Verzi Windows můžete zadat také ručně**. Vyberte **Přidat** a zadejte jednotlivé části čísla sestavení Windows.

> [!NOTE]
> Při zadávání systému Windows Server 2016 zahrnuje i výběr `All Windows Server 2016 and higher 64-bit)` pro systém windows server 2019. Chcete-li zadat pouze Windows Server 2016, použijte možnost k **Určení verze systému Windows ručně**. <!--5866480-->



##  <a name="configure-settings"></a>Konfigurace nastavení  

Pomocí tohoto postupu můžete nakonfigurovat nastavení položky konfigurace.  

Nastavení představuje obchodní nebo technické podmínky, které se používají k vyhodnocení kompatibility v klientských zařízeních. Můžete nakonfigurovat nové nastavení, nebo přejít na stávající nastavení v referenční počítači.  

1. Na stránce **Nastavení** v **Průvodci vytvořením položky konfigurace**vyberte **Nový**.  

2. Na kartě **Obecné** v dialogovém okně **Vytvořit nastavení** zadejte tyto informace:  

    - **Název**: Zadejte jedinečný název pro toto nastavení. Opět můžete použít maximálně 256 znaků.  

    - **Popis**: zadejte popis nastavení. Opět můžete použít maximálně 256 znaků.  

    - **Typ nastavení**: v seznamu vyberte jeden z následujících typů nastavení, který se má použít pro toto nastavení:  
        - [Dotaz služby Active Directory](#bkmk_adquery)
        - [Assembly](#bkmk_assembly)
        - [Systém souborů](#bkmk_file)
        - [Metabáze služby IIS](#bkmk_iis)
        - [Klíč registru](#bkmk_regkey)
        - [Hodnota registru](#bkmk_regval)
        - [Skript](#bkmk_script)
        - [Dotaz SQL](#bkmk_sql)
        - [Dotaz jazyka WQL](#bkmk_wql)
        - [Dotaz XPath](#bkmk_xpath)

    - **Datový typ**: vyberte formát, ve kterém podmínka vrátí data, než se použije k vyhodnocení nastavení. Seznam **datový typ** se nezobrazuje u všech typů nastavení.  

        > [!Tip]  
        > Datový typ s **plovoucí** desetinnou čárkou podporuje za desetinnou čárkou pouze tři číslice.  

3. Další podrobnosti tohoto nastavení můžete nakonfigurovat v seznamu **Typ nastavení**. Položky, které můžete nakonfigurovat, se liší v závislosti na zvoleném typu nastavení.  

4. Výběrem **OK** uložte nastavení a zavřete dialogové okno **vytvořit nastavení** .  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a>Dotaz služby Active Directory

- **Předpona protokolu LDAP**: Zadejte platnou předponu pro dotaz Active Directory Domain Services pro vyhodnocení dodržování předpisů v klientských počítačích. Chcete-li provést hledání globálního katalogu, použijte `LDAP://` buď `GC://`nebo.  

- **Rozlišující název (DN)**: zadejte rozlišující název objektu Active Directory Domain Services, u kterého je vyhodnocena shoda v klientských počítačích.  

- **Vyhledávací filtr**: Určete volitelný filtr LDAP pro upřesnění výsledků z dotazu Active Directory Domain Services pro vyhodnocení dodržování předpisů v klientských počítačích. Chcete-li vrátit všechny výsledky z dotazu, `(objectclass=*)`zadejte.  

- **Obor vyhledávání**: zadejte obor vyhledávání v Active Directory Domain Services  

    - **Základ**: dotazuje pouze zadaný objekt  

    - **Jedna úroveň**: Tato možnost se v této verzi Configuration Manager nepoužívá.  

    - **Podstrom**: provede dotazování zadaného objektu a jeho kompletního podstromu v adresáři.  

- **Vlastnost**: Určete vlastnost objektu Active Directory Domain Services, která se používá k vyhodnocení shody v klientských počítačích.  

    Například pokud chcete zadat dotaz na vlastnost služby Active Directory, která ukládá počet nesprávných zadání hesla uživatelem, zadejte `badPwdCount` do tohoto pole.  

- **Dotaz**: zobrazí dotaz sestavený z položek v **předponě LDAP**, **rozlišující název (DN)**, **vyhledávací filtr** (Pokud je zadaný) a **vlastnost**.  


### <a name="assembly"></a><a name="bkmk_assembly"></a>Shromážděním

Sestavení je úsek kódu, který může být sdílen mezi různými aplikacemi. Sestavení mohou mít souborovou příponu .dll nebo .exe. Globální mezipaměť sestavení (GAC) je `%SystemRoot%\Assembly` složka v klientských počítačích. Tato mezipaměť je tam, kde Windows ukládá všechna sdílená sestavení.  

- **Název sestavení:** Určuje název objektu sestavení, který chcete vyhledat. Název nemůže být stejný jako jiné objekty sestavení stejného typu. Nejprve ji Zaregistrujte v globální mezipaměti sestavení (GAC). Název sestavení může mít délku až 256 znaků.  


### <a name="file-system"></a><a name="bkmk_file"></a>Systém souborů

- **Typ**: v seznamu vyberte, jestli chcete vyhledat **soubor** nebo **složku**.  

- **Cesta**: zadejte cestu k zadanému souboru nebo složce v klientských počítačích. V cestě můžete zadat proměnné prostředí systému a `%USERPROFILE%` proměnnou prostředí.  

    > [!NOTE]  
    > Použijete-li `%USERPROFILE%` proměnnou prostředí v poli **cesta** nebo **název souboru nebo složky** , klient Configuration Manager prohledá všechny uživatelské profily v klientském počítači. Výsledkem tohoto chování může být vyhledání více instancí souboru nebo složky.  
    >   
    > Pokud nastavení dodržování předpisů nemá přístup k zadané cestě, vygeneruje se chyba zjišťování. Kromě toho pokud se soubor, který hledáte, právě používá, také se vygeneruje chyba zjišťování.  

    > [!Tip]  
    > Vyberte **Procházet** a nakonfigurujte nastavení z hodnot v referenčním počítači.   

- **Název souboru nebo složky**: zadejte název objektu souboru nebo složky, který chcete vyhledat. V názvu souboru nebo složky můžete zadat proměnné `%USERPROFILE%` prostředí systému a proměnnou prostředí. Můžete také použít zástupné znaky `*` a `?` v názvu souboru.  

    > [!NOTE]  
    > Pokud zadáte název souboru nebo složky a použijete zástupné znaky, může tato kombinace způsobit velký počet výsledků. Může to také způsobit vysoké využití prostředků v klientském počítači a vysoký síťový provoz při vytváření sestav Configuration Manager.  

- **Zahrnout podsložky**: Vyhledá také všechny podsložky v zadané cestě.  

- **Tento soubor nebo složka jsou přidruženy k 64 bitové aplikaci**: Pokud je tato možnost povolena, prohledejte pouze 64 umístění souborů, `%ProgramFiles%` jako je například na 64-bitové počítače. Pokud tato možnost není povolená, hledejte jak v 64 umístění, tak na 32 umístění, jako `%ProgramFiles(x86)%`je například.  

    > [!NOTE]  
    > Pokud jeden soubor nebo složka existuje v jednom 64bitovém počítači v 64bitovém i 32bitovém umístění se systémovými soubory, zjistí globální podmínka více souborů.  

    Typ nastavení **systému souborů** nepodporuje zadání cesty UNC ke sdílené síťové složce v poli **cesta** .  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a>Metabáze služby IIS

- **Cesta k metabázi**: Zadejte platnou cestu k metabázi Internetová informační služba (IIS). Například, `/LM/W3SVC/`.  

- **ID vlastnosti**: zadejte číselnou vlastnost nastavení metabáze služby IIS.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a>Klíč registru

- **Podregistr**: vyberte podregistr registru, který chcete vyhledat.

    > [!Tip]  
    > Vyberte **Procházet** a nakonfigurujte nastavení z hodnot v referenčním počítači. Chcete-li přejít na klíč registru na vzdáleném počítači, povolte službu **Remote Registry** na vzdáleném počítači.  

- **Klíč**: zadejte název klíče registru, který chcete vyhledat. Použijte formát `key\subkey`.  

- **Tento klíč registru je přidružen k 64 bitové aplikaci**: Kromě klíčů registru 32 na klientech, na kterých je 64 spuštěná 16Bitová verze systému Windows, hledejte i 64 klíče registru.  

    > [!NOTE]  
    > Pokud je stejný klíč registru v 64bitovém počítači přítomný v 64bitovém i 32bitovém umístění registru, globální podmínka zjistí oba klíče registru.  


### <a name="registry-value"></a><a name="bkmk_regval"></a>Hodnota registru

- **Podregistr**: vyberte podregistr registru, který se má hledat.  

    > [!Tip]  
    > Vyberte **Procházet** a nakonfigurujte nastavení z hodnot v referenčním počítači. Pokud chcete přejít na hodnotu registru na vzdáleném počítači, povolte ve vzdáleném počítači službu **Remote Registry** . Pro přístup ke vzdálenému počítači potřebujete také oprávnění správce.  

- **Klíč**: zadejte název klíče registru, který chcete vyhledat. Použijte formát `key\subkey`.  

- **Hodnota**: zadejte hodnotu, která musí být obsažena v rámci zadaného klíče registru.  

- **Tento klíč registru je přidružen k 64 bitové aplikaci**: Kromě klíčů registru 32 na klientech, na kterých je 64 spuštěná 16Bitová verze systému Windows, hledejte i 64 klíče registru.  

    > [!NOTE]  
    > Pokud je stejný klíč registru v 64bitovém počítači přítomný v 64bitovém i 32bitovém umístění registru, globální podmínka zjistí oba klíče registru.  


### <a name="script"></a><a name="bkmk_script"></a>Pravidel

Hodnota vrácená skriptem se použije k vyhodnocení dodržování předpisů globální podmínkou. Například když použijete jazyk VBScript, můžete pomocí příkazu **WScript.Echo Result** vrátit hodnotu proměnné *Result* do globální podmínky.  

- **Skript zjišťování**: vyberte **Přidat skript**a zadejte nebo přejděte do skriptu. Tento skript slouží k vyhledání hodnoty. Můžete použít skripty prostředí Windows PowerShell, VBScript nebo Microsoft JScript.  

- Skript napravení **(volitelné)**: vyberte **Přidat skript**a zadejte nebo přejděte do skriptu. Tento skript slouží k nápravě hodnot nastavení, které nedodržují předpisy. Můžete použít skripty prostředí Windows PowerShell, VBScript nebo Microsoft JScript.  

- **Spusťte skripty pomocí přihlašovacích údajů přihlášeného uživatele**: Pokud povolíte tuto možnost, skript se spustí na klientských počítačích, které používají přihlašovací údaje přihlášeného uživatele.  

> [!Note]  
> Počínaje verzí 1810 se při použití prostředí Windows PowerShell jako skriptu pro zjišťování nebo napravení vyvolají klient Configuration Manager PowerShell s `-NoProfile` parametrem. Tato možnost spustí PowerShell bez profilů. Profil PowerShellu je skript, který se spustí při spuštění PowerShellu. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a>Dotaz SQL

- **SQL Server instance**: vyberte, jestli chcete, aby se dotaz SQL spouštěl na výchozí instanci, na všech instancích nebo na zadaném názvu instance databáze.  

    > [!NOTE]  
    > Název instance musí odkazovat na místní instanci serveru SQL. Chcete-li odkazovat na skupinu prostředků clusteru serveru SQL, použijte nastavení skriptu.  

- **Databáze**: zadejte název databáze Microsoft SQL Server, pro kterou chcete spustit dotaz SQL.  

- **Sloupec**: zadejte název sloupce vrácený příkazem Transact-SQL, který se používá k vyhodnocení shody globální podmínky.  

- **Příkaz Transact-SQL**: zadejte úplný dotaz SQL, který chcete použít pro globální podmínku. Pokud chcete použít existující dotaz SQL, vyberte **otevřít**.  

    > [!IMPORTANT]  
    > Nastavení dotazu SQL nepodporuje žádné příkazy SQL, které mění databázi. Můžete používat jenom příkazy SQL, které čtou informace z databáze.  


### <a name="wql-query"></a><a name="bkmk_wql"></a>Dotaz jazyka WQL

- **Obor názvů**: zadejte obor názvů WMI, který je vyhodnocován pro dodržování předpisů na klientských počítačích. Výchozí hodnota je `root\cimv2`.  

- **Třída**: zadejte cílovou třídu služby WMI ve výše uvedeném oboru názvů.  

- **Vlastnost**: zadejte cílovou vlastnost rozhraní WMI ve výše uvedené třídě.  

- **Klauzule WHERE dotazu jazyka WQL**: Určete klauzuli opravňující k omezení výsledků. Například pro dotazování služby DHCP ve třídě Win32_Service může být `Name = 'DHCP' and StartMode = 'Auto'`klauzule WHERE.   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a>Dotaz XPath

- **Cesta**: zadejte cestu k souboru. XML v klientských počítačích, který se používá k vyhodnocení dodržování předpisů. Configuration Manager podporuje použití všech proměnných prostředí systému Windows a `%USERPROFILE%` uživatelské proměnné v názvu cesty.  

- **Název souboru XML**: zadejte název souboru obsahujícího dotaz XML ve výše uvedené cestě.  

- **Zahrnout podsložky**: tuto možnost povolte, pokud chcete prohledávat všechny podsložky v zadané cestě.  

- **Tento soubor je přidružen k 64 bitové aplikaci**: 32 kromě umístění `%Windir%\System32` `%Windir%\Syswow64` systémových souborů v systému Configuration Manager klientů, na kterých je 64 spuštěná 16bitová verze systému Windows, hledejte umístění systémového souboru systému 64.  

- **Dotaz XPath**: Zadejte platný úplný dotaz XPath (XML Path Language).  

- **Obory názvů**: Identifikujte obory názvů a předpony, které se mají použít během dotazu XPath.  

Pokud se pokusíte vyhledat zašifrovaný soubor. XML, nastavení dodržování předpisů soubor najde, ale dotaz XPath negeneruje žádné výsledky. Klient Configuration Manager negeneruje chybu.  

Pokud dotaz XPath není platný, nastavení se vyhodnotí jako nedodržující předpisy na klientských počítačích.  



##  <a name="configure-compliance-rules"></a>Konfigurace pravidel dodržování předpisů  

Pravidla dodržování předpisů určují podmínky, které definují dodržování předpisů položkou konfigurace. Nastavení musí mít aspoň jedno pravidlo dodržování předpisů, aby se dalo vyhodnotit, jestli jestli dané předpisy splňuje. Nastavení rozhraní WMI, registru a skriptu umožňuje opravit hodnoty, o kterých zjistíte, že nedodržují předpisy. Můžete vytvořit nová pravidla nebo vyhledat stávající nastavení v libovolné položce konfigurace a vybrat v něm pravidla.  


### <a name="to-create-a-compliance-rule"></a>Postup pro vytvoření pravidla dodržování předpisů  

1. Na stránce **pravidla dodržování předpisů** v **Průvodci vytvořením položky konfigurace**vyberte možnost **Nový**.  

2. V dialogovém okně **Vytvořit pravidlo** zadejte následující údaje:  

    - **Název**: zadejte název pravidla dodržování předpisů.  

    - **Popis**: zadejte popis pravidla dodržování předpisů.  

    - **Vybrané nastavení**: kliknutím na **Procházet** otevřete dialogové okno **Vybrat nastavení** . Vyberte nastavení, pro které chcete definovat pravidlo, nebo vyberte **nové nastavení**. Až budete hotovi, zvolte **Vybrat**.  

        > [!Tip]  
        > Chcete-li zobrazit informace o aktuálně vybraném nastavení, vyberte možnost **vlastnosti**.  

    - **Typ pravidla**: Vyberte typ pravidla dodržování předpisů, který chcete použít:  

        - **Hodnota**: Vytvořte pravidlo, které porovnává hodnotu vrácenou položkou konfigurace s vámi zadanou hodnotou. Další informace o dalších nastaveních najdete v tématu [pravidla hodnot](#bkmk_value).  

        - **Existenční**: Vytvořte pravidlo, které vyhodnotí nastavení v závislosti na tom, jestli existuje v klientském zařízení, nebo na počtu nalezených časů. Další informace o dalších nastaveních najdete v tématu [pravidla existenční](#bkmk_exist).  

3. Kliknutím na **tlačítko OK** zavřete dialogové okno **vytvořit pravidlo** .  




### <a name="value-rules"></a><a name="bkmk_value"></a>Pravidla hodnoty  

- **Vlastnost**: vlastnost objektu, která má být zkontrolována, se liší v závislosti na vybraném nastavení. Dostupné vlastnosti se liší v závislosti na typu nastavení. 

- **Nastavení musí splňovat následující podmínky...**: dostupná pravidla nebo oprávnění se liší v závislosti na typu nastavení.

- **Napravit pravidla nesplňující požadavky**, je-li to podporováno: tuto možnost vyberte, pokud chcete Configuration Manager automaticky opravovat pravidla, která nedodržují předpisy. Configuration Manager podporuje tuto akci s následujícími typy pravidel:  

    - **Hodnota registru**: Pokud není kompatibilní, klient nastaví hodnotu registru. Pokud neexistuje, klient vytvoří hodnotu.  

    - **Skript**: klient používá skript pro nápravu, který jste zadali s nastavením.  

    - **Dotaz jazyka WQL**  

    > [!IMPORTANT]  
    > Napravit pravidla nedodržující předpisy můžete pouze v případě, že je operátor pravidla nastavený na **Rovná se**.  

- **Pokud není nalezena instance tohoto nastavení, nahlásit neshodu**: Pokud toto nastavení není v klientských počítačích nalezeno, povolte tuto možnost, aby položka konfigurace nahlásila nedodržení předpisů.  

- **Závažnost neshody pro sestavy**: Zadejte úroveň závažnosti, která se nahlásí v Configuration Manager sestavy, pokud toto pravidlo dodržování předpisů selhává. K dispozici jsou následující úrovně závažnosti:  
    - **Žádné**  
    - **Informace**  
    - **Upozornění**  
    - **Kritická**  
    - **Kritické s událostí**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u **kritického**selhání závažnost. Tato úroveň závažnosti je rovněž zaznamenána jako událost systému Windows v protokolu událostí aplikací.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a>Pravidla existenční 

> [!NOTE]  
> Zobrazené možnosti se můžou lišit v závislosti na typu nastavení, pro které konfigurujete pravidlo.  

- **Nastavení musí existovat na klientských zařízeních**  

- **Nastavení nesmí existovat na klientských zařízeních**  

- **Počet výskytů tohoto nastavení:**  

- **Závažnost neshody pro sestavy**: Zadejte úroveň závažnosti, která se nahlásí v Configuration Manager sestavy, pokud toto pravidlo dodržování předpisů selhává. K dispozici jsou následující úrovně závažnosti:  
    - **Žádné**  
    - **Informace**  
    - **Upozornění**  
    - **Kritická**  
    - **Kritické s událostí**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u **kritického**selhání závažnost. Tato úroveň závažnosti je rovněž zaznamenána jako událost systému Windows v protokolu událostí aplikací.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a>Sledování oprav položek konfigurace
<!--4261411-->
*(Představené ve verzi 2002)*

Od verze Configuration Manager 2002 můžete **sledovat historii oprav, pokud** je tato možnost podporovaná ve vašich pravidlech dodržování předpisů v položkách konfigurace. Pokud je tato možnost povolena, jakákoli náprava, ke které dojde v klientovi pro položku konfigurace, vygeneruje stavovou zprávu. Historie je uložena v databázi Configuration Manager.

Sestavujte vlastní sestavy, abyste zobrazili historii oprav pomocí **v_CIRemediationHistory**veřejného zobrazení. `RemediationDate` Sloupec je čas ve standardu UTC, kdy klient spustil nápravu. `ResourceID` Identifikuje zařízení. Vytváření vlastních sestav pomocí zobrazení **v_CIRemediationHistory** vám pomůže:

- Identifikujte možné problémy se skripty pro nápravu
- Vyhledá trendy v nápravách, jako je například klient, který je konzistentně nekompatibilní s jednotlivými zkušebními cykly.

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Povolí možnost sledovat historii nápravy, pokud se podporuje.

- V případě nových položek konfigurace přidejte na stránce **Nastavení** Průvodce na kartě **pravidla dodržování** předpisů možnost **sledovat historii nápravy** , když vytvoříte nové nastavení.
- U stávajících položek konfigurace přidejte na kartě **pravidla dodržování** předpisů ve **vlastnostech**položky konfigurace možnost **sledovat historii nápravy** .
[![Sledovat historii nápravy, pokud je podporovaná ve verzi 2002](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Další kroky

[Vytváření standardních hodnot konfigurace](create-configuration-baselines.md)
