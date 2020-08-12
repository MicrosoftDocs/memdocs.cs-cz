---
title: Diagnostická data pro 1511
titleSuffix: Configuration Manager
description: Přečtěte si o úrovních diagnostiky a dat o využití, které shromažďuje Configuration Manager verze 1511.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94166557b07050706401c122b835579762bfa982
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128827"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-configuration-manager"></a>Úrovně shromažďování diagnostických dat o využití pro verzi 1511 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager verze 1511 shromažďuje tři úrovně diagnostiky a dat o využití: **základní**, **Rozšířená**a **plná**. Ve výchozím nastavení má tato funkce nastavenou úroveň Rozšířená. Následující části obsahují další podrobnosti o datech, která jednotlivé úrovně shromažďují.  

> [!IMPORTANT]  
>  Configuration Manager neshromažďuje kódy lokalit, názvy lokalit, IP adresy, uživatelská jména, názvy počítačů, fyzické adresy ani e-mailové adresy na úrovních Basic a Enhanced. Jakékoli shromažďování těchto informací na úrovni Úplná není záměrné, to znamená, že mohou být zahrnuty do rozšířených diagnostických informací, jako jsou soubory protokolu nebo snímky paměti. Společnost Microsoft nebude tyto informace používat k tomu, aby vás identifikovala, kontaktovala vás nebo vyvinula reklamu.  

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Postup pro změnu úrovně  
 Správci, kteří mají obor správy na základě rolí, který zahrnuje oprávnění **změnit** u třídy objektů **lokalita** , můžou měnit úroveň dat shromažďovaných pomocí nastavení dat o diagnostice a dat o využití v konzole Configuration Manager.

 Provedete to tak, že v konzole přejdete na kartu Backstage (levá horní karta se šipkou rozevíracího seznamu), vyberete **data o využití**a pak vyberete úroveň dat, kterou chcete použít.  


##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Úroveň 1 – Základní  
 Základní úroveň zahrnuje data o vaší hierarchii, data potřebná k vylepšení instalace nebo upgradu a data, která pomáhají určit Configuration Manager aktualizace, které jsou použitelné pro vaši hierarchii.  

 Od verze Configuration Manager 1511 Tato úroveň zahrnuje následující:  


-   Informace o instalaci
    - Sestavení, typ instalace, jazykové sady a funkce, které jste povolili

    - Stav nasazení balíčku aktualizací a chyby  

-   Metriky výkonu databáze (informace o zpracování replikace, hlavní SQL Server uložené procedury podle procesoru a využití disku)  

-   Základní konfigurace databáze (procesory, konfigurace clusteru a konfigurace distribuovaných zobrazení)  

-   Configuration Manager schéma databáze (hodnota hash všech definic objektů)  

-   Počet Configuration Manager verzí klienta a verzí operačního systému  

-   Počet operačních systémů pro spravovaná zařízení a zásady nastavené konektorem Exchange  

-   Počet jazyků a národních prostředí klienta

-   Počet zařízení s Windows 10 podle větve a sestavení  

-   Základní Configuration Manager data hierarchie lokality (seznam lokalit, typ, verze, stav, počet klientů a časové pásmo)  

-   Základní informace o serveru systému lokality (použité role systému lokality, stav Internetu a protokolu SSL, operační systém, procesory a fyzický nebo virtuální počítač)  

-   Základní statistické údaje o zjišťování uživatelů (počet zjišťování uživatelů a minimální/maximální/průměrné velikosti skupin)  

-   Základní informace o Endpoint Protection (verze antimalwarového klienta)  

-   Základní počty typů aplikací a nasazení (celkový počet aplikací, celkový počet aplikací s více typy nasazení, celkový počet aplikací se závislostmi, celkový počet nahrazených aplikací a počet používaných technologií nasazení)  

-   Počty základních nasazení operačního systému (OSD) (Image)  

-   Typy distribučních bodů a bodů správy a informace o základní konfiguraci (chráněné, připravené, PXE, vícesměrové vysílání, stav protokolu SSL, distribuční body pro vyžádání obsahu, podpora MDM, povolený protokol SSL atd.)  

-   Statistiky telemetrie (při spuštění, za běhu a chyby)  

##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Úroveň 2 – Rozšířená  
Rozšířená úroveň je výchozí po dokončení instalace. Tato úroveň zahrnuje data shromážděná na úrovni Basic, data specifická pro jednotlivé funkce (četnost a doba použití), Configuration Manager nastavení klienta (název komponenty, stav a určitá nastavení jako intervaly cyklického dotazování) a základní informace o aktualizacích softwaru.  

Tato úroveň se doporučuje, protože poskytuje Microsoftu minimální data, která je potřeba k tomu, aby v budoucích verzích produktů a služeb poskytovala užitečná vylepšení. Tato úroveň neshromažďuje názvy objektů (lokalit, uživatelů, počítačů ani objektů), podrobnosti o objektech souvisejících se zabezpečením nebo ohrožení zabezpečení, jako je počet systémů, které vyžadují aktualizace softwaru.  

Od verze Configuration Manager 1511 Tato úroveň zahrnuje následující:  

-   **Správa aplikací:**  

    -   Základní informace o využití/cílení pro typy nasazení, které se používají v rámci organizace (cílení na zařízení, a vyžaduje se a je k dispozici)  

    -   Informace o nasazení aplikace (instalace/odinstalace, vyžaduje schválení a povolená nebo zakázaná interakce s uživatelem)  

    -   Dostupné statistiky žádostí aplikace  

    -   Počet balíčků podle typu  

    -   Počet využitelných aplikací podle operačního systému  

    -   Počet nasazení balíčku/programu  

    -   Počet prostředí App-V a vlastností nasazení  

    -   Počet licencí na aplikace systému Windows 10  

    -   Minimální, maximální a průměrný počet nasazení aplikací na uživatele a zařízení  

    -   Typ a doba trvání časového období údržby  

-   **Služba**  

    -   Seznam/počet povolených klientských agentů  

    -   Počet instalací klientů z každého typu zdrojového umístění  

    -   Počet chyb instalace klientů  

-   **Nastavení dodržování předpisů:**  

    -   Počet položek konfigurace podle typu  

    -   Základní standardní hodnoty konfigurace (celkový počet, počet nasazení a počet odkazů)  

    -   Počet nasazení, která odkazují na předdefinovaná nastavení (hodnota nastavení není zachycena)  

    -   Počet pravidel a nasazení vytvořených pro vlastní nastavení  

    -   Počet nasazených šablon Simple Certificate Enrollment Protocol  

-   **Sušin**  

    -   Počet hranic podle typu  

    -   Informace o skupině hranic (počet hranic a systémů lokality, které jsou přiřazeny ke každé skupině hranic)  

    -   Informace o skupině distribučních bodů (počet balíčků a distribučních bodů, které jsou přiřazeny ke každé skupině distribučních bodů)  

    -   Informace o konfiguraci distribučního bodu (použití sledování mezipaměti větví a distribučního bodu)  

    -   Informace o konfiguraci Správce distribuce (vlákna, zpoždění opakování, počet opakovaných pokusů a nastavení distribučního bodu pro vyžádání obsahu)  

-   **Endpoint Protection:**  

    -   Použití zásad Endpoint Protection antimalwaru a brány Windows Firewall (počet jedinečných zásad přiřazených ke skupině)<br /><br />Nezahrnuje žádné informace o nastaveních, která jsou součástí zásad.  

    -   Endpoint Protection chyby nasazení (počet kódů chyb nasazení Endpoint Protection zásad)  

    -   Počet kolekcí vybraných k zobrazení na řídicím panelu Endpoint Protection  

    -   Počet výstrah, které jsou nakonfigurované pro funkci Endpoint Protection  

-   **Správa mobilních aplikací (MAM):**  

    -   Počet aplikací Office s podporou MAM, obchodních aplikací a zásad podle operačního systému  

    -   Počet nasazení aplikací s funkcí MAM / zásad  

    -   Počet pravidel vytvořených pro nastavení MAM  

-   **Správa mobilních zařízení (MDM):**  

    -   Počet vydaných akcí mobilního zařízení: Lock, PIN REST, vymazání a vyřazení příkazů

    -   Počet mobilních zařízení spravovaných Configuration Manager a Microsoft Intune a způsob jejich registrace (hromadně nebo na základě uživatelů)  

    -   Plán cyklického dotazování mobilních zařízení a statistika pro dobu trvání kontroly mobilních zařízení  

    -   Počet zásad mobilních zařízení  

    -   Počet uživatelů, kteří mají více zaregistrovaných mobilních zařízení  

-   **Řešení potíží s Microsoft Intune:**  

    -   Počet a velikost stavu, stavu, inventáře, RDR, DDR, UDX, stavu klientů, POL, LOG, CERT, CRP, Resync, CFD, RDO, BEX, ISM a zpráv o dodržování předpisů, které se stahují z Microsoft Intune  

    -   Počet a velikost akcí zařízení (vymazání, vyřazení, uzamčení), telemetrie a datové zprávy, které se replikují Microsoft Intune  

    -   Statistika synchronizace úplných a rozdílných uživatelů pro Microsoft Intune  

-   **Místní správa mobilních zařízení (MDM):**  

    -   Statistika úspěchů nebo selhání nasazení aplikací s místní správou mobilních zařízení  

    -   Počet balíčků a profilů hromadné registrace systému Windows 10  

-   **Nasazení operačního systému:**  

    -   Počet spouštěcích imagí, ovladačů, balíčků ovladačů, distribučních bodů s podporou vícesměrového vysílání, distribučních bodů s podporou technologie PXE a pořadí úloh  

-   **Aktualizace softwaru:**  

    -   Celkový/průměrný počet kolekcí, které mají nasazení aktualizací softwaru, a maximální/průměrný počet nasazených aktualizací  

    -   Počet pravidel automatického nasazení, která jsou vázaná na synchronizaci  

    -   Počet pravidel automatického nasazení, která vytváří nové aktualizace nebo přidává aktualizace do stávající skupiny  

    -   Dostupné a rozdílové konečné termíny používané v pravidlech automatického nasazení  

    -   Průměrný a maximální počet přiřazení na aktualizaci  

    -   Počet aktualizací vytvořených a nasazených pomocí nástroje System Center Update Publisher  

    -   Počet skupin aktualizací a přiřazení  

    -   Počet balíčků aktualizací a maximální/minimální/průměrný počet distribučních bodů, které jsou zaměřeny na balíčky  

    -   Počet skupin aktualizací a minimální/maximální/průměrný počet aktualizací na skupinu  

    -   Počet aktualizací a procento aktualizací, které jsou nasazeny, vypršela platnost, nahrazeny, stáhly a obsahují smlouvy EULA  

    -   Počet chybových kódů kontroly aktualizací a počet počítačů  

    -   Plány vyhodnocování aktualizací klientů a kontrol  

    -   Plán synchronizace bodu aktualizace softwaru  

    -   Počet pravidel automatického nasazení s více nasazeními  

    -   Konfigurace, které se používají pro aktivní plány údržby Windows 10  

    -   Verze obsahu řídicího panelu systému Windows 10  

    -   Počet klientů s Windows 10, kteří používají web Windows Update pro firmy  

    -   Statistiky použití dílčích oprav clusteru  

    -   Počet nasazených aktualizací služeb Office 365  

-   **Údaje o SQL a výkonu**  

    -   Počet největších databázových tabulek  

    -   Informace o replice SQL AlwaysOn  

    -   Počet kolekcí podle typu  

##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Úroveň 3 – Úplná  
Úplná úroveň zahrnuje všechna data na úrovni Basic a Enhanced. Obsahuje také další informace o řešení funkci Endpoint Protection, procenta dodržování předpisů pro aktualizace a informace o aktualizacích softwaru. Tato úroveň může zahrnovat taky rozšířené diagnostické informace, jako jsou systémové soubory a snímky paměti, které můžou zahrnovat osobní informace, které existovaly v paměti nebo souborech protokolu v době zachycení.  

Od verze Configuration Manager 1511 Tato úroveň zahrnuje následující:  

-   Hodnocení kolekcí a statistiky obnovení  

-   Souhrn stavu funkce Endpoint Protection (včetně počtu chráněných, ohrožených, neznámých a nepodporovaných klientů)  

-   Konfigurace zásad funkce Endpoint Protection  

-   Informace o nasazení aktualizací softwaru (procento nasazení cílených na klienta vs. čas UTC, povinná oproti volitelnému i tichému a potlačení restartování)  

-   Celkové dodržování předpisů pro nasazení aktualizací softwaru  

-   Informace o plánu hodnocení pravidel automatického nasazení  

-   Počet klientů, kteří mají zásady ochrany přístupu k síti  

-   Kódy a počty chyb nasazení aktualizací softwaru  

-   Minimální/maximální/průměrný počet neaktivních klientů v kolekcích nasazení aktualizací softwaru  

-   Počet skupin, u kterých vypršela platnost aktualizací softwaru  

-   Minimální/maximální/průměrný počet aktualizací softwaru na balíček  

-   Procenta úspěšnosti kontroly aktualizací softwaru  

-   Minimální/maximální/průměrný počet hodin od poslední kontroly aktualizací softwaru  
