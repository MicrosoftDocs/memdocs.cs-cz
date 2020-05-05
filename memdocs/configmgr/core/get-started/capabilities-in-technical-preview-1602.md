---
title: Možnosti ve verzi Technical Preview 1602
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1602.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074465"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1602 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1602. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

 V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a>Vylepšení správy mobilních zařízení  

### <a name="ios-activation-lock"></a>Zámek aktivace pro iOS  
 Configuration Manager vám může pomáhat spravovat Zámek aktivace pro iOS, což je funkce aplikace Najít iPhone pro zařízení s iOS 7,1 a novějším. Zámek aktivace se povolí automaticky, když se na zařízení používá aplikace Najít iPhone. Když je tato funkce povolená, musí se zadat Apple ID a heslo uživatele, aby bylo možné:  

- Vypnout aplikaci Můj iPhone  

- Vymazat zařízení  

- Znovu aktivovat zařízení  

  Configuration Manager může požádat o stav Zámek aktivace jak na zařízení pod dohledem, tak i na zařízeních, která používají systém iOS 7,1 nebo novější. Pro dozorovaná zařízení může služba Intune získat kód pro vyřazení zámku aktivace a přímo ho předat zařízení.  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a>Vylepšení centra softwaru ve verzi 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aktualizovat počítač PC a zásady uživatele z centra softwaru  
 Nová možnost, **zásady synchronizace** byly přidány do stránky **Možnosti** > **Údržba počítače** v centru softwaru, která způsobí, že počítač aktualizuje Configuration Manager zásady počítače a uživatele.  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a>Vylepšení údržby Windows 10  
 Ve verzi 1602 Technical Preview jsme přidali následující vylepšení údržby Windows 10:  

-   Nové možnosti filtru pro plány údržby.  Nyní můžete filtrovat podle **jazyka**, **povinného**a **názvu**. Do daného nasazení se přidají jenom upgrady, které odpovídají zadaným kritériím.  

-   Když pro synchronizaci aktualizací softwaru vyberete klasifikaci **upgrady** , zobrazí se dialogové okno s upozorněním, že k úspěšné synchronizaci aktualizací softwaru a ke správnému fungování údržby Windows 10 je nutná [oprava hotfix 3095113](https://support.microsoft.com/kb/3095113) služby WSUS.  V dialogovém okně můžete přejít na článek znalostní báze Knowledge Base pro opravu hotfix.  

-   Dostupné upgrady Windows 10 se teď zobrazují jenom v uzlu aktualizace Windows **10** \ pro**všechny systémy Windows** 10 konzoly Configuration Manager. Tyto aktualizace se už nezobrazují v uzlu aktualizace **softwaru** \ **všechny aktualizace softwaru** .  

-   Koncoví uživatelé, kteří spouštějí balíček s upgradem Windows 10, budou vyzváni dialogem, který jim umožní zjistit, že budou upgradovat svůj operační systém.  
