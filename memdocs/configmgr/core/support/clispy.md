---
title: Klientský Spy
titleSuffix: Configuration Manager
description: Pomocí klienta Spy můžete řešit problémy s distribucí softwaru, inventářem a měřením softwaru na Configuration Manager klientech.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723429"
---
# <a name="client-spy"></a>Klientský Spy

*Platí pro: Configuration Manager (Current Branch)*

Klient Spy je jedním z [nástrojů Configuration Manager](tools.md). Jedná se o nástroj pro řešení potíží s distribucí softwaru, inventářem a měřením softwaru v Configuration Managerch klientech. 

Většina informací získaných nástrojem se týká nasazení softwaru:
- Všechna aktuální nasazení softwaru 
- Historie distribuce softwaru
- Konfigurace mezipaměti klienta
- Položky v mezipaměti
- Nedokončená požadovaná nasazení
- Dostupná nasazení  

Zobrazuje taky následující informace o inventáři.
- Nejnovější datum cyklu inventarizace
- Datum poslední sestavy
- Hlavní a dílčí verze inventáře softwaru
- Kolekce souborů
- Inventář hardwaru
- Kolekce IDMIF
- Záznamy dat zjišťování (DDR) 

Zobrazují se také pravidla monitorování míry využívání softwaru. 

> [!Note]   
> Pro zvýšení výkonu nástroj shromažďuje pouze informace o jednotlivých kartách při jejich výběru. Podobně platí, že když kliknete na **aktualizovat**, aktualizuje se jenom informace pro aktuálně zobrazenou kartu.



## <a name="usage"></a>Využití


### <a name="tools-menu"></a>Nabídka nástroje

V nabídce **nástroje** jsou k dispozici následující akce:  

#### <a name="connect"></a>Připojit
Načte informace z jiného počítače.  

- Nástroj ve výchozím nastavení zobrazuje informace z aktuálního počítače. 

- Připojte se pomocí názvu vzdáleného počítače, uživatelského jména a hesla k účtu. Nástroj vytvoří připojení ke sdílené složce IPC $ na vzdáleném počítači. Odstraní připojení, když nástroj opustí nebo když se připojíte k jinému počítači.  

- K získání informací vyžaduje účet s dostatečnými oprávněními.  

- Pokud nezadáte uživatelské jméno a heslo, klient Spy použije kontext zabezpečení aktuálně přihlášeného uživatele a pokusí se vytvořit připojení.  

- Když se připojíte ke vzdálenému počítači, zobrazí se na všech zobrazených kartách informace ze vzdáleného počítače.

#### <a name="software-distribution"></a>Distribuce softwaru
Zobrazí karty [distribuce softwaru](#software-distribution) a skryje ostatní karty. Ve výchozím nastavení klient Spy zobrazuje karty distribuce softwaru.

#### <a name="inventory"></a>Inventarizace
Zobrazí kartu inventář a skryje ostatní karty.

#### <a name="software-metering"></a>Měření softwaru
Zobrazí kartu monitorování míry využívání softwaru a skryje ostatní karty.

#### <a name="save-current-tab-to-file"></a>Uložit aktuální kartu do souboru
Uloží informace na kartě aktuálně zobrazené do textového souboru, který určíte. 

#### <a name="save-all-tabs-to-file"></a>Uložit všechny karty do souboru
Uloží informace na všech kartách do textového souboru, který zadáte. Ukládá jenom informace, které váš účet uvidí.



## <a name="software-distribution-tab"></a>Karta distribuce softwaru

Nakonfigurujte nastavení na následujících čtyřech kartách:
- [Žádosti o spuštění distribuce softwaru](#bkmk_exec-requests)
- [Historie distribuce softwaru](#bkmk_history)
- [Informace o mezipaměti distribuce softwaru](#bkmk_cache-info)
- [Nedokončená spuštění distribuce softwaru](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a>Žádosti o spuštění distribuce softwaru

Tato karta zobrazuje všechna existující nasazení, včetně nasazení cílených na zařízení i pro uživatele.

Každá položka stromu na kartě žádosti o spuštění distribuce softwaru obsahuje následující čtyři atributy:
- ID inzerce. Tato hodnota může být prázdná, pokud se jedná o dostupné nasazení. 
- ID balíčku 
- Název programu 
- Uživatelský. Může to být cílový identifikátor SID uživatele nebo identifikátor SID uživatele, který žádost inicioval. Pokud se jedná o systémové požadavky, zobrazený uživatel je systém. 

U každé žádosti o spuštění se ve struktuře podstromu zobrazí taky tyto informace:
- Název programu 
- ID balíčku 
- Název balíčku 
- Čas vytvoření žádosti 
- Stav 
- Běžící stav, pokud je spuštěný stav 
- Kontext spuštění (uživatel nebo správce) 
- Stav historie (úspěch, selhání nebo NotRun) 
- LastRunTime (nikdy, pokud se program nespustil) 
- RetryCount, pokud je stav WaitingRetry 
- ContentAccess (počet opakování, pokud je stav WaitingRetry) 
- FailureCode, pokud je stav WaitingRetry 
- FailureReason, pokud je stav WaitingRetry 

Pokud požadavek vyžaduje obsah, je stav WaitingContent. Na kartě informace o mezipaměti distribuce softwaru se zobrazují podrobnosti o této žádosti o stažení.

Pokud je požadavek na stažení požadavek na stažení, zobrazí se také počet stažených bajtů.

> [!Note]   
> Používá různé ikony pro různé stavy žádosti o spuštění.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a>Historie distribuce softwaru

Tato karta obsahuje informace o všech dříve spuštěných programech. Tyto informace jsou uloženy v registru.

Hlavní větve tohoto stromu jsou různé historie uživatelů, včetně systému. Zobrazuje podstrom obsahující seznam balíčků, ze kterých byly spuštěny programy pro každého uživatele. 

ID balíčku a název balíčku pro každý podstrom balíčku zobrazují seznam programů, které mají běžet. Pro každý z nich se zobrazí následující atributy: 
- Název programu
- Stav spuštění
- Čas posledního spuštění
- Kód chyby
- Důvod selhání  

Kód chyby a důvod selhání jsou při úspěšném spuštění programu prázdné.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a>Informace o mezipaměti distribuce softwaru

#### <a name="cache-config"></a>Konfigurace mezipaměti
Obsahuje informace o Configuration Manager mezipaměti klienta. Tyto informace zahrnují umístění mezipaměti, velikost mezipaměti a to, jestli se právě používá. 

#### <a name="cached-items"></a>Položky v mezipaměti
Obsahuje podstrom všech položek, které jsou aktuálně uloženy v mezipaměti. Každá položka stromu obsahuje následující informace o každé položce: 
- Umístění položky (složka) v mezipaměti
- Aktuální stav
- ID balíčku
- Název balíčku
- Verze balíčku
- Velikost balíčku
- Aktuální počet odkazů
- Čas posledního odkazovaného času (UTC)  

#### <a name="downloading-items"></a>Stahování položek
Jedná se o položky, které klient aktuálně stahuje. Každé z nich zobrazuje stejné informace zobrazené v položkách v mezipaměti a počet stažených kilobajtů. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a>Nedokončená spuštění distribuce softwaru

Tato karta obsahuje informace, které obsahují podrobnosti o minulých a budoucích požadovaných nasazeních a seznam dostupných nasazení.

Každá větev stromu je určena pro každý uživatelský účet s dostupnými nasazeními, včetně systému.

Pro každého uživatele dílčí strom obsahuje následující tři položky:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Povinná inzerce s budoucím prováděním
Jedná se o povinná inzerování, která stále mají spuštěné programy. Může se jednat o opakovanou, jednorázovou nebo více časovým oznámením. Každý zobrazuje ID inzerce, čas dalšího spuštění a plán, ve kterém je reklama spuštěná. 

#### <a name="optional-advertisements"></a>Volitelná inzerce
Zobrazí seznam všech publikovaných reklam. Zobrazuje také podrobnosti, jako je ID inzerce, název programu a název balíčku pro každou z nich. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Předchozí povinná inzerce bez budoucího naplánovaného spuštění
Toto je seznam reklam, které existují v klientovi, které nemají naplánované spouštění v budoucích programech. Zobrazí se ID inzerce, název balíčku a název programu. Pro všechny reklamy, které jsou volitelné, se zobrazí položka podstromu.

> [!Note]  
> Informace o názvu balíčku jsou k dispozici pouze pro balíčky, které mají k nim přidruženy inzerované zásady na počítači, který je právě zobrazován. Balíčky, pro které už nejsou k dispozici dostupné zásady, zobrazují zprávu "název balíčku už není dostupný".  



## <a name="inventory-tab"></a>Karta inventář

K dispozici je pouze jedna karta obsahující informace o inventáři. Hlavní strom obsahuje následující pět položek:  

- **Inventář softwaru**: obsahuje datum, kdy poslední cyklus začalo, datum poslední sestavy a vedlejší a hlavní verze poslední sestavy.  

- **Kolekce souborů**: obsahuje datum, kdy poslední cyklus začalo, datum poslední sestavy a vedlejší a hlavní verze poslední sestavy.  

- **Inventář hardwaru**: obsahuje datum, kdy poslední cyklus začalo, datum poslední sestavy a vedlejší a hlavní verze poslední sestavy.  

- **IDMIF Collection**: obsahuje datum, kdy poslední cyklus začalo, datum poslední sestavy a vedlejší a hlavní verze poslední sestavy.  

- **DDR**: obsahuje datum, kdy poslední cyklus začala, datum poslední sestavy a vedlejší a hlavní verze poslední sestavy. Informace DDR se také zobrazí v podstromu.



## <a name="software-metering-tab"></a>Karta měření softwaru

Tato karta zobrazuje informace jako podstrom a zahrnuje všechna pravidla monitorování míry využívání softwaru. Zobrazuje všechna pravidla jako uzel, který identifikuje název souboru a ID pravidla. Rozbalíte všechny uzly ve stromové struktuře a zobrazíte následující informace:
- Název souboru Průzkumníka 
- Původní název souboru
- ID pravidla
- Verze souboru
- Jazyk


