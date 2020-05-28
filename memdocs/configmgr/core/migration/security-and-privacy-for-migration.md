---
title: Zabezpečení a ochrana osobních údajů při migraci
titleSuffix: Configuration Manager
description: Získejte osvědčené postupy zabezpečení a informace o ochraně osobních údajů při migraci do vaší Configuration Manager prostředí aktuální pobočky.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad92e4906c45b5c720ab35efc055449a27cc0850
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906217"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Zabezpečení a ochrana osobních údajů pro migraci do Configuration Manager aktuální větve

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje osvědčené postupy zabezpečení a informace o ochraně osobních údajů při migraci do vaší Configuration Manager prostředí aktuální pobočky.  

## <a name="security-best-practices-for-migration"></a>Osvědčené postupy zabezpečení při migraci  
 Pro migraci použijte následující osvědčené postupy zabezpečení.  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Použijte účet počítače pro účet poskytovatele služby SMS zdrojového webového serveru a zdrojovou lokalitu SQL Server účet, nikoli uživatelský účet.|Pokud musíte použít uživatelský účet pro migraci, po dokončení migrace odeberte podrobnosti účtu.|  
|Při migraci obsahu z distribučního bodu ve zdrojové lokalitě do distribučního bodu v cílové lokalitě použijte protokol IPsec.|I když je migrovanému obsahu zjištěna hodnota hash pro detekci manipulace, pokud jsou data během přenosu změněna, migrace se nezdaří.|  
|Omezte a monitorujte administrativní uživatele, kteří mohou vytvářet úlohy migrace.|Integrita databáze cílové hierarchie závisí na integritě dat, která uživatel s právy pro správu zvolí pro import ze zdrojové hierarchie. Kromě toho může tento administrativní uživatel číst všechna data ze zdrojové hierarchie.|  

### <a name="security-issues-for-migration"></a>Problémy se zabezpečením při migraci  
Migrace má následující problémy se zabezpečením:  

-   Klienti, kteří jsou zablokovaný ze zdrojové lokality, se můžou úspěšně přiřadit k cílové hierarchii předtím, než se migruje jejich záznam klienta.  

     I když Configuration Manager zachovává blokovaný stav klientů, které migrujete, může se klient úspěšně přiřadit k cílové hierarchii, pokud k přiřazení dojde před dokončením migrace záznamu klienta.  

-   Zprávy o auditu se nemigrují.  

Při migraci dat ze zdrojové lokality do cílové lokality ztratíte veškeré informace o auditování ze zdrojové hierarchie.  

## <a name="privacy-information-for-migration"></a>Informace o ochraně osobních údajů pro migraci  
 Migrace zjišťuje informace z databází lokality, které identifikujete ve zdrojové infrastruktuře, a ukládá tato data do databáze v cílové hierarchii. Informace, které Configuration Manager mohou zjišťovat ze zdrojové lokality nebo hierarchie, jsou závislé na funkcích, které byly povoleny ve zdrojovém prostředí, a na operacích správy, které byly provedeny v tomto zdrojovém prostředí.  

 Další informace o zabezpečení a ochraně osobních údajů najdete v jednom z následujících témat:  

-   Další informace o ochraně osobních údajů pro Configuration Manager 2007 najdete v tématu [zabezpečení a ochrana osobních údajů pro Configuration Manager 2007](https://docs.microsoft.com/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10)) v knihovně dokumentace ke službě Configuration Manager 2007.  

-   Další informace o ochraně osobních údajů pro System Center 2012 Configuration Manager najdete v tématu [zabezpečení a ochrana osobních údajů pro System center 2012 Configuration Manager](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10)) v knihovně dokumentace nástroje system center 2012 Configuration Manager.  

-   Další informace o ochraně osobních údajů pro Configuration Manager najdete v tématu [zabezpečení a ochrana osobních údajů pro Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Můžete migrovat některá nebo všechna podporovaná data ze zdrojové lokality do cílové hierarchie.  

Migrace není ve výchozím nastavení povolená a vyžaduje několik kroků konfigurace. Informace o migraci nejsou odesílány společnosti Microsoft.  

Před migrací dat ze zdrojové hierarchie zvažte své požadavky na ochranu osobních údajů.  
