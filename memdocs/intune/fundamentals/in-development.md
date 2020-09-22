---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1f261d8d61fc2c4273ae8f137a43bb6c607430d
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002694"
---
# <a name="in-development-for-microsoft-intune"></a>Ve vývoji pro Microsoft Intune

Tato stránka vám umožní v rámci připravenosti a plánování vypsat aktualizace uživatelského rozhraní Intune a funkce, které jsou ve vývoji, ale ještě nejsou vydané. Kromě informací na této stránce: 

- Pokud předpokládáme, že před změnou budete muset provést nějakou akci, zveřejníme doplňkový příspěvek v centru zpráv Office.
- Pokud funkce vstoupí do produkčního prostředí, ať už je verze Preview, nebo je všeobecně dostupná, popis funkce se přesune z této stránky na [co je nového](whats-new.md).
- Tato stránka a stránka [co je nového](whats-new.md) se pravidelně aktualizují. Přijďte se tedy znovu podívat, jestli nejsou k dispozici nové informace.
- Strategické dodávky a časová osa najdete v tématu [Microsoft 365 plán](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) .

> [!NOTE]
> Tato stránka odráží naše aktuální očekávání funkcí Intune v nadcházející verzi. Data a jednotlivé funkce se můžou změnit. Tato stránka nepopisuje všechny funkce vývoje.

**Informační kanál RSS**: Zjistěte, kdy se tato stránka aktualizuje zkopírováním a vložením následující adresy URL do čtečky informačních kanálů: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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


<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Vytvoření profilů certifikátů PKCS pro plně spravovaná zařízení s Androidem Enterprise (COBO)<!-- 4839686 -->
Profily certifikátů PKCS můžete vytvořit k nasazení certifikátů na zařízení s vlastníkem zařízení s Androidem Enterprise a pracovním profilem (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil pro**  >  **Android Enterprise > pouze vlastník zařízení**), nebo **Android Enterprise > Work Profile pouze** pro platformu > **PKCS** pro profil).

Brzy budete moct vytvořit profily certifikátů PKCS pro zařízení s plnou správou v Androidu Enterprise. Je vyžadován konektor certifikátu PFX Intune. Pokud protokol SCEP nepoužíváte a používáte jenom PKCS, můžete konektor NDES odebrat po instalaci nového konektoru PFX. Nový konektor PFX importuje soubory PFX a nasadí certifikáty PKCS na všechny platformy.

Další informace o certifikátech PKCS najdete v tématu [Konfigurace a používání certifikátů PKCS pomocí Intune](../protect/certficates-pfx-configure.md).

Platí pro:
- Android Enterprise Full Managed (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Použití NetMotion jako typu připojení VPN pro zařízení s Androidem Enterprise Work Profile<!-- 7764263 -->
Když vytváříte profil sítě VPN, NetMotion je k dispozici jako typ připojení VPN (**zařízení**  >  **Konfigurace zařízení**  >  **vytvořit profil**  >  v**Android Enterprise pracovní profil** pro Platform > > **VPN** pro **NetMotion** pro typ připojení).

Další informace o profilech sítě VPN v Intune najdete v tématu [Vytvoření profilů sítě VPN pro připojení k SERVERŮM VPN](../configuration/vpn-settings-configure.md).

Platí pro:
- Pracovní profil Android Enterprise

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Změny nastavení hesla v profilech omezení zařízení pro správce zařízení s Androidem<!-- 7662279  --> 
Zavádíme několik změn nastavení hesla pro zásady *omezení zařízení* a *dodržování předpisů* pro *Správce zařízení s Androidem*. (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořit profil**  >  **Omezení zařízení** a **Devices**  >  **zásady dodržování předpisů**pro zařízení  >  **vytvořit zásadu**) tyto změny vám pomůžou Intune přizpůsobit změny v Androidu 10 a novějším, aby se zajistilo, že se nastavení hesel v zařízeních i nadále vztahují na zařízení podle očekávání.
 
Změny zahrnují:
- Odebrání možnosti na nejvyšší úrovni pro **heslo**  
- Nastavení budou znovu uspořádána do oddílů, které jsou založeny na tom, na která zařízení se vztahují.
- **Minimální délka hesla** se zakáže pro použití, pokud není **typ hesla** nakonfigurovaný na hodnotu, na které se vztahuje délka hesla.
- Další aktualizace popisků a příkladů textu

Tyto změny se vztahují na uživatelské rozhraní pro nastavení a neovlivní stávající profily. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrace zařízení

### <a name="ending-support-for-ios-11--7327321---"></a>Koncová podpora pro iOS 11<!--7327321 -->
Po vydání iOS 14 budou registrace Intune a aplikace Portál společnosti podporovat iOS verze 12 a novější. Starší verze se nepodporují, ale budou dál dostávat zásady.

### <a name="ending-support-for-macos-1012--7327326---"></a>Koncová podpora pro macOS 10,12<!--7327326 -->
Po vydání verze macOS 11 bude registrace Intune a Portál společnosti podporovat macOS verze 10,13 a novější. Starší verze se nepodporují.


<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
V **sestavách**  >  **Log Analytics**budou k dispozici protokoly podrobností o zařízeních v Intune. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Připojení tenanta: spuštění skriptů z centra pro správu<!--7220536, CM6234688 -->
Do centra pro správu služby Microsoft Endpoint Manager budete moct využít sílu Configuration Manager funkce místního [spouštění skriptů](../../configmgr/apps/deploy-use/create-deploy-scripts.md) . Povolí další osoby, jako je helpdesk, aby se spouštěly skripty PowerShellu z cloudu proti jednotlivým Configuration Manager spravovaným zařízením. To poskytuje všechny tradiční výhody skriptů PowerShellu, které již byly definovány a schváleny správcem Configuration Manager k tomuto novému prostředí. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Nasazení aktualizací softwaru do zařízení macOS <!-- 3194876 -->
Aktualizace softwaru budete moct nasadit do skupin zařízení macOS. Tato funkce zahrnuje kritické, firmware, konfigurační soubor a další aktualizace. V příští registraci zařízení budete moct odesílat aktualizace, nebo můžete vybrat týdenní plán pro nasazení aktualizací do nebo z časového intervalu, který jste nastavili. To pomáhá při aktualizaci zařízení mimo standardní pracovní dobu nebo v případě, že je vaše Helpdesk plně přiřazená. Zobrazí se vám také podrobná sestava všech zařízení macOS s nasazenými aktualizacemi. Pokud chcete zobrazit stav konkrétních aktualizací, můžete přejít k sestavě podle jednotlivých zařízení.

<!-- ***********************************************-->
## <a name="intune-apps"></a>Aplikace Intune

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Jednotné doručování aplikací Azure AD Enterprise a Office Online v systému Windows Portál společnosti<!-- 1817861  -->
Ve verzi 2006 jsme oznámili [jednotné doručování aplikací Azure AD Enterprise a Office Online v portál společnosti](../fundamentals/whats-new.md). Tato funkce bude podporována ve Windows Portál společnosti. V podokně **vlastní nastavení** v Intune budete moct vybrat možnost **Skrýt** nebo **Zobrazit** **podnikové aplikace Azure AD** a **aplikace Office Online** ve Windows portál společnosti. Každý koncový uživatel uvidí ze zvolené služby Microsoftu celý katalog aplikací. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberete vlastní nastavení **správy tenanta**  >  **Customization** a vyhledáte toto nastavení konfigurace. Související informace najdete v tématu [Postup přizpůsobení aplikací portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).
 

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



<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
