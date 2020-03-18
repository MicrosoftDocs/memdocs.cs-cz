---
title: Co je registrace zařízení v Microsoft Intune?
titleSuffix: Microsoft Intune
description: Přečtěte si o registraci pro zařízení s iOS/iPadOS, Androidem a Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 4/24/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8a81d0cad6e7fa985733675912ada6f446eb501d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331575"
---
# <a name="what-is-device-enrollment"></a>Co je registrace zařízení?
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune umožňuje spravovat zařízení a aplikace vašich zaměstnanců a jejich přístup k firemním datům. Abyste správu mobilních zařízení (MDM) mohli používat, musí být zařízení napřed zaregistrované ve službě Intune. Když je zařízení zaregistrované, vystavuje se certifikát MDM. Tento certifikát slouží ke komunikaci se službou Intune.

Jak vidíte v následujících tabulkách, je k dispozici několik způsobů registrace zařízení zaměstnanců. Jednotlivé způsoby závisí na vlastnictví zařízení (osobní nebo firemní), typu zařízení (iOS, Windows, Android) a požadavcích na správu (resetování, spřažení, uzamčení).

Standardně se do Intune můžou registrovat zařízení pro všechny platformy. Můžete však [omezit zařízení podle platformy](enrollment-restrictions-set.md#create-a-device-type-restriction).

## <a name="iosipados-enrollment-methods"></a>metody registrace pro iOS/iPadOS

| **Metoda** | **Vyžadováno resetování** | [**Přidružení uživatele**](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) | **Uzamčeno** | **Podrobnosti** |
|:---:|:---:|:---:|:---:|:---:|
| | Zařízení se vymažou při registraci. | Jednotlivá zařízení se přidruží k uživateli.| Pokud ano, uživatelé nemůžou zrušit registraci zařízení. | |
|**[Uživatelé s vlastním zařízením (BYOD)](#bring-your-own-device)** | Ne| Ano | Ne | [Další informace](apple-mdm-push-certificate-get.md)|
|**[DEM](#device-enrollment-manager)**| Ne |Ne |Ne | [Další informace](device-enrollment-program-enroll-ios.md)|
|**[DEP](#apple-device-enrollment-program)**| Ano | Volitelné | Volitelné|[Další informace](device-enrollment-program-enroll-ios.md)|
|**[USB-SA](#usb-sa)**| Ano | Volitelné | Ne| [Další informace](apple-configurator-enroll-ios.md)|
|**[USB (přímo)](#usb-direct)**| Ne | Ne | Ne|[Další informace](apple-configurator-enroll-ios.md)|

## <a name="macos-enrollment-methods"></a>Metody registrace zařízení s macOS
| **Metoda** |  **Vyžadováno resetování** |  **Přidružení uživatele** | **Uzamčeno** | **Podrobnosti**|
|:---:|:---:|:---:|:---:|:---:|
|**[Uživatelé s vlastním zařízením (BYOD)](#bring-your-own-device)** | Ne| Ano | Ne | [Další informace](macos-enroll.md)|
|**[DEM](#device-enrollment-manager)**| Ne |Ne |Ne  | [Další informace](device-enrollment-manager-enroll.md)|
|**[DEP](#apple-device-enrollment-program)**| Ano | Volitelné | Volitelné|[Další informace](device-enrollment-program-enroll-macos.md)|

## <a name="windows-enrollment-methods"></a>Metody registrace zařízení s Windows

| **Metoda** | **Vyžadováno resetování** | **Přidružení uživatele** | **Uzamčeno** | **Podrobnosti**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[Uživatelé s vlastním zařízením (BYOD)](#bring-your-own-device)** | Ne | Ano | Ne | [Další informace](windows-enroll.md)|
|**[DEM](#device-enrollment-manager)**| Ne |Ne |Ne |[Další informace](device-enrollment-manager-enroll.md)|
|**Automatická registrace** | Ne |Ano |Ne | [Další informace](windows-enroll.md#enable-windows-10-automatic-enrollment)|
|**Autopilot** |Ano |Ano |Ne | [Další informace](enrollment-autopilot.md)
|**Hromadná registrace** |Ne |Ne |Ne | [Další informace](windows-bulk-enroll.md) |
|**Spoluspráva** |Ne |Ano |Ne | [Další informace](https://docs.microsoft.com/configmgr/core/clients/manage/co-management-overview)
|**Objekty zásad skupiny** |Ne |Ano |Ne | [Další informace](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)

## <a name="android-enrollment-methods"></a>Metody registrace zařízení s Androidem

| **Osobní** | **Metody registrace** | **Vyžadováno resetování** | **Přidružení uživatele** | **Uzamčeno** | **Podrobnosti**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**Správce zařízení s Androidem**|**Uživatel inicioval prostřednictvím Portál společnosti** | Ne | Ano | Ne | [Další informace](https://docs.microsoft.com/user-help/enroll-device-android-company-portal)|
|**Pracovní profil Android Enterprise**|**Uživatel inicioval prostřednictvím Portál společnosti**| Ne | Ano | Ne | [Další informace](android-work-profile-enroll.md)|


| **Firemní** | **Metody registrace** | **Vyžadováno resetování** | **Přidružení uživatele** | **Uzamčeno** | **Podrobnosti**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**Správce zařízení s Androidem**|**[DEM](#device-enrollment-manager) iniciované prostřednictvím portál společnosti**| Ne | Ne | Ne |[Další informace](device-enrollment-manager-enroll.md)|
|**Správce zařízení s Androidem**|**(Předem deklarované IMEI nebo SN) Uživatel inicioval prostřednictvím Portál společnosti**| Ne | Ano | Ne | [Další informace](corporate-identifiers-add.md)|
|**Správce zařízení s Androidem s rozšířeními mobility Zebra**|**Uživatel nebo [DEM](#device-enrollment-manager) iniciované prostřednictvím portál společnosti**| Ne | Ano, pokud se uživatel inicioval, ne při zahájení [DEM](#device-enrollment-manager) | Ne | [Další informace](../configuration/android-zebra-mx-overview.md)|
|**Vyhrazená Enterprise v Androidu**|**NFC, token, kód QR, nulové dotykové ovládání**| Ano | Ne | Konfigurovatelné prostřednictvím zásad | [Další informace](android-kiosk-enroll.md)|
|**Plně spravovaná platforma Android Enterprise**|**NFC, token, kód QR, nulové dotykové ovládání**| Ano | Ano | Konfigurovatelné prostřednictvím zásad | [Další informace](android-dedicated-devices-fully-managed-enroll.md)|


## <a name="bring-your-own-device"></a>Přineste si vlastní zařízení
Přineste si vlastní zařízení (BYOD), včetně telefonů, tabletů a počítačů vlastněných osobně. Kvůli registraci vlastního zařízení uživatelé nainstalují a používají aplikaci Portál společnosti. Tento program umožňuje uživatelům přístup k firemním prostředkům, jako je třeba e-mail.

## <a name="corporate-owned-device"></a>Zařízení vlastněná společností
[Mezi zařízení vlastněná společností](corporate-identifiers-add.md) patří telefony, tablety a počítače ve vlastnictví organizace, které se přidělují zaměstnancům. Registrace zařízení vlastněných společností umožňuje různé způsoby správy, například v podobě automatické registrace, sdílených zařízení nebo předem autorizovaných požadavků na registraci. Správce nebo manažer používá k registraci takových zařízení nejčastěji Správce registrace zařízení (DEM). zařízení s iOS/iPadOS se dají registrovat přímo prostřednictvím nástrojů Program registrace zařízení (DEP), které poskytuje společnost Apple. Zařízení s číslem IMEI se také dají identifikovat a označit jako vlastněné firmou.

### <a name="device-enrollment-manager"></a>Správce registrace zařízení
Správce registrace zařízení (DEM) je zvláštní uživatelský účet, který se používá k registraci a správě více zařízení vlastněných společností. Správci pak mohou nainstalovat aplikaci Portál společnosti a zaregistrovat velký počet zařízení bez uživatele. Tyto typy zařízení se hodí například pro aplikace POS a jednoúčelové aplikace, ale nehodí se pro uživatele, kteří potřebují přístup k e-mailu nebo k prostředkům společnosti. Přečtěte si další informace o [DEM](device-enrollment-manager-enroll.md).

### <a name="apple-device-enrollment-program"></a>Program Apple Device Enrollment Program
Správa pomocí Apple Program registrace zařízení (DEP) umožňuje vytvářet a nasazovat zásady "přes Air" na zařízení s iOS/iPadOS a macOS, která jsou zakoupená a spravovaná pomocí programu DEP. Zařízení se zaregistruje při prvním zapnutí zařízení uživatelem a spustí se Pomocník s nastavením. Tato metoda podporuje režim iOS/iPadOS pod dohledem, který umožňuje konfigurovat zařízení s konkrétními funkcemi.

Další informace o registraci zařízení se systémem iOS/iPadOS DEP:

- [Volba způsobu registrace zařízení se systémem iOS/iPadOS](ios-enroll.md)
- [Registrace zařízení s iOS/iPadOS pomocí Program registrace zařízení](device-enrollment-program-enroll-ios.md)

### <a name="usb-sa"></a>USB (pomocník pro instalaci)
Správci IT používají k ruční přípravě každého zařízení vlastněného společností pro registraci Apple Configurator (přes USB) a Pomocníka s nastavením. Správce IT vytvoří registrační profil a vyexportuje ho do Apple Configuratoru. Když uživatelé dostanou svá zařízení, zobrazí se jim výzva ke spuštění pomocníka s nastavením pro registraci zařízení. Tato metoda podporuje režim **iOS – Pod dohledem**, který umožňuje následující funkce:
- Registrace uzamčeného zařízení
- Beznabídkový režim a další pokročilé konfigurace a omezení

Další informace o registraci zařízení Apple Configuratoru v iOS/iPadOS pomocí Pomocníka s nastavením:

- [Rozhodnutí, jak registrovat zařízení s iOS/iPadOS](ios-enroll.md)
- [Registrace zařízení s iOS/iPadOS pomocí konfigurátoru a pomocníka s nastavením](apple-configurator-enroll-ios.md)

### <a name="usb-direct"></a>USB (přímo)
U přímé registrace musí správce každé zařízení zaregistrovat ručně vytvořením zásady registrace, kterou vyexportuje do Apple Configuratoru. Zařízení vlastněná společností, která jsou připojena přes USB, se zaregistrují přímo a nevyžadují vymazání. Zařízení se spravují jako zařízení bez uživatele. Nejsou uzamčeny nebo pod dohledem a nemohou podporovat podmíněný přístup, zjišťování jailbreaků nebo správu mobilních aplikací.

Další informace o registraci zařízení se systémem iOS/iPadOS najdete v těchto tématech:

- [Rozhodnutí, jak registrovat zařízení s iOS/iPadOS](ios-enroll.md)
- [Registrace zařízení s iOS/iPadOS pomocí konfigurátoru a přímé registrace](apple-configurator-enroll-ios.md)

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Vyčištění mobilních zařízení po vypršení platnosti certifikátu MDM

Certifikát MDM se obnovuje automaticky, když mobilní zařízení komunikují se službou Intune. Pokud se mobilní zařízení vymažou nebo se po určitou dobu nedaří komunikovat se službou Intune, certifikát MDM se neobnoví. Zařízení se z portálu Azure Portal odebere po uplynutí 180 dnů od vypršení platnosti certifikátu MDM.
