---
title: Novinky v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Zjistěte, jaké novinky přináší portál Intune Azure.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/13/2020
ms.topic: conceptual
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
ms.openlocfilehash: 3d7b57e0c4a667e4023dc6ce0e089572fd5b00e0
ms.sourcegitcommit: b5a9ce31de743879d2a6306cea76be3a093976bb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/14/2020
ms.locfileid: "79372598"
---
# <a name="whats-new-in-microsoft-intune"></a>Co je nového ve Microsoft Intune

Podívejte se, co je nového v každém týdnu v Microsoft Intune. Můžete také najít [důležitá oznámení](#notices), [Minulá vydání](whats-new-archive.md)a informace o [tom, jak jsou aktualizace služby Intune vydané](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

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
-->  

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Týden od 9. března 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Konfigurovat agenta Optimalizace doručení při stahování obsahu aplikace Win32<!-- 5410945 -->

Můžete nakonfigurovat agenta pro optimalizaci doručení ke stažení obsahu aplikace Win32 buď v režimu pozadí, nebo v režimu popředí na základě přiřazení. U stávajících aplikací Win32 bude obsah dál stahovat v režimu pozadí. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **všechny aplikace** > *Vyberte vlastnosti aplikace Win32* > **Properties**. V poli **přiřazení**vyberte **Upravit** .  Upravte přiřazení výběrem možnosti **Zahrnout** do **režimu** v **požadované** části.  Nové nastavení najdete v části **nastavení aplikace** . Další informace o optimalizaci doručení najdete v tématu [Správa aplikací Win32 – Optimalizace doručení](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="change-primary-user-for-windows-devices---3794742-idready-wnready---"></a>Změna primárního uživatele pro zařízení s Windows<!-- 3794742 idready wnready -->
Můžete změnit primárního uživatele pro zařízení s Windows Hybrid a připojená k Azure AD. Provedete to tak, že přejdete na **zařízení** > **Intune** > **všechna zařízení** > vyberte zařízení > **vlastnosti** > **primární uživatel**. Další informace najdete v tématu [Změna primárního uživatele zařízení](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Pro tuto úlohu se vytvořilo taky nové oprávnění RBAC (spravovaná zařízení/nastavit primárního uživatele). Oprávnění bylo přidáno k předdefinovaným rolím, včetně operátora helpdesku, správce školy a služby Endpoint Security Manager.

Tato funkce se zavede na zákazníky ve verzi Preview globálně. Tato funkce by se měla zobrazit během několika dalších týdnů.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Týden od 2. března 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager spojuje Configuration Manager a Intune s jednou konzolou. Od verze Configuration Manager Technical Preview 2002,2 můžete nahrát vaše Configuration Manager zařízení do cloudové služby a provádět na nich akce v centru pro správu. Další informace najdete v tématu [funkce v Configuration Manager Technical Preview verze 2002,2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Před instalací této aktualizace si přečtěte [článek o Configuration Manager Technical Preview](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) . V tomto článku se seznámíte s obecnými požadavky a omezeními používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.

#### <a name="bulk-remote-actions--4576882--"></a>Hromadné vzdálené akce<!--4576882-->
Nyní můžete vydávat hromadné příkazy pro následující vzdálené akce: restart, přejmenování, autopilot resetování, vymazání a odstranění. Pokud chcete zobrazit nové hromadné akce, přejděte do [centra pro správu Microsoft Endpoint manageru](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení** > **všechna zařízení** > **hromadných akcí**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Seznam všech zařízení Vylepšené vyhledávání, řazení a filtrování<!--6179023-->
Seznam všechna zařízení byl vylepšen pro lepší výkon, vyhledávání, řazení a filtrování. Další informace najdete v [tomto popisu podpory](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Týden od 24. února 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>vylepšení uživatelského prostředí pro macOS Portál společnosti<!-- 5568987 -->
Provedli jsme vylepšení možností registrace zařízení macOS a aplikace Portál společnosti pro Mac. Zobrazí se následující:
- Lepší prostředí Microsoft **AutoUpdate** během registrace, které zajistí, aby vaši uživatelé měli nejnovější verzi portál společnosti.
- Pokročilý krok kontroly dodržování předpisů během registrace.
- Podpora kopírovaných ID incidentů, takže uživatelé můžou rychleji posílat chyby ze svých zařízení do týmu firemní podpory.

Další informace o registraci a Portál společnosti aplikaci pro Mac najdete v tématu [registrace zařízení MacOS pomocí portál společnosti aplikace](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Zásady ochrany aplikací pro lepší mobilní zařízení nyní podporují iOS a iPadOS.<!-- 6224512  -->

V říjnu 2019 zásady ochrany aplikací Intune přidaly možnost využívat data od našich partnerů ochrany před hrozbami Microsoftu. Pomocí této aktualizace teď můžete pomocí zásad ochrany aplikací zablokovat nebo selektivně vymazat podniková data uživatelů na základě stavu zařízení, a to díky lepšímu mobilnímu používání v iOS a iPadOS.  Další informace najdete v tématu [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami v Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Export ze seznamu všechna zařízení nyní ve formátu ZIP CSV<!--6343117-->
Export ze stránky **zařízení** > **všechna zařízení** jsou teď ve formátu ZIP CSV.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Týden od 17. února 2020 (2002 vydání služby)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Aplikace Microsoft Defender Advanced Threat Protection (ATP) pro macOS<!-- 5424618 -->
Intune poskytuje snadný způsob, jak nasadit aplikaci Microsoft Defender Advanced Threat Protection (ATP) pro macOS do spravovaných zařízení Mac. Další informace najdete v tématu [Přidání ATP v programu Microsoft Defender do zařízení MacOS pomocí Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) a [programu Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Povolení řízení přístupu k síti (NAC) pomocí Cisco AnyConnect VPN na zařízeních s iOS<!-- 4860111  -->
Na zařízeních se systémem iOS můžete vytvořit profil sítě VPN a použít jiné typy připojení, včetně Cisco AnyConnect (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro Platform > **VPN** pro typ profilu > **Cisco AnyConnect** pro typ připojení).

Pomocí Cisco AnyConnect můžete povolit řízení přístupu k síti (NAC). Chcete-li použít tuto funkci:

1. V [příručce pro správce modulu Cisco identity Services](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)použijte postup v části **Konfigurace Microsoft Intune jako MDM Server** ke konfiguraci modulu Cisco identity Services Engine (ISE) v Azure.
2. V profilu konfigurace zařízení v Intune vyberte nastavení **povolit Access Control sítě (NAC)** .

Všechna dostupná nastavení sítě VPN zobrazíte tak, že přejdete na [Konfigurace nastavení sítě VPN na zařízeních s iOS](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Sériové číslo na stránce Apple MDM push Certificate<!--5947765  -->
Na stránce Apple MDM push Certificate se teď zobrazí sériové číslo. Sériové číslo je potřeba k opětovnému získání přístupu k certifikátu Apple MDM push Certificate, pokud dojde ke ztrátě přístupu k Apple ID, které vytvořilo certifikát. Pokud se chcete podívat na sériové číslo, přejděte na **zařízení** > **iOS** > **iOS registrace** > **Apple MDM push Certificate**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nové možnosti plánu aktualizace pro doručování aktualizací operačního systému do zaregistrovaných zařízení se systémem iOS/iPadOS<!--5879689  -->
Při plánování aktualizací operačního systému pro zařízení s iOS/iPadOS si můžete vybrat z následujících možností. To platí pro zařízení, která používají typy registrace Apple Business Manageru nebo Apple School Manager.
- Aktualizovat při dalším vrácení se změnami
- Aktualizovat během naplánovaného času
- Aktualizace mimo plánovaný čas

Pro tyto dvě možnosti můžete vytvořit několik časových oken.

Nové možnosti zobrazíte tak, že přejdete na **zařízení** MEM **>**  > **zásady pro iOS > Update pro iOS/iPadOS** > **vytvořit profil**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Zvolit aktualizace pro iOS/iPadOS, které se mají vložit do zaregistrovaných zařízení<!--5879689  -->
Můžete zvolit konkrétní aktualizaci pro iOS/iPadOS (s výjimkou nejnovější aktualizace), která bude nabízet zařízení, která jsou zaregistrovaná pomocí nástroje Apple Business Manager nebo Apple School Manager. Taková zařízení musí mít zásady konfigurace zařízení nastavené tak, aby po dobu určitého počtu dnů zpozdily přehlednost aktualizace softwaru. Tuto funkci zobrazíte tak, že přejdete na **zařízení** MEM > > zásady pro **iOS > ** **Update pro iOS/iPadOS** > **vytvořit profil**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Vylepšené prostředí pro vytváření sestav v Intune<!-- 3791418   -->
Intune teď nabízí vylepšené možnosti vytváření sestav, včetně nových typů sestav, lepších organizací sestav, pokročilejších zobrazení, vylepšených funkcí sestav a také konzistentních a včasných dat. Možnosti vytváření sestav budou přesunuty z verze Public Preview na GA (všeobecně dostupná). Kromě toho bude verze GA poskytovat podporu lokalizace, opravy chyb, vylepšení návrhu a agregovaná data o dodržování předpisů zařízeními na dlaždicích v [centru pro správu Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Nové typy sestav se zaměřují na následující:

- **Provozní** – poskytuje nové záznamy s negativním důrazem na stav. 
- **Organizace** – poskytuje širší souhrn celkového stavu.
- **Historická** – poskytuje vzory a trendy v časovém intervalu.
- **Specialista** – umožňuje používat nezpracovaná data k vytváření vlastních sestav.

První sada nových sestav se zaměřuje na dodržování předpisů zařízením. Další informace najdete v tématu [Microsoft Intune pro vytváření sestav](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) a [sestavy Intune](reports.md)v rámci blogů.

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Konsoliduje umístění standardních hodnot zabezpečení v uživatelském rozhraní.<!-- 6177074   -->
V centru pro správu Microsoft Endpoint Manageru jsme provedli sloučení cest k vyhledání [standardních hodnot zabezpečení](../protect/security-baselines.md) , a to odebráním *standardních hodnot zabezpečení* z několika umístění uživatelského rozhraní. Chcete-li najít směrné plány zabezpečení, použijte následující cestu: **zabezpečení koncového bodu** > **úrovně zabezpečení**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197-wnready---"></a>Rozšířená podpora importovaných certifikátů PKCS<!-- 6044197 WNReady -->
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
Uživatelské rozhraní pro centrum pro správu [služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **správu tenanta** > **rolích** bylo vylepšeno na uživatelsky přívětivější a intuitivní návrh. Toto prostředí nabízí stejné nastavení a podrobnosti, které teď použijete, ale nové prostředí využívá proces podobný průvodci.

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

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>Týden od 27. ledna 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Podpora Intune pro další kanál nasazení Microsoft Edge verze 77 pro macOS<!-- 5983950  -->
Microsoft Intune teď podporuje dodatečný **stabilní** kanál nasazení pro aplikaci Microsoft Edge pro MacOS. **Stabilní** kanál je doporučeným kanálem pro nasazení Microsoft Edge v rozlehlých sítích v podnikovém prostředí. Aktualizuje se každých šest týdnů, přičemž každá verze zahrnuje vylepšení z **verze beta** kanálu. Kromě **stabilních** a **beta** kanálů podporuje Intune kanál pro **vývoj** . Verze Public Preview nabízí stabilní a vývojářské kanály pro Microsoft Edge verze 77 a novější pro macOS. Automatické aktualizace prohlížeče jsou ve výchozím nastavení zapnuté. Další informace najdete v tématu [Přidání Microsoft Edge pro zařízení MacOS pomocí Microsoft Intune](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Vyřazení Intune Managed Browser<!--5728447 -->
Intune Managed Browser bude vyřazen. Využijte Microsoft Edge pro vaše chráněné prostředí Intune Browser. Další informace najdete v části "provedení akce" v tématu[použití Microsoft Edge pro chráněné prostředí Intune prohlížeče](whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience)v níže uvedené části [oznámení](whats-new.md#notices) .

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Týden od 20. ledna 2020 (vydání služby 2001)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Změna uživatelského prostředí při přidávání aplikací do Intune<!-- 4705829   -->
Při přidávání aplikací přes Intune se zobrazí nové uživatelské prostředí. Toto prostředí obsahuje stejné nastavení a podrobnosti, které jste použili dříve, ale nové prostředí se před přidáním aplikace do Intune řídí procesem podobným průvodci. Toto nové prostředí poskytuje před přidáním aplikace také stránku s přehledem. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **všechny aplikace** > **Přidat**. Další informace najdete v článku [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Vyžadovat restartování aplikací Win32 <!-- 5622282   -->
Můžete vyžadovat, aby se aplikace Win32 po úspěšné instalaci restartovala. Můžete také zvolit dobu (dobu odkladu), než se musí vykonat restart.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Změna uživatelského prostředí při konfiguraci aplikací v Intune<!-- 4207990   -->
Při vytváření zásad konfigurace aplikací v Intune se zobrazí nové uživatelské prostředí. Toto prostředí obsahuje stejné nastavení a podrobnosti, které jste použili dříve, ale nové prostředí se před přidáním zásady do Intune řídí procesem podobným průvodci. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **zásady konfigurace aplikací** > **Přidat**. Další informace najdete v tématu [zásady konfigurace aplikací pro Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Podpora Intune pro další kanál nasazení Microsoft Edge pro Windows 10<!-- 5861774 -->
Microsoft Intune teď podporuje dodatečný **stabilní** kanál nasazení pro aplikaci Microsoft Edge (verze 77 a novější) pro Windows 10. **Stabilní** kanál je doporučeným kanálem pro široce nasazený Microsoft Edge pro Windows 10 v podnikových prostředích. Tento kanál se aktualizuje každých šest týdnů, přičemž každá verze zahrnuje vylepšení z **verze beta** kanálu. Kromě **stabilních** a **beta** kanálů podporuje Intune kanál pro **vývoj** . Další informace najdete v tématu [Microsoft Edge pro Windows 10 – Konfigurace nastavení aplikace](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Vylepšené uživatelské rozhraní při konfiguraci rozhraní Exchange ActiveSync On-Premises Connector<!-- 5695492   -->
Aktualizovali jsme prostředí pro [konfiguraci konektoru Exchange ActiveSync On-Premises Connector](../protect/exchange-connector-install.md). V aktualizovaném prostředí se používá jedno podokno ke konfiguraci, úpravám a sumarizaci podrobností o místních konektorech.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Přidání automatických nastavení proxy do profilů sítě Wi-Fi pro pracovní profily Android Enterprise<!-- 4490822   -->
Na zařízeních se systémem Android Enterprise Work Profiles můžete vytvořit profily sítě Wi-Fi. Když vyberete typ sítě Wi-Fi, můžete také zadat typ protokolu EAP (Extensible Authentication Protocol), který se používá ve vaší síti Wi-Fi.

Když teď zvolíte typ podniku, můžete taky zadat automatické nastavení proxy serveru, včetně proxy server URL, jako je například `proxy.contoso.com`.

Pokud chcete zobrazit aktuální nastavení Wi-Fi, která můžete nakonfigurovat, přejděte na [Přidat nastavení Wi-Fi pro zařízení s Androidem Enterprise a Androidem v Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Platí pro:
- Pracovní profil Android Enterprise

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Blokovat registraci Androidu podle výrobce zařízení<!--5197392  -->
Můžete blokovat registraci zařízení na základě výrobce zařízení. To platí pro správce zařízení s Androidem a zařízení s Androidem Enterprise Work Profile. Omezení registrace zobrazíte tak, že přejdete do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení** > **omezení registrace**.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Vylepšení uživatelského rozhraní profilu typu registrace pro iOS/iPadOS<!-- 6055005 -->
Pro registraci uživatele pro iOS/iPadOS se stránka **Vytvoření nastavení profilu typu registrace** **Settings** zjednodušila a vylepšuje proces volby **typu registrace** a zároveň zachovává stejné funkce. Nové uživatelské rozhraní zobrazíte tak, že přejdete do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení** > **ios** > **registrace systému ios** > **typy registrace** > **vytvořit profil** > **Nastavení** stránky. Další informace najdete v tématu [Vytvoření profilu registrace uživatele v Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Podrobnosti o nových informacích o zařízení<!-- 4471759 5604099  -->
Následující informace jsou nyní na stránce **Přehled** pro zařízení:
- Kapacita paměti (množství fyzické paměti v zařízení)
- Kapacita úložiště (množství fyzického úložiště v zařízení) 
- Architektura procesoru

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>iOS obejít Zámek aktivace vzdálenou akci přejmenována, aby se zakázalo Zámek aktivace <!--5904591  -->
**Zámek aktivace pro obejití** vzdálené akce byla přejmenována, aby **zámek aktivace zakázáno**. Další informace najdete v tématu [zakázání zámek aktivace iOS s Intune](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Podpora nasazení aktualizací funkcí Windows 10 pro zařízení autopilotu<!-- 5948137   -->
Intune teď podporuje cílení na registrovaná zařízení s autopilotem pomocí [nasazení aktualizací funkcí Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

Zásady aktualizace funkcí Windows 10 se nedají použít při počátečním nastavování funkce autopilot (OOBE) a budou se používat jenom při první web Windows Update kontrole po dokončení zřizování zařízení (což je obvykle den).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Sestavy nasazení Windows autopilotu (Preview) <!-- 3856172   -->
Nová sestava podrobně popisuje každé zařízení nasazené prostřednictvím Windows autopilotu. Další informace najdete v tématu [Sestava nasazení autopilotu](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Nová integrovaná role Endpoint Manageru pro Intune<!--4253397   -->
K dispozici je nová integrovaná role Intune: Správce služby Endpoint Security. Tato nová role poskytuje správcům úplný přístup k uzlu Správce koncových bodů v Intune a jenom k ostatním oblastem. Role je rozšířením role správce zabezpečení ze služby Azure AD. Pokud aktuálně máte jenom globální správce jako role, pak se nevyžadují žádné změny. Pokud používáte role a chcete členitost, kterou poskytuje Endpoint Security Manager, pak tuto roli přiřaďte, až bude k dispozici. Další informace o předdefinovaných rolích najdete v tématu [řízení přístupu na základě role](role-based-access-control.md).

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>Týden od 6. ledna 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>Podpora S/MIME pro Microsoft Outlook pro iOS<!-- 2669398 -->
Intune podporuje doručování podpisových a šifrovacích certifikátů S/MIME, které se dají používat s Outlookem pro iOS na zařízeních s iOS. Další informace najdete v tématu [citlivostní označování a ochrana v Outlooku pro iOS a Android](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Mezipaměť obsahu aplikace Win32 pomocí serveru s připojenou mezipamětí společnosti Microsoft<!-- 6030314 -->
Server Microsoft Connected cache můžete nainstalovat do distribučních bodů Configuration Manager pro ukládání obsahu aplikace Win32 v Intune. Další informace najdete v tématu věnovaném [podpoře aplikací pro Intune Win32 v Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Profily šablon pro správu Windows 10 (ADMX) nyní podporují značky oboru <!--5137390 -->
Nyní můžete přiřadit značky oboru k profilům šablony pro správu (ADMX). Provedete to tak, že přejdete na **zařízení** > **Intune** > **konfiguračních profilů** > vyberte profil šablon pro správu v seznamu > **vlastnosti** > **značky oboru**. Další informace o značkách oboru naleznete v tématu [přiřazení značek oboru jiným objektům](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Týden od 30. prosince 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Načtení osobního obnovovacího klíče ze zařízení s macOS šifrovaným zařízením MEM<!-- 4851745 -->
Koncoví uživatelé mohou načíst svůj osobní obnovovací klíč (klíč trezoru) pomocí aplikace Portál společnosti pro iOS. Zařízení, které má osobní obnovovací klíč, musí být zaregistrované v Intune a zašifrované pomocí trezoru služby prostřednictvím Intune. Pomocí aplikace Portál společnosti pro iOS může koncový uživatel na své šifrované zařízení macOS načíst svůj osobní obnovovací klíč tak, že klikne na **získat obnovovací klíč**. Obnovovací klíč můžete z Intune načíst taky tak, že vyberete **zařízení** > *šifrovaných a zaregistrovaných zařízení MacOS* > **získat obnovovací klíč**. Další informace o trezoru úložišť najdete v tématu [šifrování trezoru MacOS](../protect/encrypt-devices.md#filevault-encryption-for-macos).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>aplikace VPP pro iOS a iPadOS, které jsou pro uživatele licencované<!-- 5619268 -->
Pro uživatelem zaregistrovaná zařízení s iOS a iPadOS se koncovým uživatelům už nebudou prezentovat nově vytvořeným aplikacím VPP licencovaným na zařízení, které jsou nasazené jako dostupné. Koncoví uživatelé ale budou dál zobrazovat všechny aplikace VPP licencované uživateli v rámci Portál společnosti. Další informace o aplikacích VPP najdete v tématu [Správa aplikací pro iOS a MacOS zakoupených prostřednictvím Apple Volume purchase program s Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Týden od 23. prosince 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Oznámení – systém Windows 10 1703 (RS2) se bude pohybovat mimo podporu. <!-- 5026679 -->
Od 9. října 2018 se Windows 10 1703 (RS2) přesunul z podpory platformy Microsoft pro edice Home, pro a pro Workstation. Pro edice Windows 10 Enterprise a školství se v systému Windows 10 1703 (RS2) přesunula podpora platformy 8. října 2019. Od 26. prosince 2019 budeme aktualizovat minimální verzi Windows Portál společnosti aplikace na Windows 10 1709 (RS3). Počítače s verzemi staršími než 1709 nebudou nadále získávat aktualizované verze aplikace z Microsoft Store. Tuto změnu jsme dřív komunikovali zákazníkům, kteří spravují starší verze Windows 10 prostřednictvím centra zpráv. Další informace najdete v tématu [seznam faktů pro životní cyklus systému Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Týden od 16. prosince 2019

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Aktualizace Šablony pro správu pro zařízení s Windows 10 <!-- 5941568 -->

Šablony ADMX v Microsoft Intune můžete použít k řízení a správě nastavení pro Microsoft Edge, Office a Windows. Šablony pro správu v Intune provedli následující aktualizace nastavení zásad:

- Přidání podpory pro Microsoft Edge verze 78 a 79.
- Obsahuje 11. listopadu 2019 soubory ADMX v [souborech šablon pro správu (ADMX/ADML) a nástroji pro přizpůsobení sady Office pro office 365 ProPlus, office 2019 a office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

Další informace o šablonách ADMX v Intune najdete v tématu [použití šablon Windows 10 ke konfiguraci nastavení zásad skupiny v Microsoft Intune](../configuration/administrative-templates-windows.md).

Platí pro:

- Windows 10 a novější

## <a name="week-of-december-9-2019-1912-service-release"></a>Týden z 9. prosince 2019 (verze 1912 Service)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migrace na Microsoft Edge pro spravované scénáře procházení<!-- 5173762 -->
Až se přiblížíme k odchodu Intune Managed Browser, provedli jsme změny v zásadách ochrany aplikací, abychom zjednodušili kroky potřebné k přesunu uživatelů do hraničních zařízení. Aktualizovali jsme možnosti nastavení zásad ochrany aplikací **omezit přenos webového obsahu s jinými aplikacemi** na jednu z těchto možností:

- Libovolná aplikace
- Intune Managed Browser
- Microsoft Edge
- Nespravovaný prohlížeč 

Když vyberete **Microsoft Edge**, koncovým uživatelům se zobrazí zpráva podmíněného přístupu s upozorněním, že pro spravované scénáře procházení se vyžaduje Microsoft Edge. Budou se vám zobrazovat výzvy ke stažení a přihlášení k Microsoft Edge pomocí svých účtů AAD, pokud se ještě neudělaly.  To bude odpovídat na cílení aplikací s povoleným MAM s nastavením konfigurace aplikace `com.microsoft.intune.useEdge` nastavenou na **hodnotu true**. Existující zásady ochrany aplikací, které používaly nastavení **prohlížeče spravované pomocí zásad** , budou teď **Intune Managed Browser** vybrané a v chování se zobrazí žádná změna. To znamená, že uživatelé uvidí zprávy o používání Microsoft Edge, pokud jste nastavili nastavení konfigurace aplikace **useEdge** na **hodnotu true**. Pro všechny zákazníky, kteří využívají spravované scénáře procházení, doporučujeme aktualizovat zásady ochrany aplikací tak, aby **omezili přenos webového obsahu s jinými aplikacemi** , aby uživatelům viděli správné pokyny k přechodu na Microsoft Edge bez ohledu na to, ze které aplikace spouští odkazy. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Konfigurace obsahu oznámení aplikace pro účty organizace<!-- 2576686  -->
Zásady ochrany aplikací Intune (aplikace) na zařízeních s Androidem a iOS umožňují řídit obsah oznámení aplikací pro účty org. Můžete vybrat možnost (povolení, blokování dat organizace nebo blokované) a určit, jak se budou zobrazovat oznámení pro účty organizace pro vybranou aplikaci. Tato funkce vyžaduje podporu aplikací a nemusí být k dispozici pro všechny aplikace s podporou aplikací. Toto nastavení bude podporovat Outlook pro iOS verze 4.15.0 (nebo novější) a Outlook pro Android 4.83.0 (nebo novější). Nastavení je k dispozici v konzole nástroje, ale funkce začnou platit až od 16. prosince 2019. Další informace o aplikaci najdete v tématu [co jsou zásady ochrany aplikací?](../apps/app-protection-policy.md).

#### <a name="microsoft-app-icons-update--4677605----"></a>Aktualizace ikon aplikace Microsoft<!--4677605  -->
Ikony používané pro aplikace Microsoftu v podokně cílení aplikace pro zásady ochrany aplikací a zásady konfigurace aplikací se aktualizovaly.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Vyžadovat použití schválených klávesnic v Androidu<!--4761794  -->
V rámci zásad ochrany aplikací můžete určit nastavení [**schválených klávesnic**](../apps/app-protection-policy-settings-android.md#data-protection) pro správu, které klávesnice pro Android se dají používat se spravovanými aplikacemi pro Android. Když uživatel otevře spravovanou aplikaci a ještě nepoužívá schválenou klávesnici pro tuto aplikaci, zobrazí se výzva k přepnutí na jednu ze schválených klávesnic, které už jsou na svém zařízení nainstalované. V případě potřeby se jim zobrazí odkaz pro stažení schválené klávesnice z Obchod Google Play, kterou si můžete nainstalovat a nastavit. Uživatel může upravit textová pole ve spravované aplikaci, když jejich aktivní klávesnice není jednou ze schválených klávesnic.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Aktualizované prostředí jednotného přihlašování pro aplikace a weby na zařízeních s iOS, iPadOS a macOS<!-- 4999578  -->
Intune přidal pro zařízení s iOS, iPadOS a macOS další nastavení jednotného přihlašování (SSO). Teď můžete nakonfigurovat rozšíření aplikace jednotného přihlašování napsané vaší organizací nebo vaším poskytovatelem identity. Tato nastavení slouží ke konfiguraci bezproblémového jednotného přihlašování pro aplikace a weby, které používají moderní metody ověřování, jako je OAuth a typu Saml2. 

Tato nová nastavení se rozšíří na předchozí nastavení rozšíření aplikace jednotného přihlašování a integrovaného rozšíření protokolu Kerberos (**zařízení** > **Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS/iPadOS** nebo **MacOS** pro typ platformy > **funkce zařízení** pro typ profilu). 

Pokud chcete zobrazit celou škálu nastavení rozšíření aplikace jednotného přihlašování, přejděte na adresu [SSO v iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) a [jednotné přihlašování v MacOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Platí pro:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Aktualizovali jsme dvě nastavení omezení pro zařízení s iOS a iPadOS, abyste mohli opravit jejich chování.<!-- 5701352    -->
V případě zařízení se systémem iOS můžete vytvořit profily omezení zařízení, které **umožní dopředné aktualizace PKI** a **blokovat režim s omezeným přístupem USB** (**zařízení** > **konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS/iPadOS** pro omezení platformy > **zařízení** pro typ profilu). Před touto verzí bylo nastavení uživatelského rozhraní a popisy pro následující nastavení nesprávné a byly nyní opraveny. Od této verze je chování nastavení následující:

**Zablokovat vysoce Air aktualizace PKI**: **blok** znemožní uživatelům přijímat aktualizace softwaru, pokud není zařízení připojené k počítači. **Nenakonfigurováno** (výchozí): umožňuje zařízení přijímat aktualizace softwaru bez připojení k počítači.
- Dříve toto nastavení umožňuje nakonfigurovat ho jako: **Povolit**, které umožní uživatelům přijímat aktualizace softwaru bez připojení zařízení k počítači.
**Povolí příslušenství USB, když je zařízení zamknuté**: **umožňuje dovolit** , aby data Exchange příslušenství využívala zařízení, které je po celou hodinu uzamčené. **Nenakonfigurováno** (výchozí) neaktualizuje režim omezeného portu USB na zařízení a příslušenství USB bude zablokováno v přenosu dat ze zařízení, pokud je po celou hodinu uzamčené.
- Dříve toto nastavení umožňuje nakonfigurovat ho jako **blok** pro zakázání režimu omezeného na zařízení USB na zařízeních pod dohledem.

Další informace o nastavení, které můžete nakonfigurovat, najdete v tématu [nastavení zařízení s iOS a iPadOS, které umožňuje povolit nebo zakázat funkce využívající Intune](../configuration/device-restrictions-ios.md).

Tato funkce platí pro:

- Operační systém/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Profily konfigurace síťových zařízení s drátovou sítí pro zařízení macOS<!-- 3508686  -->
   > [!NOTE]
   > Tato funkce byla zpožděna, ale brzy bude vydána.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Zablokovat uživatelům nastavení přihlašovacích údajů certifikátu ve spravovaném úložišti klíčů na zařízeních s Androidem Enterprise Device Owner<!-- 3311998 -->
Na zařízeních pro vlastníka zařízení s Androidem Enterprise můžete nakonfigurovat nové nastavení, které uživatelům zablokuje konfiguraci svých přihlašovacích údajů k certifikátu ve spravovaném úložišti klíčů (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for Platform > **Owner pouze > omezení zařízení** pro typ profilu > **Uživatelé a účty**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="protected-wipe-action-now-available--51150000---"></a>Nyní je k dispozici chráněná akce vymazání.<!--51150000 -->
Teď máte možnost použít akci vymazat zařízení k provedení chráněného vymazání zařízení. Chráněná vymazání jsou stejná jako standardní vymazání, s tím rozdílem, že je nelze obejít vypnutím zařízení. Chráněné vymazání bude pokračovat v pokusu o resetování zařízení, dokud nebylo úspěšné. V některých konfiguracích může tato akce opustit zařízení, protože se nemůže restartovat. Další informace najdete v tématu [vyřazení nebo vymazání zařízení](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Adresa MAC zařízení pro síť Ethernet přidaná na stránku Přehled zařízení<!--5562275 -->
Na stránce s podrobnostmi o zařízení se teď může zobrazit ethernetová adresa MAC zařízení (**zařízení** > **všechna zařízení** > zvolit **Přehled**> zařízení.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Vylepšené prostředí na sdíleném zařízení, když jsou povolené zásady podmíněného přístupu na základě zařízení<!-- 1734096  -->
Vylepšili jsme prostředí na sdíleném zařízení s více uživateli, kteří jsou cílem zásad podmíněného přístupu na základě zařízení, a to kontrolou nejnovějšího vyhodnocení dodržování předpisů pro uživatele při vynucování zásad. Další informace najdete v následujících článcích přehledu:
- [Přehled Azure pro podmíněný přístup](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Přehled dodržování předpisů zařízením v Intune](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Použití profilů certifikátů PKCS ke zřízení zařízení s certifikáty<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
Profily certifikátů PKCS teď můžete používat k vystavování certifikátů na *zařízeních* s Androidem for Work, iOS/IPadOS a Windows, která jsou přidružená k profilům, jako jsou ta pro Wi-Fi a VPN. Dřív tyto tři platformy podporovaly jenom uživatelské certifikáty, přičemž podpora založená na zařízeních je omezená na macOS.

> [!NOTE]
> Profily certifikátů PKCS nejsou podporovány profily sítě Wi-Fi. Místo toho použijte profily certifikátů SCEP, když používáte [typ protokolu EAP](../configuration/wi-fi-settings-windows.md#enterprise-profile).

Pokud chcete použít certifikát založený na zařízení, při [vytváření profilu certifikátu PKCS](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) pro podporované platformy vyberte **Nastavení**. Teď uvidíte nastavení **typ certifikátu**, který podporuje možnosti pro zařízení nebo uživatele.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Centralizované protokoly auditu<!--5603185, 5697164 -->
Nové centralizované možnosti protokolu auditu teď shromažďují protokoly auditu pro všechny kategorie na jednu stránku. Protokoly můžete filtrovat a získat tak data, která hledáte. Protokoly auditu zobrazíte tak, že přejdete do části **Správa tenanta** > **protokoly auditu**. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Podrobnosti o značce oboru obsažené v podrobnostech o aktivitě protokolu auditu<!--5763534 -->
Podrobnosti o aktivitě protokolu auditu teď zahrnují informace o značce oboru (pro objekty Intune, které podporují značky oboru). Další informace o protokolech auditu najdete v tématu [použití protokolů auditu ke sledování a monitorování událostí](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Týden od 2. prosince 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Nové licencování pro spolupráci s Microsoft Endpoint Configuration Manager<!--5027281-->
Configuration Manager zákazníci se Software Assurance můžou získat spolusprávu Intune pro počítače s Windows 10, aniž by si museli kupovat další licenci Intune pro spolusprávu. Zákazníci už nepotřebují, abyste koncovým uživatelům přidělili jednotlivé licence Intune/EMS pro spolusprávu Windows 10.
- Zařízení spravovaná pomocí Configuration Manager a zaregistrovaná do spolusprávy mají skoro stejná práva jako samostatné počítače spravované MDM v Intune. Po obnovení se ale nedá znovu zřídit pomocí automatického pilotního nasazení.
- Zařízení s Windows 10 zaregistrovaná v Intune jiným způsobem vyžadují úplné licence Intune.
- Zařízení na jiných platformách stále vyžadují úplné licence Intune.

Další informace najdete v tématu [licenční podmínky](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Týden od 18. listopadu 2019 (1911 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Aktualizace uživatelského rozhraní při selektivním vymazání dat aplikace<!-- 4102028 -->
Uživatelské rozhraní pro selektivní vymazání dat aplikací v Intune se aktualizovalo. Změny uživatelského rozhraní zahrnují:
- Zjednodušené prostředí pomocí formátu na úrovni Průvodce zúženého v jednom podokně.
- Aktualizace toku vytváření, který má být zahrnut do přiřazení
- Souhrnná stránka všech věcí nastavená při zobrazení vlastností, před vytvořením nové zásady nebo úpravou vlastnosti. Také při úpravách vlastností se v souhrnu zobrazí pouze seznam položek z kategorie upravovaných vlastností.

Další informace najdete v tématu [Jak z aplikací spravovaných pomocí Intune vymazat jenom firemní data](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>Podpora klávesnice třetích stran pro iOS a iPadOS<!-- 4922950 -->
V březnu 2019 jsme oznámili odebrání podpory nastavení zásad ochrany aplikací pro iOS na klávesnicích třetích stran. Funkce se vrátí do Intune s podporou iOS i iPadOS. Pokud chcete toto nastavení povolit, přejděte na kartu **Ochrana dat** v nové nebo existující zásadě ochrany aplikací pro iOS/iPadOS a vyhledejte v části **přenos dat**nastavení **klávesnic třetích stran** .

Chování nastavení této zásady se mírně liší od předchozí implementace. V aplikacích s více identitami, které používají sadu SDK verze 12.0.16 a novější, na které cílí zásady ochrany aplikací s tímto nastavením nakonfigurovaným na **blokování**, koncoví uživatelé nebudou moci na svých organizacích a osobních účtech souhlasit s klávesnicí třetích stran. Aplikace používající sady SDK verze 12.0.12 a dřívější budou dál vykazovat chování dokumentované v nadpisu blogového příspěvku [známý problém: klávesnice třetích stran nejsou v iOS pro osobní účty blokované](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Cílové skupiny uživatelů macOS, které vyžadují správu Jamf<!-- 4061739  --> 
Můžete cílit na konkrétní skupiny uživatelů, kteří budou mít [zařízení MacOS spravovaná pomocí Jamf](../protect/conditional-access-integrate-jamf.md). Díky tomu můžete použít integraci Jamf dodržování předpisů pro podmnožinu zařízení macOS, zatímco jiná zařízení se spravují přes Intune. Pokud již používáte integraci Jamf, všichni uživatelé budou ve výchozím nastavení zaměřeni na integraci.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Nová nastavení Exchange ActiveSync při vytváření profilu konfigurace e-mailového zařízení na zařízeních s iOS<!-- 4892824   --> 
V zařízeních s iOS/iPadOS můžete nakonfigurovat připojení e-mailu v profilu konfigurace zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS/iPadOS** **pro > pro** daný typ profilu). 

K dispozici jsou nová nastavení Exchange ActiveSync, včetně:
- **Data pro synchronizaci se systémem Exchange**: vyberte služby Exchange, které chcete synchronizovat (nebo blokovat synchronizaci) pro kalendář, kontakty, připomenutí, poznámky a e-mail.
- **Umožňuje uživatelům změnit nastavení synchronizace**: povoluje (nebo zablokuje) uživatelům změnu nastavení synchronizace pro tyto služby na svých zařízeních.  

Další informace o těchto nastaveních najdete [v nastavení e-mailového profilu pro zařízení s iOS v Intune](../configuration/email-settings-ios.md). 

Platí pro:

- iOS 13,0 a novější
- iPadOS 13,0 a novější

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Zabránit uživatelům v přidávání osobních účtů Google na plně spravovaná a vyhrazená zařízení s Androidem Enterprise<!-- 5353228   -->
U plně spravovaných a vyhrazených zařízení s Androidem Enterprise je k dispozici nové nastavení, které uživatelům brání v vytváření osobních účtů Google (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** pro **vlastníka zařízení > jenom > omezení zařízení** pro typ profilu > **Uživatelé a účty nastavení** > **osobní účty Google**).

Pokud chcete zobrazit nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md).

Platí pro:

- Zařízení se systémem Android Enterprise s plnou správou
- Zařízení se systémem Android Enterprise vyhrazená

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>Nastavení příkazů protokolování na straně serveru pro příkazy Siri se odebralo v profilu omezení zařízení s iOS/iPadOS. <!-- 5468501   -->
V zařízeních se systémy iOS a iPadOS se nastavení **protokolování na straně serveru pro příkazy Siri** odebere z konzoly pro správu Microsoft Endpoint Manageru **(konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS/IPadOS** pro > **omezení zařízení** pro typ profilu > **integrované aplikace**). 

Toto nastavení nemá na zařízeních žádný vliv. Chcete-li odebrat nastavení z existujících profilů, otevřete profil, proveďte změnu a potom profil uložte. Profil se aktualizuje a nastavení se odstraní ze zařízení.

Pokud chcete zobrazit všechna nastavení, která můžete konfigurovat, přečtěte si téma [nastavení zařízení s iOS a iPadOS, abyste mohli povolit nebo zakázat funkce využívající Intune](../configuration/device-restrictions-ios.md).

Platí pro:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Aktualizace funkcí Windows 10 (verze Public Preview)<!-- 2384877 -->
Teď můžete nasadit [aktualizace funkcí Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) na zařízení s Windows 10. Aktualizace funkcí Windows 10 jsou novou zásadou aktualizace softwaru, která nastavuje verzi Windows 10, kterou chcete, aby se zařízení nainstalovala a zůstala v systému. Tento nový typ zásady můžete použít spolu s existujícími aktualizačními kanály Windows 10.

Zařízení, která přijímají zásady aktualizací funkcí Windows 10, budou instalovat určenou verzi Windows a pak zůstanou v této verzi, dokud se zásada neupraví nebo neodebere. Zařízení, na kterých běží novější verze Windows, zůstávají v aktuální verzi. Zařízení, která jsou držená v určité verzi Windows, můžou pořád instalovat aktualizace kvality a zabezpečení pro tuto verzi z aktualizačních kanálů Windows 10.

Tento nový typ zásad začíná v tomto týdnu pro klienty. Pokud tato zásada ještě není pro vašeho tenanta k dispozici, bude brzy.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Přidání a změna klíčových informací v souborech plist pro aplikace macOS<!-- 4736278 -->
Na zařízeních macOS teď můžete vytvořit konfigurační profil zařízení, který nahraje soubor seznamu vlastností (. plist) přidružený k aplikaci nebo zařízení (**zařízení** > **Konfigurace profily** > **vytvořit profil** > pro **soubor předvoleb** **> pro typ** profilu).

Pouze některé aplikace podporují spravované předvolby a tyto aplikace vám nemusí umožňovat spravovat všechna nastavení. Nezapomeňte nahrát soubor seznamu vlastností, který nakonfiguruje nastavení kanálu zařízení, ne nastavení kanálu uživatele.

Další informace o této funkci najdete v tématu [Přidání souboru se seznamem vlastností do zařízení MacOS pomocí Microsoft Intune](../configuration/preference-file-settings-macos.md).

Platí pro:

- zařízení macOS se systémem 10,7 a novějším

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Upravit hodnotu názvu zařízení pro zařízení s autopilotem<!-- 2640074 -->
Můžete upravit hodnotu název zařízení pro zařízení autopilotu připojená k Azure AD.  Další informace najdete v tématu [Úprava atributů zařízení autopilotu](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Upravit hodnotu značky skupiny pro zařízení autopilotu<!-- 4816775   -->
Můžete upravit hodnotu značky skupiny pro zařízení autopilotu. Další informace najdete v tématu [Úprava atributů zařízení autopilotu](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="updated-support-experience---5012398---"></a>Aktualizované prostředí podpory<!-- 5012398 -->

Od dnešního dne se aktualizované a zjednodušené prostředí v konzole pro [Získání pomoci a podpory pro Intune](get-support.md) zavádět do klientů. Pokud toto nové prostředí zatím není k dispozici, bude brzy.

Vylepšili jsme vyhledávání v konzole a zpětnou vazbu pro běžné problémy a pracovní postup, pomocí kterého se obrátíte na podporu. Při otevírání problému podpory uvidíte odhady v reálném čase, kdy můžete očekávat zpětné volání nebo e-mailovou odpověď, a zákazníci s plánem Premier a Unified support můžou pro svůj problém snadno zadat závažnost, abyste mohli rychleji získat podporu.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Vylepšené prostředí Intune pro vytváření sestav (Public Preview) <!-- 3791418 -->
Intune teď nabízí vylepšené možnosti vytváření sestav, včetně nových typů sestav, lepších organizací sestav, pokročilejších zobrazení, vylepšených funkcí sestav a také konzistentních a včasných dat. Nové typy sestav se zaměřují na následující:

- **Provozní** – poskytuje nové záznamy s negativním důrazem na stav. 
- **Organizace** – poskytuje širší souhrn celkového stavu.
- **Historická** – poskytuje vzory a trendy v časovém intervalu.
- **Specialista** – umožňuje používat nezpracovaná data k vytváření vlastních sestav.

První sada nových sestav se zaměřuje na dodržování předpisů zařízením. Další informace najdete v tématu [Microsoft Intune pro vytváření sestav](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) a [sestavy Intune](reports.md)v rámci blogů.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Duplicitní vlastní nebo předdefinované role <!-- 1081938   -->
Nyní můžete kopírovat předdefinované a vlastní role. Další informace najdete v tématu [kopírování role](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Nová oprávnění pro roli školního správce <!-- 5621805  -->  
Do role správce školy byly přidány dvě nová oprávnění, **přiřadí se profil** a **synchronizovat zařízení**> **oprávnění** > **registračních programů**. Oprávnění profil synchronizace umožňuje správcům skupin synchronizovat zařízení s Windows autopilotem. Oprávnění přiřadit profil umožňuje odstranit uživatelem inicializované profily registrace Apple. Poskytuje jim taky oprávnění ke správě přiřazení zařízení s autopilotem a přiřazení profilu nasazení autopilotu. Seznam všech oprávnění správce školy nebo skupiny správců najdete v tématu [přiřazení správců skupin](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Zabezpečení

#### <a name="bitlocker-key-rotation---2564951----"></a>Střídání klíčů BitLockeru<!-- 2564951  -->
K vzdálenému [otočení klíčů pro obnovení BitLockeru](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) pro spravovaná zařízení s Windows verze 1909 nebo novější můžete použít akci zařízení v Intune. Aby bylo možné získat oprávnění k otočení klíčů pro obnovení, musí být zařízení nakonfigurovaná tak, aby podporovala otočení obnovovacího klíče.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Aktualizace vyhrazené registrace zařízení pro podporu nasazení certifikátu zařízení SCEP <!-- 5198878  -->
Intune teď podporuje nasazení certifikátu zařízení SCEP na vyhrazená zařízení s Androidem Enterprise pro přístup založený na certifikátech k profilům Wi-Fi. Aby mohlo nasazení fungovat, musí být aplikace Microsoft Intune na zařízení přítomná. V důsledku toho jsme aktualizovali možnosti registrace pro vyhrazená zařízení s Androidem Enterprise. Nové registrace stále začínají stejnou (s identifikátorem QR, NFC, nulovým dotykem nebo identifikátorem zařízení), ale teď mají krok, který vyžaduje, aby uživatelé nainstalovali aplikaci Intune. Stávající zařízení začnou aplikaci automaticky instalovat na určitou bázi.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Protokoly auditu Intune pro spolupráci mezi společnostmi<!--5670211 -->
Spolupráce B2B (Business-to-Business) umožňuje bezpečně sdílet aplikace a služby společnosti s uživateli typu host z jakékoli jiné organizace a přitom zachovat kontrolu nad vašimi podnikovými daty. Intune teď podporuje protokoly auditu pro uživatele typu Host B2B. Například když uživatelé typu Host provedou změny, Intune bude moct zachytit tato data prostřednictvím protokolů auditu. Další informace najdete v tématu [co je přístup uživatelů typu Host v Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b) .

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Týden od 11. listopadu 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Vylepšené možnosti registrace macOS v Portál společnosti <!-- 5074349  -->  
Portál společnosti pro zápis do macOS má jednodušší proces registrace, který se podrobněji zarovnává s Portál společnostim pro možnosti registrace v iOS. Uživatelé zařízení teď uvidí:  

- Elegantní uživatelské rozhraní.  
- Vylepšený kontrolní seznam pro registraci.  
- Informace o tom, jak zaregistrovat svá zařízení.  
- Vylepšené možnosti řešení potíží.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Webové aplikace spouštěné z aplikace Portál společnosti pro Windows<!-- 5030972 -->
Koncoví uživatelé teď můžou spouštět webové aplikace přímo z aplikace Portál společnosti pro Windows. Koncoví uživatelé můžou webovou aplikaci vybrat a pak vybrat možnost **otevřít v prohlížeči**. Publikovaná webová adresa URL se otevře přímo ve webovém prohlížeči. Tato funkce bude zahrnuta v průběhu příštího týdne. Další informace o webových aplikacích najdete v tématu [Přidání webových aplikací do Microsoft Intune](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Sloupec nový typ přiřazení v Portál společnosti pro Windows 10 <!-- 5459950  -->
Sloupec **typu přiřazení** portál společnosti > **nainstalované aplikace** > byl přejmenován na **požadováno vaší organizací**.  V tomto sloupci se uživatelům zobrazí hodnota **Ano** nebo **ne** , která označuje, že je aplikace buď požadovaná, nebo povinná jejich organizací. Tyto změny byly provedeny, protože uživatelé zařízení byli zaměňováni o konceptu dostupných aplikací. Uživatelé můžou najít další informace o instalaci aplikací z Portál společnosti v [instalaci a sdílení aplikací na vašem zařízení](../user-help/install-apps-cpapp-windows.md). Další informace o konfiguraci aplikace Portál společnosti pro uživatele naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Týden od 4. listopadu 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Základní hodnoty zabezpečení jsou podporovány v Microsoft Azure Government<!-- 4062552 -->

Instance Intune, které jsou hostované na *Microsoft Azure Government* , teď můžou používat [směrné plány zabezpečení](../protect/security-baselines.md) , které vám pomůžou zabezpečit a chránit vaše uživatele a zařízení.

## <a name="whats-new-archive"></a>Archiv co je nového
V předchozích měsících se podívejte do [archivu co je nového](whats-new-archive.md).

## <a name="notices"></a>Oznámení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


