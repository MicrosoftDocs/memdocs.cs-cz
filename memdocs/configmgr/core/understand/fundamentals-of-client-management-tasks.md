---
title: Základy správy klientů
titleSuffix: Configuration Manager
description: Přečtěte si o úlohách, které spouštíte pro správu Configuration Manager klientů.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722862"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>Základy úloh správy klientů pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po instalaci Configuration Manager klientů existuje několik úloh, které spustíte pro správu klientů.  Některé úlohy jsou spouštěny z konzoly Configuration Manager. Další úlohy jsou spouštěny z klientské aplikace Configuration Manager. Klientská aplikace Configuration Manager je nainstalována spolu s klientským Configuration Managerm softwaru.

## <a name="configuration-manager-console-tasks"></a>Configuration Manager úlohy konzoly
 V konzole Configuration Manager můžete provádět různé úlohy správy klientů:  

-   Nasazovat aplikace, aktualizace softwaru, skripty údržby a operační systémy. Nakonfigurujte instalaci na konkrétní datum a čas, zpřístupněte software uživatelům, kteří si je vyžádali, a nakonfigurujte aplikace, které chcete odinstalovat.  

-   Zajistit ochranu počítačů před malwarem či bezpečnostními hrozbami a oznamování zjištěných problémů.  

-   Definujte nastavení konfigurace klienta, které chcete monitorovat, a opravte je, pokud nedodržují předpisy.  

-   Shromažďovat informace o inventáři hardwaru a softwaru včetně monitorování a odsouhlasení informací o licencích od společnosti Microsoft.  

-   Řešit problémy s počítači pomocí vzdáleného řízení.  

-   Implementovat nastavení řízení spotřeby pro správu a monitorování spotřeby energie počítačů.  

Konzola Configuration Manager sleduje předchozí úlohy téměř v reálném čase. Informace o oznámeních a stavu jednotlivých úloh jsou k dispozici v konzole Configuration Manager. Pokud chcete zachytit data a historické trendy, využijte integrované možnosti vytváření sestav SQL Server Reporting Services. Klienti odesílají podrobnosti do lokality jako stav klienta.  Informace o stavu klienta poskytují údaje o stavu klienta a aktivitě klienta a zobrazují se v konzole nástroje nebo pomocí předdefinovaných sestav pro Configuration Manager. Tato data pomáhají identifikovat počítače, které nereagují, a v některých případech problémy jsou automaticky opraveny.  

 Další informace o úlohách správy pro klienty najdete v tématech [Správa klientů](../../core/clients/manage/manage-clients.md) a [Správa klientů pro servery se systémy Linux a UNIX](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Informace o používání sestav najdete v tématu   
            [Seznámení s vytvářením sestav](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Klientská aplikace Configuration Manager  
 Když nainstalujete klientský software Configuration Manager, je klientská aplikace Configuration Manager taky nainstalovaná. Na rozdíl od centra softwaru je klientská aplikace Configuration Manager navržená pro technickou podporu, ale pro koncového uživatele. Některé možnosti konfigurace vyžadují místní oprávnění ke správě a většina možností vyžaduje technické znalosti o tom, jak Configuration Manager klientská aplikace funguje. Aplikaci můžete použít k provádění následujících úloh v počítači klienta:  

-   Zobrazení vlastností klienta, jako je číslo sestavení, přiřazená lokalita, bod správy, se kterým komunikuje, a informace o tom, zda klient používá certifikát infrastruktury veřejných klíčů (PKI) nebo certifikát podepsaný svým držitelem.  

-   Ověřte, že klient úspěšně stáhl zásady klienta po prvním dokončení instalace klienta. Ověřte také, zda jsou nastavení klienta povolena nebo zakázána podle očekávání, podle nastavení klienta, které jsou konfigurovány v konzole Configuration Manager.  

-   Spusťte akce klienta. Například Stáhněte zásady klienta, pokud došlo k nedávné změně konfigurace v konzole Configuration Manager a nechcete čekat do dalšího naplánovaného času.  

-   Ručně přiřaďte klienta k Configuration Manager lokalitě nebo se pokuste najít web. Pak zadejte příponu DNS (Domain Name System) pro body správy, které publikují na serveru DNS.  

-   Nakonfigurujte mezipaměť klienta, která dočasně ukládá soubory. Pokud budete potřebovat více místa na disku pro instalaci softwaru, odstraňte soubory v mezipaměti.  

-   Konfigurace nastavení pro internetovou správu klientů.  

-   Zobrazení standardních hodnot konfigurace nasazených u klienta, iniciace vyhodnocení shody a zobrazení zpráv o kompatibilitě.  
