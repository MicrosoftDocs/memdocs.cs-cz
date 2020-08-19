---
title: Instalace ukázkových sestav Power BI
titleSuffix: Configuration Manager
description: Naučte se instalovat ukázkové sestavy Power BI v Configuration Manager
ms.date: 08/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb55fc79c44af83c7bb7a5e0802800f55e28e6b3
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614763"
---
# <a name="install-power-bi-sample-reports"></a>Instalace ukázkových sestav Power BI
<!--5679791-->
*Platí pro: Configuration Manager (Current Branch)*

Počínaje verzí 2002 můžete integrovat [server sestav Power BI](https://docs.microsoft.com/power-bi/report-server/get-started) s vytvářením sestav Configuration Manager. Pro stažení jsou k dispozici ukázkové sestavy, které můžete nainstalovat v Configuration Manager. Tento článek vysvětluje, jak nainstalovat ukázkové sestavy Power BI v Configuration Manager.

## <a name="prerequisites"></a>Předpoklady

- Configuration Manager bod služby Reporting Services s [server sestav Power BI integrovaným](powerbi-report-server.md)

- [Microsoft Power BI Desktop (optimalizováno pro server sestav Power BI – září 2019)](https://www.microsoft.com/download/details.aspx?id=57271)nebo novější

- [Kumulativní aktualizace (4560496) pro verzi 2002](https://support.microsoft.com/help/4560496) je doporučena, ale není vyžadována.

    > [!IMPORTANT]
    > Používejte pouze verze Power BI Desktop z [webu Microsoft Download Center](https://www.microsoft.com/download/). Nepoužívejte verzi z Microsoft Store.
    >
    > Použijte pouze verzi Power BI Desktop, která je [optimalizována pro server sestav Power BI](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>Stažení ukázkových sestav

Stažení ukázkových sestav:

1. Stažení ukázkových sestav Power BI z [webu Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452).

1. Uložte soubor `ConfigMgrSamplePowerBIReports.exe`.

1. Přesune soubor do počítače s Microsoft Power BI Desktop (optimalizováno pro Server sestav Power BI), pokud jste ho stáhli z jiného zařízení.

1. Spusťte `ConfigMgrSamplePowerBIReports.exe` soubor pro extrakci souborů. PBIT.

## <a name="install-the-sample-reports"></a>Instalace ukázkových sestav

Instalace ukázkových sestav:

1. Na serveru sestav Power BI vytvořte novou složku s názvem `Sample Reports` v kořenové složce Configuration Manager vytváření sestav.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Vytvoření ukázkové složky sestavy v kořenové Configuration Manager složce pro vytváření sestav z " lightbox="media/create-sample-reports-folder.png":::

1. Spusťte Microsoft Power BI Desktop (optimalizováno pro Server sestav Power BI).

1. Vyberte **soubor** , pak **otevřít** a přejděte do místa, kam jste uložili extrahované soubory. PBIT.

1. Vyberte jeden ze souborů. PBIT, které jste extrahovali ze `ConfigMgrSamplePowerBIReports.exe` souboru.

1. Po zobrazení výzvy zadejte název databáze Configuration Manager a název databázového serveru a pak vyberte **načíst**.

    :::image type="content" source="media/sample-report-database.png" alt-text="Zadat název databáze a databázového serveru" lightbox="media/sample-report-database.png":::

    > [!NOTE]
    > Při načítání nebo aplikování datového modelu Ignorujte všechny chyby, pokud jste nacházeli mezi sebou. Pokud se například zobrazí následující chyba: "připojení k tabulkám z více než jedné databáze není v režimu DirectQuery podporováno", vyberte **Zavřít**. Pak aktualizujte nastavení zdroje dat:
    >
    > 1. V Power BI Desktop na pásu karet vyberte **Upravit dotazy**a pak vyberte **Nastavení zdroje dat**.
    > 1. Vyberte **změnit zdroj**, potvrďte název serveru a databáze a vyberte **OK**.
    > 1. Zavřete okno nastavení zdroje dat a pak vyberte **použít změny**.

1. Po načtení dat sestavy vyberte **soubor**  >  **Uložit jako**a pak vyberte **server sestav Power BI**.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Uložit jako Server sestav Power BI" lightbox="media/save-powerbi-report-server.png":::

1. Uložte sestavu do `Sample Reports` složky, kterou jste vytvořili v bodu generování sestav.

    :::image type="content" source="media/save-sample-report.png" alt-text="Uložit do složky ukázkových sestav" lightbox="media/save-sample-report.png":::

1. Opakujte postup u ostatních ukázkových sestav. Až skončíte, zavřete Microsoft Power BI Desktop (optimalizováno pro Server sestav Power BI).

1. V konzole Configuration Manager přejdete do části **monitorování**  >  **Power BI sestavy**  >  **ukázkové sestavy**.

1. Klikněte pravým tlačítkem na jednu ze sestav a vyberte **Spustit v prohlížeči** a spusťte sestavu.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Spuštění ukázkové sestavy z konzoly Configuration Manager" lightbox="media/view-powerbi-report.png":::
