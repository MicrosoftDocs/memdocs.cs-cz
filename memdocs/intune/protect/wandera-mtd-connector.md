---
title: Nastavení mobilního zabezpečení Wandera pomocí Intune
titleSuffix: Intune on Azure
description: Jak nastavit Wandera Mobile Security pomocí Microsoft Intune pro řízení přístupu mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/2/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c0911ff9250fb1b2832df4b7e269f192ee8cda
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057517"
---
# <a name="wandera-mobile-threat-defense-connector-with-intune"></a>Konektor ochrany před mobilními hrozbami Wandera s Intune  

Řízení přístupu mobilních zařízení k podnikovým prostředkům pomocí podmíněného přístupu na základě posouzení rizik, které provádí Wandera. Wandera je řešení ochrany před mobilními hrozbami (MTD), které se integruje s Microsoft Intune.  Riziko se vyhodnocuje na základě telemetrie shromážděných ze zařízení službou Wandera, včetně:
- Ohrožení zabezpečení operačního systému
- Nainstalované škodlivé aplikace
- Škodlivé profily sítě
- Cryptojacking

Můžete nakonfigurovat zásady *podmíněného přístupu* , které jsou založené na posouzení rizik v Wandera, povolené prostřednictvím zásad dodržování předpisů zařízením v Intune. Zásady hodnocení rizik můžou zařízením nesplňujících požadavky dovolit nebo blokovat přístup k podnikovým prostředkům na základě zjištěných hrozeb.  

## <a name="how-do-intune-and-wandera-mobile-threat-defense-help-protect-your-company-resources"></a>Jak ochrany před mobilními hrozbami Intune a Wandera chrání vaše firemní prostředky?  

Mobilní aplikace Wandera se bez problémů nainstaluje pomocí Microsoft Intune. Tato aplikace zachycuje systém souborů, síťový zásobník a telemetrii zařízení a aplikací (kde je dostupná). Tyto informace se synchronizují do cloudové služby Wandera a vyhodnotí riziko pro mobilní hrozby zařízení. Tyto klasifikace úrovně rizika je možné konfigurovat tak, aby vyhovovaly vašim potřebám v konzole Wandera, PAPRSKu.

Zásady dodržování předpisů v Intune obsahují pravidlo pro MTD na základě posouzení rizik Wandera. Když je toto pravidlo aktivní, Intune vyhodnocuje soulad zařízení se zásadami, které jste povolili.

U zařízení, která nedodržují předpisy, je možné zablokovat přístup k prostředkům, jako je Microsoft 365. Uživatelům blokovaných zařízení se dostanou pokyny z aplikace Wandera, aby problém vyřešili a znovu získali přístup.

Wandera aktualizuje Intune při každé změně nejnovější úrovně hrozby zařízení (Secure, nízká, střední nebo vysoká). Tato úroveň hrozby se neustále přepočítává v cloudu zabezpečení Wandera a je založená na stavu zařízení, aktivitě sítě a mnoha kanálech pro analýzu mobilních hrozeb napříč různými kategoriemi hrozeb.

Tyto kategorie a jejich přidružené úrovně hrozeb se v RADARové konzole Wandera dají konfigurovat tak, aby Celková vypočítaná úroveň hrozeb pro každé zařízení byla přizpůsobitelná podle požadavků na zabezpečení vaší organizace. S úrovní hrozeb jsou k dispozici dva typy zásad Intune, které využívají tyto informace ke správě přístupu k podnikovým datům:

* Pomocí **zásad dodržování předpisů pro zařízení** s podmíněným přístupem správci nastavují zásady tak, aby automaticky označily spravované zařízení jako "nedodržování předpisů" na základě úrovně hrozeb hlášené v Wandera. Tento příznak dodržování předpisů následně řídí zásady podmíněného přístupu, které umožňují povolit nebo odepřít přístup k aplikacím, které využívají moderní ověřování.  Podrobnosti o konfiguraci najdete v tématu [Vytvoření zásad dodržování předpisů zařízením MTD (Mobile Threat obrany)](../protect/mtd-device-compliance-policy-create.md) s Intune.

* Pomocí **zásad ochrany aplikací** s podmíněným spuštěním můžou správci nastavit zásady, které se vynutily na úrovni nativní aplikace (třeba Android a iOS/aplikace pro Android s operačním systémem, jako je Outlook, OneDrive atd.), na základě úrovně hrozeb hlášené v Wandera.  Tyto zásady se taky dají používat s nespravovanými zařízeními (MAM-WE) k zajištění jednotných zásad napříč všemi platformami a režimy zařízení. Podrobnosti o konfiguraci najdete v tématu [Vytvoření zásady ochrany aplikací pro ochranu před mobilními hrozbami](../protect/mtd-app-protection-policy.md) v Intune.

## <a name="supported-platforms"></a>Podporované platformy  

Pro Wandera se při registraci do Intune podporují tyto platformy:

- Android 5,0 a novější  
- iOS 10,2 a novější 

Další informace o platformě a zařízení najdete na [webu Wandera](https://www.wandera.com/mobile-threat-defense/).

## <a name="prerequisites"></a>Požadavky  

- Odběr služby Microsoft Intune  
- Azure Active Directory  
- Ochrana před mobilními hrozbami Wandera (dříve Wandera zabezpečená)  

Další informace najdete v tématu [Wandera Mobile Security](https://www.wandera.com/mobile-security/).
 
## <a name="sample-scenarios"></a>Ukázkové scénáře

Tady jsou běžné scénáře použití Wandera MTD s Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Řízení přístupu na základě hrozeb od škodlivých aplikací  

Když se na zařízeních zjistí škodlivá aplikace, jako je malware, můžete zařízení z běžných nástrojů blokovat, dokud nebudete moct hrozbu vyřešit. Mezi běžné bloky patří:  
- Připojení k firemnímu e-mailu  
- Synchronizaci firemních souborů přes OneDrive for Work  
- Přístup k aplikacím společnosti  

*Blokovat při zjištění škodlivých aplikací*:

![Zjistila se koncepční bitová kopie škodlivých aplikací.](./media/wandera-mtd-connector/wandera-malicious-apps-blocked.png)  

*Přístup udělen při nápravě*: 

![Koncepční bitová kopie přístupu udělená po nápravě](./media/wandera-mtd-connector/wandera-malicious-apps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Řízení přístupu na základě ohrožení sítě  

Detekuje hrozby pro vaši síť, jako jsou útoky prostředníkem, a chrání přístup k sítím Wi-Fi na základě rizika zařízení.  

*Blokovat přístup k síti přes Wi-Fi*:  

![Zablokování přístupu k síti prostřednictvím sítě Wi-Fi](./media/wandera-mtd-connector/wandera-network-wifi-blocked.png)

*Přístup udělen při nápravě*:  

![Přístup udělený po nápravě](./media/wandera-mtd-connector/wandera-network-wifi-unblocked.png)  

## <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Řízení přístupu k SharePointu Online na základě ohrožení sítě

Zjišťuje ohrožení vaší sítě, například útoky prostředníkem, a zabraňuje synchronizaci podnikových souborů na základě rizika zařízení.

*Zablokovat SharePoint Online, když jsou zjištěny hrozby sítě*:  

![Zablokování SharePointu Online v případě zjištění ohrožení sítě](./media/wandera-mtd-connector/wandera-network-spo-blocked.png)  

*Přístup udělen při nápravě*:  

![Příklad přístupu uděleného při nápravě pro SharePoint](./media/wandera-mtd-connector/wandera-network-spo-unblocked.png)  

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Řízení přístupu na nezaregistrovaných zařízeních na základě hrozeb ze škodlivých aplikací

Když řešení ochrany před mobilními hrozbami Wandera považuje zařízení za infikované:

![Blokování zásad ochrany aplikací z důvodu zjištěného malwaru](./media/wandera-mtd-connector/wandera-mobile-app-policy-block.png)

Přístup se udělí při nápravě:

![Pro zásady ochrany aplikací se udělí přístup k nápravě.](./media/wandera-mtd-connector/wandera-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Další kroky

- [Integrace Wandera s Intune](wandera-mtd-connector-integration.md)
- [Nastavení aplikací Wandera](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Vytvoření zásad dodržování předpisů pro zařízení Wandera](mtd-device-compliance-policy-create.md)
- [Povolit konektor Wandera MTD](mtd-connector-enable.md)
