---
title: Zásady dodržování předpisů zařízením v Microsoft Intune – Azure | Microsoft Docs
description: Začněte s používáním zásad dodržování předpisů, včetně nastavení zásad dodržování předpisů a zásad dodržování předpisů zařízeními pro Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/28/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227a44436f4490c9b3e2188609a9714a0e842149
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206311"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Použití zásad dodržování předpisů k nastavení pravidel pro zařízení, která spravujete pomocí Intune

Řešení pro správu mobilních zařízení (MDM), jako je Intune, může přispět k ochraně dat organizace tím, že vyžaduje, aby uživatelé a zařízení splnili některé požadavky. V Intune se tato funkce nazývá *zásady dodržování předpisů*.

Zásady dodržování předpisů v Intune:

- Definujte pravidla a nastavení, která musí uživatelé a zařízení splňovat, aby vyhovovaly předpisům.
- Zahrňte akce, které se vztahují na zařízení, která nedodržují předpisy. Akce při nedodržení předpisů mohou upozornit uživatele na podmínky nedodržení předpisů a zabezpečit data na zařízeních nesplňujících požadavky.
- Lze [kombinovat s podmíněným přístupem](#integrate-with-conditional-access), který pak může zablokovat uživatele a zařízení, která pravidla nesplňují.

V Intune se používají dvě části zásad dodržování předpisů:

- **Nastavení zásad dodržování předpisů** – nastavení zásad pro všechna zařízení, která jsou jako předdefinované zásady dodržování předpisů, které obdrží všechna zařízení. Nastavení zásad dodržování předpisů nastaví základní hodnotu pro fungování zásad dodržování předpisů ve vašem prostředí Intune, včetně toho, jestli zařízení, která nepřijaly žádné zásady dodržování předpisů zařízení, splňují nebo nesplňují předpisy.

- **Zásady dodržování předpisů pro zařízení** – pravidla specifická pro platformu, která nakonfigurujete a nasadíte na skupiny uživatelů nebo zařízení.  Tato pravidla definují požadavky na zařízení, například minimální operační systémy nebo použití šifrování disku. Zařízení musí splňovat tato pravidla, aby se považovala za vyhovující.

Podobně jako u jiných zásad Intune závisí hodnocení zásad dodržování předpisů pro zařízení, když se zařízení zaregistruje pomocí Intune, a [cykly aktualizace zásad a profilů](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="compliance-policy-settings"></a>Nastavení zásad dodržování předpisů

*Nastavení zásad dodržování předpisů* jsou nastavení v rámci tenanta, která určují, jak služba Intune dodržuje předpisy s vašimi zařízeními. Tato nastavení se liší od nastavení, která konfigurujete v zásadě dodržování předpisů zařízením.

Pokud chcete spravovat nastavení zásad dodržování předpisů, přihlaste se do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) a v části **Endpoint security**  >  **Device compliance**  >  **nastavení zásad dodržování**předpisů zařízením Endpoint Security.

Nastavení zásad dodržování předpisů zahrnuje následující nastavení:

- **Označit zařízení, která nemají přiřazené žádné zásady dodržování předpisů**

  Toto nastavení určuje, jak Intune považuje zařízení, která nebyla přiřazena zásada dodržování předpisů zařízením. Toto nastavení má dvě hodnoty:
  - **Kompatibilní** (*výchozí*): Tato funkce zabezpečení je vypnutá. Zařízení, která neodesílají zásady dodržování předpisů zařízením, se považují za *vyhovující*.
  - **Nedodržuje předpisy**: Tato funkce zabezpečení je zapnutá. Zařízení, která nepřijala zásady dodržování předpisů pro zařízení, se považují za nedodržující předpisy.

  Pokud používáte podmíněný přístup se zásadami dodržování předpisů zařízením, doporučujeme toto nastavení změnit na **nekompatibilní** , aby se zajistilo, že přístup k prostředkům budou mít jenom zařízení, která jsou potvrzená jako vyhovující.

  Pokud koncový uživatel nedodržuje předpisy, protože není přiřazená žádná zásada, [aplikace Portál společnosti](../apps/company-portal-app.md) nezobrazuje žádné zásady dodržování předpisů.

- **Vylepšená detekce jailbreaků** (*platí jenom pro iOS/iPadOS*)

  Toto nastavení funguje jenom u zařízení, na která cílíte, pomocí zásad dodržování předpisů zařízením, která blokují zařízení s jailbreakem.  (Další informace najdete v tématu nastavení [stav zařízení](compliance-policy-create-ios.md#device-health) pro iOS/iPadOS).

  Toto nastavení má dvě hodnoty:

  - **Zakázáno** (*výchozí*): Tato funkce zabezpečení je vypnutá. Toto nastavení nemá žádný vliv na zařízení, která přijímají zásady dodržování předpisů zařízením, které blokují zařízení s jailbreakem.
  - **Povoleno**: Tato funkce zabezpečení je zapnutá. Zařízení, která přijímají zásady dodržování předpisů zařízením k blokování zařízení s jailbreakem, využívají vylepšenou detekci jailbreaků.

  Pokud je tato možnost povolená u příslušného zařízení se systémem iOS/iPadOS, zařízení:

  - Povolí služby zjišťování polohy na úrovni operačního systému.
  - Vždy umožňuje Portál společnosti používat lokátorové služby.
  - Používá své služby zjišťování polohy k častému spouštění detekce jailbreaků na pozadí. Data o umístění uživatele neukládá Intune.

  Vylepšené zjišťování jailbreaků spouští vyhodnocení v těchto případech:

  - Otevře se aplikace Portál společnosti.
  - Zařízení fyzicky přesune významnou vzdálenost, což je přibližně 500 metrů nebo více. Intune nemůže zaručit, že při každé významné změně umístění dojde k jailbreaků kontrole zjišťování, protože tato kontrolu závisí na síťovém připojení zařízení v čase.

  U iOS 13 a dalších funkcí Tato funkce vyžaduje, aby uživatelé *vždy* , když se jim zobrazí výzva, aby mohli dál povolit portál společnosti používání jejich umístění na pozadí. Pokud uživatelé nemají vždycky povolený přístup k poloze a mají nakonfigurovanou zásadu s tímto nastavením, je jejich zařízení označeno jako nedodržující předpisy.

- **Doba platnosti stavu dodržování předpisů (dny)**

  Zadejte období, během kterého musí zařízení úspěšně nahlásit všechny přijaté zásady dodržování předpisů. Pokud zařízení nehlásí stav dodržování předpisů pro zásadu ještě před vypršením doby platnosti, bude se zařízení považovat za nedodržující předpisy.

  Ve výchozím nastavení je období nastaveno na 30 dní. Můžete nakonfigurovat období od 1 do 120 dnů.

  Můžete zobrazit podrobnosti o dodržování předpisů zařízením v nastavení doby platnosti. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a přejít na **zařízení**  >  **sledování**  >  **Nastavení dodržování předpisů**. Toto nastavení má ve sloupci *Nastavení* **aktivní** název.  Další informace o tomto a souvisejícím zobrazení stavu dodržování předpisů najdete v tématu [monitorování dodržování předpisů zařízením](compliance-policy-monitor.md).

## <a name="device-compliance-policies"></a>Zásady dodržování předpisů pro zařízení

Zásady dodržování předpisů zařízením v Intune:

- Definujte pravidla a nastavení, která musí uživatelé a spravovaná zařízení splňovat, aby vyhovovaly předpisům. Příklady pravidel: vyžaduje, aby na zařízeních běžela minimální verze operačního systému, jailbreak nebo root a na *úrovni hrozby* , která je určená softwarem pro správu hrozeb, který jste integroval s Intune.
- Podpůrné akce, které se vztahují na zařízení, která nesplňují vaše pravidla dodržování předpisů. Mezi příklady akcí patří vzdálené uzamčení nebo odeslání e-mailu uživatele zařízení o stavu zařízení, aby je mohl opravit.
- Nasazení na uživatele ve skupinách uživatelů nebo v zařízeních ve skupinách zařízení. Když se zásady dodržování předpisů nasadí uživateli, kontrolují se dodržování předpisů u všech zařízení uživatele. Použití skupin zařízení pomáhá v této situaci s vykazováním dodržování předpisů.

Pokud používáte podmíněný přístup, vaše zásady podmíněného přístupu můžou pomocí výsledků dodržování předpisů zařízením zablokovat přístup k prostředkům ze zařízení nesplňujících požadavky.

Dostupná nastavení, která můžete zadat v zásadách dodržování předpisů zařízením, závisí na typu platformy, který jste vybrali při vytváření zásad. Různé platformy zařízení podporují různá nastavení a každý typ platformy vyžaduje samostatnou zásadu.  

Následující témata odkazují na vyhrazené články pro různé aspekty zásad konfigurace zařízení.

- [**Akce při nedodržení předpisů**](actions-for-noncompliance.md) – Každá zásada dodržování předpisů pro zařízení zahrnuje jednu nebo více akcí při nedodržení předpisů. Tyto akce jsou pravidla, která se aplikují na zařízení, která nesplňují podmínky nastavené v zásadách.

  Ve výchozím nastavení zahrnuje Každá zásada dodržování předpisů zařízením akci, která zařízení označí jako nedodržující předpisy, pokud se nepovede splnit pravidlo zásad. Zásady se pak vztahují na zařízení jakékoli další akce při nedodržení předpisů, které jste nakonfigurovali v závislosti na plánech, které jste pro tyto akce nastavili.

  Akce při nedodržení předpisů může pomáhat uživatelům upozornit, když zařízení nedodržuje předpisy nebo chrání data, která se můžou na zařízení nacházet. Mezi příklady akcí patří:

  - **Odesílání e-mailových upozornění** uživatelům a skupinám s podrobnostmi o zařízení, které nedodržuje předpisy. Zásadu můžete nakonfigurovat tak, aby odesílala e-mail hned po označení nedodržující předpisy, a pak ji znovu pravidelně, až do doby, kdy bude zařízení kompatibilní.
  - **Vzdáleně zamkne zařízení** , která po nějakou dobu nedodržují předpisy.
  - **Vyřadit zařízení** po nějakou dobu jako nevyhovující. Tato akce odebere zařízení ze správy Intune a odebere ze zařízení všechna firemní data.

- [**Konfigurace síťových umístění**](use-network-locations.md) – podporovaná zařízeními s Androidem můžete nakonfigurovat *Síťová umístění* a pak tato umístění používat jako pravidlo dodržování předpisů pro zařízení. Tento typ pravidla může označit zařízení jako nevyhovující, pokud je mimo nebo opustí zadanou síť. Než budete moct zadat pravidlo umístění, musíte nakonfigurovat síťová umístění.

- [**Vytvoření zásady**](create-compliance-policy.md) – pomocí informací v tomto článku si můžete projít požadavky, pracovat prostřednictvím možností pro konfiguraci pravidel, určit akce při nedodržení předpisů a přiřadit zásady do skupin. Tento článek obsahuje také informace o časech aktualizace zásad.

  Podívejte se na nastavení dodržování předpisů pro zařízení na různých platformách zařízení:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 a vyšší](compliance-policy-create-windows-8-1.md)
  - [Windows 10 a novější](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Monitorovat stav kompatibility

Intune obsahuje řídicí panel pro dodržování předpisů zařízením, který můžete použít k monitorování stavu dodržování předpisů zařízení, a pro další informace v podrobnostech o zásadách a zařízeních. Další informace o tomto řídicím panelu najdete v tématu [monitorování dodržování předpisů zařízením](compliance-policy-monitor.md).

## <a name="integrate-with-conditional-access"></a>Integrace s podmíněným přístupem

Když použijete podmíněný přístup, můžete nakonfigurovat zásady podmíněného přístupu, které budou používat výsledky zásad dodržování předpisů pro zařízení, a určit, která zařízení budou mít přístup k prostředkům vaší organizace. Toto řízení přístupu se navíc liší od akcí při nedodržení předpisů, které zahrnete do zásad dodržování předpisů pro zařízení.

Když se zařízení zaregistruje v Intune, zaregistruje se ve službě Azure AD. Stav dodržování předpisů pro zařízení je hlášený službě Azure AD. Pokud mají zásady podmíněného přístupu nastavené oprávnění *vyžadovat, aby zařízení bylo označené jako vyhovující*, podmíněný přístup pomocí tohoto stavu dodržování předpisů určí, jestli má udělit nebo blokovat přístup k e-mailu a dalším prostředkům organizace.

Pokud budete používat stav dodržování předpisů zařízením se zásadami podmíněného přístupu, přečtěte si, jak má tenant nakonfigurovaná *označení zařízení bez přiřazených zásad dodržování předpisů*, která spravujete v [nastavení zásad dodržování předpisů](#compliance-policy-settings).

Další informace o použití podmíněného přístupu se zásadami dodržování předpisů pro zařízení najdete v tématu [podmíněný přístup na základě zařízení](conditional-access-intune-common-ways-use.md#device-based-conditional-access) .

Přečtěte si další informace o podmíněném přístupu v dokumentaci k Azure AD:

- [Co je podmíněný přístup](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Co je identita zařízení](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Referenční informace o nedodržení předpisů a podmíněném přístupu na různých platformách

Následující tabulka popisuje, jak se spravují nevyhovující nastavení při použití zásad dodržování předpisů se zásadami podmíněného přístupu.

- **Opraveno**: operační systém zařízení vynutil dodržování předpisů. Uživatel musí třeba zadat kód PIN.

- **V karanténě**: operační systém zařízení nevynutil dodržování předpisů. Například zařízení s Androidem a Androidem Enterprise nevynutí uživatele šifrovat zařízení. Pokud zařízení nevyhovuje, provedou se následující akce:
  - Pokud se zásady podmíněného přístupu vztahují na uživatele, zařízení se zablokuje.
  - Aplikace Portál společnosti upozorní uživatele na jakékoli problémy s dodržováním předpisů.

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

## <a name="next-steps"></a>Další kroky

- [Konfigurace umístění](../protect/use-network-locations.md) pro použití se zařízeními s Androidem
- [Vytvoření a nasazení zásad](../protect/create-compliance-policy.md) a Kontrola požadavků
- [Monitorování dodržování předpisů zařízením](../protect/compliance-policy-monitor.md)
- [Běžné otázky, problémy a řešení se zásadami a profily zařízení v Microsoft Intune](../configuration/device-profile-troubleshoot.md)
- [Referenční informace pro entity zásad](../developer/reports-ref-policy.md) obsahují informace o entitách zásad datového skladu Intune.
