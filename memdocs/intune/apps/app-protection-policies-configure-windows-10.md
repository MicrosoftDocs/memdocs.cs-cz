---
title: Konfigurace zásad ochrany aplikací pro Windows 10
titleSuffix: Microsoft Intune
description: Toto téma popisuje, jak nakonfigurovat zásady ochrany aplikací (APP) pro zařízení s Windows 10.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83eccdddd1cc38f72c949c80c4a1488b09920f94
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988698"
---
# <a name="get-ready-for-windows-information-protection-in-windows-10"></a>Příprava pro Windows Information Protection ve Windows 10 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Povolte správu mobilních aplikací (MAM) pro Windows 10 nastavením zprostředkovatele MAM v Azure AD. Nastavení poskytovatele MAM v Azure AD vám umožní definovat stav registrace při vytváření nových zásad WIP (Windows Information Protection) s Intune. Stav registrace může být MAM nebo MDM (správa mobilních zařízení).

## <a name="to-configure-the-mam-provider"></a>Konfigurace poskytovatele MAM

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **všechny služby** a zvolte **M365 Azure Active Directory** pro přepnutí řídicích panelů.
3. Vyberte **Azure Active Directory**.
4. Ve skupině **Spravovat** zvolte **Mobilita (MDM a MAM)**.
5. Klikněte na **Microsoft Intune**.
6. Nakonfigurujte nastavení ve skupině **Obnovit výchozí adresy URL mam** v podokně **Konfigurace** .

   **Obor uživatele MAM**  
   Pomocí automatické registrace MAM můžete spravovat podniková data na zařízeních zaměstnanců, která používají Windows. Automatická registrace MAM se nakonfiguruje pro scénáře typu Přineste si vlastní zařízení.<ul><li>**Žádné**<br>Vyberte, pokud se do MAM nemůžou zaregistrovat žádní uživatelé.</li><li>**Některé**<br>Vyberte skupiny Azure AD obsahující uživatele, kteří budou zaregistrováni do MAM.</li><li>**Vše**<br>Vyberte, pokud se do MAM můžou zaregistrovat všichni uživatelé.</li></ul>

   **Adresa URL podmínek použití služby MAM**  
   Adresa URL podmínek použití služby MAM není pro Microsoft Intune podporovaná. Aby zásady ochrany platily, musí toto vstupní pole zůstat prázdné.

   **Adresa URL zjišťování MAM**  
   Adresa URL koncového bodu pro registraci do služby MAM. Koncový bod registrace se používá k registraci zařízení do správy službou MAM.

   **Adresa URL s předpisy služby MAM**  
   Adresa URL s předpisy služby MAM není pro Microsoft Intune podporovaná. Aby zásady ochrany platily, musí toto vstupní pole zůstat prázdné. 

7. Klikněte na **Uložit**.

## <a name="next-steps"></a>Další kroky

[Vytvoření zásady nedokončené výroby](windows-information-protection-policy-create.md)
