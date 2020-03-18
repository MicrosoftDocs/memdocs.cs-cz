---
title: Podmíněný přístup na základě aplikace s Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak podmíněný přístup na základě aplikace funguje s Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b399fba0-5dd4-4777-bc9b-856af038ec41
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 04a8cd4ce64b566bf2d90ef301c1be44589a53e4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329971"
---
# <a name="app-based-conditional-access-with-intune"></a>Podmíněný přístup na základě aplikace s Intune

[Zásady ochrany aplikací Intune](../apps/app-protection-policy.md) pomáhají chránit vaše firemní data na zařízeních, která jsou zaregistrovaná v Intune. Zásady ochrany aplikací můžete použít také u zařízení vlastněných zaměstnanci, která nejsou zaregistrovaná ke správě v Intune. V takovém případě potřebujete mít pořád jistotu, že jsou vaše firemní data a prostředky chráněné, i když tato zařízení vaše společnost nespravuje.

Podmíněný přístup na základě aplikace a Správa klientských aplikací přidávají vrstvu zabezpečení tím, že zajistí, že budou mít přístup k Exchangi Online a dalším službám Office 365 jenom klientské aplikace, které podporují zásady ochrany aplikací Intune.

> [!NOTE]
> Spravovaná aplikace je taková aplikace, která využívá zásady ochrany aplikací a která lze spravovat pomocí Intune.

Pokud povolíte přístup k Exchangi Online jenom aplikaci Microsoft Outlook, můžete zablokovat integrované e-mailové aplikace v iOS/iPadOS a Androidu. Kromě toho můžete u aplikací, které nepoužívají zásady ochrany aplikací Intune, blokovat přístup k SharePointu Online.

## <a name="prerequisites"></a>Požadavky

Před vytvořením zásad podmíněného přístupu na základě aplikace musíte mít:

- **Řešení Enterprise Mobility + Security (EMS)** nebo **předplatné Azure Active Directory (AD) Premium**
- Uživatelé musí mít licenci pro EMS nebo Azure AD.

Další informace najdete v tématu [ceny pro Enterprise mobility](https://www.microsoft.com/cloud-platform/enterprise-mobility-pricing) nebo [ceny Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="supported-apps"></a>Podporované aplikace

Seznam aplikací, které podporují podmíněný přístup na základě aplikace, najdete v [dokumentaci technické Reference k podmíněnému přístupu Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference)

Podmíněný přístup na základě aplikace [podporuje také obchodní aplikace (LOB)](app-modern-authentication-block.md), ale tyto aplikace potřebují používat [moderní ověřování Office 365](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a). 

## <a name="how-app-based-conditional-access-works"></a>Způsob fungování podmíněného přístupu na základě aplikace

V tomto příkladu správce použil zásady ochrany aplikací pro Outlookovou aplikaci a pravidlo podmíněného přístupu, které přidá aplikaci Outlook do seznamu schválených aplikací, které se dají použít při přístupu k podnikovému e-mailu.

> [!NOTE]
> Následující vývojový diagram lze použít pro jiné spravované aplikace.

![Proces podmíněného přístupu na základě aplikace znázorněný v diagramu toku](./media/app-based-conditional-access-intune/ca-intune-common-ways-3.png)

1. Uživatel se pokusí ověřit ve službě Azure AD z aplikace Outlook.

2. Při prvním pokusu o ověření je uživatel přesměrován do obchodu s aplikacemi, odkud si má nainstalovat zprostředkující aplikaci. Zprostředkující aplikací může být buď Microsoft Authenticator pro zařízení s iOSem, nebo Portál společnosti Microsoft pro zařízení s Androidem.

   Pokud se uživatelé pokusí použít nativní e-mailovou aplikaci, budou přesměrováni do obchodu s aplikacemi, aby si nainstalovali Outlook.

3. Zprostředkující aplikace se nainstaluje na zařízení.

4. Aplikace zprostředkovatele spustí proces registrace Azure AD, který vytvoří záznam zařízení ve službě Azure AD. To není stejné jako u procesu registrace správy mobilních zařízení (MDM), ale tento záznam je nutný, aby bylo možné na zařízení vyhovět zásadám podmíněného přístupu.

5. Zprostředkující aplikace ověří identitu aplikace. K dispozici je vrstva zabezpečení, aby aplikace zprostředkovatele mohla ověřit, jestli je aplikace autorizována pro použití uživatelem.

6. Zprostředkující aplikace odešle v rámci ověřování uživatele ID klienta aplikace do Azure AD, aby zkontrolovala, že je v seznamu schválených zásad.

7. Azure AD umožní ověření uživatele a použití aplikace na základě seznamu schválených zásad. Pokud aplikace není v seznamu, služba Azure AD odepře přístup k aplikaci.

8. Aplikace Outlook komunikuje s cloudovou službou Outlooku a iniciuje tak komunikaci s Exchangem Online.

9. Cloudová služba Outlooku komunikuje s Azure AD, aby pro uživatele načetla přístupový token služby Exchange Online.

10. Aplikace Outlook komunikuje s Exchangem Online, aby načetla firemní e-mail uživatele.

11. Firemní e-mail se doručí do uživatelovy poštovní schránky.

## <a name="next-steps"></a>Další kroky
[Vytvoření zásady podmíněného přístupu na základě aplikace](app-based-conditional-access-intune-create.md)

[Blokování aplikací, které nepoužívají moderní ověřování](app-modern-authentication-block.md)
