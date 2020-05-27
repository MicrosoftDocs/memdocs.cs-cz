---
title: Pochopení mezi omezeními služby Intune a omezením počtu zařízení Azure
titleSuffix: ''
description: Seznamte se s rozdíly mezi omezeními omezení počtu zařízení v Intune a omezeními vymezenými v Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8610b619a4ac05f37b893060b3b3a2bcb1dae528
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864850"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Principy omezení limitu počtu zařízení v Intune a Azure AD

Omezení limitu počtu zařízení se dají konfigurovat dvěma způsoby:
- Registrace v Intune
- Služba Azure Active Directory (AD) připojena nebo byla zaregistrována služba Azure AD

Tento článek vysvětluje, kdy se tato omezení uplatní v závislosti na vaší konfiguraci.

## <a name="intune-device-limit-restrictions"></a>Omezení limitu počtu zařízení v Intune

Omezení limitu počtu zařízení v Intune nastaví maximální počet zařízení, která může uživatel ovládat (maximální nastavení je 15). Pokud chcete tento **limit zařízení**nastavit, v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)na  >  **zařízení**  >  **omezení registrace**. Další informace najdete v tématu [Vytvoření omezení limitu počtu zařízení](enrollment-restrictions-set.md#create-a-device-limit-restriction) .

## <a name="azure-device-limit-restriction"></a>Omezení limitu počtu zařízení Azure

Omezení limitu počtu zařízení Azure nastaví maximální počet zařízení, která jsou buď připojená k Azure AD nebo v registrech Azure AD. Pokud chcete nastavit **maximální počet zařízení na uživatele**, použijte Azure Portal > **Azure Active Directory**  >  **zařízení**. Další informace najdete v tématu [Konfigurace nastavení zařízení](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal) .

## <a name="settings-applied-based-on-user-affinity"></a>Nastavení použité na základě přidružení uživatele

Pokud máte nastavené omezení omezení počtu zařízení v Intune i Azure, v následující tabulce se dozvíte, co se používá v závislosti na Nastavení spřažení uživatele.

| Platforma zařízení | Přidružení uživatele | Platí pro Azure | Intune platí |
| ----- | ----- | ----- | ----- | ----- |
| Pracovní profil Android Enterprise | Ano | Ano | Ano|
| Zařízení se systémem Android Enterprise vyhrazené | Ne | Ne | Ne |
| Plně spravovaná platforma Android Enterprise | Ano | Ano | Ano |
| Správce zařízení s Androidem | Ano | Ano | Ano |
| Správce zařízení s Androidem DEM | Ne | | Ne | 
| iOS/macOS BYOD | Ano | Ano | Ano |
| iOS/macOS – automatický zápis zařízení (ADE) | Ano | Ano | Ano |
| iOS/macOS ADE | Ne | Ano | Ne |
| BYOD Windows | Ano | Ano | Ano |
| Pouze Windows MD | | Ano | Ano |
| Připojeno k Windows Azure AD| Ano | Ano | Ne |
| Windows Autopilot | Ano | Ano | Ne |
| Připojeno k hybridní službě Azure AD pro Windows | Ne | Ne | Ano |
| Spoluspráva Windows | Ne | Ano | Ne |
| Windows DEM | Ne | Ano | Ne |
| Hromadná registrace Windows | Ne | Ano | Ne |


## <a name="android-and-ios-devices"></a>Zařízení s Androidem a iOS

### <a name="ios-or-android-devices-example-1"></a>Příklad 1 zařízení se systémem iOS nebo Android

- Nastavení **maximální počet zařízení na uživatele** v Azure je nastavené na 3.
- Nastavení **limitu zařízení** v Intune je nastavené na 5.
 
**Výsledek:** Maximální počet je na uživatele. Pokud například zaregistrujete tři zařízení Intune, registrace Azure pro čtvrté zařízení selže z důvodu nastavení omezení počtu registrací pro zařízení.

### <a name="ios-or-android-devices-example-2"></a>Příklad 2 zařízení s iOS nebo Androidem

- Nastavení **maximální počet zařízení na uživatele** v Azure je nastavené na 20.
- Nastavení **limitu zařízení** v Intune je nastavené na 2.

**Výsledek:** Můžete úspěšně zaregistrovat a zaregistrovat dvě zařízení. Registrace v Intune bude zablokovaná pro všechna další zařízení. ADE bez přidružení uživatele je omezeno omezeními registrace zařízení Azure, přestože není přidruženo k uživateli.

## <a name="windows-devices"></a>Zařízení s Windows

Omezení limitu počtu zařízení v Intune se nevztahují na tyto typy zápisu Windows:
- Spoluspravované registrace
- Registrace objektů zásad skupiny (GPO)
- Registrace připojená k Azure AD
- Hromadné registrace připojené k Azure AD
- Registrace autopilotu
- Registrace správce registrace zařízení

Omezení limitu počtu zařízení pro tyto typy registrace nemůžete vyhodnotit, protože se považují za scénáře sdíleného zařízení. Můžete nastavit omezení pro tyto typy zápisu v Azure Active Directory.

Pro omezení limitu počtu zařízení v Azure se **maximální počet zařízení na uživatele** vztahuje na zařízení, která jsou buď připojená ke službě Azure AD, nebo v zaregistrovaných Azure AD. Toto nastavení se nevztahuje na zařízení připojená k hybridní službě Azure AD.

### <a name="windows-10-example-1"></a>Příklad Windows 10 – příklad 1

- Nastavení **maximální počet zařízení na uživatele** v Azure je nastavené na 5.
- Nastavení **limitu zařízení** v Intune je nastavené na 3.
- Zařízení jsou připojená k hybridní službě Azure AD a zaregistrovaná automaticky (objekt zásad skupiny je nakonfigurovaný).

**Výsledek:** Vzhledem k tomu, že se registrace provedla prostřednictvím objektu zásad skupiny, se limit registrace zařízení Azure nepoužije.  Omezení limitu počtu zařízení v Intune se taky netýká.

### <a name="windows-10-example-2"></a>Příklad Windows 10 – příklad 2

- Nastavení **maximální počet zařízení na uživatele** v Azure je nastavené na 5.
- Nastavení **limitu zařízení** v Intune je nastavené na 2.
- Zařízení jsou připojená k místní doméně a zaregistrovaná pomocí **Nastavení**  >  **přístup do práce nebo do školy**  >  **připojit**.

**Výsledek:** Před zablokováním můžete zaregistrovat jenom dvě zařízení. Můžete zaregistrovat až pět zařízení.


## <a name="next-steps"></a>Další kroky

- [Vytvořte omezení limitu počtu zařízení v Azure.](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Nakonfigurujte nastavení zařízení v Azure.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Přečtěte si další informace o registraci a připojených doménách.](https://docs.microsoft.com/azure/active-directory/devices/overview#getting-devices-in-azure-ad)
