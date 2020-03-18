---
title: Konektor Lookout MTD s Microsoft Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o integraci Intune se službou Lookout Mobile Threat Defense (MTD) za účelem regulace přístupu mobilních zařízení k firemním prostředkům.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1b3927f09bb74f9058b19dad7f2f3b72f21a0d43
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329275"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Podívejte se na mobilní koncový bod Security Connector s Intune

Přístup mobilních zařízení k firemním prostředkům můžete regulovat na základě posouzení rizik, které provádí ochrana před mobilními hrozbami Lookout integrovaná ve službě Microsoft Intune. Riziko se posuzuje na základě telemetrie, kterou ze zařízení shromažďuje služba Lookout. K ní patří:

- Ohrožení zabezpečení operačního systému
- Nainstalované škodlivé aplikace
- Škodlivé profily sítě

Zásady podmíněného přístupu můžete nakonfigurovat na základě posouzení rizik ve vyhledávání, které se povoluje v zásadách dodržování předpisů Intune pro zaregistrovaná zařízení, která můžete použít k povolení nebo blokování zařízení nesplňujících požadavky pro přístup k podnikovým prostředkům na základě zjištěných hrozeb. U neregistrovaných zařízení můžete zásady ochrany aplikací použít k vykonání bloku nebo selektivního vymazání na základě zjištěných hrozeb.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Jak Intune a Prohlédněte si Mobile Endpoint Security, jak zajistit ochranu firemních prostředků?

Mobilní aplikace pro hledání, **Prohledat práci**, je nainstalovaná a spuštěná na mobilních zařízeních. Tato aplikace zaznamenává telemetrii systému souborů, zásobníku sítě, zařízení a aplikací tam, kde je k dispozici, a posílá ji do cloudové služby Lookout, kde se posoudí ohrožení zařízení mobilními hrozbami. Klasifikace úrovní rizik pro hrozby můžete změnit v konzole Lookoutu tak, aby odpovídaly vašim požadavkům.

- **Podpora zaregistrovaných zařízení** – zásady dodržování předpisů zařízením v Intune obsahují pravidlo pro ochranu před mobilními hrozbami (MTD), které může používat informace pro posouzení rizik od hledání práce. Když je povolené pravidlo MTD, Intune vyhodnotí dodržování předpisů zařízením pomocí zásad, které jste povolili. Pokud se zjistí, že zařízení nesplňuje dané předpisy, zablokuje se přístup uživatelů k podnikovým prostředkům, jako jsou Exchange Online a SharePoint Online. Uživatelé také dostanou pokyny z aplikace pro hledání pracovních aplikací nainstalované ve svých zařízeních k vyřešení problému a opětovnému získání přístupu k podnikovým prostředkům. Podpora použití vyhledávání pro práci s registrovanými zařízeními:
  - [Přidání aplikací MTD do zařízení](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Vytvoření zásady dodržování předpisů pro zařízení, které podporují MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Povolení konektoru MTD v Intune](../protect/mtd-connector-enable.md)

- **Podpora pro neregistrovaná zařízení** – Intune může při použití zásad ochrany aplikací Intune použít data posouzení rizik z aplikace prohledat v práci na nezaregistrovaných zařízeních. Správci můžou tuto kombinaci použít k ochraně podnikových dat v rámci [Microsoft Intune chráněné aplikace](../apps/apps-supported-intune-apps.md), správci můžou taky na těchto neregistrovaných zařízeních vydat blok nebo selektivní vymazání pro podniková data. Podpora používání nástroje pro práci s nezaregistrovanými zařízeními:
  - [Přidání aplikace MTD do neregistrovaných zařízení](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami](../protect/mtd-app-protection-policy.md)
  - [Povolení konektoru MTD v Intune pro neregistrovaná zařízení](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Podporované platformy

Pro Lookout se podporují tyto platformy, pokud jsou zaregistrované v Intune:

- **Android 4.1 nebo novější**  
- **iOS 8 nebo novější**  

Další informace o podpoře platforem a jazyků najdete na webu pro [hledání](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Požadavky

- Předplatné Lookout Mobile Endpoint Security pro podniky  
- Odběr služby Microsoft Intune
- Azure Active Directory Premium
- Enterprise mobility and Security (EMS) E3 nebo E5 s licencemi přiřazenými uživatelům.  

Další informace najdete v tématu [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).

## <a name="sample-scenarios"></a>Ukázkové scénáře

Tady jsou běžné scénáře použití služby Mobile Endpoint Security s Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací

Když se na zařízeních zjistí přítomnost škodlivých aplikací (třeba malwaru), můžete jim až do vyřešení problému zablokovat toto:

- Připojení k firemnímu e-mailu
- Synchronizaci firemních souborů přes OneDrive for Work
- Přístup k aplikacím společnosti

*Zablokování při zjištění přítomnosti škodlivých aplikací:*

> [!div class="mx-imgBorder"]
> ![koncepční obrázek zásad blokující přístup z důvodu škodlivých aplikací](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Přístup udělený po nápravě:*

> [!div class="mx-imgBorder"]
> ![koncepční image ukazující přístup k zařízením po opravě](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky prostředníkem, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.

*Zablokování přístupu k síti prostřednictvím Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Obrázek znázorňující blokování přístupu Wi-Fi na základě hrozeb sítě](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Přístup udělený po nápravě:*

> [!div class="mx-imgBorder"]
> ![koncepční obrázek podmíněného přístupu umožňující přístup po opravě](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky prostředníkem, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

*Zablokování SharePointu Online v případě, že se zjistí ohrožení sítě:*

> [!div class="mx-imgBorder"]
> ![koncepční obrázek blokování přístupu k SharePointu Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Přístup udělený po nápravě:*

> [!div class="mx-imgBorder"]
> ![koncepční obrázek o povolení přístupu po vypravení hrozby sítě](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Řízení přístupu na nezaregistrovaných zařízeních na základě hrozeb ze škodlivých aplikací

Když řešení ochrany před mobilními hrozbami považuje zařízení za infikované:
> [!div class="mx-imgBorder"]
> ![bloky zásad ochrany aplikací z důvodu zjištěného malwaru](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

Přístup se udělí při nápravě:

> [!div class="mx-imgBorder"]
> k nápravě pro zásady ochrany aplikací je udělený přístup ![](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Další kroky

Tady jsou hlavní kroky, které je nutné provést při implementaci tohoto řešení:

- [Nastavení integrace služby Lookout](lookout-mtd-connector-integration.md)
- [Povolení mobilního koncového bodu zabezpečení v Intune](mtd-connector-enable.md)
- [Přidání a podepsání aplikace Lookout for Work](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Konfigurace zásad dodržování předpisů zařízení služby Lookout](mtd-device-compliance-policy-create.md)
- [Vytvoření zásady ochrany aplikací MTD](mtd-app-protection-policy.md)