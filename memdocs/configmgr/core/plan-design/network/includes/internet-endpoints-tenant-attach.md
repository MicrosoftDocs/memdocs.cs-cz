---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606455"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

Spojovací bod služby zajišťuje dlouhé umístění odchozího připojení ke službě oznamování, která je hostována na `https://*.manage.microsoft.com` . Ověřte, že proxy server, který se používá pro spojovací bod služby, nezobrazuje příliš rychle časový limit odchozích připojení. Pro odchozí připojení k tomuto koncovému bodu sítě Internet doporučujeme 3 minuty. <!--7820969-->