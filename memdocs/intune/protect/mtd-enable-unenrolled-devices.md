---
title: Povolení konektoru ochrany před mobilními hrozbami pro neregistrovaná zařízení
titleSuffix: Microsoft Intune
description: Povolte pro neregistrovaná zařízení konektor ochrany před mobilními hrozbami v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5862793180efa2184f620920aad7decf3935e1ae
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80322434"
---
# <a name="enable-the-mobile-threat-defense-connector-in-intune-for-unenrolled-devices"></a>Povolení konektoru ochrany před mobilními hrozbami v Intune pro neregistrovaná zařízení

Při instalaci ochrany před mobilními hrozbami (MTD) jste nakonfigurovali zásadu pro klasifikaci hrozeb v konzole partnerského serveru ochrany před mobilními hrozbami a v Intune jste vytvořili zásady ochrany aplikací. Pokud jste už konektor Intune nakonfigurovali v konzole pro partnery MTD, můžete teď povolit připojení MTD pro partnerské aplikace MTD.

> [!NOTE]
> Tento článek se týká všech partnerů ochrany před mobilními hrozbami, které podporují zásady ochrany aplikací:
>
> - Lepší mobilní zařízení (Android, iOS/iPadOS)
> - Zimperium (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS)

## <a name="classic-conditional-access-policies-for-mtd-apps"></a>Klasické zásady podmíněného přístupu pro aplikace MTD

Když integrujete novou aplikaci do ochrany před mobilními hrozbami Intune a povolíte připojení k Intune, vytvoří Intune v Azure Active Directory zásady klasického podmíněného přístupu. Každá aplikace MTD, kterou integrujete, včetně [ATP ATP](advanced-threat-protection.md) nebo kteréhokoli z našich dalších [partnerů MTD](mobile-threat-defense.md#mobile-threat-defense-partners), vytvoří nové zásady podmíněného přístupu v klasickém rozhraní. Tyto zásady je možné ignorovat, ale neměly by být upravované, odstraňující ani zakázané.

Pokud se klasické zásady odstraní, budete muset odstranit připojení k Intune, které bylo zodpovědné za jeho vytvoření, a pak ho nastavit znovu. Tento proces znovu vytvoří klasické zásady. Migrace klasických zásad pro aplikace MTD na nový typ zásad pro podmíněný přístup se nepodporuje.

Klasické zásady podmíněného přístupu pro aplikace MTD:

- Používají Intune MTD k tomu, aby vyžadovaly, aby byla zařízení zaregistrovaná ve službě Azure AD, aby měla ID zařízení před komunikací s partnery MTD. IDENTIFIKÁTOR je povinný, aby zařízení a mohl úspěšně ohlásit svůj stav do Intune.

- Nemusíte mít žádný vliv na žádné jiné cloudové aplikace ani prostředky.

- Liší se od zásad podmíněného přístupu, které byste mohli vytvořit, abyste mohli lépe spravovat MTD.

- Ve výchozím nastavení nekomunikujete s dalšími zásadami podmíněného přístupu, které používáte pro vyhodnocení.

Pokud chcete zobrazit klasické zásady podmíněného přístupu, přejděte v [Azure](https://portal.azure.com/#home)na **Azure Active Directory** > **klasické zásady****podmíněného přístupu** > .

## <a name="to-enable-the-mtd-connector"></a>Povolení konektoru MTD

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost**konektory** >  **pro správu** > tenanta a**ochranu před mobilními hrozbami**.

3. V podokně **Mobile Threat Defense** zvolte **Přidat**.

4. V rozevíracím seznamu **Vyberte konektor Mobile Threat Defense, který chcete nastavit** vyberte své řešení MTD.

    <!-- ![MTD setup in Intune](PLACEHOLDER, need a new screenshot of this page) -->

5. Povolte možnosti přepínání podle požadavků vaší organizace. Viditelnost možností přepínání se bude lišit v závislosti na partnerovi MTD.

## <a name="mobile-threat-defense-toggle-options"></a>Možnosti přepínání ochrany před mobilními hrozbami

Podle požadavků organizace se můžete rozhodnout, jaké možnosti přepínání konektoru MTD potřebujete povolit. Tady jsou další podrobnosti:

**Nastavení zásad ochrany aplikací**

- **Připojit zařízení s Androidem verze 4,4 a novější pro * \<MTD partnerský název>* pro vyhodnocení zásad ochrany aplikací**: když tuto možnost povolíte, zásady ochrany aplikací pomocí pravidla úrovně hrozby zařízení vyhodnotí zařízení, včetně dat z tohoto konektoru.

- **Připojení zařízení s iOS verze 11 a novější k * \<MTD partner Name>* pro vyhodnocení zásad ochrany aplikací**: Pokud povolíte tuto možnost, zásady ochrany aplikací pomocí pravidla úrovně hrozby zařízení vyhodnotí zařízení, včetně dat z této spojnice.

**Společné sdílené nastavení**

- **Počet dnů, než partner přestane reagovat**: Počet dnů nečinnosti, než bude Intune kvůli ztrátě připojení považovat partnera za nereagujícího. U nereagujících partnerů MTD Intune ignoruje stav dodržování předpisů.

> [!TIP]
> Z podokna Mobile Threat Defense se můžete podívat na **Stav připojení** a čas **poslední synchronizace** mezi Intune a partnerem MTD.

## <a name="next-steps"></a>Další kroky

- [Vytvořte zásady ochrany aplikací ochrany před mobilními hrozbami (MTD) v Intune](mtd-app-protection-policy.md).
