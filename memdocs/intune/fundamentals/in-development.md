---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b7f1a4280b409ec4a12c6371fd2e6cba8a571ca
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048017"
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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Aktualizace ikon zařízení v Portál společnosti a aplikacích Intune v Androidu<!-- 6057023  -->
Aktualizujeme ikony zařízení v aplikacích Portál společnosti a Intune na zařízeních s Androidem, abyste vytvořili pokročilejší vzhled a atmosféru a mohli se přizpůsobit k systému Microsoft Fluent design. Související informace najdete v tématu [aktualizace ikon v aplikaci Portál společnosti App pro iOS/iPadOS a MacOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Portál společnosti bude podporovat automatické registrace zařízení společnosti Apple bez přidružení uživatele.<!-- 7282707  --> 
v zařízeních zaregistrovaných pomocí automatizované registrace zařízení společnosti Apple se bude podporovat iOS Portál společnosti, aniž by museli přiřazeného uživatele. Koncový uživatel se může přihlásit k Portál společnosti iOS, aby se sám navázal jako primární uživatel na zařízení se systémem iOS/iPadOS, které je zaregistrované bez spřažení zařízení. Další informace o automatizované registraci zařízení najdete v tématu [Automatická registrace zařízení s iOS/iPadOS pomocí automatizované registrace zařízení společnosti Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Windows Portál společnosti přidává podporu aplikací Configuration Manager<!-- 4297660 -->
Windows Portál společnosti teď podporuje Configuration Manager aplikace. Tato funkce umožňuje koncovým uživatelům zobrazit Configuration Manager i nasazené aplikace Intune v Portál společnosti Windows pro spoluspravované zákazníky. Tato podpora pomůže správcům konsolidovat různé prostředí portálu pro koncové uživatele. Další informace najdete v tématu [použití portál společnosti aplikace na spoluspravovaných zařízeních](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Nastavit stav dodržování předpisů zařízením od partnerů MDM třetích stran<!-- 6361689   -->
Microsoft 365 zákazníci, kteří vlastní řešení MDM třetí strany, budou moci vyhovět zásadám podmíněného přístupu pro aplikace Microsoft 365 v iOS a Androidu prostřednictvím integrace se službou Microsoft Intune dodržování předpisů zařízením. Dodavatel MDM třetí strany bude využívat službu Intune pro dodržování předpisů zařízením k odesílání dat o dodržování předpisů zařízením do Intune. Intune se pak vyhodnotí a určí, jestli je zařízení důvěryhodné, a nastavte atributy podmíněného přístupu ve službě Azure AD.  Zákazníci budou muset nastavit zásady podmíněného přístupu Azure AD z centra pro správu Microsoft Endpoint Manageru nebo z portálu Azure AD.

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Vytvoření profilů certifikátů PKCS pro plně spravovaná zařízení s Androidem Enterprise (COBO)<!-- 4839686 -->
Profily certifikátů PKCS můžete vytvořit k nasazení certifikátů na zařízení s vlastníkem zařízení s Androidem Enterprise a pracovním profilem (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil pro**  >  **Android Enterprise > pouze vlastník zařízení**), nebo **Android Enterprise > Work Profile pouze** pro platformu > **PKCS** pro profil).

Brzy budete moct vytvořit profily certifikátů PKCS pro zařízení s plnou správou v Androidu Enterprise. Je vyžadován konektor certifikátu PFX Intune. Pokud protokol SCEP nepoužíváte a používáte jenom PKCS, můžete konektor NDES odebrat po instalaci nového konektoru PFX. Nový konektor PFX importuje soubory PFX a nasadí certifikáty PKCS na všechny platformy.

Další informace o certifikátech PKCS najdete v tématu [Konfigurace a používání certifikátů PKCS pomocí Intune](../protect/certficates-pfx-configure.md).

Platí pro:
- Android Enterprise Full Managed (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>Použití NetMotion jako typu připojení VPN pro zařízení s iOS/iPadOS a macOS<!-- 1333631 -->
Když vytváříte profil sítě VPN, NetMotion je k dispozici jako typ připojení VPN (**zařízení**  >  **Konfigurace zařízení**  >  **vytvořit profil**  >  **iOS/iPadOS** nebo **MacOS** pro Platform > **VPN** pro > pro typ připojení **NetMotion** ).

Další informace o profilech sítě VPN v Intune najdete v tématu [Vytvoření profilů sítě VPN pro připojení k SERVERŮM VPN](../configuration/vpn-settings-configure.md).

Platí pro:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Další možnosti protokolu PEAP (Protected Extensible Authentication Protocol) pro profily sítě Wi-Fi s Windows 10<!-- 3805024 -->
Na zařízeních s Windows 10 můžete vytvořit profily Wi-Fi pomocí protokolu EAP (Extensible Authentication Protocol) k ověřování připojení Wi-Fi (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Windows 10 a novější** pro platformu > **Wi-Fi** pro > **Enterprise**). Když vyberete protokol PEAP (Protected EAP), jsou k dispozici nová nastavení:

- **Provést ověření serveru ve fázi protokolu PEAP 1**: ve fázi vyjednávání protokolu PEAP 1, zařízení ověřují certifikát a ověřují server.
  - **Zakázání výzev uživatele při ověřování serveru v protokolu PEAP fáze 1**: ve fázi vyjednávání protokolu PEAP 1 se nezobrazí výzvy uživatele s výzvou k autorizaci nových serverů protokolu PEAP pro důvěryhodné certifikační autority.
- **Vyžadovat kryptografickou vazbu**: zabraňuje připojením k serverům PEAP, které nepoužívají kryptografickou vazbu během vyjednávání protokolu PEAP.

Pokud se chcete podívat na nastavení, která můžete konfigurovat, přejděte na [Přidat nastavení Wi-Fi pro zařízení s Windows 10 a novějším](../configuration/wi-fi-settings-windows.md).

Platí pro: 
- Windows 10 a novější

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>Konfigurace modulu plug-in macOS Microsoft Enterprise SSO<!-- 5627576 -->
Tým Microsoft Azure AD vytvořil rozšíření aplikace jednotného přihlašování (SSO) pro přesměrování, které macOS uživatelům 10.15 + + umožňuje získat přístup k aplikacím, organizacím a webům Microsoftu, které podporují funkci jednotného přihlašování a ověřování pomocí Azure AD, s jedním přihlašováním. Ve verzi modulu plug-in Microsoft Enterprise SSO můžete nakonfigurovat rozšíření jednotného přihlašování pomocí nového typu rozšíření aplikace Microsoft Azure AD (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **MacOS** pro **funkce** platformy > zařízení pro profil > typ rozšíření **aplikace jednotného přihlašování** > > **Microsoft Azure AD**).

K zajištění jednotného přihlašování s typem rozšíření aplikace Microsoft Azure AD jednotného přihlašování musí uživatelé na svých zařízeních s macOS instalovat aplikaci Portál společnosti a přihlásit se k ní. 

Další informace o rozšířeních aplikace macOS SSO najdete v tématu [rozšíření aplikace jednotného přihlašování](../configuration/device-features-configure.md#single-sign-on-app-extension).

Platí pro:
- macOS 10,15 a novější

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>Použití rozšíření aplikace jednotného přihlašování na dalších aplikacích pro iOS/iPadOS s modulem plug-in Microsoft Enterprise SSO<!-- 7369991 -->
[Modul plug-in Microsoft Enterprise SSO pro zařízení Apple](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) se dá použít se všemi aplikacemi, které podporují rozšíření aplikace jednotného přihlašování. Tato funkce v Intune znamená, že modul plug-in funguje s mobilními aplikacemi pro iOS/iPadOS, které nepoužívají knihovnu Microsoft Authentication Library (MSAL) pro zařízení Apple. Aplikace nepotřebují používat MSAL, ale je potřeba je ověřit pomocí koncových bodů Azure AD.

Pokud chcete nakonfigurovat aplikace pro iOS/iPadOS, aby používaly jednotné přihlašování s modulem plug-in, přidejte identifikátory sady prostředků aplikace do konfiguračního profilu iOS/iPadOS (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro **funkce** platformy > zařízení pro profil > **rozšíření aplikace jednotného přihlašování**  >  **Microsoft Azure AD** pro typ rozšíření aplikace jednotného přihlašování > **identifikátory sady prostředků aplikace**).

Pokud chcete zobrazit aktuální nastavení rozšíření aplikace jednotného přihlašování, můžete nakonfigurovat, přejít na [rozšíření aplikace s jednotným přihlašováním](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Platí pro:
- iOS/iPadOS

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
V **sestavách**  >  **Log Analytics**budou k dispozici protokoly podrobností o zařízeních v Intune. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Připojení tenanta: časová osa zařízení v centru pro správu<!--7220536, CM7141381 -->
Když Configuration Manager synchronizuje zařízení s Microsoft Endpoint Managerem prostřednictvím připojení tenanta, budete moct zobrazit časovou osu událostí. Tato časová osa zobrazuje minulou aktivitu v zařízení, která vám může pomoct při řešení problémů. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Připojení tenanta: instalace aplikace z centra pro správu<!-- 7220536, CM6024389 -->
Instalaci aplikace můžete zahájit v reálném čase pro zařízení připojené k tenantovi z centra pro správu služby Microsoft Endpoint Management. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Připojení tenanta: CMPivot z centra pro správu<!--7220536, CM6024392 -->
Budete moct využít sílu [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) do centra pro správu Microsoft Endpoint Manageru. Umožněte dalším osoby, jako je helpdesk, aby bylo možné iniciovat dotazy v reálném čase z cloudu proti jednotlivým zařízením spravovaným nástrojem ConfigMgr a vracet výsledky zpátky do centra pro správu. To poskytuje všechny tradiční výhody CMPivot, které správcům IT a dalším určeným osoby schopnost rychle vyhodnotit stav zařízení ve svém prostředí a provést akci. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Připojení tenanta: spuštění skriptů z centra pro správu<!--7220536, CM6234688 -->
Do centra pro správu služby Microsoft Endpoint Manager budete moct využít sílu Configuration Manager funkce místního [spouštění skriptů](../../configmgr/apps/deploy-use/create-deploy-scripts.md) . Povolí další osoby, jako je helpdesk, aby se spouštěly skripty PowerShellu z cloudu proti jednotlivým Configuration Manager spravovaným zařízením. To poskytuje všechny tradiční výhody skriptů PowerShellu, které již byly definovány a schváleny správcem Configuration Manager k tomuto novému prostředí. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Nasazení aktualizací softwaru do zařízení macOS <!-- 3194876 -->
Aktualizace softwaru budete moct nasadit do skupin zařízení macOS. Tato funkce zahrnuje kritické, firmware, konfigurační soubor a další aktualizace. V příští registraci zařízení budete moct odesílat aktualizace, nebo můžete vybrat týdenní plán pro nasazení aktualizací do nebo z časového intervalu, který jste nastavili. To pomáhá při aktualizaci zařízení mimo standardní pracovní dobu nebo v případě, že je vaše Helpdesk plně přiřazená. Zobrazí se vám také podrobná sestava všech zařízení macOS s nasazenými aktualizacemi. Pokud chcete zobrazit stav konkrétních aktualizací, můžete přejít k sestavě podle jednotlivých zařízení.

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Přidružené licence se odvolaly před odstraněním tokenu Apple VPP.<!--6195322 -->
Při budoucí aktualizaci se při odstranění tokenu Apple VPP ve službě Microsoft Endpoint Manager automaticky odvolají všechny licence přiřazené pro Intune, které jsou přidružené k tomuto tokenu.

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

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Podpora zásad ochrany aplikací pro Symantec Endpoint Security a Check Point Sandblast<!--  4452423, 4731168 -->

V říjnu 2019 zásady ochrany aplikací Intune přidaly možnost používat data z některých našich partnerů ochrany před internetovými útoky (MTD partneři Microsoftu). Přidáváme podporu pro následující partnery, aby bylo možné použít zásady ochrany aplikací k blokování nebo selektivnímu vymazání podnikových dat uživatele na základě stavu zařízení:

- **Check Point Sandblast** v Androidu, iOS a iPadOS
- **Symantec Endpoint Security** na Androidu, iOS a iPadOS

Informace o používání zásad ochrany aplikací s partnery MTD najdete v tématu [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami v Intune](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Služba Microsoft Defender ATP vytvoří úlohu zabezpečení správce koncových bodů s podrobnostmi o ohrožení zabezpečení.<!-- 5568193  -->
Správa hrozeb a ohrožení zabezpečení (TVM) v modulu Microsoft Defender ATP zjišťuje v zařízeních nesprávně nakonfigurovaná nastavení zabezpečení. Správci používají tyto informace k aktualizaci ohrožených zařízení.

V brzké době může ochrana ATP v programu Microsoft Defender vyvolat úlohu zabezpečení správce koncových bodů (úlohy Security**Manager**  >  **Endpoint**Security  >  **Security**) s podrobnostmi o ohrožení zabezpečení a zobrazit postižená zařízení. Správci IT můžou přijmout úlohu zabezpečení a nasadit požadovanou konfiguraci. 

Další informace o úlohách zabezpečení najdete v tématu [použití Intune k nápravě ohrožení zabezpečení identifikovaných v Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>Změny vyloučení zásad antivirové ochrany Endpoint Security<!--5583940, 6018119  -->
Zavádíme dvě změny pro správu seznamů vyloučení antivirové ochrany v programu Microsoft Defender, které nakonfigurujete v rámci zásad ochrany koncových bodů zabezpečení koncového bodu. (**Zabezpečení**  >  koncového bodu **Antivirová ochrana**  >  **Vytvořit zásadu**  >  **Windows 10 a novější** pro platformu). Tyto dvě změny zabraňují konfliktům mezi zásadami a stávající zásady, které byly v konfliktu, již nebudou v konfliktu se seznamem vyloučení:

- Nejdřív přidáváme nový typ profilu pro Windows 10 a novější. **Vyloučení antivirové ochrany v programu Microsoft Defender**.  Tento nový typ profilu obsahuje jenom nastavení pro určení seznamu *procesů*Defenderu, *přípon souborů*a *souborů* a *složek* , které nechcete v programu Microsoft Defender kontrolovat. To vám může usnadnit správu seznamů vyloučení jejich oddělením od jiných konfigurací zásad.
- Druhá změna znamená, že seznam vyloučení definovaných v různých profilech se sloučí do jednoho seznamu vyloučení pro každé zařízení nebo uživatele, a to na základě jednotlivých zásad, které se vztahují na konkrétního uživatele nebo zařízení. Například když cílíte na uživatele se třemi oddělenými zásadami, seznamy vyloučení z těchto tří zásad se sloučí do jedné nadmnožiny vyloučení antivirové ochrany v programu Microsoft Defender, které se pak aplikují na uživatele. Toto sloučení zahrnuje seznamy vyloučení z nového typu profilu, které se přidaly, a také všechny existující zásady, které jste nakonfigurovali v profilu *antivirové ochrany v Microsoft Defenderu* .



<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také:

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
