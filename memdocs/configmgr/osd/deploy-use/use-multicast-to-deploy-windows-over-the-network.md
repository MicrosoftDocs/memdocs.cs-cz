---
title: Použití vícesměrového vysílání k nasazení Windows přes síť
titleSuffix: Configuration Manager
description: V prostředí Configuration Manager použijte vícesměrové vysílání, aby bylo možné současně stáhnout image operačního systému více počítačů.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720118"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití vícesměrového vysílání k nasazení Windows přes síť s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vícesměrové vysílání je metoda optimalizace sítě, kterou můžete použít ve svém Configuration Managerovém prostředí, ve kterém může více klientů stahovat stejnou bitovou kopii operačního systému ve stejnou dobu. Při použití vícesměrového vysílání stahuje více počítačů současně bitovou kopii operačního systému vícesměrově vysílanou distribučním bodem. Distribuční bod tedy nemusí každému klientovi zasílat kopii dat přes samostatné spojení.  

 Operační systémy můžete nasadit přes síť pomocí vícesměrového vysílání v následujících scénářích nasazení operačního systému:  

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

  Proveďte kroky v jednom ze scénářů nasazení operačního systému a potom použijte následující části k podpoře vícesměrového vysílání.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Nakonfigurování distribučního bodu pro podporu vícesměrového vysílání  
 Když chcete použít vícesměrové vysílání při nasazení operačního systému, musíte nakonfigurovat distribuční bod pro podporu vícesměrového vysílání. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast). Seznam portů vyžadovaných k podpoře vícesměrového vysílání najdete v tématu [porty](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Příprava image operačního systému pro nasazení pomocí vícesměrového vysílání  
 Informace o nakonfigurování image operačního systému pro podporu vícesměrového vysílání najdete v tématu [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Nasazení pořadí úkolů  
 Nasaďte operační systém do cílové kolekce. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).  
