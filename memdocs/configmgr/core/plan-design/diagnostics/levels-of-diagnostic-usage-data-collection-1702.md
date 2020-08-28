---
title: Diagnostická data pro 1702
titleSuffix: Configuration Manager
description: Přečtěte si o úrovních diagnostiky a dat o využití, které shromažďuje Configuration Manager verze 1702.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: d43ab033-2902-4681-8716-b4b17a6df372
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c3859d77726b49973257da47233fedde28f705a1
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994816"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1702-of-configuration-manager"></a>Úrovně shromažďování diagnostických dat o využití pro verzi 1702 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager verze 1702 shromažďuje tři úrovně diagnostiky a dat o využití: **základní**, **Rozšířená**a **plná**. Ve výchozím nastavení má tato funkce nastavenou úroveň Rozšířená. Následující části obsahují další podrobnosti o datech, která jednotlivé úrovně shromažďují.

Změny z předchozích verzí jsou označeny ***[New]***, ***[Aktualizováno]***, ***[odebrané]*** nebo ***[přesunuté]***.


> [!IMPORTANT]
>  Configuration Manager neshromažďuje kódy lokalit, názvy lokalit, IP adresy, uživatelská jména, názvy počítačů, fyzické adresy ani e-mailové adresy na úrovních Basic a Enhanced. Jakékoli shromažďování těchto informací na úrovni Úplná není záměrné, to znamená, že mohou být zahrnuty do rozšířených diagnostických informací, jako jsou soubory protokolu nebo snímky paměti. Společnost Microsoft nebude tyto informace používat k tomu, aby vás identifikovala, kontaktovala vás nebo vyvinula reklamu.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Postup pro změnu úrovně
 Správci, kteří mají obor správy na základě rolí, který zahrnuje oprávnění **změnit** u třídy objektů **lokalita** , můžou měnit úroveň dat shromažďovaných pomocí nastavení dat o diagnostice a dat o využití v konzole Configuration Manager.

Úroveň shromažďování dat můžete změnit v konzole nástroje tak, že přejdete do části **Správa**  >  **Přehled**  >  **Konfigurace**  >  **lokality lokality**. Otevřete **Nastavení hierarchie**a pak vyberte úroveň dat, kterou chcete použít.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Úroveň 1 – Základní
Základní úroveň zahrnuje data o vaší hierarchii, data potřebná k vylepšení instalace nebo upgradu a data, která pomáhají určit Configuration Manager aktualizace, které jsou použitelné pro vaši hierarchii.

Pro Configuration Manager verze 1702 Tato úroveň zahrnuje následující:

- Konzola správce:
   - Statistika o připojeních konzoly (verze operačního systému, jazyk, SKU a architektura, systémová paměť, počet logických procesorů, připojení ID lokality, nainstalované verze rozhraní .NET a jazykové sady konzoly)

- Základní počty typů aplikací a nasazení (celkový počet aplikací, celkový počet aplikací s více typy nasazení, celkový počet aplikací se závislostmi, celkový počet nahrazených aplikací a počet používaných technologií nasazení)

- Základní Configuration Manager data hierarchie lokality (seznam lokalit, typ, verze, stav, počet klientů a časové pásmo)

- Základní konfigurace databáze (procesory, konfigurace clusteru a konfigurace distribuovaných zobrazení)

- ***[Aktualizováno]*** Základní statistické údaje zjišťování (počet zjišťování a minimální/maximální/průměrné velikosti skupin), včetně, kdy web běží zcela s Azure Active Directory službami.

- Základní informace o Endpoint Protection (verze antimalwarového klienta)

- Počty základních nasazení operačního systému (OSD) (Image)

- Základní informace o serveru systému lokality (použité role systému lokality, stav Internetu a protokolu SSL, operační systém, procesory a fyzický nebo virtuální počítač)

- Configuration Manager schéma databáze (hodnota hash všech definic objektů)

- Nakonfigurovaná úroveň telemetrie, režim (online nebo offline) a konfigurace rychlé aktualizace

- Počet jazyků a národních prostředí klienta

- Počet Configuration Manager verzí klienta a verzí operačního systému

- Počet operačních systémů pro spravovaná zařízení a zásady nastavené konektorem Exchange

- Počet zařízení s Windows 10 podle větve a sestavení

- Metriky výkonu databáze (informace o zpracování replikace, hlavní uložené procedury systému SQL Server podle využití procesoru a disku)

- Typy distribučních bodů a bodů správy a informace o základní konfiguraci (chráněné, připravené, PXE, vícesměrové vysílání, stav protokolu SSL, distribuční body pro vyžádání obsahu, podpora MDM, povolený protokol SSL atd.)

- Informace o instalaci:
     - Sestavení, typ instalace, jazykové sady, funkce, které jste povolili   

     - Předběžná verze použití, nastavení typ média, typ větve

     - Datum vypršení platnosti Software Assurance      

     - Stav nasazení balíčku aktualizací a chyby, průběh stahování a chyby požadovaných součástí 

     - Použití aktualizačního kroužku aktualizací

     - Verze skriptu po upgradu

- Verze SQL, úroveň aktualizace Service Pack, edice, ID kolace a znaková sada     
- Telemetrické statistiky (při spuštění, za běhu, chyby)

- Použití zjišťování sítě (povolené nebo zakázané)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Úroveň 2 – Rozšířená
Rozšířená úroveň je výchozí po dokončení instalace. Tato úroveň zahrnuje data shromážděná v datech na úrovni Basic a na základě funkcí (četnost a doba použití), Configuration Manager nastavení klienta (název komponenty, stav a určitá nastavení jako intervaly dotazování) a základní informace o aktualizacích softwaru.

Tato úroveň se doporučuje, protože poskytuje Microsoftu minimální data, která je potřeba k tomu, aby v budoucích verzích produktů a služeb poskytovala užitečná vylepšení. Tato úroveň neshromažďuje názvy objektů (lokalit, uživatelů, počítačů ani objektů), podrobnosti o objektech souvisejících se zabezpečením nebo ohrožení zabezpečení, jako je počet systémů, které vyžadují aktualizace softwaru.

Pro Configuration Manager verze 1702 Tato úroveň zahrnuje následující:

- **Správa aplikací:**  

   - Požadavky na aplikace (počet vestavěných podmínek je odkazováno technologií nasazení)

   - Nahrazování aplikací, maximální hloubka řetězce

   - Statistika schválení aplikace a frekvence využití

   - ***[Aktualizováno]*** Informace o nasazení aplikace (použití instalace a odinstalace, vyžaduje schválení, povolený/zakázaný zásah uživatele, závislost, nahrazování a počet použití funkce chování při instalaci)  

   - Velikost zásad aplikace a statistika složitosti

   - Dostupné statistiky žádostí aplikace

   - ***[Nové]*** Základní informace o konfiguraci pro balíčky a programy (možnosti nasazení a příznaky programu)

   - Základní informace o využití/cílení pro typy nasazení, které se používají v rámci organizace (cílení na zařízení, požadováno vs k dispozici a univerzální aplikace)

   - Statistika hraničních skupin (počet rychlých, počtu pomalých a počtu na skupinu)

   - Počet prostředí App-V a vlastností nasazení

   - Počet využitelných aplikací podle operačního systému  

   - ***[Nové]*** Počet aplikací, na které se odkazuje v pořadí úkolů

   - Počet balíčků podle typu  

   - Počet nasazení balíčku/programu  

   - Počet licencí na aplikace systému Windows 10  

   - Počet aplikací pro Windows Store pro firmy a statistiky synchronizace (včetně souhrnných typů aplikací, stavu licencované aplikace a počtu online a offline licencovaných aplikací)  

   - Typ a doba trvání časového období údržby  

   - Minimální/maximální/průměrný počet nasazení aplikací na uživatele nebo zařízení za časové období

   - ***[Nové]*** Nejběžnější kódy chyb instalace aplikací podle technologie nasazení

   - Možnosti a počty konfigurace MSI

   - ***[Nové]*** Statistika interakce koncových uživatelů s oznámením pro požadovaná nasazení softwaru   

   - Použití univerzálního přístupu k datům (UDA), jak se vytvořilo




- **Služba**  

   - Verze klienta technologie AMT (Active Management Technology)

   - Stáří systému BIOS v rocích

   - Automatický upgrade klienta: konfigurace nasazení, včetně nasazení klienta a používání vyloučení (klient rozšířené kompatibility)

   - Konfigurace velikosti mezipaměti klienta

   - Chyby stahování nasazení klienta

   - Souhrnné informace o stavu klienta a hlavních potížích

   - Stav akce operace oznámení klienta (počet spuštěných časů, maximální počet cílových klientů a průměrná úspěšnost)
   - Počet instalací klientů z každého typu zdrojového umístění  

   - Počet chyb instalace klientů  

   - ***[Nové]*** Počet zařízení virtualizovaných technologií Hyper-V nebo Azure  

   - Počet akcí centra softwaru   

   - ***[Nové]*** Počet zařízení s podporou rozhraní UEFI

   - Metody nasazení používané pro klienta a počet klientů podle metody nasazení

   - Seznam/počet povolených klientských agentů  

   - Stáří operačního systému v měsících

   - Počet tříd inventáře hardwaru, pravidel inventáře softwaru a pravidel shromažďování souborů

   - ***[Nové]*** Statistika pro ověření stavu zařízení, včetně nejběžnějších kódů chyb, počtu místních serverů a počtů zařízení v různých stavech.



- **Cloud Services:**

  - Konfigurace a statistika využití Brána pro správu cloudu

  - ***[Nové]*** Počet klientů připojených ke službě Azure Active Directory Services

  - Počet kolekcí synchronizovaných v Operations Management Suite

  - Počet konektorů Upgrade Analytics

  - Zda je povolený cloudový konektor Operations Management Suite




- **Sbírk**

    - Využití ID kolekce (neběží mimo identifikátor)

    - Statistika vyhodnocení kolekce (čas dotazu, přiřazeno versus nepřiřazené počty, počty podle typu, Změna ID a použití pravidla)

    - Kolekce bez nasazení




- **Nastavení dodržování předpisů:**  

    - Základní standardní hodnoty konfigurace (celkový počet, počet nasazení a počet odkazů)  

    - Počet položek konfigurace podle typu  

    - Počet nasazení, která odkazují na vestavěná nastavení (teď se zachytí nastavení napravení)  

    - Počet pravidel a nasazení vytvořených pro vlastní nastavení (teď se zachytí nastavení opravit)  
    -  Počet nasazených šablon zásad dodržování předpisů pro Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certifikát (. pfx) a zásady dodržování předpisů

    - Počet certifikátů SCEP, VPN, Wi-Fi, certifikátu (. pfx) a nasazení zásad dodržování předpisů podle platformy

    - Zásady služby Passport for Work (vytvořené, nasazené)



- **Sušin**  

    - Informace o skupině hranic (počet hranic a systémů lokality, které jsou přiřazeny ke každé skupině hranic)  

    - Vztahy hraniční skupiny a záložní konfigurace

    - Statistika stažení obsahu klienta

    - Počet hranic podle typu  

    - Počet klientů sdílené mezipaměti a statistiky využití

    - Informace o konfiguraci Správce distribuce (vlákna, zpoždění opakování, počet opakovaných pokusů a nastavení distribučního bodu pro vyžádání obsahu)  

    - Informace o konfiguraci distribučního bodu (použití sledování mezipaměti větví a distribučního bodu)

    - Informace o skupině distribučních bodů (počet balíčků a distribučních bodů, které jsou přiřazeny ke každé skupině distribučních bodů)  



- **Endpoint Protection:**  

   - Zásady rozšířené ochrany před internetovými útoky (ATP) (počet zásad a to, jestli jsou nasazené zásady)

   - Počet výstrah, které jsou nakonfigurované pro funkci Endpoint Protection  

   - Počet kolekcí vybraných k zobrazení v Endpoint Protectionovém řídicím panelu  

   - Endpoint Protection chyby nasazení (počet kódů chyb nasazení Endpoint Protection zásad)  

   - Použití zásad Endpoint Protection antimalwaru a brány Windows Firewall (počet jedinečných zásad přiřazených ke skupině)<br /><br /> Nezahrnuje žádné informace o nastaveních obsažených v zásadách.  



- **Migrace**

  - Počet migrovaných objektů (použití Průvodce migrací)



- **Správa mobilních zařízení (MDM):**  

    - Počet vydaných akcí mobilního zařízení: uzamknout, připnout PIN REST, vymazat, vyřadit a synchronizovat nyní

    - Počet zásad mobilních zařízení  

    - Počet mobilních zařízení spravovaných Configuration Manager a Microsoft Intune a způsob jejich registrace (Hromadná, založená na uživatelích)  

    - Počet uživatelů, kteří mají více zaregistrovaných mobilních zařízení  

    - Plán cyklického dotazování mobilních zařízení a statistika pro dobu trvání vrácení se změnami mobilního zařízení  




- **Řešení potíží s Microsoft Intune:**

    - Počet a velikost akcí zařízení (vymazání, vyřazení, uzamčení), telemetrie a datové zprávy, které se replikují Microsoft Intune

    - Počet a velikost stavu, stavu, inventáře, RDR, DDR, UDX, stavu klientů, POL, LOG, CERT, CRP, Resync, CFD, RDO, BEX, ISM a zpráv o dodržování předpisů, které se stahují z Microsoft Intune

    - Statistika synchronizace úplných a rozdílných uživatelů pro Microsoft Intune



- **Místní správa mobilních zařízení (MDM):**  

    - Počet balíčků a profilů hromadné registrace systému Windows 10  

    - Statistika úspěchů nebo selhání nasazení aplikací s místní správou mobilních zařízení  




- **Nasazení operačního systému:**  

    - Počet spouštěcích imagí, ovladačů, balíčků ovladačů, distribučních bodů s podporou vícesměrového vysílání, distribučních bodů s podporou technologie PXE a pořadí úloh  

    - Počet zásad upgradu edice

    - Počty použití kroku pořadí úkolů



- **Aktualizace webu:**

    - Verze nainstalovaných oprav hotfix Configuration Manager



- **Aktualizace softwaru:**  

    - Dostupné a rozdílové konečné termíny používané v pravidlech automatického nasazení  

    - Průměrný a maximální počet přiřazení na aktualizaci  

    - Plány vyhodnocování aktualizací klientů a kontrol  

    - Klasifikace synchronizované bodem aktualizace softwaru

    - Statistiky použití dílčích oprav clusteru  

    - Konfigurace aktualizací Windows 10 Express

    - Konfigurace, které se používají pro aktivní plány údržby Windows 10  

    - Počet nasazených aktualizací Microsoft 365  

    - Počet skupin aktualizací a přiřazení  

    - Počet balíčků aktualizací a maximální/minimální/průměrný počet distribučních bodů, které jsou zaměřeny na balíčky  

    - Počet aktualizací vytvořených a nasazených pomocí programu System Center Update Publisher  

    - Počet klientů s Windows 10, kteří používají web Windows Update pro firmy  

    - Počet pravidel automatického nasazení, která jsou vázaná na synchronizaci  

    - Počet pravidel automatického nasazení, která vytváří nové aktualizace nebo přidává aktualizace do stávající skupiny  

    - Počet pravidel automatického nasazení s více nasazeními  
    - Počet skupin aktualizací a minimální/maximální/průměrný počet aktualizací na skupinu  

    - Počet aktualizací a procento aktualizací, které jsou nasazeny, vypršela platnost, nahrazeny, stáhly a obsahují smlouvy EULA  

    - Statistika vyrovnávání zatížení bodu aktualizace softwaru

    - Plán synchronizace bodu aktualizace softwaru  

    - Celkový/průměrný počet kolekcí, které mají nasazení aktualizací softwaru, a maximální/průměrný počet nasazených aktualizací  

    - Počet chybových kódů kontroly aktualizací a počet počítačů  

    - Verze obsahu řídicího panelu systému Windows 10  



- **Údaje o SQL a výkonu**  

    - ***[Nové]*** Konfigurace a trvání Shrnutí lokality

    - Počet největších databázových tabulek  

    - Provozní statistiky zjišťování (počet nalezených objektů)

    - Typy zjišťování, povolené a plánované (úplné, přírůstkové)

    - Informace o replice SQL AlwaysOn, využití a stav

    - Problémy s výkonem sledování změn SQL, doba uchování a stav automatického vyčištění

    - Doba uchování dat sledování změn SQL

    - ***[Nové]*** Statistika výkonu stavových a stavových zpráv, včetně nejběžnějších a nejdražších typů zpráv



- **Různé**

    - ***[Nové]*** Konfigurace bodu služby datového skladu, včetně plánu synchronizace a průměrného času

    - Počet lokalit pomocí funkce Wake on LAN (WOL)

    - Využití sestav a statistiky výkonu  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Úroveň 3 – Úplná
Úplná úroveň zahrnuje všechna data na úrovni Basic a Enhanced. Obsahuje také další informace o řešení funkci Endpoint Protection, procenta dodržování předpisů pro aktualizace a informace o aktualizacích softwaru.  Tato úroveň může zahrnovat taky rozšířené diagnostické informace, jako jsou systémové soubory a snímky paměti, které můžou zahrnovat osobní informace, které existovaly v paměti nebo souborech protokolu v době zachycení.

Pro Configuration Manager verze 1702 Tato úroveň zahrnuje následující:

- Informace o plánu hodnocení pravidel automatického nasazení

- Shrnutí stavu ATP

- Hodnocení kolekcí a statistiky obnovení

- Nastavení dodržování předpisů: Konfigurace protokolu SCEP, sítě VPN, Wi-Fi a zásad dodržování předpisů – podrobnosti o počtu skupin s prošlými aktualizacemi softwaru

- Konfigurační balíček DCM pro použití Configuration Manager

- Podrobné chyby instalace nasazení klienta
- Souhrn stavu funkce Endpoint Protection (včetně počtu chráněných, ohrožených, neznámých a nepodporovaných klientů)

- Konfigurace zásad funkce Endpoint Protection

- ***[Nové]*** Seznam procesů nakonfigurovaných s chováním při instalaci pro aplikace

- Minimální/maximální/průměrný počet hodin od poslední kontroly aktualizací softwaru

- Minimální/maximální/průměrný počet neaktivních klientů v kolekcích nasazení aktualizací softwaru

- Minimální/maximální/průměrný počet aktualizací softwaru na balíček

- Kód produktu MSI (společné aplikace, které zákazníci nasazují)

- Celkové dodržování předpisů pro nasazení aktualizací softwaru

- Kódy a počty chyb nasazení aktualizací softwaru

- Informace o nasazení aktualizací softwaru (procento nasazení cílených na klienta vs. čas UTC, povinná oproti volitelnému i tichému a potlačení restartování)

- Produkty aktualizace softwaru synchronizované bodem aktualizace softwaru

- Procenta úspěšnosti kontroly aktualizací softwaru

- Top 50 procesorů v prostředí

- Typ zásad podmíněného přístupu EAS (blokovat nebo umístit do karantény) pro zařízení, která Intune spravuje

- Podrobnosti o aplikaci Windows Store pro firmy (neagregovaný seznam synchronizovaných aplikací včetně AppID, online stavu nebo offline stavu a celkového počtu zakoupených licencí)
