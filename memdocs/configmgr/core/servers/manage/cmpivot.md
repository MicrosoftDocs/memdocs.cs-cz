---
title: CMPivot pro data v reálném čase
titleSuffix: Configuration Manager
description: Naučte se používat CMPivot v Configuration Manager k dotazování klientů v reálném čase.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 11b5a58a6d9501b0368fcb0b47bf31df1bd8a6af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700578"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot pro data v reálném čase v Configuration Manager

<!--1358456-->

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager vždy poskytoval velké centralizované úložiště dat zařízení, které zákazníci používají pro účely vytváření sestav. Lokalita obvykle shromažďuje tato data každý týden. Počínaje verzí 1806 je CMPivot novým nástrojem v konzole, který teď poskytuje přístup ke stavu zařízení ve vašem prostředí v reálném čase. Okamžitě spustí dotaz na všech aktuálně připojených zařízeních v cílové kolekci a vrátí výsledky. Tato data pak můžete filtrovat a seskupovat v nástroji. Díky poskytování dat z online klientů v reálném čase můžete rychleji odpovídat na obchodní otázky, řešit problémy a reagovat na incidenty zabezpečení.

Například při [zmírnění ohrožení zabezpečení kanálu na straně spuštění](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)je jedním z požadavků aktualizace systému BIOS. Pomocí CMPivot můžete rychle zadat dotaz na informace o systému BIOS a vyhledat klienty, kteří nedodržují předpisy.

 > [!IMPORTANT]  
 > - Určitý bezpečnostní software může blokovat skripty běžící z c:\windows\ccm\scriptstore.. To může zabránit úspěšnému spuštění dotazů CMPivot. Při spuštění CMPivot PowerShellu může taky dojít k vygenerování událostí auditu nebo upozornění na určitý bezpečnostní software.
 > - Určitý antimalwarový software může nechtěně aktivovat události proti Configuration Manager spuštění skriptů nebo funkcí CMPivot. Doporučuje se vyloučit%windir%\CCM\ScriptStore, aby antimalwarový software mohl spouštět tyto funkce bez rušivých zásahů.


## <a name="prerequisites"></a>Předpoklady

Pro použití CMPivot jsou vyžadovány následující komponenty:

- Upgradujte cílová zařízení na nejnovější verzi klienta Configuration Manager.  

- Cíloví klienti vyžadují minimálně verzi 4 prostředí PowerShell.

- Aby bylo možné shromažďovat data pro následující entity, vyžadují Cíloví klienti prostředí PowerShell verze 5,0:  
  - Správci
  - Připojení
  - Příkazu
  - SMBConfig

- CMPivot a instalační program [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) se podepisují pomocí certifikátu **Microsoft Code Signing** Certificate. Pokud tento certifikát není uvedený v úložišti **důvěryhodných vydavatelů** , budete ho muset přidat. V opačném případě CMPivot a instalační program Microsoft Edge se nespustí, když jsou zásady spouštění prostředí PowerShell nastavené na **AllSigned**. <!--7585106-->

## <a name="permissions"></a>Oprávnění

Pro CMPivot jsou potřeba následující oprávnění:

- Oprávnění **číst** pro objekt **skripty SMS**
- Oprávnění ke **spouštění skriptů** pro **kolekci**
   - Alternativně počínaje verzí 1906 můžete použít rutinu **Run CMPivot** v **kolekci**.
- Oprávnění **číst** k **sestavám inventáře**
- Výchozí obor.

> [!NOTE]
> - **Spouštění skriptů** je nadmnožinou oprávnění **Run CMPivot** .
> - Počínaje verzí 1906 byly do předdefinované role **Správce zabezpečení** Configuration Manager [přidány oprávnění pro CMPivot](cmpivot-changes.md#bkmk_cmpivot_secadmin1906) .
 
## <a name="limitations"></a>Omezení

- V hierarchii Připojte konzolu Configuration Manager k *primární lokalitě* , aby bylo možné spustit CMPivot. Pokud je připojená k lokalitě centrální správy (CAS), v konzole nástroje se nezobrazí akce **Spustit CMPivot** .
  - Od verze Configuration Manager 1902 můžete spustit CMPivot z certifikačních autorit. V některých prostředích jsou potřeba další oprávnění. Další informace najdete v tématu [změny CMPivot pro verzi 1902](cmpivot-changes.md#bkmk_cmpivot1902).

- CMPivot vrací pouze data pro klienty připojené k aktuální lokalitě.  

- Pokud kolekce obsahuje zařízení z jiné lokality, CMPivot výsledky jsou pouze ze zařízení v aktuální lokalitě.  

- Nemůžete přizpůsobit vlastnosti entity, sloupce pro výsledky nebo akce v zařízeních.  

- V počítači, na kterém je spuštěná konzola Configuration Manager, může běžet současně jenom jedna instance CMPivot.  

- Ve verzi 1806 dotaz pro entitu **Administrators** funguje pouze v případě, že se skupina jmenuje "Administrators". Nefunguje, pokud je název skupiny lokalizovaný. Například "Administrateurs" ve francouzštině.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Spustit CMPivot

1. V konzole Configuration Manager se připojte k primární lokalitě. Otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **kolekce zařízení** . Vyberte cílovou kolekci a na pásu karet klikněte na tlačítko **Spustit CMPivot** a spusťte nástroj. Pokud tuto možnost nevidíte, zkontrolujte následující konfigurace:  
   - Potvrďte u správce lokality, že váš účet má požadovaná oprávnění. Další informace najdete v tématu [předpoklady](#prerequisites).  
   - Připojte konzolu k *primární lokalitě*.  

2. Rozhraní poskytuje další informace o použití nástroje.  

     - Ručně zadejte řetězce dotazů v horní části nebo klikněte na odkazy v online dokumentaci.  

     - Klikněte na jednu **entitu** a přidejte ji do řetězce dotazu.  

     - Odkazy pro **operátory tabulky**, **agregační funkce**a **skalární funkce** otevřou referenční dokumentaci jazyka ve webovém prohlížeči. CMPivot používá [KQL (Kusto Query Language)](/azure/kusto/query/).  

3. Nechte okno CMPivot otevřené, aby se zobrazily výsledky klientů. Po zavření okna CMPivot se relace dokončí.
   - Pokud byl odeslán dotaz, klienti stále odesílají odpověď na stavovou zprávu serveru.  



## <a name="how-to-use-cmpivot"></a>Jak používat CMPivot

![Ukázka okna CMPivot](media/1358456-cmpivot-sample.png)

Okno CMPivot obsahuje následující prvky:  

1. Kolekce, která CMPivot aktuálně cílí, je v záhlaví v horní části a stavový řádek v dolní části okna. Například "PM_Team_Machines" na výše uvedeném snímku obrazovky.  

2. Podokno vlevo obsahuje seznam **entit** , které jsou k dispozici na klientech. Některé entity spoléhají na rozhraní WMI, zatímco ostatní používají PowerShell k získávání dat od klientů.   

    - Klikněte pravým tlačítkem na entitu a proveďte následující akce:  

       - **Vložit**: přidejte entitu k dotazu na aktuální pozici kurzoru. Dotaz se nespustí automaticky. Tato akce je výchozí, když dvakrát kliknete na entitu. Tuto akci použijte při vytváření dotazu.  

       - **Dotaz na vše**: spustí dotaz pro tuto entitu včetně všech vlastností. Tuto akci použijte k rychlému dotazování na jednu entitu.  

       - **Dotaz podle zařízení**: Spusťte dotaz pro tuto entitu a seskupte výsledky. Například `Disk | summarize dcount( Device ) by Name`.  

    - Rozbalte entitu a zobrazte konkrétní vlastnosti, které jsou k dispozici pro každou entitu. Dvojím kliknutím na vlastnost ji přidejte do dotazu na aktuální pozici kurzoru.  

3. Karta **Domů** zobrazuje obecné informace o CMPivot, včetně odkazů na ukázkové dotazy a podpůrnou dokumentaci.  

4. Na kartě **dotaz** se zobrazí podokno dotazu, podokno výsledků a stavový řádek. Na výše uvedeném příkladu snímku obrazovky je vybraná karta dotaz.  

5. V podokně dotazu můžete sestavit nebo zadat dotaz, který se má spustit na klientech v kolekci.  

    - CMPivot používá podmnožinu [KQL (Kusto Query Language)](/azure/kusto/query/).  

    - Vyjmutí, zkopírování nebo vložení obsahu do podokna dotazu.  
    <!-- markdownlint-disable MD038 -->
    - Ve výchozím nastavení toto podokno používá technologii IntelliSense. Například pokud začnete psát `D` , IntelliSense navrhne všechny entity, které začínají tímto písmenem. Vyberte možnost a stisknutím klávesy TAB ji vložte. Zadejte znak kanálu a mezeru `| ` a potom IntelliSense navrhne všechny operátory tabulky. Vložení `summarize` a zadání prostoru a IntelliSense navrhne všechny agregační funkce. Další informace o těchto operátorech a funkcích získáte kliknutím na kartu **Domů** v CMPivot.  

    - Podokno dotazu také nabízí následující možnosti:  

        - Spusťte dotaz.  

        - Přesunutí zpět a vpřed v seznamu historie dotazů.  

        - Vytvořte přímou kolekci členství.  

        - Exportujte výsledky dotazu do sdíleného svazku clusteru nebo do schránky.  

6. V podokně výsledků se zobrazují data vrácená aktivními klienty pro dotaz.  

   - Dostupné sloupce se liší v závislosti na entitě a dotazu.  

   - Kliknutím na název sloupce seřadíte výsledky podle této vlastnosti.  

   - Kliknutím pravým tlačítkem myši na libovolný název sloupce můžete seskupit výsledky podle stejných informací v tomto sloupci nebo seřadit výsledky.  

   - Kliknutím pravým tlačítkem myši na název zařízení můžete na zařízení provést následující další akce:  

      - **Pivot to**: dotaz na jinou entitu v tomto zařízení.
         - Počínaje verzí 2006 byl **kontingenční tabulka** nahrazená **Pivotem zařízení**. Další informace najdete v tématu [změny CMPivot pro verzi 2006](cmpivot-changes.md#bkmk_2006).

      - **Spustit skript**: spusťte Průvodce spuštěním skriptu, který spustí existující skript PowerShellu na tomto zařízení. Další informace najdete v tématu [spuštění skriptu](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Vzdálené řízení**: na tomto zařízení spusťte relaci vzdáleného řízení Configuration Manager. Další informace najdete v tématu [Postup při vzdálené správě klientského počítače se systémem Windows](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Průzkumník prostředků**: pro toto zařízení spusťte Configuration Manager Průzkumník prostředků. Další informace najdete v tématech [zobrazení inventáře hardwaru](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) nebo [zobrazení inventáře softwaru](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Kliknutím pravým tlačítkem myši na libovolnou buňku mimo zařízení proveďte následující další akce:  

     - **Kopírovat**: zkopírovat text buňky do schránky.  

     - **Zobrazit zařízení pomocí**: dotaz na zařízení s touto hodnotou pro tuto vlastnost. Například z výsledků `OS` dotazu vyberte tuto možnost v buňce v řádku verze: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Zobrazit zařízení bez**: dotaz na zařízení bez této hodnoty pro tuto vlastnost. Například z výsledků `OS` dotazu vyberte tuto možnost v buňce v řádku verze: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing IT**: spustí výchozí webový prohlížeč https://www.bing.com s touto hodnotou jako řetězec dotazu.  

   - Kliknutím na libovolný text s hypertextovými odkazy provedete zobrazení těchto konkrétních informací.  

   - V podokně výsledků se nezobrazuje více než 20 000 řádků. Upravte dotaz tak, aby se data dále vyfiltroval, nebo restartujte CMPivot na menší kolekci.  

7. Stavový řádek zobrazuje následující informace (zleva doprava):  

   - Stav aktuálního dotazu do cílové kolekce. Tento stav zahrnuje:  
     - Počet aktivních klientů, kteří dokončili dotaz (3)  
     - Počet klientů celkem (5)  
     - Počet offline klientů (2)  
     - Všichni klienti, kteří vrátili chybu (0)  

       Příklad: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - ID klientské operace. Příklad: `id(16780221)`  

   - Aktuální kolekce. Příklad: `PM_Team_Machines`  

   - Celkový počet řádků v podokně výsledků. Například `1 objects`.  



## <a name="example-scenarios"></a>Příklady scénářů

V následujících částech najdete příklady použití CMPivot ve vašem prostředí:


### <a name="example-1-stop-a-running-service"></a>Příklad 1: zastavení spuštěné služby

Správce zabezpečení vás vyzve, abyste službu prohledávání počítačů zastavili a zakázali co nejrychleji na všech zařízeních v účetním oddělení. Spustíte CMPivot na kolekci pro všechna zařízení v monitorování účtů a v entitě **služby** vyberete **dotaz na vše** . 

`Service`

Po zobrazení výsledků klikněte pravým tlačítkem na sloupec **název** a vyberte **Seskupit podle**. 

`Service | summarize dcount( Device ) by Name`

V řádku služby **prohlížeče** klikněte na číslo propojeného odkazu ve sloupci **dcount_** . 

`Service | where (Name == 'Browser') | summarize count() by Device`

Vyberete více zařízení, kliknete pravým tlačítkem myši na výběr a zvolíte **Spustit skript**. Tato akce spustí Průvodce spuštěním skriptu, ze kterého spustíte existující skript pro zastavení a zakázání služby. Díky CMPivot můžete rychle reagovat na incident zabezpečení všech aktivních počítačů a zobrazit výsledky v Průvodci spuštěním skriptu. Následně následně provedete vytváření standardních hodnot konfigurace pro opravu dalších počítačů v kolekci, které budou v budoucnu aktivní. 

![Příklad CMPivot pro službu Browser a spustit akci skriptu](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Příklad 2: proaktivně vyřešit selhání aplikace  

Pokud chcete být aktivní provozní údržbou, jednou týden, který spustíte CMPivot, na kolekci serverů, které spravujete, a v entitě **AppCrash** vyberte **Query All** . Kliknete pravým tlačítkem na sloupec **filename** a vyberete **Seřadit vzestupně**. Jedno zařízení vrátí sedm výsledků pro sqlsqm.exe s časovým razítkem 03:00 každý den. Vyberte název souboru v jednom z řádků, klikněte na něj pravým tlačítkem myši a vyberte **Bing**. Procházení výsledků hledání ve webovém prohlížeči: Další informace a řešení najdete v článku o podpoře společnosti Microsoft pro tento problém. 


### <a name="example-3-bios-version"></a>Příklad 3: verze systému BIOS

Jedním z požadavků je aktualizace systému BIOS, aby bylo možné [zmírnit spekulativní hrozby na straně prováděcího kanálu](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974). Začnete s dotazem na entitu **systému BIOS** . Potom můžete **Seskupit podle** vlastnosti **verze** . Pak klikněte pravým tlačítkem na konkrétní hodnotu, například "LENOVO-1140", a vyberte **Zobrazit zařízení pomocí**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Příklad 4: volné místo na disku

Je potřeba dočasně uložit velký soubor na síťový souborový server, ale nevíte, který z nich má dostatečnou kapacitu. Spusťte CMPivot na kolekci souborových serverů a Dotazujte entitu **disku** . Upravte dotaz pro CMPivot a rychle vraťte seznam aktivních serverů s daty úložiště v reálném čase:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot samostatná

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
## <a name="inside-cmpivot"></a>Uvnitř CMPivot

CMPivot odesílá dotazy klientům pomocí Configuration Manager "rychlý kanál". Tento komunikační kanál ze serveru na klienta se používá také jinými funkcemi, jako jsou například akce klientského oznamování, stav klienta a Endpoint Protection. Klienti vracejí výsledky prostřednictvím podobného systému zpráv rychlý stav. Stavové zprávy jsou dočasně uloženy v databázi nástroje. Další informace o portech používaných pro klientské oznámení najdete v článku o [portech](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP) .

Dotazy a výsledky jsou pouze text. Entity **InstallSoftware** a **zpracovávají** zpět některé z největších sad výsledků. Při testování výkonu je největší velikost souboru zprávy o stavu od jednoho klienta pro tyto dotazy menší než **1 KB**. Tento jednorázový dotaz by ve velkém prostředí s 50 000 aktivními klienty vygeneroval méně než 50 MB dat v síti. Všechny položky na uvítací stránce, které jsou podtržené, vrátí méně než 1 tisíc informací na klienta.

![Příklad CMPivot podtržených entit](media/cmpivot-underlined-entities.png)

Počínaje Configuration Manager 1810 se může CMPivot dotazovat data inventáře hardwaru, včetně rozšířených tříd inventáře hardwaru. Tyto nové entity (entity nepodtržené na úvodní stránce) mohou vracet mnohem větší datové sady v závislosti na tom, kolik dat je definováno pro danou vlastnost inventáře hardwaru. Například entita "InstalledExecutable" může vracet více MB dat pro každého klienta v závislosti na konkrétních datech, na která se dotazují. Při vracení větších sad dat inventáře hardwaru z větších kolekcí pomocí CMPivot se zaměříte na výkon a škálovatelnost vašich systémů.

Vyprší časový limit dotazu po jedné hodině. Například kolekce má 500 zařízení a 450 klientů je aktuálně online. Tato aktivní zařízení dostanou dotaz a vrátí výsledky téměř okamžitě. Pokud necháte okno CMPivot otevřené, protože ostatní klienti 50 přicházejí do režimu online, obdrží také dotaz a vrátí výsledky. 

## <a name="log-files"></a>Soubory protokolu

 Interakce CMPivot se zaznamenávají do následujících souborů protokolu:

**Na straně serveru:**
- SmsProv. log
- BgbServer. log
- StateSys. log

**Na straně klienta:**
- CcmNotificationAgent.log
- Skripty. log
- StateMessage.log

Další informace najdete v tématu [soubory protokolu](../../plan-design/hierarchy/log-files.md) a [řešení potíží s CMPivot](cmpivot-tsg.md).

## <a name="next-steps"></a>Další kroky

- [Změny CMPivot](cmpivot-changes.md)
- [Odstraňování potíží s CMPivotem](cmpivot-tsg.md)
- [Vytváření a spouštění powershellových skriptů](../../../apps/deploy-use/create-deploy-scripts.md)