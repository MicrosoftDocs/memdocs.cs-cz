---
title: Diagnostická data a data o využití pro 1802
titleSuffix: Configuration Manager
description: Seznamte se s úrovněmi diagnostiky a dat o využití shromážděných ve verzi 1802.
ms.date: 05/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 29dd51b8-6576-4010-81ba-3129ed2c3421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c2edff394e915273fb34f4627e3636ea6e20237c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710871"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1802-of-configuration-manager"></a>Úrovně shromažďování diagnostických dat o využití pro verzi 1802 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager verze 1802 shromažďuje tři úrovně diagnostiky a dat o využití: **základní**, **Rozšířená**a **plná**. Ve výchozím nastavení má tato funkce nastavenou úroveň Rozšířená. Následující části obsahují další podrobnosti o datech shromažďovaných na jednotlivých úrovních.

Změny z předchozích verzí jsou označeny ***[New]***, ***[Aktualizováno]***, ***[odebrané]*** nebo ***[přesunuté]***.


> [!IMPORTANT]
>  Configuration Manager neshromažďuje kódy lokalit, názvy lokalit, IP adresy, uživatelská jména, názvy počítačů, fyzické adresy ani e-mailové adresy na úrovních Basic a Enhanced. Žádná kolekce těchto informací na úrovni Úplná není záměrné. Je potenciálně součástí pokročilých diagnostických informací, jako jsou soubory protokolu nebo snímky paměti. Společnost Microsoft tyto informace nepoužívá k tomu, aby vás identifikovala, kontaktovala vás nebo vyvinula reklamu.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Postup pro změnu úrovně
 Správci, kteří mají obor správy na základě rolí, který zahrnuje oprávnění **změnit** u třídy objektů **lokalita** , můžou měnit úroveň dat shromažďovaných pomocí nastavení dat o diagnostice a dat o využití v konzole Configuration Manager.

Úroveň shromažďování dat můžete změnit v konzole nástroje tak, že přejdete do části **Správa** > **Přehled** > **Konfigurace** > **lokality lokality.** Otevřete **Nastavení hierarchie**a pak vyberte úroveň dat, kterou chcete použít.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Úroveň 1 – Základní
Základní úroveň zahrnuje data o vaší hierarchii, data potřebná k vylepšení instalace nebo upgradu a data, která pomáhají určit Configuration Manager aktualizace, které jsou použitelné pro vaši hierarchii.

Pro Configuration Manager verze 1802 Tato úroveň zahrnuje následující data:

- Statistika o připojeních konzoly Configuration Manager: verze OS, jazyk, SKU a architektura, systémová paměť, počet logických procesorů, připojení ID webu, nainstalované verze rozhraní .NET a jazykové sady konzoly

- Základní počty typů aplikací a nasazení: celkový počet aplikací, celkový počet aplikací s více typy nasazení, celkový počet aplikací se závislostmi, celkový počet nahrazených aplikací a počet používaných technologií nasazení

- Základní Configuration Manager data hierarchie lokality: seznam webů, typ, verze, stav, počet klientů a časové pásmo

- Základní konfigurace databáze: procesory, konfigurace clusteru a konfigurace distribuovaných zobrazení

- Základní statistické údaje zjišťování: počet zjišťování, minimální/maximální/průměrné velikosti skupin a pokud web běží zcela s Azure Active Directory službami

- Základní Endpoint Protection informace o verzích antimalwarového klienta

- Základní počty imagí nasazení operačního systému

- Základní informace o serveru systému lokality: použité role systému lokality, stav Internetu a protokolu SSL, operační systém, procesory, fyzický nebo virtuální počítač a využití vysoké dostupnosti serveru lokality

- Configuration Manager schéma databáze (hodnota hash všech definic objektů)

- Nakonfigurovaná úroveň telemetrie, režim online nebo offline a konfigurace rychlé aktualizace

- Počet jazyků a národních prostředí klienta

- Počet Configuration Manager verzí klienta, verzí operačního systému a verzí Office

- Počet operačních systémů pro spravovaná zařízení a zásady nastavené konektorem Exchange

- Počet zařízení s Windows 10 podle větve a sestavení

- ***[Přesunuté]*** Počet klientů s Windows 10, kteří používají web Windows Update pro firmy  

- Metriky výkonu databáze: informace o zpracování replikace, hlavní SQL Server uložené procedury podle procesoru a využití disku

- Typy distribučních bodů a bodů správy a informace o základní konfiguraci: chráněné, připravené, PXE, vícesměrové vysílání, stav protokolu SSL, distribuční body pro vyžádání obsahu, podpora MDM a povolený protokol SSL

- Seznam rozšíření s algoritmem hash na stránkách a průvodcům vlastností konzoly pro správu

- Informace o instalaci:
     - Sestavení, typ instalace, jazykové sady, funkce, které jste povolili   

     - Předběžná verze použití, nastavení typ média, typ větve

     - Datum vypršení platnosti Software Assurance      

     - Stav nasazení balíčku aktualizací a chyby, průběh stahování a chyby požadovaných součástí 

     - Použití aktualizačního kroužku aktualizací

     - Verze skriptu po upgradu

- Verze SQL, úroveň aktualizace Service Pack, edice, ID kolace a znaková sada     

- Statistika telemetrie: při spuštění, za běhu, chyby

- Jestli je zjišťování sítě povolené nebo zakázané

- ***[Přesunuté]*** Počet klientů připojených k Azure Active Directory

- ***[Nové]*** Počet fází nasazení vytvořených pomocí typu

- ***[Nové]*** Počet rozšířených klientů interoperability

- ***[Nové]*** Seznam vlastností inventáře hardwaru delší než 255 znaků s algoritmem hash



##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Úroveň 2 – Rozšířená
Rozšířená úroveň je výchozí po dokončení instalace. Tato úroveň zahrnuje data shromážděná v datech na úrovni Basic a na základě funkcí (četnost a doba použití), Configuration Manager nastavení klienta (název komponenty, stav a určitá nastavení jako intervaly dotazování) a základní informace o aktualizacích softwaru.

Tato úroveň se doporučuje, protože poskytuje Microsoftu minimální data, která je potřeba k tomu, aby v budoucích verzích produktů a služeb poskytovala užitečná vylepšení. Tato úroveň neshromažďuje názvy objektů (lokalit, uživatelů, počítačů ani objektů), podrobnosti o objektech souvisejících se zabezpečením nebo ohrožení zabezpečení, jako je počet systémů, které vyžadují aktualizace softwaru.

Pro Configuration Manager verze 1802 Tato úroveň zahrnuje následující data:

### <a name="application-management"></a>Správa aplikací  

- Požadavky na aplikace: počet předdefinovaných podmínek, na které odkazuje technologie nasazení

- Nahrazování aplikací, maximální hloubka řetězce

- Statistika schválení aplikace a frekvence využití

- Statistika velikosti obsahu aplikace

- Informace o nasazení aplikace: použití instalace a odinstalace, vyžaduje schválení, povolení/zákaz interakce s uživatelem, funkce chování při instalaci a počet použití  

- Velikost zásad aplikace a statistika složitosti

- Dostupné statistiky žádostí aplikace

- Základní informace o konfiguraci balíčků a programů: možnosti nasazení a příznaky programu

- Základní informace o využití/cílení pro typy nasazení: cílení na uživatele a zařízení, požadované versus dostupné a univerzální aplikace

- Počet prostředí App-V a vlastností nasazení

- Počet použitelností aplikace podle operačního systému  

- Počet aplikací, na které se odkazuje v pořadí úkolů

- Počet různých brandingů pro katalog aplikací

- Počet aplikací Office 365 vytvořených pomocí řídicího panelu

- Počet balíčků podle typu  

- Počet nasazení balíčku/programu  

- Počet licencí na aplikace systému Windows 10  

- Počet Instalační služba systému Windows typů nasazení podle nastavení Odinstalace obsahu

- Počet Microsoft Store pro obchodní aplikace a statistiky synchronizace: shrnuté typy aplikací, stav licencované aplikace a počet online a offline licencovaných aplikací  

- Typ a doba trvání časového období údržby  

- Minimální/maximální/průměrný počet nasazení aplikací na uživatele nebo zařízení za časové období

- Nejběžnější kódy chyb instalace aplikací podle technologie nasazení

- Možnosti a počty konfigurace MSI

- Statistika interakce koncových uživatelů s oznámením pro požadovaná nasazení softwaru   

- Použití univerzálního přístupu k datům, jak se vytvořilo

- ***[Nové]*** Agregované statistiky spřažení uživatelských zařízení 

- ***[Nové]*** Max a průměr primárních uživatelů na zařízení


### <a name="client"></a>Klient  

- Verze klienta technologie AMT (Active Management Technology)

- Stáří systému BIOS v rocích

- Počet zařízení s povoleným zabezpečeným spouštěním

- Počet zařízení podle stavu TPM

- Automatický upgrade klienta: konfigurace nasazení, včetně nasazení klienta a používání vyloučení (klient rozšířené kompatibility)

- Konfigurace velikosti mezipaměti klienta

- Chyby stahování nasazení klienta

- Souhrnné informace o stavu klienta a hlavních potížích

- Stav akce operace klientského oznamování: počet spuštěných časů, maximální počet cílových klientů a průměrná úspěšnost

- Počet instalací klientů z každého typu zdrojového umístění  

- Počet chyb instalace klientů  

- Počet zařízení virtualizovaných technologií Hyper-V nebo Azure  

- Počet akcí centra softwaru   

- Počet zařízení s podporou rozhraní UEFI

- Metody nasazení používané pro klienta a počet klientů podle metody nasazení

- Seznam/počet povolených klientských agentů  

- Stáří operačního systému v měsících

- Počet tříd inventáře hardwaru, pravidel inventáře softwaru a pravidel shromažďování souborů

- Statistika pro ověření stavu zařízení: Nejčastější kódy chyb, počet místních serverů a počty zařízení v různých stavech

- ***[Nové]*** Počet zařízení ve výchozím prohlížeči


### <a name="cloud-services"></a>Cloud Services  

- Statistika zjišťování Azure Active Directory

- Konfigurace a statistika využití Brána pro správu cloudu: počty oblastí a prostředí a statistiky ověřování/autorizace

- Počet Azure Active Directory aplikací a služeb, které jsou připojené k Configuration Manager

- Počet kolekcí synchronizovaných do Azure Log Analytics

- Počet konektorů Upgrade Analytics

- Zda je povolen konektor cloudu služby Azure Log Analytics


### <a name="co-management"></a>Spoluspráva  
- Agregované statistiky využití pro spolusprávu: počet registrovaných klientů, klienti, kteří přijímají zásady, stavy úloh, velikosti kolekcí pilotního/vyloučení a chyby registrace  

- Počet klientů metodou registrace spolusprávy  

- Statistiky chyb pro registraci spolusprávy  

- Plán registrace a historická Statistika  

- Počet klientů oprávněných pro spolusprávu  

- Přidružený tenant Microsoft Intune


### <a name="collections"></a>Kolekce  

- Využití ID kolekce (neběží mimo identifikátor)

- Statistika vyhodnocení kolekce: čas dotazu, přiřazeno versus nepřiřazené počty, počty podle typu, Změna ID a použití pravidla

- Kolekce bez nasazení


### <a name="compliance-settings"></a>Nastavení dodržování předpisů  

- Základní základní informace o konfiguraci: počet, počet nasazení a počet odkazů

- Statistiky chyb zásad dodržování předpisů

- Počet položek konfigurace podle typu  

- Počet nasazení, která odkazují na předdefinovaná nastavení, včetně nastavení oprav  

- Počet pravidel a nasazení vytvořených pro vlastní nastavení, včetně nastavení oprav  

- Počet nasazených šablon zásad dodržování předpisů pro Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certifikát (. pfx) a zásady dodržování předpisů

- Počet certifikátů SCEP, VPN, Wi-Fi, certifikátu (. pfx) a nasazení zásad dodržování předpisů podle platformy

- Zásady Windows Hello pro firmy (vytvořené, nasazené)


### <a name="content"></a>Obsah  

- ***[Aktualizováno]*** Statistika hraniční skupiny: kolik rychlého, počtu pomalých, počtu na skupinu a záložní relace

- Informace o hraniční skupině: počet hranic a systémů lokality, které jsou přiřazeny ke každé skupině hranic  

- Vztahy hraniční skupiny a záložní konfigurace

- Statistika stažení obsahu klienta

- Počet hranic podle typu  

- Počet klientů sdílené mezipaměti, statistiky využití a částečné statistické údaje ke stažení

- Informace o konfiguraci Správce distribuce: vlákna, zpoždění opakování, počet opakovaných pokusů a nastavení distribučního bodu pro vyžádání obsahu  

- Informace o konfiguraci distribučního bodu: použití sledování mezipaměti větví a distribučních bodů

- Informace o skupině distribučních bodů: počet balíčků a distribučních bodů, které jsou přiřazeny ke každé skupině distribučních bodů  


### <a name="endpoint-protection"></a>Funkce Endpoint Protection  

- Zásady služby Microsoft Defender Advanced Threat Protection (ATP) (dříve označované jako ochrana ATP v programu Windows Defender): počet zásad a to, jestli jsou nasazené zásady.

- Počet výstrah, které jsou nakonfigurované pro funkci Endpoint Protection  

- Počet kolekcí vybraných k zobrazení v Endpoint Protectionovém řídicím panelu  

- Počet zásad ochrany proti zneužití v programu Windows Defender, nasazení a cílových klientů

- Endpoint Protection chyby nasazení, počet kódů chyb nasazení Endpoint Protection zásad  

- Použití zásad Endpoint Protection antimalwaru a brány Windows Firewall (počet jedinečných zásad přiřazených ke skupině)<br /><br /> Tato data neobsahují žádné informace o nastaveních obsažených v zásadách.  


### <a name="migration"></a>Migrace  

- Počet migrovaných objektů (použití Průvodce migrací)


### <a name="mobile-device-management-mdm"></a>Správa mobilních zařízení (MDM)  

- Počet vydaných akcí mobilního zařízení: uzamknout, připnout PIN REST, vymazat, vyřadit a synchronizovat nyní

- Počet zásad mobilních zařízení  

- Počet mobilních zařízení spravovaných Configuration Manager a Microsoft Intune a způsob jejich registrace (Hromadná, založená na uživatelích)  

- Počet uživatelů, kteří mají více zaregistrovaných mobilních zařízení  

- Plán cyklického dotazování mobilních zařízení a statistika pro dobu trvání vrácení se změnami mobilního zařízení  


### <a name="microsoft-intune-troubleshooting"></a>Řešení potíží s Microsoft Intune  

- Počet a velikost akcí zařízení (vymazání, vyřazení, uzamčení), telemetrie a datové zprávy, které se replikují Microsoft Intune

- Počet a velikost stavu, stavu, inventáře, RDR, DDR, UDX, stavu klientů, POL, LOG, CERT, CRP, Resync, CFD, RDO, BEX, ISM a zpráv o dodržování předpisů, které se stahují z Microsoft Intune

- Statistika synchronizace úplných a rozdílných uživatelů pro Microsoft Intune


### <a name="on-premises-mobile-device-management-mdm"></a>Místní správa mobilních zařízení (MDM)  

- Počet balíčků a profilů hromadné registrace systému Windows 10  

- Statistika úspěchů nebo selhání nasazení aplikací s místní správou mobilních zařízení  


### <a name="os-deployment"></a>Nasazení operačního systému  

- Počet spouštěcích imagí, ovladačů, balíčků ovladačů, distribučních bodů s podporou vícesměrového vysílání, distribučních bodů s podporou technologie PXE a pořadí úloh  

- Počet spouštěcích imagí podle Configuration Manager verze klienta

- Počet spouštěcích imagí verze Windows PE

- Počet zásad upgradu edice

- Počet hardwarových identifikátorů vyloučených z technologie PXE

- Počet nasazení operačního systému podle verze operačního systému

- Počet upgradů operačního systému v průběhu času

- Počet nasazení pořadí úkolů pomocí možnosti pro předběžné stažení obsahu

- Počty použití kroku pořadí úkolů

- Nainstalovaná verze sady Windows ADK


### <a name="site-updates"></a>Aktualizace webu  

- Verze nainstalovaných oprav hotfix Configuration Manager


### <a name="software-updates"></a>Aktualizace softwaru  

- Dostupné a rozdílové konečné termíny používané v pravidlech automatického nasazení  

- Průměrný a maximální počet přiřazení na aktualizaci  

- Plány vyhodnocování aktualizací klientů a kontrol  

- Klasifikace synchronizované bodem aktualizace softwaru

- Statistiky použití dílčích oprav clusteru  

- Konfigurace aktualizací Windows 10 Express

- Konfigurace, které se používají pro aktivní plány údržby Windows 10  

- Počet nasazených aktualizací služeb Office 365  

- Počet synchronizovaných ovladačů Microsoft Surface

- Počet skupin aktualizací a přiřazení  

- Počet balíčků aktualizací a maximální/minimální/průměrný počet distribučních bodů, které jsou zaměřeny na balíčky  

- Počet aktualizací vytvořených a nasazených pomocí programu System Center Update Publisher  

- Počet vytvořených a nasazených zásad web Windows Update pro firmy

- ***[Nové]*** Agregovaná Statistika konfigurací web Windows Update pro firmy

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


### <a name="sqlperformance-data"></a>Data SQL a výkonu  

- Konfigurace a trvání Shrnutí lokality

- Počet největších databázových tabulek  

- Provozní statistiky zjišťování (počet nalezených objektů)

- Typy, povolené a naplánování zjišťování (úplné, přírůstkové)

- Informace o replice SQL AlwaysOn, využití a stav

- Problémy s výkonem sledování změn SQL, doba uchování a stav automatického vyčištění

- Doba uchování dat sledování změn SQL

- Statistika výkonu stavových a stavových zpráv, včetně nejběžnějších a nejdražších typů zpráv


### <a name="miscellaneous"></a>Různé  

- Konfigurace bodu služby datového skladu, včetně plánu synchronizace a průměrného času

- Počet skriptů a spuštění statistiky

- Počet webů s Wake On LAN (WOL)

- Využití sestav a statistiky výkonu

- ***[Nové]*** Statistika využití postupného nasazení



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Úroveň 3 – Úplná
Úplná úroveň zahrnuje všechna data na úrovni Basic a Enhanced. Obsahuje také další informace o řešení funkci Endpoint Protection, procenta dodržování předpisů pro aktualizace a informace o aktualizacích softwaru. Tato úroveň může zahrnovat taky rozšířené diagnostické informace, jako jsou systémové soubory a snímky paměti, které můžou zahrnovat osobní informace, které existovaly v paměti nebo souborech protokolu v době zachycení.

Pro Configuration Manager verze 1802 Tato úroveň zahrnuje následující data:

- Informace o plánu hodnocení pravidel automatického nasazení

- Shrnutí stavu ATP

- Hodnocení kolekcí a statistiky obnovení

- Statistiky zásad dodržování předpisů pro dodržování předpisů a chyby

- Nastavení dodržování předpisů: podrobnosti o konfiguraci SCEP, VPN, Wi-Fi a zásad dodržování předpisů

- Konfigurační balíček DCM pro použití Configuration Manager

- Podrobné chyby instalace nasazení klienta

- Shrnutí stavu Endpoint Protection: včetně počtu chráněných, neznámých a nepodporovaných klientů

- Konfigurace zásad funkce Endpoint Protection

- Seznam procesů nakonfigurovaných s chováním při instalaci pro aplikace

- Minimální/maximální/průměrný počet hodin od poslední kontroly aktualizací softwaru

- Minimální/maximální/průměrný počet neaktivních klientů v kolekcích nasazení aktualizací softwaru

- Minimální/maximální/průměrný počet aktualizací softwaru na balíček

- ***[Aktualizováno]*** Statistika nasazení kódu produktu MSI 

- Celkové dodržování předpisů pro nasazení aktualizací softwaru

- Počet skupin, u kterých vypršela platnost aktualizací softwaru

- Kódy a počty chyb nasazení aktualizací softwaru

- Informace o nasazení aktualizace softwaru: procento nasazení, která jsou zaměřena na klienta vs. čas UTC, povinná oproti netichému porovnání a potlačení restartování

- Produkty aktualizace softwaru synchronizované bodem aktualizace softwaru

- Procenta úspěšnosti kontroly aktualizací softwaru

- Top 50 procesorů v prostředí

- Typ zásad podmíněného přístupu Exchange Active Sync (EAS) pro zařízení, která Microsoft Intune spravují

- Podrobnosti o aplikaci Microsoft Store for Business: neagregovaný seznam synchronizovaných aplikací včetně AppID, online stavu nebo offline stavu a celkového počtu zakoupených licencí
