---
title: Změny CMPivot
titleSuffix: Configuration Manager
description: Přečtěte si o změnách provedených v CMPivot mezi verzemi Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 32800284c415de6a36e856abf473bc6d8d729e6f
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608239"
---
# <a name="changes-to-cmpivot"></a>Změny CMPivot

Pomocí následujících informací se dozvíte o změnách provedených v [CMPivot](cmpivot.md) mezi verzemi Configuration Manager:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a> CMPivot změny verze 2006
<!--6518631-->

Počínaje verzí 2006 byly pro CMPivot provedeny následující vylepšení:

- [CMPivot samostatnou](cmpivot.md#bkmk_standalone) a CMPivot spuštěnou z konzoly pro správu. Když CMPivot spustíte z konzoly pro správu, používá stejnou základní technologii jako CMPivot Standalone k poskytnutí parity scénáře.

- Vylepšení navigace na klávesnici v CMPivot.

- CMPivot můžete spustit z jednotlivého zařízení nebo několika zařízení z uzlu zařízení, aniž byste museli vybrat kolekci zařízení. Toto vylepšení usnadňuje lidem, například osobám, které pracují jako helpdesk, k vytváření dotazů CMPivot pro konkrétní zařízení mimo předem vytvořenou kolekci.
   - Vyberte jednotlivá zařízení nebo zařízení s vícenásobným výběrem v kolekci zařízení nebo vyberte **Spustit CMPivot**.

- Po vrácení zařízení v zobrazení seznamu dotazů můžete na jednom nebo několika zařízeních vybrat možnost **Pivot** a dotazovat se na ta zařízení, abyste mohli dále prozkoumat. Tato změna umožňuje přejít k podrobnostem bez dotazování větší sady zařízení z původní kolekce. Kontingenční **zařízení** nahradilo **překlopení na**.
   - V existující operaci CMPivot vyberte jednotlivá zařízení nebo zařízení s vícenásobným výběrem z výstupu. Klikněte pravým tlačítkem a Pivot pomocí možnosti **pivotu zařízení** . Tato akce spustí samostatnou instanci CMPivot v oboru jenom pro zařízení, která jste vybrali. To usnadňuje pivotování a dotazování na požadovaná zařízení, aniž by bylo nutné pro ně vytvořit kolekci.

- Když pro jednotlivá zařízení spustíte CMPivot, název zařízení se zobrazí v horní části okna. U více zařízení je počet vybraných zařízení uvedený v horní části okna.
- Možnost **vytvořit kolekci** na kartě Souhrn dotazu byla odebrána, protože CMPivot již nevyžaduje dotazování na kolekci. Pomocí **pivotu zařízení** otevřete novou instanci CMPivot s rozsahem jenom pro zařízení, na která chcete dotazovat. **Vytvoření kolekce** je stále k dispozici v hlavní nabídce.

![Pivot zařízení pro více zařízení pomocí CMPivot](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a> CMPivot změny verze 2002
<!--5870934-->
Usnadnili jsme navigaci CMPivot entit. Od verze Configuration Manager 2002 můžete hledat entity CMPivot. Přidaly se také nové ikony, které usnadňují odlišení entit a typů objektů entit.

![Hledání entit CMPivot](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a> CMPivot změny verze 1910
<!--5410930, 3197353-->
Počínaje verzí 1910 se CMPivot významně optimalizuje za účelem snížení síťového provozu a zatížení vašich serverů. Kromě toho se pro pomoc při řešení potíží a lovu přidalo několik entit a vylepšení entit. Pro CMPivot ve verzi 1910 byly představeny tyto změny:

- [Optimalizace modulu CMPivot](#bkmk_optimization)
- Další entity a vylepšení entit:
  - Protokoly událostí systému Windows ([WinEvent](#bkmk_WinEvent))
  - Obsah souboru ([obsah](#bkmk_File)souboru)
  - Knihovny DLL načtené procesy ([ProcessModule](#bkmk_ProcessModule))
  - Informace o Azure Active Directory ([AADStatus](#bkmk_AadStatus))
  - Stav služby Endpoint Protection ([EPStatus](#bkmk_EPStatus))
- [Vyhodnocení dotazů na místní zařízení pomocí samostatného CMPivot](#bkmk_local-eval)
- [Další vylepšení pro CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> Optimalizace modulu CMPivot
<!--3197353-->
Pro snížení síťového provozu a zatížení serverů byl CMPivot optimalizovaný v 1910. Mnoho operací dotazů se teď provádí přímo na klientovi, nikoli na serverech. Tato změna také znamená, že některé operace CMPivot vracejí minimální data z prvního dotazu. Pokud se rozhodnete přejít na data a získat další informace, může se spustit nový dotaz, který načte další data z klienta. V případě, že jste spustili dotaz "souhrnně počítané", dříve byla na server vrácena například Velká sada dat.  I když vrátíte velkou datovou sadu, která nabízí okamžitý přechod k podrobnostem, kolikrát bylo potřeba jenom souhrnný počet. V 1910 Pokud se rozhodnete přejít na konkrétního klienta, dojde k další kolekci dat, která vrátí další požadovaná data. Tato změna přináší lepší výkon a škálovatelnost pro dotazy na velký počet klientů. <!--3197353, 5458337-->

#### <a name="examples"></a>Příklady

Optimalizace CMPivot významně omezují zatížení sítě a procesoru serveru potřebné ke spouštění dotazů CMPivot. S těmito optimalizacemi teď můžeme v reálném čase proprosévání za gigabajty dat klientů. Následující dotazy ilustrují tyto optimalizace:

- Vyhledá v protokolech událostí všechny klienty ve vašem podniku, aby nedošlo k selhání ověřování.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Vyhledá soubor pomocí algoritmu hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent ( \<logname> , [ \<timespan> ])

Tato entita se používá k získání událostí z protokolů událostí a souborů protokolu trasování událostí. Entita získává data z protokolů událostí generovaných technologií protokolu událostí systému Windows. Entita také získává události v protokolových souborech generovaných trasováním událostí pro Windows (ETW). WinEvent vyhledá události, ke kterým došlo během posledních 24 hodin, ve výchozím nastavení. Nicméně výchozí 24hodinový parametr lze přepsat zahrnutím TimeSpan.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> Obsah ( \<filename> )

Obsah souboru se používá k získání obsahu textového souboru.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule ( \<processname> )  

Tato entita se používá k vytvoření výčtu modulů (DLL) zavedených daným procesem. ProcessModule je užitečné při lovu malwaru, který se skrývá v legitimních procesech.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

Tato entita se dá použít k získání aktuálních Azure Active Directory informací o identitě ze zařízení.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus slouží k získání stavu antimalwarového softwaru nainstalovaného v počítači.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> Vyhodnocení dotazů na místní zařízení pomocí samostatného CMPivot
<!--3197353-->
Pokud používáte CMPivot mimo konzolu Configuration Manager, můžete dotazovat jenom na místní zařízení bez nutnosti infrastruktury Configuration Manager. Teď můžete využít CMPivot dotazy Azure Log Analytics k rychlému zobrazení informací o rozhraní WMI na místním zařízení. Tím se také umožní ověřování a vylepšení dotazů CMPivot před jejich spuštěním ve větším prostředí. CMPivot Standalone je k dispozici pouze v angličtině. Další informace o samostatném CMPivot naleznete v tématu [CMPivot Standalone](#bkmk_standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Známé problémy pro vyhodnocení dotazů na místní zařízení

 - Pokud se na **tomto počítači** budete dotazovat na entitu služby WMI, ke které nemáte přístup, jako je například zamčená třída WMI, může se zobrazit chyba v CMPivot. Spusťte CMPivot pomocí účtu se zvýšenými oprávněními pro dotazování těchto entit. <!--5753242-->
- Pokud na **tomto počítači**Vydáte dotaz na entity jiného typu než WMI, zobrazí se **neplatný obor názvů** nebo dvojznačná výjimka.
- Spusťte CMPivot Standalone z zástupce nabídky Start, nikoli přímo z cesty ke spustitelnému souboru. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> Další vylepšení

- Dotazy typu regulárních výrazů můžete provádět pomocí `like` operátoru new. Například:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- Hodnoty entit **CcmLog ()** a **EventLog ()** jsme aktualizovali tak, aby se ve výchozím nastavení v posledních 24 hodinách prohlížely jenom zprávy. Toto chování je možné přepsat předáním volitelného časového rozmezí. Například následující dotaz se bude pohlížet na události za poslední 1 hodinu:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- Entita **File ()** byla aktualizována, aby shromáždila informace o skrytých a systémových souborech a zahrnovala hodnotu hash MD5. I když hodnota hash MD5 není stejně přesný jako hodnota hash SHA256, ve většině bulletinů malwaru se jedná o běžně nahlášený hash.  

- Komentáře můžete přidávat v dotazech.<!-- 5431463 --> Toto chování je užitečné při sdílení dotazů. Například:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot se automaticky připojí k poslední lokalitě.<!-- 5420395 --> Po spuštění CMPivot se můžete v případě potřeby připojit k nové lokalitě.

- V nabídce **Export** vyberte možnost Nová pro **dotaz na odkaz na schránku**.<!-- 5431577 --> Tato akce zkopíruje odkaz na schránku, kterou můžete sdílet s ostatními. Například:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Tento odkaz otevře CMPivot Standalone s následujícím dotazem:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > Aby tento odkaz fungoval, [nainstalujte samostatnou CMPivot](#bkmk_standalone).

- Pokud je v případě, že je zařízení zaregistrované v programu Microsoft Defender Advanced Threat Protection (ATP), klikněte pravým tlačítkem na zařízení a spusťte online portál **Microsoft defender Security Center** .

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Známé problémy pro CMPivot ve verzi 1910

- Po dosažení limitu se nemůže zobrazit hlavička maximálního počtu výsledků. <!--5431427-->
  - Každý klient je omezený na 128 KB dat na jeden dotaz.
  - Výsledky mohou být zkráceny v případě, že výsledky dotazu překračují 128 KB.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a> CMPivot změny verze 1906

Počínaje verzí 1906 byly do CMPivot přidány následující položky:

- [Spojení, další operátory a agregátory](#bkmk_cmpivot_joins)
- [Přidání oprávnění CMPivot do role správce zabezpečení](#bkmk_cmpivot_secadmin1906)
- [CMPivot samostatná](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> Přidání spojení, dalších operátorů a agregátorů v CMPivot
<!--4054074-->
Nyní máte další aritmetické operátory, agregátory a možnost Přidat spojení dotazů, jako je například použití registru a souboru dohromady. Byly přidány následující položky:

#### <a name="table-operators"></a>Operátory tabulky

|Operátory tabulky| Popis|
|-----|-----|
| [zúčastnit](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Sloučí řádky dvou tabulek, aby bylo možné vytvořit novou tabulku odpovídajícím řádkem pro stejné zařízení.|
|činit|Vykreslí výsledky jako grafický výstup.|

Operátor vykreslení již v CMPivot existuje. Byla přidána podpora pro více řad a příkaz **with** . Další informace naleznete v části [Příklady](#bkmk_cmpivot_examples1906) a v článku [operátora spojení](https://docs.microsoft.com/azure/kusto/query/joinoperator) Kusto.

#### <a name="limitations-for-joins"></a>Omezení pro spojení

1. Sloupec JOIN je vždy implicitně proveden v poli **zařízení** .
1. Pro každý dotaz můžete použít maximálně 5 spojení.
1. Můžete použít maximálně 64 kombinovaných sloupců.

#### <a name="scalar-operators"></a>Skalární operátory

|Operátor| Popis|Příklad|
|-----|-----|-----|
| + | Přidat| `2 + 1, now() + 1d`|
| - |  Odčítání| `2 - 1, now() - 1d`|
| * | Násobení| `2 * 2`|
| / | Dělení | `2 / 1`|
| % | Modulo | `2 % 1`

#### <a name="aggregation-functions"></a>Agregační funkce

|Funkce| Popis|
|-----|-----|
| percentil ()| Vrátí odhad pro zadaný percentil nejbližšího pořadí populace, který je definován výrazem.|
| sumif() | Vrátí součet výrazu, pro který je predikát vyhodnocen jako true.|

#### <a name="scalar-functions"></a>Skalární funkce

|Funkce| Popis|
|-----|-----|
| case()| Vyhodnotí seznam predikátů a vrátí první výsledek výrazu, jehož predikát je splněn. |
| Pokud () | Vyhodnotí první argument a vrátí hodnotu buď druhého nebo třetího argumentu v závislosti na tom, zda se predikát vyhodnotil jako true (second) nebo false (třetí).|
 | indexof() | Funkce hlásí index s nulovým základem prvního výskytu zadaného řetězce ve vstupním řetězci.|
| strcat() | Zřetězí mezi 1 a 64 argumenty. |
| strlen()| Vrátí délku vstupního řetězce ve znacích.|
| substring() | Extrahuje podřetězec ze zdrojového řetězce počínaje z nějakého indexu na konec řetězce. |
| tostring() | Převede vstup na operaci řetězce. |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> 4.6

- Zobrazit zařízení, výrobce, model a OSVersion:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Zobrazit graf spouštěcích časů pro zařízení:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Skládaný pruhový graf zobrazující časy spouštění zařízení v MS](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> Přidání oprávnění CMPivot do role správce zabezpečení
<!--4683130-->

Počínaje verzí 1906 byla do předdefinované role **Správce zabezpečení** Configuration Manager přidána následující oprávnění:

 - **Číst** ve skriptu SMS
 - **Spustit CMPivot** pro kolekci
 - **Číst** sestavu inventáře

>[!NOTE]
> **Spouštění skriptů** je nadmnožinou oprávnění **Run CMPivot** .

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot samostatná

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a> CMPivot změny verze 1902
<!--3610960-->
Od verze Configuration Manager 1902 můžete spustit CMPivot z lokality centrální správy (CAS) v hierarchii. Primární lokalita stále zpracovává komunikaci s klientem. Při spuštění CMPivot z lokality centrální správy komunikuje s primární lokalitou prostřednictvím vysokorychlostního kanálu pro odběr zpráv. Tato komunikace nespoléhá na standardní replikaci SQL mezi lokalitami.

Spuštění CMPivot na CAS bude vyžadovat další oprávnění, pokud SQL nebo poskytovatel není ve stejném počítači nebo v případě konfigurace služby SQL Always On. U těchto vzdálených konfigurací máte scénář dvojího směrování pro CMPivot.

Pokud chcete, aby CMPivot pracoval na certifikačních autoritách v takovém scénáři dvojího směrování, můžete definovat omezené delegování. Chcete-li pochopit důsledky zabezpečení této konfigurace, přečtěte si článek [omezeného delegování protokolu Kerberos](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) . Protokol Kerberos musí spolupracovat se všemi segmenty směrování mezi počítači.<!--5746133--> Pokud máte více než jednu vzdálenou konfiguraci, jako je například SQL nebo poskytovatel služby SMS, který se nachází společně s certifikačními autoritami nebo ne nebo více důvěryhodnými doménovými strukturami, můžete vyžadovat kombinaci nastavení oprávnění. Níže jsou uvedené kroky, které možná budete muset provést:

### <a name="cas-has-a-remote-sql-server"></a>CAS mají vzdálený SQL Server.

1. Přejít na server SQL primární lokality.
   1. Přidejte vzdálený SQL Server CAS a server lokality CAS do skupiny [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) .
   ![Configmgr_DviewAccess skupiny na SQL serveru primární lokality](media/cmpivot-dviewaccess-group.png)
1. Přejít na uživatelé a počítače služby Active Directory.
   1. Pro každý server primární lokality klikněte pravým tlačítkem a vyberte **vlastnosti**.
      1. Na kartě delegování vyberte třetí možnost **Důvěřovat tomuto počítači pro delegování pouze určeným službám**. 
      1. Vyberte možnost **použít pouze protokol Kerberos**.
      1. Přidejte službu SQL Server CAS s portem a instancí.
      1. Ujistěte se, že tyto změny odpovídají zásadám zabezpečení vaší společnosti!
   1. Pro lokalitu CAS klikněte pravým tlačítkem a vyberte **vlastnosti**.
      1. Na kartě delegování vyberte třetí možnost **Důvěřovat tomuto počítači pro delegování pouze určeným službám**. 
      1. Vyberte možnost **použít pouze protokol Kerberos**.
      1. Přidejte službu SQL Server pro každou primární lokalitu s portem a instancí.
      1. Ujistěte se, že tyto změny odpovídají zásadám zabezpečení vaší společnosti!

   ![Příklad delegování CMPivot AD pro dvojité segmenty směrování](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS mají vzdáleného zprostředkovatele.

1. Přejít na server SQL primární lokality.
   1. Přidejte účet počítače poskytovatele CAS a server lokality CAS do skupiny [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) .
1. Přejít na uživatelé a počítače služby Active Directory.
   1. Vyberte počítač poskytovatele CAS, klikněte na něj pravým tlačítkem a vyberte **vlastnosti**.
      1. Na kartě delegování vyberte třetí možnost **Důvěřovat tomuto počítači pro delegování pouze určeným službám**. 
      1. Vyberte možnost **použít pouze protokol Kerberos**.
      1. Přidejte službu SQL Server pro každou primární lokalitu s portem a instancí.
      1. Ujistěte se, že tyto změny odpovídají zásadám zabezpečení vaší společnosti!
   1. Vyberte server lokality CAS, klikněte pravým tlačítkem a vyberte **vlastnosti**.
      1. Na kartě delegování vyberte třetí možnost **Důvěřovat tomuto počítači pro delegování pouze určeným službám**. 
      1. Vyberte možnost **použít pouze protokol Kerberos**.
      1. Přidejte službu SQL Server pro každou primární lokalitu s portem a instancí.
      1. Ujistěte se, že tyto změny odpovídají zásadám zabezpečení vaší společnosti!
1. Restartujte počítač se vzdáleným poskytovatelem CAS.

### <a name="sql-always-on"></a>SQL Always On

1. Přejít na server SQL primární lokality.
   1. Přidejte server lokality CAS do skupiny [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) .
1. Přejít na uživatelé a počítače služby Active Directory.
   1. Pro každý server primární lokality klikněte pravým tlačítkem a vyberte **vlastnosti**.
      1. Na kartě delegování vyberte třetí možnost **Důvěřovat tomuto počítači pro delegování pouze určeným službám**. 
      1. Vyberte možnost **použít pouze protokol Kerberos**.
      1. Přidejte účty služby SQL Server CAS pro uzly SQL s portem a instancí.
      1. Ujistěte se, že tyto změny odpovídají zásadám zabezpečení vaší společnosti!
   1. Vyberte server lokality CAS, klikněte pravým tlačítkem a vyberte **vlastnosti**.
      1. Na kartě delegování vyberte třetí možnost **Důvěřovat tomuto počítači pro delegování pouze určeným službám**. 
      1. Vyberte možnost **použít pouze protokol Kerberos**.
      1. Přidejte službu SQL Server pro každou primární lokalitu s portem a instancí.
      1. Ujistěte se, že tyto změny odpovídají zásadám zabezpečení vaší společnosti!
1. Ujistěte se, že [je Hlavní](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover#SPNs) název služby (SPN) publikovaný pro název NASLOUCHACÍHO procesu SQL CAS a každý primární název NASLOUCHACÍHO procesu SQL.
1. Restartujte primární SQL Server.
1. Restartujte server lokality CAS a servery SQL CAS.


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a> CMPivot změny verze 1810
<!--1359068, 3607759-->

CMPivot zahrnuje následující vylepšení od Configuration Manager verze 1810:

- [Nástroj CMPivot a výkon](#bkmk_cmpivot-perf)
- [Skalární funkce](#bkmk_cmpivot-functions)  
- [Vykreslování vizualizací](#bkmk_cmpivot-charts)  
- [Inventář hardwaru](#bkmk_cmpivot-hinv)  
- [Skalární operátory](#bkmk_cmpivot-operators)  
- [Souhrn dotazů](#bkmk_cmpivot-summary)  
- [Auditní stavové zprávy](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> Nástroj CMPivot a výkon

- CMPivot bude vracet až 100 000 buněk, ale ne 20 000 řádků.
  - Pokud má entita 5 vlastností, což znamená 5 sloupců, zobrazí se až 20 000 řádků.
  - Pro entitu s 10 vlastnostmi se zobrazí až 10 000 řádků.
  - Celkový počet zobrazených dat bude menší nebo roven 100 000 buňkám.
- Na kartě Souhrn dotazu vyberte počet neúspěšných nebo offline zařízení a pak vyberte možnost **Vytvoření kolekce**. Tato možnost usnadňuje zacílení těchto zařízení na nápravné nasazení.
   - Tato možnost byla odebrána ve verzi 2006, protože CMPivot již nevyžaduje dotazování na kolekci.
- Uložte **Oblíbené** dotazy kliknutím na ikonu složky.
   ![Příklad uložení oblíbeného dotazu v CMPivot](media/cmpivot-favorite.png)

- Klienti aktualizace na verzi 1810 vrátí výstup na tento web méně než 80 KB přes rychlý komunikační kanál.
  - Tato změna zvyšuje výkon zobrazení výstupu skriptu nebo dotazu.
  - Pokud je výstup skriptu nebo dotazu větší než 80 KB, klient odesílá data prostřednictvím stavové zprávy.
  - Pokud klient není aktualizován na verzi klienta 1810, bude nadále používat stavové zprávy.

- Při spuštění CMPivot se může zobrazit následující chyba:  **CMPivot teď nejde použít v důsledku nekompatibilní verze skriptu. K tomuto problému může dojít proto, že se hierarchie právě provádí při upgradu lokality. Počkejte, než se upgrade dokončí, a pak to zkuste znovu.**

  - Pokud se zobrazí tato zpráva, může to znamenat:
    - Obor zabezpečení není správně nastavený.
    - V průběhu upgradu došlo k problémům.
    - Podkladový skript CMPivot je nekompatibilní.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> Skalární funkce
CMPivot podporuje následující skalární funkce:
- **před ()**: odečte zadaný časový rozsah TimeSpan od aktuálního času UTC.  
- **datetime_diff ()**: vypočítá rozdíl kalendáře mezi dvěma hodnotami DateTime  
- **Now ()**: vrátí aktuální čas času UTC.  
- **bin ()**: zaokrouhlí hodnoty dolů na celočíselný násobek dané velikosti přihrádky.  

> [!Note]  
> Datový typ DateTime představuje okamžitý čas, obvykle vyjádřený jako datum a denní dobu. Hodnoty času se měří v jednotkách s 1 sekundou. Hodnota DateTime je vždy v časovém pásmu UTC. Ve formátu ISO 8601 vždy vyjadřují literály data a času, například `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Příklady
- `datetime(2015-12-31 23:59:59.9)`: Určitý literál data A času   
- `now()`: Aktuální čas  
- `ago(1d)`: Aktuální čas minus jeden den  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> Vykreslování vizualizací

CMPivot nyní obsahuje základní podporu pro [operátor vykreslování](https://docs.microsoft.com/azure/kusto/query/renderoperator)KQL. Tato podpora zahrnuje následující typy:  
- **BarChart**: první sloupec má osu x a může to být text, DateTime nebo numeric. Druhý sloupec musí být numerický a zobrazený jako vodorovný pruh.  
- **columnchart**: like BarChart, se svislými pásy místo horizontálních pruhů.  
- **piechart**: první sloupec má barevnou osu, druhý sloupec je numerický.  
- **timechart**: spojnicový graf. První sloupec je osy x a měl by být typu DateTime. Druhý sloupec je osa y.  

#### <a name="example-bar-chart"></a>Příklad: pruhový graf
Následující dotaz vykresluje naposledy použité aplikace jako pruhový graf:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Příklad vizualizace pruhového grafu CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Příklad: časový graf
Pro vykreslení časových grafů použijte operátor New **bin ()** k seskupení událostí v čase. Následující dotaz ukazuje, kdy zařízení začala za posledních sedm dní:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Příklad vizualizace grafu CMPivot Time](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Příklad: výsečový graf
Následující dotaz zobrazí všechny verze operačního systému ve výsečovém grafu:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Příklad vizualizace výsečového grafu CMPivot](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> Inventář hardwaru
Použijte CMPivot k dotazování libovolné třídy inventáře hardwaru. Tyto třídy zahrnují všechna vlastní rozšíření, která provedete v inventáři hardwaru. CMPivot okamžitě vrátí výsledky uložené v mezipaměti z poslední kontroly inventáře hardwaru uložené v databázi lokality. Ve stejnou dobu aktualizuje výsledky v případě potřeby s živými daty z libovolného online klienta.

Sytost barev dat v tabulce výsledků nebo grafu označuje, zda jsou data uložena v reálném čase nebo v mezipaměti. Například tmavě modrá je data v reálném čase z online klienta. Světle modrá je data uložená v mezipaměti.

#### <a name="example"></a>Příklad

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Příklad dotazu inventáře CMPivot se vizualizací sloupcového grafu](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Omezení
- Následující entity inventáře hardwaru nejsou podporované:  
    - Vlastnosti pole, například IP adresa  
    - Real32/Real64 <!--example?-->  
    - Vlastnosti vloženého objektu <!--example?-->  
- Názvy entit inventáře musí začínat znakem.
- Předdefinované entity nemůžete přepsat vytvořením entity inventáře se stejným názvem.  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> Skalární operátory
CMPivot zahrnuje následující skalární operátory:  

> [!Note]  
> - LHS: řetězec nalevo od operátoru  
> - ZAROVNÁNÍ INDIREKCE RHS: řetězec napravo od operátoru  


|Operátor|Popis|Příklad (výnosů true)|
|--------|-----------|---------------------|
|==|Je rovno|`"aBc" == "aBc"`|
|!=|Nerovná se|`"abc" != "ABC"`|
|jako|LHS obsahuje shodu pro zarovnání INDIREKCE rhs.|`"FabriKam" like "%Brik%"`|
|! Like|LHS neobsahuje shodu pro zarovnání INDIREKCE rhs.|`"Fabrikam" !like "%xyz%"`|
|obsahuje|ZAROVNÁNÍ INDIREKCE RHS se vyskytuje jako dílčí sekvence LHS.|`"FabriKam" contains "BRik"`|
|! obsahuje|ZAROVNÁNÍ INDIREKCE RHS se nevyskytuje v LHS.|`"Fabrikam" !contains "xyz"`|
|StartsWith|ZAROVNÁNÍ INDIREKCE RHS je počáteční dílčí sekvence LHS.|`"Fabrikam" startswith "fab"`|
|! StartsWith|ZAROVNÁNÍ INDIREKCE RHS není počáteční dílčí sekvence LHS.|`"Fabrikam" !startswith "kam"`|
|EndsWith|ZAROVNÁNÍ INDIREKCE RHS je uzavírací podsekvence LHS|`"Fabrikam" endswith "Kam"`|
|! EndsWith|ZAROVNÁNÍ INDIREKCE RHS není uzavírací podsekvence LHS.|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> Souhrn dotazů

V dolní části okna CMPivot vyberte kartu **Souhrn dotazu** . Tento stav vám pomůže identifikovat klienty, kteří jsou offline, nebo řešit chyby, ke kterým může dojít. Výběrem hodnoty ve sloupci počet otevřete seznam konkrétních zařízení s tímto stavem. 

Vyberte například počet zařízení se stavem selhání. Podívejte se na konkrétní chybovou zprávu a exportujte seznam těchto zařízení. Pokud se jedná o chybu, kterou konkrétní rutina nerozpozná, vytvořte kolekci ze seznamu exportovaných zařízení a nasaďte aktualizaci Windows PowerShellu.  

### <a name="cmpivot-audit-status-messages"></a>CMPivot auditní stavové zprávy

Když ve verzi 1810 spustíte CMPivot, vytvoří se zpráva o stavu auditu s parametrem **MessageID 40805**. Stavové zprávy můžete zobrazit tak, že kliknete na **monitorování**stav  >  **systému**  >  **dotazy stavových**zpráv. Můžete spustit **všechny auditní stavové zprávy pro konkrétního uživatele**, **všechny auditní stavové zprávy pro určitou lokalitu**nebo vytvořit vlastní dotaz na stavovou zprávu.

Pro zprávu se používá následující formát:

MessageId 40805: uživatelské &lt; jméno> spuštění skriptu skriptu &lt; – identifikátor GUID> s algoritmem hash &lt; -hash> na kolekci kolekcí &lt; -ID>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 je identifikátor GUID skriptu pro CMPivot.
- Hodnota hash skriptu se dá zobrazit v souboru Scripts. log klienta.
- Můžete také zobrazit hodnotu hash uloženou v úložišti skriptů klienta. Název souboru na klientovi je &lt; Script-Guid>_ &lt; Script-hash>.
    - Příklad názvu souboru: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![Ukázka stavové zprávy CMPivot audit](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Další kroky
 
[Odstraňování potíží s CMPivotem](cmpivot-tsg.md)
