---
title: Úlohy údržby
titleSuffix: Configuration Manager
description: Seznamte se s úlohami údržby, které je potřeba provést pro Configuration Manager lokalit a hierarchií a kdy je můžete provést.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713727"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Úlohy údržby pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager lokality a hierarchie vyžadují pravidelnou údržbu a monitorování, aby poskytovaly služby efektivně a nepřetržitě. Pravidelná údržba zajišťuje, že hardware, software a Configuration Manager databáze budou dál fungovat správně a efektivně. Optimální výkon významně snižuje riziko selhání.  

 Pokud chcete nastavit výstrahy a používat stavový systém ke sledování stavu Configuration Manager, přečtěte si téma [použití výstrah a stavového systému pro Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a>Úlohy údržby

 Pravidelná údržba je důležitá pro zajištění správného provozu lokality. Udržujte si protokol údržby k dokumentaci údržby dat, kdo provedl údržbu, a veškeré komentáře k údržbě související s úlohami. Chcete-li spravovat web, zvažte každodenní nebo týdenní údržbu. Některé úlohy můžou vyžadovat jiný plán. Společná údržba může zahrnovat integrované úlohy údržby i další úkoly, jako je údržba účtů, aby se zachovalo dodržování zásad vaší společnosti.  

 Následující informace použijte jako vodítko, které vám pomohou naplánovat, kdy provádět různé úlohy údržby. Tyto seznamy použijte jako výchozí bod a přidejte úkoly, které možná budete potřebovat.  

### <a name="daily-tasks"></a>Denní úlohy
Níže jsou uvedené úlohy údržby, které můžete zvážit u denního plánu:  

- Ověřte, že předdefinované úlohy údržby, které mají naplánované spouštění, jsou úspěšně spuštěné.  

- Ověřte stav databáze Configuration Manager.  

- Zkontroluje stav serveru lokality.  

- Zaškrtněte Configuration Manager pro soubory nevyřízených položek v systému lokality.  

- Zkontroluje stav systémů lokalit.  

- Ověřte protokoly událostí operačního systému ze systémů lokality.  

- Podívejte se do protokolu chyb SQL Server z počítače databáze lokality.  

- Kontroluje výkon systému.  

- Kontrolovat výstrahy Configuration Manager.  

### <a name="weekly-tasks"></a>Týdenní úlohy

Níže jsou uvedené úlohy údržby, které můžete zvážit pro týdenní plán:  

- Ověřte, zda jsou předdefinované úlohy údržby naplánované ke spuštění týdně spuštěny.  

- Odstraňte nepotřebné soubory ze systémů lokalit.  

- V případě potřeby Vytvářejte a distribuujte sestavy koncových uživatelů.  

- Zazálohujte protokoly událostí aplikace, zabezpečení a systému a zrušte jejich zaškrtnutí.  

- Zkontrolujte velikost databáze lokality a ověřte, zda je na serveru databáze lokality dostatek volného místa na disku, aby mohla databáze lokality růst.  

- Proveďte SQL Server údržbu databáze v databázi lokality podle vašeho plánu SQL Server údržby.  

- Ověřte dostupné místo na disku ve všech systémech lokality.  

- Spusťte nástroje pro defragmentaci disku na všech systémech lokality.  

### <a name="periodic-tasks"></a>Pravidelné úlohy

Některé úkoly, které nevyžadují denní nebo týdenní údržbu, jsou důležité k zajištění celkového stavu lokality. Tyto úlohy také zajistí aktuálnost plánů zabezpečení a zotavení po havárii. Níže jsou uvedené úlohy údržby, které můžete zvážit pro pravidelný plán, než denní nebo týdenní úkoly:  

- Změňte účty a hesla, pokud je to nutné, podle vašeho plánu zabezpečení.  

- Zkontrolujte plán údržby a zkontrolujte, zda jsou naplánované úlohy údržby naplánovány správně a efektivně v závislosti na nakonfigurovaných nastaveních lokality.  

- Projděte si návrh hierarchie Configuration Manager pro všechny požadované změny.  

- Zkontrolujte výkon sítě, abyste zajistili, že nebyly provedeny změny, které mají vliv na operace lokality.  

- Ověřte, že nastavení služby Active Directory, která mají vliv na operace lokality, se nezmění. Například ověřte, zda se nezměnily podsítě přiřazené k lokalitám služby Active Directory a používané jako hranice pro lokalitu Configuration Manager.  

- Projděte si plán zotavení po havárii pro všechny požadované změny.  

- Proveďte obnovení lokality podle plánu zotavení po havárii v testovacím prostředí pomocí záložní kopie nejnovější zálohy, kterou vytvořila úloha údržby Zálohovat server webu.

- Ověřte, zda hardware neobsahuje chyby nebo dostupné aktualizace hardwaru.  

- Zkontroluje celkový stav webu.  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a>Údržba provozního stavu databáze lokality

 I když Configuration Manager lokalita a hierarchie provádí úlohy, které naplánujete a nastavíte, komponenty lokality průběžně přidávají data do databáze Configuration Manager. Jak roste objem dat, výkon databáze a volný prostor úložiště v databázi se odmítne. Můžete nastavit úlohy údržby lokality a odebrat zastaralá data, která už nepotřebujete.  

 Configuration Manager poskytuje předdefinované úlohy údržby, které můžete použít k údržbě stavu databáze Configuration Manager. Ne všechny úlohy údržby jsou ve výchozím nastavení k dispozici v každé lokalitě. Některé úlohy jsou povolené, zatímco některé nejsou, a všechny podporují plán, který můžete nastavit.  

 Většina úloh údržby pravidelně odebírá zastaralá data z databáze Configuration Manager. Snížení velikosti databáze odebráním nepotřebných dat zlepšíte výkon a integritu databáze, čímž se zvýší efektivita lokality a hierarchie. Další úlohy, jako jsou **opakované sestavení indexů**, vám pomůžou zajistit efektivitu databáze. Další úkoly, jako je úloha **Zálohování serveru lokality** , vám pomůžou připravit se na zotavení po havárii.  

> [!IMPORTANT]
> Při plánování plánu všech úloh, které odstraní data, zvažte použití těchto dat napříč hierarchií. Když úkol, který odstraňuje data, se v lokalitě spustí, informace se z databáze Configuration Manager odstraní a tato změna se replikuje na všechny lokality v hierarchii. Toto odstranění může ovlivnit jiné úkoly, které se na tato data spoléhají. Například v lokalitě centrální správy můžete nastavit, aby bylo zjišťování spouštěno jednou měsíčně k identifikaci neklientských počítačů. Plánujete instalaci klienta Configuration Manager do těchto počítačů během dvou týdnů od jejich zjišťování. V jedné lokalitě v hierarchii však správce nastaví úlohu odstranit zastaralá data zjišťování, která se spustí každých 7 dní. Výsledkem je, že sedm dní po zjištění neklientských počítačů se odstraní z databáze Configuration Manager. Zpět v lokalitě centrální správy se připravujete na nabízenou instalaci Configuration Manager klienta na tyto nové počítače 10. den. Vzhledem k tomu, že úloha Odstranit zastaralá data zjišťování nedávno spustila a odstranila data, která jsou sedm dní nebo starší, již nedávno zjištěné počítače nejsou v databázi k dispozici.

Po instalaci lokality Configuration Manager zkontrolujte dostupné úlohy údržby a povolte úlohy, které vaše operace vyžaduje. Zkontrolujte výchozí plán jednotlivých úloh a v případě potřeby nastavte plán pro vyladění úlohy údržby tak, aby vyhovovaly vaší hierarchii a prostředí. I když výchozí plán jednotlivých úloh by měl vyhovovat většině prostředí, monitorovat výkon vašich lokalit a databází a očekávat doladění úloh, aby se zvýšila efektivita nasazení. Naplánujte pravidelnou kontrolu výkonu lokality a databáze a překonfigurujte úlohy údržby a jejich plány na zachování této efektivity.  

## <a name="set-up-maintenance-tasks"></a>Nastavení úloh údržby

 Každý Configuration Manager web podporuje úlohy údržby, které pomůžou zajistit provozní efektivitu databáze lokality. Ve výchozím nastavení jsou v každé lokalitě povoleny některé úlohy údržby a všechny úlohy podporují nezávislé plány. Úlohy údržby se nastavují individuálně pro každou lokalitu a vztahují se na databázi v dané lokalitě. Některé úlohy, jako je **odstranění zastaralých dat zjišťování**, ale ovlivňují informace, které jsou k dispozici ve všech lokalitách v hierarchii.  

 V konzole Configuration Manager se zobrazí pouze úlohy údržby, které lze nastavit v lokalitě. Úplný seznam úloh údržby podle typu lokality najdete v tématu [referenční informace o úlohách údržby pro Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Pomocí následujícího postupu můžete nastavit společné nastavení úloh údržby.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Nastavení úloh údržby pro Configuration Manager verze 1906
<!--3555894-->
Počínaje verzí 1906 se úlohy údržby serveru lokality teď dají zobrazit, upravit a sledovat na vlastní kartě v zobrazení podrobností serveru lokality. Úlohy údržby můžete i nadále upravovat výběrem možnosti **Údržba lokality** ve skupině **Nastavení** , jako jste to v předchozích Configuration Manager verzích.

1. V konzole Configuration Manager klikněte na **Správa** > **Konfigurace** >lokality**lokality**.
1. Vyberte lokalitu ze seznamu a pak klikněte na kartu **úlohy údržby** na panelu podrobností.
1. Zobrazí se pouze úlohy, které jsou k dispozici ve vybrané lokalitě. Klikněte pravým tlačítkem myši na jednu z úloh údržby a vyberte jednu z následujících možností:
   - **Povolit** – zapnout úlohu.
   - **Disable** – vypněte úlohu.
   - **Upravit** – upraví plán úlohy nebo jeho vlastnosti.

![Karta pro úlohy údržby v zobrazení podrobností serveru lokality](./media/3555894-maintenance-tasks.png)

Karta **úlohy údržby** vám poskytne tyto informace:

- Pokud je úkol povolený
- Plán úlohy
- Čas posledního spuštění
- Čas posledního dokončení
- Pokud byla úloha úspěšně dokončena
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Nastavení úloh údržby pro Configuration Manager verze 1902 a předchozí

1. V konzole Configuration Manager klikněte na **Správa** > **Konfigurace** >lokality**lokality**.
2. Vyberte lokalitu, která má úlohu údržby, kterou chcete nastavit.  
3. Na kartě **Domů** ve skupině **Nastavení** vyberte **Údržba lokality**a pak zvolte úlohu údržby, kterou chcete nastavit. Zobrazí se pouze úlohy, které jsou k dispozici ve vybrané lokalitě.

4. Chcete-li nastavit úlohu, klikněte na tlačítko **Upravit**. Zajistěte, aby bylo zaškrtnuté políčko **Povolit tuto úlohu** , a nastavte plán, kdy se má úloha spustit. Pokud úloha také odstraní zastaralá data, nastavte stáří dat, která budou odstraněna z databáze při spuštění úlohy. Kliknutím na **tlačítko OK** zavřete **vlastnosti**úlohy.

   > [!NOTE]  
   > Pro **Odstranit staré zprávy o stavu**nastavíte stáří dat, která se mají odstranit při nastavení pravidel filtru zpráv.  

5. Chcete-li povolit nebo zakázat úkol bez úprav vlastností úlohy, klikněte na tlačítko **Povolit** nebo **Zakázat** . Popisek tlačítka se změní v závislosti na aktuální konfiguraci úlohy.  
6. Po dokončení konfigurace úloh údržby kliknutím na **tlačítko OK** dokončete postup.

## <a name="next-steps"></a>Další kroky

[Referenční informace k úlohám údržby](reference-for-maintenance-tasks.md)
