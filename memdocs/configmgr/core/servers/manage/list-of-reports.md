---
title: Seznam sestav
titleSuffix: Configuration Manager
description: Projděte si seznam sestav dodaných s Configuration Manager. Sestavy se zobrazují v různých kategoriích.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713762"
---
# <a name="list-of-reports-in-configuration-manager"></a>Seznam sestav v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager poskytuje mnoho předdefinovaných sestav, které pokrývají mnoho úloh vytváření sestav, které můžete chtít provést. V těchto sestavách se také můžou používat příkazy SQL, díky kterým si můžete psát vlastní sestavy.   

Configuration Manager jsou zahrnuty následující sestavy. Sestavy se zobrazují v různých kategoriích.  



## <a name="administrative-security"></a>Zabezpečení správy  

V kategorii **zabezpečení pro správu** jsou uvedeny následující šest sestav.  

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Protokol aktivit správy**|Zobrazuje záznam změn správy provedených pro administrativní uživatele, role zabezpečení, obory zabezpečení a kolekce.|  
|**Přiřazení zabezpečení pro správce**|Zobrazí administrativní uživatele, jejich přidružené role zabezpečení a obory zabezpečení přidružené k jednotlivým rolím zabezpečení pro jednotlivé uživatele.|  
|**Objekty zabezpečené jediným oborem zabezpečení**|Zobrazí objekty, které správce přiřadil pouze k určenému oboru zabezpečení. Tato sestava nezobrazuje objekty, které správce přidruží k více než jednomu oboru zabezpečení.|  
|**Zabezpečení určitého objektu nebo několika objektů nástroje Configuration Manager**|Zobrazí zabezpečitelné objekty, obory zabezpečení přidružené k těmto objektům a administrativní uživatele, kteří mají práva k těmto objektům.|  
|**Shrnutí rolí zabezpečení**|Zobrazí role zabezpečení a správce Configuration Manager přidružených k jednotlivým rolím.|  
|**Shrnutí oborů zabezpečení**|Zobrazuje rozsahy zabezpečení a Configuration Manager administrativních uživatelů a skupin zabezpečení přidružených k jednotlivým oborům.|  



## <a name="alerts"></a>Výstrahy  

Do kategorie **výstrahy** se zobrazují následující dvě sestavy.  

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Přehled výkonnostních metrik výstrah**|Zobrazí souhrn všech odložených výstrah vygenerovaných mezi počátečním a koncovým datem.|  
|**Nejčastěji generované výstrahy**|Zobrazí souhrn nejčastěji generovaných výstrah v určité oblasti funkcí od zadaného data do dnešního dne.|  



## <a name="asset-intelligence"></a>Funkce Asset Intelligence  

Do kategorie **funkce Asset Intelligence** jsou uvedeny následující sestavy 67.  

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Hardware 01A – shrnutí počítačů v určité kolekci**|Zobrazí souhrnný přehled počítačů v zadané kolekci pomocí funkce Asset Intelligence.|  
|**Hardware 03A – primární uživatelé počítačů**|Zobrazí uživatele a počet počítačů, ve kterých se nachází primární uživatel.|  
|**Hardware 03B – počítače pro určitého primárního uživatele konzoly**|Zobrazí všechny počítače, ve kterých je zadaný uživatel primárním uživatelem.|  
|**Hardware 04A – počítače s více uživateli (sdílené)**|Zobrazí počítače, které nemají primárního uživatele, protože žádný z uživatelů nemá přihlášený čas větší než 66%.|  
|**Hardware 05A – uživatelé konzoly v zadaném počítači**|Zobrazí všechny uživatele konzoly v zadaném počítači.|  
|**Hardware 06A – počítače s nezjištěnými uživateli konzoly**|Pomáhá správcům určit počítače, u kterých je potřeba zapnout protokolování zabezpečení.|  
|**Hardware 07A – zařízení USB podle výrobce**|Zobrazí zařízení USB seskupená podle výrobce.|  
|**Hardware 07B – zařízení USB podle výrobce a popisu**|Zobrazí zařízení USB seskupená podle výrobce a popisu.|  
|**Hardware 07C – počítače s určitým zařízením USB**|Zobrazí všechny počítače se zadaným zařízením USB.|  
|**Hardware 07D – zařízení USB v určitém počítači**|Zobrazí všechna zařízení USB v zadaném počítači.|  
|**Hardware 08A – hardware nepřipravený na upgrade softwaru**|Zobrazí hardware, který nesplňuje minimální požadavky na hardware.|  
|**Hardware 09A – vyhledání počítačů**|Zobrazí shrnutí počítačů, které odpovídají filtrům klíčových slov. Tyto filtry jsou název počítače, Configuration Manager lokalita, doména, hlavní uživatel konzoly, operační systém, výrobce nebo model.|  
|**Hardware 10A – počítače v zadané kolekci se změnou proběhlou v zadaném období**|Zobrazí seznam počítačů v zadané kolekci, u kterých se v zadaném období změnila třída hardwaru.|  
|**Hardware 10B – změny v zadaném počítači v zadaném období**|Zobrazí třídy, které se v zadaném počítači změnily v zadaném období.|  
|**Licence 01A – hlavní kniha multilicencí společnosti Microsoft pro výpisy licencí společnosti Microsoft**|Zobrazí inventář všech softwarových produktů společnosti Microsoft, které jsou dostupné v rámci programu Microsoft Volume Licensing.|  
|**Licence 01B – položka hlavní knihy licence společnosti Microsoft podle odbytového kanálu**|Určí a zobrazí prodejní kanál inventarizovaného softwaru s multilicencí společnosti Microsoft.|  
|**Licence 01C – počítače s určitou položkou hlavní knihy multilicencí společnosti Microsoft a prodejní kanál**|Určí a zobrazí počítače, které mají zadanou položku z hlavní knihy multilicencí společnosti Microsoft.|  
|**Licence 01D – produkty z hlavní knihy multilicencí společnosti Microsoft v určitém počítači**|Určí a zobrazí všechny položky z hlavní knihy multilicencí společnosti Microsoft v zadaném počítači.|  
|**Licence 02A – počet licencí s blížícím se koncem platnosti podle časových rozsahů**|Zobrazí počet licencí s blížícím se koncem platnosti v daném období. Zobrazené produkty mají své licence spravované službou licencování softwaru.|  
|**Licence 02B – počítače s licencemi s blížícím se koncem platnosti**|Zobrazí zadané počítače s licencemi s blížícím se koncem platnosti.|  
|**Licence 02C – informace o licencích v určitém počítači**|Zobrazí produkty v zadaném počítači, jejichž licence spravuje služba SLS (Software Licensing Service).|  
|**Licence 03A – počet licencí podle stavu licence**|Zobrazí produkty podle stavu licence, jejichž licence spravuje služba SLS (Software Licensing Service).|  
|**Licence 03B -–počítače s určitým stavem licence**|Zobrazí produkty se zadaným stavem licence, jejichž licence spravuje služba SLS (Software Licensing Service).|  
|**Licence 04A – počet produktů spravovaných službou SLS (Software Licensing Service)**|Zobrazí počet produktů, jejichž licence spravuje služba SLS (Software Licensing Service).|  
|**Licence 04B – počítače s určitým produktem spravovaným službou SLS (Software Licensing Service)**|Zobrazí počítače spravované službou licencování softwaru, která zahrnuje zadaný produkt.|  
|**Licence 05A – počítače poskytující Službu správy klíčů**|Zobrazí počítače, které pracují jako servery správy klíčů.|  
|**Licence 06A – počty procesorů pro produkty s licencemi vázanými na procesor**|Zobrazí počet procesorů v počítačích, které používají produkty s podporou licencí vázaných na procesor.|  
|**Licence 06B – počítače s určitým produktem podporujícím licence vázané na procesor**|Zobrazí seznam počítačů, ve kterých je nainstalovaný zadaný produkt společnosti Microsoft podporující licence vázané na procesor.|  
|**Licence 14A – sestava odsouhlasení multilicencí společnosti Microsoft**|Zobrazuje odsouhlasení softwarových licencí získaných prostřednictvím multilicenční smlouvy s Microsoftem a skutečný počet v inventáři.|  
|**Licence 14B – seznam produktů společnosti Microsoft v inventáři nenalezených ve službě MVLS**|Tato sestava zobrazí používané softwarové produkty společnosti Microsoft, které se nenacházejí v multilicenční smlouvě společnosti Microsoft.|  
|**Licence 15A – sestava odsouhlasení obecných licencí**|Zobrazuje odsouhlasení obecně získaných softwarových licencí a skutečný počet inventarizace.|  
|**Licence 15B – sestava odsouhlasení obecných licencí podle počítačů**|Zobrazí počítače, ve kterých je nainstalovaný licencovaný produkt zadané verze.|  
|**Software 01A – shrnutí nainstalovaného softwaru v určité kolekci**|Zobrazí shrnutí nainstalovaného softwaru seřazeného podle počtu instancí v inventáři.|  
|**Software 02A – produktové řady pro určitou kolekci**|Zobrazí produktové řady a počet softwarových produktů v řadě pro zadanou kolekci.|  
|**Software 02B – produktové kategorie pro určitou produktovou řadu**|Zobrazí produktové kategorie v zadané produktové řadě a počet softwarových produktů v kategorii.|  
|**Software 02C – software v určité produktové řadě a kategorii**|Zobrazí veškerý software v zadané produktové řadě a kategorii.|  
|**Software 02D – počítače s určitým nainstalovaným softwarem**|Zobrazí všechny počítače s nainstalovaným zadaným softwarem.|  
|**Software 02E – software nainstalovaný v určitém počítači**|Zobrazí veškerý software nainstalovaný v zadaném počítači.|  
|**Software 03A – software nezařazený do kategorií**|Zobrazí software, který je zařazený do kategorie Neznámý nebo není zařazený do žádné kategorie.|  
|**Software 04A – software nakonfigurovaný pro automatické spouštění v počítačích**|Zobrazí seznam softwarových produktů nakonfigurovaných pro automatické spouštění v počítačích.|  
|**Software 04B – počítače s určitým softwarem nakonfigurovaným pro automatické spouštění**|Zobrazí všechny počítače se zadaným softwarem nakonfigurovaným pro automatické spouštění.|  
|**Software 04C – software nakonfigurovaný pro automatické spouštění v určitém počítači**|Zobrazí nainstalovaný software nakonfigurovaný pro automatické spouštění v určitém počítači.|  
|**Software 05A – objekty pomocníka prohlížeče**|Zobrazí objekty pomocníka prohlížeče nainstalované v počítačích v zadané kolekci.|  
|**Software 05B – počítače s určitým objektem pomocníka prohlížeče**|Zobrazí všechny počítače se zadaným objektem pomocníka prohlížeče.|  
|**Software 05C – objekty pomocníka prohlížeče v určitém počítači**|Zobrazí všechny objekty pomocníka prohlížeče v zadaném počítači.|  
|**Software 06A – vyhledání nainstalovaného softwaru**|Tato sestava poskytuje shrnutí nainstalovaného softwaru. Vyhledává v závislosti na následujících kritériích: název produktu, Vydavatel nebo verze.|  
|**Software 06B – software podle názvu produktu**|Zobrazí shrnutí nainstalovaného softwaru na základě zadaného názvu produktu.|  
|**Software 07A – nedávno použité spustitelné programy podle počtu počítačů**|Zobrazí spustitelné programy, které uživatelé naposledy použili. Zahrnuje také počet počítačů, ve kterých uživatelé program používali. K zobrazení této sestavy je potřeba povolit pro tuto lokalitu monitorování míry využití softwaru.|  
|**Software 07B – počítače s nedávným použitím zadaného spustitelného programu**|Zobrazí počítače, ve kterých uživatelé naposledy použili zadaný spustitelný program. Tato sestava vyžaduje, abyste povolili klientské nastavení monitorování míry využívání softwaru.|  
|**Software 07C – spustitelné programy nedávno použité v zadaném počítači**|Zobrazí spustitelné soubory, které uživatelé nedávno použili v zadaném počítači. Tato sestava vyžaduje, abyste povolili klientské nastavení monitorování míry využívání softwaru.|  
|**Software 08A – nedávno použité spustitelné programy podle počtu uživatelů**|Zobrazí spustitelné programy, které uživatelé naposledy použili. Zahrnuje také počet uživatelů, kteří program naposledy používali. Tato sestava vyžaduje, abyste povolili klientské nastavení monitorování míry využívání softwaru.|  
|**Software 08B – uživatelé s nedávným použitím zadaného spustitelného programu**|Zobrazí uživatele, kteří naposledy použili zadaný spustitelný program. Tato sestava vyžaduje, abyste povolili klientské nastavení monitorování míry využívání softwaru.|  
|**Software 08C – spustitelné programy nedávno použité zadaným uživatelem**|Zobrazí spustitelné programy, které použil zadaný uživatel v poslední době. Tato sestava vyžaduje, abyste povolili klientské nastavení monitorování míry využívání softwaru.|  
|**Software 09A – zřídka používaný software**|Zobrazí softwarové tituly, které uživatelé nepoužívali během zadaného časového období.|  
|**Software 09B – počítače s nainstalovaným zřídka používaným softwarem**|Zobrazí počítače s nainstalovaným softwarem, který uživatelé nepoužívali v zadaném časovém období. Zadané období vychází z hodnoty zadané v sestavě Software 09A – zřídka používaný software.|  
|**Software 10A – softwarové produkty s několika definovanými vlastními popisky**|Zobrazí softwarové produkty na základě porovnání všech zadaných kritérií pro vlastní popisky. Pokud chcete hledání softwarových produktů zpřesnit, můžete vybrat až tři vlastní popisky.|  
|**Software 10B – počítače s určitým nainstalovaným softwarovým produktem s vlastním popiskem**|Zobrazí všechny počítače v této kolekci, ve kterých je nainstalovaný zadaný softwarový produkt s vlastním popiskem.|  
|**Software 11A – softwarové produkty s určitým definovaným vlastním popiskem**|Zobrazí softwarové produkty na základě porovnání nejméně jednoho zadaného kritéria pro vlastní popisky.|  
|**Software 12A – softwarové produkty bez vlastního popisku**|Zobrazí všechny softwarové tituly, které nemají definovaný vlastní popisek.|  
|**Software 14A – hledat software s povolenou identifikační softwarovou značkou**|Zobrazí počet nainstalovaných softwarových produktů s povolenou identifikační softwarovou značkou.|  
|**Software 14B – počítače s nainstalovaným určitým softwarem s povolenou identifikační softwarovou značkou**|Zobrazí všechny počítače, ve kterých je nainstalovaný software s povolenou zadanou identifikační softwarovou značkou.|  
|**Software 14C – software s povolenou identifikační softwarovou značkou nainstalovaný na určitém počítači**|Zobrazí veškerý software se zadanou identifikační softwarovou značkou povolenou v určitém počítači.|  
|**Životní cyklus 01A – počítače s konkrétním softwarovým produktem**|Zobrazí seznam počítačů, ve kterých byl zjištěn zadaný produkt.|
|**Životní cyklus 02A – seznam počítačů s produkty s vypršenou platností v organizaci**|Zobrazí počítače, ve kterých vypršela platnost produktů. Tuto sestavu můžete filtrovat podle názvu produktu.|
|**Životní cyklus 03A – seznam produktů s vypršenou platností nalezených v organizaci**|Zobrazit podrobnosti o produktech ve vašem prostředí, jejichž data životního cyklu vypršela.|
|**Životní cyklus 04A – obecný přehled životního cyklu produktu**|Zobrazte si seznam životního cyklu produktu. Vyfiltruje seznam podle názvu produktu a dnů pro vypršení platnosti.|
|**Životní cyklus 05A – řídicí panel životní cyklus produktu**|Počínaje verzí 1810 Tato sestava obsahuje podobné informace jako na řídicím panelu v konzole.|



## <a name="client-push"></a>Klientská nabízená instalace  

V kategorii **nabízených oznámení klientů** jsou uvedeny následující čtyři sestavy.  

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Podrobnosti o stavu nabízené instalace klientů**|Zobrazí informace o procesu nabízené instalace klientů pro všechny lokality.|  
|**Podrobnosti o stavu nabízené instalace klientů pro zadanou lokalitu**|Zobrazí informace o procesu nabízené instalace klientů pro zadanou lokalitu.|  
|**Souhrn stavu nabízené instalace klientů**|Zobrazí souhrnný přehled stavu nabízené instalace klientů pro všechny lokality.|  
|**Souhrn stavu nabízené instalace klientů pro zadanou lokalitu**|Zobrazí souhrnný přehled stavu nabízené instalace klientů pro zadanou lokalitu.|  



## <a name="client-status"></a>Stav klienta  

Do kategorie **stav klienta** se zobrazí následující sedm sestav.  

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Podrobnosti o nápravě klienta**|Zobrazí podrobnosti akcí týkajících se nápravy klienta pro zadanou kolekci.|  
|**Shrnutí nápravy klienta**|Zobrazí shrnutí akcí týkajících se nápravy klienta pro zadanou kolekci.|  
|**Historie stavů klienta**|Zobrazí historický přehled celkového stavu klienta v lokalitě.|  
|**Shrnutí stavů klienta**|Zobrazí výsledky kontrol aktivních klientů v zadané kolekci.|  
|**Čas klienta k žádosti o zásadu**|V posledních 30 dnech zobrazuje procento klientů, kteří požadovali zásadu alespoň jednou. Každý den představuje procento z celkového počtu klientů, kteří požadovali zásady od prvního dne v cyklu.|  
|**Podrobnosti o klientech s neúspěšnými kontrolami klientů**|Zobrazí podrobnosti o klientech v zadané kolekci, u kterých se nezdařila kontrola klientů.|  
|**Podrobnosti o neaktivních klientech**|Zobrazí podrobný seznam neaktivních klientů v zadané kolekci.|  



## <a name="company-resource-access"></a>Přístup k prostředkům společnosti  

Do kategorie **přístup k prostředkům společnosti** jsou uvedené následující tři sestavy. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Historie vystavování certifikátů**|Zobrazí historii certifikátů vydaných bodem registrace certifikátu pro uživatele a zařízení pro zadaný rozsah dat.|  
|**Seznam prostředků podle stavu vystavení certifikátu**|Zobrazí zařízení nebo uživatele v zadaném stavu vystavení certifikátu po vyhodnocení zadaného profilu certifikátu.|  
|**Seznam prostředků s certifikáty s blížícím se datem konce platnosti**|Zobrazí seznam prostředků s certifikáty, jejichž platnost vyprší k zadanému datu nebo před ním.|  



## <a name="compliance-and-settings-management"></a>Správa nastavení a dodržování předpisů  

V kategorii **Správa dodržování předpisů a nastavení** jsou uvedené následující 22 sestav. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Historie dodržování předpisů u směrného plánu konfigurace**|Zobrazí historii změn v dodržování předpisů pro směrný plán konfigurace v zadaném období.|  
|**Historie dodržování přepisů u položky konfigurace**|Zobrazí historii změn v dodržování předpisů pro určitou položku konfigurace v zadaném období.|  
|**Podrobnosti o odpovídajících pravidlech položek konfigurace ve směrném plánu konfigurace pro určitý prostředek**|Zobrazí informace o pravidlech vyhodnocených jako vyhovující pro zadanou položku konfigurace pro zadané zařízení nebo uživatele.|  
|**Podrobnosti o konfliktních pravidlech položek konfigurace v směrném plánu konfigurace pro určitý prostředek**|Zobrazí informace o pravidlech v nasazené položce konfigurace, která je v konfliktu s jinými pravidly. Zahrňte další pravidla do stejné nebo jiné nasazené položky konfigurace.|  
|**Podrobnosti o chybách položek konfigurace v směrném plánu konfigurace pro určitý prostředek**|Zobrazí informace o chybách, které zadaná položka konfigurace vygeneruje pro zadané zařízení nebo uživatele.|  
|**Podrobnosti o neodpovídajících pravidlech položek konfigurace ve směrném plánu konfigurace pro určitý prostředek**|Zobrazí informace o pravidlech pro určitou položku konfigurace vyhodnocených jako nevyhovující pro zadané zařízení nebo uživatele.|  
|**Podrobnosti o napravených pravidlech položek konfigurace v směrném plánu konfigurace pro určitý prostředek**|Zobrazí informace o pravidlech napravených zadanou položkou konfigurace pro zadané zařízení nebo uživatele.|  
|**Seznam prostředků podle stavu dodržování předpisů pro směrný plán konfigurace**|Zobrazí zařízení nebo uživatele v zadaném stavu dodržování předpisů po vyhodnocení zadaného směrného plánu konfigurace.|  
|**Seznam prostředků podle stavu dodržování předpisů pro položku konfigurace v směrném plánu konfigurace**|Zobrazí zařízení nebo uživatele v zadaném stavu dodržování předpisů po vyhodnocení zadané položky konfigurace.|  
|**Seznam nekompatibilních aplikací a zařízení pro zadaného uživatele**|Zobrazí informace o uživatelích a zařízeních s nainstalovanými aplikacemi, které nedodržují zadanou zásadu.|  
|**Seznam pravidel v konfliktu se zadaným pravidlem pro určitý prostředek**|Zobrazí seznam pravidel, která jsou v konfliktu se zadaným pravidlem pro nasazenou položku konfigurace.|  
|**Seznam neznámých prostředků pro směrný plán konfigurace**|Zobrazí seznam zařízení nebo uživatelů, kteří dosud neohlásili žádná data o dodržování předpisů pro zadaný směrný plán konfigurace.|  
|**Seznam neznámých prostředků pro položku konfigurace**|Zobrazí seznam zařízení nebo uživatelů, kteří dosud neohlásili žádná data o dodržování předpisů pro zadanou položku konfigurace.|  
|**Shrnutí pravidel a chyb u položek konfigurace v směrném plánu konfigurace pro určitý prostředek**|Zobrazí souhrn stavu dodržování pravidel a všechny chyby nastavení pro zadanou položku konfigurace. Položka konfigurace musí být nasazena do zařízení nebo uživatele.|  
|**Souhrnné dodržování předpisů podle směrných plánů konfigurace**|Zobrazí souhrn celkového dodržování předpisů ve směrných plánech konfigurace nasazených v hierarchii.|  
|**Shrnutí dodržování předpisů podle položek konfigurace pro směrný plán konfigurace**|Zobrazí souhrnné informace o dodržování předpisů u položek konfigurace v zadaném směrném plánu konfigurace.|  
|**Souhrnné dodržování zásad konfigurace**|Zobrazí souhrn dodržování zásad konfigurace.|  
|**Souhrnné dodržování předpisů u směrného plánu konfigurace pro určitou kolekci**|Zobrazí souhrn celkového dodržování předpisů u zadaného směrného plánu konfigurace. Položka konfigurace musí být nasazena do zadané kolekce.|  
|**Souhrn uživatelů, kteří mají nekompatibilní aplikace**|Zobrazí informace o uživatelích s nainstalovanými aplikacemi, které nedodržují zadanou zásadu.|  
|**Přijetí Podmínek a ujednání**|Zobrazí položky Podmínek a ujednání a verze, které jednotliví uživatelé přijali.|  



## <a name="data-warehouse"></a>Datový sklad  

Do kategorie **datového skladu** se zobrazí následující sedm sestav. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Nasazení aplikace**|Historická: Podívejte se na podrobnosti nasazení aplikace pro konkrétní aplikaci a počítač.|
|**Endpoint Protection a Update Compliance softwaru**|Historická: zobrazení počítačů, ve kterých chybí aktualizace softwaru.|
|**Obecný inventář hardwaru**|Historická: zobrazení veškerého inventáře hardwaru pro určitý počítač.|
|**Obecný inventář softwaru**|Historická: zobrazení veškerého inventáře softwaru pro určitý počítač.|
|**Přehled stavu infrastruktury**|Historická: zobrazuje přehled stavu infrastruktury Configuration Manager.|
|**Seznam zjištěného malwaru**|Historická: zobrazení malwaru zjištěného v organizaci.|
|**Souhrn distribuce softwaru**|Historická: Shrnutí distribuce softwaru pro konkrétní reklamu a počítač.|


## <a name="device-management"></a>Správa zařízení  

Do kategorie **Správa zařízení** se zobrazí následující sestavy 37. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechna mobilní zařízení ve vlastnictví firmy**|Zobrazí všechna mobilní zařízení vlastněná podnikem.|
|**Všichni klienti mobilních zařízení**|Zobrazí informace o všech klientech mobilních zařízení. Zařízení spravovaná konektorem systému Exchange Server nejsou zahrnuta.|  
|**Problémy s certifikátem u mobilních zařízení, která jsou spravovaná klientem Configuration Manager pro systém Windows CE a která nejsou v pořádku**|Zobrazí podrobné informace o problémech s certifikátem na mobilních zařízeních, která jsou spravovaná klientem Configuration Manager pro systém Windows CE.|  
|**Selhání nasazení klienta u mobilních zařízení spravovaných klientem Configuration Manager pro systém Windows CE**|Zobrazí podrobné informace o selhání nasazení u mobilních zařízení, která jsou spravovaná klientem Configuration Manager pro systém Windows CE.|  
|**Podrobnosti o stavu nasazení klienta pro mobilní zařízení, která jsou spravována klientem Configuration Manager pro systém Windows CE**|Zobrazí informace o stavu mobilních zařízení, která jsou spravována klientem Configuration Manager pro systém Windows CE.|  
|**Úspěšné nasazení klienta u mobilních zařízení spravovaných klientem Configuration Manageru pro systém Windows CE**|Zobrazí podrobné informace o úspěšném nasazení u mobilních zařízení, která jsou spravovaná klientem Configuration Manager pro systém Windows CE.|  
|**Problémy s komunikací u mobilních zařízení spravovaných klientem nástroje Configuration Manager pro systém Windows CE (zařízení nejsou v pořádku)**|Tato sestava obsahuje podrobné informace o problémech s komunikací u mobilních zařízení, která jsou spravována klientem Configuration Manager pro systém Windows CE.|  
|**Stav dodržování předpisů u výchozích zásad poštovní schránky protokolu ActiveSync pro mobilní zařízení spravovaná konektorem systému Exchange Server**|Zobrazí souhrn stavu dodržování výchozí zásady poštovní schránky Exchange ActiveSync pro mobilní zařízení spravovaná konektorem systému Exchange Server.|  
|**Počet mobilních zařízení podle konfigurací displeje**|Tato sestava zobrazí počet mobilních zařízení podle nastavení displeje.|  
|**Počet mobilních zařízení podle operačního systému**|Zobrazí počet mobilních zařízení podle operačního systému.|  
|**Počet mobilních zařízení podle paměti pro programy**|Zobrazí počet mobilních zařízení podle paměti pro programy.|  
|**Počet mobilních zařízení podle konfigurací paměti úložiště**|Počet mobilních zařízení podle konfigurací paměti úložiště|  
|**Informace o stavu mobilních zařízení spravovaných klientem nástroje Configuration Manager pro systém Windows CE**|Zobrazí podrobné informace o stavu mobilních zařízení, která jsou spravovaná klientem Configuration Manager pro systém Windows CE.|  
|**Shrnutí stavu mobilních zařízení spravovaných klientem nástroje Configuration Manager pro Windows CE**|Zobrazí souhrnné informace o stavu mobilních zařízení, která jsou spravovaná klientem Configuration Manager pro systém Windows CE.|  
|**Neaktivní mobilní zařízení spravovaná konektorem systému Exchange Server**|Zobrazí mobilní zařízení spravovaná konektorem systému Exchange Server, která se nepřipojila k serveru Exchange během zadaného počtu dnů.|  
|**Seznam zařízení podle stavu ověření stavu**|Zobrazí seznam zařízení s atributy hlášenými službou ověření stavu.|
|**Seznam zařízení zapsaných pro jednotlivé uživatele ve službě Microsoft Intune**|Zobrazí všechna zařízení, která uživatel zaregistroval v Microsoft Intune.|  
|**Seznam zařízení v konkrétní kategorii zařízení**|Zobrazí informace pro všechna zařízení v konkrétní kategorii zařízení.|
|**Problémy s místním klientem u mobilních zařízení spravovaných klientem nástroje Configuration Manager pro systém Windows CE (zařízení nejsou v pořádku)**|Tato sestava obsahuje podrobné informace o problémech s místním klientem u mobilních zařízení, která jsou spravována klientem Configuration Manager pro systém Windows CE.|  
|**Informace o klientovi mobilního zařízení**|Zobrazí informace o mobilních zařízeních, ve kterých je nainstalován klient Configuration Manager. Pomocí této sestavy můžete ověřit, která mobilní zařízení můžou úspěšně komunikovat s bodem správy.|  
|**Podrobnosti o dodržování předpisů mobilním zařízením pro konektor systému Exchange Server**|Zobrazí podrobnosti o dodržování předpisů mobilním zařízením, které se týkají výchozí zásady poštovní schránky Exchange ActiveSync nakonfigurované pomocí konektoru systému Exchange Server.|  
|**Mobilní zařízení podle operačního systému**|Zobrazí mobilní zařízení podle operačního systému.|  
|**Mobilní zařízení s jailbreakem nebo rootem**|Zobrazí mobilní zařízení s jailbreakem nebo rootem.|  
|**Mobilní zařízení nespravovaná v důsledku neúspěšného přiřazení lokality po provedeném zápisu**|Zobrazí mobilní zařízení, která dokončila registraci v Configuration Manager, obsahují certifikát, ale nepodařilo se jim dokončit přiřazení lokality.|  
|**Mobilní zařízení s určitou velikostí volné paměti pro programy**|Zobrazí všechna mobilní zařízení s určitou velikostí volné paměti pro programy.|  
|**Mobilní zařízení s určitou velikostí volné paměti vyměnitelného úložiště**|Zobrazí všechna mobilní zařízení s určitou velikostí volné paměti vyměnitelného úložiště.|  
|**Mobilní zařízení s problémy obnovy certifikátu**|Zobrazí zapsaná mobilní zařízení, kterým se nepodařilo obnovit své certifikáty. Pokud certifikát neobnovíte před uplynutím doby platnosti, mobilní zařízení se stanou nespravovanými.|  
|**Mobilní zařízení s nedostatkem volné paměti pro programy (s menší než zadanou hodnotou volné paměti v kB)**|Zobrazí mobilní zařízení, u kterých je množství paměti pro programy nižší než zadaná velikost v kB.|  
|**Mobilní zařízení s nedostatkem volné paměti vyměnitelného úložiště (s menší než zadanou hodnotou volné paměti v kB)**|Zobrazí mobilní zařízení, u kterých je množství paměti vyměnitelného úložiště nižší než zadaná velikost v kB.|  
|**Počet zařízení zapsaných pro jednotlivé uživatele v Microsoft Intune**|Zobrazí uživatele s povoleným předplatným Microsoft Intune. Zobrazuje také celkový počet zaregistrovaných zařízení pro každého uživatele.|  
|**Nevyřízená žádost o vyřazení a vymazání mobilních zařízení**|Zobrazí žádosti o vymazání, které čekají na vyřízení pro mobilní zařízení.|  
|**Nedávno zapsaná a přiřazená mobilní zařízení**|Zobrazí mobilní zařízení, která se nedávno zaregistrovala pomocí Configuration Manager a úspěšně se přiřadila k lokalitě.|  
|**Nedávno vymazaná mobilní zařízení**|Zobrazí seznam mobilních zařízení, u kterých nedávno úspěšně proběhlo vymazání.|  
|**Souhrn nastavení pro mobilní zařízení spravovaná konektorem systému Exchange Server**|Zobrazí počet mobilních zařízení, která pro každou výchozí zásadu poštovní schránky protokolu Exchange ActiveSync používá nastavení spravovaná konektorem systému Exchange Server.|  
|**Podrobný stav klíčů pro zkušební načtení systému Windows RT**|Zobrazí podrobné informace o stavu zadaného klíče pro zkušební načtení systému Windows RT.|  
|**Přehled klíčů pro zkušební načtení systému Windows RT**|Zobrazí stav klíčů pro zkušební načtení systému Windows RT.|  



## <a name="driver-management"></a>Správa ovladačů  

V kategorii **Správa ovladačů** jsou uvedeny následující 13 sestav. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny ovladače**|Zobrazí seznam všech ovladačů.|  
|**Všechny ovladače pro konkrétní platformu**|Zobrazí všechny ovladače pro zadanou platformu.|  
|**Všechny ovladače v konkrétní imagi**|Zobrazí všechny ovladače v zadané imagi.|  
|**Všechny ovladače v konkrétní kategorii**|Zobrazí všechny ovladače v zadané kategorii.|  
|**Všechny ovladače v konkrétním balíčku**|Zobrazí všechny ovladače v zadaném balíčku.|  
|**Kategorie pro určitý ovladač**|Zobrazí kategorie pro určitý ovladač.|  
|**Počítače se selháním instalace ovladačů pro určitou kolekci**|Zobrazí počítače, ve kterých se nepodařilo nainstalovat ovladače pro určitou kolekci.|  
|**Sestava Katalogu ovladačů o shodě pro určitou kolekci**|Zobrazí sestavu Katalogu ovladačů o shodě pro určitou kolekci.|  
|**Sestava Katalogu ovladačů o shodě pro určitý počítač**|Zobrazí sestavu Katalogu ovladačů o shodě pro určitý počítač.|  
|**Sestava Katalogu ovladačů o shodě pro určité zařízení v určitém počítači**|Zobrazí sestavu Katalogu ovladačů o shodě pro určité zařízení v určitém počítači.|  
|**Sestava Katalogu ovladačů o shodě pro počítače v určité kolekci s určitým zařízením**|Zobrazí sestavu Katalogu ovladačů o shodě pro počítače v určité kolekci s určitým zařízením.|  
|**Ovladače se selháním instalace v určitém počítači**|Zobrazí ovladače, které se nepodařilo nainstalovat v určitém počítači.|  
|**Podporované platformy pro určitý ovladač**|Zobrazí platformy podporované pro určitý ovladač.|  



## <a name="endpoint-protection"></a>Funkce Endpoint Protection  

Do kategorie **Endpoint Protection** se zobrazí následující šest sestav. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Sestava o antimalwarové aktivitě**|Zobrazí přehled antimalwarové aktivity.|  
|**Celkový stav a historie antimalwaru**|Zobrazí celkový stav a historii antimalwaru.|  
|**Podrobnosti o malwaru počítače**|Zobrazí podrobnosti o zadaném počítači a seznamu malwaru, který se v něm vyskytuje.|  
|**Nakažené počítače**|Zobrazí seznam počítačů se s určitou zjištěnou hrozbou.|  
|**Nejohroženější uživatelé podle hrozeb**|Zobrazí seznam uživatelů s největším počtem zjištěných hrozeb.|  
|**Seznam hrozeb pro uživatele**|Zobrazí seznam hrozeb nalezených pro zadaný uživatelský účet.|  



## <a name="hardware---cd-rom"></a>Hardware – disk CD-ROM  

V kategorii **hardware – CD-ROM** se zobrazí následující čtyři sestavy. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Informace o jednotkách CD-ROM v určitém počítači**|Zobrazí informace o jednotkách CD-ROM v zadaném počítači.|  
|**Počítače pro určitého výrobce jednotek CD-ROM**|Zobrazí seznam počítačů, které obsahují jednotku CD-ROM vyrobenou zadaným výrobcem.|  
|**Počet jednotek CD-ROM podle výrobců**|Zobrazí počet jednotek CD-ROM v inventáři podle výrobců.|  
|**Historie – Historie jednotek CD-ROM v určitém počítači**|Zobrazí historii jednotek CD-ROM v inventáři pro zadaný počítač.|  



## <a name="hardware---disk"></a>Hardware-disk  

Do kategorie **hardware – disk** patří následující osm sestav. 

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače s určitou velikostí pevného disku**|Zobrazí seznam počítačů, které mají pevné disky zadané velikosti.|  
|**Počítače s nedostatkem volného místa na disku (méně volného místa než zadaná hodnota v %)**|Zobrazí seznam počítačů v určité kolekci, které mají na disku méně volného místa, než je zadaná hodnota.|  
|**Počítače s nedostatkem volného místa na disku (méně volného místa než zadaná hodnota v MB)**|Zobrazí seznam počítačů a disků, na kterých je nedostatek volného místa. Množství volného místa, které se kontroluje, se uvádí v MB.|  
|**Počet konfigurací fyzických disků**|Zobrazí počet pevných disků inventarizovaných podle kapacity disku.|  
|**Informace o discích v určitém počítači – logické disky**|Zobrazí souhrnné informace o logických discích v zadaném počítači.|  
|**Informace o discích v určitém počítači – oddíly**|Zobrazí souhrnné informace o oddílech disku v zadaném počítači.|  
|**Informace o discích v určitém počítači – fyzické disky**|Zobrazí souhrnné informace o fyzických discích v zadaném počítači.|  
|**Historie – historie místa na logických discích v určitém počítači**|Zobrazí historii inventáře logických diskových jednotek v zadaném počítači.|  



## <a name="hardware---general"></a>Hardware – obecné  

V kategorii **Hardware – obecné** jsou uvedené následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Informace o počítači pro určitý počítač**|Zobrazí souhrnné informace o zadaném počítači.|  
|**Počítače v určité pracovní skupině nebo doméně**|Zobrazí seznam počítačů v zadané pracovní skupině nebo doméně.|  
|**Třídy inventáře přiřazené určité kolekci**|Zobrazí třídy inventáře přiřazené k zadané kolekci.|  
|**Třídy inventáře povolené v určitém počítači**|Zobrazí třídy inventáře povolené v zadaném počítači.|  
|**Informace o zařízení Windows autopilotu**|Zobrazí informace o klientském zařízení potřebné pro registraci Windows autopilotu.|



## <a name="hardware---memory"></a>Hardware – paměť  

Do kategorie **hardware – paměť** patří následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače se změnou fyzické paměti**|Zobrazí seznam počítačů, ve kterých se od posledního cyklu inventáře změnila velikost paměti RAM.|  
|**Počítače s určitou velikostí paměti**|Zobrazí seznam počítačů, které mají zadanou velikost paměti RAM (celková velikosti fyzické paměti zaokrouhlená na nejbližší MB).|  
|**Počítače s nedostatkem paměti (s pamětí nižší nebo rovnou zadané hodnotě v MB)**|Zobrazí seznam počítačů, které mají nedostatek paměti. Velikost paměti, která se kontroluje, se uvádí v MB.|  
|**Počet konfigurací paměti**|Zobrazí počet počítačů v inventáři podle velikosti paměti RAM.|  
|**Informace o paměti v určitém počítači**|Zobrazí souhrnné informace o paměti v zadaném počítači.|  



## <a name="hardware---modem"></a>Hardware a modem  

Do kategorie **hardware-modem** patří následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače pro určitého výrobce jednotek modemů**|Zobrazí seznam počítačů, které mají modem od zadaného výrobce.|  
|**Počet modemů podle výrobce**|Zobrazí počet modemů v inventáři pro každého výrobce modemu.|  
|**Informace o modemu pro určitý počítač**|Zobrazí souhrnné informace o modemu v zadaném počítači.|  



## <a name="hardware---network-adapter"></a>Hardware – síťový adaptér  

Do kategorie **hardware – síťový adaptér** patří následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače s určitým síťovým adaptérem**|Zobrazí seznam počítačů, které mají určitý síťový adaptér.|  
|**Počet síťových adaptérů podle typu**|Zobrazí počty jednotlivých typů karet síťových adaptérů v inventáři.|  
|**Informace o síťových adaptérech v určitém počítači**|Zobrazí informace o síťových adaptérech nainstalovaných v zadaném počítači.|  



## <a name="hardware---processor"></a>Hardware – procesor  

Do kategorie **hardware – procesor** patří následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače s určitou rychlostí procesoru**|Zobrazí seznam počítačů, které mají procesor se zadanou rychlostí.|  
|**Počítače s rychlými procesory (s taktovací frekvencí vyšší nebo rovnou zadané hodnotě)**|Zobrazí seznam počítačů, které mají procesory s rychlostí vyšší než zadaná rychlost.|  
|**Počítače s pomalými procesory (s taktovací frekvencí nižší nebo rovnou zadané hodnotě)**|Zobrazí seznam počítačů, které mají procesory s rychlostí nižší nebo rovnou zadané taktovací frekvenci.|  
|**Počet rychlostí procesoru**|Zobrazí počet počítačů v inventáři podle rychlosti procesoru.|  
|**Informace o procesorech v určitém počítači**|Zobrazí informace o procesorech nainstalovaných v zadaném počítači.|  



## <a name="hardware---scsi"></a>Hardware – rozhraní SCSI  

V kategorii **hardware-SCSI** jsou uvedeny následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače s určitým typem karty SCSI**|Zobrazí seznam počítačů, které mají nainstalovanou zadanou kartu SCSI.|  
|**Počet typů karty SCSI**|Zobrazí počet karet SCSI v inventáři podle typu karty.|  
|**Informace o kartách SCSI v určitém počítači**|Zobrazí informace o kartách SCSI nainstalovaných v zadaném počítači.|  



## <a name="hardware---security"></a>Hardware – zabezpečení

Následující sestava je uvedena v kategorii **hardwarového zabezpečení** .

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Podrobnosti o stavu firmwaru na zařízeních**|Zobrazí podrobnosti o stavech rozhraní UEFI, funkce SecureBoot a čipu TPM. **Poznámka**: Tato sestava není ve verzi 1810.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Hardware – zvuková karta  

Do kategorie **hardware-SCSI** patří následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače s určitou zvukovou kartou**|Zobrazí seznam počítačů, které mají zadanou zvukovou kartu.|  
|**Počet zvukových karet**|Zobrazí počet počítačů v inventáři podle typu zvukové karty.|  
|**Informace o zvukových kartách v určitém počítači**|Zobrazí souhrnné informace o zvukových kartách v zadaném počítači.|  



## <a name="hardware---video-card"></a>Hardware – grafická karta  

Do kategorie **hardware –** videokarta patří následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače s určitou videokartou**|Zobrazí seznam počítačů, které mají zadanou videokartu.|  
|**Počet videokaret podle typu**|Zobrazí seznam všech grafických karet nainstalovaných na počítačích. Zobrazuje také číslo každého typu grafické karty.|  
|**Informace o videokartách v určitém počítači**|Zobrazí informace o videokartách nainstalovaných v zadaném počítači.|  



## <a name="migration"></a>Migrace  

Do kategorie **migrace** se zobrazí následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Klienti v seznamu vyloučení**|Zobrazí klienty, kteří jsou vyloučení z migrace.|  
|**Závislost na kolekci nástroje Configuration Manager**|Zobrazí objekty, které závisí na kolekci zdrojové hierarchie.|  
|**Vlastnosti úlohy migrace**|Tato sestava zobrazí obsah zadané úlohy migrace.|  
|**Úlohy migrace**|Tato sestava zobrazí seznam úloh migrace.|  
|**Objekty, jejichž migrace se nezdařila**|Zobrazí seznam objektů, u kterých se při posledním pokusu nezdařila migrace.|  



## <a name="network"></a>Síť  

Do kategorie **síť** se zobrazí následující šest sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počet IP adres podle podsítí**|Zobrazí počet IP adres v inventáři pro každou podsíť protokolu IP.|  
|**IP – všechny podsítě podle masky podsítě**|Zobrazí seznam všech podsítí protokolu IP a masek podsítě.|  
|**IP-počítače v určité podsíti**|Zobrazí seznam počítačů a informace o protokolu IP pro zadanou podsíť protokolu IP.|  
|**IP – informace o určitém počítači**|Zobrazí souhrnné informace o protokolu IP v zadaném počítači.|  
|**IP – informace o určité IP adrese**|Zobrazí souhrnné informace o zadané IP adrese.|  
|**MAC – počítače pro určitou adresu MAC**|Zobrazí název a IP adresu počítačů, které mají zadanou adresu MAC.|  



## <a name="operating-system"></a>Operační systém  

Do kategorie **operačního systému** se zobrazí následující 10 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Historie verzí operačního systému počítače**|Zobrazí historii inventáře operačního systému v zadaném počítači.|  
|**Počítače s určitým operačním systémem**|Zobrazí počítače s určitým operačním systémem.|  
|**Počítače s určitým operačním systémem a aktualizací Service Pack**|Zobrazí počítače s určitým operačním systémem a aktualizací Service Pack.|  
|**Počet verzí operačního systému**|Zobrazí počet počítačů v inventáři podle operačního systému.|  
|**Počet operačních systémů a aktualizací Service Pack**|Zobrazí počet počítačů v inventáři podle kombinací operačního systému a aktualizace Service Pack.|  
|**Služby – počítače s určitou spuštěnou službou**|Zobrazí seznam počítačů, ve kterých je spuštěná zadaná služba.|  
|**Služby – počítače se spuštěným serverem vzdáleného přístupu**|Zobrazí seznam počítačů, ve kterých je spuštěný server vzdáleného přístupu.|  
|**Služby – informace o službách v určitém počítači**|Zobrazí souhrnné informace o službách v zadaném počítači.|  
|**Podrobnosti o údržbě Windows 10 pro konkrétní kolekci**|Zobrazí obecné informace o údržbě systému Windows 10 pro určitou kolekci.|
|**Počítače s operačními systémy Windows Server**|Zobrazí seznam počítačů, ve kterých běží operační systémy Windows Server.|  


## <a name="power-management"></a>Řízení spotřeby  

V kategorii **řízení spotřeby** jsou uvedeny následující 18 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Řízení spotřeby – aktivita počítače**|Zobrazí graf s informacemi o aktivitě monitorů, počítačů a uživatelů pro zadanou kolekci za zadané časové období.|  
|**Řízení spotřeby – aktivita počítače podle počítače**|Zobrazí graf s informacemi o aktivitě monitorů, počítačů a uživatelů pro zadaný počítač v zadaném datu.|  
|**Řízení spotřeby – podrobnosti o aktivitě počítače**|Zobrazí seznam funkcí režimu spánku a probuzení z režimu spánku u počítačů v zadané kolekci v zadané datum a čas.|  
|**Řízení spotřeby – podrobnosti o počítači**|Zobrazí podrobné informace o možnostech napájení, nastavení napájení a schématech napájení použitých v zadaném počítači.|  
|**Řízení spotřeby – podrobnosti o počítačích nevytvářejících sestavy**|Zobrazí seznam, které v zadané datum a čas nehlásí žádnou aktivitu napájení.|  
|**Řízení spotřeby – vyloučené počítače**|Zobrazí seznam počítačů vyloučených ze schématu napájení.|  
|**Řízení spotřeby – počítače s více schématy napájení**|Zobrazí seznam počítačů, ve kterých platí více konfliktních nastavení napájení.|  
|**Řízení spotřeby – spotřeba energie**|Zobrazí celkovou měsíční spotřebu energie (v kWh) v zadané kolekci během zadaného časového období.|  
|**Řízení spotřeby – spotřeba energie na den**|Zobrazí celkovou spotřebu energie (v kWh) v zadané kolekci za posledních 31 dnů.|  
|**Řízení spotřeby – náklady na energii**|Zobrazí celkové měsíční náklady na energii v zadané kolekci během zadaného časového období.|  
|**Řízení spotřeby – náklady na energii na den**|Zobrazí celkové náklady na energii v zadané kolekci za posledních 31 dnů.|  
|**Řízení spotřeby – ekologický dopad**|Zobrazí graf, který znázorňuje emise oxidu uhličitého (CO2) způsobené zadanou kolekcí v zadaném časovém období.|  
|**Řízení spotřeby – ekologický dopad na den**|Zobrazí graf, který znázorňuje emise CO2 způsobené zadanou kolekcí za posledních 31 dnů.|  
|**Řízení spotřeby – podrobnosti o režimu spánku počítače**|Zobrazí podrobné informace o počítačích, které v zadaném časovém období nepřešel do režimu spánku nebo hibernace.|  
|**Řízení spotřeby – sestava režimu spánku**|Zobrazí seznam běžných příčin, které počítačům zabránily v přechodu do režimu spánku nebo hibernace. Zobrazuje také počet počítačů ovlivněných jednotlivými příčinami v zadaném časovém období.|  
|**Řízení spotřeby – možnosti napájení**|Zobrazí možnosti řízení spotřeby počítačů v zadané kolekci.|  
|**Řízení spotřeby – nastavení napájení**|Zobrazí souhrnný seznam nastavení napájení, která používají počítače v zadané kolekci.|  
|**Řízení spotřeby – podrobnosti o nastavení napájení**|Slouží k zobrazení dalších informací o počítačích, které byly zadány v sestavě **řízení spotřeby – nastavení napájení** .|  



## <a name="replication-traffic"></a>Provoz replikace  

Do kategorie **provoz replikace** se zobrazí následující 10 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Provoz replikace globálních dat na propojení (spojnicový graf)**|Zobrazí celkový provoz replikace globálních dat na zadaném propojení pro zadaný počet dnů.|  
|**Provoz replikace globálních dat na propojení (kruhový graf)**|Zobrazí celkový provoz replikace globálních dat na zadaném propojení pro zadaný počet dnů.|  
|**Provoz replikace hierarchie podle propojení**|Zobrazí celkový provoz replikace pro každé propojení v hierarchii během zadaného počtu dnů.|  
|**Provoz top deseti replikačních skupin hierarchie podle propojení (kruhový graf)**|Zobrazuje provoz replikace pro Top 10 replikačních skupin napříč celou hierarchií identifikovaných podle propojení.|  
|**Provoz replikace propojení**|Zobrazí celkový provoz replikace všech dat během zadaného počtu dnů.|  
|**Provoz replikační skupiny na propojení**|Zobrazí síťový provoz replikační skupiny přes zadané propojení replikace databáze během zadaného počtu dnů.|  
|**Provoz replikace dat lokality na propojení (spojnicový graf)**|Zobrazí celkový provoz replikace dat lokality na zadaném propojení pro zadaný počet dnů.|  
|**Provoz replikace dat lokality na propojení (kruhový graf)**|Zobrazí celkový provoz replikace dat lokality na zadaném propojení pro zadaný počet dnů.|  
|**Celkový provoz replikace hierarchie (spojnicový graf)**|Zobrazí celkovou replikaci globálních dat a dat lokality hierarchie pro všechny směry všech propojení během zadaného počtu dnů.|  
|**Celkový provoz replikace hierarchie (kruhový graf)**|Zobrazí celkovou replikaci globálních dat a dat lokality hierarchie pro všechny směry všech propojení během zadaného počtu dnů.|  



## <a name="site---client-information"></a>Lokalita – informace o klientech  

V kategorii **lokalita-informace o klientech** se zobrazí následující 19 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Podrobná sestava stavu přiřazení klienta**|Zobrazí podrobné informace o stavu přiřazení klienta.|  
|**Podrobnosti o selhání přiřazení klienta**|Zobrazí podrobné informace o selhání přiřazení klienta.|  
|**Podrobnosti o stavu přiřazení klienta**|Zobrazí přehled informací o stavu přiřazení klienta.|  
|**Podrobnosti o úspěchu přiřazení klienta**|Zobrazí podrobné informace o úspěšně přiřazených klientech.|  
|**Sestava selhání nasazení klienta**|Zobrazí podrobné informace o klientech, jejichž nasazení se nezdařilo.|  
|**Podrobnosti o sestavě nasazení klienta**|Zobrazí souhrnné informace o stavu instalací klientů.|  
|**Sestava úspěchu nasazení klienta**|Zobrazí podrobné informace o úspěšně nasazených klientech.|  
|**Klienti nepodporující komunikaci přes protokol HTTPS**|Zobrazí podrobné informace o každém klientovi, který spouští nástroj HTTPS Communication Readiness Tool, a sestav, které neumožňují komunikaci přes protokol HTTPS.|  
|**Nenainstalované přiřazené počítače pro určitou lokalitu**|Zobrazí seznam počítačů přiřazených k zadané lokalitě, ale nehlásí se do této lokality.|  
|**Počítače s určitou verzí klienta nástroje Configuration Manager**|Zobrazí seznam počítačů, ve kterých je spuštěná zadaná verze Configuration Managerho klientského softwaru.|  
|**Počet klientů a protokol pro komunikaci**|Zobrazí shrnutí komunikačních metod používaných klienty (HTTP nebo HTTPS).|  
|**Počet klientů přiřazených a nainstalovaných pro každou lokalitu**|Zobrazí počet počítačů přiřazených a nainstalovaných pro každou lokalitu. Klienti, kteří mají síťové umístění přidružené k několika lokalitám, se počítají jako nainstalované jenom v případě, že se do této lokality hlásí.|  
|**Počet klientů podporujících komunikaci přes protokol HTTPS**|Zobrazí podrobné informace o každém klientovi, který spouští nástroj HTTPS Communication Readiness Tool, a sestavy, které mají být buď schopné, nebo neschopné komunikovat přes protokol HTTPS.|  
|**Počet klientů pro každou lokalitu**|Zobrazí počet Configuration Manager klientů nainstalovaných kódem lokality.|  
|**Počet klientů nástroje Configuration Manager podle verzí klientů**|Zobrazí počet počítačů zjištěných Configuration Manager verzí klienta.|  
|**Podrobnosti o problémech ohlášených bodu stavu pro použití náhradní lokality pro zadanou kolekci**|Zobrazí podrobné informace o problémech hlášených klienty v zadané kolekci. Tito klienti musí mít přiřazený bod stavu pro použití náhradní lokality.|  
|**Podrobnosti o problémech ohlášených bodu stavu pro použití náhradní lokality pro zadanou lokalitu**|Zobrazí podrobné informace o problémech hlášených klienty v zadané lokalitě. Tito klienti musí mít přiřazený bod stavu pro použití náhradní lokality.|  
|**Shrnutí problémů ohlášených bodu stavu pro použití náhradní lokality**|Zobrazí informace o všech problémech hlášených klienty. Tito klienti musí mít přiřazený bod stavu pro použití náhradní lokality.|  
|**Shrnutí problémů ohlášených bodu stavu pro použití náhradní lokality pro určitou kolekci**|Zobrazí souhrnné informace o problémech hlášených klienty v zadané kolekci. Tito klienti musí mít přiřazený bod stavu pro použití náhradní lokality.|  



## <a name="site---discovery-and-inventory-information"></a>Lokalita – informace o zjišťování a inventáři  

Do kategorie **informace o zjišťování lokality a inventáři** patří následující 10 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Klienti nehlásící data v poslední době (za zadaný počet dní)**|Zobrazí seznam klientů, kteří v zadaném počtu dnů nehlásili data zjišťování, inventáře hardwaru nebo inventáře softwaru.|  
|**Počítače zjištěné určitou lokalitou**|Zobrazí seznam všech počítačů, ve kterých se zjistila Zadaná lokalita. Zobrazuje také datum posledního zjišťování.|  
|**Nedávno zjištěné počítače podle metody zjišťování**|Zobrazí seznam počítačů, které lokalita zjistila během zadaného počtu dnů. Obsahuje také seznam agentů, kteří je zjistili. Pokud počítač zjistil více agentů, může se v seznamu objevit více než jednou.|  
|**Počítače nezjištěné v poslední době (za zadaný počet dnů)**|Zobrazí seznam počítačů, které nedávno nezjistil Web. Zobrazuje také počet dnů od doby, kdy lokalita zjistila počítač.|  
|**Počítače neinventarizované v poslední době (za zadaný počet dnů)**|Zobrazí seznam počítačů, které tento web v poslední době nev inventáři. Zobrazuje také datum, kdy se klient v inventáři počítače nachází v inventáři.|  
|**Počítače, které by mohly sdílet stejný jedinečný identifikátor nástroje Configuration Manager**|Zobrazí seznam počítačů, které změnily název. Změna názvu je možnou příznakem, který počítač sdílí Configuration Manager jedinečný identifikátor s jiným počítačem.|  
|**Počítače s duplicitními adresami MAC**|Zobrazí počítače, které sdílejí stejnou adresu MAC.|  
|**Počet počítačů v doménách prostředků nebo pracovních skupinách**|Zobrazí počet počítačů v jednotlivých doménách prostředků nebo pracovních skupinách.|  
|**Informace o zjištění určitého počítače**|Zobrazí seznam agentů a lokalit, které zjistily zadaný počítač.|  
|**Data inventářů pro určitý počítač**|Zobrazí datum a čas posledního spuštění inventáře v zadaném počítači.|  



## <a name="site---general"></a>Lokalita – obecné  

V kategorii **lokalita-obecné** jsou uvedené následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítače v určité lokalitě**|Zobrazí seznam klientských počítačů v zadané lokalitě.|  
|**Stav lokalit v hierarchii**|Zobrazí seznam lokalit v hierarchii společně s informacemi o verzi a stavu lokality.|  
|**Stav aktualizace nástroje Configuration Manager v hierarchii**|Zobrazí informace o Configuration Manager aktualizacích lokality pro hierarchii.|  



## <a name="site---server-information"></a>Lokalita-informace o serveru  

V kategorii **lokalita – informace o serveru** se zobrazí následující sestava.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Role systému role lokality a servery systému lokality pro určitou lokalitu**|Zobrazí seznam serverů systému lokality a jejich rolí systému lokality pro určitou lokalitu.|  



## <a name="software---companies-and-products"></a>Software – společnosti a produkty  

V kategorii **software-společnosti a produkty** se zobrazí následující 15 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny produkty v inventáři od určité softwarové společnosti**|Zobrazí seznam inventarizovaných softwarových produktů a jejich verzí od zadané softwarové společnosti.|  
|**Všechny softwarové společnosti**|Zobrazí seznam všech společností, které vyrobily inventarizovaný software.|  
|**Všechny aplikace Windows**|Zobrazí souhrn nainstalovaných aplikací pro Windows. Vyhledává pomocí následujících kritérií: název aplikace, architektura nebo Vydavatel.|  
|**Počítače s určitým produktem**|Zobrazí seznam počítačů, ve kterých je zadaný produkt v inventáři, a verze tohoto produktu.|  
|**Počítače s určitým názvem a verzí produktu**|Zobrazí seznam počítačů s inventarizovanou zadanou verzí určitého produktu.|  
|**Počítače s určitým softwarem registrovaným na panelu Přidat nebo odebrat programy**|Zobrazí souhrn všech počítačů, které mají na panelu Přidat nebo odebrat programy nebo Programy a funkce zaregistrovaný zadaný software.|  
|**Počet všech produktů a verzí v inventáři**|Zobrazí seznam softwarových produktů a verzí zařazených do inventáře a počet počítačů, ve kterých jsou nainstalované.|  
|**Počet produktů a verzí v inventáři pro určitý produkt**|Zobrazí seznam verzí zadaného produktu zařazených do inventáře a počet počítačů, ve kterých jsou nainstalované.|  
|**Počet všech instancí softwaru zaregistrovaného na panelu Přidat nebo odebrat programy**|Zobrazí souhrn všech instancí softwaru nainstalovaného a zaregistrovaného na panelu Přidat nebo odebrat programy nebo Programy a funkce v počítačích v zadané kolekci.|  
|**Počet instancí určitého softwaru zaregistrovaného na panelu Přidat nebo odebrat programy**|Zobrazí počet instancí zadaných softwarových balíčků nainstalovaných a zaregistrovaných na panelu Přidat nebo odebrat programy nebo Programy a funkce.|  
|**Výchozí počty prohlížečů**|Zobrazuje počet klientů s výchozím webovým prohlížečem jako výchozí Windows. <br>Pro Common BrowserProgIDs použijte následující referenci:<br> -AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge<br> Dotazy. HTTP: Microsoft Internet Explorer<br> -ChromeHTML: Google Chrome<br> -OperaStable: Opera software<br> -FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> -Neznámé: operační systém klienta nepodporuje dotaz, dotaz se nespustí nebo uživatel není přihlášený.|
|**Instalace určených aplikací pro Windows**|Tato sestava obsahuje seznam všech počítačů se zadanou aplikací pro Windows.|  
|**Produkty v určitém počítači**|Zobrazí souhrn softwarových produktů zařazených do inventáře a jejich výrobců v zadaném počítači.|  
|**Software v určitém počítači zaregistrovaný na panelu Přidat nebo odebrat programy**|Zobrazí souhrn softwaru nainstalovaného v zadaném počítači, který je zaregistrovaný na panelu Přidat nebo odebrat programy nebo Programy a funkce.|  
|**Aplikace pro Windows nainstalované pro určitého uživatele**|Zobrazí všechny aplikace pro Windows nainstalované pro určitého uživatele.|  



## <a name="software---files"></a>Software – soubory  

Do kategorie **software – soubory** patří následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny soubory v inventáři pro určitý produkt**|Zobrazí souhrn souborů v inventáři přidružených k zadanému softwarovému produktu.|  
|**Všechny soubory v inventáři pro určitý počítač**|Zobrazí souhrn všech souborů zařazených do inventáře v určitém počítači.|  
|**Srovnání inventáře softwaru ve dvou počítačích**|Zobrazí rozdíly mezi hlášenými inventáři softwaru pro dva zadané počítače.|  
|**Počítače s určitým souborem**|Zobrazí seznam počítačů, které mají shromážděný inventář softwaru pro určitý název souboru. Pokud počítač obsahuje více kopií souboru, může se v seznamu objevit více než jednou.|  
|**Počet počítačů s určitým názvem souboru**|Zobrazí počet počítačů, které mají shromážděný inventář softwaru pro určitý název souboru.|  



## <a name="software-distribution---application-monitoring"></a>Distribuce softwaru – monitorování aplikací  

Do kategorie **distribuce softwaru – monitorování aplikací** se zobrazí následující 10 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechna nasazení aplikací (rozšířené)**|Zobrazí podrobné souhrnné informace o všech nasazeních aplikací.|  
|**Všechna nasazení aplikací (základní)**|Zobrazí souhrnné informace o všech nasazeních aplikací.|  
|**Kompatibilita aplikací**|Zobrazí informace o kompatibilitě zadané aplikace v zadané kolekci.|  
|**Nasazení aplikace na prostředek**|Zobrazí aplikace nasazené do určitého zařízení nebo pro určitého uživatele.|  
|**Chyby infrastruktury aplikace**|Zobrazí chyby infrastruktury aplikace. Mezi tyto chyby patří interní problémy s infrastrukturou nebo chyby způsobené neplatnými pravidly požadavků.|  
|**Podrobný stav využití aplikací**|Zobrazí podrobnosti o využití nainstalovaných aplikací.|  
|**Souhrnný stav využití aplikací**|Zobrazí souhrnné informace o využití nainstalovaných aplikací.|  
|**Nasazení pořadí úkolů obsahující aplikaci**|Zobrazí nasazení pořadí úkolů, která provádějí instalaci zadané aplikace.|  


## <a name="software-distribution---collections"></a>Distribuce softwaru – kolekce  

Do kategorie **distribuce softwaru – kolekce** patří níže uvedené tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny kolekce**|Zobrazí všechny kolekce v hierarchii.|  
|**Všechny prostředky v určité kolekci**|Zobrazí všechny prostředky v zadané kolekci.|  
|**Časová období údržby dostupná pro zadaného klienta**|Zobrazí všechna období údržby, která jsou dostupná pro zadaného klienta.|  



## <a name="software-distribution---content"></a>Distribuce softwaru-obsah  

Do kategorie **distribuce softwaru – obsah** patří následující 16 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny aktivní distribuce obsahu**|Zobrazí všechny distribuční body, ve kterých právě probíhá instalace nebo odebírání obsahu.|  
|**Veškerý obsah**|Zobrazí všechny aplikace a balíčky v lokalitě.|  
|**Veškerý obsah v určitém distribučním bodě**|Zobrazí veškerý obsah, které je právě nainstalovaný v zadaném distribuční bodě.|  
|**Všechny distribuční body**|Zobrazí informace o distribučních bodech pro každou lokalitu.|  
|**Všechny stavové zprávy pro určitý balíček v určitém distribučním bodě**|Zobrazí všechny stavové zprávy pro určitý balíček v určitém distribučním bodě.|  
|**Stav distribuce obsahu aplikací**|Zobrazí informace o stavu distribuce obsahu aplikací.|  
|**Aplikace cílené na skupinu distribučních bodů**|Zobrazí informace o obsahu aplikací nasazeném do zadané skupiny distribučních bodů.|  
|**Nesynchronizované aplikace v zadané skupině distribučních bodů**|Zobrazí aplikace, u kterých přidružené soubory obsahu nebyly v zadané skupině distribučních bodů aktualizovány na nejnovější verzi.|  
|**Skupina distribučních bodů**|Zobrazí informace o zadané skupině distribučních bodů.|  
|**Souhrn využití distribučních bodů**|Zobrazí souhrnné informace o využití jednotlivých distribučních bodů.|  
|**Stav distribuce zadaného balíčku**|Zobrazí stav distribuce zadaného obsahu balíčku v jednotlivých distribučních bodech.|  
|**Balíčky cílené na skupinu distribučních bodů**|Zobrazí informace o balíčcích cílených na zadanou skupinu distribučních bodů.|  
|**Nesynchronizované balíčky v zadané skupině distribučních bodů**|Zobrazí balíčky, u kterých přidružené soubory obsahu nebyly v zadané skupině distribučních bodů aktualizovány na nejnovější verzi.|  
|**Odmítnutí obsahu zdroje sdílené mezipaměti**|Zobrazí počet zamítnutí zdroje sdílené mezipaměti na hraniční skupinu.|
|**Podmínka odmítnutí obsahu zdroje sdílené mezipaměti**|Zobrazí zdroje sdílené mezipaměti, které odmítly poskytovat obsah na základě podmínky.|
|**Podrobnosti odmítnutí obsahu zdroje sdílené mezipaměti**|Zobrazuje název obsahu, který byl odmítnut zdrojem partnerského vztahu.|



## <a name="software-distribution---package-and-program-deployment"></a>Distribuce softwaru – nasazení balíčků a programů 

Do kategorie **distribuce softwaru-Package a program Deployment** se zobrazí následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechna nasazení zadaného balíčku a programu**|Zobrazí informace o všech nasazeních zadaného balíčku a programu.|  
|**Všechna nasazení balíčků a programů**|Zobrazí všechna nasazení balíčků a programů v této lokalitě.|  
|**Všechna nasazení balíčků a programů do zadané kolekce**|Zobrazí všechna nasazení balíčků a programů do zadané kolekce.|  
|**Všechna nasazení balíčků a programů do zadaného počítače**|Zobrazí všechna nasazení balíčků a programů použitá v zadaném počítači.|  
|**Všechna nasazení balíčků a programů pro zadaného uživatele**|Zobrazí všechna nasazení balíčků a programů pro zadaného uživatele.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Distribuce softwaru-stav nasazení balíčku a programu  

Do kategorie **distribuce softwaru – balíček a stav nasazení programu** se zobrazí následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechna nasazení balíčků a programů systémových prostředků a jejich stav**|Zobrazí všechna nasazení balíčků a programů v lokalitě a souhrn stavu každého nasazení.|  
|**Všechny systémové prostředky v zadaném stavu pro zadané nasazení balíčku a programu**|Zobrazí seznam prostředků v zadaném stavu pro zadané nasazení balíčku a programu.|  
|**Graf – stav dokončení nasazení balíčku a programu po hodinách**|Zobrazí procento počítačů, ve kterých se úspěšně nainstaloval balíček. Seznam se uspořádá každou hodinu, protože správce vytvoří nasazení balíčku a programu. Může sloužit ke sledování průměrné doby nasazení balíčku a programu.|  
|**Stavové zprávy o nasazení balíčku a programu pro zadaného klienta a nasazení**|Zobrazí stavové zprávy hlášené pro zadaný počítač a nasazení balíčku a programu.|  
|**Stav zadaného nasazení balíčku a programu**|Zobrazí shrnutí stavu zadaného nasazení balíčku a programu.|  



## <a name="software-metering"></a>Monitorování míry využití softwaru  

Do kategorie **monitorování míry využívání softwaru** se zobrazí následující 13 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechna pravidla monitorování míry využívání softwaru používaná pro tuto lokalitu**|Zobrazí seznam všech pravidel monitorování míry využívání softwaru v lokalitě.|  
|**Počítače s nainstalovaným monitorovaným programem nespuštěným od zadaného data**|Zobrazí všechny počítače s určenou monitorovanou aplikací, ale žádný uživatel nespouštěl program od zadaného data.|  
|**Počítače spouštějící určitý monitorovaný softwarový program**|Zobrazí seznam počítačů, ve kterých se v zadaném měsíci a roce spouštěly programy odpovídající zadanému pravidlu monitorování míry využívání softwaru.|  
|**Souběžné používání všech monitorovaných softwarových programů**|Zobrazí maximální počet uživatelů, kteří v zadaném měsíci a roce souběžně spustili jednotlivé monitorované softwarové programy.|  
|**Analýza trendu souběžného používání určitého monitorovaného softwarového programu**|Zobrazí maximální počet uživatelů, kteří v jednotlivých měsících v minulém roce souběžně spustili zadaný monitorovaný softwarový program.|  
|**Instalační základna všech monitorovaných softwarových programů**|Zobrazí počet počítačů, ve kterých jsou podle inventáře softwaru nainstalované monitorované softwarové programy. Tato sestava vyžaduje, aby počítač shromažďuje inventář softwaru.|  
|**Průběh vytváření souhrnů monitorování míry využívání softwaru**|Zobrazí čas zpracování nedávno vytvořeného souhrnu dat monitorování na serveru lokality. Sestavy monitorování míry využívání softwaru odrážejí data měření zpracovaná pouze před těmito daty.|  
|**Shrnutí denních dob využití určitého monitorovaného softwarového programu**|Zobrazí průměrné počty využití určitého programu za posledních 90 dnů rozepsané podle hodiny a dne.|  
|**Celkové využití všech monitorovaných softwarových programů**|Zobrazí počet uživatelů, kteří v zadaném měsíci a roce spustili programy a kteří splňují všechna pravidla monitorování míry využívání softwaru. Tato pravidla jsou pro místně instalovaný software nebo pro používání Terminálové služby.|  
|**Celkové využití všech monitorovaných softwarových programů na serverech Windows Terminal Server**|Zobrazí počet uživatelů, kteří v zadaném měsíci a roce spustili pomocí Terminálové služby programy odpovídající jednotlivým pravidlům monitorování míry využívání softwaru.|  
|**Analýza trendu celkového využití určitého monitorovaného softwarového programu**|Zobrazí počet uživatelů, kteří v jednotlivých měsících v minulém roce spustili programy a kteří odpovídají zadanému pravidlu monitorování míry využívání softwaru. Tato pravidla jsou pro místně instalovaný software nebo pro používání Terminálové služby.|  
|**Analýza trendu celkového využití určitého monitorovaného softwarového programu na serverech Windows Terminal Server**|Zobrazí počet uživatelů, kteří v jednotlivých měsících v minulém roce spustili programy a kteří odpovídají zadanému pravidlu monitorování míry využívání softwaru. Tato pravidla se používají pro používání Terminálové služby.|  
|**Uživatelé spouštějící určitý monitorovaný softwarový program**|Zobrazí seznam uživatelů, kteří v zadaném měsíci a roce spustili programy a kteří odpovídají zadanému pravidlu monitorování míry využívání softwaru.|  



## <a name="software-updates---a-compliance"></a>Aktualizace softwaru – A – dodržování předpisů  

Do kategorie **aktualizace softwaru – A dodržování předpisů** patří níže uvedené osm sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Dodržování přepisů 1 – celkové dodržování předpisů**|Zobrazí celková data dodržování přepisů pro skupinu softwarových aktualizací.|  
|**Dodržování předpisů 2 – určitá aktualizace softwaru**|Zobrazí data dodržování předpisů pro určitou aktualizaci softwaru.|  
|**Dodržování předpisů 3 – skupina aktualizací (podle aktualizací)**|Zobrazí data dodržování předpisů pro softwarové aktualizace definované ve skupině softwarových aktualizací.|  
|**Dodržování předpisů 4 – aktualizace podle výrobce a měsíce roku**|Zobrazí data dodržování předpisů pro aktualizace softwaru vydané určitým výrobcem v zadaném měsíci a roce.|  
|**Dodržování předpisů 5 – určitý počítač**|Tato sestava vrací data dodržování předpisů o aktualizacích softwaru pro zadaný počítač. Pokud chcete omezit množství vrácených informací, můžete zadat výrobce a klasifikaci aktualizací softwaru.|  
|**Dodržování předpisů 6 – stavy určité aktualizace softwaru (sekundární)**|Zobrazí počet a procento počítačů v různých stavech dodržování předpisů pro zadanou aktualizaci softwaru.|  
|**Dodržování předpisů 7 – počítače v určitém stavu dodržování předpisů pro skupinu aktualizací (sekundární)**|Zobrazí všechny počítače v kolekci, které mají u určité skupiny aktualizací softwaru zadaný celkový stav dodržování předpisů.|  
|**Dodržování předpisů 8 – počítače v určitém stavu dodržování předpisů pro aktualizaci (sekundární)**|Zobrazí všechny počítače v kolekci, které mají u určité aktualizace softwaru zadaný stav dodržování předpisů.|  
|**Dodržování předpisů 9 – celkový stav a dodržování předpisů**|Zobrazí celkový stav a data dodržování předpisů pro skupinu aktualizací softwaru. (počínaje verzí 1806)| 


## <a name="software-updates---b-deployment-management"></a>Aktualizace softwaru-B – Správa nasazení  

Do kategorie **aktualizace softwaru – B – Správa nasazení** patří následující osm sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Správa 1 – nasazení skupiny aktualizací**|Zobrazí všechna nasazení, která obsahují všechny aktualizace softwaru definované v zadané skupině aktualizací softwaru.|  
|**Správa 2 – nenasazené vyžadované aktualizace**|Zobrazí všechny aktualizace softwaru specifické pro dodavatele, které klienti zjišťují podle potřeby, ale správce není nasazený do zadané kolekce.|  
|**Správa 3 – aktualizace v nasazení**|Zobrazí aktualizace softwaru obsažené v zadaném nasazení.|  
|**Správa 4 – nasazení cílící na kolekci**|Zobrazí všechna nasazení aktualizací softwaru, která se zaměřují na zadanou kolekci.|  
|**Správa 5 – nasazení cílící na počítač**|Zobrazí všechna nasazení aktualizací softwaru použitá v zadaném počítači.|  
|**Správa 6 – nasazení obsahující určitou aktualizaci**|Zobrazí všechna nasazení, která obsahují zadanou aktualizaci softwaru, a přidruženou cílovou kolekci pro nasazení.|  
|**Správa 7 – aktualizace v nasazení s chybějícím obsahem**|Zobrazí aktualizace softwaru v zadaném nasazení, které nemají načtený všechen přidružený obsah. Tento stav brání klientům v instalaci aktualizace, což zabrání nasazení v dosažení 100% dodržování předpisů.|  
|**Správa 8 – počítače s chybějícím obsahem (sekundární)**|Zobrazí všechny počítače vyžadující zadanou aktualizaci softwaru, ale přidružený obsah ještě není distribuován do distribučního bodu.|  



## <a name="software-updates---c-deployment-states"></a>Aktualizace softwaru-stavy nasazení jazyka C  

Do kategorie **aktualizace softwaru – C – stavy nasazení** patří následující šest sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Stavy 1 – stavy vynucení pro nasazení**|Zobrazí stavy vynucení pro zadané nasazení aktualizací softwaru, což je většinou druhá fáze vyhodnocování nasazení.|  
|**Stavy 2 – stavy vyhodnocování nasazení**|Zobrazí stav vyhodnocení pro zadané nasazení aktualizací softwaru, což je většinou první fáze vyhodnocování nasazení.|  
|**Stavy 3 – stavy pro nasazení a počítač**|Zobrazí stavy všech aktualizací softwaru v zadaném nasazení pro zadaný počítač.|  
|**Stavy 4 – počítače v určitém stavu pro nasazení (sekundární)**|Zobrazí všechny počítače v zadaném stavu nasazení aktualizace softwaru.|  
|**Stavy 5 – stavy pro aktualizaci v nasazení (sekundární)**|Zobrazí shrnutí stavů zadané aktualizace softwaru, na kterou se zaměřuje zadané nasazení.|  
|**Stavy 6 – počítače v určitém stavu vynucení pro aktualizaci (sekundární)**|Zobrazí všechny počítače v zadaném stavu vynucení pro zadanou aktualizaci softwaru.|  



## <a name="software-updates---d-scan"></a>Aktualizace softwaru-D – prohledávání  

Do kategorie **aktualizace softwaru-D Scan** se zobrazí následující čtyři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Kontrola 1 – poslední stavy kontroly podle kolekce**|Určete kolekci pro zobrazení počtu počítačů v jednotlivých stavech kontroly dodržování předpisů. Klienti vrátí stav při poslední kontrole dodržování předpisů.|  
|**Kontrola 2 – poslední stavy kontroly podle lokality**|Zadejte lokalitu, pro kterou chcete zobrazit počet počítačů v každém stavu kontroly dodržování předpisů. Klienti vrátí stav při poslední kontrole dodržování předpisů.|  
|**Kontrola 3 – klienti v kolekci vykazující určitý stav (sekundární)**|Zobrazí všechny počítače ze zadané kolekce, kteří měli při poslední kontrole dodržování předpisů zadaný stav dodržování předpisů.|  
|**Kontrola 4 – klienti v lokalitě vykazující určitý stav (sekundární)**|Zadejte lokalitu, aby se zobrazily všechny počítače se zadaným stavem kontroly dodržování předpisů. Klienti vrátí stav během poslední kontroly dodržování předpisů.|  



## <a name="software-updates---e-troubleshooting"></a>Aktualizace softwaru-E – řešení potíží  

Do kategorie **aktualizace softwaru-E řešení potíží** patří následující čtyři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Řešení potíží 1-chyby kontroly**|Zobrazí chyby kontroly v lokalitě a počet počítačů, ve kterých k jednotlivým chybám došlo.|  
|**Řešení potíží 2 – chyby nasazení**|Zobrazí chyby nasazení v lokalitě a počet počítačů, ve kterých k jednotlivým chybám došlo.|  
|**Řešení potíží 3-počítače se selháním kvůli určité chybě kontroly (sekundární)**|Zobrazí seznam počítačů, ve kterých se kvůli zadané chybě nezdařila kontrola.|  
|**Řešení potíží 4 – počítače se selháním kvůli určité chybě nasazení (sekundární)**|Zobrazí seznam počítačů, ve kterých se kvůli zadané chybě nezdařilo nasazení aktualizací.|  



## <a name="state-migration"></a>Migrace stavu  

Do kategorie **migrace stavu** se zobrazí následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Informace o migraci stavu pro určitý zdrojový počítač**|Zobrazí informace o migraci stavu pro zadaný počítač.|  
|**Informace o migraci stavu pro určitý bod migrace stavu**|Zobrazí informace o migraci stavu pro zadaný bod migrace stavu.|  
|**Body migrace stavu pro určitou lokalitu**|Zobrazí body migrace stavu pro zadanou lokalitu.|  



## <a name="status-messages"></a>Stavové zprávy  

Do kategorie **stavové zprávy** se zobrazí následující 12 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny zprávy s určitým ID zprávy**|Zobrazí seznam stavových zpráv, které mají zadané ID zprávy.|  
|**Klienti hlásící chyby za posledních 12 hodin pro určitou lokalitu**|Zobrazí seznam počítačů a součástí, které za posledních 12 hodin ohlásily chybu, a počet zaznamenaných chyb.|  
|**Zprávy součástí za posledních 12 hodin**|Zobrazí seznam zpráv součástí za posledních 12 hodin pro zadaný kód lokality, počítač a součást.|  
|**Zprávy součástí za poslední hodinu**|Zobrazí seznam stavových zpráv vytvořených za poslední hodinu zadanou součástí v zadaném počítači v zadané lokalitě.|  
|**Počet zpráv součásti za poslední hodinu pro určitou lokalitu**|Zobrazí počet stavových zpráv podle součásti a závažnosti zaznamenaných za poslední hodinu v zadané lokalitě.|  
|**Počet chyb za posledních 12 hodin**|Zobrazí počet stavových zpráv o chybách součástí serveru za posledních 12 hodin.|  
|**Závažné chyby (podle součásti)**|Zobrazí seznam počítačů hlásících závažné chyby podle součásti.|  
|**Závažné chyby (podle názvu počítače)**|Zobrazí seznam počítačů hlásících závažné chyby podle názvu počítače.|  
|**Posledních 1000 zpráv pro určitý počítač (chyby a upozornění)**|Zobrazí souhrn posledních 1000 stavových zpráv o chybách a upozorněních týkajících se součástí pro zadaný počítač.|  
|**Posledních 1000 zpráv pro určitý počítač (chyby a upozornění a informace)**|Zobrazí souhrn posledních 1000 stavových zpráv o chybách, upozorněních a informacích týkajících se součástí pro zadaný počítač.|  
|**Posledních 1000 zpráv pro určitý počítač (chyby)**|Zobrazí souhrn posledních 1000 stavových zpráv o chybách týkajících se součástí serveru pro zadaný počítač.|  
|**Posledních 1000 zpráv pro určitou součást serveru**|Zobrazí souhrn posledních 1000 stavových zpráv pro zadanou součást serveru.|  



## <a name="status-messages---audit"></a>Stavové zprávy-audit  

Do kategorie **stavové zprávy-audit** patří následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny zprávy o auditu pro určitého uživatele**|Zobrazí souhrn všech zpráv o auditu pro zadaného uživatele. Zprávy o auditu popisují akce provedené v konzole Configuration Manager, které přidávají, mění nebo odstraňují objekty v Configuration Manager.|  
|**Vzdálené řízení – všechny počítače vzdáleně řízené určitým uživatelem**|Zobrazí souhrn stavových zpráv s označením vzdáleného řízení klientských počítačů zadaným uživatelem.|  
|**Vzdálené řízení – informace o veškerém vzdáleném řízení**|Zobrazí souhrn stavových zpráv, které se týkají vzdáleného řízení klientských počítačů.|  



## <a name="task-sequence---deployment-status"></a>Pořadí úkolů – stav nasazení  

Do kategorie **pořadí úkolů – stav nasazení** se zobrazí následující 11 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny systémové prostředky pro nasazení pořadí úkolů v určitém stavu**|Zobrazí seznam cílových počítačů pro zadané nasazení pořadí úkolů v zadaném stavu nasazení.|  
|**Všechny systémové prostředky pro nasazení pořadí úkolů nacházející se v určitém stavu a dostupné neznámým počítačům**|Zobrazí seznam cílových počítačů pro zadané nasazení pořadí úkolů v zadaném stavu nasazení.|  
|**Počet systémových prostředků s přiřazenými a zatím nespuštěnými nasazeními pořadí úkolů**|Zobrazí počet počítačů, které přijaly pořadí úloh, ale nespustí pořadí úkolů.|  
|**Historie nasazení pořadí úkolů v počítači**|Zobrazí stav jednotlivých kroků zadaného nasazení pořadí úkolů v zadaném cílovém počítači. Pokud se nevrátí žádný záznam, pořadí úkolů se na počítači nespustilo.|  
|**Seznam počítačů s překročením určité doby pro spuštění nasazení pořadí úkolů**|Zobrazí seznam cílových počítačů, které překročily zadaný interval pro spuštění pořadí úkolů.|  
|**Doba spuštění určitého nasazení pořadí úkolů v určitém cílovém počítači**|Zobrazí celkovou dobu, kterou trvalo úspěšné dokončení zadaného pořadí úkolů v zadaném počítači.|  
|**Doba spuštění každého kroku nasazení pořadí úkolů v určitém cílovém počítači**|Zobrazí dobu trvání jednotlivých kroků zadaného nasazení pořadí úkolů v zadaném cílovém počítači.|  
|**Stav určitého nasazení pořadí úkolů pro určitý počítač**|Zobrazí souhrn stavu zadaného nasazení pořadí úkolů v zadaném počítači.|  
|**Stav nasazení pořadí úkolů v neznámém cílovém počítači**|Zobrazí stav zadaného nasazení pořadí úkolů v zadaném neznámém cílovém počítači.|  
|**Shrnutí stavu určitého nasazení pořadí úkolů**|Zobrazí shrnutí stavu všech prostředků, na které se zaměřuje určité nasazení.|  
|**Shrnutí stavu určitého nasazení pořadí úkolů dostupného pro neznámé počítače**|Zobrazí shrnutí stavu všech prostředků, které cílí na zadané nasazení, které je dostupné pro kolekci obsahující neznámé počítače.|  



## <a name="task-sequence---deployments"></a>Pořadí úkolů – nasazení  

V kategorii **pořadí úkolů – nasazení** se zobrazí následující 11 sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny systémové prostředky aktuálně spuštěné v určité skupině nebo fázi určitého nasazení pořadí úkolů**|Zobrazí seznam počítačů, které jsou právě spuštěné v zadané skupině nebo fázi zadaného nasazení pořadí úkolů.|  
|**Všechny systémové prostředky s nezdařeným nasazením pořadí úkolů v určité skupině nebo fázi**|Zobrazí seznam počítačů, ve kterých došlo v zadané skupině nebo fázi zadaného nasazení pořadí úkolů k selhání.|  
|**Všechna nasazení pořadí úkolů**|Zobrazí podrobnosti o všech nasazeních pořadí úkolů zahájených z aktuální lokality.|  
|**Všechna nasazení pořadí úkolů dostupná pro neznámé počítače**|Zobrazí podrobnosti o všech nasazeních pořadí úkolů zahájených z lokality a nasazených do kolekcí, které obsahují neznámé počítače.|  
|**Počet selhání v každé fázi nebo skupině určitého pořadí úkolů**|Zobrazí počet selhání v každé fázi nebo skupině zadaného pořadí úkolů.|  
|**Počet selhání v každé fázi nebo skupině určitého nasazení pořadí úkolů**|Zobrazí počet selhání v každé fázi nebo skupině zadaného nasazení pořadí úkolů.|  
|**Stav nasazení u všech nasazení pořadí úkolů**|Zobrazí celkový průběh všech nasazení pořadí úkolů.|  
|**Průběh spuštěného pořadí úkolů**|Zobrazí průběh zadaného pořadí úkolů.|  
|**Průběh spuštěného nasazení pořadí úkolů**|Zobrazí souhrnné informace o zadaném nasazení pořadí úkolů.|  
|**Průběh všech nasazení pro určité pořadí úkolů**|Zobrazí průběh všech nasazení zadaného pořadí úkolů.|  
|**Souhrnná sestava pro nasazení pořadí úkolů**|Zobrazí souhrnné informace o zadaném nasazení pořadí úkolů.|  



## <a name="task-sequence---progress"></a>Pořadí úkolů – průběh  

Do kategorie **pořadí úkolů** se zobrazí následující pět sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Graf – týdenní průběh pořadí úkolů**|Zobrazí týdenní průběh pořadí úkolů od data nasazení.|  
|**Průběh pořadí úkolů**|Zobrazí průběh zadaného pořadí úkolů.|  
|**Průběh všech pořadí úkolů**|Zobrazí shrnutí průběhu všech pořadí úkolů.|  
|**Průběh pořadí úkolů pro nasazení operačních systémů**|Zobrazí průběh všech pořadí úkolů, která nasazují operační systémy.|  
|**Stav všech neznámých počítačů**|Zobrazí seznam počítačů, které byly neznámé v době, kdy spustily nasazení pořadí úloh, a zda jsou nyní známými počítači.|  



## <a name="task-sequences---references"></a>Pořadí úkolů – odkazy  

Následující sestava je uvedena v kategorii **pořadí úkolů – odkazy** .

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Obsah odkazovaný určitým pořadím úkolů**|Zobrazí obsah odkazovaný zadaným pořadím úkolů.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Spřažení zařízení a uživatele  

Do kategorie **spřažení zařízení a uživatele** se zobrazí následující dvě sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Přiřazení spřažení zařízení čekajících uživatelů podle kolekce**|Tato sestava zobrazí všechna nevyřízená přiřazení spřažení uživatelských zařízení podle dat využití pro členy určité kolekce.|  
|**Přiřazení spřažení uživatelských zařízení na kolekci**|Zobrazí všechna přidružení uživatelských zařízení pro zadanou kolekci a seskupí výsledky podle typu kolekce (například uživatel nebo zařízení).|  



## <a name="user-data-and-profiles-health"></a>Stav profilů a dat uživatele  

Do kategorie **stav profilů a dat uživatele** se zobrazí následující čtyři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Sestava přesměrování složky – podrobnosti**|Zobrazí podrobnosti o stavu přesměrování složky pro každou z přesměrovaných složek pro daného uživatele.|  
|**Sestava stavu uživatelských profilů roamingu – podrobnosti**|Zobrazí podrobné informace o stavu uživatelského profilu roamingu pro zadaného uživatele.|  
|**Sestava stavu profilů a dat uživatele – podrobnosti**|Zobrazí podrobnosti o chybě nebo upozornění pro přesměrování složky nebo uživatelské profily roamingu. Tato sestava je cílem podrobností ze sestavy souhrnu.|  
|**Sestava stavu profilů a dat uživatele – souhrn**|Zobrazí souhrn stavů přesměrování složky a uživatelských profilů roamingu.|  



## <a name="users"></a>Uživatelé  

Do kategorie **Uživatelé** jsou uvedené následující tři sestavy.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Počítačů pro určité uživatelské jméno**|Zobrazí seznam počítačů, které použil zadaný uživatel.|  
|**Počet uživatelů podle domény**|Zobrazí počet uživatelů v každé doméně.|  
|**Uživatelé v určité doméně**|Zobrazí seznam uživatelů a jejich součástí v zadané doméně.|  



## <a name="virtual-applications"></a>Virtuální aplikace  

V kategorii **virtuální aplikace** se zobrazí následující sedm sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Výsledky virtuálního prostředí sady App-V**|Zobrazí informace o zadaném virtuálním prostředí v zadaném stavu v zadané kolekci.|  
|**Výsledky virtuálního prostředí sady App-V pro prostředek**|Zobrazí informace o zadaném virtuálním prostředí pro zadaný prostředek. Zobrazuje také všechny typy nasazení v zadaném virtuálním prostředí.|  
|**Stav virtuálního prostředí sady App-V**|Zobrazí informace o dodržování předpisů v zadaném virtuálním prostředí a kolekci.|  
|**Počítače s určitou virtuální aplikací**|Zobrazí shrnutí počítačů, které mají zadaného zástupce aplikace App-V vytvořeného pomocí aplikace Application Virtualization Management Sequencer.|  
|**Počítače s určitou sadou virtuální aplikace**|Zobrazí shrnutí počítačů, které mají zadaný balíček aplikace App-V.|  
|**Počet všech instancí balíčků virtuální aplikace**|Zobrazí počet zjištěných balíčků aplikace App-V.|  
|**Počet všech instancí virtuálních aplikací**|Zobrazí počet zjištěných aplikací App-V.|  



## <a name="vulnerability-assessment"></a>Posouzení ohrožení zabezpečení

V kategorii **posouzení ohrožení zabezpečení** je uvedená jedna sestava.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Celková sestava posouzení ohrožení zabezpečení**|Identifikuje ohrožení zabezpečení, správy a dodržování předpisů pro určitý počítač.|  



## <a name="wake-on-lan"></a>Funkce vzdáleného probuzení Wake On LAN  

Do kategorie **Wake on LAN** se zobrazí následující sedm sestav.

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Všechny počítače cílené pro aktivitu funkce Wake On LAN**|Zadejte typ nasazení pro zobrazení seznamu počítačů, které jsou cílem aktivity Wake on LAN.|  
|**Všechny objekty s čekající aktivitou buzení**|Zobrazí objekty, pro které se naplánovalo buzení.|  
|**Všechny lokality s povolenou funkcí Wake On LAN**|Zobrazí seznam všech lokalit v hierarchii, ve kterých se povolila funkce Wake On LAN.|  
|**Chyby přijaté při odesílání paketů buzení ze spánku za definované období**|Zobrazí chyby přijaté v zadaném období při odesílání paketů buzení ze spánku do počítačů.|  
|**Historie aktivity funkce Wake On LAN**|Zobrazí historii aktivit buzení, ke kterým došlo za určité období.|  
|**Podrobnosti stavu nasazení proxy probuzení**|Zobrazí informace o stavu nasazení funkce proxy probuzení pro každé zařízení v zadané kolekci.|  
|**Přehled stavu nasazení proxy probuzení**|Zobrazí souhrnné informace o stavu nasazení funkce proxy probuzení v zadané kolekci.|  
