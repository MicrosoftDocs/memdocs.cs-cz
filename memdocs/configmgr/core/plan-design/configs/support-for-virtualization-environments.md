---
title: Podpora pro virtualizaci
titleSuffix: Configuration Manager
description: Požadavky na instalaci Configuration Manager rolí klienta a systému lokality v prostředí virtualizace.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709590"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Podpora virtualizačních prostředí pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje instalaci rolí klienta a systému lokality v podporovaných operačních systémech, které běží jako virtuální počítač v virtualizačních prostředích v tomto článku. Tato podpora je dostupná i v případě, že hostitel virtuálního počítače (virtualizační prostředí) není podporovaný jako klient nebo server lokality.  

Například použijete Microsoft Hyper-V Server 2012 k hostování virtuálního počítače se systémem Windows Server 2012. Na virtuální počítač se systémem Windows Server 2012 můžete nainstalovat role klienta nebo systému lokality. Klienta nemůžete nainstalovat na hostitele se spuštěným Microsoft Hyper-V serverem 2012.  

## <a name="virtualization-environments"></a>Virtualizační prostředí

- Windows Server 2019  
- Windows Server 2016 <sup> [Poznámka 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Poznámka 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a>Poznámka 1: vnořená virtualizace

Configuration Manager nepodporuje [vnořenou virtualizaci](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), která je v systému Windows Server 2016 novinkou.

### <a name="virtualization-environment-support"></a>Podpora prostředí virtualizace

Každý virtuální počítač potřebuje stejné nebo větší požadavky na hardware a software, které byste použili pro fyzický Configuration Manager počítač.  

Pokud chcete ověřit, jestli je pro Configuration Manager podporovaná vaše virtualizační prostředí, použijte program ověřování virtualizace serveru. Obsahuje průvodce zásadou podpory pro online virtualizační programy. Další informace najdete v tématu [ověřovací program virtualizace Windows serveru](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> Configuration Manager nepodporuje hostované operační systémy Virtual PC nebo Virtual Server spuštěné v počítačích Mac.  

Configuration Manager nemůže spravovat virtuální počítače, pokud jsou offline. Bitovou kopii virtuálního počítače v režimu offline nelze aktualizovat ani nelze shromáždit inventarizaci pomocí klienta Configuration Manager v hostitelském počítači.  

Na virtuální počítače se neberou žádné zvláštní ohledy. Configuration Manager například nemusí určit, jestli se má znovu použít aktualizace na image virtuálního počítače, pokud se virtuální počítač zastavil a znovu spustil bez uložení stavu virtuálního počítače, na který se aktualizace použila.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a>Microsoft Azure virtuálních počítačů  

Configuration Manager můžete spustit na virtuálních počítačích v Azure, stejně jako v místním prostředí v rámci vašeho datového centra. Configuration Manager s virtuálními počítači Azure můžete použít v následujících scénářích:  

- **Scénář 1**: spuštění Configuration Manager na virtuálním počítači Azure. Použijte ho ke správě klientů na jiných virtuálních počítačích Azure.  

- **Scénář 2**: spuštění Configuration Manager na virtuálním počítači Azure. Použijte ho ke správě klientů, kteří neběží na Azure.  

- **Scénář 3**: spuštění různých Configuration Manager rolí systému lokality na virtuálních počítačích Azure. Spusťte další role v místním datovém centru, které jsou správně připojené k Azure.  

Stejné Configuration Manager požadavky na sítě, podporované konfigurace a požadavky na hardware, které platí pro místní instalaci, platí také pro instalaci na virtuálních počítačích Azure.  

Další informace najdete v tématu [Configuration Manager v Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]  
> Pro Configuration Manager weby a klienty, které běží na virtuálních počítačích Azure, se vztahují stejné licenční požadavky jako na místní instalace.  

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Virtuální plocha Windows](https://docs.microsoft.com/azure/virtual-desktop/) je funkce verze Preview Microsoft Azure a Microsoft 365. Počínaje verzí 1906 použijte Configuration Manager ke správě těchto virtuálních zařízení s Windows v Azure. Další informace najdete v tématu [podporované operační systémy pro klienty a zařízení](supported-operating-systems-for-clients-and-devices.md).
