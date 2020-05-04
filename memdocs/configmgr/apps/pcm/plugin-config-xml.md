---
title: XML konfigurace modulu plug-in
titleSuffix: Configuration Manager
description: Technické informace o prvcích XML modulu plug-in Správce převodu balíčků.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ced1cc1347167451d4efb789b40746ff849710ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709961"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Technické informace o konfiguraci modulu plug-in Správce převodu balíčku pro XML

*Platí pro: Configuration Manager (Current Branch)*

<!--1357861-->

Tento článek popisuje elementy XML v konfiguračním souboru Configuration Manager (Microsoft. ConfigurationManagement. exe. config), které řídí operaci modulu plug-in Správce převodu balíčků. Další informace o tom, jak používat tento modul plug-in, najdete v tématu [jak použít modul plug-in Správce převodu balíčků](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>Prvky konfigurace XML

Následující tabulka popisuje prvky XML v konfiguračním souboru Configuration Manager, které se vztahují k modulu plug-in Správce převodu balíčků.

|Prvek  |Typ  |Popis  |
|---------|---------|---------|
|**PcmPlugIn**|Řetězec|Název skriptu nebo spustitelného souboru, který má být použit jako modul plug-in Správce převodu balíčků.|
|**PcmPlugInTimeoutMilliseconds**|Integer|Maximální doba (v milisekundách), po kterou se má čekat na skript modulu plug-in Správce převodu balíčku nebo spustitelný soubor pro dokončení zpracování balíčku.|
|**PcmPluginExitCode**|Integer|Očekávaný ukončovací kód z procesu modulu plug-in. Tato hodnota označuje úspěch. Všechny ostatní kódy se považují za chybu.|
|**ForceRequirementsExtraction**|Logická hodnota|Povolí automatický převod na použití požadavků na shromažďování přidružených k balíčku. Tato hodnota by měla být nastavena na hodnotu true pouze při práci s modulem plug-in Správce převodu balíčků, který je navržen pro rozhodování o tom, jaké požadavky se mají použít.|



## <a name="sample-configuration-xml"></a>Ukázkový konfigurační soubor XML

V této části najdete příklad prvků XML konfigurace balíčku převodů balíčků v konfiguračním souboru Configuration Manager, **Microsoft. ConfigurationManagement. exe. config**. Ve výchozím nastavení je tento soubor v následující cestě:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

V ukázce jsou prvky související se správcem převodu balíčku uvnitř následujícího elementu:`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

