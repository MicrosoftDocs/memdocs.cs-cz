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
ms.openlocfilehash: 6e002b62fb00c4e2e8523848c4c64ad7a54ce024
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331035"
---
# <a name="determine-use-case-scenario-requirements"></a>Určení požadavků na scénáře použití

V této části určíte požadavky každé organizační skupiny při každém scénáři použití. Tento postup vám pomůže připravit se na další oblasti plánování nasazení Intune, jako je architektura, návrh, registrace a zavedení. Pomůže vám také identifikovat možné mezery a problémy spojené s projektem nasazení Intune.

Každý scénář nebo dílčí scénář použití může mít jinou množinu požadavků a jiné přidružené organizační skupiny a platformy mobilních zařízení. V požadavcích společnosti na určitý scénář použití například může být, že při registraci zařízení do Intune je potřeba použít přísnější sadu nastavení, která zahrnuje šestiznakový PIN nebo zákaz záloh do cloudu. Scénář použití pro uživatele s vlastním zařízením (BYOD) může být méně přísný, takže povolí čtyřznakový PIN a zálohování do cloudu.

Ve scénáři firemního použití také můžete mít organizační skupiny s různými sadami požadavků (např. nastavení kódu PIN, Wi-Fi, profilu VPN a nasazených aplikací). Požadavky také mohou být dány možnostmi platformy mobilního zařízení (např. čtečka otisku prstů nebo e-mailový profil).

Tady je několik příkladů scénářů použití v organizaci s různými sadami požadavků pro každý scénář nebo dílčí scénář použití, organizační skupinu a platformu mobilního zařízení. Požadavky na případy použití v organizaci také můžete zadat do následující tabulky:

| **Případy použití** | **Dílčí případy použití** | **Skupiny** | **Platformy zařízení** | **Requirements** |
|:---:|:---:|:---:|:---:|:---:|
| Firemní | Informatik | Personální, finanční oddělení | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |                                                          
| Firemní | Vedení | Personální, finanční oddělení | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |                                                         
| Firemní | Veřejný terminál | Maloobchod | Android | Nastavení zařízení, profily, aplikace |
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Informatik | Marketing, prodej | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |                                                         
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Vedení | Marketing, prodej | iOS/iPadOS | Zabezpečený e-mail, nastavení zařízení, profily, aplikace |

Pokud chcete zadat požadavky na scénáře použití a dílčí scénáře použití ve vaší organizaci, [stáhněte si šablonu předchozí tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0).


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
  - Office 365 se zásadami ochrany aplikace
  - Obchodní aplikace se zásadami ochrany

## <a name="next-steps"></a>Další kroky

V další části najdete pokyny pro [přípravu plánu spuštění Intune](planning-guide-rollout-plan.md).
