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
ms.openlocfilehash: cb9c5c43e3e5c1f9542e06ab1fa4b3b1868924e8
ms.sourcegitcommit: 37dc6b78de8bb904b83a9d571f3c9f414b54f321
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "90848381"
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

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>Podpora certifikátů s velikostí klíče 4096 na zařízeních s iOS a macOS<!-- 7659175   -->
Intune bude brzy podporovat použití velikosti klíče 4096 bitů pro profily certifikátů SCEP. (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořit profil**  >  *vybrat platformu*  >  *Profil*  =  **Certifikát SCEP**)

Podpora 4096 bitových klíčů bude pro následující platformy: 
- iOS 14 a novější
- macOS 11 a novější    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Nové nastavení složitosti hesla pro Android 10 a novější<!-- 7992114  -->
Pro podporu nových možností pro Android 10 a novější přidáváme nové nastavení s názvem **složitost hesla** pro zásady *dodržování předpisů zařízením* i zásady *omezení zařízení* . (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořit profil**  >  **Omezení zařízení** a **Devices**  >  **zásady dodržování předpisů**  >  pro zařízení**vytvořit zásadu**) s tímto nastavením budete moct spravovat míru pevnosti hesla, která je v souladu s faktory typu, délky a kvality hesla. 

Podporují se tyto úrovně složitosti:
- **Žádné** – žádné heslo
- **Nízká** – heslo splňuje jednu z následujících možností:
  - Vzor
  - Připnout pomocí sekvencí opakování (4444) nebo seřazené (1234, 4321, 2468)
- **Střední** – heslo splňuje jednu z následujících možností:
  - Připnout bez opakování (4444) nebo seřazené (1234, 4321, 2468) sekvence, délka aspoň 4
  - Abecední, délka nejméně 4
  - Alfanumerické znaky, délka nejméně 4
- **Vysoká** – heslo splňuje jednu z následujících možností:
  - Připnout bez opakování (4444) nebo seřazené (1234, 4321, 2468) sekvence, délka aspoň 8
  - Abecední, délka alespoň 6
  - Alfanumerické znaky, délka nejméně 6

Složitost hesla se nevztahuje na zařízení Samsung KNOX se systémem Android 10 a novějším. Tato zařízení, délka hesla nebo nastavení typu hesla přepíší složitost hesla.

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>Aktualizace se škálováním na verzi Preview: nové nastavení pro vytvoření požadavků na heslo pracovního profilu pro zařízení s Androidem Enterprise, která jsou ve vlastnictví firmy, s pracovním profilem<!--7088355 -->
Budoucí nastavení umožní správcům nastavovat požadavky na heslo pracovního profilu pro zařízení s Androidem Enterprise ve vlastnictví firmy s pracovním profilem.  (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořit profil**  >  **Android Enterprise** for Platform > **plně spravovaná, vyhrazená a podniková omezení pracovních profilů**  >  **Device restrictions** pro profil > **pracovního profilu**):

- Vyžadovaný typ hesla
- Minimální délka hesla
- Počet dní do vypršení platnosti hesla
- Počet hesel vyžadovaných před opětovným použitím hesla uživatelem
- Počet neúspěšných přihlášení před vymazáním obsahu zařízení


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>Nové nastavení pomocí sítě VPN pro jednotlivé aplikace nebo sítě VPN na vyžádání v zařízeních s iOS/iPadOS a macOS<!-- 7758772 7758837 7758886  -->
- **Zabránit uživatelům v zakázání automatické sítě VPN**: při vytváření automatické sítě VPN **pro jednotlivé aplikace** nebo připojení **k síti VPN** můžete vynutit, aby uživatelé ZACHOVALi automatické povolení a používání sítě VPN.
- **Přidružené domény**: Když vytváříte automatické připojení k **síti VPN pro jednotlivé aplikace** , můžete zadat přidružené domény v profilu sítě VPN, který automaticky spustí připojení VPN. 
- **Vyloučené domény**: Když vytváříte automatické připojení k **síti VPN pro jednotlivé aplikace** , můžete vytvořit seznam domén, které můžou obejít připojení VPN, když je připojená síť VPN pro jednotlivé aplikace.

V konfiguračních profilech **zařízení**můžete nakonfigurovat automatické profily sítě VPN  >  **Configuration profiles**  >  **vytvořením profilu**  >  **iOS/iPadOS** nebo **MacOS** pro Platform > **VPN** pro profil > **Automatické síti VPN**.

Další informace o přidružených doménách najdete v tématu [přidružené domény](../configuration/device-features-configure.md#associated-domains).

Nastavení, která můžete konfigurovat, najdete v tématu [nastavení virtuální privátní sítě (VPN) pro jednotlivé aplikace pro zařízení se systémem iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Platí pro:
- iOS/iPadOS 14 a novější
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>Aktualizace s přístavou Update Preview: nové nastavení pro konfiguraci osobního profilu pro zařízení s Androidem Enterprise vlastněná podnikem s pracovním profilem<!-- 7086356  -->
Pro zařízení vlastněná podnikem v Androidu s pracovním profilem můžete nakonfigurovat nová nastavení, která se dají konfigurovat jenom pro osobní profil (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **plně spravovaná, vyhrazená a podniková**  >  **omezení zařízení** pracovní profil pro profilový > **osobní profil**):

- **Kamera**: pomocí tohoto nastavení můžete zablokovat přístup k kameře během osobního používání.
- **Snímek obrazovky**: pomocí tohoto nastavení můžete blokovat zachycení obrazovky během osobního používání.
- **Povolit uživatelům povolit instalaci aplikací z neznámých zdrojů v osobním profilu**: pomocí tohoto nastavení můžete uživatelům povolit instalaci aplikací z neznámých zdrojů v osobním profilu. 

Pokud chcete zobrazit aktuální nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo zakažte funkce](../configuration/device-restrictions-android-for-work.md).

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>Blokování aplikací v aplikacích pro iOS/iPadOS a odložení aktualizací softwaru, které nejsou v operačním systému, na zařízeních macOS<!-- 7518422  -->
Když vytváříte profily omezení zařízení pro zařízení s iOS/iPadOS a macOS, je k dispozici několik nových nastavení:

**iOS/iPadOS 14.0 + blokovat klipy aplikací**
- Platí pro iOS/iPadOS 14,0 a novější.
- Zařízení musí být zaregistrovaná pomocí registrace zařízení nebo automatizované registrace zařízení (zařízení pod dohledem).
- **Blok aplikace** blokuje nastavení blokovat klipy aplikací na spravovaných zařízeních (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro > pro > pro profil pro **zařízení** ). **General** Když je blokované, uživatelé nemůžou přidávat žádné klipy aplikací a všechny existující klipy aplikací se ze zařízení odeberou.  

**macOS 11 + odložení aktualizací softwaru**
- Platí pro macOS 11 a novější. Na zařízeních macOS, která jsou pod dohledem, musí mít zařízení k registraci zařízení schválená uživatelem nebo může být zaregistrovaná prostřednictvím automatického zápisu zařízení.
- Nastavení **odložení aktualizací softwaru** zpozdí uživatele o aktualizacích softwaru bez operačního systému (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **MacOS** pro **omezení** platformy > pro profil > **Obecné**). Pokud tyto aktualizace odložíte, nově vydané aktualizace nejsou viditelné pro uživatele až po uplynutí období odložení, které je nakonfigurováno pomocí možnosti **zpoždění viditelnosti aktualizací softwaru** . Odložení aktualizací softwaru nesouvisejících s operačním systémem nemá vliv na plánované aktualizace.
- Stávající nastavení **odložení aktualizací softwaru** je v kombinaci s tímto novým nastavením. Pomocí nového nastavení můžete odložit aktualizace softwaru operačního systému a aktualizace softwaru mimo operační systém. Pokud chcete nastavit počet dnů, který bude odkládat aktualizace softwaru, budete nadále používat nastavení **zpoždění viditelnosti aktualizací softwaru** .
- Chování stávajících zásad se nemění, ovlivňuje ani neodstraní. Existující zásady budou automaticky migrovány do nového nastavení se stejnou konfigurací.

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>Zakázání náhodnosti adresy MAC na sítích Wi-Fi na zařízeních s iOS/iPadOS<!-- 7758689  -->
Od iOS/iPadOS 14 ve výchozím nastavení zařízení při připojování k síti místo fyzické adresy MAC prezentují náhodnou adresu MAC. Toto chování se doporučuje u ochrany osobních údajů, protože je těžší sledovat zařízení podle adresy MAC. Tato funkce také přerušuje funkčnost, která spoléhá na statickou adresu MAC, včetně řízení přístupu k síti (NAC). 

V profilech sítě Wi-Fi můžete zakázat náhodnost adresy MAC na základě jednotlivých sítí (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro platformu > **Wi-Fi** pro > **Basic** nebo **Enterprise** pro Wi-Fi typ).

Pokud se chcete podívat na nastavení, která můžete konfigurovat, přejděte na [Přidat nastavení Wi-Fi pro zařízení s iOS a iPadOS](../configuration/wi-fi-settings-ios.md).

Platí pro:
- iOS/iPadOS 14 a novější

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>Nastavení maximální přenosové jednotky pro připojení IKEv2 VPN na zařízeních s iOS/iPadOS<!-- 7758937  -->
Od iOS/iPadOS 14 a novějších zařízení můžete při použití připojení VPN IKEv2 nakonfigurovat vlastní maximální přenosovou jednotku (MTU) (**Devices**  >  **konfigurační profily**zařízení  >  **vytvořit profil**  >  **iOS/iPadOS** pro Platform > **VPN** pro profil-> IKEv2 pro typ připojení).

Další informace o nastaveních, která můžete konfigurovat, najdete v tématu [Nastavení IKEv2](../configuration/vpn-settings-ios.md#ikev2-settings).

Platí pro:
- iOS/iPadOS 14 a novější

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>Připojení VPN vázané na účet pro e-mailové profily na zařízeních s iOS/iPadOS<!-- 7759116  -->
Od iOS/iPadOS 14 se provoz e-mailu pro nativní e-mailové aplikace dá směrovat přes síť VPN na základě účtu, který uživatel používá. Nyní můžete určit profil sítě VPN pro jednotlivé aplikace, který bude použit pro toto připojení k síti VPN založené na účtu.  Připojení VPN pro jednotlivé aplikace se automaticky zapne, když uživatelé použijí účet organizace v e-mailové aplikaci.

Pokud se chcete podívat na nastavení, která můžete konfigurovat, přejděte na [Přidat nastavení e-mailu pro zařízení s iOS a iPadOS](../configuration/email-settings-ios.md).

Platí pro:
- iOS/iPadOS 14 a novější

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

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>Aktualizace s využitím verze Preview: resetování hesla pracovního profilu pro zařízení s Androidem Enterprise ve vlastnictví firmy s pracovním profilem <!--7217228 -->
Budoucí akce správy umožní správcům resetovat heslo pracovního profilu na zařízeních s Androidem Enterprise, která jsou ve vlastnictví firmy, s pracovním profilem.

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>Přejmenování spoluspravovaného zařízení, které je Azure Active Directory připojeno<!--7728043 -->
Budete moct přejmenovat spoluspravované zařízení, které je připojené ke službě Azure AD. Provedete to tak, že přejdete do paměti mem > **zařízení**  >  **všechna zařízení** > vyberte > zařízení **...**  >  **Přejmenujte zařízení**.

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Podpora pro PowerPrecision a PowerPrecision + baterie pro zařízení Zebra<!--3724987 -->
Na stránce Podrobnosti o hardwaru zařízení budete moct zobrazit následující informace o zařízeních Zebra pomocí PowerPrecision a PowerPrecision a baterií:
- Hodnocení stavu podle Zebra (jenom baterie PowerPrecision +)
- Počet spotřebovaných cyklů plného nabití
- Datum posledního vrácení se změnami pro baterii naposledy nalezenou v zařízení
- Sériové číslo poslední nalezené sady baterií v zařízení

<!-- ***********************************************-->
## <a name="intune-apps"></a>Aplikace Intune

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Jednotné doručování aplikací Azure AD Enterprise a Office Online v systému Windows Portál společnosti<!-- 1817861  -->
Ve verzi 2006 jsme oznámili [jednotné doručování aplikací Azure AD Enterprise a Office Online v portál společnosti](../fundamentals/whats-new.md). Tato funkce bude podporována ve Windows Portál společnosti. V podokně **vlastní nastavení** v Intune budete moct vybrat možnost **Skrýt** nebo **Zobrazit** **podnikové aplikace Azure AD** a **aplikace Office Online** ve Windows portál společnosti. Každý koncový uživatel uvidí ze zvolené služby Microsoftu celý katalog aplikací. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberete vlastní nastavení **správy tenanta**  >  **Customization** a vyhledáte toto nastavení konfigurace. Související informace najdete v tématu [Postup přizpůsobení aplikací portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Šablona sestavy dodržování předpisů Power BI V 2.0<!-- 636958  -->
Správci budou moct aktualizovat verzi šablony zprávy o kompatibilitě Power BI z verze 1.0 až verze 2.0. Verze 2.0 bude obsahovat vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Související informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md).


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Nové a vylepšené sestavy antivirové ochrany v programu Microsoft Defender pro Windows 10 a novější<!-- 6018169  -->
Přidáváme čtyři nové sestavy antivirová ochrana v programu Microsoft Defender ve Windows 10 v části **Endpoint Security**  >  **Antivirus**.
- Dvě provozní sestavy, *zařízení se zjištěným malwarem* a *stavem agenta*.
- Dvě organizační sestavy *zjistily stav malwaru* a *agenta*.

Například *Stav agenta* provozní sestavy se zobrazí na první pohled na název zařízení, uživatelské jméno, e-mailovou adresu uživatele a hlavní název uživatele a na povolení ochrany v reálném čase a na ochranu sítě. Další podrobnosti budeme sdílet, až budou tyto sestavy k dispozici pro použití.

Další informace o zabezpečení koncového bodu v Intune najdete v tématu [Správa zabezpečení koncového bodu v Microsoft Intune](../protect/endpoint-security.md).

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>Analýza místních objektů zásad skupiny pomocí služby Zásady skupiny Analytics (Preview)<!--7200950 -->
V části **zařízení**  >  **Zásady skupiny Analytics (Preview)** můžete importovat objekty zásad skupiny (GPO) v centru pro správu Správce koncových bodů. Když importujete, Intune automaticky analyzuje objekt zásad skupiny a zobrazí zásady, které mají ekvivalentní nastavení v Intune. Zobrazuje taky objekty zásad skupiny, které jsou zastaralé nebo už nejsou podporované.

Platí pro:
- Windows 10 a novější

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Nová sestava aktualizace funkcí Windows 10<!-- 6473128  -->
Sestava **aktualizací funkcí Windows** poskytne celkový přehled o dodržování předpisů pro zařízení, na která cílí zásada **aktualizace funkcí Windows 10** . V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberete **Reports**  >  pro zobrazení souhrnu této sestavy zprávy o selhání aktualizace funkcí**Windows Updates (Preview)**  >  **Feature update failures** . Chcete-li zobrazit sestavy pro konkrétní zásady, vyberte kartu **sestavy** a otevřete **sestavu aktualizace funkcí systému Windows**. 

#### <a name="new-windows-10-feature-failures-update-report---6473121-----"></a>Nová sestava aktualizace chyb funkcí Windows 10<!-- 6473121   -->
Zpráva o **chybách aktualizace funkcí** poskytne podrobnosti o selhání u zařízení, na která cílí zásada **aktualizace funkcí Windows 10** , a pokusy o aktualizaci. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberete **zařízení**  >  **monitorování**  >  **Selhání aktualizací funkcí** k zobrazení této sestavy.

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

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Vylepšené nasazení certifikátů pro Android Enterprise <!-- 6296499  -->
Zařízení se systémem Android Enterprise plně spravovaná, vyhrazená a podnikově vlastněné pracovní profily budou brzy moci používat certifikáty S/MIME pro Outlook bez toho, aby uživatel zařízení musel přístup umožňovat. Certifikáty S/MIME se nasazují pomocí profilu certifikátu importovaného PKCS pro konfiguraci zařízení. (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořit profil**  >  **Android Enterprise**  >  **Importovaný certifikát PKCS** z kategorie pro *plně spravovaný, vyhrazený a pracovní profil*, který je ve vlastnictví firmy.

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>Možnosti Tri-State pro nastavení přicházejí do zásad brány firewall zabezpečení koncového bodu.<!-- 6586159   -->
Přidáváme třetí stav konfigurace pro nastavení v zásadách brány firewall zabezpečení koncového bodu, kde platforma (Windows nebo MacOS) může podporovat další možnost (**Endpoint Security**  >  **firewall**).

Například, pokud nastavení aktuálně nabízí hodnotu **Nenakonfigurováno** a **Ano**, pokud je platforma podporována, přidáme možnost **No**.

### <a name="new-security-baseline-for-office---3150261----"></a>Nové základní hodnoty zabezpečení pro Office<!-- 3150261  -->
Přidáváme nové standardní hodnoty zabezpečení (**Endpoint security**  >  **standardní hodnoty zabezpečení**Endpoint Security) ke správě nastavení pro *systém Microsoft Office O365*. Nastavení ve standardních hodnotách budou zahrnovat konfigurace pro aplikace Office, jako je *Správa doplňku*,  *manipulace s MIME*a další.

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>Vylepšení podrobností o stavu v sestavách směrného plánu zabezpečení<!-- 7221051    -->
Vylepšujeme podrobnosti o stavu, které se zobrazí při prohlížení výsledků vašich nasazených standardních hodnot zabezpečení. (**Zabezpečení**  >  koncového bodu **Standardní hodnoty zabezpečení**  >   *Vyberte typ směrného plánu zabezpečení,* například profily **standardních hodnot zabezpečení Windows 10**  >  **Profiles**  >  *Vyberte instanci tohoto profilu k zobrazení stavu*  >  *Vybrat sestavu profilu, jako je* **stav zařízení**).

Tato vylepšení upraví společné popisky a definice, které používáme pro stav, aby lépe vyhovovaly záměru stavu. Příklad:
- **Odpovídá směrnému plánu**  se aktualizuje tak, aby **odpovídala výchozím nastavením**, což lépe popisuje záměr identifikovat, kdy konfigurace zařízení odpovídá výchozí (beze změny) základní konfiguraci.
- **Nesprávně nakonfigurované** údaje budou rozdělené do konkrétnějších podrobností, jako je **Chyba**, **konflikt**a **čeká na vyřízení**. Nové stavy přenese konzistenci do jiných oblastí konzoly.

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>Rozšířená oprávnění RBAC pro roli zabezpečení koncového bodu<!--7312374  idstaged -->
Role **Správce zabezpečení koncového bodu** pro Intune přijímá pro vzdálené úlohy oprávnění řízení přístupu na základě role (RBAC). Tato role uděluje přístup k centru pro správu Microsoft Endpoint Manageru a můžou ho používat jednotlivci, kteří spravují funkce zabezpečení a dodržování předpisů, včetně standardních hodnot zabezpečení, dodržování předpisů zařízením, podmíněného přístupu a rozšířené ochrany před internetovými útoky v programu Microsoft Defender.

Pokud chcete zobrazit oprávnění pro roli RBAC Intune, klikněte na (**Tenant admin**  >  **role Intune**správce tenanta  >  *Vyberte*  >  **oprávnění**role).

Rozšířená oprávnění pro vzdálené úlohy zahrnují následující:

- Restartovat hned
- vzdálené uzamčení
- Otočit BitLockerKeys (Preview)
- Otočit klíč trezoru
- Synchronizovat zařízení
- Microsoft Defender
- Zahájit akci Správce konfigurace

### <a name="updates-for-security-baselines---7102146-7103916----"></a>Aktualizace pro standardní hodnoty zabezpečení<!-- 7102146, 7103916  -->
Brzy budeme vydávat aktualizace následujících standardních hodnot zabezpečení (**Endpoint security**  >  **standardní hodnoty zabezpečení**Endpoint Security):
- **Směrný plán zabezpečení MDM** (zabezpečení Windows 10)
- **Základní hodnoty ATP v programu Microsoft Defender**

Aktualizované základní verze přinášejí podporu pro poslední nastavení, která vám pomůžou udržovat osvědčené konfigurace doporučené příslušnými produktovými týmy.

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>Určení zdroje konfliktů zásad pro zařízení pomocí podrobností konfigurace zabezpečení koncového bodu<!-- 7567503  idstaged  -->
V rámci řešení konfliktů budete brzy moci přejít k podrobnostem v profilu standardních hodnot zabezpečení a zobrazit *konfiguraci zabezpečení koncového bodu* pro vybrané zařízení. Odtud můžete vybrat nastavení, která zobrazí *konflikt* nebo *chybu* , a dál přejít k podrobnostem o zobrazení seznamu podrobností, které obsahují profily a zásady, které jsou součástí konfliktu. Pokud pak vyberete zásadu, která je zdrojem konfliktu, otevře Intune podokno Přehled zásad, ve kterém můžete zkontrolovat nebo upravit konfiguraci zásad. (**Zařízení**  >  *Vyberte zařízení*  >  . Konfigurace zabezpečení koncového **bodu**  >  *Vyberte profil nebo směrný plán*  >  . *Vyberte nastavení ze seznamu nastavení použitých pro zařízení*).

Následující typy zásad je možné identifikovat jako zdroj konfliktu při přechodu přes základní úroveň zabezpečení:
- Zásady konfigurace zařízení
- Zásady zabezpečení koncového bodu

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>Nové podrobnosti v konfiguraci zabezpečení koncového bodu pro zařízení<!-- 7745029   -->
Přidáváme nové podrobnosti pro zařízení, která jsou k dispozici pro zobrazení v rámci konfigurace zabezpečení koncového bodu zařízení. (**Zabezpečení**  >  koncového bodu **Standardní hodnoty zabezpečení**  >  *vybraný směrný plán*  >  **Profily**  >  *vybraný profil*  >  **Stav zařízení**  >  **Konfigurace zabezpečení koncového bodu**). Nové podrobnosti:

- **UPN (hlavní** název uživatele): hlavní název uživatele (UPN), který určuje, který profil zabezpečení koncového bodu je přiřazen danému uživateli na zařízení. To je užitečné, když chcete rozlišovat mezi několika uživateli na zařízení a několika záznamy profilu nebo směrného plánu, který je přiřazený k zařízení. 
- **Nejhorší stav**: Tato podrobnosti určuje nejnižší stav stavu pro zařízení. Pokud je tento stav **úspěšný**, zařízení neobsahují konflikty nebo chyby zásad.

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 zastaralá nasazení důvěryhodných kořenových certifikátů do zařízení zaregistrovaných správcem zařízení<!--7662775  -->
V systému Android 11 již nelze důvěryhodné kořenové certifikáty nasadit do zařízení, která jsou zaregistrovaná jako *Správce zařízení s Androidem*. Tato změna neovlivní zařízení se zabezpečením Samsung KNOX kvůli integraci Intune s platformou Knox. V případě zařízení, která nejsou Samsung, uživatelé musí do zařízení ručně nainstalovat důvěryhodný kořenový certifikát. 

Po ruční instalaci důvěryhodného kořenového certifikátu na zařízení můžete pomocí protokolu SCEP zřídit certifikáty pro zařízení. V tomto scénáři musíte pořád vytvořit a nasadit zásady *důvěryhodných certifikátů* na zařízení a propojit tyto zásady s profilem *certifikátu SCEP* .

- Pokud je důvěryhodný kořenový certifikát na zařízení, profil certifikátu SCEP se nainstaluje úspěšně. 
- Pokud se důvěryhodný certifikát nenajde, profil certifikátu SCEP selže.

<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
