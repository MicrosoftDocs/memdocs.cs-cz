---
title: Nainstalovat systém Windows do nového počítače
titleSuffix: Configuration Manager
description: Použijte Configuration Manager k instalaci operačního systému na nový počítač (holý počítač) pomocí technologie PXE, OEM nebo samostatného média.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb880b6cb6f45de06b602bc9caa8ca7b98022d5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125078"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Instalace nové verze Windows na nový počítač (holý počítač) s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma poskytuje obecné kroky Configuration Manager k instalaci operačního systému na nový počítač. V tomto scénáři si můžete vybírat z řady různých metod nasazení, jako je PXE, OEM nebo spouštěcí médium. Pokud si nejste jistí, jestli se jedná o správný scénář nasazení operačního systému, přečtěte si téma [scénáře nasazení podnikových operačních systémů](scenarios-to-deploy-enterprise-operating-systems.md).  

Následující části vám pomůžou aktualizovat existující počítač pomocí nové verze Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Rozhraní  

-   **Plánování a implementace požadavků na infrastrukturu**  

     Aby bylo možné nasadit operační systémy, jako je například Windows ADK, služba pro nasazení systému Windows (WDS), podporované konfigurace pevného disku atd., je nutné, aby byly k dispozici různé požadavky na infrastrukturu. Další informace najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurace  

1.  **Příprava spouštěcí image**  

     Spouštěcí image spustí počítač v prostředí Windows PE (minimální operační systém s omezenými součástmi a službami), které pak může na počítač nainstalovat úplný operační systém Windows.   Při nasazení operačních systémů je potřeba vybrat spouštěcí image, která se má použít, a distribuovat ji do distribučního bodu. K přípravě spouštěcí image použijte následující postupy:  

    -   Další informace o spouštěcích bitových kopiích najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

    -   Další informace o tom, jak přizpůsobit spouštěcí image, najdete v tématu [Přizpůsobení spouštěcích bitových kopií](../get-started/customize-boot-images.md).  

    -   Proveďte distribuci spouštěcí image do distribučních bodů. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Příprava image operačního systému**  

     Image operačního systému obsahuje soubory potřebné k instalaci operačního systému na cílovém počítači. K přípravě image operačního systému použijte následující postupy:  

    -   Další informace o tom, jak vytvořit bitovou kopii operačního systému, najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).

    -   Distribuce image operačního systému do distribučních bodů. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Nové instalace systému Windows lze také provést ze zdrojových instalačních souborů prostřednictvím balíčků s upgradem operačního systému, ale místo toho použijte image operačního systému, jako je například **install. wim** .
    >
    > Nasazení nových instalací Windows přes balíčky s upgradem operačního systému se pořád podporuje, ale závisí na ovladačích, které jsou s touto metodou kompatibilní. Při instalaci systému Windows z balíčku pro upgrade operačního systému jsou ovladače nainstalovány i v systému Windows PE, a to pouhým vložením v prostředí Windows PE. Některé ovladače nejsou kompatibilní s instalací v prostředí Windows PE. Pokud nejsou ovladače kompatibilní s instalací v prostředí Windows PE, použijte místo toho bitovou kopii operačního systému.  

3.  **Vytvoření pořadí úkolů pro nasazení operačního systému přes síť**  

     Pořadí úkolů použijte k automatizaci instalace operačního systému přes síť. Pomocí postupu v části [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md) vytvořte pořadí úkolů pro nasazení operačního systému. V závislosti na vybrané metodě nasazení může být potřeba zvážit další aspekty pořadí úkolů.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Nasazení  

-   K nasazení operačního systému použijte jednu z následujících metod nasazení:  

    -   [Použití technologie PXE k nasazení Windows přes síť](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Použití vícesměrového vysílání k nasazení Windows přes síť](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Vytvoření image pro výrobce OEM v továrně nebo místním úložišti](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Nasazení Windows pomocí samostatného média bez použití sítě](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Použití spouštěcího média k nasazení Windows přes síť](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitorování  

-   **Monitorování nasazení pořadí úkolů**  

     Informace o monitorování nasazení pořadí úkolů pro instalaci operačního systému najdete v tématu [monitorování nasazení operačního systému](monitor-operating-system-deployments.md).  
