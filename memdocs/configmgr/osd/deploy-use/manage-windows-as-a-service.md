---
title: Správa Windows jako služby
titleSuffix: Configuration Manager
description: Pomocí Configuration Manager můžete zobrazit stav Windows as a Service (použijete model WAAS), vytvářet plány údržby a zobrazovat výstrahy, když se klienti s Windows 10 blíží konci podpory.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710836"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Správa Windows jako služby pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager můžete ve svém prostředí zobrazit stav Windows as a Service (použijete model WAAS). Vytvořte si plány údržby, které tvoří okruhy nasazení a zajistěte, aby byly systémy Windows 10 při vydání nových sestavení stále v aktuálním stavu. Můžete také zobrazit výstrahy, když se klienti s Windows 10 blíží konci podpory pro své pololetní sestavení kanálu.

Další informace o možnostech údržby Windows 10 najdete v tématu [Přehled Windows jako služby](/windows/deployment/update/waas-overview#servicing-channels).

Pomocí následujících částí můžete spravovat Windows jako službu.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a>Požadovaný

Chcete-li zobrazit data na řídicím panelu údržby Windows 10, je nutné provést následující akce:

- Počítače s Windows 10 musí používat Configuration Manager aktualizace softwaru s Windows Server Update Services (WSUS) pro správu aktualizací softwaru. Když počítače používají pro správu aktualizací softwaru web Windows Update pro firmy (nebo Windows Insider), počítač se nevyhodnotí v plánech údržby Windows 10. Další informace najdete v tématu [Integrace s Windows Update for Business ve Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Použijte podporovanou verzi služby WSUS:
  - Služba WSUS 10.0.14393 (role ve Windows serveru 2016)
  - Služba WSUS 10.0.17763 (role ve Windows serveru 2019) (vyžaduje Configuration Manager 1810 nebo novější)
  - WSUS 6,2 a 6,3 (role v systému Windows Server 2012 a Windows Server 2012 R2)
    - Ve službě WSUS 6,2 a 6,3 [musí být nainstalována znalostní báze kb 3095113 a kb 3159706 (nebo ekvivalentní aktualizace)](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) .

- Povolte zjišťování prezenčního signálu. Údaje zobrazené na řídicím panelu údržby Windows 10 se najdou pomocí zjišťování. Další informace najdete v tématu [Konfigurace zjišťování prezenčního signálu](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    V následujících atributech jsou zjištěny a uloženy následující informace o kanálu Windows 10 a jejich sestavení:  

    - **Větev připravenosti na operační systém**: Určuje kanál operačního systému. Například **0** = jednoletá roční směrována na kanál (neodklad aktualizací), **1** = půlroční kanál (odložení aktualizací), **2** = dlouhodobá obsluha kanálu (LTSC)

    - **Sestavení operačního systému**: Určuje sestavení operačního systému. Například **10.0.10240** (RTM) nebo **10.0.10586** (verze 1511)

- Aby bylo možné zobrazit data na řídicím panelu údržby Windows 10, je nutné nainstalovat a nakonfigurovat spojovací bod služby pro režim **online, trvalých připojení** . Když jste v offline režimu, neuvidíte na řídicím panelu aktualizace dat, dokud nezískáte Configuration Manager aktualizace pro údržbu. Další informace najdete v tématu [o spojovacím bodu služby](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- V počítači, na kterém běží Konzola Configuration Manager, musí být nainstalovaný Internet Explorer 9 nebo novější.

- Musí být nakonfigurované a synchronizované aktualizace softwaru. Vyberte klasifikaci **upgrady** a synchronizujte aktualizace softwaru před tím, než budou k dispozici všechny upgrady funkcí Windows 10 v konzole Configuration Manager. Další informace najdete v tématu [Příprava na správu aktualizací softwaru](../../sum/get-started/prepare-for-software-updates-management.md).

- Od verze Configuration Manager 1902 ověřte [nastavení klienta](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) **zadání priority vlákna pro aktualizace funkcí** a ujistěte se, že je pro vaše prostředí vhodné.

- Od verze 1906 Configuration Manager ověřte [nastavení klienta](../../core/clients/deploy/about-client-settings.md#bkmk_du) **Povolit dynamické aktualizace pro aktualizace funkcí** , aby bylo zajištěno, že bude vhodné pro vaše prostředí. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Řídicí panel údržby Windows 10

Řídicí panel údržby Windows 10 obsahuje informace o počítačích s Windows 10 ve vašem prostředí, aktivních plánech údržby, dodržování předpisů a podobně. K zobrazení údajů na řídicím panelu údržby Windows 10 je potřeba mít nainstalovaný spojovací bod služby. Řídicí panel obsahuje tyto dlaždice:

- **Dlaždice využití Windows 10**: poskytuje rozpis veřejných sestavení Windows 10. Sestavení programu Windows Insiders jsou uvedena jako **jiná** a také pro všechna sestavení, která ještě nejsou ve vaší lokalitě známá. Spojovací bod služby stáhne metadata, která ho informují o sestaveních Windows, a tato data se porovnávají s daty zjišťování.

- **Dlaždice okruhů Windows 10**: poskytuje rozpis Windows 10 Podle kanálu a stavu připravenosti. Segment LTSC zahrnuje všechny verze LTSC. První dlaždice rozdělí konkrétní verze, například Windows 10 LTSC 2015.

- **Dlaždice vytvořit plán služby**: poskytuje rychlý způsob, jak vytvořit plán údržby. Určíte název, kolekci (zobrazí se jenom prvních 10 kolekcí podle velikosti, nejmenší první), balíček pro nasazení (zobrazí se jenom prvních 10 posledních upravených balíčků) a stav připravenosti. U ostatních nastavení se použijí výchozí hodnoty. Kliknutím na **Upřesnit nastavení** spustíte Průvodce vytvořením plánu údržby, ve kterém můžete nakonfigurovat všechna nastavení plánu služby.

- **Dlaždice položek po konci životnosti**: Zobrazí procento zařízení se sestaveními Windows 10, která už jsou po konci životnosti. Configuration Manager určuje procento z metadat, která stáhne spojovací bod služby a porovná je s daty zjišťování. Sestavení, které je po skončení životnosti, již nepřijímá měsíční kumulativní aktualizace, které zahrnují aktualizace zabezpečení. Počítače v této kategorii je potřeba upgradovat na další verzi sestavení. Configuration Manager zaokrouhlí nahoru na další celé číslo. Například pokud máte 10 000 počítačů a pouze jeden v sestavení s vypršenou platností, na dlaždici se zobrazí 1%.

- **Dlaždice položek blížících se ke konci životnosti**: Zobrazuje procento počítačů, jejichž sestavení se blíží ke konci životnosti (zhruba do čtyř měsíců). Podobá se dlaždici položek **po konci životnosti** . Configuration Manager zaokrouhlí nahoru na další celé číslo.

- **Dlaždice výstrah**: Zobrazuje aktivní výstrahy.

- **Dlaždice monitorování plánu**údržby: zobrazuje plány údržby, které jste vytvořili, a graf dodržování předpisů pro každou z nich. Tato dlaždice vám poskytne rychlý přehled o aktuálním stavu nasazení plánů údržby. Pokud některý ze starších okruhů nasazení vyhovuje vašim požadavkům na dodržování předpisů, můžete vybrat novější plán údržby (okruh nasazení) a kliknout na **Nasadit nyní** , místo abyste čekali, až se automaticky spustí pravidla plánu údržby.

- **Dlaždice sestavení Windows 10**: zobrazení je pevná časová osa, která poskytuje přehled o sestaveních Windows 10, která jsou aktuálně vydaná, a poskytuje obecnou představu o tom, kdy buildy přecházejí do různých stavů. Tato dlaždice se od Configuration Manager verze 1902 odebrala, protože na [řídicím panelu životního cyklu produktu](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md)jsou k dispozici podrobnější informace. <!--3446861-->

> [!IMPORTANT]
> Informace zobrazené na řídicím panelu údržby Windows 10 (třeba životní cyklus podpory verzí Windows 10) jsou jenom orientační a nejsou určené k internímu použití ve vašem podniku. Při kontrole toho, jestli máte všechny potřebné aktualizace, byste se neměli spoléhat jenom na tyto informace. Nezapomeňte si ověřit přesnost informací, které tady získáte.

## <a name="drill-through-required-updates"></a>Podrobné informace o požadovaných aktualizacích
<!--4224414-->
*(Představené ve verzi 1906)*

Můžete procházet statistiky dodržování předpisů a zjistit, která zařízení vyžadují určitou aktualizaci funkcí Windows 10. Chcete-li zobrazit seznam zařízení, potřebujete oprávnění k zobrazení aktualizací a kolekcí, do kterých zařízení patří. Přechod k podrobnostem v seznamu zařízení:

1. Přejít do **knihovny** > softwaru**Windows 10 Údržba** > **všech aktualizací Windows 10**.
1. Vyberte jakoukoli aktualizaci, kterou vyžaduje aspoň jedno zařízení.
1. Podívejte se na kartu **Souhrn** a v části **Statistika**Najděte výsečový graf.
1. Pokud chcete přejít k podrobnostem seznamu zařízení, zaškrtněte políčko **Zobrazit požadovaný** hypertextový odkaz vedle výsečového grafu.
1. Tato akce přejde na dočasný uzel v části **zařízení** , kde vidíte zařízení vyžadující aktualizaci. Můžete také provést akce pro uzel, jako je například vytvoření nové kolekce ze seznamu.

## <a name="servicing-plan-workflow"></a>Pracovní postup plánu údržby

Plány údržby Windows 10 v Configuration Manager jsou podobně jako pravidla automatického nasazení pro aktualizace softwaru. Vytvoříte plán údržby s následujícími kritérii, která Configuration Manager vyhodnotí:

- **Klasifikace upgradů**: Hodnotí se jenom aktualizace, které mají klasifikaci **Upgrady** .

- **Stav připravenosti**: Stav připravenosti definovaný v plánu údržby se porovná se stavem připravenosti upgradu. Metadata pro upgrade se načítají, když spojovací bod služby kontroluje aktualizace.

- **Časové odložení**: Počet dnů, který v plánu údržby zadáte u položky **Jak dlouho chcete čekat s nasazením nového upgradu vydaného Microsoftem ve vašem prostředí**. Pokud aktuální datum následuje po datu vydání a nakonfigurovaném počtu dnů, Configuration Manager vyhodnotí, jestli se má do nasazení zahrnout upgrade.

  Pokud určitý upgrade splňuje kritéria, plán údržby ho přidá do balíčku nasazení, balíček distribuuje do distribučních bodů a nasadí upgrade do kolekce na základě nastavení, které jste určili v plánu údržby. Nasazení můžete sledovat na dlaždici monitorování plánu údržby na řídicím panelu údržby Windows 10. Další informace najdete v tématu [monitorování aktualizací softwaru](../../sum/deploy-use/monitor-software-updates.md).

> [!NOTE]
> **Windows 10 verze 1903 a novější** se přidala do Microsoft Update jako vlastní produkt, a ne jako součást produktu **Windows 10** , jako je třeba předchozí verze. Tato změna způsobila, že provedete několik ručních kroků, abyste zajistili, že se tyto aktualizace zobrazí u klientů. Pomohli jsme snížit počet ručních kroků, které je třeba provést pro nový produkt ve verzi Configuration Manager 1906. Další informace najdete v tématu [Konfigurace produktů pro verze Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Plán údržby Windows 10

Když nasadíte půlroční kanál Windows 10, můžete vytvořit jeden nebo několik plánů údržby a definovat tak požadované okruhy nasazení v prostředí a pak je monitorovat na řídicím panelu údržby Windows 10. Plány údržby používají jenom klasifikaci aktualizací softwaru **Upgrady** , ne kumulativní aktualizace Windows 10. U těchto aktualizací je ještě nutné nasadit pomocí pracovního postupu aktualizace softwaru. Koncový uživatel pracuje s plány údržby stejně jako s aktualizacemi softwaru, včetně nastavení, která konfigurujete v plánu údržby.  

> [!NOTE]
> Upgrady pro každé sestavení Windows 10 můžete nasadit taky pomocí pořadí úkolů, ale vyžaduje to větší manuální úsilí. Museli byste importovat aktualizované zdrojové soubory jako balíček upgradu operačního systému a potom vytvořit pořadí úkolů a nasadit ho do příslušné sady počítačů. Pořadí úkolů ale zase nabízí přizpůsobení dalších možností, třeba akcí před nasazením a po nasazení.

Základní plán údržby můžete vytvořit na panelu údržby Windows 10. Až zadáte název, kolekci (zobrazí se jenom prvních 10 kolekcí podle velikosti, nejmenšího prvního), balíček pro nasazení (zobrazí se jenom prvních 10 posledních upravených balíčků) a stav připravenosti, Configuration Manager vytvoří plán údržby s výchozími hodnotami pro ostatní nastavení. Můžete také spustit průvodce vytvořením plánu obsluhy a nakonfigurovat všechna nastavení. Následující postup slouží k vytvoření plánu údržby pomocí průvodce vytvořením plánu údržby.  

> [!NOTE]  
> Můžete spravovat chování při vysoce rizikových nasazeních. Vysoce rizikové nasazení je takové nasazení, které se instaluje automaticky a u kterého hrozí riziko nechtěných výsledků. Za vysoce rizikové nasazení se například považuje pořadí úkolů, které má účel **Vyžadováno** a které nasazuje Windows 10. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### <a name="to-create-a-windows-10-servicing-plan"></a>Postup vytvoření plánu údržby Windows 10

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.

1. V pracovním prostoru Softwarová knihovna rozbalte položku **Údržba Windows 10**a potom klikněte na **Plány údržby**.

1. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit plán údržby**. Otevře se průvodce vytvořením plánu údržby.

1. Na stránce **Obecné** nakonfigurujte následující nastavení:

    - **Název**: Zadejte název plánu údržby. Název musí být jedinečný, může pojmenovat cíl pravidla a identifikovat ho od ostatních v Configuration Manager lokalitě.

    - **Popis**: Zadejte popis plánu údržby. Popis by měl poskytovat přehled o plánu údržby a všech dalších relevantních informacích, které pomáhají identifikovat a odlišit plán mezi ostatními v Configuration Manager lokalitě. Pole popisu je volitelné, je omezeno na 256 znaků a výchozí hodnota je prázdná.

1. Na stránce plán údržby zadejte **cílovou kolekci**. Členové této kolekce obdrží upgrady Windows 10 definované v tomto plánu údržby.

    - Když nasadíte vysoce rizikové nasazení, například plán údržby, v okně **Vybrat kolekci** se zobrazí pouze vlastní kolekce, které splňují nastavení ověřování nasazení, které jsou konfigurovány ve vlastnostech lokality.

    - Vysoce riziková nasazení se vždy omezují na vlastní kolekce, kolekce, které vytvoříte, a na vestavěnou kolekci **Neznámé počítače**. Když vytvoříte vysoce rizikové nasazení, nemůžete vybrat vestavěnou kolekci, například **všechny systémy**. Zrušte zaškrtnuté políčka **Skrýt kolekce s počtem členů větším, než je konfigurace minimální velikosti lokality** , aby se zobrazily všechny vlastní kolekce, které obsahují méně klientů, než je nakonfigurovaná maximální velikost. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - Nastavení ověřování nasazení jsou založena na aktuálním členství kolekce. Po nasazení plánu údržby se členství v kolekci znovu nevyhodnotí pro nastavení nasazení s vysokým rizikem.

      - Řekněme například, že jste nastavili **výchozí velikost** na 100 a **maximální velikost** na 1000. Když vytvoříte nasazení s vysokým rizikem, zobrazí se v okně **Vybrat kolekci** pouze kolekce, které obsahují méně než 100 klientů. Pokud zrušíte zaškrtnutí políčka **Skrýt kolekce s počtem členů větším, než je nastavení konfigurace minimální velikosti webu** , zobrazí se v okně kolekce, které obsahují méně než 1000 klientů.  
      Když vyberete kolekci, která obsahuje roli lokality, platí následující kritéria:
        - Pokud kolekce obsahuje server systému lokality a v nastavení ověřování nasazení, které nakonfigurujete pro blokování kolekcí se servery systému lokality, dojde k chybě a nemůžete pokračovat.
        - Pokud kolekce obsahuje server systému lokality a v nastavení ověřování nasazení nastavíte varování před kolekcemi se servery systému lokality, pak když kolekce překračuje výchozí velikost nebo když kolekce obsahuje server, Průvodce nasazením softwaru zobrazí zobrazí varování před vysokým rizikem. Budete muset souhlasit s vytvořením vysoce rizikového nasazení a vytvoří se stavová zpráva auditu.

1. Na stránce Okruh nasazení nakonfigurujte následující nastavení:

   - **Zadejte stav připravenosti Windows, pro který se má tento plán údržby použít**: vyberte jednu z následujících možností:

      - **Půlroční kanál (cílený)**: v tomto modelu údržby jsou aktualizace funkcí k dispozici, jakmile je společnost Microsoft vydává.

      - **Půlroční kanál**: Tento kanál pro údržbu se obvykle používá pro rozsáhlá nasazení. Klienti Windows 10 v pololetním kanálu obdrží stejné sestavení Windows 10 jako zařízení v cílovém kanálu, a to hned později.

        Další informace o kanálech pro údržbu a o tom, jaké možnosti jsou pro vás nejvhodnější, najdete v tématu [kanály pro údržbu](/windows/deployment/update/waas-overview#servicing-channels).

   - Počet **dní od publikování nového upgradu od Microsoftu, které chcete čekat před nasazením ve vašem prostředí**: Pokud aktuální datum následuje po datu vydání a počet dní, který nakonfigurujete pro toto nastavení, Configuration Manager vyhodnotí, jestli se má do nasazení zahrnout upgrade.

1. Na stránce upgrady nakonfigurujte kritéria hledání tak, aby se vyfiltroval upgrady, které se přidají do plánu služeb. Do přidruženého nasazení se přidají jenom upgrady, které splňují zadaná kritéria. K dispozici jsou následující filtry vlastností: <!--3098809, 3113836, 3204570 -->

   - **Architektura** (počínaje verzí 1810)
   - **Jazyk**
   - **Produktová kategorie** (počínaje verzí 1810)
   - **Požadováno**
      > [!IMPORTANT]
      > Doporučujeme, abyste jako součást kritérií vyhledávání nastavili **požadované** pole s hodnotou **>= 1**. Pomocí těchto kritérií zajistíte, aby se do plánu služeb přidaly jenom použitelné aktualizace.
   - **Nahrazeno** (počínaje verzí 1810)
   - **Nadpis**

    Kliknutím na **Náhled** zobrazíte upgrady, které splňují zadaná kritéria.

1. Na stránce Plán nasazení konfigurujte následující nastavení:

   - **Vyhodnocení plánu**: Určete, jestli Configuration Manager vyhodnotí dostupný čas a konečné termíny instalace pomocí standardu UTC nebo místního času počítače, na kterém je spuštěná konzola Configuration Manager.

       > [!NOTE]
       > Když vyberete místní čas a potom jako **Čas dostupnosti softwaru** nebo **konečný termín instalace**vyberete **co nejdříve** , k vyhodnocení, že jsou aktualizace dostupné nebo kdy se instalují na klienta, se použije aktuální čas v počítači, na kterém je spuštěná konzola Configuration Manager. Pokud je klient v jiném časovém pásmu, tyto akce se provedou, když čas klienta dosáhne doby vyhodnocení.

   - **Čas dostupnosti softwaru**: Pomocí jednoho z následujících nastavení určete, kdy mají být aktualizace softwaru dostupné klientům:

        - **Co nejdříve**: Pomocí tohoto nastavení můžete aktualizace softwaru, které jsou zahrnuté v nasazení, zpřístupnit pro klienty, jakmile to půjde. Když vytvoříte nasazení s vybraným tímto nastavením, Configuration Manager aktualizuje zásady klienta. Poté, v dalším intervalu dotazování zásad klienta, klienti zaregistrují nasazení a mohou získat aktualizace, které jsou k dispozici pro instalaci.

        - **Určený čas**: Pomocí tohoto nastavení zpřístupníte aktualizace softwaru, které jsou dostupné v nasazení, pro klienty v určité datum a čas. Když vytvoříte nasazení s povoleným tímto nastavením, Configuration Manager aktualizuje zásady klienta. Poté, v dalším intervalu dotazování zásad klienta, klienti zaregistrují nasazení. Aktualizace softwaru v nasazení však nejsou k dispozici pro instalaci až po nakonfigurované datum a čas.

   - **Konečný termín instalace**: výběrem jednoho z následujících nastavení určete konečný termín instalace pro aktualizace softwaru v nasazení:

        - **Co nejdříve:** Pomocí tohoto nastavení můžete automaticky nainstalovat aktualizace softwaru v nasazení, jakmile to bude možné.

        - **Určený čas:** Pomocí tohoto nastavení můžete aktualizace softwaru v nasazení automaticky nainstalovat v určité datum a čas. Configuration Manager Určuje konečný termín pro instalaci aktualizací softwaru přidáním nakonfigurovaného **zadaného časového** intervalu k **času dostupnosti softwaru**.

           > [!NOTE]
           > Skutečný konečný termín instalace je zobrazený konečný termín doplněný o náhodný čas v délce až 2 hodin. To snižuje možný dopad všech klientských počítačů v cílové kolekci, které instalují aktualizace obsažené v nasazení ve stejnou dobu.
           >
           > U položky klientského nastavení **Počítačový agent** můžete nastavit možnost **Zakázat náhodné přeskupování času termínu**. Tím zakážete náhodné přeskupování časů instalace požadovaných aktualizací. Další informace najdete v části [Počítačový agent](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Odložit vynucení tohoto nasazení podle uživatelských preferencí, až do období odkladu definovaného v klientovi**: tuto možnost vyberte, [ **Pokud chcete po uplynutí konečného termínu nasazení (hodiny) akceptovat dobu odkladu k vynucení** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours).

1. Na stránce Činnost koncového uživatele konfigurujte následující nastavení:  

    - **Oznámení uživateli**: Zadejte, jestli se mají v Centru softwaru zobrazovat oznámení o aktualizacích v nastavenou dobu **Čas dostupnosti softwaru** a jestli se mají zobrazovat oznámení uživatelům na klientských počítačích.

    - **Chování v konečném termínu**: Určete chování, které se má použít při dosažení termínu nasazení aktualizace. Určete, jestli se mají nainstalovat aktualizace v nasazení. Také určete, jestli se má po instalaci aktualizací restartovat systém bez ohledu na nakonfigurované časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.  

    - **Chování zařízení při restartu**: Určete, jestli se má po instalaci aktualizací, pokud je k dokončení instalace potřeba restartovat počítače, potlačit restartování systému na serverech a pracovních stanicích.

    - **Zpracování filtru zápisu pro zařízení s platformou Windows Embedded**: Když nasazujete aktualizace do zařízení s platformou Windows Embedded, která mají povolený filtr zápisu, můžete určit, že se má aktualizace nainstalovat do dočasného překrytí a že chcete změny provést později nebo je provést v termínu instalace, případně v časovém období údržby. Pokud provedete změny v termínu instalace nebo během otevření okna údržby, je nutné provést restart (změny se na zařízení zachovají).
        - Když nasazujete aktualizaci nasadit do zařízení se systémem Windows Embedded, ujistěte se, že je zařízení členem kolekce, která má nakonfigurované období údržby.

    - **Chování při opakovaném vyhodnocení nasazení aktualizací softwaru po restartu**: Chcete-li vynutit další cyklus vyhodnocení nasazení aktualizace po restartování počítače, vyberte možnost **Pokud nějaká aktualizace v tomto nasazení vyžaduje restart systému, po restartu spusťte zkušební cyklus nasazení aktualizací**.

1. Na stránce balíček pro nasazení vyberte existující balíček pro nasazení, žádný balíček pro nasazení, nebo pro vytvoření nového balíčku pro nasazení nakonfigurujte následující nastavení:

    1. **Název**: Určuje název balíčku pro nasazení. Tento název musí být jedinečný a popisuje obsah balíčku. Je omezena na 50 znaků.

    1. **Popis**: Zadejte popis, který poskytuje informace o balíčku pro nasazení. Popis je omezený na 127 znaků.

    1. **Zdroj balíčku:** Určuje umístění zdrojových souborů aktualizace softwaru. Zadejte síťovou cestu pro zdrojové umístění, třeba ** \\cestu \Server\\název_sdílené_položky\\**, nebo klikněte na tlačítko **Procházet** a vyhledejte umístění v síti. Než přejdete na další stránku, vytvořte sdílenou složku pro zdrojové soubory balíčku pro nasazení.
        - Umístění zdroje balíčku nasazení, které určíte, nemůže být použito jiným balíčkem nasazení softwaru.
        - Jak uživatel počítače poskytovatele SMS, tak uživatel, který má spuštěného průvodce stahováním aktualizací softwaru, musí pro umístění stahování mít oprávnění NTFS k **zápisu** . Měli byste pečlivě omezit přístup k umístění pro stahování, abyste snížili riziko manipulace se zdrojovými soubory aktualizace softwaru.
        - Umístění zdroje balíčku můžete změnit ve vlastnostech balíčku nasazení po Configuration Manager vytvoří balíček pro nasazení. Ale pokud to uděláte, musíte nejdříve zkopírovat obsah původního zdroje balíčku do nového umístění zdroje balíčku.

    1. **Priorita odeslání**: Zadejte prioritu odeslání balíčku pro nasazení. Configuration Manager používá prioritu odeslání balíčku pro nasazení při odeslání balíčku do distribučních bodů. Balíčky pro nasazení se odesílají v pořadí podle priority: vysoká, střední nebo nízká. Balíčky se stejnou prioritou jsou zasílány v pořadí podle data vytvoření. Pokud neexistují žádné nevyřízené položky, balíček okamžitě zpracuje bez ohledu na jeho prioritu.

    1. **Povolit binární rozdílovou replikaci**: tuto možnost povolte, pokud chcete použít binární rozdílovou replikaci.

1. Na stránce distribuční body určete distribuční body nebo skupiny distribučních bodů, které hostují soubory aktualizace. Další informace o distribučních bodech najdete v tématu [Konfigurace distribučního bodu](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > Tato stránka je dostupná pouze tehdy, když vytvoříte nový balíček pro nasazení aktualizací softwaru.  

1. Na stránce Umístění pro stahování určete, jestli se mají soubory aktualizace stáhnout z internetu, nebo z místní sítě. Nakonfigurujte tahle nastavení:

    - **Stáhnout softwarové aktualizace z internetu**: Toto nastavení vyberte, pokud chcete aktualizace stáhnout z určitého umístění na internetu. Toto nastavení je standardně zapnuté.

    - **Stáhnout softwarové aktualizace z místa v mé síti**: Toto nastavení vyberte, pokud chcete aktualizace stáhnout z místního adresáře nebo sdílené složky. Toto nastavení je užitečné, když počítač, na kterém spouštíte Průvodce, nemá přístup k Internetu. Každý počítač s přístupem k internetu může aktualizace předběžně stáhnout a uchovávat je v umístění v místní síti, které je dostupné z počítače, ve kterém běží průvodce.

1. Na stránce Výběr jazyka vyberte jazyky, pro které se vybrané aktualizace stahují. Aktualizace se stáhnou pouze v případě, že jsou ve vybraných jazycích k dispozici. Aktualizace, které nejsou specifické pro konkrétní jazyk, budou staženy vždy. Ve výchozím nastavení Průvodce vybírá jazyky, které jste nakonfigurovali ve vlastnostech bodu aktualizace softwaru. Před přechodem na další stránku je třeba vybrat alespoň jeden jazyk. Když vyberete jenom jazyky, které aktualizace nepodporuje, stažení se pro tuto aktualizaci nepovede.

1. Na stránce Shrnutí zkontrolujte nastavení a kliknutím na **Další** vytvořte plán údržby.  

Po dokončení průvodce se plán údržby spustí. Přidá aktualizace, které odpovídají zadaným kritériím, do skupiny aktualizací softwaru, stáhne aktualizace do knihovny obsahu na serveru lokality, distribuuje je do nakonfigurovaných distribučních bodů a poté nasadí skupinu aktualizace softwaru na klienty v cílové kolekci.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Úprava plánu údržby

Po vytvoření základního plánu údržby na řídicím panelu údržby Windows 10 nebo pokud potřebujete změnit nastavení existujícího plánu údržby, můžete přejít na vlastnosti plánu údržby.

> [!NOTE]
> Nastavení můžete nakonfigurovat ve vlastnostech pro plán údržby, které nejsou k dispozici v průvodci při vytváření plánu údržby. Průvodce používá výchozí nastavení pro následující nastavení: Stažení nastavení, nastavení nasazení a výstrahy.  

Pomocí následujícího postupu můžete změnit vlastnosti plánu údržby. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Postup úpravy vlastností plánu údržby

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.

1. V pracovním prostoru Softwarová knihovna rozbalte položku **Údržba Windows 10**, klikněte na **plány údržby**a potom vyberte plán údržby, který chcete upravit.

1. Na kartě **Domů** klikněte na **Vlastnosti** . Otevřou se vlastnosti vybraného plánu údržby.

    Ve vlastnostech plánu údržby, které nebyly nakonfigurovány v průvodci, jsou k dispozici následující nastavení:

    **Nastavení nasazení**: na kartě nastavení nasazení nakonfigurujte následující nastavení:

    - **Použít funkci Wake-on-LAN k probuzení klientů pro požadovaná nasazení:** Určuje, jestli se má v konečném termínu povolit funkce Wake On LAN k odesílání paketů buzení ze spánku na počítače, které v nasazení vyžadují jednu nebo víc aktualizací softwaru. Všechny počítače, které jsou v režimu spánku v konečném termínu instalace, jsou probuzeny, takže se může zahájit instalace aktualizace softwaru. Klienti, kteří jsou v režimu spánku, který nevyžaduje žádné aktualizace softwaru v nasazení, se nespustí. Ve výchozím nastavení není toto nastavení povolené.

        > [!WARNING]
        > Před použitím této možnosti musí mít počítače a sítě konfiguraci Wake On LAN.

    - **Úroveň podrobností:** Určuje úroveň podrobností pro stavové zprávy, které jsou hlášené klientskými počítači.

    **Nastavení stahování**: na kartě Nastavení stahování nakonfigurujte následující nastavení:

    - Určete, zda klient stáhne a nainstaluje aktualizace softwaru, když je klient připojen k pomalé síti nebo používá záložní umístění obsahu.

    - Určete, zda má klient stahovat a instalovat aktualizace softwaru ze záložního distribučního bodu, když obsah pro aktualizace softwaru není k dispozici v upřednostňovaném distribučním bodě.

    - **Povolit klientům sdílet obsah s ostatními klienty ve stejné podsíti:** Určete, jestli se má povolit použití funkce BranchCache pro stahování obsahu. Další informace o funkci BranchCache najdete v tématu [základní koncepty správy obsahu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Určete, jestli mají klienti stahovat aktualizace softwaru z Microsoft Update, pokud nejsou aktualizace softwaru dostupné v distribučních bodech.
        > [!IMPORTANT]
        > Nepoužívejte toto nastavení pro servisní aktualizace Windows 10. Configuration Manager (alespoň přes verzi 1610) se nepovede stáhnout aktualizace pro údržbu Windows 10 z Microsoft Update.

    - Určete, jestli chcete klientům povolit stahování po konečném termínu instalace, pokud používají měřená připojení k internetu. Poskytovatelé připojení k internetu někdy účtují podle množství dat, která odesíláte a přijímáte, když máte měřené připojení k internetu.

    **Výstrahy**: na kartě výstrahy nakonfigurujte, jak Configuration Manager a System Center Operations Manager generovat výstrahy pro toto nasazení.
    - Nedávné aktualizace softwaru můžete zkontrolovat z uzlu **Aktualizace softwaru** v pracovním prostoru **Softwarová knihovna** .

## <a name="next-steps"></a>Další kroky

Další informace najdete v tématu [základy Configuration Manager jako služba a Windows jako služba](../../core/understand/configuration-manager-and-windows-as-service.md).
