---
title: Možnosti ve verzi Technical Preview 1611
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1611.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721546"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1611 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*



V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1611. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    

**Známé problémy v této verzi Technical Preview:**   
- ***Stav splnění požadavků***: při instalaci verze 1611 se může zobrazit celkový stav požadovaných součástí s upozorněními, ale neuvádí, které požadavky způsobily upozornění. To může být způsobeno následujícími dvěma požadavky:
  - Možnosti vytvoření paměti SQL indexu
  - Kontroluje podporovanou verzi SQL Server.  

  Vzhledem k tomu, že se jedná jenom o upozornění, můžou se ignorovat.

- ***PowerShell***: když se připojíte k prostředí Windows PowerShell z konzoly Configuration Manager, může se zobrazit následující chyba: **Microsoft. ConfigurationManagement. PowerShell. Types. ps1xml není digitálně podepsán**.  

   Tento problém můžete vyřešit tak, že nahradíte některé soubory s podepsanými verzemi z verze 1610. Zkopírujte všechny soubory s následujícími příponami z ** &lt;instalačního adresáře> složce\\ \adminconsole\bin** v instalaci verze 1610: **. psd1**, **. ps1xml**a **. psm1**. Vložte tyto soubory do ** &lt;instalačního adresáře> složce\\ \adminconsole\bin** v instalaci Technical Preview 1611 a přepíše verzi 1611 souborů.


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Obsah předběžné mezipaměti pro dostupná nasazení a pořadí úkolů
V této verzi Technical Preview můžete pro dostupná nasazení a sekvence úloh použít funkci předběžného ukládání do mezipaměti, aby klienti stáhli jenom relevantní obsah, než uživatel nainstaluje obsah.

Řekněme například, že chcete nasadit pořadí úkolů místního upgradu Windows 10, chcete mít jenom jedno pořadí úloh pro všechny uživatele a máte víc architektur a/nebo jazyků. Pokud v Current Branch vytvoříte dostupné nasazení a pak uživatel klikne na **instalovat** v centru softwaru, obsah se v tomto okamžiku stáhne. Tím přidáte další čas před tím, než bude instalace připravena k zahájení. Případně můžete v Current Branch při vytváření dostupného nasazení pořadí úloh stáhnout veškerý obsah, na který pořadí úkolů odkazuje. To zahrnuje balíček s upgradem operačního systému pro všechny jazyky a architektury. Pokud má každá velikost přibližně 3 GB, může být balíček pro stahování poměrně velký.

Funkce obsahu před ukládáním do mezipaměti vám dává možnost dovolit, aby klient stahovat jenom příslušný obsah hned po přijetí nasazení. Proto když uživatel klikne na **instalovat** v centru softwaru, obsah je připravený a instalace se spustí rychle, protože obsah je na místním pevném disku.

### <a name="to-configure-the-pre-cache-feature"></a>Konfigurace funkce před ukládáním do mezipaměti

1. Vytvořte balíčky s upgradem operačního systému pro konkrétní architektury a jazyky. Určete architekturu a jazyk na kartě **zdroj dat** balíčku. Pro jazyk použijte převod desetinných míst (například 1033 je desetinné číslo pro angličtinu a 0x0409 je šestnáctkový ekvivalent). Podrobnosti najdete v tématu [Vytvoření pořadí úkolů pro upgrade operačního systému](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

    Hodnoty architektury a jazyka se používají ke spárování podmínek kroku pořadí úloh, které vytvoříte v dalším kroku, abyste zjistili, jestli by měl být balíček s upgradem operačního systému předem uložený v mezipaměti.
2. Vytvořte pořadí úkolů s podmíněnými kroky pro různé jazyky a architektury. Například pro anglickou verzi byste mohli vytvořit krok podobný následujícímu:

    ![vlastnosti před ukládáním do mezipaměti](media/precacheproperties2.png)

    ![možnosti před ukládáním do mezipaměti](media/precacheoptions2.png)  

3. Nasaďte pořadí úkolů. Pro funkci pre-cache nakonfigurujte následující nastavení:
    - Na kartě **Obecné** vyberte **předem stáhnout obsah pro toto pořadí úloh**.
    - Na kartě **nastavení nasazení** nakonfigurujte pořadí úkolů tak, aby bylo **dostupné** pro **účely**. Pokud vytvoříte **požadované** nasazení, funkce předběžného ukládání do mezipaměti nebude fungovat.
    - Na kartě **plánování** v části plán, **kdy bude toto nasazení k dispozici** , vyberte čas v budoucnosti, který klientům poskytne dostatek času na předběžné ukládání obsahu do mezipaměti, než bude nasazení zpřístupněno uživatelům. Můžete například nastavit dostupný čas na 3 hodiny v budoucnu, aby bylo možné dostatek času na to, aby byl obsah před uložením do mezipaměti.  
    - Na kartě **distribuční body** nakonfigurujte nastavení **možností nasazení** . Pokud obsah není předem uložen v mezipaměti klienta předtím, než uživatel spustí instalaci, tato nastavení se použijí.


### <a name="user-experience"></a>Uživatelské prostředí
- Když klient obdrží zásadu nasazení, začne obsah předem ukládat do mezipaměti. To zahrnuje veškerý odkazovaný obsah (všechny typy balíčků) a jenom balíček s upgradem operačního systému, který odpovídá klientovi na základě podmínek, které jste nastavili v pořadí úkolů.
- Když je nasazení zpřístupněno pro uživatele (nastavení na kartě **plánování** v nasazení), zobrazí se oznámení upozorňující uživatele na nové nasazení a nasazení bude viditelné v centru softwaru. Uživatel může přejít do centra softwaru a kliknutím na tlačítko **nainstalovat** spustit instalaci.
- Pokud obsah není zcela uložen do mezipaměti, bude používat nastavení zadané na kartě **Možnosti nasazení** v nasazení. Doporučujeme, abyste měli dostatek času mezi vytvořením nasazení a časem, kdy bude nasazení k dispozici pro uživatele, aby měli klienti dostatek času na předběžné ukládání obsahu do mezipaměti.


## <a name="see-also"></a>Viz také
[Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md)
