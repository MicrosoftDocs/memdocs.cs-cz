---
title: Přidání a přiřazení aplikace Portál společnosti pro Windows 10 pro zařízení s autopilotem zřízeným autopilotem
titleSuffix: Microsoft Intune
description: Přidejte a přiřaďte aplikaci Windows 10 Portál společnosti k Intune pro zřízená zařízení s autopilotem.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559517"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Přidání a přiřazení aplikace Portál společnosti pro Windows 10 pro zařízení s autopilotem zřízeným autopilotem

Pokud chcete spravovat zařízení a instalovat aplikace, můžou uživatelé používat aplikaci Portál společnosti. Aplikaci Portál společnosti pro Windows 10 můžete přiřadit přímo z Intune. 

## <a name="prerequisites"></a>Požadavky

Pro zařízení s autopilotem s Windows 10 se doporučuje přidružit účet Microsoft Store pro firmy k Intune. Další informace najdete v tématu [Správa hromadně zakoupených aplikací z Microsoft Store pro firmy s Microsoft Intune](windows-store-for-business.md).

Aplikaci **portál společnosti (offline)** si můžete nainstalovat pomocí následujícího postupu. Aplikace Portál společnosti se nainstaluje v kontextu zařízení, když se přiřadí do skupiny autopilots, a před přihlášením uživatele se nainstaluje do zařízení.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>Konfigurace nastavení úložiště pro zobrazení offline aplikace

1. Přihlaste se k [Microsoft Storu pro firmy](https://www.microsoft.com/business-store) pomocí svého účtu správce.
2. Vyberte kartu **Spravovat** v horní části okna.
3. V levém podokně vyberte **Nastavení**.
4. V části **Prostředí nakupování** nastavte **Zobrazovat offline aplikace** na **Zapnuto**.  
   Zobrazí se aplikace licencované offline.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>Získání offline aplikace Portál společnosti ze Storu

1. Vyhledejte a vyberte aplikaci **Portál společnosti**.
2. Nastavte **Typ licence** na **Offline**.
3. Výběrem možnosti **Získat aplikaci** offline aplikaci Portál společnosti získejte a přidejte do svého inventáře.
   Aby se aplikace vyzobrazovala v Intune, musíte buď počkat na dokončení plánu synchronizace, nebo provést ruční synchronizaci z centra pro správu Microsoft Endpoint Manageru.

## <a name="manually-sync-company-portal-app-with-intune"></a>Ruční synchronizace Portál společnosti aplikace s Intune

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)   pomocí účtu správce.
2. Vyberte možnost konektory **správy tenanta**  >  **a tokeny**  >  **Microsoft Store pro firmy**.
3. Klikněte na **Povolit**.
4. Pokud jste to ještě neudělali, klikněte na odkaz pro registraci Microsoft Storu pro firmy a podle předchozího postupu přidružte svůj účet.
5. V rozevíracím seznamu **Jazyk** vyberte jazyk, ve kterém se aplikace z Microsoft Storu pro firmy zobrazují na portálu Azure Portal. Bez ohledu na jazyk, ve kterém se budou zobrazovat, se nainstalují v jazyce koncového uživatele, pokud je dostupný.
6. Kliknutím na **Synchronizovat** přeneste aplikace zakoupené v Microsoft Storu do Intune.

## <a name="assign-the-company-portal-app"></a>Přiřazení aplikace Portál společnosti

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)   pomocí účtu správce.
2. Vyberte **aplikace**  >  **okna**.
3. V seznamu aplikací pro Windows vyberte možnost **portál společnosti (offline)**.
4. [Přiřaďte](apps-deploy.md) aplikaci Portál společnosti jako požadovanou aplikaci pro vybrané skupiny zařízení autopilot.

## <a name="next-steps"></a>Další kroky

- Další informace o přiřazování aplikací najdete v tématu [přiřazení aplikací do skupin](apps-deploy.md).

