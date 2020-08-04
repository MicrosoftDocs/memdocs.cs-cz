---
title: Možnosti ve verzi Technical Preview 1703
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1703.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 98a82d118442a7ca37ff7b2df62bf4702c15ba2c
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526011"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1703 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1703. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Nasazení hromadně zakoupených aplikací pro iOS do kolekcí zařízení

Můžete teď nasadit licencované aplikace do zařízení i pro uživatele. V závislosti na možnosti aplikace podporovat licencování zařízení bude při nasazování k vhodné licence, a to následujícím způsobem:

| Verze Configuration Manager | Aplikace podporuje licencování zařízení? | Typ kolekce nasazení | Deklarovaná licence |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|Starší než 1702|Yes|Uživatel|Uživatelská licence|
|Starší než 1702|No|Uživatel|Uživatelská licence|
|Starší než 1702|Yes|Zařízení|Uživatelská licence|
|Starší než 1702|No|Zařízení|Uživatelská licence|
|1702 a novější|Yes|Uživatel|Uživatelská licence|
|1702 a novější|No|Uživatel|Uživatelská licence|
|1702 a novější|Yes|Zařízení|Licence zařízení|
|1702 a novější|No|Zařízení|Uživatelská licence|


## <a name="direct-links-to-applications-in-software-center"></a>Přímé odkazy na aplikace v centru softwaru

Koncovým uživatelům teď můžete poskytnout přímý odkaz na aplikaci v centru softwaru. To znamená, že už nebudou muset otevírat Centrum softwaru a hledat aplikaci dřív, než ji budou moct nainstalovat. To je dostupné jenom pro Configuration Manager aplikace, ne balíčky a programy nebo sekvence úloh.

### <a name="try-it-out"></a>Vyzkoušet                 

Pomocí následujícího formátu adresy URL otevřete Centrum softwaru pro konkrétní aplikaci:

**Softwarecenter: SoftwareId =_identifikátor aplikace_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Jak získat identifikátor aplikace v aplikaci.

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.
2. V pracovním prostoru Softwarová knihovna rozbalte **Správa aplikací** a pak klikněte na **Aplikace**.
3. V zobrazení **aplikace** klikněte pravým tlačítkem na jedno ze záhlaví sloupců a potom v seznamu vyberte **jedinečné ID CI**. Uvidíte, že v seznamu se teď zobrazuje jedinečné ID každé aplikace.
4. Všimněte si **jedinečného ID CI** aplikace, ke které chcete poskytnout odkaz, například: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5. Pak v tomto případě odeberte libovolný text, který následuje za identifikátorem GUID aplikace, v tomto případě **/2**. Tím se vám ponechá identifikátor aplikace.
6. Nakonec, pokud chcete dokončit sestavování odkazu, před něj uveďte **Softwarecenter: SoftwareID =**. Pomocí výše uvedeného příkladu se poslední odkaz načte: **Softwarecenter: SoftwareId = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Pomocí tohoto odkazu můžou koncoví uživatelé otevřít Centrum softwaru přímo do vámi zadané aplikace.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certifikáty PFX pro Configuration Manager klientských počítačích se systémem Windows

Nyní můžete nasadit profily certifikátů PFX, které jste importovali, do Configuration Manager klientských počítačů se systémem Windows 10.

### <a name="try-it-out"></a>Vyzkoušet

Pomocí pokynů v tématu [Vytvoření profilů certifikátů PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md) IMPORTUJTE profil PFX, nasaďte profil a potom zkontrolujte, jestli byl certifikát nainstalovaný pro cílového uživatele.



## <a name="configure-azure-services-wizard"></a>Průvodce konfigurací služeb Azure
Technical Preview 1703 zavádí průvodce **konfigurací služeb Azure** . Tento průvodce poskytuje společné prostředí pro konfiguraci, které nahrazuje jednotlivé pracovní postupy pro nastavení cloudových služeb, které používáte s Configuration Manager. K tomu je potřeba použít **webovou aplikaci Azure** , která poskytuje údaje o předplatném a konfiguraci, které jinak zadáte při vytváření nové komponenty Configuration Manager nebo služby pomocí Azure.

V Technical Preview 1703 se pomocí tohoto průvodce nakonfiguruje jenom Windows Store pro firmy (WSfB).  Jiné cloudové služby se konfigurují pomocí samostatných pracovních postupů.

- Pomocí informací v tomto tématu v této verzi Preview nahraďte konfigurační kroky, které najdete v části [Nastavení synchronizace s Windows Storem pro firmy](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) v Current Branch tématu [Správa aplikací z Windows Storu pro firmy pomocí Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

- Další informace o webových aplikacích najdete v tématech [ověřování a autorizace v Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)a [Web Apps přehled](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Předpoklady a plánování
Když nakonfigurujete připojení mezi Configuration Manager a Windows Storem pro firmy, musíte zadat složku, do které se bude uchovávat obsah aplikace synchronizovaný ze Storu. Chcete-li zajistit, aby byla tato složka zabezpečená a aby její obsah bylo možné nasadit do zařízení, zajistěte, aby byla zajištěna následující oprávnění:
- Počítač, na který nainstalujete roli systému lokality spojovacího bodu služby (lokalita nejvyšší úrovně v hierarchii), musí mít oprávnění ke čtení a zápisu do složky, kterou jste zadali při použití účtu **počítač $** .  

- Autor aplikace musí mít oprávnění ke čtení zadané složky.  

- Účet **počítače $** každého počítače, který je hostitelem instance poskytovatele serveru SMS, musí být schopný použít složku, kterou jste zadali.

V Azure Active Directory Zaregistrujte Configuration Manager jako webovou aplikaci nebo nástroj pro správu webového rozhraní API. Tím se vytvoří ID klienta, které budete potřebovat později.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Použití Průvodce ke konfiguraci cloudové služby WSfB

1. V konzole nástroje klikněte na **Správa**  >  **Přehled**  >  **Cloud Services Správa**  >  **Azure**  >  **Azure**a pak zvolte **Konfigurovat služby Azure** pro spuštění **Průvodce službami Azure**.

2. Na stránce **služby Azure** vyberte službu, kterou chcete nakonfigurovat, a potom klikněte na **Další**. V této verzi Preview se dá nakonfigurovat jenom WSfB.

3. Na stránce **Obecné** zadejte popisný název **služby Azure** a případně i její popis a pak klikněte na **Další**.

4. Na stránce **aplikace** určete prostředí Azure a kliknutím na tlačítko **Procházet** otevřete okno aplikace serveru.

5. V okně **aplikace serveru** vyberte serverovou aplikaci, kterou chcete použít, a potom klikněte na **OK**.
   Serverové aplikace jsou webové aplikace Azure, které obsahují konfigurace pro váš účet Azure, včetně ID tenanta, ID klienta a tajného klíče pro klienty. Pokud nemáte k dispozici serverovou aplikaci, použijte jednu z následujících možností:
   - **Vytvořit**: Pokud chcete vytvořit novou serverovou aplikaci, klikněte na **vytvořit**. Zadejte popisný název aplikace a tenanta. Až se pak přihlásíte k Azure, Configuration Manager pro vás vytvořit webovou aplikaci v Azure, včetně ID klienta a tajného klíče pro použití s webovou aplikací. Později je můžete zobrazit z Azure Portal.
   - **Importovat**: Pokud chcete používat webovou aplikaci, která už ve vašem předplatném Azure existuje, klikněte na **importovat**. Zadejte popisný název aplikace a tenanta a pak zadejte ID tenanta, ID klienta a tajný klíč pro webovou aplikaci Azure, kterou chcete použít Configuration Manager. Po **ověření** informací pokračujte kliknutím na tlačítko **OK** .  </br></br>

6. Projděte si **informační** stránku a proveďte všechny další kroky a konfigurace jako směrované. Tyto konfigurace jsou nezbytné k používání služby s Configuration Manager.
   Pokud například chcete nakonfigurovat WSfB:

   1. V Azure je nutné zaregistrovat Configuration Manager jako webovou aplikaci nebo webové rozhraní API a zaznamenat ID klienta. Také zadáte klientský klíč pro použití nástrojem pro správu (což je Configuration Manager).

   2.    V konzole WSfB musíte nakonfigurovat Configuration Manager jako nástroj pro správu úložiště, povolit podporu pro offline licencované aplikace a pak koupit aspoň jednu aplikaci.   </br>

   Až budete připraveni pokračovat, klikněte na **Další** .

7. Na stránce **Konfigurace aplikace** dokončete katalog aplikací a jazykové konfigurace pro tuto službu a potom klikněte na tlačítko **Další**.
8. Po dokončení průvodce Configuration Manager konzola zobrazí, že jste nakonfigurovali **Windows Store pro firmy** jako **typ cloudové služby**.

Teď můžete použít zbývající část [obsahu Current Branch](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) pro správu aplikací z WSfB k synchronizaci, vytváření a nasazování a monitorování aplikací pro Windows Store pro firmy.

### <a name="modify-a-cloud-service-configuration"></a>Úprava konfigurace cloudové služby
Můžete zobrazit a upravit vlastnosti cloudové služby a upravit tak konfiguraci.

V konzole nástroje přejdete **na**  >  **Přehled**správy  >  **Cloud Services**služby Azure Azure  >  **Azure**  >  **Services**a pak zvolte **Konfigurovat služby Azure**, vyberte cloudovou službu a pak zvolte **vlastnosti**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Převod ze systému BIOS na rozhraní UEFI během místního upgradu
Windows 10 Creators Update zavádí jednoduchý nástroj pro převod, který automatizuje proces opětovného rozdělení pevného disku na hardware s podporou rozhraní UEFI a integruje Nástroj pro převod do místního procesu upgradu Windows 7 na Windows 10. Pokud tento nástroj zkombinujete s pořadím úkolů upgradu operačního systému a nástrojem OEM, který převede firmware ze systému BIOS na rozhraní UEFI, můžete počítače převést na systém BIOS na rozhraní UEFI v rámci místního upgradu na aktualizaci Windows 10 Creators Update. Podrobnosti najdete v tématu věnovaném [krokům pořadí úkolů ke správě převodu systému BIOS na rozhraní UEFI](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

## <a name="collapsible-task-sequence-groups"></a>Sbalitelné skupiny pořadí úloh
Tato verze přináší možnost Rozbalit a sbalit skupiny pořadí úloh. Můžete rozbalit nebo sbalit jednotlivé skupiny nebo rozbalit nebo sbalit všechny skupiny najednou.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Nastavení klienta pro konfiguraci služby Windows Analytics pro Upgrade Readiness
Od této verze můžete pomocí nastavení klienta zařízení zjednodušit konfiguraci diagnostických dat Windows, která jsou nutná k použití řešení Windows Analytics, jako je Upgrade Readiness s Configuration Manager. Configuration Manager můžou načítat data ze služby Windows Analytics, která může poskytnout cenné přehledy o aktuálním stavu prostředí na základě diagnostických dat Windows hlášených klientskými počítači. Diagnostické údaje systému Windows jsou hlášeny klientskými počítači do diagnostické služby systému Windows. příslušná data jsou následně přenesena do řešení Windows Analytics, která jsou hostována v jednom z pracovních prostorů vaší organizace v OMS. Upgrade Readiness je řešení Windows Analytics, které vám může přispět k určení priorit rozhodování o upgradech Windows pro spravovaná zařízení.

### <a name="prerequisites"></a>Požadavky
- Lokalita musí být nakonfigurovaná tak, aby používala cloudovou službu Upgrade Readiness.

### <a name="configure-windows-analytics-client-settings"></a>Konfigurace nastavení klienta Windows Analytics
Pokud chcete nakonfigurovat Windows Analytics, v konzole Configuration Manager přejděte na **Správa**  >  **nastavení klienta**, dvakrát klikněte na **vytvořit vlastní nastavení klienta zařízení** a pak zkontrolujte **Windows Analytics**.  

Pak po přechodu na kartu nastavení **Windows Analytics** proveďte následující konfiguraci:
- **Komerční ID**  
Klíč komerčního ID mapuje informace ze zařízení, která spravujete do pracovního prostoru OMS, který hostuje data Windows Analytics vaší organizace. Pokud jste už nakonfigurovali komerční klíč ID pro použití s Upgrade Readiness, použijte toto ID. Pokud ještě nemáte klíč komerčního ID, vygenerujte svůj klíč komerčního ID.

- Nastavení **úrovně diagnostických dat pro zařízení s Windows 10**

- Volba **výslovného souhlasu se shromažďováním komerčních dat v zařízeních se systémem Windows 7, 8 a 8,1**   

- **Konfigurace shromažďování dat pro Internet prozkoumat** V zařízeních se systémem Windows 8.1 nebo starším může shromažďování dat aplikace Internet Explorer umožňovat Upgrade Readiness zjišťování nekompatibility webových aplikací, které by mohly bránit hladkému upgradu na Windows 10. Shromažďování dat aplikace Internet Explorer lze povolit pro každou zónu Internetu.
