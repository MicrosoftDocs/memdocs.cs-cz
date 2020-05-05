---
title: Monitorování aktualizací softwaru
titleSuffix: Configuration Manager
description: Konzola Configuration Manager poskytuje výstrahy a stavy pro monitorování aktualizací a dodržování předpisů.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110368"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Monitorování aktualizací softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager poskytuje mnoho způsobů, jak vám pomůžou monitorovat objekty, procesy a informace o kompatibilitě aktualizací softwaru. Pomocí následujících částí můžete monitorovat aktualizace softwaru.

## <a name="software-updates-dashboard"></a>Řídicí panel aktualizace softwaru

*(Představené ve verzi 1610)*

Configuration Manager počínaje verzí 1610 můžete pomocí řídicího panelu aktualizace softwaru zobrazit aktuální stav dodržování předpisů u zařízení ve vaší organizaci a rychle analyzovat data a zjistit, která zařízení jsou v ohrožení. Řídicí panel zobrazíte tak, že přejdete na **monitorování** > **Přehled** > **zabezpečení** > **aktualizace softwaru řídicí panel**.

## <a name="drill-through-required-updates"></a>Podrobné informace o požadovaných aktualizacích
<!--4224414-->
*(Představené ve verzi 1906)*

Můžete procházet statistiky dodržování předpisů a zjistit, která zařízení vyžadují konkrétní aktualizaci softwaru Microsoft 365 Apps. Chcete-li zobrazit seznam zařízení, potřebujete oprávnění k zobrazení aktualizací a kolekcí, do kterých zařízení patří. Přechod k podrobnostem v seznamu zařízení:

1. Přejít na software **knihovny** > softwaru**aktualizace** > softwaru**všechny aktualizace softwaru**.
1. Vyberte jakoukoli aktualizaci, kterou vyžaduje aspoň jedno zařízení.
1. Podívejte se na kartu **Souhrn** a v části **Statistika**Najděte výsečový graf.
1. Pokud chcete přejít k podrobnostem seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu.
1. Tato akce přejde na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci. Můžete také provést akce pro uzel, jako je například vytvoření nové kolekce ze seznamu.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Výstrahy na aktualizace softwaru  
 Můžete nakonfigurovat výstrahy pro aktualizace softwaru tak, aby upozorňovaly administrativní uživatele, když úroveň dodržování předpisů pro nasazení aktualizace softwaru klesne pod nastavenou procentní hodnotu. Výstrahy pro nasazení aktualizace softwaru můžete nakonfigurovat v následujících umístěních:  

-   Nastavení ADR: Nastavení výstrah můžete nakonfigurovat v Průvodci vytvořením pravidla automatického nasazení a ve vlastnostech pro ADR.  

-   Nastavení nasazení: Nastavení výstrah lze nakonfigurovat v Průvodci nasazením aktualizace softwaru ve vlastnostech nasazení.  

Když nakonfigurujete nastavení výstrah, pokud dojde k zadaným podmínkám, Configuration Manager vygeneruje výstrahu. Výstrahy na aktualizace softwaru můžete zkontrolovat v následujících umístěních:  

1.  Nedávné výstrahy můžete zkontrolovat v uzlu **Aktualizace softwaru** v pracovním prostoru **Softwarová knihovna** .  

2.  Konfigurované výstrahy můžete spravovat v uzlu **Výstrahy** v pracovním prostoru **Sledování** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a>Stav synchronizace aktualizací softwaru  
 Po zahájení procesu synchronizace můžete monitorovat proces synchronizace z konzoly Configuration Manager pro všechny body aktualizace softwaru ve vaší hierarchii. Pomocí následujícího postupu monitorujte proces synchronizace aktualizací softwaru.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Monitorování procesu synchronizace aktualizací softwaru  

- V konzole Configuration Manager přejděte na **monitorování** > **Přehled** > **stav synchronizace bodu aktualizace softwaru**.  

    Body aktualizace softwaru ve vaší hierarchii Configuration Manager se zobrazí v podokně výsledků. Z tohoto hlediska můžete sledovat stav synchronizace všech míst aktualizace softwaru. Chcete-li zobrazit podrobnější informace o procesu synchronizace, můžete zkontrolovat soubor souboru wsyncmgr. log, který je umístěn ve složce <*ConfigMgrInstallationPath*> \Logs. na každém serveru lokality.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> Stav nasazení aktualizace softwaru  
 Po nasazení aktualizací softwaru do skupiny aktualizace softwaru nebo nasazení jedné aktualizace softwaru můžete sledovat stav nasazení. Stav nasazení pro skupinu aktualizace softwaru nebo aktualizaci softwaru můžete sledovat pomocí následujícího postupu.  

#### <a name="to-monitor-deployment-status"></a>Postup sledování stavu nasazení  

1.  V konzole Configuration Manager přejděte na **monitorování** > **Přehled** > **nasazení**.  

2.  Klikněte na skupinu aktualizace softwaru nebo aktualizaci softwaru, pro kterou chcete sledovat stav nasazení.  

3.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Zobrazit stav**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Sestavy aktualizací softwaru  
 Stavové zprávy pro aktualizace softwaru poskytují informace o dodržování předpisů aktualizací softwaru a o stavu vynucení a vyhodnocení nasazení aktualizací softwaru. K zobrazení těchto stavových zpráv můžete spustit sestavy aktualizací softwaru. K dispozici je více než 30 předdefinovaných sestav aktualizací softwaru. Jsou uspořádány do několika kategorií a lze je použít k hlášení konkrétních informací o aktualizacích a nasazeních softwaru. Kromě použití předem konfigurovaných sestav rovněž můžete vytvořit vlastní sestavy aktualizací softwaru tak, aby vyhovovaly potřebám vašeho podniku. Další informace najdete v tématu [operace a údržba pro vytváření sestav](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Doporučené sestavy aktualizací softwaru
Níže jsou uvedeny některé sestavy, které jsou užitečné při určování potenciálních problémů: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Dodržování předpisů 9 – celkový stav a dodržování předpisů (počínaje verzí 1806)
Sestava obsahuje následující části:

- **V pořádku klienti vs celkem klientů**: Tento pruhový graf porovnává "v pořádku" klienti, kteří s lokalitou komunikovali v zadaném časovém období vzhledem k celkovému počtu klientů v zadané kolekci.
- **Přehled dodržování předpisů**: Tento výsečový graf zobrazuje celkový stav dodržování předpisů pro konkrétní skupinu aktualizací softwaru na aktivních klientech v zadané kolekci.
- **Hlavní 5 nekompatibilní podle ID článku**: Tento pruhový graf zobrazuje horní pět aktualizací softwaru v zadané skupině, které nedodržují předpisy aktivních klientů v zadané kolekci.
- Dolní část sestavy je tabulka s dalšími podrobnostmi, které obsahují seznam aktualizací softwaru v zadané skupině.

#### <a name="management-2---updates-required-but-not-deployed"></a>Správa 2 – nenasazené vyžadované aktualizace

Tato sestava zobrazuje aktualizace softwaru specifické pro dodavatele v konkrétní klasifikaci aktualizací, které byly zjištěny podle požadavků na klienty, ale nebyly nasazeny do určité kolekce. 

#### <a name="troubleshooting-2---deployment-errors"></a>Řešení potíží 2 – chyby nasazení

Tato sestava vrátí chyby nasazení v lokalitě a počet počítačů, ve kterých došlo k jednotlivým chybám. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Monitorování obsahu  
 Můžete sledovat obsah v konzole Configuration Manager a zkontrolovat stav všech typů balíčků ve vztahu k přidruženým distribučním bodům. To může zahrnovat stav ověření obsahu pro obsah v balíčku, stav obsahu přiřazeného ke konkrétní skupině distribučních bodů, stav obsahu přiřazeného k distribučnímu bodu a stav volitelných funkcí pro jednotlivé distribuční body (ověření obsahu, PXE a vícesměrové vysílání).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitorování stavu obsahu  
 Uzel **Stav obsahu** v pracovním prostoru **Monitorování** poskytuje informace o balíčcích obsahu. Můžete zkontrolovat obecné informace o balíčku, stav distribuce pro balíček a podrobné informace o stavu pro balíček. Stav obsahu zobrazíte pomocí následujícího postupu.  

#### <a name="to-monitor-content-status"></a>Postup sledování stavu obsahu  

1.  V konzole Configuration Manager přejděte na **monitorování** > **Přehled** > stav**distribuce** > stav**obsah**. Balíčky jsou zobrazeny.  

2.  Vyberte balíček, pro který chcete zobrazit podrobné informace o stavu.  

3.  Na kartě **Domů** klikněte na možnost **Zobrazit stav**. Zobrazí se podrobné informace o stavu balíčku.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a>Stav skupiny distribučních bodů  
 Uzel **Stav skupiny distribučních bodů** v pracovním prostoru **Sledování** poskytuje informace o skupinách distribučních bodů. Můžete zobrazit obecné informace o skupině distribučních bodů, jako je stav skupiny distribučních bodů a míra dodržení předpisů, stejně jako podrobné informace o stavu pro skupinu distribučních bodů. Chcete-li zobrazit stav skupiny distribučních bodů, postupujte podle následujícího popisu.  

#### <a name="to-monitor-distribution-point-group-status"></a>Sledování stavu skupiny distribučních bodů  

1.  V konzole Configuration Manager přejděte do části **monitorování** > **Přehled** > **stav** > distribuce**stav skupiny distribuční bod**. Zobrazí se skupiny distribučních bodů.  

2.  Vyberte skupinu distribučních bodů, pro kterou chcete zobrazit podrobné informace o stavu.  

3.  Na kartě **Domů** klikněte na možnost **Zobrazit stav**. Zobrazí se informace o stavu skupiny distribučních bodů.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Stav konfigurace distribučního bodu  
 Uzel **Stav konfigurace distribučního bodu** v pracovním prostoru **Sledování** poskytuje informace o distribučním bodu. Můžete zkontrolovat, které atributy jsou povoleny pro distribuční bod, jako např. PXE, vícesměrové vysílání a ověření obsahu. Uvedeny jsou tu také podrobné informace o stavu distribučního bodu. Chcete-li zobrazit stav konfigurace distribučního bodu, postupujte podle následujícího popisu.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Monitorování stavu konfigurace distribučního bodu  

1.  V konzole Configuration Manager přejděte na **monitorování** > **Přehled** > stav > **Konfigurace distribučního bodu****stav distribuce**. Zobrazí se distribuční body.  

2.  Vyberte distribuční bod, pro který chcete zobrazit informace o stavu distribučního bodu.  

3.  V podokně výsledků klikněte na kartu **Podrobnosti** . zobrazí se informace o stavu distribučního bodu.  

## <a name="next-steps"></a>Další kroky

- [Soubory protokolu pro aktualizace softwaru](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Dokument white paper pro správu aktualizací softwaru](https://www.microsoft.com/download/confirmation.aspx?id=44578)
