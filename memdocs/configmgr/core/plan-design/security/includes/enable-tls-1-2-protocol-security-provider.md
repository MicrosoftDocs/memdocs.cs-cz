---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703212"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

Ve výchozím nastavení je povolený protokol TLS 1,2. Proto není nutné žádné změny těchto klíčů povolit. Můžete provést změny v části `Protocols` zakázání TLS 1,0 a tls 1,1 poté, co jste postupovali podle těchto pokynů v těchto článcích, a ověříte, že prostředí funguje, pokud je povolené jenom TLS 1,2.

Ověřte `\SecurityProviders\SCHANNEL\Protocols` nastavení podklíče registru, jak je znázorněno v [doporučených postupech TLS (Transport Layer Security) s .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).