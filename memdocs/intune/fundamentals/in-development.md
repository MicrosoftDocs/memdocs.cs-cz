---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764199"
---
# <a name="in-development-for-microsoft-intune"></a>Ve vývoji pro Microsoft Intune

Tato stránka vám umožní v rámci připravenosti a plánování vypsat aktualizace uživatelského rozhraní Intune a funkce, které jsou ve vývoji, ale ještě nejsou vydané. Kromě informací na této stránce: 

- Pokud předpokládáme, že před změnou budete muset provést nějakou akci, zveřejníme doplňkový příspěvek v centru zpráv Office.
- Pokud funkce vstoupí do produkčního prostředí, ať už je verze Preview, nebo je všeobecně dostupná, popis funkce se přesune z této stránky na [co je nového](whats-new.md).
- Tato stránka a stránka [co je nového](whats-new.md) se pravidelně aktualizují. Přijďte se tedy znovu podívat, jestli nejsou k dispozici nové informace.
- Strategické dodávky a časová osa najdete v tématu [Microsoft 365 plán](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) .

> [!NOTE]
> Tato stránka odráží naše aktuální očekávání funkcí Intune v nadcházející verzi. Data a jednotlivé funkce se můžou změnit. Tato stránka nepopisuje všechny funkce vývoje.

**Informační kanál RSS**: Zjistěte, kdy se tato stránka aktualizuje zkopírováním a vložením následující adresy URL do čtečky informačních kanálů:`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Tento článek byl naposledy aktualizován na datum uvedené pod nadpisem výše.**

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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Portál společnosti pro Android budou uživatelům získávat aplikace po registraci pracovního profilu. <!-- 6103999  -->
Vylepšujeme doprovodné materiály k aplikaci v Portál společnosti, aby uživatelé mohli snáze najít a nainstalovat aplikace.  Po registraci v nástroji Správa pracovních profilů se uživatelům zobrazí zpráva s oznámením, že v ní budou moci najít navrhované aplikace v Google Play. Uživatelům se na levé straně Portál společnosti zobrazí také nový odkaz **získat aplikace** . Aby bylo možné tyto nové a vylepšené prostředí vytvořit, karta **aplikace** se odebere. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Nastavení a hodnoty konfiguračního profilu zařízení se aktualizují pro platformy Windows.<!-- 4091122 -->
Když vytváříte profily konfigurace zařízení pro platformy Windows (**Devices**  >  **konfigurační profily**zařízení  >  **vytvořit profil** > jakékoli možnosti **Windows** pro platformu), některá nastavení a jejich hodnoty se liší od CSP a můžou být matoucí. Názvy nastavení a jejich hodnoty se aktualizují tak, aby byly jasné.

To platí pro:

- Profily konfigurace zařízení s Windows 10 a novějšími
- Konfigurační profily zařízení ve Windows Holografick pro firmy
- Windows 8.1 konfigurační profily zařízení
- Profily konfigurace zařízení Windows Phone 8,1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nové nastavení trezoru úložiště pro macOS Endpoint Protection zásady konfigurace zařízení<!-- 5459801   -->
Do kategorie trezoru úložišť přidáváme nové nastavení v rámci šablony [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) : skryjte obnovovací klíč. (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořte profil**, pro danou *platformu* vyberte **MacOS** a pak jako *typ profilu*nastavte **Endpoint Protection** ). Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. Uživatel zařízení si může svůj osobní obnovovací klíč kdykoli zobrazit z aplikace Portál společnosti pro iOS nebo z webu portál společnosti pro šifrované zařízení macOS. Pokud si chcete zobrazit klíč pro osobní obnovení, můžete přejít na podrobnosti o zařízení a kliknout na *získat obnovovací klíč*.

Toto nastavení nebude k dispozici v dříve vytvořených zásadách. Abyste mohli nakonfigurovat toto nastavení tak, aby ho bylo možné používat, budete muset znovu vytvořit zásady trezoru úložišť. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrace zařízení

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Vlastní zařízení můžou používat k nasazení sítě VPN.<!--5015344 -->
Tato funkce může být zpožděná.

### <a name="shared-ipads-for-business--6367326---"></a>Shared iPady for Business<!--6367326 -->
Pomocí Intune a Apple Business Manageru budete moct snadno a bezpečně nastavit sdílený iPad, aby zařízení mohla sdílet víc zaměstnanců. [Sdílený iPad](https://developer.apple.com/education/shared-ipad/) společnosti Apple nabízí individuální prostředí pro více uživatelů při zachování uživatelských dat. Pomocí spravovaného Apple ID můžou uživatelé získat přístup k aplikacím, datům a nastavením po přihlášení ke všem sdíleným iPadům v jejich organizaci. Sdílený iPad spolupracuje se federované identity.

Tuto funkci zobrazíte tak, že přejdete do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**.  >  **iOS**  >  **iOS enrollment**  >  **tokeny programu registrace** iOS > vyberte token * * > **profily**  >  **vytvořit profil**  >  **iOS**. Na stránce **Nastavení správy** vyberte **zaregistrovat bez přidružení uživatele** a zobrazí se možnost **sdílené iPady** .

**Platí pro:** iPadOS 13,4 a novější. Tato verze přidala podporu pro dočasné relace se sdíleným iPadem, takže uživatelé budou mít přístup k zařízení bez spravovaného Apple ID. Po odhlášení zařízení vymaže všechna uživatelská data, aby bylo zařízení hned připravené k použití, což eliminuje nutnost vymazání zařízení. 

<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
V **sestavách**  >  **Log Analytics**budou k dispozici protokoly podrobností o zařízeních v Intune. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.


<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Šablona sestavy dodržování předpisů Power BI V 2.0<!-- 636958  -->
Správci budou moct aktualizovat verzi šablony zprávy o kompatibilitě Power BI z verze 1.0 až verze 2.0. Verze 2.0 bude obsahovat vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Související informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Zabezpečení


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplikace zásad v Endpoint Security<!-- 5892558   -->
Budete moct vybrat zásadu, kterou jste vytvořili v uzlu zabezpečení koncového bodu v centru pro správu Microsoft Endpoint Manageru, a pak ji duplikovat a vytvořit kopii.  Zásady, které budete moci duplikovat, zahrnují ty, které vytvoříte pro: 

- Antivirus
- Šifrování disků
- Firewall
- Zjišťování koncových bodů a odpověď
- Omezení možností útoku
- Ochrana účtu

Duplikace provede kopii původní zásady, kterou pak můžete přejmenovat a upravit. Kopie nebude zahrnovat přiřazení původní.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nový profil pro zásady brány firewall zabezpečení koncového bodu<!-- 5653324   -->
Ve verzi Preview přidáváme další profil pro Windows 10 a novější zásady brány firewall v zabezpečení koncového bodu služby Intune (**Endpoint Security**  >  **firewall**  >  **Create Policy** > vyberte **Windows 10 a novější**). 

Každá instance tohoto nového profilu podporuje až 150 vlastních *pravidel firewallu v programu Microsoft Defender*. Profil pravidla firewallu v programu Microsoft Defender umožňuje definovat podrobná pravidla brány Windows Firewall pro povolení nebo blokování portů a aplikací ve Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).



