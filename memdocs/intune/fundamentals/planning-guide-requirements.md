---
title: Určení požadavků na scénáře použití
titleSuffix: Microsoft Intune
description: Tento článek vám pomůže určit požadavky ve scénářích a dílčích scénářích použití při cloudové implementaci Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: fd8cb5f7-19f0-4d80-8825-2bafa49624af
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 76d1141a1c4dd442f6fb94a06b5d20adc8c7fa77
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996329"
---
# <a name="determine-use-case-scenario-requirements"></a>Určení požadavků na scénáře použití

V této části určíte požadavky každé organizační skupiny při každém scénáři použití. Tento postup vám pomůže připravit se na další oblasti plánování nasazení Intune, jako je architektura, návrh, registrace a zavedení. Pomůže vám také identifikovat možné mezery a problémy spojené s projektem nasazení Intune.

Každý scénář nebo dílčí scénář použití může mít jinou množinu požadavků a jiné přidružené organizační skupiny a platformy mobilních zařízení. V požadavcích společnosti na určitý scénář použití například může být, že při registraci zařízení do Intune je potřeba použít přísnější sadu nastavení, která zahrnuje šestiznakový PIN nebo zákaz záloh do cloudu. Scénář použití pro uživatele s vlastním zařízením (BYOD) může být méně přísný, takže povolí čtyřznakový PIN a zálohování do cloudu.

Ve scénáři firemního použití také můžete mít organizační skupiny s různými sadami požadavků (např. nastavení kódu PIN, Wi-Fi, profilu VPN a nasazených aplikací). Požadavky také mohou být dány možnostmi platformy mobilního zařízení (např. čtečka otisku prstů nebo e-mailový profil).

Tady je několik příkladů požadavků na případy použití organizace, které ukazují různé sady požadavků pro každý scénář použití a dílčí scénář použití, organizační skupinu a platformu mobilních zařízení. Následující tabulku můžete použít také k zadání požadavků na případ použití vaší organizace:

| **Případy použití** | **Dílčí případy použití** | **Skupiny** | **Platformy zařízení** | **Požadavky** |
|:---:|:---:|:---:|:---:|:---:|
| Firemní | Informatik | Personalistika, finance | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |                                                          
| Firemní | Vedení | Personalistika, finance | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |                                                         
| Firemní | Kiosk | Retail | Android | Nastavení zařízení, profily, aplikace |
| BYOD | Informatik | Marketing, prodej | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |                                                         
| BYOD | Vedení | Marketing, prodej | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |

Můžete [si stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a zadat požadavky na případy použití a dílčího případu použití vaší organizace.


## <a name="examples-of-requirements"></a>Příklady požadavků

Tady jsou další příklady požadavků, které můžete použít ve sloupci Požadavky:

- **Zabezpečený e-mail**
  - Podmíněný přístup pro Exchange Online nebo místní Exchange
  - Zásady ochrany aplikace Outlook

- **Nastavení zařízení**
  - Nastavení čtyřmístného nebo šestimístného kódu PIN
  - Zákaz zálohování do cloudu

- **Profily**
  - Wi-Fi
  - Síť VPN
  - E-mail (Windows 10 Mobile)

- **Aplikace**
  - Microsoft 365 se zásadami ochrany aplikací
  - Obchodní aplikace se zásadami ochrany

## <a name="next-steps"></a>Další kroky

V další části najdete pokyny pro [přípravu plánu spuštění Intune](planning-guide-rollout-plan.md).
