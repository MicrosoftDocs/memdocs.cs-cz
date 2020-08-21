---
title: Konfigurace služeb Azure
titleSuffix: Configuration Manager
description: Připojte své Configuration Manager prostředí se službami Azure pro správu cloudu, Microsoft Store pro firmy a Log Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7cb0a2c71a3ea326348b87d6b34e3109a8ef9f20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700125"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Konfigurace služeb Azure pro použití s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí **Průvodce službami Azure** můžete zjednodušit proces konfigurace cloudových služeb Azure, které používáte s Configuration Manager. Tento průvodce poskytuje společné prostředí pro konfiguraci pomocí služby Azure Active Directory (Azure AD) pro registraci webových aplikací. Tyto aplikace poskytují podrobnosti o předplatném a konfiguraci a ověřují komunikaci s Azure AD. Aplikace nahrazuje stejné informace pokaždé, když nastavíte novou Configuration Manager komponentu nebo službu s Azure.

## <a name="available-services"></a>Dostupné služby

Pomocí tohoto průvodce nakonfigurujte následující služby Azure:  

- **Správa cloudu**: Tato služba umožňuje lokalitám a klientům ověřování pomocí Azure AD. Toto ověřování umožňuje použití dalších scénářů, například:  

  - [Instalace a přiřazení Configuration Manager klientů s Windows 10, kteří používají Azure AD k ověřování](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Konfigurace zjišťování uživatelů Azure AD](configure-discovery-methods.md#azureaadisc)  

  - [Konfigurace zjišťování skupin uživatelů Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Podpora určitých [scénářů bran pro správu cloudu](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

  - [E-mailová oznámení o schválení aplikace](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Konektor Log Analytics**: [Připojte se k Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm). Synchronizovat data kolekce do Log Analytics.  

    > [!Note]  
    > Tento článek odkazuje na *konektor Log Analytics*, který se dřív nazýval *konektor OMS*. Neexistuje žádný funkční rozdíl. Další informace najdete v tématu [Správa Azure – monitorování](/azure/azure-monitor/terminology#log-analytics).  

- **Microsoft Store pro firmy**: Připojte se k [Microsoft Store pro firmy](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Získejte aplikace pro Store ve vaší organizaci, které můžete nasadit pomocí Configuration Manager.  

### <a name="service-details"></a>Podrobnosti služby

V následující tabulce jsou uvedeny podrobnosti o jednotlivých službách.  

- **Klienti**: počet instancí služby, které můžete konfigurovat. Každá instance musí být odlišného tenanta Azure AD.  

- **Cloudy**: všechny služby podporují globální cloud Azure, ale ne všechny služby podporují privátní cloudy, jako je Cloud pro státní správu Azure USA.  

- **Webová aplikace**: zda služba používá aplikaci Azure AD typu *Webová aplikace nebo rozhraní API*, označovanou také jako serverová aplikace v Configuration Manager.  

- **Nativní aplikace**: jestli služba používá aplikaci Azure AD typu *Native*, která se také označuje jako klientská aplikace v Configuration Manager.  

- **Akce**: jestli můžete tyto aplikace naimportovat nebo vytvořit v průvodci Configuration Manager služby Azure.  

|Služba  |Tenanti  |Cloudy  |Webová aplikace  |Native app  |Akce  |
|---------|---------|---------|---------|---------|---------|
|Správa cloudu pomocí<br>Zjišťování Azure AD | Několik | Veřejné, soukromé | ![Podporováno](media/green_check.png) | ![Podporováno](media/green_check.png) | Importovat, vytvořit |
|Konektor Log Analytics | Jednu | Veřejné, soukromé | ![Podporováno](media/green_check.png) | ![Nepodporováno](media/Red_X.png) | Import |
|Microsoft Store pro<br>Do zaměstnání | Jednu | Veřejný | ![Podporováno](media/green_check.png) | ![Nepodporováno](media/Red_X.png) | Importovat, vytvořit |

### <a name="about-azure-ad-apps"></a>O aplikacích Azure AD

Různé služby Azure vyžadují odlišné konfigurace, které provedete v Azure Portal. Kromě toho můžou aplikace pro každou službu vyžadovat samostatná oprávnění k prostředkům Azure.  

Pro více než jednu službu můžete použít jednu aplikaci. V Configuration Manager a Azure AD je k dispozici pouze jeden objekt ke správě. Po vypršení platnosti klíče zabezpečení v aplikaci stačí aktualizovat jenom jeden klíč.

Když vytvoříte další služby Azure v průvodci, Configuration Manager je navržený tak, aby znovu vytvářely informace, které jsou běžné mezi službami. Toto chování vám pomůže s nutností zadávat stejné informace více než jednou.

Další informace o požadovaných oprávněních a konfiguracích aplikace pro jednotlivé služby najdete v příslušném Configuration Manager článku v části [dostupné služby](#available-services).

Pokud chcete získat další informace o aplikacích Azure, začněte s následujícími články:

- [Ověřování a autorizace v prostředí Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Přehled Web Apps](/azure/app-service-web/app-service-web-overview)
- [Základy registrace aplikace v Azure AD](/azure/active-directory/develop/authentication-scenarios)  
- [Registrace aplikace ve vašem tenantovi Azure Active Directory](/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Než začnete

Po určení služby, ke které se chcete připojit, se podívejte na tabulku v [podrobnostech o službě](#service-details). Tato tabulka poskytuje informace, které potřebujete k dokončení průvodce službou Azure. Vaše diskuze vám poskytne správce Azure AD. Rozhodněte se, které z následujících akcí se mají provést:

- Ručně Vytvářejte aplikace předem ve Azure Portal. Pak importujte podrobnosti aplikace do Configuration Manager.  

- Použijte Configuration Manager k přímému vytváření aplikací v Azure AD. Pokud chcete shromažďovat potřebná data ze služby Azure AD, přečtěte si informace v dalších částech tohoto článku.  

Některé služby vyžadují, aby aplikace Azure AD měly určitá oprávnění. Zkontrolujte informace o každé službě a určete všechna požadovaná oprávnění. Například předtím, než budete moct importovat webovou aplikaci, musí ji správce Azure nejdřív vytvořit v [Azure Portal](https://portal.azure.com).

Při konfiguraci konektoru Log Analytics udělte nově zaregistrovaným oprávněním *přispěvatele* webové aplikace ve skupině prostředků, která obsahuje relevantní pracovní prostor. Toto oprávnění umožňuje Configuration Manager získat přístup k tomuto pracovnímu prostoru. Když přiřadíte oprávnění, vyhledejte název registrace aplikace v oblasti **Přidat uživatele** Azure Portal. Tento proces je stejný jako při [poskytování Configuration Manager s oprávněním Log Analytics](/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Správce Azure musí tato oprávnění přiřadit předtím, než aplikaci naimportujete do Configuration Manager.

## <a name="start-the-azure-services-wizard"></a>Spuštění Průvodce službami Azure

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** .  

2. Na kartě **Domů** na pásu karet ve skupině **služby Azure** vyberte **Konfigurovat služby Azure**.  

3. Na stránce **služby Azure** v Průvodci službami Azure:  

    1. Zadejte **název** objektu v Configuration Manager.  

    2. Zadejte volitelný **Popis** , který vám usnadní identifikaci služby.  

    3. Vyberte službu Azure, ke které se chcete připojit pomocí Configuration Manager.  

4. Výběrem možnosti **Další** přejděte na stránku [vlastností aplikace Azure](#azure-app-properties) Průvodce službami Azure.  

## <a name="azure-app-properties"></a>Vlastnosti aplikace Azure

Na stránce **aplikace** v Průvodci službami Azure nejdřív vyberte **prostředí Azure** ze seznamu. Informace o tom, které prostředí jsou aktuálně k dispozici službě, najdete v tabulce v [podrobnostech o službě](#service-details) .

Zbytek stránky aplikace se liší v závislosti na konkrétní službě. Podívejte se na tabulku v [podrobnostech o službě](#service-details) , pro kterou typ aplikace používá služba a kterou akci můžete použít.

- Pokud aplikace podporuje import i vytváření akcí, vyberte **Procházet**. Tato akce otevře [dialogové okno aplikace serveru](#server-app-dialog) nebo [dialog klientské aplikace](#client-app-dialog).  

- Pokud aplikace podporuje jenom akci importu, vyberte **importovat**. Tato akce otevře [dialogové okno Importovat aplikace (Server)](#import-apps-dialog-server) nebo [dialogové okno Importovat aplikace (klient)](#import-apps-dialog-client).

Po zadání aplikací na této stránce pokračujte kliknutím na tlačítko **Další** na stránce [Konfigurace nebo zjišťování](#configuration-or-discovery) Průvodce službami Azure.

### <a name="web-app"></a>Webová aplikace

Tato aplikace je *Webová aplikace nebo rozhraní API*typu Azure AD, označovanou také jako serverová aplikace v Configuration Manager.

#### <a name="server-app-dialog"></a>Dialog serverové aplikace

Když na stránce aplikace v Průvodci službami Azure vyberete **Vyhledat** **webovou aplikaci** , otevře se dialogové okno serverová aplikace. Zobrazuje seznam, který zobrazuje následující vlastnosti všech existujících webových aplikací:

- Popisný název tenanta
- Popisný název aplikace
- Typ služby

Existují tři akce, které můžete provést z dialogového okna serverová aplikace:

- Pokud chcete znovu použít stávající webovou aplikaci, vyberte ji ze seznamu.
- Výběrem **importovat** otevřete [dialogové okno Importovat aplikace](#import-apps-dialog-server).
- Výběrem **vytvořit** otevřete [dialogové okno vytvořit serverovou aplikaci](#create-server-application-dialog).

Po výběru, importu nebo vytvoření webové aplikace vyberte **OK** a zavřete tak dialogové okno aplikace serveru. Tato akce se vrátí na [stránku aplikace](#azure-app-properties) v Průvodci službami Azure.

#### <a name="import-apps-dialog-server"></a>Dialog importovat aplikace (Server)

Když v dialogovém okně aplikace serveru nebo na stránce aplikace v Průvodci službami Azure vyberete **importovat** , otevře se dialogové okno Importovat aplikace. Tato stránka umožňuje zadat informace o webové aplikaci Azure AD, která je už vytvořená v Azure Portal. Importuje metadata o této webové aplikaci do Configuration Manager. Zadejte následující informace:

- **Název tenanta Azure AD**: název vašeho TENANTA Azure AD.
- **ID tenanta Azure AD**: identifikátor GUID vašeho TENANTA Azure AD.
- **Název aplikace**: popisný název aplikace, zobrazovaný název v registraci aplikace.
- **ID klienta**: hodnota **ID aplikace (klienta)** pro registraci aplikace. Formát je standardní identifikátor GUID.
- **Tajný klíč**: při registraci aplikace ve službě Azure AD je nutné zkopírovat tajný klíč.
- **Vypršení platnosti tajného klíče**: vyberte budoucí datum z kalendáře.
- **Identifikátor URI ID aplikace**: Tato hodnota musí být v TENANTOVI Azure AD jedinečná. Je v přístupovém tokenu, který používá klient Configuration Manager k vyžádání přístupu ke službě. Hodnota je **identifikátor URI ID aplikace** položky registrace aplikace na portálu Azure AD. Formát je podobný `https://ConfigMgrService` .

Po zadání informací vyberte možnost **ověřit**. Pak kliknutím na **OK** zavřete dialogové okno Importovat aplikace. Tato akce se vrátí buď na [stránku aplikace](#azure-app-properties) v Průvodci službami Azure, nebo v [dialogu serverová aplikace](#server-app-dialog).

> [!TIP]
> Když zaregistrujete aplikaci ve službě Azure AD, možná budete muset ručně zadat následující **identifikátor URI pro přesměrování**: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>` . Zadejte identifikátor GUID ID klienta aplikace, například: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49` .<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Dialogové okno vytvořit serverovou aplikaci

Když v dialogovém okně Serverová aplikace vyberete **vytvořit** , otevře se dialogové okno vytvořit serverovou aplikaci. Tato stránka automatizuje vytvoření webové aplikace ve službě Azure AD. Zadejte následující informace:

- **Název aplikace**: popisný název aplikace.
- **Adresa URL domovské stránky**: Tato hodnota není používána Configuration Manager, ale vyžaduje ji služba Azure AD. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.  
- **Identifikátor URI ID aplikace**: Tato hodnota musí být v TENANTOVI Azure AD jedinečná. Je v přístupovém tokenu, který používá klient Configuration Manager k vyžádání přístupu ke službě. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.  
- **Období platnosti tajného klíče**: v rozevíracím seznamu vyberte buď **1 rok** , nebo **2 roky** . Výchozí hodnota je jeden rok.

Vyberte **Přihlásit** se a ověřte se v Azure jako uživatel s právy pro správu. Tyto přihlašovací údaje se Configuration Manager neukládají. Tento uživatel nevyžaduje oprávnění v Configuration Manager a nemusí být stejný účet, který spouští Průvodce službami Azure. Po úspěšném ověření v Azure stránka zobrazuje **název tenanta Azure AD** pro referenci.

Vyberte **OK** a vytvořte webovou aplikaci ve službě Azure AD a zavřete dialogové okno vytvořit serverovou aplikaci. Tato akce se vrátí do [dialogového okna aplikace serveru](#server-app-dialog).

> [!NOTE]
> Pokud máte definované zásady podmíněného přístupu Azure AD a platí pro **všechny cloudové aplikace** , musíte z této zásady vyloučit vytvořenou serverovou aplikaci. Další informace o tom, jak vyloučit konkrétní aplikace, najdete v [dokumentaci k podmíněnému přístupu ke službě Azure AD](/azure/active-directory/conditional-access/).

### <a name="native-client-app"></a>Nativní klientská aplikace

Tato aplikace je *nativní*typ Azure AD, který se taky označuje jako klientská aplikace v Configuration Manager.

#### <a name="client-app-dialog"></a>Dialog klientské aplikace

Když na stránce aplikace v Průvodci službami Azure vyberete **Vyhledat** **nativní klientskou aplikaci** , otevře se dialogové okno klientská aplikace. Zobrazuje seznam, který zobrazuje následující vlastnosti všech existujících nativních aplikací:

- Popisný název tenanta
- Popisný název aplikace
- Typ služby

Existují tři akce, které můžete provést z dialogového okna klientská aplikace:

- Pokud chcete znovu použít existující nativní aplikaci, vyberte ji ze seznamu. 
- Výběrem **importovat** otevřete [dialogové okno Importovat aplikace](#import-apps-dialog-client).
- Vyberte **vytvořit** a otevřete tak [dialogové okno vytvořit klientskou aplikaci](#create-client-application-dialog).

Když vyberete, naimportujete nebo vytvoříte nativní aplikaci, kliknutím na **OK** zavřete dialogové okno klientská aplikace. Tato akce se vrátí na [stránku aplikace](#azure-app-properties) v Průvodci službami Azure.

#### <a name="import-apps-dialog-client"></a>Dialog importovat aplikace (klient)

Když vyberete **importovat** z dialogu klientské aplikace, otevře se dialogové okno Importovat aplikace. Tato stránka umožňuje zadat informace o nativní aplikaci Azure AD, která je už vytvořená v Azure Portal. Importuje metadata o této nativní aplikaci do Configuration Manager. Zadejte následující informace:

- **Název aplikace**: popisný název aplikace.
- **ID klienta**: hodnota **ID aplikace (klienta)** pro registraci aplikace. Formát je standardní identifikátor GUID.

Po zadání informací vyberte možnost **ověřit**. Pak kliknutím na **OK** zavřete dialogové okno Importovat aplikace. Tato akce se vrátí do [dialogového okna klientské aplikace](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Dialog vytvořit klientskou aplikaci

Když v dialogovém okně klientská aplikace vyberete **vytvořit** , otevře se dialogové okno vytvořit klientskou aplikaci. Tato stránka automatizuje vytváření nativní aplikace v Azure AD. Zadejte následující informace:

- **Název aplikace**: popisný název aplikace.
- **Adresa URL odpovědi**: Tato hodnota není používána Configuration Manager, ale vyžaduje ji služba Azure AD. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.

Vyberte **Přihlásit** se a ověřte se v Azure jako uživatel s právy pro správu. Tyto přihlašovací údaje se Configuration Manager neukládají. Tento uživatel nevyžaduje oprávnění v Configuration Manager a nemusí být stejný účet, který spouští Průvodce službami Azure. Po úspěšném ověření v Azure stránka zobrazuje **název tenanta Azure AD** pro referenci.

Pokud chcete vytvořit nativní aplikaci ve službě Azure AD, vyberte **OK** a zavřete dialogové okno vytvořit klientskou aplikaci. Tato akce se vrátí do [dialogového okna klientské aplikace](#client-app-dialog).

## <a name="configuration-or-discovery"></a>Konfigurace nebo zjišťování

Po zadání webových a nativních aplikací na stránce aplikace Průvodce službami Azure pokračuje buď na stránku **Konfigurace** , nebo na stránce **zjišťování** , a to v závislosti na službě, ke které se připojujete. Podrobnosti o této stránce se liší od služby po službu. Další informace najdete v jednom z následujících článků:  

- **Cloudová služba pro správu** , stránka **zjišťování** : [Konfigurace zjišťování uživatelů Azure AD](configure-discovery-methods.md#azureaadisc)  

- Služba **konektoru Log Analytics** , **konfigurační** stránka: [Konfigurace připojení k Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- Služba **Microsoft Store for Business** – stránka **konfigurace** : [Konfigurace Microsoft Store synchronizace pro firmy](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Nakonec dokončete Průvodce službami Azure pomocí stránek souhrn, průběh a dokončení. Dokončili jste konfiguraci služby Azure v Configuration Manager. Zopakováním tohoto postupu nakonfigurujete další služby Azure.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> Obnovit tajný klíč

Tajný klíč aplikace Azure AD musíte obnovit před koncem období platnosti. Pokud zadáte vypršení platnosti klíče, Configuration Manager se nemůže ověřit ve službě Azure AD, což způsobí, že vaše připojené služby Azure přestanou fungovat.

Počínaje verzí 2006 konzola Configuration Manager zobrazuje oznámení v následujících situacích:<!--6386392-->

- Brzo vyprší platnost jednoho nebo více tajných klíčů aplikací Azure AD.
- Platnost jednoho nebo více tajných klíčů aplikace Azure AD vypršela.

Pokud chcete oba případy zmírnit, obnovte tajný klíč.

Další informace o tom, jak s těmito oznámeními pracovat, najdete v tématu [Configuration Manager oznámení konzoly](../../manage/admin-console-notifications.md).

### <a name="renew-key-for-created-app"></a>Obnovit klíč pro vytvořenou aplikaci

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Azure Active Directory klienty** .

1. V podokně podrobností vyberte pro aplikaci tenanta Azure AD.

1. Na pásu karet vyberte **obnovit tajný klíč**. Zadejte přihlašovací údaje vlastníka aplikace nebo správce Azure AD.

### <a name="renew-key-for-imported-app"></a>Obnovit klíč pro importovanou aplikaci

Pokud jste importovali aplikaci Azure v Configuration Manager, obnovte ji pomocí Azure Portal. Všimněte si nového tajného klíče a data vypršení platnosti. Tyto informace přidejte v průvodci **obnovení tajného klíče** .  

> [!NOTE]
> Před zavřením stránky **klíče** vlastností aplikace Azure uložte tajný klíč. Tyto informace se po zavření stránky odeberou.

## <a name="view-the-configuration-of-an-azure-service"></a>Zobrazení konfigurace služby Azure

Zobrazení vlastností služby Azure, kterou jste nakonfigurovali pro použití. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte možnost **služby Azure**. Vyberte službu, kterou chcete zobrazit nebo upravit, a pak vyberte **vlastnosti**.

Pokud vyberete službu a na pásu karet kliknete na **Odstranit** , tato akce odstraní připojení v Configuration Manager. Neodebere aplikaci v Azure AD. Požádejte správce Azure, aby aplikaci odstranil, když už není potřeba. Nebo spusťte Průvodce služby Azure a importujte aplikaci.<!--483440-->

## <a name="cloud-management-data-flow"></a>Tok dat správy cloudu

Následující diagram je koncepční tok dat pro interakci mezi Configuration Manager, službou Azure AD a propojenými Cloud Services. Tento konkrétní příklad používá službu **Cloud Management** , která zahrnuje klienta Windows 10 a server i klientské aplikace. Toky pro další služby jsou podobné.

![Diagram toku dat pro Configuration Manager s využitím Azure AD a správy cloudu](media/aad-auth.png)

1. Správce Configuration Manager importuje nebo vytváří klientské a serverové aplikace ve službě Azure AD.  

2. Configuration Manager spustí se metoda zjišťování uživatelů Azure AD. Lokalita používá token aplikace serveru Azure AD k dotazování Microsoft Graph pro objekty uživatele.  

3. Web ukládá data o objektech uživatele. Další informace najdete v tématu [zjišťování uživatelů Azure AD](about-discovery-methods.md#azureaddisc).  

4. Klient Configuration Manager požaduje token uživatele Azure AD. Klient vytvoří deklaraci identity pomocí ID aplikace klientské aplikace Azure AD a serverovou aplikaci jako cílovou skupinu. Další informace najdete v tématu [deklarace identity v tokenech zabezpečení Azure AD](/azure/active-directory/develop/authentication-scenarios#security-tokens).  

5. Klient se ověřuje s webem tím, že prezentuje token Azure AD pro bránu pro správu cloudu a místní bod správy s povoleným protokolem HTTPS.  

Podrobnější informace najdete v tématu [pracovní postup ověřování Azure AD](../../../clients/manage/azure-ccmsetup.md).