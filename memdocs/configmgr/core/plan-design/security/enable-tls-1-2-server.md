---
title: Povolit TLS (Transport Layer Security) 1,2 na serverech lokality a systémech vzdálené lokality
titleSuffix: Configuration Manager
description: Informace o tom, jak povolit TLS 1,2 pro Configuration Manager servery lokality.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720545"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Postup povolení protokolu TLS 1,2 na serverech lokality a vzdálených systémech lokality

*Platí pro: Configuration Manager (Current Branch)*

Při povolování TLS 1,2 pro vaše Configuration Manager prostředí nejprve začněte s [povolením protokolu tls 1,2 pro klienty](enable-tls-1-2-client.md) . Pak povolte TLS 1,2 na serverech lokality a systémech vzdálené lokality druhé. Nakonec otestujte komunikaci mezi klientem a serverem před tím, než potenciálně zakážete starší protokoly na straně serveru. Pro povolení TLS 1,2 na serverech lokality a vzdálených systémech lokality jsou potřeba následující úlohy:

- Ujistěte se, že je protokol TLS 1,2 povolený jako protokol pro zprostředkovatele SChannel na úrovni operačního systému.
- Aktualizace a konfigurace .NET Framework pro podporu TLS 1,2
- Aktualizovat SQL Server a součásti klienta
- Aktualizace Windows Server Update Services (WSUS)

Další informace o závislostech pro konkrétní Configuration Manager funkce a scénáře najdete v tématu [o povolování TLS 1,2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Ujistěte se, že je protokol TLS 1,2 povolený jako protokol pro zprostředkovatele SChannel na úrovni operačního systému.

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>Aktualizace a konfigurace .NET Framework pro podporu TLS 1,2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a>Aktualizovat SQL Server a součásti klienta

Microsoft SQL Server 2016 a novější podporují protokol TLS 1,1 a TLS 1,2. V dřívějších verzích a závislých knihovnách může být nutné aktualizace. Další informace najdete v článku [KB 3135244: podpora TLS 1,2 pro Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Servery sekundární lokality musí používat minimálně SQL Server 2016 Express s aktualizací Service Pack 2 (13.2.50.26) nebo novější.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a>SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) také popisuje požadavky na součásti SQL Server klienta.

Nezapomeňte také aktualizovat SQL Server Native Client alespoň na verzi SQL 2012 SP4 (11. *. 7001.0). Počínaje verzí 1810 je tento požadavek [Kontrola požadavků (upozornění)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager používá SQL Server Native Client na následujících rolích systému lokality:

- Server databáze lokality
- Server lokality: lokalita centrální správy, primární lokalita nebo sekundární lokalita
- Bod správy
- Bod správy zařízení
- Bod migrace stavu
- SMS Provider
- Bod aktualizace softwaru
- Distribuční bod s povoleným vícesměrovým vysíláním
- Servisní bod aktualizace služby funkce Asset Intelligence
- Bod služby Reporting services
- Webová služba Application Catalog
- Bod registrace
- Bod ochrany koncového bodu Endpoint Protection
- Spojovací bod služby
- Bod registrace certifikátu
- Bod služby datového skladu


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a>Aktualizace Windows Server Update Services (WSUS)

Pokud chcete v dřívějších verzích služby WSUS podporovat protokol TLS 1,2, nainstalujte na server WSUS tuto aktualizaci:

- Pro server WSUS, na kterém běží Windows Server 2012, nainstalujte [update 4022721](https://support.microsoft.com/help/4022721) nebo novější kumulativní aktualizaci.
- Pro server WSUS se systémem Windows Server 2012 R2 nainstalujte [update 4022720](https://support.microsoft.com/help/4022720) nebo novější kumulativní aktualizaci.

Od Windows serveru 2016 se standardně podporuje TLS 1,2 pro službu WSUS.  Aktualizace TLS 1,2 se vyžadují jenom na serverech Windows Server 2012 a Windows Server 2012 R2 WSUS.

## <a name="next-steps"></a>Další kroky

- [Běžné problémy při povolování protokolu TLS 1.2](enable-tls-1-2-troubleshoot.md)
