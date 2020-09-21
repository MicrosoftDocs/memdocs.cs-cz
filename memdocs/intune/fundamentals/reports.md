---
title: Microsoft Intune reports
titleSuffix: Microsoft Intune
description: Intune poskytuje konkrétní typy sestav s podrobnými zobrazeními, která obsahují konzistentní a včasná data.
keywords: ''
author: erikre
ms.author: erikre
manager: dougeby
ms.date: 09/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d6c159f775ffbc169f2f91b9cf447f24eaf0df4
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813767"
---
# <a name="intune-reports"></a>Sestavy Intune
Sestavy Microsoft Intune vám umožňují efektivněji a aktivně monitorovat stav a činnost koncových bodů napříč vaší organizací a také poskytuje jiná data pro vytváření sestav v rámci Intune. Budete například moci zobrazit sestavy o dodržování předpisů zařízením, stavu zařízení a trendech zařízení. Kromě toho můžete vytvořit vlastní sestavy, abyste získali konkrétnější data. 

> [!NOTE]
> Změny vytváření sestav Intune se postupně zavádějí do časového období, které vám pomůžou připravit a přizpůsobovat se k nové struktuře.

Typy sestav jsou uspořádány do následujících oblastí fokusu:
- **Provozní** – poskytuje včasné a cílené údaje, které vám pomůžou se zaměřit a provést akci. Tito správci, odborníci na danou problematiku a helpdesk budou tyto sestavy Hledat nejužitečnější.
- **Organizace** – poskytuje širší souhrn celkového zobrazení, například stav správy zařízení. Manažeři a správci tyto sestavy uvidí nejužitečnější.
- **Historická** – poskytuje vzory a trendy v časovém intervalu. Manažeři a správci tyto sestavy uvidí nejužitečnější.
- **Specialista** – umožňuje používat nezpracovaná data k vytváření vlastních sestav. Správci tyto sestavy pomůžou najít, což je nejužitečnější.

Rozhraní pro vytváření sestav poskytuje konzistentní a komplexnější prostředí pro vytváření sestav. Dostupné sestavy poskytují následující funkce:
- **Hledání a řazení** – můžete hledat a řadit v každém sloupci bez ohledu na to, jak velkou datovou sadu používáte.
- **Stránkování dat** – data můžete kontrolovat na základě stránkování, buď stránky stránky, nebo přechodem na konkrétní stránku.
- **Výkon** – můžete rychle generovat a zobrazovat sestavy vytvořené z velkých klientů.
- **Export** – můžete rychle exportovat data vytváření sestav vygenerovaná z velkých tenantů.

### <a name="who-can-access-the-data"></a>Kdo má přístup k datům?

V protokolech mohou uživatelé s následujícími oprávněními zkontrolovat:

- Globální správce
- Správce služby Intune
- Správci přiřazení k roli Intune s oprávněním **ke čtení**

## <a name="non-compliant-devices-report-operational"></a>Sestava nevyhovujících zařízení (provozní)
Sestava zařízení nedodržujících předpisy poskytuje data, která obvykle používá role helpdesku nebo správce k identifikaci problémů a k nápravě problémů. Data nalezená v této sestavě jsou včasná, volají neočekávané chování a mají smysl. Sestava je k dispozici společně s úlohou, takže zařízení nedodržující předpisy budou dostupná, aniž by bylo nutné procházet aktivní pracovní postupy. Tato sestava poskytuje možnosti filtrování, vyhledávání, stránkování a řazení. Můžete také přejít k podrobnostem, abyste mohli řešit problémy.

Sestavu **zařízení nesplňující požadavky** můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **monitorovat**  >  **zařízení, která nedodržují předpisy**.

    ![Sestava zařízení nedodržujících předpisy](./media/intune-reports/intune-reports-02.png)

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a **vyberete zařízení nedodržující**  >  **předpisy**.

## <a name="windows-10-unhealthy-endpoints-report-operational"></a>Sestava nestavových koncových bodů ve Windows 10 (provozní)
Sestavy pro **koncové body Windows 10 v pořádku** sestavují data Surface, která obvykle používá role helpdesku nebo správce k identifikaci problémů a k nápravě problémů. Data nalezená v této sestavě jsou včasná, volají zařízení, které není v pořádku, primární hlavní název uživatele (UPN) a stav řady nastavení. Sestava je k dispozici jako karta v rámci primární úlohy **antivirové ochrany** . Tato sestava poskytuje filtrování, vyhledávání, stránkování a řazení. 

Sestavu **koncových bodů Windows 10** , které jsou v pořádku, můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Endpoint Security**  >  **antivirový**  >  **program Windows 10 – koncové body**nejsou v pořádku.

## <a name="windows-10-detected-malware-report-operational"></a>Zjištěná zpráva o malwaru Windows 10 (provozní)
Zpráva o **malwaru zjištěná ve Windows 10** poskytuje data k identifikaci zařízení s problémy malwaru a k nápravě problémů. Data, která jsou v této sestavě zastaralá, zavolají zařízení, které není v pořádku, uživatelské jméno a závažnost. Sestava je k dispozici jako karta v rámci primární úlohy **antivirové ochrany** . Tato sestava poskytuje filtrování, vyhledávání, stránkování a řazení. 

Zprávu o **malwaru zjištěné Windows 10** můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Endpoint Security**  >  **Antivirus**  >  **Windows 10 zjištěný malware**.

### <a name="bulk-actions-for-devices"></a>Hromadné akce pro zařízení
Zpráva o **malwaru zjištěná ve Windows 10** poskytuje hromadné akce, které se vztahují na zařízení vybraná v rámci sestavy. Chcete-li použít hromadnou akci, vyberte řádek odpovídající jednotlivým zařízením (až 100 zařízení po dobu) a vyberte akci. K dispozici jsou následující akce:
- **Restartovat** – Tato akce provede restart vybraných zařízení.
- **Rychlé prověřování** – Tato akce provede rychlou kontrolu na vybraných zařízeních v programu Windows Defender. 
- **Úplná kontrola** – Tato akce provede úplnou kontrolu na vybraných zařízeních v programu Windows Defender. 

Další informace o rozdílu mezi *rychlou kontrolou* a *úplným prohledáním*najdete v tématu [Konfigurace naplánovaných rychlých nebo úplných kontrol virů v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/scheduled-catch-up-scans-microsoft-defender-antivirus).

## <a name="feature-update-failures-report-operational"></a>Sestava o chybách aktualizace funkcí (provozní)
Provozní sestava **neúspěšné aktualizace funkcí** poskytuje podrobnosti o selhání pro zařízení, na která cílí zásada **aktualizace funkcí Windows 10** , a pokusy o aktualizaci. Data nalezená v této sestavě jsou včasná a volají počet zařízení s chybami. Můžete přejít k podrobnostem, abyste mohli řešit problémy. Tato sestava poskytuje filtrování, vyhledávání, stránkování a řazení. 

Zprávu o **chybách aktualizace funkcí** si můžete prohlédnout pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **monitorování**  >  **Selhání aktualizací funkcí**.

## <a name="device-compliance-report-organizational"></a>Sestava dodržování předpisů pro zařízení (organizace)

Sestavy dodržování předpisů pro zařízení mají být široké a poskytují obecnější zobrazení pro generování sestav dat k identifikaci agregovaných metrik. Tato sestava je navržena pro práci s velkými datovými sadami, aby získala úplný obrázek o dodržování předpisů zařízením. Například zpráva o dodržování předpisů zařízením pro dodržování předpisů zařízením zobrazuje všechny stavy dodržování předpisů pro zařízení, aby poskytovaly širší pohled na data, bez ohledu na to, jak velkou datovou sadu potřebujete. Tato sestava obsahuje kromě vhodné vizualizace agregovaných metrik úplné členění záznamů. Tuto sestavu můžete vygenerovat pomocí filtrů a výběrem tlačítka generovat sestavu. Tím se aktualizují data, aby se zobrazila poslední stav s možností zobrazení jednotlivých záznamů, které tvoří agregovaná data. Podobně jako u většiny sestav v novém rozhraní se tyto záznamy dají seřadit a prohledat, abyste se mohli zaměřit na informace, které potřebujete.

Chcete-li zobrazit vygenerovanou sestavu stavu zařízení, můžete použít následující postup:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **sestavy** , chcete-li zobrazit souhrn sestav.
3. Vyberte **Dodržování předpisů zařízením**.
4. Vyberte Filtry **stav dodržování předpisů**, **operační systém**a **vlastnictví** k upřesnění sestavy.
5. Chcete-li načíst aktuální data, klikněte na tlačítko **Generovat sestavu** (nebo **znovu vygenerovat**).

    ![Sestava dodržování předpisů pro zařízení](./media/intune-reports/intune-reports-02a.png)

    > [!NOTE]
    > Tato sestava **dodržování předpisů zařízení** poskytuje časové razítko, kdy se sestava naposledy vygenerovala. 

Související informace najdete v tématu [vymáhání dodržování předpisů pro Microsoft Defender ATP s podmíněným přístupem v Intune](../protect/advanced-threat-protection.md).

## <a name="reports-summary"></a>Souhrn sestav 

Sestava dodržování předpisů zařízení je k dispozici jako Souhrnná sestava v úloze **sestav** . K zobrazení sestavy dodržování předpisů zařízením použijte následující postup:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **sestavy** , chcete-li zobrazit souhrn sestav.

    ![Souhrn sestav Intune](./media/intune-reports/intune-reports-01.png)

## <a name="antivirus-agent-status-report-organizational"></a>Zpráva o stavu agenta antivirového programu (organizace)
Sestava **Stav agenta antivirového** programu poskytuje stav agenta pro zařízení vaší organizace. Tato sestava zobrazuje, která zařízení mají ochranu v reálném čase nebo v síti, i jejich stav. Data, která jsou v této sestavě zastaralá, zavolají zařízení, které není v pořádku, uživatelské jméno a závažnost. Sestava je k dispozici z primární úlohy **antivirové ochrany v programu Microsoft Defender** . Tato sestava poskytuje filtrování, vyhledávání, stránkování a řazení. 

Zprávu o **stavu antivirového agenta** si můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Výběr **sestav**  >  Stav agenta antivirové ochrany**antivirového programu společnosti Microsoft Defender**  >  **Antivirus agent status**.

## <a name="detected-malware-report-organizational"></a>Zjištěná zpráva o malwaru (organizace)
Sestava **zjištěného malwaru** poskytuje stav malwaru pro zařízení vaší organizace. Tato sestava zobrazuje počet zařízení se zjištěným malwarem a také podrobnosti o malwaru. Data nalezená v této sestavě jsou zastaralá, volají název a závažnost zařízení a také další podrobnosti související s malwarem. Sestava je k dispozici z primární úlohy **antivirové ochrany v programu Microsoft Defender** . Tato sestava také poskytuje filtrování, vyhledávání, stránkování a řazení. 

Zjištěnou zprávu o **malwaru** můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Výběr **sestav**program  >  **Microsoft Defender Antivirus**  >  **zjistil malware**.

## <a name="windows-10-feature-updates-organizational"></a>Aktualizace funkcí Windows 10 (organizace)
Sestava **aktualizací funkcí Windows 10** poskytuje celkový přehled o dodržování předpisů u zařízení, na která cílí zásada **aktualizace funkcí Windows 10** . Tato sestava uvádí stav aktualizace na základě stavu aktualizace. Můžete si také prohlédnout podrobnosti o konkrétní aktualizaci zařízení. Data zjištěná v těchto sestavách jsou včasná, volají název a stav zařízení a také další podrobnosti související s aktualizací. V úloze **aktualizace systému Windows** je k dispozici Souhrnná sestava. Tato sestava také poskytuje filtrování, vyhledávání, stránkování a řazení. 

Sestavu **aktualizací funkcí Windows 10** můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Pokud **Reports**  >  chcete zobrazit souhrnnou sestavu, vyberte sestavy**aktualizace pro Windows** .
3. Vyberte kartu **sestavy** a kliknutím na **sestavu aktualizace funkcí Windows** Zobrazte sestavu **aktualizace funkcí Windows 10** .

## <a name="device-compliance-trend-report-historical"></a>Sestava trend dodržování předpisů pro zařízení (historická)

Sestavy trendu dodržování předpisů pro zařízení jsou pravděpodobně používány správci a architekty k identifikaci dlouhodobých trendů dodržování předpisů zařízením. Agregovaná data se zobrazují v časovém intervalu a jsou užitečná pro budoucí rozhodování o investicích, řízení procesů a vyšetřování jakýchkoli anomálií. Filtry je také možné použít k zobrazení konkrétních trendů. Data poskytnutá touto sestavou jsou snímkem aktuálního stavu tenanta (téměř v reálném čase). 

Sestava trendu dodržování předpisů zařízením pro trendy dodržování předpisů zařízením může zobrazit trend stavů dodržování předpisů zařízením v časovém intervalu. Můžete určit, kde se nastaly špičky dodržování předpisů, a soustředit se na váš čas a úsilí.

Sestavu **trendů** můžete zobrazit pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **sestavy**  >  **trendy** , abyste zobrazili dodržování předpisů zařízením za 60 dní trendu.

    ![Sestava trendů Intune](./media/intune-reports/intune-reports-03.png)

## <a name="azure-monitor-integration-reports-specialist"></a>Sestavy Azure Monitor Integration (specialista)
Můžete přizpůsobit vlastní sestavy a získat požadovaná data. Data v sestavách budou volitelně k dispozici prostřednictvím [Azure monitor](/azure/azure-monitor/overview) v [sešitech](reports.md#workbooks) [Log Analytics](reports.md#log-analytics) a Azure monitor. Tato řešení umožňují vytvářet vlastní dotazy, konfigurovat výstrahy a vytvářet řídicí panely tak, aby se data o dodržování předpisů zařízením zobrazovala způsobem, který chcete. Kromě toho můžete uchovávat protokoly aktivit v účtu služby Azure Storage, integrovat se sestavami pomocí [nástrojů pro správu událostí a informací o zabezpečení (Siem)](/microsoft-365/security/office-365-security/siem-server-integration)a korelovat sestavy do protokolů aktivit služby Azure AD. K importu řídicích panelů pro potřeby vlastních sestav můžete použít také sešity Azure Monitor.

> [!NOTE]
> Komplexní funkce vytváření sestav vyžadují předplatné Azure.

Ukázková sestavová sestava by mohla společně propojit data vlastnictví zařízení s daty zápisu platforem ve vlastní sestavě. Tato vlastní sestava se pak může zobrazit na existujícím řídicím panelu na portálu Azure Active Directory.

Vlastní sestavy můžete vytvářet a zobrazovat pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **sestavy**  >  **nastavení diagnostiky** přidat [nastavení diagnostiky](reports.md#diagnostic-settings).

    ![Sestavy Intune – přidání nastavení diagnostiky](./media/intune-reports/intune-reports-04.png)

3. Kliknutím na **Přidat nastavení diagnostiky** zobrazíte podokno **nastavení diagnostiky** . 
4. Přidejte **název** nastavení diagnostiky. 
5. Vyberte nastavení **odeslat Log Analytics** a **DeviceComplianceOrg** .

    ![Sestavy Intune – nastavení diagnostiky](./media/intune-reports/intune-reports-04a.png)

6. Klikněte na **Uložit**.
7. V dalším kroku vyberte **Log Analytics** pro vytvoření a spuštění nového dotazu protokolu pomocí [Log Analytics](reports.md#log-analytics).

   ![Log Analytics – dotaz protokolu](./media/intune-reports/intune-reports-05.png)

8. Vyberte **sešity** , chcete-li vytvořit nebo otevřít interaktivní sestavu pomocí [Azure monitor sešity](reports.md#workbooks).

   ![Sešity – interaktivní sestavy](./media/intune-reports/intune-reports-07.png)

### <a name="diagnostic-settings"></a>Nastavení diagnostiky
Každý prostředek Azure vyžaduje vlastní nastavení diagnostiky. Nastavení diagnostiky definuje pro prostředek následující:

- Kategorie protokolů a data metriky, které jsou odesílány do cílů definovaných v nastavení. Dostupné kategorie se budou lišit pro různé typy prostředků.
- Jeden nebo více cílů pro odeslání protokolů. Aktuální cíle zahrnují Log Analytics pracovní prostor, Event Hubs a Azure Storage.
- Zásady uchovávání informací pro data uložená v Azure Storage.

Jedno diagnostické nastavení může definovat jedno ze všech cílů. Pokud chcete odesílat data do více než jednoho konkrétního cílového typu (například dvou různých Log Analytics pracovních prostorů), vytvořte více nastavení. Každý prostředek může mít až 5 nastavení diagnostiky.

Další informace o nastaveních diagnostiky najdete [v tématu Vytvoření nastavení diagnostiky pro shromažďování protokolů a metrik platforem v Azure](/azure/azure-monitor/platform/diagnostic-settings).

### <a name="log-analytics"></a>Log Analytics
Log Analytics je primárním nástrojem v Azure Portal pro zápis dotazů protokolu a interaktivní analýzu výsledků dotazů. I v případě, že se dotaz protokolu používá jinde v Azure Monitor, obvykle nejprve zapíšete a otestujete dotaz pomocí Log Analytics. Podrobnosti o používání Log Analytics a vytváření dotazů protokolu najdete v tématu [Přehled dotazů protokolu v Azure monitor](/azure/azure-monitor/log-query/log-query-overview). 

### <a name="workbooks"></a>Workbooks
Sešity kombinují text, analytické dotazy, metriky Azure a parametry do propracovaných interaktivních sestav. Sešity mohou upravovat všichni ostatní členové týmu, kteří mají přístup ke stejným prostředkům Azure. Další informace o sešitech najdete v tématu [Azure monitor sešity](/azure/azure-monitor/app/usage-workbooks). Můžete také pracovat se šablonami sešitu a přispívat do nich. Další informace najdete v tématu [Azure monitor šablon sešitu](https://go.microsoft.com/fwlink/?linkid=867045).

## <a name="next-steps"></a>Další kroky 

Přečtěte si další informace o těchto technologiích:
- [Blogový Microsoft Intune – rozhraní pro vytváření sestav](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553)
- [Azure Monitor](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor)
- [Co je služba Log Analytics?](/azure/azure-monitor/log-query/log-query-overview#what-is-log-analytics)
- [Dotazy na protokoly](/azure/azure-monitor/log-query/log-query-overview)
- [Začínáme s Log Analytics v Azure Monitor](/azure/azure-monitor/log-query/get-started-portal)
- [Azure Monitor sešity](/azure/azure-monitor/app/usage-workbooks)
- [nástroje pro správu událostí a informací o zabezpečení (SIEM)](/microsoft-365/security/office-365-security/siem-server-integration)