---
title: Povolení konektoru Mobile Threat Defense v Microsoft Intune
titleSuffix: Microsoft Intune
description: Povolte konektor mezi vaším partnerem Mobile Threat Defense (MTD) a Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dbb6a37e-ba47-4b69-922c-d25e66c279f6
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee2d88e444941f2b75e6dcc716748c442de459a6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329147"
---
# <a name="enable-the-mobile-threat-defense-connector-in-intune"></a>Povolení konektoru Mobile Threat Defense v Intune

Při instalaci ochrany před mobilními hrozbami (MTD) jste nakonfigurovali zásadu pro klasifikaci hrozeb v konzole partnerského serveru ochrany před mobilními hrozbami a v Intune jste vytvořili zásady dodržování předpisů pro zařízení. Pokud jste už konektor Intune nakonfigurovali v konzole pro partnery MTD, můžete teď povolit připojení MTD pro partnerské aplikace MTD.

> [!NOTE]
> Toto téma se týká všech partnerů ochrany před mobilními hrozbami.

## <a name="classic-conditional-access-policies-for-mtd-apps"></a>Klasické zásady podmíněného přístupu pro aplikace MTD

Když integrujete novou aplikaci do ochrany před mobilními hrozbami Intune a povolíte připojení k Intune, vytvoří Intune v Azure Active Directory zásady klasického podmíněného přístupu. Každá aplikace MTD, kterou integrujete, včetně [ATP ATP](advanced-threat-protection.md) nebo kteréhokoli z našich dalších [partnerů MTD](mobile-threat-defense.md#mobile-threat-defense-partners), vytvoří nové zásady podmíněného přístupu v klasickém rozhraní. Tyto zásady je možné ignorovat, ale neměly by být upravované, odstraňující ani zakázané.

Pokud se klasické zásady odstraní, budete muset odstranit připojení k Intune, které bylo zodpovědné za jeho vytvoření, a pak ho nastavit znovu. Tento proces znovu vytvoří klasické zásady. Migrace klasických zásad pro aplikace MTD na nový typ zásad pro podmíněný přístup se nepodporuje.

Klasické zásady podmíněného přístupu pro aplikace MTD:

- Používají Intune MTD k tomu, aby vyžadovaly, aby byla zařízení zaregistrovaná ve službě Azure AD, aby měla ID zařízení před komunikací s partnery MTD. IDENTIFIKÁTOR je povinný, aby zařízení a mohl úspěšně ohlásit svůj stav do Intune.

- Nemusíte mít žádný vliv na žádné jiné cloudové aplikace ani prostředky.

- Liší se od zásad podmíněného přístupu, které byste mohli vytvořit, abyste mohli lépe spravovat MTD.

- Ve výchozím nastavení nekomunikujete s dalšími zásadami podmíněného přístupu, které používáte pro vyhodnocení.

Pokud chcete zobrazit klasické zásady podmíněného přístupu, přejděte v [Azure](https://portal.azure.com/#home)na **Azure Active Directory** > **podmíněný přístup** > **klasické zásady**.

## <a name="to-enable-the-mobile-threat-defense-connector"></a>Povolení konektoru ochrany před mobilními hrozbami

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost **Správa tenanta** > **konektory a tokeny** > **ochrany před mobilními hrozbami**.

3. V podokně **ochrany před mobilními hrozbami** vyberte **Přidat**.

4. Pro **Nastavení konektoru ochrany před mobilními hrozbami**vyberte řešení MTD z rozevíracího seznamu.

5. Povolte možnosti přepínání podle požadavků vaší organizace. Viditelnost možností přepínání se bude lišit v závislosti na partnerovi MTD.  Například následující obrázek znázorňuje možnosti, které jsou k dispozici pro Symantec Endpoint Protection:

   ![Nastavení konektoru MTD v Intune na portálu Azure Portal](./media/mtd-connector-enable/enable-mtd-connector-1.png)

## <a name="mobile-threat-defense-toggle-options"></a>Možnosti přepínání ochrany před mobilními hrozbami

Podle požadavků organizace se můžete rozhodnout, jaké možnosti přepínání konektoru MTD potřebujete povolit. Všechny následující možnosti nejsou podporovány všemi partnerskými servery ochrany mobilních vláken:

**Nastavení zásad dodržování předpisů MDM**

- **Připojit zařízení s Androidem verze _\<podporovaných verzích >_ , aby _\<název partnera MTD >_** : když tuto možnost povolíte, můžete nechat zařízení s Androidem 4.1 a vyšší hlásit bezpečnostní riziko zpátky do Intune.

- **Připojit zařízení s iOS verze _\<podporovaných verzích >_ na _\<MTD Partner name >_** : když tuto možnost povolíte, můžete mít zařízení s iOS 8.0 a vyšším hlášením rizika zabezpečení zpátky do Intune.

- **Povolit synchronizaci aplikací pro zařízení iOS**: Povolí tomuto partnerovi Ochrany před mobilními hrozbami žádat o metadata aplikací pro iOS z Intune, která se použijí pro účely analýzy hrozeb.

- **Blokovat nepodporované verze operačního systému**: Blokovat zařízení, pokud je na něm spuštěn operační systém nižší verze, než je minimálně podporovaná.

**Nastavení zásad ochrany aplikací**

- **Připojit zařízení s Androidem verze *\<podporovaných verzích >* na *\<MTD Partner name >* pro vyhodnocení zásad ochrany aplikací**: Pokud povolíte tuto možnost, zásady ochrany aplikací pomocí pravidla úrovně hrozby zařízení vyhodnotí zařízení, včetně dat z této spojnice.

- **Připojení zařízení s iOS verze *\<podporovaných verzích >* na *\<MTD Partner name >* pro vyhodnocení zásad ochrany aplikací**: Pokud povolíte tuto možnost, zásady ochrany aplikací pomocí pravidla úrovně hrozby zařízení vyhodnotí zařízení, včetně dat z tohoto konektoru.

Další informace o používání konektorů ochrany před mobilními hrozbami pro vyhodnocení zásad Intune App Protection najdete v tématu [nastavení ochrany před mobilními hrozbami pro neregistrovaná zařízení](mtd-enable-unenrolled-devices.md).

**Společné sdílené nastavení**

- **Počet dnů, než partner přestane reagovat**: Počet dnů nečinnosti, než bude Intune kvůli ztrátě připojení považovat partnera za nereagujícího. U nereagujících partnerů MTD Intune ignoruje stav dodržování předpisů.

> [!IMPORTANT]
> Pokud je to možné, doporučujeme přidat a přiřadit aplikace MTD ještě před tím, než vytvoříte dodržování předpisů zařízením a pravidla zásad podmíněného přístupu. To pomáhá zajistit, aby byla aplikace MTD připravená a dostupná pro koncové uživatele, aby mohli získat přístup k e-mailu nebo jiným firemním prostředkům.

> [!TIP]
> Z podokna Mobile Threat Defense se můžete podívat na **Stav připojení** a čas **poslední synchronizace** mezi Intune a partnerem MTD.

## <a name="next-steps"></a>Další kroky

- [Vytvořte zásady ochrany aplikací ochrany před mobilními hrozbami (MTD) v Intune](mtd-app-protection-policy.md).
