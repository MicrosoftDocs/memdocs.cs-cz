---
title: Diagnostická data a data o využití pro 1910
titleSuffix: Configuration Manager
description: Přečtěte si o konkrétních datech, která Configuration Manager shromažďuje na každé úrovni verze 1910.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3ce6b9a-7d54-4374-9b7a-f017f872bd6f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95fb434f94ece47a0e896e5cf1913f3f67cac7d0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720342"
---
# <a name="diagnostic-and-usage-data-for-version-1910"></a>Data o diagnostice a použití pro verzi 1910

*Platí pro: Configuration Manager (Current Branch)*

Následující části obsahují další podrobnosti o datech shromažďovaných na jednotlivých úrovních. Další informace o úrovních a jejich změně najdete v tématu [úrovně diagnostických dat o využití](levels-overview.md).

Změny z předchozích verzí jsou označeny ***[New]***, ***[Aktualizováno]***, ***[odebrané]*** nebo ***[přesunuté]***.

> [!IMPORTANT]
> Configuration Manager neshromažďuje kódy lokalit, názvy lokalit, IP adresy, uživatelská jména, názvy počítačů, fyzické adresy ani e-mailové adresy na úrovních Basic a Enhanced. Žádná kolekce těchto informací na úrovni Úplná není záměrné. Je potenciálně součástí pokročilých diagnostických informací, jako jsou soubory protokolu nebo snímky paměti. Společnost Microsoft tyto informace nepoužívá k tomu, aby vás identifikovala, kontaktovala vás nebo vyvinula reklamu.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Úroveň 1 – Základní

Pro Configuration Manager verze 1910 Tato úroveň zahrnuje následující data:

- Statistika o připojeních konzoly Configuration Manager: verze OS, jazyk, SKU a architektura, systémová paměť, počet logických procesorů, připojení ID webu, nainstalované verze rozhraní .NET, jazykové sady konzoly a úroveň ověřování

- Základní počty typů aplikací a nasazení: celkový počet aplikací, celkový počet aplikací s více typy nasazení, celkový počet aplikací se závislostmi, celkový počet nahrazených aplikací a počet používaných technologií nasazení

- Základní Configuration Manager data hierarchie lokality: seznam webů, typ, verze, stav, počet klientů a časové pásmo

- Základní konfigurace databáze: procesory, velikost paměti, nastavení paměti, Configuration Manager konfigurace databáze, Configuration Manager velikost databáze, konfigurace clusteru, konfigurace distribuovaných zobrazení a verze sledování změn  

- Základní statistické údaje zjišťování: počet zjišťování, minimální/maximální/průměrné velikosti skupin a pokud web běží zcela s Azure Active Directory službami

- Základní Endpoint Protection informace o verzích antimalwarového klienta

- Základní počty imagí nasazení operačního systému

- Základní informace o serveru systému lokality: použité role systému lokality, stav Internetu a protokolu SSL, operační systém, procesory, fyzický nebo virtuální počítač a využití vysoké dostupnosti serveru lokality

- Configuration Manager schéma databáze (hodnota hash všech definic objektů)

- Nakonfigurovaná úroveň pro diagnostiku a data o využití, režim online nebo offline a konfigurace rychlé aktualizace

- Počet jazyků a národních prostředí klienta

- Počet Configuration Manager verzí klienta, verzí operačního systému a verzí Office

- Počet operačních systémů pro spravovaná zařízení a zásady nastavené konektorem Exchange

- Počet zařízení s Windows 10 Podle větve, sestavení a jedinečné doménové struktury služby Active Directory  

- Počet klientů s Windows 10, kteří používají web Windows Update pro firmy  

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

- Diagnostika a statistiky údajů o využití: při spuštění, za běhu, chyby  

- Jestli je zjišťování sítě povolené nebo zakázané  

- Počet klientů připojených k Azure Active Directory  

- Počet fází nasazení vytvořených pomocí typu  

- Počet rozšířených klientů interoperability  

- Seznam vlastností inventáře hardwaru delší než 255 znaků s algoritmem hash  

- Počet klientů metodou registrace spolusprávy  

- Statistiky chyb pro registraci spolusprávy  

- Počet klientů podle stáří operačního systému Windows po dobu nejbližšího tříměsíčního intervalu  

- Prvních 10 názvů procesorů používaných na klientech a serverech  

- Počty a zpracování pro klíčové Configuration Manager objekty: záznamy zjišťování dat (DDR), stavové zprávy, stavové zprávy, inventář hardwaru, inventář softwaru a celkový počet souborů v doručených oknech  

- Informace o výkonu disku a procesoru serveru lokality  

- Informace o využití v době provozu a paměti pro Configuration Manager procesy serveru lokality  

- Počet havárií pro procesy serveru Configuration Manager lokality a ID podpisu v programu Watson, pokud je k dispozici  

- Seznam Top SQL dotazů s algoritmem hash podle využití paměti a počtu zámků  

- Agregované statistiky využití pro spolusprávu: počet klientů, kteří se někdy zaregistrovali, počet zaregistrovaných klientů, počet klientů, kteří čekají na registraci, klienti, kteří dostávají zásady, stavy zatížení, kolekce pilotního/vyloučení a chyby registrace  

- Existence rozšíření nástroje Microsoft BitLocker Administration and Monitoring (MBAM) na straně serveru  

- Počet kategorií a Nezařazeno do kategorie aplikací pro funkci Asset Intelligence

- Stav a stav služby správy

- Hash atributů klíčového webu (ID webu, ID zprostředkovatele SQL a klíč výměny lokality)

- ***[Nové]*** Počet instalací Microsoft Edge

## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Úroveň 2 – Rozšířená

Pro Configuration Manager verze 1910 Tato úroveň zahrnuje následující data:

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

- Agregované statistiky spřažení uživatelských zařízení  

- Max a průměr primárních uživatelů na zařízení  

- Použití globálních podmínek aplikace podle typu  

- Konfigurace vlastního nastavení centra softwaru  

- Připravenost a počty správce převodu balíčků  

- Počet metod detekce aplikace podle typu  

- Počet chyb vynucení aplikace  

- Instalační služba MSI – vlastnosti  

- Statistika požadavků na instalaci uživatelů  

- Agregované statistiky používání funkce pro schválení e-mailu  

- Počet souborů, velikost obsahu, počet služeb a počet vlastních akcí MSIs v katalogu aplikací  

- Počet zařízení podle stavu připravenosti pro Office ProPlus

- Agregované statistiky používání skupin aplikací

- Agregované statistiky o doplňcích pro Office, použití sady nástrojů Readiness Toolkit pro Office a počty klientů s Office 365 ProPlus

- ***[Nové]*** Agregované statistiky o stavu doplňku pro Office

- ***[Nové]*** Počet a velikost sad pilotních kolekcí pro Office pro plus

### <a name="client"></a>Klient  

- Verze klienta technologie AMT (Active Management Technology)  

- Stáří systému BIOS v rocích  

- Počet zařízení s povoleným zabezpečeným spouštěním  

- Počet zařízení podle stavu TPM  

- Automatický upgrade klienta: konfigurace nasazení, včetně nasazení klienta a používání vyloučení (klient rozšířené kompatibility)  

- Konfigurace velikosti mezipaměti klienta  

- Chyby stahování nasazení klienta  

- Statistika stavu klienta a shrnutí hlavních problémů podle verze klienta, součásti, operačního systému a úlohy  

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

- Počet zařízení ve výchozím prohlížeči  

- Počet vygenerovaných ověřovacích certifikátů serveru Configuration Manager  

- Počet zařízení Microsoft Surface podle modelu  

- Počet selhání kontroly stavu klienta podle typu problému

### <a name="cloud-services"></a>Cloud Services  

- Statistika zjišťování Azure Active Directory  

- Konfigurace a statistika využití Brána pro správu cloudu: počty oblastí a prostředí a statistiky ověřování/autorizace  

- Počet Azure Active Directory aplikací a služeb, které jsou připojené k Configuration Manager  

- Počet kolekcí synchronizovaných do Azure Log Analytics  

- Počet konektorů Upgrade Analytics  

- Zda je povolen konektor cloudu služby Azure Log Analytics  

- Počet distribučních bodů pro vyžádání obsahu s cloudovým distribučním bodem jako se zdrojovým umístěním  

### <a name="cmpivot"></a>CMPivot

- Statistiky využití CMPivot  

- Počet uložených dotazů CMPivot  

- Počet dotazů podle typu entity  

### <a name="co-management"></a>Spoluspráva  

- Plán registrace a historická Statistika  

- Počet klientů oprávněných pro spolusprávu  

- Přidružený tenant Microsoft Intune  

### <a name="collections"></a>Kolekce  

- Využití ID kolekce (neběží mimo identifikátor)  

- Statistika vyhodnocení kolekce: čas dotazu, přiřazeno versus nepřiřazené počty, počty podle typu, Změna ID a použití pravidla  

- Kolekce bez nasazení  

- Počet kolekcí synchronizovaných do Azure Active Directory

### <a name="compliance-settings"></a>Nastavení dodržování předpisů  

- Základní základní informace o konfiguraci: počet, počet nasazení a počet odkazů  

- Statistiky chyb zásad dodržování předpisů  

- Počet položek konfigurace podle typu  

- Počet nasazení, která odkazují na předdefinovaná nastavení, včetně nastavení oprav  

- Počet pravidel a nasazení vytvořených pro vlastní nastavení, včetně nastavení oprav  

- Počet nasazených šablon zásad dodržování předpisů pro Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certifikát (. pfx) a zásady dodržování předpisů  

- Počet certifikátů SCEP, VPN, Wi-Fi, certifikátu (. pfx) a nasazení zásad dodržování předpisů podle platformy  

- Zásady Windows Hello pro firmy (vytvořené, nasazené)  

- Počet nasazených zásad prohlížeče Microsoft Edge  

- Počet zásad OneDrive (vytvořených, nasazených)

### <a name="content"></a>Obsah  

- Statistika hraniční skupiny: kolik rychlého, počtu pomalých, počtu na skupinu a záložní relace  

- Informace o hraniční skupině: počet hranic a systémů lokality, které jsou přiřazeny ke každé skupině hranic  

- Vztahy hraniční skupiny a záložní konfigurace  

- Statistika stažení obsahu klienta  

- Počet hranic podle typu  

- Počet klientů sdílené mezipaměti, statistiky využití a částečné statistické údaje ke stažení  

- Informace o konfiguraci Správce distribuce: vlákna, zpoždění opakování, počet opakovaných pokusů a nastavení distribučního bodu pro vyžádání obsahu  

- Informace o konfiguraci distribučního bodu: použití sledování mezipaměti větví a distribučních bodů  

- Informace o skupině distribučních bodů: počet balíčků a distribučních bodů, které jsou přiřazeny ke každé skupině distribučních bodů  

- Typ knihovny obsahu, bez ohledu na místní nebo vzdálený  

- Počet skupin hranic podle konfigurace  

### <a name="endpoint-protection"></a>Funkce Endpoint Protection  

- Zásady služby Microsoft Defender Advanced Threat Protection (ATP) (dříve označované jako ochrana ATP v programu Windows Defender): počet zásad a to, jestli jsou nasazené zásady.

- Počet výstrah, které jsou nakonfigurované pro funkci Endpoint Protection  

- Počet kolekcí vybraných k zobrazení v Endpoint Protectionovém řídicím panelu  

- Počet zásad ochrany proti zneužití v programu Windows Defender, nasazení a cílových klientů  

- Endpoint Protection chyby nasazení, počet kódů chyb nasazení Endpoint Protection zásad  

- Endpoint Protection využití antimalwarových zásad a brány Windows Firewall (počet jedinečných zásad přiřazených ke skupině). Tato data neobsahují žádné informace o nastaveních obsažených v zásadách.  

### <a name="migration"></a>Migrace  

- Počet migrovaných objektů (použití Průvodce migrací)  

### <a name="mobile-device-management-mdm"></a>Správa mobilních zařízení (MDM)  

- Počet vydaných akcí mobilního zařízení: uzamknout, připnout PIN REST, vymazat, vyřadit a synchronizovat nyní  

- Počet zásad mobilních zařízení  

- Počet mobilních zařízení, která Configuration Manager spravuje, a způsob jejich registrace (hromadně, na základě uživatelů)  

- Počet uživatelů, kteří mají více zaregistrovaných mobilních zařízení  

- Plán cyklického dotazování mobilních zařízení a statistika pro dobu trvání vrácení se změnami mobilního zařízení  

### <a name="microsoft-intune-troubleshooting"></a>Řešení potíží s Microsoft Intune  

- Počet a velikost akcí zařízení (vymazání, vyřazení, uzamčení), data o využití a datové zprávy, které se replikují do Microsoft Intune  

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

- Počet úloh údržby imagí  

- Počet importovaných počítačů  

- Počet duplicitních identifikátorů hardwaru (MAC Address a SMBIOS GUID) vyloučených z prostředí PXE a registrace klienta

- Počet pořadí úkolů podle typu (nasazení operačního systému nebo obecné pořadí úkolů)

- Počet balíčků s nastavením obsahu před ukládáním do mezipaměti

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

- Agregovaná Statistika konfigurací web Windows Update pro firmy  

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

- Počet předplatných a používání katalogu aktualizací softwaru třetích stran  

- Počet aktualizací softwaru nasazených s obsahem a bez něj  

- Agregovaná statistika počtu UUP aktualizací, které jsou požadovány, nasazeny, prošly, nahrazeny a staženy  

- Používání kategorií produktů UUP  

- Počet klientů, kteří nasadili alespoň jednu aktualizaci kvality UUP nebo aktualizace funkcí UUP  

- Hlavní kódy chyb UUP a počet ovlivněných zařízení  

- Seznam předplatných pro katalogy aktualizací softwaru třetích stran

- Použití nastavení údržby služby WSUS

### <a name="sqlperformance-data"></a>Data SQL a výkonu  

- Konfigurace a trvání Shrnutí lokality  

- Počet největších databázových tabulek  

- Provozní statistiky zjišťování (počet nalezených objektů)  

- Typy, povolené a naplánování zjišťování (úplné, přírůstkové)  

- Informace o replice SQL AlwaysOn, využití a stav  

- Problémy s výkonem sledování změn SQL, doba uchování a stav autocleanup  

- Doba uchování dat sledování změn SQL  

- Statistika výkonu stavových a stavových zpráv, včetně nejběžnějších a nejdražších typů zpráv  

- Statistika provozu bodu správy (celkový počet odeslaných a přijatých koncovým bodem)  

- Měření čítače výkonu bodu správy  

- Agregovaná Statistika výkonu volání koncových bodů centra softwaru v bodu správy

### <a name="miscellaneous"></a>Různé  

- Konfigurace bodu služby datového skladu, včetně plánu synchronizace, průměrné doby a použití funkce přizpůsobené tabulky  

- Počet skriptů a spustit/upravit statistiku  

- Počet webů s Wake On LAN (WOL)  

- Využití sestav a statistiky výkonu  

- Statistika využití postupného nasazení  

- Počty a průběh položek v Management Insights  

- Počet havárií pro jedinečné procesy bez Configuration Manager na serveru lokality a ID podpisu v programu Watson, pokud je k dispozici  

- Agregované statistiky o chybách a využití při registraci Desktop Analytics

- Počet nedůležitých oznámení konzoly

- Agregované statistiky systémového času spuštění podle operačního systému, typu formuláře a jednotky

- Agregované statistiky používání Desktop Analytics

- Konfigurace a stav úlohy údržby SQL

- ***[Nové]*** Počet složek

- ***[Nové]*** Použití nástroje pro migraci Azure

## <a name="level-3---full"></a><a name="bkmk_level3"></a> Úroveň 3 – Úplná

Pro Configuration Manager verze 1910 Tato úroveň zahrnuje následující data:

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

- Statistika nasazení kódu produktu MSI  

- Celkové dodržování předpisů pro nasazení aktualizací softwaru  

- Počet skupin, u kterých vypršela platnost aktualizací softwaru  

- Kódy a počty chyb nasazení aktualizací softwaru  

- Informace o nasazení aktualizace softwaru: procento nasazení, která jsou zaměřena na klienta vs. čas UTC, povinná oproti netichému porovnání a potlačení restartování  

- Produkty aktualizace softwaru synchronizované bodem aktualizace softwaru  

- Procenta úspěšnosti kontroly aktualizací softwaru  

- Top 50 procesorů v prostředí  

- Typ zásad podmíněného přístupu Exchange Active Sync (EAS) pro zařízení, která Microsoft Intune spravují  

- Podrobnosti o aplikaci Microsoft Store for Business: neagregovaný seznam synchronizovaných aplikací včetně AppID, online stavu nebo offline stavu a celkového počtu zakoupených licencí  

- Počet klientů nabízených s možností, aby nepovolovala použití protokolu NTLM  

- Seznam rozšíření konzoly Configuration Manager
