---
title: Konektor Pradeo Mobile Threat Defense s Intune
titleSuffix: Intune on Azure
description: Naučte se integrovat Intune s konektorem ochrany před mobilními hrozbami Pradeo k řízení přístupu mobilních zařízení k firemním prostředkům.
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
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a23155c31586992c82781998bb664bf2ce6a0889
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325351"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Konektor Pradeo Mobile Threat Defense s Intune

Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí Pradeo, řešení ochrany před mobilními hrozbami (MTD), které se integruje s Microsoft Intune. Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých aplikace Pradeo běží.

Zásady podmíněného přístupu můžete nakonfigurovat na základě posouzení rizik Pradeo povoleného prostřednictvím zásad dodržování předpisů zařízením Intune, které můžete použít k povolení nebo blokování zařízení nesplňujících požadavky pro přístup k podnikovým prostředkům na základě zjištěných hrozeb.

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="supported-platforms"></a>Podporované platformy

- **Android 4.0.3 nebo novější**

- **iOS 7 nebo novější**

## <a name="prerequisites"></a>Požadavky

- Azure Active Directory Premium

- Odběr služby Microsoft Intune

- Předplatné služby Pradeo Security for Mobile Threat Defense

  - Další informace naleznete na [webu Pradeo](https://www.pradeo.com/en-US/mobile-threat-protection).

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Jak služby Intune a Pradeo pomáhají chránit prostředky společnosti?

Aplikace Pradeo pro Android a iOS/iPadOS zaznamenává telemetrii systému souborů, zásobníku sítě, zařízení a aplikací tam, kde je k dispozici, a poté odesílá data telemetrie do cloudové služby Pradeo, aby zhodnotila riziko zařízení pro mobilní hrozby.

Zásady dodržování předpisů, které platí pro zařízení v Intune, zahrnují pravidlo pro službu ochrany před mobilními hrozbami Pradeo. Toto pravidlo je založené na hodnocení rizika službou Pradeo. Když je toto pravidlo aktivní, Intune vyhodnocuje soulad zařízení se zásadami, které jste povolili. Pokud se zjistí, že zařízení nesplňuje dané předpisy, zablokuje se přístup uživatelů k podnikovým prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé dostanou také pokyny z mobilní aplikace Pradeo nainstalované na jejich zařízeních, jak problém vyřešit a jak opět získat přístup k firemním prostředkům.

## <a name="sample-scenarios"></a>Ukázkové scénáře

Zde jsou uvedeny některé obvyklé scénáře.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat následující akce:

- Připojení k firemnímu e-mailu

- Synchronizaci firemních souborů přes OneDrive for Work

- Přístup k aplikacím společnosti

*Zablokování při zjištění přítomnosti škodlivých aplikací:*

![Zjistila se koncepční bitová kopie škodlivých aplikací.](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Přístup udělený po nápravě:*

![Udělení přístupu po zjištění přítomnosti škodlivých aplikací](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky **prostředníkem**, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.

*Zablokování přístupu k síti prostřednictvím sítě Wi-Fi:*

![Zablokování přístupu k síti prostřednictvím sítě Wi-Fi](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Přístup udělený po nápravě:*

![Koncepční bitová kopie přístupu udělená při nápravě](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky **prostředníkem**, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

*Zablokování SharePointu Online v případě, že se zjistí ohrožení sítě:*

![Zablokování SharePointu Online v případě zjištění ohrožení sítě](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Přístup udělený po nápravě:*

![Koncepční bitová kopie přístupu uděleného při nápravě pro SharePoint – příklad](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Další kroky

- [Integrace služby Pradeo s Intune](pradeo-mtd-connector-integration.md)

- [Nastavení aplikací Pradeo](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Vytvoření zásady dodržování předpisů zařízení služby Pradeo](mtd-device-compliance-policy-create.md)

- [Povolení konektoru Pradeo MTD](mtd-connector-enable.md)
