---
title: Verze Technical Preview
titleSuffix: Configuration Manager
description: Přečtěte si o větvi Technical Preview, která vám umožní testovat nové funkce a funkce v Configuration Manager.
ms.date: 09/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a27cd1e7a28b52ccc224f965b678d7d578be75eb
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081735"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

Tento článek poskytuje podrobné informace o Configuration Manager měsíční verze Technical Preview. Technical Preview přináší nové funkce, na kterých Microsoft pracuje. Zavádí nové funkce, které ještě nejsou zahrnuté v aktuální větvi Configuration Manager. Tyto funkce mohou být nakonec zahrnuty do aktualizace aktuální větve. Než dokončíme funkce, chceme si je vyzkoušet a poskytnout nám svůj názor.

Vzhledem k tomu, že tato verze je Technical Preview, mohou se podrobnosti a funkce změnit.

Tyto informace se vztahují na všechny verze větve Configuration Manager Technical Preview. V tomto článku jsou uvedeny všechny nové funkce společně s verzí Technical Preview, ve které se poprvé zobrazí. Například verze **2001** pro leden ( `01` ) z 2020 ( `20` ). Samostatné články vyhrazené pro jednotlivé verze Preview podrobně popisují jednotlivé funkce.

Informace o novinkách v *aktuální větvi* Configuration Manager najdete v tématu [novinky v Configuration Manager přírůstkových verzích](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> Požadavky a omezení

> [!IMPORTANT]
> Verze Technical Preview je licencovaná jenom pro použití v testovacím prostředí. Společnost Microsoft nemusí poskytovat služby podpory a některé funkce nemusí být k dispozici v technických náhledech. Kromě toho software Technical Preview může mít nižší nebo jiné standardy zabezpečení, ochrany osobních údajů, usnadnění přístupu, dostupnosti a spolehlivosti, které se vztahují k komerčně poskytovanému softwaru.

U většiny požadavků produktu použijte informace v [podporovaných konfiguracích](../plan-design/configs/supported-configurations.md). Následující výjimky se vztahují na větev Technical Preview:

- Každá instalace je aktivní po dobu 90 dnů, než se aktivuje jako neaktivní.

- Jediným podporovaným jazykem je angličtina.

- Podporuje jenom tyto parametry příkazového řádku pro instalaci:

  - `/silent`
  - `/testdbupgrade`

- Spojovací bod služby se nainstaluje do online režimu. Nepodporuje offline režim.

- Samostatné články pro každou konkrétní verzi Technical Preview zahrnují další omezení nebo požadavky, které jsou k dispozici.

- Ve větvi Technical Preview nejsou podporovány následující funkce:

  - [Migrace](../migration/migrate-data-between-hierarchies.md) do této větve verze Preview nebo z ní.

  - [Upgradujte](../servers/deploy/install/upgrade-to-configuration-manager.md) na tuto větev verze Preview.

  - [Site Recovery](../servers/manage/recover-sites.md) z poslední složky CD.<!--507106-->

- Neexistuje žádná podpora pro aktualizaci aktuální větve z této větve verze Preview.

    > [!Note]
    > Když jsou aktualizace dostupné pro verzi Preview, najdete je a nainstalujete z uzlu **aktualizace a údržba** konzoly Configuration Manager. Video o procesu upgradu v konzole najdete v tématu [Instalace balíčků aktualizací Configuration Manager](https://www.youtube.com/embed/KBd_EGFbUT8) v YouTube.com.

- Podporuje pouze samostatnou primární lokalitu. Neexistuje žádná podpora pro lokalitu centrální správy, pro několik primárních lokalit ani pro sekundární lokality.

Větev Technical Preview Configuration Manager podporuje následující produkty a technologie:

- Pokud není uvedeno jinak, větev Technical Preview podporuje stejné verze SQL Server jako aktuální větev. Další informace najdete v tématu [podporované verze SQL Server](../plan-design/configs/support-for-sql-server-versions.md).

- Lokalita podporuje až 10 klientů, ve kterých se dá spustit libovolná [podporovaná verze operačního systému klienta](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> Zahrnutí těchto produktů do tohoto obsahu neznamená rozšíření podpory verze, která přesahuje životní cyklus podpory. Configuration Manager nepodporuje produkty, které přesahují životní cyklus podpory. Další informace najdete v tématu [Zásady životního cyklu Microsoftu](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a> Nainstalovat a aktualizovat

Větev Configuration Manager Technical Preview pro použití v testovacím prostředí je odlišná od Configuration Manager aktuální větve pro produkční použití.

Nejdřív nainstalujte základní verzi větve Technical Preview. Po instalaci základní verze pak pomocí konzolových aktualizací nainstalujte nejnovější verzi Preview do aktuálního stavu. Nové verze Technical Preview jsou obvykle k dispozici každý měsíc.

Microsoft podporuje každou verzi Technical Preview až do doby, kdy jsou k dispozici tři po sobě jdoucí verze. Například pokud verze 1908 byla vydána, verze 1904 již není podporována. Verze 1905, 1906 a 1907 zůstaly v podpoře. Pokud je základní plán mimo podporu, je stále podporován pro instalaci nového webu Technical Preview, za předpokladu, že okamžitě aktualizujete na podporovanou verzi. Starší základní hodnoty jsou podporovány, dokud není k dispozici nová základní verze. Aktualizujte na nejnovější dostupnou verzi ze směrného plánu a pak opakujte proces aktualizace, dokud nenainstalujete nejnovější verzi Technical Preview.

> [!TIP]
> Když nainstalujete aktualizaci Technical Preview, aktualizujete svou instalaci Preview na tuto novou verzi Technical Preview. Instalace Technical Preview nemá nikdy možnost upgradovat na instalaci aktuální větve. Také nikdy nepřijímá aktualizace z verze aktuální větve.
>
> V průběhu jednoho roku existuje větev Technical Preview a verze aktuální větve se stejným číslem verze. Například verze Technical Preview 1910 a aktuální větev verze 1910.

### <a name="active-baseline-versions"></a>Aktivní základní verze

Nainstalujte základní verzi po dobu až jednoho roku po jejím vydání. Při instalaci nového webu Technical Preview použijte nejnovější základní verzi. Následující verze Configuration Manager verze Technical Preview jsou k dispozici jako konzolové aktualizace i jako nové základní verze:

- **Technical Preview verze 2007**

Stáhněte si základní verzi z [centra hodnocení](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> Poskytnutí zpětné vazby

Rádi uslyšíme váš názor na nové funkce ve verzi Technical Preview. Další informace najdete v tématu o [zpětné vazbě produktu](../understand/find-help.md#product-feedback).

Pokud máte nějaké nápady k novým funkcím, které byste chtěli zobrazit, dejte nám prosím jistotu. Zasílejte nové nápady a hlasovat o nápadech podle dalších uživatelů: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> Funkce v nejnovější verzi

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2009.md) <!--ID-->

V nejnovější verzi Configuration Manager Technical Preview jsou k dispozici následující funkce:

### <a name="technical-preview-version-2009"></a>Technical Preview verze 2009

- [Brána pro správu cloudu se sadou škálování virtuálních počítačů](2020/technical-preview-2009.md#bkmk_cmgvmss) <!--3601040-->
- [Vylepšení vzdáleného řízení](2020/technical-preview-2009.md#bkmk_remctrl) <!--4575930-->
- [Nasazení operačního systému přes CMG pomocí spouštěcího média](2020/technical-preview-2009.md#bkmk_osdcmg) <!--3555923-->
- [Zobrazení vztahů shromažďování](2020/technical-preview-2009.md#bkmk_coll) <!--3608121-->
- [Vybudit počítač v konečném termínu nasazení pomocí probuzení z partnerského zařízení](2020/technical-preview-2009.md#bkmk_wol) <!--3734819-->
- [Vylepšení oznámení v konzole](2020/technical-preview-2009.md#bkmk_notifications) <!--7410221-->
- [Oznámení pro zařízení, která už nezískávají aktualizace](2020/technical-preview-2009.md#bkmk_patch) <!--7520646-->
- [Vylepšené možnosti restartování Windows serveru pro účty bez oprávnění správce](2020/technical-preview-2009.md#bkmk_server) <!--7821529-->
- [Vylepšení nasazení operačního systému](2020/technical-preview-2009.md#bkmk_osd) <!--7799892,7068388-->

> [!NOTE]
> Funkce, které byly k dispozici v předchozí verzi Technical Preview, zůstávají dostupné v novějších verzích. Podobně funkce, které jsou přidány do Configuration Manager aktuální větve, zůstávají dostupné ve větvi Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Funkce v posledních technických náhledech

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Následující funkce byly vydány s předchozími verzemi větve Configuration Manager Technical Preview od aktuální větve verze 2006:

> [!TIP]
> Když je k dispozici nová verze aktuální větve, funkce, které jsou v této verzi k dispozici, jsou uvedeny v článku *co je nového* . Další informace najdete v tématu [co je nového v přírůstkových verzích](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2008"></a>Technical Preview verze 2008

- [Náhled dotazu na kolekci](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [Analýza chyb SetupDiag pro aktualizace funkcí](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Monitorování stavu scénáře](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Zobrazení vyhodnocení kolekce](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [Zobrazení velikosti pořadí úloh v konzole nástroje](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Úloha odstranění starých shromážděných diagnostických souborů](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Importovat objekty do aktuální složky](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

### <a name="technical-preview-version-2007"></a>Technical Preview verze 2007

- [Připojení tenanta: zobrazení inventáře hardwaru v centru pro správu Microsoft Endpoint Manageru](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Vylepšení řídicího panelu zdrojů dat klienta](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [V některých oblastech konzoly se teď používá písmo s pevnou šířkou.](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Správa velikosti zásad pořadí úloh](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Vylepšení časové osy zařízení v centru pro správu](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>Funkce v předchozích technických náhledech

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Následující funkce byly vydány s předchozími verzemi větve Configuration Manager Technical Preview. Tyto funkce zůstanou dostupné v novějších verzích, ale ještě nejsou k dispozici v aktuální větvi.

| Příznak        | Verze Technical Preview |
|----------------|---------------------------|
| Vylepšení dostupných aplikací prostřednictvím CMG <!--7033501--> | [Verze Tech Preview 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Připojení tenanta: spuštění skriptů z centra pro správu <!--6234688--> | [Verze Tech Preview 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Vylepšení rutin brány pro správu cloudu <!--6978300--> | [Verze Tech Preview 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Nahlášení selhání při instalaci a upgradu do Microsoftu <!--5622909--> | [Verze Tech Preview 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| Vylepšení nástroje pro vyčištění knihovny obsahu <!--6887878--> | [Verze Tech Preview 2005](2020/technical-preview-2005.md#bkmk_content) |
| Kopírovat data zjišťování z konzoly <!--6890051--> | [Verze Tech Preview 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| Podpora pro PowerShell verze 7 <!--6023299--> | [Verze Tech Preview 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| Průvodce novou zpětnou vazbou <!--3180826--> | [Verze Tech Preview 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Dotaz na zpětnou vazbu odeslanou společnosti Microsoft <!--6488450--> | [Verze Tech Preview 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Připojit soubory k názoru <!--3556011--> | [Verze Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Vylepšení distribučních bodů s povoleným vícesměrovým vysíláním <!--3785535--> | [Verze Tech Preview 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Šablony postupného nasazení <!--4961086--> | [Verze Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Vzdálené řízení kdekoli pomocí brány pro správu cloudu <!--4575930--> | [Verze Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Cloud Services – náklady Estimator <!--3555774--> | [Verze Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Služba respondérů technologie PXE založená na klientovi <!--3556018, fka 1357148--> | [Verze Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Podpora spouštění sítě PXE pro protokol IPv6 <!--3601254, fka 1269793--> |[Verze Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Použití Azure Active Directory <!--3607315, fka 1322145--> | [Verze Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Vylepšení funkce Asset Intelligence <!--3601024, fka 1307390--> | [Verze Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Viz také

Další informace najdete v následujících článcích:

- [Hodnocení nástroje Configuration Manager v testovacím prostředí](evaluate-with-lab-environment.md)
- [Co je nového v přírůstkových verzích nástroje Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Úvod do nástroje Configuration Manager](../understand/introduction.md)

> [!Tip]
> Další informace o funkcích aktuální větve, které vyžadují souhlas s povolením, najdete v tématu [předběžné verze funkcí](../servers/manage/pre-release-features.md).
>
> Další informace o funkcích aktuální větve, které musíte nejdřív povolit, najdete v tématu [Povolení volitelných funkcí z aktualizací](../servers/manage/install-in-console-updates.md#bkmk_options).
