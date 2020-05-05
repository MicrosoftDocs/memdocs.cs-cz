---
title: Reference k uživatelskému rozhraní Support Center
titleSuffix: Configuration Manager
description: Naučte se používat nástroje Support Center.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43bb35243b4f7e7b1e45b66319efd4ec21e92542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718613"
---
# <a name="support-center-user-interface-reference"></a>Reference k uživatelskému rozhraní Support Center

*Platí pro: Configuration Manager (Current Branch)*

Tento článek je referenční informace popisující uživatelská rozhraní (UI) nástrojů nástroje Support Center:
- Support Center
- Prohlížeč protokolů Support Center
- Support Center Viewer



## <a name="support-center-reference"></a>Reference k nástroji Support Center

Tato část popisuje uživatelské rozhraní nástroje **Support Center** . 
- [Nabídka okno](#bkmk_support-window)  
- [Karta Domů](#bkmk_support-home)  
- [Karta klient](#bkmk_support-client)  
- [Karta Zásady](#bkmk_support-policy)  
- [Karta obsah](#bkmk_support-content)  
- [Karta inventář](#bkmk_support-inventory)  
- [Karta Poradce při potížích](#bkmk_support-troubleshoot)  
- [Karta protokoly](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a>Nabídka okno

V levém horním rohu okna nástroje Support Center otevřete tuto nabídku tak, že vyberete šipku v modrém poli.

#### <a name="local-machine-connection"></a>Připojení k místnímu počítači
Support Center shromažďuje soubory protokolů a provádí řešení potíží na klientovi, na kterém je spuštěný nástroj Support Center.

#### <a name="remote-connection"></a>Vzdálené připojení
Navažte vzdálené připojení k jinému Configuration Manager klientovi. Po připojení nástroj Support Center shromáždí soubory protokolů a provede řešení potíží s klientem, ke kterému je připojený.

#### <a name="about"></a>Informace
Poskytuje informace o nástroji Support Center.

#### <a name="options"></a>Možnosti
V dialogovém okně **Možnosti** můžete:
- Snížit pohyb animovaných prvků uživatelského rozhraní  
- Změna výchozího umístění pro uložení souborů datových sad  
- Změna umístění dočasných souborů    
- Resetovat upozornění. Všechny varovné zprávy, které jste předtím potlačili, se po aktivaci zobrazí znovu.  
- Obnovte dočasnou cestu k souboru na výchozí hodnotu.`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Ukončit
Zavřete Support Center.



### <a name="home-tab"></a><a name="bkmk_support-home"></a>Karta Domů

#### <a name="collect-selected-data"></a>Shromáždit vybraná data
Support Center shromažďuje informace z klienta Configuration Manager. Ve výchozím nastavení shromažďuje následující typy:
- Soubory protokolů
- Kolektor konfigurace klienta
- Operační systém

Chcete-li shromáždit jiné typy informací, zaškrtněte políčko vedle názvu tohoto typu.

Vyberte rozevírací seznam v dolní části tlačítka **shromáždit vybraná data** na pásu karet a vyberte možnost **shromáždit všechna data**. Tato akce shromáždí kompletní sadu dat o stavu klienta.

I když Support Center shromažďuje data, vyberte **Zrušit shromažďování** a zastavte ji.

#### <a name="data-types"></a>Typy dat
Když zaškrtnete políčko u možnosti, Support Center shromáždí tento typ dat při příštím výběru **shromažďovat vybraná data**. K dispozici jsou následující typy:  

- **Soubory protokolu**: soubory protokolů klienta včetně protokolů instalace  

- **Zásady**: kolekce zásad klienta  

- **Certifikáty**: informace o veřejném klíči pro klientské certifikáty. Support Center neshromažďuje privátní klíče certifikátu.  

- **Kolektor konfigurace klienta**: Configuration Manager informace o klientovi. Tento datový typ nemůžete zakázat.  

- **Registr klienta**: shromažďuje informace o konfiguraci klienta z registru. Support Center shromažďuje jenom informace o Configuration Manager registru.  

- **WMI klienta**: informace o konfiguraci klienta z rozhraní WMI. Support Center neshromažďuje zásady klienta.  

- **Řešení potíží**: data pro řešení potíží v reálném čase, která vám pomůžou diagnostikovat běžné problémy klienta se službou Active Directory, body správy, sítí, přiřazením zásad a registrací.  

    > [!NOTE]  
    > Tento datový typ není podporovaný, když vytváříte vzdálené připojení k jinému klientovi.  

- **Výpisy ladění**: Proveďte ladění výpisu ladění klienta a souvisejících procesů. Výpisy ladění můžou být velké. Tuto možnost povolte jenom v případě, že chcete řešit problémy s výkonem klienta.  

    > [!WARNING]  
    > Shromažďování výpisů ladění způsobí, že se datové sady stanou velmi velké (v některých případech několik set MB).  
    >  
    > Výpisy ladění obsahují možné citlivé informace, včetně hesel, kryptografických tajných klíčů nebo uživatelských dat. Výpisy ladění by se měly shromažďovat jenom na doporučeních podpora Microsoftu personál. Sady dat, které obsahují výpisy ladění, by se měly pečlivě zpracovat, aby se chránily před neoprávněným přístupem.  
    >  
    > Tento datový typ není podporovaný, když vytváříte vzdálené připojení k jinému klientovi.  

- **Operační systém**: shromáždí informace o konfiguraci místního počítače. Tato data obsahují informace o instalaci Windows, síťových adaptérech a konfiguraci systémové služby. Tento datový typ nemůžete zakázat.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a>Karta klient

#### <a name="load-or-refresh"></a>Načíst nebo aktualizovat
Support Center načte nebo aktualizuje podrobnosti pro klienta Configuration Manager.

#### <a name="control-client-agent-service"></a>Řízení služby agenta klienta
Proveďte jednu z následujících akcí na Configuration Manager službě agenta klienta (Ccmexec) na připojeném klientovi:  

- **Restartovat klienta**  

    > [!IMPORTANT]  
    > Pokud se služba agenta klienta úspěšně nerestartuje, nebude možné spravovat klienta Configuration Manager až do chvíle, kdy se služba spustí.  

- **Spustit klienta**  

- **Zastavit klienta**  

    > [!IMPORTANT]  
    > Klienta nelze spravovat pomocí Configuration Manager, dokud se služba nespustí.  

#### <a name="properties"></a>Vlastnosti
Když načtete podrobnosti o klientovi, Support Center zobrazí následující vlastnosti:  

- **ID klienta**: jedinečný identifikátor, který Configuration Manager k identifikaci klienta používat.  

- **ID hardwaru**: jedinečný identifikátor, který Configuration Manager používá k identifikaci hardwaru klienta  

- **Schváleno**: označuje, zda je klient schválen v Configuration Manager  

- **Stav registrace**: udává, jestli je klient zaregistrovaný ve službě Configuration Manager  

- **Internetové**: označuje, jestli je klient na internetu.  

- **Version (verze**): číslo verze nainstalovaného klienta Configuration Manager  

- **Kód lokality**: kód lokality pro primární lokalitu, ke které je klient přiřazen.  

- **Přiřazený MP**: plně kvalifikovaný název domény (FQDN) aktuálně přiřazeného bodu správy klienta  

- **Rezidentní MP**: plně kvalifikovaný název domény rezidentního bodu správy  

- **Proxy MP**: název hostitele nebo plně kvalifikovaný název domény bodu správy proxy serveru (pokud existuje)  

- **Kód proxy serveru**: kód lokality pro sekundární lokalitu (pokud existuje)  

- **Stav proxy serveru**: stav bodu správy proxy serveru klienta Configuration Manager. Například **aktivní** nebo **čeká na vyřízení**.  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a>Karta Zásady

Místo staršího nástroje [PolicySpy](policy-spy.md) použijte akce na této kartě.

#### <a name="load-policy"></a>Načíst zásadu
Tato možnost se liší v závislosti na zobrazení:

- **Načíst vlastní zásadu**: ve skupině zobrazení vyberte **skutečnost** a pak tuto možnost vyberte ve skupině zásad. Support Center načte zásadu klienta, kterou jste právě vybrali.  

- **Načíst požadovanou zásadu**: ve skupině zobrazení vyberte **požadované** a pak tuto možnost vyberte ve skupině zásad. Support Center načte zásadu klienta požadovanou klientem.  

- **Načíst výchozí zásadu**: ve skupině zobrazení vyberte **výchozí** a potom tuto možnost vyberte ve skupině zásad. Support Center načte výchozí zásady pro tohoto klienta.  

Kliknutím na rozevírací seznam v dolní části tohoto tlačítka můžete zobrazit další možnosti:

- **Načíst nebo aktualizovat vše**: současně načítá nebo aktualizuje skutečné, požadované a výchozí zásady.  

#### <a name="actual-view"></a>Skutečné zobrazení
Otevře aktuální zobrazení zásad.

#### <a name="requested-view"></a>Požadované zobrazení
Otevře požadované zobrazení zásad.

#### <a name="default-view"></a>Výchozí zobrazení
Otevře zobrazení výchozí zásady. (Tato zásada zařízení získá při instalaci klienta Configuration Manager.)

#### <a name="request-and-evaluate-policy"></a>Vyžádat a vyhodnotit zásady
Support Center si vyžádá zásadu klienta z bodu správy a pak tuto zásadu na straně klienta vyhodnotí.

Kliknutím na rozevírací seznam v dolní části tohoto tlačítka můžete zobrazit další možnosti:  

- **Zásada žádosti**: Support Center požaduje zásadu klienta z bodu správy.  

- **Vyhodnotit zásady**: Support Center vyhodnotí zásadu klienta na klientovi.  

- **Resetovat zásadu na výchozí**: Support Center oznamuje klientovi Configuration Manager, že má znovu použít výchozí zásady. Odebere všechny zásady počítače a uživatele v klientovi.  

#### <a name="listen-for-policy-events"></a>Naslouchat událostem zásad
Support Center čeká na události zásad. Výběrem této možnosti znovu zakážete naslouchání událostem zásad. Pokud chcete zobrazit **události zásad**, vyberte šipku ve spodní části této karty. 

#### <a name="clear-events"></a>Vymazat události
Support Center vymaže všechny události zásad.



### <a name="content-tab"></a><a name="bkmk_support-content"></a>Karta obsah

Zobrazení obsahu v klientovi, včetně obsahu v mezipaměti. Sledujte průběh nasazení aktualizací softwaru a aplikací. 

#### <a name="load-or-refresh"></a>Načíst nebo aktualizovat
*Platí pro zobrazení obsahu a mezipaměti.*

Support Center načte nebo aktualizuje seznam obsahu, který je aktuálně na klientovi.

#### <a name="invoke-trigger"></a>Vyvolat Trigger
Následující položky v této nabídce vyžadují akci klienta související s obsahem:  

- **Umístění služeb**  

    - **Aktualizovat umístění obsahu**: aktualizuje distribuční body používané jakýmkoli stažením aktivního obsahu.  

    - **Aktualizovat body správy**: Aktualizuje interní seznam bodů správy používaných klientem.  

    - **Žádosti o obsah mimo časový limit**: Pokud některé požadavky na umístění obsahu běžely příliš dlouho, tato akce zastaví požadavek.  

- **Vyhodnocení nasazení aplikace**: spustí úlohu, která vyhodnotí nasazené aplikace.  

- **Vyhodnocení nasazení aktualizací softwaru**: spustí úlohu, která vyhodnotí nasazené aktualizace softwaru.  

- **Kontrola zdroje aktualizací softwaru**: spustí úlohu, která vyhledá umístění zdroje aktualizace.  

- **Aktualizace zdrojového seznamu Instalační služba systému Windows**: spustí úlohu, která aktualizuje umístění zdroje pro instalace Instalační služba systému Windows (MSI).  

#### <a name="content-view"></a>Zobrazení obsahu
Viz aplikace, balíčky a aktualizace, které jsou načteny na klientovi. Když vyberete aplikaci, balíček nebo aktualizaci, můžete zobrazit podrobnosti o tomto obsahu. U některých aplikací můžete provést také následující akce:  

- **Aktualizovat**: Obnoví zobrazení podrobností.  

- **Ověřit nebo stáhnout**: ověření, zda je aplikace k dispozici ke stažení  

- **Nainstalovat**: instalace aplikace  

- **Odinstalace**: Odinstalace aplikace  

#### <a name="cache-view"></a>Zobrazení mezipaměti
Zobrazení konfigurace mezipaměti klienta a podrobností o obsahu mezipaměti. Když připojíte nástroje Support Center k místnímu klientovi, certifikační autorita provede také následující akce:  

- Chcete-li změnit umístění mezipaměti, vyberte možnost **změnit** vedle pole **umístění mezipaměti** .  

- Chcete-li upravit velikost mezipaměti, vyberte možnost **změnit** vedle pole **Velikost mezipaměti** .  

- Pokud chcete vymazat mezipaměť klienta, vyberte **Vymazat** vedle pole **mezipaměť v poli použít** .  

Toto zobrazení ukazuje následující vlastnosti:  

- **Umístění**: umístění každé složky mezipaměti. Kliknutím na odkaz otevřete složku v Průzkumníku Windows.   
- **ID obsahu**  
- **ID mezipaměti**  
- **Velikost**  
- **Poslední odkaz**: Tato vlastnost je datum, kdy se klient naposledy četl nebo zapsal do této položky v mezipaměti.  

#### <a name="monitoring-view"></a>Zobrazení monitorování
Výběrem **monitorování** zobrazíte aktivní průběh nasazení aktualizace softwaru a aktualizací aplikace. Toto zobrazení ukazuje stavové zprávy, které jsou vyvolány ze zpráv WMI pro události aktualizací aplikace a softwaru.

V případě každé události zobrazuje zobrazení následující vlastnosti:  

- **Čas**: čas, kdy klient událost vyvolal  
- **Typ tématu**: typ stavové zprávy  
- **ID tématu**: ID zprávy o stavu, která se používá k mapování událostí v souborech protokolu  
- **Typ ID tématu: podtyp**zprávy o stavu  
- **ID stavu**: výsledek akce, kterou sledujete.  
- **Podrobnosti** a **data události**: Další informace o stavových zprávách zobrazených v tomto zobrazení. Podrobnosti o stavu můžou být někdy prázdné.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a>Karta inventář

#### <a name="load-or-refresh"></a>Načíst nebo aktualizovat
Support Center načte nebo aktualizuje seznam inventáře klientů pro aktuálně vybrané zobrazení.

#### <a name="invoke-trigger"></a>Vyvolat Trigger

> [!Note]  
> Pro jiné úlohy než **cyklus sestav měření softwaru**:  
> - Pokud si vyžádáte úlohu, když je již spuštěna jiná úloha inventáře, klient zařadí do fronty nový úkol, který se spustí po dokončení aktuální úlohy a dalších úloh ve frontě.  
> - Sledujte průběh úkolu v **InventoryAgent. log**.  

Následující položky v této nabídce žádají o akci klienta související s inventářem:  

- **Cyklus shromažďování dat zjišťování (prezenční signál)**: Aktivuje úlohu klienta, která se používá ke shromažďování informací o zjišťování zařízení.  

- **Cyklus sběru souborů**: Aktivuje úlohu klienta, která se používá ke shromažďování místních souborů.  

- **Cyklus inventáře hardwaru**: Aktivuje úlohu klienta, která se používá ke shromažďování dat inventáře hardwaru.  

- **Cyklus shromažďování IDMIF**: Aktivuje úlohu klienta, která se používá ke shromažďování dat IDMIF.  

- **Cyklus inventáře softwaru**: Aktivuje úlohu klienta, která se používá ke shromáždění dat inventáře softwaru.  

- **Cyklus sestavy měření softwaru**: Aktivuje úlohu klienta, která se používá k sestavení sestavy monitorování míry využívání softwaru, a odešle ji do bodu správy. Sledovat průběh této úlohy v **SWMTRReportGen. log**.

- **Odeslat neodeslané stavové zprávy ve frontě**: Aktivuje úlohu klienta, která vyprázdní frontu stavových zpráv.

- **Upřesnit**  
    - **Cyklus inventáře hardwaru (úplná opětovná synchronizace)**  
    - **Cyklus inventáře softwaru (úplná opětovná synchronizace)**  


#### <a name="views"></a>Zobrazení
Pokud funkce není povolená, zobrazení nezobrazí žádná data. 

- **Stav**: zobrazení sad dat inventáře, které klient shromáždil  

- **DDR**: informace o datech zjišťování klienta shromážděných z klienta  

- **HINV**: informace o datech inventáře hardwaru shromážděných z klienta  

- **SINV**: informace o datech inventáře softwaru shromážděných z klienta  

- **Shromažďování souborů**: informace o souborech shromažďovaných z klienta  

- **IDMIF**: informace o datech IDMIF a NOIDMIF shromažďovaných z klienta  

- **Měření**: informace o datech měření softwaru shromažďovaných z klienta  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a>Karta Poradce při potížích

Řešení některých nejběžnějších problémů s klienty Configuration Manager:  
- Problémy se službou Active Directory  
- Sítě Windows  
- Configuration Manager   
    - Body správy  
    - Přiřazení zásad  
    - Registrace  


> [!NOTE]  
> Tato karta není k dispozici, když se připojíte ke vzdálenému klientovi Configuration Manager.


#### <a name="start"></a>Spustit
Spustí řešení potíží s klientem.

- **Active Directory**: dotazy na službu Active Directory pro načtení informací o publikované Configuration Manager lokalitě  
- **MPCERTIFICATE**: načte certifikáty bodu správy.  
- **Opakované mplist**: Získá seznam bodů správy.  
- **MPKEYINFORMATION**: načte informace o kryptografickém klíči bodu správy.  
- **Sítě**: řešení problémů se sítí  
- **Přiřazení zásad**: načte přiřazení zásad.  
- **Registrace**: ověří, jestli je klient zaregistrovaný v lokalitě.  

#### <a name="view-selected-log"></a>Zobrazit vybraný protokol
Po výběru řádku na kartě Poradce při potížích vyberte tuto akci pro zobrazení souboru protokolu.

#### <a name="keep-previous-results"></a>Zachovat předchozí výsledky
Pokud vyřešíte potíže s klientem a pak chcete zkusit řešení potíží znovu, zvolte tuto možnost, chcete-li zachovat výsledky při prvním pokusu. V opačném případě Support Center přepíše předchozí soubory protokolu řešení potíží.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a>Karta protokoly

Tato část obsahuje seznam položek na kartě **Logs (protokoly** ) nástroje Support Center. 

Tato karta je skoro shodná s nástrojem **Prohlížeč protokolů** . Nástroj **Log Viewer** neobsahuje funkce **Konfigurovat protokolování klientů** a **skupiny protokolů** popsané v této části. V části referenční informace pro [Prohlížeč protokolů Support Center](#bkmk_log-viewer) najdete další možnosti, které jsou na této kartě k dispozici.

#### <a name="configure-client-logging"></a>Konfigurace protokolování klienta

Nastavte následující možnosti: 
- **Úroveň protokolu klienta**: podrobnosti protokolu a velikost souboru  
- **Maximální počet souborů**: povoluje více než jeden soubor protokolu daného typu.  
- **Maximální velikost souboru**: velikost souboru protokolu v bajtech, než klient vytvoří nový protokol.  

> [!NOTE]  
> Pokud nastavíte tyto hodnoty příliš nízké, klient nemusí protokolovat žádné užitečné informace. Pokud tyto hodnoty nastavíte příliš vysokou, můžou protokoly klienta spotřebovat velké objemy úložiště.  

#### <a name="log-groups"></a>Skupiny protokolů

Místo ručního výběru souborů protokolu pomocí tlačítka **otevřít protokoly** použijte tento rozevírací seznam k otevření všech souborů protokolu přidružených k následujícím oblastem funkcí: 
- **Správa požadované konfigurace**
- **Inventarizace**
- **Distribuce softwaru**
- **Aktualizace softwaru**
- **Správa aplikací**
- **Zásady**
- **Registrace klienta**
- **Nasazení operačního systému**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a>Odkaz na prohlížeč protokolů Support Center

Tato část popisuje uživatelské rozhraní nástroje **Support Center Log Viewer** . 

- [Nabídka okno](#bkmk_log-window)  
- [Karta Domů](#bkmk_log-home)  

Nástroj **Log Viewer** je skoro stejný jako karta **protokoly** nástroje **Support Center**. Nástroj **Log Viewer** neobsahuje možnosti **Konfigurace protokolování** a **skupin protokolů**klienta.


### <a name="window-menu"></a><a name="bkmk_log-window"></a>Nabídka okno

V levém horním rohu okna prohlížeče protokolů nástroje Support Center otevřete tuto nabídku tak, že vyberete šipku v modrém poli.

#### <a name="open-logs"></a>Otevřít protokoly
Přejděte do umístění souborů protokolu, které chcete otevřít. 

#### <a name="options"></a>Možnosti
V dialogovém okně **Možnosti** můžete:
- Snížit pohyb animovaných prvků uživatelského rozhraní  
- Registrovat prohlížeč protokolů jako výchozí aplikaci pro soubory protokolu s příponami. log a. lo_  
- Resetovat upozornění. Všechny varovné zprávy, které jste předtím potlačili, se po aktivaci zobrazí znovu.  

#### <a name="about"></a>Informace
Zobrazí informace o nástroji Support Center Log Viewer.

#### <a name="close"></a>Zavřít
Zavře prohlížeč protokolu Support Center.


### <a name="home-tab"></a><a name="bkmk_log-home"></a>Karta Domů

#### <a name="open-logs"></a>Otevřít protokoly 
Support Center vás vyzve k výběru jednoho nebo více souborů protokolu, které se mají otevřít.

V dolní části tlačítka **otevřít protokoly** na pásu karet vyberte rozevírací nabídku a vyberte jednu z následujících možností: 
- **Otevřít protokoly v aktuálním zobrazení**: otevře vybrané soubory protokolu v aktuálním zobrazení.  
- **Otevřít protokoly v novém okně**: otevře vybrané soubory protokolu v novém okně **prohlížeče protokolů** .  

#### <a name="close-and-clear-logs"></a>Zavřít a vymazat protokoly
Zavře všechny otevřené soubory protokolů. Vymaže také všechny zobrazené položky souborů protokolu z okna. Support Center v budoucnu tyto položky nezobrazí.

V dolní části tlačítka **Zavřít a vymazat protokoly** na pásu karet vyberte rozevírací nabídku a vyberte jednu z následujících možností: 
- **Vymazat všechny položky**: vymaže všechny zobrazené položky souboru protokolu z okna. Support Center v budoucnu tyto položky nezobrazí.  
- **Zavřít všechny protokoly**: zavře všechny otevřené soubory protokolů.  

#### <a name="find"></a>Vyhledávání
Otevře dialogové okno **Najít** . Zadejte řetězec, který chcete vyhledat. Chcete-li se vyhnout shodám u krátkých řetězců v jiných řetězcích, můžete zvolit, aby odpovídala celým slovům. Můžete také zvolit, že se má u řetězce rozlišovat velká a malá písmena.

#### <a name="find-next"></a>Najít další
Po vyhledání shody pro řetězec, který hledáte, přejdete touto možností na další shodu.

#### <a name="find-previous"></a>Najít předchozí
Po nalezení dvou nebo více shod pro řetězec, který hledáte, přejde Tato možnost na předchozí shodu.

#### <a name="options"></a>Možnosti

- **Živá aktualizace**: Sledujte změny v aktuálně otevřeném souboru protokolu. Tato funkce nefunguje, když je otevřeno více souborů protokolu. Tato možnost je ve výchozím nastavení povolená.  

- **Automatické posouvání**: Pokud zvolíte možnost **živé aktualizace** , tato možnost automaticky posune zobrazení protokolu, aby se zobrazily nově přidané položky. Tato funkce nefunguje, když je otevřeno více souborů protokolu. Tato možnost je ve výchozím nastavení povolená.  

- **Zobrazit podrobnosti**: Když vyberete zprávu souboru protokolu, v dolní části karty **protokoly** se zobrazí podrobnosti zprávy souboru protokolu. Tato možnost je ve výchozím nastavení povolená.  

- **Rychlý filtr**: vyfiltrujte zprávy souboru protokolu ve všech otevřených souborech protokolů, abyste našli konkrétní řetězec. Můžete filtrovat podle textu protokolu, názvu komponenty a ID vlákna. Chcete-li najít podobné zprávy protokolu, klikněte pravým tlačítkem myši na zprávu protokolu a vyberte možnost **rychlý filtr** pro text protokolu.  

- **Zalomit text protokolu**: zabalte dlouhé a víceřádkové zprávy tak, aby se vešly do jednoho sloupce. Toto chování usnadňuje čtení těchto zpráv. Tato možnost je ve výchozím nastavení povolená.  

- **Nezpracovaná položka protokolu – zobrazení**: zobrazí nezpracované řádky protokolu.  

- **Rozšířené filtry**: otevřete dialogové okno **Rozšířené filtry** . Další informace najdete v tématu [Rozšířené filtry souborů protokolu](#bkmk_adv-filters).  

- **Odkazy na kód chyby**: kódy chyb v textu protokolu jsou zvýrazněny a lze je kliknutímit. Tato možnost je ve výchozím nastavení povolená.  

#### <a name="error-lookup"></a>Chyba při vyhledávání
Zadejte kód chyby pro vyhledání tohoto kódu chyby v aktuálně otevřených souborech protokolů. Použijte následující formáty kódu chyby:
- **32-bitové celé číslo (podepsané)**: například`-2147024891`  
- **32-bitové celé číslo (bez znaménka)**: například`2147942405`  
- **32 – šestnáctkový**příklad:`0x80070005`  

#### <a name="decode-certificate"></a>Dekódovat certifikát
V dialogovém okně **dekódovat certifikát** vložte hodnotu serializovaného certifikátu pro jakýkoli certifikát na klienta. Vyhledá tuto hodnotu v registru, v souborech protokolů nebo ve službě WMI. Vyberte **proces** pro zobrazení obecných informací a podrobností o certifikátu. Tyto informace zahrnují cestu k certifikaci. Vyberte **exportovat** a exportujte certifikát jako soubor **. cer** .



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a>Rozšířené filtry souborů protokolů

Rozšířené filtry souborů protokolu umožňují zahrnout, vyloučit nebo zvýraznit konkrétní řetězce. Tyto řetězce se můžou vyskytnout v souboru protokolu nebo skupině souborů protokolu při prohlížení záznamů v souborech protokolu. Při vytváření filtru používejte hledání pomocí zástupných znaků. Pokud máte užitečnou kombinaci filtrů, uložte je jako *sadu filtrů*. 

Rozšířené filtry souborů protokolu nahrazují rychlé filtry. Použijte obojí, ale rychlé filtry se použijí pouze na zobrazená data protokolu. Rozšířené filtry určují, jaká data se zpočátku zobrazují předtím, než použijí jakékoli rychlé filtry.

V dialogovém okně Rozšířené filtry můžete vytvořit komplexní sady filtrů. Tyto sady filtrů hledají řetězce v mnoha součástech souboru protokolu. Mezi tyto komponenty patří zprávy, vlákna, úrovně protokolování a součásti. Sada filtrů obsahuje několik příkazů filtru, pomocí kterých můžete zahrnout, vyloučit nebo zvýraznit zprávy souboru protokolu. Filtr definuje sloupec souboru protokolu, ve kterém se má hledat, operátor a hodnota. Hodnota může obsahovat regulární výrazy, například *zástupný* znak `*`.


### <a name="add-a-filter"></a>Přidání filtru

1. V okně **Log Viewer** nebo na kartě **protokoly** nástroje Support Center vyberte **Rozšířené filtry**.  

2. V dialogu Rozšířené filtry vyberte **Přidat**. Pak vyberte jednu z následujících možností, které se mají použít pro položky protokolu, které odpovídají vašemu filtru:  
    - **Zařadit členy**  
    - **Exclude**  
    - **Zvýraznit**  

3. V dialogovém okně **Upřesnit konfiguraci filtru** vyberte sloupec a operátor:  

    - **Sloupec**: vyberte, kde se mají hledat řetězce, které odpovídají vašemu filtru:  

         - **Text protokolu**: hledání v textu souboru protokolu  

         - **Závažnost protokolu**: vyhledejte protokoly s určitou úrovní závažnosti. Nastavte tyto úrovně závažnosti v poli **hodnota** .  

         - **Součást**: vyhledat konkrétní komponentu podle názvu  

         - **ID vlákna**: Vyhledá zprávy protokolu s určitým ID vlákna.  

         - **Zdrojový soubor**: vyhledejte protokolové zprávy, které se vyskytují v určitém souboru protokolu.  

    - **Operátor**: vyberte operátor pro filtr.  

4. V poli **hodnota** zadejte hodnotu, která se má filtrovat. Pokud hodnota obsahuje regulární výrazy, vyberte možnost **Povolit porovnání regulárního výrazu**.  


### <a name="manage-filter-sets"></a>Správa sad filtrů

- Chcete-li upravit filtr, vyberte filtr a pak vyberte **Upravit**.  

- Pokud chcete filtr odstranit, vyberte filtr a pak vyberte **Odstranit**.  

- Pokud chcete vymazat všechny filtry, vyberte **Vymazat**.  

- Pokud chcete uložit aktuální sadu filtrů, vyberte **Uložit filtry**. Pak uložte sadu filtrů jako soubor **. Filterset** .  

- Pokud chcete načíst uloženou sadu filtrů, vyberte **načíst filtry**. Pak přejděte k dříve uloženému souboru **. Filterset** .  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a>Reference k nástroji Support Center Viewer

Tato část popisuje uživatelské rozhraní (UI) pro nástroj Configuration Manager **Support Center Viewer** . Dostupné karty se liší v závislosti na obsahu sady pro řešení potíží. [Nabídka okna](#bkmk_viewer-window) a [karta Domů](#bkmk_viewer-home) se zobrazí ve výchozím nastavení.
- [Nabídka okno](#bkmk_viewer-window)
- [Karta Domů](#bkmk_viewer-home)
- [Karta konfigurace](#bkmk_viewer-config)
- [Karta protokoly](#bkmk_viewer-logs)
- [Karta výpisy ladění](#bkmk_viewer-debug)
- [Karta WMI](#bkmk_viewer-wmi)
- [Karta registr](#bkmk_viewer-registry)
- [Karta Zásady](#bkmk_viewer-policy)
- [Karta certifikáty](#bkmk_viewer-certs)
- [Karta Poradce při potížích](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a>Nabídka okno

V levém horním rohu okna nástroje Support Center Viewer otevřete tuto nabídku tak, že vyberete šipku v modrém poli.

#### <a name="open-bundle"></a>Otevřít sadu prostředků
Přejděte do umístění datové sady, kterou vytvořila aplikace Support Center.

#### <a name="about"></a>Informace
Zobrazí informace o nástroji Support Center Viewer.

#### <a name="options"></a>Možnosti
V dialogovém okně **Možnosti** můžete:
- Snížit pohyb animovaných prvků uživatelského rozhraní  
- Změna umístění dočasných souborů    
- Resetovat upozornění. Všechny varovné zprávy, které jste předtím potlačili, se po aktivaci zobrazí znovu.  
- Obnovte dočasnou cestu k souboru na výchozí hodnotu.`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Ukončit
Ukončí Support Center Viewer.


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a>Karta Domů

#### <a name="open-bundle"></a>Otevřít sadu prostředků
Přejděte do umístění datové sady, kterou vytvořila aplikace Support Center.

#### <a name="open-log-file"></a>Otevřít soubor protokolu
Vyberte jeden nebo více souborů protokolu, které chcete otevřít.

#### <a name="decode-certificate"></a>Dekódovat certifikát
V dialogovém okně **dekódovat certifikát** vložte hodnotu serializovaného certifikátu pro jakýkoli certifikát na klienta. Vyhledá tuto hodnotu v registru, v souborech protokolů nebo ve službě WMI. Vyberte **proces** pro zobrazení obecných informací a podrobností o certifikátu. Tyto informace zahrnují cestu k certifikaci. Vyberte **exportovat** a exportujte certifikát jako soubor **. cer** .


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a>Karta konfigurace

Karta **Konfigurace** nástroje Support Center Viewer nabízí následující zobrazení s daty načtenými z zprostředkovatelů rozhraní WMI:

#### <a name="client"></a>Klient
Toto zobrazení obsahuje stejné informace, které jsou uvedeny na kartě **klient** nástroje Support Center.

#### <a name="operating-system"></a>Operační systém
Podrobnosti o operačním systému klienta. Používá třídu [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) .

#### <a name="computer"></a>Počítač
Podrobnosti o klientském počítači. Používá třídu [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) .

#### <a name="services"></a>Služby
Podrobnosti o službách spuštěných v klientském počítači. Používá třídu [Win32_Service](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service) .

#### <a name="network-adapters"></a>Síťové adaptéry
Podrobnosti o síťových adaptérech nainstalovaných v klientském počítači. Používá třídu [Win32_NetworkAdapterConfiguration](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) .


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a>Karta protokoly

Karta **protokoly** zobrazuje seznam souborů protokolu, které jsou součástí sady. Každý řádek na této kartě poskytuje cestu, název a velikost souboru protokolu. 

#### <a name="open"></a>Otevřít
Po výběru souboru protokolu kliknutím na toto tlačítko otevřete **Prohlížeč protokolů**. Poskytuje podmnožinu funkcí, které se zobrazují na kartě protokoly nástroje Support Center.

#### <a name="decode-certificate"></a>Dekódovat certifikát
V dialogovém okně **dekódovat certifikát** vložte hodnotu serializovaného certifikátu pro jakýkoli certifikát na klienta. Vyhledá tuto hodnotu v registru, v souborech protokolů nebo ve službě WMI. Vyberte **proces** pro zobrazení obecných informací a podrobností o certifikátu. Tyto informace zahrnují cestu k certifikaci. Vyberte **exportovat** a exportujte certifikát jako soubor **. cer** .


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a>Karta výpisy ladění

Každý řádek na této kartě poskytuje podrobné informace o souborech výpisu ladění, které jsou k dispozici pro export. Pomocí této karty můžete exportovat soubory výpisu ladění (. dmp) pro další analýzu. Tato analýza používá ladicí nástroj, jako je například WinDbg. 

> [!WARNING]  
> Výpisy ladění můžou obsahovat citlivé informace, včetně hesel, kryptografických tajných klíčů nebo uživatelských dat. Shromažďovat pouze výpisy ladění na doporučení podpora Microsoftu personál. Sady dat, které obsahují výpisy ladění, by se měly pečlivě zpracovat, aby se chránily před neoprávněným přístupem.  

#### <a name="export"></a>Export
Uloží kopii vybraného souboru výpisu ladění.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a>Karta WMI

Tato karta zobrazuje sadu dat WMI z klienta Configuration Manager, který obsahuje datový svazek. 

#### <a name="find"></a>Vyhledávání
Otevře dialog najít, který má následující funkce:  

- **Najít**: zadejte řetězec, který chcete v sadě dat WMI vyhledat. Podporuje zástupné znaky.  

- **Podívejte se na**: vyberte, jestli chcete hledat v sadě dat WMI pro vyhovující **třídu nebo název instance**, **vlastnost**nebo **hodnotu**.  

- **Odpovídá jenom celému řetězci**: ve výchozím nastavení vyhledá dialog najít řetězce, které obsahují řetězec, pro který hledáte. Toto políčko zaškrtněte, pokud chcete vyhledat pouze řetězce, které jsou přesnou shodu s vámi poskytnutým řetězcem.  

#### <a name="find-next"></a>Najít další
Toto tlačítko otevře další instanci řetězce, který jste zadali v dialogovém okně Najít v rámci sady dat WMI.

#### <a name="decode-certificate"></a>Dekódovat certifikát
V dialogovém okně **dekódovat certifikát** vložte hodnotu serializovaného certifikátu pro jakýkoli certifikát na klienta. Vyhledá tuto hodnotu v registru, v souborech protokolů nebo ve službě WMI. Vyberte **proces** pro zobrazení obecných informací a podrobností o certifikátu. Tyto informace zahrnují cestu k certifikaci. Vyberte **exportovat** a exportujte certifikát jako soubor **. cer** .


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a>Karta registr

Kartu **registr** použijte k zobrazení dat registru zahrnutých do sady dat a k exportu těchto dat pro další analýzu.

#### <a name="export"></a>Export
Uložte kopii klíče registru a podklíčů, které jste vybrali jako soubor registru (. reg).

#### <a name="find"></a>Vyhledávání
Otevře dialog najít, který má následující funkce:  

- **Najít**: zadejte řetězec, který chcete v sadě dat WMI vyhledat. Podporuje zástupné znaky.  

- **Podívejte se na**: vyberte, jestli chcete hledat v sadě dat WMI pro vyhovující **třídu nebo název instance**, **vlastnost**nebo **hodnotu**.  

- **Odpovídá jenom celému řetězci**: ve výchozím nastavení vyhledá dialog najít řetězce, které obsahují řetězec, pro který hledáte. Toto políčko zaškrtněte, pokud chcete vyhledat pouze řetězce, které jsou přesnou shodu s vámi poskytnutým řetězcem.  

#### <a name="find-next"></a>Najít další
Toto tlačítko otevře další instanci řetězce, který jste zadali v dialogovém okně Najít v rámci sady dat WMI.

#### <a name="decode-certificate"></a>Dekódovat certifikát
V dialogovém okně **dekódovat certifikát** vložte hodnotu serializovaného certifikátu pro jakýkoli certifikát na klienta. Vyhledá tuto hodnotu v registru, v souborech protokolů nebo ve službě WMI. Vyberte **proces** pro zobrazení obecných informací a podrobností o certifikátu. Tyto informace zahrnují cestu k certifikaci. Vyberte **exportovat** a exportujte certifikát jako soubor **. cer** .


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a>Karta Zásady

Karta **zásady** se používá k zobrazení dat zásad zahrnutých do sady dat. 

#### <a name="find"></a>Vyhledávání
Otevře dialog najít, který má následující funkce:  

- **Najít**: zadejte řetězec, který chcete v sadě dat WMI vyhledat. Podporuje zástupné znaky.  

- **Podívejte se na**: vyberte, jestli chcete hledat v sadě dat WMI pro vyhovující **třídu nebo název instance**, **vlastnost**nebo **hodnotu**.  

- **Odpovídá jenom celému řetězci**: ve výchozím nastavení vyhledá dialog najít řetězce, které obsahují řetězec, pro který hledáte. Toto políčko zaškrtněte, pokud chcete vyhledat pouze řetězce, které jsou přesnou shodu s vámi poskytnutým řetězcem.  

#### <a name="find-next"></a>Najít další
Toto tlačítko otevře další instanci řetězce, který jste zadali v dialogovém okně Najít v rámci sady dat WMI.

#### <a name="decode-certificate"></a>Dekódovat certifikát
V dialogovém okně **dekódovat certifikát** vložte hodnotu serializovaného certifikátu pro jakýkoli certifikát na klienta. Vyhledá tuto hodnotu v registru, v souborech protokolů nebo ve službě WMI. Vyberte **proces** pro zobrazení obecných informací a podrobností o certifikátu. Tyto informace zahrnují cestu k certifikaci. Vyberte **exportovat** a exportujte certifikát jako soubor **. cer** .


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a>Karta certifikáty

Karta **certifikáty** slouží k zobrazení certifikátů zahrnutých do sady dat a k jejich exportu.

#### <a name="view-certificate"></a>Zobrazit certifikát
Zobrazí informace o vybraném certifikátu.

#### <a name="export"></a>Export
Otevře dialogové okno **Uložit jako** , ve kterém můžete uložit kopii certifikátu, který jste vybrali.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a>Karta Poradce při potížích

Kartu **Poradce při potížích** můžete použít k zobrazení souborů protokolu vytvořených pomocí karty Poradce při potížích nástroje Support Center.

#### <a name="view-log"></a>Zobrazit protokol
Po výběru řádku na kartě **Poradce při potížích** vyberte tuto možnost, chcete-li zobrazit soubor protokolu pomocí protokolu Log Viewer.
