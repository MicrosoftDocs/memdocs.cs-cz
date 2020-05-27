---
title: Správa přenosu dat mezi aplikacemi pro iOS
titleSuffix: Microsoft Intune
description: Přečtěte si, jak používat zásady správy mobilních aplikací v Microsoft Intune ke správě přenosů dat mezi aplikacemi.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d10b2d64-8c72-4e9b-bd06-ab9d9486ba5e
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41be99c94b31c166622ee497d08de438ee59cf23
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985708"
---
# <a name="how-to-manage-data-transfer-between-ios-apps-in-microsoft-intune"></a>Správa přenosu dat mezi aplikacemi pro iOS pomocí Microsoft Intune

Aby bylo možné chránit podniková data, omezte přenos souborů jenom na aplikace, které spravujete. Aplikace pro iOS můžete spravovat těmito způsoby:

- Chraňte data organizace pro pracovní nebo školní účty tak, že nakonfigurujete zásady ochrany aplikací pro aplikace. které říkáme *aplikacím spravovaným zásadou*.  Přečtěte si téma s informacemi o [všech aplikacích spravovaných přes Intune, které je možné spravovat pomocí zásad ochrany aplikací](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

- Nasaďte a spravujte aplikace přes správu zařízení s iOS, která vyžaduje, aby se zařízení zaregistrovala v řešení správy mobilních zařízení (MDM). Aplikace, které nasazujete, můžou být *aplikace spravované zásadou* nebo jinými aplikacemi spravovanými v iOS.

Funkce **správy otevřených v** zaregistrovaných zařízeních s iOS může omezit přenosy souborů mezi aplikacemi spravovanými v iOS. V nastavení konfigurace Nastavte omezení *správy Open in* a pak je nasaďte pomocí řešení MDM.  Když uživatel nainstaluje nasazenou aplikaci, uplatní se vámi nastavená omezení.

## <a name="use-app-protection-with-ios-apps"></a>Použití ochrany aplikací s aplikacemi pro iOS
Pomocí zásad ochrany aplikací se službou pro **správu** systému iOS můžete chránit data společnosti následujícími způsoby:

- **Zařízení nespravovaná žádným řešením MDM:** Nastavení zásad ochrany aplikací můžete nastavit tak, abyste mohli řídit sdílení dat s jinými aplikacemi prostřednictvím rozšíření *otevřít* nebo *sdílet*.  Uděláte to tak, že nakonfigurujete nastavení **Odeslat organizační data na jiné aplikace** do **aplikací spravovaných podle zásad s hodnotou filtrování otevřít v/sdílet** .  Chování funkce *otevřít v/sdílet* v *aplikaci spravované zásadou* prezentuje jenom jiné *aplikace spravované zásadou* jako možnosti pro sdílení. 

- **Zařízení spravovaná řešeními MDM**: u zařízení zaregistrovaných v rámci služby Intune nebo řešení MDM jiných výrobců se sdílení dat mezi aplikacemi se zásadami ochrany aplikací a dalšími spravovanými aplikacemi pro iOS nasazenými prostřednictvím MDM řídí zásadami aplikací Intune a funkcí **pro iOS Open in** . Aby se zajistilo, že aplikace nasazené pomocí řešení MDM jsou taky přidružené k zásadám ochrany aplikací Intune, nakonfigurujte nastavení hlavního názvu uživatele (UPN), jak je popsáno v následující části [Konfigurace nastavení hlavního názvu uživatele (UPN)](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm). Chcete-li určit, jak chcete povolit přenos dat do jiných aplikací, povolte možnost **Odeslat organizační data do jiných aplikací** a pak zvolte upřednostňovanou úroveň sdílení. Pokud chcete určit, jak chcete aplikaci povolit, aby přijímala data z jiných aplikací, povolte **příjem dat z jiných aplikací** a pak zvolte upřednostňovanou úroveň přijímání dat. Další informace o přijímání a sdílení dat aplikací najdete v tématu [Nastavení přemístění dat](app-protection-policy-settings-ios.md#data-protection).

## <a name="configure-user-upn-setting-for-microsoft-intune-or-third-party-emm"></a>Konfigurace nastavení hlavního názvu uživatele (UPN) pro Microsoft Intune nebo řešení EMM (Enterprise Mobility Management) jiného výrobce
Konfigurace nastavení hlavního názvu uživatele (UPN) se **vyžaduje** pro zařízení spravovaná pomocí Intune nebo řešení EMM jiného výrobce k identifikaci zaregistrovaného uživatelského účtu. Konfigurace hlavního názvu uživatele (UPN) spolupracuje se zásadami ochrany aplikací, které nasazujete z Intune. Následující postup představuje obecné informace o tom, jak nakonfigurovat nastavení hlavního názvu uživatele (UPN) a výsledné prostředí uživatele:

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) [vytvořte a přiřaďte zásady ochrany aplikací](app-protection-policies.md) pro iOS/iPadOS. Nakonfigurujte nastavení zásad podle požadavků vaší společnosti a vyberte aplikace iOS, které by tyto zásady měly používat.

2. Nasaďte aplikace a e-mailový profil, který chcete spravovat prostřednictvím Intune nebo řešení MDM jiného výrobce, pomocí následujících obecných kroků. Na toto prostředí se vztahuje také *Příklad 1*.

3. Nasaďte aplikaci s následujícím nastavením konfigurace aplikace na spravované zařízení:

      **Key** = IntuneMAMUPN; **hodnota** = <username@company.com>

      Příklad: [' IntuneMAMUPN ', ' janellecraig@contoso.com ']
      
     > [!NOTE]
     > V Intune musí být typ registrace zásady konfigurace aplikace nastavený na **spravovaná zařízení**.
     > Kromě toho musí být aplikace nainstalovaná z Portál společnosti Intune (Pokud je nastavená jako dostupná) nebo vložená jako požadovaná pro zařízení. 

4. Nasaďte **zásadu správy Open in** prostřednictvím Intune nebo jiného poskytovatele řešení MDM do zaregistrovaných zařízení.


### <a name="example-1-admin-experience-in-intune-or-third-party-mdm-console"></a>Příklad 1: Činnost správce v Intune nebo konzole řešení MDM jiného výrobce

1. Přejděte do konzoly pro správu Intune nebo poskytovatele řešení MDM jiného výrobce. Přejděte do části konzoly, ve které nasadíte nastavení konfigurace aplikace do zaregistrovaných zařízení s iOSem.

2. V části Konfigurace aplikace zadejte tato nastavení:

   **Key** = IntuneMAMUPN; **hodnota** = <username@company.com>

   Skutečná syntaxe dvojice klíč/hodnota se může lišit podle toho, jakého máte jiného poskytovatele řešení MDM. V následující tabulce jsou uvedeny příklady poskytovatelů MDM třetích stran a přesné hodnoty, které byste měli zadat pro dvojici klíč/hodnota.

   |Jiný poskytovatel řešení MDM| Konfigurační klíč | Typ hodnoty | Konfigurační hodnota|
   | ------- | ---- | ---- | ---- |
   |Microsoft Intune| IntuneMAMUPN | Řetězec | {{UserPrincipalName}}|
   |VMware AirWatch| IntuneMAMUPN | Řetězec | {UserPrincipalName}|
   |MobileIron | IntuneMAMUPN | Řetězec | ${userUPN} **nebo** ${userEmailAddress} |
   |Správa koncových bodů Citrix | IntuneMAMUPN | Řetězec | $ {User. userPrincipalName} |
   |Správce mobilních zařízení ManageEngine | IntuneMAMUPN | Řetězec | %upn% |

> [!NOTE]  
> Pokud pro Outlook pro iOS nebo iPadOS nasadíte zásadu konfigurace aplikace spravovaná zařízení s možností "použití návrháře konfigurace" a povolíte možnost **Povolit pouze pracovní nebo školní účty**, konfigurační klíč IntuneMAMUPN se konfiguruje automaticky na pozadí této zásady. Další podrobnosti najdete v části Nejčastější dotazy v [nové aplikaci Outlook pro zásady konfigurace aplikací pro iOS a Android – konfigurace obecné aplikace](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Outlook-for-iOS-and-Android-App-Configuration-Policy/ba-p/370481). 


### <a name="example-2-end-user-experience"></a>Příklad 2: Činnost koncového uživatele

*Sdílení z* aplikace spravované zásadou *do jiných aplikací se sdílením operačního systému*

1. Uživatel otevře aplikaci Microsoft OneDrive na zaregistrovaném zařízení s iOS a přihlásí se ke svému pracovnímu účtu.  Účet, který uživatel zadá, musí odpovídat hlavnímu názvu uživatele (UPN) účtu, který jste zadali v nastavení konfigurace aplikace pro aplikaci Microsoft OneDrive.

2. Po přihlášení správce nakonfiguroval nastavení aplikace na uživatelský účet na Microsoft OneDrive.  To zahrnuje konfiguraci nastavení **Odeslat organizační data ostatním aplikacím** do **aplikací spravovaných zásadou s hodnotou sdílení operačního systému** .

3. Uživatel zobrazí pracovní soubor a pokusí se o sdílení prostřednictvím aplikace Open-in se spravovaným systémem iOS.  

4. Přenos dat je úspěšný a data jsou teď chráněná **správou Open in** v aplikaci spravované v iOS.  APLIKACE Intune se nevztahuje na aplikace, které nejsou *aplikacemi spravovanými podle zásad*.

*Sdílení z* aplikace spravované v iOS *do* aplikace spravované zásadou *s příchozími daty organizace*

1. Uživatel otevře nativní E-mail na zaregistrovaném zařízení s iOS pomocí spravovaného e-mailového profilu.  

1. Uživatel otevře přílohu pracovního dokumentu z nativního e-mailu do aplikace Microsoft Word.

1. Při spuštění aplikace Word se objeví jedna ze dvou situací:
   1. Data jsou chráněná aplikací Intune, když:
      - Uživatel je přihlášený ke svému pracovnímu účtu, který odpovídá hlavnímu názvu uživatele (UPN) účtu, který jste zadali v nastavení konfigurace aplikace pro aplikaci Microsoft Word. 
      - Nastavení aplikace nakonfigurované správcem se vztahuje na uživatelský účet v aplikaci Microsoft Word.  To zahrnuje konfiguraci nastavení **přijímat data z jiných aplikací** na **všechny aplikace s hodnotou příchozích dat organizace** .
      - Přenos dat je úspěšný a dokument je označený pracovní identitou v aplikaci.  APLIKACE Intune chrání akce uživatelů pro dokument.
   1. Tato data **nejsou** CHRÁNĚNá aplikací Intune, když:
      - Uživatel **není přihlášený** ke svému pracovnímu účtu.
      - Nastavení nakonfigurovaná správcem se v aplikaci Microsoft Word **nepoužívají,** protože uživatel není přihlášený.
      - Přenos dat je úspěšný a dokument **není označený pracovní** identitou v aplikaci.  APLIKACE Intune **nechrání akce** uživatelů pro dokument, protože není aktivní.

    > [!NOTE]
    > Uživatel může pomocí aplikace Word přidat a používat své osobní účty. Zásady ochrany aplikací se nepoužijí, pokud uživatel používá slovo mimo pracovní kontext. 

### <a name="validate-user-upn-setting-for-third-party-emm"></a>Ověření nastavení hlavního názvu uživatele (UPN) pro řešení MDM jiného výrobce

Po nakonfigurování nastavení hlavního názvu uživatele (UPN) ověřte schopnost aplikace pro iOS přijímat a dodržovat zásady ochrany aplikací Intune.

Například nastavení zásad **vyžadovat kód PIN aplikace** se snadno otestuje. Pokud se nastavení zásad rovná **požadavku**, uživateli by se měla zobrazit výzva k nastavení nebo zadání kódu PIN, než bude moci získat přístup k firemním datům.

Nejdřív pro aplikaci pro iOS [vytvořte a přiřaďte zásady ochrany aplikací](app-protection-policies.md). Další informace o tom, jak testovat zásady ochrany aplikací, najdete v tématu [ověření zásad ochrany aplikací](app-protection-policies-validate.md).


## <a name="see-also"></a>Viz také
[Co jsou zásady ochrany aplikací Intune](app-protection-policy.md)
