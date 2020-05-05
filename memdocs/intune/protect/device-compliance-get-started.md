---
title: Zásady dodržování předpisů zařízením v Microsoft Intune – Azure | Microsoft Docs
description: Začněte používat zásady dodržování předpisů pro zařízení, Přehled stavů a úrovní závažnosti, použití stavu V období odkladu, práce s podmíněným přístupem a zpracování zařízení bez přiřazených zásad.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9fa14dd54a820ed20f8b3b504a836392c7f428f
ms.sourcegitcommit: 4381afb515c06f078149bd52528d1f24b63a2df9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82538162"
---
# <a name="set-rules-on-devices-to-allow-access-to-resources-in-your-organization-using-intune"></a>Nastavení pravidel na zařízeních pro povolení přístupu k prostředkům ve vaší organizaci pomocí Intune

Mnoho řešení správy mobilních zařízení (MDM) umožňuje chránit data organizace tím, že vyžaduje, aby uživatelé a zařízení splnili některé požadavky. V Intune se tato funkce nazývá "zásady dodržování předpisů". Zásady dodržování předpisů definují pravidla a nastavení, která musí uživatelé a zařízení splňovat, aby vyhovovaly předpisům. V kombinaci s podmíněným přístupem můžou správci zablokovat uživatele a zařízení, která pravidla nesplňují.

Správce Intune může například vyžadovat:

- Koncoví uživatelé používají pro přístup k datům organizace na mobilních zařízeních heslo.
- Zařízení není jailbreak nebo rootované.
- Minimální nebo maximální verze operačního systému v zařízení
- Zařízení, které má být na úrovni hrozby nebo na něm.

Pomocí této funkce můžete také monitorovat stav dodržování předpisů u zařízení ve vaší organizaci.

> [!IMPORTANT]
> Intune sleduje u všech vyhodnocení dodržování předpisů na zařízení plán vrácení se změnami zařízení. V [cyklech aktualizace zásad a profilů](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) se zobrazí odhadované časy aktualizace.

<!---### Actions for noncompliance

You can specify what needs to happen when a device is determined as noncompliant. This can be a sequence of actions during a specific time.
When you specify these actions, Intune will automatically initiate them in the sequence you specify. See the following example of a sequence of
actions for a device that continues to be in the noncompliant status for
a week:

- When the device is first determined to be noncompliant, an email with noncompliant notification is sent to the user.

- 3 days after initial noncompliance state, a follow up reminder is sent to the user.

- 5 days after initial noncompliance state, a final reminder with a notification that access to company resources will be blocked on the device in 2 days if the compliance issues are not remediated is sent to the user.

- 7 days after initial noncompliance state, access to company resources is blocked. This requires that you have Conditional Access policy that specifies that access from noncompliant devices should    be blocked for services such as Exchange and SharePoint.

### Grace Period

This is the time between when a device is first determined as
noncompliant to when access to company resources on that device is blocked. This time allows for time that the user has to resolve
compliance issues on the device. You can also use this time to create your action sequences to send notifications to the user before their access is blocked.

Remember that you need to implement Conditional Access policies in addition to compliance policies in order for access to company resources to be blocked.--->

## <a name="device-compliance-policies-work-with-azure-ad"></a>Zásady dodržování předpisů pro zařízení fungují s Azure AD

Intune používá [podmíněný přístup](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) Azure Active Directory (AD) (otevře jiný web docs), aby se vynutilo dodržování předpisů. Když se zařízení zaregistruje v Intune, spustí se proces registrace Azure AD a v Azure AD se aktualizují informace o zařízení. Jednou z informací je stav dodržování předpisů zařízením. Tento stav dodržování předpisů používají zásady podmíněného přístupu k blokování nebo povolení přístupu k e-mailu a dalším prostředkům organizace.

- [Co je Správa zařízení v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) je skvělým prostředkem, proč a jak se zařízení registrují ve službě Azure AD.

- [Podmíněný přístup](conditional-access.md) a [běžné způsoby použití podmíněného přístupu](conditional-access-intune-common-ways-use.md) popisují tuto funkci v souvislosti s Intune.

## <a name="ways-to-use-device-compliance-policies"></a>Způsoby používání zásad dodržování předpisů zařízeními

### <a name="with-conditional-access"></a>S podmíněným přístupem

U zařízení, která dodržují pravidla zásad, můžete těmto zařízením udělit přístup k e-mailu a dalším prostředkům organizace. Pokud zařízení nedodržují pravidla zásad, nezískají přístup k prostředkům organizace. Toto je podmíněný přístup.

### <a name="without-conditional-access"></a>Bez podmíněného přístupu

Zásady dodržování předpisů zařízením taky můžete používat bez podmíněného přístupu. Při nezávislém použití zásad dodržování předpisů se cílová zařízení vyhodnotí a nahlásí se jejich stav dodržování předpisů. Můžete například získat zprávu o tom, kolik zařízení není šifrovaných nebo která zařízení mají jailbreak nebo root. Pokud používáte zásady dodržování předpisů bez podmíněného přístupu, neexistují žádná omezení přístupu k prostředkům organizace.

## <a name="ways-to-deploy-device-compliance-policies"></a>Způsoby nasazení zásad dodržování předpisů zařízeními

Zásady dodržování předpisů můžete nasadit uživatelům ve skupinách uživatelů nebo zařízením ve skupinách zařízení. Po nasazení zásady dodržování předpisů uživateli se u všech jeho zařízení kontroluje dodržování předpisů. Použití skupin zařízení pomáhá v této situaci s vykazováním dodržování předpisů.

Intune také obsahuje sadu předdefinovaných nastavení zásad dodržování předpisů. Následující předdefinované zásady se vyhodnotí na všechna zařízení zaregistrovaná v Intune:

- **Označit zařízení, která nemají přiřazené žádné zásady dodržování předpisů, jako**: Tato vlastnost má dvě hodnoty:

  - **Kompatibilní** (*výchozí*): vypnutá funkce zabezpečení
  - **Nekompatibilní**: funkce zabezpečení zapnuta

  Pokud zařízení nemá přiřazené zásady dodržování předpisů, považuje se toto zařízení za vyhovující ve výchozím nastavení. Pokud používáte podmíněný přístup se zásadami dodržování předpisů, doporučujeme změnit výchozí nastavení na **nekompatibilní**. Pokud koncový uživatel nedodržuje předpisy, protože zásada není přiřazená, zobrazí `No compliance policies have been assigned`se [aplikace Portál společnosti](../apps/company-portal-app.md) .

- **Vylepšené zjišťování jailbreaků**: Pokud je toto nastavení povolené, způsobí to, že se na zařízeních s iOS/iPadOS bude nacházet v zařízení s jailbreakem/. Toto nastavení má vliv jenom na zařízení, která jsou cílem zásad dodržování předpisů, které blokují zařízení s jailbreakem. Povolení této vlastnosti používá služby zjišťování polohy zařízení a může mít vliv na využití baterie. Data o umístění uživatele nejsou uložená službou Intune a používají se jenom k aktivaci jailbreaků detekce na pozadí. 

  Povolení tohoto nastavení vyžaduje, aby zařízení:
  - Povolte služby zjišťování polohy na úrovni operačního systému.
  - Vždy povolí Portál společnosti používat služby zjišťování polohy.

  Vyhodnocování se aktivuje otevřením aplikace Portál společnosti nebo fyzickému přesunutí zařízení o důležitou vzdálenost přibližně 500 metrů a dalších. U iOS 13 a dalších funkcí bude tato funkce vyžadovat, aby uživatelé vždy, když se jim zobrazí výzva, povolili Portál společnosti používat jejich umístění na pozadí. Pokud uživatelé nemají vždycky přístup k poloze a mají nakonfigurovanou zásadu s tímto nastavením, bude jejich zařízení označeno jako nedodržující předpisy. Všimněte si, že Intune nemůže zaručit, že při každé významné změně umístění dojde k tomu, aby jailbreaků kontrolu detekce, protože to závisí na síťovém připojení zařízení.

- **Doba platnosti stavu dodržování předpisů (dny)**: Zadejte časové období, během kterého zařízení nahlásí stav všech přijatých zásad dodržování předpisů. Zařízení, která během tohoto období nevrátí stav, se považují za nedodržující předpisy. Výchozí hodnota je 30 dní. Minimální hodnota je 1 den.

  Toto nastavení ukazuje, že **je aktivní** výchozí zásada dodržování předpisů (**zařízení** > **monitorují** > **Nastavení dodržování předpisů**). Úloha na pozadí pro tyto zásady se spouští jednou denně.

Pomocí těchto integrovaných zásad můžete tato nastavení monitorovat. Intune také aktualizuje [nebo zjišťuje aktualizace](create-compliance-policy.md#refresh-cycle-times) v různých intervalech v závislosti na platformě zařízení. [Běžné otázky, problémy a řešení se zásadami a profily zařízení v Microsoft Intune](../configuration/device-profile-troubleshoot.md) jsou dobrým prostředkem.

Sestavy dodržování předpisů představují skvělý způsob, jak můžete kontrolovat stav zařízení. [Zásady dodržování předpisů monitorují](compliance-policy-monitor.md) některé doprovodné materiály.

## <a name="non-compliance-and-conditional-access-on-the-different-platforms"></a>Nedodržování předpisů a podmíněný přístup na různých platformách

Následující tabulka popisuje, jak se spravují nevyhovující nastavení při použití zásad dodržování předpisů se zásadami podmíněného přístupu.

---------------------------

|**Nastavení zásad**| **Platforma** |
| --- | ----|
| **Konfigurace kódu PIN nebo hesla** | - **Android 4,0 a novější**: v karanténě<br>- **Samsung KNOX standard 4,0 a novější**: v karanténě<br>- **Android Enterprise**: v karanténě  <br>  <br>- **iOS 8,0 a novější**: Opraveno<br>- **macOS 10,11 a novější**: Opraveno  <br>  <br>- **Windows 8.1 a novější**: Opraveno<br>- **Windows Phone 8,1 a novější**: Opraveno|
| **Šifrování zařízení** | - **Android 4,0 a novější**: v karanténě<br>- **Samsung KNOX standard 4,0 a novější**: v karanténě<br>- **Android Enterprise**: v karanténě<br><br>- **iOS 8,0 a novější**: opravené (nastavením PIN kódu)<br>- **macOS 10,11 a novější**: opravené (nastavením PIN kódu)<br><br>- **Windows 8.1 a novější**: nejde použít.<br>- **Windows Phone 8,1 a novější**: Opraveno |
| **Zařízení s jailbreakem nebo rootem** | - **Android 4,0 a novější**: v karanténě (nejedná se o nastavení)<br>- **Samsung KNOX standard 4,0 a novější**: v karanténě (nejedná se o nastavení)<br>- **Android Enterprise**: v karanténě (nejedná se o nastavení)<br><br>- **iOS 8,0 a novější**: v karanténě (nejedná se o nastavení)<br>- **macOS 10,11 a novější**: nelze použít<br><br>- **Windows 8.1 a novější**: nejde použít.<br>- **Windows Phone 8,1 a novější**: nelze použít |
| **E-mailový profil** | - **Android 4,0 a novější**: nejde použít.<br>- **Samsung KNOX standard 4,0 a novější**: nejde použít.<br>- **Android Enterprise**: nejde použít.<br><br>- **iOS 8,0 a novější**: v karanténě<br>- **macOS 10,11 a novější**: v karanténě<br><br>- **Windows 8.1 a novější**: nejde použít.<br>- **Windows Phone 8,1 a novější**: nelze použít |
| **Minimální verze operačního systému** | - **Android 4,0 a novější**: v karanténě<br>- **Samsung KNOX standard 4,0 a novější**: v karanténě<br>- **Android Enterprise**: v karanténě<br><br>- **iOS 8,0 a novější**: v karanténě<br>- **macOS 10,11 a novější**: v karanténě<br><br>- **Windows 8.1 a novější**: v karanténě<br>- **Windows Phone 8,1 a novější**: v karanténě |
| **Maximální verze operačního systému** | - **Android 4,0 a novější**: v karanténě<br>- **Samsung KNOX standard 4,0 a novější**: v karanténě<br>- **Android Enterprise**: v karanténě<br><br>- **iOS 8,0 a novější**: v karanténě<br>- **macOS 10,11 a novější**: v karanténě<br><br>- **Windows 8.1 a novější**: v karanténě<br>- **Windows Phone 8,1 a novější**: v karanténě |
| **Ověření stavu Windows** | - **Android 4,0 a novější**: nejde použít.<br>- **Samsung KNOX standard 4,0 a novější**: nejde použít.<br>- **Android Enterprise**: nejde použít.<br><br>- **iOS 8,0 a novější**: nejde použít.<br>- **macOS 10,11 a novější**: nelze použít<br><br>- **Windows 10 a Windows 10 Mobile**: v karanténě<br>- **Windows 8.1 a novější**: v karanténě<br>- **Windows Phone 8,1 a novější**: nelze použít |

---------------------------

**Opraveno**: operační systém zařízení vynutil dodržování předpisů. Uživatel musí třeba zadat kód PIN.

**V karanténě**: operační systém zařízení nevynutil dodržování předpisů. Například zařízení s Androidem a Androidem Enterprise nevynutí uživatele šifrovat zařízení. Pokud zařízení nevyhovuje, provedou se následující akce:

- Pokud se zásady podmíněného přístupu vztahují na uživatele, zařízení se zablokuje.
- Aplikace Portál společnosti upozorní uživatele na jakékoli problémy s dodržováním předpisů.

## <a name="next-steps"></a>Další kroky

- [Vytvořte zásadu](create-compliance-policy.md) a zobrazte požadované součásti.
- Podívejte se na nastavení dodržování předpisů pro různé platformy zařízení:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 a vyšší](compliance-policy-create-windows-8-1.md)
  - [Windows 10 a novější](compliance-policy-create-windows.md)

- [Referenční informace pro entity zásad](../developer/reports-ref-policy.md) obsahují informace o entitách zásad datového skladu Intune.
