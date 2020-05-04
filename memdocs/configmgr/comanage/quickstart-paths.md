---
title: Cesty ke spolusprávě
titleSuffix: Configuration Manager
description: Seznamte se s požadavky pro dva základní způsoby, jak můžete nastavit spolusprávu.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a670660bcf7b3f5cb8209aaf6d0b59eb0f343e4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711487"
---
# <a name="paths-to-co-management"></a>Cesty ke spolusprávě

Existují dva základní způsoby, jak můžete nastavit spolusprávu. Je důležité pochopit požadavky pro jednotlivé cesty. Každá z nich vyžaduje určitou kombinaci Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune a Windows 10. 

1. [Automatický zápis stávajících zařízení spravovaných Configuration Manager do Intune](#bkmk_path1)  
2. [Zavedení klienta Configuration Manager s moderním zřizováním](#bkmk_path2)  

![Diagram cest pro spolusprávu](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a>Cesta 1: automatický zápis stávajících klientů

Když si tuto cestu vyberete, můžete svoje stávající zařízení spravovaná Configuration Manager rychle zaregistrovat do Intune. Správa těchto zařízení od Configuration Manager se neliší od před povolením spolusprávy. Nyní získáte všechny cloudové výhody. Tato cesta je pro vaše uživatele transparentní.

Tady je seznam toho, co je potřeba nastavit:
- Hybridní služba Azure AD
    - Jedna z následujících [možností hybridní identity Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Synchronizace hodnot hash hesel](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) pomocí [bezproblémového jednotného přihlašování (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Předávací ověřování](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) pomocí [bezproblémového jednotného přihlašování (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Federované jednotné přihlašování (s Active Directory Federation Services (AD FS) (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium licence
    - Konfigurovat hybridní službu Azure AD – připojení (vyberte jednu z možností):
        - Pro spravované domény
        - Pro federované domény
- Nastavení klientského agenta pro hybridní službu Azure AD – připojení
- Konfigurace automatického zápisu zařízení do Intune
- Přiřazení uživatelských licencí Intune
- Povolit spolusprávu v Configuration Manager

Kurz k této cestě najdete v tématu [kurz: povolení spolusprávy pro stávající klienty Configuration Manager](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a>Cesta 2: zavedení s moderním zřizováním

Tady je seznam toho, co je potřeba nastavit:

1. [Nastavení rozšířeného protokolu HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Vytvoření Cloud Services v Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Konfigurace bodu správy a klientů, aby používali bránu pro správu cloudu](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Nasazení klienta Configuration Manager pomocí Intune](how-to-prepare-Win10.md)  

> [!Note]  
> Brzy se přiblíží kurz pro tuto cestu.

