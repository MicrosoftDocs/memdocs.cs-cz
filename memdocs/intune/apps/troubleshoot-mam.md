---
title: Řešení potíží se správou mobilních aplikací
titleSuffix: Microsoft Intune
description: Toto téma popisuje některé tipy k odstraňování potíží pro nasazení podmíněného přístupu.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: cd5a0a3b-0013-4be3-a233-ce6e9083149f
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b91751e9879d06b40bdd9518926759da2331115f
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758257"
---
# <a name="troubleshoot-mobile-application-management"></a>Řešení potíží se správou mobilních aplikací

Toto téma obsahuje řešení běžných problémů, ke kterým došlo při použití Intune App Protection (označované také jako MAM nebo Správa mobilních aplikací).

Pokud tyto informace váš problém nevyřeší, přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md), ve kterém najdete další způsoby, jak získat nápovědu.

## <a name="common-it-administrator-issues"></a>Běžné problémy správců IT

Jedná se o běžné problémy, ke kterým může při používání zásad ochrany aplikací Intune docházet správce IT.

| Problém | Popis | Řešení |
| -- | -- | -- |
| Zásady se neuplatňují na Skype pro firmy. | Zásady ochrany aplikací bez registrace zařízení, které jsou v Azure Portal, se nevztahují na aplikaci Skype pro firmy na zařízeních s iOS/iPadOS a Androidem. | Pro Skype pro firmy se musí nastavit moderní ověřování.  Pokud chcete pro Skype nastavit moderní ověřování, řiďte se pokyny v tématu [Povolení tenanta pro moderní ověřování](https://social.technet.microsoft.com/wiki/contents/articles/34339.skype-for-business-online-enable-your-tenant-for-modern-authentication.aspx). |
| Zásady pro aplikace Office se neuplatňují. | Zásady ochrany aplikací se neuplatňují na žádné [podporované aplikace Office](https://www.microsoft.com/cloud-platform/microsoft-intune-partners) u žádného uživatele. | Zkontrolujte, jestli má uživatel licenci pro Intune a jestli na aplikace Office cílí nasazené zásady ochrany aplikací. Než se nově nasazené zásady ochrany aplikací uplatní, může to trvat až 8 hodin. |
| Správce nemůže na portálu Azure Portal nakonfigurovat zásady ochrany aplikací. | Uživatel správce IT nemůže v Azure Portal nakonfigurovat zásady ochrany aplikací. | Následující role uživatelů mají přístup k Azure Portal: <ul><li>Globální správce, který můžete nastavit v [centru pro správu Microsoft 365](https://admin.microsoft.com/)</li><li>Vlastník, který můžete nastavit v [Azure Portal](https://portal.azure.com/).</li><li>Přispěvatel, který můžete nastavit v [Azure Portal](https://portal.azure.com/).</li></ul> Nápovědu k nastavení těchto rolí najdete [v tématu řízení správy na základě rolí (RBAC) pomocí Microsoft Intune](../fundamentals/role-based-access-control.md) .|
|V sestavách zásad ochrany aplikací chybí uživatelské účty. | Sestavy z konzoly správce nezobrazují uživatelské účty, na které se nedávno nasadily zásady ochrany aplikací. | Než se uživatelé nově zacílení pomocí zásad ochrany aplikací zobrazí v sestavách jako cíloví uživatelé, může uplynout až 24 hodin. |
| Změny zásad se neuplatňují. | Než se změny a aktualizace zásad ochrany aplikací uplatní, může uplynout až 8 hodin. | Koncový uživatel se může z aplikace odhlásit a znovu přihlásit, aby vynutil synchronizaci se službou. |
| Zásady ochrany aplikace se neuplatňují na program DEP. | Zásady ochrany aplikací se nevztahují na zařízení v programu Apple DEP. | Zkontrolujte, jestli v programu Apple DEP (Device Enrollment Program) používáte přidružení uživatele. Přidružení uživatele se vyžaduje pro všechny aplikace, které v rámci DEP vyžadují ověření uživatele. <br><br>Další informace o registraci DEP pro iOS/iPadOS najdete v tématu [Automatická registrace zařízení s iOS/iPadOS pomocí program registrace zařízení společnosti Apple](../enrollment/device-enrollment-program-enroll-ios.md) .|
| Zásady přenosu dat nefungují s iOS/iPadOS | Možnost **Povolit aplikaci přenášet data do jiných aplikací** a **Povolit aplikaci přijímat data z dalších zásad aplikací** nespravuje přenos dat v iOS/iPadOS úspěšně. | Další informace najdete [v tématu Správa přenosu dat mezi aplikacemi pro iOS/iPadOS v Microsoft Intune](data-transfer-between-apps-manage-ios.md). |

## <a name="common-end-user-issues"></a>Běžné problémy koncových uživatelů

Běžné problémy koncových uživatelů jsou rozdělené do následujících kategorií:

* **Scénáře normálního použití**: koncový uživatel se může setkat s těmito scénáři u aplikací, které mají zásady ochrany aplikací Intune. Nejedná se o skutečné problémy, můžou ale být vnímané jako chyby.

* **Dialogová okna pro normální využití**: Jedná se o dialogová okna použití, která se můžou zobrazovat koncovému uživateli v aplikacích, které mají zásady ochrany aplikací Intune. Tyto zprávy a dialogy **neindikují** chybu.

* **Chybové zprávy a dialogy**: Jedná se o chybové zprávy a dialogy, které se koncovému uživateli můžou zobrazovat v aplikacích, které mají zásady ochrany aplikací Intune. Často indikují, že správce IT udělal při ochraně aplikací pro Intune nějakou chybu.

### <a name="normal-usage-scenarios"></a>Scénáře při běžném používání

Platforma | Scénář | Vysvětlení |
---| --- | --- |
iOS | Koncový uživatel může pomocí rozšíření pro sdílení pro iOS/iPadOS otevírat pracovní nebo školní data v nespravovaných aplikacích, a to i v případě, že se zásady přenosu dat nastavily **jenom na spravované aplikace** nebo **žádné aplikace.** Nemůže při tom dojít k úniku dat? | Zásady ochrany aplikací Intune nemůžou řídit rozšíření sdílené složky iOS/iPadOS bez správy zařízení. Proto **Intune „podniková“ data před jejich sdílením mimo příslušnou aplikaci zašifruje**. Můžete si to ověřit pokusem o otevření „podnikového“ souboru mimo spravovanou aplikaci. Soubor by měl být zašifrovaný a mimo spravovanou aplikaci by ho nemělo být možné otevřít.
iOS | Proč se koncovým uživatelům **zobrazí výzva k instalaci aplikace Microsoft Authenticator** | To je potřeba v případě, že se používá podmíněný přístup na základě aplikace, přečtěte si téma [vyžadování schválené klientské aplikace](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).
Android | Proč je potřeba, aby si koncový uživatel **nainstaloval aplikaci Portál společnosti** i v případě, že používám ochranu aplikací MAM bez registrace zařízení?  | V Androidu je většina funkcí ochrany aplikací integrovaná do aplikace Portál společnosti. **Aplikace Portál společnosti se sice vyžaduje vždycky, ale registrace zařízení se nevyžaduje**. K ochraně aplikací bez registrace je jenom nutné, aby měl koncový uživatel aplikaci Portál společnosti na zařízení nainstalovanou.
iOS/Android | Zásady ochrany aplikací se nepoužívají při použití konceptu e-mailu v aplikaci Outlook. | Vzhledem k tomu, že Outlook podporuje podnikový i osobní kontext, nevynutilo MAM v konceptu e-mailu.
iOS/Android | Zásady ochrany aplikací se nepoužívají pro nové dokumenty v WXP (Word, Excel, PowerPoint) | Vzhledem k tomu, že WXP podporuje podnikový i osobní kontext, neuplatňuje MAM na nových dokumentech, dokud se neuloží do identifikovaného podnikového umístění, jako je OneDrive.
iOS/Android | Aplikace, které neumožňují možnost Uložit jako do místního úložiště, když je povolená zásada | Chování aplikace pro toto nastavení řídí vývojář aplikace.
Android | Android má víc omezení než iOS/iPadOS, na čem nativní aplikace můžou přistupovat k MAM chráněnému obsahu. | Android je otevřená platforma a "nativní" přidružení aplikace může změnit koncový uživatel na potenciálně nebezpečné aplikace. Použijte [výjimky zásad přenosu dat](app-protection-policies-exception.md) pro vyloučení konkrétních aplikací.
Android | Azure Information Protection (AIP) se může uložit jako PDF, pokud je zabráněno možnost Uložit jako. | AIP respektuje zásadu MAM pro možnost zakázat tisk při použití příkazu Uložit jako PDF.
iOS | Otevírání příloh PDF v aplikaci Outlook se nepovede a akce není povolená. | Tato situace může nastat, pokud se uživatel neověřil do aplikace Acrobat Reader pro Intune nebo použil k ověření v organizaci kryptografický otisk. Otevřete si aplikaci Acrobat Reader předem a proveďte ověření pomocí přihlašovacích údajů UPN.


### <a name="normal-usage-dialogs"></a>Dialogy při běžném používání

Platforma | Zpráva nebo dialog | Vysvětlení |
--- | --- | --- |
iOS, Android | **Přihlášení**: Aby mohla organizace chránit svoje data, musí tuto aplikaci spravovat. Pokud budete chtít správu nastavit, přihlaste se svým pracovním nebo školním účtem. | Aby bylo možné tuto aplikaci používat, musí se koncový uživatel přihlásit pomocí svého pracovního nebo školního účtu, který vyžaduje zásady ochrany aplikací. Aby se zásady daly použít, musí se uživatel ověřit proti Azure Active Directory.
iOS, Android |**Vyžadováno restartování**: Organizace teď chrání svoje data v této aplikaci. Abyste mohli pokračovat, musíte aplikaci restartovat. | Aplikace přijala zásady ochrany aplikací Intune a je nutné ji restartovat, aby bylo možné zásady použít.
iOS, Android |**Akce nepovolena**: Vaše organizace vám v této aplikaci umožňuje otevřít jenom pracovní nebo školní data. | Správce IT nastavil u zásady **Povolit aplikaci přijímat data z jiných aplikací** možnost **Pouze spravované aplikace**. Proto koncoví uživatelé můžou do této aplikace přenést data jenom z jiných aplikací, které mají zásady ochrany aplikací.
iOS, Android |**Akce nepovolena**: Vaše organizace povoluje přenést její data jenom do jiných spravovaných aplikací. | Správce IT nastavil u zásady **Povolit aplikaci posílat data do jiných aplikací** možnost **Pouze spravované aplikace**. Proto může koncový uživatel z této aplikace přenášet data jenom na jiné aplikace, které mají zásady ochrany aplikací.
iOS, Android |**Upozornění na vymazání**: Vaše organizace odebrala svoje data související s touto aplikací. Pokud chcete pokračovat, restartujte aplikaci. | Správce IT pomocí ochrany aplikací pro Intune inicioval vymazání aplikace.
Android | **Vyžaduje se aplikace Portál společnosti**: Pokud chcete s touto aplikací používat svůj pracovní nebo školní účet, musíte si nainstalovat aplikaci Portál společnosti Intune. Pokračujte kliknutím na tlačítko Přejít do obchodu. | V Androidu je většina funkcí ochrany aplikací integrovaná do aplikace Portál společnosti. **Aplikace Portál společnosti se sice vyžaduje vždycky, ale registrace zařízení se nevyžaduje**. K ochraně aplikací bez registrace je jenom nutné, aby měl koncový uživatel aplikaci Portál společnosti na zařízení nainstalovanou.

### <a name="error-messages-and-dialogs-on-ios"></a>Chybové zprávy a dialogy v iOS

Chybová zpráva nebo dialog | Příčina | Náprava |
-- | --- | --- |
**Aplikace není nastavená**: Tato aplikace není nastavená, abyste ji mohli používat. Požádejte o pomoc správce IT. | Nepovedlo se zjistit požadované zásady ochrany aplikací pro aplikaci. |Zkontrolujte, jestli jsou ve skupině zabezpečení uživatele nasazené zásady ochrany aplikací iOS a cílí na tuto aplikaci.
**Vítá vás Intune Managed Browser**: Tato aplikace funguje nejlépe, když je spravována službou Microsoft Intune. Aplikaci můžete kdykoli použít k procházení webu, a pokud k její správě použijete Microsoft Intune, získáte přístup k dalším funkcím ochrany dat. | Nepovedlo se zjistit požadované zásady ochrany aplikací pro Intune Managed Browser aplikaci. <br><br>Uživatel může aplikaci stále používat k procházení webu, ale aplikaci nespravuje Intune. | Zkontrolujte, jestli jsou ve skupině zabezpečení uživetele nasazené zásady ochrany aplikací pro iOS a cílí na aplikaci Intune Managed Browser.
**Přihlášení se nezdařilo**: Teď vás nemůžeme přihlásit. Zkuste to později. | Nepodařilo se zaregistrovat uživatele ke službě MAM po tom, co se uživatel pokusil přihlásit pomocí svého pracovního nebo školního účtu. | Zkontrolujte, jestli jsou ve skupině zabezpečení uživatele nasazené zásady ochrany aplikací iOS a cílí na tuto aplikaci.
**Nenastaven účet**: Vaše organizace nenastavila váš účet tak, aby měl přístup k pracovním nebo školním datům. Požádejte prosím o pomoc svého správce IT. | Uživatelský účet nemá licenci pro Intune A Direct. | Ujistěte se, že účet uživatele má přiřazenou licenci Intune v [centru pro správu Microsoft 365](https://admin.microsoft.com).
**Zařízení nesplňuje požadavky**: Tuto aplikaci nejde použít, protože používáte zařízení s jailbreakem. Požádejte o pomoc správce IT. | Intune zjistil, že uživatel je na zařízení s jailbreakem. | Resetujte zařízení na výchozí tovární nastavení. Postupujte podle [těchto pokynů](https://support.apple.com/HT201274) z webu podpory Apple.
**Vyžaduje se připojení k internetu **: Musíte být připojení k internetu, abychom mohli ověřit, že můžete používat tuto aplikaci. | Zařízení není připojené k internetu. | Připojte zařízení k síti Wi-Fi nebo mobilní síti.
**Neznámé selhání**: Zkuste aplikaci restartovat. Pokud s tím budou dál problémy, požádejte o pomoc správce IT. | Došlo k neznámému selhání. | Chvíli počkejte a zkuste to znovu. Pokud chyba přetrvává, vytvořte [lístek podpory](../fundamentals/get-support.md#create-an-online-support-ticket) s Intune.
**Přístup k datům vaší organizace**: Pracovní nebo školní účet, který jste zadali, nemá přístup k této aplikaci. Možná se budete muset přihlásit s jiným účtem. Požádejte o pomoc správce IT. | Intune zjistil, že se uživatel pokusil přihlásit pomocí druhého pracovního nebo školního účtu, který se liší od účtu pro zařízení zaregistrovaného do MAM. MAM může na jednom zařízení najednou spravovat jenom jeden pracovní nebo školní účet. | Ať se uživatel přihlásí pomocí účtu, jehož uživatelské jméno je na přihlašovací obrazovce předem vyplněné. Možná budete muset [nakonfigurovat nastavení hlavního názvu uživatele (UPN) pro Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm). <br> <br> Nebo nechte uživatele, ať se přihlásí pomocí nového pracovního nebo školního účtu, a odeberte stávající účet zaregistrovaný v MAM.
**Potíže s připojením**: Došlo k neočekávaným potížím s připojením. Zkontrolujte připojení a zkuste to znovu.  |  Došlo k neočekávanému selhání. | Chvíli počkejte a zkuste to znovu. Pokud chyba přetrvává, vytvořte [lístek podpory](../fundamentals/get-support.md#create-an-online-support-ticket) s Intune.
**Výstraha**: Tuto aplikaci už nejde používat. O další informace požádejte správce IT. | Nepodařilo se ověřit certifikát aplikace. | Zkontrolujte, jestli je verze aplikace aktuální. <br><br> Nainstalujte aplikaci znovu.
**Chyba**: V této aplikaci došlo k chybě a je potřeba ji zavřít. Pokud se bude tato chybová zpráva zobrazovat dál, obraťte se prosím na správce IT. | Nepodařilo se přečíst PIN kód aplikace MAM z řetězce klíčů Apple iOS. | Restartujte zařízení. Zkontrolujte, jestli je verze aplikace aktuální. <br><br> Nainstalujte aplikaci znovu.

### <a name="error-messages-and-dialogs-on-android"></a>Chybové zprávy a dialogy v Androidu

Dialog / chybová zpráva | Příčina | Náprava |
-- | --- | --- |
**Nenastavena aplikace**: Tato aplikace zatím není nastavená tak, abyste ji mohli používat. Požádejte o pomoc správce IT. | Nepovedlo se zjistit požadované zásady ochrany aplikací pro aplikaci. |Zkontrolujte, jestli jsou ve skupině zabezpečení uživatele nasazené zásady ochrany aplikací pro Android a jestli cílí na tuto aplikaci.
**Aplikaci se nepodařilo spustit**: Při spouštění vaší aplikace se objevil problém. Zkuste aplikaci (nebo aplikaci Portál společnosti Intune) aktualizovat. Pokud potřebujete pomoc, obraťte se na správce IT. | Intune zjistil platné zásady ochrany aplikací pro aplikaci, ale aplikace selhává během inicializace MAM. | Zkontrolujte, jestli je verze aplikace aktuální. <br><br> Zkontrolujte, jestli je na zařízení nainstalovaná aktuální aplikace Portál společnosti Intune a jestli je aktuální. <br><br> Pokud chyba přetrvává, použijte aplikaci Portál společnosti k odeslání protokolů do Intune nebo vytvoření [lístku podpory](../fundamentals/get-support.md#create-an-online-support-ticket).
**Nenašla se žádná aplikace**: Na tomto zařízení nejsou žádné aplikace, ve kterých by vaše organizace povolovala otevření tohoto obsahu. Požádejte o pomoc správce IT. | Uživatel se pokusil otevřít pracovní nebo školní data pomocí jiné aplikace, ale Intune nemůže najít žádné jiné spravované aplikace, které jsou k otevírání těchto dat povolené. | Ujistěte se, že jsou do skupiny zabezpečení uživatele nasazené zásady ochrany aplikací pro Android a že se cílí aspoň na jednu další aplikaci s podporou MAM, která může otevřít příslušné údaje.
**Přihlášení se nezdařilo**: Zkuste se znovu přihlásit. Pokud s tím budou dál problémy, požádejte o pomoc správce IT. | Nepodařilo se ověřit účet, pomocí kterého se uživatel pokusil přihlásit. | Zkontrolujte, jestli se uživatel přihlašuje pomocí pracovního nebo školního účtu, který je už zaregistrovaný službou Intune MAM (první pracovní nebo školní účet, který se do této aplikace úspěšně přihlásil). <br><br> Vymažte data aplikace. <br><br> Zkontrolujte, jestli je verze aplikace aktuální. <br><br> Zkontrolujte, jestli je verze Portálu společnosti aktuální.
**Vyžaduje se připojení k Internetu**: musíte být připojení k Internetu, abyste mohli ověřit, že můžete používat tuto aplikaci. | Zařízení není připojené k internetu. | Připojte zařízení k síti Wi-Fi nebo mobilní síti.
**Zařízení nesplňuje požadavky**: Tuto aplikaci nejde použít, protože používáte zařízení s rootem. Požádejte o pomoc správce IT. | Intune zjistil, že uživatel je na rootovaném zařízení. | Resetujte zařízení na výchozí tovární nastavení.
**Nenastaven účet**: Tato aplikace se musí spravovat přes Microsoft Intune, ale nemáte nastavený účet. Požádejte o pomoc správce IT. | Uživatelský účet nemá licenci pro Intune A Direct. | Ujistěte se, že účet uživatele má přiřazenou licenci Intune v [centru pro správu Microsoft 365](https://admin.microsoft.com).
**Aplikaci nejde zaregistrovat**: Tato aplikace se musí spravovat přes Microsoft Intune, ale momentálně jsme ji nemohli zaregistrovat. Požádejte o pomoc správce IT. Požádejte o pomoc správce IT. | Nepodařilo se aplikaci automaticky zaregistrovat ve službě MAM, když jsou požadovány zásady ochrany aplikací. | Vymažte data aplikace. <br><br> Odešlete protokoly do Intune prostřednictvím aplikace Portál společnosti nebo souboru lístkem podpory. Další informace najdete v tématu [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).

## <a name="next-steps"></a>Další kroky

- [Jak ověřit nastavení správy mobilních aplikací](app-protection-policies-validate.md)
- Naučte se používat soubory protokolu k odstraňování potíží se zásadami Intune App Protection najdete v tématu.[https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)
- Další informace o řešení potíží s Intune najdete v článku [Použití portálu pro řešení potíží k poskytování pomoci uživatelům ve vaší společnosti](../fundamentals/help-desk-operators.md). 
- Zjistěte další informace o známých problémech v Microsoft Intune. Ty najdete v článku [Známé problémy v Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Potřebujete další pomoc? Přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).
