---
title: Koexistence MDM třetích stran
titleSuffix: Configuration Manager
description: Další informace o použití služby MDM třetí strany s Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 055d79c56417135e2b08a31bc05a3ca30b5fd581
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695099"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Koexistence MDM třetí strany s Configuration Manager

Při současné správě zařízení s Windows 10 pomocí Configuration Manager i Microsoft Intune se tato funkce nazývá [spoluspráva](overview.md). Když spravujete zařízení pomocí Configuration Manager a zaregistrujete je do služby MDM třetí strany, tato funkce se nazývá *koexistence*. Pokud se dva řídící autority pro jedno zařízení nepatřičně orchestrují mezi těmito dvěma zařízeními, může být obtížné. Díky spolusprávě Configuration Manager a Intune vyvážit [úlohy](workloads.md) a zajistěte, aby nedocházelo ke konfliktům. Tato interakce neexistuje se službami třetích stran, takže existují určitá omezení možností správy koexistence.

Klient Configuration Manager může existovat společně se službou MDM třetí strany na zařízení s Windows 10 verze 1709 nebo novějším, které je připojené k Azure Active Directory. Zařízení může být jedním z následujících typů:

- Pouze [Služba Azure AD – připojeno](/azure/active-directory/devices/azureadjoin-plan) . (Tento typ se někdy označuje jako "cloudová doména připojená".  

- [Hybridní doména připojená](/azure/active-directory/devices/hybrid-azuread-join-plan), kde je zařízení připojené k místní službě Active Directory a zaregistrované ve vašem Azure Active Directory.  

> [!Note]  
> Nepodporuje [zařízení vlastněná osobně](/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

Když klient Configuration Manager zjistí, že služba MDM jiného výrobce spravuje i zařízení, automaticky deaktivuje některé úlohy v Configuration Manager. Toto chování umožňuje službě MDM převzít tyto funkce. Zabraňuje také konfliktním nastavením na straně klienta, které by mohlo negativně ovlivnit činnost zařízení a uživatele. V tomto případě jsou deaktivované následující úlohy v Configuration Manager:

- Zásady přístupu k prostředkům pro nastavení sítě VPN, Wi-Fi, e-mailu a certifikátu
- Správa aplikací, včetně starších balíčků
- Kontrola a instalace aktualizace softwaru
- Endpoint Protection, funkce programu antimalwarové ochrany v programu Windows Defender
- Zásady dodržování předpisů pro podmíněný přístup
- Konfigurace zařízení
- Správa Klikni a spusť pro Office

Klient Configuration Manager se vyhne konfliktu se autoritou pro správu třetí strany tím, že pokračuje v následujících operacích jen pro čtení:

- Inventář hardwaru a softwaru
- Funkce Asset Intelligence
- Monitorování míry využití softwaru
- Vytváření sestav řízení spotřeby

Další informace o výhodách spolusprávy pomocí Configuration Manager a Intune najdete v tématu [výhody spolusprávy](overview.md#benefits).