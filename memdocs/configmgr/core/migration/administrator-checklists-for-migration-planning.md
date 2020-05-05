---
title: Kontrolní seznamy migrace
titleSuffix: Configuration Manager
description: Pomocí kontrolních seznamů správce vám pomůžou naplánovat strategii migrace Configuration Manager aktuální větve.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718942"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Kontrolní seznamy správce pro plánování migrace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Následující kontrolní seznamy správce vám pomůžou naplánovat strategii migrace na Configuration Manager aktuální větev.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a>Kontrolní seznam správce pro plánování migrace  
 Při plánování kroků před migrací použijte následující kontrolní seznam.  

-   **Zhodnoťte současné prostředí:**  

     Identifikujte stávající podnikové požadavky, které zdrojová hierarchie splňuje, a vytvořte plány zajišťující jejich splnění v cílové hierarchii.  

-   **Zkontrolujte funkčnost a změny, které jsou k dispozici ve verzi Configuration Manager, kterou používáte, a použijte tyto informace, které vám pomůžou při návrhu cílové hierarchie:**  

    Další informace najdete v tématu [základy Configuration Manager](../../core/understand/fundamentals.md) a [novinky](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Určete model zabezpečení správy, který se má použít pro správu na základě rolí:**  

    Další informace najdete v tématu [základy správy na základě rolí pro Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Posouzení topologie sítě a služby Active Directory:** Projděte si stávající doménovou strukturu a topologii sítě a zvažte, jak to ovlivňuje návrh hierarchie a úlohy migrace.  

-   **Dokončete návrh cílové hierarchie:**  

    Rozhodněte o umístění lokality centrální správy, primárních lokalit, sekundárních lokalit a možností distribuce obsahu.  

-   **Proveďte mapování hierarchie na počítače, které budete používat pro lokality a servery lokalit v cílové hierarchii:**  

    Identifikujte počítače, které budou používat lokality a systémové servery lokalit v cílové hierarchii, a pak zajistěte, aby měly dostatečnou kapacitu pro splnění stávajících i budoucích provozních požadavků.  

-   **Naplánujte strategii migrace objektů:**  

    Naplánujte použití dostupných úloh migrace k migraci různých objektů včetně hranic lokalit, kolekcí, inzercí a nasazení. Další informace najdete v tématu [typy úloh migrace](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) v tématu [Plánování strategie úloh migrace](../../core/migration/planning-a-migration-job-strategy.md) .  

    Configuration Manager migruje pouze objekty, které vyberete. Všechny objekty, které nejsou migrovány a které jsou požadovány v cílové hierarchii, je nutné znovu vytvořit v cílové hierarchii.  

    Objekty, které lze migrovat, jsou při konfigurování úloh migrace zobrazeny.  

-   **Naplánujte strategii migrace klientů:**  

    Naplánujte migraci klientů s použitím řízeného přístupu, který omezuje potřebnou šířku pásma sítě a požadavky na výkon serveru při migraci klientů do cílové hierarchie. Další informace o plánování strategie migrace klientů najdete v tématu [Plánování strategie migrace klientů](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Vytvořte plán pro inventář a data dodržování předpisů:**  

    Configuration Manager nepodporuje migraci inventáře hardwaru, inventáře softwaru ani dat dodržování předpisů pro aktualizace softwaru nebo klienty v nástroji pro správu požadovaných konfigurací.  

    Klient místo toho po migraci do nové lokality v cílové hierarchii obdrží zásady pro tyto konfigurace a následně odešle příslušné informace do přiřazené lokality. Tato akce vloží do databáze cílové lokality aktuální data inventáře a dodržování předpisů.  

-   **Naplánujte dokončení migrace ze zdrojové hierarchie:**  

    Rozhodněte, kdy proběhne migrace objektů a klientů. Po dokončení migrace můžete naplánovat vyřazení serverů lokalit ve zdrojové hierarchii z provozu.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a>Kontrolní seznam správce pro migraci hierarchie  
Následující kontrolní seznam vám pomůže naplánovat cílovou hierarchii před zahájením migrace.  

-   **Identifikujte počítače používané v cílové hierarchii:**  

    Configuration Manager nepodporuje místní upgrade z infrastruktury Configuration Manager 2007. Místo toho se použije migrace k přesunu dat z Configuration Manager 2007 do Configuration Manager aktuální větve. To vyžaduje, abyste používali souběžné nasazení a nainstalovali Configuration Manager do nových počítačů.  

    Podobně když migrujete z jiné hierarchie Configuration Manager, musíte nainstalovat novou cílovou hierarchii, která je souběžným nasazením do zdrojové hierarchie.  

-   **Vytvořte cílovou hierarchii:**  

    Pro přípravu na migraci nainstalujte a nakonfigurujte Configuration Manager cílovou hierarchii, která zahrnuje primární lokalitu. Příklad:  

    -   Nainstalujte lokalitu centrální správy a poté nainstalujte alespoň jednu podřízenou primární lokalitu.  

    -   Pokud neplánujete použít lokalitu centrální správy, nainstalujte samostatnou primární lokalitu.  

-   **Pokud chcete zajistit migraci informací týkajících se aktualizací softwaru, nakonfigurujte v cílové hierarchii bod aktualizace softwaru a synchronizujte aktualizace softwaru:**  

    Před migrací informací o aktualizaci softwaru ze zdrojové hierarchie musíte v cílové hierarchii nakonfigurovat a synchronizovat aktualizace softwaru.  


-   **Nainstalujte a nakonfigurujte další role systémů lokalit v cílové hierarchii:**  

    Konfigurujte další role systému lokality a systémy lokality, které budete potřebovat.  

-   **Podívejte se na provozní funkčnost v cílové hierarchii:**  

    Zkontrolujte následující:  

    -   Pokud cílová hierarchie obsahuje více lokalit, zkontrolujte funkčnost replikace databáze mezi lokalitami. Replikace databáze se nevztahuje na samostatné primární lokality.  

    -   Ověřte funkčnost všech instalovaných rolí systému lokality.  

    -   Ověřte, že klienti Configuration Manager, které nainstalujete do cílové hierarchie, mohou úspěšně komunikovat s přiřazenou lokalitou.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a>Kontrolní seznam správce pro migraci  
Následující kontrolní seznam použijte při migraci dat ze zdrojové hierarchie do cílové.  

-   **Povolte migraci v cílové hierarchii:**  

    Nakonfigurujte zdrojovou hierarchii tak, že určíte lokalitu nejvyšší úrovně ve zdrojové hierarchii. Další informace o určení zdrojové lokality najdete v tématu [Plánování strategie zdrojové hierarchie](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Pokud zdrojová hierarchie běží Configuration Manager 2007 SP2, vyberte a nakonfigurujte další lokality ve zdrojové hierarchii:**  

    Pro každou další lokalitu ve zdrojové hierarchii Configuration Manager 2007 SP2, ze které chcete shromažďovat data, musíte nakonfigurovat přihlašovací údaje pro shromažďování dat. Když nakonfigurujete jednotlivé zdrojové lokality, zahájí se proces shromažďování dat hned a pokračuje v průběhu období migrace, dokud nezastavíte shromažďování dat pro tuto lokalitu. Shromažďování dat zajišťuje, že můžete migrovat objekty ze zdrojové hierarchie, které se aktualizují nebo přidají po předchozím procesu shromažďování dat.

    > [!NOTE]  
    >  Pokud zdrojová hierarchie používá verzi System Center 2012 Configuration Manager nebo novější, nemusíte konfigurovat další zdrojové lokality.  

-   **Nakonfigurujte sdílení distribučních bodů:**  

    Distribuční body můžete sdílet mezi dvěma hierarchiemi a zpřístupnit tak obsah migrovaných objektů klientům v cílové hierarchii. Tím se zajistí, že stejný obsah zůstane dostupný pro klienty v obou hierarchiích a že tento obsah můžete spravovat až po zastavení shromažďování dat a dokončení migrace.  

    Informace o sdílených distribučních bodech najdete v tématu [Sdílení distribučních bodů mezi zdrojovou a cílovou hierarchií](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) v tématu [Plánování strategie migrace nasazení obsahu](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Vytvořte a spusťte úlohy migrace pro objekty přiřazené klientům ve zdrojové hierarchii:**  

    Vytvořte úlohy migrace pro migraci objektů mezi hierarchiemi. Požadované konfigurace jednotlivých úloh migrace se mohou lišit v závislosti na migrovaných datech.  

    Při migraci obsahu například musíte bez ohledu na použitou úlohu migrace přiřadit lokalitu v cílové hierarchii, která vlastní správu tohoto obsahu. Přiřazená lokalita bude přistupovat k původnímu umístění zdrojových souborů obsahu a odpovídá za distribuci tohoto obsahu do distribučních bodů v cílové hierarchii.  

    Další informace najdete v tématu [Vytvoření a úprava úloh migrace pro Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) v tématu [operace migrace do Configuration Manager aktuální větve](../../core/migration/operations-for-migration.md).  

-   **Proveďte migraci klientů do cílové hierarchie:**  

    Proces migrace klientů závisí na scénáři migrace:  

    -   Při migraci klientů, které mají verzi klienta, která není shodná s cílovou hierarchií, je nutné upgradovat klientský software. Upgrade vyžaduje odebrání aktuálního klienta Configuration Manager a za ním instalaci nové verze klienta, která odpovídá cílové lokalitě.  

    -   Při migraci klientů, jejichž verze odpovídá verzi cílové hierarchie, není třeba klienty upgradovat ani znovu instalovat. Proběhne pouze změna přiřazení klienta k primární lokalitě v cílové hierarchii.  

    Při migraci klienta do cílové hierarchie je klient přiřazen k datům, které jste do cílové hierarchie migrovali dříve.  

    Další informace najdete v tématu [Plánování strategie migrace klientů](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Upgradujte nebo změňte přiřazení distribučních bodů:**  

    Pokud již nepotřebujete podporovat klienty ve zdrojové hierarchii, můžete upgradovat sdílené distribuční body ze zdrojové lokality nástroje Configuration Manager 2007 nebo změnit přiřazení sdílených distribučních bodů ze služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové lokality větve. Když upgradujete nebo změníte přiřazení distribučního bodu, role systému lokality přejde na primární lokalitu v cílové hierarchii a distribuční bod je odebrán ze zdrojové lokality ve zdrojové hierarchii. Když upgradujete nebo znovu přiřadíte sdílený distribuční bod, obsah zůstane v počítači distribučního bodu a nemusíte ho znovu nasazovat do nových distribučních bodů v cílové hierarchii.  

    Můžete také upgradovat distribuční bod, který je společně umístěn na serveru sekundární lokality Configuration Manager 2007. Tím dojde k odebrání sekundární lokality, takže v cílové hierarchii zůstane pouze distribuční bod.  

    Informace o sdílených distribučních bodech najdete v tématu [Sdílení distribučních bodů mezi zdrojovou a cílovou hierarchií](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) v tématu [Plánování strategie migrace nasazení obsahu](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Dokončete migraci:**  

    Po migraci dat a klientů ze všech lokalit zdrojové hierarchie a upgradu příslušných distribučních bodů můžete migraci dokončit. Migraci dokončíte zastavením shromažďování dat pro každou zdrojovou lokalitu ve zdrojové hierarchii. Následně můžete odebrat nepotřebné informace o migraci a vyřadit infrastrukturu zdrojové hierarchie z provozu. Další informace najdete v tématu [plánování dokončení migrace](../../core/migration/planning-to-complete-migration.md).  
