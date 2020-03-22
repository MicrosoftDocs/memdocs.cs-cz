---
title: Funkce a nastavení zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Přehled různých profilů zařízení Microsoft Intune. Získejte informace o funkcích, omezeních, e-mailu, Wi-Fi, VPN, vzdělávání, certifikátech, upgradu Windows 10, BitLockeru a programu Microsoft Defender, Windows Information Protection, šablonách pro správu a vlastním nastavení konfigurace zařízení ve společnosti Microsoft. Centrum pro správu Správce koncových bodů. Pomocí těchto profilů můžete spravovat a chránit data a zařízení ve vaší společnosti.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
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
ms.openlocfilehash: 420340e18eb4e638ed7bde049e6b548037c54f87
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087097"
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
- Wvdows Phone 8.1
- Windows 8.1
- Windows 10 a novější

## <a name="custom-profile"></a>Profil Vlastní

[Vlastní nastavení](custom-settings-configure.md) umožňuje správcům přiřazovat nastavení zařízení, která nejsou integrovaná do Intune. Na zařízeních s Androidem můžete zadat hodnoty OMA-URI. Pro zařízení s iOS/iPadOS můžete importovat konfigurační soubor, který jste vytvořili v Apple Configuratoru.

Tato funkce podporuje:

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- macOS
- Wvdows Phone 8.1

## <a name="delivery-optimization"></a>Optimalizace doručení

[Optimalizace doručování](delivery-optimization-windows.md) nabízí lepší možnosti doručování aktualizací softwaru. Tato nastavení nahrazují **aktualizace softwaru** > nastavení **Windows 10 Update Ring** .

Pomocí těchto nastavení můžete řídit, jak se aktualizace softwaru stahují do zařízení ve vaší organizaci. Můžete například umožnit uživatelům získávat vlastní aktualizace nebo získávat aktualizace pomocí cloudových služeb Optimalizace doručení v profilu zařízení.

Tato funkce podporuje:

- Windows 10 a novější

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

[Nastavení vzdělávání – Windows 10](education-settings-configure.md) konfiguruje možnosti pro [aplikaci Windows Zkuste si test](https://education.microsoft.com/gettrained/win10takeatest). Když tyto možnosti nakonfigurujete, žádnou jinou aplikaci nepůjde na zařízení spustit, dokud nebude test dokončen.

[Nastavení vzdělávání – iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) používá aplikaci učebny pro iOS/iPadOS k seznámení s učením a řízení zařízení studenta v učebně. Můžete nakonfigurovat zařízení iPad, aby mohli několik studentů sdílet jedno zařízení.

## <a name="email"></a>E-mail

[Nastavení e-mailu](email-settings-configure.md) vytvoří, přiřadí a monitoruje nastavení e-mailů Exchange ActiveSync na zařízeních. E-mailové profily vám pomůžou s konzistencí, omezit volání podpory a umožnit koncovým uživatelům přístup k firemnímu e-mailu na svých osobních zařízeních, aniž by museli nastavovat. 

Tato funkce podporuje: 

- Správce zařízení s Androidem
- Android Enterprise
- iOS/iPadOS
- Wvdows Phone 8.1
- Windows 10 a novější

## <a name="endpoint-protection"></a>Ochrana koncových bodů

[Nastavení ochrany koncového bodu pro Windows 10](../protect/endpoint-protection-windows-10.md) konfiguruje nastavení BitLockeru a programu Microsoft Defender pro zařízení s Windows 10.

Informace o připojení rozšířené ochrany před internetovými útoky přes Microsoft Defender (rozšířená) s Microsoft Intune najdete v tématu [Konfigurace koncových bodů pomocí nástrojů pro správu mobilních zařízení (MDM)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Tato funkce podporuje:

- Windows 10 a novější

## <a name="esim-cellular---public-preview"></a>Mobilní profily eSIM ve verzi Public Preview

[mobilní profily eSIM](esim-device-configuration.md) umožňuje správcům konfigurovat mobilní datové tarify na spravovaných zařízeních pro Internet a přístup k datům. Po získání aktivačních kódů od mobilního operátoru použijte Intune k importu těchto aktivačních kódů a potom přiřaďte zařízení s technologií eSIM.

Tato funkce podporuje:

- Windows 10 Fall Creators Update a novější

## <a name="extensions"></a>Rozšíření

[Rozšíření jádra](kernel-extensions-overview-macos.md) umožňují správcům přidávat funkce nebo programy na úrovni jádra na zařízeních MacOS. Nakonfigurujte tato nastavení tak, aby důvěřovala všem rozšířením z konkrétního vývojáře nebo partnera, nebo povolte specifická rozšíření jádra.

Tato funkce podporuje:

- macOS

## <a name="identity-protection"></a>Ochrana identit

[Ochrana identit](../protect/identity-protection-configure.md) řídí prostředí Windows Hello pro firmy na zařízeních s Windows 10 a Windows 10 Mobile. Konfigurací těchto nastavení můžete zpřístupnit Windows Hello pro firmy uživatelům a zařízením a specifikovat požadavky na PIN kódy a gesta zařízení.  

Tato funkce podporuje:  

- Windows 10 a novější
- Windows Holographic for Business  

## <a name="kiosk"></a>Veřejný terminál

Profil [Nastavení veřejného terminálu](kiosk-settings.md) nakonfiguruje zařízení, aby spouštělo jednu aplikaci nebo spustilo spoustu aplikací. Na svém veřejném terminálu si můžete přizpůsobit i další funkce, například úvodní nabídku a webový prohlížeč.

Tato funkce podporuje:

- Windows 10 a novější

Nastavení veřejného terminálu je dostupné taky jako omezení zařízení pro [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings)a [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="oemconfig"></a>OEMConfig

[OEMConfig](android-oem-configuration-overview.md) je standard, který umožňuje výrobcům OEM (Original Equipment Manufacturer) a žádnou Emms (Enterprise Mobility Management) vytvářet a podporovat funkce specifické pro výrobce OEM standardizovaným způsobem na zařízeních s Androidem Enterprise. Pomocí OEMConfig vytvoří výrobce OEM schéma, které definuje funkce pro správu specifické pro výrobce OEM, a vloží je do aplikace nahrané do Google Play. Intune čte schéma z aplikace, umožňuje správcům Intune konfigurovat nastavení ve schématu.

Tato funkce podporuje:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>Skripty prostředí PowerShell

[Skripty PowerShellu na zařízeních s Windows 10](../apps/intune-management-extension.md) používají rozšíření pro správu Intune k nahrání skriptů PowerShellu v Intune a pak tyto skripty na svých zařízeních spustíte. Podívejte se také na to, co je potřeba k používání tohoto rozšíření, jak je přidat do Intune a další důležité informace.


Tato funkce podporuje:

- Windows 10 a novější
- Windows Holographic for Business

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
- Wvdows Phone 8.1
- Windows 8.1
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

## <a name="windows-information-protection-profile"></a>Profil Windows Information Protection

[Služba Windows Information Protection](../protect/windows-information-protection-configure.md) pomáhá chránit před únikem dat, aniž by zasahovala do možností zaměstnanců. Pomáhá také chránit podnikové aplikace a data před náhodnými úniky dat na zařízeních ve vlastnictví podniku a na osobních zařízeních, která zaměstnanci používají v práci. Použití Windows Information Protection nevyžaduje změny v prostředí nebo jiných aplikacích.

Tato funkce podporuje:

- Windows 10 a novější

## <a name="zebra-mobility-extensions-mx"></a>Zebra mobility Extensions (MX)

[Zebra mobility Extensions (MX)](android-zebra-mx-overview.md) umožňuje správcům používat a spravovat zařízení Zebra v Intune. Profily StageNow vytvoříte pomocí nastavení a potom pomocí Intune tyto profily přiřadíte a nasadíte na vaše zařízení zebra. [Protokoly StageNow a běžné problémy](android-zebra-mx-logs-troubleshoot.md) jsou skvělým prostředkem k odstraňování potíží s profily a při použití StageNow se zobrazí některé potenciální problémy.

Tato funkce podporuje:

- Správce zařízení s Androidem (rozšíření mobility)

## <a name="manage-and-troubleshoot"></a>Správa a řešení problémů

[Při správě profilů](device-profile-monitor.md) můžete zjistit stav zařízení a přiřazené profily. Také vám pomůžou vyřešit konflikty tím, že se zobrazí nastavení, které způsobuje konflikt, a profily, které obsahují tato nastavení. [Běžné problémy a řešení](device-profile-troubleshoot.md) pomáhají správcům pracovat s profily. Popisuje, co se stane při odstraňování profilu, což způsobí, že se oznámení odesílají do zařízení a další.

## <a name="next-steps"></a>Další kroky

Vyberte svou platformu a začněte.
