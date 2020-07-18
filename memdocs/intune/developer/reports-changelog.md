---
title: Protokol změn v datovém skladu Intune
titleSuffix: Microsoft Intune
description: Toto téma poskytuje seznam změn pro Microsoft Intune rozhraní API datového skladu.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: E85DBB2D-67BB-4E10-82D6-E43046B9C43C
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6f460039aaff282476c3e8e3d074a332cde716f
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461211"
---
# <a name="change-log-for-the-intune-data-warehouse-api"></a>Protokol změn pro rozhraní API datového skladu Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Udržujte si přehled o aktualizacích datového skladu Intune.

## <a name="2007"></a>2007 
_Vydáno v červenci 2020_

### <a name="v10-changes"></a>změny v 1.0

Následující tabulka uvádí přidanou vlastnost pro entitu [zařízení](../developer/intune-data-warehouse-collections.md#devices) v datovém skladu Intune.

|    Shromažďování                          |    Změnit     |    Informace o popisu                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    ethernetMacAddress    |    Přidáno    |    Jedinečný identifikátor sítě tohoto zařízení.                                                                                                                                                                                                                                                                     |
|    office365Version    |    Přidáno    |    Verze Office 365, která je na zařízení nainstalovaná.                                                                                                                                                                                                                                                                     |

V následující tabulce je uvedena přidaná vlastnost k entitě [devicePropertyHistories](../developer/intune-data-warehouse-collections.md#devicepropertyhistories) v datovém skladu Intune.

|    Shromažďování                          |    Změnit     |    Informace o popisu                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    physicalMemoryInBytes    |    Přidáno    |    Fyzická paměť v bajtech.                                                                                                                                                                                                                                                                     |
|    totalStorageSpaceInBytes    |    Přidáno    |    Celková kapacita úložiště v bajtech                                                                                                                                                                                                                                                                     |

## <a name="2004"></a>2004 
_Vydáno v dubnu 2020_

### <a name="beta-changes"></a>Změny v beta verzi

Následující tabulka uvádí přidanou vlastnost pro entitu **zařízení** v datovém skladu Intune.

|    Shromažďování                          |    Změnit     |    Informace o popisu                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    windowsOsEdition     |    Přidáno    |    Edice operačního systému Windows.                                                                                                                                                                                                                                                                     |

## <a name="2003"></a>2003 
_Vydáno v březnu 2020_

### <a name="beta-changes"></a>Změny v beta verzi

Následující tabulka obsahuje seznam přidaných vlastností k entitě **zařízení** v datovém skladu Intune.

|    Shromažďování                          |    Změnit     |    Informace o popisu                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    ethernetMacAddress    |    Přidáno    |    Jedinečný identifikátor sítě tohoto zařízení.                                                                                                                                                                                                                                                                     |
|    model    |    Přidáno    |    Model zařízení.                                                                                                                                                                                                                                                                     |
|    office365Version    |    Přidáno    |    Verze Office 365, která je na zařízení nainstalovaná.                                                                                                                                                                                                                                                                     |

Následující tabulka obsahuje seznam přidaných vlastností k entitě **devicePropertyHistory** v datovém skladu Intune.

|    Shromažďování                          |    Změnit     |    Informace o popisu                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    physicalMemoryInBytes    |    Přidáno    |    Fyzická paměť v bajtech.                                                                                                                                                                                                                                                                     |
|    totalStorageSpaceInBytes     |    Přidáno    |    Celková velikost úložiště v bajtech                                                                                                                                                                                                                                                                     |

## <a name="1903-part-2"></a>1903 (část 2)
_Vydáno v dubnu 2019_

### <a name="beta-changes"></a>Změny v beta verzi

V následující tabulce je uveden seznam nedávných odebraných kolekcí a kolekcí nahrazení v datovém skladu Intune.

|    Shromažďování                          |    Změnit     |    Další informace                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    mobileAppDeviceUserInstallStatus    |    Odebráno    |    Místo toho použijte [mobileAppInstallStatusCounts](intune-data-warehouse-collections.md#mobileappinstallstatuscounts) .                                                                                                                                                                                                                                                                     |
|    Entita enrollmenttypes                     |    Odebráno    |    Místo toho použijte [deviceEnrollmentTypes](intune-data-warehouse-collections.md#deviceenrollmenttypes) .                                                                                                                                                                                                                                                                                      |
|    mdmStatuses                         |    Odebráno    |    Místo toho použijte [complianceStates](intune-data-warehouse-collections.md#compliancestates) .                                                                                                                                                                                                                                                                                               |
|    workPlaceJoinStateTypes             |    Odebráno    |    `azureAdRegistered`Místo toho použijte vlastnost v [devicePropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories) kolekcích [zařízení](intune-data-warehouse-collections.md#devices) .                                                                                                                                                                                                             |
|    clientRegistrationStateTypes        |    Odebráno    |    Místo toho použijte [deviceRegistrationStates](intune-data-warehouse-collections.md#deviceregistrationstates) .                                                                                                                                                                                                                                                                             |
|    currentUser                         |    Odebráno    |    Místo toho použijte kolekci [uživatelů](intune-data-warehouse-collections.md#users) .                                                                                                                                                                                                                                                                                                      |
|    mdmDeviceInventoryHistories         |    Odebráno    |    Mnohé z vlastností byly redundantní nebo se teď dají najít v kolekcích [devicePropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories) nebo [Devices](intune-data-warehouse-collections.md#devices) . Všechny vlastnosti **mdmDeviceInventoryHistories** , které již nejsou uvedeny s těmito dvěma kolekcemi, již nejsou k dispozici. Níže najdete podrobnosti.    |

V následující tabulce jsou uvedeny staré vlastnosti dříve nalezené v kolekci **mdmDeviceInventoryHistories** a změna nebo nahrazení. Všechny vlastnosti, které byly v **mdmDeviceInventoryHistories** , ale nejsou uvedené níže, se odebraly.

|    Původní vlastnost                |    Změnit nebo nahradit                                                           |
|--------------------------------|---------------------------------------------------------------------------------|
|    cellularTechnology          |    cellularTechnology v kolekci zařízení                                     |
|    deviceClientId              |    ID zařízení v kolekci                                               |
|    deviceManufacturer          |    výrobce v kolekci zařízení                                           |
|    deviceModel                 |    model v kolekci zařízení                                                  |
|    deviceName                  |    zařízení v kolekci zařízení                                             |
|    deviceOsPlatform            |    deviceTypeKey v kolekci zařízení                                          |
|    deviceOsVersion             |    osVersion v kolekci devicePropertyHistories                              |
|    deviceType                  |    deviceTypeKey v kolekci zařízení, odkazování na kolekci deviceTypes    |
|    encryptionState             |    vlastnost encryptionState v kolekci zařízení                           |
|    exchangeActiveSyncId        |    vlastnost easDeviceId v kolekci zařízení                               |
|    exchangeDeviceId            |    easDeviceId v kolekci zařízení                                            |
|    imei                        |    kolekce IMEI v zařízeních                                                   |
|    isSupervised                |    vlastnost s přídohledem v kolekci zařízení                              |
|    Jailbreak                  |    devicePropertyHistories v kolekci pro jailbreak                             |
|    meid                        |    vlastnost MEID v kolekci zařízení                                      |
|    OEM                         |    výrobce v kolekci zařízení                                           |
|    osName                      |    deviceTypeKey v kolekci zařízení, odkazování na kolekci deviceTypes    |
|    phoneNumber                 |    kolekce phoneNumber v zařízeních                                            |
|    platformType                |    model v kolekci zařízení                                                  |
|    product                     |    deviceTypeKey v kolekci zařízení                                          |
|    productVersion              |    osVersion v kolekci devicePropertyHistories                              |
|    serialNumber                |    Sériové v kolekci zařízení                                           |
|    storageFree                 |    vlastnost freeStorageSpaceInBytes v kolekci zařízení                   |
|    storageTotal                |    vlastnost totalStorageSpaceInBytes v kolekci zařízení                |
|    subscriberCarrierNetwork    |    vlastnost subscriberCarrier v kolekci zařízení                         |
|    wifimac                     |    wiFiMacAddress v kolekci zařízení                                         |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [devicePropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories) : 

|    Původní vlastnost                  |    Změnit nebo nahradit                                               |
|----------------------------------|---------------------------------------------------------------------|
|    KódKategorie                    |    deviceCategoryKey, odkazování na kolekci deviceCategories       |
|    certExpirationDate            |    Odebráno                                                          |
|    clientRegistrationStateKey    |    deviceRegistrationStateKey                                       |
|    createdDate                   |    enrolledDateTime v kolekci zařízení                           |
|    deviceTypeKey                 |    deviceTypeKey v kolekci zařízení                              |
|    easID                         |    easDeviceId v kolekci zařízení                                |
|    enrolledByUser                |    kolekce userId v zařízeních                                     |
|    enrollmentTypeKey             |    deviceEnrollmentTypeKey v kolekci zařízení                    |
|    graphDeviceIsCompliant        |    Odebráno                                                          |
|    graphDeviceIsManaged          |    Odebráno                                                          |
|    lastContact                   |    lastSyncDateTime v kolekci zařízení                           |
|    lastContactNotification       |    Odebráno                                                          |
|    lastContactWorkplaceJoin      |    Odebráno                                                          |
|    lastExchangeStatusUtc         |    Odebráno                                                          |
|    lastModifiedDateTimeUTC       |    Odebráno                                                          |
|    lastPolicyUpdateUtc           |    Odebráno                                                          |
|    managementAgentKey            |    managementStateKey                                               |
|    manufacturer                  |    výrobce v kolekci zařízení                               |
|    mdmStatusKey                  |    complianceStateKey, odkazování na kolekci complianceStates    |
|    model                         |    model v kolekci zařízení                                      |
|    Atribut                      |    operatingSystem v kolekci zařízení                            |
|    osRevisionNumber              |    kolekce osVersion v zařízeních                                  |
|    processorArchitecture         |    Odebráno                                                          |
|    referenceId                   |    azureAdDeviceId v kolekci zařízení                            |
|    serialNumber                  |    Sériové v kolekci zařízení                               |
|    workplaceJoinStateKey         |    azureAdRegistered                                                |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [zařízení](intune-data-warehouse-collections.md#devices) : 

|    Původní vlastnost                  |    Změnit nebo nahradit                                               |
|----------------------------------|---------------------------------------------------------------------|
|    KódKategorie                    |    deviceCategoryKey, odkazování na kolekci deviceCategories       |
|    certExpirationDate            |    Odebráno                                                          |
|    clientRegistrationStateKey    |    deviceRegistrationStateKey                                       |
|    createdDate                   |    enrolledDateTime                                                 |
|    easId                         |    easDeviceId                                                      |
|    enrolledByUser                |    userId                                                           |
|    enrollmentTypeKey             |    deviceEnrollmentTypeKey                                          |
|    graphDeviceIsCompliant        |    Odebráno                                                          |
|    graphDeviceIsManaged          |    Odebráno                                                          |
|    lastContact                   |    lastSyncDateTime                                                 |
|    lastContactNotification       |    Odebráno                                                          |
|    lastContactWorkplaceJoin      |    Odebráno                                                          |
|    lastExchangeStatusUtc         |    Odebráno                                                          |
|    lastPolicyUpdateUtc           |    Odebráno                                                          |
|    mdmStatusKey                  |    complianceStateKey, odkazování na kolekci complianceStates    |
|    Atribut                      |    operatingSystem                                                  |
|    processorArchitecture         |    Odebráno                                                          |
|    referenceId                   |    azureAdDeviceId                                                  |
|    workplaceJoinStateKey         |    azureAdRegistered                                                |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [enrollmentActivities](intune-data-warehouse-collections.md#enrollmentactivities) : 

|    Původní vlastnost         |    Změnit nebo nahradit         |
|-------------------------|-------------------------------|
|    enrollmentTypeKey    |    deviceEnrollmentTypeKey    |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [mamApplications](intune-data-warehouse-collections.md#mamapplications) : 

|    Původní vlastnost       |    Změnit nebo nahradit    |
|-----------------------|--------------------------|
|    applicationKey     |    mamApplicationKey     |
|    applicationName    |    mamApplicationName    |
|    applicationId      |    mamApplicationId      |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [mamApplicationInstances](intune-data-warehouse-collections.md#mamapplicationinstances) : 

|    Původní vlastnost     |    Změnit nebo nahradit    |
|---------------------|--------------------------|
|    applicationId    |    mamApplicationId      |
|    deviceId         |    mamDeviceId           |
|    deviceType       |    mamDeviceType         |
|    deviceName       |    mamDeviceName         |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [mamCheckins](intune-data-warehouse-collections.md#mamcheckins) : 

|    Původní vlastnost      |    Změnit nebo nahradit    |
|----------------------|--------------------------|
|    applicationKey    |    mamApplicationKey     |

V následující tabulce jsou uvedeny změny vlastností nalezené v kolekci [uživatelů](intune-data-warehouse-collections.md#users) : 

|    Původní vlastnost             |    Změnit nebo nahradit    |
|-----------------------------|--------------------------|
|    startDateInclusiveUtc    |    Odebráno               |
|    endDateInclusiveUtc      |    Odebráno               |
|    Aktuální                |    Odebráno               |

## <a name="1903"></a>1903
_Vydáno v březnu 2019_

### <a name="v10-changes-reflecting-back-to-beta"></a>Verze 1.0 změny odrážející zpět na beta verzi
V případě, že verze 1.0 byla poprvé představena v 1808, liší se v několika významných způsobech z verze beta rozhraní API. V 1903 se tyto změny projeví zpátky v beta verzi rozhraní API. Pokud máte důležité sestavy, které používají verzi beta rozhraní API, důrazně doporučujeme, abyste tyto sestavy přepnuli na V 1.0, aby nedocházelo k nepodstatným změnám. Další informace o verzích rozhraní API datového skladu a zpětné kompatibilitě naleznete v [informacích o verzi rozhraní API](reports-api-url.md) .

## <a name="1902"></a>1902 
_Vydáno v únoru 2019_

### <a name="power-bi-compliance-app"></a>Aplikace Power BI dodržování předpisů

Přístup k datovému skladu Intune v Power BI online pomocí aplikace [Intune pro dodržování předpisů (datový sklad)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) . Pomocí této Power BI aplikace teď můžete přistupovat k předem vytvořeným sestavám a sdílet je bez jakéhokoli nastavení a bez nutnosti opustit webový prohlížeč.

> [!NOTE]
> Existují dva další filtry, které můžete použít v aplikaci Intune pro dodržování předpisů.

#### <a name="add-additional-filters-to-the-intune-compliance-app"></a>Přidání dalších filtrů do aplikace Intune pro dodržování předpisů
1. Ve webových prohlížečích otevřete aplikaci [Intune pro dodržování předpisů (datový sklad)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) .
2. Klikněte na **zařízení, která nedodržují předpisy** , a v filtr **ComplianceStatus** vyberte **nekompatibilní** .
3. Klikněte na **neznámá zařízení** a vyberte v filtru **ComplianceStatus** **ještě nedostupné** .

## <a name="1812"></a>1812 
_Vydáno v prosinci 2018_

### <a name="enrollment-activities-collection-released-to-v10"></a>Kolekce aktivit registrace byla vydána do verze 1.0 

Kolekce aktivit registrace je teď dostupná ve verzi 1.0. Tuto kolekci můžete použít k pochopení svazku selhání registrace a trendů ve vašem prostředí. Další informace najdete v tématech [enrollmentActivities](intune-data-warehouse-collections.md#enrollmentactivities), [enrollmentEventStatuses](intune-data-warehouse-collections.md#enrollmenteventstatuses), [enrollmentFailureCategories](intune-data-warehouse-collections.md#enrollmentfailurecategories)a [enrollmentFailureReasons](intune-data-warehouse-collections.md#enrollmentfailurereasons).

## <a name="1808"></a>1808
_Vydáno v srpnu 2018_

### <a name="v10-collections"></a>Kolekce v1.0  

Nastavením parametru dotazu `api-version=v1.0` můžete teď používat verzi datového skladu Intune v1.0. Aktualizace kolekcí v datovém skladu mají aditivní povahu a nijak nenarušují existující scénáře.

### <a name="enrollment-activities-collection-released-to-beta"></a>Kolekce aktivit registrace vydaná do beta verze

Nová kolekce `Enrollment Activities` se vydala ve verzi beta. Můžete ji použít k pochopení průběhu registrace tím, že se zaměříte na nejběžnější chyby. 


## <a name="1805"></a>1805
_Vydáno v květnu 2018_

### <a name="correction-to-device-count-in-devices-collection"></a>Oprava počtu zařízení v kolekci **Zařízení** 

Opravili jsme kolekci **Zařízení**, čímž se může snížit celkový počet zařízení vyfiltrovaných podle atributu `isDeleted`. Toto snížení je výsledkem opravy a není to chyba. Další informace o kolekci **Zařízení** najdete v části [Referenční informace pro entity zařízení](reports-ref-devices.md). 


## <a name="1801"></a>1801
_Vydáno v lednu 2018_

### <a name="intune-data-warehouse-application-only-authentication----1867540---"></a>Ověřování v Intune Data Warehouse pouze na úrovni aplikace <!-- 1867540 -->

Můžete nastavit aplikaci pomocí Azure Active Directory (Azure AD) a ověřit ji přes Intune Data Warehouse. Další informace najdete v tématu [Ověřování v datovém skladu Intune pouze na úrovni aplikace](data-warehouse-app-only-auth.md).

### <a name="azure-ad-and-intune-credential-requirements----2077525---"></a>Požadavky na přihlašovací údaje pro Azure AD a Intune <!-- 2077525 -->

- Při přístupu k datovému skladu Intune (včetně rozhraní API) se už nevyžaduje přiřazení licence Intune uživateli.
- Název role Intune **Sestavy** se změnil na **Datový sklad Intune**. 

    Další informace najdete v tématu [Požadavky na přihlašovací údaje pro Azure AD a Intune](reports-api-url.md#azure-ad-and-intune-credential-requirements).

### <a name="odata-query-options----2077711---"></a>Možnosti dotazu OData <!-- 2077711 -->

Jako parametr dotazu OData můžete použít <code>$select</code>. Aktuální verze podporuje tyto parametry dotazu OData: <code>$filter</code>, <code>$orderby</code>, <code>$select</code>, <code>$skip</code> a <code>$top</code>. Další informace najdete v tématu [Možnosti dotazu OData](reports-api-url.md#odata-query-options).

### <a name="new-entities-in-the-in-data-warehouse-data-model----2077804---"></a>Nové entity v datovém modelu datového skladu  <!-- 2077804 -->

- Byla přidána entita [**MobileAppDeviceuserInstallStatus**](reports-ref-application.md). **MobileAppDeviceUserInstallStatus** představuje stav instalace mobilní aplikace pro dané zařízení a uživatele.
- Entita, [**MobileAppInstallStates**](reports-ref-application.md#mobileappinstallstates), byla přidána. Entita **MobileAppInstallState** představuje stav instalace mobilní aplikace po jejím přiřazení do skupiny obsahující zařízení, uživatele, nebo obě tyto možnosti. 

## <a name="1710"></a>1710
_Vydáno v listopadu 2017_

### <a name="a-new-entity-collection-named-current-user-is-limited-to-currently-active-user-data----1544273---"></a>Nová kolekce entit z názvem Aktuální uživatel se omezuje na data aktuálně aktivních uživatelů  <!-- 1544273 -->

Kolekce entit **Uživatelé** obsahuje všechny uživatele Azure Active Directory (Azure AD), kteří mají v podniku přiřazené licence. Tyto záznamy zahrnují stavy uživatelů za dobu shromažďování dat i v případě odebrání uživatele. Uživatel například může být přidaný do Intune a potom v průběhu posledního měsíce dojde k jeho odebrání. Přestože tento uživatel není v době vytvoření sestavy přítomen, existují data o uživateli a stavu. Můžete vytvořit sestavu, která ukazuje trvání historické přítomnosti uživatele ve vašich datech.

Naproti tomu nová kolekce entit **Aktuální uživatel** obsahuje pouze uživatele, kteří nebyli odebráni. Kolekce entit **Aktuální uživatel** obsahuje pouze aktuálně aktivní uživatele. Informace o kolekci entit **Aktuální uživatel** najdete v části [Referenční informace o entitě aktuálního uživatele](reports-ref-data-model.md).

## <a name="1709"></a>1709
_Vydáno: říjen 2017_

### <a name="user-device-association-entity-collection-added-to-intune-data-warehouse-data-model----1187917---"></a>Přidala se kolekce entit přidružení uživatelských zařízení do datového modelu datového skladu Intune. <!-- 1187917 -->

Pomocí informací o přidružení uživatelů a zařízení, které přidružují kolekce entit uživatelů a zařízení, teď můžete vytvářet sestavy a vizualizace dat. Tento datový model lze zpřístupnit přes soubor Power BI (PBIX) načtený ze stránky Datový sklad v Intune, přes koncový bod OData nebo vývojem vlastního klienta. Další informace najdete v tématu [Přidružení zařízení uživatele](reports-ref-user-device.md).

### <a name="new-entities-in-the-in-data-warehouse-data-model----1479526--------"></a>Nové entity v datovém modelu datového skladu  <!-- 1479526 --><!-- -->

- Přidali jsme entitu [**UserDeviceAssociation**](reports-ref-user-device.md). **UserDeviceAssociation** obsahuje přidružení zařízení uživatelů ve vaší organizaci. Pomocí informací o přidružení uživatelů a zařízení, které přidružují kolekce entit uživatelů a zařízení, teď můžete vytvářet sestavy a vizualizace dat.  
- Přidali jsme entitu [**IntuneManagementExtension**](reports-ref-intunemanagementextension.md). **IntuneManagementExtension** obsahuje entity pro mobilní zařízení, které sledují informace, jako je verze a stav instalace.

## <a name="next-steps"></a>Další kroky
- Podívejte [se, co je nového v Intune každý týden](../fundamentals/whats-new.md). Můžete také získat informace o nadcházejících změnách, důležitá oznámení o službě a informace o minulých vydaných verzích.
- Přečtěte si [Blog Microsoft Intune](https://www.microsoft.com/microsoft-365/blog/microsoft-intune/).
