---
title: Monitorování hierarchie
titleSuffix: Configuration Manager
description: Naučte se monitorovat infrastrukturu v Configuration Manager pomocí pracovního prostoru Monitorování v konzole nástroje.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 504943df58c0471a0ef821a269cc22b2d12d76d8
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068034"
---
# <a name="monitor-the-hierarchy"></a>Monitorování hierarchie

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li monitorovat hierarchii v Configuration Manager, použijte pracovní prostor **monitorování** v konzole Configuration Manager.  

> [!NOTE]  
> Výjimkou z tohoto umístění je migrace lokalit. Tento proces se sleduje v uzlu **migrace** v pracovním prostoru **Správa** . Další informace najdete v tématu [operace migrace do Configuration Manager aktuální větve](../../migration/operations-for-migration.md).  

Společně s použitím konzoly Configuration Manager pro monitorování použijte následující funkce:

- [Úvod do vytváření sestav](introduction-to-reporting.md)
- [Soubory protokolu](../../plan-design/hierarchy/log-files.md).  

Pokud sledujete lokality, vyhledejte projevy, které indikují problémy vyžadující, abyste provedli opatření. Příklad:  

- Nevyřízené položky souborů na serverech lokality a systémech lokality.  

- Stavové zprávy, které indikují chybu nebo problém.  

- Selhání komunikace v lokalitě.  

- Chybové zprávy a upozornění v protokolu událostí systému na serverech.  

- Chybové zprávy a upozornění v protokolu událostí systému Microsoft SQL Server.  

- Lokality nebo klienti, kteří neohlásili stav v dlouhou dobu.  

- Pomalá odezva z databáze systému SQL Server.  

- Známky selhání hardwaru.  

Pokud úlohy monitorování odhalí jakékoli známky problémů, prozkoumejte zdroj problému. Pak ji rychle opravte, abyste minimalizovali riziko selhání lokality.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> Monitorování běžných úloh správy

Configuration Manager poskytuje integrované monitorování v konzole Configuration Manager.

### <a name="alerts"></a>Výstrahy

Další informace najdete v tématu [monitorování výstrah](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Nastavení dodržování předpisů

Další informace najdete v tématu [Postup monitorování nastavení dodržování předpisů](../../../compliance/deploy-use/monitor-compliance-settings.md).

### <a name="content"></a>Obsah

Obecné informace o monitorování obsahu najdete v tématu [Správa obsahu a infrastruktury obsahu](../deploy/configure/manage-content-and-content-infrastructure.md).  

Další informace o monitorování konkrétních typů obsahu:

- [Monitorování aplikací](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Monitorování balíčků a programů](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Monitorování obsahu pro aktualizace softwaru](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Monitorování obsahu pro nasazení operačního systému](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Funkce Endpoint Protection

Další informace najdete v tématu [monitorování Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>Nasazení operačního systému

Další informace najdete v tématu [monitorování nasazení operačního systému](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Monitorování řízení spotřeby

Další informace najdete v tématu [monitorování a plánování řízení spotřeby](../../clients/manage/power/monitor-and-plan-for-power-management.md).  

### <a name="monitor-software-metering"></a>Monitorování monitorování míry využívání softwaru

Další informace najdete v tématu [monitorování využití aplikací pomocí monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Monitorování aktualizací softwaru

Další informace najdete v tématu [monitorování aktualizací softwaru](../../../sum/deploy-use/monitor-software-updates.md).  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> Monitorování hierarchie lokality

Uzel **hierarchie lokality** pracovního prostoru **sledování** poskytuje přehled vaší hierarchie Configuration Manager a propojení mezi lokalitami. 

K monitorování stavu jednotlivých lokalit použijte uzel **hierarchie lokality** . Také Sledujte odkazy replikace mezi lokalitami a jejich vztah k vnějším faktorům, jako je například zeměpisné umístění.  

Stav lokality i stav propojení mezi lokalitami se replikují jako data lokality, ne jako globální data. Když připojíte konzolu Configuration Manager k podřízené primární lokalitě, nemůžete zobrazit stav lokality nebo propojení pro jiné primární lokality nebo jejich podřízené sekundární lokality. Například v hierarchii s více primárními lokalitami, pokud připojíte konzolu nástroje k primární lokalitě, můžete zobrazit stav podřízených sekundárních lokalit, primární lokalitu a lokalitu centrální správy. V tomto zobrazení nemůžete zobrazit stav jiných webů pod lokalitou centrální správy.  

Chcete-li řídit zobrazení v uzlu **hierarchie lokality** , použijte akci **Konfigurovat nastavení** . Hierarchie replikuje nastavení, které nakonfigurujete v tomto uzlu.  

### <a name="hierarchy-diagram"></a>Diagram hierarchie

Diagram hierarchie zobrazuje vaše lokality na topologické mapě. Vyberte lokalitu a zobrazte souhrn stavových zpráv z dané lokality. Podrobné procházení pro zobrazení stavových zpráv a přístup k **vlastnostem**webu.  

Chcete-li zobrazit stav vysoké úrovně pro lokalitu nebo propojení replikace mezi lokalitami, umístěte ukazatel myši na objekt. Stav odkazu replikace se nereplikuje globálně. Chcete-li zobrazit podrobnosti o připojení replikace mezi všemi primárními lokalitami v hierarchii, Připojte konzolu k lokalitě centrální správy.  

Následující možnosti pozměňují diagram hierarchie:  

#### <a name="groups"></a>Skupiny

Nakonfigurujte počet primárních lokalit a sekundárních lokalit, které aktivují změnu v diagramu hierarchie. Tato změna v zobrazení kombinuje lokality do jednoho objektu. Pak uvidíte celkový počet lokalit a kumulativní souhrn stavových zpráv a stavu lokality na vysoké úrovni.

#### <a name="favorite-sites"></a>Oblíbené weby

Zadejte jednotlivé lokality, které mají být v oblíbených lokalitách. Oblíbené lokality jsou v diagramu hierarchie označené ikonou s hvězdičkou. Oblíbené weby nejsou v kombinaci s ostatními lokalitami při používání skupin. Vždycky se zobrazují jednotlivě.  

### <a name="geographical-view"></a>Zeměpisné zobrazení

> [!IMPORTANT]
> Od srpna 2020 se tato funkce už nepoužívá. Použijte možnost **Diagram hierarchie** .<!--8116777-->

Zeměpisné zobrazení ukazuje umístění jednotlivých lokalit na zeměpisné mapě. Zobrazuje jenom weby, které nakonfigurujete v umístění. Když v tomto zobrazení vyberete lokalitu, zobrazí se odkazy replikace na nadřazené nebo podřízené lokality. Na rozdíl od zobrazení diagramu hierarchie není v tomto zobrazení možné zobrazit podrobnosti o stavových zprávách nebo odkazech replikace.  

> [!NOTE]  
> Chcete-li použít zeměpisné zobrazení, je nutné, aby počítač, ke kterému je připojena konzola Configuration Manager, měl nainstalovaný prohlížeč Internet Explorer a měl přístup k mapám Bing pomocí protokolu HTTP.  

Následující možnost upraví zeměpisné zobrazení:  

#### <a name="site-location"></a>Umístění webu

Pro každou lokalitu zadejte zeměpisné umístění pomocí jednoho z následujících typů:

- Adresa ulice
- Název místa, jako je název města
- Souřadnice zeměpisné šířky a délky

Pokud například chcete použít zeměpisnou šířku a délku Redmond, Washington, zadejte **N 47 40 26,3572 W 122 7 17,4432** jako umístění lokality. Nemusíte zadávat symboly pro stupně, minuty nebo sekundy zeměpisné šířky a délky. Configuration Manager používá mapy Bing k zobrazení umístění v zeměpisném zobrazení. Pak můžete hierarchii zobrazit v geografických umístěních. Toto zobrazení nabízí přehled o místních problémech, které mohou ovlivnit konkrétní lokality nebo replikaci mezi lokalitami.  

Pokud zadáte umístění, můžete pro vyhledání konkrétní lokality ve vaší hierarchii použít pole **Umístění** . Po vybrání lokality zadejte ve sloupci **Umístění** její umístění, a to jako název města nebo adresu. Configuration Manager používá k překladu umístění mapy Bing.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Další kroky

[Monitorování replikace databáze](monitor-replication.md)
