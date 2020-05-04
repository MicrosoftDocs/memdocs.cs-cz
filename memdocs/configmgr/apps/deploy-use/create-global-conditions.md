---
title: Vytváření globálních podmínek
titleSuffix: Configuration Manager
description: Vytvořte globální podmínky pro určení způsobu, jakým je aplikace poskytována a nasazena do klientských zařízení.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710283"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Vytvoření globálních podmínek v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager globální podmínky jsou pravidla, která představují obchodní nebo technické podmínky, které můžete použít k určení toho, jak je aplikace poskytována a nasazena do klientských zařízení. Globální podmínky lze zobrazit v průvodci vytvořením typu nasazení na stránce **Požadavky** .  

> [!NOTE]  
>  Globální podmínky lze upravovat pouze z lokality, ve které byly vytvořeny.  

 Configuration Manager globální podmínky můžete vytvořit pomocí následujících postupů.  

## <a name="provide-basic-information-about-the-global-condition"></a>Zadání základních informací o globální podmínce  
 Využít lze několik typů globální podmínek. S různými typy globálních podmínek jsou spojeny různé možnosti. Když vyberete konkrétní typ globální podmínky, Configuration Manager zobrazí možnosti, které se vztahují na váš výběr.  

1.  V konzole Configuration Manager vyberte možnost **softwarová knihovna** > **Správa** > aplikací**globální podmínky**.  

3.  Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit globální podmínku**.  

4.  V dialogovém okně **Vytvořit globální podmínku** zadejte název a volitelný popis globální podmínky.  

5.  V rozevíracím seznamu **typ zařízení** vyberte, zda je globální podmínka určena pro počítač se **systémem Windows** nebo mobilní zařízení se **systémem Windows** .  

6.  Z rozbalovacího seznamu **Typ podmínky** vyberte jednu z následujících možností:  

    -   **Nastavení** – Tato možnost zkontroluje existenci jedné nebo více položek v klientských zařízeních. Můžete například zjistit, že v klientském zařízení existuje soubor, složka nebo hodnota klíče registru.  

    -   **Výraz** – Tato možnost umožňuje nastavit složitější pravidla, která zkontrolují, jestli je podmínka na klientských zařízeních splněná. Například můžete zjistit, zda je fyzická paměť v počítači mezi 2 GB a 4 GB nebo zda mobilní zařízení používá vstup z dotykového zobrazení.  

## <a name="set-up-rules-for-the-global-condition"></a>Nastavení pravidel pro globální podmínku  
 Postup definování pravidel globální podmínky se liší v závislosti na tom, zda konfigurujete nastavení, nebo výraz. Pomocí příslušného postupu můžete nastavit nastavení nebo výraz pro globální podmínku.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Nastavení nastavení globální podmínky  

1. V rozbalovacím seznamu **Typ podmínky** vyberte položku **Nastavení**.  

2. V rozbalovacím seznamu **Typ nastavení** vyberte položku, která má být použita jako podmínka, jejíž požadavky se budou kontrolovat. K dispozici jsou následující typy nastavení a konfigurace.  

   - **Dotaz služby Active Directory**  

     -   **Předpona protokolu LDAP** – Zadejte platnou předponu protokolu LDAP k dotazu služby Active Directory Domain Services, pomocí nějž bude vyhodnocena shoda v klientských počítačích. Použít můžete předponu **LDAP://** nebo **GC://**.  

     -   **Rozlišující název (DN)** – zadejte rozlišující název objektu Active Directory Domain Services, u kterého bude vyhodnocena shoda v klientských počítačích.  

     -   **Vyhledávací filtr** – Zadejte volitelný filtr LDAP k zpřesnění výsledků z dotazu služby Active Directory Domain Services, pomocí nějž bude vyhodnocena shoda v klientských počítačích.  

     -   **Obor vyhledávání** – Zadejte obor vyhledávání ve službě Active Directory Domain Services:  

         -   **Základ** – dotazuje pouze zadaný objekt.  

         -   **Jedna úroveň** – Tato možnost se v této verzi Configuration Manager nepoužívá.  

         -   **Podstrom** – dotazuje se na zadaný objekt a jeho úplný podstrom v adresáři.  

     -   **Vlastnost** – Udává vlastnost objektu služby Active Directory Domain Services, která bude použita k vyhodnocení shody v klientských počítačích.  

     -   **Dotaz** – zobrazí dotaz LDAP vytvořený z položek v **předponě LDAP**, **rozlišující název (DN)**, **vyhledávací filtr** (Pokud je zadaný) a **vlastnost**. Tento dotaz bude použit k vyhodnocení shody v klientských počítačích.  

   - **Assembly**  

     -   **Název sestavení** – Udává název objektu sestavení, který má být hledán. Název nesmí být stejný jako žádný jiný objekt sestavení stejného typu a název musí být zaregistrován v globální mezipaměti sestavení (GAC). Název sestavení může mít maximálně 256 znaků.  

     > [!NOTE]  
     >  Sestavení je úsek kódu, který může být sdílen mezi různými aplikacemi. Sestavení mohou mít příponu názvu souboru. dll nebo. exe. Globální mezipaměť sestavení je složka s názvem *%systemroot%\assembly* umístěná v klientském počítači, v níž jsou uložena všechna sdílená sestavení.  

   - **Systém souborů**  

     - **Typ** – v rozevíracím seznamu vyberte, zda chcete vyhledat **soubor** nebo **složku**.  

     - **Cesta** – Zadejte cestu k požadovanému souboru nebo složce v klientském počítači. V cestě můžete zadat proměnné prostředí systému a proměnnou prostředí *%USERPROFILE%* .  

       > [!NOTE]  
       >  Použijete-li proměnnou prostředí *%USERPROFILE%* v poli **Cesta** nebo **Název souboru nebo složky** , budou prohledány všechny profily uživatelů v klientském počítači. Následkem toho může být nalezeno několik instancí souboru nebo složky.  

     - **Název souboru nebo složky** – Zadejte název objektu souboru nebo složky, který chcete vyhledávat. V názvu souboru nebo složky můžete zadat proměnné prostředí systému a proměnnou prostředí *%USERPROFILE%*. Můžete také použít * a? v názvu souboru se nachází zástupné znaky.  

       > [!NOTE]  
       >  Pokud zadáte název souboru nebo složky se zástupnými znaky, může být počet výsledků velký. Výsledkem může být použití vysokého využití prostředků v klientském počítači a vysokém provozu v síti při hlášení výsledků do Configuration Manager.  

     - **Zahrnout podsložky** – Povolte tuto možnost, pokud chcete prohledávat také všechny podsložky zadané cesty.  

     - **Tento soubor nebo složka jsou přidruženy k 64 aplikaci** – určete, zda má být 32 kromě umístění% windir% \syswow64 (*% windir%* \syswow64 jako) v Configuration Managerch klientech, na kterých je 64 spuštěná 16bitová verze systému Windows, prohledáno umístění systémového souboru (%*windir%*) 64.  

       > [!NOTE]  
       >  Pokud v 64bitovém počítači existuje stejný soubor nebo složka jak v umístění 64bitových, tak v umístění 32bitových systémových souborů, globální podmínka najde více souborů.  

       Typ nastavení **Systém souborů** nepodporuje určení cesty UNC ke sdílení sítě v poli **Cesta** .  

   - **Metabáze služby IIS**  

     -   **Cesta metabáze** – Zadejte platnou cestu k metabázi služby IIS.  

     -   **ID vlastnosti** – Zadejte číselnou vlastnost nastavení metabáze služby IIS.  

   - **Klíč registru**  

     -   **Podregistr** – v rozevíracím seznamu vyberte podregistr registru, ve kterém chcete vyhledávat.  

     -   **Klíč** – Zadejte název klíče registru, který chcete vyhledávat. Název zadejte ve formátu *key\subkey*.  

     -   **Tento klíč registru je přidružen k 64bitové aplikaci** – Udává, zda mají být v klientech s 64bitovou verzí systému Windows vyhledávány kromě 32bitových klíčů registru také 64bitové klíče registru.  

         > [!NOTE]  
         >  Pokud v 64bitovém počítači existuje stejný klíč registru jak v 64bitovém, tak v 32bitovém umístění registru, globální podmínka najde oba typy klíčů registru.  

   - **Hodnota registru**  

     -   **Podregistr** – Z rozbalovacího seznamu vyberte podregistr registru, v němž chcete vyhledávat.  

     -   **Klíč** – Zadejte název klíče registru, který chcete vyhledávat. Název zadejte ve formátu *key\subkey*.  

     -   **Hodnota** – Zadejte hodnotu, kterou musí daný klíč registru obsahovat.  

     -   **Tento klíč registru je přidružen k 64bitové aplikaci** – Udává, zda mají být v klientech s 64bitovou verzí systému Windows vyhledávány kromě 32bitových klíčů registru také 64bitové klíče registru.  

         > [!NOTE]  
         >  Pokud v 64bitovém počítači existuje stejný klíč registru jak v 64bitovém, tak v 32bitovém umístění registru, globální podmínka najde oba typy klíčů registru.  

   - **Skript**  

     -   **Skript zjišťování** – klikněte na tlačítko **Přidat** a zadejte, nebo přejděte ke skriptu, který chcete použít. Můžete použít skripty Windows PowerShell, VBScript nebo JScript.  

     -   **Spouštět skripty pomocí přihlašovacích údajů přihlášeného uživatele** – Pokud povolíte tuto možnost, skript se spustí v klientských počítačích s použitím přihlašovacích údajů uživatele, který je přihlášený.  

         > [!NOTE]  
         >  Hodnota vrácená skriptem bude použita k vyhodnocení shody globální podmínky. Pokud například použijete jazyk VBScript, můžete použít příkaz **WScript. echo Result** a vrátit hodnotu proměnné výsledku do globální podmínky.  
         >   
         >  Pokud váš skript vrátí více hodnot, musí být tyto hodnoty na jednom řádku a odděleny středníkem. V případě, že je každá hodnota na samostatném řádku, vyhodnocení se nezdaří.  

   - **Dotaz SQL**  

     -   **Instance serveru SQL** – Vyberte, zda má být příkaz jazyka SQL spuštěn na výchozí instanci, na všech instancích nebo na instanci databáze zadaného názvu.  

         > [!NOTE]  
         >  Název instance musí odkazovat na místní instanci serveru SQL. Chcete-li odkazovat na skupinu prostředků clusteru serveru SQL, použijte nastavení skriptu.  

     -   **Databáze** – Zadejte název databáze Microsoft SQL Server, pro niž bude příkaz jazyka SQL proveden.  

     -   **Sloupec** – Zadejte název sloupce vrácený příkazem Transact-SQL, který má být použit k vyhodnocení shody globální podmínky.  

     -   **Příkaz Transact-SQL** – Zadejte celý příkaz jazyka SQL, který má být použit pro globální podmínku. Můžete také zvolit **otevřít** a otevřít existující dotaz SQL.  

   - **Dotaz jazyka WQL**  

     -   **Obor názvů** – Zadejte obor názvů WMI, který bude použit k vytvoření dotazu jazyka WQL, který bude použit k vyhodnocení shody v klientských počítačích. Výchozí hodnota je Root\cimv2.  

     -   **Třída** – Udává třídu služby WMI, která bude použita k vytvoření dotazu jazyka WQL, který bude použit k vyhodnocení shody v klientských počítačích.  

     -   **Vlastnost** – Udává vlastnost WMI, která bude použita k vytvoření dotazu jazyka WQL, který bude použit k vyhodnocení shody v klientských počítačích.  

     -   **Klauzule WHERE dotazu jazyka WQL** – Položku **Klauzule WHERE dotazu jazyka WQL** můžete použít k zadání klauzule WHERE, která bude použita pro zadaný obor názvů, třídu a vlastnost v klientských počítačích.  

   - **Dotaz XPath**  

     -   **Cesta** – Zadejte cestu k souboru XML na klientských počítačích, které se použijí k vyhodnocení kompatibility. Configuration Manager podporuje použití všech proměnných prostředí systému Windows a uživatelské proměnné *% USERPROFILE%* v názvu cesty.  

     -   **Název souboru XML** – zadejte název souboru obsahujícího dotaz XML, který se má použít k vyhodnocení shody v klientských počítačích.  

     -   **Zahrnout podsložky** – tuto možnost povolte, pokud chcete prohledávat také všechny podsložky v zadané cestě.  

     -   **Tento soubor je přidružen k 64 bitové aplikaci** – určete, zda má být 32 kromě umístění% windir% \syswow64 (*%* windir% \syswow64 jako) v Configuration Managerch klientech, na kterých 64 běží 16bitová verze systému Windows, prohledáno umístění systémového souboru (*% windir%*) 64.  

     -   **Dotaz XPath** – Zadejte platný celý dotaz v jazyce XPath (XML path language), který bude použit k vyhodnocení shody v klientských počítačích.  

     -   **Obory názvů** – Otevře dialogové okno **Obory názvů XML** , v němž můžete identifikovat obory názvů a předpony, jež mají být použity pro dotaz XPath.  

3. V rozbalovacím seznamu **Datový typ** vyberte formát, v němž podmínka vrátí data, než budou použita ke kontrole požadavků.  

   > [!NOTE]  
   >  Rozevírací seznam **datový typ** se nezobrazuje u všech typů nastavení.  

4. Nastavte další podrobnosti o tomto nastavení pod rozevíracím seznamem **Typ nastavení** . Položky, které můžete nastavit, se budou lišit v závislosti na zvoleném typu nastavení.  

5. Kliknutím na **tlačítko OK** uložte pravidlo a zavřete dialogové okno **vytvořit globální podmínku** .  

### <a name="set-up-an-expression-for-the-global-condition"></a>Nastavení výrazu pro globální podmínku  

1.  V rozbalovacím seznamu **Typ podmínky** vyberte položku **Výraz**.  

2.  Zvolením možnosti **Přidat klauzuli** otevřete dialogové okno **Přidat klauzuli** .  

3.  V rozbalovacím seznamu **Vybrat kategorii** vyberte, zda je tento výraz určen pro zařízení, nebo pro uživatele. Jako další alternativu můžete zvolit položku **Vlastní** a použít globální podmínku nakonfigurovanou dříve.  

4.  Z rozbalovacího seznamu **Vybrat podmínku** vyberte podmínku, která má být použita k vyhodnocení, zda uživatel nebo zařízení splňují požadavky pravidla. Obsah tohoto seznamu se bude lišit v závislosti na zvolené kategorii.  

5.  Z rozbalovacího seznamu **Zvolte operátor** vyberte operátor, který bude použit k porovnání zvolené podmínky se zadanou hodnotou, a tím k vyhodnocení, zda uživatel nebo zařízení splňují požadavky pravidla. Dostupní operátoři se budou lišit v závislosti na zvolené podmínce.  

6.  V poli **Hodnota** zadejte hodnoty, které budou použity se zvolenou podmínkou a operátorem k vyhodnocení, zda uživatel nebo zařízení splňují požadavky pravidla. Dostupné hodnoty se budou lišit v závislosti na zvolené podmínce a zvoleném operátorovi.  

7.  Kliknutím na **tlačítko OK** uložte výraz a zavřete dialogové okno **Přidat klauzuli** .  

8.  Až dokončíte přidávání klauzulí do globální podmínky, kliknutím na **tlačítko OK** zavřete dialogové okno **vytvořit globální podmínku** a uložte globální podmínku.  
