---
title: Plánování úloh migrace
titleSuffix: Configuration Manager
description: Použijte úlohy migrace ke konfiguraci dat, která chcete migrovat do vašeho Configuration Manager aktuálního prostředí pobočky.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719670"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Plánování strategie úloh migrace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí úloh migrace můžete nakonfigurovat konkrétní data, která chcete migrovat, do Configuration Manager aktuální větve prostředí. Úlohy migrace identifikují objekty, které chcete migrovat, a spouští se v lokalitě nejvyšší úrovně ve vaší cílové hierarchii. Pro každou zdrojovou lokalitu můžete nastavit jednu nebo víc úloh migrace. To vám umožní migrovat všechny objekty najednou nebo omezené podmnožiny dat s každou úlohou.  

 Úlohy migrace můžete vytvořit po Configuration Manager úspěšně shromáždila data z jedné nebo více lokalit ze zdrojové hierarchie. Data je možné migrovat v libovolném pořadí ze zdrojových lokalit, v nichž byla data shromážděna. Se zdrojovou lokalitou Configuration Manager 2007 můžete migrovat data pouze z lokality, ve které byl objekt vytvořen. U zdrojových lokalit, na kterých je spuštěný System Center 2012 Configuration Manager nebo novější, jsou všechna data, která můžete migrovat, dostupná v lokalitě nejvyšší úrovně ve zdrojové hierarchii.  

 Před migrací klientů mezi hierarchiemi se ujistěte, že objekty používané klienty byly migrovány a že jsou dostupné v cílové hierarchii. Když například migrujete ze zdrojové hierarchie Configuration Manager 2007 SP2, můžete mít oznámení o inzerovaném programu pro obsah, který je nasazený do vlastní kolekce, která má klienta. V tomto scénáři doporučujeme před migrací klienta migrovat kolekci, reklamu a související obsah. Tato data nelze přidružit k klientovi v cílové hierarchii, pokud není obsah, kolekce a inzerce migrovány před migrací klienta. Pokud nebude klient přiřazen k datům souvisejícím s dříve použitou reklamou a obsahem, může být klientovi nabídnut obsah k instalaci v cílové hierarchii, což může být zbytečné. Proběhne-li migrace klienta až po migraci dat, bude klient přiřazen k tomuto obsahu a reklamě, a pokud se nejedná o opakovanou reklamu, nebude mu již tento obsah pro migrovanou reklamu nabízen.  

 Některé objekty vyžadují více než jen migraci dat ze zdrojové hierarchie do cílové hierarchie. Například pro úspěšnou migraci aktualizací softwaru pro klienty do cílové hierarchie je nutné nasadit aktivní bod aktualizace softwaru, nakonfigurovat katalog produktů a synchronizovat bod aktualizace softwaru s Windows Server Update Services (WSUS) v cílové hierarchii.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a>Typy úloh migrace  
 Configuration Manager podporuje následující typy úloh migrace. Každý typ úlohy je navržen tak, aby pomohly definovat objekty, které lze do této úlohy zahrnout.  

 **Migrace kolekce** (podporuje se jenom při migraci z Configuration Manager 2007 SP2): migrujte objekty, které souvisí s vybranými kolekcemi. Ve výchozím nastavení zahrnuje migrace kolekce všechny objekty, které jsou přidruženy ke členům kolekce. Při použití úlohy migrace kolekce lze vyloučit určité instance objektů.  

 **Migrace objektu**: migrujte jednotlivé objekty, které vyberete. Vyberete pouze konkrétní data, která chcete migrovat.  

 **Migrace dříve migrovaného objektu**: migrujte objekty, které jste dříve migrovali při aktualizaci ve zdrojové hierarchii po jejich poslední migraci.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a>Objekty, které lze migrovat  
 Ne každý objekt lze migrovat pomocí určitého typu úlohy migrace. V následujícím seznamu jsou uvedeny typy objektů, které je možné migrovat pomocí jednotlivých typů úloh migrace.  

> [!NOTE]  
>  Úlohy migrace kolekcí jsou k dispozici pouze při migraci objektů ze zdrojové hierarchie Configuration Manager 2007 SP2.  

 **Typy úloh, které můžete použít k migraci každého objektu**  

-   **Reklamy** (dostupné k migraci z podporovaných zdrojových lokalit Configuration Manager 2007)  

    -   Migrace kolekce  


-   **katalog Asset Intelligence**  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Požadavky funkce Asset Intelligence na hardware**  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Seznam softwaru funkce Asset Intelligence**  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Hranice**  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Standardní hodnoty konfigurace**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Položky konfigurace**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Časové intervaly pro správu a údržbu**  

    -   Migrace kolekce  


-   **Bitové spouštěcí kopie nasazení operačního systému**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Balíčky ovladačů nasazení operačního systému**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Ovladače nasazení operačního systému**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Bitové kopie nasazení operačního systému**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Balíčky nasazení operačního systému**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Balíčky pro distribuci softwaru**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Pravidla distribuce softwaru**  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Balíčky pro nasazení aktualizace softwaru**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Šablony pro nasazení aktualizace softwaru**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Nasazení aktualizací softwaru**  

    -   Migrace kolekce  


-   **Seznamy aktualizací softwaru**  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Pořadí úloh**  

    -   Migrace kolekce  

    -   Migrace objektu  

    -   Migrace dříve migrovaného objektu  

-   **Balíčky virtuálních aplikací**  

    -   Migrace kolekce  

    -   Migrace objektu  

    > [!IMPORTANT]  
    >  Přestože lze balíček virtuální aplikace migrovat pomocí migrace objektu, balíčky není možné migrovat pomocí úlohy migrace typu **Migrace dříve migrovaného objektu**. Místo toho je nutné odstranit migrovaný balíček virtuální aplikace z cílové lokality a poté vytvořit novou úlohu migrace, v níž bude migrována virtuální aplikace.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a>Obecné plánování všech úloh migrace  
 Pomocí Průvodce vytvořením úlohy migrace vytvořte úlohu migrace pro migraci objektů do cílové hierarchie. Typ úlohy migrace, kterou vytvoříte, závisí na tom, jaké objekty jsou dostupné k migraci. Můžete vytvořit a použít více úloh migrace k migraci dat ze stejné zdrojové lokality nebo z několika zdrojových lokalit. Použití jednoho typu úlohy migrace nebrání použití jiného typu úlohy migrace.  

 Jakmile úloha migrace úspěšně proběhne, je její stav uveden jako **Dokončeno** a úlohu není možné spustit znovu. Lze však vytvořit novou úlohu migrace k migrování některého z objektů, jež byly migrovány původní úlohou, přičemž nová úloha migrace může zahrnovat také další objekty. Když vytvoříte další úlohy migrace, budou dříve migrované objekty zobrazovat stav **migrace**. Tyto objekty lze znovu vybrat, chcete-li je migrovat znovu, ale pokud nebyl objekt aktualizován ve zdrojové hierarchii, není nutné znovu migrovat tyto objekty. Jestliže byl objekt aktualizován ve zdrojové hierarchii poté, co byl původně migrován, je možné tento objekt identifikovat použitím úlohy migrace typu **Objekty upravené po migraci**.  

 Před spuštěním je možné úlohu migrace odstranit. Po dokončení úlohy migrace zůstane však tato funkce viditelná v konzole Configuration Manager a nelze ji odstranit. Každá úloha migrace, která byla dokončena nebo dosud nebyla spuštěna, zůstává viditelná v konzole Configuration Manager, dokud nedokončíte proces migrace a vyčištění dat migrace.  

> [!NOTE]  
>  Po dokončení migrace pomocí akce **Vyčištění dat migrace** můžete stejnou hierarchii překonfigurovat jako aktuální zdrojovou hierarchii a obnovit tak viditelnost dříve migrovaných objektů.  

 Objekty obsažené v jakékoli úloze migrace můžete zobrazit v konzole Configuration Manager, a to tak, že vyberete úlohu migrace a kliknete na kartu **objekty v úloze** .  

 Informace v následujících částech vám pomohou při plánování všech úloh migrace.  

### <a name="data-selection"></a>Výběr dat  
 Při vytváření úlohy migrace kolekce je nutné vybrat jednu či více kolekcí. Po výběru kolekcí se v Průvodci vytvořením úlohy migrace zobrazí objekty, které jsou k těmto kolekcím přidruženy. Ve výchozím nastavení jsou migrovány všechny objekty přidružené k vybraným kolekcím, ale můžete zrušit kontrolu objektů, které nechcete s touto úlohou migrovat. Pokud zrušíte kontrolu objektu, který má závislé objekty, jsou tyto závislé objekty také nezaškrtnuty. Všechny nezaškrtnuté objekty jsou přidány do seznamu vyloučení. Objekty umístěné na seznamu vyloučení jsou vyřazeny z automatického výběru pro budoucí úlohy migrace. Seznam vyloučení je nutné ručně upravit, pokud z něj chcete odstranit objekty, které mají být automaticky vybrány k migraci v úlohách migrace vytvořených v budoucnu.  

### <a name="site-ownership-for-migrated-content"></a>Vlastnictví lokality pro migrovaný obsah  
 Při migraci obsahu pro nasazení je nutné objekt obsahu přiřadit k lokalitě v cílové hierarchii. Tato lokalita se pak stává vlastníkem tohoto obsahu v cílové hierarchii. Přestože je lokalita nejvyšší úrovně ve vaší cílové hierarchii lokalitou, která ve skutečnosti migruje metadata pro obsah, k původním zdrojovým souborům pro obsah v rámci sítě přistupuje přiřazená lokalita.  

 Chcete-li minimalizovat šířku pásma sítě použitou během migrace, zvažte převedení vlastnictví obsahu na nejbližší dostupnou lokalitu. Vzhledem k tomu, že informace o obsahu jsou v Configuration Manager globálně sdíleny, budou k dispozici v každé lokalitě.  

 Informace o obsahu jsou sdíleny ve všech lokalitách v cílové hierarchii pomocí replikace databáze. Veškerý obsah, který přiřadíte k primární lokalitě a následně nasadíte do distribučních bodů v ostatních primárních lokalitách, se přenáší pomocí replikace na základě souborů. Tento přenos je veden přes lokalitu centrální správy a následně do každé další primární lokality. Díky centralizaci balíčků, které plánujete distribuovat do několika primárních lokalit před nebo během migrace, když přiřadíte lokalitu jako vlastníka obsahu, můžete snížit přenos dat napříč sítěmi s malou šířkou pásma.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Obory zabezpečení správy na základě rolí pro migrovaná data  
 Při migraci dat do cílové hierarchie je nutné k objektům, jejichž data jsou migrována, přiřadit jeden nebo více oborů zabezpečení správy na základě rolí. To zajistí, že k těmto datům budou mít po jejich migraci přístup jen příslušní správci. Zadané obory zabezpečení jsou definovány úlohou migrace a jsou použity pro každý objekt migrovaný v rámci této úlohy. Pokud vyžadujete, aby se pro různé sady objektů používaly jiné obory zabezpečení, a chcete tyto obory přiřadit během migrace, je nutné migrovat různé sady objektů pomocí různých úloh migrace.  

 Před nastavením úlohy migrace si prostudujte, jak funguje Správa na základě rolí v Configuration Manager. V případě potřeby nastavte jeden nebo víc oborů zabezpečení pro data, která migrujete, abyste měli kontrolu nad tím, kdo bude mít přístup k migrovaných objektům v cílové hierarchii.  

 Další informace o oborech zabezpečení a správě na základě rolí najdete v tématu [základy správy na základě rolí pro Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Kontrola akcí migrace  
 Při nastavování úlohy migrace se v Průvodci vytvořením úlohy migrace zobrazí seznam akcí, které je nutné provést k zajištění úspěšné migrace, a seznam akcí, které Configuration Manager během migrace vybraných dat trvat. Pečlivě zkontrolujte tyto informace a zkontrolujte očekávaný výsledek.  

### <a name="schedule-migration-jobs"></a>Plánování úloh migrace  
 Ve výchozím nastavení se úloha migrace spustí ihned po jejím vytvoření. Můžete ale určit, kdy se úloha migrace spustí při vytvoření úlohy, nebo úpravou vlastností úlohy. Úlohu migrace můžete naplánovat tak, aby běžela takto:  

-   Spustit úlohu nyní  

-   Spustit úlohu v určitý čas spuštění  

-   Nespouštět úlohu  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Upřesnění řešení konfliktů u migrovaných dat  
 Úlohy migrace ve výchozím nastavení nepřepisují data v cílové databázi, pokud nezměníte konfiguraci úlohy migrace tak, aby přeskočila nebo přepsala data, která byla dříve migrována do cílové databáze.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a>Plánování úloh migrace kolekcí  
 Úlohy migrace kolekcí jsou k dispozici pouze při migraci dat ze zdrojové hierarchie s podporovanou verzí Configuration Manager 2007. Při migraci podle kolekcí je třeba zadat jednu nebo více kolekcí pro migraci. U každé zadané kolekce úloha migrace automaticky vybere všechny související objekty pro migraci. Když například vyberete určitou kolekci uživatelů, dojde k identifikaci členů kolekce a můžete migrovat nasazení přiřazená k této kolekci. Volitelně můžete pro migraci vybrat další objekty nasazení, které jsou k těmto členům přiřazeny. Všechny tyto vybrané položky budou přidány do seznamu objektů, které lze migrovat.  

 Když migrujete kolekci, Configuration Manager také migruje nastavení kolekce, včetně časových intervalů pro správu a údržbu a proměnných kolekce, ale nemůže migrovat nastavení kolekce pro zřizování klientů AMT.  

 Informace v následujících částech vám pomohou získat informace o dalších konfiguracích, které se můžou vztahovat na úlohy migrace na základě kolekcí.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Vyloučení objektů z úloh migrace kolekcí  
 V případě potřeby můžete určité objekty z úlohy migrace kolekce vyloučit. Když vyloučíte konkrétní objekt z úlohy migrace kolekce, tento objekt se přidá do globálního seznamu vyloučení, který obsahuje všechny objekty, které jste vyloučili z úloh migrace vytvořených pro všechny zdrojové lokality v aktuální zdrojové hierarchii. Objekty v seznamu vyloučení jsou stále k dispozici pro migraci v budoucích úlohách, nejsou však automaticky zahrnuty při vytváření nové úlohy migrace na základě kolekce.  

 Seznam vyloučení můžete upravovat a odebírat z něj dříve vyloučené objekty. Objekt odebraný ze seznamu vyloučení je následně automaticky vybrán při zadání přiřazené kolekce během vytváření nové úlohy migrace.  

### <a name="unsupported-collections"></a>Nepodporované kolekce  
 Configuration Manager může migrovat všechny výchozí kolekce uživatelů, kolekce zařízení a většinu vlastních kolekcí ze zdrojové hierarchie Configuration Manager 2007. Configuration Manager ale nemůžou migrovat kolekce obsahující uživatele a zařízení ve stejné kolekci.  

 Následující kolekce nelze migrovat:  

-   Kolekce obsahující uživatele a zařízení.  

-   Kolekce, která obsahuje odkaz na kolekci jiného typu prostředku. Například kolekce založená na zařízení, která má buď podřízenou kolekci, nebo odkaz na kolekci založenou na uživateli. V tomto příkladu je migrována pouze kolekce nejvyšší úrovně.  

-   Kolekce obsahující pravidlo pro zahrnutí neznámých počítačů. Migrace kolekce proběhne, pravidlo zahrnující neznámé počítače však migrováno nebude.  

### <a name="empty-collections"></a>Prázdné kolekce  
 Prázdná kolekce nemá přiřazeny žádné prostředky. Když Configuration Manager migruje prázdnou kolekci, převede ji na organizační složku, která nemá žádné uživatele ani zařízení. Tato složka se vytvoří s názvem prázdné kolekce v uzlu **kolekce uživatelů** nebo **kolekce zařízení** v pracovním prostoru **prostředky a kompatibilita** v konzole Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Propojené a podřízené kolekce  
 Když migrujete kolekce, které jsou propojeny s jinými kolekcemi nebo které mají podřízené kolekce, Configuration Manager kromě propojených kolekcí a podkolekcí vytvoří složku v uzlu **kolekce uživatelů** nebo **kolekce zařízení** .  

### <a name="collection-dependencies-and-include-objects"></a>Závislosti kolekcí a zahrnuté objekty  
 Když v Průvodci vytvořením úlohy migrace zadáte kolekci, která se má migrovat, všechny závislé kolekce se automaticky vyberou pro zahrnutí do úlohy. To zaručuje, že po migraci budou k dispozici všechny potřebné prostředky.  

 Například: vybíráte kolekci pro zařízení s Windows 10 a jmenujeme **Win_10**. Tato kolekce je omezena na kolekci, která obsahuje všechny klientské operační systémy a má název **All_Clients**. Kolekce **All_Clients** bude automaticky vybrána pro migraci.  

### <a name="collection-limiting"></a>Omezení kolekce  
 Když Configuration Manager aktuální větev, kolekce jsou globální data a vyhodnocují se v každé lokalitě v hierarchii. Proto je vhodné naplánovat, jak pro kolekci po její migraci omezit její obor. Při migraci můžete identifikovat kolekci z cílové hierarchie a použít ji k omezení oboru migrované kolekce. Migrovaná kolekce tak nebude zahrnovat neočekávané členy.  

 Například v Configuration Manager 2007 jsou kolekce vyhodnocovány v lokalitě, která je vytvořila a v podřízených lokalitách. Inzerování je možno nasadit pouze do podřízené lokality, což omezí obor tohoto inzerování na příslušnou podřízenou lokalitu. V porovnání s Configuration Manager aktuální větví se kolekce vyhodnocují v každé lokalitě a pro každou lokalitu se pak vyhodnocuje přidružená inzerce. Funkce omezení kolekce umožňuje zúžit členy kolekce na základě jiné kolekce a vyhnout se tak přidání neočekávaných členů.  

### <a name="site-code-replacement"></a>Nahrazení kódu lokality  
 Při migraci kolekce obsahující kritéria, která identifikují lokalitu Configuration Manager 2007, je nutné zadat konkrétní lokalitu v cílové hierarchii. To zajišťuje, že migrovaná kolekce zůstane v cílové hierarchii funkční a nedojde k rozšíření jejího oboru.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Určení chování migrovaných oznámení o inzerovaných programech  
 Ve výchozím nastavení jsou úlohy migrace na základě kolekcí zakázané reklamy, které migrují do cílové hierarchie. To se týká i programů přiřazených k inzerování. Když vytvoříte úlohu migrace na základě kolekce, která obsahuje reklamy, zobrazí se na stránce **Nastavení** Průvodce vytvořením úlohy migrace možnost **Povolit programy pro nasazení v Configuration Manager po migraci inzerce** . Vyberete-li tuto možnost, programy přiřazené k inzerováním budou po migraci povoleny. Jako osvědčený postup tuto možnost nevybírejte. Místo toho povolte programy po migraci, když budete moci ověřit klienty, kteří je obdrží.  

> [!NOTE]  
>  Možnost **Povolit programy pro nasazení v Configuration Manager po migraci inzerce se** zobrazí jenom v případě, že vytváříte úlohu migrace na základě kolekce a úloha migrace obsahuje reklamy.  

 Chcete-li po migraci povolit program, zrušte zaškrtnutí políčka **Zakázat tento program v počítačích, kde je inzerován** na kartě **Upřesnit** ve vlastnostech programu.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a>Plánování úloh migrace objektů  
 Na rozdíl od migrace kolekcí musíte vybrat všechny objekty a jejich instance, které chcete migrovat. Pro přidání do seznamu objektů, které chcete migrovat pro konkrétní úlohu migrace, můžete vybrat jednotlivé objekty (například reklamy z hierarchie Configuration Manager 2007 nebo publikaci ze služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální hierarchie větve). Objekty, které nepřidáte do seznamu migrace, nebudou úlohou migrace objektů migrovány do cílové lokality.  

 Úlohy migrace na základě objektů nemají žádné další konfigurace, které by bylo možné naplánovat nad rámec těch, které platí pro všechny úlohy migrace.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a>Plánování úloh migrace dříve migrovaných objektů  
 Dojde-li ve zdrojové hierarchii k aktualizaci objektu, který jste již migrovali do cílové hierarchie, můžete jej znovu migrovat pomocí úlohy migrace typu **Objekty upravené po migraci**. Když například přejmenujete nebo aktualizujete zdrojové soubory balíčku ve zdrojové hierarchii, verze balíčku ve zdrojové hierarchii se zvýší. Po zvýšení verze balíčku jej tento typ úlohy může identifikovat pro migraci.  

 Tento typ úlohy je podobný typu migrace objektů. Liší se pouze tím, že při výběru objektů pro migraci můžete vybrat pouze objekty, které byly aktualizovány od své migrace v rámci předchozí úlohy.   

 Když vyberete tento typ úlohy, chování řešení konfliktů na stránce **Nastavení** Průvodce vytvořením úlohy migrace je nakonfigurované tak, aby přepsalo dříve migrované objekty. Toto nastavení nelze změnit.  

> [!NOTE]  
>  Tento typ úlohy může identifikovat objekty automaticky aktualizované zdrojovou hierarchií a objekty aktualizované správcem.  
