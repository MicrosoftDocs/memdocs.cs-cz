---
title: Odinstalace lokalit
titleSuffix: Configuration Manager
description: Příručka pro odebrání rolí a odinstalace lokalit a hierarchií
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718046"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Odinstalace rolí, lokalit a hierarchií v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek slouží jako vodítko pro odinstalaci Configuration Manager role systému lokality, lokality nebo hierarchie.

Počínaje verzí 2002 můžete také odebrat lokalitu centrální správy (CAS) z hierarchie, ale zachovat primární lokalitu.

## <a name="site-system-role"></a><a name="bkmk_role"></a>Role systému lokality

Z následujících důvodů je vhodné odebrat roli ze serveru systému lokality:

- Širší změna infrastruktury, jako třeba síťová nebo fyzická umístění
- Vyřazení základního serveru z provozu
- Konsolidace rolí za účelem snížení nákladů a složitosti
- Překonfigurování nebo změna návrhu rolí webu
- Ukončit použití funkce, kterou role podporuje

Pokud se rozhodnete, že potřebujete roli odebrat, nejdřív Vezměte v úvahu odpovědi na následující otázky:

- Stále potřebujete roli v lokalitě? Pokud ano, má již role jiný systém lokality?

- Jsou jiné systémy lokality s touto rolí správně ve velikosti, aby podporovaly vaše podnikové požadavky na výkon a dostupnost?

- Jsou všichni klienti již překonfigurováni na používání jiné role? Spoléháte se na výchozí chování klienta, abyste mohli vrátit nebo zjistit jiný server?

### <a name="procedure-to-remove-a-site-system-role"></a>Postup odebrání role systému lokality

K odebrání role použijte následující postup:

1. V konzole **Configuration Manager** otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a pak vyberte uzel **servery a role systému lokality** .

1. Vyberte server systému lokality s rolí, kterou chcete odebrat. V podokně podrobností **role systému lokality** vyberte cílovou roli.

1. Na pásu karet na kartě **role webového** serveru ve skupině **role lokality** vyberte **Odebrat roli**. Potvrďte, že chcete roli odebrat.

### <a name="additional-information-for-specific-roles"></a>Další informace pro konkrétní role

Některé role mohou mít další kroky a požadavky.

#### <a name="software-update-point"></a>Bod aktualizace softwaru

Po odebrání bodu aktualizace softwaru Configuration Manager aktualizace zásad klienta, aby se bod aktualizace softwaru odebral ze seznamu. Když odeberete poslední bod aktualizace softwaru v lokalitě, nebude seznam bodů aktualizace softwaru obsahovat žádné body aktualizace softwaru. V případě, že nejsou k dispozici žádné role, Správa aktualizací softwaru je v lokalitě v podstatě zakázaná.

Pokud máte v primární lokalitě více než jeden bod aktualizace softwaru a odeberete bod aktualizace softwaru, který je zdrojem synchronizace, vyberte jiný bod aktualizace softwaru v lokalitě, který bude novým zdrojem synchronizace.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a>Sekundární lokalita  

Kromě toho, že vyřadíte [hierarchii z provozu](#bkmk_hierarchy), hlavní důvod odebrání sekundární lokality je z důvodu širší změny infrastruktury, jako je třeba síťové nebo fyzické umístění. Přečtěte si také důvody pro [Výběr sekundární lokality](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

Pokud se rozhodnete, že potřebujete odebrat sekundární lokalitu, zvažte nejprve odpověď na následující otázky:

- Odebrali jste všechny role systému lokality ze serveru lokality?

- Jsou k sekundární lokalitě přidruženy nějaké hranice nebo skupiny hranic? Před odebráním lokality překonfigurujte hranice.

- Pořád existují klienti v umístění?

- Nakonfigurovali jste jiné možnosti správy obsahu, jako je například [ukládání do sdílené mezipaměti](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)?

### <a name="options-to-delete-secondary-sites"></a>Možnosti odstranění sekundárních lokalit

Sekundární lokalitu nemůžete přesunout ani změnit její přiřazení na jinou primární lokalitu. Když odeberete sekundární lokalitu z její přímé nadřazené lokality, vyberte, jestli se má odinstalovat nebo odstranit.

#### <a name="uninstall-the-secondary-site"></a>Odinstalace sekundární lokality

Tuto možnost použijte, pokud chcete odebrat funkční sekundární lokalitu, která je přístupná ze sítě. Tato možnost odinstaluje Configuration Manager ze serveru sekundární lokality. Pak odstraní všechny informace o lokalitě a jejích prostředcích z Configuration Manager webu.

Pokud je pro sekundární lokalitu Configuration Manager nainstalovaná SQL Server Express, Configuration Manager odinstaluje také SQL Express. Pokud jste nainstalovali SQL Server Express před instalací sekundární lokality, Configuration Manager SQL Server Express odinstalovat.

#### <a name="delete-the-secondary-site"></a>Odstranit sekundární lokalitu

Tuto možnost použijte v následujících situacích:

- Instalace se nezdařila

- Po odinstalaci se konzola Configuration Manager stále zobrazuje v sekundární lokalitě

    Tato možnost odstraní všechny informace o lokalitě a jejích prostředcích z Configuration Manager hierarchie, ale neprovede žádné změny na serveru lokality.

    > [!TIP]
    >  K odstranění sekundární lokality můžete použít také nástroj pro údržbu hierarchie s možností **/DELSITE** . Další informace najdete v tématu [Nástroj Údržba hierarchie (Preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>Předpoklady odstranění sekundární lokality

Administrativní uživatel, který spouští Configuration Manager instalační program, potřebuje následující bezpečnostní oprávnění:

- Práva místního **správce** na serveru sekundární lokality

- Pokud je server databáze primární lokality vzdálený od primárního serveru lokality, oprávnění místního **správce** k serveru databáze vzdálené lokality pro primární lokalitu.

- Role zabezpečení **správce infrastruktury** nebo správce s **úplnými oprávněními** pro nadřazenou primární lokalitu

- Oprávnění **sysadmin** v databázi sekundární lokality

### <a name="procedure-to-delete-a-secondary-site"></a>Postup odstranění sekundární lokality

Chcete-li odinstalovat nebo odstranit sekundární lokalitu, použijte následující postup:

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte uzel **lokality** .

1. Vyberte server sekundární lokality, který chcete odebrat. Na pásu karet na kartě **Domů** ve skupině **lokalita** vyberte možnost **Odstranit**.

1. Na stránce **Obecné** vyberte, zda má být sekundární lokalita odinstalována nebo odstraněna.

1.  Dokončete průvodce.

## <a name="primary-site"></a><a name="bkmk_primary"></a>Primární lokalita  

Primární lokalitu můžete z hierarchie chtít odinstalovat z následujících důvodů:

- Konsolidace webů za účelem snížení nákladů a složitosti
- Překonfigurujte nebo změňte návrh lokalit v hierarchii.

Před odinstalováním podřízené primární lokality, která používá [distribuovaná zobrazení](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) pro svůj odkaz replikace na certifikační autority, nejprve vypněte distribuovaná zobrazení ve vaší hierarchii. Další informace najdete v tématu [Odinstalace primární lokality nakonfigurované s distribuovanými zobrazeními](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a>Naplánování odinstalace primární lokality

Než odinstalujete primární lokalitu, Projděte si následující úlohy:

- Kontrola hranic, skupin hranic a záložních vztahů. Pokud přiřadíte klienty k nové lokalitě, ale nezměníte hranice, mohou být považovány za roaming. Další informace najdete v tématu [definice hranic lokality a skupin hranic](../configure/define-site-boundaries-and-boundary-groups.md).

- Zajistěte, aby všichni aktivní klienti byli přiřazeni k jiné primární lokalitě v hierarchii. Jinak budou klienti po odinstalování lokality nespravováni. Další informace najdete v tématu [přiřazení klientů k lokalitě](../../../clients/deploy/assign-clients-to-a-site.md).

  - Zkontrolujte seznam rolí lokality, abyste se ujistili, že nová lokalita poskytuje stejnou úroveň služby.

  - Ujistěte se, že v druhé lokalitě máte správnou velikost ostatních systémů lokality. Budou muset podporovat vaše podnikové požadavky na výkon a dostupnost u dalších klientů.

  - Pokud má tento web spoustu klientů, přiřaďte je znovu ve fázích. Monitorování replikace databáze jako klienti aktualizují úplný soupis a jiná data specifická pro konkrétní lokalitu. Pokud spravujete aktualizace softwaru, klienti se přiřadí k novému bodu aktualizace softwaru. Toto chování způsobí úplnou kontrolu kompatibility aktualizací.

  - Opětovné přiřazení klienta může ovlivnit sestavy a dotazy, které spoléhají na data inventáře, a dodržování předpisů na základě stavu. Zvažte dočasné úpravy všech cyklů klienta během přechodu.

  - Zkontrolujte všechny metody přiřazení klienta, abyste se ujistili, že žádné neodkazují na tuto primární lokalitu.

- Ověřte, zda všechny aktivně používané objekty v hierarchii mají statické odkazy na kód lokality. Například dotazy kolekce, pořadí úloh nebo skripty pro správu.

- Pokud hierarchie používá [záložní lokalitu](../configure/boundary-group-procedures.md#bkmk_site-fallback) pro automatické přiřazení lokality, ujistěte se, že neodkazuje na tuto primární lokalitu.

- Překonfigurujte všechny [metody instalace klienta](../../../clients/deploy/plan/client-installation-methods.md) , které mohou odkazovat na kód statické lokality.

- Pokud má tato primární lokalita nějaké služby připojené ke cloudu pro konkrétní lokalitu, nezapomeňte je odebrat. Pokud stále potřebujete cloudové prostředky, přesuňte je do jiné primární lokality v hierarchii. Odeberte je z primární lokality, kterou se chystáte odinstalovat, a přidejte je do jiné primární lokality.

- Pokud má primární lokalita nějaké [metody zjišťování](../configure/run-discovery.md) pro hierarchii, přesuňte je do jiné lokality.

- Vyřaďte všechna média pro [nasazení operačního systému](../../../../osd/deploy-use/create-task-sequence-media.md)na základě lokality.

- Odinstalujte všechny role systému lokality z lokality a ze serveru lokality. Další informace najdete v tématu [odinstalace rolí systému lokality](#bkmk_role). I když se tento přípravný krok nepožaduje, pomůže určit další závislosti před odinstalováním lokality.

- Odinstalujte všechny sekundární lokality v rámci této primární lokality. Další informace najdete v části [sekundární lokalita](#bkmk_secondary) .

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a>Předpoklady pro odinstalaci primární lokality

Administrativní uživatel, který spouští Configuration Manager instalační program, potřebuje následující bezpečnostní oprávnění:

- Práva místního **správce** na serveru CAS

- Pokud je databázový server CAS vzdálený od serveru lokality, oprávnění místního **správce** k serveru databáze vzdálené lokality pro certifikační autority.

- Oprávnění **sysadmin** v databázi lokality CAS

- Oprávnění místního **správce** na serveru primární lokality

- Pokud je server databáze primární lokality vzdálený od primárního serveru lokality, oprávnění místního **správce** k serveru databáze vzdálené lokality pro primární lokalitu.

- Role zabezpečení **správce infrastruktury** nebo správce s **úplnými oprávněními** na certifikačních autoritách

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a>Postup odinstalace primární lokality

Spuštěním instalačního programu Configuration Manager odinstalujete primární lokalitu, která nemá přidruženou sekundární lokalitu. K odinstalaci primární lokality použijte následující postup:

> [!TIP]
> Pokud server primární lokality již není k dispozici, odstraňte primární lokalitu z databáze lokality pomocí nástroje pro údržbu hierarchie na certifikačních autoritách. Další informace najdete v tématu [Nástroj Údržba hierarchie (Preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Spusťte instalaci Configuration Manager na serveru primární lokality pomocí jedné z následujících metod:

    - V nabídce **Start** vyberte **Configuration Manager nastavení**.

    - V adresáři pro *instalační médium*Configuration Manager otevřete `\SMSSETUP\BIN\X64\setup.exe`. Ujistěte se, že je tato verze stejná jako verze lokality.

    - V adresáři, ve kterém je *nainstalováno*Configuration Manager `\BIN\X64\setup.exe`, otevřete.

1. Přečtěte si informace na stránce **než začnete** .

1. Na stránce **Začínáme** vyberte možnost **odinstalovat Configuration Manager lokalitu**.

    > [!IMPORTANT]  
    >  Když je k primární lokalitě připojena sekundární lokalita, je nutné nejprve odebrat sekundární lokalitu, aby bylo možné odinstalovat primární lokalitu.  

1. Na stránce **odinstalovat Configuration Manager lokalitu** jsou ve výchozím nastavení povolené obě následující možnosti:

    - Odebrat databázi lokality z primárního serveru lokality
    - Odebrání konzoly Configuration Manager

1. Vyberte **Ano** , pokud chcete potvrdit odinstalaci primární lokality Configuration Manager.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a>Odinstalace primární lokality, která používá distribuovaná zobrazení

1. Než odinstalujete podřízenou primární lokalitu, vypněte distribuovaná zobrazení u každého odkazu v hierarchii mezi certifikačními autoritami a primární lokalitou.

1. Po vypnutí distribuovaných zobrazení na jednotlivých odkazech potvrďte, že data z primární lokality se dokončí znovu při inicializaci v certifikačních autoritách. Informace o tom, jak monitorovat inicializaci dat, najdete v tématu [monitorování replikace](../../manage/monitor-replication.md).

1. Po úspěšném dokončení opětovné inicializace dat s CAS můžete [primární lokalitu odinstalovat](#bkmk_pri-process).

1. Po odinstalaci primární lokality můžete distribuovaná zobrazení překonfigurovat na odkazy z certifikačních autorit na jiné primární lokality.

    > [!IMPORTANT]
    > Pokud odinstalujete primární lokalitu před vypnutím distribuovaných zobrazení v jednotlivých lokalitách nebo před tím, než se data z primární lokality úspěšně znovu inicializuje v certifikačních autoritách, může dojít k selhání replikace dat.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a>Vyřazení hierarchie z provozu

Některé organizace mají několik hierarchií z důvodu fúzí, akvizic, testovacích prostředí nebo jiných obchodních požadavků. Pokud konsolidujete správu do jedné hierarchie, může tato akce snížit náklady a složitost. Dalším důvodem pro vyřazení hierarchie je, že migrujete do cloudové služby pro správu, jako je například Microsoft Intune, a jste připraveni odebrat místní infrastrukturu.

Pokud chcete vyřadit z provozu hierarchii s více lokalitami, je důležité pořadí odebrání. Začněte odinstalací lokalit na konci hierarchie a potom nahoru:

1. Odeberte sekundární lokality připojené k primárním lokalitám.
2. Odinstalujte primární lokality.
3. Po odinstalaci všech primárních lokalit můžete certifikační autority odinstalovat.

Další informace najdete v následujících částech:

- [Odebrat sekundární lokalitu](#bkmk_secondary)
- [Odinstalace primární lokality](#bkmk_primary)
- [Odinstalace certifikačních autorit](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a>Odinstalace certifikačních autorit

Posledním krokem k vyřazení hierarchie z provozu je odinstalace certifikačních autorit. Pro odinstalaci certifikačních autorit, které nemají podřízené primární lokality, spusťte instalační program Configuration Manager.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Předpoklady pro odinstalaci certifikačních autorit

Administrativní uživatel, který spouští Configuration Manager instalační program, potřebuje následující bezpečnostní oprávnění:

- Práva místního **správce** na serveru CAS

- Pokud je databázový server CAS vzdálený od serveru lokality, oprávnění místního **správce** k serveru databáze vzdálené lokality pro certifikační autority.

#### <a name="procedure-to-uninstall-the-cas"></a>Postup odinstalace certifikačních autorit

1. Spusťte instalaci Configuration Manager na serveru CAS pomocí jedné z následujících metod:

    - V nabídce **Start** vyberte **Configuration Manager nastavení**.

    - V adresáři pro *instalační médium*Configuration Manager otevřete `\SMSSETUP\BIN\X64\setup.exe`. Ujistěte se, že je tato verze stejná jako verze lokality.

    - V adresáři, ve kterém je *nainstalováno*Configuration Manager `\BIN\X64\setup.exe`, otevřete.

1. Přečtěte si informace na stránce **než začnete** .

1. Na stránce **Začínáme** vyberte možnost **odinstalovat Configuration Manager lokalitu**.

    > [!IMPORTANT]  
    >  Než budete moci odinstalovat certifikační autority, odeberte všechny podřízené primární lokality.  

1. Na stránce **odinstalovat Configuration Manager lokalitu** jsou ve výchozím nastavení povolené obě následující možnosti:

    - Odebrání databáze lokality ze serveru CAS
    - Odebrání konzoly Configuration Manager

1. Výběrem **Ano** potvrďte odinstalaci Configuration Manager lokality centrální správy (CAS).

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a>Odebrání certifikačních autorit

<!-- 3607277 -->

Pokud se v hierarchii verze 2002 skládá z certifikačních autorit a jedné podřízené primární lokality, můžete certifikační autority odebrat. Tato akce zjednodušuje infrastrukturu Configuration Manager pro jednu samostatnou primární lokalitu. Odstraňuje složitosti replikace typu Site-to-site a zaměřuje úlohy správy na jednu lokalitu.

Další informace najdete v tématu [Odebrání certifikačních autorit](remove-central-administration-site.md).
