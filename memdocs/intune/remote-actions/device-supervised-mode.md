---
title: Zapnutí režimu iOS/iPadOS pod dohledem s využitím Microsoft Intune
titleSuffix: ''
description: Naučte se, jak v Intune zapnout režim pod dohledem pro iOS/iPadOS.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8190814-07f0-42d8-9b3a-87c67dd2b7ed
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da02d51ce5860c3be0e0e51341b5f41f01245303
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983053"
---
# <a name="turn-on-iosipados-supervised-mode"></a>Zapnout režim pod dohledem pro iOS/iPadOS


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple iOS/iPadOS pod dohledem poskytuje správcům více možností při správě zařízení Apple. to je užitečné pro zařízení vlastněná společností, která jsou nasazená ve velkém měřítku. Můžete například omezit AirDrop nebo můžete uživatelům znemožnit změny názvu zařízení. Seznam nastavení vyžadujících režim Pod dohledem najdete v tématu [Nastavení omezení pro zařízení s iOSem v Intune](../configuration/device-restrictions-ios.md).

Intune podporuje režim Pod dohledem v rámci [Programu registrace zařízení Apple (DEP)](../enrollment/device-enrollment-program-enroll-ios.md).

Seznam Apple Controls, které vyžadují dohled, najdete v [referenčních informacích k nastavení datové části](http://help.apple.com/configurator/mac/2.4/#/cad5370d089)společnosti Apple.

## <a name="turn-on-supervised-mode-during-enrollment"></a>Zapnutí režimu Pod dohledem během registrace

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete zapnout režim pod dohledem pro zařízení při [vytváření profilu registrace Apple v programu DEP](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile). V části **Nastavení správy zařízení** zaškrtněte políčko **Pod dohledem**.

## <a name="turn-on-supervised-mode-after-enrollment"></a>Zapnutí režimu Pod dohledem po registraci

Jediným způsobem, jak zapnout režim pod dohledem, je připojit zařízení s iOS/iPadOS k počítači Mac a [použít Apple Configuratoru](../enrollment/apple-configurator-enroll-ios.md) (při kterém se zařízení resetuje). Po registraci nemůžete nakonfigurovat zařízení pro dohledový režim v Intune.

## <a name="identify-a-supervised-device"></a>Zjištění, jestli je zařízení pod dohledem

Pokud chcete zjistit, jestli je zařízení pod dohledem, zkontrolujte zamykací obrazovku nebo stránku **Informace**:
- Na zamykací obrazovce zařízení bude sdělení **iPhone je ve správě organizace „název společnosti“.**
- Na stránce **o** zařízení bude **Tento iPhone pod dohledem. Název společnosti může sledovat internetový provoz a vyhledat toto zařízení.**

## <a name="next-steps"></a>Další kroky

Další možnosti správy zařízení najdete v tématu [Co je správa zařízení v Microsoft Intune](device-management.md).
