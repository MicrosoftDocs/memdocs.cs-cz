---
title: Zařízení – Datový sklad Intune
titleSuffix: Microsoft Intune
description: Téma referenčních informací ke kategorii Zařízení pro kolekce entit v rozhraní API datového skladu Intune
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6955E12D-70D7-4802-AE3B-8B276F01FA4F
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31eef700f7aa38b70c5e9a2fa75fd3faee4c9713
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078052"
---
# <a name="reference-for-devices-entities"></a>Referenční informace o entitách zařízení

Kategorie **zařízení** obsahuje entity pro mobilní zařízení, které sledují informace, jako například:

- Typ zařízení
- Stav zápisu a registrace zařízení
- Vlastnictví zařízení
- Stav správy zařízení
- Stav členství zařízení v Azure AD
- Stav registrace
- Historické informace o zařízení
- Inventář aplikací na daném zařízení

## <a name="devicetypes"></a>deviceTypes

Entita **deviceTypes** představuje typ zařízení, na který odkazují jiné entity datového skladu. Typ zařízení obvykle popisuje model zařízení, výrobce nebo kombinaci obou těchto možností.

| Vlastnost  | Popis |
|---------|------------|
| deviceTypeID |Jedinečný identifikátor typu zařízení |
| deviceTypeKey |Jedinečný identifikátor typu zařízení v datovém skladu – náhradní klíč |
| deviceTypeName |Typ zařízení |

### <a name="example"></a>Příklad

| deviceTypeID  | Název | Popis |
|---------|------------|--------|
| 0 |Aplikace klasické pracovní plochy |Zařízení se systémem Windows |
| 1 |WindowsRT |Zařízení se systémem WindowsRT |
| 2 |WinMO6 |Zařízení se systémem Windows Mobile 6.0 |
| 3 |Nokia |Zařízení Nokia |
| 4 |WindowsPhone |Zařízení Windows Phone |
| 5 |Mac |Zařízení Mac |
| 6 |WinCE |Zařízení se systémem Windows CE |
| 7 |WinEmbedded |Zařízení se systémem Windows Embedded |
| 8 |IPhone |Zařízení iPhone |
| 9 |IPad |Zařízení iPad |
| 10 |IPod |Zařízení iPod |
| 11 |Android |Zařízení Android spravované pomocí Správce zařízení |
| 12 |ISocConsumer |Zařízení iSoc Consumer |
| 14 |MacMDM |Zařízení se systémem Mac OS X spravované pomocí integrovaného agenta MDM |
| 15 |HoloLens |Zařízení HoloLens |
| 16 |SurfaceHub |Zařízení Surface Hub |
| 17 |AndroidForWork |Zařízení Android spravované pomocí vlastníka profilu Androidu |
| 100 |Blackberry |Zařízení Blackberry |
| 101 |Palm |Zařízení Palm |
| 255 |Není známo |Neznámý typ zařízení |

## <a name="enrollmentactivities"></a>enrollmentActivities 
Entita **enrollmentActivity** označuje aktivitu registrace zařízení.

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
Entita **enrollmentEventStatus** indikuje výsledek registrace zařízení.

| Vlastnost                   | Popis                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | Jedinečný identifikátor stavu registrace v datovém skladu (náhradní klíč)  |
| enrollmentEventStatusName  | Název stavu registrace. Podívejte se na následující příklady:                            |

### <a name="example"></a>Příklad

| enrollmentEventStatusName  | Popis                            |
|----------------------------|----------------------------------------|
| Úspěch                    | Úspěšná registrace zařízení         |
| Failed                     | Neúspěšná registrace zařízení             |
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
| Není známo                         | Neznámou chybu.                                                                                                |
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
| Není známo                          | Neznámá chyba.                                                                                                                                                                                         |
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
## <a name="ownertypes"></a>ownerTypes

Entita **enrollmentType** označuje, jestli je zařízení firemní, osobně vlastněné nebo neznámé.

| Vlastnost  | Popis | Příklad |
|---------|------------|--------|
| ownerTypeID |Jedinečný identifikátor typu vlastníka. | |
| ownerTypeKey |Jedinečný identifikátor typu vlastníka v datovém skladu – náhradní klíč. | |
| ownerTypeName |Představuje typ vlastníka zařízení:  <br>Podnik – zařízení je ve vlastnictví podniku. <br>Osobní – zařízení je v osobním vlastnictví (BYOD).  <br>Neznámé – žádné informace o tomto zařízení nejsou dostupné. |Firemní osobní neznámý |

> [!Note]  
> Při vytváření `ownerTypeName` dynamických skupin pro zařízení v nástroji AzureAD je potřeba nastavit hodnotu `deviceOwnership` filtru jako. `Company` Další informace najdete v tématu [pravidla pro zařízení](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="managementstates"></a>managementStates

Entita **managementStates** poskytuje podrobné informace o stavu zařízení. Podrobnosti můžou být užitečné v případech, kdy se používají vzdálené akce, nebo pokud jde o zařízení s jailbreakem nebo rootem.

| Vlastnost  | Popis |
|---------|------------|
| managementStateID | Jedinečný identifikátor stavu správy |
| managementStateKey | Jedinečný identifikátor stavu správy v datovém skladu – náhradní klíč |
| managementStateName | Určuje stav vzdálené akce použité pro toto zařízení. |

### <a name="example"></a>Příklad

| managementStateID  | Název | Popis |
|---------|------------|--------|
| 0 |Spravovaní | Spravováno bez čekajících vzdálených akcí |
| 1 |RetirePending | Pro toto zařízení existuje příkaz pro vyřazení z provozu, který čeká na vyřízení. |
| 2 |RetireFailed | Příkaz pro vyřazení z provozu u tohoto zařízení selhal. |
| 3 |WipePending | Pro toto zařízení existuje příkaz pro vymazání, který čeká na vyřízení. |
| 4 |WipeFailed | Příkaz pro vymazání u tohoto zařízení selhal. |
| 5 |Není v pořádku | Stav Není v pořádku. |
| 6 |DeletePending | Pro toto zařízení existuje příkaz pro odstranění, který čeká na vyřízení. |
| 7 |RetireIssued | Pro toto zařízení se vystavil příkaz pro vyřazení z provozu. |
| 8 |WipeIssued | Příkaz pro vymazání se vystavil. |
| 9 |WipeCanceled | Příkaz pro vymazání se zrušil. |
| 10 |RetireCanceled | Příkaz pro vyřazení z provozu se zrušil. |
| 11 |Zjištěno | Zařízení je v Intune nově zjištěno, po prvním přihlášení přejde do stavu Spravováno. |

## <a name="managementagenttypes"></a>managementAgentTypes

Entita **ManagementAgentType** představuje agenty používané ke správě zařízení.

| Vlastnost  | Popis |
|---------|------------|
| managementAgentTypeID | Jedinečný identifikátor typu agenta správy. |
| managementAgentTypeKey | Jedinečný identifikátor typu agenta správy v datovém skladu – náhradní klíč. |
| managementAgentTypeName |Určuje typ agenta, který se používá ke správě zařízení. |

### <a name="example"></a>Příklad

| ManagementAgentTypeID  | Název | Popis |
|---------|------------|--------|
| 1 |EAS | Zařízení se spravuje prostřednictvím protokolu Exchange Active Sync. |
| 2 |MDM | Zařízení se spravuje pomocí agenta MDM. |
| 3 |EasMdm | Zařízení se spravuje pomocí protokolu Exchange Active Sync i pomocí agenta MDM. |
| 4 |IntuneClient | Zařízení se spravuje pomocí agenta Intune pro počítače. |
| 5 |EasIntuneClient | Zařízení se spravuje pomocí protokolu Exchange Active Sync i pomocí agenta Intune pro počítače. |
| 8 |ConfigManagerClient | Zařízení spravuje agent Configuration Manager. |
| 16 |Není známo | Neznámý typ agenta správy |

## <a name="devices"></a>zařízení

Entita **zařízení** obsahuje seznam všech zaregistrovaných zařízení, která jsou pod správou, a jejich odpovídající vlastnosti.

|          Vlastnost          |                                                                                       Popis                                                                                      |
|:--------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| deviceKey                  | Jedinečný identifikátor zařízení v datovém skladu – náhradní klíč                                                                                                               |
| deviceId                   | Jedinečný identifikátor zařízení                                                                                                                                                     |
| deviceName                 | Název zařízení na platformách, které umožňují pojmenování zařízení. Na ostatních platformách Intune vytvoří název z dalších vlastností. Tento atribut nemusí být dostupný pro všechna zařízení. |
| deviceTypeKey              | Klíč atributu typu zařízení pro toto zařízení                                                                                                                                    |
| deviceRegistrationState    | Klíč atributu stavu registrace klienta pro toto zařízení                                                                                                                      |
| ownerTypeKey               | Klíč atributu typu vlastníka pro toto zařízení: podnikový, osobní nebo neznámý                                                                                                    |
| enrolledDateTime           | Datum a čas, kdy se zařízení zaregistrovalo.                                                                                                                                         |
| lastSyncDateTime           | Poslední známé přihlášení zařízení k Intune.                                                                                                                                              |
| managementAgentKey         | Klíč agenta správy, který je k tomuto zařízení přidružený.                                                                                                                             |
| managementStateKey         | Klíč stavu správy, který je přidružený k tomuto zařízení a který udává poslední stav vzdálené akce nebo informaci, jestli jde o zařízení s jailbreakem nebo rootem.                                                |
| azureADDeviceId            | ID zařízení Azure pro toto zařízení                                                                                                                                                  |
| azureADRegistered          | Udává, zda je zařízení zaregistrované v Azure Active Directory.                                                                                                                             |
| deviceCategoryKey          | Klíč kategorie, která je k tomuto zařízení přidružená.                                                                                                                                     |
| deviceEnrollmentType       | Klíč typu registrace, který je přidružený k tomuto zařízení a který udává metodu registrace.                                                                                             |
| complianceStateKey         | Klíč stavu dodržování předpisů, který je k tomuto zařízení přidružený.                                                                                                                             |
| osVersion                  | Verze operačního systému v zařízení                                                                                                                                                |
| easDeviceId                | ID protokolu Exchange ActiveSync zařízení.                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Jedinečný identifikátor uživatele přidružený k zařízení                                                                                                                           |
| rowLastModifiedDateTimeUTC | Datum a čas ve standardu UTC, kdy se toto zařízení v datovém skladu naposledy změnilo.                                                                                                       |
| manufacturer               | Výrobce zařízení                                                                                                                                                             |
| model                      | Model zařízení                                                                                                                                                                    |
| operatingSystem            | Operační systém zařízení Windows, iOS/iPadOS atd.                                                                                                                                   |
| IsDeleted                  | Binární soubor zobrazující, zda se zařízení odstranilo nebo ne.                                                                                                                                 |
| androidSecurityPatchLevel  | Úroveň opravy zabezpečení Androidu                                                                                                                                                           |
| MEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Stav dohledu zařízení                                                                                                                                                               |
| freeStorageSpaceInBytes    | Volné místo úložiště v bajtech                                                                                                                                                                 |
| totalStorageSpaceInBytes   | Celková velikost úložiště v bajtech                                                                                                                                                                |
| encryptionState            | Stav šifrování zařízení                                                                                                                                                      |
| subscriberCarrier          | Poskytovatel předplatného na zařízení                                                                                                                                                       |
| phoneNumber                | Telefonní číslo zařízení                                                                                                                                                             |
| IMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Mobilní technologie zařízení                                                                                                                                                    |
| WiFiMacAddress             | Wi-Fi MAC                                                                                                                                                                              |
| ICCD                       | Identifikátor karty integrovaného okruhu                                                                                                                                                     |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

Entita **devicePropertyHistory** má stejné vlastnosti jako tabulka zařízení a denní snímky každého záznamu zařízení za den v posledních 90 dnech. Sloupec DateKey označuje den pro každý řádek.

|          Vlastnost          |                                                                                      Popis                                                                                     |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| dateKey                    | Odkaz na tabulku kalendářních dat udávající den.                                                                                                                                          |
| deviceKey                  | Jedinečný identifikátor zařízení v datovém skladu – náhradní klíč Jedná se o odkaz na tabulku zařízení obsahující ID zařízení v Intune.                               |
| deviceName                 | Název zařízení na platformách, které umožňují pojmenování zařízení. Na ostatních platformách Intune vytvoří název z dalších vlastností. Tento atribut nemusí být dostupný pro všechna zařízení. |
| deviceRegistrationStateKey | Klíč atributu stavu registrace zařízení pro toto zařízení                                                                                                                    |
| ownerTypeKey               | Klíč atributu typu vlastníka pro toto zařízení: podnikový, osobní nebo neznámý                                                                                                  |
| managementStateKey         | Klíč stavu správy, který je přidružený k tomuto zařízení a který udává poslední stav vzdálené akce nebo informaci, jestli jde o zařízení s jailbreakem nebo rootem.                                                |
| azureADRegistered          | Udává, zda je zařízení zaregistrované v Azure Active Directory.                                                                                                                             |
| complianceStateKey         | Klíč k vlastnosti ComplianceState                                                                                                                                                            |
| OSVersion                  | Verze operačního systému.                                                                                                                                                                          |
| Jailbreak                 | Zda má zařízení jailbreak nebo root.                                                                                                                                         |
| deviceCategoryKey          | Klíč atributu kategorie zařízení pro toto zařízení 

