---
title: Nastavení zásad podmíněného přístupu na základě aplikace v Intune
titleSuffix: Microsoft Intune
description: Zjistěte, jak vytvořit zásadu podmíněného přístupu na základě aplikace v Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d07b87bca934dac924f2d2c281ecb7b2a2e8a2c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989796"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Nastavení zásad podmíněného přístupu na základě aplikace v Intune

Nastavte zásady podmíněného přístupu na základě aplikací pro aplikace, které jsou součástí seznamu schválených aplikací. Na seznamu schválených aplikací jsou aplikace, které testoval Microsoft.

Než budete moct používat zásady podmíněného přístupu na základě aplikace, musíte mít ve svých aplikacích použité [Zásady ochrany aplikací Intune](../apps/app-protection-policies.md) .

> [!IMPORTANT]
> Tento článek vás provede jednotlivými kroky přidání jednoduchých zásad podmíněného přístupu na základě aplikace. Stejný postup můžete použít pro jiné cloudové aplikace. Další informace najdete v tématu [Plánování nasazení podmíněného přístupu](https://docs.microsoft.com/azure/active-directory/conditional-access/plan-conditional-access) .

## <a name="create-app-based-conditional-access-policies"></a>Vytvoření zásad podmíněného přístupu na základě aplikace

Podmíněný přístup je technologie Azure Active Directory (Azure AD). Uzel podmíněného přístupu, ke kterému přistupujete z *Intune* , je stejný uzel, ke kterému přistupujete ze *služby Azure AD*. Vzhledem k tomu, že se jedná o stejný uzel, nemusíte pro konfiguraci zásad přepínat mezi Intune a Azure AD.

Než budete moct vytvořit zásady podmíněného přístupu z centra pro správu Microsoft Endpoint Manageru, musíte mít licenci Azure AD Premium.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Vytvoření zásady podmíněného přístupu na základě aplikace

1. Přihlaste se do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) .

2. Vyberte položku **Endpoint Security**  >  **podmíněný přístup**  >  **nové zásady**.

3. Zadejte **název**zásady a potom v části *přiřazení*vyberte **Uživatelé a skupiny**. Pomocí možností Zahrnout a Vyloučit vyberte požadované skupiny pro nasazení zásady a zvolte **Hotovo**.

4. Vyberte **cloudové aplikace nebo akce**a vyberte aplikace, které chcete chránit. Zvolte například **možnost vybrat aplikace**a vyberte možnost **Office 365 (Preview)**.

   Zvolením možnosti **Hotovo** uložte změny.

5. Vyberte **podmínky**,  >  které**klientské aplikace** použijí pro použití zásad pro aplikace a prohlížeče. Zvolte například **Ano** a pak povolte **Prohlížeč** a **Mobilní aplikace a desktopoví klienti**.

   Zvolením možnosti **Hotovo** uložte změny.

6. V části *řízení přístupu*vyberte **udělit** pro použití podmíněného přístupu na základě dodržování předpisů zařízením. Vyberte například **udělit přístup**  >  **vyžadovat schválenou klientskou aplikaci** a **vyžadovat zásady ochrany aplikací (Preview)** a pak vyberte **vyžadovat jeden z vybraných ovládacích prvků** .

   Zvolením možnosti **Vybrat** uložte změny.

7. V nabídce **Povolit zásadu**vyberte **zapnuto**a pak výběrem **vytvořit** uložte změny.





## <a name="next-steps"></a>Další kroky
[Blokování aplikací, které nepoužívají moderní ověřování](app-modern-authentication-block.md)

## <a name="see-also"></a>Viz také

[Ochrana dat aplikací pomocí zásad](../apps/app-protection-policies.md) 
 ochrany aplikací [Podmíněný přístup v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
