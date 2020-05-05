---
title: Configuration Manager a Windows jako služba
titleSuffix: Configuration Manager
description: Získejte základní informace o přijetí Configuration Manager aktuální větve pro podporu Windows jako služby.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718550"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager a Windows jako služba

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager poskytuje komplexní kontrolu nad aktualizacemi funkcí pro Windows 10. Pokud chcete plně přijmout Windows jako model služby, musíte taky přijmout Configuration Manager aktuální model větve. Abyste mohli zůstat v aktuálním prostředí s Windows 10, musíte zůstat v aktuálním Configuration Manager, abyste mohli co nejlépe využívat. K dispozici jsou nové verze Configuration Manager, aby plně využily Skvělé nové podnikové funkce pro Windows 10. Tento článek je určený jako cílová stránka pro klíčové články vyžadované k přijetí Configuration Manager aktuální větve. Configuration Manager aktuální větev vás připraví na způsob, jakým se jako služba stane Windows.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Klíčové články o přijetí Configuration Manager aktuální větve

| Článek        | Popis          | 
| ------------- |-------------|
|[Přehled Configuration Manager aktuální větve](../plan-design/changes/whats-new-incremental-versions.md)|Poskytuje stručný přehled klíčových bodů pro nový model údržby pro Configuration Manager (Current Branch).|
|[Životní cyklus podpory](../servers/manage/current-branch-versions-supported.md)|Vysvětluje nový model podpory a údržby.|
|[Odebrané a zastaralé položky](../plan-design/changes/deprecated/removed-and-deprecated.md)|Poskytuje úvodní oznámení o budoucích změnách, které můžou ovlivnit použití Configuration Manager.|
|[Aktualizace Configuration Manager aktuální větve](../servers/manage/updates.md)|Vysvětluje snadnou konzolovou metodu použití aktualizací funkcí na Configuration Manager.|
|[Získání dostupných aktualizací](../servers/manage/install-in-console-updates.md#get-available-updates)|Vysvětluje dva režimy, které jsou k dispozici pro získání nových Configuration Manager aktualizací funkcí.|
|[Aktualizovat kontrolní seznam](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Poskytuje kontrolní seznamy pro konkrétní verzi aktualizace, pokud jsou k dispozici.| 
|[Nainstalovat nové aktualizace funkcí Configuration Manager](../servers/manage/install-in-console-updates.md#bkmk_install)|V této části najdete popis jednoduchých kroků instalace pro aktualizace funkcí.|
|[Podpora pro Windows 10](../plan-design/configs/support-for-windows-10.md)|Poskytuje podpůrnou matrici pro verze Windows 10 (a ADK).|
|[Verze Technical Preview pro Configuration Manager](../get-started/technical-preview.md)|Poskytuje informace o programu ConfigMgr Technical Preview.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Klíčové články týkající se přijetí Windows jako služby

| Článek        | Popis          |
| ------------- |-------------|
|[Správa Windows jako služby](../../osd/deploy-use/manage-windows-as-a-service.md)|Vysvětluje, jak pomocí plánů údržby nasadit aktualizace funkcí Windows 10.|
|[Upgrade Windows 10 prostřednictvím pořadí úkolů](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Podrobnosti o vytváření pořadí úkolů pro upgrade Windows 10 s dalšími doporučeními.|
|[Postupná nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Postupná nasazení automatizují koordinované, sekvenční zavedení pořadí úkolů napříč více kolekcemi.|  
|[Optimalizace doručování aktualizací Windows 10](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Pomocí Configuration Manager můžete spravovat obsah aktualizací, aby zůstal aktuální s Windows 10.|
|[Použití desktopové analýzy](../../desktop-analytics/overview.md)|Desktop Analytics umožňuje vyhodnotit a analyzovat připravenost zařízení ve vašem prostředí pro upgrade na Windows 10.|
|[Integrace web Windows Update pro firmy (volitelné)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Vysvětluje, jak definovat a nasadit zásady web Windows Update pro firmy (WUfB) pomocí Configuration Manager.|
|[Použití spolusprávy s Microsoft Intune a web Windows Update pro firmy (volitelné)](../../comanage/overview.md)|Poskytuje přehled spolusprávy.|


## <a name="related-articles"></a>Související články

- [Místní upgrade na Configuration Manager aktuální větev ze System Center 2012 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Plánování migrace na Configuration Manager aktuální větev](../migration/planning-for-migration.md)
