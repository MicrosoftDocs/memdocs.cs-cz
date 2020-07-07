---
title: Přidání aplikací ochrany před mobilními hrozbami do neregistrovaných zařízení
titleSuffix: Microsoft Intune
description: Přidejte aplikace ochrany před mobilními hrozbami do zařízení, která uživatelé nezaregistrovali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: f667b6ad9ba9f7c353d89b4d3fc4ff749499bfaf
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972027"
---
# <a name="add-mobile-threat-defense-apps-to-unenrolled-devices"></a>Přidání aplikací ochrany před mobilními hrozbami do neregistrovaných zařízení

Když ve výchozím nastavení používáte zásady ochrany aplikací Intune s ochranou před mobilními hrozbami, Intune dovede koncového uživatele na zařízení, aby nainstaloval a přihlásil se ke všem požadovaným aplikacím, aby umožnil připojení k příslušným službám.

Koncoví uživatelé potřebují k registraci zařízení Microsoft Authenticator (iOS) a ochranu před mobilními hrozbami (Android i iOS), která obdrží oznámení o identifikaci hrozby ve svých mobilních zařízeních a obdržení pokynů k nápravě hrozeb.

Volitelně můžete pomocí Intune přidávat a nasazovat Microsoft Authenticator a taky aplikace pro ochranu před mobilními hrozbami (MTD).

> [!NOTE]
> Tento článek se týká všech partnerů ochrany před mobilními hrozbami, které podporují zásady ochrany aplikací:
>
> - Lepší mobilní zařízení (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS)
> - Wandera (Android, iOS/iPadOS)
> - Zimperium (Android, iOS/iPadOS)

> U neregistrovaných zařízení **nepotřebujete zásady konfigurace aplikace pro iOS** , které nastaví ochranu před mobilními hrozbami pro aplikaci iOS, kterou používáte s Intune. Jedná se o klíčový rozdíl v porovnání s registrovanými zařízeními Intune.

## <a name="configure-microsoft-authenticator-for-ios-via-intune-optional"></a>Konfigurace Microsoft Authenticator pro iOS přes Intune (volitelné)

Pokud používáte zásady ochrany aplikací Intune s ochranou před mobilními hrozbami, Intune bude koncovému uživateli instalovat, přihlašovat se k němu a zaregistrovat zařízení pomocí Microsoft Authenticator (iOS).

Pokud ale chcete, aby byla aplikace k dispozici koncovým uživatelům prostřednictvím Portál společnosti Intune, přečtěte si pokyny, [jak přidat aplikace z obchodu pro iOS do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi Microsoft Authenticator-iOS](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) při dokončování části **Konfigurace informací o aplikaci** . Nezapomeňte v posledním kroku [přiřadit aplikaci do skupin s Intune](../apps/apps-deploy.md) .

> [!NOTE]
> U zařízení se systémem iOS je potřeba [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to), aby mohla být identita uživatelů ověřena pomocí Azure AD. Portál společnosti Intune funguje jako zprostředkovatel na zařízeních s Androidem, aby uživatelé mohli své identity zkontrolovat pomocí Azure AD.

## <a name="making-mobile-threat-defense-apps-available-via-intune-optional"></a>Zpřístupnění aplikací ochrany před mobilními hrozbami přes Intune (volitelné)

Pokud používáte zásady ochrany aplikací Intune s ochranou před mobilními hrozbami, Intune bude koncovému uživateli instalovat a přihlásit se k požadované klientské aplikaci ochrany před mobilními hrozbami.

Pokud ale chcete, aby byla aplikace k dispozici koncovým uživatelům prostřednictvím Portál společnosti Intune, můžete postupovat podle následujících kroků v [Azure Portal](https://portal.azure.com/). Ujistěte se, že jste obeznámeni s procesem:

- [Přidání aplikace do Intune](../apps/apps-add.md)
- [Přiřazení aplikace k Intune](../apps/apps-deploy.md)

### <a name="making-lookout-for-work-available-to-end-users"></a>Umožnění Lookout for Work k dispozici koncovým uživatelům

- **Android**  
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Tuto [adresu URL Lookout for Work-obchod Play](https://play.google.com/store/apps/details?id=com.lookout.enterprise) použijte při dokončování části **Konfigurace informací o aplikaci** .

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi Lookout for Work-iOS](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) při dokončování části **Konfigurace informací o aplikaci** .

<!-- ### Making Symantec Endpoint Protection Mobile available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). When completing the **Configure app information** section, use this [SEP Mobile app store URL](https://play.google.com/store/apps/details?id=com.skycure.skycure). For **Minimum operating system**, select **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SEP Mobile - App Store URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) when completing the **Configure app information** section.

### Making Check Point SandBlast Mobile available to end users
- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Check Point SandBlast Mobile - Play Store URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) when completing the **Configure app information** section. 

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Check Point SandBlast Mobile - App Store URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) when completing the **Configure app information** section. -->

### <a name="making-zimperium-available-to-end-users"></a>Zpřístupnění Zimperium koncovým uživatelům

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Při dokončování části **Konfigurace informací o aplikaci** použijte tuto [adresu Zimperium obchod Play](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) .
- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Tuto [adresu URL obchodu s aplikacemi Zimperium](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) použijte při dokončování části **Konfigurace informací o aplikaci** .

<!-- ### Making Pradeo available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Pradeo - Play Store URL](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Pradeo - App Store URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) when completing the **Configure app information** section. -->

### <a name="making-better-mobile-available-to-end-users"></a>Zpřístupnění lepšího mobilního telefonu koncovým uživatelům

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Tuto [aktivní adresu URL ochrany obchod Play](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) použijte při dokončování části **Konfigurace informací o aplikaci** .

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi v programu ActiveShield –](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) při dokončování části **Konfigurace informací o aplikaci** .

<!-- ### Making Sophos available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Sophos - Play Store URL](https://play.google.com/store/apps/details?id=com.sophos.smsec) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield - App Store URL](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) when completing the **Configure app information** section.  -->

### <a name="making-wandera-available-to-end-users"></a>Zpřístupnění Wandera koncovým uživatelům
- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [Wandera adresu URL mobilního obchod Play](https://play.google.com/store/apps/details?id=com.wandera.android) při dokončování části **Konfigurace informací o aplikaci** .

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Tuto [adresu URL obchodu s mobilními aplikacemi Wandera](https://itunes.apple.com/app/wandera/id605469330) použijte při dokončování části **Konfigurace informací o aplikaci** .

## <a name="next-steps"></a>Další kroky

- [Povolení konektoru ochrany před mobilními hrozbami v Intune pro neregistrovaná zařízení](mtd-enable-unenrolled-devices.md)
