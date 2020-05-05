---
title: Předpoklady pro lokality
titleSuffix: Configuration Manager
description: Přečtěte si informace o požadavcích pro instalaci různých typů Configuration Manager lokalit.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8362dbf5cf7264c19f683ce5a224f1e0ec348b36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718144"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Předpoklady pro instalaci Configuration Managerch lokalit

*Platí pro: Configuration Manager (Current Branch)*

Než začnete s instalací lokality, přečtěte si informace o požadavcích na instalaci různých typů Configuration Manager lokalit.


## <a name="primary-sites-and-the-central-administration-site"></a>Primární lokality a lokalita centrální správy

Následující požadavky platí pro instalaci jednoho z následujících typů:

- Lokalita centrální správy jako první lokalita hierarchie
- Samostatná primární lokalita
- Podřízená primární lokalita

Pokud instalujete lokalitu centrální správy jako součást rozšíření hierarchie, přečtěte si téma [rozšíření samostatné primární lokality](#bkmk_expand).

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a>Předpoklady pro instalaci primární lokality nebo lokality centrální správy  

- Musí být nainstalovány potřebné role, funkce a součásti systému Windows Server. Další informace najdete v tématu [požadavky na systém lokality](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq) .  

- Uživatelský účet, který nainstaluje lokalitu, musí mít následující oprávnění:  

    - **Správce** na následujících serverech:  
        - Server lokality  
        - Každý server, který je hostitelem **databáze lokality**  
        - Každá instance **poskytovatele služby SMS** pro danou lokalitu  

    - **Správce** systému v instanci SQL Server, která je hostitelem databáze lokality  

        > [!IMPORTANT]  
        > Po dokončení instalace Configuration Manager musí účet počítače serveru lokality uchovávat práva správce systému pro SQL Server. Neodstraňujte z tohoto účtu práva správce systému SQL.  

- Pokud instalujete primární lokalitu, budete potřebovat následující další práva:  

    - **Správce** na dalších serverech, kde instalujete počáteční bod správy a distribuční bod, pokud není na serveru lokality  

- Pokud instalujete novou podřízenou primární lokalitu pod lokalitou centrální správy, budete potřebovat následující dodatečná práva:  

    - **Správce** na serveru, který je hostitelem lokality centrální správy  

    - Práva pro správu na základě rolí v rámci Configuration Manager rovnocenná roli zabezpečení **správce infrastruktury** nebo správce s **úplnými oprávněními** .  

- Použijte správné zdrojové instalační soubory a spusťte instalační program z tohoto umístění. Informace o správných zdrojových souborech, které se mají použít k instalaci různých typů lokalit, najdete v tématu [Možnosti instalace různých typů lokalit](prepare-to-install-sites.md#bkmk_options).  

- Webový server musí mít přístup k aktualizovaným instalačním souborům od společnosti Microsoft, a to jedním z následujících způsobů:  

    - Než začnete s instalací, Stáhněte si a uložte kopii těchto souborů v místní síti. Další informace najdete v tématu Nástroj pro [stažení instalačního programu](setup-downloader.md).  

    - Pokud místní kopie tohoto souboru není k dispozici, server lokality musí mít přístup k Internetu. Během instalace tyto soubory stáhne od Microsoftu.  

- Server lokality a Server databáze lokality musí splňovat všechny požadované konfigurace. Před zahájením instalace Configuration Manager [Spusťte ručně kontrolu požadovaných součástí](prerequisite-checker.md) a identifikujte a opravte problémy.  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a>Předpoklady rozšíření samostatné primární lokality

Samostatná primární lokalita musí splňovat následující požadavky, aby ji bylo možné rozšířit do hierarchie s lokalitou centrální správy:

#### <a name="source-file-version-matches-site-version"></a>Verze zdrojového souboru odpovídá verzi lokality

Nainstalujte novou lokalitu centrální správy pomocí média z disku CD-ROM. Nejnovější složku, která odpovídá verzi samostatné primární lokality. Chcete-li zajistit, aby se verze shodovaly, použijte zdrojové soubory, které se nacházejí na [disku CD. Poslední složka](../../manage/the-cd.latest-folder.md) v samostatné primární lokalitě.

Další informace o správných zdrojových souborech, které se mají použít k instalaci různých lokalit, najdete v tématu [Možnosti instalace různých typů lokalit](prepare-to-install-sites.md#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Zastavit aktivní migraci z jiné hierarchie

Samostatnou primární lokalitu nelze nakonfigurovat k migraci dat z jiné hierarchie Configuration Manager. Zastavte aktivní migraci do samostatné primární lokality z jiných hierarchií Configuration Manager a odeberte všechny konfigurace pro migraci. Mezi tyto konfigurace patří:

- Úlohy migrace, které nebyly dokončeny  
- Shromažďování dat  
- Konfigurace aktivní zdrojové hierarchie  

Tato konfigurace je nezbytná, protože Configuration Manager migruje data z lokality nejvyšší úrovně v hierarchii. Když rozbalíte samostatnou primární lokalitu, konfigurace pro migraci se nepřesunou do lokality centrální správy.  

Pokud po rozšíření samostatné primární lokality překonfigurujete migraci v primární lokalitě, lokalita centrální správy provede operace migrace.

Další informace o konfiguraci migrace najdete v tématu [Konfigurace zdrojových hierarchií a zdrojových lokalit pro migraci](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

#### <a name="computer-account-as-administrator"></a>Účet počítače jako správce

Počítačový účet serveru, který je hostitelem nové lokality centrální správy, musí být členem skupiny **správců** na serveru samostatné primární lokality.

Aby bylo možné úspěšně rozšířit samostatnou primární lokalitu, účet počítače nové lokality centrální správy musí mít práva **správce** v samostatné primární lokalitě. To se vyžaduje jenom během rozšiřování lokality. Až se rozšíření lokality dokončí, můžete účet odebrat ze skupiny uživatelů v primární lokalitě.  

#### <a name="installation-account-permissions"></a>Oprávnění účtu instalace

Uživatelský účet, který spouští Configuration Manager instalačnímu programu pro instalaci nové lokality centrální správy, musí mít oprávnění pro správu na základě rolí v samostatné primární lokalitě.

Chcete-li nainstalovat lokalitu centrální správy jako součást rozšíření lokality, uživatelský účet, který spouští instalační program nástroje pro instalaci lokality centrální správy, musí být definován v rámci správy na základě rolí v samostatné primární lokalitě jako správce s **úplnými oprávněními** nebo **správcem infrastruktury**.

Další informace, včetně úplného seznamu požadovaných oprávnění, najdete v tématu [účet instalace lokality](../../../plan-design/hierarchy/accounts.md#site-installation-account).

#### <a name="top-level-site-roles"></a>Role webů nejvyšší úrovně

Před rozšířením lokality odinstalujte následující role systému lokality ze samostatné primární lokality:

- funkce Asset Intelligence bod synchronizace  
- Bod ochrany koncového bodu Endpoint Protection  
- Spojovací bod služby  

Configuration Manager podporuje pouze tyto role v lokalitě nejvyšší úrovně v hierarchii. Tyto role systému lokality odinstalujte před rozšířením samostatné primární lokality. Po rozšíření lokality přeinstalujte tyto role systému lokality v lokalitě centrální správy.  

Všechny ostatní role systému lokality mohou zůstat nainstalovány v primární lokalitě.  

#### <a name="open-the-sql-server-service-broker-port"></a>Otevřete port SQL Server Service Broker

Je nutné, aby byl pro SQL Server Service Broker (SSB) mezi samostatnou primární lokalitou a serverem pro lokalitu centrální správy otevřený port sítě.  

Aby bylo možné úspěšně replikovat data mezi lokalitou centrální správy a primární lokalitou, Configuration Manager vyžaduje otevřený port mezi dvěma lokalitami, aby mohl SSB použít. Když nainstalujete lokalitu centrální správy a rozbalíte samostatnou primární lokalitu, Kontrola požadavků neověřuje, jestli je port, který zadáte pro SSB, otevřený v primární lokalitě.  

#### <a name="known-issues-with-azure-services"></a>Známé problémy se službami Azure

Po rozšíření lokality je třeba překonfigurovat následující služby Azure s Configuration Manager:

- [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  
- [Microsoft Store pro firmy](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Brána pro správu cloudu](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

Ve verzi 1806 a novější si obnovte Azure Active Directory tajný klíč tenanta. Další informace najdete v tématu [obnovení tajného klíče](../configure/azure-services-wizard.md#bkmk_renew).

Případně můžete odebrat a znovu vytvořit připojení k této službě:

1. V konzole Configuration Manager odstraňte službu Azure z uzlu **služby Azure** .  

2. V Azure Portal odstraňte klienta, který je přidružený ke službě, z uzlu Azure Active Directory tenantů. Tato akce také odstraní webovou aplikaci Azure AD, která je přidružená ke službě.  

3. Překonfigurujte připojení ke službě Azure pro použití s Configuration Manager.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a>Sekundární lokality

Níže jsou uvedené předpoklady pro instalaci sekundárních lokalit:  

- Musí být nainstalovány potřebné role, funkce a součásti systému Windows Server. Další informace najdete v tématu [požadavky na systém lokality](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq) .  

- Správce, který nakonfiguruje instalaci sekundární lokality v konzole Configuration Manager, musí mít oprávnění pro správu na základě rolí, která odpovídají roli zabezpečení **správce infrastruktury** nebo **správce s úplnými oprávněními**.  

- Účet počítače nadřazené primární lokality musí být **správce** na serveru sekundární lokality.  

- Když sekundární lokalita používá dřív nainstalovanou instanci SQL Server k hostování databáze sekundární lokality:  

    - Účet počítače nadřazené primární lokality musí mít oprávnění **sysadmin** v instanci SQL Server na serveru sekundární lokality.  

    - **Místní systémový** účet počítače serveru sekundární lokality musí mít oprávnění **sysadmin** v instanci SQL Server na serveru sekundární lokality.  

        > [!IMPORTANT]  
        > Po dokončení instalace Configuration Manager musí oba účty zachovat oprávnění sysadmin pro SQL Server. Neodstraňujte z těchto účtů práva sysadmin.  

- Server sekundární lokality musí splňovat všechny požadované konfigurace. Tyto konfigurace zahrnují SQL Server a výchozí role systému lokality bodu správy a distribučního bodu.  


## <a name="next-steps"></a>Další kroky

Po potvrzení požadovaných součástí jste připraveni spustit instalaci. Další informace najdete v tématu [instalace Configuration Managerch lokalit pomocí Průvodce instalací](use-the-setup-wizard-to-install-sites.md)nástroje.
