---
title: Co je nového v Desktop Analytics
titleSuffix: Configuration Manager
description: Shrnutí nových funkcí v nejnovější měsíční verzi cloudové služby Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 1d45d115f279603fa74e143c603c116146278ffe
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268157"
---
# <a name="whats-new-in-desktop-analytics"></a>Co je nového v Desktop Analytics

Zjistěte, co je nového v jednotlivých měsících v Desktop Analytics.

> [!TIP]
> Zavedení každé měsíční aktualizace může trvat až tři dny. Některé funkce můžou vycházet v průběhu několika týdnů a nemusí být k dispozici všem zákazníkům hned první týden.

Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="may-2020"></a>Květen 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Snižte počet aplikací k revizi.

<!-- 5542186 -->

Aby bylo možné konsolidovat a snižovat počet aplikací zobrazených na stránce assets (prostředky) na portálu, teď kombinuje všechny verze aplikací se stejným názvem a vydavatelem. Toto nastavení odráží počet aplikací na dlaždici **aplikace zajímavosti** . Například místo výpisu stovek instancí Microsoft Edge existuje jedna instance pro všechny verze. Pro všechny verze můžete udělat rozhodnutí jednou. Pokud potřebujete rozhodnout o konkrétních verzích aplikace, je toto chování konfigurovatelné.

Další informace najdete v tématu [o prostředcích – aplikace](about-assets.md#apps).

## <a name="march-2020"></a>Březen 2020

### <a name="support-for-multiple-hierarchies"></a>Podpora pro více hierarchií

<!-- 4814075, 6079184 -->

Nyní můžete připojit více Configuration Manager hierarchií k jednomu Azure Active Directory tenantovi s jedním komerčním ID pro desktopovou analýzu. Portál rozděluje zařízení z různých hierarchií a vylepšuje prostředí globálních pilotů a plánů nasazení.

- Pokud nakonfigurujete globální pilotní nasazení, pokud zahrnete kolekce, které obsahují více než 20% vašich celkových zaregistrovaných zařízení, zobrazí se na portálu upozornění.
- Pokud při vytváření plánu nasazení vyberete kolekce pro více hierarchií, na portálu se zobrazí upozornění.

> [!NOTE]
> Podpora pro více hierarchií vyžaduje Configuration Manager verze 1910 nebo novější.

Další informace najdete v následujících článcích:

- [Globální pilotní nasazení](deploy-pilot.md#bkmk_GlobalPilot)
- [Jak vytvořit plány nasazení](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Identifikace zabezpečení kompatibility

<!-- 5746559 -->

Data o kompatibilitě Windows klasifikují některé aplikace a ovladače s *ochranou*, což může způsobit selhání nebo vrácení aktualizace Windows 10. Pomocí nástroje Desktop Analytics teď můžete tato ochranná opatření identifikovat předem, abyste mohli prostředek napravit před nasazením aktualizace. Další informace najdete v tématu [posouzení kompatibility – zabezpečení](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Leden 2020

### <a name="additional-app-usage-detail"></a>Podrobnosti o využití dalších aplikací

<!-- 5533890 -->

Když vyberete aplikaci a zobrazíte další informace, podokno podrobností teď obsahuje další informace o použití. Tato data můžete použít k pochopení důležitosti instalace aplikace a také zařízení, ve kterých uživatelé aplikaci pravidelně používají. Další informace najdete v tématu [o prostředcích – využití aplikací](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Poskytnutí zpětné vazby k Desktop Analytics

<!-- 5451636 -->

Pokud chcete sdílet svůj názor na Desktop Analytics, vyberte ikonu **odeslat smajlíka** v horní části portálu na pravé straně. Další informace najdete v tématu [sdílení názoru na produkt](get-support.md#bkmk_feedback).

## <a name="october-2019"></a>Říjen 2019

### <a name="improvements-to-compatibility-recommendations"></a>Vylepšení doporučení pro kompatibilitu

<!-- 3594545 -->

Desktop Analytics teď poskytuje další podrobnosti, když zjistí, že upgrade Windows zcela nebo částečně odebere aplikaci nebo ovladač. Další informace najdete v tématu [posouzení kompatibility](compat-assessment.md#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Migrace z Windows Analytics do existujícího tenanta

<!-- 5202803 -->

Po připojení k Desktop Analytics můžete teď po zprovoznění migrovat vstupy z existujícího pracovního prostoru Windows Analytics.

## <a name="september-2019"></a>Září 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Migrace vstupů z Windows Analytics

<!-- 4252663 -->

Během připojování teď můžete migrovat vstupy z existujícího pracovního prostoru Windows Analytics.

### <a name="offboard-from-desktop-analytics"></a>Odpojení z Desktop Analytics

<!-- 4972396 -->

Pokud ve svém prostředí nastavíte službu Desktop Analytics, ale chcete ji přestat používat, můžete teď účet zavřít. Pokud změníte svůj názor v 90 dnech, můžete účet znovu aktivovat. Další informace najdete v tématu [Jak zavřít svůj účet](account-close.md).

## <a name="august-2019"></a>Srpen 2019

### <a name="reset-your-account"></a>Resetování vašeho účtu

<!-- 3733897 -->

Pokud ve svém prostředí nastavili analýzu stolních počítačů, ale chcete začít s registrací a registraci, můžete ji teď resetovat. Další informace o tomto procesu najdete v tématu [Resetování účtu](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Automatické rozhodnutí o upgradu pro systém a aplikace ze Storu

<!-- 3587232 -->

Aby bylo možné omezit vaše úsilí při vytváření poznámek v aplikacích zajímavosti, určité typy aplikací jsou automaticky označeny jako *nedůležité*. Rozhodnutí o upgradu plánu nasazení pro tyto aplikace je také označeno jako *připravené*. Následující aplikace jsou kompatibilní a měly by po upgradu Windows i nadále fungovat:

- Systémové aplikace a komponenty publikované Microsoftem

- Aplikace spravované a aktualizované z Microsoft Store

Další informace najdete v tématu věnovaném [automatickému upgradu pro systém a aplikace ze Storu](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Co je nového v Configuration Manager

Dokumentace k Desktop Analytics vždycky odkazuje na funkce v nejnovější verzi Configuration Manager aktuální větvi. Další informace o nejnovějších změnách v Configuration Manager najdete v následujících článcích:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Novinky ve verzi 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Zastaralé funkce:

Když Microsoft plánuje odebrat významnou funkci služby Desktop Analytics, tato změna se bude předem nahlásila jako zastaralá funkce Configuration Manager. Další informace najdete v tématu [zastaralé funkce](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
