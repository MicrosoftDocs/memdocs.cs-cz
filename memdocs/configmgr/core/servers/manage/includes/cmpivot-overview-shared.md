---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 80302a1c369c36a08cc1a55e20cf339dbc8d2883
ms.sourcegitcommit: 6d987bb69d0eb9955a3003202864f58d6aaa426a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381040"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Dotazy

Dotazy se dají použít k vyhledávání podmínek, identifikaci trendů, analýze vzorů a poskytování mnoha dalších přehledů na základě vašich dat. CMPivot používá podmnožinu modelu toku dat služby [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query) pro příkaz tabelárního výrazu. Typickou strukturou příkazu tabulkového výrazu je složení klientských entit a tabulkových datových operátorů (například filtry a projekce). Složení je reprezentované znakem svislé čáry (|), který poskytuje příkaz jako pravidelný tvar, který vizuálně představuje tok tabulkových dat zleva doprava. Každý operátor přijme tabulkovou datovou sadu "z kanálu" a další vstupy (včetně jiných tabulkových datových sad) od těla operátoru a poté vygeneruje tabulkovou datovou sadu pro další operátor, který následuje:`entity | operator1 | operator2 | ...`

V následujícím příkladu je entita `CCMRecentlyUsedApplications` (odkaz na naposledy použité aplikace) a operátor, kde (který odfiltruje záznamy z jeho vstupu na základě některého predikátu pro záznam):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Entity

Entity jsou objekty, na které se dá dotázat z klienta. V současné době podporujeme následující entity:


|Entita|Description|
|---|---|
|AadStatus|Stav Azure Active Directory|
|Administrators|Členové místní skupiny Administrators|
|AppCrash|Poslední zprávy o chybách aplikací|
|AppVClientApplication|Klientská aplikace AppV|
|AppVClientPackage|Klientský balíček AppV|
|AutoStartSoftware|Software, který se spouští automaticky s operačním systémem nebo hned po něm|
|Základní|Základní|
|Baterie|Baterie|
|Systému BIOS|Informace o systému BIOS|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|Podrobnosti šifrování BitLockeru|
|BitLockerPolicy|Zásada BitLockeru|
|BootConfiguration|Konfigurace spouštění|
|BrowserHelperObject|Objekt pomocníka prohlížeče|
|BrowserUsage|Použití prohlížeče|
|CcmLog()|Řádky do 24 hodin (ve výchozím nastavení) ze souboru protokolu ccm|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Nedávno použité aplikace|
|CCMWebAppInstallInfo|Webové aplikace|
|JEDNOTKA|Jednotka CD|
|ClientEvents|Události klienta|
|ComputerSystem|Systém počítače|
|ComputerSystemEx|Počítačový systém ex|
|ComputerSystemProduct|Produkt počítačového systému|
|ConnectedDevice|Připojené zařízení|
|Připojení|Aktivní připojení TCP v zařízení nebo mimo něj|
|Aplikace klasické pracovní plochy|Aplikace klasické pracovní plochy|
|DesktopMonitor|Stolní monitor|
|Zařízení|Základní informace o zařízení|
|Disk|Informace o místním úložném zařízení v systému počítače se systémem Windows|
|DMA|DMA|
|DMAChannel|Kanál DMA|
|DriverVxD|Ovladač-VxD|
|EmbeddedDeviceInformation|Informace o integrovaném zařízení|
|Prostředí|Prostředí|
|EPStatus|Stav antimalwarového softwaru v počítači|
|EventLog ()|Události do 24 hodin (ve výchozím nastavení) z protokolu událostí|
|Soubor ()|Informace o konkrétním souboru|
|Sdílená složka|Informace o aktivních sdílených souborech|
|Firmware|Firmware|
|IDEController|Kontroler IDE|
|InstalledExecutable|Instalovaný spustitelný soubor|
|InstalledSoftware|Aplikace nainstalovaná na zařízení|
|Příkazu|Získá konfiguraci sítě, včetně použitelných rozhraní, IP adres a serverů DNS.|
|IRQTable|Tabulka IRQ|
|Klávesnice|Klávesnice|
|LoadOrderGroup|Skupina pořadí načtení|
|Logický disk|Logický disk|
|MDMDevDetail|Informace o zařízení|
|Memory (Paměť)|Memory (Paměť)|
|Údajů|Údajů|
|Základní desky|Základní desky|
|Síťový adaptér|Síťový adaptér|
|NetworkAdapterConfiguration|Konfigurace síťového adaptéru|
|NetworkClient|Síťový klient|
|NetworkLoginProfile|Profil přihlášení k síti|
|NTEventlogFile|Soubor protokolu událostí NT|
|Office365ProPlusConfigurations|Konfigurace Office 365 ProPlus|
|OfficeAddin|Doplňky Office|
|OfficeClientMetric|Metrika klienta Office|
|OfficeDeviceSummary|Souhrn zařízení Office|
|OfficeDocumentMetric|Metriky dokumentů Office|
|OfficeDocumentSolution|Řešení dokumentu Office|
|OfficeMacroError|Chyba makra Office|
|OfficeProductInfo|Informace o produktu Office|
|OfficeVbaRuleViolation|Porušení pravidel Office VBA|
|OfficeVbaSummary|Shrnutí vyhledávání pro Office VBA|
|OperatingSystem|Operační systém|
|OperatingSystemEx|Operační systém ex|
|OperatingSystemRecoveryConfiguration|Konfigurace obnovení operačního systému|
|OptionalFeature|Volitelná funkce|
|Operační systém|Základní informace o operačním systému|
|PageFileSetting|Nastavení stránkovacího souboru|
|ParallelPort|Paralelní port|
|Oddíl|Diskové oddíly|
|PCMCIAController|Řadič PCMCIA|
|PhysicalDisk|PhysicalDisk|
|PhysicalMemory|Fyzická paměť|
|PNPDEVICEDRIVER|Ovladač zařízení PNP|
|PointingDevice|Polohovací zařízení|
|PortableBattery|Přenosná baterie|
|Porty|Porty|
|PowerCapabilities|Možnosti napájení|
|PowerClientOptOutSettings|Nastavení vyloučení řízení spotřeby|
|PowerConfigurations|Konfigurace napájení|
|PowerManagementDaily|Každodenní data řízení spotřeby|
|PowerManagementInsomniaReasons|Důvody napájení režimu spánku|
|PowerManagementMonthly|Měsíční data řízení spotřeby|
|PowerSettings|Nastavení napájení|
|PrinterConfiguration|Konfigurace tiskárny|
|PrinterDevice|Zařízení tiskárny|
|PrintJobs|Tiskové úlohy|
|Proces|Proces v operačním systému|
|ProcessModule()|Moduly načtené zadanými procesy|
|Procesor|Procesor|
|ProtectedVolumeInformation|Informace o chráněném svazku|
|Protokol|Protokol|
|QuickFixEngineering|Technik rychlé opravy|
|SCSIController|Řadič SCSI|
|SerialPortConfiguration|Konfigurace sériového portu|
|SerialPorts|Sériové porty|
|ServerFeature|Serverová součást|
|Služba|Služba na počítačovém systému s Windows|
|Služby|Služby|
|Sdílené složky|Sdílené složky|
|SMBConfig|Konfigurace protokolu SMB zařízení|
|SMSAdvancedClientPorts|Porty klienta Configuration Manager|
|SMSAdvancedClientSSLConfigurations|Configuration Manager konfigurace protokolu SSL klienta|
|SMSAdvancedClientState|Configuration Manager stav klienta|
|SMSDefaultBrowser|Výchozí prohlížeč|
|SMSSoftwareTag|Softwarová značka|
|SMSWindows8Application|Aplikace pro Windows|
|SMSWindows8ApplicationUserInfo|Informace o uživateli aplikace pro Windows|
|SoftwareShortcut|Zástupce softwaru|
|SoftwareUpdate|K dispozici je aktualizace softwaru, ale není na zařízení nainstalována.|
|SoundDevices|Zvuková zařízení|
|SWLicensingProduct|Produkt pro licencování softwaru|
|SWLicensingService|Služba licencování softwaru|
|SystemAccount|Systémový účet|
|SystemBootData|Systémová data spuštění|
|SystemBootSummary|Souhrn spuštění systému|
|SystemConsoleUsage|Využití systémové konzoly|
|SystemConsoleUser|Uživatel konzoly systému|
|SystemDevices|Systémová zařízení|
|SystemDrivers|Systémové ovladače|
|SystemEnclosure|Skříň systému|
|TapeDrive|Pásková jednotka|
|TimeZone|Časové pásmo|
|TPM|TPM|
|TPMStatus|Stav čipu TPM|
|TSIssuedLicense|Licence vydané TS|
|TSLicenseKeyPack|Balík klíčů TS License Key|
|UninterruptiblePowerSupply|Nepřerušitelný zdroj napájení|
|USBController|Řadič USB|
|USBDevice|Zařízení USB|
|Uživatel|Uživatelský účet s aktivním připojením k zařízení|
|USMFolderRedirectionHealth|Stav přesměrování složky|
|USMUserProfile|Stav uživatelského profilu|
|VideoController|Grafický adaptér|
|VirtualMachine|Virtuální počítač|
|VirtualMachine64|Virtuální počítač (64)|
|Svazek|Svazek|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Verze agenta web Windows Update|
|WinEvent ()|Události do 24 hodin (ve výchozím nastavení) z protokolu událostí systému Windows|
|WriteFilterState|Stav filtru zápisu|

## <a name="table-operators"></a>Operátory tabulky

Operátory tabulky lze použít k filtrování, sumarizaci a transformaci datových proudů. V současné době jsou podporovány následující operátory:

|Operátory tabulky|Description|
|---|---|
|count|Vrátí tabulku s jedním záznamem, který obsahuje počet záznamů.|
|distinct|Vytvoří tabulku s jedinečnou kombinací zadaných sloupců vstupní tabulky.|
|join|Sloučí řádky dvou tabulek, aby bylo možné vytvořit novou tabulku odpovídajícím řádkem pro stejné zařízení.|
|Řadit podle|Seřadit řádky vstupní tabulky do pořadí podle jednoho nebo více sloupců|
|projekt|Vyberte sloupce, které se mají zahrnout, přejmenovat nebo vyřadit a vložit nové počítané sloupce.|
|Souhrn|Vytvoří tabulku, která agreguje obsah vstupní tabulky.|
|take|Vrátit se k zadanému počtu řádků|
|top|Vrátí prvních N záznamů seřazených podle zadaných sloupců.|
|where|Filtruje tabulku na podmnožinu řádků, které odpovídají predikátu.|

## <a name="scalar-operators"></a>Skalární operátory

Následující tabulka shrnuje operátory:

|Operátory|Popis|Příklad
|---|---|---|
|==|Je rovno|`1 == 1, 'aBc' == 'AbC'`|
|!=|Není rovno|`1 != 2, 'abc' != 'abcd'`|
|< |Tolik|`1 < 2, 'abc' < 'DEF'`|
|> |Zvýšen|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Menší nebo rovno|`1 <= 2, 'abc' <= 'abc'`|
|>=|Větší nebo rovno|`2 >= 1, 'abc' >= 'ABC'`|
|+|Přidat|`2 + 1, now() + 1d`|
|-|Odčítání|`2 - 1, now() - 1h`|
|*|Násobení|`2 * 2`|
|/|Dělení|`2 / 1`|
|%|Modulo|`2 % 1`|
|jako|Levá strana (LHS) obsahuje shodu pro pravou stranu (zarovnání INDIREKCE RHS)|`'abc' like '%B%'`|
|! Like|LHS neobsahuje shodu pro zarovnání INDIREKCE rhs.|`'abc' !like '_d_'`|
|obsahuje|ZAROVNÁNÍ INDIREKCE RHS se vyskytuje jako dílčí sekvence LHS.|`'abc' contains 'b'`|
|! obsahuje|ZAROVNÁNÍ INDIREKCE RHS se nevyskytuje v LHS.|`'team' !contains 'i'`|
|StartsWith|ZAROVNÁNÍ INDIREKCE RHS je počáteční dílčí sekvence LHS.|`'team' startswith 'tea'`|
|! StartsWith|ZAROVNÁNÍ INDIREKCE RHS není počáteční dílčí sekvence LHS.|`'abc' !startswith 'bc'`|
|EndsWith|ZAROVNÁNÍ INDIREKCE RHS je uzavírací podsekvence LHS|`'abc' endswith 'bc'`|
|! EndsWith|ZAROVNÁNÍ INDIREKCE RHS není uzavírací podsekvence LHS.|`'abc' !endswith 'a'`|
|a|True pouze v případě, že zarovnání INDIREKCE RHS a LHS mají hodnotu true|`(1 == 1) and (2 == 2)`|
|nebo|True pouze v případě, že je true zarovnání INDIREKCE RHS nebo LHS|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Agregační funkce

Agregační funkce lze použít s operátorem tabulky Shrnutí pro vypočtené shrnuté hodnoty. V současné době jsou podporovány následující agregační funkce:

|Funkce|Popis|
|---|---|
|avg()|Vrátí průměr hodnot napříč skupinou.|
|count()|Vrátí počet záznamů na skupinu Shrnutí.|
|countif()|Vrátí počet řádků, pro který je predikát vyhodnocen jako true.|
|dcount()|Vrátí počet jedinečných hodnot ve skupině.|
|max()|Vrátí maximální hodnotu napříč skupinou.|
|min()|Vrátí minimální hodnotu v rámci skupiny.|
|percentil ()|Vrátí odhad pro zadaný percentil nejbližšího pořadí populace, který je definován výrazem.|
|sum()|Vrátí součet hodnot napříč skupinou.|
|sumif()|Vrátí součet výrazu, pro který je predikát vyhodnocen jako true.|

## <a name="scalar-functions"></a>Skalární funkce

Skalární funkce lze použít ve výrazech. V současné době jsou podporovány následující skalární funkce:

|Funkce|Popis|
|---|---|
|ago()|Odečte zadané časové rozmezí od aktuálního času UTC.|
|bin()|Zaokrouhlí hodnoty dolů na počet násobků DateTime z dané velikosti přihrádky.|
|case()|Vyhodnotí seznam predikátů a vrátí první výsledek výrazu, jehož predikát je splněn.|
|datetime_add()|Vypočítá nový typ DateTime ze zadané hodnoty DatePart vynásobený zadanou velikostí, která se přidala k zadané hodnotě DateTime.|
|datetime_diff()|Vypočítá rozdíl mezi dvěma hodnotami data a času.|
|iif()|Vyhodnotí první argument a vrátí hodnotu buď druhého nebo třetího argumentu v závislosti na tom, zda se predikát vyhodnotil jako true (second) nebo false (třetí).|
|indexof()|Funkce hlásí index s nulovým základem prvního výskytu zadaného řetězce ve vstupním řetězci.|
|isnotnull()|Vyhodnotí svůj jediný argument a vrátí hodnotu typu Boolean, která označuje, jestli se argument vyhodnocuje na hodnotu, která není null.|
|isnull()|Vyhodnotí svůj jediný argument a vrátí hodnotu typu Boolean, která označuje, jestli se argument vyhodnocuje na hodnotu null.|
|now()|Vrátí aktuální čas času UTC.|
|strcat()|Zřetězí mezi 1 a 64 argumenty.|
|strlen()|Vrátí délku vstupního řetězce ve znacích.|
|substring()|Extrahuje podřetězec ze zdrojového řetězce počínaje z nějakého indexu na konec řetězce.|
|tostring()|Převede vstup na řetězcovou reprezentaci.|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a>Další entity, operátory a funkce pro CMPivot z Configuration Manager

> [!Important]
> Když spouštíte CMPivot z centra pro správu Microsoft Endpoint Manageru, tyto položky se nepodporují.

|Typ|Položka|Description|
|--|--|---|
|Entita|AccountSID|Account SID (identifikátor zabezpečení účtu)|
|Entita|Obsah ()|Obsah konkrétního souboru|
|Entita|NAPClient|Klient NAP|
|Entita|NAPSystemHealthAgent|Agent stavu systému NAP|
|Entita|Registr ()|Všechny hodnoty pro určitý klíč registru<!--7371183-->|
|Operátor tabulky|činit|Vykreslí výsledky jako grafický výstup.|
