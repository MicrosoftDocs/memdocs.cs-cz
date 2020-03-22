---
title: Použití protokolů StageNow na zařízeních s Androidem Zebra v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na časté problémy a řešení při použití StageNow na zařízeních s Androidem s Microsoft Intune. Dozvíte se taky, jak získat protokoly, a podívejte se na příklady, jak číst protokoly pro úspěch nebo chyby.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 607e2303cbec9ec7fc069db602d51684b71e6575
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083832"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Řešení potíží a zobrazení potenciálních problémů na zařízeních s Androidem Zebra v Microsoft Intune



V Microsoft Intune můžete [ke správě zařízení se systémem Android Zebra použít rozšíření Zebra mobility (MX)](android-zebra-mx-overview.md). Při používání zařízení Zebra vytvoříte profily v StageNow pro správu nastavení a nahrajete je do Intune. Intune používá aplikaci StageNow k použití nastavení na zařízeních. Aplikace StageNow také na zařízení, které se používá k odstraňování potíží, vytvoří podrobný soubor protokolu.

Tato funkce platí pro:

- Android

Můžete například vytvořit profil v StageNow a nakonfigurovat zařízení. Při vytváření profilu StageNow vygeneruje poslední krok soubor pro otestování profilu. Tento soubor spotřebujete na zařízení pomocí aplikace StageNow.

V jiném příkladu vytvoříte profil v StageNow a otestujete ho. V Intune přidejte profil StageNow a přiřaďte ho k zařízením zebra. Při kontrole stavu přiřazeného profilu zobrazuje profil stav vysoké úrovně.

V obou těchto případech můžete získat další podrobnosti ze souboru protokolu StageNow, který je uložený v zařízení pokaždé, když se použije profil StageNow.

Některé problémy nesouvisejí s obsahem profilu StageNow a nereflektují se v protokolech.

V tomto článku se dozvíte, jak číst protokoly StageNow a uvádí další možné problémy se zařízeními Zebra, která se nemusí odrazit v protokolech.

Další informace o této funkci najdete v [Zebra zařízeních s rozšířeními Zebra mobility](android-zebra-mx-overview.md) .

## <a name="get-the-logs"></a>Získat protokoly

### <a name="use-the-stagenow-app-on-the-device"></a>Použití aplikace StageNow na zařízení
Když otestujete profil přímo pomocí StageNow na počítači v systému, místo použití [Intune k nasazení profilu](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow)aplikace StageNow na zařízení uloží protokoly z testu. K získání souboru protokolu použijte možnost **Další (...)** v aplikaci StageNow na zařízení.

### <a name="get-logs-using-android-debug-bridge"></a>Získání protokolů pomocí Android Debug Bridge
Pokud chcete získat protokoly, až bude profil už nasazený pomocí Intune, připojte ho k počítači s [Android Debug Bridge (ADB)](https://developer.android.com/studio/command-line/adb) (otevře se web Androidu).

V zařízení jsou protokoly uložené v `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>Získat protokoly z e-mailu
Aby se protokoly dostaly po nasazení profilu s Intune, můžou koncoví uživatelé odeslat e-mailem protokoly pomocí e-mailové aplikace na zařízení. Na zařízení Zebra otevřete aplikaci Portál společnosti a [odešlete protokoly](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android). Pomocí funkce Odeslat protokoly vytvoří také ID incidentu PowerLift, na které můžete odkazovat, pokud se obrátíte na podporu Microsoftu.

## <a name="read-the-logs"></a>Přečtěte si protokoly

Při prohlížení protokolů dojde k chybě vždy, když se zobrazí značka `<characteristic-error>`. Podrobnosti o chybě se zapisují do `<parm-error>` značky > vlastnosti `desc`.

## <a name="error-types"></a>Typy chyb

Zařízení Zebra zahrnují různé úrovně zasílání zpráv o chybách:

- Zprostředkovatel kryptografických služeb není na zařízení podporován. Nejedná se třeba o mobilní zařízení, které nemá mobilního manažera.
- Verze MX nebo OSX se neshodují. Každý CSP má verzi. Celou matrici podpory najdete v [dokumentaci k Zebra](http://techdocs.zebra.com/mx/) (otevření webu Zebra).
- Zařízení nahlásí jiný problém nebo chybu.

## <a name="examples"></a>Příklady

Máte například následující vstupní profil:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

V protokolu je kód XML totožný se vstupem. Tento shodný výstup znamená, že se profil úspěšně nastavil na zařízení bez chyb:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

V jiném příkladu máte následující vstup:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

V protokolu se zobrazí chyba, protože obsahuje značku `<characteristic-error>`. V tomto scénáři se profil pokusil nainstalovat balíček pro Android (APK), který v dané cestě neexistuje:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Další možné problémy se zařízeními Zebra

V této části jsou uvedené další možné problémy, se kterými se můžete setkat při používání zařízení Zebra se správcem zařízení. Tyto problémy nejsou hlášeny v protokolech StageNow.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView je zastaralá.

Když se starší zařízení přihlásí pomocí aplikace Portál společnosti, můžou se uživatelům zobrazit zpráva, že komponenta System WebView je zastaralá a potřebuje upgradovat. Pokud je zařízení nainstalované Google Play, připojte ho k Internetu a vyhledejte aktualizace. Pokud zařízení nemá nainstalované Google Play, získejte aktualizovanou verzi komponenty a použijte ji pro zařízení. Nebo aktualizujte na nejnovější operační systém zařízení vydaný nástrojem zebra.

### <a name="management-actions-take-a-long-time"></a>Akce správy trvají dlouhou dobu.

Pokud služby Google Play Services nejsou k dispozici, dokončení některých úloh trvá až 8 hodin. [Omezení portál společnosti Intune aplikace pro Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (otevře jiný web společnosti Microsoft) může být dobrým prostředkem.

### <a name="device-spoofing-suspected-shows-in-intune"></a>V Intune se zobrazuje "podezření na falšování zařízení"

Tato chyba znamená, že Intune předpokládá, že zařízení s Androidem, které není Zebra, hlásí svůj model a výrobce jako zařízení zebra.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>Portál společnosti aplikace je starší než minimální požadovaná verze.

Intune může aktualizovat minimální požadovanou verzi Portál společnosti aplikace. Pokud v zařízení není nainstalovaná Google Play, Portál společnosti aplikace se automaticky neaktualizuje. Pokud je minimální požadovaná verze novější než nainstalovaná verze, aplikace Portál společnosti přestane fungovat. Aktualizujte na nejnovější aplikaci Portál společnosti pomocí [zkušebního načtení na zařízeních Zebra](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Další kroky

[Diskuzní vývěsky Zebra](https://developer.zebra.com/community/home/discussions) (otevře web Zebra)

[Používání a Správa zařízení Zebra s rozšířeními mobility Zebra v Intune](android-zebra-mx-overview.md)
