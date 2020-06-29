---
title: Omezení registrace zařízení pro rozhraní Android Enterprise Security Configuration Framework
titleSuffix: Microsoft Intune
description: Omezení registrace zařízení pro architekturu konfigurace podnikového zabezpečení Androidu.
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
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502846"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Omezení registrace zařízení s Androidem Enterprise

Před registrací zařízení pro platformu pro [konfiguraci Android Enterprise Security]()musí organizace nakonfigurovat vhodná omezení. Tato omezení zajistí, že se uživatelé můžou zaregistrovat jenom
- schválená zařízení.
- zadaný počet zařízení.
- zařízení se zadanými platformami.
- zařízení se zadanými operačními systémy.
- zařízení od určených výrobců.

Další informace o omezení registrace zařízení najdete v tématu [Nastavení omezení registrace](enrollment-restrictions-set.md).

## <a name="work-profile-basic-level-1-security-restrictions"></a>Omezení zabezpečení pracovního profilu Basic (úroveň 1)

Pro základní zabezpečení pracovního profilu Android Enterprise (úroveň 1) musí být implementována následující omezení zařízení:

| Typ | Platforma | Verze | Umožňuje osobní zařízení. |
|--------|--------|--------|--------|
| Android Enterprise | Povolit | Android 5,0 a novější.<p>Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno.   V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze. Další informace najdete v tématu [Doporučené požadavky pro Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). | Yes |
| Správce zařízení s Androidem| Blok | Všechny verze | Yes |

## <a name="work-profile-high-level-3-security-restrictions"></a>Omezení zabezpečení pracovního profilu high (Level 3)
Pro zajištění vysokého zabezpečení pracovních profilů pro Android Enterprise (úroveň 3) by se měly implementovat následující omezení zařízení:

| Typ | Platforma | Verze | Umožňuje osobní zařízení. |
|--------|--------|--------|--------|
| Android Enterprise | Povolit | Android 8,0 a novější | Yes |
| Správce zařízení s Androidem| Blok | Všechny verze | Yes |

## <a name="fully-managed-security-restrictions"></a>Plně spravovaná omezení zabezpečení
Ujistěte se, že organizace podporuje registraci zařízení s plně spravovaným Androidem Enterprise, a to kontrolou plně spravované registrace Android Enterprise. 

## <a name="next-steps"></a>Další kroky

[Nastavení zásad konfigurace aplikací](android-app-configuration-policies.md)
