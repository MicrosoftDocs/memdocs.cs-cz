---
title: Zjištění a nastavení odpovědí koncového bodu zabezpečení koncového bodu Intune | Microsoft Docs
description: Nastavení zásad pro zjištění a odpověď koncového bodu zabezpečení koncového bodu v Microsoft Intune
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
ms.openlocfilehash: dd41cfc0d08771c461e6f681ed18791535202bef
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431313"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad pro zjišťování a odpověď koncových bodů pro zabezpečení koncových bodů v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro *zjišťování koncových bodů a zásady odezvy* v uzlu zabezpečení koncového bodu služby Intune jako součást [zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Podporované platformy a profily:

- **Windows 10 a novější**:
  - Profil: **detekce a odpověď koncového bodu**

## <a name="endpoint-detection-and-response-profile"></a>Zjišťování koncových bodů a profil odpovědi

### <a name="endpoint-detection-and-response"></a>Zjišťování koncových bodů a odpověď

- **Typ balíčku konfigurace klienta ATP v programu Microsoft Defender**

  Nahrajte podepsaný konfigurační balíček, který bude sloužit k připojení klienta Microsoft Defender ATP.

  - **Nenakonfigurováno** (*výchozí*)
  - **Připojování objektu BLOB**  
  - **Objekt BLOB zrušení**  

  Když je nastavená možnost *připojování objektu BLOB*, můžete nakonfigurovat následující nastavení:

  - **Objekt BLOB pro připojování rozšířené ochrany před internetovými útoky**  
    Kliknutím na **Vybrat soubor pro zprovoznění** otevřete podokno *Vybrat soubor k zprovoznění* , kde zadáte `.onboarding` soubor.

  Když nastavíte možnost odinstalace na stavový *objekt BLOB*, můžete nakonfigurovat následující nastavení:
  
  - **Objekt BLOB pro zrušení rozšířené ochrany před internetovými útoky**  
     Kliknutím na **Vybrat soubor** pro zrušení otevřete podokno *Vybrat soubor* pro oddálení, kde zadáte `.offboarding` soubor.

- **Sdílení ukázky pro všechny soubory**  

  Vrátí nebo nastaví parametr konfigurace sdílení ukázky rozšířené ochrany před internetovými útoky v programu Microsoft Defender.  
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

- **Urychlení četnosti vytváření sestav telemetrie**

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zvýšit četnost generování sestav telemetrie rozšířené ochrany před internetovými útoky v programu Microsoft Defender

## <a name="next-steps"></a>Další kroky

[Zásady zabezpečení koncového bodu pro EDR](../protect/endpoint-security-edr-policy.md)
