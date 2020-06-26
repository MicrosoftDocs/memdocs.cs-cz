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
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4a8e61f30cfc21d6dfebef2315296e60dadcb7f1
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382811"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Blokovat aplikace, které nepoužívají moderní ověřování (ADAL)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Podmíněný přístup na základě aplikace se zásadami ochrany aplikací spoléhá na aplikace používající [moderní ověřování](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a), což je implementace OAuth2. Většina současných mobilních a desktopových aplikací Office používá moderní ověřování. Existují však aplikace třetích stran a starší aplikace Office, které používají jiné metody ověřování, například základní ověřování a ověřování na základě formulářů.

## <a name="block-access-to-apps"></a>Blokovat přístup k aplikacím

Pokud chcete blokovat přístup k aplikacím, které nepoužívají moderní ověřování, implementujte podmíněný přístup pomocí zásad ochrany aplikací Intune. Další informace najdete v tématu [podmíněný přístup na základě aplikace s Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Další informace

Další informace o podmíněném přístupu Azure AD najdete v následujících tématech:
- [Co je podmíněný přístup v Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Způsob fungování podmíněného přístupu na základě aplikace](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Nastavení služby SharePoint Online a Exchange Online pro Azure Active Directory podmíněný přístup](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Další kroky

- [Podmíněný přístup na základě aplikace s Intune](app-based-conditional-access-intune.md)
