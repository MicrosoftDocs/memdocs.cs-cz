---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e5c7ce18cc00934438e945933188d9634b36653
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332471"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Vývoj pro Microsoft Intune – březen 2020

Tato stránka vám umožní v rámci připravenosti a plánování vypsat aktualizace uživatelského rozhraní Intune a funkce, které jsou ve vývoji, ale ještě nejsou vydané. Kromě informací na této stránce: 

- Pokud předpokládáme, že před změnou budete muset provést nějakou akci, zveřejníme doplňkový příspěvek v centru zpráv Office.
- Pokud funkce vstoupí do produkčního prostředí, ať už je verze Preview, nebo je všeobecně dostupná, popis funkce se přesune z této stránky na [co je nového](whats-new.md).
- Tato stránka a stránka [co je nového](whats-new.md) se pravidelně aktualizují. Přijďte se tedy znovu podívat, jestli nejsou k dispozici nové informace.
- Strategické dodávky a časová osa najdete v tématu [Microsoft 365 plán](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) .

> [!NOTE]
> Tato stránka odráží naše aktuální očekávání na možnosti Intune v budoucí verzi. Data a jednotlivé funkce se můžou změnit. Tato stránka nepopisuje všechny funkce vývoje.

**Informační kanál RSS**: Zjistěte, kdy se tato stránka aktualizuje zkopírováním a vložením následující adresy URL do čtečky informačních kanálů: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Správa aplikací

### <a name="retarget-web-clips-to-microsoft-edge-on-iosipados-devices---5455276---"></a>Změna cílení webových klipů na zařízení s iOS nebo iPadOS na Microsoft Edge<!-- 5455276 -->
Webové klipy, které fungují jako připnuté webové aplikace v zařízeních s iOS/iPadOS, budou muset být aktualizované. Nově nasazené webové klipy se otevřou v Microsoft Edge místo Intune Managed Browser, pokud je to potřeba pro otevření v chráněném prohlížeči. Aby bylo zajištěno, že budou otevřeny v Microsoft Edge místo Managed Browser, je třeba změnit cílení na stávající webové klipy.

### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS a iOS – aktualizace Portál společnosti<!-- 5779439, 5780234  -->
Podokno profil Portál společnosti macOS a iOS se aktualizuje tak, aby obsahovalo tlačítko Odhlásit se. Tato aktualizace navíc zahrnuje vylepšení uživatelského rozhraní do podokna profil v macOS Portál společnosti. Další informace o Portál společnosti naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

### <a name="updates-to-branding-and-customization-pane---5236032---"></a>Aktualizace značky a podokna přizpůsobení<!-- 5236032 -->
Aktualizujeme podokno Intune, které se v současné době nazývá branding a přizpůsobení, včetně těchto vylepšení:

- Přejmenujte podokno na **přizpůsobení**.
- Vylepšení organizace a návrhu nastavení.
- Vylepšení textu a popisů nastavení

Pokud chcete toto nastavení v Intune najít, přejděte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte možnost **Správa tenanta** > **přizpůsobení**. Informace o existujícím přizpůsobení najdete v části [How to configure Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

### <a name="configure-the-ios-microsoft-azure-ad-sso-app-extension---567534----"></a>Konfigurace rozšíření aplikace pro iOS Microsoft Azure AD SSO<!-- 567534  -->
Microsoft Azure AD tým vyvíjí rozšíření aplikace jednotného přihlašování (SSO) pro jednotné přihlašování (SSO), které uživatelům s iOS a iPadOS 13.0 + umožní bezproblémově získat přístup k aplikacím a webům Microsoftu s jedním přihlašováním. Po vydání rozšíření aplikace AAD SSO budete moct nakonfigurovat rozšíření jednotného přihlašování s **funkcemi zařízení** > profil **rozšíření aplikace jednotného přihlašování** v konzole pro správu s minimálními kliknutími.

Další informace o rozšířeních aplikace SSO pro iOS nebo o tom, jak nakonfigurovat funkce zařízení, najdete v tématu [rozšíření aplikace jednotného přihlašování](../configuration/device-features-configure.md#single-sign-on-app-extension).

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Portál společnosti pro iOS pro podporu režimu na šířku<!--6048329  -->
Uživatelé budou moct zaregistrovat svoje zařízení, Hledat aplikace a získat podporu na základě orientace obrazovky podle jejich výběru. Aplikace bude automaticky rozpoznávat a upravovat obrazovky, aby odpovídaly režimu na výšku nebo na šířku, pokud uživatelé nezamkne obrazovku v režimu na výšku.

### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128-idready-idstaged---"></a>Konfigurace dostupnosti registrace v Portál společnosti pro Android a iOS<!-- 4260128 idready idstaged -->
Bude k dispozici nové nastavení, které vám umožní nakonfigurovat, jestli registrace zařízení v Portál společnosti v zařízeních s Androidem a iOS jsou k dispozici s výzvami, k dispozici bez výzvy nebo uživatelům nedostupným. Pokud chcete toto nastavení v Intune najít, přejděte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte možnost **Správa tenanta** > **přizpůsobení** > **upravte** > **registrace zařízení**. Další informace o existujícím přizpůsobení Portál společnosti naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Vylepšené prostředí pro přihlašování v Portál společnosti pro Android<!-- 6103997  -->
Aktualizujeme rozložení několika přihlašovacích obrazovek v aplikaci Portál společnosti pro Android, aby bylo prostředí pro uživatele užitečnější, jednoduché a čisté.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profily konfigurace síťových zařízení s drátovou sítí pro zařízení macOS<!-- 3508686  -->
Bude k dispozici nový profil konfigurace zařízení macOS, který konfiguruje drátové sítě (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **MacOS** pro typ profilu > platformed **Network** pro typ profilu). Pomocí této funkce můžete vytvořit profily 802.1 x ke správě drátových sítí a tyto drátové sítě nasadit do zařízení macOS.

Platí pro:
- macOS

### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices----1947932----"></a>Profily sítě VPN s připojením IKEv2 VPN můžou používat Always On se zařízeními se systémem iOS/iPadOS. <!-- 1947932  -->
Na zařízeních se systémem iOS/iPadOS můžete vytvořit profil sítě VPN, který používá připojení IKEv2 (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS/iPadOS** pro pro typ profilu Platform > **VPN** ). V budoucí aktualizaci můžete nakonfigurovat Always On s IKEv2. Po nakonfigurování se profily IKEv2 VPN připojují automaticky a udržují se připojení (nebo rychlé opětovné připojení) k síti VPN. Zůstane připojený i při přesunu mezi sítěmi nebo po restartování zařízení.

V systému iOS/iPadOS je vždycky zapnutá síť VPN omezená na profily IKEv2.

Pokud chcete zobrazit aktuální nastavení IKEv2, která můžete konfigurovat, přejděte na téma [Přidání nastavení sítě VPN na zařízeních s iOS/iPadOS v Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Platí pro:
- iOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Vylepšené prostředí uživatelského rozhraní při vytváření konfiguračních profilů na zařízeních s iOS/iPadOS a macOS<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
Když vytváříte profil pro zařízení s iOS/iPadOS nebo macOS, bude se aktualizovat prostředí v centru pro správu správy koncových bodů. Tato změna má vliv na následující konfigurační profily zařízení (**zařízení** > **konfiguračních profilech** > **Vytvoření profilu** > **iOS** nebo **MacOS** pro platformu):

- Vlastní: iOS/iPadOS, macOS
- Funkce zařízení: iOS/iPadOS, macOS
- Omezení zařízení: iOS/iPadOS, macOS
- Ochrana koncového bodu: macOS
- Rozšíření: macOS
- Soubor předvoleb: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Vylepšené uživatelské rozhraní při vytváření OEMConfig konfigurací profilů na zařízeních s Androidem Enterprise<!-- 5568645   -->
Když vytváříte nebo upravujete profil OEMConfig pro zařízení s Androidem Enterprise, bude se aktualizovat prostředí v centru pro správu správy koncových bodů. Aktualizované prostředí vám poskytne přehled o nastaveních, která jste nakonfigurovali na první pohled. Tato změna má vliv na konfigurační profil zařízení OEMConfig (**zařízení** > **konfiguračních profilů** > **vytvořit profil** > **Android Enterprise** for Platform > **OEMConfig** pro typ profilu).

Tato funkce platí pro:
- Android Enterprise 

### <a name="enterprise-app-trust-settings-modification-setting-will-be-removed-from-iosipados-device-restriction-profiles---6225131----"></a>Nastavení pro změnu nastavení vztahu důvěryhodnosti podnikových aplikací se odebere z profilů omezení zařízení s iOS/iPadOS.<!-- 6225131  -->
Na zařízeních se systémem iOS/iPadOS vytvoříte profil omezení zařízení (**zařízení** > **Konfigurace profilů** > **vytvořit profil** > **iOS/iPadOS** pro **omezení** platformy > pro typ profilu). Nastavení pro **změnu nastavení vztahu důvěryhodnosti podnikových aplikací** bude odebráno společností Apple a bude odebráno z Intune. Pokud toto nastavení aktuálně používáte v profilu, nemá žádný vliv a zůstane ve vašem profilu, dokud nevytvoříte nový profil. Toto nastavení se taky odebere z jakéhokoli vytváření sestav v Intune.

Platí pro:
- iOS/iPadOS

Pokud chcete zobrazit nastavení, která můžete omezit, přejděte na [nastavení zařízení s iOS a iPadOS a povolte nebo zakažte funkce](../configuration/device-restrictions-ios.md).

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Nastavení a hodnoty konfiguračního profilu zařízení se aktualizují pro platformy Windows.<!-- 4091122 -->
Když vytváříte profily konfigurace zařízení pro platformy Windows (**zařízení** > **konfigurační profily** > **vytvořit profil** > libovolnou možnost **Windows** pro platformu), některá nastavení a jejich hodnoty se liší od CSP a můžou být matoucí. Názvy nastavení a jejich hodnoty budou aktualizovány, aby byly lépe jasné.

Platí pro:

- Profily konfigurace zařízení s Windows 10 a novějšími
- Konfigurační profily zařízení ve Windows Holografick pro firmy
- Windows 8.1 konfigurační profily zařízení
- Profily konfigurace zařízení Windows Phone 8,1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Vylepšené uživatelské rozhraní při vytváření profilů omezení zařízení pro zařízení s Androidem a Androidem Enterprise<!-- 5841361 -->
Když vytvoříte profil pro zařízení s Androidem nebo Androidem Enterprise, bude se aktualizovat prostředí v centru pro správu správy koncových bodů. Tato změna má vliv na následující konfigurační profily zařízení (**zařízení** > **konfiguračních** profilech > **Vytvoření profilu** > **Správce zařízení s Androidem** nebo **Android Enterprise** for Platform):

- Omezení zařízení: Správce zařízení s Androidem
- Omezení zařízení: vlastník zařízení se systémem Android Enterprise
- Omezení zařízení: pracovní profil Android Enterprise

Další informace o omezeních zařízení, která můžete konfigurovat, najdete v tématu [Správce zařízení s Androidem](../configuration/device-restrictions-android.md) a [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355----"></a>Odstranění sad a polí sady prostředků v profilech konfigurace zařízení OEMConfig na zařízeních s Androidem Enterprise<!-- 5550355  -->
Na zařízeních s Androidem Enterprise vytvoříte a aktualizujete profily OEMConfig. Uživatelé budou moct pomocí **Návrháře konfigurace** v Intune odstraňovat sady a pole sad.

Další informace o profilech OEMConfig najdete v tématu [použití a Správa zařízení se systémem Android Enterprise pomocí nástroje OEMConfig v Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Tato funkce platí pro:
- Android Enterprise

### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Podpora WPA a WPA2 v profilech pro iOS Enterprise Wi-Fi<!--6215273   -->
Do [profilu podnikové sítě Wi-Fi pro iOS](../configuration/wi-fi-settings-ios.md) přidáváme pole *typ zabezpečení* (**zařízení** > **konfiguračních** profilech > **vytvořit profil** a potom pro něj vyberte **iOS/iPadOS** pro *platformu* a pak **Wi-Fi** pro *profil* ). To se podobá možnostem dostupným pro základní profil Wi-Fi pro iOS. Tato změna vám umožní vytvořit nové profily, které určují typ zabezpečení **WPA-Enterprise** nebo **WPA/WPA2-podnikové**, a pak určíte výběr pro *typ protokolu EAP*.

### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-profiles---5615208-----"></a>Nové uživatelské prostředí pro profily certifikátů, e-mailů, VPN a Wi-Fi<!-- 5615208   -->
Aktualizace [uživatelského prostředí](../configuration/device-profile-create.md) v centru pro správu služby Endpoint Management (**zařízení** > **konfiguračních profilech** > **vytvořit profil**) pro vytváření a úpravu následujících typů profilů. Nové prostředí bude mít stejné nastavení jako předtím, ale bude používat prostředí podobné průvodci, které nevyžaduje tolik horizontální posouvání. Pro nové prostředí nebudete muset měnit existující konfigurace.
- Odvozené přihlašovací údaje
- E-mail
- Certifikát PKCS
- Importovaný certifikát PKCS
- Certifikát SCEP
- Důvěryhodný certifikát
- Síť VPN
- Wi-Fi

(**Zařízení** > **konfigurační profily** > **vytvořit profil**a potom pro *typ profilu* vyberte některý z předchozích profilů.)

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurace aplikace Microsoft Defender ATP pro macOS  <!-- 5520115  -->
Brzy budete moct nakonfigurovat [Nastavení](../protect/endpoint-protection-macos.md) pro aplikaci Microsoft Defender ATP pro zařízení, která používají MacOS jako součást konfiguračního profilu zařízení ochrany koncových bodů (**zařízení** > **konfiguračních** profilech > **vytvořit profil**, vyberte pro *platformu* **MacOS** a pak jako *typ profilu* **Endpoint Protection** ). Pro konfiguraci zařízení macOS bude k dispozici osm nastavení. 

Ochrana ATP v programu Defender je podporovaná na macOS 10,13 (s vysokou verzí Sierra) a novějších a aplikace [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) musí být *po* těchto nastaveních nasazená do zařízení. Nastavení byste měli před nasazením aplikace poslat do zařízení. Beta verze macOS se nepodporují.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nové nastavení trezoru úložiště pro macOS Endpoint Protection zásady konfigurace zařízení<!-- 5459801   -->
Do kategorie trezoru úložišť přidáváme nové nastavení v rámci šablony [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) : skryjte obnovovací klíč. (**Zařízení** > **konfiguračních profilů** > **vytvořit profil**vyberte pro *platformu* **MacOS** a pak jako *typ profilu*nastavte **Endpoint Protection** ). Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. Uživatel zařízení si může svůj osobní obnovovací klíč kdykoli zobrazit z aplikace Portál společnosti pro iOS nebo z webu portál společnosti pro šifrované zařízení macOS. Pokud si chcete zobrazit klíč pro osobní obnovení, můžete přejít na podrobnosti o zařízení a kliknout na *získat obnovovací klíč*.

Toto nastavení nebude k dispozici v dříve vytvořených zásadách. Abyste mohli nakonfigurovat toto nastavení tak, aby ho bylo možné používat, budete muset znovu vytvořit zásady trezoru úložišť. 

###  <a name="ui-update-when-configuring-compliance-policy----3961639----"></a>Aktualizace uživatelského rozhraní při konfiguraci zásad dodržování předpisů <!-- 3961639  -->
Aktualizujeme uživatelské rozhraní pro konfiguraci zásad dodržování předpisů v Microsoft Endpoint Manageru (**zařízení** > **zásady dodržování předpisů** > **zásady** > **vytvořit zásadu**). Zobrazí se nové uživatelské prostředí, které bude obsahovat stejné nastavení a podrobnosti, které jste použili dříve. Nové prostředí bude postupovat podle procesu podobného průvodci a vytvoří zásady dodržování předpisů a bude obsahovat stránku, kde můžete přidat *přiřazení* zásad a pak stránku *souhrnu* , kde můžete před vytvořením zásady zkontrolovat konfiguraci. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Konfigurovat agenta Optimalizace doručení při stahování obsahu aplikace Win32<!-- 5410945  -->
Agent pro optimalizaci doručení budete moct nakonfigurovat tak, aby stahoval obsah aplikace Win32 buď v režimu pozadí, nebo v režimu popředí na základě přiřazení. U stávajících aplikací Win32 bude obsah dál stahovat v režimu pozadí. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **všechny aplikace** > *Vyberte vlastnosti aplikace Win32* > **Properties**. V poli **přiřazení**vyberte **Upravit** .  Upravte přiřazení výběrem možnosti **Zahrnout** do **režimu** v **požadované** části.  V části **nastavení aplikace** najdete nové nastavení, když bude k dispozici. Další informace o optimalizaci doručení najdete v tématu [Správa aplikací Win32 – Optimalizace doručení](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Změna primárního uživatele pro zařízení s Windows <!-- 3794742 -->
Můžete změnit primárního uživatele pro zařízení s Windows Hybrid a připojená k Azure AD. Provedete to tak, že přejdete na **zařízení** > **Intune** > **všechna zařízení** > vyberte zařízení > **vlastnosti** > **primární uživatel**.

### <a name="new-android-report-on-android-devices-overview-page---5435435---"></a>Stránka s přehledem nové sestavy pro Android na zařízeních s Androidem<!-- 5435435 -->
Do konzoly pro správu Microsoft Endpoint Manageru přidáme sestavu na stránce Přehled zařízení s Androidem, která zobrazuje, kolik zařízení s Androidem je zaregistrované v jednotlivých řešeních pro správu zařízení. Tento graf (podobně jako stejný graf, který už je v konzole Azure), zobrazuje počet zaregistrovaných zařízení s pracovním profilem, plně spravovaným, vyhrazeným a správcem zařízení. Chcete-li zobrazit sestavu, vyberte možnost **zařízení** > **Android** > **Overview**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Další vlastnosti inventáře zařízení datového skladu<!-- 6125732  -->
Další vlastnosti inventáře zařízení budou k dispozici v datovém skladu Intune. Následující vlastnosti budou zpřístupněny prostřednictvím kolekce [zařízení](../developer/intune-data-warehouse-collections.md#devices) :

- Kapacita úložiště
- Kapacita paměti
- Verze Office 365
- Model zařízení

Další informace o datovém skladu najdete v tématu [Microsoft Intune rozhraní API datového skladu](../developer/reports-nav-intune-data-warehouse.md).

### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738--"></a>Příručka uživatelů ze správy zařízení s Androidem do správy profilů práce<!--5857738-->
Vydáváme nové nastavení dodržování předpisů pro platformu pro správce zařízení s Androidem. Toto nastavení umožňuje nastavit nekompatibilní zařízení, pokud je spravované pomocí Správce zařízení.

Na těchto nevyhovujících zařízeních se na stránce **aktualizovat nastavení zařízení** uživatelům zobrazí zpráva o **nastavení přesunout na novou správu zařízení** . Pokud klepnete na tlačítko **vyřešit** , provedou se tímto způsobem:

1. Rušení registrace správy správců zařízení
2. Registrace ve správě pracovních profilů
3. Řešení problémů s dodržováním předpisů

Google podporuje Správce zařízení v nových verzích Androidu ve snaze přejít na moderní, bohatou a bezpečnější správu zařízení pomocí Androidu Enterprise.  Intune může poskytnout úplnou podporu pro zařízení s Androidem spravovaná pomocí Správce zařízení s Androidem 10 nebo novějším prostřednictvím nástroje Q2 CY2020. Zařízení spravovaná správcem zařízení (s výjimkou Samsung), která po této době používají Android 10 nebo novější, se nebudou moct zcela spravovat. Zvláště ovlivněná zařízení nebudou dostávat nové požadavky na heslo. Další informace najdete v tomto [oznámení](#decreasing-support-for-android-device-administrator).

### <a name="retire-noncompliant-devices---1827291---"></a>Vyřazení zařízení nesplňujících požadavky<!-- 1827291 -->
Přidáváme novou volitelnou akci dodržování předpisů pro vyřazení zařízení nesplňujících požadavky (**zařízení** > **zásady dodržování předpisů** > **zásady** > **vytvořit zásadu** a pak zobrazit dostupné *Akce* na stránce *Akce při nedodržení předpisů* ).  Vyřazení zařízení, které nedodržuje předpisy, odebere z něj všechna firemní data a také odebere zařízení ze správy Intune. Tato akce se spustí, když je dosaženo nakonfigurované hodnoty ve dnech. Minimální hodnota je 30 dní.  K vyřazení zařízení pomocí části *vyřazení zařízení nedodržujících předpisy* se bude vyžadovat explicitní schválení správce IT, kde správci můžou vyřadit všechna oprávněná zařízení.

### <a name="new-information-in-device-details---5604099---"></a>Podrobnosti o nových informacích o zařízení<!-- 5604099 -->
Na stránce **Přehled** pro zařízení se zobrazí následující informace:

- Kapacita úložiště (množství fyzického úložiště v zařízení)
- Kapacita paměti (množství fyzické paměti v zařízení)

### <a name="script-support-for-macos-devices---4280361----"></a>Podpora skriptů pro zařízení macOS<!-- 4280361  -->
Budete moct přidávat a nasazovat skripty pro zařízení macOS. Tato podpora rozšiřuje vaši schopnost nakonfigurovat zařízení macOS nad rámec toho, co je možné na zařízeních macOS využít nativní možnosti MDM.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

### <a name="help-and-support-workflow-update-to-support-additional-services---5654170---"></a>Aktualizace pracovního postupu pomoc a podpora pro podporu dalších služeb<!-- 5654170 -->
Aktualizujeme stránku pro pomoc a podporu v centru pro správu Microsoft Endpoint Manageru, takže budete moct zvolit typ správy, který používáte, pro lepší poskytování konkrétní podpory (**řešení potíží + podpora** >  **nápovědě a podpoře**). Tato změna vám umožní vybrat z následujících typů správy:
- Configuration Manager (zahrnuje analýzu stolního počítače)
- Intune
- Spoluspráva

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Zabezpečení

### <a name="derived-credentials-support-on-android-cobo-devices--4839592--"></a>Podpora odvozených přihlašovacích údajů na zařízeních s Androidem COBO<!--4839592-->
V zařízeních s plnou správou pro Android Enterprise budete moct používat odvozená pověření. Podpora bude zahrnovat načítání odvozených přihlašovacích údajů pro Entrust Datacard, Intercede a DISA purebred. U aplikací, které ji podporují, budete moct používat odvozená pověření pro ověřování aplikací, podepisování Wi-Fi, VPN nebo šifrování S/MIME.

### <a name="use-antivirus-policy-to-manage-settings-for-microsoft-defender-antivirus-and-the-windows-security-experience--6131401---"></a>Použití zásad antivirové ochrany pro správu nastavení antivirové ochrany v programu Microsoft Defender a prostředí zabezpečení systému Windows<!--6131401 -->
V uzlu *zabezpečení koncového bodu* budete moct nakonfigurovat nastavení pro **antivirovou ochranu**. Když konfigurujete zásady pro antivirovou ochranu, definujete nastavení pro zařízení s Windows 10 prostřednictvím dvou typů profilů:

- Antivirová ochrana v programu Microsoft Defender: umožňuje spravovat nastavení cloudové ochrany, vyloučení antivirové ochrany, nápravy, možnosti kontroly a další funkce.
- Prostředí zabezpečení systému Windows: umožňuje spravovat způsob, jakým uživatelé na svých zařízeních nastanou nastavení zabezpečení systému Windows. Budete moct nakonfigurovat, co můžou koncoví uživatelé zobrazit v centru zabezpečení v programu Microsoft Defender a v oznámeních, která obdrží.

### <a name="users-personal-encrypted-recovery-key---6273943---"></a>Osobní šifrovaný obnovovací klíč uživatele<!-- 6273943 -->
K dispozici je nová funkce Intune, která umožňuje uživatelům načíst svůj osobní zašifrovaný klíč obnovení **trezoru úložiště** pro zařízení Mac přes aplikaci pro Android portál společnosti nebo prostřednictvím aplikace Intune pro Android. V aplikaci Portál společnosti i v aplikaci Intune bude odkaz, ve kterém se otevře prohlížeč Chrome pro web Portál společnosti, kde může uživatel zobrazit obnovovací klíč **trezoru** souborů potřebný pro přístup k zařízením Mac. Další informace o šifrování najdete v tématu [použití šifrování zařízení s Intune](../protect/encrypt-devices.md).

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Nastavení předvoleb ochrany osobních údajů pro zařízení macOS<!-- 2934232 --> 
S vydáním verze macOS Catalina 10,15 Společnost Apple přidala nové vylepšení zabezpečení a ochrany osobních údajů. Ve výchozím nastavení nemůžou aplikace a procesy získat přístup k určitým datům bez souhlasu uživatele. Pokud uživatelé neposkytnou souhlas, aplikace a procesy nemusí fungovat. Intune přidává podporu pro nastavení, která správcům IT umožní povolit nebo zakázat souhlas s přístupem k datům jménem koncových uživatelů na zařízeních s macOS 10,14 a novějším. Tato nastavení zajistí, že aplikace a procesy budou nadále fungovat správně a omezují počet výzev, které koncoví uživatelé zaznamenají.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Aktualizovaný text a popisky uživatelského rozhraní pro nastavení profilu Endpoint Protection ve Windows 10<!-- 5983747 -->
Aktualizujeme text pro různá nastavení, která nakonfigurujete jako konfigurační profily zařízení s Windows 10, aby bylo snazší pochopit zamýšlené použití a výsledky.

Nastavení, která aktualizujeme, zahrnují konfigurační profily zařízení s Windows 10 pro:

- [Omezení zařízení](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > antivirová ochrana v programu Microsoft Defender  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > antivirová ochrana v programu Microsoft Defender

Nastavení podporovaná v Intune se nemění. Toto je pouze aktualizace textu uživatelského rozhraní v centru pro správu služby Microsoft Endpoint Management.

<!-- ***********************************************-->
## <a name="notices"></a>Oznámení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
