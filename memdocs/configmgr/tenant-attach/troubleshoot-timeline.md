---
title: Řešení potíží s časovou osou zařízení
titleSuffix: Configuration Manager
description: Řešení potíží s časovou osou zařízení pro Configuration Manager připojení klienta
ms.date: 09/8/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 54a58548-45f3-4f75-93d6-d2fd96227e6a
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 979ec6f081a318886eda9eeac91c16adc635701d
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564292"
---
# <a name="troubleshoot-the-timeline-for-devices-uploaded-to-the-admin-center-preview"></a><a name="bkmk_timeline"></a> Řešení potíží s časovou osou pro zařízení odeslaná do centra pro správu (Preview)
<!--CM7141381, IN7552762 pubpreview Sept8, 2020 -->
*Platí pro: Configuration Manager (Current Branch)*

K řešení potíží s časovou osou zařízení v centru pro správu Microsoft Endpoint Manageru použijte následující postup:

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.


## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_common"></a> Běžné chyby v centru pro správu Microsoft Endpoint Manageru

Při zobrazení nebo synchronizaci časové osy z centra pro správu Microsoft Endpoint Manageru můžete spustit jednu z těchto chyb.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_401"></a> V Azure Active Directory chybí potřebná konfigurace.

**Chybová zpráva:** V Azure Active Directory chybí potřebná konfigurace. Nezapomeňte připojit Configuration Manager lokality k vašemu tenantovi Azure a přiřadit správnou roli uživatele v Azure AD.

**Možné příčiny:**

- Ujistěte se, že je nakonfigurované zjišťování [uživatelů služby Azure AD](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) a zjišťování [uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) a že je uživatel zjištěný pomocí obou.
- V uživatelském účtu může chybět role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny. Změny tohoto oprávnění mohou trvat až hodinu.

### <a name="unable-to-get-timeline-information"></a><a name="bkmk_403"></a> Nepovedlo se získat informace o časové ose.

**Chybová zpráva:** Nepovedlo se získat informace o časové ose. Ujistěte se, že je nakonfigurované zjišťování uživatelů Azure AD a AD a že je uživatel zjištěn v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

**Možné příčiny:**

Ověřte, že má účet následující oprávnění:
- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Oprávnění **číst prostředek** v rámci **kolekce** v Configuration Manager.
- Oprávnění pro **oznamování prostředků** v rámci **kolekce** v Configuration Manager.
   - Toto oprávnění je nutné, aby bylo možné synchronizovat nejnovější události.

### <a name="unable-to-get-timeline-information"></a><a name="bkmk_404"></a> Nepovedlo se získat informace o časové ose.

**Chybová zpráva:** Informace o zařízení ještě nejsou synchronizované z Configuration Manager do centra pro správu Microsoft Endpoint Manageru. Po připojení lokality k vašemu tenantovi Azure počkejte až 15 minut.

**Možné řešení:** Počkejte přibližně 15 minut a problém by se měl vyřešit automaticky.

### <a name="unexpected-error-occurred"></a><a name="bkmk_500"></a> Stala se neočekávaná chyba.

**Chybová zpráva:** Stala se neočekávaná chyba.

**Možné příčiny:**

- Ověřte, že máte minimálně verzi Configuration Manager 2002 s [kumulativní aktualizací](https://support.microsoft.com/help/4560496/) a odpovídající verzí konzoly, která je nainstalovaná.
- Pokud je k dispozici velký počet událostí (více než 10 000, přibližně) a více hledání se požaduje rychle, je možné, že dojde k neočekávané chybě. Můžete se také podívat na [časový limit](#bkmk_timeout)výsledků hledání.

### <a name="getting-results-timed-out"></a><a name="bkmk_timeout"></a> Při získávání výsledků vypršel časový limit.

**Chybová zpráva:** Při získávání výsledků vypršel časový limit. Ujistěte se, že spojovací bod služby Configuration Manager je funkční a má připojení ke cloudu.

**Možná příčina:** Pokud je k dispozici velký počet událostí (více než 10 000, přibližně) a více hledání se požaduje rychle, je možné zobrazit časový limit. Může se zobrazit také [Neočekávaná chyba](#bkmk_500).

## <a name="known-issues"></a>Známé problémy

### <a name="boundary-group-id-is-used-rather-than-the-name"></a>Místo názvu se použije ID hraniční skupiny.

**Scénář:** Pokud používáte Configuration Manager verze 2002 a zařízení mění skupiny hranic, může se zobrazit zpráva o události, kde se zobrazí ID skupiny hranic, nikoli název.

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Další kroky

[Odstraňování potíží s připojením tenanta](troubleshoot.md)