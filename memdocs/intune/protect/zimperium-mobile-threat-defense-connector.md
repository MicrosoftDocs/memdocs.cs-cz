---
title: Konektor Zimperium MTD s Intune
titleSuffix: Intune on Azure
description: Přečtěte si o integraci Intune se službou Zimperium Mobile Threat Defense za účelem regulace přístupu mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b443f922b31523ec6f27971648ba1ea9c5123867
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989398"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Konektor Zimperium Mobile Threat Defense s Intune

Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí Zimperium, řešení ochrany před mobilními hrozbami (MTD), které se integruje s Microsoft Intune. Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých aplikace Zimperium běží.

Zásady podmíněného přístupu můžete nakonfigurovat na základě posouzení rizik, které je povolené, pomocí zásad dodržování předpisů zařízení v Intune pro zaregistrovaná zařízení, která můžete použít k povolení nebo blokování zařízení nesplňujících požadavky pro přístup k podnikovým prostředkům na základě zjištěných hrozeb. U neregistrovaných zařízení můžete zásady ochrany aplikací použít k vykonání bloku nebo selektivního vymazání na základě zjištěných hrozeb.

## <a name="supported-platforms"></a>Podporované platformy

- **Android 4.1 nebo novější**

- **iOS 8 nebo novější**

## <a name="prerequisites"></a>Požadavky

- Azure Active Directory Premium

- Odběr služby Microsoft Intune

- Předplatné služby Zimperium Mobile Threat Defense

  - Další informace najdete na [webu Zimperium](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Jak služby Intune a Zimperium pomáhají chránit prostředky společnosti?

Aplikace Zimperium pro Android a iOS/iPadOS zachytí telemetrii systému souborů, zásobníku sítě, zařízení a aplikací tam, kde je k dispozici, a pak pošle data telemetrie do cloudové služby Zimperium, aby zhodnotila riziko zařízení pro mobilní hrozby.

- **Podpora zaregistrovaných zařízení** – zásady dodržování předpisů zařízením v Intune obsahují pravidlo pro ochranu před mobilními hrozbami (MTD), které může používat informace o posouzení rizik z Zimperium. Když je povolené pravidlo MTD, Intune vyhodnotí dodržování předpisů zařízením pomocí zásad, které jste povolili. Pokud se zjistí, že zařízení nesplňuje dané předpisy, zablokuje se přístup uživatelů k podnikovým prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé dostanou také pokyny z mobilní aplikace Zimperium nainstalované na jejich zařízeních, jak problém vyřešit a jak opět získat přístup k firemním prostředkům. Podpora použití Zimperium s registrovanými zařízeními:
  - [Přidání aplikací MTD do zařízení](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Vytvoření zásady dodržování předpisů pro zařízení, které podporují MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Povolení konektoru MTD v Intune](../protect/mtd-connector-enable.md)

- **Podpora neregistrovaných zařízení** – Intune může při použití zásad ochrany aplikací Intune použít data posouzení rizik z aplikace Zimperium na nezaregistrovaných zařízeních. Správci můžou tuto kombinaci použít k ochraně podnikových dat v rámci [Microsoft Intune chráněné aplikace](../apps/apps-supported-intune-apps.md), správci můžou taky na těchto neregistrovaných zařízeních vydat blok nebo selektivní vymazání pro podniková data. Podpora použití Zimperium s nezaregistrovanými zařízeními:
  - [Přidání aplikace MTD do neregistrovaných zařízení](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami](../protect/mtd-app-protection-policy.md)
  - [Povolení konektoru MTD v Intune pro neregistrovaná zařízení](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Ukázkové scénáře

Níže najdete několik scénářů pro integraci řešení Zimperium s Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat následující:

- Připojení k firemnímu e-mailu

- Synchronizaci firemních souborů přes OneDrive for Work

- Přístup k aplikacím společnosti

*Zablokování při zjištění přítomnosti škodlivých aplikací:*

> [!div class="mx-imgBorder"]
> ![Zjistila se koncepční bitová kopie škodlivých aplikací.](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Přístup po nápravě udělen:*

> [!div class="mx-imgBorder"]
> ![Koncepční bitová kopie přístupu udělená po nápravě](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Zjišťuje hrozby v síti, například **útoky prostředníkem**, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.

*Blokovat přístup k síti přes Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Blokovat přístup k síti přes Wi-Fi](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Přístup po nápravě udělen:*

> [!div class="mx-imgBorder"]
> ![Přístup udělen při nápravě](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje hrozby v síti, například **útoky prostředníkem**, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

*Zablokovat SharePoint Online, když jsou zjištěny hrozby sítě:*

> [!div class="mx-imgBorder"]
> ![Zablokování SharePointu Online v případě zjištění ohrožení sítě](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Přístup po nápravě udělen:*

> [!div class="mx-imgBorder"]
> ![Sharepointový příklad přístupu uděleného po nápravě](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Řízení přístupu na nezaregistrovaných zařízeních na základě hrozeb ze škodlivých aplikací

Když řešení ochrany před mobilními hrozbami Zimperium považuje zařízení za infikované:

> [!div class="mx-imgBorder"]
> ![Blokování zásad ochrany aplikací z důvodu zjištěného malwaru](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

Přístup se udělí při nápravě:

> [!div class="mx-imgBorder"]
> ![Pro zásady ochrany aplikací se udělí přístup k nápravě.](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Další kroky

- [Integrace řešení Zimperium do Intune](zimperium-mtd-connector-integration.md)

- [Nastavení aplikací Zimperium](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Vytvoření zásad dodržování předpisů pro zařízení Zimperium](mtd-device-compliance-policy-create.md)

- [Povolení konektoru Zimperium MTD](mtd-connector-enable.md)

- [Vytvoření zásady ochrany aplikací MTD](../protect/mtd-app-protection-policy.md)
