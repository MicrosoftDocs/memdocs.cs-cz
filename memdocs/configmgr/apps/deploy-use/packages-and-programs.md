---
title: Balíčky a programy
titleSuffix: Configuration Manager
description: Podporují nasazení, která používají starší balíčky a programy s Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c87ae35fa3e5a76c57342a0d1cad4167b0f14685
ms.sourcegitcommit: e43e6e83e3b38137ceebc6d299eacd94a925db85
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88895961"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Balíčky a programy v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager nadále podporuje balíčky a programy, které se používaly v Configuration Manager 2007. Nasazení využívající balíčky a programy může být vhodnější než aplikace při nasazení některého z následujících nástrojů nebo skriptů:  

- Nástroje pro správu, které neinstalují aplikaci na počítač
- "Jednorázové" skripty, které není potřeba průběžně monitorovat  
- Skripty, které se spouštějí podle opakovaného plánu a nemůžou používat globální vyhodnocení

> [!TIP]  
> Zvažte použití funkce [skripty](create-deploy-scripts.md) v konzole Configuration Manager. Skripty můžou být vhodnějším řešením pro některé z předchozích scénářů namísto použití balíčků a programů.

Když migrujete balíčky ze starší verze Configuration Manager, můžete je nasadit v hierarchii Configuration Manager. Po dokončení migrace se balíčky zobrazí v uzlu **Balíčky** v pracovním prostoru **Softwarová knihovna**.

Tyto balíčky můžete upravovat a nasazovat stejným způsobem jako při použití distribuce softwaru. **Průvodce importem balíčku z definice** zůstává v Configuration Manager pro import starších balíčků. Inzerce se při migraci z Configuration Manager 2007 do hierarchie Configuration Manager převede na nasazení.  

> [!NOTE]  
> Pomocí nástroje Package Conversion Manager můžete převést balíčky a programy na aplikace Configuration Manager.  
>
> Počínaje verzí 1806 je správce převodu balíčků integrovaný do Configuration Manager. Další informace najdete v tématu [Package Conversion Manager](../pcm/package-conversion-manager.md).  

Balíčky můžou využívat některé nové funkce Configuration Manager, včetně skupin distribučních bodů a monitorování. Aplikace Microsoft Application Virtualization (App-V) nelze nasadit s balíčky a programy v Configuration Manager. Pokud chcete distribuovat virtuální aplikace, vytvořte je jako aplikace Configuration Manager. Další informace najdete v tématu [nasazení virtuálních aplikací App-V](../get-started/deploying-app-v-virtual-applications.md).  


## <a name="create-a-package-and-program"></a>Vytvoření balíčku a programu

### <a name="use-the-create-package-and-program-wizard"></a>Použití Průvodce vytvořením balíčku a programu

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **balíčky** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** klikněte na možnost **vytvořit balíček**.  

3. Na stránce **balíček** v **Průvodci vytvořením balíčku a programu**zadejte následující informace:  

    - **Název**: zadejte název balíčku, který má maximálně 50 znaků.  

    - **Popis**: zadejte popis tohoto balíčku o maximální 128 znaků.  

    - **Výrobce** (volitelné): zadejte název výrobce, který vám usnadní identifikaci balíčku v konzole Configuration Manager. Název nesmí být delší než 32 znaků.

    - **Jazyk** (volitelné): zadejte jazykovou verzi balíčku, která má maximálně 32 znaků.  

    - **Verze** (volitelné): zadejte číslo verze balíčku, který má maximálně 32 znaků.

    - **Tento balíček obsahuje zdrojové soubory**: Toto nastavení určuje, jestli balíček vyžaduje, aby se na klientských zařízeních nacházely zdrojové soubory. Ve výchozím nastavení Průvodce tuto možnost nepovolí a Configuration Manager nepoužívá distribuční body pro balíček. Když vyberete tuto možnost, zadejte obsah balíčku pro distribuci do distribučních bodů.  

    - **Zdrojová složka**: Pokud balíček obsahuje zdrojové soubory, zvolte **Procházet** a otevřete dialogové okno **nastavit zdrojovou složku** a zadejte umístění zdrojových souborů pro daný balíček.  

        > [!NOTE]  
        > Účet počítače serveru lokality musí mít k zadané zdrojové složce oprávnění pro čtení.
        >
        > Systém Windows omezuje cestu ke zdroji na 256 znaků nebo méně. Toto omezení platí pro zdroj balíčku i pro aplikace. Další informace najdete v tématu [pojmenování souborů, cest a oborů názvů](/windows/win32/fileio/naming-a-file).

    - Pokud chcete v klientovi předem ukládat obsah do mezipaměti, začněte ve verzi 1906 a určete **architekturu** a **jazyk** balíčku. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. Na stránce **typ programu** v **Průvodci vytvořením balíčku a programu**vyberte typ programu, který chcete vytvořit, a pak zvolte **Další**. Můžete vytvořit program pro [počítač](#create-a-standard-program) nebo [zařízení](#create-a-device-program), nebo můžete tento krok přeskočit a vytvořit program později.  

    > [!TIP]  
    > Pokud chcete vytvořit nový program pro existující balíček, nejdřív vyberte balíček. Pak na kartě **Domů** ve skupině **balíček** zvolte možnost **vytvořit program** . otevře se **Průvodce vytvořením programu**.  

#### <a name="create-a-standard-program"></a>Vytvořit standardní program

1. Na stránce **typ programu** v **Průvodci vytvořením balíčku a programu**zvolte možnost **standardní program**a klikněte na tlačítko **Další**.  

2. Na stránce **standardní program** zadejte následující informace:  

    - **Název** – Zdejte název programu. Název nesmí být delší než 50 znaků.  

        > [!NOTE]  
        > Název programu musí být v rámci balíčku jedinečný. Po vytvoření programu nelze změnit jeho název.  

    - **Příkazový řádek**: Zadejte příkazový řádek, který se má použít ke spuštění tohoto programu, nebo klikněte na tlačítko **Procházet** a přejděte do umístění souboru.  

        Pokud nezadáte příponu pro název souboru, Configuration Manager se pokusí použít. com,. exe a. bat jako možná rozšíření.  

        Když klient spustí program, Configuration Manager vyhledá soubor v následujících umístěních:

        - V rámci balíčku
        - Místní složka systému Windows
        - Místní *cesta% Path%*

        Pokud soubor nenalezne, program se nezdařil.  

    - **Spouštěcí složka** (volitelné): zadejte složku, ze které se program spouští, maximálně 127 znaků. Tato složka může být absolutní cesta na straně klienta. Může to být také cesta, která je relativní vzhledem ke složce distribučního bodu obsahující balíček.

    - **Spustit**: Zadejte režim, ve kterém se program spustí na klientských počítačích. Vyberte jednu z následujících možností:  

        - **Normální**: program se spouští v normálním režimu založeném na výchozím nastavení systému a programu. Tento režim je výchozí.  

        - **Minimalizovaný**: program se spouští na klientských zařízeních minimalizovaně. Uživatelé můžou v oznamovací oblasti nebo na hlavním panelu zobrazit aktivitu instalace.  

        - **Maximalizováno**: program se spustí na klientských zařízeních v maximalizovaném okně. Uživatelům se zobrazí všechny aktivity instalace.  

        - **Skryté**: program běží na klientských zařízeních jako skrytý. Uživatelům se nezobrazí žádná aktivita instalace.  

    - **Program lze spustit**: Určete, jestli se program spustí, jenom když je uživatel přihlášený, jenom když není přihlášený žádný uživatel nebo bez ohledu na to, jestli je uživatel přihlášený ke klientskému počítači.  

    - **Režim spuštění**: Určete, jestli se program spouští s oprávněními správce nebo s oprávněními uživatele, který je aktuálně přihlášený.  

    - **Umožněte uživatelům zobrazení a interakci s instalací programu**: Toto nastavení použijte, pokud je k dispozici, a určete, jestli chcete uživatelům dovolit pracovat s instalací programu. Tato možnost je dostupná jenom v případě, že jsou splněné následující podmínky:

        - Nastavení **programu lze spustit** **pouze v případě, že není přihlášen žádný uživatel nebo bez** ohledu na **to, zda je uživatel přihlášen** .
        - Nastavení **režimu spuštění** se **spouští s právy správce** .  

    - **Režim jednotky**: zadejte informace o tom, jak se tento program v síti spouští. Zvolte jednu z následujících možností:  

        - **Spouští se s názvem UNC**: Určuje, jestli se program spouští s názvem UNC (Universal Naming Convention). Toto nastavení je výchozí.  

        - **Vyžaduje písmeno jednotky**: Určete, že program vyžaduje písmeno jednotky, aby plně způsobilo jeho umístění. V případě tohoto nastavení může Configuration Manager na klientovi použít jakékoli dostupné písmeno jednotky.  

        - **Vyžaduje konkrétní písmeno jednotky**: Určete, že program vyžaduje konkrétní písmeno jednotky, které určíte, aby plně způsobilo jeho umístění. Například **Z:**. Pokud klient již používá zadané písmeno jednotky, program se nespustí.  

    - Při **přihlášení znovu připojit k distribučnímu bodu**: Určete, zda se klient znovu připojí k distribučnímu bodu, když se uživatel přihlásí. Ve výchozím nastavení Průvodce tuto možnost nepovoluje.

3. Na stránce **požadavky** v **Průvodci vytvořením balíčku a programu** zadejte následující informace:  

    - **Nejprve spustit jiný program**: Identifikujte balíček a program, který se spustí před spuštěním tohoto balíčku a programu.  

    - **Požadavky na platformu**: vyberte **Tento program může běžet na libovolné platformě** nebo **Tento program může běžet pouze na zadaných platformách**. Pak zvolte verze operačních systémů, které musí klienti nainstalovat k instalaci tohoto balíčku a programu.  

    - **Odhadované místo na disku**: zadejte množství místa na disku, které program vyžaduje ke spuštění v počítači. Výchozí nastavení je **neznámé**. V případě potřeby zadejte celé číslo větší nebo rovno nule. Pokud nastavíte hodnotu, vyberte také jednotky pro danou hodnotu.  

    - **Maximální povolená doba běhu (v minutách)**: Určete maximální dobu, po kterou se očekává, že program bude běžet na klientském počítači. Výchozí hodnota je **120** minut. Používejte pouze celá čísla větší než nula.  

        > [!IMPORTANT]  
        > Pokud používáte časová období údržby ve stejné kolekci, do které nasadíte tento program, může dojít ke konfliktu, pokud je **maximální povolená doba běhu** delší než plánované časové období údržby. Pokud nastavíte maximální dobu běhu na **neznámou**, program se spustí během časového období údržby. Po zavření okna údržby pak bude i nadále běžet podle potřeby. Pokud nastavíte maximální dobu běhu na určitou dobu, která je větší než délka jakéhokoli dostupného časového období údržby, klient nespustí program.  

        Pokud nastavíte tuto hodnotu jako **neznámou**, Configuration Manager nastaví maximální povolenou dobu běhu na 12 hodin (720 minut).  

        > [!NOTE]  
        > Pokud program překračuje maximální dobu běhu, Configuration Manager ho zastaví, pokud jsou splněné následující podmínky:
        >
        > - Povolíte možnost **Spustit s právy správce** .
        > - Nepovolíte možnost **Povolit uživatelům zobrazení a interakci s instalací programu.**  

#### <a name="create-a-device-program"></a>Vytvoření programu zařízení  

1. Na stránce **typ programu** v **Průvodci vytvořením balíčku a programu**vyberte **program pro zařízení**a potom zvolte **Další**.  

2. Na stránce **program pro zařízení** zadejte následující nastavení:  

    - **Název**: zadejte název programu, který může být delší než 50 znaků.  

        > [!NOTE]  
        > Název programu musí být v rámci balíčku jedinečný. Po vytvoření programu nelze změnit jeho název.  

    - **Komentář** (volitelné): Zadejte komentář pro tento program zařízení s maximálně 127 znaky.  

    - **Složka ke stažení**: zadejte název složky na zařízení, kam budou ukládat zdrojové soubory balíčku. Výchozí hodnota je `\Temp\`.  

    - **Příkazový řádek**: Zadejte příkazový řádek, který se má použít ke spuštění tohoto programu. Chcete-li přejít do umístění souboru, klikněte na tlačítko **Procházet**.  

    - **Spusťte příkazový řádek ve složce pro stahování**: tuto možnost vyberte, pokud chcete program spustit ze složky pro stahování.  

    - **Spustit příkazový řádek z této složky**: tuto možnost vyberte, pokud chcete zadat jinou složku, ze které se má program spustit.  

3. Na stránce **požadavky** zadejte následující nastavení:  

    - **Odhadované místo na disku**: zadejte množství místa na disku, které je nutné pro daný software. Klient zobrazí tuto hodnotu uživatelům mobilních zařízení před instalací programu.  

    - **Stáhnout program**: zadejte informace o tom, kdy může mobilní zařízení tento program stáhnout. Můžete zadat **Co nejdříve**, **Jen přes rychlou síť** nebo **Pouze když je zařízení ukotveno**.  

    - **Další požadavky**: Určete všechny další požadavky pro tento program. Uživatelé tyto požadavky uvidí před instalací softwaru. Můžete třeba uživatele upozornit, že před spuštěním programu musí ukončit všechny ostatní aplikace.  

## <a name="deploy-packages-and-programs"></a>Nasazení balíčků a programů  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **balíčky** .  

2. Vyberte balíček, který chcete nasadit. Na kartě **Domů** na pásu karet ve skupině **nasazení** klikněte na možnost **nasadit**.  

3. Na stránce **Obecné** v nástroji **Průvodce nasazením softwaru**zadejte název balíčku a programu, který chcete nasadit. Vyberte kolekci, do které chcete balíček a program nasadit, a jakékoli volitelné komentáře.  

    Chcete-li uložit obsah balíčku do výchozí skupiny distribučních bodů kolekce, vyberte možnost **použít výchozí skupiny distribučních bodů přidružené k této kolekci**. Pokud jste tuto kolekci nepřiřadili ke skupině distribučních bodů, tato možnost není k dispozici.  

4. Na stránce **obsah** klikněte na tlačítko **Přidat**. Vyberte distribuční body nebo skupiny distribučních bodů, do kterých chcete distribuovat obsah pro tento balíček a program.  

5. Na stránce **nastavení nasazení** nakonfigurujte následující nastavení:  

    - **Účel**: vyberte jednu z následujících možností:

        - **K dispozici**: uživatel uvidí publikovaný balíček a program v centru softwaru a může je nainstalovat na vyžádání.  

        - **Požadováno**: balíček a program se nasadí automaticky podle nakonfigurovaného plánu. V centru softwaru můžete sledovat stav nasazení a nainstalovat ho před konečným termínem.  

        > [!NOTE]
        > Pokud se do zařízení přihlásí více uživatelů, nemusí se nasazení balíčku a pořadí úkolů zobrazit v centru softwaru.

    - **Odeslat pakety pro probuzení**: Pokud nastavíte účel nasazení na **požadováno** a vyberete tuto možnost, lokalita nejprve odešle paket pro probuzení do počítačů v konečném termínu instalace. Než budete moct použít tuto možnost, nakonfigurujte počítače pro Wake On LAN. Další informace najdete v tématu [Postup konfigurace funkce Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Umožňuje klientům v měřeném připojení k internetu stahovat obsah po uplynutí konečného termínu instalace, což může způsobit další náklady.**  

    > [!NOTE]  
    > Když nasadíte balíček a program, možnost **předem nasadit software na primární zařízení uživatele** není k dispozici.  

6. Na stránce **plánování** nakonfigurujte, kdy se má tento balíček a program nasadit na klientská zařízení.  

    Možnosti na této stránce se liší v závislosti na tom, zda jste nastavili akci nasazení na hodnotu **k dispozici** nebo **požadováno**.  

    U **požadovaných** nasazení nakonfigurujte chování při opětovném spuštění programu z rozevírací nabídky chování při opětovném **spuštění** . Vybírat můžete z těchto možností:  

    | Chování při spuštění | Popis |
    |----------------|-------------|
    | **Nikdy znovu nespouštět nasazený program** | Klient nebude program znovu spouštět. K tomuto chování dochází i v případě, že se program původně nezdařil nebo se změnily soubory programu. |
    | **Vždy znovu spustit program** | Klient vždy znovu spustí program, když je naplánováno nasazení. K tomuto chování dochází i v případě, že byl program již úspěšně spuštěn. Při aktualizaci programu je to užitečné při opakovaném nasazení. |
    | **Spustit znovu, pokud se předchozí pokus nezdařil** | Klient spustí program znovu po naplánování nasazení, a to pouze v případě, že při předchozím pokusu o spuštění došlo k chybě. |
    | **Znovu spustit, pokud se pokus při předchozím pokusu podařil** | Klient znovu spustí program pouze v případě, že byl dříve úspěšně spuštěn na klientovi. Toto chování je užitečné při opakovaném nasazení, když program pravidelně aktualizujete a každá aktualizace vyžaduje úspěšnou instalaci předchozí aktualizace. |

7. Na stránce **Činnost koncového uživatele** zadejte následující informace:  

    - **Umožňuje uživatelům spustit program nezávisle na přiřazení**: uživatelé můžou tento software instalovat z centra softwaru bez ohledu na naplánovanou dobu instalace.  

    - **Instalace softwaru**: Umožňuje instalaci softwaru mimo nakonfigurovaná časová období údržby.  

    - **Restart systému (Pokud je to nutné pro dokončení instalace)**: Pokud instalace softwaru vyžaduje, aby se restart zařízení dokončí, nechte tuto akci probíhat mimo nakonfigurované časové intervaly pro správu a údržbu.  

    - **Vložená zařízení**: při nasazení balíčků a programů do zařízení se systémem Windows Embedded s povolenými filtry zápisu můžete určit, že budou instalovat balíčky a programy v dočasném překrytí a později provést změny. Případně potvrďte změny v termínu instalace nebo během časového období údržby. Pokud provedete změny v konečném termínu instalace nebo během časového období údržby, je nutné restartovat počítač a změny budou v zařízení uchovány.  

        > [!NOTE]  
        > Při nasazení balíčku nebo programu do zařízení se systémem Windows Embedded se ujistěte, že je zařízení členem kolekce, která má nakonfigurované časové období údržby. Další informace o způsobu použití časových období údržby při nasazování balíčků a programů do zařízení se systémem Windows Embedded najdete v tématu [vytváření aplikací pro Windows Embedded](../get-started/creating-windows-embedded-applications.md).  

8. Na stránce **Distribuční body** zadejte následující informace:  

    - **Možnosti nasazení**: Zadejte akci, kterou klient používá při použití distribučního bodu v aktuální skupině hranic. Vyberte také akci klienta, pokud používá distribuční bod ze sousední skupiny hranic nebo výchozí skupiny hranic lokality.

        > [!IMPORTANT]  
        > Pokud nakonfigurujete možnost nasazení tak, aby **spouštěla program z distribučního bodu**, Nezapomeňte povolit možnost **Kopírovat obsah tohoto balíčku do sdílené složky balíčků v distribučních bodech** na kartě **přístup k datům** ve vlastnostech balíčku. V opačném případě je balíček nedostupný pro spuštění z distribučních bodů.  

    - **Povolit klientům používat distribuční body z výchozí skupiny hranic lokality**: Pokud tento obsah není k dispozici z libovolného distribučního bodu v aktuální nebo sousední skupině hranic, povolte tuto možnost, aby vyzkoušela distribuční body ve výchozí skupině hranic lokality.

9. Dokončete průvodce.  

Nasazení můžete zobrazit v uzlu **nasazení** v pracovním prostoru **monitorování** a v podokně podrobností na kartě nasazení balíčku, když vyberete nasazení. Další informace najdete v tématu [monitorování balíčků a programů](#monitor-packages-and-programs).  


## <a name="monitor-packages-and-programs"></a>Monitorování balíčků a programů

K monitorování nasazení balíčků a programů použijte stejné postupy, které můžete použít k monitorování aplikací, jak je popsáno v části [monitorování aplikací](monitor-applications-from-the-console.md).  

Balíčky a programy zahrnují také řadu předdefinovaných sestav, které umožňují monitorovat informace o stavu nasazení balíčků a programů. Tyto sestavy mají kategorii sestav **Distribuce softwaru – balíčky a programy** a **Distribuce softwaru – stav nasazení balíčků a programů**.  

Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).  


## <a name="manage-packages-and-programs"></a>Správa balíčků a programů

V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **balíčky** . Vyberte balíček, který chcete spravovat, a pak vyberte úlohu správy.  

### <a name="create-prestage-content-file"></a>Vytvořit soubor připraveného obsahu

Otevře **Průvodce vytvořením souboru připraveného obsahu**, který vytvoří soubor, který obsahuje obsah balíčku. Tento soubor použijte k ručnímu importu balíčku do vzdáleného distribučního bodu. Tato akce je užitečná, když máte malou šířku pásma sítě mezi serverem lokality a distribučním bodem.

### <a name="create-program"></a>Vytvořit program

Otevře **Průvodce vytvořením programu**, který vytvoří nový program pro tento balíček.

### <a name="export"></a>Export

Otevře **Průvodce exportem balíčku**, který umožňuje exportovat vybraný balíček a jeho obsah do souboru. Tento soubor použijte k importu souboru do jiné hierarchie.

Informace o importu balíčků a programů najdete v tématu věnovaném [vytváření balíčků a programů](#create-a-package-and-program).

### <a name="deploy"></a>Nasazení

Otevře se **Průvodce nasazením softwaru**, který umožňuje nasadit vybraný balíček a program do kolekce. Další informace najdete v tématu [nasazení balíčků a programů](#deploy-packages-and-programs).

### <a name="distribute-content"></a>Distribuovat obsah

Otevře **Průvodce distribucí obsahu**, který odešle obsah balíčku a programu do vybraných distribučních bodů nebo skupin distribučních bodů.

### <a name="update-distribution-points"></a>Aktualizace distribučních bodů

Aktualizuje distribuční body o nejnovější obsah pro vybraný balíček a program.


## <a name="see-also"></a>Viz také

- [Skripty](create-deploy-scripts.md)

- [Package Conversion Manager](../pcm/package-conversion-manager.md)

- [Definiční soubory balíčků](package-definition-files.md)
