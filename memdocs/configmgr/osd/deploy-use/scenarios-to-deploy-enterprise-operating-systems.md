---
title: Scénáře nasazení podnikových operačních systémů
titleSuffix: Configuration Manager
description: Přečtěte si o několika scénářích nasazení podnikových operačních systémů pomocí Configuration Manager.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8304ba7384eba2fc7bfa41d4caf5a256380931c5
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546633"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Scénáře nasazení podnikových operačních systémů pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager jsou k dispozici následující scénáře nasazení operačního systému:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Upgrade systému Windows na nejnovější verzi
Tento scénář upgraduje operační systém na počítačích, na kterých je aktuálně spuštěný systém Windows 7, Windows 8.1 nebo Windows 10. Proces upgradu udržuje v počítači aplikace, nastavení a uživatelská data. Neexistují žádné externí závislosti, jako je například Windows ADK. Tento proces může být rychlejší a pružnější než tradiční nasazení operačního systému.  

Další informace najdete v tématu [upgrade Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md).

#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot pro existující zařízení
<!--3607717, fka 1358333-->
Počínaje verzí 1810 je k dispozici pro existující zařízení Windows autopilot pro stávající zařízení s Windows 10 verze 1809 nebo novější. Tato funkce umožňuje obnovení image a zřízení zařízení se systémem Windows 7 pro uživatele se systémem Windows autopilot na základě jednoho Configuration Managerho pořadí úloh.

Další informace najdete v tématu [Windows Autopilot pro existující zařízení](../../../autopilot/existing-devices.md).

#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aktualizace existujícího počítače na novou verzi Windows
Tento scénář oddíly a formátuje (maže) existující počítač a instaluje do počítače nový operační systém. Po instalaci operačního systému můžete migrovat nastavení a uživatelská data.  

Další informace najdete v tématu [Aktualizace existujícího počítače s novou verzí Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Instalace nové verze Windows do nového počítače (holý počítač)
Tento scénář instaluje operační systém na nový počítač. Jedná se o novou instalaci operačního systému a neobsahuje žádná nastavení ani migraci dat uživatele.  

Další informace najdete v tématu [instalace nové verze Windows na nový počítač (holý počítač)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Nahrazení existujícího počítače a nastavení přenosu
Tento scénář instaluje operační systém na nový počítač. Volitelně můžete migrovat uživatelská nastavení a data ze starého počítače na nový počítač.  

Další informace najdete v tématu [nahrazení existujícího počítače a nastavení přenosů](replace-an-existing-computer-and-transfer-settings.md).


