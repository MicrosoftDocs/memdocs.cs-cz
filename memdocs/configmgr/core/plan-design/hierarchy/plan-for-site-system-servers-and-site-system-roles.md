---
title: Plánování rolí systému lokality
titleSuffix: Configuration Manager
description: Při plánování Configuration Manager hierarchie zvažte systémové servery lokality a role systému lokality.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722442"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Plánování systémových serverů lokality a rolí systému lokality v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Každá Configuration Manager lokalita, kterou nainstalujete, obsahuje server lokality, který je **systémovým serverem lokality**. Lokalita může také obsahovat další systémové servery lokality na počítačích, které jsou vzdálené od serveru lokality. Systémové servery lokality (systém lokality nebo vzdálený systémový server lokality) podporují **role systému lokality**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a>Servery systému lokality  

Když nainstalujete roli systému lokality na počítač, bude tento počítač serverem systému lokality. V každé lokalitě můžete nainstalovat jeden nebo více dalších serverů systému lokality. Nemusíte instalovat další systémové servery lokality a můžete zvolit, že se mají spouštět všechny role systému lokality přímo na počítači serveru lokality. Každý systémový server lokality podporuje jednu nebo více rolí systému lokality. Další servery mohou rozšířit možnosti a kapacitu lokality tím, že sdílí zátěž pro zpracování, které role systému lokality místo na serveru.  

Když zvažujete přidání serveru systému lokality, ujistěte se, že server splňuje předpoklady pro zamýšlené použití. Přidejte ho taky do umístění v síti, které má dostatečnou šířku pásma pro komunikaci s očekávanými koncovými body. Mezi tyto koncové body patří server lokality, prostředky domény, cloudové umístění, servery systému lokality a klienti.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a>Role systému lokality  

Nainstalujte role systému lokality na server a poskytněte tak další možnosti pro lokalitu. Příklady obsahují:  

- Další body správy, aby lokalita mohla podporovat více zařízení, až po podporovanou kapacitu webu.  

- Další distribuční body pro rozšíření infrastruktury obsahu a vylepšení výkonu distribucí obsahu do zařízení.  

- Jedna nebo více rolí systému lokality, které jsou specifické pro danou funkci. Například bod aktualizace softwaru umožňuje spravovat aktualizace softwaru pro spravovaná zařízení. Bod služby Reporting Services umožňuje spouštět sestavy pro sledování, pochopení a sdílení informací o vašem prostředí.  

Různé Configuration Manager lokality mohou podporovat různé sady rolí systému lokality. Podporovaná sada rolí systému lokality závisí na typu lokality. (Typy lokalit zahrnují lokalitu centrální správy, primární lokality nebo sekundární lokality.) Topologie vaší hierarchie může omezit umístění některých rolí na určité typy lokalit. Třeba spojovací bod služby se podporuje jenom v lokalitě nejvyšší úrovně v hierarchii. Lokalita nejvyšší úrovně může být lokalita centrální správy nebo samostatná primární lokalita. Tato role není podporována v podřízené primární lokalitě nebo v sekundárních lokalitách.  

Po instalaci lokality můžete umístění některých rolí systému lokality přesunout z výchozího umístění na serveru lokality na jiný server. Například role bodu správy nebo distribučního bodu se ve výchozím nastavení instalují na primárním nebo sekundárním serveru lokality. Nainstalujte také další instance některých rolí systému lokality, abyste rozšířili možnosti vaší lokality a splňovali vaše obchodní požadavky. Některé role jsou povinné, zatímco jiné jsou nepovinné.  

### <a name="configuration-manager-site-server"></a>Server Configuration Manager lokality

Tato role identifikuje server, na kterém Configuration Manager instalační program pro instalaci lokality, nebo server, na který nainstalujete sekundární lokalitu. Tuto roli nemůžete přesunout ani odinstalovat, dokud se lokalita neodinstaluje.  

### <a name="configuration-manager-site-system"></a>Configuration Manager systém lokality

Tato role je přiřazená k jakémukoli počítači, na kterém buď nainstalujete lokalitu, nebo nainstalujete roli systému lokality. Tuto roli nelze přesunout ani odinstalovat, dokud z počítače neodeberete poslední roli systému lokality.  

### <a name="configuration-manager-component-site-system-role"></a>Role systému lokality Configuration Manager součásti

Tato role určuje systém lokality, na kterém běží instance služby **SMS Executive** . Je nutné, aby podporoval jiné role, jako jsou body správy. Tuto roli nelze přesunout ani odinstalovat, dokud z počítače neodeberete poslední příslušnou roli systému lokality.  

### <a name="configuration-manager-site-database-server"></a>Server databáze lokality Configuration Manager

Lokalita přiřadí tuto roli k systémovým serverům lokality, které obsahují instanci databáze lokality. Tuto roli můžete přesunout jenom na nový server spuštěním instalačního programu, aby se lokalita změnila tak, aby používala jinou instanci SQL Server k hostování databáze lokality.  

### <a name="sms-provider"></a>SMS Provider

Lokalita přiřadí tuto roli každému počítači, který je hostitelem instance poskytovatele serveru SMS. Poskytovatel je rozhraní mezi konzolou Configuration Manager a databází lokality. Ve výchozím nastavení se tato role automaticky nainstaluje na server lokality centrální správy a primárních lokalit. Nainstalujte další instance v každé lokalitě, abyste zajistili přístup dalším uživatelům s právy pro správu nebo redundanci.  

Pokud chcete nainstalovat další poskytovatele, spusťte instalační program Configuration Manager a [spravujte poskytovatele služby SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Pak nainstalujte další poskytovatele na další počítače. Na počítač nainstalujte jenom jednu instanci poskytovatele služby SMS. Tento počítač musí být ve stejné doméně jako server lokality.  

### <a name="application-catalog-web-service-point"></a>Bod webové služby Katalog aplikací

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Role systému lokality, která poskytuje informace o softwaru na webu Katalog aplikací z knihovny softwaru. I když je tato role podporovaná jenom v primárních lokalitách, můžete v lokalitě nebo ve víc lokalitách ve stejné hierarchii nainstalovat víc instancí této role.  

### <a name="application-catalog-website-point"></a>Bod webu Katalog aplikací

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Role systému lokality, která poskytuje uživatelům seznam dostupného softwaru z katalogu aplikací. I když je tato role podporovaná jenom v primárních lokalitách, můžete v lokalitě nebo ve víc lokalitách ve stejné hierarchii nainstalovat víc instancí této role.  

### <a name="asset-intelligence-synchronization-point"></a>Bod synchronizace katalogu Asset Intelligence

Role systému lokality, která se připojuje k Microsoftu a stahuje informace pro katalog funkce Asset Intelligence. Tato role také nahrává Nezařazeno do kategorie tituly, aby je Microsoft mohl v katalogu zvážit pro budoucí zahrnutí. Hierarchie podporuje pouze jednu instanci této role v lokalitě nejvyšší úrovně ve vaší hierarchii. Pokud rozbalíte samostatnou primární lokalitu do větší hierarchie, odinstalujte tuto roli z primární lokality. Pak ji nainstalujte v lokalitě centrální správy.

Další informace najdete v tématu [funkce Asset Intelligence v Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Bod registrace certifikátu

Role systému lokality, která komunikuje se serverem, na kterém je spuštěna služba zápisu síťových zařízení (NDES). Tato role spravuje požadavky na certifikáty zařízení, které používají Simple Certificate Enrollment Protocol (SCEP). Tato role je podporovaná jenom v primárních lokalitách a lokalitě centrální správy.

I když jediný bod registrace certifikátu může poskytovat funkce celé hierarchii, možná budete chtít nainstalovat víc instancí této role v lokalitě a ve více lokalitách ve stejné hierarchii. Tento návrh pomáhá s vyrovnáváním zatížení. Pokud v hierarchii existuje víc instancí, klienti se náhodně přiřadí k jednomu z bodů registrace certifikátu.  

Každý bod registrace certifikátu vyžaduje přístup k samostatné instanci NDES. Nemůžete nakonfigurovat dva nebo víc bodů registrace certifikátu tak, aby používaly stejnou instanci NDES. Kromě toho neinstalujte bod registrace certifikátu na stejný server, na kterém běží NDES.  

### <a name="cloud-management-gateway-connection-point"></a>Bod připojení brány pro správu cloudu

Role systému lokality pro komunikaci s [bránou pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Bod služby datového skladu

Bod služeb datového skladu použijte k ukládání a hlášení o dlouhodobých historických datech v prostředí Configuration Manager. Další informace najdete v tématu [datový sklad](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Distribuční bod

Role systému lokality, která obsahuje zdrojové soubory pro klienty ke stažení, například:

- Obsah aplikace
- Balíčky softwaru
- Aktualizace softwaru
- Image operačního systému
- Spouštěcí image  

Ve výchozím nastavení se tato role při instalaci nové primární nebo sekundární lokality nainstaluje na server lokality. Tato role není podporována v lokalitě centrální správy. Nainstalujte více instancí této role v podporované lokalitě a ve více lokalitách ve stejné hierarchii. Další informace najdete v tématech [základní koncepty správy obsahu](fundamental-concepts-for-content-management.md)a [Správa obsahu a infrastruktury obsahu](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="endpoint-protection-point"></a>Bod ochrany koncového bodu Endpoint Protection

Role systému lokality, kterou Configuration Manager používá k přijetí licenčních podmínek Endpoint Protection a ke konfiguraci výchozího členství pro službu Cloud Protection. Hierarchie podporuje jenom jednu instanci této role a ta se musí nacházet v lokalitě nejvyšší úrovně. Pokud rozbalíte samostatnou primární lokalitu do větší hierarchie, odinstalujte tuto roli z primární lokality a pak ji nainstalujte v lokalitě centrální správy. Další informace najdete v tématu [Endpoint Protection v Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Bod registrace

Role systému lokality, která používá certifikáty PKI pro Configuration Manager k registraci mobilních zařízení a počítačů s macOS. I když je tato role podporovaná jenom v primárních lokalitách, můžete v lokalitě nebo ve víc lokalitách ve stejné hierarchii nainstalovat víc instancí této role.  

Pokud uživatel zapíše mobilní zařízení pomocí Configuration Manager a účet uživatele služby Active Directory je v doménové struktuře, která je pro doménovou strukturu serveru lokality nedůvěryhodná, nainstalujte bod zápisu do doménové struktury uživatele. Pak Configuration Manager může ověřit uživatele.  

### <a name="enrollment-proxy-point"></a>Zprostředkující bod registrace

Role systému lokality, která spravuje Configuration Manager žádosti o registraci z mobilních zařízení a počítačů s macOS. I když je tato role podporovaná jenom v primárních lokalitách, můžete v lokalitě nebo ve víc lokalitách ve stejné hierarchii nainstalovat víc instancí této role.  

Pokud podporujete mobilní zařízení na internetu, nainstalujte zprostředkující bod registrace v hraniční síti a nainstalujte ho do intranetu.

### <a name="exchange-server-connector"></a>konektor systému Exchange Server

Informace o této roli najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Bod záložního stavu

Role systému lokality, která vám pomůže monitorovat instalaci klienta. Identifikuje klienty, kteří nejsou spravováni, protože nemohou komunikovat se svým bodem správy. I když je tato role podporovaná jenom v primárních lokalitách, můžete v lokalitě nebo ve víc lokalitách ve stejné hierarchii nainstalovat víc instancí této role.

### <a name="management-point"></a>Bod správy

Role systému lokality, která poskytuje klientům informace o umístění zásad a služeb. Také přijímá konfigurační data od klientů.  

Ve výchozím nastavení se tato role při instalaci nové primární nebo sekundární lokality nainstaluje na server lokality. Primární lokality podporují víc instancí této role. Sekundární lokality podporují jeden bod správy. Tato role v sekundární lokalitě se také označuje jako bod správy proxy, a proto poskytuje místní kontaktní bod pro klienty, kteří získají zásady počítače a uživatele.  

Nastavte body správy pro podporu protokolu HTTP nebo HTTPs. Můžou taky podporovat mobilní zařízení, která spravujete pomocí Configuration Manager místní správy mobilních zařízení (MDM). Aby se snížilo zatížení při zpracování na serveru databáze lokality podle bodů správy v rámci požadavků na služby od klientů, použijte [repliky databáze pro body správy](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="reporting-services-point"></a>Bod služby Reporting services

Role systému lokality, která se integruje s SQL Server Reporting Services k vytváření a správě sestav pro Configuration Manager. Tato role je podporovaná v primárních lokalitách a lokalitě centrální správy a v podporované lokalitě můžete nainstalovat víc instancí této role. Další informace najdete v tématu [Plánování vytváření sestav](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Spojovací bod služby

Role systému lokality, která odesílá data o využití z vaší lokality a je nutná k zpřístupnění aktualizací Configuration Manager v konzole nástroje. Hierarchie podporuje jenom jednu instanci této role a ta se musí nacházet v lokalitě nejvyšší úrovně ve vaší hierarchii. Pokud rozbalíte samostatnou primární lokalitu do větší hierarchie, odinstalujte tuto roli z primární lokality a pak ji nainstalujte v lokalitě centrální správy. Další informace najdete v tématu [o spojovacím bodu služby](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Bod aktualizace softwaru

Role systému lokality, která se integruje s Windows Server Update Services (WSUS) za účelem poskytování aktualizací softwaru pro Configuration Manager klientů. Tato role je podporovaná ve všech lokalitách:  

- Nainstalujte tento systém lokality v lokalitě centrální správy pro synchronizaci se službou WSUS.  

- Nastavte každou instanci této role v podřízených primárních lokalitách na synchronizaci s lokalitou centrální správy.  

- Pokud je přenos dat přes síť pomalý, zvažte instalaci bodu aktualizace softwaru v sekundárních lokalitách.  

Další informace najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Bod migrace stavu

Při migraci počítače do nového operačního systému Tato role systému lokality ukládá data o stavu uživatele. Tato role je podporována v primárních lokalitách a v sekundárních lokalitách. Nainstalujte více instancí této role v lokalitě a ve více lokalitách ve stejné hierarchii. Další informace o ukládání stavu uživatele, když nasazujete operační systém, najdete v tématu [Správa stavu uživatele](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Další kroky

Některé Configuration Manager role systému lokality vyžadují připojení k Internetu. Pokud vaše prostředí vyžaduje internetový provoz pro použití proxy server, nakonfigurujte tyto role systému lokality tak, aby používaly proxy server. Další informace najdete v tématu [Podpora proxy serveru](../network/proxy-server-support.md).  
