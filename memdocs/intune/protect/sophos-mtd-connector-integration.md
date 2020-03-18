---
title: Nastavení integrace s integrací na mobilní zařízení s Intune
titleSuffix: Intune on Azure
description: Jak nastavit mobilní řešení Sophos pomocí Microsoft Intune pro řízení přístupu mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 06747035f2d04be01dad12a9c89b712a4baae6b4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325239"
---
# <a name="integrate-sophos-mobile-with-intune"></a>Integrace Sophos Mobile s Intune  

Provedením následujících kroků Integrujte řešení ochrany před mobilními hrozbami s Intune.  

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="before-you-begin"></a>Před zahájením  

Před zahájením procesu integrace služby Sophos Mobile s Intune se ujistěte, že máte následující:  
- Odběr služby Microsoft Intune  
- Přihlašovací údaje správce Azure Active Directory pro udělení následujících oprávnění:  
  - Přihlášení a čtení profilu uživatele  
  - Přístup k adresáři jako přihlášený uživatel  
  - Číst data z adresáře  
  - Odeslání informací o zařízení do Intune  
- Přihlašovací údaje správce pro přístup k konzole Sophos Mobile admin.  


### <a name="sophos-mobile-app-authorization"></a>Sophos Authorization mobilní aplikace  
  
Postup autorizace mobilní aplikace Sophos je následující:  
- Umožněte, aby mobilní služba Sophos komunikovala informace týkající se stavu zařízení zpátky do Intune.  
- Díky členství ve skupině registrací ve službě Azure AD můžete mobilní zařízení naplnit do své databáze.  
- Umožněte, aby konzola pro správu mobilních zařízení mohla používat jednotné přihlašování (SSO) Azure AD.  
- Umožněte, aby se mobilní aplikace Sophos přihlásila pomocí jednotného přihlašování služby Azure AD.  


## <a name="to-set-up-sophos-mobile-integration"></a>Nastavení integrace s Sophos Mobile  

1. Přihlaste se k [Azure Portal]( https://portal.azure.com/), **v Intune** > **dodržování předpisů zařízením** > **ochrany před mobilními hrozbami** > a vyberte **Přidat**.  
2. Na stránce **Přidat konektor** použijte rozevírací seznam a vyberte možnost **Sophos**. A pak vyberte **vytvořit**.  
3. Vyberte odkaz a *otevřete konzolu pro správu Sophos*.  
4. Přihlaste se ke [konzole pro správu Sophos](https://central.sophos.com/) pomocí vašich přihlašovacích údajů Sophos.  
5. Přejít na **Nastavení** **mobilního** ** >  > nastavení** > **Sophos Setup**.  
6. Na stránce s **instalačním programem Sophos** vyberte kartu **Intune MTD** .  
   ![Sophos Setup](./media/sophos-mtd-connector-integration/sophos-setup.png) 
 
7. Vyberte **BIND (vazba**) a pak vyberte **Ano**. Sophos se připojí k Intune a vyžaduje, abyste se přihlásili k předplatnému Intune. 
8. V okně Microsoft Intune ověřování zadejte svoje přihlašovací údaje Intune a **přijměte** žádost o oprávnění pro *ochranu před mobilními vlákny*pro uživatele Sophos.  
   ![ověřování Intune](./media/sophos-mtd-connector-integration/intune-authentication.png)

9. Na stránce s **instalačním programem Sophos** vyberte **Save (Uložit** ) a dokončete konfiguraci pro Intune:  
   ![Uložit nastavení Sophos](./media/sophos-mtd-connector-integration/save-sophos-configuration.png)  

1. Jakmile se objeví zpráva **Successful Integration** (integrace proběhla úspěšně), je integrace hotová.  
1. V konzole Intune je teď k dispozici software Sophos.  


## <a name="next-steps"></a>Další kroky  
[Konfigurace klientských aplikací Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
