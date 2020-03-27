---
title: Zapnutí režimu iOS/iPadOS pod dohledem s využitím Microsoft Intune
titleSuffix: ''
description: Naučte se, jak v Intune zapnout režim pod dohledem pro iOS/iPadOS.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8190814-07f0-42d8-9b3a-87c67dd2b7ed
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da03bb3fdf1f0d67639f7719215d756b7d598d7c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325077"
---
# <a name="turn-on-iosipados-supervised-mode"></a>Zapnutí dohledového režimu systému iOS/iPadOS


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple iOS/iPadOS pod dohledem poskytuje správcům více možností při správě zařízení Apple. to je užitečné pro zařízení vlastněná společností, která jsou nasazená ve velkém měřítku. Můžete například omezit AirDrop nebo můžete uživatelům znemožnit změny názvu zařízení. Seznam nastavení vyžadujících režim Pod dohledem najdete v tématu [Nastavení omezení pro zařízení s iOSem v Intune](../configuration/device-restrictions-ios.md).

Intune podporuje režim Pod dohledem v rámci [Programu registrace zařízení Apple (DEP)](../enrollment/device-enrollment-program-enroll-ios.md).

Seznam ovládacích prvků Apple, které vyžadují dohled, najdete na webu společnosti Apple v [referenčních informacích o nastavení datové části](http://help.apple.com/configurator/mac/2.4/#/cad5370d089).

## <a name="turn-on-supervised-mode-during-enrollment"></a>Zapnutí režimu Pod dohledem během registrace

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete zapnout režim pod dohledem pro zařízení při [vytváření profilu registrace Apple v programu DEP](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile). V části **Nastavení správy zařízení** zaškrtněte políčko **Pod dohledem**.

## <a name="turn-on-supervised-mode-after-enrollment"></a>Zapnutí režimu Pod dohledem po registraci

Jediným způsobem, jak zapnout režim pod dohledem, je připojit zařízení s iOS/iPadOS k počítači Mac a [použít Apple Configuratoru](../enrollment/apple-configurator-enroll-ios.md) (při kterém se zařízení resetuje). Po registraci není možné nakonfigurovat režim Pod dohledem pro zařízení v Intune.

## <a name="identify-a-supervised-device"></a>Zjištění, jestli je zařízení pod dohledem

Pokud chcete zjistit, jestli je zařízení pod dohledem, zkontrolujte zamykací obrazovku nebo stránku **Informace**:
- Na zamykací obrazovce zařízení bude sdělení **iPhone je ve správě organizace „název společnosti“.**
- Na stránce **o** zařízení bude **Tento iPhone pod dohledem. Název společnosti může sledovat internetový provoz a vyhledat toto zařízení.**

## <a name="next-steps"></a>Další kroky

Další možnosti správy zařízení najdete v tématu [Co je správa zařízení v Microsoft Intune](device-management.md).
