---
title: Přidání a přiřazení aplikací pro ochranu před mobilními hrozbami (MTD) do Microsoft Intune
titleSuffix: Microsoft Intune
description: Pomocí Intune můžete přidat aplikace pro ochranu před mobilními hrozbami (MTD), aplikaci Microsoft Authenticator a zásady konfigurace iOS na portálu Azure Portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb83a8e5b907ee55dd1c02d3af0dc04002790a18
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83991112"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Přidání a přiřazení aplikací pro ochranu před mobilními hrozbami (MTD) pomocí Intune

Pomocí Intune můžete přidávat a nasazovat aplikace pro ochranu před mobilními hrozbami (MTD), aby koncoví uživatelé mohli dostávat oznámení, když se v jejich mobilních zařízeních identifikuje hrozba, a získat pokyny k nápravě hrozeb.

> [!NOTE]
> Tento článek se týká všech partnerů ochrany před mobilními hrozbami.

## <a name="before-you-begin"></a>Před zahájením

V Intune proveďte následující kroky. Ujistěte se, že jste obeznámeni s procesem:

- [Přidání aplikace do služby Intune](../apps/apps-add.md)
- [Přidání zásad konfigurace aplikace pro iOS do služby Intune](../apps/app-configuration-policies-use-ios.md)
- [Přiřazení aplikace pomocí služby Intune](../apps/apps-deploy.md)

> [!TIP]
> Portál společnosti Intune funguje jako zprostředkovatel na zařízeních s Androidem, aby uživatelé mohli své identity zkontrolovat pomocí Azure AD.

## <a name="configure-microsoft-authenticator-for-ios"></a>Konfigurace aplikace Microsoft Authenticator pro iOS

U zařízení se systémem iOS je potřeba [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to), aby mohla být identita uživatelů ověřena pomocí Azure AD. Kromě toho potřebujete zásadu konfigurace aplikace pro iOS, která nastavuje MTD aplikaci pro iOS, kterou používáte s Intune.

Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi Microsoft Authenticator](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) při konfiguraci **informací o aplikaci**.

## <a name="configure-mtd-applications"></a>Konfigurace aplikací MTD

Vyberte část, která odpovídá vašemu poskytovateli MTD:

- [Lookout for Work](#configure-lookout-for-work-apps)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#configure-symantec-endpoint-protection-mobile-apps)
- [Check Point SandBlast Mobile](#configure-check-point-sandblast-mobile-apps)
- [Zimperium](#configure-zimperium-apps)
- [Pradeo](#configure-pradeo-apps)
- [Better Mobile](#configure-better-mobile-apps)
- [Sophos Mobile](#configure-sophos-apps)
- [Wandera](#configure-wandera-apps)

### <a name="configure-lookout-for-work-apps"></a>Konfigurace aplikací Lookout for Work

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu Google App Storu](https://play.google.com/store/apps/details?id=com.lookout.enterprise) pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Pro **adresu URL AppStore**použijte [Lookout for Work tuto adresu URL obchodu s aplikacemi pro iOS](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) .

- **Aplikace Lookout for Work mimo obchod App Store společnosti Apple**
  - Je nutné znovu podepsat aplikaci Lookout for Work iOS. Lookout distribuuje svou aplikaci Lookout for Work pro iOS mimo obchod App Store. Před distribucí této aplikace ji musíte znovu podepsat pomocí certifikátu podnikového vývojáře pro iOS.  
  - Podrobné pokyny k opětovnému podepsání aplikace Lookout for Work pro iOS najdete v článku [o opětovném podepsání aplikace Lookout for Word pro iOS](https://personal.support.lookout.com/hc/articles/114094038714) na webu Lookout.

  - **Povolení ověřování službou Azure AD v aplikaci Lookout for Work pro iOS uživateli**

    1. Přejděte na [portál Azure Portal](https://portal.azure.com), přihlaste se pomocí svých přihlašovacích údajů a přejděte na stránku aplikace.

    2. Přidejte **aplikaci Lookout for Work pro iOS** jako **nativní klientskou aplikaci**.

    3. Text **com.lookout.enterprise.názevfirmy** nahraďte identifikátorem zákaznického balíčku, který jste vybrali při podepisování IPA.

    4. Přidejte další identifikátor URI pro přesměrování: ** &lt; CompanyPortal://Code/>** následovaný verzí s kódováním URL vašeho původního identifikátoru URI pro přesměrování.

    5. Přidejte k aplikaci **Delegovaná oprávnění**.

    > [!NOTE]
    > Další podrobnosti najdete v článku o [konfiguraci nativní klientské aplikace pomocí Azure AD](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).

  - **Přidání souboru IPA aplikace Lookout for Work**

    - Nahrajte znovu podepsaný soubor. IPA, jak je popsáno v článku [Přidání obchodních aplikací pro iOS do Intune](../apps/lob-apps-ios.md) . Kromě toho je potřeba nastavit jako minimální verzi operačního systému iOS 8.0 nebo novější.

### <a name="configure-symantec-endpoint-protection-mobile-apps"></a>Konfigurace aplikací Symantec Endpoint Protection Mobile

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu s mobilními aplikacemi SEP](https://play.google.com/store/apps/details?id=com.skycure.skycure) pro **adresu URL AppStore**.  Jako **Minimální operační systém** vyberte **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s mobilními aplikacemi SEP](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) pro **adresu URL AppStore**.

### <a name="configure-check-point-sandblast-mobile-apps"></a>Konfigurace aplikací Check Point SandBlast Mobile

- **Android**  
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Pro **adresu URL AppStore**použijte tuto [adresu URL pro SandBlast mobilní aplikace v tomto kontrolním bodě](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) .

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Pro **adresu URL AppStore**použijte tuto [adresu URL pro SandBlast mobilní aplikace v tomto kontrolním bodě](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) .  

### <a name="configure-zimperium-apps"></a>Konfigurace aplikací Zimperium

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Tuto [adresu URL obchodu s aplikacemi Zimperium](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) použijte pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Tuto [adresu URL obchodu s aplikacemi Zimperium](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) použijte pro **adresu URL AppStore**.  
 
### <a name="configure-pradeo-apps"></a>Konfigurace aplikací Pradeo

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Tuto [adresu URL obchodu s aplikacemi Pradeo](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) použijte pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Tuto [adresu URL obchodu s aplikacemi Pradeo](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) použijte pro **adresu URL AppStore**.

### <a name="configure-better-mobile-apps"></a>Konfigurace aplikací Better Mobile

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [aktivní adresu URL obchodu s aplikacemi](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) pro **AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) v programu ActiveShield pro **adresu URL AppStore**.

### <a name="configure-sophos-apps"></a>Konfigurace aplikací Sophos

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu s aplikacemi Sophos](https://play.google.com/store/apps/details?id=com.sophos.smsec) pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) v programu ActiveShield pro **adresu URL AppStore**.

### <a name="configure-wandera-apps"></a>Konfigurace aplikací Wandera

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu Wandera mobilních aplikací](https://play.google.com/store/apps/details?id=com.wandera.android) pro **adresu URL AppStore**. V případě **minimálního operačního systému**vyberte **Android 5,0**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu Wandera mobilních aplikací](https://itunes.apple.com/app/wandera/id605469330) pro **adresu URL AppStore**.

## <a name="configure-your-mtd-apps-with-an-ios-app-configuration-policy"></a>Konfigurace aplikací MTD k zásadám konfigurace aplikace pro iOS

### <a name="lookout-for-work-app-configuration-policy"></a>Zásady konfigurace aplikací pro Lookout for Work

Vytvořte zásady konfigurace aplikace pro iOS, jak je popsáno v článku [použití zásad konfigurace aplikace pro iOS](../apps/app-configuration-policies-use-ios.md) .

### <a name="sep-mobile-app-configuration-policy"></a>Zásady konfigurace aplikace SEP Mobile

Použijte stejný účet Azure AD, který jste dříve nakonfigurovali v [konzole pro správu Symantec Endpoint Protection](https://aad.skycure.com), který by měl být stejný účet, pomocí kterého se přihlašujete k Intune.

- **Stáhněte si** soubor zásad konfigurace aplikace pro iOS:
  - Přejděte na [konzoly pro správu Symantec Endpoint Protection](https://aad.skycure.com) a přihlaste se pomocí svých přihlašovacích údajů správce.

  - Přejděte na **Settings** (Nastavení) a v části **Integrations** (Integrace) zvolte **Intune**. Zvolte **EMM Integration Selection** (Výběr integrace EMM). Zvolte **Microsoft** a pak svůj výběr uložte.

  - Klikněte na odkaz **Integration setup files** (Integrační soubory nastavení) a vygenerovaný soubor \*.zip uložte. Soubor .zip obsahuje soubor ***.plist**, který se použije k vytvoření zásad konfigurace aplikace pro iOS v Intune.

  - Pokud chcete přidat zásady konfigurace aplikace SEP Mobile pro iOS, přečtěte si pokyny ohledně [používání zásad konfigurace aplikací služby Microsoft Intune pro iOS](../apps/app-configuration-policies-use-ios.md).

    - Pro **formát nastavení konfigurace**vyberte **zadat XML data**, zkopírujte obsah ze souboru ***. plist** a vložte jeho obsah do těla zásad konfigurace.

> [!NOTE]
> Pokud se vám nedaří soubory načíst, obraťte se na [podporu Symantec Endpoint Protection Mobile pro firmy](https://support.symantec.com/en_US/contact-support.html).

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Zásady konfigurace aplikace Check Point SandBlast Mobile

Pokud chcete přidat zásady konfigurace aplikace Check Point SandBlast Mobile pro iOS, přečtěte si pokyny ohledně [používání zásad konfigurace aplikací služby Microsoft Intune pro iOS](../apps/app-configuration-policies-use-ios.md).

- Pro **formát nastavení konfigurace**vyberte **zadat XML data**, zkopírujte následující obsah a vložte ho do těla zásad konfigurace.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Zásady konfigurace aplikace Zimperium

Pokud chcete přidat zásady konfigurace aplikace Zimperium pro iOS, přečtěte si pokyny ohledně [používání zásad konfigurace aplikací služby Microsoft Intune pro iOS](../apps/app-configuration-policies-use-ios.md).

- Pro **formát nastavení konfigurace**vyberte **zadat XML data**, zkopírujte následující obsah a vložte ho do těla zásad konfigurace.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Zásady konfigurace aplikace Pradeo

Pradeo nepodporuje zásady konfigurace aplikací pro iOS/iPadOS.  Místo toho, pokud chcete získat nakonfigurovanou aplikaci, pracujte s Pradeo a implementací vlastních souborů IPA nebo APK, které jsou předem nakonfigurované podle požadovaného nastavení.

### <a name="better-mobile-app-configuration-policy"></a>Zásady konfigurace aplikace Better Mobile

Pokud chcete přidat zásady konfigurace aplikace Better Mobile pro iOS, přečtěte si pokyny ohledně [používání zásad konfigurace aplikací služby Microsoft Intune pro iOS](../apps/app-configuration-policies-use-ios.md).

- Pro **formát nastavení konfigurace**vyberte **zadat XML data**, zkopírujte následující obsah a vložte ho do těla zásad konfigurace. Adresu URL `https://client.bmobi.net` nahraďte příslušnou adresou URL konzoly.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Zásady konfigurace mobilních aplikací pro Sophos

Vytvořte zásady konfigurace aplikace pro iOS, jak je popsáno v článku [použití zásad konfigurace aplikace pro iOS](../apps/app-configuration-policies-use-ios.md) . Další informace najdete v tématu [Sophos zachytit X pro mobilní zařízení iOS – dostupné spravované nastavení](https://community.sophos.com/kb/133963) ve znalostní bázi Sophos Knowledge Base.

### <a name="wandera-app-configuration-policy"></a>Zásady konfigurace aplikace Wandera

Pokud chcete přidat zásady konfigurace aplikace Wandera pro iOS, přečtěte si pokyny k používání zásad konfigurace aplikací [Microsoft Intune pro iOS](../apps/app-configuration-policies-use-ios.md) .

- V případě **formátu nastavení konfigurace**vyberte možnost **zadat data XML**.

Přihlaste se k portálu pro paprskový Wandera a přejděte do **Nastavení**  >  **integrace**  >  **aplikace EMM nabízená**instalace. Vyberte **Intune**a potom zkopírujte obsah níže a vložte ho do těla zásad konfigurace.  

  ```
  <dict><key>secretKey</key>
  <string>SeeRADAR</string>
  <key>apiKey</key>
  <string> SeeRADAR </string>
  <key>customerId</key>
  <string> SeeRADAR </string>
  <key>email</key>
  <string>{{mail}}</string>
  <key>firstName</key>
  <string>{{username}}</string>
  <key>lastName</key>
  <string></string>
  <key>activationType</key>
  <string>PROVISION_THEN_AWP</string></dict>
  ```

## <a name="assign-apps-to-groups"></a>Přiřazení aplikací skupinám

Tento krok platí pro všechny partnery MTD. Přečtěte si pokyny pro [přiřazení aplikací do skupin pomocí Intune](../apps/apps-deploy.md).

## <a name="next-steps"></a>Další kroky

- [Konfigurace zásad dodržování předpisů zařízení pro MTD](mtd-device-compliance-policy-create.md)
