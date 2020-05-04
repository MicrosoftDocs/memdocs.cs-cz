---
title: Plánování vytváření sestav
titleSuffix: Configuration Manager
description: Z podrobných informací o instalaci zabezpečení a šířky pásma sítě je důležité naplánovat vytváření sestav v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713678"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Plánování vytváření sestav v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vytváření sestav v Configuration Manager poskytuje sadu nástrojů a prostředků, které vám pomůžou používat pokročilé možnosti vytváření sestav SQL Server Reporting Services nebo Server sestav Power BI. Následující části vám pomůžou při plánování vytváření sestav v Configuration Manager.

## <a name="where-to-install-the-reporting-services-point"></a>Kam se má nainstalovat bod služby Reporting Services

Při spouštění sestav Configuration Manager v lokalitě mají sestavy přístup k informacím v databázi lokality, ve které se připojuje. Následující části vám pomohou při určení místa instalace bodu služby Reporting Services a používaného zdroje dat.

> [!NOTE]
> Další informace o plánování systémů lokalit v nástroji Configuration Manager najdete v tématu [Přidání rolí systému lokality](../deploy/configure/add-site-system-roles.md).

### <a name="supported-site-system-servers"></a> Podporované servery systému lokality

Bod služby Reporting Services můžete nainstalovat v lokalitě centrální správy (CAS) a primárních lokalitách. Funguje na více systémech lokality v lokalitě a v jiných lokalitách v hierarchii. Configuration Manager nepodporuje bod služeb generování sestav v sekundárních lokalitách. První bod služby Reporting Services v lokalitě je nastaven jako výchozí server sestav. V lokalitě můžete přidat více bodů služby Reporting Services, ale sestavy Configuration Manager aktivně používají výchozí server sestav v každé lokalitě. Nainstalujte bod služby Reporting Services na serveru lokality nebo ve vzdáleném systému lokality. Nejlepšího výkonu dosáhnete, když SQL Server Reporting Services používáte na vzdáleném serveru systému lokality.

### <a name="data-replication-considerations"></a> Aspekty replikace dat

Při určování místa instalace bodů služby Reporting Services zvažte následující skutečnosti:

- Bod služby Reporting Services s databází CAS jako zdroj dat pro generování sestav má přístup ke všem globálním datům a datům lokality v hierarchii Configuration Manager. Pokud potřebujete sestavy obsahující data lokality pro více lokalit v hierarchii, zvažte instalaci bodu služby Reporting Services do systému lokality v certifikačních autoritách. Pak použijte svou databázi jako zdroj dat pro vytváření sestav.

- Bod služby Reporting Services, jehož zdrojem dat pro sestavy je databáze podřízené primární lokality, má přístup k globálním datům a datům lokality pouze pro místní primární lokalitu a všechny podřízené sekundární lokality. Data lokality pro ostatní primární lokality v hierarchii Configuration Manager se nereplikují do této primární lokality. Služba Reporting Services nemůže získat přístup k datům lokality pro jiné primární lokality. Pokud potřebujete sestavy obsahující data lokality pro určitou primární lokalitu nebo globální data a nechcete, aby uživatel měl přístup k datům lokality z jiných primárních lokalit, nainstalujte bod služby Reporting Services do systému lokality v primární lokalitě. Pak jako zdroj dat pro sestavy použijte databázi primární lokality.

Další informace o globálních datech a data lokality najdete v tématu [typy dat](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Aspekty šířky pásma sítě

V závislosti na tom, jak nakonfigurujete lokalitu, systémy lokality ve stejné lokalitě spolu navzájem komunikují pomocí protokolu SMB (Server Message Block), HTTP nebo HTTPS. Configuration Manager tuto komunikaci nespravuje. Může k tomu dojít kdykoli bez řízení šířky pásma sítě. Než nainstalujete roli bodu služby Reporting Services do systému lokality, zkontrolujte dostupnou šířku pásma sítě.

Další informace o plánování systémů lokalit najdete v tématu [Přidání rolí systému lokality](../deploy/configure/add-site-system-roles.md).

## <a name="plan-for-role-based-administration"></a>Plánování správy na základě rolí

Zabezpečení pro vytváření sestav je podobné jako u jiných objektů v Configuration Manager, kde můžete přiřadit role zabezpečení a oprávnění správcům. Správci mohou spouštět a upravovat pouze ty sestavy, ke kterým mají příslušná zabezpečovací práva. Chcete-li spustit sestavy v konzole Configuration Manager, uživatelé potřebují právo **číst** pro oprávnění **lokalita** a oprávnění konfigurovaná pro konkrétní objekty.

Na rozdíl od jiných objektů v Configuration Manager jsou ve službě Reporting Services nakonfigurována také práva zabezpečení, která jste nastavili pro administrativní uživatele v konzole Configuration Manager. Když konfigurujete práva zabezpečení v konzole Configuration Manager, bod služby Reporting Services se připojí ke službě Reporting Services a nastaví příslušná oprávnění pro sestavy.

Například role zabezpečení **správce aktualizací softwaru** má oprávnění **Spustit sestavu** a **Upravit sestavu** . Uživatelé s rolí **správce aktualizace softwaru** mohou spouštět a upravovat pouze sestavy aktualizací softwaru. Konzola Configuration Manager nezobrazuje sestavy pro ostatní objekty v této roli. Výjimkou z tohoto chování je, že některé sestavy nejsou přidružené ke konkrétním Configuration Manager zabezpečitelné objekty. U těchto sestav musí mít správce právo **Číst** pro oprávnění **Lokalita** , aby je mohl spouštět, a právo **Změnit** pro oprávnění **Lokalita** , aby je mohl upravovat.  

> [!IMPORTANT]
> Pro uživatele z jiné domény, než je účet bodu služby Reporting Services pro úspěšné spouštění sestav, navažte mezi těmito dvěma doménami obousměrný vztah důvěryhodnosti.

Sestavy plně podporují správu na základě rolí. Configuration Manager filtruje data všech zahrnutých sestav na základě oprávnění uživatele, který sestavu spouští. Uživatelé s konkrétními rolemi mohou zobrazit pouze informace definované pro své role.

Další informace o právech zabezpečení pro vytváření sestav najdete v tématu [Konfigurace generování sestav](configuring-reporting.md).

Další informace o správě na základě rolí v Configuration Manager najdete v tématu [Konfigurace správy na základě rolí](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Doporučení pro vytváření sestav

Při vytváření sestav v Configuration Manager Vezměte v úvahu následující doporučení a tipy:

- Nejlepšího výkonu dosáhnete instalací bodu služby Reporting Services ve vzdáleném systému lokality. I když ho můžete nainstalovat na server lokality, bod služby Reporting Services se při jeho instalaci ve vzdáleném systému lokality provede nejlépe. Když tato role provádí zpracování na pozadí, může soutěžit o systémové prostředky s jinými rolemi. Existuje mnoho proměnných, které je třeba vzít v úvahu při výkonu lokality a role, ale obecně Tato konfigurace vylepšuje vytváření sestav a celkový výkon lokality.

- Optimalizujte SQL Server Reporting Services dotazy. Obvykle se zpoždění vytváření sestav nacházejí v důsledku doby spuštění dotazů a načtení výsledků. Microsoft SQL Server nástroje, jako je například analyzátor dotazů a profileru, vám můžou přispět k optimalizaci dotazů.

- Naplánujte, aby zpracování předplatného sestavy běželo mimo dobu standardu Office. Kdykoli je to možné, může zpracování předplatných v době mimo špičku minimalizovat zpracování procesoru na serveru databáze lokality Configuration Manager. Tento postup také zlepšuje dostupnost pro neočekávané požadavky na sestavy.

- Aktualizace webu uchovávají předdefinované sestavy. Pokud upravíte standardní sestavu, při aktualizaci lokality přejmenuje sestavu pomocí předpony podtržítka (`_`). Tím se zajistí, že aktualizace lokality nepřepisuje upravenou sestavu standardní sestavou.

## <a name="security-and-privacy"></a>Zabezpečení a ochrana osobních údajů

V sestavách Configuration Manager se zobrazují informace, které shromažďuje během standardních Configuration Managerch operací správy. Můžete například zobrazit sestavu informací, které Configuration Manager shromažďovat ze zjišťování nebo z inventáře. Sestavy mohou také obsahovat informace o aktuálním stavu pro operace správy klienta, například nasazování softwaru a kontrolu kompatibility.

Další informace o všech doporučeních zabezpečení a ochraně osobních údajů pro Configuration Manager operace, které mohou generovat data, která lze zobrazit v sestavách, naleznete v tématu [zabezpečení a ochrana osobních údajů pro Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Další kroky

[Požadavky vytváření sestav](prerequisites-for-reporting.md)
