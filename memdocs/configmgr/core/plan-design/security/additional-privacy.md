---
title: Další informace o ochraně osobních údajů
titleSuffix: Configuration Manager
description: Přečtěte si, jak společnost Microsoft shromažďuje a používá data z Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6891a46050bb83e54fb34b97d9129fcb5873785
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718669"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Další informace o ochraně osobních údajů pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Aktualizace a údržba

Configuration Manager používá model aktualizace, který pomáhá udržet aktuální prostředí s nejnovějšími aktualizacemi a funkcemi. Tato funkce používá roli systému lokality nazývanou bod připojení služby. Vyberte server, na který se má tato role nainstalovat. 

Další informace o shromažďovaných informacích a způsobu jejich použití najdete v tématu [data o využití](#usage-data).



## <a name="usage-data"></a>Údaje o využití

Configuration Manager shromažďuje data o využití a diagnostiku o sobě, což Microsoft využívá ke zlepšení prostředí pro instalaci, kvality a zabezpečení budoucích verzí.
Data o využití a diagnostika jsou povolená pro každou hierarchii Configuration Manager. Skládá se z SQL Server dotazů, které se spouští každý týden v každé primární lokalitě a v lokalitě centrální správy. Používá-li hierarchie lokalitu centrální správy, data z primárních lokalit se poté replikují do této lokality. V lokalitě nejvyšší úrovně v hierarchii spojovací bod služby odesílá tyto informace při kontrole aktualizací. Pokud je spojovací bod služby v režimu offline, informace se přenesou pomocí nástroje pro připojení služby.

Configuration Manager shromažďuje data pouze z databáze SQL serveru lokality a neshromažďuje data přímo z klientů nebo serverů lokality.

Správci mohou změnit úroveň shromažďovaných dat, a to tak, že v konzole Configuration Manager v části **data o využití** budou.

Další informace o úrovních a nastavení dat o využití najdete v tématu [Diagnostika a data o využití](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Konektor Log Analytics

Konektor Log Analytics synchronizuje data, jako jsou kolekce, od Configuration Manager až po cloudovou službu Azure. ID a tajný klíč předplatného Azure jsou uložené v databázi Configuration Manager, když správce tuto funkci nakonfiguruje. Azure Active Directory tajný klíč klienta i sdílený klíč v pracovním prostoru Azure jsou uložené v místní databázi Configuration Manager. Veškerá komunikace mezi Configuration Manager a Azure používá protokol HTTPS. Společnosti Microsoft neposkytují žádné další informace o kolekcích mimo náhodné diagnostiky a data o využití. 

Další informace o informacích, které Log Analytics shromažďuje, najdete v tématu [zabezpečení dat Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Funkce Asset Intelligence

Funkce Asset Intelligence umožňuje správcům definovat, sledovat a aktivně spravovat shodu s normami konfigurace. Měření a zprávy o nasazení a používání fyzických i virtuálních aplikací pomáhá organizacím provádět lepší obchodní rozhodnutí o licencování softwaru a udržovat kompatibilitu s licenčními smlouvami. Po shromáždění dat o využití od klientů Configuration Manager můžete pomocí různých funkcí zobrazit data, včetně kolekcí, dotazů a sestav.

Při každé synchronizaci se od Microsoftu stáhne katalog známého softwaru. Můžete se rozhodnout odeslat Microsoftu informace o Nezařazeno do kategorie softwarových titulech, které jsou zjištěné v rámci vaší organizace, aby je bylo možné znovu vyhledat a přidat do katalogu. Před odesláním těchto informací zobrazí dialogové okno data, která budou odeslána. Nahraná data se nedají odvolat. Funkce Asset Intelligence neodesílá informace o uživatelích a počítačích nebo používání licencí společnosti Microsoft.

Po odeslání softwarového titulu výzkumníci Microsoftu označí, roztřídí a poté zpřístupní dané znalosti všem ostatním zákazníkům, kteří tuto funkci používají, a dalším spotřebitelům katalogu. Veškerý nahraný softwarový titul se bude stát veřejným. Aplikace a její kategorizace se stanou součástí katalogu a pak je můžete stáhnout do dalších uživatelů katalogu. Než nakonfigurujete shromažďování dat funkce Asset Intelligence a rozhodnete, zda budete odesílat informace společnosti Microsoft, zvažte požadavky vaší organizace na ochranu osobních údajů.

Ve výchozím nastavení není funkce Asset Intelligence ve Configuration Manager povolený. Nahrávání Nezařazeno do kategoriech titulů se nikdy neprovádí automaticky a systém není navržený pro automatizaci této úlohy. Je třeba ručně vybrat a ověřit odeslání každého softwarového titulu.



## <a name="endpoint-protection"></a>Funkce Endpoint Protection

Služba Microsoft Cloud Protection se dřív jmenovala jako služba Microsoft Active Protection Service nebo MAPS.

Příslušné produkty jsou nástroje System Center Endpoint Protection a funkce Endpoint Protection Configuration Manager (pro správu nástroje System Center Endpoint Protection a programu Windows Defender pro Windows 10). Tato funkce není implementována pro System Center Endpoint Protection pro Linux nebo System Center Endpoint Protection for Mac.

Antimalwarová Komunita služby Microsoft Cloud Protection je nedobrovolný celosvětový online komunitní komunita, která zahrnuje uživatele nástroje System Center Endpoint Protection. Když se připojíte ke službě Microsoft Cloud Protection Service, služba System Center Endpoint Protection automaticky odesílá informace společnosti Microsoft. Společnost Microsoft používá tyto informace k určení softwaru pro účely šetření potenciálních hrozeb a ke zlepšení efektivity Endpoint Protection System Center. Tato komunita pomáhá zastavit šíření nových škodlivých softwarových infekcí. Pokud zpráva služby Microsoft Cloud Protection obsahuje podrobnosti o malwaru nebo potenciálně nežádoucím softwaru, které může klient Endpoint Protection odebrat, Microsoft Cloud služba ochrany stáhne nejnovější podpis, který je vyřeší. Služba Microsoft Cloud Protection může také najít falešně pozitivní a opravit je. (Falešně pozitivní je, že se něco původně identifikovaného jako malware nestane.) 

Sestavy služby Microsoft Cloud Protection obsahují informace o možných souborech malwaru, jako jsou názvy souborů, kryptografická hodnota hash, dodavatel, velikost a časová razítka. Kromě toho může služba Microsoft Cloud Protection shromažďovat úplné adresy URL, které označují původ souboru. Tyto adresy URL mohou občas obsahovat osobní údaje, jako jsou hledané výrazy nebo data zadaná ve formulářích. Zprávy také mohou zahrnovat akce, které jste provedli, když Endpoint Protection upozorněni na nežádoucí software. Sestavy služby Microsoft Cloud Protection obsahují tyto informace, které Microsoftu pomohou posoudit, jak efektivně Endpoint Protection může detekovat a odebírat malware a potenciálně nežádoucí software a pokusit se identifikovat nový malware.

Pokud máte základní nebo pokročilé členství, můžete se připojit ke službě Microsoft Cloud Protection. Základní sestavy členů obsahují informace popsané dříve. Sestavy rozšířených členů jsou komplexnější a mohou zahrnovat další podrobnosti o softwaru, který Endpoint Protection detekuje, jako je umístění takového softwaru, názvy souborů, jak software funguje a jak ovlivnil počítač. Tyto sestavy a sestavy od dalších Endpoint Protectionch uživatelů, kteří se účastní služby Microsoft Cloud Protection, pomohou pracovníkům Microsoftu rychleji zjišťovat nové hrozby. Pro programy, které splňují kritéria analýzy, jsou pak vytvořeny definice malwaru a aktualizované definice jsou zpřístupněny všem uživatelům prostřednictvím Microsoft Update.

Aby bylo možné zjistit a opravit určité druhy infekcí malwaru, produkt pravidelně odesílá informace o stavu zabezpečení vašeho počítače do služby Microsoft Cloud Protection. Tyto informace obsahují informace o nastavení zabezpečení počítače a souborech protokolů, které popisují ovladače a další software, který se při spuštění počítače načítají.

Pošle se také číslo, které jedinečně identifikuje váš počítač. Kromě toho může služba Microsoft Cloud Protection shromažďovat IP adresy, ke kterým se potenciální malwarové soubory připojují.

Sestavy služby Microsoft Cloud Protection se používají ke zlepšení softwaru a služeb společnosti Microsoft. Sestavy mohou být také použity pro statistické nebo jiné testování nebo analytické účely a pro generování definicí. K nim mají přístup jenom zaměstnanci, dodavatelé, partneři a dodavatelé Microsoftu, kteří potřebují používat sestavy.

Služba Microsoft Cloud Protection záměrně neshromažďuje osobní údaje. Pokud služba Microsoft Cloud Protection shromažďuje nějaké osobní údaje, společnost Microsoft je nepoužívá k vaší identifikaci nebo kontaktování vaší osoby.

Další informace najdete v tématu [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarchie webu – Zeměpisné zobrazení na mapách Bing Maps

V konzole Configuration Manager přejděte do pracovního prostoru **monitorování** , vyberte uzel **hierarchie lokality** a přepněte do **geografického zobrazení**. Toto zobrazení vám umožní používat mapy, které Microsoft Bing Maps poskytuje k zobrazení Configuration Manager topologie fyzického serveru. Chcete-li povolit tuto funkci, informace o umístění, které poskytnete, budou odesílány z vašeho serveru do webové služby Bing Maps.

Společnost Microsoft používá informace pro provoz a zlepšování služby Microsoft Bing Maps a dalších webových stránek a služeb společnosti Microsoft. Další informace najdete v tématu [prohlášení o zásadách ochrany osobních údajů společnosti Microsoft](https://go.microsoft.com/fwlink/?LinkId=823548).

Lze zvolit nepoužívání zeměpisného zobrazení hierarchie webu. Výchozí zobrazení diagramu hierarchie vám umožní zobrazit hierarchii a nepoužívá službu Bing Maps.
