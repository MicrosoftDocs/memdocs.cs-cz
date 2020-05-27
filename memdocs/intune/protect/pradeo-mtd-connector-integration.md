---
title: Nastavení integrace služby Pradeo s Intune
titleSuffix: Intune on Azure
description: Integrace konektoru Pradeo do Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 82872ba6-80f8-4cc9-adf4-0ccd8ff26dd2
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fb2317474b49dcb4bb39a0590c8ad7fa4ac8aa4
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984878"
---
# <a name="integrate-pradeo-mobile-threat-defense-with-intune"></a>Integrace ochrany před mobilními hrozbami Pradeo pomocí Intune

Při integraci řešení Pradeo Mobile Threat Defense do Intune je potřeba provést následující kroky.

> [!NOTE]  
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="before-you-begin"></a>Před zahájením

> [!NOTE]
> Následující kroky je potřeba provést v [konzole Pradeo Security](https://pradeo-security.com/).

Před zahájením procesu integrace řešení Pradeo a Intune zkontrolujte, že máte následující:

- Odběr služby Microsoft Intune

- Přihlašovací údaje správce Azure Active Directory pro udělení následujících oprávnění:

  - Přihlášení a čtení profilu uživatele

  - Přístup k adresáři jako přihlášený uživatel

  - Čtení dat z adresáře

  - Odeslání informací o zařízení do Intune

- Přihlašovací údaje správce pro přístup ke konzole Pradeo Security

### <a name="pradeo-app-authorization"></a>Autorizace aplikace Pradeo Security

Postup autorizace aplikace Pradeo:

- Povolte službě Pradeo předávání informací, které se týkají stavu zařízení, zpět do Intune.

- Pradeo se synchronizuje s členstvím skupiny registrace Azure AD, aby se naplnila databáze zařízení.

- Povolte u konzoly pro správu Pradeo použití jednotného přihlašování (SSO) k Azure AD.

- Povolte aplikaci Pradeo přihlášení pomocí jednotného přihlašování k Azure AD.

## <a name="to-set-up-pradeo-integration"></a>Nastavení integrace služby Pradeo

1. Přejděte do [konzoly Pradeo Security](https://www.pradeo-security.com) a přihlaste se pomocí přihlašovacích údajů.

2. Z nabídky vyberte **Administration – Enterprise Mobility Management**.

3. Vyberte **logo Intune**.

4. V okně **EMM (Enterprise mobility management) – Intune** vyberte v části **Step 1** (Krok 1) tlačítko **Pradeo Connector** (konektor Pradeo). 

    ![Snímek obrazovky okna Intune Pradeo EMM](./media/pradeo-mtd-connector-integration/pradeo_setup.png)

5. Do okna pro připojení Microsoft Intune zadejte přihlašovací údaje Intune.

5. Otevře se webová stránka Pradeo. V části **Step 2** (Krok 2) vyberte tlačítko **Pradeo Device Health** (Stav zařízení Pradeo).

7. V okně Pradeo-Intune Connector vyberte **Accept** (Přijmout). 

8. V okně Pradeo device API connector (konektor rozhraní API zařízení Pradeo) vyberte **Accept** (Přijmout).

9. Otevře se webová stránka Pradeo. V části **Step 3** (Krok 3) vyberte tlačítko **Connect to Microsoft** (připojit k Microsoftu). 

10. Do okna pro ověřování Microsoft Intune zadejte přihlašovací údaje Intune.

11. Jakmile se objeví zpráva **Successful Integration** (integrace proběhla úspěšně), je integrace hotová.

## <a name="next-steps"></a>Další kroky

- [Nastavení aplikací Pradeo pro zaregistrovaná zařízení](mtd-apps-ios-app-configuration-policy-add-assign.md)
