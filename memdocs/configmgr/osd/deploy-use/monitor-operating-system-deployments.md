---
title: Monitorování nasazení operačních systémů
titleSuffix: Configuration Manager
description: Pro usnadnění monitorování objektů nasazení operačního systému poskytuje konzola Configuration Manager výstrahy, sestavy a různé indikátory stavu.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ebae877e8a74c67f1ffd869a75db21209c0b5b9c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124976"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>Monitorování nasazení operačního systému v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Konzola Configuration Manager poskytuje následující možnosti, které vám pomůžou monitorovat objekty nasazení operačního systému.  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> Výstrahy nasazení operačního systému  
 V nastavení nasazení pořadí úkolů můžete nakonfigurovat výstrahu, která upozorní administrativní uživatele, když úroveň dodržování předpisů pro dané nasazení klesne pod nastavenou procentní hodnotu.  

 Když nakonfigurujete nastavení výstrah, pokud dojde k zadaným podmínkám, Configuration Manager vygeneruje výstrahu. Výstrahy nasazení pořadí úkolů můžete zobrazit na těchto místech:  

1.  Nedávné výstrahy můžete zobrazit v uzlu **Operační systémy** v pracovním prostoru **Softwarová knihovna** .  

2.  Konfigurované výstrahy můžete spravovat v uzlu **Výstrahy** v pracovním prostoru **Sledování** .  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a>Stav nasazení pořadí úloh  
 Po nasazení pořadí úkolů můžete monitorovat stav nasazení. Stav nasazení pořadí úkolů můžete monitorovat podle následujícího postupu.  

#### <a name="to-monitor-deployment-status"></a>Postup sledování stavu nasazení  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru Sledování klikněte na možnost **Nasazení**.  

3.  Klikněte na pořadí úkolů, u kterého chcete monitorovat stav nasazení.  

4.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Zobrazit stav**.  

> [!NOTE]  
> Po zahájení upgradu se vygeneruje stavová zpráva 52200. Obsahuje uživatele, který provedl upgrade.  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a> Sestavy nasazení operačního systému  
 Je dostupná řada předdefinovaných sestav nasazení operačního systému. Ty jsou rozdělené do několika kategorií a dají se použít k zjištění určitých informací o migraci stavu a nasazeních pořadí úkolů. Kromě použití předem konfigurovaných sestav rovněž můžete vytvořit vlastní sestavy aktualizací softwaru tak, aby vyhovovaly potřebám vašeho podniku. Další informace najdete v tématu [operace a údržba pro vytváření sestav](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Monitorování obsahu  
 Můžete sledovat obsah v konzole Configuration Manager a zkontrolovat stav všech typů balíčků ve vztahu k přidruženým distribučním bodům. To může zahrnovat stav ověření obsahu pro obsah v balíčku, stav obsahu přiřazeného ke konkrétní skupině distribučních bodů, stav obsahu přiřazeného k distribučnímu bodu a stav volitelných funkcí pro jednotlivé distribuční body (ověření obsahu, PXE a vícesměrové vysílání).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitorování stavu obsahu  
 Uzel **Stav obsahu** v pracovním prostoru **Monitorování** poskytuje informace o balíčcích obsahu. Můžete zkontrolovat obecné informace o balíčku, stav distribuce pro balíček a podrobné informace o stavu pro balíček. Stav obsahu zobrazíte pomocí následujícího postupu.  

#### <a name="to-monitor-content-status"></a>Postup sledování stavu obsahu  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru Sledování rozbalte možnost **Stav distribuce**a pak klikněte na položku **Stav obsahu**. Balíčky jsou zobrazeny.  

3.  Vyberte balíček, pro který chcete zobrazit podrobné informace o stavu.  

4.  Na kartě **Domů** klikněte na možnost **Zobrazit stav**. Zobrazí se podrobné informace o stavu balíčku.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a>Stav skupiny distribučních bodů  
 Uzel **Stav skupiny distribučních bodů** v pracovním prostoru **Sledování** poskytuje informace o skupinách distribučních bodů. Můžete zobrazit obecné informace o skupině distribučních bodů, jako je stav skupiny distribučních bodů a míra dodržení předpisů, stejně jako podrobné informace o stavu pro skupinu distribučních bodů. Chcete-li zobrazit stav skupiny distribučních bodů, postupujte podle následujícího popisu.  

#### <a name="to-monitor-distribution-point-group-status"></a>Sledování stavu skupiny distribučních bodů  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru sledování rozbalte možnost **Stav distribuce**a pak klikněte na položku **Stav skupiny distribučních bodů**. Zobrazí se skupiny distribučních bodů.  

3.  Vyberte skupinu distribučních bodů, pro kterou chcete zobrazit podrobné informace o stavu.  

4.  Na kartě **Domů** klikněte na možnost **Zobrazit stav**. Zobrazí se informace o stavu skupiny distribučních bodů.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Stav konfigurace distribučního bodu  
 Uzel **Stav konfigurace distribučního bodu** v pracovním prostoru **Sledování** poskytuje informace o distribučním bodu. Můžete zkontrolovat, které atributy jsou povoleny pro distribuční bod, jako např. PXE, vícesměrové vysílání a ověření obsahu. Uvedeny jsou tu také podrobné informace o stavu distribučního bodu. Chcete-li zobrazit stav konfigurace distribučního bodu, postupujte podle následujícího popisu.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Monitorování stavu konfigurace distribučního bodu  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru monitorování rozbalte možnost **Stav distribuce**a pak klikněte na položku **Stav konfigurace distribučního bodu**. Zobrazí se distribuční body.  

3.  Vyberte distribuční bod, pro který chcete zobrazit informace o stavu distribučního bodu.  

4.  V podokně výsledků klikněte na kartu **Podrobnosti** . zobrazí se informace o stavu distribučního bodu.  
