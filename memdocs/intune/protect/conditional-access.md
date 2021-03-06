---
title: Podmíněný přístup s Microsoft Intune
titleSuffix: Microsoft Intune
description: Naučte se definovat podmínky, které uživatelé, zařízení a aplikace musí splnit, aby měli přístup k prostředkům společnosti v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/06/2018
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2284af22d25329fad74a7559030520a187a7c38a
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992921"
---
# <a name="learn-about-conditional-access-and-intune"></a>Další informace o podmíněném přístupu a Intune

Pomocí podmíněného přístupu můžete řídit zařízení a aplikace, které se můžou připojit k e-mailu a prostředkům společnosti. 

Enterprise Mobility + Security (EMS) není samostatný produkt. Jedná se o řešení, které se účastní všech služeb a produktů, které jsou součástí EMS. Podmíněný přístup poskytuje podrobné řízení přístupu, které zajistí zabezpečení firemních dat a současně uživatelům poskytuje prostředí, které jim umožní provádět jejich nejlepší práci z libovolného zařízení a z libovolného místa.

Můžete definovat podmínky, které omezují přístup k podnikovým datům podle polohy, zařízení, stavu uživatele a „choulostivosti“ aplikace.

> [!NOTE]
> Podmíněný přístup také rozšiřuje své možnosti na [Microsoft 365 služby](/office365/enterprise/office-365-client-support-conditional-access).

![Diagram podmíněného přístupu](./media/conditional-access/ca-diagram-1.png)

## <a name="use-conditional-access-with-intune"></a>Použití podmíněného přístupu s Intune

Podmíněný přístup je Azure Active Directory funkce, která je součástí licence Azure Active Directory Premium. Intune tuto funkci vylepšuje tím, že do řešení přidává dodržování předpisů pro mobilní zařízení a správu mobilních aplikací. 

![Intune a podmíněný přístup při použití EMS](./media/conditional-access/intune-with-ca-1.png)

Způsoby použití podmíněného přístupu s Intune:

- **Podmíněný přístup podle zařízení**

  - Podmíněný přístup pro místní Exchange

  - Podmíněný přístup na základě řízení přístupu k síti

  - Podmíněný přístup na základě rizika zařízení

  - Podmíněný přístup pro počítače s Windows

    - Ve vlastnictví firmy

    - Přineste si vlastní zařízení (BYOD)

- **Podmíněný přístup založený na aplikacích**

## <a name="next-steps"></a>Další kroky

[Běžné způsoby použití podmíněného přístupu s Intune](conditional-access-intune-common-ways-use.md)