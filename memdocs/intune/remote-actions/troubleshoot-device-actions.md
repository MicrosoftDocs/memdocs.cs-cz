---
title: Řešení potíží s akcemi zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Získejte pomoc s řešením problémů s akcemi zařízení.
keywords: ''
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ROBOTS: ''
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: d5b80cd7c90b7899e25b14c4cb2de1590530f43a
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910804"
---
# <a name="troubleshoot-device-actions-in-intune"></a>Řešení potíží s akcemi zařízení v Intune

Microsoft Intune má mnoho akcí, které vám pomůžou se spravovanými zařízeními. Tento článek obsahuje odpovědi na některé běžné dotazy, které vám můžou pomoct při řešení potíží se zařízením.

## <a name="disable-activation-lock-action"></a>Zakázat Zámek aktivace akci

### <a name="i-clicked-the-disable-activation-lock-action-in-the-portal-but-nothing-happened-on-the-device"></a>Na portálu jsem kliknul na akci zakázat Zámek aktivace, ale na zařízení nic neproběhlo.
To se očekává. Po zahájení akce zakázat Zámek aktivace se službě Intune požádalo o aktualizovaný kód od společnosti Apple. Po zobrazení zařízení na obrazovce Zámek aktivace ručně zadáte kód do pole heslo. Tento kód je platný jenom po dobu 15 dnů, takže nezapomeňte kliknout na akci a zkopírovat kód před tím, než vydáte vymazání.

### <a name="why-dont-i-see-the-disable-activation-lock-code-in-the-hardware-overview-blade-of-my-iosipados-device"></a>Proč se nezobrazuje kód zakázat Zámek aktivace v okně s přehledem hardwaru zařízení s iOS/iPadOS?
K nejpravděpodobnějším důvodům patří:
- Platnost kódu vypršela a byla odstraněna ze služby.
- Zařízení není pod dohledem zásad omezení zařízení, aby bylo možné Zámek aktivace.

Můžete kontrolovat kód v aplikaci Graph Explorer s následujícím dotazem:

```GET - https://graph.microsoft.com/beta/deviceManagement/manageddevices('deviceId')?$select=activationLockBypassCode.```

### <a name="why-is-the-disable-activation-lock-action-greyed-out-for-my-iosipados-device"></a>Proč je akce zakázat Zámek aktivace pro zařízení s iOS/iPadOS šedá?
K nejpravděpodobnějším důvodům patří: 
- Platnost kódu vypršela a byla odstraněna ze služby.
- Zařízení není pod dohledem zásad omezení zařízení, aby bylo možné Zámek aktivace.

### <a name="is-the-disable-activation-lock-code-case-sensitive"></a>Rozlišuje velká a malá písmena Zámek aktivace kódu?
No. A nemusíte zadávat pomlčky.

## <a name="remove-devices-action"></a>Akce odebrání zařízení

### <a name="how-do-i-tell-who-started-a-retirewipe"></a>Návody informovat, kdo zahájil vyřazení/vymazání?
V centru pro [správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)přejdete do **Tenant administration**části  >  **protokoly auditu** správy tenanta > zkontrolujte **iniciované** sloupce.
Pokud položku nevidíte, nejpravděpodobnější osoba, která iniciovala tuto akci, je uživatel tohoto zařízení. Pravděpodobně použili Portál společnosti aplikaci nebo portal.manage.microsoft.com.

### <a name="why-wasnt-my-application-uninstalled-after-using-retire"></a>Proč se mi po použití vyřazení nenainstalovala moje aplikace?
Protože není považována za spravovanou aplikaci. V tomto kontextu je spravovaná aplikace aplikace, která byla nainstalována pomocí služby Intune. Sem patří:
- Aplikace se nasadila jako povinná.
- Aplikace byla nasazená jako dostupná a pak koncovým uživatelem nainstalovaná v aplikaci Portál společnosti.

### <a name="why-is-wipe-grayed-out-for-android-enterprise-work-profile-devices"></a>Proč je pro zařízení se systémem Android Enterprise Work profilování vymazáno šedé?
Toto chování je očekávané. Google neumožňuje obnovení továrního nastavení zařízení pracovního profilu od poskytovatele MDM.

### <a name="why-can-i-sign-back-into-my-office-apps-after-my-device-was-retired"></a>Proč se můžu po vyřazení zařízení do aplikací Office přihlásit zpátky?
Protože vyřazení zařízení z provozu neodvolává přístupové tokeny. Pomocí zásad podmíněného přístupu můžete zmírnit tuto podmínku.

### <a name="how-can-i-monitor-a-retirewipe-action-after-it-was-issued"></a>Jak můžu monitorovat akci vyřazení/vymazání po jejím vydání?
V centru pro [správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)přejdete do **Tenant administration**části  >  **protokoly auditu**správy tenanta.

### <a name="why-do-wipes-sometimes-show-as-pending-indefinitely"></a>Proč se vymazání někdy zobrazuje na neomezenou dobu?
Zařízení před zahájením resetování vždy hlásí svůj stav zpět do služby Intune. Proto se akce zobrazí jako čeká na vyřízení. Pokud jste ověřili, že se akce úspěšně provedla, odstraňte zařízení ze služby.

### <a name="what-happens-if-i-start-a-retirewipe-on-an-offline-device-or-a-device-that-hasnt-communicated-with-the-service-in-a-while"></a>Co se stane, když jsem při spuštění vyřazení z provozu nebo vymazání na zařízení v režimu offline nebo zařízení, které nekomunikovalo se službou
Zařízení zůstane ve stavu **vyřazení/vymazání** , dokud nevyprší platnost certifikátu MDM. Certifikát MDM trvá po dobu jednoho roku od registrace a automaticky obnovuje každý rok. Pokud zařízení zkontroluje, než vyprší platnost certifikátu MDM, bude vyřazení/vymazání. Pokud zařízení nevrací se změnami do vypršení platnosti certifikátu MDM, nebude se moct vrátit ke službě. 180 dní po vypršení platnosti certifikátu MDM se zařízení automaticky odebere z Azure Portal.


## <a name="reset-passcode-action"></a>Akce resetovat heslo

### <a name="why-is-the-reset-passcode-action-greyed-out-on-my-android-device-admin-enrolled-device"></a>Proč se akce resetování hesla na zařízení s registrací Správce zařízení s Androidem šedá?
V případě boje proti Ransom z obchodu Google odebrala funkce resetování hesla v rozhraní API pro správu zařízení (platí pro zařízení s Androidem verze 7,0 nebo vyšší).

### <a name="why-do-i-get-a-not-supported-message-when-i-issue-a-passcode-reset-to-my-android-80-or-later-work-profile-enrolled-device"></a>Proč se mi zobrazuje zpráva "Nepodporovaná", když vydávám resetování hesla na zařízení se systémem Android 8,0 nebo novějším zaregistrovaným pracovním profilem?
Protože token resetování nebyl v zařízení aktivován. Aktivace tokenu resetování:
1. V zásadách konfigurace musíte vyžadovat heslo k pracovnímu profilu.
2. Koncový uživatel musí nastavit vhodný přístupový kód pracovního profilu.
3. Koncový uživatel musí přijmout sekundární výzvu, aby bylo možné resetování hesla.
Po dokončení těchto kroků už tuto odpověď nebudete dostávat.

### <a name="why-am-i-prompted-to-set-a-new-passcode-on-my-iosipados-device-when-i-issue-the-remove-passcode-action"></a>Proč se mi při vystavování akce odebrat heslo zobrazí výzva k nastavení nového hesla na zařízení se systémem iOS/iPadOS?
Vzhledem k tomu, že jedna ze zásad dodržování předpisů vyžaduje heslo.


## <a name="wipe-action"></a>Akce vymazání

### <a name="i-cant-restart-a-windows-10-device-after-using-the-wipe-action"></a>Po použití akce vymazání nejde restartovat zařízení s Windows 10.
To může být způsobeno tím, že použijete **zařízení pro vymazání a chcete pokračovat v mazání i v případě, že zařízení ztratí napájení. Pokud vyberete tuto možnost, uvědomte si, že může dojít k tomu, že se některá zařízení s Windows 10 nespustí znovu.** na zařízení s Windows 10.

To může být způsobeno tím, že instalace systému Windows má zásadní poškození, které brání přeinstalaci operačního systému. V takovém případě se proces nezdařil a opustí systém v [prostředí Windows Recovery Environment]( /windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

### <a name="i-cant-restart-a-bitlocker-encrypted-device-after-using-the-wipe-action"></a>Po použití akce vymazání nejde restartovat zařízení zašifrované BitLockerem
To může být způsobeno tím, že použijete **zařízení pro vymazání a chcete pokračovat v mazání i v případě, že zařízení ztratí napájení. Pokud vyberete tuto možnost, uvědomte si, že může dojít k tomu, že se některá zařízení s Windows 10 nespustí znovu.** možnost na zařízení šifrované pomocí BitLockeru.

Pokud chcete tento problém vyřešit, na zařízení znovu nainstalujte Windows 10 pomocí spouštěcího média.


## <a name="next-steps"></a>Další kroky

Získejte pomoc [od Microsoftu](../fundamentals/get-support.md)nebo využijte [komunitní fóra](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).