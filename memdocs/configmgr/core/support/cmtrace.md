---
title: CMTrace
titleSuffix: Configuration Manager
description: Přečtěte si, jak používat nástroj CMTrace k zobrazení souborů protokolu pro Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723422"
---
# <a name="cmtrace"></a>CMTrace

*Platí pro: Configuration Manager (Current Branch)*

CMTrace je jedním z [nástrojů Configuration Manager](tools.md). Umožňuje zobrazit a monitorovat soubory protokolu, včetně těchto typů:  

- Soubory protokolu ve formátu Configuration Manager nebo Správce komponent klienta (CCM)  

- Jednoduché textové soubory ASCII nebo Unicode, například protokoly Instalační služba systému Windows  

Nástroj pomáhá analyzovat soubory protokolu zvýrazňováním, filtrováním a vyhledáváním chyb.

Počínaje verzí 1806 se nástroj pro prohlížení protokolu CMTrace automaticky nainstaluje spolu s klientem Configuration Manager. Přidá se do instalačního adresáře klienta, který je `%WinDir%\CCM\CMTrace.exe`ve výchozím nastavení.<!--1357971-->

> [!Note]  
> CMTrace není automaticky zaregistrován pro Windows, aby se otevřela Přípona souboru. log. Další informace najdete v tématu [přidružení souborů](#file-associations).  

Počínaje verzí 1906 je **OneTrace** nový prohlížeč protokolů s nástrojem Support Center. Funguje podobně jako CMTrace, s vylepšeními. Další informace najdete v tématu [Support Center OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Využití

Spusťte **CMTrace. exe**. Při prvním spuštění nástroje se zobrazí výzva k přidružení souboru. Další informace najdete v tématu [přidružení souborů](#file-associations).

Většinu akcí v CMTrace můžete provést z následujících nabídek:

- [Soubor](#file-menu)
- [Nástroje](#tools-menu)

### <a name="file-menu"></a>Nabídka Soubor

V nabídce **soubor** jsou k dispozici následující akce:  

- [Otevřít](#open)
- [Otevřít na serveru](#open-on-server)
- [Tisk](#print)
- [Předvolby](#preferences)

V nabídce soubor se zobrazí také posledních osm posledních souborů. Jedním z těchto protokolů se rychle znovu otevřete tak, že ho vyberete v nabídce soubor.

#### <a name="open"></a>Otevřít

Zobrazí dialogové okno otevřít, ve kterém můžete vyhledat soubor protokolu.

Filtrovat zobrazení souborů následujících typů:

- Soubory protokolu (\*. log)  
- Staré soubory protokolu (\*. LO_)
- Všechny soubory (\*.\*)

Ve výchozím nastavení nejsou vybrané tyto dvě možnosti:  

- **Ignorovat existující řádky**: Pokud je vybrána, CMTrace ignoruje stávající obsah vybraného souboru protokolu a zobrazí nové řádky pouze tak, jak jsou přidány. Tuto možnost použijte, chcete-li monitorovat pouze nové akce, pokud nepotřebujete úplnou historii souboru protokolu.  

- **Sloučit vybrané soubory**: Pokud tuto možnost povolíte a vyberete více než jeden soubor protokolu, CMTrace sloučí vybrané protokoly v zobrazení. Zobrazuje je, jako by se jedná o jeden soubor protokolu. Sloučený protokol aktualizuje stejné a podporuje všechny další funkce CMTrace, jako by se jedná o jeden soubor protokolu.  

#### <a name="open-on-server"></a>Otevřít na serveru

Přejděte do složky protokoly Configuration Manager v počítači systému lokality s dialogovým oknem standardní procházení. Můžete také procházet síť pro vzdálený počítač.

Když vyberete vzdálený počítač, který chcete procházet, CMTrace zkontroluje sdílenou složku Configuration Manager. Pokud se nedaří najít sdílenou složku se soubory protokolu Configuration Manager, zobrazí se chybová zpráva.  

Chcete-li se připojit přímo ke známému počítači bez procházení, použijte akci [otevřít](#open) . Pak zadejte název serveru a sdílenou složku pomocí formátu UNC.

#### <a name="print"></a>Tisk

Zobrazí dialogové okno standardní tisk v systému Windows. Tato akce pošle aktuální soubor protokolu na tiskárnu. Naformátuje výstup podle nastavení na kartě Tisk CMTrace předvoleb.

#### <a name="preferences"></a>Předvolby

Nakonfigurujte nastavení pro CMTrace. K dispozici jsou následující možnosti:  

- Karta **Obecné**  

    - **Interval aktualizace**: Určuje, jak často CMTrace kontroluje změny v souborech protokolů a načítá nové řádky. Ve výchozím nastavení je tato hodnota 500 milisekund.  

    - **Zvýraznění**: nastaví barvu, kterou CMTrace používá při zvýrazňování zvolených řádků protokolu. Ve výchozím nastavení je tato barva základní žlutá (červená: 255, zelená: 255, modrá: 0).  

    - **Sloupce**: nakonfiguruje sloupce, které jsou viditelné v zobrazení protokolu, a pořadí, ve kterém se zobrazí. Ve výchozím nastavení zobrazuje text protokolu, komponentu, datum a čas a vlákno.  

- Karta **Tisk**  

    - **Sloupce**: Nastavte, které sloupce používá při tisku souborů protokolu a v pořadí, ve kterém se zobrazí. Ve výchozím nastavení se vytisknou stejné sloupce jako v zobrazení.  

    - **Orientace**: nastaví výchozí orientaci tisku při tisku souborů protokolu. Toto nastavení potlačíte v dialogovém okně Tisk. Ve výchozím nastavení používá orientaci na výšku.  

- Karta **Upřesnit**  

    - **Interval aktualizace**: vynutí, aby CMTrace při načítání velkého počtu řádků aktualizoval zobrazení protokolu v zadaném intervalu. Ve výchozím nastavení je tato možnost zakázána s hodnotou nula.  

        > [!Note]  
        > Obecně platí, že **interval aktualizace**neměňte. Může významně prodloužit dobu potřebnou k otevření velkých souborů protokolu.

### <a name="tools-menu"></a>Nabídka nástroje

V nabídce **nástroje** jsou k dispozici následující akce:

- [Najít](#find)
- [Najít další](#find-next)
- [Kopírovat do schránky](#copy-to-clipboard)
- [Zvýraznit](#highlight)
- [Filtr](#filter)
- [Chyba při vyhledávání](#error-lookup)
- [Pozastavení](#pause)
- [Zobrazit/skrýt podrobnosti](#showhide-details)
- [Zobrazit/skrýt podokno informací](#showhide-info-pane)

#### <a name="find"></a>Vyhledávání

Vyhledá v otevřeném souboru protokolu zadaný textový řetězec.  

#### <a name="find-next"></a>Najít další

Najde další vyhovující řetězec, jak jste předtím zadali v dialogovém okně Najít.  

#### <a name="copy-to-clipboard"></a>Kopírovat do schránky

Zkopíruje vybrané řádky jako prostý text do schránky systému Windows. Pokud zkoumáte soubory protokolu Configuration Manager a CCM, zkopírují se sloupce ve stejném pořadí jako v zobrazení. Jednotlivé sloupce oddělují znakem tabulátoru. Tuto akci použijte při kopírování protokolů do e-mailových zpráv nebo jiných dokumentů.  

#### <a name="highlight"></a>Zvýraznit

Zadejte řetězec, který CMTrace používá k hledání textu jednotlivých položek protokolu. Potom zvýrazní libovolný text protokolu, který odpovídá řetězci, který zadáte.  

- Zvýraznění používá barvu, kterou jste zadali v části Předvolby.  

- Chcete-li zvýrazňování vypnout, vymažte řetězec z tohoto pole.  

- Pokud zadáte desítkové nebo šestnáctkové číslo, CMTrace se pokusí porovnat hodnotu se sloupcem vlákna. Toto chování použijte, pokud chcete zvýraznit zpracování jednoho vlákna, aniž byste museli vyfiltrovat další vlákna, která by s ním mohla spolupracovat.  

- Pokud chcete porovnat řetězce podle velikosti písmen, povolte možnost rozlišovat **velká a malá**písmena.  

#### <a name="filter"></a>Filtr

Umožňuje zobrazit nebo skrýt řádky protokolu na základě zadaných kritérií. Použijte filtry na libovolný ze čtyř sloupců bez ohledu na to, zda jsou viditelné. Tato nastavení platí pro každý otevřený soubor protokolu.

Příklady:
<!--SCCMDocs issue #603-->

- Vyfiltruje text **souboru Smsts. log** , který obsahuje "Action" nebo "Group".
- Filter **InventoryAgent. log** , kde text položky obsahuje "cíl".

#### <a name="error-lookup"></a>Chyba při vyhledávání

Chcete-li zobrazit popis, zadejte nebo vložte kód chyby buď v desítkovém nebo šestnáctkovém formátu. Mezi možné zdroje chyb patří: Windows, WMI nebo WinHTTP.

#### <a name="pause"></a>Pozastavení

Pozastavte nebo restartujte monitorování protokolu. Následující případy použití jsou některými možnými důvody k použití této akce:  

- Když CMTrace zobrazuje informace o souboru protokolu příliš rychle  

- Když pozastavíte monitorování protokolu, informace, které CMTrace zobrazí, nebudou ztraceny, pokud se aktuální soubor vrátí do nového protokolu.  

- Když chcete zastavit CMTrace zobrazování nových dat při prohlédnutí souboru protokolu  

#### <a name="showhide-details"></a>Zobrazit/skrýt podrobnosti

Zobrazí nebo skryje všechny sloupce kromě textu protokolu. Také rozbalí sloupec text protokolu k šířce okna. Tuto akci použijte při prohlížení protokolů na počítači s nízkým rozlišením zobrazení. Zobrazí se více textu protokolu.  

> [!Note]  
> Při prohlížení souborů prostého textu CMTrace automaticky skryje podrobnosti, protože jsou vždycky prázdné.  

#### <a name="showhide-info-pane"></a>Zobrazit/skrýt podokno informací

Umožňuje zobrazit nebo skrýt podokno informace. Tuto akci použijte při prohlížení protokolů na počítači s nízkým rozlišením zobrazení. Zobrazí se další podrobnosti protokolování.  


## <a name="log-pane"></a>Podokno protokolu

Podokno protokol je v horní části okna CMTrace. Zobrazuje řádky ze souborů protokolu.

Když vyberete řádek, je dočasně zvýrazněný pomocí barevného schématu výběru v systému Windows.

Zvýrazněné řádky odpovídají kritériím definovaným pomocí možnosti **zvýraznění** v nabídce **nástroje** . Zvýraznění používá barvu, kterou zadáte v části **Předvolby**.

CMTrace zobrazuje řádky s chybami s použitím červené barvy pozadí a žlutého textu. V protokolech formátu CCM mají položky protokolu explicitní hodnotu typu, která označuje položku jako chybu. Pro jiné formáty protokolu CMTrace rozlišuje velká a malá písmena v každé položce pro libovolný textový řetězec, který odpovídá "Error".

Zobrazuje řádky s upozorněními pomocí žlutého pozadí. V protokolech formátu CCM mají položky protokolu explicitní hodnotu typu, která označuje položku jako upozornění. Pro jiné formáty protokolu CMTrace rozlišuje velká a malá písmena v každé položce pro libovolný textový řetězec, který odpovídá "Warn".


## <a name="info-pane"></a>Podokno informací

Podokno informace je v dolní části okna CMTrace. Zahrnuje následující funkce:

- Podrobnosti o aktuálně vybrané položce protokolu  

- Textové pole, které zobrazuje text protokolu  

- Zobrazí se konce řádků, aby byl formátovaný text čitelnější.  

- Snadnější čtení dlouhých položek, které nejsou plně viditelné v podokně protokolu  

Umožňuje zobrazit nebo skrýt podokno informace pomocí možnosti **Zobrazit/Skrýt informační podokno** v nabídce **nástroje** . Pokud podokno informace zabere více než polovinu okna protokolu, CMTrace ho automaticky skryje.

### <a name="progress-bar"></a>Indikátor průběhu

Při prvním otevření souboru protokolu CMTrace nahrazuje podokno informace indikátorem průběhu. Tento průběh indikuje, kolik stávajícího obsahu souboru se načetlo. Průběh dosáhne 100 procent, CMTrace odebere indikátor průběhu a nahradí ho podoknem informace. Při načítání velkých souborů vám toto chování poskytne informace o tom, jak dlouho může zatížení trvat.

### <a name="status-bar"></a>Stavový řádek

U souborů protokolu Configuration Manager Format a CCM-Format zobrazuje stavový řádek pro vybrané položky protokolu uplynulý čas. Pokud vyberete jednu položku, nástroj zobrazí čas od první položky protokolu k vybrané položce. Pokud vyberete více položek, vypočítá se čas z nejvyšší horní části vybrané položky na vybranou položku. CMTrace tyto informace formátuje následujícím způsobem:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Integrace prostředí Windows

CMTrace podporuje [přidružení souborů](#file-associations) a [přetahování myší](#drag-and-drop).

### <a name="file-associations"></a>Přidružení souborů

CMTrace se může přidružit k příponám. log a. lo_ názvů souborů. Po spuštění programu zkontroluje registr a určí, zda je již k těmto příponám názvů souborů přidružen. Pokud již CMTrace není přidružen k žádným příponám názvů souborů, budete vyzváni k přidružení přípon názvů souborů k CMTrace. Pokud vyberete tuto možnost Příště již **Nezobrazovat**, CMTrace tuto kontrolu pokaždé, když se na tomto počítači spustí.

### <a name="drag-and-drop"></a>Přetahování myší

CMTrace podporuje základní funkce přetahování myší. Přetáhněte soubor protokolu z Průzkumníka Windows do CMTrace a otevřete ho.


## <a name="other-tips"></a>Další tipy

### <a name="last-directory-registry-key"></a>Poslední klíč registru adresáře

<!--511280-->
Ve výchozím nastavení CMTrace ukládá poslední umístění protokolu, které jste otevřeli. Toto chování je užitečné na serveru lokality, protože je ve výchozím nastavení cesta k protokolům.

Při prvním spuštění na klientovi se použije jako výchozí aktuální pracovní adresář. Toto umístění může být cesta, kam jste uložili CMTrace, nebo cestu, například `%userprofile%\Desktop`.

**Poslední hodnota adresáře** v klíči `HKEY_CURRENT_USER\Software\Microsoft\Trace32` registru řídí toto výchozí umístění. Pokud tuto hodnotu `%windir%\CCM\Logs` nastavíte na klienty, pak CMTrace při prvním spuštění otevře soubory v umístění protokolu klienta.


## <a name="see-also"></a>Viz také

- [Soubory protokolů](../plan-design/hierarchy/log-files.md)

- [Prohlížeč souborů protokolu Support Center](support-center.md#support-center-log-file-viewer)

- [OneTrace Support Center](support-center-onetrace.md)
