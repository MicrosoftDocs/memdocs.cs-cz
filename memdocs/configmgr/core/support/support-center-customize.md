---
title: Přizpůsobení služby Support Center
titleSuffix: Configuration Manager
description: Přizpůsobení konfiguračního souboru nástroje Support Center.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc17437e508ea69a19043c29bf9ad4501cbac3e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078511"
---
# <a name="customize-support-center"></a>Přizpůsobení služby Support Center

*Platí pro: Configuration Manager (Current Branch)*

Nástroj [Support Center](support-center.md) obsahuje konfigurační soubor, který můžete přizpůsobit. Ve výchozím nastavení platí, že při instalaci nástroje Support Center je tento soubor v následující cestě `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`:. Konfigurační soubor změní chování programu:

- [Přizpůsobení shromažďování dat: umožňuje](#bkmk_datacoll)upravit sady klíčů registru a obory názvů WMI, které zahrnuje během shromažďování dat.  

- [Přizpůsobení skupin protokolů](#bkmk_loggroups): Definujte nové skupiny souborů protokolů pomocí regulárních výrazů. Přidejte do skupin protokolů taky další soubory protokolů.  

- [Shromažďování dalších souborů protokolu pomocí zástupných znaků](#bkmk_wildcards): k shromažďování dalších souborů protokolu použijte hledání pomocí zástupných znaků  

Chcete-li provést tyto změny, potřebujete oprávnění místního správce v klientovi, kde jste nainstalovali centrum podpory. Tato přizpůsobení proveďte pomocí textu nebo editoru XML, jako je například Poznámkový blok nebo Visual Studio.

> [!Important]  
> Konfigurační soubor nástroje Support Center je soubor ve formátu XML. Je zásadní pro provoz nástroje Support Center. Úprava tohoto souboru se doporučuje jenom pro uživatele, kteří mají zkušenosti s XML a regulárními výrazy.  

Před přizpůsobením konfiguračního souboru nástroje Support Center uložte zálohu originálu. Tato záloha umožňuje obnovit původní funkce nástroje Support Center, pokud při úpravách souboru provedete chyby. Pokud zálohu nevytvoříte a Support Center nebude po úpravě konfiguračního souboru správně fungovat, nainstalujte Support Center. Konfigurační soubor můžete také zkopírovat z jiné instalace programu Support Center.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a>Přizpůsobení shromažďování dat

Chcete-li přizpůsobit shromažďování dat na straně klienta, upravte konfigurační soubor nástroje Support Center pomocí elementů XML obsažených v `<dataCollectorSettings>` elementu.


### <a name="wmi-data-collection"></a>Shromažďování dat WMI

`<CcmWmiDataCollector>` Element obsahuje `<collectionScopes>` element. Pomocí tohoto prvku můžete změnit obory názvů WMI, ze kterých centrum podpory shromažďuje data. Obsahuje také `<ignoreScopes>` element. Tento prvek použijte k vyfiltrování kolekce dat z částí oborů názvů definovaných v `<collectionScopes>` elementu.  
    
#### <a name="example"></a>Příklad
Výchozí konfigurační soubor shromažďuje data z `root\ccm` oboru názvů. Zahrnuje tuto cestu do `<add/>` elementu v. `<collectionScopes>` 

Také ignoruje vše v rámci `\cimodels`cest `\invagt`, `\events`, a `\policy` pro tento obor názvů. Zahrnuje tyto cesty v `<add/>` prvcích obsažených v. `<ignoreScopes>`

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Shromažďování dat registru

`<RegistryDataCollector>` Element obsahuje `<registryKeys>` element. Pomocí tohoto prvku můžete změnit klíče a podklíče registru, které nástroje Support Center shromáždí `HKEY_LOCAL_MACHINE` pod cestou. Support Center nepodporuje shromažďování dat registru z jiných kořenových cest registru.

#### <a name="example"></a>Příklad
Chcete-li shromáždit klíče registru pro klasické programy nainstalované v zařízení, přidejte do `<add/>` `<registryKeys>` elementu následující element:`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a>Přizpůsobení skupin souborů protokolu

Chcete-li upravit, které soubory protokolu nástroje Support Center shromáždí a jak se zobrazí v seznamu **skupiny protokolů** , použijte prvky v `<logGroups>` elementu. Když spustíte Support Center, vyhledá tato část konfiguračního souboru. Potom vytvoří skupinu v seznamu **skupin protokolů** pro každou hodnotu atributu jedinečného klíče nalezenou v `<add/>` prvcích obsažených v `<logGroups>` elementu.

- **Skupina protokolů komponent**: `<componentLogGroup>` element používá atribut key k definování názvu skupiny protokolů, který se zobrazí v seznamu. Používá také atribut hodnoty, který obsahuje regulární výraz (Regex). Pomocí tohoto regulárního výrazu shromáždí sadu souvisejících souborů protokolu.  

- **Statická skupina protokolů:** `<staticLogGroup>` Element používá atribut key k definování názvu skupiny protokolů, který se zobrazí v seznamu. Používá také atribut hodnoty, který definuje název souboru protokolu.  

Pokud se stejná hodnota atributu Key používá v `<add/>` prvku v rámci `<componentLogGroup>` elementu i elementu, nástroj `<staticLogGroup>` Support Center vytvoří jednu skupinu. Tato skupina zahrnuje soubory protokolu definované pomocí obou prvků, které používají stejný klíč.

#### <a name="example"></a>Příklad
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a>Shromažďování dalších souborů protokolu pomocí zástupných znaků

K shromažďování dalších souborů protokolu použijte zástupné znaky v cestě k souboru nebo názvu souboru. Tyto zástupné znaky zahrnují proměnné prostředí `%WINDIR%`v rámci systému, například, ale vyloučení proměnných prostředí vymezených uživatelem, `%USERPROFILE%`jako je. Chcete-li shromáždit další soubory protokolu pomocí tohoto nerekurzivního hledání souborů protokolů, `<add/>` použijte element v `<additionalLogFiles>` rámci elementu. 

Tyto příklady ukazují, jak nástroj Support Center používá tuto funkci ve výchozím konfiguračním souboru.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Příklad 1: shromáždění všech souborů protokolu web Windows Update v adresáři Windows
Následující prvek shromažďuje všechny soubory s názvem `WindowsUpdate.log` nalezené v adresáři systému Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Příklad 2: shromáždění všech souborů protokolů v adresáři Windows logs
Následující prvek shromažďuje všechny soubory, které se `.log` nacházejí v adresáři v protokolech systému Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Úplný příklad XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
