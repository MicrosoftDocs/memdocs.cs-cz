---
title: Volitelná diagnostická data z klientských aplikací Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o volitelných diagnostických datech, která klientské aplikace Intune shromažďují.
keywords: Ochrana osobních údajů, osobní údaje
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5d78438301e8469189d0c70a2cf52b58938e277
ms.sourcegitcommit: 37dc6b78de8bb904b83a9d571f3c9f414b54f321
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "90864495"
---
# <a name="optional-diagnostic-data-from-intune-client-apps"></a>Volitelná diagnostická data z klientských aplikací Intune

Intune shromažďuje různá volitelná data pro detekci, diagnostiku a opravu problémů uživatelů prostřednictvím různých klientských aplikací Intune. Mezi klientské aplikace Intune patří:
- iOS/iPadOS Portál společnosti
- macOS Portál společnosti
- Portál společnosti Windows
- Portál společnosti pro Android
- Aplikace Intune pro Android
- postranní vozík macOS
- Postranní vozík Windows
- Správa mobilních aplikací pro Android (MAM)

Nepovinná data shromážděná z klientů se nevyžadují k úspěšnému spuštění služeb Intune. Shromážděná data pomáhají:
- Můžeme zvýšit vylepšení produktů.
- Poskytuje rozšířené informace, které nám pomůžou detekovat, diagnostikovat a opravovat problémy.

## <a name="data-collected"></a>Shromažďovaná data

Volitelná diagnostická data shromažďovaná klientskými aplikacemi Intune mohou zahrnovat následující oblasti:

- Informace o uživateli generované společností Microsoft
    - ID uživatele Azure AD
    - ID zařízení
    - ID korelace
    - Identifikátor GUID relace aplikace
    - ID uživatele sady SDK
- Informace o správci a účtu
    - ID tenanta
    - ID tenanta Azure AD
- Informace o hardwaru a softwaru
    - Verze operačního systému zařízení
    - Model zařízení
    - Značka zařízení
    - ID aplikace
    - Jazyk uživatele
    - Časové pásmo uživatele
- Události a informace o chybě služby
    - Událost zápisu
    - Událost selhání
        - Chyba sítě
        - Běhové selhání
        - Selhání plánu úlohy
        - Selhání registrace
        - Chyba ověřování Azure AD
    - Zpráva o selhání
    - Stav souhlasu
    - Stav dodržování předpisů
    - Stav zásad
- Události Portál společnosti
    - Chyba Portál společnosti
    - Akce stránky Portál společnosti
    - Portál společnosti zobrazení stránky
    - Verze Portál společnosti
- Měření výkonu
    - Doba trvání
    - Doba odezvy
 
## <a name="data-not-collected"></a>Neshromážděná data
Data neobsahují žádné informace o zákaznících, třeba:
- Název zařízení
- Telefonní číslo.
- Obsah pro soubory nebo fotografii uživatele

## <a name="turn-off-data-collection"></a>Vypnutí shromažďování dat
Uživatelé můžou z aplikace nastavení vypnout [shromažďování dat o využití](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android) pro jednotlivá zařízení.


## <a name="next-steps"></a>Další kroky

[Přečtěte si další informace o shromažďování dat v Intune.](privacy-data-collect.md)



