---
title: Řešení potíží s registrací zařízení s iOS nebo iPadOS v Microsoft Intune
titleSuffix: Microsoft Intune
description: Návrhy pro řešení některých nejběžnějších problémů při registraci zařízení se systémem iOS nebo iPadOS v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/18/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e4d3e150e8e4ed890de4717c6093104e2b49d1f
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/26/2020
ms.locfileid: "80274876"
---
# <a name="troubleshoot-iosipados-device-enrollment-problems-in-microsoft-intune"></a>Řešení potíží s registrací zařízení s iOS nebo iPadOS v Microsoft Intune

Tento článek pomáhá správcům Intune pochopit a řešit problémy při registraci zařízení se systémem iOS nebo iPadOS v Intune.

## <a name="prerequisites"></a>Požadavky

Než začnete řešit potíže, je důležité shromáždit některé základní informace. Tyto informace vám pomůžou lépe porozumět problému a zkrátit dobu, po kterou je možné najít řešení.

Shromážděte následující informace o problému:

- Jaká je přesná chybová zpráva?
- Kde se zobrazí chybová zpráva?
- Kdy problém začal? Byl zápis někdy zpracován?
- Jakou platformu (Android, iOS/iPadOS, Windows) má problém?
- Kolika uživatelů se to týká? Ovlivnili všichni uživatelé nebo jen některé?
- Kolik zařízení je ovlivněno? Jsou všechna zařízení ovlivněná nebo jenom některá?
- Co je Autorita MDM?
- Jak se provádí registrace? Znamená to, že vlastní zařízení (BYOD) nebo Apple automatického zápisu zařízení (ADE) pomocí registračních profilů?

## <a name="error-messages"></a>Chybovými zprávami

### <a name="profile-installation-failed-a-network-error-has-occurred"></a>Instalace profilu se nezdařila. Došlo k chybě sítě.

**Příčina:** Došlo k nespecifikovanému problému se systémem iOS nebo iPadOS na zařízení.

#### <a name="resolution"></a>Rozlišení

1. Aby nedošlo ke ztrátě dat v následujících krocích (obnovení iOS/iPadOS odstraní všechna data v zařízení), ujistěte se, že zálohujete data.
2. Zařízení umístěte do režimu obnovení a pak ho obnovte. Ujistěte se, že jste ji nastavili jako nové zařízení. Další informace o tom, jak obnovit zařízení s iOS/iPadOS, najdete v tématu [https://support.apple.com/HT201263](https://support.apple.com/HT201263).
3. Zařízení znovu zaregistrujte.

### <a name="profile-installation-failed-connection-to-the-server-could-not-be-established"></a>Instalace profilu se nezdařila. Nepovedlo se navázat spojení se serverem.

**Příčina:** Váš tenant Intune je nakonfigurovaný tak, aby povoloval jenom zařízení vlastněná společností. 

#### <a name="resolution"></a>Rozlišení
1. Přihlaste se k portálu Azure Portal.
2. Vyberte **Další služby**, vyhledejte Intune a pak vyberte **Intune**.
3. Zvolte **Registrace zařízení** > **Omezení registrace**.
4. V části **omezení typů zařízení**vyberte omezení, které chcete nastavit > **vlastnosti** > **vyberte platformy** > vyberte možnost **Povolení** pro **iOS**a pak klikněte na **OK**.
5. Vyberte **Konfigurovat platformy**, vyberte možnost **povoleno** pro zařízení s iOS a iPadOS v osobním vlastnictví a pak klikněte na **OK**.
6. Zařízení znovu zaregistrujte.

**Příčina:** Nezbytné záznamy CNAME v DNS neexistují.

#### <a name="resolution"></a>Rozlišení
Vytvořte záznamy o prostředcích DNS CNAME pro doménu vaší společnosti. Pokud je například doména vaší společnosti contoso.com, vytvořte ve službě DNS záznam CNAME, který přesměruje EnterpriseEnrollment.contoso.com na EnterpriseEnrollment-s.manage.microsoft.com.

Vytváření položek CNAME DNS není povinné, ale záznamy CNAME usnadňují uživatelům registraci. Pokud se nenajde žádný záznam CNAME pro registraci, zobrazí se uživatelům výzva, aby ručně zadali název serveru MDM: enrollment.manage.microsoft.com.

Pokud existuje více než jedna ověřená doména, vytvořte záznam CNAME pro každou doménu. Záznamy o prostředcích CNAME musí obsahovat tyto informace:

|TYP|Název hostitele|Odkazuje na|Hodnota TTL|
|------|------|------|------|
|CNAME|EnterpriseEnrollment.doména_společnosti.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hr|
|CNAME|EnterpriseRegistration.doména_společnosti.com|EnterpriseRegistration.windows.net|1 hr|

Pokud vaše společnost používá více domén pro přihlašovací údaje uživatelů, vytvořte záznamy CNAME pro každou doménu.

> [!NOTE]
> Změny záznamů DNS se mohou projevit až po 72 hodinách. Před rozšířením záznamu DNS nemůžete v Intune ověřit změnu DNS.

**Příčina:** Zaregistrujete zařízení, které bylo dříve zaregistrováno pod jiným uživatelským účtem, a předchozí uživatel nebyl ze služby Intune odpovídajícím způsobem odebrán.

#### <a name="resolution"></a>Rozlišení
1. Zruší všechny aktuální instalace profilu.
2. Otevřete [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) v Safari.
3. Zařízení znovu zaregistrujte.

> [!NOTE]
> Pokud se registrace stále nezdařila, odeberte soubory cookie v Safari (neblokovat soubory cookie) a pak zařízení znovu zaregistrujte.

**Příčina:** Zařízení je už zaregistrované pomocí jiného poskytovatele MDM.

#### <a name="resolution"></a>Rozlišení
1. Otevřete **Nastavení** na zařízení se systémem iOS/iPadOS, kde najdete **Obecné > Správa zařízení**.
2. Odeberte všechny stávající profily správy.
3. Zařízení znovu zaregistrujte.

**Příčina:** Uživatel, který se pokouší zaregistrovat zařízení, nemá licenci Microsoft Intune.

#### <a name="resolution"></a>Rozlišení
1. Přejít do [centra pro správu Office 365](https://admin.microsoft.com)a pak zvolte **Uživatelé > aktivní uživatelé**.
2. Vyberte uživatelský účet, kterému chcete přiřadit uživatelskou licenci pro Intune, a pak zvolte licence na **produkty > upravit**.
3. Přepněte přepínač **na pozici pro** licenci, kterou chcete tomuto uživateli přiřadit, a pak zvolte **Uložit**.
4. Zařízení znovu zaregistrujte.

### <a name="this-service-is-not-supported-no-enrollment-policy"></a>Tato služba se nepodporuje. Žádné zásady registrace.

**Příčina**: certifikát Apple MDM push Certificate není v Intune nakonfigurovaný, nebo je certifikát neplatný. 

#### <a name="resolution"></a>Rozlišení

- Pokud není nabízený certifikát MDM nakonfigurovaný, postupujte podle kroků v části [získání certifikátu Apple MDM push Certificate](apple-mdm-push-certificate-get.md#steps-to-get-your-certificate).
- Pokud je certifikát MDM push Certificate neplatný, postupujte podle kroků v části [obnovení certifikátu Apple MDM push Certificate](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).

### <a name="company-portal-temporarily-unavailable-the-company-portal-app-encountered-a-problem-if-the-problem-persists-contact-your-system-administrator"></a>Portál společnosti dočasně nedostupné. V aplikaci Portál společnosti došlo k problému. Pokud potíže potrvají, obraťte se na správce systému.

**Příčina:** Aplikace Portál společnosti není aktuální nebo je poškozená.

#### <a name="resolution"></a>Rozlišení
1. Odeberte ze zařízení aplikaci Portál společnosti.
2. Stáhněte si a nainstalujte aplikaci **Microsoft Intune portál společnosti** z **App Storu**.
3. Zařízení znovu zaregistrujte.
 > [!NOTE]
    > K této chybě může dojít také v případě, že se uživatel pokouší zaregistrovat více zařízení, než je registrace zařízení nakonfigurovaná tak, aby povolovala. Pokud tyto kroky problém nevyřeší, postupujte podle kroků v části řešení pro limit **zařízení** .

### <a name="device-cap-reached"></a>Bylo dosaženo limitu zařízení

**Příčina:** Uživatel se pokusí zaregistrovat více zařízení, než je limit pro registraci zařízení.

#### <a name="resolution"></a>Rozlišení
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **všechna zařízení**a ověřte počet zařízení, která uživatel zaregistroval.
    > [!NOTE]
    > Měli byste také mít vliv na přihlášení ovlivněného uživatele na [uživatelský portál Intune](https://portal.manage.microsoft.com/) a ověřit zařízení, která jsou zaregistrovaná. Můžou existovat zařízení, která se zobrazují na [uživatelském portálu Intune](https://portal.manage.microsoft.com/) , ale ne na [portálu pro správu Intune](https://portal.azure.com/?Microsoft_Intune=1&Microsoft_Intune_DeviceSettings=true&Microsoft_Intune_Enrollment=true&Microsoft_Intune_Apps=true&Microsoft_Intune_Devices=true#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview). Tato zařízení se také počítají do limitu registrace zařízení.
2. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **omezení registrace** > Ověřte limit registrace zařízení. Ve výchozím nastavení je limit nastavený na 15. 
3. Pokud počet zaregistrovaných zařízení dosáhl limitu, odeberte nepotřebná zařízení nebo zvyšte limit pro registraci zařízení. Vzhledem k tomu, že všechna zaregistrovaná zařízení využívají licenci Intune, doporučujeme, abyste nejdřív odebrali nepotřebná zařízení.
4. Zařízení znovu zaregistrujte.

### <a name="workplace-join-failed"></a>Workplace Join se nezdařilo

**Příčina:** Aplikace Portál společnosti není aktuální nebo je poškozená.  

#### <a name="resolution"></a>Rozlišení
1. Odeberte ze zařízení aplikaci Portál společnosti.
2. Stáhněte si a nainstalujte aplikaci **Microsoft Intune portál společnosti** z **App Storu**.
3. Zařízení znovu zaregistrujte.

### <a name="user-license-type-invalid"></a>Neplatný typ uživatelské licence

**Příčina:** Uživatel, který se pokouší zaregistrovat zařízení, nemá platnou licenci Intune.

#### <a name="resolution"></a>Rozlišení
1. Otevřete centrum pro [správu Microsoft 365](https://admin.microsoft.com)a pak zvolte **Uživatelé** > **aktivní uživatelé**.
2. Vyberte ovlivněný uživatelský účet > **licence k produktům** > **Upravit**.
3. Ověřte, jestli se tomuto uživateli přiřadí platná licence Intune.
4. Zařízení znovu zaregistrujte.

### <a name="user-name-not-recognized-this-user-account-is-not-authorized-to-use-microsoft-intune-contact-your-system-administrator-if-you-think-you-have-received-this-message-in-error"></a>Uživatelské jméno nebylo rozpoznáno. Tento uživatelský účet nemá autorizaci používat Microsoft Intune. Pokud si myslíte, že jste tuto zprávu dostali omylem, obraťte se na správce systému.

**Příčina:** Uživatel, který se pokouší zaregistrovat zařízení, nemá platnou licenci Intune.

1. Otevřete centrum pro [správu Microsoft 365](https://admin.microsoft.com)a pak zvolte **Uživatelé** > **aktivní uživatelé**.
2. Vyberte příslušný účet uživatele a pak zvolte licence na **produkty** > **Upravit**.
3. Ověřte, jestli se tomuto uživateli přiřadí platná licence Intune.
4. Zařízení znovu zaregistrujte.

### <a name="profile-installation-failed-the-new-mdm-payload-does-not-match-the-old-payload"></a>Instalace profilu se nezdařila. Nová datová část MDM se neshoduje se starou datovou částí.

**Příčina:** V zařízení je již nainstalován profil pro správu.

#### <a name="resolution"></a>Rozlišení

1. Otevřete **Nastavení** zařízení se systémem iOS/IPadOS > **Obecná** > **Správa zařízení**.
2. Klepněte na existující profil pro správu a klepněte na **Odebrat správu**.
3. Zařízení znovu zaregistrujte.

### <a name="noenrollmentpolicy"></a>NoEnrollmentPolicy

**Příčina:** Certifikát služby Apple Push Notification Service (APNs) chybí, je neplatný nebo vypršela jeho platnost.

#### <a name="resolution"></a>Rozlišení
Ověřte, že se do Intune přidal platný certifikát APNs. Další informace najdete v tématu [Nastavení registrace zařízení s iOS/iPadOS](ios-enroll.md).

### <a name="accountnotonboarded"></a>AccountNotOnboarded

**Příčina:** Došlo k potížím s certifikátem APNs (Apple Push Notification Service), který je nakonfigurovaný v Intune.

#### <a name="resolution"></a>Rozlišení
Obnovte certifikát APNs a pak zařízení znovu zaregistrujte.

> [!IMPORTANT]
> Ujistěte se, že jste obnovili certifikát APNs. Neměňte certifikát APNs. Pokud certifikát nahradíte, budete muset znovu zaregistrovat všechna zařízení s iOS/iPadOS v Intune. 

- Informace o obnovení certifikátu APNs v samostatné službě Intune najdete v tématu [obnovení certifikátu Apple MDM push Certificate](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).
- Informace o obnovení certifikátu APNs v Office 365 najdete v tématu [Vytvoření certifikátu APNS pro zařízení s iOS/iPadOS](https://support.office.com/article/Create-an-APNs-Certificate-for-iOS-devices-522b43f4-a2ff-46f6-962a-dd4f47e546a7).

### <a name="xpc_type_error-connection-invalid"></a>Neplatné připojení XPC_TYPE_ERROR

Když zapnete zařízení spravované přes ADE, které má přiřazený profil registrace, registrace se nepovede a zobrazí se tato chybová zpráva:

```
asciidoc
mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" } }
iPhone mobileassetd[83] <Notice>: Client connection invalid (Connection invalid); terminating connection
iPhone com.apple.accessibility.AccessibilityUIServer(MobileAsset)[288] <Notice>: [MobileAssetError:29] Unable to copy asset information from https://mesu.apple.com/assets/ for asset type com.apple.MobileAsset.VoiceServices.CombinedVocalizerVoices
iPhone mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" }
```

**Příčina:** Mezi zařízením a službou Apple ADE dojde k problému s připojením.

#### <a name="resolution"></a>Rozlišení
Opravte problém s připojením nebo použijte k registraci zařízení jiné síťové připojení. Pokud se problém opakuje, může se také stát, že budete muset kontaktovat společnost Apple.


## <a name="other-issues"></a>Další problémy

### <a name="ade-enrollment-doesnt-start"></a>Registrace ADE se nespustí.
Když zapnete zařízení spravované přes ADE, které má přiřazený profil registrace, proces registrace Intune se iniciuje.

**Příčina:** Profil registrace se vytvoří před nahráním tokenu ADE do Intune.

#### <a name="resolution"></a>Rozlišení

1. Upravte registrační profil. V profilu můžete provádět změny. Účelem je aktualizovat čas změny profilu.
2. Synchronizovat zařízení spravovaná přes ADE: v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **iOS** > **Registrace iOS** > **tokeny programu** > vyberte token, který se teď má > **synchronizovat**. Žádost o synchronizaci se pošle společnosti Apple.

### <a name="ade-enrollment-stuck-at-user-login"></a>Registrace ADE zablokovaná při přihlášení uživatele
Když zapnete zařízení spravované přes ADE, které má přiřazený profil registrace, počáteční nastavení po zadání přihlašovacích údajů se vytvoří.

**Příčina:** Multi-Factor Authentication (MFA) je povolené. V současné době MFA nefunguje během registrace na zařízeních ADE.

#### <a name="resolution"></a>Rozlišení
Zakažte MFA a pak zařízení znovu zaregistrujte.


## <a name="next-steps"></a>Další kroky

- [Řešení potíží s registrací zařízení v Intune](troubleshoot-device-enrollment-in-intune.md)
- [Zeptejte se fóra služby Intune](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Podívejte se na blog týmu podpory Microsoft Intune.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Podívejte se na blog Microsoft Enterprise mobility and Security.](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)
