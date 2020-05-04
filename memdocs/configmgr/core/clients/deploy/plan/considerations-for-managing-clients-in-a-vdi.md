---
title: Správa klientů VDI
titleSuffix: Configuration Manager
description: Správa Configuration Manager klientů v infrastruktuře virtuálních klientských počítačů (VDI).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713321"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Správa klientů Configuration Manager v infrastruktuře virtuálních klientských počítačů (VDI)

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje instalaci klienta Configuration Manager na následujících scénářích infrastruktury virtuálních klientských počítačů (VDI):  

- **Osobní virtuální počítače** – osobní virtuální počítače se obecně používají v případě, že se chcete ujistit, že jsou data a nastavení uživatelů na virtuálním počítači mezi relacemi zachovaná.  

- **Relace služby Vzdálená plocha** – Služba vzdálené plochy umožňuje serveru hostovat víc souběžných klientských relací. Uživatelé se můžou připojit k relaci a pak na tomto serveru spouštět aplikace.  

- **Virtuální počítače ve fondu** – virtuální počítače ve fondu se mezi relacemi netrvaly. Při zavření relace jsou všechna data a nastavení zahozena. Virtuální počítače ve fondu jsou užitečné, když nelze použít vzdálenou plochu, protože požadovaná obchodní aplikace nemůže běžet na Windows serveru, který je hostitelem klientských relací.  

  V následující tabulce jsou uvedeny pokyny pro správu klienta Configuration Manager v infrastruktuře virtuálních klientských počítačů.  

|Typ virtuálního počítače|Požadavky|  
|--------------------------|--------------------|  
|Osobní virtuální počítače|Configuration Manager zpracovává osobní virtuální počítače identicky na fyzickém počítači. Klienta Configuration Manager lze předem nainstalovat do image virtuálního počítače nebo nasadit po zřízení virtuálního počítače.|  
|Vzdálená plocha|Klient Configuration Manager není nainstalován pro jednotlivé relace vzdálené plochy. Místo toho se klient instaluje jenom jednou na serveru služby Vzdálená plocha. Všechny funkce Configuration Manager lze použít na serveru služby Vzdálená plocha.|  
|Virtuální počítače ve fondu|Když je virtuální počítač ve fondu vyřazený z provozu, budou ztraceny všechny změny, které provedete pomocí Configuration Manager.<br /><br /> Data vrácená z Configuration Managerch funkcí, jako je inventář hardwaru, inventář softwaru a měření softwaru, nemusí být relevantní pro vaše potřeby, protože virtuální počítač může být funkční jenom na krátkou dobu. Zvažte možnost vyloučit z úloh inventáře virtuální počítače ve fondu.|  

 Protože virtualizace podporuje spouštění více Configuration Manager klientů na jednom fyzickém počítači, mnoho operací klienta má vestavěnou náhodnou prodlevu pro plánované akce, jako jsou například inventář hardwaru a softwaru, kontroly antimalwaru, instalace softwaru a kontroly aktualizací softwaru. Tato prodleva pomáhá distribuovat výpočetní výkon procesoru a přenos dat pro počítač, který obsahuje více virtuálních počítačů, na kterých běží klient Configuration Manager.  

> [!NOTE]  
>  S výjimkou klientů se systémem Windows Embedded, kteří jsou v režimu obsluhy, Configuration Manager klienti, kteří nejsou spuštěni ve virtualizovaných prostředích, také používají toto náhodné zpoždění. Pokud máte mnoho nasazených klientů, toto chování pomáhá zabránit špičkám v šířce pásma sítě a snižuje požadavky na výpočetní výkon procesoru v Configuration Manager systémech lokality, jako je například bod správy a server lokality. Interval zpoždění se liší podle možnosti Configuration Manager.  
>   
>  Prodleva náhodného přeskupování je ve výchozím nastavení pro požadované aktualizace softwaru zakázáno pomocí následujícího klientského nastavení: **Agent počítače**: **Zakázat náhodné přeskupování času termínu**.
