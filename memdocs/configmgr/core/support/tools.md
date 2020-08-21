---
title: Configuration Manager – nástroje
titleSuffix: Configuration Manager
description: Přečtěte si o nástrojích, které vám pomůžou se správou a řešením Configuration Manager infrastruktury.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb2529dbbe923a5035f0b7586dab696cd6fc917e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699411"
---
# <a name="configuration-manager-tools"></a>Configuration Manager – nástroje

*Platí pro: Configuration Manager (Current Branch)*

Mezi nástroje Configuration Manager patří [klientské](#client-tools) a [serverové nástroje](#server-tools). Tyto nástroje vám pomůžou při podpoře a odstraňování potíží s infrastrukturou Configuration Manager.

Od verze Configuration Manager 1806 jsou tyto nástroje zahrnuté do `CD.Latest\SMSSETUP\Tools` složky na serveru lokality. Není nutná žádná další instalace.<!--1357145--> Použijte tyto verze nástrojů s Configuration Manager verze 1806 a novější.

Všechny operační systémy Windows uvedené jako Podporovaní klienti v [podporovaných operačních systémech pro klienty a zařízení](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) se podporují pro použití s těmito nástroji.

> [!Note]  
> Produkt [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) je stále k dispozici na webu služby Stažení softwaru. Pro Configuration Manager verze 1806 a novější použijte verze nástrojů na disku CD-ROM. Poslední složka na serveru lokality. Některé nástroje byly dříve v sadě nástrojů, ale nejsou součástí verze 1806. Tyto starší nástroje již nejsou podporovány.


## <a name="client-tools"></a>Nástroje klienta

Tyto nástroje jsou v `ClientTools` podsložce:

- [CMTrace](cmtrace.md): umožňuje zobrazit, monitorovat a analyzovat soubory protokolu Configuration Manager.  

- [Klient Spy](clispy.md): řešení potíží souvisejících s distribucí softwaru, inventářem a měřením

- [Nástroj pro monitorování nasazení](deployment-monitoring-tool.md): řešení problémů s nasazením aplikací, aktualizací a směrného plánu  

- [Zásady Spy](policy-spy.md): zobrazení přiřazení zásad  

- [Nástroj Power Viewer](power-viewer-tool.md): zobrazení stavu funkce řízení spotřeby  

- [Nástroj pro odeslání plánu](send-schedule-tool.md): aktivovat plány a vyhodnocení směrných plánů konfigurace  

> [!Note]  
> `ClientTools`Složka také obsahuje soubor Microsoft.Diagnostics.Tracing.EventSource.dll. Tato knihovna vyžaduje několik nástrojů klienta. Nemůžete ho přímo použít.  


## <a name="server-tools"></a>Nástroje serveru

Tyto nástroje jsou v `ServerTools` podsložce:

- [Správce fronty úlohy DP](dp-job-manager.md): řeší úlohy distribuce obsahu do distribučních bodů  

- [Prohlížeč vyhodnocení kolekce](ceviewer.md): zobrazení podrobností o vyhodnocení kolekce  

- [Průzkumník knihovny obsahu](content-library-explorer.md): zobrazit obsah úložiště jediné instance knihovny obsahu  

- [Přenos knihovny obsahu](content-library-transfer.md): přenáší knihovnu obsahu mezi jednotkami  

- [Nástroj pro vlastnictví obsahu](content-ownership-tool.md): změní vlastnictví osamocených balíčků. Tyto balíčky existují v lokalitě bez vlastnícího serveru lokality.

- [Nástroj pro správu a auditování na základě rolí](rbaviewer.md): pomáhá správcům auditovat konfiguraci rolí.  

- [Nástroj pro Shrnutí měřičů spuštění](run-meter-summ.md): úloha Shrnutí měření spuštění a analýza dat měření

> [!Note]  
> Složka ServerTools obsahuje také následující soubory:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Některé serverové nástroje vyžadují tyto knihovny. Nemůžete je přímo použít.  

## <a name="other-tools-and-toolkits"></a>Další nástroje a sady nástrojů

- [Support Center](support-center.md): Shromážděte informace z klientů pro snazší analýzu při odstraňování potíží.

    Počínaje verzí 1906 je **OneTrace** nový prohlížeč protokolů s nástrojem Support Center. Funguje podobně jako CMTrace, s vylepšeními. Další informace najdete v tématu [Support Center OneTrace](support-center-onetrace.md).

- [Rozšiřování a migrace místního serveru na Microsoft Azure](azure-migration-tool.md): pomáhá programově vytvářet virtuální počítače Azure pro Configuration Manager. <!--3556022--> 

- [Nástroj pro vyčištění knihovny obsahu](../plan-design/hierarchy/content-library-cleanup-tool.md): pomocí **ContentLibraryCleanup.exe** v nástroji `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` můžete odebrat osamocený obsah z distribučního bodu.  

- [Nástroj pro údržbu hierarchie](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): pomocí **Preinst.exe** ve `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` sdílené složce na serveru lokality předejte příkazy do komponenty Hierarchy Manager.  

- [Nástroj pro resetování aktualizací](../servers/manage/update-reset-tool.md): pomocí **CMUpdateReset.exe** v nástroji `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` můžete opravit problémy, které mají problémy při stahování nebo replikaci v konzolových aktualizacích.  

- [Nástroj pro připojení služby](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): pomocí **ServiceConnectionTool.exe** v `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` můžete udržovat svůj server v aktuálním stavu, kdy je spojovací bod služby offline.   

- [Sada Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): sada nástrojů, procesů a pokyny pro automatizaci nasazení desktopových a SERVEROVÝCH operačních systémů.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): samostatný nástroj pro správu a import vlastních aktualizací softwaru.

- [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md): Převeďte starší balíčky na aplikace.