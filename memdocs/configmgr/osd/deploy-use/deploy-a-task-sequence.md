---
title: Nasazení pořadí úkolů
titleSuffix: Configuration Manager
description: Tyto informace slouží k nasazení pořadí úloh do počítačů v kolekci.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2347275ffdc194e73cf792d6f83ffa75732f8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711410"
---
# <a name="deploy-a-task-sequence"></a>Nasazení pořadí úkolů

*Platí pro: Configuration Manager (Current Branch)*

Po vytvoření pořadí úloh a distribuci odkazovaného obsahu ho nasaďte do kolekce zařízení. Tato akce umožní, aby se pořadí úkolů spouštělo na zařízení. Nasazené pořadí úkolů může být spuštěno automaticky nebo při instalaci uživatelem zařízení.

> [!WARNING]  
> Můžete spravovat chování při vysoce rizikových nasazeních pořadí úkolů. Vysoce rizikové nasazení je takové nasazení, které se instaluje automaticky a u kterého hrozí riziko nechtěných výsledků. Například pořadí úkolů, které má účel **požadováno** , který nasazuje operační systém, je považováno za vysoce rizikové nasazení. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

## <a name="process"></a>Proces

Pomocí následujícího postupu můžete nasadit pořadí úloh do počítačů v kolekci.  

> [!NOTE]  
> Stavové zprávy pro nasazení pořadí úloh se zobrazují v okně zpráv v primární lokalitě, ale nezobrazují se v lokalitě centrální správy.  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

2. V seznamu **Pořadí úloh** vyberte pořadí úloh, které chcete nasadit.  

3. Na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte **nasadit**.  

    > [!NOTE]  
    > Pokud není k dispozici **nasazení** , pořadí úkolů má neplatný odkaz. Opravte odkaz a poté zkuste pořadí úloh nasadit znovu.  

4. Na stránce **Obecné** zadejte následující informace.  

    - **Pořadí úloh**: Určete pořadí úkolů, které se má nasadit. Ve výchozím nastavení toto pole zobrazuje vybrané pořadí úkolů.  

    - **Kolekce**: vyberte kolekci obsahující počítače, ve kterých se má pořadí úkolů Spustit.  

        Nesaďte pořadí úkolů, které nainstaluje operační systém do nevhodných kolekcí, jako je například kolekce všech serverů datového centra. Ujistěte se, že vybraná kolekce obsahuje pouze ty počítače, ve kterých chcete spustit pořadí úloh.  

        Další informace o nasazení s vysokým rizikem najdete v tématu [nasazení s vysokým rizikem](#bkmk_high-risk).

    - **Použít výchozí skupiny distribučních bodů přidružené k této kolekci**: Uložte obsah pořadí úloh do výchozí skupiny distribučních bodů kolekce. Pokud jste vybranou kolekci nepřidali se skupinou distribučních bodů, je tato možnost zobrazena šedě.  

    - **Automaticky distribuovat obsah pro závislosti**: Pokud má nějaký odkazovaný obsah závislosti, webový server také odešle závislý obsah do distribučních bodů.  

    - **Předem stáhnout obsah pro toto pořadí úloh**: Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](configure-precache-content.md).  

    - **Vybrat šablonu nasazení**: Uložit a zadat šablonu nasazení pro pořadí úkolů.<!--1357391-->  

        > [!IMPORTANT]  
        > Některé položky nejsou uloženy v šabloně.<!--510610--> Při spuštění Průvodce nasazením nezapomeňte použít následující položky:  
        >
        > - Instalace softwaru
        > - Plánování
        > - Předem stáhnout obsah

    - **Komentář (volitelné**: Určete další informace, které popisují toto nasazení pořadí úkolů.  

5. Na stránce **nastavení nasazení** zadejte následující informace:  

    - **Účel**: V rozevíracím seznamu vyberte jednu z těchto možností:  

        - **K dispozici**: uživatel uvidí pořadí úloh v centru softwaru a může je nainstalovat na vyžádání.  

        - **Požadováno**: Configuration Manager automaticky spustí pořadí úloh podle nakonfigurovaného plánu. Pokud pořadí úkolů není skryté, může uživatel stále sledovat jeho stav nasazení. Můžou taky pomocí centra softwaru nainstalovat pořadí úkolů před konečným termínem.  

        > [!NOTE]
        > Pokud se do zařízení přihlásí více uživatelů, nemusí se nasazení balíčku a pořadí úkolů zobrazit v centru softwaru.  

    - **Zpřístupnit pro následující**: Určete, jestli je pořadí úkolů k dispozici pro jeden z následujících typů:  

        - Pouze klienti Configuration Manager  
        - Configuration Manager klienty, média a technologie PXE  
        - Pouze média a technologie PXE  
        - Pouze média a technologie PXE (skryté)  

        > [!IMPORTANT]  
        > Nastavení **Pouze média a technologie PXE (skryté)** pro automatické nasazení pořadí úloh. Pokud chcete, aby se počítač automaticky spouštěl do nasazení bez zásahu uživatele, vyberte možnost **Povolení bezobslužného nasazení operačního systému** a nastavte proměnnou **SMSTSPreferredAdvertID** jako součást média. Další informace o proměnných pořadí úkolů najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID).  

    - **Odeslat pakety pro probuzení**: Pokud je nasazení **vyžadováno** a vyberete tuto možnost, lokalita odešle paket pro probuzení do počítačů předtím, než klient spustí nasazení. Tento paket probudí počítač z režimu spánku v konečném termínu instalace. Než použijete tuto možnost, musí být počítače a sítě nakonfigurované pro Wake On LAN. Další informace najdete v tématu [plánování probuzení klientů](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    - **Umožňuje klientům v měřeném připojení k internetu stahovat obsah po uplynutí konečného termínu instalace, což může způsobit další náklady**: Tato možnost je k dispozici pouze pro **požadovaná** nasazení. Pokud máte vlastní pořadí úloh, které nainstaluje aplikaci, ale neprovádí nasazení operačního systému, můžete určit, jestli chcete klientům dovolit, aby po uplynutí konečného termínu instalace stáhli obsah, když používají měřené připojení k Internetu. Poskytovatelé připojení k internetu někdy účtují podle množství dat, která používáte, když jste na měřeném připojení k Internetu.  

        > [!NOTE]  
        > Zatímco použití měřeného internetového připojení může fungovat pro pořadí úloh, která neimplementují operační systém, není podporované.  

6. Na stránce **plánování** zadejte následující informace:  

    > [!IMPORTANT]  
    > Když se klient Windows PE spustí z prostředí PXE nebo ze spouštěcího média, klient nevyhodnotí plány nasazení. Tyto plány zahrnují dobu zahájení, vypršení platnosti a konečný termín. Nastavte jenom plány v nasazení na klienty, kteří začínají z úplného operačního systému Windows. K řízení aktivních sekvencí úloh nasazených klientům, kteří začínají pomocí Windows PE, zvažte použít jiné metody, třeba okna údržby.  

    - **Naplánovat, kdy bude toto nasazení k dispozici**: Zadejte datum a čas, kdy bude pořadí úkolů dostupné pro spuštění na cílovém počítači. Když vyberete možnost **UTC** , pořadí úkolů bude k dispozici pro několik počítačů současně. V opačném případě je nasazení k dispozici v různých časech v závislosti na místním čase na každém počítači.  

        Pokud čas zahájení předchází požadovanému času, klient stáhne obsah pořadí úloh v počátečním čase.  

    - **Naplánovat, kdy toto nasazení vyprší**: Zadejte datum a čas, kdy vyprší platnost pořadí úkolů na cílovém počítači. Když vyberete možnost **UTC** , pořadí úkolů vyprší na několika cílových počítačích ve stejnou dobu. V opačném případě nasazení vyprší v různých časech v závislosti na místním čase na každém počítači.  

    - **Plán přiřazení**: u **požadovaného** nasazení určete, kdy klient spustí pořadí úkolů. Můžete přidat více plánů. Plán přiřazení může mít jednu z následujících konfigurací:  

        - Konkrétní datum a čas  
        - Způsob opakování měsíčně, týdně nebo vlastního  
        - Co nejdříve  
        - Přihlášení nebo odhlášení událostí  

        > [!NOTE]  
        > Pokud naplánujete čas zahájení pro požadované nasazení, které je dřívější než datum a čas, kdy je pořadí úkolů k dispozici, klient Configuration Manager stáhne obsah v přiřazeném čase zahájení. K tomuto chování dochází, i když jste naplánovali, aby bylo pořadí úloh k dispozici později.<!--SCCMDocs issue 777-->  

    - **Chování při spuštění**: Určete, kdy se má pořadí úkolů znovu spustit. Vyberte jednu z následujících možností:  

        - **Nikdy znovu nespouštět nasazený program**: Pokud klient dříve spustil pořadí úkolů, nespustí se znovu. Pořadí úkolů se nespustí znovu ani v případě, že původně selhalo nebo došlo ke změně souborů pořadí úkolů.  

        - **Vždy znovu spustit program**: pořadí úkolů se na klientovi vždy znovu spustí, když je naplánováno nasazení. Znovu se spustí i v případě, že pořadí úkolů již bylo úspěšně spuštěno. Toto nastavení je užitečné, pokud používáte opakovaná nasazení, ve kterých je pořadí úkolů rutinně aktualizováno.  

            > [!IMPORTANT]  
            > Tato možnost je ve výchozím nastavení zaškrtnutá. Nemá ale žádný vliv, dokud přiřadíte požadované nasazení. Uživatel může vždy znovu spustit dostupná nasazení.  

        - **Spustit znovu, pokud se předchozí pokus nezdařil**: pořadí úkolů se znovu spustí, když je naplánováno nasazení, a to pouze v případě, že bylo dříve spuštěno. Toto nastavení je užitečné pro požadované nasazení. Pokud poslední pokus o spuštění neproběhl úspěšně, pokusí se automaticky znovu spustit v závislosti na plánu přiřazení.  

        - **Znovu spustit, pokud bylo úspěšné při předchozím pokusu**: pořadí úkolů se znovu spustí jenom v případě, že se v klientovi dřív úspěšně spustil. Toto nastavení je užitečné, když používáte opakovaná nastavení, v nichž je pořadí úloh rutinně aktualizováno a každá aktualizace vyžaduje úspěšnou instalaci předchozí aktualizace.  

        > [!NOTE]  
        > Uživatel může znovu spustit dostupné nasazení pořadí úloh. Před nasazením dostupného pořadí úloh v produkčním prostředí nejprve otestujte, co se stane, když uživatel znovu spustí pořadí úloh vícekrát.  

7. Na stránce **Činnost koncového uživatele** zadejte následující informace:  

    - **Povolí uživateli spustit program nezávisle na přiřazení**: Určuje, jestli uživatel může spustit požadované nasazení mimo plán přiřazení. Tato možnost je vždycky povolená pro dostupná nasazení.  

    - **Zobrazit průběh pořadí úloh**: Určete, jestli Configuration Manager klient zobrazuje průběh pořadí úkolů.  

    - **Instalace softwaru**: Určete, jestli má uživatel povoleno instalovat software mimo nakonfigurované časové období údržby po naplánovaném čase.  

    - **Restart systému (pokud je to nutné pro dokončení instalace**: Určuje, jestli smí uživatel restartovat počítač po instalaci softwaru mimo nakonfigurované časové období údržby po čase přiřazení.  

    - **Zpracování filtru zápisu pro zařízení se systémem Windows Embedded**: Toto nastavení řídí chování při instalaci na zařízeních se systémem Windows Embedded, která jsou povolena pomocí filtru zápisu. Vyberte možnost potvrdit změny při dokončení instalace nebo během časového období údržby. Když vyberete tuto možnost, vyžaduje se restartování a změny se na zařízení zachovají. V opačném případě se aplikace nainstaluje do dočasného překrytí a potvrdí se později. Když nasadíte pořadí úloh do zařízení se systémem Windows Embedded, ujistěte se, že je zařízení členem kolekce, která má nakonfigurované časové období údržby.  

    - **Povolit spuštění pořadí úloh pro klienta na internetu**: Určete, jestli se může pořadí úkolů spouštět na internetovém klientovi. Operace, které vyžadují spouštěcí médium, jako je například instalace operačního systému, nejsou tímto nastavením podporovány. Tuto možnost použijte pouze pro obecné instalace softwaru nebo pro sekvence úloh založená na skriptech, které provádějí operace v rámci standardního operačního systému.  

        - Toto nastavení se podporuje pro nasazení místního upgradu pořadí úkolů Windows 10 do internetových klientů přes bránu pro správu cloudu. Další informace najdete v tématu [nasazení místního upgradu Windows 10 přes CMG](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. Na stránce **výstrahy** určete nastavení výstrah, která chcete pro toto nasazení pořadí úkolů použít.  

9. Na stránce **Distribuční body** zadejte následující informace:  

    - **Možnosti nasazení**: Určete jednu z následujících možností:  

        > [!NOTE]  
        > Když použijete vícesměrové vysílání k nasazení operačního systému, Stáhněte obsah do počítačů podle potřeby nebo před spuštěním pořadí úloh.  

        - **Pokud to vyžaduje spuštěné pořadí úkolů, stáhnout veškerý obsah místně**: Určete, že klienti stáhnou obsah z distribučního bodu, který je potřebný pro pořadí úkolů. Klient spustí pořadí úloh. Když krok v pořadí úkolů vyžaduje obsah, stáhne se před spuštěním kroku.  

        - Před **spuštěním pořadí úloh stáhnout veškerý obsah místně**: Určete, že klienti stáhnou obsah z distribučního bodu předtím, než se spustí pořadí úkolů. Pokud pořadí úkolů zpřístupníte pro nasazení PXE a spouštěcí média na stránce **nastavení nasazení** , tato možnost se nezobrazí.  

        - **Přístup k obsahu přímo z distribučního bodu, pokud to vyžaduje běžící pořadí úloh**: Určete, jestli klienti spouštějí obsah z distribučního bodu. Tato možnost je k dispozici pouze v případě, že povolíte všechny balíčky přidružené k pořadí úkolů pro použití sdílené složky balíčku v distribučním bodě. Chcete-li obsahu povolit použití sdílené složky balíčku, nahlédněte na kartu **Přístup k datům** v nabídce **Vlastnosti** jednotlivých balíčků.  

            > [!IMPORTANT]  
            > U největších zabezpečení vyberte možnosti pro **místní stažení obsahu v případě potřeby spuštěného pořadí úloh** nebo **stažení veškerého obsahu místně před spuštěním pořadí úkolů**. Když vyberete jednu z těchto možností, Configuration Manager vytvoří hodnotu hash balíčku, aby se zajistila integrita balíčku. Když vyberete možnost **přístupu k obsahu přímo z distribučního bodu, pokud to vyžaduje běžící pořadí úloh**, Configuration Manager před spuštěním zadaného programu neověřuje hodnotu hash balíčku. Vzhledem k tomu, že lokalita nemůže zajistit integritu balíčku, je možné, že uživatelé s právy správce mohou měnit nebo manipulovat s obsahem balíčku.  

    - **Není-li místní distribuční bod k dispozici, použijte vzdálený distribuční bod**: Určete, zda mohou klienti používat distribuční body ze sousední skupiny hranic ke stažení obsahu, který je požadovaný pořadím úloh.  

    - **Umožňuje klientům používat distribuční body z výchozí skupiny hranic lokality**: Určete, jestli mají klienti stahovat obsah z distribučního bodu ve výchozí skupině hranic lokality, když není dostupný z distribučního bodu v aktuální nebo sousední skupině hranic.  

        > [!Note]  
        > Počínaje verzí 1810, když zařízení spouští pořadí úkolů a potřebuje získat obsah, použije chování skupiny hranic podobné jako klient Configuration Manager. Další informace najdete v tématu [Podpora pořadí úkolů pro skupiny hranic](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).<!--1359025-->  

10. Pokud chcete tato nastavení uložit, abyste ho mohli znovu použít, na kartě **Souhrn** vyberte **Uložit jako šablonu**. Zadejte název šablony a vyberte nastavení, které chcete uložit.  

11. Dokončete průvodce.  

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Nasazení místního upgradu Windows 10 přes CMG

<!-- 1357149 -->
Pořadí úkolů místního upgradu Windows 10 podporuje nasazení do internetových klientů spravovaných prostřednictvím [brány pro správu cloudu](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG). Tato možnost umožňuje vzdáleným uživatelům snadněji upgradovat na Windows 10, aniž by se museli připojit k intranetu.

Zajistěte, aby veškerý obsah odkazovaný pořadím úkolů místního upgradu byl distribuován do CMG s povoleným obsahem. (Povolte [Nastavení CMG](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings): **Povolit, aby CMG fungoval jako distribuční bod cloudu a poskytoval obsah z Azure Storage**.) Můžete také použít [cloudový distribuční bod](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Jinak zařízení nemůžou pořadí úkolů Spustit.

Když nasadíte pořadí úkolů upgradu, použijte následující nastavení:

- **Povolí spuštění pořadí úkolů pro klienta na internetu**na kartě činnost koncového uživatele v nasazení.  

- Na kartě distribuční body v nasazení vyberte jednu z následujících možností:

  - **Pokud to vyžaduje běžící pořadí úloh, Stáhněte si obsah lokálně**. Počínaje verzí 1910 může stroj sekvence úloh stahovat balíčky na vyžádání z CMG s povoleným obsahem nebo z cloudového distribučního bodu. Tato změna poskytuje větší flexibilitu pro nasazení místního upgradu Windows 10 na Internetová zařízení.<!--3601238-->

  - **Před spuštěním pořadí úloh stáhnout veškerý obsah místně**. V Configuration Manager verze 1906 a starší, další možnosti, jako je například **Stažení obsahu místně, pokud to vyžaduje běžící pořadí úloh** , v tomto scénáři nefungují. Modul pořadí úloh nemůže stáhnout obsah ze zdroje cloudu. Klient Configuration Manager musí před spuštěním pořadí úloh stáhnout obsah ze zdroje cloudu. Tuto možnost můžete v případě potřeby použít ve verzi 1910, pokud je to nutné pro splnění vašich požadavků.

- (*Volitelné*) **Předem stáhnout obsah pro toto pořadí úloh**na kartě Obecné v nasazení. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](configure-precache-content.md).  

> [!NOTE]
> Spusťte pořadí úloh z centra softwaru. Tento scénář nepodporuje médium s Windows PE, PXE nebo pořadím úkolů.

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a>Nasazení s vysokým rizikem

Při nasazení s vysokým rizikem, jako je například operační systém, se v okně **Vybrat kolekci** zobrazují pouze vlastní kolekce, které splňují nastavení ověřování nasazení, které jsou konfigurovány ve vlastnostech lokality. Vysoce riziková nasazení se vždy omezují na vlastní kolekce, kolekce, které vytvoříte, a na vestavěnou kolekci **Neznámé počítače**. Když vytvoříte vysoce rizikové nasazení, nemůžete vybrat vestavěnou kolekci, například **všechny systémy**. Chcete-li zobrazit všechny vlastní kolekce, které obsahují méně klientů, než je nakonfigurovaná maximální velikost, zakažte možnost **Skrýt kolekce s počtem členů větším, než je konfigurace minimální velikosti webu**. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Nastavení ověřování nasazení jsou založena na aktuálním členství kolekce. Po nasazení pořadí úloh Configuration Manager nevyhodnotí členství v kolekci pro nastavení nasazení s vysokým rizikem.  

Řekněme například, že jste nastavili **výchozí velikost** na 100 a **maximální velikost** na 1000. Když vytvoříte nasazení s vysokým rizikem, zobrazí se v okně **Vybrat kolekci** pouze kolekce, které obsahují méně než 100 klientů. Pokud zrušíte zaškrtnutí políčka **Skrýt kolekce s počtem členů větším, než je nastavení konfigurace minimální velikosti webu** , zobrazí se v okně kolekce, které obsahují méně než 1000 klientů.  

Když vyberete kolekci, která obsahuje roli lokality, platí následující chování:  

- Pokud kolekce obsahuje server systému lokality a nakonfigurovali jste nastavení ověřování nasazení pro blokování kolekcí se servery systému lokality, dojde k chybě. Nemůžete pokračovat ve vytváření nasazení.  

- Pokud platí jedno z následujících kritérií, Průvodce nasazením softwaru zobrazí upozornění s vysokým rizikem. Chcete-li pokračovat, je nutné souhlasit s vytvořením vysoce rizikového nasazení. Lokalita vygeneruje zprávu o stavu auditu.  

  - Pokud kolekce obsahuje server systému lokality a nakonfigurovali jste nastavení ověřování nasazení tak, aby se zobrazovalo upozornění na kolekce se servery systému lokality  

  - Pokud kolekce překročí výchozí hodnotu velikosti

  - Pokud kolekce obsahuje server  

## <a name="see-also"></a>Viz také

[Správa pořadí úkolů pro automatizaci úloh](manage-task-sequences-to-automate-tasks.md)
