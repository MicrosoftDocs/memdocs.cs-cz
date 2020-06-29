---
title: Rozhraní Android Enterprise Security Configuration Framework
titleSuffix: Microsoft Intune
description: Přečtěte si o omezeních a nastaveních navrhovaných pro základní a vysoké zabezpečení zařízení s Androidem Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6ecd15ea98ff9fa5ff0ff6ff570e644a8dcf5003
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502852"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Zásady konfigurace aplikací rozhraní Android Enterprise Security Configuration Framework

V [rámci architektury konfigurace podnikového zabezpečení Androidu](android-configuration-framework.md)musíte správně nastavit zásady konfigurace aplikací pro zařízení s Androidem Enterprise.

Zařízení s Androidem Enterprise Work Profiling jsou navržená tak, aby od sebe izolují pracovní a osobní data. Zařízení s plnou správou Androidu Enterprise jsou navržená jenom pro pracovní nebo školní data. Aplikace Microsoftu nasazené na těchto zařízeních proto musí být nakonfigurované tak, aby povolovaly osobní účty.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Zakázání osobních účtů pro aplikace Microsoftu na zařízeních s Androidem Enterprise

1. Přidejte aplikace do spravovaných Google Play. Další informace najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise pomocí Intune](../apps/apps-add-android-for-work.md).
2. Vytvořte zásadu pro každou spravovanou Google Play aplikaci, jak je popsáno v tématu [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise]().
3. V každé zásadě vytvořte následující jeden klíč:

    | Klíč | Hodnoty |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Jeden nebo více; oddělovače UPN.<br>Jediné povolené účty jsou spravované uživatelské účty definované pomocí tohoto klíče.<br>Pro zařízení zaregistrovaná v Intune se dá použít token {{userPrincipalName}}, který představuje zaregistrovaný uživatelský účet. |


## <a name="next-steps"></a>Další kroky
Použijte [nastavení zabezpečení pracovní profil pro Android Enterprise](android-work-profile-security-settings.md) nebo [plně spravovaná nastavení zabezpečení Android Enterprise](android-fully-managed-security-settings.md).