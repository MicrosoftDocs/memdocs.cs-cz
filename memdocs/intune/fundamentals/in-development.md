---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5fb4bfba0dbcdfe28b2fbce8123b0e2e919fd308
ms.sourcegitcommit: e618ea7cb864635c838b672bc71a1e926bf7c047
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2020
ms.locfileid: "84458083"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>Stránka vylepšení zařízení v portálech společnosti pro iOS/iPadOS a macOS<!-- 6055001  -->
Provedli jsme několik vylepšení uživatelského prostředí na stránce **zařízení** v aplikaci Portál společnosti pro iOS/IPadOS a Mac. Přepracovanéi jsme stránku **zařízení** , která bude mít moderní dojem a lepší organizaci informací o zařízení. Pomocí jednoho sloupce s definovanými hlavičkami oddílů budou uživatelé iOS/iPadOS a macOS vaší organizace moct snadno zkontrolovat stav svých zařízení, aby se zajistila bezpečnost a udržoval přístup k prostředkům jejich organizace. Kromě toho jsme přidali pro uživatele, u kterých zařízení nedodržuje předpisy, i další kroky pro řešení potíží. Další informace o Portál společnosti najdete v tématu [přizpůsobení aplikace Portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Vylepšení Portál společnosti možností registrace macOS<!-- 6444452  -->
Portál společnosti pro registraci v macOS bude mít jednodušší proces registrace, který se podrobněji zarovnává s Portál společnostim pro možnosti registrace v iOS. Uživatelům zařízení se zobrazí:  
- Elegantní uživatelské rozhraní.  
- Vylepšený kontrolní seznam pro registraci.  
- Informace o tom, jak zaregistrovat svá zařízení.  
- Vylepšené možnosti řešení potíží.  

Další informace o Portál společnosti najdete v tématu [přizpůsobení aplikace Portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>Použít autonomní nastavení samostatného režimu aplikace ke konfiguraci Portál společnosti pro iOS jako aplikace pro přihlášení a odhlášení<!-- 7055619  -->
Portál společnosti pro iOS budete moct nakonfigurovat tak, aby používala autonomní režim jedné aplikace (ASAM). Pomocí nastavení ASAM v konzole Microsoft Endpoint Manager můžete nakonfigurovat iOS Portál společnosti, aby se v režimu jedné aplikace přešel a odhlásily po odhlášení a přihlášení. Když je Portál společnosti v ASAM, nebudou moct uživatelé na zařízení používat žádnou jinou aplikaci ani tlačítko domů, dokud se nebudou přihlašovat k Portál společnosti. Po odhlášení se Portál společnosti vrátí do režimu jedné aplikace. 

Pokud chcete nakonfigurovat portál společnosti v Asam ve Správci Microsoft Endpoint Manager, vyberte **zařízení**  >  **Konfigurace profily**  >  **vytvořit profil**. Jako platformu vyberte **iOS/iPadOS** a jako profil vyberte **omezení zařízení** . Na kartě **nastavení konfigurace** vyberte **autonomní režim jedné aplikace**. Nastavte **název aplikace** na `Company Portal` a nastavte **ID sady prostředků aplikace** na `com.app.CompanyPortal` . Další informace najdete v tématu [autonomní režim jedné aplikace (Asam)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) a [režim jedné aplikace](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Nastavit stav dodržování předpisů zařízením od partnerů MDM třetích stran<!-- 6361689   -->
Microsoft 365 zákazníci, kteří vlastní řešení MDM třetí strany, budou moci vyhovět zásadám podmíněného přístupu pro aplikace Microsoft 365 v iOS a Androidu prostřednictvím integrace se službou Microsoft Intune dodržování předpisů zařízením. Dodavatel MDM třetí strany bude využívat službu Intune pro dodržování předpisů zařízením k odesílání dat o dodržování předpisů zařízením do Intune. Intune se pak vyhodnotí a určí, jestli je zařízení důvěryhodné, a nastavte atributy podmíněného přístupu ve službě Azure AD.  Zákazníci budou muset nastavit zásady podmíněného přístupu Azure AD z centra pro správu Microsoft Endpoint Manageru nebo z portálu Azure AD.  

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Přidání odkazu na web podpory portálu společnosti na e-maily při nedodržení předpisů<!-- 7225498    -->
Do šablony e-mailových oznámení přidáváme nové nastavení, které přidá odkaz na web portál společnosti a pošle e-mailová oznámení, která se odesílají uživatelům nevyhovujících zařízení. (**Zabezpečení**  >  koncového bodu **Dodržování předpisů zařízením**  >  **Oznámení**  >  **Vytvořit oznámení**).  Uživatelé, kteří obdrží e-mail, protože zařízení, které nedodržuje předpisy, může pomocí odkazu otevřít web a získat další informace o tom, proč jejich zařízení nedodržuje předpisy.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nové nastavení trezoru úložiště pro macOS Endpoint Protection zásady konfigurace zařízení<!-- 5459801   -->
Do kategorie trezoru úložišť přidáváme nové nastavení v rámci šablony [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) : skryjte obnovovací klíč. (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořte profil**, pro danou *platformu* vyberte **MacOS** a pak jako *typ profilu*nastavte **Endpoint Protection** ). Toto nastavení skrývá osobní klíč od koncového uživatele během šifrování trezoru 2. Uživatel zařízení si může svůj osobní obnovovací klíč kdykoli zobrazit z aplikace Portál společnosti pro iOS nebo z webu portál společnosti pro šifrované zařízení macOS. Pokud si chcete zobrazit klíč pro osobní obnovení, můžete přejít na podrobnosti o zařízení a kliknout na *získat obnovovací klíč*.

Toto nastavení nebude k dispozici v dříve vytvořených zásadách. Abyste mohli nakonfigurovat toto nastavení tak, aby ho bylo možné používat, budete muset znovu vytvořit zásady trezoru úložišť. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>Konfigurace ukládání obsahu do mezipaměti na zařízeních macOS<!-- 7106872 -->
Na zařízeních MacOS můžete vytvořit konfigurační profil, který konfiguruje ukládání obsahu do mezipaměti (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **MacOS** pro **funkce** platformy > pro profil). Pomocí těchto nastavení můžete odstranit mezipaměť, zapnout sdílenou mezipaměť, nastavit limit mezipaměti na disku a další.

Další informace o ukládání obsahu do mezipaměti najdete v tématu [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (otevření webu společnosti Apple).

Pokud se chcete podívat na nastavení, která můžete konfigurovat, přejděte do části [Nastavení funkcí zařízení MacOS v Intune](../configuration/macos-device-features-settings.md).

Platí pro:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nové nastavení sítě VPN pro zařízení s Windows 10 a novějšími systémy<!-- 6602122  -->
Když vytváříte profil sítě VPN pomocí typu připojení IKEv2, můžete nakonfigurovat nová nastavení. (**Devices**  >  **konfigurační profily**zařízení  >  **vytvořit profil**  >  **Windows 10 a novější** pro platformu > **VPN** pro > **základní síť VPN**):

- **Tunelové zařízení**: umožňuje zařízení automaticky se připojovat k síti VPN bez nutnosti zásahu uživatele, včetně přihlášení uživatele. Tato funkce vyžaduje, abyste povolili funkci **Always On**a jako metodu ověřování používali **certifikáty počítače** .
- Nastavení kryptografie: umožňuje nakonfigurovat algoritmy používané k zabezpečení IKE a podřízená přidružení zabezpečení, která vám umožní odpovídat nastavení klienta a serveru.

Pokud chcete zobrazit nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Windows a přidejte připojení k síti VPN pomocí Intune](../configuration/vpn-settings-windows-10.md).

Platí pro:
- Windows 10 a novější

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Blokovat sdílené dočasné relace iPadu na sdílených zařízeních iPad<!-- 6613794 -->
V Intune je k dispozici nový **blok sdílené dočasné relace pro iPad** , který blokuje dočasné relace na sdílených zařízeních iPadu (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro > **omezení zařízení** pro typ profilu > **sdíleného iPadu**). Pokud je tato možnost povolená, koncoví uživatelé nemůžou používat účet hosta. Musí se přihlásit k zařízení pomocí spravovaného Apple ID a hesla. 

Další informace o nastaveních, která můžete konfigurovat, najdete v tématu [nastavení zařízení s iOS a iPadOS, které umožňuje povolit nebo zakázat funkce](../configuration/device-restrictions-ios.md).

Platí pro:
- Sdílená zařízení iPad s iOS/iPadOS 13,4 a novějšími

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Jako výchozí spouštěcí spouštěč pro plně spravovaná zařízení s Androidem Enterprise použít spouštěč Microsoftu<!-- 4927976  -->
Na zařízeních pro vlastníka zařízení s Androidem Enterprise můžete nastavit spouštěč Microsoftu jako výchozí spouštěcí spouštěč pro plně spravovaná zařízení (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **pro zařízení profily**  >  **Device restrictions** pro > **prostředí zařízení**). Ke konfiguraci všech dalších nastavení spouštěče Microsoftu použijte zásady konfigurace aplikací. 

Existují taky některé další aktualizace uživatelského rozhraní, včetně **vyhrazených zařízení** , která se přejmenují do **prostředí zařízení**.

Pokud chcete zobrazit všechna nastavení, která můžete omezit, přečtěte si téma [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md). 

Platí pro:
- Zařízení s plně spravovaným vlastníkem zařízení s Androidem Enterprise (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Přidejte nová nastavení schématu a vyhledejte existující nastavení schématu pomocí OEMConfig v Androidu Enterprise.<!-- 6394386  -->
V Intune můžete použít OEMConfig ke správě nastavení na zařízeních s Androidem Enterprise (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **OEMConfig** for Profile). Když použijete **Návrháře konfigurace**, zobrazí se vlastnosti ve schématu aplikace. Nyní můžete v **Návrháři konfigurace**:
- Přidejte do schématu aplikace nová nastavení.
- Ve schématu aplikace vyhledejte nová a stávající nastavení.

Další informace o profilech OEMConfig v Intune najdete v tématu [používání a Správa zařízení s Androidem Enterprise pomocí OEMConfig v Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Platí pro:
- Android Enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrace zařízení

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Automatizované chyby synchronizace registrace zařízení<!-- 6988214 -->
Pro zařízení s iOS/iPadOS a macOS se budou hlásit nové chyby, včetně
- Telefonní číslo obsahuje neplatné znaky nebo je toto pole prázdné. 
- Neplatný nebo prázdný název konfigurace pro profil. 
- Neplatná hodnota kurzoru/neplatné nebo, pokud se nenajde žádný kurzor.
- Odmítnuto nebo vypršela platnost tokenu. 
- Pole oddělení je prázdné nebo je jeho délka příliš dlouhá. 
- V Apple se nenašel profil a je potřeba vytvořit nový. 
- Počet odebraných zařízení Apple Business Manageru se přidá na stránku Přehled, kde vidíte stav svých zařízení.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Vlastní zařízení můžou používat k nasazení sítě VPN.<!--5015344 -->
Nový profil pro **přeskočení kontroly připojení k doméně** pomocí nového profilu autopilotu přeskočit přepínač umožňuje nasadit hybridní zařízení služby Azure AD join bez přístupu k podnikové síti pomocí vašeho vlastního klienta Win32 VPN od jiného výrobce. Pokud se chcete podívat na nový přepínač, přejděte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**   >  **Windows**  >  **Windows enrollment**  >  **profily nasazení**registrace  >  **vytvořit profil**předspouštěného  >  **prostředí (OOBE)**.

### <a name="shared-ipads-for-business--6367326---"></a>Shared iPady for Business<!--6367326 -->
Pomocí Intune a Apple Business Manageru budete moct snadno a bezpečně nastavit sdílený iPad, aby zařízení mohla sdílet víc zaměstnanců. [Sdílený iPad](https://developer.apple.com/education/shared-ipad/) společnosti Apple nabízí individuální prostředí pro více uživatelů při zachování uživatelských dat. Pomocí spravovaného Apple ID můžou uživatelé získat přístup k aplikacím, datům a nastavením po přihlášení ke všem sdíleným iPadům v jejich organizaci. Sdílený iPad spolupracuje se federované identity.

Tuto funkci zobrazíte tak, že přejdete na [Centrum pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**.  >  **iOS**  >  **iOS enrollment**  >  **tokeny programu registrace** iOS > zvolit token > **profily**  >  **vytvořit profil**  >  **iOS**. Na stránce **Nastavení správy** vyberte **zaregistrovat bez přidružení uživatele** a zobrazí se možnost **sdílené iPady** .

**Platí pro:** iPadOS 13,4 a novější. Tato verze přidala podporu pro dočasné relace se sdíleným iPadem, takže uživatelé budou mít přístup k zařízení bez spravovaného Apple ID. Po odhlášení zařízení vymaže všechna uživatelská data, aby bylo zařízení hned připravené k použití, což eliminuje nutnost vymazání zařízení. 

<!-- ***********************************************-->
## <a name="device-management"></a>Správa zařízení

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Změna primárního uživatele na spoluspravovaných zařízeních<!--7319183 -->
Pro spoluspravovaná zařízení s Windows budete moct změnit primárního uživatele zařízení. Další informace o tom, jak ho najít a změnit, najdete v tématu [vyhledání primárního uživatele zařízení v Intune](../remote-actions/find-primary-user.md).

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Podpora skriptů PowerShellu pro zařízení BYOD<!-- 1862833  -->
PowerShellové skripty budou podporovat registrovaná zařízení Azure AD v Intune. Další informace o PowerShellu najdete [v tématu použití skriptů PowerShellu na zařízeních s Windows 10 v Intune](../apps/intune-management-extension.md). Tato funkce nepodporuje zařízení s Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bude zahrnovat protokol podrobností o zařízení.<!--6014987  -->
V **sestavách**  >  **Log Analytics**budou k dispozici protokoly podrobností o zařízeních v Intune. Můžete korelovat podrobnosti o zařízení a vytvářet vlastní dotazy a sešity Azure.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Nastavení primárního uživatele Intune také nastaví vlastnost Owner služby Azure AD.<!--7319227 -->
Tato nadcházející funkce automaticky nastaví vlastnost Owner u nově zaregistrovaných zařízení připojených k hybridní službě Azure AD současně s nastaveným primárním uživatelem Intune. Další informace o primárním uživateli najdete v tématu [vyhledání primárního uživatele zařízení v Intune](../remote-actions/find-primary-user.md).

Toto je změna procesu registrace a vztahuje se jenom na nově zaregistrovaná zařízení. Pro existující zařízení připojená k hybridní službě Azure AD musíte ručně aktualizovat vlastnost vlastníka Azure AD. K tomu můžete použít [funkci změnit primárního uživatele](../remote-actions/find-primary-user.md#change-a-devices-primary-user) nebo [skript](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

Když se zařízení s Windows 10 stanou připojenými k adresáři Azure Azure Hybrid, stane se prvním uživatelem tohoto zařízení primárním uživatelem ve Správci koncových bodů.  V současné době se uživatel nenastavuje na odpovídajícím objektu zařízení Azure AD. To způsobuje nekonzistenci při porovnání vlastnosti *Owner* z portálu Azure AD s vlastností *primárního uživatele* v centru pro správu služby Microsoft Endpoint Manager. Vlastnost Owner služby Azure AD se používá pro zabezpečení přístupu k klíčům pro obnovení BitLockeru. Tato vlastnost není naplněná na zařízeních připojených k hybridní službě Azure AD. Toto omezení brání nastavení samoobslužného obnovení BitLockeru ze služby Azure AD. Tato funkce toto omezení řeší.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Připojení tenanta: časová osa zařízení v centru pro správu<!--7220536, CM7141381 -->
Když Configuration Manager synchronizuje zařízení s Microsoft Endpoint Managerem prostřednictvím připojení tenanta, budete moct zobrazit časovou osu událostí. Tato časová osa zobrazuje minulou aktivitu v zařízení, která vám může pomoct při řešení problémů. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Připojení tenanta: instalace aplikace z centra pro správu<!-- 7220536, CM6024389 -->
Instalaci aplikace můžete zahájit v reálném čase pro zařízení připojené k tenantovi z centra pro správu služby Microsoft Endpoint Management. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Připojení tenanta: CMPivot z centra pro správu<!--7220536, CM6024392 -->
Budete moct využít sílu [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) do centra pro správu Microsoft Endpoint Manageru. Umožněte dalším osoby, jako je helpdesk, aby bylo možné iniciovat dotazy v reálném čase z cloudu proti jednotlivým zařízením spravovaným nástrojem ConfigMgr a vracet výsledky zpátky do centra pro správu. To poskytuje všechny tradiční výhody CMPivot, které správcům IT a dalším určeným osoby schopnost rychle vyhodnotit stav zařízení ve svém prostředí a provést akci. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Připojení tenanta: spuštění skriptů z centra pro správu<!--7220536, CM6234688 -->
Do centra pro správu služby Microsoft Endpoint Manager budete moct využít sílu Configuration Manager funkce místního [spouštění skriptů](../../configmgr/apps/deploy-use/create-deploy-scripts.md) . Povolí další osoby, jako je helpdesk, aby se spouštěly skripty PowerShellu z cloudu proti jednotlivým Configuration Manager spravovaným zařízením. To poskytuje všechny tradiční výhody skriptů PowerShellu, které již byly definovány a schváleny správcem Configuration Manager k tomuto novému prostředí. Další informace najdete v tématu [Configuration Manager Technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nová logika sloučení pro zařízení s Windows 10<!--179048-->
Pokud se dnes zákazník znovu pokusí vytvořit kopii zařízení a pak ho znovu zaregistruje, zobrazí se v konzole pro správu Microsoft Endpoint Manageru víc záznamů pro toto zařízení. Nová logika sloučení je ve vývoji ke sloučení takových duplicitních záznamů pro zařízení s Windows 10.

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>Dostupnost PIN kódu vzdáleného zámku pro zařízení macOS<!--7281557-->
Dostupnost kódů PIN vzdáleného zámku pro zařízení macOS se zvýší z 7 dnů na 30 dnů.

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
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
