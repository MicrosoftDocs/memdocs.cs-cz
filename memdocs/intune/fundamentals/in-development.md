---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a807a90cdca18d79e7b92b4efeb56d341da2596
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438717"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>Ve vývoji Microsoft Intune – duben 2020

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Aktualizace zásad konfigurace aplikací pro Android<!-- 6113334  -->
Zásady konfigurace aplikací pro Android se aktualizují tak, aby správcům při vytváření konfiguračního profilu aplikace mohli vybrat typ registrace zařízení. Tato funkce je přidávána do účtu pro profily certifikátů, které jsou založeny na typu registrace (pracovní profil nebo vlastník zařízení).  Při vydaných verzích dojde k následujícímu:

- Stávající zásady vytvořené před vydáním této funkce, které nemají žádné profily certifikátů přidružené k zásadám, budou ve výchozím nastavení profil pracovního profilu a vlastníka zařízení pro typ registrace zařízení.
- Stávající zásady vytvořené před vydáním této funkce, které mají přidružené profily certifikátů, budou mít výchozí jenom pracovní profil.
- Pokud je vytvořený nový profil a pro typ registrace zařízení je vybraný profil pracovního profilu a vlastníka zařízení, nebudete moct k zásadě konfigurace aplikace přidružit profil certifikátu.
- Pokud je vytvořen nový profil a je vybrán pouze pracovní profil, mohou být využívány Zásady certifikátů pracovního profilu vytvořené v části Konfigurace zařízení.
- Pokud je vytvořen nový profil a je vybrán pouze vlastník zařízení, může být využita zásada certifikátu vlastníka zařízení vytvořená v části Konfigurace zařízení.

Stávající zásady nebudou opravovat ani vydávat nové certifikáty.

Kromě toho přidáváme e-mailové profily gmail a devět e-mailů, které budou fungovat pro typy registrace pracovní profil i vlastník zařízení, včetně použití profilů certifikátů v obou typech konfigurace e-mailu.  Všechny zásady Gmail nebo devět, které jste vytvořili v části Konfigurace zařízení pro pracovní profily, se budou i nadále používat pro zařízení a není nutné je přesouvat do zásad konfigurace aplikací.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete najít zásady konfigurace aplikací tak, že vyberete **aplikace** > zásady **Konfigurace aplikací**. Další informace o zásadách konfigurace aplikací najdete v tématu [zásady konfigurace aplikací pro Microsoft Intune](../apps/app-configuration-policies-overview.md).

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams je teď součástí sady Office 365 pro macOS<!-- 5903936  -->
Uživatelům, kteří jsou přiřazeni systém Microsoft Office pro macOS ve službě Microsoft Endpoint Manager, teď budou kromě stávajících aplikací systém Microsoft Office (Word, Excel, PowerPoint, Outlook a OneNote) dostávat i týmy Microsoftu. Intune rozpozná existující zařízení Mac, na kterých je nainstalovaný jiný Office pro aplikace macOS, a pokusí se nainstalovat Microsoft Teams při příštím ověření zařízení v Intune. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete najít **sadu Office 365 Suite** pro MacOS, a to tak, že vyberete **aplikace** > **MacOS** > **Přidat**. Další informace najdete v tématu [přiřazení Office 365 k MacOS zařízením pomocí Microsoft Intune](../apps/apps-add-office365-macos.md).

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Podpora pro podokno přizpůsobení pro skupinu <!-- 4722837  -->
Nastavení můžete cílit v podokně přizpůsobení na skupiny uživatelů. Na portálu Intune vyberte **klientské aplikace** > **přizpůsobení**. Další informace najdete v tématu [postup přizpůsobení aplikací Portál společnosti Intune, Portál společnosti webu a Intune App] (společnost-portál-app.md].

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profily konfigurace síťových zařízení s drátovou sítí pro zařízení macOS<!-- 3508686  -->
Bude k dispozici nový profil konfigurace zařízení macOS, který konfiguruje drátové sítě (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **MacOS** pro typ profilu > platformed **Network** pro typ profilu). Pomocí této funkce můžete vytvořit profily 802.1 x ke správě drátových sítí a tyto drátové sítě nasadit do zařízení macOS.

Platí pro:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Vylepšené prostředí uživatelského rozhraní při vytváření konfiguračních profilů na zařízeních s iOS/iPadOS a macOS<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
Když vytváříte profil pro zařízení s iOS/iPadOS nebo macOS, bude se aktualizovat prostředí v centru pro správu správy koncových bodů. Tato změna má vliv na následující konfigurační profily zařízení (**zařízení** > **konfiguračních profilech** > **Vytvoření profilu** > **iOS** nebo **MacOS** pro platformu):

- Vlastní: iOS/iPadOS, macOS
- Funkce zařízení: iOS/iPadOS, macOS
- Omezení zařízení: iOS/iPadOS, macOS
- Ochrana koncového bodu: macOS
- Rozšíření: macOS
- Soubor předvoleb: macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Nastavení a hodnoty konfiguračního profilu zařízení se aktualizují pro platformy Windows.<!-- 4091122 -->
Když vytváříte profily konfigurace zařízení pro platformy Windows (**zařízení** > **konfigurační profily** > **vytvořit profil** > libovolnou možnost **Windows** pro platformu), některá nastavení a jejich hodnoty se liší od CSP a můžou být matoucí. Názvy nastavení a jejich hodnoty se aktualizují tak, aby byly jasné.

Platí pro:

- Profily konfigurace zařízení s Windows 10 a novějšími
- Konfigurační profily zařízení ve Windows Holografick pro firmy
- Windows 8.1 konfigurační profily zařízení
- Profily konfigurace zařízení Windows Phone 8,1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurace aplikace Microsoft Defender ATP pro macOS  <!-- 5520115  -->
Brzy budete moct nakonfigurovat [Nastavení](../protect/endpoint-protection-macos.md) pro aplikaci Microsoft Defender ATP pro zařízení, která používají MacOS jako součást konfiguračního profilu zařízení ochrany koncových bodů (**zařízení** > **konfiguračních** profilech > **vytvořit profil**, vyberte pro *platformu* **MacOS** a pak jako *typ profilu* **Endpoint Protection** ). Pro konfiguraci zařízení macOS bude k dispozici osm nastavení. 

Ochrana ATP v programu Defender je podporovaná na macOS 10,13 (s vysokou verzí Sierra) a novějších a aplikace [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) musí být *po* těchto nastaveních nasazená do zařízení. Nastavení byste měli před nasazením aplikace poslat do zařízení. Beta verze macOS se nepodporují.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nové nastavení trezoru úložiště pro macOS Endpoint Protection zásady konfigurace zařízení<!-- 5459801   -->
Do kategorie trezoru úložišť přidáváme nové nastavení v rámci šablony [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) : skryjte obnovovací klíč. (**Zařízení** > **konfiguračních profilů** > **vytvořit profil**vyberte pro *platformu* **MacOS** a pak jako *typ profilu*nastavte **Endpoint Protection** ). Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. Uživatel zařízení si může svůj osobní obnovovací klíč kdykoli zobrazit z aplikace Portál společnosti pro iOS nebo z webu portál společnosti pro šifrované zařízení macOS. Pokud si chcete zobrazit klíč pro osobní obnovení, můžete přejít na podrobnosti o zařízení a kliknout na *získat obnovovací klíč*.

Toto nastavení nebude k dispozici v dříve vytvořených zásadách. Abyste mohli nakonfigurovat toto nastavení tak, aby ho bylo možné používat, budete muset znovu vytvořit zásady trezoru úložišť. 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Odeslání nabízených oznámení jako akce při nedodržení předpisů <!-- 1733150   -->
V případě platforem iOS a Android přidáváme novou akci při nedodržení předpisů, která odešle nabízené oznámení v aplikaci Portál společnosti. Uživatelé můžou kliknout na oznámení, která spustí aplikaci Portál společnosti, která pak zobrazí důvod, proč nedodržují předpisy. Správci budou moct tuto novou akci nakonfigurovat pro nedodržování předpisů v centru pro správu Microsoft Endpoint Manageru, a to tak, že přejdete na **zařízení** > **zásady dodržování předpisů** > **vytvořit zásadu**a pak vyberete *akci* pro odeslání nabízeného oznámení aplikace.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Předběžné vydání testování pro spravované aplikace Google Play<!-- 2681933  -->
Organizace, které používají [ukončené testy testů Google Play pro předběžné vydání aplikací](https://support.google.com/googleplay/android-developer/answer/3131213) , budou moci spravovat tyto stopy v Intune. Budete moci selektivně přiřadit obchodní aplikace, které jsou publikovány do předprodukčních běhů Google Play do pilotních skupin, aby bylo možné provádět testování. V Intune také budete moct zjistit, jestli aplikace obsahuje předprodukční záznam testovacího sestavení, který je v něm publikovaný, a taky umožnit přiřazení této stopy ke skupinám uživatelů a zařízení AAD. Tato funkce je k dispozici pro všechny aktuálně podporované podnikové scénáře Androidu (pracovní profil, plně spravované a vyhrazené). V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete přidat spravované aplikace Google Play výběrem možnosti **aplikace** > **Android** > **Přidat**. Další informace najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise pomocí Intune](../apps/apps-add-android-for-work.md).

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Správa nastavení S/MIME pro Outlook v Androidu<!-- 6517085   -->
Zásady konfigurace aplikací budete moct použít ke správě nastavení S/MIME pro Outlook na zařízeních, na kterých běží Android Enterprise. Budete také moci zvolit, zda povolit uživatelům zařízení povolit nebo zakázat nastavení S/MIME v aplikaci Outlook. Pokud chcete použít zásady konfigurace aplikací pro Android, v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) přejít na **aplikace** > **zásady konfigurace aplikací** > **Přidat** > **spravovaná zařízení**.

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Další možnosti v profilech jednotného přihlašování a rozšíření aplikace jednotného přihlašování na zařízeních s iOS/iPadOS<!-- 6504155  -->
Na zařízeních s iOS/iPadOS můžete:

- V části profily jednotného přihlašování (**zařízení** > **konfigurační profily** > **vytvořit profil** > **iOS/iPadOS** pro **funkce zařízení** > pro profil > **jednotné přihlašování**) nastavte hlavní název protokolu Kerberos jako název účtu správce zabezpečení účtů (SAM) v profilech jednotného přihlašování. 
- V profilech rozšíření aplikace jednotného přihlašování (**zařízení** > **konfigurační profily** > **vytvořit profil** > **iOS/iPadOS** pro **funkce zařízení** > pro profil > **rozšíření aplikace jednotného přihlašování**, nakonfigurujte rozšíření iOS/IPADOS Microsoft Azure AD s menším počtem kliknutí pomocí nového typu rozšíření aplikace jednotného přihlašování. Můžete povolit rozšíření Azure AD pro sdílená zařízení a odeslat data specifická pro rozšíření do rozšíření.

Platí pro:
- iOS/iPadOS 13.0 +

Další informace o použití jednotného přihlašování na zařízeních s iOS/iPadOS najdete v tématu [Přehled rozšíření aplikace jednotného přihlašování](../configuration/device-features-configure.md#single-sign-on-app-extension) a [seznam nastavení jednotného přihlašování](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrace zařízení

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Vlastní zařízení můžou používat k nasazení sítě VPN.<!--5015344 -->
Nový profil pro **přeskočení kontroly připojení k doméně** pomocí nového profilu autopilotu přeskočit přepínač umožňuje nasadit hybridní zařízení služby Azure AD join bez přístupu k podnikové síti pomocí vašeho vlastního klienta Win32 VPN od jiného výrobce. Pokud se chcete podívat na nový přepínač, přejděte do [centra pro správu Microsoft Endpoint manageru](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení**  > **Windows** > **windows** > **profily nasazení** > **vytvořit profil** > spouštěné **v počátečním prostředí**.

<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="script-support-for-macos-devices---4280361----"></a>Podpora skriptů pro zařízení macOS<!-- 4280361  -->
Budete moct přidávat a nasazovat skripty pro zařízení macOS. Tato podpora rozšiřuje vaši schopnost nakonfigurovat zařízení macOS nad rámec toho, co je možné na zařízeních macOS využít nativní možnosti MDM.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
Protokoly podrobností o zařízeních v Intune budou dostupné v **Sestavách** > **Log Analytics**. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Nabízené oznámení, když se změní typ vlastnictví zařízení<!-- 5575875  -->
Můžete nakonfigurovat nabízená oznámení, která se budou posílat uživatelům s Androidem i iOS Portál společnosti, když se jejich typ vlastnictví zařízení změní z možnosti osobní na podnik jako na základě ochrany osobních údajů. Toto nastavení najdete v Microsoft Endpoint Manageru tak, že vyberete možnost **Správa tenanta** > **přizpůsobení**. Další informace o tom, jak vlastnictví zařízení ovlivňuje koncové uživatele, najdete v tématu [Změna vlastnictví zařízení](../enrollment/corporate-identifiers-add.md#change-device-ownership).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Zabezpečení

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Podpora odvozených přihlašovacích údajů na zařízeních s Androidem, která plně spravuje<!--4839592-->
V zařízeních s plnou správou pro Android Enterprise budete moct používat odvozená pověření. Podpora bude zahrnovat načítání odvozených přihlašovacích údajů pro Entrust Datacard, Intercede a DISA purebred. U aplikací, které ji podporují, budete moct používat odvozená pověření pro ověřování aplikací, podepisování Wi-Fi, VPN nebo šifrování S/MIME.

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



