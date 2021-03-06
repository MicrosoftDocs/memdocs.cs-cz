---
title: Co je nového v Desktop Analytics
titleSuffix: Configuration Manager
description: Shrnutí nových funkcí v nejnovější měsíční verzi cloudové služby Desktop Analytics.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd188b80375861cd08784d0574e737bfce7f2d92
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993142"
---
# <a name="whats-new-in-desktop-analytics"></a>Co je nového v Desktop Analytics

Zjistěte, co je nového v jednotlivých měsících v Desktop Analytics.

> [!TIP]
> Zavedení každé měsíční aktualizace může trvat až tři dny. Některé funkce můžou vycházet v průběhu několika týdnů a nemusí být k dispozici všem zákazníkům hned první týden.

Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>Srpen 2020

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Aplikace nasazené z Configuration Manager jsou ve výchozím nastavení důležité.

<!-- 4859763 -->

Konfigurace **důležitosti** aplikace je důležitá pro desktopovou analýzu k určení zařízení, která se mají zahrnout do pilotních nasazení. Správce, který je potřebný k ruční konfiguraci důležitosti pro všechny aplikace v rámci analýzy stolních počítačů. Jenom jednou, když zkušební projekt ověříte, můžete pokračovat v produkčním nasazení.

Pro každou aplikaci, kterou nasazujete pomocí Configuration Manager, ji služba Analytics Desktop ve výchozím nastavení automaticky nakonfiguruje jako důležitou. Toto chování vám umožní rychleji nakonfigurovat aplikace ve vašem prostředí, aby se dosáhlo rychlejšího vývoje produkčního nasazení.

Další informace najdete v tématu [assets-Apps](about-assets.md#apps).

<!-- 6049643 -->

### <a name="improved-processing-of-diagnostic-data-during-snapshot-generation"></a>Vylepšené zpracování diagnostických dat během generování snímku

Společnost Microsoft zlepšila, jak shromažďují a zpracovávají diagnostická data Windows ze zařízení zaregistrovaných v Desktop Analytics. Tato vylepšení zvyšují spolehlivost každodenního generování snímků a připravují se na nové funkce ve vývoji. V důsledku této práce Microsoft dočasně zakázal počet zařízení, která **tuto aplikaci spustila za posledních 30 dnů** v plánech nasazení. Další informace najdete v tématu [assets-Apps](about-assets.md#usage).

## <a name="july-2020"></a>Červenec 2020

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10 verze 2004, teď k dispozici v Desktop Analytics

<!-- 7370207 -->

Když v portálu pro Desktop Analytics monitorete aktualizace zabezpečení a funkcí, uvidíte teď Windows 10 verze 2004. Při vytváření plánu nasazení můžete jako cílovou verzi vybrat Windows 10, verze 2004.

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>Vylepšená podpora pro zobrazení portálu z libovolného zařízení

<!-- 6270240 -->

Portál Analytics pro stolní počítače teď můžete zobrazit v centru pro správu Microsoft Endpoint Manageru z různých typů zařízení. Nyní splňuje pokyny pro přístupnost webového obsahu (WCAG) 2,1 pro rozlišení obrazovky, které je menší než 320 x 256 pixelů. Například následující obrázek je z portálu z Apple iPhone 8:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="Portál pro Desktop Analytics na iPhonu 8":::

### <a name="notifications-for-service-impacting-events"></a>Oznámení pro události týkající se vlivu služby

<!-- 4982509 -->

Portál pro Desktop Analytics teď může zobrazovat bannery s oznámením. Tato oznámení umožňují Microsoftu komunikovat s vámi o důležitých událostech a problémech. Například známé problémy se službou, latencí dat nebo novými požadavky. Další informace najdete v tématu [oznámení služby](troubleshooting.md#service-notifications).

## <a name="june-2020"></a>Červen 2020

### <a name="improvement-to-prerequisites"></a>Vylepšení požadavků

Desktop Analytics už nevyžaduje nasazení Microsoft 365 služby v tenantovi Azure Active Directory (Azure AD). Aplikace pro **správu klientů Office 365** ve službě Azure AD je teď aplikací pro **desktopovou analýzu** , která umožňuje Configuration Manager načítání informací a stavu ze služby.

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
