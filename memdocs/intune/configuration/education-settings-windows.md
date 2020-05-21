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
ms.openlocfilehash: 55e38ac8b5503e98df4878529ac892b55a52be47
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429621"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Konfigurace aplikace pořizovat test na zařízeních s Windows 10 pomocí Intune

Aplikace převzít test vám umožní bezpečně spravovat online testy na zařízeních s Windows 10 vaší učebnou. Pokud chcete nastavit aplikaci pořizovat test, budete muset vytvořit profil konfigurace zařízení v Intune a nakonfigurovat nastavení zabezpečení pro vyhodnocení. Tento článek popisuje nastavení, která najdete pro aplikaci vyzkoušet si test. 

Po nakonfigurování profilu ho přiřaďte a nasaďte na své studenty. 

Pokud chcete získat další informace o této funkci, [Vyzkoušejte si testovací aplikaci v Intune](education-settings-configure.md) .

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Provést nastavení testu

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
- **Připojení tiskárny**: **vyžadovat** přístup pouze k aplikaci převzít test ze zařízení, která jsou připojena k tiskárně. Toto nastavení také zpřístupní tlačítko pro tisk aplikace pro test-uživatelé vyplňující. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém může studentům dovolit přístup k aplikaci ze zařízení, která nejsou připojená k tiskárně.  
- **Sledování obrazovky**: **umožňuje** sledovat aktivitu obrazovky, zatímco uživatelé probíhají test. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit v monitorování obrazovky během testu.
- **Návrhy textu**: vyberte možnost **Allow** , takže test uživatelé vyplňující může zobrazit návrhy textu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zablokovat návrhy textu, zatímco uživatelé probíhají test.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Přečtěte si další informace o [aplikaci Vyzkoušejte si test](education-settings-configure.md).
