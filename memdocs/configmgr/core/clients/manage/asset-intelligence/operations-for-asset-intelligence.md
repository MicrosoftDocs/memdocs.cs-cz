---
title: Použití funkce Asset Intelligence
titleSuffix: Configuration Manager
description: Proveďte běžné úkoly funkce Asset Intelligence v Configuration Manager.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1e272e8e71ceaa15c712cb3a53d9db835747d327
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714168"
---
# <a name="how-to-use-asset-intelligence-in-configuration-manager"></a>Použití funkce Asset Intelligence v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje informace, které vám pomůžou se správou typických úloh funkce Asset Intelligence v hierarchii Configuration Manager:  

##  <a name="view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Zobrazení informací funkce Asset Intelligence  
 Informace funkce Asset Intelligence můžete zobrazit na domovské stránce **Asset Intelligence** a v sestavách Asset Intelligence.  

###  <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Domovská stránka funkce Asset Intelligence  
 Domovská stránka funkce **Asset Intelligence** obsahuje souhrnný řídicí panel s informacemi z katalogu Asset Intelligence. Na domovské stránce můžete zjistit informace o synchronizaci katalogu a stavu inventarizovaného softwaru. Domovská stránka funkce **Asset Intelligence** se dělí na tyto části:  

- **Synchronizace katalogu**: Obsahuje informace o tom, jestli je funkce Asset Intelligence povolená, aktuální stav bodu synchronizace katalogu Asset Intelligence, plán synchronizace, stav importu licenční smlouvy zákazníka, čas poslední aktualizace stavu a čas příští plánované aktualizace a počet změn, ke kterým došlo po instalaci systému lokality bodu synchronizace katalogu Asset Intelligence.  

  > [!NOTE]  
  >  Část synchronizace katalogu Asset Intelligence na domovské stránce funkce **Asset Intelligence** se zobrazí jenom v případě, že je nainstalovaná role systému lokality bodu synchronizace katalogu Asset Intelligence.  

- **Stav inventarizovaného softwaru**: Obsahuje počet a procento inventarizovaného softwaru, kategorie softwaru a rodiny softwaru, které jsou určené Microsoftem, určené administrativním uživatelem, čekají na online identifikaci nebo jsou neidentifikované a nejsou ve stavu čekání. Informace zobrazené v tabulkovém formátu udávají počty v jednotlivých skupinách, zatímco informace v grafu znázorňují příslušná procenta.  

  Následující postup slouží k zobrazení informací funkce Asset Intelligence na domovské stránce funkce **Asset Intelligence** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Zobrazení informací funkce Asset Intelligence na domovské stránce funkce Asset Intelligence  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**. Zobrazí se sestavy katalogu Asset Intelligence.  

###  <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Sestavy funkce Asset Intelligence  
 Existuje přes 60 sestav katalogu Asset Intelligence, které zobrazují informace shromážděné funkcí Asset Intelligence. Řada z nich odkazuje na podrobnější sestavy, ve kterých se můžete dotazovat na obecné informace a potom přejít na podrobnější údaje. Sestavy funkce Asset Intelligence jsou umístěny v konzole Configuration Manager v pracovním prostoru **monitorování** v uzlu **vytváření sestav** . Tyto sestavy poskytují informace o hardwaru, správě licencí a softwaru. Další informace o sestavách v Configuration Manager najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Přesnost množství nainstalovaných softwarových titulů a informací o licencích uvedených v sestavách katalogu Asset Intelligence se může lišit od skutečného počtu nainstalovaných softwarových titulů nebo licencí používaných v daném prostředí z důvodu složitých závislostí a omezení, která souvisí s inventarizací informací o softwarových licencích k softwarovým titulům nainstalovaným v podnikovém prostředí. Sestavy katalogu Asset Intelligence by neměly při zjišťování toho, jestli zakoupené softwarové licence odpovídají předpisům, sloužit jako jediný zdroj informací.  

 Pomocí následujícího postupu můžete zobrazit informace funkce Asset Intelligence s využitím sestav katalogu Asset Intelligence.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Zobrazení informací funkce Asset Intelligence pomocí sestav katalogu Asset Intelligence  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru **Sledování** rozbalte možnost **Vytváření sestav**, rozbalte **Sestavy**a potom klikněte na **Asset Intelligence**. Zobrazí se sestavy katalogu Asset Intelligence.  

    > [!WARNING]  
    >  Pokud uzel **Sestavy** neobsahuje žádné složky sestav, zkontrolujte, jestli jste nakonfigurovali vytváření sestav. Další informace najdete v tématu [Konfigurace generování sestav](../../../../core/servers/manage/configuring-reporting.md).  

3.  Vyberte sestavu katalogu Asset Intelligence, kterou chcete spustit, a potom na kartě **Domů** ve skupině **Skupina sestav** klikněte na **Spustit**.  

##  <a name="synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a>Synchronizace katalogu funkce Asset Intelligence  
 Místní katalog Asset Intelligence můžete synchronizovat s katalogem System Center Online, aby se načetla nejnovější kategorizace softwarových titulů. Když ručně zadáte požadavek na synchronizaci katalogu s katalogem System Center Online, může proces synchronizace s katalogem System Center Online trvat 15 minut nebo i delší dobu. Configuration Manager aktualizuje nastavení **poslední úspěšné aktualizace** na domovské stránce **funkce Asset Intelligence** s aktuálním časem, kdy se synchronizace úspěšně dokončí.  

> [!NOTE]  
>  Před použitím těchto postupů je nejdřív potřeba nainstalovat roli systému lokality bodu synchronizace katalogu Asset Intelligence. Informace o instalaci bodu synchronizace funkce Asset Intelligence najdete v tématu [konfigurace funkce Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Pomocí následujícího postupu můžete vytvořit plán synchronizace katalogu Asset Intelligence.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Vytvoření plánu synchronizace katalogu Asset Intelligence  

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**.  

3. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Synchronizovat**a potom klikněte na **Naplánovat synchronizaci**.  

4. V dialogu **Plán bodu synchronizace katalogu Asset Intelligence** vyberte **Povolit synchronizaci s plánem**a potom nakonfigurujte jednoduchý nebo vlastní plán.  

5. Klikněte na tlačítko **OK** a uložte změny.  

   > [!NOTE]  
   >  Informace o plánu synchronizace, včetně další plánované synchronizace, najdete v uzlu **Asset Intelligence** v pracovním prostoru **Prostředky a kompatibilita** v lokalitě nejvyšší úrovně v hierarchii.  

   Pomocí následujícího postupu můžete ručně synchronizovat katalog Asset Intelligence.  

> [!WARNING]  
>  Katalog System Center Online přijme jenom jeden manuální požadavek na synchronizaci za 12 hodin.  

###  <a name="to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> Ruční synchronizace katalogu Asset Intelligence  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**.  

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Synchronizovat**, na **Synchronizovat katalog Asset Intelligence**a potom na **OK**.  

##  <a name="customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a>Přizpůsobení katalogu funkce Asset Intelligence  
 Informace o kategoriích katalogu Asset Intelligence získané z katalogu System Center Online se ukládají do databáze lokality s oprávněním jenom ke čtení a nedají se upravit ani odstranit. V katalogu ale můžete vytvářet, upravovat a odstraňovat vlastní kategorie softwaru, rodiny softwaru, popisky softwaru a požadavky na hardware. Potom můžete ve stávajících nebo uživatelem definovaných informacích o softwarových titulech použít vlastní kategorizační údaje namísto informací získaných z katalogu System Center Online. Pokud změníte nebo přidáte informace o kategoriích, budou se informace katalogu považovat za definované uživatelem. Uživatelem definovaných informace o kategoriích se ukládají do jiných databázových tabulek než ověřené informace z katalogu.  

###  <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a>Kategorie softwaru  
 Kategorie softwaru ve funkci Asset Intelligence slouží k širší kategorizaci inventarizovaných softwarových titulů a používají se také k obecnému seskupení více konkrétních rodin softwaru. Kategorie softwaru může sdružovat třeba energetické společnosti a v rámci této kategorie softwaru může existovat rodina softwaru pro ropné a plynařské společnosti nebo vodní elektrárny. Katalog Asset Intelligence obsahuje řadu předdefinovaných kategorií softwaru a dají se vytvářet i další, uživatelem definované kategorie, které dále určují inventarizovaný software. Stav ověření všech předdefinovaných kategorií softwaru je vždycky **Ověřeno**, kdežto informace o vlastních kategoriích softwaru přidaných do katalogu Asset Intelligence mají stav **Definovaný uživatelem**.  

 Pomocí následujícího postupu můžete vytvořit kategorii softwaru definovanou uživatelem.  

##### <a name="to-create-a-user-defined-software-category"></a>Vytvoření kategorie softwaru definované uživatelem  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Katalog**.  

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit kategorii softwaru**.  

4.  Na stránce **Obecné** zadejte název nové kategorie softwaru a volitelně také popis.  

    > [!NOTE]  
    >  Stav ověření všech nových vlastních kategorií softwaru je vždycky nastavený na **Definovaný uživatelem**.  

     Klikněte na **Další**.  

5.  Na stránce **Souhrn** zkontrolujte nastavení a klikněte na **Další**.  

6.  Na stránce **Dokončení** klikněte na tlačítko **Zavřít** a opusťte průvodce.  

###  <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Rodiny softwaru  
 Rodiny softwaru ve funkci Asset Intelligence slouží k dalšímu rozdělení inventarizovaných softwarových titulů v rámci kategorií softwaru. Kategorie softwaru může sdružovat třeba energetické společnosti a v rámci této kategorie softwaru může existovat rodina softwaru pro ropné a plynařské společnosti nebo vodní elektrárny. Katalog Asset Intelligence obsahuje řadu předdefinovaných rodin softwaru a dají se vytvářet i další, uživatelem definované rodiny, které určují inventarizovaný software. Stav ověření všech předdefinovaných rodin softwaru je vždycky **Ověřeno**, kdežto informace o vlastních rodinách softwaru přidaných do katalogu Asset Intelligence mají stav **Definovaný uživatelem**.  

 Pomocí následujícího postupu můžete vytvořit rodinu softwaru definovanou uživatelem.  

##### <a name="to-create-a-user-defined-software-family"></a>Vytvoření rodiny softwaru definované uživatelem  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Katalog**.  

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit rodinu softwaru**.  

4.  Na stránce **Obecné** zadejte název nové rodiny softwaru a volitelně také popis.  

    > [!NOTE]  
    >  Stav ověření všech nových vlastních rodin softwaru je vždycky nastavený na **Definovaný uživatelem**.  

5.  Na stránce **Souhrn** zkontrolujte nastavení a klikněte na **Další**.  

6.  Na stránce **Dokončení** klikněte na tlačítko **Zavřít** a opusťte průvodce.  

###  <a name="software-labels"></a><a name="BKMK_SoftwareLabels"></a> Popisky softwaru  
 Vlastní popisky softwaru ve funkci Asset Intelligence umožňují vytvářet filtry, pomocí kterých se dají seskupovat softwarové tituly. Ty pak můžete zobrazit pomocí sestav katalogu Asset Intelligence. Můžete třeba vytvořit popisek softwaru s názvem Shareware, přidružit ho k řadě aplikací a potom spustit sestavu, která vám zobrazí všechny tituly s popiskem softwaru Shareware. Stav ověření všech vlastních popisků softwaru, které přidáte do katalogu Asset Intelligence, je **Definovaný uživatelem** .  

 Pomocí následujícího postupu můžete vytvořit popisek softwaru definovaný uživatelem.  

##### <a name="to-create-a-user-defined-software-label"></a>Vytvoření popisku softwaru definovaného uživatelem  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Katalog**.  

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit popisek softwaru**.  

4.  Na stránce **Obecné** zadejte název nové rodiny softwaru a volitelně také popis.  

    > [!NOTE]  
    >  Stav ověření všech nových vlastních popisků softwaru je vždycky nastavený na **Definovaný uživatelem**.  

5.  Na stránce **Souhrn** zkontrolujte nastavení a klikněte na **Další**.  

6.  Na stránce **Dokončení** klikněte na tlačítko **Zavřít** a opusťte průvodce.  

###  <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Požadavky na hardware  
 Informace o požadavcích na hardware vám můžou pomoct zkontrolovat, jestli počítače splňují hardwarové požadavky softwarových titulů dřív, než se stanou cílem nasazení softwaru. Katalog Asset Intelligence obsahuje řadu předdefinovaných požadavků na hardware a dají se vytvářet i nové, uživatelem definované informace o požadavcích na hardware, které vyhovují konkrétním požadavkům. Stav ověření všech předdefinovaných požadavků na hardware je vždycky **Ověřeno**, kdežto informace o vlastních požadavcích na hardware přidaných do katalogu Asset Intelligence mají stav **Definovaný uživatelem**.  

> [!IMPORTANT]  
>  Požadavky na hardware zobrazené v konzole Configuration Manager jsou načteny z katalogu funkce Asset Intelligence v místním počítači a nejsou založené na informacích o softwarovém titulu v inventáři z klienta System Center 2012 Configuration Manager. Informace o požadavcích na hardware se neaktualizují v rámci procesu synchronizace s katalogem System Center Online. Můžete vytvořit uživatelem definované požadavky na hardware pro inventarizovaný software, ke kterému nejsou přidružené požadavky na hardware.  

 Pomocí následujícího postupu můžete vytvořit požadavek na hardware definovaný uživatelem.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Vytváření požadavků na hardware definovaných uživatelem  

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Hardwarové požadavky**.  

3. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit hardwarové požadavky**.  

4. Na stránce **Obecné** zadejte následující informace:  

   1. **Softwarový titul**: Určuje softwarový titul, ke kterému chcete hardwarové požadavky přidružit. Nesmí se jednat o softwarový titul, který už existuje v katalogu Asset Intelligence.  

   2. **Stav ověření**: Zobrazí stav ověření hardwarových požadavků **Definovaný uživatelem** . Toto nastavení nelze změnit.  

   3. **Minimální kmitočet CPU (MHz)**: Určuje minimální rychlost procesoru v megahertzích (MHz) vyžadovanou softwarovým titulem.  

   4. **Minimální velikost RAM (KB)**: Určuje minimální velikost paměti RAM v kilobajtech (KB) vyžadovanou softwarovým titulem.  

   5. **Minimální místo na disku (KB)**: Určuje minimální velikost volného místa na disku v kilobajtech (KB) vyžadovanou softwarovým titulem.  

   6. **Minimální velikost disku (KB)**: Určuje minimální velikost pevného disku v kilobajtech (kB) vyžadovanou softwarovým titulem.  

      Klikněte na **Další**.  

5. Na stránce **Souhrn** zkontrolujte nastavení a klikněte na **Další**.  

6. Na stránce **Dokončení** klikněte na tlačítko **Zavřít** a opusťte průvodce.  

###  <a name="modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a>Úprava informací o kategorizaci pro software v inventáři  
 Předdefinovaný software v katalogu Asset Intelligence má nakonfigurované určité informace o kategorizaci, třeba název produktu, výrobce, kategorii softwaru a rodinu softwaru. Pokud předdefinované informace o kategorizaci nevyhovují vašim požadavkům, můžete je ve vlastnostech softwarového titulu změnit. Když upravíte informace o kategorizaci předdefinovaného softwaru, stav ověření daného softwaru se změní z **Ověřeno** na **Definovaný uživatelem**.  

> [!IMPORTANT]  
>  Informace o kategorizaci se dají upravovat jenom v lokalitě nejvyšší úrovně.  

 Pomocí následujícího postupu můžete upravit informace o kategorizaci softwaru v inventáři.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Úprava kategorizace softwarových titulů  

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Inventarizovaný software**.  

3. Vyberte jeden nebo více softwarových titulů, u kterých chcete změnit kategorizaci.  

4. Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

5. Na kartě **Obecné** můžete upravit tyto informace o kategorizaci:  

   -   **Název produktu**: Určuje název inventarizovaného softwarového titulu.  

   -   **Dodavatel**: Určuje název výrobce, který vyvinul inventarizovaný softwarový titul.  

   -   **Kategorie**: Určuje kategorii softwaru, která je aktuálně přiřazená k inventarizovanému softwarovému titulu.  

   -   **Rodina**: Určuje rodinu softwaru, která je aktuálně přiřazená k inventarizovanému softwarovému titulu.  

6. Klikněte na tlačítko **OK** a uložte změny.  

   Pomocí následujícího postupu můžete obnovit původní informace o kategorizaci softwaru v inventáři.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Obnovení původních informací o kategorizaci softwaru  
 Configuration Manager ukládá informace o kategorizaci získané ze služby System Center Online v databázi. Tyto informace se nedají odstranit. Když tyto informace upravíte, můžete později obnovit původní informace o kategorizaci z katalogu System Center Online. Původní nastavení se dá obnovit i u inventarizovaného softwaru, který není v katalogu Asset Intelligence.  

 Pomocí následujícího postupu můžete obnovit původní nastavení informací o kategorizaci.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Obnovení původního nastavení informací o kategorizaci  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Inventarizovaný software**.  

3.  Vyberte jeden nebo více softwarových titulů, u kterých chcete obnovit původní nastavení. Nastavení se dá obnovit jenom u softwaru ve stavu **Definovaný uživatelem** .  

    > [!TIP]  
    >  Kliknutím na sloupec **Stav** seřadíte položky podle stavu ověření. Řazení umožňuje zobrazit všechen software podle stavu ověření a rychle vybrat více položek, u kterých chcete obnovit původní nastavení.  

4.  Na kartě **Domů** ve skupině **Produkt** klikněte na **Původní**.  

5.  Kliknutím na **Ano** obnovíte u softwaru původní informace o kategorizaci.  

6.  Po obnovení původních informací o kategorizaci softwaru, který je v katalogu Asset Intelligence, se změní stav ověření z **Definovaný uživatelem** na **Ověřeno**. Po obnovení původních informací o softwaru, který není součástí katalogu, se stav ověření změní z **Definovaný uživatelem** na **Nezařazeno**.  

##  <a name="request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a>Požadavek na aktualizaci katalogu pro Nezařazeno do kategorie softwarové tituly  
 Informace o nezařazených softwarových titulech se dají odeslat do katalogu System Center Online k prozkoumání a kategorizaci. Když odešlete nezařazený softwarový titul a zároveň o jeho kategorizaci požádají aspoň 4 zákazníci, odborníci určí, kategorizují a potom zpřístupní informace o kategorizaci tohoto softwarového titulu všem zákazníkům, kteří používají službu System Center Online. Společnost Microsoft přikládá nejvyšší prioritu softwarovým titulům, které mají nejvíce požadavků na kategorizaci. Není moc pravděpodobné, že by svou kategorii dostal vlastní software a obchodní aplikace, a doporučujeme takové softwarové tituly vůbec neposílat Microsoftu ke kategorizaci.  

 Při odeslání informací o softwarovém titulu ke kategorizaci do služby System Center Online platí tyto podmínky:  

-   Do služby System Center Online se zanesou jenom základní informace o softwarovém titulu a informace o softwarovém titulu ke kategorizaci můžou před zařazením procházet kontrolou.  

-   Informace o licencích na software se nikdy nepřenáší.  

-   Všechny odeslané softwarové tituly budou veřejně dostupné v rámci katalogu System Center Online a můžou si je stáhnout jiní zákazníci.  

-   Do katalogu System Center Online se neuloží zdroj softwarového titulu. Ke kategorizaci do katalogu System Center Online by se ale neměly odesílat aplikace, které obsahují důvěrné nebo soukromé informace.  

> [!NOTE]  
>  Další informace o funkce Asset Intelligence informacích o ochraně osobních údajů najdete v tématu [zabezpečení a ochrana osobních údajů pro funkce Asset Intelligence](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Pomocí následujícího postupu můžete odeslat požadavek na kategorizaci softwarového titulu z katalogu Asset Intelligence do služby System Center Online.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Požadavek na aktualizaci katalogu o nezařazené softwarové tituly  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Inventarizovaný software**.  

3.  Vyberte jeden nebo více názvů produktů, které chcete odeslat do katalogu System Center Online ke kategorizaci. Do katalogu System Center Online se dají ke kategorizaci odesílat jenom nezařazené softwarové tituly v inventáři. Pokud správce kategorizoval softwarový titul v inventáři a způsobil tak změnu stavu na Definovaný uživatelem, musíte na inventarizovaný softwarový titul kliknout pravým tlačítkem myši a kliknutím na **Původní** ho vrátit do stavu **Nezařazeno** . Teprve pak ho můžete odeslat ke kategorizaci do katalogu System Center Online.  

    > [!NOTE]  
    >  Configuration Manager může po určitou dobu zpracovat až 2000 softwarových titulů pro kategorizaci. Pokud vyberete více než 2000 softwarových titulů, zpracuje se jenom prvních 2000 softwarových titulů. Zbývající softwarové tituly musíte vybrat ke kategorizaci v dávkách po méně než 2000.  

    > [!TIP]  
    >  Kliknutím na sloupec **Stav** seřadíte položky podle stavu ověření. To vám umožní zobrazit všechny nezařazené názvy produktů a rychle vybrat více položek, které chcete odeslat ke kategorizaci.  

4.  Na kartě **Domů** ve skupině **Produkt** klikněte na **Vyžádat aktualizaci katalogu**.  

5.  Přečtěte si sdělení o ochraně osobních údajů při odeslání ke kategorizaci do katalogu System Center Online. Kliknutím na **Podrobnosti** zobrazíte informace, které se odešlou do katalogu System Center Online.  

6.  Vyberte **Tuto zprávu jsem přečetl(a) a rozumím jí**a potom kliknutím na **OK** povolte odeslání vybraných softwarových titulů ke kategorizaci.  

7.  Zkontrolujte, jestli se stav inventarizovaných softwarových produktů odeslaných ke kategorizaci do katalogu System Center Online změnil z **Nezařazeno** na **Čekající**.  

    > [!NOTE]  
    >  Software odeslaný ke kategorizaci do katalogu System Center Online má v lokalitě centrální správy stav ověření **Čekající** , ale v podřízených primárních lokalitách se u něj pořád zobrazuje stav ověření **Nezařazeno** .  

##  <a name="resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a> Řešení konfliktů podrobných informací o softwaru  
 Po přijetí nově aktualizovaných podrobností o kategorizaci softwaru z katalogu System Center Online, které jsou v konfliktu se stávajícími podrobnými informacemi o softwaru, si můžete vybrat, jak chcete konflikt vyřešit. Software s aktuálním konfliktem má stav ověření **S možností aktualizace**. Po vyřešení konfliktu podrobností o softwaru se do katalogu Asset Intelligence uloží to nastavení informací o kategorizaci softwaru, které určíte. U stejné hodnoty kategorizace softwaru nemůže znovu dojít ke konfliktu podrobností o softwaru, ledaže by se po vyřešení konfliktu změnila hodnota v katalogu System Center Online.  

 Konflikt podrobností o softwaru můžete vyřešit pomocí následujícího postupu.  

#### <a name="to-resolve-a-software-details-conflict"></a>Řešení konfliktu podrobných informací o softwaru  

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na **Asset Intelligence**a potom na **Inventarizovaný software**.  

3. Ve sloupci **Stav** vyhledejte softwarové tituly ve stavu **S možností aktualizace** .  

4. Vyberte softwarový titul, pro který chcete vyřešit konflikt, a potom na kartě **Domů** ve skupině **Produkt** klikněte na **Vyřešit konflikt**.  

5. Zkontrolujte tyto informace:  

   -   **Místní hodnota**: Určuje stávající informace o kategorizaci softwaru v katalogu Asset Intelligence, které jsou v konfliktu s novějšími podrobnostmi o kategorizaci softwaru v katalogu System Center Online.  

   -   **Stažená hodnota**: Udává nové informace o kategorizaci softwaru v katalogu System Center Online v souvislosti s konfliktními informaci o kategorizaci softwaru v katalogu Asset Intelligence.  

6. Vyberte jedno z těchto nastavení, které určuje, jak vyřešit konflikt podrobností o softwaru:  

   - **Neměnit informační hodnotu v místně upravovaném katalogu**: Vyřeší konflikt podrobností o softwaru tak, že zachová stávající informace o kategorizaci softwaru v katalogu Asset Intelligence. Pokud vyberete toto nastavení, stav softwarového titulu se změní z hodnoty **S možností aktualizace** na **Definovaný uživatelem**.  

   - **Přepsat informační hodnotu v místně upravovaném katalogu hodnotou z katalogu System Center Online**: Vyřeší konflikt podrobností o softwaru tak, že přepíše stávající informace o kategorizaci softwaru v katalogu Asset Intelligence a nahradí je novými informacemi získanými z katalogu System Center Online. Pokud vyberete toto nastavení, stav softwarového titulu se změní z hodnoty **S možností aktualizace** na **Ověřeno**.  

     Uložte řešení konfliktu kliknutím na **OK** .  
