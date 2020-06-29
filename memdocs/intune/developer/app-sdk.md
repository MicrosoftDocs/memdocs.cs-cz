---
title: Výhody sady Intune App SDK
titleSuffix: Microsoft Intune
description: Sada Intune App SDK je dostupná pro platformy iOS i Android a umožňuje povolit funkce správy mobilních aplikací v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: cd9f05e7-26e6-45e0-8d38-67d8232b1cae
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0a732db0adf9d08bf8a453a365002d8e1f8b22d
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502710"
---
# <a name="microsoft-intune-app-sdk-overview"></a>Přehled sady Microsoft Intune App SDK
Sada Intune App SDK, která je dostupná pro iOS i Android, umožňuje, aby vaše aplikace podporovala [Zásady ochrany aplikací](../apps/app-protection-policy.md)Intune. Když vaše aplikace používá zásady ochrany aplikací, dá se spravovat přes Intune a jako spravovaná aplikace je rozpozná Intune. Sada SDK se snaží minimalizovat množství změn v kódu, které vyžaduje vývojář aplikace. Zjistíte, že většinu funkcí sady SDK můžete povolit beze změny chování vaší aplikace. Pro pokročilé prostředí koncových uživatelů a správců IT můžete využít rozhraní API sady SDK k přizpůsobení chování vaší aplikace pro podporu funkcí, které vyžadují zapojení vaší aplikace.

Jakmile povolíte aplikaci, aby podporovala zásady ochrany aplikací Intune, můžou správci IT tyto zásady nasadit, aby chránily podniková data v rámci aplikace.

## <a name="app-protection-features"></a>Funkce ochrany aplikací

Níže najdete příklady funkcí ochrany aplikací Intune, které se dají aktivovat pomocí sady SDK.

### <a name="control-users-ability-to-move-corporate-files"></a>Řízení možnosti uživatelů přesouvat firemní soubory
Správci IT můžou řídit, kam se dají přesouvat pracovní nebo školní data v aplikaci. Můžou třeba nasadit zásadu, která zakazuje aplikacím zálohovat podniková data do cloudu.

### <a name="configure-clipboard-restrictions"></a>Konfigurace omezení schránky
Správci IT můžou konfigurovat chování schránky v aplikacích spravovaných v Intune. Můžou například nasadit zásadu, která zabrání koncovým uživatelům vyjmout nebo zkopírovat data z aplikace a vložit je do nespravované osobní aplikace.

### <a name="enforce-encryption-on-saved-data"></a>Vynucení šifrování uložených dat
Správci IT můžou vynutit zásadu, která zajišťuje, aby data ukládaná aplikací do zařízení šifrovala.

### <a name="remotely-wipe-corporate-data"></a>Vzdálené vymazání podnikových dat
Správci IT můžou vzdáleně vymazat podniková data z aplikací spravovaných v Intune. Tato funkce je založená na identitě a odstraní jenom soubory přidružené k podnikové identitě koncového uživatele. K tomu funkce vyžaduje zapojení aplikace. Aplikace může určit identitu, u které má dojít k vymazání, na základě uživatelského nastavení. Když uvedená uživatelská nastavení v aplikaci chybí, výchozím chováním bude vymazání adresáře aplikace a upozornění koncového uživatele, že došlo k odebrání přístupu.

### <a name="enforce-the-use-of-a-managed-browser"></a>Vynucení používání spravovaného prohlížeče
Správce IT může vynutit, aby se webové odkazy v aplikaci otevíraly pomocí [aplikace Intune Managed Browser](../apps/manage-microsoft-edge.md). Tato funkce zajistí, aby odkazy zobrazované v podnikovém prostředí zůstaly uchované v rámci aplikací spravovaných v Intune.

### <a name="enforce-a-pin-policy"></a>Vynucení zásady kódu PIN
Správce IT může po koncovém uživateli vyžadovat, aby před přístupem k podnikovým datům v aplikaci zadal PIN. Tím se zajistí, že uživatel, který aplikaci používá, je tím samým uživatelem, který se původně přihlásil pomocí pracovního nebo školního účtu. Když si koncoví uživatelé nakonfigurují PIN, sada Intune App SDK použije Azure Active Directory k ověření přihlašovacích údajů koncových uživatelů podle registrovaného účtu Intune.

### <a name="require-users-to-sign-in-with-a-work-or-school-account-for-app-access"></a>Vyžadovat, aby se uživatelé přihlásili pomocí pracovního nebo školního účtu pro přístup k aplikaci
Správci IT můžou vyžadovat, aby se uživatelé před přístupem k aplikaci přihlásili pomocí pracovního nebo školního účtu. Sada Intune App SDK použije Azure Active Directory k poskytnutí jednotného přihlašování, při kterém se jednou zadané přihlašovací údaje znovu použijí pro následující přihlášení. Také podporujeme ověřování řešení správy identity sdružených se službou Azure Active Directory.

### <a name="check-device-health-and-compliance"></a>Kontrola stavu zařízení a dodržování předpisů
Správci IT můžou před přístupem koncových uživatelů k aplikacím kontrolovat stav zařízení a dodržování zásad Intune. V systému iOS/iPadOS tato zásada kontroluje, jestli zařízení nemá jailbreak. Na Androidu tato zásada kontroluje, jestli zařízení nemá root.

### <a name="support-multi-identity"></a>Podpora více identit
Podpora více identit je funkce sady SDK umožňující koexistenci účtů spravovaných zásadou (podnikových) a nespravovaných (osobních) v jediné aplikaci.

Mnoho uživatelů si například v mobilních aplikacích Office pro iOS a Android konfiguruje podnikové i osobní e-mailové účty. Když uživatel pracuje s daty s podnikovým účtem, správce IT musí mít jistotu, že se použije zásada ochrany aplikací. Když ale uživatel přistupuje k osobnímu e-mailovému účtu, tato data by měla být mimo dosah správce IT. Sada Intune App SDK toho dosahuje tím, že v aplikaci cílí zásady ochrany aplikace **jenom** na podnikovou identitu.

Tato funkce více identit vám pomůže vyřešit problém s ochranou dat, se kterým se setkávají organizace s aplikacemi ze Storu, které podporují osobní i pracovní účty.
 
### <a name="app-protection-without-device-enrollment"></a>Ochrana aplikací bez registrace zařízení

>[!IMPORTANT]
>Intune App Protection bez registrace zařízení je dostupná v nástrojích Intune App Wrapping Tools a sadách Intune App SDK pro Android, Intune App SDK pro iOS a Xamarinových vazbách sady Intune App SDK.

Mnoho uživatelů s osobními zařízeními chce pracovat s podnikovými daty bez registrace svého osobního zařízení u poskytovatele správy mobilních zařízení (MDM). Registrace MDM vyžaduje globální kontrolu nad zařízením, proto uživatelé často váhají předat tuto kontrolu nad vlastním osobním zařízením podniku.

Ochrana aplikací bez registrace zařízení umožňuje službě Microsoft Intune nasadit zásady ochrany aplikací přímo na aplikaci, aby se nemusela spoléhat na nasazení zásad prostřednictvím kanálu pro správu zařízení.

### <a name="on-demand-application-vpn-connections-with-citrix-mvpn"></a>Připojení VPN aplikace na vyžádání pomocí Citrix mVPN 
Můžete spravovat zařízení a aplikace s kombinací Citrix XenMobile MDX a Microsoft Intune. Tato kombinace znamená, že můžete spravovat aplikace pomocí zásad ochrany aplikací Intune při použití technologie mVPN společnosti Citrix. Integrace s Citrixem je dostupná pro sadu Intune App SDK pro iOS a Android a při použití nástroje Intune App Wrapping Tool pro iOS a Android (s příznakem -citrix).
 
Další informace o Citrix MDX najdete v tématech, které pojednávají o [sadě nástrojů MDX](https://docs.citrix.com/en-us/mdx-toolkit/10/about-mdx-toolkit.html), [nástroji Citrix MDX App Wrapper pro iOS](https://docs.citrix.com/en-us/mdx-toolkit/10/xmob-mdx-kit-app-wrap-ios.html) a [nástroji Citrix MDX App Wrapper pro Android](https://docs.citrix.com/en-us/mdx-toolkit/10/xmob-mdx-kit-app-wrap-android.html).

## <a name="next-steps"></a>Další kroky

- Začněte [se sadou Microsoft Intune App SDK](app-sdk-get-started.md).
