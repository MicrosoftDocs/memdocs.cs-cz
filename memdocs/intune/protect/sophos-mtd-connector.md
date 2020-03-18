---
title: Použití programu Sophos Mobile s Intune
titleSuffix: Intune on Azure
description: Jak používat mobilní řešení Sophos s Microsoft Intune k řízení přístupu mobilních zařízení k firemním prostředkům.
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
ms.openlocfilehash: d40d290fbe07ab4d1f0cf66761b0c78867cf5677
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325219"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Nastavení konektoru ochrany před mobilními hrozbami v Intune

Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí společnost Sophos Mobile, řešení ochrany před mobilními hrozbami (MTD), které se integruje s Microsoft Intune. Riziko se vyhodnocuje na základě telemetrie shromážděných ze zařízení s mobilní aplikací Sophos.
Na základě zásad dodržování předpisů zařízením v Intune můžete nakonfigurovat zásady podmíněného přístupu, které jsou založené na nástroji Sophos Mobile Threat Assessment, které můžete použít k povolení nebo blokování zařízení nesplňujících požadavky pro přístup k podnikovým prostředkům na základě zjištěných hrozeb.

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="supported-platforms"></a>Podporované platformy

- Android 5,0 a novější
- iOS 11,0 a novější

## <a name="prerequisites"></a>Požadavky

- Azure Active Directory Premium
- Odběr služby Microsoft Intune
- Předplatné ochrany před mobilními hrozbami v Sophos

Další informace najdete na [webu Sophos](https://www.sophos.com/products/mobile-control.aspx).

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>Jak Intune a Sophos Mobile chrání firemní prostředky?

Mobilní aplikace Sophos pro Android a iOS/iPadOS zaznamenává systém souborů, zásobník sítě, zařízení a telemetrii aplikací tam, kde je k dispozici, a poté odesílá data telemetrie do mobilní cloudové služby Sophos, aby zhodnotila riziko zařízení pro mobilní hrozby.

Zásady dodržování předpisů pro zařízení v Intune obsahují pravidlo pro ochranu před mobilními hrozbami, které je založené na posouzení rizikového mobilního rizika pro Sophos. Když je toto pravidlo aktivní, Intune vyhodnocuje soulad zařízení se zásadami, které jste povolili. Pokud se zjistí, že zařízení nesplňuje dané předpisy, zablokuje se přístup uživatelů k podnikovým prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé také dostanou pokyny z mobilní aplikace Sophos nainstalované ve svých zařízeních k vyřešení problému a opětovnému získání přístupu k podnikovým prostředkům.  

## <a name="sample-scenarios"></a>Ukázkové scénáře

Zde jsou uvedeny některé obvyklé scénáře.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat následující akce:

- Připojení k firemnímu e-mailu
- Synchronizaci firemních souborů přes OneDrive for Work
- Přístup k aplikacím společnosti

*Blokovat při zjištění škodlivých aplikací*:

![Zjistila se koncepční bitová kopie škodlivých aplikací.](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*Přístup udělen při nápravě*:  
![koncepční bitovou kopii přístupu uděleného po opravě](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Detekuje hrozby pro vaši síť, jako jsou útoky prostředníkem, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.  

*Blokovat přístup k síti přes Wi-Fi*:  
![blokovat přístup k síti přes Wi-Fi](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*Přístup udělen při nápravě*:   
![přístup udělen při nápravě](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Detekuje hrozby pro vaši síť, jako jsou útoky prostředníkem, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.  

*Zablokovat SharePoint Online, když jsou zjištěny hrozby sítě*:

![Zablokování SharePointu Online v případě zjištění ohrožení sítě](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*Přístup udělen při nápravě*:

![Sharepointový příklad přístupu uděleného po nápravě](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Další kroky

- [Integrace Sophos s Intune](sophos-mtd-connector-integration.md)
- [Nastavení aplikací Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Vytvořit zásady dodržování předpisů zařízením Sophos](mtd-device-compliance-policy-create.md)
- [Povolit konektor Sophos MTD](mtd-connector-enable.md)
