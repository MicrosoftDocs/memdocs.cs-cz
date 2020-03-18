---
title: Nastavení integrace Better Mobile s Intune
titleSuffix: Intune on Azure
description: Integrace konektoru Better Mobile do Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a509c24e4b84c1f72a5efa4f6691f69b8a309f00
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329955"
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

  - Číst data z adresáře

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
2. Zvolte **Integrace** > **EMM/MDM** > **PŘIDAT ÚČET**.

     ![Obrázek lepší konzoly pro správu mobilních zařízení](./media/better-mobile-mtd-connector-integration/better_mobile_console.png)

3. Zvolte **Intune**.
4. Vedle položky **NÁZEV ÚČTU** zadejte popisovač.
5. V okně **Přihlášení k Microsoftu** zadejte svoje přihlašovací údaje k Intune.
6. V okně **Požadovaná oprávnění** zvolte **Přijmout**.
7. Vyhledejte skupiny zabezpečení Azure AD Security, ze kterých má Better Mobile synchronizovat zařízení, a vyberte je v seznamu. Potom vyberte **Pokračovat**.
8. Vyberte **Hotovo**.
9. Znovu se zobrazí stránka **Přidat účet**. Stránku zavřete.

## <a name="next-steps"></a>Další kroky

- [Nastavení lepších mobilních aplikací pro zaregistrovaná zařízení](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Nastavení lepších mobilních aplikací pro neregistrovaná zařízení](mtd-add-apps-unenrolled-devices.md)
