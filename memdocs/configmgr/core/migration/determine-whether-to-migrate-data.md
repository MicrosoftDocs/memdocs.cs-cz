---
title: Vyberte, co se má migrovat.
titleSuffix: Configuration Manager
description: Seznamte se s daty, která můžete migrovat, a která data nemůžete migrovat na Configuration Manager aktuální větev.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718914"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Určení, zda se mají migrovat data do Configuration Manager aktuální větve

*Platí pro: Configuration Manager (Current Branch)*

Migrace v Configuration Manager aktuální větve poskytuje proces pro přenos dat a konfigurací, které jste vytvořili z podporovaných verzí Configuration Manager do vaší nové hierarchie.  Můžete to použít ke:  

-   Kombinovat více hierarchií do jedné.  

-   Přesunutí dat a konfigurací z nasazení testovacího prostředí do produkčního nasazení.

-   Přesunutí dat a konfigurace z předchozí verze Configuration Manager, například Configuration Manager 2007, která nemá žádnou cestu upgradu na Configuration Manager aktuální větve nebo ze služby System Center 2012 Configuration Manager (která podporuje cestu pro upgrade na Configuration Manager aktuální větve).  

S výjimkou role distribučního bodu a počítačů hostujících distribuční body nelze migrovat, přenášet či sdílet žádnou infrastrukturu (lokality, role systémů lokalit nebo počítače hostující role systémů lokalit) mezi hierarchiemi.  

 I když nemůžete migrovat serverovou infrastrukturu, můžete migrovat Configuration Manager klienty mezi hierarchiemi. Migrace klientů zahrnuje migraci dat používaných klienty ze zdrojové hierarchie do cílové a následnou instalaci nebo nové přiřazení klientského softwaru, po kterém se klient stane součástí nové hierarchie.

Když nainstalujete klienta do nové hierarchie a klient odešle svá data, jeho jedinečné ID Configuration Manager pomůže Configuration Manager přidružit data, která jste předtím migrovali u každého klientského počítače.  

 Funkce, které poskytuje migrace, vám pomůžou udržovat investice, které jste provedli v konfiguracích a nasazeních, a současně vám umožní plně využít základní změny v produktu (poprvé se zavedly do System Center 2012 Configuration Manager a pak pokračovaly v Configuration Manager). Tyto změny zahrnují zjednodušenou Configuration Manager hierarchii, která používá méně lokalit a prostředků, a vylepšené zpracování, které pochází z použití nativního 64ho kódu, který běží na 64 hardwaru.  

 Informace o verzích Configuration Manager, které migrace podporuje, najdete v tématu [předpoklady pro migraci](../../core/migration/prerequisites-for-migration.md).  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a>Data, která můžete migrovat na Configuration Manager aktuální větev

Migrace může migrovat většinu objektů mezi podporovanými Configuration Manager hierarchiemi. Migrované instance některých objektů z podporované verze Configuration Manager 2007 musí být upraveny tak, aby odpovídaly schématu a formátu objektů nástroje System Center 2012 Configuration Manager.

Tyto úpravy nemají vliv na data v databázi zdrojové lokality. Objekty migrované z podporované verze System Center 2012 Configuration Manager nebo Configuration Manager aktuální větve nevyžadují úpravy.  

Níže jsou objekty, které mohou být migrovány na základě verze Configuration Manager ve zdrojové hierarchii. Některé objekty, jako jsou dotazy, se nemigrují. Chcete-li tyto objekty, které se nemigrují, nadále používat, musíte je v nové hierarchii znovu vytvořit. Další objekty, včetně některých klientských dat, se při správě klientů v této hierarchii automaticky znovu vytvoří v nové hierarchii.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Objekty, které lze migrovat z verze System Center 2012 Configuration Manager nebo Configuration Manager aktuální větev

-   Aplikace pro System Center 2012 Configuration Manager a novější verze  

-   Virtuální prostředí App-V z nástroje System Center 2012 Configuration Manager a novějších verzí  

-   Přizpůsobení funkce Asset Intelligence  

-   Hranice  

-   Kolekce: pro migraci kolekcí z podporované verze nástroje System Center 2012 Configuration Manager nebo Configuration Manager aktuální větve použijte úlohu migrace objektů.  

-   Nastavení dodržování předpisů:  

    -   Standardní hodnoty konfigurace  

    -   Položky konfigurace  

-   Nasazení  

-   Nasazení operačního systému:  

    -   Spouštěcí image  

    -   Balíčky ovladačů  

    -   Ovladače  

    -   Obrázky  

    -   Balíčky  

    -   Pořadí úloh  

-   Výsledky hledání: uložená kritéria hledání  

-   Aktualizace softwaru:  

    -   Nasazení  

    -   Balíčky pro nasazení  

    -   Šablony  

    -   Seznamy aktualizací softwaru  

-   Balíčky distribuce softwaru  

-   Pravidla distribuce softwaru  

-   Balíčky virtuálních aplikací  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objekty, které lze migrovat z Configuration Manager 2007 SP2

-   Inzerování  

-   Aplikace pro System Center 2012 Configuration Manager a novější verze  

-   Virtuální prostředí App-V z nástroje System Center 2012 Configuration Manager a novějších verzí  

-   Přizpůsobení funkce Asset Intelligence  

-   Hranice  

-   Kolekce: migrujete kolekce z podporované verze Configuration Manager 2007 pomocí úlohy migrace kolekce.  

-   Nastavení dodržování předpisů (ve verzi Configuration Manageru 2007 označované jako správa požadované konfigurace):  

    -   Standardní hodnoty konfigurace  

    -   Položky konfigurace  

-   Nasazení operačního systému:  

    -   Spouštěcí image  

    -   Balíčky ovladačů  

    -   Ovladače  

    -   Obrázky  

    -   Balíčky  

    -   Pořadí úloh  

-   Výsledky hledání: složky výsledků hledání  

-   Aktualizace softwaru:  

    -   Nasazení  

    -   Balíčky pro nasazení  

    -   Šablony  

    -   Seznamy aktualizací softwaru  

-   Balíčky distribuce softwaru  

-   Pravidla distribuce softwaru  

-   Balíčky virtuálních aplikací  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a>Data, která nelze migrovat na Configuration Manager aktuální větev

Nelze migrovat následující typy objektů:  

-   Informace o zřizování AMT pro klienty  

-   Soubory na klientech, včetně:  

    -   Data inventáře a historie klientů  

    -   Soubory v mezipaměti klientů  

-   Dotazy  

-   Configuration Manager 2007 a bezpečnostní práva a instance pro web a objekty  

-   Sestavy Configuration Manager 2007 z SQL Server Reporting Services  

-   Webové sestavy Configuration Manager 2007  

-   Sestavy aktuální větve pro System Center 2012 Configuration Manager a Configuration Manager  

-   System Center 2012 Configuration Manager a Configuration Manager aktuální správy založené na rolích Branch:  

    -   Role zabezpečení  

    -   Obory zabezpečení  
