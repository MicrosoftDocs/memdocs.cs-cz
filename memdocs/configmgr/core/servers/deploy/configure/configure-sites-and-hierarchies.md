---
title: Konfigurace lokalit a hierarchií
titleSuffix: Configuration Manager
description: V tomto kontrolním seznamu se ujistěte, že máte v úvahu nejběžnější konfigurace, které mají vliv na lokality i hierarchie.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720993"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Konfigurace lokalit a hierarchií pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po instalaci první lokality Configuration Manager nebo přidání dalších lokalit do hierarchie nástroje použijte tento kontrolní seznam k zajištění, že budete uvažovat o nejběžnějších konfiguracích, které mají vliv na lokality i hierarchie.  

Následující poznámky ke konfiguraci platí pro většinu nasazení:  

- Některé možnosti jsou navzájem sestaveny, například zjišťování doménové struktury služby Active Directory, hranice a skupiny hranic.  

- Některé konfigurace mají výchozí hodnoty, které se mají použít bez změny konfigurace, a to aspoň po spuštění.  

- Další konfigurace, jako jsou skupiny hranic a skupiny distribučních bodů, je potřeba před použitím nakonfigurovat.  

| Akce | Podrobnosti |  
|------------|-------------|  
| Konfigurace správy na základě rolí | Oddělením přiřazení správy můžete určit, kteří uživatelé s právy pro správu mohou zobrazovat a spravovat různé objekty a data v prostředí Configuration Manager.<br /><br /> Konfigurace pro správu na základě rolí jsou sdílené se všemi lokalitami v hierarchii.   <br/><br/>Další informace najdete v tématu [Konfigurace správy na základě rolí](configure-role-based-administration.md). |  
| Publikování dat lokality na Active Directory Domain Services | Umožňuje klientům snadno vyhledat služby a efektivně využívat prostředky webu.<br /><br /> Nejprve [rozšíříte schéma služby Active Directory](../../../plan-design/network/extend-the-active-directory-schema.md). Pak každou lokalitu nakonfigurovat pro [publikování dat lokality](publish-site-data.md) zvlášť |  
| Konfigurace spojovacího bodu služby | Naplánujte instalaci a konfiguraci spojovacího bodu služby v lokalitě nejvyšší úrovně ve vaší hierarchii. Další informace najdete v tématu [o spojovacím bodu služby](about-the-service-connection-point.md). |  
| Přidání rolí systému lokality | Nainstalujte jednu nebo více dalších rolí systému lokality pro jednotlivé lokality. Další informace najdete v tématu [Přidání rolí systému lokality](add-site-system-roles.md). |  
| Konfigurace hranic lokality a skupin hranic | Zadejte hranice definující síťová umístění v intranetu, která můžou obsahovat zařízení, která chcete spravovat. Poté nakonfigurujte skupiny hranic tak, aby klienti v těchto síťových umístěních mohli najít prostředky Configuration Manager. Další informace najdete v tématu [definice hranic lokality a skupin hranic](define-site-boundaries-and-boundary-groups.md). |  
| Konfigurace skupin distribučních bodů | Nakonfigurujte logické skupiny distribučních bodů, aby bylo snazší spravovat nasazení. Další informace najdete v tématu [Správa skupin distribučních bodů](install-and-configure-distribution-points.md#bkmk_manage). |  
| Spuštění zjišťování | Spusťte zjišťování k vyhledání prostředků ve vaší síti, včetně síťové infrastruktury, zařízení a uživatelů.<br /><br /> Další informace najdete v tématu [spuštění zjišťování](run-discovery.md). |  
| Přidání redundance a kapacity pro správce | Nainstalujte další poskytovatele serveru SMS a konzoly Configuration Manager, abyste správcům rozšířili kapacitu pro správu vaší infrastruktury:<br /><br /> **Nainstalujte další poskytovatele serveru SMS** , abyste zajistili redundanci připojení ke konzole a rozhraní API k lokalitě. Další informace najdete v tématu [Správa poskytovatele serveru SMS](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Nainstalujte další Configuration Manager konzol** pro poskytnutí přístupu dalším uživatelům s právy pro správu. Další informace najdete v tématu [instalace konzol Configuration Manager](../install/install-consoles.md). |  
| Konfigurace součástí lokality | Nakonfigurujte součásti lokality v jednotlivých lokalitách a upravte chování rolí systému lokality a vytváření sestav stavu lokality. Další informace najdete v tématu [součásti lokality](site-components.md). |  
| Vytvoření vlastních kolekcí | Pomocí informací, které lokalita zjistí o zařízeních a uživatelích, vytvořte vlastní kolekce objektů, abyste zjednodušili budoucí úlohy správy. Další informace najdete v tématu [vytváření kolekcí](../../../clients/manage/collections/create-collections.md). |  
| Konfigurace nastavení pro správu nasazení s vysokým rizikem | Nakonfigurujte v lokalitě nastavení, která upozorní správce při vytváření vysoce rizikového nasazení. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../manage/settings-to-manage-high-risk-deployments.md). |  
| Konfigurace replik databáze pro body správy | Nakonfigurujte repliku databáze, aby se snížilo zatížení procesoru, které je umístěno na serveru databáze lokality, podle bodů správy, a to tak, aby byly požadavky služby od klientů. Další informace najdete v tématu [repliky databáze pro body správy](database-replicas-for-management-points.md). |  
| Konfigurace skupiny dostupnosti Always On SQL Server | Nakonfigurujte skupiny dostupnosti jako řešení pro vysokou dostupnost a zotavení po havárii pro hostování databáze lokality v primárních lokalitách a lokalitě centrální správy. Další informace najdete v tématu [SQL Server AlwaysOn pro databázi lokality s vysokou dostupností](sql-server-alwayson-for-a-highly-available-site-database.md). |  
| Úprava replikace mezi lokalitami | Další informace o těchto tématech najdete v tématu [přenos dat mezi lokalitami](../../../plan-design/hierarchy/data-transfers-between-sites.md) :<br /><br /> Konfigurace [replikace na základě souborů](../../../plan-design/hierarchy/file-based-replication.md) mezi sekundárními lokalitami<br /><br /> Konfigurace [odkazů replikace databáze](../../../plan-design/hierarchy/database-replication.md)<br /><br /> Konfigurace [distribuovaných zobrazení](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| Konfigurovat servery lokality v pasivním režimu | Počínaje verzí 1806 nakonfigurujte server lokality v pasivním režimu pro každou primární lokalitu a lokalitu centrální správy. Tato funkce poskytuje vysoce dostupný server lokality. Další informace najdete v tématu [Vysoká dostupnost serveru lokality](site-server-high-availability.md). |  
