---
title: Shromažďování dat do datového skladu
titleSuffix: Microsoft Intune
description: Shromažďování dat do datového skladu Intune poskytuje podrobnosti týkající se rozhraní API datového skladu.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29f09230-dc56-43db-b599-d961967bda49
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0a9ecebd86404d4218142d1a3acb591974b027d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608090"
---
# <a name="intune-data-warehouse-collections"></a>Shromažďování dat do datového skladu

Následující shromažďování dat do datového skladu poskytuje vlastnosti, popisy a příklady pro kolekce v1.0 entit rozhraní API datového skladu. 

## <a name="apprevisions"></a>appRevisions
Entita **appRevision** obsahuje seznam všech verzí aplikací.

|          Vlastnost          |                                      Popis                                      |                Příklad               |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------|
| appKey                     | Jedinečný identifikátor aplikace                                                         | 123                                  |
| applicationId              | Jedinečný identifikátor aplikace – podobá se AppKey, ale tento klíč je přirozený.        | b66bc706-ffff-7437-0340-032819502773 |
| revision                   | Verze, kterou uvedl správce během nahrávání binárního souboru.                   | 2                                    |
| title                      | Název aplikace                                                                     | Excel                                |
| vydavatel                  | Vydavatel aplikace                                                                 | Partnerský vztah Microsoftu                            |
| uploadState                | Stav nahrávání aplikace                                                              | 1                                    |
| appTypeKey                 | Odkaz na entitu AppType, která je popsaná v následujícím oddílu.                            | 1                                    |
| vppProgramTypeKey          | Odkaz na entitu VppProgramType, která je popsaná níže.                                        | 30876                                |
| creationTime               | Čas vytvoření této revize                                            | 23. 11. 2016 0:00                      |
| modifiedTime               | Čas poslední změny nějakého prvku, který s touto revizí souvisí.                            | 23. 11. 2016 0:00                      |
| velikost                       | Velikost binárního souboru v bytech                                                          | 120 392 000                          |
| startDateInclusiveUTC      | Datum a čas ve standardu UTC, kdy se tato revize aplikace v datovém skladu vytvořila.      | 23. 11. 2016 0:00                      |
| endDateExclusiveUTC        | Datum a čas ve standardu UTC, od kdy je tato revize aplikace zastaralá                        | 23. 11. 2016 0:00                      |
| Aktuální                  | Určuje, jestli tato verze aplikace v datovém skladu je nebo není aktuální.         | Pravda/nepravda                           |
| rowLastModifiedDateTimeUTC | Datum a čas ve standardu UTC, kdy se tato verze aplikace v datovém skladu naposledy změnila. | 23. 11. 2016 0:00                      |

## <a name="apptypes"></a>appTypes
Entita **appType** obsahuje seznam zdrojů instalace aplikace.

|   Vlastnost  |        Popis        |
|-------------|---------------------------|
| appTypeID   | ID pro daný typ           |
| appTypeKey  | Náhradní klíč pro daný klíč |
| appTypeName | Typ aplikace                  |

### <a name="example"></a>Příklad

| AppTypeID |                Název               |                     Popis                     |
|-----------|-----------------------------------|-----------------------------------------------------|
| 0         | Aplikace z obchodu pro Android               | Aplikace z obchodu pro Android                             |
| 1         | Obchodní aplikace pro Android                 | Obchodní aplikace pro Android                  |
| 2         | Spravovaná aplikace z obchodu pro Android (MAM) | Aplikace z obchodu pro Android s povolenou správou |
| 3         | Aplikace z obchodu pro iOS                   | Aplikace z obchodu pro iOS                                 |
| 4         | Obchodní aplikace pro iOS                     | Obchodní aplikace pro iOS                      |
| 5         | Spravovaná aplikace obchodu pro iOS (MAM)     | Aplikace z obchodu pro iOS s povolenou správou       |
| 6         | Aplikace Microsoft 365 pro podniky        | Aplikace Microsoft 365 pro Windows 10     |
| 7         | Webová aplikace                         | Webová aplikace                                        |
| 8         | Aplikace pro Windows Phone 8.1 Store     | Aplikace pro Windows Phone 8.1 Store                    |
| 9         | Aplikace pro Windows Store               | Aplikace pro Windows Store                              |
| 10        | Obchodní aplikace pro Windows                | Obchodní aplikace Windows AppX              |
| 11        | Windows Mobile MSI              | Obchodní aplikace MSI                      |
| 12        | Obchodní aplikace pro Windows Phone           | Obchodní aplikace pro Windows Phone             |

## <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities
Následující tabulka shrnuje stav přiřazení zásad dodržování předpisů k zařízením. Uvádí počet zařízení nacházejících se v jednotlivých stavech shody.

|    Vlastnost   |                                                                                      Popis                                                                                     |  Příklad |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey       | Klíč data, kdy se vytvořil souhrn pro zásady dodržování předpisů.                                                                                                                   | 20161204 |
| Neznámý       | Počet zařízení, která jsou offline nebo kterým se nepodařilo komunikovat s Intune nebo Azure AD z jiných důvodů.                                                                           | 5        |
| notApplicable | Počet zařízení, ve kterých nejsou použitelné zásady dodržování předpisů, na které zacílil správce.                                                                                     | 201      |
| kompatibilní     | Počet zařízení, ve kterých se úspěšně použily jedny nebo více zásad dodržování předpisů, na které zacílil správce.                                                                        | 4083     |
| V období odkladu | Počet zařízení, která nevyhovují předpisům, ale jsou v období odkladu definovaném správcem.                                                                                  | 57       |
| nekompatibilních  | Počet zařízení, u kterých se nepodařilo použít jedny nebo více zásad dodržování předpisů, na které zacílil správce nebo u kterých uživatel nedodržel zásady, na které správce zacílil. | 43       |
|    error      |    Počet zařízení, kterým se nepodařilo komunikovat s Intune nebo Azure AD a která vrátila chybovou zprávu.                                                                          |    3     |

## <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities
Následující tabulka shrnuje stav přiřazení zásad dodržování předpisů k zařízením pro jednotlivé zásady a pro jednotlivé typy zásad. Uvádí počet zařízení nacházejících se v jednotlivých stavech shody pro všechny přiřazené zásady dodržování předpisů.

|      Vlastnost     |                                                                                      Popis                                                                                     |  Příklad |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey           | Klíč data, kdy se vytvořil souhrn pro zásady dodržování předpisů.                                                                                                                   | 20161219 |
| policyKey         | Klíč pro zásady dodržování předpisů, pro který se vytvořil souhrn.                                                                                                                   | 10178    |
| policyPlatformKey | Klíč pro typ platformy zásad dodržování předpisů, pro který se vytvořil souhrn.                                                                                            | 5        |
| Neznámý           | Počet zařízení, která jsou offline nebo kterým se nepodařilo komunikovat s Intune nebo Azure AD z jiných důvodů.                                                                           | 13       |
| notApplicable     | Počet zařízení, ve kterých nejsou použitelné zásady dodržování předpisů, na které zacílil správce.                                                                                     | 3        |
| kompatibilní         | Počet zařízení, ve kterých se úspěšně použily jedny nebo více zásad dodržování předpisů, na které zacílil správce.                                                                        | 45       |
| V období odkladu     | Počet zařízení, která nevyhovují předpisům, ale jsou v období odkladu definovaném správcem.                                                                                  | 3        |
| nekompatibilních      | Počet zařízení, u kterých se nepodařilo použít jedny nebo více zásad dodržování předpisů, na které zacílil správce nebo u kterých uživatel nedodržel zásady, na které správce zacílil. | 7        |
| error             | Počet zařízení, kterým se nepodařilo komunikovat s Intune nebo Azure AD a která vrátila chybovou zprávu.                                                                             | 3        |
## <a name="compliancestates"></a>complianceStates

|      Vlastnost      |                       Popis                      |
|--------------------|--------------------------------------------------------|
| complianceStatus   | Stav dodržování předpisů zařízení s klíčem mdmStatusKey       |
| complianceStateKey | Klíč dodržování předpisů, který odpovídá zařízení a stavu dodržování předpisů. |
| complianceStateID  | ID, které odpovídá tomuto stavu dodržování předpisů.                |

### <a name="example"></a>Příklad

|  complianceStatus  |                       Popis                      |
|--------------------|--------------------------------------------------------|
|    Neznámý         |    Neznámý                                                                        |
|    Odpovídající       |    Dodržuje předpisy.                                                                      |
|    Nevyhovuje    |       Zařízení nedodržuje předpisy a má zablokovaný přístup k podnikovým prostředkům.             |
|    Konflikt        |    Konflikt s jinými pravidly                                                      |
|    Chyba           |       Chyba                                                                       |
|    ConfigManager   |    Spravované nástrojem Configuration Manager                                                      |
|    V období odkladu   |       Zařízení nedodržuje předpisy, ale stále má přístup k podnikovým prostředkům.          |

## <a name="dates"></a>dates
Entita **date** zastupuje kalendářní data, na která odkazují různé entity datového skladu.

|     Vlastnost    |                       Popis                      |    Příklad    |
|-----------------|--------------------------------------------------------|---------------|
| dateKey         | Jedinečný identifikátor daného kalendářního data v datovém skladu. | 20160703      |
| fullDate        | Dané datum v úplném formátu data a času.        | 3. 7. 2016 0:00 |
| dayOfWeek       | Den týdne                                            | 1             |
| dayOfMonth      | Den měsíce                                           | 3             |
| dayOfYear       | Den roku                                            | 185           |
| weekOfYear      | Týden roku                                           | 28            |
| monthOfYear     | Měsíc roku                                      | 7             |
| calendarQuarter | Kalendářní čtvrtletí                                       | 3             |
| calendarYear    | Kalendářní rok                                          | 2016          |
| dateKey         | Jedinečný identifikátor daného kalendářního data v datovém skladu. | 20160703      |
| fullDate        | Dané datum v úplném formátu data a času.        | 3. 7. 2016 0:00 |
| dayOfWeek       | Den týdne                                            | 1             |
| dayOfMonth      | Den měsíce                                           | 3             |
| dayOfYear       | Den roku                                            | 185           |
| weekOfYear      | Týden roku                                           | 28            |
| monthOfYear     | Měsíc roku                                      | 7             |
| calendarQuarter | Kalendářní čtvrtletí                                       | 3             |
| calendarYear    | Kalendářní rok                                          | 2016          |

## <a name="devicecategories"></a>deviceCategories

|      Vlastnost      |                                    Popis                                   |                Příklad               |
|--------------------|----------------------------------------------------------------------------------|--------------------------------------|
| deviceCategoryID   | Jedinečný identifikátor kategorie zařízení                                       | fb415ba2-7c08-41f6-a5e5-685b50da2c4c |
| deviceCategoryKey  | Jedinečný identifikátor kategorie zařízení v datovém skladu – náhradní klíč | 1                                    |
| deviceCategoryName | Zobrazovaný název pro kategorii zařízení                                            | Chytré telefony                          |

## <a name="deviceconfigurationprofiledeviceactivities"></a>deviceConfigurationProfileDeviceActivities
Entita **DeviceConfigurationProfileDeviceActivity** obsahuje počet zařízení v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den. Číslo odráží konfigurační profily Zařízení přiřazené entitě. Pokud se například zařízení nachází v úspěšném stavu pro všechny své přiřazené zásady, zvýší čítač úspěšných zařízení pro daný den o jedno. Pokud má zařízení přiřazené dva profily, jeden je v úspěšném stavu a druhý v chybovém stavu, entita zvýší čítač úspěšných zařízení o jedno a umístí zařízení do chybového stavu. Entita uvádí, kolik zařízení je v jakém stavu v daném dni za posledních 30 dní.

|  Vlastnost |                                          Popis                                          |  Příklad |
|-----------|-----------------------------------------------------------------------------------------------|----------|
| dateKey   | Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo. | 20160703 |
| pending   | Počet jedinečných zařízení v čekajícím stavu                                                    | 123      |
| succeeded | Počet jedinečných zařízení v úspěšném stavu                                                    | 12       |
| error     | Počet jedinečných zařízení v chybovém stavu                                                      | 10       |
| failed    | Počet jedinečných zařízení v neúspěšném stavu                                                     | 2        |

## <a name="deviceconfigurationprofileuseractivities"></a>deviceConfigurationProfileUserActivities 
Entita **DeviceConfigurationProfileUserActivity** obsahuje počet uživatelů v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den. Číslo odráží konfigurační profily Zařízení přiřazené entitě. Pokud se například uživatel nachází v úspěšném stavu pro všechny své přiřazené zásady, posune čítač úspěšných uživatelů pro daný den o jedna nahoru. Pokud má uživatel přiřazené dva profily, jeden je v úspěšném stavu a druhý je v chybovém stavu, započítá se uživatel v chybovém stavu. Entita **DeviceConfigurationProfileUserActivity** uvádí, kolik uživatelů je v jakém stavu v daném dni za posledních 30 dní. 

| Vlastnost  | Popis  | Příklad  |
|------------|----------------------------------------------------------------------------------------------|-----------|
| dateKey  | Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo  | 20160703  |
| pending  | Počet jedinečných uživatelů v čekajícím stavu  | 123  |
| succeeded  | Počet jedinečných uživatelů v úspěšném stavu  | 12  |
| error  | Počet jedinečných uživatelů v chybovém stavu  | 10  |
| failed  | Počet jedinečných uživatelů v neúspěšném stavu  | 2  |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

|          Vlastnost          |                                                                                      Popis                                                                                     |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dateKey                    | Odkaz na tabulku kalendářních dat udávající den.                                                                                                                                          |
| deviceKey                  | Jedinečný identifikátor zařízení v datovém skladu – náhradní klíč Jedná se o odkaz na tabulku zařízení obsahující ID zařízení v Intune.                               |
| deviceName                 | Název zařízení na platformách, které umožňují pojmenování zařízení. Na ostatních platformách Intune vytvoří název z dalších vlastností. Tento atribut nemusí být dostupný pro všechna zařízení. |
| deviceRegistrationStateKey | Klíč atributu stavu registrace zařízení pro toto zařízení                                                                                                                    |
| ownerTypeKey               | Klíč atributu typu vlastníka pro toto zařízení: podnikový, osobní nebo neznámý                                                                                                  |
| managementStateKey         | Klíč stavu správy, který je přidružený k tomuto zařízení a který udává poslední stav vzdálené akce nebo informaci, jestli jde o zařízení s jailbreakem nebo rootem.                                                |
| azureADRegistered          | Udává, zda je zařízení zaregistrované v Azure Active Directory.                                                                                                                             |
| complianceStateKey         | Klíč k vlastnosti ComplianceState                                                                                                                                                            |
| oSVersion                  | Verze operačního systému.                                                                                                                                                                          |
| Jailbreak                 | Zda má zařízení jailbreak nebo root.                                                                                                                                         |
| deviceCategoryKey          | Klíč atributu kategorie zařízení pro toto zařízení                                                                                                                                    |
| physicalMemoryInBytes      | Fyzická paměť v bajtech.                                                                                                                                    |
| totalStorageSpaceInBytes      | Celková kapacita úložiště v bajtech                                                                                                                                    |


## <a name="deviceregistrationstates"></a>deviceRegistrationStates
Entita **DeviceRegistrationState** zastupuje typ registrace, na který odkazují jiné kolekce datového skladu. 

|           Vlastnost          |                                     Popis                                     |
|-----------------------------|-------------------------------------------------------------------------------------|
| deviceRegistrationStateID   | Jedinečný identifikátor stavu registrace                                            |
| deviceRegistrationStateKey  | Jedinečný identifikátor stavu registrace v datovém skladu – náhradní klíč |
| deviceRegistrationStateName | Stav registrace                                                                  |
|    notRegistered                     |    Nezaregistrováno                                                                                                                                                                  |
|    registrovat                        |       Registrované                                                                                                                                                                   |
|    odvolán                           |       Tento stav znamená, že správce IT daného klienta zablokoval a že je možné tohoto klienta odblokovat. Zařízení může mít také stav Odvoláno poté, co se vymaže nebo vyřadí z provozu.        |
|    Konflikt pro zprávy                       |    Konflikt klíčů                                                                                                                                                                    |
|    approvalPending                   |    Čekající schválení                                                                                                                                                                |
|    certificateReset                  |    Resetovat certifikát                                                                                                                                                               |
|    notRegisteredPendingEnrollment    |    Nezaregistrováno, nevyřízená registrace                                                                                                                                               |
|    Neznámý                           |    Neznámý stav                                                                                                                                                                   |

## <a name="devices"></a>zařízení
Entita **device** obsahuje seznam všech zaregistrovaných zařízení ve správě a jejich odpovídající vlastnosti.

|          Vlastnost          |                                                                                       Popis                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| deviceKey                  | Jedinečný identifikátor zařízení v datovém skladu – náhradní klíč                                                                                                               |
| deviceId                   | Jedinečný identifikátor zařízení                                                                                                                                                     |
| deviceName                 | Název zařízení na platformách, které umožňují pojmenování zařízení. Na ostatních platformách Intune vytvoří název z dalších vlastností. Tento atribut nemusí být dostupný pro všechna zařízení. |
| deviceTypeKey              | Klíč atributu typu zařízení pro toto zařízení                                                                                                                                    |
| deviceRegistrationState    | Klíč atributu stavu registrace klienta pro toto zařízení                                                                                                                      |
| ownerTypeKey               | Klíč atributu typu vlastníka pro toto zařízení: podnikový, osobní nebo neznámý                                                                                                    |
| enrolledDateTime           | Datum a čas, kdy se zařízení zaregistrovalo.                                                                                                                                         |
| ethernetMacAddress           | Jedinečný identifikátor sítě tohoto zařízení.                                                                                                                                         |
| lastSyncDateTime           | Poslední známé přihlášení zařízení k Intune.                                                                                                                                              |
| managementAgentKey         | Klíč agenta správy, který je k tomuto zařízení přidružený.                                                                                                                             |
| managementStateKey         | Klíč stavu správy, který je přidružený k tomuto zařízení a který udává poslední stav vzdálené akce nebo informaci, jestli jde o zařízení s jailbreakem nebo rootem.                                                |
| azureADDeviceId            | ID zařízení Azure pro toto zařízení                                                                                                                                                  |
| azureADRegistered          | Udává, zda je zařízení zaregistrované v Azure Active Directory.                                                                                                                             |
| deviceCategoryKey          | Klíč kategorie, která je k tomuto zařízení přidružená.                                                                                                                                     |
| deviceEnrollmentType       | Klíč typu registrace, který je přidružený k tomuto zařízení a který udává metodu registrace.                                                                                             |
| complianceStateKey         | Klíč stavu dodržování předpisů, který je k tomuto zařízení přidružený.                                                                                                                             |
| office365Version           | Verze Microsoft 365, která je na zařízení nainstalovaná.                                                                                                                             |
| oSVersion                  | Verze operačního systému v zařízení                                                                                                                                                |
| easDeviceId                | ID protokolu Exchange ActiveSync zařízení.                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Jedinečný identifikátor uživatele přidružený k zařízení                                                                                                                           |
| rowLastModifiedDateTimeUTC | Datum a čas ve standardu UTC, kdy se toto zařízení v datovém skladu naposledy změnilo.                                                                                                       |
| manufacturer               | Výrobce zařízení                                                                                                                                                             |
| model                      | Model zařízení                                                                                                                                                                    |
| operatingSystem            | Operační systém zařízení Windows, iOS/iPadOS atd.                                                                                                                                   |
| IsDeleted                  | Binární soubor zobrazující, zda se zařízení odstranilo nebo ne.                                                                                                                                 |
| androidSecurityPatchLevel  | Úroveň opravy zabezpečení Androidu                                                                                                                                                           |
| mEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Stav dohledu zařízení                                                                                                                                                               |
| freeStorageSpaceInBytes    | Volné úložiště v bajtech                                                                                                                                                                 |
| encryptionState            | Stav šifrování zařízení                                                                                                                                                      |
| subscriberCarrier          | Poskytovatel předplatného na zařízení                                                                                                                                                       |
| phoneNumber                | Telefonní číslo zařízení                                                                                                                                                             |
| iMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Mobilní technologie zařízení.                                                                                                                                                    |
| wiFiMacAddress             | Síť MAC Wi-Fi.                                                                                                                                                                              |
| windowsOsEdition             | Edice operačního systému Windows.                                                                                                                                                                              |


## <a name="devicetypes"></a>deviceTypes
Entita **deviceType** zastupuje typ zařízení, na který odkazují jiné entity datového skladu. Typ zařízení obvykle popisuje model zařízení, výrobce nebo kombinaci obou těchto možností.

|    Vlastnost    |                                  Popis                                 |
|----------------|------------------------------------------------------------------------------|
| deviceTypeID   | Jedinečný identifikátor typu zařízení                                       |
| deviceTypeKey  | Jedinečný identifikátor typu zařízení v datovém skladu – náhradní klíč |
| deviceTypeName | Typ zařízení                                                                |

### <a name="example"></a>Příklad

| deviceTypeID |        Název       |                      Popis                      |
|--------------|-------------------|-------------------------------------------------------|
| -1           | Není k dispozici   | Tento typ zařízení není k dispozici.                     |
| 0            | Aplikace klasické pracovní plochy           | Zařízení se systémem Windows                              |
| 1            | Windows           | Zařízení s Windows                                      |
| 2            | WinMO6            | Zařízení se systémem Windows Mobile 6.0                           |
| 3            | Nokia             | Zařízení Nokia                                        |
| 4            | WindowsPhone      | Zařízení Windows Phone                                |
| 5            | Mac               | Zařízení Mac                                          |
| 6            | WinCE             | Zařízení se systémem Windows CE                                   |
| 7            | WinEmbedded       | Zařízení se systémem Windows Embedded                             |
| 8            | IPhone            | Zařízení iPhone                                       |
| 9            | IPad              | Zařízení iPad                                         |
| 10           | IPod              | Zařízení iPod                                         |
| 11           | Android           | Zařízení Android spravované pomocí Správce zařízení   |
| 12           | ISocConsumer      | Zařízení iSoc Consumer                                |
| 13           | Unix              | Zařízení se systémem Unix                                         |
| 14           | MacMDM            | Zařízení OS X spravované pomocí integrovaného agenta MDM |
| 15           | HoloLens          | Zařízení HoloLens                                       |
| 16           | SurfaceHub        | Zařízení Surface Hub                                  |
| 17           | AndroidForWork    | Zařízení Android spravované pomocí vlastníka profilu Androidu  |
| 18           | AndroidEnterprise | Zařízení s Androidem Enterprise                          |
| 100          | Blackberry        | Zařízení Blackberry                                   |
| 101          | Palm              | Zařízení Palm                                         |
| 255          | Neznámý           | Neznámý typ zařízení                                 |

## <a name="deviceenrollmenttypes"></a>deviceEnrollmentTypes
Entita **deviceEnrollmentType** určuje, jak se zařízení zaregistrovalo. Typ registrace zaznamenává metodu registrace. Příklady ukazují různé typy registrace a jejich význam.

|         Vlastnost         |                                    Popis                                    |
|--------------------------|-----------------------------------------------------------------------------------|
| deviceEnrollmentTypeID   | Jedinečný identifikátor typu registrace                                       |
| deviceEnrollmentTypeKey  | Jedinečný identifikátor typu registrace v datovém skladu – náhradní klíč |
| deviceEnrollmentTypeName | Název typu registrace                                                           |

### <a name="example"></a>Příklad

| enrollmentTypeID |                Název                |                                        Popis                                       |
|------------------|------------------------------------|------------------------------------------------------------------------------------------|
| 0                | Neznámý                            | Typ registrace se neshromáždil.                                                      |
| 1                | UserEnrollment                     | Registrace řízená uživatelem prostřednictvím kanálu uživatelé s vlastním zařízením (BYOD)                                           |
| 2                | DeviceEnrollmentManager            | Registrace uživatele pomocí účtu správce registrace zařízení                              |
| 3                | AppleBulkWithUser                  | Hromadná registrace Apple s uživatelskou výzvou (DEP, Apple Configurator)                   |
| 4                | AppleBulkWithoutUser               | Hromadná registrace Apple bez uživatelské výzvy   (DEP, Apple Configurator, Mobile Config) |
| 5                | WindowsAzureADJoin                 | Připojení k Azure AD s Windows 10                                                                |
| 6                | WindowsBulkUserless                | Hromadná registrace Windows 10 prostřednictvím nástroje ICD s certifikátem                               |
| 7                | WindowsAutoEnrollment              | Automatická registrace Windows 10   (Přidání pracovního účtu)                                    |
| 8                | WindowsBulkAzureDomainJoin         | Hromadné připojení k Azure AD s Windows 10                                                           |
| 9                | WindowsCoManagement                | Spoluspráva Windows 10 aktivovaná autopilotem nebo Zásady skupiny.                       |
| 10               | WindowsAzureADJoinsUsingDeviceAuth | Připojení k Azure AD pomocí Device Auth ve Windows 10                                            |

## <a name="enrollmentactivities"></a>enrollmentActivities 
Entita **EnrollmentActivity** označuje aktivitu registrace zařízení.

| Vlastnost                      | Popis                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Klíč data, kdy se tato aktivita registrace nahrála.               |
| deviceEnrollmentTypeKey       | Klíč typu registrace.                                        |
| deviceTypeKey                 | Klíč typu zařízení                                                |
| enrollmentEventStatusKey      | Klíč stavu indikující úspěch nebo neúspěch registrace.    |
| enrollmentFailureCategoryKey  | Klíč kategorie selhání registrace (Pokud se registrace nezdařila)        |
| enrollmentFailureReasonKey    | Klíč důvodu selhání registrace (Pokud se registrace nezdařila)          |
| osVersion                     | Verze operačního systému zařízení.                               |
| count                         | Celkový počet aktivit registrace, které odpovídají klasifikacím uvedeným výše.  |

## <a name="enrollmenteventstatuses"></a>enrollmentEventStatuses 
Entita **EnrollmentEventStatus** indikuje výsledek registrace zařízení.

| Vlastnost                   | Popis                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | Jedinečný identifikátor stavu registrace v datovém skladu (náhradní klíč)  |
| enrollmentEventStatusName  | Název stavu registrace. Podívejte se na následující příklady:                            |

### <a name="example"></a>Příklad

| enrollmentEventStatusName  | Popis                            |
|----------------------------|----------------------------------------|
| Success                    | Úspěšná registrace zařízení         |
| Neúspěšný                     | Neúspěšná registrace zařízení             |
| Není k dispozici              | Stav registrace není k dispozici.  |

## <a name="enrollmentfailurecategories"></a>enrollmentFailureCategories 
Entita **EnrollmentFailureCategory** indikuje, proč se registrace zařízení nezdařila. 

| Vlastnost                       | Popis                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| enrollmentFailureCategoryKey   | Jedinečný identifikátor kategorie selhání registrace v datovém skladu (náhradní klíč)  |
| enrollmentFailureCategoryName  | Název kategorie selhání registrace. Podívejte se na následující příklady:                            |

### <a name="example"></a>Příklad

| enrollmentFailureCategoryName   | Popis                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Neuvedeno                  | Kategorie selhání registrace se nedá použít.                                                            |
| Není k dispozici                   | Kategorie selhání registrace není k dispozici.                                                             |
| Neznámý                         | Neznámou chybu.                                                                                                |
| Authentication                  | Ověření se nezdařilo.                                                                                        |
| Autorizace                   | Volání bylo ověřeno, ale není autorizováno k registraci.                                                         |
| AccountValidation               | Nepovedlo se ověřit účet pro registraci. (Účet zablokován, registrace není povolená.)                      |
| UserValidation                  | Uživatele nelze ověřit. (Uživatel neexistuje, chybí licence)                                           |
| DeviceNotSupported              | Zařízení není podporováno pro správu mobilních zařízení.                                                         |
| Inúdržba                   | Účet je v údržbě.                                                                                    |
| Důvodu chybného požadavku                      | Klient odeslal požadavek, který služba nerozpoznala nebo nepodporovala.                                        |
| FeatureNotSupported             | Funkce používané tímto zápisem nejsou pro tento účet podporovány.                                        |
| EnrollmentRestrictionsEnforced  | Omezení registrace nakonfigurovaná správcem zablokovala tuto registraci.                                          |
| ClientDisconnected              | Vypršel časový limit klienta nebo byl zápis přerušen koncovým uživatelem.                                                        |
| UserAbandonment                 | Zápis byl opuštěn koncovým uživatelem. (Koncový uživatel zahájil registraci, ale nedokázal ho dokončit včas)  |

## <a name="enrollmentfailurereasons"></a>enrollmentFailureReasons  
Entita **EnrollmentFailureReason** označuje podrobnější důvod selhání registrace zařízení v dané kategorii selhání.  

| Vlastnost                     | Popis                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| enrollmentFailureReasonKey   | Jedinečný identifikátor důvodu selhání registrace v datovém skladu (náhradní klíč)  |
| enrollmentFailureReasonName  | Název důvodu selhání registrace. Podívejte se na následující příklady:                            |

### <a name="example"></a>Příklad

| enrollmentFailureReasonName      | Popis                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Neuvedeno                   | Důvod selhání registrace se nedá použít.                                                                                                                                                       |
| Není k dispozici                    | Důvod selhání registrace není k dispozici.                                                                                                                                                        |
| Neznámý                          | Neznámá chyba.                                                                                                                                                                                         |
| UserNotLicensed                  | Uživatel se v Intune nenašel nebo nemá platnou licenci.                                                                                                                                     |
| UserUnknown                      | Intune nezná uživatele.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Zařízení může zaregistrovat jenom jeden uživatel. Toto zařízení dřív zaregistroval jiný uživatel.                                                                                                                |
| EnrollmentOnboardingIssue        | Autorita správy mobilních zařízení (MDM) Intune ještě není nakonfigurovaná.                                                                                                                                 |
| AppleChallengeIssue              | Instalace profilu správy iOS byla zpožděna nebo se nezdařila.                                                                                                                                         |
| AppleOnboardingIssue             | K registraci do Intune se vyžaduje certifikát Apple MDM push Certificate.                                                                                                                                       |
| DeviceCap                        | Uživatel se pokusil zaregistrovat více zařízení, než je povolené maximum.                                                                                                                                        |
| AuthenticationRequirementNotMet  | Službě registrace v Intune se nepovedlo autorizovat tuto žádost.                                                                                                                                            |
| UnsupportedDeviceType            | Toto zařízení nesplňuje minimální požadavky na registraci v Intune.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | Registrace tohoto zařízení se nepovedla kvůli nakonfigurovanému pravidlu omezení registrace.                                                                                                                          |
| BulkDeviceNotPreregistered       | Nenašlo se číslo IMEI (International Mobile Equipment Identifier) tohoto zařízení.  Bez tohoto identifikátoru se zařízení rozpoznávají jako zařízení, která jsou v tuto chvíli zablokovaná.  |
| FeatureNotSupported              | Uživatel se pokusil o přístup k funkci, která ještě není vydaná pro všechny zákazníky nebo není kompatibilní s vaší konfigurací Intune.                                                            |
| UserAbandonment                  | Zápis byl opuštěn koncovým uživatelem. (Koncový uživatel zahájil registraci, ale nedokázal ho dokončit včas)                                                                                           |
| APNSCertificateExpired           | Zařízení Apple se nedají spravovat pomocí certifikátu Apple MDM push Certificate s vypršenou platností.                                                                                                                            |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions
**IntuneManagementExtension** uvádí seznam stavů **intuneManagementExtension** na jednotlivých zařízeních s Windows 10 za den. Uchovávají se data za posledních 60 dní.

|       Vlastnost      |                          Popis                          | Příklad |
|---------------------|---------------------------------------------------------------|---------|
| dateKey             | Jedinečný identifikátor data                                | 123     |
| tenantKey           | Jedinečný identifikátor tenanta                              | 456     |
| deviceKey           | Jedinečný identifikátor zařízení                              | 789     |
| extensionVersionKey | Jedinečný identifikátor verze IntuneManagementExtension | 1       |
| extensionStateKey   | Jedinečný identifikátor stavu                            | 2       |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates
**IntuneManagementExtensionHealthState** uvádí seznam všech možných stavů **IntuneManagementExtension**.

|      Vlastnost     |                   Popis                  | Příklad |
|-------------------|------------------------------------------------|---------|
| extensionStateKey | Jedinečný identifikátor stavu           | 2       |
| extensionState    | Stav IntuneManagementExtension | V pořádku |

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions
Entita **IntuneManagementExtensionVersion** uvádí seznam všech verzí, které **IntuneManagementExtension** používá.

|       Vlastnost      |                          Popis                          | Příklad |
|---------------------|---------------------------------------------------------------|---------|
| extensionVersionKey | Jedinečný identifikátor verze IntuneManagementExtension | 1       |
| extensionVersion    | Číslo verze tvořené 4 číslicemi                                   | 1.0.2.0 |

## <a name="mamapplications"></a>MamApplications

Entita **MamApplication** obsahuje seznam obchodních aplikací, které jsou spravované přes správu mobilních aplikací (MAM) bez registrace ve vašem podniku.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| mamApplicationKey |Jedinečný identifikátor aplikace MAM | 432 |
| mamApplicationName |Název aplikace MAM |Příklad názvu aplikace MAM |
| mamApplicationId |ID aplikace MAM | 123 |
| IsDeleted |Určuje, jestli je tento záznam aplikace MAM aktualizovaný. <br>True – aplikace MAM má v této tabulce nový záznam s aktualizovanými poli. <br>False – jedná se o nejnovější záznam pro tuto aplikaci MAM. |Pravda/nepravda |
| startDateInclusiveUTC |Datum a čas ve standardu UTC, kdy se tato aplikace MAM v datovém skladu vytvořila |23.11.2016 12:00:00 |
| deletedDateUTC |Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True |23.11.2016 12:00:00 |
| rowLastModifiedDateTimeUTC |Datum a čas ve standardu UTC, kdy se tato aplikace MAM v datovém skladu naposledy změnila |23.11.2016 12:00:00 |


## <a name="mamapplicationinstances"></a>MamApplicationInstances

Entita **MamApplicationInstance** obsahuje seznam aplikací spravovaných přes správu mobilních aplikací (MAM) jako jedinečné instance pro uživatele a zařízení. Všichni uživatelé a zařízení, kteří jsou v této entitě uvedení, jsou chránění, protože mají přiřazenou aspoň jednu zásadu MAM.


|          Vlastnost          |                                                                                                  Popis                                                                                                  |               Příklad                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   Vlastnosti applicationinstancekey   |                                                               Jedinečný identifikátor instance aplikace MAM v datovém skladu – náhradní klíč                                                                |                 123                  |
|           userId           |                                                                              ID uživatele, který má tuto aplikaci MAM nainstalovanou.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              Jedinečný identifikátor instance aplikace MAM – podobá se vlastnosti ApplicationInstanceKey, ale tento identifikátor představuje přirozený klíč.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | ID aplikace mam, pro kterou se vytvořila tato instance aplikace mam   | 23.11.2016 12:00:00   |
|     applicationVersion     |                                                                                     Verze aplikace pro danou aplikaci MAM                                                                                      |                  2                   |
|        createdDate         |                                                                 Datum vytvoření daného záznamu instance aplikace MAM Hodnota může být null.                                                                 |        23.11.2016 12:00:00        |
|          platforma          |                                                                          Platforma zařízení, na kterém je daná aplikace MAM nainstalovaná                                                                           |                  2                   |
|      platformVersion       |                                                                      Verze platformy zařízení, na kterém je daná aplikace MAM nainstalovaná                                                                       |                 2,2                  |
|         sdkVersion         |                                                                            Verze sady SDK MAM, pomocí které byla daná aplikace MAM zabalena                                                                            |                 3.2                  |
| mamDeviceId | ID zařízení, ke kterému je přidružená instance aplikace MAM   | 23.11.2016 12:00:00   |
| mamDeviceType | Typ zařízení, ke kterému je přidružená instance aplikace MAM   | 23.11.2016 12:00:00   |
| mamDeviceName | Název zařízení, ke kterému je přidružená instance aplikace MAM   | 23.11.2016 12:00:00   |
|         IsDeleted          | Určuje, jestli je tento záznam instance aplikace MAM aktualizovaný. <br>True – tato instance aplikace MAM má v této tabulce nový záznam s aktualizovanými poli. <br>False – jedná se o nejnovější záznam pro tuto instanci aplikace MAM. |              Pravda/nepravda              |
|   startDateInclusiveUtc    |                                                              Datum a čas ve standardu UTC, kdy se tato instance aplikace MAM v datovém skladu vytvořila                                                               |        23.11.2016 12:00:00        |
|       deletedDateUtc       |                                                                             Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True                                                                              |        23.11.2016 12:00:00        |
| rowLastModifiedDateTimeUtc |                                                           Datum a čas ve standardu UTC, kdy se tato instance aplikace MAM v datovém skladu naposledy změnila                                                            |        23.11.2016 12:00:00        |

## <a name="mamcheckins"></a>MamCheckins

Entita **MamCheckin** představuje data shromážděná v době, kdy se instance aplikace MAM přihlásila ke službě Intune. 

> [!Note]  
> Pokud se instance aplikace přihlásí několikrát denně, uloží se to v datovém skladu jako jediné přihlášení.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| dateKey |Klíč data, kdy se přihlášení aplikace MAM v datovém skladu zaznamenalo | 20160703 |
| Vlastnosti applicationinstancekey |Klíč instance aplikace, který je k tomuto přihlášení aplikace MAM přidružený | 123 |
| userKey |Klíč uživatele, který je k tomuto přihlášení aplikace MAM přidružený | 4323 |
| mamApplicationKey |Aplikační klíč aplikace přidružený k vrácení aplikace MAM se změnami | 432 |
| Vlastnosti devicehealthkey |Klíč pro stav, který je k tomuto přihlášení aplikace MAM přidružený | 321 |
| Vlastnosti platformkey |Představuje platformu zařízení, které je k tomuto přihlášení aplikace MAM přidružené |123 |
| lastCheckInDate |Datum a čas posledního přihlášení dané aplikace MAM Hodnota může být null. |23.11.2016 12:00:00 |

## <a name="mamdevicehealths"></a>MamDeviceHealths

Entita **MamDeviceHealth** představuje zařízení, na kterých jsou nasazené zásady správy mobilních aplikací (MAM), i když jsou tato zařízení s jailbreakem.

| Vlastnost | Popis | Příklad |
|---------|------------|--------|
| Vlastnosti devicehealthkey |Jedinečný identifikátor zařízení a jeho přidruženého stavu v datovém skladu – náhradní klíč |123 |
| Přidružený |Jedinečný identifikátor zařízení a jeho přidruženého stavu – podobá se vlastnosti DeviceHealthKey, ale tento identifikátor představuje přirozený klíč. |b66bc706-FFFF-7777-0340-032819502773 |
| deviceHealthName |Představuje stav zařízení. <br>Není k dispozici – žádné informace o tomto zařízení nejsou dostupné. <br>V pořádku – nejedná se o zařízení s jailbreakem. <br>Není v pořádku – jedná se o zařízení s jailbreakem. |Není k dispozici, V pořádku, Není v pořádku |
| rowLastModifiedDateTimeUtc |Datum a čas ve standardu UTC, kdy se tento konkrétní stav zařízení MAM v datovém skladu naposledy změnil |23.11.2016 12:00:00 |

## <a name="mamplatforms"></a>MamPlatforms

Entita **MamPlatform** obsahuje seznam názvů a typů platforem, na kterých byla aplikace MAM nainstalována.


|          Vlastnost          |                                    Popis                                    |                         Příklad                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        Vlastnosti platformkey         |     Jedinečný identifikátor platformy v datovém skladu – náhradní klíč      |                           123                           |
|          platforma          | Jedinečný identifikátor platformy – podobá se vlastnosti PlatformKey, jedná se ale o přirozený klíč. |                           123                           |
|        platformName        |                                   Název platformy                                   | Není k dispozici <br>Žádné <br>Windows <br>iOS <br>Android. |
| rowLastModifiedDateTimeUtc | Datum a čas ve standardu UTC, kdy se tato platforma v datovém skladu naposledy změnila  |                 23.11.2016 12:00:00                  |

## <a name="managementagenttypes"></a>managementAgentTypes
Entita **managementAgentType** představuje agenty používané ke správě zařízení.

|         Vlastnost        |                                       Popis                                       |
|-------------------------|-----------------------------------------------------------------------------------------|
| managementAgentTypeID   | Jedinečný identifikátor typu agenta správy.                                         |
| managementAgentTypeKey  | Jedinečný identifikátor typu agenta správy v datovém skladu – náhradní klíč |
| managementAgentTypeName | Určuje typ agenta, který se používá ke správě zařízení.                              |

### <a name="example"></a>Příklad

| ManagementAgentTypeID |                Název               |                                  Popis                                 |
|-----------------------|-----------------------------------|------------------------------------------------------------------------------|
| 1                     | EAS                               | Zařízení se spravuje prostřednictvím protokolu Exchange Active Sync.                         |
| 2                     | MDM                               | Zařízení se spravuje pomocí agenta MDM.                                   |
| 3                     | EasMdm                            | Zařízení se spravuje pomocí protokolu Exchange Active Sync i pomocí agenta MDM.        |
| 4                     | IntuneClient                      | Zařízení se spravuje pomocí agenta Intune pro počítače.                               |
| 5                     | EasIntuneClient                   | Zařízení se spravuje pomocí protokolu Exchange Active Sync i pomocí agenta Intune pro počítače. |
| 8                     | ConfigManagerClient               | Zařízení spravuje agent Configuration Manager.     |
| 10                    | ConfigurationManagerClientMdm     | Zařízení se spravuje pomocí Configuration Manageru a MDM.                    |
| 11                    | ConfigurationManagerCLientMdmEas  | Zařízení se spravuje pomocí Configuration Manager, MDM a Exchange Active Sync.               |
| 16                    | Neznámý                           | Neznámý typ agenta správy                                              |
| 32                    | Jamf                              | Atributy zařízení se načítají z Jamf.                               |
| 64                    | GoogleCloudDevicePolicyController |  Zařízení se spravuje přes CloudDPC Googlu.                                 |

## <a name="managementstates"></a>managementStates
Entita **ManagementState** poskytuje podrobné informace o stavu daného zařízení. Podrobnosti můžou být užitečné v případech, kdy se používají vzdálené akce, nebo pokud jde o zařízení s jailbreakem nebo rootem.

|       Vlastnost      |                                     Popis                                    |
|---------------------|------------------------------------------------------------------------------------|
| managementStateID   | Jedinečný identifikátor stavu správy                                       |
| managementStateKey  | Jedinečný identifikátor stavu správy v datovém skladu – náhradní klíč |
| managementStateName | Určuje stav vzdálené akce použité pro toto zařízení.                 |

### <a name="example"></a>Příklad

| managementStateID |      Název      |                                                   Popis                                                   |
|-------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| 0                 | Spravované        | Spravováno bez čekajících vzdálených akcí                                                                       |
| 1                 | RetirePending  | Pro toto zařízení existuje příkaz pro vyřazení z provozu, který čeká na vyřízení.                                                             |
| 2                 | RetireFailed   | Příkaz pro vyřazení z provozu u tohoto zařízení selhal.                                                                      |
| 3                 | WipePending    | Pro toto zařízení existuje příkaz pro vymazání, který čeká na vyřízení.                                                               |
| 4                 | WipeFailed     | Příkaz pro vymazání u tohoto zařízení selhal.                                                                        |
| 5                 | Není v pořádku      | Stav Není v pořádku                                                                                              |
| 6                 | DeletePending  | Pro toto zařízení existuje příkaz pro odstranění, který čeká na vyřízení.                                                             |
| 7                 | RetireIssued   | Pro toto zařízení se vystavil příkaz pro vyřazení z provozu.                                                               |
| 8                 | WipeIssued     | Příkaz pro vymazání se vystavil.                                                                               |
| 9                 | WipeCanceled   | Příkaz pro vymazání se zrušil.                                                                               |
| 10                | RetireCanceled | Příkaz pro vyřazení z provozu se zrušil.                                                                             |
| 11                | Zjištěno     | Zařízení je v Intune nově zjištěné, po prvním přihlášení přejde do stavu Spravováno. |

## <a name="mobileappinstallstates"></a>mobileAppInstallStates
Entita MobileAppInstallState představuje stav instalace mobilní aplikace po jejím přiřazení do skupiny obsahující zařízení, uživatele, nebo obě tyto možnosti.

|       Vlastnost      |                        Popis                       |
|---------------------|----------------------------------------------------------|
| appInstallStateKey  | Jedinečné ID stavu instalace aplikace pro váš účet |
| appInstallState     | Hodnota výčtu stavu instalace aplikace                     |
| appInstallStateName | Název stavu instalace aplikace                           |

## <a name="mobileappinstallstatuscounts"></a>mobileAppInstallStatusCounts
Představuje stav instalace mobilní aplikace pomocí správy mobilních aplikací pro daný typ cílového zařízení prostřednictvím Microsoft Intune.

|      Vlastnost      |                                                          Popis                                                          |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| dateKey            | Klíč data záznamu stavu instalace aplikace                                                                     |
| appKey             | Klíč mobilní aplikace, který se používá k identifikaci instance AppRevision.                                                          |
| deviceTypeKey      | Klíč typu zařízení přidruženého k mobilní aplikaci                                                              |
| appInstallStateKey | Klíč stavu instalace aplikace, který se používá k identifikaci instance MobileAppInstallState.                                         |
| errorCode          | Kód chyby, který vrací instalační program aplikace, mobilní platforma nebo služba, které se instalace aplikace týká. |
| count              | Celkový počet                                                                                                                  |

## <a name="ownertypes"></a>ownerTypes
Entita **ownerType** určuje, jestli je zařízení firemní, v osobním vlastnictví nebo neznámé.

|    Vlastnost   |                                                                                     Popis                                                                                    |           Příklad          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| ownerTypeID   | Jedinečný identifikátor typu vlastníka.                                                                                                                                               |                            |
| ownerTypeKey  | Jedinečný identifikátor typu vlastníka v datovém skladu – náhradní klíč                                                                                                       |                            |
| ownerTypeName | Představuje typ vlastníka zařízení: podniková zařízení jsou vlastněná podnikem.  Osobní – zařízení je v osobním vlastnictví (BYOD).   Neznámé – žádné informace o tomto zařízení nejsou dostupné. | Firemní osobní neznámý |

> [!Note]  
> Pro `ownerTypeName` Filtr v AzureAD při vytváření dynamických skupin pro zařízení je potřeba nastavit hodnotu `deviceOwnership` jako `Company` . Další informace najdete v tématu [pravidla pro zařízení](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="policies"></a>Zásady
Entita **Policy** obsahuje seznam konfiguračních profilů zařízení, konfiguračních profilů aplikací a zásady dodržování předpisů. Zásady se správou mobilních zařízení (MDM) můžete přiřadit skupině ve vašem podniku.

|          Vlastnost          |                                                                       Popis                                                                      |                Příklad               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| policyKey                  | Jedinečný klíč reprezentující zásady v datovém skladu                                                                                              | 123                                  |
| policyId                   | Jedinečný identifikátor zásad v datovém skladu                                                                                                 | b66bc706-ffff-7437-0340-032819502773 |
| policyName                 | Název zásad                                                                                                                                    | „Směrný plán Windows 10“                |
| policyVersion              | Verze zásad Když dojde k úpravě nebo změně zásad, vytvoří se novější verze.                                                             | 1, 2, 3                              |
| IsDeleted                  | Určuje, jestli je záznam zásad aktualizovaný.  True – zásada má nový záznam s aktualizovanými poli.  False – jedná se o nejnovější záznam pro zásady. | Pravda/nepravda                           |
| startDateInclusiveUTC      | Datum a čas ve standardu UTC, kdy se tyto zásady v datovém skladu vytvořily.                                                                              | 23. 11. 2016 0:00                      |
| deletedDateUTC             | Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True                                                                                                   | 23. 11. 2016 0:00                      |
| rowLastModifiedDateTimeUTC | Datum a čas ve standardu UTC, kdy se tyto zásady v datovém skladu naposledy změnily.                                                                        | 23. 11. 2016 0:00                      |

## <a name="policydeviceactivities"></a>policyDeviceActivities
Následující tabulka uvádí počet zařízení v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den. Číslo odráží data pro jednotlivé profily typu zásad. Pokud se například zařízení nachází v úspěšném stavu pro všechny své přiřazené zásady, zvýší čítač úspěšných zařízení pro daný den o jedno. Pokud má zařízení přiřazené dva profily, jeden je v úspěšném stavu a druhý v chybovém stavu, entita zvýší čítač úspěšných zařízení o jedno a umístí zařízení do chybového stavu. Entita **policyDeviceActivity** uvádí, kolik zařízení je v jakém stavu v daném dni za posledních 30 dní.

|  Vlastnost |                                           Popis                                           |        Příklad        |
|-----------|-------------------------------------------------------------------------------------------------|-----------------------|
| dateKey   | Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo. | 20160703              |
| pending   | Počet jedinečných zařízení v čekajícím stavu                                                    | 123                   |
| succeeded | Počet jedinečných zařízení v úspěšném stavu                                                    | 12                    |
| policyKey | Klíč zásad, který jde připojit k zásadám a získat tak název zásad.                                  | Směrný plán Windows 10 |
| error     | Počet jedinečných zařízení v chybovém stavu                                                      | 10                    |
| failed    | Počet jedinečných zařízení v neúspěšném stavu                                                     | 2                     |

## <a name="policyplatformtypes"></a>policyPlatformTypes

|        Vlastnost        |                      Popis                      |     Příklad    |
|------------------------|-------------------------------------------------------|----------------|
| policyPlatformTypeKey  | Jedinečný klíč pro typ platformy zásad        | 20170519       |
| policyPlatformTypeId   | Jedinečný identifikátor pro typ platformy zásad | 1              |
| policyPlatformTypeName | Název typu platformy zásad              | AndroidForWork |

## <a name="policytypeactivities"></a>policyTypeActivities
Entita **PolicyTypeActivity** obsahuje kumulativní počet zařízení v úspěšném, čekajícím, neúspěšném nebo chybovém stavu. Zobrazí tyto stavy s ohledem na konfigurační profil zařízení, konfigurační profil aplikace nebo zásady dodržování předpisů na den.

|    Vlastnost   |                                          Popis                                          |           Příklad           |
|---------------|-----------------------------------------------------------------------------------------------|-----------------------------|
| dateKey       | Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo. | 20160703                    |
| policyKey     | Klíč zásad, který jde připojit k zásadám a získat tak název zásad.                                | Směrný plán Windows 10         |
| policyTypeKey | Typ klíče zásad, který jde připojit k typu zásad a získat tak název typu zásad.             | Zásady dodržování předpisů Windows 10 |
| pending       | Počet jedinečných zařízení v čekajícím stavu                                                    | 123                         |
| succeeded     | Počet jedinečných zařízení v úspěšném stavu                                                    | 12                          |
| error         | Počet jedinečných zařízení v chybovém stavu                                                      | 10                          |
| failed        | Počet jedinečných zařízení v neúspěšném stavu                                                     | 2                           |

## <a name="policytypes"></a>policyTypes
Entita **PolicyType** obsahuje seznam typů konfiguračních profilů zařízení, konfiguračních profilů aplikací a zásady dodržování předpisů. Zásady se správou mobilních zařízení (MDM) můžete přiřadit skupině ve vašem podniku.

|    Vlastnost    |                       Popis                      |            Příklad            |
|----------------|--------------------------------------------------------|-------------------------------|
| policyTypeId   | Jedinečný identifikátor zásad ve zdrojovém systému  | 123                           |
| policyTypeKey  | Jedinečný identifikátor zásad v datovém skladu | 1                             |
| policyTypeName | Název typu zásad                               | Zásady dodržování předpisů Windows 10 |

## <a name="policyuseractivities"></a>policyUserActivities
Následující tabulka uvádí počet uživatelů v úspěšném, čekajícím, neúspěšném nebo chybovém stavu za den. Číslo odráží data pro jednotlivé profily typu zásad. Pokud se například uživatel nachází v úspěšném stavu pro všechny své přiřazené zásady, posune čítač úspěšných uživatelů pro daný den o jedna nahoru. Pokud má uživatel přiřazené dva profily, jeden je v úspěšném stavu a druhý je v chybovém stavu, započítá se uživatel v chybovém stavu. Entita **PolicyUserActivity** uvádí, kolik uživatelů se v daném dni během posledních 30 dnů zobrazuje.

|  Vlastnost |                                          Popis                                          |       Příklad       |
|-----------|-----------------------------------------------------------------------------------------------|---------------------|
| dateKey   | Klíč data, kdy se přihlášení konfiguračního profilu zařízení v datovém skladu zaznamenalo. | 20160703            |
| pending   | Počet jedinečných zařízení v čekajícím stavu                                                    | 123                 |
| succeeded | Počet jedinečných zařízení v úspěšném stavu                                                    | 12                  |
| policyKey | Klíč zásad, který jde připojit k zásadám a získat tak název zásad.                                | Směrný plán Windows 10 |
| error     | Počet jedinečných zařízení v chybovém stavu                                                      | 10                  |

## <a name="termsandconditions"></a>termsAndConditions
Entita **termsAndConditions** představuje metadata a obsah daných zásad podmínek a ujednání. Obsah zásad podmínek a ujednání se uživatelům zobrazí při jejich prvním pokusu o registraci do Intune a následně při úpravách, u kterých správce vyžaduje opětovné přijetí. Umožňuje správcům předat ustanovení, která musí uživatel odsouhlasit, aby mohl zařízení do Intune zaregistrovat.

|    Vlastnost        |    Popis    |    Příklad        |
|----------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
|    termsAndConditionsKey    |    Klíč odpovídající záznamu v kolekci ' userTermsAndConditionsAcceptances '    |    123    |
|    termsAndCondidionsId    |    ID této položky termsAndConditions    |    276edcb7-7440-4339-b6c5-8b6fc556fee6    |
|    termsAndConditionsVersion    |    Verze této položky termsAndConditions    |    1    |
|    name    |    Název této položky termsAndConditions        |    Podmínky použití Intune     |
|    Popis    |    Popis těchto podmínek a ujednání     |         |
|    title    |    Název těchto podmínek a ujednání     |    Podnikové zásady správy zařízení        |
|    summaryOfTerms    |    Souhrn podmínek předaných uživateli     |    Souhlasím s podmínkami a ujednáními.    |
|    termsAndConditionsBodyText    |    Text těchto podmínek a ujednání       |    *Šifrování zařízení* Vynucení šestimístného číselného kódu PIN    |
|    IsDeleted    |    Hodnota true nebo false určující, zda se tato hodnota odstranila.     |    Nepravda    |
|    startDateInclusiveUTC    |    Počáteční datum těchto podmínek a ujednání.     |    23. 8. 2018 4:01:34    |
|    endDateEclusiveUTC    |    Koncové datum těchto podmínek a ujednání.     |    31. 12. 9999 12:00:00    |

## <a name="userdeviceassociations"></a>userDeviceAssociations
Entita **UserDeviceAssociation** obsahuje přidružení zařízení uživatelů ve vaší organizaci.

|        Název        |                                             Popis                                            |     Příklad     |
|--------------------|----------------------------------------------------------------------------------------------------|-----------------|
| userKey            | Jedinečný identifikátor uživatele v datovém skladu   (náhradní klíč)                            | 123             |
| deviceKey          | Jedinečný identifikátor zařízení v datovém skladu                                             | 123             |
| createdDateTimeUTC | Datum a čas, kdy se přidružení zařízení uživatele vytvořilo. Používá formát UTC.                     | 23. 11. 2016 0:00 |
| IsDeleted          | Udává, že uživatel registraci zařízení zrušil a že přidružení už není aktuální. | Pravda/nepravda      |
| endedDateTimeUTC   | Datum a čas ve standardu UTC, kdy došlo ke změně vlastnosti IsDeleted na hodnotu True                                               | 23. 6. 2017 0:00  |

## <a name="users"></a>uživatelé
Entita **user** obsahuje seznam všech uživatelů Azure Active Directory (Azure AD) s přiřazenými licencemi ve vaší společnosti.

Kolekce entit **uživatele** obsahuje uživatelská data. Tyto záznamy zahrnují stavy uživatelů za dobu shromažďování dat i v případě odebrání uživatele. Uživatel například může být přidaný do Intune a potom v průběhu posledního měsíce dojde k jeho odebrání. Přestože tento uživatel není v době vytvoření sestavy přítomný, data o něm a jeho stavu existují z předchozího měsíce. Můžete vytvořit sestavu, která ukazuje trvání historické přítomnosti uživatele ve vašich datech.

|          Vlastnost          |                                                                                                           Popis                                                                                                          |                Příklad               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Jedinečný identifikátor uživatele v datovém skladu – náhradní klíč                                                                                                                                                         | 123                                  |
| userId                     | Jedinečný identifikátor uživatele – podobá se vlastnosti UserKey, jedná se ale o přirozený klíč.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| userEmail                  | E-mailová adresa uživatele                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName (Hlavní název uživatele)                        | Hlavní název uživatele (UPN) uživatele                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Zobrazované jméno uživatele                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | Určuje, jestli tento uživatel má licenci na službu Intune.                                                                                                                                                                              | Pravda/nepravda                           |
| IsDeleted                  | Určuje, zda všem uživatelským licencím vypršela platnost a zda byl proto uživatel odebrán z Intune. Pro jeden záznam se tento příznak nemění. Místo toho se vytvoří nový záznam pro nový stav uživatele. | Pravda/nepravda                           |
| rowLastModifiedDateTimeUTC | Datum a čas ve standardu UTC, kdy se tento záznam v datovém skladu naposledy změnil                                                                                                                                                 | 23. 11. 2016 0:00                      |

## <a name="usertermsandconditionsacceptances"></a>userTermsAndConditionsAcceptances
Entita **userTermsAndConditionsAcceptance** představuje stav přijetí daných zásad podmínek a ujednání daným uživatelem. Uživatelé musí přijmout nejaktuálnější verzi podmínek, aby se jim přístup k portálu společnosti zachoval.

|    Vlastnost    |    Popis    |    Příklad    |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------|
|    dateKey    |    Klíč odpovídající hodnotám data v kolekci dates.     |    20180823    |
|    userKey    |    Mapování klíče uživatele na uživatele v kolekci Users.     |    20000    |
|    termsAndConditionsKey    |    Klíč odpovídající záznamu v kolekci ' termsAndConditions '    |    1    |
|    acceptedDateTimeUTC    |    Datum a čas, kdy uživatel tyto podmínky a ujednání přijal.    |    23. 8. 2018 4:01:34    |
|    lastModifiedDateTimeUTC    |    Datum a čas, kdy se tato položka naposledy změnila.     |    23. 8. 2018 4:01:34    |

## <a name="vppprogramtypes"></a>vppProgramTypes 
Entita **vppProgramType** obsahuje seznam možných typů programu VPP pro aplikaci.

|      Vlastnost      |          Popis         |
|--------------------|------------------------------|
| vppProgramTypeID   | ID pro daný typ           |
| vppProgramTypeKey  | Náhradní klíč pro daný klíč |
| vppProgramTypeName | Typ programu VPP          |

### <a name="example"></a>Příklad

|             VppProgramID             |         Název        | Popis                |
|--------------------------------------|---------------------|----------------------------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Partnerský vztah Microsoftu           | Program VPP společnosti Microsoft |
| 00000000-0000-0000-0000-000000000000 | Ještě není k dispozici | Výchozí hodnota, žádný program VPP   |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple               | Program VPP společnosti Apple     |

## <a name="next-steps"></a>Další kroky

Další informace o datovém skladu Intune najdete v článku [Datový model datového skladu](reports-ref-data-model.md).