---
title: Endpoint Protection nejčastějších dotazech klienta
titleSuffix: Configuration Manager
description: Získejte odpovědi na nejčastější dotazy k programu Windows Defender a Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906837"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Endpoint Protection nejčastějších dotazech klienta

*Platí pro: Configuration Manager (Current Branch)*


Tyto nejčastější dotazy jsou určené uživatelům, kterým správce IT nasadil do spravovaného počítače program Windows Defender nebo aplikaci Endpoint Protection. Tento obsah se nemusí vztahovat na jiný antimalwarový software. Microsoft System Center Endpoint Protection spravuje Windows Defender ve Windows 10. Může také nasadit a spravovat klienta Endpoint Protection do počítačů před Windows 10. Tento článek popisuje program Windows Defender, ale informace v něm uvedené platí i pro aplikaci Endpoint Protection.  

-   [Proč potřebuji antivirový a antispywarový software?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Jak poznám, že můj počítač napadl škodlivý software?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Jak můžu najít verzi programu Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [Co mám dělat, když program Windows Defender nebo aplikace Endpoint Protection objeví v mém počítači škodlivý software?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [Co je to virus?](#what-is-a-virus)  
-   [Co je to spyware?](#what-is-spyware)  
-   [Jaký je rozdíl mezi viry, spywarem a dalším potenciálně nebezpečným softwarem?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Odkud pocházejí viry, spyware a další potenciálně nežádoucí software?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Můžu získat škodlivý software bez vědomí?](#can-i-get-malicious-software-without-knowing-it)  
-   [Proč je důležité si před instalací softwaru číst licenční smlouvy?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Jaký je rozdíl mezi aplikací Endpoint Protection a programem Windows Defender?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Proč program Windows Defender nezjistí soubory cookie?](#why-doesnt-windows-defender-detect-cookies)  
-   [Jak můžu zabránit malwaru?](#how-can-i-prevent-malware)  
-   [Co jsou definice virů a spywaru?](#what-are-virus-and-spyware-definitions)  
-   [Chcete Návody udržovat definice virů a spywaru v aktuálním stavu?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Návody odebrat nebo obnovit položky v karanténě pomocí programu Windows Defender nebo Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Co je ochrana v reálném čase?](#what-is-real-time-protection)  
-   [Návody víte, že v mém počítači běží program Windows Defender nebo Endpoint Protection?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Jak nastavím výstrahy programu Windows Defender nebo aplikace Endpoint Protection?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a> K čemu potřebuji antivirový a antispywarový software?  

 Je velmi důležité zajistit, aby byl ve vašem počítači spuštěný software, který chrání před škodlivým softwarem. Škodlivý software, který zahrnuje viry, spyware nebo jiný potenciálně nežádoucí software, se může pokusit nainstalovat do vašeho počítače, kdykoli se připojíte k internetu. Může také váš počítač napadnout, když instalujete nějaký program z disku CD, DVD nebo jiného vyměnitelného média. Škodlivý software také může být naprogramovaný tak, aby se spouštěl v neočekávanou dobu, nejen hned po instalaci.  

 Windows Defender nebo Endpoint Protection nabízí tři způsoby, jak škodlivému softwaru zabránit v napadení vašeho počítače:  

-   **Pomocí** ochrany v reálném čase – ochrana v reálném čase umožňuje programu Windows Defender neustále monitorovat váš počítač a upozorňovat vás, když se v počítači pokusí nainstalovat nebo spustit škodlivý software, včetně virů, spywaru nebo jiného potenciálně nežádoucího softwaru. Potom program Windows Defender tento software pozastaví a umožní vám naložit se softwarem podle doporučení nebo provést jinou akci.

-   **Možnosti prohledávání** – pomocí programu Windows Defender můžete vyhledat potenciální hrozby, jako jsou viry, spyware a další škodlivý software, který by mohl ohrozit váš počítač. Také v něm můžete naplánovat pravidelné kontroly a odebrat škodlivý software zjištěný při kontrole.  

-   **Služba Microsoft Active Protection Service komunita** – online služba Microsoft Active Protection Service komunita vám pomůže zjistit, jak jiní lidé reagují na software, u kterého ještě nedošlo k klasifikování rizik. Na základě těchto informací si můžete vybrat, jestli tento software ve svém počítači povolíte. Pokud budete v komunitě sami aktivní, vaše volby se přidají do hodnocení komunity, které pomáhá ostatním lidem rozhodnout se o dalším postupu.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Jak poznám, že můj počítač napadl škodlivý software?  

 Pokud se projeví některý z těchto příznaků, může to znamenat, že máte v počítači nějakou formu škodlivého softwaru, jako jsou viry, spyware nebo jiný potenciálně nežádoucí software:  

-   Všimnete si nových panelů nástrojů, odkazů nebo oblíbených položek, které jste sami nepřidali do webového prohlížeče.  

-   Neočekávaně se změní domovská stránka, ukazatel myši nebo vyhledávací program.  

-   Zadáte adresu určitého webu, například vyhledávacího webu, ale bez upozornění se otevře jiný web.  

-   Z počítače se automaticky odstraňují soubory.  

-   Váš počítač se používá k útoku na jiné počítače.  

-   Zobrazují se vám místní reklamy, i když nejste připojení k internetu.  

-   Počítač najednou začne pracovat pomaleji než obvykle. Ne všechny problémy s výkonem počítače způsobuje škodlivý software, ale škodlivý software, hlavně spyware, může způsobit výraznou změnu.  

V počítači může být škodlivý software, i když žádné z těchto příznaků nepozorujete. Tento typ softwaru může bez vašeho vědomí nebo souhlasu shromažďovat informace o vás a vašem počítači. V zájmu ochrany svých osobních údajů a počítače byste měli mít neustále spuštěný program Windows Defender nebo aplikaci Endpoint Protection.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Jak můžu najít verzi programu Windows Defender?
 Chcete-li zobrazit verzi programu Windows Defender spuštěnou v počítači, spusťte program Windows Defender (klikněte na tlačítko **Start** a vyhledejte **program Windows Defender**), klikněte na **Nastavení**a posuňte se k dolnímu okraji nastavení programu Windows Defender a vyhledejte **informace o verzi**.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Co mám dělat, když program Windows Defender nebo aplikace Endpoint Protection objeví v mém počítači škodlivý software?  

 Pokud program Windows Defender objeví ve vašem počítači škodlivý nebo potenciálně nežádoucí software (buď při monitorování počítače pomocí ochrany v reálném čase, nebo po spuštění kontroly), upozorní vás na zjištěnou položku zobrazením oznámení v pravém dolním rohu obrazovky.  

 V oznámení najdete tlačítko **Vyčistit počítač** a odkaz **Zobrazit podrobnosti** , který umožňuje zobrazit další informace o zjištěné položce. Kliknutím na odkaz **Zobrazit podrobnosti** otevřete okno **Podrobnosti o potenciální hrozbě** , ve kterém najdete další informace o zjištěné položce. Teď si můžete vybrat, jakou akci chcete s položkou provést, nebo kliknout na **Vyčistit počítač**. Pokud potřebujete pomoc při rozhodování, jakou akci chcete se zjištěnou položkou provést, použijte jako vodítko úroveň výstrahy, kterou program Windows Defender k dané položce přiřadil (další informace najdete v článku Pochopení úrovní výstrah).  

 Úrovně výstrah pomáhají zvolit způsob reakce na viry, spyware a další potenciálně nežádoucí software. I když program Windows Defender doporučuje odebrat všechny viry a spyware, ne všechen označený software je opravdu škodlivý nebo nežádoucí. Následující informace vám pomohou rozhodnout se, jak postupovat, když program Windows Defender zjistí ve vašem počítači potenciálně nežádoucí software.  

 V závislosti na úrovni výstrah můžete se zjištěnou položkou provést některou z následujících akcí:  

- **Odebrat** – Tato akce trvale odstraní software z počítače.  

- **Umístit do karantény** – Tato akce umístí software do karantény, aby jej nebylo možné spustit. Když program Windows Defender umístí software do karantény, přesune ho do jiného umístění v počítači a potom zabrání v jeho spuštění, dokud se nerozhodnete software obnovit nebo ho neodeberete z počítače.  

- **Povolit** – Tato akce přidá software do seznamu povolených v programu Windows Defender a povolí jeho spuštění ve vašem počítači. Program Windows Defender už nebude zobrazovat výstrahy upozorňující na riziko, jaké může daný software představovat pro vaše osobní údaje nebo váš počítač.  

  Pokud pro některou položku, třeba pro určitý software, vyberete akci **Povolit** , program Windows Defender už nebude zobrazovat výstrahy upozorňující na riziko, jaké může daný software představovat pro vaše osobní údaje nebo váš počítač. Proto přidávejte software do seznamu povolených aplikací jenom v případě, že danému softwaru a jeho vydavateli důvěřujete.  

### <a name="how-to-remove-potentially-harmful-software"></a>Odebrání potenciálně škodlivého softwaru

Pokud chcete rychle a snadno odebrat všechny nežádoucí nebo potenciálně škodlivé položky zjištěné programem Windows Defender, použijte možnost **Vyčistit počítač** .  

1.  Když v oznamovací oblasti uvidíte oznámení, které program Windows Defender zobrazí po zjištění potenciálních hrozeb, klikněte na **Vyčistit počítač**.  

2.  Program Windows Defender odebere potenciální hrozbu (nebo hrozby) a po vyčištění počítače zobrazí oznámení.  

3.  Pokud chcete získat další informace o zjištěných hrozbách, klikněte na kartu **Historie** a potom vyberte možnost **Všechny nalezené položky**.  

4.  Pokud se všechny zjištěné položky nezobrazí, klikněte na **Zobrazit podrobnosti**. Pokud se zobrazí výzva k zadání hesla správce nebo k potvrzení, zadejte heslo nebo potvrďte akci.

> [!NOTE]  
>  Pokud je to možné, program Windows Defender při čištění počítače odebere jenom napadenou část souboru, ne celý soubor.  

##  <a name="what-is-a-virus"></a>Co je to virus?  
 Počítačové viry jsou softwarové programy záměrně vytvořené tak, aby narušovaly provoz počítače, zaznamenávaly, poškozovaly nebo odstraňovaly data, případně přes internet napadaly další počítače. Viry často zpomalují počítač a svou činností způsobují další potíže.  

##  <a name="what-is-spyware"></a> Co je to spyware?  
 Spyware je software, který se může sám nainstalovat nebo spustit ve vašem počítači, aniž by si vyžádal váš souhlas, zobrazil upozornění nebo vám poskytl možnost kontroly. Jakmile spyware napadne váš počítač, nemusí se projevit žádné symptomy, ale provoz počítače může ovlivnit řada škodlivých nebo nežádoucích programů. Spyware může například sledovat vaše chování online nebo shromažďovat informace o vás (včetně informací, které mohou prozradit vaši totožnost, a dalších citlivých údajů), měnit nastavení počítače nebo zpomalovat činnost počítače.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a> Jaký je rozdíl mezi viry, spywarem a dalším potenciálně nebezpečným softwarem?  
 Viry i spyware se do počítače nainstalují bez vašeho vědomí a mohou mít potenciálně rušivé a ničivé účinky. Mají také schopnost zachycovat informace z vašeho počítače a ty pak poškozovat nebo odstraňovat. Viry i spyware mohou negativně ovlivnit výkon počítače.  

 Hlavní rozdíl mezi viry a spywarem spočívá v jejich chování ve vašem počítači. Viry, podobně jako živé organismy, mají za cíl napadnout počítač, replikovat se a pak se rozšířit do co největšího počtu dalších počítačů. Spyware je ale podobně jako Mole – chce se přesunout do vašeho počítače a co nejrychleji zůstat, takže v době, kdy tam je, posílá cenné informace o vašem počítači do vnějšího zdroje.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Odkud pocházejí viry, spyware a další potenciálně nežádoucí software?  
 Nežádoucí software, jako jsou viry, se může nainstalovat prostřednictvím webů nebo programů, které stáhnete nebo nainstalujete z disku CD, DVD, externího pevného disku nebo zařízení. Spyware se nejčastěji instaluje prostřednictvím bezplatného softwaru, třeba programů pro sdílení souborů, šetřičů obrazovky nebo panelů nástrojů pro vyhledávání.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a> Může se škodlivý software nainstalovat bez mého vědomí?  
 Ano, některý škodlivý software můžete nainstalovat z webu prostřednictvím vloženého skriptu nebo programu na webové stránce. Některý škodlivý software zase vyžaduje, abyste instalaci provedli vy. Tento software využívá automaticky otevíraná okna na internetu nebo bezplatný software a vyžaduje, abyste přijali soubor ke stažení. Pokud ale pravidelně aktualizujete systém Microsoft Windows® a nenastavíte nižší úroveň nastavení zabezpečení, snižujete riziko napadení na minimum.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Proč je důležité si před instalací softwaru číst licenční smlouvy?  
 Při návštěvě webů nesouhlasí automaticky stahování všeho, co web nabízí. Pokud stahujete bezplatný software, například programy pro sdílení souborů nebo šetřiče obrazovky, pozorně si přečtěte licenční smlouvu. Hledejte věty, které říkají, že musíte přijmout reklamy a automaticky otevíraná okna od dané společnosti nebo že bude daný software odesílat nějaké informace svému vydavateli.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Jaký je rozdíl mezi aplikací Endpoint Protection a programem Windows Defender?  
 Endpoint Protection je antimalwarový software, což znamená, že je určený ke zjišťování přítomnosti široké škály škodlivého softwaru, včetně virů, spywaru a dalšího potenciálně nežádoucího softwaru, a k ochraně před ním. Program Windows Defender automaticky nainstalovaný v operačním systému Windows je software, který zjišťuje přítomnost spywaru a zastavuje jeho činnost.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a> Proč program Windows Defender nezjistí soubory cookie?  
 Soubory cookie jsou malé textové soubory, které weby ukládají do vašeho počítače za účelem ukládání informací o vás a vašich předvolbách. Weby používají soubory cookie k tomu, aby vám nabízely přizpůsobené prostředí a shromáždily informace o používání webu. Windows Defender nezjistí soubory cookie, protože je nepovažuje za hrozbu pro vaše osobní údaje nebo zabezpečení vašeho počítače. Většina internetových prohlížečů umožňuje blokovat soubory cookie.  

##  <a name="how-can-i-prevent-malware"></a> Jak se mám chránit proti malwaru?  
 Mezi největší hrozby pro dnešní uživatele počítačů patří viry a spyware. V obou případech platí, že se proti těmto potížím dá snadno bránit – stačí jenom trocha plánování:  

-   Udržujte software v počítači aktuální a nezapomeňte nainstalovat všechny opravy. Nezapomínejte pravidelně aktualizovat svůj operační systém.  

-   Přesvědčte se, jestli váš antivirový a antispywarový software, tedy program Windows Defender, používá nejnovější aktualizace proti potenciálním hrozbám (další informace najdete v tématu Jak zajistím aktuálnost definic virů a spywaru?). Také se ujistěte, že vždycky používáte nejnovější verzi programu Windows Defender.  

-   Stahujte jenom aktualizace z důvěryhodných zdrojů. Pro operační systémy Windows vždy přejít do [katalogu Microsoft Update](https://catalog.update.microsoft.com).  Pro jiný software vždy používejte legitimní weby společnosti nebo osoby, která ho vytváří.

-   Pokud dostanete e-mail s přílohou a nejste si jistí jeho zdrojem, měli byste ho okamžitě odstranit. Nestahujte žádné aplikace ani soubory z neznámých zdrojů a buďte opatrní při obchodování soubory s ostatními uživateli.  

-   Nainstalujte a používejte bránu firewall. Doporučujeme povolit bránu Windows Firewall.  

##  <a name="what-are-virus-and-spyware-definitions"></a> Co jsou definice virů a spywaru?  
 Při použití programu Windows Defender nebo aplikace Endpoint Protection je důležité mít aktuální definice virů a spywaru. Definice jsou soubory, které fungují jako neustále rostoucí encyklopedie potenciálních softwarových hrozeb. Windows Defender nebo Endpoint Protection na základě definic určuje, jestli je zjištěný software virus, spyware nebo jiný potenciálně nežádoucí software, a potom vás upozorní na potenciální rizika. V zájmu udržení aktuálního stavu definic program Windows Defender nebo aplikace Endpoint Protection spolupracuje se službou Microsoft Update a automaticky instaluje nově vydané definice. Můžete také nastavit program Windows Defender nebo aplikaci Endpoint Protection tak, aby před každou kontrolou vyhledávaly aktualizované definice online.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a> Jak zajistím aktuálnost definic virů a spywaru?  
 Definice virů a spywaru jsou soubory, které fungují jako encyklopedie známého škodlivého softwaru, včetně virů, spywaru a dalšího potenciálně nežádoucího softwaru. Nový škodlivý software vzniká neustále, a proto program Windows Defender nebo aplikace Endpoint Protection potřebuje ke zjištění toho, jestli software, který se snaží nainstalovat, spustit nebo změnit nastavení v počítači, není virus, spyware nebo jiný potenciálně nežádoucí software, aktuální definice.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Automatické vyhledání nových definic před plánovanými kontrolami (doporučeno)  

1.  Otevřete program Windows Defender nebo aplikaci Endpoint Protection kliknutím na ikonu v oznamovací oblasti nebo spuštěním z nabídky **Start** .  

2.  Klikněte na **Nastavení**a potom klikněte na **Naplánovaná kontrola**.  

3.  Ověřte, jestli je zaškrtnuté políčko **Před spuštěním naplánované kontroly ověřit, zda jsou k dispozici nejnovější definice virů a spywaru** , a potom klikněte na **Uložit změny**. Pokud se zobrazí výzva k zadání hesla správce nebo k potvrzení, zadejte heslo nebo potvrďte akci.  

### <a name="to-check-for-new-definitions-manually"></a>Ruční vyhledání nových definic

 Windows Defender nebo Endpoint Protection aktualizuje definice virů a spywaru ve vašem počítači automaticky. Pokud se definice neaktualizovaly na více než sedm dnů (například pokud jste počítač zapnuli na týden), program Windows Defender nebo Endpoint Protection vás upozorní, že jsou definice zastaralé.  

1.  Otevřete program Windows Defender nebo aplikaci Endpoint Protection kliknutím na ikonu v oznamovací oblasti nebo spuštěním z nabídky **Start** .  

2.  Pokud chcete nové definice vyhledat ručně, klikněte na kartu **Aktualizace** a potom klikněte na **Aktualizovat definice**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a> Jak odeberu nebo obnovím položky, které program Windows Defender nebo aplikace Endpoint Protection umístí do karantény?  

 Když program Windows Defender nebo aplikace Endpoint Protection umístí software do karantény, přesune ho do jiného umístění v počítači a potom zabrání v jeho spuštění, dokud se nerozhodnete software obnovit nebo ho neodeberete z počítače.  

 U všech kroků v tomto postupu platí, že pokud se zobrazí výzva k zadání hesla správce nebo k potvrzení, zadejte heslo nebo potvrďte akci.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Postup odebrání nebo obnovení položek, které program Windows Defender nebo aplikace Endpoint Protection umístí do karantény


1.  Klikněte na kartu **Historie** , vyberte **Položky v karanténě**a potom vyberte možnost **Položky v karanténě** .  

2.  Kliknutím na **Zobrazit podrobnosti** zobrazíte všechny položky.  

3.  Zkontrolujte všechny položky a potom u každé klikněte na **Odebrat** nebo **Obnovit**. Pokud chcete z počítače odebrat všechny položky umístěné do karantény, klikněte na **Odebrat vše**.  

##  <a name="what-is-real-time-protection"></a> Co je ochrana v reálném čase?  

 Ochrana v reálném čase umožňuje programu Windows Defender neustále monitorovat váš počítač a zobrazit výstrahu v případě, že se potenciální hrozby jako viry a spyware snaží nainstalovat nebo spustit v počítači. Tato funkce představuje důležitý prvek, kterým program Windows Defender pomáhá chránit váš počítač, a proto je dobré mít ochranu v reálném čase pořád zapnutou. Pokud se ochrana v reálném čase vypne, program Windows Defender vás na to upozorní a změní stav počítače na **riziko**.  

 Vždycky když ochrana v reálném čase zjistí hrozbu nebo potenciální hrozbu, program Windows Defender zobrazí oznámení. V takovém případě si můžete vybrat z těchto možností:  

- Odeberte zjištěnou položku kliknutím na tlačítko **Vyčistit počítač** . Program Windows Defender položku automaticky odebere z počítače.  

- Kliknutím na **Zobrazit podrobnosti** otevřete okno Podrobnosti o potenciální hrozbě a pak vyberte, kterou akci chcete se zjištěnou položkou provést.  

  Můžete zvolit software a nastavení, které chcete monitorovat pomocí programu Windows Defender, ale doporučujeme vám zapnout ochranu v reálném čase a povolit všechny možnosti ochrany v reálném čase. Následující tabulka obsahuje vysvětlení dostupných možností.  

|||  
|-|-|  
|**Možnost ochrany v reálném čase**|**Účel**|  
|Kontrolovat všechny stahované soubory|Tato možnost monitoruje stahované soubory a programy, včetně souborů automaticky stahovaných prostřednictvím aplikací Windows Internet Explorer a Microsoft Outlook® Express, jako jsou ovládací prvky ActiveX® a programy pro instalaci softwaru. Tyto soubory můžete stáhnout, nainstalovat nebo spustit přímo z prohlížeče. Mohou obsahovat škodlivý software, včetně virů, spywaru a dalšího potenciálně nežádoucího softwaru, který se může nainstalovat bez vašeho vědomí.<br /><br /> Pomocí možnosti ochrany v reálném čase program Windows Defender neustále monitoruje váš počítač a vyhledává škodlivé soubory nebo programy, které jste mohli stáhnout. Tato funkce monitorování znamená, že program Windows Defender nemusí zpomalovat práci na internetu nebo s e-maily tím, že by vyžadoval kontrolu souborů nebo programů, které chcete stáhnout.|  
|Monitorovat v tomto počítači aktivitu programů a souborů|Tato možnost monitoruje spouštění souborů a programů v počítači a upozorní vás na případné akce, které tyto soubory a programy provádějí a ke kterým u nich dochází. Tato funkce je důležitá, protože škodlivý software může využít chyby zabezpečení v programech, které nainstalujete, ke spuštění škodlivého nebo nežádoucího softwaru bez vašeho vědomí. Například když spustíte program, který často používáte, může se na pozadí spustit spyware. Windows Defender monitoruje programy a upozorní vás, pokud zjistí podezřelou aktivitu.|  
|Povolit monitorování chování|Tato možnost monitoruje sady chování a hledá v nich podezřelé postupy, které nemusí odhalit tradiční metody zjišťování virů.|  
|Povolit systém kontroly sítě|Tato možnost pomáhá chránit váš počítač před neoprávněným použitím známých chyb zabezpečení, což snižuje dobu mezi okamžikem, kdy byla zjištěna chyba zabezpečení a je použita aktualizace.|  

### <a name="to-turn-off-real-time-protection"></a>Vypnutí ochrany v reálném čase  

1.  Klikněte na **Nastavení**a potom na položku **Ochrana v reálném čase.**  

2.  Zrušte zaškrtnutí možností ochrany v reálném čase, které chcete vypnout, a potom klikněte na **Uložit změny**. Pokud se zobrazí výzva k zadání hesla správce nebo k potvrzení, zadejte heslo nebo potvrďte akci.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a> Jak poznám, že v mém počítači běží program Windows Defender nebo aplikace Endpoint Protection?  

 Po instalaci programu Windows Defender do počítače můžete zavřít hlavní okno a nechat program Windows Defender spuštěný na pozadí. Program Windows Defender zůstane v počítači dál spuštěný, bude ho monitorovat a chránit proti hrozbám.  

 Samozřejmě poznáte, že je program Windows Defender spuštěný, vždycky když zobrazí nějaké oznámení v oznamovací oblasti. Tato oznámení obsahují výstrahy na potenciální hrozby zjištěné programem Windows Defender.  

 Budou se zobrazovat také další výstražná oznámení, například pokud z nějakého důvodu dojde k vypnutí ochrany v reálném čase, pokud delší dobu neaktualizujete definice virů a spywaru nebo pokud budou dostupné upgrady programu. Windows Defender také krátce zobrazí oznámení pokaždé, když bude kontrolovat počítač.  

> [!TIP]
> 
> Pokud v oznamovací oblasti nevidíte ikonu programu Windows Defender, kliknutím na šipku v oznamovací oblasti zobrazíte skryté ikony včetně ikony programu Windows Defender.  


 Barvy ikony závisí na aktuální stavu počítače:  

-   Zelená značí, že je počítač ve stavu Chráněn.  

-   Žlutá značí, že je počítač ve stavu Potenciálně nechráněn.  

-   Červená značí, že je počítač ve stavu Ohrožen.  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Jak nastavím výstrahy programu Windows Defender nebo aplikace Endpoint Protection?  
 Když je v počítači spuštěný Windows Defender, automaticky zobrazuje výstrahy na zjištěné viry, spyware a další potenciálně nežádoucí software. Windows Defender také můžete nastavit tak, aby zobrazoval výstrahy při spuštění softwaru, který ještě neprošel analýzou, a když nějaký software provádí změny v počítači.  

### <a name="to-set-up-alerts"></a>Postup nastavení výstrah  

1.  Klikněte na **Nastavení**a potom na položku **Ochrana v reálném čase.**  

2.  Zkontrolujte, jestli je zaškrtnuté políčko **Zapnout ochranu v reálném čase (doporučeno)** .  

3.  Zaškrtněte políčka u možností ochrany v reálném čase, které chcete používat, a potom klikněte na **Uložit změny**. Pokud se zobrazí výzva k zadání hesla správce nebo k potvrzení, zadejte heslo nebo potvrďte akci.  

### <a name="see-also"></a>Viz také  
 [Řešení potíží s programem Windows Defender nebo klientem Endpoint Protection](troubleshoot-endpoint-client.md)   

 [Klientská Endpoint Protectionová ochrana](endpoint-protection-client-help.md)
