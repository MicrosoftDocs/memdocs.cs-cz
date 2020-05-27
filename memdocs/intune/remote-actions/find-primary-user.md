---
title: Najde primárního uživatele Microsoft Intune zařízení.
titleSuffix: ''
description: Najděte primárního uživatele (nebo spřažení uživatelského zařízení) zařízení Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 761f46cdf8865694ba8960044954a16c415a3eba
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988229"
---
# <a name="find-the-primary-user-of-an-intune-device"></a>Vyhledání primárního uživatele zařízení v Intune

Primární uživatel, označovaný také jako spřažení uživatelských zařízení, je vlastnost každého zařízení Intune. K zařízení Intune může být přiřazený žádný nebo jeden primární uživatel. Když není přiřazený žádný primární uživatel, zařízení se označuje jako "sdílené zařízení".

## <a name="find-a-devices-primary-user"></a>Najít primárního uživatele zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > zvolit zařízení.
3. Na stránce **Přehled** uvidíte primárního uživatele v seznamu.

## <a name="change-a-devices-primary-user"></a>Změna primárního uživatele zařízení

Primárního uživatele zařízení je možné aktualizovat pro zařízení s Windows 10, která jsou připojená k Azure AD nebo je připojená k hybridní službě Azure AD.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **všechna zařízení** > vyberte zařízení > **vlastnosti**  >  **změnit primárního uživatele**.
3. Vyberte nového uživatele a zvolte **Vybrat**.

Až se primární uživatel aktualizuje, aktualizuje se taky v okně Intune a na Azure AD Device Blade.
>[!NOTE]
>1. Aktualizace primárního uživatele napříč správcem koncových bodů a Azure AD může trvat až 10 minut, než se odrážejí.
>2. Primární uživatel se aktuálně nemůže změnit na spoluspravovaných zařízeních s Windows 10. 
>3. Změna primárního uživatele zařízení neprovede žádné změny členství v místní skupině, jako je přidání nebo odebrání uživatelů z místní skupiny Administrators.
>4. Změna primárního uživatele nemění uživatele zaregistrovaného uživatelem. 


## <a name="what-is-the-primary-user"></a>Co je primární uživatel?
Vlastnost primární uživatel slouží k mapování licencovaného uživatele Intune na jejich zařízení v nástroji:
- Aplikace Portál společnosti
- Web koncového uživatele
- Prostředí pro IT specialisty, jako jsou například stránky pro řešení potíží v Azure Portal. Tyto stránky mapují uživatelské účty na zařízení pomocí primárního uživatele. 

### <a name="company-portal-app"></a>Aplikace Portál společnosti
Aplikace Portál společnosti očekává, že uživatelský účet, který se přihlásil do Portál společnosti, je primárním uživatelem tohoto zařízení. Pokud byl k primárnímu uživateli přiřazen jiný uživatel, Portál společnosti zobrazí upozornění:

"Toto zařízení je už přiřazené někomu ve vaší organizaci. Obraťte se na firemní podporu, která se stane primárním uživatelem zařízení. Můžete dál používat Portál společnosti, ale funkce budou omezené. "

Pokud zařízení Intune nemá přiřazeného primárního uživatele, aplikace Portál společnosti ji detekuje jako sdílené zařízení. Sdílená zařízení jsou vizuálně identifikovatelná pomocí popisku "Shared", který se zobrazuje na dlaždici zařízení. V tomto režimu můžete Portál společnosti i nadále používat k vyžádání a instalaci dostupných aplikací. Akce samoobslužné služby (resetování/přejmenování/vyřazení) nejsou ale k dispozici.  

Aby se v Portál společnosti zobrazovala na sdílených zařízeních, musí být dostupné aplikace přiřazené ke skupině uživatelů. Budou nainstalovány v kontextu systému nebo v kontextu uživatele v závislosti na tom, jak byl aplikace konfigurována správcem IT. Další informace o kontextu aplikace najdete v tématu [instalace aplikací na zařízeních s Windows 10](../apps/apps-windows-10-app-deploy.md). Pro použití této funkce se vyžaduje Portál společnosti verze 10.3.4651.0 nebo novější.


## <a name="who-is-assigned-as-the-primary-user"></a>Kdo je přiřazen jako primární uživatel?
Intune automaticky přidá primárního uživatele do zařízení během nebo po registraci. Metoda registrace určuje, kdy se primární uživatel přidá do zařízení.

| Platforma | Způsob registrace | Přiřazeno primárnímu uživateli | Primární uživatel je přiřazený. |
| ---- | ---- | ---- | ---- |
| Windows | Přidat práci nebo školu (řízený uživatelem) | Registrace uživatele | Během registrace |   
| Windows | Přihlašování moderní aplikace (řízené uživatelem) | Registrace uživatele | Během registrace | 
| Windows | Registrovat jenom v MDM (řízený uživatelem) | Registrace uživatele | Během registrace | 
| Windows | Připojení ke službě Azure AD (neintegrované prostředí) | Registrace uživatele | Během registrace | 
| Windows | Připojení ke službě Azure AD (prostředí autopilot mimo box) | Registrace uživatele | Během registrace | 
| Windows | Zaregistrovat jenom v MDM | Registrace uživatele | Během registrace | 
| Windows | Objekt zásad skupiny Hybrid AADJ + automatický zápis | První uživatel, který se přihlásí k Windows | Když se první uživatel přihlásí k Windows| 
| Windows | Spoluspráva | První uživatel, který se přihlásí k Windows | Když se první uživatel přihlásí k Windows | 
| Windows | Připojení k Azure AD (token hromadného zápisu) | Žádná | Neuvedeno | 
| Windows | Připojení k Azure AD (režim automatického nasazení autopilotu) | Žádná | Neuvedeno | 
| Různé platformy | Registrace řízená uživatelem v aplikaci Portál společnosti | Registrace uživatele | Během registrace |
| Různé platformy | Správce registrace zařízení (DEM) | Registrace uživatele DEM | Během registrace |
| iOS/iPadOS, macOS | Apple automatizované registrace zařízení (DEP s přidružením uživatele) | Registrace uživatele | Během registrace |
| iOS/iPadOS, macOS | Apple automatizované registrace zařízení (DEP bez přidružení uživatele) | Žádná | Neuvedeno |
| Android | Zařízení se systémem Android, která jsou ve vlastnictví společnosti, vyhrazena | Žádná | Neuvedeno |

## <a name="primary-user-and-azure-ad-device-owner"></a>Vlastník zařízení s primárním uživatelem a Azure AD
V některých případech se primární uživatel Intune může lišit od vlastnosti **vlastníka** zařízení Azure AD (zobrazitelné v **zařízeních**  >  **Azure AD**). Vlastník zařízení Azure AD se přidá během registrace zařízení do Azure Active Directory.

## <a name="next-steps"></a>Další kroky
[Spravujte zařízení Intune.](device-management.md)
