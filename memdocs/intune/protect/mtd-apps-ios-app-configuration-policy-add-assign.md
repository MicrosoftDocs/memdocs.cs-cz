---
title: Přidání a přiřazení aplikací pro ochranu před mobilními hrozbami (MTD) do Microsoft Intune
titleSuffix: Microsoft Intune
description: Pomocí Intune můžete přidat aplikace pro ochranu před mobilními hrozbami (MTD), aplikaci Microsoft Authenticator a zásady konfigurace iOS na portálu Azure Portal.
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
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03dbdccd1626db5ad97bc230a3d6b9a82060ee2e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590486"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Přidání a přiřazení aplikací pro ochranu před mobilními hrozbami (MTD) pomocí Intune

Pomocí Intune můžete přidávat a nasazovat aplikace pro ochranu před mobilními hrozbami (MTD), aby koncoví uživatelé mohli dostávat oznámení, když se v jejich mobilních zařízeních identifikuje hrozba, a získat pokyny k nápravě hrozeb.

> [!NOTE]
> Tento článek se týká všech partnerů ochrany před mobilními hrozbami.

## <a name="before-you-begin"></a>Než začnete

V Intune proveďte následující kroky. Ujistěte se, že jste obeznámeni s procesem:

- [Přidání aplikace do služby Intune](../apps/apps-add.md)
- [Přidání zásad konfigurace aplikace pro iOS do služby Intune](../apps/app-configuration-policies-use-ios.md)
- [Přiřazení aplikace pomocí služby Intune](../apps/apps-deploy.md)

> [!TIP]
> Portál společnosti Intune funguje jako zprostředkovatel na zařízeních s Androidem, aby uživatelé mohli své identity zkontrolovat pomocí Azure AD.

## <a name="configure-microsoft-authenticator-for-ios"></a>Konfigurace aplikace Microsoft Authenticator pro iOS

U zařízení se systémem iOS je potřeba [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to), aby mohla být identita uživatelů ověřena pomocí Azure AD. Kromě toho potřebujete zásadu konfigurace aplikace pro iOS, která nastavuje MTD aplikaci pro iOS, kterou používáte s Intune.

Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi Microsoft Authenticator](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) při konfiguraci **informací o aplikaci**.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>Konfigurace aplikací MTD pomocí zásad konfigurace aplikace

Aby bylo možné zjednodušit registraci uživatelů, aplikace ochrany před mobilními hrozbami na zařízeních spravovaných MDM používají konfiguraci aplikace. V případě neregistrovaných zařízení není konfigurace aplikace založená na MDM dostupná, proto prosím přečtěte si téma [Přidání aplikací ochrany před mobilními hrozbami do neregistrovaných zařízení](../protect/mtd-add-apps-unenrolled-devices.md).

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

> [!NOTE]
> Při počátečním testování použijte testovací skupinu při přiřazování uživatelů a zařízení v části přiřazení v zásadách konfigurace. 

- **Android**
  - V pokynech k [použití Microsoft Intune zásady konfigurace aplikací pro Android](../apps/app-configuration-policies-use-android.md) přidejte zásady konfigurace aplikací pro Android Wandera pomocí informací uvedených níže po zobrazení výzvy.

1. Na **portálu Wandera pro paprsky**klikněte na tlačítko **Přidat +** v části formát **nastavení konfigurace** .
2. V seznamu **konfiguračních klíčů**vyberte **URL aktivačního profilu** . Klikněte na **OK**.
3. V poli **Adresa URL profilu aktivace** vyberte **řetězec** z nabídky **typ hodnoty** a pak zkopírujte a vložte **adresu URL odkazu ke sdílení** z požadovaného aktivačního profilu v paprsku.
4. V **Nastavení**definujte **formát nastavení konfigurace > použijte návrháře konfigurace** a postupujte podle následujících kroků.

> [!NOTE] 
> Na rozdíl od iOS budete muset pro každý Wandera aktivační profil definovat jedinečnou zásadu konfigurace podnikových aplikací pro Android. Pokud nepotřebujete více profilů aktivace Wandera, můžete pro všechna cílová zařízení použít jednu konfiguraci aplikace pro Android. Při vytváření profilů aktivace v Wandera nezapomeňte v přidružené konfiguraci uživatele vybrat Azure Active Directory, abyste zajistili, že Wandera bude moct synchronizovat zařízení s Microsoft Endpoint Managerem přes UEM Connect.

- **iOS**
  - V pokynech k [použití Microsoft Intune zásad konfigurace aplikací pro iOS](../apps/app-configuration-policies-use-ios.md) můžete přidat zásady konfigurace aplikace Wandera pro iOS pomocí informací uvedených níže po zobrazení výzvy.

1. V **paprskovém portálu Wandera**přejděte na **zařízení > aktivace** a vyberte libovolný aktivační profil. Klikněte na **strategie nasazení > spravovaná zařízení > Microsoft Intune** a vyhledejte **nastavení konfigurace aplikace pro iOS**.  
2. Rozbalením tohoto pole zobrazíte soubor XML konfigurace aplikace pro iOS a zkopírujete ho do systémové schránky.  
3. V **Nastavení** definujte **formát nastavení konfigurace > zadejte XML data** a postupujte podle následujících kroků:
4. Vložte XML do textového pole konfigurace aplikace ve službě Microsoft Endpoint Manager.

> [!NOTE]
> U všech zařízení, která se mají zřídit pomocí Wandera, se dají použít jedna zásada konfigurace pro iOS.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Přiřazení aplikací ochrany před mobilními hrozbami koncovým uživatelům přes Intune

Chcete-li nainstalovat aplikaci ochrany před mobilními hrozbami na zařízení koncového uživatele, můžete postupovat podle následujících kroků v Azure Portal. Ujistěte se, že jste obeznámeni s procesem:

- [Přiřazení aplikací do skupin pomocí Intune](../apps/apps-deploy.md)

Vyberte část, která odpovídá vašemu poskytovateli MTD:

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Přiřazuje se Lookout for Work

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

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Přiřazení Symantec Endpoint Protection Mobile

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu s mobilními aplikacemi SEP](https://play.google.com/store/apps/details?id=com.skycure.skycure) pro **adresu URL AppStore**.  Jako **Minimální operační systém** vyberte **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s mobilními aplikacemi SEP](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) pro **adresu URL AppStore**.

### <a name="assigning-check-point-sandblast-mobile"></a>Přiřazuje se Check Point SandBlast Mobile

- **Android**  
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Pro **adresu URL AppStore**použijte tuto [adresu URL pro SandBlast mobilní aplikace v tomto kontrolním bodě](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) .

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Pro **adresu URL AppStore**použijte tuto [adresu URL pro SandBlast mobilní aplikace v tomto kontrolním bodě](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) .  

### <a name="assigning-zimperium"></a>Přiřazuje se Zimperium

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Tuto [adresu URL obchodu s aplikacemi Zimperium](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) použijte pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Tuto [adresu URL obchodu s aplikacemi Zimperium](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) použijte pro **adresu URL AppStore**.  
 
### <a name="assigning-pradeo"></a>Přiřazuje se Pradeo

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Tuto [adresu URL obchodu s aplikacemi Pradeo](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) použijte pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Tuto [adresu URL obchodu s aplikacemi Pradeo](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) použijte pro **adresu URL AppStore**.

### <a name="assigning-better-mobile"></a>Přiřazovat lepší mobilní zařízení

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [aktivní adresu URL obchodu s aplikacemi](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) pro **AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) v programu ActiveShield pro **adresu URL AppStore**.

### <a name="assigning-sophos"></a>Přiřadí se Sophos

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu s aplikacemi Sophos](https://play.google.com/store/apps/details?id=com.sophos.smsec) pro **adresu URL AppStore**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu s aplikacemi](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) v programu ActiveShield pro **adresu URL AppStore**.

### <a name="assigning-wandera"></a>Přiřazuje se Wandera

- **Android**
  - Přečtěte si pokyny pro [přidávání aplikací z Android Storu do Microsoft Intune](../apps/store-apps-android.md). Použijte tuto [adresu URL obchodu Wandera mobilních aplikací](https://play.google.com/store/apps/details?id=com.wandera.android) pro **adresu URL AppStore**. V případě **minimálního operačního systému**vyberte **Android 5,0**.

- **iOS**
  - Přečtěte si pokyny pro [přidávání aplikací z iOS Storu do Microsoft Intune](../apps/store-apps-ios.md). Použijte tuto [adresu URL obchodu Wandera mobilních aplikací](https://itunes.apple.com/app/wandera/id605469330) pro **adresu URL AppStore**.

## <a name="next-steps"></a>Další kroky

- [Konfigurace zásad dodržování předpisů zařízení pro MTD](mtd-device-compliance-policy-create.md)
