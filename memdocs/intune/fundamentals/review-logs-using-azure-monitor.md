---
title: Směrování protokolů k Azure Monitor pomocí Microsoft Intune-Azure | Microsoft Docs
description: Pomocí nastavení diagnostiky můžete odesílat protokoly auditu a provozní protokoly v Microsoft Intune do účtu úložiště Azure, centra událostí nebo Log Analytics. Určete, jak dlouho chcete data uchovávat, a zobrazte si odhadované náklady pro klienty s různou velikostí.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/12/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 95191d64-9895-4f2e-8c5b-f0e85be086d8
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e8045ac53369a471ce232f0eca3e185be2e3e85
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330663"
---
# <a name="send-log-data-to-storage-event-hubs-or-log-analytics-in-intune-preview"></a>Odeslání dat protokolu do úložiště, centra událostí nebo Log Analytics v Intune (Preview)

Microsoft Intune obsahují integrované protokoly, které poskytují informace o vašem prostředí:

- **Protokoly auditu** zobrazují záznam aktivit, které generují změnu v Intune, včetně možnosti vytvořit, aktualizovat (Upravit), odstranit, přiřadit a vzdálené akce.
- **Operační protokoly (Preview)** zobrazují podrobnosti o uživatelích a zařízeních, která se úspěšně (nebo nezdařila) k registraci, a podrobnosti o nevyhovujících zařízeních.
- **Protokoly organizace pro dodržování předpisů zařízením (Preview)** zobrazit sestavu organizace pro dodržování předpisů zařízením v Intune a podrobnosti o nevyhovujících zařízeních.

Tyto protokoly je taky možné posílat do Azure Monitor služeb, včetně účtů úložiště, Center událostí a Log Analytics. Konkrétně můžete:

* Archivujte protokoly Intune do účtu služby Azure Storage, aby se data zachovala, nebo se budou archivovat na nastavený čas.
* Streamování protokolů Intune do centra událostí Azure pro analýzy pomocí oblíbených nástrojů pro správu událostí a SIEM (Security Information and Event Management), jako je Splunk a QRadar.
* Integrujte protokoly Intune s vlastními řešeními protokolů tak, že je streamujte do centra událostí.
* Odešlete protokoly Intune pro Log Analytics, abyste povolili bohatou vizualizaci, monitorování a upozorňování na připojená data.

Tyto funkce jsou součástí **nastavení diagnostiky** v Intune.

V tomto článku se dozvíte, jak pomocí **nastavení diagnostiky** odesílat data protokolu různým službám, nabízí příklady a odhad nákladů a odpovědi na některé běžné dotazy. Po povolení této funkce budou protokoly směrovány na Azure Monitor službu, kterou zvolíte.

## <a name="prerequisites"></a>Požadavky

Pokud chcete používat tuto funkci, potřebujete tyto položky:

* Předplatné Azure: Pokud ještě nemáte předplatné Azure, můžete si [zaregistrovat bezplatnou zkušební verzi](https://azure.microsoft.com/free/).
* Prostředí Microsoft Intune (tenant) v Azure
* Uživatel, který je **globálním správcem** nebo **správcem služby Intune** pro tenanta Intune.

V závislosti na tom, kde chcete směrovat data protokolu auditu, potřebujete jednu z následujících služeb:

* [Účet služby Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-account-overview) s oprávněními *klíče listkey* . Doporučujeme použít obecný účet úložiště, nikoli účet Blob Storage. Informace o cenách úložiště najdete v [cenové kalkulačce služby Azure Storage](https://azure.microsoft.com/pricing/calculator/?service=storage). 
* [Obor názvů centra událostí Azure](https://docs.microsoft.com/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) , který se má integrovat s řešeními třetích stran.
* [Pracovní prostor Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) pro odesílání protokolů do Log Analytics.

## <a name="send-logs-to-azure-monitor"></a>Odeslat protokoly do Azure monitoru

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost **sestavy** > **nastavení diagnostiky**. Když ho otevřete poprvé, zapněte ho. V opačném případě přidejte nastavení.

    > [!div class="mx-imgBorder"]
    > ![Zapnutím nastavení diagnostiky v Intune odešlete protokoly do Azure Monitor](./media/review-logs-using-azure-monitor/diagnostics-settings-turn-on.png)

3. Zadejte tyto vlastnosti:

    - **Název**: zadejte název pro nastavení diagnostiky. Toto nastavení zahrnuje všechny vlastnosti, které zadáte. Zadejte například `Route audit logs to storage account`.
    - **Archivovat do účtu úložiště**: uloží data protokolu do účtu služby Azure Storage. Tuto možnost použijte, pokud chcete data uložit nebo archivovat.

        1. Vyberte tuto možnost > **nakonfigurovat**. 
        2. V seznamu vyberte existující účet úložiště > **OK**.

    - **Streamování do centra událostí**: streamuje protokoly do centra událostí Azure. Pokud chcete analyzovat data protokolu pomocí nástrojů SIEM, jako je Splunk a QRadar, vyberte tuto možnost.

        1. Vyberte tuto možnost > **nakonfigurovat**. 
        2. V seznamu vyberte existující obor názvů a zásadu centra událostí > **OK**.

    - **Odeslat do Log Analytics**: odesílá data do služby Azure Log Analytics. Pokud chcete používat vizualizace, monitorování a upozorňování na protokoly, vyberte tuto možnost.

        1. Vyberte tuto možnost > **nakonfigurovat**. 
        2. Vytvořte nový pracovní prostor a zadejte podrobnosti o pracovním prostoru. Nebo vyberte existující pracovní prostor ze seznamu > **OK**.

            Další podrobnosti o těchto nastaveních najdete v [pracovním prostoru Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) .

    - **LOG** > **AuditLogs**: tuto možnost vyberte, pokud chcete odesílat [protokoly auditu Intune](monitor-audit-logs.md) do svého účtu úložiště, centra událostí nebo Log Analytics. Protokoly auditu zobrazují historii každého úkolu, který v Intune generuje změnu, včetně toho, kdo ho a kdy.

      Pokud se rozhodnete použít účet úložiště, zadejte také počet dní, po které chcete zachovat data (uchování). Chcete-li zachovat data navždy, nastavte dobu **uchování (dny)** na `0` (nula).

    - **LOG** > **OperationalLogs**: operační protokoly (Preview) zobrazuje úspěšnost nebo neúspěch uživatelů a zařízení, která se registrují v Intune, a také podrobnosti o nevyhovujících zařízeních. Tuto možnost vyberte, pokud chcete odesílat protokoly zápisu do svého účtu úložiště, centra událostí nebo Log Analytics.

      Pokud se rozhodnete použít účet úložiště, zadejte také počet dní, po které chcete zachovat data (uchování). Chcete-li zachovat data navždy, nastavte dobu **uchování (dny)** na `0` (nula).

      > [!NOTE]
      > Provozní protokoly jsou ve verzi Preview. Pokud chcete poskytnout zpětnou vazbu, včetně informací v provozních protokolech, navštivte web [UserVoice](https://microsoftintune.uservoice.com/forums/291681-ideas/suggestions/36613948-diagnostics-settings-feedback).

    - **LOG** > **DeviceComplianceOrg**: protokoly organizace pro dodržování předpisů zařízením (Preview) zobrazení sestavy organizace pro dodržování předpisů zařízením v Intune a podrobnosti o nevyhovujících zařízeních. Tuto možnost vyberte, pokud chcete odesílat protokoly dodržování předpisů do svého účtu úložiště, centra událostí nebo Log Analytics.

      Pokud se rozhodnete použít účet úložiště, zadejte také počet dní, po které chcete zachovat data (uchování). Chcete-li zachovat data navždy, nastavte dobu **uchování (dny)** na `0` (nula).
 
      > [!NOTE]
      > Protokoly organizace pro dodržování předpisů zařízením jsou ve verzi Preview. Pokud chcete poskytnout zpětnou vazbu, včetně informací v sestavě, navštivte web [UserVoice](https://microsoftintune.uservoice.com/forums/291681-ideas/suggestions/36613948-diagnostics-settings-feedback).

    Po dokončení bude vaše nastavení vypadat podobně jako u následujících nastavení: 

    > [!div class="mx-imgBorder"]
    > ![Ukázkový obrázek, který odesílá protokoly auditu Intune do účtu služby Azure Storage](./media/review-logs-using-azure-monitor/diagnostics-settings-example.png)

4. **Uložte** změny. Vaše nastavení se zobrazí v seznamu. Po vytvoření můžete nastavení změnit výběrem možnosti **Upravit nastavení** > **Uložit**.

## <a name="use-audit-logs-throughout-intune"></a>Používání protokolů auditu v Intune

Protokoly auditu můžete exportovat i v jiných částech Intune, včetně registrace, dodržování předpisů, konfigurace, zařízení, klientských aplikací a dalších.

Další informace najdete v tématu [sledování a monitorování událostí pomocí protokolů auditu](monitor-audit-logs.md). Můžete zvolit, kam chcete protokoly auditu odeslat, jak je popsáno v tématu [odeslání protokolů do služby Azure monitor](#send-logs-to-azure-monitor) (v tomto článku).

## <a name="audit-log-properties"></a>Vlastnosti protokolu auditu

V protokolu auditu můžete najít vlastnosti, které mají konkrétní hodnoty. Následující tabulka uvádí tyto podrobnosti.

| Vlastnost | Popis vlastnosti | Hodnoty |
|----------------|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ActivityType  | Akce, kterou správce potřebuje. | Vytvořit, odstranit, opravit, akce, SetReference, Removereference –, získat, Hledat |
| ActorType  | Osoba, která přijímá akci | Neznámý = 0, ItPro, IW, System, partner, aplikace, GuestUser |
| Kategorie  | Podokno, ve kterém byla akce provedena | Jiné = 0, zápis = 1, dodržování předpisů = 2, DeviceConfiguration = 3, zařízení = 4, aplikace = 5, EBookManagement = 6, ConditionalAccess = 7, OnPremiseAccess = 8, role = 9, SoftwareUpdates = 10, DeviceSetupConfiguration = 11, DeviceIntent = 12, DeviceIntentSetting = 13, DeviceSecurity = 14, GroupPolicyAnalytics = 15 |
| ActivityResult | Zda byla akce úspěšná nebo ne. | Úspěch = 1 |

## <a name="cost-considerations"></a>Důležité informace o nákladech

Pokud už máte licenci Microsoft Intune, budete k nastavení účtu úložiště a centra událostí potřebovat předplatné Azure. Předplatné Azure je obvykle bezplatné. Ale platíte za využívání prostředků Azure, včetně účtu úložiště pro archivaci a centra událostí pro streamování. Množství dat a náklady se liší v závislosti na velikosti tenanta.

### <a name="storage-size-for-activity-logs"></a>Velikost úložiště pro protokoly aktivit

Každá událost protokolu auditu zabere v úložišti dat asi 2 kB. Pro tenanta s 100 000 uživateli můžete mít přibližně 1 500 000 událostí za den. Možná budete potřebovat přibližně 3 GB úložiště dat za den. Vzhledem k tomu, že zápisy obvykle probíhá v rámci pěti minut, můžete očekávat přibližně 9 000 operací zápisu za měsíc.

V následujících tabulkách je uveden odhad nákladů v závislosti na velikosti tenanta. Zahrnuje taky účet úložiště pro obecné účely V2 v Západní USA aspoň na jeden rok uchovávání dat. Pokud chcete získat odhad objemu dat, který pro vaše protokoly očekáváte, použijte [cenovou kalkulačku služby Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).

**Protokol auditu s 100 000 uživateli**

| | |
|---|---|
|Počet událostí za den| 1,5 milionu|
|Odhadovaný objem dat za měsíc| 90 GB|
|Odhadované náklady za měsíc (USD)| 1,93 USD|
|Odhadované náklady za rok (USD)| 23,12 USD|

**Protokol auditu s 1 000 uživateli**

| | |
|---|---|
|Počet událostí za den| 15 000|
|Odhadovaný objem dat za měsíc| 900 MB|
|Odhadované náklady za měsíc (USD)| 0,02 USD|
|Odhadované náklady za rok (USD)| 0,24 USD|

### <a name="event-hub-messages-for-activity-logs"></a>Zprávy centra událostí pro protokoly aktivit

Události se obvykle účtují v intervalech po pěti minutách a odesílají se jako jediná zpráva se všemi událostmi v daném časovém rámci. Zpráva v centru událostí má maximální velikost 256 KB. Pokud celková velikost všech zpráv v rámci časového rámce překročí tento svazek, pošle se více zpráv.

Například přibližně 18 událostí za sekundu se obvykle používá pro velký tenant více než 100 000 uživatelů. To je rovno 5 400 událostem každých pět minut (300 sekund × 18 událostí). Protokoly auditu mají přibližně 2 KB na jednu událost. To je rovno 10,8 MB dat. Proto se zprávy 43 odesílají do centra událostí v intervalu 5 minut.

Následující tabulka obsahuje odhad měsíčních nákladů na základní centrum událostí v oblasti USA – západ v závislosti na objemu dat událostí. Pokud chcete získat odhad objemu dat, který jste očekávali v protokolech, použijte [cenovou kalkulačku Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

**Protokol auditu s 100 000 uživateli**

| | |
|---|---|
|Počet událostí za sekundu| 18|
|Počet událostí za pětiminutový interval| 5 400|
|Objem za interval| 10,8 MB|
|Počet zpráv za interval| 43|
|Počet zpráv za měsíc| 371 520|
|Odhadované náklady za měsíc (USD)| 10,83 USD|

**Protokol auditu s 1 000 uživateli**

| | |
|---|---|
|Počet událostí za sekundu|0.1 |
|Počet událostí za pětiminutový interval| 52|
|Objem za interval|104 kB |
|Počet zpráv za interval|1 |
|Počet zpráv za měsíc|8 640 |
|Odhadované náklady za měsíc (USD)|10,80 USD |

### <a name="log-analytics-cost-considerations"></a>Log Analytics – požadavky na náklady

Pokud chcete zkontrolovat náklady související se správou pracovního prostoru Log Analytics, přečtěte si téma [Správa nákladů pomocí řízení objemu dat a uchování v Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-cost-storage).

## <a name="frequently-asked-questions"></a>Nejčastější dotazy

Získejte odpovědi na nejčastější dotazy a přečtěte si o známých problémech s protokoly Intune v Azure Monitor.

### <a name="which-logs-are-included"></a>Které protokoly jsou zahrnuty?

Protokoly auditu a provozní (ve verzi Preview) jsou k dispozici pro směrování pomocí této funkce.

### <a name="after-an-action-when-do-the-corresponding-logs-show-up-in-the-event-hub"></a>Když se po akci zobrazí odpovídající protokoly v centru událostí?

Protokoly se obvykle zobrazují v centru událostí do několika minut po provedení akce. [Co je Azure Event Hubs?](https://docs.microsoft.com/azure/event-hubs/) poskytuje další informace.

### <a name="after-an-action-when-do-the-corresponding-logs-show-up-in-the-storage-account"></a>Když se po akci zobrazí odpovídající protokoly v účtu úložiště?

U účtů Azure Storage je latence kdekoli od 5 do 15 minut od spuštění akce.

### <a name="what-happens-if-an-administrator-changes-the-retention-period-of-a-diagnostic-setting"></a>Co se stane, když správce změní dobu uchování nastavení diagnostiky?

Nové zásady uchovávání informací se aplikují na protokoly shromážděné po změně. Protokoly shromážděné před změnou zásad nebudou nijak ovlivněny.

### <a name="how-much-does-it-cost-to-store-my-data"></a>Kolik stojí za to, že se mají data ukládat?

Náklady na úložiště závisí na velikosti vašich protokolů a na době uchování, kterou zvolíte. Seznam odhadovaných nákladů na klienty, které závisí na vygenerovaném svazku protokolu, najdete v části [velikost úložiště pro protokoly aktivit](#storage-size-for-activity-logs) (v tomto článku).

### <a name="how-much-does-it-cost-to-stream-my-data-to-an-event-hub"></a>Kolik stojí za streamování dat do centra událostí?

Náklady na streamování závisí na počtu přijatých zpráv za minutu. Podrobnosti o výpočtu nákladů a odhadech nákladů na základě počtu zpráv najdete v tématu [zprávy centra událostí pro protokoly aktivit](#event-hub-messages-for-activity-logs) (v tomto článku).

### <a name="how-do-i-integrate-intune-audit-logs-with-my-siem-system"></a>Návody integrovat protokoly auditu Intune se svým systémem SIEM?

Pomocí služeb Azure Monitor a Event Hubs můžete protokoly streamovat do systému SIEM. Nejdřív [Streamujte protokoly do centra událostí](https://docs.microsoft.com/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub). Pak [nastavte nástroj Siem](https://docs.microsoft.com/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub#access-data-from-your-event-hub) pomocí nakonfigurovaného centra událostí. 

### <a name="what-siem-tools-are-currently-supported"></a>Jaké nástroje SIEM se v tuto chvíli podporují?

V současné době je Azure Monitor podporován [logikou](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory) [Splunk](https://docs.microsoft.com/azure/active-directory/reports-monitoring/tutorial-integrate-activity-logs-with-splunk), QRadar a sumo (otevře nový web). Další informace o fungování konektorů najdete v tématu [Streamování dat monitorování Azure do centra událostí, aby je mohl používat externí nástroj](https://docs.microsoft.com/azure/azure-monitor/platform/stream-monitoring-data-event-hubs).

### <a name="can-i-access-the-data-from-an-event-hub-without-using-an-external-siem-tool"></a>Můžu získat přístup k datům z centra událostí bez použití externího nástroje SIEM?

Ano. Pro přístup k protokolům z vlastní aplikace můžete použít [rozhraní API služby Event Hubs](https://docs.microsoft.com/azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph).

### <a name="what-data-is-stored"></a>Jaká data jsou uložená?

Intune neukládá žádná data odesílaná prostřednictvím kanálu. Intune směruje data do kanálu Azure Monitor, a to na autoritě tenanta. Další informace najdete v tématu [přehled Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview).

## <a name="next-steps"></a>Další kroky

* [Archivace protokolů aktivit do účtu úložiště](https://docs.microsoft.com/azure/active-directory/reports-monitoring/quickstart-azure-monitor-route-logs-to-storage-account)
* [Směrování protokolů aktivit do centra událostí](https://docs.microsoft.com/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub)
* [Integrace protokolů aktivit s využitím Log Analytics](https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)
