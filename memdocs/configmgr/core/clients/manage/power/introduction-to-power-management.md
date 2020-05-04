---
title: Úvod do řízení spotřeby
titleSuffix: Configuration Manager
description: Načtěte si Úvod do řízení spotřeby v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715218"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Úvod do řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Řízení spotřeby v Configuration Manager řeší nutnost, aby řada organizací mohla monitorovat a snižovat spotřebu energie jejich počítačů. Tato funkce využívá možnosti řízení spotřeby systému Windows a umožňuje provést odpovídající a konzistentní nastavení všech počítačů v celé organizaci. Můžete použít odlišná nastavení spotřeby v pracovní době a mimo pracovní dobu. Schéma napájení může být například mimo pracovní dobu výrazně úspornější. V případech, kdy je třeba, aby počítače běžely trvale, můžete použití obecných nastavení řízení spotřeby vynechat.  

 Řízení spotřeby v Configuration Manager zahrnuje několik sestav, které vám pomůžou analyzovat spotřebu energie a nastavení napájení počítačů ve vaší organizaci. Můžete také vytvářet sestavy a použít je k řešení problémů s řízením spotřeby.  

 Podrobný postup konfigurace a používání řízení spotřeby najdete v tématu [Kontrolní seznam správce pro řízení spotřeby](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Na virtuálních počítačích se nepodporuje Configuration Manager řízení spotřeby. Schémata napájení nemůžete použít na virtuální počítače, ani z nich nemůžete získávat údaje o napájení.  

## <a name="the-power-management-workflow"></a>Pracovní postup řízení spotřeby  
 K naplánování a implementaci řízení spotřeby v Configuration Manager použijte následující tři fáze.  

### <a name="monitoring-and-planning-phase"></a>Fáze monitorování a plánování  
 Řízení spotřeby používá Configuration Manager inventáře hardwaru ke shromažďování dat o využití počítače a nastavení spotřeby pro počítače v lokalitě. Tato data můžete analyzovat prostřednictvím mnoha sestav a určit tak optimální nastavení řízení spotřeby pro počítače. Během fáze monitorování a plánování správy napájení můžete například vytvořit kolekce založené na datech, které jsou shromážděny v sestavě **Možnosti napájení** a tato data použít k identifikaci počítačů, které neumožňují řízení spotřeby. Pak můžete tyto počítače z řízení spotřeby vyloučit.  

> [!IMPORTANT]  
>  Nepoužívejte na počítače ve vaší lokalitě schémata napájení, dokud neshromáždíte a nezanalyzujete data napájení z klientských počítačů. Pokud použijete nové nastavení řízení spotřeby bez předchozího prozkoumání stávajícího nastavení, může to vést ke zvýšení spotřeby energie.  

### <a name="enforcement-phase"></a>Fáze vynucení  
 Řízení spotřeby umožňuje vytvářet schémata napájení, které lze použít na kolekce počítačů ve vaší lokalitě. Tato schémata napájení určují nastavení řízení spotřeby systému Windows na počítačích ve vaší lokalitě. Můžete použít schémata napájení, která jsou součástí Configuration Manager, nebo můžete nakonfigurovat vlastní schémata napájení. Data o napájení shromážděná během fáze monitorování a plánování můžete použít jako podklad pro vyhodnocení úspor, které vám zavedení schématu napájení přinese. Další informace najdete v tématu [Kontrolní seznam správce pro řízení spotřeby](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Fáze dodržování předpisů  
 Ve fázi dodržování předpisů můžete vytvořit sestavy, které vám pomohou při vyhodnocení spotřeby a úspory nákladů na energii ve vaší organizaci. Můžete také spustit sestavy, které popisují vylepšení v množství CO2 vygenerovaného počítači. Jsou dostupné také sestavy, které vám pomůžou ověřit, že nastavení spotřeby byla v počítačích správně provedena, případně vyřešit problémy s funkcí řízení spotřeby.  
