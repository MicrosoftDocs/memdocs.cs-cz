---
title: Nastavení kontrolního bodu SandBlast MTD
titleSuffix: Microsoft Intune
description: Přečtěte si o integraci Intune se službou Check Point SandBlast Mobile Threat Defense za účelem regulace přístupu mobilních zařízení k firemním prostředkům.
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
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: afd3f7a7c92fba23fc28903b328bc95f8555ba3d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329755"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Konektor Check Point SandBlast Mobile Threat Defense s Intune

Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí služba Check Point SandBlast Mobile, řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune. Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých běží služba Check Point SandBlast Mobile.

Zásady podmíněného přístupu můžete nakonfigurovat na základě služby Check Point SandBlast pro vyhodnocování mobilních rizik povolených prostřednictvím zásad dodržování předpisů zařízením v Intune, které můžete použít k povolení nebo blokování zařízení nesplňujících požadavky pro přístup k podnikovým prostředkům na základě zjištěných hrozeb.

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="supported-platforms"></a>Podporované platformy

- **Android 4.1 nebo novější**

- **iOS 8 nebo novější**

## <a name="pre-requisites"></a>Požadavky

- Azure Active Directory Premium

- Odběr služby Microsoft Intune

- Předplatné ochrany před mobilními hrozbami Check Point SandBlast
  - Další informace najdete na [webu služby CheckPoint SandBlast](https://www.checkpoint.com/).

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Jak pomáhají služby Intune a Check Point SandBlast Mobile chránit prostředky společnosti?

Služba Check Point Sandblast Mobile App pro Android a iOS/iPadOS zachycuje systém souborů, zásobník sítě, telemetrii zařízení a aplikací tam, kde je k dispozici, a pošle data telemetrie do cloudové služby Check Point SandBlast, aby zhodnotila riziko zařízení pro mobilní hrozby.

Zásady dodržování předpisů zařízení služby Intune zahrnují pravidlo pro ochranu před mobilními hrozbami Check Point SandBlast, která je založená na posouzení rizika službou Check Point SandBlast. Když je toto pravidlo aktivní, Intune vyhodnocuje soulad zařízení se zásadami, které jste povolili. Pokud se zjistí, že zařízení nesplňuje dané předpisy, zablokuje se přístup uživatelů k podnikovým prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé dostanou také pokyny z mobilní aplikace Check Point SandBlast nainstalované na jejich zařízeních, jak problém vyřešit a jak opět získat přístup k firemním prostředkům.

Zde jsou uvedeny některé obvyklé scénáře:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat následující:

- Připojení k firemnímu e-mailu

- Synchronizaci firemních souborů přes OneDrive for Work

- Přístup k aplikacím společnosti

*Zablokování při zjištění přítomnosti škodlivých aplikací:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD – zablokování při zjištění škodlivých aplikací](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Přístup po nápravě udělen:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD – udělení přístupu](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Zjišťuje hrozby v síti, například **útoky prostředníkem**, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.

*Blokovat přístup k síti přes Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD – zablokování přístupu k síti přes Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Přístup po nápravě udělen:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD – udělení přístupu přes Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje hrozby v síti, například **útoky prostředníkem**, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

*Zablokovat SharePoint Online, když jsou zjištěny hrozby sítě:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD – zablokování přístupu SharePointu Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Přístup po nápravě udělen:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD – udělení přístupu SharePointu Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Další kroky

- [Integrace služby CheckPoint SandBlast s Intune](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Nastavení aplikace CheckPoint SandBlast Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Vytvoření zásad dodržování předpisů pro zařízení s CheckPoint SandBlast Mobile](mtd-device-compliance-policy-create.md)

- [Povolení konektoru CheckPoint SandBlast Mobile MTD](mtd-connector-enable.md)
