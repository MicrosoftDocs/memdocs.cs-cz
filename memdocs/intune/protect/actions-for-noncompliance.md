---
title: Zpráva a akce při nedodržení předpisů v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte e-mailové oznámení, které se odešle do zařízení nedodržujícího předpisy. Přidejte akce, které se provedou, když je zařízení označeno jako nedodržující předpisy. Můžete třeba přidat období odkladu, během kterého musí uživatel dodržení předpisů zajistit, nebo vytvořit plán k zablokování přístupu, dokud zařízení nebude předpisy dodržovat. Použijte k tomu Microsoft Intune v Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b74ea17e0fdadfbb6f7c1ec82e502f57187ba74e
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864916"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Konfigurace akcí pro zařízení nedodržující předpisy v Intune

U zařízení, která nevyhovují zásadám nebo pravidlům dodržování předpisů, můžete přidat **Akce při nedodržení předpisů**. Tato funkce konfiguruje posloupnost akcí uspořádaných podle času, například e-mailem koncového uživatele a dalších.

## <a name="overview"></a>Přehled

Ve výchozím nastavení Každá zásada dodržování předpisů zahrnuje akci při nedodržení předpisů **Označit zařízení jako nekompatibilní** s plánem nula dnů (**0**). Výsledkem tohoto výchozího nastavení je, že Intune zjistí, že zařízení nedodržuje předpisy, Intune hned zařízení označí jako nedodržující předpisy. Pak bude [podmíněný přístup](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) Azure Active Directory (AD) moci zařízení blokovat.

Konfigurací **akcí při nedodržení předpisů** získáte flexibilitu při rozhodování o tom, co dělat pro zařízení nedodržující předpisy, a kdy to udělat. Například můžete zvolit, aby zařízení neblokovalo okamžitě, a dát uživateli možnost, aby se zajistilo, že bude dodržovat předpisy.

Pro každou akci, kterou můžete nastavit, můžete nakonfigurovat plán, který určuje, kdy se tato akce projeví na základě počtu dní, po kterých je zařízení označeno jako nedodržující předpisy. Můžete také nakonfigurovat více instancí akce. Když v zásadě nastavíte více instancí akce, akce se spustí znovu v pozdějším naplánovaném čase, pokud zařízení zůstává nekompatibilní.

Ne všechny akce jsou k dispozici pro všechny platformy.

## <a name="available-actions-for-noncompliance"></a>Dostupné akce při nedodržení předpisů

K dispozici jsou následující akce při nedodržení předpisů. Pokud není uvedeno jinak, každá akce je k dispozici pro všechny platformy podporované službou Intune:

- **Označit zařízení jako nevyhovující**: ve výchozím nastavení je tato akce nastavená pro každou zásadu dodržování předpisů a má časový plán nula (**0**), což znamená, že zařízení se ihned označí jako nedodržující předpisy.

  Když změníte výchozí plán, zadáte dobu odkladu, ve které může uživatel opravit problémy nebo že bude kompatibilní bez označení jako nevyhovující.

- **Odeslat e-mail koncovému uživateli**: Tato akce odešle uživateli e-mailové oznámení.
Když povolíte tuto akci:

  - Vyberte *šablonu zprávy s oznámením* , kterou tato akce odešle. Než budete moct přiřadit jednu tuto akci, musíte [vytvořit šablonu zprávy s oznámením](#create-a-notification-message-template) . Když vytvoříte vlastní oznámení, přizpůsobíte předmět, text zprávy a může obsahovat logo společnosti, název společnosti a další kontaktní informace.
  - Zvolte, že se má zpráva odeslat dalším příjemcům výběrem jedné nebo více skupin Azure AD.

Po odeslání e-mailu Intune zahrne do e-mailového oznámení podrobnosti o zařízení, které nedodržuje předpisy.

- **Vzdáleně uzamknout zařízení, které nedodržuje předpisy**: pomocí této akce můžete vystavit vzdálený zámek zařízení. Uživateli se zobrazí výzva k zadání PIN kódu nebo hesla k odemknutí zařízení. Další informace o funkci [vzdáleného uzamčení](../remote-actions/device-remote-lock.md).

- **Vyřazení zařízení nesplňujících požadavky**: Tato akce odebere ze zařízení všechna firemní data a odebere zařízení ze správy Intune. Aby nedocházelo k náhodnému vymazání zařízení, tato akce podporuje minimální plán na **30** dní.

  Tuto akci podporují následující platformy:
  - Android
  - iOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 nebo novější

  Přečtěte si další informace o [vyřazování zařízení z provozu](../remote-actions/devices-wipe.md#retire).

- **Odeslat nabízené oznámení koncovému uživateli**: Nakonfigurujte tuto akci pro odeslání nabízeného oznámení o nedodržení předpisů zařízení prostřednictvím aplikace Portál společnosti nebo aplikace Intune na zařízení.

  Tuto akci podporují následující platformy:
  - Android:
    - Správce zařízení s Androidem
    - Vlastník zařízení se systémem Android Enterprise
    - Pracovní profil Android Enterprise
  - iOS/iPadOS

  Nabízené oznámení se odešle při prvním ověření zařízení v Intune a zjistí, že nedodržují předpisy pro zásady dodržování předpisů. Když uživatel vybere oznámení, otevře se aplikace Portál společnosti nebo aplikace Intune a zobrazí informace o tom, proč nejsou vyhovující. Uživatel pak může provést akci, aby problém vyřešil. Podrobnosti o nedodržení předpisů vygeneruje Intune a nedá se přizpůsobit.

  > [!IMPORTANT]
  > Intune, aplikace Portál společnosti a aplikace Microsoft Intune, nemůžou zaručit doručení nabízeného oznámení. Oznámení se můžou zobrazovat po několik hodin zpoždění, pokud je to u všech. To zahrnuje i v případě, že uživatelé vypnuli nabízená oznámení.
  >
  > Nespoléhá se na tuto metodu oznámení pro naléhavé zprávy.

  Každá instance akce odesílá oznámení v jednom okamžiku. Pokud chcete znovu odeslat stejné oznámení ze zásady, nakonfigurujte další instance akce v této zásadě, přičemž každý z nich bude mít jiný plán.
  
  Například můžete naplánovat první akci na 0 dní a pak přidat druhou instanci akce nastavenou na tři dny. Tato prodleva před druhým oznámením uživateli přiřadí několik dní k vyřešení problému a zabrání druhému oznámení.

  Chcete-li zabránit uživatelům s e-maily s příliš velkým počtem duplicitních zpráv, přečtěte si a zjednodušte, které zásady dodržování předpisů zahrnují nabízené oznámení o nedodržení předpisů, a Projděte si plány, abyste se vyhnuli opakovanému odesílání oznámení pro stejný problém

  Rozmyslete si:
  - Pro jednu zásadu, která zahrnuje více instancí nabízených oznámení nastavených na stejný den, se za tento den pošle jenom jedno oznámení.

  - Pokud více zásad dodržování předpisů zahrnuje stejné podmínky dodržování předpisů a zahrnuje akci nabízených oznámení se stejným plánem, na stejné zařízení se ve stejný den pošle víc oznámení.

## <a name="before-you-begin"></a>Před zahájením

Při konfiguraci zásad dodržování předpisů zařízením nebo později můžete [Přidat akce, které nedodržují předpisy](#add-actions-for-noncompliance) , a to úpravou zásad. Do každé zásady můžete přidat další akce, které budou vyhovovat vašim potřebám. Mějte na paměti, že každá zásada dodržování předpisů automaticky zahrnuje výchozí akci při nedodržení předpisů, která označuje zařízení jako nedodržující předpisy s plánem nastaveným na 0 dní.

Pokud chcete používat zásady dodržování předpisů pro zařízení k blokování zařízení z firemních prostředků, musíte nastavit podmíněný přístup Azure AD. Pokyny [k použití podmíněného přístupu s Intune](conditional-access-intune-common-ways-use.md) najdete [v tématu podmíněný přístup v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) nebo běžné způsoby používání služby Intune.

Pokud chcete vytvořit zásady dodržování předpisů pro zařízení, přečtěte si následující pokyny pro konkrétní platformu:

- [Android](compliance-policy-create-android.md)
- [Pracovní profily Androidu](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Vytvoření šablony zprávy s oznámením

Pokud chcete svým uživatelům odeslat e-mail, vytvořte šablonu zprávy s oznámením. Pokud zařízení nedodržuje předpisy, musíte do šablony zadat podrobnosti, které se zobrazují v e-mailu odeslaném vašim uživatelům.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **oznámení zásady dodržování předpisů**  >  **Notifications**  >  **vytvořit oznámení**.
3. V části *základy*zadejte následující informace:

   - **Název**
   - **Subjekt**
   - **Zpráva**

4. V části *základy*nakonfigurujte pro oznámení následující možnosti, které jsou *povolené*pro všechny výchozí hodnoty:

   - **Záhlaví e-mailu – zahrnout logo společnosti**
   - **Zápatí e-mailu – uveďte název společnosti**
   - **Zápatí e-mailu – zahrnutí informací o kontaktu**

   Logo, které nahrajete jako součást brandingu Portál společnosti, se používá pro e-mailové šablony. Další informace o značce Portálu společnosti najdete v tématu o [přizpůsobení brandingu firemní identity](../apps/company-portal-app.md#customizing-the-user-experience).

   ![Příklad oznámení o dodržování předpisů v Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Pokračujte výběrem tlačítka **Next** (Další).

5. V části **Revize + vytvořit**Zkontrolujte konfigurace a ověřte, že je šablona zprávy s oznámením připravená k použití. Vytvoření oznámení dokončíte výběrem **vytvořit** .

> [!NOTE]
> Můžete také vybrat stávající šablonu oznámení, kterou jste vytvořili dříve, a **Upravit** její informace, abyste šablonu aktualizovali.

## <a name="add-actions-for-noncompliance"></a>Přidání akcí při nedodržení předpisů

Když vytvoříte zásady dodržování předpisů pro zařízení, Intune automaticky vytvoří akci pro případ nedodržování těchto předpisů. Pokud zařízení nesplňuje vaše zásady dodržování předpisů, tato akce označí zařízení jako nevyhovující. Můžete přizpůsobit, jak dlouho bude zařízení takto označené. Tuto akci není možné odebrat.

Můžete přidat volitelné akce při vytváření zásad dodržování předpisů nebo aktualizovat existující zásady.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **zásady zásady dodržování předpisů**zařízení  >  **Policies**, vyberte jednu z vašich zásad a pak vyberte **vlastnosti**.

   Ještě zásadu nemáte? Vytvořte zásadu pro [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) nebo jinou platformu.

   > [!NOTE]
   > Zařízení JAMF a zařízení nastavená pomocí skupin zařízení nemohou v současnosti přijímat akce dodržování předpisů.

3. Vyberte **Akce při nedodržení předpisů**  >  **Přidat**.

4. Vyberte vaši **Akci**:

   - **Odeslat e-mail koncovému uživateli**: Pokud zařízení nedodržuje předpisy, vyberte možnost odeslání e-mailu uživateli. Navíc:
     - Vyberte **Šablonu zprávy**, kterou jste dříve vytvořili.
     - Zadejte libovolné **Další příjemce** výběrem skupin.

   - **Vzdáleně uzamknout zařízení, které nedodržuje předpisy**: Pokud zařízení nedodržuje předpisy, uzamkněte ho. Tato akce vynutí, aby uživatel zadal kód PIN nebo heslo k odemknutí zařízení.

   - **Vyřadit zařízení nesplňující požadavky**: když zařízení nedodržuje předpisy, odeberte ze zařízení všechna firemní data a odeberte zařízení ze správy Intune.

   - **Odeslat nabízené oznámení koncovému uživateli**: Nakonfigurujte tuto akci pro odeslání nabízeného oznámení o nedodržení předpisů zařízení prostřednictvím aplikace Portál společnosti nebo aplikace Intune na zařízení.

5. Konfigurace **plánu**: zadejte počet dní (0 až 365) po nedodržení předpisů, které aktivují akci na zařízeních uživatelů. (*Vyřazení zařízení nesplňujících požadavky* podporuje minimálně 30 dnů.) Po uplynutí této lhůty můžete vyhovět zásadám [podmíněného přístupu](conditional-access-intune-common-ways-use.md) . Pokud zadáte **0** (nula) počet dnů, pak se podmíněný přístup projeví **okamžitě**. Pokud například zařízení nedodržuje předpisy, použijte podmíněný přístup k okamžitému blokování přístupu k e-mailu, SharePointu a dalším prostředkům organizace.

   Když vytvoříte zásady dodržování předpisů, automaticky se vytvoří akce **Označit zařízení jako nevyhovující** a automaticky se nastaví na **0** dní (hned). Když se tato akce vrátí, zařízení se vyhodnotí jako nedodržující předpisy okamžitě. Pokud se taky používá podmíněný přístup, pak se podmíněný přístup hned zahájí. Pokud chcete povolenou dobu odkladu, změňte **plán** na akci **Označit zařízení jako nevyhovující** .

   V zásadách dodržování předpisů můžete například chtít uživatele informovat. Můžete přidat akci **Odeslat e-mail pro koncového uživatele** . U této akce **Odeslat e-mail** nastavte **plán** na dva dny. Pokud je zařízení nebo koncový uživatel stále vyhodnoceno jako nedodržující předpisy, pošle se vám e-mail na dva dny. Pokud chcete uživateli poslat znovu e-mail s pěti dny nedodržení předpisů, přidejte další akci a nastavte **plán** na pět dní.

  Další informace o dodržování předpisů a integrovaných akcích najdete v tématu [Přehled dodržování předpisů](device-compliance-get-started.md).

6. Po dokončení vyberte **Přidat**  >  **OK** a uložte provedené změny.

## <a name="next-steps"></a>Další kroky

[Monitorujte své zásady](compliance-policy-monitor.md).
