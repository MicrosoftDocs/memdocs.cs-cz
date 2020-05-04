---
title: Monitorování stavu nasazení klienta
titleSuffix: Configuration Manager
description: Monitorovat stav nasazení klienta v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713314"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Postup sledování stavu nasazení klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení klientů v rámci vaší lokality trvá určitou dobu a některé instalace nejsou napoprvé úspěšné. Konzola Configuration Manager nabízí způsob, jak v reálném čase sledovat nasazení klientů v rámci kolekce pomocí hlášení stavu nasazení klienta.  

> [!NOTE]  
>  Nejlepší a nejspolehlivější způsob, jak monitorovat nasazení klientů, je pomocí konzoly Configuration Manager (jak je popsáno v tomto článku). Oddíl **Stav klienta** pracovního prostoru **Sledování** v konzole poskytuje stav nasazení klientů přesně a v reálném čase. Můžete sledovat nasazení klientů pomocí jiných nástrojů, jako je například Správce serveru v systému Windows Server nebo System Center Operations Manager, ale můžete obdržet výstrahy z běžné aktivity instalace klientů. Kvůli způsobu, jakým se program pro instalaci klientů (CCMSetup.exe) spouští v různých prostředích, mohou tyto jiné nástroje generovat falešné výstrahy a upozornění, které přesně neodrážejí stav nasazení klientů.  

 V pracovním prostoru **Sledování** konzoly můžete sledovat následující stavy nasazení klientů uskutečněných v rámci kolekce, kterou zadáte:  

- Odpovídající  

- Probíhá  

- Nevyhovuje  

- Failed  

- Není známo  

  Configuration Manager hlásí nasazení pro produkční klienty nebo předprodukční klienty. Konzola nástroje Configuration Manager také obsahuje graf neúspěšných nasazení klientů za zadanou dobu, což umožňuje zjistit, jestli akce, které podnikáte k vyřešení problémů nasazení, zlepšují úspěšnost nasazení v čase.  

## <a name="to-monitor-client-deployments"></a>Monitorování nasazení klientů  

- V konzole Configuration Manager klikněte na **sledování** > **stav klienta**.  

- Klikněte na **Nasazení produkčního klienta** nebo **Nasazení předprodukčního klienta**, v závislosti na verzi klienta, kterého chcete sledovat.  

- Zkontrolujte grafy stavu nasazení klientů a selhání nasazení klientů.  

- Chcete-li změnit rozsah sestavy, klikněte na tlačítko **Procházet...** a vyberte jinou kolekci.  

  Další informace o předprodukčních nasazeních klientů najdete v tématu [testování upgradu klienta v předprodukční kolekci](../../../core/clients/manage/upgrade/test-client-upgrades.md).

  > [!NOTE]
  > Stav nasazení v počítačích hostujících role systému lokality v předprodukční kolekci může být hlášen jako **nedodržující předpisy** i v případě, že byl klient úspěšně nasazen. Když zvýšíte úroveň klienta do produkčního prostředí, stav nasazení bude uveden správně.   

  Pokud chcete monitorovat stav nasazených klientů, přečtěte si téma [Postup monitorování klientů](../../../core/clients/manage/monitor-clients.md) .  

  Pomocí sestav Configuration Manager můžete zjistit další informace o stavu klientů v lokalitě nástroje. Další informace o spouštění sestav najdete v tématu [Úvod do vytváření sestav](../../servers/manage/introduction-to-reporting.md).  
