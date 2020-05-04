---
title: Operace a údržba pro vytváření sestav
titleSuffix: Configuration Manager
description: Přečtěte si podrobnosti o správě sestav a předplatných sestav v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713713"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Operace a údržba pro vytváření sestav v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po umístění infrastruktury pro vytváření sestav v Configuration Manager existuje řada operací, které obvykle slouží ke správě sestav a odběrů sestav.

> [!NOTE]
> Tento článek se zaměřuje na sestavy v SQL Server Reporting Services. Počínaje verzí 2002 můžete integrovat vytváření sestav pomocí Server sestav Power BI. Další informace najdete v tématu věnovaném [integraci s server sestav Power BI](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Spuštění sestavy ze služby Reporting Services

Configuration Manager ukládá své sestavy do SQL Server Reporting Services. Sestava načte data z databáze lokality Configuration Manager. K sestavám můžete přistupovat v konzole Configuration Manager nebo pomocí Správce sestav přes webový prohlížeč. Otevřete sestavy z webového prohlížeče v jakémkoli počítači, který má přístup k bodu služby Reporting Services, a uživatel má dostatečná práva k zobrazení sestav. Chcete-li spustit sestavy, potřebujete oprávnění **ke čtení** pro oprávnění **lokalita** a oprávnění **Spustit sestavu** pro konkrétní objekty.

Při spuštění sestavy se v jazyce místního operačního systému zobrazí název, popis a kategorie sestavy. Další informace najdete v tématu [jazyky pro sestavy](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> Správce sestav je webový přístup k sestavě a nástroj pro správu. Můžete ji použít ke správě jedné instance serveru sestav přes připojení HTTPS. Použití Správce sestav pro provozní úlohy: zobrazit sestavy, upravit vlastnosti sestavy a spravovat související odběry sestav. Tento článek popisuje kroky pro zobrazení sestavy a úpravě vlastností sestav ve Správci sestav. Další informace o dalších možnostech ve Správci sestav najdete v tématu [co je správce sestav?](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode)

Pro spuštění sestavy Configuration Manager použijte následující postupy.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Spuštění sestavy v konzole Configuration Manager

1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Rozbalte položku **vytváření sestav**a potom vyberte možnost **sestavy**. Tento uzel obsahuje seznam dostupných sestav.

    > [!TIP]
    > Pokud tento uzel neobsahuje žádné sestavy, ověřte, zda je bod služby Reporting Services nainstalován a nakonfigurován. Další informace najdete v tématu [Konfigurace vytváření sestav](configuring-reporting.md).

1. Vyberte sestavu, kterou chcete spustit. Na kartě **Domů** na pásu karet v části **Skupina sestav** vyberte **Spustit** . otevře se sestava.

1. Pokud jsou požadované parametry, zadejte je a pak vyberte **Zobrazit sestavu**.

### <a name="run-a-report-in-a-web-browser"></a>Spuštění sestavy ve webovém prohlížeči

1. Ve webovém prohlížeči, přejít na adresu URL správce sestav, například `https://Server1/Reports`. Tuto adresu najdete na stránce **Adresa URL správce sestav** ve službě Reporting Services Configuration Manager.

1. Ve Správci sestav vyberte složku sestav pro Configuration Manager, například **ConfigMgr_CAS**.

    > [!TIP]
    > Pokud správce sestav neuvádí žádné sestavy, ověřte, zda je bod služby Reporting Services nainstalován a nakonfigurován. Další informace najdete v tématu [Konfigurace vytváření sestav](configuring-reporting.md).

1. Vyberte kategorii sestavy pro sestavu, kterou chcete spustit, a pak vyberte konkrétní sestavu. Sestava se otevře ve Správci sestav.

1. Pokud jsou požadované parametry, zadejte je a pak vyberte **Zobrazit sestavu**.

## <a name="modify-the-properties-of-a-report"></a>Úprava vlastností sestavy

Mezi vlastnosti sestavy patří název a popis sestavy. Můžete zobrazit vlastnosti sestavy n konzoly Configuration Manager.

Chcete-li změnit vlastnosti, použijte Správce sestav:

1. Ve webovém prohlížeči, přejít na adresu URL správce sestav, například `https://Server1/Reports`.

1. Ve Správci sestav vyberte složku sestav pro Configuration Manager, například **ConfigMgr_CAS**.

1. Vyberte kategorii sestavy a potom vyberte konkrétní sestavu. Sestava se otevře ve Správci sestav.

1. Vyberte kartu **vlastnosti** . upravte název a popis sestavy a pak vyberte **použít**.

Správce sestav uloží vlastnosti sestavy na serveru sestav. Konzola Configuration Manager zobrazuje aktualizované vlastnosti sestavy pro sestavu.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a>Úprava sestavy

Když sestava existující Configuration Manager nenačte požadované informace, upravte ji v Tvůrce sestav. Pomocí Tvůrce sestav můžete také změnit rozložení nebo návrh sestavy. I když můžete přímo upravit výchozí sestavu, je vhodné ji naklonovat. Otevřete sestavu, kterou chcete upravit, a pak vyberte **Uložit jako**.

Chcete-li upravit sestavu, potřebujete oprávnění **Upravit oprávnění lokality** a **Upravit sestavu** pro konkrétní objekty v sestavě.

> [!IMPORTANT]
> Aktualizace webu uchovávají předdefinované sestavy. Pokud upravíte standardní sestavu, při aktualizaci lokality přejmenuje sestavu pomocí předpony podtržítka (`_`). Tím se zajistí, že aktualizace lokality nepřepisuje upravenou sestavu standardní sestavou.
>
> Pokud upravíte předdefinované sestavy před instalací aktualizace lokality, zálohujte vlastní sestavy. Po aktualizaci obnovte sestavu ve službě Reporting Services. Pokud v předdefinované sestavě uděláte významné změny, vytvořte místo toho novou sestavu. Nové sestavy, které vytvoříte před upgradem lokality, nebudou přepsány.

Pro úpravu vlastností sestavy Configuration Manager použijte následující postup.

1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Rozbalte položku **vytváření sestav**a potom vyberte uzel **sestavy** .

1. Vyberte sestavu, kterou chcete upravit. Na kartě **Domů** na pásu karet v části **Skupina sestav** vyberte **Upravit**. Může vás vyzvat k zadání přihlašovacích údajů. Pokud Tvůrce sestav není v počítači nainstalován, Configuration Manager vás vyzve k jeho instalaci. Pro úpravy a vytváření sestav se vyžaduje Tvůrce sestav.

1. V Tvůrce sestav upravte odpovídající nastavení sestavy. Vyberte **Uložit** a uložte sestavu na server sestav.

## <a name="create-reports"></a>Vytvářet sestavy

Existují dva typy sestav, které můžete vytvořit:

- **Sestava založená na modelu** vám umožňuje interaktivně vybrat položky, které chcete zahrnout do sestavy. Další informace o vytváření vlastních modelů sestav najdete v tématu [vytváření vlastních modelů sestav pro Configuration Manager v SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

- **Sestava založená na jazyce SQL** umožňuje načíst data založená na příkazu SQL sestavy.

> [!IMPORTANT]
> Aby bylo možné vytvořit novou sestavu, váš účet potřebuje oprávnění pro **úpravu lokality** . Sestavu můžete vytvořit pouze ve složkách, pro které máte oprávnění **Upravit sestavu** .

### <a name="create-a-model-based-report"></a>Vytvoření sestavy založené na modelu

Pomocí následujícího postupu můžete vytvořit sestavu Configuration Manager založenou na modelu.

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte uzel **sestavy** .

1. Na kartě **Domů** na pásu karet v části **vytvořit** vyberte **vytvořit sestavu**. Tato akce otevře **Průvodce vytvořením sestavy**.

1. Na stránce **informace** nakonfigurujte následující nastavení:

    - **Typ**: vyberte **sestavu založenou na modelu**.

    - **Název**: zadejte název sestavy.

    - **Popis**: zadejte popis sestavy.

    - **Server**: zobrazí název serveru sestav, na kterém jste tuto sestavu vytvořili.

    - **Cesta**: vyberte **Procházet** a určete složku, do které chcete sestavu uložit.

1. Na stránce **Výběr modelu** vyberte dostupný model v seznamu pro vytvoření této sestavy. Část **Preview** zobrazuje SQL Server zobrazení a entit, které jsou k dispozici v tomto modelu sestavy.

1. Dokončete Průvodce vytvořením sestavy.

1. Otevřete Tvůrce sestav pro konfiguraci nastavení sestavy. Další informace najdete v tématu [Úprava sestavy Configuration Manager](#bkmk_edit).

1. V Tvůrce sestav vytvořte rozložení sestavy, vyberte data v dostupných zobrazeních SQL Server a přidejte do sestavy parametry.

1. Výběrem **Spustit** spusťte sestavu. Ověřte, že sestava poskytuje informace, které očekáváte. V případě potřeby vyberte **Návrh** pro další úpravu sestavy.

1. Vyberte **Uložit** a uložte sestavu na server sestav.

### <a name="create-a-sql-based-report"></a>Vytvoření sestavy založené na jazyce SQL

Když vytvoříte příkaz SQL pro vlastní sestavu, neodkazujte přímo na SQL Server tabulky. Vždy odkaz na podporované SQL Server zobrazení z databáze lokality. Tato zobrazení mají jména, která začínají `v_`na. Další informace najdete v tématu [vytváření vlastních sestav pomocí SQL Server zobrazení v Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

Na veřejné uložené procedury lze také odkazovat z databáze lokality. Tyto uložené procedury mají názvy, které začínají `sp_`na.

K vytvoření sestavy Configuration Manager založené na jazyce SQL použijte následující postup.

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte uzel **sestavy** .

1. Na kartě **Domů** na pásu karet v části **vytvořit** vyberte **vytvořit sestavu**. Tato akce otevře **Průvodce vytvořením sestavy**.

1. Na stránce **informace** nakonfigurujte následující nastavení:

    - **Typ**: vyberte **sestavu založenou na jazyce SQL**.

    - **Název**: zadejte název sestavy.

    - **Popis**: zadejte popis sestavy.

    - **Server**: zobrazí název serveru sestav, na kterém jste tuto sestavu vytvořili.

    - **Cesta**: vyberte **Procházet** a určete složku, do které chcete sestavu uložit.

1. Dokončete Průvodce vytvořením sestavy.

1. Otevřete Tvůrce sestav pro konfiguraci nastavení sestavy. Další informace najdete v tématu [Úprava sestavy Configuration Manager](#bkmk_edit).

1. V Tvůrce sestav zadejte příkaz SQL pro sestavu. Můžete také vytvořit příkaz SQL pomocí sloupců v dostupných zobrazeních. V případě potřeby přidejte do sestavy parametry.

1. Výběrem **Spustit** spusťte sestavu. Ověřte, že sestava poskytuje informace, které očekáváte. V případě potřeby vyberte **Návrh** pro další úpravu sestavy.

1. Vyberte **Uložit** a uložte sestavu na server sestav.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a>Správa odběrů sestav

Odběry sestav v SQL Server Reporting Services umožňují konfigurovat automatické doručování určených sestav e-mailem nebo sdílenou složkou v naplánovaných intervalech. Pokud chcete nakonfigurovat odběry sestav, použijte **Průvodce vytvořením předplatného** v Configuration Manager.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Vytvoření odběru sestavy pro doručení sestavy do sdílené složky

Když vytvoříte odběr sestavy pro doručení sestavy do sdílené složky, služba Reporting Services zkopíruje sestavu v zadaném formátu do sdílené složky, kterou určíte. Můžete se přihlásit k odběru a požádat o doručení pouze pro jednu sestavu najednou.

Když vytvoříte odběr, který používá sdílenou složku, zadejte jako cíl existující sdílenou složku. Server sestav nevytvoří složku nebo síťovou sdílenou složku. Když zadáte cílovou složku v předplatném, použijte cestu UNC a nezahrnujte koncová lomítka (`\`) do cesty ke složce. V následujícím příkladu je platná cesta UNC k cílové složce: `\\server\reportfiles\operations\2001`.

> [!NOTE]
> Při vytváření odběru zadáte uživatelské jméno a heslo. Tento účet potřebuje přístup k této sdílené složce s oprávněním k **zápisu** do cílové složky.

Služba Reporting Services může vykreslovat sestavy v různých formátech souborů. Například MHTML nebo Excel. Při vytváření předplatného vyberte formát. I když můžete vybrat libovolný podporovaný formát vykreslování, některé formáty při vykreslování do souboru fungují lépe než jiné.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Omezení pro odběry sestav do sdílené složky

Následující seznam obsahuje omezení odběrů sestav do sdílené složky:

- Na rozdíl od sestav, které hostuje a spravujete na serveru sestav, služba Reporting Services doručuje sestavy do sdílené složky jako statické soubory.

- Interaktivní funkce sestavy nefungují pro sestavy uložené jako soubory. Sestava představuje všechny interaktivní funkce jako statické prvky.

- Pokud sestava obsahuje grafy, použije se výchozí prezentace.

- Pokud se sestava propojuje s jinou sestavou, vykreslí se odkaz jako statický text.

Pokud chcete zachovat interaktivní funkce v doručené sestavě, použijte doručování e-mailů. Další informace najdete v tématu [Vytvoření odběru sestavy pro doručení sestavy e-mailem](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Postup vytvoření odběru sestavy pro sdílenou složku

K vytvoření odběru sestavy pro doručování sestavy do sdílené složky použijte následující postup.  

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte uzel **sestavy** .

1. Vyberte složku sestav a potom vyberte sestavu, ke které se chcete přihlásit. Na kartě **Domů** na pásu karet v části **Skupina sestav** vyberte **vytvořit odběr**. Tato akce otevře **Průvodce vytvořením předplatného**.

1. Na stránce **doručení odběru** nakonfigurujte následující nastavení:  

    - **Sestavu doručuje**: vyberte **sdílená složka systému Windows**.

    - **Název souboru**: zadejte název souboru pro sestavu. Ve výchozím nastavení soubor sestavy neobsahuje příponu názvu souboru. Vyberte možnost **při vytvoření přidat příponu souboru** , aby se automaticky přidala přípona názvu souboru na základě formátu.

    - **Cesta**: zadejte cestu UNC k existující složce, do které chcete doručit tuto sestavu. Například, `\\server\reportfiles\operations`.

    - **Formát vykreslení**: pro soubor sestavy vyberte jeden z následujících formátů:

      - **Soubor XML s daty sestavy**
      - **CSV (oddělený čárkami)**
      - **Soubor TIFF**
      - **Soubor aplikace Acrobat (PDF)**
      - **HTML 4,0**
        > [!NOTE]
        > Pokud sestava obsahuje obrázky, formát HTML 4,0 je nezahrne.
      - **MHTML (webový archiv)**
      - Nástroj pro **vykreslování RPL** (rozložení stránky sestavy)
      - **Excel**
      - **Word**

    - **Uživatelské jméno**: Zadejte uživatelský účet systému Windows s oprávněním k *zápisu* do zadané **cesty**.

    - **Heslo**: zadejte heslo pro výše uvedený uživatelský účet systému Windows.

    - **Možnost přepsání**: výběrem jedné z následujících možností nakonfigurujete chování, když v cílové složce existuje soubor se stejným názvem:

      - **Přepsat existující soubor novější verzí**
      - **Nepřepisovat existující soubor**
      - **Při přidávání novějších verzí zvyšovat čísla názvů souborů**: Tato možnost připojí číslo k názvu souboru nové sestavy, aby ho lišila od předchozích verzí.

    - **Popis**: Volitelně můžete zadat další informace o odběru sestavy.

1. Na stránce **plán předplatného** vyberte jednu z následujících možností plánu doručení pro odběr sestavy:

    - **Použít sdílený plán**: sdílený plán je dříve definovaný plán, který mohou používat ostatní odběry sestav. Když vyberete tuto možnost, vyberte také sdílený plán. Pokud neexistují žádné sdílené plány, vyberte možnost vytvořit nový plán.

    - **Vytvořit nový plán**: Nakonfigurujte plán, podle kterého se sestava spouští. Plán zahrnuje interval, čas spuštění a datum a koncové datum pro toto předplatné. Ve výchozím nastavení vytvoří nové předplatné nový plán, který se spustí každou hodinu od aktuálního data a času.

1. Na stránce **parametry předplatného** zadejte parametry, které tato sestava vyžaduje pro spuštění bezobslužné instalace. Pokud sestava nemá žádné parametry, průvodce tuto stránku nezobrazuje.

1. Dokončete průvodce.

1. Ověřte, že Configuration Manager úspěšně vytvořil odběr sestavy. Vyberte uzel **předplatná** pro zobrazení a úpravy odběrů sestav.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a>Vytvoření odběru sestavy pro doručení sestavy e-mailem

Když vytvoříte odběr sestavy pro doručení sestavy e-mailem, služba Reporting Services pošle e-mailem příjemcům, které nakonfigurujete. E-mail obsahuje sestavu jako přílohu. Server sestav neověřuje e-mailové adresy ani je nezíská z e-mailového serveru. Můžete odeslat e-mailem sestavy do libovolného platného e-mailového účtu v rámci vaší organizace nebo mimo ni.

> [!NOTE]
> Pokud chcete povolit možnost předplatného **e-mailu** , musíte nakonfigurovat nastavení e-mailu ve službě Reporting Services. Další informace najdete v tématu [doručování e-mailů ve službě Reporting Services](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

Můžete vybrat jednu nebo obě následující možnosti doručení e-mailu:

- Odešle oznámení s odkazem na vygenerovanou sestavu.

- Odešlete vloženou nebo připojenou sestavu. Formát vykreslování a prohlížeč určují, zda budou sestavy vloženy nebo připojeny.

  - Pokud Váš prohlížeč podporuje HTML 4,0 a MHTML a vyberete formát **MHTML (webový archiv)** , e-mail do zprávy vloží zprávu.
  - Všechny ostatní formáty dodávají sestavy jako přílohy.
  - Služba Reporting Services nekontroluje velikost přílohy nebo zprávy předtím, než odešle zprávu. Pokud by příloha nebo zpráva překročila maximální limit povolený poštovním serverem, sestava se nedodá.

Pomocí následujícího postupu můžete vytvořit odběr sestavy pro doručení sestavy pomocí e-mailu.  

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a vyberte uzel **sestavy** .

1. Vyberte složku sestav a potom vyberte sestavu, ke které se chcete přihlásit. Na kartě **Domů** na pásu karet v části **Skupina sestav** vyberte **vytvořit odběr**. Tato akce otevře **Průvodce vytvořením předplatného**.

1. Na stránce **doručení odběru** nakonfigurujte následující nastavení:  

    - **Sestavu doručil**: vyberte **E-mail**.

    - **Komu**: Zadejte platnou e-mailovou adresu jako příjemce.

        > [!NOTE]
        > Chcete-li zadat více příjemců, jednotlivé e-mailové adresy`;`oddělte středníkem ().

    - **CC**: Volitelně můžete zadat e-mailovou adresu pro příjem kopie této sestavy.

    - **Skrytá**: Volitelně můžete zadat e-mailovou adresu pro příjem neskryté kopie této sestavy.

    - **Odpovědět na**: zadejte adresu pro odpověď. Pokud příjemce odpoví na e-mailovou zprávu, odpověď odkazuje na tuto adresu.

    - **Předmět**: Určete řádek předmětu e-mailové zprávy odběru.

    - **Priorita**: Vyberte příznak priority této e-mailové zprávy: **Nízká**, **Normal**nebo **High**. Microsoft Exchange používá tento příznak k označení důležitosti e-mailové zprávy.

    - **Komentář**: zadejte text pro tělo e-mailové zprávy odběru.

    - **Popis**: Volitelně můžete zadat další informace o odběru sestavy.

    - **Zahrnout odkaz**: do textu e-mailové zprávy zadejte adresu URL pro tuto sestavu.

    - **Zahrnout sestavu**: připojit zprávu k e-mailové zprávě Pomocí možnosti **formát vykreslování** Určete formát sestavy, který se má připojit.

    - **Formát vykreslení**: pro připojený soubor sestavy vyberte jeden z následujících formátů:

      - **Soubor XML s daty sestavy**
      - **CSV (oddělený čárkami)**
      - **Soubor TIFF**
      - **Soubor aplikace Acrobat (PDF)**
      - **MHTML (webový archiv)**
      - **Excel**
      - **Word**

1. Na stránce **plán předplatného** vyberte jednu z následujících možností plánu doručení pro odběr sestavy:

    - **Použít sdílený plán**: sdílený plán je dříve definovaný plán, který mohou používat ostatní odběry sestav. Když vyberete tuto možnost, vyberte také sdílený plán. Pokud neexistují žádné sdílené plány, vyberte možnost vytvořit nový plán.

    - **Vytvořit nový plán**: Nakonfigurujte plán, podle kterého se sestava spouští. Plán zahrnuje interval, čas spuštění a datum a koncové datum pro toto předplatné. Ve výchozím nastavení vytvoří nové předplatné nový plán, který se spustí každou hodinu od aktuálního data a času.

1. Na stránce **parametry předplatného** zadejte parametry, které tato sestava vyžaduje pro spuštění bezobslužné instalace. Pokud sestava nemá žádné parametry, průvodce tuto stránku nezobrazuje.

1. Dokončete průvodce.

1. Ověřte, že Configuration Manager úspěšně vytvořil odběr sestavy. Vyberte uzel **předplatná** pro zobrazení a úpravy odběrů sestav.
