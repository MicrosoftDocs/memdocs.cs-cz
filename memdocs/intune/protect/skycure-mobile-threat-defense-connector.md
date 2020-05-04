---
title: Konektor Symantec s Microsoft Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o integraci Intune se Symantec Endpoint Protection Mobile za účelem regulace přístupu mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: df4ce3f6-a093-432c-ab86-7a83865e389e
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6f8f3cf9ced5b613323093ed2baafcf65667997
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80275080"
---
# <a name="symantec-endpoint-protection-mobile-connector"></a>Konektor Symantec Endpoint Protection Mobile

Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí Symantec Endpoint Protection Mobile (SEP Mobile), což je řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune. Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých běží SEP Mobile. Patří do ní:

- Fyzická ochrana

- Síťová ochrana

- Ochrana aplikací

- Ochrana chyb zabezpečení

Pomocí zásad dodržování předpisů zařízením v Intune můžete povolit posouzení mobilního rizika SEP a pak pomocí zásad podmíněného přístupu povolit nebo blokovat přístup zařízení nedodržující předpisy k podnikovým prostředkům na základě zjištěných hrozeb.

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="supported-platforms"></a>Podporované platformy

- **Android 4.1 nebo novější**

- **iOS 8 nebo novější**

## <a name="pre-requisites"></a>Požadavky

- Azure Active Directory Premium

- Odběr služby Microsoft Intune

- Předplatné Symantec Endpoint Protection Mobile

Více informací najde na [webu Symantecu](https://help.symantec.com/cs/sep_mobile/SEPMOBILE/v131237277_v127904070/Integrating-Microsoft-Intune-with-Endpoint-Protection-Mobile?locale=EN_US).

## <a name="how-do-intune-and-sep-mobile-help-protect-your-company-resources"></a>Jak Intune a SEP Mobile pomáhají chránit prostředky společnosti?

Mobilní aplikace SEP pro Android nebo iOS/iPadOS zaznamenává telemetrii systému souborů, zásobníku sítě, zařízení a aplikací tam, kde je k dispozici, a pošle ji do cloudové služby Symantec a vyhodnotí riziko zařízení pro mobilní hrozby.

Zásady dodržování předpisů, které platí pro zařízení v Intune, zahrnují pravidlo pro SEP Mobile, které je založené na hodnocení rizik službou SEP Mobile. Když je toto pravidlo aktivní, Intune vyhodnocuje soulad zařízení se zásadami, které jste povolili.

Pokud se zjistí, že zařízení dané předpisy nedodržuje, zablokuje se přístup k prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé zablokovaných zařízení obdrží od aplikace SEP Mobile pokyny, jak problém vyřešit a jak k firemním prostředkům znovu získat přístup.

Intune podporuje dva režimy integrace s SEP Mobile:

- **Základní nastavení**: Umožňuje v režimu jen pro čtení službě SEP Mobile viditelnost zařízení v Intune.

- **Úplná integrace**: Umožňuje službě SEP Mobile nahlásit riziko zařízení a podrobnosti bezpečnostního incidentu službě Intune.

## <a name="sample-scenarios"></a>Ukázkové scénáře

Zde jsou uvedeny některé obvyklé scénáře:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat následující:

- Připojení k firemnímu e-mailu

- Synchronizaci firemních souborů přes OneDrive for Work

- Přístup k aplikacím společnosti

*Zablokování při zjištění přítomnosti škodlivých aplikací:*

![Zjistila se koncepční bitová kopie škodlivých aplikací.](./media/skycure-mobile-threat-defense-connector/symantec-arch-1.png)

*Přístup po nápravě udělen:*

![Obrázek přístupu uděleného při nápravě po zjištění škodlivých aplikací](./media/skycure-mobile-threat-defense-connector/symantec-arch-2.png)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Zjišťuje hrozby v síti, například **útoky prostředníkem**, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.

*Blokovat přístup k síti přes Wi-Fi:*

![Zablokování přístupu k síti prostřednictvím sítě Wi-Fi](./media/skycure-mobile-threat-defense-connector/symantec-arch-3.png)

*Přístup po nápravě udělen:*

![Přístup udělený po nápravě](./media/skycure-mobile-threat-defense-connector/symantec-arch-4.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje hrozby v síti, například **útoky prostředníkem**, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

*Zablokovat SharePoint Online, když jsou zjištěny hrozby sítě:*

![Zablokování SharePointu Online v případě zjištění ohrožení sítě](./media/skycure-mobile-threat-defense-connector/symantec-arch-5.png)

*Přístup po nápravě udělen:*

![Sharepointový příklad přístupu uděleného po nápravě](./media/skycure-mobile-threat-defense-connector/symantec-arch-6.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Symantec Endpoint Protection Mobile Threat Defense solution considers a device to be infected:
![App protection policy blocks due to detected malware](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Další kroky

K integraci Intune s SEP Mobile musíte dokončit tyto kroky:

- [Nastavení integrace SEP Mobile s Intune](skycure-mtd-connector-integration.md)

- [Přidání a přiřazení mobilních aplikací SEP, Microsoft Authenticator a zásad konfigurace aplikací pro iOS/iPadOS](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Vytvoření zásad dodržování předpisů pro zařízení s SEP Mobile v Intune](mtd-device-compliance-policy-create.md)

- [Povolení konektoru MTD SEP Mobile v Intune](mtd-connector-enable.md)
