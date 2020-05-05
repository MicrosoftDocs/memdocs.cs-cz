---
title: Hierarchie zdrojů migrace
titleSuffix: Configuration Manager
description: Nakonfigurujte zdrojovou hierarchii a zdrojové lokality, abyste mohli migrovat data do svého Configuration Managerho prostředí aktuální pobočky.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718921"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Konfigurace zdrojových hierarchií a zdrojových lokalit pro migraci na Configuration Manager aktuální větev

*Platí pro: Configuration Manager (Current Branch)*

Pokud chcete povolit migraci dat do vašeho Configuration Manager aktuálního prostředí pobočky, musíte nakonfigurovat podporovanou zdrojovou hierarchii Configuration Manager a jednu nebo víc zdrojových lokalit v této hierarchii, které obsahují data, která chcete migrovat.  

> [!NOTE]  
>  Operace migrace se spouští v lokalitě nejvyšší úrovně v cílové hierarchii. Pokud provádíte konfiguraci migrace při použití konzoly Configuration Manager, která je připojená k primární podřízené lokalitě, je nutné, aby se konfigurace mohla replikovat do lokality centrální správy, spustit a následně replikovat stav zpět do primární lokality, ke které jste se připojili.  

 Informace a postupy v následujících částech použijte k určení zdrojové hierarchie a přidání dalších zdrojových lokalit. Po dokončení těchto postupů můžete vytvořit úlohy migrace a začít migrovat data ze zdrojové hierarchie do cílové hierarchie.  

-   [Zadat zdrojovou hierarchii pro migraci](#BKBM_ConfigSrcHierarchy)  

-   [Identifikace dalších zdrojových lokalit zdrojové hierarchie](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a>Zadat zdrojovou hierarchii pro migraci  
 K migraci dat do cílové hierarchie je nutné zadat podporovanou zdrojovou hierarchii obsahující data, která chcete migrovat. Ve výchozím nastavení se lokalita nejvyšší úrovně v této hierarchii stala zdrojovou lokalitou zdrojové hierarchie. Pokud migrujete z hierarchie Configuration Manager 2007, pak můžete nastavit další zdrojové lokality pro migraci po shromáždění dat z počáteční zdrojové lokality. Pokud migrujete z verze System Center 2012 Configuration Manager nebo Configuration Manager aktuální hierarchie větví, není nutné nastavovat další zdrojové lokality pro migraci dat ze zdrojové hierarchie. Je tomu tak proto, že tyto verze Configuration Manager používají sdílenou databázi, která je k dispozici v lokalitě nejvyšší úrovně ve zdrojové hierarchii. Sdílená databáze obsahuje všechny informace, které můžete migrovat.  

 Pomocí následujících postupů určete zdrojovou hierarchii pro migraci a Identifikujte další zdrojové lokality v hierarchii Configuration Manager 2007.  

 Spusťte tento postup s konzolou Configuration Manager připojenou k cílové hierarchii:  

### <a name="to-configure-a-source-hierarchy"></a>Konfigurace zdrojové hierarchie   

1. V konzole Configuration Manager klikněte na možnost **Správa**.  

2. V pracovním prostoru **Správa** rozbalte možnost **Migrace**a klikněte na položku **Zdrojová hierarchie**.  

3. Na kartě **Domů** ve skupině **migrace** klikněte na možnost **zadat zdrojovou hierarchii**.  

4. V dialogovém okně **zadat zdrojovou hierarchii** pro položku **zdrojová hierarchie**vyberte možnost **nová zdrojová hierarchie**.  

5. U **Configuration Manager serveru lokality na nejvyšší úrovni**zadejte název nebo IP adresu lokality nejvyšší úrovně v podporované zdrojové hierarchii.  

6. Zadejte účty pro přístup ke zdrojové lokalitě s následujícími oprávněními:  

   - Účet zdrojové lokality: oprávnění **číst** pro poskytovatele služby SMS zadané lokality nejvyšší úrovně ve zdrojové hierarchii. Sdílení a upgrade distribučního bodu vyžadují pro lokalitu ve zdrojové hierarchii oprávnění **Upravit** a **Odstranit** .

   - Účet databáze zdrojové lokality: oprávnění **číst** a **spustit** pro databázi SQL Server pro zadanou lokalitu nejvyšší úrovně ve zdrojové hierarchii.  

     Pokud zadáte použití účtu počítače, používá Configuration Manager účet počítače lokality nejvyšší úrovně v cílové hierarchii. Pro tuto možnost zajistěte, aby byl tento účet členem skupiny zabezpečení **Distributed COM Users** v doméně, ve které se nachází lokalita nejvyšší úrovně ve zdrojové hierarchii.  

7. Chcete-li sdílet distribuční body mezi zdrojovými a cílovými hierarchiemi, zaškrtněte políčko **Povolit sdílení distribučního bodu pro server zdrojové lokality** . Pokud v tuto chvíli nepovolíte sdílení distribučních bodů, můžete tak učinit úpravou přihlašovacích údajů zdrojové lokality po dokončení shromažďování dat.  

8. Konfiguraci uložíte kliknutím na **OK** . Tím se otevře dialogové okno **stav shromažďování dat** a automaticky se spustí shromažďování dat.  

9. Po dokončení shromažďování dat kliknutím na tlačítko **Zavřít** zavřete dialogové okno **stav shromažďování dat** a dokončete konfiguraci.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a>Identifikace dalších zdrojových lokalit zdrojové hierarchie  
 Když konfigurujete podporovanou zdrojovou hierarchii, lokalita nejvyšší úrovně v této hierarchii se automaticky nakonfiguruje jako zdrojová lokalita a data se z této lokality automaticky shromažďují. Další akce, kterou provedete, závisí na verzi Configuration Manager, kterou spouští zdrojová hierarchie:  

-   Pro zdrojovou hierarchii Configuration Manager 2007 můžete zahájit migraci z této počáteční zdrojové lokality nebo nastavit další zdrojové lokality ze zdrojové hierarchie po dokončení shromažďování dat pro počáteční zdrojovou lokalitu. Chcete-li migrovat data, která jsou k dispozici pouze z podřízené lokality, nastavte další zdrojové lokality pro hierarchii Configuration Manager 2007. Můžete například nakonfigurovat další zdrojové lokality pro shromažďování dat o obsahu, který chcete migrovat, když je vytvořen v podřízené lokalitě ve zdrojové hierarchii a není k dispozici v nejvyšší lokalitě zdrojové hierarchie.  

-   Pro System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojovou hierarchii větve nemusíte konfigurovat další zdrojové lokality. Je tomu tak proto, že tyto verze Configuration Manager používají sdílenou databázi, která je k dispozici v lokalitě nejvyšší úrovně ve zdrojové hierarchii. Sdílená databáze obsahuje všechny informace, které můžete migrovat ze všech lokalit v této zdrojové hierarchii. Tím se data, která můžete migrovat, zpřístupní z lokality nejvyšší úrovně ve zdrojové hierarchii.  

Když nakonfigurujete další zdrojové lokality pro zdrojovou hierarchii Configuration Manager 2007, je nutné nakonfigurovat další zdrojové lokality z horní části zdrojové hierarchie na nejnižší. Nadřazený web musíte nakonfigurovat jako zdrojovou lokalitu před tím, než nakonfigurujete všechny jeho podřízené lokality jako zdrojové lokality.  

Pomocí následujícího postupu můžete nakonfigurovat další zdrojové lokality pro Configuration Manager 2007 zdrojové hierarchie:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Identifikace dalších zdrojových lokalit ve zdrojové hierarchii 

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte možnost **Migrace**a klikněte na položku **Zdrojová hierarchie**.  

3.  Vyberte lokalitu, kterou chcete nakonfigurovat jako zdrojovou lokalitu.  

4.  Na kartě **Domů** ve skupině **Zdrojová lokalita** klikněte na možnost **Konfigurovat**.  

5.  V dialogovém okně **pověření zdrojové lokality** zadejte pro účty pro přístup ke zdrojové lokalitě účty, které mají následující oprávnění:  

    -   Účet zdrojové lokality: oprávnění **číst** pro poskytovatele služby SMS zadané lokality nejvyšší úrovně ve zdrojové hierarchii. Sdílení a upgrade distribučního bodu vyžadují pro lokalitu ve zdrojové hierarchii oprávnění **Upravit** a **Odstranit** .  

    -   Účet databáze zdrojové lokality: oprávnění **číst** a **spustit** pro databázi SQL Server pro zadanou lokalitu nejvyšší úrovně ve zdrojové hierarchii.  

    Pokud zadáte použití účtu počítače, používá Configuration Manager účet počítače lokality nejvyšší úrovně v cílové hierarchii. Pro tuto možnost zajistěte, aby byl tento účet členem skupiny zabezpečení **Distributed COM Users** v doméně, ve které se nachází lokalita nejvyšší úrovně ve zdrojové hierarchii.  

6.  Chcete-li sdílet distribuční body mezi zdrojovými a cílovými hierarchiemi, zaškrtněte políčko **Povolit sdílení distribučního bodu pro server zdrojové lokality** . Pokud v tuto chvíli nepovolíte sdílení distribučních bodů, můžete tak učinit úpravou přihlašovacích údajů pro zdrojovou lokalitu po dokončení shromažďování dat.  

7. Konfiguraci uložíte kliknutím na **OK** . Tím se otevře dialogové okno **stav shromažďování dat** a automaticky se spustí shromažďování dat.  

8.  Po dokončení shromažďování dat kliknutím na tlačítko **Zavřít** dokončete konfiguraci.  
