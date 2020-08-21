---
title: Správa klientů VDI
titleSuffix: Configuration Manager
description: Správa Configuration Manager klientů v infrastruktuře virtuálních klientských počítačů (VDI).
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d79edb5ad1a60c5876163281ec5c1d1c17eff0a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692804"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Správa klientů Configuration Manager v infrastruktuře virtuálních klientských počítačů (VDI)

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje instalaci klienta Configuration Manager na následujících scénářích infrastruktury virtuálních klientských počítačů (VDI):

- **Osobní virtuální počítače**: virtuální počítač (VM) udržuje uživatelská data a nastavení mezi relacemi.

- **Relace služby Vzdálená plocha**: hostování více souběžných klientských relací na centralizovaném serveru. Uživatelé se připojují k relaci a spouštějí aplikace na daném serveru.

- **Virtuální počítače ve fondu**: virtuální počítač se neuchovává mezi relacemi. Když uživatel zavře relaci, virtuální prostředí zruší všechna data a nastavení. Virtuální počítače ve fondu jsou užitečné, když nemůžete použít službu Vzdálená plocha. Například Pokud požadovaná aplikace nemůže běžet na serveru Windows, který hostuje klientské relace.

- **Virtuální klient Windows**: služba virtualizace plochy a aplikací, která běží na Microsoft Azure. Počínaje verzí 1906 použijte Configuration Manager ke správě těchto virtuálních zařízení s Windows v Azure.

## <a name="personal-vms"></a>Osobní virtuální počítače

Configuration Manager pracuje s osobními virtuálními počítači, které jsou stejné jako u fyzického počítače. Klienta Configuration Manager můžete předinstalovat na image virtuálního počítače nebo po jeho zřízení.

Další informace najdete v tématu [Podpora virtualizačních prostředí](../../../plan-design/configs/support-for-virtualization-environments.md).

## <a name="remote-desktop-services"></a>Vzdálená plocha

Nenainstalujete klienta Configuration Manager pro jednotlivé relace vzdálené plochy. Nainstalujte ji jednou na server, který je hostitelem služby Vzdálená plocha. Na serveru služby Vzdálená plocha můžete použít všechny klientské funkce Configuration Manager.

Další informace najdete v tématu [Vítá vás služba Vzdálená plocha](/windows-server/remote/remote-desktop-services/welcome-to-rds).

## <a name="pooled-vms"></a>Virtuální počítače ve fondu

Když vyřadíte z provozu virtuální počítač ve fondu, ztratí se všechny změny provedené v Configuration Manager.

Vzhledem k tomu, že virtuální počítač může být funkční jenom po krátkou dobu, některé funkce Configuration Manager nemusí vracet relevantní data. Například inventář hardwaru, inventář softwaru a měření softwaru. Zvažte možnost vyloučit z úloh inventáře virtuální počítač ve fondu.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

Další informace najdete v tématu [podporované operační systémy pro klienty a zařízení](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="other-considerations"></a>Další důležité informace

Protože virtualizace podporuje spouštění více Configuration Manager klientů na jednom fyzickém počítači, mnoho operací klienta má vestavěnou náhodnou prodlevu pro plánované akce. Například inventář hardwaru a softwaru, kontroly antimalwaru, instalace softwaru a prověřování aktualizací softwaru. Tato prodleva pomáhá distribuovat výpočetní výkon procesoru a přenos dat pro server, který obsahuje více virtuálních počítačů používajících klienta Configuration Manager.

S výjimkou klientů se systémem Windows Embedded v režimu obsluhy Configuration Manager klienti, kteří nejsou ve virtualizovaných prostředích, také tuto náhodnou prodlevu používají. Toto chování pomáhá zabránit špičkám v šířce pásma sítě. Také snižuje nároky na procesor v systémech lokality, jako je třeba bod správy a server lokality. Interval zpoždění se liší podle možnosti Configuration Manager. Příklad najdete v tématu [informace o nastavení klienta – zakázat náhodné přeskupování termínu](../about-client-settings.md#disable-deadline-randomization).

Pro pomoc s Configuration Manager výkonu klienta ve virtuálních prostředích podporujících více uživatelských relací zakáže zásady uživatele ve výchozím nastavení. Počínaje verzí 1910 můžete v tomto scénáři povolit zásady uživatele. Další informace najdete v tématu [o nastavení klienta – povolení zásad uživatele pro více uživatelských relací](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).