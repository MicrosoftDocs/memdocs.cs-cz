---
title: Vytvoření profilu zařízení s iOS/iPadOS nebo macOS pomocí Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte profil zařízení se systémem iOS, iPadOS nebo macOS a pak nakonfigurujte nastavení pro průchozí tisk, rozložení domovské obrazovky, oznámení aplikací, sdílené zařízení, jednotné přihlašování a nastavení filtru webového obsahu v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ffa3d11b92c38373da22e53b96fe9cf9e520b5b
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149185"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>Přidání nastavení funkcí zařízení se systémem iOS, iPadOS nebo macOS v Intune

Intune zahrnuje mnoho funkcí a nastavení, které správcům pomůžou řídit zařízení s iOS, iPadOS a macOS. Správci můžou například:

- Umožněte uživatelům přístup k tiskárnám pro tisk ve vaší síti.
- Přidávání aplikací a složek na domovskou obrazovku, včetně přidávání nových stránek
- Zvolit, jak a jak se zobrazují oznámení aplikací
- Konfigurace zamykací obrazovky pro zobrazení zprávy nebo inventárního štítku, zejména pro sdílená zařízení
- Poskytněte uživatelům zabezpečené jednotné přihlašování pro sdílení přihlašovacích údajů mezi aplikacemi.
- Filtrovat weby, které používají jazyk pro dospělé a povolují nebo blokují konkrétní weby

Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu ho potom nahrajte nebo nasaďte do zařízení se systémem iOS/iPadOS a macOS ve vaší organizaci.

Tento článek popisuje různé funkce, které můžete nakonfigurovat, a ukazuje, jak vytvořit profil konfigurace zařízení. Můžete si také prohlédnout všechna dostupná nastavení pro zařízení se [systémem iOS/iPadOS](ios-device-features-settings.md) a [MacOS](macos-device-features-settings.md) .

## <a name="airprint"></a>AirPrint

Postupné tisku je funkce společnosti Apple, která umožňuje zařízením tisk do souborů přes bezdrátovou síť. V Intune můžete do zařízení přidat informace o prostředcích pro tisk.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v článku o prostudování v [systému iOS/iPadOS](ios-device-features-settings.md#airprint) a [ve službě MacOS pro tisk](macos-device-features-settings.md#airprint).

Další informace o protiskech najdete v tématu [o](https://support.apple.com/HT201311) prostudování na webu společnosti Apple.

To platí pro:

- iOS 7,0 a novější
- iPadOS 13,0 a novější
- macOS 10,10 a novější

## <a name="app-notifications"></a>App notifications

Vyberte, jak budou aplikace na zařízeních s iOS a iPadOS dostávat oznámení. Například z Intune můžete odesílat oznámení aplikací tak, aby se zobrazovala v centru oznámení, zobrazit na zamykací obrazovce nebo přehrát zvuk.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v tématu [oznámení aplikací v systému iOS/iPadOS](ios-device-features-settings.md#app-notifications).

Další informace o této funkci najdete v tématu [oznámení](https://developer.apple.com/notifications/) na webu společnosti Apple.

To platí pro:

- iOS 9,3 a novější
- iPadOS 13,0 a novější

## <a name="associated-domains"></a>Přidružené domény

Přidružené domény umožňují vytvořit relaci mezi vašimi doménami, například `contoso.com`a vašimi aplikacemi. Tato funkce umožňuje:

- Sdílejte data a přihlaste přihlašovací údaje mezi aplikacemi a weby ve vaší organizaci.
- Používejte funkce aplikací, které jsou založené na vašem webu, jako je například rozšíření aplikace jednotného přihlašování, univerzální odkazy a automatické vyplňování hesel.

  Například vytvořte přidruženou doménu, aby bylo možné automatické vyplňování hesel doporučit, jako je například heslo, pro weby přidružené k vaší aplikaci.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v tématu [přidružené domény v MacOS](macos-device-features-settings.md#associated-domains).

Další informace o této funkci najdete v tématu [nastavení přidružených domén aplikace](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) na webu společnosti Apple.

To platí pro:

- macOS 10,15 a novější

## <a name="home-screen-layout"></a>Rozložení domovské obrazovky

Tato nastavení konfigurují rozložení a složky aplikace v Dock a na domácích obrazovkách na zařízeních s iOS a iPadOS. Můžete:

- K přidání aplikací nebo složek na obrazovku použijte nastavení **Dock** . V Docku zařízení můžete například zobrazit Safari a e-mailovou aplikaci.
- Přidejte **stránky** , které chcete zobrazit na domovské obrazovce, a aplikace, které chcete zobrazit na jednotlivých stránkách. Přidejte například stránku **Contoso** a na tuto stránku přidejte aplikaci nastavení.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v tématu [rozložení domovské obrazovky v systému iOS/iPadOS](ios-device-features-settings.md#home-screen-layout).

To platí pro:

- iOS 9,3 a novější
- iPadOS 13,0 a novější

## <a name="lock-screen-message"></a>Zpráva zamykací obrazovky

Pomocí těchto nastavení můžete zobrazit vlastní zprávu nebo text v přihlašovacím okně a na zamykací obrazovce. Můžete například zadat "Pokud došlo ke ztrátě, vrátit se do..." zpráva a zobrazit informace o inventárním štítku.

Seznam nastavení, která můžete v Intune nakonfigurovat, najdete v tématu [Nastavení zpráv na zamykací obrazovce v iOS/iPadOS](ios-device-features-settings.md#lock-screen-message).

Další informace o zprávě zamykací obrazovky najdete v tématu [LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage) na webu společnosti Apple.

To platí pro:

- iOS 9,3 a novější
- iPadOS 13,0 a novější

## <a name="login-items"></a>Přihlašovací položky

Pomocí této funkce můžete zvolit aplikace, vlastní aplikace, soubory a složky, které se otevřou, když se uživatelé přihlásí k zařízením.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v tématu [přihlášení k položkám v MacOS](macos-device-features-settings.md#login-items).

To platí pro:

- macOS 10,13 a novější

## <a name="login-window"></a>Přihlašovací okno

Můžete ovládat vzhled přihlašovací obrazovky a funkcí, které uživatelé budou mít k dispozici, než se přihlásí. Přidejte například hlavičku s vlastní zprávou, vyberte, zda je zobrazeno tlačítko režimu spánku a další.

Seznam nastavení, která můžete v Intune nakonfigurovat, najdete v tématu [přihlašovací okno v MacOS](macos-device-features-settings.md#login-window).

To platí pro:

- macOS 10,7 a novější

## <a name="single-sign-on"></a>Jednotné přihlašování

Většina obchodních aplikací vyžaduje z důvodu zabezpečení určitou úroveň ověřování uživatelů. V mnoha případech ověřování vyžaduje, aby uživatelé opakovaně zadali stejné přihlašovací údaje. Pro zlepšení uživatelského prostředí můžou vývojáři vytvářet aplikace, které používají jednotné přihlašování (SSO). Použití jednotného přihlašování omezuje počet, kolikrát musí uživatel zadat přihlašovací údaje.

Profil jednotného přihlašování je založený na protokolu Kerberos. Kerberos je protokol ověřování v síti, který používá kryptografii tajného klíče k ověřování aplikací klient-server. Nastavení Intune definují informace účtu Kerberos při přístupu k serverům nebo konkrétním aplikacím a zpracovávají výzvy protokolu Kerberos pro webové stránky a nativní aplikace. Apple doporučuje místo nastavení jednotného přihlašování použít [rozšíření aplikace jednotného přihlašování k protokolu Kerberos](#single-sign-on-app-extension) (v tomto článku).  

Pokud chcete použít jednotné přihlašování, ujistěte se, že máte:

- Aplikace, která je kódována tak, aby hledala úložiště přihlašovacích údajů uživatele v rámci jednotného přihlašování na zařízení.
- Intune je nakonfigurované pro jednotné přihlašování zařízení iOS/iPadOS.

Seznam nastavení, která můžete v Intune nakonfigurovat, najdete v tématu [jednotné přihlašování v systému iOS/iPadOS](ios-device-features-settings.md#single-sign-on).

To platí pro:

- iOS 7,0 a novější
- iPadOS 13,0 a novější

## <a name="single-sign-on-app-extension"></a>Rozšíření aplikace s jednotným přihlašováním

Tato nastavení konfigurují rozšíření aplikace, které umožňuje jednotné přihlašování (SSO) pro zařízení s iOS, iPadOS a macOS. Většina obchodních aplikací a webů organizace vyžaduje určitou úroveň zabezpečeného ověřování uživatelů. V mnoha případech ověřování vyžaduje, aby uživatelé opakovaně zadali stejné přihlašovací údaje. Jednotné přihlašování umožňuje uživatelům přístup k aplikacím a webům po zadání přihlašovacích údajů jednou. Jednotné přihlašování také nabízí lepší možnosti ověřování pro uživatele a snižuje počet opakovaných výzev k zadání přihlašovacích údajů.

Pomocí těchto nastavení můžete v Intune nakonfigurovat rozšíření aplikace jednotného přihlašování vytvořené vaší organizací, vaším poskytovatelem identity, Microsoftem nebo společností Apple. Rozšíření aplikace jednotného přihlašování zpracovává ověřování pro vaše uživatele. Tato nastavení konfigurují rozšíření aplikace jednotného přihlašování pro typ přesměrování a přihlašovací údaje.

- Typ přesměrování je navržený pro moderní ověřovací protokoly, jako je OAuth a typu Saml2. Na zařízeních macOS můžete použít obecné rozšíření přesměrování. Pro zařízení s iOS/iPadOS si můžete vybrat mezi rozšířením Microsoft Azure AD SSO Extension ([Microsoft Enterprise SSO-in](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)) a obecným rozšířením pro přesměrování.
- Typ přihlašovacích údajů je určený pro toky ověřování typu Challenge a Response. Můžete si vybrat rozšíření přihlašovací údaje specifické pro protokol Kerberos poskytované společností Apple a obecné rozšíření přihlašovacích údajů.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v tématu [rozšíření aplikace pro iOS/IPADOS SSO](ios-device-features-settings.md#single-sign-on-app-extension) a [rozšíření aplikace MacOS SSO](macos-device-features-settings.md#single-sign-on-app-extension).

Další informace o vývoji rozšíření aplikace jednotného přihlašování najdete na webu společnosti Apple v [rozšiřitelném podnikovém přihlašování](https://developer.apple.com/videos/play/tech-talks/301) . Pokud si chcete přečíst popis této funkce, podívejte se na [nastavení datové části rozšíření jednotného přihlašování](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web). 

> [!NOTE]
> Funkce **rozšíření aplikace jednotného přihlašování** se liší od funkce **jednotného přihlašování** :
>
> - Nastavení **rozšíření aplikace s jednotným přihlašováním** platí pro iPadOS 13,0 (a novější), iOS 13,0 (a novější) a MacOS 10,15 (a novější). Nastavení **jednotného přihlašování** platí pro iPadOS 13,0 (a novější) a iOS 7,0 a novější.
>
> - Nastavení **rozšíření aplikace s jednotným přihlašováním** definuje rozšíření pro použití poskytovateli identity nebo organizacemi k zajištění bezproblémového podnikového přihlašování. Nastavení **jednotného přihlašování** definuje informace o účtu Kerberos pro přístup uživatelů k serverům nebo aplikacím.
>
> - **Rozšíření aplikace jednotného přihlašování** používá k ověření operační systém Apple. Může tak poskytnout prostředí koncového uživatele, které je lepší než **jednotné přihlašování**.
>
> - Z perspektivy vývoje s použitím **rozšíření aplikace s jednotným přihlašováním**můžete použít libovolný typ přesměrované ověřování SSO nebo přihlašovacích údajů jednotného přihlašování. S **jednotným přihlašováním**můžete použít jenom ověřování pomocí protokolu Kerberos SSO.
>
> - **Rozšíření aplikace pro jednotné přihlašování** pomocí protokolu Kerberos bylo vyvinuto společností Apple a je integrováno do platforem iOS/iPadOS 13.0 + a MacOS 10.15 +. Integrované rozšíření protokolu Kerberos se dá použít k protokolování uživatelů do nativních aplikací a webů, které podporují ověřování pomocí protokolu Kerberos. **Jednotné přihlašování** není Apple implementace protokolu Kerberos.
>
> - Integrované **rozšíření pro jednotné přihlašování** pomocí protokolu Kerberos zpracovává výzvy protokolu Kerberos pro webové stránky a aplikace stejně jako **jednotné přihlašování**. Integrované rozšíření protokolu Kerberos ale podporuje změny hesla a v podnikových sítích je lépe fungovat. Při rozhodování mezi **rozšířením jednotného přihlašování** pomocí protokolu Kerberos a **jednotným přihlašováním**doporučujeme použít rozšíření kvůli lepšímu výkonu a funkcím.

To platí pro:

- iOS 13,0 a novější
- iPadOS 13,0 a novější
- macOS 10,15 a novější

## <a name="wallpaper"></a>Tapeta

Přidejte vlastní obrázek. png,. jpg nebo. jpeg do zařízení se systémem iOS/iPadOS pod dohledem. Pomocí Intune můžete například přidat logo společnosti do zamykací obrazovky na svých zařízeních.

Seznam nastavení, která můžete nakonfigurovat v Intune, najdete v tématu [Tapeta v iOS/iPadOS](ios-device-features-settings.md#wallpaper).

To platí pro:

- iOS
- iPadOS 13,0 a novější

## <a name="web-content-filter"></a>Filtr webového obsahu

Tato nastavení využívají vestavěný algoritmus automatického filtru od společnosti Apple k vyhodnocení webových stránek a blokují obsah pro dospělé a jazyk pro dospělé. Můžete také vytvořit seznam povolených webových odkazů a omezených webových odkazů. Můžete například dovolit, aby se otevíraly jenom `contoso` weby.

Seznam nastavení, která můžete v Intune nakonfigurovat, najdete v tématu [Filtr webového obsahu v systému iOS/iPadOS](ios-device-features-settings.md#web-content-filter).

To platí pro:

- iOS 7,0 a novější
- iPadOS 13,0 a novější

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Konfigurace zařízení** > **profily** > konfigurace**vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte platformu zařízení. Možnosti:  

        - **iOS/iPadOS**
        - **macOS**

    - **Profil**: vyberte **funkce zařízení**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrý název zásady je například **MacOS: konfiguruje přihlašovací obrazovku**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte platformu:

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo. `JohnGlenn_ITDepartment` Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nemusí ještě nic dělat. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Zobrazí všechna nastavení funkcí zařízení pro zařízení s [iOS/iPadOS](ios-device-features-settings.md) a [MacOS](macos-device-features-settings.md) .
