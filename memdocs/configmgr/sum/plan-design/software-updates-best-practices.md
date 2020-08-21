---
title: Osvědčené postupy pro aktualizace softwaru
titleSuffix: Configuration Manager
description: Tyto osvědčené postupy použijte pro aktualizace softwaru v nástroji Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 3a48ce044f3d1aecbebf2ba93e936dd34b904140
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696634"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Osvědčené postupy pro aktualizace softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje osvědčené postupy pro aktualizace softwaru v nástroji Configuration Manager. Tyto informace jsou seřazené podle osvědčených postupů pro počáteční instalaci a pro probíhající operace.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> Osvědčené postupy pro instalaci  

Při instalaci aktualizací softwaru v nástroji Configuration Manager použijte následující osvědčené postupy.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> Použití sdílené databáze služby WSUS pro body aktualizace softwaru  

Při instalaci více než jednoho bodu aktualizace softwaru v primární lokalitě použijte stejnou databázi WSUS pro všechny body aktualizace softwaru ve stejné doménové struktuře Active Directory. Pokud sdílíte stejnou databázi, významně to snižuje riziko, ale zcela eliminuje vliv na výkon klienta a sítě, ke kterému může dojít při přepnutí klientů na nový bod aktualizace softwaru. K rozdílové kontrole stále dochází, když klient přejde do nového bodu aktualizace softwaru, který sdílí databázi se starým bodem aktualizace softwaru, ale vyhledávání je mnohem menší než v případě, že má server WSUS svou vlastní databázi. Další informace o přepínání bodů aktualizace softwaru najdete v tématu [Přepínání bodů aktualizace softwaru](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Pokud používáte sdílenou databázi WSUS pro body aktualizace softwaru, sdílejte také místní složky obsahu služby WSUS.  

Další informace o sdílení databáze WSUS najdete v následujících blogových příspěvcích:  

- [Implementace sdíleného SUSDBu pro Configuration Manager body aktualizace softwaru](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Pokyny pro více instancí služby WSUS, které sdílí databázi obsahu při použití Configuration Manager](/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb).


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> Když Configuration Manager a služba WSUS používají stejný SQL Server, nakonfigurujte jeden tak, aby používal pojmenovanou instanci a druhý pro použití výchozí instance.  

Pokud databáze Configuration Manager a WSUS sdílejí stejnou instanci SQL Server, nemůžete snadno určit využití prostředků mezi těmito dvěma aplikacemi. Pro Configuration Manager a WSUS použijte různé instance SQL Server. Tato konfigurace usnadňuje řešení potíží a diagnostiku problémů s využitím prostředků, ke kterým může dojít u každé aplikace.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> Zadejte nastavení ukládat aktualizace místně.  

Při instalaci služby WSUS vyberte nastavení pro **ukládání aktualizací místně**. Toto nastavení způsobí, že služba WSUS stáhne licenční smlouvy, které jsou přidruženy k aktualizacím softwaru. Stáhne je během procesu synchronizace a uloží je na místní pevný disk pro server WSUS. Pokud toto nastavení nevyberete, mohou klientské počítače selhat při kontrole aktualizací softwaru, které mají licenční podmínky. Součást **Správce synchronizace služby WSUS** v bodu aktualizace softwaru ověřuje, že ve výchozím nastavení je toto nastavení povoleno každých 60 minut.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> Provozní osvědčené postupy  

Když používáte aktualizace softwaru, použijte následující nejlepší postupy:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> Omezení aktualizací softwaru na 1000 v jednom nasazení aktualizace softwaru  

Omezte počet aktualizací softwaru na 1000 v každém nasazení aktualizace softwaru. Když vytváříte pravidlo automatického nasazení, ověřte, že zadaná kritéria nevedou k více než 1000 aktualizacím softwaru. Pokud ručně nasadíte aktualizace softwaru, nevybírejte více než 1000 aktualizací.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> Vytvoření nové skupiny aktualizací softwaru pokaždé, když se pravidlo automatického nasazení spustí pro "patch úterý" a pro obecné nasazení  

V nasazení je povolený limit 1000 aktualizací softwaru. Když vytváříte pravidlo automatického nasazení (ADR), určíte, jestli se má použít existující skupina aktualizací, nebo vytvořit novou skupinu aktualizací pokaždé, když se pravidlo spustí. Pokud určíte kritéria v pravidle automatického nasazení, která budou mít za následek více aktualizací softwaru a pravidlo se bude spouštět podle plánu opakování, vytvořte novou skupinu aktualizací softwaru pokaždé, když se pravidlo spustí. Toto chování brání nasazení v překročení limitu 1000 aktualizací softwaru na jedno nasazení.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> Použití existující skupiny aktualizací softwaru pro pravidla automatického nasazení pro aktualizace definic Endpoint Protection  

Když pomocí pravidla automatického nasazení nasadíte Endpoint Protection aktualizace definic častým způsobem, vždy použijte existující skupinu aktualizací softwaru. V opačném případě může pravidlo automatického nasazení vytvořit stovky skupin aktualizací softwaru v průběhu času. Vydavatelé aktualizací definic obvykle nastavují aktualizace definic, jejichž platnost vyprší, pokud jsou nahrazeny čtyřmi novějšími aktualizacemi. Proto skupina aktualizací softwaru vytvořená pomocí pravidla automatického nasazení nikdy neobsahuje více než čtyři aktualizace definicí vydavatele: jednu aktivní a tři nahrazené.  



## <a name="see-also"></a>Viz také  
 [Plánování aktualizací softwaru](plan-for-software-updates.md)