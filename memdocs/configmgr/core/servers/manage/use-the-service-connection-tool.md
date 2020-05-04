---
title: Nástroj pro připojení služby
titleSuffix: Configuration Manager
description: Přečtěte si o tomto nástroji, který vám umožní připojit se ke cloudové službě Configuration Manager a ručně odeslat informace o využití.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e535653e0f31e186a6bdbde8da77750f2afdfdb0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710815"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Použití nástroje pro připojení služby pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Použijte **Nástroj pro připojení služby** , když je spojovací bod služby v režimu offline nebo když vaše servery systému lokality Configuration Manager nejsou připojené k Internetu. Tento nástroj vám může přispět k aktuálnosti vašeho webu s nejnovějšími aktualizacemi pro Configuration Manager.  

Při spuštění se nástroj ručně připojí ke cloudové službě Configuration Manager, aby mohl odeslat informace o využití vaší hierarchie a stáhnout aktualizace. Odesílání dat o využití je potřeba, aby mohla cloudová služba poskytnout správné aktualizace pro vaše nasazení.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Předpoklady použití nástroje pro připojení služby
Následují předpoklady a známé problémy.

**Požadovaný**

- Máte nainstalovaný spojovací bod služby, který je nastavený na možnost **Offline, připojení na vyžádání**.  

- Nástroj se musí spustit z příkazového řádku.  

- Každý počítač, ve kterém se nástroj spustí (počítač se spojovacím bodem služby a počítač připojený k internetu), musí mít systém pro platformu x64 a musí mít nainstalované tyto položky:  

  - Soubory **Distribuovatelných součástí Visual C++** x86 a x64.   Ve výchozím nastavení Configuration Manager nainstaluje verzi x64 do počítače, který je hostitelem spojovacího bodu služby.  

    Chcete-li stáhnout kopii souborů Visual C++, přejděte na stránku [Balíčky distribuovatelných součástí Visual C++ pro Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) na webu Microsoft Download Center.  

  - .NET Framework 4.5.2 nebo novější.  

- Účet, který používáte ke spouštění nástroje, musí mít:
  - Oprávnění**místního správce** v počítači, který je hostitelem spojovacího bodu služby (ve kterém se nástroj spouští).
  - Oprávnění**Číst** k databázi lokality.  



- Budete potřebovat jednotku USB s dostatečným volným místem pro uložení souborů a aktualizací nebo jiný způsob přenosu souborů mezi počítačem se spojovacím bodem služby a počítačem, který má přístup k internetu. (Tento scénář vychází z předpokladu, že vaše lokalita a spravované počítače nemají přímé připojení k internetu.)  



## <a name="use-the-service-connection-tool"></a>Použití nástroje pro připojení služby  

 Nástroj pro připojení služby (**serviceconnectiontool. exe**) najdete na instalačním médiu Configuration Manager ve složce **%path%\smssetup\tools\ServiceConnectionTool** . Vždy používejte Nástroj pro připojení služby, který odpovídá používané verzi Configuration Manager.


 V tomto postupu se v příkladech příkazového řádku používají následující názvy souborů a umístění složek (tyto cesty a názvy souborů nemusíte použít, můžete je nahradit alternativami, které odpovídají vašemu prostředí a předvolbám):  

- Cesta k jednotce USB, na které jsou uložená data pro přenos mezi servery: **D:\USB\\**  

- Název souboru .cab, který obsahuje data exportovaná z lokality: **UsageData.cab**  

- Název prázdné složky, do které se uloží stažené aktualizace nástroje Configuration Manager pro přenos mezi servery: **UpdatePacks**  

V počítači, který je hostitelem spojovacího bodu služby:  

- Otevřete příkazový řádek s oprávněními správce a poté změňte adresáře na umístění, které obsahuje nástroj **serviceconnectiontool.exe**.  

  Ve výchozím nastavení můžete tento nástroj najít na instalačním médiu Configuration Manager ve složce **%path%\smssetup\tools\ServiceConnectionTool** . Všechny soubory v této složce musí být ve stejné složce, aby nástroj pro připojení služby fungoval.  

Když spustíte následující příkaz, nástroj připraví soubor .cab, který obsahuje informace o využití, a zkopíruje ho do zadaného umístění. Data v souboru .cab jsou založená na úrovni diagnostických dat o využití, které je lokalita nakonfigurovaná shromažďovat. (viz [data o využití a Diagnostika pro Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Spusťte následující příkaz pro vytvoření souboru .cab:  

- **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Také je třeba zkopírovat složku ServiceConnectionTool s veškerým jejím obsahem na jednotku USB nebo ji jinak zpřístupnit v počítači, který budete používat pro kroky 3 a 4.  

### <a name="overview"></a>Přehled
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>Existují tři hlavní kroky pro použití nástroje pro připojení služby.  

1.  **Příprava**: Tento krok je spuštěn v počítači, který je hostitelem spojovacího bodu služby. Když je nástroj spuštěný, převede data o využití do souboru. cab a uloží ho na jednotku USB (nebo do jiného umístění pro přenos, které zadáte).  

2.  **Připojit**: pro účely tohoto kroku spustíte nástroj ve vzdáleném počítači, který se připojuje k Internetu, abyste mohli nahrát data o využití a pak stahovat aktualizace.  

3.  **Importovat**: Tento krok běží na počítači, který je hostitelem spojovacího bodu služby. Při spuštění nástroj importuje aktualizace, které jste stáhli, a přidá je do vaší lokality, abyste je mohli zobrazit a nainstalovat z konzoly Configuration Manager.  

Počínaje verzí 1606 můžete při připojení k Microsoftu odeslat více souborů .cab najednou (každý z jiné hierarchie) a zadat proxy server a uživatele pro proxy server.   

#### <a name="to-upload-multiple-cab-files"></a>Nahrání více souborů. cab
- Umístěte všechny soubory .cab exportované z jednotlivých hierarchií do stejné složky. Název každého souboru musí být jedinečný, v případě potřeby je můžete ručně přejmenovat.
- Následně při spuštění příkazu k odeslání dat do Microsoftu zadejte složku obsahující soubory .cab. (Před aktualizací 1606 bylo možné odeslat data pouze z jedné hierarchie najednou, a nástroj vyžadoval zadání názvu souboru .cab ve složce)
- Později, když spustíte úlohu importu na spojovacím bodu služby v hierarchii, nástroj automaticky importuje pouze data pro danou hierarchii.  

#### <a name="to-specify-a-proxy-server"></a>Určení proxy server
Pomocí následujících volitelných parametrů můžete zadat proxy server (Další informace o používání těchto parametrů najdete v oddílu Parametry příkazového řádku v tomto tématu):
- **-proxyserveruri [FQDN_of_proxy_server]**  Pomocí tohoto parametru můžete určit proxy server, který se má použít pro toto připojení.
- **-proxyusername [uživatelské_jméno]**  Tento parametr použijte v případě, že musíte zadat uživatele pro proxy server.

#### <a name="specify-the-type-of-updates-to-download"></a>Zadejte typ aktualizací, které se mají stáhnout.
Od verze 1706 se změnila výchozí chování nástrojů a nástroj podporuje možnosti, které určují, jaké soubory si stáhnete.
- Ve výchozím nastavení nástroj stáhne pouze nejnovější dostupnou aktualizaci, která se vztahuje na verzi vaší lokality. Nestahují opravy hotfix.

Chcete-li toto chování změnit, použijte jeden z následujících parametrů pro změnu souborů, které jsou staženy. 

> [!NOTE]
> Verze vaší lokality se určí z dat v souboru. cab, který se nahraje při spuštění nástroje.
>
> Verzi můžete ověřit tak, že v souboru. cab vyhledáte soubor *SiteVersion*. txt.

- **– DownloadAll**  Tato možnost stáhne vše, včetně aktualizací a oprav hotfix, bez ohledu na verzi vaší lokality.
- **– downloadhotfix**  Tato možnost stáhne všechny opravy hotfix bez ohledu na verzi vašeho webu.
- **– downloadsiteversion**  Tato možnost stáhne aktualizace a opravy hotfix, jejichž verze je vyšší než verze vaší lokality.

Příklad příkazového řádku, který používá *-downloadsiteversion*:
- **serviceconnectiontool. exe-Connect *-downloadsiteversion* -usagedatasrc D:\USB-updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Postup použití nástroje pro připojení služby  

1. V počítači, který je hostitelem spojovacího bodu služby:  

   - Otevřete příkazový řádek s oprávněními správce a poté změňte adresáře na umístění, které obsahuje nástroj **serviceconnectiontool.exe**.   

2. Spusťte následující příkaz, aby nástroj připravil soubor .cab, který obsahuje informace o využití, a zkopíroval ho do zadaného umístění:  

   - **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   Pokud odesíláte soubory .cab z více než jedné hierarchie najednou, musí mít každý soubor .cab ve složce jedinečný název. Soubory, které přidáte do složky, můžete ručně přejmenovat.

   Chcete-li zobrazit informace o využití, které se shromáždily k odeslání do cloudové služby nástroje Configuration Manager, spusťte následující příkaz, který data exportuje do souboru .csv, který následně můžete zobrazit pomocí aplikace, jako je Excel:  

   - **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. Až dokončíte přípravný krok, připojte jednotku USB (nebo jinak přeneste exportovaná data) k počítači, který má přístup k internetu.  

4. Na počítači s přístupem k internetu otevřete příkazový řádek s oprávněním správce a poté změňte adresáře na umístění, které obsahuje kopii nástroje  **serviceconnectiontool.exe** a další soubory z této složky.  

5. Spuštěním následujícího příkazu zahajte odesílání informací o využití a stahování aktualizací pro Configuration Manager:  

   - **serviceconnectiontool. exe-Connect-usagedatasrc D:\USB-updatepackdest D:\USB\UpdatePacks**

   Další příklady tohoto příkazového řádku najdete v oddílu [Možnosti příkazového řádku](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) dále v tomto tématu.

   > [!NOTE]  
   >  Při spuštění příkazového řádku pro připojení ke cloudové službě Configuration Manageru se může zobrazit chyba podobná této:  
   >   
   > - Neošetřená výjimka: System.UnauthorizedAccessException:  
   >   
   >      Přístup k cestě C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql byl odepřen.  
   >   
   > Tuto chybu můžete bezpečně ignorovat, zavřít okno chyby a pokračovat.  

6. Po stažení aktualizací pro Configuration Manager připojte jednotku USB (nebo jinak přeneste exportovaná data) k počítači, který je hostitelem spojovacího bodu služby.  

7. Na počítači, který je hostitelem spojovacího bodu služby, otevřete příkazový řádek s oprávněním správce, změňte adresáře na umístění, které obsahuje nástroj **serviceconnectiontool.exe**, a poté spusťte následující příkaz:  

   - **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. Po dokončení importu můžete příkazový řádek zavřít. (Importují se pouze aktualizace pro příslušnou hierarchii).  

9. Otevřete konzolu Configuration Manager a přejděte do části **Správa** > **aktualizace a údržba**. Importované aktualizace jsou teď dostupné k instalaci. (Před verzí 1702 se aktualizace a údržba **Administration** > **Cloud Services**.)

   Informace o instalaci aktualizací najdete v tématu [instalace konzolových aktualizací pro Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="log-files"></a><a name="bkmk_cmd"></a>Soubory protokolu

**ServiceConnectionTool. log**

Pokaždé, když spustíte nástroj pro připojení služby, se soubor protokolu vygeneruje ve stejném umístění jako nástroj s názvem **ServiceConnectionTool. log**.  Tento soubor protokolu poskytne jednoduché informace o spuštění nástroje na základě toho, jaké příkazy se používají.  Existující soubor protokolu bude nahrazen při každém spuštění nástroje.

**ConfigMgrSetup.log**

Při použití nástroje k připojení a stažení aktualizací se soubor protokolu vygeneruje v kořenovém adresáři systémové jednotky s názvem **ConfigMgrSetup. log**.  Tento soubor protokolu vám poskytne podrobnější informace, například jaké soubory se stáhnou, extrahují a jestli jsou kontroly hash úspěšné.

## <a name="command-line-options"></a><a name="bkmk_cmd"></a> Možnosti příkazového řádku  
Chcete-li zobrazit informace o nástroji spojovacího bodu služby, otevřete příkazový řádek ve složce, která nástroj obsahuje, a spusťte tento příkaz:  **serviceconnectiontool.exe**.  


|Možnosti příkazového řádku|Podrobnosti|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [jednotka:][cesta][název_souboru.cab]**|Tento příkaz uloží aktuální data o využití do souboru .cab.<br /><br /> Spusťte tento příkaz jako **místní správce** na serveru, který je hostitelem spojovacího bodu služby.<br /><br /> Příklad:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [jednotka:][cesta] -updatepackdest [jednotka:][cesta] -proxyserveruri [plně kvalifikovaný název domény proxy serveru] -proxyusername [uživatelské jméno]** <br /> <br /> Pokud používáte nástroj Configuration Manager verze nižší než 1606, musíte zadat název souboru .cab, a nemůžete použít možnosti pro proxy server.  Podporované parametry příkazu jsou: <br /> **-connect -usagedatasrc [jednotka:][cesta][název souboru] -updatepackdest [jednotka:][cesta]** |Tento příkaz se připojí ke cloudové službě nástroje Configuration Manager, odešle soubory .cab s daty o využití ze zadaného umístění a stáhne dostupné balíčky aktualizace a obsah konzoly. Možnosti pro proxy servery jsou volitelné.<br /><br /> Spusťte tento příkaz jako **místní správce** na počítači, který se může připojit k internetu.<br /><br /> Příklad připojení bez proxy serveru: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Příklad připojení s použitím proxy serveru: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Pokud používáte verzi nižší než 1606, musíte zadat název souboru .cab, a nemůžete použít možnosti pro proxy server. Použijte následující příklad příkazového řádku: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [jednotka:][cesta]**|Tento příkaz importuje balíčky aktualizací a obsah konzoly, které jste předtím stáhli do konzoly Configuration Manageru.<br /><br /> Spusťte tento příkaz jako **místní správce** na serveru, který je hostitelem spojovacího bodu služby.<br /><br /> Příklad:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [jednotka:][cesta][název_souboru.csv]**|Tento příkaz exportuje data o využití do souboru .csv, který potom můžete zobrazit.<br /><br /> Spusťte tento příkaz jako **místní správce** na serveru, který je hostitelem spojovacího bodu služby.<br /><br /> Příklad: **-export -dest D:\USB\usagedata.csv**|  
