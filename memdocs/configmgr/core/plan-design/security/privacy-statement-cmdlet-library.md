---
title: Prohlášení o zásadách ochrany osobních údajů pro rutiny
titleSuffix: Configuration Manager
description: Informace o tom, jak společnost Microsoft shromažďuje a používá data související s rutinami Configuration Manager
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714644"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Configuration Manager prohlášení o zásadách ochrany osobních údajů knihovny rutin

*Platí pro: Configuration Manager (Current Branch)*

Toto prohlášení o zásadách ochrany osobních údajů se zabývá funkcemi pro knihovnu rutin Configuration Manager.  

## <a name="usage-data"></a>Údaje o využití  

#### <a name="what-this-feature-does"></a>K čemu slouží tato funkce

Knihovna rutin Configuration Manager umožňuje spravovat Configuration Manager hierarchii pomocí rutin a skriptů prostředí Windows PowerShell. Knihovna rutin shromažďuje informace o tom, jak pomocí rutin v knihovně identifikovat trendy a vzorce používání. Knihovna rutin taky shromažďuje typy a počty chyb, které dostanete při použití rutin.  

#### <a name="information-collected-processed-or-transmitted"></a>Shromažďované, zpracovávané a odesílané informace
   
Shromážděná data o využití zahrnují spouštění, zastavování a ukončování rutin, spouštění zastaralých rutin a metriky aktivity pro operace poskytovatele SMS související s rutinami. Tyto informace nejsou identifikovatelné osobně. Shromážděné informace o chybách zahrnují chyby, které rutiny vracejí, a podrobnosti chyb pro chyby výjimek. Některé zprávy s podrobnostmi o chybě můžou nechtěně zahrnovat jednotlivé identifikátory, třeba sériové číslo zařízení, které je připojené k vašemu počítači. Knihovna rutin filtruje a zajistila jejich anonymita informace, které jsou v hlášení o chybách, aby před přenosem do Microsoftu odebrala jednotlivé identifikátory.  

#### <a name="use-of-information"></a>Používání informací
   
Společnost Microsoft tyto informace používá ke zlepšení kvality, zabezpečení a integrity produktů a služeb, které nabízí.  

#### <a name="choicecontrol"></a>Možnost volby/řízení   

Tato funkce dat o používání je ve výchozím nastavení povolená. Knihovna rutin Configuration Manager obsahuje dva klíče registru, které tuto funkci ovládají.  

 Pokud chcete plně odhlásit, nastavte tyto dvě hodnoty klíče registru. Jsou pro každé z těchto zprostředkovatelů trasování událostí pro Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider: CeipLevel = 0 (výslovný data o využití pro poskytovatele jednotky)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets: CeipLevel = 0 (výslovný z dat použití pro rutiny)  

  Změny nastavení dat o využití jsou specifické pro počítač, ve kterém se nastavily.  


## <a name="next-steps"></a>Další kroky

[Configuration Manager dokumentaci ke knihovně rutin](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
