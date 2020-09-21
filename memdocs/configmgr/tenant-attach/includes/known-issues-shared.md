---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: e6023808f60d0ac7753745d5882516dda0f85be2
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90802931"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-configuration-manager-site-is-configured-to-require-multi-factor-authentication-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Pokud je lokalita Configuration Manager nakonfigurovaná tak, aby vyžadovala Multi-Factor Authentication, většina funkcí připojení tenantů nefunguje
<!--7986450, 7988266-->
**Scénář:** Pokud je počítač [poskytovatele služby SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) , který komunikuje se [spojovacím bodem služby](../../core/servers/deploy/configure/about-the-service-connection-point.md) , nakonfigurován na používání služby Multi-Factor Authentication, nebudete moci instalovat aplikace, spouštět dotazy CMPivot a provádět další akce z konzoly pro správu. Zobrazí se kód chyby 403, zakázáno.  

**Alternativní řešení:** Aktuálním řešením je nakonfigurovat místní hierarchii na výchozí úroveň ověřování **ověřování systému Windows**. Další informace najdete v [části ověřování v článku o poskytovateli serveru SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth).

