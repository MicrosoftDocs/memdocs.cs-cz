---
title: Změny a tipy konzoly Configuration Manager
titleSuffix: Configuration Manager
description: Přečtěte si o změnách konzoly Configuration Manager a tipy pro jejich použití.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0a434f013da48d660efa78f5e2cdca6ced0826d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700714"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Změny a tipy konzoly Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí níže uvedených informací získáte informace o změnách konzoly Configuration Manager a tipů k použití konzoly nástroje:

## <a name="general-tips"></a>Obecné tipy

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Vylepšení hledání konzoly
<!--4640570-->
*(Představené ve verzi 1910)*

- V uzlech **balíčky ovladačů** a **dotazy** můžete použít možnost Hledat **všechny podsložky** .<!--2841181,5424892--> Počínaje verzí 2002 Tato možnost slouží také v uzlech **položky konfigurace** a **standardní hodnoty konfigurace** .<!--5891241-->

- Když hledání vrátí více než 1 000 výsledků, kliknutím na tlačítko **OK** na panelu oznámení zobrazíte další výsledky.<!--4640570-->

    ![Snímek obrazovky s panelem upozornění pro příliš mnoho výsledků hledání](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Výchozí omezení výsledků hledání je 1 000. Tuto výchozí hodnotu můžete změnit. V konzole Configuration Manager otevřete na pásu karet kartu **Hledat** . Ve skupině **Možnosti** vyberte **Nastavení hledání**. Změňte hodnotu **výsledků hledání** . Zobrazení většího počtu výsledků hledání může trvat delší dobu.
    >
    > Ve výchozím nastavení je maximální horní limit 100 000. Pokud chcete tento limit změnit, nastavte hodnotu DWORD **QueryResultCountMaximum** v následujícím klíči registru:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > Nastavení in-Console odpovídá hodnotě **QueryResultCountLimit** ve stejném klíči. Správce může tyto hodnoty nakonfigurovat v podregistru HKLM pro všechny uživatele zařízení. Hodnota HKCU přepisuje nastavení HKLM.

### <a name="role-based-administration-for-folders"></a>Správa na základě rolí pro složky
<!--3600867-->
*(Představené ve verzi 1906)*

Pro složky můžete nastavit rozsahy zabezpečení. Pokud máte přístup k objektu ve složce, ale nemáte přístup ke složce, nebudete moct objekt zobrazit. Podobně platí, že pokud máte přístup do složky, ale ne do objektu, neuvidíte tento objekt. Klikněte pravým tlačítkem myši na složku, zvolte možnost **nastavit rozsahy zabezpečení**a pak zvolte rozsahy zabezpečení, které chcete použít.

### <a name="views-sort-by-integer-values"></a>Zobrazení – seřadit podle celočíselných hodnot

*(Představené ve verzi 1902)*

Provedli jsme vylepšení způsobu řazení dat v různých zobrazeních. Například v uzlu **nasazení** pracovního prostoru **monitorování** nyní následující sloupce seřadí jako čísla namísto řetězcových hodnot:  

- Počet chyb
- Počet probíhajících
- Jiné číslo
- Počet úspěchů
- Neznámé číslo  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Přesunutí upozornění na velký počet výsledků

*(Představené ve verzi 1902)*

Když v konzole vyberete uzel, který vrátí více než 1 000 výsledků, Configuration Manager zobrazí následující upozornění:

> Configuration Manager vrátil velký počet výsledků. Výsledky můžete zúžit pomocí vyhledávání. Případně můžete kliknutím sem zobrazit maximálně 100000 výsledků.

Mezi tímto upozorněním a polem hledání je teď další prázdné místo. Tento přesun pomáhá zabránit nechtěnému výběru upozornění pro zobrazení dalších výsledků.

### <a name="send-feedback"></a>Váš názor

*(Představené ve verzi 1806)*
<!--1357542-->

Odešlete zpětnou vazbu produktu z konzoly.  

- **Poslat smajlíka**: pošlete nám svůj názor na to, co se vám líbí.  

- **Odeslání zamračení**: pošlete nám svůj názor na to, co jste nechtěli.  

- **Odeslání návrhu**: přejdete na UserVoice, abyste mohli sdílet svůj nápad.  

Další informace najdete v tématu o [zpětné vazbě produktu](../../understand/find-help.md#BKMK_1806Feedback).


## <a name="assets-and-compliance-workspace"></a>Pracovní prostor prostředky a kompatibilita

### <a name="real-time-actions-from-device-lists"></a>Akce ze seznamů zařízení v reálném čase
<!--4616810-->
*(Představené ve verzi 1906)*

Existují různé způsoby, jak zobrazit seznam zařízení v uzlu **zařízení** v pracovním prostoru **prostředky a kompatibilita** .

- V pracovním prostoru **prostředky a kompatibilita** vyberte uzel **kolekce zařízení** . Vyberte kolekci zařízení a zvolte akci pro **zobrazení členů**. Tato akce otevře dílčí uzel uzlu **zařízení** se seznamem zařízení pro tuto kolekci.  

  - Když vyberete dílčí uzel kolekce, můžete nyní začít **CMPivot** ze skupiny kolekcí na pásu karet.  

- V pracovním prostoru **monitorování** vyberte uzel **nasazení** . Vyberte nasazení a na pásu karet zvolte akci **Zobrazit stav** . V podokně Stav nasazení dvakrát klikněte na celkový počet assetů, aby bylo možné přejít k seznamu zařízení.  

  - Když v tomto seznamu vyberete zařízení, teď můžete začít **CMPivot** a **spouštět skripty** ze skupiny zařízení na pásu karet.  


### <a name="collections-tab-in-devices-node"></a>Karta kolekce v uzlu zařízení
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **prostředky a kompatibilita** , přejít na uzel **zařízení** a vyberte zařízení. V podokně podrobností přepněte na kartu nové **kolekce** . Tato karta obsahuje seznam kolekcí, které zahrnují toto zařízení. 

> [!Note]  
> - Tato karta není momentálně k dispozici v poduzlu zařízení v uzlu **kolekce zařízení** . Například když vyberete možnost **zobrazení členů** v kolekci.
> - Tato karta se pro některé uživatele nemusí naplnit očekávaným způsobem. Úplný seznam kolekcí, do kterých zařízení patří, zobrazíte tak, že musíte mít roli zabezpečení **správce s úplnými oprávněními** . Jedná se o známý problém. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Přidat sloupec SMBIOS GUID do uzlů kolekce zařízení a zařízení

*(Představené ve verzi 1906)*

<!--4526580-->
V uzlech kolekce **zařízení** a **zařízení** teď můžete přidat nový sloupec pro **identifikátor SMBIOS GUID**. Tato hodnota je stejná jako vlastnost **GUID systému BIOS** třídy systémového prostředku. Je to jedinečný identifikátor hardwaru zařízení.

### <a name="search-device-views-using-mac-address"></a>Prohledat zobrazení zařízení pomocí adresy MAC

<!--3600878-->
*(Představené ve verzi 1902)*

Adresu MAC můžete vyhledat v zobrazení zařízení konzoly Configuration Manager. Tato vlastnost je užitečná pro Správce nasazení operačního systému při řešení potíží s nasazeními založenými na technologii PXE. Když si zobrazíte seznam zařízení, přidejte do zobrazení sloupec **adresa MAC** . Pomocí vyhledávacího pole přidejte kritéria hledání **adresy MAC** .

### <a name="view-users-for-a-device"></a>Zobrazit uživatele pro zařízení

Počínaje verzí 1806 jsou v uzlu **zařízení** k dispozici následující sloupce:  

- **Počet primárních uživatelů:** <!--1357280-->  

- **Aktuálně přihlášený uživatel** <!--1358202-->  

    > [!NOTE]  
    > Zobrazení aktuálně přihlášeného uživatele vyžaduje [zjišťování uživatelů](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) a [spřažení uživatelských zařízení](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Další informace o tom, jak zobrazit jiný než výchozí sloupec, najdete v tématu [Jak používat konzolu pro správu](admin-console.md#columns).

### <a name="improvement-to-device-search-performance"></a>Zlepšení výkonu hledání zařízení

<!-- 3614690 -->
Počínaje verzí 1806 při hledání v kolekci zařízení nehledá klíčové slovo u všech vlastností objektu. Pokud nejste konkrétní informace o tom, co hledat, vyhledává se v následujících čtyřech vlastnostech:

- Název
- Počet primárních uživatelů:
- Aktuálně přihlášený uživatel
- Jméno posledního přihlášeného uživatele

Toto chování významně zlepšuje čas potřebný k hledání podle názvu, zejména ve velkém prostředí. Tato změna neovlivní vlastní vyhledávání podle konkrétních kritérií.


## <a name="software-library-workspace"></a>Pracovní prostor knihovny softwaru

### <a name="order-by-program-name-in-task-sequence"></a>Seřadit podle názvu programu v pořadí úkolů
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** . Upravte pořadí úkolů a vyberte nebo přidejte krok [instalovat balíček](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) . Pokud má balíček více než jeden program, rozevírací seznam nyní Seřadí programy abecedně.

### <a name="task-sequences-tab-in-applications-node"></a>Karta pořadí úloh v uzlu aplikace
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**, pak přejít do uzlu **aplikace** a vyberte aplikaci. V podokně podrobností přepněte na kartu nové **pořadí úkolů** . Tato karta obsahuje pořadí úloh, která odkazují na tuto aplikaci.

### <a name="drill-through-required-updates"></a>Podrobné informace o požadovaných aktualizacích
<!--4224414-->
*(Představené ve verzi 1906)*

1. V konzole Configuration Manager klikněte na jedno z následujících míst:

   - **Softwarová knihovna**  >  **Aktualizace softwaru**  >  **Všechny aktualizace softwaru**
   - **Softwarová knihovna**  >  **Údržba**  >  Windows 10 **Všechny aktualizace Windows 10**
   - **Softwarová knihovna**  >  Správa klientů Office **365**  >  **Aktualizace Office 365**

1. Vyberte jakoukoli aktualizaci, kterou vyžaduje aspoň jedno zařízení.
1. Podívejte se na kartu **Souhrn** a v části  **Statistika**Najděte výsečový graf.
1. Pokud chcete přejít k podrobnostem seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu.
1. Tato akce přejde na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci. Můžete také provést akce pro uzel, jako je například vytvoření nové kolekce ze seznamu.

> [!NOTE]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

### <a name="maximize-the-browse-registry-window"></a>Maximalizace okna Procházet Registry

<!--3594151 includes all MMS 1902 console changes-->
*(Představené ve verzi 1902)*

1. V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .
1. Vyberte aplikaci, která má typ nasazení s metodou detekce. Například metoda zjišťování Instalační služba systému Windows.
1. V podokně podrobností přepněte na kartu **typy nasazení** .
1. Otevřete vlastnosti typu nasazení a přepněte na kartu **Metoda zjišťování** . Vyberte možnost **Přidat klauzuli**.
1. Změňte **Typ nastavení** na **registr** a kliknutím na **Procházet** otevřete okno **Procházet registr** . Nyní můžete toto okno maximalizovat.  

### <a name="edit-a-task-sequence-by-default"></a>Upravit pořadí úkolů ve výchozím nastavení

*(Představené ve verzi 1902)*

V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** . **Upravit** je nyní výchozí akce při otevírání pořadí úkolů. Předchozí akce byla dříve nastavena na **vlastnosti**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Přejít na kolekci z nasazení aplikace

*(Představené ve verzi 1902)*

1. V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .
1. Vyberte aplikaci. V podokně podrobností přepněte na kartu **nasazení** .
1. Vyberte nasazení a pak na pásu karet na kartě nasazení zvolte možnost Nová **kolekce** . Tato akce přepne zobrazení do kolekce, která je cílem nasazení.
   - Tato akce je k dispozici také v místní nabídce na nasazení v tomto zobrazení.


## <a name="monitoring-workspace"></a>Pracovní prostor monitorování

### <a name="correct-names-for-client-operations"></a>Správné názvy pro klientské operace
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **monitorování** vyberte **operace klientů**. Operace **Přepnutí na další bod aktualizace softwaru** je nyní správně pojmenována.

### <a name="show-collection-name-for-scripts"></a>Zobrazit název kolekce pro skripty
<!--4616810-->
*(Představené ve verzi 1906)*

V pracovním prostoru **monitorování** vyberte uzel **stav skriptu** . Kromě ID teď obsahuje i **název kolekce** .

### <a name="remove-content-from-monitoring-status"></a>Odebrat obsah ze stavu monitorování

*(Představené ve verzi 1902)*

1. V pracovním prostoru **monitorování** rozbalte možnost **stav distribuce**a vyberte **stav obsahu**.
1. Vyberte položku v seznamu a na pásu karet zvolte možnost **Zobrazit stav** .
1. V podokně Podrobnosti o aktivech klikněte pravým tlačítkem myši na distribuční bod a vyberte novou možnost **Odebrat**. Tato akce odebere obsah z vybraného distribučního bodu.

### <a name="copy-details-in-monitoring-views"></a>Kopírovat podrobnosti v zobrazeních monitorování

*(Představené ve verzi 1806)*
<!--1357856-->
Informace o kopírování najdete v podokně **Podrobnosti o aktivech** v následujících uzlech monitorování:  

- **Stav distribuce obsahu**  

- **Stav nasazení**  

![Zobrazení stavu nasazení, kopírování podrobností prostředků](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Pracovní prostor pro správu

<!--4223683-->
Počínaje verzí 1906 můžete povolit některé uzly pod uzlem **zabezpečení** , aby používaly službu pro správu. Tato změna umožňuje konzole komunikovat s poskytovatelem serveru SMS přes protokol HTTPS místo přes rozhraní WMI. Další informace najdete v tématu [nastavení služby správy](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Další kroky

- [Použití konzoly](admin-console.md)
- [Oznámení ke konzole](admin-console-notifications.md)
- [Funkce pro usnadnění přístupu](../../understand/accessibility-features.md)