---
title: Vytvoření zásad dodržování předpisů pro zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Vytvoření zásad dodržování předpisů pro zařízení, Přehled stavů a úrovní závažnosti, použití stavu V období odkladu, práce s podmíněným přístupem, zpracování zařízení bez přiřazené zásady a rozdíly v dodržování předpisů na portálu Azure Portal a Classic v nástroji Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
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
ms.openlocfilehash: f84df30204f866e5498e97b8d64ed3fc6fd4ba28
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084908"
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

2. Vyberte **zařízení** > **zásady dodržování předpisů** > **zásady** > **vytvořit zásadu**.

3. Vyberte **platformu** pro tuto zásadu z následujících možností:
   - *Správce zařízení s Androidem*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 a novější*
   - *Windows 10 a novější*

    Pro *Android Enterprise*vyberete také **Typ zásady**:
     - *Zásady dodržování předpisů pro vlastníka zařízení s Androidem*
     - *Zásady dodržování předpisů pracovního profilu Androidu*

    Pak vyberte **vytvořit** a otevřete tak okno **vytvořit konfiguraci zásad** .

4. Na kartě **základy** zadejte **název** , který vám pomůže je později identifikovat. Dobrým názvem zásad je například **Označit zařízení s jailbreakem/iPadOS jailbreak jako nevyhovující předpisům**.

   Můžete také zvolit, že chcete zadat **Popis**.
  
5. Na kartě **Nastavení dodržování předpisů** rozbalte dostupné kategorie a nakonfigurujte nastavení pro zásady.  Následující články popisují nastavení pro jednotlivé platformy:
   - [Správce zařízení s Androidem](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8,1, Windows 8.1 a novější](compliance-policy-create-windows-8-1.md)
   - [Windows 10 a novější](compliance-policy-create-windows.md)  

6. Na kartě **umístění** můžete vynutit dodržování předpisů na základě umístění zařízení. Vyberte si z existujících umístění. Pokud ještě nemáte dostupné umístění, přečtěte si pokyny v tématu [použití umístění (síťová ochranná)](use-network-locations.md) .
   > [!TIP]
   > **Umístění** jsou dostupná jenom pro platformu pro *Správce zařízení s Androidem* .

7. Na kartě **Akce při nedodržení předpisů** určete posloupnost akcí, které se mají automaticky použít u zařízení, která nesplňují tyto zásady dodržování předpisů.

   Můžete přidat několik akcí a nakonfigurovat plány a další podrobnosti pro některé akce. Můžete například změnit plán výchozí akce *Označit zařízení jako nevyhovující* , aby se mohlo objevit po jednom dni. Pak můžete přidat akci, která uživateli pošle e-mail, když zařízení nedodržuje upozornění na tento stav. Můžete také přidat akce, které budou zamykat nebo vyřadit zařízení, která nedodržují předpisy.

   Informace o akcích, které můžete konfigurovat, najdete v tématu [Přidání akcí pro zařízení nedodržující předpisy](actions-for-noncompliance.md), včetně postupu vytváření e-mailů s oznámením, které se budou posílat uživatelům.

   Další příklad obsahuje umístění, kam přidáte alespoň jedno umístění k zásadě dodržování předpisů. V takovém případě se výchozí akce při nedodržení předpisů použije, když vyberete aspoň jedno umístění. Pokud zařízení není připojené k žádnému z vybraných umístění, považuje se za nevyhovující. Plán můžete nakonfigurovat tak, aby uživatelům poskytl období odkladu, například jeden den.

8. Na kartě **značky oboru** vyberte značky, které vám pomůžou filtrovat zásady na konkrétní skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Po přidání nastavení můžete také přidat značku oboru do zásad dodržování předpisů. 

   Informace o použití značek oboru najdete v tématu [použití značek oboru k filtrování zásad](../fundamentals/scope-tags.md).

9. Na kartě **přiřazení** přiřaďte zásadu k vašim skupinám.  

   Vyberte **+ Vybrat skupiny, které chcete zahrnout** , a potom zásadu přiřaďte do jedné nebo více skupin. Zásada bude platit pro tyto skupiny, když zásadu uložíte po dalším kroku. 

10. Na kartě **Revize + vytvořit** zkontrolujte nastavení a vyberte **vytvořit** , až budete připraveni Uložit zásady dodržování předpisů.  

    Uživatelé nebo zařízení, na které vaše zásada cílí, se vyhodnotí pro dodržování předpisů při jejich vrácení s Intune.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Aktualizovat časy cyklů

Intune používá ke kontrole aktualizací zásad dodržování předpisů různé aktualizační cykly. Pokud se zařízení nedávno zaregistrovalo, vrácení se změnami se spouští častěji. V [cyklech aktualizace zásad a profilů](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) se zobrazí odhadované časy aktualizace.

V každém okamžiku můžou uživatelé aplikaci Portál společnosti otevřít a synchronizovat zařízení, aby se aktualizace zásad hned zkontrolovaly.

### <a name="assign-an-ingraceperiod-status"></a>Přiřazení stavu V období odkladu

Stav V období odkladu u zásad dodržování předpisů představuje hodnotu. Tato hodnota je určena kombinací období odkladu zařízení a skutečným stavem zařízení pro tyto zásady dodržování předpisů.

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
