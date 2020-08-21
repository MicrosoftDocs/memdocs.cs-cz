---
title: Integrace se Serverem sestav Power BI
titleSuffix: Configuration Manager
description: Integrujte Server sestav Power BI s vytvářením sestav Configuration Manager pro moderní vizualizaci a lepší výkon.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eaceea5f83bd93fee8261a94147383cde001f90b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699581"
---
# <a name="integrate-with-power-bi-report-server"></a>Integrace se Serverem sestav Power BI

*Platí pro: Configuration Manager (Current Branch)*

<!--3721603-->

Počínaje verzí 2002 můžete integrovat [server sestav Power BI](/power-bi/report-server/get-started) s vytvářením sestav Configuration Manager. Tato integrace poskytuje moderní vizualizaci a lepší výkon. Přidává konzolovou podporu pro Power BI sestavy podobné tomu, co už existují s SQL Server Reporting Services.

Uložit Power BI Desktop soubory sestav (. PBIX) a nasaďte je do Server sestav Power BI. Tento postup je podobný jako u SQL Server Reporting Servicesch souborů sestav (. RDL). Sestavy můžete také spustit v prohlížeči přímo z konzoly Configuration Manager.

## <a name="prerequisites"></a>Předpoklady

- Server sestav Power BI licence Další informace najdete v tématu věnovaném [licencování server sestav Power BI](/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Stažení [server sestav Microsoft Power BI – září 2019](https://www.microsoft.com/download/details.aspx?id=57270)nebo novější.

    > [!NOTE]
    > Neinstalujte Server sestav Power BI hned. Správný proces založený na vašem prostředí najdete v tématu [konfigurace bodu služby Reporting Services](#configure-the-reporting-services-point).

- Stáhněte si [Microsoft Power BI Desktop (optimalizováno pro server sestav Power BI-září 2019)](https://www.microsoft.com/download/details.aspx?id=57271)nebo novější.

    > [!IMPORTANT]
    > - Ve službě [Stažení softwaru](https://www.microsoft.com/download/)použijte pouze verze Power BI Desktop, nepoužívejte z Microsoft Store verzi.
    > - Použijte pouze verzi [Power BI Desktop, která uvádí, že je **optimalizovaná pro server sestav Power BI**](/power-bi/report-server/install-powerbi-desktop).

- Power BI Integration používá ke generování sestav stejnou správu na základě rolí.
    > [!NOTE]
    > Server sestav Power BI nepodporuje sestavy s povolenými RBAC, takže všichni čtenáři sestav uvidí stejné výsledky bez ohledu na jejich přiřazený obor.

## <a name="configure-the-reporting-services-point"></a>Konfigurace bodu služby Reporting Services

Tento proces se liší v závislosti na tom, zda již máte tuto roli v lokalitě.

### <a name="you-have-a-reporting-services-point"></a>Máte bod služby Reporting Services

Tento proces použijte pouze v případě, že v lokalitě již máte bod služby Reporting Services. Proveďte všechny kroky tohoto procesu na stejném serveru:

1. V **Configuration Manager serveru pro sestavy**zálohujte **šifrovací klíče**. Další informace najdete v tématu [šifrovací klíče SSRS – zálohování a obnovení šifrovacích klíčů](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Pokud tento krok přeskočíte, ztratíte přístup k žádným vlastním sestavám v SQL Server Reporting Services.

1. Odeberte roli bodu služby Reporting Services z lokality.

1. Odinstalujte SQL Server Reporting Services, ale Udržujte databázi.

1. Nainstalujte Server sestav Power BI.

1. Nakonfigurovat Server sestav Power BI

    1. Použijte předchozí databázi serveru sestav.

    1. Pro obnovení **šifrovacích klíčů**použijte **Server pro sestavy Configuration Manager** .

1. Přidejte roli bodu služby Reporting Services do Configuration Manager.

### <a name="you-dont-have-a-reporting-services-point"></a>Nemáte bod služby Reporting Services.

Tento proces použijte pouze v případě, že v lokalitě ještě nemáte bod služby Reporting Services. Proveďte všechny kroky tohoto procesu na stejném serveru:

1. Nainstalujte Server sestav Power BI.

2. Přidejte roli bodu služby Reporting Services do Configuration Manager. Další informace najdete v tématu [Konfigurace vytváření sestav](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Konfigurace konzoly Configuration Manager

1. V počítači s konzolou Configuration Manager aktualizujte konzolu Configuration Manager na nejnovější verzi.

1. Nainstalujte Power BI Desktop. Ujistěte se, že je jazyk stejný.

1. Po instalaci spusťte Power BI Desktop alespoň jednou, než otevřete konzolu Configuration Manager.

## <a name="create-power-bi-reports"></a>Vytváření sestav Power BI

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte nový uzel **sestavy Power BI** .

1. Na pásu karet vyberte **vytvořit sestavu**. Tato akce otevře Power BI Desktop.

1. Vytvoření sestavy v Power BI Desktopu

    - Pokud se v Power BI Desktop připojíte ke zdroji dat, vyberte v nastavení připojení možnost **DirectQuery** .

    - V těchto sestavách použijte pouze podporovaná zobrazení SQL. Další informace najdete v tématu [vytváření vlastních sestav pomocí SQL Server zobrazení v Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Až bude sestava připravena k uložení, přejděte do nabídky **soubor** , vyberte **Uložit jako**a pak zvolte **server sestav Power BI**.

1. V okně **výběr server sestav Power BI** jako **novou adresu serveru sestav**zadejte adresu URL bodu služby Reporting Services. Například, `https://rsp.contoso.com/Reports`.

V konzole Configuration Manager se v seznamu Power BI sestav zobrazí nová sestava.

## <a name="next-steps"></a>Další kroky

Po vytvoření sestavy použijte následující akce v konzole Configuration Manager:

- **Spustit v prohlížeči**: otevře sestavu Power BI ve webovém prohlížeči. Tuto adresu URL můžete sdílet s ostatními, například: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Tyto sestavy můžete zobrazit pouze ve webovém prohlížeči.

- **Upravit**: proveďte změny sestavy v Power BI Desktop. U existující sestavy použijte možnost **Uložit** a uložte změny zpátky na server sestav.

Další informace o souborech protokolu, které se mají použít pro vytváření sestav, najdete v tématu [Přehled souborů protokolu – vytváření sestav](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).