---
title: Import konfiguračních dat
titleSuffix: Configuration Manager
description: Importujte konfigurační data, pokud jsou obsažená ve formátu souboru CAB a vyhovují podporovanému schématu jazyka modelování služby.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 3c31f97e2a494fa4b0d3e9e825a81b562859e5dd
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240350"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Import konfiguračních dat pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Kromě vytváření standardních hodnot konfigurace a položek konfigurace v konzole Configuration Manager můžete importovat konfigurační data, pokud jsou obsažená ve formátu souboru CAB (. cab) a vyhovují podporovanému schématu SML (Service Modeling Language). Konfigurační data můžete importovat z:  

- Doporučená konfigurační data (konfigurační balíčky) stažená od Microsoftu nebo od jiných dodavatelů softwaru.  

- Konfigurační data, která byla exportována z verze System Center 2012 Configuration Manager a novější.  

- Konfigurační data, která byla externě vytvořená a která odpovídají schématu SML.  

  Příklad konfiguračního balíčku, který pomáhá zajistit dodržování předpisů pro role serveru lokality System Center 2012 Configuration Manager najdete v tématu [System Center 2012 Configuration Manager Configuration Pack](https://www.microsoft.com/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Když importujete standardní hodnoty konfigurace, některé nebo všechny položky konfigurace, které jsou odkazované ve standardních hodnotách konfigurace, můžou být i součástí souboru CAB. Během procesu importu Configuration Manager ověřuje, že všechny položky konfigurace, které jsou odkazovány ve standardních hodnotách konfigurace, jsou buď zahrnuty v souboru CAB, nebo již existují v Configuration Manager lokalitě. Proces importu se nezdaří, pokud se pokusíte importovat standardní hodnoty konfigurace, které odkazují na konfigurační data, která Configuration Manager nelze najít.  

Mezi další příčiny, které můžou proces importu narušit, patří:  

-   Konfigurační data odkazují na konfigurační data, která Configuration Manager nemůžou najít, ani ve své databázi nebo v samotném souboru CAB.  

-   Konfigurační data jsou již přítomna v databázi Configuration Manager se stejným názvem a verzí konfiguračních dat, ale verze obsahu se liší.  

-   Konfigurační data jsou již přítomna v databázi Configuration Manager se stejnou verzí obsahu, ale výpočet hodnoty hash je identifikuje jako jiný.  

-   Novější verze konfiguračních dat se stejným názvem už existuje nebo byla nedávno Odstraněná v databázi Configuration Manager.  

-   V hierarchii Configuration Manager s více lokalitami byla konfigurační data původně importována z nadřazené lokality. Je třeba je aktualizovat ze stejné lokality, nikoli z podřízené lokality.  

### <a name="import-configuration-data"></a>Import konfiguračních dat  

1.  V konzole Configuration Manager klikněte na **prostředky a**  >  **položky konfigurace** dodržování předpisů nebo **standardní hodnoty konfigurace** .
2.  Na kartě **Domů** ve skupině **vytvořit** klikněte na **importovat konfigurační data**.  
3.  Na stránce **Vybrat soubory** v **Průvodci importem dat konfigurace**klikněte na tlačítko **Přidat**, a potom v dialogovém okně **Otevřít** vyberte soubory CAB, které chcete importovat.  
4.  Zaškrtněte políčko **vytvořit novou kopii importovaných standardních hodnot konfigurace a položek konfigurace** , pokud chcete, aby byla importovaná konfigurační data upravitelná v konzole Configuration Manager.  
5.  Na stránce **Souhrn** zkontrolujte akce, které budou provedeny, a pak dokončete průvodce.  

Importovaná konfigurační data se zobrazí v uzlu **Nastavení dodržování předpisů** v pracovním prostoru **prostředky a kompatibilita** .  
