---
title: Úvod k Asset Intelligence
titleSuffix: Configuration Manager
description: Funkce Asset Intelligence v Configuration Manager slouží k inventarizaci a správě využití softwarových licencí v celém podniku.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714182"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Seznámení s funkcí Asset Intelligence v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Inventarizace a správa využití softwarových licencí v celém podniku pomocí katalogu Asset Intelligence. Funkce Asset Intelligence přidává třídy inventáře hardwaru pro zlepšení množství informací, které Configuration Manager shromažďuje. Tyto informace zahrnují názvy hardwaru a softwaru používané ve vašem prostředí. Tyto informace obsahují více než 60 sestav v snadno použitelném formátu. Mnohé z těchto sestav odkazují na další konkrétní sestavy. Dotaz na Obecné informace a podrobnější informace najdete v podrobnostech. 

Přidejte vlastní informace do katalogu Asset Intelligence. Například vlastní kategorie softwaru, rodiny softwaru, popisky softwaru a požadavky na hardware. Pokud chcete dynamicky aktualizovat katalog Asset Intelligence nejnovějšími dostupnými informacemi, připojte ho k Microsoft Cloud. 

Použijte funkci Asset Intelligence, která vám umožní sjednotit využití licenční licence k podnikovému softwaru. Importujte informace o softwarových licencích do databáze lokality Configuration Manager, abyste se mohli podívat na to, jaký software se používá.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a>Katalog Asset Intelligence  

Katalog Asset Intelligence je sada databázových tabulek uložených v databázi lokality. Tyto tabulky zahrnují kategorizaci a identifikační informace pro více než 300 000 softwarových titulů a verzí. Také vám pomůžou se správou požadavků na hardware pro konkrétní softwarové tituly.  

Funkce Asset Intelligence poskytuje informace o softwarových licencích pro používané softwarové tituly, a to jak z Microsoftu, tak ze softwaru jiného výrobce než Microsoftu. V katalogu Asset Intelligence je k dispozici předdefinovaná sada hardwarových požadavků pro softwarové tituly a můžete vytvořit nové informace o požadavcích na hardware definované uživatelem, aby splňovaly vlastní požadavky. Informace můžete přizpůsobit také v katalogu Asset Intelligence. informace o softwarových titulech můžete nahrát do cloudu Microsoftu ke kategorizaci.  

Aktualizace katalogu Asset Intelligence, které obsahují nově vydaný software, jsou k dispozici ke pravidelnému stahování, aby bylo možné provádět hromadné aktualizace katalogu. Dá se taky dynamicky aktualizovat pomocí bodu synchronizace katalogu Asset Intelligence.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a>Kategorie softwaru  

Kategorie softwaru funkce Asset Intelligence se používají pro rozsáhlou kategorizaci softwarových titulů v inventáři a jako skupiny na vysoké úrovni pro více konkrétních rodin softwaru. Kategorie softwaru může sdružovat třeba energetické společnosti a v rámci této kategorie softwaru může existovat rodina softwaru pro ropné a plynařské společnosti nebo vodní elektrárny. Katalog Asset Intelligence má předdefinované mnoho kategorií softwaru. Můžete vytvořit uživatelsky definované kategorie, které budou dále definovat software v inventáři. Stav ověření všech předdefinovaných kategorií softwaru je vždycky **ověřený**. Vlastní informace o kategorii softwaru přidané do katalogu Asset Intelligence jsou **definované uživatelem**. 

Další informace o správě kategorií softwaru najdete v tématu Konfigurace funkce [Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Předdefinované informace o kategorii softwaru uložené v katalogu Asset Intelligence jsou jen pro čtení. Nemůžete ho změnit ani odstranit. Uživatelé s právy pro správu můžou  uživatelsky definované kategorie softwaru přidávat, měnit nebo odstraňovat.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Rodiny softwaru  

Rodiny softwaru Asset Intelligence slouží k definování softwarových titulů v inventáři v rámci kategorií softwaru. V katalogu Asset Intelligence je předdefinovaný mnoho rodin softwaru. Můžete vytvořit uživatelsky definované kategorie, které budou dále definovat software v inventáři. Stav ověření všech předdefinovaných rodin softwaru je vždycky **ověřený**. Vlastní informace o rodině softwaru přidané do katalogu Asset Intelligence jsou **definované uživatelem**. 

Další informace o správě rodin softwaru najdete v tématu Konfigurace funkce [Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Předdefinované informace o rodině softwaru jsou jen pro čtení a nelze je změnit. Uživatelé s právy pro správu můžou uživatelsky definované rodiny softwaru přidávat, měnit nebo odstraňovat.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> Popisky softwaru  

Vlastní popisky softwaru pro funkci Asset Intelligence umožňují vytvářet filtry pro seskupování softwarových titulů a jejich zobrazení v sestavách Asset Intelligence. Pomocí popisků softwaru můžete vytvořit uživatelsky definované skupiny softwarových titulů, které sdílejí společný atribut. Můžete třeba vytvořit popisek softwaru s názvem shareware, přidružit ho k Sharewarem názvům v inventáři a spuštěním sestavy zobrazit všechny softwarové tituly s tímto popiskem. Neexistují žádné předdefinované popisky. Stav ověření popisků softwaru je vždycky nastavený na **Definovaný uživatelem**. 

Další informace o tom, jak spravovat štítky softwaru, najdete v tématu [Konfigurace funkce Asset Intelligence](configuring-asset-intelligence.md).  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Požadavky na hardware  

Informace o požadavcích na hardware vám umožní ověřit, jestli počítače splňují požadavky na hardware pro softwarové tituly před tím, než se cílí na nasazení softwaru. Spravujte požadavky na hardware pro softwarové tituly v pracovním prostoru **prostředky a kompatibilita** v uzlu **hardwarové požadavky** pod uzlem **funkce Asset Intelligence** . 

V katalogu Asset Intelligence je předdefinovaný mnoho požadavků na hardware. Vytvoří nové uživatelem definované informace o požadavcích na hardware, aby splňovaly vlastní požadavky. Stav ověření všech předdefinovaných požadavků na hardware je vždycky **ověřený**. Uživatelem definované informace o požadavcích na hardware přidaných do katalogu Asset Intelligence jsou **definované uživatelem**. 

Další informace o tom, jak spravovat požadavky na hardware, najdete v tématu [Konfigurace funkce Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Požadavky na hardware zobrazené v konzole Configuration Manager se načítají z katalogu Asset Intelligence. Nejsou založené na inventáři informací softwarového titulu od klientů. 
> 
> Informace o požadavcích na hardware se neaktualizují v rámci procesu synchronizace s Microsoftem. 
> 
> Můžete vytvořit uživatelem definované požadavky na hardware pro software v inventáři, který nemá přidružené hardwarové požadavky.  

Ve výchozím nastavení se pro každý uvedený hardwarový požadavek zobrazí tyto informace:  

- **Softwarový titul**: softwarový titul přidružený k hardwarovému požadavku  

- **Minimální procesor (MHz)**: minimální rychlost procesoru v MHz (MHz) požadovaná softwarovým titulem.  

- **Minimální velikost RAM (KB)**: minimální velikost paměti RAM v kilobajtech (KB) vyžadovaná softwarovým titulem  

- **Minimální místo na disku (KB)**: minimální volné místo na pevném disku v KB vyžadované softwarovým titulem  

- **Minimální velikost disku (KB)**: minimální velikost pevného disku v KB, kterou vyžaduje softwarový titul.  

- **Stav ověření**: stav ověření pro požadavek na hardware  

Předdefinované hardwarové požadavky uložené v katalogu Asset Intelligence jsou jen pro čtení a nejde je odstranit. Uživatelé s právy pro správu můžou přidat, upravit nebo odstranit uživatelem definované požadavky na hardware pro softwarové tituly, které nejsou uložené v katalogu Asset Intelligence.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a>Tituly softwaru v inventáři  

Pokud chcete zobrazit informace o softwarovém titulu v inventáři v konzole Configuration Manager, otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte uzel **funkce Asset Intelligence** a vyberte uzel **software v inventáři** . Agent pro inventář hardwaru shromažďuje informace o softwaru inventáře z Configuration Manager klientů na základě titulů softwaru uložených v katalogu Asset Intelligence.  

> [!Note]  
> Agent pro inventář hardwaru shromažďuje inventář na základě tříd generování sestav inventáře hardwaru Asset Intelligence, které povolíte. Další informace o tom, jak povolit třídy vytváření sestav, najdete v tématu [Konfigurace funkce Asset Intelligence](configuring-asset-intelligence.md).  

Ve výchozím nastavení se pro každý inventarizovaný softwarový titul zobrazí tyto informace:  

- **Name (název**): název softwarového titulu v inventáři  

- **Dodavatel**: název dodavatele, který vyvinul softwarový titul v inventáři.  

- **Version (verze**): verze produktu v inventáři softwarového titulu  

- **Kategorie**: kategorie softwaru, která je aktuálně přiřazená k softwarovému titulu v inventáři  

- **Rodina**: rodina softwaru, která je aktuálně přiřazená k softwarovému titulu v inventáři  

- **Popisek** [**1**, **2**a **3**]: vlastní popisky přidružené k softwarovému titulu. K inventarizovaným softwarovým titulům můžou být přiřazené až tři vlastní popisky.  

- **Count**(počet): počet Configuration Manager klientů, kteří mají softwarový titul v inventáři  

- **State (stav**): stav ověření pro softwarový titul v inventáři  

> [!NOTE]  
> Informace o kategorizaci pro software v inventáři můžete měnit pouze v lokalitě nejvyšší úrovně ve vaší hierarchii. Mezi tyto informace patří název produktu, dodavatel, kategorie softwaru a rodina softwaru. Když upravíte informace o kategorizaci předdefinovaného softwaru, stav ověření softwaru se změní z **Ověřeno** na **Definovaný uživatelem**.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a>Bod synchronizace katalogu Asset Intelligence  

Bod synchronizace katalogu Asset Intelligence je Configuration Manager role systému lokality. Slouží k připojení ke cloudu Microsoftu na portu TCP 443 pro správu aktualizací informací o dynamickém katalogu. Tuto roli webu nainstalujte jenom v lokalitě nejvyšší úrovně v hierarchii. Nakonfigurujte všechna přizpůsobení katalogu Asset Intelligence pomocí Configuration Manager konzoly připojené k lokalitě nejvyšší úrovně. 

Když nakonfigurujete všechny aktualizace v lokalitě nejvyšší úrovně, informace o katalogu se replikují do ostatních lokalit v hierarchii. Role lokality umožňuje požádat o synchronizaci katalogu na vyžádání s Microsoftem nebo naplánovat automatickou synchronizaci katalogu. Kromě stažení nových informací katalogu může bod synchronizace katalogu Asset Intelligence odeslat do Microsoftu vlastní informace o softwarových titulech ke kategorizaci. Microsoft zpracovává všechny nahrané softwarové tituly jako veřejné informace. Ujistěte se, že vlastní softwarové tituly neobsahují důvěrné nebo proprietární informace.  

Po odeslání Nezařazeno do kategorie softwarového titulu ho Microsoft nekontroluje, dokud neexistují nejméně čtyři požadavky na kategorizaci od zákazníků na stejný softwarový titul. Výzkumní pracovníci Microsoftu pak identifikují, kategorizují a zpřístupní informace o kategorizaci softwarových titulů všem zákazníkům, kteří používají online službu. Nejvyšší priorita se přikládá softwarovým titulům, které mají nejvíce požadavků na kategorizaci. Vlastní software a obchodní aplikace pravděpodobně nezískají kategorii. Neodesílat tyto softwarové tituly Microsoftu ke kategorizaci.  

Bod synchronizace katalogu Asset Intelligence se vyžaduje pro připojení ke cloudu Microsoftu. Informace o tom, jak nainstalovat roli, najdete v tématu [Konfigurace funkce Asset Intelligence](configuring-asset-intelligence.md).  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a>Domovská stránka funkce Asset Intelligence  

Uzel **funkce Asset Intelligence** v pracovním prostoru **prostředky a kompatibilita** je Domovská stránka funkce Asset Intelligence v Configuration Manager. Tato domovská stránka obsahuje souhrnné zobrazení řídicího panelu pro informace katalogu Asset Intelligence.  

> [!NOTE]  
> Po zobrazení se Domovská stránka **funkce Asset Intelligence** automaticky neaktualizuje.  

**Funkce Asset Intelligence** Domovská stránka obsahuje následující oddíly:  

- **Synchronizace katalogu**: informace o tom, jestli je funkce Asset Intelligence povolená a aktuální stav bodu synchronizace katalogu Asset Intelligence.  

    > [!NOTE]  
    > Stránka domů zobrazí tuto část pouze při instalaci bodu synchronizace katalogu Asset Intelligence.  

    V této části najdete taky tyto informace:  

    - Plán synchronizace  

    - Pokud jste importovali licenční prohlášení zákazníka   

    - Poslední aktualizace stavu  

    - Čas příští plánované aktualizace  

    - Počet změn po instalaci bodu synchronizace katalogu Asset Intelligence   

- **Stav softwaru v inventáři**: počet a procento softwaru v inventáři, kategorie softwaru a rodin softwaru identifikovaných společností Microsoft, které identifikoval správce, čeká na vyřízení online nebo neidentifikováno a nečeká na vyřízení. Informace zobrazené v tabulkovém formátu udávají počty v jednotlivých skupinách, zatímco informace v grafu znázorňují příslušná procenta.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Sestavy funkce Asset Intelligence  

Sestavy funkce Asset Intelligence jsou umístěné v konzole Configuration Manager v pracovním prostoru **sledování** ve složce **Asset Intelligence** v uzlu **vytváření sestav** . Tyto sestavy poskytují informace o hardwaru, správě licencí a softwaru. Další informace o sestavách v Configuration Manager najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> Přesnost množství nainstalovaných softwarových titulů a licencí zobrazených v sestavách Asset Intelligence se může lišit od skutečného počtu nainstalovaných softwarových titulů nebo licencí používaných v daném prostředí. Případný rozdíl je způsobený složitými závislostmi a omezeními při inventarizaci informací o softwarových licencích pro softwarové tituly, které jsou nainstalované v podnikovém prostředí. Nepoužívejte sestavy funkce Asset Intelligence jako jediný zdroj pro stanovení dodržování předpisů pro zakoupené licence softwaru.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a>Sestavy hardwaru  

Hardwarové sestavy Asset Intelligence poskytují informace o hardwarových prostředcích v organizaci. Pomocí informací o inventáři hardwaru, jako je rychlost, paměť a periferní zařízení, mohou sestavy hardwaru funkce Asset Intelligence prezentovat informace o zařízeních USB, hardwaru, který se musí upgradovat, a dokonce i o počítačích, které nejsou připravené na konkrétní upgrade softwaru.  

> [!NOTE]  
> Některá uživatelská data v sestavách hardwaru Asset Intelligence se shromažďují z protokolu událostí zabezpečení systému Windows. Pro lepší přesnost sestav vymažte tento protokol, když znovu přiřadíte počítač novému uživateli.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a>Sestavy správy licencí  

Sestavy správy licencí Asset Intelligence poskytují údaje o licencích, které se používají. Sestava **Hlavní kniha licencí** obsahuje seznam nainstalovaných aplikací od společnosti Microsoft ve formátu od Microsoftu pomocí licenčního prohlášení společnosti Microsoft (MLS). Tento formát poskytuje pohodlný způsob, jak získat licence získané s použitím licencí. Další sestavy správy licencí poskytují informace o počítačích působících jako servery, na kterých je spuštěna služba správy klíčů (KMS) pro statistiku aktivace Windows.  

> [!IMPORTANT]  
> Některé sestavy správy licencí Asset Intelligence obsahují informace o funkci služby správy klíčů (KMS), způsob správy multilicencí. Pokud jste server služby správy klíčů neimplementovali, některé sestavy nemusí vracet žádná data.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a>Sestavy softwaru  

Sestavy softwaru Asset Intelligence poskytují informace o rodinách softwaru, kategoriích a konkrétních softwarových titulech, které jsou nainstalované na počítačích v organizaci. Sestavy softwaru obsahují informace, jako jsou objekty pomocníka prohlížeče a software, který se spouští automaticky. Tyto sestavy se dají použít k identifikaci adwaru, spywaru a dalšího malwaru. Můžete je také použít k identifikaci redundance softwaru, aby bylo možné zjednodušit získání a podporu softwaru.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a>Sestavy identifikačních softwarových značek  

Sestavy identifikačních softwarových značek Asset Intelligence poskytují informace o softwaru, který obsahuje identifikační softwarovou značku kompatibilní se standardem ISO/IEC 19770-2. Identifikační značky softwaru poskytují autoritativní informace používané k identifikaci nainstalovaného softwaru. Když povolíte třídu generování sestav inventáře hardwaru **SMS_SoftwareTag** , Configuration Manager shromáždí informace o softwaru s identifikačními softwarovými značkami. 

Informace o softwaru poskytují tyto sestavy:  

- **Software 14A-hledat software s povolenou identifikační softwarovou značkou**: počet nainstalovaných softwarů s povolenou identifikační softwarovou značkou  

- **14B-počítače s nainstalovaným určitým softwarem s povolenou identifikační softwarovou značkou**: všechny počítače, které mají nainstalovaný software s povolenou konkrétní identifikační softwarovou značkou  

- **Softwarový 14c – software s povolenou identifikační softwarovou značkou nainstalovaný na určitém počítači**: veškerý nainstalovaný software s konkrétní identifikační softwarovou značkou povolenou v určitém počítači  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a>Omezení generování sestav  

Sestavy funkce Asset Intelligence můžou poskytovat velké množství informací o nainstalovaných softwarových titulech a zakoupených softwarových licencí. Tyto informace nepoužívejte jako jediný zdroj pro určení dodržování předpisů softwarových licencí.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Příklady závislosti  
Přesnost množství zobrazeného v sestavách Asset Intelligence pro nainstalované softwarové tituly a informace o licencích se může lišit od aktuálně používaných částek. Případný rozdíl je způsobený složitými závislostmi při inventarizaci informací o softwarových licencích pro softwarové tituly, které se využívají v podnikovém prostředí. Následující příklady znázorňují závislosti při inventarizaci nainstalovaného softwaru v podniku pomocí funkce Asset Intelligence, které by mohly ovlivnit přesnost sestav Asset Intelligence:  

- **Závislosti inventáře hardwaru klienta**: sestavy nainstalovaných softwarových funkcí Asset Intelligence jsou založené na datech shromážděných z Configuration Manager klientů rozšířením inventáře hardwaru, aby bylo možné vytvářet zprávy katalogu Asset Intelligence. Vzhledem k této závislosti na generování sestav inventáře hardwaru odrážejí sestavy funkce Asset Intelligence data jenom od klientů, kteří úspěšně dokončí procesy inventáře hardwaru s povolenými třídami generování sestav WMI funkce Asset Intelligence. Vzhledem k tomu, že Configuration Manager klienti provádějí procesy inventáře hardwaru podle plánu definovaného správcem, může dojít k prodlevě při generování sestav dat, která mají vliv na přesnost sestav Asset Intelligence. 

    Může se třeba stát, že se inventarizovaný licencovaný softwarový titul odinstaluje potom, co klient dokončí úspěšný cyklus inventarizace hardwaru. V sestavách Asset Intelligence se zobrazí softwarový titul, který se bude instalovat až do příštího plánovaného cyklu generování sestav inventáře hardwaru klienta.  

- **Závislosti balíčků softwaru**: sestavy funkce Asset Intelligence jsou založené na nainstalovaných datech softwarového titulu shromážděných pomocí standardních Configuration Manager procesů inventáře hardwaru klienta. Některá data softwarového titulu se nemusí shromažďovat správně. Příklady, které by mohly způsobit nepřesné vytváření sestav funkce Asset Intelligence:  

    - Instalace softwaru, které nevyhovují standardním instalačním procesům  

    - Instalace softwaru, které byly změněny před instalací   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Právní omezení  
Informace zobrazené v sestavách Asset Intelligence podléhají mnoha omezením. Informace, které se v nich zobrazují, nepředstavují právní, účetní nebo jiné odborné poradenství. Informace poskytované sestavami Asset Intelligence jsou pouze pro informace. Nepoužívejte ji jako jediný zdroj informací pro určení dodržování předpisů při využívání softwarových licencí.  

Následující omezení jsou příklady použití funkce Asset Intelligence, které mohou ovlivnit přesnost sestav:  

- **Omezení počtu využití licencí společnosti Microsoft**:  

    - Počet získaných licencí na software společnosti Microsoft je založený na informacích, které správci dodávají. Pečlivě ho zkontrolujte, abyste se ujistili, že je k dispozici správný počet licencí softwaru.  

    - Nahlášený počet softwarových licencí Microsoftu obsahuje informace jenom o softwarových licencích Microsoftu získaných prostřednictvím multilicenčních programů. Neodráží informace o softwarových licencích získaných prostřednictvím maloobchodních, OEM nebo jiných prodejních kanálů o softwarových licencích.  

    - Softwarové licence získané za posledních 45 dnů se nemusí do počtu nahlášených softwarových licencí Microsoftu zahrnout, a to kvůli plánům a požadavkům generování sestav prodejců softwaru.  

    - V počtech softwarových licencí Microsoftu se taky nemusí odrážet převody softwarových licencí z důvodů fúze nebo akvizice společností.  

    - Nestandardní podmínky a ujednání v rámci smlouvy Microsoft Volume Licensing (MVLS) můžou ovlivnit počet nahlášených softwarových licencí. Mohou vyžadovat dodatečnou kontrolu zástupcem společnosti Microsoft.  

- **Omezení počtu nainstalovaných softwarových titulů**: Configuration Manager klienti musí úspěšně dokončit cykly generování sestav inventáře hardwaru, aby sestavy Asset Intelligence přesně hlásily počet nainstalovaných softwarových titulů. Po úspěšném cyklu generování sestav inventáře hardwaru může docházet k prodlevě mezi instalací nebo odinstalací licencovaného softwarového titulu. Tato akce se nemusí projevit v sestavách Asset Intelligence spuštěných dřív, než klient ohlásí svůj další naplánovaný inventář hardwaru.  

- **Omezení odsouhlasení licencí**: odsouhlasení počtu nainstalovaných softwarových titulů na základě počtu zakoupených softwarových licencí se počítá pomocí porovnání počtu licencí zadaného správcem a množství nainstalovaných softwarových titulů shromážděných z Configuration Manager inventáře hardwaru klienta na základě plánu nastaveného správcem. Toto porovnání nepředstavuje konečné závěry licencí od Microsoftu. Skutečný stav licencí závisí na konkrétních licencích na softwarové tituly a právy k používání, která udělují licenční podmínky.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a>Stavy ověření funkce Asset Intelligence  

Stavy ověření funkce Asset Intelligence reprezentují zdroj a aktuální stav ověření informací katalogu Asset Intelligence. V následující tabulce jsou uvedené možné stavy ověření funkce Asset Intelligence a akce správce, které je můžou způsobit.  

| Stav | Definice | Akce správce | Poznámka |  
|---------------|--------------------|------------------------------|-----------------|  
|**Ověřeno**|Microsoft výzkumníki definovali položku katalogu|Žádná|Nejlepší stav|  
|**Definováno uživatelem**|Výzkumníki Microsoftu nedefinovali položku katalogu.|Přizpůsobení informací místního katalogu|Tento stav se zobrazuje v sestavách Asset Intelligence.|  
|**Čeká na vyřízení**|Výzkumníki Microsoftu nedefinovali položku katalogu, ale tuto položku odeslali Microsoftu ke kategorizaci.|Žádná další akce po požadavku na kategorizaci|Položka katalogu zůstane v tomto stavu, dokud do kategorie výzkumníků Microsoftu nepatří položka a synchronizujete svůj katalog Asset Intelligence.|  
|**Aktualizovatelné**|Uživatelem definovaná položka katalogu byla při synchronizaci katalogu odlišná od Microsoftu.|Pomocí akce **vyřešit konflikt** můžete rozhodnout, jestli chcete použít nové informace o kategorizaci nebo předchozí uživatelem definovanou hodnotu. Další informace o řešení konfliktů najdete v tématu [operace pro funkci Asset Intelligence](operations-for-asset-intelligence.md).|Po vyřešení konfliktu kategorizace se položka nebude ověřovat jako kolidující, pokud později aktualizace kategorizace nezavádějí nové informace o položce.|  
|**Nezařazeno do kategorie**|Položka katalogu nebyla definována výzkumnými pracovníky Microsoftu, položka nebyla odeslána společnosti Microsoft ke kategorizaci a správce nemá přiřazenou hodnotu kategorizace definovanou uživatelem.|Vyžádejte si kategorizaci nebo upravte informace místního katalogu. Další informace najdete v tématu [operace pro funkci Asset Intelligence](operations-for-asset-intelligence.md).|Žádná|  

> [!NOTE]  
> Položky katalogu, které odesíláte do Microsoftu ke kategorizaci, mají stav ověření **čeká** na lokalitu centrální správy, ale v podřízených primárních lokalitách budou nadále zobrazovat stav ověření **Nezařazeno do kategorie** .  

Příklady, kdy může být stav ověřování převeden z jednoho stavu do jiného, najdete v tématu [Příklady přechodů stavu ověření pro funkci Asset Intelligence](example-validation-state-transitions-for-asset-intelligence.md).  
