---
title: Verze Technical Preview
titleSuffix: Configuration Manager
description: Přečtěte si o větvi Technical Preview, která vám umožní testovat nové funkce a funkce v Configuration Manager.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfcdd74b7b5c31e3f3ab6bb38a7ea96de9d05eec
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905143"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

Tento článek poskytuje podrobné informace o Configuration Manager měsíční verze Technical Preview. Technical Preview přináší nové funkce, na kterých Microsoft pracuje. Zavádí nové funkce, které ještě nejsou zahrnuté v aktuální větvi Configuration Manager. Tyto funkce mohou být nakonec zahrnuty do aktualizace aktuální větve. Než dokončíme funkce, chceme si je vyzkoušet a poskytnout nám svůj názor.

Vzhledem k tomu, že tato verze je Technical Preview, mohou se podrobnosti a funkce změnit.

Tyto informace se vztahují na všechny verze větve Configuration Manager Technical Preview. V tomto článku jsou uvedeny všechny nové funkce společně s verzí Technical Preview, ve které se poprvé zobrazí. Například verze **2001** pro leden ( `01` ) z 2020 ( `20` ). Samostatné články vyhrazené pro jednotlivé verze Preview podrobně popisují jednotlivé funkce.

Informace o novinkách v *aktuální větvi* Configuration Manager najdete v tématu [novinky v Configuration Manager přírůstkových verzích](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS:`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a>Požadavky a omezení

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

## <a name="install-and-update"></a><a name="bkmk_install"></a>Nainstalovat a aktualizovat

Větev Configuration Manager Technical Preview pro použití v testovacím prostředí je odlišná od Configuration Manager aktuální větve pro produkční použití.

Nejdřív nainstalujte základní verzi větve Technical Preview. Po instalaci základní verze pak pomocí konzolových aktualizací nainstalujte nejnovější verzi Preview do aktuálního stavu. Nové verze Technical Preview jsou obvykle k dispozici každý měsíc.

Microsoft podporuje každou verzi Technical Preview až do doby, kdy jsou k dispozici tři po sobě jdoucí verze. Například pokud verze 1908 byla vydána, verze 1904 již není podporována. Verze 1905, 1906 a 1907 zůstaly v podpoře. Pokud je základní plán mimo podporu, je stále podporován pro instalaci nového webu Technical Preview, za předpokladu, že okamžitě aktualizujete na podporovanou verzi. Starší základní hodnoty jsou podporovány, dokud není k dispozici nová základní verze. Aktualizujte na nejnovější dostupnou verzi ze směrného plánu a pak opakujte proces aktualizace, dokud nenainstalujete nejnovější verzi Technical Preview.

> [!TIP]
> Když nainstalujete aktualizaci Technical Preview, aktualizujete svou instalaci Preview na tuto novou verzi Technical Preview. Instalace Technical Preview nemá nikdy možnost upgradovat na instalaci aktuální větve. Také nikdy nepřijímá aktualizace z verze aktuální větve.
>
> V průběhu jednoho roku existuje větev Technical Preview a verze aktuální větve se stejným číslem verze. Například verze Technical Preview 1910 a aktuální větev verze 1910.

### <a name="active-baseline-versions"></a>Aktivní základní verze

Nainstalujte základní verzi po dobu až jednoho roku po jejím vydání. Při instalaci nového webu Technical Preview použijte nejnovější základní verzi.

- **Technical Preview verze 2002**: větev Configuration Manager Technical preview verze 2002 je k dispozici jako aktualizace v konzole i jako nová základní verze.

Stáhněte si základní verzi z [centra hodnocení](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a>Poskytnutí zpětné vazby

Rádi uslyšíme váš názor na nové funkce ve verzi Technical Preview. Další informace najdete v tématu o [zpětné vazbě produktu](../understand/find-help.md#product-feedback).

Pokud máte nějaké nápady k novým funkcím, které byste chtěli zobrazit, dejte nám prosím jistotu. Zasílejte nové nápady a hlasovat o nápadech podle dalších uživatelů: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a>Funkce v nejnovější verzi

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2003.md) <!--ID-->

V nejnovější verzi Configuration Manager Technical Preview jsou k dispozici následující funkce:

### <a name="technical-preview-version-2004"></a>Technical Preview verze 2004

- [Připojení tenanta Microsoft Endpoint Manageru: podrobnosti o klientovi ConfigMgr](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [Oznámení od Microsoftu](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [Kopírovat data zjišťování z konzoly](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [Vylepšení CMPivot](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [Podpora pro PowerShell verze 7](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [Vylepšení formátování a rozdělení disku na oddíly pořadí úkolů](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [Pravidla přehledu správy pro nasazení operačního systému](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [Rutiny PowerShellu pro typy nasazení pořadí úloh](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

> [!NOTE]
> Funkce, které byly k dispozici v předchozí verzi Technical Preview, zůstávají dostupné v novějších verzích. Podobně funkce, které jsou přidány do Configuration Manager aktuální větve, zůstávají dostupné ve větvi Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Funkce v posledních technických náhledech

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Následující funkce byly vydány s předchozími verzemi větve Configuration Manager Technical Preview od aktuální větve verze 2002:

> [!TIP]
> Když je k dispozici nová verze aktuální větve, funkce, které jsou v této verzi k dispozici, jsou uvedeny v článku *co je nového* . Další informace najdete v tématu [co je nového v přírůstkových verzích](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2003"></a>Technical Preview verze 2003

- [Připojení klientů Configuration Manager ke službě Microsoft Defender ATP prostřednictvím konzoly Microsoft Endpoint Manager](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Sledování oprav položek konfigurace](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Zobrazit skupiny hranic pro zařízení](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Průvodce novou zpětnou vazbou](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Vylepšení řídicího panelu Microsoft Edge Management](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Vylepšení CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Dotaz na zpětnou vazbu odeslanou společnosti Microsoft](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Nová metoda SDK pro průběh pořadí úloh](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Vylepšení nasazení operačního systému](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>Funkce v předchozích technických náhledech

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Následující funkce byly vydány s předchozími verzemi větve Configuration Manager Technical Preview. Tyto funkce zůstanou dostupné v novějších verzích, ale ještě nejsou k dispozici v aktuální větvi.

| Funkce        | Verze Technical Preview |
|----------------|---------------------------|
| Připojit soubory k názoru <!--3556011--> | [Verze Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Vylepšení distribučních bodů s povoleným vícesměrovým vysíláním <!--3785535--> | [Verze Tech Preview 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Šablony postupného nasazení <!--4961086--> | [Verze Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Vzdálené řízení kdekoli pomocí brány pro správu cloudu <!--4575930--> | [Verze Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Vylepšení Centrum komunity <!--3555935--> | [Verze Tech Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Vylepšení Centrum komunity <!--4224401--> | [Verze Tech Preview 1905](2019/technical-preview-1905.md#bkmk_hub) |
| Centrum komunity a GitHub <!--3555935--> | [Verze Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Cloud Services – náklady Estimator <!--3555774--> | [Verze Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Stažení sestav z Centrum komunity <!--3555936--> | [Verze Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Centrum komunity <!--3556020, fka 1357766--> | [Verze Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
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
