---
title: Integrace kontrolního bodu SandBlast MTD
titleSuffix: Microsoft Intune
description: Jak nastavit Check Point SandBlast Mobile Threat Defense (MTD) s Intune za účelem regulace přístupu mobilních zařízení k firemním prostředkům.
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
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a02880f6da2e8a7810a37658bd19736b4631a9f8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989227"
---
# <a name="integrate-check-point-sandblast-mobile-with-intune"></a>Integrace Check Point SandBlast Mobile a Intune

Provedením následujících kroků Integrujte řešení ochrany před mobilními hrozbami Check Point SandBlast do Intune.

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="before-you-begin"></a>Před zahájením

Pokyny v tomto článku se provádějí v [konzole Check Point SandBlast Mobile](https://intune-4.eu1.locsec.net/). 

Před zahájením procesu integrace Check Point SandBlast Mobile a Intune zkontrolujte, že máte následující:

- Odběr služby Microsoft Intune

- Přihlašovací údaje správce Azure Active Directory pro udělení následujících oprávnění:

  - Přihlášení a čtení profilu uživatele

  - Přístup k adresáři jako přihlášený uživatel

  - Čtení dat z adresáře

  - Odeslání informací o zařízení do Intune

- Přihlašovací údaje správce pro přístup ke konzole Check Point SandBlast Mobile MTD

### <a name="check-point-sandblast-app-authorization"></a>Autorizace aplikace Check Point SandBlast

Proces autorizace aplikace Check Point SandBlast:

- Povolte službě Check Point SandBlast Mobile předávání informací týkajících se stavu zařízení zpět do Intune.

- Kontrolní bod SandBlast mobilní synchronizace se synchronizuje s členstvím skupiny registrace Azure AD, aby se naplnila databáze zařízení.

- Povolte u konzoly pro správu Check Point SandBlast použití jednotného přihlašování (SSO) k Azure AD.

- Povolte aplikaci Check Point SandBlast Mobile přihlášení pomocí jednotného přihlašování k Azure AD.

## <a name="to-set-up-check-point-sandblast-mobile-integration"></a>Nastavení integrace Check Point SandBlast Mobile

1. Přejděte do [konzoly Check Point SandBlast Mobile MTD](https://intune-4.eu1.locsec.net/) a přihlaste se pomocí přihlašovacích údajů.

2. Klikněte na kartu **Settings** (Nastavení).

3. Zvolte **Device management** (Správa zařízení) a pak **Settings**.

4. V rozevíracím seznamu **MDM Service** zvolte **Microsoft Intune**.

5. Jakmile nastavíte Microsoft Intune jako službu MDM, okno **konfigurace Microsoft Intune** se zobrazí, vyberte možnost **Přidat do mojí organizace** pro každou platformu zařízení: iOS/IPadOS, Android a Windows pro autorizaci kontrolního bodu SandBlast Mobile ke komunikaci s Intune a Azure AD.

    ![Obrázek znázorňující konfiguraci Check Point MTD v Intune](./media/checkpoint-sandblast-mobile-mtd-connector-integration/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > Aby bylo možné pokračovat k dalšímu kroku, je nutné přidat platformy všech zařízení.

6. Zvolte **Accept** (Přijmout) a autorizujte tak aplikaci Check Point SandBlast Mobile pro komunikaci s Intune a Azure Active Directory.

7. Po povolení všech platforem zařízení je nutné zadat skupinu zabezpečení Azure AD.

8. Zvolte **Verify** (Ověřit) a po úspěšném ověření skupiny zabezpečení zvolte **Save** (Uložit).

## <a name="next-steps"></a>Další kroky

- [Nastavení aplikací Check Point SandBlast Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)
