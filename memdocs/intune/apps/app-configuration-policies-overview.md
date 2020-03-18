---
title: Zásady konfigurace aplikací v Microsoft Intune
titleSuffix: ''
description: Naučte se používat zásady konfigurace aplikací na zařízeních s iOS/iPadOS nebo Androidem v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 834B4557-80A9-48C0-A72C-C98F6AF79708
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f7d58d2766444be924bd525b5aff20e17a302d56
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326379"
---
# <a name="app-configuration-policies-for-microsoft-intune"></a>Zásady konfigurace aplikací v Microsoft Intune

Zásady konfigurace aplikací vám pomůžou eliminovat problémy s instalací aplikací tím, že vám umožní přiřadit nastavení konfigurace k zásadě, která je přiřazená koncovým uživatelům před spuštěním aplikace. Nastavení se pak doplní automaticky, když je aplikace nakonfigurovaná na zařízeních koncových uživatelů a koncoví uživatelé nepotřebují provádět žádné akce. Nastavení konfigurace jsou pro každou aplikaci jedinečná. 

Zásady konfigurace aplikací můžete vytvářet a používat k poskytování konfiguračních nastavení pro iOS/iPadOS nebo pro aplikace pro Android. Tato nastavení konfigurace umožňují přizpůsobit aplikaci pomocí konfigurace a správy aplikací. Nastavení zásad konfigurace se používají, když aplikace kontroluje tato nastavení, obvykle při prvním spuštění aplikace. 

Nastavení konfigurace aplikace může například vyžadovat, abyste zadali některé z následujících údajů:

- Vlastní číslo portu
- Nastavení jazyka
- Nastavení zabezpečení
- Nastavení brandingu, jako je logo společnosti

Pokud koncoví uživatelé museli místo toho zadat tato nastavení, můžou to udělat nesprávně. Zásady konfigurace aplikací můžou zajistit konzistenci napříč podnikem a snižovat volání helpdesku od koncových uživatelů, kteří se pokoušejí nakonfigurovat vlastní nastavení sami. Pomocí zásad konfigurace aplikací může být přijímání nových aplikací snazší a rychlejší.

Dostupné parametry konfigurace jsou v konečném rozhodování od vývojářů aplikace. Dokumentaci od dodavatele aplikace byste měli zkontrolovat, aby bylo možné zjistit, zda aplikace podporuje konfiguraci a jaké konfigurace jsou k dispozici. U některých aplikací Intune naplní dostupná nastavení konfigurace. 

> [!NOTE]
> Ve spravovaných Obchod Google Play budou aplikace, které podporují konfiguraci, označeny jako:
> 
> ![Snímek obrazovky nakonfigurované aplikace](./media/app-configuration-policies-overview/configured-app.png)
>
> V případě, že jako typ registrace pro zařízení s Androidem používáte spravovaná zařízení, uvidíte jenom aplikace ze [spravovaného Google Play Storu](https://play.google.com/work), ne z [úložiště Google Play](https://play.google.com/store/apps). Spravované Obchod Google Play, které můžete také znáte jako Android for Work (AfW) a Android Enterprise, jsou aplikace v pracovním profilu, které obsahují verze aplikací, které podporují konfiguraci aplikací.

Zásadu konfigurace aplikace můžete přiřadit skupině koncových uživatelů a zařízení pomocí kombinace [zahrnutí a vyloučení přiřazení](apps-inc-exl-assignments.md). Jakmile přidáte zásady konfigurace aplikace, můžete u těchto zásad konfigurace aplikací nastavit přiřazení. Když nastavíte přiřazení zásad, můžete zahrnout a vyloučit [skupiny](../fundamentals/groups-add.md) koncových uživatelů, pro které se zásady vztahují. Když zvolíte možnost zahrnout jednu nebo více skupin, můžete zahrnout konkrétní nebo integrované skupiny. Integrované skupiny jsou **Všichni uživatelé**, **Všechna zařízení** a **Všichni uživatelé a všechna zařízení**.

Zásady konfigurace aplikací se službou Intune můžete použít dvěma způsoby:
- **Spravovaná zařízení** – Intune spravuje zařízení jako poskytovatel správy mobilních zařízení (MDM). Aplikace musí být navržená tak, aby podporovala konfiguraci aplikace.
- **Spravované aplikace** – aplikace, která byla vyvinutá pro integraci sady Intune App SDK. Tato funkce se označuje jako Správa mobilních aplikací bez registrace ([mam-We](app-management.md#mobile-application-management-mam-basics)). Můžete také zabalit aplikaci, která implementuje a podporuje sadu Intune App SDK. Další informace o zabalení aplikace najdete v tématu [Příprava obchodních aplikací na zásady ochrany aplikací](../developer/apps-prepare-mobile-application-management.md).

    > [!NOTE]
    > Aplikace spravované v Intune se při nasazení v kombinaci se zásadami Intune App Protection nahlásí s intervalem 30 minut pro stav zásad konfigurace aplikací Intune. Pokud se k uživateli nepřiřazují zásady Intune App Protection, interval vrácení se změnami zásad konfigurace aplikace Intune se nastaví na 720 minut.

## <a name="apps-that-support-app-configuration"></a>Aplikace podporující konfiguraci aplikací

### <a name="managed-devices"></a>Spravovaná zařízení
Zásady konfigurace aplikací můžete použít pro aplikace, které ji podporují. Aby bylo možné podporovat konfiguraci aplikací v Intune, musí být aplikace napsané tak, aby podporovaly používání konfigurací aplikací definovaných operačním systémem. Podrobnosti o tom, které klíče konfigurace aplikace podporují, najdete v dodavateli vaší aplikace.

### <a name="managed-apps"></a>Spravované aplikace
Obchodní aplikace si můžete připravit buď tak, že [sadu Intune App SDK](../developer/app-sdk.md) zařadíte do aplikace, nebo po jejím vývoji aplikaci pomocí [Nástroje pro zabalení aplikace Intune](../developer/apps-prepare-mobile-application-management.md). Sada Intune App SDK se snaží minimalizovat množství změn v kódu, které vyžaduje vývojář aplikace. Další informace najdete v tématu [Přehled sady Intune App SDK](../developer/app-sdk.md). Porovnání mezi sadou Intune App SDK a nástrojem pro zabalení aplikace Intune najdete v tématu [Příprava obchodních aplikací na zásady ochrany aplikací](../developer/apps-prepare-mobile-application-management.md#feature-comparison).

Výběr **spravovaných aplikací** jako **typ registrace zařízení** konkrétně odkazuje na aplikace nakonfigurované zásadami konfigurace Intune na zařízení, které není zaregistrované ve správě zařízení, zatímco **spravovaná zařízení** se vztahují na aplikace nasazené prostřednictvím kanálu MDM, a proto se spravují přes Intune. Podle těchto popisů vyberte vhodnou volbu. 

![Typ registrace zařízení](./media/app-configuration-policies-overview/device-enrollment-type.png)

> [!NOTE]
> Pro aplikace s více identitami, jako je Microsoft Outlook, se můžou zvážit uživatelské předvolby. Prioritní Doručená pošta, například, bude respektovat nastavení uživatele a nemění konfiguraci. Další parametry umožňují řídit, jestli uživatel může nebo nemůže změnit nastavení. Další informace najdete v tématu [nasazení aplikace Outlook pro iOS/iPadOS a nastavení konfigurace aplikací pro Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="validate-the-applied-app-configuration-policy"></a>Ověření použitých zásad konfigurace aplikace

Zásady konfigurace aplikací můžete ověřit pomocí následujících tří metod:

   1. Viditelně na zařízení. Vykazuje cílová aplikace chování použité v zásadách konfigurace aplikace?
   2. Přes diagnostické protokoly (viz část diagnostické protokoly).
   3. Na portálu Intune. V části **monitorování** zásad může být zajištěn příslušný stav:

      ![První snímek stavu instalace zařízení](./media/app-configuration-policies-overview/device-install-status-1.png)

      ![Druhý snímek stavu instalace zařízení](./media/app-configuration-policies-overview/device-install-status-2.png)

      Kromě toho v části **Intune** -> **zařízení** -> **všechna zařízení** na levé straně obrazovky, v možnosti **Konfigurace aplikace** se zobrazí všechny přiřazené zásady a jejich stav:

      ![Snímek obrazovky s konfigurací aplikace](./media/app-configuration-policies-overview/app-configuration.png)

## <a name="diagnostic-logs"></a>Diagnostické protokoly

### <a name="iosipados-configuration-on-unmanaged-devices"></a>Konfigurace iOS/iPadOS na nespravovaných zařízeních

Konfiguraci iOS/iPadOS můžete ověřit pomocí **diagnostického protokolu Intune** na nespravovaných zařízeních pro konfiguraci spravované aplikace. Kromě následujících kroků můžete získat přístup k protokolům spravovaných aplikací pomocí Microsoft Edge. Další informace najdete v tématu [použití Microsoft Edge v systému iOS/iPadOS pro přístup k protokolům spravovaných aplikací](manage-microsoft-edge.md#use-microsoft-edge-on-ios-to-access-managed-app-logs).

1. Pokud na zařízení ještě není nainstalovaná, Stáhněte si a nainstalujte **Microsoft Edge** z App Storu. Další informace najdete v tématu [Microsoft Intune Protected Apps](apps-supported-intune-apps.md).
2. Spusťte **Microsoft Edge** a na navigačním panelu vyberte **o** > **intunehelp** .
3. Klikněte **na Začínáme.**
4. Klikněte na **sdílet protokoly**.
5. Pomocí e-mailové aplikace dle vašeho výběru můžete protokol odeslat sami sobě, aby se mohl zobrazit v počítači. 
6. Zkontrolujte soubor **IntuneMAMDiagnostics. txt** v prohlížeči textových souborů.
7. Hledat `ApplicationConfiguration`. Výsledky budou vypadat takto:

    ``` JSON
        {
            (
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.BlockListURLs";
                    Value = "https://www.aol.com";
                },
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.bookmarks";
                    Value = "Outlook Web|https://outlook.office.com||Bing|https://www.bing.com";
                }
            );
        },
        {
            ApplicationConfiguration =             
            (
                {
                Name = IntuneMAMUPN;
                Value = "CMARScrubbedM:13c45c42712a47a1739577e5c92b5bc86c3b44fd9a27aeec3f32857f69ddef79cbb988a92f8241af6df8b3ced7d5ce06e2d23c33639ddc2ca8ad8d9947385f8a";
                },
                {
                Name = "com.microsoft.outlook.Mail.NotificationsEnabled";
                Value = false;
                }
            );
        }
    ```

Podrobnosti konfigurace aplikace by měly odpovídat zásadám konfigurace aplikací nakonfigurovaným pro vašeho tenanta. 

![Cílová konfigurace aplikace](./media/app-configuration-policies-overview/targeted-app-configuration-3.png)

### <a name="iosipados-configuration-on-managed-devices"></a>Konfigurace iOS/iPadOS na spravovaných zařízeních

Konfiguraci iOS/iPadOS můžete ověřit pomocí **diagnostického protokolu Intune** na spravovaných zařízeních pro konfiguraci spravované aplikace.

1. Pokud na zařízení ještě není nainstalovaná, Stáhněte si a nainstalujte **Microsoft Edge** z App Storu. Další informace najdete v tématu [Microsoft Intune Protected Apps](apps-supported-intune-apps.md).
2. Spusťte **Microsoft Edge** a na navigačním panelu vyberte **o** > **intunehelp** .
3. Klikněte **na Začínáme.**
4. Klikněte na **sdílet protokoly**.
5. Pomocí e-mailové aplikace dle vašeho výběru můžete protokol odeslat sami sobě, aby se mohl zobrazit v počítači. 
6. Zkontrolujte soubor **IntuneMAMDiagnostics. txt** v prohlížeči textových souborů.
7. Hledat `AppConfig`. Výsledky by měly odpovídat zásadám konfigurace aplikací nakonfigurovaným pro vašeho tenanta.

### <a name="android-configuration-on-managed-devices"></a>Konfigurace Androidu na spravovaných zařízeních

Konfiguraci iOS/iPadOS můžete ověřit pomocí **diagnostického protokolu Intune** na spravovaných zařízeních pro konfiguraci spravované aplikace.

Pokud chcete shromažďovat protokoly ze zařízení s Androidem, musíte vy nebo koncový uživatel stáhnout protokoly ze zařízení přes připojení USB (nebo v **Průzkumníku souborů** ekvivalentní na zařízení). Postup je následující:

1. Připojte zařízení s Androidem k počítači pomocí kabelu USB.
2. V počítači vyhledejte adresář, který má název vašeho zařízení. V tomto adresáři Najděte `Android Device\Phone\Android\data\com.microsoft.windowsintune.companyportal`.
3. Ve složce `com.microsoft.windowsintune.companyportal` otevřete složku soubory a otevřete `OMADMLog_0`.
3. Vyhledejte `AppConfigHelper` pro vyhledání zpráv souvisejících s konfigurací aplikace. Výsledky budou vypadat podobně jako následující blok dat:

    `2019-06-17T20:09:29.1970000       INFO   AppConfigHelper     10888  02256  Returning app config JSON [{"ApplicationConfiguration":[{"Name":"com.microsoft.intune.mam.managedbrowser.BlockListURLs","Value":"https:\/\/www.aol.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.bookmarks","Value":"Outlook Web|https:\/\/outlook.office.com||Bing|https:\/\/www.bing.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.homepage","Value":"https:\/\/www.arstechnica.com"}]},{"ApplicationConfiguration":[{"Name":"IntuneMAMUPN","Value":"AdeleV@M365x935807.OnMicrosoft.com"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled","Value":"false"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled.UserChangeAllowed","Value":"false"}]}] for user User-875363642`
    
## <a name="graph-api-support-for-app-configuration"></a>Podpora Graph API pro konfiguraci aplikací

K provádění úloh konfigurace aplikace můžete použít Graph API. Podrobnosti najdete v tématu [Graph API cílené konfigurace mam reference](https://docs.microsoft.com/graph/api/resources/intune-shared-targetedmanagedappconfiguration?view=graph-rest-beta). Další informace o Intune a graphu najdete [v tématu práce s Intune v Microsoft Graph](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-beta).

## <a name="troubleshooting"></a>Odstraňování potíží

### <a name="using-logs-to-show-a-configuration-parameter"></a>Použití protokolů k zobrazení konfiguračního parametru
Když se v protokolech zobrazí parametr konfigurace, u kterého se potvrdí, že se má použít, ale zdá se, že nebude fungovat, může se jednat o problém s implementací konfigurace vývojářem aplikace. Vyzkoušejte si nejprve konkrétního vývojáře aplikace nebo ověřte jeho znalostní bázi, může vám pomoci s Microsoftem. Pokud se jedná o problém s tím, jak se konfigurace zpracovává v rámci aplikace, bude nutné ji vyřešit v budoucí aktualizované verzi této aplikace.

## <a name="next-steps"></a>Další kroky

### <a name="managed-devices"></a>Spravovaná zařízení

- Naučte se používat konfiguraci aplikací u zařízení s iOS/iPadOS.  Viz [Přidání zásad konfigurace aplikací pro spravovaná zařízení s iOS/iPadOS](app-configuration-policies-use-ios.md).
- Přečtěte si, jak používat konfiguraci aplikací u zařízení s Androidem.  Viz [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem](app-configuration-policies-use-android.md).

### <a name="managed-apps"></a>Spravované aplikace

- Přečtěte si, jak používat konfiguraci aplikací u spravovaných aplikací. Viz [Přidání zásad konfigurace aplikací pro spravované aplikace bez registrace zařízení](app-configuration-policies-managed-app.md).
