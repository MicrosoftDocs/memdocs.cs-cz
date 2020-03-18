---
title: Zpráva a akce při nedodržení předpisů v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte e-mailové oznámení, které se odešle do zařízení nedodržujícího předpisy. Přidejte akce, které se provedou, když je zařízení označeno jako nedodržující předpisy. Můžete třeba přidat období odkladu, během kterého musí uživatel dodržení předpisů zajistit, nebo vytvořit plán k zablokování přístupu, dokud zařízení nebude předpisy dodržovat. Použijte k tomu Microsoft Intune v Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/08/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17a3a3b38b28eda0e4bde9c353482d0234fa3329
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330011"
---
# <a name="automate-email-and-add-actions-for-noncompliant-devices-in-intune"></a>Automatizace e-mailu a přidání akcí pro zařízení nedodržující předpisy v Intune

U zařízení, která nevyhovují zásadám nebo pravidlům dodržování předpisů, můžete přidat **Akce při nedodržení předpisů**. Tato funkce konfiguruje posloupnost akcí uspořádaných podle času, například e-mailem koncového uživatele a dalších.

## <a name="overview"></a>Přehled

Když Intune ve výchozím nastavení detekuje zařízení, které nedodržuje předpisy, okamžitě ho označí jako nedodržující předpisy. Azure Active Directory (AD) [podmíněný přístup](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) pak zařízení zablokuje. Pokud zařízení nedodržuje předpisy, **Akce při nedodržení předpisů** vám také poskytne flexibilitu při rozhodování o tom, co dělat. Zařízení třeba nemusíte okamžitě zablokovat, ale můžete dát uživateli nějaký čas na to, aby dodržení předpisů zajistil.

Existuje několik typů akcí:

- **Odeslat e-mail koncovému uživateli**: přizpůsobte si e-mailové oznámení před odesláním koncovému uživateli. Můžete přizpůsobit příjemce, předmět, a text zprávy včetně loga společnosti a kontaktních údajů.

    Kromě toho Intune v e-mailovém oznámení uvede podrobnosti o zařízení nedodržujícím předpisy.

- **Vzdáleně uzamknout zařízení, které nedodržuje předpisy**: pro zařízení, která nedodržují předpisy, můžete vydat vzdálený zámek. Uživateli se zobrazí výzva k zadání PIN kódu nebo hesla k odemknutí zařízení. Další informace o funkci [vzdáleného uzamčení](../remote-actions/device-remote-lock.md).

- **Označit zařízení jako nedodržující předpisy**: nastavte, za kolik dní má být zařízení označeno jako nedodržující předpisy. Může to být okamžitě nebo můžete dát uživateli nějaký čas na to, aby dodržení předpisů zařízením zajistil.

V tomto článku se dozvíte, jak:

- Vytvořit šablonu zprávy s oznámením
- Vytvořit akci pro případ nedodržování předpisů, například odeslat e-mail nebo vzdáleně uzamknout zařízení


## <a name="before-you-begin"></a>Před zahájením

- Abyste mohli akce při nedodržení předpisů nastavit, musíte mít aspoň jednu zásadu dodržování předpisů zařízením. Podívejte se, jak vytvořit zásady dodržování předpisů zařízeními pro tyto platformy:

  - [Androidemem](compliance-policy-create-android.md)
  - [Pracovní profily Androidu](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows](compliance-policy-create-windows.md)

- Pokud používáte zásady dodržování předpisů zařízením k blokování zařízení z firemních prostředků, musíte nastavit podmíněný přístup Azure AD. Pokyny [k použití podmíněného přístupu s Intune](conditional-access-intune-common-ways-use.md) najdete [v tématu podmíněný přístup v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) nebo běžné způsoby používání služby Intune.

## <a name="create-a-notification-message-template"></a>Vytvoření šablony zprávy s oznámením

Pokud chcete svým uživatelům odeslat e-mail, vytvořte šablonu zprávy s oznámením. Pokud zařízení nedodržuje předpisy, musíte do šablony zadat podrobnosti, které se zobrazují v e-mailu odeslaném vašim uživatelům.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **zásady dodržování předpisů** > **oznámení** > **vytvořit oznámení**.
3. V části *základy*zadejte následující informace:

   - **Název**
   - **Předmět**
   - **Zpráva**

4. V části *základy*nakonfigurujte pro oznámení následující možnosti, které jsou *povolené*pro všechny výchozí hodnoty:

   - **Záhlaví e-mailu – Připojte logo společnosti**
   - **Zápatí e-mailu – Uveďte název společnosti**
   - **Zápatí e-mailu – Uveďte kontaktní údaje**

   Logo, které nahrajete jako součást brandingu Portál společnosti, se používá pro e-mailové šablony. Další informace o značce Portálu společnosti najdete v tématu o [přizpůsobení brandingu firemní identity](../apps/company-portal-app.md#company-identity-branding-customization).

   ![Příklad oznámení o dodržování předpisů v Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Pokračujte výběrem **Další** .

5. V části **Revize + vytvořit**Zkontrolujte konfigurace a ověřte, že je šablona zprávy s oznámením připravená k použití. Vytvoření oznámení dokončíte výběrem **vytvořit** .

> [!NOTE]
> Můžete také vybrat stávající šablonu oznámení, kterou jste vytvořili dříve, a **Upravit** její informace, abyste šablonu aktualizovali.

## <a name="add-actions-for-noncompliance"></a>Přidání akcí při nedodržení předpisů

Když vytvoříte zásady dodržování předpisů pro zařízení, Intune automaticky vytvoří akci pro případ nedodržování těchto předpisů. Pokud zařízení nesplňuje vaše zásady dodržování předpisů, tato akce označí zařízení jako nevyhovující. Můžete přizpůsobit, jak dlouho bude zařízení takto označené. Tuto akci není možné odebrat.

Kromě výchozí akce označovat, že zařízení nedodržují předpisy, můžete přidat volitelné akce při vytváření zásad dodržování předpisů nebo aktualizovat existující zásady.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **zásady dodržování předpisů** > **zásady**, vyberte jednu z vašich zásad a pak vyberte **vlastnosti**.

   Ještě zásadu nemáte? Vytvořte zásadu pro [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) nebo jinou platformu.

   > [!NOTE]
   > Zařízení JAMF a zařízení nastavená pomocí skupin zařízení nemohou v současnosti přijímat akce dodržování předpisů.

3. Vyberte **Akce při nedodržení předpisů** > **Přidat**.

4. Vyberte vaši **Akci**:

   - **Odeslat e-mail koncovému uživateli**: Pokud zařízení nedodržuje předpisy, vyberte možnost odeslání e-mailu uživateli. Také:
     - Vyberte **Šablonu zprávy**, kterou jste dříve vytvořili.
     - Zadejte libovolné **Další příjemce** výběrem skupin.

   - **Vzdáleně uzamknout zařízení, které nedodržuje předpisy**: Pokud zařízení nedodržuje předpisy, uzamkněte ho. Tato akce vynutí, aby uživatel zadal kód PIN nebo heslo k odemknutí zařízení.

5. Konfigurace **plánu**: zadejte počet dní (0 až 365) po nedodržení předpisů, které aktivují akci na zařízeních uživatelů. Po uplynutí této lhůty můžete vyhovět zásadám [podmíněného přístupu](conditional-access-intune-common-ways-use.md) . Pokud zadáte **0** (nula) počet dnů, pak se podmíněný přístup projeví **okamžitě**. Pokud například zařízení nedodržuje předpisy, použijte podmíněný přístup k okamžitému blokování přístupu k e-mailu, SharePointu a dalším prostředkům organizace.

   Když vytvoříte zásady dodržování předpisů, automaticky se vytvoří akce **Označit zařízení jako nevyhovující** a automaticky se nastaví na **0** dní (hned). Když se tato akce vrátí, zařízení se vyhodnotí jako nedodržující předpisy okamžitě. Pokud se taky používá podmíněný přístup, pak se podmíněný přístup hned zahájí. Pokud chcete povolenou dobu odkladu, změňte **plán** na akci **Označit zařízení jako nevyhovující** .

   V zásadách dodržování předpisů můžete například chtít uživatele informovat. Můžete přidat akci **Odeslat e-mail pro koncového uživatele** . U této akce **Odeslat e-mail** nastavte **plán** na 2 dny. Pokud je zařízení nebo koncový uživatel stále vyhodnoceno jako nedodržující předpisy dne 2, pošle se vám e-mail na den 2. Pokud chcete uživatele poslat znovu e-mailem po 5 dnech nedodržení předpisů, přidejte další akci a nastavte **plán** na 5 dní.

   Další informace o dodržování předpisů a integrovaných akcích najdete v tématu [Přehled dodržování předpisů](device-compliance-get-started.md).

6. Po dokončení vyberte **Přidat** > **OK** k uložení změn.

## <a name="next-steps"></a>Další kroky

[Monitorujte své zásady](compliance-policy-monitor.md).
