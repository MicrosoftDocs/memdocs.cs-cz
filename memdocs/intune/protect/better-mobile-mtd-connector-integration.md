---
title: Nastavení integrace Better Mobile s Intune
titleSuffix: Intune on Azure
description: Integrace konektoru Better Mobile do Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6208c8f225cc3e54a61181960223f3f8cad8423d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989742"
---
# <a name="integrate-better-mobile-with-intune"></a>Integrace Better Mobile s Intune

Při integraci řešení Better Mobile Threat Defense do Intune je potřeba provést následující kroky.

## <a name="before-you-begin"></a>Před zahájením

Následující kroky se dokončí v [lepší konzole pro správu mobilních](https://aad.bmobi.net) zařízení a umožní připojení k lepší službě Mobile Service pro zařízení zaregistrovaná v Intune (pomocí dodržování předpisů zařízením) a neregistrovaná zařízení (pomocí zásad ochrany aplikací).

Před zahájením procesu integrace řešení Better Mobile a Intune zkontrolujte, že máte následující:

- Odběr služby Microsoft Intune

- Přihlašovací údaje správce Azure Active Directory pro udělení následujících oprávnění:

  - Přihlášení a čtení profilu uživatele

  - Přístup k adresáři jako přihlášený uživatel

  - Čtení dat z adresáře

  - Odeslání informací o zařízení do Intune

- Přihlašovací údaje správce pro přístup ke konzole pro správu Better Mobile

### <a name="better-mobile-app-authorization"></a>Autorizace aplikace Better Mobile

Postup autorizace aplikace Better Mobile:

- Povolte službě Better Mobile předávání informací, které se týkají stavu zařízení, zpět do Intune.

- Better Mobile se synchronizuje s členstvím skupiny registrace Azure AD, aby se mohla naplnit databáze zařízení.

- Povolte u konzoly pro správu Better Mobile použití jednotného přihlašování (SSO) k Azure AD.

- Povolte aplikaci Better Mobile přihlášení pomocí jednotného přihlašování k Azure AD.

## <a name="to-set-up-better-mobile-integration"></a>Nastavení integrace Better Mobile

1. Přejděte ke [konzole pro správu Better Mobile](https://aad.bmobi.net) a přihlaste se pomocí svých přihlašovacích údajů.
2. Vyberte **Integration**  >  **EMM/MDM**  >  **Přidat účet**.

     ![Obrázek lepší konzoly pro správu mobilních zařízení](./media/better-mobile-mtd-connector-integration/better_mobile_console.png)

3. Vyberte **Intune**.
4. Vedle položky **NÁZEV ÚČTU** zadejte popisovač.
5. V okně **Přihlášení k Microsoftu** zadejte svoje přihlašovací údaje k Intune.
6. V okně **Požadovaná oprávnění** zvolte **Přijmout**.
7. Vyhledejte skupiny zabezpečení Azure AD Security, ze kterých má Better Mobile synchronizovat zařízení, a vyberte je v seznamu. Potom vyberte **Pokračovat**.
8. Vyberte **Done** (Hotovo).
9. Znovu se zobrazí stránka **Přidat účet**. Stránku zavřete.

## <a name="next-steps"></a>Další kroky

- [Nastavení lepších mobilních aplikací pro zaregistrovaná zařízení](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Nastavení lepších mobilních aplikací pro neregistrovaná zařízení](mtd-add-apps-unenrolled-devices.md)
