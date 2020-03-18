---
title: nastavení zařízení s iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních s iOS/iPadOS k omezení funkcí, včetně nastavení požadavků na heslo, řízení uzamčené obrazovky, používání integrovaných aplikací, přidávání omezených nebo schválených aplikací, zpracování zařízení Bluetooth, připojení ke cloudu pro zálohování a ukládání, povolení celoobrazovkového režimu, přidání domén a řízení způsobu interakce uživatelů s webovým prohlížečem Safari v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 951982f862bc4ba742d87af67f198d3c5114c546
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332323"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>nastavení zařízení s iOS a iPadOS pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popisuje různá nastavení, která můžete řídit na zařízeních s iOS a iPadOS. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, nastavit pravidla pro hesla, povolit nebo omezit konkrétní aplikace a další.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí na vaše zařízení s iOS/iPadOS.

> [!TIP]
> Tato nastavení používají nastavení MDM od společnosti Apple. Další informace o těchto nastaveních najdete v tématu [Nastavení správy mobilních zařízení společnosti Apple](https://support.apple.com/guide/mdm/welcome/web) (otevření webu společnosti Apple).

## <a name="before-you-begin"></a>Před zahájením

[Vytvoří konfigurační profil omezení zařízení](device-restrictions-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace s některými nastaveními, která platí pro všechny možnosti registrace. Další informace o různých typech registrace najdete v tématu Registrace zařízení se [systémem iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="general"></a>Obecné

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Sdílet data o využití**: vyberte možnost **blokovat** , pokud chcete zabránit tomu, aby zařízení odesílalo data o diagnostice a využití do Applu. **Nenakonfigurováno** (výchozí) umožňuje odesílat tato data.

- **Snímek obrazovky**: vyberte možnost **blokovat** , pokud chcete zabránit snímekům obrazovky nebo snímku obrazovky na zařízení. V systému iOS/iPadOS 9,0 a novějších blokují také nahrávky obrazovky. **Nenakonfigurováno** (výchozí) umožňuje uživateli zachytit obsah obrazovky jako obrázek nebo jako video.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Nedůvěryhodné certifikáty TLS**: vyberte **blok** , aby se zabránilo nedůvěryhodným certifikátům TLS (Transport Layer Security) na zařízení. **Nenakonfigurováno** (výchozí) POVOLÍ certifikáty TLS.
- **Zablokovat vysoce Air aktualizace PKI**: **blok** znemožní uživatelům přijímat aktualizace softwaru, pokud není zařízení připojené k počítači. **Nenakonfigurováno** (výchozí): umožňuje zařízení přijímat aktualizace softwaru bez připojení k počítači.
- **Omezení sledování služby AD**: volbou možnosti **omezit** zakažte identifikátor inzerce zařízení. **Není nakonfigurováno** (výchozí) udržuje povoleno.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Úprava nastavení odeslání diagnostiky**: **blok** znemožní uživateli měnit nastavení odesílání diagnostiky a analýzy aplikací v části **Diagnostika a použití** (nastavení zařízení). **Nenakonfigurováno** (výchozí) umožňuje uživateli změnit tato nastavení zařízení.

  Chcete-li použít toto nastavení, nastavte nastavení **sdílet data o využití** pro **blokování**.

  Tato funkce platí pro:  
  - iOS 9.3.2 a novější
  - iPadOS 13,0 a novější

- **Sledování vzdálené obrazovky podle aplikace učebny**: zvolit **blok** , aby aplikace učebny zabránila vzdálenému zobrazení obrazovky na zařízení. **Nenakonfigurováno** (výchozí) umožňuje aplikaci Apple učeben zobrazit obrazovku.

  Chcete-li použít toto nastavení, nastavte nastavení **zachycení obrazovky** na **blokovat**.

  Tato funkce platí pro:  
  - iOS 9,3 a novější
  - iPadOS 13,0 a novější

- **Aplikace učebny s upozorněním na obrazovku**: Pokud je tato možnost **povolená**, můžou učitelé tiše sledovat obrazovku zařízení s iOS a iPadOS pomocí aplikace učebny bez vědomí vašich studentů. Studentská zařízení zaregistrovaná ve třídě pomocí aplikace učebny automaticky poskytnou oprávnění učiteli tohoto kurzu. **Nenakonfigurováno** (výchozí) zabrání této funkci.

  Chcete-li použít toto nastavení, nastavte nastavení **zachycení obrazovky** na **blokovat**.

- **Důvěryhodnost podnikových aplikací**: vyberte **blok** pro odebrání veřejného tlačítka **Enterprise Developer** v nastavení > obecných profilů > & správu zařízení na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživateli zvolit důvěřování aplikacím, které se nestahují z App Storu.
- **Změna účtu**: když se nastaví **blok**, uživatel nebude moct aktualizovat nastavení specifická pro zařízení v aplikaci nastavení pro iOS/iPadOS. Uživatel například nemůže vytvořit nové účty zařízení nebo změnit uživatelské jméno nebo heslo. **Nenakonfigurováno** (výchozí) umožňuje uživatelům změnit tato nastavení.

  Tato funkce se vztahuje také na nastavení přístupná z aplikace nastavení pro iOS/iPadOS, jako je pošta, kontakty, kalendář, Twitter a další. Tato funkce se nevztahuje na aplikace s nastaveními účtu, která se nedají konfigurovat z aplikace nastavení pro iOS/iPadOS, jako je například aplikace Microsoft Outlook.

- **Čas obrazovky**: vyberte možnost **blokovat** , pokud chcete uživatelům zabránit v nastavení vlastních omezení na obrazovce čas (nastavení zařízení). **Není nakonfigurováno** umožňuje uživateli nakonfigurovat na zařízení omezení zařízení (například Rodičovská kontrola nebo obsah a omezení ochrany osobních údajů).

  Toto nastavení bylo přejmenováno z **možnosti Povolit omezení v nastavení zařízení**. Dopad této změny:  
  
  - iOS 11.4.1 a starší: **blok** brání koncovým uživatelům v nastavení vlastních omezení v nastavení zařízení. Chování je stejné. a pro koncové uživatele nejsou žádné změny.
  - iOS 12,0 a novější: **blok** znemožní koncovým uživatelům nastavit vlastní **čas na obrazovku** v nastavení zařízení (nastavení > Obecné > čas obrazovky), včetně omezení obsahu a ochrany osobních údajů. V zařízeních upgradovaných na iOS 12,0 se už v nastavení zařízení nezobrazí karta omezení (Nastavení > Obecné > Správa zařízení > > omezení profilu správy. Tato nastavení se nacházejí v **čase obrazovky**.
  
- **Použití možnosti pro vymazání veškerého obsahu a nastavení na zařízení**: vyberte **blokovat** , aby uživatelé nemohli na zařízení používat možnost pro vymazání veškerého obsahu a nastavení. **Není nakonfigurováno** (výchozí) poskytuje uživatelům přístup k těmto nastavením.
- **Úprava názvu zařízení**: vyberte **blokovat** , aby se název zařízení nemohlo změnit. **Nenakonfigurováno** (výchozí) umožňuje uživateli změnit název zařízení.
- **Úprava nastavení oznámení**: vyberte **blok** , aby se nastavení oznámení nedaly změnit. **Nenakonfigurováno** (výchozí) umožňuje uživateli změnit nastavení oznámení o zařízení.
- **Úprava tapety**: **blok** brání v změně tapety. **Nenakonfigurováno** (výchozí) umožňuje uživateli změnit tapetu v zařízení.
- **Změny nastavení vztahu důvěryhodnosti pro podnikovou aplikaci**: **blok** znemožní uživateli měnit nastavení vztahu důvěryhodnosti podnikových aplikací na zařízeních pod dohledem. **Nenakonfigurováno** (výchozí) umožňuje uživateli důvěřovat aplikacím, které se nestahují z App Storu.
- **Změny profilu konfigurace**: **blok** zabraňuje změnám konfiguračního profilu na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživateli instalovat konfigurační profily.
- **Zámek aktivace**: vyberte **povolit** pro povolení zámek aktivace na zařízeních s iOS/iPadOS, která jsou pod dohledem. Zámek aktivace znemožňuje opětovné aktivaci ztraceného nebo odcizeného zařízení.
- **Blokovat odebrání aplikace**: vyberte možnost **blokovat** , pokud chcete uživatelům zabránit v odebírání aplikací. **Nenakonfigurováno** (výchozí) umožňuje uživatelům odebírat aplikace ze zařízení.
- **Povolí příslušenství USB, když je zařízení zamknuté**: **umožňuje dovolit** , aby data Exchange příslušenství využívala zařízení, které je po celou hodinu uzamčené. **Nenakonfigurováno** (výchozí) neaktualizuje režim omezeného portu USB na zařízení a příslušenství USB bude zablokováno v přenosu dat ze zařízení, pokud je po celou hodinu uzamčené.
- **Vynutit automatické datum a čas**: **vyžaduje** , aby zařízení pod dohledem, aby automaticky nastavila datum &ho času. Časové pásmo zařízení se aktualizuje, když má zařízení mobilní připojení nebo má Wi-Fi s povolenými službami zjišťování polohy.
- **Vyžadovat, aby studenti požádali o oprávnění k opuštění kurzu učebnosti**: **vyžadovat** , aby studenti zaregistrovaní v nespravovaném kurzu pomocí aplikace učeben požádali o oprávnění od učitelů k opuštění tohoto kurzu. **Nenakonfigurováno** (výchozí) nenutí studenta požádat o oprávnění.

  Tato funkce platí pro:  
  - iOS 11,3 a novější
  - iPadOS 13,0 a novější

- **Povolit učebně zamknout aplikaci a uzamknout zařízení bez zobrazení výzvy**: **Povolit** umožní učitelům uzamknout aplikace nebo zamknout zařízení pomocí aplikace učeben bez vyzvání studenta. Uzamykání aplikací znamená, že zařízení může přistupovat jenom k aplikacím určeném pro učitele. **Nenakonfigurováno** (výchozí) znemožní učitelům uzamknout aplikace nebo zařízení pomocí aplikace učebny bez vyzvání studenta.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Automaticky připojovat třídy učeben bez výzvy k zadání**: **Povolit** automaticky umožňuje studentům připojit se ke třídě, která je v aplikaci učebny bez vyzvání k učiteli. **Nenakonfigurováno** (výchozí) vyzývá učitele, aby se studenti chtěli připojit ke třídě, která je v aplikaci učebny.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Blokovat vytvoření sítě VPN**: **blok** zabraňuje uživatelům v vytváření nastavení konfigurace sítě VPN. **Nenakonfigurováno** (výchozí) umožňuje uživatelům vytvářet v zařízení sítě VPN.
- **Úprava nastavení eSIM**: **blok** znemožní uživatelům odebrat nebo přidat plán na mobilní zařízení na kartě zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům změnit tato nastavení.

  Tato funkce platí pro:  
  - iOS 12,1 a novější
  - iPadOS 13,0 a novější

- **Odložit aktualizace softwaru**: Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), v zařízení se zobrazí aktualizace softwaru, které Apple uvolňuje. Například pokud se aktualizace pro iOS/iPadOS uvolní od společnosti Apple v konkrétní datum, pak se tato aktualizace přirozeně zobrazuje na zařízení po datu vydání verze.

  **Možnost Povolit** umožňuje prodlevu při zobrazení aktualizací softwaru na zařízeních, od 0-90 dnů. Toto nastavení neřídí, kdy jsou aktualizace nebo nejsou nainstalovány. 

  - **Zpoždění viditelnosti aktualizací softwaru**: zadejte hodnotu od 0-90 dnů. Po vypršení zpoždění budou uživatelé dostávat oznámení o aktualizaci na nejstarší verzi operačního systému, která je k dispozici při spuštění zpoždění.

    Pokud je například iOS 12. a k dispozici **1. ledna**a je **zpoždění viditelnosti** nastaveno na **5 dní**, pak se iOS 12. a nezobrazí jako dostupná aktualizace na zařízeních koncových uživatelů. Po **šestém dni** od vydání je tato aktualizace dostupná a koncoví uživatelé ji můžou nainstalovat.

    Toto nastavení platí pro:  
    - iOS 11,3 a novější
    - iPadOS 13,0 a novější

## <a name="password"></a>Heslo

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Heslo**: **vyžaduje** , aby koncový uživatel zadal heslo pro přístup k zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům přístup k zařízení bez zadání hesla.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

> [!IMPORTANT]
> Pokud u zařízení zaregistrovaných uživatelem nakonfigurujete nastavení hesla, budou jednoduchá nastavení **hesla** automaticky nastavená tak, aby se **zablokovala**, a bude vynucený kód PIN s 6 číslicemi.
>
> Například nakonfigurujete nastavení **vypršení platnosti hesla** a tuto zásadu nahrajete do zařízení zaregistrovaných uživatelem. V zařízeních dojde k následujícímu:
>
> - Nastavení **vypršení platnosti hesla** je ignorováno.
> - Jednoduchá hesla, například `1111` nebo `1234`, nejsou povolena.
> - Je vynutil kód PIN pro číslice 6.

- **Jednoduchá hesla**: vyberte **blok** pro vyžadování složitějších hesel. **Nenakonfigurováno** umožňuje jednoduchá hesla, jako jsou `0000` a `1234`.

- **Požadovaný typ hesla**: Vyberte typ hesla, které vaše organizace vyžaduje. Možnosti:
  - **Výchozí ze zařízení**
  - **Číselné**
  - **Písmena**
- **Počet nealfanumerických znaků v hesle**: zadejte počet znaků symbolu, například `#` nebo `@`, které musí heslo obsahovat.

- **Minimální délka hesla**: zadejte minimální délku, kterou musí uživatel zadat, a to v rozmezí 4 až 14 znaků. Do zařízení zaregistrovaných uživatelem zadejte délku 4 až 6 znaků.
  
  > [!NOTE]
  > U zařízení, která jsou zaregistrovaná uživatelem, můžou uživatelé nastavit PIN kód o více než 6 číslic. V zařízení se ale neuplatní více než 6 číslic. Správce například nastaví minimální délku `8`. U zařízení zaregistrovaných uživatelem se uživatelům vyžaduje jenom zadání kódu PIN pro 6 číslic. Intune nevynutí na uživatelem zaregistrovaná zařízení kód PIN delší než 6 číslic.

- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet neúspěšných přihlášení, než se zařízení vymaže (mezi 4-11).
  
  iOS/iPadOS má integrované zabezpečení, které může mít vliv na toto nastavení. Například iOS/iPadOS může zpozdit spuštění zásady v závislosti na počtu neúspěšných přihlášení. Může také zvážit opakované zadání stejného hesla jako jednoho pokusu. [Příručka zabezpečení iOS/iPadOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) společnosti Apple (Otevírá web společnosti Apple) je dobrým prostředkem a poskytuje konkrétnější údaje o heslech.
  
- **Maximální počet minut po uzamčení obrazovky, po kterém se vyžaduje zadání hesla**<sup>1</sup>: zadejte, jak dlouho zůstane zařízení nečinné, než uživatel musí znovu zadat heslo. Pokud je čas, který zadáte, delší dobu, než je aktuálně nastaveno na zařízení, zařízení bude ignorovat čas, který zadáte. Podporováno na zařízeních s iOS 8.0 + a iPadOS 13.0 +.

- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**<sup>1</sup>: zadejte maximální počet minut nečinnosti, který je v zařízení povolený, dokud se nezamkne obrazovka.

  **Možnosti iOS/iPadOS**:  

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nedotkne.
  - **Okamžitě**: po 30 sekundách nečinnosti se zamkne obrazovka.
  - **1**: obrazovka se zamkne po 1 minutách nečinnosti.
  - **2**: obrazovka se zamkne po 2 minutách nečinnosti.
  - **3**: obrazovka se zamkne po 3 minutách nečinnosti.
  - **4**: obrazovka se zamkne po 4 minutách nečinnosti.
  - **5**: obrazovka se zamkne po 5 minutách nečinnosti.

  **iPadOS možnosti**:  

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nedotkne.
  - **Okamžitě**: po 2 minutách nečinnosti se zamkne obrazovka.
  - **2**: obrazovka se zamkne po 2 minutách nečinnosti.
  - **5**: obrazovka se zamkne po 5 minutách nečinnosti.
  - **10**: po 10 minutách nečinnosti se zamkne obrazovka.
  - **15**: po 15 minutách nečinnosti se zamkne obrazovka.

  Pokud se hodnota nevztahuje na iOS a iPadOS, pak Apple používá nejbližší *nejnižší* hodnotu. Pokud například zadáte `4` minut, zařízení iPadOS používají `2` minut. Pokud zadáte `10` minut, zařízení s iOS budou používat `5` minut. Toto je omezení Apple.
  
  > [!NOTE]
  > Uživatelské rozhraní Intune pro toto nastavení nedělí podporované hodnoty pro iOS a iPadOS. Uživatelské rozhraní může být v budoucí verzi aktualizováno.

- **Vypršení platnosti hesla (dny)** : zadejte počet dní, než bude nutné změnit heslo zařízení.
- **Zakázat opakované použití předchozích hesel**: zadejte počet nových hesel, která se musí použít, až bude možné znovu použít starou.
- **Dotykové ID a odemknutí ID obličeje**: vyberte **blok** , abyste zabránili použití otisku prstu nebo obličeje k odemknutí zařízení. **Není nakonfigurováno** umožňuje uživateli odemknout zařízení pomocí těchto metod.

  Blokování tohoto nastavení také znemožňuje zařízení odemknout pomocí ověřování FaceID.

  ID obličeje platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Úprava hesla**: vyberte **blok** a zastavte si změnu, přidání nebo odebrání hesla. Po blokování této funkce se změny v omezeních hesla ignorují na zařízeních pod dohledem. **Nenakonfigurováno** (výchozí) umožňuje přidávat, měnit a odebírat hesla.

  - **Úprava Touch ID a ID obličeje**: **blok** zastaví uživateli změnu, přidání nebo odebrání otisků prstů TouchID a ID obličeje. **Nenakonfigurováno** (výchozí) umožňuje uživateli aktualizovat otisky prstů TOUCHID a ID obličeje na zařízení.

    Blokování tohoto nastavení také uživateli brání v změně, přidání nebo odebrání ověřování FaceID.

    ID obličeje platí pro:  
    - iOS 11,0 a novější
    - iPadOS 13,0 a novější

- **Blokovat automatické vyplňování hesel**: Pokud chcete zabránit použití funkce automatického vyplňování hesel v iOS/iPadOS, vyberte **blokovat** . Výběr **bloku** má také následující dopad:

  - Uživatelům se nezobrazí výzva k použití uloženého hesla v Safari nebo ve všech aplikacích.
  - Automatická silná hesla jsou zakázaná a silná hesla se uživatelům nedoporučují.

  **Není nakonfigurováno** (výchozí) tyto funkce povolují.

- **Zablokovat žádosti o blízkost hesla**: zvolit **blok** , aby zařízení uživatele nepožadovalo hesla z blízkých zařízení. **Nenakonfigurováno** (výchozí) povoluje tyto požadavky na heslo.
- **Blokování sdílení hesel**: **blok** zabraňuje sdílení hesel mezi zařízeními pomocí přetažení. **Nenakonfigurováno** (výchozí) umožňuje sdílet hesla.
- **Pro automatické vyplňování informací pro heslo nebo platební kartu vyžadovat ověření dotykového ID nebo ID obličeje**: Pokud je nastavené na **vyžadovat**, musí se uživatelé ověřit pomocí TouchID nebo FaceID, než se můžou v Safari a dalších aplikacích vyplňovat hesla nebo informace o kreditních kartách. **Nenakonfigurováno** (výchozí) umožňuje uživatelům řídit tuto funkci v nastavení zařízení.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější
  
<sup>1</sup> když nakonfigurujete **maximální počet minut nečinnosti** , po kterém se zamkne obrazovka a **maximální počet minut po uzamčení obrazovky, když se bude vyžadovat nastavení hesla** , uplatní se v uvedeném pořadí. Pokud například nastavíte hodnotu pro obě nastavení na **5** minut, obrazovka se vypne automaticky po pěti minutách a zařízení se zamkne po dalších pět minut. Pokud ale uživatel vypne obrazovku ručně, druhé nastavení se použije okamžitě. Ve stejném příkladu potom, co uživatel vypne obrazovku, zařízení zamkne pět minut později.

## <a name="locked-screen-experience"></a>Prostředí zamknuté obrazovky

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Přístup k řídicímu centru při uzamčeném zařízení**: vyberte **blok** , aby se zabránilo přístupu k aplikaci řídicího centra, když je zařízení zamčené. **Nenakonfigurováno** (výchozí) umožňuje uživatelům přístup k aplikaci řídicího centra, když je zařízení zamčené.
- **Oznámení, když je zařízení zamknuté**: **blok** zabrání přístupu k oznámením, když je zařízení zamčené. **Nenakonfigurováno** (výchozí) umožňuje uživateli přístup k oznámením bez odemknutí zařízení.
- **Zobrazení dnes, když je zařízení uzamčené**: **blok** zabrání přístupu k zobrazení dnes, když je zařízení uzamčené. **Nenakonfigurováno** (výchozí) umožňuje uživateli zobrazit zobrazení dnes, když je zařízení zamčené.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Oznámení peněženky, když je zařízení uzamčené**: **blok** brání přístupu k aplikaci peněženky, když je zařízení zamčené. **Nenakonfigurováno** (výchozí) umožňuje uživateli přístup k aplikaci peněženky, když je zařízení zamčené.

## <a name="app-store-doc-viewing-gaming"></a>App Store, zobrazování dokumentů, hraní her

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Zobrazení firemních dokumentů v nespravovaných aplikacích**: **blok** zabraňuje zobrazení firemních dokumentů v nespravovaných aplikacích. **Nenakonfigurováno** (výchozí) umožňuje zobrazení podnikových dokumentů v libovolné aplikaci. Například chcete zabránit uživatelům v ukládání souborů z aplikace OneDrive do Dropboxu. Nakonfigurujte toto nastavení jako **blok**. Jakmile zařízení obdrží zásady (například po restartování), už neumožňuje uložení.


  > [!NOTE]
  > Pokud je toto nastavení blokované, zablokují se taky klávesnice třetích stran nainstalované z App Storu.

  - **Povolení čtení nespravovaných aplikací ze spravovaných účtů kontaktů**: Pokud nastavíte možnost **povoleno**, nespravované aplikace, jako je integrovaná aplikace pro iOS nebo iPadOS Contacts, můžou číst a přistupovat ke kontaktovým informacím ze spravovaných aplikací, včetně mobilní aplikace Outlook. **Nenakonfigurováno** (výchozí) zabraňuje čtení, včetně odebrání duplicit, z vestavěné aplikace kontaktů na zařízení.  
  
    Toto nastavení povoluje nebo znemožňuje čtení kontaktních informací. Neřídí synchronizaci kontaktů mezi aplikacemi.
  
    Pokud chcete použít toto nastavení, nastavte možnost **zobrazení firemních dokumentů v nespravovaných aplikacích** na **blokovat**.

  Další informace o těchto dvou nastaveních a jejich dopad na Outlook pro iOS/iPadOS kontaktování exportu najdete v tématu [Podpora tipů: použití nastavení vlastního profilu Intune s aplikací pro nativní kontakty iOS/iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- Považovat postupné **přetažení jako nespravovaného cíle**: **vyžadovat** , aby se přetažení považovalo za nespravovaný cíl přetažení. Zastaví spravované aplikace z odesílání dat pomocí přetažení. 
- **Zobrazení nefiremních dokumentů v podnikových aplikacích**: **blok** zabraňuje zobrazení nefiremních dokumentů v podnikových aplikacích. **Nenakonfigurováno** (výchozí) umožňuje zobrazit libovolný dokument v podnikových spravovaných aplikacích.

  Nastavení **blokování** taky brání synchronizaci exportu kontaktů v Outlooku pro iOS/iPadOS. Další informace najdete v tématu [Podpora tipů: povolení aplikace Outlook pro iOS/IPadOS synchronizace kontaktů s ovládacími prvky](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453)správy mobilních zařízení (MDM) iOS12.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Vyžadovat heslo pro iTunes Store pro všechny nákupy**: **vyžaduje** , aby uživatel zadal heslo Apple ID pro každý nákup v aplikaci nebo iTunes. **Nenakonfigurováno** (výchozí) umožňuje nákupy bez výzvy k zadání hesla pokaždé, když.
- **Nákupy v aplikaci**: vyberte možnost **blokovat** , aby se zabránilo nákupům v aplikaci ze Storu. **Nenakonfigurováno** (výchozí) umožňuje nákup obchodů v běžící aplikaci.
- **Stáhnout obsah z úložiště obchodu iBooks s označením jako ' Erotika '** : vyberte možnost **blokovat** , pokud chcete zabránit uživatelům v stahování médií z obchodu iBooks úložiště, které je označeno jako erotika. **Nenakonfigurováno** (výchozí) umožňuje uživateli stahovat knihy s kategorií "Erotika".
- **Umožňuje spravovaným aplikacím psát kontakty na nespravované účty kontaktů**: Pokud je nastavené na **povoleno**, spravované aplikace, jako je například mobilní aplikace Outlook, můžou ukládat nebo synchronizovat kontaktní informace, včetně obchodních a firemních kontaktů, do integrované aplikace pro iOS/iPadOS Contacts. Pokud je nastavené na **Nenakonfigurováno** (výchozí), spravované aplikace nemůžou ukládat ani synchronizovat kontaktní informace na integrované aplikaci pro iOS/iPadOS kontakty na zařízení.
  
  Pokud chcete použít toto nastavení, nastavte možnost **zobrazení firemních dokumentů v nespravovaných aplikacích** na **blokovat**.

- **Oblast hodnocení**: Vyberte oblast hodnocení, kterou chcete použít pro povolené soubory ke stažení. A pak zvolte povolené hodnocení **filmů**, **televizních**pořadů a **aplikací**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **App Store**: **blok** zabrání přístupu k obchodu s aplikacemi na zařízeních pod dohledem. **Nenakonfigurováno** (výchozí) umožňuje přístup.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

  - **Instalují se aplikace z App Storu**: vyberte **blok** pro blokování obchodu s aplikacemi z domovské obrazovky zařízení. Koncoví uživatelé můžou aplikace dál instalovat pomocí iTunes nebo Apple Configuratoru. **Nenakonfigurováno** (výchozí) povolí App Storu na domovské obrazovce.
  - **Automatické stahování aplikací**: výběrem možnosti **blokovat** zabráníte automatickému stahování aplikací zakoupených na jiných zařízeních. Nemá vliv na aktualizace existujících aplikací. **Nenakonfigurováno** (výchozí) umožňuje, aby se aplikace na zařízení nakoupily na jiných zařízeních s iOS/iPadOS.

- **Explicitní Hudba iTunes, podcast nebo obsah zpráv**: vyberte **blok** , abyste zabránili explicitnímu obsahu iTunes v hudbě, podcastech nebo zprávách. **Nenakonfigurováno** (výchozí) povolí zařízení přístup k obsahu, který je hodnocen jako dospělý ze Storu.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Přidání Game Center přátelé**: **blok** zabraňuje uživatelům v přidávání Game Centerch přátel. **Nenakonfigurováno** (výchozí) umožňuje uživateli přidávat přátele do Game Center.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Game Center**: **blokovat** použití aplikace Game Center **Nenakonfigurováno** (výchozí) umožňuje použití aplikace Game Center v zařízení.
- **Hry pro více hráčů**: vyberte možnost **blokovat** , aby se zabránilo hraní her. **Nenakonfigurováno** (výchozí) umožňuje uživateli hrát hry s více hráči na zařízení.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Přístup k síťové jednotce v aplikaci soubory**: použití protokolu SMB (Server Message Block), zařízení mají přístup k souborům nebo jiným prostředkům na síťovém serveru. Při **vypnutí** se zabrání přístupu k souborům na síťové jednotce SMB. **Nenakonfigurováno** (výchozí) umožňuje přístup.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="built-in-apps"></a>Integrované aplikace

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Siri**: **Block** znemožní přístup k Siri. **Nenakonfigurováno** (výchozí) umožňuje použití hlasového asistenta Siri na zařízení.
  - **Siri, když je zařízení uzamčené**: Pokud chcete zabránit přístupu k Siri, když je zařízení uzamčené, vyberte **blokovat** . **Nenakonfigurováno** (výchozí) povolí použití hlasového asistenta Siri na zařízení, když je zamčený.

- **Upozornění na podvod v Safari**: **vyžaduje** zobrazení upozornění na podvod ve webovém prohlížeči na zařízení. **Nenakonfigurováno** (výchozí) tuto funkci zakáže.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Vyhledávání Spotlightu, které vrátí výsledky z Internetu**: **blok** přestane vracet žádné výsledky z internetu hledání. **Nenakonfigurováno** (výchozí) umožňuje vyhledávání Spotlightu připojit se k Internetu a poskytnout tak výsledky hledání.

- **Soubory cookie prohlížeče Safari**: Vyberte způsob zpracování souborů cookie v zařízení. Možnosti:
  - Povolit
  - Blokovat všechny soubory cookie
  - Povolení souborů cookie z navštívených webů
  - Povoluje soubory cookie z aktuálního webu

- **Safari JavaScript**: **blok** znemožní v zařízení spouštět skripty Java v prohlížeči. **Nenakonfigurováno** (výchozí) povolí skripty Java.

- **Automaticky otevíraná okna Safari**: **zakažte blokování automaticky** otevíraných oken ve webovém prohlížeči. **Nenakonfigurováno** (výchozí) povolí blokování automaticky otevíraných oken.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Kamera**: vyberte možnost **blokovat** , pokud chcete zabránit přístupu k fotoaparátu na zařízení. **Nenakonfigurováno** (výchozí) umožňuje přístup k kameře zařízení.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

  - **FaceTime**: **blok** , aby se zabránilo přístupu k aplikaci FaceTime. **Nenakonfigurováno** (výchozí) povolí přístup k aplikaci FaceTime na zařízení.

    Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Filtr vulgárních výrazů v Siri**: **vyžadovat, aby** Siri nemohlo diktovat nebo diktovat vulgární jazyk.

  Chcete-li použít toto nastavení, nastavte nastavení **Siri** na **blokovat**.

- **Siri dotazování na uživatelem generovaný obsah z Internetu**: **blok** zabraňuje tomu, aby Siri přístup k webům, aby mohla odpovídat na otázky. **Nenakonfigurováno** (výchozí) umožňuje Siri přistupovat k obsahu generovanému uživateli z Internetu.

  Chcete-li použít toto nastavení, nastavte nastavení **Siri** na **blokovat**.

- **Apple News**: vyberte možnost **blokovat** , aby se zabránilo přístupu k aplikaci Apple News na zařízení. **Nenakonfigurováno** (výchozí) umožňuje použití aplikace Apple News.
- **iBooks Store**: **blok** znemožní přístup k úložišti iBooks. **Nenakonfigurováno** (výchozí) umožňuje uživatelům procházet a kupovat knihy z iBooks Storu.
- **Aplikace zprávy na zařízení**: **blok** zabraňuje uživatelům v používání aplikace zprávy pro iMessage. Pokud zařízení podporuje textové zasílání zpráv, může uživatel i nadále odesílat a přijímat textové zprávy pomocí serveru SMS. **Nenakonfigurováno** (výchozí) umožňuje použití aplikace zprávy k posílání a čtení zpráv přes Internet.
- **Podcasty**: **blokování** brání uživatelům v použití aplikace Podcasty. **Nenakonfigurováno** (výchozí) umožňuje použití aplikace Podcasty.
- **Hudební služba**: **blok** vrátí aplikaci v hudbě do klasického režimu a zakáže hudební službu. **Nenakonfigurováno** (výchozí) umožňuje použití aplikace Apple Music.
- **služba iTunes Radio Service**: **blok** zabraňuje uživatelům v používání aplikace iTunes Radio. **Nenakonfigurováno** (výchozí) umožňuje použití aplikace iTunes Radio.
- **iTunes Store**: **Nenakonfigurováno** (výchozí) povolí iTunes na zařízeních. **Blok** zabraňuje uživatelům v zařízení používat iTunes. 

  Tato funkce platí pro:  
  - iOS 4,0 a novější
  - iPadOS 13,0 a novější

- **Najít iPhone**: **Nenakonfigurováno** (výchozí) umožňuje pomocí této funkce najít moji aplikaci získat přibližnou polohu zařízení. **Blok** zabraňuje této funkci v aplikaci najít moji. 

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

- **Najít přátele**: **Nenakonfigurováno** (výchozí) umožňuje pomocí této funkce najít moji aplikaci najít rodinu a přátele ze zařízení Apple nebo iCloud.com. **Blok** zabraňuje této funkci v aplikaci najít moji.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

- **Změny v nastavení aplikace Find My Friends**: **Block** zabraňuje změnám v nastavení aplikace Find My Friends. **Nenakonfigurováno** (výchozí) umožňuje uživateli měnit nastavení aplikace najít přátele.

- **Vyhledávání Spotlightu, které vrátí výsledky z Internetu**: **blok** přestane vracet žádné výsledky z internetu hledání. **Nenakonfigurováno** (výchozí) umožňuje vyhledávání Spotlightu připojit se k Internetu a poskytnout tak výsledky hledání.

- **Blokovat odebírání systémových aplikací ze zařízení**: Volba možnosti **blokovat** zakáže možnost odebrání systémových aplikací ze zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům odebrat systémové aplikace.

- **Safari**: **zablokujte** v zařízení použití prohlížeče Safari. **Nenakonfigurováno** (výchozí) umožňuje uživatelům používat prohlížeč Safari.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Safari AutoFill**: **Block** zakáže funkci automatického vyplňování v prohlížeči Safari na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům změnit nastavení automatického dokončování ve webovém prohlížeči.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

## <a name="restricted-apps"></a>Omezené aplikace

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Typ seznamu omezených aplikací**: vytvoří seznam aplikací, které uživatelé nemůžou instalovat ani používat. Možnosti:

  - **Nenakonfigurováno** (výchozí): neexistují žádná omezení z Intune. Uživatelé mají přístup k aplikacím, které přiřadíte, a k integrovaným aplikacím.
  - **Zakázané aplikace**: aplikace nespravované přes Intune, které nechcete v zařízení nainstalovat. Uživatelům není instalace zakázané aplikace znemožněna. Pokud ale uživatel z tohoto seznamu nainstaluje aplikaci, nahlásí se v Intune.
  - **Schválené aplikace**: aplikace, které můžou uživatelé instalovat. Uživatelé nesmí instalovat aplikace, které nejsou uvedené. Aplikace, které spravuje Intune, jsou povolené automaticky. Uživatelům není znemožněna instalace aplikace, která není na seznamu schválených. Pokud tomu tak je, nahlásí se v Intune.

Pokud chcete do těchto seznamů přidat aplikace, můžete:

- **Přidejte** adresu URL obchodu iTunes pro aplikaci, kterou chcete. Pokud například chcete přidat aplikaci Microsoft work folders, zadejte `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` nebo `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`.

  Pokud chcete najít adresu URL aplikace, otevřete aplikaci iTunes App Store a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop` nebo `Microsoft Word`. Vyberte aplikaci a zkopírujte adresu URL.

  K vyhledání aplikace můžete také použít iTunes a potom pomocí úlohy **Kopírovat odkaz** získat adresu URL aplikace.

- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app url>, <app name>, <app publisher>`. Případně **exportujte** existující seznam obsahující seznam aplikací s omezeným přístupem ve stejném formátu.

> [!IMPORTANT]
> Profily zařízení, které používají nastavení aplikací s omezeným přístupem, se musí přiřadit ke skupinám uživatelů.

## <a name="show-or-hide-apps"></a>Zobrazit nebo skrýt aplikace

Platí pro zařízení se systémem iOS 9.3 + a iPadOS 13.0 +.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Typ seznamu aplikací**: Vytvořte seznam aplikací, které chcete zobrazit nebo skrýt. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094). Možnosti:

  - **Skryté aplikace**: Zadejte seznam aplikací, které jsou pro uživatele skryté. Uživatelé nemůžou tyto aplikace zobrazit ani otevřít.
  
    Apple znemožní skrývání některých nativních aplikací. Nemůžete třeba na zařízení skrýt aplikaci **Nastavení** . [Odstranění integrovaných aplikací Apple](https://support.apple.com/HT208094) zobrazí seznam aplikací, které se dají skrýt.
  
  - **Viditelné aplikace**: Zadejte seznam aplikací, které uživatelé mohou zobrazit a spustit. Žádné jiné aplikace nebude možné zobrazit ani spustit.

- **Adresa URL aplikace**: zadejte adresu URL aplikace pro Store aplikace, kterou chcete zobrazit nebo skrýt. Příklad:

  - Pokud chcete přidat aplikaci Microsoft work folders, zadejte `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` nebo `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`. 

  - Chcete-li přidat aplikaci Microsoft Word, zadejte `https://itunes.apple.com/de/app/microsoft-word/id586447913` nebo `https://apps.apple.com/de/app/microsoft-word/id586447913`.

  Pokud chcete najít adresu URL aplikace, otevřete aplikaci iTunes App Store a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop` nebo `Microsoft Word`. Vyberte aplikaci a zkopírujte adresu URL.

  K vyhledání aplikace můžete také použít iTunes a potom pomocí úlohy **Kopírovat odkaz** získat adresu URL aplikace.

- **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Název aplikace**: zadejte název aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Vydavatel**: zadejte vydavatele aplikace, kterou chcete.

Pokud chcete přidat aplikace, můžete:

- **Přidat**: vyberte, pokud chcete vytvořit seznam aplikací.
- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app url>, <app name>, <app publisher>`. Případně můžete **exportovat** a vytvořit seznam aplikací s omezeným přístupem, které jste přidali, ve stejném formátu.

## <a name="wireless"></a>Bezdrátová síť

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

Poznámka potřeba pro datový roaming (Tip nebo důležitá Poznámka pro usnadnění nejasností zákazníků): Toto nastavení se nezobrazí v profilu správy cílového zařízení. Důvodem je to, že toto nastavení se považuje za akci vzdáleného zařízení a pokaždé, když se v zařízení změní stav datového roamingu, bude službou Intune zablokovaný znovu. I když není v profilu správy, funguje, pokud se zobrazuje jako úspěch z vytváření sestav v konzole pro správu. 
- **Datový roaming**: vyberte možnost **blokovat** , pokud chcete datový roaming zabránit v mobilní síti. **Nenakonfigurováno** (výchozí) povolí datový roaming, když je zařízení v mobilní síti.

  > [!IMPORTANT]
  > Toto nastavení se považuje za akci vzdáleného zařízení. Toto nastavení se proto nezobrazí v profilu správy na zařízení. Pokaždé, když se v zařízení změní stav roamingu dat, služba Intune zablokuje **datový roaming** . Pokud se v Intune zobrazuje stav sestavy úspěch, pak víte, že funguje, i když se toto nastavení nezobrazí v profilu správy na zařízení.

- **Globální načítání na pozadí při roamingu**: při roamingu v mobilní síti znemožní **blokování** použití globální funkce načítání na pozadí. **Nenakonfigurováno** (výchozí) umožňuje zařízení při roamingu v mobilní síti načíst data, například e-mailu.
- **Hlasové vytáčení**: vyberte možnost **blokovat** , pokud chcete uživatelům zabránit v používání funkce hlasového vytáčení na zařízení. **Nenakonfigurováno** (výchozí) umožňuje hlasové vytáčení zařízení.
- **Hlasový roaming**: vyberte **blok** , aby se zabránilo hlasovému roamingu přes mobilní síť. **Nenakonfigurováno** (výchozí) povolí hlasový roaming, když je zařízení v mobilní síti.
- **Osobní hotspot**: **blok** vypne osobní hotspot na zařízení uživatelů při každé synchronizaci zařízení. Toto nastavení nemusí být kompatibilní s některými provozovateli. **Nenakonfigurováno** (výchozí) udržuje konfiguraci osobního hotspotu jako výchozí nastavenou uživatelem.

  > [!IMPORTANT]
  > Toto nastavení se považuje za akci vzdáleného zařízení. Toto nastavení se proto nezobrazí v profilu správy na zařízení. Pokaždé, když se změní stav osobního hotspotu na zařízení, služba Intune zablokuje **osobní hotspot** . Pokud se v Intune zobrazuje stav sestavy úspěch, pak víte, že funguje, i když se toto nastavení nezobrazí v profilu správy na zařízení.

- **Pravidla pro mobilní použití (jenom spravované aplikace)** : Definujte datové typy, které spravované aplikace můžou používat při použití v mobilních sítích. Možnosti:
  - **Zablokovat používání mobilních dat**: blokuje používání mobilních dat pro **všechny spravované aplikace** nebo umožňuje **zvolit konkrétní aplikace**.
  - **Zablokovat používání mobilních dat při roamingu**: při roamingu používejte mobilní data pro **všechny spravované aplikace** nebo **vyberte konkrétní aplikace**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Změny nastavení využití mobilních dat v aplikaci**: vyberte možnost **blokovat** , aby se zabránilo změnám nastavení využití mobilních dat v aplikaci. **Nenakonfigurováno** (výchozí) umožňuje uživateli řídit, které aplikace můžou používat mobilní data.
- **Změny nastavení plánu mobilní**sítě: **blok** znemožní uživatelům měnit nastavení v plánu pro mobilní síť. **Nenakonfigurováno** (výchozí) umožňuje uživatelům provádět změny.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Úprava osobního hotspotu**: Pokud je nastavená možnost **blokovat**, uživatel nemůže změnit nastavení osobního hotspotu. **Nenakonfigurováno** (výchozí) umožňuje koncovým uživatelům povolit nebo zakázat svůj osobní hotspot.

  Pokud zablokujete toto nastavení a zablokujete nastavení **osobní hotspotu** , bude osobní hotspot vypnutý.

  Tato funkce platí pro:  
  - iOS 12,2 a novější
  - iPadOS 13,0 a novější

- **Připojit se k sítím Wi-Fi jenom pomocí konfiguračních profilů**: **vyžaduje** , aby zařízení používalo jenom sítě Wi-Fi nastavené prostřednictvím konfiguračních profilů Intune. **Nenakonfigurováno** (výchozí) umožňuje zařízení používat jiné sítě Wi-Fi.

  Pokud je nastaveno na **vyžadovat**, ujistěte se, že má zařízení profil sítě Wi-Fi. Pokud nepřiřazujete profil sítě Wi-Fi, může toto nastavení zabránit tomu, aby se zařízení připojovalo k Internetu. Jinými slovy, pokud je tento profil omezení zařízení přiřazen před profilem Wi-Fi, zařízení může být zablokované v připojení k Internetu.
  
  Pokud se nemůže připojit, zaregistrujte zařízení a pak ho znovu zaregistrujte pomocí profilu sítě Wi-Fi. Potom nastavte toto nastavení na **vyžadovat** v profilu omezení zařízení a přiřaďte k zařízení profil.

- **Wi-Fi vždycky zapnuté**: Pokud je nastavené na **vyžadovat**, Wi-Fi zůstane v aplikaci nastavení. Nedá se vypnout v nastavení nebo v řídicím centru, a to ani v případě, že je zařízení v režimu v letadle. **Nenakonfigurováno** (výchozí) umožňuje uživateli řídit zapnutí nebo vypnutí Wi-Fi.

  Konfigurace tohoto nastavení nezabrání uživatelům v výběru sítě Wi-Fi.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="connected-devices"></a>Připojená zařízení

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Detekce zápěstí pro spárovaná Apple Watch**: **vyžaduje** , aby se u spárovaného Apple Watch použilo zjišťování zápěstí. V případě potřeby nebude Apple Watch zobrazovat oznámení, pokud se nepoužívá. 

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Vyžadovat párovací heslo pro odchozí požadavky AirPlay**: **vyžaduje** párování hesla, pokud uživatel použije AirPlay ke streamování obsahu do jiných zařízení Apple. **Nenakonfigurováno** (výchozí) povolí uživateli streamování obsahu pomocí AirPlay bez zadání hesla.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Přetažení**: **blok** zabraňuje použití přetahování na zařízení. **Nenakonfigurováno** (výchozí) umožňuje použití funkce prohodit pro výměnu obsahu s blízkými zařízeními.
- **Apple Watch párování**: **blok** brání párování s Apple Watch. **Nenakonfigurováno** (výchozí) povolí zařízení párování s Apple Watch.
- **Úpravy Bluetooth**: **blok** zabrání koncovému uživateli ve změně nastavení Bluetooth na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživateli změnit tato nastavení.
- **Párování hostitelů pro řízení zařízení, se kterými se zařízení s iOS/iPadOS může spárovat**: **není nakonfigurovaná** (výchozí) umožňuje správcům řídit, která zařízení se můžou spárovat se zařízením s iOS/iPadOS. **Blok** zabraňuje párování hostitelů.
- **Blokovat tisk**: vyberte možnost **blokovat** , pokud chcete zabránit použití funkce pro tisk do zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživateli používat postupné tisku.
  - **Blokovat úložiště přihlašovacích údajů pro tisk v řetězci klíčů**: **blok** zabraňuje použití úložiště klíčů pro uživatelské jméno a heslo v zařízení. **Nenakonfigurováno** (výchozí) umožňuje ukládání uživatelského jména a hesla pro tisk do aplikace pro řetězce klíčů.
  - **Vyžadovat důvěryhodný certifikát TLS pro spolutisk**: **vyžaduje** , aby zařízení používalo důvěryhodné certifikáty pro komunikaci tisku TLS.
  - **Zablokovat blokovat iBeacon u rozpoznávání tiskových tiskáren**: **blok** zabraňuje škodlivým signálům přes útok Bluetooth v přenosu dat v síti. **Nenakonfigurováno** (výchozí) umožňuje reklamní tiskové tiskárny na zařízení.
- **Blokování nastavení nových okolních zařízení**: **blok** zakáže výzvu k nastavení nových zařízení, která jsou v okolí. **Nenakonfigurováno** (výchozí) umožňuje uživatelům výzvy, aby se připojili k jiným blízkým zařízením Apple.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Přístup k souborům na jednotce USB**: zařízení se můžou připojit a otevírat soubory na USB jednotce. Pokud je zařízení USB připojené k zařízení, **zakažte zakázat** přístup zařízení k jednotce USB v aplikaci soubory. Zakázáním této funkce se taky zablokuje koncovým uživatelům přenos souborů na jednotku USB připojenou k iPadu. **Nenakonfigurováno** (výchozí) povolí přístup k jednotce USB v aplikaci Files.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="keyboard-and-dictionary"></a>Klávesnice a slovník

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Vyhledávání definic slov**: **Block** znemožní uživateli zvýraznit slovo a pak vyhledat jeho definici na zařízení. **Nenakonfigurováno** (výchozí) umožňuje přístup k funkci vyhledávání definic.
- **Prediktivní klávesnice**: **Nenakonfigurováno** (výchozí) umožňuje pomocí prediktivních klávesnic navrhovat slova, která může chtít uživatel. **Blokování** brání této funkci.
- **Automatické opravy**: **Nenakonfigurováno** (výchozí) umožňuje zařízení automaticky opravovat slova s překlepem. **Blok** zabraňuje použití automatických oprav.
- **Kontrola pravopisu klávesnice**: **Nenakonfigurováno** (výchozí) umožňuje použít kontrolu pravopisu na zařízení. **Blok** umožňuje kontrolu pravopisu.
- **Klávesové zkratky**: **Nenakonfigurováno** (výchozí) umožňuje používání klávesových zkratek na zařízení. **Blok** zabrání uživateli v používání klávesových zkratek.
- **Diktování**: **blok** zabrání uživateli v použití hlasového vstupu k zadání textu. **Nenakonfigurováno** (výchozí) umožňuje uživateli používat vstup diktování.
- **QuickPath**: **Nenakonfigurováno** (výchozí) umožňuje uživatelům používat QuickPath, což umožňuje průběžné zadávání na klávesnici zařízení. Uživatelé můžou k vytváření slov psát přetáhnutím prstem přes tyto klávesy. **Blok** zabraňuje uživatelům v používání QuickPath. 

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="cloud-and-storage"></a>Cloud a úložiště

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Šifrované zálohování**: **vyžaduje** , aby bylo zálohování zařízení nutné šifrovat.
- **Synchronizace spravovaných aplikací do cloudu**: **Nenakonfigurováno** (výchozí) umožňuje, aby aplikace Intune spravovaly data na účet iCloud uživatele. **Blok** zabraňuje synchronizaci těchto dat s iCloud.
- **Blokovat zálohování v podnikové knize**: vyberte možnost **blokovat** , pokud chcete uživatelům zabránit v zálohování podnikových knih. **Nenakonfigurováno** (výchozí) umožňuje uživatelům zálohovat tyto knihy.
- **Blokování synchronizace metadat v podnikovém adresáři (poznámky a zvýraznění)** : **blok** zabraňuje synchronizaci poznámek a světel v podnikových knihách. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Synchronizace datových proudů do iCloud**: **není nakonfigurovaná** (výchozí) umožňuje uživatelům povolit, aby se **Váš fotografický Stream** na svém zařízení synchronizoval s iCloud a aby byly na všech zařízeních uživatele dostupné fotky. **Blok** zabraňuje synchronizaci streamování fotografií do iCloud. Blokování této funkce může způsobit ztrátu dat. 
- **Knihovna fotografií iCloud**: Pokud chcete zakázat používání knihovny fotografií iCloud k ukládání fotek a videí do cloudu, nastavte **blokování** . Ze zařízení se odeberou všechny fotky, které nejsou kompletně stažené z knihovny fotografií iCloud. **Nenakonfigurováno** (výchozí) umožňuje použití knihovny fotografií iCloud.
- **Sdílený datový proud fotek**: výběrem možnosti **blokovat** zakážete **Sdílení fotek iCloud** na zařízení. **Nenakonfigurováno** (výchozí) umožňuje sdílení fotek.
- **Předání**: **Nenakonfigurováno** (výchozí) umožňuje uživatelům začít pracovat na zařízení se systémem iOS/iPadOS a potom pokračovat v práci, kterou zahájili na jiném zařízení s iOS/iPadOS nebo MacOS. **Blok** zabraňuje tomuto předání.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Zálohování do iCloud**: **Nenakonfigurováno** (výchozí) umožňuje uživateli zálohovat zařízení na iCloud. **Blokování** zabrání uživateli v zálohování zařízení do iCloud.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Blokování synchronizace dokumentů iCloud**: **Nenakonfigurováno** (výchozí) povolí synchronizaci dokumentu a klíč-hodnota do prostoru úložiště iCloud. **Blok** zabraňuje iCloud synchronizaci dokumentů a dat.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Blokovat synchronizaci řetězce klíčů iCloud**: Pokud chcete zakázat synchronizaci přihlašovacích údajů uložených v řetězci klíčů do iCloud, vyberte **blok** . **Nenakonfigurováno** (výchozí) umožňuje uživatelům synchronizovat tyto přihlašovací údaje.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

## <a name="autonomous-single-app-mode"></a>Autonomní režim jedné aplikace

Pomocí těchto nastavení můžete nakonfigurovat zařízení s iOS/iPadOS, aby spouštěla konkrétní aplikace v autonomním režimu jedné aplikace. Když je tento režim nakonfigurovaný a uživatel spustí jednu z nakonfigurovaných aplikací, zařízení se zamkne do této aplikace. Přepínání aplikace nebo úlohy je zakázané, dokud uživatel neukončí povolenou aplikaci.

Například ve škole nebo univerzitním prostředí přidejte aplikaci, která umožní uživatelům provést test na zařízení. Nebo zařízení uzamkněte do aplikace Portál společnosti, dokud se koncový uživatel neověří. Když uživatel akce aplikace dokončí nebo tuto zásadu odeberete, zařízení se vrátí do normálního stavu.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Název aplikace**: zadejte název aplikace, kterou chcete.
- **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace, kterou chcete.
- **Přidat**: vyberte, pokud chcete vytvořit seznam aplikací.

Soubor CSV můžete také **naimportovat** se seznamem názvů aplikací a jejich ID sady. Případně **exportujte** existující seznam obsahující aplikace.

## <a name="kiosk"></a>Veřejný terminál

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Aplikace, která se má spustit v celoobrazovkovém režimu**: Vyberte typ aplikací, které chcete spustit v celoobrazovkovém režimu. Možnosti:
  - **Nenakonfigurováno** (výchozí): Nastavení veřejného terminálu se nepoužijí. Zařízení neběží v celoobrazovkovém režimu.
  - **Aplikace ze Storu**: zadejte adresu URL aplikace v iTunes App Storu.
  - **Spravovaná aplikace**: vyberte aplikaci, kterou jste přidali do Intune.
  - **Vestavěná aplikace**: zadejte [ID sady](bundle-ids-built-in-ios-apps.md) předdefinovaných aplikací.

- **Dotykové ovládání**pro usnadnění: **vyžaduje** , aby na zařízení bylo nastavení usnadnění dotykového ovládání. Tato funkce pomáhá uživatelům s gesty na obrazovce, která by pro ně mohla být obtížná. **Není nakonfigurováno** , nespustí nebo povolí tuto funkci v celoobrazovkovém režimu.
- **Invertování barev**: **vyžaduje** nastavení usnadnění invertování barev, aby uživatelé s zrakovým postižením mohli obrazovku pro zobrazení změnit. **Není nakonfigurováno** , nespustí nebo povolí tuto funkci v celoobrazovkovém režimu.
- **Mono zvuk**: **vyžaduje** , aby na zařízení bylo nastavení usnadnění Mono zvuk. **Není nakonfigurováno** , nespustí nebo povolí tuto funkci v celoobrazovkovém režimu.
- **Ovládání hlasu**: **vyžaduje** povolení ovládání hlasu na zařízení a umožňuje uživatelům plně ovládat operační systém pomocí příkazů Siri. **Nenakonfigurováno** zakáže ovládací prvek hlasu na zařízení.

  Toto nastavení platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější
  
  > [!TIP]
  > Pokud máte ve vaší organizaci k dispozici obchodní aplikace a nejsou v nich k dispozici **hlasové řízení** připravené na den 0 při vydání iOS 13,0, doporučujeme toto nastavení ponechat **nenakonfigurované**.

- **VoiceOver**: **vyžaduje** , aby se na zařízení načetlo nastavení usnadnění VoiceOver pro čtení textu na obrazovce. **Není nakonfigurováno** , nespustí nebo povolí tuto funkci v celoobrazovkovém režimu.
- **Zoom**: **vyžaduje** , aby na zařízení bylo nastaveno přiblížení, aby uživatelé mohli použít dotykové ovládání k přiblížení obrazovky. **Není nakonfigurováno** , nespustí nebo povolí tuto funkci v celoobrazovkovém režimu.
- **Auto Lock**: **Block** znemožňuje automatické uzamykání zařízení. **Nenakonfigurováno** umožňuje tuto funkci.
- **Přepínač vyzvánění**: **Block** zakáže přepínač vyzvánění (ztlumení) na zařízení. **Nenakonfigurováno** umožňuje tuto funkci.
- **Otočení obrazovky**: **blok** znemožňuje změnu orientace obrazovky, když uživatel otočí zařízení. **Nenakonfigurováno** umožňuje tuto funkci.
- **Tlačítko pro režim spánku obrazovky**: vyberte možnost **blokovat** . Tím zakážete na zařízení tlačítko probuzení z režimu spánku obrazovky. **Nenakonfigurováno** umožňuje tuto funkci.
- **Dotyk**: **Block** zakáže dotykovou obrazovku na zařízení. **Není nakonfigurováno** umožňuje uživateli používat dotykovou obrazovku.
- **Tlačítka hlasitosti**: **blok** zabraňuje použití tlačítek hlasitosti na zařízení. **Není nakonfigurováno** , umožňuje tlačítka hlasitosti.
- **Řízení dotykového**ovládání pro usnadnění: **umožňuje povolit** uživatelům používat funkci usnadnění dotykového ovládání. **Není nakonfigurováno** , zakáže tuto funkci.
- **Invertování barev – ovládací prvek**: **Povolit** Invertovat změny barev, aby uživatelé mohli upravovat funkci invertování barev. **Není nakonfigurováno** , zakáže tuto funkci.
- **Mluvit na vybraném textu**: **povolí** nastavení usnadnění výběru řeči na zařízení. Tato funkce přečte text, který uživatel vybírá nahlas. **Není nakonfigurováno** , zakáže tuto funkci.
- **Úpravy hlasového ovládacího prvku**: **umožňuje** uživatelům změnit stav ovládacího prvku hlas na svých zařízeních. **Nenakonfigurovaní** znemožní uživatelům měnit stav ovládacího prvku hlas na svých zařízeních.

  Toto nastavení platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

- **Ovládací prvek VoiceOver**: **Povolit** VoiceOver změny, aby uživatelé mohli aktualizovat funkci VoiceOver, jako je například způsob, jakým je rychlé čtení textu na obrazovce. **Není nakonfigurováno** , zabraňuje VoiceOver změnám.
- **Ovládací prvek Lupa**: **povolí** změny přiblížení uživatele. **Není nakonfigurováno** , zabraňuje změnám lupy.

> [!NOTE]
> Než budete moct nakonfigurovat zařízení se systémem iOS/iPadOS pro celoobrazovkový režim, musíte k uvedení zařízení do režimu pod dohledem použít nástroj Apple Configuratoru nebo Apple Program registrace zařízení. Podívejte se na téma Příručka Apple na používání nástroje Apple Configuratoru.
> Pokud je aplikace pro iOS/iPadOS, kterou zadáte, nainstalovaná po přiřazení profilu, zařízení nepřejde do celoobrazovkového režimu, dokud se zařízení nerestartuje.

## <a name="domains"></a>Domény

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Neoznačená e-mailová** doména > **Adresa URL e-mailové domény**: přidejte jednu nebo více adres URL do seznamu. Když koncoví uživatelé dostanou e-mail z jiné domény než z domén, které zadáte, v aplikaci pro iOS/iPadOS pošty se e-mail označí jako nedůvěryhodný.

- **Spravované webové domény** > **Adresa URL webové domény**; Přidejte do seznamu jednu nebo více adres URL. Po stažení dokumentů z domén, které zadáte, se považují za spravované. Toto nastavení platí jenom pro dokumenty stažené prostřednictvím prohlížeče Safari.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Domény pro automatické vyplňování hesel v Safari** > **doméně**: do seznamu přidejte jednu nebo více adres URL. Uživatelé si mohou uložit jenom webová hesla z adres URL uvedených v tomto seznamu. Toto nastavení platí jenom pro prohlížeč Safari a zařízení v režimu pod dohledem. Pokud nezadáte žádné adresy URL, bude možné ukládat hesla ze všech webů.

  Toto nastavení platí pro:  
  - iOS 9,3 a novější
  - iPadOS 13,0 a novější

## <a name="settings-that-require-supervised-mode"></a>Nastavení, které vyžaduje režim pod dohledem

režim iOS/iPadOS pod dohledem se dá povolit jenom při počátečním nastavení zařízení prostřednictvím Program registrace zařízení společnosti Apple nebo pomocí Apple Configuratoru. Po povolení režimu pod dohledem může Intune v zařízení nakonfigurovat následující funkce:

- Zámek aplikace (režim jedné aplikace) 
- Globální proxy server HTTP 
- Zakázání zámku aktivace 
- Autonomní režim jedné aplikace 
- Filtr webového obsahu 
- Nastavení pozadí a zamykací obrazovky 
- Tiché doručení aplikací bez vyžádání 
- Vždy zapnutá síť VPN 
- Povolení pouze instalace spravovaných aplikací 
- iBooks Store 
- Zprávy iMessage 
- Herní centrum 
- AirDrop 
- AirPlay 
- Hostitelské párování 
- Synchronizace cloudu 
- Vyhledávání Spotlight 
- Handoff 
- Vymazání zařízení 
- Uživatelské rozhraní pro omezení 
- Instalace konfiguračních profilů uživatelským rozhraním 
- News 
- Klávesové zkratky 
- Změny hesla 
- Změny názvu zařízení 
- Automatická stahování aplikací 
- Úpravy vztahu důvěryhodnosti u podnikových aplikací 
- Apple Music 
- Doručení pošty 
- Spárování s Apple Watch 

> [!NOTE]
> Apple potvrzuje, že určitá nastavení se přesunou do režimu pod dohledem – jenom v 2019. Při použití těchto nastavení doporučujeme tuto možnost vzít v úvahu, takže nemusíte čekat, až společnost Apple je migruje do režimu pod dohledem:
>
> - Instalace aplikací koncovými uživateli
> - Odebrání aplikace
> - FaceTime
> - Safari
> - iTunes
> - Explicitní obsah
> - Dokumenty a data v iCloudu
> - Hry pro víc hráčů
> - Přidat přátele z herního centra
> - Siri

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Na zařízeních [MacOS](device-restrictions-macos.md) můžete také omezit funkce a nastavení zařízení.
