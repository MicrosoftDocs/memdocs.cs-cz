---
title: Vytvoření sestavy Intune z datového kanálu OData pomocí Power BI
titleSuffix: Microsoft Intune
description: Vytvořte vizualizaci mapy stromové struktury pomocí Power BI Desktopu s interaktivním filtrem z rozhraní API datového skladu Intune.
keywords: Datový sklad Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: A2C8A336-29D3-47DF-BB4A-62748339391D
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87c1a63ffdfc0b923f636159536f6d6cf6420db9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331763"
---
# <a name="create-an-intune-report-from-the-odata-feed-with-power-bi"></a>Vytvoření sestavy Intune z datového kanálu OData pomocí Power BI

Tento článek vysvětluje, jak vytvořit vizualizaci stromové struktury vašich dat Intune pomocí Power BI Desktop, které uživatelé interaktivní filtrují. Například vaše finanční ŘEDITELka může chtít zjistit, jak celkové rozdělení zařízení porovnává mezi zařízeními vlastněná společností a osobními zařízeními. Mapa stromové struktury poskytuje podrobný přehled celkového počtu typů zařízení. Můžete zkontrolovat počet zařízení s iOS/iPadOS, Androidem a Windows, která jsou ve vlastnictví společnosti nebo v osobním vlastnictví.

## <a name="overview-of-creating-the-chart"></a>Přehled vytvoření grafu

Graf vytvoříte takto:
1. Pokud ještě nemáte Power BI Desktop, nainstalujte ho.
2. Připojte se k datovému modelu datového skladu Intune a načtěte aktuální data modelu.
3. Vytvořte nebo spravujte relace datového modelu.
4. Vytvořte graf s daty z tabulky **zařízení**.
5. Vytvořte interaktivní filtr.
6. Zobrazte hotový graf.

### <a name="a-note-about-tables-and-entities"></a>Poznámka k tabulkám a entitám

V Power BI pracujete s tabulkami. Tabulka obsahuje datová pole. Každé datové pole má datový typ. Pole může obsahovat jenom data datového typu. Datové typy jsou čísla, text, kalendářní data a tak dále. Tabulky v Power BI se při načtení modelu vyplní posledními historickými daty z vašeho tenanta. I když se konkrétní data časem mění, struktura tabulky se nezmění, dokud se základní datový model neaktualizuje.

Používání pojmů *entita* a *tabulka* může být matoucí. Datový model je přístupný prostřednictvím informačního kanálu OData (Open Data Protocol). Kontejnery, které se v Power BI nazývají tabulky, se v prostředí OData nazývají entity. Oba tyto pojmy označují stejnou věc, která obsahuje vaše data. Další informace o OData najdete v [přehledu OData](/odata/overview).

## <a name="install-power-bi-desktop"></a>Instalace Power BI Desktopu

Nainstalujte si nejnovější verzi aplikace Power BI Desktop. Power BI Desktop si můžete stáhnout z webu: [PowerBI.microsoft.com](https://powerbi.microsoft.com/desktop)

## <a name="connect-to-the-odata-feed-for-the-intune-data-warehouse-for-your-tenant"></a>Připojení k datovému kanálu OData pro datový sklad Intune pro vašeho tenanta

> [!Note]  
> Potřebujete oprávnění k **Sestavám** v Intune. Další informace najdete v sekci [Autorizace](reports-api-url.md#authorization).

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Otevřete podokno **datový sklad Intune** tak, že v části **Další úkoly** na pravé straně okna **Microsoft Intune-přehled** vyberete odkaz datový sklad.
3. Zkopírujte adresu URL vlastního kanálu. Například: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=beta`
4. Otevřete Power BI Desktop.
5. V řádku nabídek vyberte **soubor** > **získat data** > datový **kanál OData**.
6. Vložte adresu URL vlastního informačního kanálu, kterou jste zkopírovali v předchozím kroku, do pole Adresa URL v okně datového **kanálu OData** .
7. Vyberte **Základní**.

    ![Kanál OData pro datový sklad Intune pro vašeho tenanta](./media/reports-proc-create-with-odata/reports-create-01-odatafeed.png)

8. Vyberte **OK**.
9. Vyberte **Účet organizace** a pak se přihlaste pomocí přihlašovacích údajů Intune.

    ![Přihlašovací údaje pro účet organizace](./media/reports-proc-create-with-odata/reports-create-02-org-account.png)

10. Vyberte **Připojit**. Otevře se Navigátor se seznamem tabulek v datovém skladu Intune.

    ![Snímek obrazovky navigátoru – seznam tabulek datového skladu](./media/reports-proc-create-with-odata/reports-create-02-loadentities.png)

11. Vyberte **zařízení** a tabulky **ownerTypes**.  Vyberte **Načíst**. Power BI načte data do modelu.

## <a name="create-a-relationship"></a>Vytvoření relace

Můžete importovat víc tabulek k analýze nejen dat v jedné tabulce, ale souvisejících dat mezi tabulkami. Power BI má funkci s názvem automatické **rozpoznávání** , která se pokouší vyhledat a vytvořit relace za vás. Tabulky v datovém skladu byly sestaveny tak, aby fungovaly s funkcí automatického rozpoznávání v Power BI. I když ale Power BI nenaleznou relace automaticky, můžete je stále spravovat.

![Správa vztahů souvisejících dat napříč tabulkami](./media/reports-proc-create-with-odata/reports-create-03-managerelationships.png)

1. Vyberte **Spravovat relace**.
2. Vyberte Automatické **rozpoznávání...,** Pokud Power BI ještě nerozpoznaly relace.

Relace se zobrazí ve sloupci Z do sloupce Do. V tomto příkladu datové pole **ownerTypeKey** v tabulce **zařízení** odkazuje na datové pole **ownerTypeKey** v okně **ownerTypes**. Pomocí relace můžete vyhledat jednoduchý název kódu typu zařízení v tabulce **zařízení** .

## <a name="create-a-treemap-visualization"></a>Vytvoření vizualizace mapy stromové struktury

Graf stromové struktury zobrazuje hierarchická data jako pole v rámečcích. Každá větev hierarchie je pole, které obsahuje menší pole zobrazující nižší větve. Pomocí Power BI plochy můžete vytvořit mapu stromové struktury dat Intune, která zobrazuje relativní množství typů výrobců zařízení.

![Power BI vizualizace stromové struktury](./media/reports-proc-create-with-odata/reports-create-03-treemap.png)

1. V podokně **vizualizace** vyhledejte a vyberte **mapu stromové**struktury. Graf **stromové** struktury bude přidán na plátno sestavy.
2. V podokně **pole** Najděte `devices` tabulce.
3. Rozbalte tabulku `devices` a vyberte pole `manufacturer` data.
4. Přetáhněte datové pole `manufacturer` na plátno pro sestavy a umístěte ho do grafu **mapy stromové** struktury.
5. Přetáhněte datové pole `deviceKey` z tabulky `devices` do podokna **vizualizace** a přetáhněte je do části **Values (hodnoty** ) v poli **přidat datová pole**.  

Teď máte vizuál, který znázorňuje rozdělení výrobců zařízení v rámci vaší organizace.

![Mapa stromové struktury s daty – distribuce výrobců zařízení](./media/reports-proc-create-with-odata/reports-create-06-treemapwdata.png)

## <a name="add-a-filter"></a>Přidání filtru

Do mapy stromové struktury můžete přidat filtr, který vám pomocí vaší aplikace umožní zodpovědět další otázky.

1. Pokud chcete přidat filtr, vyberte plátno pro sestavy a vyberte **ikonu průřezu** (![stromovou mapu s datovým modelem a podporovanými relacemi](./media/reports-proc-create-with-odata/reports-create-slicer.png)) v části **vizualizace**. Na plátně se zobrazí prázdná vizualizace **průřezu** .
2. V podokně **pole** Najděte `ownerTypes` tabulce.
3. Rozbalte tabulku `ownerTypes` a vyberte pole `ownerTypeName` data.
4. Přetáhněte datové pole `onwerTypeName` z tabulky `ownerTypes` do podokna **filtry** a přetáhněte ho do části **filtry na této stránce** v poli **přidat datová pole**.  

   Pod `OwnerTypes` tabulkou se nachází datové pole s názvem `OwnerTypeKey`, které obsahuje data pro to, jestli je zařízení ve vlastnictví společnosti nebo osobní. Vzhledem k tomu, že byste chtěli v tomto filtru Zobrazit popisné názvy, vyhledejte `ownerTypes` tabulku a přetáhněte **ownerTypeName** do průřezu. Tento příklad ukazuje, jak datový model podporuje relace mezi tabulkami.

![Mapa stromové struktury s filtrem – podporuje relace mezi tabulkami](./media/reports-proc-create-with-odata/reports-create-08_ownertype.png)

Teď máte interaktivní filtr, pomocí kterého můžete přepínat mezi zařízeními ve vlastnictví společnosti a v osobním vlastnictví. Pomocí tohoto filtru uvidíte, jak se jejich rozdělení mění.

1. V průřezu vyberte **Společnost** , aby se zobrazila distribuce zařízení vlastněné společností.
2. Vyberte **osobní** v průřezu, abyste viděli zařízení v osobním vlastnictví.

## <a name="next-steps"></a>Další kroky

- Další informace o [vytváření a správě relací](https://powerbi.microsoft.com/documentation/powerbi-desktop-create-and-manage-relationships/) v Power BI Desktopu najdete v dokumentaci k Power BI.
- Přečtěte si článek [Datový model datového skladu Intune](reports-ref-data-model.md).
