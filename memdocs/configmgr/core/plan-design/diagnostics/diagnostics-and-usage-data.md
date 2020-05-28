---
title: Data o využití a diagnostika
titleSuffix: Configuration Manager
description: Seznamte se s daty o využití a diagnostiku, kterou Configuration Manager shromažďuje samo o sobě.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904400"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Data o využití a Diagnostika pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager shromažďuje data o využití a diagnostiku o sobě, což společnost Microsoft používá ke zlepšení prostředí pro instalaci, kvality a zabezpečení budoucích verzí.  

Každá Configuration Manager hierarchie umožňuje data o využití a diagnostiku. Skládá se z SQL Server dotazů, které se spouští každý týden v každé primární lokalitě a v lokalitě centrální správy (CAS). Když hierarchie používá certifikační autority, podřízené primární lokality replikují svá data do těchto certifikačních autorit. V lokalitě nejvyšší úrovně v hierarchii [spojovací bod služby](../../servers/deploy/configure/about-the-service-connection-point.md) odesílá tyto informace při kontrole aktualizací. Pokud je spojovací bod služby v režimu offline, přenášíte informace pomocí [Nástroje pro připojení služby](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager shromažďuje data pouze z databáze SQL serveru lokality a neshromažďuje data přímo z klientů nebo serverů lokality.  

Další informace najdete v tématu [prohlášení o zásadách ochrany osobních údajů společnosti Microsoft](https://privacy.microsoft.com/privacystatement).  

> [!div class="nextstepaction"]
> [Jak Microsoft používá data o využití a diagnostiku](how-diagnostics-and-usage-data-is-used.md)
