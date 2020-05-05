---
title: Registrace vyhrazených zařízení s Androidem Enterprise nebo plně spravovaných zařízení v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak v Intune zaregistrovat podniková vyhrazená zařízení s Androidem nebo plně spravovaná zařízení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0913937714b59aca56c1e61fabe9d8154b6d4d24
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149139"
---
# <a name="enroll-your-android-enterprise-dedicated-devices-or-fully-managed-devices"></a>Registrace vyhrazených zařízení s Androidem Enterprise nebo plně spravovaných zařízení

Po nastavení [podnikových vyhrazených zařízení s Androidem](android-kiosk-enroll.md) nebo [plně spravovaných zařízení](android-fully-managed-enroll.md) v Intune můžete zařízení zaregistrovat. Registrace v Intune pro vyhrazená zařízení i pro plně spravovaná zařízení začíná Obnovením továrního nastavení. Způsob registrace zařízení s Androidem Enterprise závisí na operačním systému.

| Způsob registrace | Minimální verze operačního systému Android pro vyhrazená a plně spravovaná zařízení |
| ----- | ----- |
| Bezkontaktní komunikace (NFC) | 6.0 |
| Zadání tokenu | 6.0 |
| Kód QR | 7.0 |
| Zero Touch  | 8.0<br><br> U zúčastněných výrobců. |
| [Registrace pro mobilní zařízení Knox](https://docs.microsoft.com/mem/intune/enrollment/android-samsung-knox-mobile-enroll)  | 6.0<br><br> Jenom na zařízeních Samsung KNOX 2,8 nebo vyšších. |

## <a name="enroll-by-using-near-field-communication-nfc"></a>Registrace pomocí bezkontaktní komunikace (NFC)

U zařízení 6 a novějších, která podporují NFC, můžete zařízení zřídit vytvořením speciálně formátované značky NFC. Můžete použít svou vlastní aplikaci nebo nástroj pro vytváření značek NFC. Další informace najdete v dokumentaci k [registraci zařízení se systémem Android Enterprise v jazyce C s Microsoft Intune](https://blogs.technet.microsoft.com/cbernier/2018/10/15/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune/) a v [dokumentaci k rozhraní API pro správu Androidu](https://developers.google.com/android/management/provision-device#nfc_method).

## <a name="enroll-by-using-a-token"></a>Registrace pomocí tokenu

U zařízení s Androidem 6 a vyšším můžete k registraci zařízení použít token. Android 6,1 a novější verze mohou také využít kontrolu kódu QR při použití metody registrace **AFW # Setup** .

1. Zapněte vymazané zařízení.
2. Na **uvítací** obrazovce vyberte svůj jazyk.
3. Připojte se k **Wi-Fi** síti a zvolte **DALŠÍ**.
4. Přijměte podmínky a ujednání Googlu a zvolte **DALŠÍ**.
5. Na obrazovce pro přihlášení ke Googlu zadejte místo účtu Google text **afw#setup** a zvolte **DALŠÍ**.
6. U aplikace **Android Device Policy** zvolte **NAINSTALOVAT**.
7. Pokračujte v instalaci těchto zásad.  Některá zařízení můžou vyžadovat přijetí dodatečných podmínek.
8. Na obrazovce **Zaregistrovat toto zařízení** umožněte zařízení naskenovat kód QR nebo zvolte ruční zadání tokenu.
9. Podle pokynů na obrazovce dokončete registraci.

## <a name="enroll-by-using-a-qr-code"></a>Registrace pomocí kódu QR

Zařízení s Androidem 7 a vyšším můžete zaregistrovat naskenováním kódu QR z registračního profilu.

> [!Note]
> Zvětšení v prohlížeči může způsobit, že zařízení nebudou moct naskenovat kód QR. Tento problém se dá vyřešit zvýšením zvětšení v prohlížeči.

1. Čtení kódu QR spustíte na zařízení s Androidem tak, že několikrát klepnete na první obrazovku, kterou uvidíte po vymazání.
2. U zařízení s Androidem 7 a 8 budete vyzváni k instalaci čtečky kódů QR. Zařízení s Androidem 9 a vyšším už mají čtečku kódů QR nainstalovanou.
3. Pomocí čtečky kódů QR naskenujte kód QR registračního profilu a podle pokynů na obrazovce se zaregistrujte.

## <a name="enroll-by-using-google-zero-touch"></a>Registrace pomocí systému Google Zero Touch

Abyste mohli použít systém Zero Touch od Googlu, musí ho zařízení podporovat a být spřažené s dodavatelem, který je součástí této služby.  Další informace najdete v tématu [web s nulovým dotykovým programem Google](https://www.android.com/enterprise/management/zero-touch/).

1. Vytvořte novou konfiguraci v konzole Zero Touch.
2. V rozevíracím seznamu EMM DPC zvolte **Microsoft Intune**.
3. V konzole pro nulové dotykové ovládání Google zkopírujte nebo vložte následující JSON do pole DPC Extras. Řetězec *YourEnrollmentToken* nahraďte registračním tokenem, který jste vytvořili jako součást registračního profilu. Nezapomeňte registrační token uzavřít do dvojitých uvozovek.

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
        }
    }
    ```

4. Zvolte **Použít**.

## <a name="enroll-by-using-knox-mobile-enrollment"></a>Registrovat pomocí zápisu pro mobilní zařízení Knox
Pokud chcete použít registraci mobilního telefonu Samsung v Samsung, musí na zařízení běžet Android OS verze 6 nebo novější a Samsung KNOX 2,8 nebo vyšší. Další informace najdete v tématu [Automatická registrace zařízení pomocí služby Knox Mobile Enrollment](https://docs.microsoft.com/mem/intune/enrollment/android-samsung-knox-mobile-enroll).

## <a name="next-steps"></a>Další kroky
- [Nasazení aplikací pro Android](../apps/apps-deploy.md)
- [Přidat zásady konfigurace pro Android](../configuration/device-profiles.md)

