---
title: Správa Microsoft Edge pro iOS a Android s Intune
titleSuffix: ''
description: Pomocí zásad ochrany aplikací Intune s Microsoft Edge zajistíte, aby se k podnikovým webům vždycky používala ochrana na pracovišti.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 373c3c5a6a3167943d78e5a17ac9b7cab8afba8a
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943854"
---
# <a name="manage-web-access-by-using-microsoft-edge-with-microsoft-intune"></a>Správa webového přístupu pomocí Microsoft Edge s Microsoft Intune

Použití zásad ochrany aplikací Intune s Microsoft Edge pomáhá zajistit, aby se k podnikovým webům vždycky používaly bezpečnostní opatření na pracovišti. K dispozici jsou následující funkce Microsoft Edge Enterprise, které jsou povolené zásadami Intune:

- **Dual-identity.** Uživatelé můžou přidat pracovní účet i osobní účet pro procházení. Mezi těmito dvěma identitami se dokončí oddělení, které se podobá architektuře a prostředí v aplikacích Office 365 a Outlook. Správci Intune můžou nastavit požadované zásady pro chráněné prostředí pro procházení v rámci pracovního účtu.
- **Integrace zásad ochrany aplikací Intune.** Vzhledem k tomu, že je Microsoft Edge integrovaný do sady Intune SDK, můžete zacílit zásady ochrany aplikací na ochranu před ztrátou dat. Mezi tyto možnosti patří řízení vyjmutí, kopírování a vložení, prevence zachycení obrazovky a zajištění, že se odkazy vybrané uživatelem otevírají jenom v jiných spravovaných aplikacích.
- **Integrace služby Azure Application proxy.** Můžete řídit přístup k aplikacím software jako služba (SaaS) a webovým aplikacím. To pomáhá zajistit, aby se aplikace založené na prohlížeči spouštěly pouze v zabezpečeném prohlížeči Microsoft Edge, ať už se koncoví uživatelé připojují z podnikové sítě nebo se připojují z Internetu.
- **Konfigurace aplikace** Pomocí nastavení konfigurace aplikace můžete posílit zabezpečení stav vaší organizace a nakonfigurovat funkce snadného použití pro koncové uživatele. Můžete například definovat záložky, zástupce domovské stránky, povolené nebo Blokované weby a proxy aplikace Azure Active Directory (Azure AD).

Zásady ochrany Microsoft Intune pro Microsoft Edge usnadňují ochranu dat a prostředků vaší organizace. Pomocí těchto zásad s Microsoft Edge zajistíte ochranu prostředků vaší společnosti nejen v nativně nainstalovaných aplikacích, ale také při jejich použití prostřednictvím webového prohlížeče.

## <a name="getting-started"></a>Začínáme

Vy a vaši koncoví uživatelé si můžete stáhnout Microsoft Edge z veřejných obchodů s aplikacemi pro použití ve svých organizacích. Požadavky na operační systém pro zásady prohlížeče jsou některé z těchto možností:
- Android 5 a novější
- iOS 12,0 a novější

## <a name="application-protection-policies-for-microsoft-edge"></a>Zásady ochrany aplikací pro Microsoft Edge

Vzhledem k tomu, že je Microsoft Edge integrovaný do sady Intune SDK, můžete pro ně použít zásady ochrany aplikací.

Tato nastavení můžete použít na:
- Zařízení zaregistrovaná v Intune.
- Zařízení zaregistrovaná v jiném produktu pro správu mobilních zařízení.
- Nespravovaná zařízení.

Pokud Microsoft Edge necílí na zásady Intune, uživatelé ji nemůžou použít pro přístup k datům z jiných aplikací spravovaných pomocí Intune, jako jsou například aplikace Office. 

   >[!NOTE]
   > Pokud se použije zásada Save-as, která zabraňuje stažení obrázku, je u Microsoft Edge zakázaná dlouhá stisknutí.

## <a name="conditional-access-for-microsoft-edge"></a>Podmíněný přístup pro Microsoft Edge

Podmíněný přístup Azure AD můžete použít k přesměrování uživatelů na přístup k firemnímu obsahu jenom přes Microsoft Edge. Tím se omezí přístup k webovým aplikacím připojeným k Azure AD na Microsoft Edge s ochranou zásad v mobilním prohlížeči. Tato aplikace blokuje přístup ze všech ostatních nechráněných prohlížečů, jako je Safari nebo Chrome. Můžete použít podmíněný přístup k prostředkům Azure, jako jsou Exchange Online a SharePoint Online, centrum pro správu Microsoft 365 a dokonce i místní weby, které jste provedli na externích uživatelích přes [Azure proxy aplikací služby AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

> [!NOTE]
> Nové webové klipy (připnuté webové aplikace) na zařízeních se systémem iOS se otevřou v Microsoft Edge místo Intune Managed Browser, pokud je to potřeba pro otevření v chráněném prohlížeči. U starších webových klipů pro iOS je nutné tyto webové klipy změnit na místo toho, aby je bylo možné otevřít v Microsoft Edge, Managed Browser.

Omezení webové aplikace připojené k Azure AD na používání Microsoft Edge v iOS a Androidu:
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. V uzlu Intune vyberte **podmíněný přístup** > **Nová zásada**.
3. V části **řízení přístupu** v podokně vyberte **udělit** .
4. Vyberte **Vyžaduje se klientem schválená aplikace**.
5. V podokně **grant** zvolte **Vybrat** . Tuto zásadu musíte přiřadit ke cloudovým aplikacím, které mají být dostupné jenom pro aplikaci Intune Managed Browser.

    ![Snímek obrazovky se zásadami podmíněného přístupu – grant](./media/manage-microsoft-edge/manage-microsoft-edge-01.png)

6. V části přiřazení vyberte**aplikace** **podmínky** > . Zobrazí se podokno **aplikace** .
7. V části **Konfigurovat**vyberte **Ano** , pokud chcete zásady použít pro konkrétní klientské aplikace.
8. Zkontrolujte, že je jako klientská aplikace vybraná možnost **Prohlížeč**.

    ![Snímek obrazovky se zásadami podmíněného přístupu – vybrat klientské aplikace](./media/manage-microsoft-edge/manage-microsoft-edge-02.png)

    > [!NOTE]
    > Pokud chcete omezit to, které nativní (neprohlížečové) aplikace mají přístup k těmto cloudovým aplikacím, můžete také vybrat **Mobilní aplikace a desktopoví klienti**.

9. V části **přiřazení** vyberte **Uživatelé a skupiny**a pak zvolte uživatele nebo skupiny, kterým chcete tuto zásadu přiřadit.

10. V části **Přiřazení** vyberte **Cloudové aplikace** a zvolte, které aplikace chcete chránit pomocí této zásady.

Po nakonfigurování výše uvedených zásad budou uživatelé nuceni používat Microsoft Edge pro přístup k webovým aplikacím připojeným k Azure AD, které jste s touto zásadou chráněni. Pokud se uživatelé v tomto scénáři pokusí použít nespravovaný prohlížeč, obdrží zprávu, že musí používat Microsoft Edge.

> [!TIP]
> Podmíněný přístup je technologie Azure AD. Uzel podmíněného přístupu, ke kterému se přistupuje z Intune, je stejný uzel, ke kterému se přistupuje z Azure AD.

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Jednotné přihlašování k webovým aplikacím připojeným k Azure AD v prohlížečích chráněných zásadami

Microsoft Edge v iOS a Androidu může využít jednotné přihlašování (SSO) pro všechny webové aplikace (SaaS a místní), které jsou připojené ke službě Azure AD. Jednotné přihlašování umožňuje uživatelům přístup k webovým aplikacím připojeným k Azure AD prostřednictvím Microsoft Edge, aniž by museli znovu zadávat své přihlašovací údaje.

Jednotné přihlašování vyžaduje, aby zařízení bylo zaregistrované v aplikaci Microsoft Authenticator pro zařízení s iOS nebo Portál společnosti Intune na Androidu. Když je uživatel z nich, zobrazí se výzva k registraci svého zařízení při přechodu na webovou aplikaci připojenou k Azure AD v prohlížeči chráněném zásadami. (To platí jenom v případě, že zařízení ještě není zaregistrované.) Po registraci zařízení u účtu uživatele spravovaného službou Intune má tento účet povolený jednotné přihlašování pro webové aplikace připojené k Azure AD.

> [!NOTE]
> Registrace zařízení představuje jednoduché vrácení se změnami pomocí služby Azure AD. Nevyžaduje úplný zápis zařízení a neposkytuje mu žádná další oprávnění k tomuto zařízení.

## <a name="create-a-protected-browser-app-configuration"></a>Vytvoření konfigurace aplikace chráněného prohlížeče

Vytvoření konfigurace aplikace pro Microsoft Edge:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **zásady** > konfigurace aplikace**Přidat**.
3. V podokně **Přidat zásady konfigurace** zadejte **název** a volitelný **Popis** nastavení konfigurace aplikace.
4. Jako typ **Registrace zařízení** zvolte **Spravované aplikace**.
5. Zvolte **vybrat požadovanou aplikaci**. Pak v podokně **cílové aplikace** zvolte **Managed Browser** nebo **Edge** pro iOS/iPadOS, Android nebo pro obojí.
6. Kliknutím na **OK** se vraťte do podokna **Přidat zásady konfigurace** .
7. Klikněte na **Nastavení konfigurace**. V podokně **Konfigurace** definujte páry klíč-hodnota pro zadání konfigurací pro Microsoft Edge. Informace o různých párech klíč a hodnota, které můžete definovat, najdete v dalších částech tohoto článku.

    > [!NOTE]
    > Microsoft Edge používá stejné dvojice klíč-hodnota jako Managed Browser. V Androidu musí být Microsoft Edge cílem zásad ochrany aplikací, aby se projevily zásady konfigurace aplikací.

8. Jakmile budete hotovi, vyberte **OK**.
9. V podokně **Přidat zásady konfigurace** klikněte na možnost **Přidat**.<br>
    Nová konfigurace se vytvoří a zobrazí v podokně **Konfigurace aplikace** .

## <a name="assign-the-configuration-settings-you-created"></a>Přiřazení vytvořeného nastavení aplikace 

Nastavení přiřadíte skupinám uživatelů ve službě Azure AD. Pokud má daný uživatel cílovou aplikaci chráněného prohlížeče nainstalovanou, spravuje se podle vámi zadaného nastavení.

1. V podokně **aplikace** na řídicím panelu Správa mobilních aplikací Intune vyberte **zásady konfigurace aplikací**.
2. V seznamu konfigurací aplikací vyberte tu, kterou chcete přiřadit.
3. V dalším podokně vyberte **přiřazení**.
4. V podokně **přiřazení** vyberte skupinu Azure AD, ke které chcete přiřadit konfiguraci aplikace, a pak vyberte **OK**.

## <a name="direct-users-to-microsoft-edge-instead-of-the-intune-managed-browser"></a>Přímé nasměrování uživatelů na Microsoft Edge místo Intune Managed Browser 

Microsoft Edge se dá použít jako prohlížeč chráněný zásadami. Aby bylo zajištěno, že budou vaši uživatelé směrováni na používání správné aplikace v prohlížeči, zaměřte se na všechny aplikace spravované přes Intune (například Outlook, OneDrive a SharePoint) s následujícím nastavením konfigurace:

|    Key    |    Hodnota    |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.useEdge`    |    Hodnota `true` přesměruje uživatele na stažení a používání Microsoft Edge.<br>Tato hodnota `false` umožní uživatelům používat Intune Managed Browser.    |

Pokud tato hodnota konfigurace aplikace není **nastavená** , v následující logice se určí, který prohlížeč se použije k otevření firemních odkazů.

V Androidu:
- Intune Managed Browser se spustí, pokud má uživatel Intune Managed Browser a Microsoft Edge stažený na svém zařízení. 
- Microsoft Edge se spustí, pokud se na zařízení stáhne jenom Microsoft Edge a je zaměřený na zásady Intune.
- Managed Browser se spustí, pokud se na zařízení používá jenom Managed Browser a je zaměřený na zásady Intune.

Pro iOS/iPadOS pro aplikace, které mají integrovanou sadu Intune SDK pro iOS v. 9.0.9+:
- Intune Managed Browser se spustí, pokud se na zařízení nachází Managed Browser a Microsoft Edge.  
- Microsoft Edge se spustí, pokud je na zařízení jenom Microsoft Edge a je zaměřený na zásady Intune.
- Managed Browser se spustí, pokud se na zařízení používá jenom Managed Browser a je zaměřený na zásady Intune.

## <a name="configure-application-proxy-settings-for-microsoft-edge"></a>Konfigurace nastavení proxy aplikace pro Microsoft Edge

Pomocí Microsoft Edge a [Azure proxy aplikací služby AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) můžete poskytnout uživatelům přístup k intranetovým webům na svých mobilních zařízeních. 

Toto jsou některé příklady scénářů, které Azure Proxy aplikací služby AD povolit: 

- Uživatel používá mobilní aplikaci Outlook, která je chráněná službou Intune. Pak klikněte na odkaz na intranetový server v e-mailu a Microsoft Edge rozpozná, že tento intranetový server byl uživateli zpřístupněn prostřednictvím proxy aplikací. Uživatel je automaticky směrován prostřednictvím proxy aplikace, aby před dosažením intranetového serveru provedl ověřování pomocí služby Multi-Factor Authentication a podmíněného přístupu. Uživatel teď může získat přístup k interním webům i na jejich mobilních zařízeních a odkaz v Outlooku funguje podle očekávání.
- Uživatel otevře Microsoft Edge na svém zařízení s iOS nebo Androidem. Pokud je Microsoft Edge chráněný pomocí Intune a proxy aplikací je povolený, může uživatel přejít na intranetový server pomocí interní adresy URL, ke které se používá. Microsoft Edge rozpozná, že tento intranetový server byl uživateli zpřístupněn prostřednictvím proxy aplikací. Uživatel je automaticky směrován prostřednictvím proxy aplikace, aby bylo možné provést ověření před dosažením intranetového webu. 

### <a name="before-you-start"></a>Než začnete

- Pomocí Proxy aplikací služby AD Azure nastavte interní aplikace.
  - Postup konfigurace proxy aplikací a publikování aplikací najdete v [dokumentaci k instalaci](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- Aplikace Microsoft Edge musí mít přiřazenou [zásadu ochrany aplikací Intune](app-protection-policy.md) .

> [!NOTE]
> Aktualizovaným datům přesměrování proxy aplikací může trvat až 24 hodin, než se projeví v aplikaci Managed Browser nebo Microsoft Edge.

#### <a name="step-1-enable-automatic-redirection-to-microsoft-edge-from-outlook"></a>Krok 1: povolení automatického přesměrování na Microsoft Edge z Outlooku
Nakonfigurujte Outlook pomocí zásad ochrany aplikací, které umožňují nastavení **sdílet webový obsah pomocí prohlížečů spravovaných zásadou**.

![Snímek obrazovky se zásadami ochrany aplikací – sdílení webového obsahu pomocí prohlížečů spravovaných zásadou](./media/manage-microsoft-edge/manage-microsoft-edge-03.png)

#### <a name="step-2-set-the-app-configuration-setting-to-enable-app-proxy"></a>Krok 2: nastavení konfigurace aplikace pro povolení proxy aplikací
Aby bylo možné povolit proxy aplikace pro Microsoft Edge, cílovému serveru Microsoft Edge s následující dvojicí klíč/hodnota:

|    Key    |    Hodnota    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    true    |

Další informace o tom, jak používat Microsoft Edge a Azure Proxy aplikací služby AD společně pro bezproblémový (a chráněný) přístup k místním webovým aplikacím, najdete v tématu [lepší spolupráce: Intune a Azure Active Directory tým pro zlepšení přístupu uživatelů](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). Tento Blogový příspěvek odkazuje na Intune Managed Browser, ale obsah platí i pro Microsoft Edge.

## <a name="configure-a-homepage-shortcut-for-microsoft-edge"></a>Konfigurace zástupce domovské stránky pro Microsoft Edge

Toto nastavení umožňuje nakonfigurovat zástupce domovské stránky pro Microsoft Edge. Zástupce domovské stránky, který nakonfigurujete, se zobrazí jako první ikona pod panelem hledání, když uživatel otevře novou kartu v Microsoft Edge. Uživatel nemůže tohoto zástupce v spravovaném kontextu upravit ani odstranit. Zástupce domovské stránky zobrazuje název vaší organizace a rozlišuje ho. 

Použijte následující dvojici klíč/hodnota ke konfiguraci zástupce domovské stránky:

|    Key    |    Hodnota    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Zadejte platnou adresu URL. Nesprávné adresy URL se z bezpečnostních důvodů blokují.<br>**Případě** <`https://www.bing.com`>     |

## <a name="configure-multiple-top-site-shortcuts-for-new-tab-pages-in-microsoft-edge"></a>Konfigurace více nejoblíbenějších zástupců webů pro nové stránky karet v Microsoft Edge 
Podobně jako při konfiguraci zástupce domovské stránky můžete na nové stránky karty na webu Microsoft Edge nakonfigurovat několik nejoblíbenějších zástupců webů. Uživatel nemůže tyto klávesové zkratky ve spravovaném kontextu upravit ani odstranit. Poznámka: můžete nakonfigurovat celkem 8 klávesových zkratek, včetně zástupce domovské stránky. Pokud jste nakonfigurovali zástupce domovské stránky, přepíše se první nejvyšší nakonfigurovaná lokalita. 

|    Key    |    Hodnota    |
|-------------------------------------------------------------------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. managedTopSites   |    Zadejte sadu hodnot URL. Každý hlavní zástupce webu se skládá z názvu a adresy URL. Název a adresu URL oddělte `|` znakem. Příklad: <br> `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

## <a name="configure-your-organizations-logo-and-brand-color-for-new-tab-pages-in-microsoft-edge"></a>Nakonfigurovat logo vaší organizace a barvu značky pro nové stránky karet v Microsoft Edge

Tato nastavení umožňují přizpůsobit novou stránku karty pro Microsoft Edge a zobrazovat logo vaší organizace a barvu značky jako pozadí stránky.

Pokud chcete nahrát logo a barvu vaší organizace, nejdřív proveďte následující kroky:
-  -> V Azure Portal přejděte do centra pro [správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)přizpůsobení**Správa** -> tenanta**přizpůsobení** -> **identity společnosti**.
- Pokud chcete nastavit logo značky, vyberte v části zobrazit možnost pouze logo společnosti. Doporučují se průhledné loga na pozadí. 
- Chcete-li nastavit barvu pozadí vaší značky, v části Zobrazit Vyberte možnost Barva motivu. Microsoft Edge použije světlejší barevný stín na nové stránce karty, což zajistí vysokou čitelnost stránky. 

Pak použijte následující páry klíč/hodnota, které přidělí vaší organizaci branding do Microsoft Edge:

|    Key    |    Hodnota    |
|--------------------------------------------------------------------|------------|
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. BrandLogo    |    True    |
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. BrandColor    |    True    |

## <a name="display-relevant-industry-news-on-new-tab-pages"></a>Zobrazit relevantní novinky v odvětví na nových stránkách karty

V rámci Microsoft Edge Mobile můžete nakonfigurovat nové možnosti stránky s kartami a zobrazit tak novinky v oboru, které jsou relevantní pro vaši organizaci. Když tuto funkci povolíte, Microsoft Edge Mobile použije název domény vaší organizace k agregaci zpráv z webu o vaší organizaci, oboru organizace a konkurenci, takže vaši uživatelé můžou najít relevantní externí novinky z centralizované stránky nové karty v rámci Microsoft Edge. Novinky v oboru jsou ve výchozím nastavení vypnuté a můžete je použít k jejímu přihlášení ve vaší organizaci. 

|    Key    |    Hodnota    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. IndustryNews    |    **hodnota true** zobrazí zprávy v odvětví na stránce Nová karta pro mobilní zařízení Microsoft Edge.<p>**False** (výchozí) skryje v oboru zprávy na nové kartě.    |

## <a name="configure-managed-bookmarks-for-microsoft-edge"></a>Konfigurace spravovaných záložek pro Microsoft Edge

Pro usnadnění přístupu můžete nakonfigurovat záložky, které chcete, aby uživatelé měli k dispozici, když používají Microsoft Edge. 

Tady jsou některé podrobnosti:

- Tyto záložky se zobrazí pouze uživatelům, kteří používají [podnikový režim](https://docs.microsoft.com/intune/apps/app-configuration-managed-browser#how-to-configure-bookmarks-for-a-protected-browser) Microsoft Edge. 
- Tyto záložky nemohou uživatelé odstranit ani upravit.
- Tyto záložky se zobrazí v horní části seznamu. Všechny záložky, které vytvářejí uživatelé, se zobrazí pod těmito záložkami.
- Pokud jste povolili přesměrování proxy aplikací, můžete přidat webové aplikace proxy aplikací pomocí své interní nebo externí adresy URL.
- Při zadávání adres URL do seznamu se ujistěte, že jste zadali předponu všechny adresy URL pomocí **http://** nebo **https://** .

Ke konfiguraci spravovaných záložek použijte následující pár klíč/hodnota:

|    Key    |    Hodnota    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    Hodnota této konfigurace je seznam záložek. Každá záložka se skládá z názvu záložky a adresy URL záložky. Název a adresu URL oddělte `|` znakem.      Příklad:<br>`Microsoft Bing|https://www.bing.com`<br>Chcete-li nakonfigurovat více záložek, oddělte každou dvojici dvojitým znakem `||`.<p>Příklad:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

## <a name="display-myapps-within-microsoft-edge-bookmarks"></a>Zobrazit MyApp v záložkách Microsoft Edge

Ve výchozím nastavení se uživatelům zobrazí weby aplikace Mojeapl, které jsou pro ně nakonfigurované ve složce uvnitř záložek Microsoft Edge. Složka je označena názvem vaší organizace.

|    Key    |    Hodnota    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. MyApps    |    **hodnota true** zobrazí MyApp v rámci záložek Microsoft Edge.<p>**Hodnota false** skryje aplikaci MyApp v rámci Microsoft Edge.    |
    
## <a name="use-https-protocol-as-default"></a>Jako výchozí použít protokol HTTPS

Můžete nastavit Microsoft Edge Mobile na výchozí, aby používal protokol HTTPS, když ho uživatel nezadá. Obecně se to považuje za osvědčený postup. K povolení protokolu HTTPS jako výchozího protokolu použijte následující pár klíč/hodnota:

|    Key    |    Hodnota    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.defaultHTTPS`     |     **true** nastaví výchozí protokol pro použití HTTPS.     |


## <a name="specify-allowed-or-blocked-sites-list-for-microsoft-edge"></a>Zadejte seznam povolených nebo blokovaných webů pro Microsoft Edge.
Pomocí konfigurace aplikace můžete definovat, ke kterým lokalitám mají uživatelé přístup při používání jejich pracovního profilu. Pokud použijete seznam povolených uživatelů, budou mít uživatelé přístup jenom k webům, které jste výslovně zadali. Pokud použijete seznam blokovaných uživatelů, budou mít uživatelé přístup ke všem webům kromě těch, které jste výslovně zablokovali. Měli byste jenom nastavit buď povolený, nebo blokovaný seznam, ne obojí. Pokud napíšete obojí, bude se jednat o povolený seznam.  

Pomocí následujících párů klíč/hodnota můžete nakonfigurovat seznam povolených nebo blokovaných webů pro Microsoft Edge. 

|    Key    |    Hodnota    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Vybírejte z těchto možností:<p>1. Zadejte povolené adresy URL (jenom tyto adresy URL jsou povoleny, k žádným jiným webům nelze přicházet):<br>`com.microsoft.intune.mam.managedbrowser.AllowListURLs`<p>2. Zadejte blokované adresy URL (všechny ostatní weby jsou k dispozici):<br>`com.microsoft.intune.mam.managedbrowser.BlockListURLs`    |    Odpovídající hodnotou klíče je seznam adres URL. Zadejte všechny adresy, které chcete povolit nebo blokovat, a to jako jedinou hodnotu rozdělenou svislou čárou `|`.<br>**4.6**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`  |

Následující lokality jsou vždy povoleny bez ohledu na nastavení definovaného seznamu povolených nebo blokovaných seznamů:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

### <a name="url-formats-for-allowed-and-blocked-site-list"></a>Formáty adres URL pro seznam povolených a blokovaných webů 
K vytvoření seznamu povolených a blokovaných webů můžete použít různé formáty adresy URL. Tyto povolené vzory jsou podrobně popsány v následující tabulce. Některé poznámky než začnete: 
- Při zadávání adres URL do seznamu se ujistěte, že jste zadali předponu všechny adresy URL pomocí **http://** nebo **https://** .
- V souladu s pravidly v následujícím seznamu\*povolených vzorů můžete použít zástupný znak ().
- Zástupný znak může odpovídat jenom celé součásti názvu hostitele (oddělené tečkami) nebo celými částmi cesty (oddělené lomítky). Například `http://*contoso.com` **není podporován.**
- V adrese můžete specifikovat čísla portů. Pokud nezadáte číslo portu, použijí se tyto hodnoty:
  - Port 80 pro protokol HTTP
  - Port 443 pro protokol HTTPS
- Použití zástupných znaků pro číslo portu **není podporováno.** Například `http://www.contoso.com:*` a `http://www.contoso.com:*/` podporované nejsou. 

    |    zprostředkovatele identity    |    Podrobnosti    |    Shody    |    Neodpovídá    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Odpovídá jediné stránce    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Odpovídá jediné stránce    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    Odpovídá všem adresám URL začínajícím na `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Vyhledá všechny subdomény pod`contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Odpovídá všem subdoménám končícím na`contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Odpovídá jediné složce    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Odpovídá jedné stránce s použitím čísla portu    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Odpovídá jediné zabezpečené stránce    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Odpovídá jediné složce a všem podsložkám    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Tady jsou uvedené příklady některých vstupů, které nemůžete zadat:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP adresy
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

## <a name="transition-users-to-their-personal-context-when-trying-to-access-a-blocked-site"></a>Při pokusu o přístup k blokovanému webu převeďte uživatele do svého osobního kontextu.

Pomocí modelu duální identity postaveného na Microsoft Edge můžete vašim koncovým uživatelům povolit flexibilnější prostředí, než bylo možné s Intune Managed Browser. Když uživatelé projdou blokovaný web na Microsoft Edge, můžete je vyzvat, aby otevřeli odkaz v jejich osobním kontextu místo jejich pracovního kontextu. Díky tomu můžou být pořád chráněná a přitom udržují firemní prostředky v bezpečí. Pokud se například uživateli pošle odkaz na článek příspěvky prostřednictvím Outlooku, může odkaz otevřít v osobním kontextu nebo na kartě InPrivate. Jejich pracovní kontext neumožňuje webům s novinkami. Ve výchozím nastavení jsou tyto přechody povoleny.

Použijte následující dvojici klíč/hodnota ke konfiguraci, zda jsou tyto měkké přechody povoleny:

|    Key    |    Hodnota    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock`    |    **true** (výchozí) umožňuje Microsoft Edge přejít uživatele do svého osobního kontextu a otevřít blokované weby.<p>**False** zabrání Microsoft Edge v převodu uživatelů. Uživatelům se zobrazí zpráva s informacemi o tom, že lokalita, ke které se pokouší získat přístup, je blokovaná.    |

## <a name="open-restricted-links-directly-in-inprivate-tab-pages"></a>Otevřít omezené odkazy přímo na kartách InPrivate

Můžete nakonfigurovat, jestli mají být odkazy s omezeným přístupem otevřeny přímo v procházení InPrivate, což uživatelům poskytuje pohodlnější možnosti procházení. Tím ušetříte uživatelům krok pro převzetí služeb při selhání do svého osobního kontextu pro zobrazení lokality. Procházení InPrivate je považováno za nespravované, takže uživatelé nebudou mít přístup při použití režimu procházení InPrivate.  Poznámka: aby se toto nastavení projevilo, musíte také nakonfigurovat výše uvedené nastavení `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock` na **hodnotu true**.

|    Key    |    Hodnota    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked`    |    **hodnota true** automaticky otevře weby přímo na kartě InPrivate bez vyzvání uživatele, aby provedl přepnutí na svůj osobní účet. <p> **Hodnota false** (výchozí) zablokuje web v rámci Microsoft Edge a uživatel se zobrazí výzva k přepnutí na svůj osobní účet k zobrazení.    |


## <a name="disable-microsoft-edge-features-to-customize-the-end-user-experience-for-your-organizations-needs"></a>Vypnutí funkcí Microsoft Edge pro přizpůsobení prostředí koncových uživatelů pro potřeby vaší organizace

### <a name="disable-prompts-to-share-usage-data-for-personalization"></a>Zakázat výzvy ke sdílení dat o využití pro přizpůsobení 

Ve výchozím nastavení vyzve Microsoft Edge uživatele k shromažďování dat o využití a přizpůsobení jejich možností procházení. Sdílení těchto dat můžete zakázat tím, že zabráníte zobrazení této výzvy koncovým uživatelům. 

|    Key    |    Hodnota    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableShareUsageData`    |     **hodnota true** zakáže zobrazení této výzvy koncovým uživatelům.    |

### <a name="disable-prompts-to-share-browsing-history"></a>Zakázat zobrazování výzev ke sdílení historie procházení 

Ve výchozím nastavení vyzve Microsoft Edge uživatele k shromažďování dat historie procházení a k přizpůsobení jejich možností procházení. Sdílení těchto dat můžete zakázat tím, že zabráníte zobrazení této výzvy koncovým uživatelům.

|    Key    |    Hodnota    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory`    |     **hodnota true** zakáže zobrazení této výzvy koncovým uživatelům.     |

### <a name="disable-prompts-that-offer-to-save-passwords"></a>Zakázat výzvy, které umožňují uložit hesla

Ve výchozím nastavení nabízí Microsoft Edge na iOS k ukládání hesel uživatelů do řetězce klíčů. Pokud chcete zakázat tuto výzvu pro vaši organizaci, nakonfigurujte následující nastavení:

|    Key    |    Hodnota    |
|-----------------------|-----------------------|
|    `com.microsoft.intune.mam.managedbrowser.disabledFeatures`    |    **heslo** zakáže výzvy, které nabízí ukládání hesel pro koncového uživatele.    |

### <a name="disable-users-from-adding-extensions-to-microsoft-edge"></a>Zakázat uživatelům přidávat rozšíření do Microsoft Edge 

Můžete zakázat rozhraní rozšíření v rámci Microsoft Edge, aby uživatelé nemohli instalovat jakékoli aplikace v rozsahu. Uděláte to tak, že nakonfigurujete následující nastavení:

|    Key    |    Hodnota    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableExtensionFramework`    |    **hodnota true** zakáže rozhraní rozšíření.    |

### <a name="disable-inprivate-browsing-and-microsoft-accounts-to-restrict-browsing-to-work-only-contexts"></a>Zakázání procházení InPrivate a účtů Microsoft pro omezení prohlížení na kontexty, které jsou jenom pro práci

Pokud vaše organizace funguje v vysoce regulovaném odvětví nebo používá síť VPN pro jednotlivé aplikace, která uživatelům umožňuje přístup k pracovním prostředkům přes Microsoft Edge, můžete se rozhodnout pro procházení InPrivate v Microsoft Edge, které je považováno za nepracovní kontext. 

|    Key    |    Hodnota    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disabledFeatures`    |    Služba **InPrivate** vypíná procházení InPrivate.   |

### <a name="restrict-microsoft-edge-use-to-allowed-accounts-only"></a>Omezit použití Microsoft Edge jenom na povoleno – účty

Kromě blokování procházení InPrivate a MSA můžete použít Microsoft Edge jenom v případě, že je uživatel přihlášený pomocí svého účtu AAD. Tato funkce je dostupná jenom pro uživatele zaregistrované v MDM. Další informace o konfiguraci tohoto nastavení najdete tady:

>[!NOTE]
> `com.microsoft.intune.mam.managedbrowser.disabledFeatures`dá se použít k zákazu více funkcí současně. Pokud například chcete zakázat InPrivate a heslo, použijte `inprivate|password`.

## <a name="configure-microsoft-edge-as-a-kiosk-app-on-android-devices"></a>Konfigurace Microsoft Edge jako aplikace veřejného terminálu na zařízeních s Androidem

### <a name="enable-microsoft-edge-as-a-kiosk-app"></a>Povolit Microsoft Edge jako beznabídkovou aplikaci
Pokud chcete Microsoft Edge povolit jako beznabídkovou aplikaci, nejdřív nakonfigurujte toto nadřazené nastavení:

|    Key    |    Hodnota    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.enableKioskMode`    |    **true** povolí konfiguraci veřejného terminálu pro Microsoft Edge.    |

### <a name="show-address-bar-in-kiosk-mode"></a>Zobrazit adresní řádek v celoobrazovkovém režimu
Pokud chcete zobrazit adresní řádek v Microsoft Edge, když je v celoobrazovkovém režimu, nakonfigurujte následující nastavení:

|    Key    |    Hodnota    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode`    |    **hodnota true** zobrazí adresní řádek. <br> **hodnota false** (výchozí) skryje adresní řádek.    |

### <a name="show-bottom-action-bar-in-kiosk-mode"></a>Zobrazit spodní panel akcí v celoobrazovkovém režimu
|    Key    |    Hodnota    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode`    |    **hodnota true** zobrazí dolní panel akcí v rámci Microsoft Edge. <br> **false** (výchozí) skryje spodní panel.    |


## <a name="use-microsoft-edge-to-access-managed-app-logs"></a>Přístup k protokolům spravovaných aplikací pomocí Microsoft Edge


Uživatelé s Microsoft Edge nainstalované na svém zařízení s iOS nebo Androidem můžou zobrazit stav správy všech aplikací publikovaných Microsoftem. Můžou odesílat protokoly pro řešení potíží se spravovanými aplikacemi pro iOS nebo Android pomocí následujících kroků:

1. Otevřete na svém zařízení Microsoft Edge.
2. Do pole adresy zadejte `about:intunehelp`.
3. Microsoft Edge spustí režim řešení potíží.

Seznam nastavení uložených v aplikačních protokolech najdete v tématu [Kontrola protokolů ochrany aplikace v aplikaci Managed Browser](app-protection-policy-settings-log.md).

Informace o tom, jak zobrazit protokoly na zařízeních s Androidem, najdete v tématu [odeslání protokolů správci IT e-mailem](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="security-and-privacy-for-microsoft-edge"></a>Zabezpečení a ochrana osobních údajů pro Microsoft Edge

Níže jsou uvedené další požadavky na zabezpečení a ochranu osobních údajů pro Microsoft Edge:

- Microsoft Edge nevyužívá nastavení, která uživatelé nastavili pro nativní prohlížeč na svých zařízeních, protože Microsoft Edge nemá k těmto nastavením přístup.
- Můžete nakonfigurovat možnost **vyžadovat pro přístup jednoduchý kód PIN** nebo **vyžadovat pro přístup podnikové přihlašovací údaje** v zásadách ochrany aplikací přidružených k Microsoft Edge. Pokud uživatel na stránce ověřování vybere odkaz na odkaz, může procházet libovolné internetové weby bez ohledu na to, zda byly přidány do blokovaného seznamu v zásadě.
- Microsoft Edge může blokovat přístup k webům jenom v případě, že se k nim přistupuje přímo. Neblokuje přístup, pokud uživatelé k přístupu k webu použijí zprostředkující služby (třeba překladatelské služby).
- Pokud chcete povolení ověřování a přístup k dokumentaci k Intune, ***. Microsoft.com** se vyloučí z nastavení povoleného a blokovaného seznamu. Je vždycky povolená.
- Uživatelé mohou shromažďování dat vypnout. Microsoft automaticky shromažďuje anonymní informace o výkonu a využití aplikace Managed Browser za účelem zlepšení svých produktů a služeb. Uživatelé můžou shromažďování těchto dat na svých zařízeních vypnout pomocí nastavení **Data o využití**. Nad shromažďováním těchto dat nemáte žádnou kontrolu. Na zařízeních se systémem iOS se nedají otevřít weby, u kterých vypršela platnost certifikátu nebo které mají nedůvěryhodný certifikát.

## <a name="restrict-microsoft-edge-use-to-a-work-or-school-account"></a>Omezení použití Microsoft Edge na pracovní nebo školní účet

Dodržování zásad zabezpečení a dodržování předpisů u našich největších a vysoce regulovaných zákazníků je klíčovým pilířem Microsoft 365 hodnoty. Některé společnosti mají požadavek na zachycení všech komunikačních informací v rámci svého podnikového prostředí, a to i v případě, že se zařízení používají jenom pro firemní komunikaci. Pro podporu těchto požadavků je možné nakonfigurovat Edge pro iOS a Android na registrovaných zařízeních tak, aby umožňovala zřídit jenom jeden podnikový účet, který se zřídí v rámci hraničních zařízení pro iOS a Android.

Další informace o konfiguraci nastavení režimu povolených účtů organizace najdete tady:

- [Nastavení Androidu](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [nastavení iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="next-steps"></a>Další kroky

- [Co jsou zásady ochrany aplikací?](app-protection-policy.md) 
