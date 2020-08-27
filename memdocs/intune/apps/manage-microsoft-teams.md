---
title: Správa týmů pro iOS a Android pomocí Intune
titleSuffix: ''
description: Použijte zásady ochrany aplikací a konfigurace Intune s týmy pro iOS a Android, abyste zajistili, že prostředí pro týmovou spolupráci jsou vždycky k dispozici s ochranou na pracovišti.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: befbbeee928b9eda6edb42d58e9caed9b4abd600
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910277"
---
# <a name="manage-team-collaboration-access-by-using-teams-for-ios-and-android-with-microsoft-intune"></a>Správa přístupu k týmové spolupráci pomocí týmů pro iOS a Android s využitím Microsoft Intune

Microsoft Teams je centrum pro týmovou spolupráci v Microsoft 365, které integruje osoby, obsah a nástroje, které váš tým potřebuje k zajištění vyšší efektivity.

V případě, že se přihlásíte k odběru Enterprise Mobility + Security sady, která zahrnuje Microsoft Intune a Azure Active Directory Premium funkce, jako je například podmíněný přístup, jsou k dispozici bohatší a nejširší funkce ochrany pro data Office 365. Minimálně budete chtít nasadit zásadu podmíněného přístupu, která umožňuje připojení k týmům pro iOS a Android z mobilních zařízení a zásad ochrany aplikací Intune, které zajistí ochranu prostředí pro spolupráci.

## <a name="apply-conditional-access"></a>Použití podmíněného přístupu
Organizace můžou použít zásady podmíněného přístupu Azure AD a zajistit tak, že uživatelé budou mít přístup k pracovnímu nebo školnímu obsahu jenom pomocí týmů pro iOS a Android. K tomu budete potřebovat zásadu podmíněného přístupu, která cílí na všechny potenciální uživatele. Podrobnosti o vytvoření této zásady najdete v v [vyžadovat zásady ochrany aplikací pro cloudovou aplikaci přístup s podmíněným přístupem](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Postupujte podle pokynů v části Krok 1: Konfigurace zásad podmíněného přístupu Azure AD pro Office 365 ve [scénáři 1: aplikace Office 365 vyžadují schválené aplikace se zásadami ochrany aplikací](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), které umožňují týmům pro iOS a Android, ale blokuje klientům mobilních zařízení s podporou OAuth, aby se připojili k koncovým bodům 365 sady Office.

   >[!NOTE]
   > Tato zásada zajišťuje, že mobilní uživatelé budou mít přístup ke všem koncovým bodům Office pomocí příslušných aplikací.

## <a name="create-intune-app-protection-policies"></a>Vytvoření zásad ochrany aplikací Intune

Zásady ochrany aplikací (aplikace) definují, které aplikace jsou povoleny, a akce, které mohou provádět s daty vaší organizace. Volby dostupné v aplikaci umožňují organizacím přizpůsobit ochranu na jejich konkrétní potřeby. V některých případech nemusí být zřejmé, která nastavení zásad jsou nutná k implementaci kompletního scénáře. Microsoft zavedl taxonomii pro své rozhraní ochrany dat aplikací pro správu mobilních aplikací v iOS a Androidu, aby organizacím pomohly určit prioritu posílení koncových bodů mobilních klientů.

Architektura aplikace Data Protection je rozdělená na tři různé úrovně konfigurace, přičemž každá úroveň se sestavuje na předchozí úrovni:

- **Ochrana podnikových dat** na úrovni Basic (úroveň 1) zajišťuje, aby byly aplikace chráněny pomocí kódu PIN a zašifrované a prováděly operace selektivního vymazání. U zařízení s Androidem Tato úroveň ověřuje ověření zařízení s Androidem. Toto je konfigurace na úrovni vstupu, která poskytuje podobné řízení ochrany dat v zásadách poštovní schránky Exchange Online a zavádí uživatele a naplňování do aplikace.
- **Enterprise Enhanced Data Protection** (úroveň 2) zavádí mechanismy prevence úniku dat aplikace a minimální požadavky na operační systém. Jedná se o konfiguraci, která platí pro většinu mobilních uživatelů, kteří přistupují k pracovním nebo školním datům.
- **Podniková ochrana dat** (úroveň 3) zavádí pokročilé mechanismy ochrany dat, rozšířenou konfiguraci kódu PIN a ochranu před mobilními hrozbami aplikace. Tato konfigurace je žádoucí pro uživatele, kteří mají přístup k datům s vysokým rizikem.

Pokud chcete zobrazit konkrétní doporučení pro jednotlivé úrovně konfigurace a minimální aplikace, které musí být chráněné, přečtěte si téma [Ochrana dat pomocí zásad ochrany aplikací](app-protection-framework.md).

Bez ohledu na to, jestli je zařízení zaregistrované v řešení UEM (Unified Endpoint Management), je potřeba vytvořit zásady ochrany aplikací Intune pro aplikace pro iOS i Android, a to pomocí kroků v tématu [jak vytvořit a přiřadit zásady ochrany aplikací](app-protection-policies.md). Tyto zásady musí splňovat minimálně tyto podmínky:

1. Zahrnují všechny Microsoft 365 mobilní aplikace, jako je například Edge, Outlook, OneDrive, Office nebo týmy. tím zajistíte, že uživatelé budou mít zabezpečený přístup k pracovním nebo školním datům v rámci libovolné aplikace Microsoftu.

2. Jsou přiřazeny všem uživatelům. Tím se zajistí, že všichni uživatelé budou chráněni bez ohledu na to, jestli používají týmy pro iOS nebo Android.

3. Určete, která úroveň rozhraní splňuje vaše požadavky. Většina organizací by měla implementovat nastavení definovaná v **Enterprise Enhanced Data Protection** (Level 2), protože umožňuje řízení požadavků na ochranu a přístup k datům.

Další informace o dostupných nastaveních najdete v tématu nastavení [zásad ochrany aplikací pro Android](app-protection-policy-settings-android.md) a [nastavení zásad ochrany aplikací pro iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Aby bylo možné použít zásady ochrany aplikací Intune proti aplikacím na zařízeních s Androidem, které nejsou zaregistrované v Intune, musí uživatel nainstalovat taky Portál společnosti Intune. Další informace najdete v tématu [co očekávat, když je vaše aplikace pro Android spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Využití konfigurace aplikace

Týmy pro iOS a Android podporují nastavení aplikace, která umožňují jednotnou správu koncových bodů, jako je Microsoft Endpoint Manager, což správcům umožňuje přizpůsobit chování aplikace.

Konfigurace aplikace se dá doručit buď prostřednictvím kanálu operačního systému správy mobilních zařízení (MDM) v zaregistrovaných zařízeních ([Konfigurace kanálu konfigurace spravovaných aplikací](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) pro iOS nebo [Android v podnikovém](https://developer.android.com/work/managed-configurations) kanálu pro Android), nebo přes kanál Intune App Protection Policy (App). Týmy pro iOS a Android podporují následující scénáře konfigurace:

- Povolí jenom pracovní nebo školní účty.

> [!IMPORTANT]
> V případě scénářů konfigurace, které vyžadují registraci zařízení v Androidu, musí být zařízení zaregistrovaná v Androidu Enterprise a týmy pro Android se musí nasadit prostřednictvím spravovaného Google Play Storu. Další informace najdete v tématech [Nastavení registrace zařízení s pracovním profilem Android Enterprise](../enrollment/android-work-profile-enroll.md) a [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](app-configuration-policies-use-android.md).

Každý scénář konfigurace zvýrazní konkrétní požadavky. Například jestli scénář konfigurace vyžaduje registraci zařízení, takže funguje s jakýmkoli poskytovatelem UEM nebo vyžaduje zásady Intune App Protection.

> [!NOTE]
> Pomocí Microsoft Endpoint Manageru se konfigurace aplikací dodaná prostřednictvím kanálu MDM operačního systému označuje jako zásady konfigurace aplikací **spravovaných zařízení** (ACP). Konfigurace aplikace dodaná prostřednictvím kanálu zásad ochrany aplikací se označuje jako zásada konfigurace aplikace **spravované aplikace** .

## <a name="only-allow-work-or-school-accounts"></a>Povolí jenom pracovní nebo školní účty.

Dodržování zásad zabezpečení a dodržování předpisů u našich největších a vysoce regulovaných zákazníků je klíčovým pilířem Microsoft 365 hodnoty. Některé společnosti mají požadavek na zachycení všech komunikačních informací v rámci svého podnikového prostředí, a to i v případě, že se zařízení používají jenom pro firemní komunikaci. Pro podporu těchto požadavků je možné nakonfigurovat týmy pro iOS a Android na registrovaných zařízeních tak, aby povolovala zřízení jednoho podnikového účtu v rámci aplikace.

Další informace o konfiguraci nastavení režimu pro povolení účtů organizace najdete tady:

- [Nastavení Androidu](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [nastavení iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Tento scénář konfigurace funguje jenom se zaregistrovanými zařízeními. Nicméně jakýkoli poskytovatel UEM je podporován. Pokud nepoužíváte Microsoft Endpoint Manager, budete se muset obrátit na dokumentaci k UEM, jak tyto konfigurační klíče nasadit.

## <a name="next-steps"></a>Další kroky

- [Co jsou zásady ochrany aplikací?](app-protection-policy.md) 
- [Zásady konfigurace aplikací v Microsoft Intune](app-configuration-policies-overview.md)