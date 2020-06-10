---
title: Konfigurace klasifikací a produktů
titleSuffix: Configuration Manager
description: Pomocí těchto kroků můžete nakonfigurovat klasifikace aktualizací softwaru a produkty k synchronizaci v konzole Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 4f13ff305ba5fc2b5c5080bafb6fed2412ff8366
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614086"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Konfigurace klasifikací a produktů k synchronizaci  

*Platí pro: Configuration Manager (Current Branch)*

Metadata aktualizací softwaru se načítají během procesu synchronizace v Configuration Manager v závislosti na nastavení, která zadáte ve vlastnostech komponenty bodu aktualizace softwaru. Po první synchronizaci aktualizací softwaru nebo při vydání nových produktů a klasifikací musíte přejít na vlastnosti a vybrat nové položky. Pomocí následujícího postupu proveďte konfiguraci klasifikací a produktů k synchronizaci.  

> [!NOTE]  
> Postup z této části použijte pouze v lokalitě nejvyšší úrovně.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Konfigurace klasifikací a produktů k synchronizaci  

1. V konzole **Configuration Manager** přejděte na **Správa**  >  **Konfigurace lokality**  >  **lokality**.

2. Vyberte lokalitu centrální správy nebo samostatnou primární lokalitu.  

3. Na kartě **Domů** v části **Nastavení** klikněte na **Konfigurovat součásti pracoviště**a potom na možnost **Bod aktualizace softwaru**.

4. Na kartě **Klasifikace** určete klasifikace aktualizace softwaru, pro které chcete aktualizace softwaru synchronizovat.  

    Každá aktualizace softwaru je definována pomocí klasifikace aktualizace, která pomáhá organizovat různé typy aktualizací. Při procesu synchronizace se synchronizují metadata aktualizace softwaru pro zadané klasifikace. Configuration Manager poskytuje možnost synchronizovat aktualizace softwaru s následujícími klasifikacemi aktualizací:  

     - **Kritické aktualizace**: Určuje široce vydanou opravu pro určitý problém, která řeší kritickou chybu nesouvisející se zabezpečením.  
     - **Aktualizace definic**: Určuje široce vydanou a častou aktualizaci softwaru, která obsahuje dodatky k databázi definicí produktu.  
     - **Balíčky funkcí**: označuje nové funkce produktu, které jsou nejdříve distribuované mimo vydání produktu, a které jsou obvykle zahrnuté v příštím plném vydání produktu.  
     - **Aktualizace zabezpečení**: Určuje široce vydanou opravu ohrožení zabezpečení souvisejícího s konkrétním produktem.  
     - Aktualizace **Service Pack**: Určuje testovaný a kumulativní sadu všech oprav hotfix, aktualizací zabezpečení, důležitých aktualizací a aktualizací, které se vztahují na produkt. Kromě toho mohou aktualizace Service Pack obsahovat další opravy pro problémy, které se nacházejí interně od vydání produktu.  
     - **Nástroje**: Určuje nástroj nebo funkci, která pomáhá dokončit jednu nebo více úloh.  
     - **Kumulativní aktualizace**: Určuje testovaný, kumulativní sadu oprav hotfix, aktualizace zabezpečení, důležité aktualizace a aktualizace, které jsou zabaleny společně pro snadné nasazení. Kumulativní aktualizace obecně řeší určitou oblast, například zabezpečení nebo součást produktu.  
     - **Aktualizace**: Určuje široce vydanou opravu konkrétního problému. Aktualizace řeší nekritickou chybu, která nesouvisí se zabezpečením.  
     - **Upgrade**: Určuje upgrade pro funkce a funkce Windows 10. Abyste získali klasifikaci **upgradu** , musí být v lokalitách a bodech aktualizace softwaru spuštěn minimálně WSUS 6,2 s [opravou hotfix 3095113](https://support.microsoft.com/kb/3095113) . Další informace o instalaci této aktualizace a dalších aktualizacích pro **upgrady**najdete v tématu [předpoklady pro aktualizace softwaru](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).
    
    > [!NOTE]
    > Zaškrtnutím políčka **zahrnout ovladače Microsoft Surface a aktualizace firmwaru** můžete synchronizovat ovladače Microsoft Surface.<!--1098490--> Aby bylo možné úspěšně synchronizovat ovladače Surface, musí všechny body aktualizace softwaru používat systém Windows Server 2016 nebo novější. Pokud povolíte bod aktualizace softwaru na počítači s Windows Serverem 2012 po povolení ovladačů Surface, výsledky kontroly pro aktualizace ovladačů nejsou přesné. Výsledkem jsou nesprávná data o dodržování předpisů zobrazená v konzole Configuration Manager a v sestavách Configuration Manager. Další informace najdete v tématu [Správa ovladačů Surface pomocí Configuration Manager](../deploy-use/surface-drivers.md).

5. Na kartě **Produkty** vyberte produkty, pro které chcete aktualizace softwaru synchronizovat, a potom klikněte na **Zavřít**.  

    - Configuration Manager ukládá seznam produktů a rodin produktů, ze kterých si můžete vybrat při první instalaci bodu aktualizace softwaru. Produkty a řady produktů vydané po vydání Configuration Manager nemusí být k dispozici pro výběr, dokud nedokončíte synchronizaci aktualizací softwaru, čímž aktualizujete seznam dostupných produktů a řad produktů, ze kterého můžete vybírat.  

    - Metadata jednotlivých aktualizací softwaru definují produkty, na které lze aktualizaci použít. Produkt je určité vydání operačního systému nebo aplikace, třeba Windows Server 2012. Rodina produktů je základní operační systém nebo aplikace, z nichž je konkrétní produkt odvozen. Příkladem produktové řady je systém Windows a systém Windows Server 2012 je jejím členem. Je možné určit řadu produktů nebo jednotlivé produkty dané řady. Čím více produktů vyberete, tím déle bude synchronizace aktualizací softwaru trvat.  

    - Pokud se aktualizace softwaru vztahují k více produktům a pro synchronizaci byl vybrán alespoň jeden z nich, v konzole Configuration Manager se zobrazí všechny produkty, i když některé z nich nebyly vybrány. Například pokud je Windows Server 2012 jediným operačním systémem, který jste vybrali, a pokud se aktualizace softwaru vztahuje na systémy Windows 8 a Windows Server 2012, v konzole Configuration Manager se zobrazí oba produkty.  

    > [!NOTE]  
    > **Windows 10 verze 1903 a novější** se přidala do Microsoft Update jako vlastní produkt, a ne jako součást produktu **Windows 10** , jako je třeba předchozí verze. Tato změna způsobila, že provedete několik ručních kroků, abyste zajistili, že se tyto aktualizace zobrazí u klientů. Pomohli jsme snížit počet ručních kroků, které je třeba provést pro nový produkt ve verzi Configuration Manager 1906. <!--4682946-->
    >
    > Když aktualizujete na Configuration Manager verze 1906 a produkt **Windows 10** je vybraný pro synchronizaci, automaticky se provedou následující akce:
    > - Pro synchronizaci se přidá **Windows 10 verze 1903 a novější** .
    > - [Pravidla automatického nasazení](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) obsahující produkt **Windows 10** se budou aktualizovat tak, aby zahrnovala **Windows 10, verze 1903 a novější**.
    > - [Plány údržby](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) se aktualizují tak, aby zahrnovaly **Windows 10, verze 1903 a novější** produkt.


## <a name="configuring-products-for-versions-of-windows-10"></a>Konfigurace produktů pro verze Windows 10

### <a name="windows-10-version-1909"></a>Windows 10 verze 1909

Windows 10 verze 1909 sdílí společný základní operační systém se systémem Windows 10 verze 1903. Obě tyto verze jsou obsluhované se stejnými kumulativními aktualizacemi. Další informace o Windows 10 verze 1909 najdete v příspěvku na blogu [Možnosti pro doručení ve Windows 10, verze 1909](https://aka.ms/1909mechanics) .

Aby se zajistilo, že klienti s Windows 10 verze 1909 a Windows 10, verze 1903, nainstalují aktualizace z Configuration Manager:

- Schválí aktualizace pro verze 1909 a 1903 systému Windows 10.
  - Aktualizace mají různé názvy a pravidla použitelnosti pro každou verzi operačního systému.
  - Schválení každé aktualizace na verzi a architektury operačního systému udržuje běžný proces schvalování správců.
- Instalační soubory kumulativní aktualizace jsou stejné pro verze 1909 a 1903 systému Windows 10.
  - Configuration Manager stáhne pouze ty zdrojové soubory aktualizace.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Aktualizace funkcí pro Windows 10 verze 1909

Když schválíte aktualizace funkcí pro Windows 10 verze 1909, zobrazí se několik různých možností:

- Klientům se systémem Windows 10, verze 1903 jsou nabízeny [balíčky pro povolení](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)vydané 12. listopadu 2019.
  - Balíček pro povolení je malý, rychle nainstalovaný soubor, který aktivuje funkce Windows 10, verze 1909 a restartuje zařízení.
  - Požadavky balíčku pro povolení zahrnují:
    - Minimální kumulativní aktualizace [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389)vydaná 8. října 2019.
    - Minimální aktualizace servisního zásobníku [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390)vydané 24. září 2019.
  - Tato aktualizace, stejně jako jakákoli jiná aktualizace funkcí, není k dispozici pro import z `https:\\catalog.update.microsoft.com` .
  - Aktualizace se automaticky synchronizuje se službou WSUS, pokud máte **Windows 10, verze 1903 a novější** klasifikace produktů a **upgradů** vybrané k synchronizaci.
  - V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Údržba Windows 10**a vyberte uzel **všechny aktualizace Windows 10** . Vyhledejte výraz "Enable" nebo "4517245".

    > [!TIP]
    > Vzhledem k tomu, že se jedná o aktualizace funkcí, nejsou v uzlu **všechny aktualizace softwaru** .

- Klienti s Windows 10, verze 1809 a starší se upgradují s jednou přímou aktualizací funkcí.
  - Jedná se stejně jako všechny ostatní předchozí instalace pro aktualizace funkcí, které jste provedli pro Windows 10.

> [!NOTE]
> Balíček povolení i tradiční aktualizace funkcí pro Windows 10 verze 1909 se v hlášení zobrazí jako "nainstalované", a to bez ohledu na to, jaká cesta se použila k její instalaci.

### <a name="windows-10-version-1903-and-later"></a>Windows 10 verze 1903 a novější

**Windows 10 verze 1903 a novější** se přidala do Microsoft Update jako vlastní produkt, a ne jako součást produktu **Windows 10** , jako je třeba předchozí verze. Tato změna způsobila, že provedete několik ručních kroků, abyste zajistili, že se tyto aktualizace zobrazí u klientů. Pomohli jsme snížit počet ručních kroků, které je třeba provést pro nový produkt ve verzi Configuration Manager 1906. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10 verze 1903 a novější s Configuration Manager verze 1906
Když aktualizujete na Configuration Manager verze 1906 a produkt **Windows 10** je vybraný pro synchronizaci, automaticky se provedou následující akce:
- Pro synchronizaci se přidá **Windows 10 verze 1903 a novější** .
- [Pravidla automatického nasazení](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) obsahující produkt **Windows 10** se budou aktualizovat tak, aby zahrnovala **Windows 10, verze 1903 a novější**.
- [Plány údržby](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) se aktualizují tak, aby zahrnovaly **Windows 10, verze 1903 a novější** produkt.

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10 verze 1903 a novější s Configuration Manager verze 1902
Pokud používáte Configuration Manager 1902 s Windows 10, klienty verze 1903, budete potřebovat:
- Vyberte **Windows 10, verze 1903 a novější** produkt pro synchronizaci.
- Aktualizujte všechna [pravidla automatického nasazení](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) pro klienty se systémem Windows 10 verze 1903.
- Aktualizujte [plány údržby](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) pro klienty se systémem Windows 10 verze 1903.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a>Program Windows Insider
<!--3556023-->
Od září 2019 můžete obsluhovat a aktualizovat zařízení s Windows Insider Preview Builds pomocí Configuration Manager. Tato změna znamená, že můžete spravovat tato zařízení beze změny normálních procesů nebo povolení web Windows Update pro firmy. Aktualizace funkcí a kumulativní aktualizace pro buildy Windows Insider Preview si můžete stáhnout do Configuration Manager stejně jako všechny ostatní aktualizace nebo upgrady Windows 10. Další informace najdete v příspěvku na blogu [služby WSUS v tématu publikování předběžných verzí Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) .

Další informace o podpoře Windows Insider v Configuration Manager najdete v tématu [Podpora pro Windows 10](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Požadavky

- Configuration Manager verze 1906 nebo vyšší, nakonfigurované pro [správu aktualizací softwaru](../plan-design/plan-for-software-updates.md).
- Zařízení s Windows 10 s [buildem Windows Insider Preview](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started)
- Kolekce obsahující zařízení Windows Insider

### <a name="enable-windows-insider-upgrades-and-updates"></a>Povolit upgrady a aktualizace Windows Insider

Je potřeba povolit produkty a klasifikace pro upgrady a aktualizace Windows Insider. Aktualizace funkcí, kumulativní aktualizace a další aktualizace programu Windows Insider jsou uvedené v kategorii produkt **Předběžná verze Windows Insider** .

1. V konzole **Configuration Manager** přejděte na **Správa**  >  **Konfigurace lokality**  >  **lokality**.
2. Vyberte lokalitu centrální správy nebo samostatnou primární lokalitu.  
3. Na kartě **Domů** v části **Nastavení** klikněte na **Konfigurovat součásti pracoviště**a potom na možnost **Bod aktualizace softwaru**.
4. Na kartě **produkty** zajistěte, aby byly pro synchronizaci vybrány následující produkty:
    - Předběžná verze Windows Insider
    - Windows 10 verze 1903 a novější
5. Na kartě **klasifikace** ověřte, zda jsou pro synchronizaci vybrány následující klasifikace:
    - Programů
    - Aktualizace zabezpečení
    - Aktualizace (volitelné)
6. Kliknutím na tlačítko **OK** zavřete **Vlastnosti komponenty bodu aktualizace softwaru**.

### <a name="upgrading-windows-insider-devices"></a>Upgrade zařízení se systémem Windows Insider

Po synchronizaci upgradů pro Windows Insider je můžete zobrazit z **knihovny softwaru**  >  **Windows 10 – Údržba**  >  **všech aktualizací Windows 10**.

![Aktualizace funkcí Windows Insider pro údržbu Windows 10](media/3556023-windows-insiders-pre-release-feature-update.png)

Nasaďte aktualizace funkcí pro Windows Insider do cílové kolekce stejně jako všechny ostatní upgrady. Při nasazení těchto aktualizací funkcí ale budete chtít mít na paměti následující věci:

- Tyto upgrady se budou uplatňovat pro všechny klienty Windows 10 verze 1903 nebo starší s vyhovující architekturou, edicí a jazykem.
- Existují licenční podmínky, vaše nasazení musí přijmout podmínky, aby je bylo možné nainstalovat.
- Zvažte použití [priority vlákna v nastavení klienta](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority).
- Dynamická aktualizace automaticky nainstaluje důležité aktualizace, včetně nejnovější kumulativní aktualizace, přímo z Microsoft Update. Toto chování začalo s aktualizacemi funkcí pro Windows 10 verze 1903. 
  - [Dynamickou aktualizaci můžete explicitně zakázat v nastavení klienta](../../core/clients/deploy/about-client-settings.md#bkmk_du) nebo pomocí [souboru setupconfig. ini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Další informace najdete v blogovém příspěvku s [dynamickými aktualizacemi Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) .

Další informace o tom, jak nasadit upgrady, najdete v tématu [Správa systému Windows jako služby](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Udržování aktuálního stavu zařízení Insider

Kumulativní aktualizace pro Windows Insider budou dostupné pro službu WSUS a rozšíření pro Configuration Manager. Tyto kumulativní aktualizace budou vydány s frekvencí podobnou kumulativními aktualizacemi Windows 10 verze 1903. Kumulativní aktualizace programu Windows Insider jsou v kategorii produktů **Windows Insider pre-Release** a klasifikované jako **aktualizace zabezpečení** nebo **aktualizace**. Kumulativní aktualizace pro Windows Insider můžete nasadit pomocí běžného procesu aktualizace softwaru, jako je například použití [pravidel automatického nasazení](../deploy-use/automatically-deploy-software-updates.md) nebo [dvoufázové nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Rozšířené aktualizace zabezpečení a Configuration Manager

Program [Extended Security Updates (EVJ)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) je poslední možností pro zákazníky, kteří potřebují spouštět některé starší verze produktů Microsoftu po skončení podpory. Zahrnuje kritické a/nebo důležité aktualizace zabezpečení (definované [centrem MSRC (Microsoft Security Response Center)](https://www.microsoft.com/msrc)po dobu delší než tři roky po ukončení rozšířené podpory produktu.

Produkty, které přesahují životní cyklus podpory, se nepodporují pro použití s Configuration Manager. To zahrnuje všechny produkty, které jsou pokryté v programu EVJ. Například Windows 7. Aktualizace zabezpečení vydané v rámci programu EVJ budou publikovány ve službě Windows Server Update Services (WSUS). Tyto aktualizace se zobrazí v konzole Configuration Manager. I když produkty, které jsou pokryté programem EVJ, už nejsou podporované pro použití s Configuration Manager, [nejnovější vydanou verzi Configuration Manager aktuální větev](../../core/servers/manage/updates.md#version-details) můžete použít k nasazení a instalaci aktualizací zabezpečení systému Windows vydaných v rámci programu. Nejnovější vydanou verzi je taky možné použít k nasazení Windows 10 na zařízení s Windows 7.

Funkce správy klientů, které nesouvisejí se správou aktualizací softwaru systému Windows nebo nasazení operačního systému, již nebudou testovány v operačních systémech, které jsou zahrnuty v rámci programu EVJ, a nezaručujeme, že budou nadále fungovat. Pro příjem podpory správy klientů doporučujeme, abyste v nejbližší době provedli upgrade nebo migraci na aktuální verzi operačních systémů.


## <a name="next-steps"></a>Další kroky

Spustí synchronizaci aktualizací softwaru, aby se načetly aktualizace softwaru na základě nových kritérií. Další informace najdete v tématu [synchronizace aktualizací softwaru](synchronize-software-updates.md).
