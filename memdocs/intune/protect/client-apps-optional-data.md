---
title: Volitelná diagnostická data z klientských aplikací Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o volitelných diagnostických datech, která klientské aplikace Intune shromažďují.
keywords: Ochrana osobních údajů, osobní údaje
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/15/2020
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
ms.openlocfilehash: e4d8833860b5c16375e5a68ea0174d81357df819
ms.sourcegitcommit: bcfacddbee1faa3826eea89697018450dfa9d264
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2020
ms.locfileid: "91134845"
---
# <a name="optional-diagnostic-data-from-intune-client-apps"></a>Volitelná diagnostická data z klientských aplikací Intune

Intune shromažďuje různá volitelná data pro detekci, diagnostiku a opravu problémů uživatelů prostřednictvím různých klientských aplikací Intune.  Tato volitelná diagnostická data shromažďujeme, abychom vám pomohli aktivně detekovat problémy ve vaší organizaci, aby je bylo možné vyřešit dřív, než se stanou problémem. Mezi klientské aplikace Intune patří:
- iOS/iPadOS Portál společnosti
- macOS Portál společnosti
- Portál společnosti Windows
- Portál společnosti pro Android
- Aplikace Intune pro Android
- Agent pro správu Microsoft Intune pro macOS
- Rozšíření pro správu Microsoft Intune
- Správa mobilních aplikací pro Android (MAM)

Nepovinná data shromážděná z klientů se nevyžadují k úspěšnému spuštění služeb Intune. Shromážděná data pomáhají:
- Poskytuje rozšířené informace, které nám pomůžou aktivně detekovat, diagnostikovat a opravovat problémy.
- Provede vylepšení produktů a služeb.


## <a name="data-collected"></a>Shromažďovaná data

Volitelná diagnostická data shromažďovaná klientskými aplikacemi Intune mohou zahrnovat následující oblasti:

- Informace o uživateli generované společností Microsoft
    - ID uživatele Azure AD
    - ID zařízení
    - ID korelace
    - ID relace aplikace
    - ID uživatelské relace
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
Domníváme se, že pro lidi existují přesvědčivé důvody pro sdílení těchto volitelných dat. Všechna volitelná diagnostická data, která Microsoft shromažďuje během používání Microsoft 365 aplikací pro podnikové aplikace a služby, je pseudonymně vymezený ve standardu ISO/IEC 19944:2017 (oddíl 8.3.3). Uživatelé můžou pro jednotlivá zařízení [vypnout shromažďování dat o využití](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android) .


## <a name="next-steps"></a>Další kroky
[Přečtěte si další informace o shromažďování dat v Intune.](privacy-data-collect.md)



