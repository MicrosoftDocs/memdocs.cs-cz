---
title: Použití rozhraní Graph API k exportu sestav Intune | Microsoft Docs
description: Přečtěte si informace o exportování sestav Intune pomocí rozhraní Graph API.
keywords: ''
ms.author: erikre
author: Erikre
manager: dougeby
ms.date: 09/15/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6739a24f105ac6b8c5c69f193ae51c55f449d383
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90816611"
---
# <a name="export-intune-reports-using-graph-apis"></a>Export sestav Intune pomocí rozhraní Graph API

Všechny sestavy, které byly migrovány do infrastruktury vytváření sestav Intune, budou k dispozici pro export z jednoho rozhraní API pro export nejvyšší úrovně. K provedení volání HTTP je nutné použít rozhraní Microsoft Graph API. Microsoft Graph je webové rozhraní API RESTful, které umožňuje přístup k prostředkům služby Microsoft Cloud. 

> [!NOTE]
> Informace o tom, jak provádět REST API volání, včetně nástrojů pro interakci s Microsoft Graph, najdete v tématu [použití rozhraní API Microsoft Graph](https://docs.microsoft.com/graph/use-the-api).

Microsoft Endpoint Manager bude exportovat sestavy na základě následujícího koncového bodu rozhraní Microsoft Graph API:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```
## <a name="example-devices-report-request-and-response"></a>Ukázková zařízení – žádost a odpověď

Při vytváření žádosti musíte zadat `reportName` parametr jako součást textu žádosti na základě sestavy, kterou chcete exportovat. Níže je uveden příklad žádosti o export pro sestavu **zařízení** . Na žádost musíte použít metodu POST HTTP. Metoda POST slouží k vytvoření nového prostředku nebo provedení akce.

### <a name="request-example"></a>Příklad požadavku

Níže uvedená žádost obsahuje metodu HTTP použitou v žádosti o Microsoft Graph.

```http
{ 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "localization": "true", 
    "ColumnName": "ui" 
} 
```
### <a name="response-example"></a>Příklad odpovědi

V závislosti na výše uvedené žádosti se v grafu vrátí zpráva odpovědi. Zpráva odpovědi je požadovaná data nebo výsledek operace.

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "notStarted", 
    "url": null, 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "0001-01-01T00:00:00Z" 
} 
```
Pak můžete pomocí pole zadat `id` dotaz na stav exportu pomocí žádosti o získání: 

Příklad: ```https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('Devices_05e62361-783b-4cec-b635-0aed0ecf14a3') ```

Tuto adresu URL budete muset dál volat, dokud nedostanete odpověď s `status: completed` atributem. Bude vypadat jako v následujícím příkladu:

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "completed", 
    "url": "https://amsua0702repexpstorage.blob.core.windows.net/cec055a4-97f0-4889-b790-dc7ad0d12c29/Devices_05e62361-783b-4cec-b635-0aed0ecf14a3.zip?sv=2019-02-02&sr=b&sig=%2BP%2B4gGiZf0YzlQRuAV5Ji9Beorg4nnOtP%2F7bbFGH7GY%3D&skoid=1db6df02-4c8b-4cb3-8394-7ac2390642f8&sktid=72f988bf-86f1-41af-91ab-2d7cd011db47&skt=2020-08-19T03%3A48%3A32Z&ske=2020-08-19T09%3A44%3A23Z&sks=b&skv=2019-02-02&se=2020-08-19T09%3A44%3A23Z&sp=r", 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "2020-08-19T09:44:23.8540289Z" 
} 
```
Z tohoto pole pak můžete přímo stáhnout komprimovaný soubor CSV `url` .  

## <a name="report-parameters"></a>Parametry sestavy

Existují tři hlavní parametry, které můžete odeslat v těle žádosti, abyste mohli definovat žádost o export: 

- `reportName`Požadovanou. Tento parametr je název sestavy, kterou chcete zadat.  
- `filter`: Není vyžadováno pro většinu sestav. 
- `select`: Není vyžadováno. Pokud nezadáte `select` hodnotu, zobrazí se výchozí sada sloupců, která pro většinu sestav představuje celou datovou sadu. 

## <a name="available-reports"></a>Dostupné sestavy

Následující tabulka obsahuje možné hodnoty pro `reportName` parametr. Tyto sestavy jsou aktuálně dostupné pro export.

|         Report (exportní parametr)  |            Přidružená sestava ve Správci Microsoft Endpoint Manager        |
|-|-|
|         DeviceCompliance  |            Organizace dodržování předpisů zařízením        |
|         DeviceNonCompliance  |            Zařízení, která nedodržují předpisy        |
|         Zařízení  |            Seznam všech zařízení        |
|         DetectedAppsAggregate  |            Sestava zjištěných aplikací        |
|         FeatureUpdatePolicyFailuresAggregate  |            V části **zařízení**  >  **Monitor**  >  **Chyba monitorování aktualizací funkcí**       |
|         DeviceFailuresByFeatureUpdatePolicy  |            V části **zařízení**  >  **Monitor**  >  **selhání monitorování aktualizací funkcí**  >  *klikněte na chyba* .        |
|         FeatureUpdateDeviceState  |            V **části sestavy**  >  **aktualizace oken**  >  **sestavy**aktualizace  >  **funkcí Windows sestava aktualizací**         |
|         UnhealthyDefenderAgents  |            V části **Endpoint Security**  >  **Antivirus**  >  **Win10 chybné koncové body** .        |
|         DefenderAgents  |            V části **sestavy**  >  **MicrosoftDefender**  >  **Reports**  >  **Agent status**        |
|         ActiveMalware  |            V části **Endpoint Security**  >  **Antivirus**  >  **Win10 zjistil malware** .        |
|         Malware  |            V části **sestavy**  >  **MicrosoftDefender**se  >  **Reports**  >  **zjistil malware** .        |

Každá z uvedených sestav je popsána níže.

### <a name="devicecompliance-report"></a>Sestava DeviceCompliance

Následující tabulka obsahuje možný výstup při volání `DeviceCompliance` sestavy:

| Dostupné vlastnosti |
|-|
| DeviceId |
| IntuneDeviceId |
| AadDeviceId |
| DeviceName |
| DeviceType |
| OSDescription |
| OSVersion |
| OwnerType |
| LastContact |
| InGracePeriodUntil |
| IMEI |
| SerialNumber |
| ManagementAgents |
| PrimaryUser |
| UserId |
| UPN |
| UserEmail |
| Uživatelské jméno |
| DeviceHealthThreatLevel |
| RetireAfterDatetime |
| PartnerDeviceId |
| ComplianceState |
| Operační systém |

`DeviceCompliance`Výstup sestavy můžete filtrovat podle následujících sloupců:
- `ComplianceState`
- `OS` 
- `OwnerType`
- `DeviceType` 

### <a name="devicenoncompliance-report"></a>Sestava DeviceNonCompliance

Následující tabulka obsahuje možný výstup při volání `DeviceNonCompliance` sestavy:

|     Dostupné vlastnosti  |
|-|
|     DeviceId  |
|            IntuneDeviceId   |
| AadDeviceId   |
| DeviceName   |
| DeviceType   |
| OSDescription   |
|            OSVersion   |
| OwnerType   |
| LastContact   |
| InGracePeriodUntil   |
| IMEI   |
|            SerialNumber   |
| ManagementAgents   |
| PrimaryUser   |
| UserId     |
| UPN   |
|            UserEmail   |
| Uživatelské jméno   |
| DeviceHealthThreatLevel   |
| RetireAfterDatetime   |
| PartnerDeviceId   |
|            ComplianceState         |
| Operační systém |

`DeviceNonCompliance`Výstup sestavy můžete filtrovat podle následujících sloupců:
- `OS` 
- `OwnerType`
- `DeviceType` 
- `UserId`
- `ComplianceState`

### <a name="devices-report"></a>Sestava zařízení

Následující tabulka obsahuje možný výstup při volání `Devices` sestavy:

|     Dostupné vlastnosti |
|-|
|     DeviceId  |
| DeviceName  |
| DeviceType  |
| ClientRegistrationStatus  |
|            OwnerType  |
| CreatedDate  |
| LastContact  |
| ManagementAgents  |
| ManagementState  |
|            ReferenceId  |
| CategoryId  |
| EnrollmentType  |
| CertExpirationDate  |
| Stavu MDM  |
|            OSVersion  |
| GraphDeviceIsManaged  |
| EasID  |
| SerialNumber  |
| EnrolledByUser  |
|            Manufacturer  |
| Modelování  |
| OSDescription  |
| IsManaged –  |
| EasActivationStatus  |
|            IMEI  |
| EasLastSyncSuccessUtc  |
| EasStateReason  |
| EasAccessState  |
| EncryptionStatus  |
|            SupervisedStatus  |
| PhoneNumberE164Format  |
| InGracePeriodUntil  |
| AndroidPatchLevel  |
| WifiMacAddress  |
|            SCCMCoManagementFeatures  |
| MEID  |
| SubscriberCarrierNetwork  |
| StorageTotal  |
| StorageFree  |
|            ManagedDeviceName  |
| LastLoggedOnUserUPN  |
| MDMWinsOverGPStartTime  |
| StagedDeviceType  |
| UserApprovedEnrollment  |
|            ExtendedProperties  |
| EntitySource  |
| PrimaryUser  |
| CategoryName  |
| UserId  |
|            UPN  |
| UserEmail  |
| Uživatelské jméno  |
| RetireAfterDatetime  |
| PartnerDeviceId  |
|            HasUnlockToken  |
| CompliantState  |
| ManagedBy  |
| Vlastnictví  |
| DeviceState  |
|            DeviceRegistrationState  |
| SupervisedStatusString  |
| EncryptionStatusString  |
| Operační systém  |
| SkuFamily  |
|            JoinType  |
| PhoneNumber  |
| JailBroken  |
| EasActivationStatusString        |

`DeviceNonCompliance`Výstup sestavy můžete filtrovat podle následujících sloupců:
- `OwnerType`
- `DeviceType` 
- `ManagementAgents`
- `CategoryName` 
- `ManagementState` 
- `CompliantState` 
- `JailBroken` 
- `LastContact` 
- `CreatedDate` 
- `EnrollmentType` 

### <a name="detectedappsaggregate-report"></a>Sestava DetectedAppsAggregate

Následující tabulka obsahuje možný výstup při volání `DetectedAppsAggregate` sestavy:

|     Dostupné vlastnosti  |
|-|
|     ApplicationKey  |
| ApplicationName  |
|            ApplicationVersion  |
| Počet zařízení  |
| BundleSize  |

Můžete zvolit filtrování `DetectedAppsAggregate` výstupu sestavy na základě následujícího sloupce:
- `ApplicationName`

### <a name="featureupdatepolicyfailuresaggregate-report"></a>Sestava FeatureUpdatePolicyFailuresAggregate

Následující tabulka obsahuje možný výstup při volání `FeatureUpdatePolicyFailuresAggregate` sestavy:

| Dostupné vlastnosti  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     NumberOfDevicesWithErrors     |

Tuto sestavu nelze filtrovat.

### <a name="devicefailuresbyfeatureupdatepolicy-report"></a>Sestava DeviceFailuresByFeatureUpdatePolicy

Následující tabulka obsahuje možný výstup při volání `DeviceFailuresByFeatureUpdatePolicy` sestavy:

| Dostupné vlastnosti  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     DeviceId  |
|     AADDeviceId  |
|     AlertId  |
|     EventDateTimeUTC  |
|     LastUpdatedAlertStatusDateTimeUTC  |
|     AlertType  |
|     AlertStatus  |
|     AlertClassification  |
|     WindowsUpdateVersion  |
|     Sestavení  |
|     Zadaná hodnota alertmessage  |
|     AlertMessageDescription  |
|     AlertMessageData  |
|     Win32ErrorCode  |
|     RecommendedAction  |
|     ExtendedRecommendedAction  |
|     StartDateTimeUTC  |
|     ResolvedDateTimeUTC  |
|     DeviceName  |
|     UPN     |

`DeviceFailuresByFeatureUpdatePolicy`Výstup sestavy můžete filtrovat podle následujících sloupců:
- `PolicyId`**(Povinné)** 
- `AlertMessage` 
- `RecommendedAction` 
- `WindowsUpdateVersion` 

### <a name="featureupdatedevicestate-report"></a>Sestava FeatureUpdateDeviceState

Následující tabulka obsahuje možný výstup při volání `FeatureUpdateDeviceState` sestavy:

| Dostupné vlastnosti  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     DeviceId  |
|     AADDeviceId  |
|     PartnerPolicyId  |
|     EventDateTimeUTC  |
|     LastSuccessfulDeviceUpdateStatus  |
|     LastSuccessfulDeviceUpdateSubstatus  |
|     LastSuccessfulDeviceUpdateStatusEventDateTimeUTC  |
|     CurrentDeviceUpdateStatus  |
|     CurrentDeviceUpdateSubstatus  |
|     CurrentDeviceUpdateStatusEventDateTimeUTC  |
|     LatestAlertMessage  |
|     LatestAlertMessageDescription  |
|     LatestAlertRecommendedAction  |
|     LatestAlertExtendedRecommendedAction  |
|     UpdateCategory  |
|     WindowsUpdateVersion  |
|     LastWUScanTimeUTC  |
|     Sestavení  |
|     DeviceName  |
|     OwnerType  |
|     UPN  |
|     AggregateState     |

`FeatureUpdateDeviceState`Výstup sestavy můžete filtrovat podle následujících sloupců:
- `PolicyId`**(Povinné)**
- `AggregateState`
- `LatestAlertMessage`
- `OwnerType`

### <a name="unhealthydefenderagents-and-defenderagents-reports"></a>Sestavy UnhealthyDefenderAgents a DefenderAgents

`UnhealthyDefenderAgents`Sestavy a `DefenderAgents` jsou dvě odlišné sestavy, které mají stejnou sadu vlastností a filtrů. Následující tabulka obsahuje možný výstup při volání `UnhealthyDefenderAgents` `DefenderAgents` sestav nebo:

| Dostupné sloupce  |
|-|
|     DeviceId  |
|     DeviceName  |
|     DeviceState  |
|     PendingFullScan  |
|     PendingReboot  |
|     PendingManualSteps  |
|     PendingOfflineScan  |
|     CriticalFailure  |
|     MalwareProtectionEnabled  |
|     RealTimeProtectionEnabled  |
|     NetworkInspectionSystemEnabled  |
|     SignatureUpdateOverdue  |
|     QuickScanOverdue  |
|     FullScanOverdue  |
|     RebootRequired  |
|     FullScanRequired  |
|     EngineVersion  |
|     SignatureVersion  |
|     AntiMalwareVersion  |
|     LastQuickScanDateTime  |
|     LastFullScanDateTime  |
|     LastQuickScanSignatureVersion  |
|     LastFullScanSignatureVersion  |
|     LastReportedDateTime  |
|     UPN  |
|     UserEmail  |
|     Uživatelské jméno     |

`UnhealthyDefenderAgents`Výstup sestavy a můžete filtrovat `DefenderAgents` podle následujících sloupců:
- `DeviceState` 
- `SignatureUpdateOverdue` 
- `MalwareProtectionEnabled`
- `RealTimeProtectionEnabled` 
- `NetworkInspectionSystemEnabled`

### <a name="activemalware-and-malware-reports"></a>Sestavy ActiveMalware a malwaru

`ActiveMalware`Sestavy a `Malware` jsou dvě odlišné sestavy, které mají stejnou sadu vlastností a filtrů. Následující tabulka obsahuje možný výstup při volání `ActiveMalware` `Malware` sestav nebo:

| Dostupné sloupce  |
|-|
|     DeviceId  |
|     DeviceName  |
|     MalwareId  |
|     Malware  |
|     AdditionalInformationUrl  |
|     Závažnost  |
|     MalwareCategory  |
|     ExecutionState  |
|     State  |
|     InitialDetectionDateTime  |
|     LastStateChangeDateTime  |
|     DetectionCount  |
|     UPN  |
|     UserEmail  |
|     Uživatelské jméno     |

`ActiveMalware`Výstup sestavy a můžete filtrovat `Malware` podle následujících sloupců:
- `Severity` 
- `ExecutionState` 
- `State` 

## <a name="next-steps"></a>Další kroky

- [Dokumentace k Microsoft Graph](https://docs.microsoft.com/graph/)
- [Sestavy Intune](https://docs.microsoft.com/mem/intune/fundamentals/reports)