---
title: Zjištění a nastavení odpovědí koncového bodu zabezpečení koncového bodu Intune | Microsoft Docs
description: Nastavení zásad pro zjištění a odpověď koncového bodu zabezpečení koncového bodu v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: e7896d2b5dff7132056ed004443e7fa3623f016e
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820013"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad pro zjišťování a odpověď koncových bodů pro zabezpečení koncových bodů v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro [zjišťování koncových bodů a zásady odezvy](../protect/endpoint-security-edr-policy.md) v uzlu zabezpečení koncového bodu služby Intune.

Podporované platformy a profily:

- **Windows 10 a novější**: tuto platformu použijte pro zásady, které nasadíte do zařízení spravovaných pomocí Intune.
  - Profil: **detekce a odpověď koncového bodu (MDM)**

- **Windows 10 a Windows Server (nástroj ConfigMgr)**: tuto platformu použijte pro zásady, které nasadíte do zařízení spravovaných pomocí Configuration Manager.
  - Profil: **detekce a odpověď koncového bodu (ConfigMgr)**

## <a name="endpoint-detection-and-response-mdm"></a>Detekce a odpověď koncového bodu (MDM)

**Zjištění a odpověď koncového bodu**:

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
  - **Nenakonfigurováno**   (*výchozí*)
  - **Ano**

- **Urychlení četnosti vytváření sestav telemetrie**

  - **Nenakonfigurováno**   (*výchozí*)
  - **Ano** – zvýšit četnost generování sestav telemetrie rozšířené ochrany před internetovými útoky v programu Microsoft Defender

## <a name="endpoint-detection-and-response-configmgr"></a>Zjištění a odpověď koncového bodu (ConfigMgr)

**Zjištění a odpověď koncového bodu**:

- **Sdílení ukázky pro všechny soubory**  

  Vrátí nebo nastaví parametr konfigurace sdílení ukázky rozšířené ochrany před internetovými útoky v programu Microsoft Defender.  
  - **Nenakonfigurováno**   (*výchozí*)
  - **Ano**

- **Urychlení četnosti vytváření sestav telemetrie**

  - **Nenakonfigurováno**   (*výchozí*)
  - **Ano** – zvýšit četnost generování sestav telemetrie rozšířené ochrany před internetovými útoky v programu Microsoft Defender

## <a name="next-steps"></a>Další kroky

[Zásady zabezpečení koncového bodu pro EDR](../protect/endpoint-security-edr-policy.md)
