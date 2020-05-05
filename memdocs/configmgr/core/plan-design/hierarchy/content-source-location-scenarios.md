---
title: Umístění zdroje obsahu
titleSuffix: Configuration Manager
description: Přečtěte si o nastaveních Configuration Manager, která klientům umožňují najít obsah v pomalých sítích.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720237"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Scénáře umístění zdroje obsahu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Před verzí 1610 Configuration Manager podporovaná několik nastavení, která spolu definují, jak a kde klienti hledají obsah, když se nacházejí v pomalé síti. Možné kombinace mají vliv na používání klientů umístění obsahu a to, jestli můžou úspěšně použít záložní umístění, když upřednostňovaný zdroj obsahu není dostupný.  

> [!IMPORTANT]  
> **Pokud vaše weby používají verzi 1511, 1602 nebo 1606**, informace v tomto tématu se vztahují na vaši infrastrukturu. Viz také [skupiny hranic pro verze 1511, 1602 a 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) pro informace, které jsou specifické pro skupiny hranic v těchto verzích Configuration Manager.
>
> **Pokud vaše weby používají verzi 1610 nebo novější**, použijte informace v části [definování hranic lokality a skupin hranic pro Configuration Manager](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) k pochopení, jak klienti hledají distribuční body s dostupným obsahem.





**Následující tři nastavení definují chování, když klienti požadují obsah:**

- **Povolit záložní umístění zdroje pro obsah** (povoleno nebo zakázáno): Jedná se o možnost, kterou lze povolit na kartě **skupiny hranic** v distribučním bodě. To umožňuje klientovi používat distribuční bod, který je nakonfigurován jako záložní umístění, pokud není obsah dostupný v upřednostňovaném distribučním bodě.  

  - **Chování nasazení pro rychlost síťového připojení**: každé nasazení je nakonfigurované s jedním z následujících chování, které se má použít, pokud je připojení k distribučnímu bodu pomalé:  

    -   **Stažení obsahu z distribučního bodu a jeho místní spuštění**  

    -   **Nestahovat obsah**: Tato možnost se používá pouze v případě, že klient používá záložní umístění k získání obsahu.  

    Rychlost připojení pro distribuční bod je nakonfigurovaná na kartě **odkazy** skupiny hranic a je specifická pro tuto skupinu hranic.  

  - **Distribuce balíčku na vyžádání** (do upřednostňovaných distribučních bodů): Tato možnost je povolená, když vyberete možnost **distribuovat obsah pro tento balíček do preferovaných distribučních bodů** na kartě **Nastavení distribuce** vlastností balíčku nebo aplikace. Pokud je tato možnost povolena, tato možnost nastaví Configuration Manager k automatickému zkopírování obsahu do preferovaného distribučního bodu, který ještě nemá obsah poté, co klient požaduje obsah z tohoto distribučního bodu.  


 **Pro všechny scénáře platí následující požadavky:**


-   Obsah je dostupný v záložním distribučním bodě.  

-   Distribuční body jsou online a přístupné  


## <a name="scenario-1"></a>Scénář 1  
 Platí v případě, že existují následující konfigurace:  

-   **Obsah je dostupný v upřednostňovaném distribučním bodě**  

-   **Povolit zálohu**: není povoleno  

-   **Chování nasazení pro pomalou síť**: jakákoli konfigurace  


**Podrobnosti:** (konfigurace pro distribuci balíčku na vyžádání není v tomto scénáři relevantní.)  

1.  Klient odešle požadavek na obsah do bodu správy.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body, které obsah obsahují.  

3.  Klient stáhne obsah z preferovaného distribučního bodu v seznamu.  

## <a name="scenario-2"></a>Scénář 2  
 Existují následující konfigurace:  

-   **Obsah je dostupný v upřednostňovaném distribučním bodě**  

-   **Povolit zálohu**: povoleno  

-   **Chování nasazení pro pomalou síť**: Nestahovat obsah  


**Podrobnosti:** (konfigurace pro distribuci balíčku na vyžádání není v tomto scénáři relevantní.)  

1.  Klient odešle požadavek na obsah do bodu správy. Klient obsahuje příznak s požadavkem, který označuje, že záložní distribuční body jsou povoleny.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body a záložními distribučními body, které obsah obsahují.  

3.  Klient stáhne obsah z preferovaného distribučního bodu v seznamu.  

## <a name="scenario-3"></a>Scénář 3  
 Existují následující konfigurace:  

-   **Obsah je dostupný v upřednostňovaném distribučním bodě**  

-   **Povolit zálohu**: povoleno  

-   **Chování nasazení pro pomalou síť**: stáhnout a nainstalovat obsah  


**Podrobnosti:** (konfigurace pro distribuci balíčku na vyžádání není v tomto scénáři relevantní.)  

1.  Klient odešle požadavek na obsah do bodu správy. Klient obsahuje příznak s požadavkem, který označuje, že záložní distribuční body jsou povoleny.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body a záložními distribučními body, které obsah obsahují.  

3.  Klient stáhne obsah z preferovaného distribučního bodu v seznamu.  

## <a name="scenario-4"></a>Scénář 4  
 Existují následující konfigurace:  

-   **Obsah není v upřednostňovaném distribučním bodě k dispozici.**  

-   **Distribuovat obsah pro tento balíček do preferovaných distribučních bodů** není povolený.  

-   **Povolit zálohu**: není povoleno  

-   **Chování nasazení pro pomalou síť**: jakákoli konfigurace  


**Zobrazí**  

1.  Klient odešle požadavek na obsah do bodu správy.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body, které mají obsah. V seznamu nejsou žádné preferované distribuční body.  

3.  Klient se nezdařil, protože **obsah zprávy není k dispozici** a přejde do režimu opakování. Každou hodinu se spustí nový požadavek na obsah.  

## <a name="scenario-5"></a>Scénář 5  
 Existují následující konfigurace:  

-   **Obsah není v upřednostňovaném distribučním bodě k dispozici.**  

-   **Distribuovat obsah pro tento balíček do preferovaných distribučních bodů** není povolený.  

-   **Povolit zálohu**: povoleno  

-   **Chování nasazení pro pomalou síť**: Nestahovat obsah  


**Zobrazí**  

1.  Klient odešle požadavek na obsah do bodu správy. Klient obsahuje příznak s požadavkem, který označuje, že záložní distribuční body jsou povoleny.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body a záložními distribučními body, které mají obsah. K dispozici nejsou žádné upřednostňované distribuční body, které mají obsah, ale alespoň jeden záložní distribuční bod má obsah.  

3.  Obsah se nestáhne, protože vlastnost nasazení pro situaci, kdy klient používá záložní distribuční bod, je nastavená na **Nestahovat obsah** (který se používá, když se klienti vrátí k získání obsahu). Klient se nezdařil, protože **obsah zprávy není k dispozici** a přejde do režimu opakování. Klient vytvoří novou žádost o obsah každou hodinu.  

## <a name="scenario-6"></a>Scénář 6  
 Existují následující konfigurace:  

-   **Obsah není v upřednostňovaném distribučním bodě k dispozici.**  

-   **Distribuovat obsah pro tento balíček do preferovaných distribučních bodů** není povolený.  

-   **Povolit zálohu**: povoleno  

-   **Chování nasazení pro pomalou síť**: stáhnout a nainstalovat obsah  


**Zobrazí**  

1.  Klient odešle požadavek na obsah do bodu správy. Klient obsahuje příznak s požadavkem, který označuje, že jsou povoleny záložní distribuční body.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body a záložními distribučními body, které mají obsah. K dispozici nejsou žádné upřednostňované distribuční body, které obsahují obsah, ale alespoň jeden záložní distribuční bod s obsahem.  

3.  Obsah se stáhne z záložního distribučního bodu na seznamu, protože vlastnost Deployment pro, kdy klient používá záložní distribuční bod, je nastavená na **Stažení a instalaci obsahu**.  

## <a name="scenario-7"></a>Scénář 7  
 Existují následující konfigurace:  

-   **Obsah není v upřednostňovaném distribučním bodě k dispozici.**  

-   **Distribuovat obsah pro tento balíček do preferovaných distribučních bodů** je povolený.  

-   **Povolit zálohu**: není povoleno  

-   **Chování nasazení pro pomalou síť**: jakákoli konfigurace  


**Zobrazí**  

1.  Klient odešle požadavek na obsah do bodu správy.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body, které mají obsah. Neexistují žádné preferované distribuční body, které mají obsah.  

3.  Klient se nezdařil, protože **obsah zprávy není k dispozici** a přejde do režimu opakování. Každou hodinu se vytvoří nový požadavek na obsah.  

4.  Bod správy vytvoří aktivační událost správce distribuce pro distribuci obsahu do všech upřednostňovaných distribučních bodů pro klienta, který vytvořil požadavek na obsah.  

5.  Správce distribuce distribuuje obsah do všech preferovaných distribučních bodů. Ve většině případů je obsah úspěšně distribuován do upřednostňovaných distribučních bodů během hodiny.  

6.  Klient iniciuje nový požadavek na obsah do bodu správy.  

7.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body, které mají obsah. Klient stáhne obsah z preferovaného distribučního bodu v seznamu.  

## <a name="scenario-8"></a>Scénář 8  
 Existují následující konfigurace:  

-   **Obsah není v upřednostňovaném distribučním bodě k dispozici.**  

-   **Distribuovat obsah pro tento balíček do preferovaných distribučních bodů** je povolený.  

-   **Povolit zálohu**: povoleno  

-   **Chování nasazení pro pomalou síť**: Nestahovat obsah  


**Zobrazí**  

1.  Klient odešle požadavek na obsah do bodu správy. Klient obsahuje příznak s požadavkem, který označuje, že záložní distribuční body jsou povoleny.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body a záložními distribučními body, které mají obsah. K dispozici nejsou žádné upřednostňované distribuční body, které mají obsah, ale alespoň jeden záložní distribuční bod má obsah.  

3.  Obsah se nestáhne, protože vlastnost nasazení pro situaci, kdy klient používá záložní distribuční bod, je nastavená na **nestahovat**. Klient se nezdařil, protože **obsah zprávy není k dispozici** a přejde do režimu opakování. Klient vytvoří novou žádost o obsah každou hodinu.  

4.  Bod správy vytvoří aktivační událost správce distribuce pro distribuci obsahu do všech upřednostňovaných distribučních bodů pro klienta, který vytvořil požadavek na obsah.  

5.  Správce distribuce distribuuje obsah do všech preferovaných distribučních bodů. Ve většině případů je obsah úspěšně distribuován do upřednostňovaných distribučních bodů během hodiny.  

6.  Klient iniciuje nový požadavek na obsah do bodu správy.  

7.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body, které mají obsah.  

8.  Klient stáhne obsah z preferovaného distribučního bodu v seznamu.  

## <a name="scenario-9"></a>Scénář 9  
 Existují následující konfigurace:  

-   **Obsah není v upřednostňovaném distribučním bodě k dispozici.**  

-   **Distribuovat obsah pro tento balíček do preferovaných distribučních bodů** je povolený.  

-   **Povolit zálohu**: povoleno  

-   **Chování nasazení pro pomalou síť**: stáhnout a nainstalovat obsah  


**Zobrazí**  

1.  Klient odešle požadavek na obsah do bodu správy. Klient obsahuje příznak s požadavkem, který označuje, že záložní distribuční body jsou povoleny.  

2.  Seznam umístění obsahu je vrácen do klienta z bodu správy s upřednostňovanými distribučními body a záložními distribučními body, které mají obsah. K dispozici nejsou žádné upřednostňované distribuční body, které mají obsah, ale alespoň jeden záložní distribuční bod má obsah.  

3.  Obsah se stáhne z záložního distribučního bodu na seznamu, protože vlastnost Deployment pro, kdy klient používá záložní distribuční bod, je nastavená na **Stažení a instalaci obsahu**. Toto nastavení nasazení umožňuje klientovi, který musí použít záložní umístění obsahu, získat obsah z tohoto umístění.  

4.  Bod správy vytvoří aktivační událost správce distribuce pro distribuci obsahu do všech upřednostňovaných distribučních bodů pro klienta, který vytvořil požadavek na obsah.  

5.  Správce distribuce distribuuje obsah do všech preferovaných distribučních bodů, což umožňuje dalším klientům získat obsah bez použití záložního distribučního bodu.  
