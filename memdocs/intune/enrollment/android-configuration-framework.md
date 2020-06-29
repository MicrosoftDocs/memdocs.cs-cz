---
title: Rozhraní Android Enterprise Security Configuration Framework
titleSuffix: Microsoft Intune
description: Přečtěte si o omezeních a nastaveních navrhovaných pro základní a vysoké zabezpečení zařízení s Androidem Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502847"
---
# <a name="android-enterprise-security-configuration-framework"></a>Rozhraní Android Enterprise Security Configuration Framework

Rozhraní Android Enterprise Security Configuration Framework je série doporučení pro nastavení zásad dodržování předpisů a konfigurace zařízení. Tato doporučení vám pomůžou přizpůsobit ochranu zabezpečení mobilních zařízení ve vaší organizaci vašim konkrétním potřebám.

Organizace s vědomím v bezpečí hledají způsoby, jak zajistit ochranu firemních dat na mobilních zařízeních. Jedna metoda, která slouží k ochraně těchto dat, je prostřednictvím registrace zařízení. Registrace zařízení pomáhá organizacím:
- Nasaďte zásady dodržování předpisů (například sílu PIN, jailbreaků/root Validation atd.).
- Nasaďte zásady konfigurace (například Wi-Fi, certifikáty, VPN).
- Spravujte životní cyklus aplikace.

Abychom vám pomohli nastavit kompletní scénář zabezpečení, společnost Microsoft zavedla novou taxonomii pro [Konfigurace zabezpečení ve Windows 10](https://aka.ms/secconframework). Intune používá podobnou taxonomii pro svůj konfigurační rámec pro Android Enterprise Security. Zahrnují doporučené dodržování předpisů zařízením a nastavení omezení pro zařízení pro základní, rozšířené a vysoké zabezpečení. Tato taxonomie je vysvětlena v následujících článcích:

1. [Metodologie nasazení pro Android Enterprise Framework](framework-deployment-methodology.md): Doporučená metodologie pro nasazení rozhraní pro konfiguraci zabezpečení.
2. [Omezení registrace zařízení s Androidem](device-enrollment-restrictions.md): pro zařízení s Androidem Enterprise se předregistrují omezení.
3. [Nastavení zásad konfigurace aplikací pro zařízení s Androidem Enterprise](android-app-configuration-policies.md): Nakonfigurujte na zařízeních aplikace, aby se nepovolovaly osobní účty.
4. [Nastavení zabezpečení pracovního profilu Android Enterprise](android-work-profile-security-settings.md): specifická nastavení konfigurace pro základní a vysoké zabezpečení na zařízeních pracovního profilu.
5. [Nastavení zabezpečení pro plně spravovaná zařízení s Androidem Enterprise](android-fully-managed-security-settings.md): specifická nastavení konfigurace pro základní, Rozšířená a vysoká zabezpečení na plně spravovaných zařízeních.

## <a name="android-enterprise-enrollment-modes"></a>Režimy registrace Androidu Enterprise

Se systémem Android 5,0, Google představil Android Enterprise, který zahrnuje dva režimy registrace. Rozhraní Android Enterprise Security Configuration Framework poskytuje doporučení pro oba režimy.
- [Plně spravovaná zařízení (vlastník zařízení)](android-fully-managed-enroll.md): pro společnost vlastněná společností, která je přidružená k jednomu uživateli. Taková zařízení jsou výhradně pro práci a nikoli pro osobní použití.
- [Pracovní profil (vlastník profilu)](android-work-profile-enroll.md): obvykle pro zařízení v osobním vlastnictví, kde to vyžaduje jasnou hranici mezi pracovními a osobními údaji. Zásady, které řídí, zajistí, že pracovní data nejde přenést do osobního profilu.


## <a name="next-steps"></a>Další kroky

[Metodologie nasazení pro Android Enterprise Framework](framework-deployment-methodology.md)