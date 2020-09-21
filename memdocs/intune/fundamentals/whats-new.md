---
title: Novinky v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Zjistěte, jaké novinky přináší portál Intune Azure.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/17/2020
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
ms.openlocfilehash: 0561a7f7615b4f8aee8fd60b2b2b2481923c07ff
ms.sourcegitcommit: eaa077aa028a76a4873e4aa7437888f901a7e77f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90767141"
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
## <a name="week-of-september-14-2020"></a>Týden od 14. září 2020
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861-wnready---"></a>Jednotné doručování aplikací Azure AD Enterprise a Office Online v systému Windows Portál společnosti<!-- 1817861 wnready -->
Ve verzi 2006 jsme na [webu portál společnosti představili jednotné doručování aplikací Azure AD Enterprise a Office Online](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal). Tato funkce je podporovaná ve Windows Portál společnosti. V podokně **vlastní nastavení** Intune vyberte možnost **Skrýt** nebo **Zobrazit** **podnikové aplikace Azure AD** a **aplikace Office Online** ve Windows portál společnosti. Každý koncový uživatel uvidí ze zvolené služby Microsoftu celý katalog aplikací. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **přizpůsobení správy tenanta**  >  **Customization** a najděte toto nastavení konfigurace. Související informace najdete v tématu [Postup přizpůsobení aplikací portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-september-7-2020"></a>Týden od 7. září 2020
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="tenant-attach-device-timeline-in-the-admin-center"></a>Připojení tenanta: časová osa zařízení v centru pro správu
<!--7220536, CM7141381-->
Když Configuration Manager synchronizuje zařízení s Microsoft Endpoint Managerem prostřednictvím připojení tenanta, budete moct zobrazit časovou osu událostí. Tato časová osa zobrazuje minulou aktivitu v zařízení, která vám může pomoct při řešení problémů. Další informace najdete v tématu [připojení klienta: časová osa zařízení v centru pro správu](../../configmgr/tenant-attach/timeline.md).

#### <a name="tenant-attach-resource-explorer-in-the-admin-center"></a><a name="bkmk_hinv"></a> Připojení tenanta: Průzkumník prostředků v centru pro správu
<!--IN7220536, CM6479284 -->
V centru pro správu Microsoft Endpoint Management můžete zobrazit inventář hardwaru pro nahraná Configuration Manager zařízení pomocí Průzkumníka prostředků. Další informace najdete v tématu věnovaném [připojení klienta: Průzkumník prostředků v centru pro správu](../../configmgr/tenant-attach/resource-explorer.md).

#### <a name="tenant-attach-cmpivot-from-the-admin-center"></a>Připojení tenanta: CMPivot z centra pro správu
<!--IN7220536, CM6024392-->
Využijte sílu CMPivot do centra pro správu služby Microsoft Endpoint Manager. Umožněte dalším osoby, jako je helpdesk, aby bylo možné iniciovat dotazy v reálném čase z cloudu proti jednotlivým zařízením spravovaným nástrojem ConfigMgr a vracet výsledky zpátky do centra pro správu. To poskytuje všechny tradiční výhody CMPivot, které správcům IT a dalším určeným osoby schopnost rychle vyhodnotit stav zařízení ve svém prostředí a provést akci.

Další informace o CMPivot z centra pro správu najdete v tématu [CMPivot požadavky](../../configmgr/tenant-attach/cmpivot-start.md), [CMPivot Overview](../../configmgr/tenant-attach/cmpivot-overview-attached.md)a [CMPivot Sample Scripts](../../configmgr/tenant-attach/cmpivot-samples-attached.md).

## <a name="week-of-august-31-2020"></a>Týden od 31. srpna 2020

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="new-version-of-the-pfx-certificate-connector-and-changes-for-pkcs-certificate-profile-support-----4839686----"></a>Nová verze konektoru certifikátů PFX a změny pro podporu profilu certifikátu PKCS <!--  4839686  -->

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
Power BI šablonových aplikací umožňují Power BI partnerům vytvářet Power BI aplikace s malým nebo žádným kódováním a nasazovat je na jakéhokoli Power BIho zákazníka. Správci mohou aktualizovat verzi šablony sestavy dodržování předpisů Power BI z verze 1.0 až V 2.0. Verze 2.0 zahrnuje vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Další informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md) a [aktualizace šablony aplikace](/power-bi/service-template-apps-install-distribute#update-a-template-app). Další informace najdete v blogovém příspěvku [s oznámením o nové verzi sestavy dodržování předpisů Power BI s datovým skladem Intune](https://aka.ms/new_compliance_report).

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

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Jednotné doručování aplikací Azure AD Enterprise a Office Online v Portál společnosti<!-- 7414033  -->
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
### <a name="licensing"></a>Licencování

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

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>Týden od 25. května 2020

### <a name="app-management"></a>Správa aplikací

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>Windows 32 – bitové (x86) aplikace na zařízeních ARM64<!-- 5477661 -->
Aplikace Windows 32-bit (x86), které jsou nasazeny jako dostupné pro zařízení ARM64, se teď zobrazí v Portál společnosti. Další informace o Windows 32-bitových aplikacích najdete v tématu [Správa aplikací Win32](../apps/apps-win32-app-management.md).

#### <a name="windows-company-portal-app-icon---7114635---"></a>Ikona aplikace pro Windows Portál společnosti<!-- 7114635 -->
Změnila se ikona aplikace Portál společnosti pro Windows. Další informace o Portál společnosti najdete v tématu [přizpůsobení aplikace Portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>Týden od 18. května 2020

### <a name="app-management"></a>Správa aplikací  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>Aktualizace ikon v aplikaci Portál společnosti pro iOS/iPadOS a macOS<!--6057697 -->
V Portál společnosti jsme aktualizovali ikony, aby bylo možné vytvořit pokročilejší vzhled a chování, které se podporuje na zařízeních s duální obrazovkou a zarovnává se se systémem Microsoft Fluent design System. Aktualizované ikony zobrazíte tak, že přejdete na [aktualizace uživatelského rozhraní pro aplikace Intune pro koncové uživatele](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Použití zjišťování koncových bodů a zásad odezvy k zapojení zařízení do ATP pro Defender<!-- 7130165  -->

Zásady zabezpečení koncového bodu [pro zjišťování koncových bodů a odpověď](../protect/endpoint-security-edr-policy.md) (EDR) použijte k připojení a konfiguraci zařízení pro nasazení aplikace Microsoft Defender Advanced Threat Protection (Defender ATP). EDR podporuje zásady pro zařízení s Windows spravovaná přes Intune (MDM) a samostatné zásady pro zařízení s Windows spravovaná pomocí Configuration Manager. 

Pokud chcete používat zásady pro Configuration Manager zařízení, musíte [nastavit Configuration Manager pro podporu zásad EDR](../protect/tenant-attach-intune.md). Nastavení zahrnuje:

- Nakonfigurujte Správce konfigurace pro *připojení tenanta*.
- Pokud chcete povolit podporu zásad EDR, nainstalujte konzolovou aktualizaci pro Configuration Manager. Tato aktualizace se vztahuje jenom na hierarchie, které mají povolené *připojení tenanta*.
- Synchronizujte svoje kolekce zařízení s vaší hierarchií do centra pro správu služby Microsoft Endpoint Manager.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Týden od 11. května 2020 (2005 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Přizpůsobení akcí zařízení samoobslužných služeb v Portál společnosti<!--4393379 -->
Můžete přizpůsobit dostupné akce samoobslužného zařízení, které se zobrazí koncovým uživatelům v aplikaci Portál společnosti a na webu. Aby se zabránilo nezamýšleným akcím zařízení, můžete nakonfigurovat tato nastavení pro aplikaci Portál společnosti tak, že vyberete možnost přizpůsobení **správy tenanta**  >  **Customization**. K dispozici jsou následující akce:
- Skrýt tlačítko **Odebrat** na podnikovém zařízení s Windows
- Skrýt tlačítko pro **obnovení** na podnikových zařízeních s Windows
- Skrýt tlačítko pro **obnovení** na podnikových zařízeních iOS.
- Skrýt tlačítko **Odebrat** na podnikových zařízeních iOS.
Další informace najdete v tématu [Akce zařízení Samoobslužná služba z portál společnosti](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Automaticky aktualizovat dostupné aplikace VPP<!-- 3640511  -->
Aplikace, které se publikují jako dostupné aplikace programu Volume purchase program (VPP), se automaticky aktualizují, pokud je pro token VPP povolená **Automatická aktualizace aplikací** . Dříve dostupné aplikace VPP se neaktualizovaly automaticky. Místo toho museli koncoví uživatelé přejít na Portál společnosti a znovu nainstalovat aplikaci, pokud byla k dispozici novější verze. Požadované aplikace nadále podporují automatické aktualizace.




#### <a name="android-company-portal-user-experience---5736084----"></a>Uživatelské prostředí pro Android Portál společnosti<!-- 5736084  -->
Ve vydání 2005 Portál společnosti Androidu se koncovým uživatelům zařízení s Androidem, kteří mají v zásadách ochrany aplikací vystavili upozornění, zablokování nebo vymazání, se zobrazí nové uživatelské prostředí. Místo aktuálního prostředí dialogu se koncovým uživatelům zobrazí celá stránka popisující důvod upozornění, blokování nebo vymazání a postup, jak problém vyřešit. Další informace najdete v tématu [prostředí ochrany aplikací pro zařízení s Androidem](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) a [nastavení zásad ochrany aplikací pro Android v Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Podpora pro více účtů v Portál společnosti pro macOS<!-- 5779449  -->
Portál společnosti v zařízeních macOS nyní ukládá do mezipaměti uživatelské účty a usnadňuje tak přihlašování. Uživatelé už se nemusí přihlašovat k Portál společnosti při každém spuštění aplikace. Kromě toho Portál společnosti zobrazí výběr účtu, pokud jsou do mezipaměti více uživatelských účtů, aby uživatelé nemuseli zadávat své uživatelské jméno. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Nově dostupné chráněné aplikace<!-- 7060934   -->
K dispozici jsou teď tyto chráněné aplikace:
- Papírová deska
- Breezy pro Intune
- Hearsay vztah k Intune
- ISEC7 Mobile Exchange Delegate pro Intune
- Lexmark pro Intune
- Meetio Enterprise
- Microsoft tabule
- Nyní® Mobile – Intune
- Qlik – rozpoznávání mobilních zařízení 
- Agent ServiceNow® – Intune
- Připojování® ServiceNow – Intune
- Smartcrypt pro Intune
- TACT pro Intune
- Nula – e-mail pro zástupce

Další informace o chráněných aplikacích najdete v tématu [Microsoft Intune Protected Apps](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Hledání v dokumentaci k Intune z Portál společnosti<!-- 1736480   -->
V dokumentaci k Intune teď můžete vyhledávat přímo z Portál společnosti aplikace pro macOS. V řádku nabídek vyberte vyhledávání v **nápovědě**  >  **Search** a zadejte klíčová slova hledání, abyste mohli rychle najít odpovědi na své otázky.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Vylepšení podpory OEMConfig pro zařízení Zebra Technologies<!-- 4184154 -->
Intune plně podporuje všechny funkce, které poskytuje Zebra OEMConfig. Zákazníci, kteří spravují zařízení Zebra Technologies pomocí Androidu Enterprise a OEMConfig, můžou na jedno zařízení nasadit několik profilů OEMConfig. Zákazníci si také můžou zobrazit bohatou zprávu o stavu svých profilů Zebra OEMConfig.

Další informace najdete v tématu [nasazení více profilů OEMConfig do zařízení Zebra v Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

U jiných výrobců OEM se nemění chování OEMConfig.

Platí pro:
- Android Enterprise
- Zařízení Zebra Technologies, která podporují OEMConfig. Konkrétní podrobnosti o podpoře získáte od zebra.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Konfigurace systémových rozšíření na zařízeních macOS<!-- 6255624 -->
Na zařízeních MacOS můžete vytvořit profil rozšíření jádra pro konfiguraci nastavení na úrovni jádra (**Devices**  >  **konfigurační profily**zařízení  >  **MacOS** pro **rozšíření jádra** > platformy pro profil). Apple je nakonec zastaralá rozšíření jádra a nahrazuje je systémovými rozšířeními v budoucí verzi.

Rozšíření systému běží v uživatelském prostoru a nemají přístup k jádru. Cílem je zvýšit zabezpečení a poskytnout více koncovým uživatelským ovládacím prvkům a omezit tak útoky na úrovni jádra. Rozšíření jádra i systémová rozšíření umožňují uživatelům instalovat rozšíření aplikací, která rozšiřuje nativní možnosti operačního systému.

V Intune můžete nakonfigurovat rozšíření jádra i systémová rozšíření (**Devices**  >  **konfigurační profily**zařízení  >  **MacOS** pro rozšíření Platform > **System** pro profil). Rozšíření jádra se vztahují na 10.13.2 a novější. Systémová rozšíření se vztahují na 10,15 a novější. V macOS 10,15 až macOS 10.15.4 mohou běžet rozšíření jádra a systémová rozšíření vedle sebe. 

Další informace o těchto rozšířeních na zařízeních macOS najdete v tématu [Přidání rozšíření MacOS](../configuration/kernel-extensions-overview-macos.md).

Platí pro:
- macOS 10,15 a novější

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Konfigurace předvoleb ochrany osobních údajů aplikací a procesů na zařízeních macOS<!-- 2934232   --> 
S vydáním verze macOS Catalina 10,15 Společnost Apple přidala nové vylepšení zabezpečení a ochrany osobních údajů. Ve výchozím nastavení nemůžou aplikace a procesy získat přístup k určitým datům bez souhlasu uživatele. Pokud uživatelé neposkytnou souhlas, nemusí aplikace a procesy fungovat. Intune přidává podporu pro nastavení, která správcům IT umožní povolit nebo zakázat souhlas s přístupem k datům jménem koncových uživatelů na zařízeních s macOS 10,14 a novějším. Tato nastavení zajistí, že aplikace a procesy budou dál fungovat správně, a sníží počet výzev. 

Další informace o nastaveních, která můžete spravovat, najdete v tématu [předvolby ochrany osobních údajů pro MacOS](../configuration/device-restrictions-macos.md#privacy-preferences).

Platí pro:
- macOS 10,14 a novější

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Omezení registrace podporují značky oboru<!--4209550  -->
Nyní můžete přiřadit značky oboru k omezením registrace. Provedete to tak, že přejdete do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Devices**  >  **omezení registrace**  >  **vytvořit omezení**. Vytvořte buď typ omezení, a zobrazí se stránka **značky oboru** . Další informace najdete v tématu [Nastavení omezení registrace](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Podpora autopilotu pro zařízení HoloLens 2<!--6305220  -->
Windows autopilot teď podporuje zařízení HoloLens 2. Další informace o použití autopilotu pro HoloLens najdete v tématu [Windows autopilot for HoloLens 2](/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Použít pro iOS hromadnou synchronizaci vzdálených akcí<!--6440956  idmiss-->
Můžete teď použít synchronizaci vzdálených akcí až po 100 zařízení s iOS. Tuto funkci zobrazíte tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**  >  **všechna zařízení**  >  **Akce hromadných zařízení**. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Automatický interval synchronizace zařízení je mimo 12 hodin.<!--3077535  -->
V případě automatizované registrace zařízení od společnosti Apple se interval automatizované synchronizace zařízení mezi Intune a Apple Business Managerem snížil z 24 hodin na 12 hodin. Další informace o synchronizaci najdete v tématu [synchronizace spravovaných zařízení](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Podpora odvozených přihlašovacích údajů pro DISA purebred na zařízeních s Androidem<!-- 6939073     -->
*DISA purebred* teď můžete použít jako [odvozeného poskytovatele přihlašovacích údajů](../protect/derived-credentials.md) na zařízeních s plnou správou Androidu Enterprise. Podpora zahrnuje načítání odvozených přihlašovacích údajů pro DISA purebred. U aplikací, které ji podporují, můžete použít odvozenou přihlašovací údaje pro ověřování aplikací, podepisování Wi-Fi, VPN nebo šifrování S/MIME. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Odeslání nabízených oznámení jako akce při nedodržení předpisů <!-- 1733150   -->
Teď můžete nakonfigurovat [akci pro nedodržování předpisů](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) , která pošle nabízené oznámení uživateli, když jejich zařízení nesplňuje podmínky zásad dodržování předpisů. Nová akce **pošle nabízené oznámení koncovému uživateli**a podporuje se na zařízeních s Androidem a iOS.

Když uživatel vybere nabízené oznámení na svém zařízení, otevře se Portál společnosti nebo aplikace Intune, kde se zobrazí podrobnosti o tom, proč nedodržují předpisy.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Obsah a nové funkce zabezpečení koncového bodu<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

V dokumentaci k Intune [Endpoint Security](../protect/endpoint-security.md) je teď k dispozici. V uzlu zabezpečení koncového bodu centra pro správu Microsoft Endpoint Manageru můžete:

- Vytvoření a nasazení zásad zabezpečení s fokusem na spravovaná zařízení
- Nakonfigurujte integraci pomocí rozšířené ochrany před internetovými útoky v programu Microsoft Defender a spravujte bezpečnostní úkoly, které vám pomůžou napravit rizika pro rizikové zařízení, která jsou určená vaším týmem ATP.
- Konfigurace standardních hodnot zabezpečení
- Správa zásad dodržování předpisů a podmíněného přístupu zařízení
- Pokud je Configuration Manager nakonfigurovaná pro připojení klienta, můžete zobrazit stav dodržování předpisů pro všechna zařízení z Intune i Configuration Manager.

Kromě dostupnosti obsahu jsou pro řešení Endpoint Security v tomto měsíci novinkou následující:

- [**Zásady zabezpečení koncového bodu**](../protect/endpoint-security-policy.md) **nejsou ve verzi** ***Preview*** a teď jsou připravené k použití v produkčním prostředí ( *všeobecně dostupné*) se dvěma výjimkami:

  - V nové *veřejné verzi Preview*můžete použít [profil **pravidla firewallu v programu Microsoft Defender** ](../protect/endpoint-security-firewall-policy.md#firewall-profiles) pro zásady brány firewall systému Windows 10. U každé instance tohoto profilu můžete nakonfigurovat až 150 pravidel brány firewall, která budou chtít vaše profily firewallu v programu Microsoft Defenderu zdarma. 
  - Zásady zabezpečení ochrany účtů zůstávají ve verzi Preview. 

- Teď můžete [**vytvořit duplikáty zásad zabezpečení koncového bodu**](../protect/endpoint-security-policy.md#duplicate-a-policy). Duplicity udržují konfiguraci nastavení původní zásady, ale získají nový název. Nová instance zásad pak neobsahuje žádná přiřazení do skupin, dokud neupravíte novou instanci zásady tak, aby se přidala. Duplikovat můžete následující zásady:
  - Antivirus
  - Šifrování disků
  - Firewall
  - Zjišťování koncových bodů a odpověď
  - Omezení možností útoku
  - Ochrana účtu

- Nyní můžete [**vytvořit duplikát standardních hodnot zabezpečení**](../protect/security-baselines.md#duplicate-a-security-baseline). Duplicity udržují konfiguraci nastavení původního směrného plánu, ale získají nový název. Nová instance směrného plánu neobsahuje žádná přiřazení do skupin, dokud neupravíte novou instanci směrného plánu tak, aby se přidala.

- K dispozici je nová sestava pro zásady antivirové ochrany Endpoint Security: [**koncové body Windows 10**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints)nejsou v pořádku. Tato sestava je novou stránkou, kterou si můžete vybrat, když vaše aplikace zobrazuje vaše zásady ochrany koncových bodů. V sestavě se zobrazí stav antivirové ochrany zařízení s Windows 10 spravovaných přes MDM.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Podpora podpisových a šifrovacích certifikátů S/MIME pomocí Outlooku v Androidu<!-- 7207474  -->
V Outlooku v Androidu teď můžete použít certifikáty pro podepisování S/MIME a šifrování. Pomocí této podpory můžete tyto certifikáty zřídit pomocí profilů certifikátů SCEP, PKCS a PKCS. Podporovány jsou následující platformy Android:

- Pracovní profil Android Enterprise
- Správce zařízení s Androidem

Brzy se připraví podpora pro zařízení s plnou správou pro Android Enterprise.

Další informace o této podpoře najdete v tématu [citlivostní označování a ochrana v Outlooku pro iOS a Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) v dokumentaci k Exchangi.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="device-reports-ui-update---6269408---"></a>Aktualizace uživatelského rozhraní sestav zařízení<!-- 6269408 -->
Podokno přehled sestav nyní obsahuje **Souhrn** a kartu **sestavy** . V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **sestavy**a potom vyberte kartu **sestavy** , abyste viděli dostupné typy sestav. Související informace najdete v tématu [sestavy Intune](reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Skriptování

#### <a name="macos-script-support---6376978----"></a>Podpora skriptů macOS<!-- 6376978  -->
Podpora skriptů pro macOS je teď všeobecně dostupná. Kromě toho jsme doplnili podporu pro skripty přiřazené uživateli i pro zařízení macOS, která byla zaregistrovaná pomocí automatizované registrace zařízení společnosti Apple (dříve Program registrace zařízení). Další informace najdete v tématu [použití skriptů prostředí v zařízeních MacOS v Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Týden od 4. května 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Portál společnosti pro Android provede uživatele k získání aplikací po registraci pracovního profilu. <!-- 6103999 -->
Vylepšili jsme doprovodné materiály k aplikaci v Portál společnosti, aby uživatelé mohli snáze najít a nainstalovat aplikace. Po registraci v nástroji Správa pracovních profilů se uživatelům zobrazí zpráva s vysvětlením, jak najít navrhované aplikace v označení verze Google Play. Poslední krok v části [registrace zařízení s Androidem](../user-help/enroll-device-android-work-profile.md) se aktualizoval, aby se zobrazila nová zpráva. Uživatelům se na levé straně Portál společnosti zobrazí také nový odkaz **získat aplikace** . Aby bylo možné tyto nové a vylepšené prostředí vytvořit, karta **aplikace** byla odebrána. Aktualizované obrazovky zobrazíte tak, že přejdete na [aktualizace uživatelského rozhraní pro aplikace Intune pro koncové uživatele](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Týden od 20. dubna 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager spojuje Configuration Manager a Intune s jednou konzolou. Configuration Manager počínaje verzí 2002 můžete do cloudové služby nahrát vaše Configuration Manager zařízení a v centru pro správu provádět akce, které jim provedete. Další informace najdete v tématu [připojení tenanta Microsoft Endpoint Manager: synchronizace zařízení a akce zařízení](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>systém Microsoft Office 365 přeplus přejmenovat<!-- 6368143 -->
Systém Microsoft Office 365 ProPlus se přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](/deployoffice/name-change). V naší dokumentaci na ni běžně odkazujeme jako na Microsoft 365 aplikace. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete sadu aplikací najít tak, že vyberete **aplikace**  >  **Windows**  >  **Přidat**. Informace o přidávání aplikací najdete v tématu [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Týden od 13. dubna 2020 (2004 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Správa nastavení S/MIME pro Outlook na zařízeních S Androidem Enterprise<!-- 6517085   -->
Zásady konfigurace aplikací můžete použít ke správě nastavení S/MIME pro Outlook na zařízeních, na kterých běží Android Enterprise. Můžete také zvolit, jestli chcete povolit uživatelům zařízení povolit nebo zakázat nastavení S/MIME v Outlooku. Pokud chcete používat zásady konfigurace aplikací pro Android, v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) přejít na **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**  >  **spravovaná zařízení**. Další informace o konfiguraci nastavení pro Outlook najdete v tématu [nastavení konfigurace Microsoft Outlooku](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Předběžné vydání testování pro spravované aplikace Google Play<!-- 2681933  -->
Organizace, které používají [ukončené zkušební běhy Google Play pro testování předběžných verzí aplikací](https://support.google.com/googleplay/android-developer/answer/3131213) , můžou tyto stopy spravovat pomocí Intune. Můžete selektivně přiřadit aplikace, které jsou publikovány do předprodukčních běhů Google Play do pilotních skupin, aby bylo možné provádět testování. V Intune se můžete podívat, jestli aplikace obsahuje předprodukční zkušební záznam buildu, který se do něj publikuje, a může jim přiřadit tuto stopu ke skupinám uživatelů nebo zařízení Azure AD. Tato funkce je k dispozici pro všechny aktuálně podporované podnikové scénáře Androidu (pracovní profil, plně spravované a vyhrazené). V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete přidat spravovanou aplikaci Google Play tak, že vyberete **aplikace**  >  **Android**  >  **Add**. Další informace najdete v tématu [práce se spravovanými Google Play uzavřených testovacích běhů](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### <a name="microsoft-teams-is-now-included-in-microsoft-365-for-macos---5903936----"></a>Microsoft Teams je teď součástí Microsoft 365 pro macOS<!-- 5903936  -->
Uživatelé, kteří jsou přiřazeni Microsoft 365 pro macOS ve službě Microsoft Endpoint Manager, teď budou kromě stávajících aplikací Microsoft 365 (Word, Excel, PowerPoint, Outlook a OneNote) dostávat i týmy Microsoftu. Intune rozpozná existující zařízení Mac, na kterých je nainstalovaný jiný Office pro aplikace macOS, a pokusí se nainstalovat Microsoft Teams při příštím ověření zařízení v Intune. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete najít **sadu Office 365 Suite** pro MacOS tak, že vyberete **aplikace**  >  **MacOS**  >  **Přidat**. Další informace najdete v tématu [přiřazení Office 365 k MacOS zařízením pomocí Microsoft Intune](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Aktualizace zásad konfigurace aplikací pro Android<!-- 6113334  -->
Zásady konfigurace aplikací pro Android se aktualizovaly, aby správci před vytvořením konfiguračního profilu aplikace mohli vybrat typ registrace zařízení. Tato funkce je přidávána do účtu pro profily certifikátů, které jsou založeny na typu registrace (pracovní profil nebo vlastník zařízení).  Tato aktualizace poskytuje následující:

1. Pokud je vytvořený nový profil a pro typ registrace zařízení je vybraný profil pracovního profilu a vlastníka zařízení, nebudete moct k zásadě konfigurace aplikace přidružit profil certifikátu.
2. Pokud je vytvořen nový profil a je vybrán pouze pracovní profil, mohou být využívány Zásady certifikátů pracovního profilu vytvořené v části Konfigurace zařízení.
3. Pokud je vytvořen nový profil a je vybrán pouze vlastník zařízení, může být využita zásada certifikátu vlastníka zařízení vytvořená v části Konfigurace zařízení. 

> [!IMPORTANT]
> Stávající zásady vytvořené před vydáním této funkce (duben 2020 Release-2004), které nemají žádné profily certifikátů přidružené k zásadám, budou ve výchozím nastavení funkční profil a profil vlastníka zařízení pro typ registrace zařízení. Existující zásady vytvořené před vydáním této funkce, které mají profily certifikátů, které jsou k nim přidružené, budou také nastavené jako výchozí pouze pracovní profil.

Kromě toho přidáváme e-mailové profily gmail a devět e-mailů, které budou fungovat pro typy registrace pracovní profil i vlastník zařízení, včetně použití profilů certifikátů v obou typech konfigurace e-mailu.  Všechny zásady Gmail nebo devět, které jste vytvořili v části Konfigurace zařízení pro pracovní profily, se budou i nadále používat pro zařízení a není nutné je přesouvat do zásad konfigurace aplikací.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)můžete zásady konfigurace aplikací najít **výběrem možnosti**  >  **zásady konfigurace**aplikací. Další informace o zásadách konfigurace aplikací najdete v tématu [zásady konfigurace aplikací pro Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Nabízené oznámení, když se změní typ vlastnictví zařízení<!-- 5575875 -->
Můžete nakonfigurovat nabízená oznámení, která se budou posílat uživatelům s Androidem i iOS Portál společnosti, když se jejich typ vlastnictví zařízení změní z osobních na firemní, protože se mu připadá ochrana osobních údajů. Toto nabízené oznámení je ve výchozím nastavení vypnuté. Nastavení najdete v části Microsoft Endpoint Manager – vyberte **Tenant administration**  >  **vlastní nastavení**správy tenanta. Další informace o tom, jak vlastnictví zařízení ovlivňuje koncové uživatele, najdete v tématu [Změna vlastnictví zařízení](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Podpora pro podokno přizpůsobení pro skupinu<!-- 4722837  -->
Nastavení můžete cílit v podokně **přizpůsobení** na skupiny uživatelů. Tato nastavení v Intune najdete tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberete přizpůsobení **správy tenanta**  >  **Customization**. Další informace o přizpůsobení najdete v tématu [přizpůsobení aplikace Portál společnosti Intune, portál společnosti webu a aplikace Intune](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Vícenásobné vyhodnocování každého pokusu o připojení – pravidla VPN na vyžádání podporovaná v iOS, iPadOS a macOS<!-- 6424615  -->
Uživatelské prostředí Intune umožňuje více pravidel sítě VPN na vyžádání ve stejném profilu sítě VPN s **vyhodnocením každé akce pokusu o připojení** (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** nebo **MacOS** pro Platform > **VPN** pro profil > **Automatické připojení VPN**  >  **na vyžádání**).

V seznamu se respektuje jenom první pravidlo. Toto chování je opravené a Intune vyhodnocuje všechna pravidla v seznamu. Každé pravidlo je vyhodnoceno v pořadí, v jakém se zobrazuje v seznamu pravidla na vyžádání.

> [!NOTE]
> Pokud máte existující profily sítě VPN, které používají tato pravidla sítě VPN na vyžádání, oprava se projeví při příštím změně profilu sítě VPN. Například proveďte menší změnu, například změňte název připojení a pak profil uložte.
>
> Pokud používáte certifikáty SCEP k ověřování, tato změna způsobí, že se certifikáty pro tento profil sítě VPN znovu vystaví.

Platí pro:
- iOS/iPadOS
- macOS

Další informace o profilech sítě VPN najdete v tématu [Vytvoření profilů sítě VPN](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Další možnosti v profilech jednotného přihlašování a rozšíření aplikace jednotného přihlašování na zařízeních s iOS/iPadOS<!-- 6504155   -->

Na zařízeních s iOS/iPadOS můžete:
- V části profily jednotného**Devices**přihlašování (  >  **konfigurační profily zařízení**  >  **vytvořit profil**  >  **iOS/iPadOS** pro platformu > **funkce zařízení** pro profil > **jednotné přihlašování**) nastavte hlavní název protokolu Kerberos jako název účtu správce zabezpečení účtů (SAM) v profilech jednotného přihlašování. 
- V profilech rozšíření aplikace jednotného přihlašování (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro platformu > **funkce zařízení** pro profil > **rozšíření aplikace s jednotným přihlašováním**) nakonfigurujte rozšíření iOS/iPadOS Microsoft Azure AD s menším počtem kliknutí pomocí nového typu rozšíření aplikace jednotného přihlašování. Můžete povolit rozšíření Azure AD pro zařízení v režimu sdíleného zařízení a odeslat data specifická pro rozšíření do tohoto rozšíření.

Platí pro:
- iOS/iPadOS 13.0 +

Další informace o použití jednotného přihlašování na zařízeních s iOS/iPadOS najdete v tématu [Přehled rozšíření aplikace jednotného přihlašování](../configuration/device-features-configure.md#single-sign-on-app-extension) a [seznam nastavení jednotného přihlašování](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Odstranit token registrace Apple automatizovaného zařízení, pokud je k dispozici výchozí profil<!--6393220 -->
Dřív jste nedokázali odstranit výchozí profil, což znamená, že se k němu nepodařilo odstranit token automatického zápisu zařízení, který je k němu přidružený. Nyní můžete token odstranit v těchto případech:
- k tokenu nejsou přiřazená žádná zařízení.
- v takovém případě je k dispozici výchozí profil, odstraňte výchozí profil a pak odstraňte přidružený token.
Další informace najdete v tématu [odstranění tokenu ADE z Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Podpora škálované podpory pro Apple Automated Device Enrollment a zařízení, profily a tokeny Apple Configuratoru 2<!--3542402 -->
Intune teď pro distribuované IT oddělení a organizace podporuje až 1000 profilů zápisu na tokeny, 2000 automatické registrace zařízení (dříve označované jako DEP) tokeny na jeden účet Intune a 75 000 zařízení na token. Neexistují žádné zvláštní limity pro zařízení na registrační profil, a to pod maximálním počtem zařízení na token.

Intune teď podporuje až 1000 profilů Apple Configuratoru 2.

Další informace najdete v tématu [podporovaný svazek](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Všechna zařízení – změny položky sloupce<!--6967616 -->
Na stránce **všechna zařízení** se změnily položky pro sloupec **spravováno** v:
- Místo *MDM* se teď zobrazuje *Intune* .
- *Společně spravovaná* se teď místo *agenta MDM/ConfigMgr* zobrazuje spoluspravované.

Exportní hodnoty se nezměnily.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Informace o verzi programu Trusted Platform Manager (TPM) nyní na stránce hardware zařízení<!--6224914 idmiss -->
Číslo verze TPM teď můžete zobrazit na stránce hardware zařízení ([Centrum pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Devices** > vyberte zařízení > **hardware** > v části **systémového skříně**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Shromažďování protokolů pro lepší řešení potíží se skripty přiřazenými zařízením macOS<!-- 6359853  -->
Teď můžete shromažďovat protokoly pro lepší řešení potíží se skripty přiřazenými k zařízením macOS. Protokoly můžete shromažďovat až do 60 MB (komprimovaných) nebo 25 souborů, podle toho, co nastane dřív. Další informace najdete v tématu [řešení potíží se zásadami skriptů prostředí MacOS pomocí shromažďování protokolů](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Zabezpečení

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Odvozené přihlašovací údaje pro zřízení plně spravovaných zařízení s Androidem Enterprise s certifikáty<!--4839592    -->
Intune teď podporuje použití [odvozených přihlašovacích údajů](../protect/derived-credentials.md) jako metody ověřování pro zařízení s Androidem. Odvozené přihlašovací údaje jsou implementací standardu NIST (National Institute of Standards and Technology) 800-157 pro nasazení certifikátů do zařízení. Naše podpora pro Android se rozbalí v naší podpoře pro zařízení se systémem iOS/iPadOS.

Odvozené přihlašovací údaje spoléhají na použití osobního ověřování identity (PIV) nebo karty Common Access Card (CAC), jako je například čipová karta. Pokud chcete získat odvozené přihlašovací údaje pro své mobilní zařízení, uživatelé začnou v aplikaci Microsoft Intune a dodržujte pracovní postup registrace, který je jedinečný pro poskytovatele, kterého používáte. Společný pro všechny poskytovatele je požadavek na použití čipové karty v počítači k ověření pro odvozeného zprostředkovatele přihlašovacích údajů. Poskytovatel pak vydá certifikát zařízení, které je odvozeno od čipové karty uživatele.

Odvozené přihlašovací údaje můžete použít jako metodu ověřování pro profily konfigurace zařízení pro VPN a Wi-Fi. Můžete je také použít k ověřování aplikací a podepisování a šifrování S/MIME pro aplikace, které je podporují.

Intune teď podporuje následující odvozené zprostředkovatele přihlašovacích údajů s Androidem:
- Entrust Datacard
- Intercede

Třetí poskytovatel, DISA purebred, bude pro Android dostupný v budoucí verzi.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Základní plán zabezpečení Microsoft Edge je teď všeobecně dostupný.<!--6586139 -->

Je dostupná nová verze [standardních hodnot zabezpečení Microsoft Edge](../protect/security-baselines.md#available-security-baselines) , která je vydaná jako obecně dostupná (GA). Předchozí směrové hodnoty hran byly ve verzi Preview.  Nová základní verze v dubnu 2020 (hraná verze 80 a novější). 

S vydáním tohoto nového směrného plánu už nebudete moct vytvářet profily založené na předchozích verzích základní verze, ale můžete dál používat profily, které jste vytvořili v těchto verzích. Můžete se také rozhodnout [aktualizovat stávající profily, aby používaly nejnovější základní verzi](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Týden od 6. dubna 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Nové nastavení skriptu prostředí pro zařízení macOS<!-- 6884363 -->
Při konfiguraci skriptů prostředí pro zařízení macOS můžete teď nakonfigurovat tato nová nastavení: 
- Skrytí oznámení skriptu na zařízeních
- Frekvence skriptu
- Maximální počet pokusů o opakování při chybě skriptu

Další informace najdete v tématu [použití skriptů prostředí v zařízeních MacOS v Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Týden od 30. března 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Nová adresa URL centra pro správu služby Microsoft Endpoint Manager<!-- 3704810 -->
Pro zarovnávání s oznámením Microsoft Endpoint Manageru v Ignite minulý rok jsme změnili adresu URL centra pro správu Microsoft Endpoint Manageru (dříve Microsoft 365 správu zařízení) na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) . Stará adresa URL centra pro správu ( [https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com) ) bude i nadále fungovat, ale doporučujeme vám začít přistoupit k centru pro správu Microsoft Endpoint Manageru pomocí nové adresy URL.

Další informace najdete v tématu [zjednodušení IT úloh pomocí centra pro správu služby Microsoft Endpoint Manager](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Správa aplikací  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Portál společnosti pro iOS podporuje režim na šířku<!--6048329  -->   
Uživatelé teď můžou zaregistrovat svoje zařízení, Hledat aplikace a získat podporu na základě orientace obrazovky podle jejich výběru. Aplikace bude automaticky rozpoznávat a upravovat obrazovky, aby odpovídaly režimu na výšku nebo na šířku, pokud uživatelé nezamkne obrazovku v režimu na výšku.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Podpora skriptů pro zařízení macOS (Public Preview)<!-- 4280361  -->
Můžete přidávat a nasazovat skripty pro zařízení macOS. Tato podpora rozšiřuje vaši schopnost nakonfigurovat zařízení macOS nad rámec toho, co je možné na zařízeních macOS využít nativní možnosti MDM. Další informace najdete v tématu [použití skriptů prostředí v zařízeních MacOS v Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Týden od 24. března 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Vylepšené uživatelské rozhraní při vytváření profilů omezení zařízení pro zařízení s Androidem a Androidem Enterprise<!-- 5841361 -->
Když vytvoříte profil pro zařízení s Androidem nebo Androidem Enterprise, bude se aktualizovat prostředí v centru pro správu správy koncových bodů. Tato změna má vliv na následující konfigurační profily zařízení **(**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Správce zařízení s Androidem** nebo **Android Enterprise** for Platform):

- Omezení zařízení: Správce zařízení s Androidem
- Omezení zařízení: vlastník zařízení se systémem Android Enterprise
- Omezení zařízení: pracovní profil Android Enterprise

Další informace o omezeních zařízení, která můžete konfigurovat, najdete v tématu [Správce zařízení s Androidem](../configuration/device-restrictions-android.md) a [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Vylepšené prostředí uživatelského rozhraní při vytváření konfiguračních profilů na zařízeních s iOS/iPadOS a macOS<!-- 5569002 5568997 -->
Když vytváříte profil pro zařízení se systémem iOS nebo macOS, prostředí v centru pro správu správy koncových bodů se aktualizuje. Tato změna má vliv na následující konfigurační profily zařízení (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** nebo **MacOS** pro platformu):

- Vlastní: iOS/iPadOS, macOS
- Funkce zařízení: iOS/iPadOS, macOS
- Omezení zařízení: iOS/iPadOS, macOS
- Ochrana koncového bodu: macOS
- Rozšíření: macOS
- Soubor předvoleb: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Skrytí nastavení konfigurace uživatele ve funkcích zařízení na zařízeních macOS<!-- 6524869 -->

Když vytvoříte konfigurační profil funkcí zařízení na zařízeních MacOS, je k dispozici nová možnost **Skrýt z nastavení konfigurace uživatele** (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **MacOS** pro **funkce** Platform > pro > pro **přihlašovací položky**profilu).

Tato funkce nastaví zaškrtnutí skryté aplikace v seznamu **uživatelé & skupiny** přihlášení k aplikacím na zařízeních MacOS. Existující profily ukazují toto nastavení v seznamu jako nenakonfigurované. Pro konfiguraci tohoto nastavení můžou správci aktualizovat existující profily.

Když je tato možnost nastavená na hodnotu **Skrýt**, pro aplikaci se kontroluje zaškrtávací políčko Skrýt a uživatelé je nemůžou změnit. Po přihlášení uživatelů ke svým zařízením taky aplikaci uživatelům skryje.

> [!div class="mx-imgBorder"]
> ![Skrýt aplikace na zařízeních macOS po přihlášení uživatelů k zařízení v Microsoft Intune a v nástroji Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Další informace o nastavení, které můžete nakonfigurovat, najdete v tématu [Nastavení funkcí zařízení MacOS](../configuration/macos-device-features-settings.md).

Tato funkce platí pro:

- macOS

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>Týden od 16. března 2020 (2003 vydání služby)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS a iOS – aktualizace Portál společnosti<!-- 5779439, 5780234  -->
Podokno profil pro macOS a iOS Portál společnosti bylo aktualizované tak, aby obsahovalo tlačítko pro odhlášení. Kromě toho se v podokně profil v macOS Portál společnosti provedla vylepšení uživatelského rozhraní. Další informace o Portál společnosti naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Změna cílení webových klipů na zařízení s iOS na Microsoft Edge<!-- 5455276   -->
Nově nasazené webové klipy (připnuté webové aplikace) na zařízeních s iOS, které jsou nutné k otevření v chráněném prohlížeči, se otevřou na webu Microsoft Edge, nikoli na Intune Managed Browser. Aby bylo zajištěno, že budou otevřeny na webu Microsoft Edge a nikoli na Managed Browser, je třeba změnit cílení na stávající webové klipy. Další informace najdete v tématu [Správa webového přístupu pomocí Microsoft Edge s Microsoft Intune](../apps/manage-microsoft-edge.md) a [Přidání webových aplikací do Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Použití diagnostického nástroje Intune s Microsoft Edgem pro Android<!-- 4735244  -->
Microsoft Edge pro Android je teď integrovaný s diagnostickým nástrojem Intune. Podobně jako při práci na Microsoft Edge pro iOS se zadáním "About: intunehelp" do adresního řádku (pole adresa) Microsoft Edge na zařízení spustí diagnostický nástroj Intune. Tento nástroj bude poskytovat podrobné protokoly. Uživatelé můžou provádět shromažďování a posílání těchto protokolů na IT oddělení nebo zobrazovat protokoly MAM pro konkrétní aplikace.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Aktualizace brandingu a přizpůsobení Intune<!-- 5236032  -->
Aktualizovali jsme podokno Intune s názvem branding a přizpůsobení, včetně těchto vylepšení:

- Přejmenujte podokno na **přizpůsobení**.
- Vylepšení organizace a návrhu nastavení.
- Vylepšení textu a popisů nastavení

Tato nastavení v Intune najdete tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberete přizpůsobení **správy tenanta**  >  **Customization**. Informace o existujícím přizpůsobení najdete v části [How to configure Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Osobní šifrovaný obnovovací klíč uživatele<!-- 6273943  -->
K dispozici je nová funkce Intune, která umožňuje uživatelům načíst svůj osobní zašifrovaný klíč obnovení **trezoru hesel** pro zařízení Mac přes aplikaci pro Android portál společnosti nebo prostřednictvím aplikace Intune pro Android. V aplikaci Portál společnosti i v aplikaci Intune je odkaz, ve kterém se otevře prohlížeč Chrome na webu Portál společnosti kde se uživatel může podívat na obnovovací klíč **trezoru** souborů, který je potřebný pro přístup k zařízením Mac. Další informace o šifrování najdete v tématu [použití šifrování zařízení s Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Optimalizované registrace vyhrazeného zařízení <!-- 6114580  -->
Optimalizujeme registraci pro vyhrazená zařízení s Androidem Enterprise a usnadňuje certifikátům SCEP přidruženým k Wi-Fi, aby se mohla vztahovat na vyhrazená zařízení zaregistrovaná před 22. listopadu 2019. Pro nové registrace se bude aplikace Intune dál instalovat, ale koncoví uživatelé už během registrace nebudou muset provádět krok **Povolit agenta Intune** . K instalaci dojde na pozadí automaticky a certifikáty SCEP přidružené k Wi-Fi se dají nasadit a nastavit bez zásahu koncového uživatele.  

Tyto změny se budou zavádět postupně po celém měsíci od března po nasazení služby Intune back-end. Všichni klienti budou mít toto nové chování na konci března. Související informace najdete v tématu [Podpora certifikátů SCEP na vyhrazených zařízeních s Androidem Enterprise](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Nové uživatelské prostředí při vytváření šablon pro správu na zařízeních s Windows<!--5096036 -->
Na základě zpětné vazby od zákazníků a našeho přechodu na nové prostředí Azure na celé obrazovce jsme znovu vytvořili prostředí pro Šablony pro správu profilování pomocí zobrazení složek. Neudělali jsme žádné změny nastavení ani stávajících profilů. Stávající profily tak zůstanou stejné a budou použitelné v novém zobrazení. Můžete i nadále procházet všechny možnosti nastavení tím, že vyberete **všechna nastavení**a použijete hledání. Stromové zobrazení je rozdělené podle konfigurace počítačů a uživatelů. Nastavení pro Windows, Office a Edge najdete v přidružených složkách.  

Platí pro:
- Windows 10 a novější

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>Profily sítě VPN s připojením IKEv2 VPN můžou používat Always On se zařízeními se systémem iOS/iPadOS.<!-- 1947932   -->
Na zařízeních s iOS/iPadOS můžete vytvořit profil VPN, který používá připojení IKEv2 (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro Platform > **VPN** pro typ profilu). Teď můžete nakonfigurovat Always-On s IKEv2. Po nakonfigurování se profily IKEv2 VPN připojují automaticky a udržují se připojení (nebo rychlé opětovné připojení) k síti VPN. Zůstane připojený i při přesunu mezi sítěmi nebo po restartování zařízení.

V systému iOS/iPadOS je vždycky zapnutá síť VPN omezená na profily IKEv2.

Pokud chcete zobrazit nastavení IKEv2, která můžete nakonfigurovat, přejděte na téma [Přidání nastavení sítě VPN na zařízení s iOS v Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Platí pro:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Odstranění sad a polí sady prostředků v profilech konfigurace zařízení OEMConfig na zařízeních s Androidem Enterprise<!-- 5550355   -->
Na zařízeních s Androidem Enterprise vytvoříte a aktualizujete profily OEMConfig (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **Android Enterprise** for Platform > **OEMConfig** pro typ profilu). Uživatelé teď můžou pomocí **Návrháře konfigurace** v Intune odstraňovat sady a pole sad.

Další informace o profilech OEMConfig najdete v tématu [použití a Správa zařízení se systémem Android Enterprise pomocí nástroje OEMConfig v Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Platí pro:
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Konfigurace rozšíření iOS/iPadOS Microsoft Azure AD App Extension pro jednotné přihlašování<!-- 5672534   -->
Tým Microsoft Azure AD vytvořil rozšíření aplikace jednotného přihlašování (SSO) pro přesměrování, které umožňuje uživatelům iOS/iPadOS 13.0 + získat přístup k aplikacím a webům Microsoftu s jedním přihlašováním. Všechny aplikace, které dříve používaly zprostředkované ověřování pomocí aplikace Microsoft Authenticator, budou i nadále získávat jednotné přihlašování s novým rozšířením jednotného přihlašování. V případě verze rozšíření aplikace jednotného přihlašování k Azure AD můžete nakonfigurovat rozšíření jednotného přihlašování (SSO) s typem rozšíření aplikace jednotného přihlašování (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** for Platform > pro typ profilu > **rozšíření aplikace jednotného přihlašování**). **Device features**

Platí pro:
- iOS 13,0 a novější
- iPadOS 13,0 a novější

Další informace o rozšířeních aplikace jednotného přihlašování pro iOS najdete v tématu [rozšíření aplikace jednotného přihlašování](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Nastavení pro změnu nastavení vztahu důvěryhodnosti podnikových aplikací se odebere z profilů omezení zařízení s iOS/iPadOS.<!-- 6225131   -->
Na zařízeních se systémem iOS/iPadOS vytvoříte profil omezení zařízení (konfigurace**zařízení**  >  **profily**  >  **vytvořit profil**  >  **iOS/iPadOS** pro platformu > **omezení zařízení** pro typ profilu). Nastavení pro **změnu nastavení vztahu důvěryhodnosti podnikových aplikací** se odeberou od společnosti Apple a odebere se z Intune. Pokud toto nastavení aktuálně používáte v profilu, nemá žádný vliv a odebere se z existujících profilů. Toto nastavení se taky odebere z jakéhokoli vytváření sestav v Intune.

Platí pro:
- iOS/iPadOS

Pokud chcete zobrazit nastavení, která můžete omezit, přejděte na [nastavení zařízení s iOS a iPadOS a povolte nebo zakažte funkce](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Řešení potíží: nedokončená oznámení zásad MAM se změnila na informační ikonu<!--6348954 -->
Ikona oznámení pro nedokončené zásady MAM v okně Poradce při potížích se změnila na informační ikonu.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Aktualizace uživatelského rozhraní při konfiguraci zásad dodržování předpisů<!-- 3961639    -->

Aktualizovali jsme uživatelské rozhraní pro [vytváření zásad dodržování předpisů](../protect/create-compliance-policy.md#create-the-policy) v Microsoft Endpoint Manageru (zásady**Devices**  >  **zásad dodržování předpisů**zařízeními  >  **Policies**  >  **vytvořit zásadu**). Nové uživatelské prostředí obsahuje stejné nastavení a podrobnosti, které jste použili dříve. Nové prostředí se řídí procesem podobným průvodci při vytváření zásad dodržování předpisů a zahrnuje stránku, kde můžete přidat *přiřazení* pro zásadu a stránku *recenze + vytvořit* , kde můžete před vytvořením zásady zkontrolovat konfiguraci.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Vyřazení zařízení nesplňujících požadavky<!-- 1827291       -->
Přidali jsme novou akci pro zařízení nedodržující předpisy, která můžete přidat do libovolné zásady a  [vyřadit zařízení nesplňující požadavky](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  Nová akce, **vyřazení zařízení nedodržujících předpisy**, má za následek odebrání všech firemních dat ze zařízení a také odebere zařízení ze správy Intune.  Tato akce se spustí, když se dosáhne nakonfigurované hodnoty v dnech a v tomto okamžiku se zařízení bude mít nárok na vyřazení. Minimální hodnota je 30 dní.  K vyřazení zařízení pomocí části *vyřazení zařízení nedodržujících předpisy* se bude vyžadovat explicitní schválení správce IT, kde správci můžou vyřadit všechna oprávněná zařízení.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Podpora WPA a WPA2 v profilech pro iOS Enterprise Wi-Fi<!--6215273   -->
[Profily sítě Wi-Fi pro iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) teď podporují pole *typ zabezpečení* . V poli *typ zabezpečení*můžete vybrat možnost **WPA Enterprise** nebo **WPA/WPA2 Enterprise**a pak zadat výběr pro *typ protokolu EAP*.  (**Zařízení**  >  **Konfigurační profily**  >  **Vytvořte profil** a vyberte pro *platformu* **iOS/iPadOS** a pak na *profil*sítě **Wi-Fi** . 

Nové možnosti organizace jsou ty, které jsou k dispozici pro základní profil Wi-Fi pro iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Nové uživatelské prostředí pro profily certifikátů, e-mailů, VPN a Wi-Fi a VPN<!-- 5615208   -->
Aktualizovali jsme [prostředí pro uživatele](../configuration/device-profile-create.md) v centru pro správu správy koncových**Devices**bodů (  >  **konfigurační profily**zařízení  >  **vytvořit profil**) pro vytváření a úpravu následujících typů profilů. Nové prostředí prezentuje stejné nastavení jako předtím, ale používá i průvodce, který nepotřebuje tolik horizontální posouvání. Pro nové prostředí nebudete muset měnit existující konfigurace.

- Odvozené přihlašovací údaje
- E-mail
- Certifikát PKCS
- Importovaný certifikát PKCS
- Certifikát SCEP
- Důvěryhodný certifikát
- Síť VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Konfigurace dostupnosti registrace v Portál společnosti pro Android a iOS<!-- 4260128  -->
Můžete nakonfigurovat, jestli registrace zařízení v Portál společnosti v zařízeních s Androidem a iOS jsou k dispozici s výzvami, k dispozici bez výzvy nebo uživatelům nedostupným. Tato nastavení v Intune najdete tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberete přizpůsobení **správy tenanta**  >  **Customization**  >  **Upravit**  >  **registraci zařízení**.  

Podpora nastavení registrace zařízení vyžaduje, aby koncoví uživatelé měli tyto Portál společnosti verze:
-    Portál společnosti v iOS: verze 4,4 nebo novější
-    Portál společnosti na Androidu: verze 5.0.4715.0 nebo novější

Další informace o existujícím přizpůsobení Portál společnosti naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Stránka s přehledem nové sestavy pro Android na zařízeních s Androidem<!-- 5435435   -->
Do konzoly pro správu Microsoft Endpoint Manageru jsme přidali zprávu na stránce Přehled zařízení s Androidem, která zobrazuje, kolik zařízení s Androidem je zaregistrované v jednotlivých řešeních pro správu zařízení. Tento graf (podobně jako stejný graf, který už je v konzole Azure), zobrazuje počet zaregistrovaných zařízení s pracovním profilem, plně spravovaným, vyhrazeným a správcem zařízení. Pokud chcete zobrazit sestavu, vyberte **zařízení**  >  **Android**  >  **Přehled**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Příručka uživatelů ze správy zařízení s Androidem do správy profilů práce<!--5857738   -->
Vydáváme nové nastavení dodržování předpisů pro platformu pro správce zařízení s Androidem. Toto nastavení umožňuje nastavit nekompatibilní zařízení, pokud je spravované pomocí Správce zařízení.

Na těchto nevyhovujících zařízeních se na stránce **aktualizovat nastavení zařízení** uživatelům zobrazí zpráva o **nastavení přesunout na novou správu zařízení** . Pokud klepnete na tlačítko **vyřešit** , provedou se tyto kroky:

1. Rušení registrace správy správců zařízení
2. Registrace ve správě pracovních profilů
3. Řešení problémů s dodržováním předpisů 
 
Google podporuje Správce zařízení v nových verzích Androidu ve snaze přejít na moderní, bohatou a bezpečnější správu zařízení pomocí Androidu Enterprise.  Intune může poskytnout úplnou podporu pro zařízení s Androidem spravovaná pomocí Správce zařízení s Androidem 10 nebo novějším prostřednictvím nástroje Q2 CY2020. Zařízení spravovaná správcem zařízení (s výjimkou Samsung), která po této době používají Android 10 nebo novější, se nebudou moct zcela spravovat. Zvláště ovlivněná zařízení nebudou dostávat nové požadavky na heslo.

Další informace o tomto nastavení najdete v tématu [přesunutí zařízení s Androidem ze Správce zařízení do správy pracovního profilu](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Datový sklad teď poskytuje adresu MAC.<!-- 6123680  -->
Datový sklad Intune poskytuje v entitě adresu MAC jako novou vlastnost ( `EthernetMacAddress` ), `device` která správcům umožňuje korelaci mezi uživatelem a hostitelskou adresou MAC. Tato vlastnost pomáhá oslovit konkrétní uživatele a řešit incidenty, ke kterým dochází v síti. Správci mohou tuto vlastnost také použít v [sestavách Power BI](../developer/reports-proc-get-a-link-powerbi.md) pro sestavování bohatších sestav. Další informace najdete v tématu entita [zařízení](../developer/intune-data-warehouse-collections.md#devices) datového skladu Intune.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Další vlastnosti inventáře zařízení datového skladu<!-- 6125732  -->
Další vlastnosti inventáře zařízení jsou k dispozici v datovém skladu Intune. Následující vlastnosti jsou nyní zpřístupněny prostřednictvím kolekce beta [zařízení](../developer/reports-ref-devices.md#devices) :
- `ethernetMacAddress` – Jedinečný identifikátor sítě tohoto zařízení.
- `model` – Model zařízení.
- `office365Version` – Verze Microsoft 365, která je v zařízení nainstalovaná.
- `windowsOsEdition` – Verze operačního systému.

Následující vlastnosti jsou nyní zpřístupněny prostřednictvím kolekce [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) beta:
- `physicalMemoryInBytes` – Fyzická paměť v bajtech.
- `totalStorageSpaceInBytes` -Celková kapacita úložiště v bajtech.

Další informace najdete v tématu [Microsoft Intune rozhraní API datového skladu](../developer/reports-nav-intune-data-warehouse.md).

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Aktualizace pracovního postupu pomoc a podpora pro podporu dalších služeb<!-- 5654170   -->
Aktualizovali jsme stránku pomoc a podpora v centru pro správu Microsoft Endpoint Manageru, kde teď [zvolíte typ správy, který používáte](get-support.md#options-to-access-help-and-support). Tato změna vám umožní vybrat z následujících typů správy:

- Configuration Manager (zahrnuje analýzu stolního počítače)
- Intune
- Spoluspráva

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Zabezpečení

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Použití náhledu zásad s fokusem správce zabezpečení v rámci zabezpečení koncového bodu<!--6131401  -->
Jako veřejná verze Preview jsme do uzlu Security Endpoint v centru pro správu Microsoft Endpoint Management přidali několik nových skupin zásad. Jako správce zabezpečení můžete tyto nové zásady využít k zaměření na konkrétní aspekty zabezpečení zařízení pro správu diskrétních skupin souvisejících nastavení bez režie většího těla zásad konfigurace zařízení.

S výjimkou nových *antivirových zásad pro antivirová ochrana v programu Microsoft Defender* (viz níže) jsou nastavení v jednotlivých nových zásadách a profilech ve verzi Preview stejná jako nastavení, která jste už mohli nakonfigurovat v [profilech konfigurace zařízení](../configuration/device-profile-create.md) ještě dnes.

Níže jsou uvedené nové typy zásad, které jsou všechny ve verzi Preview, a jejich dostupné typy profilů:

- **Antivirus (Preview)**:
  - macOS:
    - **Antivirová ochrana** – Správa [nastavení zásad](../protect/antivirus-microsoft-defender-settings-macos.md) pro MACOS pro správu ochrany [ATP v programu Microsoft Defender pro Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 a novější:
    - **Antivirová ochrana v programu Microsoft Defender** – spravujte [nastavení zásad](../protect/antivirus-microsoft-defender-settings-windows.md) ochrany před cloudem, vyloučení antivirové ochrany, nápravy, možnosti kontroly a další.

      Antivirový profil pro *antivirovou ochranu v programu Microsoft Defender* je výjimka, která zavádí novou instanci nastavení, která se nachází jako součást profilu omezení zařízení. Tato nová nastavení antivirové ochrany:

        - Jsou stejná nastavení, která se nacházejí v omezeních zařízení, ale podporují třetí možnost konfigurace, která není k dispozici, pokud je nakonfigurovaná jako omezení zařízení.
        - Platí pro zařízení, která jsou spoluspravovaná pomocí Configuration Manager, když je [posuvník úlohy spolusprávy](/configmgr/comanage/how-to-switch-workloads) pro Endpoint Protection nastavený na Intune.

     Naplánujte *použití nového antivirového*  >  profilu*Microsoft Defenderu* místo konfigurace přes profil omezení zařízení.

  - **Prostředí zabezpečení systému Windows** – Spravujte nastavení zabezpečení systému Windows, která koncoví uživatelé mohou zobrazit v centru zabezpečení v programu Microsoft Defender a v oznámeních, která obdrží. Tato nastavení se nezměnila z těch, která jsou k dispozici jako konfigurace zařízení Endpoint Protection Profile.

- **Šifrování disku (Preview)**:
  - macOS:
    - **FileVault**
  - Windows 10 a novější:
    - **BitLocker**
- **Firewall (Preview)**:
  - macOS:
    - **macOS firewall**
  - Windows 10 a novější:
    - **Firewall v programu Microsoft Defender**
- **Detekce a odpověď koncového bodu (Preview)**:
  - Windows 10 a novější: - **Windows 10 Intune**
- **Omezení možností útoku (Preview)**:
  - Windows 10 a novější:
    - **Izolace aplikací a prohlížečů**
    - **Ochrana webu**
    - **Řízení aplikace**
    - **Pravidla pro omezení možností útoku**
    - **Řízení zařízení**
    - **Ochrana Exploit Protection**
- **Ochrana účtů (Preview)**:
  - Windows 10 a novější:
    - **Ochrana účtu**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Týden od 9. března 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Konfigurovat agenta Optimalizace doručení při stahování obsahu aplikace Win32<!-- 5410945 -->

Můžete nakonfigurovat agenta pro optimalizaci doručení ke stažení obsahu aplikace Win32 buď v režimu pozadí, nebo v režimu popředí na základě přiřazení. U stávajících aplikací Win32 bude obsah dál stahovat v režimu pozadí. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **všechny aplikace**  >  *Vybrat vlastnosti aplikace Win32*  >  **Properties**. V poli **přiřazení**vyberte **Upravit** .  Upravte přiřazení výběrem možnosti **Zahrnout** do **režimu** v **požadované** části.  Nové nastavení najdete v části **nastavení aplikace** . Další informace o optimalizaci doručení najdete v tématu [Správa aplikací Win32 – Optimalizace doručení](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Změna primárního uživatele pro zařízení s Windows<!-- 3794742   -->
Můžete změnit primárního uživatele pro zařízení s Windows Hybrid a připojená k Azure AD. Provedete to tak, že přejdete na zařízení **Intune**  >  **Devices**  >  **všechna zařízení** > zvolit **vlastnosti**zařízení >  >  **primární uživatel**. Další informace najdete v tématu [Změna primárního uživatele zařízení](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Pro tuto úlohu se vytvořilo taky nové oprávnění RBAC (spravovaná zařízení/nastavit primárního uživatele). Oprávnění bylo přidáno k předdefinovaným rolím, včetně operátora helpdesku, správce školy a služby Endpoint Security Manager.

Tato funkce se zavede na zákazníky ve verzi Preview globálně. Tato funkce by se měla zobrazit během několika dalších týdnů.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Týden od 2. března 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager spojuje Configuration Manager a Intune s jednou konzolou. Od verze Configuration Manager Technical Preview 2002,2 můžete nahrát vaše Configuration Manager zařízení do cloudové služby a provádět na nich akce v centru pro správu. Další informace najdete v tématu [funkce v Configuration Manager Technical Preview verze 2002,2](/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Před instalací této aktualizace si přečtěte [článek o Configuration Manager Technical Preview](/configmgr/core/get-started/technical-preview) . V tomto článku se seznámíte s obecnými požadavky a omezeními používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.

#### <a name="bulk-remote-actions--4576882--"></a>Hromadné vzdálené akce<!--4576882-->
Nyní můžete vydávat hromadné příkazy pro následující vzdálené akce: restart, přejmenování, autopilot resetování, vymazání a odstranění. Nové hromadné akce zobrazíte tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**  >  **všechna zařízení**  >  **hromadných akcí**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Seznam všech zařízení Vylepšené vyhledávání, řazení a filtrování<!--6179023-->
Seznam všechna zařízení byl vylepšen pro lepší výkon, vyhledávání, řazení a filtrování. Další informace najdete v [tomto popisu podpory](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>Správa aplikací  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Vylepšené prostředí pro přihlašování v Portál společnosti pro Android    
Aktualizovali jsme rozložení několika přihlašovacích obrazovek v aplikaci Portál společnosti pro Android, aby bylo prostředí pro uživatele užitečnější, jednoduché a čisté. Pokud se chcete podívat na vylepšení, přečtěte si téma [co je nového v uživatelském rozhraní aplikace](./whats-new-app-ui.md).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Týden od 24. února 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>vylepšení uživatelského prostředí pro macOS Portál společnosti<!-- 5568987 -->
Provedli jsme vylepšení možností registrace zařízení macOS a aplikace Portál společnosti pro Mac. Zobrazí se následující vylepšení:
- Lepší prostředí Microsoft **AutoUpdate** během registrace, které zajistí, aby vaši uživatelé měli nejnovější verzi portál společnosti.
- Pokročilý krok kontroly dodržování předpisů během registrace.
- Podpora kopírovaných ID incidentů, takže uživatelé můžou rychleji posílat chyby ze svých zařízení do týmu firemní podpory.

Další informace o registraci a Portál společnosti aplikaci pro Mac najdete v tématu [registrace zařízení MacOS pomocí portál společnosti aplikace](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Zásady ochrany aplikací pro lepší mobilní zařízení nyní podporují iOS a iPadOS.<!-- 6224512  -->

V říjnu 2019 zásady ochrany aplikací Intune přidaly možnost využívat data od našich partnerů ochrany před hrozbami Microsoftu. Pomocí této aktualizace teď můžete pomocí zásad ochrany aplikací zablokovat nebo selektivně vymazat podniková data uživatelů na základě stavu zařízení, a to díky lepšímu mobilnímu používání v iOS a iPadOS.  Další informace najdete v tématu [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami v Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Export ze seznamu všechna zařízení nyní ve formátu ZIP CSV<!--6343117-->
Export ze stránky **Devices**  >  **všechna zařízení** jsou teď ve formátu ZIP CSV.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Týden od 17. února 2020 (2002 vydání služby)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Aplikace Microsoft Defender Advanced Threat Protection (ATP) pro macOS<!-- 5424618 -->
Intune poskytuje snadný způsob, jak nasadit aplikaci Microsoft Defender Advanced Threat Protection (ATP) pro macOS do spravovaných zařízení Mac. Další informace najdete v tématu [Přidání ATP v programu Microsoft Defender do zařízení MacOS pomocí Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) a [programu Microsoft Defender Advanced Threat Protection for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Povolení řízení přístupu k síti (NAC) pomocí Cisco AnyConnect VPN na zařízeních s iOS<!-- 4860111  -->
Na zařízeních se systémem iOS můžete vytvořit profil sítě VPN a použít jiné typy připojení, včetně Cisco AnyConnect (profily**Konfigurace zařízení**  >  **Profiles**  >  **vytvořit profil**  >  **iOS** pro Platform > **VPN** pro typ profilu > **Cisco AnyConnect** pro typ připojení).

Pomocí Cisco AnyConnect můžete povolit řízení přístupu k síti (NAC). Chcete-li použít tuto funkci:

1. V [příručce pro správce modulu Cisco identity Services](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)použijte postup v části **Konfigurace Microsoft Intune jako MDM Server** ke konfiguraci modulu Cisco identity Services Engine (ISE) v Azure.
2. V profilu konfigurace zařízení v Intune vyberte nastavení **povolit Access Control sítě (NAC)** .

Všechna dostupná nastavení sítě VPN zobrazíte tak, že přejdete na [Konfigurace nastavení sítě VPN na zařízeních s iOS](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Sériové číslo na stránce Apple MDM push Certificate<!--5947765  -->
Na stránce Apple MDM push Certificate se teď zobrazí sériové číslo. Sériové číslo je potřeba k opětovnému získání přístupu k certifikátu Apple MDM push Certificate, pokud dojde ke ztrátě přístupu k Apple ID, které vytvořilo certifikát. Sériové číslo zobrazíte tak, že přejdete na **zařízení**  >  **iOS**  >  **iOS registrace**  >  **Apple MDM push Certificate**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nové možnosti plánu aktualizace pro doručování aktualizací operačního systému do zaregistrovaných zařízení se systémem iOS/iPadOS<!--5879689  -->
Při plánování aktualizací operačního systému pro zařízení s iOS/iPadOS si můžete vybrat z následujících možností. Tyto možnosti se vztahují na zařízení, která používají typy registrace Apple Business Manageru nebo Apple School Manager.
- Aktualizovat při dalším vrácení se změnami
- Aktualizovat během naplánovaného času
- Aktualizace mimo plánovaný čas

Pro tyto dvě možnosti můžete vytvořit několik časových oken.

Nové možnosti zobrazíte tak, že přejdete na adresu mem > **zařízení**  >  **iOS**  >  **Aktualizace zásady pro iOS/iPadOS**  >  **vytvořit profil**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Zvolit aktualizace pro iOS/iPadOS, které se mají vložit do zaregistrovaných zařízení<!--5879689  -->
Můžete zvolit konkrétní aktualizaci pro iOS/iPadOS (s výjimkou nejnovější aktualizace), která bude nabízet zařízení, která jsou zaregistrovaná pomocí nástroje Apple Business Manager nebo Apple School Manager. Taková zařízení musí mít zásady konfigurace zařízení nastavené tak, aby po dobu určitého počtu dnů zpozdily přehlednost aktualizace softwaru. Tuto funkci zobrazíte tak, že přejdete do paměti mem > **zařízení**  >  **iOS**  >  **Aktualizace zásady pro iOS/iPadOS**  >  **vytvořit profil**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Vylepšené prostředí pro vytváření sestav v Intune<!-- 3791418   -->
Intune teď nabízí vylepšené možnosti vytváření sestav, včetně nových typů sestav, lepších organizací sestav, pokročilejších zobrazení, vylepšených funkcí sestav a také konzistentních a včasných dat. Možnosti vytváření sestav budou přesunuty z verze Public Preview na GA (všeobecně dostupná). Kromě toho bude verze GA poskytovat podporu lokalizace, opravy chyb, vylepšení návrhu a agregovaná data o dodržování předpisů zařízeními na dlaždicích v [centru pro správu Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Nové typy sestav se zaměřují na následující informace:

- **Provozní** – poskytuje nové záznamy s negativním důrazem na stav. 
- **Organizace** – poskytuje širší souhrn celkového stavu.
- **Historická** – poskytuje vzory a trendy v časovém intervalu.
- **Specialista** – umožňuje používat nezpracovaná data k vytváření vlastních sestav.

První sada nových sestav se zaměřuje na dodržování předpisů zařízením. Další informace najdete v tématu [Microsoft Intune pro vytváření sestav](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) a [sestavy Intune](reports.md)v rámci blogů.

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Konsoliduje umístění standardních hodnot zabezpečení v uživatelském rozhraní.<!-- 6177074   -->
V centru pro správu Microsoft Endpoint Manageru jsme provedli sloučení cest k vyhledání [standardních hodnot zabezpečení](../protect/security-baselines.md) , a to odebráním *standardních hodnot zabezpečení* z několika umístění uživatelského rozhraní. Pokud chcete najít standardní hodnoty zabezpečení, použijte následující cestu: **Endpoint security**  >  **základní hodnoty zabezpečení**Endpoint Security.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Rozšířená podpora importovaných certifikátů PKCS<!-- 6044197  -->
Rozšířili jsme podporu použití [importovaných certifikátů PKCS](../protect/certificates-imported-pfx-configure.md#supported-platforms) k podpoře *plně spravovaných zařízení s Androidem Enterprise*. Obecně platí, že import certifikátů PFX se používá pro scénáře šifrování S/MIME, kde se na všech zařízeních vyžadují šifrovací certifikáty uživatele, aby mohlo dojít k dešifrování e-mailu.

Následující platformy podporují import certifikátů PFX:

- Android – Správce zařízení
- Android Enterprise – plně spravovaná
- Android Enterprise – pracovní profil
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Zobrazit konfiguraci zabezpečení koncového bodu pro zařízení<!-- 6206460  -->
Aktualizovali jsme název možnosti v centru pro správu Microsoft Endpoint Manageru, aby se zobrazily [Konfigurace zabezpečení koncového bodu, které se vztahují na konkrétní zařízení](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). Tato možnost se přejmenuje na **konfiguraci zabezpečení koncového bodu** , protože zobrazuje příslušné standardní hodnoty zabezpečení a další zásady vytvořené mimo standardní hodnoty zabezpečení. Dříve byla tato možnost pojmenována jako *směrné plány zabezpečení*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Připravujeme změny uživatelských rozhraní rolí Intune<!--5801612   -->
Uživatelské rozhraní pro role správce klienta [služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Tenant administration**  >  **Roles** bylo vylepšeno na uživatelsky přívětivější a intuitivní návrh. Toto prostředí nabízí stejné nastavení a podrobnosti, které teď použijete, ale nové prostředí využívá proces podobný průvodci.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Týden od 17. února 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="microsofts-new-office-app---5859926---"></a>Nová aplikace Office v Microsoftu<!-- 5859926 -->
Nová aplikace Office je teď všeobecně dostupná ke stažení a použití. Aplikace Office je konsolidované prostředí, ve kterém můžou uživatelé pracovat přes Word, Excel a PowerPoint v rámci jedné aplikace. Aplikaci můžete cílit pomocí zásady ochrany aplikací, aby se zajistila ochrana dat, ke kterým se dostanete.

Další informace najdete v tématu [Jak povolit zásady ochrany aplikací Intune v aplikaci Office Mobile Preview](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Týden od 10. února 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 končí rozšířenou podporou<!--3042987 -->
Systém Windows 7 dosáhl konce rozšířené podpory od 14. ledna 2020. Intune zastaralá podpora pro zařízení s Windows 7 ve stejnou dobu. Technickou pomoc a automatické aktualizace, které vám pomůžou chránit váš počítač, už nejsou dostupné. Měli byste upgradovat na Windows 10. Další informace najdete v [blogovém příspěvku plán změn](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge verze 77 a novější na zařízeních s Windows 10<!-- 5843584 -->
Intune teď podporuje odinstalaci Microsoft Edge verze 77 a novější na zařízeních s Windows 10. Další informace najdete v tématu [Přidání Microsoft Edge pro Windows 10 do Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Obrazovka, která se odebrala z Portál společnosti, registrace pracovních profilů Android<!--6103987 -->
Obrazovka **co dál?** byla odebrána z toku registrace pracovního profilu Androidu v portál společnosti, aby se zjednodušilo uživatelské prostředí. Pokud chcete zobrazit aktualizovaný tok zápisu pracovních profilů Androidu, přejděte k části [registrace v pracovním profilu Android](../user-help/enroll-device-android-work-profile.md) .  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Vylepšený výkon aplikace Portál společnosti<!-- 6178652 -->
Aplikace Portál společnosti se aktualizovala tak, aby podporovala Vylepšený výkon pro zařízení, která používají procesory ARM64, jako je Surface Pro X. dřív, Portál společnosti provozovaná v emulovaném režimu ARM32. Ve verzi 10.4.7080.0 a vyšších se teď aplikace Portál společnosti nativně zkompiluje pro ARM64. Další informace o aplikaci Portál společnosti naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

## <a name="whats-new-archive"></a>Archiv co je nového
V předchozích měsících se podívejte do [archivu co je nového](whats-new-archive.md).

## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
