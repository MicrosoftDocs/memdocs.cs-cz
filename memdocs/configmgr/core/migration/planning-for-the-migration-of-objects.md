---
title: Migrace objektů
titleSuffix: Configuration Manager
description: Naučte se plánovat migraci objektů mezi hierarchiemi v Configuration Managerm aktuálním prostředí pobočky.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 996cff4b8b333a59b774afb979bbdd89aae536a1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692889"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Plánování migrace Configuration Managerch objektů do Configuration Manager aktuální větev

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager aktuální větve můžete migrovat mnoho různých objektů, které jsou přidruženy k různým funkcím, které se nacházejí ve zdrojové lokalitě.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Plánování migrace aktualizací softwaru  
 Můžete migrovat objekty aktualizace softwaru, jako jsou balíčky aktualizací softwaru a nasazení aktualizací softwaru.  

 Chcete-li úspěšně migrovat objekty aktualizace softwaru, je třeba nejprve nastavit cílovou hierarchii s konfiguracemi, které odpovídají vašemu prostředí zdrojové hierarchie. To vyžaduje následující akce:  

-   Nasadit aktivní bod aktualizace softwaru v cílové hierarchii  

-   Nastavení katalogu produktů a jazyků, aby odpovídaly konfiguraci vaší zdrojové hierarchie  

-   Synchronizace bodu aktualizace softwaru v cílové hierarchii s Windows Server Update Services (WSUS)  

Když migrujete aktualizace softwaru, zohledněte následující poznámky:  

-   Migrace objektů aktualizací softwaru může selhat, pokud jste nesynchronizované informace v cílové hierarchii tak, aby odpovídaly konfiguraci zdrojové hierarchie.  

    > [!WARNING]  
    >  Configuration Manager nepodporuje použití nástroje WSUSutil pro synchronizaci dat mezi zdrojovou a cílovou hierarchií.  

-   Nemůžete migrovat vlastní aktualizace, které jsou publikované pomocí nástroje System Center Updates Publisher. Místo toho se musí vlastní aktualizace znova publikovat v cílové hierarchii.  

Když migrujete ze zdrojové hierarchie Configuration Manager 2007, proces migrace změní některé objekty aktualizace softwaru na formát používaný cílovou hierarchií. Následující tabulka vám může posloužit k plánování migrace objektů aktualizací softwaru z Configuration Manager 2007.  

|Objekt Configuration Manager 2007|Název objektu po migraci|  
|-----------------------------------|---------------------------------|  
|Seznamy aktualizací softwaru|Seznamy aktualizací softwaru se převedou na skupiny aktualizací softwaru.|  
|Nasazení aktualizací softwaru|Nasazení aktualizací softwaru se převedou na skupiny nasazení a aktualizací.<br /><br /> Po migraci nasazení aktualizace softwaru z Configuration Manager 2007 je musíte povolit v cílové hierarchii, aby ji bylo možné nasadit.|  
|Balíčky aktualizací softwaru|Balíčky aktualizací softwaru zůstávají dále balíčky aktualizací softwaru.|  
|Šablony aktualizací softwaru|Šablony aktualizací softwaru zůstávají dále šablonami aktualizací softwaru.<br /><br /> Hodnota **doby trvání** v šablonách nasazení Configuration Manager 2007 se nemigruje.|  

Při migraci objektů z nástroje System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větve nejsou objekty aktualizací softwaru změněny.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Plánování migrace obsahu  
 Obsah můžete migrovat z podporované zdrojové hierarchie do svojí cílové hierarchie. V případě zdrojové hierarchie Configuration Manager 2007 zahrnuje tento obsah balíčky distribuce softwaru a programy a virtuální aplikace, jako je Microsoft Application Virtualization (App-V). Pro System Center 2012 Configuration Manager a Configuration Manager aktuální zdrojové hierarchie větví zahrnuje tento obsah aplikace a virtuální aplikace App-V. Když migrujete obsah mezi hierarchiemi, zkomprimované zdrojové soubory se migrují do cílové hierarchie.  

### <a name="packages-and-programs"></a>Balíčky a programy  
 Když migrujete balíčky a programy, tyto se migrací nezmění. Před migrací je však nutné nastavit každý balíček tak, aby používal cestu UNC (Universal Naming Convention) k umístění zdrojového souboru. Jako součást konfigurace pro migraci balíčků a programů musíte určit lokalitu v cílové hierarchii pro správu tohoto obsahu. Obsah se nemigruje z přiřazené lokality, ale po migraci má přiřazená lokalita přístup k původnímu umístění zdrojového souboru pomocí mapování UNC.  

 Když migrujete balíček a program do cílové hierarchie a když migrace ze zdrojové hierarchie zůstane aktivní, můžete zpřístupnit obsah klientům v této hierarchii pomocí sdíleného distribučního bodu. Aby bylo možné používat sdílený distribuční bod, obsah musí zůstat přístupný v distribučním bodě ve zdrojové lokalitě. Další informace o sdílených distribučních bodech najdete v tématu [Sdílení distribučních bodů mezi zdrojovými a cílovými hierarchiemi](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) v tématu [Plánování strategie migrace nasazení obsahu](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 Pokud se v případě změny verze obsahu ve zdrojové hierarchii nebo v cílové hierarchii změní verze obsahu, klienti již nebudou moci přistupovat k obsahu ze sdíleného distribučního bodu v cílové hierarchii. V tomto scénáři je nutné znovu migrovat obsah a obnovit konzistentní verzi balíčku mezi zdrojovou a cílovou hierarchií. Tyto informace se synchronizují během cyklu shromažďování dat.  

> [!TIP]  
>  Pro každý balíček, který migrujete, aktualizujte balíček v cílové hierarchii. Tato akce může zabránit problémům s nasazením balíčku do distribučních bodů v cílové hierarchii. Když ale aktualizujete balíček v distribučním bodu v cílové hierarchii, klienti v této hierarchii už nebudou moct získat tento balíček ze sdíleného distribučního bodu. Chcete-li aktualizovat balíček v cílové hierarchii, v konzole Configuration Manager přejděte do knihovny softwaru, klikněte pravým tlačítkem na balíček a poté vyberte možnost **Aktualizovat distribuční body**. Proveďte tuto akci pro každý balíček, který migrujete.  

> [!TIP]  
> Pomocí nástroje Package Conversion Manager můžete převést balíčky a programy na aplikace Configuration Manager. Další informace najdete v tématu [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Virtuální aplikace  
Když migrujete balíčky sady App-V z podporované lokality Configuration Manager 2007, proces migrace je převede na aplikace v cílové hierarchii. Kromě toho se v závislosti na stávající reklamě pro balíček sady App-V vytvoří v cílové hierarchii následující typy nasazení:  

-   Pokud se nevyskytuje žádné inzerování, vytvoří se jeden typ nasazení, který používá výchozí nastavení.  

-   Pokud existuje jedno inzerování, vytvoří se jeden typ nasazení, který používá stejné nastavení jako inzerování Configuration Manager 2007.  

-   Pokud existuje víc inzerování, vytvoří se pro každou inzerci Configuration Manager 2007 typ nasazení s použitím nastavení pro toto inzerování.  

> [!IMPORTANT]  
>  Pokud migrujete dříve migrovaný balíček Configuration Manager 2007 sady App-V, migrace se nezdařila, protože balíčky virtuálních aplikací nepodporují chování přepsání migrace. V tomto případě musíte vymazat migrovaný balíček virtuální aplikace z cílové hierarchie a pak vytvořit novou úlohu migrace virtuální aplikace.  

> [!NOTE]  
>  Po dokončení migrace balíčku sady App-V můžete použít Průvodce aktualizací obsahu ke změně zdrojové cesty pro typy nasazení sady App-V. Další informace o tom, jak aktualizovat obsah pro typ nasazení, najdete v tématu Správa typů nasazení v tématu [úlohy správy pro Configuration Manager aplikace](../../apps/deploy-use/management-tasks-applications.md).  

Když migrujete ze služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větví, můžete kromě typů nasazení App-V a aplikací migrovat objekty pro virtuální prostředí App-V. Další informace o prostředí App-V najdete v tématu [nasazení virtuálních aplikací App-v](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Inzerování  
Reklamu z podporované zdrojové lokality Configuration Manager 2007 můžete migrovat do cílové hierarchie pomocí migrace založené na kolekcích. Pokud upgradujete klienta, historie dřív spuštěných inzerování se zachová pro ochranu klienta před opětným spuštěním migrovaných inzerování.  

> [!NOTE]  
>  Inzerování pro virtuální balíčky se nedá migrovat. Toto je výjimka v migraci inzerování.  

### <a name="applications"></a>Aplikace  
 Můžete migrovat aplikace z podporovaného Configuration Manager System Center 2012 nebo Configuration Manager aktuální zdrojové hierarchie větve do cílové hierarchie. Pokud znova přidělíte klienta ze zdrojové hierarchie do cílové hierarchie, klient zachová historii dřív nainstalovaných aplikací pro ochranu klienta před opětným spuštěním migrované aplikace.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Plánování migrace kolekcí  
 Můžete migrovat kritéria pro kolekce z podporovaného nástroje System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větve. V takovém případě použijete úlohu migrace založenou na objektech. Když migrujete kolekci, migrujete pravidla kolekce a ne informace o členech kolekce nebo informace o objektech vztahujících se k členům kolekce.  

 Migrace objektu kolekce není podporovaná, když migrujete ze zdrojové hierarchie Configuration Manager 2007.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Plánování migrace nasazení operačních systémů  
Z podporované zdrojové hierarchie můžete migrovat následující objekty nasazení operačních systémů:  

-   Image a balíčky operačních systémů. Zdrojová cesta spouštěcích imagí je aktualizována na výchozí umístění bitové kopie pro sadu Windows Administrative Installation Kit (Windows AIK) v cílové lokalitě. Dole jsou uvedené požadavky a omezení migrace imagí a balíčků operačních systémů:  

    -   K úspěšné migraci souborů imagí musí účet počítače serveru poskytovatele SMS pro lokalitu nejvyšší úrovně v cílové hierarchii mít oprávnění **ke čtení** a **zápisu** do zdrojových souborů IMAGÍ umístění sady Windows AIK zdrojové lokality.  

    -   Když migrujete instalační balíček operačního systému, zajistěte, aby konfigurace balíčku ve zdrojové lokalitě odkazovala na složku, která obsahuje soubor WIM, a ne na samotný soubor WIM. Pokud instalační balíček bude směřovat k souboru WIM, migrace instalačního balíčku nebude úspěšná.  

    -   Když migrujete balíček spouštěcích imagí ze zdrojové lokality Configuration Manager 2007, ID balíčku balíčku se v cílové lokalitě nezachová. Důsledkem je, že klienti v cílové hierarchii nemohou používat balíčky spouštěcích imagí, které jsou dostupné ve sdílených distribučních bodech.  

-   Sekvence úloh. Když migrujete pořadí úkolů, které obsahuje odkaz na klientský instalační balíček, tento odkaz se nahradí odkazem na klientský instalační balíček cílové hierarchie.  

    > [!NOTE]  
    >  Při migraci pořadí úkolů může Configuration Manager migrovat objekty, které nejsou v cílové hierarchii požadovány. Mezi tyto objekty patří spouštěcí bitové kopie a instalační balíčky klienta Configuration Manager 2007.  

-   Ovladače a balíčky ovladačů. Když migrujete balíčky ovladačů, účet počítače poskytovatele služby SMS v cílové hierarchii musí mít oprávnění Úplné řízení ke zdroji balíčku.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Plánování migrace správy požadovaných konfigurací  
Migrovat můžete položky konfigurace a základní údaje konfigurace.  

> [!NOTE]  
>  Neinterpretované položky konfigurace z Configuration Manager 2007 zdrojové hierarchie se pro migraci nepodporují. Tyto položky konfigurace nejde migrovat nebo importovat do cílové hierarchie. Další informace o neinterpretované položkách konfigurace najdete v tématu neinterpretované položky konfigurace v tématu [o položkách konfigurace v tématu o konfiguraci požadovaných konfigurací](/previous-versions/system-center/configuration-manager-2007/bb694136(v=technet.10)#uninterpreted-configuration-item) v knihovně dokumentace k nástroji Configuration Manager 2007.  

Můžete importovat konfigurační balíčky Configuration Manager 2007. Proces importu automaticky převede konfigurační balíčky tak, aby byly kompatibilní s Configuration Manager aktuální větev.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Plánování migrace hranic  
 Hranice mezi hierarchiemi můžete migrovat. Když migrujete hranice z Configuration Manager 2007, každá hranice ze zdrojové lokality se migruje současně a přidá se do nové skupiny hranic, která je vytvořená v cílové hierarchii. Při migraci hranic z verze System Center 2012 Configuration Manager nebo Configuration Manager aktuální hierarchie větví se každá vybraná hranice přidá do nové skupiny hranic v cílové hierarchii.  

 U každé automaticky vytvořené skupiny hranic je povolené umístění obsahu, ale ne přiřazení lokality. To brání překrývání hranic při přiřazování lokalit mezi zdrojovou a cílovou hierarchií. Když migrujete ze zdrojové lokality Configuration Manager 2007, pomůže vám to zabránit novým klientům Configuration Manager 2007, kteří se instalují z nesprávně přidružování k cílové hierarchii. Ve výchozím nastavení Configuration Manager klienti aktuální větve automaticky nepřiřazují k lokalitám Configuration Manager 2007.  

 Když při migraci sdílíte distribuční bod s cílovou hierarchií, veškeré hranice přiřazené k příslušné distribuci se automaticky migrují do cílové hierarchie. V cílové hierarchii migrace vytvoří pro každý sdílený distribuční bod novou skupinu hranic určenou jen pro čtení. Pokud změníte hranice u distribučního bodu ve zdrojové hierarchii, skupina hranic v cílové hierarchii implementuje tyto změny v průběhu příštího cyklu shromažďování.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> Plánování migrace sestav  
Configuration Manager nepodporuje migraci sestav. Místo toho můžete pomocí nástroje Tvůrce sestav služby SQL Server Reporting Services exportovat sestavy ze zdrojové hierarchie, a následně je importovat do cílové hierarchie.  

> [!NOTE]  
>  Vzhledem k tomu, že existují změny schématu pro sestavy mezi Configuration Manager 2007 a Configuration Manager aktuální větve, otestujte každou sestavu, kterou importujete z hierarchie Configuration Manager 2007, aby se zajistilo, že funguje podle očekávání.  

Další informace o vytváření sestav najdete v tématu [Úvod do vytváření sestav](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> Plánování migrace organizačních složek a složek výsledků hledání  
 Organizační složky a složky hledání můžete migrovat z podporované zdrojové hierarchie do cílové. Z nástroje System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větví můžete navíc migrovat kritéria uložených hledání do cílové hierarchie.  

 Proces migrace ve výchozím nastavení zachovává strukturu složek hledání a správních složek objektů a kolekcí. V Průvodci vytvořením úlohy migrace ale na stránce **Nastavení** můžete nastavit úlohu migrace, která nemigruje organizační strukturu pro objekty, tak, že zrušíte registraci pole pro tuto možnost. Organizační struktury kolekcí se vždycky zachovají.  

 Jednu výjimku představuje složka hledání obsahující virtuální aplikace. Při migraci balíčku App-V se balíček sady App-V transformuje do aplikace v Configuration Manager. Po migraci složky výsledků hledání se najde jenom zbývající balíčky a složka výsledků hledání nemůže najít balíček sady App-V, protože tento převod na aplikaci v případě migrace balíčku sady App-V.  

 Při migraci uloženého hledání ze služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větve migrujete kritéria hledání a nikoli informace o výsledcích hledání. Migraci uloženého hledání nelze použít ze zdrojové lokality Configuration Manager 2007.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Plánování migrace funkce Asset Intelligence přizpůsobení  
 Přizpůsobení funkce Asset Intelligence můžete migrovat z podporované zdrojové hierarchie do cílové. Ve struktuře funkce Asset Intelligence přizpůsobení mezi Configuration Manager 2007 a Configuration Manager aktuální větví nejsou žádné významné změny.  

> [!NOTE]  
> Configuration Manager aktuální větev nepodporuje migraci objektů funkce Asset Intelligence z webu Configuration Manager 2007, který používá funkce Asset Intelligence Service 2,0 (AIS 2,0).  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Plánování migrace přizpůsobení pravidel monitorování míry využívání softwaru  
 Měření softwaru mezi Configuration Manager 2007 a Configuration Manager aktuální větví nejsou významné změny. Pravidla monitorování míry využití softwaru můžete migrovat z podporované zdrojové hierarchie do cílové.  

 Pravidla monitorování míry využití softwaru migrovaná do cílové hierarchie se ve výchozím nastavení nepřiřadí k určité lokalitě cílové hierarchie, ale vztahují se na všechny klienty v hierarchii. Pokud chcete pravidlo monitorování míry využití softwaru vztáhnout na klienty v určité lokalitě, musíte ho po migraci upravit.