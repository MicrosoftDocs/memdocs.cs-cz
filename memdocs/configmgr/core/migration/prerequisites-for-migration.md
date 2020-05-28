---
title: Předpoklady migrace
titleSuffix: Configuration Manager
description: Pochopte podporované verze Configuration Manager, podporované jazyky zdrojové lokality a požadované konfigurace pro migraci.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36e62ea5198824a6b3466853cdbcfc3057d1829e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428728"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Předpoklady pro migraci v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li provést migraci z podporované zdrojové hierarchie, musíte mít přístup ke všem příslušným Configuration Manager zdrojové lokalitě a oprávnění v rámci cílové lokality Configuration Manager ke konfiguraci a spuštění operací migrace.  

 Informace v následujících částech vám pomohou pochopit verze Configuration Manager, které jsou podporovány pro migraci, a požadované konfigurace.  

-   [Podporované verze nástroje Configuration Manager při migraci](#BKMK_SupportedMigrationVersions)  

-   [Jazyky zdrojové lokality podporované při migraci](#BKMK_SorceSiteLanguage)  

-   [Požadované konfigurace pro migraci](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a>Podporované verze Configuration Manager pro migraci  
 Můžete migrovat data ze zdrojové hierarchie, která používá některou z následujících verzí Configuration Manager:  

- Configuration Manager 2007 SP2 (pro účely migrace není potřeba Configuration Manager 2007 R2 nebo R3 ve zdrojové lokalitě. Pokud však zdrojová lokalita používá verzi SP2, jsou lokality s nainstalovaným doplňkem R2 nebo R3 podporovány pro migraci na Configuration Manager aktuální větev).  

- System Center 2012 Configuration Manager SP2 nebo System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Kromě migrace můžete použít místní upgrade lokalit, na kterých je spuštěný System Center 2012 Configuration Manager, a Configuration Manager aktuální větev.  

- Hierarchie Configuration Manager stejné nebo nižší verze Configuration Manager.  

  Pokud máte například cílovou hierarchii, která spouští Configuration Manager aktuální větvi 1606, mohli byste pomocí migrace zkopírovat data ze zdrojové hierarchie, ve které běží verze 1606 nebo 1602. Nemůžete ale migrovat data ze zdrojové hierarchie, která spouští 1610.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a>Jazyky zdrojové lokality, které jsou podporovány pro migraci  
 Při migraci dat mezi Configuration Manager hierarchiemi jsou data uložena do cílové hierarchie nástroje v jazykově neutrálním formátu pro Configuration Manager. Vzhledem k tomu, že Configuration Manager 2007 neukládá data v jazykově neutrálním formátu, proces migrace musí při migraci z Configuration Manager 2007 převést objekty do tohoto formátu. Proto jsou pro migraci podporovány pouze zdrojové lokality Configuration Manager 2007, které jsou nainstalovány s následujícími jazyky:  

-   Angličtina  

-   Francouzština  

-   Němčina  

-   Japonština  

-   Korejština  

-   Ruština  

-   Zjednodušená čínština  

-   Tradiční čínština  

Při migraci dat z nástroje System Center 2012 Configuration Manager nebo Configuration Manager aktuální hierarchie větví neexistují žádná omezení jazyka zdrojové lokality. Objekty jsou v databázi zdrojové lokality již uloženy v jazykově neutrálním formátu.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a>Požadované konfigurace pro migraci  
Pro použití migrace a operací migrace se vyžadují následující konfigurace:  

- **Konfigurace, spouštění a monitorování migrace v konzole Configuration Manager:**  

   V cílové lokalitě musí mít váš účet přiřazenou roli zabezpečení správy na základě rolí **Správce infrastruktury**. Tato role zabezpečení uděluje oprávnění ke správě všech operací migrace, jako je vytváření úloh migrace, čištění, monitorování a akce sdílení a upgradu distribučních bodů.  

- **Shromažďování dat:**  

   Aby bylo možno v cílové lokalitě shromažďovat data, musíte pro každou zdrojovou lokalitu konfigurovat následující dva přístupové účty:  

  -   **Účet zdrojové lokality** : Tento účet se používá pro přístup k poskytovateli serveru SMS zdrojové lokality.  

      -   Pro zdrojovou lokalitu Configuration Manager 2007 SP2 vyžaduje tento účet oprávnění **číst** ke všem objektům zdrojové lokality.  

      -   Pro System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojovou lokalitu větve vyžaduje tento účet oprávnění **číst** ke všem objektům zdrojové lokality. Toto oprávnění účtu udělíte pomocí správy založené na rolích. Informace o tom, jak používat správu na základě rolí, najdete v tématu [základy správy na základě rolí pro Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Účet databáze zdrojové lokality:** Tento účet se používá pro přístup k databázi SQL Serveru zdrojové lokality. Vyžaduje pro databázi zdrojové lokality oprávnění **Připojit**, **Spustit**a **Vybrat** .  

  Tyto účty můžete konfigurovat při nastavování nové zdrojové hierarchie, při shromažďování dat pro další zdrojovou lokalitu nebo při opětovném konfigurování pověření pro zdrojovou lokalitu. Lze použít doménové uživatelské účty nebo účty počítače lokality nejvyšší úrovně cílové hierarchie.  

  > [!IMPORTANT]  
  >  Pokud používáte účet Configuration Manager počítače pro některý z přístupových účtů, zajistěte, aby tento účet byl členem skupiny zabezpečení **Distributed COM Users** v doméně, ve které se nachází zdrojová lokalita.  

  Při shromažďování dat se používají následující síťové protokoly a porty:  

  - NetBIOS/SMB-445 (TCP)  

  - RPC (WMI)-135 (TCP & UDP)  

  - Dynamické RPC. Dynamické porty používají rozsah čísel portů, který je definovaný verzí operačního systému. Tyto porty se označují také jako dočasné porty. Další informace o výchozích rozsazích portů naleznete v části [Přehled služeb a požadavky na síťové porty pro systém Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).<!-- SCCMDocs#1053 -->

  - SQL Server – porty protokolu TCP používané databázemi zdrojové a cílové lokality.  

- **Migrace aktualizací softwaru:**  

   Před migrací aktualizací softwaru musíte v cílové hierarchii konfigurovat bod aktualizace softwaru. Další informace najdete v části [Plánování migrace aktualizací softwaru](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Sdílení distribučních bodů:**  

   Pro úspěšné sdílení distribučních bodů ze zdrojové lokality musí alespoň jedna primární lokalita nebo lokalita centrální správy v cílové hierarchii používat stejná čísla portů pro požadavky klientů jako zdrojová lokalita. Informace o portech požadavků klientů najdete v tématu [Postup konfigurace portů pro komunikaci klientů](../../core/clients/deploy/configure-client-communication-ports.md) .  

   U každé lokality jsou sdíleny pouze distribuční body instalované na systémových serverech konfigurovaných s názvy FQDN.  

   Kromě toho musí mít **Účet zdrojové** lokality (který přistupuje k poskytovateli služby SMS pro zdrojový webový server) oprávnění **Upravit** pro objekt **lokalita** ve zdrojové lokalitě, aby bylo možné sdílet distribuční bod ze služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové lokality větve. Toto oprávnění účtu udělíte pomocí správy založené na rolích. Informace o tom, jak používat správu na základě rolí, najdete v tématu [základy správy na základě rolí pro Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Upgrade nebo změna přiřazení distribučních bodů:**  

   **Účet pro přístup ke zdrojové lokalitě** konfigurovaný pro shromažďování dat od poskytovatele serveru SMS zdrojové lokality musí mít následující oprávnění:  

  - K upgradu distribučního bodu Configuration Manager 2007 vyžaduje účet oprávnění **číst**, **Spustit**a **Odstranit** ke třídě **lokalita** na serveru lokality konfigurace Manager2007 pro úspěšné odebrání distribučního bodu ze zdrojové lokality Manager2007 konfigurace.  

  - Chcete-li změnit přiřazení distribučního bodu aktuální větve nástroje System Center 2012 Configuration Manager nebo Configuration Manager, musí mít účet oprávnění **Upravit** pro objekt **lokalita** ve zdrojové lokalitě. Toto oprávnění účtu udělíte pomocí správy založené na rolích. Informace o tom, jak používat správu na základě rolí, najdete v tématu [základy správy na základě rolí pro Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    Pro úspěšný upgrade nebo změnu přiřazení distribučních bodů v nové hierarchii je třeba, aby porty konfigurované pro požadavky klientů v lokalitě spravující distribuční bod ve zdrojové hierarchii odpovídaly portům konfigurovaným pro požadavky klientů v cílové lokalitě, která bude distribuční bod spravovat. Informace o portech požadavků klienta najdete v tématu [Konfigurace portů pro komunikaci klientů](../../core/clients/deploy/configure-client-communication-ports.md).  
