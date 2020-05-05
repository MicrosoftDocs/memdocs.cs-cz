---
title: Spy pro zásady
titleSuffix: Configuration Manager
description: Pomocí zásady Spy můžete zobrazit a řešit potíže se systémem zásad na Configuration Manager klientech.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723177"
---
# <a name="policy-spy"></a>Spy pro zásady

*Platí pro: Configuration Manager (Current Branch)*

Zásada Spy je jedním z [Configuration Manager nástrojů](tools.md). Je to nástroj pro zobrazení a řešení potíží se systémem zásad na Configuration Manager klientech. Spusťte **PolicySpy. exe** a otevřete tak uživatelské rozhraní. Další informace o použití příkazového řádku najdete v tématu [syntaxe příkazového řádku](#bkmk_policyspy-syntax).

> [!Important]  
> Spusťte zásadu Spy jako správce. Pokud ho **nespustíte jako správce**, zobrazí se v části informace o klientovi následující chyba:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a>Syntaxe příkazového řádku

Zásada Spy je primárně určena pro použití prostřednictvím jejího uživatelského rozhraní. Poskytuje omezené možnosti příkazového řádku pro podporu automatizace a dávkového zpracování.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Nastavení`/export`
Tato možnost tiše exportuje zásady místního nebo vzdáleného počítače. `<ExportFilename>`je název souboru, do kterého nástroj uloží exportovaný zásady XML. Pokud zadáte `<computername>` možnost, zásada Spy exportuje zásady tohoto počítače místo místního počítače.

> [!Note]  
> Tato možnost příkazového řádku neposkytuje způsob, jak zadat přihlašovací údaje uživatele. Chcete-li použít alternativní přihlašovací údaje pro přístup ke vzdálenému počítači, pomocí příkazu **runas** otevřete nový příkazový řádek s požadovanými zabezpečovacími pověřeními.  


## <a name="usage"></a>Využití

### <a name="tools-menu"></a>Nabídka nástroje

V nabídce **nástroje** jsou k dispozici následující akce:  

- **Otevřít vzdálené**: připojí se ke Configuration Manager zásad klienta na vzdáleném počítači. Pomocí dialogového okna připojit můžete načíst název vzdáleného počítače a volitelné přihlašovací údaje uživatele. Pokud se připojení nezdařilo, zobrazí se informace o chybě v podokně informace o klientovi. Pokud se připojení znovu nepovede, zkuste se připojit výběrem možnosti **aktualizovat** v nabídce **Upravit** nebo stisknutím klávesy F5.  

- **Otevřít soubor**: otevře soubor exportu zásady (XML) vytvořený pomocí možnosti **Exportovat zásadu** . Tento nástroj zobrazí exportované zásady přesně stejně jako aktivní zásady. Zakáže některé funkce, které se použijí jenom v případě, že se připojíte ke skutečnému klientovi.  

- **Požadavek na přiřazení počítače**: aktivuje požadavek na přiřazení zásad počítače na cílovém počítači. Tato funkce je při zobrazení exportovaných zásad zakázaná.  

- **Vyhodnotit zásady počítače**: aktivuje na cílovém počítači vyhodnocení zásad počítače. Tato funkce je při prohlížení exportovaných zásad zakázaná.  

- **Požádat o přiřazení uživatelů**: aktivuje požadavek na přiřazení uživatelských zásad pro aktuálně přihlášeného uživatele. Tato funkce je k dispozici pouze v případě, že je v místním počítači zobrazena zásada.  

- **Vyhodnotit zásady uživatele**: aktivuje hodnocení zásad uživatele pro aktuálně přihlášeného uživatele. Tato funkce je k dispozici pouze v případě, že je v místním počítači zobrazena zásada.  

- **Resetování zásad**: Odebere všechny jiné než výchozí zásady a obnoví soubory cookie zásad pro daný web. Pak aktivuje požadavek na přiřazení zásad počítače. Tato funkce je při prohlížení exportovaných zásad zakázaná.  

- **Zásady exportu**: exportuje zásadu cílového počítače do souboru XML. Zobrazit tento soubor na jakémkoli počítači se zásadou Spy Chcete-li otevřít soubor exportu, vyberte možnost **otevřít soubor** v nabídce **nástroje** . Tato funkce je při prohlížení exportovaných zásad zakázaná.  


### <a name="edit-menu"></a>Nabídka upravit

V nabídce **Úpravy** jsou k dispozici následující akce:  

- **Odstranit**: Odstraní instanci vybranou v podokně výsledků. Tato akce je podporovaná jenom pro instance zásad. Pokud se pokusíte odstranit cokoli jiného než instance zásad, nástroj zobrazí chybovou zprávu. Tato funkce je při prohlížení exportovaných zásad zakázaná.  

- **Refresh**: aktualizuje všechny výsledky, aby se zobrazily nejnovější informace. Všechny uzly stromu rozbalené před aktualizací se následně rozšíří automaticky. Pokud se zásada Spy úspěšně nepřipojila k zásadám cílového počítače, pokusí se znovu připojit. Tato funkce je při prohlížení exportovaných zásad zakázaná.  

- **Vymazat události**: vymaže všechny položky na kartě události.  



## <a name="results-pane"></a>Podokno výsledků

V podokně výsledků se zobrazují různá zobrazení systému zásad v cílovém počítači. Kliknutím na jednu z následujících čtyř karet získáte přístup k těmto zobrazením: 
- [Actual](#bkmk_policyspy-actual)
- [Požádáno](#bkmk_policyspy-requested)
- [Výchozí](#bkmk_policyspy-default)
- [Události](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a>Provedené

Tato karta zobrazuje aktuální zásady klienta. Aktuální zásada určuje chování klienta a chování jeho klientských agentů, jako je distribuce softwaru a inventář. Na kartě se zobrazí výsledky ve stromovém formátu s kořenovým uzlem pro obor názvů počítače a pro každý obor názvů specifický pro uživatele. Rozbalte uzel oboru názvů, aby se zobrazil seznam tříd. Rozbalte třídu pro zobrazení seznamu jeho instancí. Seznam tříd obsahuje pouze třídy, které mají instance.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a>Požadavků

Tato karta zobrazuje přiřazení zásad, která klient získal ze své přiřazené lokality. Karta zobrazuje výsledky ve stromovém formátu s kořenovým uzlem pro obor názvů počítače a pro každý obor názvů specifický pro uživatele. Rozbalení uzlu oboru názvů zobrazí následující uzly:  

- **Konfigurace**: zobrazuje seznam tříd konfigurace odvozených od CCM_Policy_Config, včetně objektu zásad, přiřazení a dalších.  

- **Nastavení**: zobrazí všechna aktivní nastavení vygenerovaná zásadami. Nastavení se zobrazí pod uzlem konfigurace. 

> [!Note]   
> Existuje více instancí se stejným názvem, protože klient nesloučil tato nastavení do konečné výsledné sady. Zásada Spy zobrazuje instance v tomto uzlu pomocí vlastností RealKey namísto jejich skutečných klíčů zásad. Tyto instance korelujte s výslednou sadou zobrazenou na aktuální kartě.  


### <a name="default"></a><a name="bkmk_policyspy-default"></a>Výchozí

Tato karta zobrazuje stejné informace jako **požadovaná** karta. Zahrnuje také obsah oborů názvů DefaultMachine a DefaultUser.


### <a name="events"></a><a name="bkmk_policyspy-events"></a>Událost

Tato karta zobrazuje události agenta zásad, jak se vyskytují. Zobrazení vytvoří odběr událostí rozhraní WMI pro všechny události odvozené od CCM_PolicyAgent_Event. Zobrazení obsahuje maximálně 200 událostí. V případě potřeby odstraní nejstarší události v horní části seznamu. Pokud vyberete poslední položku v seznamu, seznam se automaticky posune dolů, protože přidá nové události. V opačném případě si zobrazení zachová aktuální pozici a musíte se posouvat dolů nebo stisknout klávesu end a zobrazit nové události. Toto zobrazení je při prohlížení exportovaných zásad vždy prázdné.



## <a name="client-info-pane"></a>Podokno informace o klientovi
V podokně informace o klientovi se zobrazí seznam vlastností pro cílový počítač. Zobrazí následující vlastnosti, pokud jsou k dispozici:  
- Název
- ID
- Verze
- Web
- Přiřazený MP
- Rezidentní MP
- Server MP proxy
- Stav proxy serveru



## <a name="details-pane"></a>Podokno podrobností
V podokně podrobností se zobrazí podrobné informace o aktuálním výběru. Pokud není žádný výběr aktivní, zobrazí se informace o samotné zásadě, včetně verze. V opačném případě se zobrazí reprezentace vybrané položky ve formátu MOF (Správa objektů).

Zásada Spy používá vlastní rutinu generace MOF, která umožňuje vytvořit uživatelsky přívětivější zobrazení HTML než soubory MOF vygenerované rozhraním WMI. Toto chování umožňuje, aby se v zásadách Spy přidaly následující funkce, které by měly být MOF čitelnější:  

- Zvýrazňování syntaxe  

- Odsaditelné objekty a pole  

- Vlastnosti jsou uspořádány do systémových, zděděných a místních skupin. Ve výchozím nastavení sbalí systém a zděděné skupiny. Okamžitě uvidíte, které vlastnosti instance skutečně používají.  

- Zkopírujte soubor MOF nebo zkopírujte soubor MOF s prostým textem do schránky. Tato funkce je užitečná pro vložení souboru MOF do jiných aplikací, a to přímým voláním nástroje MofComp.  

V podokně podrobností se instance objektů zásad odvozené z CCM_Policy_Policy zobrazí tělo zásady pod objektem MOF, který se zobrazí. Pokud klient nestáhl tělo zásady, zásada Spy zobrazí hypertextový odkaz. Kliknutím na odkaz stáhnete tělo zásady přímo z bodu správy klienta. Pokud nástroj úspěšně stáhne tělo zásady, nahradí hypertextový odkaz obsahem odpovědi. V opačném případě zásada Spy aktualizuje zobrazení, které indikuje, že se požadavek nezdařil.

