---
title: Správa podnikového webového přístupu pomocí prohlížeče chráněného zásadami
titleSuffix: Microsoft Intune
description: Pomocí prohlížeče chráněného zásadami, který je přiřazený přes Intune, můžete spravovat procházení podnikových webů a přenášení webových dat.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1feca24f-9212-4d5d-afa9-7c171c5e8525
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 936dc5d4167252fcb2280ca3c9aa8b450a924a98
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083637"
---
# <a name="manage-web-access-using-a-microsoft-intune-policy-protected-browser"></a>Správa webového přístupu pomocí Microsoft Intune prohlížeče chráněného zásadami

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Pomocí prohlížeče chráněného zásadami Intune (Microsoft Edge nebo Intune Managed Browser) můžete zajistit, že se při přístupu k podnikovým webům vždy uplatní ochranná opatření.  Po nakonfigurování se službou Intune můžete využít následujících výhod chráněných prohlížečů:

- Zásady ochrany aplikací
- Podmíněný přístup
- Jednotné přihlašování
- Nastavení konfigurace aplikace
- Integrace služby Azure Application proxy

> [!IMPORTANT]
> Intune Managed Browser bude vyřazen. Využijte Microsoft Edge pro vaše chráněné prostředí Intune Browser. 

## <a name="microsoft-edge-support"></a>Podpora Microsoft Edge

Na zařízeních s iOS/iPadOS a Androidem můžete na podnikových scénářích použít Microsoft Edge. Microsoft Edge podporuje všechny stejné scénáře správy jako Intune Managed Browser s přidáním vylepšení pro činnost koncového uživatele. Následující funkce Microsoft Edge Enterprise, které jsou povolené zásadami Intune, zahrnují:

- **Dual-identity** – uživatelé můžou pro procházení přidat jak pracovní účet, tak i osobní účet. Mezi těmito dvěma identitami se dokončí oddělení, které se podobá architektuře a prostředí v aplikacích Office 365 a Outlook. Správci Intune budou moct nastavit požadované zásady pro chráněné prostředí pro procházení v rámci pracovního účtu. 
- **Integrace zásad ochrany aplikací Intune** – správci teď můžou cílit na zásady ochrany aplikací na Microsoft Edge, včetně ovládacího prvku pro vyjmutí, kopírování a vložení, zabránění zachycení obrazovky a zajištění, aby se odkazy vybrané uživatelem otevíraly jenom v jiných spravovaných aplikacích.
- **Integrace služby Azure Application proxy** – správci můžou řídit přístup k aplikacím SaaS a webovým aplikacím, což pomáhá zajistit, aby se aplikace založené na prohlížeči spouštěly jenom v zabezpečeném prohlížeči Microsoft Edge, ať už se koncoví uživatelé připojují z podnikové sítě nebo se připojí z Internetu. 
- **Zástupci spravovaných oblíbených položek a domovské stránky** – pro usnadnění přístupu můžou správci nastavit adresy URL tak, aby se zobrazovaly v části Oblíbené, pokud jsou koncoví uživatelé ve firemním kontextu. Správci můžou nastavit zástupce domovské stránky, který se zobrazí jako primární zástupce, když firemní uživatel otevře novou stránku nebo novou kartu v Microsoft Edge.

Zásady ochrany Microsoft Intune pro Microsoft Edge usnadňují ochranu dat a prostředků vaší organizace. Microsoft Edge chráněný Intune zajišťuje ochranu prostředků vaší společnosti nejen v nativně nainstalovaných aplikacích, ale také při jejich použití prostřednictvím webového prohlížeče.

## <a name="getting-started"></a>Začínáme

Microsoft Edge a Intune Managed Browser jsou aplikace webového prohlížeče, které vy a vaši koncoví uživatelé můžete po stažení z některého z veřejných obchodů s aplikacemi využívat ve vaší organizaci. 

Požadavky na operační systém pro zásady prohlížeče:
- Android 4 a novější nebo
- iOS/iPadOS 8,0 a novější.

Starší verze systému Android a iOS/iPadOS budou moci nadále používat Managed Browser, ale nebudou moci instalovat nové verze aplikace a nemusí mít přístup ke všem funkcím aplikace. Doporučujeme vám tato zařízení aktualizovat na podporovanou verzi operačního systému.

>[!NOTE]
>Aplikace Managed Browser nepodporuje kryptografický protokol Secure Sockets Layer ve verzi 3 (SSLv3).


## <a name="application-protection-policies-for-protected-browsers"></a>Zásady ochrany aplikací pro chráněné prohlížeče

Aplikace Microsoft Edge a Managed Browser jsou integrované se sadou Intune SDK, takže v nich můžete používat také zásady ochrany aplikací, včetně:
- Řízení použití operací vyjmutí, kopírování a vložení
- Prevence pořizování snímků obrazovky
- Možnost otevírání podnikových odkazů jenom ve spravovaných aplikacích a prohlížečích

Podrobnosti najdete v článku [Co jsou zásady ochrany aplikací](app-protection-policy.md).

Tato nastavení můžete použít na:

- Zařízení, která jsou zaregistrovaná v Intune
- Zaregistrovaná pomocí jiného produktu MDM
- Nespravovaná zařízení

>[!NOTE]
>Pokud si uživatelé nainstalují aplikaci Managed Browser z obchodu s aplikacemi a služba Intune ji nebude spravovat, mohou ji používat jako základní webový prohlížeč s podporou jednotného přihlašování přes web Microsoft MyApps. Uživatelé jsou přesměrováni přímo na web MyApps, kde uvidí všechny své zřízené aplikace SaaS.
Pokud nejsou aplikace Managed Browser nebo Microsoft Edge spravované službou Intune, nemají přístup k datům jiných takto spravovaných aplikací. 


## <a name="conditional-access-for-protected-browsers"></a>Podmíněný přístup pro chráněné prohlížeče

Managed Browser je nově schválenou klientskou aplikací pro podmíněný přístup. To znamená, že můžete omezit přístup mobilních prohlížečů k webovým aplikacím připojeným ke službě Azure AD tak, aby uživatelé mohli používat jenom Managed Browser, a blokovat přístup ze všech ostatních nechráněných prohlížečů, například Safari nebo Chrome. Tato ochrana se dá použít na prostředky Azure, jako je Exchange Online a SharePoint Online, centrum pro správu Microsoft 365 a dokonce i místní weby, které jste nastavili pro externí uživatele prostřednictvím [Azure proxy aplikací služby AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started). 

> [!NOTE]
> Nové webové klipy (připnuté webové aplikace) na zařízeních se systémem iOS se otevřou v Microsoft Edge místo Intune Managed Browser, pokud je to potřeba pro otevření v chráněném prohlížeči. U starších webových klipů pro iOS je nutné tyto webové klipy změnit na místo toho, aby je bylo možné otevřít v Microsoft Edge, Managed Browser.

Pokud chcete webovým aplikacím připojeným ke službě Azure AD omezit možnost používání aplikace Intune Managed Browser na mobilních platformách, můžete vytvořit zásadu podmíněného přístupu, která vyžaduje schválené klientské aplikace. 

> [!TIP]  
> Podmíněný přístup je technologie Azure Active Directory (Azure AD). Uzel podmíněného přístupu, ke kterému se přistupuje z *Intune*, je stejný uzel, ke kterému se přistupuje z *Azure AD*.  

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **podmíněný přístup** > **nové zásady**.
3. Přidejte **název**zásady. 
4. V části **Přiřazení** vyberte **Podmínky** > **Klientské aplikace**. Zobrazí se podokno **klientské aplikace** .
5. V části **Konfigurovat** klikněte na **Ano**, aby se zásada použila u konkrétních klientských aplikací.
6. Zkontrolujte, že je jako klientská aplikace vybraná možnost **Prohlížeč**.

    ![Azure AD – Managed Browser – Výběr klientských aplikací](./media/app-configuration-managed-browser/managed-browser-conditional-access-02.png)

    > [!NOTE]
    > Pokud chcete omezit to, které nativní (neprohlížečové) aplikace mají přístup k těmto cloudovým aplikacím, můžete také vybrat **Mobilní aplikace a desktopoví klienti**.

7. Klikněte na **hotovo** > **Hotovo**.
8. V části **přiřazení** vyberte **Uživatelé a skupiny** a zvolte uživatele nebo skupiny, kterým chcete přiřadit tuto zásadu. Kliknutím na **Hotovo** zavřete podokno.
9. V části **přiřazení** vyberte **cloudové aplikace nebo akce** a vyberte aplikace, které chcete chránit pomocí těchto zásad. Kliknutím na **Hotovo** zavřete podokno.
10. V části **řízení přístupu** v podokně vyberte **udělit** . 
11. Klikněte na **udělit přístup** a pak klikněte na **vyžadovat schválenou klientskou aplikaci**. 
12. V podokně **udělení** klikněte na **Vybrat** . Tuto zásadu musíte přiřadit ke cloudovým aplikacím, které mají být dostupné jenom pro aplikaci Intune Managed Browser.

    ![Azure AD – Managed Browser zásady podmíněného přístupu](./media/app-configuration-managed-browser/managed-browser-conditional-access-01.png)



Jakmile nakonfigurujete výše uvedenou zásadu, budou uživatelé pro přístup k webovým aplikacím připojeným ke službě Azure AD, které chráníte pomocí této zásady, nuceni používat Intune Managed Browser. Pokud se uživatel pokusí v tomto scénáři použít nespravovaný prohlížeč, zobrazí se mu zpráva, že musí použít Intune Managed Browser.

Managed Browser nepodporuje zásady podmíněného přístupu na portálu Classic. Další informace najdete v článku [Migrace zásad z portálu Classic na portálu Azure Portal](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-migration).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Jednotné přihlašování k webovým aplikacím připojeným ke službě Azure AD v prohlížečích chráněných zásadami

Microsoft Edge a Intune Managed Browser v iOS/iPadOS a Androidu můžou využít výhody jednotného přihlašování pro všechny webové aplikace (SaaS a on-Prem), které jsou připojené ke službě Azure AD. Když je aplikace Microsoft Authenticator v systému iOS/iPadOS nebo v aplikaci Portál společnosti Intune v systému Android, uživatelé prohlížeče chráněného zásadami budou mít přístup k webovým aplikacím připojeným k Azure AD, aniž by museli znovu zadávat své přihlašovací údaje.

Jednotné přihlašování vyžaduje, aby vaše zařízení bylo zaregistrované v aplikaci Microsoft Authenticator v systému iOS/iPadOS nebo Portál společnosti Intune na Androidu. Uživatelům s aplikací Authenticator nebo Portálem společnosti Intune se zobrazí výzva, aby si zařízení zaregistrovali, když přejdou do webové aplikace připojené ke službě Azure AD v prohlížeči chráněném zásadami, pokud už nemají zařízení zaregistrováno jinou aplikací. Jakmile se zařízení zaregistruje pomocí účtu spravovaného přes Intune, bude mít tento účet povoleno jednotné přihlašování u webových aplikací připojených ke službě Azure AD. 

> [!NOTE]
> Registrace zařízení představuje jednoduché vrácení se změnami pomocí služby Azure AD. Nevyžaduje úplnou registraci zařízení a nedává pracovníkům IT žádná další oprávnění k zařízení.

## <a name="create-a-protected-browser-app-configuration"></a>Vytvoření konfigurace aplikace chráněného prohlížeče

>[!IMPORTANT]
>Aby se konfigurace aplikace použily, musí už na zařízení být chráněný prohlížeč nebo jiná aplikace uživatele spravovaná [zásadami ochrany aplikací Intune](app-protection-policy.md).

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **zásady konfigurace aplikací** > **Přidat** > **spravované aplikace**.
3. Na stránce **základy** v podokně **vytvořit zásadu konfigurace aplikace** zadejte **název** a volitelný **Popis** nastavení konfigurace aplikace.
4. Zvolte **vybrat veřejnou aplikaci** a zvolte **Managed Browser** a/nebo **Edge** pro iOS/iPadOS, pro Android nebo pro obojí.
5. Kliknutím na **Vybrat** se vraťte do podokna **vytvořit zásadu konfigurace aplikace** .
6. Kliknutím na **Další** zobrazte stránku **Nastavení** .
7. Na stránce **Nastavení** definujte páry klíč-hodnota pro zadání konfigurací pro aplikaci. Informace o různých párech klíč a hodnota, které můžete definovat, najdete v dalších částech tohoto článku.
8. Kliknutím na **Další** zobrazte stránku **přiřazení** a potom klikněte na **Vybrat skupiny** , které chcete zahrnout, nebo **Vyberte skupiny, které chcete vyloučit**.
9. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** .
10. Po kontrole zásad konfigurace aplikací klikněte na **vytvořit** .

Vytvoří se nová konfigurace, která se zobrazí v podokně **zásady konfigurace aplikace** .


## <a name="assign-the-configuration-settings-you-created"></a>Přiřazení vytvořeného nastavení aplikace

Nastavení přiřazujete skupinám uživatelů ve službě Azure AD. Pokud má daný uživatel cílovou aplikaci chráněného prohlížeče nainstalovanou, spravuje se podle vámi zadaného nastavení.

1. V podokně **aplikace** na řídicím panelu Správa mobilních aplikací Intune vyberte **zásady konfigurace aplikací**.
2. V seznamu konfigurací aplikací vyberte tu, kterou chcete přiřadit.
3. V dalším podokně klikněte na možnost **přiřazení**.
4. V podokně **přiřazení** vyberte skupinu Azure AD, ke které chcete přiřadit konfiguraci aplikace, a pak zvolte **OK**.

## <a name="how-to-set-microsoft-edge-as-the-protected-browser-for-your-organization"></a>Jak nastavit Microsoft Edge jako chráněný prohlížeč pro vaši organizaci

Toto nastavení umožňuje nakonfigurovat, jestli budou vaši uživatelé přesměrováni na Microsoft Edge nebo Intune Managed Browser, za předpokladu, že oba prohlížeče cílí na zásady ochrany aplikací. **Toto nastavení zásad konfigurace aplikace by mělo být cílené na spravované aplikace Intune, ze kterých se webový odkaz otevírá.** 

Pokud je toto nastavení nastaveno na hodnotu "pravda":

- Uživatelé budou při otevírání odkazů z aplikací spravovaných pomocí Intune, které jsou cílem tohoto nastavení, přesměrováni na Microsoft Edge. 
- Pokud aplikace ještě nemáte, zobrazí se jim výzva ke stažení Microsoft Edge ze Storu bez ohledu na to, jestli Intune Managed Browser stáhnout.

Pokud je toto nastavení nastaveno na hodnotu "NEPRAVDA":

- Pokud mají vaši uživatelé stažený **Managed Browser i Microsoft** Edge, Managed Browser se spustí. 
- Pokud vaši uživatelé stáhli Managed Browser **nebo** Microsoft Edge, **spustí se aplikace v prohlížeči** . 
- Pokud vaši uživatelé nestáhli žádnou aplikaci v prohlížeči, zobrazí se výzva ke stažení Managed Browser.

Pomocí výše uvedeného postupu vytvoříte konfiguraci aplikace Microsoft Edge. Při výběru **nastavení konfigurace** v podokně **Konfigurace** zadejte následující pár klíč-hodnota (krok 9):

| Klíč                              |  Hodnota   |
|----------------------------------|----------|
| **com. Microsoft. Intune. useEdge** | **true** |

> [!NOTE]
> V zásadách ochrany aplikací, které spravují Microsoft Edge a přidružené aplikace zadané v konfiguraci aplikace, zajistěte, aby byla nastavená tato nastavení zásad ochrany dat:
> - Posílání organizačních dat do jiných aplikací: **aplikace spravované podle zásad**
> - Omezení přenosu webového obsahu u jiných aplikací: **prohlížeče spravované podle zásad**

## <a name="how-to-configure-application-proxy-settings-for-protected-browsers"></a>Postup konfigurace nastavení proxy aplikací pro chráněné prohlížeče

Microsoft Edge a Intune Managed Browser a [Azure proxy aplikací služby AD]( https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) se dají použít společně k podpoře následujících scénářů pro uživatele zařízení se systémem iOS/IPadOS a Androidem:

- Uživatel stáhne aplikaci Microsoft Outlook a přihlásí se do ní. Zásady ochrany aplikací Intune se automaticky použijí. Zašifrují uložená data a zablokují uživateli možnost přesouvat firemní soubory do nespravovaných aplikací nebo umístnění na zařízení. Když uživatel potom v Outlooku klikne na odkaz směřující na intranetový server, můžete nastavit, aby takový odkaz otevřel místo běžného prohlížeče aplikaci chráněného prohlížeče. Chráněný prohlížeč rozpozná, že tento intranetový server se uživateli zpřístupnil prostřednictvím proxy aplikací. Uživatel je automaticky směrován prostřednictvím proxy aplikace, aby před dosažením intranetového serveru provedl ověření s jakýmkoli platným službou Multi-Factor Authentication a podmíněný přístup. Tento server, který nebylo dříve možné najít, když byl uživatel vzdálený, je nyní dostupný a odkaz v Outlooku funguje podle očekávání.
- Vzdálený uživatel otevře chráněný prohlížeč a přejde na intranetový server pomocí interní adresy URL. Chráněný prohlížeč rozpozná, že tento intranetový server se uživateli zpřístupnil prostřednictvím proxy aplikací. Uživatel je automaticky směrován prostřednictvím proxy aplikace, aby před dosažením intranetového serveru provedl ověření s jakýmkoli platným službou Multi-Factor Authentication a podmíněný přístup. Tento server, který nebylo možné najít, když byl uživatel vzdálený, je nyní dostupný.

### <a name="before-you-start"></a>Než začnete

- Nastavte svoje interní aplikace prostřednictvím proxy aplikací Azure AD.
  - Postup konfigurace proxy aplikací a publikování aplikací najdete v [dokumentaci k instalaci](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy). 
  - [Uživatelé musí být přiřazeni](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-add-on-premises-application#add-a-user-for-testing) k podnikové aplikaci, pro kterou bude provedeno přesměrování. To se musí udělat i v případě, že je aplikace nastavená na průchozí režim pro předběžné ověření a pokud je požadavek na přiřazení uživatele vypnutý v nastavení proxy serveru aplikace.
- Musíte používat minimálně verzi 1.2.0 aplikace Managed Browser.
- Uživatelé aplikace Managed Browser nebo Microsoft Edge mají k dané aplikaci přiřazené [zásady ochrany aplikací Intune](app-protection-policy.md).

    > [!NOTE]
    > Aktualizovaným datům přesměrování proxy aplikací může trvat až 24 hodin, než se projeví v aplikaci Managed Browser nebo Microsoft Edge.


#### <a name="step-1-enable-automatic-redirection-to-a-protected-browser-from-outlook"></a>Krok 1: Zapněte automatické přesměrování z Outlooku do chráněného prohlížeče.
Outlook musí být nakonfigurován zásadami ochrany aplikací, které povolují nastavení **Omezit webový obsah tak, aby se spouštěl v Managed Browseru**.

#### <a name="step-2-assign-an-app-configuration-policy-assigned-for-the-protected-browser"></a>Krok 2: přiřazení zásady konfigurace aplikace přiřazené chráněnému prohlížeči
Tento postup nakonfiguruje aplikaci Managed Browser nebo Microsoft Edge tak, aby používala přesměrování proxy aplikací. 

Otevřete kartu **Edge** v nastavení konfigurace pro zásadu a vyberte **Povolit** pro hodnotu přesměrování proxy aplikace. Povolením tohoto nastavení umožníte uživatelům přístup k firemním odkazům a místním webovým aplikacím, které jsou publikované prostřednictvím služby Azure Application proxy.

Další informace o tom, jak lze Managed Browser, Microsoft Edge a proxy aplikací Azure AD používat společně za účelem bezproblémového (a chráněného) přístupu k místním webovým aplikacím, najdete v blogovém příspěvku Enterprise Mobility + Security s názvem [Better together: Intune and Azure Active Directory team up to improve user access](https://cloudblogs.microsoft.com/enterprisemobility/2017/07/06/better-together-intune-and-azure-active-directory-team-up-to-improve-user-access) (Ve dvou se to lépe táhne: Intune a Azure Active Directory společně vylepšují uživatelský přístup).

## <a name="how-to-configure-the-homepage-for-a-protected-browser"></a>Postup konfigurace domovské stránky chráněného prohlížeče

Toto nastavení vám umožňuje nakonfigurovat domovskou stránku, kterou uživatelé uvidí, když chráněný prohlížeč spustí nebo když otevřou novou kartu. 
- Toto nastavení zobrazí webovou stránku v Managed Browseru.  Microsoft Edge místo toho zobrazí zástupce domovské stránky.
- Ikona zástupce domovské stránky se zobrazí jako ikona pod ovládacím prvkem vyhledávání.  Není možné ji upravit ani odstranit.
- Zástupce domovské stránky bude za účelem odlišení zobrazovat název vaší organizace.  Vždy se bude zobrazovat jako první ikona.

Pomocí postupu pro vytvoření konfigurace aplikace Managed Browser nebo Microsoft Edge zadejte následující dvojici klíč-hodnota:

|                                Klíč                                |                                                           Hodnota                                                            |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| <strong>com.microsoft.intune.mam.managedbrowser.homepage</strong> | Zadejte platnou adresu URL. Nesprávné adresy URL se z bezpečnostních důvodů blokují.<br>Příklad: `https://www.bing.com` |

## <a name="how-to-configure-bookmarks-for-a-protected-browser"></a>Postup konfigurace záložek chráněného prohlížeče

Toto nastavení vám umožňuje nakonfigurovat sadu záložek, které budou dostupné uživatelům aplikace Microsoft Edge nebo Managed Browser.

- Tyto záložky nemohou uživatelé odstranit ani upravit.
- Tyto záložky se zobrazí v horní části seznamu. Všechny záložky vytvořené uživateli se zobrazí pod těmito záložkami.
- Pokud jste povolili přesměrování Proxy aplikací, můžete přidat webové aplikace Proxy aplikací pomocí jejich interní nebo externí adresy URL.

Pomocí postupu pro vytvoření konfigurace aplikace Managed Browser nebo Microsoft Edge zadejte následující dvojici klíč-hodnota:

|                                Klíč                                 |                                                                                                                                                                                                                                                         Hodnota                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <strong>com.microsoft.intune.mam.managedbrowser.bookmarks</strong> | Hodnotou pro tuto konfiguraci je seznam záložek. Každou záložku tvoří název záložky a adresa URL záložky. Název a adresu URL oddělte znakem <strong>&#124;</strong>.<br><br>Příklad:<br> <code>Microsoft Bing&#124;https://www.bing.com</code><br><br>Pokud chcete nakonfigurovat více záložek, oddělte každý pár těmito dvěma znaky: <strong>&#124;&#124;</strong>.<br><br>Příklad:<br> <code>Bing&#124;https://www.bing.com&#124;&#124;Contoso&#124;https://www.contoso.com</code> |

## <a name="how-to-specify-allowed-and-blocked-urls-for-a-protected-browser"></a>Určení povolených a blokovaných adres URL v chráněném prohlížeči

Pomocí postupu pro vytvoření konfigurace aplikace Managed Browser nebo Microsoft Edge zadejte následující dvojici klíč-hodnota:

|Klíč|Hodnota|
|-|-|
|Vybírejte z těchto možností:<br><ul><li>Určení povolených adres URL (povolené jsou pouze tyto adresy URL; na žádné jiné weby nebudou mít uživatelé přístup):<br> **com.microsoft.intune.mam.managedbrowser.AllowListURLs**<br><br></li><li>Určení blokovaných adres URL (na všechny ostatní weby budou mít uživatelé přístup):<br>**com.microsoft.intune.mam.managedbrowser.BlockListURLs**</li></ul>|Odpovídající hodnotou klíče je seznam adres URL. Zadejte všechny adresy, které chcete povolit nebo blokovat, jako jedinou hodnotu oddělenou znaky svislé čáry **&#124;** .<br><br>Příklady:<br><br><code>URL1&#124;URL2&#124;URL3</code><br><code>http://*.contoso.com/*&#124;https://*.bing.com/*&#124;https://expenses.contoso.com</code>|

>[!IMPORTANT]
>Nezadávejte oba klíče. Pokud budou oba klíče cílit na stejného uživatele, použije se klíč pro určení povolených adres, protože představuje nejvíce omezující možnost.
>Dále také zkontrolujte, že nejsou blokovány důležité weby, jako například webové stránky vaší organizace.

### <a name="url-format-for-allowed-and-blocked-urls"></a>Formát adresy URL pro povolené a blokované adresy URL
V následující části najdete informace o povolených formátech a zástupných znacích, které můžete použít při zadávání adres URL v seznamech povolených a blokovaných webů:

- V souladu s následujícími pravidly můžete v seznamu povolených vzorů použít zástupný znak ( **&#42;** ).

- Při zadávání adres URL do seznamu nezapomeňte u všech uvést předponu **http** nebo **https** .

- V adrese můžete specifikovat čísla portů. Pokud nezadáte číslo portu, použijí se tyto hodnoty:

  - Port 80 pro protokol HTTP

  - Port 443 pro protokol HTTPS

  Použití zástupných znaků pro číslo portu se nepodporuje. Například `http://www.contoso.com:;` a `http://www.contoso.com: /;` podporované nejsou.

- Informace o povolených vzorech, které můžete použít při zadávání adres URL, najdete v následující tabulce:

|                  URL                  |                     Podrobnosti                      |                                                Odpovídá                                                |                                Neodpovídá                                 |
|---------------------------------------|--------------------------------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
|        `http://www.contoso.com`         |              Odpovídá jediné stránce               |                                            `www.contoso.com`                                            |  `host.contoso.com`<br /><br />`www.contoso.com/images`<br /><br />`contoso.com`/   |
|          `http://contoso.com`           |              Odpovídá jediné stránce               |                                             `contoso.com/`                                              | `host.contoso.com`<br /><br />`www.contoso.com/images`<br /><br />`www.contoso.com` |
|    `http://www.contoso.com/&#42;`     | Odpovídá všem adresám URL začínajícím na `www.contoso.com` |      `www.contoso.com`<br /><br />`www.contoso.com/images`<br /><br />`www.contoso.com/videos/tvshows`      |              `host.contoso.com`<br /><br />`host.contoso.com/images`              |
|    `http://*.contoso.com/*`     |     Odpovídá všem dílčím doménám domény contoso.com     | `developer.contoso.com/resources`<br /><br />`news.contoso.com/images`<br /><br />`news.contoso.com/videos` |                               `contoso.host.com`                                |
|     `http://www.contoso.com/images`     |             Odpovídá jediné složce              |                                        `www.contoso.com/images`                                         |                          `www.contoso.com/images/dogs`                          |
|       `http://www.contoso.com:80`       |  Odpovídá jediné stránce s použitím čísla portu   |                                       `http://www.contoso.com:80`                                       |                                                                               |
|        `https://www.contoso.com`        |          Odpovídá jediné zabezpečené stránce           |                                        `https://www.contoso.com`                                        |                            `http://www.contoso.com`                             |
| `http://www.contoso.com/images/&#42;` |    Odpovídá jediné složce a všem podsložkám    |                  `www.contoso.com/images/dogs`<br /><br />`www.contoso.com/images/cats`                   |                            `www.contoso.com/videos`                             |

- Tady jsou uvedené příklady některých vstupních hodnot, které nemůžete zadat:

  - `*.com`

  - `*.contoso/*`

  - `www.contoso.com/*images`

  - `www.contoso.com/*images*pigs`

  - `www.contoso.com/page*`

  - IP adresy

  - `https://*`

  - `http://*`

  - `http://www.contoso.com:*`

  - `http://www.contoso.com: /*`
  
## <a name="soft-transitions-from-work-to-personal-accounts"></a>Měkké přechody z práce na osobní účty

Základem pro Microsoft Edge Mobile Enterprise je model duální identity, který znamená, že Microsoft Edge podporuje jak pracovní, tak osobní identity. Stejně jako u aplikací Office 365 a Outlook umožňuje tento model Dual-identity koncovým uživatelům používat Microsoft Edge pro všechny potřeby procházení a snadno se pohybovat mezi těmito dvěma prostředími na základě zásad obsahu definovaných správcem. Procházení v osobním kontextu není ovlivněno a firemní informace jsou zcela uloženy do pracovního kontextu v rámci Microsoft Edge. 

Jednou z výhod tohoto modelu je, že když se uživatel pokusí otevřít odkaz (například článek o novince atd.) na webu, který není ve vaší organizaci povolený, může to udělat v osobním kontextu, který je zcela oddělený od jejich pracovního kontextu. Tyto měkké přechody z jsou ve výchozím nastavení povolené. 

Pomocí postupu pro vytvoření konfigurace aplikace Managed Browser nebo Microsoft Edge zadejte následující dvojici klíč-hodnota:

| Klíč                                                                | Hodnota                                                 |
|--------------------------------------------------------------------|-------------------------------------------------------|
| **com. Microsoft. Intune. mam. managedbrowser. AllowTransitionOnBlock** | **False** blokuje výskyt těchto jemných přechodů. |

## <a name="how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios"></a>Jak se dostat k protokolům spravovaných aplikací pomocí Managed Browseru na zařízení s iOSem

Koncoví uživatelé, kteří nainstalují spravovaný prohlížeč na svém zařízení s iOS/iPadOS, můžou zobrazit stav správy všech aplikací publikovaných Microsoftem. Můžou posílat protokoly pro řešení potíží se spravovanými aplikacemi pro iOS/iPadOS.

1. Otevřete **Nastavení**iOS/iPadOS.
2. Vyberte nastavení aplikace **Managed Browser**.
3. Přepněte **Povolit diagnostiku Intune** a nastavte tak prohlížeč do režimu pro řešení problémů.
4. Otevřete **Managed Browser**. Klikněte na **Zobrazit stav aplikace v Intune** a zkontrolujte nastavení zásad pro jednotlivé aplikace.
5. Stiskněte **Začínáme** a **Sdílet protokoly** nebo **Odeslat protokoly do Microsoftu** a pošlete protokoly pro řešení problémů správci IT nebo Microsoftu.

Prohlížeč Managed Browser můžete otevřít v režimu pro řešení problémů také z aplikace.

1. Otevřete Managed Browser.
2. Do pole adresy zadejte `about:intunehelp`.
Prohlížeč Managed Browser spustí režim pro řešení problémů.

Seznam nastavení uložených v aplikačních protokolech najdete v tématu [Kontrola protokolů ochrany aplikace v aplikaci Managed Browser](app-protection-policy-settings-log.md).

## <a name="security-and-privacy-for-the-managed-browser"></a>Zabezpečení a ochrana osobních údajů v aplikaci Managed Browser

- Aplikace Managed Browser nevyužívá nastavení, která uživatelé použijí pro prohlížeče integrované na jejich zařízeních. Aplikace Managed Browser nemá k těmto nastavením přístup.

- Pokud v zásadách ochrany aplikací přidružených k prohlížeči Managed Browser nakonfigurujete možnost **Vyžadovat pro přístup jednoduchý PIN kód** nebo **Vyžadovat pro přístup podnikové přihlašovací údaje** a uživatel klikne na stránce ověřování na odkaz nápovědy, bude moct na internetu přejít na libovolný web, i když bude tento web v zásadách uvedený v seznamu blokovaných webů.

- Aplikace Managed Browser může blokovat přístup k webům jen v případě, že se k nim přistupuje přímo. V případě, že se k webu přistupuje přes zprostředkující služby (třeba překladatelské služby), aplikace přístup neblokuje.

- Kvůli povolení ověřování a přístupu k dokumentaci Intune adresa **&#42;.microsoft.com** v seznamech povolených a blokovaných webů nefiguruje. Je vždycky povolená.

### <a name="turn-off-usage-data"></a>Vypnutí dat o využití
Microsoft automaticky shromažďuje anonymní informace o výkonu a využití aplikace Managed Browser za účelem zlepšení svých produktů a služeb. Uživatelé můžou shromažďování těchto dat na svých zařízeních vypnout pomocí nastavení **Data o využití**. Nad shromažďováním těchto dat nemáte žádnou kontrolu.

- Na zařízeních s iOS/iPadOS se nedají otevřít weby, u kterých vypršela platnost certifikátu nebo které mají nedůvěryhodný certifikát.

## <a name="next-steps"></a>Další kroky

- [Co jsou zásady ochrany aplikací?](app-protection-policy.md) 
