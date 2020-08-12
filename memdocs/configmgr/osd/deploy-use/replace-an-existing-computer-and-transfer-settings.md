---
title: Nahrazení existujícího počítače a nastavení přenosu
titleSuffix: Configuration Manager
description: V Configuration Manager vyberte z metod nasazení, jako je spouštěcí médium, vícesměrové vysílání nebo Centrum softwaru, k nahrazení existujícího počítače novým počítačem.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 860ee3aeb255921ccd8bf3b1695a9647b514752f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124864"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Nahrazení existujícího počítače a nastavení přenosu pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma poskytuje obecné kroky Configuration Manager k nahrazení existujícího počítače novým počítačem. V tomto scénáři si můžete vybrat z mnoha různých metod nasazení, jako je spouštěcí médium, vícesměrové vysílání a Centrum softwaru. Můžete taky nainstalovat bod migrace stavu pro ukládání nastavení a jejich obnovení v novém operačním systému po jeho instalaci. Pokud si nejste jistí, jestli se jedná o správný scénář nasazení operačního systému, přečtěte si téma [scénáře nasazení podnikových operačních systémů](scenarios-to-deploy-enterprise-operating-systems.md).  

 Následující části vám pomůžou aktualizovat existující počítač pomocí nové verze Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Rozhraní  

-   **Plánování a implementace požadavků na infrastrukturu**  

     Před nasazením operačních systémů, jako je například Windows ADK, Nástroj pro migraci uživatelských souborů a nastavení (USMT), služba pro nasazení systému Windows (WDS), podporované konfigurace pevného disku atd., je nutné provést několik různých požadavků na infrastrukturu. Další informace najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) .  

-   **Instalace bodu migrace stavu (vyžadovaná jenom při přenosu nastavení)**  

     Když chcete zaznamenat nastavení z existujícího počítače a potom obnovit nastavení v novém operačním systému, musíte nainstalovat bod migrace stavu. Další informace najdete v části [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurace  

1.  **Příprava spouštěcí image**  

     Spouštěcí image spustí počítač v prostředí Windows PE (minimální operační systém s omezenými součástmi a službami), které pak může na počítač nainstalovat úplný operační systém Windows. Při nasazení operačních systémů je potřeba vybrat spouštěcí image, která se má použít, a distribuovat ji do distribučního bodu. K přípravě spouštěcí image použijte následující postupy:  

    -   Další informace o spouštěcích bitových kopiích najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

    -   Další informace o tom, jak přizpůsobit spouštěcí image, najdete v tématu [Přizpůsobení spouštěcích bitových kopií](../get-started/customize-boot-images.md).  

    -   Proveďte distribuci spouštěcí image do distribučních bodů. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Příprava image operačního systému**  

     Image operačního systému obsahuje soubory potřebné k instalaci operačního systému na cílovém počítači. K přípravě image operačního systému použijte následující postupy:  

    -   Další informace o tom, jak vytvořit bitovou kopii operačního systému, najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).  

    -   Distribuce image operačního systému do distribučních bodů. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Vytvoření pořadí úkolů pro nasazení operačního systému přes síť**  

     Pořadí úkolů použijte k automatizaci instalace operačního systému přes síť. Pomocí postupu v části [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md) vytvořte pořadí úkolů pro nasazení operačního systému. V závislosti na vybrané metodě nasazení může být potřeba zvážit další aspekty pořadí úkolů.  

    > [!NOTE]  
    >  Pokud v tomto scénáři zaznamenáte a obnovíte uživatelská nastavení a soubory, můžete používat bod migrace stavu nebo ukládat soubory lokálně. Další informace najdete v tématu [Správa stavu uživatele](../get-started/manage-user-state.md).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Nasazení  

-   K nasazení operačního systému použijte jednu z následujících metod nasazení:  

    -   [Použití Centra softwaru k nasazení Windows přes síť](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Použití spouštěcího média k nasazení Windows přes síť](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Použití vícesměrového vysílání k nasazení Windows přes síť](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Vytvoření image pro výrobce OEM v továrně nebo místním úložišti](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Monitorování  

-   **Monitorování nasazení pořadí úkolů**  

     Informace o monitorování nasazení pořadí úkolů pro instalaci operačního systému najdete v tématu [monitorování nasazení operačního systému](monitor-operating-system-deployments.md).  
