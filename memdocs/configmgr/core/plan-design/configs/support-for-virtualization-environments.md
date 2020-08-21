---
title: Podpora pro virtualizaci
titleSuffix: Configuration Manager
description: Požadavky na instalaci Configuration Manager rolí klienta a systému lokality v prostředí virtualizace.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d2977fc34e9c398e9e266cbc9b223ea74a1dd18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700227"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Podpora virtualizačních prostředí pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje instalaci rolí klienta a systému lokality v podporovaných operačních systémech, které běží jako virtuální počítač (VM) v určitých virtualizačních prostředích. Tato podpora je dostupná i v případě, že virtuální hostitel (virtualizační prostředí) není podporovaný jako klient nebo server lokality.

Například pro hostování virtuálního počítače se systémem Windows Server 2019 používáte Microsoft Hyper-V Server 2016. Na virtuální počítač se systémem Windows Server 2019 můžete nainstalovat role klienta nebo systému lokality. Klienta nemůžete nainstalovat na hostitele se spuštěným Microsoft Hyper-V serverem 2016.

## <a name="virtualization-environments"></a>Virtualizační prostředí

- Windows Server 2019  
- Windows Server 2016 <sup> [Poznámka 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Poznámka 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager nepodporuje [vnořenou virtualizaci](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), která je v systému Windows Server 2016 novinkou.

### <a name="virtualization-environment-support"></a>Podpora prostředí virtualizace

Každý virtuální počítač potřebuje stejné nebo větší požadavky na hardware a software, které byste použili pro fyzický Configuration Manager počítač.

K ověření, že Configuration Manager podporuje vaše virtualizační prostředí, použijte program ověřování virtualizace serveru. Obsahuje průvodce zásadou podpory pro online virtualizační programy. Další informace najdete v tématu [ověřovací program virtualizace Windows serveru](https://www.windowsservercatalog.com/svvp.aspx).

Configuration Manager nemůže spravovat virtuální počítače, pokud jsou offline. Klient Configuration Manager v hostitelském počítači nemůže spravovat offline bitovou kopii virtuálního počítače. Například nemůže instalovat aktualizace softwaru ani shromažďovat inventář hardwaru.

Obecně platí, že Configuration Manager neposkytuje žádné zvláštní aspekty pro virtuální počítače. Pokud například zastavíte virtuální počítač a neuložíte jeho stav, Configuration Manager nemusí určit, jestli má znovu instalovat aktualizaci softwaru.

Pro pomoc s Configuration Manager výkonu klienta ve virtuálních prostředích podporujících více uživatelských relací zakáže zásady uživatele ve výchozím nastavení. Počínaje verzí 1910 můžete v tomto scénáři povolit zásady uživatele. Další informace najdete v tématu [o nastavení klienta – povolení zásad uživatele pro více uživatelských relací](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Microsoft Azure virtuálních počítačů

Configuration Manager můžete spustit na virtuálních počítačích v Azure, stejně jako v místním prostředí v rámci vašeho datového centra. Configuration Manager s virtuálními počítači Azure můžete použít v následujících scénářích:

- **Scénář 1**: spuštění Configuration Manager na virtuálním počítači Azure. Použijte ho ke správě klientů na jiných virtuálních počítačích Azure.

- **Scénář 2**: spuštění Configuration Manager na virtuálním počítači Azure. Použijte ho ke správě klientů, kteří neběží na Azure.

- **Scénář 3**: spuštění různých Configuration Manager rolí systému lokality na virtuálních počítačích Azure Spusťte další role v místním datovém centru, které jsou správně připojené k Azure.

Stejné Configuration Manager požadavky na sítě, podporované konfigurace a požadavky na hardware platí také pro virtuální počítače Azure.

Další informace najdete v tématu [Configuration Manager v Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]
> Pro Configuration Manager weby a klienty, které běží na virtuálních počítačích Azure, se vztahují stejné licenční požadavky jako na místní instalace.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Virtuální plocha Windows](/azure/virtual-desktop/) je služba virtualizace plochy a aplikací, která běží na Microsoft Azure. Počínaje verzí 1906 použijte Configuration Manager ke správě těchto virtuálních zařízení s Windows v Azure. Další informace najdete v tématu [podporované operační systémy pro klienty a zařízení](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="next-steps"></a>Další kroky

[Správa klientů Configuration Manager v infrastruktuře virtuálních klientských počítačů (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)