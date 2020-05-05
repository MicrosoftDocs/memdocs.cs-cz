---
title: Správa zařízení s pracovním profilem Android Enterprise v Microsoft Intune
titleSuffix: ''
description: Microsoft Intune spravuje zařízení s pracovním profilem Android Enterprise, která poskytují další možnosti správy a ochranu osobních údajů, když uživatelé používají svoje osobní zařízení s Androidem pro práci.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2cc3c960-1fdd-47ca-a693-420d47b403de
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a2f8ccfccfdca26416b0da92e6f27425e13c90c6
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078035"
---
# <a name="manage-android-work-profile-devices-with-intune"></a>Správa zařízení s pracovním profilem Androidu v Intune

Android Enterprise nabízí sadu možností registrace, které uživatelům poskytují nejaktuálnější a zabezpečené funkce. Registrace pomocí pracovního profilu Android Enterprise umožňuje sadu funkcí a služeb, které oddělují osobní aplikace a data od pracovních aplikací a dat. Poskytuje taky další možnosti správy a ochranu osobních údajů, když uživatelé používají svoje osobní zařízení s Androidem pro práci. 

## <a name="supported-devices"></a>Podporovaná zařízení

Funkce pro správu Androidu Enterprise se spoléhají na funkce, které jsou součástí novějšího operačního systému Android. Pro zařízení, která nepodporují Android Enterprise, zůstane k dispozici běžná Správa Androidu. Další informace najdete v tématu [požadavky na Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="onboarding"></a>Onboarding

Před registrací zařízení se systémem Android Enterprise Work Profile je nutné provést některé kroky připojování. Tyto kroky naváže spojení mezi vaším klientem Intune a spravovaným Google Play. Další informace najdete v tématu [Povolení registrace zařízení s pracovními profily Android Enterprise](android-work-profile-enroll.md).

## <a name="work-profile-management"></a>Správa pracovních profilů

Když spravujete zařízení se systémem Android Enterprise Work Profile v Intune, nebudete spravovat celé zařízení. Možnosti správy mají vliv jenom na pracovní profil, který se vytvoří v zařízení během registrace. Všechny aplikace, které se nasadí na zařízení pomocí Intune, se nainstalují do pracovního profilu. Ikony aplikací v pracovním profilu jsou odlišené od osobních aplikací v zařízení. Všechny aplikace a data Androidu mimo část zařízení vyhrazenou pro Android Enterprise zůstanou osobní a pod kontrolou koncového uživatele. Uživatelé můžou do osobní části zařízení nainstalovat libovolnou aplikaci. Správci můžou spravovat a monitorovat aplikace a akce vymezené pro pracovní profil.

Intune poskytuje řadu předdefinovaných obecných nastavení, která můžete na zařízeních s pracovním profilem Androidu konfigurovat. Další informace najdete v tématu, které se věnuje [nastavení zásad na zařízeních s pracovním profilem Androidu](../protect/compliance-policy-create-android-for-work.md).

## <a name="app-publishing-and-distribution"></a>Publikování a distribuce aplikací

Spravovaná Google Play je nedílnou součástí distribuce a správy aplikací pro Android Enterprise. Všechny aplikace nasazené na zařízení s Androidem Enterprise Work Profiles v pracovním profilu pocházejí ze spravované služby Google Play. Pokud chcete v obchodu Play spravovat a nasazovat aplikace, přihlaste se na web Google Play pomocí přihlašovacích údajů správce vaší společnosti pro správu účtu Google. Můžete schvalovat aplikace pro podnikové nasazení Androidu, aby se zobrazovaly v pracovních profilech zařízení. Tyto aplikace se potom budou synchronizovat s konzolou Intune, kde je pak možné je pomocí služby Intune nasadit a spravovat. Obchodní aplikace, které vyvinula vaše organizace, se musí publikovat na spravovaných Google Play pomocí konzoly pro publikování aplikací pro Android od společnosti Google. Obchodní aplikace se musí nakonfigurovat na konzole pro publikování aplikací pro Android. Omezí se tak přístup do vaší organizace.

Aplikace se můžou instalovat bez interakce uživatelů, kteří ani nemusí povolit **instalaci z neznámých zdrojů**. Uživatelé můžou procházet obchod Play for Work a na svoje zařízení z něj instalovat volitelné nebo dostupné aplikace. Další informace najdete v tématu [přiřazení aplikací k zařízením s pracovním profilem Android Enterprise s Intune](../apps/apps-add-android-for-work.md).

## <a name="app-configuration"></a>Konfigurace aplikací

Android Enterprise poskytuje infrastrukturu pro nasazení hodnot konfigurace aplikací do aplikací, které je podporují. Když zadáte konfigurační hodnoty pro pracovní aplikace, zajistíte tak při prvním spuštění aplikace uživatelem jejich správné nastavení. Podpora konfigurace aplikace vyžaduje, aby vývojáři aplikací vytvářeli svoje aplikace výslovně tak, aby podporovaly hodnoty spravované konfigurace. V takovém případě pak můžou použít Intune k zadání a použití tohoto nastavení konfigurace. Další informace najdete v tématu [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem](../apps/app-configuration-policies-use-android.md).

## <a name="email-configuration"></a>Konfigurace e-mailu

Android Enterprise neposkytuje výchozí e-mailovou aplikaci ani objekt nativního e-mailového profilu, jako jsou ty, které poskytuje iOS/iPadOS. Místo toho je možné nastavit konfigurace e-mailu s použitím nastavení konfigurací aplikací u e-mailových aplikací, které je podporují. Gmail a devět práce jsou dvě klientské aplikace Exchange ActiveSync (EAS) v Obchod Play, které podporují konfiguraci s konfigurací aplikací pro Android Enterprise.

Když jsou aplikace Gmail a Nine Work spravované jako pracovní aplikace, služba Intune pro ně poskytuje šablony konfigurace. Jiné e-mailové aplikace, které podporují konfigurační profily aplikací, je možné nakonfigurovat pomocí zásad konfigurace mobilních aplikací.

Pokud používáte podmíněný přístup protokolu Exchange ActiveSync pro zařízení se systémem Android Enterprise Work Profile, zvažte použití aplikace Gmail nebo devět pracovních e-mailů. Podporuje se také aplikace Microsoft Outlook pro Android nebo kterákoliv jiná e-mailová aplikace, která používá moderní ověřování prostřednictvím ADAL. Další informace najdete v tématu [Jak nakonfigurovat nastavení e-mailu v Microsoft Intune](../configuration/email-settings-configure.md).

## <a name="app-protection-policies"></a>Zásady ochrany aplikace

Používané zásady ochrany aplikace jsou plně podporované v pracovním i osobním profilu. Obchodní aplikace je možné publikovat na konzole pro publikování aplikací pro Android na adrese https://play.google.com/apps/publish. Tato konzola zahrnuje možnost nastavit pro vaši organizaci aplikace jako soukromé. Další informace najdete v tématu [Přidání zásad dodržování předpisů pro zařízení v systému Android Enterprise Work Profiles v Intune](../protect/compliance-policy-create-android-for-work.md). Obecné informace o zásadách ochrany aplikací najdete v tématu [Co jsou zásady ochrany aplikací](../apps/app-protection-policy.md).

## <a name="vpn-profiles"></a>Profily sítě VPN

Podpora sítě VPN je podobná profilům Android VPN. Pro správu Android Enterprise jsou k dispozici stejné poskytovatele sítě VPN a možnosti základní konfigurace se dvěma rozdíly:

- **Síť VPN vymezená pro pracovní profil** – připojení VPN jsou omezená jenom na aplikace nasazené do pracovního profilu. Připojení VPN můžou používat jenom aplikace spravované pro Android firemním. Osobní aplikace na zařízení spravované připojení VPN použít nemůžou. Další informace najdete v tématu [nastavení sítě VPN pro Android Enterprise](../configuration/vpn-settings-android-enterprise.md).

- **Síť VPN specifická pro aplikaci** – tuto síť lze v Intune nakonfigurovat, pokud poskytovatel VPN podporuje:
  - Konfiguraci sítě VPN specifické pro aplikaci
  - možnost Konfigurovat síť VPN pro jednotlivé aplikace pomocí konfiguračního profilu aplikace pro Android Enterprise.
  Další informace najdete v tématu o [vytvoření profilu VPN pro aplikaci pro zařízení s Androidem pomocí vlastního profilu Microsoft Intune](../configuration/android-pulse-secure-per-app-vpn.md).

## <a name="certificate-profiles"></a>Profily certifikátů

Na zařízeních s pracovními profily Android Enterprise jsou k dispozici stejné možnosti konfigurace profilu certifikátu, které jsou dostupné pro správu Androidu. Android Enterprise poskytuje Vylepšená rozhraní API pro správu certifikátů. Vylepšená správa certifikátů poskytuje následující funkce:

- Zajišťuje uživatelům tiché a bezproblémové nasazení.
- Zajišťuje odebrání nasazených certifikátů po vyřazení zařízení z Intune a odebrání pracovního profilu.
- Poskytuje vylepšené zasílání zpráv uživatelům s informacemi o tom, že IT oddělení nasadilo a nakonfigurovalo prostřednictvím svojí služby správy certifikát.

Další informace najdete v tématu [Konfigurace profilu certifikátu pro zařízení v Microsoft Intune](../protect/certificates-configure.md).

## <a name="wi-fi-profiles"></a>Profily sítě Wi-Fi

Profily Wi-Fi, které spravuje Android Enterprise, se odeberou, když se zařízení vyřadí z Intune a pracovní profil se odstraní. Další informace najdete v tématu [Jak nakonfigurovat nastavení Wi-Fi v Microsoft Intune](../configuration/wi-fi-settings-configure.md).

## <a name="next-steps"></a>Další kroky
- [Registrace zařízení s Androidem](android-enroll.md)
- [Přiřazení aplikací k zařízením s pracovním profilem Android Enterprise s Intune](../apps/apps-add-android-for-work.md)
