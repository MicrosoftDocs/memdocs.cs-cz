---
title: Možnosti registrační metody služby Intune pro zařízení s Windows
titleSuffix: Microsoft Intune
description: Možnosti pro každou metodu registrace pro zařízení s Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 701794ba476f87aaf079e39c834f3e8e3f2c280d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913881"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Možnosti registrační metody služby Intune pro zařízení s Windows
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

Existuje několik způsobů, jak zaregistrovat zařízení zaměstnanců v Intune. Každá metoda má jiné osvědčené postupy a možnosti, jak je znázorněno v následujících tabulkách.

## <a name="best-practices-by-enrollment-method"></a>Osvědčené postupy podle metody registrace
| **Osvědčené postupy** | **[Připojené k Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Služba Azure AD připojená k autopilotu (režim založený na uživateli)](../../autopilot/enrollment-autopilot.md)** |**[Služba Azure AD připojená k autopilotu (režim nasazení sami)](../../autopilot/enrollment-autopilot.md)** |**[Hromadné ingestování](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Spoluspráva](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Běžně používané v EDU|![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Zařízení můžou sloužit jako sdílená zařízení.|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Osobní zařízení musí mít přístup k prostředkům společnosti.|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Samoobslužná údržba aplikací|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Možnosti podle metody registrace

| **Možnosti** | **[Připojené k Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Služba Azure AD připojená k autopilotu (režim založený na uživateli)](../../autopilot/enrollment-autopilot.md)** |**[Služba Azure AD připojená k autopilotu (režim nasazení sami)](../../autopilot/enrollment-autopilot.md)** |**[Hromadné ingestování](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Spoluspráva](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Podmíněný přístup                                      |![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)\*\*|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Uživatel je přidružený k zařízení.                    |![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Vyžaduje Azure AD Premium.                               |![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Zařízení můžete pracovat s prostředky chráněnými certifikační autoritou.             |![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Uživatelé nesmí být správci na svých zařízeních.               |![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Schopnost konfigurace procesu nastavení zařízení        |![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Schopnost zaregistrovat zařízení bez zásahu uživatele      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![×](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Schopnost spouštět powershellové skripty                       |![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/checkmark.png)\*| 
|Podporuje automatickou registraci po připojení k doméně AD.      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Podporuje automatickou registraci po připojení k hybridní službě Azure AD.|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|
|Podporuje automatickou registraci po připojení ke službě Azure AD.       |![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\* Úlohy klientských aplikací v Configuration Manager musí být přesunuté do pilotního nasazení Intune nebo do Intune.

\** [Pro podmíněný přístup se zablokovala zařízení s výjimkou Windows 10 1803 +.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Další kroky

[Nastavení registrace pro Windows](windows-enroll.md)