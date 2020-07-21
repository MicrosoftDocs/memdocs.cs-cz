---
title: Při vývoji – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune funkce vývoje
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: caec61f93b3b651c18d2c4fd81467d462de75fc1
ms.sourcegitcommit: cb9b452f8e566fe026717b59c142b65f426e5033
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/20/2020
ms.locfileid: "86491231"
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

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Portál společnosti přidává podporu aplikací Configuration Manager<!-- 4297660 -->
Portál společnosti teď podporuje Configuration Manager aplikace. Tato funkce umožňuje koncovým uživatelům zobrazit Configuration Manager i aplikace nasazené v Intune v Portál společnosti pro spoluspravované zákazníky. Tato podpora pomůže správcům konsolidovat různé prostředí portálu pro koncové uživatele. Další informace najdete v tématu [použití portál společnosti aplikace na spoluspravovaných zařízeních](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Konfigurace zařízení

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Nastavit stav dodržování předpisů zařízením od partnerů MDM třetích stran<!-- 6361689   -->
Microsoft 365 zákazníci, kteří vlastní řešení MDM třetí strany, budou moci vyhovět zásadám podmíněného přístupu pro aplikace Microsoft 365 v iOS a Androidu prostřednictvím integrace se službou Microsoft Intune dodržování předpisů zařízením. Dodavatel MDM třetí strany bude využívat službu Intune pro dodržování předpisů zařízením k odesílání dat o dodržování předpisů zařízením do Intune. Intune se pak vyhodnotí a určí, jestli je zařízení důvěryhodné, a nastavte atributy podmíněného přístupu ve službě Azure AD.  Zákazníci budou muset nastavit zásady podmíněného přístupu Azure AD z centra pro správu Microsoft Endpoint Manageru nebo z portálu Azure AD.  

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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nová logika sloučení pro zařízení s Windows 10<!--179048-->
Pokud se dnes zákazník znovu pokusí vytvořit kopii zařízení a pak ho znovu zaregistruje, zobrazí se v konzole pro správu Microsoft Endpoint Manageru víc záznamů pro toto zařízení. Nová logika sloučení je ve vývoji ke sloučení takových duplicitních záznamů pro zařízení s Windows 10.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Nasazení aktualizací softwaru do zařízení macOS <!-- 3194876 -->
Aktualizace softwaru budete moct nasadit do skupin zařízení macOS. Tato funkce zahrnuje kritické, firmware, konfigurační soubor a další aktualizace. V příští registraci zařízení budete moct odesílat aktualizace, nebo můžete vybrat týdenní plán pro nasazení aktualizací do nebo z časového intervalu, který jste nastavili. To pomáhá při aktualizaci zařízení mimo standardní pracovní dobu nebo v případě, že je vaše Helpdesk plně přiřazená. Zobrazí se vám také podrobná sestava všech zařízení macOS s nasazenými aktualizacemi. Pokud chcete zobrazit stav konkrétních aktualizací, můžete přejít k sestavě podle jednotlivých zařízení.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorování a odstraňování potíží

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Šablona sestavy dodržování předpisů Power BI V 2.0<!-- 636958  -->
Správci budou moct aktualizovat verzi šablony zprávy o kompatibilitě Power BI z verze 1.0 až verze 2.0. Verze 2.0 bude obsahovat vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Související informace najdete v tématu [připojení k datovému skladu pomocí Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Řízení přístupu na základě role

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Podpora značek oboru pro zásady přizpůsobení<!--6182440 -->
Budete moct přiřadit značky oboru k zásadám přizpůsobení. Provedete to tak, že přejdete do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Tenant administration** >  **přizpůsobení** , kde se zobrazí možnosti konfigurace **značky oboru** .

<!-- ***********************************************-->
## <a name="security"></a>Zabezpečení

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Podpora zásad ochrany aplikací pro Symantec Endpoint Security a Check Point Sandblast<!--  4452423, 4731168 -->

V říjnu 2019 zásady ochrany aplikací Intune přidaly možnost používat data z některých našich partnerů ochrany před internetovými útoky (MTD partneři Microsoftu). Přidáváme podporu pro následující partnery, aby bylo možné použít zásady ochrany aplikací k blokování nebo selektivnímu vymazání podnikových dat uživatele na základě stavu zařízení:

- **Check Point Sandblast** v Androidu, iOS a iPadOS
- **Symantec Endpoint Security** na Androidu, iOS a iPadOS

Informace o používání zásad ochrany aplikací s partnery MTD najdete v tématu [Vytvoření zásady ochrany aplikací ochrany před mobilními hrozbami v Intune](../protect/mtd-app-protection-policy.md).


<!-- ***********************************************-->
## <a name="notices"></a>Sdělení

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Viz také

Podrobnosti o posledním vývoji najdete v tématu [co je nového v Microsoft Intune](whats-new.md).
