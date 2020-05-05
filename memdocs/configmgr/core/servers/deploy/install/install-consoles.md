---
title: Nainstalovat konzolu
titleSuffix: Configuration Manager
description: Nainstalujte konzolu Configuration Manager pro připojení k lokalitě centrální správy nebo k primární lokalitě.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718235"
---
# <a name="install-the-configuration-manager-console"></a>Instalace konzoly Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Správci používají konzolu Configuration Manager ke správě prostředí Configuration Manager. Každá konzola Configuration Manager se může připojit k lokalitě centrální správy (CAS) nebo k primární lokalitě. Nemůžete připojit konzolu Configuration Manager k sekundární lokalitě.

Konzola Configuration Manager je vždy nainstalována na serveru lokality pro certifikační autority nebo primární lokalitu. Chcete-li nainstalovat konzolu nástroje, která je oddělena od instalace serveru lokality, spusťte samostatný instalační program.  



## <a name="prerequisites"></a>Požadavky

- Máte práva místního **správce** pro cílový počítač pro konzolu nástroje.  

- Máte oprávnění **ke čtení** pro umístění instalačních souborů konzoly Configuration Manager.  



## <a name="source-paths"></a>Zdrojové cesty

Rozhodněte, kterou zdrojovou cestu použít:  

- ConsoleSetup složka na serveru lokality:`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Při instalaci serveru lokality se zkopírují instalační soubory konzoly nástroje a podporované jazykové sady pro lokalitu do podsložky **Tools\ConsoleSetup** . Volitelně můžete zkopírovat složku **ConsoleSetup** do alternativního umístění a spustit instalaci. Když aktualizujete lokalitu, vždy udržuje místní verzi v aktuálním stavu.  

- Configuration Manager instalační médium:`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Instalace konzoly Configuration Manager z instalačního média vždy nainstaluje anglickou verzi. K tomuto chování dochází i v případě, že server lokality podporuje různé jazyky, nebo je operační systém cílového počítače nastaven na jiný jazyk.  

Pokud je to možné, spusťte instalační program konzoly ze složky **ConsoleSetup** , nikoli ze zdrojového média.

> [!Important]  
> Konzolu neinstalujte pomocí **disku CD-ROM. Nejnovější** zdrojové soubory. Jedná se o nepodporovaný scénář a může způsobit problémy s instalací konzoly. Další informace najdete [na disku CD. Poslední složka](../../manage/the-cd.latest-folder.md#unsupported-scenarios)<!-- SCCMDocs issue 1359 -->  

Pokud vytvoříte balíček pro instalaci konzoly nástroje do jiných počítačů, ujistěte se, že balíček obsahuje následující soubory:<!--3612513-->

- ConsoleSetup. exe
- AdminConsole. msi
- ConfigMgr. AC_Extension. i386. CAB (počínaje verzí 1902)
- ConfigMgr. AC_Extension. amd64. CAB (počínaje verzí 1902)



## <a name="use-the-setup-wizard"></a>Použití průvodce instalací  

1. Přejděte do cesty ke zdroji a otevřete soubor **ConsoleSetup. exe**.  

    > [!IMPORTANT]  
    > Konzolu nástroje vždy nainstalujte pomocí **ConsoleSetup. exe**. I když můžete nainstalovat konzolu Configuration Manager spuštěním souboru AdminConsole. msi, tato metoda nespouští požadavky nebo kontroly závislostí. Instalace se nemusí nainstalovat správně.  

2. V průvodci vyberte **Další**.  

3. Na stránce **Server lokality** zadejte plně kvalifikovaný název domény (FQDN) serveru lokality, ke které se připojí konzola Configuration Manager.  

4. Na stránce **instalační složka** zadejte instalační složku pro konzolu Configuration Manager. Cesta ke složce nesmí obsahovat koncové mezery ani znaky Unicode.  

5. Na stránce **Program zlepšování softwaru a služeb na základě zkušeností uživatelů** vyberte, jestli se má připojit k program Zlepšování softwaru A služeb na základě zkušeností uživatelů (CEIP).  

    > [!Note]  
    > Configuration Manager počínaje verzí 1802 je funkce CEIP z produktu odebrána.

6. Na stránce **připraveno k instalaci** vyberte **instalovat**.  



## <a name="install-from-a-command-prompt"></a>Instalace z příkazového řádku  

> [!TIP]  
> Instalace konzoly Configuration Manager z příkazového řádku vždy nainstaluje anglickou verzi. K tomuto chování dochází i v případě, že je operační systém cílového počítače nastavený na jiný jazyk. Chcete-li nainstalovat konzolu Configuration Manager v jiném jazyce než angličtině, [použijte Průvodce instalací](#use-the-setup-wizard)nástroje.  


### <a name="consolesetupexe-command-line-options"></a>ConsoleSetup. exe – možnosti příkazového řádku

#### <a name="q"></a>/q

Nainstaluje konzolu Configuration Manager bezobslužně. Při použití této možnosti jsou vyžadovány možnosti **EnableSQM**, **targetDir**a **DefaultSiteServerName** .

#### <a name="uninstall"></a>/uninstall

Odinstaluje konzolu Configuration Manager. Tuto možnost zadejte jako první, když ji použijete s možností **/q** .

#### <a name="langpackdir"></a>LangPackDir

Určuje cestu ke složce, která obsahuje soubory jazyka. Ke stažení jazykových souborů můžete použít nástroj pro stažení **instalačního programu** . Pokud tuto možnost nepoužijete, instalační program vyhledá složku jazyka v aktuální složce. Pokud se složka jazyka nenajde, instalační program bude i nadále instalovat pouze angličtinu. Další informace najdete v tématu Nástroj pro [stažení instalačního programu](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Určuje instalační složku pro instalaci konzoly Configuration Manager. Tato možnost je vyžadována, pokud použijete možnost **/q** .

#### <a name="enablesqm"></a>EnableSQM

Určuje, jestli se má připojit k program Zlepšování softwaru a služeb na základě zkušeností uživatelů (CEIP). K programu CEIP se připojte pomocí hodnoty **1** a hodnotou **0** se připojte k programu. Tato možnost je vyžadována, pokud použijete možnost **/q** .

> [!Important]  
> Configuration Manager počínaje verzí 1802 je funkce CEIP z produktu odebrána. Použití parametru způsobí, že se instalace nezdaří.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Určuje plně kvalifikovaný název domény serveru lokality, ke kterému se konzola připojí, když se otevře. Tato možnost je vyžadována, pokud použijete možnost **/q** .


### <a name="examples"></a>Příklady

> [!Important]  
> Pro verzi 1802 a novější nezahrnujte parametr **EnableSQM** .

#### <a name="silent-install"></a>Bezobslužná instalace

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Tichá instalace pomocí jazykových sad

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Bezobslužná odinstalace

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Viz také

Správce uvidí objekty v konzole na základě oprávnění přiřazených ke svému uživatelskému účtu. Další informace najdete v tématu [základy správy na základě rolí](../../../understand/fundamentals-of-role-based-administration.md).

Další informace o tom, jaké jsou základy navigace v konzole Configuration Manager, najdete v tématu [použití konzoly](../../manage/admin-console.md).
