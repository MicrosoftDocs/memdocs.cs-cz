---
title: Možnosti příkazového řádku instalačního programu
titleSuffix: Configuration Manager
description: Vytvořte skripty pro automatizaci k instalaci Configuration Manager z příkazového řádku.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718249"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Možnosti příkazového řádku pro instalační program Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Následující informace použijte ke konfiguraci skriptů nebo k instalaci Configuration Manager z příkazového řádku.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a>Možnosti příkazového řádku pro instalační program

Spusťte instalační program z `\BIN\X64` adresáře Configuration Manager instalační cestu na serveru lokality.

### `/DEINSTALL`

Odinstalujte lokalitu. Spusťte instalační program z počítače serveru lokality.  

### `/DONTSTARTSITECOMP`

Nainstalujte lokalitu, ale zabrání spuštění služby Správce součástí lokality. Dokud se služba Správce součástí lokality nespustí, lokalita není aktivní. Správce součástí lokality zodpovídá za instalaci a spuštění služby SMS_Executive a pro další procesy v lokalitě. Po dokončení instalace lokality se při spuštění služby Správce součástí lokality nainstaluje Služba SMS_Executive a další procesy, které jsou nezbytné k tomu, aby lokalita fungovala.  

### `/HIDDEN`

Skrýt uživatelské rozhraní během instalace. Tuto možnost použijte pouze ve spojení s možností **/Script** . Soubor skriptu bezobslužné instalace musí poskytovat všechny požadované možnosti, jinak se instalace nezdařila.  

### `/NOUSERINPUT`

Zakažte vstup uživatele během instalace, ale zobrazí se Průvodce instalací nástroje. Tuto možnost použijte pouze ve spojení s možností **/Script** . Soubor skriptu bezobslužné instalace musí poskytovat všechny požadované možnosti, jinak se instalace nezdařila.  

### `/RESETSITE`

Spusťte resetování lokality, která obnoví databázi a účty služeb pro lokalitu.

Další informace najdete v tématu [spuštění resetování lokality](../../manage/modify-your-infrastructure.md#bkmk_reset).  

### `/TESTDBUPGRADE`

Spusťte test na zálohování databáze lokality, abyste se ujistili, že se databáze může upgradovat.

> [!IMPORTANT]  
> Nespouštějte tuto možnost příkazového řádku v databázi produkčního webu. Spuštění této možnosti příkazového řádku v databázi produkční lokality provede upgrade databáze lokality a může způsobit nefunkčnost vaší lokality.

#### <a name="usage"></a>Využití

Zadejte název instance a název databáze pro databázi lokality. Pokud zadáte pouze název databáze, instalační program použije výchozí název instance.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Spusťte bezobslužný upgrade lokality. Zadejte kód Product Key, včetně spojovníků (`-`). Zadejte také cestu k dříve staženým požadovaným souborům instalace.  

Další informace o požadovaných instalačních souborech najdete v tématu Nástroj pro [stažení instalačního programu](setup-downloader.md).  

#### <a name="usage"></a>Využití

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Spusťte bezobslužnou instalaci. Použijte inicializační soubor instalace s touto možností. Další informace o tom, jak spustit instalaci bez obsluhy, najdete v tématu [Instalace lokalit pomocí příkazového řádku](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Využití

`/SCRIPT <setup script path>`

### `/SDKINST`

Nainstalujte poskytovatele služby SMS v zadaném počítači. Zadejte plně kvalifikovaný název domény (FQDN) pro počítač poskytovatele serveru SMS. Další informace o poskytovateli serveru SMS najdete v tématu [plánování poskytovatele serveru SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Využití

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Odinstalujte poskytovatele služby SMS v zadaném počítači. Zadejte plně kvalifikovaný název domény pro počítač poskytovatele serveru SMS.  

#### <a name="usage"></a>Využití

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Spravujte jazyky, které jsou nainstalované na dříve nainstalované lokalitě. Zadejte umístění souboru skriptu jazyka, který obsahuje nastavení jazyka. Další informace najdete v části [Možnosti příkazového řádku pro správu jazyků](#bkmk_Lang) .  

#### <a name="usage"></a>Využití

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a>Možnosti příkazového řádku pro správu jazyků

### <a name="identification"></a>Identifikace

- **Název klíče:** Action  

    - **Požadováno:** Ano  

    - **Hodnoty:**`ManageLanguages`  

    - **Podrobnosti:** Spravuje podporu jazyka serveru, klienta a mobilního klienta v lokalitě.  

### <a name="options"></a>Možnosti

- **Název klíče:** AddServerLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky serveru, které budou k dispozici pro Configuration Manager konzolu, sestavy a objekty Configuration Manager. Ve výchozím nastavení je dostupná angličtina.  

- **Název klíče:** AddClientLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky, které budou k dispozici pro klientské počítače. Ve výchozím nastavení je dostupná angličtina.  

- **Název klíče:** DeleteServerLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky, které mají být odebrány a které již nebudou k dispozici pro Configuration Manager konzolu, sestavy a objekty Configuration Manager. Ve výchozím nastavení je dostupná angličtina, nemůžete ji odebrat.  

- **Název klíče:** DeleteClientLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky, které mají být odebrány a které již nebudou k dispozici pro klientské počítače. Ve výchozím nastavení je dostupná angličtina, nemůžete ji odebrat.  

- **Název klíče:** MobileDeviceLanguage  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda jsou nainstalovány jazyky klienta mobilního zařízení.  

- **Název klíče:** PrerequisiteComp  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Stáhnout  

        - `1`= Již staženo  

    - **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu `0`, instalační program soubory stáhne.  

- **Název klíče:** PrerequisitePath  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*cesta k instalaci požadovaných souborů*>  

    - **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a>Klíče souborů skriptu bezobslužné instalace

Následující části vám pomůžou vytvořit skript pro bezobslužnou instalaci. V seznamech se zobrazuje:

- Dostupné klávesy skriptu pro instalaci a jejich odpovídající hodnoty
- Pokud jsou požadovány
- Jaký typ instalace se používá
- Krátký popis klíče

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Bezobslužná instalace lokality centrální správy (CAS)

Následující podrobnosti použijte k instalaci certifikační autority pomocí souboru skriptu bezobslužné instalace.  

#### <a name="identification"></a>Identifikace

- **Název klíče:** Action  

    - **Požadováno:** Ano  

    - **Hodnoty:**`InstallCAS`  

    - **Podrobnosti:** Nainstaluje certifikační autority.  

- **Název klíče:** CDLatest  

    - **Požadováno:** Ano, pouze při použití média z disku CD. Poslední složka

    - **Hodnota**

        - `1`= používáte médium z CD. Nejnovější

        - Libovolná jiná hodnota než 1 = nepoužíváte disk CD. Nejnovější média

    - **Podrobnosti:** Při instalaci nebo obnovení primární lokality nebo certifikačních autorit a spuštění instalačního programu z disku CD-ROM. Nejnovější složku, zahrňte tento klíč a hodnotu. Tato hodnota informuje o nastavení, že používáte médium z CD. Nejnovější.

#### <a name="options"></a>Možnosti

- **Název klíče:** ProductID  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= platný kód Product Key s pomlčkami

        - `Eval`= Nainstalujte zkušební verzi Configuration Manager

    - **Podrobnosti:** Určuje kód Product Key instalace Configuration Manager, včetně pomlček.

- **Název klíče:** SiteCode  

    - **Požadováno:** Ano  

    - **Hodnoty:** <>*kód lokality* , například`ABC`

    - **Podrobnosti:** Určuje tři alfanumerické znaky, které jedinečně identifikují lokalitu ve vaší hierarchii.  

- **Název klíče:** Název webu  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název webu*>  

    - **Podrobnosti:** Určuje název tohoto webu.  

- **Název klíče:** SMSInstallDir  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*Configuration Manager cesta instalace*>  

    - **Podrobnosti:** Určuje instalační složku pro soubory Configuration Manager programu.  

- **Název klíče:** SDKServer  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*plně kvalifikovaný název domény poskytovatele služby SMS*>  

    - **Podrobnosti:** Udává plně kvalifikovaný název domény (FQDN) serveru, který bude hostitelem poskytovatele serveru SMS. Po počáteční instalaci lze nastavit další poskytovatele služeb SMS pro lokalitu.  

- **Název klíče:** PrerequisiteComp  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Stáhnout  

        - `1`= Již staženo  

    - **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu `0`, instalační program soubory stáhne.  

- **Název klíče:** PrerequisitePath  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*cesta k instalaci požadovaných souborů*>  

    - **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.  

- **Název klíče:** AdminConsole  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má nainstalovat konzola Configuration Manager.  

- **Název klíče:** JoinCEIP  

    > [!Note]  
    > Počínaje verzí Configuration Manager 1802 je funkce CEIP z produktu odebrána.

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Nepřipojovat  

        - `1`= Připojit  

    - **Podrobnosti:** Určuje, jestli se má připojit k program Zlepšování softwaru a služeb na základě zkušeností uživatelů (CEIP).  

- **Název klíče:** AddServerLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky serveru, které budou k dispozici pro Configuration Manager konzolu, sestavy a objekty Configuration Manager. Ve výchozím nastavení je dostupná angličtina.  

- **Název klíče:** AddClientLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky, které budou k dispozici pro klientské počítače. Ve výchozím nastavení je dostupná angličtina.  

- **Název klíče:** DeleteServerLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Po instalaci upraví lokalitu. Určuje jazyky, které mají být odebrány a které již nebudou k dispozici pro Configuration Manager konzolu, sestavy a objekty Configuration Manager. Ve výchozím nastavení je dostupná angličtina, nemůžete ji odebrat.  

- **Název klíče:** DeleteClientLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Po instalaci upraví lokalitu. Určuje jazyky, které mají být odebrány a které již nebudou k dispozici pro klientské počítače. Ve výchozím nastavení je dostupná angličtina, nemůžete ji odebrat.  

- **Název klíče:** MobileDeviceLanguage  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda jsou nainstalovány jazyky klienta mobilního zařízení.  

#### <a name="sqlconfigoptions"></a>MožnostiKonfSQL

- **Název klíče:** SQLServerName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název systému SQL Server*>  

    - **Podrobnosti:** Určuje název serveru nebo clusterované instance, která je spuštěna SQL Server pro hostování databáze lokality.  

- **Název klíče:** DatabaseName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název databáze lokality*> nebo název *instance*>\\<<název*databáze lokality*>  

    - **Podrobnosti:** Určuje název databáze SQL Server, která se má vytvořit, nebo databáze SQL Server, která se má použít, když instalační program nainstaluje databázi CAS.  

        > [!IMPORTANT]  
        > Pokud nepoužíváte výchozí instanci, zadejte název instance a název databáze lokality.  

- **Název klíče:** SQLSSBPort  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*číslo portu SSB*>  

    - **Podrobnosti:** Určuje port SQL Server Service Broker (SSB), který SQL Server používá. Ve výchozím nastavení používá SSB port TCP 4022, ale můžete použít jiný port.  

- **Název klíče:** SQLDataFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. mdb*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru. MDB databáze.  

- **Název klíče:** SQLLogFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. ldf*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru Database. ldf.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Název klíče:** CloudConnector  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má v této lokalitě nainstalovat bod připojení služby. Protože spojovací bod služby můžete nainstalovat jenom v lokalitě nejvyšší úrovně v hierarchii, nastavte tuto hodnotu na `1` pro podřízenou primární lokalitu.  

- **Název klíče:** CloudConnectorServer  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény serveru bodu připojení služby*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény serveru, který bude hostitelem role systému lokality spojovacího bodu služby.  

- **Název klíče:** UseProxy  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda spojovací bod služby používá proxy server.  

- **Název klíče:** Proxy server  

    - **Požadováno:** Požadováno, pokud se **UseProxy** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény proxy serveru*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény proxy server, který používá spojovací bod služby.  

- **Název klíče:** ProxyPort  

    - **Požadováno:** Požadováno, pokud se **UseProxy** rovná 1  

    - **Hodnoty:** <*číslo portu*>  

    - **Podrobnosti:** Určuje číslo portu, který se má použít pro port proxy serveru.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Název klíče:** SAActive

    - **Požadováno:** Ne

    - **Hodnota**

        - `0`= Software Assurance není k dispozici.

        - `1`= Je aktivní Software Assurance.

    - **Podrobnosti:** Určete, jestli máte aktivní Software Assurance. Další informace najdete v tématu [Nejčastější dotazy k produktu a licencování](../../../understand/product-and-licensing-faq.md).

- **Název klíče:** CurrentBranch

    - **Požadováno:** Ne

    - **Hodnota**

        - `0`= Nainstalovat LTSB

        - `1`= Instalovat aktuální větev

    - **Podrobnosti:** Určete, jestli se má použít Configuration Manager aktuální větev nebo LTSB (Long-Term Servicing Branch). Další informace najdete v tématu [kterou větev Configuration Manager mám použít?](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-install-for-a-primary-site"></a>Bezobslužná instalace pro primární lokalitu

Pomocí následujících informací můžete nainstalovat primární lokalitu pomocí souboru skriptu bezobslužné instalace.  

#### <a name="identification"></a>Identifikace

- **Název klíče:** Action  

    - **Požadováno:** Ano  

    - **Hodnoty:**`InstallPrimarySite`  

    - **Podrobnosti:** Nainstaluje primární lokalitu.  

- **Název klíče:** CDLatest  

    - **Požadováno:** Ano, pouze při použití média z disku CD. Poslední složka

    - **Hodnota**

        - `1`= používáte médium z CD. Nejnovější

        - Libovolná jiná hodnota než 1 = nepoužíváte disk CD. Nejnovější média

    - **Podrobnosti:** Při instalaci nebo obnovení primární lokality nebo certifikačních autorit a spuštění instalačního programu z disku CD-ROM. Nejnovější složku, zahrňte tento klíč a hodnotu. Tato hodnota informuje o nastavení, že používáte médium z CD. Nejnovější.

#### <a name="options"></a>Možnosti

- **Název klíče:** ProductID  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= platný kód Product Key s pomlčkami

        - `Eval`= Nainstalujte zkušební verzi Configuration Manager

    - **Podrobnosti:** Určuje kód Product Key instalace Configuration Manager, včetně pomlček.

- **Název klíče:** SiteCode  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*kód lokality*>  

    - **Podrobnosti:** Určuje tři alfanumerické znaky, které jedinečně identifikují lokalitu ve vaší hierarchii.  

- **Název klíče:** SiteName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název webu*>  

    - **Podrobnosti:** Určuje název tohoto webu.  

- **Název klíče:** SMSInstallDir  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*Configuration Manager cesta instalace*>

    - **Podrobnosti:** Určuje instalační složku pro soubory Configuration Manager programu.  

- **Název klíče:** SDKServer  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*plně kvalifikovaný název domény poskytovatele služby SMS*>  

    - **Podrobnosti:** Udává plně kvalifikovaný název domény (FQDN) serveru, který bude hostitelem poskytovatele serveru SMS. Po počáteční instalaci lze nastavit další poskytovatele služeb SMS pro lokalitu.  

- **Název klíče:** PrerequisiteComp  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Stáhnout  

        - `1`= Již staženo  

    - **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu `0`, instalační program soubory stáhne.  

- **Název klíče:** PrerequisitePath  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*cesta k instalaci požadovaných souborů*>  

    - **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.  

- **Název klíče:** AdminConsole  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má nainstalovat konzola Configuration Manager.  

- **Název klíče:** JoinCEIP  

    > [!Note]  
    > Počínaje verzí Configuration Manager 1802 je funkce CEIP z produktu odebrána.

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Nepřipojovat  

        - `1`= Připojit  

    - **Podrobnosti:** Určuje, zda se má připojit k programu CEIP.  

- **Název klíče:** ManagementPoint  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*plně kvalifikovaný název domény serveru lokality bodu správy*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény serveru, který bude hostitelem role systému lokality bodu správy.  

- **Název klíče:** ManagementPointProtocol  

    - **Požadováno:** Ne  

    - **Hodnoty:** `HTTPS` nebo`HTTP`  

    - **Podrobnosti:** Určuje protokol, který se má používat pro bod správy.  

- **Název klíče:** DistributionPoint  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*plně kvalifikovaný název domény serveru lokality distribučního bodu*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény serveru, který bude hostitelem role systému lokality distribučního bodu.  

- **Název klíče:** DistributionPointProtocol  

    - **Požadováno:** Ne  

    - **Hodnoty:** `HTTPS` nebo`HTTP`  

    - **Podrobnosti:** Určuje protokol, který se má použít pro distribuční bod.  

- **Název klíče:** Parametr rolecommunicationprotocol  

    - **Požadováno:** Ano  

    - **Hodnoty:** `EnforceHTTPS` nebo`HTTPorHTTPS`  

    - **Podrobnosti:** Určuje, jestli se mají nakonfigurovat všechny systémy lokality tak, aby přijímaly jenom komunikaci přes protokol HTTPS od klientů, nebo aby se nakonfigurovala metoda komunikace pro každou roli systému lokality. Když vyberete `EnforceHTTPS`, musí mít klienti platný certifikát PKI (Public Key Infrastructure) pro ověřování klientů.  

- **Název klíče:** Parametr clientsusepkicertificate  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Nepoužívat  

        - `1`= Použít  

    - **Podrobnosti:** Určuje, zda klienti použijí klientský certifikát PKI ke komunikaci s rolemi systému lokality.  

- **Název klíče:** AddServerLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky serveru, které budou k dispozici pro Configuration Manager konzolu, sestavy a objekty Configuration Manager. Ve výchozím nastavení je dostupná angličtina.  

- **Název klíče:** AddClientLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Určuje jazyky, které budou k dispozici pro klientské počítače. Ve výchozím nastavení je dostupná angličtina.  

- **Název klíče:** DeleteServerLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Po instalaci upraví lokalitu. Určuje jazyky, které mají být odebrány a které již nebudou k dispozici pro Configuration Manager konzolu, sestavy a objekty Configuration Manager. Ve výchozím nastavení je dostupná angličtina, nemůžete ji odebrat.  

- **Název klíče:** DeleteClientLanguages  

    - **Požadováno:** Ne  

    - **Hodnoty:** DEU, ru, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, rev nebo ZHH  

    - **Podrobnosti:** Po instalaci upraví lokalitu. Určuje jazyky, které mají být odebrány a které již nebudou k dispozici pro klientské počítače. Ve výchozím nastavení je dostupná angličtina, nemůžete ji odebrat.  

- **Název klíče:** MobileDeviceLanguage  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda jsou nainstalovány jazyky klienta mobilního zařízení.  

#### <a name="sqlconfigoptions"></a>MožnostiKonfSQL

- **Název klíče:** SQLServerName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název systému SQL Server*>  

    - **Podrobnosti:** Určuje název serveru nebo clusterované instance, která se spustí SQL Server pro hostování databáze lokality.  

- **Název klíče:** DatabaseName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název databáze lokality*> nebo název *instance*>\\<<název*databáze lokality*>  

    - **Podrobnosti:** Určuje název databáze SQL Server, která se má vytvořit, nebo databáze SQL Server, která se má použít při instalaci databáze primární lokality.  

        > [!IMPORTANT]  
        > Pokud nepoužíváte výchozí instanci, zadejte název instance a název databáze lokality.  

- **Název klíče:** SQLSSBPort  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*číslo portu SSB*>  

    - **Podrobnosti:** Určuje port SSB, který SQL Server používá. Ve výchozím nastavení používá SSB port TCP 4022, ale můžete použít jiný port.  

- **Název klíče:** SQLDataFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. mdb*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru. MDB databáze.  

- **Název klíče:** SQLLogFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. ldf*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru Database. ldf.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Název klíče:** CCARSiteServer  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*plně kvalifikovaný název domény lokality centrální správy*>  

    - **Podrobnosti:** Určuje CAS, ke kterým se primární lokalita připojí, když se připojí k hierarchii Configuration Manager. Určete certifikační autority během instalace.  

- **Název klíče:** CASRetryInterval  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*interval v minutách*>  

    - **Podrobnosti:** Určuje interval opakování pokusu o připojení k certifikačním autoritám po neúspěšném připojení v minutách. Například pokud připojení ke CAS dojde k chybě, primární lokalita počká na počet minut, který zadáte pro hodnotu **CASRetryInterval** , a pak se znovu pokusí o připojení.  

- **Název klíče:** WaitForCASTimeout  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*časový limit v minutách od 0 do 100*>  

    - **Podrobnosti:** Určuje maximální hodnotu časového limitu (v minutách), který má primární lokalita připojit k certifikační autoritě. Pokud se například primární lokalita nepřipojí k certifikační autoritě, primární lokalita se znovu pokusí připojit k certifikačním autoritám na základě hodnoty **CASRetryInterval** , dokud nedosáhne **parametru WaitForCASTimeout** období. Můžete zadat hodnotu z `0` do. `100`  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Název klíče:** CloudConnector  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má v této lokalitě nainstalovat bod připojení služby. Protože spojovací bod služby můžete nainstalovat jenom v lokalitě nejvyšší úrovně v hierarchii, nastavte tuto hodnotu na `0` pro podřízenou primární lokalitu.  

- **Název klíče:** CloudConnectorServer  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény serveru bodu připojení služby*\>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény serveru, který bude hostitelem role systému lokality spojovacího bodu služby.  

- **Název klíče:** UseProxy  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda spojovací bod služby používá proxy server.  

- **Název klíče:** Proxy server  

    - **Požadováno:** Požadováno, pokud se **UseProxy** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény proxy serveru*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény proxy server, který používá spojovací bod služby.  

- **Název klíče:** ProxyPort  

    - **Požadováno:** Požadováno, pokud se **UseProxy** rovná 1  

    - **Hodnoty:** <*číslo portu*>  

    - **Podrobnosti:** Určuje číslo portu, který se má použít pro port proxy serveru.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Název klíče:** SAActive

    - **Požadováno:** Ne

    - **Hodnota**

        - `0`= Software Assurance není k dispozici.

        - `1`= Je aktivní Software Assurance.

    - **Podrobnosti:** Určete, jestli máte aktivní Software Assurance. Další informace najdete v tématu [Nejčastější dotazy k produktu a licencování](../../../understand/product-and-licensing-faq.md).

- **Název klíče:** CurrentBranch

    - **Požadováno:** Ne

    - **Hodnota**

        - `0`= Nainstalovat LTSB

        - `1`= Instalovat aktuální větev

    - **Podrobnosti:** Určete, jestli se má použít Configuration Manager aktuální větev nebo LTSB (Long-Term Servicing Branch). Další informace najdete v tématu [kterou větev Configuration Manager mám použít?](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-recovery-for-a-cas"></a>Bezobslužné obnovení pro certifikační autority

Následující podrobnosti použijte k obnovení certifikačních autorit pomocí souboru skriptu bezobslužné instalace.  

#### <a name="identification"></a>Identifikace

- **Název klíče:** Action  

    - **Požadováno:** Ano  

    - **Hodnoty:**`RecoverCCAR`  

    - **Podrobnosti:** Obnoví CAS.  

- **Název klíče:** CDLatest  

    - **Požadováno:** Ano, pouze při použití média z disku CD. Poslední složka

    - **Hodnota**

        - `1`= používáte médium z CD. Nejnovější

        - Libovolná jiná hodnota než 1 = nepoužíváte disk CD. Nejnovější média

    - **Podrobnosti:** Při instalaci nebo obnovení primární lokality nebo certifikačních autorit a spuštění instalačního programu z disku CD-ROM. Nejnovější složku, zahrňte tento klíč a hodnotu. Tato hodnota informuje o nastavení, že používáte médium z CD. Nejnovější.

#### <a name="recoveryoptions"></a>MožnostiObnovení

- **Název klíče:** ServerRecoveryOptions  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `1`= Obnovit server lokality a SQL Server

        - `2`= Obnovit pouze server lokality

        - `4`= Obnovit pouze SQL Server  

    - **Podrobnosti:** Určuje, jestli instalační program obnoví server lokality, SQL Server, nebo obojí. Na základě zadané hodnoty jsou vyžadovány i následující možnosti:  

        - **1** nebo **2**: k obnovení lokality pomocí zálohy lokality zadejte hodnotu pro **klíče siteserverbackuplocation**. Pokud nezadáte žádnou hodnotu, instalační program znovu nainstaluje lokalitu bez obnovení ze zálohovacího skladu.  

        - **4**: klíč **BackupLocation** se vyžaduje při konfiguraci hodnoty **10** pro klíč **DatabaseRecoveryOptions** , který má obnovit databázi lokality ze zálohy.  

- **Název klíče:** DatabaseRecoveryOptions  

    - **Požadováno:** Tento klíč je vyžadován, pokud má nastavení **ServerRecoveryOptions** hodnotu **1** nebo **4**.  

    - **Hodnota**

        - `10`= Obnovit databázi lokality ze zálohy.  

        - `20`= Použít databázi lokality, kterou jste ručně obnovili s jinou metodou.  

        - `40`= Vytvořit novou databázi pro web. Tuto možnost použijte, pokud není k dispozici žádná záloha databáze lokality. Lokalita obnoví globální data a data lokality prostřednictvím replikace z jiných lokalit.  

        - `80`= Přeskočit obnovení databáze.  

    - **Podrobnosti:** Určuje způsob, jakým Instalační program obnovuje databázi lokality v SQL Server.  

- **Název klíče:** ReferenceSite  

    - **Požadováno:** Tento klíč je vyžadován, pokud má nastavení **DatabaseRecoveryOptions** hodnotu **40**.  

    - **Hodnoty:** <*plně kvalifikovaný název domény referenčního webu*>  

    - **Podrobnosti:** Pokud je záloha databáze starší než doba uchování dat sledování změn, nebo když obnovujete lokalitu bez zálohy, zadejte referenční primární lokalitu, kterou CAS používá k obnovení globálních dat.  

        Když neurčíte referenční lokalitu a záloha je starší než doba uchování dat sledování změn, všechny primární lokality se znovu dokončí obnovenými daty z certifikačních autorit.  

        Když neurčíte referenční lokalitu a záloha je v rámci doby uchování sledování změn, replikují se z primárních lokalit pouze změny provedené po zálohování. Pokud dojde ke konfliktům změn z různých primárních lokalit, certifikační autorita použije první z nich, kterou obdrží.  

- **Název klíče:** SiteServerBackupLocation  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k zálohovacímu skladu serveru lokality*>  

    - **Podrobnosti:** Udává cestu k zálohovacímu skladu serveru lokality. Tento klíč je volitelný při nastavení **ServerRecoveryOptions** na hodnotu **1** nebo **2**. K obnovení lokality pomocí zálohy lokality zadejte hodnotu klíče **SiteServerBackupLocation** . Pokud nezadáte žádnou hodnotu, instalační program znovu nainstaluje lokalitu bez obnovení ze zálohovacího skladu.  

- **Název klíče:** BackupLocation  

    - **Požadováno:** Tento klíč se vyžaduje, když nakonfigurujete hodnotu **1** nebo **4** pro klíč **ServerRecoveryOptions** a nakonfigurujete hodnotu **10** pro klíč **DatabaseRecoveryOptions** .  

    - **Hodnoty:** <*cesta k zálohovacímu skladu databáze lokality*>  

    - **Podrobnosti:** Udává cestu k zálohovacímu skladu databáze lokality.  

#### <a name="options"></a>Možnosti

- **Název klíče:** ProductID  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= platný kód Product Key s pomlčkami

        - `Eval`= Nainstalujte zkušební verzi Configuration Manager

    - **Podrobnosti:** Určuje kód Product Key instalace Configuration Manager, včetně pomlček.

- **Název klíče:** SiteCode  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*kód lokality*>  

    - **Podrobnosti:** Určuje tři alfanumerické znaky, které jedinečně identifikují lokalitu ve vaší hierarchii. Zadejte kód lokality, který byl použit lokalitou před chybou.

- **Název klíče:** SiteName  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*název webu*>  

    - **Podrobnosti:** Určuje název tohoto webu.  

- **Název klíče:** SMSInstallDir  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*Configuration Manager cesta instalace*>  

    - **Podrobnosti:** Určuje instalační složku pro soubory Configuration Manager programu.  

- **Název klíče:** SDKServer  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*plně kvalifikovaný název domény poskytovatele služby SMS*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény pro server, který je hostitelem poskytovatele služby SMS. Zadejte server, který hostuje poskytovatele služby SMS, před selháním.  

        Po počáteční instalaci můžete nakonfigurovat další poskytovatele služby SMS pro tuto lokalitu. Další informace o poskytovateli serveru SMS najdete v tématu [plánování poskytovatele serveru SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Název klíče:** PrerequisiteComp  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Stáhnout  

        - `1`= Již staženo  

    - **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu **0**, instalační program soubory stáhne.  

- **Název klíče:** PrerequisitePath  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*cesta k instalaci požadovaných souborů*>  

    - **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.  

- **Název klíče:** AdminConsole  

    - **Požadováno:** Tento klíč je vyžadován s výjimkou případů, kdy má nastavení **ServerRecoveryOptions** hodnotu **4**.  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má nainstalovat konzola Configuration Manager.  

- **Název klíče:** JoinCEIP  

    > [!Note]  
    > Počínaje verzí Configuration Manager 1802 je funkce CEIP z produktu odebrána.

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Nepřipojovat  

        - `1`= Připojit  

    - **Podrobnosti:** Určuje, zda se má připojit k programu CEIP.  

#### <a name="sqlconfigoptions"></a>MožnostiKonfSQL

- **Název klíče:** SQLServerName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název systému SQL Server*>  

    - **Podrobnosti:** Určuje název serveru nebo clusterované instance, která běží SQL Server a který hostuje databázi lokality. Zadejte stejný server, který hostuje databázi lokality před selháním.  

- **Název klíče:** DatabaseName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název databáze lokality*> nebo název *instance*>\\<<název*databáze lokality*>  

    - **Podrobnosti:** Určuje název databáze SQL Server, která se má vytvořit, nebo databáze SQL Server, která se má použít při instalaci databáze CAS. Zadejte stejný název databáze, který byl použit před selháním.  

        > [!IMPORTANT]  
        > Pokud nepoužíváte výchozí instanci, zadejte název instance a název databáze lokality.  

- **Název klíče:** SQLSSBPort  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*číslo portu SSB*>  

    - **Podrobnosti:** Určuje port SSB, který SQL Server používá. Ve výchozím nastavení používá SSB port TCP 4022. Zadejte stejný port SSB, který byl použit před selháním.  

- **Název klíče:** SQLDataFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. mdb*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru. MDB databáze.  

- **Název klíče:** SQLLogFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. ldf*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru Database. ldf.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Název klíče:** CloudConnector  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má v této lokalitě nainstalovat bod připojení služby. Protože spojovací bod služby můžete nainstalovat jenom v lokalitě nejvyšší úrovně v hierarchii, tato hodnota musí být **0** pro podřízenou primární lokalitu.  

- **Název klíče:** CloudConnectorServer  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény serveru bodu připojení služby*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény serveru, který bude hostitelem role systému lokality spojovacího bodu služby.  

- **Název klíče:** UseProxy  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda spojovací bod služby používá proxy server.  

- **Název klíče:** Proxy server  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény proxy serveru*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény proxy server, který používá spojovací bod služby.  

- **Název klíče:** ProxyPort  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*číslo portu*>  

    - **Podrobnosti:** Určuje číslo portu, který se má použít pro port proxy serveru.  

### <a name="unattended-recovery-for-a-primary-site"></a>Bezobslužné obnovení primární lokality

Pomocí následujících informací můžete obnovit primární lokalitu pomocí souboru skriptu bezobslužné instalace.  

#### <a name="identification"></a>Identifikace

- **Název klíče:** Action  

    - **Požadováno:** Ano  

    - **Hodnoty:**`RecoverPrimarySite`  

    - **Podrobnosti:** Obnoví primární lokalitu.  

- **Název klíče:** CDLatest  

    - **Požadováno:** Ano, pouze při použití média z disku CD. Poslední složka

    - **Hodnota**

        - `1`= používáte médium z CD. Nejnovější

        - Libovolná jiná hodnota než 1 = nepoužíváte disk CD. Nejnovější média

    - **Podrobnosti:** Při instalaci nebo obnovení primární lokality nebo certifikačních autorit a spuštění instalačního programu z disku CD-ROM. Nejnovější složku, zahrňte tento klíč a hodnotu. Tato hodnota informuje o nastavení, že používáte médium z CD. Nejnovější.

#### <a name="recoveryoptions"></a>MožnostiObnovení

- **Název klíče:** ServerRecoveryOptions  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `1`= Obnovit server lokality a SQL Server

        - `2`= Obnovit pouze server lokality

        - `4`= Obnovit pouze SQL Server  

    - **Podrobnosti:** Určuje, jestli instalační program obnoví server lokality, SQL Server, nebo obojí. Na základě zadané hodnoty jsou vyžadovány i následující možnosti:  

        - **1** nebo **2**: k obnovení lokality pomocí zálohy lokality zadejte hodnotu pro **klíče siteserverbackuplocation**. Pokud nezadáte žádnou hodnotu, instalační program znovu nainstaluje lokalitu bez obnovení ze zálohovacího skladu.  

        - **4**: klíč **BackupLocation** se vyžaduje při konfiguraci hodnoty **10** pro klíč **DatabaseRecoveryOptions** , který má obnovit databázi lokality ze zálohy.  

- **Název klíče:** DatabaseRecoveryOptions  

    - **Požadováno:** Tento klíč je vyžadován, pokud má nastavení **ServerRecoveryOptions** hodnotu **1** nebo **4**.  

    - **Hodnota**

        - `10`= Obnovit databázi lokality ze zálohy.  

        - `20`= Použít databázi lokality, kterou jste ručně obnovili s jinou metodou.  

        - `40`= Vytvořit novou databázi pro web. Tuto možnost použijte, pokud není k dispozici žádná záloha databáze lokality. Lokalita obnoví globální data a data lokality prostřednictvím replikace z jiných lokalit.  

        - `80`= Přeskočit obnovení databáze.  

    - **Podrobnosti:** Určuje způsob, jakým Instalační program obnovuje databázi lokality v SQL Server.  

- **Název klíče:** SiteServerBackupLocation  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k zálohovacímu skladu serveru lokality*>  

    - **Podrobnosti:** Udává cestu k zálohovacímu skladu serveru lokality. Tento klíč je volitelný při nastavení **ServerRecoveryOptions** na hodnotu **1** nebo **2**. K obnovení lokality pomocí zálohy lokality zadejte hodnotu klíče **SiteServerBackupLocation** . Pokud nezadáte žádnou hodnotu, instalační program znovu nainstaluje lokalitu bez obnovení ze zálohovacího skladu.  

- **Název klíče:** BackupLocation  

    - **Požadováno:** Tento klíč se vyžaduje, když nakonfigurujete hodnotu **1** nebo **4** pro klíč **ServerRecoveryOptions** a nakonfigurujete hodnotu **10** pro klíč **DatabaseRecoveryOptions** .  

    - **Hodnoty:** <*cesta k zálohovacímu skladu databáze lokality*>  

    - **Podrobnosti:** Udává cestu k zálohovacímu skladu databáze lokality.  

#### <a name="options"></a>Možnosti

- **Název klíče:** ProductID  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= platný kód Product Key s pomlčkami

        - `Eval`= Nainstalujte zkušební verzi Configuration Manager

    - **Podrobnosti:** Určuje kód Product Key instalace Configuration Manager, včetně pomlček.

- **Název klíče:** SiteCode  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*kód lokality*>  

    - **Podrobnosti:** Určuje tři alfanumerické znaky, které jedinečně identifikují lokalitu ve vaší hierarchii. Zadejte kód lokality, který byl použit lokalitou před chybou.

- **Název klíče:** SiteName  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*název webu*>  

    - **Podrobnosti:** Určuje název tohoto webu.  

- **Název klíče:** SMSInstallDir  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*Configuration Manager cesta instalace*>  

    - **Podrobnosti:** Určuje instalační složku pro soubory Configuration Manager programu.  

- **Název klíče:** SDKServer  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*plně kvalifikovaný název domény poskytovatele služby SMS*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény pro server, který je hostitelem poskytovatele služby SMS. Zadejte server, který hostuje poskytovatele služby SMS, před selháním. Po počáteční instalaci můžete nakonfigurovat další poskytovatele služby SMS pro tuto lokalitu. Další informace o poskytovateli serveru SMS najdete v tématu [plánování poskytovatele serveru SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Název klíče:** PrerequisiteComp  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Stáhnout  

        - `1`= Již staženo  

    - **Podrobnosti:** Určuje, zda byly staženy požadované instalační soubory. Pokud například použijete hodnotu **0**, instalační program soubory stáhne.  

- **Název klíče:** PrerequisitePath  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*cesta k instalaci požadovaných souborů*>  

    - **Podrobnosti:** Určuje cestu k požadovaným souborům instalace. V závislosti na hodnotě **PrerequisiteComp** instalační program použije tuto cestu k ukládání stažených souborů nebo k vyhledání dříve stažených souborů.  

- **Název klíče:** AdminConsole  

    - **Požadováno:** Tento klíč je vyžadován s výjimkou případů, kdy má nastavení **ServerRecoveryOptions** hodnotu **4**.  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má nainstalovat konzola Configuration Manager.  

- **Název klíče:** JoinCEIP  

    > [!Note]  
    > Počínaje verzí Configuration Manager 1802 je funkce CEIP z produktu odebrána.

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Nepřipojovat  

        - `1`= Připojit  

    - **Podrobnosti:** Určuje, zda se má připojit k programu CEIP.  

#### <a name="sqlconfigoptions"></a>MožnostiKonfSQL

- **Název klíče:** SQLServerName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název systému SQL Server*>  

    - **Podrobnosti:** Určuje název serveru nebo clusterované instance, která se spustí SQL Server pro hostování databáze lokality. Zadejte stejný server, který hostuje databázi lokality před selháním.  

- **Název klíče:** DatabaseName  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*název databáze lokality*> nebo název *instance*>\\<<název*databáze lokality*>

    - **Podrobnosti:** Určuje název databáze SQL Server, která se má vytvořit, nebo databáze SQL Server, která se má použít při instalaci databáze CAS. Zadejte stejný název databáze, který byl použit před selháním.  

        > [!IMPORTANT]  
        > Pokud nepoužíváte výchozí instanci, zadejte název instance a název databáze lokality.  

- **Název klíče:** SQLSSBPort  

    - **Požadováno:** Ano  

    - **Hodnoty:** <*číslo portu SSB*>  

    - **Podrobnosti:** Určuje port SSB, který SQL Server používá. Ve výchozím nastavení používá SSB port TCP 4022. Zadejte stejný port SSB, který byl použit před selháním.  

- **Název klíče:** SQLDataFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. mdb*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru. MDB databáze.  

- **Název klíče:** SQLLogFilePath  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*cesta k souboru Database. ldf*>  

    - **Podrobnosti:** Určuje alternativní umístění pro vytvoření souboru Database. ldf.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Název klíče:** CCARSiteServer  

    - **Požadováno:** Podívejte se na podrobnosti.  

    - **Hodnoty:** <*kód lokality pro certifikační autority*>  

    - **Podrobnosti:** Určuje CAS, ke kterým se primární lokalita připojí, když se připojí k hierarchii Configuration Manager. Toto nastavení je povinné, pokud byla primární lokalita připojena k certifikační autoritě před selháním. Zadejte kód lokality, který byl použit pro certifikační autority před chybou.  

- **Název klíče:** CASRetryInterval  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*interval v minutách*>  

    - **Podrobnosti:** Určuje interval opakování pokusu o připojení k certifikačním autoritám po neúspěšném připojení v minutách. Například pokud připojení ke CAS dojde k chybě, primární lokalita počká na počet minut, který zadáte pro hodnotu **CASRetryInterval** , a pak se znovu pokusí o připojení.  

- **Název klíče:** WaitForCASTimeout  

    - **Požadováno:** Ne  

    - **Hodnoty:** <*časový limit v minutách*>  

    - **Podrobnosti:** Určuje maximální hodnotu časového limitu (v minutách), který má primární lokalita připojit k certifikační autoritě. Pokud se například primární lokalita nepřipojí k certifikační autoritě, primární lokalita se znovu pokusí připojit k certifikačním autoritám na základě hodnoty **CASRetryInterval** , dokud nedosáhne **parametru WaitForCASTimeout** období. Můžete zadat hodnotu `0` do `100`.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Název klíče:** CloudConnector  

    - **Požadováno:** Ano  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, jestli se má v této lokalitě nainstalovat bod připojení služby. Protože spojovací bod služby můžete nainstalovat jenom v lokalitě nejvyšší úrovně v hierarchii, musí být `0` tato hodnota pro podřízenou primární lokalitu.  

- **Název klíče:** CloudConnectorServer  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény serveru bodu připojení služby*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény serveru, který bude hostitelem role systému lokality spojovacího bodu služby.  

- **Název klíče:** UseProxy  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnota**

        - `0`= Neinstalovat  

        - `1`= Instalovat  

    - **Podrobnosti:** Určuje, zda spojovací bod služby používá proxy server.  

- **Název klíče:** Proxy server  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*plně kvalifikovaný název domény proxy serveru*>  

    - **Podrobnosti:** Určuje plně kvalifikovaný název domény proxy server, který používá spojovací bod služby.  

- **Název klíče:** ProxyPort  

    - **Požadováno:** Požadováno, pokud se **CloudConnector** rovná 1  

    - **Hodnoty:** <*číslo portu*>  

    - **Podrobnosti:** Určuje číslo portu, který se má použít pro port proxy serveru.  
