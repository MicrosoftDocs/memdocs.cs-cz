---
title: Správa konfiguračních dat
titleSuffix: Configuration Manager
description: Po vytvoření položek konfigurace a směrných plánů v Configuration Manager můžete použít jiné příkazy k provádění různých akcí.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: c375b5d773775e1be89f1e9dda38ee04e7f9f63f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240248"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Spravovat konfigurační data v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po vytvoření položek konfigurace a standardních hodnot konfigurace v Configuration Manager jsou k dispozici další příkazy, které vám pomohou provádět různé akce.  

## <a name="manage-configuration-items"></a>Správa položek konfigurace  

-   V pracovním prostoru **prostředky a kompatibilita** rozbalte položku **Nastavení dodržování předpisů**  >  **položky konfigurace**, vyberte položku konfigurace, kterou chcete spravovat, a potom vyberte úlohu správy.  

|Úloha správy|Podrobnosti|  
|---------------------|-------------|  
|**Vytvoření podřízené položky konfigurace**|Otevře **Průvodce vytvořením podřízené položky konfigurace** , kde můžete vytvořit podřízenou položku konfigurace z vybrané položky konfigurace.<br /><br /> Nejde vytvořit podřízenou položku konfigurace z položky konfigurace mobilního zařízení.<br /><br /> Podrobnosti najdete v tématu [Vytvoření podřízených položek konfigurace](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Historie revizí**|Otevře dialogové okno **Historie revizí položky konfigurace** , kde můžete zobrazit a spravovat předchozí revize vybrané položky konfigurace.|  
|**Zobrazit definici XML**|Zobrazí soubor definice XML pro vybranou položku konfigurace v novém okně. Tyto informace mohou být užitečné, když chcete vytvořit konfigurační data ručně.|  
|**Export**|Exportuje položku konfigurace ve formátu souboru CAB, pokud byl vytvořený v dané lokalitě. Pak ho můžete importovat do stejné nebo jiné Configuration Manager lokality. Konfigurační data se převedou na schéma DCM Digest.|  
|**Kopírovat**|Vytvoří kopii vybrané položky konfigurace s názvem, který zadáte. Nová položka konfigurace nezachovává žádný vztah k původní položce konfigurace. To znamená, že duplicitní položka konfigurace nebude dále dědit informace o konfiguraci z původní položky konfigurace.|  
|**Odstranit**|Otevře dialogové okno **Odstranit položku konfigurace** , kde můžete zkontrolovat všechny odkazy na tuto položku konfigurace.<br /><br /> Před odstraněním položky konfigurace musíte odebrat všechny odkazy na tuto položku konfigurace.|  

## <a name="manage-configuration-baselines"></a>Správa standardních hodnot konfigurace  

-   V pracovním prostoru **prostředky a kompatibilita** rozbalte standardní hodnoty konfigurace **Nastavení dodržování předpisů**  >  **Configuration Baselines**, vyberte standardní hodnoty konfigurace, které chcete spravovat, a pak vyberte úlohu správy.  


|Úloha správy|Podrobnosti|  
|---------------------|-------------|  
|**Zobrazit členy**|Zobrazí všechny položky konfigurace, na které odkazuje standardní hodnota konfigurace.|  
|**Plánovat souhrn**|Konfiguruje plán, podle kterého se data zobrazená v uzlu **standardní hodnoty konfigurace** v konzole Configuration Manager aktualizují pomocí nejnovějších informací z databáze lokality.|  
|**Spustit souhrn**|Souhrn způsobí, že data zobrazená v uzlu **Standardní hodnoty konfigurace** se aktualizují pomocí nejnovějších dat z databáze lokality. Dokončení této akce může trvat několik minut. Abys se v konzole zobrazila nejnovější data, budete možná muset kliknout na **Aktualizovat** .|  
|**Zobrazit definici XML**|Zobrazí soubor definice XML pro vybranou standardní hodnotu konfigurace v novém okně. Tyto informace mohou být užitečné, když chcete vytvořit konfigurační data ručně.|  
|**Povolit**|Povolí standardní hodnotu konfigurace pro sledování dodržování předpisů.|  
|**Zakázat**|Zakáže standardní hodnotu konfigurace, takže se pro ni už nevyhodnocuje dodržování předpisů na klientských počítačích. Standardní hodnoty konfigurace, které odkazují na tuto standardní hodnotu konfigurace, budou taky zakázané.|  
|**Export**|Exportuje standardní hodnotu konfigurace ve formátu souboru CAB, pokud byl vytvořený v dané lokalitě. Pak ho můžete importovat do stejné nebo jiné Configuration Manager lokality. Konfigurační data se převedou na schéma DCM Digest.<br /><br /> Informace o tom, jak importovat konfigurační data, najdete v tématu [import konfiguračních dat](../../compliance/deploy-use/import-configuration-data.md).|  
|**Kopírovat**|Vytvoří kopii vybrané standardní hodnoty konfigurace s názvem, který zadáte. Nová standardní hodnota konfigurace nezachovává žádný vztah k původní standardní hodnotě konfigurace.|  
|**Odstranit**|Otevře dialogové okno **Odstranit standardní hodnotu konfigurace** , kde můžete zkontrolovat všechny odkazy na tuto standardní hodnotu konfigurace.<br /><br /> Před odstraněním standardní hodnoty konfigurace musíte odebrat všechny odkazy na tuto standardní hodnotu konfigurace.|  
|**Nasazení**|Otevře dialogové okno **Nasazení standardní hodnoty konfigurace** , kde můžete nasadit jednu nebo víc standardních hodnot konfigurace do zařízení ve vaší hierarchii.<br /><br /> Podrobnosti najdete v tématu [nasazení standardních hodnot konfigurace](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
