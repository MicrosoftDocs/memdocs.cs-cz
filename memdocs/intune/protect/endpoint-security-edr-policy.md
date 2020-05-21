---
title: Správa nastavení zjišťování koncových bodů a odpovědí pomocí zásad zabezpečení Endpoint v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady pro zařízení, která spravujete pomocí zásad zjišťování koncových bodů zabezpečení koncového bodu a zásad odezvy ve službě Microsoft Endpoint Manager.
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
ms.openlocfilehash: 3ca9d8f1db36856d9d696a2a1c3933ff4a54b7c3
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431305"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Zjišťování koncových bodů a zásady odezvy pro zabezpečení koncového bodu v Intune

Při integraci služby Defender ATP s Intune můžete použít zásady zabezpečení koncového bodu pro zjišťování koncových bodů a odpověď (EDR) ke správě nastavení EDR a připojení zařízení ke službě Defender ATP.

Možnosti detekce a reakce koncových bodů ATP v programu Microsoft Defender poskytují pokročilé detekce útoků téměř v reálném čase a napadnutelné. Analytici zabezpečení můžou efektivně upřednostňovat výstrahy, získávat přehled o plném rozsahu porušení a reagovat na reakce na nápravu hrozeb.

Zásady zabezpečení koncového bodu pro EDR najdete v části *Správa* v uzlu **Security Endpoint** v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Zobrazit [nastavení pro zjišťování koncových bodů a profily odpovědí](../protect/endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-profiles"></a>Předpoklady pro profily EDR

- Windows 10 nebo novější
- Aby mohla služba Intune spravovat zjišťování koncových bodů a nastavení odpovědí na zařízení, musíte zařízení připojit do programu Defender ATP.

## <a name="edr-profiles"></a>Profily EDR

**Profily Windows 10**:

- **Zjištění a odpověď koncového bodu** – umožňuje spravovat [nastavení pro detekci a odpověď koncového bodu služby Microsoft Defender ATP](endpoint-security-edr-profile-settings.md).

  Možnosti detekce a reakce koncových bodů ATP v programu Microsoft Defender poskytují pokročilé detekce útoků téměř v reálném čase a napadnutelné.

  Další informace najdete v tématu [zjištění a odpověď koncového bodu](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) v dokumentaci ke službě Microsoft Defender atp.

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
