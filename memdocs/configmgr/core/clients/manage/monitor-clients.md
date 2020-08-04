---
title: Monitorování klientů
titleSuffix: Configuration Manager
description: Získejte podrobné pokyny k monitorování klientů v Configuration Manager
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a10e169db36c62b083c56114159b54185a1040
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2020
ms.locfileid: "87525909"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Postup monitorování klientů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po instalaci klienta Configuration Manager do zařízení s Windows ve vaší lokalitě monitorujte svůj stav a činnost v konzole Configuration Manager.  


## <a name="about-client-status"></a><a name="bkmk_about"></a>O stavu klienta

Configuration Manager poskytuje následující typy informací jako stav klienta:  

- **Online stav klienta**: web považuje zařízení za **online** , pokud je připojené k přiřazenému bodu správy. Pro indikaci, že je klient online, odesílá do bodu správy zprávy typu příkazového testu. Pokud bod správy neobdrží zprávu během pěti minut, web považuje klienta za **offline**.  

- **Aktivita klienta**: web považuje klienta za **aktivní** , pokud v posledních sedmi dnech komunikoval s Configuration Manager. Lokalita považuje klienta za **neaktivní** , pokud nedokončil následující akce během sedmi dnů:  

    - Požadovaná aktualizace zásad  
    - Odeslala se zpráva prezenčního signálu.  
    - Odeslán inventář hardwaru  

- **Kontroly klienta**: stav pravidelného vyhodnocení, které klient Configuration Manager spustí na zařízení. Vyhodnocení zkontroluje zařízení a může opravit některé problémy, které najde. Další informace najdete v tématu [kontroly stavu klienta](#BKMK_ClientHealth).  

     Na zařízeních, na kterých běží Windows 7, bude klientská kontroly spuštěna jako naplánovaná úloha. V novějších verzích operačních systémů se kontrolu klienta spouští automaticky během časového období údržby systému Windows.  

     Nápravu můžete nakonfigurovat tak, aby se nespouštěla na konkrétních zařízeních, třeba na podnikových serverech. Pokud existují další položky, které chcete vyhodnotit, použijte Configuration Manager nastavení dodržování předpisů k monitorování dalších konfigurací. Další informace o nastavení dodržování předpisů najdete v tématu [plánování a konfigurace nastavení dodržování předpisů](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

- **Vyřazeno z provozu**: lokalita označila záznam zařízení pro odstranění. K tomuto chování může dojít v případě, že se nová registrace pro stejné zařízení přiřadí ke stejné nebo jiné primární lokalitě v hierarchii. Lokalita tato zařízení odstraní při příštím spuštění úlohy údržby lokality **Odstranit stará data zjišťování**.<!-- SCCMDocs issue #1418 -->  

- **Zastaralé**: web zjistil nový záznam zařízení se stejným ID hardwaru, takže označí starý záznam jako zastaralý. Sestavy nepočítají zastaralé záznamy stejného zařízení vícekrát. Stále můžete cílit na zásady na zastaralá zařízení. Pokud web po 90 dnech nečinnosti neobdrží prezenční signál pro zastaralý záznam, odebere zastaralé zařízení, když spustí úlohu údržby lokality **Odstranit zastaralá data zjišťování klientů**.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a>Monitorování jednotlivých klientů

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Vyberte uzel **zařízení** nebo zvolte kolekci v části **kolekce zařízení**.  

    Ikony na začátku každého řádku označují online stav zařízení:  

    | Ikona | Description |
    | ---- | ----------- |  
    |![ikona online stavu pro klienty](../../../core/clients/manage/media/online-status-icon.png)|Zařízení je online.|  
    |![ikona offline stavu pro klienty](../../../core/clients/manage/media/offline-status-icon.png)|Zařízení je offline.|  
    |![ikona neznámého stavu pro klienty](../../../core/clients/manage/media/unknown-status-icon.png)|Online stav není známý.|  
    |![klient není nainstalován](../../../core/clients/manage/media/client-not-installed.png)|Klient není na zařízení nainstalován.|  

2. Pokud chcete podrobnější online stav, přidejte informace o online stavu klienta do zobrazení zařízení. Klikněte pravým tlačítkem na záhlaví sloupce a vyberte pole online stavu, která chcete přidat:

    - **Online stav zařízení**: udává, jestli je klient aktuálně online nebo offline. (Tento stav je stejné informace, jaké jsou vydány ikonami.)  

    - **Poslední online čas**: udává, kdy se online stav klienta změnil na online.  

    - **Poslední čas v režimu offline** indikuje, kdy se stav změnil na offline.  

3. Výběrem jednotlivého klienta v podokně se seznamem zobrazíte další stav v podokně podrobností. Tyto informace zahrnují činnost klienta a stav kontroly klienta.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a>Řídicí panel stavu klienta

<!--3599209-->
Nasadíte aktualizace softwaru a další aplikace, které vám pomůžou zabezpečit vaše prostředí, ale tato nasazení dosáhnou jenom zdravých klientů. Bezstavové Configuration Manager klienti nepříznivě ovlivňují celkové dodržování předpisů. Určení stavu klienta může být náročné v závislosti na jmenovateli: kolik zařízení by mělo být v oboru správy? Pokud například zjistíte všechny systémy ze služby Active Directory, i když některé z těchto záznamů jsou pro vyřazené počítače, tento proces zvýší váš jmenovatel.

Počínaje verzí 1902 si prohlédněte řídicí panel s informacemi o stavu klientů Configuration Manager ve vašem prostředí. Zobrazit stav klienta, stav scénáře a běžné chyby. Filtrovat zobrazení podle několika atributů, aby se zobrazily případné problémy podle verzí operačního systému a klienta.

V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Rozbalte položku **stav klienta**a vyberte uzel **řídicí panel stavu klienta** .

![Snímek obrazovky řídicího panelu stavu klienta](media/3599209-client-health-dashboard.png)

> [!Tip]  
> Neexistují žádné změny, které by bylo možné ccmevalovat.  

Ve výchozím nastavení se na řídicím panelu stavu klienta zobrazují online klienti a klienti v posledních třech dnech aktivní. Proto se na tomto řídicím panelu můžou zobrazovat odlišná čísla než v jiných historických zdrojích stavu klienta. Například jiné uzly v části **stav klienta**nebo sestavy v kategorii stav klienta.

### <a name="filters"></a>Filtry

V horní části řídicího panelu je k dispozici sada filtrů pro úpravu dat zobrazených na řídicím panelu.

- **Kolekce**: ve výchozím nastavení se na řídicím panelu zobrazí zařízení v kolekci **všechny systémy** . Vyberte kolekci zařízení ze seznamu pro určení oboru zobrazení pro podmnožinu zařízení v určité kolekci.  

- **Online/offline**: ve výchozím nastavení se na řídicím panelu zobrazí jenom online klienti. Tento stav pochází z kanálu oznámení klienta, který každých pět minut aktualizuje stav klienta. Další informace najdete v tématu [o stavu klienta](monitor-clients.md#bkmk_about).  

- **Aktivní \# dny**: ve výchozím nastavení se na řídicím panelu zobrazí klienti, kteří jsou v posledních třech dnech aktivní.  

- **Pouze selhání**: umožňuje určit rozsah zobrazení jenom na zařízení, která hlásí chybu stavu klienta.  

    > [!Tip]  
    > Tento filtr použijte spolu s dlaždicemi verze klienta a verze operačního systému. Další informace najdete v tématu [verze dlaždic](#version-tiles).

### <a name="client-health-percentage"></a>Procento stavu klienta

Tato dlaždice zobrazuje celkový stav klienta ve vaší hierarchii.

Dobrý Configuration Manager klient má následující vlastnosti:

- Online  
- Aktivně se odesílají data  
- Projde všemi kontrolami vyhodnocení stavu klienta.  

Další informace najdete v tématu [o stavu klienta](monitor-clients.md#bkmk_about).

Dobrý klient úspěšně komunikuje s lokalitou. Oznamuje všechna data v závislosti na definovaných plánech v nastavení klienta.

Vyberte segment tohoto grafu pro přechod k podrobnostem o zobrazení seznamu zařízení.

### <a name="version-tiles"></a>Dlaždice verze

Existují dvě dlaždice, které zobrazují stav klienta Configuration Manager verze klienta a verze operačního systému. Tyto dlaždice jsou užitečné, když provedete změny v filtrech, jako je například **Chyba**. Můžou vám pomůžou zdůraznit, jestli jsou některé problémy v určité verzi konzistentní. Tyto informace vám pomůžou při rozhodování o upgradu.

Vyberte segment těchto grafů pro přechod k podrobnostem do zobrazení seznamu zařízení.

### <a name="scenario-health"></a>Stav scénáře

Tento pruhový graf zobrazuje celkový stav pro následující základní scénáře:

- Zásady klienta
- Zjišťování prezenčního signálu
- Inventář hardwaru
- Inventář softwaru
- Stavové zprávy

Selektory použijte k úpravě fokusu na konkrétní scénáře v grafu.

Vždy se zobrazí následující dva pruhy:

- **Zkombinované (vše)**: kombinace všech scénářů (a)  
- **Kombinované (any)**: alespoň jeden z scénářů (nebo)

> [!Tip]  
> Stav scénáře se neměří od konfigurace nastavení klienta. Tyto hodnoty se můžou lišit v závislosti na výsledné sadě zásad na zařízení. Pomocí následujících kroků upravte zkušební období pro stav scénářů:
>
> - V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **stav klienta** .  
> - Na pásu karet vyberte **Nastavení stavu klienta**.  
>
> Ve výchozím nastavení platí, že pokud klient neodešle data specifická pro konkrétní scénář za **7 dní**, Configuration Manager považuje za tento scénář špatný stav.

### <a name="top-10-client-health-failures"></a>Prvních 10 selhání stavu klientů

Tento graf uvádí nejběžnější chyby ve vašem prostředí. Tyto chyby pocházejí ze systému Windows nebo Configuration Manager.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a>Monitorování stavu všech klientů

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **stav klienta** . Projděte si celkové statistiky pro činnost klienta a kontroly klientů napříč lokalitou. Změňte rozsah informací výběrem jiné kolekce.  

2. Chcete-li přejít k podrobnostem o hlášených statistikách, vyberte název hlášených informací. Například **aktivní klienti s úspěšnou kontrolou klienta nebo žádné výsledky**. Pak zkontrolujte informace o jednotlivých klientech.  

3. Vyberte **aktivita klienta** , aby se zobrazily grafy znázorňující činnost klienta ve vaší Configuration Manager lokalitě.  

4. Vyberte **Kontrola klienta** . zobrazí se grafy znázorňující stav kontrol klientů ve vaší Configuration Manager lokalitě.  

    Nakonfigurujte výstrahy, které vás upozorní, když výsledky kontroly klienta nebo aktivita klienta poklesne pod zadané procento. Tato lokalita může také upozorňovat na případ, kdy náprava selhává v zadaném procentu klientů. Další informace najdete v tématu [Postup konfigurace stavu klienta](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a>Kontroly stavu klienta

Kontrola klienta spustí následující kontroly a nápravy:  

|Kontrola klienta|Akce nápravy|Další informace|  
|------------------|------------------------|----------------------|  
|Ověření, jestli se kontrola klienta nedávno spustila|Spusťte kontrolu klienta.|Kontroluje, jestli se kontrola klienta spustila aspoň jednou za poslední tři dny.|  
|Ověření, jestli jsou požadavky klienta nainstalované|Nainstalujte požadavky klienta.|Kontroluje, jestli jsou nainstalované požadavky klienta. Přečte soubor ccmsetup.xml ve složce instalace klienta, kde zjistí požadavky.|  
|Test celistvosti úložiště WMI|Opětovná instalace klienta Configuration Manager|Kontroluje, zda jsou v rozhraní WMI přítomny Configuration Manager položky klienta.|  
|Ověření, jestli je služba klienta spuštěná|Spusťte službu klienta (Hostitel agenta serveru SMS).|Žádné další informace|  
|Test jímky událostí WMI|Restartujte službu klienta.|Zkontroluje, jestli je ztracená událost rozhraní WMI související s Configuration Manager.|  
|Ověření, jestli existuje služba WMI (Windows Management Instrumentation)|Žádná náprava|Žádné další informace|  
|Ověření, že byl klient nainstalovaný správně|Přeinstalujte klienta.|Žádné další informace|  
|Ověření, že typ spouštění antimalwarové služby je automatický|Změňte nastavení typu spouštění služby na hodnotu automaticky.|Žádné další informace|  
|Ověření, jestli je spuštěná antimalwarová služba|Spusťte antimalwarovou službu.|Žádné další informace|  
|Ověření, jestli typ spouštění služby Windows Update je automatický nebo ruční|Změňte nastavení typu spouštění služby na hodnotu automaticky.|Žádné další informace|  
|Ověření, že typ spouštění služby klienta (Hostitel agenta serveru SMS) je automatický|Změňte nastavení typu spouštění služby na hodnotu automaticky.|Žádné další informace|  
|Ověření, jestli je spuštěná služba WMI (Windows Management Instrumentation)|Spusťte službu WMI (Windows Management Instrumentation).|Žádné další informace|  
|Ověření stavu databáze Microsoft SQL CE|Opětovná instalace klienta Configuration Manager|Žádné další informace|  
|Test integrity rozhraní WMI služby Microsoft Policy Platform|Oprava služby Microsoft Policy Platform|Žádné další informace|  
|Ověřte, že služba Microsoft Policy Platform existuje.|Oprava služby Microsoft Policy Platform|Žádné další informace|  
|Ověřte, že typ spouštění služby Microsoft Policy Platform je ruční.|Změňte nastavení typu spouštění služby na hodnotu ručně.|Žádné další informace|  
|Ověření, jestli existuje služba Background Intelligent Transfer Service|Žádná náprava|Žádné další informace|  
|Ověření, že typ spouštění služby Background Intelligent Transfer Service je automatický nebo ruční|Změňte nastavení typu spouštění služby na hodnotu automaticky.|Žádné další informace|  
|Ověření, že typ spouštění služby Network Inspection Service je ruční|Změňte nastavení typu spouštění služby na hodnotu ručně, pokud je nainstalovaná.|Žádné další informace|  
|Ověření, že typ spouštění služby WMI (Windows Management Instrumentation) je automatický|Změňte nastavení typu spouštění služby na hodnotu automaticky.|Žádné další informace|  
|Ověření, že typ spouštění služby web Windows Update v zařízeních se systémem Windows 8 je automatický nebo ruční|Změňte nastavení typu spouštění služby na hodnotu ručně.|Žádné další informace|  
|Ověření, jestli existuje služba klienta (Hostitel agenta serveru SMS)|Žádná náprava|Žádné další informace|  
|Ověření, že typ spouštění služby vzdáleného řízení nástroje Configuration Manager je automatický nebo ruční|Změňte nastavení typu spouštění služby na hodnotu automaticky.|Žádné další informace|  
|Ověření, jestli je spuštěna služba vzdáleného řízení nástroje Configuration Manager|Spusťte službu vzdáleného řízení.|Žádné další informace|  
|Ověření, jestli je spuštěná služba proxy probuzení (Proxy probuzení nástroje ConfigMgr)|Spusťte službu Proxy probuzení nástroje ConfigMgr.|Tato kontroly klienta se provádí pouze v případě, že nastavení klienta **řízení spotřeby**: **Povolit proxy probuzení** je nastaveno na **hodnotu Ano** v podporovaných klientských operačních systémech.|  
|Ověření, že typ spouštění služby proxy probuzení (Proxy probuzení nástroje ConfigMgr) je automatický|Změňte nastavení typu spouštění služby Proxy probuzení nástroje ConfigMgr na hodnotu automaticky.|Tato kontroly klienta se provádí pouze v případě, že nastavení klienta **řízení spotřeby**: **Povolit proxy probuzení** je nastaveno na **hodnotu Ano** v podporovaných klientských operačních systémech.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Soubory protokolu nasazení klienta

Další informace o souborech protokolu používaných při nasazení klienta a operacích správy najdete v tématu [soubory protokolů](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
