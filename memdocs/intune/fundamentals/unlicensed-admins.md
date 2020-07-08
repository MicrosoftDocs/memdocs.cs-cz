---
title: Nelicencovaná správci v Microsoft Intune
description: Přečtěte si, jak udělit nelicencovaným správcům oprávnění k přístupu k Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6dcd41377234bbb1b40e513f16c3393d763b17f
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088186"
---
# <a name="unlicensed-admins"></a>Nelicencovaní správci

Správci služby Intune a správce koncového bodu Microsoftu můžete udělit přístup ke správcům bez licencí Intune.

1. Přihlaste se k centru pro správu [služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Tenant administration**  >  **role**  >  **Správce klienta Správa licencí**.
2. Vyberte možnost **Povolení přístupu k nelicencovaným správcům**  >  **Ano**.
    >[!WARNING]
    >Po kliknutí na **Ano**toto nastavení nemůžete zrušit.

3. Od této chvíle se uživatelé, kteří se přihlásí do centra pro správu služby Microsoft Endpoint Manager, nemusejí zažádat o licenci Intune. Jejich rozsah přístupu je definován rolemi, které jsou jim přiřazeny.

Intune podporuje až 350 správců s nelicencovanými licencemi na jednu skupinu zabezpečení a vztahuje se jenom na přímé členy. Správci nad tímto limitem budou mít nepředvídatelné chování.




