---
title: Konfigurace stavu klienta
titleSuffix: Configuration Manager
description: V Configuration Manager vyberte nastavení stavu klienta.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384906"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Postup konfigurace stavu klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než budete moci monitorovat Configuration Manager klienty a opravit problémy, nakonfigurujte nastavení stavu klienta lokality. Tato nastavení určují parametry, které lokalita používá k označení klientů jako neaktivních. Také nakonfigurujte možnosti, které vás upozorní, pokud aktivita klienta klesne pod určenou prahovou hodnotu.

## <a name="configure-client-status"></a>Konfigurace stavu klienta

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **stav klienta** . Na kartě **Domů** na pásu karet ve skupině **stav klienta** vyberte **Nastavení stavu klienta**.

1. Nakonfigurujte tahle nastavení:

    > [!NOTE]
    > Pokud klient nesplňuje žádné nastavení, lokalita ho označí jako neaktivní.

    - **Požadavky na zásady klienta v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klient požádal o zásady z lokality. Výchozí hodnota je `7` dnů.

      Porovnejte tuto hodnotu s nastavením **intervalu dotazování zásad klienta** ve skupině **zásad klienta** nastavení klienta. Výchozí hodnota je 60 minut. Jinými slovy, klient by měl každou hodinu dotazovat lokalitu na zásadu. Pokud po jednom týdnu zásady nevyžadují, lokalita ji označí jako neaktivní.

    - **Zjišťování prezenčního signálu v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klient odeslal do lokality záznam zjišťování prezenčního signálu. Výchozí hodnota je `7` dnů.

      Porovnejte tuto hodnotu s plánem pro [metodu zjišťování prezenčního signálu](../../servers/deploy/configure/about-discovery-methods.md). Ve výchozím nastavení lokalita spouští zjišťování prezenčního signálu jednou týdně.

    - **Inventář hardwaru v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klient odeslal do lokality záznam inventáře hardwaru. Výchozí hodnota je `7` dnů.

      Porovnejte tuto hodnotu s nastavením **plánu inventarizace hardwaru** ve skupině **inventáře hardwaru** nastavení klienta. Výchozí hodnota je 7 dní.

    - **Inventář softwaru v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klient odeslal do webu záznam inventáře softwaru. Výchozí hodnota je `7` dnů.

      Porovnejte tuto hodnotu s nastavením **Naplánování inventáře softwaru a kolekce souborů** ve skupině **inventáře softwaru** nastavení klienta. Výchozí hodnota je 7 dní.

    - **Stavové zprávy v průběhu následujících dnů:** Zadejte počet dní od okamžiku, kdy klient odeslal do lokality všechny stavové zprávy. Výchozí hodnota je `7` dnů. Klient může odesílat stavové zprávy pro různé druhy aktivit, jako je například spuštění pořadí úkolů. Lokalita odstraní staré stavové zprávy jako součást úlohy údržby a **odstraní zastaralé stavové zprávy**.

1. Zadejte následující hodnotu, která určuje, jak dlouho lokalita udržuje data historie stavu klienta:

    - **Uchovat historii stavu klienta po následující počet dnů:** Ve výchozím nastavení lokalita udržuje informace o stavu klienta pro `31` dny. Toto nastavení nemá žádný vliv na chování klienta nebo webu. Je podobný úloze údržby pro historii stavu klienta.

## <a name="configure-the-schedule"></a>Konfigurace plánu

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **stav klienta** . Na kartě **Domů** na pásu karet ve skupině **stav klienta** vyberte **naplánovat aktualizaci stavu klienta**.

1. Nakonfigurujte interval, ve kterém chcete aktualizovat stav klienta.

    > [!NOTE]
    > Když změníte plán pro aktualizace stavu klienta, projeví se to až do další plánované aktualizace stavu klienta v předchozím plánu.

## <a name="configure-alerts"></a>Konfigurace upozornění

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **kolekce zařízení** .

1. Vyberte kolekci, pro kterou chcete nakonfigurovat výstrahy. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.

    > [!NOTE]
    > Nemůžete konfigurovat výstrahy pro kolekce uživatelů.

1. Přepněte na kartu **výstrahy** a vyberte **Přidat**.

   > [!TIP]
   > Kartu **výstrahy** můžete zobrazit pouze v případě, že vaše role zabezpečení má oprávnění pro výstrahy.

    Zvolte výstrahy, které má lokalita generovat pro prahové hodnoty stavu klienta, a vyberte **OK**.

1. V seznamu **podmínky** na kartě **výstrahy** vyberte jednotlivé výstrahy stavu klienta a zadejte následující informace:

    - **Název výstrahy**: přijměte výchozí název nebo zadejte nový název výstrahy.

    - **Závažnost výstrahy**: vyberte úroveň výstrahy, kterou zobrazuje konzola Configuration Manager.

    - **Vyvolat výstrahu**: zadejte procento prahové hodnoty pro výstrahu.

## <a name="automatic-remediation-exclusion"></a>Automatické vyloučení nápravy

1. V klientském počítači, kde chcete zakázat automatickou nápravu, otevřete Editor registru.

    > [!WARNING]
    > Pokud používáte Editor registru nesprávně, můžete způsobit vážné problémy, které by mohly vyžadovat přeinstalaci systému Windows. Společnost Microsoft nemůže zaručit, že můžete vyřešit problémy, které jsou výsledkem nesprávného použití Editoru registru. Využijte ji na vlastní riziko.

1. Přejděte do klíče registru **HKEY_LOCAL_MACHINE \software\microsoft\ccm\ccmeval**.

1. Změňte hodnotu položky **NotifyOnly** :

    - `TRUE`: Klient nebude automaticky opravovat žádné nalezené problémy. Tato lokalita vás stále upozorní v pracovním prostoru **monitorování** o všech problémech s tímto klientem.

    - `FALSE`: Toto nastavení je výchozí. Klient automaticky opraví problémy při jejich hledání a tato lokalita vás upozorní v pracovním prostoru **monitorování** .

Když instalujete klienty nástroje, můžete je vyloučit z automatické nápravy pomocí vlastnosti instalace **NotifyOnly** . Další informace najdete v tématu [o vlastnostech instalace klienta](about-client-installation-properties.md).

## <a name="next-steps"></a>Další kroky

[Monitorování klientů](../manage/monitor-clients.md)
