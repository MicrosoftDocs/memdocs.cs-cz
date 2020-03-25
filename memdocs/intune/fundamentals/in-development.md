---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220128"
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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Portál společnosti pro iOS pro podporu režimu na šířku<!--6048329  -->
Uživatelé budou moct zaregistrovat svoje zařízení, Hledat aplikace a získat podporu na základě orientace obrazovky podle jejich výběru. Aplikace bude automaticky rozpoznávat a upravovat obrazovky, aby odpovídaly režimu na výšku nebo na šířku, pokud uživatelé nezamkne obrazovku v režimu na výšku.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Vylepšené prostředí pro přihlašování v Portál společnosti pro Android<!-- 6103997  -->
Aktualizujeme rozložení několika přihlašovacích obrazovek v aplikaci Portál společnosti pro Android, aby bylo prostředí pro uživatele užitečnější, jednoduché a čisté.

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

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Vylepšené uživatelské rozhraní při vytváření OEMConfig konfigurací profilů na zařízeních s Androidem Enterprise<!-- 5568645   -->
Když vytváříte nebo upravujete profil OEMConfig pro zařízení s Androidem Enterprise, bude se aktualizovat prostředí v centru pro správu správy koncových bodů. Aktualizované prostředí vám poskytne přehled o nastaveních, která jste nakonfigurovali na první pohled. Tato změna má vliv na konfigurační profil zařízení OEMConfig (**zařízení** > **konfiguračních profilů** > **vytvořit profil** > **Android Enterprise** for Platform > **OEMConfig** pro typ profilu).

Tato funkce platí pro:
- Android Enterprise 

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

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurace aplikace Microsoft Defender ATP pro macOS  <!-- 5520115  -->
Brzy budete moct nakonfigurovat [Nastavení](../protect/endpoint-protection-macos.md) pro aplikaci Microsoft Defender ATP pro zařízení, která používají MacOS jako součást konfiguračního profilu zařízení ochrany koncových bodů (**zařízení** > **konfiguračních** profilech > **vytvořit profil**, vyberte pro *platformu* **MacOS** a pak jako *typ profilu* **Endpoint Protection** ). Pro konfiguraci zařízení macOS bude k dispozici osm nastavení. 

Ochrana ATP v programu Defender je podporovaná na macOS 10,13 (s vysokou verzí Sierra) a novějších a aplikace [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) musí být *po* těchto nastaveních nasazená do zařízení. Nastavení byste měli před nasazením aplikace poslat do zařízení. Beta verze macOS se nepodporují.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nové nastavení trezoru úložiště pro macOS Endpoint Protection zásady konfigurace zařízení<!-- 5459801   -->
Do kategorie trezoru úložišť přidáváme nové nastavení v rámci šablony [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) : skryjte obnovovací klíč. (**Zařízení** > **konfiguračních profilů** > **vytvořit profil**vyberte pro *platformu* **MacOS** a pak jako *typ profilu*nastavte **Endpoint Protection** ). Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. Uživatel zařízení si může svůj osobní obnovovací klíč kdykoli zobrazit z aplikace Portál společnosti pro iOS nebo z webu portál společnosti pro šifrované zařízení macOS. Pokud si chcete zobrazit klíč pro osobní obnovení, můžete přejít na podrobnosti o zařízení a kliknout na *získat obnovovací klíč*.

Toto nastavení nebude k dispozici v dříve vytvořených zásadách. Abyste mohli nakonfigurovat toto nastavení tak, aby ho bylo možné používat, budete muset znovu vytvořit zásady trezoru úložišť. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Konfigurovat agenta Optimalizace doručení při stahování obsahu aplikace Win32<!-- 5410945  -->
Agent pro optimalizaci doručení budete moct nakonfigurovat tak, aby stahoval obsah aplikace Win32 buď v režimu pozadí, nebo v režimu popředí na základě přiřazení. U stávajících aplikací Win32 bude obsah dál stahovat v režimu pozadí. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **všechny aplikace** > *Vyberte vlastnosti aplikace Win32* > **Properties**. V poli **přiřazení**vyberte **Upravit** .  Upravte přiřazení výběrem možnosti **Zahrnout** do **režimu** v **požadované** části.  V části **nastavení aplikace** najdete nové nastavení, když bude k dispozici. Další informace o optimalizaci doručení najdete v tématu [Správa aplikací Win32 – Optimalizace doručení](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Změna primárního uživatele pro zařízení s Windows <!-- 3794742 -->
Můžete změnit primárního uživatele pro zařízení s Windows Hybrid a připojená k Azure AD. Provedete to tak, že přejdete na **zařízení** > **Intune** > **všechna zařízení** > vyberte zařízení > **vlastnosti** > **primární uživatel**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="new-information-in-device-details---5604099---"></a>Podrobnosti o nových informacích o zařízení<!-- 5604099 -->
Na stránce **Přehled** pro zařízení se zobrazí následující informace:

- Kapacita úložiště (množství fyzického úložiště v zařízení)
- Kapacita paměti (množství fyzické paměti v zařízení)

### <a name="script-support-for-macos-devices---4280361----"></a>Podpora skriptů pro zařízení macOS<!-- 4280361  -->
Budete moct přidávat a nasazovat skripty pro zařízení macOS. Tato podpora rozšiřuje vaši schopnost nakonfigurovat zařízení macOS nad rámec toho, co je možné na zařízeních macOS využít nativní možnosti MDM.

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
