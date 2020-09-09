---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 8d456185e39df8d76b949baf26de755970a9a89b
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89563994"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Pokud je povolené Multi-Factor Authentication, většina funkcí připojení tenanta nefunguje.
<!--7986450, 7988266-->
**Scénář:** Pokud je počítač [poskytovatele služby SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) , který komunikuje se [spojovacím bodem služby](../../core/servers/deploy/configure/about-the-service-connection-point.md) , nakonfigurován na používání služby Multi-Factor Authentication, nebudete moci instalovat aplikace, spouštět dotazy CMPivot a provádět další akce z konzoly pro správu. Zobrazí se kód chyby 403, zakázáno.  

**Alternativní řešení:** Aktuálním řešením je nakonfigurovat hierarchii na výchozí úroveň ověřování **ověřování systému Windows**. Další informace najdete v [části ověřování v článku o poskytovateli serveru SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth).

