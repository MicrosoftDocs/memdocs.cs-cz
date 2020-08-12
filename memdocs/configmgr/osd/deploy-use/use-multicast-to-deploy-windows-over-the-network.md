---
title: Použití vícesměrového vysílání k nasazení Windows přes síť
titleSuffix: Configuration Manager
description: Používejte vícesměrové vysílání v prostředí Configuration Manager, aby bylo možné současně stáhnout image operačního systému více počítačů.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124701"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití vícesměrového vysílání k nasazení Windows přes síť s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vícesměrové vysílání je metoda optimalizace sítě, kterou můžete použít, pokud více klientů bude pravděpodobně stahovat stejnou bitovou kopii operačního systému ve stejnou dobu. Pokud používáte vícesměrové vysílání, více počítačů současně stáhne bitovou kopii operačního systému jako vícesměrové vysílání distribučním bodem. Toto chování je místo každého klienta, který stahuje kopii Image přes samostatné připojení z distribučního bodu.

Nasaďte operační systémy přes síť pomocí vícesměrového vysílání v následujících scénářích nasazení operačního systému:

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)

Proveďte kroky v jednom z těchto scénářů nasazení operačního systému. Pak použijte následující části k podpoře vícesměrového vysílání.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a>Konfigurace distribučních bodů pro vícesměrové vysílání

Pokud chcete používat vícesměrové vysílání, nakonfigurujte aspoň jeden distribuční bod, který bude podporovat vícesměrové vysílání. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

Seznam portů vyžadovaných k podpoře vícesměrového vysílání najdete v tématu [porty](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## <a name="prepare-an-os-image-for-multicast"></a>Příprava image operačního systému pro vícesměrové vysílání

Je nutné nakonfigurovat bitovou kopii operačního systému pro podporu vícesměrového vysílání. Další informace najdete v tématu [Příprava image operačního systému pro nasazení vícesměrového vysílání](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Nasazení pořadí úkolů

Nasaďte operační systém do cílové kolekce. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="next-steps"></a>Další kroky

[Uživatelská prostředí pro nasazení operačního systému](../understand/user-experience.md)
