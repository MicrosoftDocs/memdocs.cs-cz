---
title: Aktualizace operačního systému stávajícího počítače
titleSuffix: Configuration Manager
description: K rozdělení a zformátování stávajícího počítače a instalaci nového operačního systému do počítače můžete použít několik metod v Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b635301d9d5bd8a0fb81771255acddb21097f23b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124898"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aktualizace existujícího počítače na novou verzi Windows

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager rozdělit a naformátovat existující počítač a pak nainstalovat nový operační systém. Tento proces se někdy označuje jako obnova *obrazu* nebo *vymazání a načtení*. V tomto scénáři si můžete vybrat z mnoha různých metod nasazení, jako je PXE, spouštěcí médium nebo Centrum softwaru. Můžete také použít bod migrace stavu k uložení nastavení a pak je obnovit do nového operačního systému.

Pokud chcete zvolit správný scénář nasazení operačního systému, přečtěte si téma [scénáře nasazení podnikových operačních systémů](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a>Rozhraní  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Plánování a implementace požadavků na infrastrukturu

Před nasazením operačního systému je nutné, aby bylo provedeno několik požadavků na infrastrukturu. Mezi tyto požadavky patří Windows ADK, Nástroj pro migraci uživatelských souborů a nastavení (USMT) a služba pro nasazení systému Windows (WDS). Další informace najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Nainstalovat bod migrace stavu

Pokud chcete zaznamenat nastavení z existujícího počítače a potom obnovit nastavení v novém operačním systému, zvažte použití bodu migrace stavu. Další informace najdete v části [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurace  

### <a name="prepare-a-boot-image"></a>Příprava spouštěcí image

Spouštěcí image spustí počítač v prostředí Windows PE. Windows PE je minimální operační systém s omezenými součástmi a službami. V systému Windows PE může Configuration Manager v počítači nainstalovat plný operační systém Windows.

Další informace najdete v následujících článcích:

- [Správa spouštěcích imagí](../get-started/manage-boot-images.md)

- [Přizpůsobení spouštěcích imagí](../get-started/customize-boot-images.md)

- [Distribuovat obsah](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Příprava image operačního systému

Bitová kopie operačního systému obsahuje soubory potřebné k instalaci operačního systému do cílového počítače.

Další informace najdete v následujících článcích:

- [Správa imagí operačního systému](../get-started/manage-operating-system-images.md)

- [Distribuovat obsah](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Vytvoření pořadí úkolů pro nasazení operačního systému

K automatizaci instalace operačního systému použijte pořadí úkolů. V závislosti na vybrané metodě nasazení může být potřeba zvážit další aspekty pořadí úkolů.

Další informace najdete v následujících článcích:

- [Vytvoření pořadí úkolů pro instalaci operačního systému](create-a-task-sequence-to-install-an-operating-system.md)

- [Správa stavu uživatele](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a>Nasazení

- K nasazení operačního systému použijte jednu z následujících metod nasazení:  

  - [Použití technologie PXE k nasazení Windows přes síť](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Použití vícesměrového vysílání k nasazení Windows přes síť](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Vytvoření image pro výrobce OEM v továrně nebo místním úložišti](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Nasazení Windows pomocí samostatného média bez použití sítě](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Použití spouštěcího média k nasazení Windows přes síť](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Použití Centra softwaru k nasazení Windows přes síť](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitorování  

Další informace najdete v tématu [monitorování nasazení operačního systému](monitor-operating-system-deployments.md).  

> [!Note]
> Při obnovení bitové kopie zařízení UEFI vytvoří Správce spouštění systému Windows nový záznam v zaváděcím zavaděči. Toto chování je nejužitečnější při opakovaném obnovení obrazu zařízení, jako je například v testovacím prostředí nebo v laboratoři studenta. Obecně to nemá vliv na výkon ani využití zařízení. Pokud se seznam příliš zvětší, můžou některá konkrétní hardwarová zařízení narazit na funkční problémy. Například nespouštíte externí jednotku USB nebo nemůžete vybrat aktuální spouštěcí položku ze seznamu. Pomocí příkazu Windows **bcdedit** vymažte nepoužívané spouštěcí položky. Další informace najdete v tématu [bcdedit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
