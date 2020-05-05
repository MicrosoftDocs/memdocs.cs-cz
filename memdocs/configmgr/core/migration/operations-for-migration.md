---
title: Operace migrace
titleSuffix: Configuration Manager
description: Vytvořte a spusťte úlohy pro migraci dat a klientů do Configuration Manager aktuální větev.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720916"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Operace migrace do Configuration Manager aktuální větve

*Platí pro: Configuration Manager (Current Branch)*

Pro migraci v Configuration Manager můžete migrovat data a klienty po úspěšném shromáždění dat ze zdrojové lokality v podporované zdrojové hierarchii. Pomocí informací v následujících částech vytvoříte a spustíte úlohy migrace pro migraci dat a klientů a potom dokončíte proces migrace.  

-   [Vytvoření a úprava úloh migrace](#Create_Edit_migration_Jobs)  

-   [Spuštění úloh migrace](#Run_Migration_Jobs)  

-   [Upgrade nebo změna přiřazení sdíleného distribučního bodu](#BKMK_ProcUpgrdSS)  

-   [Monitorování migrace v pracovním prostoru Migrace](#Monitor_MIgration)  

-   [Migrace klientů](#BKMK_MigrateClients)  

-   [Dokončit migraci](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a>Vytvoření a úprava úloh migrace  
 Pomocí následujících postupů můžete vytvořit úlohy migrace dat, upravit seznam vyloučení pro úlohy migrace na základě kolekcí, nastavit sdílené distribuční body a upravit plány úloh migrace.  

> [!NOTE]  
>  Následující postup pro vytvoření úlohy migrace, která migruje podle kolekcí, se vztahuje pouze na zdrojové hierarchie, na kterých běží podporovaná verze Configuration Manager 2007. Typ úlohy migrace na základě kolekce není k dispozici, když migrujete z nástroje System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větve.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Vytvoření úlohy migrace za účelem migrace podle kolekcí  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **úlohy migrace**.  

3.  Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit úlohu migrace**.  

4.  Na stránce **Obecné** v Průvodci vytvořením úlohy migrace nastavte následující možnosti a pak zvolte **OK**:  

    -   Zadejte název úlohy migrace.  

    -   V rozevíracím seznamu **Typ úlohy** vyberte možnost **Migrace kolekce**.  

5.  Na stránce **Vybrat kolekce** nastavte následující nastavení a klikněte na tlačítko **Další**:  

    -   Vyberte kolekce, jejichž migraci chcete provést.  

    -   Chcete-li migrovat pouze kolekce, nikoli objekty, které jsou k těmto kolekcím přidruženy, zrušte výběr položky **migrovat objekty přidružené k zadaným kolekcím**. Pokud zrušíte kontrolu této možnosti, nejsou v této úloze migrovány žádné přidružené objekty a můžete přeskočit kroky 6 a 7.  

6.  Na stránce **Vybrat objekty** zrušte zaškrtnutí všech typů objektů nebo konkrétních dostupných objektů, které nechcete migrovat. Ve výchozím nastavení jsou vybrány všechny přidružené typy objektů a dostupné objekty. Zvolte **Další**.  

7.  Na stránce **vlastnictví obsahu** přiřaďte vlastnictví obsahu z každé zdrojové lokality v seznamu k lokalitě v cílové hierarchii a pak zvolte možnost **Další**.  

8.  Na stránce **obor zabezpečení** vyberte jeden nebo více administrativních oborů zabezpečení založených na rolích, které chcete přiřadit k objektům, které chcete migrovat v této úloze migrace, a poté klikněte na tlačítko **Další**.  

9. Na stránce **omezení kolekce** nastavte kolekci z cílové hierarchie, abyste omezili rozsah jednotlivých uvedených kolekcí, a pak zvolte **Další**. Pokud nejsou uvedeny žádné kolekce, klikněte na tlačítko **Další**.  

10. Na stránce **Nahrazení kódu webového serveru** přiřaďte kód lokality z cílové hierarchie, abyste nahradili kód lokality Configuration Manager 2007 pro každou uvedenou kolekci a pak zvolte možnost **Další**. Pokud nejsou uvedeny žádné kolekce, klikněte na tlačítko **Další**.  

11. Na stránce **zkontrolovat informace** vyberte možnost **Uložit do souboru** a uložte zobrazené informace pro pozdější prohlížení. Až budete připraveni pokračovat, klikněte na tlačítko **Další**.  

12. Na stránce **Nastavení** nastavte, kdy se má úloha migrace spustit, zvolte všechna další nastavení, která pro tuto úlohu migrace potřebujete, a pak zvolte **Další**.  

13. Potvrďte nastavení a dokončete průvodce.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Vytvoření úlohy migrace za účelem migrace podle objektů  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **úlohy migrace**.  

3.  Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit úlohu migrace**.  

4.  Na stránce **Obecné** v Průvodci vytvořením úlohy migrace nastavte následující možnosti a pak klikněte na tlačítko **Další**:  

    -   Zadejte název úlohy migrace.  

    -   V rozevíracím seznamu **Typ úlohy** vyberte možnost **Migrace objektu**.  

5.  Na stránce **Vybrat objekty** vyberte typy objektů, které chcete migrovat. Ve výchozím nastavení jsou vybrány všechny dostupné objekty pro každý vybraný typ objektů.  

6.  Na stránce **vlastnictví obsahu** přiřaďte vlastnictví obsahu z každé zdrojové lokality v seznamu k lokalitě v cílové hierarchii a pak zvolte možnost **Další**. Pokud nejsou uvedeny žádné zdrojové lokality, klikněte na tlačítko **Další**.  

7.  Na stránce **obor zabezpečení** vyberte jeden nebo více administrativních oborů zabezpečení založených na rolích, které chcete přiřadit k objektům v této úloze migrace, a pak zvolte možnost **Další**.  

8.  Na stránce **zkontrolovat informace** vyberte možnost **Uložit do souboru** a uložte zobrazené informace pro pozdější prohlížení. Až budete připraveni pokračovat, klikněte na tlačítko **Další**.  

9. Na stránce **Nastavení** nastavte čas, kdy se úloha migrace spustí, a vyberte jakákoli další nastavení, která potřebujete pro tuto úlohu migrace. Pak klikněte na tlačítko **Další**.  

10. Potvrďte nastavení a dokončete průvodce.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Vytvoření úlohy migrace za účelem migrace změněných objektů  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **úlohy migrace**.  

3.  Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit úlohu migrace**.  

4.  Na stránce **Obecné** v Průvodci vytvořením úlohy migrace nastavte následující nastavení a klikněte na tlačítko **Další**:  

    -   Zadejte název úlohy migrace.  

    -   V rozevíracím seznamu **typ úlohy** vyberte možnost **objekty upravené po migraci**.  

5.  Na stránce **Vybrat objekty** vyberte typy objektů, které chcete migrovat. Ve výchozím nastavení jsou vybrány všechny dostupné objekty pro každý vybraný typ objektů.  

6.  Na stránce **vlastnictví obsahu** přiřaďte vlastnictví obsahu z každé zdrojové lokality v seznamu k lokalitě v cílové hierarchii a pak zvolte možnost **Další**. Pokud nejsou uvedeny žádné zdrojové lokality, klikněte na tlačítko **Další**.  

7.  Na stránce **obor zabezpečení** vyberte jeden nebo více administrativních oborů zabezpečení založených na rolích, které chcete přiřadit k objektům v této úloze migrace, a pak zvolte možnost **Další**.  

8.  Na stránce **zkontrolovat informace** vyberte možnost **Uložit do souboru** a uložte zobrazené informace pro pozdější prohlížení. Až budete připraveni pokračovat, klikněte na tlačítko **Další**.  

9. Na stránce **Nastavení** nastavte čas, kdy se úloha migrace spustí, a pro tuto úlohu migrace vyberte všechna další nastavení, která požadujete. Na rozdíl od ostatních typů úloh migrace musí tato úloha migrace přepsat dříve migrované objekty v databázi Configuration Manager. Zvolte **Další**.  

10. Potvrďte nastavení a potom průvodce dokončete.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a>Úprava seznamu vyloučení pro migraci  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** vyberte možnost **migrace** , abyste získali přístup k seznamu vyloučení. Dále lze do seznamu vyloučení získat přístup z uzlu **Zdrojová hierarchie** nebo **Úlohy migrace** .  

3.  Na kartě **Domů** ve skupině **migrace** vyberte možnost **Upravit seznam vyloučení**.  

4.  V dialogovém okně **Upravit seznam vyloučení** vyberte vyloučený objekt, který chcete odebrat ze seznamu vyloučení, a pak zvolte možnost **Odebrat**.  

5.  Kliknutím na **tlačítko OK** uložte změny a dokončete úpravu. Chcete-li zrušit aktuální změny a obnovit všechny odebrané objekty, klikněte na **tlačítko Storno**a pak zvolte možnost **ne**. Odstranění objektů se tím zruší a dialogové okno **Úpravy seznamu vyloučení** se zavře.  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Sdílení distribučních bodů ze zdrojové hierarchie  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**, zvolte možnost **zdrojová hierarchie**a poté vyberte zdrojovou lokalitu, kterou chcete nastavit.  

3.  Na kartě **Domů** ve skupině **zdrojová lokalita** klikněte na možnost **Konfigurovat**.  

4.  V dialogovém okně **pověření zdrojového webového serveru** vyberte možnost **Povolit sdílení distribučního bodu pro server zdrojové lokality**a klikněte na **tlačítko OK**.  

5.  Po dokončení shromažďování dat klikněte na tlačítko **Zavřít**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Změna plánu úlohy migrace  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **úlohy migrace**.  

3.  Vyberte úlohu migrace, kterou chcete změnit. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

4.  Ve vlastnostech úlohy migrace vyberte kartu **Nastavení** , změňte čas spuštění úlohy migrace a klikněte na **tlačítko OK**.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Spouštění úloh migrace  
 Následující postup slouží ke spuštění úlohy migrace, která dosud nebyla zahájena.  


1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **úlohy migrace**.  

3.  Vyberte úlohu migrace, kterou chcete spustit. Na kartě **Domů** ve skupině **úloha migrace** vyberte možnost **Spustit**.  

4.  Kliknutím na **Ano** spusťte úlohu migrace.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a>Upgrade nebo změna přiřazení sdíleného distribučního bodu  
 Můžete upgradovat podporovaný distribuční bod sdílený ze zdrojové lokality Configuration Manager 2007 (nebo změnit přiřazení podporovaného distribučního bodu sdíleného ze Configuration Manager zdrojové lokality) tak, aby byl distribučním bodem v cílové hierarchii.  

> [!IMPORTANT]  
>  Před upgradem distribučního bodu větve Configuration Manager 2007 je nutné odinstalovat klientský software Configuration Manager 2007 z počítače distribučního bodu větve. Pokud se klientský software Configuration Manager 2007 nainstaluje při pokusu o upgrade distribučního bodu, upgrade se nezdaří a obsah, který byl dříve nasazen do distribučního bodu větve, bude z počítače odebrán.  

> [!CAUTION]  
>  Když upgradujete nebo znovu přiřadíte sdílený distribuční bod, role systému lokality distribučního bodu a počítač systému lokality budou odebrány ze zdrojové lokality a přidány jako distribuční bod do lokality v cílové hierarchii, kterou vyberete.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Upgrade nebo změna přiřazení sdíleného distribučního bodu  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **zdrojová hierarchie**.  

3.  Vyberte lokalitu, která je vlastníkem distribučního bodu, který chcete upgradovat, klikněte na kartu **sdílené distribuční body** a vyberte opravňující distribuční bod, který chcete upgradovat nebo znovu přiřadit.  

4.  Na kartě **distribuční bod** ve skupině **distribuční bod** klikněte na možnost **znovu přiřadit**.  

5.  V průvodci změnou přiřazení sdíleného distribučního bodu zadejte nastavení, jako je například instalace nového distribučního bodu pro cílovou hierarchii, a to následujícím způsobem:  

    -   Na stránce **konverze obsahu** si přečtěte pokyny pro místo potřebné k převedení stávajícího obsahu. Pak na stránce **Nastavení jednotky** v průvodci zkontrolujte, že je na jednotce vybraného počítače distribučního bodu požadovaná velikost volného místa na disku.  

6.  Potvrďte nastavení a potom průvodce dokončete.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a>Monitorování aktivity migrace v pracovním prostoru migrace  
 K monitorování migrace použijte konzolu Configuration Manager.  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **úlohy migrace**.  

3.  Vyberte úlohu migrace, kterou chcete monitorovat.  

4.  Stav vybrané úlohy migrace a další podrobnosti jsou zobrazeny na kartách **Shrnutí** a **Objekty v úloze**.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrace klientů  
 Po migraci dat klientů mezi hierarchiemi, ale ještě před dokončením migrace, naplánujte migraci klientů do cílové hierarchie. Migrace klientů mezi hierarchiemi zahrnuje odinstalaci klientského softwaru Configuration Manager z počítačů přiřazených ke zdrojové hierarchii a následnou instalaci Configuration Manager klientského softwaru z cílové hierarchie. Při instalaci klienta z cílové hierarchie jej rovněž přiřadíte k primární lokalitě v dané hierarchii. Další informace o migraci klientů najdete v tématu [Plánování strategie migrace klientů](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a>Dokončit migraci  
 Tento postup slouží k dokončení migrace ze zdrojové hierarchie.  

1.  V konzole Configuration Manager vyberte možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **migrace**a pak zvolte možnost **zdrojová hierarchie**.  

3.  Pro zdrojovou hierarchii Configuration Manager 2007 vyberte zdrojovou lokalitu, která se nachází na nejnižší úrovni zdrojové hierarchie. U služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větve vyberte dostupnou zdrojovou lokalitu.  

4.  Na kartě **Domů** ve skupině **vyčistit** vyberte **Zastavit shromažďování dat**.  

5.  Kliknutím na **Ano** akci potvrďte.  

6.  Pro zdrojovou hierarchii Configuration Manager 2007 zopakujte kroky 3, 4 a 5, než budete pokračovat k dalšímu kroku. Projděte si tyto kroky v každé lokalitě v hierarchii, od dolního okraje hierarchie po horní. Pro System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojovou hierarchii větve přejděte k dalšímu kroku.  

7.  Na kartě **Domů** ve skupině **vyčistit** vyberte možnost **vyčistit data migrace**.  

8.  V dialogovém okně **Vyčištění dat migrace** vyberte v rozevíracím seznamu **zdrojová hierarchie** kód lokality a server lokality nejvyšší úrovně ve zdrojové hierarchii a pak zvolte **OK**.  

9. Kliknutím na **tlačítko Ano** dokončete proces migrace pro zdrojovou hierarchii.  
