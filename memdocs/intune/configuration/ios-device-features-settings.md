---
title: nastavení funkcí zařízení s iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na všechna nastavení pro konfiguraci zařízení se systémy iOS a iPadOS pro, rozložení domovské obrazovky, oznámení aplikací, sdílená zařízení, jednotné přihlašování a nastavení filtru webového obsahu v Microsoft Intune. Pomocí těchto nastavení v profilu konfigurace zařízení můžete nakonfigurovat zařízení se systémem iOS/iPadOS, aby tyto funkce společnosti Apple používala ve vaší organizaci.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 32d46374186596e8c8721b77510738caadcf78b8
ms.sourcegitcommit: 02635469d684d233fef795d2a15615658e62db10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/16/2020
ms.locfileid: "84814950"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>nastavení zařízení s iOS a iPadOS pro použití běžných funkcí iOS/iPadOS v Intune

Intune obsahuje některá vestavěná nastavení, která uživatelům iOS/iPadOS můžou na svých zařízeních používat jiné funkce společnosti Apple. Můžete například ovládat tiskárny pro víceúčelové tiskárny, přidávat aplikace a složky na stránky Dock a Home screen, zobrazovat oznámení aplikací, zobrazit podrobnosti o značce assetu na zamykací obrazovce, používat ověřování pomocí jednotného přihlašování a používat ověřování certifikátů.

Pomocí těchto funkcí můžete řídit zařízení s iOS/iPadOS jako součást řešení správy mobilních zařízení (MDM).

Tento článek uvádí tato nastavení a popisuje, co jednotlivé nastavení dělá. Další informace o těchto funkcích najdete v [Přidání nastavení funkcí zařízení s iOS/iPadOS nebo MacOS](device-features-configure.md).

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil funkcí zařízení s iOS/iPadOS](device-features-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace s některými nastaveními, která platí pro všechny možnosti registrace. Další informace o různých typech registrace najdete v tématu Registrace zařízení se [systémem iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

> [!NOTE]
> Nezapomeňte přidat všechny tiskárny do stejného profilu. Apple zabrání v zacílení několika profilů pro tisk na stejné zařízení.

- **IP adresa**: zadejte adresu IPv4 nebo IPv6 tiskárny. Pokud k identifikaci tiskáren používáte názvy hostitelů, můžete získat IP adresu tím, že v terminálu otestujete tiskárnu. Další podrobnosti najdete v článku získání IP adresy a cesty (v tomto článku).
- **Cesta**: cesta je typicky `ipp/print` pro tiskárny v síti. Další podrobnosti najdete v článku získání IP adresy a cesty (v tomto článku).
- **Port**: zadejte port naslouchání cíle přenosu. Pokud necháte tuto vlastnost prázdnou, použije se při tisku výchozí port. K dispozici v iOS 11.0 + a iPadOS 13.0 +.
- **TLS**: **Povolte** zabezpečená připojení k tisku pomocí protokolu TLS (Transport Layer Security). K dispozici v iOS 11.0 + a iPadOS 13.0 +.

Pokud chcete přidat servery pro tisk přes mosty, můžete:

- **Přidání** přidá do seznamu přidat server pro příjem. Je možné přidat spoustu tiskových serverů.
- **Importujte** textový soubor s oddělovači (. csv) s těmito informacemi. Případně můžete **exportovat** a vytvořit tak seznam serverů pro tisk do, které jste přidali.

### <a name="get-server-ip-address-resource-path-and-port"></a>Získat IP adresu serveru, cestu prostředku a port

Chcete-li přidat servery s modulem pro tisk, budete potřebovat IP adresu tiskárny, cestu k prostředku a port. Následující kroky ukazují, jak tyto informace získat.

1. Na Macu, který je připojený ke stejné místní síti (podsíti) jako tiskárny pro Protisk, otevřete **terminál** (z **/aplikace/Utility**).
2. V terminálu zadejte `ippfind` a vyberte Enter.

    Poznamenejte si informace o tiskárně. Například může vracet něco podobného jako `ipp://myprinter.local.:631/ipp/port1` . První část je název tiskárny. Poslední část ( `ipp/port1` ) je cesta prostředku.

3. V terminálu zadejte `ping myprinter.local` a vyberte Enter.

   Poznamenejte si IP adresu. Například může vracet něco podobného jako `PING myprinter.local (10.50.25.21)` .

4. Použijte hodnoty IP adresy a prostředku cesty. V tomto příkladu je IP adresa `10.50.25.21` a cesta k prostředku `/ipp/port1` .

## <a name="home-screen-layout"></a>Rozložení domovské obrazovky

Tato funkce platí pro:

- iOS 9,3 nebo novější
- iPadOS 13,0 a novější

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

> [!NOTE]
> Do Docku, stránky nebo složky na stránce přidejte jenom jednu aplikaci. Přidání stejné aplikace na všech místech zabraňuje tomu, aby se aplikace zobrazovala na zařízeních a mohla zobrazovat chyby hlášení.
>
> Například pokud přidáte aplikaci kamera do Docku a stránku, aplikace kamery není zobrazená a hlášení může pro tuto zásadu zobrazovat chybu. Chcete-li přidat aplikaci kamera do rozložení domovské obrazovky, vyberte pouze Dock nebo Page, nikoli obojí.

### <a name="dock"></a>Vyjměte

Pomocí nastavení **Dock** přidejte až šest položek nebo složek do Docku na obrazovce. Mnoho zařízení podporuje méně položek. Například zařízení iPhone podporují až čtyři položky. V takovém případě se na zařízeních zobrazí jenom první čtyři položky, které přidáte.

Pro Dock zařízení můžete přidat až **šest** položek (kombinované aplikace a složky).

- **Přidat**: přidá aplikace nebo složky do Docku na zařízeních.
- **Zadejte**: přidat **aplikaci** nebo **složku**:

  - **Aplikace**: tuto možnost vyberte, pokud chcete přidat aplikace do Dock na obrazovce. Zadejte:

    - **Název aplikace**: zadejte název aplikace. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízení iOS/iPadOS.
    - **ID sady prostředků aplikace**: Zadejte ID sady prostředků aplikace. Některé příklady najdete v tématu [ID sady pro integrované aplikace pro iOS/iPadOS](bundle-ids-built-in-ios-apps.md) .

  - **Složka**: tuto možnost vyberte, pokud chcete přidat složku do Docku na obrazovce.

    Aplikace, které přidáte na stránku ve složce, jsou seřazené zleva doprava a ve stejném pořadí jako seznam. Pokud přidáte více aplikací, než se vejde na stránku, přesunou se aplikace na jinou stránku.

    - **Název složky**: zadejte název složky. Tento název se zobrazuje uživatelům na jejich zařízeních.
    - **Seznam stránek**: **přidejte** stránku a zadejte následující vlastnosti:

      - **Název stránky**: zadejte název stránky. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízení iOS/iPadOS.
      - **Název aplikace**: zadejte název aplikace. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízení iOS/iPadOS.
      - **ID sady prostředků aplikace**: Zadejte ID sady prostředků aplikace. Některé příklady najdete v tématu [ID sady pro integrované aplikace pro iOS/iPadOS](bundle-ids-built-in-ios-apps.md) .

      Pro Dock zařízení můžete přidat až **20** stránek.

> [!NOTE]
> Když použijete nastavení rozložení domovské obrazovky a přidáte stránky nebo do Docku přidáte stránky a aplikace, ikony na domovské obrazovce a stránkách jsou zamčené. Nelze je přesunout ani odstranit. Toto chování může být záměrné pomocí zásad pro iOS/iPadOS a Apple MDM.

#### <a name="example"></a>Příklad

V následujícím příkladu zobrazuje Dock obrazovka aplikace Safari, pošty a akcií. Aplikace Pošta je vybrána k zobrazení vlastností:

> [!div class="mx-imgBorder"]
> ![Ukázka nastavení Dock obrazovky pro iOS/iPadOS v Intune](./media/ios-device-features-settings/dock-screen-mail-app.png)

Když přiřadíte zásady k iPhonu, bude Dock vypadat podobně jako na následujícím obrázku:

> [!div class="mx-imgBorder"]
> ![Ukázka rozložení zařízení s iOS/iPadOS Dock na iPhonu](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Stránky

Přidejte stránky, které chcete zobrazit na domovské obrazovce, a aplikace, které chcete zobrazit na jednotlivých stránkách. Aplikace, které přidáte na stránku, jsou seřazené zleva doprava ve stejném pořadí jako seznam. Pokud přidáte více aplikací, než se vejde na stránku, přesunou se aplikace na jinou stránku.

> [!TIP]
> Chcete-li změnit pořadí položek v seznamech na domovské obrazovce a na stránkách, můžete je přetáhnout.

Na zařízení můžete přidat až **40** stránek.

- **Seznam stránek**: **přidejte** stránku a zadejte následující vlastnosti:

  - **Název stránky**: zadejte název stránky. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manageru a *není* zobrazený na zařízení se systémem iOS/iPadOS.

  Do zařízení můžete přidat až **60** položek (sloučené aplikace a složky).

  - **Přidat**: přidá aplikace nebo složky na stránku na zařízeních.

    - **Zadejte**: přidat **aplikaci** nebo **složku**:

      - **Aplikace**: tuto možnost vyberte, pokud chcete přidat aplikace na stránku na obrazovce. Dále zadejte:

        - **Název aplikace**: zadejte název aplikace. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízení iOS/iPadOS.
        - **ID sady prostředků aplikace**: Zadejte ID sady prostředků aplikace. Některé příklady najdete v tématu [ID sady pro integrované aplikace pro iOS/iPadOS](bundle-ids-built-in-ios-apps.md) .

      - **Složka**: tuto možnost vyberte, pokud chcete přidat složku do Docku na obrazovce.

        Aplikace, které přidáte na stránku ve složce, jsou seřazené zleva doprava a ve stejném pořadí jako seznam. Pokud přidáte více aplikací, než se vejde na stránku, přesunou se aplikace na jinou stránku.

        - **Název složky**: zadejte název složky. Tento název se zobrazí uživatelům na zařízeních.
        - **Přidat**: přidá stránky do složky. Zadejte také následující vlastnosti:

          - **Název stránky**: zadejte název stránky. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízení iOS/iPadOS.
          - **Název aplikace**: zadejte název aplikace. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízení iOS/iPadOS.
          - **ID sady prostředků aplikace**: Zadejte ID sady prostředků aplikace. Některé příklady najdete v tématu [ID sady pro integrované aplikace pro iOS/iPadOS](bundle-ids-built-in-ios-apps.md) .

#### <a name="example"></a>Příklad

V následujícím příkladu je přidána nová stránka s názvem **Contoso** . Na stránce se zobrazí aplikace najít přátele a nastavení:

> [!div class="mx-imgBorder"]
> ![rozložení domovské obrazovky pro iOS/iPadOS – nové nastavení stránky a příklad v Intune](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

Vybraná aplikace nastavení zobrazuje vlastnosti:

> [!div class="mx-imgBorder"]
> ![Nastavení rozložení domovské obrazovky pro iOS/iPadOS příklad vlastností aplikace v Intune](./media/ios-device-features-settings/page-settings-app-properties.png)

Když přiřadíte zásady k iPhonu, stránka bude vypadat podobně jako na následujícím obrázku:

> [!div class="mx-imgBorder"]
> ![zařízení s iOS/iPadOS s upravenou domovskou obrazovkou v Intune](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>App notifications

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Přidat**: Přidat oznámení pro aplikace:

  > [!div class="mx-imgBorder"]
  > ![Přidání oznámení aplikace v profilu iOS/iPadOS v Intune](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - **ID sady prostředků aplikace**: zadejte **ID sady prostředků** aplikace, kterou chcete přidat. Některé příklady najdete v tématu [ID sady pro integrované aplikace pro iOS/iPadOS](bundle-ids-built-in-ios-apps.md) .
  - **Název aplikace**: zadejte název aplikace, kterou chcete přidat. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízeních.
  - **Vydavatel**: zadejte vydavatele aplikace, kterou přidáváte. Tento název se používá pro váš odkaz v centru pro správu Microsoft Endpoint Manager. Nezobrazuje *se* na zařízeních.
  - **Oznámení**: **povolí** nebo **zakáže** aplikaci odesílat oznámení do zařízení.
    - **Zobrazit v centru oznámení**: **Povolit** aplikaci umožní zobrazovat oznámení v centru oznámení zařízení. **Disable** zabrání aplikaci v zobrazování oznámení v centru oznámení.
    - **Zobrazit na zamykací obrazovce**: **Povolit** zobrazí na zamykací obrazovce zařízení oznámení aplikací. **Disable** zabrání aplikaci zobrazovat oznámení na zamykací obrazovce.
    - **Typ výstrahy**: po odemčení zařízení vyberte, jak se má oznámení zobrazovat. Možnosti:
      - **Žádné**: nezobrazuje se žádné oznámení.
      - **Banner**: krátce se zobrazí zpráva s oznámením.
      - **Modální**: zobrazuje se oznámení a uživatelé je musí před pokračováním v používání zařízení zavřít ručně.
    - Ikona příznaku **u aplikace**: výběrem **Povolit** přidejte do ikony aplikace badge. BADGE znamená, že aplikace odeslala oznámení.
    - **Zvuky**: výběrem **Povolit zapnete** zvuk, když se doručí oznámení.

## <a name="lock-screen-message"></a>Zpráva zamykací obrazovky

Tato funkce platí pro:

- iOS 9.3 nebo novější
- iPadOS 13,0 a novější

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- Informace o inventárním **štítku**: zadejte informace o inventárním štítku zařízení. Zadejte například `Owned by Contoso Corp` nebo `Serial Number: {{serialnumber}}`.

  Text, který zadáte, se zobrazí v okně přihlášení a zamykací obrazovka na zařízeních.

- **Poznámka pod čarou na zamykací obrazovce**: Pokud dojde ke ztrátě nebo odcizení zařízení, zadejte poznámku, která může přispět k vrácení zařízení zpět. Můžete zadat libovolný text, který chcete. Zadejte třeba `If found, call Contoso at ...`.

  Tokeny zařízení lze také použít k přidání informací o jednotlivých zařízeních do těchto polí. Chcete-li například zobrazit sériové číslo, zadejte `Serial Number: {{serialnumber}}` nebo `Device ID: {{DEVICEID}}` . Na zamykací obrazovce se text zobrazí jako podobný `Serial Number 123456789ABC` . Při zadávání proměnných nezapomeňte použít složené závorky `{{ }}` . [Tokeny konfigurace aplikace](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) obsahují seznam proměnných, které se dají použít. Můžete také použít `DEVICENAME` nebo libovolná jiná hodnota specifická pro zařízení.

  > [!NOTE]
  > Proměnné nejsou v uživatelském rozhraní ověřeny a rozlišují se velká a malá písmena. V důsledku toho mohou být profily uloženy s nesprávným vstupem. Pokud například zadáte `{{DeviceID}}` místo `{{deviceid}}` nebo {{DEVICEID}}, pak se místo jedinečného ID zařízení zobrazí literální řetězec. Nezapomeňte zadat správné informace. Podporují se všechna malá a velká písmena, ale ne kombinace. 

## <a name="single-sign-on"></a>Jednotné přihlašování

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Sféra**: zadejte část domény adresy URL. Zadejte například `contoso.com`.
- **Hlavní název protokolu Kerberos**: Intune vyhledá tento atribut pro každého uživatele ve službě Azure AD. Intune pak před generováním XML, který se nainstaluje na zařízení, naplní příslušné pole (například hlavní název uživatele (UPN)). Možnosti:

  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení bude operační systém při nasazení profilu do zařízení vyzvat uživatele k zadání hlavního názvu protokolu Kerberos. Pro MDMs pro instalaci profilů jednotného přihlašování je vyžadován hlavní název.
  - **Hlavní název uživatele**: hlavní název uživatele (UPN) se analyzuje následujícím způsobem:

    > [!div class="mx-imgBorder"]
    > ![iOS/iPadOS – atribut jednotného přihlašování pro uživatele v Intune](./media/ios-device-features-settings/User-name-attribute.png)

    Sféru také můžete přepsat textem, který zadáte do textového pole **Sféra**.

    Například contoso má několik oblastí, včetně Evropy, Asie a Severní Amerika. Společnost Contoso chce, aby uživatelé v Asii používali jednotné přihlašování a aplikace vyžaduje hlavní název uživatele (UPN) ve `username@asia.contoso.com` formátu. Když vyberete **hlavní název uživatele**, vyřadí se sféra pro každého uživatele ze služby Azure AD, která je `contoso.com` . Takže pro uživatele v Asii vyberte **hlavní název uživatele**a zadejte `asia.contoso.com` . Hlavní název uživatele (UPN) se `username@asia.contoso.com` místo `username@contoso.com` .

  - **ID zařízení v Intune**: Intune automaticky vybere ID zařízení v Intune.

    Ve výchozím nastavení aplikace používají ID zařízení. Ale pokud vaše aplikace používá ID zařízení a sféru, můžete ji zadat do textového pole **Sféra**.

    > [!NOTE]
    > Implicitně platí, že pokud používáte ID zařízení, sféru nevyplňujte.

  - **ID zařízení Azure AD**
  - **Název účtu SAM**: Intune naplní místní název účtu správce zabezpečení účtů (SAM).


- **Aplikace**: **přidejte** aplikace na zařízení uživatelů, která můžou používat jednotné přihlašování.

  `AppIdentifierMatches`Pole musí zahrnovat řetězce, které odpovídají ID sady prostředků aplikace. Tyto řetězce můžou být přesné shody, jako `com.contoso.myapp` je, nebo zadejte shodu předpony u ID sady prostředků pomocí \* zástupného znaku. Zástupný znak musí být uveden za znakem tečky (.) a může se objevit pouze jednou, na konci řetězce, například `com.contoso.*` . Při použití zástupného znaku se udělí přístup k účtu všem aplikacím, jejichž ID sady prostředků začíná příslušnou předponou.

  **Název aplikace** použijte k zadání popisného názvu, který pomůže při identifikaci ID sady prostředků.

- **Předpony adresy URL**: **přidejte** všechny adresy URL ve vaší organizaci, které vyžadují ověřování s jednotným přihlašováním uživatele.

  Když se například uživatel připojí k některé z těchto webů, zařízení s iOS/iPadOS používá přihlašovací údaje jednotného přihlašování. Uživatelé nemusejí zadávat žádné další přihlašovací údaje. Je-li povoleno ověřování Multi-Factor Authentication, je nutné, aby uživatel zadal druhé ověření.

  > [!NOTE]
  > V těchto adresách URL se musí používat správně naformátovaný plně kvalifikovaný název domény. Apple vyžaduje, aby byly ve `http://<yourURL.domain>` formátu.

  Odpovídající vzory adres URL musí mít na začátku `http://` nebo `https://`. Je spuštěna jednoduchá řetězcová shoda, takže se `http://www.contoso.com/` předpona adresy URL neshoduje `http://www.contoso.com:80/` . U iOS 10.0 + a iPadOS 13.0 + se dá použít jeden zástupný znak \* k zadání všech vyhovujících hodnot. Například `http://*.contoso.com/` odpovídá `http://store.contoso.com/` a `http://www.contoso.com` .

  `http://.com`Vzory a `https://.com` odpovídají všem adresám URL protokolu HTTP a HTTPS, v uvedeném pořadí.

- **Certifikát obnovení**: Pokud používáte certifikáty pro ověřování (nikoli hesla), vyberte jako ověřovací certifikát existující certifikát SCEP nebo PFX. Obvykle se jedná o stejný certifikát, který je nasazený pro uživatele pro jiné profily, jako je VPN, Wi-Fi nebo e-mail.

## <a name="web-content-filter"></a>Filtr webového obsahu

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Typ filtru**: tuto možnost vyberte, pokud chcete určit konkrétní weby. Možnosti:

  - **Konfigurace adres URL**: použijte integrovaný webový filtr společnosti Apple, který hledá výrazy pro dospělé, včetně vulgárních výrazů a sexuálního explicitního jazyka. Tato funkce vyhodnocuje každou webovou stránku jako načtenou a identifikuje a blokuje nevhodný obsah. Můžete také přidat adresy URL, které nechcete zkontrolovat pomocí filtru. Nebo zablokujte konkrétní adresy URL bez ohledu na nastavení filtru Apple.

    - **Povolené adresy URL**: **přidejte** adresy URL, které chcete povolit. Tyto adresy URL obcházejí webový filtr společnosti Apple.

        > [!NOTE]
        > Adresy URL, které zadáte, jsou adresy URL, které nechcete evauluated webovým filtrem Apple. Tyto adresy URL nejsou seznamem povolených webů. Chcete-li vytvořit seznam povolených webů, nastavte **typ filtru** **pouze na konkrétní weby**.

    - **Blokované adresy URL**: **přidejte** adresy URL, které chcete ukončit otevírání bez ohledu na nastavení webového filtru Apple.

  - **Jenom konkrétní weby** (jenom pro webový prohlížeč Safari): tyto adresy URL se přidají do záložek prohlížeče Safari. Uživatelé můžou navštěvovat **jenom** tyto weby. žádné jiné weby nelze otevřít. Tuto možnost použijte jenom v případě, že znáte přesný seznam adres URL, ke kterým mají uživatelé přístup.

    - **Adresa URL**: zadejte adresu URL webu, který chcete udělit. Zadejte například `https://www.contoso.com`.
    - **Cesta záložky**: Apple toto nastavení změnil. Všechny záložky přecházejí do složky **schválené weby** . Záložky nejdou do cesty záložky, kterou zadáte.
    - **Title**: zadejte popisný název záložky.

    Pokud nezadáte žádné adresy URL, uživatelé nebudou mít přístup k žádným webům s výjimkou `microsoft.com` , `microsoft.net` a `apple.com` . Tyto adresy URL jsou automaticky povolené službou Intune.

## <a name="single-sign-on-app-extension"></a>Rozšíření aplikace s jednotným přihlašováním

Tato funkce platí pro:

- iOS 13,0 a novější
- iPadOS 13,0 a novější

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Typ rozšíření aplikace jednotného přihlašování**: Vyberte typ rozšíření aplikace jednotného přihlašování. Možnosti:

  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení operační systém nebude používat rozšíření aplikací. Pokud chcete zakázat rozšíření aplikace, můžete změnit typ rozšíření aplikace jednotného přihlašování na **Nenakonfigurováno**.
  - **Microsoft Azure AD**: používá modul plug-in Microsoft Enterprise SSO, což je rozšíření aplikace jednotného přihlašování typu přesměrování. Tento modul plug-in poskytuje jednotné přihlašování pro účty služby Active Directory ve všech aplikacích, které podporují funkci [podnikového jednotného přihlašování od společnosti Apple](https://developer.apple.com/documentation/authenticationservices) . Tento typ rozšíření aplikace jednotného přihlašování použijte k povolení jednotného přihlašování v aplikacích Microsoftu, organizačních aplikacích a websites, které se ověřují pomocí Azure AD.

    Modul plug-in jednotného přihlašování funguje jako zprostředkovatel pokročilého ověřování, který nabízí vylepšení zabezpečení a uživatelského prostředí. Všechny aplikace, které dřív používaly zprostředkované ověřování pomocí aplikace Microsoft Authenticator, budou i nadále získávat jednotné přihlašování s [modulem plug-in Microsoft Enterprise SSO pro zařízení Apple](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin).

    > [!IMPORTANT]
    > K zajištění jednotného přihlašování s typem rozšíření aplikace Microsoft Azure AD jednotného přihlašování, nejdřív na zařízení nainstalujte Microsoft Authenticator aplikace pro iOS/iPadOS. Aplikace ověřovatele doručí do zařízení modul plug-in Microsoft Enterprise SSO a nastavení rozšíření aplikace pro jednotné přihlašování aktivuje modul plug-in. Po nainstalování ověřovacích dat a profilu rozšíření aplikace jednotného přihlašování do zařízení musí uživatelé zadat své přihlašovací údaje pro přihlášení a navázat relaci na jejich zařízeních. Tato relace se pak použije v různých aplikacích, aniž by se museli uživatelé znovu ověřovat. Další informace o ověřovateli najdete v tématu [co je Microsoft Authenticator aplikace](https://docs.microsoft.com/azure/active-directory/user-help/user-help-auth-app-overview).

  - **Přesměrování**: k použití jednotného přihlašování s moderními toky ověřování použijte obecné a přizpůsobitelné rozšíření aplikace pro přesměrování. Ujistěte se, že znáte ID rozšíření pro rozšíření aplikace vaší organizace.
  - **Přihlašovací údaje**: pomocí obecného rozšíření aplikace s přizpůsobitelnou přihlašovacími údaji můžete používat jednotné přihlašování s toky ověřování typu Challenge a Response. Ujistěte se, že znáte ID rozšíření pro rozšíření aplikace vaší organizace.
  - **Kerberos**: použijte integrované rozšíření protokolu Kerberos společnosti Apple, které je součástí iOS 13.0 + a iPadOS 13.0 +. Tato možnost je verze rozšíření **přihlašovacích údajů** specifická pro Kerberos.

  > [!TIP]
  > Pomocí typů **přesměrování** a **přihlašovacích údajů** přidáte vlastní hodnoty konfigurace, které budou předávány prostřednictvím rozšíření. Pokud používáte **přihlašovací údaje**, zvažte použití integrovaného nastavení konfigurace poskytovaného společností Apple v typu **Kerberos** .

- **Režim sdíleného zařízení** (jenom Microsoft Azure AD): Pokud nasazujete modul plug-in Microsoft Enterprise SSO do zařízení s iOS/iPadOS nakonfigurovaných pro funkci režimu sdíleného zařízení Azure AD, vyberte **Povolit** . Zařízení ve sdíleném režimu umožňují mnoha uživatelům globálně přihlašovat se k aplikacím, které podporují režim sdíleného zařízení. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení nejsou zařízení s iOS/iPadOS určená ke sdílení mezi více uživateli.

  Další informace o režimu sdíleného zařízení a jeho povolení najdete v tématu Přehled režimu [sdíleného zařízení](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices) a [sdíleného zařízení pro zařízení s iOS](https://docs.microsoft.com/azure/active-directory/develop/msal-ios-shared-devices).  

  Tato funkce platí pro:
  
  - iOS/iPadOS 13,5 a novější

- **ID rozšíření** (přesměrování a přihlašovací údaje): zadejte identifikátor sady prostředků, který identifikuje vaše rozšíření aplikace jednotného přihlašování, například `com.apple.extensiblesso` .

- **ID týmu** (přesměrování a přihlašovací údaje): zadejte identifikátor týmu rozšíření aplikace jednotného přihlašování. Identifikátor týmu je alfanumerický řetězec (čísla a písmena), který vygenerovala společnost Apple, jako je například `ABCDE12345` . ID týmu se nevyžaduje.

  [Najděte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře se webová stránka společnosti Apple), kde najdete další informace.

- **Sféra** (přihlašovací údaje a Kerberos): zadejte název sféry ověřování. Název sféry by měl být velkými písmeny, například `CONTOSO.COM` . Název vaší sféry je typicky stejný jako název vaší domény DNS, ale jenom na velká písmena.

- **Domény** (přihlašovací údaje a Kerberos): zadejte doménu nebo názvy hostitelů pro weby, které se dají ověřit pomocí jednotného přihlašování. Například pokud je váš web `mysite.contoso.com` , pak `mysite` je název hostitele a `contoso.com` je název domény. Když se uživatelé připojí k některé z těchto webů, aplikace App Extension zpracuje výzvu ověřování. Toto ověřování umožňuje uživatelům k přihlášení použít ID obličeje, dotykové ID nebo Apple PINCODE/přístupový kód.

  - Všechny domény v profilech služby Intune, které mají rozšíření pro aplikace jednotného přihlašování, musí být jedinečné. Doménu nemůžete opakovat v žádném profilu rozšíření aplikace pro přihlášení, i když používáte různé typy rozšíření aplikace jednotného přihlašování.
  - U těchto domén se nerozlišují velká a malá písmena.

- **Adresy URL** (pouze přesměrované): zadejte PŘEDPONY adresy URL vašich zprostředkovatelů identity, na jejichž základě rozšíření pro přesměrování aplikace používá jednotné přihlašování. Když budou uživatelé přesměrováni na tyto adresy URL, rozšíření aplikace jednotného přihlašování se zasáhne a zobrazí výzvu k přihlášení SSO.

  - Všechny adresy URL v profilech rozšíření aplikace jednotného přihlašování Intune musí být jedinečné. Doménu nejde opakovat v žádném profilu rozšíření aplikace jednotného přihlašování, a to ani v případě, že používáte různé typy rozšíření aplikace jednotného přihlašování.
  - Adresy URL musí začínat na `http://` nebo `https://` .

- **Další konfigurace** (Microsoft Azure AD, přesměrování a přihlašovací údaje): zadejte další data specifická pro rozšíření, která chcete předat rozšíření aplikace jednotného přihlašování:
  - **Klíč**: zadejte název položky, kterou chcete přidat, například `user name` .
  - **Typ**: zadejte typ dat. Možnosti:

    - Řetězec
    - Boolean: v **konfigurační hodnotě**zadejte `True` nebo `False` .
    - Integer: v **hodnotě konfigurace**zadejte číslo.

  - **Hodnota**: zadejte data.

  - **Přidat**: vyberte, pokud chcete přidat konfigurační klíče.

- **Použití řetězce klíčů** (jenom Kerberos): **blok** zabraňuje ukládání a ukládání hesel do řetězce klíčů. Pokud je blokováno, uživatelé nebudou vyzváni k uložení hesla a po vypršení platnosti lístku protokolu Kerberos je nutné znovu zadat heslo. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém ukládat hesla a uložit je do řetězce klíčů. Uživatelům se po vypršení platnosti lístku nezobrazí výzva k zadání hesla.
- **ID obličeje, dotykové ID nebo heslo** (jenom Kerberos): **vyžaduje** , aby uživatelé při aktualizaci lístku Kerberos zadali své ID a dotykové jméno a heslo zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat, aby uživatelé pomocí biometrika nebo hesla zařízení aktualizovali lístek protokolu Kerberos. Pokud je **použití řetězce klíčů** blokované, pak toto nastavení neplatí.
- **Výchozí sféra** (pouze Kerberos): **Enable** nastaví hodnotu **sféry** , kterou jste zadali jako výchozí sféru. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí nastavit výchozí sféru.

  > [!TIP]
  > - Toto nastavení **Povolte** , pokud konfigurujete více rozšíření aplikace pro jednotné přihlašování pomocí protokolu Kerberos ve vaší organizaci.
  > - Toto nastavení **Povolte** , pokud používáte více sfér. Nastaví hodnotu **sféry** , kterou jste zadali jako výchozí sféru.
  > - Pokud máte pouze jednu sféru, ponechte ji **nenakonfigurovanou** (výchozí).

- **Hlavní název** (jenom Kerberos): zadejte uživatelské jméno objektu zabezpečení protokolu Kerberos. Nemusíte zahrnovat název sféry. Například v `user@contoso.com` , `user` je hlavní název a `contoso.com` je název sféry.

  > [!TIP]
  > - Můžete také použít proměnné v hlavním názvu tak, že zadáte složené závorky `{{ }}` . Pokud například chcete zobrazit uživatelské jméno, zadejte `Username: {{username}}` . 
  > - Buďte ale opatrní s náhradou proměnných, protože proměnné nejsou v uživatelském rozhraní ověřené a rozlišují velká a malá písmena. Nezapomeňte zadat správné informace.

- **Kód lokality služby Active Directory** (pouze Kerberos): zadejte název lokality služby Active Directory, kterou má rozšíření protokolu Kerberos použít. Tuto hodnotu pravděpodobně nebudete muset měnit, protože rozšíření protokolu Kerberos může automaticky najít kód lokality služby Active Directory.
- **Název mezipaměti** (jenom Kerberos): zadejte název obecné služby zabezpečení (GSS) mezipaměti protokolu Kerberos. Tuto hodnotu pravděpodobně nemusíte nastavovat.
- **ID sady prostředků aplikace** (jenom Kerberos): **přidejte** identifikátory sady prostředků aplikace, které by měly na svých zařízeních používat jednotné přihlašování. Těmto aplikacím je udělen přístup k lístku pro udělení lístku protokolu Kerberos, ověřovacímu lístku a ověřování uživatelů pro služby, kterým mají oprávnění k přístupu.
- **Mapování sféry domény** (jenom Kerberos): **přidejte** přípony DNS domény, které by se měly namapovat do vaší sféry. Toto nastavení použijte, pokud názvy DNS hostitelů neodpovídají názvu sféry. Pravděpodobně nemusíte vytvářet vlastní mapování domén na sféru.
- **PKINIT certifikát** (jenom Kerberos): **Vyberte** certifikát kryptografie s veřejným klíčem pro počáteční ověřování (PKINIT), který se dá použít pro ověřování protokolem Kerberos. Můžete si vybrat z certifikátů [PKCS](../protect/certficates-pfx-configure.md) nebo [SCEP](../protect/certificates-scep-configure.md) , které jste přidali v Intune. Další informace o certifikátech najdete v tématu [použití certifikátů k ověřování v Microsoft Intune](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Tapeta

Pokud se zařízením s existující imagí nepřiřazuje profil bez obrázku, může docházet k neočekávanému chování. Můžete například vytvořit profil bez obrázku. Tento profil je přiřazen k zařízením, která již mají bitovou kopii. V tomto scénáři se image může změnit na výchozí nastavení zařízení, jinak se v zařízení může zachovat původní image. Toto chování se řídí a je omezené platformou MDM od společnosti Apple.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Umístění zobrazení tapety**: vyberte umístění na zařízeních k zobrazení obrázku. Možnosti:
  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Vlastní image se do zařízení nepřidá. Ve výchozím nastavení může operační systém nastavit vlastní obrázek.
  - **Zamykací obrazovka**: Přidá obrázek na zamykací obrazovku.
  - **Domovská obrazovka**: Přidá obrázek na domovskou obrazovku.
  - **Zamykací obrazovka a Domovská obrazovka**: používá stejnou bitovou kopii na zamykací obrazovce a na domovské obrazovce.
- **Obrázek tapety**: nahrajte existující obrázek. png,. jpg nebo. jpeg, který chcete použít. Ujistěte se, že velikost souboru je menší než 750 KB. Můžete také **Odebrat** obrázek, který jste přidali.

> [!TIP]
> Chcete-li zobrazit různé obrázky na zamykací obrazovce a na domovské obrazovce, vytvořte profil s obrázkem zamykací obrazovky. Vytvořte jiný profil s obrázkem na domovské obrazovce. Přiřaďte oba profily ke skupinám uživatelů a zařízení s iOS/iPadOS.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily funkcí zařízení pro zařízení [MacOS](macos-device-features-settings.md) .
