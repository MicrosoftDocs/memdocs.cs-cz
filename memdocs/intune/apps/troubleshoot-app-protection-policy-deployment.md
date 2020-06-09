---
title: Řešení potíží s nasazením zásad ochrany aplikací Intune
description: Popisuje, jak řešit problémy, které se mohou vyskytnout při nasazení zásad ochrany aplikací Intune.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.subservice: apps
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 7f4d3f8193eeaf9597d56c8cf1cd999147915e61
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531566"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Řešení potíží s nasazením zásad ochrany aplikací v Intune

## <a name="introduction"></a>Úvod

Tento článek vám pomůže pochopit a řešit problémy při použití zásad ochrany aplikací v Microsoft Intune. Postupujte podle částí, které se vztahují k vaší situaci.

## <a name="basic-steps"></a>Základní kroky

### <a name="collect-initial-data"></a>Shromažďování počátečních dat

Než začnete s odstraňováním potíží, měli byste shromáždit některé základní informace, které vám pomůžou lépe pochopit problém a zkrátit dobu, po kterou se má řešení najít.

Shromážděte následující údaje:

- Jaké nastavení zásad se nepoužívá? Používá se nějaká zásada?
- K čemu slouží uživatelské prostředí? Mají uživatelé nainstalovanou a spuštěnou cílovou aplikaci?
- Kdy tento problém začal? Byla ochrana aplikací někdy zpracovaná?
- Kterou platformu (Android nebo iOS) má problém?
- Kolik uživatelů je ovlivněno? Jsou všechna zařízení nebo jenom některá zařízení ovlivněná?
- Kolik zařízení je ovlivněno? Jsou všechna zařízení nebo jenom některá zařízení ovlivněná?
- I když zásady ochrany aplikací Intune nevyžadují službu správy mobilních zařízení (MDM), mají vliv na uživatele, kteří používají Intune nebo modul EMM třetích stran?
- Ovlivnily se všechny spravované aplikace nebo jenom konkrétní aplikace? Například jsou obchodní aplikace, které mají vliv na [Intune App SDK](../developer/app-sdk-get-started.md) , ale aplikace pro Store nejsou?

Teď můžete začít řešit potíže na základě odpovědí na tyto otázky.

### <a name="verify-prerequisites"></a>Ověření požadavků

Dalším krokem při řešení potíží je ověření, jestli jsou splněné všechny požadavky.

I když můžete používat zásady ochrany aplikací Intune nezávisle na řešení MDM, musí být splněné následující předpoklady:

- Uživatel musí mít přiřazenou licenci Intune.
- Uživatel musí patřit do skupiny zabezpečení, která je cílem zásady ochrany aplikací. Stejné zásady ochrany aplikací musí cílit na konkrétní aplikaci, která se používá.
- Pro zařízení s Androidem je Portál společnosti aplikace nutná pro příjem zásad ochrany aplikací.
- Pokud používáte aplikace [Word, Excel nebo PowerPoint](https://products.office.com/business/office) , musí být splněny následující další požadavky:
    - Uživatel musí mít licenci pro [aplikace Microsoft 365 pro firmy nebo podnik](https://products.office.com/business/compare-more-office-365-for-business-plans) propojený s účtem uživatele Azure Active Directory (Azure AD). Předplatné musí obsahovat aplikace Office na mobilních zařízeních a může obsahovat účet pro ukládání do cloudu přes [OneDrive pro firmy](https://onedrive.live.com/about/business/). Licence na Office 365 se dají přiřadit v [centru pro správu Microsoft 365](https://admin.microsoft.com) pomocí následujících [pokynů](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - Uživatel musí mít spravované umístění, které je nakonfigurováno pomocí podrobné funkce **Uložit jako** . Tento příkaz je umístěný v nastavení zásady ochrany aplikací pro **ukládání kopií dat organizace** . Pokud je spravovaným umístěním například [OneDrive](https://onedrive.live.com/about/), měla by být aplikace OneDrive nakonfigurovaná v aplikaci Word, Excel nebo PowerPointu daného uživatele.
    - Pokud je spravovaným umístěním OneDrive, musí být aplikace cílem zásady ochrany aplikací, které jsou pro uživatele nasazené.

  > [!NOTE]
  > Mobilní aplikace Office v současné době podporují jenom SharePoint Online a ne místní SharePoint.

- Pokud používáte zásady ochrany aplikací Intune spolu s místními prostředky (Microsoft Skype pro firmy a Microsoft Exchange Server), musíte povolit [hybridní moderní ověřování (HMA) pro Skype pro firmy a Exchange](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Zásady ochrany aplikací Intune vyžadují, aby byla identita uživatele konzistentní mezi aplikací a [sadou Intune App SDK](../developer/app-sdk-get-started.md). Jediným způsobem, jak zaručit tuto konzistenci, je prostřednictvím moderního ověřování. Existují scénáře, ve kterých aplikace mohou fungovat v místní konfiguraci bez moderního ověřování. Výsledky se ale neshodují ani nezaručují.

Další informace o tom, jak povolit HMA pro hybridní a místní konfiguraci Skypu pro firmy, najdete v následujících článcích:

- **Hybridní**<br>
[Hybridní moderní ověřování pro SfB a Exchange dosáhne GA](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **Místní**<br>
[Moderní ověřování pro SfB OnPrem s AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Zkontroluje stav zásad ochrany aplikací.

Chcete-li zjistit stav ochrany aplikace, postupujte podle následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **monitor**  >  **stav ochrany aplikace**a pak vyberte dlaždici **přiřazení uživatelé** .
3. Na stránce **vytváření sestav aplikací** vyberte **Vybrat uživatele** a zobrazte seznam uživatelů a skupin.
4. Vyhledejte a vyberte ze seznamu jednoho ze všech ovlivněných uživatelů a pak vyberte **Vybrat uživatele**. V horní části podokna vytváření sestav aplikace uvidíte, jestli má uživatel licenci pro ochranu aplikací a má licenci pro O365. Můžete také zobrazit stav aplikace pro všechna zařízení uživatele.
5. Tyto důležité informace si poznamenejte jako cílené aplikace, typy zařízení, zásady, stav vrácení se změnami zařízení a čas poslední synchronizace.

> [!NOTE]
> Zásady ochrany aplikací se použijí jenom v případě, že se aplikace používají v pracovním kontextu. Například když uživatel přistupuje k aplikacím pomocí pracovního účtu.

Další informace najdete v tématu [ověření nastavení zásad ochrany aplikací v Microsoft Intune](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Ověření konzistence identity uživatele mezi aplikací a sadou Intune App SDK

Ve většině scénářů se uživatelé přihlašují ke svým účtům pomocí hlavního názvu uživatele (UPN). V některých prostředích (například v místních scénářích) ale uživatelé můžou použít jinou formu přihlašovacích údajů pro přihlášení. V těchto případech se může stát, že hlavní název uživatele (UPN), který se používá v aplikaci, se neshoduje s objektem UPN ve službě Azure AD. Pokud k tomuto problému dojde, zásady ochrany aplikací se nepoužijí podle očekávání.

Doporučené osvědčené postupy od Microsoftu odpovídají hlavnímu názvu uživatele (UPN) k primární adrese SMTP. Tento postup umožňuje uživatelům přihlašovat se ke spravovaným aplikacím, ochraně aplikací Intune a dalším prostředkům služby Azure AD pomocí konzistentní identity. Další informace najdete v tématu [populace Azure AD userPrincipalName](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Pokud vaše prostředí vyžaduje alternativní metody přihlašování, přečtěte si téma [Konfigurace alternativního přihlašovacího ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), konkrétně [hybridní moderní ověřování s alternativním identifikátorem](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Ověření cílení na uživatele

Zásady ochrany aplikací Intune musí být cílené na uživatele. Pokud nepřiřazujete zásady ochrany aplikací uživateli nebo skupině uživatelů, zásada se nepoužije.

Pokud chcete ověřit, jestli se zásada aplikuje na cílového uživatele, postupujte takto:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **monitor**  >  **stav ochrany aplikace**a pak vyberte dlaždici **stav uživatele** (na základě platformy operačního systému zařízení).
V podokně **vytváření sestav aplikací** vyberte **Vybrat uživatele** a vyhledejte uživatele.
3. Vyberte uživatele ze seznamu. Můžete zobrazit podrobnosti o tomto uživateli.

Když přiřadíte zásadu do skupiny uživatelů, ujistěte se, že je uživatel ve skupině uživatelů. Postupujte přitom takto:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **skupiny > všechny skupiny**a pak vyhledejte a vyberte skupinu, která se používá pro přiřazení zásad ochrany aplikací.
3. V části **Spravovat** vyberte **členy**.
4. Pokud tento ovlivněný uživatel není uvedený, přečtěte si téma [Správa přístupu k aplikacím a prostředkům pomocí skupin Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) a pravidel členství ve skupinách. Ujistěte se, že je příslušný uživatel součástí skupiny.
5. Ujistěte se, že ovlivněný uživatel není v žádné z vyloučených skupin pro danou zásadu.

> [!IMPORTANT]
> - Zásady ochrany aplikací Intune je potřeba přiřadit ke skupinám uživatelů, nikoli ke skupinám zařízení.
> - Pokud ovlivněné zařízení používá Apple Program registrace zařízení (DEP), ujistěte se, že je povolené **přidružení uživatele** . Přidružení uživatele se vyžaduje pro všechny aplikace, které v rámci DEP vyžadují ověření uživatele.
> - Pokud příslušné zařízení používá Android Enterprise, budou zásady ochrany aplikací podporovat jenom pracovní profily.


### <a name="verify-that-the-managed-app-is-targeted"></a>Ověření cílení spravované aplikace

Když konfigurujete zásady ochrany aplikací Intune, cílové aplikace musí používat [sadu Intune App SDK](../developer/app-sdk-get-started.md). V opačném případě zásady ochrany aplikací nemusí správně fungovat.

Ujistěte se, že je cílová aplikace uvedená v [Microsoft Intune chráněných aplikacích](../apps/apps-supported-intune-apps.md). V případě LOB nebo vlastních aplikací ověřte, že aplikace používají nejnovější verzi sady [Intune App SDK](../developer/app-sdk-get-started.md). Je třeba počítat s následujícím:

Pro iOS je tento postup důležitý, protože každá verze obsahuje opravy, které mají vliv na to, jak se tyto zásady používají a jak fungují. Další informace najdete v tématu [verze iOS sady Intune App SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
V případě Androidu není tento postup důležitý. Uživatelé ale musí mít nainstalovanou nejnovější verzi aplikace Portál společnosti, protože Portál společnosti aplikace funguje jako agent zprostředkovatele zásad.

> [!NOTE]
> Od září 2019 se Intune přesune na podporu aplikací pro iOS, které mají Intune App SDK 8.1.1 a novější verze. Aplikace vytvořené pomocí verzí sady SDK starších než 8.1.1 již nebudou podporovány. 

## <a name="more-information"></a>Další informace

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Speciální požadavky na zařízení spravovaná přes MDM Intune

Když vytvoříte zásady ochrany aplikací, můžete je cílit na všechny typy aplikací nebo na následující typy aplikací:

- Aplikace na nespravovaných zařízeních
- Aplikace na zařízeních spravovaných přes Intune
- Aplikace v pracovním profilu Android

> [!NOTE] 
> Chcete-li určit typy aplikací, nastavte možnost **cíl na možnost Ne pro všechny typy aplikací** na hodnotu **ne**a pak vyberte ze seznamu **typy aplikací** .

Pro iOS se pro nastavení zásad ochrany aplikací (aplikace) do aplikací na zařízeních zaregistrovaných v Intune musí zadat následující další [nastavení konfigurace aplikace](../apps/app-configuration-policies-use-ios.md) :

- **IntuneMAMUPN** musí být nakonfigurovaná pro všechny aplikace spravované pro MDM (Intune nebo modul EMM jiného výrobce). Další informace najdete v tématu Konfigurace nastavení hlavního názvu uživatele (UPN) pro Microsoft Intune nebo modul EMM třetích stran.
- **IntuneMAMDeviceID** musí být nakonfigurovaná pro všechny aplikace spravované MDM pro ostatní výrobce.
- **IntuneMAMDeviceID** musí být nakonfigurovaný jako token ID zařízení. Například Key = IntuneMAMDeviceID, Value = {{deviceID}}. Další informace najdete v tématu [Přidání zásad konfigurace aplikací pro spravovaná zařízení s iOSem](../apps/app-configuration-policies-use-ios.md).
- Pokud je nakonfigurovaná jenom hodnota **IntuneMAMDeviceID** , aplikace Intune bude zařízení považovat za nespravované.

### <a name="scenario-policy-changes-are-not-working"></a>Scénář: změny zásad nefungují.
[Sada Intune App SDK](../developer/app-sdk-get-started.md) pravidelně kontroluje změny zásad. Tento proces se však může zpozdit z některého z následujících důvodů:

- Aplikace se ve službě nevrátila.
- Aplikace Portál společnosti byla ze zařízení odebrána.

Zásady ochrany aplikací Intune závisí na identitě uživatele. Proto se vyžaduje platné přihlášení, které používá pracovní nebo školní účet pro aplikaci a konzistentní připojení ke službě. Pokud uživatel není přihlášený k aplikaci nebo když byla aplikace Portál společnosti ze zařízení odebrána, aktualizace zásad se nepoužijí.

Kromě toho může trvat až 8 hodin změny a aktualizace zásad ochrany aplikací. Pokud je to možné, zavřete všechny aplikace a restartování zařízení obvykle vynutí, aby se aktualizace zásad platila dřív.

Chcete-li zjistit stav ochrany aplikace, postupujte podle následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **monitor**  >  **stav ochrany aplikace**a pak vyberte dlaždici **přiřazení uživatelé** .
3. Na stránce vytváření sestav aplikací vyberte **Vybrat uživatele** a otevřete seznam uživatelů a skupin.
4. Vyhledejte a vyberte ze seznamu jednoho ze všech ovlivněných uživatelů a pak vyberte **Vybrat uživatele**.
5. Zkontrolujte aktuálně použité zásady, včetně stavu a času poslední synchronizace.
6. Pokud stav není **vrácen se změnami**nebo pokud se zobrazí zpráva, že nedošlo k nedávné synchronizaci, ověřte, zda má uživatel konzistentní síťové připojení. Pro uživatele Androidu se ujistěte, že mají nainstalovanou nejnovější verzi aplikace Portál společnosti.

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) kontroluje selektivní vymazání každých 30 minut. Změny stávajících zásad pro uživatele, kteří už jsou přihlášení, se ale nemusí zobrazovat po dobu až 8 hodin. Pokud chcete tento proces urychlit, přihlaste se uživateli z aplikace a pak se znovu přihlaste nebo restartujte své zařízení.

Zásady ochrany aplikací Intune zahrnují podporu více identit. Intune může zásady ochrany aplikací použít jenom na pracovní nebo školní účet, který se přihlásil k aplikaci. Podporuje se ale jenom jeden pracovní nebo školní účet na zařízení.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Scénář: zásady se aplikují, ale uživatelé iOS můžou dál přenášet pracovní soubory do nespravovaných aplikací.
Funkce **Správa Open-in** ( ![ tlačítko otevřít v ](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg) ) pro zařízení s iOS může omezit přenosy souborů mezi aplikacemi, které jsou nasazené prostřednictvím kanálu MDM. Uživatel může být schopný přenést pracovní soubory ze spravovaných umístění, jako je OneDrive a Exchange, do nespravovaných aplikací nebo umístění v závislosti na konfiguraci. Funkce **správy otevřené v** iOS funguje mimo jiné metody přenosu dat. Proto to není ovlivněno nastaveními **Uložit jako** a **Kopírovat/vložit** .

Zásady ochrany aplikací Intune můžete použít společně s funkcí **Správa Open in** pro iOS k ochraně firemních dat následujícím způsobem:

- **Zařízení vlastněná zaměstnanci, která nejsou spravovaná řešením MDM**: nastavení zásad ochrany aplikací můžete nastavit tak, aby aplikace mohla **přenášet data jenom na aplikace spravované zásadou**. V takovém případě chování při **otevření** v aplikaci spravované zásadou poskytuje jenom další aplikace spravované zásadami jako možnosti pro sdílení. Pokud se například uživatel pokusí odeslat chráněný soubor jako přílohu z OneDrivu v nativní e-mailové aplikaci, tento soubor je nečitelný.

- **Zařízení spravovaná řešením MDM**: pro zařízení, která jsou zaregistrovaná v Intune nebo v řešení MDM třetí strany, se sdílení dat mezi aplikacemi pomocí zásad ochrany aplikací a dalších spravovaných aplikací pro iOS, které jsou nasazené přes MDM, řídí pomocí aplikace Intune a funkce **pro správu otevřené v** systému iOS.<br/><br/>
Aby se zajistilo, že aplikace, které nasazujete pomocí řešení MDM, jsou přidružené taky k zásadám ochrany aplikací Intune, nakonfigurujte nastavení hlavního názvu uživatele (UPN) podle postupu popsaného v části [Konfigurace nastavení hlavního názvu](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm)uživatele<br/><br/>Pokud chcete určit, jak chcete povolit přenos dat do jiných aplikací, povolte možnost **Odeslat org data do jiných aplikací**a potom vyberte upřednostňovanou úroveň sdílení.<br/><br/>Pokud chcete určit, jak chcete aplikaci povolit, aby přijímala data z jiných aplikací, povolte **příjem dat z jiných aplikací**a potom vyberte upřednostňovanou úroveň přijímání dat.

Další informace o tom, jak přijímat a sdílet data aplikací, najdete v tématu [Nastavení přemístění dat](../apps/app-protection-policy-settings-ios.md#data-protection).

Další informaci získáte v článku o [správě přenosu dat mezi aplikacemi pro iOS pomocí Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Odkazy

Pokud pořád hledáte řešení souvisejícího s nějakým problémem nebo pokud chcete získat další informace o Intune, vystavte si na našem [Microsoft Intune fóru](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)dotaz. Řada techniků podpory, MVP a členů našeho vývojového týmu navštíví fóra. Proto je velmi pravděpodobné, že můžete najít někoho, kdo má informace, které potřebujete.

Chcete-li otevřít žádost o podporu pro tým podpory Microsoft Intune produktů, přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).

Další informace o zásadách ochrany aplikací Intune najdete v těchto článcích:

- [Řešení potíží se správou mobilních aplikací](../apps/troubleshoot-mam.md)
- [Časté otázky ke správě mobilních aplikací (MAM) a ochraně aplikací](../apps/mam-faq.md)
- [Tip podpory: řešení potíží s zásadami ochrany aplikací Intune pomocí souborů protokolu na místních zařízeních](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Všechny nejnovější novinky, informace a technické tipy najdete v našich oficiálních blogůch:

- [Blog týmu podpory Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Blog Microsoftu Enterprise mobility and Security](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Další kroky

- Další informace o řešení potíží s Intune najdete v článku [Použití portálu pro řešení potíží k poskytování pomoci uživatelům ve vaší společnosti](../fundamentals/help-desk-operators.md). 
- Zjistěte další informace o známých problémech v Microsoft Intune. Další informace najdete v tématu [úspěšnost zákazníka v Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Potřebujete další pomoc? Přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).
