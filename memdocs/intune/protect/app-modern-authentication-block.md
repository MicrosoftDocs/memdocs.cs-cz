---
title: Blokování aplikací bez moderního ověřování v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o aplikacích a moderních ověřováních (ADAL) pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f529a80403d27cf9d12c03c6090670095bf569fa
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329967"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Blokovat aplikace, které nepoužívají moderní ověřování (ADAL)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Podmíněný přístup na základě aplikace se zásadami ochrany aplikací spoléhá na aplikace používající [moderní ověřování](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a), což je implementace OAuth2. Většina současných mobilních a desktopových aplikací Office používá moderní ověřování. Existují však aplikace třetích stran a starší aplikace Office, které používají jiné metody ověřování, například základní ověřování a ověřování na základě formulářů.

## <a name="block-access-to-apps"></a>Blokovat přístup k aplikacím

Pokud chcete blokovat přístup k aplikacím, které nepoužívají moderní ověřování, implementujte přístup k podmínkám pomocí zásad ochrany aplikací Intune. Další informace najdete v tématu [podmíněný přístup na základě aplikace s Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Další informace

Další informace o podmíněném přístupu Azure AD najdete v následujících tématech:
- [Co je podmíněný přístup v Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Způsob fungování podmíněného přístupu na základě aplikace](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Nastavení služby SharePoint Online a Exchange Online pro Azure Active Directory podmíněný přístup](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Další kroky

- [Podmíněný přístup na základě aplikace s Intune](app-based-conditional-access-intune.md)