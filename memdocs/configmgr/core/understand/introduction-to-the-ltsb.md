---
title: Seznámení s LTSB
titleSuffix: Configuration Manager
description: Přečtěte si informace o dlouhodobé údržbě Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1370c1bf80283ff30ad54378ad58ecd9a5d24d47
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699360"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Úvod do větve dlouhodobé údržby Configuration Manager

*Platí pro: System Center Configuration Manager (větev dlouhodobé údržby)*

LTSB (Long-Term Servicing Branch) pro Configuration Manager je samostatná větev navržená jako možnost instalace dostupná všem zákazníkům. Je ale jedinou možností pro zákazníky, kteří ponechají své právo programu Software Assurance (SA) nebo ekvivalentní práva k předplatnému pro Configuration Manager.

V závislosti na Configuration Manager verze 1606 má LTSB omezenou funkčnost v porovnání s aktuální větví Configuration Manager.

> [!TIP]   
> Configuration Manager LTSB se nevztahují na kanál pro dlouhodobé obsluhy sady System Center (LTSC). Další informace najdete v tématu [Přehled možností vydání produktu System Center](/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Funkce, které nejsou k dispozici

Aktuální větev Configuration Manager podporuje následující funkce, které nejsou k dispozici, když používáte LTSB:

- Konzolové aktualizace, které přidávají nové funkce a vylepšení.
- Podpora nově vydaných operačních systémů pro použití jako serverů lokality a klientů.
- Místní správa MDM
- Řídicí panel údržby Windows 10 a plány údržby, včetně podpory pro nejnovější verze Windows 10.  
- Podpora budoucích verzí Windows serveru a Windows 10 LTSB
- Funkce Asset Intelligence
- Cloudové distribuční body
- Exchange Online jako konektor Exchange    

I když podpora pro tyto funkce není v LTSB k dispozici, některé funkce zůstanou v konzole Configuration Manager viditelné, ale nedají se vybrat ani použít.

Integrace cloudu a všechny funkce, které jsou součástí Configuration Manager aktuální větvi verze 1610 nebo novější, nejsou dostupné pro LTSB. Tyto funkce zahrnují, ale nejsou omezeny na následující:<!--SCCMDocs#1823-->

- Spoluspráva
- Desktop Analytics
- Brána pro správu cloudu
- Integrace Azure Active Directory
- Aplikace z Microsoft Store pro firmy

## <a name="find-ltsb-documentation"></a>Najít dokumentaci k LTSB

LTSB vychází z aktuální větve verze 1606. Použijte [dokumentaci k aktuální větvi](../../index.yml)s upozorněními a omezeními, která jsou specifická pro LTSB. Tato upozornění a omezení se identifikují v následujících článcích:

- [Instalace LTSB](install-the-ltsb.md)
- [Upgrade LTSB na aktuální větev](convert-to-current-branch.md)
- [Podporované konfigurace pro LTSB](supported-configurations-for-ltsb.md)
- [Správa LTSB Configuration Manager](manage-the-ltsb.md)

Když odkazujete na dokumentaci k aktuální větvi pro LTSB, budou se podrobnosti, které se vztahují na verzi 1606 nebo starší, vztahovat také na LTSB. Funkce nebo podrobnosti, které jsou představeny pomocí verze 1610 nebo novější, nejsou podporovány rozhraním LTSB.

## <a name="licensing-overview-for-the-ltsb"></a>Přehled licencování pro LTSB   

Zákazníci s aktivním softwarem Software Assurance (SA) na Configuration Manager licencí nebo s ekvivalentními právy k předplatnému od 1. října 2016 mají práva k použití verze Configuration Manager z října 2016 verze 1606. Zákazníci s právy k Configuration Manager od 1. října 2016 budou při instalaci najít dvě licencované možnosti: aktuální větev a dlouhodobá obsluha větve (LTSB).

Zákazníci, kteří mají trvalá práva k System Center Configuration Manager nebo které umožňují, aby se přidružení zabezpečení nebo předplatné poniklo po 1. říjnu, může nainstalovat verzi System Center Configuration Manager LTSB, která je aktuální v době trvání platnosti.

Další informace o těchto licencích najdete v tématu [Úplné podmínky a ujednání pro produkty, které zakoupíte v rámci multilicenčních programů společnosti Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).

Další informace o licencování pro Configuration Manager větvích najdete v článku [Configuration Manager licencování a větví](learn-more-editions.md).

## <a name="next-steps"></a>Další kroky

Pokud se rozhodnete, že Configuration Manager LTSB je správná větev pro vaše prostředí, [nainstalujte novou](install-the-ltsb.md#install-a-new-site) lokalitu LTSB jako součást nové hierarchie nebo [upgradujte lokalitu a hierarchii nástroje System Center 2012 Configuration Manager](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) .