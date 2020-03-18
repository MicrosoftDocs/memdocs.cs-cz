---
title: Data z Intune odesílaná Applu
titleSuffix: Microsoft Intune
description: Seznam dat, která Intune odesílá Applu
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/26/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b204a956-18ec-11e8-accf-0ed5f89f718b
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da9ab5fe5a8716e3af0ae02122f51d06e6e55e6f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329451"
---
# <a name="data-intune-sends-to-apple"></a>Data z Intune odesílaná Applu

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Pokud se na zařízení povolí některá z následujících služeb Apple, Microsoft Intune naváže spojení s Applem a bude s ním sdílet informace o uživateli a o zařízení: 

- [Program Apple DEP (Device Enrollment Program)](../enrollment/device-enrollment-program-enroll-ios.md)
- [Certifikát Apple MDM Push Certificate (APNS)](../enrollment/apple-mdm-push-certificate-get.md)
- [Apple School Manager (ASM)](https://docs.microsoft.com/schooldatasync/apple-school-manager-integration-with-intune-for-education-and-school-data-sync)
- [Program Apple VPP (Volume Purchase Program)](../apps/vpp-apps-ios.md)

Aby mohla služba Microsoft Intune navázat spojení, je napřed nutné pro každou službu Apple vytvořit účet Apple.

Následující tabulka uvádí data, která Microsoft Intune odesílá ze zařízení do povolených služeb Apple. 

| Service | Data odesílaná Applu | Používáno pro |
|---|---| ---|
| [APNS](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/MobileDeviceManagementProtocolRef/3-MDM_Protocol/MDM_Protocol.html#//apple_ref/doc/uid/TP40017387-CH3-SW2) | Token, PushMagic | Pokud server přijme zařízení, dané zařízení poskytne serveru svůj token zařízení pro nabízená oznámení. Pomocí tohoto tokenu by měl server odesílat nabízené zprávy do daného zařízení. Tato přihlašovací zpráva obsahuje také řetězec PushMagic. Server si musí pamatovat tento řetězec a zahrnout ho do každé nabízené zprávy, kterou odesílá do daného zařízení. |
| [ASM/DEP](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/MobileDeviceManagementProtocolRef/3-MDM_Protocol/MDM_Protocol.html#//apple_ref/doc/uid/TP40017387-CH3-SW2) | Token serveru | Token zařízení pro nabízená oznámení, který se používá k ověření služby Apple |
| ASM/DEP | server_name | Identifikovatelný název pro server MDM |
| ASM/DEP | server_uuid | Systémem generovaný identifikátor serveru |
| ASM/DEP | admin_id | Apple ID osoby, která vygenerovala aktuálně používané tokeny |
| ASM/DEP | org_name | Název organizace |
| ASM/DEP | org_email | E-mailová adresa organizace |
| ASM/DEP | org_phone | Telefon organizace |
| ASM/DEP | org_address | Adresa organizace |
| ASM/DEP | org_id | ID zákazníka s programem DEP. Tento klíč je dostupný jenom ve verzi protokolu 3 nebo novější. |
| ASM/DEP | serial_number | Sériové číslo zařízení (řetězec) |
| ASM/DEP | model | Název modelu (řetězec) |
| ASM/DEP | description | Popis zařízení (řetězec) |
| ASM/DEP | asset_tag | Inventární štítek zařízení (řetězec) |
| ASM/DEP | profile_status | Stav instalace profilu. Možné hodnoty: **empty**, **assigned**, **pushed** nebo **removed** |
| ASM/DEP | profile_uuid | Jedinečné ID přiřazeného profilu |
| ASM/DEP | device_assigned_by | E-mail osoby, která přiřadila dané zařízení |
| ASM/DEP | os | Operační systém zařízení: iOS/iPadOS, OSX nebo tvOS. Tento klíč je platný v X-Server-Protocol-Version 2 nebo v novější verzi. |
| ASM/DEP | device_family | Produktová řada Apple, do které dané zařízení patří: iPad, iPhone, iPod, Mac nebo AppleTV. Tento klíč je platný v X-Server-Protocol-Version 2 nebo v novější verzi. |
| ASM/DEP | profile_name | Řetězec. Popisný název pro profil. |
| ASM/DEP | support_phone_number | Volitelný parametr. Řetězec. Telefonní číslo podpory pro organizaci. |
| ASM/DEP | support_email_address | Volitelný parametr. Řetězec. E-mailová adresa podpory pro organizaci. Tento klíč je platný v X-Server-Protocol-Version 2 nebo v novější verzi. |
| ASM/DEP | Oddělení | Volitelný parametr. Řetězec. Uživatelem definovaný název oddělení nebo umístění. |
| ASM/DEP | zařízení | Pole řetězců obsahující sériová čísla zařízení (může být prázdné) |
| VPP | Identifikátor GUID ID uživatele Intune | Identifikátor GUID vygenerovaný službou Intune |
| VPP | Spravovaný hlavní název uživatele (UPN) AppleID | AppleID, které určil správce při konfiguraci spojení s Applem pomocí tokenu VPP |
| VPP | Sériové číslo | Sériové číslo spravovaného zařízení |

Pokud chcete ukončit používání služeb Apple v Microsoft Intune a odstranit data, je nutné deaktivovat token Apple v Microsoft Intune a také odstranit váš účet Apple. Vyhledejte si v účtu Apple postup pro správu účtu.


