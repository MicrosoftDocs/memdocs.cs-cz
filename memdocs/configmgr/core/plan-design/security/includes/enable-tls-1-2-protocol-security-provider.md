---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720531"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

Ve výchozím nastavení je povolený protokol TLS 1,2. Proto není nutné žádné změny těchto klíčů povolit. Můžete provést změny v části `Protocols` zakázání TLS 1,0 a TLS 1,1 poté, co jste postupovali podle těchto pokynů v těchto článcích, a ověříte, že prostředí funguje, pokud je povolené jenom TLS 1,2.

Ověřte nastavení `\SecurityProviders\SCHANNEL\Protocols` podklíče registru, jak je znázorněno v [doporučených postupech TLS (Transport Layer security) s .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

