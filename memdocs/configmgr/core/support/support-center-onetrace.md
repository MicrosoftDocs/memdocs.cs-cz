---
title: Support Center OneTrace (Preview)
titleSuffix: Configuration Manager
description: OneTrace je nový prohlížeč protokolů s centrem podpory, který má vylepšení oproti CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723107"
---
# <a name="support-center-onetrace-preview"></a>Support Center OneTrace (Preview)

<!--3555962-->

Počínaje verzí 1906 je OneTrace nový prohlížeč protokolů s nástrojem Support Center. Funguje podobně jako CMTrace, s následujícími vylepšeními:

- Zobrazení s kartami
- Ukotvit okna
- Vylepšené možnosti vyhledávání
- Možnost Povolit filtry bez nutnosti opustit zobrazení protokolu
- Tipy pro rychlou identifikaci clusterů s chybami v ScrollBar
- Rychlé otevírání protokolů pro velké soubory

[![Snímek obrazovky prohlížeče protokolu OneTrace](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace pracuje s mnoha typy souborů protokolu, například:

- Configuration Manager protokoly klienta
- Protokoly Configuration Manager serveru
- Stavové zprávy
- web Windows Update souboru protokolu ETW ve Windows 10
- Soubor protokolu web Windows Update v systému Windows 7 & Windows 8.1

## <a name="prerequisites"></a>Požadavky

- .NET Framework verze 4,6 nebo novější

## <a name="install"></a>Instalace

OneTrace se nainstaluje pomocí programu Support Center. Na serveru lokality vyhledejte instalační program nástroje Support Center v následující cestě: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Ve výchozím nastavení je aplikace OneTrace nainstalována na adrese `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe` .

> [!Note]  
> Support Center a OneTrace use Windows Presentation Foundation (WPF). Tato součást není k dispozici v systému Windows PE. Nadále používat CMTrace ve spouštěcích bitových kopiích s nasazeními pořadí úloh.  

## <a name="log-groups"></a>Skupiny protokolů

<!--5559993-->

Počínaje verzí 2002 podporuje OneTrace přizpůsobitelné skupiny protokolů, podobně jako funkce v nástroji Support Center. Skupiny protokolů umožňují otevřít všechny soubory protokolu pro jeden scénář. OneTrace v současné době zahrnuje skupiny pro následující scénáře:

- Správa aplikací
- Nastavení dodržování předpisů (také označované jako správa požadované konfigurace)
- Aktualizace softwaru

Chcete-li zobrazit skupiny protokolů, přejděte do nabídky **zobrazení** a vyberte možnost **skupiny protokolů**.

![Snímek obrazovky skupiny protokolů OneTrace pro správu aplikací](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Přizpůsobení skupin protokolů

Tyto skupiny můžete přizpůsobit změnou konfiguračního souboru XML, který je ve výchozím nastavení v následující cestě: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml` .

V následujícím příkladu je jedna část výchozího konfiguračního souboru:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

`GroupType`Vlastnost přijímá následující hodnoty:

- `0`: Neznámé nebo jiné
- `1`: Configuration Manager protokoly klienta
- `2`: Configuration Manager protokoly serveru

`GroupFilePath`Vlastnost může obsahovat explicitní cestu pro soubory protokolu. Pokud je prázdná, OneTrace spoléhá na konfiguraci registru pro daný typ skupiny. Pokud jste například nastavili `GroupType=1` , bude se ve výchozím nastavení automaticky hledat v `C:\Windows\CCM\Logs` protokolech ve skupině. V tomto příkladu není nutné zadávat `GroupFilePath` .

## <a name="see-also"></a>Viz také

- [Prohlížeč protokolů Support Center](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
