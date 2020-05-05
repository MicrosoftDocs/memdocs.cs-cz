---
title: Základy zabezpečení
titleSuffix: Configuration Manager
description: Přečtěte si o vrstvách zabezpečení v Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722834"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Základy zabezpečení pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek shrnuje následující základní součásti zabezpečení libovolného Configuration Managerho prostředí:
- [Vrstvy zabezpečení](#bkmk_layers)
- [Správa na základě rolí](#bkmk_rba)
- [Zabezpečení koncových bodů klientů](#bkmk_endpoints)
- [Účty Configuration Manager a skupiny](#bkmk_accounts)
- [Ochrana osobních údajů](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a>Vrstvy zabezpečení

Zabezpečení pro Configuration Manager se skládá z následujících vrstev: 
- [OPERAČNÍ systém Windows a zabezpečení sítě](#bkmk_layer-windows)
- [Síťová infrastruktura: brány firewall, zjišťování neoprávněných vniknutí, infrastruktura veřejných klíčů (PKI)](#bkmk_layer-network)
- [Configuration Manager kontroly zabezpečení](#bkmk_layer-cm)
- [SMS Provider](#bkmk_layer-provider)
- [Oprávnění databáze webu](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a>OPERAČNÍ systém Windows a zabezpečení sítě
První vrstvu poskytují funkce zabezpečení systému Windows pro operační systém i síť. Tato vrstva obsahuje následující součásti:  

-   Sdílení souborů pro přenos souborů mezi součástmi Configuration Manager  

-   Seznamy řízení přístupu (ACL), které pomáhají zabezpečit soubory a klíče registru  

-   Protokol IPsec (Internet Protocol Security), který vám může přispět k zabezpečení komunikace  

-   Zásady skupiny nastavení zásad zabezpečení  

-   Oprávnění modelu DCOM (Distributed Component Object Model) pro distribuované aplikace, jako je například konzola Configuration Manager  

-   Služba AD DS (Active Directory Domain Services) pro uchovávání objektů zabezpečení  

-   Zabezpečení účtů systému Windows včetně některých skupin, které Configuration Manager vytvoří během instalace  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a>Síťová infrastruktura

Další bezpečnostní komponenty, jako jsou brány firewall a zjišťování neoprávněných vniknutí, vám pomůžou zajistit ochranu celého prostředí. Certifikáty vydané oborovými standardními implementacemi infrastruktury veřejných klíčů (PKI) umožňují ověřování, podepisování a šifrování.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a>Configuration Manager kontroly zabezpečení

Kromě zabezpečení poskytovaného Windows serverem a síťovou infrastrukturou Configuration Manager řídí přístup ke konzole a prostředkům několika způsoby. Ve výchozím nastavení mají oprávnění k souborům a klíčům registru, které konzola Configuration Manager vyžaduje v počítačích, kde ji instalujete, pouze místní správci.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a>Poskytovatel serveru SMS

Další vrstva zabezpečení je založena na přístupu prostřednictvím schématu WMI (Windows Management Instrumentation), konkrétně prostřednictvím poskytovatele služby SMS. Poskytovatel serveru SMS je Configuration Manager komponenta, která uděluje uživateli přístup k dotazům na informace v databázi lokality. Ve výchozím nastavení je přístup k poskytovateli omezen na členy místní skupiny SMS Admins . Tato skupina nejprve obsahuje pouze uživatele, který nainstaloval Configuration Manager. Chcete-li přidělit jiným účtům oprávnění k úložišti modelu CIM (Common Information Model) a k poskytovateli služby SMS, přidejte tyto účty do skupiny SMS Admins.  

Počínaje verzí 1810 můžete určit minimální úroveň ověřování pro správce pro přístup k Configuration Manager lokalit. Tato funkce vynutila správcům přihlášení k systému Windows s požadovanou úrovní. <!--1357013-->  

Další informace najdete v tématu [plánování poskytovatele serveru SMS](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a>Oprávnění databáze webu

Poslední vrstva zabezpečení je založena na oprávněních k objektům v databázi lokality. Ve výchozím nastavení může místní systémový účet a uživatelský účet, který jste použili k instalaci Configuration Manager, spravovat všechny objekty v databázi lokality. Udělení a omezení oprávnění dalším uživatelům s právy pro správu v konzole Configuration Manager pomocí správy na základě rolí.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a>Správa na základě rolí  

 Configuration Manager používá správu na základě rolí k zajištění zabezpečení objektů, jako jsou kolekce, nasazení a lokality. Tento model správy centrálně definuje a spravuje nastavení zabezpečení přístupu ke všem lokalitám a nastavením lokalit v hierarchii. 

 Správce přiřadí *role zabezpečení* správcům a oprávněním skupin. Oprávnění jsou propojena s různými typy objektů Configuration Manager, například k vytvoření nebo změně nastavení klienta. 

 *Obory zabezpečení* seskupují určité instance objektů, za jejichž správu je správce zodpovědný, například aplikace, která instaluje systém Microsoft Office. 

 Kombinace rolí zabezpečení, oborů zabezpečení a kolekcí definuje objekty, které může administrativní uživatel zobrazit a spravovat. Configuration Manager nainstaluje některé výchozí role zabezpečení pro typické úlohy správy. Vytvořte vlastní role zabezpečení pro podporu specifických podnikových požadavků.  

 Další informace najdete v tématu [Konfigurace správy na základě rolí](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a>Zabezpečení koncových bodů klienta  

 Configuration Manager zabezpečuje komunikaci klientů s rolemi systému lokality pomocí certifikátů podepsaných svým držitelem nebo certifikátů PKI nebo Azure Active Directory (Azure AD) tokeny. Některé scénáře vyžadují použití certifikátů PKI. Například [Internetová správa klientů](../clients/manage/plan-internet-based-client-management.md)a pro [klienty mobilních zařízení](../../mdm/plan-design/plan-on-premises-mdm.md).  

 Role systému lokality, ke kterým se klienti připojují, můžete nakonfigurovat buď pomocí protokolu HTTPS, nebo prostřednictvím komunikace klienta HTTP. Klientské počítače vždy komunikují s použitím nejbezpečnější dostupné metody. Pokud máte role systémů lokality, které umožňují komunikaci pomocí protokolu HTTP, klientské počítače se vrátí k použití metody méně zabezpečené komunikace.  

 Další informace najdete v tématu [Plánování zabezpečení](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a>Účty Configuration Manager a skupiny  

 Configuration Manager používá pro většinu operací lokalit místní systémový účet. Některé úlohy správy mohou vyžadovat vytvoření a údržbu dalších účtů. Configuration Manager během instalace vytvoří několik výchozích skupin a rolí SQL Server. Je možné, že budete muset ručně přidat počítače nebo uživatelské účty do výchozích skupin a SQL Server rolí.  

 Další informace najdete v tématu [účty používané v Configuration Manager](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a>Důvěrnost  

 Před implementací Configuration Manager zvažte své požadavky na ochranu osobních údajů. I když produkty pro správu podniku nabízejí mnoho výhod, protože můžou efektivně spravovat spoustu klientů, může tento software ovlivnit ochranu osobních údajů uživatelů ve vaší organizaci. Configuration Manager obsahuje řadu nástrojů pro shromažďování dat a monitorování zařízení. Některé nástroje mohou zvýšit ochranu osobních údajů ve vaší organizaci.  

 Když například nainstalujete klienta Configuration Manager, povolí se ve výchozím nastavení spousta nastavení správy. Tato konfigurace způsobí, že klientský software pošle informace do Configuration Manager lokality. Lokalita uchovává informace o klientech v databázi lokality. Informace o klientovi nejsou odesílány přímo společnosti Microsoft. Další informace najdete v tématu [Diagnostika a data o využití](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Viz také

- [Plánování zabezpečení](../plan-design/security/plan-for-security.md)  

- [Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurace zabezpečení](../plan-design/security/configure-security.md)   

- [Komunikace mezi koncovými body](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Technické informace o kryptografických ovládacích prvcích](../plan-design/security/cryptographic-controls-technical-reference.md)  
