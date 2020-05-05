---
title: Změny ze verze 2012
titleSuffix: Configuration Manager
description: Identifikujte změny a nové funkce v Configuration Manageru a v nástroji System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720825"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>Co se změnilo v nástroji System Center 2012 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktuální větev Configuration Manager přináší důležité změny ze služby System Center 2012 Configuration Manager. Tento článek popisuje významné změny a nové funkce, které jsou k dispozici v původní základní verzi 1511 Configuration Manager aktuální větve. Další informace o změnách zavedených v části Nedávné aktualizace pro Configuration Manager najdete v článku [novinky v Configuration Manager přírůstkových verzích](whats-new-incremental-versions.md).

> [!NOTE]
> Počínaje verzí 1910 je teď Configuration Manager součástí Microsoft Endpoint Manageru. Další informace najdete v tématu [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

Verze z prosince 2015 (verze 1511) Configuration Manager byla počáteční verzí aktuální Configuration Manager produktu od společnosti Microsoft. Obvykle se označuje jako Configuration Manager aktuální větev. *Aktuální větev* označuje, že tato verze podporuje přírůstkové aktualizace produktu. Nabízí také způsob, jak rozlišovat mezi touto verzí a předchozími verzemi Configuration Manager.  

Configuration Manager aktuální větev:  

- Nepoužívá v názvu produktu rok nebo identifikátor produktu, na rozdíl od minulých verzí, například Configuration Manager 2007 nebo Configuration Manager System Center 2012.  

- Podporuje přírůstkové aktualizace, které se označují také jako verze aktualizací. Počáteční verze byla verze 1511. Novější verze jsou vydávány několikrát za rok jako konzolové aktualizace, jako je verze 1910.  

- Se instaluje s použitím základní verze. Zatímco 1511 byla původní základní verze, nové základní verze se také uvolní v čase, jako je 2002. Základní verze lze použít k instalaci nové lokality Configuration Manager a hierarchie nástroje nebo k upgradu z podporované verze nástroje System Center 2012 Configuration Manager.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a>Konzolové aktualizace

Configuration Manager používá konzolovou metodu služby nazvanou **aktualizace a údržba** , která usnadňuje vyhledání a instalaci doporučených aktualizací.  

Některé verze jsou dostupné jenom jako aktualizace pro existující weby v konzole Configuration Manager. Tyto aktualizace nemůžete použít k instalaci nové lokality Configuration Manager. Například aktualizace 1910 je k dispozici pouze v rámci konzoly Configuration Manager. Používá se k aktualizaci lokality, která již používá podporovanou verzi Configuration Manager.

Verze aktualizace je pravidelně vydaná také jako nová *základní* verze. Například aktualizace verze 2002 je také směrný plán. Pro instalaci nové lokality nebo hierarchie použijte základní verzi. Nemusíte začínat starší základní verzí, jako je 1802, a upgradovat svůj způsob na nejaktuálnější verzi. Vždy používejte nejnovější směrné plány.

Další informace najdete v těchto článcích:

- [Aktualizace pro Configuration Manager](../../servers/manage/updates.md)
- [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a>Bod připojení služby  

Configuration Manager Current Branch zahrnuje novou roli systému lokality, **spojovací bod služby**:  

- Kontaktní bod pro mnoho funkcí s podporou cloudu

- Stáhne aktualizace vašeho webu.

- Nahrává diagnostiku a data o využití vašeho webu do cloudu Microsoftu.

Tato role systému lokality podporuje režimy provozu online i offline. Další informace najdete v tématu [o spojovacím bodu služby](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a>Data o využití a diagnostika

Configuration Manager shromažďuje diagnostická data a údaje o využití vašich lokalit a infrastruktury. Tyto informace jsou kompilovány a odesílány do cloudové služby společnosti Microsoft prostřednictvím spojovacího bodu služby. Configuration Manager vyžaduje, aby tato data stahoval aktualizace, které jsou použitelné pro vaše prostředí. Při nastavování spojovacího bodu služby můžete určit úroveň dat, která shromažďuje, a to, jestli se mají data automaticky (online) nebo ručně (offline) odeslat.

Další informace najdete v tématu [Diagnostika a data o využití](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a>Zastaralé funkce  

Některé funkce, jako je nativní [Podpora pro Intel Active Management Technology](#bkmk_AMT) na bázi AMT, se z konzoly Configuration Manager odeberou. Další funkce, jako je například ochrana síťového přístupu, jsou zcela odebrány. Kromě toho už nejsou podporované některé starší produkty od Microsoftu, jako je Windows Vista, Windows Server 2008 a SQL Server 2008.  

Seznam zastaralých funkcí najdete v tématu [odebrané a zastaralé položky](deprecated/removed-and-deprecated.md).  

Podrobnosti o podporovaných produktech, operačních systémech a konfiguracích najdete v části [podporované konfigurace](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a>Podpora Intel Active Management Technology (AMT)  

Configuration Manager Current Branch odebere nativní podporu pro počítače na bázi AMT z konzoly Configuration Manager. Pokud používáte [doplněk Intel SCS pro Microsoft Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html), jsou počítače s technologií AMT pořád plně spravované. Doplněk poskytuje přístup k nejnovějším funkcím pro správu AMT při odebrání zavedených omezení, dokud by tyto změny nemohly začlenit Configuration Manager.  

Odebrání integrované AMT pro Configuration Manager zahrnuje vzdálenou správu. Role systému lokality bodu vzdálené správy již není k dispozici.  

> [!Note]
> Tato změna neovlivní vzdálenou správu v nástroji System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Změny ve funkcích

V následujících částech jsou shrnuty některé významné změny v oblastech funkcí mezi System Center 2012 R2 Configuration Manager a verzí 1511 Configuration Manager aktuální větve. Další informace o dalších nejnovějších změnách ve funkcích najdete v článku [novinky v přírůstkových verzích](whats-new-incremental-versions.md).

### <a name="client-deployment"></a>Nasazení klienta  

Configuration Manager zavádí novou funkci pro testování nových verzí klienta Configuration Manager před upgradem zbytku lokality na nový software. Můžete nastavit předprodukční kolekci, ve které chcete pilotní nasazení nového klienta. Až budete s novým klientským softwarem spokojeni v předprodukčním prostředí, můžete klienta zvýšit tak, aby automaticky Upgradoval zbytek lokality na novou verzi.  

Další informace o testování klientů najdete v tématu [testování upgradu klienta v předprodukční kolekci](../../clients/manage/upgrade/test-client-upgrades.md).  

### <a name="os-deployment"></a>Nasazení operačního systému  

Uvědomte si následující změny nasazení operačního systému:

- V Průvodci vytvořením pořadí úloh je k dispozici nový typ pořadí úloh: **upgrade operačního systému z balíčku s upgradem**. Vytvoří kroky pro upgrade počítačů ze systému Windows 7 nebo Windows 8.1 na Windows 10. Další informace najdete v tématu [upgrade Windows na nejnovější verzi](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Při nasazení operačních systémů je teď dostupná sdílená mezipaměť prostředí Windows PE. Počítače, ve kterých se spouští pořadí úkolů pro nasazení operačního systému, můžou pomocí sdílené mezipaměti prostředí Windows PE získat obsah ze zdroje sdílené mezipaměti a nemusí stahovat obsah z distribučního bodu. Toto chování pomáhá minimalizovat provoz v síti WAN ve scénářích firemní pobočky, kde není k dispozici žádný místní distribuční bod. Další informace najdete v tématu [Příprava sdílené mezipaměti prostředí Windows PE pro omezení provozu v síti WAN](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- Teď si můžete ve svém prostředí zobrazit stav Windows jako služby. Můžete také vytvořit plány údržby, které tvoří okruhy nasazení, a zajistit, aby se počítače s Windows 10 aktuálními pobočkami při vydání nových sestavení aktualizovaly v aktuálním stavu. Kromě toho můžete zobrazit výstrahy, když se klienti Windows 10 blíží konci podpory jejich sestavení. Další informace najdete v tématu [Správa systému Windows jako služby](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### <a name="application-management"></a>Správa aplikací  

Uvědomte si následující změny správy aplikací:

- Configuration Manager umožňuje nasadit aplikace Univerzální platforma Windows (UWP) pro zařízení s Windows 10 nebo novějším. Další informace najdete v tématu [vytváření aplikací pro Windows](../../../apps/get-started/creating-windows-applications.md).  

- Centrum softwaru má nový, moderní vzhled. Aplikace dostupné pro uživatele, které se dřív zobrazovaly jenom v katalogu aplikací, se teď zobrazují v centru softwaru na kartě aplikace. Toto chování usnadňuje nasazení těchto nasazení a znemožňuje uživatelům, aby odkazovali na samostatný katalog aplikací. Kromě toho se již nevyžaduje prohlížeč s podporou technologie Silverlight. Další informace najdete v tématu [plánování a konfigurace správy aplikací](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

- Nový typ aplikace Instalační služba Windows přes MDM umožňuje vytvářet a nasazovat aplikace založené na Instalační službě systému Windows na zaregistrované počítače s Windows 10. Další informace najdete v tématu [vytváření aplikací pro Windows](../../../apps/get-started/creating-windows-applications.md).  

- V Configuration Manager 2012, pokud chcete zadat odkaz na aplikaci ve Windows Storu, můžete buď zadat odkaz přímo, nebo přejít ke vzdálenému počítači, ve kterém je aplikace nainstalovaná. V Configuration Manager aktuální větev můžete přesto zadat odkaz přímo, ale teď místo procházení k referenčnímu počítači můžete vyhledat aplikaci přímo z konzoly Configuration Manager.  

### <a name="software-updates"></a>Aktualizace softwaru  

Mějte na paměti následující změny v aktualizacích softwaru:

- Configuration Manager teď může detekovat rozdíl mezi metodami správy aktualizací softwaru pro počítače. Konkrétně může rozlišovat mezi počítačem s Windows 10, který se připojuje k web Windows Update pro firmy (WUfB), a počítačem připojenému ke službě WSUS. Atribut **UseWUServer** je nový a určuje, jestli je počítač spravovaný pomocí WUfB. V kolekci můžete pomocí tohoto nastavení odebrat tyto počítače ze správy aktualizací softwaru. Další informace najdete v tématu [Integrace s Windows Update for Business ve Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- Nyní můžete naplánovat a spustit úlohu čištění služby WSUS z konzoly Configuration Manager. Když ve vlastnostech **komponenty bodu aktualizace softwaru** zvolíte spuštění úlohy čištění služby WSUS, spustí se při další synchronizaci aktualizací softwaru. Aktualizace softwaru s vypršenou platností se na serveru služby WSUS nastaví na stav zamítnuto a Agent web Windows Update v počítačích už tyto aktualizace softwaru nekontroluje. Další informace najdete v oddílu [Naplánování a spuštění úlohy čištění služby WSUS](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Nastavení dodržování předpisů  

Pamatujte na následující změny nastavení dodržování předpisů:

- Configuration Manager vylepšuje pracovní postup pro vytváření položek konfigurace. Když teď při vytváření položky konfigurace vyberete podporované platformy, jsou dostupná jenom nastavení odpovídající dané platformě. Viz Začínáme [s nastavením dodržování předpisů](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- Průvodce **vytvořením položky konfigurace** teď usnadňuje výběr typu položky konfigurace, kterou chcete vytvořit. Kromě toho jsou dostupné nové a aktualizované položky konfigurace pro tato zařízení:  

    - Zařízení s Windows 10 spravovaná pomocí klienta Configuration Manager  

    - Mac OS X zařízení spravovaných pomocí klienta Configuration Manager  

    - Stolní a serverové počítače s Windows spravované pomocí klienta Configuration Manager  

    - Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager  

    Další informace najdete v tématu [Vytvoření položek konfigurace](../../../compliance/deploy-use/create-configuration-items.md).  

- Podpora správy nastavení na počítačích Mac OS X spravovaných bez Configuration Manager klienta.

### <a name="on-premises-mobile-device-management"></a>Místní správa mobilních zařízení  

Mobilní zařízení teď můžete spravovat pomocí místní infrastruktury Configuration Manager. Všechna data zařízení a správy se zpracovávají místně a nejsou součástí Microsoft Intunech nebo jiných cloudových služeb. Tento typ správy zařízení nevyžaduje klientský software. Configuration Manager spravuje zařízení s funkcemi, které jsou integrované v operačním systému zařízení.  

Další informace najdete v tématu [Správa mobilních zařízení s místní infrastrukturou](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## <a name="next-steps"></a>Další kroky

[Novinky v přírůstkových verzích](whats-new-incremental-versions.md)
