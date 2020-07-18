---
title: Podpora přijetí koncovými uživateli pomocí podmíněného přístupu
titleSuffix: Microsoft Intune
description: Naučte se, jak pomocí podmíněného přístupu řídit registraci v Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c2d7ce3f-fe97-4044-ad9e-25ac8fa301c9
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5eb3f743e90dc4f2769b455a981676676ab43704
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462214"
---
# <a name="drive-end-user-adoption-with-conditional-access-in-microsoft-intune"></a>Podpora přijetí koncovými uživateli pomocí podmíněného přístupu v Microsoft Intune

Povolení funkcí podmíněného přístupu v Intune, například blokování e-mailu pro neregistrovaná zařízení, může přispět k registraci a dodržování předpisů, ale není nutné, aby migrace proběhla úspěšně. Úspěch by měly určovat vaše cíle přijetí migrace a požadavky na zabezpečení.

## <a name="migration-campaign-with-conditional-access"></a>Kampaň migrace s podmíněným přístupem

Tady je typický přístup k rozšíření kampaně migrace s podmíněným přístupem:

1. Nastavte pravidla podmíněného přístupu, která se mají vyhovět pro všechny uživatele, ale konkrétně vylučte uživatele, kteří potřebují migrovat ze starého poskytovatele MDM. Můžete vytvořit skupinu uživatelů Azure AD se všemi vyloučenými uživateli podmíněného přístupu.

2. Když uživatelé migrují, odeberte je ze skupiny vyloučení podmíněného přístupu.

3. Po dokončení migrace nakonfigurujte všechny zásady podmíněného přístupu tak, aby se ve výchozím nastavení blokovaly, pokud Intune přístup nepovolí.

### <a name="advantages"></a>Výhody

- Poskytuje řízení přístupu pro nové uživatelské účty nebo uživatelské účty, které nebyly spravované předchozím řešením.

- Poskytuje uživatelům předchozího řešení období odkladu migrace.

- Minimalizuje ztrátu produktivity.

### <a name="disadvantages"></a>Nevýhody

- Uživatelé předchozího řešení můžou potenciálně přistupovat k prostředkům pomocí nespravovaných zařízení, dokud je pro tyto uživatele nepovolí podmíněný přístup.


Existuje i celá řada dalších přístupů. Můžete zvolit jednodušší proces, který odloží veškerý podmíněný přístup do doby, než se do každé fáze dokončí pokyn k registraci, nebo přísnější proces, který vynutí podmíněný přístup od začátku a vyžaduje plné dodržování předpisů pro veškerý přístup.

- Přečtěte si další informace o [podmíněném přístupu](../protect/conditional-access.md).

## <a name="task-list-for-conditional-access"></a>Seznam úkolů pro podmíněný přístup

### <a name="task-1-decide-how-you-are-going-to-implement-conditional-access"></a>Úloha 1: Rozhodněte se, jak budete podmíněný přístup implementovat.

[Běžné způsoby použití podmíněného přístupu](../protect/conditional-access-intune-common-ways-use.md)

### <a name="task-2-set-up-intune-conditional-access"></a>Úkol 2: nastavení podmíněného přístupu Intune

Zvolte jednu z následujících možností:

- [Konfigurace podmíněného přístupu v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

- [Konfigurace hybridního moderního ověřování](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview)

- [Nastavení zásad podmíněného přístupu na základě aplikace pro Exchange Online](../protect/app-based-conditional-access-intune-create.md)

- [Nastavení zásad podmíněného přístupu na základě aplikace pro SharePoint Online](../protect/app-based-conditional-access-intune-create.md)

- [Blokovat aplikace, které nepoužívají moderní ověřování (ADAL nebo MSAL)](../protect/app-modern-authentication-block.md) 

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o [typickém cyklu migrace](migration-guide-cycle.md).
