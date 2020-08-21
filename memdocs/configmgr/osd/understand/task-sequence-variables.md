---
title: Reference k proměnným pořadí úkolů
titleSuffix: Configuration Manager
description: Přečtěte si o proměnných pro řízení a přizpůsobení Configuration Manager sekvence úloh.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86a19970b58747d83ae8823eb8e2a85c40c03c4d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697343"
---
# <a name="task-sequence-variables"></a>Proměnné pořadí úkolů

*Platí pro: Configuration Manager (Current Branch)*

Tento článek je odkazem na všechny dostupné proměnné v abecedním pořadí. Konkrétní proměnnou můžete najít pomocí funkce **Najít** v prohlížeči (obvykle **CTRL**  +  **F**). Proměnná poznámky, pokud je specifická pro konkrétní krok. Článek o [krocích pořadí úkolů](task-sequence-steps.md) zahrnuje seznam proměnných specifických pro jednotlivé kroky.

Další informace najdete v tématu [Použití proměnných pořadí úkolů](using-task-sequence-variables.md).

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a> Odkaz na proměnnou pořadí úloh

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

Pořadí úkolů vyhledá předchozí instalaci operačního systému při spuštění prostředí Windows PE na pevných discích počítače. Umístění složky Windows je uložené v této proměnné. Můžete nakonfigurovat pořadí úkolů, aby načetlo tuto hodnotu z prostředí a použilo ji k určení stejného umístění složky Windows pro novou instalaci operačního systému.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

Pořadí úkolů vyhledá předchozí instalaci operačního systému při spuštění prostředí Windows PE na pevných discích počítače. V této proměnné je uloženo umístění pevného disku, kde je nainstalován operační systém. Můžete nakonfigurovat pořadí úkolů, aby načetlo tuto hodnotu z prostředí a použilo ji k určení stejného umístění pevného disku pro nový operační systém.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Platí pro krok [zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState) .*

(vstup)

Určuje ID balíčku Configuration Manager balíčku, který obsahuje soubory nástroje USMT. Tato proměnná je povinná.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Platí pro krok [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState) .*

(vstup)

Určuje ID balíčku Configuration Manager balíčku, který obsahuje soubory nástroje USMT. Tato proměnná je povinná.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Ukládá jedinečné ID nasazení aktuálně spuštěného pořadí úkolů. Používá stejný formát jako Configuration Manager ID nasazení distribuce softwaru. Pokud je pořadí úkolů spuštěné ze samostatného média, není tato proměnná definovaná.

#### <a name="example"></a>Příklad

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje inventární štítek počítače.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a> _SMSTSBootImageID

Pokud aktuálně spuštěné pořadí úkolů odkazuje na balíček spouštěcí bitové kopie, tato proměnná ukládá ID balíčku spouštěcí bitové kopie. Pokud pořadí úkolů neodkazuje na balíček spouštěcí bitové kopie, tato proměnná není nastavená.

#### <a name="example"></a>Příklad

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

Pořadí úkolů tuto proměnnou nastaví, když detekuje počítač, který je v režimu UEFI.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
Pořadí úkolů tuto proměnnou nastaví, když ukládá obsah do mezipaměti na místním disku. Proměnná obsahuje cestu k mezipaměti. Pokud tato proměnná neexistuje, neexistuje mezipaměť.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Ukládá hodnotu Configuration Manager identifikátor GUID klienta. Pokud je pořadí úkolů spuštěné ze samostatného média, tato proměnná není nastavená.

#### <a name="example"></a>Příklad

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Určuje název kroku aktuálně spuštěného pořadí úkolů. Tato proměnná se nastavuje před tím, než správce pořadí úkolů spustí jednotlivé kroky.

#### <a name="example"></a>Příklad

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje výchozí bránu používanou počítačem.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

Pokud aktuální pořadí úkolů běží v režimu stažení na vyžádání, tato proměnná je `true` . Režim stažení na vyžádání znamená, že správce pořadí úkolů stáhne obsah místně pouze v případě, že má přístup k obsahu.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a> _SMSTSInWinPE

Pokud aktuální krok pořadí úkolů běží v prostředí Windows PE, tato proměnná je `true` . Otestujte tuto proměnnou pořadí úkolů a určete aktuální prostředí operačního systému.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje IP adresu, kterou počítač používá.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a> _SMSTSLastActionName

Ukládá název poslední spouštěné akce. Tato proměnná se týká **_SMSTSLastActionRetCode**. Pořadí úkolů protokoluje tyto hodnoty do souboru souboru Smsts. log. Tato proměnná je při řešení potíží s pořadím úkolů prospěšná. V případě neúspěchu kroku může vlastní skript zahrnovat název kroku spolu s návratovým kódem.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Uloží návratový kód z poslední spouštěné akce. Tuto proměnnou jde použít jako podmínku k určení toho, jestli se spustí další krok.

#### <a name="example"></a>Příklad

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- Pokud byl poslední krok úspěšný, tato proměnná je `true` .  

- Pokud se poslední krok nezdařil, je to `false` .  

- Pokud pořadí úloh přeskočilo poslední akci, protože krok je zakázán nebo je přidružená podmínka vyhodnocena jako **NEPRAVDA**, tato proměnná není resetována. Stále obsahuje hodnotu pro předchozí akci.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a> _SMSTSLastContentDownloadLocation

<!-- 2840337 -->
Počínaje verzí 1906 Tato proměnná obsahuje poslední umístění, ve kterém se pořadí úkolů stáhlo nebo se pokusilo stáhnout obsah. Zkontrolujte tuto proměnnou místo analýzy protokolů klienta pro toto umístění obsahu.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Určuje, že pořadí úkolů bylo zahájeno pomocí jedné z následujících metod:  

- **SMS**: klient Configuration Manager, například když ho uživatel spustí z centra softwaru
- **UFD**: starší USB média
- **UFD + Format**: novější USB média
- **CD**: spouštěcí disk CD
- **DVD**: spouštěcí DVD
- **PXE**: spouštění ze sítě pomocí technologie PXE
- **HD**: Předzpracované médium na pevném disku

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a> _SMSTSLogPath

Ukládá úplnou cestu k adresáři protokolů. Pomocí této hodnoty určíte, kde kroky pořadí úloh protokolují své akce. Tato hodnota není nastavená, pokud není k dispozici pevný disk.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje adresu MAC, kterou počítač používá.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a> _SMSTSMachineName

Ukládá a určuje název počítače. Ukládá název počítače, který pořadí úkolů používá k protokolování všech stavových zpráv. Chcete-li změnit název počítače v novém operačním systému, použijte proměnnou [OSDComputerName](#OSDComputerName-input) .

### <a name="_smstsmake"></a><a name="SMSTSMake"></a> _SMSTSMake

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje značku počítače.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Určuje cestu definovanou proměnnou [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) . Tato cesta Určuje, kde pořadí úkolů ukládá dočasné soubory mezipaměti v cílovém počítači, když je spuštěný. Při definování SMSTSLocalDataDrive před spuštěním pořadí úkolů, například nastavením proměnné kolekce, Configuration Manager pak po spuštění pořadí úkolů definuje _SMSTSMDataPath proměnnou.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a> _SMSTSMediaType

Určuje typ média, který se používá k zahájení instalace. Příklady typů médií: spouštěcí médium, úplné médium, prostředí PXE a předzpracované médium.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a> _SMSTSModel

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje model počítače.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a> _SMSTSMP

Ukládá adresu URL nebo IP adresu Configuration Managerho bodu správy.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a> _SMSTSMPPort

Ukládá číslo portu Configuration Managerho bodu správy.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a> _SMSTSOrgName

Ukládá název značky, který pořadí úkolů zobrazuje v dialogovém okně průběh.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Platí pro krok [upgradovat operační systém](task-sequence-steps.md#BKMK_UpgradeOS) .*

Ukládá hodnotu ukončovacího kódu, kterou instalační program systému Windows vrací, aby označovala úspěch nebo neúspěch. Tato proměnná je užitečná s `/Compat` možností příkazového řádku.

#### <a name="example"></a>Příklad

Po dokončení kontroly jen pro sledování stavu proveďte v pozdějších krocích akci v závislosti na kódu chyby nebo ukončení. Po úspěšném zahájení proveďte upgrade. Případně můžete nastavit značku v prostředí, která se bude shromažďovat v inventáři hardwaru. Můžete například přidat soubor nebo nastavit klíč registru. Pomocí této značky můžete vytvořit kolekci počítačů, které jsou připravené k upgradu, nebo které před upgradem vyžadují akci.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a> _SMSTSPackageID

Ukládá ID aktuálně spuštěného pořadí úkolů. Toto ID používá stejný formát jako ID Configuration Manager balíčku.

#### <a name="example"></a>Příklad

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a> _SMSTSPackageName

Ukládá název aktuálně spuštěného pořadí úkolů. Správce Configuration Manager tento název určuje při vytváření pořadí úkolů.

#### <a name="example"></a>Příklad

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Nastavte na, `true` Pokud aktuální pořadí úkolů běží v režimu spuštění z distribučního bodu. Tento režim znamená, že správce pořadí úkolů získá požadované sdílené složky balíčku z distribučního bodu.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje sériové číslo počítače.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Určuje, zda instalační program systému Windows provedení operace vrácení zpět během místního upgradu. Hodnoty proměnné mohou být `true` nebo `false` .

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Ukládá kód lokality Configuration Manager.

#### <a name="example"></a>Příklad

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a> _SMSTSTimezone

Tato proměnná ukládá informace o časovém pásmu v následujícím formátu:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Příklad

Pro časové pásmo **východ (USA a Kanada)**:

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a> _SMSTSType

Určuje typ aktuálně spuštěného pořadí úkolů. Může mít jednu z následujících hodnot:  

- **1**: Obecné pořadí úloh
- **2**: pořadí úloh nasazení operačního systému

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a> _SMSTSUseCRL

Když pořadí úkolů používá ke komunikaci s bodem správy protokol HTTPS, tato proměnná Určuje, jestli používá seznam odvolaných certifikátů (CRL).

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Určuje, jestli uživatel spustil pořadí úkolů. Tato proměnná se nastavuje jenom v případě, že je pořadí úkolů spuštěné z centra softwaru. Například pokud je [_SMSTSLaunchMode](#SMSTSLaunchMode) nastaveno na `SMS` .

Tato proměnná může mít následující hodnoty:  

- `true`: Určuje, jestli je pořadí úkolů ručně spuštěné uživatelem z centra softwaru.  

- `false`: Určuje, zda je pořadí úkolů iniciováno automaticky plánovačem Configuration Manager.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Určuje, jestli pořadí úkolů používá protokol SSL ke komunikaci s bodem správy Configuration Manager. Pokud nakonfigurujete systémy lokality pro protokol HTTPS, hodnota je nastavena na `true` .

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a> _SMSTSUUID

*Platí pro krok [nastavit dynamické proměnné](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Určuje UUID počítače.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a> _SMSTSWTG

Určuje, zda je počítač spuštěn jako zařízení s operačním systémem Windows To Go.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a> _TS_CRMEMORY

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, jestli se **minimální velikost paměti (MB)** vrátila jako true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a> _TS_CRSPEED

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, jestli **minimální rychlost procesoru (MHz)** vrátila hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a> _TS_CRDISK

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, jestli se **minimální volné místo na disku (MB)** vrátilo jako true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a> _TS_CROSTYPE

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, zda **je aktuální operační systém, který má být aktualizován** , vrátila hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a> _TS_CRARCH

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, zda **Architektura aktuální kontroly operačního systému** vrátila hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a> _TS_CRMINOSVER

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, zda **Minimální verze operačního systému** vrátila hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a> _TS_CRMAXOSVER

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, zda je **maximální verze operačního systému** vrácená hodnotou true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a> _TS_CRCLIENTMINVER

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která má **minimální kontrolu verze klienta** vrácenou true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a> _TS_CROSLANGUAGE

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která určuje, zda **jazyk aktuální kontroly operačního systému** vrátil hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a> _TS_CRACPOWER

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná, která je určená jen pro čtení, má za **následek** to, že napájení napájené ze zásuvky vrátilo hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a> _TS_CRNETWORK

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná určená jen pro čtení, která kontroluje, zda je v **připojeném síťovém adaptéru** vrácena hodnota true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_cruefi"></a><a name="TSCRUEFI"></a> _TS_CRUEFI

*Počínaje verzí 2006* <!--6452769-->
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná určená jen pro čtení, která má **počítač v režimu UEFI** , vrátila hodnotu BIOS ( `0` ) nebo UEFI ( `1` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a> _TS_CRWIRED

*Počínaje verzí 2002* <!--6005561-->  
*Platí pro krok [kontrolovat připravenost](task-sequence-steps.md#BKMK_CheckReadiness) .*

Proměnná jen pro čtení, která znamená, že **síťový adaptér nemá kontrolu bezdrátového připojení** , vrátil hodnotu true ( `1` ) nebo false ( `0` ). Pokud tuto kontrolu nepovolíte, hodnota této proměnné jen pro čtení bude prázdná.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a> _TSAppInstallStatus

Pořadí úkolů nastaví tuto proměnnou na stav instalace aplikace během kroku [instalovat aplikaci](task-sequence-steps.md#BKMK_InstallApplication) . Nastaví jednu z následujících hodnot:  

- **Nedefinováno**: krok instalovat aplikaci se nespustil.  

- **Chyba**: nejméně jedna aplikace selhala kvůli chybě během kroku instalace aplikace.  

- **Upozornění**: během kroku instalace aplikace se nevyskytly žádné chyby. Jedna nebo více aplikací nebo požadovaná závislost se nenainstalovala, protože nebyl splněn požadavek.  

- **Úspěch**: během kroku instalovat aplikaci nebyly zjištěny žádné chyby ani upozornění.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a> _TSSecureBoot

*Počínaje verzí 2002* <!--5842295-->  

Pomocí této proměnné můžete určit stav zabezpečeného spouštění na zařízení s podporou rozhraní UEFI. Proměnná může mít jednu z následujících hodnot:

- `NA`: Přidružená hodnota registru neexistuje, což znamená, že zařízení nepodporuje zabezpečené spouštění.
- `Enabled`: Zařízení má povolené zabezpečené spouštění.
- `Disabled`: Zařízení má zakázané zabezpečené spouštění.

### <a name="osdadapter"></a><a name="OSDAdapter"></a> OSDAdapter

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Tato proměnná pořadí úloh je proměnná *pole* . Každý prvek v poli představuje nastavení jednoho síťového adaptéru v počítači. Pomocí kombinace názvu proměnné pole s indexem síťového adaptéru založeným na nule a názvu vlastnosti Získejte přístup k nastavení pro každý adaptér.

Pokud krok použít nastavení sítě konfiguruje více síťových adaptérů, definuje vlastnosti *druhého* síťového adaptéru pomocí indexu **1** v názvu proměnné. Například: určují, základě a OSDAdapter1DNSDomain.

Následující názvy proměnných použijte k definování vlastností *prvního* síťového adaptéru, který má být krok konfigurován:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Toto nastavení je povinné. Možné hodnoty jsou `True` nebo `False`. Příklad:

`true`: Povolte pro adaptér protokol DHCP (Dynamic Host Configuration Protocol).

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Seznam IP adres pro adaptér oddělených čárkami. Tato vlastnost je ignorována, pokud není nastavena vlastnost **nemá proměnná EnableDHCP** na hodnotu `false` . Toto nastavení je povinné.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Seznam masek podsítě oddělených čárkami. Tato vlastnost je ignorována, pokud není nastavena vlastnost **nemá proměnná EnableDHCP** na hodnotu `false` . Toto nastavení je povinné.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Seznam adres bran IP oddělených čárkami. Tato vlastnost je ignorována, pokud není nastavena vlastnost **nemá proměnná EnableDHCP** na hodnotu `false` . Toto nastavení je povinné.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Doména DNS (Domain Name System) pro adaptér.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Seznam serverů DNS pro adaptér oddělených čárkami. Toto nastavení je povinné.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Nastavte na `true` zaregistrování IP adresy pro adaptér ve službě DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Nastavte na hodnotu pro `true` registraci IP adresy pro adaptér ve službě DNS pod úplným názvem DNS počítače.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Nastavte na `true` Povolit filtrování protokolu IP v adaptéru.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Seznam protokolů, které se můžou spouštět přes protokol IP, oddělených čárkami. Tato vlastnost je ignorována, je-li vlastnost **EnableIPProtocolFiltering** nastavena na hodnotu `false` .

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Nastavte na `true` Povolit filtrování portů TCP pro adaptér.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Seznam portů oddělených čárkami, kterým se mají udělit přístupová oprávnění pro TCP Tato vlastnost je ignorována, je-li vlastnost **EnableTCPFiltering** nastavena na hodnotu `false` .

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Možnosti pro rozhraní NetBIOS nad protokolem TCP/IP. Možné hodnoty jsou následující:  

- `0`: Použít nastavení rozhraní NetBIOS ze serveru DHCP  
- `1`: Povolení rozhraní NetBIOS přes TCP/IP  
- `2`: Zakázat rozhraní NetBIOS přes TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

`true`Pro překlad IP adres nastavte, aby se služba WINS používala.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Seznam IP adres serveru WINS oddělených čárkami. Tato vlastnost je ignorována, pokud není nastavena vlastnost **nemá proměnná EnableWINS** na hodnotu `true` .

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

Adresa MAC používaná k párování nastavení s fyzickým síťovým adaptérem.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

Název síťového připojení, který se zobrazí v programu ovládací panel Síťová připojení. Název je dlouhý 0 až 255 znaků.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Index nastavení síťového adaptéru v poli nastavení.

#### <a name="example"></a>Příklad

- **Proměnné OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a> Proměnné OSDAdapterCount

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje počet síťových adaptérů nainstalovaných v cílovém počítači. Při nastavování hodnoty **proměnné OSDAdapterCount** nastavte také všechny možnosti konfigurace pro každý adaptér.

Pokud například nastavíte hodnotu **OSDAdapter0TCPIPNetbiosOptions** pro první adaptér, musíte nakonfigurovat všechny hodnoty pro daný adaptér.

Pokud tuto hodnotu nezadáte, pořadí úkolů ignoruje všechny **OSDAdapter** hodnoty.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a> Nastaví proměnná osdapplydriverbootcriticalcontentuniqueid

*Platí pro krok [použít balíček ovladače](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(vstup)

Určuje ID obsahu ovladače velkokapacitního paměťového zařízení, který se má nainstalovat z balíčku ovladačů. Pokud se tato proměnná nezadá, nenainstaluje se žádný ovladač velkokapacitního paměťového zařízení.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Platí pro krok [použít balíček ovladače](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(vstup)

Určuje, jestli je nainstalovaný ovladač velkokapacitního paměťového zařízení. Tato proměnná musí být **SCSI**.

Pokud je nastavená [Nastaví proměnná osdapplydriverbootcriticalcontentuniqueid](#OSDApplyDriverBootCriticalContentUniqueID) , tato proměnná je povinná.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Platí pro krok [použít balíček ovladače](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(vstup)

Určuje ID (kritické pro spouštění) ovladače velkokapacitního paměťového zařízení, který se má nainstalovat. Toto ID se uvádí v části **SCSI** souboru Txtsetup. OEM ovladače zařízení.

Pokud je nastavená [Nastaví proměnná osdapplydriverbootcriticalcontentuniqueid](#OSDApplyDriverBootCriticalContentUniqueID) , tato proměnná je povinná.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Platí pro krok [použít balíček ovladače](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(vstup)

Určuje soubor INF ovladače velkokapacitního paměťového zařízení, který se má nainstalovat.

Pokud je nastavená [Nastaví proměnná osdapplydriverbootcriticalcontentuniqueid](#OSDApplyDriverBootCriticalContentUniqueID) , tato proměnná je povinná.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Platí pro krok [automaticky použít ovladače](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

(vstup)

Pokud je v katalogu ovladačů více ovladačů zařízení, které jsou kompatibilní s hardwarovým zařízením, tato proměnná Určuje akci kroku.

#### <a name="valid-values"></a>Platné hodnoty

- `true` (výchozí): Nainstalujte jenom nejlepší ovladač zařízení.  

- `false`: Nainstaluje všechny kompatibilní ovladače zařízení a Windows vybere nejlepší ovladač, který se má použít.  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Platí pro krok [automaticky použít ovladače](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

(vstup)

Seznam jedinečných ID kategorií v katalogu ovladačů oddělených čárkami. Krok **automaticky použít ovladač** se považuje jenom na ovladače alespoň v jedné ze zadaných kategorií. Tato hodnota je volitelná a ve výchozím nastavení není nastavená. Získání dostupných ID kategorií pomocí výčtu seznamu **SMS_CategoryInstance** objektů na webu.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a> OSDBitLockerRebootCount

*Platí pro krok [Vypnout nástroj BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker) .*

<!-- 4512937 -->
Počínaje verzí 1906 použijte tuto proměnnou k nastavení počtu restartování po obnovení ochrany.

#### <a name="valid-values"></a>Platné hodnoty

Celé číslo od `1` do `15` .

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a> OSDBitLockerRebootCountOverride

*Platí pro krok [Vypnout nástroj BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker) .*

<!-- 4512937 -->
Počínaje verzí 1906 nastavte tuto hodnotu pro přepsání počtu nastaveného krokem nebo proměnnou [OSDBitLockerRebootCount](#OSDBitLockerRebootCount) . I když ostatní metody akceptují jenom hodnoty 1 až 15, pokud nastavíte tuto proměnnou na 0, BitLocker zůstane neaktivní po neomezenou dobu. Tato proměnná je užitečná v případě, že pořadí úkolů nastavuje jednu hodnotu, ale chcete nastavit samostatnou hodnotu na základě jednotlivých zařízení nebo kolekcí.

#### <a name="valid-values"></a>Platné hodnoty

Celé číslo od `0` do `15` .

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*Platí pro krok [zapnout nástroj BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) .*

(vstup)

Místo generování náhodného hesla pro obnovení použije krok **zapnout nástroj BitLocker** zadanou hodnotu jako heslo pro obnovení. Hodnota musí být platné číselné heslo pro obnovení nástroje BitLocker.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*Platí pro krok [zapnout nástroj BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) .*

(vstup)

Místo vygenerování náhodného spouštěcího klíče pro spouštěcí klíč možnosti správy klíčů **pouze na sběrnici USB** používá krok **zapnout nástroj BitLocker** jako spouštěcí klíč čip Trusted Platform Module (TPM). Hodnota musí být platný 256bitový spouštěcí klíč nástroje BitLocker s kódováním Base64.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(vstup)

Určuje název účtu systému Windows, který má oprávnění k uložení zaznamenané bitové kopie do sdílené síťové složky ([OSDCaptureDestination](#OSDCaptureDestination)). Zadejte také [Proměnná OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

Další informace o účtu image operačního systému Capture najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a> Proměnná OSDCaptureAccountPassword

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(vstup)

Určuje heslo pro účet systému Windows ([OSDCaptureAccount](#OSDCaptureAccount)) používané k uložení zaznamenané bitové kopie ve sdílené síťové složce ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(vstup)

Určuje umístění, ve kterém pořadí úkolů uloží zaznamenanou bitovou kopii operačního systému. Maximální délka názvu adresáře je 255 znaků. Pokud sdílená síťová složka vyžaduje ověření, zadejte proměnné [OSDCaptureAccount](#OSDCaptureAccount) a [Proměnná OSDCaptureAccountPassword](#OSDCaptureAccountPassword) .

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a> OSDComputerName (vstup)

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje název cílového počítače.

#### <a name="example"></a>Příklad

`%_SMSTSMachineName%` výchozí

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a> OSDComputerName (výstup)

*Platí pro krok [zaznamenat nastavení systému Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Nastavte na název pro NetBIOS počítače. Hodnota je nastavena pouze v případě, že je proměnná [OSDMigrateComputerName](#OSDMigrateComputerName) nastavena na hodnotu `true` .

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a> OSDConfigFileName

*Platí pro krok [použít bitovou kopii operačního systému](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(vstup)

Určuje název souboru odpovědí nasazení operačního systému přidruženého k balíčku bitové kopie nasazení operačního systému.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Platí pro krok [použít data bitové kopie](task-sequence-steps.md#BKMK_ApplyDataImage) .*

(vstup)

Určuje hodnotu indexu obrázku, který se použije pro cílový počítač.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a> OSDDiskIndex

*Platí pro krok [Formátovat a rozdělit disk na oddíly](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(vstup)

Určuje číslo fyzického disku, který se má rozdělit na oddíly.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a> OSDDNSDomain

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje primární server DNS, který používá cílový počítač.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje pořadí hledání DNS pro cílový počítač.

### <a name="osddomainname"></a><a name="OSDDomainName"></a> OSDDomainName

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje název domény služby Active Directory, ke které se připojí cílový počítač. Zadaná hodnota musí být platný název domény služby Active Directory Domain Services.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a> OSDDomainOUName

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje název formátu RFC 1779 organizační jednotky (OU), ke které se připojí cílový počítač. Pokud zadáte tuto hodnotu, musí obsahovat úplnou cestu.

#### <a name="example"></a>Příklad

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
*Platí pro krok [instalovat balíček](task-sequence-steps.md#BKMK_InstallPackage) .*

*Počínaje verzí 1902*  
*Platí pro krok [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) .*

(vstup)

Chcete-li zabránit zobrazení nebo protokolování potenciálně citlivých dat, nastavte tuto proměnnou na `TRUE` . Tato proměnná maskuje název programu v **souboru Smsts. log** během kroku **instalace balíčku** .

Počínaje verzí 1902 se při nastavování této proměnné `TRUE` z kroku **Spustit příkazový řádek** v souboru protokolu také skryje příkazový řádek.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje, jestli je povolené filtrování protokolu TCP/IP.

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false` výchozí  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Platí pro krok [Formátovat a rozdělit disk na oddíly](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(vstup)

Určuje, jestli se má na pevném disku GPT vytvořit oddíl EFI. Počítače založené na rozhraní EFI používají tento oddíl jako spouštěcí disk.

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false` výchozí

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a> OSDImageCreator

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(vstup)

Volitelné jméno uživatele, který image vytvořil. Toto jméno je uložené v souboru WIM. Maximální délka uživatelského jména je 255 znaků.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a> OSDImageDescription

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(vstup)

Volitelný popis zaznamenané image operačního systému definovaný uživatelem. Tento popis je uložený v souboru WIM. Maximální délka popisu je 255 znaků.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a> OSDImageIndex

*Platí pro krok [použít bitovou kopii operačního systému](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(vstup)

Určuje hodnotu indexu bitové kopie souboru WIM, která se použije pro cílový počítač.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a> OSDImageVersion

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(vstup)

Volitelné uživatelsky definované číslo verze, které se má přiřadit k zaznamenané bitové kopii operačního systému. Toto číslo verze je uložené v souboru WIM. Tato hodnota může být libovolná kombinace alfanumerických znaků s maximální délkou 32.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Platí pro krok [použít balíček ovladače](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(vstup)

Určuje další možnosti, které se mají přidat do příkazového řádku DISM při použití balíčku ovladače. Pořadí úkolů neověřuje možnosti příkazového řádku.

Chcete-li použít tuto proměnnou, povolte nastavení, **instalovat balíček ovladačů prostřednictvím spuštění DISM s možností rekurze**v kroku **použít balíček ovladače** .

Další informace najdete v tématu [Možnosti příkazového řádku Windows 10 DISM](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a> OSDJoinAccount

*Platí pro následující kroky:*  

- [Použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(vstup)

Určuje uživatelský účet domény, který se používá k přidání cílového počítače do domény. Tato proměnná je při připojování k doméně povinná.

Další informace o účtu připojení k doméně pořadí úkolů najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Platí pro krok [připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(vstup)

Určuje název domény služby Active Directory, ke které se připojí cílový počítač. Název domény musí mít délku 1 až 255 znaků.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Platí pro krok [připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(vstup)

Určuje název formátu RFC 1779 organizační jednotky (OU), ke které se připojí cílový počítač. Pokud zadáte tuto hodnotu, musí obsahovat úplnou cestu. Délka názvu organizační jednotky musí být mezi 0 a 32 767 znaky. Tato hodnota není nastavená, pokud je proměnná [OSDJoinType](#OSDJoinType) nastavená na `1` (připojit k pracovní skupině).

#### <a name="example"></a>Příklad

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a> OSDJoinPassword

*Platí pro následující kroky:*  

- [Použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(vstup)

Určuje heslo pro [OSDJoinAccount](#OSDJoinAccount) , které cílový počítač používá pro připojení k doméně služby Active Directory. Pokud prostředí pořadí úkolů tuto proměnnou neobsahuje, instalační program systému Windows se pokusí zadat prázdné heslo. Pokud je proměnná [OSDJoinType](#OSDJoinType) proměnná nastavená na `0` (připojit k doméně), je tato hodnota povinná.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Platí pro krok [připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(vstup)

Určuje, jestli se má po připojení cílového počítače k doméně nebo pracovní skupině přeskočit restartování.

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a> OSDJoinType

*Platí pro krok [připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(vstup)

Určuje, jestli se má cílový počítač připojit k doméně systému Windows, nebo k pracovní skupině.

#### <a name="valid-values"></a>Platné hodnoty

- `0`: Připojte cílový počítač k doméně systému Windows.  
- `1`: Připojte cílový počítač k pracovní skupině.  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Platí pro krok [připojit k doméně nebo pracovní skupině](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(vstup)

Určuje název pracovní skupiny, ke které se připojí cílový počítač. Délka názvu pracovní skupiny musí být v rozmezí od 1 do 32 znaků.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a> OSDKeepActivation

*Platí pro krok [připravit systém Windows pro zaznamenání](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) .*

(vstup)

Určuje, jestli má nástroj Sysprep zachovat nebo resetovat příznak aktivace produktu.

#### <a name="valid-values"></a>Platné hodnoty

- `true`: zachovat aktivační příznak
- `false` (výchozí): resetovat aktivační příznak

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(vstup)

Určuje heslo účtu místního správce. Pokud povolíte možnost **náhodně generovat heslo místního správce a vypnout účet na všech podporovaných platformách**, pak tento krok tuto proměnnou ignoruje. Zadaná hodnota musí mít délku v rozmezí 1 až 255 znaků.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
*Počínaje verzí 1902*  
*Platí pro krok [Spustit skript PowerShellu](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(vstup)

Aby se zabránilo protokolování potenciálně citlivých dat, krok **Spustit skript PowerShellu** neprotokoluje parametry skriptu v souboru **souboru Smsts. log** . Chcete-li zahrnout parametry skriptu do protokolu pořadí úloh, nastavte tuto proměnnou na **hodnotu true**.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Platí pro krok [zaznamenání nastavení sítě](task-sequence-steps.md#BKMK_CaptureNetworkSettings) .*

(vstup)

Určuje, zda pořadí úloh zachycuje informace o síťovém adaptéru. Tyto informace zahrnují nastavení konfigurace protokolu TCP/IP, DNS a WINS.

#### <a name="valid-values"></a>Platné hodnoty

- `true` výchozí
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a> Proměnné OSDMigrateAdditionalCaptureOptions

*Platí pro krok [zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState) .*

(vstup)

Zadejte další možnosti příkazového řádku pro nástroj pro migraci stavu uživatele (USMT), který pořadí úkolů používá k zaznamenání stavu uživatele. Tento krok nezveřejňuje tato nastavení v editoru pořadí úloh. Zadejte tyto možnosti jako řetězec, který pořadí úkolů připojí k automaticky vygenerovanému příkazovému řádku nástroje USMT pro příkaz ScanState.

Před spuštěním pořadí úloh se u možností nástroje USMT určených touto proměnnou pořadí úkolů neověřuje přesnost.

Další informace o dostupných možnostech najdete v tématu [syntaxe příkazu ScanState](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a> Proměnné OSDMigrateAdditionalRestoreOptions

*Platí pro krok [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState) .*

(vstup)

Určuje další možnosti příkazového řádku pro nástroj pro migraci stavu uživatele (USMT), který pořadí úkolů používá při obnovování stavu uživatele. Zadejte další možnosti jako řetězec, který pořadí úkolů připojí k automaticky vygenerovanému příkazovému řádku nástroje USMT pro LoadState.

Před spuštěním pořadí úloh se u možností nástroje USMT určených touto proměnnou pořadí úkolů neověřuje přesnost.

Další informace o dostupných možnostech najdete v tématu [syntaxe příkazu LoadState](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Platí pro krok [zaznamenat nastavení systému Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(vstup)

Určuje, jestli má proběhnout migrace názvu počítače.

#### <a name="valid-values"></a>Platné hodnoty

- `true` (výchozí). Proměnná [OSDComputerName (Output)](#OSDComputerName-output) se nastaví na název NetBIOS počítače.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Platí pro krok [zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState) .*

(vstup)

Určuje konfigurační soubory, které řídí zaznamenávání uživatelských profilů. Tato proměnná se používá pouze v případě, že je [OSDMigrateMode nastavenou hodnotu](#OSDMigrateMode) nastaveno na `Advanced` . Tato hodnota seznamu odděleného čárkami se nastavuje proto, aby se mohla provést přizpůsobená migrace uživatelských profilů.

#### <a name="example"></a>Příklad

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Platí pro krok [zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState) .*

(vstup)

Pokud nástroj USMT nemůže zachytit některé soubory, tato proměnná umožní pokračovat v zachycení stavu uživatele.

#### <a name="valid-values"></a>Platné hodnoty

- `true` výchozí  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Platí pro krok [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState) .*

(vstup)

Pokračujte v procesu i v případě, že nástroj USMT nemůže obnovit některé soubory.

#### <a name="valid-values"></a>Platné hodnoty

- `true` výchozí  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Platí pro následující kroky:*  

- [Zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState)  

(vstup)

Zapne podrobné protokolování pro nástroj USMT. Tento krok vyžaduje tuto hodnotu.

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false` výchozí  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Platí pro krok [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState) .*

(vstup)

Určuje, jestli se má obnovit účet místního počítače.

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false` výchozí  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Platí pro krok [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState) .*

(vstup)

Pokud je proměnná [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) `true` , tato proměnná musí obsahovat heslo přiřazené *všem* migrovanýchm místním účtům. Nástroj USMT přiřadí stejné heslo ke všem migrovanýchm místním účtům. Zvažte toto heslo jako dočasné a později ho změňte pomocí nějaké jiné metody.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a> OSDMigrateMode nastavenou hodnotu

*Platí pro krok [zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState) .*

(vstup)

Umožňuje přizpůsobit soubory, které nástroj USMT zachytí.

#### <a name="valid-values"></a>Platné hodnoty

- `Simple`: Pořadí úkolů používá jenom standardní konfigurační soubory nástroje USMT.  

- `Advanced`: Proměnná pořadí úloh [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) určuje konfigurační soubory, které nástroj USMT používá.  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Platí pro krok [zaznamenání nastavení sítě](task-sequence-steps.md#BKMK_CaptureNetworkSettings) .*

(vstup)

Určuje, jestli pořadí úkolů migruje informace o členství v pracovní skupině nebo doméně.

#### <a name="valid-values"></a>Platné hodnoty

- `true` výchozí
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Platí pro krok [zaznamenat nastavení systému Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(vstup)

Určuje, jestli krok migruje informace o uživateli a organizaci.

#### <a name="valid-values"></a>Platné hodnoty

- `true` (výchozí). Proměnná [OSDRegisteredOrgName (Output)](#OSDRegisteredOrgName-output) se nastaví na název registrované organizace počítače.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Platí pro krok [zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState) .*

(vstup)

Určuje, jestli se mají zaznamenávat šifrované soubory.

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false` výchozí  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Platí pro krok [zaznamenat nastavení systému Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(vstup)

Určuje, jestli má proběhnout migrace časového pásma počítače.

#### <a name="valid-values"></a>Platné hodnoty

- `true` (výchozí). Proměnná [OSDTimeZone (výstup)](#OSDTimeZone-output) je nastavena na časové pásmo počítače.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje, zda se cílový počítač připojí k doméně služby Active Directory nebo pracovní skupině.

#### <a name="value-values"></a>Hodnoty hodnot

- `0`: Připojte se k doméně služby Active Directory.  
- `1`: Připojte se k pracovní skupině

### <a name="osdpartitions"></a><a name="OSDPartitions"></a> OSDPartitions

*Platí pro krok [Formátovat a rozdělit disk na oddíly](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(vstup)

Tato proměnná pořadí úloh je proměnná pole nastavení oddílu. Každý prvek v poli představuje nastavení jednoho oddílu na pevném disku. Pomocí kombinace názvu proměnné pole s číslem diskového oddílu založeným na nule a názvu vlastnosti získáte přístup k nastavení definovaným pro každý oddíl.

Následující názvy proměnných použijte k definování vlastností *prvního* oddílu, který tento krok vytvoří na pevném disku:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Určuje typ oddílu. Tato vlastnost je povinná. Platné hodnoty jsou `Primary` , `Extended` , `Logical` a `Hidden` .

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Určuje typ systému souborů, který se má použít při formátování oddílu. Tato vlastnost je nepovinná. Pokud nezadáte systém souborů, tento krok nezformátuje oddíl. Platné hodnoty jsou `FAT32` a `NTFS` .

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Určuje, jestli je oddíl spustitelný. Tato vlastnost je povinná. Pokud je tato hodnota nastavená na `TRUE` disky MBR, pak krok označí tento oddíl jako aktivní.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Určuje typ použitého formátu. Tato vlastnost je povinná. Pokud je tato hodnota nastavená na `TRUE` , krok provede rychlé formátování. V opačném případě krok provede úplný formát.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Určuje název, který se přiřadí ke svazku při jeho formátování. Tato vlastnost je nepovinná.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Určuje velikost oddílu. Tato vlastnost je nepovinná. Pokud tato vlastnost není zadána, je oddíl vytvořen pomocí veškerého zbývajícího volného místa. Jednotky určuje proměnná **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

Tento krok používá tyto jednotky k interpretaci proměnné **OSDPartitions0Size** . Tato vlastnost je nepovinná. Platné hodnoty jsou `MB` (výchozí), `GB` a `Percent` .

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Když tento krok vytvoří oddíly, vždy použije další dostupné písmeno jednotky v systému Windows PE. Pomocí této volitelné vlastnosti můžete určit název jiné proměnné pořadí úkolů. Tento krok používá tuto proměnnou k uložení písmene nové jednotky pro budoucí referenci.

Pokud definujete více oddílů pomocí tohoto kroku pořadí úkolů, vlastnosti pro *druhý* oddíl se definují pomocí **1** indexu v názvu proměnné. Například: **: OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**a **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Platí pro krok [Formátovat a rozdělit disk na oddíly](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(vstup)

Určuje styl oddílu, který se má použít při dělení disku na oddíly.

#### <a name="valid-values"></a>Platné hodnoty

- `GPT`: Použijte styl tabulky oddílů GUID.
- `MBR`: Použít styl oddílu hlavního spouštěcího záznamu

### <a name="osdproductkey"></a><a name="OSDProductKey"></a> OSDProductKey

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(vstup)

Určuje kód Product Key systému Windows. Zadaná hodnota musí mít délku v rozmezí 1 až 255 znaků.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(vstup)

Určuje náhodně generované heslo pro účet místního správce v novém operačním systému.

#### <a name="valid-values"></a>Platné hodnoty

- `true` (výchozí): instalační program systému Windows zakáže účet místního správce v cílovém počítači.  

- `false`: Instalační program systému Windows povolí účet místního správce v cílovém počítači a nastaví heslo účtu na hodnotu [OSDLocalAdminPassword](#OSDLocalAdminPassword) .  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (vstup)

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje název výchozí registrované organizace v novém operačním systému. Zadaná hodnota musí mít délku v rozmezí 1 až 255 znaků.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (výstup)

*Platí pro krok [zaznamenat nastavení systému Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Nastaví se na název registrované organizace počítače. Hodnota je nastavena pouze v případě, že je proměnná [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) nastavena na hodnotu `true` .

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(vstup)

Určuje výchozí registrované uživatelské jméno v novém operačním systému. Zadaná hodnota musí mít délku v rozmezí 1 až 255 znaků.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(vstup)

Určuje maximální povolený počet připojení. Zadané číslo musí být v rozsahu od 5 do 9999 připojení.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(vstup)

Určuje režim licence systému Windows Server, který se používá.

#### <a name="valid-values"></a>Platné hodnoty

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Platí pro krok [upgradovat operační systém](task-sequence-steps.md#BKMK_UpgradeOS) .*

(vstup)

Určuje další možnosti příkazového řádku, které se přidají do instalační program systému Windows během upgradu Windows 10. Pořadí úkolů neověřuje možnosti příkazového řádku.

Další informace najdete v článku [Možnosti příkazového řádku instalačního programu systému Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Platí pro krok [úložiště stavu požadavku](task-sequence-steps.md#BKMK_RequestStateStore) .*

(vstup)

Pokud se účtu počítače nepovede připojit k bodu migrace stavu, tato proměnná Určuje, zda se pořadí úkolů vrátí k použití účtu přístupu k síti (NAA).

Další informace o účtu přístupu k síti najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Platné hodnoty

- `true`  
- `false` výchozí  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Platí pro krok [úložiště stavu požadavku](task-sequence-steps.md#BKMK_RequestStateStore) .*

(vstup)

Určuje, kolikrát se tento krok pořadí úkolů pokusí najít bod migrace stavu, než selže. Zadaný počet musí být v rozmezí od 0 do 600.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Platí pro krok [úložiště stavu požadavku](task-sequence-steps.md#BKMK_RequestStateStore) .*

(vstup)

Určuje dobu v sekundách, kterou krok pořadí úkolů čeká mezi pokusy o opakování. Počet sekund může obsahovat maximálně 30 znaků.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a> Proměnnou OSDStateStorePath

*Platí pro následující kroky:*  

- [Zaznamenat stav uživatele](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Úložiště stavu uvolnění](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Úložiště stavu požadavku](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Obnovit stav uživatele](task-sequence-steps.md#BKMK_RestoreUserState)  

(vstup)

Sdílená síťová složka nebo název místní cesty složky, ve které pořadí úkolů ukládá nebo obnovuje stav uživatele. Není k dispozici žádná výchozí hodnota.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Platí pro krok [použít bitovou kopii operačního systému](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(výstup)

Určuje písmeno jednotky oddílu, který obsahuje soubory operačního systému po použití bitové kopie.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (vstup)

*Platí pro krok [zaznamenání bitové kopie operačního systému](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

Určuje cestu k adresáři systému Windows instalovaného operačního systému v referenčním počítači. Pořadí úkolů ho ověří jako podporovaný operační systém pro zachycení pomocí Configuration Manager.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (výstup)

*Platí pro krok [připravit systém Windows pro zaznamenání](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) .*

Určuje cestu k adresáři systému Windows instalovaného operačního systému v referenčním počítači. Pořadí úkolů ho ověří jako podporovaný operační systém pro zachycení pomocí Configuration Manager.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a> OSDTimeZone (vstup)

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje výchozí nastavení časového pásma, které se používá v novém operačním systému.

Nastavte hodnotu této proměnné na jazykový neutrální název časového pásma. Například použijte řetězec v `Std` hodnotě pro časové pásmo v následujícím klíči registru: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones` .

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a> OSDTimeZone (výstup)

*Platí pro krok [zaznamenat nastavení systému Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Nastaví se na časové pásmo počítače. Hodnota je nastavena pouze v případě, že je proměnná [OSDMigrateTimeZone](#OSDMigrateTimeZone) nastavena na hodnotu `true` .

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a> OSDWindowsSettingsInputLocale

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje výchozí vstupní nastavení národního prostředí, které se používá v novém operačním systému.

Další informace o hodnotě souboru odpovědí instalačního programu systému Windows najdete v tématu [Microsoft-Windows-International-Core-InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a> OSDWindowsSettingsSystemLocale

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje výchozí nastavení národního prostředí systému, které se používá v novém operačním systému.

Další informace o hodnotě souboru odpovědí instalačního programu systému Windows najdete v tématu [Microsoft-Windows-International-Core-SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a> OSDWindowsSettingsUILanguage

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje výchozí nastavení jazyka uživatelského rozhraní, které se používá v novém operačním systému.

Další informace o hodnotě souboru odpovědí instalačního programu systému Windows najdete v tématu [Microsoft-Windows-International-Core-UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a> OSDWindowsSettingsUILanguageFallback

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje nastavení jazyka náhradního uživatelského rozhraní, které se používá v novém operačním systému.

Další informace o hodnotě souboru odpovědí instalačního programu systému Windows najdete v tématu [Microsoft-Windows-International-Core-UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a> OSDWindowsSettingsUserLocale

*Platí pro krok [použít nastavení systému Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Určuje výchozí nastavení národního prostředí uživatele používané v novém operačním systému.

Další informace o hodnotě souboru odpovědí instalačního programu systému Windows najdete v tématu [Microsoft-Windows-International-Core-UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Platí pro krok [použít data bitové kopie](task-sequence-steps.md#BKMK_ApplyDataImage) .*

(vstup)

Určuje, jestli se mají odstranit soubory v cílovém oddílu.

#### <a name="valid-values"></a>Platné hodnoty

- `true` výchozí
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Platí pro krok [použít nastavení sítě](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(vstup)

Určuje název pracovní skupiny, ke které se připojí cílový počítač.

Zadejte buď tuto proměnnou, nebo proměnnou [OSDDomainName](#OSDDomainName) . Název pracovní skupiny nesmí být delší než 32 znaků.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a> SetupCompletePause

*Platí pro krok [upgradovat operační systém](task-sequence-steps.md#BKMK_UpgradeOS) .*

<!-- 4680263 -->

Počínaje verzí 1910 použijte tuto proměnnou k řešení problémů s časováním v rámci pořadí úkolů v rámci místního upgradu na zařízení s vysokým výkonem při dokončení instalace systému Windows. Když přiřadíte hodnotu v sekundách k této proměnné, proces instalace systému Windows zpozdí prodlevu před spuštěním pořadí úloh. Tento časový limit poskytuje Configuration Manager klientovi další čas k inicializaci.

Následující položky protokolu jsou běžné příklady tohoto problému, které můžete s touto proměnnou opravit:

- Komponenta TSManager zaznamenává položky podobné následujícím chybám v **protokolu souboru Smsts. log**:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Instalační program systému Windows zaznamenává položky podobné následujícím chybám v **SetupComplete. log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Platí pro krok [nastavit systém Windows a nástroj ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) .*

(vstup)

Určuje vlastnosti instalace klienta, které pořadí úkolů používá při instalaci klienta Configuration Manager.

Další informace najdete v tématu [informace o parametrech instalace a vlastnostech klienta](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Platí pro krok [připojit k síťové složce](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(vstup)

Určuje uživatelský účet, který se používá pro připojení ke sdílené síťové složce v [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Zadejte heslo účtu s hodnotou [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) .

Další informace o účtu připojení síťové složky pořadí úkolů najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Platí pro krok [připojit k síťové složce](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(vstup)

Určuje písmeno jednotky, ke které se má provést připojení. Tato hodnota je volitelná. Pokud není zadaný, síťové připojení není namapované na písmeno jednotky. Pokud je zadána tato hodnota, hodnota musí být v rozsahu od D do Z. Nepoužívejte X, je písmeno jednotky používané prostředím Windows PE během fáze prostředí Windows PE.

#### <a name="examples"></a>Příklady

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Platí pro krok [připojit k síťové složce](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(vstup)

Určuje heslo pro [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) , které se používá pro připojení ke sdílené síťové složce v [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Platí pro krok [připojit k síťové složce](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(vstup)

Určuje síťovou cestu pro připojení. Pokud potřebujete namapovat tuto cestu k písmenu jednotky, použijte hodnotu [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) .

#### <a name="example"></a>Příklad

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Platí pro krok [instalovat aktualizace softwaru](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(vstup)

Určuje, jestli se mají nainstalovat všechny aktualizace, nebo jenom ty povinné.

#### <a name="valid-values"></a>Platné hodnoty

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a> SMSRebootMessage

*Platí pro krok [restartovat počítač](task-sequence-steps.md#BKMK_RestartComputer) .*

(vstup)

Určuje, jaká zpráva se má zobrazit uživatelům před restartováním cílového počítače. Pokud tato proměnná není nastavená, zobrazí se výchozí text zprávy. Zadaná zpráva nesmí být delší než 512 znaků.

#### <a name="example"></a>Příklad

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Platí pro krok [restartovat počítač](task-sequence-steps.md#BKMK_RestartComputer) .*

(vstup)

Určuje počet sekund, po který se má uživateli zobrazit upozornění před restartováním počítače.

#### <a name="examples"></a>Příklady

- `0` (výchozí): Nezobrazovat zprávu o restartování  
- `60`: Zobrazí upozornění na jednu minutu.  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

Počet sekund, po který se má počkat, než se klient pokusí stáhnout zásady od posledního pokusu, který nevrátil žádné zásady. Ve výchozím nastavení klient počká **0** sekund, než se zopakuje.

Tuto proměnnou lze nastavit pomocí příkazu před spuštěním z médií nebo PXE.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

Počet, kolikrát se klient pokusí stáhnout zásadu, když se při prvním pokusu nenaleznou žádné zásady. Ve výchozím nastavení se klient opakuje o **hodnotu 0** krát.

Tuto proměnnou lze nastavit pomocí příkazu před spuštěním z médií nebo PXE.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Určuje, jak pořadí úkolů přidružuje uživatele k cílovému počítači. Nastavte proměnnou na jednu z následujících hodnot:  

- **Automaticky**: když pořadí úkolů NASADÍ operační systém do cílového počítače, vytvoří vztah mezi zadanými uživateli a cílovým počítačem.  

- **Čeká na vyřízení**: pořadí úkolů vytvoří vztah mezi zadanými uživateli a cílovým počítačem. Správce musí pro jeho nastavení schválit relaci.  

- **Zakázáno**: pořadí úkolů nespojuje uživatele s cílovým počítačem při nasazení operačního systému.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
V případě odpojených scénářů se modul pořadí úloh opakovaně pokouší odeslat stavové zprávy do bodu správy. Toto chování v tomto scénáři způsobuje zpoždění při zpracování pořadí úkolů.

Nastavte tuto proměnnou na `true` a modul pořadí úkolů se nebude pokoušet odeslat stavové zprávy, když se první zpráva nepodaří odeslat. Tento první pokus zahrnuje více opakovaných pokusů.

Když se pořadí úkolů restartuje, hodnota této proměnné přetrvává. Pořadí úkolů se ale pokusí odeslat počáteční stavovou zprávu. Tento první pokus zahrnuje více opakovaných pokusů. V případě úspěchu bude pořadí úloh pokračovat ve stavu odesílání bez ohledu na hodnotu této proměnné. Pokud se stav nepovede odeslat, pořadí úkolů použije hodnotu této proměnné.

> [!NOTE]  
> [Generování sestav o stavu pořadí úkolů](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) spoléhá na tyto stavové zprávy a zobrazí průběh, historii a podrobnosti jednotlivých kroků. Pokud se stavové zprávy nepodařilo odeslat, nejsou zařazeny do fronty. Po obnovení připojení do bodu správy nejsou odesílány později. Výsledkem tohoto chování je, že generování sestav stavu pořadí úloh bude neúplné a chybějící položky.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Platí pro krok [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) .*

(vstup)

Ve výchozím nastavení v 64 operačním systému pořadí úloh vyhledá a spustí program v příkazovém řádku pomocí přesměrovače systému souborů WOW64. Toto chování umožňuje příkazu najít 32 bitové verze programů a knihoven DLL operačního systému. Nastavení této proměnné `true` zakáže používání přesměrovače systému souborů WOW64. Příkaz najde nativní 64 verze programů a knihoven DLL operačního systému. Tato proměnná nemá žádný vliv, pokud je spuštěná v 32 operačním systému.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

Tato proměnná obsahuje hodnotu přerušit kód pro nástroj pro stažení externího programu. Tento program je určen v proměnné [SMSTSDownloadProgram](#SMSTSDownloadProgram) . Pokud program vrátí kód chyby, který se rovná hodnotě proměnné SMSTSDownloadAbortCode, stažení obsahu se nezdaří a nebude proveden pokus o jinou metodu stažení.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

Pomocí této proměnné můžete určit alternativního poskytovatele obsahu (ACP). AKT je stahovací program, který se používá ke stahování obsahu. Pořadí úkolů místo výchozího Configuration Managerho stahovacího programu používá AKT. V rámci procesu stahování obsahu pořadí úloh kontroluje tuto proměnnou. Je-li tento parametr zadán, spustí pořadí úloh program, který stáhne obsah.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

Počet, kolikrát se Configuration Manager pokusí stáhnout obsah z distribučního bodu. Ve výchozím nastavení se klient opakuje **2** časy.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

Počet sekund, po které Configuration Manager čekat, než se znovu pokusí stáhnout obsah z distribučního bodu. Ve výchozím nastavení počká klient **15** sekund, než se znovu pokusí.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Platí pro krok [automaticky použít ovladače](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Při vyžádání katalogu ovladačů Tato proměnná představuje počet sekund, po které pořadí úkolů počká na připojení k serveru HTTP. Pokud připojení trvá déle než nastavení časového limitu, pořadí úkolů zruší požadavek. Ve výchozím nastavení je časový limit nastavený na **60** sekund.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Platí pro krok [automaticky použít ovladače](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Při vyžádání katalogu ovladačů Tato proměnná představuje počet sekund, po které pořadí úkolů počká na odpověď. Pokud připojení trvá déle než nastavení časového limitu, pořadí úkolů zruší požadavek. Ve výchozím nastavení je časový limit nastavený na **480** sekund.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Platí pro krok [automaticky použít ovladače](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Při vyžádání katalogu ovladačů Tato proměnná představuje počet sekund, po které pořadí úkolů počká na překlad názvů HTTP. Pokud připojení trvá déle než nastavení časového limitu, pořadí úkolů zruší požadavek. Ve výchozím nastavení je časový limit nastavený na **60** sekund.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Platí pro krok [automaticky použít ovladače](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

Při odesílání požadavku na katalog ovladačů Tato proměnná představuje počet sekund, po které pořadí úkolů počká na odeslání žádosti. Pokud požadavek trvá déle než nastavení časového limitu, pořadí úkolů zruší požadavek. Ve výchozím nastavení je časový limit nastavený na **60** sekund.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

Pokud v pořadí úkolů dojde k chybě, zobrazí se dialogové okno s chybou. Pořadí úkolů je automaticky zavře po uplynutí počtu sekund zadaného touto proměnnou. Ve výchozím nastavení je tato hodnota **900** sekund (15 minut).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

Pomocí této proměnné lze změnit jazyk zobrazení v jazykově neutrální spouštěcí bitové kopii.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Určuje, kde pořadí úkolů ukládá dočasné soubory mezipaměti v cílovém počítači, když je spuštěný.

Nastavte tuto proměnnou před spuštěním pořadí úkolů, například nastavením proměnné kolekce. Po spuštění pořadí úloh Configuration Manager definuje proměnnou [_SMSTSMDataPath](#SMSTSMDataPath) na základě toho, na jakou proměnnou SMSTSLocalDataDrive byla definovaná.

### <a name="smstsmp"></a><a name="SMSTSMP"></a> SMSTSMP

Pomocí této proměnné můžete zadat adresu URL nebo IP adresu bodu správy Configuration Manager.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Platí pro následující kroky:*  

- [Instalovat aplikaci](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalovat aktualizace softwaru](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(vstup)

Pokud klient není v intranetu, pomocí této proměnné povolte opakované žádosti opakované mplist o aktualizaci klienta. Ve výchozím nastavení je tato proměnná nastavena na `True` .

Pokud jsou klienti připojeni k Internetu, nastavte tuto proměnnou na, aby `False` nedocházelo k zbytečným zpožděním.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Platí pro následující kroky:*  

- [Instalovat aplikaci](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalovat aktualizace softwaru](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(vstup)

Pokud pořadí úloh nepovede načíst seznam bodů správy (opakované mplist) ze služeb zjišťování polohy, tato proměnná Určuje, kolik milisekund se počká, než se znovu pokusí krok zopakovat. Ve výchozím nastavení pořadí úkolů počká na `60000` milisekundy (60 sekund), než se zopakuje. Opakuje se až třikrát.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Pomocí této proměnné můžete klientovi povolit použití sdílené mezipaměti prostředí Windows PE. Nastavením této proměnné `true` povolíte tuto funkci.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Vlastní port sítě, který sdílená mezipaměť prostředí Windows PE používá pro počáteční všesměrové vysílání. Výchozí port konfigurovaný v nastavení klienta je **8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a> Proměnné SMSTSPersistContent

Pomocí této proměnné lze dočasně zachovat obsah v mezipaměti pořadí úloh. Tato proměnná se liší od [SMSTSPreserveContent](#SMSTSPreserveContent), která uchovává obsah v mezipaměti klienta Configuration Manager po dokončení pořadí úloh. Proměnné SMSTSPersistContent používá mezipaměť pořadí úloh, SMSTSPreserveContent používá mezipaměť klienta Configuration Manager.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a> SMSTSPostAction

Určuje příkaz, který se spustí po dokončení pořadí úloh. Například určete `shutdown.exe /r /t 30 /f` restart počítače 30 sekund po dokončení pořadí úloh.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Vynutí, aby pořadí úkolů spouštělo konkrétní cílené nasazení na cílovém počítači. Tuto proměnnou nastavte pomocí příkazu před zahájením z médií nebo PXE. Pokud je tato proměnná nastavená, pořadí úkolů přepíše všechna požadovaná nasazení.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

Tato proměnná označí obsah v pořadí úkolů tak, aby byl po nasazení uchováván v mezipaměti klienta Configuration Manager. Tato proměnná se liší od [proměnné SMSTSPersistContent](#SMSTSPersistContent), která uchovává pouze obsah po dobu trvání pořadí úkolů. Proměnné SMSTSPersistContent používá mezipaměť pořadí úloh, SMSTSPreserveContent používá mezipaměť klienta Configuration Manager. Pokud `true` Chcete tuto funkci povolit, nastavte SMSTSPreserveContent.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Určuje, kolik sekund se má čekat před restartováním počítače. Pokud je tato proměnná nula (0), správce pořadí úkolů před restartováním nezobrazí dialogové okno s oznámením.

#### <a name="example"></a>Příklad

- `0`: Nezobrazovat oznámení  

- `60`: Zobrazit oznámení po dobu jedné minuty  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a> SMSTSRebootDelayNext

<!--4447680-->
Počínaje verzí 1906 použijte tuto proměnnou s existující proměnnou [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) . Pokud chcete, aby pozdější restartování probíhalo s jiným časovým limitem, než je první, nastavte SMSTSRebootDelayNext na jinou hodnotu v sekundách.

#### <a name="example"></a>Příklad

Chcete uživatelům poskytnout oznámení o restartování po 60 minutách na začátku pořadí úkolů místního upgradu systému Windows 10. Po prvním dlouhém časovém limitu budete chtít, aby další časové limity byly jenom 60 sekund. Nastavte SMSTSRebootDelay na `3600` a SMSTSRebootDelayNext na `60` .  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Určuje zprávu, která se zobrazí v dialogovém okně oznámení o restartování. Pokud tato proměnná není nastavená, zobrazí se výchozí zpráva.

#### <a name="example"></a>Příklad

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a> Proměnná SMSTSRebootRequested

Označuje, že se po dokončení aktuálního kroku pořadí úkolů vyžaduje restartování. Pokud krok pořadí úkolů vyžaduje restart, aby se akce mohla dokončit, nastavte tuto proměnnou. Po restartování počítače bude pořadí úkolů dál běžet od dalšího kroku pořadí úkolů.

- `HD`: Restart do nainstalovaného operačního systému
- `WinPE`: Restart do přidružené spouštěcí bitové kopie

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Po dokončení aktuálního kroku pořadí úkolů vyžádá provedení opakovaného pokusu. Pokud je tato proměnná pořadí úloh nastavená, nastavte také proměnnou [Proměnná SMSTSRebootRequested](#SMSTSRebootRequested) na `true` . Po restartování počítače správce pořadí úkolů znovu spustí stejný krok pořadí úkolů.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a> SMSTSRunCommandLineAsUser

*Počínaje verzí 2002* <!-- 5573175 -->  
*Platí pro krok [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) .*

Pomocí proměnných pořadí úkolů můžete nakonfigurovat kontext uživatele pro krok **Spustit příkazový řádek** . Pokud chcete použít proměnné [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) a [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) , není nutné konfigurovat krok **Spustit příkazový řádek** se zástupným účtem.

Nakonfigurujte `SMSTSRunCommandLineAsUser` jednu z následujících hodnot:

- `true`: Všechny další kroky **příkazového řádku spouštěné** v kontextu uživatele zadaného v `SMSTSRunCommandLineUserName` .

- `false`: Všechny další kroky **příkazového řádku spouštějte** v kontextu, který jste nakonfigurovali v kroku.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Platí pro krok [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) .*

(vstup)

Určuje účet, pomocí kterého se má příkazový řádek spustit. Hodnota je řetězec ve tvaru uživatelské jméno nebo doména\uživatelské jméno. Zadejte heslo účtu s proměnnou [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) .

> [!NOTE]
> Počínaje verzí 2002 použijte proměnnou [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) s touto proměnnou ke konfiguraci kontextu uživatele pro tento krok.
>
> V části verze 1910 a starší nakonfigurujte krok **Spustit příkazový řádek** s nastavením na **Spustit tento krok jako následující účet**. Pokud povolíte tuto možnost, Pokud nastavujete uživatelské jméno a heslo pomocí proměnných, zadejte pro účet libovolnou hodnotu.

Další informace o účtu Spustit jako pro pořadí úloh najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword

*Platí pro krok [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) .*

(vstup)

Určuje heslo k účtu určenému proměnnou [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) .

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a> SMSTSRunPowerShellAsUser

*Počínaje verzí 2002* <!-- 5573175 -->  
*Platí pro krok [Spustit skript PowerShellu](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

Pomocí proměnných pořadí úkolů můžete nakonfigurovat kontext uživatele pro krok **spuštění skriptu PowerShellu** . Pokud chcete použít proměnné [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) a [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) , nemusíte konfigurovat krok **Spustit skript PowerShellu** se zástupným účtem.

Nakonfigurujte `SMSTSRunPowerShellAsUser` jednu z následujících hodnot:

- `true`: Všechny další **spuštěné kroky skriptu PowerShellu** se spouštějí v kontextu uživatele zadaného v `SMSTSRunPowerShellUserName` .

- `false`: Všechny další **spuštěné kroky skriptu PowerShellu** se spouštějí v kontextu, který jste nakonfigurovali v kroku.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a> SMSTSRunPowerShellUserName

*Platí pro krok [Spustit skript PowerShellu](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(vstup)

Určuje účet, pomocí kterého se skript prostředí PowerShell spustí. Hodnota je řetězec ve tvaru uživatelské jméno nebo doména\uživatelské jméno. Zadejte heslo účtu s proměnnou [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) .

> [!NOTE]
> Pokud chcete tyto proměnné použít, nakonfigurujte krok **Spustit skript PowerShellu** s nastavením na **Spustit tento krok jako následující účet**. Pokud povolíte tuto možnost, Pokud nastavujete uživatelské jméno a heslo pomocí proměnných, zadejte pro účet libovolnou hodnotu.

Další informace o účtu Spustit jako pro pořadí úloh najdete v tématu [účty](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a> SMSTSRunPowerShellUserPassword

*Platí pro krok [Spustit skript PowerShellu](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(vstup)

Určuje heslo k účtu určenému proměnnou [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) .

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Platí pro krok [instalovat aktualizace softwaru](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(vstup)

Určuje časový limit kontroly aktualizací softwaru v průběhu tohoto kroku. Například pokud očekáváte, že se během kontroly bude počítat větší množství aktualizací, zvyšte hodnotu. Výchozí hodnota je `3600` sekund (60 minut). Hodnota proměnné se nastaví v sekundách.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Určuje primární uživatele cílového počítače pomocí následujícího formátu: `<DomainName>\<UserName>` . Oddělte více uživatelů pomocí čárky ( `,` ). Další informace najdete v tématu [přidružení uživatelů k cílovému počítači](../get-started/associate-users-with-a-destination-computer.md).

#### <a name="example"></a>Příklad

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Platí pro krok [instalovat aktualizace softwaru](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(vstup)

Tato volitelná proměnná pořadí úkolů řídí chování klienta v případě, že instalace aktualizace softwaru vyžaduje dva restarty. Před tímto krokem nastavte tuto proměnnou, aby se zabránilo selhání pořadí úkolů kvůli druhému restartování z instalace aktualizace softwaru.

Nastavte hodnotu SMSTSWaitForSecondReboot v sekundách, pokud chcete určit, jak dlouho pořadí úkolů při tomto kroku pozastaví tento krok, když se počítač restartuje. V případě, že dojde k druhému restartování, umožněte dostatek času.

Například pokud nastavíte SMSTSWaitForSecondReboot na `600` , pořadí úkolů se po restartování pozastaví na 10 minut, než se spustí další kroky. Tato proměnná je užitečná v případě, že krok pořadí úkolů instalovat aktualizace softwaru nainstaluje stovky aktualizací softwaru.

> [!Note]
> Tato proměnná platí pouze pro pořadí úkolů, které nasazuje operační systém. Nefunguje ve vlastním pořadí úkolů. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a> TSDebugMode

<!--3612274-->
Počínaje verzí 1906 nastavte tuto proměnnou na `TRUE` objekt na kolekci nebo počítači, na který je pořadí úkolů nasazeno. Jakékoli zařízení, které má tuto sadu proměnných, vloží do režimu ladění jakékoli nasazené pořadí úkolů.

Další informace najdete v tématu [ladění pořadí úkolů](../deploy-use/debug-task-sequence.md).

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a> TSDebugOnError

<!-- 5012536 -->
Počínaje verzí 1910 nastavte tuto proměnnou na `TRUE` automaticky spustit [ladicí program pořadí úkolů](../deploy-use/debug-task-sequence.md) , když pořadí úkolů vrátí chybu.

Nastavit tuto proměnnou pomocí:

- Krok [nastavit proměnnou pořadí úloh](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- Proměnná kolekce. Další informace naleznete v tématu [jak nastavit proměnné](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Tuto proměnnou použijte k určení, kdy bude pořadí úkolů zobrazovat pokrok koncovým uživatelům. Chcete-li skrýt nebo zobrazit průběh v různých časech, nastavte tuto proměnnou několikrát v pořadí úkolů.  

- `true`: Skrýt průběh pořadí úloh  

- `false`: Zobrazí průběh pořadí úloh.  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Platí pro krok [instalovat aplikaci](task-sequence-steps.md#BKMK_InstallApplication) .*

(vstup)

Určete, zda modul pořadí úkolů považuje zjištěné upozornění za chybu v průběhu tohoto kroku. Pořadí úkolů nastaví proměnnou [_TSAppInstallStatus](#TSAppInstallStatus) na hodnotu v `Warning` případě, že jedna nebo více aplikací nebo požadovaná závislost se nenainstalovala, protože nesplňovala požadavek. Když nastavíte tuto proměnnou na `True` a pořadím úkolů nastavíte **_TSAppInstallStatus** na `Warning` , výsledek je chyba. Hodnota `False` je výchozí chování.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a> TSProgressInfoLevel

*Počínaje verzí 2002*<!--5932692-->  

Tuto proměnnou zadejte, chcete-li řídit typ informací zobrazených v okně průběh pořadí úloh. Pro tuto proměnnou použijte následující hodnoty:

- `1`: Zahrňte aktuální krok a celkový postup do textu průběhu. Například **2 z 10**.
- `2`: Zahrňte aktuální krok, celkový počet kroků a procento dokončení. Příklad: **2 z 10 (dokončeno 20%)**.
- `3`: Uveďte procento dokončení. Například **(20% dokončeno)**.

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a> TSUEFIDrive

Použijte ve vlastnostech oddílu FAT32 v poli **Proměnná** . Když pořadí úkolů detekuje tuto proměnnou, připraví disk pro přechod na rozhraní UEFI před restartováním počítače. Další informace najdete v tématu [postup pro správu převodu systému BIOS na rozhraní UEFI v části pořadí úkolů](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a> WorkingDirectory

*Platí pro krok [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) .*

(vstup)

Určuje spouštěcí adresář pro akci příkazového řádku. Zadaný název adresáře nesmí být delší než 255 znaků.

#### <a name="examples"></a>Příklady

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Zastaralé proměnné

Následující proměnné jsou zastaralé:

- **OSDAllowUnsignedDriver**: se nepoužívá při nasazení systému Windows Vista a novějších operačních systémů.
- **OSDBuildStorageDriverList**: platí pouze pro systémy Windows XP a windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: vyžaduje se jenom při nasazení Windows XP nebo windows serveru 2003.
- **OSDInstallEditionIndex**: není potřeba post-Windows Vista.
- **OSDPreserveDriveLetter**: Další informace najdete v tématu [OSDPreserveDriveLetter](#osdpreservedriveletter) .

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Tato proměnná pořadí úloh je zastaralá.
>
> Při nasazení operačního systému ve výchozím nastavení instalační program systému Windows určuje nejvhodnější písmeno jednotky, které se má použít (obvykle C:).

*Předchozí chování*: při použití image proměnná OSDPreverveDriveLetter určuje, jestli pořadí úkolů používá písmeno jednotky zaznamenané v souboru bitové kopie (WIM). Nastavte hodnotu této proměnné na, pokud chcete `false` použít umístění, které určíte v nastavení **cíl** v kroku pořadí úkolů **použít operační systém** . Další informace najdete v tématu [použití bitové kopie operačního systému](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Viz také:

- [Kroky pořadí úkolů](task-sequence-steps.md)
- [Použití proměnných pořadí úloh](using-task-sequence-variables.md)
- [Aspekty plánování pro automatizaci úloh](../plan-design/planning-considerations-for-automating-tasks.md)