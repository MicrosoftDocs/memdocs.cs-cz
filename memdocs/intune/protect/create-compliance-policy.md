---
title: Vytvoření zásad dodržování předpisů pro zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Vytvoření zásad dodržování předpisů pro zařízení, Přehled stavů a úrovní závažnosti, použití stavu V období odkladu, práce s podmíněným přístupem, zpracování zařízení bez přiřazené zásady a rozdíly v dodržování předpisů na portálu Azure Portal a Classic v nástroji Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
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
ms.openlocfilehash: 7275963f521955c9e89c4b417c11f752e2f06ce1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329483"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Vytvoření zásady dodržování předpisů v Microsoft Intune

Zásady dodržování předpisů pro zařízení jsou klíčovou funkcí Intune, která umožňuje chránit prostředky organizace. V Intune můžete vytvořit pravidla a nastavení, která musí zařízení splňovat, aby se považovala za vyhovující, jako je třeba minimální verze operačního systému. Pokud zařízení nedodržuje předpisy, můžete zablokovat přístup k datům a prostředkům pomocí [podmíněného přístupu](conditional-access.md).

Můžete také provést akce při nedodržení předpisů, jako je například odeslání e-mailu s oznámením uživateli. Základní informace o tom, jaké zásady dodržování předpisů dělají a jak se používají, najdete v tématu [Začínáme s dodržováním předpisů zařízením](device-compliance-get-started.md).

V tomto článku najdete:

- Obsahuje seznam požadavků a kroků pro vytvoření zásady dodržování předpisů.
- Ukazuje, jak přiřadit zásady vašim skupinám uživatelů a zařízení.
- V této části najdete popis dalších funkcí, včetně tagů oboru pro filtrování zásad a kroků, které můžete provést na zařízeních, která nedodržují předpisy.
- Vypíše časy obnovení při vracení se změnami, když zařízení dostanou aktualizace zásad.

## <a name="before-you-begin"></a>Před zahájením

Pokud chcete používat zásady dodržování předpisů zařízením, ujistěte se, že jste:

- Použití následujících předplatných:

  - Intune
  - Pokud používáte podmíněný přístup, budete potřebovat Azure Active Directory (AD) Premium Edition. [Azure Active Directory Price](https://azure.microsoft.com/pricing/details/active-directory/) uvádí, co se vám s různými edicemi dostanou. Dodržování předpisů v Intune nevyžaduje Azure AD.

- Použití podporované platformy:

  - Správce zařízení s Androidem
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Wvdows Phone 8.1

- Registrace zařízení v Intune (vyžaduje se pro zobrazení stavu dodržování předpisů)

- Zaregistrujte zařízení jednomu uživateli nebo se zaregistrujte bez primárního uživatele. Zařízení zaregistrovaná pro více uživatelů nejsou podporovaná.

## <a name="create-the-policy"></a>Vytvoření zásady

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **zásady dodržování předpisů** > **vytvořit zásadu**.

3. Zadejte následující vlastnosti:

   - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **Označit zařízení s jailbreakem/iPadOS jailbreak jako nevyhovující předpisům**.

   - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

   - **Platforma**: vyberte platformu zařízení. Možnosti:
     - **Správce zařízení s Androidem**
     - **Android Enterprise**
     - **iOS/iPadOS**
     - **macOS**
     - **Windows Phone 8.1**
     - **Windows 8.1 a novější**
     - **Windows 10 a novější**

     Pro *Android Enterprise*musíte vybrat **typ profilu**:
     - **Vlastník zařízení**
     - **Pracovní profil**

   - **Nastavení**: Následující seznam článků popisuje nastavení pro jednotlivé platformy:
     - [Správce zařízení s Androidem](compliance-policy-create-android.md)
     - [Android Enterprise](compliance-policy-create-android-for-work.md)
     - [iOS/iPadOS](compliance-policy-create-ios.md)
     - [macOS](compliance-policy-create-mac-os.md)
     - [Windows Phone 8,1, Windows 8.1 a novější](compliance-policy-create-windows-8-1.md)
     - [Windows 10 a novější](compliance-policy-create-windows.md)  

   - **Umístění** *(Správce zařízení s Androidem)* : v zásadách můžete vynutit dodržování předpisů podle umístění zařízení. Vyberte si z existujících umístění. Žádné umístění ještě nemáte? V Intune jsou k dispozici pokyny k [použití umístění (síťová síť)](use-network-locations.md) .  

   - **Akce při nedodržení předpisů**: u zařízení, která nevyhovují zásadám dodržování předpisů, můžete přidat posloupnost akcí, které se mají použít automaticky. Pokud je zařízení označené jako nevyhovující, můžete plán třeba další den změnit. Můžete také nakonfigurovat druhou akci, která uživateli nevyhovujícího zařízení pošle e-mail.

     Další informace, včetně návodu na vytvoření e-mailu s oznámením pro uživatele, najdete v článku o [přidání akcí pro nevyhovující zařízení](actions-for-noncompliance.md).

     Pokud například používáte funkci Umístění, přidáte do zásady dodržování předpisů nějaké umístění a vyberete aspoň jedno umístění, použije se pro nevyhovující zařízení výchozí akce. Pokud zařízení není připojené k vybraným umístěním, považuje se hned za nevyhovující. Uživatelům můžete dát určitou lhůtu, třeba jeden den.

   - **Scope (značky)** : značky oboru představují skvělý způsob, jak filtrovat zásady na konkrétní skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Po přidání nastavení můžete také přidat značku oboru do zásad dodržování předpisů. [Použití značek oboru k filtrování zásad](../fundamentals/scope-tags.md) je dobrým prostředkem.

4. Po dokončení vyberte **OK** > **vytvořit** a uložte provedené změny. Zásada se vytvoří a zobrazí se v seznamu. Potom tyto zásady přiřaďte do skupin.

## <a name="assign-the-policy"></a>Přiřazení zásady

Po vytvoření zásady je dalším krokem přiřazení těchto zásad ke skupinám:

1. Vyberte zásadu, kterou jste vytvořili. Existující zásady jsou v **zařízeních** > **zásadách dodržování předpisů** > **zásady**.

2. Vyberte *zásady* > **přiřazení**. Můžete zahrnout nebo vyloučit skupiny zabezpečení služby Azure Active Directory (AD).

3. Vyberte **Vybrané skupiny** a zobrazte skupiny zabezpečení Azure AD. Vyberte skupiny, které chcete použít pro tuto zásadu > klikněte na **Uložit** a zásadu nasaďte.

Uživatelé nebo zařízení, na které vaše zásada cílí, se vyhodnotí pro dodržování předpisů při jejich vrácení se změnami pomocí Intune.

### <a name="evaluate-how-many-users-are-targeted"></a>Vyhodnocení počtu cílových uživatelů

Když přiřadíte zásady, můžete také **vyhodnotit** , kolik uživatelů je ovlivněno. Tato funkce vypočítává uživatele. nepočítá zařízení.

1. V Intune vyberte **zařízení** > **zásady dodržování předpisů** > **zásady**.

2. Vyberte *zásadu* > **přiřazení** > **vyhodnotit**. Zobrazí se zpráva o tom, kolik uživatelů cílí na tyto zásady.

Pokud je tlačítko **vyhodnotit** šedé, ujistěte se, že je zásada přiřazena jedné nebo více skupinám.

<!-- ## Actions for noncompliance

For devices that don't meet your compliance policies, you can add a sequence of actions to apply automatically. You can change the schedule when the device is marked non-compliant, such as after one day. You can also configure a second action that sends an email to the user when the device isn't compliant.

[Add actions for noncompliant devices](actions-for-noncompliance.md) provides more information, including creating a notification email to your users.

For example, you're using the Locations feature, and add a location in a compliance policy. The default action for noncompliance applies when you select at least one location. If the device isn't connected to the selected locations, it's immediately considered not compliant. You can give your users a grace period, such as one day.

## Scope tags

Scope tags are a great way to assign and filter policies to specific groups, such as Sales, HR, All US-NC employees, and so on. After you add the settings, you can also add a scope tag to your compliance policies. [Use scope tags to filter policies](../fundamentals/scope-tags.md) is a good resource.
-->

## <a name="refresh-cycle-times"></a>Aktualizovat časy cyklů

Intune používá ke kontrole aktualizací zásad dodržování předpisů různé aktualizační cykly. Pokud se zařízení nedávno zaregistrovalo, vrácení se změnami se spouští častěji. V [cyklech aktualizace zásad a profilů](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) se zobrazí odhadované časy aktualizace.

V každém okamžiku můžou uživatelé aplikaci Portál společnosti otevřít a synchronizovat zařízení, aby se aktualizace zásad hned zkontrolovaly.

### <a name="assign-an-ingraceperiod-status"></a>Přiřazení stavu V období odkladu

Stav V období odkladu u zásad dodržování předpisů představuje hodnotu. Tuto hodnotu určuje kombinace období odkladu a skutečný stav daných zásad dodržování předpisů u zařízení.

Konkrétně, pokud má zařízení pro přiřazené zásady dodržování předpisů stav Nevyhovující předpisům a:

- K zařízení není přiřazené žádné období odkladu, ale přiřazená hodnota zásady dodržování předpisů není kompatibilní.
- Zařízení má období odkladu, které vypršelo, takže přiřazená hodnota zásady dodržování předpisů není kompatibilní.
- Zařízení má období odkladu, které je v budoucnu, takže přiřazená hodnota pro zásady dodržování předpisů je V období odkladu.

V následující tabulce najdete souhrnný přehled těchto bodů:

|Skutečný stav dodržování předpisů|Hodnota přiřazeného období odkladu|Účinný stav dodržování předpisů|
|---------|---------|---------|
|Nevyhovující předpisům |Bez přiřazeného období odkladu |Nevyhovující předpisům |
|Nevyhovující předpisům |Včerejší datum|Nevyhovující předpisům|
|Nevyhovující předpisům |Zítřejší datum|V období odkladu|

Další informace o monitorování zásad dodržování předpisů zařízením najdete v článku [Monitorování zásad dodržování předpisů zařízením v Intune](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Přiřazení výsledného stavu zásad dodržování předpisů

Pokud má nějaké zařízení několik zásad dodržování předpisů a pro dvě nebo více z nich má různé stavy dodržování předpisů, přiřadí se mu jediný výsledný stav dodržování předpisů. Toto přiřazení vychází z koncepční úrovně závažnosti přiřazené jednotlivých stavům dodržování předpisů. Jednotlivé stavy dodržování předpisů mají následující úroveň závažnosti:

|Stav  |Závažnost  |
|---------|---------|
|Neznámé     |1|
|Neužívá se     |2|
|Kompatibilní|3|
|V období odkladu|4|
|Nevyhovující předpisům|5|
|Chyba|6|

Pokud má zařízení více zásad dodržování předpisů, přiřadí se mu nejvyšší úroveň závažnosti ze všech zásad.

Například zařízení má přiřazené tři zásady dodržování předpisů: jeden neznámý stav (závažnost = 1), jeden stav kompatibility (závažnost = 3) a jeden stav V období odkladu (závažnost = 4). Stav V období odkladu má nejvyšší úroveň závažnosti. To znamená, že všechny tři zásady mají stav dodržování předpisů V období odkladu.

## <a name="next-steps"></a>Další kroky

[Monitorujte své zásady](compliance-policy-monitor.md).
