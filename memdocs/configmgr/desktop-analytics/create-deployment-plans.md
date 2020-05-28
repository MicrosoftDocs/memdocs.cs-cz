---
title: Jak vytvořit plány nasazení
titleSuffix: Configuration Manager
description: Návod pro vytváření plánů nasazení v Desktop Analytics
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268755"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Vytvoření plánů nasazení v Desktop Analytics

Tento článek popisuje kroky pro vytvoření plánu nasazení v Desktop Analytics. Než začnete, nejdřív se [seznamte s plány nasazení](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Vytvoření plánu pro Windows 10

Podle pokynů v této části použijte Desktop Analytics k vytvoření plánu pro nasazení Windows 10.

1. Otevřete [portál Desktop Analytics](https://aka.ms/desktopanalytics). Používejte přihlašovací údaje, které mají alespoň oprávnění **přispěvatelé v pracovním prostoru** .  

2. Ve skupině spravovat vyberte **plány nasazení** .  

3. V podokně **plány nasazení** vyberte **vytvořit**.  

4. V podokně **vytvořit plán nasazení** nakonfigurujte následující nastavení:  

    - **Název**: jedinečný název plánu nasazení  

    - **Produkty a verze**: vyberte verzi Windows 10, kterou chcete nasadit. Microsoft doporučuje vytvářet plány nasazení, které používají nejnovější verzi.  

    - **Skupiny zařízení**: vyberte jednu nebo více skupin ze stejné hierarchie. Tyto skupiny jsou [kolekce zařízení](connect-configmgr.md#bkmk_Collections) synchronizované z Configuration Manager.

        Pokud připojíte více Configuration Manager hierarchií ke stejné instanci aplikace Desktop Analytics, zobrazí se zobrazovaný název hierarchie s názvem kolekce v globální pilotní konfiguraci. Tento název je vlastnost **Zobrazovaný název** v připojení Desktop Analytics v konzole Configuration Manager.<!-- 4814075 -->

        > [!NOTE]
        > Podpora pro více hierarchií vyžaduje Configuration Manager verze 1910 nebo novější.
        >
        > Pokud vyberete kolekce pro více hierarchií, na portálu se zobrazí upozornění. Plán nasazení nelze vytvořit s kolekcemi z více hierarchií.<!-- 4814075 -->

    - **Pravidla připravenosti**: Tato pravidla vám pomůžou určit, která zařízení jsou opravňující k upgradu. Další informace najdete v tématu [pravidla připravenosti](#readiness-rules).  

    - **Datum dokončení**: vyberte datum, kdy má být systém Windows plně nasazen do všech cílových zařízení.  

5. Vyberte **Vytvořit**. Nový plán se zobrazí v seznamu plánů nasazení během zpracování. Pro urychlení zpracování si vyžádejte aktualizaci dat na vyžádání. Další informace najdete v tématu [Nejčastější dotazy k Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Kliknutím na název otevřete plán nasazení.  

7. V nabídce plán nasazení vyberte ve skupině **Příprava** možnost **identifikovat důležitost**.  

    1. Na kartě **aplikace** vyberte možnost Zobrazit pouze **neprověřené** prostředky.  

    2. Vyberte každou aplikaci a pak vyberte **Upravit**. Můžete vybrat více než jednu aplikaci, kterou chcete upravit současně.  

    3. V seznamu **důležitost** vyberte úroveň důležitosti. Pokud chcete, aby aplikace Desktop Analytics ověřila aplikaci v rámci pilotního projektu, vyberte **kritické** nebo **důležité**. Neověřuje aplikace označené jako **nedůležité**. Při přiřazování úrovní důležitosti posuďte informace o [kompatibilitě](compat-assessment.md) a dalších plánech.  

        Při přiřazování úrovní důležitosti můžete také zvolit rozhodnutí o upgradu.  

    4. Po dokončení vyberte **Uložit** .  

8. V nabídce plán nasazení vyberte ve skupině **připravit** možnost **identifikovat pilotní projekt**.  

    1. Přečtěte si doporučené zařízení pro pilotní nasazení.  

    2. Vyberte jednotlivá zařízení a vyberte **Přidat do pilotního nasazení**. Pokud nesouhlasím s doporučením, vyberte **nahradit**.  

        Pokud chcete získat další informace o tom, jak tato doporučení využívá funkce Desktop Analytics, vyberte ikonu informace v pravém horním rohu podokna **určení pilotního projektu** .

## <a name="readiness-rules"></a>Pravidla připravenosti

Tato pravidla vám pomůžou určit, která zařízení jsou oprávněná k místnímu upgradu. Tato pravidla můžete nastavit při vytváření plánu nasazení nebo je upravit později.

Postup změny pravidel připravenosti:

1. Na portálu Desktop Analytics vyberte plán nasazení.
1. Vedle pole název vyberte **Upravit**.
1. Vyberte **pravidla připravenosti**.
1. Vyberte **operační systém Windows**.
1. Proveďte změny podle potřeby a vyberte **Uložit**.

Pro upgrady **operačního systému Windows** jsou k dispozici dvě pravidla: ovladače zařízení a aplikace systému Windows.

### <a name="device-drivers"></a>Ovladače zařízení

Nakonfigurujte, jestli vaše zařízení obdrží ovladače od web Windows Update. Tato hodnota je ve výchozím nastavení **vypnutá** . Toto pravidlo povolte, když používáte web Windows Update pro firmy ke správě aktualizací, včetně ovladačů. Pokud ke správě aktualizací softwaru používáte Configuration Manager, nastavte toto pravidlo na **vypnuto**.

### <a name="windows-applications"></a>Aplikace systému Windows

Aplikace, které Desktop Analytics ukáže jako *zajímavosti* , jsou založené na prahové hodnotě pro nízký počet instalací. Nastavte tuto prahovou hodnotu v pravidlech připravenosti pro plán nasazení. Ve výchozím nastavení je tato prahová hodnota **2,0%**. Hodnotu můžete změnit z `0.0` na `10.0` .


## <a name="next-steps"></a>Další kroky

Přejděte k dalšímu článku, který nasadíte do pilotních zařízení.
> [!div class="nextstepaction"]  
> [Pilotní nasazení](deploy-pilot.md)  
