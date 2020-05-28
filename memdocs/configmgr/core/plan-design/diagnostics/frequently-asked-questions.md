---
title: Nejčastější dotazy týkající se diagnostiky a dat o využití
titleSuffix: Configuration Manager
description: Nejčastější dotazy týkající se dat o využití a diagnostiky pro Configuration Manager
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709541"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Nejčastější dotazy týkající se dat o využití a diagnostiky

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje odpovědi na nejčastější dotazy týkající se dat o využití a diagnostiky v Configuration Manager.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a>Můžu vypnout diagnostiku a data o využití?

Chcete-li spravovat, kdy lokalita odesílá data, použijte spojovací bod služby v režimu offline. Pak pomocí nástroje pro připojení služby ručně odešlete data. Další informace najdete v následujících článcích:

- [O spojovacím bodu služby](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Použití nástroje pro připojení služby](../../servers/manage/use-the-service-connection-tool.md)

Pro podporu nových verzí Windows 10 a cloudových služeb, jako je Microsoft Intune, je potřeba pravidelně aktualizovat aktuální větev Configuration Manager. Microsoft vyžaduje aspoň základní úroveň diagnostických dat a dat o využití. Tato data se používají k udržení aktuálního produktu v aktuálním stavu, zlepšení možností aktualizace a zlepšení kvality a zabezpečení produktu.

Do služby se neodesílají žádná data, když je spojovací bod služby v režimu offline. Když přepnete do online režimu nebo použijete nástroj pro připojení služby, pošle služba data službě, aby kontrolovala aktualizace.

Můžete také zvolit úroveň dat, která Configuration Manager shromažďuje. Další informace najdete v tématu [úrovně diagnostických dat o využití](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a>Jaká je doba uchovávání dat?

Microsoft ukládá data o využití a diagnostiku Configuration Manager po dobu jednoho roku.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a>Odesílají se data o využití a diagnostika při spuštění instalačního programu?

No. Data o využití a diagnostika se odesílají, až když je lokalita nainstalovaná a funkční.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a>Jak často se data odesílají?

Uložené procedury SQL se spouštějí každých sedm dní od data instalace lokality.

- V online režimu spojovací bod služby nahraje data po spuštění dotazů.

- V offline režimu můžete k nahrání dat použít nástroj pro připojení služby. (Data nejsou zpočátku k dispozici pro použití v režimu offline až sedm dní po instalaci lokality.)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a>Můžou se data použít k vytvoření mapy sítě?

No. Tato data neobsahují žádné podrobnosti o síti, jako jsou IP adresy nebo podrobné geografické informace. Další informace najdete v tématu [úrovně diagnostických dat o využití](levels-overview.md#bkmk_versions)a další podrobnosti o verzi, kterou používáte.

Data obsahují informace o časovém pásmu z každé lokality. Tyto informace mohou poskytnout přehled o širokém geografickém umístění a globální rozptýlení lokalit v hierarchii.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a>Můžete zobrazit data ve vlastních tabulkách SQL?

No. Configuration Manager shromažďuje data o využití a diagnostiku prostřednictvím uložených procedur SQL. Tyto uložené procedury jsou spouštěny s výchozími tabulkami produktů v databázi. Všechny tyto tabulky SQL jsou s předponou **TEL_**. Jako součást dotazu SQL na zjištění schématu jsou všechny názvy tabulek zakódovány pomocí algoritmu hash pro porovnání se známými výchozími hodnotami. Toto chování určuje, že vlastní tabulky v databázi existují. Přítomnost vlastních tabulek informuje společnost Microsoft o tom, že jste rozšířili schéma databáze z výchozího nastavení. Neobsahuje žádná data uložená v těchto tabulkách.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a>Vidíte další databáze?

No. Uložené procedury pro shromažďování dat jsou omezeny na databázi lokality Configuration Manager. Společnost Microsoft nemůže zobrazit názvy jiných databází ani žádná data v jiných databázích.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a>Odesílají se všechna data do jiných integrovaných cloudových služeb?

Ano, při integraci těchto služeb s Configuration Manager. V rámci interakce s jakoukoli cloudovou službou Configuration Manager odesílá data do této služby. Tato data jsou specifická pro danou cloudovou službu a jsou oddělená od Configuration Manager Diagnostika a dat o využití. Další informace o konkrétních datech používaných v interakci s jinou cloudovou službou najdete v dokumentaci k této službě.

Například následující cloudové služby jsou součástí Microsoft Endpoint Manageru:

- [Ochrana osobních údajů v datech Desktop Analytics](../../../desktop-analytics/privacy.md)
- [Ochrana soukromí a osobní údaje v Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Požadavky na Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a>Shromažďuje Configuration Manager shromažďovat osobní údaje?

No. Konfigurace neshromažďuje ani neodesílá žádná osobní data ani zákaznická data. Jedná se o místní produkt, který můžete přímo nasazovat, spravovat a provozovat. Diagnostická data a údaje o využití, které Microsoft shromažďuje, vylepšuje možnosti instalace, kvality a zabezpečení budoucích verzí.

Další informace o Configuration Manager dat najdete v tématu [úrovně diagnostických dat o využití](levels-overview.md).
