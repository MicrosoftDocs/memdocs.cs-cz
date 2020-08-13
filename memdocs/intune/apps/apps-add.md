---
title: Přidání aplikací do Microsoft Intune
titleSuffix: ''
description: Zjistěte, jak přidat aplikace do Microsoft Intune, aby je bylo možné přiřadit uživatelům a zařízením. Intune podporuje širokou škálu typů aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1ded457-0ecf-4f9c-a2d2-857d57f8d30a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed6923a53560f1dafc29079fd9a119f72cd75359
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179447"
---
# <a name="add-apps-to-microsoft-intune"></a>Přidání aplikací do Microsoft Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Než budete moct konfigurovat, přiřazovat, chránit nebo monitorovat aplikace, musíte je přidat do Microsoft Intune.

Uživatelé aplikací a zařízení ve vaší společnosti (pracovníci vaší společnosti) můžou mít na aplikace několik požadavků. Než do Intune přidáte aplikace a zpřístupníte je pracovníkům, může vám pomoct vyhodnotit a pochopit základy aplikací. Existují různé typy aplikací, které jsou k dispozici pro Intune. Musíte určit požadavky aplikace, které uživatelé potřebují ve vaší společnosti, například platformy a možnosti, které vaše pracovní síly potřebují. Musíte určit, jestli se Intune bude používat ke správě zařízení (včetně aplikací), nebo jestli má Intune spravovat aplikace bez správy zařízení. Také je nutné určit aplikace a možnosti, které vaše pracovní síly potřebují a kteří je potřebují. Informace v tomto článku vám pomůžou s prvními kroky.

## <a name="app-types-in-microsoft-intune"></a>Typy aplikací v Microsoft Intune

Intune podporuje širokou škálu typů aplikací. Dostupné možnosti se pro jednotlivé typy aplikací liší. Intune umožňuje přidat a přiřadit tyto typy aplikací:

| Typy aplikací | Instalace | Aktualizace |
|---|---|---|
| Aplikace pocházející ze Storu (aplikace ze Storu) | Intune nainstaluje aplikaci na zařízení.  | Aplikace se aktualizují automaticky. |
| Interně napsané aplikace (obchodní) | Intune nainstaluje aplikaci na zařízení (vy dodáte instalační soubor). | Aplikaci musíte aktualizovat sami. |
| Aplikace, které jsou integrované (integrované aplikace) | Intune nainstaluje aplikaci na zařízení.  | Aplikace se aktualizují automaticky. |
| Aplikace na webu (webový odkaz) | Intune vytvoří zástupce webové aplikace na domovské obrazovce zařízení. | Aplikace se aktualizují automaticky. |
| Aplikace z jiných služeb Microsoftu  | Intune vytvoří zástupce aplikace v Portál společnosti. Další informace najdete v tématu [Možnosti nastavení zdroje aplikace](../apps/company-portal-app.md#app-source-setting-options). | Aplikace se aktualizují automaticky. |

### <a name="specific-app-type-details"></a>Podrobnosti o konkrétním typu aplikace
 
Následující tabulka obsahuje konkrétní typy aplikací a popis, jak je můžete přidat v podokně **Přidat aplikaci** v Intune:

| **Konkrétní typ aplikace** | **Obecný typ** | **Konkrétní postupy aplikace** |
| --- | --- | --- |
| Aplikace pro Android Store  | Aplikace pro Store  | Jako **typ aplikace** vyberte **Android** a zadejte adresu URL obchodu Google Play pro aplikaci. |
| Podnikové aplikace pro Android  | Aplikace pro Store  | Jako **Typ aplikace**vyberte **Android** a zadejte adresu URL spravovaného Google Play Storu pro aplikaci. <sup>1</sup> |
| aplikace pro iOS/iPadOS Store  | Aplikace pro Store  | Jako **typ aplikace** vyberte **iOS**, vyhledejte aplikaci a vyberte aplikaci v Intune. |
| Aplikace pro Microsoft Store  | Aplikace pro Store  | Jako **Typ aplikace**vyberte **Windows** a zadejte adresu URL obchodu Microsoft Store pro aplikaci. |
| Spravované aplikace Google Play | Aplikace pro Store  | Jako **Typ aplikace**vyberte **spravovaná Google Play** , vyhledejte aplikaci a vyberte aplikaci v Intune. |
| Aplikace Office 365 pro Windows 10  | Aplikace pro Store (Office 365) | V části **Microsoft 365 aplikace** jako **Typ aplikace**vyberte **Windows 10** a pak vyberte aplikaci Office 365, kterou chcete nainstalovat.  |
| Aplikace Office 365 pro macOS | Aplikace pro Store (Office 365) | V části **Microsoft 365 aplikace** jako **Typ aplikace**vyberte **MacOS** a pak vyberte sadu aplikací Office 365. |
| Microsoft Edge, verze 77 a novější pro Windows 10 | Aplikace pro Store | V části Microsoft Edge vyberte **Windows 10** **, verze 77 a novější** jako **Typ aplikace**. |
| Microsoft Edge, verze 77 a novější pro macOS | Aplikace pro Store | Jako **Typ aplikace**vyberte **MacOS** v části **Microsoft Edge, verze 77 a novější** . |
| Obchodní aplikace (LOB) pro Android | Obchodní aplikace | Jako **Typ aplikace**vyberte **obchodní** aplikaci, vyberte **soubor balíčku aplikace**a pak zadejte instalační soubor pro Android s příponou **. apk**.  |
| aplikace LOB pro iOS/iPadOS | Obchodní aplikace | Jako **Typ aplikace**vyberte **obchodní** aplikaci, vyberte **soubor balíčku aplikace**a pak zadejte instalační soubor pro iOS/iPadOS s příponou **. ipa**.  |
| Obchodní aplikace pro Windows | Obchodní aplikace | Jako typ aplikace vyberte **Obchodní**, vyberte **Soubor balíčku aplikace** a pak zadejte instalační soubor pro Windows s příponou **.msi**, **.appx**, **.appxbundle**, **.msix** nebo **.msixbundle**. |
| Integrovaná aplikace pro iOS/iPadOS  | Integrovaná aplikace | Jako **typ aplikace** vyberte **Integrovaná aplikace** a potom integrovanou aplikaci vyberte v seznamu poskytovaných aplikací.  |
| Integrovaná aplikace pro Android  | Integrovaná aplikace | Jako **typ aplikace** vyberte **Integrovaná aplikace** a potom integrovanou aplikaci vyberte v seznamu poskytovaných aplikací.  |
| Webové aplikace  | Webová aplikace  | Jako **typ aplikace** vyberte **Webový odkaz** a pak zadejte platnou adresu URL odkazující na webovou aplikaci.  |
| Systémové aplikace typu Android Enterprise  | Aplikace pro Store  | Jako **Typ aplikace**vyberte **aplikace pro Android Enterprise System** a potom zadejte název aplikace, vydavatele a soubor balíčku.  |
| Aplikace pro Windows (Win32)  | Obchodní aplikace  | Jako **typ aplikace** vyberte **aplikaci pro Windows (Win32)**, vyberte **Soubor balíčku aplikace** a pak vyberte instalační soubor s příponou **.intunewin**.  |
| Obchodní aplikace pro macOS | Obchodní aplikace  | Jako **Typ aplikace**vyberte **obchodní** typ, vyberte **soubor balíčku aplikace**a pak vyberte instalační soubor s příponou **. intunemac**.  |

<sup>1</sup> Další informace o pracovních profilech Androidu a Enterprise a Android najdete v části [Principy licencovaných aplikací](apps-add.md#understanding-licensed-apps) níže.

Aplikaci můžete do Microsoft Intune přidat tak, že vyberete **aplikace**  >  **všechny aplikace**  >  **Přidat**. Zobrazí se podokno **Vybrat typ aplikace** a můžete vybrat **Typ aplikace**. 

>[!TIP]
> Obchodní aplikace je aplikace, kterou přidáte z instalačního souboru aplikace. Pokud třeba chcete nainstalovat aplikaci LOB pro iOS/iPadOS, přidáte aplikaci tak, že jako **Typ aplikace** v podokně **Vybrat typ aplikace** vyberete **obchodní aplikace** . Potom vyberete soubor balíčku aplikace (má příponu .ipa). Tyto typy aplikací obvykle vznikají interně.

## <a name="assess-app-requirements"></a>Vyhodnocení požadavků na aplikaci
Jako správce IT určujete nejen to, které aplikace vaše skupina musí používat, ale i funkce potřebné pro jednotlivé skupiny a podskupiny. U každé aplikace určujete vhodnou platformu, skupiny uživatelů, které aplikaci potřebují, zásady konfigurace, které se mají použít u těchto skupin uživatelů, a zásady ochrany, které se mají použít.  

Dále musíte určit, jestli je třeba zaměřit se na správu mobilních zařízení (MDM) nebo jestli bude stačit správa mobilních aplikací (MAM). 

Správa zařízení pomocí MDM přes Intune je užitečná v těchto případech:
- Uživatelé potřebují Wi-Fi nebo firemní připojení k síti VPN, aby mohli vykonávat svoji práci.
- Uživatelé potřebují sadu aplikací, které se na jejich zařízení budou doručovat bez vyžádání.
- Vaše organizace musí dodržovat zákonné nebo jiné zásady, které vyžadují konkrétní řídicí mechanismy MDM, jako je zabezpečení nebo šifrování.

Správa aplikací pomocí MAM přes Intune bez správy zařízení je užitečná v těchto případech:
- Uživatelům chcete povolit používání vlastních zařízení (BYOD).
- Místo průběžných upozornění na zařízení chcete uživatelům jednorázově zobrazit zprávu, že jste zavedli ochranu MAM.
- Chcete zajistit soulad se zásadami, které vyžadují méně funkcí pro správu na osobních zařízeních. Chcete například spravovat firemní data u aplikací, ale nechcete je spravovat na celém zařízení.

Další informace najdete v tématu [Porovnání správy mobilních zařízení (MDM) a správy mobilních aplikací (MAM)](../fundamentals/byod-technology-decisions.md).

### <a name="determine-who-will-use-the-app"></a>Určení, kdo bude používat aplikaci

Při určování, které aplikace vaši pracovníci potřebují, zvažte různé skupiny uživatelů a různé aplikace, které používají. Znalost těchto skupin je užitečná i po přidání aplikace. Až aplikaci přidáte, přiřadíte skupinu uživatelů, která bude danou aplikaci moct používat. 

Nejprve na základě citlivosti dat obsažených v aplikaci musíte určit skupinu, která bude mít k aplikaci přístup. Je možné, že budete muset zahrnout nebo vyloučit určité typy rolí v rámci organizace. Pro vaši prodejní skupinu se například můžou vyžadovat jenom některé obchodní aplikace, ale lidé z technického, finančního, personálního nebo právního oddělení obchodní aplikaci používat nemusí. Dále vaše prodejní skupina může na svých mobilních zařízeních potřebovat další ochranu dat a přístup k interním firemním službám. Musíte určit, jak se tato skupina bude přes aplikaci připojovat k prostředkům. Budou se data, ke kterým má aplikace přístup, uchovávat v cloudu nebo místně? Musíte také promyslet, jak se uživatelé budou přes aplikaci připojovat k prostředkům. 

Intune podporuje také povolení přístupu pro klientské aplikace, které vyžadují zabezpečený přístup k místním datům, jako jsou servery obchodních aplikací. Tento typ přístupu se obvykle zajišťuje pomocí [certifikátů spravovaných službou Intune](../protect/certificates-configure.md) pro řízení přístupu v kombinaci se standardní bránou sítě VPN nebo proxy serverem v hraniční síti, například Proxy aplikací služby Azure Active Directory. [Nástroj pro zabalení aplikace v Intune a sada App SDK](../developer/apps-prepare-mobile-application-management.md) můžou pomáhat s tím, že se data v rámci vaší obchodní aplikace budou pořizovat, takže nemůže předat podnikovým aplikacím nebo službám.

S určením, jak máte identifikovat organizační skupiny pro jednotlivé scénáře použití a dílčí použití, vám pomůže [Průvodce plánováním nasazení, návrhem a implementací Intune](../fundamentals/planning-guide.md). Informace o přiřazení aplikací ke skupinám najdete v článku [Přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).

### <a name="determine-the-type-of-app-for-your-solution"></a>Určení typu aplikace pro konkrétní řešení

Vybírat můžete z těchto typů aplikací:
- **Aplikace ze Storu**: aplikace, které se nahrály do obchodu Microsoft Storu, iOS/iPadOS nebo Store pro Android, jsou aplikace pro Store. Poskytovatel aplikace pro Store udržuje a poskytuje aktualizace aplikace. Aplikaci si vyberete v seznamu v obchodě Store a přidáte ji pomocí Intune jako aplikaci dostupnou pro vaše uživatele.
- **Interně napsané aplikace (obchodní)**: Aplikace vytvořené interně se nazývají obchodní aplikace (LOB). Funkce tohoto typu aplikace se vytvořila pro jednu z podporovaných platforem Intune, jako je Windows, iOS/iPadOS, macOS nebo Android. Vaše organizace vytvoří a poskytuje aktualizace jako samostatný soubor. Aktualizace aplikace poskytujete uživatelům tak, že přidáte a nasadíte aktualizace přes Intune.
- **Aplikace na webu**: Webová aplikace představuje aplikaci klient-server. Server poskytuje webovou aplikaci, která zahrnuje uživatelské rozhraní, obsah a funkce. Moderní webové hostingové platformy dále běžně nabízejí zabezpečení, vyrovnávání zatížení a další výhody. Tento typ aplikace se samostatně udržuje na webu. Na tento typ aplikace se odkazuje pomocí Intune. Můžete také určit, které skupiny uživatelů mají k aplikaci přístup. Všimněte si, že Android webové aplikace nepodporuje.
- **Aplikace z jiných služeb Microsoftu**: aplikace, které byly vytvořené z Azure AD nebo Office Online. **Podnikové aplikace Azure AD** se registrují a přiřazují prostřednictvím [Azure Portal](https://portal.azure.com). **Aplikace Office Online** se přiřazují pomocí řídicích mechanismů licencování dostupných v [centru pro správu M365](https://admin.microsoft.com). Můžete skrýt nebo zobrazit aplikace služby Azure AD Enterprise a Office Online koncovým uživatelům v Portál společnosti. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **přizpůsobení správy tenanta**  >  **Customization** a najděte toto nastavení konfigurace. Tuto možnost vyberte, pokud chcete pro každého koncového uživatele **Skrýt** nebo **Zobrazit** buď **aplikace Azure AD Enterprise** nebo **aplikace Office Online** , v portál společnosti. Každý koncový uživatel uvidí ze zvolené služby Microsoftu celý katalog aplikací. Ve výchozím nastavení se každý další zdroj aplikace nastaví jako **skrytý**. Další informace najdete v tématu [Možnosti nastavení zdroje aplikace](../apps/company-portal-app.md#app-source-setting-options). 

Při určování aplikací potřebných pro vaši organizaci zvažte, jak se tyto aplikace integrují s cloudovými službami, k jakým datům mají aplikace přístup, jestli jsou aplikace dostupné pro uživatele, kteří používají vlastní zařízení (BYOD), a jestli aplikace vyžadují přístup k internetu.

Další informace o typech aplikací, které vaše organizace potřebuje, najdete v části Aplikace v oddílu Funkční požadavky článku [Vytvoření návrhu](../fundamentals/planning-guide-design.md#feature-requirements).

### <a name="understanding-app-management-and-protection-policies"></a>Principy zásad ochrany a správy aplikací
Intune vám umožňuje upravit funkce nasazovaných aplikací tak, aby byly v souladu se zásadami dodržování předpisů a zabezpečení vaší společnosti. Tento řídicí mechanismus vám umožňuje určit, jak jsou data vaší společnosti chráněná. Aplikace spravované přes Intune jsou povolené s bohatou sadou zásad ochrany mobilních aplikací, jako jsou:

- Omezení funkcí kopírování a vkládání a uložení jako
- Konfigurace webových odkazů, které se otevřou v aplikaci Microsoft Edge.
- Povolení použití více identit a podmíněného přístupu na úrovni aplikace.

Aplikace spravované přes Intune můžou také povolit ochranu aplikací bez nutnosti registrace, čímž vám umožňují použít zásady ochrany před únikem informací bez správy uživatelských zařízení. Pomocí sady Intune App SDK a nástroje App Wrapping můžete dále do mobilních a obchodních aplikací začlenit i správu mobilních aplikací. Další informace o těchto nástrojích najdete v článku [Přehled sady Intune App SDK](../developer/app-sdk.md).

### <a name="understanding-licensed-apps"></a>Princip licencovaných aplikací
Kromě pochopení webových aplikací, aplikací pro Store a obchodních aplikací byste měli také něco vědět o cíli aplikací programu Volume Purchase Program a licencovaných aplikací, jako jsou: 
- **Apple Volume purchase program for Business (iOS)**: App Store pro iOS/iPadOS umožňuje nakoupit více licencí pro aplikaci, kterou chcete ve své firmě spustit. Zakoupením více kopií můžete efektivně spravovat aplikace ve vaší společnosti. Další informace najdete v tématu [Správa hromadně zakoupených aplikací iOiOS/iPadOSS](vpp-apps-ios.md).
- **Pracovní profil Androidu**: Zařízením s pracovním profilem Androidu se aplikace přiřazují jiným způsobem než zařízením se standardním Androidem. Všechny aplikace, které instalujete pro pracovní profily Androidu, pocházejí ze spravovaného obchodu Google Play. Intune můžete použít k vyhledání aplikací, které chcete, a jejich schválení. Aplikace se pak zobrazí v uzlu **Licencované aplikace** na portálu Azure Portal a můžete spravovat přiřazení aplikace stejně jako u jakékoli jiné aplikace.
- **Microsoft Store pro firmy (Windows 10)**: Microsoft Store pro firmy je místo, kde můžete najít a zakoupit aplikace pro svou organizaci, a to jednotlivě i hromadně. Pokud Store propojíte s Microsoft Intune, můžete hromadně zakoupené aplikace spravovat na portálu Azure Portal. Další informace najdete v článku [Správa aplikací zakoupených v Microsoft Storu pro firmy](windows-store-for-business.md).

    > [!NOTE]
    > Mezi přípony souborů aplikací Windows patří **.msi**, **.appx**, **.appxbundle**, **.msix** a **.msixbundle**.  

## <a name="before-you-add-apps"></a>Před přidáním aplikací
Než začnete aplikace přidávat a přiřazovat, zvažte následující body:

- Pokud chcete přidat a přiřadit aplikaci z obchodu, musí mít uživatelé u tohoto obchodu zřízený účet, aby si aplikaci mohli nainstalovat.
- Některé aplikace nebo položky, které přiřadíte, můžou záviset na integrovaných aplikacích pro iOS/iPadOS. Pokud například přiřadíte knihu v úložišti iOS/iPadOS, musí se v zařízení vyskytovat aplikace iBooks. Pokud jste integrovanou aplikaci iBooks odebrali, nemůžete ji pomocí Intune obnovit.

> [!IMPORTANT]
> Pokud po nasazení a instalaci aplikace změníte název aplikace pomocí Intune na portálu Azure Portal, nebude už možné na tuto aplikaci cílit příkazy.

## <a name="cloud-storage-space"></a>Prostor v cloudovém úložišti
Všechny aplikace, které vytváříte pomocí instalace typu Instalační program softwaru (například obchodní aplikace), se zabalí a nahrají do cloudového úložiště Intune. Zkušební předplatné Intune zahrnuje 2 gigabajty (GB) cloudového úložiště, které se používá k ukládání spravovaných aplikací a aktualizací. Plné předplatné neomezuje celkový objem úložného prostoru.

Požadavky na cloudové úložiště jsou následující:

- Všechny instalační soubory musí být umístěné stejné složce.
- Maximální velikost nahrávaného souboru je 8 GB.

  > [!NOTE]
  > Obchodní aplikace pro Windows, včetně Win32, Windows Universal AppX, sady Windows Universal AppX, Windows Universal MSI X a sady Windows Universal MSI X, mají maximální velikost 8 GB na aplikaci. Všechny ostatní obchodní aplikace, včetně obchodních aplikací pro iOS/iPadOS, mají omezení maximální velikosti 2 GB na aplikaci.

## <a name="create-and-edit-categories-for-apps"></a>Vytvoření a úprava kategorií pro aplikace

Když aplikace seřadíte do kategorií, uživatelé je jednodušeji najdou na portálu společnosti. K aplikaci můžete přiřadit jednu i více kategorií, například *Aplikace pro vývojáře* nebo *Aplikace pro komunikaci*.

Když přidáte aplikaci do Intune, budete mít možnost vybrat požadovanou kategorii. Informace k přidání aplikací a přiřazení kategorií získáte v tématech pro jednotlivé platformy. Pokud chcete vytvořit a upravit vlastní kategorie, postupujte podle následujících pokynů:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **Apps**  >  **kategorie aplikací**pro aplikace.  
    V podokně **Kategorie aplikací** se zobrazí seznam aktuálních kategorií. 
5. Proveďte jednu z následujících akcí:
    - Pokud chcete přidat kategorii, v podokně **Vytvořit kategorii** vyberte **Přidat** a zadejte název kategorie.  
    Názvy je možné zadat jenom v jednom jazyce a služba Intune je nepřekládá.
    - Pokud chcete kategorii upravit, vyberte tři tečky (**...**) vedle kategorie a pak vyberte **Připnout na řídicí panel** nebo **Odstranit**.
6. Vyberte **Vytvořit**.

## <a name="apps-that-are-added-automatically-by-intune"></a>Aplikace přidané automaticky službou Intune

Dříve služba Intune obsahovala řadu integrovaných aplikací, které jste mohli rychle přiřadit. Na základě názorů zákazníků Intune jsme tento seznam odebrali a integrované aplikace se už nezobrazují. Pokud jste už ale nějaké integrované aplikace přiřadili, budou se v seznamu aplikací zobrazovat i nadále. Aplikace můžete dál přiřazovat podle potřeby.

> [!NOTE]
> Pro instalaci požadované neobchodní aplikace se Intune pokusí nainstalovat aplikaci odesláním instalačního příkazu, když se zařízení zaregistruje, a když se nezjistí stav instalace aplikace, *čeká na instalaci*.

## <a name="installing-updating-or-removing-required-apps"></a>Instalace, aktualizace a odebrání požadovaných aplikací

Intune automaticky přeinstaluje, aktualizuje nebo odebere požadovanou aplikaci během 24 hodin a nebude čekat na 7denní cyklus opakovaného vyhodnocení.

Intune automaticky přeinstaluje, aktualizuje nebo odebere požadovanou aplikaci na základě těchto podmínek:
- Pokud koncový uživatel odinstaluje aplikaci, jejíž instalaci na jeho zařízení požadujete, Intune automaticky tuto aplikaci přeinstaluje po uplynutí naplánované doby.
- Pokud se požadovanou aplikaci nepodaří nainstalovat nebo aplikace na zařízení z nějakého důvodu chybí, Intune vyhodnotí dodržování předpisů a přeinstaluje aplikaci po uplynutí naplánované doby.  
- Správce nastaví aplikaci pro skupinu uživatelů jako dostupnou a koncoví uživatelé si ji nainstalují na zařízení z Portálu společnosti. Později správce aktualizuje aplikaci z v1 na v2. Intune aktualizuje aplikaci, jakmile uplyne naplánovaná doba, za předpokladu, že je na zařízení některá z předchozích verzí dané aplikace.
- Pokud se správce rozhodne aplikaci odinstalovat, ale aplikaci se nepodaří ze zařízení odinstalovat, Intune vyhodnotí dodržování předpisů a odinstaluje aplikaci po uplynutí naplánované doby.   

## <a name="uninstall-an-app"></a>Odinstalace aplikace

Pokud potřebujete odinstalovat aplikaci ze zařízení uživatele, použijte následující postup.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vybrat **aplikace**  >  **všechny aplikace**  >  *the app*  >  **přiřazení**aplikace  >  **Přidat skupinu**.
3. V podokně **Přidat skupinu** vyberte **odinstalovat**.
4. Vyberte možnost **zahrnuté skupiny** a vyberte skupiny uživatelů, na které se vztahuje přiřazení této aplikace.
5. Vyberte skupiny, u kterých chcete použít přiřazení odinstalace.
6. V podokně **Vybrat skupiny** klikněte na **Vybrat** .
7. Nastavte přiřazení kliknutím na **OK** v podokně **přiřazení** .
8. Pokud se rozhodnete některé skupiny uživatelů vyloučit, aby nebyly přiřazením aplikace ovlivněné, klikněte na **Vyloučit skupiny**.
9. Pokud jste se rozhodli některé skupiny vyloučit, ve **Vybrat skupiny** zvolte **Vybrat**.
10. V podokně **Přidat skupinu** vyberte **OK** .
11. V podokně **přiřazení** aplikace vyberte **Uložit** .

> [!IMPORTANT]
> Aby se aplikace úspěšně odinstalovala, nezapomeňte odebrat členy nebo přiřazení skupiny pro instalaci, než je přiřadíte k odinstalování. Pokud je skupina přiřazena k instalaci aplikace i k odinstalaci aplikace, aplikace zůstane a nebude odebrána.

## <a name="app-installation-errors"></a>Chyby instalace aplikací

Podrobnosti o chybách instalace aplikací Intune najdete v tématu [Chyby instalace aplikací](troubleshoot-app-install.md).

## <a name="next-steps"></a>Další kroky

Informace o tom, jak přidat aplikace pro jednotlivé platformy do Intune, najdete tady:

- [Aplikace pro Android Store](store-apps-android.md)
- [Obchodní aplikace pro Android](lob-apps-android.md)
- [Aplikace pro iOS Store](store-apps-ios.md)
- [Obchodní aplikace pro iOS](lob-apps-ios.md)
- [Obchodní aplikace pro macOS](lob-apps-macos.md)
- [Webové aplikace (pro všechny platformy)](web-app.md)
- [Aplikace pro Microsoft Store](store-apps-windows.md)
- [Obchodní aplikace pro Windows](lob-apps-windows.md)
- [Aplikace Office 365 pro Windows 10](apps-add-office365.md)
- [Aplikace Office 365 pro macOS](apps-add-office365-macos.md)
- [Spravované aplikace Google Play](apps-add-android-for-work.md)
- [Microsoft Edge pro Windows 10](apps-windows-edge.md)
- [Microsoft Edge pro macOS](apps-edge-macos.md)
- [Integrované aplikace](apps-add-built-in.md)
- [Aplikace systému Android Enterprise](apps-ae-system.md)
- [Aplikace Win32](apps-win32-app-management.md)
