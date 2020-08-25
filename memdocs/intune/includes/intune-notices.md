---
title: zahrnout soubor
description: zahrnout soubor
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 7027eac119ef36adfdb9a0057a74d276696620b3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820052"
---
Tato oznámení obsahují důležité informace, které vám pomůžou připravit se na budoucí změny a funkce Intune.

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Microsoft Intune ukončí podporu pro Windows Phone 8,1 a Windows 10 Mobile.<!-- 3544938, 3544909 -->
Hlavní podpora společnosti Microsoft pro Windows Phone 8,1 skončila v červenci 2017 a rozšířená podpora skončila v červnu 2019. Aplikace Portál společnosti pro Windows Phone 8,1 byla v režimu Sustained od října 2017. Kromě toho Microsoft Intune od 20. února 2020 pro Windows Phone 8,1 skončila podpora. 

Hlavní podpora Microsoftu pro Windows 10 Mobile skončila v prosinci 2019. Jak je uvedeno v příkazu podpory, uživatelé s Windows 10 Mobile už nebudou mít nárok na přijímání nových aktualizací zabezpečení, oprav hotfix bez zabezpečení, bezplatné podpory s asistencí nebo online aktualizace obsahu od Microsoftu. V závislosti na podpoře všech mobilních operačních systémů Microsoft Intune ukončí podporu jak pro Portál společnosti mobilní aplikace pro Windows 10, tak i pro mobilní operační systém Windows 10 od 10. srpna 2020.

Od 10. srpna se registrace pro Windows Phone 8,1 a zařízení s Windows 10 Mobile nezdaří a z uživatelského rozhraní Intune se odeberou typy profilů Windows Mobile. Zařízení, která jsou už zaregistrovaná, už nebudou kontrolovat službu Intune a odstraníme data zařízení a zásad.

### <a name="end-of-support-for-legacy-pc-management"></a>Konec podpory pro správu starších počítačů

Podpora starší verze správy počítačů od 15. října 2020. Upgradujte zařízení na Windows 10 a znovu je zaregistrujte jako zařízení pro správu mobilních zařízení (MDM), abyste je mohli spravovat přes Intune.

[Další informace](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Přejděte do centra pro správu Microsoft Endpoint Manageru pro veškerou správu Intune.
V MC208118 zveřejněné poslední březen jsme představili novou jednoduchou adresu URL pro správu Microsoft Endpoint Manageru – Intune: [https://endpoint.microsoft.com](https://endpoint.microsoft.com) . Microsoft Endpoint Manager je jednotná platforma, která zahrnuje Microsoft Intune a Configuration Manager. **Od 1. srpna 2020**odebereme správu Intune na [https://portal.azure.com](https://portal.azure.com) místo toho, abyste ho použili [https://endpoint.microsoft.com](https://endpoint.microsoft.com) pro celou správu koncových bodů. 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Snížení podpory pro správce zařízení s Androidem<!--7371518-->
Správa Správce zařízení s Androidem byla vydaná v Androidu 2,2 jako způsob správy zařízení s Androidem. Od verze Android 5 byla vydaná pokročilejší architektura pro správu [Androidu Enterprise](../enrollment/connect-intune-android-enterprise.md) (pro zařízení, která se můžou spolehlivě připojit k Google Mobile Services). Google podporuje pohyb správy správců zařízení tím, že snižuje podporu správy v nových verzích Androidu.

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?
Z důvodu těchto změn od společnosti Google už v říjnu 2020 nebudete mít k dispozici rozsáhlé možnosti správy na zařízeních spravovaných správcem zařízení, která mají vliv na správu. 

> [!NOTE]
> Toto datum bylo dříve sděleno jako čtvrté čtvrtletí 2020, ale bylo přesunuto na základě [nejnovějších informací z Google](https://www.blog.google/products/android-enterprise/da-migration/).

##### <a name="device-types-that-will-be-impacted"></a>Typy zařízení, které budou mít vliv na
Zařízení, na která bude mít vliv podpora správce pro snižování zařízení, jsou ta, pro kterou platí všechny tři podmínky:
- Zaregistrováno v správě Správce zařízení.
- Běžící Android 10 nebo novější.
- Nejedná se o zařízení Samsung.

Tato zařízení nebudou mít vliv, pokud jsou některá z následujících:
- Není zaregistrované v rámci správy správců zařízení.
- S verzí Androidu nižší než Android 10.
- Zařízení Samsung V tomto období nebude mít vliv na zařízení Samsung KNOX, protože prostřednictvím integrace Intune s platformou Knox je zajištěná Rozšířená podpora. Tím získáte další čas k naplánování přechodu mimo správu Správce zařízení pro zařízení Samsung.

##### <a name="settings-that-will-be-impacted"></a>Nastavení, které bude mít vliv na
[Snížení podpory správců zařízení ve službě Google](https://developers.google.com/android/work/device-admin-deprecation) brání v použití konfigurace těchto nastavení na ovlivněných zařízeních.

###### <a name="configuration-profile-device-restriction-settings"></a>Nastavení omezení pro zařízení konfiguračního profilu

- Blokovat **kameru**
- Nastavit **minimální délku hesla**
- Nastavit **počet neúspěšných přihlášení před vymazáním zařízení** (nebude se vztahovat na zařízení bez nastaveného hesla, ale bude platit na zařízeních s heslem)
- Nastavit **vypršení platnosti hesla (dny)**
- Nastavit **požadovaný typ hesla**
- Nastavení **zabránit použití předchozích hesel**
- Blokování **Smart Lock a dalších agentů** pro určování důvěryhodnosti

###### <a name="compliance-policy-settings"></a>Nastavení zásad dodržování předpisů

- Nastavit **požadovaný typ hesla**
- Nastavit **minimální délku hesla**
- Nastavit **počet dní do vypršení platnosti hesla**
- Nastavte **počet předchozích hesel, aby se zabránilo opakovanému použití**


![Snímek obrazovky videa stránky zásad dodržování předpisů pro Android](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>Další dopady na základě verze operačního systému Android

**Android 10**: pro všechna zařízení spravovaná správcem zařízení (včetně Samsung) se systémem Android 10 nebo novějším má Google možnost agenti správy zařízení, jako je portál společnosti získat přístup k informacím o identifikátoru zařízení. Toto omezení má vliv na následující funkce Intune po aktualizaci zařízení na Android 10 nebo novější:
- Řízení přístupu k síti pro VPN už nebude fungovat.
- Označení zařízení jako vlastněných společností pomocí IMEI nebo sériového čísla nebudou automaticky označovat zařízení jako ve vlastnictví firmy.
- IMEI a sériové číslo se už nebudou zobrazovat správcům IT v Intune.

**Android 11**: v současnosti testujeme podporu Androidu 11 na nejnovější verzi beta verze pro vývojáře, která vám pomůže vyhodnotit, jestli to způsobí dopad na zařízení spravovaná správcem zařízení.

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>Uživatelské prostředí s ovlivněným nastavením na ovlivněných zařízeních

Ovlivněná nastavení konfigurace:
- U již zaregistrovaných zařízení, která již mají použitá nastavení, se nastavení ovlivněných konfigurací bude i nadále vymáhat.
- U nově zaregistrovaných zařízení, nově přiřazených nastavení a aktualizovaných nastavení se ovlivněná nastavení konfigurace neuplatní (ale přesto se vynutilo všechna ostatní nastavení konfigurace).

Ovlivněná nastavení dodržování předpisů:
- U již zaregistrovaných zařízení, která už nastavení používala, se ovlivněná nastavení dodržování předpisů budou dál zobrazovat jako důvody pro nedodržování předpisů na stránce aktualizovat nastavení zařízení, že zařízení nedodržuje předpisy a požadavky na heslo budou v aplikaci nastavení i nadále vyplněny.
- U nově zaregistrovaných zařízení, nově přiřazených nastavení a aktualizovaných nastavení se ovlivněná nastavení dodržování předpisů budou dál zobrazovat jako důvody pro nedodržování předpisů na stránce aktualizovat nastavení zařízení a zařízení nedodržuje předpisy, ale přísnější požadavky na heslo se v aplikaci nastavení neuplatní.

#### <a name="cause-of-impact"></a>Příčina dopadu 
Na zařízení bude mít vliv v říjnu 2020. V tomto okamžiku bude k dispozici Portál společnosti aktualizace aplikace, která zvýší cílení rozhraní Portál společnosti API z úrovně 28 na úroveň 29 ([podle požadavku Google](https://www.blog.google/products/android-enterprise/da-migration/)). 

V tomto okamžiku bude mít vliv na zařízení spravovaná správcem zařízení, která nejsou vyráběná společností Samsung, jakmile uživatel dokončí obě tyto akce:
- Aktualizace pro Android 10 nebo novější.
- Aktualizuje aplikaci Portál společnosti na verzi, která cílí na úroveň rozhraní API 29.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit?
Abyste se vyhnuli omezení funkčnosti nacházejícím se v říjnu 2020, doporučujeme následující:
- **Nové registrace**: připojení nových zařízení do správy [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) Management (Pokud je k dispozici) nebo [zásad ochrany aplikací](../apps/app-protection-policies.md). Nepoužívejte registraci nových zařízení do správy Správce zařízení. 
- **Dřív zaregistrovaná zařízení**: Pokud na zařízení spravovaném správcem zařízení běží Android 10 nebo novější nebo se může aktualizovat na Android 10 nebo novější (obzvláště pokud se nejedná o zařízení Samsung), přesuňte ho od správy zařízení k [Androidu Enterprise](../enrollment/connect-intune-android-enterprise.md) managementu a/nebo [zásadám ochrany aplikací](../apps/app-protection-policies.md). Pomocí zjednodušeného toku můžete [zařízení s Androidem přesunout ze Správce zařízení do správy pracovního profilu](../enrollment/android-move-device-admin-work-profile.md).

#### <a name="additional-information"></a>Další informace
- [Přesunutí zařízení s Androidem ze Správce zařízení do správy pracovního profilu](../enrollment/android-move-device-admin-work-profile.md)
- [Nastavení registrace zařízení s pracovním profilem Android Enterprise](../enrollment/android-work-profile-enroll.md)
- [Nastavení registrace vyhrazených zařízení s Androidem Enterprise](../enrollment/android-kiosk-enroll.md)
- [Nastavení registrace zařízení se systémem Android Enterprise s plnou správou](../enrollment/android-fully-managed-enroll.md)
- [Jak vytvořit zásady ochrany aplikací pro přiřazení](../apps/app-protection-policies.md)
- [Jak používat Intune v prostředích bez Google Mobile Services](../apps/manage-without-gms.md)
- [Principy zásad ochrany aplikací a pracovních profilů na zařízeních s Androidem Enterprise](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Blog Google o tom, co potřebujete znát o vyřazení Správce zařízení za zastaralé](https://www.blog.google/products/android-enterprise/da-migration/)
- [Pokyny pro migraci ze strany správce zařízení na Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Dokumentace Google pro zastaralá rozhraní API Správce zařízení](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>Plánování změn: aktualizace toku registrace Intune pro automatické registrace zařízení společnosti Apple pro iOS/iPadOS
V červenci Portál společnosti vydání změníme tok registrace iOS/iPadOS pro automatický zápis zařízení společnosti Apple (dříve označovaný jako DEP). Změna toku registrace se objevuje jenom během toku "zapsat s přidružením uživatele". Pokud jste dřív v rámci vaší konfigurace nastavili možnost "instalovat Portál společnosti" na hodnotu Ne, uživatelé si pořád můžou nainstalovat Portál společnosti aplikaci ze Storu, která by pak mohla aktivovat registraci, do které by uživatel přidal příslušné sériové číslo. S tímto nadcházejícím Portál společnosti verzí odebereme obrazovku s potvrzením sériového čísla. Místo toho budete chtít vytvořit odpovídající zásadu konfigurace aplikace, abyste se mohli přenést vedle Portál společnosti, abyste měli jistotu, že se uživatelé můžou úspěšně zaregistrovat, nebo nastavit "instalovat Portál společnosti" na "Ano" jako součást vaší konfigurace. 
 - Další informace najdete v příspěvku [sem](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629) .
