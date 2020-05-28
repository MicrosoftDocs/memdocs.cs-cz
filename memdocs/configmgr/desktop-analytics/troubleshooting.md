---
title: Řešení potíží s Desktop Analytics
titleSuffix: Configuration Manager
description: Technické podrobnosti, které vám pomůžou při řešení problémů s desktopovou analýzou.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 69694fa39375daf436abf59fcd48edda41a9fc62
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268245"
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

Od verze Configuration Manager 1906 použijte nástroj **DesktopAnalyticsLogsCollector. ps1** z instalačního adresáře Configuration Manager, abyste pomohli řešit problémy s nástrojem Desktop Analytics. Spustí se základní kroky pro řešení potíží a shromáždí příslušné protokoly do jednoho pracovního adresáře. Další informace najdete v tématu [kolektor protokolů](log-collector.md).

### <a name="enable-verbose-logging"></a>Zapnout podrobné protokolování

1. V spojovacím bodě služby přejděte na následující klíč registru:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Nastavte hodnotu **LoggingLevel** na`0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a>Aplikace Azure AD

Desktop Analytics přidá do služby Azure AD následující aplikace:

- **Configuration Manager mikroslužba**: připojuje Configuration Manager s desktopovou analýzou. Tato aplikace nemá žádné požadavky na přístup.  

- **MALogAnalyticsReader**: monitoruje pracovní prostor Azure Log Analytics, aby se zajistilo úspěšné zkopírování denního snímku. Další informace najdete v tématu [aplikační role MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- **Správce klienta Office 365**: umožňuje Configuration Manager načítání informací o plánu nasazení a stavu připravenosti zařízení z Desktop Analytics.

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

Ve výchozím nastavení se všechna data na portálu Desktop Analytics automaticky aktualizují každý den. Tato aktualizace zahrnuje změny v diagnostických datech a všechny změny provedené v konfiguraci (data správců). Měl by se zobrazit na portálu Desktop Analytics o každý den v čase 08:00 UTC.

Když provedete změny dat správců, můžete aktivovat aktualizaci dat správců na vyžádání v pracovním prostoru. Na libovolné stránce portálu Desktop Analytics otevřete informační rámeček měna data:

![Snímek karty informačního rámečku datové měny na portálu Desktop Analytics](media/data-currency-flyout.png)

Pak vyberte **použít změny**:

![Snímek obrazovky s plovoucím panelem měna dat v portálu pro Desktop Analytics](media/data-currency-flyout-expand.png)

Tento proces obvykle trvá mezi 15-60 minutami. Časování závisí na velikosti vašeho pracovního prostoru a rozsahu změn, které vyžadují procesy. Když si vyžádáte aktualizaci dat na vyžádání, nevede to k žádným změnám diagnostických dat.  Další informace najdete v tématu [Nejčastější dotazy k Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Pokud se změny v časových snímcích, které jsou uvedené výše, nezobrazuje, počkejte další 24 hodin na příští denní aktualizaci. Pokud se zobrazí delší prodlevy, zkontrolujte řídicí panel stavu služby. Pokud se služba hlásí jako v pořádku, obraťte se na podporu Microsoftu.<!-- 3896921 -->

> [!IMPORTANT]
> Možnost Analytics pro stolní počítače, která **zobrazuje poslední data** , je zastaralá. Tato akce bude odebrána v budoucí verzi služby Desktop Analytics. Další informace najdete v tématu [zastaralé funkce](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  
