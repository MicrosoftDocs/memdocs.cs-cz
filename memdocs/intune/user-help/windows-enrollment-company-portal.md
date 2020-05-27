---
title: Registrace zařízení s Windows v Portál společnosti Intune | Microsoft Docs
description: Začínáme s registrací zařízení s Windows v Portál společnosti
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/24/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 36250832-c6fd-4e8d-b681-de735023ebc3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jieyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5e7cd5e5fa5f04e674b2fd9d37c8895b72372c4c
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881406"
---
# <a name="windows-device-enrollment-in-intune-company-portal"></a>Registrace zařízení s Windows v Portál společnosti Intune  

Zaregistrujte zařízení s Windows v aplikaci Portál společnosti Intune, abyste získali zabezpečený přístup k pracovním a školním aplikacím, e-mailům a souborům. Pokud vaše organizace vyžaduje nebo doporučí určité aplikace, jako je například Office nebo OneDrive, obdržíte je buď během registrace, nebo budou po registraci k dispozici v Portál společnosti.  

Zařízení s Windows 10 můžete zaregistrovat pomocí Portál společnosti webu *nebo* aplikace. Pokud zaregistrujete zařízení v dřívější verzi Windows, musíte zařízení zaregistrovat prostřednictvím webu Portál společnosti.  

## <a name="install-company-portal-app"></a>Instalace aplikace Portál společnosti  
V zařízení už možná máte nainstalovanou aplikaci Portál společnosti. Ověřte aplikaci v seznamu __všechny aplikace__ .  Pokud nevidíte Portál společnosti v seznamu aplikací, postupujte podle těchto kroků a nainstalujte je.  

1. Otevřete na svém zařízení **Microsoft Store** .

2. Do **vyhledávacího** pole zadejte **portál společnosti**.

3. V seznamu výsledků vyberte **portál společnosti**  >  **nainstalovat**.

4. Vyberte buď **Instalovat**, nebo **Zdarma**. Mezi těmito dvěma možnostmi není žádný rozdíl; slova se zobrazí v závislosti na tom, jak vaše organizace tuto aplikaci nastavila.  

## <a name="find-windows-10-version-number"></a>Najít číslo verze Windows 10  
Postup registrace se liší u různých verzí zařízení s Windows 10. Následující postup popisuje, jak najít číslo verze na zařízeních s Windows 10 Desktop a Mobile. Až poznáte vaši verzi, pokračujte doporučenými kroky registrace.  

### <a name="windows-10-desktop-devices"></a>Zařízení s Windows 10 Desktop  

1. Přejděte na **Start**.

2. Na panelu hledání zadejte frázi "informace o vašem počítači". Z výsledků vyberte __o svém počítači__ .  


   ![nastavení vyhledávání pro informace o počítači](media/searching_for_about_your_pc.png)  

3. Přejděte dolů na **specifikace Windows** a najděte **verzi** Windows 10, která je nainstalovaná na vašem počítači.  


   ![Windows 10 Desktop – Informace o počítači](media/settings_about_pc.png)  

4. Pokud je vaše verze  

    * __1607 nebo novější__: Zaregistrujte zařízení pomocí [ **Settings**  >  **účtu**nastavení  >  **přístup k pracovnímu nebo školnímu** postupu](enroll-windows-10-device.md#enroll-windows-10-version-1607-and-later-device).   
    * __1511 nebo starší__: Zaregistrujte zařízení pomocí účtu nastavení, na který [ **Settings**  >  **Account**  >  **vaše účty** směrují](enroll-windows-10-device.md#enroll-windows-10-version-1511-and-earlier-device).  

### <a name="windows-10-mobile-devices"></a>Zařízení s Windows 10 Mobile

1. Přejít na __všechny aplikace__ a vybrat aplikaci __Nastavení__ .
2. Vyberte __systém__  >  __o produktu__.
3. V části __informace o zařízení__vyhledejte __verzi__.  
4. Pokud je vaše verze  

    * __1607 nebo novější__: Zaregistrujte své zařízení pomocí [ **Nastavení**  >  **přístup do pracovní nebo školní** trasy](enroll-windows-10-device.md#enroll-windows-10-version-1607-and-later-device).   
    * __1511 nebo starší__: Zaregistrujte své zařízení pomocí [ **Nastavení**  >  trasa**účty** ](enroll-windows-10-device.md#enroll-windows-10-version-1511-and-earlier-device).  

## <a name="enroll-non-windows-10-devices"></a>Registrace zařízení bez Windows 10  
Následující články použijte k registraci dalších podporovaných zařízení s Windows prostřednictvím webu Portál společnosti:   
* [Windows 8.1. nebo zařízení s Windows RT 8,1](enroll-your-W81-or-rt81-windows.md)  
* [Zařízení Windows Phone 8,1](enroll-your-wp81-windows.md)    

## <a name="it-administrator-support"></a>Podpora správce IT  
Pokud jste správcem IT a máte potíže s registrací zařízení, přečtěte si téma řešení potíží s registrací [zařízení s Windows v Microsoft Intune](https://support.microsoft.com/help/4469913). V tomto článku jsou uvedené běžné chyby, jejich příčiny a kroky, jak je vyřešit.  

## <a name="next-steps"></a>Další kroky  
Teď, když znáte podporovaná zařízení a číslo verze Windows 10, přejděte k doporučenému článku o registraci.  
 
Další informace o správě zařízení, Portál společnosti a způsobu použití obou škol a v práci najdete v následujících článcích:  
* [Použití spravovaných zařízení pro přístup k pracovnímu nebo školnímu prostředku](use-managed-devices-to-get-work-done.md)  
* [Co se stane po registraci zařízení v Intune](what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md)  
* [Jaké informace moje organizace uvidí, když zaregistruji své zařízení?](what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md)  

Potřebujete pomoc? Obraťte se na podporu ve vaší společnosti. Pokud chcete najít kontaktní informace oddělení IT, [navštivte web portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980) .  
