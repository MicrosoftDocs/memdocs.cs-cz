---
title: Zobrazení inventáře hardwaru a softwaru u počítačů s Windows
titleSuffix: Microsoft Intune
description: Jak zobrazit informace o hardwaru a softwaru počítačů s Windows, které spravujete pomocí klienta softwaru Intune
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3c10f4c9-520b-4864-92fc-a45a9f640ad4
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e2d5e3f1e5839040c3ffd2229c34f3063a3ce87
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330127"
---
# <a name="view-hardware-and-software-inventory-for-windows-pcs"></a>Zobrazení inventáře hardwaru a softwaru u počítačů s Windows

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Informace v tomto tématu se vztahují jenom na desktopové systémy Windows, které spravujete jako počítače (PC) pomocí softwarového klienta Intune. Pokud chcete zobrazit inventář pro počítače s Windows zaregistrované jako mobilní zařízení, přečtěte si téma [zobrazení podrobností o zařízení v Intune](../remote-actions/device-inventory.md).

Intune shromažďuje podrobné informace o hardwaru a softwaru pro stolní počítače, které spravujete jako počítače pomocí softwarového klienta Intune. V následujících postupech se dozvíte toto:

- Jak vytvořit sestavu s informacemi o hardwarových možnostech počítačů, které spravujete

- Jak vytvořit sestavu se seznamem softwaru nainstalovaného na jednotlivých počítačích

- Jak aktualizovat inventář počítačů, abyste měli jistotu, že jsou data v sestavě aktuální

## <a name="to-display-information-about-pcs-you-manage"></a>Zobrazení informací o počítačích, které spravujete

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **sestavy** &gt; **sestavy inventáře počítače**.

2. Na stránce **Vytvořit novou sestavu** přijměte výchozí hodnoty, případně je upravte, aby se vyfiltrovaly výsledky, které bude sestava obsahovat. Můžete třeba vybrat, aby se v sestavě zobrazily jenom počítače, které používají Windows 8.1.

3. Kliknutím na **Zobrazit sestavu** otevřete **sestavu inventáře počítače** v novém okně.

    Když vyberete záhlaví příslušných sloupců, jako je třeba **Název**, **Typ skříně** nebo **Výrobce**, můžete sestavu podle těchto sloupců seřadit.

## <a name="to-display-software-installed-on-pcs-you-manage"></a>Zobrazení softwaru nainstalovaného na počítačích, které spravujete

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **sestavy** &gt; **zjištěné zprávy o softwaru**.

2. Na stránce **Vytvořit novou sestavu** přijměte výchozí hodnoty, případně je upravte, aby se vyfiltrovaly výsledky, které bude sestava obsahovat. Můžete třeba vybrat, aby se v sestavě zobrazil jenom software publikovaný Microsoftem.

3. Zvolte **Zobrazit sestavu**. **Sestav rozpoznaného softwaru** se otevře v novém okně.

    Když vyberete záhlaví příslušných sloupců, jako je třeba **Název**, **Vydavatel** nebo **Kategorie** , můžete sestavu podle těchto sloupců seřadit. Zvolením směrové šipky vedle položky seznamu můžete aktualizace v seznamu rozbalit a zobrazit tak další podrobnosti (třeba počítače, na kterých jsou nainstalované).

## <a name="to-refresh-computer-inventory-to-ensure-it-is-current"></a>Aktualizace inventáře počítače, abyste měli jistotu, že je aktuální

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) zvolte **Skupiny** &gt; **Všechna zařízení** (nebo jinou skupinu obsahující počítač, pro který chcete inventář aktualizovat).

2. Vyberte počítač. Nebo když stisknete a podržíte **Ctrl**, můžete vybrat víc počítačů.

3. Na hlavním panelu vyberte **vzdálené úlohy** &gt; **aktualizovat inventář**.

4. Pokud chcete zobrazit stav úlohy, v pravém dolním rohu stránky zvolte **Vzdálené úlohy**.

    V dialogovém okně **Stav úlohy** se zobrazí aktuální vzdálené úlohy, stav úloh, název zařízení, všechny hlášené chyby a odkaz na informace o odstraňování problémů.

## <a name="see-also"></a>Viz také

[Běžné úlohy správy počítačů s Windows pomocí klientského softwaru Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
