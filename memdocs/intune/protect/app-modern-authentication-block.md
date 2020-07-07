---
title: Blokování aplikací bez moderního ověřování v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o aplikacích a moderních ověřováních (ADAL) pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
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
ms.openlocfilehash: bd8070dd1584beac0744ebfae63aa4fd066fa2bf
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022241"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Blokovat aplikace, které nepoužívají moderní ověřování (ADAL)

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

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
