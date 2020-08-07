---
title: Správa Edge pro iOS a Android pomocí Intune
titleSuffix: ''
description: Použijte zásady ochrany aplikací a konfigurace Intune s Edgem pro iOS a Android a zajistěte, aby se k podnikovým webům vždycky používala ochrana na pracovišti.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49d731ef6e9508367ded8ed5d711b744be7d2db1
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912552"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Správa webového přístupu pomocí Edge pro iOS a Android s využitím Microsoft Intune

Hraniční podpora pro iOS a Android je navržená tak, aby uživatelům umožnila procházení webu a podporuje více identit. Uživatelé můžou přidat pracovní účet i osobní účet pro procházení. Mezi těmito dvěma identitami se dokončí oddělení, které je podobné tomu, co se nabízí v jiných mobilních aplikacích Microsoftu.

Hraniční podpora pro iOS je podporovaná v iOS 12,0 a novějších. Na Androidu 5 a novějším se podporuje Edge pro Android.

> [!NOTE]
> Edge pro iOS a Android nespotřebovává nastavení, která uživatelé nastavili pro nativní prohlížeč na svých zařízeních, protože Edge pro iOS a Android nemá k těmto nastavením přístup.

V případě, že se přihlásíte k odběru Enterprise Mobility + Security sady, která zahrnuje Microsoft Intune a Azure Active Directory Premium funkce, jako je například podmíněný přístup, jsou k dispozici bohatší a nejširší funkce ochrany pro data Office 365. Přinejmenším budete chtít nasadit zásadu podmíněného přístupu, která umožňuje připojení pouze k hraničním prostředkům pro iOS a Android z mobilních zařízení a zásad ochrany aplikací Intune, které zajistí ochranu prostředí pro procházení.

> [!NOTE]
> Nové webové klipy (připnuté webové aplikace) na zařízeních se systémem iOS se otevřou v Edge pro iOS a Android místo Intune Managed Browser, pokud je to potřeba pro otevření v chráněném prohlížeči. U starších webových klipů pro iOS je nutné tyto webové klipy znovu zaměřit, aby se místo Managed Browser otevíraly v hraničních zařízeních pro iOS a Android.

## <a name="apply-conditional-access"></a>Použití podmíněného přístupu
Organizace můžou pomocí zásad podmíněného přístupu Azure AD zajistit, aby uživatelé měli přístup k pracovnímu nebo školnímu obsahu jenom pomocí Edge pro iOS a Android. K tomu budete potřebovat zásadu podmíněného přístupu, která cílí na všechny potenciální uživatele. Podrobnosti o vytvoření této zásady najdete v v [vyžadovat zásady ochrany aplikací pro cloudovou aplikaci přístup s podmíněným přístupem](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Postupujte podle [scénáře 2: aplikace prohlížeče vyžadují schválené aplikace se zásadami ochrany aplikací](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies), které umožňují hraniční instalaci pro iOS a Android, ale blokuje další webové prohlížeče mobilních zařízení z připojení k koncovým bodům Office 365.

   >[!NOTE]
   > Tato zásada zajišťuje, že mobilní uživatelé mají přístup ke všem koncovým bodům Office 365 z hraničního prostředí pro iOS a Android. Tato zásada taky zabrání uživatelům v používání služby InPrivate pro přístup k koncovým bodům Office 365.

Pomocí podmíněného přístupu můžete taky cílit na místní weby, které jste nastavili externím uživatelům prostřednictvím [Azure proxy aplikací služby AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="create-intune-app-protection-policies"></a>Vytvoření zásad ochrany aplikací Intune

Zásady ochrany aplikací (aplikace) definují, které aplikace jsou povoleny, a akce, které mohou provádět s daty vaší organizace. Volby dostupné v aplikaci umožňují organizacím přizpůsobit ochranu na jejich konkrétní potřeby. V některých případech nemusí být zřejmé, která nastavení zásad jsou nutná k implementaci kompletního scénáře. Microsoft zavedl taxonomii pro své rozhraní ochrany dat aplikací pro správu mobilních aplikací v iOS a Androidu, aby organizacím pomohly určit prioritu posílení koncových bodů mobilních klientů.

Architektura aplikace Data Protection je rozdělená na tři různé úrovně konfigurace, přičemž každá úroveň se sestavuje na předchozí úrovni:

- **Ochrana podnikových dat** na úrovni Basic (úroveň 1) zajišťuje, aby byly aplikace chráněny pomocí kódu PIN a zašifrované a prováděly operace selektivního vymazání. U zařízení s Androidem Tato úroveň ověřuje ověření zařízení s Androidem. Toto je konfigurace na úrovni vstupu, která poskytuje podobné řízení ochrany dat v zásadách poštovní schránky Exchange Online a zavádí uživatele a naplňování do aplikace.
- **Enterprise Enhanced Data Protection** (úroveň 2) zavádí mechanismy prevence úniku dat aplikace a minimální požadavky na operační systém. Jedná se o konfiguraci, která platí pro většinu mobilních uživatelů, kteří přistupují k pracovním nebo školním datům.
- **Podniková ochrana dat** (úroveň 3) zavádí pokročilé mechanismy ochrany dat, rozšířenou konfiguraci kódu PIN a ochranu před mobilními hrozbami aplikace. Tato konfigurace je žádoucí pro uživatele, kteří mají přístup k datům s vysokým rizikem.

Pokud chcete zobrazit konkrétní doporučení pro jednotlivé úrovně konfigurace a minimální aplikace, které musí být chráněné, přečtěte si téma [Ochrana dat pomocí zásad ochrany aplikací](app-protection-framework.md).

Bez ohledu na to, jestli je zařízení zaregistrované v řešení UEM (Unified Endpoint Management), je potřeba vytvořit zásady ochrany aplikací Intune pro aplikace pro iOS i Android, a to pomocí kroků v tématu [jak vytvořit a přiřadit zásady ochrany aplikací](app-protection-policies.md). Tyto zásady musí splňovat minimálně tyto podmínky:

1. Zahrnují všechny Microsoft 365 mobilní aplikace, jako je například Edge, Outlook, OneDrive, Office nebo týmy. tím zajistíte, že uživatelé budou mít zabezpečený přístup k pracovním nebo školním datům v rámci libovolné aplikace Microsoftu.

2. Jsou přiřazeny všem uživatelům. Tím se zajistí, že všichni uživatelé budou chráněni bez ohledu na to, jestli používají Edge pro iOS nebo Android.

3. Určete, která úroveň rozhraní splňuje vaše požadavky. Většina organizací by měla implementovat nastavení definovaná v **Enterprise Enhanced Data Protection** (Level 2), protože umožňuje řízení požadavků na ochranu a přístup k datům.

Další informace o dostupných nastaveních najdete v tématu nastavení [zásad ochrany aplikací pro Android](app-protection-policy-settings-android.md) a [nastavení zásad ochrany aplikací pro iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Aby bylo možné použít zásady ochrany aplikací Intune proti aplikacím na zařízeních s Androidem, které nejsou zaregistrované v Intune, musí uživatel nainstalovat taky Portál společnosti Intune. Další informace najdete v tématu [co očekávat, když je vaše aplikace pro Android spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-android.md).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Jednotné přihlašování k webovým aplikacím připojeným k Azure AD v prohlížečích chráněných zásadami

Edge pro iOS a Android může využít jednotné přihlašování (SSO) ke všem webovým aplikacím (SaaS a místním), které jsou připojené ke službě Azure AD. Jednotné přihlašování umožňuje uživatelům přístup k webovým aplikacím připojeným k Azure AD prostřednictvím Edge pro iOS a Android, aniž by museli znovu zadávat svoje přihlašovací údaje.

Jednotné přihlašování vyžaduje, aby zařízení bylo zaregistrované v aplikaci Microsoft Authenticator pro zařízení s iOS nebo Portál společnosti Intune na Androidu. Když je uživatel z nich, zobrazí se výzva k registraci svého zařízení, když přejde do webové aplikace připojené k Azure AD v prohlížeči chráněném zásadami (to platí jenom v případě, že zařízení ještě není zaregistrované). Po registraci zařízení u účtu uživatele spravovaného službou Intune má tento účet povolený jednotné přihlašování pro webové aplikace připojené k Azure AD.

> [!NOTE]
> Registrace zařízení představuje jednoduché vrácení se změnami pomocí služby Azure AD. Nevyžaduje úplný zápis zařízení a neposkytuje mu žádná další oprávnění k tomuto zařízení.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Využití konfigurace aplikace ke správě možností procházení

Edge pro iOS a Android podporuje nastavení aplikace, která umožňují sjednocenou správu koncových bodů, jako je Microsoft Endpoint Manager, což správcům umožňuje přizpůsobit chování aplikace.

Konfigurace aplikace se dá doručit buď prostřednictvím kanálu operačního systému správy mobilních zařízení (MDM) v zaregistrovaných zařízeních ([Konfigurace kanálu konfigurace spravovaných aplikací](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) pro iOS nebo [Android v podnikovém](https://developer.android.com/work/managed-configurations) kanálu pro Android), nebo přes kanál Intune App Protection Policy (App). Edge pro iOS a Android podporuje následující scénáře konfigurace:

- Povolí jenom pracovní nebo školní účty.
- Obecná nastavení konfigurace aplikace
- Nastavení pro ochranu dat

> [!IMPORTANT]
> V případě scénářů konfigurace, které vyžadují registraci zařízení v Androidu, musí být zařízení zaregistrovaná v Androidu Enterprise a Edge pro Android se musí nasadit prostřednictvím spravovaného Google Play Storu. Další informace najdete v tématech [Nastavení registrace zařízení s pracovním profilem Android Enterprise](../enrollment/android-work-profile-enroll.md) a [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](app-configuration-policies-use-android.md).

Každý scénář konfigurace zvýrazní konkrétní požadavky. Například jestli scénář konfigurace vyžaduje registraci zařízení, takže funguje s jakýmkoli poskytovatelem UEM nebo vyžaduje zásady Intune App Protection.

> [!NOTE]
> Pomocí Microsoft Endpoint Manageru se konfigurace aplikací dodaná prostřednictvím kanálu MDM operačního systému označuje jako zásady konfigurace aplikací **spravovaných zařízení** (ACP). Konfigurace aplikace dodaná prostřednictvím kanálu zásad ochrany aplikací se označuje jako zásada konfigurace aplikace **spravované aplikace** .

## <a name="only-allow-work-or-school-accounts"></a>Povolí jenom pracovní nebo školní účty.

Dodržování zásad zabezpečení a dodržování předpisů u našich největších a vysoce regulovaných zákazníků je klíčovým pilířem Microsoft 365 hodnoty. Některé společnosti mají požadavek na zachycení všech komunikačních informací v rámci svého podnikového prostředí, a to i v případě, že se zařízení používají jenom pro firemní komunikaci. Pro podporu těchto požadavků je možné nakonfigurovat Edge pro iOS a Android na registrovaných zařízeních tak, aby povolovala zřízení jednoho podnikového účtu v rámci aplikace.

Další informace o konfiguraci nastavení režimu pro povolení účtů organizace najdete tady:

- [Nastavení Androidu](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [nastavení iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Tento scénář konfigurace funguje jenom se zaregistrovanými zařízeními. Nicméně jakýkoli poskytovatel UEM je podporován. Pokud nepoužíváte Microsoft Endpoint Manager, budete se muset obrátit na dokumentaci k UEM, jak tyto konfigurační klíče nasadit.

## <a name="general-app-configuration-scenarios"></a>Obecné scénáře konfigurace aplikací

Edge pro iOS a Android nabízí správcům možnost přizpůsobení výchozí konfigurace pro několik nastavení v aplikaci. Tato možnost se v současné době nabízí jenom v případě, že Edge pro iOS a Android má Intune App Protection zásady použité pro pracovní nebo školní účet, který je přihlášený k aplikaci, a nastavení zásad se doručují prostřednictvím zásad konfigurace aplikací spravovaných aplikací.

> [!IMPORTANT]
> Edge pro Android nepodporuje nastavení Chromu, která jsou k dispozici ve spravovaných Google Play.

Edge podporuje následující nastavení konfigurace:

- Nové prostředí na stránce karty
- Prostředí záložky
- Prostředí chování aplikace
- Prostředí celoobrazovkového režimu

Tato nastavení se dají nasadit do aplikace bez ohledu na stav registrace zařízení.

### <a name="new-tab-page-experiences"></a>Nové prostředí na stránce karty

Edge pro iOS a Android nabízí organizacím několik možností pro úpravu nového prostředí na stránce karet.

#### <a name="organization-logo-and-brand-color"></a>Logo organizace a barva značky

Tato nastavení umožňují přizpůsobit novou stránku karty na hranici pro iOS a Android, která zobrazuje logo vaší organizace a barvu značky jako pozadí stránky.

Pokud chcete nahrát logo a barvu vaší organizace, nejdřív proveďte následující kroky:
1. V rámci služby [Microsoft Endpoint Manager](https://endpoint.microsoft.com)přejděte do části **Správa tenanta**  ->  **vlastní nastavení**  ->  **brandingu identitu společnosti**.
2. Pokud chcete nastavit logo značky, klikněte vedle **Zobrazit v záhlaví**na možnost pouze logo organizace. Doporučují se průhledné loga na pozadí.
3. Pokud chcete nastavit barvu pozadí vaší značky, vyberte **barvu motivu**. Edge pro iOS a Android používá světlejší barevný stín na nové stránce karty, což zajistí vysokou čitelnost stránky.

V dalším kroku využijte následující páry klíč/hodnota k získání brandingu vaší organizace na Edge pro iOS a Android:

|    Klíč    |    Hodnota    |
|--------------------------------------------------------------------|------------|
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. BrandLogo    |    **hodnota true** zobrazuje logo značky organizace.<br>**false** (výchozí) nebude zobrazovat logo.    |
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. BrandColor    |    **true** zobrazuje barvu značky organizace.<br>**false** (výchozí) nebude zobrazovat barvu.    |

#### <a name="homepage-shortcut"></a>Zástupce domovské stránky

Toto nastavení umožňuje nakonfigurovat zástupce domovské stránky pro zařízení s iOS a Androidem. Zástupce domovské stránky, který nakonfigurujete, se zobrazí jako první ikona pod panelem hledání, když uživatel otevře novou kartu na okrajích pro iOS a Android. Uživatel nemůže tohoto zástupce v spravovaném kontextu upravit ani odstranit. Zástupce domovské stránky zobrazuje název vaší organizace a rozlišuje ho. 

|    Klíč    |    Hodnota    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Zadejte platnou adresu URL. Nesprávné adresy URL se z bezpečnostních důvodů blokují.<br>Příklad: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Více zástupců nejoblíbenějších webů

Podobně jako u konfigurace zástupce domovské stránky můžete pro iOS a Android nakonfigurovat několik hlavních zástupců webů na nových stránkách karet. Uživatel nemůže tyto klávesové zkratky ve spravovaném kontextu upravit ani odstranit. Poznámka: můžete nakonfigurovat celkem 8 klávesových zkratek, včetně zástupce domovské stránky. Pokud jste nakonfigurovali zástupce domovské stránky, přepíše se první nejvyšší nakonfigurovaná lokalita. 

|    Klíč    |    Hodnota    |
|-------------------------------------------------------------------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. managedTopSites   |    Zadejte sadu hodnot URL. Každý hlavní zástupce webu se skládá z názvu a adresy URL. Název a adresu URL oddělte `|` znakem.<br>Příklad: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Novinky v oboru

V rámci hraničních nastavení pro iOS a Android můžete nakonfigurovat nové možnosti stránkování, které budou zobrazovat zprávy v oboru, které jsou relevantní pro vaši organizaci. Když tuto funkci povolíte, Edge pro iOS a Android používá název domény vaší organizace k agregaci zpráv z webu o vaší organizaci, oboru organizace a konkurenci, takže vaši uživatelé budou moct najít relevantní externí novinky z centralizované stránky nové karty v rámci hraničních zařízení pro iOS a Android. Novinky v oboru jsou ve výchozím nastavení vypnuté. 

|    Klíč    |    Hodnota    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. IndustryNews    |    **hodnota true** zobrazí novinky v odvětví na nové stránce karty.<br>**false** (výchozí) skryje v oboru zprávy na nové kartě.    |

### <a name="bookmark-experiences"></a>Prostředí záložky

Edge pro iOS a Android nabízí organizacím několik možností pro správu záložek.

#### <a name="managed-bookmarks"></a>Spravované záložky

Pro usnadnění přístupu můžete nakonfigurovat záložky, které chcete, aby uživatelé měli k dispozici, když používají Edge pro iOS a Android.

- Záložky se zobrazí jenom v pracovním nebo školním účtu a nezveřejňují se pro osobní účty.
- Záložky nelze odstranit ani upravit pomocí uživatelů.
- Záložky se zobrazí v horní části seznamu. Všechny záložky, které vytvářejí uživatelé, se zobrazí pod těmito záložkami.
- Pokud jste povolili přesměrování proxy aplikací, můžete přidat webové aplikace proxy aplikací pomocí své interní nebo externí adresy URL.
- Při zadávání adres URL do seznamu se ujistěte, že jste zadali předponu všechny adresy URL pomocí **http://** nebo **https://** .
- Záložky se vytvoří ve složce s názvem za názvem organizace, který je definovaný v Azure Active Directory.

|    Klíč    |    Hodnota    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    Hodnota této konfigurace je seznam záložek. Každá záložka se skládá z názvu záložky a adresy URL záložky. Název a adresu URL oddělte `|` znakem.<br> Příklad: `Microsoft Bing|https://www.bing.com`<p>Chcete-li nakonfigurovat více záložek, oddělte každou dvojici dvojitým znakem `||` .<br>Příklad:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Záložka moje aplikace

Ve výchozím nastavení mají uživatelé záložku Moje aplikace nakonfigurovanou v rámci složky organizace uvnitř Edge pro iOS a Android.

|    Klíč    |    Hodnota    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. MyApps    |    **true** (výchozí) zobrazí moje aplikace na okraji pro záložky s iOS a Androidem.<br>**false** skryje moje aplikace v rámci Edge pro iOS a Android.    |

### <a name="app-behavior-experiences"></a>Prostředí chování aplikace

Edge pro iOS a Android nabízí organizacím několik možností pro správu chování aplikace.

#### <a name="default-protocol-handler"></a>Výchozí obslužná rutina protokolu

Ve výchozím nastavení používá Edge pro iOS a Android popisovač protokolu HTTPS, když uživatel nezadá protokol v adrese URL. Obecně platí, že se jedná o osvědčený postup, ale je možné ho zakázat.

|    Klíč    |    Hodnota    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. defaultHTTPS     |     **true** (výchozí) popisovač výchozí hodnoty protokolu https<br>**false** , výchozí obslužná rutina protokolu je http     |

#### <a name="disable-data-sharing-for-personalization"></a>Zakázat sdílení dat pro přizpůsobení

Ve výchozím nastavení se na hraničních zařízeních pro iOS a Android zobrazuje výzva uživatelům pro shromažďování dat o využití a sdílení historie procházení a přizpůsobení jejich možností procházení. Organizace můžou toto sdílení dat zakázat tím, že zabrání zobrazení této výzvy koncovým uživatelům.

|    Klíč    |    Hodnota    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. disableShareUsageData    |     **hodnota true** zakáže zobrazení této výzvy koncovým uživatelům.<br>**false** (výchozí) uživatelům se zobrazí výzva ke sdílení dat o využití.    |
|     com. Microsoft. Intune. mam. managedbrowser. disableShareBrowsingHistory    |     **hodnota true** zakáže zobrazení této výzvy koncovým uživatelům.<br>**false** (výchozí) uživatelům se zobrazí výzva ke sdílení historie procházení.     |

#### <a name="disable-specific-features"></a>Zakázat konkrétní funkce

Edge pro iOS a Android umožňuje organizacím zakázat některé funkce, které jsou ve výchozím nastavení povolené. Pokud chcete tyto funkce zakázat, nakonfigurujte následující nastavení:

|    Klíč    |    Hodnota    |
|-----------------------|-----------------------|
|    com. Microsoft. Intune. mam. managedbrowser. disabledFeatures    |    **heslo** zakáže výzvy, které nabízejí uložení hesel pro koncového uživatele.<br>Služba **InPrivate** vypíná procházení InPrivate.<p>Chcete-li zakázat více funkcí, oddělujte hodnoty pomocí `|` . `inprivate|password`Zakáže například úložiště InPrivate i hesla.     |

> [!NOTE]
> Hraniční podpora pro Android nepodporuje zakázání správce hesel.

#### <a name="disable-extensions"></a>Zakázat rozšíření

V rámci hraničního rozhraní pro Android můžete zakázat architekturu rozšíření, která uživatelům brání v instalaci všech rozšíření aplikace. Uděláte to tak, že nakonfigurujete následující nastavení:

|    Klíč    |    Hodnota    |
|-----------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. disableExtensionFramework    |    **hodnota true** zakáže rozhraní rozšíření.<br>**false** (výchozí) povolí rozhraní rozšíření.    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Prostředí celoobrazovkového režimu na zařízeních s Androidem

Edge pro Android se dá povolit jako veřejná aplikace s následujícími nastaveními:

|    Klíč    |    Hodnota    |
|-----------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. enableKioskMode    |    **true** povolí celoobrazovkový režim pro Edge pro Android<br>**false** (výchozí) zakáže celoobrazovkový režim.    |
|    com. Microsoft. Intune. mam. managedbrowser. showAddressBarInKioskMode    |    **hodnota true** zobrazí panel Adresa v celoobrazovkovém režimu.<br> **false** (výchozí) skryje adresní řádek, když je povolený celoobrazovkový režim.    |
|    com. Microsoft. Intune. mam. managedbrowser. showBottomBarInKioskMode    |    **hodnota true** zobrazí dolní panel akcí v celoobrazovkovém režimu.<br> **false** (výchozí) skryje spodní panel, když je povolený celoobrazovkový režim.    |

## <a name="data-protection-app-configuration-scenarios"></a>Scénáře konfigurace aplikace pro ochranu dat

Edge pro iOS a Android podporuje zásady konfigurace aplikací pro následující nastavení ochrany dat, když je aplikace spravovaná pomocí Microsoft Endpoint Manageru se zásadami Intune App Protection použitými pro pracovní nebo školní účet, který je přihlášený k aplikaci, a nastavení zásad se doručují prostřednictvím zásad konfigurace aplikací spravovaných aplikací:

- Správa synchronizace účtu
- Správa omezených webů
- Správa konfigurace proxy serveru
- Správa webů s jednotným přihlašováním NTLM

Tato nastavení se dají nasadit do aplikace bez ohledu na stav registrace zařízení.

### <a name="manage-account-synchronization"></a>Správa synchronizace účtu

Ve výchozím nastavení umožňuje služba Microsoft Edge Sync uživatelům přístup k datům procházení napříč všemi přihlášenými zařízeními. Mezi data podporovaná synchronizací patří:

- Oblíbené
- Hesla
- Adresy a další (položka formuláře pro automatické vyplnění)

Funkce synchronizace je povolena prostřednictvím souhlasu uživatele a uživatelé mohou zapnout nebo vypnout synchronizaci pro každý z výše uvedených typů dat. Další informace najdete v tématu [synchronizace Microsoft Edge](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync).

Organizace mají možnost zakázat synchronizaci Edge na iOS a Androidu. 

|Klíč  |Hodnota  |
|---------|---------|
|com. Microsoft. Intune. mam. managedbrowser. Account. syncDisabled     |**true** (výchozí) umožňuje synchronizaci Edge.<br>**false** zakáže synchronizaci hran          |

### <a name="manage-restricted-web-sites"></a>Správa omezených webů

Organizace můžou definovat, k jakým webům můžou uživatelé přistupovat v kontextu pracovního nebo školního účtu pro iOS a Android. Pokud použijete seznam povolených uživatelů, budou mít uživatelé přístup jenom k lokalitám uvedeným explicitně. Pokud použijete blokovaný seznam, uživatelé budou mít přístup ke všem webům kromě těch, které jsou výslovně blokované. Měli byste jenom nastavit buď povolený, nebo blokovaný seznam, ne obojí. Pokud je nakonfigurujete, bude dodržen pouze seznam povolených.

Organizace také definuje, co se stane, když se uživatel pokusí přejít na web s omezeným přístupem. Ve výchozím nastavení jsou přechody povoleny. Pokud to organizace umožňuje, můžou se weby s omezeným přístupem otevírat v kontextu osobního účtu, v kontextu InPrivate služby Azure AD nebo bez ohledu na to, jestli je web zcela blokovaný. Další informace o různých scénářích, které jsou podporovány, naleznete v tématu [omezené přechody webů v Microsoft Edge Mobile](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). Díky tomu, že se převádějí prostředí, uživatelé organizace zůstanou chránění a udržují firemní prostředky v bezpečí.

> [!NOTE]
> Hraniční aplikace pro iOS a Android může blokovat přístup k webům jenom v případě, že se k nim přistupuje přímo. Neblokuje přístup, pokud uživatelé k přístupu k webu použijí zprostředkující služby (třeba překladatelské služby).

Pomocí následujících párů klíč/hodnota můžete nakonfigurovat seznam povolených nebo blokovaných webů pro systém iOS a Android. 

|Klíč  |Hodnota  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |Odpovídající hodnotou klíče je seznam adres URL. Všechny adresy URL, které chcete použít, můžete zadat jako jednu hodnotu oddělenou `|` znakem kanálu.<p>**Příklady:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |Odpovídající hodnotou klíče je seznam adres URL. Zadejte všechny adresy URL, které chcete blokovat, jako jednu hodnotu oddělenou znakem svislé čáry `|` .<br>**Příklady:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com. Microsoft. Intune. mam. managedbrowser. AllowTransitionOnBlock     |**true** (výchozí) umožňuje hraničním systémům pro iOS a Android přejít na servery s omezeným přístupem. Pokud nejsou osobní účty zakázané, zobrazí se uživatelům výzva k přepnutí do osobního kontextu pro otevření webu s omezeným přístupem nebo k přidání osobního účtu. Pokud je com. Microsoft. Intune. mam. managedbrowser. openInPrivateIfBlocked nastavené na true, uživatelé můžou v kontextu InPrivate otevřít lokalitu s omezeným přístupem.<p>**false** zabraňuje přechodu uživatelů na Edge pro iOS a Android. Uživatelům se zobrazí zpráva s informacemi o tom, že lokalita, ke které se pokouší získat přístup, je blokovaná.         |
|com. Microsoft. Intune. mam. managedbrowser. openInPrivateIfBlocked     |**hodnota true** umožňuje otevírání webů s omezeným přístupem v kontextu InPrivate účtu služby Azure AD. Pokud je účet Azure AD jediným účtem konfigurovaným pro iOS a Android, automaticky se otevře lokalita s omezeným přístupem v kontextu InPrivate. Pokud má uživatel nakonfigurovaný osobní účet, zobrazí se uživateli výzva k výběru mezi otevřením InPrivate nebo přepnutím na osobní účet.<p> **false** (výchozí) vyžaduje otevření webu s omezeným přístupem v osobním účtu uživatele. Pokud jsou osobní účty zakázané, bude lokalita blokovaná.<p>Aby se toto nastavení projevilo, com. Microsoft. Intune. mam. managedbrowser. AllowTransitionOnBlock musí být nastavené na true.          |
|com. Microsoft. Intune. mam. managedbrowser. durationOfOpenInPrivateSnackBar     | Zadejte počet sekund, po který se uživatelům zobrazí odkaz s oznámením na panelu kávu otevřeném v režimu InPrivate. Vaše organizace vyžaduje použití režimu InPrivate pro tento obsah. " Ve výchozím nastavení se oznámení na panelu kávu zobrazí po dobu 7 sekund.

Následující lokality jsou vždy povoleny bez ohledu na nastavení definovaného seznamu povolených nebo blokovaných seznamů:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>Formáty adres URL pro seznam povolených a blokovaných webů 

K vytvoření seznamu povolených a blokovaných webů můžete použít různé formáty adresy URL. Tyto povolené vzory jsou podrobně popsány v následující tabulce.

- Při zadávání adres URL do seznamu se ujistěte, že jste zadali předponu všechny adresy URL pomocí **http://** nebo **https://** .
- \*V souladu s pravidly v následujícím seznamu povolených vzorů můžete použít zástupný znak ().
- Zástupný znak může odpovídat jenom celé součásti názvu hostitele (oddělené tečkami) nebo celými částmi cesty (oddělené lomítky). Například `http://*contoso.com` není podporován. **not**
- V adrese můžete specifikovat čísla portů. Pokud nezadáte číslo portu, použijí se tyto hodnoty:
  - Port 80 pro protokol HTTP
  - Port 443 pro protokol HTTPS
- Použití zástupných znaků pro číslo portu **není podporováno.** Například `http://www.contoso.com:*` a `http://www.contoso.com:*/` podporované nejsou. 

    |    URL    |    Podrobnosti    |    Shody    |    Neodpovídá    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Odpovídá jediné stránce    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Odpovídá jediné stránce    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    Odpovídá všem adresám URL začínajícím na `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Vyhledá všechny subdomény pod`contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Odpovídá všem subdoménám končícím na`contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Odpovídá jediné složce    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Odpovídá jedné stránce s použitím čísla portu    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Odpovídá jediné zabezpečené stránce    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Odpovídá jediné složce a všem podsložkám    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Tady jsou uvedené příklady některých vstupů, které nemůžete zadat:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP adresy
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Správa konfigurace proxy serveru

Můžete použít Edge pro iOS a Android a [Azure proxy aplikací služby AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) společně a poskytnout uživatelům přístup k intranetovým webům na svých mobilních zařízeních. Příklad: 

- Uživatel používá mobilní aplikaci Outlook, která je chráněná službou Intune. Pak klikněte na odkaz na intranetový server v e-mailu a hraniční aplikace pro iOS a Android rozpozná, že tento intranetový server byl uživateli zpřístupněn prostřednictvím proxy aplikací. Uživatel je automaticky směrován prostřednictvím proxy aplikace, aby před dosažením intranetového serveru provedl ověřování pomocí služby Multi-Factor Authentication a podmíněného přístupu. Uživatel teď může získat přístup k interním webům i na jejich mobilních zařízeních a odkaz v Outlooku funguje podle očekávání.
- Uživatel otevře Edge pro iOS a Android na svém zařízení s iOS nebo Androidem. Pokud je Edge pro iOS a Android chráněný pomocí Intune a proxy aplikací je povolený, může uživatel přejít na intranetový server pomocí interní adresy URL, ke které se používá. Hraniční aplikace pro iOS a Android rozpozná, že tento intranetový server byl uživateli zpřístupněn prostřednictvím proxy aplikací. Uživatel je automaticky směrován prostřednictvím proxy aplikace, aby bylo možné provést ověření před dosažením intranetového webu. 

Než začnete, potřebujete:

- Pomocí Proxy aplikací služby AD Azure nastavte interní aplikace.
  - Postup konfigurace proxy aplikací a publikování aplikací najdete v [dokumentaci k instalaci](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- Aplikace Edge pro iOS a Android musí mít přiřazenou [zásadu ochrany aplikací Intune](app-protection-policy.md) .
- Aplikace Microsoftu musí mít zásady ochrany aplikací, které mají **omezení přenosu webového obsahu s jinými** nastaveními přenosů dat pro aplikace nastavené na **Microsoft Edge**.

> [!NOTE]
> Aktualizace dat přesměrování proxy aplikací může trvat až 24 hodin, než se projeví na hraničních zařízeních pro iOS a Android.

Cílová hrana pro iOS s následující dvojicí klíč/hodnota pro povolení proxy aplikací:

|    Klíč    |    Hodnota    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** povolí aplikace Azure AD scénáře přesměrování proxy serveru.<br>**false** (výchozí) zabrání scénářům aplikace Azure AD proxy.    |

> [!NOTE]
> Edge pro Android nespotřebovává tento klíč. Místo toho aplikace Edge pro Android spotřebovává konfiguraci služby Azure Proxy aplikací služby AD automaticky, pokud má účet služby Azure AD, který je přihlášený, nastavené zásady ochrany aplikací.

Další informace o tom, jak používat Edge pro iOS a Android a Azure Proxy aplikací služby AD v kombinaci s bezproblémovém (a chráněným) přístupem k místním webovým aplikacím, najdete v tématu [lepší spolupráce: Intune a Azure Active Directory tým pro zlepšení přístupu uživatelů](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). Tento Blogový příspěvek odkazuje na Intune Managed Browser, ale obsah se vztahuje i na Edge pro iOS a Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Správa webů s jednotným přihlašováním NTLM

Organizace můžou pro přístup k intranetovým webům vyžadovat, aby si uživatelé ověřili pomocí protokolu NTLM. Ve výchozím nastavení se uživatelům zobrazí výzva k zadání přihlašovacích údajů pokaždé, když přistupují k webu, který vyžaduje ověřování NTLM, protože ukládání přihlašovacích údajů NTLM je zakázané. 

Organizace můžou povolit ukládání přihlašovacích údajů NTLM do mezipaměti pro konkrétní weby. Po zadání přihlašovacích údajů uživatele a úspěšném ověření přihlašovacích údajů se pro tyto weby ve výchozím nastavení uloží do mezipaměti po dobu 30 dnů.


|Klíč  |Hodnota  |
|---------|---------|
|com. Microsoft. Intune. mam. managedbrowser. NTLMSSOURLs     |Odpovídající hodnotou klíče je seznam adres URL. Všechny adresy URL, které chcete použít, můžete zadat jako jednu hodnotu oddělenou `|` znakem kanálu.<p>**Příklady:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Další informace o typech podporovaných formátů adres URL naleznete v tématu [formáty URL pro seznam povolených a blokovaných webů](#url-formats-for-allowed-and-blocked-site-list).         |
|com. Microsoft. Intune. mam. managedbrowser. durationOfNTLMSSO     |Počet hodin pro přihlašovací údaje do mezipaměti, výchozí hodnota je 720 hodin.         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Nasazení scénářů konfigurace aplikací pomocí služby Microsoft Endpoint Manager

Pokud jako poskytovatele správy mobilních aplikací používáte Microsoft Endpoint Manager, následující kroky vám umožní vytvořit zásady konfigurace aplikace spravované aplikace. Po vytvoření konfigurace můžete přiřadit její nastavení skupinám uživatelů.

1. Přihlaste se ke [službě Microsoft Endpoint Manager](https://endpoint.microsoft.com).

2. Vyberte **aplikace** a pak vyberte **zásady konfigurace aplikací**.

3. V okně **zásady konfigurace aplikací** zvolte **Přidat** a vyberte **spravované aplikace**.

4. V části **základy** zadejte **název**a volitelný **Popis** nastavení konfigurace aplikace.

5. Pro **veřejné aplikace**vyberte **Vybrat veřejné aplikace**a potom v okně **cílové aplikace** zvolte možnost aplikace **pro iOS a Android** výběrem možnosti aplikace platformy iOS i Android. Kliknutím na **Vybrat** uložte vybrané veřejné aplikace.

6. Kliknutím na tlačítko **Další** dokončete základní nastavení zásady konfigurace aplikace.

7. V části **Nastavení** rozbalte **nastavení konfigurace Edge**.

8. Pokud chcete spravovat nastavení ochrany dat, nakonfigurujte odpovídající nastavení podle potřeby:

    - Pro **přesměrování proxy aplikací**vyberte z dostupných možností: **Povolit**, **Zakázat** (výchozí).

    - V poli **Adresa URL zástupce domovské stránky**zadejte platnou adresu URL, která bude obsahovat předponu buď *http://* nebo *https://*. Nesprávné adresy URL se z bezpečnostních důvodů blokují.

    - U **spravovaných záložek**zadejte název a platnou adresu URL, která obsahuje předponu buď *http://* nebo *https://*.

    - U **povolených adres URL**zadejte platnou adresu URL (jsou povoleny pouze tyto adresy URL. k ostatním webům nelze přicházet). Další informace o typech podporovaných formátů adres URL naleznete v tématu [formáty URL pro seznam povolených a blokovaných webů](#url-formats-for-allowed-and-blocked-site-list).

    - V případě **blokovaných adres URL**zadejte platnou adresu URL (zablokují se jenom tyto adresy URL). Další informace o typech podporovaných formátů adres URL naleznete v tématu [formáty URL pro seznam povolených a blokovaných webů](#url-formats-for-allowed-and-blocked-site-list).

    - Pro **přesměrování lokalit s omezeným přístupem do osobního kontextu**vyberte z dostupných možností: **Povolit** (výchozí), **Zakázat**.

    > [!NOTE]
    > Pokud jsou v zásadách definované povolené adresy URL i blokované adresy URL, bude se dodržovat jenom seznam povolených.

9. Pokud chcete další nastavení konfigurace aplikace, která nejsou vystavená výše uvedeným zásadám, rozbalte uzel **Obecné nastavení konfigurace** a odpovídajícím způsobem zadejte páry klíč-hodnota.

10. Po dokončení konfigurace nastavení klikněte na tlačítko **Další**.

11. V části **přiřazení** zvolte **Vybrat skupiny, které chcete zahrnout**. Vyberte skupinu Azure AD, ke které chcete přiřadit zásadu konfigurace aplikace, a pak zvolte **Vybrat**.

12. Až budete s přiřazením hotovi, klikněte na tlačítko **Další**.

13. V okně **vytvořit kontrolu zásad konfigurace aplikace + vytvořit** zkontrolujte nakonfigurovaná nastavení a klikněte na **vytvořit**.

Nově vytvořená zásada konfigurace se zobrazí v okně **Konfigurace aplikace** .

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Přístup k protokolům spravovaných aplikací pomocí hraničních zařízení s iOS a Androidem

Uživatelé s hranou pro iOS a Android nainstalovaný na svém zařízení s iOS nebo Androidem můžou zobrazit stav správy všech aplikací publikovaných Microsoftem. Můžou odesílat protokoly pro řešení potíží se spravovanými aplikacemi pro iOS nebo Android pomocí následujících kroků:

1. Otevřete na svém zařízení Edge pro iOS a Android.
2. Do pole adresy zadejte `about:intunehelp`.
3. Hraniční režim pro iOS a Android se spouští v režimu odstraňování potíží.

Seznam nastavení uložených v protokolech aplikací najdete v tématu [Kontrola protokolů ochrany klientských aplikací](app-protection-policy-settings-log.md).

Informace o tom, jak zobrazit protokoly na zařízeních s Androidem, najdete v tématu [odeslání protokolů správci IT e-mailem](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="next-steps"></a>Další kroky

- [Co jsou zásady ochrany aplikací?](app-protection-policy.md) 
- [Zásady konfigurace aplikací v Microsoft Intune](app-configuration-policies-overview.md)
