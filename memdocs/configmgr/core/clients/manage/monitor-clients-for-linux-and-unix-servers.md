---
title: Monitorování klientů se systémem Linux/UNIX
titleSuffix: Configuration Manager
description: Monitorování klientů na serverech se systémy Linux a UNIX v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715358"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Postup monitorování klientů pro servery se systémy Linux a UNIX v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Informace ze serverů se systémy Linux a UNIX můžete zobrazit v konzole Configuration Manager pomocí stejných metod, které používáte k zobrazení informací z klientů se systémem Windows.  

 Mezi dostupné informace patří:  

- Podrobnosti o stavu od klientů v řídicích panelech konzoly Configuration Manager  

- Podrobnosti o klientech ve výchozích Configuration Manager sestav  

- podrobnosti inventáře v Průzkumníku prostředků.  

  Následující části popisují, jak získat tyto podrobnosti z Průzkumníka prostředků a sestav.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a>Použití Průzkumníka prostředků k zobrazení inventáře pro servery se systémy Linux a UNIX  

 Jakmile klient Configuration Manager odešle inventář hardwaru do Configuration Manager lokality, můžete k zobrazení těchto informací použít Průzkumník prostředků. Klient Configuration Manager pro systémy Linux a UNIX nepřidává do Průzkumník prostředků nové třídy ani zobrazení pro inventář. Data inventáře ze systémů Linux a UNIX se mapují do existujících tříd WMI. Pomocí Průzkumníku prostředků můžete podrobnosti inventáře pro servery Linux a UNIX zobrazit v klasifikaci založené na Windows.  

 Například můžete vytvořit seznam všech nativně nainstalovaných programů nalezených na serverech se systémy Linux a UNIX. Příkladem nativně nainstalovaných programů jsou balíčky **.rpms** v systému Linux nebo **.pkgs** v systému Solaris. Po odeslání inventáře klientem se systémem Linux nebo UNIX můžete zobrazit seznam všech nativně nainstalovaných programů Linux nebo UNIX v Průzkumník prostředků v konzole Configuration Manager.  

 Informace o tom, jak používat Průzkumník prostředků, najdete v tématu [použití Průzkumník prostředků k zobrazení inventáře hardwaru](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Použití sestav k zobrazení informací pro servery se systémem UNIX a Linux  
 Sestavy pro Configuration Manager obsahují informace ze serverů se systémy Linux a UNIX společně s informacemi z počítačů se systémem Windows. K integraci dat ze systémů Linux a UNIX do sestav není nutná žádná další konfigurace.  

 Například při spuštění sestavy s názvem počet verzí operačního systému se zobrazí seznam různých operačních systémů a počet klientů, které každý operační systém používají. Sestava je založená na informacích o inventáři hardwaru odeslaných různými Configuration Manager klientech, kteří běží v různých operačních systémech.  

 Je také možné vytvořit vlastní sestavy, které jsou specifické pro data serveru se systémy Linux a UNIX. Vlastnost **Popisek** třídy inventáře hardwaru **Operační systém** je užitečný atribut, který můžete použít k identifikaci určitých operačních systémů v dotazu sestavy.  

 Informace o sestavách v Configuration Manager najdete v tématu [Úvod do vytváření sestav](../../servers/manage/introduction-to-reporting.md).  
