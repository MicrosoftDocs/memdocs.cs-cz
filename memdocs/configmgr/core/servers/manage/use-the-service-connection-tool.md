---
title: Nástroj pro připojení služby
titleSuffix: Configuration Manager
description: Přečtěte si o tomto nástroji, který vám umožní připojit se ke cloudové službě Configuration Manager a ručně odeslat informace o využití.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b56b849be6abd2634e29d35e58494d4d3215857
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126082"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Použití nástroje pro připojení služby pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud je spojovací bod služby v režimu offline, použijte **Nástroj pro připojení služby** . Můžete ji použít i v případě, že servery systému lokality Configuration Manager nejsou připojené k Internetu. Tento nástroj vám může přispět k aktuálnosti vašeho webu s nejnovějšími aktualizacemi pro Configuration Manager.

Když nástroj spustíte, připojí se ke cloudové službě Configuration Manager, nahraje informace o využití vaší hierarchie a stáhne aktualizace. Odesílání dat o využití je potřeba, aby cloudová služba mohla poskytovat správné aktualizace pro vaše prostředí.

## <a name="prerequisites"></a>Požadavky

- Lokalita má bod připojení služby a konfiguruje ji pro **offline připojení na vyžádání**.

- Spusťte nástroj z příkazového řádku jako správce. Neexistuje žádné uživatelské rozhraní.

- Nástroj spustíte ze spojovacího bodu služby a počítače, který se může připojit k Internetu. Každý z těchto počítačů musí mít 64bitový operační systém a musí mít následující součásti:

  - Soubory **Distribuovatelných součástí Visual C++** x86 a x64. Ve výchozím nastavení Configuration Manager nainstaluje verzi x64 do počítače, který je hostitelem spojovacího bodu služby. Chcete-li stáhnout tuto součást, přečtěte si téma [Visual C++ distribuovatelných balíčků pro Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784).

  - **.NET Framework 4.5.2** nebo novější

- Účet, který použijete ke spuštění nástroje, potřebuje následující oprávnění:

  - **Místní správce** v počítači, který je hostitelem spojovacího bodu služby

  - Oprávnění **ke čtení** pro databázi lokality

- Potřebujete metodu přenosu souborů mezi počítačem s přístupem k Internetu a spojovacím bodem služby. Například jednotka USB s dostatkem volného místa pro uložení souborů a aktualizací.

## <a name="overview"></a>Přehled

1. **Příprava**: Spusťte nástroj ve spojovacím bodě služby. Data o využití se umístí do souboru. cab v umístění, které zadáte. Zkopírujte datový soubor do počítače s připojením k Internetu.

2. **Připojit**: Spusťte nástroj na počítači s připojením k Internetu. Nahraje data o využití a pak stáhne Configuration Manager aktualizace. Zkopírujte stažené aktualizace do spojovacího bodu služby.

    Můžete nahrát několik datových souborů najednou, z různých hierarchií. Můžete také zadat proxy server a uživatele pro proxy server.

3. **Import**: Spusťte nástroj ve spojovacím bodě služby. Naimportuje aktualizace a přidá je do vašeho webu. [Tyto aktualizace](install-in-console-updates.md) pak můžete zobrazit a nainstalovat v konzole Configuration Manager.

### <a name="upload-multiple-data-files"></a>Nahrávání více datových souborů

- Všechny exportované datové soubory umístěte z různých hierarchií do stejné složky. Každému souboru zadejte jedinečný název. V případě potřeby je můžete ručně přejmenovat.

- Když spustíte nástroj pro nahrání dat společnosti Microsoft, zadáte složku, která obsahuje datové soubory.

- Když spustíte nástroj pro import dat, nástroj importuje pouze data pro tuto hierarchii.

### <a name="specify-a-proxy-server"></a>Zadejte proxy server

Pokud počítač s připojením k Internetu vyžaduje proxy server, nástroj podporuje základní konfiguraci proxy serveru. Použijte volitelné parametry **-proxyserveruri** a **-proxyusername**. Další informace najdete v tématu [parametry příkazového řádku](#bkmk_cmd).

### <a name="specify-the-type-of-updates-to-download"></a>Zadejte typ aktualizací, které se mají stáhnout.

Nástroj podporuje možnosti, které určují, jaké soubory se mají stáhnout. Ve výchozím nastavení nástroj stáhne pouze nejnovější dostupnou aktualizaci, která se vztahuje na verzi vaší lokality. Nestahují opravy hotfix.

Chcete-li toto chování změnit, použijte jeden z následujících parametrů pro změnu souborů, které stahuje:

- **-DownloadAll**: Stáhněte všechny aktualizace včetně aktualizací a oprav hotfix bez ohledu na verzi vaší lokality.
- **-downloadhotfix**: Stáhněte všechny opravy hotfix bez ohledu na verzi vašeho webu.
- **-downloadsiteversion**: stáhne aktualizace a opravy hotfix s novější verzí, než je verze vašeho webu.

    > [!IMPORTANT]
    > Kvůli známému problému ve verzi Configuration Manager 2002 není výchozí chování fungovat podle očekávání. Aktualizujte na verzi 2006 nebo pomocí parametru **-downloadsiteversion** stáhněte potřebné aktualizace verze 2002.<!-- 7594517 -->

Další informace najdete v tématu [parametry příkazového řádku](#bkmk_cmd).

> [!TIP]
> Nástroj určuje verzi vašeho webu z datového souboru. Verzi ověříte tak, že v souboru. cab vyhledáte textový soubor s názvem s verzí webu.

## <a name="use-the-tool"></a>Použití nástroje  

Nástroj pro připojení služby je v instalačním médiu Configuration Manager v následující cestě: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe` . Vždy používejte Nástroj pro připojení služby, který odpovídá používané verzi Configuration Manager. Všechny tyto soubory musí být ve stejné složce, aby nástroj pro připojení služby fungoval.

Zkopírujte složku **ServiceConnectionTool** s veškerým jejím obsahem do počítače s připojením k Internetu.

V tomto postupu používají příklady příkazového řádku následující názvy souborů a umístění složek. Tyto cesty a názvy souborů nemusíte používat. Můžete použít alternativy, které odpovídají vašemu prostředí a předvolbách.

- Cesta ke zdrojovému instalačnímu souboru médií Configuration Manager ve spojovacím bodu služby:`C:\Source`

- Cesta k jednotce USB, kam ukládáte data pro přenos mezi počítači:`D:\USB\`

- Název datového souboru, který exportujete z lokality:`UsageData.cab`

- Název prázdné složky, do které nástroj ukládá stažené aktualizace pro Configuration Manager:`UpdatePacks`

### <a name="prepare"></a>Příprava

1. V počítači, který je hostitelem spojovacího bodu služby, otevřete příkazový řádek jako správce a změňte adresář na umístění nástroje. Například:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Spuštěním následujícího příkazu Připravte datový soubor:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Pokud budete nahrávat datové soubory z více než jedné hierarchie současně, poskytněte každému datovému souboru jedinečný název. V případě potřeby můžete soubory přejmenovat později.

    Data v souboru jsou založená na úrovni diagnostických dat a dat o využití, která pro lokalitu nakonfigurujete. Další informace najdete v tématu [Přehled diagnostiky a dat o využití](../../plan-design/diagnostics/diagnostics-and-usage-data.md). Pomocí tohoto nástroje můžete exportovat data do souboru CSV a zobrazit obsah. Další informace najdete v tématu [-Export](#-export).

1. Poté, co nástroj dokončí export dat o použití, zkopírujte datový soubor do počítače, který má přístup k Internetu.

### <a name="connect"></a>Připojit

1. Na počítači s přístupem k Internetu otevřete příkazový řádek jako správce a změňte adresář na umístění nástroje. Toto umístění je kopií celé složky **ServiceConnectionTool** . Například:

    `cd D:\USB\ServiceConnectionTool\`

1. Spuštěním následujícího příkazu nahrajte datový soubor a stáhněte Configuration Manager aktualizace:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Další příklady najdete v tématu [parametry příkazového řádku](#bkmk_cmd).

    > [!NOTE]  
    > Při spuštění tohoto příkazového řádku se může zobrazit následující chyba:
    >
    > **Neošetřená výjimka: System. UnauthorizedAccessException: přístup k cestě ' C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql ' byl odepřen.**
    >
    > Tuto chybu můžete bezpečně ignorovat. Pokud chcete pokračovat, zavřete okno chyb.

1. Poté, co nástroj dokončí stahování aktualizací, je zkopírujte do spojovacího bodu služby.

### <a name="import"></a>Import

1. V počítači, který je hostitelem spojovacího bodu služby, otevřete příkazový řádek jako správce a změňte adresář na umístění nástroje. Například:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Spuštěním následujícího příkazu importujte aktualizace:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. Po dokončení importu Zavřete příkazový řádek. Importuje pouze aktualizace pro příslušnou hierarchii.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **aktualizace a údržba** . Importované aktualizace jsou teď dostupné k instalaci. Další informace najdete v tématu [instalace konzolových aktualizací](install-in-console-updates.md).

## <a name="log-files"></a>Soubory protokolu

- **ServiceConnectionTool. log**: pokaždé, když spustíte nástroj pro připojení služby, se zapisuje do tohoto souboru protokolu. Cesta k souboru protokolu je vždy stejné jako nástroj. Tento soubor protokolu poskytuje jednoduché podrobnosti o využití nástroje na základě parametrů, které používáte. Při každém spuštění tohoto nástroje se nahradí existující soubor protokolu.

- **ConfigMgrSetup. log**: během fáze [připojení](#connect) nástroj zapisuje do tohoto souboru protokolu v kořenovém adresáři systémového disku. Tento soubor protokolu poskytuje podrobnější informace. Například jaké soubory nástroj stáhne a zda jsou kontroly hodnoty hash úspěšné.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a>Parametry příkazového řádku

V této části jsou uvedeny v abecedním pořadí všechny dostupné parametry pro nástroj pro připojení služby.

### <a name="-connect"></a>– připojit

Použijte během fáze [připojení](#connect) na počítači s přístupem k Internetu. Připojuje se ke cloudové službě Configuration Manager, aby mohl nahrát datový soubor a stahovat aktualizace.

Vyžaduje následující parametry:

- **-usagedatasrc**: umístění datového souboru, který se má nahrát.
- **-updatepackdest**: cesta ke staženým aktualizacím

Můžete použít také následující volitelné parametry:

- **-proxyserveruri**: plně kvalifikovaný název domény proxy server
- **-proxyusername**: uživatelské jméno pro proxy server
- **-DownloadAll**: Stáhněte si všechno, včetně aktualizací a oprav hotfix, bez ohledu na verzi vaší lokality.
- **-downloadhotfix**: Stáhněte všechny opravy hotfix bez ohledu na verzi vašeho webu.
- **-downloadsiteversion**: Stáhněte aktualizace a opravy hotfix, které mají novější verzi než verze vašeho webu.

#### <a name="example-of-connect-without-a-proxy-server"></a>Příklad připojení bez proxy server

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Příklad připojení pomocí proxy server

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Příklad připojení ke stažení jenom pro verzi webu použitelné aktualizace

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-cíl

Požadovaný parametr s parametrem **-Export** pro zadání cesty a názvu souboru CSV, který se má exportovat. Další informace najdete v tématu [-Export](#-export).

### <a name="-downloadall"></a>-downloadall

Volitelný parametr s parametrem **-Connect** ke stažení všeho, včetně aktualizací a oprav hotfix, bez ohledu na verzi vaší lokality. Další informace najdete v tématu [– připojení](#connect).

### <a name="-downloadhotfix"></a>-downloadhotfix

Volitelný parametr s parametrem **-Connect** , aby se stáhly jenom všechny opravy hotfix bez ohledu na verzi vašeho webu. Další informace najdete v tématu [– připojení](#-connect).

### <a name="-downloadsiteversion"></a>-downloadsiteversion

Volitelný parametr s parametrem **-Connect** , aby bylo možné stahovat pouze aktualizace a opravy hotfix, které mají novější verzi než verze vašeho webu. Další informace najdete v tématu [– připojení](#-connect).

### <a name="-export"></a>– Export

Použijte během fáze [přípravy](#prepare) k exportu údajů o využití do souboru CSV. Spusťte ji jako správce spojovacího bodu služby. Tato akce vám umožní zkontrolovat obsah údajů o využití před nahráním do Microsoftu. K určení umístění souboru CSV vyžaduje parametr **-cíl** .

#### <a name="example-of-export"></a>Příklad exportu

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-Import

Použijte během fáze [importu](#import) u spojovacího bodu služby k importu aktualizací do lokality. K určení umístění stažených aktualizací vyžaduje parametr **-updatepacksrc** .

#### <a name="example-of-import"></a>Příklad importu

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>– Příprava

Použijte během fáze [přípravy](#prepare) u spojovacího bodu služby k exportu údajů o využití z lokality. K určení umístění exportovaného datového souboru vyžaduje parametr **-usagedatadest** .

#### <a name="example-of-prepare"></a>Příklad přípravy

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>– proxyserveruri

Volitelný parametr s parametrem **-Connect** pro určení plně kvalifikovaného názvu domény vašeho proxy server. Další informace najdete v tématu [– připojení](#-connect).

### <a name="-proxyusername"></a>– proxyusername

Volitelný parametr s parametrem **-Connect** pro určení uživatelského jména k ověření pomocí proxy server. Další informace najdete v tématu [– připojení](#-connect).

### <a name="-updatepackdest"></a>– updatepackdest

Požadovaný parametr s parametrem **-Connect** , který určuje cestu pro stažené aktualizace. Další informace najdete v tématu [– připojení](#-connect).

### <a name="-updatepacksrc"></a>– updatepacksrc

Požadovaný parametr s parametrem **-Import** , který určuje cestu stažených aktualizací. Další informace najdete v tématu [-Import](#-import).

### <a name="-usagedatadest"></a>– usagedatadest

Požadovaný parametr s parametrem **-Prepare** pro určení cesty a názvu souboru exportovaného datového souboru. Další informace najdete v tématu [– Příprava](#-prepare).

## <a name="next-steps"></a>Další kroky

[Instalace konzolových aktualizací](install-in-console-updates.md)

[Jak zobrazit data o využití a diagnostiku](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
