---
title: Zabránění únikům dat na nespravovaných zařízeních
titleSuffix: Microsoft Intune
description: Pomocí Microsoft Intune můžete povolit přístup k firemním datům na zařízeních a zapnout ochranu před úniky dat.
keywords: ochrana dat zabránit úniku informací zařízení O365 Office 365
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: b1512c3a-3bbd-4111-a0df-c874a0a335df
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d694a2221dff705d6ec2c1dc1db426740d95cdbe
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329427"
---
# <a name="prevent-data-leaks-on-non-managed-devices-using-microsoft-intune"></a>Zabránění únikům dat na nespravovaných zařízeních pomocí Microsoft Intune

Pokud povolíte přístup k firemním datům hostovaným v Office 365, můžete řídit, jak je uživatelé sdílejí a ukládají, abyste předešli riziku úmyslného nebo náhodného úniku. Microsoft Intune poskytuje zásady ochrany aplikací, jejichž nastavením zabezpečíte firemní data na zařízeních vlastněných uživateli. Zařízení není třeba registrovat ve službě Intune. 

Zásady ochrany aplikací nastavené v Intune platí i pro zařízení spravovaná pomocí řešení pro správu zařízení od jiných výrobců než Microsoftu. Osobní data na zařízeních nejsou nijak dotčena – oddělení IT spravuje jenom firemní data. 

Pro ochranu firemních dat můžete nastavit zásady ochrany aplikací pro mobilní aplikace Office na zařízeních s Windows, iOS/iPadOS nebo Androidem. Tyto zásady umožňují stanovit pravidla, třeba kód PIN podle aplikace nebo šifrování firemních dat, případně pokročilejší nastavení omezující způsob použití funkcí Vyjmout, Kopírovat, Vložit a Uložit jako ze strany uživatelů mezi spravovanými a nespravovanými aplikacemi. Firemní data můžete také vzdáleně vymazat, aniž by si uživatelé museli zaregistrovat zařízení.

Zásady ochrany aplikací Intune fungují nezávisle na správě zařízení. Zásady ochrany aplikací umožňují spravovat mobilní aplikace Office na nespravovaných zařízeních i zařízeních spravovaných v Intune, jakož i na zařízeních spravovaných v řešeních MDM od jiných výrobců než Microsoftu.

## <a name="before-you-begin"></a>Před zahájením

Následující akční plán je možné provést při splnění následujících požadavků:

* Vaše společnost je připravena na zabezpečený přechod do cloudu.
* Vaše společnost používá Office 365 Exchange Online, SharePoint Online, OneDrive pro firmy nebo Yammer.
* Vaše společnost má licence na Microsoft 365, Enterprise Mobility + Security (EMS) nebo Azure Information Protection.
* Vaše společnost umožňuje uživatelům přístup k podnikovým datům ze zařízení s Windows, iOS/iPadOS nebo Androidem vlastněných společností, která jsou ve vlastnictví společnosti nebo v osobním vlastnictví.
* Vaše společnost nechce vyžadovat registraci zařízení patřících uživatelům ve službě pro správu zařízení.

## <a name="action-plan"></a>Akční plán

Pro zařízení s iOS/iPadOS a Androidem:

1. Seznamte se s tím, jak [zásady ochrany aplikací fungují](../apps/app-protection-policy.md).
2. Podívejte se, jak [vytvořit a nasadit zásady ochrany aplikací](../apps/app-protection-policies.md) pro mobilní aplikace Office.
3. [Monitorujte zásady ochrany aplikací](../apps/app-protection-policies-monitor.md), které vytváříte a nasazujete.

Pro zařízení s Windows 10:

1. Podívejte se, jak [funguje Windows Information Protection (WIP)](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip).
2. Připravte se na [konfiguraci zásad ochrany aplikací pro Windows 10](../apps/app-protection-policies-configure-windows-10.md).
3. [Vytvořte a nasaďte zásady ochrany aplikací WIP v Intune](../apps/windows-information-protection-policy-create.md).

## <a name="what-to-tell-employees-and-students"></a>Co sdělit zaměstnancům a studentům

Podle potřeby nasdílejte následující odkazy na další informace:

* [Co očekávat, když je vaše aplikace pro iOS/iPadOS spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-ios.md)
* [Co očekávat, když ke správě svojí aplikace pro Android používáte zásady ochrany aplikací](../fundamentals/end-user-mam-apps-android.md)

## <a name="next-steps"></a>Další kroky

Potřebujete pomoc s povolením této funkce nebo jiných scénářů EMS nebo Office 365? Pokud máte alespoň 150 licencí na Microsoft 365, Enterprise Mobility + Security nebo Azure Active Directory Premium, využijte [výhod služby FastTrack](https://docs.microsoft.com/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program).
