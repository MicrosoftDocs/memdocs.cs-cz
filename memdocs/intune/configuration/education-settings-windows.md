---
title: Nastavení vzdělávání pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení vzdělávání pro zařízení s Windows 10. Tato nastavení použijte v profilu konfigurace zařízení pomocí aplikace vzít si test, vyberte, jak se uživatelé nebo studenti přihlásí, monitorovat obrazovku během testu a další v Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 551f0a442f81712cff29a9ff6f55c62aeaba547a
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078188"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Konfigurace aplikace pořizovat test na zařízeních s Windows 10 pomocí Intune

Aplikace převzít test vám umožní bezpečně spravovat online testy na zařízeních s Windows 10 vaší učebnou. Pokud chcete nastavit aplikaci pořizovat test, budete muset vytvořit profil konfigurace zařízení v Intune a nakonfigurovat nastavení zabezpečení pro vyhodnocení. Tento článek popisuje nastavení, která najdete pro aplikaci vyzkoušet si test. 

Po nakonfigurování profilu ho přiřaďte a nasaďte na své studenty. 

Pokud chcete získat další informace o této funkci, [Vyzkoušejte si testovací aplikaci v Intune](education-settings-configure.md) .

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Provést nastavení testu
Po vytvoření profilu konfigurace zařízení, přejít na **typ profilu** a vyberte **zabezpečené hodnocení (vzdělávání)**. Najdete v něm následující nastavení aplikace, které si můžete vyzkoušet. 


- **Typ účtu**: Vyberte způsob, jakým se uživatelé přihlásí k testu. Možnosti:
  - Účet Azure AD
  - Účet domény
  - Místní účet
  - Účet místního hosta: dostupný jenom na zařízeních s Windows 10 verze 1903 a novějším.    
- **Uživatelské jméno účtu**: zadejte uživatelské jméno účtu, který se používá v aplikaci pořizovat test. Účty můžete zadat v následujícím formátu:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Název účtu**: Pokud chcete nastavit typ účtu místního hosta, zadejte název účtu, který se používá v aplikaci pořizovat test. Název účtu se zobrazí jako dlaždice na přihlašovací obrazovce. Studenty spustí test kliknutím na dlaždici.  
- **Adresa URL pro vyhodnocení**: zadejte adresu URL testu, který mají uživatelé provést. Další informace o získání adresy URL najdete v dokumentaci k [provedení testu](https://docs.microsoft.com/education/windows/take-tests-in-windows-10).
- **Připojení k tiskárně**: vyberte **vyžadovat** , pokud chcete jenom přístup k aplikaci pořizovat test ze zařízení, která jsou připojená k tiskárně. Toto nastavení také zpřístupní tlačítko pro tisk aplikace pro test-uživatelé vyplňující. **Není nakonfigurované** , umožňuje studentům přístup k aplikaci ze zařízení, která nejsou připojená k tiskárně.  
- **Monitorování obrazovky**: Chcete-li monitorovat aktivitu obrazovky, zatímco uživatelé probíhají testy, vyberte možnost **Allow** . **Není nakonfigurované** , znemožní vám monitorovat obrazovku během testu.
- **Návrhy textu**: vyberte možnost **Allow** , takže test uživatelé vyplňující může zobrazit návrhy textu. **Nenakonfigurované** návrhy textu bloků, zatímco uživatelé probíhají test.

## <a name="next-steps"></a>Další kroky

Nezapomeňte [profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).
