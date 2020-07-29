---
title: Monitorování integrace rozšířené ochrany před internetovými útoky v programu Microsoft Defender (ATP) v Microsoft Intune – Azure | Microsoft Docs
description: Monitorujte rozšířenou ochranu před internetovými útoky v programu Microsoft Defender (ATP Microsoft Defender) s Intune, včetně dodržování předpisů a stavu připojování zařízení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264471"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Monitorování stavu zařízení při integraci služby Microsoft Defender ATP s Intune

Když integrujete Microsoft Intune a službu Microsoft Defender Advanced Threat Protection (ATP), můžete zobrazit informace o dodržování předpisů a registraci zařízení v centru pro správu Microsoft Endpoint Manager.

## <a name="monitor-device-compliance"></a>Monitorování dodržování předpisů zařízením

Monitorujte stav zařízení, která mají zásady dodržování předpisů ATP v programu Microsoft Defender.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení**  >  **monitorování**  >  **dodržování zásad**.

3. Vyhledejte v seznamu Zásady ochrany ATP v programu Microsoft Defender a podívejte se, která zařízení jsou kompatibilní nebo nekompatibilní.

Můžete také použít *provozní* sestavu pro zařízení nedodržující předpisy ze stejného umístění:

- Vyberte **zařízení**  >  **monitorovat**  >  **zařízení, která nedodržují předpisy**.

Další informace o sestavách najdete v tématu [sestavy Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Zobrazit stav zprovoznění

Pokud chcete zobrazit stav připojování vašich zařízení spravovaných přes Intune, přečtěte si část **Security Endpoint Security**v  >  **programu Microsoft Defender ATP**. Na této stránce můžete také vytvořit profil konfigurace zařízení, který bude začlenit další zařízení do ATP programu Microsoft Defender.

## <a name="next-steps"></a>Další kroky

[Vymáhání dodržování předpisů pro Microsoft Defender ATP pomocí podmíněného přístupu v Intune](../protect/advanced-threat-protection.md)
