---
title: Postup povolení protokolu TLS (Transport Layer Security) 1,2 na klientech
titleSuffix: Configuration Manager
description: Informace o tom, jak povolit TLS 1,2 pro klienty Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720552"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Jak povolit TLS 1,2 na klientech

*Platí pro: Configuration Manager (Current Branch)*

Při povolování protokolu TLS 1,2 pro prostředí Configuration Manager Začněte tím, že zajistíte, aby klienti měli možnost používat protokol TLS 1,2 před povolením TLS 1,2 a zakázali starší protokoly na serverech lokality a vzdálených systémech lokality. Existují tři úlohy pro povolení TLS 1,2 na klientech:

- Aktualizovat Windows a WinHTTP
- Ujistěte se, že je protokol TLS 1,2 povolený jako protokol pro zprostředkovatele SChannel na úrovni operačního systému.
- Aktualizace a konfigurace .NET Framework pro podporu TLS 1,2

Další informace o závislostech pro konkrétní Configuration Manager funkce a scénáře najdete v tématu [o povolování TLS 1,2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a>Aktualizovat Windows a WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 a novější verze Windows nativně podporují protokol 1,2 TLS pro komunikaci mezi klientem a serverem přes WinHTTP. 

Starší verze Windows, třeba Windows 7 nebo Windows Server 2012, ve výchozím nastavení nepovolujte TLS 1,1 nebo TLS 1,2 standardně pro zabezpečenou komunikaci pomocí protokolu WinHTTP. Pro tyto starší verze Windows nainstalujte [Update 3140245](https://support.microsoft.com/help/3140245) , aby se aktivovala níže uvedená hodnota registru, kterou je možné nastavit tak, aby se v seznamu výchozích zabezpečených protokolů pro WinHTTP přidal protokol TLS 1,1 a TLS 1,2. Při instalaci opravy vytvořte následující hodnoty registru:

> [!IMPORTANT]
> *Před* povolením TLS 1,2 a zakázáním starších protokolů na serverech Configuration Manager povolte tato nastavení na všech klientech, kteří používají starší verze Windows. V opačném případě je můžete omylem osamocení.

Ověřte hodnotu nastavení `DefaultSecureProtocols` registru, například:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Pokud tuto hodnotu změníte, restartujte počítač.

Výše uvedený příklad ukazuje hodnotu `0xAA0` pro nastavení WinHTTP. `DefaultSecureProtocols` [KB 3140245: aktualizace povolit TLS 1,1 a tls 1,2 jako výchozí zabezpečené protokoly v WinHTTP v systému Windows](https://support.microsoft.com/help/3140245) uvádí hexadecimální hodnotu pro každý protokol. Ve výchozím nastavení ve Windows je `0x0A0` tato hodnota pro WinHTTP povolená SSL 3,0 a TLS 1,0. Následující příklad uchovává tyto výchozí hodnoty a zároveň umožňuje protokol TLS 1,1 a TLS 1,2 pro WinHTTP. Tato konfigurace zajišťuje, že změna neruší žádnou jinou aplikaci, která by mohla být závislá na protokolu SSL 3,0 nebo TLS 1,0. Hodnotu můžete použít jenom `0xA00` k povolení TLS 1,1 a TLS 1,2. Configuration Manager podporuje nejbezpečnější protokol, který systém Windows vyjednává mezi oběma zařízeními.

 Pokud chcete zcela zakázat protokol SSL 3,0 a TLS 1,0, použijte nastavení protokoly SChannel Disabled v systému Windows. Další informace najdete v tématu [jak omezit použití určitých kryptografických algoritmů a protokolů v souboru Schannel. dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Ujistěte se, že je protokol TLS 1,2 povolený jako protokol pro zprostředkovatele SChannel na úrovni operačního systému.

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>Aktualizace a konfigurace .NET Framework pro podporu TLS 1,2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Další kroky

- [Povolit TLS 1,2 na serverech lokality a vzdálených systémech lokality](enable-tls-1-2-server.md)
- [Běžné problémy při povolování protokolu TLS 1.2](enable-tls-1-2-troubleshoot.md)

