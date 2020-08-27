---
title: Správa Outlooku pro iOS a Android s Intune
description: Použijte zásady ochrany aplikací a konfigurace Intune s Outlookem pro iOS a Android, abyste zajistili, že prostředí pro týmovou spolupráci jsou vždycky dostupná s ochranou.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90bbc3bfbe4f7e6120359f86ad9cb1c55b2ed500
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907782"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Správa přístupu k zasílání zpráv pomocí Outlooku pro iOS a Android s Microsoft Intune

Aplikace Outlook pro iOS a Android je navržená tak, aby uživatelům ve vaší organizaci umožnila více z jejich mobilních zařízení, a to prostřednictvím e-mailu, kalendáře, kontaktů a dalších souborů.

V případě, že se přihlásíte k odběru Enterprise Mobility + Security sady, která zahrnuje Microsoft Intune a Azure Active Directory Premium funkce, jako je například podmíněný přístup, jsou k dispozici bohatší a nejširší funkce ochrany pro data Office 365. Minimálně budete chtít nasadit zásadu podmíněného přístupu, která umožňuje připojení k aplikaci Outlook pro iOS a Android z mobilních zařízení a zásady ochrany aplikací Intune, které zajistí ochranu prostředí pro spolupráci.

## <a name="apply-conditional-access"></a>Použití podmíněného přístupu
Organizace můžou pomocí zásad podmíněného přístupu Azure AD zajistit, že uživatelé budou mít přístup k pracovnímu nebo školnímu obsahu jenom přes Outlook pro iOS a Android. K tomu budete potřebovat zásadu podmíněného přístupu, která cílí na všechny potenciální uživatele. Podrobnosti o vytvoření této zásady najdete v v [vyžadovat zásady ochrany aplikací pro cloudovou aplikaci přístup s podmíněným přístupem](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Postupujte podle pokynů v části Krok 1: Konfigurace zásad podmíněného přístupu Azure AD pro Office 365 ve [scénáři 1: aplikace Office 365 vyžadují schválené aplikace se zásadami ochrany aplikací](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), které umožňují Outlook pro iOS a Android, ale blokuje klientům Exchange ActiveSync s protokolem OAuth, aby se připojili k Exchangi Online.

   > [!NOTE]
   > Tato zásada zajišťuje, že mobilní uživatelé budou mít přístup ke všem koncovým bodům Office pomocí příslušných aplikací.

2. Postupujte podle pokynů v části Krok 2: Konfigurace zásad podmíněného přístupu Azure AD pro Exchange Online pomocí ActiveSync (EAS) ve [scénáři 1: aplikace Office 365 vyžadují schválené aplikace se zásadami ochrany aplikací](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), které brání klientům Exchange ActiveSync využít základní ověřování v připojení k Exchangi Online.

   Výše uvedené zásady využívají řízení udělení [vyžaduje zásadu ochrany aplikací](/azure/active-directory/active-directory-conditional-access-technical-reference), která zajišťuje, aby se pro přidružený účet v Outlooku pro iOS a Android před udělením přístupu používala zásada Intune App Protection. Pokud uživatel nemá přiřazenou zásadu Intune App Protection, nemá licenci pro Intune nebo není tato aplikace zahrnutá v zásadách Intune App Protection, pak mu zásada brání v získání přístupového tokenu a získání přístupu k datům zasílání zpráv.

3. Nakonec Sledujte [Postup: blokování staršího ověřování do služby Azure AD s podmíněným přístupem](/azure/active-directory/conditional-access/block-legacy-authentication) k blokování staršího ověřování pro jiné protokoly Exchange na zařízeních s iOS a Androidem. Tato zásada by měla cílit jenom na platformy Office 365 Exchange Online Cloud App a iOS a Android. Tím se zajistí, že se mobilní aplikace používající protokoly Exchange Web Services, IMAP4 nebo POP3 se základním ověřováním nemůžou připojit k Exchangi Online.

## <a name="create-intune-app-protection-policies"></a>Vytvoření zásad ochrany aplikací Intune

Zásady ochrany aplikací (aplikace) definují, které aplikace jsou povoleny, a akce, které mohou provádět s daty vaší organizace. Volby dostupné v aplikaci umožňují organizacím přizpůsobit ochranu na jejich konkrétní potřeby. V některých případech nemusí být zřejmé, která nastavení zásad jsou nutná k implementaci kompletního scénáře. Microsoft zavedl taxonomii pro své rozhraní ochrany dat aplikací pro správu mobilních aplikací v iOS a Androidu, aby organizacím pomohly určit prioritu posílení koncových bodů mobilních klientů.

Architektura aplikace Data Protection je rozdělená na tři různé úrovně konfigurace, přičemž každá úroveň se sestavuje na předchozí úrovni:

- **Ochrana podnikových dat** na úrovni Basic (úroveň 1) zajišťuje, aby byly aplikace chráněny pomocí kódu PIN a zašifrované a prováděly operace selektivního vymazání. U zařízení s Androidem Tato úroveň ověřuje ověření zařízení s Androidem. Toto je konfigurace na úrovni vstupu, která poskytuje podobné řízení ochrany dat v zásadách poštovní schránky Exchange Online a zavádí uživatele a naplňování do aplikace.
- **Enterprise Enhanced Data Protection** (úroveň 2) zavádí mechanismy prevence úniku dat aplikace a minimální požadavky na operační systém. Jedná se o konfiguraci, která platí pro většinu mobilních uživatelů, kteří přistupují k pracovním nebo školním datům.
- **Podniková ochrana dat** (úroveň 3) zavádí pokročilé mechanismy ochrany dat, rozšířenou konfiguraci kódu PIN a ochranu před mobilními hrozbami aplikace. Tato konfigurace je žádoucí pro uživatele, kteří mají přístup k datům s vysokým rizikem.

Pokud chcete zobrazit konkrétní doporučení pro jednotlivé úrovně konfigurace a minimální aplikace, které musí být chráněné, přečtěte si téma [Ochrana dat pomocí zásad ochrany aplikací](app-protection-framework.md).

Bez ohledu na to, jestli je zařízení zaregistrované v řešení UEM (Unified Endpoint Management), je potřeba vytvořit zásady ochrany aplikací Intune pro aplikace pro iOS i Android, a to pomocí kroků v tématu [jak vytvořit a přiřadit zásady ochrany aplikací](app-protection-policies.md). Tyto zásady musí splňovat minimálně tyto podmínky:

1. Zahrnují všechny Microsoft 365 mobilní aplikace, jako je například Edge, Outlook, OneDrive, Office nebo týmy. tím zajistíte, že uživatelé budou mít zabezpečený přístup k pracovním nebo školním datům v rámci libovolné aplikace Microsoftu.

2. Jsou přiřazeny všem uživatelům. Tím se zajistí Ochrana všech uživatelů bez ohledu na to, jestli používají Outlook pro iOS nebo Android.

3. Určete, která úroveň rozhraní splňuje vaše požadavky. Většina organizací by měla implementovat nastavení definovaná v **Enterprise Enhanced Data Protection** (Level 2), protože umožňuje řízení požadavků na ochranu a přístup k datům.

Další informace o dostupných nastaveních najdete v tématu nastavení [zásad ochrany aplikací pro Android](app-protection-policy-settings-android.md) a [nastavení zásad ochrany aplikací pro iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Aby bylo možné použít zásady ochrany aplikací Intune proti aplikacím na zařízeních s Androidem, které nejsou zaregistrované v Intune, musí uživatel nainstalovat taky Portál společnosti Intune. Další informace najdete v tématu [co očekávat, když je vaše aplikace pro Android spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Využití konfigurace aplikace

Outlook pro iOS a Android podporuje nastavení aplikace, která umožňují sjednocenou správu koncových bodů, jako je Microsoft Endpoint Manager, což správcům umožňuje přizpůsobit chování aplikace.

Konfigurace aplikace se dá doručit buď prostřednictvím kanálu operačního systému správy mobilních zařízení (MDM) v zaregistrovaných zařízeních ([Konfigurace kanálu konfigurace spravovaných aplikací](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) pro iOS nebo [Android v podnikovém](https://developer.android.com/work/managed-configurations) kanálu pro Android), nebo přes kanál Intune App Protection Policy (App). Outlook pro iOS a Android podporuje následující scénáře konfigurace:

- Povolí jenom pracovní nebo školní účty.
- Obecná nastavení konfigurace aplikace
- Nastavení S/MIME
- Nastavení pro ochranu dat

Konkrétní procesní kroky a podrobnou dokumentaci k nastavení konfigurace aplikace Outlook pro iOS a Android najdete v tématu [nasazení aplikace Outlook pro iOS a nastavení konfigurace aplikací pro Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="next-steps"></a>Další kroky

- [Co jsou zásady ochrany aplikací?](app-protection-policy.md) 
- [Zásady konfigurace aplikací v Microsoft Intune](app-configuration-policies-overview.md)