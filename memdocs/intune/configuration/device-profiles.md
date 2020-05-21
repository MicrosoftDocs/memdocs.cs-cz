---
title: Funkce a nastavení zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Přehled různých profilů zařízení Microsoft Intune. Získejte informace o funkcích, omezeních, e-mailu, Wi-Fi, VPN, vzdělávání, certifikátech, upgradu Windows 10, BitLockeru a programu Microsoft Defender, Windows Information Protection, šablonách pro správu a vlastním nastavení konfigurace zařízení v centru pro správu Microsoft Endpoint Manageru. Pomocí těchto profilů můžete spravovat a chránit data a zařízení ve vaší společnosti.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: aeaa184717f96def1b84447d9ded207c93d8b423
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429800"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Použití funkcí a nastavení v zařízeních pomocí profilů zařízení v Microsoft Intune

Microsoft Intune zahrnuje nastavení a funkce, které můžete povolit nebo zakázat na různých zařízeních v rámci vaší organizace. Tato nastavení a funkce se přidají do části "konfigurační profily". Můžete vytvářet profily pro různá zařízení a různé platformy, včetně iOS/iPadOS, Správce zařízení s Androidem, Androidu Enterprise a Windows. Pak pomocí Intune aplikujte nebo přiřadíte profil k zařízením.

Jako součást řešení správy mobilních zařízení (MDM) použijte tyto konfigurační profily k dokončení různých úloh. Například:

- Na zařízeních s Windows 10 použijte šablonu profilu, která blokuje ovládací prvky ActiveX v Internet Exploreru.
- V zařízeních se systémem iOS/iPadOS a macOS umožňují uživatelům používat tiskárny pro tisk ve vaší organizaci.
- Povolí nebo zakáže přístup k Bluetooth na zařízení.
- Vytvořte profil Wi-Fi nebo VPN, který poskytuje různým zařízením přístup k podnikové síti.
- Spravujte aktualizace softwaru, včetně okamžiku, kdy jsou nainstalovány.
- Spusťte zařízení s Androidem jako vyhrazené veřejné veřejné zařízení, které může spouštět jednu aplikaci nebo spouštět spoustu aplikací.

Tento článek obsahuje přehled různých typů profilů, které můžete vytvořit. Pomocí těchto profilů povolíte nebo zakážete některé funkce v zařízeních.

## <a name="administrative-templates"></a>Šablony pro správu

[Šablony pro správu](administrative-templates-windows.md) obsahují stovky nastavení, která můžete nakonfigurovat pro Internet Explorer, OneDrive, vzdálenou plochu, Word, Excel a další programy Office.

Tyto šablony poskytují správcům zjednodušené zobrazení nastavení, které se podobá zásadám skupiny, ale jsou 100% cloudu.

Tato funkce podporuje:

- Windows 10 a novější

## <a name="certificates"></a>Certifikáty

[Certifikáty](../protect/certificates-configure.md) konfigurují certifikáty Trusted, SCEP a PKCS, které jsou přiřazené k zařízením. Tyto certifikáty ověřují profily Wi-Fi, VPN a e-mailu.

Tato funkce podporuje:

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 a novější

## <a name="custom-profile"></a>Profil Vlastní

[Vlastní nastavení](custom-settings-configure.md) umožňuje správcům přiřazovat nastavení zařízení, která nejsou integrovaná do Intune. Na zařízeních s Androidem můžete zadat hodnoty OMA-URI. Pro zařízení s iOS/iPadOS můžete importovat konfigurační soubor, který jste vytvořili v Apple Configuratoru.

Tato funkce podporuje:

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1

## <a name="delivery-optimization"></a>Optimalizace doručení

[Optimalizace doručování](delivery-optimization-windows.md) nabízí lepší možnosti doručování aktualizací softwaru. Tato nastavení nahrazují nastavení aktualizace **softwaru**  >  nastavení**vyzvánění pro Windows 10** .

Pomocí těchto nastavení můžete řídit, jak se aktualizace softwaru stahují do zařízení ve vaší organizaci. Můžete například umožnit uživatelům získávat vlastní aktualizace nebo získávat aktualizace pomocí cloudových služeb Optimalizace doručení v profilu zařízení.

Tato funkce podporuje:

- Windows 10 a novější

## <a name="derived-credential"></a>Odvozené přihlašovací údaje

[Odvozené přihlašovací údaje](../protect/derived-credentials.md) jsou certifikáty na čipových kartách, které umožňují ověřování, podepisování a šifrování. V Intune můžete vytvořit profily s těmito přihlašovacími údaji pro použití v aplikacích, e-mailových profilech, připojení k síti VPN, S/MIME a Wi-Fi.

Tato funkce podporuje:

- Android Enterprise
- iOS/iPadOS

## <a name="device-features"></a>Funkce zařízení

[Funkce zařízení](device-features-configure.md) řídí funkce na zařízeních s iOS/IPadOS a MacOS, jako jsou například zprávy o prostředcích pro tisk, oznámení a zamykací obrazovce.

Tato funkce podporuje:

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>Rozhraní pro konfiguraci firmwaru zařízení

[Rozhraní DFCI (Device firmware Configuration Interface](device-firmware-configuration-interface-windows.md) ) umožňuje správcům povolit nebo zakázat nastavení rozhraní UEFI (BIOS) pomocí Intune. Pomocí těchto nastavení můžete zvýšit zabezpečení na úrovni firmwaru, což je obvykle odolnější vůči škodlivým útokům.

Tato funkce podporuje:

- Windows 10 1809 a novější v podporovaném firmwaru

## <a name="device-restrictions"></a>Omezení zařízení

[Omezení zařízení](device-restrictions-configure.md) řídí zabezpečení, hardware, sdílení dat a další nastavení na zařízeních. Můžete například vytvořit profil omezení zařízení, který uživatelům zařízení s iOS/iPadOS brání v používání kamery zařízení. 

Tato funkce podporuje:

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 a novější
- Windows 10 Team

## <a name="domain-join"></a>Připojení k doméně

[Připojení k doméně](domain-join-configure.md) konfiguruje místní informace o doméně služby Active Directory. Tyto informace se nasadí do hybridních zařízení připojených k Azure AD, když se zřídí pomocí Windows autopilotu a Intune. Tento profil oznamuje zařízením, ke kterým se doména a organizační jednotka připojí.

Tato funkce podporuje:

- Windows 10 a novější

## <a name="edition-upgrade"></a>Upgrade edice

[Upgrady edice Windows 10](edition-upgrade-configure-windows-10.md) automaticky upgradují zařízení s některými verzemi Windows 10 na novější edici.

Tato funkce podporuje:

- Windows 10 a novější

## <a name="education"></a>Vzdělávání

[Nastavení vzdělávání – Windows 10](education-settings-configure.md) konfiguruje možnosti pro [aplikaci Windows Zkuste si test](https://docs.microsoft.com/education/windows/take-tests-in-windows-10). Když tyto možnosti nakonfigurujete, žádnou jinou aplikaci nepůjde na zařízení spustit, dokud nebude test dokončen.

[Nastavení vzdělávání – iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) používá aplikaci učebny pro iOS/iPadOS k seznámení s učením a řízení zařízení studenta v učebně. Můžete nakonfigurovat zařízení iPad, aby mohli několik studentů sdílet jedno zařízení.

## <a name="email"></a>E-mail

[Nastavení e-mailu](email-settings-configure.md) vytvoří, přiřadí a monitoruje nastavení e-mailů Exchange ActiveSync na zařízeních. E-mailové profily vám pomůžou s konzistencí, omezit volání podpory a umožnit koncovým uživatelům přístup k firemnímu e-mailu na svých osobních zařízeních, aniž by museli nastavovat. 

Tato funkce podporuje:

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 a novější

## <a name="endpoint-protection"></a>Ochrana koncového bodu

[Endpoint Protection](../protect/endpoint-protection-configure.md) konfiguruje nastavení BitLockeru a programu Microsoft Defender pro zařízení s Windows 10. A nakonfigurujte bránu firewall, bránu a další prostředky na zařízeních macOS.

Informace o připojení rozšířené ochrany před internetovými útoky přes Microsoft Defender (rozšířená) s Microsoft Intune najdete v tématu [Konfigurace koncových bodů pomocí nástrojů pro správu mobilních zařízení (MDM)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Tato funkce podporuje:

- macOS
- Windows 10 a novější

## <a name="esim-cellular---public-preview"></a>Mobilní profily eSIM ve verzi Public Preview

[mobilní profily eSIM](esim-device-configuration.md) umožňuje správcům konfigurovat mobilní datové tarify na spravovaných zařízeních pro Internet a přístup k datům. Po získání aktivačních kódů od mobilního operátoru použijte Intune k importu těchto aktivačních kódů a potom přiřaďte zařízení s technologií eSIM.

Tato funkce podporuje:

- Windows 10 Fall Creators Update a novější

## <a name="extensions"></a>Rozšíření

[rozšíření systému MacOS a rozšíření jádra](kernel-extensions-overview-macos.md) umožňují správcům přidávat funkce nebo programy, které rozšiřuje nativní možnosti operačního systému. Nakonfigurujte tato nastavení tak, aby důvěřovala všem rozšířením z konkrétního vývojáře nebo partnera nebo aby povolovala specifická rozšíření.

Tato funkce podporuje:

- macOS

## <a name="identity-protection"></a>Ochrana identit

[Ochrana identit](../protect/identity-protection-configure.md) řídí prostředí Windows Hello pro firmy na zařízeních s Windows 10 a Windows 10 Mobile. Konfigurací těchto nastavení můžete zpřístupnit Windows Hello pro firmy uživatelům a zařízením a specifikovat požadavky na PIN kódy a gesta zařízení.  

Tato funkce podporuje:  

- Windows 10 a novější
- Windows Holographic for Business  

## <a name="kiosk"></a>Kiosk

Profil [Nastavení veřejného terminálu](kiosk-settings.md) nakonfiguruje zařízení, aby spouštělo jednu aplikaci nebo spustilo spoustu aplikací. Na svém veřejném terminálu si můžete přizpůsobit i další funkce, například úvodní nabídku a webový prohlížeč.

Tato funkce podporuje:

- Windows 10 a novější

Nastavení veřejného terminálu je dostupné taky jako omezení zařízení pro [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)a [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="microsoft-defender-atp"></a>Ochrana ATP v programu Microsoft Defender

[Microsoft Defender Advanced Threat Protection (ATP)](../protect/advanced-threat-protection.md) se integruje s Intune, aby monitoroval a chránil zařízení. Nastavíte úrovně rizika a určíte, co se stane, když zařízení překročí tuto úroveň. V kombinaci s podmíněným přístupem můžete přispět k tomu, abyste zabránili škodlivé aktivitě ve vaší organizaci.

Tato funkce podporuje:

- Windows 10 a novější

## <a name="oemconfig"></a>OEMConfig

[OEMConfig](android-oem-configuration-overview.md) je standard, který umožňuje výrobcům OEM (Original Equipment Manufacturer) a žádnou Emms (Enterprise Mobility Management) vytvářet a podporovat funkce specifické pro výrobce OEM standardizovaným způsobem na zařízeních s Androidem Enterprise. Pomocí OEMConfig vytvoří výrobce OEM schéma, které definuje funkce pro správu specifické pro výrobce OEM, a vloží je do aplikace nahrané do Google Play. Intune čte schéma z aplikace, umožňuje správcům Intune konfigurovat nastavení ve schématu.

Tato funkce podporuje:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>Skripty prostředí PowerShell

[Skripty PowerShellu na zařízeních s Windows 10](../apps/intune-management-extension.md) používají rozšíření pro správu Intune k nahrání skriptů PowerShellu v Intune a pak tyto skripty na svých zařízeních spustíte. Podívejte se také na to, co je potřeba k používání tohoto rozšíření, jak je přidat do Intune a další důležité informace.

Tato funkce podporuje:

- Windows 10 a novější
- Windows Holographic for Business

## <a name="preference-file"></a>Soubor předvoleb

[Soubory předvoleb](preference-file-settings-macos.md) na zařízeních MacOS obsahují informace o aplikacích. Soubory předvoleb můžete například použít k řízení nastavení webového prohlížeče, přizpůsobení aplikací a dalším možnostem.

Tato funkce podporuje:

- macOS

## <a name="shared-multi-user-device"></a>Sdílené zařízení s více uživateli

[Windows 10](shared-user-device-settings-windows.md) a [Windows holografick for Business](shared-user-device-settings-windows-holographic.md) zahrnuje nastavení pro správu zařízení s více uživateli, označovaná taky jako sdílená zařízení nebo sdílené počítače. Když se uživatel přihlásí k zařízení, můžete se rozhodnout, jestli uživatel může změnit možnosti spánku, nebo uložit soubory na zařízení. V jiném příkladu můžete ušetřit místo tím, že vytvoříte profil, který odstraní neaktivní přihlašovací údaje ze zařízení s Windows HoloLens.

Tato sdílená nastavení zařízení s více uživateli umožňují správcům řídit některé funkce zařízení a spravovat tato sdílená zařízení pomocí Intune.

Tato funkce podporuje:

- Windows 10 a novější
- Windows Holographic for Business

## <a name="update-policies"></a>Zásady aktualizací

[zásady aktualizace pro iOS/iPadOS](../protect/software-updates-ios.md) ukazují, jak vytvořit a přiřadit zásady pro iOS/iPadOS pro instalaci softwarových aktualizací do zařízení se systémem iOS/iPadOS. Můžete také zkontrolovat stav instalace.

Zásady aktualizace na zařízeních s Windows najdete v tématu [Optimalizace doručení](delivery-optimization-windows.md). 

Tato funkce podporuje:

- iOS/iPadOS

## <a name="vpn"></a>Síť VPN

[Nastavení VPN](vpn-settings-configure.md) přiřadí uživatelům a zařízením v organizaci profily sítě VPN, aby se mohli snadno a bezpečně připojit k síti. 

Virtuální privátní sítě (VPN) umožňují uživatelům zabezpečený vzdálený přístup k firemní síti. Zařízení používají profil připojení VPN k navázání připojení se serverem VPN. 

Tato funkce podporuje: 

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 a novější

## <a name="wi-fi"></a>Wi-Fi

[Nastavení Wi-Fi](wi-fi-settings-configure.md) přiřadí uživatelům a zařízením nastavení bezdrátové sítě. Po přiřazení profilu Wi-Fi získají uživatelé přístup k vaší podnikové síti, aniž by ji museli konfigurovat sami. 

Tato funkce podporuje: 

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (pouze import)
- Windows 10 a novější

## <a name="zebra-mobility-extensions-mx"></a>Zebra mobility Extensions (MX)

[Zebra mobility Extensions (MX)](android-zebra-mx-overview.md) umožňuje správcům používat a spravovat zařízení Zebra v Intune. Profily StageNow vytvoříte pomocí nastavení a potom pomocí Intune tyto profily přiřadíte a nasadíte na vaše zařízení zebra. [Protokoly StageNow a běžné problémy](android-zebra-mx-logs-troubleshoot.md) jsou skvělým prostředkem k odstraňování potíží s profily a při použití StageNow se zobrazí některé potenciální problémy.

Tato funkce podporuje:

- Správce zařízení s Androidem (rozšíření mobility)

## <a name="manage-and-troubleshoot"></a>Správa a řešení potíží

[Při správě profilů](device-profile-monitor.md) můžete zjistit stav zařízení a přiřazené profily. Také vám pomůžou vyřešit konflikty tím, že se zobrazí nastavení, které způsobuje konflikt, a profily, které obsahují tato nastavení. [Běžné problémy a řešení](device-profile-troubleshoot.md) pomáhají správcům pracovat s profily. Popisuje, co se stane při odstraňování profilu, což způsobí, že se oznámení odesílají do zařízení a další.

## <a name="next-steps"></a>Další kroky

Vyberte svou platformu a začněte.
