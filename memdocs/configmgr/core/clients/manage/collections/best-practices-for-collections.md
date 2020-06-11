---
title: Osvědčené postupy pro kolekce
titleSuffix: Configuration Manager
description: Získejte doporučení pro konfiguraci kolekcí a hodnocení shromažďování v Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ee640a70eea9f2e8470e852409911d28e542bc2
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663365"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Osvědčené postupy pro kolekce v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Některé doprovodné materiály ke správě kolekcí můžou být protichůdné. Například z důvodů výkonu byste měli omezit počet kolekcí, které se často aktualizují. Aktualizace kolekcí je ale často praktická, protože většina funkcí Configuration Manager závisí na kolekcích. Při návrhu a konfiguraci kolekcí a vyhodnocování kolekcí pečlivě zvažte jak dopady na výkon, tak i obchodní požadavky.

Pro kolekce v Configuration Manager použijte následující osvědčené postupy.  

## <a name="configure-maintenance-window-for-updates"></a>Konfigurovat časové období údržby pro aktualizace

Můžete nakonfigurovat časové intervaly pro správu a údržbu pro kolekce zařízení a omezit tak dobu, po kterou Configuration Manager můžou na tato zařízení instalovat software. Pokud nakonfigurujete časové intervaly pro správu a údržbu, aby byla příliš malá, klient nebude moci instalovat důležité aktualizace softwaru, což klientovi ponechá problémy, které aktualizace snižuje.

Důležité informace, které je potřeba vzít v úvahu při plánování oken údržby:

- Výchozí maximální doba běhu aktualizace softwaru je 60 minut.
- Když Configuration Manager vypočítá, jestli se aktualizace může nainstalovat, přidá pět minut do maximální doby běhu pro restartování.
- Zbývající doba trvání časového období údržby musí být delší než maximální doba běhu aktualizace softwaru plus pět minut.

## <a name="avoid-frequent-collection-evaluation"></a>Vyhnout se častému vyhodnocování kolekcí

Úplné vyhodnocení kolekce vyhodnocuje nejen cílovou kolekci, ale také všechny kolekce, které kolekce omezuje, pokud dojde k aktualizaci. Kolekce bez plánu je také vyhodnocena, pokud je jejich omezení aktualizace kolekce. Proto je možné, že některé kolekce mohou být vyhodnocovány častěji, než očekáváte.

V případě zaneprázdněného Configuration Managerho prostředí můžete zlepšit výkon vyhodnocení kolekce škálováním back-v, aby nedocházelo k opakovanému vyhodnocení kolekcí. V hloubkovém stromu můžete snížit četnost vyhodnocování shromažďování, protože se kolekce dokončí podrobněji na úrovni stromu, protože hodnocení kolekce vyšší úrovně také spustí hodnocení kolekce nižší úrovně.

## <a name="understand-the-collection-evaluation-graph"></a>Pochopení grafu vyhodnocení kolekce

Mějte na paměti, jak graf hodnocení kolekce funguje, abyste mohli navrhnout vhodnou strukturu kolekce. Nespoléhá se na úplné vyhodnocení shromažďování dat, aby se vždy aktualizovaly všechny kolekce. Pokud se přírůstkově aktualizuje aktualizace kolekce podle plánu, nemusí se aktualizace na kolekce, které nejsou povolené pro přírůstkové aktualizace, aktualizovat. Vzhledem k tomu, že během přírůstkových hodnocení pravděpodobně došlo k aktualizacím, úplné vyhodnocení nemusí aktualizovat kolekci a ukončit graf vyhodnocení kolekce pro daný cyklus. V takovém případě nejsou k dispozici žádná referenční hodnocení kolekce. Další informace najdete v tématu [graf vyhodnocení kolekce](collection-evaluation.md#collection-evaluation-graph).

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a>Omezení přírůstkových aktualizací

Povolení přírůstkových aktualizací pro mnoho kolekcí může způsobit zpoždění při vyhodnocování. Je nejvhodnější omezit počet přírůstkově aktualizovaných kolekcí na 200. Přesné číslo závisí na:

- Celkový počet kolekcí
- Frekvence přidávání a měnění nových prostředků v hierarchii
- Počet klientů v hierarchii
- Složitost pravidel členství kolekce v hierarchii

Pokud cyklus přírůstkového hodnocení trvá déle než nakonfigurovaná frekvence aktualizace, pak Configuration Manager neustále zpracovává hodnocení shromažďování, což by mohlo mít dopad na výkon systému. Snižte počet přírůstkově aktualizovaných kolekcí nebo zvyšte dobu mezi cykly přírůstkového vyhodnocení.

Vzhledem k potenciálním dopadům přírůstkových kolekcí je důležité mít zásady nebo postupy pro vytváření kolekcí a přiřazování plánů aktualizací. Příklady požadavků zásad můžou být:

- Pro kolekce, které se používají pro rozsah zabezpečení, nastavení klienta a časová období údržby, používejte jenom přírůstkové aktualizace. Tyto aktualizace kolekcí ovlivňují chování klienta a přístup k prostředkům.
- Pro aplikace bez souhlasu s licencováním, inzerovat aplikace do stávajících kolekcí a používejte globální podmínky k omezení dostupnosti.
- Vyosnovujte příslušná období pro jiné kolekce, které mají naplánované úplné aktualizace kolekcí.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>Vyhněte se vyhodnocování velkých stromů z certifikačních autorit

V prostředí Configuration Manager nevyhodnocují lokalita centrální správy (CAS) členství v kolekci. Primární lokality jsou jediné lokality, které vyhodnotí kolekce. Sekundární lokality fungují jako proxy servery, které používají jenom data, která replikují z primární lokality.

Pro vyžádání aktualizace kolekce certifikační autorita odešle požadavek do každé primární lokality. Primární lokality vyhodnocují kolekci a odešlou výsledky zpátky do certifikačních autorit. Výsledky hodnocení kolekce se zobrazí až po tom, co se všechny pokyny pro vyhodnocení kolekce replikují do všech lokalit. všechny lokality vyhodnocují všechny kolekce a všechny se vrátí do certifikačních autorit a konsolidují.

Následující diagram znázorňuje tok, když si CAS vyžádá ruční aktualizaci kolekce:

![Ruční aktualizace kolekce z CAS](media/manual-collection-update-from-cas.png)

Aktualizace kolekce z certifikačních autorit s více primárními lokalitami může být časově náročná. Pokud se kolekce nevyhodnocuje včas, je to, že se žádost opakuje.

Po zahájení vlákna vyhodnocení kolekce a načtení grafu vyhodnocení pokračuje vyhodnocení, dokud není graf vyhodnocení kolekce prázdný. Vlákno se pak ukončí a bude k dispozici pro další vyhodnocení. Pokud však jiné cykly vyhodnocování kolekce vyhodnocuje, že vlákno vyhodnocuje kolekce, vlákno se okamžitě restartuje, aby se pokusilo o vyhodnocení "zmeškaného" cyklu.

Každá metoda vyhodnocení se spouští ve vlastním vlákně. Je možné, že v rámci vlákna se Configuration Manager může pokusit grafovat stejnou kolekci více než jednou. Configuration Manager potom druhou a následnou žádost poklesne.

Aby nedocházelo k těmto scénářům, vyhněte se ručním hodnocením shromažďování velkých stromů, zejména při práci z certifikačních autorit s více lokalitami.

## <a name="consider-collection-depth-and-cross-referencing"></a>Zvážení hloubky kolekce a křížového odkazu

Chcete-li si vyvážit rovnováhu mezi podnikovými požadavky a výkonem, je důležité pochopit strukturu kolekce, kterou vytvoříte, a její závislosti na dalších kolekcích. Pokud vytvoříte kolekci s pravidly, která odkazují na jednu nebo více kolekcí, které odkazují také na jiné kolekce, vyhodnotí se všechny tyto kolekce a vytvoří se členství v kolekci.

Pravidla zahrnutí a vyloučení kolekce v Configuration Manager odkazují na kolekce snadněji než zápis vlastního dotazu WQL. Pokud ale použijete možnost zahrnout a vyloučit kolekce, výsledkem je vysoký výkon, můžete místo toho použít metodu dotazu WQL:

Připojit

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Slevy

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>Monitorování hodnocení kolekce pomocí CEViewer

Pomocí [nástroje CEViewer (Collection Evaluation Viewer)](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) můžete monitorovat počet vyhodnocených kolekcí a dobu, po kterou se jednotlivé kolekce aktualizují. CEViewer je na *disku CD-ROM. Poslední* složka na serveru lokality.

Chcete-li ručně provést podobnou kontrolu s SQL, můžete použít následující dotaz:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


