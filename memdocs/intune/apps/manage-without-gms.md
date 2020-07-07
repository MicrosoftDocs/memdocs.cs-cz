---
title: Jak používat Intune v prostředích bez Google Mobile Services
titleSuffix: Microsoft Intune
description: Naučte se používat Intune v prostředích bez Google Mobile Services.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7955afb2aef88e3787546843cc477bce22369a4d
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022377"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Jak používat Intune v prostředích bez Google Mobile Services

Microsoft Intune používá Google Mobile Services (GMS) ke komunikaci s portálem Microsoft Intune společnosti při správě zařízení s Androidem. V některých případech můžou zařízení dočasně nebo trvale mít přístup k GMS. Zařízení se například může dodávat bez GMS nebo se může připojit k zavřené síti, kde GMS není k dispozici. Tento dokument shrnuje rozdíly a omezení, které můžete sledovat při instalaci a používání Intune ke správě zařízení s Androidem bez GMS.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Instalace aplikace Portál společnosti Intune bez přístupu k Obchod Google Play 

### <a name="for-users-outside-of-peoples-republic-of-china"></a>Pro uživatele mimo Čínskou lidovou republiku

Pokud Google Play není k dispozici, zařízení s Androidem můžou stáhnout [Microsoft Intune portál společnosti pro Android](https://www.microsoft.com/en-us/download/details.aspx?id=49140) a aplikace bokem. Při instalaci tímto způsobem aplikace neobdrží aktualizace nebo opravy automaticky. Je nutné, abyste aplikaci pravidelně aktualizovali a ručně aktualizovali. 

### <a name="for-users-in-peoples-republic-of-china"></a>Pro uživatele v Čínské lidové republice

Protože Obchod Google Play v současnosti není k dispozici v Číně, musí zařízení s Androidem získávat aplikace z čínských tržiště aplikací. Další informace najdete v tématu [instalace aplikace Portál společnosti v Číně v Čínské lidové republice](../user-help/install-company-portal-android-china.md).

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Omezení správy Správce zařízení Intune, když GMS není k dispozici 

### <a name="unavailable-intune-features"></a>Nedostupné funkce Intune

Některé funkce Intune spoléhají na komponenty GMS, jako je Google Play Store nebo Google Play Services. Vzhledem k tomu, že tyto komponenty nejsou k dispozici v prostředích bez GMS, nemusí být k dispozici následující funkce v konzole pro správu Intune.  

| Scénář  | Funkce  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Zásady dodržování předpisů pro zařízení  | Při vytváření nebo úpravách zásad dodržování předpisů pro správce zařízení s Androidem nejsou k dispozici všechny možnosti uvedené v části **Google Play ochrana** .  |
| Zásady ochrany aplikací (podmíněné spuštění)  | **Ověření zařízení SafetyNet** a **vyžadovat podmínky kontroly hrozeb u aplikací** nelze použít k podmíněnému spuštění.  |
| Klientské aplikace  | Aplikace typu **Android** nejsou k dispozici. K nasazení a správě aplikací použijte místo toho **obchodní aplikaci** .  |
| Mobile Threat Defense  | Spolupracujte se svým dodavatelem MTD a zjistěte, jestli je jejich řešení integrované s Intune, pokud je dostupné v oblasti zájmu a jestli spoléhá na GMS.  |

### <a name="some-tasks-may-be-delayed"></a>Některé úkoly můžou být zpožděné. 

V prostředích, kde je GMS k dispozici, se Intune spoléhá na nabízená oznámení, která dokončí úlohy. Pokud se například pokusíte zařízení vzdáleně vymazat, oznámení se většinou dostanou do zařízení během několika sekund. V případech, kdy GMS není k dispozici, mohou být nabízená oznámení také nedostupná. Proto Intune musí počkat na další čas vrácení se změnami zařízení, aby se úlohy dokončily.  

Zaregistrovaná zařízení se systémem Android nahlásí každých 8 hodin do Intune. Pokud se třeba zařízení nahlásí do Intune v 1 ODP. a vzdálené úlohy se vystaví v 1:05. odp., Intune se obrátí na zařízení za 9 PM, aby se úkoly dokončily. 

Dokončení následujících úloh může vyžadovat až 8 hodin: 

**Konzola Intune**:
- Úplné vymazání
- Selektivní vymazání
- Nasazení nových nebo aktualizovaných aplikací
- vzdálené uzamčení
- resetování hesla

**Portál společnosti Intune aplikace pro Android**:
- Vzdálené odebrání zařízení
- Resetování zařízení
- Instalace dostupných obchodních aplikací

**Portál společnosti Intune web**:
- Odebrání zařízení (místní a vzdálené)
- Resetování zařízení
- Resetování hesla zařízení

Pokud se zařízení nedávno zaregistrovalo, spouští se ověření dodržování předpisů, nedodržování předpisů a konfigurace častěji. Další informace o vracení se změnami zařízení najdete v tématu [běžné otázky, problémy a řešení pro zásady a profily zařízení v Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací do skupin pomocí Microsoft Intune](../apps/apps-deploy.md)
