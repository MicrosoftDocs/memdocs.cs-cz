---
title: Informace o souborech protokolu
titleSuffix: Configuration Manager
description: Pomocí souborů protokolu můžete řešit problémy s Configuration Manager klienty a systémy lokality.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6be23adc7ac082545bffeef59ed52d3455d9931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720300"
---
# <a name="about-log-files-in-configuration-manager"></a>Soubory protokolu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager komponenty klienta a webového serveru zaznamenávají informace o procesu do jednotlivých souborů protokolu. Informace v těchto protokolových souborech vám můžou pomoct při řešení problémů, ke kterým může dojít. Ve výchozím nastavení Configuration Manager povolí protokolování pro klientské a serverové součásti.

Tento článek poskytuje obecné informace o souborech protokolu Configuration Manager. Obsahuje nástroje, které je potřeba použít, jak nakonfigurovat protokoly a kde je najít. Další informace o konkrétních souborech protokolu najdete v tématu [Referenční dokumentace souborů protokolu](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a>Jak to funguje

Většina procesů v Configuration Manager zapisuje provozní informace do souboru protokolu, který je vyhrazen pro daný proces. Soubory protokolu jsou označeny příponami **. log** nebo **. LO_** . Configuration Manager zapisuje do souboru. log, dokud protokol nedosáhne své maximální velikosti. Když je protokol plný, soubor. log se zkopíruje do souboru se stejným názvem, ale s příponou. lo_, a proces nebo součást pokračuje v zapisování do souboru. log. Když soubor. log znovu dosáhne své maximální velikosti, soubor. lo_ se přepíše a proces se opakuje. Některé součásti vytváří historii souborů protokolu připojením data a časového razítka k názvu souboru protokolu a udržováním přípony. log.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a>Nástroje prohlížeče protokolů

Všechny soubory protokolu Configuration Manager jsou prostého textu, takže je můžete zobrazit s libovolným čtečkou textu, jako je Poznámkový blok. Protokoly používají jedinečné formátování, které se nejlépe zobrazuje s jedním z následujících specializovaných nástrojů:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Prohlížeč protokolů Support Center](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Chcete-li zobrazit protokoly, použijte nástroj Prohlížeč protokolu Configuration Manager **CMTrace**. Je umístěný ve `\SMSSetup\Tools` složce zdrojového média Configuration Manager. Nástroj CMTrace se přidá do všech spouštěcích imagí, které jsou přidány do knihovny softwaru. Nástroj pro zobrazení protokolu CMTrace je automaticky nainstalován společně s klientem Configuration Manager.<!--1357971--> Další informace najdete v tématu [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

Počínaje verzí 1906 je **OneTrace** nový prohlížeč protokolů s nástrojem Support Center. Funguje podobně jako CMTrace, s vylepšeními. Další informace najdete v tématu [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Prohlížeč protokolů Support Center

**Support Center** zahrnuje moderní prohlížeč protokolů. Tento nástroj nahrazuje CMTrace a poskytuje přizpůsobitelné rozhraní s podporou karet a oken ukotvit. Má rychlou prezentační vrstvu a dokáže načíst velké soubory protokolů během několika sekund. Další informace najdete v tématu [Přehled nástroje Support Center Log Viewer](../../support/support-center-ui-reference.md#bkmk_log-viewer).

> [!Note]  
> Support Center a OneTrace use Windows Presentation Foundation (WPF). Tato součást není k dispozici v systému Windows PE. Nadále používat CMTrace ve spouštěcích bitových kopiích s nasazeními pořadí úloh.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a>Konfigurace možností protokolování

Můžete změnit konfiguraci souborů protokolu, například úroveň podrobností, velikost a historii. Tato nastavení můžete změnit několika způsoby:

- [Během instalace klienta](#bkmk_logoptions-clientprop)
- [Použití Configuration Manager Service Manager](#bkmk_logoptions-sm)
- [Použití registru Windows](#bkmk_logoptions-registry)
- [V konzole Configuration Manager](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a>Konfigurovat možnosti protokolování při instalaci klienta

Během instalace můžete nastavit konfiguraci souborů protokolu klienta. Použijte následující vlastnosti:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Další informace najdete v tématu [vlastnosti instalace klienta](../../clients/deploy/about-client-installation-properties.md#clientMsiProps).

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a>Konfigurace možností protokolování pomocí Configuration Manager Service Manager

Můžete změnit, kde Configuration Manager ukládá soubory protokolů a jejich velikost.  

Chcete-li změnit velikost souborů protokolu, změnit název a umístění souboru protokolu nebo vynutit, aby bylo možné zapsat více součástí do jednoho souboru protokolu, proveďte následující kroky:  

#### <a name="modify-logging-for-a-component"></a>Úprava protokolování pro komponentu  

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **stav systému**a pak vyberte uzel stav **lokality** nebo **Stav součásti** .  

2. Na pásu karet vyberte možnost **Start**a poté vyberte možnost **Configuration Manager Service Manager**.  

3. Po otevření Configuration Manager Service Manager se připojte k lokalitě, kterou chcete spravovat. Pokud není zobrazena lokalita, kterou chcete spravovat, vyberte možnost **lokalita**, vyberte možnost **připojit**a pak zadejte název serveru lokality pro správnou lokalitu.  

4. Rozbalte lokalitu a potom na **součásti** nebo **servery**podle toho, kde se nacházejí součásti, které chcete spravovat.  

5. Na pravém panelu vyberte jednu nebo víc součástí.  

6. V nabídce **Komponenta** vyberte **protokolování**.  

7. V dialogovém okně **Protokolování součásti nástroje Configuration Manager** dokončete výběr dostupných možností konfigurace pro váš výběr.  

8. Kliknutím na **OK** uložte konfiguraci.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a>Konfigurace možností protokolování pomocí registru Windows

<!-- SCCMDocs#992 -->
Pomocí registru systému Windows na serverech nebo klientech změňte následující možnosti protokolování:

- Úroveň podrobností
- Maximální historie
- Maximální velikost

Při řešení potíží můžete povolit podrobné protokolování pro Configuration Manager a zapsat další podrobnosti do souborů protokolu.

> [!Warning]
> Nespravovaná konfigurace těchto nastavení může způsobit, Configuration Manager bude protokolovat velké množství informací, nebo žádný vůbec. I když můžou být tato data pro řešení potíží výhodná, buďte opatrní při změně těchto hodnot v produkčních lokalitách. Vždy otestujte tyto změny v testovacím prostředí jako první. Může dojít k nadměrnému protokolování, které by mohlo ztížit nalezení relevantních informací v souborech protokolu.

Až provedete změny těchto nastavení registru, restartujte součást:

- Pokud změníte nastavení klienta, restartujte službu **Hostitel agenta serveru SMS** (Ccmexec).
- Pokud změníte nastavení serveru, restartujte službu **SMS Executive** .

Nastavení registru se liší v závislosti na komponentě:

- [Klient a bod správy](#bkmk_reg-client)
- [Server lokality](#bkmk_reg-site)
- [Role systému lokality](#bkmk_reg-role)
- [Konzola Configuration Manager](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a>Možnosti protokolování klienta a bodu správy

Chcete-li nakonfigurovat možnosti protokolování pro všechny součásti v systému lokality klienta nebo bodu správy, nakonfigurujte tyto **REG_DWORD** hodnoty v následujícím klíči registru systému Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Název  |Hodnoty  |Popis  |
|---------|---------|---------|
|LogLevel|`0`: Verbose<br>`1`: Výchozí<br>`2`: Upozornění a chyby<br>`3`: Pouze chyby|Úroveň podrobností, která se má zapsat do souborů protokolu.|
|LogMaxHistory|Libovolné celé číslo větší nebo rovno nule, například:<br>`0`: Žádná historie<br>`1`: Výchozí|Když soubor protokolu dosáhne maximální velikosti, klient ho přejmenuje jako zálohu a vytvoří nový soubor protokolu. Zadejte, kolik předchozích verzí má být zachováno.|
|LogMaxSize|Libovolné celé číslo větší než nebo rovno 10 000, například:<br>250000|Maximální velikost souboru protokolu v bajtech Když protokol naroste do zadané velikosti, klient ho přejmenuje jako soubor historie a vytvoří nový soubor. Výchozí hodnota je 250 000 bajtů.|

> [!Note]  
> Neměňte jiné hodnoty, které mohou existovat v tomto klíči registru.

Pro pokročilé ladění můžete také přidat tuto **REG_SZ** hodnotu pod následující klíč registru Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Název  |Hodnoty  |Popis  |
|---------|---------|---------|
|Povoleno | `True`: povolit protokoly ladění<br>`False`: zakázat protokoly ladění |Povolí protokolování ladění pro účely řešení potíží.|

Toto nastavení způsobí, že klient bude protokolovat informace nízké úrovně pro řešení potíží. Vyhněte se použití tohoto nastavení v produkčních lokalitách. Může dojít k nadměrnému protokolování, které by mohlo ztížit nalezení relevantních informací v souborech protokolu. Po vyřešení tohoto problému Nezapomeňte toto nastavení vypnout.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a>Možnosti protokolování serveru lokality

Nastavení můžete nakonfigurovat globálně nebo pro konkrétní komponentu na serveru lokality Configuration Manager.

Tyto hodnoty nakonfigurujte v následujícím klíči registru Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Název  |Hodnoty  |Typ  |Popis
|---------|---------|---------|---------|
|SqlEnabled| `1`: povolit trasování SQL<br> `0`: zakázat trasování SQL |REG_DWORD|Přidejte protokolování trasování SQL do všech protokolů serveru lokality.|
|ArchiveEnabled| `1`: Povolit archivy protokolů<br> `0`: zakázat archivy protokolů | REG_DWORD |Archivujte protokoly webového serveru do samostatného umístění pro historické uchovávání.|
|ArchivePath| Platná cesta ke složce, například`C:\Logs\Archive` | REG_SZ |Cesta k archivaci protokolů serveru lokality.|

Povolit pouze trasování SQL pro účely řešení potíží. Nepoužívejte ho v produkčních lokalitách. Může dojít k nadměrnému protokolování, které by mohlo ztížit nalezení relevantních informací v souborech protokolu. Po vyřešení tohoto problému Nezapomeňte toto nastavení vypnout.

> [!Note]  
> Neměňte jiné hodnoty, které mohou existovat v tomto klíči registru.

Pokud chcete nakonfigurovat možnosti protokolování pro konkrétní součást serveru, nakonfigurujte tyto **REG_DWORD** hodnoty v následujícím klíči registru Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Název  |Hodnoty  |Popis  |
|---------|---------|---------|
|LoggingLevel|`0`: Verbose<br>`1`: Výchozí<br>`2`: Upozornění a chyby<br>`3`: Pouze chyby|Úroveň podrobností, která se má zapsat do souborů protokolu.|
|LogMaxHistory|Libovolné celé číslo větší nebo rovno nule, například:<br>`0`: Žádná historie<br>`1`: Výchozí|Když soubor protokolu dosáhne maximální velikosti, server ho přejmenuje jako zálohu a vytvoří nový soubor protokolu. Zadejte, kolik předchozích verzí má být zachováno.|
|MaxFileSize|Libovolné celé číslo větší než nebo rovno 10 000, například:<br>250000|Maximální velikost souboru protokolu v bajtech Když protokol naroste do zadané velikosti, klient ho přejmenuje jako soubor historie a vytvoří nový soubor. Výchozí hodnota je 250 000 bajtů.|
|DebugLogging| `1`: povolit protokoly ladění<br>`0`: zakázat protokoly ladění |Povolí protokolování ladění pro účely řešení potíží.|

Nastavení DebugLogging způsobí, že server bude protokolovat informace na nízké úrovni pro řešení potíží. Vyhněte se použití tohoto nastavení v produkčních lokalitách. Může dojít k nadměrnému protokolování, které by mohlo ztížit nalezení relevantních informací v souborech protokolu. Po vyřešení tohoto problému Nezapomeňte toto nastavení vypnout.

> [!Note]  
> Neměňte jiné hodnoty, které mohou existovat v tomto klíči registru.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a>Možnosti protokolování role systému lokality

Nastavení můžete nakonfigurovat globálně nebo pro konkrétní součást systému lokality, která je hostitelem role serveru Configuration Manager.

Pokud chcete nakonfigurovat možnosti protokolování pro konkrétní součást serveru, nakonfigurujte tyto **REG_DWORD** hodnoty v následujícím klíči registru Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Například pro roli distribučního bodu:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Název  |Hodnoty  |Popis  |
|---------|---------|---------|
|LogLevel|`0`: Verbose<br>`1`: Výchozí<br>`2`: Upozornění a chyby<br>`3`: Pouze chyby|Úroveň podrobností, která se má zapsat do souborů protokolu.|
|LogMaxHistory|Libovolné celé číslo větší nebo rovno nule, například:<br>`0`: Žádná historie<br>`1`: Výchozí|Když soubor protokolu dosáhne maximální velikosti, server ho přejmenuje jako zálohu a vytvoří nový soubor protokolu. Zadejte, kolik předchozích verzí má být zachováno.|
|LogMaxSize|Libovolné celé číslo větší než nebo rovno 10 000, například:<br>250000|Maximální velikost souboru protokolu v bajtech Když se protokol zvětší na zadanou velikost, server ho přejmenuje jako soubor historie a vytvoří nový soubor. Výchozí hodnota je 250 000 bajtů.|

> [!Note]  
> Neměňte jiné hodnoty, které mohou existovat v tomto klíči registru.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a>Možnosti protokolování Configuration Manager konzoly

Chcete-li změnit úroveň podrobností protokolu AdminUI. log pro konzolu Configuration Manager, použijte následující postup:

1. Otevřete konfigurační soubor konzoly **Microsoft. ConfigurationManagement. exe. config**v editoru XML, jako je Poznámkový blok. Výchozí konfigurační soubor je v následujícím umístění:`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. V rámci**zdrojového** **elementu zdroje** >  **System. Diagnostics** > změňte atribut **určit atributy switchValue** z `Error` na `Verbose`. Příklad:

    Původní: `<source name="SmsAdminUISnapIn" switchValue="Error">` nové:`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Uložte soubor a restartujte konzolu.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a>Konfigurace možností protokolování v konzole Configuration Manager

<!-- 4433455 -->

Od verze 1910 povolte nebo zakažte podrobné protokolování pro klienta nebo kolekci z konzoly:

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , vyberte uzel **zařízení** a zvolte cílové zařízení.

1. Na pásu karet na kartě **Domů** ve skupině **zařízení** vyberte **Diagnostika klienta**. Vyberte jednu z dostupných akcí.

Další informace najdete v tématu [Diagnostika klientů](../../clients/manage/client-notification.md#client-diagnostics).

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a>Vyhledání souborů protokolu

Configuration Manager a závislé součásti uchovávají soubory protokolu v různých umístěních. Tato umístění závisí na procesu, který vytváří soubor protokolu a konfiguraci vašeho prostředí.

Výchozí hodnoty jsou následující umístění. Pokud jste ve svém prostředí přizpůsobili instalační adresáře, můžou se skutečné cesty lišit.

- Služba`C:\Windows\CCM\logs`
- WebServer`C:\Program Files\Microsoft Configuration Manager\Logs`
- Bod správy:`C:\SMS_CCM\Logs`
- Konzola Configuration Manager:`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog`
- SLUŽBU`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Umístění protokolu pořadí úloh

Umístění souboru protokolu pořadí úloh **souboru Smsts. log** se liší v závislosti na fázi pořadí úkolů:

- V systému Windows PE před [formátováním a krokem disku oddílu](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) : `X:\Windows\temp\smstslog\smsts.log` (X je jednotka RAM systému Windows PE)
- V systému Windows PE po **formátování a kroku disku oddílu** : `X:\smstslog\smsts.log`, zkopírováno `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` do, když je jednotka připravena
- V novém operačním systému Windows před instalací klienta:`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- V systému Windows po instalaci klienta:`C:\Windows\CCM\Logs\smstslog\smsts.log`
- V systému Windows po dokončení pořadí úloh:`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> Proměnná pořadí úkolů jen pro čtení [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) vždy obsahuje cestu k aktuálnímu souboru protokolu.


## <a name="see-also"></a>Viz také

- [Reference souborů protokolu](log-files.md)

- [OneTrace Support Center](../../support/support-center-onetrace.md)

- [Prohlížeč souborů protokolu Support Center](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
