---
title: Upgrade na Windows 10
titleSuffix: Configuration Manager
description: Naučte se používat Configuration Manager k upgradu operačního systému z Windows 7 nebo novějšího na Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8bfb45ba835851c33d6017f7f0a884bd2c1e9421
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429323"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Upgrade Windows na nejnovější verzi pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje kroky v Configuration Manager k upgradu operačního systému v počítači. Můžete vybírat z různých metod nasazení, jako je samostatné médium nebo Centrum softwaru. Scénář místního upgradu má následující funkce:  

- Upgraduje operační systém na Windows 10 nebo Windows Server 2016 a novější.

- Zachovává aplikace, nastavení a uživatelská data v počítači.

- Nemá žádné externí závislosti, jako je například Windows ADK.

- Je rychlejší a pružnější než tradiční nasazení operačního systému

> [!Note]  
> Pořadí úkolů místního upgradu Windows 10 podporuje nasazení do internetových klientů spravovaných prostřednictvím [brány pro správu cloudu](../../core/clients/manage/cmg/plan-cloud-management-gateway.md). Tato možnost umožňuje vzdáleným uživatelům snadněji upgradovat na Windows 10, aniž by se museli připojit k intranetu. Další informace najdete v tématu [nasazení místního upgradu Windows 10 přes CMG](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Podporované verze

### <a name="upgrade-version"></a>Verze upgradu

Vytvořit pouze balíčky s upgradem operačního systému pro upgrade na následující verze operačního systému:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Původní verze

Aby bylo možné cílit na pořadí úkolů upgradu operačního systému, zařízení musí spustit jednu z následujících verzí operačního systému:

#### <a name="windows-client"></a>Klient Windows

- Windows 7
- Windows 8.1
- Starší verze Windows 10. Například můžete upgradovat Windows 10 verze 1809 na Windows 10, verze 1903.  

Další informace najdete v tématu věnovaném [cestám upgradu Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths).

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- Starší verze systému Windows Server 2016
- Starší verze systému Windows Server 2019

Další informace o podporovaných cestách upgradu Windows serveru najdete v článku věnovaném [podporovaným cestám upgradu Windows serveru 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) a [centru upgradu Windows serveru](https://aka.ms/upgradecenter).


## <a name="plan"></a><a name="BKMK_Plan"></a>Rozhraní  

### <a name="task-sequence-requirements-and-limitations"></a>Požadavky a omezení pořadí úkolů

Přečtěte si následující požadavky a omezení pro pořadí úkolů, abyste mohli upgradovat operační systém, abyste se ujistili, že vyhovuje vašim potřebám:  

- Přidejte pouze kroky pořadí úloh, které se vztahují k základní úloze upgradu operačního systému. Mezi tyto kroky patří především instalace balíčků, aplikací nebo aktualizací. Použijte taky kroky, které spouštějí příkazové řádky, PowerShell nebo nastavují dynamické proměnné.  

- Zkontrolujte ovladače a aplikace, které jsou nainstalované na počítačích. Před nasazením pořadí úkolů upgradu zajistěte, aby byly ovladače kompatibilní se systémem Windows 10.  

Následující úkoly nejsou kompatibilní s místním upgradem. Vyžadují, abyste používali tradiční nasazení operačního systému:  

- Změna členství počítače v doméně nebo aktualizace místní skupiny Administrators.  

- Implementace zásadní změny v počítači, například:

  - Změna diskových oddílů
  - Změna systémové architektury z x86 na x64
  - Implementace rozhraní UEFI. (Další informace o možné možnosti najdete v tématu [převedení ze systému BIOS na rozhraní UEFI během místního upgradu](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).)
  - Úprava základního jazyka operačního systému  

- Máte vlastní požadavky, včetně použití vlastní základní image, použití šifrování disku od jiných výrobců nebo offline operací prostředí WinPE.  

### <a name="infrastructure-requirements"></a>Požadavky na infrastrukturu  

Jediným předpokladem pro scénář upgradu je dostupnost distribučního bodu. Distribuujte balíček s upgradem operačního systému a všechny další balíčky, které zahrnete do pořadí úkolů. Další informace naleznete v části [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurace  

### <a name="prepare-the-os-upgrade-package"></a>Příprava balíčku s upgradem operačního systému  

Balíček s upgradem Windows 10 obsahuje zdrojové soubory potřebné k upgradu operačního systému na cílovém počítači. Balíček s upgradem musí mít stejnou edici, architekturu a jazyk jako klienti, které upgradujete. Další informace najdete v tématu [Správa balíčků s upgradem operačního systému](../get-started/manage-operating-system-upgrade-packages.md).  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Vytvoření pořadí úkolů pro upgrade operačního systému  

Pomocí kroků v části [Vytvoření pořadí úkolů upgradujte operační systém](create-a-task-sequence-to-upgrade-an-operating-system.md) a automatizujte tak upgrade operačního systému.  

> [!NOTE]  
> Chcete-li vytvořit pořadí úkolů pro upgrade operačního systému na systém Windows 10, obvykle použijte postup v části [Vytvoření pořadí úkolů pro upgrade operačního systému](create-a-task-sequence-to-upgrade-an-operating-system.md). Pořadí úkolů zahrnuje krok **upgradu operačního systému** , stejně jako další doporučené kroky a skupiny pro zpracování kompletního procesu upgradu.
>
> Můžete vytvořit vlastní pořadí úkolů a přidat krok [upgradu operačního systému](../understand/task-sequence-steps.md#BKMK_UpgradeOS) . Tento krok je jediným nutným pro upgrade operačního systému na Windows 10. Pokud zvolíte tuto metodu, chcete-li dokončit upgrade, přidejte také krok [restartovat počítač](../understand/task-sequence-steps.md#BKMK_RestartComputer) po kroku **upgradu operačního systému** . Nezapomeňte použít nastavení **Aktuálně nainstalované výchozí operační systém** k restartování počítače do NAINSTALOVANÉho operačního systému a ne do prostředí Windows PE.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a>Nasazení  

K nasazení operačního systému použijte jednu z následujících metod nasazení:  

- [Použití Centra softwaru k nasazení Windows přes síť](use-software-center-to-deploy-windows-over-the-network.md)  

- [Nasazení Windows pomocí samostatného média bez použití sítě](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > Při použití samostatného média musíte do pořadí úkolů přidat spouštěcí bitovou kopii. Tato konfigurace zajistí, aby bylo pořadí úloh dostupné v průvodci médii pořadí úloh.


## <a name="monitor"></a>Monitorování  

Informace o monitorování nasazení pořadí úkolů pro upgrade operačního systému najdete v tématu [monitorování nasazení operačního systému](monitor-operating-system-deployments.md).  
