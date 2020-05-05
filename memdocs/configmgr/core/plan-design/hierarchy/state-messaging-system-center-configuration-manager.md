---
title: Stavové zprávy
titleSuffix: Configuration Manager
description: Popisy stavových zpráv v podporovaných verzích Configuration Manager.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720930"
---
# <a name="state-messages-in-configuration-manager"></a>Stavové zprávy v Configuration Manager 

*Platí pro: Configuration Manager (Current Branch)*

Zprávy o stavu obsahují stručné informace o podmínkách pro klienta Configuration Manager. Stavový systém zasílání zpráv je používán konkrétními součástmi Configuration Manager, jako jsou aktualizace softwaru a nastavení konfigurace.

Klienti Configuration Manager odesílají zprávy o stavu pro náhradní stavové zprávy nebo systémy lokality bodu správy, aby hlásily aktuální stav operací. Můžete vytvářet sestavy pro zobrazení stavových zpráv odesílaných klienty Configuration Manager.

Každá funkce Configuration Manager, která používá stavové zprávy, je identifikována typem tématu zprávy o stavu. Typy témat stavových zpráv, které jsou uvedeny v tomto článku, lze použít k definování Configuration Manager funkce, ke které se vztahuje stavová zpráva.

> [!NOTE]  
> Hodnota ID stavové zprávy nula (0) se obvykle označuje, že typ tématu je v neznámém stavu.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0 | Stav dodržování předpisů je neznámý|
| 1 | Odpovídající | 
| 2 | Neodpovídající | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0  | Stav vynucení neznámý |
| 1  | Probíhá instalace aktualizace (í)        | 
| 2  | Čeká se na restart.          | 
| 3  | Čeká se na dokončení jiné instalace.         | 
| 4  | Úspěšná instalace aktualizace (2)          | 
| 5  | Čeká se na restart systému.         | 
| 6  | Nepovedlo se nainstalovat aktualizace (y).         | 
| 7  | Stahují se aktualizace (y).   | 
| 8  | Stažené aktualizace (y)    | 
| 9  | Nepovedlo se stáhnout aktualizaci (e).     | 
| 10 | Čekání na časový interval pro správu a údržbu před instalací         | 
| 11 | Čekání na orchestraci         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|      
| 0 | Stav vyhodnocení neznámý|                 
| 1 |Vyhodnocení aktivované      |
| 2 |Vyhodnocení bylo úspěšné.      |
| 3 |Neúspěšné vyhodnocení      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0 | Neznámý stav detekce|
| 1 | Není požadováno   |
| 2 | Nezjištěno    |
| 3 | Zjištěno   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0 | Stav dodržování předpisů je neznámý|
| 1 |Odpovídající     |
| 2 |Neodpovídající     |
| 3 |Zjištěn konflikt    |
| 4 |Chyba      |
| 5 |Není známo     |
| 6 |Částečné dodržování předpisů   |
| 7 |Dodržování předpisů není nakonfigurované    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0  | Stav vynucení neznámý|
| 1  |Vynucení zahájeno          |
| 2  |Vynucení čeká na obsah         |
| 3  | Čeká se na dokončení jiné instalace.        |
| 4  |Čekání na časový interval pro správu a údržbu před instalací         |
| 5  |Před instalací je vyžadován restart.         |
| 6  |Obecná chyba        |
| 7  |Instalace čekající na vyřízení         |
| 8  |Instalace aktualizace          |
| 9  |Čeká se na restart systému.        |
| 10 |Úspěšná instalace aktualizace         |
| 11 |Nepovedlo se nainstalovat aktualizaci.        |
| 12 |Stahování aktualizace        |
| 13 | Stažená aktualizace        |
| 14 |Nepovedlo se stáhnout aktualizaci.        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
|0 |Neznámý stav detekce|
| 1 | Aktualizace není povinná.  |
| 2 | Aktualizace je povinná.   |
| 3 | Aktualizace je nainstalovaná.  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0 |Stav kontroly neznámý|
| 1 | Kontrola čeká na obsah.   |
| 2 | Probíhá kontrola.    |
| 3 | Kontrola dokončena    |
| 4 | Kontrola čeká na opakování.   |
| 5 | Kontrola se nezdařila   |
| 6 | Kontrola se dokončila s chybami. |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Žádná ID stavu

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Žádná ID stavu

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Žádná ID stavu

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 100 |Nasazení klienta bylo spuštěno.      |       
| 101 |Čeká se na stažení.       |       
| 102 |Naplánovaná nasazení       |       
| 103 | Čekání na okno před nasazením |
| 104 |Nasazení bylo přeskočeno.       |       
| 301 |Neznámá chyba při nasazování klienta |       
| 302 |Nepovedlo se vytvořit službu CCMSetup.  |       
| 303 |Nepovedlo se odstranit službu CCMSetup. |       
| 304 |Nejde nainstalovat přes Integrovaný operační systém se zapnutým FBWF (File-based Filter) na systémové jednotce. |       
| 305 |Nativní režim zabezpečení není platný v systému Windows 2000.  |       
| 306 |Nepovedlo se spustit proces stahování CCMSetup.  |       
| 307 |Neplatný příkazový řádek CCMSetup |       
| 308 |Nepovedlo se stáhnout soubor přes WINHTTP na adrese. |       
| 309 |Nepovedlo se stáhnout soubory pomocí BITS na adrese. |       
| 310 |Nepovedlo se nainstalovat verzi BITS. |       
| 311 |Nejde ověřit, jestli je požadovaný soubor podepsaný MS.  |       
| 312 |Kopírování souboru se nezdařilo, protože disk je plný. |       
| 313 |Instalace Client. msi se nepovedla kvůli chybě MSI. |       
| 314 |Nepodařilo se načíst soubor manifestu CCMSetup. XML. |       
| 315 |Nepovedlo se získat klientský certifikát.  |       
| 316 |Požadovaný soubor není podepsán od společnosti Microsoft. |       
| 317 |Aby bylo možné pokračovat v instalaci, je vyžadován restart.  |       
| 318 |Nelze nainstalovat klienta na MP, protože verze MP a klienta se neshodují. |       
| 319 |Operační systém nebo aktualizace Service Pack nejsou podporovány.  |       
| 320 |Nasazení se nepodporuje.       |       
| 321 |Chybějící bity        |       
| 322 |Zdrojová složka není k dispozici.       |       
| 323 |AppV není podporována              |       
| 324 |Nesprávná verze lokality              |       
| 325 |Neshoda hodnot hash požadavků       |       
| 326 |Neúspěšná registrace MDM      |       
| 327 |Zjistila se registrace MDM.      |       
| 328 |Zjistila se Intune.       |       
| 329 |Měřená síť není povolená.      |       
| 400 |Nasazení klienta se podařilo. |  
| 401 |Bylo vyžadováno restartování nasazení.     |       
| 402 |Nasazení bylo úspěšné, úspěšné restartování     |
| 500 |Přiřazení klienta bylo spuštěno.|
| 601 |Neznámá chyba přiřazení klienta|
| 602 |Následující kód lokality je neplatný.|
| 603 |Přiřazení k MP se nezdařilo.|
| 604 |Nepovedlo se zjistit výchozí bod správy.|
| 605 |Nepovedlo se stáhnout podpisový certifikát lokality.|
| 606 |Automatické zjištění kódu lokality se nezdařilo.|
| 607 |Nepovedlo se přiřadit lokalitu; verze klienta vyšší než verze lokality|
| 608 |Nepovedlo se získat verzi lokality z Active Directory Domain Services a SLP.|
| 609 |Nepovedlo se získat verzi klienta.|
| 700 |Přiřazení klienta bylo úspěšné.|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Žádná ID stavu

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 100 | Stav registrace   |
| 101 | Registrace naplánována   |
| 102 | Registrace zrušena   |
| 105 | Registrace zahájena   |
| 106 | Registrace byla úspěšná, ale není zřízená.
| 107 | Zápis byl úspěšný a byl zřízen
| 108 | Registrace – žádný aktivní uživatel   |
| 110 | Registrace se nezdařila   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 | Stav klienta web Windows Update pro firmy| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 | Místo na disku   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Žádná ID stavu

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Žádná ID stavu

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Žádná ID stavu

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 | Klient úspěšně komunikuje s bodem správy. |
| 2 | Klientovi se nepodařilo komunikovat s bodem správy. |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Klient úspěšně načetl certifikát z místního úložiště certifikátů.    |
| 2 |Klientovi se nepovedlo načíst certifikát z místního úložiště certifikátů. |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Žádná ID stavu

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Žádná ID stavu

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Žádná ID stavu

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Žádná ID stavu

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Žádná ID stavu

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Žádná ID stavu

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Žádná ID stavu

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Žádná ID stavu

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Žádná ID stavu

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Žádná ID stavu

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Žádná ID stavu

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Žádná ID stavu

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Žádná ID stavu

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Žádná ID stavu

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Klient není připraven pro nativní režim.  |
| 2 |Klient je připraven pro nativní režim.     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 | Úspěch|
| 2 | Neúspěšné |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Žádná ID stavu

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Žádná ID stavu

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Žádná ID stavu

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Žádná ID stavu 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Sada přidružení uživatele       |
| 2 |Přidružení uživatele se odebralo.       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Žádná ID stavu

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Žádná ID stavu

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1000  |Položka konfigurace byla úspěšná.           |
| 1001 |Položka konfigurace již byla úspěšně nainstalována.         |
| 1002 |Předběžná kontrola položky konfigurace byla úspěšná.          |
| 1003 |Rychlý stav položky konfigurace byl úspěšný.          |
| 2000 |Probíhá položka konfigurace           |
| 2001 |Probíhající položka konfigurace čeká na obsah.         |
| 2002 |Probíhá instalace položky konfigurace.          |
| 2003 |Probíhá čekání na restartování položky konfigurace.         |
| 2004 |Probíhající položka konfigurace čeká na časový interval pro správu a údržbu        |
| 2005 |Plán čeká na probíhající položku konfigurace         |
| 2006 |Probíhá stahování položky konfigurace závislého obsahu.     |
| 2007 |Probíhá instalace závislostí pro položku konfigurace        |
| 2008 |Probíhá čekání na restartování položky konfigurace.         |
| 2009 |Obsah probíhající položky konfigurace byl stažen         |
| 2010 |Probíhající aktualizace položky konfigurace         |
| 2011 |Položka konfigurace probíhá čekání na opětovné připojení uživatele        |
| 2012 |Právě probíhající položka konfigurace čeká na odhlášení uživatele.         |
| 2013 |Právě probíhající položka konfigurace čeká na přihlášení uživatele.         |
| 2014 |Probíhá čekání na instalaci položky konfigurace         |
| 2015 |Právě probíhající položka konfigurace čeká na opakování.         |
| 2016 |Probíhá čekání na presmode položky konfigurace         |
| 2017 |Probíhající položka konfigurace čeká na orchestraci.        |
| 2018 |Probíhající položka konfigurace čeká na síť.         |
| 2019 |Probíhající položka konfigurace čeká na aktualizaci VE stavu         |
| 2020 |Probíhá aktualizace položky konfigurace v.         |
| 3000 |Požadavky položky konfigurace nejsou splněné.           |
| 3001 |Požadavky na položku konfigurace nejsou splněné, hostitel se nedá použít.        |
| 4000 |Neznámá položka konfigurace           |
| 5000 |Chyba položky konfigurace            |
| 5001 |Chyba při vyhodnocování položky konfigurace          |
| 5002 |Chyba při instalaci položky konfigurace          |
| 5003 |Při načítání obsahu došlo k chybě položky konfigurace.         |
| 5004 |Chyba položky konfigurace při instalaci závislosti         |
| 5005 |Chyba položky konfigurace při načítání závislosti obsahu        |
| 5006 |Konflikt pravidel chyb položky konfigurace          |
| 5007 |Chyba položky konfigurace, která čeká na opakování          |
| 5008 |Chyba položky konfigurace při odinstalaci nahrazování        |
| 5009 |Chyba stahování položky konfigurace nahrazena         |
| 5010 |Chyba při aktualizaci položky konfigurace VE          |
| 5011 |Chyba při instalaci licence na položku konfigurace         |
| 5012 |Chyba při načítání položky konfigurace povolení všech důvěryhodných aplikací       |
| 5013 |Chyba položky konfigurace – nejsou k dispozici žádné licence         |
| 5014 |Chybový operační systém položky konfigurace není podporován.          |
| 6000 |Spuštění položky konfigurace bylo úspěšné.            |
| 6010 |Chyba při spuštění položky konfigurace            |
| 6020 |Neznámé spuštění položky konfigurace|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Žádná ID stavu

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Žádná ID stavu

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Žádná ID stavu

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Žádná ID stavu

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Žádná ID stavu

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Žádná ID stavu

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Žádná ID stavu

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Žádná ID stavu

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Nespravované Endpoint Protection   |
| 2 |Endpoint Protection čekání na instalaci  |
| 3 |Endpoint Protection spravované   |
| 4 |Instalace Endpoint Protection se nezdařila  |
| 5 |Endpoint Protection čeká na restartování  |
| 6 |Endpoint Protection se nepodporuje.   |
| 7 |Endpoint Protection spoluspravované   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0 |Neznámý stav aplikace zásad Endpoint Protection    |
| 1 |Aplikace zásad Endpoint Protection byla úspěšně dokončena.    |
| 2 |Nepovedlo se neúspěšná aplikace zásad Endpoint Protection    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 0 |  Není známo    |
| 1 |  Aktivní    |
| 2 |  Inactive    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 | Proxy probuzení není nainstalovaný.    |
| 2 | Proxy probuzení čeká na instalaci.   |
| 3 | Proxy probuzení je nainstalovaný.    |
| 4 | Instalace proxy probuzení se nezdařila   |
| 5 | Proxy probuzení čeká na restartování.   |
| 6 | Proxy probuzení není v tomto operačním systému podporované.  |
| 7 | Proxy server probuzení – odhlásit se   |
| 8 | Odinstalace proxy probuzení se nezdařila   |
| 9 | Běhový modul proxy probuzení se nepodporuje.   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Žádná ID stavu

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Žádná ID stavu

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Žádná ID stavu

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
|0 | Sada kanálů služby nabízených oznámení Windows|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Žádná ID stavu

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Žádná ID stavu

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Žádná ID stavu

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Žádná ID stavu

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Žádná ID stavu

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Žádná ID stavu

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Žádná ID stavu

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Žádná ID stavu

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Žádná ID stavu

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Žádná ID stavu

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Žádná ID stavu

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Žádná ID stavu

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Vydaná výzva         |
| 2 |Chyba výzvy se nezdařila        |
| 3 |Požadavek se nepovedlo vytvořit.        |
| 4 |Žádost se nepovedlo odeslat.        |
| 5 |Ověření výzvy bylo úspěšné.       |
| 6 |Chyba ověření výzvy       |
| 7 |Chyba         |
| 8 |Nevyřízená chyba         |
| 9 |Vydávání          |
| 10 |Zpracování odpovědi nebylo úspěšné.       |
| 11 |Čeká na odpověď         |
| 12 |Zápis byl úspěšný         |
| 13 |Registrace není nutná.         |
| 14 |Odvoláno          |
| 15 |Odebráno z kolekce        |
| 16 |Ověřeno obnovení         |
| 17 |Instalace se nezdařila        |
| 18 |Nainstalovaný         |
| 19 |Neúspěšné odstranění         |
| 20 |Odstranění         |
| 21 |Požadováno obnovení        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Vydaná výzva         |
| 2 |Chyba výzvy se nezdařila        |
| 3 |Požadavek se nepovedlo vytvořit.        |
| 4 |Žádost se nepovedlo odeslat.        |
| 5 |Ověření výzvy bylo úspěšné.       |
| 6 |Chyba ověření výzvy       |
| 7 |Chyba         |
| 8 |Nevyřízená chyba         |
| 9 |Vydávání          |
| 10 |Zpracování odpovědi nebylo úspěšné.       |
| 11 |Čeká na odpověď         |
| 12 |Zápis byl úspěšný         |
| 13 |Registrace není nutná.         |
| 14 |Odvoláno          |
| 15 |Odebráno z kolekce        |
| 16 |Ověřeno obnovení         |
| 17 |Instalace se nezdařila        |
| 18 |Nainstalovaný         |
| 19 |Neúspěšné odstranění         |
| 20 |Odstranění         |
| 21 |Požadováno obnovení        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 | Nastavení PIN kódu stavu bylo úspěšné.       |
| 2 | Nepovedlo se nastavit PIN kód stavu       |
| 3 | Instalace stavového kódu PIN není podporována.      |
| 4 | Probíhá nastavení kódu PIN pro stav      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Žádná ID stavu

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Žádná ID stavu

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Žádná ID stavu

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Žádná ID stavu

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Žádná ID stavu

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Žádná ID stavu

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Vydaná výzva    |
| 2 |Chyba výzvy se nezdařila   |
| 3 |Požadavek se nepovedlo vytvořit.   |
| 4 |Žádost se nepovedlo odeslat.   |
| 5 |Ověření výzvy bylo úspěšné.  |
| 6 |Chyba ověření výzvy  |
| 7 |Chyba    |
| 8 |Nevyřízená chyba    |
| 9 |Vydávání     |
| 10 |Zpracování odpovědi nebylo úspěšné.  |
| 11 |Čeká na odpověď    |
| 12 |Zápis byl úspěšný    |
| 13 |Registrace není nutná.    |
| 14 |Odvoláno     |
| 15 |Odebráno z kolekce   |
| 16 |Ověřeno obnovení    |
| 17 |Instalace se nezdařila   |
| 18 |Nainstalovaný    |
| 19 |Neúspěšné odstranění    |
| 20 |Odstranění    |
| 21 |Požadováno obnovení   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
|| 1 | Úspěch dodržování předpisů    |
| 2 | Neúspěšné dodržování předpisů v MP   |
| 3 | Neúspěšné dodržování předpisů u klienta   |
| 4 | Neúspěšné dodržování předpisů v Intune   |
| 5 | Neúspěšné dodržování předpisů v AAD   |
| 6 | Dodržování předpisů pro spolusprávu Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Přidal se zdroj sdílené mezipaměti.       |
| 2 |Zdroj sdílené mezipaměti se odebral.      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Zdroj sdílené mezipaměti byl deaktivován.       |
| 2 |Zdroj sdílené mezipaměti je aktivní.       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Stáhnout agregovaná nahrávání dat       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Nahrání dat odmítnutí zdroje partnerského zařízení     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Žádná ID stavu

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Žádná ID stavu

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Žádná ID stavu

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Žádná ID stavu

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID stavové zprávy     |  Popis zprávy o stavu |
|:-------------|:------|
| 1 |Ověření stavu je podporované.      |
| 2 |Ověření stavu se nepodporuje.      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Žádná ID stavu

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Žádná ID stavu

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Žádná ID stavu

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Žádná ID stavu

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Žádná ID stavu

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Žádná ID stavu

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Žádná ID stavu

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Žádná ID stavu

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Žádná ID stavu

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Žádná ID stavu

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Žádná ID stavu

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Žádná ID stavu

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Žádná ID stavu

## <a name="next-steps"></a>Další kroky

- [Popis zasílání zpráv o stavu v Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Dokument white paper pro správu aktualizací softwaru pro Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
