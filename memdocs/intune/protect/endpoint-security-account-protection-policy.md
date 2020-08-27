---
title: Správa nastavení ochrany účtů útoků pomocí zásad zabezpečení Endpoint v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady pro zařízení, která spravujete pomocí zásad ochrany účtů služby Endpoint Security ve Správci Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f08282fe6bd8675474415290d50c0b07b4e1fc25
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915054"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Zásady ochrany účtů pro zabezpečení koncového bodu v Intune

Zásady zabezpečení koncového bodu služby Intune se používají pro ochranu účtů k ochraně identity a účtů uživatelů. Zásady ochrany účtů se zaměřují na nastavení pro Windows Hello a Credential Guard, které je součástí správy identit a přístupu Windows.

- *Windows Hello pro firmy* nahrazuje hesla se silným dvojúrovňovém ověřováním na počítačích a mobilních zařízeních.
- *Credential Guard* pomáhá chránit přihlašovací údaje a tajné klíče, které používáte s vašimi zařízeními.

Další informace najdete v tématu [Správa identit a přístupu](/windows/security/identity-protection/) v dokumentaci pro správu identit a přístupu Windows.

Zásady zabezpečení koncového bodu pro ochranu účtu najdete v části *Správa* v uzlu **zabezpečení koncového** bodu v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Zobrazit [Nastavení profilů ochrany účtů](../protect/endpoint-security-asr-profile-settings.md)

## <a name="prerequisites-for-account-protection-profiles"></a>Předpoklady pro profily ochrany účtů

- Windows 10 nebo novější

## <a name="account-protection-profiles"></a>Profily ochrany účtů

*Profily ochrany účtů jsou ve verzi Preview*.

**Profily Windows 10**:

- **Ochrana účtů** *(Preview)* – nastavení zásad ochrany účtů vám pomůžou chránit přihlašovací údaje uživatele.

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)