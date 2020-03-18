---
title: Novinky v Microsoft Intune – Azure za předchozí měsíce | Microsoft Docs
titleSuffix: ''
description: Zkontrolujte starší oznámení ze stránky novinek Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/28/2020
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 9ba01d60-4a03-4e3e-9aba-8be905c0054c
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17fa979f9563eb0735a68d2cc0ed82d800f8816f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330139"
---
# <a name="whats-new-in-the-microsoft-intune---previous-months"></a>Novinky v Microsoft Intune – předchozí měsíce

[!INCLUDE [azure_portal](../includes/azure_portal.md)]


<!-- ########################## -->
## <a name="october-2019"></a>Říjen 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="improved-checklist-design-in-company-portal-app-for-android---5550857---"></a>Vylepšený návrh kontrolního seznamu v aplikaci Portál společnosti App pro Android<!-- 5550857 -->  
Kontrolní seznam nastavení v aplikaci Portál společnosti pro Android byl aktualizovaný s odlehčeným návrhem a novými ikonami. Změny se zarovnají s posledními aktualizacemi provedenými v aplikaci Portál společnosti pro iOS. Pro souběžné porovnání změn si přečtěte téma [co je nového v uživatelském rozhraní aplikace](whats-new-app-ui.md). Pokud se chcete podívat na aktualizované kroky registrace, přečtěte si téma [registrace v pracovním profilu Android](../user-help/enroll-device-android-work-profile.md) a [registrace zařízení s Androidem](../user-help/enroll-device-android-company-portal.md).  

#### <a name="win32-apps-on-windows-10-s-mode-devices---3747604---"></a>Aplikace Win32 na zařízeních S Windows 10 S v režimu<!-- 3747604 --> 
Aplikace Win32 můžete instalovat a spouštět na zařízeních spravovaných v režimu Windows 10 S. K tomu můžete vytvořit jednu nebo více doplňkových zásad pro režim S pomocí nástrojů PowerShellu pro řízení aplikací v programu Windows Defender (WDAC). Přihlaste doplňkové zásady pomocí registračního portálu pro ochranu zařízení a pak tyto zásady nahrajte a distribuujte prostřednictvím Intune. V Intune tuto možnost najdete tak, že vyberete **klientské aplikace** > **doplňkové zásady Windows 10 S**. Další informace najdete v tématu [Povolení aplikací Win32 na zařízeních s režimem S](../apps/apps-win32-s-mode.md).

#### <a name="set-win32-app-availability-based-on-a-date-and-time---3510685---"></a>Nastavení dostupnosti aplikace Win32 na základě data a času<!-- 3510685 -->
Jako správce můžete nakonfigurovat čas zahájení a konečný termín pro požadovanou aplikaci Win32. V počátečním čase rozšíření pro správu Intune spustí stažení obsahu aplikace a uloží je do mezipaměti. Aplikace se nainstaluje v čase konečného termínu. V případě dostupných aplikací se čas spuštění určí, když se aplikace zobrazí v Portál společnosti. Další informace najdete v tématu [Správa aplikací Win32 v Intune](../apps/apps-win32-app-management.md#set-win32-app-availability-and-notifications).

#### <a name="require-device-restart-based-on-grace-period-after-win32-app-install---3136567---"></a>Vyžadovat restart zařízení na základě období odkladu po instalaci aplikace Win32<!-- 3136567 -->
Můžete vyžadovat, aby se zařízení po úspěšném dokončení instalace aplikace Win32 restartovalo. Další informace najdete v tématu [Správa aplikací Win32](../apps/apps-win32-app-management.md).

#### <a name="dark-mode-for-ios-company-portal---4911422---"></a>Tmavý režim pro iOS Portál společnosti<!-- 4911422 -->
Pro iOS Portál společnosti je k dispozici tmavý režim. Uživatelé můžou stahovat firemní aplikace, spravovat jejich zařízení a získávat v nich podporu v barevném schématu podle nastavení zařízení. Portál společnosti pro iOS bude automaticky odpovídat nastavení zařízení koncového uživatele pro tmavý nebo lehký režim. Další informace najdete v tématu [představení tmavého režimu Microsoft Intune portál společnosti pro iOS](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Introducing-dark-mode-on-Microsoft-Intune-Company-Portal-for-iOS/ba-p/918453). Další informace o Portál společnosti pro iOS najdete v tématu [Jak konfigurovat aplikaci Microsoft Intune portál společnosti](../apps/company-portal-app.md).

#### <a name="android-company-portal-enforced-minimum-app-version---2378776---"></a>Minimální verze aplikace pro Android Portál společnosti vynutila<!-- 2378776 -->
Pomocí nastavení **Minimální verze portál společnosti** zásady ochrany aplikací můžete zadat konkrétní minimální verzi portál společnosti, která se vynutila na zařízení koncového uživatele. Toto nastavení podmíněného spuštění umožňuje **blokovat přístup**, **Vymazat data**nebo **upozorňovat** jako na možné akce, pokud není hodnota splněna. Možné formáty pro tuto hodnotu se řídí vzorem *[hlavní]. [ Vedlejší]* , *[hlavní]. [ Vedlejší]. [Build]* nebo *[hlavní]. [ Vedlejší]. [Build]. [Revize]* .

Nastavení **Minimální verze portál společnosti** , pokud je nakonfigurováno, bude mít vliv na každého koncového uživatele, který získá 5.0.4560.0 verze portál společnosti a jakékoli budoucí verze portál společnosti. Toto nastavení nebude mít žádný vliv na uživatele, kteří používají verzi Portál společnosti, která je starší než verze, ve které byla tato funkce vydána. Koncoví uživatelé, kteří používají automatické aktualizace aplikace na jejich zařízení, nejspíš neuvidí žádná dialogová okna této funkce, protože budou pravděpodobně na nejnovější verzi Portál společnosti. Toto nastavení platí jenom pro Android s ochranou aplikací pro zapsaná a neregistrovaná zařízení. Další informace najdete v tématu [nastavení zásad ochrany aplikací pro Android – podmíněné spuštění](../apps/app-protection-policy-settings-android.md#conditional-launch).

#### <a name="add-mobile-threat-defense-apps-to-unenrolled-devices---3005337---"></a>Přidání aplikací ochrany před mobilními hrozbami do neregistrovaných zařízení<!-- 3005337 -->
Můžete vytvořit zásady ochrany aplikací Intune, které můžou blokovat nebo selektivně vymazat podniková data uživatelů na základě stavu zařízení. Stav zařízení se určí pomocí vašeho zvoleného řešení ochrany před mobilními hrozbami (MTD). Tato funkce existuje v současnosti se zaregistrovanými zařízeními Intune jako nastavením dodržování předpisů pro zařízení. Díky této nové funkci rozšiřujeme detekci hrozeb od dodavatele ochrany před mobilními hrozbami, aby fungovalo na nezaregistrovaných zařízeních. V Androidu Tato funkce vyžaduje nejnovější Portál společnosti na zařízení. V systému iOS bude tato funkce dostupná pro použití v případě, že aplikace integrují nejnovější sadu Intune SDK (v 12.0.15 +). V případě, že první aplikace přijme nejnovější sadu Intune SDK, aktualizujeme téma Co je nového. Zbývající aplikace budou k dispozici na určitou bázi. Další informace najdete v tématu [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami v Intune](../protect/mtd-app-protection-policy.md).

#### <a name="available-google-play-app-reporting-for-android-work-profiles---3041956-----"></a>Dostupná Google Play vytváření sestav aplikací pro pracovní profily Androidu<!-- 3041956   -->
Pro instalaci dostupné aplikace na firemním profilu Androidu Enterprise, vyhrazená a plně spravovaná zařízení můžete zobrazit stav instalace aplikace a také nainstalovanou verzi spravovaných aplikací Google Play. Další informace najdete v tématu [monitorování zásad ochrany aplikací](../apps/app-protection-policies-monitor.md), [Správa zařízení s pracovním profilem Androidu pomocí Intune](../enrollment/android-enterprise-overview.md) a [spravovaného Google Play typu aplikace](../apps/apps-add-android-for-work.md#managed-google-play-app-types).

#### <a name="microsoft-edge-version-77-and-later-for-windows-10-and-macos-public-preview---3872025-4678761----"></a>Microsoft Edge verze 77 a novější pro Windows 10 a macOS (Public Preview)<!-- 3872025, 4678761  -->
Microsoft Edge verze 77 a novější bude k dispozici pro nasazení na počítačích se systémy Windows 10 a macOS.

Verze Public Preview nabízí **vývoj** a **beta** kanály pro Windows 10 a **beta** kanál pro MacOS. Nasazení je pouze anglické (EN), ale koncoví uživatelé mohou změnit jazyk zobrazení v prohlížeči v části **nastavení** > **jazyky**. Microsoft Edge je aplikace Win32 nainstalovaná v kontextu systému a jako architektury (aplikace x86 v operačním systému x86 a x64 v operačním systému x64). Automatické aktualizace prohlížeče jsou navíc ve výchozím nastavení **zapnuté** a Microsoft Edge nejde odinstalovat. Další informace najdete v tématu [Přidání Microsoft Edge pro Windows 10 do Microsoft Intune](../apps/apps-windows-edge.md) a [dokumentace k Microsoft Edge](https://go.microsoft.com/fwlink/?linkid=2103823).

#### <a name="update-to-app-protection-ui-and-ios-app-provisioning-ui---4102027-4102029-----"></a>Aktualizace uživatelského rozhraní ochrany aplikací a uživatelského rozhraní pro zřizování aplikací pro iOS<!-- 4102027, 4102029   -->
Aktualizovali jsme uživatelské rozhraní pro vytváření a úpravu zásad ochrany aplikací a zřizovacích profilů aplikací pro iOS v Intune. Změny uživatelského rozhraní zahrnují:
- Zjednodušené prostředí pomocí formátu na úrovni Průvodce zúženého v jednom okně.
- Aktualizace toku vytváření, který má být zahrnut do přiřazení
- Souhrnná stránka všech věcí nastavená při zobrazení vlastností, před vytvořením nové zásady nebo úpravou vlastnosti. Také při úpravách vlastností se v souhrnu zobrazí pouze seznam položek z kategorie upravovaných vlastností.

Další informace najdete v tématech [Vytvoření a přiřazení zásad ochrany aplikací](../apps/app-protection-policies.md) a [používání zřizovacích profilů aplikací pro iOS](../apps/app-provisioning-profile-ios.md).

#### <a name="intune-guided-scenarios---4850318-4831296-3610611----"></a>Scénáře s asistencí pro Intune<!-- 4850318, 4831296, 3610611  -->
Intune teď poskytuje scénáře s asistencí, které vám pomůžou dokončit konkrétní úkol nebo sadu úkolů v rámci Intune. Scénář s asistencí je přizpůsobený sled kroků (pracovní postup), který se nachází na středovém prostředí pro případ celého použití. Běžné scénáře jsou definovány na základě role, kterou správce, uživatel nebo zařízení přehrává ve vaší organizaci. Tyto pracovní postupy obvykle vyžadují kolekci pečlivě Orchestrované profily, nastavení, aplikace a řízení zabezpečení, které poskytují nejlepší uživatelské prostředí a zabezpečení. Mezi nové scénáře s asistencí patří:
- [Nasazení Microsoft Edge pro mobilní zařízení](guided-scenarios-edge.md)
- [Zabezpečené systém Microsoft Office mobilní aplikace](guided-scenarios-office-mobile.md)
- [Moderní plocha spravovaná cloudem](guided-scenarios-cloud-managed-pc.md)

Další informace najdete v článku [Přehled scénářů s asistencí pro Intune](guided-scenarios-overview.md).

#### <a name="additional-app-configuration-variable-available---4969237-----"></a>Je dostupná další konfigurační proměnná aplikace.<!-- 4969237   -->
Při vytváření zásad konfigurace aplikací můžete zahrnout proměnnou konfigurace `AAD Device ID` jako součást nastavení konfigurace. V Intune vyberte **klientské aplikace** > **zásady konfigurace aplikací** > **Přidat**. Zadejte podrobnosti zásady konfigurace a vyberte **nastavení konfigurace** . zobrazí se okno **nastavení konfigurace** . Další informace najdete v tématu [zásady konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise – použijte návrháře konfigurace](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

#### <a name="create-groups-of-management-objects-called-policy-sets---3762880----"></a>Vytvoření skupin objektů pro správu nazývaných sady zásad<!-- 3762880  -->
Sady zásad umožňují vytvořit sadu odkazů na již existující entity správy, které je třeba identifikovat, cílit a monitorovat jako jednu koncepční jednotku. Sady zásad nenahrazují existující koncepty ani objekty. V Intune můžete dál přiřazovat jednotlivé objekty a v rámci sady zásad můžete odkazovat na jednotlivé objekty. Proto se v sadě zásad projeví všechny změny těchto jednotlivých objektů.  V Intune vyberete **sady zásad** > **vytvořit** k vytvoření nové sady zásad.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení
tokenu prostředku
#### <a name="new-device-firmware-configuration-interface-profile-for-windows-10-and-later-devices-public-preview---2266073----"></a>Nový profil rozhraní pro konfiguraci firmwaru zařízení pro zařízení s Windows 10 a novější verzí (Public Preview)<!-- 2266073  -->
V systému Windows 10 a novějších můžete vytvořit profil konfigurace zařízení pro řízení nastavení a funkcí (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** pro platformu). V této aktualizaci je k dispozici nový typ profilu rozhraní konfigurace firmwaru zařízení, který umožňuje Intune spravovat nastavení rozhraní UEFI (BIOS).

Další informace o této funkci najdete v tématu [použití profilů DFCI na zařízeních s Windows v Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md).

Platí pro:

- Windows 10 RS5 (1809) a novější v podporovaném firmwaru

#### <a name="ui-update-for-creating-and-editing-windows-10-update-rings---4099089-----------"></a>Aktualizace uživatelského rozhraní pro vytváření a úpravy aktualizačních kanálů Windows 10<!-- 4099089         -->
Aktualizovali jsme uživatelské rozhraní ex'erience pro [vytváření a úpravy aktualizačních kanálů Windows 10](../protect/windows-update-for-business-configure.md#create-and-assign-update-rings) pro Intune. Změny uživatelského rozhraní zahrnují:  
- Formát na úrovni průvodce je zúžený do jediného okna konzoly, ve kterém se při konfiguraci aktualizačních kanálů zobrazí okno neustálému zvětšování, které jste předtím viděli.   
- Revidovaný pracovní postup obsahuje přiřazení před dokončením počáteční konfigurace prstence.
- Souhrnná stránka, kterou můžete použít ke kontrole všech konfigurací, které jste provedli, před uložením a nasazením nového aktualizačního kanálu. Při úpravách aktualizačního kanálu zobrazuje souhrn pouze seznam položek nastavených v kategorii vlastností, které jste upravili.

#### <a name="ui-update-for-creating-and-editing-ios-software-update-policy---4099090---------"></a>Aktualizace uživatelského rozhraní pro vytváření a úpravy zásad aktualizace softwaru pro iOS<!-- 4099090       --> 
Aktualizovali jsme prostředí uživatelského rozhraní pro [vytváření](../protect/software-updates-ios.md#configure-the-policy) a [úpravu](../protect/software-updates-ios.md#edit-a-policy) zásad aktualizace softwaru iOS pro Intune.  Změny uživatelského rozhraní zahrnují:  
- Formát na úrovni průvodce je zhuštěný do jediného okna konzoly, ve kterém se při konfiguraci zásad aktualizace nezobrazuje okno neustálému zvětšování.   
- Revidovaný pracovní postup zahrnuje přiřazení před dokončením počáteční konfigurace zásady.
- Souhrnná stránka, kterou můžete použít ke kontrole všech konfigurací, které jste provedli, před uložením a nasazením nové zásady. V rámci úpravy zásady se v souhrnu zobrazí jenom seznam položek nastavených v kategorii vlastností, které jste upravili.

#### <a name="engaged-restart-settings-are-removed-from-windows-update-rings----4464404--------"></a>Nastavení připraveného restartování se z web Windows Updatech okruhů odeberou.<!--  4464404      -->
Jak už bylo oznámeno, aktualizační kanály Windows 10 v Intune teď [podporují nastavení pro konečné termíny](../protect/windows-update-settings.md) a už nepodporují *restart*. Nastavení pro probíhající *restart* již není k dispozici při konfiguraci nebo správě aktualizačních kroužků v Intune.  

Tato změna se zarovnává s posledními [změnami údržby Windows](https://docs.microsoft.com//windows/whats-new/whats-new-windows-10-version-1903#servicing) a na zařízeních s Windows 10 1903 nebo novějším, přičemž *termíny* nahrazují konfigurace pro *následné restartování*.

#### <a name="prevent-installation-of-apps-from-unknown-sources-on-android-enterprise-work-profile-devices---4760025-----"></a>Zabránit instalaci aplikací z neznámých zdrojů na zařízeních s pracovními profily Android Enterprise<!-- 4760025   -->
Na zařízeních s pracovním profilem Android Enterprise uživatelé nemůžou instalovat aplikace aplikací z neznámých zdrojů. V této aktualizaci se nachází nové nastavení – **Zakázat instalaci aplikací z neznámých zdrojů v osobním profilu**. Ve výchozím nastavení toto nastavení brání uživatelům v nasazování aplikací z neznámých zdrojů do osobního profilu na zařízení.

Pokud chcete zobrazit nastavení, které můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md).

Platí pro:

- Pracovní profil Android Enterprise

#### <a name="create-a-global-http-proxy-on-android-enterprise-device-owner-devices---4816339-----"></a>Vytvoření globálního proxy serveru HTTP na zařízeních s vlastníkem zařízení s Androidem Enterprise<!-- 4816339   -->
Na zařízeních s Androidem Enterprise můžete nakonfigurovat globální proxy server HTTP tak, aby odpovídal standardům procházení webu vaší organizace (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for Platform > **>** pro typ profilu > **konektivita**zařízení. Po nakonfigurování budou všechny přenosy HTTP používat tento proxy server.

Pokud chcete tuto funkci nakonfigurovat a zobrazit všechna nakonfigurovaná nastavení, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md).

Platí pro:

- Vlastník zařízení se systémem Android Enterprise

#### <a name="connect-automatically-setting-is-removed-in-wi-fi-profiles-on-android-device-administrator-and-android-enterprise---5021055-----"></a>Nastavení připojit automaticky se odebere v profilech sítě Wi-Fi na správce zařízení s Androidem a na Androidu Enterprise.<!-- 5021055   -->
Na zařízeních s Androidem pro správce zařízení a Androidem je možné vytvořit profil Wi-Fi pro konfiguraci různých nastavení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Správce zařízení s androidem** nebo **Android Enterprise** pro platformu > **Wi-Fi** pro typ profilu). V této aktualizaci se nastavení **Připojit automaticky** odebere, protože ho [nepodporuje Android](https://developer.android.com/reference/android/net/wifi/WifiManager.html#enableNetwork%28int%2c%20boolean%29). 

Pokud použijete toto nastavení v profilu Wi-Fi, možná jste si všimli, že se **připojení automaticky** nepracuje. Nemusíte nic dělat, ale mějte na paměti, že toto nastavení se odebere v uživatelském rozhraní Intune.

Pokud chcete zobrazit aktuální nastavení, přejděte na nastavení [Androidu Wi-Fi](../configuration/wi-fi-settings-android.md) nebo [Nastavení Android Enterprise Wi-Fi](../configuration/wi-fi-settings-android-enterprise.md).

Platí pro:

- Správce zařízení s Androidem 
- Android Enterprise


#### <a name="new-device-configuration-settings-for-supervised-ios-and-ipados-devices---5199328-----"></a>Nové nastavení konfigurace zařízení pro zařízení s iOS a iPadOS pod dohledem<!-- 5199328   -->
Na zařízeních se systémy iOS a iPadOS můžete vytvořit profil, který omezí funkce a nastavení na zařízeních (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS/iPadOS** pro **omezení** platformy > pro typ profilu). V této aktualizaci můžete řídit nová nastavení: 
- Přístup k síťové jednotce v aplikaci soubory  
- Přístup k jednotce USB v aplikaci soubory 
- Wi-Fi vždycky zapnuté 

Tato nastavení zobrazíte tak, že přejdete na [nastavení zařízení s iOS a povolíte nebo zakážete funkce využívající Intune](../configuration/device-restrictions-ios.md).

Platí pro:

- iOS 13,0 a novější
- iPadOS 13,0 a novější

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="toggle-to-only-show-enrollment-status-page-on-devices-provisioned-by-out-of-box-experience-oobe--3959566--"></a>Přepnout na zobrazení stránky stav registrace na zařízeních, která se zřídila při spuštění předpřipraveného prostředí (OOBE)<!--3959566-->
Nyní se můžete rozhodnout, že se stránka stavu registrace zobrazí jenom na zařízeních zřízených pomocí příkazu autopilot OOBE.

Pokud se chcete podívat na nový přepínač, vyberte > **Intune** **registrace zařízení** > **registrace Windows** > **stavová stránka** > **vytvořit profil** > **Nastavení** > **zobrazit jenom stránku na zařízeních, která se zřídila při prvním zapnutí prostředí (OOBE)** .

#### <a name="specify-which-android-device-operating-system-versions-enroll-with-work-profile-or-device-administrator-enrollment---4350697-----"></a>Zadejte, které verze operačního systému zařízení s Androidem se mají zaregistrovat pomocí pracovního profilu nebo registrace Správce zařízení.<!-- 4350697   -->
Pomocí omezení typu zařízení v Intune můžete použít verzi operačního systému zařízení k určení toho, která zařízení uživatelů budou používat registraci pracovního profilu Android Enterprise nebo Správce zařízení s Androidem.  Další informace najdete v tématu [Nastavení omezení registrace](../enrollment/enrollment-restrictions-set.md).



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="intune-supports-ios-11-and-later---4665324----"></a>Intune podporuje iOS 11 a novější.<!-- 4665324  -->
Registrace a Portál společnosti v Intune teď podporují iOS verze 11 a novější. Starší verze se nepodporují.

#### <a name="new-restrictions-for-renaming-windows-devices---3478938----"></a>Nová omezení pro přejmenování zařízení s Windows<!-- 3478938  -->
Při přejmenování zařízení s Windows musíte dodržovat nová pravidla:
- maximálně 15 znaků (musí být menší než nebo rovno 63 bajtů, včetně koncové hodnoty NULL)
- Není null nebo prázdný řetězec
- Povolené znakové sady ASCII: písmena (a-z, A – Z), číslice (0-9) a spojovníky
- Povolené kódování Unicode: znaky > = 0x80, musí být platný UTF8, musí být možné mapovat na IDN (to znamená, že RtlIdnToNameprepUnicode je úspěšných, viz RFC 3492)
- Názvy nesmí obsahovat jenom číslice.
- Žádné mezery v názvu
- Nepovolené znaky: {|} ~ [\] ^ ':; < = >? & @! " # $ % ` ( ) + / , . _ *)

 Další informace najdete v tématu [přejmenování zařízení v Intune](../remote-actions/device-rename.md).

### <a name="new-android-report-on-devices-overview-page---4924364---"></a>Stránka Přehled nové sestavy pro Android na zařízeních<!-- 4924364 -->
Nová sestava na stránce Přehled zařízení zobrazuje počet zaregistrovaných zařízení s Androidem v jednotlivých řešeních pro správu zařízení. Tento graf zobrazuje počet zaregistrovaných zařízení v pracovním profilu, plně spravovaných, vyhrazených a správcích zařízení. Pokud chcete zobrazit sestavu, vyberte > **zařízení** **Intune** > **Přehled**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="microsoft-edge-baseline-preview----3787164----"></a>Microsoft Edge – základní údaje (Preview)<!--  3787164  -->
Přidali jsme náhled základní úrovně zabezpečení pro [nastavení Microsoft Edge](../protect/security-baseline-settings-edge.md). 

#### <a name="pkcs-certificates-for-macos---1333650---------"></a>Certifikáty PKCS pro macOS<!-- 1333650       -->
[Certifikáty PKCS teď můžete používat s MacOS](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile). Můžete vybrat certifikát PKCS jako typ profilu pro macOS a nasadit certifikáty uživatelů a zařízení, které mají [přizpůsobená pole Předmět a alternativní název subjektu](../protect/certficates-pfx-configure.md#subject-name-format).  

Certifikát PKCS pro macOS podporuje také nové nastavení a _povoluje přístup všem aplikacím_. Pomocí tohoto nastavení můžete všem přidruženým aplikacím povolit přístup k privátnímu klíči certifikátu.  Další informace o tomto nastavení najdete v dokumentaci Apple na adrese https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf.

####   <a name="derived-credentials-to-provision-ios-mobile-devices-with-certificates----1736036-1736037-1772050-2777333-----------"></a>Odvozená pověření pro zřizování mobilních zařízení s iOS pomocí certifikátů<!--  1736036, 1736037, 1772050, 2777333         -->  
Intune podporuje použití [odvozených přihlašovacích údajů](../protect/derived-credentials.md) jako metody ověřování a pro podepisování a šifrování S/MIME pro zařízení S iOS. Odvozené přihlašovací údaje jsou implementací standardu *NIST (National Institute of Standards and Technology) 800-157* pro nasazení certifikátů do zařízení.  

Odvozené přihlašovací údaje spoléhají na použití osobního ověřování identity (PIV) nebo karty Common Access Card (CAC), jako je například čipová karta. Pokud chcete získat odvozené přihlašovací údaje pro své mobilní zařízení, uživatelé začnou v aplikaci Portál společnosti a dodržujte pracovní postup registrace, který je jedinečný pro poskytovatele, kterého používáte.  Společný pro všechny poskytovatele je požadavek na použití čipové karty v počítači k ověření pro odvozeného zprostředkovatele přihlašovacích údajů. Poskytovatel pak vydá certifikát zařízení, které je odvozeno od čipové karty uživatele.  

Intune podporuje následující odvozené zprostředkovatele přihlašovacích údajů:
- DISA purebred
- Entrust Datacard
- Intercede

Odvozené přihlašovací údaje použijete jako metodu ověřování pro profily konfigurace zařízení VPN, Wi-Fi a e-mailu. Můžete je také použít k ověřování aplikací a k podepisování a šifrování S/MIME.  

Další informace o standardu najdete v tématu [odvozené piv přihlašovací údaje](https://www.nccoe.nist.gov/projects/building-blocks/piv-credentials) na adrese www.nccoe.nist.gov.

#### <a name="use-graph-api-to-specify-a-on-premises-user-principal-name-as-a-variable-for-scep-certificates----5437939----------"></a>Pomocí Graph API zadat hlavní název uživatele místního uživatele jako proměnnou pro certifikáty SCEP.<!--  5437939        -->  
Když použijete [Graph API Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0), můžete jako proměnnou alternativní název subjektu (San) pro certifikáty SCEP zadat onPremisesUserPrincipalName.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->tokenu prostředku
### <a name="microsoft-365-device-management"></a>Správa zařízení Microsoft 365

#### <a name="improved-administration-experience-in-microsoft-365-device-management---5551239---"></a>Vylepšené možnosti správy v Microsoft 365 správě zařízení<!-- 5551239 -->
Aktualizované a zjednodušené prostředí pro správu je teď všeobecně dostupné v pracovním prostoru specialista správy zařízení Microsoft 365 v [https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com), včetně těchto:

- **Aktualizovaná navigace**: najdou se Zjednodušená navigace na první úrovni, která logicky seskupuje funkce.
- **Nové filtry platformy**: můžete vybrat jednu platformu, která na stránkách zařízení a aplikace zobrazuje jenom zásady a aplikace pro vybranou platformu.
- **Nová Domovská stránka**: rychlé zobrazení stavu služby, stavu vašeho tenanta, zpráv atd. na nové domovské stránce.
Další informace o těchto vylepšeních najdete v [blogovém příspěvku Enterprise mobility + Security](https://go.microsoft.com/fwlink/?linkid=2109094) na webu Microsoft Tech Community.

#### <a name="introducing-endpoint-security-node-in-microsoft-365-device-management---5630102---"></a>Představujeme uzel zabezpečení koncového bodu v Microsoft 365 správě zařízení<!-- 5630102 -->

Uzel **zabezpečení koncového bodu** je teď v https://devicemanagement.microsoft.comvšeobecně dostupný v Microsoft 365 pracovní prostor pro správu zařízení, který seskupuje možnosti pro zabezpečení koncových bodů, jako jsou:

- Směrné plány zabezpečení: Pre'configured skupina nastavení, která vám pomůžou použít známou skupinu nastavení a výchozí hodnoty, které Microsoft doporučuje.
- Úkoly zabezpečení: Využijte výhod správy hrozeb a ohrožení zabezpečení ATPs v programu Microsoft Defender a použijte Intune k nápravě slabých míst koncových bodů.
- Microsoft Defender ATP: integrovaná ochrana před internetovými útoky v programu Microsoft Defender (ATP), která umožňuje zabránit narušení zabezpečení. "

Tato nastavení budou nadále přístupná z jiných použitelných uzlů, jako jsou zařízení, a aktuálně nakonfigurovaný stav bude stejný bez ohledu na to, kde máte přístup k těmto možnostem a tyto funkce povolíte.

Další informace o těchto vylepšeních najdete v [blogovém příspěvku o úspěchu pro zákazníky v Intune](https://aka.ms/Endpoint_security_node) na webu Microsoft Tech Community.

<!-- ########################## -->
## <a name="september-2019"></a>Září 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="managed-google-play-private-lob-apps---1464182----"></a>Spravované Google Play soukromé obchodní aplikace<!-- 1464182  -->tokenu prostředku
Intune teď umožňuje správcům IT publikovat soukromé obchodní aplikace pro Android do spravovaných Google Play prostřednictvím IFRAME vloženého v konzole nTune.  Dříve museli správci IT publikovat obchodní aplikace přímo do konzoly pro publikování Google, která vyžadovala několik kroků a byla časově náročná. Tato nová funkce umožňuje snadno publikovat obchodní aplikace s minimální sadou kroků, aniž byste museli opustit konzolu Intune.  Správci už nebudou muset ručně registrovat jako vývojáře s Google a nebude už muset platit poplatek za registraci Google $25.  Tato funkce může využít některý ze scénářů správy Android Enterprise, které používají spravované Google Play (pracovní profil, vyhrazená, plně spravovaná a neregistrovaná zařízení). V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat**. Pak v seznamu **Typ aplikace** vyberte **spravovaná Google Play** . Další informace o spravovaných aplikacích Google Play najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise v Intune](../apps/apps-add-android-for-work.md).

#### <a name="windows-company-portal-experience---1473353-3598357---"></a>Prostředí Windows Portál společnosti<!-- 1473353, 3598357 -->
Probíhá aktualizace Windows Portál společnosti. Na stránce aplikace v rámci Windows Portál společnosti budete moct používat víc filtrů. Stránka s podrobnostmi o zařízení se taky aktualizuje s vylepšeným uživatelským prostředím. Právě probíhá zavádění těchto aktualizací pro všechny zákazníky a očekává se dokončení na konci příštího týdne.

#### <a name="macos-support-for-web-apps---3174427---"></a>Podpora macOS pro webové aplikace<!-- 3174427 -->
Webové aplikace, které umožňují přidat a'shortcut k adrese URL na webu, mohou být nainstalovány do Docku pomocí Portál společnosti macOS. Koncoví uživatelé mohou získat přístup k **instalační** akci z podrobností aplikace pa'e pro webovou aplikaci v MacOS portál společnosti. Další informace o typu aplikace **webový odkaz** najdete v tématu [přidání aplikací do Microsoft Intune](../apps/apps-add.md) a [Přidání webových aplikací do Microsoft Intune](../apps/web-app.md).

#### <a name="macos-support-for-vpp-apps---3173501----"></a>Podpora macOS pro aplikace VPP<!-- 3173501  -->
aplikace macOS, zakoupené pomocí Apple Business Manageru, se v konzole zobrazí, když se tokeny programu Apple VPP synchronizují v Intune. Pomocí konzoly služby Intune můžete přiřadit, odvolat a znovu přiřadit licence na zařízení a uživatele pro skupiny. Microsoft Intune pomáhá spravovat aplikace VPP zakoupené pro použití ve vaší společnosti:

- Vykazuje informace o licencích z App Storu.
- Sleduje počet použitých licencí.
- Pomůže vám zabránit instalaci více kopií aplikace, než na kolik máte licence.

Další informace o Intune a VPP najdete v tématu [Správa hromadně zakoupených aplikací a knih pomocí Microsoft Intune](../apps/vpp-apps.md).

#### <a name="managed-google-play-iframe-support---2871756----"></a>Podpora spravované Google Play IFRAME<!-- 2871756  -->
Intune teď poskytuje podporu pro přidávání a správu webových odkazů přímo v konzole Intune prostřednictvím spravovaného Google Play IFRAME.  To umožňuje správcům IT odeslat obrázek adresy URL a ikony a potom tyto odkazy nasadit na zařízení stejně jako běžné aplikace pro Android. Tato funkce může využít některý ze scénářů správy Android Enterprise, které používají spravované Google Play (pracovní profil, vyhrazená, plně spravovaná a neregistrovaná zařízení). V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat**. Pak v seznamu **Typ aplikace** vyberte **spravovaná Google Play** . Další informace o spravovaných aplikacích Google Play najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise v Intune](../apps/apps-add-android-for-work.md).

#### <a name="silently-install-android-lob-apps-on-zebra-devices---4252734----"></a>Tichá instalace obchodních aplikací pro Android na zařízeních Zebra<!-- 4252734  -->
Při instalaci obchodních aplikací (LOB) pro Android do [zařízení Zebra](../configuration/android-zebra-mx-overview.md)se místo výzvy ke stažení a instalaci obchodní aplikace budete moct aplikaci nainstalovat tiše. V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat**. V podokně **Vybrat typ aplikace** vyberte **obchodní aplikace**. Další informace najdete v tématu [Přidání obchodní aplikace pro Android do Microsoft Intune](../apps/lob-apps-android.md).

V současné době se po stažení aplikace LOB na zařízení uživatele zobrazí oznámení o **úspěšném stažení** . Oznámení se může zrušit jenom klepnutím na **Vymazat vše** v odstínu oznámení. Tento problém s oznámením bude opraven v nadcházející verzi a instalace bude zcela tichá bez vizuálních indikátorů.

#### <a name="read-and-write-graph-api-operations-for-intune-apps---5031704----"></a>Čtení a zápis Graph APIch operací pro aplikace Intune<!-- 5031704  -->
Aplikace můžou volat Graph API Intune s použitím identity čtení i zápisu pomocí identity aplikace bez přihlašovacích údajů uživatele. Další informace o přístupu k rozhraní Microsoft Graph API pro Intune najdete [v tématu práce s Intune v Microsoft Graph](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0).

#### <a name="protected-data-sharing-and-encryption-for-intune-app-sdk-for-ios---3586942----"></a>Chráněné sdílení a šifrování dat pro sadu Intune App SDK pro iOS<!-- 3586942  -->
Sady Intune App SDK pro iOS bude používat 256bitových šifrovacích klíčů, když je povoleno šifrování pomocí zásad ochrany aplikací. Aby bylo možné chráněné sdílení dat, bude nutné, aby všechny aplikace měly sadu SDK verze 8.1.1.

#### <a name="updates-to-microsoft-intune-app---4997846---"></a>Aktualizace aplikace Microsoft Intune<!-- 4997846 -->
Microsoft Intune aplikace pro Android se aktualizovala s následujícími vylepšeními:
- Aktualizace a vylepšení rozložení tak, aby obsahovalo Dolní navigační údaje nejdůležitějších akcí.
- Přidala se další stránka, která zobrazuje profil uživatele.
- Do aplikace pro uživatele se přidalo zobrazování oznámení s možnou akcí, například nutnost aktualizovat nastavení zařízení.
- Přidali jsme zobrazení vlastních nabízených oznámení a zarovnejte aplikaci s podporou, která byla nedávno přidaná v aplikaci Portál společnosti pro iOS a Android. Další informace najdete v tématu [odesílání vlastních oznámení v Intune](../remote-actions/custom-notifications.md).
""
#### <a name="for-ios-devices-customize-the-enrollment-process-privacy-screen-of-the-company-portal---4394993---"></a>Pro zařízení s iOS si Přizpůsobte obrazovku ochrana osobních údajů procesu registrace Portál společnosti<!-- 4394993 -->
Pomocí Markdownu můžete přizpůsobit obrazovku osobních údajů Portál společnosti, kterou koncoví uživatelé uvidí během registrace iOS. Konkrétně budete moct přizpůsobit seznam věcí, které vaše organizace nemůže zobrazit nebo dělat na zařízení. Další informace najdete v tématu [Konfigurace aplikace Portál společnosti Intune](../apps/company-portal-app.md#privacy-statement-customization).



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="support-for-ikev2-vpn-profiles-for-ios---1943438-----"></a>Podpora pro profily IKEv2 VPN pro iOS<!-- 1943438   -->
V této aktualizaci můžete vytvořit profily sítě VPN pro nativního klienta VPN iOS pomocí protokolu IKEv2. IKEv2 je nový typ připojení v **konfiguraci zařízení** > **profily** > **vytvořit profil** > **iOS** pro typ profilu > **VPN** pro typ profilu > **Typ připojení**.

Tyto profily sítě VPN konfigurují nativního klienta VPN, takže nebudou nainstalovány ani vloženy žádné klientské aplikace VPN do spravovaných zařízení. Tato funkce vyžaduje, aby byla zařízení zaregistrovaná v Intune (registrace MDM).

Aktuální nastavení sítě VPN, která můžete nakonfigurovat, najdete v tématu [Konfigurace nastavení sítě VPN na zařízeních s iOS](../configuration/vpn-settings-ios.md).

Platí pro:

- iOS

#### <a name="device-features-device-restrictions-and-extension-profiles-for-ios-and-macos-settings-are-shown-by-enrollment-type---4886161-----"></a>Funkce zařízení, omezení zařízení a profily rozšíření pro nastavení iOS a macOS se zobrazují podle typu registrace.<!-- 4886161   -->

V Intune vytvoříte profily pro zařízení s iOS a macOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** nebo **MacOS** pro **funkce zařízení**>, **omezení zařízení**nebo **rozšíření** pro typ profilu). 

V této části "ktualizovat" jsou dostupná nastavení na portálu Intune zařazená do kategorie podle typu registrace, na který se vztahují:

- iOS
  - Zápis uživatele ""
  - Registrace zařízení
  - Automatický zápis zařízení (pod dohledem)
  - Všechny typy registrace

- macOS
  - Schválené uživatelem
  - Registrace zařízení
  - Automatický zápis zařízení
  - Všechny typy registrace

Platí pro:

- iOS

#### <a name="new-voice-control-settings-for-supervised-ios-devices-running-in-kiosk-mode---4892835-----"></a>Nové nastavení ovládání hlasu pro zařízení s iOS běžící v celoobrazovkovém režimu<!-- 4892835   -->
V Intune můžete vytvářet zásady, které budou spouštět zařízení se systémem iOS pod dohledem jako veřejný terminál nebo vyhrazené zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro > **omezení zařízení** pro typ profilu > veřejný **terminál**).

V této aktualizaci můžete řídit nová nastavení:
- **Ovládání hlasu**: povolí hlasové ovládání zařízení v celoobrazovkovém režimu.
- **Změna ovládání hlasu**: umožňuje uživatelům změnit nastavení hlasového ovládacího prvku v zařízení v celoobrazovkovém režimu.

Aktuální nastavení zobrazíte tak, že přejdete na [Nastavení veřejného terminálu iOS](../configuration/device-restrictions-ios.md#kiosk).

Platí pro:

- iOS 13,0 a novější

#### <a name="use-single-sign-on-for-apps-and-websites-on-your-ios-and-macos-devices---4893175-----"></a>Použití jednotného přihlašování pro aplikace a weby na zařízeních s iOS a macOS<!-- 4893175   -->
V této aktualizaci je k dispozici několik nových nastavení jednotného přihlašování pro zařízení s iOS a macOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** nebo **MacOS** pro **funkce zařízení** > pro typ profilu).

Pomocí těchto nastavení můžete nakonfigurovat jednotné přihlašování, zejména pro aplikace a weby, které používají ověřování pomocí protokolu Kerberos. Můžete si vybrat mezi obecnými přihlašovacími údaji jednotného přihlašování aplikace a integrovaným rozšířením Kerberos společnosti Apple.

Pokud chcete zobrazit aktuální funkce zařízení, které můžete konfigurovat, přejděte na [funkce zařízení s iOS](../configuration/ios-device-features-settings.md) a [MacOS funkce zařízení](../configuration/macos-device-features-settings.md).

Platí pro:

- iOS 13. ' a novější
- macOS 10,15 a novější

#### <a name="associate-domains-to-apps-on-macos-1015-devices---4898079-----"></a>Přidružení domén k aplikacím na macOS 10.15 a zařízeních<!-- 4898079   -->
Na zařízeních macOS můžete konfigurovat různé funkce a nasdílet je do zařízení pomocí zásad (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **MacOS** pro **funkce zařízení** > pro typ profilu). V této aktualizaci můžete k aplikacím přidružit domény. Tato funkce pomáhá sdílet přihlašovací údaje s weby souvisejícími s vaší aplikací a lze ji použít s rozšířením jednotného přihlašování společnosti Apple, univerzálními odkazy a automatického vyplňování hesel. 

Pokud chcete zobrazit aktuální funkce, které můžete nakonfigurovat, přejděte na [Nastavení funkcí zařízení MacOS v Intune](../configuration/macos-device-features-settings.md).

Platí pro:

- macOS 10,15 a novější

#### <a name="use-itunes-and-aps-in-the-itunes-app-store-url-when-showing-or-hiding-apps-on-ios-supervised-devices---4928474-----"></a>Při zobrazování nebo skrývání aplikací na zařízeních s iOS pod dohledem použijte iTunes a a'ps v adrese URL obchodu iTunes.<!-- 4928474   --> 
V Intune můžete vytvořit zásady, které budou zobrazovat nebo skrývat aplikace na zařízeních s iOS pod dohledem (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro > **omezení zařízení** pro typ profilu > **Zobrazit nebo skrýt aplikace**). 

Můžete zadat adresu URL obchodu s aplikacemi iTunes, například `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8`. V této aktualizaci lze v adrese URL použít jak `apps`, tak `itunes`, například:
- `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8`
- `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`

Další informace o těchto nastaveních najdete v tématu [zobrazení nebo skrytí aplikací](../configuration/device-restrictions-ios.md#show-or-hide-apps).

Platí pro:
- iOS

#### <a name="windows-10-compliance-policy-password-type-values-are-clearer-and-match-csp---5138985---"></a>Hodnoty typu hesla zásad dodržování předpisů ve Windows 10 jsou jasné a neshodné s poskytovatelem CSP.<!-- 5138985 -->
V zařízeních s Windows 10 můžete vytvořit zásady dodržování předpisů, které vyžadují konkrétní funkce hesla ( **zásady** > **dodržování předpisů zařízením** > **vytvořit zásadu** > **Windows 10 a novější** pro zabezpečení platformy > **System**). V této aktualizaci:
- Hodnoty **typu hesla** jsou jasné a aktualizované tak, aby ODPOVÍDALy [zprostředkovateli DeviceLock/AlphanumericDevicePasswordRequired](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired).
- Nastavení **vypršení platnosti hesla (dny)** se aktualizuje, aby se povolily hodnoty z 1-730 dnů. 

Další informace o nastavení dodržování předpisů ve Windows 10 najdete v tématu [nastavení Windows 10 a novějších k označení zařízení jako odpovídajících nebo nevyhovujících](../protect/compliance-policy-create-windows.md)předpisům. 

Platí pro:
- Windows 10 a novější

 #### <a name="updated-ui-for-configuring-microsoft-exchange-on-premises-access---4092920---"></a>Aktualizované uživatelské rozhraní pro konfiguraci přístupu k místnímu systému Microsoft Exchange<!-- 4092920 -->  
Aktualizovali jsme konzolu, kde jste [nakonfigurovali přístup k místnímu přístupu Microsoft Exchange](../protect/conditional-access-exchange-create.md). Všechny konfigurace pro přístup k místnímu Exchangi jsou teď dostupné ve stejném podokně konzoly, kde můžete *Povolit řízení přístupu k místnímu Exchangi*.  

#### <a name="allow-or-restrict-adding-app-widgets-to-the-home-screen-on-android-enterprise-work-profile-devices---1109650----"></a>Povolení nebo omezení přidání widgetů aplikací na domovskou obrazovku na zařízeních s pracovními profily Android Enterprise<!-- 1109650  --> 
Na zařízeních s Androidem Enterprise můžete nakonfigurovat funkce v pracovním profilu (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for Platform > **Work Profiles > jenom omezení zařízení** pro typ profilu). V této aktualizaci můžete uživatelům dovolit přidávat widgety, které jsou zpřístupněny aplikacemi pracovní profil na domovské obrazovce zařízení.

Pokud chcete zobrazit nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md).

Platí pro:
- Pracovní profil Android Enterprise

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="new-tenants-will-default-away-from-android-device-administrator-management---4869790-----"></a>Ve výchozím nastavení budou noví klienti pryč ze správy zařízení s Androidem.<!-- 4869790   -->
Možnosti Správce zařízení s Androidem jsou nahrazené Androidem Enterprise. Proto doporučujeme místo toho použít Android Enterprise pro nové registrace. V budoucí aktualizaci budou muset noví klienti v rámci registrace zařízení s Androidem v případě použití správy Správce zařízení provést následující nezbytné kroky: Přejít na **Intune** > **registrace zařízení** > **registrace Androidu** > **osobních a firemních zařízení s oprávněními** Správce zařízení > **ke správě zařízení použít Správce zařízení**.

Stávající klienti nebudou mít ve svých prostředích žádné změny.

Další informace o Správci zařízení s Androidem v Intune najdete v tématu [registrace Správce zařízení s Androidem](https://docs.microsoft.com/intune/android-enroll-device-administrator).

#### <a name="list-of-dep-devices-associated-with-a-profile---5012045----"></a>Seznam zařízení DEP přidružených k profilu<!-- 5012045  -->
Teď můžete zobrazit stránkovaný seznam zařízení Apple automatizované Program registrace zařízení (DEP), která jsou přidružená k profilu. Seznam můžete vyhledat na libovolné stránce v seznamu. Pokud chcete zobrazit seznam, přejděte na **Intune** > **registrace zařízení** > registrace **Apple** > **tokeny programu registrace** > vyberte profily >ch **profilů** > vyberte profil > **přiřazená zařízení** (v části **monitor**).

#### <a name="ios-user-enrollment-in-preview---4817900---"></a>Registrace uživatele pro iOS ve verzi Preview<!-- 4817900 -->
Verze iOS 13,1 od společnosti Apple zahrnuje registraci uživatelů, novou formu zjednodušené správy pro zařízení s iOS. Dá se použít místo registrace zařízení nebo automatického zápisu zařízení (dříve Program registrace zařízení) pro osobní zařízení vlastněná společností. Intune Preview podporuje tuto sadu funkcí tím, že vám umožní:

- Registrace cílového uživatele pro skupiny uživatelů.
- Poskytněte koncovým uživatelům možnost výběru mezi jednodušším zápisem uživatele nebo silnějším zápisem zařízení při registraci svých zařízení.

Od verze 9/24/2019 s vydáním iOS 13,1 jsme v procesu zavedli tyto aktualizace všem zákazníkům a očekáváme, že budou dokončeny na konci příštího týdne.

Platí pro:

- iOS 13,1 a novější

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="more-android-fully-managed-support---3464667-4631425-4631440-5227935-4062195-----"></a>Další plně spravovaná podpora Androidu<!-- 3464667, 4631425, 4631440, 5227935, 4062195   -->
Přidali jsme následující podporu pro plně spravovaná zařízení s Androidem:

- Certifikáty SCEP pro plně spravovanou Android jsou k dispozici pro ověřování certifikátů na zařízeních spravovaných jako vlastník zařízení. Certifikáty SCEP jsou už na zařízeních pracovního profilu podporované.  Pomocí certifikátů SCEP pro vlastníka zařízení budete moct: <!-- 5227935 -->
    - Vytvoření profilu SCEP v části DO v Androidu Enterprise
    - propojení certifikátů SCEP s profilem Wi-Fi pro ověřování
    - propojení certifikátů SCEP a provádění profilů sítě VPN pro ověřování
    - propojení certifikátů SCEP pro ověřování e-mailových profilů (přes AppConfig)
- Systémové aplikace jsou podporované na zařízeních s Androidem Enterprise. V Intune přidejte aplikaci systému Android Enterprise, a to tak, že vyberete **klientské aplikace** > **aplikací** > **Přidat**. V seznamu **Typ aplikace** vyberte aplikace pro **Android Enterprise System**. Další informace najdete v tématu [Přidání aplikací pro Android Enterprise System do Microsoft Intune](../apps/apps-ae-system.md). <!-- 4062195 -->
- V části **dodržování předpisů zařízením** > **vlastníka zařízení**pro **Android Enterprise** > můžete vytvořit zásady dodržování předpisů, které nastaví úroveň ověření Google SafetyNet.   <!-- 4631425 -->
- Na zařízeních s plnou správou Androidu Enterprise se podporují poskytovatelé ochrany před mobilními hrozbami. V **dodržování předpisů zařízením** > **vlastníka zařízení**s **Androidem Enterprise** > můžete vybrat přijatelnou úroveň hrozeb. <!-- 4631440 --> [Nastavení Androidu Enterprise k označení zařízení jako kompatibilních nebo nekompatibilních s použitím Intune](../protect/compliance-policy-create-android-for-work.md#device-owner) seznam aktuálních nastavení.
- Na zařízeních s plnou správou Androidu Enterprise se teď dá nakonfigurovat aplikace spouštěče Microsoftu prostřednictvím zásad konfigurace aplikací, které umožňují standardizované prostředí koncového uživatele na plně spravovaném zařízení. K přizpůsobení zařízení s Androidem se dá použít aplikace Microsoft spouštěče. Pomocí aplikace spolu s účet Microsoft nebo pracovním nebo školním účtem máte přístup k vašemu kalendáři, dokumentům a posledním aktivitám v přizpůsobeném kanálu. <!-- 5334044 -->

V této aktualizaci jsme spokojeni s oznámením, že podpora Intune pro plně spravovanou platformu Android Enterprise je teď všeobecně dostupná.

Platí pro:

- Zařízení se systémem Android Enterprise s plnou správou

#### <a name="send-custom-notifications-to-a-single-device---4928910---"></a>Odesílání vlastních oznámení na jedno zařízení<!-- 4928910 -->
Teď můžete vybrat jedno zařízení a pak použít akci vzdáleného zařízení k [odeslání vlastního oznámení jenom na toto zařízení](../remote-actions/custom-notifications.md#send-a-custom-notification-to-a-single-device).

#### <a name="wipe-and-passcode-reset-actions-arent-available-for-ios-devices-that-are-enrolled-by-using-user-enrollment---4950491---"></a>Akce vymazání a resetování hesla nejsou k dispozici pro zařízení s iOS, která jsou zaregistrovaná pomocí zápisu uživatelů.<!-- 4950491 -->
Zápis uživatele je nový typ registrace zařízení Apple. Při registraci zařízení pomocí registrace uživatele nebudou pro taková zařízení k dispozici vzdálené akce resetování a resetování hesla.

#### <a name="intune-support-for-ios-13-and-macos-catalina-devices---4665317---"></a>Podpora Intune pro zařízení s iOS 13 a macOS Catalina<!-- 4665317 -->
Intune teď podporuje správu zařízení se systémem iOS 13 i macOS Catalina.
Další informace najdete v [příspěvku na blogu Microsoft Intune podpoře pro iOS 13 a iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Support-for-iOS-13-and-iPadOS/ba-p/861998).

#### <a name="intune-support-for-ipados-and-ios-131-devices--5439574--"></a>Podpora Intune pro zařízení iPadOS a iOS 13,1<!--5439574-->
Intune teď podporuje správu zařízení iPadOS i iOS 13,1. Další informace najdete v [tomto příspěvku blogu](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Support-for-iOS-13-1-and-iPadOS/ba-p/873094).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="bitlocker-support-for-client-driven-recovery-password-rotation----3444125---"></a>Podpora BitLockeru pro otočení hesla pro obnovení na základě klienta<!--  3444125 -->
Použijte nastavení Endpoint Protection Intune ke konfiguraci [rotace hesla pro obnovení](../protect/endpoint-protection-windows-10.md#windows-encryption) na zařízeních s Windows verze 1909 nebo novějším na základě klienta.

Toto nastavení inicializuje obnovení hesla na základě klienta po obnovení jednotky operačního systému (buď pomocí programu Bootmgr nebo WinRE) a odemknutí hesla pro obnovení na pevné datové jednotce. Toto nastavení aktualizuje specifické heslo pro obnovení, které bylo použito, a jiná nepoužívaná hesla na svazku zůstanou beze změny. Další informace najdete v dokumentaci k nástroji BitLocker CSP pro [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp).

#### <a name="tamper-protection-for-windows-defender-antivirus---4705448----------"></a>Ochrana proti úmyslné ochraně pro antivirovou ochranu v programu Windows Defender<!-- 4705448        -->
Použijte Intune ke správě *ochrany před zneužitím antivirové ochrany* v programu Windows Defender. Pokud použijete konfigurační profily zařízení pro Windows 10 Endpoint Protection, najdete [nastavení pro ochranu proti falšování](../protect/endpoint-protection-windows-10.md#microsoft-defender-security-center) ve skupině Security Center programu Microsoft Defender. Ochranu proti neoprávněným nastavením ochrany proti chybám můžete *nastavit tak, aby se* zapnulo omezení ochrany před odesláním, nastavení *zakázáno* pro jejich vypnutí, nebo nastavit, aby se zařízení*nenakonfigurovalo* jako aktuální konfigurace.  

Další informace o ochraně před zneužitím najdete v dokumentaci k Windows v tématu [zabránění změnám nastavení zabezpečení pomocí ochrany před neoprávněnými](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/prevent-changes-to-security-settings-with-tamper-protection) změnami.

#### <a name="advanced-settings-for-windows-defender-firewall-are-now-generally-available----5317392---------"></a>Rozšířená nastavení pro firewall v programu Windows Defender jsou teď všeobecně dostupná.<!--  5317392       -->  
[Vlastní pravidla brány firewall v programu Windows Defender pro službu Endpoint Protection](../protect/endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices), která konfigurujete jako součást profilu konfigurace zařízení, jsou ve verzi Public Preview a jsou všeobecně dostupná (GA).  Tato pravidla můžete použít k určení příchozího a odchozího chování aplikací, síťových adres a portů. Tato pravidla byla vydaná v červenci jako verze Public Preview. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="intune-user-interface-update--tenant-status-dashboard---5273210----"></a>Aktualizace uživatelského rozhraní Intune – řídicí panel stavu tenanta<!-- 5273210  -->
Uživatelské rozhraní pro řídicí panel stavu tenanta se aktualizovalo tak, aby bylo zarovnané na styly uživatelského rozhraní Azure. Další informace najdete v tématu [stav tenanta](tenant-status.md).

### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="scope-tags-now-support-terms-of-use-policies---2358863----"></a>Značky oboru teď podporují zásady používání podmínek použití<!-- 2358863  -->
Nyní můžete přiřadit [značky oboru](scope-tags.md) k zásadám použití. Provedete to tak, že přejdete na **Intune** > **registrace zařízení** > **podmínky** > vyberte položku v seznamu > **vlastnosti** > **značky oboru** > vyberte značku oboru.

<!-- ########################## -->
## <a name="august-2019"></a>Srpen 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="control-ios-app-uninstall-behavior-at-device-unenrollment---3504144-----"></a>Řízení chování při odinstalaci aplikace pro iOS při zrušení registrace zařízení<!-- 3504144   -->
Správci mohou spravovat, zda je aplikace v zařízení odebrána nebo udržována v případě, že je zařízení odregistrováno na úrovni uživatele nebo skupiny zařízení. 

#### <a name="categorize-microsoft-store-for-business-apps---3926922---"></a>Kategorizace Microsoft Store pro obchodní aplikace<!-- 3926922 -->
Microsoft Store pro obchodní aplikace můžete zařadit do kategorií. Provedete to tak, že v **Intune** > **klientských aplikacích** > **aplikace** > vyberete **kategorii**> **informace o aplikaci** Microsoft Store pro obchodní aplikace > . V rozevírací nabídce přiřaďte kategorii.

#### <a name="customized-notifications-for-microsoft-intune-app-users---4843354----"></a>Přizpůsobená oznámení pro uživatele aplikací Microsoft Intune<!-- 4843354  -->
Microsoft Intune aplikace pro Android teď podporuje zobrazení vlastních nabízených oznámení a jejich vyrovnání s podporou, která se nedávno přidala v Portál společnosti aplikacích pro iOS a Android. Další informace najdete v tématu [odesílání vlastních oznámení v Intune](../remote-actions/custom-notifications.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

### <a name="configure-microsoft-edge-settings-using-administrative-templates-for-windows-10-and-newer---5228061---"></a>Konfigurace nastavení Microsoft Edge pomocí šablon pro správu pro Windows 10 a novější<!-- 5228061 -->
V zařízeních s Windows 10 a novějších můžete vytvořit šablony pro správu a nakonfigurovat nastavení zásad skupiny v Intune. V této aktualizaci můžete nakonfigurovat nastavení, která se vztahují na Microsoft Edge verze 77 a novější.

Další informace o šablonách pro správu najdete v tématu [použití šablon Windows 10 ke konfiguraci nastavení zásad skupiny v Intune](../configuration/administrative-templates-windows.md).

Platí pro:

- Windows 10 a novější (Windows RS4 +)

#### <a name="new-features-for-android-enterprise-dedicated-devices-in-multi-app-mode---3755304-3041943-3041946-----"></a>Nové funkce pro vyhrazená zařízení s Androidem Enterprise v režimu více aplikací<!-- 3755304 3041943 3041946   -->

V Intune můžete ovládat funkce a nastavení pomocí veřejného terminálu na vyhrazených zařízeních s Androidem Enterprise (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** pro vlastní platformu > jenom pro **vlastníka zařízení, omezení zařízení** pro typ profilu).

V této aktualizaci se přidávají následující funkce:

- **Vyhrazená zařízení** > **více aplikacemi**: **tlačítko virtuální domů** se dá na zařízení zobrazit roztažením nahoru nebo plovoucí na obrazovce, aby ho uživatelé mohli přesunout.
- **Vyhrazená zařízení** > **více aplikacemi**: **přístup svítící** umožňuje uživatelům používat svítící. 
- **Vyhrazená zařízení** > **více aplikacemi**: **ovládání hlasitosti médií** umožňuje uživatelům řídit hlasitost média zařízení pomocí posuvníku. 
- **Vyhrazená zařízení** > **více aplikacemi**: **Povolte šetřič obrazovky**, nahrajte vlastní obrázek a ovládací prvek, když se zobrazí spořič obrazovky.

Pokud chcete zobrazit aktuální nastavení, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings).

Platí pro:

- Zařízení se systémem Android Enterprise vyhrazená

#### <a name="new-app-and-configuration-profiles-for-android-enterprise-fully-managed-devices---3574215-3574238-3574235-3574232-----"></a>Nové aplikace a konfigurační profily pro zařízení s plnou správou pro Android Enterprise<!-- 3574215 3574238 3574235 3574232   -->
Pomocí profilů můžete nakonfigurovat nastavení, která použijí nastavení sítě VPN, e-mailu a Wi-Fi, na zařízení s vlastníkem zařízení s Androidem Enterprise (plně spravovaná). V této aktualizaci můžete:

- Pomocí [zásad konfigurace aplikací](../apps/app-configuration-policies-use-android.md) nasaďte nastavení Outlooku, Gmail a devět pracovních e-mailů.
- Pomocí profilů konfigurace zařízení nasaďte [Nastavení důvěryhodných kořenových certifikátů](../protect/certificates-configure.md).
- Pomocí profilů konfigurace zařízení nasaďte nastavení [sítě VPN](../configuration/vpn-settings-android-enterprise.md) a [Wi-Fi](../configuration/wi-fi-settings-android-enterprise.md) .

> [!IMPORTANT]
> S touto funkcí se uživatelé ověřují pomocí svého uživatelského jména a hesla pro profily sítě VPN, Wi-Fi a e-mailu. V současné době není ověřování založené na certifikátech k dispozici.

Platí pro:  
- Vlastník zařízení se systémem Android Enterprise (plně spravovaný)

#### <a name="control-the-apps-files-documents-and-folders-that-open-when-users-sign-in-to-macos-devices--3914202-----"></a>Řízení aplikací, souborů, dokumentů a složek, které se otevřou, když se uživatelé přihlásí k zařízením macOS<!--3914202   -->
Můžete povolit a nakonfigurovat funkce na zařízeních macOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **MacOS** pro **funkce zařízení** > pro typ profilu). 

V této aktualizaci se nachází nové nastavení přihlašovacích položek, které určuje, které aplikace, soubory, dokumenty a složky se otevřou, když se uživatel přihlásí k zaregistrovanému zařízení. 

Pokud chcete zobrazit aktuální nastavení, přejděte na [Nastavení funkcí zařízení MacOS v Intune](../configuration/macos-device-features-settings.md).

Platí pro:  
- macOS

#### <a name="deadlines-replace-engaged-restart-settings-for-windows-update-rings---4464404----------"></a>Konečné termíny nahrazují nastavení opětovného spuštění pro web Windows Update okruhy<!-- 4464404        -->
Pro zajištění souladu s nejnovějšími [změnami údržby Windows](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903#servicing)teď aktualizační kanály Windows 10 v Intune [podporují nastavení pro konečné termíny](../protect/windows-update-settings.md). *Konečné termíny* určují, kdy zařízení nainstaluje funkce a aktualizace zabezpečení.  V zařízeních se systémem Windows 10 1903 nebo novějším mají *termíny* přednost před konfiguracemi pro *následné restartování*.  V budoucnu se *konečné termíny* *nahrazují i v dřívějších* verzích Windows 10.  

Když nebudete konfigurovat *konečné termíny*, budou se zařízení dál používat s nastavením jejich nastavení, ale Intune bude v budoucí aktualizaci zastaralá o podporu *pro nastavení.*  

Naplánujte použití *konečných termínů* pro všechna vaše zařízení s Windows 10. Po nastavení *konečných termínů* můžete změnit konfigurace Intune, aby se *restarty* nenakonfigurovaly. Pokud je nastavené na Nenakonfigurováno, Intune zastaví správu těchto nastavení na zařízeních, ale neodebere poslední konfigurace nastavení ze zařízení. Poslední konfigurace, které byly nastavené pro probíhající *restart* , zůstávají aktivní a používají se na zařízeních, dokud se tato nastavení neupraví jinou metodou než Intune. Později, když se změní verze Windows, nebo když se u *konečných termínů* podpora Intune dokončí rozšíření zařízení na verzi Windows, začne používat nové nastavení, které už jsou na svém místě.

#### <a name="support-for-multiple-microsoft-intune-certificate-connectors-----4704642--------"></a>Podpora více Microsoft Intunech konektorů certifikátů<!--   4704642      -->
Intune teď podporuje instalaci a používání více [Microsoft Intunech konektorů certifikátů pro operace PKCS](../protect/certficates-pfx-configure.md). Tato změna podporuje vyrovnávání zatížení a vysokou dostupnost konektoru. Každá instance konektoru může zpracovávat žádosti o certifikát z Intune.  Pokud jeden konektor není k dispozici, ostatní konektory pokračují v zpracování požadavků.

Chcete-li použít více konektorů, nemusíte upgradovat na nejnovější verzi softwaru konektoru.  

#### <a name="new-settings-and-changes-to-existing-settings-to-restrict-features-on-ios-and-macos-devices---4867699-4867709-----"></a>Nové nastavení a změny stávajících nastavení pro omezení funkcí v zařízeních s iOS a macOS<!-- 4867699 4867709   -->
Můžete vytvořit profily k omezení nastavení na zařízeních s iOS a macOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** nebo **MacOS** pro typ platformy > **omezení zařízení**). Tato aktualizace obsahuje následující funkce:

- V **macOS** > **omezení zařízení** > **cloudu a úložišti**, **použijte nové nastavení** pro překládání, které uživatelům zabrání ve spouštění práce na jednom zařízení macOS a pokračujte v práci na jiném zařízení MacOS nebo iOS.

  Pokud chcete zobrazit aktuální nastavení, přejděte na [nastavení zařízení MacOS a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-macos.md).

- V případě zařízení se **systémem iOS** > **omezení zařízení**existuje několik změn:

  - **Integrované aplikace** > **Najít iPhone (jenom pod dohledem)** : nové nastavení, které tuto funkci blokuje v funkci najít aplikaci. 
  - **Integrované aplikace** > **Najít přátele (jenom pod dohledem)** : nové nastavení, které tuto funkci blokuje v funkci najít aplikaci. 
  - **Bezdrátová** > **Změna stavu Wi-Fi (jenom pod dohledem)** : nové nastavení, které uživatelům brání v zapnutí nebo vypnutí Wi-Fi na zařízení.
  - **Klávesnice a slovník** > **QuickPath (jenom pod dohledem)** : nové nastavení, které blokuje funkci QuickPath.
  - **Cloud a úložiště**: **pokračování aktivity** se přejmenovalo na **odevzdání**.

  Pokud chcete zobrazit aktuální nastavení, přejděte na [nastavení zařízení s iOS, abyste mohli povolit nebo zakázat funkce využívající Intune](../configuration/device-restrictions-ios.md).

Platí pro:  
- macOS 10,15 a novější
- iOS 13 a novější

#### <a name="some-unsupervised-ios-device-restrictions-will-become-supervised-only-with-the-ios-130-release---4867809-----"></a>Některá z nesledovaných omezení zařízení s iOS se budou pod dohledem – jenom s vydáním iOS 13,0.<!-- 4867809   -->
V této aktualizaci se některá nastavení vztahují na zařízení, která jsou jenom pod dohledem, pomocí verze iOS 13,0. Pokud jsou tato nastavení nakonfigurovaná a přiřazená k zařízením, která nejsou pod dohledem před vydáním iOS 13,0, nastavení se pořád aplikují na tato zařízení, která nejsou pod dohledem. I nadále platí i po upgradu zařízení na iOS 13,0. Tato omezení se odeberou na nekontrolovaných zařízeních, která se zálohují a obnovují.

Nastavení zahrnuje tyto položky:

- App Store, zobrazování dokumentů, hraní her
  - App Store
  - Explicitní obsah iTunes, hudba, podcast nebo zprávy
  - Přidání přátel Game Center
  - Hry pro víc hráčů
- Integrované aplikace
  - Fotoaparát
    - FaceTime
  - Safari
    - Automatické vyplnění
- Cloud a úložiště
  - Zálohování do iCloud
  - Zablokovat synchronizaci dokumentů iCloud
  - Blokovat synchronizaci řetězce klíčů iCloud

Pokud chcete zobrazit aktuální nastavení, přejděte na [nastavení zařízení s iOS, abyste mohli povolit nebo zakázat funkce využívající Intune](../configuration/device-restrictions-ios.md).

Platí pro:  
- iOS 13,0 a novější

#### <a name="improved-device-status-for-macos-filevault-encryption---4944983-----------"></a>Vylepšený stav zařízení pro šifrování trezoru macOS<!-- 4944983         -->
Aktualizovali jsme několik zpráv o [stavu zařízení](../protect/encryption-monitor.md#device-encryption-status) pro šifrování trezoru úložiště na zařízeních MacOS.

#### <a name="some-windows-defender-antivirus-scan-settings-in-the-reporting-show-a-failed-status---5119229---"></a>Některá nastavení kontroly antivirové ochrany v programu Windows Defender v hlášení zobrazují stav selhání<!-- 5119229 -->
V Intune můžete vytvořit zásady, které budou používat antivirovou ochranu v programu Windows Defender ke skenování zařízení s Windows 10 (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** pro > **omezení zařízení** pro typ profilu > **antivirová ochrana v programu Windows Defender**). Čas, kdy **má probíhat každodenní Rychlá kontrola** a **typ Systémové kontroly k provedení** sestav, zobrazuje stav selhání, pokud je ve skutečnosti stav úspěch. 

V této aktualizaci je toto chování opraveno. Takže když se nastavení úspěšně dokončí, zobrazí se při úspěšném prověřování stav úspěch a v případě, že se nastavení nepovede, zobrazí se stav úspěšného provedení **každodenní rychlé kontroly** a **typ kontroly prováděné systémem** .

Další informace o nastavení antivirové ochrany v programu Windows Defender najdete v tématu [nastavení zařízení s Windows 10 (a novější) k povolení nebo omezení funkcí v Intune](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### <a name="zebra-technologies-is-a-supported-oem-for-oemconfig-on-android-enterprise-devices---4843713---"></a>Technologie Zebra je podporovaným výrobcem OEM pro OEMConfig na zařízeních s Androidem Enterprise.<!-- 4843713 -->
V Intune můžete vytvořit profily konfigurace zařízení a použít nastavení pro zařízení s Androidem Enterprise pomocí OEMConfig (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for Platform > **OEMConfig** pro typ profilu).

V této aktualizaci je Zebra technologie podporovaným výrobcem OEM (Original Equipment Manufacturer) pro OEMConfig. Další informace o OEMConfig najdete v tématu [použití a Správa zařízení s Androidem Enterprise pomocí OEMConfig](../configuration/android-oem-configuration-overview.md).

Platí pro:  
- Android Enterprise


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="default-scope-tags---3702875----"></a>Výchozí značky oboru<!-- 3702875  -->
Nově integrovaná značka výchozího oboru je nyní k dispozici. Všechny neoznačené objekty Intune, které podporují značky oboru, se automaticky přiřazují k výchozí značce oboru. **Výchozí** značka oboru je přidána do všech existujících přiřazení rolí, aby bylo udržování parity s prostředím pro správu v současnosti. Pokud nechcete, aby správce viděli objekty Intune s výchozím označením oboru, odeberte z přiřazení role výchozí značku oboru. Tato funkce je podobná funkci obory zabezpečení v Configuration Manager. Další informace najdete v tématu [použití značek RBAC a Scope k distribuci](scope-tags.md).

#### <a name="android-enrollment-device-administrator-support---4869749-----"></a>Podpora Správce zařízení registrace Androidu<!-- 4869749   -->
Do registrační stránky pro Android se přidala možnost registrace Správce zařízení s Androidem ( > **registrace zařízení** v**Intune** > **registraci v Androidu**). Správce zařízení s Androidem bude ve výchozím nastavení pro všechny klienty stále povolen.  Další informace najdete v tématu [registrace Správce zařízení s Androidem](../enrollment/android-enroll-device-administrator.md).

#### <a name="skip-more-screens-in-setup-assistant---4877451----"></a>Přeskočit další obrazovky v Průvodci nastavením <!--4877451  -->
Můžete nastavit Program registrace zařízení profily pro přeskočení následujících obrazovek pomocníka s nastavením:
- Pro iOS
    - Vzhled
    - Jazyk Express
    - Preferovaný jazyk
    - Migrace zařízení do zařízení
- Pro macOS
    - Čas obrazovky
    - Nastavení Touch ID

Další informace o přizpůsobení pomocníka s nastavením najdete v tématu [vytvoření registračního profilu Apple pro iOS](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) a [vytvoření registračního profilu Apple pro MacOS ](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

#### <a name="add-a-user-column-to-the-autopilot-device-csv-upload-process---3823054---"></a>Přidání uživatelského sloupce do procesu nahrání souboru CSV pro zařízení s autopilotem<!-- 3823054 -->
Nyní můžete přidat uživatelský sloupec do nahrávání sdíleného svazku clusteru pro zařízení s autopilotem. To vám umožní hromadně přiřazovat uživatele v době, kdy naimportujete sdílený svazek clusteru. Další informace najdete v tématu [registrace zařízení s Windows v Intune pomocí automatických pilotů Windows](../enrollment/enrollment-autopilot.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="configure-automatic-device-clean-up-time-limit-down-to-30-days--4231059----"></a>Nakonfigurujte automatický časový limit pro vyčištění zařízení na 30 dní.<!--4231059  -->
Můžete nastavit automatický časový limit pro vyčištění zařízení, který je kratší než 30 dní (místo předchozího limitu 90 dní) po posledním přihlášení. Provedete to tak, že přejdete na **zařízení** > **Intune** > **Nastavení** > **pravidla čištění zařízení**.

#### <a name="build-number-included-on-android-device-hardware-page---4461910-----"></a>Číslo sestavení zahrnuté na stránce hardware pro zařízení s Androidem<!-- 4461910   -->
Nová položka na stránce hardware pro každé zařízení s Androidem zahrnuje číslo buildu operačního systému daného zařízení. Další informace najdete v tématu [zobrazení podrobností o zařízení v Intune](../remote-actions/device-inventory.md).

<!-- ########################## -->
## <a name="july-2019"></a>Červenec 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="customized-notifications-for-users-and-groups---16766574------------"></a>Přizpůsobená oznámení pro uživatele a skupiny<!-- 16766574          -->
Odešlete vlastní nabízená oznámení z aplikace Portál společnosti uživatelům na zařízeních s iOS a Androidem, která spravujete pomocí Intune. Tato mobilní nabízená oznámení jsou vysoce přizpůsobitelná s bezplatným textem a lze je použít pro libovolný účel. Můžete je cílit na různé skupiny uživatelů ve vaší organizaci. Další informace najdete v tématu [vlastní oznámení](../remote-actions/custom-notifications.md).

#### <a name="googles-device-policy-controller-app---3041950----"></a>Aplikace kontroleru zásad zařízení Google<!-- 3041950  -->
Aplikace spravované domovské obrazovky teď poskytuje přístup k aplikaci zásad zařízení s Androidem. Spravovaná aplikace pro domovskou obrazovku je vlastní spouštěč používaný pro zařízení zaregistrovaná v Intune jako vyhrazená zařízení Android Enterprise (AE) pomocí celoobrazovkového režimu s více aplikacemi. K aplikaci zásad pro zařízení s Androidem můžete získat přístup, nebo se uživatelé k aplikaci zásad zařízení s Androidem pořídit pro účely podpory a ladění. Tato funkce je k dispozici v době, kdy se zařízení zaregistruje a zamkne do spravované domovské obrazovky. K použití této funkce nejsou potřeba žádné další instalace.

#### <a name="outlook-protection-settings-for-ios-and-android-devices---3212619---"></a>Nastavení ochrany Outlooku pro zařízení s iOS a Androidem<!-- 3212619 -->
Pro Outlook pro iOS a Android teď můžete nakonfigurovat obecná nastavení konfigurace aplikací a ochrany dat, a to pomocí jednoduchých ovládacích prvků pro správu Intune bez registrace zařízení. Obecné nastavení konfigurace aplikací poskytuje paritu nastavení správci můžou povolit při správě Outlooku pro iOS a Android na zaregistrovaných zařízeních. Další informace o nastavení aplikace Outlook najdete v tématu [nasazení aplikace Outlook pro iOS a nastavení konfigurace aplikací pro Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).


#### <a name="managed-home-screen-and-managed-settings-icons---4918107---"></a>Ikony spravované domovské obrazovky a spravovaného nastavení<!-- 4918107 -->
Ikona spravované aplikace na domovské obrazovce a ikona **spravovaného nastavení** se aktualizovaly. Spravovaná aplikace pro domovskou obrazovku se používá jenom u zařízení zaregistrovaných v Intune jako vyhrazená zařízení s Androidem Enterprise (AE) a provozovaná v celoobrazovkovém režimu s více aplikacemi. Další informace o spravované aplikaci pro domovskou obrazovku najdete v tématu [Konfigurace aplikace pro domovskou obrazovku spravované Microsoftem pro Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### <a name="android-device-policy-on-android-enterprise-dedicated-devices---4918136---"></a>Zásady zařízení s Androidem na vyhrazených zařízeních s Androidem Enterprise<!-- 4918136 -->
Přístup k aplikaci zásad zařízení s Androidem můžete získat z obrazovky ladění aplikace pro správu domácí obrazovky. Spravovaná aplikace pro domovskou obrazovku se používá jenom u zařízení zaregistrovaných v Intune jako vyhrazená zařízení s Androidem Enterprise (AE) a provozovaná v celoobrazovkovém režimu s více aplikacemi. Další informace najdete v tématu [Konfigurace aplikace pro domovskou obrazovku spravované Microsoftem pro Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### <a name="ios-company-portal-updates---3902931---"></a>aktualizace pro iOS Portál společnosti<!-- 3902931 -->
Název vaší společnosti při výzvě ke správě aplikací pro iOS nahradí aktuální text "i.manage.microsoft.com". V případě, že se uživatel pokusí nainstalovat aplikaci pro iOS z Portál společnosti nebo když uživatelé povolí správu aplikace, uvidí například název společnosti namísto "i.manage.microsoft.com". Tato akce bude zahrnuta pro všechny zákazníky za několik následujících dní.

#### <a name="aad-and-app-on-android-enterprise-devices---3574267---"></a>AAD a aplikace na zařízeních s Androidem Enterprise<!-- 3574267 -->
Při připojování plně spravovaných zařízení s Androidem Enterprise se uživatelé teď při počátečním nastavení nového zařízení nebo obnovení továrního nastavení registrují s Azure Active Directory (AAD). Předtím, než se pro plně spravované zařízení dokončí, musí uživatel ručně spustit aplikaci Microsoft Intune a spustit registraci AAD. Když se teď uživatel při počátečním nastavení zaregistruje na domovské stránce zařízení, zařízení se zaregistruje i zaregistruje.

Kromě aktualizací AAD se teď podporují zásady ochrany aplikací Intune (aplikace) na plně spravovaných podnikových zařízeních s Androidem. Tato funkce bude k dispozici, jakmile ji nasadíme. Další informace najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise pomocí Intune](../apps/apps-add-android-for-work.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="use-applicability-rules-when-creating-windows-10-device-configuration-profiles----2549910-eeready------"></a>Při vytváření profilů konfigurace zařízení s Windows 10 použít pravidla použitelnosti <!-- 2549910 eeready    -->

Vytvoříte profily konfigurace zařízení s Windows 10 (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10** pro **pravidla použitelnosti**platformy >). V této aktualizaci můžete vytvořit **pravidlo použitelnosti** , aby se profil mohl vztahovat jenom na konkrétní edici nebo konkrétní verzi. Můžete například vytvořit profil, který povolí některá nastavení nástroje BitLocker. Po přidání profilu použijte pravidlo použitelnosti, aby se profil mohl vztahovat jenom na zařízení s Windows 10 Enterprise.

Pokud chcete přidat pravidlo použitelnosti, přečtěte si téma [pravidla použitelnosti](../configuration/device-profile-create.md#applicability-rules).

Platí pro: Windows 10 a novější

#### <a name="use-tokens-to-add-device-specific-information-in-custom-profiles-for-ios-and-macos-devices---3330008----"></a>Použití tokenů k přidání informací specifických pro zařízení v uživatelských profilech pro zařízení s iOS a macOS<!-- 3330008  -->
Pomocí vlastních profilů na zařízeních s iOS a macOS můžete nakonfigurovat nastavení a funkce, které nejsou integrované do Intune (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** nebo **MacOS** pro Platform > **Custom** pro typ profilu). V této aktualizaci můžete do souborů `.mobileconfig` přidat tokeny a přidat informace specifické pro zařízení. Můžete například přidat `Serial Number: {{serialnumber}}` do konfiguračního souboru, aby se zobrazilo sériové číslo zařízení.

Pokud chcete vytvořit vlastní profil, přečtěte si téma [vlastní nastavení pro iOS](../configuration/custom-settings-ios.md) nebo [MacOS vlastní nastavení](../configuration/custom-settings-macos.md).

Platí pro:
- iOS
- macOS

#### <a name="new-configuration-designer-when-creating-an-oemconfig-profile-for-android-enterprise---3712769-----"></a>Nový Návrhář konfigurace při vytváření profilu OEMConfig pro Android Enterprise<!-- 3712769   -->
V Intune můžete vytvořit konfigurační profil zařízení, který používá aplikaci OEMConfig (konfigurace zařízení > Profily > vytvořit profil > Android Enterprise for Platform > OEMConfig pro typ profilu). Když to uděláte, otevře se Editor JSON se šablonou a hodnotami, které můžete změnit. 

Tato aktualizace obsahuje návrháře konfigurace s vylepšeným uživatelským prostředím, které zobrazuje podrobnosti vložené do aplikace včetně nadpisů, popisů a dalších. Editor JSON je stále k dispozici a zobrazuje všechny změny, které provedete v Návrháři konfigurace.

Pokud chcete zobrazit aktuální nastavení, přejděte na [používání a Správa zařízení s Androidem Enterprise pomocí OEMConfig](../configuration/android-oem-configuration-overview.md).

Platí pro: Android Enterprise

#### <a name="updated-ui-for-configuring-windows-hello---4089576--------------"></a>Aktualizované uživatelské rozhraní pro konfiguraci Windows Hello<!-- 4089576            -->
Aktualizovali jsme konzolu, ve které [nakonfigurujete Intune tak, aby používala Windows Hello pro firmy](../protect/windows-hello.md). Všechna nastavení konfigurace jsou nyní k dispozici ve stejném podokně konzoly, kde povolíte podporu pro Windows Hello.

#### <a name="intune-powershell-sdk---4924113---"></a>Sada Intune PowerShell SDK<!-- 4924113 --> 
Sada Intune PowerShell SDK, která poskytuje podporu pro rozhraní Intune API prostřednictvím Microsoft Graph, se aktualizovala na verzi 6.1907.1.0. Sada SDK teď podporuje následující:
- Funguje s Azure Automation.
- Podporuje operace čtení jenom pro aplikace. 
- Podporuje popisné zkrácené názvy jako aliasy.
- Vyhovuje konvencím pojmenování PowerShellu. Konkrétně byl parametr `PSCredential` (na rutině `Connect-MSGraph`) přejmenován na `Credential`.
- Při použití rutiny `Invoke-MSGraphRequest` podporuje Ruční určení hodnoty hlavičky `Content-Type`.

Další informace najdete v tématu [sada PowerShell SDK pro Microsoft Intune Graph API](https://www.powershellgallery.com/packages/Microsoft.Graph.Intune).

#### <a name="manage-filevault-for-macos----3858502--4557986--1210104----"></a>Správa trezoru pro macOS<!--  3858502 + 4557986 + 1210104  -->
Pomocí Intune můžete [Spravovat šifrování klíčů trezoru úložiště pro zařízení MacOS](../protect/encrypt-devices.md). K šifrování zařízení použijte konfigurační profil zařízení Endpoint Protection.

Naše podpora pro trezor souborů obsahuje šifrování nešifrovaných zařízení, v úschově zařízení pro osobní obnovení, automatické nebo ruční střídání osobních šifrovacích klíčů a načtení klíčů pro podniková zařízení. Koncoví uživatelé můžou k získání osobního obnovovacího klíče pro svá zašifrovaná zařízení použít taky web Portál společnosti.

Také jsme rozšířili sestavu šifrování tak, aby obsahovala informace o souběžných informacích [o trezoru úložiště](../protect/encryption-monitor.md) pro BitLocker, takže můžete zobrazit všechny podrobnosti o šifrování zařízení na jednom místě.

### <a name="new-office-windows-and-onedrive-settings-in-windows-10-administrative-templates----3510695---"></a>Nové nastavení Office, Windows a OneDrivu v šablonách pro správu Windows 10 <!-- 3510695 -->

V Intune můžete vytvořit šablony pro správu, které napodobují místní správu zásad skupiny ( > **profily** pro**správu zařízení** > **vytvořit profil** > **Windows 10 a novější** pro **šablonu** pro typ profilu >).

Tato aktualizace zahrnuje další nastavení Office, Windows a OneDrivu, která můžete přidat do šablon. S těmito novými nastaveními teď můžete nakonfigurovat více než 2500 nastavení, která jsou na bázi 100% cloudu.

Další informace o této funkci najdete v tématu [použití šablon Windows 10 ke konfiguraci nastavení zásad skupiny v Intune](../configuration/administrative-templates-windows.md).

Platí pro: Windows 10 a novější

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="updates-for-enrollment-restrictions---2871968---"></a>Aktualizace pro omezení registrace<!-- 2871968 -->
Byla aktualizována omezení registrace pro nové klienty, aby byly ve výchozím nastavení povoleny pracovní profily Android Enterprise. Stávající klienti nebudou mít žádné změny. Pokud chcete používat pracovní profily Android Enterprise, musíte [svůj účet Intune připojit k vašemu spravovanému účtu Google Play](../enrollment/connect-intune-android-enterprise.md).

#### <a name="ui-updates-for-apple-enrollment-and-enrollment-restrictions--4089575-4089579----"></a>Aktualizace uživatelského rozhraní pro registrace Apple a omezení registrace<!--4089575, 4089579  -->
Oba následující procesy používají uživatelské rozhraní ve stylu Průvodce:
- Registrace zařízení Apple. Další informace najdete v tématu [Automatická registrace zařízení s iOS pomocí program registrace zařízení společnosti Apple](../enrollment/device-enrollment-program-enroll-ios.md).
- Vytvoření omezení registrace. Další informace najdete v tématu [Nastavení omezení registrace](../enrollment/enrollment-restrictions-set.md).

#### <a name="handling-pre-configuration-of-corporate-device-identifiers-for-android-q-devices---4711509-----"></a>Zpracování předběžné konfigurace identifikátorů podnikových zařízení pro zařízení s Androidem Q<!-- 4711509   -->
V Androidu Q (v10 za účelem) bude Google odebrat možnost agentů MDM na starších zařízeních s Androidem spravovaná (Správce zařízení), aby shromáždila informace o identifikátoru zařízení.  Intune obsahuje funkci, která správcům IT umožňuje [předem nakonfigurovat seznam sériových čísel zařízení nebo IMEI](../enrollment/corporate-identifiers-add.md#identify-corporate-owned-devices-with-imei-or-serial-number) , aby tato zařízení mohla automaticky označovat jako vlastněná společností. Tato funkce nebude fungovat pro zařízení s Androidem Q, která jsou spravovaná správcem zařízení.  Bez ohledu na to, jestli se sériové číslo nebo IMEI zařízení nahraje, se při registraci v Intune vždycky považuje za osobní.  Po registraci můžete vlastnictví ručně přepínat na podnik.  To má vliv pouze na nové registrace a stávající zaregistrovaná zařízení ovlivněna nebudou.  Tato změna nemá vliv na zařízení s Androidem spravovaná pomocí pracovních profilů a bude dál fungovat, jak ještě dnes.  Zařízení se systémem Android Q zaregistrovaná jako správce zařízení už navíc nebudou moct v konzole Intune hlásit sériové číslo nebo IMEI jako vlastnosti zařízení.

#### <a name="icons-have-changed-for-android-enterprise-enrollments-work-profile-dedicated-devices-and-fully-managed-devices---4977730---"></a>Změnily se ikony pro registrace Android Enterprise (pracovní profil, vyhrazená zařízení a plně spravovaná zařízení).<!-- 4977730 -->
Změnili jsme ikony profilů registrace pro Android Enterprise. Pokud chcete zobrazit nové ikony, přejděte na **Intune** > **registrace** > **registraci v Androidu** > v části **profily zápisu**.

#### <a name="windows-diagnostic-data-collection-change---4113859---"></a>Změna shromažďování diagnostických dat Windows<!-- 4113859 -->
Výchozí hodnota pro shromažďování diagnostických dat se změnila pro zařízení s Windows 10 verze 1903 a novější. Počínaje systémem Windows 10 1903 je shromažďování diagnostických dat ve výchozím nastavení povoleno. Diagnostická data Windows jsou důležitá technická data ze zařízení s Windows, která se týkají zařízení a způsobu provádění Windows a souvisejícího softwaru. Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization). V případě, že se v profilu autopilotu pomocí [System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)nenastavuje jinak, zařízení autopilotu se také přihlásí do "plné" telemetrie.

#### <a name="windows-autopilot-reset-removes-the-devices-primary-user---4156123---"></a>Resetování Windows autopilotu odebere primárního uživatele zařízení.<!-- 4156123 -->
Když se na zařízení používá resetování autopilotního projektu, primární uživatel zařízení se odebere. Další uživatel, který se přihlásí po obnovení, se nastaví jako primární uživatel. Tato funkce bude zahrnuta pro všechny zákazníky za několik následujících dní.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="improve-device-location---3855417----"></a>Vylepšit umístění zařízení<!-- 3855417  -->
Pomocí akce **Najít zařízení** můžete přiblížit přesnou souřadnici zařízení. Další informace o vyhledání ztracených zařízení s iOS najdete v tématu [vyhledání ztracených zařízení s iOS](../remote-actions/device-locate.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="advanced-settings-for-windows-defender-firewall--public-preview----1311949-------"></a>Rozšířená nastavení pro firewall v programu Windows Defender (Public Preview)<!--  1311949     -->  
Pomocí Intune můžete spravovat [vlastní pravidla brány firewall jako součást profilu konfigurace zařízení](../protect/endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices) pro službu Endpoint Protection ve Windows 10. Pravidla mohou určovat příchozí a odchozí chování aplikací, síťových adres a portů. 

#### <a name="updated-ui-for-managing-security-baselines---4091125-------"></a>Aktualizované uživatelské rozhraní pro správu standardních hodnot zabezpečení<!-- 4091125     -->
Aktualizovali jsme [prostředí pro vytváření a úpravy](../protect/security-baselines.md#create-the-profile) v konzole Intune pro naše základní směry zabezpečení. Změny zahrnují:

Jednodušší formát ve stylu průvodce, který je zúžený na jedno okno. v jednom okně. Tento nový návrh se zapíná s oknem neustálému zvětšování, který vyžaduje, aby odborníci na IT přešli do několika samostatných podoken.  
Nyní můžete vytvářet přiřazení v rámci prostředí vytváření a úprav, aniž byste se museli vracet později, aby bylo možné přiřadit směrné plány. Přidali jsme souhrn nastavení, která můžete zobrazit před vytvořením nového směrného plánu a úpravou stávajícího. Při úpravách zobrazuje souhrn pouze seznam položek, které jsou nastaveny v rámci jedné kategorie upravovaných vlastností.

<!-- ########################## -->
## <a name="june-2019"></a>Červeně 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="configure-which-browser-is-allowed-to-link-to-organization-data---3145939---"></a>Nakonfigurovat, který prohlížeč smí propojit s daty organizace<!-- 3145939 -->
Zásady Intune App Protection (aplikace) na zařízeních s Androidem a iOS teď umožňují přenášet webové odkazy organizace na konkrétní prohlížeč mimo Intune Managed Browser nebo Microsoft Edge.  Další informace o aplikaci najdete v tématu [co jsou zásady ochrany aplikací?](../apps/app-protection-policy.md).

#### <a name="all-apps-page-identifies-onlineoffline-microsoft-store-for-business-apps--4089647---"></a>Stránka všechny aplikace identifikuje online nebo offline Microsoft Store pro obchodní aplikace.<!--4089647 -->
Stránka **všechny aplikace** teď obsahuje popis, který identifikuje aplikace Microsoft Store pro firmy (MSFB) jako online nebo offline aplikace. Každá aplikace MSFB teď obsahuje příponu pro **online** nebo **offline**. Stránka s podrobnostmi o aplikaci zahrnuje také **typ licence** a **podporuje instalaci kontextu zařízení** (pouze offline licencované aplikace).

#### <a name="company-portal-app-on-windows-shared-devices--4393553---"></a>Portál společnosti aplikace na sdílených zařízeních s Windows<!--4393553 -->
Uživatelé teď můžou k aplikaci Portál společnosti přistupovat na sdílených zařízeních se systémem Windows. Koncovým uživatelům se na dlaždici zařízení zobrazí **sdílený** popisek. To platí pro Windows Portál společnosti app verze 10.3.45609.0 a novější.

#### <a name="view-all-installed-apps-from-new-company-portal-web-page---4224326---"></a>Zobrazit všechny nainstalované aplikace z nové Portál společnosti webové stránky<!-- 4224326 -->
Stránka Portál společnosti nové **nainstalované aplikace** na webu obsahuje seznam všech spravovaných aplikací (požadovaných i dostupných), které jsou nainstalovány na zařízeních uživatele. Kromě typu přiřazení uživatelé uvidí vydavatele aplikace, datum publikování a aktuální stav instalace. Pokud jste neudělali žádné aplikace, které uživatelé potřebují nebo nejsou k dispozici, zobrazí se zpráva s vysvětlením, že nebyly nainstalovány žádné aplikace společnosti. Pokud chcete zobrazit novou stránku na webu, přejděte na [web portál společnosti](https://portal.manage.microsoft.com) a klikněte na **nainstalované aplikace**.  

#### <a name="new-view-lets-app-users-see-all-managed-apps-installed-on-device---2352913---"></a>Nové zobrazení umožňuje uživatelům aplikace zobrazit všechny spravované aplikace nainstalované na zařízení.<!-- 2352913 -->  
Aplikace Portál společnosti pro Windows teď obsahuje seznam všech spravovaných aplikací (požadovaných i dostupných), které jsou nainstalované na zařízení uživatele. Uživatelé můžou také zobrazit pokusy o instalaci aplikací a jejich aktuální stavy. Pokud jste neudělali aplikace, které uživatelé potřebují nebo k nim nejsou k dispozici, zobrazí se zpráva s vysvětlením, že nebyly nainstalovány žádné aplikace společnosti. Chcete-li zobrazit nové zobrazení, přejděte do navigačního podokna Portál společnosti a vyberte **aplikace** > **nainstalované aplikace**.

#### <a name="new-features-in-microsoft-intune-app"></a>Nové funkce v aplikaci Microsoft Intune App
Přidali jsme nové funkce do aplikace Microsoft Intune (Preview) pro Android. Uživatelé na plně spravovaných zařízeních s Androidem teď můžou:  

* Umožňuje zobrazit a spravovat zařízení, která zaregistrovali prostřednictvím aplikace Portál společnosti Intune nebo Microsoft Intune.
* Pro podporu se obraťte na svou organizaci.
* Poslat svůj názor Microsoftu.
* Zobrazit podmínky a ujednání, pokud je nastavila jejich organizace.

#### <a name="new-sample-apps-showing-intune-sdk-integration-available-on-github---2653471---"></a>Nové ukázkové aplikace ukazující integraci sady Intune SDK dostupnou na GitHubu<!-- 2653471 -->
Účet GitHub msintuneappsdk přidal nové ukázkové aplikace pro iOS (SWIFT), Android, Xamarin. iOS, Xamarin Forms a Xamarin. Android. Tyto aplikace jsou určeny k doplnění naší stávající dokumentace a poskytnutí ukázek, jak integrovat sadu Intune APP SDK do vašich vlastních mobilních aplikací. Pokud jste vývojář aplikací, který potřebuje další pokyny pro sadu Intune SDK, přečtěte si následující propojené ukázky:
- [Chat](https://github.com/msintuneappsdk/Chatr-Sample-Intune-iOS-App) – nativní aplikace pro zasílání rychlých zpráv pro iOS (SWIFT), která pro zprostředkované ověřování používá službu Azure Active Directory Authentication Library (ADAL).
- [Tasker](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App) – nativní aplikace seznamu úkolů pro Android, která používá ADAL pro zprostředkované ověřování.
- [Tasker](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Xamarin-Android-Apps) – aplikace seznamu úkolů Xamarin. Android, která používá ADAL pro zprostředkované ověřování, toto úložiště má také aplikaci Xamarin. Forms.
- [Ukázková aplikace Xamarin. iOS](https://github.com/msintuneappsdk/sample-intune-xamarin-ios) – ukázková aplikace Barebones Xamarin. iOS


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="configure-settings-for-kernel-extensions-on-macos-devices---2043024---"></a>Konfigurace nastavení pro rozšíření jádra na zařízeních macOS<!-- 2043024 -->
Na zařízeních macOS můžete vytvořit konfigurační profil zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > zvolit **MacOS** pro platformu). Tato aktualizace zahrnuje novou skupinu nastavení, která vám umožní nakonfigurovat a používat na svých zařízeních rozšíření jádra. Můžete přidat konkrétní rozšíření nebo povolíte všechna rozšíření od konkrétního partnera nebo vývojáře.

Další informace o této funkci najdete v tématu [Přehled rozšíření jádra](../configuration/kernel-extensions-overview-macos.md) a [nastavení rozšíření jádra](../configuration/kernel-extensions-settings-macos.md).

Platí pro: macOS 10.13.2 a novější

#### <a name="apps-from-the-store-only-setting-for-windows-10-devices-includes-more-configuration-options---2697002---"></a>Aplikace z nastavení jenom pro Store pro zařízení s Windows 10 obsahují další možnosti konfigurace.<!-- 2697002 -->
Když vytváříte profil omezení zařízení pro zařízení s Windows, můžete použít **aplikace z nastavení jenom úložiště** , aby uživatelé mohli instalovat jenom aplikace z Windows App Storu (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** pro > **omezení zařízení** pro typ profilu). V této aktualizaci je toto nastavení rozšířeno na podporu více možností.

Nové nastavení zobrazíte tak, že přejdete na [nastavení zařízení s Windows 10 (a novější) a povolíte nebo zakážete funkce](../configuration/device-restrictions-windows-10.md#app-store).

Platí pro: Windows 10 a novější

#### <a name="deploy-multiple-zebra-mobility-extensions-device-profiles-to-a-device-same-user-group-or-same-devices-group---4089955---"></a>Nasazení více profilů zařízení rozšíření Zebra mobility na zařízení, stejnou skupinu uživatelů nebo stejnou skupinu zařízení<!-- 4089955 -->
V Intune můžete použít rozšíření Zebra mobility (MX) v profilu konfigurace zařízení k přizpůsobení nastavení pro Zebra zařízení, která nejsou integrovaná do Intune. V současné době můžete nasadit jeden profil na jedno zařízení. V této aktualizaci můžete nasadit několik profilů do:
- Stejná skupina uživatelů
- Stejná skupina zařízení
- Jedno zařízení

[Používání a Správa zařízení Zebra pomocí rozšíření Zebra mobility v Microsoft Intune](../configuration/android-zebra-mx-overview.md) ukazuje, jak používat MX v Intune.

Platí pro: Android

#### <a name="some-kiosk-settings-on-ios-devices-are-set-using-block-replacing-allow---4404075----"></a>Některá nastavení veřejného terminálu na zařízeních s iOS se nastavují pomocí Block, kde se nahrazuje "povolení".<!-- 4404075  -->
Když vytvoříte profil omezení zařízení na zařízeních s iOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro > **omezení zařízení** pro typ profilu > veřejný **terminál**), nastavíte **automaticky zámek**, **přepínač vyzvánění**, **otočení obrazovky**, **tlačítko režimu spánku obrazovky**a **tlačítka hlasitosti**.

V této aktualizaci jsou hodnoty **zablokované** (blokuje funkci) a **nejsou nakonfigurované** (umožňuje funkci). Nastavení zobrazíte tak, že přejdete na [nastavení zařízení s iOS a povolíte nebo zakážete funkce](../configuration/device-restrictions-ios.md#kiosk).

Platí pro: iOS

#### <a name="use-face-id-for-password-authentication-on-ios-devices---4490704---"></a>Použití ID obličeje pro ověřování hesla na zařízeních s iOS<!-- 4490704 -->
Když vytvoříte profil omezení zařízení pro zařízení s iOS, můžete pro heslo použít otisk prstu. V této aktualizaci nastavení hesla otisku prstu taky povoluje rozpoznávání obličeje (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro > **omezení zařízení** pro typ profilu > **heslo**). V důsledku toho se změnila následující nastavení:

- **Odemčení otiskem prstu** je teď **dotykové ID a odemknutí ID obličeje**.
- **Úprava otisku prstu (jenom pod dohledem)** je teď **dotykové ID a úprava ID obličeje (jenom pod dohledem)** .

ID obličeje je dostupné v iOS 11,0 a novějších verzích. Nastavení zobrazíte tak, že přejdete na [nastavení zařízení s iOS a povolíte nebo zakážete funkce využívající Intune](../configuration/device-restrictions-ios.md#password).

Platí pro: iOS

#### <a name="restricting-gaming-and-app-store-features-on-ios-devices-is-now-dependent-on-ratings-region---4593948---"></a>Omezení her a funkcí pro obchod s aplikacemi na zařízeních s iOS je teď závislé na oblasti hodnocení.<!-- 4593948 -->
Na zařízeních se systémem iOS můžete povolit nebo zakázat funkce týkající se her, App Storu a zobrazení dokumentů (**Konfigurace zařízení** > **profily** > **vytvoření profilu** > **iOS** pro > **omezení zařízení** pro typ profilu > **App Store, zobrazování dokumentů, hry**). Můžete také zvolit oblast hodnocení, například USA.

V této aktualizaci se funkce **aplikace** přesune, aby byla podřízená **oblasti hodnocení**a byla závislá na **oblasti hodnocení**. Nastavení zobrazíte tak, že přejdete na [nastavení zařízení s iOS a povolíte nebo zakážete funkce využívající Intune](../configuration/device-restrictions-ios.md#app-store-doc-viewing-gaming).

Platí pro: iOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="windows-autopilot-support-for-hybrid-azure-ad-join---4809146--"></a>Podpora Windows autopilotu pro hybridní službu Azure AD JOIN<!-- 4809146-->
Windows autopilot pro stávající zařízení teď podporuje hybridní připojení ke službě Azure AD (kromě stávající podpory Azure AD JOIN). Platí pro zařízení s Windows 10 verze 1809 a novější. Další informace najdete v tématu věnovaném [autopilotu Windows pro existující zařízení](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="see-the-security-patch-level-for-android-devices---4461911---"></a>Zobrazit úroveň opravy zabezpečení pro zařízení s Androidem<!-- 4461911 -->
Teď můžete zobrazit úroveň opravy zabezpečení pro zařízení s Androidem. Pokud to chcete udělat, vyberte **zařízení** > **Intune** > **všechna zařízení** > vyberte **hardware**> zařízení.
Úroveň opravy je uvedena v části **operační systém** .

#### <a name="assign-scope-tags-to-all-managed-devices-in-a-security-group---3173810---"></a>Přiřadit značky oboru všem spravovaným zařízením ve skupině zabezpečení<!-- 3173810 -->
Nyní můžete přiřadit značky oboru ke skupině zabezpečení a všechna zařízení ve skupině zabezpečení budou také přidružena k těmto značkám oboru. Všechna zařízení v těchto skupinách budou mít také přiřazenou značku oboru. Tagy oboru nastavené touto funkcí přepíší sadu značek oboru s aktuálním tokem značek oboru zařízení. Další informace najdete v tématu [použití značek RBAC a Scope pro distribuci](scope-tags.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Zabezpečení zařízení

#### <a name="use-keyword-search-with-security-baselines------"></a>Použití hledání klíčových slov pomocí standardních hodnot zabezpečení<!--  -->
Když vytváříte nebo upravujete [profily standardních hodnot zabezpečení](../protect/security-baselines.md#create-the-profile), můžete zadat klíčová slova na novém panelu *hledání* a vyfiltrovat dostupné skupiny nastavení na ty, které obsahují vaše kritéria hledání.

#### <a name="the-security-baselines-feature-is-now-generally-available---3785395---"></a>Funkce standardních hodnot zabezpečení je teď všeobecně dostupná.<!-- 3785395 -->
Funkce **standardních hodnot zabezpečení** není ve verzi Preview a je teď obecně dostupná (GA).  To znamená, že funkce je připravena k použití v produkčním prostředí. Jednotlivé základní šablony ale mohou zůstat ve verzi Preview a jsou vyhodnoceny a vydány pro GA na základě vlastních plánů.

#### <a name="the-mdm-security-baseline-template-is-now-generally-available---3794072-4217151--3534649---"></a>Šablona standardních hodnot zabezpečení MDM je teď všeobecně dostupná.<!-- 3794072, 4217151,  3534649 -->
Šablona základní hodnoty zabezpečení MDM se přesunula z verze Preview a teď je všeobecně dostupná (GA). Šablona GA je **pro květen 2019**označena jako základní hodnota zabezpečení MDM.  Jedná se o novou šablonu, která není upgradem z verze Preview.  Jako novou šablonu budete muset zkontrolovat nastavení, která [obsahuje](../protect/security-baseline-settings-mdm.md), a pak vytvořit nové profily, pomocí kterých šablonu nasadíte do svého zařízení. Další šablony standardních hodnot zabezpečení mohou zůstat ve verzi Preview. Seznam dostupných směrných plánů najdete v tématu [dostupné standardní hodnoty zabezpečení](../protect/security-baselines.md#available-security-baselines).  

Kromě nové šablony obsahuje *základní plán zabezpečení MDM pro květen 2019* dvě nastavení, která jsme nedávno oznámili v našem vývojovém článku:  
- Nad zámkem: hlas – aktivovat aplikace z uzamčené obrazovky  
- DeviceGuard: při příštím restartování zařízení použijte zabezpečení na základě virtualizace (VBS).  

*Základní hodnota zabezpečení MDM pro květen 2019* obsahuje také přidání několika nových nastavení, odebrání ostatních a revizi výchozí hodnoty jednoho nastavení. Podrobný seznam změn z verze Preview na GA najdete v tématu **co se změnilo v nové šabloně**.

#### <a name="security-baseline-versioning---3194322---"></a>Základní verze zabezpečení<!-- 3194322 -->
Standardní hodnoty zabezpečení pro Intune podporují správu verzí. V rámci této podpory platí, že při vydání nových verzí jednotlivých standardních hodnot zabezpečení můžete aktualizovat stávající základní profily zabezpečení tak, aby používaly novější základní verzi bez nutnosti opětovného vytvoření a nasazení nového směrného plánu od začátku. Kromě toho můžete v konzole Intune zobrazit informace o jednotlivých standardních hodnotách, jako je počet jednotlivých profilů, u kterých používáte základní hodnoty, kolik z různých základních verzí vaše profily používá a kdy nejnovější vydání konkrétního zabezpečení. směrný plán byl.  Další informace najdete v tématu **základní hodnoty zabezpečení**.

#### <a name="the-use-security-keys-for-sign-in-setting-has-moved---4501151---"></a>Bylo přesunuto nastavení použít klíče zabezpečení pro přihlášení.<!-- 4501151 -->
Nastavení konfigurace zařízení pro ochranu identity s názvem **použít klíče zabezpečení pro přihlášení** se už nenašlo jako dílčí nastavení *Konfigurace Windows Hello pro firmy*. Teď je to nastavení nejvyšší úrovně, které je vždycky dostupné, a to i v případě, že nepovolíte používání Windows Hello pro firmy. Další informace najdete v tématu [Identita Protection](../protect/identity-protection-windows-settings.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="new-permissions-for-assigned-group-admins---4504437-----"></a>Nová oprávnění pro přiřazené správce skupiny<!-- 4504437   -->
Integrovaná role školního správce Intune teď má oprávnění k vytváření, čtení, aktualizaci a odstraňování (CRUD) pro spravované aplikace. Tato aktualizace znamená, že pokud jste přihlášeni jako správce skupiny v Intune for Education, můžete teď vytvářet, zobrazovat, aktualizovat a odstraňovat MDM Push Certificate iOS, tokeny MDM serveru iOS a tokeny VPP pro iOS společně se [všemi stávajícími oprávněními](https://docs.microsoft.com/intune-education/group-admin-delegate#group-admin-permissions), která máte. Pokud chcete některou z těchto akcí provést, přečtěte si **Nastavení tenanta** > **správu zařízení s iOS**.  

#### <a name="applications-can-use-the-graph-api-to-call-read-operations-without-user-credentials---4655885---"></a>Aplikace můžou použít Graph API k volání operací čtení bez přihlašovacích údajů uživatele.<!-- 4655885 -->
Aplikace můžou volat Intune Graph API operace čtení pomocí identity aplikace bez přihlašovacích údajů uživatele. Další informace o přístupu k rozhraní Microsoft Graph API pro Intune najdete [v tématu práce s Intune v Microsoft Graph](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0).

#### <a name="apply-scope-tags-to-microsoft-store-for-business-apps---4392555---"></a>Použití značek oboru na Microsoft Store pro obchodní aplikace<!-- 4392555 -->
Pro Microsoft Store pro obchodní aplikace teď můžete použít značky oboru. Další informace o značkách oboru najdete v tématu [použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci](scope-tags.md).

<!-- ########################## -->
## <a name="may-2019"></a>Květen 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="reporting-for-potentially-harmful-apps-on-android-devices---4223162---"></a>Vytváření sestav pro potenciálně škodlivé aplikace na zařízeních s Androidem<!-- 4223162 -->
Intune teď poskytuje další informace o potenciálně škodlivých aplikacích na zařízeních s Androidem. 

#### <a name="windows-company-portal-app---3316993---"></a>Aplikace Portál společnosti pro Windows<!-- 3316993 -->
Aplikace pro Windows Portál společnosti teď bude mít novou stránku označenou jako **zařízení**. Na stránce **zařízení** se zobrazí koncoví uživatelé všechna zaregistrovaná zařízení. Uživatelům se tato změna v Portál společnosti uvidí, když používají verzi 10.3.4291.0 a novější. Informace o konfiguraci Portál společnosti naleznete v tématu [How to Configure a Microsoft Intune portál společnosti App](../apps/company-portal-app.md).

#### <a name="intune-policies-update-authentication-method-and-company-portal-app-installation---1927359----"></a>Zásady služby Intune aktualizují metodu ověřování a instalaci aplikace Portál společnosti.<!-- 1927359  -->
V zařízeních, která jsou už zaregistrovaná prostřednictvím pomocníka s nastavením prostřednictvím některého z metod registrace podnikových zařízení společnosti Apple, Intune už nebude podporovat Portál společnosti, když je ručně nainstalují koncoví uživatelé z App Storu. Tato změna platí pouze v Apple Pomocníka s nastavením ověřování během registrace. Tato změna ovlivní také pouze zařízení s Iosem zaregistrovaná prostřednictvím:  
* Apple configurator
* Obchodní ředitel společnosti Apple
* Apple School Manager
* Program registrace zařízení Apple (DEP)

Pokud je uživatelé nainstalovat aplikaci portál společnosti z App storu a potom se pokuste registraci těchto zařízení jeho prostřednictvím, dojde k chybě. U těchto zařízení se očekává, že bude používat jenom Portál společnosti, když ho služba Intune po registraci automaticky dokončí. Profily registrace v Intune na portálu Azure portal bude aktualizován, takže můžete určit, jak ověřovat zařízení a pokud se zobrazí v aplikaci portál společnosti. Pokud chcete, aby uživatelé zařízení DEP budou používat aplikaci portál společnosti, musíte zadat předvolby v registrační profil. 

Kromě toho se odebírá obrazovka **identifikace zařízení** v iOS portál společnosti. Proto správci, kteří chtějí povolit podmíněný přístup nebo nasazovat firemní aplikace, musí aktualizovat profil zápisu DEP. Tento požadavek platí jenom v případě, že se registrace DEP ověřuje pomocí Pomocníka s nastavením. V takovém případě musíte Portál společnosti do zařízení vložit. Provedete to tak, že v **Intune** > **registraci zařízení** > zápisu **Apple** > **tokeny programu registrace** > **zvolíte profily > profilů** > vyberte profil > **vlastnosti** > nastavte **instalovat portál společnosti** na **Ano**.

Pokud chcete Portál společnosti nainstalovat do již zaregistrovaných zařízení DEP, budete muset přejít na > klientských aplikací Intune a vložit ho jako spravovanou aplikaci se zásadami konfigurace aplikace. 

#### <a name="configure-how-end-users-update-a-line-of-business-lob-app-using-an-app-protection-policy---3568384---"></a>Konfigurace způsobu, jakým koncoví uživatelé aktualizují obchodní aplikaci (LOB) pomocí zásad ochrany aplikací<!-- 3568384 -->
Teď můžete nakonfigurovat, kde můžou koncoví uživatelé získat aktualizovanou verzi obchodní aplikace (LOB). Koncovým uživatelům se tato funkce zobrazí v dialogovém okně pro podmíněné spuštění podmíněné **verze aplikace** , ve kterém se koncovým uživatelům zobrazí výzva k aktualizaci na minimální verzi aplikace LOB. Tyto podrobnosti o aktualizaci musíte zadat v rámci zásad ochrany aplikací LOB (aplikace). Tato funkce je dostupná v iOS a Androidu. V systému iOS Tato funkce vyžaduje, aby byla aplikace integrovaná (nebo zabalená pomocí nástroje pro zabalení) se sadou Intune SDK pro iOS v. 10.0.7 nebo vyšší. V Androidu by tato funkce vyžadovala nejnovější Portál společnosti. Pokud chcete nakonfigurovat, jak koncový uživatel aktualizuje obchodní aplikaci, potřebuje, aby se do této aplikace poslala zásada konfigurace spravované aplikace s klíčem, `com.microsoft.intune.myappstore`. Hodnota odeslané bude určovat, ze kterého Storu bude koncový uživatel aplikaci stahovat. Pokud je aplikace nasazená prostřednictvím Portál společnosti, musí být hodnota `CompanyPortal`. Pro jakékoli jiné úložiště musíte zadat úplnou adresu URL.

#### <a name="intune-management-extension-powershell-scripts---3734186----"></a>Skripty PowerShellu pro rozšíření správy Intune<!-- 3734186  -->
Skripty PowerShellu můžete nakonfigurovat tak, aby se spouštěly s oprávněními správce uživatele v zařízení. Další informace najdete v tématu [použití skriptů PowerShellu na zařízeních s Windows 10 v Intune a ve](../apps/intune-management-extension.md) [správě aplikací Win32](../apps/app-management.md).

#### <a name="android-enterprise-app-management---4459905---"></a>Správa firemních aplikací pro Android<!-- 4459905 -->
Aby správci IT usnadnili konfiguraci a používání správy Android Enterprise managementu, Intune do konzoly pro správu Intune automaticky přidá čtyři běžné aplikace pro Android Enterprise. Čtyři aplikace pro Android Enterprise jsou tyto aplikace:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** – používá se pro plně spravované scénáře pro Android Enterprise.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** – vám pomůže se přihlašovat k vašim účtům, pokud použijete dvojúrovňové ověřování.
- **[Portál společnosti Intune](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** – používá se pro scénáře zásad ochrany aplikací (App) a Android Enterprise Work Profile.
- [Spravovaná Domovská obrazovka](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise) – používá se pro scénáře podnikových scénářů nebo veřejného terminálu pro Android.

Dříve museli správci IT v rámci instalace ručně najít a schválit tyto aplikace v rámci [spravovaného Google Play Storu](https://play.google.com/store/apps) . Tato změna odstraní výše popsané kroky, aby zákazníci usnadnili používání Enterprise managementu v Androidu, aby je bylo snazší a rychlejší.

Správci uvidí tyto čtyři aplikace automaticky přidané do jejich seznamu aplikací Intune v době, kdy poprvé připojí svého tenanta Intune ke spravovaným Google Play. Další informace najdete v tématu [připojení účtu Intune ke spravovanému účtu Google Play](../enrollment/connect-intune-android-enterprise.md). Pro klienty, kteří už připojili svého tenanta nebo kteří už používají Android Enterprise, nemusíte dělat žádné správce. Tyto čtyři aplikace se automaticky zobrazí do 7 dnů od dokončení zavedení služby květen 2019.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="updated-pfx-certificate-connector-for-microsoft-intune---1533038---"></a>Aktualizovaný konektor certifikátu PFX pro Microsoft Intune<!-- 1533038 -->
Vydali jsme aktualizaci [konektoru PFX Certificate Connector pro Microsoft Intune](../protect/certficates-pfx-configure.md#whats-new-for-connectors) , která řeší problém, kdy se stávající certifikáty PFX budou dál zpracovávat, což způsobí, že konektor přestane zpracovávat nové požadavky.

#### <a name="intune-security-tasks-for-defender-atp-in-public-preview---3208597---"></a>Úkoly zabezpečení Intune pro program Defender ATP (ve verzi Public Preview)<!-- 3208597 -->
Ve verzi Public Preview můžete pomocí Intune spravovat [úlohy zabezpečení pro Microsoft Defender Advanced Threat Protection (ATP)](../protect/atp-manage-vulnerabilities.md). Tato integrace s ATP a přináší přístup založený na riziku pro zjišťování, stanovení priorit a nápravu chyb zabezpečení koncových bodů a chybných konfigurací a zároveň zkracuje dobu mezi zjišťováním a omezením jejich zmírnění.

#### <a name="check-for-a-tpm-chipset-in-a-windows-10-device-compliance-policy---3617671-----"></a>Zjištění sady čipů TPM v zásadách dodržování předpisů pro zařízení s Windows 10<!-- 3617671   -->
Mnoho zařízení s Windows 10 a novějším má čipové sady TPM (Trusted Platform Module). Tato aktualizace obsahuje nové nastavení dodržování předpisů, které kontroluje verzi čipu TPM v zařízení.

Toto nastavení popisuje [nastavení zásad dodržování předpisů pro Windows 10 a novější](../protect/compliance-policy-create-windows.md#device-security) .

Platí pro: Windows 10 a novější

#### <a name="prevent-end-users-from-modifying-their-personal-hotspot-and-disable-siri-server-logging-on-ios-devices---4097904-----"></a>Zabránit koncovým uživatelům v úpravách jejich osobního HotSpotu a zakázat přihlašování Siri serveru na zařízeních s iOS<!-- 4097904   -->  
Vytvoříte profil omezení zařízení na zařízení s iOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro **zařízení > omezení** pro typ profilu). Tato aktualizace obsahuje nová nastavení, která můžete nakonfigurovat:

- **Integrované aplikace**: protokolování na straně serveru pro příkazy Siri
- **Bezdrátové**: Změna uživatele osobní hotspotu (jenom pod dohledem)

Tato nastavení zobrazíte tak, že přejdete na [integrovaná nastavení aplikace pro iOS](../configuration/device-restrictions-ios.md#built-in-apps) a [nastavení bezdrátové sítě pro iOS](../configuration/device-restrictions-ios.md#wireless).

Platí pro: iOS 12,2 a novější

#### <a name="new-classroom-app-device-restriction-settings-for-macos-devices---4097905-----"></a>Nová nastavení omezení pro zařízení macOS v aplikaci učeben<!-- 4097905   --> 
Pro zařízení macOS můžete vytvořit profily konfigurace zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **MacOS** pro **omezení** platformy > pro typ profilu). Tato aktualizace zahrnuje nová nastavení aplikace učebny, možnost blokovat snímky obrazovky a možnost zakázat knihovnu fotografií iCloud.

Pokud chcete zobrazit aktuální nastavení, přejděte na [nastavení zařízení MacOS a povolte nebo omezte funkce pomocí Intune](../configuration/device-restrictions-macos.md).

Platí pro: macOS

#### <a name="the-ios-password-to-access-app-store-setting-is-renamed---4557891----"></a>Heslo pro iOS pro přístup k nastavení obchodu s aplikacemi se přejmenuje.<!-- 4557891  -->
**Heslo pro přístup k nastavení obchodu s aplikacemi** je přejmenované na **vyžadovat heslo pro úložiště iTunes pro všechny nákupy** (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro > **omezení zařízení** pro typ profilu > **App Store, zobrazování dokumentů a hry**).

Dostupná nastavení zobrazíte tak, že přejdete do [App Storu, zobrazení dokumentů a herního nastavení iOS](../configuration/device-restrictions-ios.md#app-store-doc-viewing-gaming).

Platí pro: iOS

#### <a name="microsoft-defender-advanced-threat-protection--baseline--preview----3754134---"></a>Směrný plán Microsoft Defender Advanced Threat Protection (Preview)<!--  3754134 -->
Přidali jsme náhled základní úrovně zabezpečení pro nastavení [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](../protect/security-baseline-settings-defender-atp.md) . Tato standardní hodnota je dostupná, když vaše prostředí splňuje požadavky na používání [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](../protect/advanced-threat-protection.md#prerequisites).

#### <a name="outlook-signature-and-biometric-settings-for--ios-and-android-devices---4050557---"></a>Podpis Outlooku a biometrické nastavení pro zařízení s iOS a Androidem<!-- 4050557 -->
Teď můžete určit, jestli je výchozí podpis povolený v Outlooku na zařízeních s iOS a Androidem. Kromě toho můžete zvolit, aby uživatelé mohli měnit nastavení biometriky v Outlooku v iOS.

#### <a name="network-access-control-nac-support-for-f5-access-for-ios-devices---4500808---"></a>Podpora NAC (Network Access Control) pro přístup F5 pro zařízení s iOS<!-- 4500808 -->
F5 vydala aktualizaci BIG-IP 13, která umožňuje funkci NAC pro přístup F5 v systému iOS v Intune. Chcete-li použít tuto funkci:

- Aktualizujte BIG-IP na 13.1.1.5 Refresh. BIG-IP 14 se nepodporuje.
- Integrujte BIG-IP s Intune for NAC. Postup v článku [Přehled: Konfigurace APM pro zařízení stav kontrol pomocí systémů správy koncových bodů](https://techdocs.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html).
- Zaškrtněte nastavení **povolit Access Control sítě (NAC)** v profilu sítě VPN v Intune.

Dostupná nastavení zobrazíte tak, že přejdete na [Konfigurace nastavení sítě VPN na zařízeních s iOS](../configuration/vpn-settings-ios.md).

Platí pro: iOS

#### <a name="updated-pfx-certificate-connector-for-microsoft-intune---doc-vso-1521237----"></a>Aktualizovaný konektor certifikátu PFX pro Microsoft Intune<!-- doc-vso 1521237  -->  
Vydali jsme aktualizaci [konektoru certifikátů PFX pro Microsoft Intune](../protect/certficates-pfx-configure.md#whats-new-for-connectors) , který předává interval dotazování od 5 minut do 30 sekund.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="autopilot-device-orderid-attribute-name-changed-to-group-tag----4659453---"></a>Název atributu KódObjednávky zařízení pro Autopilot se změnil na značku Group <!-- 4659453 -->

Aby byl název atributu **KódObjednávky** v zařízeních pro autopiloti intuitivnější, byl změněn na **značku Group**. Při použití CSV k nahrávání informací o zařízeních autopilotu je nutné použít značku skupiny jako záhlaví sloupce, nikoli ČísloObjednávky.  

#### <a name="windows-enrollment-status-page-esp-is-now-generally-available---3605348---"></a>Stránka stavu registrace systému Windows (ESP) je nyní obecně dostupná.<!-- 3605348 -->
Stránka stavu registrace je nyní mimo verzi Preview. Další informace najdete v tématu [nastavení stránky stavu registrace](../enrollment/windows-enrollment-status.md).

#### <a name="intune-user-interface-update---autopilot-enrollment-profile-creation---4593669---"></a>Aktualizace uživatelského rozhraní Intune – vytvoření profilu registrace autopilotu<!-- 4593669 -->
Uživatelské rozhraní pro vytvoření profilu registrace autopilotu se aktualizovalo tak, aby bylo zarovnané na styly uživatelského rozhraní Azure. Další informace najdete v tématu [Vytvoření profilu registrace autopilotu](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile). Další scénáře Intune se budou aktualizovat na tento nový styl uživatelského rozhraní.

#### <a name="enable-autopilot-reset-for-all-windows-devices---4225665---"></a>Povolit resetování autopilotu pro všechna zařízení s Windows<!-- 4225665 -->
Automatické vynulování pilotního nasazení teď funguje pro všechna zařízení s Windows, i když nejsou nakonfigurovaná na použití stránky stavu registrace. Pokud se stránka stavu registrace pro zařízení nenakonfigurovala při počáteční registraci zařízení, bude po přihlášení zařízení po přihlášení přímo na plochu. Synchronizace a zobrazení kompatibility v Intune může trvat až osm hodin. Další informace najdete v tématu [resetování zařízení pomocí vzdálené správy Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset-remote).

#### <a name="exact-imei-format-not-required-when-searching-all-devices--30407680---"></a>Při hledání všech zařízení se nevyžaduje přesný formát IMEI.<!--30407680 -->
Při hledání **všech zařízení**nebudete muset vkládat mezery do čísel IMEI.

#### <a name="deleting-a-device-in-the-apple-portal-will-be-reflected-in-the-intune-portal--2489996---"></a>Odstranění zařízení na portálu Apple se projeví na portálu Intune.<!--2489996 -->
Pokud se zařízení odstraní z portálu od společnosti Apple Program registrace zařízení nebo z portálu Apple Business Manager, zařízení se během další synchronizace automaticky odstraní z Intune.

### <a name="the-enrollment-status-page-now-tracks-win32-apps---2714451---"></a>Stránka stavu registrace teď sleduje aplikace Win32.<!-- 2714451 -->
To platí jenom pro zařízení s Windows 10 verze 1903 a novější. Další informace najdete v tématu [nastavení stránky stavu registrace](../enrollment/windows-enrollment-status.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="reset-and-wipe-devices-in-bulk-by-using-the-graph-api---3295288---"></a>Hromadné resetování a vymazání zařízení pomocí Graph API<!-- 3295288 -->
Při hromadném obnovení a vymazání zařízení 100 můžete použít Graph API.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="the-encryption-report-is-out-of-public-preview---4587546--------"></a>Zpráva o šifrování není Public Preview.<!-- 4587546      -->
[Sestava pro šifrování nástrojem BitLocker a zařízení](../protect/encryption-monitor.md) je nyní všeobecně dostupná a již není součástí verze Public Preview.


<!-- ########################## -->
## <a name="april-2019"></a>Duben 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací
#### <a name="user-experience-update-for-the-company-portal-app-for-ios---2536024---"></a>Aktualizace uživatelského prostředí pro aplikaci Portál společnosti pro iOS<!-- 2536024 -->
Změnila se Domovská stránka aplikace Portál společnosti pro zařízení s iOS. Tato změna způsobí, že se Domovská stránka bude lépe řídit vzorci uživatelského rozhraní iOS a zároveň poskytuje vylepšenou zjistitelnost pro aplikace a e-knihy.

#### <a name="changes-to-company-portal-enrollment-for-ios-12-device-users--3448635---"></a>Změny registrace Portál společnosti pro uživatele zařízení s iOS 12<!--3448635 -->
Portál společnosti na obrazovkách a krocích pro registraci zařízení s iOS byly aktualizovány aktualizace pro změny v registraci MDM vydané v Apple iOS 12,2. Aktualizovaný pracovní postup vyzve uživatele k zadání těchto akcí:  

* Umožněte prohlížeči Safari otevřít web Portál společnosti a před návratem do aplikace Portál společnosti stáhnout profil pro správu.  
* Otevřete aplikaci nastavení a nainstalujte na jejich zařízení profil správy.
* Vraťte se do aplikace Portál společnosti, abyste mohli dokončit registraci.  

Aktualizované kroky a obrazovky registrace najdete v tématu [registrace zařízení se systémem iOS v Intune](https://docs.microsoft.com/user-help/enroll-your-device-in-intune-ios).

#### <a name="openssl-encryption-for-android-app-protection-policies---3747362---"></a>OpenSSL šifrování pro zásady ochrany aplikací pro Android<!-- 3747362 -->
Zásady ochrany aplikací Intune (aplikace) na zařízeních s Androidem teď používají knihovnu šifrování OpenSSL, která je kompatibilní se standardem FIPS 140-2. Další informace najdete v části [šifrování](../apps/app-protection-policy-settings-android.md#encryption) [v tématu Nastavení zásad ochrany aplikací pro Android v Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="enable-win32-app-dependencies---2617348----"></a>Povolit závislosti aplikací Win32<!-- 2617348  -->
Jako správce můžete vyžadovat, aby byly před instalací aplikace Win32 nainstalovány jako závislosti jiné aplikace. Konkrétně musí zařízení před instalací aplikace Win32 nainstalovat závislé aplikace. V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat** , aby se zobrazilo okno **Přidat aplikaci** . Jako **Typ aplikace**vyberte **aplikace pro Windows (Win32)** . Po přidání aplikace můžete vybrat **závislosti** a přidat tak závislé aplikace, které musí být nainstalovány, než bude možné nainstalovat aplikaci Win32. Další informace najdete v tématu [samostatná verze Intune – Správa aplikací Win32](./../apps/app-management.md). 

#### <a name="app-version-installation-information-for-microsoft-store-for-business-apps---3537391-----"></a>Informace o instalaci verze aplikace pro aplikace Microsoft Store for Business<!-- 3537391   -->
Sestavy instalace aplikací obsahují informace o verzi aplikace Microsoft Store pro obchodní aplikace. V Intune vyberte **klientské aplikace** > **aplikace**. Vyberte **aplikaci Microsoft Store pro firmy** a potom v části **monitorování** vyberte **stav instalace zařízení** .

#### <a name="additions-to-win32-apps-requirement-rules---3676883-----"></a>Přidání pravidel požadavků pro aplikace Win32<!-- 3676883   -->
Pravidla požadavků můžete vytvořit na základě PowerShellových skriptů, hodnot registru a informací o systému souborů. V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat**. Pak jako **Typ aplikace** v okně **Přidat aplikaci** vyberte **aplikace pro Windows (Win32)** .  Vyberte **požadavky** > **Přidat** a nakonfigurujte další pravidla požadavků. Pak jako **typ požadavku**vyberte buď **typ souboru**, **registr**, nebo **skript** . Další informace najdete v tématu [Správa aplikací Win32](./../apps/app-management.md).

#### <a name="configure-your-win32-apps-to-be-installed-on-intune-enrolled-azure-ad-joined-devices---3695227----"></a>Konfigurace aplikací Win32, které se mají nainstalovat na zařízení připojená k Azure AD zaregistrovaným v Intune<!-- 3695227  -->
Můžete přiřadit aplikace Win32, které se mají nainstalovat do zaregistrovaných zařízení připojených k Azure AD v Intune. Další informace o aplikacích Win32 v Intune najdete v tématu [Správa aplikací Win32](./../apps/app-management.md).

#### <a name="device-overview-shows-primary-user--3794259----"></a>Přehled zařízení zobrazuje primárního uživatele<!--3794259  -->
Na stránce s přehledem zařízení se zobrazí primární uživatel, který se taky označuje jako uživatel spřažení zařízení a uživatele (UDA). Pokud chcete zobrazit primárního uživatele pro zařízení, vyberte zařízení > **Intune** > **všechna zařízení** > **zvolit zařízení.** Primární uživatel se zobrazí v horní části stránky s **přehledem** .

#### <a name="additional-managed-google-play-app-reporting-for-android-enterprise-work-profile-devices---4105925----"></a>Další spravované Google Play vytváření sestav aplikací pro zařízení s Androidem Enterprise Work Profile<!-- 4105925  -->
U spravovaných aplikací Google Play nasazených do zařízení se systémem Android Enterprise Work profilů můžete zobrazit konkrétní číslo verze aplikace nainstalované na zařízení. To platí jenom pro požadované aplikace.  

#### <a name="ios-third-party-keyboards---4111843-----"></a>Klávesnice třetích stran iOS<!-- 4111843   -->
Podpora zásad ochrany aplikací Intune pro nastavení **klávesnice třetích stran** pro iOS už není podporovaná kvůli změně platformy iOS. Toto nastavení nebudete moct konfigurovat v konzole pro správu Intune a na klientovi se v sadě Intune App SDK neuplatní.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="updated-certificate-connectors---icm-113304612---"></a>Aktualizované konektory certifikátů<!-- ICM 113304612 -->
Pro Microsoft Intune jsme vydali aktualizace pro [Intune Certificate Connector i pro Certificate connectory PFX](../protect/certficates-pfx-configure.md#whats-new-for-connectors). Nové verze opraví několik známých problémů.

#### <a name="set-login-settings-and-control-restart-options-on-macos-devices---1210083----"></a>Nastavení přihlašovacích nastavení a řízení možností restartování na zařízeních macOS<!-- 1210083  -->
Na zařízeních macOS můžete vytvořit konfigurační profil zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > zvolit **MacOS** pro **funkce zařízení** > pro typ profilu). Tato aktualizace zahrnuje nové nastavení přihlašovacího okna, jako je například zobrazení vlastního nápisu, výběr způsobu přihlášení uživatelů, zobrazení nebo skrytí nastavení napájení a další.

Pokud se chcete podívat na tato nastavení, přejděte na [Nastavení funkcí zařízení MacOS](../configuration/macos-device-features-settings.md).

#### <a name="configure-wifi-on-android-enterprise-device-owner-dedicated-devices-running-in-multi-app-kiosk-mode--3041940----"></a>Konfigurace Wi-Fi v Androidu Enterprise, vyhrazená zařízení vlastníka zařízení, která běží v celoobrazovkovém režimu s více aplikacemi<!--3041940  -->
V celoobrazovkovém režimu s více aplikacemi můžete povolit nastavení v systému Android Enterprise a vlastníka zařízení v případě, že běží jako vyhrazené zařízení. V této aktualizaci můžete uživatelům povolit konfiguraci a připojení k sítím Wi-Fi (**Intune** > **Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for Platform > **owner, omezení zařízení** pro typ profilu > **vyhrazená zařízení** > **beznabídkový režim**: konfigurace **multi-App** > **Wi-Fi**).

Pokud chcete zobrazit všechna nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo zakažte funkce](../configuration/device-restrictions-android-for-work.md).

Platí pro: zařízení se systémem Android Enterprise vyhrazená v celoobrazovkovém režimu s více aplikacemi

#### <a name="configure-bluetooth-and-pairing-on-android-enterprise-device-owner-dedicated-devices-running-in-multi-app-kiosk-mode---3041941----"></a>Konfigurace Bluetooth a párování v Androidu Enterprise, vyhrazená zařízení vlastníka zařízení, která běží v celoobrazovkovém režimu s více aplikacemi<!-- 3041941  -->
V celoobrazovkovém režimu s více aplikacemi můžete povolit nastavení v systému Android Enterprise a vlastníka zařízení v případě, že běží jako vyhrazené zařízení. V této aktualizaci můžete koncovým uživatelům povolit Bluetooth a spárovat zařízení přes**Bluetooth ( > ** **Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** pro platformu > **jenom pro vlastníka zařízení, omezení** pro typ profilu > **vyhrazená zařízení** > **beznabídkový režim**: konfigurace pro **více aplikací** > **Bluetooth**).

Pokud chcete zobrazit všechna nastavení, která můžete nakonfigurovat, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo zakažte funkce](../configuration/device-restrictions-android-for-work.md).

Platí pro: zařízení se systémem Android Enterprise vyhrazená v celoobrazovkovém režimu s více aplikacemi

#### <a name="create-and-use-oemconfig-device-configuration-profiles-in-intune---3305883----"></a>Vytvoření a použití profilů konfigurace zařízení OEMConfig v Intune<!-- 3305883  -->
V této aktualizaci Intune podporuje konfiguraci zařízení se systémem Android Enterprise pomocí OEMConfig. Konkrétně můžete vytvořit profil konfigurace zařízení a použít nastavení pro zařízení s Androidem Enterprise pomocí OEMConfig (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for Platform).

Podpora pro výrobce OEM je aktuálně založená na jednotlivých DODAVATELích. Pokud není požadovaná aplikace OEMConfig v seznamu aplikací OEMConfig dostupná, kontaktujte `IntuneOEMConfig@microsoft.com`.

Další informace o této funkci najdete [v Microsoft Intune používání a Správa zařízení se systémem Android Enterprise pomocí OEMConfig](../configuration/android-oem-configuration-overview.md).

Platí pro: Android Enterprise

#### <a name="windows-update-notifications---3316758-3316782----"></a>Oznámení web Windows Update<!-- 3316758, 3316782  -->
Přidali jsme dvě *Nastavení uživatelského prostředí* do konfigurací web Windows Update Ring, které můžete spravovat v konzole Intune. Teď můžete:
- Zablokuje nebo povolí uživatelům [vyhledávání aktualizací Windows](../protect/windows-update-settings.md).
- Spravujte [web Windows Update úroveň oznámení](../protect/windows-update-settings.md) , kterou uživatelé uvidí.

#### <a name="new-device-restriction-settings-for-android-enterprise-device-owner---3574254----"></a>Nová nastavení omezení pro zařízení s Androidem Enterprise, vlastníkem zařízení<!-- 3574254  -->
Na zařízeních s Androidem Enterprise můžete vytvořit profil omezení zařízení, abyste povolili nebo omezili funkce, nastavili pravidla hesel a další možnosti (**Konfigurace zařízení** > **profily** > **vytvořit profil** > vyberte **Android Enterprise** for Platform > **Owner jenom > omezení zařízení** pro typ profilu). 

Tato aktualizace zahrnuje nastavení nového hesla, umožňuje úplný přístup k aplikacím v Obchod Google Play pro plně spravovaná zařízení a další. Pokud chcete zobrazit aktuální seznam nastavení, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo zakažte funkce](../configuration/device-restrictions-android-for-work.md). 

Platí pro: zařízení se systémem Android Enterprise s plnou správou

#### <a name="check-for-a-tpm-chipset-in-a-windows-10-device-compliance-policy---3617671---"></a>Zjištění sady čipů TPM v zásadách dodržování předpisů pro zařízení s Windows 10<!-- 3617671 -->

Tato funkce je zpožděná a plánuje se pozdější vydání.

#### <a name="updated-ui-changes-for-microsoft-edge-browser-on-windows-10-and-later-devices---3775833-----"></a>Aktualizované změny uživatelského rozhraní pro prohlížeč Microsoft Edge v zařízeních s Windows 10 a novějším<!-- 3775833   -->
Když vytváříte profil konfigurace zařízení, můžete povolit nebo zakázat funkce Microsoft Edge na zařízeních s Windows 10 a novějších (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** pro platformu, > **omezení zařízení** pro typ profilu > **Microsoft Edge Browser**). V této aktualizaci jsou nastavení Microsoft Edge výstižnější a usnadňuje pochopení.

Tyto funkce zobrazíte tak, že přejdete na [Nastavení omezení pro zařízení v prohlížeči Microsoft Edge](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser).

Platí pro: Windows 10 a novější

#### <a name="expanded-support-for-android-enterprise-fully-managed-devices--preview-----3903241-3903244-3903246-----"></a>Rozšířená podpora pro plně spravovaná zařízení s Androidem Enterprise (Preview)<!--   3903241, 3903244, 3903246   -->
Pořád ve veřejné verzi Preview rozšířili jsme naši podporu pro plně spravovaná zařízení s Androidem Enterprise, která se nejdřív oznámila v lednu 2019, aby obsahovala tyto:

- Na plně spravovaných a vyhrazených zařízeních můžete vytvořit [zásady dodržování předpisů](../protect/compliance-policy-create-android-for-work.md) , které budou zahrnovat pravidla pro hesla a požadavky na operační systém ( **zásady** > **dodržování předpisů zařízením** > **vytvořit zásadu** > **Android Enterprise** pro **vlastníka zařízení** > pro typ profilu).

  Na vyhrazených zařízeních se může zařízení zobrazovat jako **nevyhovující**. Podmíněný přístup není k dispozici na vyhrazených zařízeních. Ujistěte se, že jste dokončili všechny úkoly nebo akce, abyste získali vyhrazená zařízení, která vyhovují vašim přiřazeným zásadám.

- [Podmíněný přístup](../protect/conditional-access.md) – zásady podmíněného přístupu, které se vztahují na Android, se vztahují také na zařízení se systémem Android Enterprise s plnou správou. Uživatelé teď můžou zaregistrovat svoje plně spravované zařízení v Azure Active Directory pomocí **Microsoft Intune aplikace**. Pak si přečtěte a vyřešte všechny problémy dodržování předpisů pro přístup k prostředkům organizace.

- Nová aplikace pro koncové uživatele (Microsoft Intune aplikace) – je k dispozici nová aplikace koncového uživatele pro zařízení s Androidem spravovaná s názvem **Microsoft Intune**. Tato nová aplikace je lehká a moderní a poskytuje podobné funkce jako aplikace Portál společnosti, ale pro plně spravovaná zařízení. Další informace najdete v tématu [Microsoft Intune aplikace na Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune).

Pokud chcete nastavit zařízení s plnou správou Androidu, přečtěte si **registrace zařízení** > **registraci v Androidu** > zařízení **ve vlastnictví firmy a plně spravovaná uživatelská zařízení**. Podpora plně spravovaných zařízení s Androidem zůstává ve verzi Preview a některé funkce Intune nemusí být plně funkční.  

Další informace o této verzi Preview najdete v našem blogu [Microsoft Intune-Preview 2 pro zařízení s plnou správou Android Enterprise](https://aka.ms/preview2_AE_fullymanaged).

#### <a name="use-compliance-manager-to-create-assessments-for-microsoft-intune---4404750---"></a>Použití Správce dodržování předpisů k vytváření posouzení pro Microsoft Intune<!-- 4404750 -->

[Správce dodržování předpisů](https://servicetrust.microsoft.com/ComplianceManager) (otevře další web společnosti Microsoft) je nástroj pro vyhodnocení rizik na základě pracovního postupu na portálu Microsoft Trust Service. Umožňuje sledovat, přiřazovat a ověřovat aktivity dodržování předpisů právními předpisy vaší organizace týkající se služeb Microsoftu. Můžete si vytvořit vlastní posouzení dodržování předpisů pomocí služeb Office 365, Azure, Dynamics, Professional Services a Intune. V Intune jsou k dispozici dvě posouzení – FFIEC a GDPR.

Správce dodržování předpisů vám pomůže zaměřit se na vaše úsilí tím, že rozbalí ovládací prvky spravované společností Microsoft a řídí ovládací prvky spravované vaší organizací. Posouzení můžete dokončit a pak vyexportovat a vytisknout posouzení.

[Rada pro posuzování federálních finančních institucí (FFIEC)](https://www.microsoft.com/trustcenter/compliance/FFIEC) (otevírá jiný web společnosti Microsoft) je sada standardů pro online bankovnictví vydaná FFIEC. Je to nejvíce požadované posouzení finančních institucí, které používají Intune. Interpretuje, jak Intune pomáhá splňovat FFIEC kyberbezpečnosti pokyny týkající se úloh veřejných cloudů. Posuzování FFIEC služby Intune je druhé hodnocení FFIEC ve Správci dodržování předpisů.

V následujícím příkladu vidíte rozpis pro ovládací prvky FFIEC. Microsoft pokrývá ovládací prvky 64. Zodpovídáte za zbývající 12 kontrol.

![Podívejte se na ukázku posouzení Intune pro FFIEC, včetně akcí zákazníků a akcí Microsoftu.](./media/whats-new/intune-ffiec-assessment-status.png)

[Obecné nařízení o ochraně osobních údajů (GDPR)](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview) (otevře další web společnosti Microsoft) je právní právo Evropské unie (EU), které pomáhá chránit práva jednotlivců a jejich dat. GDPR je nejužitečnější hodnocení, které je užitečné při dodržování předpisů týkajících se ochrany osobních údajů. 

V následujícím příkladu vidíte rozpis pro ovládací prvky GDPR. Microsoft pokrývá ovládací prvky 49. Zodpovídáte za zbývající ovládací prvky 66.

![Podívejte se na ukázku posouzení Intune pro GDPR, včetně akcí zákazníků a akcí Microsoftu.](./media/whats-new/intune-assessment-status.png)


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="configure-profile-to-skip-some-screens-during-setup-assistant---2276470----"></a>Nakonfigurovat profil pro přeskočení některých obrazovek během Průvodce nastavením<!-- 2276470  -->
Když vytváříte profil registrace macOS, můžete ho nakonfigurovat tak, aby po absolvování Průvodce nastavením přeskočil kteroukoli z následujících obrazovek:
- Vzhled
- Tón zobrazení
- iCloudStorage Pokud vytvoříte nový profil nebo upravíte profil, je nutné, aby se vybrané přeskočené obrazovky synchronizovaly se serverem Apple MDM.  Uživatelé můžou vydat ruční synchronizaci zařízení, aby při vybírání změn profilu nedocházelo k žádnému zpoždění.
Další informace najdete v tématu [Automatická registrace zařízení MacOS pomocí program registrace zařízení nebo Apple School Manageru](../enrollment/device-enrollment-program-enroll-macos.md).

#### <a name="bulk-device-naming-when-enrolling-corporate-ios-devices--3566569----"></a>Při registraci firemních zařízení s iOS se hromadně pojmenování zařízení<!--3566569  -->
Pokud používáte jednu z podnikových metod registrace společnosti Apple (DEP/ABM/ASM), můžete nastavit formát názvu zařízení tak, aby automaticky pojmenovaná příchozí zařízení s iOS. V šabloně můžete zadat formát, který zahrnuje typ zařízení a sériové číslo. Provedete to tak, že v **Intune** > **registraci zařízení** > registraci **Apple** > **registrační program tokeny** > **Vybrat token** >**vytvořit profil** > **Formát zařízení**. Můžete upravovat stávající profily, ale název se použije jenom u nově synchronizovaných zařízení.

#### <a name="updated-default-timeout-message-on-enrollment-status-page---3959331---"></a>Aktualizovaná výchozí zpráva s časovým limitem na stránce stavu registrace<!-- 3959331 -->
Aktualizovali jsme výchozí zprávu s časovým limitem, kterou uživatelé uvidí, když stránka stavu registrace (ESP) překračuje hodnotu časového limitu zadanou v profilu ESP. Nová výchozí zpráva se uživatelům zobrazí a pomůže jim pochopit další akce, které je potřeba provést s nasazením ESP.  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="retire-noncompliant-devices---1827291-----"></a>Vyřazení zařízení nesplňujících požadavky<!-- 1827291   -->
Tato funkce byla zpožděna a plánuje se pro budoucí verzi.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="intune-data-warehouse-v10-changes-reflecting-back-to-beta---4403765---"></a>Změny V datovém skladu Intune V 1.0 odrážející zpátky do beta verze<!-- 4403765 -->
V případě, že verze 1.0 byla poprvé představena v 1808, liší se v několika významných způsobech z verze beta rozhraní API. V 1903 se tyto změny projeví zpátky v beta verzi rozhraní API. Pokud máte důležité sestavy, které používají verzi beta rozhraní API, důrazně doporučujeme, abyste tyto sestavy přepnuli na V 1.0, aby nedocházelo k nepodstatným změnám. Další informace najdete v tématu [protokol změn pro rozhraní API datového skladu Intune](../developer/reports-changelog.md#1903-part-2).

#### <a name="monitor-security-baseline-status-public-preview----3082047---"></a>Monitorovat stav standardních hodnot zabezpečení (Public Preview) <!-- 3082047 --> 
Přidali jsme zobrazení pro [jednotlivé kategorie](../protect/security-baselines-monitor.md#per-category-view) do monitorování standardních hodnot zabezpečení. (Standardní hodnoty zabezpečení zůstávají ve verzi Preview.) Zobrazení podle kategorií zobrazuje každou kategorii ze směrného plánu společně s procentem zařízení, která spadají do každé skupiny stavů pro danou kategorii. Teď můžete zjistit, kolik zařízení se neshoduje s jednotlivými kategoriemi, jsou nesprávně nakonfigurované nebo se nedají použít.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="scope-tags-for-apple-vpp-tokens--2371886----"></a>Značky oboru pro tokeny programu Apple VPP<!--2371886  -->
Nyní můžete přidat značky oboru do tokenů programu Apple VPP. K tokenu Apple VPP s touto značkou budou mít přístup jenom uživatelé přiřazení se stejnou značkou Scope. Aplikace VPP a e-knihy zakoupené s tímto tokenem zdědí značky oboru. Další informace o značkách oboru najdete v tématu [použití značek RBAC a Scope](scope-tags.md).

<!-- ########################## -->
## <a name="march-2019"></a>Březen 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací
#### <a name="deploy-microsoft-visio-and-microsoft-project---3725386----"></a>Nasazení aplikace Microsoft Visio a aplikace Microsoft Project<!-- 3725386  -->
V případě, že vlastníte licence pro tyto aplikace, teď můžete nasadit Microsoft Visio pro pro Office 365 a desktopový klient Microsoft Project Online jako nezávislé aplikace na zařízení s Windows 10 pomocí Microsoft Intune. V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat** , aby se zobrazilo okno **Přidat aplikaci** . V okně **Přidat aplikaci** vyberte jako **Typ aplikace**možnost **Windows 10** . Pak vyberte **Konfigurovat sadu aplikací** a vyberte aplikace, které chcete nainstalovat. Další informace o aplikacích Office 365 pro zařízení s Windows 10 najdete v článku [přiřazení aplikací office 365 k zařízením s Windows 10 pomocí Microsoft Intune](../apps/apps-add-office365.md).

#### <a name="microsoft-visio-pro-for-office-365-product-name-change---3593653----"></a>Změna názvu produktu Microsoft Visio pro pro Office 365<!-- 3593653  -->
**Microsoft Visio pro for Office 365** se teď označuje jako **Microsoft Visio Online Plan 2**.  Další informace o aplikaci Microsoft Visio najdete v tématu [plán 2 pro Visio online](https://products.office.com/visio/visio-online-plan-2). Další informace o aplikacích Office 365 pro zařízení s Windows 10 najdete v článku [přiřazení aplikací office 365 k zařízením s Windows 10 pomocí Microsoft Intune](../apps/apps-add-office365.md).

#### <a name="intune-app-protection-policy-app-character-limit-setting---3291302----"></a>Nastavení limitu počtu znaků v zásadách ochrany aplikací Intune (APP)<!-- 3291302  -->
Správci Intune můžou zadat výjimku pro aplikaci Intune omezit nastavení zásad **vyjmutí, kopírování a vložení s jinými aplikacemi** .  Jako správce můžete zadat počet znaků, které mohou být vyjmuty nebo zkopírovány ze spravované aplikace. Toto nastavení umožní sdílet zadaný počet znaků do libovolné aplikace bez ohledu na nastavení omezit vyjmutí, kopírování a vložení s jinými aplikacemi. Všimněte si, že verze Portál společnosti Intune aplikace pro Android vyžaduje verzi 5.0.4364.0 nebo novější. Další informace najdete v tématech [Ochrana dat iOS](../apps/app-protection-policy-settings-ios.md#data-protection), [Ochrana dat Android](../apps/app-protection-policy-settings-android.md#data-protection)a [Kontrola protokolů ochrany klientských aplikací](../apps/app-protection-policy-settings-log.md#app-protection-policy-settings).

#### <a name="office-deployment-tool-odt-xml-for-office-proplus-deployment---3192477-----"></a>Office Deployment Tool (ODT) XML pro nasazení Office ProPlus<!-- 3192477   -->
Při vytváření instance Office pro plus v konzole pro správu Intune budete moct zadat XML nástroje pro nasazení Office (ODT). To umožní větší úpravou, pokud existující možnosti uživatelského rozhraní Intune nevyhovují vašim potřebám. Další informace najdete v tématu [přiřazení aplikací Office 365 k zařízením s Windows 10 pomocí Microsoft Intune](../apps/apps-add-office365.md) a [možností konfigurace pro nástroj pro nasazení Office](https://docs.microsoft.com/DeployOffice/configuration-options-for-the-office-2016-deployment-tool).

#### <a name="app-icons-will-now-be-displayed-with-an-automatically-generated-background---1429026----"></a>Ikony aplikací se nyní zobrazí s automaticky generovaným pozadím<!-- 1429026  -->
V aplikaci pro Windows Portál společnosti se teď ikony aplikací zobrazí s automaticky generovaným pozadím na základě dominantní barvy ikony (Pokud se dá detekovat). V případě potřeby bude toto pozadí nahrazovat šedé ohraničení, které bylo dříve viditelné na dlaždicích aplikace. Uživatelům se tato změna projeví ve verzích Portál společnosti novějších než 10.3.3451.0.

#### <a name="install-available-apps-using-the-company-portal-app-after-windows-bulk-enrollment---2751523-----"></a>Instalace dostupných aplikací pomocí aplikace Portál společnosti po hromadné registraci Windows<!-- 2751523   -->
Zařízení s Windows, která jsou registrovaná v Intune pomocí [hromadné registrace Windows](../enrollment/windows-bulk-enroll.md) (zřizovací balíčky), budou moct používat aplikaci Portál společnosti k instalaci dostupných aplikací. Další informace o aplikaci Portál společnosti najdete v tématu [Ruční přidání portál společnosti Windows 10](../apps/store-apps-company-portal-app.md) a [postup konfigurace aplikace Microsoft Intune portál společnosti](../apps/company-portal-app.md).

#### <a name="the-microsoft-teams-app-can-be-selected-as-part-of-the-office-app-suite---3828932----"></a>Aplikace Microsoft Teams se dá vybrat jako součást sady Office App Suite.<!-- 3828932  -->
Aplikace Microsoft Teams se dá zahrnout nebo vyloučit jako součást instalace sady Office pro plus a sady aplikací. Tato funkce funguje pro sadu Office pro plus číslo buildu 16.0.11328.20116 +. Uživatel se musí odhlásit a pak přihlásit k zařízení, aby se instalace dokončila. V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat**. Vyberte jednu z typů aplikace **sady Office 365** a potom vyberte možnost **Konfigurovat sadu aplikací**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="automatically-start-an-app-when-running-multiple-apps-in-kiosk-mode-on-windows-10-and-later-devices---2351390---"></a>Automatické spuštění aplikace při spuštění více aplikací v celoobrazovkovém režimu na zařízeních s Windows 10 a novějším<!-- 2351390 -->

V zařízeních se systémem Windows 10 a novějším můžete spustit zařízení v celoobrazovkovém režimu a spustit spoustu aplikací. V této aktualizaci je k dispozici nastavení automatického **spuštění** (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** **pro > Platform** pro typ profilu > veřejný **terminál s více aplikacemi**). Toto nastavení slouží k automatickému spuštění aplikace, když se uživatel přihlásí k zařízení.

Pokud chcete zobrazit seznam a popis všech nastavení veřejného terminálu, přečtěte si téma [nastavení zařízení s Windows 10 a novějším, která se mají spustit jako veřejný terminál v Intune](../configuration/kiosk-settings-windows.md).

Platí pro: Windows 10 a novější

#### <a name="operational-logs-also-show-details-on-non-compliant-devices---4063755----"></a>Provozní protokoly také zobrazují podrobnosti o nevyhovujících zařízeních.<!-- 4063755  -->
Při směrování protokolů Intune do funkce Azure monitor můžete také směrovat provozní protokoly. V této aktualizaci poskytují provozní protokoly také informace o zařízeních, která nedodržují předpisy.

Další informace o této funkci najdete v tématu [odeslání dat protokolu do úložiště, centra událostí nebo Log Analytics v Intune](review-logs-using-azure-monitor.md).

#### <a name="route-logs-to-azure-monitor-in-more-intune-workloads---3804627---"></a>Směrování protokolů pro Azure Monitor v dalších úlohách Intune<!-- 3804627 -->
V Intune můžete směrovat audit a provozní protokoly na centra událostí, úložiště a Log Analytics v Azure Monitor (**Intune** > **monitorování** **nastavení diagnostiky** > ). V této aktualizaci můžete tyto protokoly směrovat ve více úlohách Intune, včetně dodržování předpisů, konfigurací, klientských aplikací a dalších.

Další informace o protokolech směrování a Azure Monitor najdete v tématu [posílání dat protokolu do úložiště, centra událostí nebo Log Analytics](review-logs-using-azure-monitor.md).

#### <a name="create-and-use-mobility-extensions-on-android-zebra-devices-in-intune---3305880-----"></a>Vytváření a používání rozšíření mobility na zařízeních s Androidem Zebra v Intune<!-- 3305880   -->
V této aktualizaci podporuje Intune konfiguraci zařízení se systémem Android zebra. Konkrétně můžete vytvořit profil konfigurace zařízení a použít nastavení pro zařízení s Androidem Zebra s využitím profilů služby mobility (mobility), které vygenerovala StageNow (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android** pro Platform > **MX Profile (jenom Zebra)** pro typ profilu).

Další informace o této funkci najdete v tématu [používání a Správa zařízení Zebra s rozšířeními mobility v Intune](../configuration/android-zebra-mx-overview.md).

Platí pro: Android

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení
#### <a name="encryption-report-for-windows-10-devices-in-public-preview---2351538---"></a>Sestava šifrování pro zařízení s Windows 10 (ve verzi Public Preview)<!-- 2351538 -->
Chcete-li zobrazit podrobnosti o stavu šifrování zařízení s Windows 10, použijte novou [sestavu šifrování (Preview)](../protect/encryption-monitor.md) . K dispozici jsou podrobnosti o zařízeních, verzi TPM, připravenosti na šifrování a stavu, zasílání zpráv o chybách a dalších.  

#### <a name="access-bitlocker-recovery-keys-from-the-intune-portal-in-public-preview---2351547-----"></a>Přístup k obnovovacím klíčům BitLockeru z portálu Intune (ve verzi Public Preview)<!-- 2351547   -->
Pomocí Intune teď můžete [Zobrazit podrobnosti](../protect/encryption-monitor.md) o ID klíče BitLockeru a obnovovacích klíčích BitLockeru z Azure Active Directory.

#### <a name="microsoft-edge-support-for-intune-scenarios-on-ios-and-android-devices---3411007---"></a>Podpora Microsoft Edge pro scénáře Intune na zařízeních s iOS a Androidem<!-- 3411007 -->
Microsoft Edge bude podporovat všechny stejné scénáře správy jako Intune Managed Browser s přidáním vylepšení pro činnost koncového uživatele. Mezi funkce Microsoft Edge Enterprise, které jsou povolené v zásadách Intune, patří podpora duální identity, integrace zásad ochrany aplikací, integrace služby Azure Application proxy a spravovaných zástupců a domovské stránky. Další informace najdete v tématu [Podpora Microsoft Edge](../apps/app-configuration-managed-browser.md#microsoft-edge-support).

#### <a name="exchange-onlineintune-connector-deprecate-support-for-eas-only-devices--3105122----"></a>Exchange Online/Intune Connector zastaralá podpora pro zařízení jenom s EAS<!--3105122  -->
Konzola Intune už nepodporuje prohlížení a správu zařízení jenom pro EAS připojených k Exchangi Online s konektorem Intune. Místo toho máte následující možnosti:
- Registrace zařízení ve správě mobilních zařízení (MDM)
- Použití zásad Intune App Protection ke správě zařízení
- Používat ovládací prvky Exchange, jak je uvedeno v [klientech a mobilních zařízeních v Exchangi Online](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/clients-and-mobile-in-exchange-online)

#### <a name="search-the-all-devices-page-for-an-exact-device-by-using-name--4254930---"></a>Na stránce všechna zařízení vyhledejte přesná zařízení pomocí [name].<!--4254930 -->
Teď můžete vyhledat přesný název zařízení. Přejít na **zařízení** > **Intune** > **všechna zařízení** > do vyhledávacího pole, abyste mohli vyhledat přesnou shodu s názvem zařízení {}. Například **{Device12345}** .

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="support-for-additional-connectors-on-the-tenant-status-page---3617202----"></a>Podpora dalších konektorů na stránce stavu tenanta<!-- 3617202  -->
[Stránka stav tenanta](tenant-status.md) teď zobrazuje informace o stavu dalších konektorů, včetně *rozšířené ochrany před internetovými útoky v programu Windows Defender* (ATP) a dalších konektorů ochrany před mobilními hrozbami.

#### <a name="support-for-the-power-bi-compliance-app-from-the-data-warehouse-blade-in-microsoft-intune---4260871---"></a>Podpora aplikace Power BI dodržování předpisů z okna datového skladu v Microsoft Intune<!-- 4260871 -->
Dříve se odkaz **stáhnout Power BI soubor** v okně **datového skladu Intune** stáhl do sestavy datového skladu Intune (soubor. pbix). Tato sestava byla nahrazena aplikací Power BI dodržování předpisů. Aplikace Power BI dodržování předpisů nebude vyžadovat zvláštní načítání nebo instalaci. Otevře se přímo na online portálu Power BI a zobrazí data speciálně pro vašeho tenanta Intune na základě vašich přihlašovacích údajů. V Intune vyberte odkaz **nastavit datový sklad Intune** na pravé straně okna Intune. Pak klikněte na **získat Power BI aplikaci**. Další informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="granting-intune-read-only-access-to-some-azure-active-directory-roles---3637917----"></a>Udělení přístupu k některým rolím Azure Active Directory k Intune jen pro čtení<!-- 3637917  -->
K těmto rolím Azure AD se udělil přístup jenom pro čtení Intune. Oprávnění udělená rolím Azure AD nahrazují oprávnění udělená pomocí řízení přístupu na základě role (RBAC) Intune.

Přístup k datům auditu Intune jen pro čtení:

- Správce dodržování předpisů
- Správce dat dodržování předpisů

Přístup ke všem datům Intune je určený jen pro čtení:

- Správce zabezpečení
- Operátor zabezpečení
- Čtenář zabezpečení

Další informace najdete v tématu [řízení přístupu na základě role](role-based-access-control.md).

#### <a name="scope-tags-for-ios-app-provisioning-profiles--2934430-----"></a>Značky oboru pro zřizovací profily aplikací pro iOS<!--2934430   -->
Do zřizovacího profilu aplikace pro iOS můžete přidat značku oboru, aby k němu měl přístup jenom lidé s rolemi přiřazenými k zřizovacímu profilu aplikace pro iOS. Další informace najdete v tématu [použití značek RBAC a Scope](scope-tags.md).

#### <a name="scope-tags-for-app-configuration-policies--2371891-----"></a>Značky oboru pro zásady konfigurace aplikací<!--2371891   -->
Můžete přidat značku oboru do zásad konfigurace aplikace, aby k zásadám konfigurace aplikací měli přístup jenom lidé s rolemi přiřazenými k této značce oboru. Zásady konfigurace aplikací se můžou zaměřit na nebo přidružit k aplikacím, které mají přiřazenou stejnou značku oboru. Další informace najdete v tématu [použití značek RBAC a Scope](scope-tags.md).

#### <a name="microsoft-edge-support-for-intune-scenarios-on-ios-and-android-devices---3411007---"></a>Podpora Microsoft Edge pro scénáře Intune na zařízeních s iOS a Androidem<!-- 3411007 -->
Microsoft Edge bude podporovat všechny stejné scénáře správy jako Intune Managed Browser s přidáním vylepšení prostředí pro koncové uživatele. Mezi funkce Microsoft Edge Enterprise, které jsou povolené v zásadách Intune, patří podpora duální identity, integrace zásad ochrany aplikací, integrace služby Azure Application proxy a spravovaných zástupců a domovské stránky. Další informace najdete v tématu [Podpora Microsoft Edge](../apps/app-configuration-managed-browser.md#microsoft-edge-support).




<!-- ########################## -->
## <a name="february-2019"></a>Únor 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací
#### <a name="intune-macos-company-portal-dark-mode---3300524----"></a>Tmavý režim Intune macOS Portál společnosti<!-- 3300524  -->
Intune macOS Portál společnosti teď podporuje tmavý režim pro macOS. Když povolíte tmavý režim na macOS 10.14 + +, Portál společnosti upraví jeho vzhled na barvy, které se projeví v tomto režimu.

#### <a name="intune-will-leverage-google-play-protect-apis-on-android-devices---2577355-----"></a>Intune bude využívat Google Play chránit rozhraní API na zařízeních s Androidem.<!-- 2577355   -->
Někteří správci IT mají na BYODou šířku místa, kde můžou koncoví uživatelé ukončit root nebo jailbreaking svůj mobilní telefon. Toto chování, ale někdy nechtěně úmyslné, má za následek obejít mnoho zásad Intune, které jsou nastavené tak, aby chránily data organizace na zařízeních koncových uživatelů. Proto Intune poskytuje základní a jailbreaků detekci registrovaných i neregistrovaných zařízení. V této verzi bude Intune využívat Google Play chránit rozhraní API, aby je bylo možné přidat k existujícím kontrolám zjišťování kořenu pro nezaregistrovaná zařízení. I když Google nesdílí celou řadu kontrol, ke kterým dojde, očekáváme, že tato rozhraní API zjišťují uživatele, kteří si svá zařízení rootují z jakéhokoli důvodu, aby mohli na starších zařízeních získat novější aktualizace operačního systému. Tito uživatelé si pak můžou zablokovat přístup k firemním datům, jinak se jejich firemní účty můžou vymazat z aplikací s povolenými zásadami. Pro další hodnotu bude mít správce IT nyní několik aktualizací sestav v rámci okna Intune App Protection – sestava "uživatelé s příznakem" zobrazí informace o tom, kteří uživatelé se budou zjišťovat prostřednictvím služby Google Play SafetyNet prověřování rozhraní API. "potenciálně škodlivé aplikace" budou zobrazuje, které aplikace se zjišťují přes kontrolu rozhraní API pro ověřování aplikací přes Google. Tato funkce je dostupná na Androidu.

#### <a name="win32-app-information-available-in-troubleshooting-blade---2617342-----"></a>Informace o aplikaci Win32 dostupné v okně Poradce při potížích<!-- 2617342   -->
V okně pro **řešení potíží s** aplikací Intune teď můžete shromažďovat soubory protokolu chyb pro instalaci aplikace Win32. Další informace o řešení potíží s instalací aplikací najdete v tématu řešení potíží s [instalací aplikací](./../apps/troubleshoot-app-install.md) a [odstraňování potíží s aplikacemi Win32](./../apps/troubleshoot-app-install.md#win32-app-installation-troubleshooting).

#### <a name="app-status-details-for-ios-apps---3761235-----"></a>Podrobnosti o stavu aplikace pro aplikace pro iOS<!-- 3761235   -->
K dispozici jsou nové zprávy o chybách instalace aplikací, které souvisejí s následujícími:
- Selhání pro aplikace VPP při instalaci na sdíleném iPadu
- Chyba při zakázaném App Storu
- Nepovedlo se najít licenci VPP pro aplikaci.
- Nepovedlo se nainstalovat systémové aplikace pomocí poskytovatele MDM.
- Nepovedlo se nainstalovat aplikace, když je zařízení v režimu ztráty nebo celoobrazovkovém režimu.
- Nepovedlo se nainstalovat aplikaci, když uživatel není přihlášený k App Storu.

V Intune vyberte **klientské aplikace** > **aplikací** > název aplikace > **stav instalace zařízení**. Ve sloupci **Podrobnosti o stavu** budou k dispozici nové chybové zprávy.

#### <a name="new-app-categories-screen-in-the-company-portal-app-for-windows-10---3834780----"></a>Obrazovka nové kategorie aplikací v aplikaci Portál společnosti pro Windows 10<!-- 3834780  -->
Přidala se nová obrazovka s názvem **kategorie aplikací** , která vylepšuje možnosti procházení a výběru aplikací v portál společnosti pro Windows 10. Uživatelé teď uvidí své aplikace seřazené pod kategoriemi, jako jsou **Doporučené**, **vzdělávání**a **produktivita**. Tato změna se zobrazí v Portál společnosti verzích 10.3.3451.0 a novějším. Pokud si chcete zobrazit novou obrazovku, přečtěte si téma [co je nového v uživatelském rozhraní aplikace](whats-new-app-ui.md). Další informace o aplikacích v Portál společnosti najdete v tématu [instalace a sdílení aplikací na vašem zařízení](https://docs.microsoft.com/user-help/install-apps-cpapp-windows).  

#### <a name="power-bi-compliance-app---1455231-doc-work-item---"></a>Aplikace Power BI dodržování předpisů<!-- 1455231 doc-work-item -->
Přístup k datovému skladu Intune v Power BI online pomocí aplikace [Intune pro dodržování předpisů (datový sklad)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) . Pomocí této Power BI aplikace teď můžete přistupovat k předem vytvořeným sestavám a sdílet je bez jakéhokoli nastavení a bez nutnosti opustit webový prohlížeč. Další informace najdete v tématu [Změna aplikace pro dodržování předpisů Power BIm protokolu](../developer/reports-changelog.md#power-bi-compliance-app).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="powershell-scripts-can-run-in-a-64-bit-host-on-64-bit-devices---1862675-----"></a>Skripty PowerShellu se můžou spouštět na 64 hostitele na 64 zařízeních.<!-- 1862675   -->
Když přidáte skript prostředí PowerShell do konfiguračního profilu zařízení, skript se vždy spustí v 32-bit i v 64 operačních systémech. V rámci této aktualizace může správce spustit 64 skript na 64ovém hostiteli PowerShellu na zařízeních (**Konfigurace zařízení** > **skripty PowerShellu** > **Přidání** > **Konfigurace** > **spuštění skriptu v 64 hostitele PowerShellu**).

Další informace o používání PowerShellu najdete [v tématu skripty PowerShellu v Intune](../apps/intune-management-extension.md).

Platí pro: Windows 10 a novější

#### <a name="macos-users-are-prompted-to-update-their-password---1873216---"></a>uživatelům macOS se zobrazí výzva k aktualizaci hesla.<!-- 1873216 -->
Intune vynucuje nastavení **ChangeAtNextAuth** na zařízeních MacOS. Toto nastavení má vliv na koncové uživatele a zařízení, které mají zásady hesel dodržování předpisů nebo profily hesel omezení zařízení. Koncovým uživatelům se zobrazí výzva, aby si aktualizovali heslo. K této výzvě dochází vždy, když uživatel poprvé spustí úkol, který vyžaduje ověření, například přihlášení k zařízení. Uživatelům se taky může zobrazit výzva k aktualizaci hesla při jakékoli akci, která vyžaduje oprávnění správce, třeba pro vyžadování přístupu k řetězci klíčů.

Všechny nové nebo existující změny zásad hesla vyzve správce k aktualizaci hesla koncovými uživateli.

Platí pro:  
macOS

#### <a name="assign-scep-certificates-to-a-userless-macos-device---2340521------"></a>Přiřazení certifikátů SCEP k zařízení macOS pro uživatele<!-- 2340521    -->
Pomocí atributů zařízení macOS zařízení, včetně zařízení bez přidružení uživatele, můžete přiřadit certifikáty Simple Certificate Enrollment Protocol (SCEP) a přidružit profil certifikátu k profilům sítě Wi-Fi nebo VPN. Tím se rozšíří podpora, kterou už potřebujeme k [přiřazení certifikátů SCEP k zařízením s přidružením uživatele a bez něj](../protect/certificates-profile-scep.md) , na kterém běží Windows, iOS a Android.  Tato aktualizace přidává možnost výběru typu *certifikátu při konfiguraci* profilu certifikátu SCEP pro MacOS.

Platí pro:
- macOS

#### <a name="intune-conditional-access-ui-update---2432313-----"></a>Aktualizace uživatelského rozhraní pro podmíněný přístup v Intune<!-- 2432313   -->
Provedli jsme vylepšení uživatelského rozhraní pro podmíněný přístup v konzole Intune. Mezi ně patří:
- Okno *podmíněného přístupu* v Intune se nahradilo oknem z Azure Active Directory. Tím zajistíte, že v konzole Intune budete mít přístup k celé škále nastavení a konfigurací pro [podmíněný přístup](../protect/conditional-access.md) (což zůstává technologie Azure AD). 
- Přejmenovali jsme *místní okno přístupu* na přístup k *Exchangi*a přejmenovali jste nastavení *konektoru Exchange Service Connector* na toto přejmenované okno.  Tato změna slučuje, kde [konfigurujete a sledujete podrobnosti týkající se Exchange Online a místního](../protect/exchange-connector-install.md)prostředí.  

#### <a name="kiosk-browser-and-microsoft-edge-browser-apps-can-run-on-windows-10-devices-in-kiosk-mode---2935135-----"></a>Prohlížeč veřejného terminálu a aplikace pro prohlížeč Microsoft Edge se můžou spouštět na zařízeních s Windows 10 v celoobrazovkovém režimu.<!-- 2935135   -->
Zařízení s Windows 10 můžete používat v celoobrazovkovém režimu ke spuštění jedné aplikace nebo mnoha aplikací. Tato aktualizace zahrnuje několik změn v aplikacích prohlížeče v celoobrazovkovém režimu, včetně těchto:

- Přidejte prohlížeč Microsoft Edge nebo webový prohlížeč na veřejném počítači, aby se spouštěly jako aplikace na veřejném zařízení (**Konfigurace zařízení** > **profily** > **novém profilu** > **Windows 10 a novějším** **pro > pro** typ profilu).
- K dispozici jsou nové funkce a nastavení pro povolení nebo omezení (**Konfigurace zařízení** > **profily** > **novém profilu** > **Windows 10 a novější** pro > **omezení zařízení** pro typ profilu), včetně:

- Prohlížeč Microsoft Edge:
  - Použít celoobrazovkový režim Microsoft Edge
  - Aktualizovat prohlížeč po době nečinnosti

- Oblíbené položky a hledání:
  - Povolí změny vyhledávacího modulu.

Seznam těchto nastavení najdete tady:

- [Nastavení zařízení s Windows 10 a novějším, která se mají spustit jako veřejný terminál](../configuration/kiosk-settings-windows.md)
- [Omezení zařízení prohlížeče Microsoft Edge](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser)
- [Oblíbené a hledání v omezeních zařízení](../configuration/device-restrictions-windows-10.md#favorites-and-search)

Platí pro: Windows 10 a novější

#### <a name="new-device-restriction-settings-for-ios-and-macos-devices---3448774-----"></a>Nová nastavení omezení pro zařízení s iOS a macOS<!-- 3448774   -->
Můžete omezit některá nastavení a funkce na zařízeních s iOS a macOS (**Konfigurace zařízení** > **profily** > **novém profilu** > **iOS** nebo **MacOS** pro **omezení zařízení** > pro typ profilu). Tato aktualizace přidává další funkce a nastavení, která můžete ovládat, včetně nastavení času obrazovky, změny nastavení karty a mobilních plánů a dalších na zařízeních s iOS. Také se zpožděním viditelnosti aktualizací softwaru uživatelů a blokování ukládání obsahu do mezipaměti na zařízeních macOS.

Informace o funkcích a nastaveních, které můžete omezit, najdete v těchto tématech:

- [nastavení omezení pro zařízení s iOS](../configuration/device-restrictions-ios.md)
- [nastavení omezení pro zařízení macOS](../configuration/device-restrictions-macos.md)

Platí pro:

- iOS
- macOS

#### <a name="kiosk-devices-are-now-called-dedicated-devices-on-android-enterprise-devices---3598402-----"></a>Zařízení s veřejným veřejným zařízením se teď na zařízeních s Androidem Enterprise označují jako vyhrazená zařízení.<!-- 3598402   -->
Pro zarovnávání s terminologií pro Android se veřejné **terminály** změní na **vyhrazená zařízení** pro zařízení s Androidem enterprise (**Konfigurace zařízení** > **profily** > **vytvořit profil** > * * Android Enterprise for Platform > **Owner jenom** > **omezení zařízení** > **vyhrazená zařízení**).

Dostupná nastavení zobrazíte tak, že přejdete na [nastavení zařízení a povolíte nebo zakážete funkce](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings).

Platí pro:  
Android Enterprise

#### <a name="safari-and-delaying-user-software-update-visibility-ios-settings-are-moving-in-the-intune-ui---3640850-3803313-----"></a>Prohlížeč Safari a zpoždění viditelnosti aktualizace softwaru uživatele v uživatelském rozhraní Intune se pohybují.<!-- 3640850, 3803313   -->
U zařízení se systémem iOS můžete nastavit nastavení Safari a nakonfigurovat aktualizace softwaru. V této aktualizaci se tato nastavení pohybují do různých částí uživatelského rozhraní Intune:

- Nastavení Safari přesunuté z **prohlížeče Safari** (**Konfigurace zařízení** > **profily** > **novém profilu** > **iOS** pro **omezení** platformy > pro typ profilu) do **[integrovaných aplikací](../configuration/device-restrictions-ios.md#built-in-apps)** .
- Nastavení **zpoždění aktualizace softwaru uživatele pro zařízení s iOS pod dohledem** (**aktualizace softwaru** > **zásady aktualizace pro iOS**) se přesouvá na **omezení zařízení** >  **[Obecné](../configuration/device-restrictions-ios.md#general)** .  Podrobnosti o dopadu na stávající zásady najdete v tématu [aktualizace softwaru pro iOS](../protect/software-updates-ios.md#configure-the-policy).

Seznam nastavení najdete v tématu:

- [omezení zařízení s iOS](../configuration/device-restrictions-ios.md) 
- [aktualizace softwaru iOS](../protect/software-updates-ios.md)

Tato funkce platí pro:

- iOS

#### <a name="enabling-restrictions-in-the-device-settings-is-renamed-to-screen-time-on-ios-devices---3699164-----"></a>Povolení omezení v nastavení zařízení se přejmenují na čas obrazovky na zařízeních s iOS.<!-- 3699164   -->
Můžete nakonfigurovat **omezení povolení v nastavení zařízení** na zařízeních iOS (**Konfigurace zařízení** > **profily** > **Nový profil** > **iOS** pro > **omezení zařízení** pro typ profilu > **Obecné**). V této aktualizaci je toto nastavení přejmenováno na **čas obrazovky (jenom pod dohledem)** .

Chování je stejné. Určen

- iOS 11.4.1 a starší: **blok** brání koncovým uživatelům v nastavení vlastních omezení v nastavení zařízení. 
- iOS 12,0 a novější: **blok** znemožní koncovým uživatelům v nastavení zařízení nastavit vlastní **čas obrazovky** , včetně obsahu & omezení ochrany osobních údajů. V zařízeních upgradovaných na iOS 12,0 se už nebudou zobrazovat karty omezení v nastavení zařízení. Tato nastavení se nacházejí v **čase obrazovky**. 

Seznam nastavení najdete v tématu [omezení pro zařízení s iOS](../configuration/device-restrictions-ios.md#general).

Platí pro:
- iOS


#### <a name="intune-powershell-module---951068----"></a>Modul Intune PowerShell<!-- 951068  -->
Modul Intune PowerShell, který poskytuje podporu rozhraní Intune API prostřednictvím Microsoft Graph, je teď k dispozici v [Microsoft Galerie prostředí PowerShell](https://www.powershellgallery.com/packages/Microsoft.Graph.Intune/6.1902.1.10).

- [Podrobnosti o tom, jak používat tento modul](https://github.com/Microsoft/Intune-PowerShell-SDK/blob/master/README.md)
- [Příklady scénářů, které používají tento modul](https://github.com/Microsoft/Intune-PowerShell-SDK/blob/master/Samples/README.md)

#### <a name="improved-support-for-delivery-optimization--3183757----"></a>Vylepšená podpora pro optimalizaci doručování<!--3183757  -->
V Intune jsme rozšířili podporu pro konfiguraci optimalizace doručování. Teď můžete v konzole Intune nakonfigurovat rozšířený seznam [nastavení Optimalizace doručení](../configuration/delivery-optimization-settings.md) a směrovat ho přímo na vaše zařízení.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení

#### <a name="rename-an-enrolled-windows-device---1911112----"></a>Přejmenování zaregistrovaného zařízení se systémem Windows<!-- 1911112  -->
Teď můžete přejmenovat zaregistrované zařízení s Windows 10 (RS4 nebo novější). Pokud to chcete udělat, vyberte zařízení ** > ** **Intune** > **všechna zařízení** > vyberte zařízení > **Přejmenovat zařízení**. Tato funkce v současné době nepodporuje přejmenování hybridních zařízení se systémem Windows Azure AD.

#### <a name="auto-assign-scope-tags-to-resources-created-by-an-admin-with-that-scope---3173823----"></a>Automaticky přiřadí značky oboru k prostředkům vytvořeným správcem s tímto oborem.<!-- 3173823  -->
Když správce vytvoří prostředek, všechny značky oboru přiřazené správci se automaticky přiřadí těmto novým prostředkům.

### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="failed-enrollment-report-moves-to-the-device-enrollment-blade---3560202----"></a>Zpráva o selhání registrace se přesune do okna registrace zařízení.<!-- 3560202  -->
Sestava **neúspěšné registrace** byla přesunuta do části **monitorování** okna **registrace zařízení** . Byly přidány dva nové sloupce (metoda registrace a verze operačního systému).

#### <a name="company-portal-abandonment-report-renamed-to-incomplete-user-enrollments--3815076-eemiss---"></a>Sestava opuštění Portál společnosti přejmenována na nedokončené registrace uživatelů<!--3815076 eemiss -->
Sestava o **opuštění portál společnosti** byla přejmenována na **nedokončené registrace uživatele**.






<!-- ########################## -->
## <a name="january-2019"></a>Leden 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Správa aplikací

#### <a name="intune-app-pin---2298397---"></a>PIN kód aplikace Intune<!-- 2298397 -->
Jako správce IT teď můžete nakonfigurovat počet dní, po které může koncový uživatel čekat, než bude nutné změnit PIN kód aplikace Intune. Nové nastavení má *za následek Resetování PIN kódu po několika dnech* a je dostupné v Azure Portal tak, že > **klientské aplikace** služby **Intune** > **Zásady ochrany aplikací** > **vytvořit zásadu** > **Nastavení** > **požadavky na přístup**. Tato funkce, která je dostupná pro zařízení s [iOS](../apps/app-protection-policy-settings-ios.md) a [Androidem](../apps/app-protection-policy-settings-android.md) , podporuje kladnou celočíselnou hodnotu.

#### <a name="intune-device-reporting-fields---2748738---"></a>Pole pro vytváření sestav zařízení v Intune<!-- 2748738 -->
Intune poskytuje další pole pro vytváření sestav zařízení, včetně ID registrace aplikace, výrobce Androidu, modelu a verze opravy zabezpečení i modelu iOS. V Intune jsou tato pole dostupná, a to tak, že vyberete **klientské aplikace** > **stav ochrany aplikací** a zvolíte **sestavu ochrana aplikací: iOS, Android**. Kromě toho vám tyto parametry pomůžou nakonfigurovat nastavení seznam **povolených** pro výrobce zařízení (Android), seznam **povolených** pro model zařízení (Android a iOS) a minimální verzi opravy zabezpečení Androidu.

#### <a name="toast-notifications-for-win32-apps---3136566-----"></a>Oznámení informačních zpráv pro aplikace Win32<!-- 3136566   -->
Můžete potlačit zobrazování oznámení informační zprávy koncového uživatele na přiřazení aplikace. V Intune vyberte **klientské aplikace** > **aplikace** > vyberte **přiřazení** > aplikací > **Zahrnout skupiny**.

#### <a name="intune-app-protection-policies-ui-update---3251427----"></a>Aktualizace uživatelského rozhraní zásad ochrany aplikací Intune<!-- 3251427  -->
Změnili jsme štítky pro nastavení a tlačítka pro ochranu aplikací Intune, aby bylo snazší porozumět. Mezi tyto změny patří:  
- Ovládací prvky se změní z **yes** / žádné ovládací prvky, které **by** měly **blokovat** / **Povolit** a **Zakázat** ovládací prvky **Povolit** / . Popisky jsou také aktualizovány.  
- Nastavení se přeformátují, takže nastavení a jeho popisek jsou vedle sebe v ovládacím prvku k zajištění lepší navigace.

Výchozí nastavení a počet nastavení zůstávají stejné, ale tato změna umožňuje uživateli pochopit, Procházet a používat nastavení snadněji, aby bylo možné použít vybrané zásady ochrany aplikací. Informace najdete v tématu [Nastavení iOS](../apps/app-protection-policy-settings-ios.md) a [nastavení Androidu](../apps/app-protection-policy-settings-android.md).

#### <a name="additional-settings-for-outlook---3301182----"></a>Další nastavení pro Outlook<!-- 3301182  -->
V Intune teď můžete nakonfigurovat následující další nastavení pro Outlook pro iOS a Android:

- Povoluje použití pracovních nebo školních účtů v Outlooku v iOS a Androidu.
- Nasazení moderního ověřování pro Office 365 a hybridních moderních ověřování v místních účtech
- Při výběru základního ověřování použít `SAMAccountName` pro pole username v e-mailovém profilu
- Povoluje uložení kontaktů.
- Konfigurace externích příjemců s upozorněním na upozornění
- Konfigurovat **prioritní doručenou poštu**
- Vyžadovat pro přístup k Outlooku pro iOS biometrika
- Blokovat externí image

> [!NOTE]
> Pokud používáte zásady Intune App Protection ke správě přístupu k podnikovým identitám, měli byste zvážit, že nepovolíte možnost **vyžadovat biometrika**. Další informace najdete v tématu **vyžadování podnikových přihlašovacích údajů pro** přístup k [nastavení přístupu iOS](../apps/app-protection-policy-settings-ios.md#access-requirements) a [nastavení přístupu pro Android](../apps/app-protection-policy-settings-android.md#access-requirements).

Další informace najdete v tématu [nastavení konfigurace aplikace Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

#### <a name="delete-android-enterprise-apps---1352553---"></a>Odstranění podnikových aplikací pro Android<!-- 1352553 -->
Spravované aplikace Google Play můžete z Microsoft Intune odstranit. Pokud chcete odstranit spravovanou aplikaci Google Play, otevřete Microsoft Intune v Azure Portal a vyberte **klientské aplikace** > **aplikace**. V seznamu aplikace vyberte tři tečky (...) napravo od spravované aplikace Google Play a pak v zobrazeném seznamu vyberte **Odstranit** . Při odstranění spravované aplikace Google Play ze seznamu aplikací se spravovaná aplikace Google Play automaticky neschválí.

#### <a name="managed-google-play-app-type---1352580---"></a>Typ spravované aplikace Google Play<!-- 1352580 -->
Typ **spravované aplikace Google Play** vám umožní přidat [spravované aplikace Google Play](https://play.google.com/work/search?q=microsoft&c=apps) do Intune. Jako správce Intune teď můžete v Intune Procházet, vyhledávat, schvalovat, synchronizovat a přiřazovat schválené spravované Google Play aplikace.  Už nemusíte procházet konzolu spravované Google Play samostatně a už se nemusíte znovu ověřovat.  V Intune vyberte **klientské aplikace** > **aplikace** > **Přidat**. V seznamu **Typ aplikace** vyberte **spravované Google Play** jako typ aplikace.

#### <a name="default-android-pin-keyboard---3802457---"></a>Výchozí klávesnice pro PIN kód pro Android<!-- 3802457 -->
U koncových uživatelů, kteří na svých zařízeních s Androidem nastavili kód PIN pro Intune App Protection (APP) s typem PIN typu numeric, se teď zobrazí výchozí klávesnice pro Android namísto pevného uživatelského rozhraní klávesnice s Androidem, které jste předtím navrhli. Tato změna byla provedena konzistentně při používání výchozích klávesnic pro Android i iOS pro oba typy kódu PIN typu "numeric" nebo "heslo". Další informace o nastavení přístupu koncového uživatele v Androidu, například PIN kódu aplikace, najdete v tématu [požadavky na přístup k Androidu](../apps/app-protection-policy-settings-android.md#access-requirements).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="administrative-templates-are-in-public-preview-and-moved-to-their-own-configuration-profile----3322847---"></a>Šablony pro správu jsou ve verzi Public Preview a přesunuté do vlastního konfiguračního profilu. <!-- 3322847 -->

Šablony pro správu v Intune (**Konfigurace zařízení** > **šablony pro správu**) jsou momentálně ve verzi Public Preview. S touto aktualizací:

- Šablony pro správu zahrnují nastavení 300, která se dají spravovat v Intune. Dříve tato nastavení existuje pouze v editoru zásad skupiny.
- Šablony pro správu jsou k dispozici ve verzi Public Preview.
- Šablony pro správu se přesunují z **Konfigurace zařízení** > **šablony pro správu** do **Konfigurace zařízení** > **profily** > **vytvořit profil** > na **platformě**vyberte **Windows 10 a novější** > v **typu profilu**, vyberte **šablony pro správu**.
- Vytváření sestav je povolené.

Další informace o této funkci najdete v článku [šablony Windows 10, kde můžete nakonfigurovat nastavení zásad skupiny](../configuration/administrative-templates-windows.md).

Platí pro: Windows 10 a novější

#### <a name="use-smime-to-encrypt-and-sign-multiple-devices-for-a-user---1333642---"></a>Použít S/MIME k šifrování a podepsání více zařízení pro uživatele<!-- 1333642 -->
Tato aktualizace zahrnuje šifrování S/MIME e-mailů pomocí nového profilu importovaného certifikátu (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > vyberte platformu > typ profilu **Importovaný certifikát PKCS**). V Intune můžete importovat certifikáty ve formátu PFX. Intune pak může doručit stejné certifikáty do více zařízení zaregistrovaných jedním uživatelem. To také zahrnuje:
- Nativní e-mailový profil v iOS podporuje povolení šifrování S/MIME pomocí importovaných certifikátů ve formátu PFX.
- Nativní e-mailová aplikace v zařízeních Windows Phone 10 automaticky používá certifikát S/MIME.
- Privátní certifikáty je možné doručit na různé platformy. Některé e-mailové aplikace ale S/MIME nepodporují.
- Na jiných platformách může být nutné ručně nakonfigurovat e-mailovou aplikaci a povolit S/MIME.  
- E-mailové aplikace, které podporují šifrování S/MIME, můžou zpracovávat načítání certifikátů pro šifrování S/MIME e-mailů způsobem, který MDM nepodporuje (například ho načítají z úložiště certifikátů svého vydavatele).
Další informace o této funkci najdete v tématu [S/MIME – přehled pro podepsání a šifrování e-mailu](../protect/certificates-s-mime-encryption-sign.md).
Podporováno v systémech: Windows, Windows Phone 10, macOS, iOS, Android

#### <a name="new-options-to-automatically-connect-and-persist-rules-when-using-dns-settings-on-windows-10-and-later-devices---1333665-2999078---"></a>Nové možnosti pro automatické připojení a zachování pravidel při použití nastavení DNS v zařízeních se systémem Windows 10 nebo novějším<!-- 1333665, 2999078 -->
V zařízeních se systémem Windows 10 a novějším můžete vytvořit konfigurační profil sítě VPN, který obsahuje seznam serverů DNS k překladu domén, například contoso.com. Tato aktualizace obsahuje nová nastavení pro překlad názvů (**Konfigurace zařízení** > **profily** > **vytvořit profil** > vyberte **Windows 10 a novější** pro platformu > vyberte možnost **VPN** pro typ profilu > **nastavení DNS** >**Přidat**): 
- **Automaticky připojit**: Pokud je tato možnost **povolena**, zařízení se automaticky připojí k síti VPN, když zařízení kontaktuje doménu, kterou zadáte, například contoso.com.
- **Persistent**: ve výchozím nastavení jsou všechna pravidla tabulky zásad překladu IP adres (NRPT) aktivní, pokud je zařízení připojené pomocí tohoto profilu sítě VPN. Pokud je toto nastavení **povolené** u pravidla NRPT, zůstane toto pravidlo aktivní na zařízení, i když se VPN odpojí. Pravidlo zůstane, dokud se neodebere profil sítě VPN nebo dokud se pravidlo ručně neodebere, což se dá udělat pomocí PowerShellu.
Nastavení [sítě VPN pro Windows 10](../configuration/vpn-settings-windows-10.md) popisují nastavení.

#### <a name="use-trusted-network-detection-for-vpn-profiles-on-windows-10-devices---1500165---"></a>Použití zjišťování důvěryhodných sítí pro profily sítě VPN na zařízeních s Windows 10<!-- 1500165 -->
Při použití zjišťování důvěryhodných sítí můžete zabránit tomu, aby profily sítě VPN automaticky vytvářely připojení VPN, když je uživatel již v důvěryhodné síti. Pomocí této aktualizace můžete přidat přípony DNS, které umožní detekci důvěryhodných sítí na zařízeních s Windows 10 a novějším (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** pro Platform > **VPN** pro typ profilu).
[Nastavení sítě VPN pro Windows 10](../configuration/vpn-settings-windows-10.md) uvádí aktuální nastavení sítě VPN.

#### <a name="manage-windows-holographic-for-business-devices-used-by-multiple-users---1907917-1063203---"></a>Správa zařízení s Windows holografickým pro firmy používaných více uživateli<!-- 1907917, 1063203 -->
V současné době můžete nakonfigurovat nastavení sdílených počítačů na zařízeních s Windows 10 a Windows holografickým pro firmy pomocí vlastního nastavení OMA-URI. V této aktualizaci se přidá nový profil pro konfiguraci nastavení sdíleného zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** > **sdílené zařízení s více uživateli**).
Další informace o této funkci najdete v [Nastavení Intune, kde můžete spravovat sdílená zařízení](../configuration/shared-user-device-settings.md).
Platí pro: Windows 10 a novější, Windows Holographic for Business

#### <a name="new-windows-10-update-settings--2626030--2512994----"></a>Nová nastavení aktualizací Windows 10<!--2626030  2512994  -->
Pro [aktualizační kanály Windows 10](../protect/windows-update-for-business-configure.md)můžete nakonfigurovat:
- **Chování Automatické aktualizace** – použijte novou možnost, *Obnovit výchozí* nastavení pro obnovení původních nastavení automatických aktualizací na počítači s Windows 10 na počítačích, na kterých běží *aktualizace z října 2018* .
- **Blokování uživatele při pozastavení aktualizací Windows** – umožňuje nakonfigurovat nové nastavení aktualizací softwaru, které vám umožní zablokovat nebo nechat uživatelům pozastavit instalaci aktualizací z *Nastavení* jejich počítačů.

#### <a name="ios-email-profiles-can-use-smime-signing-and-encryption---2662949---"></a>e-mailové profily pro iOS můžou používat podepisování a šifrování S/MIME.<!-- 2662949 -->
Můžete vytvořit e-mailový profil, který obsahuje různá nastavení. Tato aktualizace zahrnuje nastavení S/MIME, která se dají použít k podepisování a šifrování e-mailových komunikací na zařízeních s iOS (**Konfigurace zařízení** > **profily** > **vytvořit profil** > zvolit **iOS** pro > **e-mail** pro typ profilu).
[nastavení konfigurace e-mailu pro iOS](../configuration/email-settings-ios.md) zobrazí seznam nastavení.

#### <a name="some-bitlocker-settings-support-windows-10-pro-edition---2727036---"></a>Některá nastavení BitLockeru podporují edici Windows 10 pro.<!-- 2727036 -->
Můžete vytvořit konfigurační profil, který nastaví nastavení ochrany koncových bodů na zařízeních s Windows 10, včetně BitLockeru. Tato aktualizace přidává pro některá nastavení BitLockeru podporu pro Windows 10 Professional Edition.
Tato nastavení ochrany zobrazíte tak, že přejdete na [nastavení ochrany koncového bodu pro Windows 10](../protect/endpoint-protection-windows-10.md#windows-encryption).

#### <a name="shared-device-configuration-is-renamed-to-lock-screen-message-for-ios-devices-in-the-azure-portal---2809362---"></a>Konfigurace sdíleného zařízení se přejmenovala na zprávu zamykací obrazovky pro zařízení s iOS v Azure Portal<!-- 2809362 -->
Když vytváříte konfigurační profil pro zařízení s iOS, můžete přidat nastavení **Konfigurace sdíleného zařízení** a zobrazit konkrétní text na zamykací obrazovce. Tato aktualizace obsahuje následující změny: 
- Nastavení **Konfigurace sdíleného zařízení** v Azure Portal se přejmenují na "zpráva na zamykací obrazovce (jenom pod dohledem)" (**Konfigurace zařízení** > **profily** > **vytvořit profil** > vyberte **iOS** pro platformu > vyberte **funkce zařízení** pro typ profilu > **zpráva zamykací obrazovky**).
- Při přidávání zpráv na zamykací obrazovce můžete do **informací o značce assetu** a na **zamykací obrazovce**vložit sériové číslo, název zařízení nebo jinou hodnotu specifickou pro zařízení jako proměnnou. Můžete například zadat `Device name: {{devicename}}` nebo `Serial number is {{serialnumber}}` pomocí složených závorek. [tokeny iOS](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) vypisuje dostupné tokeny, které se dají použít.
[Nastavení pro zobrazení zpráv na zamykací obrazovce](../configuration/ios-device-features-settings.md#lock-screen-message) obsahuje seznam nastavení.

#### <a name="new-app-store-doc-viewing-gaming-device-restriction-settings-added-to-ios-devices---2827760--"></a>Nové App Storu, zobrazení dokumentů, nastavení omezení herních zařízení přidaná do zařízení se systémem iOS<!-- 2827760-->
V části **Konfigurace zařízení** > **profily** > **vytvoření profilu** > **iOS** pro > **omezení zařízení** pro typ profilu > **App Store, zobrazování dokumentů, hraní her**, jsou přidána následující nastavení: povolení spravovaných aplikací pro psaní kontaktů do nespravovaných účtů kontaktů povolení nespravovaných aplikací ke čtení ze spravovaných účtů kontaktů, pokud chcete zobrazit tato nastavení, přejděte na [omezení zařízení s iOS](../configuration/device-restrictions-ios.md#app-store-doc-viewing-gaming).

#### <a name="new-notification-hints-and-keyguard-settings-to-android-enterprise-device-owner-devices---3201839-3201843---"></a>Nové oznámení, doporučení a nastavení pro ochranu zařízení pro zařízení s Androidem Enterprise Device Owner<!-- 3201839 3201843 -->
Tato aktualizace zahrnuje několik nových funkcí na zařízeních s Androidem Enterprise, při spuštění jako vlastník zařízení. Pokud chcete tyto funkce použít, klikněte na **Konfigurace zařízení** > **profily** > **vytvořit profil** > na **platformě**, v možnosti **typ profilu**vyberte **Android Enterprise** >, vyberte **jenom vlastník zařízení** > **omezení zařízení**.

Obsahuje například tyto nové funkce:

- Zakažte zobrazování systémových oznámení, včetně příchozích volání, systémových výstrah, systémových chyb a dalších.
- Navrhuje přeskočit úvodní kurzy a tipy pro aplikace, které se otevřou poprvé.
- Zakažte Pokročilá nastavení ochrany před internetovými ochranou, jako je fotoaparát, oznámení, odemknutí otiskem prstu a další.

Nastavení zobrazíte tak, že přejdete na [Nastavení omezení pro zařízení s Androidem Enterprise](../configuration/device-restrictions-android-for-work.md).

#### <a name="android-enterprise-device-owner-devices-can-use-always-on-vpn-connections---3202194---"></a>Zařízení vlastníka zařízení s Androidem Enterprise můžou používat připojení VPN typu Always On.<!-- 3202194 -->
V této aktualizaci použijete k připojení vždy zapnutá síť VPN na zařízeních s Androidem enterprise zařízení vlastníka. Neustále aktivní připojení VPN zůstávají ve spojení nebo se ihned znovu připojí, jakmile uživatel odemkne zařízení, zařízení se restartuje nebo se změní bezdrátová síť. Připojení také můžete přepnout do „zamčeného“ režimu, který blokuje veškerý síťový provoz, dokud není připojení VPN zase aktivní.
V > **profily** můžete povolit vždycky ZAPNUTOU síť VPN > **vytvořit profil** > **Android Enterprise** for Platform > **omezení zařízení** jenom pro **vlastníka zařízení >** nastavení **připojení** . Nastavení zobrazíte tak, že přejdete na [Nastavení omezení pro zařízení s Androidem Enterprise](../configuration/device-restrictions-android-for-work.md).

#### <a name="new-setting-to-end-processes-in-task-manager-on-windows-10-devices---3285177---"></a>Nové nastavení pro koncové procesy ve Správci úloh na zařízeních s Windows 10<!-- 3285177 --> 
Tato aktualizace zahrnuje nové nastavení k ukončení procesů pomocí Správce úloh na zařízení s Windows 10. Pomocí konfiguračního profilu zařízení (**Konfigurace zařízení** > **profily** > **vytvořit profil** > na **platformě**vyberte v možnosti **typ profilu**> **Windows 10** , vyberte možnost **omezení zařízení** > **Obecné** nastavení), můžete toto nastavení zakázat nebo zakázat.
Pokud se chcete podívat na tato nastavení, přejděte na [Nastavení omezení pro zařízení s Windows 10](../configuration/device-restrictions-windows-10.md).
Platí pro: Windows 10 a novější

#### <a name="use-microsoft-recommended-settings-with-security-baselines-public-preview---2055484-----"></a>Použít nastavení Doporučené Microsoftem se standardními hodnotami zabezpečení (Public Preview)<!-- 2055484   -->

Intune se integruje s dalšími službami, které se zaměřují na zabezpečení, včetně Ochrany ATP v programu Windows Defender a Ochrany ATP v Office 365. Zákazníci požadují ve službách Microsoft 365 společnou strategii a soudržnější sadu ucelených bezpečnostních pracovních postupů. Naším cílem je srovnat strategie tak, abychom mohli vytvářet řešení přemosťující operace zabezpečení a běžné úlohy správy. V Intune se zaměřujeme na dosažení tohoto cíle publikováním sady doporučených standardních hodnot zabezpečení (v Intune > **standardních hodnot zabezpečení**služby**Intune** ).  Správce může vytvořit zásady zabezpečení přímo z těchto směrných plánů a pak je nasadit na své uživatele. Můžete také přizpůsobit doporučení osvědčených postupů pro splnění potřeb vaší organizace. Intune zajišťuje, že zařízení zůstávají v souladu s těmito standardními hodnotami, a upozorní správce, pokud uživatelé nebo zařízení tyto hodnoty nedodržují.

Tato funkce je ve verzi Public Preview, takže všechny vytvořené profily nyní nebudou přesunuty do šablon standardních hodnot zabezpečení, které jsou všeobecně dostupné (GA). Neměli byste v produkčním prostředí používat tyto šablony verze Preview.

Další informace o standardních hodnotách zabezpečení najdete [v tématu vytvoření směrného plánu zabezpečení Windows 10 v Intune](../protect/security-baselines-monitor.md).

Tato funkce se týká: Windows 10 a novější

#### <a name="non-administrators-can-enable-bitlocker-on-windows-10-devices-joined-to-azure-ad---2147379-----"></a>Uživatelé bez oprávnění správce můžou povolit BitLocker na zařízeních s Windows 10, která jsou připojená k Azure AD.<!-- 2147379   -->
Pokud povolíte nastavení BitLockeru na zařízeních s Windows 10 (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** pro > **Endpoint Protection** pro typ profilu > **šifrování Windows**), přidáte nastavení BitLockeru.

Tato aktualizace zahrnuje nové nastavení nástroje BitLocker umožňuje standardní uživatelé (bez oprávnění správce), aby šifrování povolil.

Nastavení zobrazíte tak, že přejdete na [nastavení ochrany koncových bodů pro Windows 10](../protect/endpoint-protection-windows-10.md#windows-encryption).

#### <a name="check-for-configuration-manager-compliance---2192052--eepublished----"></a>Ověřit Configuration Manager dodržování předpisů<!-- 2192052  eepublished  -->
Tato aktualizace zahrnuje nové nastavení dodržování předpisů Configuration Manager ( **zásady** > **dodržování předpisů zařízením** > **vytvořit zásadu** > **Windows 10 a novější** > **Configuration Manager dodržování předpisů**). Configuration Manager bude posílat signály funkci dodržování předpisů v Intune. Pomocí tohoto nastavení můžete vyžadovat, aby všechny signály Configuration Manager vracely "vyhovující".

Můžete například vyžadovat, aby v zařízeních byly nainstalované všechny aktualizace softwaru. V Configuration Manager má tento požadavek stav nainstalováno. Pokud jsou některé programy v zařízení v neznámém stavu, zařízení nedodržuje předpisy v Intune.

[Configuration Manager dodržování předpisů](../protect/compliance-policy-create-windows.md#configuration-manager-compliance) popisuje toto nastavení.

Platí pro: Windows 10 a novější

#### <a name="customize-wallpaper-on-supervised-ios-devices-using-a-device-configuration-profile---2809324-----"></a>Přizpůsobení tapety na zařízeních s iOS pod dohledem pomocí profilu konfigurace zařízení<!-- 2809324   -->
Když vytváříte konfigurační profil zařízení pro zařízení s iOS, můžete upravit některé funkce (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **iOS** pro **funkce zařízení** > pro typ profilu). Tato aktualizace zahrnuje nová nastavení **tapety** , která umožní správci použít na domovské obrazovce nebo na zamykací obrazovce obrázek. png,. jpg nebo. jpeg. Tato nastavení tapety se vztahují jenom na zařízení pod dohledem. 

Seznam těchto nastavení najdete v tématu [Nastavení funkcí pro zařízení s iOS](../configuration/ios-device-features-settings.md).

#### <a name="windows-10-kiosk-is-generally-available---3594661----"></a>Veřejné terminály s Windows 10 jsou všeobecně dostupné<!-- 3594661  -->
V této aktualizaci je k dispozici beznabídková funkce na zařízeních s Windows 10 a novějším (GA). Všechna nastavení, která můžete přidat a nakonfigurovat, najdete v tématu [Nastavení veřejného terminálu pro Windows 10 (a novější)](../configuration/kiosk-settings.md).

#### <a name="contact-sharing-via-bluetooth-is-removed-in-device-restrictions--device-owner-for-android-enterprise---3598396-----"></a>Sdílení kontaktů přes Bluetooth se odebírá v omezeních zařízení > vlastník zařízení pro Android Enterprise.<!-- 3598396   -->
Když vytvoříte profil omezení zařízení pro zařízení s Androidem Enterprise, budete mít k dispozici **Sdílení kontaktů prostřednictvím nastavení Bluetooth** . V této aktualizaci se odstraní **Sdílení kontaktů prostřednictvím nastavení Bluetooth** (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Android Enterprise** for platform > **omezení zařízení > vlastník zařízení** pro typ profilu > **Obecné**).

**Sdílení kontaktů prostřednictvím nastavení Bluetooth** není pro správu vlastníka zařízení s Androidem Enterprise podporováno. Takže když se toto nastavení odebere, nebude mít vliv na žádná zařízení ani klienty, ani když je toto nastavení povolené a nakonfigurované ve vašem prostředí.

Pokud chcete zobrazit aktuální seznam nastavení, přejděte na [nastavení zařízení s Androidem Enterprise a povolte nebo zakažte funkce](../configuration/device-restrictions-android-for-work.md).

Platí pro: vlastník zařízení se systémem Android Enterprise


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="more-detailed-enrollment-restriction-failure-messaging---3111564---"></a>Podrobnější zasílání zpráv o selhání omezení registrace<!-- 3111564 -->
Podrobnější chybové zprávy jsou k dispozici v případě, že nejsou splněna omezení registrace. Pokud se chcete podívat na tyto zprávy, přejděte na **Intune** > **řešení potíží** > a zkontrolujte tabulku selhání registrace. Další informace najdete v [seznamu selhání registrace](help-desk-operators.md#enrollment-failure-reference).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Správa zařízení
#### <a name="preview-of-support-for-android-corporate-owned-fully-managed-devices---1574342----"></a>Verze Preview podpory pro zařízení s Androidem, která jsou ve vlastnictví společnosti, plně spravovaná<!-- 1574342  -->
Intune teď podporuje plně spravovaná zařízení s Androidem, scénář "vlastník zařízení ve vlastnictví firmy", ve kterém jsou zařízení úzce spravovaná IT a přidružená k jednotlivým uživatelům. To správcům umožňuje spravovat celé zařízení, vynutilo rozšířené množství ovládacích prvků zásad nedostupných pro pracovní profily a omezuje uživatelům instalovat aplikace jenom ze spravovaných Google Play. Další informace najdete v tématu [Nastavení registrace Intune pro zařízení s Androidem s plnou správou](../enrollment/android-fully-managed-enroll.md) a [registrace vyhrazených zařízení nebo plně spravovaných zařízení](../enrollment/android-dedicated-devices-fully-managed-enroll.md).  Upozorňujeme, že tato funkce je ve verzi Preview. Některé možnosti Intune, jako jsou certifikáty, dodržování předpisů a podmíněný přístup, nejsou aktuálně k dispozici u zařízení s plně spravovanými uživateli Androidu.

#### <a name="selective-wipe-support-for-wip-without-enrollment-devices---1434452---"></a>Podpora selektivního vymazání pro Nedokončená práce bez registračních zařízení<!-- 1434452 -->
Windows Information Protection bez registrace (NV) umožňuje zákazníkům chránit podniková data na zařízeních s Windows 10 bez nutnosti úplné registrace MDM. Po ochraně dokumentů pomocí zásad pro nedokončené výroby může být chráněná data selektivně smazána správcem služby Intune. Když vyberete uživatele a zařízení a odešlete žádost o vymazání, všechna data, která byla chráněná prostřednictvím zásad výroby, se nedají použít. V Intune na portálu Azure Portal vyberte **Mobilní aplikace** > **Selektivní vymazání aplikace**.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="tenant-status-dashboard---1124854---"></a>Řídicí panel stavu tenanta<!-- 1124854 -->
Stránka nový [stav tenanta](tenant-status.md) poskytuje jedno umístění, kde můžete zobrazit stav a související podrobnosti pro vašeho tenanta.  Řídicí panel je rozdělen na čtyři oblasti:
- **Podrobnosti o tenantovi** – zobrazí informace, které obsahují název a umístění tenanta, vaši autoritu MDM, celkový počet zaregistrovaných zařízení ve vašem tenantovi a počet licencí. Tato část uvádí také aktuální verzi služby pro vašeho tenanta.
- **Stav konektoru** – zobrazí informace o dostupných konektorech, které jste nakonfigurovali, a můžete také zobrazit seznam těch, které jste ještě nepovolili.  
   V závislosti na aktuálním stavu každého konektoru jsou označeny jako v pořádku, varování nebo není v pořádku. Vyberte spojnici, pro kterou chcete procházet, a zobrazte podrobnosti nebo nakonfigurujte další informace.
- **Intune Service Health** – zobrazí podrobnosti o aktivních incidentech nebo výpadkech pro vašeho tenanta. Informace v této části jsou načteny přímo z centra zpráv Office.
- **Novinky Intune** – zobrazí aktivní zprávy pro vašeho tenanta. Zprávy zahrnují například oznámení, když váš tenant obdrží nejnovější funkce Intune.  Informace v této části jsou načteny přímo z centra zpráv Office.

#### <a name="new-help-and-support-experience-in-company-portal-for-windows-10---1488939--"></a>Nové prostředí pro nápovědu a podporu v Portál společnosti pro Windows 10<!-- 1488939-->
Nová stránka podpory & Portál společnosti pomoc pomáhá uživatelům při řešení potíží a vyžádat si nápovědu k problémům s aplikacemi a přístupem. Na nové stránce můžou e-maily Odeslat podrobnosti o chybě a diagnostickém protokolu a najít podrobnosti o helpdesku své organizace. V části Nejčastější dotazy najdete také odkazy na příslušnou dokumentaci k Intune.

#### <a name="new-help-and-support-experience-for-intune---3307080---"></a>Nové prostředí pro nápovědu a podporu pro Intune<!-- #3307080 -->
Zavádíme nové prostředí pro pomoc a podporu pro všechny klienty za několik dalších dní. Toto nové prostředí je dostupné pro Intune a k němu se dá získat přístup při použití oken Intune v [Azure Portal](https://portal.azure.com/).
Nové prostředí vám umožňuje popsat problém vlastními slovy a získat přehled možností řešení potíží a postupy z webu, jak problém opravit. Tato řešení jsou nabízená pomocí algoritmu strojového učení založeného na pravidlech, která se řídí dotazy uživatelů.
Kromě pokynů specifických pro vydání můžete použít pracovní postup vytvoření nového případu k otevření případu podpory e-mailem nebo telefonem. Toto nové prostředí nahrazuje předchozí pomoc a podporu pro statickou sadu předdefinovaných možností, které jsou založeny na oblasti konzoly, kterou jste v nástroji, když otevřete pomoc a podpora.
Další informace najdete v tématu [Jak získat podporu pro Microsoft Intune](get-support.md).

#### <a name="new-operational-logs-and-ability-to-send-logs-to-azure-monitor-services---3762211----"></a>Nové provozní protokoly a možnost odesílat protokoly do služby Azure Monitor Services<!-- 3762211  -->
Intune obsahuje integrované protokolování auditu, které sleduje události při provádění změn. Tato aktualizace zahrnuje nové funkce protokolování, včetně: 
- Provozní protokoly (Preview), které zobrazují podrobnosti o uživatelích a zařízeních, která jsou zaregistrovaná, včetně úspěšných a neúspěšných pokusů.
- Protokoly auditu a provozní protokoly je možné odesílat do Azure Monitor, včetně účtů úložiště, Center událostí a Log Analytics. Tyto služby umožňují ukládat, používat analýzy jako Splunk a QRadar a získávat vizualizace dat protokolování.

Další informace o této funkci najdete [v posílání dat protokolu do úložiště, centra událostí nebo Log Analytics v Intune](review-logs-using-azure-monitor.md) .

#### <a name="skip-more-setup-assistant-screens-on-an-ios-dep-device---2687509----"></a>Přeskočit další obrazovky pomocníka s nastavením na zařízení se systémem iOS DEP<!-- 2687509  -->
Kromě obrazovek, které můžete v současnosti přeskočit, můžete nastavit zařízení se systémem iOS DEP, aby při zápisu zařízení do pomocníka s nastavením přeskočili následující obrazovky: tónový displej, ochrana osobních údajů, migrace Androidu, tlačítko domů, iMessage & FaceTime, zprovoznění, sledování Migrace, vzhled, čas zobrazení, aktualizace softwaru, Nastavení SIM.
Pokud chcete vybrat, které obrazovky se mají přeskočit, přejděte na **registrace zařízení** > registrace **Apple** > **tokeny programu registrace** > **vyberte profily > profilů** > vyberte profil > **vlastnosti** > **přizpůsobení průvodce nastavením** > pro všechny obrazovky, které chcete přeskočit > **OK**, vyberte **Skrýt** .
Pokud vytvoříte nový profil nebo upravíte profil, je nutné, aby se vybrané přeskočené obrazovky synchronizovaly se serverem Apple MDM. Uživatelé můžou vydat ruční synchronizaci zařízení, aby při vybírání změn profilu nedocházelo k žádnému zpoždění.

#### <a name="android-enterprise-app-we-app-deployment---1171203---"></a>Android Enterprise APP – nasazení aplikace v aplikaci<!-- 1171203 -->
U zařízení s Androidem v zaregistrovaných zásadách ochrany aplikací, ale ve scénáři nasazení (App-We), teď můžete použít spravovaný Google Play k nasazení aplikací pro Store a obchodních aplikací uživatelům. Konkrétně můžete koncovým uživatelům poskytnout katalog aplikací a prostředí pro instalaci, které už nevyžadují, aby koncoví uživatelé vystavi zabezpečení jejich zařízení tím, že umožňují instalaci z neznámých zdrojů. Kromě toho tento scénář nasazení bude poskytovat Vylepšené uživatelské prostředí.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="scope-tags-for-apps---1081941---"></a>Značky oboru pro aplikace<!-- 1081941 -->
Můžete vytvořit značky oboru pro omezení přístupu k rolím a aplikacím. Do aplikace můžete přidat značku oboru, aby k ní měl přístup jenom lidé s rolemi přiřazenými k této značce oboru. V současné době se aplikace přidané do Intune ze spravovaných Google Play nebo aplikace zakoupené pomocí Apple Volume Purchase Program (VPP) nedají přiřadit ke značkám oboru (budoucí podpora se plánuje). Další informace najdete v tématu [použití značek oboru k filtrování zásad](scope-tags.md).




<!-- ########################## -->
## <a name="december-2018"></a>Prosince 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="updates-for-application-transport-security---748318---"></a>Aktualizace pro zabezpečení přenosu aplikace<!-- 748318 -->

Microsoft Intune podporuje zabezpečení TLS (Transport Layer Security) 1.2 +, aby bylo zajištěno, že služba Intune je ve výchozím nastavení bezpečnější a že se bude v souladu s dalšími službami společnosti Microsoft, jako je systém Microsoft Office 365. Aby bylo možné tento požadavek splnit, portál společnosti pro iOS a macOS vynutilí aktualizované požadavky na ATS (Application Transport Security) společnosti Apple, které budou také vyžadovat protokol TLS 1.2 +. ATS slouží k vynucení vyššího zabezpečení veškeré komunikace aplikací přes protokol HTTPS. Tato změna ovlivní zákazníky Intune, kteří používají aplikace Portál společnosti pro iOS a macOS. Další informace najdete v [blogu podpory pro Intune](https://aka.ms/compportalats).

#### <a name="the-intune-app-sdk-will-support-256-bit-encryption-keys---1832174---"></a>Sada Intune App SDK bude podporovat 256 bitů šifrovacích klíčů.<!-- 1832174 -->
Intune App SDK pro Android teď používá 256 šifrovacích klíčů, pokud je šifrování povolené zásadami ochrany aplikací. Sady SDK bude dále poskytovat podpora 128bitových klíčů z důvodu kompatibility s obsahem a aplikace, které používají starší verze sady SDK.

#### <a name="microsoft-auto-update-version-450-required-for-macos-devices---3503442---"></a>Pro zařízení macOS se vyžaduje 4.5.0 verze automatického aktualizace od Microsoftu.<!-- 3503442 -->
Aby bylo možné pokračovat v přijímání aktualizací Portál společnosti a dalších aplikací Office, musí zařízení spravovaná službou Intune upgradovat na Microsoft 4.5.0 Update. Uživatelé už můžou mít tuto verzi pro svoje aplikace Office.

### <a name="device-management"></a>Správa zařízení

#### <a name="intune-requires-macos-1012-or-later---2827778---"></a>Intune vyžaduje macOS 10,12 nebo novější.<!-- 2827778 -->
Intune teď vyžaduje verzi macOS 10,12 nebo novější. Zařízení s předchozími verzemi macOS nemůžou použít Portál společnosti k registraci do Intune. Aby uživatelé mohli dostávat podporu a nové funkce, musí upgradovat svoje zařízení na macOS 10,12 nebo novější a upgradovat Portál společnosti na nejnovější verzi.

<!-- ########################## -->
## <a name="november-2018"></a>Listopadu 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="uninstalling-apps-on-corporate-owned-supervised-ios-devices---1281677---"></a>Odinstalace aplikací ve vlastnictví zařízení iOS vlastněných společností<!-- 1281677 -->
Můžete odebrat libovolnou aplikaci na zařízeních s iOS, která jsou ve vlastnictví. Libovolnou aplikaci můžete odebrat, když cílem přiřazení typu **Odinstalovat** budou skupiny uživatelů nebo zařízení. U zařízení s iOSem, která jsou osobní nebo nejsou pod dohledem, budete nadále moci odebrat jen aplikace, které byly nainstalované pomocí Intune.

#### <a name="downloading-intune-win32-app-content---2617320---"></a>Stahuje se obsah aplikace Win32 pro Intune.<!-- 2617320 -->
Klienti s Windows 10 RS3 a novějšími stáhne obsah aplikace Intune Win32 pomocí součásti Optimalizace doručení v klientovi s Windows 10. Optimalizace doručení poskytuje funkce peer-to-peer, které jsou ve výchozím nastavení zapnuté. V současné době se Optimalizace doručení dá nakonfigurovat pomocí zásad skupiny. Další informace najdete v tématu [optimalizace doručování pro Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization).

#### <a name="end-user-device-and-app-content-menu---2771453---"></a>Nabídka obsahu zařízení a aplikace pro koncové uživatele<!-- 2771453 -->
Koncoví uživatelé teď můžou pomocí místní nabídky na zařízeních a aplikacích aktivovat běžné akce, jako je přejmenování zařízení nebo kontrola dodržování předpisů.

#### <a name="set-custom-background-in-managed-home-screen-app----3041945---"></a>Nastavení vlastního pozadí v aplikaci spravované na domovské obrazovce <!-- 3041945 -->
Přidáváme nastavení, které vám umožní přizpůsobit vzhled aplikace spravované domovské obrazovky v zařízeních s Androidem Enterprise, multi-App a celoobrazovkovém režimu.  Pokud chcete nakonfigurovat **vlastní adresu URL pozadí**, na webu Azure Portal přejděte na Intune > Konfigurace zařízení. Vyberte aktuální profil konfigurace zařízení nebo vytvořte nový a upravte nastavení beznabídkového režimu.
Nastavení veřejného terminálu najdete v tématu [omezení pro zařízení s Androidem Enterprise](../configuration/device-restrictions-android-for-work.md).

#### <a name="app-protection-policy-assignment-save-and-apply---3104570---"></a>Uložení a použití přiřazení zásad ochrany aplikací<!-- 3104570 -->
Teď máte lepší kontrolu nad [přiřazením zásad ochrany aplikací](../apps/app-protection-policies.md). Když vyberete *přiřazení* pro nastavení nebo úpravu přiřazení zásady, musíte před použitím změny **Uložit** svou konfiguraci. Pomocí **zahození** zrušte zaškrtnutí všech změn, které provedete bez uložení změn do seznamů zahrnutí nebo vyloučení.  Když budete vyžadovat uložení nebo zahození, přiřadí se zásadám ochrany aplikací jenom uživatelé, kterým máte v úmyslu.

#### <a name="new-microsoft-edge-browser-settings-for-windows-10-and-later---3174639---"></a>Nové nastavení prohlížeče Microsoft Edge pro Windows 10 a novější<!-- 3174639 -->
Tato aktualizace obsahuje nová nastavení, která vám pomůžou řídit a spravovat prohlížeč Microsoft Edge na vašich zařízeních. Seznam těchto nastavení najdete v tématu [omezení pro zařízení s Windows 10 (a novější)](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser).

#### <a name="new-apps-support-with-app-protection-policies---3330037---"></a>Podpora nových aplikací pomocí zásad ochrany aplikací<!-- 3330037 -->
Teď můžete spravovat tyto aplikace pomocí [zásad ochrany aplikací Intune](../apps/app-protection-policies.md):
- Stream (iOS)
- Postup (Android, iOS)
- PowerApps (Android, iOS)
- Tok (Android, iOS)

Zásady ochrany aplikací slouží k ochraně podnikových dat a řízení přenosu dat pro tyto aplikace, jako jsou jiné aplikace spravované zásadou Intune. Poznámka: Pokud tok ještě není viditelný v konzole, přidáte tok při vytváření nebo úpravách a zásadách ochrany aplikací. Provedete to tak, že použijete možnost **a další aplikace** a v poli vstupní pole zadáte *ID aplikace* pro tok. Pro Android použijte *com. Microsoft. Flow*a pro iOS použijte *com. Microsoft. procsimo*.


### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="support-for-ios-12-oauth-in-ios-email-profiles--2155106---"></a>Podpora pro iOS 12 OAuth v e-mailových profilech iOS<!--2155106 -->
E-mailové profily Intune pro iOS podporují OAuth (Open Authorization) v iOS 12. Pokud chcete tuto funkci zobrazit, vytvořte nový profil (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **iOS** jako platforma > **E-mail** jako typ profilu), nebo aktualizujte existující e-mailový profil iOS. Pokud OAuth povolíte v profilu, který už je nasazený uživatelům, jsou uživatelé vyzváni k opětovnému ověření a stažení svých e-mailů.

[E-mailové profily pro iOS](../configuration/email-settings-ios.md) obsahují více informací o použití OAuth.

#### <a name="network-access-control-nac-support-for-citrix-sso-for-ios---3259404---"></a>Podpora sítě Access Control (NAC) pro Citrix SSO pro iOS<!-- 3259404 -->
Společnost Citrix vydala aktualizaci brány Citrix, která umožňuje síťové Access Control (NAC) pro Citrix SSO pro iOS v Intune. Můžete se rozhodnout, jestli chcete do služby Intune zahrnout ID zařízení v rámci profilu sítě VPN, a potom tento profil nasdílet do zařízení s iOS. Abyste mohli používat tuto funkci, budete muset nainstalovat nejnovější aktualizaci pro bránu Citrix.

[Konfigurace nastavení sítě VPN na zařízeních s iOS](../configuration/vpn-settings-ios.md#base-vpn-settings) nabízí další informace o používání NAC, včetně některých dalších požadavků. 

#### <a name="ios-and-macos-version-numbers-and-build-numbers-are-shown---1892471---"></a>zobrazí se čísla verzí iOS a macOS a čísla sestavení.<!-- 1892471 -->
V oblasti **Dodržování předpisů zařízením** > **Dodržování předpisů zařízením** se zobrazují verze operačního systému iOS a macOS, která lze použít v zásadách dodržování předpisů. Tato aktualizace zahrnuje číslo sestavení, které je možné konfigurovat pro obě platformy.
Při vydání aktualizací zabezpečení společnost Apple obvykle ponechává stávající číslo verze, ale aktualizuje číslo buildu. Pomocí čísla buildu v zásadách dodržování předpisů můžete snadno zkontrolovat, jestli je nainstalovaná aktualizace řešící ohrožení zabezpečení.
Pokud chcete tuto funkci použít, přečtěte si téma zásady dodržování předpisů pro [iOS](../protect/compliance-policy-create-ios.md#device-health) a [MacOS](../protect/compliance-policy-create-mac-os.md#device-properties) .

#### <a name="update-rings-are-being-replaced-with-delivery-optimization-settings-for-windows-10-and-later---2753807---"></a>Aktualizační kroužky se nahrazují nastavením Optimalizace doručení pro Windows 10 a novější.<!-- 2753807 -->
Optimalizace doručení je nový konfigurační profil pro Windows 10 a novější. Tato funkce poskytuje efektivnější možnosti pro doručování aktualizací softwaru do zařízení ve vaší organizaci. Tato aktualizace také pomáhá doručovat nastavení v nových a existujících aktualizačních zazvoněních pomocí konfiguračního profilu.
Pokud chcete nakonfigurovat konfigurační profil optimalizace doručování, přečtěte si téma [nastavení Optimalizace doručení Windows 10 (a novější)](../configuration/delivery-optimization-windows.md).

#### <a name="new-device-restriction-settings-added-to-ios-and-macos-devices---2827760---"></a>Nová nastavení omezení zařízení přidaná do zařízení se systémem iOS a macOS<!-- 2827760 -->
Tato aktualizace obsahuje nová nastavení pro zařízení s iOS a macOS, která jsou vydaná s iOS 12:

**Nastavení iOS**: 
- Obecné: blokování odebírání aplikací (jenom pod dohledem)
- Obecné: blokový režim s omezeným přístupem USB (jenom pod dohledem)
- Obecné: vynucení automatického data a času (jenom pod dohledem)
- Heslo: blokovat automatické vyplňování hesla (jenom pod dohledem)
- Heslo: zablokovat žádosti o blízkost hesla (jenom pod dohledem)
- Heslo: blokování sdílení hesel (jenom pod dohledem)

**MacOS nastavení**: 
- Heslo: blokovat automatické vyplňování hesla
- Heslo: zablokovat žádosti o blízkost hesla
- Heslo: blokování sdílení hesel

Další informace o těchto nastaveních najdete v tématu Nastavení omezení pro zařízení s [iOS](../configuration/device-restrictions-ios.md) a [MacOS](../configuration/device-restrictions-macos.md) .

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="autopilot-support-for-hybrid-azure-active-directory-joined-devices-preview---1048100--"></a>Podpora autopilotu pro zařízení připojená k hybridnímu Azure Active Directory (Preview)<!-- 1048100-->
Zařízení připojená k hybridní službě Azure Active Directory si teď můžete nastavit pomocí Autopilotu. Zařízení musí být připojená do vaší podnikové sítě, aby mohla použít hybridní funkci Autopilotu. Další informace najdete v článku o [nasazení zařízení připojených k hybridní službě Azure AD pomocí Intune a Windows Autopilotu](../enrollment/windows-autopilot-hybrid.md).
Tato funkce se bude zavádět pro uživatelskou základnu v průběhu několika dalších dnů. Následující postup bude možné provést až po jejím zavedení pro váš účet.

#### <a name="select-apps-tracked-on-the-enrollment-status-page---2531007---"></a>Výběr aplikací sledovaných na stránce stavu registrace<!-- 2531007 -->
Můžete si vybrat, které aplikace se budou sledovat na stránce Stav registrace. Dokud tyto aplikace nenainstalujete, uživatel nebude moct zařízení používat. Další informace najdete v tématu [nastavení stránky stavu registrace](../enrollment/windows-enrollment-status.md).

#### <a name="search-for-autopilot-device-by-serial-number--2595788---"></a>Vyhledat zařízení autopilotu podle sériového čísla<!--2595788 -->
Zařízení s autopilotem teď můžete vyhledávat podle sériového čísla. Provedete to tak, že zvolíte **registrace zařízení** > **registraci systému Windows** > **zařízení** > do pole **Hledat podle sériového čísla** zadejte sériové číslo > stiskněte klávesu ENTER.

#### <a name="track-installation-of-office-proplus--2620217---"></a>Sledovat instalaci Office ProPlus<!--2620217 -->
Uživatelé můžou sledovat průběh instalace [Office ProPlus](../apps/apps-add-office365.md) pomocí [stránky stavu registrace](../enrollment/windows-enrollment-status.md). Další informace najdete v tématu [nastavení stránky stavu registrace](../enrollment/windows-enrollment-status.md).

#### <a name="alerts-for-expiring-vpp-token-or-company-portal-license-running-low---2237572---"></a>Výstrahy pro vypršení platnosti tokenu VPP nebo licence na Portál společnosti s nízkým provozem<!-- 2237572 -->
Pokud používáte program Volume purchase program (VPP) k předběžnému zřízení Portál společnosti během registrace DEP, Intune vás upozorní, když se brzo vyprší platnost tokenu VPP a když jsou spuštěné licence pro Portál společnosti nízké.

#### <a name="macos-device-enrollment-program-support-for-apple-school-manager-accounts--3006133---"></a>Podpora macOS Program registrace zařízení pro účty Apple School Manageru<!--3006133 -->
Intune teď podporuje použití Program registrace zařízení na zařízeních macOS pro účty Apple School Manageru.  Další informace najdete v tématu [Automatická registrace zařízení MacOS pomocí Apple School Manageru nebo program registrace zařízení](../enrollment/device-enrollment-program-enroll-macos.md).

#### <a name="new-intune-device-subscription-sku--3312071--"></a>Nová SKU předplatného zařízení Intune<!--3312071-->
Abychom v podnicích pomohli snížit náklady na správu zařízení, nabízíme teď novou skladovou položku pro předplatné na základě zařízení. Tato skladová položka je licencovaná měsíčně podle počtu zařízení. Ceny se liší podle licenčního programu. Je k dispozici přímo prostřednictvím centra pro správu Microsoft 365, a to prostřednictvím služby [smlouva Enterprise](https://www.microsoft.com/licensing/licensing-programs/enterprise?activetab=enterprise-tab:primaryr2) (EA), [smlouvy o poskytování produktů a služeb](https://www.microsoft.com/licensing/mpsa/default) (MPSA), [Microsoft Open Agreement](https://partner.microsoft.com/licensing/licensing-agreements)a [poskytovatele Cloud Solution Provider](https://www.microsoftpartnercommunity.com/t5/Partnership-101/What-is-the-Cloud-Solution-Provider-CSP-program/td-p/2453) (CSP).

### <a name="device-management"></a>Správa zařízení

#### <a name="temporarily-pause-kiosk-mode-on-android-devices-to-make-changes---3041935---"></a>Dočasně pozastavit celoobrazovkový režim na zařízeních s Androidem a provést změny<!-- 3041935 -->
Při používání zařízení s Androidem v beznabídkovém režimu s více aplikacemi může správce IT potřebovat udělat v zařízení změny. Tato aktualizace zahrnuje nová nastavení veřejného terminálu s více aplikacemi, která správcům IT umožňuje dočasně pozastavit celoobrazovkový režim pomocí PIN kódu a získat přístup k celému zařízení.
Nastavení veřejného terminálu najdete v tématu [omezení pro zařízení s Androidem Enterprise](../configuration/device-restrictions-android-for-work.md).

#### <a name="enable-virtual-home-button-on-android-enterprise-kiosk-devices----3042021---"></a>Povolit virtuální domovské tlačítko na zařízeních s Androidem Enterprise <!-- 3042021 -->
Nové nastavení umožní uživatelům klepnutím na softwarové tlačítko přepínat mezi aplikací Managed Home Screen a jinými přiřazenými aplikacemi na zařízení v beznabídkovém režimu s více aplikacemi. Toto nastavení je zvláště užitečné v situacích, kdy beznabídková aplikace uživatele nereaguje správně na tlačítko Zpět. Toto nastavení budete moci nakonfigurovat pro zařízení s Androidem ve vlastnictví firmy pro použití s jednou aplikací. Pokud chcete nakonfigurovat **Virtuální tlačítko Domů**, na webu Azure Portal přejděte na Intune > Konfigurace zařízení. Vyberte aktuální profil konfigurace zařízení nebo vytvořte nový a upravte nastavení beznabídkového režimu.
Nastavení veřejného terminálu najdete v tématu [omezení pro zařízení s Androidem Enterprise](../configuration/device-restrictions-android-for-work.md).




<!-- ########################## -->
## <a name="october-2018"></a>Říjen 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="access-to-key-profile-properties-using-the-company-portal-app---772203---"></a>Přístup k vlastnostem klíčového profilu pomocí aplikace Portál společnosti<!-- 772203 -->
Koncoví uživatelé teď mají přístup ke klíčovým vlastnostem účtu a akcím, jako je například resetování hesla, z aplikace Portál společnosti. 

#### <a name="3rd-party-keyboards-can-be-blocked-by-app-settings-on-ios---1248481---"></a>nastavení aplikací v iOS můžou blokovat klávesnice třetích stran.<!-- 1248481 -->
Na zařízeních s iOSem můžou správci Intune zablokovat použití klávesnic jiných výrobců pro přístup k datům organizace z aplikací chráněných zásadami. Když budou nastavené Zásady ochrany aplikací (APP) k blokování klávesnic jiných výrobců, uživatelům zařízení se při první interakci s firemními daty pomocí klávesnice jiného výrobce zobrazí zpráva. Všechny jiné možnosti než nativní klávesnice budou zablokované a uživatelům zařízení se nezobrazí. Uživatelům se dialog se zprávou zobrazí jenom jednou. 

#### <a name="user-account-access-of-intune-apps-on-managed-android-and-ios-devices---1248496---"></a>Přístup uživatelských účtů k aplikacím Intune na spravovaných zařízeních s Androidem a iOS<!-- 1248496 -->
Jako správce Microsoft Intune můžete řídit, které uživatelské účty se přidají do aplikací Microsoft Office na spravovaných zařízeních. Můžete omezit přístup jenom na povolené uživatelské účty organizace a zablokovat osobní účty zaregistrovaných zařízení. 

#### <a name="outlook-ios-and-android-app-configuration-policy--1828527---"></a>Zásady konfigurace aplikace Outlook pro iOS a Android<!--1828527 -->
Teď můžete vytvořit zásadu konfigurace aplikace Outlook pro iOS a Android pro místní uživatele, kteří využívají základní ověřování pomocí protokolu ActiveSync. Další nastavení konfigurace se přidají po jejich povolení pro Outlook pro iOS a Android.

#### <a name="office-365-pro-plus-language-packs---1833450---"></a>Jazykové sady pro sadu Office 365 pro plus<!-- 1833450 -->
Jako správce Intune budete moct nasadit další jazyky pro aplikace Office 365 Pro Plus spravované prostřednictvím Intune. Seznam dostupných jazyků zahrnuje **Typ** jazykové sady (Základní, Částečná a Kontrola pravopisu). Na portálu Azure Portal vyberte **Microsoft Intune** > **Klientské aplikace** > **Aplikace** > **Přidat**. V okně **Přidat aplikaci** v seznamu **Typ aplikace** vyberte v části **Sada Office 365** možnost **Windows 10**. V okně **Nastavení sady aplikací** vyberte **Jazyky**.

#### <a name="windows-line-of-business-lob-apps-file-extensions---1884873---"></a>Obchodní aplikace (LOB) – přípony souborů aplikací pro Windows<!-- 1884873 -->
Přípony souborů pro obchodní aplikace Windows teď budou zahrnovat soubory *. msi*, *. appx*, *. appxbundle*, *. msix*a *. msixbundle*. Aplikaci můžete v Microsoft Intune přidat výběrem možností **Klientské aplikace** > **Aplikace** > **Přidat**. Zobrazí se podokno **Přidat aplikaci**, které vám umožní vybrat **Typ aplikace**. Pro obchodní aplikace pro Windows vyberte jako typ aplikace **Obchodní aplikace**, vyberte **Soubor balíčku aplikace** a pak zadejte instalační soubor s příslušnou příponou.

#### <a name="windows-10-app-deployment-using-intune---2309001---"></a>Nasazení aplikací pro Windows 10 pomocí Intune<!-- 2309001 -->
V rámci stávající podpory obchodních aplikací a Microsoft Store pro obchodní aplikace můžou správci pomocí Intune nasadit většinu stávajících aplikací v organizaci pro koncové uživatele na zařízeních s Windows 10. Správci mohou přidávat, instalovat a odinstalovávat aplikace pro uživatele Windows 10 v různých formátech, jako jsou MSI, Setup.exe nebo MSP. Před stažením a instalací Intune vyhodnotí pravidla požadavků a prostřednictvím centra akcí Windows 10 upozorní koncové uživatele na stav nebo požadavky na restartování. Tato funkce účinně uvolňuje ruce organizacím, které chtějí přesunout tuto úlohu do Intune a do cloudu. Tato funkce je v tuto chvíli ve veřejné verzi Preview. Očekáváme, že během několik dalších měsíců přidáme k této funkci důležité nové schopnosti. 

#### <a name="app-protection-policy-app-settings-for-web-data---2662995---"></a>Nastavení zásad ochrany aplikací (APP) pro webová data<!-- 2662995 -->
Nastavení zásad ochrany aplikací (APP) pro webový obsah na zařízeních s Androidem a iOS bude aktualizované, aby lépe pracovalo s webovými odkazy http a https a také s přenosy dat prostřednictvím univerzálních odkazů iOS a odkazů aplikací pro Android. 

#### <a name="end-user-device-and-app-content-menu---2771453---"></a>Nabídka obsahu zařízení a aplikace pro koncové uživatele<!-- 2771453 -->
Koncoví uživatelé teď můžou pomocí místní nabídky zařízení a aplikací aktivovat běžné akce, jako jsou například přejmenování zařízení nebo kontrola dodržování předpisů. 

#### <a name="windows-company-portal-keyboard-shortcuts---2771518---"></a>Klávesové zkratky v Portálu společnosti pro Windows<!-- 2771518 -->
Koncoví uživatelé teď budou moct aktivovat akce aplikací a zařízení v aplikaci Portál společnosti pro Windows pomocí klávesových zkratek (akcelerátorů).

#### <a name="require-non-biometric-pin-after-a-specified-timeout---1506985---"></a>Po zadaném časovém limitu vyžadovat kód PIN, který není biometrické<!-- 1506985 -->
Po uplynutí časového limitu určeného správcem Intune požaduje nebiometrický kód PIN. Služba tak lépe zabezpečí aplikace s podporou Správy mobilních aplikací (MAM), protože omezí použití biometrické identifikace pro přístup k firemním datům. Toto nastavení má vliv na uživatele, kteří pro přístup k aplikacím s podporou APP/MAM používají Touch ID (iOS), Face ID (iOS), Biometriku Androidu nebo jiné budoucí způsoby biometrického ověřování. S tímto nastavením mají správci Intune přesnější kontrolu nad přístupem uživatelů, takže mohou vyloučit případy, kdy zařízení s více otisky prstů nebo jinými biometrickými metodami přístupu může odhalit firemní data nesprávnému uživateli. Na portálu Azure Portal otevřete **Microsoft Intune**. Vyberte **Klientské aplikace** > **Zásady ochrany aplikací** > **Přidat zásadu** > **Nastavení**. Najděte část **Přístup** s konkrétními nastaveními. Informace o nastavení přístupu najdete v [nastavení iOSu](../apps/app-protection-policy-settings-ios.md#access-requirements) a [nastavení Androidu](../apps/app-protection-policy-settings-android.md#access-requirements).

#### <a name="intune-app-data-transfer-settings-on-ios-mdm-enrolled-devices---2244713---"></a>Nastavení přenosu dat aplikací v Intune na zařízeních zaregistrovaných pro iOS MDM<!-- 2244713 -->
Ovládání nastavení Intune APP pro přenos dat na zařízeních s iOSem zaregistrovaných v MDM můžete oddělit od zadání identity registrovaného uživatele, která se označuje také jako hlavní název uživatele (UPN). Správci, kteří nepoužívají aplikaci IntuneMAMUPN, nezaznamenají změnu chování. Pokud je tato funkce k dispozici, musí správci, kteří k řízení chování při přenosech dat na registrovaných zařízeních používají Intune MAMUPN, zkontrolovat nové nastavení a podle potřeby aktualizovat nastavení APP.

#### <a name="windows-10-win32-apps---2617325---"></a>Aplikace Win32 pro Windows 10<!-- 2617325 -->
Aplikace Win32 můžete nakonfigurovat tak, aby se instalovaly v kontextu uživatele pro jednotlivé uživatele, nebo pro všechny uživatele zařízení.

#### <a name="windows-win32-apps-and-powershell-scripts---2617330---"></a>Aplikace Windows Win32 a skripty PowerShellu<!-- 2617330 -->
Koncoví uživatelé už nemusí být kvůli instalaci aplikací Win32 nebo spouštění powershellových skriptů přihlášení k zařízení. 

#### <a name="troubleshooting-client-app-installation---1363711---"></a>Řešení potíží s instalací klientské aplikace<!-- 1363711 -->
Potíže s instalací klientských aplikací můžete řešit tak, že se podíváte do sloupce s názvem **Instalace aplikace** v okně **Řešení potíží**. Okno **Řešení potíží** zobrazíte tak, že na portálu Intune vyberete **Řešení potíží** v části **Nápověda a podpora**.

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="create-dns-suffixes-in-vpn-configuration-profiles-on-devices-running-windows-10---1333668---"></a>Vytvoření přípon DNS v konfiguračních profilech sítě VPN na zařízeních s Windows 10<!-- 1333668 -->
Při vytváření profilu konfigurace zařízení v síti VPN (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Windows 10 a novější** Platforma > **VPN** pro typ profilu), zadáváte nastavení DNS. S touto aktualizací můžete také zadat v Intune více **přípon DNS**. Pokud použijete přípony DNS, můžete k vyhledání síťového prostředku použít jeho krátký název místo plně kvalifikovaného názvu domény (FQDN). V této aktualizaci můžete v Intune změnit pořadí přípon DNS.
Seznam aktuálních nastavení DNS je v [nastavení sítě VPN ve Windows 10](../configuration/vpn-settings-windows-10.md#dns-settings).
Platí pro: zařízení s Windows 10

#### <a name="support-for-always-on-vpn-for-android-enterprise-work-profiles---1333705---"></a>Podpora pro pracovní profily s Androidem Enterprise v rámci vždycky zapnuté sítě VPN<!-- 1333705 -->
V této aktualizaci můžete využít neustále aktivní připojení VPN na zařízeních s Androidem Enterprise, která používají spravované pracovní profily. Neustále aktivní připojení VPN zůstávají ve spojení nebo se ihned znovu připojí, jakmile uživatel odemkne zařízení, zařízení se restartuje nebo se změní bezdrátová síť. Připojení také můžete přepnout do „zamčeného“ režimu, který blokuje veškerý síťový provoz, dokud není připojení VPN zase aktivní.
Neustále aktivní připojení VPN můžete povolit v nastavení **Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Android Enterprise** pro platformu > **Omezení zařízení** > **Možnosti připojení**.

#### <a name="issue-scep-certificates-to-user-less-devices---1744554---"></a>Vystavení certifikátů SCEP pro zařízení bez uživatelů<!-- 1744554 -->
Certifikáty se v současnosti vydávají jenom uživatelům. S touto aktualizací můžete certifikáty SCEP vydat i zařízením, včetně zařízení bez uživatelů, jako jsou terminály (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Windows 10 a novější** pro platformu > **Certifikát SCEP** pro profil). Další aktualizace zahrnují:
- Vlastnost **Subjekt** v profilu SCEP je nyní vlastní textové pole, které může obsahovat nové proměnné. 
- Vlastnost **Alternativní název subjektu (SAN)** v profilu SCEP má nyní formát tabulky a může obsahovat nové proměnné. Správce může do tabulky přidat atribut a vyplnit hodnotu vlastního textového pole. Alternativní název subjektu (SAN) podporuje následující atributy: 
  - DNS
  - E-mailová adresa
  - Hlavní název uživatele (UPN)

  Tyto nové proměnné můžete přidat jako statický text do textového pole s vlastní hodnotou. Například atribut DNS můžete přidat jako `DNS = {{AzureADDeviceId}}.domain.com`.

  > [!NOTE]
  > Složené závorky, středníky a symboly kanálu {}; | nebudou fungovat na statickém textu sítě SAN. Do složených závorek můžete uzavřít jenom jednu z nových proměnných certifikátu zařízení, aby mohla být přijata jako `Subject` nebo `Subject alternative name`. 

Nové proměnné certifikátu zařízení:  

```
"{{AAD_Device_ID}}",
"{{Device_Serial}}",
"{{Device_IMEI}}",
"{{SerialNumber}}",
"{{IMEINumber}}",
"{{AzureADDeviceId}}",
"{{WiFiMacAddress}}",
"{{IMEI}}",
"{{DeviceName}}",
"{{FullyQualifiedDomainName}}",
"{{MEID}}",
```

> [!NOTE]
> - `{{FullyQualifiedDomainName}}` funguje jenom pro Windows a zařízení připojená k doméně. 
> - Když do subjektu nebo alternativního názvu subjektu (SAN) pro certifikát zařízení zadáváte vlastnosti zařízení, jako je IMEI, sériové číslo a plně kvalifikovaný název domény, uvědomte si, že osoba, která má k zařízení přístup, může tyto vlastnosti zfalšovat. 

V části [Vytvoření profilu certifikátu SCEP](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile) je seznam aktuálních proměnných při vytvoření konfiguračního profilu SCEP. 

Platí pro: Windows 10 a novější a iOS, podporuje síť Wi-Fi

#### <a name="remotely-lock-uncompliant-devices---2064495---"></a>Vzdáleně uzamknout zařízení, která nedodržují předpisy<!-- 2064495 -->
Pokud zařízení nevyhovuje, můžete vytvořit akci, která vychází ze zásady dodržování předpisů a která zařízení vzdáleně zamkne. V Intune vyberte **Dodržování předpisů zařízením**, vytvořte novou nebo vyberte některou ze stávajících zásad > **Vlastnosti**. Vyberte **Akce při nedodržení předpisů** > **Přidat** a zvolte, že chcete zařízení vzdáleně zamknout.
Podporované platformy: 
- Android
- iOS
- macOS
- Windows 10 Mobile 
- Windows Phone 8.1 a novější 

#### <a name="windows-10-and-later-kiosk-profile-improvements-in-the-azure-portal---2748224---"></a>Vylepšení profilu veřejného terminálu Windows 10 a novějšího v Azure Portal<!-- 2748224 -->
Tato aktualizace zahrnuje následující vylepšení konfiguračního profilu zařízení s beznabídkovým režimem s Windows 10 (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Windows 10 a novější** pro platformu > **Beznabídkový režim (Preview)** pro typ profilu): 
- V současnosti můžete na stejném zařízení vytvářet více profilů beznabídkového režimu. Po této aktualizaci bude Intune u každého zařízení podporovat jenom jeden profil. Pokud přesto potřebujete více profilů beznabídkového režimu, můžete použít vlastní identifikátor URI.
- V profilu **Beznabídkový režim s více aplikacemi** můžete vybrat velikost dlaždice aplikace a určit pořadí **rozložení nabídky Start** v mřížce aplikace. Pokud chcete provádět vlastní úpravy většího rozsahu, pokračujte k odeslání souboru XML.
- Nastavení aplikace Kiosk Browser se přesouvají do nastavení **Veřejný terminál**. V současnosti má nastavení **Kiosk Web Browser** na webu Azure Portal vlastní kategorii.
Platí pro: Windows 10 a novější

#### <a name="pin-prompt-when-you-change-fingerprints-or-face-id-on-an-ios-device----2637704----"></a>Výzva k zadání kódu PIN při změně otisků prstů nebo ID obličeje na zařízení s iOS <!-- 2637704  -->
Uživatelům se teď po provedení biometrických změn na zařízení s iOSem zobrazuje výzva k zadání kódu PIN. Týká se to i změn zaregistrovaných otisků prstů nebo Face ID. Načasování výzvy závisí na konfiguraci časového limitu *Překontrolovat požadavky na přístup za (minuty)* .  Pokud není kód PIN nastavený, zobrazí se uživateli výzva k jeho nastavení. 
 
Tato funkce je dostupná jen pro iOS a vyžaduje zapojení aplikací, které integrují sadu Intune APP SDK pro iOS verze 9.0.1 nebo novější. Integrace této sady SDK je nezbytná kvůli vynucení tohoto chování u cílových aplikací. K této integraci dochází průběžně a závisí na týmech konkrétních aplikací. Mezi zapojené aplikace patří například WXP, Outlook, Managed Browser a Yammer.

#### <a name="network-access-control-support-on-ios-vpn-clients---1333693---"></a>Podpora řízení přístupu k síti u klientů VPN iOS<!-- 1333693 -->
V této aktualizaci zavádíme nové nastavení, kterým můžete při vytváření konfiguračního profilu VPN pro Cisco AnyConnect, F5 Access a Citrix SSO pro iOS povolit řízení přístupu k síti (NAC). Toto nastavení umožní zahrnutí ID NAC zařízení do profilu VPN. V současné době neexistují žádní klienti VPN ani partnerská řešení NAC podporující toto nové ID NAC, ale jakmile se tak stane, budeme vás informovat prostřednictvím [blogového příspěvku o podpoře](ttps://aka.ms/iOS12_and_vpn).

Abyste mohli používat NAC, budete muset:
1. vyjádřením výslovného souhlasu povolit službě Intune zahrnout ID zařízení do profilů VPN,
2. aktualizovat software nebo firmware poskytovatele NAC pomocí pokynů, které získáte přímo od svého poskytovatele NAC.

Informace o tomto nastavení v profilu VPN v iOSu najdete v článku, který se zabývá [přidáním nastavení VPN v zařízeních s iOSem v Microsoft Intune](../configuration/vpn-settings-ios.md). Další informace o řízení přístupu k síti najdete v článku [Integrace řešení pro řízení přístupu k síti (NAC) do Intune](../protect/network-access-control-integrate.md). 

Platí pro: iOS

#### <a name="remove-an-email-profile-from-a-device-even-when-theres-only-one-email-profile---1818139---"></a>Odebrat e-mailový profil ze zařízení, i když je k dispozici jenom jeden e-mailový profil<!-- 1818139 -->
Dříve nebylo možné ze zařízení odebrat e-mailový profil, *pokud* jich tam nebylo více. S touto aktualizací se toto chování změní. Teď můžete e-mailový profil odebrat, i když na zařízení není žádný další. Podrobnosti najdete v tématu [Přidání e-mailového nastavení na zařízení pomocí Intune](../configuration/email-settings-configure.md).

#### <a name="powershell-scripts-and-aad---2309469---"></a>PowerShellové skripty a AAD<!-- 2309469 -->
Cílem powershellových skriptů v Intune mohou být skupiny zabezpečení zařízení služby AAD.

#### <a name="new-required-password-type-default-setting-for-android-android-enterprise---2649963---"></a>Nové nastavení "požadovaný typ hesla" pro Android, Android Enterprise<!-- 2649963 -->
Když vytvoříte nové zásady dodržování předpisů (**Intune** > **Dodržování předpisů zařízením** > **Zásady** > **Vytvořit zásadu** > **Android** nebo **Android Enterprise** pro Platforma > Zabezpečení systému), výchozí hodnota pro **Požadovaný typ hesla** se změní:

z: Výchozí ze zařízení na: Aspoň číslice.

Platí pro Android, Android Enterprise.

Pokud se chcete podívat na tato nastavení, přejděte do [Androidu](../protect/compliance-policy-create-android.md) nebo [Androidu Enterprise](../protect/compliance-policy-create-android-for-work.md).

#### <a name="use-a-pre-shared-key-in-a-windows-10-wi-fi-profile---2662938---"></a>Použití předsdíleného klíče v profilu Wi-Fi s Windows 10<!-- 2662938 -->
S touto aktualizací můžete k ověření konfiguračního profilu sítě Wi-Fi pro Windows 10 použít předsdílený klíč (PSK) s protokolem zabezpečení WPA/WPA2-osobní. U zařízení s Windows 10 a aktualizací ze října 2018 můžete také zadat konfiguraci nákladů pro síť s měřením dat.

Pokud chcete použít předsdílený klíč, musíte v současnosti importovat profil Wi-Fi nebo vytvořit vlastní profil. Seznam aktuálních nastavení je v [nastavení sítě Wi-Fi pro Windows 10](../configuration/wi-fi-settings-windows.md). 

#### <a name="remove-pkcs-and-scep-certificates-from-your-devices---3218390---"></a>Odebrání certifikátů PKCS a SCEP z vašich zařízení<!-- 3218390 -->
V některých scénářích zůstávaly certifikáty PKCS a SCEP na zařízeních i po odebrání zásad ze skupiny, odstranění nasazené konfigurace nebo nastavení pro dodržování předpisů nebo aktualizaci existujícího profilu SCEP nebo PKCS správcem. Tato aktualizace toto chování mění. Budou existovat určité scénáře, kdy se certifikáty PKCS a SCEP ze zařízení odeberou, a jiné scénáře, kdy tyto certifikáty zůstanou na zařízení. Tyto scénáře najdete v tématu [Odebrání certifikátů SCEP a PKCS v Microsoft Intune](../protect/remove-certificates.md).

#### <a name="use-gatekeeper-on-macos-devices-for-compliance---2504381---"></a>Použití serveru gatekeeper na zařízeních macOS pro dodržování předpisů<!-- 2504381 -->
Tato aktualizace zahrnuje Gatekeeper pro macOS, který umožňuje u zařízení vyhodnotit dodržování předpisů. Pokud chcete nastavit vlastnost Gatekeeper, přejděte na článek [Přidání zásad dodržování předpisů pro zařízení s macOS v Intune](../protect/compliance-policy-create-mac-os.md).


### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="apply-autopilot-profile-to-enrolled-win-10-devices-not-already-registered-for-autopilot---1558983---"></a>Použít profil autopilotu pro zaregistrovaná zařízení s Windows 10, která ještě nejsou zaregistrovaná pro automatický pilotní<!-- 1558983 -->
Profily Autopilotu můžete použít u zaregistrovaných zařízení s Windows 10, která nejsou zaregistrovaná do Autopilotu. V profilu Autopilotu zvolte možnost **Převést všechna cílová zařízení na AutoPilot**, abyste mohli k automatické registraci zařízení bez Autopilotu použít službu nasazení Autopilotu. Vyřízení registrace trvá 48 hodin. Jakmile bude registrace zařízení zrušena a zařízení bude resetováno, Autopilot zajistí registraci.

#### <a name="create-and-assign-multiple-enrollment-status--page-profiles-to-azure-ad-groups---2526564---"></a>Vytvoření a přiřazení více profilů stránky stavu registrace do skupin Azure AD<!-- 2526564 -->
Nově můžete [vytvořit a přiřadit](../enrollment/windows-enrollment-status.md) více profilů stránky o stavu registrace skupinám Azure ADD.

#### <a name="migration-from-device-enrollment-program-to-apple-business-manager-in-intune--2748613--"></a>Migrace z Program registrace zařízení do Apple Business Manageru v Intune<!--2748613-->
V Intune funguje Apple Business Manager (ABM), takže je možné upgradovat účet z Programu registrace zařízení (DEP) na ABM. Proces v Intune je stejný. Pokud chcete účet Apple upgradovat z DEP na ABM, přejděte na [https://support.apple.com/HT208817]( https://support.apple.com/HT208817).

#### <a name="alert-and-enrollment-status-tabs-on-the-device-enrollment-overview-page--2748656--"></a>Karty stavu výstrah a registrace na stránce Přehled registrace zařízení<!--2748656-->
Na stránce s přehledem registrace zařízení se teď zobrazují upozornění a chyby registrace na samostatných kartách.

#### <a name="enrollment-abandonment-report---1382924---"></a>Sestava opuštění registrace<!-- 1382924 -->
Nová sestava, která poskytuje podrobné informace o opuštěných registracích, je k dispozici v části **Registrace zařízení** > **Monitorování**. Další informace najdete v článku, který se věnuje [sestavě opuštění Portálu společnosti](../enrollment/enrollment-report-company-portal-abandon.md).

#### <a name="new-azure-active-directory-terms-of-use-feature---2870393---"></a>Nové funkce Azure Active Directory podmínek použití<!-- 2870393 -->
Azure Active Directory má funkci podmínek použití, kterou můžete využít místo stávajících podmínek a ujednání služby Intune. Funkce podmínek použití služby Azure AD poskytuje větší flexibilitu ohledně toho, které podmínky a kdy se mají zobrazovat, lepší podporu lokalizace, větší kontrolu nad tím, jak se podmínky vykreslují, a vylepšené generování sestav. Funkce podmínek použití služby Azure AD vyžaduje Azure Active Directory Premium P1, která je také součástí sady Enterprise Mobility + Security E3. Další informace najdete v článku [Správa firemních podmínek a ujednání pro přístup uživatelů](../enrollment/terms-and-conditions-create.md).

#### <a name="android-device-owner-mode-support--3188762--"></a>Podpora režimu vlastníka zařízení s Androidem<!--3188762-->
U registrace mobilního zařízení Samsung Knox teď Intune podporuje registraci zařízení do režimu správy Vlastník zařízení Android. Uživatelé připojení prostřednictvím Wi-Fi nebo mobilních sítí mohou svá zařízení při prvním zapnutí registrovat několika klepnutími. Další informace najdete v článku věnovaném [automatické registraci zařízení s Androidem pomocí technologie Knox Mobile Enrollment od Samsungu](../enrollment/android-samsung-knox-mobile-enroll.md).

### <a name="device-management"></a>Správa zařízení
#### <a name="new-settings-for-software-updates-----1907869---"></a>Nová nastavení pro aktualizace softwaru  <!-- 1907869 -->  
- Teď můžete nakonfigurovat některá oznámení, která upozorňují koncové uživatele na restarty, které jsou nutné k dokončení instalace nejnovějších aktualizací softwaru.   
- Nyní můžete nakonfigurovat výzvu k restartování pro restartování, ke kterým dochází mimo pracovní dobu, která podporuje BYOD scénáře.

#### <a name="group-windows-autopilot-enrolled-devices-by-correlator-id---2075110---"></a>Seskupení zařízení s Windows autopilotem zaregistrovaných podle ID korelace<!-- 2075110 -->
Intune teď podporuje seskupování zařízení s Windows podle ID korelátoru, pokud jsou zaregistrovaná pomocí [Autopilotu pro existující zařízení](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) v nástroji Configuration Manager. ID korelátoru je parametr konfiguračního souboru Autopilotu. Intune automaticky nastaví [atribut enrollmentProfileName zařízení služby Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) tak, aby odpovídal nastavení OfflineAutopilotprofile-<correlator ID>. Umožní se tím, aby se pro offline registrace Autopilotu vytvořily libovolné dynamické skupiny Azure AD na základě ID korelátoru prostřednictvím atributu enrollmentprofileName. Další informace najdete v tématu [Windows Autopilot pro existující zařízení](../enrollment/enrollment-autopilot.md#windows-autopilot-for-existing-devices).

#### <a name="intune-app-protection-policies---2984657---"></a>Zásady ochrany aplikací Intune<!-- 2984657 -->
Zásady ochrany aplikací Intune umožňují pro aplikace chráněné přes Intune (například Microsoft Outlook a Microsoft Word) nakonfigurovat různá nastavení ochrany dat. Změnili jsme vzhled a chování těchto nastavení pro [iOS](../apps/app-protection-policy-settings-ios.md) i [Android](../apps/app-protection-policy-settings-android.md) , aby bylo snazší najít jednotlivá nastavení. Existují tři kategorie nastavení zásad:
- **Přemístění dat** – tato skupina obsahuje kontrolní mechanismy ochrany před únikem informací, například omezení operací Vyjmout, Kopírovat, Vložit a Uložit jako. Tato nastavení určují, jak uživatelé pracují s daty v aplikacích.
- **Požadavky na přístup** – tato skupina obsahuje možnosti kódu PIN pro jednotlivé aplikace, které určují, jak koncový uživatel získá přístup k aplikacím v pracovním kontextu.  
- **Podmíněné spouštění** – tato skupina obsahuje nastavení, jako je minimální verze operačního systému, detekce zařízení s jailbreakem a rootem a období odkladu pro offline režim.  
  
Funkce nastavení se nezmění, ale při práci v toku vytváření zásad bude snazší je najít.

#### <a name="restricts-apps-and-block-access-to-company-resources-on-android-devices---2451462----"></a>Omezí aplikace a zablokuje přístup k firemním prostředkům na zařízeních s Androidem.<!-- 2451462  -->  
V části **Dodržování předpisů zařízením** > **Zásady** > **Vytvořit zásadu** > **Android** > **Zabezpečení systému** v oddílu *Zabezpečení zařízení* existuje nové nastavení s názvem **Omezené aplikace**. Nastavení **Omezené aplikace** pomocí zásad dodržování předpisů blokuje přístup k firemním prostředkům, pokud jsou v zařízení nainstalované některé aplikace. Zařízení se považuje za neodpovídající předpisům, dokud se z něj aplikace s omezeným přístupem neodeberou.
Platí pro: 
- Android

### <a name="intune-apps"></a>Aplikace Intune

#### <a name="intune-will-support-a-maximum-package-size-of-8-gb-for-lob-apps---1727158---"></a>Intune bude podporovat maximální velikost balíčku 8 GB pro obchodní aplikace.<!-- 1727158 -->
Služba Intune zvýšila maximální velikost balíčku u obchodních aplikací na 8 GB. Další informace najdete v článku [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

#### <a name="add-custom-brand-image-for-company-portal-app---1916266---"></a>Přidat vlastní obrázek značky pro aplikaci Portál společnosti<!-- 1916266 -->
Správce služby Microsoft Intune může nahrát obrázek vlastní značky, který se v aplikaci Portál společnosti pro iOS zobrazí jako pozadí stránky s profilem uživatele. Další informace o konfiguraci aplikace Portál společnosti najdete v tématu [Konfigurace aplikace Portál společnosti služby Microsoft Intune](../apps/company-portal-app.md).

#### <a name="intune-will-maintain-the-office-localized-language-when-updating-office-on-end-users-machines---2971030---"></a>Intune bude při aktualizaci Office na počítačích koncových uživatelů udržovat lokalizovaný jazyk Office.<!-- 2971030 -->
Když Intune nainstaluje Office na počítače koncových uživatelů, získají koncoví uživatelé automaticky stejné jazykové sady, které měli s předchozími instalacemi Office .MSI. Další informace najdete v článku [Přiřazení aplikací Office 365 k zařízením s Windows 10 pomocí Microsoft Intune](../apps/apps-add-office365.md).

### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="new-intune-support-experience-in-the-microsoft-365-device-management-portal---3076965---"></a>Nové prostředí podpory Intune na portálu pro správu zařízení Microsoft 365<!-- 3076965 -->
Na [portálu Správa zařízení Microsoft 365]( https://devicemanagement.microsoft.com) zavádíme nové prostředí pro nápovědu a podporu Intune. Nové prostředí vám umožňuje popsat problém vlastními slovy a získat přehled možností řešení potíží a postupy z webu, jak problém opravit. Tato řešení jsou nabízena prostřednictvím algoritmů strojového učení založeného na pravidlech, které se řídí dotazy uživatelů.  

Kromě pokynů ke konkrétnímu problému můžete také využít nového pracovního postupu vytváření případů a otevřít případ podpory e-mailem nebo telefonicky.  

U zákazníků v této vlně nasazení toto nové prostředí nahradí aktuální prostředí pro nápovědu a podporu, které obsahuje statickou skupinu předem vybraných možností. Ty jsou založené na oblasti konzoly, ve které se nacházíte při otevření nápovědy a podpory.  

*Tato nová pomocná a podpůrná prostředí se navádějí na některé, ale ne všechny klienty a jsou k dispozici na portálu pro správu zařízení. Účastníci tohoto nového prostředí se náhodně vyberou z dostupných tenantů Intune. Do rozšiřování zavedení budou přidány noví klienti.*  

Další informace najdete v tématech [Nápověda a podpora](get-support.md#help-and-support-experience) v tématu Jak získat podporu pro Microsoft Intune.  

#### <a name="powershell-module-for-intune--preview-available---951068---"></a>Modul PowerShell pro Intune – náhled k dispozici<!-- 951068 -->
Nový modul prostředí PowerShell, který poskytuje podporu pro rozhraní Intune API prostřednictvím Microsoft Graphu, je teď dostupný ve verzi Preview na [GitHubu](https://aka.ms/intunepowershell). Podrobnosti o tom, jak tento modul používat, najdete v souboru README v uvedeném umístění.

<!-- ########################## -->
## <a name="september-2018"></a>Září 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="remove-duplication-of-app-protection-status-tiles---3083391---"></a>Odebrat duplicity dlaždic stavu ochrany aplikací<!-- 3083391 -->
Dlaždice **Stav uživatele pro iOS** a **Stav uživatele pro Android** se vyskytovaly na stránce **Klientské aplikace – přehled** i na stránce **Klientské aplikace – stav ochrany aplikace**. Dlaždice stavu byly odebrány ze stánky **Klientské aplikace – přehled**, aby se zabránilo duplicitě. 

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="support-for-more-third-party-certification-authorities-ca---3093107---"></a>Podpora dalších certifikačních autorit (CA) třetích stran<!-- 3093107 -->
Když použijete protokol SCEP (Simple Certificate Enrollment Protocol), můžete teď vydat nové certifikáty a prodloužit platnost certifikátů na mobilních zařízeních s Windows, iOS, Androidem a macOS.

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="intune-moves-to-support-ios-10-and-later---2454656---"></a>Intune se přesune na podporu iOS 10 a novější.<!-- 2454656 -->  
Registrace Intune, Portál společnosti a spravovaný prohlížeč nyní podporují pouze zařízení s iOSem verze 10 a novějších. Pokud chcete zjistit, na která zařízení nebo uživatele ve vaší organizaci to bude mít vliv, přejděte do Intune na webu Azure Portal > **Zařízení** > **Všechna zařízení**. Podrobnosti o verzi operačního systému zobrazíte tak, že si vyfiltrujete operační systém a potom kliknete na **Sloupce**. Požádejte tyto uživatele, aby si upgradovali zařízení na podporovanou verzi operačního systému.  

Pokud máte některé z níže uvedených zařízení nebo chcete některé z těchto zařízení zaregistrovat, mějte na paměti, že tato zařízení podporují jenom iOS 9 a dřívější verze.  Pokud chcete dále používat Portál společnosti Intune, je nutné tato zařízení upgradovat na zařízení podporující iOS 10 nebo novější verze:  

* iPhone 4S 
* iPod Touch  
* iPad 2 
* iPad (3. generace) 
* iPad Mini (1. generace)  

### <a name="device-management"></a>Správa zařízení

#### <a name="microsoft-365-device-management-administration-center---3078424---"></a>Centrum pro správu správy zařízení Microsoft 365<!-- 3078424 -->
Jednou z příslibů Microsoft 365 je zjednodušená správa a za rok jsme Microsoft 365 služby back-endu integrovaly do back-endové služby, které poskytují ucelené scénáře, jako je Intune a podmíněný přístup Azure AD. Nové [centrum pro správu Microsoft 365](https://devicemanagement.microsoft.com) je místem, kde můžete konsolidovat, zjednodušovat a integrovat prostředí pro správu. Pracovní prostor pro specialisty na správu zařízení poskytuje snadný přístup ke všem úkolům a informacím o správě zařízení a aplikací a úloh, které vaše organizace potřebuje. Očekáváme, že se stane primárním pracovním prostorem na cloudu pro výpočetní týmy koncových uživatelů organizací.


<!-- ########################## -->
## <a name="august-2018"></a>Srpen 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="packet-tunnel-support-for-ios-per-app-vpn-profiles-for-custom-and-pulse-secure-connection-types---1520957---"></a>Podpora tunelového připojení paketů pro profily sítě VPN pro iOS pro vlastní typy a typy připojení Pulse Secure<!-- 1520957 -->
Pokud používáte profily VPN pro jednotlivé aplikace pro iOS, můžete použít tunelování v aplikační vrstvě (proxy aplikace) nebo na úrovni paketů (tunel pro pakety). Tyto možnosti jsou dostupné u následujících typů připojení:
- Vlastní VPN
- Pulse Secure Pokud si nejste jisti, jakou hodnotu použít, vyhledejte informace v dokumentaci poskytovatele připojení VPN.

#### <a name="delay-when-ios-software-updates-are-shown-on-the-device---1949583---"></a>Zpoždění při zobrazení aktualizací softwaru iOS na zařízení<!-- 1949583 -->
V části Intune > **Aktualizace softwaru** > **Aktualizovat zásady pro iOS** můžete nakonfigurovat dny a časy, kdy se na zařízení nemají instalovat žádné aktualizace. V budoucí aktualizaci budete moct odložit čas, kdy se aktualizace softwaru viditelně zobrazí v zařízení, o 1–90 dní. 
Aktuální nastavení jsou uvedena v části [Konfigurace zásad aktualizace iOS v Microsoft Intune](../protect/software-updates-ios.md).

#### <a name="office-365-proplus-version---2213968---"></a>Verze sady Office 365 plus<!-- 2213968 -->
Při přiřazování aplikací Office 365 ProPlus k zařízením s Windows 10 pomocí Intune si můžete vybrat verzi Office. Na portálu Azure Portal vyberte **Microsoft Intune** > **Aplikace** > **Přidat aplikaci**. Potom z rozevíracího seznamu **Typ** vyberte **Office 365 ProPlus Suite (Windows 10)** . Volbou **Nastavení sady aplikací** otevřete související okno. V části **Aktualizační kanál** nastavte požadovanou hodnotu, například **Měsíčně**. Volitelně můžete odebrat ze zařízení koncových uživatelů jiné verze Office (msi) tak, že vyberete **Ano**. Vyberte **Konkrétní** a nainstalujte tak pro vybraný kanál na zařízeních koncových uživatelů konkrétní verzi Office. V tomto okamžiku můžete vybrat **konkrétní verzi** Office, která se má použít. Dostupné verze se budou v průběhu času měnit. Při vytváření nového nasazení tedy můžou být dostupné novější verze a některé starší verze nemusí být k dispozici. Aktuální nasazení budou dál nasazovat starší verzi, ale seznam verzí se bude průběžně aktualizovat podle kanálu. Další informace najdete v článku [Základní informace o aktualizačních kanálech Office 365 ProPlus](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus).

#### <a name="support-for-register-dns-setting-for-windows-10-vpn---2282852---"></a>Podpora pro registraci nastavení DNS pro síť VPN s Windows 10<!-- 2282852 -->
Od této aktualizace můžete profily sítě VPN ve Windows 10 nakonfigurovat tak, aby dynamicky registrovaly IP adresy přiřazené k rozhraní sítě VPN pomocí interní služby DNS bez nutnosti používat vlastní profily.
Informace o aktuálně dostupných nastaveních profilů VPN najdete v seznamu [Nastavení sítě VPN ve Windows 10](../configuration/vpn-settings-windows-10.md).

#### <a name="the-macos-company-portal-installer-now-includes-the-version-number-in-the-installer-file-name--2652728--"></a>Instalační služba macOS Portál společnosti nyní zahrnuje číslo verze v názvu souboru instalačního programu.<!--2652728-->

#### <a name="ios-automatic-app-updates---2729759---"></a>Automatické aktualizace aplikací pro iOS<!-- 2729759 -->
Automatické aktualizace aplikací fungují u aplikací licencovaných pro zařízení i uživatele v iOSu verze 11.0 a novějších.

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="windows-hello-will-target-users-and-devices---1106609---"></a>Windows Hello bude cílit na uživatele a zařízení<!-- 1106609 -->
Když vytvoříte zásady [Windows Hello pro firmy](../protect/windows-hello.md), bude platit pro všechny uživatele v organizaci (v celém tenantovi). Po této aktualizaci se tyto zásady s využitím zásad konfigurace zařízení budou dát použít také pro konkrétní uživatele nebo konkrétní zařízení (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Identity Protection** > **Windows Hello pro firmy**).
V Intune na portálu Azure Portal je konfigurace a nastavení Windows Hello nově k dispozici v částech **Registrace zařízení** i **Konfigurace zařízení**. **Registrace zařízení** cílí na celou organizaci (celého tenanta) a podporuje program Windows AutoPilot (OOBE). **Konfigurace zařízení** cílí na zařízení a uživatele používající zásadu aplikovanou při přihlášení.
Tato funkce platí pro:  
- Windows 10 a novější
- Windows Holographic for Business

#### <a name="zscaler-is-an-available-connection-for-vpn-profiles-on-ios---1769858---"></a>Zscaler je dostupné připojení pro profily sítě VPN v iOS.<!-- 1769858 -->
Při vytváření konfiguračního profilu VPN pro zařízení s iOSem (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **iOS** platforma > typ profilu **VPN**) existuje několik typů připojení, mimo jiné Cisco, Citrix a další. S touto aktualizací se mezi typy připojení přidává Zscaler. 
Dostupné typy připojení jsou uvedeny v části [Nastavení sítě VPN pro zařízení s iOSem](../configuration/vpn-settings-ios.md).

#### <a name="fips-mode-for-enterprise-wi-fi-profiles-for-windows-10---1879077---"></a>Režim FIPS pro profily firemní sítě Wi-Fi pro Windows 10<!-- 1879077 -->
Nově můžete pro podnikové profily Wi-Fi pro Windows 10 povolit na portálu Intune Azure režim FIPS (Federal Information Processing Standards). Pokud režim FIPS na vašich profilech Wi-Fi povolíte, ujistěte se, že je povolený v infrastruktuře sítě Wi-Fi.
Postup vytvoření profilu Wi-Fi najdete v článku [Nastavení Wi-Fi pro zařízení s Windows 10 a novější verzí v Intune](../configuration/wi-fi-settings-windows.md).

#### <a name="control-s-mode-on-windows-10-and-later-devices---public-preview---1958649---"></a>Řízení S režimem v zařízeních s Windows 10 a novějších verzích – Public Preview<!-- 1958649 -->
Od této aktualizace funkcí můžete vytvářet profil konfigurace zařízení, který přepne zařízení s Windows 10 z režimu S nebo uživatelům v přepnutí zařízení z režimu S zabrání. Funkci najdete v části Intune > **Konfigurace zařízení** > **Profily** >  **Windows 10 a novější** > **Upgrade edice a přepnutí režimu**.
Článek [Introducing Windows 10 in S mode](https://www.microsoft.com/windows/s-mode) (Představení Windows 10 v režimu S) poskytuje o režimu S podrobnější informace.
Platí pro: nejnovější build [Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/) (v období verze Preview).

#### <a name="windows-defender-atp-configuration-package-automatically-added-to-configuration-profile---2144658---"></a>Konfigurační balíček ochrany ATP v programu Windows Defender se automaticky přidal do konfiguračního profilu.<!-- 2144658 -->
Když používáte [Rozšířenou ochranu před internetovými útoky (ATP) a připojujete](../protect/advanced-threat-protection.md#onboard-devices-by-using-a-configuration-profile) zařízení k Intune, museli jste si dříve stáhnout konfigurační balíček a přidat ho do konfiguračního profilu. Od této aktualizace Intune automaticky načítá balíček z Centra zabezpečení v programu Windows Defender a přidává ho do profilu za vás.
Platí pro Windows 10 a novější.

#### <a name="require-users-to-connect-during-device-setup--2311457--"></a>Vyžadovat, aby se uživatelé připojili během instalace zařízení<!--2311457-->
Nyní můžete nastavit profily zařízení tak, aby se během instalace Windows 10 muselo zařízení ještě před opuštěním stránky Síť připojit k síti. Funkce je sice ve verzi Preview, ale ve Windows Insider sestavení 1809 nebo novějších je toto nastavení povinné.
Platí pro: nejnovější build [Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/) (v období verze Preview).

#### <a name="restricts-apps-and-block-access-to-company-resources-on-ios-and-android-enterprise-devices---2451462---"></a>Omezí aplikace a zablokuje přístup k firemním prostředkům na zařízeních se systémy iOS a Android Enterprise.<!-- 2451462 -->
V části **Dodržování předpisů zařízením** > **Zásady** > **Vytvořit zásadu** > **iOS** > **Zabezpečení systému** je k dispozici nové nastavení **Aplikace s omezeným přístupem**. Toto nové nastavení pomocí zásad dodržování předpisů blokuje přístup k firemním prostředkům, pokud jsou v zařízení nainstalované některé aplikace. Zařízení se považuje za neodpovídající předpisům, dokud se z něj aplikace s omezeným přístupem neodeberou.
Platí pro: iOS

#### <a name="modern-vpn-support-updates-for-ios---2459928-1819876-and-2650856---"></a>Aktualizace moderní sítě VPN pro iOS<!-- 2459928, 1819876, and 2650856 -->
S touto aktualizací se přidává podpora následujících klientů VPN pro iOS:
- F5 Access (verze 3.0.1 a vyšší)
- Citrix SSO
- Palo Alto Networks GlobalProtect verze 5.0 a vyšší – další změny v aktualizaci:
- Stávající připojení typu **F5 Access** se v iOSu přejmenovalo na **Starší verze F5 Access**.
- Stávající připojení typu **Palo Alto Networks GlobalProtect** se v iOSu přejmenovalo na **Palo Alto Networks GlobalProtect (starší verze)** .
Stávající profily s těmito typy připojení budou i nadále fungovat s příslušnou starší verzí klienta VPN. Pokud v iOSu používáte klienty Cisco Legacy AnyConnect, Starší verze F5 Access, Citrix VPN nebo Palo Alto Networks GlobalProtect verze 4.1 a starší, doporučujeme přejít na nové aplikace. Proveďte to co nejdříve, abyste zařízením s iOSem zajistili přístup k síti VPN i po aktualizaci na verzi iOS 12.
Podrobnosti o iOSu 12 a profilech VPN najdete na [blogu technické podpory Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2013806).

#### <a name="export-azure-classic-portal-compliance-policies-to-recreate-these-policies-in-the-intune-azure-portal---2469637---"></a>Export zásad dodržování předpisů z portálu Azure Classic pro jejich opětovné vytvoření na portálu Intune Azure<!-- 2469637 -->
Zásady dodržování předpisů vytvořené na portálu Azure Classic se přestanou používat. Existující zásady si můžete prohlédnout a odstranit je, nelze je ale aktualizovat. Pokud potřebujete jakékoli zásady dodržování předpisů z aktuálního portálu Intune Azure migrovat, můžete je vyexportovat do souboru hodnot oddělených čárkami ( *.csv*). Podrobnosti ze souboru potom můžete využít k opětovnému vytvoření těchto zásad v Intune na portálu Azure Portal.

> [!IMPORTANT]
> Po vyřazení portálu Azure Classic už k zásadám nebudete mít přístup, ani si je nebudete moci prohlížet. Proto zásady nezapomeňte exportovat a znovu vytvořit na webu Azure Portal dříve, než bude provoz portálu Azure Classic ukončen.

#### <a name="better-mobile---new-mobile-threat-defense-partner---22662717---"></a>Lepší partner ochrany před mobilními hrozbami Mobile – nový<!-- 22662717 -->
Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí lépe mobilní, řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune.

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="lock-the-company-portal-in-single-app-mode-until-user-sign-in--1067692---"></a>Uzamknout portál společnosti v režimu jedné aplikace, dokud se uživatel přihlašuje<!--1067692 --> 
Pokud během registrace DEP neověřujete uživatele pomocí Průvodce nastavením, ale prostřednictvím aplikace Portál společnosti, máte nyní možnost aplikaci Portál společnosti spustit v režimu Jedna aplikace. Tato možnost ihned po dokončení chodu Průvodce nastavením uzamkne zařízení a uživatel k němu získá přístup až po přihlášení. Tak je zajištěno, že se u zařízení dokončí fáze zavádění a nezůstane osamocené ve stavu, kdy není svázáno s žádným uživatelem.

#### <a name="assign-a-user-and-friendly-name-to-an-autopilot-device--1346521---"></a>Přiřazení uživatele a popisného názvu k zařízení autopilotu<!--1346521 -->
Nově můžete [přiřadit uživatele k jedinému zařízení Autopilot](../enrollment/enrollment-autopilot.md). Správci budou také moct dávat zařízením v programu AutoPilot popisné názvy, které uživatele při nastavování přivítají.
Platí pro: nejnovější build [Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/) (v období verze Preview).

#### <a name="use-vpp-device-licenses-to-pre-provision-the-company-portal-during-dep-enrollment---1608345---"></a>Pomocí licencí zařízení VPP předem zajistěte Portál společnosti během registrace DEP.<!-- 1608345 -->
Licence zařízení z programu VPP (Volume Purchase Program) můžete teď použít k předběžnému zřízení Portálu společnosti během registrace do programu DEP (Device Enrollment Program neboli Program registrace zařízení). Pokud to chcete udělat, zadejte při [vytváření nebo úpravě profilu registrace](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) token VPP, který chcete použít k instalaci aplikace Portál společnosti. Dbejte na to, aby tokenu nevypršela platnost a abyste měli dost licencí pro aplikaci Portál společnosti. V případech, kdy platnost tokenu vyprší nebo dojdou licence, nabídne Intune instalaci aplikace Portál společnost z App Storu (při které se zobrazí výzva k zadání Apple ID).

#### <a name="confirmation-required-to-delete-vpp-token-that-is-being-used-for-company-portal-pre-provisioning---2237634---"></a>K odstranění tokenu VPP, který se používá pro Portál společnosti předběžné zřizování, se vyžaduje potvrzení.<!-- 2237634 -->
Vyžaduje se potvrzení odstranění tokenu VPP (Volume Purchase Program), pokud se používá k předběžnému zřízení portálu společnosti během registrace do programu DEP.

#### <a name="block-windows-personal-device-enrollments---1849498---"></a>Blokovat registraci osobních zařízení Windows<!-- 1849498 -->
V Intune můžete [blokovat registraci osobních zařízení s Windows](../enrollment/enrollment-restrictions-set.md) do [ správy mobilních zařízení](../enrollment/windows-enroll.md). Pomocí této funkce se nedají blokovat zařízení zaregistrovaná prostřednictvím [agenta Intune pro počítače](manage-windows-pcs-with-microsoft-intune.md). Tato funkce se bude vydávat v příštích několika týdnech, takže ji v uživatelském rozhraní nemusíte vidět hned.

#### <a name="specify-machine-name-patterns-in-an-autopilot-profile--1849855--"></a>Určení vzorů názvu počítače v profilu autopilotu<!--1849855-->
Můžete [zadat šablonu pro názvy počítačů](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile), která se použije ke generování a nastavení [názvu počítače](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp) při registraci do programu AutoPilot. Platí pro: nejnovější build [Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/) (v období verze Preview).

#### <a name="for-windows-autopilot-profiles-hide-the-change-account-options-on-the-company-sign-in-page-and-domain-error-page--1901669---"></a>Pro profily Windows autopilotu skryjte možnosti změnit účet na přihlašovací stránce společnosti a na chybové stránce domény.<!--1901669 -->
Nyní jsou k dispozici [nové možnosti profilu Windows AutoPilot](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile), které správcům umožňují na přihlašovací stránce společnosti a na chybové stránce domény skrýt volbu změny účtu. Předpokladem skrytí těchto možností je, aby v Azure Active Directory byla nakonfigurována funkce Branding společnosti. Platí pro: nejnovější build [Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/) (v období verze Preview).

### <a name="macos-support-for-apple-device-enrollment-program---747651---"></a>Podpora macOS pro Apple Program registrace zařízení<!-- 747651 -->
Intune teď podporuje registraci zařízení s macOS do Programu registrace zařízení (DEP) společnosti Apple. Další informace najdete v článku [Automatická registrace zařízení s macOS do Programu registrace zařízení Apple](../enrollment/device-enrollment-program-enroll-macos.md).

### <a name="device-management"></a>Správa zařízení

#### <a name="delete-jamf-devices---2653306--"></a>Odstranit zařízení Jamf<!-- 2653306-->
Zařízení spravovaná prostřednictvím JAMF můžete odstranit tak, že přejdete na **Zařízení** > zvolíte zařízení Jamf > **Odstranit**.

#### <a name="change-terminology-to-retire-and-wipe---2175759---"></a>Změna terminologie na vyřazení a vymazání<!-- 2175759 -->
V uživatelském rozhraní Intune a v dokumentaci k Intune jsme změnili kvůli sjednocení s Graph API následující výrazy:
- **Odebrání firemních dat** se mění na „vyřazení“.
- **Obnovení továrního nastavení** se mění na **vymazání**.

#### <a name="confirmation-dialog-if-admin-tries-to-delete-mdm-push-certificate---297909500--"></a>Potvrzovací dialog, pokud se správce pokusí odstranit MDM Push Certificate<!-- 297909500-->
Pokud se jakýkoliv uživatel pokusí odstranit certifikát Apple MDM Push Certificate, zobrazí se v dialogovém okně potvrzení počet souvisejících zařízení s iOSem a macOS. Dojde-li k odstranění certifikátu, musí se tato zařízení znovu zaregistrovat.

#### <a name="additional-security-settings-for-windows-installer---2282430---"></a>Nastavení dalšího zabezpečení pro Instalační službu systému Windows<!-- 2282430 -->
Můžete uživatelům umožnit ovládání instalace aplikací. Pokud je tato možnost povolená, instalace, které by se jinak kvůli narušení zabezpečení zastavily, budou moct pokračovat. Můžete Instalační službu systému Windows nastavit tak, aby při instalaci libovolné aplikace do systému používala zvýšenou úroveň oprávnění. Dále můžete povolit, aby se položky WIP (Windows Information Protection) indexovaly a aby se metadata o nich ukládala do nešifrovaného umístění. Pokud je tato zásada zakázaná, chráněné položky WIP se neindexují a ve výsledcích v Cortaně nebo v Průzkumníkovi souborů se nezobrazují. Funkčnost těchto možností je ve výchozím nastavení zakázaná. 

#### <a name="new-user-experience-update-for-the-company-portal-website--2000968---"></a>Nová aktualizace uživatelského prostředí pro Portál společnosti web<!--2000968 -->
Do Portál společnosti webu jsme přidali nové funkce založené na zpětné vazbě od zákazníků. Na svých zařízeních si všimnete značného vylepšení stávající funkčnosti a použitelnosti. Oblasti webu – jako třeba podrobnosti o zařízení, váš názor a podpora a přehled zařízení – získaly nový, moderní a živý vzhled. Další vylepšení:

- Zjednodušené pracovní postupy na všech platformách zařízení
- Vylepšené průběhy identifikace a registrace zařízení
- Další užitečné chybové zprávy
- Příjemnější jazyk, méně technického žargonu
- Možnost sdílet přímé odkazy na aplikace
- Vylepšený výkon u velkých katalogů aplikací
- Lepší přístupnost pro všechny uživatele  

Aktualizovali jsme [dokumentaci na Portálu společnosti Intune](https://docs.microsoft.com/user-help/using-the-intune-company-portal-website), aby tyto změny reflektovala. Pokud si chcete prohlédnout ukázku vylepšených aplikací, přejděte na článek [Aktualizace uživatelského rozhraní pro aplikace Intune pro koncové uživatele](whats-new-app-ui.md).  

### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="enhanced-jailbreak-detection-in-compliance-reporting---2198738---"></a>Vylepšené zjišťování jailbreaků v hlášení dodržování předpisů<!-- 2198738 -->
Vylepšené stavy nastavení detekce jailbreaků se nově zobrazují při veškerém generování sestav dodržování předpisů v konzole správce.

### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="scope-tags-for-policies--1081974---"></a>Značky oboru pro zásady<!--1081974 -->
Nově můžete [vytvářet značky oboru](scope-tags.md) a omezovat s jejich pomocí přístup k prostředkům Intune. Přidejte značku oboru k přiřazení role a poté přidejte značku oboru ke konfiguračnímu profilu. Daná role bude mít přístup pouze k prostředkům s konfiguračními profily, které mají odpovídající značky oboru (nebo žádnou značku oboru).





<!-- ########################## -->
## <a name="july-2018"></a>Červenec 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="line-of-business-lob-app-support-for-macos---1895847---"></a>Obchodní podpora (LOB) pro macOS<!-- 1895847 -->
Microsoft Intune umožňuje nasazovat obchodní aplikace pro macOS jako **povinné** nebo **k dispozici s registrací**. Koncoví uživatelé můžou aplikace nasazovat jako **povinné** prostřednictvím Portálu společnosti pro macOS nebo [webu Portál společnosti](https://portal.manage.microsoft.com).

#### <a name="ios-built-in-app-support-for-kiosk-mode---2051098---"></a>Podpora integrované aplikace iOS pro celoobrazovkový režim<!-- 2051098 -->
Kromě aplikací ze Storu a spravovaných aplikací můžete nyní vybrat i integrovanou aplikaci (jako je Safari), která poběží na zařízení s iOSem v celoobrazovkovém režimu.

#### <a name="edit-your-office-365-pro-plus-app-deployments---2150145---"></a>Úprava nasazení aplikace sady Office 365 pro plus<!-- 2150145 -->
Jako správce Microsoft Intune máte širší možnosti úpravy nasazování aplikací Office 365 Pro Plus. Navíc už nemusíte odstraňovat nasazení, aby se změnily jakékoli vlastnosti sady. Na portálu Azure Portal vyberte **Microsoft Intune** > **Klientské aplikace** > **Aplikace**. V seznamu aplikací vyberte vaši sadu Office 365 Pro Plus.  

#### <a name="updated-intune-app-sdk-for-android-is-now-available---2744271--"></a>Aktualizovaná sada Intune App SDK pro Android je teď dostupná<!-- 2744271-->
K dispozici je aktualizovaná verze sady Intune App SDK pro Android, která podporuje vydanou verzi Android P. Pokud jste vývojáři aplikací a používáte sadu Intune SDK pro Android, musíte si nainstalovat aktualizovanou verzi sady Intune App SDK. Tím zajistíte, že funkce Intune budou v aplikacích pro Android fungovat očekávaným způsobem, a to i na zařízeních s Androidem P. Tato verze sady Intune App SDK nabízí integrovaný plug-in, který aktualizuje sadu SDK, Nemusíte přepisovat veškerý stávající kód, který je integrovaný. Podrobné informace najdete v tématu o [sadě Intune SDK pro Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android). Pokud používáte staré označení Intune, doporučujeme použít ikonu aktovky. Podrobné informace najdete v [tomto úložišti GitHub](https://github.com/msintuneappsdk/intune-app-partner-badge).

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>Další možnosti synchronizace v aplikaci Portál společnosti pro Windows  
Aplikace Portál společnosti pro Windows teď umožňuje zahájit synchronizaci přímo z hlavního panelu Windows a z nabídky Start. Tato funkce je užitečná hlavně v případě, že vaším jediným úkolem je synchronizace zařízení a získání přístupu k podnikovým prostředkům. Pokud chcete tuto novou funkci použít, klikněte pravým tlačítkem na ikonu Portál společnosti, která je připnutá na hlavní panel nebo v nabídce Start. V možnostech nabídky (označuje se také jako seznam odkazů) vyberte **Synchronizovat toto zařízení**. Portál společnosti se otevře na stránce **Nastavení** a zahájí synchronizaci. Pokud se chcete podívat na nové funkce, podívejte se, [co je nového v uživatelském rozhraní](whats-new-app-ui.md).

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>Nové možnosti procházení v aplikaci Portál společnosti pro Windows  
Při procházení nebo hledání aplikací v aplikaci Portál společnosti pro Windows teď můžete přepínat mezi stávajícím zobrazením **dlaždic** a nově přidaným zobrazením **podrobností**. Toto nové zobrazení obsahuje podrobnosti aplikace, například název, vydavatele, datum publikování a stav instalace.  

Na stránce **Aplikace** si v zobrazení **Nainstalované** můžete prohlédnout podrobnosti o dokončených a probíhajících instalacích aplikací. Vzhled nového zobrazení najdete v tématu [Aktualizace uživatelského rozhraní pro aplikace Intune pro koncové uživatele](whats-new-app-ui.md).  

#### <a name="improved-company-portal-app-experience-for-device-enrollment-managers"></a>Vylepšené prostředí aplikace Portál společnosti pro správce registrace zařízení  
Když se správce registrace zařízení přihlásí k aplikaci Portál společnosti pro Windows, bude se od teď v této aplikaci uvádět jen jeho aktuální spuštěné zařízení. Tímto vylepšením se omezí vypršení časového limitu, ke kterým dříve docházelo, když se aplikace snažila zobrazit všechna zařízení zaregistrovaná správcem.  

#### <a name="block-app-access-based-on-unapproved-device-vendors-and-models----1425689----"></a>Blokovat přístup k aplikaci na základě neschválených dodavatelů a modelů zařízení <!-- 1425689 ! -->
Správce IT v Intune může vynutit konkrétní seznam výrobců zařízení s Androidem a/nebo modelů s iOSem prostřednictvím zásad Intune App Protection. Správce IT může poskytnout středníky oddělený seznam výrobců pro zásady Androidu a modelů zařízení pro zásady iOS. Zásady Intune App Protection jsou pouze pro Android a iOS. V tomto konkrétním seznamu můžete provést dvě samostatné akce:
- Budete moct blokovat přístup k aplikacím na zařízeních, která nejsou specifikována.
- Nebo selektivně vymazat podniková data na zařízeních, která nejsou specifikována. 

Uživatel nebude moct přistupovat k cílové aplikaci, pokud nebudou splněny požadavky prostřednictvím zásad. Na základě nastavení může být uživatel zablokován nebo mu mohou být v aplikaci vymazána podniková data. Na zařízeních s iOSem tato funkce vyžaduje zapojení aplikací (jako jsou WXP, Outlook, Managed Browser, Yammer), aby integrovaly sadu Intune App SDK. V opačném případě nebude možné vynutit tuto funkci v cílových aplikacích. K této integraci dochází průběžně a závisí na týmech konkrétních aplikací. Na Androidu tato funkce vyžaduje nejnovější verzi Portálu společnosti. 

Na zařízeních koncových uživatelů klient Intune provede akci založenou na jednoduché shodě řetězců zadaných v okně Intune pro zásady ochrany aplikací. Závisí to zcela na hodnotě, kterou zařízení vykazuje. Doporučujeme správci IT, aby zajistil přesnost zamýšleného chování. Toho se dá dosáhnout testováním tohoto nastavení na základě různých výrobců a modelů zacílených na malé skupiny uživatelů. Pokud si chcete zobrazit a přidat zásady ochrany aplikací, vyberte v Microsoft Intune **Klientské aplikace** > **Zásady ochrany aplikací**. Další informace o zásadách ochrany aplikací najdete v článku [Co jsou zásady ochrany aplikací](../apps/app-protection-policy.md) a [Selektivní vymazání dat pomocí akcí přístupu zásad ochrany aplikací v Intune](../apps/app-protection-policies-access-actions.md).

#### <a name="access-to-macos-company-portal-pre-release-build---1734766---"></a>Přístup k macOS Portál společnosti předběžného vydání buildu<!-- 1734766 -->
Pomocí aplikace Microsoft AutoUpdate se můžete zapojit do programu Insider a získávat tak buildy dříve. Registrace vám umožní používat aktualizované Portál společnosti před tím, než bude dostupný koncovým uživatelům. Další informace najdete na [blogu Microsoft Intune](https://blogs.technet.microsoft.com/intunesupport/2018/07/13/use-microsoft-autoupdate-for-early-access-to-the-macos-company-portal-app/).

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="create-device-compliance-policy-using-firewall-settings-on-macos-devices---1497640---"></a>Vytvoření zásad dodržování předpisů pro zařízení pomocí nastavení brány firewall na zařízeních macOS<!-- 1497640 -->
Při vytváření nových zásad dodržování předpisů systému macOS (**Dodržování předpisů zařízením** > **Zásady** > **Vytvořit zásadu** > **Platforma: macOS** > **Zabezpečení systému**) jsou dostupná některá nová nastavení pro **bránu firewall**: 

- **Firewall:** Umožňuje konfigurovat způsob zpracování příchozích připojení ve vašem prostředí.
- **Příchozí připojení:** **Blokuje** všechna příchozí připojení s výjimkou připojení potřebných pro základní internetové služby, jako je DHCP, Bonjour a IPSec. Toto nastavení blokuje také všechny služby sdílení.
- **Neviditelný režim:** **Aktivací** neviditelného režimu zakážete zařízení odpovídat na zjišťovací požadavky. Oprávněným aplikacím bude zařízení dále odpovídat na příchozí žádosti.

Platí pro: macOS 10.12 a novější

#### <a name="new-wi-fi-device-configuration-profile-for-windows-10-and-later---1879077---"></a>Nový profil konfigurace zařízení Wi-Fi pro Windows 10 a novější<!-- 1879077 -->
V současné době můžete importovat a exportovat profily Wi-Fi pomocí souborů XML. S touto aktualizací můžete vytvořit konfigurační profil Wi-Fi zařízení přímo v Intune, podobně jako na některých jiných platformách.

Pokud chcete vytvořit profil, otevřete položku **Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Windows 10 a novější** > **Wi-Fi**. 

Platí pro Windows 10 a novější.

#### <a name="kiosk---obsolete-is-grayed-out-and-cant-be-changed---2149998---"></a>Veřejný terminál – zastaralý je šedý a nedá se změnit.<!-- 2149998 -->
Funkce veřejného terminálu (ve verzi Preview) (**Konfigurace zařízení** > **profily** > **vytvořit profil** > **Windows 10 a novější** > **omezení zařízení**) se zastaralá a v [případě systému Windows 10 a novějších verzí se nahradila nastaveními pro celoobrazovkový](../configuration/kiosk-settings.md)režim. Položka **Veřejný terminál (zastaralé)** se v této aktualizaci zobrazuje šedě a uživatelské rozhraní neumožňuje změny ani aktualizace. 

Pokud budete chtít povolit režim veřejného terminálu, podívejte se na článek[Nastavení veřejného terminálu pro Windows 10 a novější](../configuration/kiosk-settings.md).

Platí pro: Windows 10 a novější, Windows Holographic for Business.

#### <a name="apis-to-use-3rd-party-certification-authorities---2184013---"></a>Rozhraní API pro používání certifikačních autorit třetích stran<!-- 2184013 -->
V této aktualizaci je k dispozici rozhraní API založené na Javě, které umožňuje integraci nezávislých certifikačních autorit s Intune a protokolem SCEP. Uživatelé pak budou moct přidat certifikát SCEP do profilu a použít ho pro zařízení využívající MDM.

V současné době Intune podporuje [žádosti protokolu SCEP používající Active Directory Certificate Services](../protect/certificates-scep-configure.md).

#### <a name="toggle-to-show-or-not-show-the-end-session-button-on-a-kiosk-browser---2455253---"></a>Přepnutím zobrazíte nebo nezobrazete tlačítko ukončit relaci v prohlížeči veřejného terminálu.<!-- 2455253 -->
Nyní můžete nakonfigurovat, jestli se má v prohlížečích Kiosk zobrazovat tlačítko pro ukončení relace. Tento ovládací prvek najdete v části **Konfigurace zařízení** > **Beznabídkový režim (Preview)**  > **Kiosk Web Browser**. Pokud toto tlačítko zapnete a uživatel na něj klikne, zobrazí aplikace výzvu k potvrzení ukončení relace. Po potvrzení prohlížeč vymaže všechny údaje o procházení a přejde zpátky na výchozí adresu URL.

#### <a name="create-an-esim-cellular-configuration-profile---2564077---"></a>Vytvoření profilu konfigurace mobilní sítě pro eSIM kartu<!-- 2564077 -->
V části **Konfigurace zařízení** můžete vytvořit mobilní profil eSIM. Můžete naimportovat soubor, který obsahuje mobilní aktivační kódy poskytnuté vaším mobilním operátorem. Pak můžete tyto profily nasadit do zařízení s Windows 10 podporujících eSIM LTE, jako je například Surface Pro LTE a další zařízení podporující eSIM.

Zkontrolujte, jestli vaše [zařízení podporuje profily eSIM](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data).

Platí pro Windows 10 a novější.

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings---1058963-eenotready---"></a>Výběr kategorií zařízení pomocí nastavení přístup do práce nebo do školy<!-- 1058963 eenotready --> 
Pokud jste povolili [mapování skupin zařízení](../enrollment/device-group-mapping.md), uživatelům s Windows 10 se teď po registraci prostřednictvím tlačítka **Připojit** v **Nastavení** > **Účty** > **Přístup do práce nebo do školy** zobrazí výzva k výběru kategorie zařízení. 

#### <a name="use-samaccountname-as-the-account-username-for-email-profiles---1500307---"></a>Jako uživatelské jméno účtu pro e-mailové profily použijte sAMAccountName.<!-- 1500307 -->
Můžete používat místní **sAMAccountName** jako uživatelské jméno účtu pro e-mailové profily v Androidu, iOSu a Windows 10. Můžete také získat doménu z atributu `domain` nebo `ntdomain` v Azure Active Directory (Azure AD). Nebo budete moct zadat vlastní statickou doménu.

Pokud chcete tuto funkci používat, musíte atribut `sAMAccountName` synchronizovat z místního prostředí Active Directory do Azure AD.

Platí pro [Android](../configuration/email-settings-android.md), [iOS](../configuration/email-settings-ios.md), [Windows 10 a novější](../configuration/email-settings-windows-10.md).

#### <a name="see-device-configuration-profiles-in-conflict---1556983---"></a>Zobrazit konfliktní profily konfigurace zařízení<!-- 1556983 -->
V části **Konfigurace zařízení** se zobrazuje seznam existujících profilů. S touto aktualizací se přidá nový sloupec, který bude poskytovat podrobné informace o profilech, u kterých došlo ke konfliktu. Výběrem řádku s konfliktem můžete zobrazit nastavení a profil, u kterého se konflikt vyskytl. 

Přečtěte si další informace o [správě konfiguračních profilů](../configuration/device-profile-monitor.md#view-conflicts).

#### <a name="new-status-for-devices-in-device-compliance---2308882---"></a>Nový stav pro zařízení v dodržování předpisů zařízením<!-- 2308882 -->
Na stránku **Dodržování předpisů zařízením** > **Zásady** > vyberte zásadu > **Přehled** jsou přidané následující nové stavy:
- Úspěšné
- chyba
- Konflikt
- Čeká se na zadání
- Nepoužitelné Také se zobrazí obrázek, který ukazuje počet zařízení s jinou platformou. Když se třeba díváte na profil iOSu, na nové dlaždici se zobrazí počet zařízení s jiným systémem než iOS, která jsou také přiřazená k tomuto profilu. Viz [Zásady dodržování předpisů zařízením](../protect/compliance-policy-monitor.md#view-status-of-device-policies).

#### <a name="device-compliance-supports-3rd-party-anti-virus-solutions---2325484---"></a>Dodržování předpisů zařízením podporuje antivirová řešení třetích stran.<!-- 2325484 -->
Při vytváření zásad dodržování předpisů zařízením (**Dodržování předpisů zařízením** > **Zásady** > **Vytvořit zásadu** > **Platforma: Windows 10 nebo novější** > **Nastavení** > **Zabezpečení systému**) jsou dostupné nové možnosti **[Zabezpečení zařízení](../protect/compliance-policy-create-windows.md)** : 
- **Antivirus:** Když je tato možnost nastavená na **Vyžadovat**, můžete dodržování předpisů kontrolovat pomocí antivirových řešení, která jsou registrovaná Centrem zabezpečení systému Windows, jako je Symantec nebo Windows Defender. 
- **Antispyware:** Když je tato možnost nastavená na **Vyžadovat**, můžete dodržování předpisů kontrolovat pomocí antispywarových řešení, která jsou registrovaná Centrem zabezpečení systému Windows, jako je Symantec nebo Windows Defender. 

Platí pro: Windows 10 a novější 

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="automatically-mark-android-devices-enrolled-by-using-samsung-knox-mobile-enrollment-as-corporate---2404851---"></a>Automatické označení zařízení s Androidem registrovaných pomocí technologie Samsung Knox Mobile Enrollment jako firemních<!-- 2404851 -->
Ve výchozím nastavení se zařízení s Androidem registrovaná pomocí technologie Samsung Knox Mobile Enrollment označují v poli **Vlastnictví zařízení** jako **Firemní**. Před registrací pomocí technologie Knox Mobile Enrollment nemusíte firemní zařízení identifikovat ručně pomocí IMEI nebo sériových čísel.

#### <a name="devices-without-profiles-column-in-the-list-of-enrollment-program-tokens---1853904---"></a>Sloupec zařízení bez profilů v seznamu tokenů programu registrace<!-- 1853904 -->
V seznamu tokenů programu registrace se nachází nový sloupec, který zobrazuje počet zařízení bez přiřazeného profilu. Pomáhá správcům při přiřazování profilů těmto zařízením před jejich přidělením uživatelům. Pokud chcete tento nový sloupec zobrazit, přejděte na **Registrace zařízení** > **Registrace Apple** > **Tokeny programu registrace**.

### <a name="device-management"></a>Správa zařízení

#### <a name="bulk-delete-devices-on-devices-blade---1793693---"></a>Okno hromadného odstranění zařízení v zařízeních<!-- 1793693 -->
V okně Zařízení můžete odstranit více zařízení najednou. Zvolte **Zařízení** > **Všechna zařízení** > vyberte zařízení, která chcete odstranit > **Odstranit**. U zařízení, která nejde odstranit, se zobrazí upozornění.

#### <a name="google-name-changes-for-android-for-work-and-play-for-work--842873---"></a>Změny názvu Google pro Android for Work a Play for Work<!--842873 -->
Intune aktualizoval terminologii „Android for Work“ tak, aby odrážela změny brandingu společnosti Google. Termíny „Android for Work“ a „Play for Work“ se už nepoužívají. V závislosti na kontextu se používá jiná terminologie:
- Termín „Android Enterprise“ označuje celkovou moderní sadu správy Androidu.
- Termín „Pracovní profil“ nebo „Vlastník profilu“ označuje vlastní zařízení uživatelů (BYOD) spravovaná pomocí pracovních profilů.
- Termín „Spravovaný obchod Google Play“ označuje Google App Store.

#### <a name="rules-for-removing-devices---1609459---"></a>Pravidla pro odebrání zařízení<!-- 1609459 -->
Jsou k dispozici nová pravidla, která vám umožňují automaticky odebrat zařízení, která se nastavený počet dnů neohlásila. Pokud chcete nové pravidlo zobrazit, přejděte do podokna **Intune** a vyberte **Zařízení** a **Pravidla čištění zařízení**.

#### <a name="corporate-owned-single-use-support-for-android-devices---1630973---"></a>Podpora pro zařízení s Androidem ve vlastnictví firmy<!-- 1630973 -->

Intune teď podporuje zamykatelná zařízení s beznabídkovým režimem Androidu a s vysokou úrovní správy. To správcům umožní další uzamčení použití zařízení na jednu aplikaci nebo malou sadu aplikací a zabrání uživatelům povolit na zařízení jiné aplikace nebo na něm provádět jiné akce. Pokud chcete nastavit beznabídkový režim Androidu, přejděte do Intune > **Registrace zařízení** > **Registrace Androidu** > **Beznabídkový režim a registrace zařízení úloh**. Další informace najdete v článku o [nastavení registrace zařízení s beznabídkovým režimem Androidu Enterprise](../enrollment/android-kiosk-enroll.md).

#### <a name="per-row-review-of-duplicate-corporate-device-identifiers-uploaded---2203794--"></a>Kontrola duplicitních identifikátorů podnikových zařízení v jednotlivých řádcích<!-- 2203794-->
Při nahrávání firemních ID teď Intune poskytuje seznam duplicit a nabídne možnost nahradit nebo ponechat existující informace. Sestava se zobrazí, pokud vzniknou duplicity, když zvolíte **Registrace zařízení** > **Identifikátory podnikových zařízení** > **Přidat identifikátory**. 

#### <a name="manually-add-corporate-device-identifiers---2203803---"></a>Ruční přidání identifikátorů podnikových zařízení<!-- 2203803 -->
Teď je možné přidat ID podnikových zařízení ručně. Zvolte **Registrace zařízení** > **Identifikátory podnikových zařízení** > **Přidat**. 


<!-- ########################## -->
## <a name="june-2018"></a>Červen 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="microsoft-edge-mobile-support-for-intune-app-protection-policies---1817882---"></a>Podpora Microsoft Edge Mobile pro zásady ochrany aplikací Intune<!-- 1817882 -->
Prohlížeč Microsoft Edge pro mobilní zařízení nyní podporuje zásady ochrany aplikací definované v Intune.

#### <a name="retrieve-the-associated-app-user-model-id-aumid-for-microsoft-store-for-business-apps-in-kiosk-mode---1560077----"></a>Načtení ID uživatelského modelu přidružené aplikace (AUMID) pro aplikace Microsoft Store for Business v celoobrazovkovém režimu<!-- 1560077 ! -->
Intune teď může načíst ID uživatelských modelů aplikací (AUMIDs) pro aplikace Microsoft Store for Business (WSfB), aby poskytovala vylepšenou konfiguraci profilu veřejného terminálu.

Další informace o aplikacích pro Microsoft Store pro firmy najdete v článku [Správa aplikací z Microsoft Storu pro firmy](../apps/windows-store-for-business.md).

#### <a name="new-company-portal-branding-page---1916370---"></a>Nová stránka Portál společnosti brandingu<!-- 1916370 -->
Stránka brandingu Portálu společnosti obsahuje nové rozložení, zprávy a popisky.


### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="pradeo---new-mobile-threat-defense-partner---1169249---"></a>Pradeo – nový partner ochrany před mobilními hrozbami<!-- 1169249 -->
Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí Pradeo, řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune.

#### <a name="use-fips-mode-with-the-ndes-certificate-connector---1333688---"></a>Použití režimu FIPS s certifikátem NDES Certificate Connector<!-- 1333688 -->
Když jste nainstalovali konektor NDES Certificate na počítač se zapnutým režimem FIPS (Federal Information Processing Standard), vydávání a odvolávání certifikátů nefungovalo podle očekávání. Díky této aktualizaci bude konektor NDES Certificate standard FIPS podporovat. 

Tato aktualizace také zahrnuje:

- Konektor NDES Certificate vyžaduje rozhraní .NET 4.5 Framework, které je automaticky součástí Windows Serveru 2016 a Windows Serveru 2012 R2. Dříve bylo minimální požadovanou verzí rozhraní .NET 3.5 Framework.
- NDES Certificate Connector podporuje také protokol TLS 1.2. Pokud server s nainstalovaným NDES Certificate Connectorem podporuje TLS 1.2, použije se TLS 1.2. Pokud server nepodporuje TLS 1.2, použije se TLS 1.1. V současnosti se k ověřování zařízení a serveru používá protokol TLS 1.1.

Další informace najdete v tématech o [konfiguraci a použití certifikátů SCEP](../protect/certificates-scep-configure.md) a [konfiguraci a použití certifikátů PKCS](../protect/certficates-pfx-configure.md).

#### <a name="support-for-palo-alto-networks-globalprotect-vpn-profiles---1333680----"></a>Podpora profilů sítě VPN v Palo Alto Networks GlobalProtect<!-- 1333680 ! -->
S touto aktualizací můžete zvolit Palo Alto Networks GlobalProtect jako typ připojení VPN pro profily VPN v Intune (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Typ profilu** > **VPN**). V této vydané verzi se podporují následující platformy: 

- iOS
- Windows 10

#### <a name="additions-to-local-device-security-options-settings---1403702---"></a>Přidání nastavení možností místního zabezpečení zařízení<!-- 1403702 -->
U zařízení s Windows 10 teď můžete nakonfigurovat další nastavení možností místního zabezpečení zařízení. Další nastavení jsou dostupná v oblastech Klient sítě Microsoft, Server sítě Microsoft, Přístup k síti a zabezpečení a Interaktivní přihlášení. Tato nastavení najdete v kategorii Ochrana koncového bodu při vytváření zásad konfigurace zařízení s Windows 10.

#### <a name="enable-kiosk-mode-on-windows-10-devices---1560072----"></a>Povolit celoobrazovkový režim na zařízeních s Windows 10<!-- 1560072 ! -->
Na zařízeních s Windows 10 můžete vytvořit konfigurační profil a povolit beznabídkový režim (**Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Windows 10** > **Omezení zařízení** > **Beznabídkový režim**). V této aktualizaci je nastavení **Beznabídkový režim (Preview)** přejmenováno na **Beznabídkový režim (zastaralé)** . **Beznabídkový režim (zastaralé)** už nedoporučujeme používat, do červnové aktualizace ale zůstane funkční. **Beznabídkový režim (zastaralé)** se nahrazuje novým typem profilu **Beznabídkový režim** (**Vytvořit profil** > **Windows 10** > **Beznabídkový režim (Preview)** ), který bude obsahovat nastavení pro konfiguraci beznabídkového režimu na systému Windows 10 RS4 a novějším.

Platí pro Windows 10 a novější.

#### <a name="device-profile-graphical-user-chart-is-back---2160133---"></a>Graf grafického uživatele profilu zařízení je zpátky.<!-- 2160133 -->
Při vylepšování číselných počtů zobrazených v grafu profilu zařízení (**Konfigurace zařízení** > **Profily** > vyberte existující profil > **Přehled**) byl uživatelský graf dočasně odebrán.

V této aktualizaci se uživatelský graf vrací a zobrazuje se na portálu Azure Portal.

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="support-for-windows-autopilot-enrollment-without-user-authentication---1165118---"></a>Podpora registrace Windows autopilotu bez ověření uživatele<!-- 1165118 -->
Intune teď podporuje registraci pomocí řešení Windows Autopilot bez ověření uživatele. Je to nová možnost v profilu nasazení Windows Autopilot, která nastavuje režim automatického nasazení.  Pokud chcete úspěšně dokončit tento typ registrace, musí zařízení běžet na sestavení Windows 10 Insider Preview 17672 nebo novějším a musí mít čip TPM 2.0. Vzhledem k tomu, že se nevyžaduje žádné ověřování uživatelů, byste tuto možnost měli přiřazovat jenom pro zařízení, nad kterými máte fyzickou kontrolu.

#### <a name="new-languageregion-setting-when-configuring-oobe-for-autopilot---1821766---"></a>Nové nastavení jazyka nebo oblasti při konfiguraci POČÁTEČNÍho nasazení pro autopilot<!-- 1821766 -->
Nové nastavení konfigurace je dostupné pro nastavení jazyka a oblasti pro profily Autopilot během prvního spuštění počítače. Když chcete toto nové nastavení zobrazit, zvolte **Registrace zařízení** > **Registrace zařízení s Windows** > **Profily nasazení** > **Vytvořit profil** > **Režim nasazení** = **Nasazení sebou samým** > **Nakonfigurovaly se výchozí hodnoty**.

#### <a name="new-setting-for-configuring-device-keyboard---1821768---"></a>Nové nastavení pro konfiguraci klávesnice zařízení<!-- 1821768 -->
Nové nastavení bude dostupné pro konfiguraci klávesnice pro profily Autopilot během prvního spuštění počítače. Když chcete toto nové nastavení zobrazit, zvolte **Registrace zařízení** > **Registrace zařízení s Windows** > **Profily nasazení** > **Vytvořit profil** > **Režim nasazení** = **Nasazení sebou samým** > **Nakonfigurovaly se výchozí hodnoty**.

#### <a name="autopilot-profiles-moving-to-group-targeting---1877935---"></a>Profily autopilotu přesunu do cílení na skupinu<!-- 1877935 -->
Profily nasazení AutoPilot můžete přiřadit skupinám Azure AD, které obsahují zařízení AutoPilot.

### <a name="device-management"></a>Správa zařízení

#### <a name="set-compliance-by-device-location---851881----"></a>Nastavit dodržování předpisů podle umístění zařízení<!-- 851881 ! -->
Někdy můžete chtít omezit přístup k podnikovým prostředkům na konkrétní umístění definovaná podle síťového připojení. Teď můžete vytvořit zásady dodržování předpisů (**Dodržování předpisů zařízením** > **Umístění**) na základě IP adresy zařízení. Pokud se zařízení přesune mimo rozsah IP adres, nebude moct přistupovat k podnikovým prostředkům.

Platí pro: Zařízení s Androidem verze 6.0 a novější s aktualizovanou aplikací Portál společnosti

#### <a name="prevent-consumer-apps-and-experiences-on-windows-10-enterprise-rs4-autopilot-devices---1621980---"></a>Zabránění uživatelským aplikacím a prostředím v zařízeních Windows 10 Enterprise RS4 autopilot<!-- 1621980 -->
Budete moct zabránit v instalaci uživatelských aplikací a prostředí na zařízeních Windows 10 Enterprise RS4 AutoPilot. Když chcete tuto funkci zobrazit, přejděte na **Intune** > **Konfigurace zařízení** > **Profily** > **Vytvořit profil** > **Platforma** = **Windows 10 nebo novější** > **Typ profilu** = **Omezení zařízení** > **Konfigurovat** > **Windows Spotlight** > **Uživatelské funkce**. 

#### <a name="uninstall-the-latest-from-windows-10-software-updates---1732948---"></a>Odinstalace nejnovější aktualizace softwaru Windows 10<!-- 1732948 -->
Pokud na počítačích s Windows 10 najdete problém způsobující chybu, můžete se rozhodnout odinstalovat (vrátit zpět) nejnovější aktualizaci funkcí nebo nejnovější aktualizaci kvality. Odinstalace aktualizace funkcí nebo kvality je dostupná jenom pro kanál pro údržbu, ve kterém se dané zařízení nachází. Při odinstalaci se aktivují zásady, které na počítačích s Windows 10 obnoví předchozí aktualizaci. Konkrétně u aktualizací funkcí je možné omezit dobu 2 až 60 dnů, po kterou lze provést odinstalaci nejnovější verze. Pokud chcete nastavit možnosti odinstalace aktualizací softwaru, vyberte na webu Azure Portal v okně **Microsoft Intune** možnost **Aktualizace softwaru**. Pak v okně **Aktualizace softwaru** vyberte **Aktualizační kanály Windows 10**. Pak můžete v části **Přehled** zvolit možnost **Odinstalovat**.

#### <a name="search-all-devices-for-imei-and-serial-number---1793685---"></a>Vyhledat čísla IMEI a sériové číslo pro všechna zařízení<!-- 1793685 -->
Teď můžete hledat IMEI a sériová čísla v okně Všechna zařízení (pole pro e-mail, hlavní název uživatele (UPN), název zařízení a název správy jsou nadále dostupná). V Intune zvolte **Zařízení** > **Všechna zařízení** a do vyhledávacího pole zadejte hledanou položku.

#### <a name="management-name-field-will-be-editable---1875989---"></a>Pole název správy bude editovatelné.<!-- 1875989 -->
V okně **vlastností** zařízení teď můžete upravit pole název správy. Pokud chcete toto pole upravit, vyberte **Zařízení** > **Všechna zařízení** > vyberte zařízení > **Vlastnosti**. Pole s názvem správy můžete použít k jednoznačné identifikaci zařízení.

#### <a name="new-all-devices-filter-device-category---1878520---"></a>Filtr nových zařízení – filtr: kategorie zařízení<!-- 1878520 -->
Teď můžete filtrovat seznam **Všechna zařízení** podle kategorie zařízení. Když to chcete udělat, zvolte **Zařízení** > **Všechna zařízení** > **Filtrovat** > **Kategorie zařízení**.

#### <a name="use-teamviewer-to-screen-share-ios-and-macos-devices---1985547---"></a>Použití TeamVieweru pro sdílení obrazovky zařízení s iOS a MacOS<!-- 1985547 -->
Správci se teď můžou připojit k [TeamVieweru](../remote-actions/teamviewer-support.md) a spustit relaci sdílení obrazovky se zařízeními s iOSem a macOS. Uživatelé iPhonů, iPadů a zařízení s macOS mohou své obrazovky živě sdílet s libovolnými jinými stolními nebo mobilními zařízeními. 

#### <a name="multiple-exchange-connector-support---2070451---"></a>Podpora více konektorů Exchange<!-- 2070451 -->
Už neplatí omezení v podobě jednoho Microsoft Intune Exchange Connectoru na každého tenanta. Intune teď podporuje několik konektorů Exchange, abyste mohli nastavit podmíněný přístup Intune s několika místními organizacemi Exchange.

S místním konektorem Exchange v Intune můžete spravovat přístup zařízení k místním poštovním schránkám Exchange podle toho, jestli je zařízení zaregistrované v Intune a splňuje zásady dodržování předpisů zařízením. Konektor nastavíte tak, že místní konektor Exchange v Intune stáhnete z portálu Azure Portal a nainstalujete ho na server v organizaci Exchange. Na řídicím panelu Microsoft Intune zvolte **Místní přístup** a pak v **Nastavení** vyberte **Konektor Exchange ActiveSync**. Stáhněte místní konektor Exchange a nainstalujte ho na server v organizaci Exchange. Protože už teď neplatí omezení v podobě jednoho konektoru Exchange na každého tenanta, pokud máte další organizace Exchange, můžete stejným postupem stáhnout a nainstalovat konektor pro každou další organizaci Exchange.

#### <a name="new-device-hardware-detail-ccid---2156657---"></a>Podrobnosti o hardwaru nového zařízení: CCID<!-- 2156657 -->
U každého zařízení je teď uvedený údaj CCID (Chip Card Interface Device). Když ho chcete zobrazit, zvolte **Zařízení** > **Všechna zařízení** > zvolte zařízení > **Hardware** a zkontrolujte část **Podrobnosti o síti**>.

#### <a name="assign-all-users-and-all-devices-as-scope-groups---2196803---"></a>Přiřadit všechny uživatele a všechna zařízení jako skupiny oborů<!-- 2196803 -->
Všechny uživatele, všechna zařízení a všechny uživatele a zařízení teď můžete přiřadit do skupin oborů. Když to chcete udělat, zvolte **Role Intune** > **Všechny role** > **Správce zásad a profilů** > **Přiřazení** > zvolte přiřazení > **Rozsah (Skupiny)** .

#### <a name="udid-information-now-included-for-ios-and-macos-devices---2219806---"></a>Informace o UDID, které se teď zahrnují pro zařízení s iOS a macOS<!-- 2219806 -->
Když chcete identifikátor UDID (Unique Device Identifier) pro zařízení s iOSem a macOS zobrazit, přejděte na **Zařízení** > **Všechna zařízení** > zvolte zařízení > **Hardware**. Identifikátor UDID je dostupný jenom pro firemní zařízení (podle nastavení v části **Zařízení** > **Všechna zařízení** > zvolte zařízení > **Vlastnosti** > **Vlastnictví zařízení**).

### <a name="intune-apps"></a>Aplikace Intune

#### <a name="improved-troubleshooting-for-app-installation---928990---"></a>Vylepšené řešení potíží při instalaci aplikací<!-- 928990 -->
U zařízení spravovaných pomocí Microsoft Intune MDM může občas dojít k chybě instalace. Když k těmto chybám instalace dojde, může být obtížné pochopit, proč k nim došlo nebo je odstranit. Spouštíme verzi Public Preview našich funkcí řešení potíží s aplikacemi. U každého jednotlivého zařízení si všimnete nového uzlu **Spravované aplikace**. Jedná se o seznam aplikací, které byly dodány prostřednictvím MDM Intune. Uvnitř uzlu uvidíte seznam stavů instalací aplikací. Pokud vyberete konkrétní aplikaci, uvidíte zobrazení řešení potíží pro tuto konkrétní aplikaci. V zobrazení řešení potíží se zobrazí úplný životní cyklus aplikace, například kdy byla aplikace vytvořena, upravena, zacílena a dodána do zařízení. Pokud navíc nebyla instalace aplikace úspěšná, zobrazí se vám kód chyby a užitečná zpráva týkající se příčiny chyby. 

#### <a name="intune-app-protection-policies-and-microsoft-edge---1818968---"></a>Zásady ochrany aplikací Intune a Microsoft Edge<!-- 1818968 -->
Prohlížeč Microsoft Edge pro mobilní zařízení (iOS a Android) teď podporuje zásady ochrany aplikací Microsoft Intune. Uživatelé zařízení s iOS a Androidem, kteří se přihlásí pomocí podnikových účtů Azure AD v aplikaci Microsoft Edge, budou chráněni službou Intune. Na zařízeních s iOSem umožní zásada **Vyžadovat spravovaný prohlížeč pro webový obsah** uživatelům otevírat odkazy v Microsoft Edgi, pokud je spravovaný.

<!-- ########################## -->
## <a name="may-2018"></a>Květen 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="configuring-your-app-protection-policies---2144597-part-2---"></a>Konfigurace zásad ochrany aplikací<!-- 2144597 Part 2 -->

Na portálu Azure Portal nyní přejdete přímo do Intune a nikoli do okna služby Intune App Protection. Pro zásady ochrany aplikací v rámci Intune nově existuje pouze jedno umístění. Všimněte si, že všechny vaše zásady ochrany aplikací se nacházejí v okně **Mobilní aplikace** v Intune v části **Zásady ochrany aplikací**. Tato integrace usnadňuje práci se správou cloudu. Nezapomeňte, že všechny zásady ochrany aplikací jsou už přenesené do Intune a kterékoli z předem nakonfigurovaných zásad můžete upravit. Zásady ochrany zásad aplikací (APP) a podmíněného přístupu (CA) Intune se teď nacházejí v části **podmíněný přístup**, které najdete v části **správa** v okně **Microsoft Intune** nebo v části **zabezpečení** v okně **Azure Active Directory** . Další informace o úpravách zásad podmíněného přístupu najdete [v tématu podmíněný přístup v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Další informace viz téma [Co jsou zásady ochrany aplikací](../apps/app-protection-policy.md).

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="require-installation-of-policies-apps-certificate-and-network-profiles---1553555---"></a>Vyžadovat instalaci zásad, aplikací, certifikátů a profilů sítě<!-- 1553555 -->
Správci můžou koncovým uživatelům zablokovat přístup k počítači s Windows 10 RS4, dokud Intune nenainstaluje zásady, aplikace a profily certifikátů a síťových profilů během zřizování zařízení s autopilotem. Další informace najdete v článku [Nastavení stránky stavu registrace](../enrollment/windows-enrollment-status.md).

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="samsung-knox-mobile-enrollment-support--1112863--"></a>Podpora registrace mobilních zařízení Samsung KNOX<!--1112863-->
Pokud Intune používáte s technologií Samsung Knox Mobile Enrollment (KME), můžete registrovat velké počty zařízení s Androidem vlastněné společností. Uživatelé připojení prostřednictvím Wi-Fi nebo mobilních sítí mohou svá zařízení při prvním zapnutí registrovat několika klepnutími. Při použití aplikace Knox Deployment App se mohou zařízení registrovat pomocí Bluetooth nebo NFC. Další informace najdete v článku věnovaném [automatické registraci zařízení s Androidem pomocí technologie Knox Mobile Enrollment od Samsungu](../enrollment/android-samsung-knox-mobile-enroll.md).

### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží 

#### <a name="requesting-help-in-the-company-portal-for-windows-10---1874137---"></a>Vyžádání pomoc v Portál společnosti pro Windows 10<!-- 1874137 -->
Portál společnosti pro Windows 10 teď odesílá protokoly aplikace přímo Microsoftu, když uživatel iniciuje pracovní postup pro získání pomoci s problémem. Usnadní se tak řešení problémů, které jsou předávány Microsoftu.

<!-- ########################## -->
## <a name="april-2018"></a>Duben 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="passcode-support-for-mam-pin-on-android---1438086---"></a>Podpora hesla pro MAM PIN v Androidu<!-- 1438086 -->

Správci Intune mohou nastavit požadavek, aby se při spuštění aplikace povinně zadávalo heslo místo číselného kódu PIN MAM. Při takové konfiguraci musí uživatel po zobrazení výzvy nastavit a používat heslo, aby získal přístup k aplikacím s podporou MAM. Heslo je definované jako číselný kód PIN s aspoň jedním speciálním znakem nebo velkým/malým písmenem. Intune podporuje heslo podobným způsobem jako existující číselný kód PIN, umožňuje stanovit minimální délku a povoluje opakování znaků a sekvencí prostřednictvím konzoly pro správu. Tato funkce vyžaduje nejnovější verzi Portálu společnosti na Androidu. Tato funkce je už k dispozici pro iOS.

#### <a name="line-of-business-lob-app-support-for-macos---1473977---"></a>Obchodní podpora (LOB) pro macOS<!-- 1473977 -->
Microsoft Intune bude poskytovat možnost instalace obchodních aplikací pro macOS z portálu Azure Portal. Do Intune budete moct přidat obchodní aplikaci pro masOS poté, co ji předběžně zpracoval nástroj dostupný v GitHubu. Na portálu Azure Portal v okně **Intune** zvolte **Klientské aplikace**. V okně **Klientské aplikace** zvolte **Aplikace** > **Přidat**. V okně **Přidat aplikaci** vyberte **Obchodní aplikace**. 

#### <a name="built-in-all-users-and-all-devices-group-for-android-enterprise-work-profile-app-assignment---1813073---"></a>Předdefinované skupiny všichni uživatelé a všechna zařízení pro přiřazení aplikace pracovního profilu Android Enterprise<!-- 1813073 -->
K přiřazení aplikace pracovního profilu Android Enterprise můžete použít předdefinované skupiny **Všichni uživatelé** a **Všechna zařízení**. Podrobnosti najdete v tématu [Zahrnutí a vyloučení přiřazení aplikací v Microsoft Intune](../apps/apps-inc-exl-assignments.md).

#### <a name="intune-will-reinstall-required-apps-that-are-uninstalled-by-users---1947010---"></a>Intune znovu nainstaluje požadované aplikace odinstalované uživateli.<!-- 1947010 -->
Pokud koncový uživatel odinstaluje některou z povinných aplikací, Intune nečeká na sedmidenní cyklus vyhodnocení a během 24 hodin ji automaticky znovu nainstaluje.

#### <a name="update-where-to-configure-your-app-protection-policies---2144597---"></a>Aktualizace místa konfigurace zásad ochrany aplikací<!-- 2144597 -->

V Azure Portal v rámci služby Microsoft Intune vás dočasně přesměrujeme z okna **Intune App Protection** služby do okna **mobilní aplikace** . Všechny vaše zásady ochrany aplikací se už nacházejí v okně **Mobilní aplikace** v Intune v oblasti konfigurace aplikací. Místo toho, abyste přešli na Intune App Protection, stačí přejít na Intune. V dubnu 2018 toto přesměrování ukončíme a okno služby **Intune App Protection** úplně odebereme, aby se zásady ochrany aplikací nacházely v Intune jen na jednom místě. 

**Co to pro mě znamená?**
Tato změna ovlivní jak zákazníky samostatné verze Intune, tak zákazníky hybridní verze (Intune s Configuration Managerem). Tato integrace pomůže zjednodušit práci se správou cloudu.

**Jak se mám na tuto změnu připravit?**
Místo okna služby **Intune App Protection** a ujistěte se, že jste v okně **mobilní** aplikace v Intune označili pracovní postup zásad ochrany aplikací na oblíbenou položku **Intune** . Přesměrujeme Vás na krátkou dobu a pak se okno **App Protection** odebere. Nezapomeňte, že všechny zásady ochrany aplikací jsou už v Intune, a můžete upravit některé ze zásad podmíněného přístupu. Další informace o úpravách zásad podmíněného přístupu najdete [v tématu podmíněný přístup v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Další informace viz téma [Co jsou zásady ochrany aplikací](../apps/app-protection-policy.md). 

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="device-profile-chart-and-status-list-show-all-devices-in-a-group---1449153---"></a>Graf profilu zařízení a seznam stavů Zobrazit všechna zařízení ve skupině<!-- 1449153 -->
Při konfiguraci profilu zařízení (**Konfigurace zařízení** > **Profily**) vyberete profil zařízení, například iOS. Tento profil přiřadíte ke skupině, která obsahuje zařízení s iOSem a zařízení s jiným systémem. Počet v grafu zobrazuje, že profil je použitý u zařízení s iOSem *a* u zařízení s jiným systémem (**Konfigurace zařízení** > **Profily** > vyberte existující profil > **Přehled**). Když vyberete graf na kartě **Přehled** zobrazí se v části **Stav zařízení** seznam všech zařízení ve skupině, nikoli pouze seznam zařízení s iOSem. 

Po této aktualizaci se v grafu (**Konfigurace zařízení** > **Profily** > vyberte stávající profil > **Přehled**) zobrazí jenom počet odpovídající určitému profilu zařízení. Pokud například konfigurační profil zařízení platí pro zařízení s iOSem, zobrazí se v grafu pouze počet zařízení s iOSem. Když vyberete graf a otevřete **Stav zařízení**, zobrazí se pouze zařízení s iOSem.

Během přípravy této aktualizace je uživatelský graf dočasně nedostupný. 

#### <a name="always-on-vpn-for-windows-10--1333666---"></a>VPN Always On pro Windows 10<!--1333666 -->

V současné době je možné [Always On](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-auto-trigger-profile#always-on) použít na zařízeních s Windows 10 prostřednictvím vlastního profilu VPN vytvořeného pomocí OMA-URI.

Po této aktualizaci mohou správci přímo v Intune na webu Azure Portal povolit profily sítě VPN Always On pro Windows 10. Profily VPN Always On se automaticky připojí v těchto případech:

- Při přihlášení uživatelů do zařízení
- Při změně sítě na zařízení
- Při opětovném zapnutí obrazovky na zařízení po vypnutí

#### <a name="new-printer-settings-for-education-profiles---1308900---"></a>Nová nastavení tiskárny pro vzdělávací profily<!-- 1308900 -->

Ve vzdělávacích profilech je k dispozici nové nastavení v kategorii **Tiskárny**: **Tiskárny**, **Výchozí tiskárna**, **Přidat nové tiskárny**.

#### <a name="show-caller-id-in-personal-profile---android-enterprise-work-profile--1098984---"></a>Zobrazit ID volajícího v osobním profilu – Android Enterprise Work Profile<!--1098984 -->
Při použití osobního profilu na zařízení nemusí koncoví uživatelé vidět podrobnosti ID volajícího z pracovního kontaktu. 

Od této aktualizace je v části **Android Enterprise** > **Omezení zařízení** > **Nastavení pracovního profilu** k dispozici nové nastavení:
- Zobrazit v osobním profilu ID volajícího pracovního kontaktu

Pokud je povoleno (nenakonfigurováno), podrobnosti volajícího pracovního kontaktu se v osobním profilu zobrazují. V případě blokování se číslo volajícího pracovního kontaktu v osobním profilu nezobrazuje. 

Platí pro: Zařízení s pracovním profilem Android v systému Android OS v6.0 a novějších.

#### <a name="new-windows-defender-credential-guard-settings-added-to-endpoint-protection-settings--1102252-----from-1802-and-1804--"></a>Nová nastavení ochrany přihlašovacích údajů v programu Windows Defender přidaná do nastavení ochrany koncových bodů<!--1102252 --><!--from 1802 and 1804-->

V této aktualizaci zahrnuje [ochrana Credential Guard v programu Windows Defender](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard) (**Konfigurace zařízení** > **Profily** > **Ochrana koncového bodu**) následující nastavení: 

- **Ochrana Credential Guard v programu Windows Defender**: Zapne ochranu přihlašovacích údajů Credential Guard se zabezpečením na základě virtualizace. Pokud je tato funkce zapnutá, budou po dalším restartování přihlašovací údaje chráněny **úrovní zabezpečení platformy, která je nastavená na zabezpečené spouštění,** a zapnutým **zabezpečením založeným na virtualizaci**. Vaše možnosti jsou:
  - **Zakázáno**: Pokud byla ochrana Credential Guard dříve zapnutá možností **Povoleno bez zámku**, vzdáleně vypne ochranu Credential Guard.

  - **Povoleno s uzamčením UEFI**: Zajistí, že ochrana Credential Guard nepůjde vypnout v klíčích registru ani v zásadách skupiny. Pokud jste použili toto nastavení a chcete ochranu Credential Guard zakázat, musíte nastavit zásady skupiny na Zakázáno. Potom bezpečnostní funkci odeberte z každého počítače, u kterého je uživatel fyzicky přítomen. Tyto kroky smažou konfiguraci uloženou v rozhraní UEFI. Dokud je uložená konfigurace UEFI, je povolená i ochrana přihlašovacích údajů Credential Guard.

  - **Povoleno bez zámku**: Umožňuje vzdáleně zakázat ochranu Credential Guard v zásadách skupiny. Na zařízeních s tímto nastavením musí běžet přinejmenším Windows 10 (verze 1511).

Následující související technologie se při konfiguraci ochrany přihlašovacích údajů Credential Guard zapnou automaticky: 

- **Povolit zabezpečení na základě virtualizace (VBS)** : Při příštím restartování povolí zabezpečení na základě virtualizace (VBS). Zabezpečení na základě virtualizace nabízí podporu služeb zabezpečení pomocí hypervisoru Windows a vyžaduje zabezpečené spouštění.
- **Zabezpečené spouštění s přímým přístupem do paměti (DMA)** : Zapne VBS se zabezpečeným spouštěním a přímým přístupem k paměti. Ochrana DMA vyžaduje hardwarovou podporu a povolí se jenom na správně nakonfigurovaných zařízeních. 

#### <a name="use-a-custom-subject-name-on-scep-certificate---2064190---"></a>Použití vlastního názvu subjektu v certifikátu SCEP<!-- 2064190 -->
V profilu certifikátu SCEP můžete u vlastního subjektu použít běžný název **OnPremisesSamAccountName**. Můžete například použít `CN={OnPremisesSamAccountName})`.

#### <a name="block-camera-and-screen-captures-on-android-enterprise-work-profiles---1098977---"></a>Blokování snímků a snímků obrazovky v pracovních profilech Android Enterprise<!-- 1098977 -->
Při konfiguraci omezení zařízení s Androidem jsou k dispozici dvě nové vlastnosti umožňující blokování: 
- Kamera: Blokování přístupu ke všem kamerám na zařízení
- Snímek obrazovky: Blokování vytváření snímků obrazovky a tím také ochrana obsahu před zobrazením na zobrazovacích zařízení, která nemají zabezpečený výstup videa

Platí pro pracovní profily Android Enterprise.

#### <a name="use-cisco-anyconnect-client-for-ios---1333708---"></a>Použití klienta Cisco AnyConnect pro iOS<!-- 1333708 -->

Když vytváříte nový profil VPN pro iOS, jsou teď k dispozici dvě možnosti: **Cisco AnyConnect** a **Cisco Legacy AnyConnect**. Profily Cisco AnyConnect podporují verzi 4.0.7x a novější. Stávající profily VPN Cisco AnyConnect pro iOS jsou označené jako **Cisco Legacy AnyConnect** a budou dál fungovat s Cisco AnyConnect 4.0.5x stejně jako dnes.

> [!NOTE]
> Tato změna platí jen pro iOS. Pro Android, pracovní profily Android Enterprise a macOS bude dál existovat jenom jedna možnost Cisco AnyConnect.


### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="new-enrollment-steps-for-users-on-devices-with-macos-high-sierra-10132--1734567---"></a>Nové kroky registrace pro uživatele na zařízeních s macOS vysokým Sierra 10.13.2 +<!--1734567 -->
Systém macOS high Sierra 10.13.2 představil nový koncept registrace MDM, který vyžaduje schválení uživatelem (User Approved). Schválené registrace umožňují v Intune spravovat některá citlivá nastavení zabezpečení. Další informace najdete v dokumentaci podpory Apple tady: https://support.apple.com/HT208019.

Zařízení zaregistrovaná v aplikaci Portál společnosti pro macOS se považují za neschválená uživatelem, dokud koncový uživatel neotevře předvolby systému a neschválí je ručně. Z tohoto důvodu nyní Portál společnosti pro macOS instruuje uživatele systému macOS 10.13.2 a novějšího, aby na konci procesu registrace přešli do příslušného umístění a ručně registraci schválili. Konzola správce Intune oznámí, zda je zaregistrované zařízení schváleno uživatelem.

#### <a name="jamf-enrolled-macos-devices-can-now-register-with-intune---2370684---"></a>Zařízení macOS zaregistrovaná v Jamf se teď můžou zaregistrovat v Intune.<!-- 2370684 -->
Verze 1.3 a 1.4 portálu společnosti macOS neregistrovaly zařízení Jamf do Intune úspěšně. Verze 1.4.2 portálu macOS tento problém řeší.

#### <a name="updated-help-experience-in-company-portal-app-for-android---1631531---"></a>Aktualizované prostředí pro nápovědu v aplikaci Portál společnosti App pro Android<!-- 1631531 -->
Aktualizovali jsme prostředí nápovědy v aplikaci Portál společnosti pro Android, aby bylo v souladu s osvědčenými postupy pro platformu Android. Když teď dojde k potížím s aplikací, může uživatel klepnout na **Nabídka** > **Nápověda** a:
- Odeslat Microsoftu diagnostický protokol
- Odeslat e-mail s popisem problému a ID incidentu pracovníkovi podpory ve své společnosti  

Pokud si chcete aktualizované prostředí nápovědy prohlédnout, přejděte na [Odeslání protokolů e-mailem](../user-help/send-logs-to-your-it-admin-by-email-android.md) a [Odeslání chyb do Microsoftu](../user-help/send-logs-to-microsoft-android.md).


#### <a name="new-enrollment-failure-trend-chart-and-failure-reasons-table---1471783---"></a>Nový graf trendu selhání registrace a tabulka důvodů selhání<!-- 1471783 -->
Na stránce s přehledem registrací můžete vidět trend neúspěšných registrací a pět nejčastějších příčin selhání. Kliknutím na tento graf nebo tabulku můžete přejít k podrobnostem a najít rady pro řešení problémů a návrhy vedoucí k nápravě.


### <a name="device-management"></a>Správa zařízení

#### <a name="advanced-threat-protection-atp-and-intune-are-fully-integrated---1629303---"></a>Rozšířená ochrana před internetovými útoky (ATP) a Intune jsou plně integrované.<!-- 1629303 -->

[Rozšířená ochrana před internetovými útoky (ATP)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/dashboard-windows-defender-advanced-threat-protection) zobrazuje úroveň rizika u zařízení s Windows 10. V Centru zabezpečení v programu Windows Defender (portál ATP) můžete vytvořit připojení k Microsoft Intune. Jakmile se vytvoří, pomocí zásad dodržování předpisů Intune se určí přijatelná úroveň ohrožení. Pokud dojde k překročení úrovně hrozby, zásada podmíněného přístupu Azure Active Directory (AD) pak může blokovat přístup k různým aplikacím v rámci vaší organizace.

Tato funkce umožňuje ochraně ATP kontrolovat soubory, zjišťovat hrozby a ohlašovat jakákoli rizika pro zařízení s Windows 10.

Viz [Povolení ATP pomocí podmíněného přístupu v Intune](../protect/advanced-threat-protection.md).

#### <a name="support-for-user-less-devices---1637553---"></a>Podpora pro zařízení bez uživatelů<!-- 1637553 -->
U zařízení bez určeného uživatele, jako je Microsoft Surface Hub, podporuje Intune hodnocení dodržování předpisů. Zásady dodržování předpisů mohou cílit na konkrétní zařízení. Dodržování (a nedodržování) předpisů je tedy možné stanovit i u zařízení, která nemají přiřazené uživatele.

#### <a name="delete-autopilot-devices---1713650---"></a>Odstranění zařízení Autopilot<!-- 1713650 -->
Správci Intune mohou [odstranit zařízení AutoPilot](../enrollment/enrollment-autopilot.md#delete-autopilot-devices).

#### <a name="improved-device-deletion-experience--1832333---"></a>Vylepšené prostředí pro odstraňování zařízení<!--1832333 -->
Před [odstraněním zařízení z Intune](../remote-actions/devices-wipe.md#delete-devices-from-the-intune-portal) už nemusíte odebírat firemní data ani na zařízení obnovovat tovární nastavení.

Pokud se chcete podívat na nové prostředí, přihlaste se k Intune a vyberte **Zařízení** > **Všechna zařízení** > název zařízení > **Odstranit**.

Pokud i nadále chcete potvrzovat vymazání nebo vyřazení, můžete použít standardní cestu životního cyklu zařízení a před **odstraněním** vybrat možnost **Odebrat firemní data** a **Obnovení továrního nastavení**. 

#### <a name="play-sounds-on-ios-when-in-lost-mode---1947769---"></a>Přehrávání zvuků v systému iOS v režimu ztráty<!-- 1947769 -->
Pokud jsou sledovaná zařízení s iOSem v [režimu ztráty](../remote-actions/device-lost-mode.md) MDM (Mobile Device Management), můžete [přehrát zvuk](../remote-actions/device-locate.md#activate-lost-mode-sound-alert-on-an-ios-device) (**Zařízení** > **Všechna zařízení** > vyberte zařízení s iOSem > **Přehled** > **Další**). Zvuk se přehrává, dokud je zařízení v režimu ztráty nebo na něm uživatel nevypne zvuk. Platí pro zařízení s iOSem 9.3 nebo novějším.

#### <a name="block-or-allow-web-results-in-searches-made-on-an-intune-device--1972804--"></a>Blokování nebo povolení výsledků hledání na webu v zařízení Intune<!--1972804-->

Správci teď mohou na zařízení blokovat webové výsledky hledání.

#### <a name="improved-error-messaging-for-apple-mdm-push-certificate-upload-failure---2172331---"></a>Vylepšené zasílání zpráv o chybách pro Apple MDM Push Certificate chyba nahrávání<!-- 2172331 -->

Chybová zpráva vysvětluje, že při obnovení stávajícího certifikátu MDM je potřeba použít stejné Apple ID.

#### <a name="test-the-company-portal-for-macos-on-virtual-machines---2216679---"></a>Testování Portál společnosti pro macOS na virtuálních počítačích<!-- 2216679 -->

Zveřejnili jsme pokyny, které správcům IT pomůžou testovat aplikaci Portál společnosti pro macOS na virtuálních počítačích s aplikacemi Parallels Desktop a VMware Fusion. Další informace najdete v článku [Registrace virtuálních počítačů s macOS pro účely testování](../enrollment/macos-enroll.md#enroll-virtual-macos-machines-for-testing).

### <a name="intune-apps"></a>Aplikace Intune

#### <a name="user-experience-update-for-the-company-portal-app-for-ios--1412866---"></a>Aktualizace uživatelského prostředí pro aplikaci Portál společnosti pro iOS<!--1412866 -->
Vydali jsme důležitou aktualizaci uživatelského prostředí aplikace Portál společnosti pro iOS. Tato aktualizace nabízí zcela přepracovaný vzhled aplikace, včetně modernějšího vzhledu a chování. Zachovali jsme funkčnost aplikace, ale zvýšili její využitelnost a přístupnost.  

Další vylepšení:
- Podpora pro iPhone X
- Rychlejší spouštění aplikace a odezva při načítání, které uživateli šetří čas
- Další indikátory průběhu, které uživatelům poskytují aktuální informace o stavu
- Vylepšené nahrávání protokolů, které usnadňuje hlášení vzniklých problémů  

Pokud si chcete nový vzhled prohlédnout, přejděte na [Co je nového v uživatelském rozhraní aplikace](whats-new-app-ui.md).

#### <a name="protect-on-premises-exchange-data-using-intune-app-and-ca---1056954---"></a>Ochrana místních dat Exchange pomocí aplikace a certifikační autority Intune<!-- 1056954 -->
Nově můžete chránit přístup k místním datům systému Exchange z Outlooku Mobile prostřednictvím zásad ochrany aplikací Intune a podmíněného přístupu. Pokud chcete na portálu Azure Portal přidat nebo upravit zásady ochrany aplikací, vyberte **Microsoft Intune** > **Klientské aplikace** > **Zásady ochrany aplikací**. Ještě než začnete tuto funkci využívat, zkontrolujte, že splňujete [požadavky na Outlook pro iOS a Android](https://technet.microsoft.com/library/mt846639(v=exchg.160).aspx).


### <a name="user-interface"></a>Uživatelské rozhraní

#### <a name="improved-device-tiles-in-the-windows-10-company-portal--2213364---"></a>Vylepšené dlaždice zařízení ve Windows 10 Portál společnosti<!--2213364 -->

Aktualizovali jsme dlaždice, aby je dokázali přečíst i uživatelé se zhoršeným zrakem a aby fungovaly lépe s nástroji na čtení obrazovky.

#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos---2216677---"></a>Odesílání diagnostických sestav v aplikaci Portál společnosti pro macOS<!-- 2216677 -->
Aktualizovali jsme aplikaci Portál společnosti pro zařízení s macOS a zlepšili jsme způsob, jakým uživatelé nahlašují chyby týkající se Intune. Co aplikace Portál společnosti zaměstnancům umožňuje:

- Posílat diagnostická hlášení přímo vývojovému týmu Microsoft.
- Posílat e-mailem ID incidentů týmu IT podpory vaší společnosti.

Další informace najdete v článku o [posílání chyb ze zařízení s macOS](../user-help/send-errors-macos.md).

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10---1195010---"></a>V Portál společnosti aplikaci pro Windows 10 se Intune přizpůsobí systému pro návrh Fluent.<!-- 1195010 -->
Aplikace Portál společnosti Intune pro Windows 10 byla aktualizována o [navigační zobrazení systému návrhu FDS](https://docs.microsoft.com/windows/uwp/design/basics/navigation-basics). Po straně aplikace je statický svislý seznam všech hlavních stránek. Když na odkaz kliknete, stránka se rychle zobrazí nebo můžete mezi stránkami přepínat. Jde o první z řady aktualizací, které jsou výsledkem naší trvalé snahy o vytvoření přizpůsobivého, empatického a známého prostředí Intune. Pokud si chcete nový vzhled prohlédnout, přejděte na [Co je nového v uživatelském rozhraní aplikace](whats-new-app-ui.md).

<!-- ########################## -->
## <a name="march-2018"></a>Březen 2018

### <a name="app-management"></a>Správa aplikací

#### <a name="alerts-for-expiring-ios-line-of-business-lob-apps-for-microsoft-intune---748789---"></a>Výstrahy na vypršení platnosti obchodních aplikací (LOB) pro iOS pro Microsoft Intune<!-- 748789 -->

Na portálu Azure Portal vás Intune upozorní na obchodní aplikace pro iOS, jejichž platnost brzy vyprší. Při nahrání nové verze obchodní aplikace pro iOS Intune oznámení o vypršení platnosti ze seznamu aplikací odebere. Toto oznámení o vypršení platnosti bude aktivní jen u nově nahraných obchodních aplikací pro iOS. 30 dní před vypršením platnosti profilu pro zřizování obchodních aplikací pro iOS se zobrazí upozornění. Potom se výstraha změní na Platnost vypršela.

#### <a name="customize-your-company-portal-themes-with-hex-codes--1049561---"></a>Přizpůsobení Portál společnostich motivů pomocí hexadecimálních kódů<!--1049561 -->

Pomocí šestnáctkových kódů si můžete přizpůsobit barvu motivu v aplikacích Portál společnosti. Když zadáte šestnáctkový kód, Intune určí barvu textu, která poskytuje nejvyšší úroveň kontrastu mezi barvou textu a barvou pozadí. Můžete si zobrazit náhled barvy textu a loga společnosti oproti barvě v části **Klientské aplikace** > **Portál společnosti**.

### <a name="including-and-excluding-app-assignment-based-on-groups-for-android-enterprise---1813081---"></a>Zahrnutí a vyloučení přiřazení aplikací na základě skupin pro Android Enterprise<!-- 1813081 -->

Android Enterprise (dříve Android for Work) umožňuje zahrnout nebo vyloučit skupiny, ale nepodporuje vytvořené integrované skupiny **Všichni uživatelé** a **Všechna zařízení**. Podrobnosti najdete v tématu [Zahrnutí a vyloučení přiřazení aplikací v Microsoft Intune](../apps/apps-inc-exl-assignments.md).


### <a name="device-management"></a>Správa zařízení

### <a name="export-all-devices-into-csv-files-in-ie-microsoft-edge-or-chrome---2258071---"></a>Export všech zařízení do souborů CSV v IE, Microsoft Edge nebo Chrome<!-- 2258071 -->
V části **Zařízení** > **Všechna zařízení** můžete **exportovat** zařízení do seznamu ve formátu CSV. Uživatelé Internet Exploreru s více než 10 000 zařízeními můžou zařízení úspěšně vyexportovat do více souborů. Každý z nich může obsahovat až 10 000 zařízení.

Uživatelé Microsoft Edge a Chrome s >mi 30000 zařízeními můžou zařízení úspěšně vyexportovat do více souborů. Každý z nich může obsahovat až 30 000 zařízení.

V tématu [Správa zařízení](../remote-actions/device-management.md) se dozvíte podrobnosti o tom, co můžete se spravovanými zařízeními dělat.

#### <a name="new-security-enhancements-in-the-intune-service----1637539---"></a>Nová vylepšení zabezpečení ve službě Intune <!-- 1637539 -->   

Zavedli jsme přepínací tlačítko v Intune v Azure, které můžou používat samostatné zákazníky Intune, aby pocházely s zařízeními bez jakýchkoli zásad přiřazených jako **kompatibilních** (funkce zabezpečení vypnuté), nebo aby tato zařízení považovala za **nekompatibilní** (funkce zabezpečení zapnuté) To zajistí přístup k prostředkům až po vyhodnocení dodržování předpisů zařízením.

Dopad této funkce závisí na tom, zda už máte přiřazené zásady dodržování předpisů nebo nikoliv.

- Pokud patříte mezi nové nebo stávající účty a nemáte ke svým zařízením přiřazené žádné zásady dodržování předpisů, je tento přepínač automaticky nastaven na **Vyhovující předpisům**. V konzole bude je funkce ve výchozím nastavení vypnutá. Na koncové uživatele to nemá žádný vliv.
- Pokud patříte mezi stávající účty a máte nějaká zařízení, ke kterým jsou přiřazené zásady dodržování předpisů, je tento přepínač automaticky nastaven na **Nevyhovující předpisům**. Od zavedení březnové aktualizace je tato funkce ve výchozím nastavení zapnutá.

Pokud používáte zásady dodržování předpisů s podmíněným přístupem a tato funkce je zapnutá, jsou teď všechna zařízení bez alespoň jedné přiřazené zásady dodržování předpisů blokovaná podmíněným přístupem. Koncoví uživatelé přidružení k těmto zařízením, kteří měli předtím přístup k e-mailu, o tento přístup přijdou, dokud všem zařízením nepřiřadíte alespoň jednu zásadu dodržování předpisů.   

Mějte na paměti, že ačkoliv se výchozí stav tlačítka zobrazí v uživatelském rozhraní bezprostředně po březnových aktualizacích služby Intune, nevynutí se okamžitě. Veškeré provedené změny přepínacího tlačítka ovlivní dodržování předpisů zařízením až poté, co tlačítko na vašem účtu aktivujeme. Až dokončíme váš účet, informujte vás prostřednictvím centra zpráv. Po provedení březnových aktualizací to může trvat několik dní.

**Další informace**: [https://aka.ms/compliance_policies](https://aka.ms/compliance_policies)

#### <a name="enhanced-jailbreak-detection---846515---"></a>Vylepšené zjišťování jailbreaků<!-- 846515 -->

Vylepšené zjišťování jailbreaků je novým nastavením dodržování předpisů, které zlepší způsob, jak Intune vyhodnocuje zařízení s jailbreakem. Toto nastavení způsobí, že se zařízení bude v Intune vracet častěji, což používá služby zjišťování polohy zařízení a ovlivňuje využití baterie.

#### <a name="reset-passwords-for-android-o-devices---1238299---"></a>Resetování hesel pro zařízení s Androidem O<!-- 1238299 -->
U zaregistrovaných zařízení s Androidem 8.0 a pracovním profilem můžete resetovat hesla. Když do zařízení s Androidem 8.0 pošlete žádost o resetování hesla, nastaví se aktuálnímu uživateli nové heslo pro odemčení zařízení nebo výzva spravovaného profilu. Po zaslání se heslo nebo výzva okamžitě projeví.

#### <a name="targeting-compliance-policies-to-devices-in-device-groups--1307012---"></a>Zaměření zásad dodržování předpisů na zařízení ve skupinách zařízení<!--1307012 -->

Můžete cílit zásady dodržování předpisů na uživatele ve skupinách uživatelů. Od této aktualizace můžete cílit zásady dodržování předpisů na zařízení ve skupinách zařízení. Zařízení cílená jako součást skupiny zařízení nebudou přijímat akce při nedodržení předpisů.

#### <a name="new-management-name-column---1333586---"></a>Nový sloupec pro název správy<!-- 1333586 -->
 V okně zařízení přibyl nový sloupec s názvem **Název správy**. Půjde o automaticky generovaný název bez možnosti úprav, který bude přiřazený podle zařízení na základě tohoto vzorce:
- Výchozí název pro všechna zařízení: <username><em><devicetype></em><enrollmenttimestamp>
- Pro hromadně přidaná zařízení: <PackageId/ProfileId><em><DeviceType></em><EnrollmentTime>

Je to volitelný sloupec v okně zařízení. Není k dispozici ve výchozím nastavení a přístup k němu je jen přes výběr sloupců. Na název zařízení nemá tento nový sloupec vliv.

#### <a name="ios-devices-are-prompted-for-a-pin-every-15-minutes--1550837---"></a>zařízení se systémem iOS se zobrazí výzva k zadání kódu PIN každých 15 minut.<!--1550837 -->
Po použití zásad dodržování předpisů nebo konfigurace u zařízení s iOSem se uživatelům každých 15 minut zobrazí výzva k zadání PINu. Uživatelům se výzva zobrazuje tak dlouho, dokud PIN nenastaví.

#### <a name="schedule-your-automatic-updates--1805514---"></a>Naplánování automatických aktualizací<!--1805514 -->
Pomocí [nastavení aktualizačního okruhu Windows](../protect/windows-update-for-business-configure.md) máte v Intune možnost řídit instalaci automatických aktualizací. Od této aktualizace můžete naplánovat opakované aktualizace na základě týdne, dne a času.

#### <a name="use-fully-distinguished-name-as-subject-for-scep-certificate--2221763---"></a>Jako předmět certifikátu SCEP použijte plně rozlišující název.<!--2221763 -->
Při vytváření profilu certifikátu SCEP zadáváte název subjektu. Od této aktualizace můžete jako subjekt použít plně rozlišující název. Jako **Název subjektu** vyberte **Vlastní** a pak zadejte `CN={{OnPrem_Distinguished_Name}}`. Pokud chcete použít proměnnou `{{OnPrem_Distinguished_Name}}`, nezapomeňte synchronizovat atribut uživatele `onpremisesdistingishedname` pomocí služby [Azure Active Directory (AD) Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) se službou Azure AD.

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="enable-bluetooth-contact-sharing---android-for-work--1098983---"></a>Povolení sdílení kontaktů přes Bluetooth – Android for Work<!--1098983 -->
Ve výchozím nastavení Android brání v synchronizaci kontaktů v pracovním profilu se zařízeními Bluetooth. V důsledku toho se kontakty pracovního profilu nezobrazují na ID volajícího u zařízení Bluetooth.

Od této aktualizace je v části **Android for Work** > **Omezení zařízení** > **Nastavení pracovního profilu** k dispozici nové nastavení:
- Sdílení kontaktů přes Bluetooth

Správce Intune může toto nastavení nakonfigurovat a povolit sdílení. Toto nastavení je užitečné při párování zařízení se zařízením Bluetooth do auta, které zobrazuje ID volajícího při použití hands-free. Pokud je nastavení povoleno, kontakty pracovního profilu se zobrazí. Pokud není nastavení povoleno, kontakty pracovního profilu se nezobrazí.

#### <a name="configure-gatekeeper-to-control-macos-app-download-source---1690459---"></a>Konfigurace serveru gatekeeper pro řízení zdroje stahování aplikace macOS<!-- 1690459 -->

Můžete konfigurovat Gatekeepera, aby vaše zařízení chránil před aplikacemi díky kontrole nad tím, odkud je možné aplikace stahovat. Nakonfigurovat můžete tyto zdroje stahování: **Mac App Store**, **Mac App Store a identifikovaní vývojáři** nebo **Kdekoliv**. Kromě toho je možné nakonfigurovat, jestli uživatelé smí nainstalovat aplikaci kliknutím se stisknutou klávesou Control, které tuto kontrolu Gatekeepera přepíše.

Tato nastavení najdete v části **Konfigurace zařízení** -> **Vytvořit profil** -> **macOS** -> **Ochrana koncového bodu**.

#### <a name="configure-the-mac-application-firewall---1690461---"></a>Konfigurace brány firewall pro aplikace pro Mac<!-- 1690461 -->

Je možné nakonfigurovat bránu firewall pro aplikace pro Mac. Můžete to využít k řízení připojení na základě jednotlivých aplikací místo na základě portů. Díky tomu snadněji využijete výhod ochrany pomocí brány firewall a pomůže vám to zabránit nežádoucím aplikacím v převzetí kontroly nad síťovými porty otevřenými pro oprávněné aplikace.

Tuto funkci najdete v části **Konfigurace zařízení** -> **Vytvořit profil** -> **macOS** -> **Ochrana koncového bodu**.

Jakmile nastavení brány firewall povolíte, můžete ji nakonfigurovat pomocí dvou strategií:

- Blokovat všechna příchozí připojení

   Můžete blokovat všechna příchozí připojení u cílových zařízení. Pokud se k tomu rozhodnete, zablokují se příchozí připojení u všech aplikací.

- Povolit nebo blokovat konkrétní aplikace

   Můžete povolit nebo blokovat příjem příchozích připojení u konkrétních aplikací. Můžete také povolit neviditelný režim, který zabrání odpovědím na zjišťovací požadavky.

#### <a name="detailed-error-codes-and-messages---1376342---"></a>Podrobné kódy a zprávy o chybách<!-- 1376342 -->

V Konfiguraci zařízení jsou k dispozici podrobnější kódy chyb a chybové zprávy. Toto vylepšené generování sestav obsahuje nastavení, stav těchto nastavení a podrobnosti o řešení potíží.

##### <a name="more-information"></a>Další informace

- Blokovat všechna příchozí připojení

   Tím se zablokuje příjem příchozích připojení u všech služeb sdílení (jako sdílení souborů a obrazovky). Služby systému, které mají příjem příchozích připojení stále povolený, jsou:
  - configd – implementuje DHCP a další služby konfigurace sítě
  - mDNSResponder – implementuje Bonjour
  - Racoon – implementuje protokol IPSec.

    Abyste mohli služby sdílení používat, musí být **Příchozí připojení** nastavené na **Nenakonfigurováno** (ne **Blokovat**).

- Neviditelný režim

   Povolením zabráníte počítači v odpovídání na zjišťovací požadavky. Počítač bude nadále odpovídat na požadavky oprávněných aplikací. Neočekávané požadavky, jako je ICMP (ping), se ignorují.

#### <a name="disable-checks-on-device-restart--1805490---"></a>Zakázat kontrolu restartování zařízení<!--1805490 -->
V Intune máte možnost řídit [správu aktualizací softwaru](../protect/windows-update-for-business-configure.md). Od této aktualizace je k dispozici vlastnost <strong>Kontroly při restartu</strong>, která je ve výchozím nastavení povolená. Pokud chcete přeskočit typické kontroly, které se provádí při restartu zařízení (například aktivní uživatelé, stav baterie a další), vyberte <strong>Přeskočit</strong>.

#### <a name="new-windows-10-insider-preview-channels-available-for-deployment-rings---1746293---"></a>Nové kanály Windows 10 Insider Preview dostupné pro kroužky nasazení<!-- 1746293 -->
Nově můžete při vytváření aktualizačního kanálu nasazení Windows 10 vybrat tyto kanály pro údržbu Windows 10 Insider Preview:
- Sestavení Windows Insider – Fast
- Sestavení Windows Insider – Slow
- Sestavení Windows Insider – Release 

Podrobnosti o těchto kanálech najdete v tématu [Správa sestavení Insider Preview](https://insider.windows.com/en-us/for-business-getting-started/#explore).
Informace o vytváření kanálů nasazení v Intune najdete v tématu [Správa softwarových aktualizací v Intune](../protect/windows-update-for-business-configure.md).

### <a name="new-windows-defender-exploit-guard-settings---1631893---"></a>Nové nastavení ochrany zneužití v programu Windows Defender<!-- 1631893 -->

Nově je k dispozici šest nových nastavení <strong>Omezení možností útoku</strong> a rozšířené možnosti <strong>Řízený přístup ke složkám: Ochrana složek</strong>. Tato nastavení najdete tady: Konfigurace zařízení\Profily\
Vytvořit profil\Ochrana koncového bodu\Ochrana Exploit Guard v programu Windows Defender.

#### <a name="attack-surface-reduction"></a>Omezení možností útoku

|Název nastavení  |Možnosti nastavení  |Popis  |
|---------|---------|---------|
|Advanced ransomware protection (Rozšířená ochrana před ransonwarem)|Povoleno, Audit, Nenakonfigurováno|Umožňuje použít agresivní ochranu před ransomwarem.|
|Flag credential stealing from the Windows local security authority subsystem (Označit příznakem použití jiných přihlašovacích údajů ze subsystému Windows Local Security Authority)|Povoleno, Audit, Nenakonfigurováno|Umožňuje označit příznakem použití jiných přihlašovacích údajů ze subsystému Windows Local Security Authority (lsass.exe).|
|Process creation from PSExec and WMI commands (Vytvoření procesů z příkazů PSExec a WMI)|Blokovat, Audit, Nenakonfigurováno|Umožňuje zablokovat vytváření procesů pocházejících z příkazů PSExec a WMI.|
|Untrusted and unsigned processes that run from USB (Nedůvěryhodné a nepodepsané procesy spouštěné z USB)|Blokovat, Audit, Nenakonfigurováno|Umožňuje zablokovat nedůvěryhodné a nepodepsané procesy, které se spouští z USB.|
|Spustitelné soubory, které nesplňují kritéria prevalence, stáří nebo seznamu důvěryhodných souborů|Blokovat, Audit, Nenakonfigurováno|Umožňuje zablokovat spuštění spustitelných souborů, dokud nesplní kritéria prevalence, stáří nebo seznamu důvěryhodných položek.|

#### <a name="controlled-folder-access"></a>Řízený přístup ke složkám

|              Název nastavení               |                                                              Možnosti nastavení                                                              | Popis |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| Ochrana složek (již implementováno) | Nenakonfigurováno, Povolit, Pouze audit (již implementováno)<br><br> <strong>Nová</strong><br>Block disk modification (Blokovat změny disku), Audit disk modification (Auditovat změny disku) |             |

Umožňuje chránit soubory a složky před neautorizovanými změnami od neznámých aplikací.<br><br>**Povolit**: Brání nedůvěryhodným aplikacím ve změnách nebo odstranění souborů v chráněných složkách a v zápisu do sektorů disku.<br><br>
**Block disk modification only** (Blokovat jenom změny disku):<br>Umožňuje zablokovat nedůvěryhodným aplikacím možnost zapisovat do sektorů disku. Nedůvěryhodné aplikace stále můžou změnit nebo odstranit soubory v chráněných složkách.|

### <a name="intune-apps"></a>Aplikace Intune

### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview---710595---"></a>Azure Active Directory weby můžou vyžadovat aplikaci Intune Managed Browser a podporovat jednotné přihlašování pro Managed Browser (Public Preview).<!-- 710595 -->

Pomocí Azure Active Directory (Azure AD) můžete přístup k webovým stránkám na mobilních zařízeních omezit na aplikaci Intune Managed Browser. V Managed Browseru zůstanou data webových stránek zabezpečená a oddělená od osobních dat koncových uživatelů. Kromě toho bude Managed Browser podporovat možnosti jednotného přihlašování pro weby chráněné pomocí Azure AD. Přihlášení k Managed Browseru nebo jeho používání na zařízení s jinou aplikací, kterou spravuje Intune, umožňuje, aby měl Managed Browser přístup k podnikovým webům chráněným pomocí Azure AD, aniž by uživatel musel zadávat své přihlašovací údaje. Tato funkce se vztahuje na weby jako Outlook Web Access (OWA) a SharePoint Online i na jiné podnikové weby jako prostředky v intranetu, ke kterým se přistupuje prostřednictvím proxy aplikace Azure. Další informace najdete v tématu [řízení přístupu v Azure Active Directory podmíněný přístup](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls).

#### <a name="company-portal-app-for-android-visual-updates--976944---"></a>Aplikace Portál společnosti pro Visual Update pro Android<!--976944 -->

Aktualizovali jsme aplikaci Portál společnosti pro Android v souladu s pokyny pro [Material Design](https://material.io/) Androidu. Obrázky nových ikon najdete v [novinkách v uživatelském rozhraní aplikací](whats-new-app-ui.md).

#### <a name="company-portal-enrollment-improved---1874230-eeready--"></a>Vylepšení registrace Portál společnosti<!-- 1874230 eeready-->
Uživatelé, kteří registrují zařízení pomocí Portálu společnosti ve Windows 10 sestavení 1703 a vyšším, teď můžou dokončit první krok registrace bez opuštění aplikace.
#### <a name="hololens-and-surface-hub-now-appear-in-device-lists--1725868---"></a>HoloLens a Surface Hub se nyní zobrazují v seznamech zařízení<!--1725868 -->
Do aplikace Portál společnosti pro Android jsme přidali podporu zobrazení zařízení HoloLens a Surface Hub zaregistrovaných v Intune.

#### <a name="custom-book-categories-for-volume-purchase-program-vpp-ebooks---1488911---"></a>Vlastní kategorie knih pro e-knihy programu Volume-purchase program (VPP)<!-- 1488911 -->
Můžete vytvářet vlastní kategorie e-knih a pak k nim přiřadit e-knihy v rámci programu VPP. Koncoví uživatelé pak uvidí nově vytvořené kategorie e-knih a knihy k nim přiřazené. Podrobnosti najdete v tématu [Správa aplikací a knih zakoupených v rámci multilicenčního programu pomocí Microsoft Intune](../apps/vpp-apps.md).  

#### <a name="support-changes-for-company-portal-app-for-windows-send-feedback-option---2070166---"></a>Podpora změn pro možnost Odeslat názor z aplikace Portál společnosti pro Windows<!-- 2070166 -->
Od 30. dubna 2018 bude možnost **Váš názor** v aplikaci Portál společnosti pro Windows fungovat pouze u zařízení se systémem Windows 10 Anniversary Update (1607) a novějším. Možnost odeslání názoru se už nebude podporovat při použití aplikace Portál společnosti pro Windows se systémem:  
- Windows 10, verze 1507  
- Windows 10, verze 1511  
- Wvdows Phone 8.1

Pokud vaše zařízení používá Windows 10 RS1 nebo novější, stáhněte si nejnovější verzi aplikace Portál společnosti pro Windows ze Storu. Pokud používáte nepodporovanou verzi, odesílejte své názory prostřednictvím následujících kanálů:
- Aplikace Centrum Feedback ve Windows 10
- E-mail WinCPfeedback@microsoft.com  

#### <a name="new-windows-defender-application-guard-settings---1631890---"></a>Nové nastavení ochrany Application Guard v programu Windows Defender<!-- 1631890 -->

- **Enable graphics acceleration (Povolit akceleraci grafiky)** : Správci můžou pro Ochranu Application Guard v programu Windows Defender povolit virtuální grafický procesor. Toto nastavení umožní procesoru přesunout vykreslování grafiky na virtuální grafický procesor. Může zlepšit výkon při práci s graficky náročnými weby nebo při sledování videa v kontejneru.

- **SaveFilestoHost**: Správci můžou povolit předávání souborů z Microsoft Edge, který běží v kontejneru, do hostitelského souborového systému. Zapnutím tohoto nastavení umožníte uživatelům stahovat soubory z Microsoft Edge v kontejneru do hostitelského souborového systému.

#### <a name="mam-protection-policies-targeted-based-on-management-state---1665993---"></a>Cílení na zásady ochrany MAM na základě stavu správy<!-- 1665993 -->
Můžete cílit na zásady MAM na základě stavu správy zařízení:
- **Zařízení s Androidem**: Je možné cílit na nespravovaná zařízení, zařízení spravovaná v Intune a Android Enterprise Profiles spravované v Intune (dříve Android for Work).
- **Zařízení s iOS**: Je možné cílit na nespravovaná zařízení (jen MAM) nebo zařízení spravovaná v Intune.

    > [!NOTE]
    > - Podporu této funkce pro iOS budeme zavádět v průběhu dubna 2018.

Podrobnosti najdete v tématu [Cílení zásad ochrany aplikací na základě stavu správy zařízení](../apps/app-protection-policies.md).

#### <a name="improvements-to-the-language-in-the-company-portal-app-for-windows---1683758---"></a>Vylepšení jazyka v aplikaci Portál společnosti pro Windows<!-- 1683758 -->
Vylepšili jsme jazyk v aplikaci Portál společnosti pro Windows 10 tak, aby byl uživatelsky přívětivější a lépe přizpůsobený vaší firmě. Obrázky s ukázkami změn najdete v tématu [Co je nového v uživatelském rozhraní aplikací](whats-new-app-ui.md).

#### <a name="new-additions-to-our-docs-about-user-privacy---1440709---"></a>Nové dodatky k naší dokumentaci o ochraně osobních údajů uživatelů<!-- 1440709 -->
V rámci naší snahy poskytnout koncovým uživatelům větší kontrolu nad jejich daty a ochranou osobních údajů jsme zaktualizovali naše dokumenty, v nichž vysvětlujeme, jak zobrazit a odebrat data lokálně uložená aplikacemi Portál společnosti. Tyto novinky najdete zde:

- **Android**: [Odebrání zařízení s Androidem z Intune](../user-help/unenroll-your-device-from-intune-android.md)
- **Android, pokud uživatel odmítnul Podmínky použití**: [Odebrání správy zařízení, pokud jste odmítli Podmínky použití](../user-help/unenroll-your-device-from-intune-if-you-declined-terms-of-use-android.md)
- **iOS**: [Odebrání zařízení s iOSem z Intune](../user-help/unenroll-your-device-from-intune-ios.md)
- **Windows**: [Odebrání zařízení s Windows z Intune](../user-help/unenroll-your-device-from-intune-windows.md)

<!-- ########################## -->
## <a name="february-2018"></a>Únor 2018

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="intune-support-for-multiple-apple-dep--apple-school-manager-accounts---747685---"></a>Podpora Intune pro víc účtů Apple DEP/Apple School Manageru<!-- 747685 -->

Intune teď podporuje registraci zařízení z až 100 různých účtů [Apple Device Enrollment Program (DEP)](../enrollment/device-enrollment-program-enroll-ios.md) nebo [Apple School Manager](../enrollment/apple-school-manager-set-up-ios.md). Pro každý nahraný token lze profily registrace a zařízení spravovat samostatně. K jednotlivým nahraným tokenům DEP nebo School Manager lze automaticky přiřadit různé profily registrace. Pokud je nahraných více tokenů School Manager, může se v každém okamžiku sdílet pomocí služby Microsoft School Data Sync jenom jeden.

Po dokončení migrace už nebudou fungovat beta verze rozhraní Graph API a publikované skripty pro správu Apple DEP nebo ASM přes rozhraní Graph. Nové beta verze rozhraní Graph API jsou ve vývoji a budou se vydávat po dokončení migrace.

#### <a name="see-enrollment-restrictions-per-user---1634444-eeready-wnready---"></a>Viz omezení registrace na uživatele.<!-- 1634444 eeready wnready -->
V okně **Řešení potíží** teď můžete zobrazit platná [omezení registrace](../enrollment/enrollment-restrictions-set.md) pro jednotlivé uživatele tak, že v seznamu **Přiřazení** vyberete **Omezení registrace**.

#### <a name="new-option-for-user-authentication-for-apple-bulk-enrollment---747625-eeready---"></a>Nová možnost pro ověřování uživatelů pro hromadnou registraci Apple<!-- 747625 eeready -->

> [!NOTE]
> U nových tenantů se projeví okamžitě. U stávajících tenantů bude tato funkce zavedena v průběhu dubna. Až do zavedení nemusíte mít k těmto novým funkcím přístup.

Intune teď nabízí možnost ověřovat zařízení pomocí aplikace Portál společnosti u těchto metod registrace:

- Program Apple Device Enrollment Program
- Apple School Manager
- Registrace Apple Configuratoru

Při použití možnosti Portálu společnosti lze vynutit vícefaktorové ověřování Azure Active Directory bez blokování těchto metod registrace.

Při použití možnosti Portálu společnosti pro registraci přidružení uživatelů přeskočí Intune ověřování uživatelů v Pomocníkovi s nastavením iOSu. To znamená, že zařízení se napřed zaregistruje jako zařízení bez uživatelů a neobdrží tedy konfigurace ani zásady pro skupiny uživatelů. Obdrží jenom konfigurace a zásady pro skupiny zařízení. Intune ale na toto zařízení automaticky nainstaluje aplikaci Portál společnosti. První uživatel, který aplikaci Portál společnosti spustí a přihlásí se do ní, se v Intune přidruží k tomuto zařízení. V tomto okamžiku pak obdrží konfigurace a zásady dané skupiny uživatelů. Přidružení uživatelů není možné změnit bez opětovné registrace.

#### <a name="intune-support-for-multiple-apple-dep--apple-school-manager-accounts---747685-eeready---"></a>Podpora Intune pro víc účtů Apple DEP/Apple School Manageru<!-- 747685 eeready -->

Intune teď podporuje registraci zařízení z až 100 různých účtů Apple DEP (Device Enrollment Program) nebo Apple School Manager. Pro každý nahraný token lze profily registrace a zařízení spravovat samostatně. K jednotlivým nahraným tokenům DEP nebo School Manager lze automaticky přiřadit různé profily registrace. Pokud je nahraných více tokenů School Manager, může se v každém okamžiku sdílet pomocí služby Microsoft School Data Sync jenom jeden.

Po dokončení migrace už nebudou fungovat beta verze rozhraní Graph API a publikované skripty pro správu Apple DEP nebo ASM přes rozhraní Graph. Nové beta verze rozhraní Graph API jsou ve vývoji a budou se vydávat po dokončení migrace.

### <a name="remote-printing-over-a-secure-network---1709994----"></a>Vzdálený tisk přes zabezpečenou síť<!-- 1709994  -->
Řešení bezdrátového mobilního tisku v PrinterOn umožní uživatelům vzdáleně tisknout odkudkoli přes zabezpečenou síť. PrinterOn se integruje s Intune App SDK pro iOS i Android. Zásady ochrany aplikací budete moct cílit na tuto aplikaci pomocí okna **Zásady ochrany aplikací** v Intune v konzole pro správu. Koncoví uživatelé si budou moct stáhnout aplikaci PrinterOn for Microsoft prostřednictvím Obchodu Play nebo iTunes a pak ji používat ve svém ekosystému Intune.

### <a name="macos-company-portal-support-for-enrollments-that-use-the-device-enrollment-manager---1352411---"></a>Podpora macOS Portál společnosti pro registrace, které používají správce registrace zařízení<!-- 1352411 -->

Uživatelé teď můžou používat Správce registrace zařízení při registraci na Portálu společnosti v macOS.

### <a name="device-management"></a>Správa zařízení

#### <a name="windows-defender-health-status-and-threat-status-reports--854704---"></a>Stavové zprávy o stavu hrozeb v programu Windows Defender<!--854704 -->

Klíčem ke správě počítačů s Windows je pochopení stavu programu Windows Defender.  Touto aktualizací Intune přidá do stavu agenta Windows Defender nové sestavy a akce. Pomocí souhrnné sestavy stavu v [úloze dodržování předpisů zařízením](../protect/compliance-policy-monitor.md) zjistíte, která zařízení vyžadují:
- aktualizaci signatur,
- Restartovat
- ruční zásah,
- úplnou kontrolu,
- stavy ostatních agentů vyžadujících zásah.

Podrobná sestava pro jednotlivé kategorie stavu uvádí jednotlivé počítače, které vyžadují pozornost, nebo ty, které jsou **čisté**.

#### <a name="new-privacy-settings-for-device-restrictions--1308926---"></a>Nové nastavení ochrany osobních údajů pro omezení zařízení<!--1308926 -->
Pro zařízení jsou k dispozici [dvě nová nastavení ochrany osobních údajů](../configuration/device-restrictions-windows-10.md#privacy):
- **Publikovat aktivity uživatele**: Tuto možnost nastavte na **Blokovat**, pokud chcete zabránit ve sdílení a zjišťování naposledy použitých prostředků při přepínání úloh.
- **Jen místní aktivity**: Tuto možnost nastavte na **Blokovat**, pokud chcete zabránit ve sdílení a zjišťování naposledy použitých prostředků při přepínání úloh jen u místní aktivity.

#### <a name="new-settings-for-the-microsoft-edge-browser--1469166---"></a>Nová nastavení pro prohlížeč Microsoft Edge<!--1469166 -->
Pro zařízení s prohlížečem Microsoft Edge jsou teď k dispozici [dvě nová nastavení](../configuration/device-restrictions-windows-10.md#microsoft-edge-browser): **Path to favorites file** (Cesta k souboru oblíbených položek) a **Changes to Favorites** (Změny oblíbených položek).

### <a name="app-management"></a>Správa aplikací

#### <a name="protocol-exceptions-for-applications--1035509---"></a>Výjimky protokolu pro aplikace<!--1035509 -->

Můžete teď vytvořit výjimky ze zásady přenosu dat ve správě mobilních dat Intune, abyste mohli otevřít konkrétní nespravované aplikace. Tyto aplikace musí být pro IT důvěryhodné. Pokud zásady přenosu dat nastavíte **jenom na spravované aplikace**, bude kromě vytvořených výjimek přenos dat i nadále omezený jen na aplikace, které se spravují přes Intune. Tato omezení můžete vytvořit pomocí protokolů (iOS) nebo balíčků (Android).

Do zásad přenosu aplikací MAM můžete například přidat jako výjimku balíček Webex. To umožní, aby se odkazy Webex ve spravované outlookové e-mailové zprávě otevíraly přímo v aplikaci Webex. V ostatních nespravovaných aplikacích bude přenos dat i nadále omezen. Další informace najdete v tématu [Výjimky zásad přenosu dat pro aplikace](../apps/app-protection-policies-exception.md).

#### <a name="windows-information-protection-wip-encrypted-data-in-windows-search-results---1469193---"></a>Zašifrovaná data Windows Information Protection (nedokončená výroba) ve výsledcích hledání ve Windows<!-- 1469193 -->
Nastavení v zásadách Windows Information Protection (WIP) vám teď umožňuje řídit, jestli se mají do výsledků hledání ve Windows zahrnovat šifrovaná data WIP. Tuto možnost zásad ochrany aplikací nastavíte tak, že v zásadách Windows Information Protection v části **Upřesnit nastavení** vyberete **Povolit Windows Search Indexeru prohledávat šifrované položky**. Zásady ochrany aplikací musí být nastavené pro platformu *Windows 10* a možnost **Stav registrace** musí být nastavená na hodnotu **S registrací**. Další informace najdete v části týkající se možnosti [Povolit Windows Search Indexeru prohledávat šifrované položky](../apps/windows-information-protection-policy-create.md#allow-windows-search-indexer-to-search-encrypted-items).

#### <a name="configuring-a-self-updating-mobile-msi-app---1740840---"></a>Konfigurace automaticky aktualizované mobilní aplikace MSI<!-- 1740840 -->
Známou automaticky aktualizovanou mobilní aplikaci MSI můžete nakonfigurovat tak, aby ignorovala proces kontroly verzí. Tato možnost je užitečná, když chcete předejít konfliktu časování. K tomuto typu konfliktu časování může například dojít, když aplikaci automaticky aktualizuje vývojář a současně Intune. Jak vývojář, tak Intune můžou vynucovat verzi aplikace na klientovi Windows, což může způsobit konflikt. Pro tyto automaticky aktualizované aplikace MSI můžete v okně **Informace o aplikaci** nakonfigurovat nastavení **Ignorovat verzi aplikace**. Po přepnutí tohoto nastavení na **Ano** bude Microsoft Intune ignorovat verzi aplikace, která je nainstalovaná na klientovi Windows.

#### <a name="related-sets-of-app-licenses-supported-in-intune---1864117---"></a>Související sady licencí aplikací podporovaných v Intune<!-- 1864117 -->
Intune na portálu Azure Portal teď podporuje související sady licencí aplikací jako jedinou položku aplikace v uživatelském rozhraní. Kromě toho všechny aplikace licencované offline a synchronizované z Microsoft Storu pro firmy se sloučí do jediné položky aplikace a všechny podrobnosti nasazení z jednotlivých balíčků se budou migrovat do jediné položky. Pokud se chcete podívat na související sady licencí aplikací na portálu Azure Portal, vyberte **Licence aplikací** v okně **Klientské aplikace**.

### <a name="device-configuration"></a>Konfigurace zařízení
#### <a name="windows-information-protection-wip-file-extensions-for-automatic-encryption---1463582---"></a>Přípony souborů Windows Information Protection (nedokončené výroby) pro automatické šifrování<!-- 1463582 -->
Nastavení v zásadách Windows Information Protection (WIP) teď umožňuje určit, které přípony souborů se při kopírování ze sdílené složky SMB (Server Message Block) v rámci hranic firmy definovaných zásadami WIP mají automaticky šifrovat.

#### <a name="configure-resource-account-settings-for-surface-hubs"></a>Konfigurace nastavení účtu prostředku pro Surface Huby

Můžete teď vzdáleně nakonfigurovat nastavení účtu prostředku pro Surface Huby.

Surface Hub využívá účet prostředku k ověření u Skypu nebo Exchange, aby bylo možné se připojit ke schůzce.
Můžete vytvořit jedinečný účet prostředku, aby se Surface Hub mohl zobrazit ve schůzce jako konferenční místnost.
Účet prostředku se například může zobrazit jako **Konferenční místnost B41/6233**.

> [!NOTE]
> - Pokud pole ponecháte prázdná, přepíšete dříve nakonfigurované atributy na zařízení.
>
> - Vlastnosti účtu prostředku se můžou na Surface Hubu dynamicky měnit. Jedná se například o případ zapnutí rotace hesla. Proto je možné, že bude chvíli trvat, než se realita na zařízení promítne u hodnot v konzole Azure.
>
>   Pokud chcete zjistit, co je aktuálně nakonfigurováno na Surface Hubu, můžete zahrnout informace o účtu prostředku do inventáře hardwaru (který už má sedmidenní interval) nebo jako vlastnosti jen pro čtení. Z důvodu vyšší přesnosti po provedení vzdálené akce můžete získat stav parametrů ihned po spuštění akce aktualizace účtu nebo parametrů na Surface Hubu.

##### <a name="attack-surface-reduction"></a>Omezení možností útoku

|Název nastavení  |Možnosti nastavení  |Popis  |
|---------|---------|---------|
|Execution of password-protected executable content from email (Spuštění spustitelného obsahu chráněného heslem z e-mailu)|Blokovat, Audit, Nenakonfigurováno|Umožňuje zabránit spuštění spustitelných souborů chráněných heslem, které se stáhly prostřednictvím e-mailu.|
|Advanced ransomware protection (Rozšířená ochrana před ransonwarem)|Povoleno, Audit, Nenakonfigurováno|Umožňuje použít agresivní ochranu před ransomwarem.|
|Flag credential stealing from the Windows local security authority subsystem (Označit příznakem použití jiných přihlašovacích údajů ze subsystému Windows Local Security Authority)|Povoleno, Audit, Nenakonfigurováno|Umožňuje označit příznakem použití jiných přihlašovacích údajů ze subsystému Windows Local Security Authority (lsass.exe).|
|Process creation from PSExec and WMI commands (Vytvoření procesů z příkazů PSExec a WMI)|Blokovat, Audit, Nenakonfigurováno|Umožňuje zablokovat vytváření procesů pocházejících z příkazů PSExec a WMI.|
|Untrusted and unsigned processes that run from USB (Nedůvěryhodné a nepodepsané procesy spouštěné z USB)|Blokovat, Audit, Nenakonfigurováno|Umožňuje zablokovat nedůvěryhodné a nepodepsané procesy, které se spouští z USB.|
|Spustitelné soubory, které nesplňují kritéria prevalence, stáří nebo seznamu důvěryhodných souborů|Blokovat, Audit, Nenakonfigurováno|Umožňuje zablokovat spuštění spustitelných souborů, dokud nesplní kritéria prevalence, stáří nebo seznamu důvěryhodných položek.|

##### <a name="controlled-folder-access"></a>Řízený přístup ke složkám

|              Název nastavení               |                                                              Možnosti nastavení                                                              | Popis |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| Ochrana složek (již implementováno) | Nenakonfigurováno, Povolit, Pouze audit (již implementováno)<br><br> <strong>Nová</strong><br>Block disk modification (Blokovat změny disku), Audit disk modification (Auditovat změny disku) |             |

Umožňuje chránit soubory a složky před neautorizovanými změnami od neznámých aplikací.<br><br>**Povolit**: Brání nedůvěryhodným aplikacím ve změnách nebo odstranění souborů v chráněných složkách a v zápisu do sektorů disku.<br><br>
**Block disk modification only** (Blokovat jenom změny disku):<br>Umožňuje zablokovat nedůvěryhodným aplikacím možnost zapisovat do sektorů disku. Nedůvěryhodné aplikace stále můžou změnit nebo odstranit soubory v chráněných složkách.|

#### <a name="additions-to-system-security-settings-for-windows-10-and-later-compliance-policies--1704133--"></a>Přidání nastavení zabezpečení systému pro zásady dodržování předpisů pro Windows 10 a novější<!--1704133-->

Teď jsou dostupná další nastavení dodržování předpisů pro Windows 10, včetně vyžadování brány firewall a Antivirové ochrany v programu Windows Defender.

### <a name="intune-apps"></a>Aplikace Intune

#### <a name="support-for-offline-apps-from-the-microsoft-store-for-business--1222672--"></a>Podpora pro offline aplikace z Microsoft Store pro firmy<!--1222672-->
Aplikace Offline zakoupené v Microsoft Storu pro firmy se teď synchronizují na portálu Azure Portal. Tyto aplikace můžete nasadit pro skupiny zařízení nebo skupiny uživatelů. Offline aplikace instaluje Intune, nikoli Store.

#### <a name="prevent-end-users-from-manually-adding-or-removing-accounts-in-the-work-profile---1728700---"></a>Zabránit koncovým uživatelům v ručním přidávání a odebírání účtů v pracovním profilu<!-- 1728700 -->

Když nasadíte aplikaci Gmail do profilu Android for Work, můžete teď zabránit tomu, aby koncoví uživatelé ručně přidávali nebo odebírali účty v pracovním profilu s použitím nastavení **Přidat nebo odebrat účty** v profilu omezení pro zařízení s Androidem for Work.

<!-- ########################## -->
## <a name="january-2018"></a>Leden 2018

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="alerts-for-expired-tokens-and-tokens-that-will-soon-expire---1639263---"></a>Výstrahy na tokeny a tokeny, jejichž platnost brzy vyprší<!-- 1639263 -->
Na stránce s přehledem se nyní zobrazují upozornění na tokeny, jejichž platnost vypršela nebo brzy vyprší. Když kliknete na upozornění pro jeden token, přejdete na stránku s podrobnostmi o daném tokenu.  Když kliknete na upozornění s více tokeny, přejdete na seznam všech tokenů s jejich stavem. Správci by měli tokeny obnovovat před datem vypršení jejich platnosti.

### <a name="device-management"></a>Správa zařízení

#### <a name="remote-erase-command-support-for-macos-devices---1438084---"></a>Podpora vzdáleného příkazu Erase pro zařízení macOS<!-- 1438084 -->

Správci můžou vydat příkaz pro vzdálené vymazání zařízení s macOS.

> [!IMPORTANT]
> Příkaz erase nejde vrátit zpět a měl by se používat opatrně.

Příkaz pro vymazání odebere ze zařízení všechna data včetně operačního systému. Zároveň se tím dané zařízení odebere ze správy v Intune. Uživateli se nezobrazí žádné upozornění a mazání začne okamžitě po spuštění příkazu.

Je nutné nakonfigurovat 6místný PIN kód pro obnovení. Tento PIN kód lze použít k odemknutí vymazaného zařízení, po kterém se zahájí opětovná instalace operačního systému. Po zahájení mazání se PIN kód zobrazí ve stavovém řádku v okně s přehledem zařízení v Intune. PIN kód zůstane zobrazený, dokud probíhá mazání. Po dokončení mazání zařízení úplně zmizí ze správy Intune. Nezapomeňte si PIN kód pro obnovení poznamenat, aby se dal v případě potřeby použít k obnovení zařízení.

#### <a name="revoke-licenses-for-an-ios-volume-purchasing-program-token---820870---"></a>Odvolání licencí pro token Volume purchase program pro iOS<!-- 820870 -->
Pro daný token VPP můžete odvolat licenci všech aplikací pro iOS koupených přes Volume Purchase Program (VPP).

### <a name="app-management"></a>Správa aplikací

#### <a name="revoking-ios-volume-purchase-program-apps----820863---"></a>Odvolávání aplikací pro iOS Volume purchase program <!-- 820863 -->
Pro dané zařízení, které má jednu nebo více aplikací pro iOS koupených přes Volume Purchase Program (VPP), můžete odvolat licenci aplikace přidruženou na základě zařízení. Odvoláním licence aplikace se příslušná aplikace VPP neodinstaluje ze zařízení. Pokud chcete odinstalovat aplikaci VPP, musíte nastavit akci přiřazení na **Odinstalovat**. Další informace najdete v tématu [Správa aplikací pro systém iOS nakoupených prostřednictvím programu hromadného nákupu pomocí Microsoft Intune](../apps/vpp-apps-ios.md).

#### <a name="assign-office-365-mobile-apps-to-ios-and-android-devices-using-built-in-app-type---1332318---"></a>Přiřazení mobilních aplikací Office 365 k zařízením s iOS a Androidem pomocí integrovaného typu aplikace<!-- 1332318 -->
**Integrovaný** typ aplikace usnadňuje vytvoření aplikací Office 365 a jejich přiřazení k zařízením s iOSem a Androidem, která spravujete. Mezi tyto aplikace O365 se řadí například Word, Excel, PowerPoint a OneDrive. K typu aplikace můžete přiřadit konkrétní aplikace a pak upravit konfiguraci informací o aplikaci.

#### <a name="including-and-excluding-app-assignment-based-on-groups---1406920---"></a>Zahrnutí a vyloučení přiřazení aplikací na základě skupin<!-- 1406920 -->

Během přiřazování aplikací a po výběru typu přiřazení můžete vybrat skupiny, které se mají zahrnout, a také skupiny, které se mají vyloučit.

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="you-can-assign-an-application-configuration-policy-to-groups-by-including-and-excluding-assignments----1480316---"></a>Zásady konfigurace aplikací můžete přiřadit skupinám tak, že zahrnete a vyjmete jejich přiřazení. <!-- 1480316 -->

Zásady konfigurace aplikace můžete přiřadit skupině uživatelů a zařízení s použitím kombinace zahrnutí a vyloučení přiřazení. Je možné zvolit přiřazení ve formě vlastního výběru skupin nebo virtuální skupiny. Virtuální skupina může zahrnovat možnosti **Všichni uživatelé**, **Všechna zařízení** nebo **Všichni uživatelé a všechna zařízení**.

#### <a name="support-for-windows-10-edition-upgrade-policy-----903672archived-1119689---"></a>Podpora pro zásady upgradu edice Windows 10  <!-- 903672(archived), 1119689 -->  
Můžete vytvořit zásady upgradu edice Windows 10, které zařízení s Windows 10 upgradují na Windows 10 Education, Windows 10 Education N, Windows 10 Professional, Windows 10 Professional N, Windows 10 Professional Education a Windows 10 Professional Education N. Podrobnosti o upgradech edicí Windows 10 najdete v článku [Jak nakonfigurovat upgrady edicí Windows 10](../configuration/edition-upgrade-configure-windows-10.md).

#### <a name="conditional-access-policies-for-intune-is-only-available-from-the-azure-portal----1737088-1634311---"></a>Zásady podmíněného přístupu pro Intune jsou dostupné jenom z Azure Portal <!-- 1737088 1634311 -->

Od této verze je možné zásady podmíněného přístupu konfigurovat a spravovat jenom na portálu [Azure Portal](https://portal.azure.com) v části **Azure Active Directory** > **Podmíněný přístup**. Na toto okno se také pohodlně dostanete z Intune na portálu Azure Portal přes **Intune** > **Podmíněný přístup**.

#### <a name="updates-to-compliance-emails--1637547---"></a>Aktualizace e-mailů dodržování předpisů<!--1637547 -->

E-mail, ve kterém se odesílá hlášení o zařízení nesplňujícím požadavky, obsahuje podrobnosti o tomto zařízení.

### <a name="intune-apps"></a>Aplikace Intune

#### <a name="new-functionality-for-the-resolve-action-for-android-devices--1583480--"></a>Nová funkce pro akci vyřešit pro zařízení s Androidem<!--1583480-->

Aplikace Portál společnosti pro Android rozšiřuje akci Vyřešit pro možnost **Aktualizovat nastavení zařízení** tak, aby bylo možné řešit [problémy se šifrováním zařízení](../user-help/encrypt-your-device-android.md).

#### <a name="remote-lock-available-in-company-portal-app-for-windows-10--676506--"></a>Vzdálené uzamčení dostupné v aplikaci Portál společnosti pro Windows 10<!--676506-->
Koncoví uživatelé teď můžou vzdáleně uzamknout svoje zařízení z aplikace Portál společnosti pro Windows 10. To se nezobrazí pro místní zařízení, které aktivně používají.

#### <a name="easier-resolution-of-compliance-issues-for-the-company-portal-app-for-windows-10--676546--"></a>Jednodušší řešení potíží s dodržováním předpisů pro Portál společnosti aplikaci pro Windows 10<!--676546-->
Koncoví uživatelé, kteří používají zařízení s Windows, budou moct v aplikaci Portál společnosti klepnout na důvod nedodržení předpisů. Pokud to bude možné, přejdou tímto klepnutím přímo do správného umístění v aplikaci Nastavení, aby mohli problém vyřešit.

<!-- ########################## -->
## <a name="december-2017"></a>Prosinec 2017

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="new-automatic-redeployment-setting---1469168---"></a>Nové nastavení automatického opětovného nasazení<!-- 1469168 -->
Nastavení **Automatické opětovné nasazení** umožňuje uživatelům s právy správce odstranit všechna uživatelská data a nastavení pomocí klávesové zkratky **CTRL+Win+R** na zamykací obrazovce zařízení. Zařízení se automaticky překonfiguruje a znovu zaregistruje ke správě. Toto nastavení najdete v části Windows 10 > Omezení zařízení > Obecné > Automatické opětovné nasazení. Podrobnosti popisuje článek [Nastavení omezení pro zařízení s Windows 10 v Intune](../configuration/device-restrictions-windows-10.md#general).

#### <a name="support-for-additional-source-editions-in-the-windows-10-edition-upgrade-policy----903672--1119689---"></a>Podpora pro další zdrojové edice v zásadách upgradu edice Windows 10 <!-- 903672,  1119689 -->
Zásady upgradu edice Windows 10 teď můžete použít k upgradu z dalších edic Windows 10 (Windows 10 Pro, Windows 10 Pro Education, Windows 10 Cloud atd.). Před touto verzí bylo podporováno méně cest upgradu. Podrobné informace najdete v článku o [konfiguraci upgradů edice Windows 10](../configuration/edition-upgrade-configure-windows-10.md).

#### <a name="new-windows-defender-security-center-wdsc-device-configuration-profile-settings---1335507---"></a>Nové nastavení profilu konfigurace zařízení Security Center Windows Defenderu (WDSC)<!-- 1335507 -->

Intune přidá nový oddíl nastavení profilu konfigurace zařízení v části Endpoint Protection s názvem **Centrum zabezpečení v programu Windows Defender**. Správci IT mohou nakonfigurovat, ke kterým pilířům aplikace Centrum zabezpečení v programu Windows Defender mají koncoví uživatelé přístup. Pokud správce IT skryje pilíř v aplikaci Centrum zabezpečení v programu Windows Defender, nezobrazují se v zařízení uživatele žádná oznámení související s skrytým pilířem.

Toto jsou pilíře, které mohou správci skrýt z nastavení profilu konfigurace zařízení v aplikaci Centrum zabezpečení v programu Windows Defender:
- Ochrana proti virům a ohrožením
- Výkon a stav zařízení
- Ochrana brány firewall a sítě
- Aplikace a ovládací prvek Prohlížeč
- Možnosti pro rodinu

Správci IT mohou také přizpůsobit výběr oznámení, která budou uživatelé dostávat. Můžete například nakonfigurovat, jestli uživatelé dostanou všechna oznámení vygenerovaná viditelnými pilíři WDSC nebo pouze závažná oznámení. Nezávažná oznámení zahrnují pravidelné přehledy aktivity nástroje Antivirová ochrana v programu Windows Defender a oznámení o času dokončení kontroly. Všechna další oznámení se považují za závažná. Kromě toho můžete také upravit samotný obsah oznámení. Například můžete přidat kontaktní informace oddělení IT, která se vloží do oznámení publikovaných v zařízeních uživatelů.

#### <a name="multiple-connector-support-for-scep-and-pfx-certificate-handling---1361755---"></a>Podpora více konektorů pro zpracování certifikátů SCEP a PFX<!-- 1361755 -->

Zákazníci, kteří k doručení certifikátů do zařízení používají místní konektor NDES, teď můžou v jednom tenantovi nakonfigurovat více konektorů.

Tato nová funkce podporuje následující scénář:

- **Vysoká dostupnost**

Každý konektor NDES si vyžádá žádosti o certifikát z Intune.  Pokud jeden konektor NDES přejde do offline režimu, může další konektor dál zpracovávat žádosti.

#### <a name="customer-subject-name-can-use-aad_device_id-variable----1468599---"></a>Název subjektu zákazníka může použít AAD_DEVICE_ID proměnnou. <!-- 1468599 -->

Když v Intune vytvoříte profil certifikátu SCEP, můžete k vytvoření vlastního názvu subjektu použít proměnnou AAD_DEVICE_ID.   Pokud k vyžádání certifikátu použijete tento profil SCEP, nahradí se proměnná identifikátorem zařízení AAD, které požádalo o certifikát.


### <a name="device-management"></a>Správa zařízení

#### <a name="manage-jamf-enrolled-macos-devices-with-intunes-device-compliance-engine---1592747---"></a>Správa zařízení macOS zaregistrovaných v Jamf s modulem dodržování předpisů pro zařízení v Intune<!-- 1592747 -->
K odeslání informací o stavu zařízení s macOS do Intune teď můžete použít i řešení Jamf, které je vyhodnotí na základě zásad dodržování předpisů definovaných v konzole Intune. V závislosti na stavu dodržování předpisů zařízením a dalších podmínkách (například umístění, riziko pro uživatele atd.) bude podmíněný přístup vymáhat dodržování předpisů pro zařízení macOS s přístupem k cloudovým a místním aplikacím připojeným k Azure AD, včetně Office 365. Další informace o [nastavení integrace řešení Jamf](../protect/conditional-access-integrate-jamf.md) a [dodržování předpisů u zařízení spravovaných v řešení Jamf](../protect/conditional-access-assign-jamf.md).

#### <a name="new-ios-device-action-----1424701---"></a>Nová akce zařízení s iOS  <!-- 1424701 -->

Kontrolovaná zařízení s iOSem 10.3 teď můžete vypnout. Tato akce vypne zařízení okamžitě, bez upozornění pro koncového uživatele. Akci **Vypnout (jen pod dohledem)** najdete ve vlastnostech zařízení, když zařízení vyberete v úloze **Zařízení**.

#### <a name="disallow-datetime-changes-to-samsung-knox-devices---1468103---"></a>Zakázat změny data a času u zařízení se zabezpečením Samsung KNOX<!-- 1468103 -->

Přidali jsme novou funkci, která v zařízeních se zabezpečením Samsung Knox umožňuje zablokovat změnu změny data a času. Najdete je zde: **Profily konfigurace zařízení** > **Omezení zařízení (Android)**  > **Obecné**.

#### <a name="surface-hub-resource-account-supported---1566442----"></a>Surface Hub podporovaný účet prostředku<!-- 1566442  -->

Přidali jsme novou akci zařízení, která správcům pomůže definovat a aktualizovat účet zdroje přidružený k Surface Hubu.

Surface Hub využívá účet zdroje k ověření přes Skype nebo Exchange, aby bylo možné se připojit ke schůzce. Můžete vytvořit jedinečný účet zdroje, takže se Surface Hub zobrazí ve schůzce jako konferenční místnost. Účet zdroje se například může zobrazit jako *Konferenční místnost B41/6233*. Účet zdroje (známý také jako účet zařízení) pro Surface Hub je obvykle potřeba nakonfigurovat pro umístění konferenční místnosti a v případě, kdy je nutné změnit další parametry účtu zdroje.

Pokud chtějí správci aktualizovat účet zdroje v zařízení, musí zadat aktuální přihlašovací údaje služby Active Directory nebo Azure Active Directory přidružené k tomuto zařízení. Pokud je na zařízení aktivní rotace hesla, musí správce přejít do Azure Active Directory a heslo najít.

> [!NOTE]
> Všechna pole se odešlou ve skupině a přepíšou všechna dříve nakonfigurovaná pole. Také prázdná pole mohou přepsat existující pole.

Správci mohou nakonfigurovat následující nastavení:

- **Účet zdroje**
  - **Uživatel služby Active Directory**

    Název_domény\uživatelské_jméno nebo hlavní název uživatele (UPN): user@domainname.com

  - **Heslo**

- **Volitelné parametry účtu zdroje** (musí se nastavit pomocí daného účtu zdroje)

  - **Interval rotace hesla**

    Zajišťuje, že Surface Hub automaticky aktualizuje heslo k účtu každý týden z bezpečnostních důvodů. Pokud chcete nakonfigurovat jakékoli parametry po zapnutí této možnosti, musíte nejprve resetovat heslo k účtu ve službě Azure Active Directory.

  - **Adresa SIP (Session Initiation Protocol)**

    Používá se pouze v případě nezdařeného automatického zjišťování.

  - **E-mail**

    E-mailová adresu účtu zdroje nebo zařízení.

  - **Server Exchange**

    Je potřeba, pouze pokud se nezdaří automatické zjišťování.

  - **Synchronizace kalendáře**

    Určuje, zda je povolená synchronizace kalendáře a dalších služeb serveru Exchange. Například: synchronizace schůzek.

#### <a name="install-office-apps-on-macos-devices---1494311---"></a>Instalace aplikací Office na zařízení macOS<!-- 1494311 -->
Teď můžete na zařízení macOS instalovat aplikace Office. Tento nový typ aplikace vám umožní nainstalovat Word, Excel, PowerPoint, Outlook a OneNote. Tyto aplikace jsou také dodávané prostřednictvím funkce Microsoft AutoUpdate (MAU). Je to kvůli jejich zabezpečení a aktuálnosti.

### <a name="app-management"></a>Správa aplikací

#### <a name="delete-an-ios--volume-purchasing-program-token---820879---"></a>Odstranění tokenu programu Volume purchase program pro iOS<!-- 820879 -->
K odstranění tokenu programu Volume Purchasing Program (VPP) pro iOS můžete použít konzolu. To může být nutné v případě, že máte duplicitní instance tokenu VPP.

### <a name="intune-apps"></a>Aplikace Intune


### <a name="role-based-access-control"></a>Řízení přístupu na základě role

#### <a name="a-new-entity-collection-named-current-user-is-limited-to-currently-active-user-data---1667026---"></a>Nová kolekce entit s názvem aktuální uživatel je omezena na aktuálně aktivní uživatelská data.<!-- 1667026 -->

Kolekce entit **Uživatelé** obsahuje všechny uživatele Azure Active Directory (Azure AD), kteří mají v podniku přiřazené licence. Uživatel například může být přidaný do Intune a potom v průběhu posledního měsíce dojde k jeho odebrání. Přestože tento uživatel není v době vytvoření sestavy přítomen, existují data o uživateli a stavu. Můžete vytvořit sestavu, která ukazuje trvání historické přítomnosti uživatele ve vašich datech.

Naproti tomu nová kolekce entit **Aktuální uživatel** obsahuje pouze uživatele, kteří nebyli odebráni. Kolekce entit **Aktuální uživatel** obsahuje pouze aktuálně aktivní uživatele. Informace o kolekci entit **Aktuální uživatel** najdete v části [Referenční informace o entitě aktuálního uživatele](../developer/reports-ref-data-model.md).

### <a name="updated-graph-apis---1736360---"></a>Aktualizovaná rozhraní API grafu<!-- 1736360 -->

V této verzi jsme aktualizovali několik rozhraní API služby Graph pro Intune. V této chvíli se jedná o beta verze. Další informace najdete v měsíčním [protokolu změn rozhraní API služby Graph](https://developer.microsoft.com/graph/docs/concepts/changelog).

### <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

#### <a name="intune-supports-windows-information-protection-wip-denied-apps---1479103---"></a>Intune podporuje aplikace Windows Information Protection (NV) – odepřené.<!-- 1479103 -->
V Intune můžete zadat odepřené aplikace. Pokud je aplikace zakázaná, má zablokovaný přístup k podnikovým informacím. Je to v podstatě opak seznamu povolených aplikací. Další informace najdete v [doporučeném seznamu aplikací se zákazem pro Windows Information Protection](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp?f=255&MSPPError=-2147217396#recommended-deny-list-for-windows-information-protection).

<!-- ########################## -->
## <a name="november-2017"></a>Listopad 2017

### <a name="troubleshoot-enrollment-issues----746324---"></a>Řešení potíží s registrací <!-- 746324 -->

Pracovní prostor **Řešení potíží** teď zobrazuje problémy s registrací uživatelů. Podrobnosti o problému a navrhované nápravné kroky můžou správcům a pracovníkům technické podpory pomoct problém vyřešit. Některé problémy s registrací nejsou zaznamenané a k některým chybám nemusí návrhy k odstranění problému existovat.

### <a name="group-assigned-enrollment-restrictions---747598---"></a>Omezení registrace přiřazených skupině<!-- 747598 -->

Jako správce Intune teď můžete [vytvořit vlastní omezení registrace typů a limitu počtu zařízení u skupin uživatelů](../enrollment/enrollment-restrictions-set.md).

Intune Azure Portal vám umožňuje vytvořit až 25 instancí každého typu omezení, které pak můžete přiřadit ke skupinám uživatelů. Omezení přiřazená ke skupinám přepíší výchozí omezení.

Všechny instance typů omezení se budou uchovávat v seznamu se striktním pořadím. Toto pořadí definuje hodnotu priority pro případ řešení konfliktů. U uživatele, na něhož se vztahuje více instancí omezení, se uplatní jenom instance s nejvyšší prioritou. Prioritu dané instance můžete změnit tak, že ji přetáhnete na jiné místo v seznamu.

Tato funkce bude vydána spolu s migrací nastavení Androidu for Work z nabídky registrace Androidu for Work do nabídky Omezení registrace. Tato migrace může trvat několik dnů, a proto je možné, že v rámci listopadové verze se nejprve upgradují jiné části vašeho účtu a teprve poté se u omezení registrace povolí přiřazení skupin.

### <a name="support-for-multiple-network-device-enrollment-service-ndes-connectors---1528104---"></a>Podpora více konektorů služby zápisu síťových zařízení (NDES)<!-- 1528104 -->

Služba zápisu síťových zařízení umožňuje, aby mobilní zařízení spuštěná bez doménových přihlašovacích údajů získala certifikáty založené na protokolu SCEP (Simple Certificate Enrollment Protocol).
Od této aktualizace se podporuje více konektorů NDES.

### <a name="manage-android-for-work-devices-independently-from-android-devices---1490731-eeready--"></a>Správa zařízení s Androidem for Work nezávisle na zařízeních s Androidem<!-- 1490731 EEready-->

Intune podporuje správu registrace zařízení s Androidem for Work odděleně od platformy Android. Tato nastavení se spravují v části **Registrace zařízení** > **Omezení registrace** > **Omezení typů zařízení**. (Dříve se nacházela v části **Registrace zařízení** > **Registrace Androidu for Work** > **Nastavení registrace Android for Work**.)

Ve výchozím nastavení jsou nastavení zařízení s Androidem for Work stejná jako nastavení zařízení s Androidem. Po změně nastavení Androidu for Work tomu už tak nebude.

Pokud zablokujete registraci Androidu for Work u osobních zařízení, budou se jako Android for Work moct zaregistrovat jenom firemní zařízení s Androidem.

Při práci s těmito novými nastaveními vezměte v úvahu tyto informace:

#### <a name="if-you-have-never-previously-onboarded-android-for-work-enrollment"></a>Pokud jste ještě nikdy nepoužili registraci Androidu for Work

Nová platforma Android for Work je ve výchozím nastavení omezení typů zařízení zablokovaná. Jakmile začnete funkci používat, můžete zařízením povolit, aby se zaregistrovala v Androidu for Work. Uděláte to tak, že změníte výchozí omezení typu zařízení nebo vytvoříte nové, které bude mít přednost před výchozím omezením.

#### <a name="if-you-have-onboarded-android-for-work-enrollment"></a>Pokud jste už registraci Androidu for Work použili

Pokud jste se už dřív připojili, záleží na nastavení, které jste zvolili:

| Nastavení | Stav Androidu for Work ve výchozím omezení typu zařízení | Poznámky |
| --- | --- | --- |
| **Spravovat všechna zařízení jako Android for Work** | Blokováno | Všechna zařízení s Androidem se musí zaregistrovat bez Androidu for Work. |
| **Spravovat podporovaná zařízení jako Android for Work** | Povoleno | Všechna zařízení s Androidem, která podporují Android for Work, se musí zaregistrovat s Androidem for Work. |
| **Spravovat podporovaná zařízení pro uživatele v těchto skupinách jako Android for Work** | Blokováno | Vytvořila se samostatná zásada omezení typu zařízení, která přepíše výchozí zásadu. Tato zásada definuje skupiny, které jste dříve vybrali a povolili jim registraci Androidu for Work. Uživatelé ve vybraných skupinách budou moct dál zaregistrovat svoje zařízení s Androidem for Work. Žádní jiní uživatelé se v Androidu for Work nebudou moct zaregistrovat. |

Ve všech případech se vaše zamýšlená regulace zachová. K tomu, aby se zachovala možnost globálního používání Androidu for Work ve vašem prostředí nebo možnost používání této platformy konkrétními skupinami, nevyžadujeme z vaší strany žádnou akci.

### <a name="google-play-protect-support-on-android---908720---"></a>Google Play chránit podporu pro Android<!-- 908720 -->

S vydáním verze Android Oreo zavádí Google sadu bezpečnostních funkcí s názvem Google Play Protect, které uživatelům a organizacím umožňují provozovat zabezpečené aplikace a zabezpečené image Androidu. Intune teď podporuje funkce Google Play Protect, a to včetně vzdáleného ověření SafetyNet. Správci můžou nastavit požadavky na zásady dodržování předpisů, které vyžadují, aby funkce Google Play Protect byla nakonfigurovaná a funkční.
Nastavení **Ověření zařízení SafetyNet** vyžaduje, aby se zařízení připojilo ke službě Googlu, která ověří, že je zařízení v pořádku a není ohrožené. Správci můžou rovněž nastavením konfiguračního profilu pro Android for Work vyžádat, aby nainstalované aplikace byly ověřeny pomocí služeb Google Play. Pokud zařízení nedodržuje předpisy Google Play chránit požadavky, může podmíněný přístup zablokovat uživatelům přístup k podnikovým prostředkům.

- Přečtěte si, [jak vytvořit zásadu dodržování předpisů zařízeními pro službu Google Play Protect](../protect/compliance-policy-create-android.md).

### <a name="text-protocol-allowed-from-managed-apps---1414050----"></a>Povolený textový protokol ze spravovaných aplikací<!-- 1414050  -->

Aplikace spravované prostřednictvím sady Intune App SDK můžou posílat SMS zprávy.


### <a name="app-install-report-updated-to-include-install-pending-status---1249446---"></a>Sestava instalace aplikace se aktualizovala tak, aby obsahovala stav čeká na instalaci.<!-- 1249446 -->  

Sestava **Stav instalace aplikace** dostupná pro každou aplikaci v seznamu **Aplikace** v úloze **Klientské aplikace** teď obsahuje počet **čekajících instalací** uživatelů a zařízení.

### <a name="ios-11-app-inventory-api-for-mobile-threat-detection---1391759---"></a>rozhraní API inventáře aplikace iOS 11 pro detekci mobilních hrozeb<!-- 1391759 -->

Intune shromažďuje informace o inventáři aplikací ze zařízení jak v osobním, tak i firemním vlastnictví, a zpřístupňuje je zprostředkovatelům služby ochrany před mobilními hrozbami, jako je třeba aplikace Lookout for Work. Inventář aplikací můžete shromažďovat od uživatelů zařízení s iOSem 11 a novějším.

**Inventář aplikací**  
Inventáře ze zařízení s iOSem 11 a novějším v osobním i firemním vlastnictví se posílají zprostředkovateli služby ochrany před mobilními hrozbami. Data v inventáři aplikací zahrnují tyto údaje:

- ID aplikace
- Verze aplikace
- Krátká verze aplikace
- Název aplikace
- Velikost sady prostředků aplikace
- Dynamická velikost aplikace
- Zda je aplikace ověřena nebo ne
- Zda je aplikace spravována nebo ne

### <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone---1463747-wnready---"></a>Migrace hybridních zařízení a uživatelů správy mobilních zařízení (MDM) do samostatného řešení Intune<!-- 1463747 wnready -->
Pro přesun uživatelů a jejich zařízení z hybridní správy MDM do Intune na Azure Portalu jsou dostupné nové procesy a nástroje, které vám umožní:
- Kopírovat zásady a profily z konzoly Configuration Manageru do Intune na portálu Azure Portal
- Přesunout podmnožinu uživatelů do Intune na portálu Azure Portal a zbytek nechat v hybridním MDM
- Migrovat zařízení do Intune na portálu Azure Portal, aniž by bylo nutné je znovu zaregistrovat

### <a name="on-premises-exchange-connector-high-availability-support----676614---"></a>Podpora vysoké dostupnosti místního konektoru Exchange <!-- 676614 -->
Když Exchange Connector vytvoří připojení k Exchangi pomocí zadaného serveru Client Access Server (CAS), konektor teď má možnost zjišťovat další servery CAS. Pokud primární server CAS přestane být dostupný, při selhání převezme služby konektoru jiný server CAS (pokud je k dispozici), dokud primární server CAS nebude znovu dostupný. Podrobnosti najdete v článku [Podpora vysoké dostupnosti místního konektoru Exchange](../protect/exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support).

### <a name="remotely-restart-ios-device-supervised-only---1424595---"></a>Vzdáleně restartovat zařízení s iOS (jenom pod dohledem)<!-- 1424595 -->

Pomocí akce zařízení můžete teď aktivovat restartování zařízení s iOSem 10.3 a novějším, které je v režimu pod dohledem. Další informace o použití akce restartování zařízení najdete v tématu [Vzdálené restartování zařízení přes Intune](../remote-actions/device-restart.md).

> [!Note]
> Tento příkaz vyžaduje, aby byla zařízení v režimu pod dohledem, a přístupová práva k **zámku zařízení**. Zařízení se restartuje okamžitě. Zařízení s iOSem zamčená pomocí hesla se po restartování k síti Wi-Fi znovu nepřipojí a je možné, že po restartování nebudou moct komunikovat se serverem.

### <a name="single-sign-on-support-for-ios---1333645---"></a>Podpora jednotného přihlašování pro iOS<!-- 1333645 -->  

Pro uživatele iOSu můžete využít jednotné přihlašování. Díky této aktualizaci konfigurace datové části fungují aplikace pro iOS, které jsou naprogramovány tak, aby v datové části jednotného přihlašování hledaly přihlašovací údaje uživatele. Ke konfiguraci hlavního názvu a sféry můžete použít také hlavní název uživatele (UPN) a ID zařízení v Intune. Podrobnosti najdete v článku [Nakonfigurování Intune na jednotné přihlašování pro zařízení s iOSem](../configuration/ios-device-features-settings.md#single-sign-on).

### <a name="add-find-my-iphone-for-personal-devices--1427287--"></a>Přidat "Najít iPhone" pro osobní zařízení<!--1427287-->
Teď můžete zobrazit, jestli je u zařízení s iOSem zapnutý zámek aktivace. Tato funkce se dříve nacházela v Intune na portálu Classic.

### <a name="remotely-lock-managed-macos-device-with-intune---1437691---"></a>Vzdálené uzamčení spravovaných zařízení macOS pomocí Intune<!-- 1437691 -->

Ztracené zařízení s macOS můžete zamknout a nastavit pro ně 6místný číselný kód PIN pro obnovení. Když se zařízení zamkne, v okně **přehledu zařízení** se bude zobrazovat kód PIN, dokud se nepošle jiná akce zařízení.

Další informace si můžete přečíst v článku [Vzdálené uzamčení spravovaných zařízení přes Intune](../remote-actions/device-remote-lock.md).

### <a name="new-scep-profile-details-supported---1559808---"></a>Jsou podporovány nové podrobnosti profilu SCEP<!-- 1559808 -->

Při vytváření profilu SCEP na platformách Windows, iOS, macOS a Android teď správci můžou nakonfigurovat další nastavení.  Správci můžou nastavit IMEI, sériové číslo nebo běžný název včetně e-mailu ve formátu názvu subjektu.

<!-- #### Update to what device details your company may see -1616825
The Company Portal app for Android can now use geofencing to protect access to company resources. It uses network details such as IP address, default gateway address, and Domain Name System (DNS) to determine whether to allow access to protected company resources. -->

### <a name="retain-data-during-a-factory-reset---1588489---"></a>Zachovat data při obnovení továrního nastavení <!--1588489 -->
Při obnovení továrního nastavení ve Windows 10 verze 1709 a novější je dostupná nová funkce. Správci můžou určit, jestli se při obnovení továrního nastavení data registrace zařízení a další zřízená data v zařízení zachovají.

Při obnovení továrního nastavení se zachovají následující data:
- Uživatelské účty přidružené k zařízení
- Stav počítače (připojení k doméně, připojení ke službě Azure Active Directory)
- Registrace správy mobilních zařízení
- Aplikace nainstalované výrobcem OEM (aplikace ze Storu a aplikace Win32)
- Profil uživatele
- Uživatelská data mimo profil uživatele
- Automatické přihlášení uživatele

Nezachovají se následující data:
- Soubory uživatele
- Aplikace nainstalované uživatelem (aplikace ze Storu a aplikace Win32)
- Nevýchozí nastavení zařízení


### <a name="window-10-update-ring-assignments-are-displayed---1621837---"></a>Zobrazí se přiřazení aktualizačního kruhu Window 10.<!-- 1621837 -->
Při **řešení potíží** u aktuálně zobrazeného uživatele si můžete zobrazit veškerá přiřazení aktualizačních kanálů Windows 10.  

### <a name="windows-defender-advanced-threat-protection-reporting-frequency-settings----1455974----"></a>Nastavení četnosti vytváření sestav rozšířené ochrany před internetovými útoky v programu Windows Defender <!-- 1455974  -->
Služba Rozšířená ochrana před internetovými útoky v programu Windows Defender umožňuje správcům spravovat četnost hlášení u spravovaných zařízení. Pomocí nové možnosti **Zvýšit četnost hlášení telemetrie** služba Rozšířená ochrana před internetovými útoky v programu Windows Defender častěji shromažďuje a vyhodnocuje rizika. Výchozí nastavení hlášení optimalizuje rychlost a výkon. Zvýšení četnosti hlášení může být velmi cennou pomůckou pro zařízení s vysokým rizikem. Toto nastavení najdete v profilu **Ochrana ATP v programu Windows Defender** v části **Konfigurace zařízení**.

### <a name="audit-updates---1412961---"></a>Aktualizace auditu<!-- 1412961 -->  
Auditování Intune poskytuje záznam o operacích změn souvisejících s Intune.  Všechny operace vytvoření, aktualizace, odstranění a odebrání se zaznamenávají a uchovávají po dobu jednoho roku.  Azure Portal zobrazuje data auditování v každé úloze za posledních 30 dnů, která se dají filtrovat.  Příslušné rozhraní Graph API umožňuje načíst data auditování uložená za poslední rok.

Auditování najdete ve skupině **MONITOROVAT**. Pro každou úlohu existuje položka nabídky **Protokoly auditu**.

### <a name="company-portal-app-for-macos-is-available--1541700--"></a>K dispozici je Portál společnosti aplikace pro macOS.<!--1541700-->
Portál společnosti Intune v systému macOS má aktualizované prostředí, které je optimalizované ke správnému zobrazení všech informací a oznámení o dodržování předpisů, což uživatelé potřebují pro všechna zaregistrovaná zařízení. Po nasazení Portálu společnosti Intune do zařízení v něm začne nástroj Microsoft AutoUpdate pro macOS zajišťovat aktualizace. Nový Portál společnosti Intune pro macOS můžete stáhnout po přihlášení na web Portál společnosti pro macOS ze zařízení macOS.

### <a name="microsoft-planner-is-now-part-of-the-mobile-app-management-mam-list-of-approved-apps----1248473---"></a>Microsoft Planner je teď součástí seznamu schválených aplikací pro správu mobilních aplikací (MAM). <!-- 1248473 -->
Aplikace Microsoft Planner pro iOS a Android je teď součástí schválených aplikací pro správu mobilních aplikací (MAM). Aplikaci lze nakonfigurovat prostřednictvím okna Intune App Protection na portálu Azure Portal pro všechny tenanty.
- Další informace najdete v [seznamu schválených aplikací MAM](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

### <a name="per-app-vpn-requirement-update-frequency-on-ios-devices-----1547061---"></a>Frekvence aktualizace požadavků sítě VPN podle aplikace na zařízeních s iOS  <!-- 1547061 -->  
Správci mohou nyní v aplikacích zařízení s iOSem odebrat požadavky sítě VPN podle aplikace; dotčená zařízení to provedou po jejich dalším vrácení se změnami do Intune, které obvykle probíhá do 15 minut.  

### <a name="support-for-system-center-operations-manager-management-pack-for-exchange-connector---885457---"></a>Podpora System Center Operations Manager Management Pack pro Exchange Connector<!-- 885457 -->
K dispozici je teď System Center Operations Manager Management Pack pro Exchange Connector, které vám pomůžou s analýzou protokolů Exchange Connectoru. Při řešení problémů vám tato funkce poskytuje různé způsoby monitorování služby.

### <a name="co-management-for-windows-10-devices----1243445---"></a>Spoluspráva pro zařízení s Windows 10 <!-- 1243445 -->
Společná správa je řešení, které představuje most mezi tradiční a moderní správou a poskytne vám cestu k přechodu pomocí přístupu ve fázích. V základu je společná správa řešením, kdy jsou zařízení s Windows 10 současně spravovaná pomocí Configuration Manageru a Microsoft Intune a také připojená k Active Directory (AD) a Azure Active Directory (Azure AD).  Tato konfigurace poskytuje cestu, která se modernizovat v průběhu času, podle tempa, které je pro vaši organizaci nejvhodnější, pokud nemůžete přesunout vše najednou.  

### <a name="restrict-windows-enrollment-by-os-version---245498---"></a>Omezení registrace zařízení s Windows podle verze operačního systému<!-- 245498 -->
Jako správce Intune teď můžete pro registrace zařízení zadat minimální a maximální verzi Windows 10. Tato omezení můžete nastavit v okně **Konfigurace platforem**.

Intune dál podporuje registraci telefonů a počítačů s Windows 8.1. S minimální a maximální mezí se ale dají nastavit jenom verze Windows 10. Pokud chcete povolit registraci zařízení s Windows 8.1, nechte minimální mez prázdnou.

### <a name="alerts-for-windows-autopilot-unassigned-devices----1631236---"></a>Výstrahy pro zařízení s nepřiřazeným autopilotem Windows autopilot <!-- 1631236 -->
Na stránce **Microsoft Intune** > **Registrace zařízení** > **Přehled** je k dispozici nové upozornění, které se týká zařízení s nepřiřazeným Windows AutoPilotem. Toto upozornění ukazuje, kolik zařízení z programu AutoPilot nemá přiřazené profily nasazení AutoPilotu. Na základě informací v upozornění můžete vytvořit profily a přiřadit je potřebným zařízením. Když na upozornění kliknete, zobrazí se úplný seznam zařízení Windows AutoPilotu a podrobné informace o zařízeních. Další informace najdete v článku [Registrace zařízení s Windows pomocí programu Windows AutoPilot Deployment](../enrollment/enrollment-autopilot.md).


### <a name="refresh-button-for-devices-list------1333581---"></a>Tlačítko Aktualizovat pro seznam zařízení   <!-- 1333581 -->
Protože se seznam zařízení neaktualizuje automaticky, můžete zařízení, která se v seznamu zobrazují, aktualizovat pomocí nového tlačítka Aktualizovat.

### <a name="support-for-symantec-cloud-certification-authority-ca----1333638---"></a>Podpora certifikační autority (CA) Symantec Cloud <!-- 1333638 -->    
Intune teď podporuje certifikační autoritu Symantec Cloud. To umožňuje, aby Intune Certificate Connector vystavoval zařízením spravovaným přes Intune certifikáty PKCS z certifikační autority Symantec Cloud. Pokud už Intune Certificate Connector používáte s certifikační autoritou Microsoft, můžete existující nastavení Intune Certificate Connectoru použít k přidání podpory pro certifikační autoritu Symantec.

### <a name="new-items-added-to-device-inventory----1404455---"></a>Nové položky přidané do inventáře zařízení  <!--1404455 -->
V [inventáři, který pořizují zaregistrovaná zařízení](../remote-actions/device-inventory.md), jsou teď dostupné následující nové položky:

- Adresa MAC pro Wi-Fi
- Celkové místo v úložišti
- Celkové volné místo
- MEID
- Poskytovatel služeb pro odběratele

### <a name="set-access-for-apps-by-minimum-android-security-patch-on-the-device---1278463---"></a>Nastavení přístupu pro aplikace pomocí minimální opravy zabezpečení Androidu na zařízení<!-- 1278463 -->   
Správce může definovat minimální opravu zabezpečení Androidu, která musí být na zařízení nainstalovaná, aby zařízení pod spravovaným účtem získalo přístup ke spravované aplikaci.

> [!Note]  
> Tato funkce omezuje jenom opravy zabezpečení vydané společností Google na zařízeních s Androidem 6.0 a novějším.

### <a name="app-conditional-launch-support---1193313---"></a>Podpora podmíněného spuštění aplikace<!-- 1193313 -->
Správci IT teď můžou pomocí portálu pro správu Azure nastavit požadavek, aby se prostřednictvím správy mobilních aplikací (MAM) při spouštění aplikace místo číselného kódu PIN vynutilo heslo. Při takové konfiguraci musí uživatel po zobrazení výzvy nastavit a používat heslo, aby získal přístup k aplikacím s podporou MAM. Heslo je definované jako číselný kód PIN s aspoň jedním speciálním znakem nebo velkým/malým písmenem. Tato verze Intune tuto funkci povolí **jenom v iOSu**. Intune podporuje heslo podobným způsobem jako číselný kód PIN, stanovuje minimální délku a povoluje opakování znaků a sekvencí. Tato funkce vyžaduje, aby aplikace (to znamená WXP, Outlook, Managed Browser, Yammer) integrovaly sadu Intune App SDK s kódem této funkce místo vynucení nastavení hesla v cílových aplikacích.

### <a name="app-version-number-for-line-of-business-in-device-install-status-report---1233999---"></a>Číslo verze aplikace pro obchodní zařízení ve zprávě o stavu instalace zařízení<!-- 1233999 -->
Od této verze se ve zprávě o stavu instalace zařízení zobrazí u obchodních aplikací pro iOS a Android číslo verze aplikace. Tyto informace můžete využít k řešení potíží s aplikacemi nebo nalezení zařízení, na kterých běží zastaralé verze aplikací.

### <a name="admins-can-now-configure-the-firewall-settings-on-a-device-using-a-device-configuration-profile---951708---"></a>Správci teď můžou nakonfigurovat nastavení brány firewall na zařízení pomocí profilu konfigurace zařízení.<!-- 951708 -->   
Správci můžou zapnout bránu firewall pro zařízení a také nakonfigurovat různé protokoly pro doménové, privátní a veřejné sítě.  Tato nastavení brány firewall najdete v profilu „Ochrana koncového bodu“.

### <a name="windows-defender-application-guard-helps-protect-devices-from-untrusted-websites-as-defined-by-your-organization---958257---"></a>Ochrana Application Guard v programu Windows Defender pomáhá chránit zařízení před nedůvěryhodnými weby podle definice vaší organizace.<!-- 958257 -->   
Správci můžou definovat weby jako „důvěryhodné“ nebo „podnikové“ pomocí pracovního postupu Windows Information Protection nebo nového profilu „Ohraničení sítě“ v konfiguracích zařízení. Pokud se zobrazují v Microsoft Edge, všechny lokality, které nejsou uvedené 64 na hranici důvěryhodné sítě zařízení s Windows 10, se místo toho otevřou v prohlížeči v rámci virtuálního počítače Hyper-V.

Application Guard najdete v konfiguračních profilech zařízení v profilu „Ochrana koncového bodu“. Tam můžou správci konfigurovat interakce mezi virtualizovaným prohlížečem a hostitelským počítačem, nedůvěryhodné a důvěryhodné weby a ukládání dat vygenerovaných ve virtualizovaném prohlížeči. Pokud chcete Application Guard na zařízení používat, musí se nejdříve nakonfigurovat ohraničení sítě. Je důležité, aby se pro zařízení definovalo jenom jedno ohraničení sítě.  

### <a name="windows-defender-application-control-on-windows-10-enterprise-provides-mode-to-trust-only-authorized-apps---1031096---"></a>Řízení aplikací v programu Windows Defender ve Windows 10 Enterprise poskytuje režim pro důvěřování jenom autorizovaným aplikacím.<!-- 1031096 -->    
Protože každý den vznikají tisíce nových škodlivých souborů, nemusí už boj proti malwaru pomocí antivirové ochrany využívající podpisy souborů poskytovat dostatečnou obranu před novými útoky. Pomocí Řízení aplikací v programu Windows Defender ve Windows 10 Enterprise můžete konfiguraci zařízení změnit z režimu, kdy jsou aplikace důvěryhodné, pokud nejsou blokované antivirovou ochranou nebo jiným řešením zabezpečení, na režim, kdy operační systém důvěřuje jenom aplikacím autorizovaným vaší organizací. Důvěryhodnost se aplikacím přiřazuje v Řízení aplikací v programu Windows Defender.

Pomocí Intune můžete zásady řízení aplikací nakonfigurovat v režimu „pouze audit“ nebo v režimu vynucení. Aplikace nejsou blokované při spuštění v režimu "pouze audit". Režim "jenom audit" protokoluje všechny události v protokolech místních klientů. Můžete také nakonfigurovat, jestli je povolené spouštět jenom součásti Windows a aplikace pro Microsoft Store, nebo jestli se můžou spouštět i další aplikace s dobrou reputací, jak je definuje Intelligent Security Graph.

### <a name="window-defender-exploit-guard-is-a-new-set-of-intrusion-prevention-capabilities-for-windows-10---1063615---"></a>Ochrana před zneužitím v programu Windows Defender je nová sada funkcí prevence neoprávněných vniknutí pro Windows 10.<!-- 1063615 -->   
Ochrana Exploit Guard v programu Windows Defender obsahuje vlastní pravidla pro snížení zneužitelnosti aplikací, brání hrozbám z maker skriptů, automaticky blokuje síťová připojení k IP adresám se špatnou reputací a může zabezpečit data před ransomwarem a neznámými hrozbami. Ochrana Exploit Guard v programu Windows Defender se skládá z těchto součástí:

- **Omezení možností útoku** vám poskytne pravidla, která umožňují zabránit hrozbám v makrech, skriptech a e-mailech.
- **Řízený přístup ke složkám** automaticky blokuje přístup k obsahu chráněných složek.
- **Filtrování sítě** blokuje odchozí připojení z jakékoli aplikace k IP nebo doméně se špatnou reputací.
- **Ochrana Exploit Protection** poskytuje omezení paměti, toku řízení a zásad, která se dají využít k ochraně aplikace před zneužitím.

### <a name="manage-powershell-scripts-in-intune-for-windows-10-devices---790537---"></a>Správa powershellových skriptů v Intune u zařízení s Windows 10<!-- 790537 -->

Rozšíření správy Intune umožňuje nahrát powershellové skripty do Intune, aby je bylo možné spouštět v zařízeních s Windows 10. Toto rozšíření doplňuje funkce správy mobilních zařízení (MDM) s Windows 10 a usnadňuje přechod na moderní správu. Podrobnosti najdete v článku [Správa powershellových skriptů v Intune u zařízení s Windows 10](../apps/intune-management-extension.md).

### <a name="new-device-restriction-settings-for-windows-10--------1308850---"></a>Nová nastavení omezení pro zařízení s Windows 10     <!-- 1308850 -->
- Zasílání zpráv (jenom mobilní) – zakázání testování nebo zpráv MMS
- Heslo – nastavení k povolení standardu FIPS a použití sekundárních zařízení Windows Hello k ověřování 
- Zobrazit – nastavení k zapnutí nebo vypnutí škálování GDI pro starší verze aplikací

### <a name="windows-10-kiosk-mode-device-restrictions---1308872---"></a>Omezení zařízení v celoobrazovkovém režimu Windows 10<!-- 1308872 -->   
Uživatele zařízení s Windows 10 můžete omezit na režim veřejného terminálu, který uživatele omezuje na sadu předdefinovaných aplikací.  To uděláte tak, že vytvoříte profil omezení zařízení s Windows 10 a nastavíte režim Veřejný terminál.

Režim veřejného terminálu podporuje dva režimy: **s jednou aplikací** (umožňuje uživateli spustit jenom jednu aplikaci) nebo **s více aplikacemi** (povoluje přístup k sadě aplikací).  Definujete uživatelský účet a název zařízení a tím se určí podporované aplikace.  Když je uživatel přihlášený, je omezený na definované aplikace.  Další informace najdete v článku [AssignedAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp). 

Režim veřejného terminálu vyžaduje:

- Intune musí být autoritou pro správu mobilních zařízení (MDM).
- Aplikace už musí být v cílovém zařízení nainstalované.
- Zařízení musí být [správně zřízené](https://docs.microsoft.com/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions).

### <a name="new-device-configuration-profile-for-creating-network-boundaries---1311967---"></a>Nový profil konfigurace zařízení pro vytváření hranic sítě<!-- 1311967 -->   
Součástí jiných profilů konfigurace zařízení je nový profil konfigurace zařízení s názvem **Ohraničení sítě**. Tento profil slouží k definování online prostředků, které chcete, aby se považovaly za podnikové a důvěryhodné. Ohraničení sítě pro zařízení musíte definovat *před tím*, než na něm bude možné používat funkce jako ochrana Application Guard v programu Windows Defender a Windows Information Protection. Pro každé zařízení je důležité definovat jenom jednu hranici sítě.

Můžete definovat podnikové cloudové prostředky, rozsahy IP adres a interní proxy servery, které se mají považovat za důvěryhodné. Po definování můžou ohraničení sítě využívat ostatní funkce jako ochrana Application Guard v programu Windows Defender a Windows Information Protection.

### <a name="two-additional-settings-for-windows-defender-antivirus---1338409---"></a>Dvě další nastavení pro antivirovou ochranu v programu Windows Defender<!-- 1338409 -->  
**Úroveň blokování souborů**

| | |
|---|---|
| Nenakonfigurované | Nastavení **Nenakonfigurováno** používá výchozí úroveň blokování Antivirové ochrany v programu Windows Defender a zajišťuje silnou detekci bez zvýšeného rizika detekování legitimních souborů. |
| Vysoký | Nastavení **Vysoká** aplikuje silnou úroveň zjišťování.
| Vysoká +  | Nastavení **Vysoká +** poskytuje vysokou úroveň s dalšími ochrannými opatřeními, která můžou mít vliv na výkon klienta.
| Žádná tolerance  | Nastavení **Žádná tolerance** blokuje všechny neznámé spustitelné soubory. |

I když je to nepravděpodobné, může nastavení **Vysoká** způsobit, že se detekují některé legitimní soubory.
Doporučujeme nastavit úroveň blokování souborů na výchozí hodnotu **Nenakonfigurováno**.

**Prodloužení časového limitu pro kontrolu souborů v cloudu**  

| | |
|--|--|
| Počet sekund (0–50) | Zadejte maximální dobu, po kterou má Antivirová ochrana v programu Windows Defender blokovat soubor při čekání na výsledek z cloudu. Výchozí doba je 10 sekund: dodatečná doba, kterou tady zadáte (až 50 sekund), se k těmto 10 sekundám přičte. Ve většině případů trvá kontrola mnohem kratší dobu než maximální. Prodloužení doby umožňuje, aby cloud podezřelé soubory důkladně prozkoumal. Doporučujeme, abyste toto nastavení povolili a zadali aspoň dalších 20 sekund. |

### <a name="citrix-vpn-added-for-windows-10-devices---1512457---"></a>Přidaná síť Citrix VPN pro zařízení s Windows 10<!-- 1512457 -->  
Pro zařízení s Windows 10 můžete nakonfigurovat Citrix VPN. Citrix VPN můžete zvolit ze seznamu *Vyberte typ připojení* v okně **Základní síť VPN** při konfiguraci VPN pro Windows 10 a novější.

> [!Note]
> Konfigurace Citrix existovala pro iOS a Android.

### <a name="wi-fi-connections-support-pre-shared-keys-on-ios---1550823---"></a>Připojení Wi-Fi podporují v iOS předem sdílené klíče.<!-- 1550823 -->
Zákazníci můžou nakonfigurovat profily sítě Wi-Fi, aby mohli na zařízeních s iOSem používat předsdílené klíče (PSK) pro připojení typu WPA/WPA2-Personal. Tyto profily se doručí do zařízení uživatelů, když se zařízení zaregistruje v Intune.

Když je profil doručený do zařízení, bude další krok záviset na tom, jak je profil nakonfigurovaný.  Pokud je profil nastavený na automatické připojení, aktivuje se připojení automaticky, až bude příště potřeba síť.  Pokud je profil nastavený na ruční připojení, musí uživatel aktivovat připojení ručně.  

### <a name="access-to-managed-app-logs-for-ios---1469920---"></a>Přístup k protokolům spravovaných aplikací pro iOS<!-- 1469920 -->
Koncoví uživatelé, kteří mají nainstalovaný Managed Browser, teď můžou zobrazit stav správy všech aplikací publikovaných Microsoftem a posílat protokoly pro řešení problémů se spravovanými aplikacemi pro iOS.

Informace o tom, jak na zařízení s iOSem povolit v Managed Browseru režim pro řešení problémů, najdete v tématu [Jak se dostat k protokolům spravovaných aplikací pomocí Managed Browseru na zařízení s iOSem](../apps/app-configuration-managed-browser.md#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

### <a name="improvements-to-device-setup-workflow-in-the-company-portal-for-ios-in-version-290---1417174---"></a>Vylepšení pracovního postupu instalace zařízení v Portál společnosti pro iOS ve verzi 2.9.0<!-- 1417174 -->

Pracovní postup instalace zařízení v aplikaci Portál společnosti pro iOS byl vylepšen. Jazyk je uživatelsky přívětivější a tam, kde to bylo možné, jsme také sjednotili obrazovky. Díky použití názvu vaší firmy všude v textu instalace je jazyk lépe přizpůsobený vaší firmě. Tento aktualizovaný pracovní postup uvidíte  [na stránce Co je nového v uživatelském rozhraní](whats-new-app-ui.md).

### <a name="user-entity-contains-latest-user-data-in-data-warehouse-data-model---1544273---"></a>Entita uživatele obsahuje nejnovější uživatelská data v datovém modelu datového skladu.<!-- 1544273 -->
První verze datového modelu datového skladu Intune obsahovala jenom poslední historická data Intune. Při vytváření sestav nebylo možné zachytit aktuální stav uživatele. V této aktualizaci se **entita uživatele** naplní nejnovějšími uživatelskými daty.

<!-- ########################## -->
## <a name="october-2017"></a>Říjen 2017

### <a name="ios-and-android-line-of-business-app-version-number-is-visible---1380712---"></a>číslo verze obchodní aplikace pro iOS a Android je viditelné.<!-- 1380712 -->

Aplikace v Intune teď zobrazují číslo verze obchodních aplikací pro iOS a Android. Číslo se zobrazuje na portálu Azure Portal v seznamu aplikací a v okně přehledu aplikace. Koncoví uživatelé uvidí číslo aplikace v aplikaci Portál společnosti a na webovém portálu.

__Číslo úplné verze:__ Číslo úplné verze identifikuje konkrétní vydanou verzi aplikace. Číslo se zobrazí jako _Verze_(_build_). Příklad: 2.2(2.2.17560800)

Celé číslo verze tvoří dvě části:

- **Verze**  
  Číslo verze je čitelné číslo vydané verze aplikace. Koncovým uživatelům slouží k identifikaci různých vydaných verzí aplikace.

- **Číslo buildu**  
  Číslo buildu je interní číslo, které může sloužit k rozpoznání aplikace a její programové správě. Číslo buildu se vztahuje k iteraci aplikace, která odkazuje na změny v kódu.

Další informace o číslech verzí a vývoji obchodních aplikací si přečtěte v článku [Začínáme s Microsoft Intune App SDK](../developer/app-sdk-get-started.md#line-of-business-app-version-numbers).

### <a name="device-and-app-management-integration---677972---"></a>Integrace správy zařízení a aplikací<!-- 677972 -->
Teď, když je Správa mobilních zařízení (MDM) a Správa mobilních aplikací (MAM) v Intune dostupná jak z Azure Portal, Intune zahájil integraci prostředí pro správu IT v rámci správy aplikací a zařízení. Tyto změny jsou zaměřené na zjednodušení způsobu správy zařízení a aplikací.

Další informace o změnách MDM a MAM najdete na [blogu týmu podpory Intune](https://blogs.technet.microsoft.com/intunesupport/2017/09/19/support-tip-setting-up-communication-between-mam-managed-and-mdm-managed-apps/).

### <a name="new-enrollment-alerts-for-apple-devices---1471790---"></a>Nové výstrahy registrace pro zařízení Apple<!-- 1471790 -->
Stránka s přehledem registrace bude správcům IT zobrazovat užitečná upozornění týkající se správy zařízení Apple. Upozornění se budou zobrazovat na stránce přehledu vždy, když se bude blížit konec platnosti certifikátu Apple MDM Push Certificate a tokenu Programu registrace zařízení nebo když už jejich platnost vypršela. Budou se zobrazovat také v případě, že v Programu registrace zařízení existují nepřiřazená zařízení.

### <a name="support-token-replacement-for-app-configuration-without-device-enrollment---1080364---"></a>Podpora nahrazení tokenu pro konfiguraci aplikace bez registrace zařízení<!-- 1080364 -->

U aplikací v zařízeních, která nejsou zaregistrovaná, můžete pro dynamické hodnoty v konfiguracích aplikací použít tokeny. Další informace najdete v článku [Přidání zásad konfigurace aplikací pro spravované aplikace bez registrace zařízení](../apps/app-configuration-policies-managed-app.md).

### <a name="updates-to-the-company-portal-app-for-windows-10--1299474--"></a>Aktualizace aplikace Portál společnosti pro Windows 10<!--1299474-->
Stránka Nastavení aplikace Portál společnosti pro Windows 10 je aktualizovaná, aby nastavení a zamýšlené akce uživatelů byly konzistentnější v rámci všech nastavení. Stránka také byla aktualizována tak, aby rozložením odpovídala jiným aplikacím pro Windows. Na stránce [Co je nového v uživatelském rozhraní aplikace](whats-new-app-ui.md) najdete obrázky aplikace před a po aktualizaci.

### <a name="inform-end-users-what-device-information-can-be-seen-for-windows-10-devices--1337920--"></a>Informování koncových uživatelů o tom, jaké informace o zařízení se dají zobrazit pro zařízení s Windows 10<!--1337920-->
Na obrazovku Podrobnosti o zařízení v aplikaci Portál společnosti pro Windows 10 jsme přidali **Typ vlastnictví**. To umožní uživatelům zjistit další informace o ochraně osobních údajů přímo z této stránky z dokumentace pro koncové uživatele Intune. Budou také moci najít tyto informace na obrazovce **o produktu** .

### <a name="feedback-prompts-for-the-company-portal-app-for-android--1165249--"></a>Výzvy k zadání názoru pro aplikaci Portál společnosti pro Android<!--1165249-->
Aplikace portál společnosti pro Android teď požaduje zpětnou vazbu koncového uživatele. Tato zpětná vazba se pošle přímo společnosti Microsoft a poskytne koncovým uživatelům příležitost zadat recenzi k aplikaci ve veřejném obchodě Google Play. Zpětná vazba není povinná a je možné ji snadno zrušit, takže uživatelé mohou dále používat aplikaci.

<!-- #### Update to what device details an organization can see 1616825
The Company Portal app for Android can now use geofencing to protect access to company resources. It uses network details such as IP address, default gateway address, and Domain Name System (DNS) to determine whether to allow access to protected company resources.-->

### <a name="helping-your-users-help-themselves-with-the-company-portal-app-for-android---1573324-1573150-1558616-1564878---"></a>Pomoc uživatelům s aplikací Portál společnosti pro Android<!-- 1573324, 1573150, 1558616, 1564878 -->

Aplikace Portál společnosti pro Android přidala pokyny pro koncové uživatele, které jim pomůžou porozumět novým případům použití a v případě potřeby i vyřešit problém vlastními silami.
- Koncoví uživatelé budou nasměrováni na [portál Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile), kde můžou zařízení odebrat v případě, že dosáhli maximálního počtu zařízení, která smí přidat.
- Koncovým uživatelům se zobrazí postup, aby mohli [opravit chyby aktivace na zařízeních se zabezpečením Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) nebo [vypnout režim snížené spotřeby](https://go.microsoft.com/fwlink/?linkid=2077422&clcid=0x409). Pokud ani jedno z řešení jejich problém nevyřeší, zobrazí se jim vysvětlení, jak mohou [odeslat protokoly do Microsoftu](../user-help/send-logs-to-microsoft-android.md).

### <a name="new-resolve-action-available-for-android-devices---1583480---"></a>K dispozici je nová akce vyřešit pro zařízení s Androidem.<!-- 1583480 -->

Aplikace Portál společnosti pro Android představuje akci Vyřešit na stránce _Aktualizovat nastavení zařízení_. Výběrem této možnosti koncový uživatel přejde přímo na nastavení, které způsobuje, že jeho zařízení nevyhovuje předpisům. V současné době aplikace Portál společnosti pro Android podporuje tuto akci u [hesla zařízení](../user-help/set-your-pin-or-password-android.md), [ladění USB](../user-help/you-need-to-turn-off-usb-debugging-android.md) a u nastavení [Neznámé zdroje](../user-help/you-need-to-turn-off-unknown-sources-android.md).

### <a name="device-setup-progress-indicator-in-android-company-portal---1565657---"></a>Indikátor průběhu instalace zařízení v Androidu Portál společnosti<!-- 1565657 -->
Aplikace Portál společnosti pro Android zobrazuje indikátor průběhu instalace zařízení, když uživatel provádí registraci zařízení. Indikátor zobrazuje nové stavy, od „Nastavení zařízení...“, přes „Probíhá registrace zařízení...“ a „Dokončení registrace zařízení...“ a potom „Dokončení nastavení zařízení...“.

### <a name="certificate-based-authentication-support-on-the-company-portal-for-ios--1029830--"></a>Podpora ověřování na základě certifikátů na Portál společnosti pro iOS<!--1029830-->
Přidali jsme podporu ověřování pomocí certifikátů v aplikaci Portál společnosti pro iOS. Uživatelé, kteří mají certifikátů, zadejte svoje uživatelské jméno a pak klepněte na odkaz Přihlásit se pomocí certifikátu. V aplikacích Portál společnosti pro Android a Windows je už ověřování pomocí certifikátů podporované. Další informace najdete na stránce o [přihlášení do aplikace Portál společnosti](../user-help/sign-in-to-the-company-portal.md).

### <a name="apps-that-are-available-with-or-without-enrollment-can-now-be-installed-without-being-prompted-for-enrollment---1334712---"></a>Aplikace, které jsou dostupné s registrací nebo bez registrace, lze nyní nainstalovat bez výzvy k registraci<!-- 1334712 -->

Firemní aplikace, které byly v aplikaci Portál společnosti pro Android dostupné s registrací nebo bez registrace, se teď můžou nainstalovat bez výzvy k registraci.

### <a name="windows-autopilot-deployment-program-support-in-microsoft-intune----747617----"></a>Podpora programu Windows AutoPilot Deployment v Microsoft Intune <!-- 747617  -->
Teď můžete Microsoft Intune používat s programem Windows AutoPilot Deployment, abyste uživatelům umožnili zřizovat firemní zařízení bez zapojení IT pracovníků. Můžete přizpůsobit software spouštěný při prvním zapnutí a nasměrovat uživatele k tomu, aby své zařízení připojili k Azure AD a zaregistrovali v Intune. Microsoft Intune a Windows AutoPilot společně eliminují potřebu nasazovat, udržovat a spravovat image operačního systému. Podrobnosti najdete v článku [Registrace zařízení s Windows pomocí programu Windows AutoPilot Deployment](../enrollment/enrollment-autopilot.md).

### <a name="quickstart-for-device-enrollment----1425655---"></a>Rychlý Start pro registraci zařízení <!-- 1425655 --> 
V **zápisu zařízení** je nyní k dispozici rychlý Start a poskytuje tabulku odkazů pro správu platforem a konfiguraci procesu registrace. Stručný popis jednotlivých položek a odkazy na dokumentaci s podrobnými pokyny poskytují užitečnou dokumentaci, která zjednodušuje zahájení práce.

### <a name="device-categorization---1427491---"></a>Kategorizace zařízení<!-- 1427491 -->
Graf platforem zaregistrovaných zařízení v okně **Zařízení > Přehled** uspořádá zařízení podle platforem, včetně Androidu, iOSu, macOS, Windows a Windows Mobile.  Zařízení s jinými operačními systémy jsou seskupená do kategorie „Ostatní“.  Ta zahrnuje zařízení od výrobců Blackberry, NOKIA a dalších.  

Pokud chcete zjistit, která zařízení jsou ve vašem tenantovi ovlivněna, zvolte **Spravovat > Všechna zařízení** a pak pomocí **Filtrovat** omezte pole **OS**.

### <a name="zimperium---new-mobile-threat-defense-partner-----954681---"></a>Zimperium – nový partner ochrany před mobilními hrozbami  <!-- 954681 -->  
Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí Zimperium, řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune.

#### <a name="how-integration-with-intune-works"></a>Jak integrace se službou Intune funguje
Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých služba Zimperium běží. Zásady podmíněného přístupu EMS můžete nakonfigurovat na základě posouzení rizik s Zimperium, které jsou povolené prostřednictvím zásad dodržování předpisů zařízením Intune, které můžete použít k povolení nebo blokování nevyhovujících zařízení pro přístup k podnikovým prostředkům na základě zjištěných hrozeb.

### <a name="new-settings-for-windows-10-device-restriction-profile-----978575-1308849---"></a>Nová nastavení pro profil omezení zařízení s Windows 10 <!--- 978575, 1308849, -->  
Do profilu omezení zařízení s Windows 10 v kategorii filtru SmartScreen v programu Windows Defender přidáváme nová nastavení.

Podrobnosti o profilu omezení zařízení s Windows 10 najdete v tématu [Nastavení omezení pro zařízení Windows 10 a novější](../configuration/device-restrictions-windows-10.md).

### <a name="remote-support-for-windows-and-windows-mobile-devices-----1070473---"></a>Vzdálená podpora pro zařízení s Windows a Windows Mobile  <!-- 1070473 -->  
Intune vám teď pomocí samostatně zakoupeného softwaru [TeamViewer](https://www.teamviewer.com) umožňuje poskytovat vzdálenou pomoc uživatelům, kteří používají zařízení s Windows a Windows Mobile.

### <a name="scan-devices-with-windows-defender---1280988--1280990-----"></a>Kontrola zařízení pomocí programu Windows Defender<!-- 1280988  1280990   -->
Na spravovaných zařízeních s Windows 10 teď můžete pomocí Antivirové ochrany v programu Windows Defender provádět **rychlou kontrolu**, **úplnou kontrolu** a **aktualizaci signatur**. V okně s přehledem zařízení zvolte akci, která se má na zařízení spustit. Před odesláním příkazu do zařízení budete vyzváni k potvrzení. 

**Rychlá kontrola:** Při rychlé kontrole se kontrolují místa, kde se registruje spuštění malwaru, jako jsou klíče registru a známé spouštěcí složky Windows. Rychlá kontrola trvá průměrně pět minut. V kombinaci s nastavením **trvalé ochrany v reálném čase**, která soubory kontroluje při otevření, zavření a vždy, když uživatel přejde do nějaké složky, poskytuje rychlá kontrola ochranu před malwarem, který se může nacházet v systému nebo jádru. Uživatelé uvidí na svých zařízeních výsledky kontroly potom, co se dokončí. 

**Úplná kontrola:** Úplnou kontrolu využijete u zařízení napadených malwarem, kdy umožňuje zjistit, jestli v zařízení nezůstaly nějaké neaktivní komponenty, které vyžadují důkladnější vyčištění. Slouží také ke spuštění kontrol na vyžádání. Úplná kontrola může trvat hodinu. Uživatelé uvidí na svých zařízeních výsledky kontroly potom, co se dokončí. 

**Aktualizace signatur:** Tímto příkazem se u Antivirové ochrany v programu Windows Defender aktualizují definice a signatury malwaru. Tím se zajistí účinnost Antivirové ochrany v programu Windows Defender při zjišťování malwaru. Tato funkce je určená jen pro zařízení s Windows 10 a očekává, že je zařízení připojené k internetu. 

### <a name="the-enabledisable-button-is-removed-from-the-intune-certificate-authority-page-of-the-intune-azure-portal----1400455---"></a>Na stránce certifikační autorita Intune služby Intune se odebere tlačítko Povolit/zakázat Azure Portal <!-- 1400455 -->
 Odstraňujeme nadbytečný krok při nastavení Certificate Connectoru v Intune. V současné době stáhnete Certificate Connector a pak ho povolíte v konzole Intune. Pokud ale konektor v konzole Intune zakážete, dál vydává certifikáty.

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?
Od října už se tlačítko Povolit/Zakázat na stránce certifikační autority na portálu Azure Portal zobrazovat nebude. Funkce konektoru zůstává stejná. Do zařízení zaregistrovaných v Intune se budou certifikáty dál nasazovat. Certificate Connector můžete dál stáhnout a nainstalovat. Pokud chcete zastavit vydávání certifikátů, Certificate Connector teď místo zakázání odinstalujete.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit?
Pokud máte Certificate Connector aktuálně zakázaný, měli byste ho odinstalovat.

### <a name="new-settings-for-windows-10-team-device-restriction-profile------1308838---"></a>Nová nastavení pro profil omezení zařízení s Windows 10 Team  <!--- 1308838 -->
V této verzi jsme přidali spoustu nových nastavení do profilu omezení zařízení s Windows 10 Team, která vám pomůžou řídit Surface Hub zařízení.

Další informace o tomto profilu najdete v článku [Nastavení omezení zařízení s Windows 10 Team](../configuration/device-restrictions-windows-10-teams.md).

### <a name="prevent-users-of-android-devices-from-changing-their-device-date-and-time----1333292---"></a>Zabránit uživatelům zařízení s Androidem změnit datum a čas zařízení <!-- 1333292 -->
Pomocí [vlastních zásad zařízení s Androidem](../configuration/custom-settings-android.md) můžete uživatelům zabránit, aby na zařízení změnili datum a čas.

Uděláte to tak, že nakonfigurujete vlastní zásadu pro Android s identifikátorem URI nastavení ./Vendor/MSFT/PolicyManager/My/System/AllowDateTimeChange. Nastavte tuto zásadu na **TRUE** a pak ji přiřaďte požadovaným skupinám.

### <a name="bitlocker-device-configuration---1397398---"></a>Konfigurace zařízení BitLockeru<!-- 1397398 -->
Možnost **Šifrování Windows > Základní nastavení** obsahuje nové nastavení **Upozornění na jiné šifrování disku**, které vám umožní zakázat [výzvu s upozorněním](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowwarningforotherdiskencryption) na jiné šifrování disku, které se na zařízení uživatele může používat.  Tato výzva s upozorněním vyžaduje souhlas koncového uživatele s nastavením BitLockeru na zařízení a toto nastavení blokuje, dokud ho koncový uživatel nepotvrdí.  Toto nové nastavení zakazuje upozornění koncového uživatele.


### <a name="volume-purchase-program-for-business-apps-will-now-sync-to-your-intune-tenant---800882---"></a>Aplikace Volume purchase program pro firmy se teď budou synchronizovat s vaším klientem Intune.<!-- 800882 -->  
Vývojáři třetích stran můžou soukromě distribuovat aplikace autorizovaným členům programu Volume Purchase Program (VPP) for Business, kteří jsou uvedeni ve službě iTunes Connect. Tito členové programu VPP for Business se mohou přihlásit do zvláštního App Storu pro tento program a aplikace si zakoupit.

Od této verze se teď začnou aplikace VPP for Business zakoupené koncovým uživatelem synchronizovat s jeho tenanty Intune.

### <a name="select-apple-countryregion-store-to-sync-vpp-apps----1332311---"></a>Výběr země/oblasti obchodu Apple pro synchronizaci aplikací VPP <!-- 1332311 -->  
Při nahrávání tokenu VPP můžete nakonfigurovat obchod země/oblasti programu Volume purchase program (VPP). Intune synchronizuje aplikace VPP pro všechna národní prostředí ze zadaného úložiště v zemi nebo oblasti VPP.

> [!NOTE]  
> V současné době Intune synchronizuje aplikace VPP jenom z obchodu VPP země/oblast, která se shoduje s národním prostředím Intune, ve kterém se vytvořil tenant Intune.


### <a name="block-copy-and-paste-between-work-and-personal-profiles-in-android-for-work---1098994---"></a>Blokování kopírování a vkládání mezi pracovními a osobními profily v Androidu for Work<!-- 1098994 -->
V této verzi můžete pracovní profil pro Android for Work nakonfigurovat tak, aby bylo zablokované kopírování a vkládání mezi pracovními a osobními aplikacemi. Toto nové nastavení najdete v profilu **Omezení zařízení** pro platformu **Android for Work** v **Nastavení pracovního profilu**.

### <a name="create-ios-apps-limited-to-specific-regional-apple-app-stores---1281692---"></a>Vytváření aplikací pro iOS omezených na konkrétní místní obchody Apple App<!-- 1281692 -->
Během vytváření spravované aplikace pro Apple App Store budete moct zadat národní prostředí země nebo oblasti.

> [!Note]  
> V současné době můžete vytvářet jenom spravované aplikace Apple App Store, které jsou k dispozici v úložišti země/oblasti USA.

### <a name="update-ios-vpp-user-and-device-licensed-apps----1305564---"></a>Aktualizace licencovaných aplikací pro iOS VPP uživatelů a zařízení <!-- 1305564 -->  
Token VPP pro iOS budete moci nakonfigurovat tak, aby se prostřednictvím služby Intune aktualizovaly všechny aplikace zakoupené pro tento token. Intune zjistí aktualizace aplikací VPP v App Storu a automaticky je nabídne zařízení, jakmile se zařízení ohlásí.

Pokyny k nastavení tokenu VPP a povolení automatických aktualizací najdete v článku [Správa aplikací pro systém iOS nakoupených prostřednictvím programu hromadného nákupu pomocí Microsoft Intune] (/intune/vpp-apps-ios).


### <a name="user-device-association-entity-collection-added-to-intune-data-warehouse-data-model---1187917---"></a>Přidala se kolekce entit přidružení uživatelských zařízení do datového modelu datového skladu Intune.<!-- 1187917 -->
Pomocí informací o přidružení uživatelů a zařízení, které přidružují kolekce entit uživatelů a zařízení, teď můžete vytvářet sestavy a vizualizace dat. Tento datový model lze zpřístupnit přes soubor Power BI (PBIX) načtený ze stránky Datový sklad v Intune, přes koncový bod OData nebo vývojem vlastního klienta.

### <a name="review-policy-compliance-for-windows-10-update-rings---1067886---"></a>Kontrola dodržování zásad pro aktualizační kanály Windows 10<!-- 1067886 -->
Přes Aktualizace softwaru > Stav nasazení podle kruhu aktualizace budete moct zkontrolovat sestavu zásad pro aktualizační kanály Windows 10. Tato sestava zásad obsahuje stav nasazení pro nakonfigurované aktualizační okruhy. 

### <a name="new-report-that-lists-ios-devices-with-older-ios-versions-----1352223---"></a>Nová sestava se seznamem zařízení s iOS se staršími verzemi iOS  <!-- 1352223 -->
Sestava **zařízení se zastaralým iOSem** je k dispozici z pracovního prostoru **Aktualizace softwaru**. V sestavě můžete zobrazit seznam zařízení s iOSem pod dohledem, na která byla zacílena zásada aktualizace iOSu a pro která jsou k dispozici aktualizace. Pro každé zařízení můžete zobrazit stav, proč nebylo automaticky aktualizováno. 

### <a name="view-app-protection-policy-assignments-for-troubleshooting----1475003---"></a>Zobrazení přiřazení zásad ochrany aplikací pro řešení potíží<!--  1475003 -->
V této nadcházející verzi bude do rozevíracího seznamu **Přiřazení**, který je dostupný v okně pro řešení potíží, přidána možnost **Zásady ochrany aplikací**. Výběrem zásad ochrany aplikací teď můžete zobrazit zásady ochrany aplikací přiřazené vybraným uživatelům.



### <a name="improvements-to-device-setup-workflow-in-company-portal--1490692--"></a>Vylepšení pracovního postupu instalace zařízení v Portál společnosti<!--1490692-->
Vylepšili jsme pracovní postup instalace zařízení v aplikaci Portál společnosti pro Android. Jazyk je uživatelsky přívětivější a přizpůsobenější potřebám vaší společnosti. Tam, kde to bylo možné, jsme také zkombinovali obrazovky. Tato vylepšení najdete na stránce s [novinkami v uživatelském rozhraní aplikace](whats-new-app-ui.md#week-of-october-2-2017).

### <a name="improved-guidance-around-the-request-for-access-to-contacts-on-android-devices--1484985--"></a>Vylepšené pokyny k žádosti o přístup ke kontaktům na zařízeních s Androidem<!--1484985-->

Aplikace Portál společnosti často po koncových uživatelích vyžaduje, aby přijali oprávnění Kontaktů. Pokud koncový uživatel tento přístup zamítne, zobrazí se mu nyní oznámení v aplikaci, které je upozorní na udělení podmíněného přístupu. 

### <a name="secure-startup-remediation-for-android--1490712--"></a>Zabezpečená náprava při spuštění pro Android<!--1490712-->

Koncoví uživatelé, kteří používají zařízení s Androidem, budou moct v aplikaci Portál společnosti klepnout na důvod nedodržení předpisů. Pokud to bude možné, přejdou tímto klepnutím přímo do správného umístění v aplikaci Nastavení, aby mohli problém vyřešit. 

### <a name="additional-push-notifications-for-end-users-on-the-company-portal-app-for-android-oreo--1475932--"></a>Další nabízená oznámení pro koncové uživatele v aplikaci Portál společnosti pro Android Oreo<!--1475932-->

Koncovým uživatelům se zobrazí další oznámení, která je upozorní, že aplikace Portál společnosti pro Android Oreo provádí úlohy na pozadí, třeba načítání zásad ze služby Intune. Pro koncové uživatele tak bude transparentnější, kdy Portál společnosti na jejich zařízení provádí úlohy správy. Jde o součást celkové [optimalizace uživatelského rozhraní Portálu společnosti](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) pro aplikaci Portál společnosti pro Android Oreo. 

Provedli jsme další optimalizace nových prvků uživatelského rozhraní, které jsou v Androidu Oreo povoleny.  Koncovým uživatelům se zobrazí další oznámení, která je upozorní, že Portál společnosti provádí úlohy na pozadí, třeba načítání zásad ze služby Intune.  Pro koncové uživatele tak bude transparentnější, kdy Portál společnosti na jejich zařízení provádí úlohy správy.

### <a name="new-behaviors-for-the-company-portal-app-for-android-with-work-profiles---1485783---"></a>Nové chování pro aplikaci Portál společnosti pro Android s pracovními profily<!-- 1485783 -->

Při registraci zařízení s Androidem for Work s pracovním profilem se o správu úloh na tomto zařízení stará aplikace Portál společnosti v pracovním profilu. 

Pokud v osobním profilu nepoužíváte nějakou aplikaci s podporou MAM, neslouží už aplikace Portál společnosti k žádnému účelu. Kvůli příjemnější práci v pracovním profilu Intune po úspěšné registraci pracovního profilu automaticky skryje osobní aplikaci Portál společnosti.

Aplikaci Portál společnosti pro Android můžete v osobním profilu kdykoli povolit tak, že přejdete na [Portál společnosti v Obchodě Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) a klepnete na **Povolit**.

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode--1428681--"></a>Portál společnosti pro Windows 8.1 a Windows Phone 8,1 přesun do trvalého režimu<!--1428681-->

Počínaje říjnem 2017 přejdou aplikace Portál společnosti pro Windows 8.1 a Windows Phone 8.1 do udržovacího režimu. To znamená, že tyto aplikace a existující scénáře (například registrace a dodržování předpisů) budou pro tyto platformy nadále podporovány. Tyto aplikace budu pořád dostupné ke stažení přes existující vydávací kanály, jako je Microsoft Store. 

Jakmile tyto aplikace budou v udržovacím režimu, budou dostávat jen důležité aktualizace zabezpečení. Pro tyto aplikace se už nebudou vydávat další aktualizace ani funkce. Kvůli novým funkcím doporučujeme zařízení aktualizovat na Windows 10 nebo Windows 10 Mobile. 


### <a name="block-unsupported-samsung-knox-device-enrollment----1490695---"></a>Zablokovat nepodporovanou registraci zařízení Samsung KNOX <!-- 1490695 -->

Aplikace Portál společnosti se pokusí zaregistrovat pouze podporovaná zařízení Samsung Knox. Aby se předešlo chybám při aktivaci zabezpečením Knox, které brání registraci MDM, pokus o registraci proběhne jenom u těch zařízení, která jsou v [seznamu zařízení publikovaném společností Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Některá čísla modelů zařízení Samsung mohou podporovat Knox, ale jiná nemusí. Než si zařízení koupíte a nasadíte, ověřte si u prodejce, zda je vaše zařízení kompatibilní se systémem Knox. Kompletní seznam ověřených zařízení najdete v [nastavení zásad pro Android a Samsung Knox Standard](supported-devices-browsers.md#intune-supported-web-browsers).

### <a name="end-of-support-for-android-43-and-lower---1171126-1326920---"></a>Konec podpory pro Android 4,3 a nižší<!-- 1171126, 1326920 -->
Spravované aplikace a aplikace Portál společnosti pro Android budou pro přístup k firemním prostředkům vyžadovat operační systém Android 4.4 nebo novější. Od prosince budou všechna zaregistrovaná zařízení vyřazena, čímž dojde ke ztrátě přístupu k firemním prostředkům. Pokud používáte zásady ochrany aplikací bez správy mobilních zařízení MDM, aplikace nebudou získávat aktualizace a kvalita jejich činnosti bude časem upadat.

### <a name="inform-end-users-what-device-information-can-be-seen-on-enrolled-devices--1165314--"></a>Informování koncových uživatelů o tom, jaké informace o zařízení je možné zobrazit v zaregistrovaných zařízeních<!--1165314-->
Na obrazovku Podrobnosti o zařízení ve všech aplikacích Portál společnosti přidáváme **Typ vlastnictví**. Uživatelům to umožní zjistit další informace o ochraně osobních údajů přímo z článku [Jaké informace moje společnost uvidí?](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md). Tuto funkci budeme v blízké budoucnosti postupně zavádět ve všech aplikacích Portál společnosti. Pro iOS jsme implementaci této funkce oznámili v [září](#september-2017).

<!-- ########################## -->
## <a name="september-2017"></a>Září 2017

### <a name="intune-supports-ios-11--1428975--"></a>Intune podporuje iOS 11.<!--1428975-->
Intune podporuje iOS 11. Tuto podporu jsme již dříve oznámili na [blogu podpory Intune](https://blogs.technet.microsoft.com/intunesupport/2017/09/12/support-tip-intune-support-for-ios-11/).

### <a name="end-of-support-for-ios-80---1164477---"></a>Konec podpory pro iOS 8,0<!-- 1164477 -->
Spravované aplikace a aplikace Portál společnosti pro iOS budou pro přístup k firemním prostředkům vyžadovat operační systém iOS 9.0 nebo novější. Zařízení, která nebudou do tohoto září aktualizována, již nebudou mít k těmto aplikacím nebo k Portálu společnosti přístup. 

### <a name="refresh-action-added-to-the-company-portal-app-for-windows-10--1132468--"></a>Do aplikace Portál společnosti pro Windows 10 se přidala akce aktualizace.<!--1132468-->
Aplikace Portál společnosti pro Windows 10 umožňuje uživatelům aktualizovat data v aplikaci, a to buď potažením prstem, nebo stisknutím klávesy F5 na počítačích.

### <a name="inform-end-users-what-device-information-can-be-seen-for-ios--739894--"></a>Informování koncových uživatelů o tom, jaké informace o zařízení se dají zobrazit pro iOS<!--739894-->

Do obrazovky s podrobnostmi o zařízení v aplikaci Portál společnosti pro iOS jsme přidali **typ vlastnictví** . To umožní uživatelům zjistit další informace o ochraně osobních údajů přímo z této stránky z dokumentace pro koncové uživatele Intune. Budou také moci najít tyto informace na obrazovce o produktu.

### <a name="allow-end-users-to-access-the-company-portal-app-for-android-without-enrollment---1169910---"></a>Umožněte koncovým uživatelům přístup k aplikaci Portál společnosti pro Android bez registrace.<!---1169910--->

Koncoví uživatelé brzy nebudou muset svá zařízení registrovat, aby získali přístup k aplikaci Portál společnosti pro Android. Koncovým uživatelům v organizacích, které používají zásady ochrany aplikací, už nebudou při otevření aplikace Portál společnosti chodit výzvy k registraci jejich zařízení. Koncoví uživatelé budou také moct bez registrace zařízení z Portálu společnosti instalovat aplikace. 


### <a name="easier-to-understand-phrasing-for-the-company-portal-app-for-android---1396349---"></a>Snadnější pochopení formulace pro Portál společnosti aplikaci pro Android<!---1396349--->  

Proces registrace aplikace Portál společnosti pro Android byl zjednodušen novým textem, který koncovým uživatelům umožňuje jednodušší registraci. Pokud máte vlastní dokumentaci k registraci, měli byste ji aktualizovat, aby odrážela nové obrazovky. Ukázkové obrázky najdete na naší stránce [aktualizací uživatelského rozhraní aplikací Intune pro koncové uživatele](whats-new-app-ui.md#week-of-september-11-2017).

### <a name="windows-10-company-portal-app-added-to-windows-information-protection-allow-policy---677129---"></a>Windows 10 Portál společnosti aplikace přidaná do Windows Information Protection zásady povolení<!-- 677129 -->

Aplikace Portál společnosti pro Windows 10 byla aktualizována o podporu WIP (Windows Information Protection). Tuto aplikaci lze přidat do zásad povolení WIP. Díky této změně se už tato aplikace nemusí přidávat do seznamu **výjimek**.


<!-- ########################## -->
## <a name="august-2017"></a>Srpen 2017

### <a name="improvements-to-device-overview---1404453---"></a>Vylepšení přehledu zařízení<!-- 1404453 -->  
Ve vylepšeném přehledu zařízení se teď zobrazují registrovaná zařízení, jsou ale vyloučena zařízení spravovaná přes Exchange Active Sync. Zařízení Exchange ActiveSync nemají stejné možnosti správy jako registrovaná zařízení. Pokud chcete v Intune na Azure Portalu zjistit počet registrovaných zařízení a počet registrovaných zařízení podle platformy, přejděte na **Zařízení** > **Přehled**.

### <a name="improvements-to-device-inventory-collected-by-intune"></a>Vylepšení inventáře zařízení shromažďovaného službou Intune
<!-- 961134, 1104426, 1281327, 1333543 -->
V této verzi jsme provedli následující vylepšení informací o inventáři shromažďovaných zařízeními, která spravujete:
 
- Pro zařízení s Androidem teď můžete do inventáře zařízení přidat sloupec, ve kterém se zobrazuje nejnovější úroveň opravy jednotlivých zařízení. Tento údaj zobrazíte, když do seznamu zařízení přidáte sloupec **Úroveň opravy zabezpečení**.
- Zobrazení zařízení teď můžete filtrovat podle data registrace zařízení. Můžete například zobrazit jen zařízení, která byla zaregistrována po zadaném datu.
- Provedli jsme vylepšení filtru používaného poslední položkou **data vrácení se změnami** .
- V seznamu zařízení si teď u zařízení ve vlastnictví firmy můžete zobrazit telefonní číslo.
Pomocí podokna filtru můžete navíc vyhledat zařízení podle telefonního čísla.

Další podrobnosti o inventáři zařízení najdete v článku [Jak zobrazit inventář zařízení spravovaných přes Intune](../remote-actions/device-inventory.md).

### <a name="conditional-access-support-for-macos-devices"></a>Podpora podmíněného přístupu pro zařízení macOS 
<!-- 720172 -->
Teď můžete nastavit zásadu podmíněného přístupu, která vyžaduje, aby se zařízení Mac zaregistrovala do Intune a vyhovovala zásadám dodržování předpisů zařízením. Uživatelé si mohou například stáhnout aplikaci Portál společnosti Intune pro macOS a zaregistrovat svá zařízení Mac ve službě Intune. Intune prostřednictvím požadavků, jako je kód PIN, šifrování, verze operačního systému a integrita systému, vyhodnotí, zda zařízení Mac předpisy dodržuje nebo ne.

- Přečtěte si další informace o [podpoře podmíněného přístupu pro zařízení MacOS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).

### <a name="company-portal-app-for-macos-is-in-public-preview---1484796---"></a>Aplikace Portál společnosti pro macOS je ve verzi Public Preview.<!---1484796--->
Portál společnosti App for macOS je teď k dispozici jako součást veřejné verze Preview pro podmíněný přístup v Enterprise Mobility + Security. Tato verze podporuje macOS 10.11 a novější. Můžete ji získat zde: [https://aka.ms/macOScompanyportal](https://aka.ms/macOScompanyportal). 


### <a name="new-device-restriction-settings-for-windows-10"></a>Nová nastavení omezení pro zařízení s Windows 10    
<!--1063965, 1308850  -->
V této verzi jsme přidali nová nastavení pro [profil omezení zařízení s Windows 10](/intune/device-restrictions-windows-10) v následujících kategoriích:

- Filtr SmartScreen v programu Windows Defender
- App Store

### <a name="updates-to-the-windows-10-endpoint-protection-device-profile-for-bitlocker-settings"></a>Aktualizace profilu zařízení ochrany koncových bodů Windows 10 o nastavení BitLockeru
<!--1459533 -->    
V této verzi jsme provedli následující vylepšení, jak nastavení BitLockeru funguje v profilu zařízení s Windows 10 Endpoint Protection:
 
- V části **Nastavení jednotky s operačním systémem BitLocker**pro nastavení **BitLockeru s nekompatibilním čipem TPM**když vyberete **blokovat**, dříve to způsobí, že BitLocker bude skutečně povolený. Teď je to opravené a při výběru této možnosti se BitLocker zablokuje.
- V části **Nastavení jednotky s operačním systémem BitLocker**pro nastavení **agenta obnovení dat založeného na certifikátech**teď můžete explicitně zablokovat agenta obnovení dat založeného na certifikátech. Standardně je ale tento agent povolený.
- V **Nastavení BitLockeru pro jednotky s operačním systémem** teď můžete pomocí nastavení **Agent obnovení dat** explicitně zablokovat agenta obnovení dat.
Další informace najdete v tématu o [nastavení služby Endpoint Protection pro Windows 10 a novější](../protect/endpoint-protection-windows-10.md).


### <a name="new-signed-in-experience-for-android-company-portal-users-and-app-protection-policy-users---621669---"></a>Nové přihlášené prostředí pro uživatele Androidu Portál společnosti a zásady ochrany aplikací<!-- 621669 -->
Koncoví uživatelé teď můžou pomocí aplikace Portál společnosti pro Android procházet aplikace, spravovat zařízení a zobrazit kontakt na IT oddělení, aniž by své zařízení s Androidem zaregistrovali. Pokud už koncový uživatel používá aplikaci chráněnou zásadami Intune App Protection a spustí Portál společnosti pro Android, už se mu navíc nezobrazí výzva k registraci zařízení.

### <a name="new-setting-in-the-android-company-portal-app-to-toggle-battery-optimization--1405990--"></a>Nové nastavení v aplikaci pro Android Portál společnosti pro přepnutí optimalizace baterie<!--1405990-->
Stránka **Nastavení** v aplikaci Portál společnosti pro Android obsahuje nové nastavení, které uživatelům umožní snadno vypnout optimalizaci baterie pro aplikace Portál společnosti a Microsoft Authenticator. Název aplikace uvedený v nastavení se liší v závislosti na tom, která aplikace spravuje pracovní účet. Doporučujeme, aby uživatelé optimalizaci baterie vypnuli kvůli lepšímu výkonu pracovních aplikací, které synchronizují e-maily a data. 

### <a name="multi-identity-support-for-onenote-for-ios--------1234281---"></a>Podpora více identit pro OneNote pro iOS     <!-- 1234281 -->
Koncoví uživatelé teď můžou v Microsoft OneNotu pro iOS používat různé účty (pracovní a osobní). Na firemní data v pracovních poznámkových blocích lze uplatnit zásady ochrany aplikací, aniž to ovlivní osobní poznámkové bloky. Pomocí zásad můžete například uživateli povolit hledání informací v pracovních poznámkových blocích, ale zabránit v kopírování a vkládání firemních dat z pracovních do osobních poznámkových bloků.
 
- Přečtěte si další informace o aplikacích, které podporují [ochranu aplikací a více identit](https://www.microsoft.com/cloud-platform/microsoft-intune-apps) s Intune.

### <a name="new-settings-to-allow-and-block-apps-on-samsung-knox-standard-devices"></a>Nová nastavení, která povolí nebo blokují aplikace na zařízeních se zabezpečením Samsung Knox Standard
<!-- 1305423 822899-->  
V této verzi přidáváme nová [nastavení omezení zařízení](../configuration/device-restrictions-android.md), která vám umožní zadat následující seznamy aplikací:
 
- Aplikace, které mají uživatelé dovoleno instalovat.
- Aplikace, které mají uživatelé zakázáno spouštět.
- Aplikace, které jsou před uživatelem zařízení skryté.
 
Aplikaci můžete zadat pomocí adresy URL, názvu balíčku nebo ze seznamu spravovaných aplikací.

### <a name="new-azure-ad-app-based-conditional-access-policy-ui-link-from-intune"></a>Nové propojení uživatelského rozhraní zásad podmíněného přístupu založeného na aplikaci Azure AD z Intune
<!-- 1016201 -->
Správci IT teď můžou nastavit podmíněné zásady na základě aplikací prostřednictvím nového uživatelského rozhraní zásad podmíněného přístupu v úloze Azure AD. Podmíněný přístup na základě aplikace, který je v části Intune App Protection v Azure Portal, zůstane v tomto časovém intervalu a bude využíván vedle sebe. Existuje také praktický odkaz na nové uživatelské rozhraní zásad podmíněného přístupu v rámci úlohy Intune.

- Přečtěte si další informace o [podmíněném přístupu na základě aplikace v Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference).

<!-- ########################## -->
## <a name="july-2017"></a>Červenec 2017

### <a name="restrict-android-and-ios-device-enrollment-restriction-by-os-version-----1333256--1245463----"></a>Omezení registrace zařízení s Androidem a iOS podle verze operačního systému <!--- 1333256,  1245463 --->
Intune nyní podporuje omezení registrace iOSu a Androidu podle čísla verze operačního systému. V části **Omezení typu zařízení** teď správce IT může nastavit konfiguraci platformy tak, aby se registrace omezovala na rozsah mezi minimální a maximální hodnotou verze operačního systému. Verze operačního systému Android je nutné zadávat ve formátu Hlavní.Podverze.Sestavení.Revize, kde Podverze, Sestavení a Revize jsou nepovinné hodnoty. Verze iOS je nutné zadávat ve formátu Hlavní.Podverze.Sestavení, kde Podverze a Sestavení jsou nepovinné hodnoty. Přečtěte si další informace o [omezení registrace zařízení](../enrollment/enrollment-restrictions-set.md).

>[!NOTE]
>Neomezuje registrace prostřednictvím registračních programů Apple nebo nástroje Apple Configurator.

### <a name="restrict-android-ios-and-macos-device-personally-owned-device-enrollment-----1333272--1333275-1245709----"></a>Omezení registrace zařízení v osobním vlastnictví zařízení s Androidem, iOS a macOS <!--- 1333272,  1333275, 1245709 --->
Intune může omezit registraci osobních zařízení tím, že kódy IMEI podnikových zařízení umístí do seznamu povolených. Intune teď tuto funkci rozšířil na iOS, Android a macOS na základě sériových čísel zařízení. Nahráním sériových čísel do Intune můžete zařízení předem deklarovat jako majetek společnosti. Pomocí omezení registrace můžete blokovat zařízení v osobním vlastnictví (BYOD) a umožnit registraci pouze zařízením ve vlastnictví společnosti. Přečtěte si další informace o [omezení registrace zařízení](../enrollment/enrollment-restrictions-set.md).

Pokud chcete importovat sériová čísla, přejděte na **Registrace zařízení** > **Identifikátory podnikových zařízení**, klikněte na **Přidat** a potom nahrajte soubor CSV (žádné záhlaví a dva odstavce pro sériová čísla a podrobnosti jako čísla IMEI). Pokud chcete omezit zařízení v osobním vlastnictví, přejděte na **Registrace zařízení** > **Omezení registrace**. V části **Omezení typů zařízení** vyberte **Výchozí** a potom vyberte **Konfigurace platformy**. Zařízení se systémem iOS, Android a macOS v osobním vlastnictví můžete **povolit** nebo **zakázat**.


### <a name="new-device-action-to-force-devices-to-sync-with-intune---711369---"></a>Nová akce zařízení pro vynucení synchronizace zařízení s Intune<!-- 711369 -->
V této verzi jsme přidali novou akci zařízení, která vynutí u vybraného zařízení okamžité ohlášení ve službě Intune. Jakmile se zařízení ohlásí, začne okamžitě přijímat veškeré čekající akce nebo zásady, které mu byly přiřazeny.  Tato akce vám může pomoct okamžitě ověřit a řešit potíže se zásadami, které jste přiřadili, aniž byste čekali na další plánované vrácení se změnami.
Podrobnosti najdete v části [Synchronizace zařízení](../remote-actions/device-sync.md).

### <a name="force-supervised-ios-devices-to-automatically-install-the-latest-available-software-update---777100---"></a>Vynutit zařízení iOS pod dohledem k automatické instalaci nejnovější dostupné aktualizace softwaru<!-- 777100 -->
V pracovním prostoru aktualizací softwaru jsou dostupné nové zásady, které donutí zařízení s iOSem, která jsou pod dohledem, automaticky instalovat nejnovější dostupnou aktualizaci softwaru. Podrobnosti najdete v článku [Konfigurace zásad aktualizací pro iOS](/intune/software-updates-ios).

### <a name="check-point-sandblast-mobile---new-mobile-threat-defense-partner----954651-1172027---"></a>Check Point SandBlast Mobile – nový partner ochrany před mobilními hrozbami <!-- 954651, 1172027 -->
Přístup mobilních zařízení k podnikovým prostředkům můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí služba Checkpoint SandBlast Mobile, řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune.

#### <a name="how-integration-with-intune-works"></a>Jak integrace se službou Intune funguje?
Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých služba Check Point SandBlast Mobile běží. Pomocí zásad dodržování předpisů zařízením v Intune můžete nakonfigurovat zásady podmíněného přístupu EMS na základě kontrolního bodu SandBlastu mobilního rizika. Podle zjištěných hrozeb můžete u zařízení nesplňujících požadavky povolit nebo zakázat přístup k podnikovým prostředkům.


### <a name="deploy-an-app-as-available-in-the-microsoft-store-for-business---748101---"></a>Nasazení aplikace jako dostupné ve Microsoft Store pro firmy<!-- 748101 -->
V této verzi teď správci můžou Microsoft Store pro firmy přiřadit jako dostupný. Pokud to udělají, koncoví uživatelé si můžou aplikaci nainstalovat z aplikace nebo webu Portál společnosti, aniž by byli přesměrováni do Microsoft Storu.

### <a name="ui-updates-to-the-company-portal-website--1313244-part-1--"></a>Aktualizace uživatelského rozhraní na web Portál společnosti<!--1313244 part 1-->
Provedli jsme několik aktualizací uživatelského rozhraní [webu Portál společnosti](https://portal.manage.microsoft.com) k vylepšení prostředí pro koncové uživatele.

- __Vylepšení dlaždic aplikací__: Ikony aplikací se teď budou zobrazovat s automaticky generovaným pozadím na základě převládající barvy ikony (pokud se dá zjistit). Tam, kde se toto pozadí použije, nahradí šedé ohraničení, které bylo dříve vidět na dlaždicích aplikací.

    Web Portál společnosti bude v nadcházející verzi zobrazovat velké ikony, kdykoli to bude možné. Doporučujeme, aby správci IT publikovali aplikace pomocí ikon s vysokým rozlišením a minimální velikostí 120 x 120 pixelů. 

- __Změny v navigaci__: Položky navigačního panelu se přesunuly do „hamburgerové“ nabídky vlevo nahoře. Stránka Kategorie byla odebrána. Uživatelé teď můžou filtrovat obsah podle kategorií během procházení.

- __Aktualizace Vybraných aplikací__: Přidali jsme na web vyhrazenou stránku, kde můžou uživatelé procházet aplikace, které jste speciálně vybrali, a upravili jsme uživatelské rozhraní sekce Vybrané na domovské stránce.

### <a name="ibooks-support-for-the-company-portal-website--1231841--"></a>Podpora iBooks pro web Portál společnosti<!--1231841-->
Na web Portál společnosti jsme přidali speciálně určenou stránku, která uživatelům umožňuje procházet a stahovat knihy iBooks. 


### <a name="additional-help-desk-troubleshooting-details-----applies-to-1263399-1326964-1341642----"></a>Další podrobnosti o řešení potíží s oddělením technické podpory<!---  Applies to 1263399, 1326964, 1341642 --->
Intune má aktualizované zobrazení pro řešení problémů, které je doplněné k informacím poskytovaným správcům a pracovníkům helpdesku. Teď si můžete zobrazit tabulku **Přiřazení**, ve které jsou shrnuta všechna přiřazení uživatele na základě členství ve skupinách. Tento seznam obsahuje:
- Mobilní aplikace
- Zásady slučitelnosti
- Konfigurační profily

Tabulka **Zařízení** teď navíc obsahuje sloupce **Typ připojení ke službě Azure AD** a **Vyhovuje Azure AD**. Další informace najdete v článku [Pomoc uživatelům s řešením problémů](help-desk-operators.md).



### <a name="intune-data-warehouse-public-preview"></a>Datový sklad Intune (Public Preview)
Datový sklad Intune denně vzorkuje data, aby mohl poskytovat historický přehled vašeho tenanta. K datům můžete mít získat přístup pomocí souboru Power BI (soubor PBIX) a odkazu OData, který je kompatibilní s celou řadu analytických nástrojů, nebo prostřednictvím interakce s rozhraním REST API. Další informace najdete v tématu [Použití Datového skladu Intune](../developer/reports-nav-create-intune-reports.md).


### <a name="light-and-dark-modes-available-for-the-company-portal-app-for-windows-10---676547---"></a>Světlé a tmavé režimy, které jsou k dispozici pro aplikaci Portál společnosti pro Windows 10<!---676547--->
Koncoví uživatelé budou mít možnost přizpůsobit barevný režim aplikace Portál společnosti pro Windows 10. Uživatel může změny provádět v sekci Nastavení aplikace Portál společnosti. Změna se zobrazí, jakmile uživatel aplikaci restartuje. Pro Windows 10 verze 1607 a novější se režim aplikace nastaví podle výchozího nastavení systému. Pro Windows 10 verze 1511 a starší se režim aplikace nastaví do světlého režimu.

### <a name="enable-end-users-to-tag-their-device-group-in-the-company-portal-app-for-windows-10---807046--"></a>Povolit koncovým uživatelům označit skupinu zařízení v aplikaci Portál společnosti pro Windows 10<!---807046-->
Koncoví uživatelé teď můžou vybrat, do které skupiny jejich zařízení patří, když ho označí přímo v aplikaci Portál společnosti pro Windows 10.

<!-- ########################## -->
## <a name="june-2017"></a>Červen 2017

### <a name="new-role-based-administration-access-for-intune-admins-----1099990---"></a>Nový přístup pro správu na základě rolí pro správce Intune  <!-- 1099990 -->  
Přidávají se nové role správce podmíněného přístupu, která umožňuje zobrazovat, vytvářet, upravovat a odstraňovat zásady podmíněného přístupu Azure AD. Dříve měli toto oprávnění jenom globální správci a správci zabezpečení. Oprávnění této role se dají udělit správcům Intune, aby měli přístup k zásadám podmíněného přístupu.


### <a name="tag-corporate-owned-devices-with-serial-number---1215070---"></a>Označení zařízení vlastněných společností pomocí sériového čísla<!-- 1215070 -->  
Intune nyní podporuje ukládání sériových čísel v systémech iOS, macOS a Android jako identifikátorů podnikových zařízení. Sériová čísla nemůžete používat k blokování registrace osobních zařízení, protože sériová čísla se při registraci neověřují. Blokování osobních zařízení podle sériového čísla bude dostupné v blízké budoucnosti.


### <a name="new-remote-actions-for-ios-devices---854689---"></a>Nové vzdálené akce pro zařízení s iOS<!-- 854689 -->
V této verzi jsme přidali dvě nové akce vzdáleného zařízení pro sdílené iPady, které spravují aplikaci Apple Classroom:

- [Odhlásit aktuálního uživatele](../remote-actions/device-logout-user.md) – odhlásí aktuálního uživatele zařízení s iOS, které zvolíte.
- [Odebrat uživatele](../remote-actions/device-remove-user.md) – odstraní vybraného uživatele z místní mezipaměti zařízení s iOSem.


### <a name="support-for-shared-ipads-with-the-ios-classroom-app---1044681---"></a>Podpora sdílených iPady s aplikací učebny pro iOS<!-- 1044681 -->
V této verzi jsme rozšířili podporu správy aplikace Classroom pro iOS tak, aby zahrnovala studenty, kteří se přihlásí do sdílených iPadů pomocí svých spravovaných Apple ID.


### <a name="changes-to-intune-built-in-apps---1332306---"></a>Změny integrovaných aplikací Intune<!-- 1332306 -->
Dříve služba Intune obsahovala řadu integrovaných aplikací, které jste mohli rychle přiřadit. Na základě vaší zpětné vazby jsme tento seznam odebrali a integrované aplikace už neuvidíte.
Pokud jste už ale nějaké integrované aplikace přiřadili, budou se v seznamu aplikací dál zobrazovat. Tyto aplikace můžete dál přiřazovat podle potřeby.
V pozdější verzi plánujeme přidat jednodušší způsob výběru a přiřazování integrovaných aplikací z Azure Portalu.

### <a name="easier-installation-of-office-365-apps----1121362----"></a>Jednodušší instalace aplikací Office 365<!--- 1121362 --->
Nový typ aplikace **Office 365 ProPlus** vám usnadní přiřazování aplikací Office 365 ProPlus 2016 na vámi spravovaná zařízení, na kterých běží nejnovější verze Windows 10. Pokud vlastníte příslušné licence, můžete si také nainstalovat Microsoft Project a Microsoft Visio. Požadované aplikace jsou spojeny dohromady a v seznamu aplikací v konzole Intune se zobrazují jako jedna aplikace.
Další informace najdete v tématu [Jak přidat aplikace Office 365 pro Windows 10](../apps/apps-add-office365.md).


### <a name="support-for-offline-apps-from-the-microsoft-store-for-business----777044----"></a>Podpora pro offline aplikace z Microsoft Store pro firmy<!--- 777044 --->
Aplikace Offline zakoupené v Microsoft Storu pro firmy se teď budou synchronizovat na Azure Portal. Tyto aplikace můžete nasadit pro skupiny zařízení nebo skupiny uživatelů. Offline aplikace bude instalovat služba Intune, nikoli Store.

### <a name="microsoft-teams-is-now-part-of-the-app-based-ca-list-of-approved-apps-----1257019---"></a>Microsoft Teams je teď součástí seznamu schválených aplikací pro certifikační autoritu na základě aplikace.  <!-- 1257019 -->
Aplikace Microsoft Teams pro iOS a Android je teď součástí schválených aplikací pro zásady podmíněného přístupu na základě aplikací pro Exchange a SharePoint Online. Aplikaci můžete nakonfigurovat pomocí okna Intune App Protection v Azure Portal pro všechny klienty, kteří aktuálně používají podmíněný přístup na základě aplikace.

### <a name="managed-browser-and-app-proxy-integration---1287310---"></a>Integrace spravovaného prohlížeče a proxy aplikací<!-- 1287310 -->
Spravovaný prohlížeč Intune Managed Browser je nyní možné integrovat do služby Azure AD Application Proxy, což umožní uživatelům získat přístup k interním webům, i když pracují vzdáleně. Uživatelé prohlížeče jako obvykle zadají adresu URL webu a Managed Browser požadavek prostřednictvím webové brány proxy aplikace přesměruje. Další informace najdete v tématu [Správa přístupu k internetu pomocí zásad spravovaného prohlížeče](../apps/app-configuration-managed-browser.md).

### <a name="new-app-configuration-settings-for-the-intune-managed-browser---682951---"></a>Nové nastavení konfigurace aplikace pro Intune Managed Browser<!-- 682951 -->
V této verzi jsme pro aplikaci Intune Managed Browser pro iOS a Android přidali další konfigurace. Pomocí zásad konfigurace aplikace nyní můžete prohlížeči nakonfigurovat výchozí domovskou stránku a záložky.
Další informace najdete v tématu [Správa přístupu k internetu pomocí zásad spravovaného prohlížeče](../apps/app-configuration-managed-browser.md).

### <a name="bitlocker-settings-for-windows-10----951707---"></a>Nastavení BitLockeru pro Windows 10 <!-- 951707 -->
Nyní můžete nastavení nástroje BitLocker konfigurovat pro zařízení s Windows 10 pomocí nového profilu zařízení Intune. Například můžete vyžadovat, aby se zařízení šifrovala, a také nakonfigurovat další nastavení, která se použijí při zapnutí nástroje BitLocker.
Další informace najdete v tématu o [nastavení služby Endpoint Protection pro Windows 10 a novější](../protect/endpoint-protection-windows-10.md).

### <a name="new-settings-for-windows-10-device-restriction-profile----978527--978550-978569-1050031-1058611-----"></a>Nová nastavení pro profil omezení zařízení s Windows 10<!--- 978527,  978550, 978569, 1050031, 1058611,  --->
V této verzi jsme přidali nová nastavení pro profil omezení zařízení s Windows 10 v následujících kategoriích:

- Windows Defender
- Mobilní síť a připojení
- Prostředí zamknuté obrazovky
- Ochrana osobních údajů
- Hledat
- Windows Spotlight
- Prohlížeč Microsoft Edge

Další informace o nastavení Windows 10 najdete v tématu [Nastavení omezení pro zařízení Windows 10 a novější](../configuration/device-restrictions-windows-10.md).


### <a name="company-portal-app-for-android-now-has-a-new-end-user-experience-for-app-protection-policies--1305217--"></a>Portál společnosti aplikace pro Android teď má nové prostředí koncového uživatele pro zásady ochrany aplikací.<!--1305217-->
Na základě zpětné vazby od zákazníků jsme aplikaci Portál společnosti pro Android upravili tak, aby zobrazovala tlačítko **Přístup k obsahu společnosti**. Naším záměrem je předejít zbytečné registraci koncových uživatelů, když pouze potřebují přístup k aplikacím s podporou zásad ochrany aplikací – funkce správy mobilních aplikací Intune. Tyto změny najdete na stránce s [novinkami v uživatelském rozhraní aplikace](whats-new-app-ui.md).

### <a name="new-menu-action-to-easily-remove-company-portal--1164569--"></a>Nová akce nabídky pro snadné odebrání Portál společnosti<!--1164569-->
Na základě zpětné vazby od uživatelů jsme do aplikace Portál společnosti pro Android přidali novou akci nabídky k zahájení odebrání Portálu společnosti ze zařízení. Tato akce odebere zařízení ze správy Intune, aby uživatel mohl aplikaci ze zařízení odebrat. Tyto změny najdete na stránce [novinek v uživatelském rozhraní aplikace](whats-new-app-ui.md) a v [dokumentaci pro koncové uživatele Androidu](../user-help/unenroll-your-device-from-intune-android.md).

### <a name="improvements-to-app-syncing-with-windows-10-creators-update--676505--"></a>Vylepšení synchronizace aplikací s Windows 10 Creators Update<!--676505-->
Aplikace Portál společnosti pro Windows 10 teď automaticky zahájí synchronizaci pro požadavky na instalaci zařízení s Windows 10 Creators Update (verze 1703). Omezí se tím potíže s pozastavením instalací aplikace ve stavu čekající synchronizace. Uživatelé navíc budou moct synchronizaci zahájit ručně uvnitř aplikace. Tyto změny najdete na stránce s [novinkami v uživatelském rozhraní aplikace](whats-new-app-ui.md).

### <a name="new-guided-experience-for-windows-10-company-portal---1058938---"></a>Nové prostředí s asistencí pro Windows 10 Portál společnosti<!---1058938--->
Aplikace Portál společnosti pro Windows 10 bude obsahovat návod s pokyny Intune pro zařízení, která nejsou identifikovaná nebo zaregistrovaná. Nové prostředí obsahuje podrobné pokyny, které provedou uživatele registrací do Azure Active Directory (která je nutná pro funkce podmíněného přístupu), a zápis do MDM (který je nutný pro funkce správy zařízení). Prostředí s asistencí bude přístupné z domovské stránky portálu společnosti. Uživatelé můžou aplikaci dál používat, i když registraci a zápis neprovedou, ale budou mít k dispozici omezené funkce.

Tato aktualizace se zobrazí pouze na zařízení s Windows 10 Anniversary Update (build 1607) a novějšími verzemi. Tyto změny najdete na stránce s [novinkami v uživatelském rozhraní aplikace](whats-new-app-ui.md).


### <a name="microsoft-intune-and-conditional-access-admin-consoles-are-generally-available"></a>Konzoly správců Microsoft Intune a podmíněného přístupu jsou obecně dostupné
Oznamujeme obecnou dostupnost nové služby Intune v konzole pro správu Azure Portal a v konzole pro správu podmíněného přístupu. Prostřednictvím Intune na Azure Portalu teď můžete spravovat všechny funkce Intune MAM a MDM v jednom sjednoceném prostředí pro správce a využívat seskupování a cílení služby Azure AD. Podmíněný přístup v Azure přináší v jedné sjednocené konzole bohatě funkční možnosti napříč Azure AD a Intune. A z prostředí pro správu vám přechod na platformu Azure umožňuje používat moderní prohlížeče.

Intune se teď na Azure Portalu na adrese portal.azure.com zobrazuje bez popisku **Preview**.

Pokud jste v centru zpráv nedostali některou z řady zpráv požadující provedení nějaké akce, abychom mohli migrovat vaše skupiny, nemusíte jako stávající zákazníci nic dělat. Možná jste také v centru zpráv dostali oznámení, že migrace trvá déle z důvodu chyb na naší straně. Usilovně pokračujeme v práci na migraci všech ovlivněných zákazníků.

### <a name="improvements-to-the-app-tiles-in-the-company-portal-app-for-ios"></a>Vylepšení dlaždic aplikací v aplikaci Portál společnosti pro iOS
Aktualizovali jsme vzhled dlaždic aplikací na domovské stránce tak, aby odrážely barvu brandingu nastavenou v Portálu společnosti. Další informace najdete v [novinkách v uživatelském rozhraní aplikace](whats-new-app-ui.md).

### <a name="account-picker-now-available-for-the-company-portal-app-for-ios"></a>Pro aplikaci Portál společnosti pro iOS je teď dostupný výběr účtu
Uživatelům zařízení s iOSem se při přihlašování do Portálu společnosti může zobrazit náš nový výběr účtu, pokud k přihlašování do jiných aplikací Microsoftu používají svůj pracovní nebo školní účet. Další informace najdete v [novinkách v uživatelském rozhraní aplikace](whats-new-app-ui.md).

<!-- ########################## -->
## <a name="may-2017"></a>Květen 2017

### <a name="change-your-mdm-authority-without-unenrolling-managed-devices--1103950--"></a>Změňte autoritu MDM, aniž byste museli zrušit registraci spravovaných zařízení.<!--1103950-->
Autoritu pro správu mobilních zařízení teď můžete změnit, aniž byste museli kontaktovat podporu Microsoftu a zrušit registraci a provést novou registraci stávajících spravovaných zařízení. V konzole nástroje Configuration Manager můžete změnit autoritu pro správu mobilních zařízení z Nastavit na nástroj Configuration Manager (hybridní) na Microsoft Intune (samostatné) a naopak.


### <a name="improved-notification-for-samsung-knox-startup-pins--1087143--"></a>Vylepšené oznámení pro spouštěcí PIN kódy Samsung KNOX<!--1087143-->
Pokud koncoví uživatelé na zařízeních se zabezpečením Samsung Knox potřebují nastavit spouštěcí PIN, aby vyhovoval požadavkům na šifrování, přenese je oznámení, které se zobrazí po klepnutí, přímo na místo v aplikaci Nastavení.  Dříve oznámení odkázalo koncové uživatele na obrazovku pro změnu hesla.

### <a name="device-enrollment"></a>Registrace zařízení

#### <a name="apple-school-manager-asm-support-with-shared-ipad---748864-770395--"></a>Podpora Apple School Manageru (ASM) se sdíleným iPadem<!-- 748864, 770395-->

Pro první registraci zařízení s iOSem teď Intune místo programu Apple Device Enrollment Program podporuje použití Apple School Manageru (ASM). K použití aplikace Classroom pro sdílené iPady a k povolení synchronizace dat z ASM do Azure Active Directory prostřednictvím služby Synchronizace školních dat Microsoftu se vyžaduje zprovoznění ASM. Další informace najdete v tématu [Povolení registrace zařízení s iOSem pomocí Apple School Manageru](../enrollment/apple-school-manager-set-up-ios.md).

> [!NOTE]
> Konfigurace fungování sdílených iPadů s aplikací Classroom vyžaduje konfigurace iOS Education v Azure, které ještě nejsou k dispozici.  Tato funkce bude brzy přidána.

### <a name="device-management"></a>Správa zařízení

#### <a name="provide-remote-assistance-to-android-devices-using-teamviewer---675418---"></a>Poskytnutí vzdálené pomoci pro zařízení s Androidem pomocí TeamVieweru<!-- 675418 -->

Intune vám teď pomocí softwaru [TeamViewer](https://www.teamviewer.com), který se prodává zvlášť, umožňuje poskytovat vzdálenou pomoc uživatelům používajícím zařízení s Androidem. Další informace najdete v článku o [poskytování vzdálené pomoci pro zařízení s Androidem, která se spravují přes Intune](../remote-actions/teamviewer-support.md).

### <a name="app-management"></a>Správa aplikací

#### <a name="new-app-protection-policies-conditions-for-mam---679864---"></a>Nové podmínky zásad ochrany aplikací pro MAM<!-- 679864 -->

Teď můžete nastavit požadavek pro MAM bez uživatelů registrace, který vynucuje tyto zásady:

- Minimální verzi aplikací
- Minimální verzi operačního systému
- Minimální verzi Intune APP SDK cílové aplikace (pouze iOS)

Tato funkce je k dispozici pro Android i iOS. Intune podporuje vynucení minimální verze pro verze platformy OS, verze aplikací a Intune APP SDK. V iOSu můžou aplikace s integrovanou sadou SDK také nastavit vynucení minimální veze na úrovni SDK. Pokud nebudou splněny minimální požadavky prostřednictvím zásad ochrany aplikace na třech různých úrovních uvedených výše, uživatel nebude moct k cílové aplikaci přistupovat. Uživatel teď může odebrat svůj účet (pro aplikace s více identitami), zavřít aplikaci nebo aktualizovat verzi operačního systému nebo aplikace.

Můžete také nakonfigurovat další nastavení, abyste poskytovali neblokující oznámení, které bude doporučovat upgrade operačního systému nebo aplikace. Toto oznámení se dá zavřít a aplikace se dá používat jako obvykle.

Další informace najdete v [Nastavení zásad ochrany aplikací pro iOS](../apps/app-protection-policy-settings-ios.md) a [Nastavení zásad ochrany aplikací pro Android](../apps/app-protection-policy-settings-android.md).

#### <a name="configure-app-configurations-for-android-for-work---621621---"></a>Konfigurace konfigurace aplikací pro Android for Work<!-- 621621 -->
Některé aplikace pro Android z obchodu podporují možnosti spravované konfigurace, které správci IT umožňují řídit, jak aplikace běží v pracovním profilu. S Intune teď můžete zobrazit konfigurace podporované aplikací a nakonfigurovat je z Azure Portalu pomocí návrháře konfigurace nebo editoru JSON. Další informace najdete v článku o [používání konfigurací aplikací pro Android for Work](../apps/app-configuration-policies-use-android.md).

#### <a name="new-app-configuration-capability-for-mam-without-enrollment---677969---"></a>Nová možnost konfigurace aplikací pro MAM bez registrace<!-- 677969 -->
Teď můžete vytvářet zásady konfigurace aplikací prostřednictvím MAM bez kanálu registrace. Tato funkce je ekvivalentní zásadám konfigurace aplikací dostupným v konfiguraci aplikací ve správě mobilních zařízení (MDM). Příklad konfigurace aplikací pomocí MAM bez registrace najdete v článku o [správě přístupu k internetu pomocí zásad Managed Browseru v Microsoft Intune](../apps/app-configuration-managed-browser.md).

#### <a name="configure-allowed-and-blocked-url-lists-for-the-managed-browser---682960---"></a>Konfigurace povolených a blokovaných seznamů adres URL pro Managed Browser<!-- 682960 -->
Teď můžete nakonfigurovat seznam povolených a blokovaných domén a adres URL pro Intune Managed Browser pomocí nastavení konfigurace aplikací na portálu Azure Portal. Tato nastavení jde nakonfigurovat bez ohledu na to, jestli se používá na spravovaném nebo nespravovaném zařízení. Další informace najdete v článku o [správě přístupu k internetu pomocí zásad Managed Browseru v Microsoft Intune](../apps/app-configuration-managed-browser.md).

#### <a name="app-protection-policy-helpdesk-view---1069473---"></a>Zobrazení helpdesku zásady ochrany aplikací<!-- 1069473 -->
Uživatelé IT Helpdesku teď můžou zkontrolovat stav licencí uživatelů a stav zásad ochrany aplikací přiřazených uživatelům v okně Řešení potíží. Podrobnosti najdete v tématu o [řešení potíží](./help-desk-operators.md).

### <a name="device-configuration"></a>Konfigurace zařízení

#### <a name="control-website-visits-on-ios-devices---723832---"></a>Řízení návštěv webu na zařízeních s iOS<!-- 723832 -->
Můžete teď řídit, které webové stránky můžou uživatelé zařízení s iOSem navštívit, a to pomocí jedné z těchto dvou metod:

- Přidejte povolené a blokované adresy URL pomocí integrovaného filtru webového obsahu od společnosti Apple.

- Povolte přístup z prohlížeče Safari jenom k určeným webovým stránkám. V Safari se vytvoří záložky pro weby, které určíte.

Další informace najdete v článku o [nastavení filtru webového obsahu pro zařízení s iOSem](../configuration/ios-device-features-settings.md#web-content-filter).

#### <a name="preconfigure-device-permissions-for-android-for-work-apps---621614---"></a>Předem nakonfigurovat oprávnění zařízení pro aplikace pro Android for Work<!-- 621614 -->
U aplikací nasazených do pracovních profilů zařízení Android for Work můžete teď nakonfigurovat stav oprávnění pro jednotlivé aplikace.  Aplikace pro Android, které vyžadují oprávnění zařízení, jako je například přístup k umístění nebo fotoaparátu zařízení, ve výchozím nastavení vyzvou uživatele, aby oprávnění přijali nebo odmítli.  Pokud například aplikace používá mikrofon zařízení, potom bude koncový uživatel vyzván, aby aplikaci udělil oprávnění používat mikrofon. Tato funkce umožňuje definovat oprávnění jménem koncového uživatele.  Můžete nakonfigurovat oprávnění k a) automatickému odmítnutí bez upozornění uživatele, b) automatickému schválení bez upozornění uživatele nebo c) vyzvání uživatele k přijmutí nebo odmítnutí. Další informace najdete v článku [Nastavení omezení pro zařízení s Androidem for Work v Microsoft Intune](../configuration/device-restrictions-android-for-work.md).

#### <a name="define-app-specific-pin-for-android-for-work-devices---728976-1102534---"></a>Definovat PIN kód pro zařízení s Androidem for Work specifický pro aplikaci<!-- 728976, 1102534 -->
Zařízení s Androidem 7.0 a vyšším s pracovním profilem spravovaným jako zařízení s Androidem for Work umožňují správci definovat zásady hesla, které se vztahují jenom na aplikace v pracovním profilu.  Vaše možnosti jsou:

- Definovat jenom zásady hesla pro celé zařízení – jedná se o heslo, které musí uživatel používat k odemknutí celého zařízení.
- Definovat jenom zásady hesla pracovního profilu – uživatelé budou vyzváni k zadání hesla při každém otevření jakékoli aplikace v pracovním profilu.
- Definovat zásady hesla pro zařízení i pro pracovní profil – správce IT má možnost definovat zásady hesla zařízení a pracovního profilu o různé síle (třeba čtyřmístný PIN kód pro odemknutí zařízení a šestimístný PIN kód pro otevření libovolné pracovní aplikace).

Další informace najdete v článku [Nastavení omezení pro zařízení s Androidem for Work v Microsoft Intune](../configuration/device-restrictions-android-for-work.md).

> [!NOTE]
> Tyto možnosti jsou k dispozici jenom u Androidu 7.0 a vyššího.  Ve výchozím nastavení může koncový uživatel použít dva samostatně definované PIN kódy, nebo se může rozhodnout zkombinovat tyto dva nadefinované PIN kódy do silnějšího z nich.

#### <a name="new-settings-for-windows-10-devices---978585---"></a>Nová nastavení pro zařízení s Windows 10<!-- 978585 -->
Přidali jsme nová [nastavení omezení zařízení s Windows](../configuration/device-restrictions-windows-10.md), která řídí funkce, jako jsou bezdrátové displeje, zjišťování zařízení, přepínání úloh a chybové zprávy SIM karet.

#### <a name="updates-to-certificate-configuration---918991-and-823198---"></a>Aktualizace konfigurace certifikátu<!-- 918991 and 823198 -->
Při vytváření profilu certifikátu SCEP je pro <strong>Formát názvu subjektu</strong> dostupná možnost <strong>Vlastní</strong> pro zařízení s iOSem, Androidem a Windows. Před touto aktualizací bylo pole <strong>Vlastní</strong> k dispozici jenom pro zařízení s iOSem. Další informace najdete v tématu [Vytvoření profilu certifikátu SCEP](../protect/certificates-profile-scep.md).

Při vytváření profilu certifikátu PKCS je pro **Alternativní název subjektu** dostupná možnost **Vlastní atribut Azure AD**. Když vyberete **Vlastní atribut Azure AD**, je dostupná možnost **Oddělení**. Další informace najdete v tématu [Vytvoření profilu certifikátu PKCS](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile).

#### <a name="configure-multiple-apps-that-can-run-when-an-android-device-is-in-kiosk-mode---662059---"></a>Konfigurace více aplikací, které se dají spustit, když je zařízení s Androidem v celoobrazovkovém režimu<!-- 662059 -->
Když je zařízení s Androidem v režimu veřejného terminálu, mohli jste dřív konfigurovat jenom jednu aplikaci, která mohla být spuštěná. Teď můžete konfigurovat víc aplikací pomocí ID aplikace, adresy URL obchodu nebo výběrem aplikace pro Android, kterou už spravujete. Další informace najdete v tématu o [nastavení režimu veřejného terminálu (kiosku)](../configuration/device-restrictions-android.md#kiosk).

<!-- ########################## -->
## <a name="april-2017"></a>Duben 2017

### <a name="support-for-managing-the-apple-classroom-app"></a>Podpora správy aplikace Apple Classroom
Na iPadech teď můžete spravovat aplikaci Classroom pro iOS. Nainstalujte aplikaci Classroom na iPady učitelů se správnými údaji o předmětu a studentech, pak nakonfigurujte iPady studentů zaregistrované k předmětu, abyste je mohli pomocí této aplikace ovládat.
Podrobnosti najdete v článku [Konfigurace nastavení iOS Education](education-settings-configure-ios.md).

### <a name="support-for-managed-configuration-options-for-android-apps---621621---"></a>Podpora spravovaných možností konfigurace pro aplikace pro Android<!-- 621621 -->
Aplikace Android v obchodu Play podporující možnosti spravované konfigurace se teď dají konfigurovat pomocí Intune.  Tato funkce umožňuje IT pracovníkům zobrazit seznam hodnot konfigurace podporovaných aplikací a poskytuje prvotřídní uživatelské rozhraní s asistencí, které jim umožňuje tyto hodnoty konfigurovat.

### <a name="new-android-policy-for-complex-pins---722069---"></a>Nové zásady Androidu pro komplexní PIN kódy<!-- 722069 -->
V profilu zařízení s Androidem 5.0 a vyšším teď můžete nastavit požadovaný typ [hesla](../configuration/device-restrictions-android.md#password) na Číselné komplexní.  Pomocí tohoto nastavení můžete uživatelům zařízení zabránit ve vytvoření PINu, který obsahuje opakující se nebo po sobě jdoucí čísla jako 1111 nebo 1234.

### <a name="additional-support-for-android-for-work-devices"></a>Další podpora pro zařízení s Androidem for Work
- **Správa nastavení hesla a pracovního profilu**<!-- 612808 -->

  Tato nová zásada omezení pro zařízení s Androidem for Work vám teď umožní spravovat nastavení hesla a pracovního profilu na zařízeních s Androidem for Work, která spravujete.

- **Povolit sdílení dat mezi pracovními a osobními profily**<!-- 1045102 -->

Tento profil pro omezení zařízení s Androidem for Work teď obsahuje nové možnosti, které vám pomůžou nakonfigurovat sdílení dat mezi pracovním a osobním profilem.

- **Omezit kopírování a vkládání mezi pracovními a osobními profily**<!-- 1046094 -->

  Nový vlastní profil zařízení pro zařízení s Androidem for Work teď umožňuje zakázat akce Kopírovat a Vložit mezi pracovními a osobními aplikacemi.

Další informace najdete v tématu o [omezeních zařízení pro Android for Work](../configuration/device-restrictions-android-for-work.md).

### <a name="assign-lob-apps-to-ios-and-android-devices---1057568---"></a>Přiřazení obchodních aplikací k zařízením s iOS a Androidem<!-- 1057568 -->
Uživatelům nebo zařízením teď můžete přiřadit obchodní aplikace pro [iOS](../apps/lob-apps-ios.md) (soubory .ipa) a [Android](../apps/lob-apps-android.md) (soubory .apk).


### <a name="new-device-policies-for-ios---723774-723815-723826-723830---"></a>Nové zásady pro zařízení s iOS<!-- 723774, 723815, 723826, 723830 -->
- **Aplikace na ploše** – určuje, které aplikace uživatelé uvidí na [ploše svého zařízení s iOSem](../configuration/ios-device-features-settings.md#home-screen-layout). Tato zásada změní rozložení plochy, ale nenasadí žádné aplikace.

- **Připojení k zařízením AirPrint** – určuje, ke kterým [zařízením AirPrint](../configuration/ios-device-features-settings.md#airprint) (síťovým tiskárnám) se můžou koncoví uživatelé zařízení s iOSem připojit.

- **Připojení k zařízením AirPlay** – určuje, ke kterým [zařízením AirPlay](../configuration/ios-device-features-settings.md) (jako Apple TV) se můžou koncoví uživatelé zařízení s iOSem připojit.

- **Vlastní zpráva na zamčené obrazovce** – nakonfigurujte vlastní zprávu, která se zobrazí uživatelům na zamčené obrazovce jejich zařízení s iOSem místo výchozí zprávy. Další informace najdete v tématu [Aktivace režimu ztráty u zařízení s iOSem](../remote-actions/device-lost-mode.md)

### <a name="restrict-push-notifications-for-ios-apps---723767---"></a>Omezení nabízených oznámení pro aplikace pro iOS<!-- 723767 -->
V profilu omezení zařízení Intune teď můžete nakonfigurovat tato [nastavení oznámení](../configuration/ios-device-features-settings.md#app-notifications) pro zařízení s iOSem:

- Úplně zapnout nebo vypnout oznámení pro konkrétní aplikaci
- Zapnut nebo vypnout oznámení v centru oznámení pro konkrétní aplikaci
- Určit typ upozornění, a to buď **žádné**, **banner** nebo **modální upozornění**
- Určit, jestli jsou pro tuto aplikaci povolené odznaky
- Určit, jestli jsou povolené zvuky oznámení

### <a name="configure-ios-apps-to-run-in-single-app-mode-autonomously---737837---"></a>Konfigurace aplikací pro iOS tak, aby se spouštěly samostatně v režimu jedné aplikace<!-- 737837 -->
Pomocí profilu zařízení Intune teď můžete nakonfigurovat, aby zařízení s iOSem spouštěla zadané aplikace v [autonomním režimu jedné aplikace](../configuration/device-restrictions-ios.md#autonomous-single-app-mode). Pokud je tento režim nakonfigurovaný a uživatel spustí aplikaci, v zařízení se zablokuje spuštění jakékoli další aplikace. Příkladem je nakonfigurování aplikace, která uživatelům umožňuje absolvovat na zařízení test. Když se akce aplikace dokončí nebo tuto zásadu odeberete, zařízení se vrátí do normálního stavu.

### <a name="configure-trusted-domains-for-email-and-web-browsing-on-ios-devices---723765---"></a>Konfigurace důvěryhodných domén pro e-mail a procházení webu na zařízeních s iOS<!-- 723765 -->
V profilu omezení zařízení s iOSem teď můžete nakonfigurovat tato [nastavení domén](../configuration/device-restrictions-ios.md#domains):

- **Zrušit označení e-mailových domén** – E-maily, které uživatel posílá nebo přijímá a které neodpovídají doménám zadaným tady, se označí jako nedůvěryhodné.

- **Spravované webové domény** – Dokumenty stažené z adres URL, které zadáte tady, se budou považovat za spravované (jenom Safari).  

- **Domény pro automatické vyplňování hesel v Safari**  – Uživatelé můžou ukládat hesla v Safari jenom z adres URL odpovídajících vzorům, které tady zadáte. Pokud toto nastavení chcete použít, musí být zařízení v režimu pod dohledem a nesmí být nakonfigurované pro více uživatelů. (iOS 9.3+)


### <a name="vpp-apps-available-in-ios-company-portal---748782---"></a>Aplikace VPP dostupné v iOS Portál společnosti<!-- 748782 -->
Multilicenční aplikace (VPP) pro iOS teď můžete koncovým uživatelům přiřadit jako **Dostupné** instalace. Koncoví uživatelé budou k instalaci aplikace potřebovat účet Apple Store.

### <a name="synchronize-ebooks-from-apple-vpp-store---800878---"></a>Synchronizovat e-knihy z Apple VPP Storu<!-- 800878 -->
Pomocí Intune můžete [synchronizovat knihy](../apps/vpp-apps-ios.md), které jste zakoupili z Apple Storu v rámci multilicenčního programu, a přiřadit je uživatelům.

### <a name="multi-user-management-for-samsung-knox-standard-devices---971988---"></a>Správa více uživatelů pro zařízení se Samsung KNOX standardem<!-- 971988 -->
U zařízení, která používají Samsung Knox Standard, je teď v Intune podporovaná [správa více uživatelů](../enrollment/android-enroll.md). To znamená, že koncoví uživatelé se můžou přihlašovat a odhlásit ze zařízení pomocí přihlašovacích údajů Azure Active Directory a zařízení je centrálně spravované bez ohledu na to, jestli se používá.  Když se koncoví uživatelé přihlásí, mají přístup k aplikacím a také se na ně vztahují všechny zásady. Po odhlášení uživatelů se všechna data aplikací vymažou.

### <a name="additional-windows-device-restriction-settings---818566---"></a>Další nastavení omezení pro zařízení s Windows<!-- 818566 -->
Přidali jsme podporu dalších [Nastavení omezení pro zařízení s Windows](../configuration/device-restrictions-windows-10.md) , jako je další podpora prohlížeče Microsoft Edge, přizpůsobení zamykací obrazovky zařízení, přizpůsobení nabídky Start, Tapeta sady vyhledávání ve Windows Spotlight a nastavení proxy serveru.

### <a name="multi-user-support-for-windows-10-creators-update---822547---"></a>Podpora více uživatelů pro Windows 10 Creators Update<!-- 822547 -->
Přidali jsme podporu [správy více uživatelů](../enrollment/windows-enroll.md) pro zařízení s Windows 10 Creators Updatem připojená k doméně Azure Active Directory. To znamená, že když se k zařízení přihlásí různí standardní uživatelé pomocí svých přihlašovacích údajů Azure AD, dostanou všechny aplikace a zásady přiřazené k jejich uživatelskému jménu. Uživatelé v současnosti nemůžou používat Portál společnosti pro samoobslužné scénáře, například instalování aplikací.

### <a name="fresh-start-for-windows-10-pcs---1004830---"></a>Nové spuštění pro počítače s Windows 10<!-- 1004830 -->
K dispozici je teď nová [akce zařízení Začít znovu](../remote-actions/device-fresh-start.md) pro počítače s Windows 10.  Když tuto akci provedete, odeberou se všechny aplikace, které byly v počítači PC nainstalované, a počítač PC se automaticky aktualizuje na nejnovější verzi Windows. To se dá využít k odebrání aplikací předem nainstalovaných výrobcem, které se často dodávají s novým počítačem PC. Můžete nakonfigurovat, jestli se při provedení této akce mají zachovat uživatelská data.

### <a name="additional-windows-10-upgrade-paths---903672---"></a>Další způsoby upgradu Windows 10<!-- 903672 -->
Vytvořením [zásad upgradu edice teď můžete zařízení upgradovat](../configuration/edition-upgrade-configure-windows-10.md) na následující další edice Windows 10:

- Windows 10 Professional
- Windows 10 Professional N
- Windows 10 Professional Education
- Windows 10 Professional Education N

### <a name="bulk-enroll-windows-10-devices---747607---"></a>Hromadná registrace zařízení s Windows 10<!-- 747607 -->
K Azure Active Directory a Intune můžete teď pomocí Windows Configuration Designeru (WCD) připojit velký počet zařízení s Windows 10 Creators Updatem. Pokud chcete pro svého tenanta Azure AD povolit [hromadnou registraci MDM](../enrollment/windows-bulk-enroll.md), vytvořte zřizovací balíček, který zařízení k tenantovi Azure AD připojí pomocí Windows Configuration Designeru, a použijte balíček na zařízení ve vlastnictví firmy, která chcete hromadně zaregistrovat a spravovat. Po použití balíčku na vaše zařízení se připojí k Azure AD, zaregistrují se v Intune a budou připravení pro uživatele Azure AD, aby se přihlásili.  Uživatelé Azure AD jsou na těchto zařízeních standardními uživateli a obdrží přiřazené zásady a požadované aplikace. Samoobslužné scénáře a scénáře s Portálem společnosti v současnosti nejsou podporované.

### <a name="new-mam-settings-for-pin-and-managed-storage-locations---581122-736644---"></a>Nové nastavení MAM pro PIN a spravovaná umístění úložiště<!-- 581122, 736644 -->
K dispozici jsou teď dvě nová nastavení aplikací, která vám pomůžou se scénáři správy mobilních aplikací (MAM):

- **Zakázat PIN kód aplikace, když je PIN kód zařízení spravovaný** – zjistí, jestli se na zaregistrovaném zařízení nachází PIN zařízení, a pokud ano, obchází PIN aplikace aktivovaný zásadami ochrany aplikací. Toto nastavení umožní snížit počet případů, kdy se uživatelům při spuštění aplikace s povolenou správou mobilních zařízení na zaregistrovaném zařízení zobrazí výzva k zadání PINu. Tato funkce je k dispozici pro Android i iOS.

- **Vyberte, do kterých služeb úložiště se můžou ukládat firemní data** – umožňuje určit umístění úložiště, do kterých se můžou ukládat firemní data. Uživatelé můžou ukládat do zvolených služeb umístění úložiště, takže všechny ostatní služby umístění úložiště, které nejsou uvedené, budou zablokované.

  Seznam podporovaných služeb umístění úložiště:

  - OneDrivu
  - Business SharePoint Online
  - Místní úložiště

### <a name="help-desk-troubleshooting-portal---907448---"></a>Portál helpdesku pro řešení potíží<!-- 907448 -->
Nový [portál pro řešení potíží](help-desk-operators.md) umožňuje operátorům helpdesku a správcům Intune zobrazit uživatele a jejich zařízení a provádět úlohy k vyřešení technických problémů Intune.

<!-- ########################## -->
## <a name="march-2017"></a>Březen 2017

### <a name="support-for-ios-lost-mode--431695--"></a>Podpora režimu ztráty iOS<!--431695-->
Pro zařízení s iOSem 9.3 nebo novějším je v Intune přidaná podpora pro **režim ztráty**. Teď máte možnost zařízení uzamknout, aby se nedalo používat, a na jeho zamykací obrazovce zobrazit zprávu a kontaktní telefonní číslo.

Koncový uživatel nebude moct zařízení odemknout, dokud správce režim ztráty nevypne. Když je režim ztráty zapnutý, můžete pomocí akce **Najít zařízení** zobrazit zeměpisnou polohu zařízení na mapě v konzole Intune.

Musí se jednat o zařízení s iOSem ve vlastnictví firmy, které je zaregistrované prostřednictvím programu DEP a je v režimu dohledu.

Další informace najdete v článku [Co je správa zařízení v Microsoft Intune](../remote-actions/device-management.md).

### <a name="improvements-to-device-actions-report--677150--"></a>Vylepšení sestavy akcí zařízení<!--677150-->
Provedli jsme vylepšení sestavy akcí zařízení za účelem zvýšení výkonu. Tuto sestavu teď navíc můžete filtrovat podle stavu. Sestavu můžete například filtrovat tak, aby zobrazovala pouze akce zařízení, které byly dokončeny. "

### <a name="custom-app-categories--748805--"></a>Vlastní kategorie aplikací<!--748805-->
Teď můžete vytvářet, upravovat a přiřazovat kategorie pro aplikace, které přidáte do Intune. V současné době se kategorie dají zadávat jenom v angličtině.
Přečtěte si téma [Jak přidat aplikaci do Intune](../apps/apps-add.md).

### <a name="assign-lob-apps-to-users-with-unenrolled-devices--748823--"></a>Přiřazení obchodních aplikací uživatelům s nezaregistrovanými zařízeními<!--748823-->
Obchodní aplikace a aplikace z obchodu teď můžete přiřazovat bez ohledu na to, jestli zařízení jsou, nebo nejsou zaregistrovaná do Intune. Pokud zařízení uživatele není zaregistrované v Intune, musí kvůli jeho instalaci přejít na web Portál společnosti, ne do aplikace Portál společnosti.

### <a name="new-compliance-reports--846671--"></a>Nové sestavy dodržování předpisů<!--846671-->
Teď máte k dispozici sestavy dodržování předpisů, ze kterých zjistíte, nakolik zařízení ve firmě dodržují předpisy, a které vám pomůžou rychle vyřešit problémy uživatelů související s dodržováním předpisů. Můžete zjistit:

- Celkový stav dodržování předpisů zařízeními
- Stav dodržování předpisů pro individuální nastavení
- Stav dodržování předpisů pro individuální zásadu

Tyto sestavy vám také umožňují přejít až k individuálnímu zařízení a zobrazit konkrétní nastavení a zásady, které se tohoto zařízení týkají.

<!--- You can now create an edition upgrade policy to upgrade devices to the following additional Windows 10 editions:

- Windows 10 Professional
- Windows 10 Professional N
- Windows 10 Professional Education
- Windows 10 Professional Education N --->

### <a name="direct-access-to-apple-enrollment-scenarios--951869--"></a>Přímý přístup ke scénářům registrace Apple<!--951869-->
U účtů Intune vytvořených po lednu 2017 umožňuje Intune přímý přístup ke scénářům registrace Apple pomocí úlohy Registrovat zařízení na portálu Azure Portal. Náhled na registraci Apple byl předtím přístupný jen přes odkazy na Azure Portalu. Zpřístupnění těchto funkcí v Azure bude u účtů Intune vytvořených před lednem 2017 vyžadovat jednorázovou migraci. Plán této migrace zatím nebyl oznámen, podrobnosti ale budou zpřístupněny co nejdříve. Pokud váš existující účet nemá k tomuto náhledu přístup, k otestování tohoto nového prostředí důrazně doporučujeme vytvořit zkušební účet.


<!-- ########################## -->
## <a name="february-2017"></a>Únor 2017

### <a name="ability-to-restrict-mobile-device-enrollment--747600-795782--"></a>Možnost omezit registraci mobilního zařízení<!--747600, 795782-->
Intune přidává nová omezení registrace řídící to, které platformy mobilních zařízení se mohou zaregistrovat. Intune odděluje platformy mobilních zařízení, jako je iOS, macOS, Android, Windows a Windows Mobile.

- Omezení registrace mobilních zařízení neomezuje registraci klienta pro počítače.  
- Pouze pro iOS a Android existuje další možnost blokování registrace osobních zařízení.

Pokud správce IT neoznačí nová zařízení jako vlastněná podnikem, Intune všechna nová zařízení označí jako osobní. Podrobnosti najdete v [tomto článku](../enrollment/device-enrollment.md).

### <a name="view-all-actions-on-managed-devices--677150--"></a>Zobrazit všechny akce na spravovaných zařízeních<!--677150-->
V nové sestavě __Akce zařízení__ se zobrazí, kdo provedl vzdálené akce, jako je obnovení továrního nastavení zařízení, a dále stav dané akce. Viz [Co je správa zařízení?](../remote-actions/device-management.md)

### <a name="non-managed-devices-can-access-assigned-apps--664691--"></a>Nespravovaná zařízení mají přístup k přiřazeným aplikacím.<!--664691-->
Jako součást změn v návrhu na webu Portál společnosti budou moci uživatelé iOSu a Androidu na svoje nespravovaná zařízení instalovat aplikace, které mají přiřazené jako dostupné bez registrace. S použitím přihlašovacích údajů pro Intune se budou moct uživatelé přihlásit na web Portál společnosti a zobrazit seznam aplikací, které mají přiřazené. Balíčky aplikací, které jsou dostupné bez registrace, jsou k dispozici ke stažení prostřednictvím webu Portál společnosti. Aplikace, které vyžadují registraci, aby je bylo možné nainstalovat, nejsou touto změnou ovlivněny, protože když budou chtít tyto aplikace uživatelé nainstalovat, zobrazí se jim výzva k registraci.

### <a name="custom-app-categories--748805--"></a>Vlastní kategorie aplikací<!--748805-->
Teď můžete vytvářet, upravovat a přiřazovat kategorie pro aplikace, které přidáte do Intune. V současné době se kategorie dají zadávat jenom v angličtině.
Přečtěte si téma [Jak přidat aplikaci do Intune](../apps/apps-add.md).

### <a name="display-device-categories--814654--"></a>Zobrazit kategorie zařízení<!--814654-->
Kategorie zařízení teď můžete zobrazit jako sloupec v seznamu zařízení. Kategorii můžete upravit také v části vlastností v okně vlastností zařízení. Přečtěte si téma [Jak přidat aplikaci do Intune](../apps/apps-add.md).

### <a name="configure-windows-update-for-business-settings--776716--"></a>Konfigurace nastavení web Windows Update pro firmy<!--776716-->

Windows jako služba představuje nový způsob poskytování aktualizací pro Windows 10. Od verze Windows 10 budou všechny nové aktualizace funkcí a aktualizace pro zvýšení kvality zahrnovat obsah všech předchozích aktualizací. To znamená, že pokud si nainstalujete nejnovější aktualizaci, máte jistotu, že jsou vaše zařízení s Windows 10 zcela aktuální. Na rozdíl od předchozích verzí Windows je teď nutné nainstalovat celou aktualizaci (a ne jenom její část).

Pomocí web Windows Update pro firmy můžete zjednodušit možnosti správy aktualizací, abyste nemuseli schvalovat jednotlivé aktualizace pro skupiny zařízení. Můžete nakonfigurovat strategii zavádění aktualizací, abyste měli pod kontrolou řízení rizik ve vašem prostředí, a služba Windows Update zajistí, aby se aktualizace nainstalovaly ve správný čas. Prostřednictvím Microsoft Intune můžete na zařízeních nakonfigurovat nastavení aktualizací a pozdržet instalaci aktualizací. Intune aktualizace neukládá, ale pouze přiřazení zásad aktualizace. Zařízení získávají aktualizace přímo ze služby Windows Update. Pomocí Intune můžete nakonfigurovat a spravovat **aktualizační kanály Windows 10**. Aktualizační kanál obsahuje skupinu nastavení, která konfigurují, kdy a jak se budou aktualizace Windows 10 instalovat. Podrobnosti najdete v článku [Konfigurace nastavení služby Windows Update pro firmy](../protect/windows-update-for-business-configure.md).
