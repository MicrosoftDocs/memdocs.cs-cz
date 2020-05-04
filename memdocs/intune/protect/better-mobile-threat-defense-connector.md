---
title: Konektor Better Mobile Threat Defense s Intune
titleSuffix: Intune on Azure
description: Nastavte konektor Better Mobile Threat Defense s Intune.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329907"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Konektor Better Mobile Threat Defense s Intune

Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí lépe mobilní, řešení ochrany před mobilními hrozbami (MTD), které se integruje s Microsoft Intune. Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých aplikace Better Mobile běží.

Zásady podmíněného přístupu můžete nakonfigurovat na základě lepšího posouzení mobilního rizika prostřednictvím zásad dodržování předpisů zařízení v Intune pro zaregistrovaná zařízení, která můžete použít k povolení nebo blokování zařízení nesplňujících požadavky pro přístup k podnikovým prostředkům na základě zjištěných hrozeb. U neregistrovaných zařízení můžete zásady ochrany aplikací použít k vykonání bloku nebo selektivního vymazání na základě zjištěných hrozeb.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Jak Intune a Better Mobile pomáhají chránit prostředky společnosti?

Aplikace Better Mobile je nainstalovaná a spuštěná na mobilních zařízeních. Tato aplikace zaznamenává telemetrii systému souborů, zásobníku sítě, zařízení a aplikací tam, kde je k dispozici, a posílá ji do cloudové služby Better Mobile, kde se posoudí ohrožení zařízení mobilními hrozbami.

- **Podpora zaregistrovaných zařízení** – zásady dodržování předpisů zařízením v Intune obsahují pravidlo pro ochranu před mobilními hrozbami (MTD), které může využívat informace pro posouzení rizik z lepšího mobilního nastavení. Když je povolené pravidlo MTD, Intune vyhodnotí dodržování předpisů zařízením pomocí zásad, které jste povolili. Pokud se zjistí, že zařízení nesplňuje dané předpisy, zablokuje se přístup uživatelů k podnikovým prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé dostanou také pokyny z mobilní aplikace Better Mobile nainstalované na jejich zařízeních, jak problém vyřešit a jak opět získat přístup k firemním prostředkům. Podpora použití lepšího mobilního zařízení s registrovanými zařízeními:
  - [Přidání aplikací MTD do zařízení](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Vytvoření zásady dodržování předpisů pro zařízení, které podporují MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Povolení konektoru MTD v Intune](../protect/mtd-connector-enable.md)

- **Podpora pro neregistrovaná zařízení** – Intune může při použití zásad ochrany aplikací Intune použít data posouzení rizik z lepší mobilní aplikace na nezaregistrovaných zařízeních. Správci můžou tuto kombinaci použít k ochraně podnikových dat v rámci [Microsoft Intune chráněné aplikace](../apps/apps-supported-intune-apps.md), správci můžou taky na těchto neregistrovaných zařízeních vydat blok nebo selektivní vymazání pro podniková data. Podpora použití lepšího mobilního zařízení s neregistrovanými zařízeními:
  - [Přidání aplikace MTD do neregistrovaných zařízení](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami](../protect/mtd-app-protection-policy.md)
  - [Povolení konektoru MTD v Intune pro neregistrovaná zařízení](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Podporované platformy

- **Android 4.1 nebo novější**

- **iOS 8,0 a novější**

## <a name="prerequisites"></a>Požadavky

- Azure Active Directory Premium

- Odběr služby Microsoft Intune

- Předplatné ochrany před mobilními hrozbami Better Mobile

  - Další informace najdete na [webu Better Mobile](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Ukázkové scénáře

Zde jsou uvedeny některé obvyklé scénáře.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat následující akce:

- Připojení k firemnímu e-mailu

- Synchronizaci firemních souborů přes OneDrive for Work

- Přístup k aplikacím společnosti

Zablokování při zjištění přítomnosti škodlivých aplikací:

![Obrázek zobrazující zjištěné škodlivé aplikace](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Přístup se udělí při nápravě:

![Udělení přístupu po zjištění přítomnosti škodlivých aplikací](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky **prostředníkem**, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.

Blokovat přístup k síti přes Wi-Fi:

![Zablokování přístupu k síti prostřednictvím sítě Wi-Fi](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Přístup se udělí při nápravě:

![Obrázek, který zobrazuje přístup udělený při nápravě](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky **prostředníkem**, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

Zablokovat SharePoint Online, když jsou zjištěny hrozby sítě:

![Zablokování SharePointu Online v případě zjištění ohrožení sítě](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Přístup po nápravě udělen:

![Sharepointový příklad přístupu uděleného po nápravě](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Řízení přístupu na nezaregistrovaných zařízeních na základě hrozeb ze škodlivých aplikací

Když se lepší řešení ochrany před mobilními hrozbami považuje za zařízení ![, které se má zadezinfikovat: zablokují se zjištěné malware v zásadách ochrany aplikací](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

Přístup se udělí při nápravě:

![Pro zásady ochrany aplikací se udělí přístup k nápravě.](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Další kroky

- [Integrace Better Mobile s Intune](better-mobile-mtd-connector-integration.md)

- [Nastavení aplikací Better Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Vytvoření zásad dodržování předpisů pro zařízení s Better Mobile](mtd-device-compliance-policy-create.md)

- [Povolení konektoru MTD Better Mobile](mtd-connector-enable.md)

- [Vytvoření zásady ochrany aplikací MTD](mtd-app-protection-policy.md) 
