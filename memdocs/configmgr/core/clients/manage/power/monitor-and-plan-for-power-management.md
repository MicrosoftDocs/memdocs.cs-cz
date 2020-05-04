---
title: Monitorování a plánování řízení spotřeby
titleSuffix: Configuration Manager
description: Naučte se monitorovat a plánovat řízení spotřeby v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715211"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Jak monitorovat a plánovat řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Následující informace vám pomůžou monitorovat a plánovat řízení spotřeby v Configuration Manager.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Využití sestav při řízení spotřeby  
 Řízení spotřeby v Configuration Manager zahrnuje několik sestav, které vám pomůžou analyzovat spotřebu energie a nastavení napájení počítačů ve vaší organizaci. Sestavy se také dají použít při odstraňování potíží.  

 Než budete moct začít používat sestavy řízení spotřeby, musíte pro svoji hierarchii nakonfigurovat vytváření sestav. Další informace o vytváření sestav v Configuration Manager najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Informace o řízení spotřeby využívané denními sestavami se uchovávají v Configuration Manager databázi lokality po dobu 31 dnů.  
>           Informace o řízení spotřeby využívané měsíčními sestavami se uchovávají v databázi lokality Configuration Manager po dobu 13 měsíců.  
>   
>  Když spouštíte sestavy během fáze monitorování a plánování a dodržování předpisů v řízení spotřeby, uložte nebo exportujte výsledky z jakýchkoliv sestav, pro které chcete zachovat data pro pozdější porovnání v případě, že jsou později odebrána pomocí Configuration Manager.  

## <a name="list-of-power-management-reports"></a>Seznam sestav řízení spotřeby  
 Následující seznamy obsahují podrobnosti o sestavách řízení spotřeby, které jsou k dispozici v Configuration Manager.  

> [!NOTE]  
>  Sestavy řízení spotřeby zobrazují počet fyzických počítačů a virtuálních počítačů ve vybrané kolekci. V sestavách řízení spotřeby se ale zobrazují jenom informace o řízení spotřeby z fyzických počítačů.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Sestava Aktivita počítače  
 Sestava **Aktivita počítače** zobrazí tyto informace o aktivitě pro zadanou kolekci v zadaném období:  

- **Zapnutý počítač** – počítač je zapnutý.  

- **Zapnutý monitor** – monitor je zapnutý.  

- **Aktivní uživatel** – došlo ke zjištění aktivity myši počítače, klávesnice počítače nebo připojení ke vzdálené ploše počítače.  

  Tato sestava se používá během fáze monitorování a plánování a fáze vynucení a pomáhá pochopit souvislosti mezi aktivitou počítače, aktivitou monitoru a aktivitou uživatele v průběhu 24 hodin. Pokud sestavu spustíte pro víc dnů, vrátí agregovaná data z tohoto období. Tato sestava vám může pomoct určit typickou pracovní (špička) a nepracovní dobu (mimo špičku), abyste se mohli rozhodnout, kdy budete uplatňovat nakonfigurovaná schémata napájení.  

  Graf zobrazuje časová období, kdy může být počítač zapnutý, ale uživatel není aktivní. Během této doby zvažte použití přísnějšího nastavení napájení, aby se snížily náklady na napájení počítačů, které jsou zapnuté, ale nepoužívají se. Počítač se počítá jako aktivní, pokud v průběhu jedné hodiny zobrazené v grafu zaznamenal aspoň na jednu minutu aktivitu počítače, uživatele nebo monitoru. Pokud počítač nehlásí data řízení spotřeby, nebude zahrnutý do sestavy **Aktivita počítače**.  

  Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Počáteční datum**|V rozevíracím seznamu vyberte počáteční datum pro tuto sestavu.|  
|**Koncové datum (volitelné)**|V rozevíracím seznamu vyberte volitelné koncové datum pro tuto sestavu.|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače).|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Pokud nezadáte hodnotu **Koncové datum (volitelné)** , bude sestava obsahovat odkaz na následující sestavu s dalšími informacemi.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o aktivitě počítače**|Kliknutím na odkaz **Kliknutím získáte podrobné informace** zobrazíte seznam aktivních, neaktivních a nehlásících se počítačů k zadanému datu.<br /><br /> Další informace najdete v části [Computer Activity Details Report](#BKMK_Activity_Details) tohoto tématu.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a>Sestava aktivita počítače podle počítače  
 Sestava **Aktivita počítače podle počítače** zobrazí graf, který znázorňuje následující aktivitu pro zadaný počítač k zadanému datu:  

- **Zapnutý počítač** – počítač je zapnutý.  

- **Zapnutý monitor** – monitor je zapnutý.  

- **Aktivní uživatel** – zjistila se aktivita myši počítače, klávesnice počítače nebo připojení ke vzdálené ploše počítače.  

  Tuto sestavu můžete spustit nezávisle nebo ji volat ze sestavy **Podrobnosti o aktivitě počítače**.  

> [!NOTE]  
>  Informace o aktivitě počítače se shromažďují z klientských počítačů při inventarizaci hardwaru. V závislosti na čase spuštění inventáře hardwaru se může shromažďovat aktivita v rámci nastaveného schématu napájení ve špičce nebo mimo špičku.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Datum sestavy**|V rozevíracím seznamu vyberte datum pro tuto sestavu.|  
|**Název počítače**|Zadejte název počítače, pro který chcete získat sestavu.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o počítači**|Kliknutím na odkaz **Kliknutím získáte podrobné informace** zobrazíte možnosti napájení, nastavení napájení a použitá schémata napájení pro vybraný počítač.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 Sestava **Podrobnosti o aktivitě počítače** zobrazí seznam aktivních nebo neaktivních počítačů s jejich možnostmi režimu spánku a probuzení z režimu spánku. Tuto sestavu volá sestava [Aktivita počítače](#BKMK_Activity) a není určená k tomu, aby ji přímo volal správce lokality.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Datum sestavy**|V rozevíracím seznamu vyberte datum, které chcete pro tuto sestavu použít.|  
|**Hodina sestavy**|V rozevíracím seznamu vyberte hodinu ze dne s vybraným datem, pro kterou chcete spustit sestavu. Platné hodnoty jsou mezi **00:00** a **23:00**.|  
|**Stav počítače**|V rozevíracím seznamu vyberte stav počítače, pro který chcete spustit sestavu. Platné hodnoty jsou **všechny** (počítače, které se zapnuly nebo vypnuly), **zapnuté** a **vypnuté** (počítače, které se vypnuly, v režimu spánku nebo v režimu hibernace). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  
|**Podporující režim spánku**|V rozevíracím seznamu vyberte, jestli chcete v sestavě zobrazit počítače podporující režim spánku. Platné hodnoty jsou **všechny** (podporuje počítače a nepodporují režim spánku), **ne** (počítače, které nejsou v režimu spánku), a **Ano** (počítače, které jsou schopné přejít do režimu spánku).|  
|**Podporující probuzení z režimu spánku**|V rozevíracím seznamu vyberte, jestli chcete v sestavě zobrazit počítače podporující probuzení z režimu spánku. Platné hodnoty jsou **všechny** (podporuje počítače a nepodporují probuzení z režimu spánku), **ne** (počítače, které nejsou schopné probuzení z režimu spánku), a **Ano** (počítače, které jsou schopné probuzení z režimu spánku).|  
|**Schéma napájení**|V rozevíracím seznamu vyberte typy schémat napájení, které chcete v sestavě zobrazit. Platné hodnoty jsou **všechny** (počítače, které nemají žádné použité plány řízení spotřeby). počítače s použitým plánem řízení spotřeby; počítače vyloučené z řízení spotřeby, **Neurčeno** (počítače, ve kterých se nastavilo plánované napájení), **definované** (počítače s použitým plánem řízení spotřeby) a **vyloučené** (počítače, které se vyloučí z řízení spotřeby).|  
|**Operační systém**|V rozevíracím seznamu vyberte operační systémy počítače, které chcete zobrazit v sestavě, nebo výběrem možnosti **Vše** zobrazte všechny operační systémy.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Aktivita počítače podle počítače**|Kliknutím na název počítače zobrazíte konkrétní aktivitu pro daný počítač přes zvolené období generování sestav. Tyto aktivity zahrnují **počítač zapnut** (byl zapnutý počítač?), **monitorování zapnuto** (je zapnuto monitorování?) a **uživatel byl aktivní** (aktivita byla zjištěna z myši, klávesnice nebo připojení ke vzdálené ploše počítače).<br /><br /> Další informace najdete v části [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) tohoto tématu.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Sestava Podrobnosti o počítači  
 Sestava **Podrobnosti o počítači** zobrazí podrobné informace o možnostech napájení, nastavení napájení a schématech napájení použitých v zadaném počítači. Tuto sestavu volají sestavy **Aktivita počítače podle počítače**, **Počítače s více schématy napájení**, **Možnosti napájení** a **Podrobnosti o nastavení napájení**. Není určená k tomu, aby ji přímo spouštěl správce lokality.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název počítače**|Zadejte název počítače, pro který chcete získat sestavu.|  
|**Režim napájení**|V rozevíracím seznamu vyberte typ nastavení napájení, který chcete zobrazit ve výsledcích sestavy. Výběrem možnosti **Napájen ze sítě** zobrazíte nastavení napájení používané tehdy, když se počítač napájí ze sítě, a výběrem možnosti **Baterie** zobrazíte nastavení napájení používané tehdy, když počítač běží na baterii.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a>Sestava Podrobnosti o počítačích nevytvářejících sestavy  
 Sestava **Podrobnosti o počítačích nevytvářejících sestavy** zobrazí seznam počítačů v zadané kolekci, které k zadanému datu a času nenahlásily žádnou aktivitu napájení. Tuto sestavu volá sestava **Aktivita počítače** a není určená k tomu, aby ji přímo volal správce lokality.  

> [!NOTE]  
>  Počítače hlásí informace o řízení spotřeby v rámci nastaveného plánu inventarizace hardwaru. Než začnete některý počítač považovat za počítač, který nevytváří sestavy, zkontrolujte, jestli nahlásil inventář hardwaru.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Datum sestavy**|V rozevíracím seznamu vyberte datum pro tuto sestavu.|  
|**Hodina sestavy**|V rozevíracím seznamu vyberte hodinu ze dne s vybraným datem, pro kterou chcete spustit sestavu. Platné hodnoty jsou mezi **00:00** a **23:00**.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Vyřazené počítače  
 Sestava **vyloučené počítače** zobrazí seznam počítačů v zadané kolekci, které jsou vyloučené z Configuration Manager řízení spotřeby.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  
|**Důvod**|V rozevíracím seznamu vyberte důvod, proč jsou počítače vyloučené z řízení spotřeby. Můžete zobrazit **všechny** (vyloučené počítače), **vyloučené správcem** (jenom počítače vyloučené správcem) a **vyloučit ho uživatel** (jenom počítače, které byly vyloučené uživatelem centra softwaru).|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o napájení počítače**|Kliknutím na název počítače zobrazíte možnosti napájení, nastavení napájení a použitá schémata napájení pro vybraný počítač.<br /><br /> Další informace najdete v části [Computer Details Report](#BKMK_Computer_Details) tohoto tématu.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a>Počítače s více schématy napájení  
 Sestava **Počítače s více schématy napájení** zobrazí seznam počítačů, které jsou členy více kolekcí, z nichž každá používá jiná schémata napájení. Pro každý počítač s potenciálně konfliktním nastavením napájení sestava zobrazí název počítače a schémata napájení použitá v každé kolekci, do které počítač patří.  

> [!IMPORTANT]  
>  Pokud je počítač členem více kolekcí, kde každá kolekce má jiné schéma napájení, použije se nejméně omezující schéma napájení.  
>   
>  Pokud je počítač členem více kolekcí, kde každá kolekce má různou dobu probuzení, použije se čas nejbližší k půlnoci.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o napájení počítače**|Kliknutím na název počítače zobrazíte možnosti napájení, nastavení napájení a použitá schémata napájení pro vybraný počítač.<br /><br /> Další informace najdete v části [Computer Details Report](#BKMK_Computer_Details) tohoto tématu.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Spotřeba energie  
 Sestava **Spotřeba energie** zobrazí následující informace:  

- Graf zobrazující celkovou měsíční spotřebu počítačů v zadané kolekci za zadané časové období v kilowatthodinách (kWh).  

- Graf zobrazující průměrnou spotřebu jednotlivých počítačů v zadané kolekci za zadané časové období v kilowatthodinách (kWh).  

- Tabulka zobrazující celkovou měsíční spotřebu v kilowatthodinách (kWh) a průměrnou spotřebu počítačů v zadané kolekci za zadané časové období.  

  Tyto informace vám můžou pomoct pochopit trendy spotřeby energie ve vašem prostředí. Jakmile u počítačů ve vybrané kolekci použijete schéma napájení, měla by jejich spotřeba energie klesnout.  

> [!NOTE]  
>  Pokud po použití schématu napájení přidáte do kolekce členy nebo je z ní odeberete, bude to mít vliv na výsledky zobrazené sestavou **Spotřeba energie** a může to ztížit porovnání výsledků z monitorovací a plánovací fáze a fáze vynucení.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Počáteční datum**|V rozevíracím seznamu vyberte počáteční datum pro tuto sestavu.|  
|**Koncové datum**|V rozevíracím seznamu vyberte koncové datum pro tuto sestavu.|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Stolní počítač zapnut**|Zadejte spotřebu energie stolního počítače, když je zapnutý. Výchozí hodnota je **0,07** kW za hodinu.|  
|**Přenosný počítač zapnut**|Zadejte spotřebu energie přenosného počítače, když je zapnutý. Výchozí hodnota je **0,02** kW za hodinu.|  
|**Stolní počítač v režimu spánku**|Zadejte spotřebu energie stolního počítače, který přešel do režimu spánku. Výchozí hodnota je **0,003** kW za hodinu.|  
|**Přenosný počítač v režimu spánku**|Zadejte spotřebu energie přenosného počítače, který přešel do režimu spánku. Výchozí hodnota je **0,001** kW za hodinu.|  
|**Stolní počítač vypnut**|Zadejte spotřebu energie stolního počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Přenosný počítač vypnut**|Zadejte spotřebu energie přenosného počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Stolní monitor zapnut**|Zadejte spotřebu energie stolního monitoru, když je zapnutý. Výchozí hodnota je **0,028** kW za hodinu.|  
|**Monitor přenosného počítače zapnut**|Zadejte spotřebu energie monitoru přenosného počítače, když je zapnutý. Výchozí hodnota je **0** kW za hodinu.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Sestava Spotřeba energie na den  
 Sestava **Spotřeba energie na den** zobrazí následující informace:  

- Graf zobrazující celkovou denní spotřebu počítačů v zadané kolekci za posledních 31 dní v kilowatthodinách (kWh).  

- Graf zobrazující průměrnou denní spotřebu jednotlivých počítačů v zadané kolekci za posledních 31 dní v kilowatthodinách (kWh).  

- Tabulka zobrazující celkovou denní spotřebu v kilowatthodinách (kWh) a průměrnou denní spotřebu počítačů v zadané kolekci za posledních 31 dní.  

  Tyto informace vám můžou pomoct pochopit trendy spotřeby energie ve vašem prostředí. Jakmile u počítačů ve vybrané kolekci použijete schéma napájení, měla by jejich spotřeba energie klesnout.  

> [!NOTE]  
>  Pokud po použití schématu napájení přidáte do kolekce členy nebo je z ní odeberete, bude to mít vliv na výsledky zobrazené sestavou **Spotřeba energie** a může to ztížit porovnání výsledků z monitorovací a plánovací fáze a fáze vynucení.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Stolní počítač zapnut**|Zadejte spotřebu energie stolního počítače, když je zapnutý. Výchozí hodnota je **0,07** kW za hodinu.|  
|**Přenosný počítač zapnut**|Zadejte spotřebu energie přenosného počítače, když je zapnutý. Výchozí hodnota je **0,02** kW za hodinu.|  
|**Stolní počítač v režimu spánku**|Zadejte spotřebu energie stolního počítače, který přešel do režimu spánku. Výchozí hodnota je **0,003** kW za hodinu.|  
|**Přenosný počítač v režimu spánku**|Zadejte spotřebu energie přenosného počítače, který přešel do režimu spánku. Výchozí hodnota je **0,001** kW za hodinu.|  
|**Stolní počítač vypnut**|Zadejte spotřebu energie stolního počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Přenosný počítač vypnut**|Zadejte spotřebu energie přenosného počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Stolní monitor zapnut**|Zadejte spotřebu energie stolního monitoru, když je zapnutý. Výchozí hodnota je **0,028** kW za hodinu.|  
|**Monitor přenosného počítače zapnut**|Zadejte spotřebu energie monitoru přenosného počítače, když je zapnutý. Výchozí hodnota je **0** kW za hodinu.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Sestava Náklady na energii  
 Sestava **Náklady na energii** zobrazí následující informace:  

- Graf zobrazující celkové měsíční náklady na energii pro počítače v zadané kolekci za zadané časové období.  

- Graf zobrazující průměrné měsíční náklady na energii pro jednotlivé počítače v zadané kolekci za zadané časové období.  

- Tabulka zobrazující celkové měsíční náklady na energii a průměrné měsíční náklady na energii pro počítače v zadané kolekci za posledních 31 dní.  

  Tyto informace vám můžou pomoct pochopit trendy nákladů na energii ve vašem prostředí. Jakmile u počítačů ve vybrané kolekci použijete schéma napájení, měly by jejich náklady na energii klesnout.  

  Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Počáteční datum**|V rozevíracím seznamu vyberte počáteční datum pro tuto sestavu.|  
|**Koncové datum**|V rozevíracím seznamu vyberte koncové datum pro tuto sestavu.|  
|**Náklady na kWh**|Zadejte náklady na kWh elektřiny. Výchozí hodnota je **0,09**.<br /><br /> V sekci skrytých parametrů můžete upravit jednotku měny používanou v této sestavě.|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Stolní počítač zapnut**|Zadejte spotřebu energie stolního počítače, když je zapnutý. Výchozí hodnota je **0,07** kW za hodinu.|  
|**Přenosný počítač zapnut**|Zadejte spotřebu energie přenosného počítače, když je zapnutý. Výchozí hodnota je **0,02** kW za hodinu.|  
|**Stolní počítač v režimu spánku**|Zadejte spotřebu energie stolního počítače, který přešel do režimu spánku. Výchozí hodnota je **0,003** kW za hodinu.|  
|**Přenosný počítač v režimu spánku**|Zadejte spotřebu energie přenosného počítače, který přešel do režimu spánku. Výchozí hodnota je **0,001** kW za hodinu.|  
|**Stolní počítač vypnut**|Zadejte spotřebu energie stolního počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Přenosný počítač vypnut**|Zadejte spotřebu energie přenosného počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Stolní monitor zapnut**|Zadejte spotřebu energie stolního monitoru, když je zapnutý. Výchozí hodnota je **0,028** kW za hodinu.|  
|**Monitor přenosného počítače zapnut**|Zadejte spotřebu energie monitoru přenosného počítače, když je zapnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Měna**|Zadejte popisek měny, který se má použít v této sestavě. Výchozí hodnota je **USD ($)**.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Sestava Náklady na energii za den  
 Sestava **Náklady na energii za den** zobrazí následující informace:  

- Graf zobrazující celkové denní náklady na energii pro počítače v zadané kolekci za posledních 31 dní.  

- Graf zobrazující průměrné denní náklady na energii pro jednotlivé počítače v zadané kolekci za posledních 31 dní.  

- Tabulka zobrazující celkové denní náklady na energii a průměrné denní náklady na energii pro počítače v zadané kolekci za posledních 31 dní.  

  Tyto informace vám můžou pomoct pochopit trendy nákladů na energii ve vašem prostředí. Jakmile u počítačů ve vybrané kolekci použijete schéma napájení, měly by jejich náklady na energii klesnout.  

  Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  
|**Náklady na kWh**|Zadejte náklady na kWh elektřiny. Výchozí hodnota je **0,09**.<br /><br /> V sekci skrytých parametrů můžete upravit jednotku měny používanou v této sestavě.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Stolní počítač zapnut**|Zadejte spotřebu energie stolního počítače, když je zapnutý. Výchozí hodnota je **0,07** kW za hodinu.|  
|**Přenosný počítač zapnut**|Zadejte spotřebu energie přenosného počítače, když je zapnutý. Výchozí hodnota je **0,02** kW za hodinu.|  
|**Stolní počítač v režimu spánku**|Zadejte spotřebu energie stolního počítače, který přešel do režimu spánku. Výchozí hodnota je **0,003** kW za hodinu.|  
|**Přenosný počítač v režimu spánku**|Zadejte spotřebu energie přenosného počítače, který přešel do režimu spánku. Výchozí hodnota je **0,001** kW za hodinu.|  
|**Stolní počítač vypnut**|Zadejte spotřebu energie stolního počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Přenosný počítač vypnut**|Zadejte spotřebu energie přenosného počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Stolní monitor zapnut**|Zadejte spotřebu energie stolního monitoru, když je zapnutý. Výchozí hodnota je **0,028** kW za hodinu.|  
|**Monitor přenosného počítače zapnut**|Zadejte spotřebu energie monitoru přenosného počítače, když je zapnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Měna**|Zadejte popisek měny, který se má použít v této sestavě. Výchozí hodnota je **USD ($)**.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Sestava Ekologický dopad  
 Sestava **Ekologický dopad** zobrazí následující informace:  

- Graf zobrazující celkový měsíční počet vygenerovaných CO2 (v tunách) pro počítače v zadané kolekci za zadané časové období.  

- Graf zobrazující průměrné měsíční vygenerované CO2 (v tunách) pro každý počítač v zadané kolekci za zadané časové období.  

- Tabulka zobrazující celkové měsíční vygenerované CO2 a průměrné měsíční vygenerované CO2 pro počítače v zadané kolekci za zadané časové období.  

  Sestava **vlivu na životní prostředí** vypočítá množství vygenerovaného CO2 (v tunách) pomocí času, kdy byl počítač nebo monitor zapnutý za dobu 24 hodin.  

  Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Počáteční datum sestavy**|V rozevíracím seznamu vyberte počáteční datum pro tuto sestavu.|  
|**Koncové datum sestavy**|V rozevíracím seznamu vyberte koncové datum pro tuto sestavu.|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Stolní počítač zapnut**|Zadejte spotřebu energie stolního počítače, když je zapnutý. Výchozí hodnota je **0,07** kW za hodinu.|  
|**Přenosný počítač zapnut**|Zadejte spotřebu energie přenosného počítače, když je zapnutý. Výchozí hodnota je **0,02** kW za hodinu.|  
|**Stolní počítač v režimu spánku**|Zadejte spotřebu energie stolního počítače, který přešel do režimu spánku. Výchozí hodnota je **0,003** kW za hodinu.|  
|**Přenosný počítač v režimu spánku**|Zadejte spotřebu energie přenosného počítače, který přešel do režimu spánku. Výchozí hodnota je **0,001** kW za hodinu.|  
|**Stolní počítač vypnut**|Zadejte spotřebu energie stolního počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Přenosný počítač vypnut**|Zadejte spotřebu energie přenosného počítače, když je vypnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Stolní monitor zapnut**|Zadejte spotřebu energie stolního monitoru, když je zapnutý. Výchozí hodnota je **0,028** kW za hodinu.|  
|**Monitor přenosného počítače zapnut**|Zadejte spotřebu energie monitoru přenosného počítače, když je zapnutý. Výchozí hodnota je **0** kW za hodinu.|  
|**Uhlíkový faktor (tuny/kWh)** (mix CO2)|Zadejte hodnotu uhlíkového faktoru (v tunách/kWh), kterou vám většinou sdělí váš poskytovatel elektrické energie. Výchozí hodnota je **0,0015** tuny na kWh.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Sestava Ekologický dopad na den  
 Sestava **Ekologický dopad na den** zobrazí následující informace:  

- Graf zobrazující celkový denní počet vygenerovaných CO2 (v tunách) pro počítače v zadané kolekci za posledních 31 dnů.  

- Graf zobrazující průměrné denní vygenerované CO2 (v tunách) pro každý počítač v zadané kolekci za posledních 31 dní.  

- Tabulka zobrazující celkový denní vygenerovaný CO2 a průměrný denní CO2 vygenerovaný pro počítače v zadané kolekci za posledních 31 dní.  

  Sestava **ekologický dopad na den** vypočítá množství vygenerovaného CO2 (v tunách) pomocí času, kdy byl počítač nebo monitor zapnutý za 24 hodin.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  
|**Typ zařízení**|V rozevíracím seznamu vyberte typ počítače, pro který chcete vytvořit sestavu. Platné hodnoty jsou **všechny** (stolní i přenosné počítače), **plocha** (jenom stolní počítače) a **přenosný počítač** (jenom přenosné počítače). Tyto hodnoty se vrátí jenom pro zvolené období generování sestav.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Stolní počítač zapnut**|Zadejte spotřebu energie stolního počítače, když je zapnutý. Výchozí hodnota je **0,07** kWh.|  
|**Přenosný počítač zapnut**|Zadejte spotřebu energie přenosného počítače, když je zapnutý. Výchozí hodnota je **0,02** kWh.|  
|**Stolní počítač vypnut**|Zadejte spotřebu energie stolního počítače, když je vypnutý. Výchozí hodnota je **0** kWh.|  
|**Přenosný počítač vypnut**|Zadejte spotřebu energie přenosného počítače, když je vypnutý. Výchozí hodnota je **0** kWh.|  
|**Stolní počítač v režimu spánku**|Zadejte spotřebu energie stolního počítače, který přešel do režimu spánku. Výchozí hodnota je **0,003** kWh.|  
|**Přenosný počítač v režimu spánku**|Zadejte spotřebu energie přenosného počítače, který přešel do režimu spánku. Výchozí hodnota je **0,001** kWh.|  
|**Stolní monitor zapnut**|Zadejte spotřebu energie stolního monitoru, když je zapnutý. Výchozí hodnota je **0,028** kWh.|  
|**Monitor přenosného počítače zapnut**|Zadejte spotřebu energie monitoru přenosného počítače, když je zapnutý. Výchozí hodnota je **0** kWh.|  
|**Uhlíkový faktor (tuny/kWh)** (mix CO2)|Zadejte hodnotu uhlíkového faktoru (v tunách/kWh), kterou vám většinou sdělí váš poskytovatel elektrické energie. Výchozí hodnota je **0,0015** tuny na kWh.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava neobsahuje odkazy na žádné jiné sestavy řízení spotřeby.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Sestava Podrobnosti o režimu spánku počítače  
 Sestava **Podrobnosti o režimu spánku počítače** zobrazí seznam počítačů, které z určitého důvodu v zadaném časovém období nepřešly do režimu spánku nebo hibernace. Tuto sestavu volá **Sestava režimu spánku** a nespouští ji přímo správce lokality.  

 **Sestava režimu spánku** zobrazí počítače jako **Nepodporující režim spánku** , pokud nejsou schopné přejít do režimu spánku a byly v průběhu celého zadaného intervalu sestavy zapnuté. Sestava zobrazí počítače jako **Neuvádět podporující do režimu hibernace** , pokud nejsou schopné přejít do režimu hibernace a byly v průběhu celého zadaného intervalu sestavy zapnuté.  

> [!NOTE]  
>  Řízení spotřeby může shromažďovat příčiny, které zabránily v přechodu do režimu spánku nebo hibernace, jenom u počítačů se systémem Windows 7 nebo Windows Server 2008 R2.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Interval sestavy (dny)**|Zadejte počet dnů pro vytvoření sestavy. Aktuální hodnota činí **7** dní.|  
|**Příčina nefunkčnosti režimu spánku**|V rozevíracím seznamu vyberte jednu z příčin, která může počítačům zabránit v přechodu do režimu spánku nebo hibernace.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o počítači**|Kliknutím na odkaz **Kliknutím získáte podrobné informace** zobrazíte možnosti napájení, nastavení napájení a použitá schémata napájení pro vybraný počítač.<br /><br /> Další informace najdete v části [Computer Details Report](#BKMK_Computer_Details) tohoto tématu.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 **Sestava režimu spánku** zobrazí seznam běžných příčin, které počítačům zabránily v přechodu do režimu spánku nebo hibernace, a počet počítačů ovlivněných jednotlivými příčinami v zadaném období. Existuje několik příčin, které můžou počítači zabránit v přechodu do režimu spánku nebo hibernace, třeba proces spuštěný v počítači, otevřená relace vzdálené plochy nebo neschopnost počítače přejít do režimu spánku nebo hibernace. Z této sestavy můžete otevřít sestavu **Podrobnosti o režimu spánku počítače**, která zobrazí seznam počítačů ovlivněných jednotlivými příčinami toho, že počítače nepřejdou do režimu spánku nebo hibernace.  

 Sestava režimu spánku zobrazí počítače jako **Nepodporující režim spánku** , pokud nejsou schopné přejít do režimu spánku a byly v průběhu celého zadaného intervalu sestavy zapnuté. Sestava zobrazí počítače jako **Neuvádět podporující do režimu hibernace** , pokud nejsou schopné přejít do režimu hibernace a byly v průběhu celého zadaného intervalu sestavy zapnuté.  

> [!NOTE]  
>  Řízení spotřeby může shromažďovat příčiny, které zabránily v přechodu do režimu spánku nebo hibernace, jenom u počítačů se systémem Windows 7 nebo Windows Server 2008 R2.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**Interval sestavy (dny)**|Zadejte počet dnů pro vytvoření sestavy. Aktuální hodnota činí **7** dní. Maximální hodnota je **365** dní. Pokud chcete sestavu spustit pro dnešní den, zadejte hodnotu **0** .|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o režimu spánku počítače**|Kliknutím na číslo ve sloupci **Ovlivněné počítače** zobrazíte seznam počítačů, které kvůli vybrané příčině nemohly přejít do režimu spánku nebo hibernace.<br /><br /> Další informace najdete v části [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) tohoto tématu.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Sestava Možnosti napájení  
 Sestava **Možnosti napájení** zobrazí možnosti hardwaru řízení spotřeby u počítačů v zadané kolekci. Tato sestava se většinou používá v monitorovací fázi řízení spotřeby, aby se určily možnosti řízení spotřeby počítačů ve vaší organizaci. Informace zobrazené v této sestavě se pak dají použít k vytváření kolekcí počítačů, ve kterých chcete použít schémata napájení nebo které chcete vyloučit z řízení spotřeby. Sestava zobrazuje tyto možnosti řízení spotřeby:  

- **Podporující režim spánku** – uvádí, jestli počítač podporuje přechod do režimu spánku, pokud je tak nakonfigurovaný.  

- **Podporující do režimu hibernace** – uvádí, jestli může počítač přejít do režimu hibernace, pokud je tak nakonfigurovaný.  

- **Probudit z režimu spánku** – uvádí, jestli se počítač může probudit z režimu spánku, pokud je tak nakonfigurovaný.  

- **Probudit z režimu hibernace** – uvádí, jestli se počítač může probudit z režimu hibernace, pokud je tak nakonfigurovaný.  

  Hodnoty hlášené sestavou **Možnosti napájení** uvádí možnosti přechodu počítačů do režimu spánku a hibernace tak, jak je hlásí systém Windows. Hodnoty v sestavě ale nezahrnují případy, kdy těmto funkcím brání nastavení systému Windows nebo BIOS.  

  Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  
|**Filtr zobrazení**|V rozevíracím seznamu vyberte možnost **Nepodporováno** , pokud chcete zobrazit pouze počítače v zadané kolekci, které nepodporují režim spánku, hibernace, probuzení z režimu spánku nebo probuzení z režimu hibernace. Výběrem **Zobrazit vše** zobrazíte všechny počítače v zadané kolekci.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Tato sestava nemá žádné skryté parametry, které byste mohli nastavit.  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o počítači**|Kliknutím na název počítače zobrazíte možnosti napájení, nastavení napájení a použitá schémata napájení pro vybraný počítač.<br /><br /> Další informace najdete v části [Computer Details Report](#BKMK_Computer_Details) tohoto tématu.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Sestava Nastavení napájení  
 Sestava **Nastavení napájení** zobrazí souhrnný seznam nastavení napájení, které používají počítače v zadané kolekci. Pro každé nastavení napájení se zobrazí možné režimy napájení, hodnoty a jednotky a také počet počítačů, které používají tyto hodnoty. Tato sestava se dá použít během monitorovací fáze řízení spotřeby k tomu, aby správci pomohla pochopit stávající nastavení napájení používané počítači v lokalitě a naplánovat optimální nastavení napájení, které se má uplatnit prostřednictvím schématu napájení. Sestava je užitečná také při odstraňování potíží, když je potřeba zkontrolovat, jestli se správně uplatňuje nastavení napájení.  

> [!NOTE]  
>  Zobrazené nastavení se z klientských počítačů shromažďuje během inventarizace hardwaru. V závislosti na čase spuštění inventáře hardwaru se můžou shromažďovat informace o použitých schématech napájení ve špičce nebo mimo špičku.  

 Ke konfiguraci této sestavy slouží následující parametry.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Název kolekce**|V rozevíracím seznamu vyberte kolekci pro tuto sestavu.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Zadejte počet jazyků, ve kterých chcete zobrazit názvy nastavení napájení hlášené klientskými počítači. Pokud chcete zobrazit jenom nejoblíbenější jazyk, nechte u tohoto nastavení výchozí hodnotu **1**. Pokud chcete zobrazit všechny jazyky, nastavte hodnotu **0**.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o nastavení napájení**|Kliknutím na počet počítačů ve sloupci **Počítače** zobrazíte seznam všech počítačů, které používají nastavení napájení v daném řádku.<br /><br /> Další informace najdete v části [Power Settings Details Report](#BKMK_Settings_Details) tohoto tématu.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 Sestava **Podrobnosti o nastavení napájení** zobrazí další informace o počítačích vybraných v sestavě **Nastavení napájení** . Tuto sestavu volá sestava **Nastavení napájení** a nespouští ji přímo správce lokality.  

#### <a name="required-report-parameters"></a>Požadované parametry sestavy  
 Ke spuštění této sestavy je potřeba zadat následující parametry.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**Kolekce**|V rozevíracím seznamu vyberte kolekci, kterou chcete pro tuto sestavu použít.|  
|**GUID nastavení napájení**|V rozevíracím seznamu vyberte GUID nastavení napájení, pro které chcete vytvořit sestavu. Seznam všech nastavení napájení a jejich použití najdete v tématu [dostupná nastavení plánu řízení spotřeby](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) v tématu [Postup vytvoření a použití schémat napájení](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Režim napájení**|V rozevíracím seznamu vyberte typ nastavení napájení, který chcete zobrazit ve výsledcích sestavy. Výběrem možnosti **Napájen ze sítě** zobrazíte nastavení napájení používané tehdy, když se počítač napájí ze sítě, a výběrem možnosti **Baterie** zobrazíte nastavení napájení používané tehdy, když počítač běží na baterii.|  
|**Index nastavení**|V rozevíracím seznamu vyberte hodnotu pro vybraný název nastavení napájení, pro který chcete vytvořit sestavu. Pokud třeba chcete zobrazit všechny počítače s nastavením **Vypnout pevný disk po** na hodnotě **10** minut, u položky **Název nastavení napájení** vyberte hodnotu **Vypnout pevný disk po** a u položky **Index nastavení** hodnotu **10**.|  

#### <a name="hidden-report-parameters"></a>Skryté parametry sestavy  
 Volitelně můžete zadat následující skryté parametry, které umožňují změnit chování této sestavy.  

|Název parametru|Popis|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Zadejte počet jazyků, ve kterých chcete zobrazit názvy nastavení napájení hlášené klientskými počítači. Pokud chcete zobrazit jenom nejoblíbenější jazyk, nechte u tohoto nastavení výchozí hodnotu **1**. Pokud chcete zobrazit všechny jazyky, nastavte hodnotu **0**.|  

#### <a name="report-links"></a>Odkazy na sestavy  
 Tato sestava obsahuje odkazy na následující sestavu, která poskytuje další informace o vybrané položce.  

|Report Name|Podrobnosti|  
|-----------------|-------------|  
|**Podrobnosti o počítači**|Kliknutím na název počítače zobrazíte možnosti napájení, nastavení napájení a použitá schémata napájení pro vybraný počítač.<br /><br /> Další informace najdete v části [Computer Details Report](#BKMK_Computer_Details) tohoto tématu.|  
