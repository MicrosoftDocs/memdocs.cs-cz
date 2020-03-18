---
title: Sestava nekompletních zápisů uživatelů v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o sestavě nedokončené registrace uživatelů.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a3fc8976c4799759088db4c4f28a9f50dff8e37
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332851"
---
# <a name="incomplete-user-enrollments-report"></a>Sestava nekompletních zápisů uživatelů

Tato sestava obsahuje informace o tom, kde v procesu registrace Portál společnosti uživatelé nedokončují proces registrace.

Pokud chcete zobrazit sestavu, vyberte > **Intune** **registrace zařízení** > **nedokončené registrace uživatelů**.

Pomocí těchto informací můžete aktualizovat dokumenty pro připojování, aby uživatelé mohli dokončit registraci. Pokud například končí mnoho uživatelů u podmínek použití, můžete tuto oblast prozkoumat a upravit, aby byla pro uživatele intuitivnější.

## <a name="what-is-an-incomplete-enrollment"></a>Co je neúplná registrace?

Neúplný zápis je v případě, že uživatel provede některou z následujících akcí:

- Explicitně zvolí akci, která zastaví registraci.
- Zavře Portál společnosti v průběhu registrace.
- Stráví více než 30 minut mezi částmi registrace.

Pokud se uživatel rozhodne zastavit registraci a restartovat několikrát, zobrazí se více pokusů a vícenásobné nedokončené registrace. Pokud uživatel čeká na 30 minut mezi různými obrazovkami registrace, považuje se za několik neúplných zápisů.

## <a name="what-does-the-report-show"></a>Co tato sestava zobrazuje?

Sestavy obsahují data pro zařízení s iOS/iPadOS a Androidem.

Sestavy zobrazují data za poslední dva týdny, ale můžete nastavit filtr sestavy tak, aby zobrazovala libovolné období do 30 dnů v minulosti.

Pomocí **filtru** můžete zvolit rozsah kalendářních dat, operační systém a část registrace.

### <a name="number-and-percentage-tiles"></a>Dlaždice pro počet a procentuální hodnotu

V horní části sestavy můžete zobrazit počet a procento neúplných registrací ve vztahu ke všem registraci.

- Zahájené registrace: Počet pokusů o registraci.
- Neúplné registrace: počet pokusů o registraci, které nevedly k vypsání plně zaregistrovaných a kompatibilních zařízení.
- Nekompletní rychlost: procento pokusů o registraci, které byly opuštěny (zrušené registrace/iniciovaná registrace).

### <a name="line-graph"></a>Spojnicový graf

Spojnicový graf zobrazuje denní nedokončená registrace pro každé ze čtyř částí základního zápisu:

- Kontrolní seznam instalace
- Obrazovky platformy
- Podmínky použití
- Dodržování předpisů / aktivace

### <a name="user-abandonment-actions"></a>Akce uživatelů, po kterých došlo k opuštění registrace

Následující tabulky obsahují seznam akcí uživatele, které se dotáže na nekompletní registraci. Příklady obrazovek registrace můžete vidět ve videích s registrací zařízení s [iOSem](https://channel9.msdn.com/Series/IntuneEnrollment/iOS-Enrollment) a [Androidem](https://channel9.msdn.com/Series/IntuneEnrollment/Android-Enrollment). 


#### <a name="setup-checklist-section"></a>Část Kontrolní seznam instalace

| Název akce | Obrazovka nebo tok | Platforma | Akce |
| ---- |---- |---- |---- |
| EnrollmentWrapUp | Výzva k otevření stránky v Portálu společnosti | iOS/Android | **Zrušit** |
| EnrollmentWrapUp | Obrazovka registrace zařízení až do dokončení **načítání firemních prostředků** | iOS/Android | Trvalo > 30 minut |
| DeviceCategory | Výběr kategorie zařízení (pokud ji správce nakonfiguroval) až do kliknutí na **Hotovo** | iOS/Android | Trvalo > 30 minut |
| PreEnrollmentWizard | Obrazovka nastavení přístupu, pokud byla registrace zahájena, ale vrátila se k nastavení přístupu | iOS/Android| **Odložit** |
| PreEnrollmentWizard | Obrazovka nastavení přístupu až do kliknutí na **Další** na obrazovce **Co dál** | iOS/Android | Trvalo > 30 minut |

#### <a name="platform-screens-section"></a>Část Obrazovky platformy

| Název akce | Obrazovka nebo tok | Platforma | Akce |
| ---- |---- |---- |---- |
| iOSProfileLaunch | Výzva k zobrazení konfiguračního profilu | iOS/iPadOS | **Ignorovat** |
| iOSProfileLaunch | Obrazovka instalace profilu | iOS/iPadOS | **Zrušit** |
| iOSProfileLaunch | Výzva k určení důvěryhodnosti zdroje profilu pro registraci zařízení | iOS/iPadOS | **Zrušit** |
| iOSProfileLaunch | Obrazovka instalace profilu až do dokončení instalace profilu | iOS/iPadOS | Trvalo > 30 minut |
| AndroidPermissions | Obrazovka aktivace správce zařízení | Android | **Zrušit** |
| AndroidPermissions | Od výzvy ke schválení uskutečňování telefonních hovorů a jejich správy až do **aktivace** správce zařízení | Android | Trvalo > 30 minut |
| KnoxActivation | Aktivace agenta KLMS (pouze Samsung) | Android| **Zrušit** |
| KnoxActivation | Aktivace agenta KLMS až do výběru možnosti **Potvrdit** | Android | Trvalo > 30 minut|

#### <a name="terms-of-use-section"></a>Část Podmínky použití

| Název akce | Obrazovka nebo tok | Platforma | Akce |
| ---- |---- |---- |---- |
| TermsofUse | Podmínky použití (pokud je správce nakonfiguroval) | iOS/Android | **Odmítnout vše** |
| TermsofUse | Podmínky použití až do výběru možnosti **Přijmout vše** | iOS/Android | Trvalo > 30 minut |

#### <a name="complianceactivation-section"></a>Část Dodržování předpisů / aktivace

| Název akce | Obrazovka nebo tok | Platforma | Akce |
| ---- |---- |---- |---- |
| Dodržování předpisů | Dodržování předpisů zařízením (pokud je správce nakonfiguroval) se v nastavení přístupu po registraci zobrazuje jinak než zeleně.| iOS/Android | **Odložit** |
| Dodržování předpisů | Dodržování předpisů zařízením se zobrazuje jinak než zeleně až do aktualizace, po které se zobrazuje zeleně. | iOS/Android | Trvalo > 30 minut |
| Aktivace | Aktivace registrace (pokud ji správce nakonfiguroval) se v nastavení přístupu zobrazuje jinak než zeleně. | iOS/Android | **Odložit** |
| Dodržování předpisů | Aktivace zařízení se zobrazuje jinak než zeleně až do aktualizace, po které se zobrazuje zeleně. | iOS/Android | Trvalo > 30 minut |

## <a name="next-steps"></a>Další kroky

Po kontrole nedokončených sazeb registrace si můžete projít [Možnosti registrace](enrollment-options.md) a zjistit, jestli můžete provést nějaké změny, abyste mohli vylepšit registraci.
