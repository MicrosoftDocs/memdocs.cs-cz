---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 13a5b771f712420939f87073854faab3c38270c9
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252470"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> Když je poskytovatel serveru SMS vzdálený od certifikačních autorit, může dojít k vnitřní chybě serveru z konzoly pro správu.

**Chybová zpráva:** Kód chyby on-Prem: 500 interní chyba serveru

**Scénář 1:** Pokud používáte Configuration Manager verze 2002 a pro certifikační autority existuje vzdálený poskytovatel, může dojít k vnitřní chybě serveru z konzoly pro správu.

**Scénář 2:** Při spuštění Configuration Manager verze 2006 se tato chyba může zobrazit i v případě, že spojovacímu bodu služby se nepovede připojit k poskytovateli v primární lokalitě a vrátit se k poskytovateli pro certifikační autority. 

**Scénář 3:** Pokud byly certifikační autority upgradovány na verzi 2006, ale ještě nebyl upgradován primární server, požadavky budou směrovány přes poskytovatele CAS. Pokud je zprostředkovatel vzdálený, může dojít k vnitřní chybě serveru z konzoly pro správu. 

**Alternativní řešení:** Postupujte podle pokynů pro [certifikační autority](../../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) s scénářem vzdáleného poskytovatele v článku CMPivot, abyste mohli vyřešit tento scénář dvojího směrování.

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Pokud je povolené Multi-Factor Authentication, většina funkcí připojení tenanta nefunguje.
<!--7986450, 7988266-->
**Scénář:** Pokud je počítač [poskytovatele služby SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) , který komunikuje se [spojovacím bodem služby](../../core/servers/deploy/configure/about-the-service-connection-point.md) , nakonfigurován na používání služby Multi-Factor Authentication, nebudete moci instalovat aplikace, spouštět dotazy CMPivot a provádět další akce z konzoly pro správu. Zobrazí se kód chyby 403, zakázáno.  

**Alternativní řešení:** Aktuálním řešením je nakonfigurovat hierarchii na výchozí úroveň ověřování **ověřování systému Windows**. Další informace najdete v [části ověřování v článku o poskytovateli serveru SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth).

