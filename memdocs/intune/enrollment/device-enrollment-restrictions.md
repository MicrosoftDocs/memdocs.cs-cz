---
title: Omezení registrace zařízení pro rozhraní Android Enterprise Security Configuration Framework
titleSuffix: Microsoft Intune
description: Omezení registrace zařízení pro architekturu konfigurace podnikového zabezpečení Androidu.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 618be398d963e0a796ad9be7e8810201fc5e12f5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995088"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Omezení registrace zařízení s Androidem Enterprise

Před registrací zařízení pro platformu pro [konfiguraci Android Enterprise Security](android-configuration-framework.md)musí organizace nakonfigurovat vhodná omezení. Tato omezení zajistí, že se uživatelé můžou zaregistrovat jenom

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
| Android Enterprise | Povolit | Android 5,0 a novější.<p>Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno.   V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze. Další informace najdete v tématu [Doporučené požadavky pro Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). | Ano |
| Správce zařízení s Androidem| Blok | Všechny verze | Ano |

## <a name="work-profile-high-level-3-security-restrictions"></a>Omezení zabezpečení pracovního profilu high (Level 3)
Pro zajištění vysokého zabezpečení pracovních profilů pro Android Enterprise (úroveň 3) by se měly implementovat následující omezení zařízení:

| Typ | Platforma | Verze | Umožňuje osobní zařízení. |
|--------|--------|--------|--------|
| Android Enterprise | Povolit | Android 8,0 a novější | Ano |
| Správce zařízení s Androidem| Blok | Všechny verze | Ano |

## <a name="fully-managed-security-restrictions"></a>Plně spravovaná omezení zabezpečení
Ujistěte se, že organizace podporuje registraci zařízení s plnou správou Android Enterprise tím, že zkontroluje [registraci plně spravovaných zařízení](android-fully-managed-enroll.md#enroll-the-fully-managed-devices). 

## <a name="conditional-access-policies"></a>Zásady podmíněného přístupu
Organizace můžou pomocí zásad podmíněného přístupu Azure AD zajistit, aby uživatelé měli přístup k pracovnímu nebo školnímu obsahu jenom na registrovaných zařízeních s Androidem. K tomu budete potřebovat zásadu podmíněného přístupu, která cílí na všechny potenciální uživatele. Podrobnosti o vytvoření této zásady najdete v v [vyžadovat spravovaná zařízení pro cloudovou aplikaci přístup s podmíněným přístupem](/azure/active-directory/conditional-access/require-managed-devices). 

Postupujte podle kroků v části [scénář: vyžadovat registraci zařízení pro zařízení s iOS a Androidem](/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices), která zajistí, že se k Microsoft 365 koncovým bodům můžou připojit jenom zaregistrovaná mobilní zařízení, která jsou kompatibilní.

## <a name="next-steps"></a>Další kroky

[Nastavení zásad konfigurace aplikací](android-app-configuration-policies.md)