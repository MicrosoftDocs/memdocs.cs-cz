---
title: Přidání a přiřazení aplikace Portál společnosti pro Windows 10 pro zařízení s autopilotem zřízeným autopilotem
titleSuffix: Microsoft Intune
description: Přidejte a přiřaďte aplikaci Windows 10 Portál společnosti k Intune pro zřízená zařízení s autopilotem.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
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
ms.openlocfilehash: ec131df32e06c1c43b8904dde732b4e6a17a91aa
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323819"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Přidání a přiřazení aplikace Portál společnosti pro Windows 10 pro zařízení s autopilotem zřízeným autopilotem

Pokud chcete spravovat zařízení a instalovat aplikace, můžou uživatelé používat aplikaci Portál společnosti. Aplikaci Portál společnosti pro Windows 10 můžete přiřadit přímo z Intune. 

## <a name="prerequisites"></a>Požadavky

Pro zařízení s autopilotem s Windows 10 se doporučuje přidružit účet Microsoft Store pro firmy k Intune. Další informace najdete v tématu [Správa hromadně zakoupených aplikací z Microsoft Store pro firmy s Microsoft Intune](windows-store-for-business.md).

Portál společnosti (offline) se volí k instalaci pomocí následujících kroků. Aplikace Portál společnosti se nainstaluje v kontextu zařízení, když se přiřadí do skupiny autopilots, a před přihlášením uživatele se nainstaluje do zařízení. 

## <a name="configure-settings-to-show-offline-app"></a>Konfigurovat nastavení pro zobrazení offline aplikace

1. Přihlaste se k [Microsoft Storu pro firmy](https://www.microsoft.com/business-store) pomocí svého účtu správce.
2. Vyberte kartu **Spravovat** v horní části okna.
3. V levém podokně vyberte **Nastavení**.
4. V části **Prostředí nakupování** nastavte **Zobrazovat offline aplikace** na **Zapnuto**.  
    Zobrazí se aplikace licencované offline.

## <a name="get-the-offline-company-portal-app"></a>Získání offline aplikace Portál společnosti

1. Vyhledejte a vyberte aplikaci **Portál společnosti**.
2. Nastavte **Typ licence** na **Offline**.
3. Výběrem možnosti **Získat aplikaci** offline aplikaci Portál společnosti získejte a přidejte do svého inventáře.

## <a name="assign-the-company-portal-app"></a>Přiřazení aplikace Portál společnosti

1. Přihlaste se k [centru pro správu Microsoft Endpoint manageru](https://go.microsoft.com/fwlink/?linkid=2109431) s vaším účtem správce. 
2. V pravém podokně vyberte kartu **aplikace** .
3. V části **podle platformy**vyberte **Windows**.
4. Vyberte **portál společnosti (offline)** .
5. Musíte buď počkat, než se plán synchronizace dokončí, nebo proveďte ruční synchronizaci z centra pro správu Microsoft Endpoint Manageru.
6. Přiřaďte aplikaci Portál společnosti jako požadovanou aplikaci pro vybrané skupiny zařízení autopilot.

## <a name="next-steps"></a>Další kroky

- Další informace o přiřazování aplikací najdete v tématu [přiřazení aplikací do skupin](apps-deploy.md).

