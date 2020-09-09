---
title: Přiřazení klienta – časová osa zařízení (Preview)
titleSuffix: Configuration Manager
description: Zobrazit časovou osu pro zařízení Configuration Manager v centru pro správu.
ms.date: 09/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: b2d914d8-6714-4fa1-9e14-0046b77e6b40
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5065e893a8670911c055910889e8fbae472bfc4c
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564301"
---
# <a name="tenant-attach-device-timeline-in-the-admin-center-preview"></a><a name="bkmk_timeline"></a> Připojení tenanta: časová osa zařízení v centru pro správu (Preview)
<!--CM7141381, IN7552762 pubpreview Sept 8, 2020-->
*Platí pro: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. Když Configuration Manager synchronizuje zařízení s Microsoft Endpoint Managerem prostřednictvím připojení tenanta, uvidíte časovou osu událostí. Tato časová osa zobrazuje minulou aktivitu v zařízení, která vám může pomoct při řešení problémů.

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

## <a name="prerequisites"></a>Požadavky

K použití časové osy z centra pro správu jsou potřeba tyto položky:

- Všechny předpoklady pro [připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr](client-details.md#prerequisites).
- Minimální verze Configuration Manager verze 2002 s [kumulativní aktualizací](https://support.microsoft.com/help/4560496/) a odpovídající verzí konzoly, která je nainstalována.
- Povolit shromažďování dat služby Endpoint Analytics v Configuration Manager:
   1. V konzole Configuration Manager klikněte na **Správa**  >  **nastavení klienta**  >  **výchozí nastavení klienta**.
   1. Klikněte pravým tlačítkem a vyberte **vlastnosti** a pak vyberte nastavení **agenta počítače** .
   1. Nastavte **možnost Povolit shromažďování dat služby Endpoint Analytics** na **hodnotu Ano**.
      - V centru pro správu se budou zobrazovat jenom události shromážděné po přijetí klienta s touto zásadou. Události před přijetím zásady nebudou dostupné.

## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Oprávnění **číst prostředek** v rámci **kolekce** v Configuration Manager.
- Oprávnění pro **oznamování prostředků** v rámci **kolekce** v Configuration Manager. <!--7984188-->
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD.
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.

## <a name="generate-events"></a>Generování událostí

Zařízení odesílají události jedenkrát za den do centra pro správu. V centru pro správu jsou viditelné pouze události shromážděné po přijetí zásady **shromažďování dat služby Endpoint Analytics** pro klienta. Vygenerujte události testu snadno tím, že nainstalujete aplikaci nebo aktualizaci z Configuration Manager nebo restartujete zařízení. Události se uchovávají po dobu 30 dnů. Pomocí [grafu](#collected-events) můžete zobrazit shromažďované události.

## <a name="collected-events"></a>Shromážděné události

|Název události|Název zprostředkovatele|ID události|
|---|---|---|
|Chyba aplikace|Chyba aplikace|1000|
|Zablokování aplikace|Zablokování aplikace|1002|
|Selhání jádra|Microsoft-Windows-WER-SystemErrorReporting|1001|
|Selhání aplikace|Zasílání zpráv o chybách systému Windows|1001|
|Agent web Windows Update – instalace aktualizace|Microsoft-Windows-WindowsUpdateClient|19|
|Neznámé vypnutí|Spouštění|0|
|Iniciované vypnutí|Spouštění|1074|
|Neobvyklé vypnutí|Spouštění|41|
|Změna hraniční skupiny|Microsoft – ConfigMgr|20000|
|Nasazení aplikací|Microsoft – ConfigMgr|20001|
|Configuration Manager – instalace aktualizace|Microsoft – ConfigMgr|20002|
|Změna verze firmwaru|Microsoft – ConfigMgr|20003|

## <a name="view-the-timeline"></a>Zobrazit časovou osu

1. V prohlížeči přejděte na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Vyberte **zařízení** a potom **všechna zařízení**.
1. Vyberte zařízení, které se synchronizuje z Configuration Manager prostřednictvím [připojení klienta](device-sync-actions.md).
1. Vyberte **Časová osa**. Ve výchozím nastavení jsou události zobrazeny za posledních 24 hodin.
   - Pomocí tlačítka **Filtr** můžete změnit **časový rozsah**, **úrovně události**a **název zprostředkovatele**.
   - Pokud vyberete událost, zobrazí se vám podrobná zpráva.
   - Vyberte **synchronizovat** a načtěte poslední data generovaná v klientovi. Zařízení ve výchozím nastavení odesílá události jedenkrát za den do centra pro správu. <!--7984188-->
   - Výběrem **aktualizovat** znovu načtete stránku a zobrazíte nově shromážděné události.

   :::image type="content" source="./media/7141381-timeline.png" alt-text="Časová osa událostí pro zařízení" lightbox="./media/7141381-timeline.png":::

## <a name="next-steps"></a>Další kroky

[Řešení potíží s časovou osou zařízení](troubleshoot-timeline.md)