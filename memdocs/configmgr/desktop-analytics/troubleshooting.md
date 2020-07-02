---
title: Řešení potíží s Desktop Analytics
titleSuffix: Configuration Manager
description: Technické podrobnosti, které vám pomůžou při řešení problémů s desktopovou analýzou.
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 68506ba11e356a1e9f14d58880a80bdf3cfcb5f4
ms.sourcegitcommit: fb03634b8494903fc6855ad7f86c8694ffada8df
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85828971"
---
# <a name="troubleshoot-desktop-analytics"></a>Řešení potíží s Desktop Analytics

Podrobnosti v tomto článku vám pomůžou při řešení potíží s integrací Desktop Analytics s Configuration Manager.

## <a name="confirm-prerequisites"></a>Potvrdit požadavky

Mnohé běžné problémy způsobují chybějící požadavky. Nejdřív potvrďte následující konfigurace:

- [Požadavky](overview.md#prerequisites)  

- [Aktualizace součástí Windows](enroll-devices.md#update-devices)  

- [Jak povolit sdílení dat](enable-data-sharing.md), které se zabývá následujícími tématy:  

  - Internetové koncové body, ke kterým se klienti potřebují připojit  

  - Ověřování proxy serveru  

  - Úrovně diagnostických dat  

## <a name="monitor-connection-health"></a>Monitorování stavu připojení

Pomocí řídicího panelu **stavu připojení** v Configuration Manager přejděte k podrobnostem o kategoriích podle stavu zařízení. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte uzel **Údržba Desktop Analytics** a vyberte řídicí panel **stav připojení** .  

Další informace najdete v tématu [monitorování stavu připojení](monitor-connection-health.md).

> [!NOTE]
> Připojení Configuration Manager k Desktop Analytics se spoléhá na spojovací bod služby. Změny této role systému lokality mohou mít vliv na synchronizaci s cloudovou službou. Další informace najdete v tématu [o spojovacím bodu služby](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

Od verze 2002, pokud se lokalita Configuration Manager nepovede připojit k požadovaným koncovým bodům pro cloudovou službu, vyvolá kritickou stavovou zprávu ID 11488. Když se nemůže připojit ke službě, stav součásti SMS_SERVICE_CONNECTOR se změní na kritický. Zobrazit podrobný stav v uzlu [Stav součásti](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) konzoly Configuration Manager.<!-- 5566763 -->

## <a name="log-files"></a>Soubory protokolů

Další informace najdete v tématu [soubory protokolů pro Desktop Analytics](../core/plan-design/hierarchy/log-files.md#desktop-analytics) .

Od verze Configuration Manager 1906 použijte nástroj **DesktopAnalyticsLogsCollector.ps1** z instalačního adresáře Configuration Manager instalace, abyste pomohli řešit problémy s desktopovou analýzou. Spustí se základní kroky pro řešení potíží a shromáždí příslušné protokoly do jednoho pracovního adresáře. Další informace najdete v tématu [kolektor protokolů](log-collector.md).

### <a name="enable-verbose-logging"></a>Zapnout podrobné protokolování

1. V spojovacím bodě služby přejděte na následující klíč registru:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Nastavte hodnotu **LoggingLevel** na`0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a>Aplikace Azure AD

Desktop Analytics přidá do služby Azure AD následující aplikace:

- **Configuration Manager mikroslužba**: připojuje Configuration Manager s desktopovou analýzou. Tato aplikace nemá žádné požadavky na přístup.  

- **MALogAnalyticsReader**: monitoruje pracovní prostor Azure Log Analytics, aby se zajistilo úspěšné zkopírování denního snímku. Další informace najdete v tématu [aplikační role MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- **Desktop Analytics**: umožňuje Configuration Manager načítání informací o plánu nasazení a stavu připravenosti zařízení z Desktop Analytics.

Pokud po dokončení instalace potřebujete tyto aplikace zřídit, otevřete podokno **připojené služby** . Vyberte **Konfigurovat přístup uživatelů a aplikací**a zřiďte aplikace.  

- **Aplikace Azure AD pro Configuration Manager**. Pokud po dokončení instalace potřebujete zřídit nebo vyřešit problémy s připojením, přečtěte si téma [Vytvoření a import aplikace pro Configuration Manager](#create-and-import-app-for-configuration-manager). Tato aplikace vyžaduje **zápis dat kolekce cm** a **čtení dat kolekce cm** v rozhraní API **služby Configuration Manager** .  

### <a name="create-and-import-app-for-configuration-manager"></a>Vytvoření a import aplikace pro Configuration Manager

Pokud nemůžete vytvořit aplikaci Azure AD pro Configuration Manager v Průvodci konfigurací služeb Azure nebo pokud chcete znovu použít existující aplikaci, musíte ji vytvořit a naimportovat ručně. Po dokončení [úvodního zprovoznění](set-up.md#initial-onboarding) na portálu Desktop Analytics použijte následující postup:

#### <a name="create-app-in-azure-ad"></a>Vytvoření aplikace ve službě Azure AD

1. Otevřete [Azure Portal](https://portal.azure.com) jako uživatel s oprávněními *globálního správce* , přejít na **Azure Active Directory**a vyberte **Registrace aplikací**. Pak vyberte **Nová registrace**.  

2. Na panelu **vytvořit** nakonfigurujte následující nastavení:  

    - **Název**: jedinečný název, který identifikuje aplikaci, například:`Desktop-Analytics-Connection`  

    - **Podporované typy účtů**: **účty v tomto organizačním adresáři (Contoso)**

    - **Identifikátor URI přesměrování (volitelné)**: **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Vyberte **Zaregistrovat**.  

3. Vyberte aplikaci, poznamenejte si **ID aplikace (klienta)** a **ID adresáře (tenant)**. Hodnoty jsou identifikátory GUID, které slouží ke konfiguraci Configuration Managerho připojení.  

4. V nabídce **Správa** vyberte **certifikáty & tajných**kódů. Vyberte **Nový tajný klíč klienta**. Zadejte **Popis**, zadejte dobu trvání vypršení platnosti a pak vyberte **Přidat**. Zkopírujte **hodnotu** klíče, která se používá ke konfiguraci Configuration Managerho připojení.

    > [!Important]  
    > Toto je jediná příležitost ke zkopírování hodnoty klíče. Pokud ho teď nezkopírujete, budete muset vytvořit další klíč.  
    >
    > Uložte hodnotu klíče do zabezpečeného umístění.  

5. V nabídce **Správa** vyberte **oprávnění rozhraní API**.  

    1. Na panelu **oprávnění rozhraní API** vyberte **Přidat oprávnění**.  

    2. V panelu **oprávnění rozhraní API** přepněte na **rozhraní API, které moje organizace používá**.  

    3. Vyhledejte a vyberte rozhraní API pro **Configuration Manager mikroslužeb** .  

    4. Vyberte skupinu **oprávnění aplikace** . Rozbalte **CmCollectionData**a vyberte obě následující oprávnění: **zapsat data kolekce cm** a **načíst data kolekce cm**.  

    5. Vyberte **Přidat oprávnění**.  

6. Na panelu **oprávnění rozhraní API** vyberte **udělit souhlas správce...**. Vyberte **Ano**.  

#### <a name="import-app-in-configuration-manager"></a>Importovat aplikaci v Configuration Manager

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Na pásu karet vyberte **Konfigurovat služby Azure** .  

2. Na stránce **služby Azure** v Průvodci službami Azure nakonfigurujte následující nastavení:  

    - Zadejte **název** objektu v Configuration Manager.  

    - Zadejte volitelný **Popis** , který vám usnadní identifikaci služby.  

    - V seznamu dostupných služeb vyberte možnost **Analýza plochy** .  
  
   Vyberte **Další**.  

3. Na stránce **aplikace** vyberte příslušné **prostředí Azure**. Pak vyberte **importovat** pro webovou aplikaci. V okně **importovat aplikace** nakonfigurujte následující nastavení:  

    - **Název tenanta Azure AD**: Tento název se jmenuje v Configuration Manager  

    - **ID tenanta Azure AD**: **ID adresáře** , které jste ZKOPÍROVALi z Azure AD  

    - **ID klienta**: **ID aplikace** , které jste zkopírovali z aplikace Azure AD  

    - **Tajný klíč**: **hodnota** klíče, kterou jste zkopírovali z aplikace Azure AD  

    - **Vypršení platnosti tajného klíče**: stejné datum vypršení platnosti klíče  

    - **Identifikátor URI ID aplikace**: Toto nastavení by se mělo automaticky vyplnit následující hodnota:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Vyberte možnost **ověřit**a potom kliknutím na **tlačítko OK** zavřete okno Importovat aplikace. Na stránce aplikace v Průvodci službami Azure vyberte **Další** .  

Chcete-li pokračovat v průvodci na stránce **diagnostická data** , přečtěte si téma [připojení ke službě](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Řešení potíží s aplikací v Configuration Manager

Pokud máte problémy s vytvářením nebo importem aplikace, nejprve si prohlédněte **SMSAdminUI. log** pro konkrétní chybu. Pak zkontrolujte následující konfigurace:

- Úspěšně jste zaregistrovali klienta ve službě Desktop Analytics. Další informace najdete v tématu [jak nastavit analýzu plochy](set-up.md).

- Všechny požadované koncové body jsou přístupné. Další informace najdete v tématu [koncové body](enable-data-sharing.md#endpoints).

- Ujistěte se, že uživatel, který se přihlásí, má správná oprávnění. Další informace najdete v tématu [předpoklady](overview.md#prerequisites).

- Ujistěte se, že se uživatel může přihlásit k Azure obecně. Tato akce určuje, jestli existují nějaké Obecné problémy s ověřováním Azure AD.

- Zkontroluje stavové zprávy pro součást **SMS_SERVICE_CONNECTOR** týkající se *pracovního procesu Desktop Analytics*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a>Role aplikace MALogAnalyticsReader

Při nastavování Desktop Analytics souhlasíte jménem vaší organizace. Tímto souhlasem je přiřazení aplikace MALogAnalyticsReader k pracovnímu prostoru role čtecího modulu Log Analytics. Tato role aplikace je vyžadována analýzou plochy.

Pokud dojde k potížím s tímto procesem během instalace, použijte k ručnímu přidání tohoto oprávnění následující postup:

1. Otevřete [Azure Portal](https://portal.azure.com)a vyberte **všechny prostředky**. Vyberte pracovní prostor typu **Log Analytics**.  

2. V nabídce pracovní prostor vyberte **řízení přístupu (IAM)** a pak vyberte **Přidat**.  

3. Na panelu **Přidat oprávnění** nakonfigurujte následující nastavení:  

    - **Role**: **Čtenář**  

    - **Přiřadit přístup k**: **uživatel, skupina nebo aplikace Azure AD**  

    - **Vyberte**: **MALogAnalyticsReader**  

4. Vyberte **Uložit**.

Na portálu se zobrazí oznámení, že se přidalo přiřazení role.

## <a name="data-latency"></a>Latence dat

<!-- 3846531 -->
Když nakonfigurujete Desktop Analytics, zaregistrujete nové klienty nebo nakonfigurujete nové plány nasazení, sestavy v Configuration Manager a portálu pro analýzu plochy nemusí okamžitě zobrazovat úplná data. Může to trvat 2-3 dní, než se dostanou tyto kroky:

- Aktivní zařízení odesílají diagnostická data do služby Desktop Analytics.
- Služba zpracovává data.
- Služba se synchronizuje s vaším Configuration Managerovým webem

Když synchronizujete kolekce zařízení z hierarchie Configuration Manager k Desktop Analytics, může trvat až jednu hodinu, než se tyto kolekce objeví na portálu Desktop Analytics. Podobně při vytváření plánu nasazení v Desktop Analytics může trvat až jednu hodinu, než se nové kolekce spojené s plánem nasazení zobrazí v hierarchii Configuration Manager. Primární lokality vytvoří kolekce a lokalita centrální správy se synchronizuje s desktopovou analýzou. Configuration Manager může trvat až 24 hodin, než se vyhodnotí a aktualizuje členství v kolekci. Pro urychlení tohoto procesu ručně aktualizujte členství v kolekci.<!-- 4984639 -->

> [!Note]
> Pro aktualizace ručních kolekcí, aby odrážely změny, musí být nejprve součást SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker synchronizována. Spuštění tohoto procesu může trvat až jednu hodinu. Další informace najdete v tématu **M365ADeploymentPlanWorker. log**.

V portálu pro Desktop Analytics existují dva typy dat: **data správců** a **diagnostická data**:

- **Data správců** se vztahují na všechny změny, které provedete v konfiguraci pracovního prostoru. Například při změně **rozhodnutí o upgradu** prostředku nebo **důležitosti** , kterou měníte data správců. Tyto změny mají často složený efekt, protože mohou změnit stav připravenosti zařízení na nainstalovanou majetkovou položku.

- **Diagnostická data** odkazují na metadata systému odeslaná z klientských zařízení do společnosti Microsoft. Tato data se vyjedná z desktopové analýzy. Zahrnuje atributy jako inventář zařízení a stav aktualizace zabezpečení a funkcí.

Ve výchozím nastavení se všechna data na portálu Desktop Analytics automaticky aktualizují každý den. Tato aktualizace zahrnuje změny v diagnostických datech před dvěma dny a všechny změny provedené v konfiguraci (data správců). Měl by se zobrazit na portálu Desktop Analytics o každý den v čase 08:00 UTC.

Když provedete změny dat správců, můžete aktivovat aktualizaci dat správců na vyžádání v pracovním prostoru. Na libovolné stránce portálu Desktop Analytics otevřete informační rámeček měna data:

![Snímek karty informačního rámečku datové měny na portálu Desktop Analytics](media/data-currency-flyout.png)

Pak vyberte **použít změny**:

![Snímek obrazovky s plovoucím panelem měna dat v portálu pro Desktop Analytics](media/data-currency-flyout-expand.png)

Tento proces obvykle trvá mezi 15-60 minutami. Časování závisí na velikosti vašeho pracovního prostoru a rozsahu změn, které vyžadují procesy. Když si vyžádáte aktualizaci dat na vyžádání, nevede to k žádným změnám diagnostických dat.  Další informace najdete v tématu [Nejčastější dotazy k Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Pokud se změny v časových snímcích, které jsou uvedené výše, nezobrazuje, počkejte další 24 hodin na příští denní aktualizaci. Pokud se zobrazí delší prodlevy, zkontrolujte řídicí panel stavu služby. Pokud se služba hlásí jako v pořádku, obraťte se na podporu Microsoftu.<!-- 3896921 -->

> [!IMPORTANT]
> Možnost Analytics pro stolní počítače, která **zobrazuje poslední data** , je zastaralá. Tato akce bude odebrána v budoucí verzi služby Desktop Analytics. Další informace najdete v tématu [zastaralé funkce](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="service-notifications"></a>Oznámení služby

<!-- 4982509 -->

Portál pro Desktop Analytics může zobrazit bannery oznámení správcům. Tato oznámení umožňují Microsoftu komunikovat s vámi o důležitých událostech a problémech. Následující části obsahují podrobnosti o oznámeních, která se mohou zobrazit.

### <a name="see-whats-new-this-month-in-desktop-analytics"></a>Podívejte se, co je nového v tomto měsíci v Desktop Analytics.

Toto informativní oznámení vám poskytne informace o změnách služby. Další informace najdete v tématu [co je nového v Desktop Analytics](whats-new.md) ( `https://aka.ms/danews` ).

### <a name="there-are-new-prerequisites-to-continue-using-desktop-analytics-review-the-new-requirements"></a>Existují nové požadavky. Pokud chcete pokračovat v používání Desktop Analytics, přečtěte si nové požadavky.

Toto informativní oznámení vám poskytne informace o změnách požadavků. Například nový koncový bod sítě Internet nebo aktualizace softwaru. Další informace najdete v tématu [předpoklady](overview.md#prerequisites) ( `https://aka.ms/daprereqs` ).

### <a name="were-investigating-an-issue-that-impacts-desktop-analytics"></a>Zkoumáme problém, který ovlivňuje analýzu stolních počítačů.

Toto upozornění indikuje, že společnost Microsoft ví o problému, který ovlivňuje službu Desktop Analytics. Problém obvykle vygeneruje snímky. Když se zobrazí toto oznámení, společnost Microsoft prozkoumá problém, který určí rozsah a zdroj dopadu. Nemusíte kontaktovat podpora Microsoftu. Další informace najdete v tématu [tok dat](privacy.md#data-flow).

### <a name="were-investigating-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Zkoumáme problém s latencí dat. Pokud jste během posledních 24 hodin zaregistrovali nová zařízení nebo jste změnili nějaké prostředky, nemusí se zdát hned.

Toto upozornění indikuje, že společnost Microsoft ví o problému, který ovlivňuje službu Desktop Analytics. Microsoft nepřetržitě monitoruje službu a potvrzuje, že všechny součásti aktualizují snímky ve správný čas. Během tohoto monitorování se jedna z těchto komponent nedokončila podle očekávání. Jakmile se zobrazí toto oznámení, vyzkoumá Microsoft problém. Nemusíte kontaktovat podpora Microsoftu. Další informace najdete v tématu [tok dat](privacy.md#data-flow).

Pokud jste nedávno [zaregistrovaná zařízení](enroll-devices.md) nebo [změnili prostředky,](about-assets.md)počkejte, až společnost Microsoft problém vyřeší. Nemusíte opakovat žádné akce.

### <a name="weve-resolved-a-temporary-issue-with-data-latency-daily-refresh-of-portal-data-is-delayed"></a>Vyřešili jsme dočasný problém s latencí dat. Denní aktualizace dat portálu je zpožděná.

Toto oznámení vám oznamuje, že došlo k potížím s latencí dat. Služba stále zpracovává snímek a aktualizace dat je zpožděna. Další informace najdete v tématu [latence dat](#data-latency).

### <a name="weve-resolved-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Vyřešili jsme problém s latencí dat. Pokud jste během posledních 24 hodin zaregistrovali nová zařízení nebo jste změnili nějaké prostředky, nemusí se zdát hned.

Toto oznámení vám umožní zjistit, že společnost Microsoft vyřešila dříve nahlášený problém s latencí dat. Můžou se zobrazit zastaralá data pro zítřejší snímek. Pokud jste [zaregistrovali zařízení](enroll-devices.md) nebo udělali změny konfigurace zařízení za posledních 24 hodin, neuvidíte je hned na portálu. K kategorizaci [prostředků](about-assets.md) a přípravě [plánů nasazení](about-deployment-plans.md)můžete dál používat desktopovou analýzu. Tyto akce mohou použít data z předchozího snímku.

### <a name="weve-resolved-an-issue-with-desktop-analytics-daily-refresh-of-the-portal-data-is-on-track"></a>Vyřešili jsme problém s desktopovou analýzou. Denní aktualizace dat portálu se sleduje.

Toto oznámení vám oznamuje, že Microsoft identifikoval komponentu snímku, která během zpracování zastavila práci. Společnost Microsoft restartovala komponentu, což bude trvat čas na zpracování snímku. Microsoft nepřetržitě monitoruje službu a potvrzuje, že všechny součásti aktualizují snímky ve správný čas.
