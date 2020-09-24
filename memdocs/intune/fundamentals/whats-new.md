---
title: Novinky v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Zjistěte, jaké novinky přináší portál Intune Azure.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a0f1b386127470585b935fca30792e1ff6c89df
ms.sourcegitcommit: bcfacddbee1faa3826eea89697018450dfa9d264
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2020
ms.locfileid: "91134879"
---
# <a name="whats-new-in-microsoft-intune"></a>Co je nového v Microsoft Intune

Podívejte se, co je nového v jednom týdnu v Microsoft Intune v [centru pro správu Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Můžete také najít [důležitá oznámení](#notices), [Minulá vydání](whats-new-archive.md)a informace o [tom, jak jsou aktualizace služby Intune vydané](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Zavedení každé [měsíční aktualizace](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) může trvat až tři dny a bude v tomto pořadí:
>
> - Den 1: Asie a Tichomoří (APAC)
> - Den 2: Evropa, Střední východ, Afrika (Evropa)
> - Den 3: Severní Amerika
> - Den 4 +: Intune pro státní správu
>
> Některé funkce můžou vycházet v průběhu několika týdnů a nemusí být k dispozici všem zákazníkům hned první týden. 
>
> Seznam nadcházejících funkcí ve verzi najdete na [stránce pro vývoj na webu](in-development.md) .

**Informační kanál RSS**: po aktualizaci této stránky se zobrazí upozornění zkopírováním a vložením následující adresy URL do čtečky informačních kanálů: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts

<!-- ########################## -->
## <a name="week-of-september-21-2020"></a>Týden od 21. září 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### <a name="device-management"></a>Správa zařízení

### <a name="tenant-attach-run-scripts-from-the-admin-center"></a>Připojení tenanta: spuštění skriptů z centra pro správu
<!--7220536, CM6234688-->
Využijte možnosti Configuration Manager funkce místního [spouštění skriptů](../../configmgr/apps/deploy-use/create-deploy-scripts.md) do centra pro správu Microsoft Endpoint Manager. Umožněte dalším osoby, jako je helpdesk, ke spouštění skriptů PowerShellu z cloudu na základě individuální Configuration Manager spravovaného zařízení v reálném čase. To poskytuje všechny tradiční výhody skriptů PowerShellu, které již byly definovány a schváleny správcem Configuration Manager k tomuto novému prostředí. Další informace najdete v tématu věnovaném [připojení tenanta: spuštění skriptů z centra pro správu](../../configmgr/tenant-attach/scripts.md).

### <a name="app-management"></a>Správa aplikací

#### <a name="app-protection-policies-allow-administrators-to-configure-incoming-org-data-locations---4176693---"></a>Zásady ochrany aplikací umožňují správcům konfigurovat umístění příchozích dat organizace.<!-- 4176693 -->
Nyní můžete určit, které důvěryhodné zdroje dat smějí být otevřeny do dokumentů organizace. Podobně jako u stávajících možností **Uložit kopie pro** zásady ochrany aplikací pro organizace můžete definovat, která umístění příchozích dat jsou důvěryhodná. Tato funkce se týká následujících nastavení zásad ochrany aplikací:
- **Uložení kopií dat org**
- **Otevřít data do organizačních dokumentů**
- **Umožňuje uživatelům otevírat data z vybraných služeb.**

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **Zásady ochrany aplikací**  >  **vytvořit zásadu**. Aby bylo možné tuto funkci používat, musí aplikace spravované zásadou Intune implementovat podporu tohoto ovládacího prvku. Další informace najdete v [Nastavení zásad ochrany aplikací pro iOS](../apps/app-protection-policy-settings-ios.md) a [Nastavení zásad ochrany aplikací pro Android](../apps/app-protection-policy-settings-android.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355----"></a>Aktualizace se škálováním na verzi Preview: nové nastavení pro vytvoření požadavků na heslo pracovního profilu pro zařízení s Androidem Enterprise, která jsou ve vlastnictví firmy, s pracovním profilem<!--7088355  -->
Nová nastavení teď poskytují správcům možnost nastavovat požadavky na heslo pracovního profilu pro zařízení s Androidem Enterprise ve vlastnictví firmy s pracovním profilem:

- Vyžadovaný typ hesla
- Minimální délka hesla
- Počet dní do vypršení platnosti hesla
- Počet hesel vyžadovaných před opětovným použitím hesla uživatelem
- Počet neúspěšných přihlášení před vymazáním obsahu zařízení

Další informace najdete v tématu [nastavení zařízení s Androidem Enterprise a povolení nebo omezení funkcí v Intune](../configuration/device-restrictions-android-for-work.md).

#### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356-----"></a>Aktualizace s přístavou Update Preview: nové nastavení pro konfiguraci osobního profilu pro zařízení s Androidem Enterprise vlastněná podnikem s pracovním profilem<!-- 7086356   -->
Pro zařízení vlastněná podnikem v Androidu s pracovním profilem můžete nakonfigurovat nová nastavení, která se dají konfigurovat jenom pro osobní profil (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **plně spravovaná, vyhrazená a podniková**  >  **omezení zařízení** pracovní profil pro profilový > **osobní profil**):

- **Kamera**: pomocí tohoto nastavení můžete zablokovat přístup k kameře během osobního používání.
- **Snímek obrazovky**: pomocí tohoto nastavení můžete blokovat zachycení obrazovky během osobního používání.
- **Povolit uživatelům povolit instalaci aplikací z neznámých zdrojů v osobním profilu**: pomocí tohoto nastavení můžete uživatelům povolit instalaci aplikací z neznámých zdrojů v osobním profilu. 

Platí pro:
- Zařízení vlastněná podnikem v Androidu s pracovním profilem a osobním povoleným zařízením.

Pokud chcete zobrazit všechna nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo zakažte funkce](../configuration/device-restrictions-android-for-work.md).

#### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics--7200950-----"></a>Analýza místních objektů zásad skupiny pomocí Zásady skupiny Analytics<!--7200950   -->
V části **zařízení**  >  **Zásady skupiny Analytics (Preview)** můžete importovat objekty zásad skupiny (GPO) v centru pro správu Správce koncových bodů. Když importujete, Intune automaticky analyzuje objekt zásad skupiny a zobrazí zásady, které mají ekvivalentní nastavení v Intune. Zobrazuje taky objekty zásad skupiny, které jsou zastaralé nebo už nejsou podporované. Podrobnější přehled najdete v podrobnostech o **sestavách**služby  >   **analýzy zásad skupiny (Preview)** > sestava připravenosti na migraci.

Další informace o této funkci najdete v tématu [Zásady skupiny Analytics](../configuration/group-policy-analytics.md).

Platí pro:
- Windows 10 a novější

#### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422-----"></a>Blokování aplikací v aplikacích pro iOS/iPadOS a odložení aktualizací softwaru, které nejsou v operačním systému, na zařízeních macOS<!-- 7518422   -->
Když vytváříte profily omezení zařízení pro zařízení s iOS/iPadOS a macOS, je k dispozici několik nových nastavení:

**iOS/iPadOS 14.0 + blokovat klipy aplikací**

- Platí pro iOS/iPadOS 14,0 a novější.
- Zařízení musí být zaregistrovaná pomocí registrace zařízení nebo automatizované registrace zařízení (zařízení pod dohledem).
- **Blok aplikace** blokuje nastavení blokovat klipy aplikací na spravovaných zařízeních (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro > pro > pro profil pro **zařízení** ). **General** Když je blokované, uživatelé nemůžou přidávat žádné klipy aplikací a stávající klipy aplikací se odeberou.

**macOS 11 + odložení aktualizací softwaru**

- Platí pro macOS 11 a novější. Na zařízeních macOS, která jsou pod dohledem, musí mít zařízení k registraci zařízení schválená uživatelem nebo může být zaregistrovaná prostřednictvím automatického zápisu zařízení.
- Stávající nastavení **odložení aktualizací softwaru** může nyní zpozdit aktualizace operačního systému a jiného typu než operační systém (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **MacOS** pro > **omezení zařízení** pro > **Obecné**). Stávající **zpoždění nastavení aktualizací softwaru** se vztahuje na aktualizace operačního systému a jiných operačních systémů. Odložení aktualizací softwaru, které nejsou v operačním systému, nemá vliv na plánované aktualizace.
- Chování stávajících zásad se nemění, ovlivňuje ani neodstraní. Existující zásady budou automaticky migrovány do nového nastavení se stejnou konfigurací.

Nastavení omezení zařízení, která můžete konfigurovat, najdete v tématu [iOS/iPadOS](../configuration/device-restrictions-ios.md) a [MacOS](../configuration/device-restrictions-macos.md).

#### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886-----"></a>Nové nastavení pomocí sítě VPN pro jednotlivé aplikace nebo sítě VPN na vyžádání v zařízeních s iOS/iPadOS a macOS<!-- 7758772 7758837 7758886   -->
V konfiguračních profilech **zařízení**můžete nakonfigurovat automatické profily sítě VPN  >  **Configuration profiles**  >  **vytvořením profilu**  >  **iOS/iPadOS** nebo **MacOS** pro Platform > **VPN** pro profil > **Automatické síti VPN**. K dispozici je nové nastavení sítě VPN pro jednotlivé aplikace, které můžete nakonfigurovat:

- **Zabránit uživatelům v zakázání automatické sítě VPN**: při vytváření automatické sítě VPN **pro jednotlivé aplikace** nebo připojení **k síti VPN** můžete vynutit, aby uživatelé ZACHOVALi automatické povolení a používání sítě VPN.
- **Přidružené domény**: Když vytváříte automatické připojení k **síti VPN pro jednotlivé aplikace** , můžete přidat přidružené domény v profilu sítě VPN, který automaticky spustí připojení VPN. Další informace o přidružených doménách najdete v tématu [přidružené domény](../configuration/device-features-configure.md#associated-domains).
- **Vyloučené domény**: Když vytváříte automatické připojení k **síti VPN pro jednotlivé aplikace** , můžete přidat domény, které můžou obejít připojení VPN, když je připojená síť VPN pro jednotlivé aplikace.

Pokud si chcete zobrazit tato nastavení a další nastavení, která můžete konfigurovat, přejděte na [nastavení sítě VPN pro iOS/iPadOS](../configuration/vpn-settings-ios.md) a [MacOS nastavení VPN](../configuration/vpn-settings-macos.md).

Nastavte [virtuální privátní síť (VPN) pro jednotlivé aplikace pro zařízení se systémem iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Platí pro:
- iOS/iPadOS 14 a novější
- macOS Big Sur (macOS 11)

#### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>Nastavení maximální přenosové jednotky pro připojení IKEv2 VPN na zařízeních s iOS/iPadOS<!-- 7758937  -->
Od iOS/iPadOS 14 a novějších zařízení můžete při použití připojení IKEv2 VPN nakonfigurovat vlastní maximální přenosovou jednotku (MTU) (**Devices**  >  **konfigurační profily**zařízení  >  **vytvořit profil**  >  **iOS/iPadOS** pro Platform > **VPN** for Profiles * * > **IKEv2** pro typ připojení).

Další informace o tomto nastavení a dalších, které můžete konfigurovat, najdete v tématu [Nastavení IKEv2](../configuration/vpn-settings-ios.md#ikev2-settings).

Platí pro:
- iOS/iPadOS 14 a novější

#### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116-----"></a>Připojení VPN vázané na účet pro e-mailové profily na zařízeních s iOS/iPadOS<!-- 7759116   -->
Od iOS/iPadOS 14 se provoz e-mailu pro nativní e-mailové aplikace dá směrovat přes síť VPN na základě účtu, který uživatel používá. V Intune můžete nakonfigurovat **profil sítě VPN pro nastavení sítě VPN pro jednotlivé účty** (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **iOS/iPadOS** for Platform > **e-mail** pro profil > **Nastavení e-mailu Exchange ActiveSync**). 

Tato funkce umožňuje vybrat profil sítě VPN pro jednotlivé aplikace, který se použije pro připojení k síti VPN založené na účtu. Připojení VPN pro jednotlivé aplikace se automaticky zapne, když uživatelé použijí účet organizace v e-mailové aplikaci.

Pokud se chcete podívat na toto nastavení a další, které můžete nakonfigurovat, přejděte na [Přidat nastavení e-mailu pro zařízení s iOS a iPadOS](../configuration/email-settings-ios.md).

Platí pro:
- iOS/iPadOS 14 a novější

#### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689-----"></a>Zakázání náhodnosti adresy MAC na sítích Wi-Fi na zařízeních s iOS/iPadOS<!-- 7758689   -->
Od iOS/iPadOS 14 ve výchozím nastavení zařízení prezentují náhodný adresou MAC místo fyzické adresy MAC při připojování k síti. Toto chování se doporučuje u ochrany osobních údajů, protože je těžší sledovat zařízení podle adresy MAC. Tato funkce také přerušuje funkčnost, která spoléhá na statickou adresu MAC, včetně řízení přístupu k síti (NAC).

V profilech sítě Wi-Fi můžete zakázat náhodnost adresy MAC na základě jednotlivých sítí (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro platformu > **Wi-Fi** pro > **Basic** nebo **Enterprise** pro Wi-Fi typ).

Pokud chcete toto nastavení zobrazit a další, které můžete nakonfigurovat, přejděte na téma [Přidání nastavení Wi-Fi pro zařízení s iOS a iPadOS](../configuration/wi-fi-settings-ios.md).

Platí pro:
- iOS/iPadOS 14 a novější

#### <a name="new-settings-for-device-control-profiles----8368028---"></a>Nová nastavení pro profily řízení zařízení <!-- 8368028 -->
Do [profilu *řízení zařízení* ](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) jsme přidali pár nastavení pro zásady *omezení možností útoku* pro zařízení s Windows 10 nebo novějším:

- **Vyměnitelné úložiště**
- **Připojení USB (jenom HoloLens)**
 
Zásady pro *omezení možností útoku* jsou součástí [zabezpečení koncového bodu](../protect/endpoint-security-policy.md) v Intune.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="enrollment-status-page-shows-critical-kiosk-policies--7021540---"></a>Stránka stavu registrace zobrazuje důležité zásady veřejného terminálu.<!--7021540 -->
Teď uvidíte na stránce Stav registrace tyto zásady, které jsou sledované.
- Přiřazený přístup
- Nastavení prohlížeče veřejného terminálu
- Nastavení prohlížeče Edge

Všechny ostatní zásady veřejného terminálu nejsou aktuálně sledovány.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987----"></a>Podpora pro PowerPrecision a PowerPrecision + baterie pro zařízení Zebra<!--3724987  -->
Na stránce Podrobnosti o hardwaru zařízení teď můžete zobrazit následující informace o zařízeních Zebra pomocí PowerPrecision a PowerPrecision a baterií:
- Hodnocení stavu podle Zebra (jenom baterie PowerPrecision +)
- Počet spotřebovaných cyklů plného nabití
- Datum posledního vrácení se změnami pro baterii naposledy nalezenou v zařízení
- Sériové číslo poslední nalezené sady baterií v zařízení

#### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228----"></a>Aktualizace s využitím verze Preview: resetování hesla pracovního profilu pro zařízení s Androidem Enterprise ve vlastnictví firmy s pracovním profilem <!--7217228  -->
Teď můžete obnovit heslo pracovního profilu na zařízeních s Androidem Enterprise, která jsou ve vlastnictví firmy, pomocí pracovního profilu. Další informace najdete v tématu [resetování hesla](../remote-actions/device-passcode-reset.md#reset-a-passcode).

#### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043----"></a>Přejmenování spoluspravovaného zařízení, které je Azure Active Directory připojeno<!--7728043  -->
Teď můžete přejmenovat spoluspravované zařízení, které je připojené ke službě Azure AD. Další informace najdete v tématu [přejmenování zařízení v Intune](../remote-actions/device-rename.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="microsoft-tunnel-gateway-vpn-solution-in-preview---7843124----"></a>Řešení VPN brány Microsoft Tunnel Gateway ve verzi Preview<!-- 7843124  -->
Teď můžete nasadit [Microsoft Tunnel Gateway](../protect/microsoft-tunnel-overview.md) , který bude poskytovat vzdálený přístup k místním prostředkům na zařízeních s iOS a Androidem Enterprise (plně spravovaná firemní pracovní profil, pracovní profil).

Tunelové propojení Microsoftu podporuje moderní ověřování pomocí sítě VPN pro jednotlivé aplikace a celé zařízení, dělení tunelového propojení a možnosti podmíněného přístupu.  Tunelové propojení může podporovat více serverů brány pro zajištění vysoké dostupnosti pro produkční připravenost.

#### <a name="additional-biometric-authentication-support-for-android-devices---5706213----"></a>Další podpora biometrického ověřování pro zařízení s Androidem<!-- 5706213  -->
Nová zařízení s Androidem využívají více různorodé sady biometrika než otisky prstů. Když výrobci OEM implementují podporu pro biometrika bez otisků prstů, koncoví uživatelé můžou využít tuto možnost pro zabezpečený přístup a lepší prostředí. S vydáním verze 2009 služby Intune můžete koncovým uživatelům dovolit, aby v závislosti na tom, co zařízení s Androidem podporuje, používali otisk prstu nebo odemknutí obličeje. Můžete nakonfigurovat, zda lze k ověřování použít všechny typy biometriky mimo otisk prstu. Další informace najdete v tématu [prostředí pro ochranu aplikací pro zařízení s Androidem](../apps/app-protection-policy.md#app-protection-experience-for-android-devices).

#### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-------"></a>Nové podrobnosti v konfiguraci zabezpečení koncového bodu pro zařízení<!-- 7745029     -->
Teď si můžete zobrazit další podrobnosti o zařízeních jako součást *Konfigurace zabezpečení koncového bodu*zařízení. Když přejdete k podrobnostem, abyste si zobrazili podrobnosti o stavu zásad, které jste nasadili na zařízení, najdete následující:
 
- **UPN (hlavní** název uživatele): hlavní název uživatele (UPN), který určuje, který profil zabezpečení koncového bodu je přiřazen danému uživateli na zařízení. To je užitečné, když chcete rozlišovat mezi několika uživateli na zařízení a několika záznamy profilu nebo směrného plánu, který je přiřazený k zařízení. 

Další informace najdete v tématu [řešení konfliktů pro standardní hodnoty zabezpečení](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines).

#### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374------"></a>Rozšířená oprávnění RBAC pro roli zabezpečení koncového bodu<!--7312374    -->
Role **Správce zabezpečení koncového bodu** pro Intune má další [oprávnění řízení přístupu na základě role (RBAC) pro **vzdálené úlohy**](../protect/endpoint-security.md#permissions-granted-by-the-endpoint-security-manager-role).
 
Tato role uděluje přístup k centru pro správu Microsoft Endpoint Manageru a můžou ho používat jednotlivci, kteří spravují funkce zabezpečení a dodržování předpisů, včetně standardních hodnot zabezpečení, dodržování předpisů zařízením, podmíněného přístupu a rozšířené ochrany před internetovými útoky v programu Microsoft Defender.
 
Mezi nová oprávnění pro *vzdálené úlohy* patří:
 
- Restartovat hned
- vzdálené uzamčení
- Otočit BitLockerKeys (Preview)
- Otočit klíč trezoru
- Synchronizovat zařízení
- Microsoft Defender
- Zahájit akci Správce konfigurace
 
Pokud chcete zobrazit úplnou sadu oprávnění pro jakékoli role RBAC v Intune, klikněte na (**Tenant admin**  >  **role Intune**správce tenanta  >  *Vyberte*  >  **oprávnění**role).

#### <a name="updates-for-security-baselines---7102146-7103916-------"></a>Aktualizace pro standardní hodnoty zabezpečení<!-- 7102146, 7103916     -->
Pro následující [standardní hodnoty zabezpečení](../protect/security-baselines.md)máme k dispozici nové verze:  
 
- **[Směrný plán zabezpečení MDM (zabezpečení Windows 10)](../protect/security-baseline-settings-mdm-all.md?pivots-mdm-sept-2020)**
- **[Základní hodnoty ATP v programu Microsoft Defender](../protect/security-baseline-settings-defender-atp.md?pivots=atp-sept-2020)**
 
Aktualizované základní verze přinášejí podporu pro poslední nastavení, která vám pomůžou udržovat osvědčené konfigurace doporučené příslušnými produktovými týmy.

Informace o tom, co se změnilo mezi verzemi, najdete v tématu [Porovnání základních verzí](../protect/security-baselines.md#compare-baseline-versions) a Naučte se, jak exportovat. Soubor CSV, který zobrazuje změny.  

#### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503------"></a>Určení zdroje konfliktů zásad pro zařízení pomocí podrobností konfigurace zabezpečení koncového bodu<!-- 7567503    -->
V rámci řešení konfliktů můžete teď přejít k podrobnostem v profilu standardních hodnot zabezpečení a zobrazit tak *konfiguraci zabezpečení koncového bodu* pro vybrané zařízení. Odtud můžete vybrat nastavení, která zobrazí *konflikt* nebo *chybu* , a dál přejít k podrobnostem o zobrazení seznamu podrobností, které obsahují profily a zásady, které jsou součástí konfliktu.
 
Pokud pak vyberete zásadu, která je zdrojem konfliktu, otevře Intune podokno Přehled zásad, kde můžete zkontrolovat nebo upravit konfiguraci zásad.
 
Následující typy zásad je možné identifikovat jako zdroj konfliktu při přechodu přes základní úroveň zabezpečení:

- Zásady konfigurace zařízení
- Zásady zabezpečení koncového bodu
 
Další informace najdete v tématu [řešení konfliktů pro standardní hodnoty zabezpečení](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines).

#### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>Podpora certifikátů s velikostí klíče 4096 na zařízeních s iOS a macOS<!-- 7659175   -->
Když konfigurujete profil *certifikátu SCEP* pro zařízení s iOS/IPadOS nebo MacOS, můžete teď zadat **Velikost klíče (bity)** **4096** bitů. 
 
Intune podporuje 4096 bitů pro následující platformy: 
- iOS 14 a novější
- macOS 11 a novější  
 
Informace o konfiguraci profilů certifikátů SCEP najdete v tématu [Vytvoření profilu certifikátu SCEP](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile).

#### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 zastaralá nasazení důvěryhodných kořenových certifikátů do zařízení zaregistrovaných správcem zařízení<!--7662775  -->
Od verze Android 11 nemohou důvěryhodné kořenové certifikáty nadále instalovat důvěryhodný kořenový certifikát do zařízení, která se registrují jako *Správce zařízení s Androidem*. Toto omezení neovlivňuje zařízení se zabezpečením Samsung KNOX. V případě zařízení, která nejsou Samsung, uživatelé musí do zařízení ručně nainstalovat důvěryhodný kořenový certifikát. 
 
Po ruční instalaci důvěryhodného kořenového certifikátu do zařízení můžete k zřízení certifikátů na zařízení použít protokol SCEP. Na zařízení musíte ještě vytvořit a nasadit zásady *důvěryhodných certifikátů* a propojit tyto zásady s profilem *certifikátu SCEP* .

- Pokud je důvěryhodný kořenový certifikát na zařízení, může se profil certifikátu SCEP nainstalovat úspěšně. 
- Pokud se důvěryhodný certifikát v zařízení nepodaří najít, profil certifikátu SCEP selže.

Další informace najdete v tématu [profily důvěryhodných certifikátů pro správce zařízení s Androidem](../protect/certificates-configure.md#trusted-certificate-profiles-for-android-device-administrator).


#### <a name="tri-state-options-for-more-settings-in-endpoint-security-firewall-policy---6586159----"></a>Možnosti Tri-State pro další nastavení v zásadách brány firewall zabezpečení koncového bodu<!-- 6586159  -->
Přidali jsme třetí stav konfigurace do několika dalších nastavení v [zásadách brány firewall zabezpečení koncového bodu pro Windows 10](../protect/endpoint-security-firewall-profile-settings.md).

Aktualizují se tato nastavení:
- **Stavová protokol FTP (File Transfer Protocol) (FTP)** nyní podporuje *nenakonfigurovaná*, *povolená*a *zakázaná*.
- **Vyžádat moduly klíčů tak, aby ignorovaly pouze ověřovací sady, které nepodporují** . teď nepodporují *nenakonfigurovaná*, *povolená*a *zakázaná*.

#### <a name="improved-certificate-deployment-for-android-enterprise----6296499-------"></a>Vylepšené nasazení certifikátů pro Android Enterprise <!-- 6296499     -->
Vylepšili jsme podporu pro používání [certifikátů S/MIME pro Outlook](../protect/certificates-s-mime-encryption-sign.md) pro šifrování a podepisování na zařízeních s Androidem Enterprise, která se registrují jako plně spravované, vyhrazené a pracovní profily vlastněné firmou. Dřív použití S/MIME vyžadovalo, aby uživatel zařízení povolil přístup. Nyní můžete použít certifikáty S/MIME bez zásahu uživatele.   

K nasazení certifikátů S/MIME na podporovaná zařízení S Androidem použijte [Profil certifikátu importovaný na PKCS](../protect/certificates-imported-pfx-configure.md) nebo [Profil certifikátu SCEP](../protect/certificates-profile-scep.md) pro konfiguraci zařízení. Vytvořte profil pro **Android Enterprise** a pak vyberte **importovaný certifikát PKCS** z kategorie pro *plně spravovaný, vyhrazený a firemní pracovní profil*.

#### <a name="improved-status-details-in-security-baseline-reports---7221051---"></a>Vylepšení podrobností o stavu v sestavách směrného plánu zabezpečení<!-- 7221051 -->
Začali jsme zdokonalit mnoho podrobností o [stavu pro směrný plán zabezpečení](../protect/security-baselines-monitor.md). Po zobrazení informací o standardních verzích, které jste nasadili, se teď zobrazí smysluplnější a detailní stav.
 
Konkrétně při výběru standardních hodnot, výběru *verze*a výběru instance daného směrného plánu, se v úvodním přehledu zobrazí následující informace:
 
- Graf **stav směrného plánu zabezpečení** – tento graf nyní zobrazuje následující podrobnosti o stavu:
  - **Odpovídá výchozímu směrnému plánu** – tento stav nahrazuje *základnu* a určí, kdy se konfigurace zařízení shoduje s výchozí (neupravenou) konfigurací standardních hodnot.
  - **Odpovídá vlastnímu nastavení** – určuje, kdy konfigurace zařízení odpovídá standardnímu plánu, který jste nakonfigurovali (vlastní) a nasazení.
  - **Nesprávně nakonfigurované** – jedná se o tři stavy stavu ze zařízení: *Chyba*, *čeká*nebo *konflikt*. Tyto samostatné stavy jsou k dispozici z dalších zobrazení, jak je popsáno níže.
  - **Nepoužívá** se – to představuje zařízení, které tuto zásadu nemůže přijmout. Například zásada aktualizuje nastavení specifické pro nejnovější verzi Windows, ale zařízení používá starší (starší) verzi, která toto nastavení nepodporuje. 
- **Základní hodnota zabezpečení stav podle kategorií** – Toto je zobrazení seznamu, které zobrazuje stav zařízení podle kategorie. Dostupné sloupce jsou zrcadlové v grafu *Stav standardních hodnot zabezpečení* , ale místo chybně *nakonfigurované* uvidíte tři sloupce pro stav, který je nesprávně nakonfigurovaný:
  - **Chyba**: zásadu se nepovedlo použít. Tato zpráva se obvykle zobrazí s chybovým kódem, který odkazuje na vysvětlení.
  - **Konflikt**: pro stejné zařízení se aplikují dvě nastavení a Intune ho nedokáže rozřadit do konfliktu. Správce by měl provést kontrolu.
  - **Čeká na vyřízení**: zařízení ještě není zaregistrované v Intune, aby bylo možné tyto zásady přijmout.

#### <a name="new-setting-for-password-complexity-for-android-10-and-later-for-device-administrator-enrolled-devices---7992114---"></a>Nové nastavení složitosti hesla pro zařízení s Androidem 10 a novějším pro zařízení zaregistrovaná správcem zařízení<!-- 7992114 -->

Pro podporu nových možností pro Android 10 a novější na zařízeních zaregistrovaných jako správce zařízení s Androidem jsme přidali nové nastavení s názvem **složitost hesla** pro zásady [*dodržování předpisů zařízením*](../protect/compliance-policy-create-android.md#password) i zásady [*omezení zařízení*](../configuration/device-restrictions-android.md#password) .  Toto nové nastavení slouží ke správě *míry* síly hesla, která je v faktorech v typu hesla, délce a kvalitě. 
 
Složitost hesla se nevztahuje na zařízení se systémem Samsung KNOX. Tato zařízení, délka hesla a typ nastavení přepíší složitost hesla.

Složitost hesla podporuje následující možnosti:

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
 
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="bulk-actions-for-devices-listed-in-operational-report---8218481----"></a>Hromadné akce pro zařízení uvedená v provozní sestavě<!-- 8218481  -->
V rámci nových zpráv o antivirovém programu, které jsou součástí zabezpečení Microsoft Endpoint Manageru, poskytuje **systém Windows 10 zjištěné malwarové** sestavy hromadné akce, které se vztahují na zařízení vybraná v rámci sestavy. Akce zahrnují **restart**, **rychlou kontrolu**a **úplnou kontrolu**. Další informace najdete v tématu [zjištěná zpráva o malwaru ve Windows 10](../fundamentals/reports.md#windows-10-detected-malware-report-operational).

#### <a name="export-intune-reports-using-graph-apis---8270831----"></a>Export sestav Intune pomocí rozhraní Graph API<!-- 8270831  -->
Všechny sestavy, které byly migrovány do infrastruktury vytváření sestav Intune, budou k dispozici pro export z jediného rozhraní API pro export nejvyšší úrovně. Další informace najdete v tématu [Export sestav Intune pomocí rozhraní Graph API](../fundamentals/reports-export-graph-apis.md).

#### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Nové a vylepšené sestavy antivirové ochrany v programu Microsoft Defender pro Windows 10 a novější<!-- 6018169  -->
Do Microsoft Endpoint Manageru přidáváme čtyři nové sestavy pro antivirovou ochranu v programu Microsoft Defender ve Windows 10. Mezi tyto sestavy patří:
- Dvě provozní sestavy, *koncové body Windows 10 v pořádku* a *zjištěné malware se systémem Windows 10*. V Microsoft Endpoint Manageru vyberte **Endpoint Security**  >  **Antivirus**.
- Dvě sestavy organizace, *Stav agenta antivirového* programu a *zjištěného malwaru*. V Microsoft Endpoint Manageru vyberte **sestavy**  >  **antivirová ochrana v programu Microsoft Defender**.

Další informace najdete v tématu [sestavy Intune](../fundamentals/reports.md) a [Správa zabezpečení koncového bodu v Microsoft Intune](../protect/endpoint-security.md).

#### <a name="new-windows-10-feature-update-failures-report---6473121-----"></a>Nová sestava o chybách aktualizace funkcí Windows 10<!-- 6473121   -->
Provozní sestava **neúspěšné aktualizace funkcí** poskytuje podrobnosti o selhání pro zařízení, na která cílí zásada **aktualizace funkcí Windows 10** , a pokusy o aktualizaci. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **monitorování**  >  **Selhání aktualizací funkcí** . tím zobrazíte tuto sestavu. Další informace najdete v tématu [Sestava selhání aktualizací funkcí](../fundamentals/reports.md#feature-update-failures-report-operational) a [ověřování a vytváření sestav pro aktualizace Windows 10](../protect/windows-update-for-business-configure.md#validation-and-reporting-for-windows-10-updates).

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Nová sestava aktualizace funkcí Windows 10<!-- 6473128  -->
Sestava **aktualizace funkcí Windows 10** poskytuje celkový přehled o dodržování předpisů u zařízení, na která cílí zásada **aktualizace funkcí Windows 10** . V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **sestavy**  >  **aktualizace Windows** , abyste zobrazili souhrn této sestavy. Chcete-li zobrazit sestavy pro konkrétní zásady, vyberte z úlohy **aktualizace systému Windows** kartu **sestavy** a otevřete **sestavu aktualizace funkcí systému Windows**. Další informace najdete v tématu [aktualizace funkcí Windows 10](../fundamentals/reports.md#windows-10-feature-updates-organizational).


<!-- ########################## -->
## <a name="week-of-september-7-2020"></a>Týden od 7. září 2020
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381--"></a>Připojení tenanta: časová osa zařízení v centru pro správu<!--7220536, CM7141381-->
Když Configuration Manager synchronizuje zařízení s Microsoft Endpoint Managerem prostřednictvím připojení tenanta, budete moct zobrazit časovou osu událostí. Tato časová osa zobrazuje minulou aktivitu v zařízení, která vám může pomoct při řešení problémů. Další informace najdete v tématu [připojení klienta: časová osa zařízení v centru pro správu](../../configmgr/tenant-attach/timeline.md).

#### <a name="tenant-attach-resource-explorer-in-the-admin-center--in7220536-cm6479284---"></a><a name="bkmk_hinv"></a> Připojení tenanta: Průzkumník prostředků v centru pro správu<!--IN7220536, CM6479284 -->
V centru pro správu Microsoft Endpoint Management můžete zobrazit inventář hardwaru pro nahraná Configuration Manager zařízení pomocí Průzkumníka prostředků. Další informace najdete v tématu věnovaném [připojení klienta: Průzkumník prostředků v centru pro správu](../../configmgr/tenant-attach/resource-explorer.md).

#### <a name="tenant-attach-cmpivot-from-the-admin-center--in7220536-cm6024392--"></a>Připojení tenanta: CMPivot z centra pro správu<!--IN7220536, CM6024392-->
Využijte sílu CMPivot do centra pro správu služby Microsoft Endpoint Manager. Umožněte dalším osoby, jako je helpdesk, aby bylo možné iniciovat dotazy v reálném čase z cloudu proti jednotlivým zařízením spravovaným nástrojem ConfigMgr a vracet výsledky zpátky do centra pro správu. To poskytuje všechny tradiční výhody CMPivot, které správcům IT a dalším určeným osoby schopnost rychle vyhodnotit stav zařízení ve svém prostředí a provést akci.

Další informace o CMPivot z centra pro správu najdete v tématu [CMPivot požadavky](../../configmgr/tenant-attach/cmpivot-start.md), [CMPivot Overview](../../configmgr/tenant-attach/cmpivot-overview-attached.md)a [CMPivot Sample Scripts](../../configmgr/tenant-attach/cmpivot-samples-attached.md).

## <a name="week-of-august-31-2020"></a>Týden od 31. srpna 2020

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="new-version-of-the-pfx-certificate-connector-and-changes-for-pkcs-certificate-profile-support----4839686----"></a>Nová verze konektoru certifikátů PFX a změny pro podporu profilu certifikátu PKCS<!--  4839686  -->

Vydali jsme novou verzi konektoru certifikátů PFX verze **6.2008.60.607**. Tato nová verze konektoru:

- Podporuje profily certifikátů PKCS na všech podporovaných platformách kromě Windows 8.1
 
  V konektoru certifikátů PFX jsme konsolidují veškerou podporu PCKS.  To znamená, že pokud ve svém prostředí nepoužíváte protokol SCEP a nepoužíváte službu NDES pro jiné záměry, můžete odebrat konektor Microsoft Certificate Connector a odinstalovat NDES z vašeho prostředí. 
 
- Vzhledem k tomu, že se funkce Microsoft Certificate Connector neodebrala, můžete je dál používat k podpoře profilů certifikátů PKCS.
- Podporuje odvolání certifikátů pro Outlook S/MIME
- Vyžaduje .NET Framework 4.7.2

Další informace o konektorech certifikátů, včetně seznamu verzí konektoru pro oba konektory certifikátů, najdete v tématu [konektory certifikátů](../protect/certificate-connectors.md) .


<!-- ########################## -->
## <a name="week-of-august-24-2020-2008-service-release"></a>Týden z 24. srpna 2020 (2008 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322----"></a>Přidružené licence se odvolaly před odstraněním tokenu Apple VPP.<!--6195322  -->
Při odstranění tokenu Apple VPP v Microsoft Endpoint Manageru se všechny licence přiřazené k tomuto tokenu, které jsou přidružené k tomuto tokenu, automaticky odvolají před odstraněním.

#### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-shows-descriptions----7414768-wnstaged---"></a>Vylepšení aktualizace stránky nastavení zařízení v Portál společnosti aplikaci pro Android, která zobrazuje popisy <!-- 7414768 wnstaged -->
V aplikaci Portál společnosti na zařízeních s Androidem se na stránce **aktualizovat nastavení zařízení** zobrazí seznam nastavení, která je potřeba aktualizovat, aby splňovala předpisy. Uživatelé rozbalí problém a zobrazí se další informace a zobrazí se tlačítko **vyřešit** .

Toto uživatelské prostředí je vylepšené. Uvedená nastavení se ve výchozím nastavení rozbalí a zobrazí se popis a v případě potřeby se zobrazí tlačítko **vyřešit** . Dříve byly problémy sbaleny ve výchozím nastavení. Toto nové výchozí chování omezuje počet kliknutí, takže uživatelé mohou rychleji řešit problémy.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631-----"></a>Použití NetMotion jako typu připojení VPN pro zařízení s iOS/iPadOS a macOS<!-- 1333631   -->
Když vytváříte profil sítě VPN, NetMotion je k dispozici jako typ připojení VPN (**zařízení**  >  **Konfigurace zařízení**  >  **vytvořit profil**  >  **iOS/iPadOS** nebo **MacOS** pro Platform > **VPN** pro > pro typ připojení **NetMotion** ).

Další informace o profilech sítě VPN v Intune najdete v tématu [Vytvoření profilů sítě VPN pro připojení k SERVERŮM VPN](../configuration/vpn-settings-configure.md).

Platí pro:
- iOS/iPadOS
- macOS

#### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024----"></a>Další možnosti protokolu PEAP (Protected Extensible Authentication Protocol) pro profily sítě Wi-Fi s Windows 10<!-- 3805024  -->
Na zařízeních s Windows 10 můžete vytvořit profily Wi-Fi pomocí protokolu EAP (Extensible Authentication Protocol) k ověřování připojení Wi-Fi (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Windows 10 a novější** pro platformu > **Wi-Fi** pro > **Enterprise**).

Když vyberete protokol PEAP (Protected EAP), jsou k dispozici nová nastavení:
- **Provést ověření serveru ve fázi protokolu PEAP 1**: ve fázi vyjednávání protokolu PEAP 1 se Server ověří ověřením certifikátu.
  - **Zakázání výzev uživatele při ověřování serveru v protokolu PEAP fáze 1**: ve fázi vyjednávání protokolu PEAP 1 se nezobrazí výzvy uživatele s výzvou k autorizaci nových serverů protokolu PEAP pro důvěryhodné certifikační autority.
- **Vyžadovat kryptografickou vazbu**: zabraňuje připojením k serverům PEAP, které během vyjednávání protokolu PEAP nepoužívají kryptografických.

Nastavení, která můžete konfigurovat, najdete v tématu [Přidání nastavení Wi-Fi pro zařízení s Windows 10 a novějším](../configuration/wi-fi-settings-windows.md).

Platí pro: 
- Windows 10 a novější

#### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576--idstaged---"></a>Konfigurace modulu plug-in macOS Microsoft Enterprise SSO<!-- 5627576  idstaged -->

> [!IMPORTANT]
> V macOS se stále vyvíjí rozšíření jednotného přihlašování (SSO) Microsoft Azure AD. Je uvedená v uživatelském rozhraní Intune, ale nefunguje podle očekávání. V macOS Nepoužívejte **Microsoft Azure AD** pro typ rozšíření aplikace jednotného přihlašování.

Tým Microsoft Azure AD vytvořil rozšíření aplikace jednotného přihlašování (SSO) pro přesměrování, které macOS uživatelům 10.15 + + umožňuje získat přístup k aplikacím, organizacím a webům Microsoftu, které podporují funkci jednotného přihlašování a ověřování pomocí Azure AD, s jedním přihlašováním. Ve verzi modulu plug-in Microsoft Enterprise SSO můžete nakonfigurovat rozšíření jednotného přihlašování pomocí nového typu rozšíření aplikace Microsoft Azure AD (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **MacOS** pro **funkce** platformy > zařízení pro profil > typ rozšíření **aplikace jednotného přihlašování** > > **Microsoft Azure AD**).

K zajištění jednotného přihlašování s typem rozšíření aplikace Microsoft Azure AD jednotného přihlašování musí uživatelé na svých zařízeních s macOS instalovat aplikaci Portál společnosti a přihlásit se k ní. 

Další informace o rozšířeních aplikace macOS SSO najdete v tématu [rozšíření aplikace jednotného přihlašování](../configuration/device-features-configure.md#single-sign-on-app-extension).

Platí pro:
- macOS 10,15 a novější

#### <a name="prevent-users-from-unlocking-android-enterprise-work-profile-devices-using-face-and-iris-scanning--6069759-idmiss---"></a>Zabránit uživatelům v odemčení zařízení s podnikovým profilem Androidu pomocí skenování obličeje a Iris<!--6069759 idmiss -->
Nyní můžete uživatelům zabránit v použití kontroly obličeje nebo Iris k odemknutí svých zařízení spravovaných pomocí aplikace, a to buď na úrovni zařízení, nebo na úrovni pracovního profilu. Dá se nastavit v části **zařízení**  >  **konfigurační profily**  >  **vytvořit profil**  >  pro**Android Enterprise** for Platform > **Work Profile > omezení zařízení** pro profil > **Nastavení pracovního profilu** a **hesla** .

Další informace najdete v tématu [nastavení zařízení s Androidem Enterprise a povolení nebo omezení funkcí v Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Platí pro: 
- Pracovní profil Android Enterprise

#### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991----"></a>Použití rozšíření aplikace jednotného přihlašování na dalších aplikacích pro iOS/iPadOS s modulem plug-in Microsoft Enterprise SSO<!-- 7369991  -->
[Modul plug-in Microsoft Enterprise SSO pro zařízení Apple](/azure/active-directory/develop/apple-sso-plugin) se dá použít se všemi aplikacemi, které podporují rozšíření aplikace jednotného přihlašování. Tato funkce v Intune znamená, že modul plug-in funguje s mobilními aplikacemi pro iOS/iPadOS, které nepoužívají knihovnu Microsoft Authentication Library (MSAL) pro zařízení Apple. Aplikace nepotřebují používat MSAL, ale je potřeba je ověřit pomocí koncových bodů Azure AD.

Pokud chcete nakonfigurovat aplikace pro iOS/iPadOS, aby používaly jednotné přihlašování s modulem plug-in, přidejte identifikátory sady prostředků aplikace do konfiguračního profilu iOS/iPadOS (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro **funkce** platformy > zařízení pro profil > **rozšíření aplikace jednotného přihlašování**  >  **Microsoft Azure AD** pro typ rozšíření aplikace jednotného přihlašování > **identifikátory sady prostředků aplikace**).

Pokud chcete zobrazit aktuální nastavení rozšíření aplikace jednotného přihlašování, můžete nakonfigurovat, přejít na [rozšíření aplikace s jednotným přihlašováním](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Platí pro:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="deploy-endpoint-security-antivirus-policy-to-tenant-attached-devices-preview---5475441----"></a>Nasazení zásad ochrany koncového bodu zabezpečení Endpoint na zařízení připojená k tenantovi (Preview)<!-- 5475441  -->
V rámci verze Preview můžete nasadit zásady zabezpečení koncového bodu [pro antivirová](../protect/endpoint-security-antivirus-policy.md) řešení do zařízení, která spravujete pomocí Configuration Manager. Tento scénář vyžaduje, abyste nakonfigurovali připojení tenanta mezi podporovanou verzí Configuration Manager a vaším předplatným služby Intune. Podporovány jsou následující verze Configuration Manager:

- Configuration Manager aktuální větev 2006

Další informace najdete v tématu [požadavky na zásady zabezpečení koncového bodu Intune](../protect/tenant-attach-intune.md#specific-requirements-for-intune-endpoint-security-policies) pro podporu připojení tenanta.

#### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119------"></a>Změny vyloučení zásad antivirové ochrany Endpoint Security<!--5583940, 6018119    -->
Zavedli jsme dvě změny pro správu seznamů vyloučení antivirové ochrany v programu Microsoft Defender, které nakonfigurujete v rámci [zásad ochrany koncových bodů zabezpečení koncového bodu](../protect/endpoint-security-antivirus-policy.md). Tyto změny vám pomůžou zabránit konfliktům mezi různými zásadami a vyřešit konflikty seznamu vyloučení, které můžou existovat v dříve nasazených zásadách.

Obě změny platí pro nastavení zásad pro následující zprostředkovatele CSP ( [Microsoft Defender Configuration Service Provider](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) ):

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

Změny jsou následující:

- Nový typ profilu: **vyloučení antivirové ochrany v programu Microsoft Defender** – použijte tento nový typ profilu pro Windows 10 a novější, abyste definovali zásadu, která se zaměřuje jenom na výjimky z antivirové ochrany. Tento profil pomáhá zjednodušit správu seznamů vyloučení oddělením od jiných konfigurací zásad.

  Vyloučení, která můžete konfigurovat, zahrnují *procesy*programu Defender, *přípony souborů*a *soubory* a *složky* , které nechcete v programu Microsoft Defender kontrolovat.

- **Sloučení zásad** – Intune teď sloučí seznam vyloučení, která jste definovali v samostatných profilech, do jednoho seznamu vyloučení, který se má použít u každého zařízení nebo uživatele. Pokud například zacílíte na uživatele se třemi samostatnými zásadami, seznamy vyloučení z těchto tří zásad se sloučí do jedné nadmnožiny *vyloučení antivirové ochrany v programu Microsoft Defender*, které se pak vztahují na tohoto uživatele.

#### <a name="import-and-export-lists-of-address-ranges-for-windows-firewall-rules---8125400----"></a>Import a Export seznamů rozsahů adres pro pravidla brány Windows Firewall<!-- 8125400  -->

Přidali jsme podporu pro **Import** nebo **Export** seznamu rozsahů adres pomocí souborů. CSV do profilu pravidel firewallu Microsoft Defenderu v zásadách brány firewall pro zabezpečení koncového bodu. Následující nastavení pravidla brány Windows Firewall teď podporují import a export:

- **Rozsahy místních adres**
- **Vzdálené rozsahy adres**

Vylepšili jsme také ověřování položky místního rozsahu a vzdálených adres, aby bylo možné zabránit duplicitním nebo neplatným položkám.

Další informace o těchto nastaveních najdete v tématu nastavení pro [pravidla firewallu v programu Microsoft Defender](../protect/endpoint-security-firewall-profile-settings.md#microsoft-defender-firewall-rules).





<!-- ########################## -->
## <a name="week-of-august-17-2020"></a>Týden od 17. srpna 2020

### <a name="intune-apps"></a>Aplikace Intune

#### <a name="custom-brand-image-now-displayed-in-the-windows-company-portal-profile-page---4280187---"></a>Obrázek vlastní značky se teď zobrazuje na stránce profilu Windows Portál společnosti.<!-- 4280187 -->
Jako správce Microsoft Intune můžete nahrát vlastní image značky do Intune, která se zobrazí jako obrázek pozadí na stránce profilu uživatele v aplikaci Windows Portál společnosti. Další informace najdete v tématu [přizpůsobení aplikací portál společnosti Intune, portál společnosti webu a Intune](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Portál společnosti přidává podporu aplikací Configuration Manager<!-- 4297660 -->
Portál společnosti teď podporuje Configuration Manager aplikace. Tato funkce umožňuje koncovým uživatelům zobrazit Configuration Manager i aplikace nasazené v Intune v Portál společnosti pro spoluspravované zákazníky. Tato nová verze Portál společnosti zobrazí Configuration Manager nasazených aplikací pro všechny spoluspravované zákazníky. Tato podpora pomůže správcům konsolidovat různé prostředí portálu pro koncové uživatele. Další informace najdete v tématu [použití portál společnosti aplikace na spoluspravovaných zařízeních](../../configmgr/comanage/company-portal.md). 

### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="set-device-compliance-state-from-third-party-mdm-providers---6361689---"></a>Nastavit stav dodržování předpisů zařízením od poskytovatelů MDM třetích stran<!-- 6361689 -->

Intune teď podporuje [řešení MDM třetích stran jako zdroj podrobností o dodržování předpisů zařízením](../protect/device-compliance-partners.md). Tato data dodržování předpisů třetí strany se dají použít k prosazování zásad podmíněného přístupu pro Microsoft 365 aplikací v iOS a Androidu prostřednictvím integrace s Microsoft Intune.  Intune vyhodnocuje podrobnosti o dodržování předpisů od poskytovatele třetí strany a určí, jestli je zařízení důvěryhodné, a pak nastaví atributy podmíněného přístupu v Azure AD.  Budete pokračovat v vytváření zásad podmíněného přístupu Azure AD z centra pro správu Microsoft Endpoint Manageru nebo z portálu Azure AD.

V této verzi jsou podporovány následující poskytovatelé MDM od jiných výrobců jako verze Public Preview:

- Pracovní prostor VMware ONE UEM (dříve označovaný jako pro sledování)

*Tato aktualizace je pro zákazníky nahromadá globálně. Tato možnost by se měla zobrazit během příštího týdne.*

<!-- ########################## -->
## <a name="week-of-august-10-2020"></a>Týden od 10. srpna 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="tenant-attach-install-an-application-from-the-admin-center----in7220536-cm6024389--"></a>Připojení tenanta: instalace aplikace z centra pro správu <!-- IN7220536 CM6024389-->
Nyní můžete spustit instalaci aplikace v reálném čase pro zařízení připojené k tenantovi z centra pro správu služby Microsoft Endpoint Manager. Další informace najdete v tématu věnovaném [připojení tenanta: instalace aplikace z centra pro správu](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## <a name="week-of-july-27-2020"></a>Týden od 27. července 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="power-bi-compliance-report-template-v20---636958---"></a>Šablona sestavy dodržování předpisů Power BI V 2.0<!-- 636958 -->
Aplikace šablon Power BI umožňují partnerům Power BI vytvářet aplikace Power BI zcela bez nutnosti psaní kódu (nebo jen s minimálním psaním kódu) a nasazovat je zákazníkům Power BI. Správci mohou aktualizovat verzi šablony sestavy dodržování předpisů Power BI z verze 1.0 až V 2.0. Verze 2.0 zahrnuje vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Další informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md) a [aktualizace šablony aplikace](/power-bi/service-template-apps-install-distribute#update-a-template-app). Další informace najdete v blogovém příspěvku [s oznámením o nové verzi sestavy dodržování předpisů Power BI s datovým skladem Intune](https://aka.ms/new_compliance_report).

<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>Týden od 13. července 2020 (2007 vydání služby)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Podpora konektoru On-Premises Exchange<!-- 7138486  -->
Intune odebírá podporu funkce konektoru On-Premises Connector ze služby Intune počínaje verzí 2007 (červenec). Stávající zákazníci s aktivním konektorem budou v tuto chvíli moci pokračovat s aktuálními funkcemi. Noví zákazníci a stávající zákazníci, kteří nemají aktivní konektor, už nebudou moct vytvářet nové konektory ani spravovat zařízení Exchange ActiveSync (EAS) z Intune. Pro tyto zákazníky společnost Microsoft doporučuje používat [hybridní moderní ověřování Exchange (HMA)](/office365/enterprise/hybrid-modern-auth-overview) k ochraně přístupu k místnímu Exchangi. HMA umožňuje Intune App Protection zásady (označované také jako MAM) a podmíněný přístup prostřednictvím Outlook Mobile pro místní Exchange.

#### <a name="smime-for-outlook-on-ios-and-android-devices-without-enrollment---6517155---"></a>S/MIME pro Outlook na zařízeních s iOS a Androidem bez registrace<!-- 6517155 -->
Teď můžete povolit S/MIME pro Outlook na zařízeních s iOS a Androidem pomocí zásad konfigurace aplikací pro spravované aplikace. To umožňuje doručování zásad bez ohledu na stav registrace zařízení. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**  >  **spravované aplikace**. Kromě toho můžete zvolit, jestli chcete uživatelům dovolit, aby toto nastavení v Outlooku změnili. K automatickému nasazení certifikátů S/MIME do Outlooku pro iOS a Android se ale musí zařízení zaregistrovat. Obecné informace o S/MIME najdete v tématu [s/MIME – přehled pro podepsání a šifrování e-mailu v Intune](../protect/certificates-s-mime-encryption-sign.md). Další informace o nastavení konfigurace Outlooku najdete v tématu [nastavení konfigurace Microsoft Outlooku](../apps/app-configuration-policies-outlook.md) a [Přidání zásad konfigurace aplikací pro spravované aplikace bez registrace zařízení](../apps/app-configuration-policies-managed-app.md). Informace o aplikaci Outlook pro iOS a Android S/MIME najdete v tématu [scénáře S/MIME](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) a [konfigurační klíče nastavení s/MIME](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Nové nastavení sítě VPN pro zařízení s Windows 10 a novějšími systémy<!-- 6602122   -->

Když vytváříte profil sítě VPN pomocí typu připojení IKEv2, můžete nakonfigurovat nová nastavení. (**Devices**  >  **konfigurační profily**zařízení  >  **vytvořit profil**  >  **Windows 10 a novější** pro platformu > **VPN** pro > **základní síť VPN**):

- **Tunelové zařízení**: umožňuje zařízení automaticky se připojovat k síti VPN bez nutnosti zásahu uživatele, včetně přihlášení uživatele. Tato funkce vyžaduje, abyste povolili funkci **Always On**a jako metodu ověřování používali **certifikáty počítače** .
- Nastavení kryptografie: umožňuje nakonfigurovat algoritmy používané k zabezpečení IKE a podřízená přidružení zabezpečení, která vám umožní odpovídat nastavení klienta a serveru.

Pokud chcete zobrazit nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Windows a přidejte připojení k síti VPN pomocí Intune](../configuration/vpn-settings-windows-10.md).

Platí pro:

- Windows 10 a novější

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Konfigurace více nastavení spouštěče Microsoftu v profilu omezení zařízení na zařízeních s Androidem Enterprise (COBO)<!-- 6285001  -->

Na zařízeních se systémem Android Enterprise s plnou správou můžete nakonfigurovat další nastavení spouštěče Microsoftu pomocí profilu omezení zařízení **(**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > jenom pro zařízení **jenom pro vlastníka**zařízení, která jsou  >  **Device restrictions**  >  **Device experience**  >  **plně spravovaná**). 

Tato nastavení zobrazíte tak, že přejdete na [nastavení zařízení s Androidem Enterprise a povolíte nebo zakážete funkce](../configuration/device-restrictions-android-for-work.md#device-experience).

Můžete také nakonfigurovat nastavení spouštěče Microsoft pomocí [konfiguračního profilu aplikace](../apps/configure-microsoft-launcher.md).

Platí pro:

- Zařízení s plně spravovaným vlastníkem zařízení s Androidem Enterprise (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Nové funkce pro spravovanou domovskou obrazovku na vyhrazených zařízeních vlastníka zařízení s Androidem Enterprise (COSU)<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

Na zařízeních s Androidem Enterprise můžou správci použít profily konfigurace zařízení k přizpůsobení spravované domovské obrazovky na vyhrazených zařízeních pomocí celoobrazovkového režimu s více aplikacemi**Devices**(  >  **konfigurační profily**zařízení  >  **vytvořit profil**pro zařízení s  >  **Android Enterprise** platformou Cloud > **jenom**  >  **Device Restrictions** > pro vlastní zařízení **Device experience**  >  **Dedicated device**  >  **Multi-app**.

Konkrétně můžete:

- Přizpůsobení ikon, změna orientace obrazovky a zobrazení oznámení aplikací pro ikony BADGE <!--7414175-->
- Skrýt zástupce spravovaného nastavení <!--7133328-->
- Snadnější přístup k nabídce ladění <!--7133720-->
- Vytvoření seznamu povolených sítí Wi-Fi <!-- 7134873-->
- Snazší přístup k informacím o zařízení <!-- 7135184-->

Další informace najdete v tématu [nastavení zařízení s Androidem Enterprise a povolení nebo omezení funkcí](../configuration/device-restrictions-android-for-work.md) a [tohoto blogu](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

Platí pro:

- Vlastníci zařízení s Androidem Enterprise, vyhrazená zařízení (COSU)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>Šablony pro správu aktualizované pro Microsoft Edge 84<!--7722068-->
Nastavení ADMX dostupná pro Microsoft Edge se aktualizovala. Koncoví uživatelé teď můžou konfigurovat a nasazovat nová nastavení ADMX přidaná na Edge 84. Další informace najdete v [poznámkách k verzi Edge 84](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>Zařízení ve vlastnictví firmy (Preview)<!--4442275  -->
Intune teď podporuje zařízení se systémem Android Enterprise v podniku s pracovním profilem pro operační systémy Android 8 a vyšší. Zařízení vlastněná společností s pracovním profilem jsou jedním z scénářů podnikové správy v sadě Android Enterprise Solution. Tento scénář je určený pro samostatná uživatelská zařízení určená pro podnikové a osobní použití. Tento scénář, který je ve vlastnictví firmy, nabízí:

- pracovní a osobní profilové kontejnery
- řízení na úrovni zařízení pro správce
- záruka pro koncové uživatele, že jejich osobní data a aplikace zůstanou v soukromí

První verze Public Preview bude obsahovat podmnožinu funkcí, které budou zahrnuty do všeobecně dostupné verze. Další funkce budou přidány do provozu. Mezi funkce, které budou dostupné v první verzi Preview, patří:

- Registrace: Správci můžou vytvořit několik profilů zápisu s jedinečnými tokeny, jejichž platnost nevyprší. Registrace zařízení se dá dělat prostřednictvím NFC, záznamu tokenu, kódu QR, nulového dotyku nebo registrace pro telefonickou instalaci v Knox.
- Konfigurace zařízení: podmnožina existujících plně spravovaných a vyhrazených nastavení zařízení.
- Dodržování předpisů zařízením: zásady dodržování předpisů, které jsou aktuálně k dispozici pro plně spravovaná zařízení.
- Akce zařízení: odstranit zařízení (resetování továrního nastavení), restartovat zařízení a uzamknout zařízení.  
- Správa aplikací: přiřazení aplikací, konfigurace aplikací a přidružené možnosti vytváření sestav 
- Podmíněný přístup

Další informace o společnosti vlastněné ve verzi Preview pracovního profilu najdete na blogu věnovaném [podpoře](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>Aktualizace akce vzdáleného uzamčení pro zařízení macOS<!--7032805   -->
Změny akce vzdálené uzamčení pro zařízení macOS zahrnují:
- PIN kód pro obnovení se zobrazí po dobu 30 dní před odstraněním (místo 7 dnů).
- Pokud má správce druhý otevřený prohlížeč a pokusí se znovu aktivovat příkaz z jiné karty nebo prohlížeče, Intune umožní příkazu projít. Stav vytváření sestav se ale nastaví jako neúspěšný, nikoli generování nového PIN kódu.
- Správce není oprávněn vystavovat jiný příkaz vzdáleného uzamčení, pokud předchozí příkaz stále čeká nebo pokud zařízení není vráceno zpět.
Tyto změny jsou navržené tak, aby se zabránilo přepsání správného kódu PIN po několika příkazech vzdáleného zamykání.

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>Sestava akcí zařízení rozlišuje mezi vymazáním a chráněným vymazáním.<!--7118901 -->
Sestava **Akce zařízení** teď rozlišuje mezi akcemi vymazání a chráněných vymazání. Pokud se chcete podívat na sestavu, přejděte do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**  >  .**monitorujte**  >  **Akce zařízení** (v části **jiné**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Verze Preview nástroje pro migraci pravidel firewallu v programu Microsoft Defender<!-- 6423187   -->
Ve verzi Public Preview pracujeme na nástroji založeném na prostředí PowerShell, který bude migrovat pravidla firewallu v programu Microsoft Defender. Když nainstalujete a spustíte nástroj, automaticky se vytvoří zásady pravidla firewallu zabezpečení koncového bodu pro Intune, které jsou založené na aktuální konfiguraci klienta s Windows 10. Další informace najdete v tématu [Přehled nástroje Migrace pravidla firewallu pro Endpoint Security](../protect/endpoint-security-firewall-rule-tool.md).

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>Zjišťování koncových bodů a zásady odezvy pro zařízení připojená k klientovi do MDATP jsou všeobecně dostupné.<!-- 7303816   -->
V rámci zabezpečení koncového bodu v Intune se [zásady detekce a odezvy koncového bodu (EDR) pro použití se zařízeními spravovanými Configuration Manager](../protect/endpoint-security-edr-policy.md) už nejsou ve *verzi Preview* a jsou teď *všeobecně dostupné*.

Pokud chcete používat zásady EDR se zařízeními z podporované verze Configuration Manager, nakonfigurujte [pro Configuration Manager klienta připojení](../../configmgr/tenant-attach/device-sync-actions.md). Po dokončení konfigurace připojení tenanta můžete nasadit zásady EDR k zapojení zařízení spravovaných aplikací Configuration Manager k Rozšířené ochraně před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP).

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>Nastavení Bluetooth jsou k dispozici v profilech řízení zařízení pro zásady omezení pro útoky v zabezpečení koncového bodu. <!--7032084   -->
Přidali jsme nastavení pro správu Bluetooth na zařízeních s Windows 10 do [profilu řízení zařízení](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) pro *zásady omezení pro útoky na zabezpečení koncového bodu*.  Jedná se o stejná nastavení jako ta, která byla k dispozici v profilech omezení zařízení pro *konfiguraci zařízení*.

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Správa zdrojových umístění pro aktualizace definic pomocí zásad služby Endpoint Security AntiVir pro zařízení s Windows 10<!-- 6347801   -->  
Přidali jsme dvě nová nastavení do kategorie *Updates (aktualizace* ) [zásad ochrany koncových bodů Endpoint Security pro zařízení s Windows 10](../protect/antivirus-microsoft-defender-settings-windows.md#updates)  , která vám pomůžou spravovat, jak zařízení získávají definice aktualizací:

- *Definovat sdílené složky pro stahování aktualizací definic*
- *Definování pořadí zdrojů pro stahování aktualizací definic*

Pomocí nových nastavení můžete přidat sdílené složky UNC jako umístění zdrojů pro aktualizace definic a definovat pořadí, ve kterém se budou kontaktovat různá zdrojová umístění.

#### <a name="improved-security-baselines-node---7433136------"></a>Vylepšený uzel standardních hodnot zabezpečení<!-- 7433136    -->
Provedli jsme některé změny pro zlepšení použitelnosti [uzlu základní hodnoty zabezpečení](../protect/security-baselines.md) v centru pro správu služby Microsoft Endpoint Manager. Když teď přejdete na **Endpoint security**  >  **základní hodnoty zabezpečení** Endpoint Security a pak vyberete typ standardních hodnot zabezpečení, jako je základní hodnota zabezpečení MDM, zobrazí se v podokně **profily** . V podokně profily zobrazíte profily, které jste vytvořili pro daný typ směrného plánu.  Dřív se v konzole zobrazilo podokno s přehledem, které obsahovalo agregovaná data, která se vždycky neshodovala s podrobnostmi uvedenými v sestavách pro jednotlivé profily.

V podokně profily si můžete vybrat profil, pro který chcete zobrazit podrobné zobrazení vlastností profilů, a také různé sestavy, které jsou k dispozici v rámci *monitorování*.  Podobně na stejné úrovni jako profily stále můžete vybrat **verze** pro zobrazení různých verzí tohoto typu profilu, který jste nasadili. Když přejdete na verzi, získáte přístup také k sestavám, které se podobají sestavám profilu. 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Podpora odvozených přihlašovacích údajů pro Windows<!-- 4886090   -->
Pomocí zařízení s Windows teď můžete použít odvozená pověření. Tím se rozšíří stávající podpora pro iOS/iPadOS a Android a budou k dispozici pro stejné odvozené zprostředkovatele přihlašovacích údajů:
- Entrust Datacard
- Intercede
- DISA purebred

Podpora pro vdovy zahrnuje použití odvozeného pověření k ověření profilů sítě Wi-Fi nebo VPN. V případě zařízení s Windows se odvozené přihlašovací údaje vydávají z klientské aplikace, kterou poskytuje odvozený zprostředkovatel přihlašovacích údajů, který používáte.

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Správa šifrování trezoru v úložištích pro zařízení zašifrovaná uživatelem zařízení a ne pro Intune<!--5239424  -->
Intune teď může [na zařízení MacOS, které bylo zašifrované uživatelem zařízení](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices), a ne pomocí zásad Intune, spravovat šifrování disků trezoru.  Tento scénář vyžaduje:
- Zařízení, které přijme zásady šifrování disku z Intune, které umožňuje trezor úložišť.
- Uživatel zařízení, který bude používat web Portál společnosti k nahrání osobního obnovovacího klíče pro zašifrované zařízení do Intune. Pokud chcete tento klíč nahrát, vyberte možnost *obnovovací klíč úložiště* pro svoje šifrované zařízení MacOS.

Jakmile uživatel nahraje obnovovací klíč, Intune ho otočí a potvrdí, že je platný. Intune teď může spravovat klíč a šifrování, jako by používaly zásady k zašifrování zařízení přímo. Pokud uživatel potřebuje obnovit své zařízení, může získat přístup k obnovovacímu klíči pomocí libovolného zařízení z následujících umístění:   
- Web portálu společnosti
- Aplikace Portál společnosti pro iOS/iPadOS 
- Aplikace Portál společnosti pro Android
- Aplikace Intune

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>Skrýt osobní obnovovací klíč od uživatele zařízení během šifrování disku macOS trezoru<!--  5475632-->
Když ke konfiguraci šifrování disku trezoru macOS použijete zásady zabezpečení koncového bodu, můžete pomocí nastavení [**Skrýt obnovovací klíč**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) zabránit zobrazení *osobního obnovovacího klíče* uživateli zařízení, když se zařízení šifruje. Skrytím klíče během šifrování můžete zajistit jeho zabezpečení, protože uživatelé nebudou moct zapisovat mimo jiné při čekání na šifrování zařízení. 

Později, pokud je potřeba obnovení, může uživatel vždy použít jakékoli zařízení k zobrazení svého osobního obnovovacího klíče prostřednictvím Portál společnosti Intune webu, Portál společnosti iOS/iPadOS, Android Portál společnosti nebo aplikace Intune.

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>Vylepšené zobrazení podrobností o standardních hodnotách zabezpečení pro zařízení<!-- 5536846  -->
Teď můžete přejít k podrobnostem pro zařízení a zobrazit podrobnosti o nastaveních pro základní hodnoty zabezpečení, které se vztahují k danému zařízení. Nastavení se zobrazí v jednoduchém, nestrukturovaném seznamu, který zahrnuje kategorii nastavení, název nastavení a stav. Další informace najdete v tématu [zobrazení konfigurací zabezpečení koncového bodu na zařízení](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>Protokoly dodržování předpisů pro zařízení teď v angličtině<!--6014904  -->
V protokolech DeviceComplianceOrg Intune byly dřív jenom výčty pro ComplianceState, OwnerType a DeviceHealthThreatLevel. Nyní mají tyto protokoly ve sloupcích anglické informace.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-----"></a>Přiřadit změny oprávnění profilování a aktualizace profilu<!--7177586   -->
Změnila se oprávnění řízení přístupu na základě rolí pro přiřazení profilu a profilu aktualizace pro automatický tok registrace zařízení:

Přiřadit profil: Správci s tímto oprávněním mohou také přiřadit profily k tokenům a přiřadit k tokenu výchozí profil pro automatický zápis zařízení.

Aktualizovat profil: Správci s tímto oprávněním můžou aktualizovat existující profily jenom pro automatický zápis zařízení.

Tyto role zobrazíte tak, že přejdete do centra pro správu [služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  role správce**klienta**  >  **Roles**  >  **všechny role**  >  **vytvořit**  >  **Permissions**  >  **role**oprávnění.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Skriptování

#### <a name="additional-data-warehouse-v10-properties---6125732----"></a>Další vlastnosti datového skladu v 1.0<!-- 6125732  -->
Další vlastnosti jsou k dispozici pomocí datového skladu Intune v 1.0. Následující vlastnosti jsou nyní zpřístupněny prostřednictvím entity [zařízení](../developer/reports-ref-devices.md#devices) :
- `ethernetMacAddress` – Jedinečný identifikátor sítě tohoto zařízení.
- `office365Version` – Verze Microsoft 365, která je v zařízení nainstalovaná.

Následující vlastnosti jsou nyní zpřístupněny prostřednictvím entity [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) :
- `physicalMemoryInBytes` – Fyzická paměť v bajtech.
- `totalStorageSpaceInBytes` -Celková kapacita úložiště v bajtech.

Další informace najdete v tématu [Microsoft Intune rozhraní API datového skladu](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>Týden od 6. července 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Aktualizace ikon zařízení v Portál společnosti a aplikacích Intune v Androidu<!-- 6057023 -->
Na zařízeních s Androidem jsme aktualizovali ikony zařízení v aplikacích Portál společnosti a Intune, aby bylo možné vytvořit pokročilejší vzhled a atmosféru a sjednotit se s návrhovým systémem Microsoft Fluent. Související informace najdete v tématu [aktualizace ikon v aplikaci Portál společnosti App pro iOS/iPadOS a MacOS](whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>iOS Portál společnosti bude podporovat automatické registrace zařízení společnosti Apple bez přidružení uživatele.<!-- 7282707 --> 
Portál společnosti iOS se teď podporuje na zařízeních zaregistrovaných pomocí automatizované registrace zařízení společnosti Apple bez přiřazeného uživatele. Koncový uživatel se může přihlásit k Portál společnosti iOS, aby se sám navázal jako primární uživatel na zařízení se systémem iOS/iPadOS, které je zaregistrované bez spřažení zařízení. Další informace o automatizované registraci zařízení najdete v tématu [Automatická registrace zařízení s iOS/iPadOS pomocí automatizované registrace zařízení společnosti Apple](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr v centru pro správu (Preview)<!-- 7552762 -->

V centru pro správu Microsoft Endpoint Manageru se teď můžete podívat na podrobnosti o klientech nástroje ConfigMgr, včetně kolekcí, členství ve skupině hranic a informací o klientovi v reálném čase pro konkrétní zařízení. Další informace najdete v tématu [připojení klienta: podrobnosti o klientovi nástroje ConfigMgr v centru pro správu (Preview)](../../configmgr/tenant-attach/client-details.md).

## <a name="week-of-june-22-2020"></a>Týden od 22. června 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Nově dostupné chráněné aplikace pro Intune<!-- 7248952 -->
K dispozici jsou teď tyto chráněné aplikace:
- Videokonference BlueJeans
- Cisco Jabber pro Intune
- Tableau Mobile pro Intune
- NULA pro Intune

Další informace o chráněných aplikacích najdete v tématu [Microsoft Intune Protected Apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Využijte službu Endpoint Analytics ke zvýšení produktivity uživatelů a snížení nákladů na podporu.<!-- 5653063 --> 
V průběhu příštího týdne bude tato funkce zahrnuta. Služba Endpoint Analytics je cílem zlepšit produktivitu uživatelů a snížit náklady na podporu tím, že poskytuje přehled o prostředí uživatele. Přehledy umožňují optimalizovat činnost koncového uživatele pomocí proaktivní podpory a detekovat regrese uživatelského prostředí tím, že vyhodnotí dopad změn konfigurace na uživatele. Další informace najdete v tématu Služba [Endpoint Analytics ve verzi Preview](https://aka.ms/uea).

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Proaktivně napravit problémy zařízení koncových uživatelů pomocí balíčků skriptů<!-- 5933328 -->
Můžete vytvořit a spustit balíčky skriptů na zařízeních koncových uživatelů, abyste proaktivně našli a opravili hlavní problémy podpory ve vaší organizaci. Nasazení balíčků skriptů vám pomůže omezit volání podpory. Vyberte si vytvořit vlastní balíčky skriptů nebo nasaďte jeden ze skriptovacích balíčků, které jsme napsali a použili v našem prostředí, aby se snížily lístky podpory. Intune umožňuje zobrazit stav nasazených balíčků skriptu a monitorovat výsledky detekce a nápravy. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **sestavy**  >  **Endpoint analytics**  >  **proaktivní nápravy služby**Endpoint Analytics. Další informace najdete v tématu [proaktivní nápravy](https://aka.ms/uea_prs).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Používání ATP v programu Microsoft Defender v zásadách dodržování předpisů pro Android<!-- 4425686  -->

Teď můžete pomocí Intune připojit [zařízení s Androidem k Rozšířené ochraně před internetovými útoky v programu Microsoft Defender](../protect/advanced-threat-protection-configure.md#onboard-devices) (MicrosoftDefender ATP). Po zaregistrování registrovaných zařízení můžou zásady dodržování předpisů pro Android využívat signály *úrovně hrozby z ochrany* ATP v programu Microsoft Defender. Jedná se o stejné signály, které jste předtím mohli použít pro zařízení s Windows 10.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Konfigurace webové ochrany v programu Defender ATP pro zařízení s Androidem<!-- 6185563  -->

Při použití rozšířené ochrany před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) pro zařízení s Androidem můžete [nakonfigurovat ochranu ATP na webu Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md) , aby se zakázala funkce vyhledávání phishing, nebo zakázat kontrolu v používání sítě VPN.

V závislosti na tom, jak se zařízení s Androidem zaregistruje v Intune, jsou k dispozici tyto možnosti:

- Správce zařízení s Androidem – pomocí vlastního nastavení OMA-URI zakažte funkci webové ochrany nebo během kontrol zakážete jenom použití VPN.
- Pracovní profil Android Enterprise – pomocí konfiguračního profilu aplikace a návrháře konfigurace zakažte všechny možnosti webové ochrany.

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>Týden od 15. června 2020 (vydání služby 2006)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Ochrana přenosu dat pro spravované aplikace v telekomunikačních aplikacích<!-- 6884491  -->
Když se v chráněné aplikaci zjistí telefonní číslo s hypertextovými odkazy, Intune zkontroluje, jestli se nastavily zásady ochrany, které jim umožní přenášet číslo do aplikace pro vytáčené připojení. Můžete zvolit, jak se má tento typ přenosu obsahu zpracovat při zahájení z aplikace spravované zásadou. Při vytváření zásad ochrany aplikací v Microsoft Endpoint Manageru vyberte možnost spravovaná aplikace z **dat odeslat organizaci ostatním aplikacím**a pak vyberte možnost z **přenosu dat do**. Další informace o tomto nastavení ochrany dat najdete v tématu nastavení [zásad ochrany aplikací pro Android v](../apps/app-protection-policy-settings-android.md) tématu [nastavení zásad ochrany aplikací](../apps/app-protection-policy-settings-ios.md)pro Microsoft Intune a iOS. 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---7414033----"></a>Jednotné doručování aplikací Azure AD Enterprise a Office Online v systému Windows Portál společnosti<!-- 7414033  -->
V podokně **přizpůsobení** služby Intune můžete vybrat možnost **Skrýt** nebo **Zobrazit** **podnikové aplikace Azure AD** a **aplikace Office Online** v portál společnosti. Každý koncový uživatel uvidí ze zvolené služby Microsoftu celý katalog aplikací. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. Tato funkce se nejprve projeví na webu Portál společnosti, kde se očekává podpora Portál společnosti systému Windows. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **přizpůsobení správy tenanta**  >  **Customization** a najděte toto nastavení konfigurace. Související informace najdete v tématu [Postup přizpůsobení aplikací portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Vylepšení Portál společnosti možností registrace macOS<!-- 6444452  -->
Portál společnosti pro zápis do macOS má jednodušší proces registrace, který se podrobněji zarovnává s Portál společnostim pro možnosti registrace v iOS. Uživatelům zařízení se zobrazí:  
- Elegantní uživatelské rozhraní.  
- Vylepšený kontrolní seznam pro registraci.  
- Informace o tom, jak zaregistrovat svá zařízení.  
- Vylepšené možnosti řešení potíží.  

Další informace o Portál společnosti najdete v tématu [přizpůsobení aplikace Portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>Stránka vylepšení zařízení v portálech společnosti pro iOS/iPadOS a macOS<!-- 6055001 -->
Provedli jsme změny na stránce Portál společnosti **zařízení** , aby se vylepšilo prostředí aplikací pro uživatele se systémem iOS/IPadOS a Mac. Kromě toho, že jsme vytvořili mnohem moderní vzhled a atmosféru, jsme změnili uspořádání podrobností o zařízení v rámci jednoho sloupce s definovanými záhlavími oddílů, aby uživatelé viděli stav zařízení. Pro uživatele, jejichž zařízení nedodržují předpisy, jsme také přidali jasné zprávy a kroky pro řešení potíží. Další informace o Portál společnosti najdete v tématu [přizpůsobení aplikace Portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md). Postup ruční synchronizace zařízení najdete v tématu [Ruční synchronizace zařízení s iOS](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>Nastavení cloudu pro iOS/iPadOS Portál společnosti aplikaci<!-- 7071303  -->
Nové nastavení **cloudu** pro iOS/iPadOS portál společnosti umožňuje uživatelům přesměrovat ověřování do příslušného cloudu pro vaši organizaci. Ve výchozím nastavení je nastavení nakonfigurováno na **Automatické**, které směruje ověřování do cloudu automaticky zjištěného zařízením uživatele. Pokud se ověřování pro vaši organizaci musí přesměrovat do jiného cloudu, než je Cloud, který se automaticky detekuje (například veřejná nebo státní správa), můžou uživatelé ručně vybrat příslušný Cloud tak, že si vyberete **Nastavení** aplikace > **portál společnosti**  >  **cloudu**. Vaši uživatelé by měli změnit nastavení **cloudu** jenom z **automatického** , pokud se přihlásí z jiného zařízení a příslušný Cloud se nedetekuje automaticky podle zařízení. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Duplicitní tokeny programu Apple VPP<!-- 7101606  -->
Tokeny programu Apple VPP se stejným **umístěním tokenu** jsou teď označené jako **duplicitní** a dají se po odebrání duplicitního tokenu synchronizovat znovu. K tokenům, které jsou označené jako duplicitní, můžete i nadále přiřazovat licence a odvolat je. Licence pro nové aplikace a koupené knihy se ale neprojeví, když je token označený jako duplicitní. Pokud chcete najít tokeny programu Apple VPP pro vašeho tenanta, z [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte konektory **pro správu tenanta**  >  **a tokeny**  >  **Apple VPP**. Další informace o tokenech VPP najdete v tématu [Správa aplikací pro iOS a MacOS zakoupených prostřednictvím Apple Volume purchase program s Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>Přidání více kořenových certifikátů pro ověřování EAP-TLS v profilech sítě Wi-Fi na zařízeních macOS<!-- 2077871  -->

Na zařízeních MacOS můžete vytvořit profil Wi-Fi a vybrat typ ověřování protokolem EAP (Extensible Authentication Protocol) (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **MacOS** pro platformu > **Wi-Fi** pro cloudovou > **typ Wi-Fi** nastavenou na Enterprise).

Když nastavíte **typ protokolu EAP** na ověřování **EAP-TLS**, **EAP-TTLS**nebo **PEAP** , můžete přidat několik kořenových certifikátů. Dřív jste mohli přidat jenom jeden kořenový certifikát.

Další informace o nastaveních, která můžete konfigurovat, najdete v tématu [Přidání nastavení Wi-Fi pro zařízení MacOS v Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Platí pro:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Použití certifikátů PKCS se profily sítě Wi-Fi na Windows 10 a novějších zařízeních<!-- 3246388   -->
Profily Wi-Fi pro Windows můžete ověřit pomocí certifikátů SCEP (**Konfigurace zařízení**  >  **profily**  >  **vytvořit profil**  >  **Windows 10 a novější** pro Platform > **Wi-Fi** pro typ profilu > **Podnikový**  >  **typ protokolu EAP**). Nyní můžete použít certifikáty PKCS se profily sítě Windows Wi-Fi. Tato funkce umožňuje uživatelům ověřovat profily sítě Wi-Fi pomocí nových nebo existujících profilů certifikátů PKCS ve vašem tenantovi. 

Další informace o nastavení Wi-Fi, která můžete nakonfigurovat, najdete [v tématu Přidání nastavení Wi-Fi pro zařízení s Windows 10 a novějším v Intune](../configuration/wi-fi-settings-windows.md).

Platí pro:
- Windows 10 a novější

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profily konfigurace síťových zařízení s drátovou sítí pro zařízení macOS<!-- 3508686  -->
K dispozici je nový profil konfigurace zařízení MacOS, který konfiguruje drátové sítě (**Devices**  >  **konfigurační profily**zařízení  >  **vytvoří profil**  >  **MacOS** pro platformu > **kabelové sítě** pro profil). Pomocí této funkce můžete vytvořit profily 802.1 x ke správě drátových sítí a tyto drátové sítě nasadit do zařízení macOS.

Další informace o této funkci najdete v tématu [kabelové sítě na zařízeních MacOS](../configuration/wired-networks-configure.md).

Platí pro:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Jako výchozí spouštěcí spouštěč pro plně spravovaná zařízení s Androidem Enterprise použít spouštěč Microsoftu<!-- 4927976   -->
Na zařízeních pro vlastníka zařízení s Androidem Enterprise můžete nastavit spouštěč Microsoftu jako výchozí spouštěcí spouštěč pro plně spravovaná zařízení (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **pro zařízení profily**  >  **Device restrictions** pro > **prostředí zařízení**). Ke konfiguraci všech dalších nastavení spouštěče Microsoftu použijte [zásady konfigurace aplikací](../apps/configure-microsoft-launcher.md). 

Existují taky některé další aktualizace uživatelského rozhraní, včetně **vyhrazených zařízení** , která se přejmenují do **prostředí zařízení**.

Pokud chcete zobrazit všechna nastavení, která můžete omezit, přečtěte si téma [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md). 

Platí pro:
- Zařízení s plně spravovaným vlastníkem zařízení s Androidem Enterprise (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>Použít autonomní nastavení samostatného režimu aplikace ke konfiguraci aplikace Portál společnosti pro iOS na přihlášení a odhlášení aplikace<!-- 7055619   -->
V zařízeních s iOS/iPadOS můžete nakonfigurovat aplikace tak, aby běžely v autonomním režimu jedné aplikace (ASAM). Nyní aplikace Portál společnosti podporuje ASAM a lze ji nakonfigurovat tak, aby byla aplikací "přihlášení a odhlášení". V tomto režimu se uživatelé musí přihlašovat do aplikace Portál společnosti, aby mohli používat jiné aplikace a tlačítko na domovské obrazovce zařízení. Když se odhlásí z aplikace Portál společnosti, zařízení se vrátí do režimu jedné aplikace a zamkne se v Portál společnosti aplikaci.

Pokud chcete nakonfigurovat portál společnosti v Asam, přečtěte si v části **zařízení**  >  **konfigurační profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro **omezení** platformy > zařízení pro profil > **autonomní režim jedné aplikace**.

Další informace najdete v tématu [autonomní režim jedné aplikace (Asam)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) a [režim jedné aplikace](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (otevře web společnosti Apple).

Platí pro:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>Konfigurace ukládání obsahu do mezipaměti na zařízeních macOS<!-- 7106872   -->
Na zařízeních MacOS můžete vytvořit konfigurační profil, který konfiguruje ukládání obsahu do mezipaměti (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **MacOS** pro **funkce** platformy > pro profil). Pomocí těchto nastavení můžete odstranit mezipaměť, zapnout sdílenou mezipaměť, nastavit limit mezipaměti na disku a další.

Další informace o ukládání obsahu do mezipaměti najdete v tématu [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (otevření webu společnosti Apple).

Nastavení, která můžete nakonfigurovat, najdete [v tématu Nastavení funkcí zařízení MacOS v Intune](../configuration/macos-device-features-settings.md).

Platí pro:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Přidejte nová nastavení schématu a vyhledejte existující nastavení schématu pomocí OEMConfig v Androidu Enterprise.<!-- 6394386   -->
V Intune můžete použít OEMConfig ke správě nastavení na zařízeních s Androidem Enterprise (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **OEMConfig** for Profile). Když použijete **Návrháře konfigurace**, zobrazí se vlastnosti ve schématu aplikace. Nyní můžete v **Návrháři konfigurace**:

- Přidejte do schématu aplikace nová nastavení.
- Ve schématu aplikace vyhledejte nová a stávající nastavení.

Další informace o profilech OEMConfig v Intune najdete v tématu [používání a Správa zařízení s Androidem Enterprise pomocí OEMConfig v Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Platí pro:
- Android Enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Blokovat sdílené dočasné relace iPadu na sdílených zařízeních iPad<!-- 6613794  -->
V Intune je k dispozici nový **blok sdílené dočasné relace pro iPad** , který blokuje dočasné relace na sdílených zařízeních iPadu (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro > **omezení zařízení** pro typ profilu > **sdíleného iPadu**). Pokud je tato možnost povolená, koncoví uživatelé nemůžou používat účet hosta. Musí se přihlásit k zařízení pomocí spravovaného Apple ID a hesla. 

Další informace najdete v tématu [nastavení zařízení s iOS a iPadOS, která umožňují povolit nebo zakázat funkce](../configuration/device-restrictions-ios.md).

Platí pro:
- Sdílená zařízení iPad s iOS/iPadOS 13,4 a novějšími

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>Vlastní zařízení můžou používat k nasazení sítě VPN.<!--5015344  -->
Nový profil pro **přeskočení kontroly připojení k doméně** pomocí nového profilu autopilotu přeskočit přepínač umožňuje nasadit hybridní zařízení služby Azure AD join bez přístupu k podnikové síti pomocí vašeho vlastního klienta Win32 VPN od jiného výrobce. Pokud se chcete podívat na nový přepínač, přejděte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**   >  **Windows**  >  **Windows enrollment**  >  **profily nasazení**registrace  >  **vytvořit profil**předspouštěného  >  **prostředí (OOBE)**.

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Profily stránky stavu registrace se dají nastavit na skupiny zařízení.<!--3952138 -->
Dříve mohli profily na stránce stavu registrace (ESP) cílit jenom na skupiny uživatelů. Nyní je můžete nastavit také na cílové skupiny zařízení. Další informace najdete v tématu [nastavení stránky stavu registrace](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Automatizované chyby synchronizace registrace zařízení<!-- 6988214 -->
Pro zařízení s iOS/iPadOS a macOS se budou hlásit nové chyby, včetně
- Telefonní číslo obsahuje neplatné znaky nebo je toto pole prázdné. 
- Neplatný nebo prázdný název konfigurace pro profil. 
- Neplatná hodnota kurzoru/neplatné nebo, pokud se nenajde žádný kurzor.
- Odmítnuto nebo vypršela platnost tokenu. 
- Pole oddělení je prázdné nebo je jeho délka příliš dlouhá. 
- V Apple se nenašel profil a je potřeba vytvořit nový. 
- Počet odebraných zařízení Apple Business Manageru se přidá na stránku Přehled, kde vidíte stav svých zařízení.

#### <a name="shared-ipads-for-business--6367326-----"></a>Shared iPady for Business<!--6367326   -->
Službu Intune a Apple Business Manager můžete použít ke snadnému a bezpečnému nastavení sdíleného iPadu tak, aby zařízení mohla sdílet více zaměstnanců. [Sdílený iPad](https://developer.apple.com/education/shared-ipad/) společnosti Apple nabízí individuální prostředí pro více uživatelů při zachování uživatelských dat. Pomocí spravovaného Apple ID můžou uživatelé získat přístup k aplikacím, datům a nastavením po přihlášení ke všem sdíleným iPadům v jejich organizaci. Sdílený iPad spolupracuje se federované identity.

Tuto funkci zobrazíte tak, že přejdete na [Centrum pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**.  >  **iOS**  >  **iOS enrollment**  >  **tokeny programu**registrace iOS  >  **zvolit profily tokenů**  >  **Profiles**  >  **vytvořit profil**  >  **iOS**. Na stránce **Nastavení správy** vyberte **zaregistrovat bez přidružení uživatele** a zobrazí se možnost **sdílené iPady** .

Vyžaduje: iPadOS 13,4 a novější. Tato verze přidala podporu pro dočasné relace se sdíleným iPadem, takže uživatelé budou mít přístup k zařízení bez spravovaného Apple ID. Po odhlášení zařízení vymaže všechna uživatelská data, aby bylo zařízení hned připravené k použití, což eliminuje nutnost vymazání zařízení. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Aktualizované uživatelské rozhraní pro automatizované registrace zařízení společnosti Apple<!--7430322 -->
Uživatelské rozhraní bylo aktualizováno, aby nahradilo Program registrace zařízení od Applu k automatizované registraci zařízení, aby odráželo terminologii Apple.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>PIN kód pro vzdálené uzamčení zařízení je k dispozici pro macOS<!--7281557   -->
Dostupnost pro vzdálené zámky zařízení macOS se zvýšila z 7 dnů na 30 dnů.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Změna primárního uživatele na spoluspravovaných zařízeních<!--7319183  -->
Pro spoluspravovaná zařízení s Windows můžete změnit primárního uživatele zařízení. Další informace o tom, jak ho najít a změnit, najdete v tématu [vyhledání primárního uživatele zařízení v Intune](../remote-actions/find-primary-user.md). Tato funkce se bude postupně nacházet během několika dalších týdnů.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Nastavení primárního uživatele Intune také nastaví vlastnost Owner služby Azure AD.<!--7319227 -->
Tato nová funkce automaticky nastaví vlastnost Owner u nově zaregistrovaných zařízení připojených k hybridní službě Azure AD současně s nastaveným primárním uživatelem Intune. Další informace o primárním uživateli najdete v tématu [vyhledání primárního uživatele zařízení v Intune](../remote-actions/find-primary-user.md).

Toto je změna procesu registrace a vztahuje se jenom na nově zaregistrovaná zařízení. Pro existující zařízení připojená k hybridní službě Azure AD musíte ručně aktualizovat vlastnost vlastníka Azure AD. K tomu můžete použít [funkci změnit primárního uživatele](../remote-actions/find-primary-user.md#change-a-devices-primary-user) nebo [skript](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

Když se zařízení s Windows 10 stanou připojenými k adresáři Azure Azure Hybrid, stane se prvním uživatelem tohoto zařízení primárním uživatelem ve Správci koncových bodů.  V současné době se uživatel nenastavuje na odpovídajícím objektu zařízení Azure AD. To způsobuje nekonzistenci při porovnání vlastnosti *Owner* z portálu Azure AD s vlastností *primárního uživatele* v centru pro správu služby Microsoft Endpoint Manager. Vlastnost Owner služby Azure AD se používá pro zabezpečení přístupu k klíčům pro obnovení BitLockeru. Tato vlastnost není naplněná na zařízeních připojených k hybridní službě Azure AD. Toto omezení brání nastavení samoobslužného obnovení BitLockeru ze služby Azure AD. Tato funkce toto omezení řeší.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>Skrýt obnovovací klíč od uživatelů během šifrování trezoru 2 pro zařízení macOS<!-- 5459801  -->
Do kategorie *trezoru úložišť* jsme přidali nové nastavení v rámci šablony [MacOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) : **skryjte obnovovací klíč**. Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. 

Chcete-li zobrazit osobní obnovovací klíč šifrovaného zařízení macOS, může uživatel zařízení přejít do některého z následujících umístění a kliknout na tlačítko *získat obnovovací klíč* pro zařízení MacOS: 

- Aplikace Portál společnosti pro iOS/iPadOS
- Aplikace Intune
- Web portálu společnosti
- Aplikace Portál společnosti pro Android

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Podpora podpisových a šifrovacích certifikátů S/MIME s Outlookem v plně spravovaném Androidu<!--5896415   -->
Nyní můžete používat certifikáty pro podepisování S/MIME a šifrování pomocí Outlooku na zařízeních, na kterých běží plně spravovaná platforma Android Enterprise.

Tím se rozšíří podpora přidaná za poslední měsíc pro jiné verze Androidu (podpora podpisových a šifrovacích certifikátů S aplikací s Outlookem v Androidu). Tyto certifikáty můžete zřídit pomocí profilů certifikátů SCEP a PKCS.

Další informace o této podpoře najdete v tématu [citlivostní označování a ochrana v Outlooku pro iOS a Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) v dokumentaci k Exchangi.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Přidání odkazu na web podpory portálu společnosti na e-maily při nedodržení předpisů<!-- 7225498    -->
Když [nakonfigurujete šablonu zprávy s oznámením](../protect/actions-for-noncompliance.md#create-a-notification-message-template) pro odesílání e-mailových oznámení o nedodržení předpisů, použijte nové nastavení **portál společnosti odkaz na web** , který automaticky zahrne odkaz na portál společnosti Web. Když je tato možnost nastavená na *Povolit*, můžou uživatelé s nekompatibilními zařízeními, kteří přijímají e-mail na základě této šablony, použít odkaz k otevření webu, kde se dozvíte víc o tom, proč jejich zařízení nedodržuje předpisy. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Licensing

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Správci už nepotřebují licenci Intune pro přístup ke konzole pro správu Microsoft Endpoint Manageru.<!--1335430 -->
Teď můžete nastavit přepínač na úrovni tenanta, který odebere licenční požadavek Intune pro správce pro přístup k konzole správce paměti a rozhraní API pro grafy dotazů. Po odebrání licenčního požadavku ho nikdy nemůžete obnovit. 


> [!Note]
> Některé akce, včetně toku konektoru pro TeamViewer, ještě vyžadují licenci na Intune.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Skripty 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>Dostupnost skriptů prostředí na zařízeních macOS<!-- 7134839  -->
Skripty prostředí pro zařízení macOS jsou teď dostupné pro státní Cloud a čínské zákazníky. Další informace o skriptech prostředí najdete v tématu [použití skriptů prostředí v zařízeních MacOS v Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>Týden od 8. června 2020   

### <a name="app-management"></a>Správa aplikací  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>Aktualizace informativní obrazovky v Portál společnosti pro iOS/iPadOS <!--7032452 -->
Informační obrazovka v Portál společnosti pro iOS/iPadOS se aktualizovala, aby lépe vysvětlil, co správce může zobrazit a dělat na zařízeních. Tato objasnění se týkají pouze zařízení vlastněných společností. Aktualizovali jsme jenom text, neudělaly se žádné skutečné úpravy, které správce uvidí nebo na uživatelských zařízeních nevidí. Aktualizované obrazovky zobrazíte tak, že přejdete na [aktualizace uživatelského rozhraní pro aplikace Intune pro koncové uživatele](./whats-new-app-ui.md).

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Aktualizovaná činnost podmíněného spuštění aplikace pro Android a činnost koncového uživatele<!-- 5736084 -->
Verze 2006 Portál společnosti pro Android obsahuje změny, které jsou sestavené s aktualizacemi ze verze 2005. V 2005 jsme zavedli aktualizaci, kde koncoví uživatelé zařízení se systémem Android, kteří vystavili upozornění, zablokování nebo vymazání pomocí zásad ochrany aplikací, uvidí celou stránku s popisem důvodu upozornění, blokování nebo vymazání a kroků k nápravě problémů. V 2006 se uživatelé aplikací pro Android, kteří mají přiřazenou zásadu ochrany aplikací, provedou pomocí průvodce, aby opravili problémy, které způsobují zablokování přístupu k aplikaci. 



## <a name="whats-new-archive"></a>Archiv co je nového
V předchozích měsících se podívejte do [archivu co je nového](whats-new-archive.md).

## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
