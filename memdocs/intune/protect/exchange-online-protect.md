---
title: Exchange bez správy zařízení
titleSuffix: Microsoft Intune
description: Pomocí Microsoft Intune můžete zaměstnancům udělit přístup Microsoft 365 k e-mailu v Exchange Online bez nastavení systému pro správu zařízení.
keywords: Přístup k e-mailu Microsoft 365 Exchange
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/31/2017
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.technology: ''
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8491d716751a4d370003583059546f17b689657e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996125"
---
# <a name="protect-microsoft-365-exchange-online-without-requiring-device-management"></a>Ochrana Microsoft 365 Exchange Online bez nutnosti správy zařízení

Pokud chcete zaměstnancům umožnit přístup k pracovnímu e-mailu a nezabývat se přitom zavedením systému pro správu zařízení, můžete. Přístup k Microsoft 365 Exchange Online můžete udělit prostřednictvím Intune. Před provedením potřebných kroků ověřte, že máte licence na Microsoft 365 nebo Azure Active Directory (Premium) a Intune. Zaměstnanci musí mít [podporované zařízení s iOS/iPadOS nebo Androidem](../fundamentals/supported-devices-browsers.md). 

Pokud se rozhodnete zavést systém pro správu zřízení, můžete. Tento typ ochrany aplikací funguje nezávisle na správě zařízení. 

## <a name="action-plan"></a>Akční plán

1. [Přečtěte si o podmíněném přístupu](conditional-access.md). 
2. [Přečtěte si o podmíněném přístupu na základě aplikace](app-based-conditional-access-intune.md).
3. [Nastavte zásady podmíněného přístupu na základě aplikace pro Exchange Online](app-based-conditional-access-intune-create.md).
4. [Blokuje aplikace, které se nedají spravovat](app-modern-authentication-block.md), konkrétně aplikace, které neAzure Active Directory používají knihovnu MSAL Authentication Library (ADAL) nebo Microsoft Authentication Library ().
5. Volitelné [Nastavte zásady podmíněného přístupu na základě aplikace pro SharePoint Online](app-based-conditional-access-intune-create.md). Tyto zásady blokují přístup k firemním datům z aplikací, které nelze spravovat a zabezpečit. Tyto zásady také omezují přístup přes mobilní SharePoint. 

## <a name="what-to-tell-employees-and-students"></a>Co sdělit zaměstnancům a studentům

* Požádejte zaměstnance a studenty, aby si stáhli a nainstalovali Microsoft Outlook nebo Microsoft SharePoint pro iOS/iPadOS z Apple App Storu nebo pro Android z Obchod Google Play. 
* Pokud zablokujete přístup k aplikacím, které nepoužívají moderní ověřování, nezapomeňte se zaměstnancům a studentům o tomto omezení zmínit. 

## <a name="next-steps"></a>Další kroky

Pro zvýšení zabezpečení firemních dat jste použili podmíněný přístup na základě aplikace. V dalších krocích se dozvíte o jiných způsobech, jakými můžete zlepšit ochranu firemních dat, mezi které patří: 

* Nastavení [podmíněného přístupu na základě dodržování předpisů zařízením, rizik zařízení, umístění a atributů uživatele ve službě Active Directory a Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal).  
* Nastavení zásad ochrany aplikací, které pomáhají chránit firemní data před úmyslným nebo neúmyslným únikem informací 
* Využití služby Azure Information Protection k ochraně firemních dat mimo vaši síť 

Chcete pomáhat s povolením tohoto nebo jiných scénářů EMS nebo Microsoft 365? Pokud máte alespoň 150 licencí na Microsoft 365, Enterprise Mobility + Security nebo Azure Active Directory Premium, využijte [výhod služby FastTrack](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program).
