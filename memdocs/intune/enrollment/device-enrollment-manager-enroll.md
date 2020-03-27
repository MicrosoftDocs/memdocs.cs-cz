---
title: Registrace zařízení pomocí účtu správce registrace zařízení
titleSuffix: Microsoft Intune
description: Naučte se používat účet správce registrace zařízení k registraci zařízení v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6b0c901cd52edcd674a2d787bc703c371dcf519
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327143"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>Registrace zařízení v Intune pomocí účtu správce registrace zařízení

Jeden účet Azure Active Directory s účtem správce registrace zařízení (DEM) můžete použít k registraci až 1000 mobilních zařízení. Správce registrace zařízení je oprávnění Intune, které můžete použít pro uživatelský účet AAD. Toto oprávnění umožňuje zaregistrovat až 1000 zařízení. Účet správce registrace zařízení je užitečný ve scénářích, kdy jsou zařízení zaregistrovaná a připravená na předání uživatelům. V Microsoft Intune v rámci návrhu je limit 150 účtů správce registrace zařízení (DEM).

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>Omezení zařízení zaregistrovaných pomocí účtu DEM

Pro uživatelské účty správce registrace zařízení a zařízení, která jsou zaregistrovaná pod účtem správce registrace zařízení, platí následující omezení:

- Uživateli účtu DEM musí být přiřazena licence Intune.
- Zařízení nemůžete vymazat z Portálu společnosti. Zařízení zaregistrované pod účtem uživatele DEM nemůžete vymazat v Intune na webu Azure Portal.
- V aplikaci nebo na webu Portál společnosti se zobrazí jenom místní zařízení.
- Uživatelské účty DEM nemůžou používat aplikace Apple Volume Purchase Program (VPP) s uživatelskými licencemi programu Apple VPP z důvodu požadavků na Apple ID pro jednotlivé uživatele pro správu aplikací.
- Účty DEM nejde použít při registraci zařízení prostřednictvím automatického zápisu zařízení (ADE) společnosti Apple.
- Aplikace VPP je možné instalovat do zařízení, pokud tato zařízení mají licence Apple VPP.
- Zařízení, které jsou zablokovaná pro podmíněný přístup s výjimkou Windows 10 1803 +
- Všechna zařízení zaregistrovaná pomocí účtů DEM musí být řádně licencovaná, aby je bylo možné spravovat přes Intune. Licence může být Uživatelská licence pro Intune nebo licence k zařízení v Intune.
- Pokud [zaregistrujete zařízení se systémem Android Enterprise Work Profile](android-work-profile-enroll.md) pomocí účtu DEM, je k dispozici omezení 10 zařízení, která je možné zaregistrovat pro každý účet.


## <a name="add-a-device-enrollment-manager"></a>Přidání správce registrace zařízení

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte **zařízení** > **zaregistrovat zařízení** > **správce registrace zařízení**.

2. Vyberte **Přidat**.

3. V okně **Přidat uživatele** zadejte hlavní název uživatele (UPN) pro uživatele DEM a vyberte **Přidat**. Uživatel DEM se přidá do seznamu uživatelů DEM.

## <a name="permissions-for-dem"></a>Oprávnění pro DEM

Role globálního správce nebo správce služby Intune pro Azure AD je potřeba:
- k přiřazení oprávnění DEM uživatelskému účtu Azure AD,
- k zobrazení všech uživatelů DEM.

Pokud uživatel nemá přiřazenou roli globálního správce ani správce služby Intune, ale má povolené oprávnění ke čtení pro přiřazenou roli Správci registrace zařízení, může zobrazit jenom uživatele DEM, které sám vytvořil.


## <a name="remove-device-enrollment-manager-permissions"></a>Odebrání oprávnění správce registrace zařízení

Odebrání správce registrace zařízení neovlivní zaregistrovaná zařízení.

**Odebrání správce registrace zařízení**

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte **zařízení** > **zaregistrovat zařízení** > **správce registrace zařízení**.
2. V okně **Správci registrace zařízení** vyberte uživatele DEM a pak vyberte **Odstranit**.

