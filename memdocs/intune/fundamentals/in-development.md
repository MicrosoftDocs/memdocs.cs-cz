---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0098ff8f7916dd08b32fbc4acc9289a403a860ef
ms.sourcegitcommit: d1c7548b4177d720065b822356f9a08d1e1657c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82881056"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Podpora pro více účtů v Portál společnosti pro Mac<!-- 5779449  -->
Portál společnosti v zařízeních macOS nyní ukládá do mezipaměti uživatelské účty a usnadňuje tak přihlašování. Uživatelé už se nemusí přihlašovat k Portál společnosti při každém spuštění aplikace. Kromě toho Portál společnosti zobrazí výběr účtu, pokud jsou do mezipaměti více uživatelských účtů, aby uživatelé nemuseli zadávat své uživatelské jméno. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Automaticky aktualizovat dostupné aplikace VPP<!-- 3640511  -->
Aplikace, které se publikují jako dostupné aplikace programu Volume purchase program (VPP), se automaticky aktualizují, pokud je pro token VPP povolená **Automatická aktualizace aplikací** . Aktuálně dostupné aplikace VPP se neaktualizují automaticky. Místo toho musí koncoví uživatelé přejít na Portál společnosti a znovu nainstalovat aplikaci, pokud je k dispozici novější verze. Požadované aplikace ale v současné době podporují automatické aktualizace.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Přizpůsobení akcí zařízení samoobslužných služeb v Portál společnosti<!--4393379  -->
Budete moct přizpůsobit dostupné akce samoobslužného zařízení, které se zobrazí koncovým uživatelům v aplikaci Portál společnosti a na webu. Aby se zabránilo nezamýšleným akcím zařízení, můžete nakonfigurovat tato nastavení pro aplikaci Portál společnosti, a to tak, že vyberete možnost**přizpůsobení** >  **správy** > tenanta**vytvořit** > **Skrýt funkce**. K dispozici jsou následující akce:
- Skrýt tlačítko **Odebrat** na podnikovém zařízení s Windows
- Skrýt tlačítko pro **obnovení** na podnikových zařízeních s Windows
- Skrýt tlačítko pro **obnovení** na podnikových zařízeních iOS.
- Skrýt tlačítko **Odebrat** na podnikových zařízeních iOS.

Další informace najdete v tématu [Akce zařízení Samoobslužná služba z portál společnosti](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Jednotné doručování aplikací Azure AD Enterprise nebo Office Online v Portál společnosti<!--4404429 -->
Zobrazení aplikací Azure AD Enterprise nebo Office Online v Portál společnosti budete moct přepínat (**skrývat** nebo **zobrazovat**). Každý uživatel uvidí ze zvolené služby Microsoftu celý katalog aplikací. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. Tato funkce se nejprve projeví na Portál společnosti webu ve verzi 2005 s podporou na portálech Windows, iOS/iPadOS a macOS společnosti, které by měly dodržovat. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte**přizpůsobení** **správy** > tenanta a najděte toto budoucí nastavení. Související informace najdete v tématu [Postup přizpůsobení aplikací portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Hledání v dokumentaci k Intune z Portál společnosti<!-- 1736480 -->
V dokumentaci k Intune teď můžete vyhledávat přímo z Portál společnosti aplikace pro macOS. V řádku nabídek vyberte**vyhledávání** v **nápovědě** > a zadejte klíčová slova hledání, abyste mohli rychle najít odpovědi na své otázky.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Portál společnosti pro Android budou uživatelům získávat aplikace po registraci pracovního profilu. <!-- 6103999  -->
Vylepšujeme doprovodné materiály k aplikaci v Portál společnosti, aby uživatelé mohli snáze najít a nainstalovat aplikace.  Po registraci v nástroji Správa pracovních profilů se uživatelům zobrazí zpráva s oznámením, že v ní budou moci najít navrhované aplikace v Google Play. Uživatelům se na levé straně Portál společnosti zobrazí také nový odkaz **získat aplikace** . Aby bylo možné tyto nové a vylepšené prostředí vytvořit, karta **aplikace** se odebere. 

### <a name="android-company-portal-user-experience---5736084---"></a>Uživatelské prostředí pro Android Portál společnosti<!-- 5736084 -->
Ve vydání 2005 Portál společnosti Androidu se koncovým uživatelům zařízení s Androidem, kteří mají v zásadách ochrany aplikací vystavili upozornění, zablokování nebo vymazání, se zobrazí nové uživatelské prostředí. Místo aktuálního prostředí dialogu se koncovým uživatelům zobrazí celá stránka popisující důvod upozornění, blokování nebo vymazání a postup, jak problém vyřešit. Další informace najdete v tématu [prostředí ochrany aplikací pro zařízení s Androidem](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) a [nastavení zásad ochrany aplikací pro Android v Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Nastavení a hodnoty konfiguračního profilu zařízení se aktualizují pro platformy Windows.<!-- 4091122 -->
Když vytváříte profily konfigurace zařízení pro platformy Windows (**Devices** > **konfigurační profily** > zařízení**vytvořit profil** > jakékoli možnosti **Windows** pro platformu), některá nastavení a jejich hodnoty se liší od CSP a můžou být matoucí. Názvy nastavení a jejich hodnoty se aktualizují tak, aby byly jasné.

To platí pro:

- Profily konfigurace zařízení s Windows 10 a novějšími
- Konfigurační profily zařízení ve Windows Holografick pro firmy
- Windows 8.1 konfigurační profily zařízení
- Profily konfigurace zařízení Windows Phone 8,1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurace aplikace Microsoft Defender ATP pro macOS  <!-- 5520115  -->
Brzy budete moct nakonfigurovat [Nastavení](../protect/endpoint-protection-macos.md) pro aplikaci Microsoft Defender ATP pro zařízení, která používají MacOS jako součást konfiguračního profilu zařízení Endpoint Protection (konfigurace**zařízení** > **profily** > **vytvořit profil**, vyberte **MacOS** pro *platformu*a pak **Endpoint Protection** pro *typ profilu*). Pro konfiguraci zařízení macOS bude k dispozici osm nastavení. 

Ochrana ATP v programu Defender je podporovaná na macOS 10,13 (s vysokou verzí Sierra) a novějších a aplikace [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) musí být *po* těchto nastaveních nasazená do zařízení. Nastavení byste měli před nasazením aplikace poslat do zařízení. Beta verze macOS se nepodporují.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nové nastavení trezoru úložiště pro macOS Endpoint Protection zásady konfigurace zařízení<!-- 5459801   -->
Do kategorie trezoru úložišť přidáváme nové nastavení v rámci šablony [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) : skryjte obnovovací klíč. (Konfigurace**zařízení** > **profily** > **vytvořit profil**, pro danou *platformu* vyberte **MacOS** a pak jako *typ profilu*nastavte **Endpoint Protection** ). Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. Uživatel zařízení si může svůj osobní obnovovací klíč kdykoli zobrazit z aplikace Portál společnosti pro iOS nebo z webu portál společnosti pro šifrované zařízení macOS. Pokud si chcete zobrazit klíč pro osobní obnovení, můžete přejít na podrobnosti o zařízení a kliknout na *získat obnovovací klíč*.

Toto nastavení nebude k dispozici v dříve vytvořených zásadách. Abyste mohli nakonfigurovat toto nastavení tak, aby ho bylo možné používat, budete muset znovu vytvořit zásady trezoru úložišť. 

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Konfigurace systémových rozšíření na zařízeních macOS<!-- 6255624  -->
Na zařízeních MacOS můžete vytvořit profil rozšíření jádra pro konfiguraci nastavení na úrovni jádra (**konfigurační profily** > **zařízení** > **MacOS** pro **rozšíření jádra** > platformy pro profil). Apple je nakonec zastaralá rozšíření jádra a v budoucí verzi je nahrazuje rozšířeními systému. Rozšíření systému běží v uživatelském prostoru a neposkytují přístup k jádru. Cílem je zvýšit zabezpečení a poskytnout více koncovým uživatelským ovládacím prvkům a omezit tak útoky na úrovni jádra. Rozšíření jádra i systémová rozšíření umožňují uživatelům instalovat rozšíření aplikací, která rozšiřuje nativní možnosti operačního systému.

V Intune můžete nakonfigurovat rozšíření jádra i systémová rozšíření (**konfigurační profily** > **zařízení** > **MacOS** pro rozšíření Platform > **System** pro profil). Rozšíření jádra se vztahují na 10.13.2 a novější. Systémová rozšíření se vztahují na 10,15 a novější. V macOS 10,15 až macOS 10.15.4 mohou běžet rozšíření jádra a systémová rozšíření vedle sebe. 

Další informace o rozšíření jádra na zařízeních macOS najdete v tématu [Přidání rozšíření jádra MacOS](../configuration/kernel-extensions-overview-macos.md).

To platí pro:
- macOS 10,15 a novější

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrace zařízení

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Vlastní zařízení můžou používat k nasazení sítě VPN.<!--5015344 -->
Tato funkce může být zpožděná.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Automatický interval synchronizace zařízení je mimo 12 hodin.<!--3077535 -->
V případě automatizované registrace zařízení od společnosti Apple se interval automatizované synchronizace zařízení mezi Intune a Apple Business Managerem zkrátí z 24 hodin na 12 hodin. Další informace o synchronizaci najdete v tématu [synchronizace spravovaných zařízení](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Podpora autopilotu pro zařízení HoloLens 2<!--6305220-->
Windows autopilot bude podporovat zařízení HoloLens 2. Další informace o použití modulu Autopilot v Intune najdete v tématu [registrace zařízení s Windows v Intune pomocí automatických pilotů Windows](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Omezení registrace budou podporovat značky oboru<!--4209550 -->
K omezením registrace budete moct přiřadit značky oboru. Provedete to tak, že přejdete do centra**pro** >  >  [správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)**omezení** > registrace**vytvořit omezení**. Vytvořte buď typ omezení, a zobrazí se stránka **značky oboru** .

### <a name="shared-ipads-for-business--6367326---"></a>Shared iPady for Business<!--6367326 -->
Pomocí Intune a Apple Business Manageru budete moct snadno a bezpečně nastavit sdílený iPad, aby zařízení mohla sdílet víc zaměstnanců. [Sdílený iPad](https://developer.apple.com/education/shared-ipad/) společnosti Apple nabízí individuální prostředí pro více uživatelů při zachování uživatelských dat. Pomocí spravovaného Apple ID můžou uživatelé získat přístup k aplikacím, datům a nastavením po přihlášení ke všem sdíleným iPadům v jejich organizaci. Sdílený iPad spolupracuje se federované identity.

Tuto funkci zobrazíte tak, že přejdete do centra**pro** >  >  [správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)**zařízení** > **iOS** > .**tokeny programu registrace** iOS > vyberte token * * > **profily** > **vytvořit profil** > **iOS**. Na stránce **Nastavení správy** vyberte **zaregistrovat bez přidružení uživatele** a zobrazí se možnost **sdílené iPady** .

**Platí pro:** iPadOS 13,4 a novější. Tato verze přidala podporu pro dočasné relace se sdíleným iPadem, takže uživatelé budou mít přístup k zařízení bez spravovaného Apple ID. Po odhlášení zařízení vymaže všechna uživatelská data, aby bylo zařízení hned připravené k použití, což eliminuje nutnost vymazání zařízení. 

<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
V **sestavách** > **Log Analytics**budou k dispozici protokoly podrobností o zařízeních v Intune. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.

### <a name="new-details-for-the-autopilot-report--5405786---"></a>Nové podrobnosti pro sestavu autopilot<!--5405786 -->
Chcete-li zobrazit nové podrobnosti o stavu instalace aplikací a zásad, přejděte do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte **zařízení** > **monitorování** > **nasazení autopilotu**.

### <a name="macos-script-support---6376978----"></a>Podpora skriptů macOS<!-- 6376978  -->
Podpora skriptů pro macOS je teď všeobecně dostupná. Kromě toho budeme přidávat podporu pro skripty přiřazené uživateli i pro zařízení macOS, která byla zaregistrovaná pomocí automatizované registrace zařízení společnosti Apple (dříve Program registrace zařízení). Další informace najdete v tématu [použití skriptů prostředí v zařízeních MacOS v Intune](../apps/macos-shell-scripts.md).

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

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Podpora odvozených přihlašovacích údajů pro DISA purebred na zařízeních s Androidem<!--4839592 -->
*DISA purebred* budete moct používat jako [odvozeného poskytovatele přihlašovacích údajů](../protect/derived-credentials.md) u plně spravovaných zařízení s Androidem Enterprise (konektory**pro správu** > tenanta a**přihlašovací údaje odvozené**od**tokenů** > ). Podpora bude zahrnovat načtení odvozeného pověření pro DISA purebred. U aplikací, které ji podporují, budete moct používat odvozená pověření pro ověřování aplikací, podepisování Wi-Fi, VPN nebo šifrování S/MIME. 

V dubnu přidala Intune podporu pro *Entrust Datacard* a *Intercede* jako poskytovatele pro odvozená pověření. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Nastavení předvoleb ochrany osobních údajů pro zařízení macOS<!-- 2934232 --> 
S vydáním verze macOS Catalina 10,15 Společnost Apple přidala nové vylepšení zabezpečení a ochrany osobních údajů. Ve výchozím nastavení nemůžou aplikace a procesy získat přístup k určitým datům bez souhlasu uživatele. Pokud uživatelé neposkytnou souhlas, aplikace a procesy nemusí fungovat. Intune přidává podporu pro nastavení, která správcům IT umožní povolit nebo zakázat souhlas s přístupem k datům jménem koncových uživatelů na zařízeních s macOS 10,14 a novějším. Tato nastavení zajistí, že aplikace a procesy budou nadále fungovat správně a omezují počet výzev, které koncoví uživatelé zaznamenají.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplikace zásad v Endpoint Security<!-- 5892558   -->
Budete moct vybrat zásadu, kterou jste vytvořili v uzlu zabezpečení koncového bodu v centru pro správu Microsoft Endpoint Manageru, a pak ji duplikovat a vytvořit kopii.  Zásady, které budete moci duplikovat, zahrnují ty, které vytvoříte pro: 

- Antivirus
- Šifrování disku
- Brána firewall
- Zjištění a odpověď koncového bodu
- Omezení možností útoku
- Ochrana účtu

Duplikace provede kopii původní zásady, kterou pak můžete přejmenovat a upravit. Kopie nebude zahrnovat přiřazení původní.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Odeslání nabízených oznámení jako akce při nedodržení předpisů <!-- 1733150   -->
V případě platforem iOS a Android přidáváme novou akci při nedodržení předpisů, která odešle nabízené oznámení aplikace v aplikaci Portál společnosti. Uživatelé můžou kliknout na oznámení, která spustí aplikaci Portál společnosti, která pak zobrazí důvod, proč nedodržují předpisy. Správci budou moct tuto novou akci nakonfigurovat pro nedodržování předpisů v centru pro správu Microsoft Endpoint Manageru tak, že přejdete na **zařízení** > **zásady** > dodržování předpisů**vytvořit zásadu**a pak vyberte *akci* pro odeslání nabízeného oznámení aplikace. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nový profil pro zásady brány firewall zabezpečení koncového bodu<!-- 5653324   -->
Ve verzi Preview přidáváme další profil pro Windows 10 a novější zásady brány firewall v zabezpečení koncového bodu služby Intune (**Endpoint Security** > **firewall** > **Create Policy** > vyberte **Windows 10 a novější**). 

Každá instance tohoto nového profilu podporuje až 150 vlastních *pravidel firewallu v programu Microsoft Defender*. Profil pravidla firewallu v programu Microsoft Defender umožňuje definovat podrobná pravidla brány Windows Firewall pro povolení nebo blokování portů a aplikací ve Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).



