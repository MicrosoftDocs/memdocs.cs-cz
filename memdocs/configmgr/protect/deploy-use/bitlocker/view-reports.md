---
title: Zobrazení sestav nástroje BitLocker
titleSuffix: Configuration Manager
description: Další informace o sestavách správy nástroje BitLocker v Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d10717f980922e1f6d1fca9224e288b4df709da2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717353"
---
# <a name="view-bitlocker-reports"></a>Zobrazení sestav nástroje BitLocker

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Po [instalaci sestav](setup-websites.md) v bodu služby Reporting Services můžete zobrazit sestavy. Sestavy ukazují dodržování předpisů BitLockeru pro podniky a pro jednotlivá zařízení. Poskytují tabulkové informace a grafy a filtry, které umožňují zobrazit data z různých perspektiv.

V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte uzel **sestavy** . V kategorii **Správa BitLockeru** jsou následující sestavy:

- [Kompatibilita počítačů s nástrojem BitLocker](#bkmk-compliancereport)

- [Řídicí panel dodržování předpisů v Enterprise BitLockeru](#bkmk-dashboard)

- [Podrobnosti o kompatibilitě Enterprise BitLockeru](#bkmk-compliancedetails)

- [Shrnutí kompatibility Enterprise nástroje BitLocker](#bkmk-compliancesummary)

- [Sestava auditu obnovení](#bkmk-audit)

Ke všem těmto sestavám můžete přistupovat přímo z webu bodu služby Reporting Services.

> [!NOTE]
> Pro tyto sestavy zobrazíte kompletní data:
>
> - Vytvoření a nasazení zásad správy BitLockeru do kolekce zařízení
> - Klienti v cílové kolekci potřebují odesílat inventář hardwaru

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a>Kompatibilita počítačů s nástrojem BitLocker

Pomocí této sestavy můžete shromažďovat informace, které jsou specifické pro určitý počítač. Poskytuje podrobné informace o šifrování pro jednotku operačního systému a všechny pevné datové jednotky. Chcete-li zobrazit podrobnosti o jednotlivých jednotkách, rozbalte položku název počítače. Označuje také zásadu, která se použije u každého typu jednotky v počítači.

[![Příklad obrazovky sestavy dodržování předpisů pro počítače BitLockeru](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

Pomocí této sestavy můžete také určit poslední známý stav šifrování BitLockeru u ztracených nebo odcizených počítačů. Configuration Manager určuje dodržování předpisů pro zařízení na základě zásad BitLockeru, které nasadíte. Předtím, než se pokusíte určit stav šifrování BitLockeru zařízení, ověřte zásady, které jste do něj nasadili.

> [!NOTE]
> Tato sestava nezobrazuje stav šifrování svazku vyměnitelného data.

### <a name="computer-details"></a>Podrobnosti o počítači

|Název&nbsp;sloupce|Popis|
|----------------|----|
|Název počítače|Název počítače DNS zadaného uživatelem.|
|Název domény|Plně kvalifikovaný název domény počítače.|
|Typ počítače|Typ počítače, platné typy jsou **nepřenosné** a **přenosné**.|
|Operační systém|Typ operačního systému počítače.|
|Celkové dodržování předpisů|Celkový stav dodržování předpisů BitLockerem počítače. Platné stavy jsou **kompatibilní** a **nekompatibilní**. [Stav dodržování předpisů na jednotku](#bkmk_volume) může označovat odlišné stavy dodržování předpisů. Toto pole však reprezentuje stav dodržování předpisů ze zadaných zásad.|
|Dodržování předpisů pro operační systém|Stav dodržování předpisů operačního systému v počítači. Platné stavy jsou **kompatibilní** a **nekompatibilní**.|
|Dodržování předpisů s pevnými datovými jednotkami|Stav dodržování předpisů u pevné datové jednotky v počítači. Platné stavy jsou **kompatibilní** a **nekompatibilní**.|
|Datum poslední aktualizace|Datum a čas, kdy počítač naposledy kontaktoval server, aby nahlásil stav dodržování předpisů.|
|Výjimky|Určuje, jestli je uživatel v zásadách BitLockeru osvobozený od daně nebo není vyloučený.|
|Vyloučený uživatel|Uživatel, který je vyloučený ze zásad nástroje BitLocker.|
|Datum výjimky|Datum, kdy byla výjimka udělena.|
|Podrobnosti o stavu dodržování předpisů|Chybové a stavové zprávy o stavu dodržování předpisů počítače ze zadaných zásad.|
|Síla šifrování zásad|Síla šifry, kterou jste vybrali v zásadách správy BitLockeru.|
|Zásady: jednotka operačního systému|Určuje, zda je pro jednotku operačního systému a odpovídající typ ochrany vyžadováno šifrování.|
|Zásada: pevná datová jednotka|Určuje, zda je pro pevnou datovou jednotku vyžadováno šifrování.|
|Výrobce|Název výrobce počítače, jak se zobrazuje v počítači BIOS.|
|Model|Název modelu výrobce počítače, jak se zobrazuje v počítači BIOS.|
|Uživatelé zařízení|Známé uživatele v počítači.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a>Svazek počítače

|Název&nbsp;sloupce|Popis|
|----------------|----|
|Písmeno jednotky|Písmeno jednotky v počítači.|
|Typ jednotky|Typ jednotky Platné hodnoty jsou **jednotka operačního systému** a **pevná datová jednotka**. Tyto položky jsou fyzické jednotky namísto logických svazků.|
|Síla šifry|Síla šifry, kterou jste vybrali během v zásadách správy BitLockeru.|
|Typy ochrany|Typ ochrany, kterou jste vybrali v zásadě k zašifrování jednotky. Platnými typy ochrany pro jednotku s operačním systémem jsou **TPM** nebo **TPM + PIN**. Platný typ ochrany pro pevný datový disk je **heslo**.|
|Stav ochrany|Indikuje, že počítač povolil typ ochrany zadaný v zásadě. Platné stavy jsou **zapnuté** nebo **vypnuté**.|
|Stav šifrování|Stav šifrování jednotky. Platné stavy jsou **šifrované**, **nešifrované**nebo **zašifrování**.|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a>Řídicí panel dodržování předpisů v Enterprise BitLockeru

Tato sestava obsahuje následující grafy, které znázorňují stav dodržování předpisů BitLockeru napříč vaší organizací:

- Distribuce stavu dodržování předpisů

- Nekompatibilní distribuce – distribuce chyb

- Distribuce stavu dodržování předpisů podle typu jednotky

[![Příklad obrazovky řídicího panelu kompatibility Enterprise nástroje BitLocker](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>Distribuce stavu dodržování předpisů

Tento výsečový graf zobrazuje stav dodržování předpisů pro počítače v organizaci. Zobrazuje také procento počítačů s tímto stavem dodržování předpisů ve srovnání s celkovým počtem počítačů ve vybrané kolekci. Zobrazí se také skutečný počet počítačů s jednotlivými stavy.

Výsečový graf zobrazuje následující stavy dodržování předpisů:

- Odpovídající

- Neodpovídající

- Výjimka uživatele

- Dočasné vyloučení uživatele

- Zásady nejsou vynutily.

- Neznámý. Tyto počítače oznámily chybu stavu nebo jsou součástí kolekce, ale jejich stav dodržování předpisů nikdy neohlásil. Pokud je počítač odpojen od organizace, může dojít k nedostatku stavu dodržování předpisů.

### <a name="non-compliant---errors-distribution"></a>Nekompatibilní distribuce – distribuce chyb

Tento výsečový graf zobrazuje kategorie počítačů ve vaší organizaci, které nejsou kompatibilní se zásadami nástroj BitLocker Drive Encryption. Zobrazuje také počet počítačů v jednotlivých kategoriích. Sestava vypočítá všechny procentuální hodnoty z celkového počtu neodpovídajících počítačů v kolekci.

- Uživatelem odložení šifrování

- Nepovedlo se najít kompatibilní čip TPM.

- Systémový oddíl není k dispozici nebo je dostatečně velký

- ČIP TPM je viditelný, ale není inicializovaný.

- Konflikt zásad

- Čekání na Automatické zřizování čipu TPM

- Došlo k neznámé chybě.

- Žádné informace. Tyto počítače nemají nainstalovaného agenta pro správu nástroje BitLocker nebo jsou nainstalovány, ale nejsou aktivovány. Například služba nefunguje.

### <a name="compliance-status-distribution-by-drive-type"></a>Distribuce stavu dodržování předpisů podle typu jednotky

Tento pruhový graf znázorňuje aktuální stav dodržování předpisů BitLockerem podle typu jednotky. Stavy jsou **kompatibilní** a **nekompatibilní**. Pro pevné datové jednotky a jednotky operačního systému se zobrazí pruhy. Sestava zahrnuje počítače bez pevné datové jednotky a na panelu **jednotky operačního systému** zobrazí pouze hodnotu. Graf neobsahuje uživatele, kterým byla udělena výjimka ze zásady nástroj BitLocker Drive Encryption nebo kategorie bez zásad.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a>Podrobnosti o kompatibilitě Enterprise BitLockeru

Tato sestava obsahuje informace o celkovém dodržování předpisů BitLockerem v celé organizaci pro kolekci počítačů, do kterých jste nasadili zásady správy BitLockeru.

[![Příklad obrazovky s podrobnostmi o kompatibilitě nástroje BitLocker Enterprise](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|Název sloupce|Popis|
|--- |--- |
|Spravované počítače|Počet počítačů, do kterých jste nasadili zásadu správy BitLockeru.|
|% Vyhovující|Procento odpovídajících počítačů v organizaci.|
|% Neodpovídajících|Procento počítačů, které nedodržují předpisy v organizaci|
|% Neznámé dodržování předpisů|Procento počítačů se stavem dodržování předpisů, které není známo.|
|% Vyloučení|Procento počítačů vyjmutých z požadavku na šifrování BitLockeru|
|% Bez výjimky|Procento počítačů, které nejsou vyjmuty z požadavku na šifrování BitLockeru.|
|Odpovídající|Počet odpovídajících počítačů v organizaci.|
|Nevyhovující předpisům|Počet počítačů, které nedodržují předpisy, v organizaci.|
|Neznámé dodržování předpisů|Počet počítačů se stavem dodržování předpisů, které nejsou známy.|
|Kontroly|Počet počítačů, které jsou vyjmuty z požadavku šifrování BitLockeru.|
|Bez výjimky|Počet počítačů, které nejsou vyjmuty z požadavku na šifrování BitLockeru.|

### <a name="computer-details"></a>Podrobnosti o počítači

|Název sloupce|Popis|
|--- |--- |
|Název počítače|Název počítače DNS spravovaného zařízení.|
|Název domény|Plně kvalifikovaný název domény počítače.|
|Stav dodržování předpisů|Celkový stav dodržování předpisů počítače Platné stavy jsou **kompatibilní** a **nekompatibilní**.|
|Výjimky|Určuje, jestli je uživatel v zásadách BitLockeru osvobozený od daně nebo není vyloučený.|
|Uživatelé zařízení|Uživatelé zařízení.|
|Podrobnosti o stavu dodržování předpisů|Chybové a stavové zprávy o stavu dodržování předpisů počítače ze zadaných zásad.|
|Poslední kontakt|Datum a čas, kdy počítač naposledy kontaktoval server, aby nahlásil stav dodržování předpisů.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a>Shrnutí kompatibility Enterprise nástroje BitLocker

Pomocí této sestavy můžete zobrazit celkové dodržování předpisů BitLockeru napříč vaší organizací. Zobrazuje také dodržování předpisů pro jednotlivé počítače, do kterých jste nasadili zásady správy BitLockeru.

[![Příklad obrazovky souhrnu kompatibility Enterprise nástroje BitLocker](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|Název sloupce|Popis|
|--- |--- |
|Spravované počítače|Počet počítačů, které spravujete pomocí zásad BitLockeru.|
|% Vyhovující|Procento odpovídajících počítačů ve vaší organizaci.|
|% Neodpovídajících|Procento nekompatibilních počítačů ve vaší organizaci.|
|% Neznámé dodržování předpisů|Procento počítačů se stavem dodržování předpisů, které není známo.|
|% Vyloučení|Procento počítačů vyjmutých z požadavku na šifrování BitLockeru|
|% Bez výjimky|Procento počítačů, které nejsou vyjmuty z požadavku na šifrování BitLockeru.|
|Odpovídající|Počet odpovídajících počítačů ve vaší organizaci.|
|Neodpovídající|Počet neodpovídajících počítačů ve vaší organizaci.|
|Neznámé dodržování předpisů|Počet počítačů se stavem dodržování předpisů, které nejsou známy.|
|Kontroly|Počet počítačů, které jsou vyjmuty z požadavku šifrování BitLockeru.|
|Bez výjimky|Počet počítačů, které nejsou vyjmuty z požadavku na šifrování BitLockeru.|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a>Sestava auditu obnovení

> [!NOTE]
> Tato sestava je k dispozici také na [webu Správa a monitorování nástroje BitLocker](helpdesk-portal.md#reports).
>
> Chcete-li zobrazit tuto sestavu v konzole Configuration Manager, přejdete do pracovního prostoru **monitorování** . V navigačním podokně rozbalte uzel **vytváření sestav** , rozbalte položku **sestavy**a poté rozbalte složku **Správa nástroje BitLocker** . Vyberte podsložku pro lokalizovanou verzi sestavy, například **en-US**.

Pomocí této sestavy můžete auditovat uživatele, kteří požadovali přístup k klíčům pro obnovení BitLockeru. Filtrovat můžete podle následujících kritérií:

- Konkrétní typ uživatele, například uživatel oddělení technické podpory nebo koncový uživatel
- Pokud se žádost nezdařila nebo byla úspěšná
- Konkrétní typ požadovaného klíče: heslo obnovovacího klíče, ID obnovovacího klíče nebo hodnota hash hesla čipu TPM
- Rozsah dat, během kterého došlo k načtení

[![Ukázkový snímek sestavy auditu pro obnovení BitLockeru](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|Název&nbsp;sloupce|Popis|
|----------------|----|
|Datum a čas požadavku|Datum a čas, kdy koncový uživatel nebo uživatel Helpdesk požádal o klíč.|
|Zdroj žádosti o audit|Lokalita, ze které pochází požadavek. Platné hodnoty jsou **Samoobslužný portál** nebo **Helpdesk**.|
|Výsledek žádosti|Stav požadavku Platné hodnoty jsou **úspěšné** nebo **neúspěšné**.|
|Uživatel helpdesku|Administrativní uživatel, který si vyžádal klíč Pokud správce helpdesku obnoví klíč bez zadání uživatelského jména, pole **koncového uživatele** je prázdné. Standardní uživatel technické podpory musí zadat uživatelské jméno, které se zobrazí v tomto poli. Pro obnovení prostřednictvím samoobslužného portálu se v tomto poli a v poli **koncový uživatel** zobrazuje jméno uživatele, který požadavek odeslal.|
|koncový uživatel|Jméno uživatele, který požadoval načtení klíče.|
|Počítač|Název počítače, který se obnovil.|
|Typ klíče|Typ klíče, který uživatel požadoval Existují tři typy klíčů:<br/><br/>- **Heslo obnovovacího klíče**: používá se k obnovení počítače v režimu obnovení.<br/>- **ID obnovovacího klíče**: používá se k obnovení počítače v režimu obnovení pro jiného uživatele.<br/>- **Hodnota hash hesla TPM**: používá se k obnovení počítače s UZAMČENÝM čipem TPM.|
|Popis důvodu|Proč uživatel požadoval zadaný typ klíče na základě možnosti, kterou vybrali ve formuláři.|
