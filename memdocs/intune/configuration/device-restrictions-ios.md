---
title: nastavení zařízení s iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních s iOS/iPadOS k omezení funkcí v Microsoft Intune. Vytvářejte požadavky na heslo, řídíte uzamčenou obrazovku, využijte integrované aplikace, přidávejte omezené nebo schválené aplikace, zpracujte zařízení Bluetooth, připojte se ke cloudu pro zálohování a úložiště, povolte celoobrazovkový režim, přidejte domény a můžete řídit, jak uživatelé pracují s webovým prohlížečem Safari.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b82e69c06868416f60a137a71fc72db8e39375b9
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813852"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>nastavení zařízení s iOS a iPadOS pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popisuje různá nastavení, která můžete řídit na zařízeních s iOS a iPadOS. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, nastavit pravidla pro hesla, povolit nebo omezit konkrétní aplikace a další.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí na vaše zařízení s iOS/iPadOS.

> [!TIP]
> Tato nastavení používají nastavení MDM od společnosti Apple. Další informace o těchto nastaveních najdete v tématu [Nastavení správy mobilních zařízení společnosti Apple](https://support.apple.com/guide/mdm/welcome/web) (otevření webu společnosti Apple).

## <a name="before-you-begin"></a>Než začnete

Vytvořte [konfigurační profil omezení zařízení s iOS/iPadOS](device-restrictions-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace s některými nastaveními, která platí pro všechny možnosti registrace. Další informace o různých typech registrace najdete v tématu Registrace zařízení se [systémem iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="general"></a>Obecné

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Sdílet data o využití**: **blokovat** zabrání zařízením v posílání diagnostických dat a dat o využití do Applu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém odesílat tato data.

- **Snímek obrazovky**: **blok** zabraňuje zachycení snímků obrazovky nebo obrazovek na zařízeních. V systému iOS/iPadOS 9,0 a novějších blokují také nahrávky obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém nechat uživatele zachytit obsah obrazovky jako obrázek nebo jako video.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Nedůvěryhodné certifikáty TLS**: **blok** zabraňuje nedůvěryhodným certifikátům TLS (Transport Layer Security) na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat certifikáty TLS.
- **Zablokovat vysoce dolety aktualizace PKI**: **blok** znemožní uživatelům přijímat aktualizace softwaru, pokud nejsou zařízení připojená k počítači. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení přijímat aktualizace softwaru bez připojení k počítači.
- **Omezení sledování služby AD**: **limit** zakáže identifikátor inzerce zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém ponechat povolený.
- **Vztah důvěryhodnosti pro podnikovou aplikaci**: **blok** **odebere v nastavení** > obecné > profily & správu zařízení na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby důvěřovali aplikacím, které nebyly staženy z App Storu.
- **Blokovat klipy aplikací**: **Ano** blokovat klipy aplikací na spravovaných zařízeních. Konkrétně nastavení na **hodnotu Ano**:

  - Zabrání uživatelům přidávat na zařízení klipy aplikací.
  - Odebere existující klipy aplikací na zařízeních.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidávat a odebírat klipy aplikací na zařízeních.

  Tato funkce platí pro:  
  - iOS 14,0 a novější
  - iPadOS 14,0 a novější

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Úprava nastavení odesílání**diagnostických informací: **blok** brání uživatelům ve změně nastavení odesílání diagnostiky a analýzy aplikací v části **Diagnostika a použití** (nastavení zařízení). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit tato nastavení zařízení.

  Chcete-li použít toto nastavení, nastavte nastavení **sdílet data o využití** pro **blokování**.

  Tato funkce platí pro:  
  - iOS 9.3.2 a novější
  - iPadOS 13,0 a novější

- **Sledování vzdálené obrazovky podle aplikace v učebně**: **blok** brání aplikaci učebny vzdáleně zobrazit obrazovku na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém aplikaci Apple učebně dovolit zobrazit obrazovku.

  Chcete-li použít toto nastavení, nastavte nastavení **zachycení obrazovky** na **blokovat**.

  Tato funkce platí pro:  
  - iOS 9,3 – iOS 12. x: vyžaduje zařízení pod dohledem
  - iOS 13,0 a novější: nevyžaduje zařízení pod dohledem
  - iPadOS 13,0 a novější: zařízení musí být zaregistrovaná pomocí zápisu zařízení nebo automatického zápisu zařízení (ADE).

- **Sledování obrazovky s nezodpovězenými obrazovkami podle aplikace učebny**: **Povolit** umožní učitelům tiše sledovat obrazovky iOS/iPadOS v studentech pomocí aplikace učebny bez vědomí studentů. Studentská zařízení zaregistrovaná ve třídě pomocí aplikace učebny automaticky poskytnou oprávnění učiteli tohoto kurzu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit této funkci.

  Chcete-li použít toto nastavení, nastavte nastavení **zachycení obrazovky** na **blokovat**.

- **Změna účtu**: **blok** znemožní uživatelům aktualizovat nastavení specifická pro zařízení z aplikace nastavení pro iOS/iPadOS. Například uživatelé nemůžou vytvářet nové účty zařízení nebo měnit uživatelské jméno nebo heslo. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit tato nastavení změnit.

  Tato funkce se vztahuje také na nastavení přístupná z aplikace nastavení pro iOS/iPadOS, jako je pošta, kontakty, kalendář, Twitter a další. Tato funkce se nevztahuje na aplikace s nastaveními účtu, která se nedají konfigurovat z aplikace nastavení pro iOS/iPadOS, jako je například aplikace Microsoft Outlook.

- **Čas obrazovky**: **zablokování** uživatelům zabránit v nastavení vlastních omezení na čase obrazovky (nastavení zařízení). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízeních nakonfigurovali omezení zařízení (například Rodičovská kontrola nebo obsah a omezení ochrany osobních údajů).

  Toto nastavení bylo přejmenováno z **možnosti Povolit omezení v nastavení zařízení**. Dopad této změny:  
  
  - iOS 11.4.1 a starší: **blok** zabraňuje uživatelům v nastavení zařízení v nastavení vlastních omezení. Chování je stejné. a neexistují žádné změny pro uživatele.
  - iOS 12,0 a novější: **blok** zabraňuje uživatelům v nastavení zařízení nastavit vlastní **čas obrazovky** (nastavení > obecné > čas obrazovky), včetně omezení obsahu a ochrany osobních údajů. V zařízeních upgradovaných na iOS 12,0 se už v nastavení zařízení nezobrazí karta omezení (nastavení > obecné > Správa zařízení > > omezení profilu správy. Tato nastavení se nacházejí v **čase obrazovky**.
  
- **Použití možnosti pro vymazání veškerého obsahu a nastavení na zařízení**: **blok** zabraňuje použití možnosti pro vymazání veškerého obsahu a nastavení na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém poskytnout uživatelům přístup k těmto nastavením.
- **Úprava názvu zařízení**: **blok** znemožňuje změnu názvu zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit název zařízení.
- **Úprava nastavení oznámení**: **blok** nepovoluje změnu nastavení oznámení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení oznámení o zařízení.
- **Úprava tapety**: **blok** brání v změně tapety. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízeních změnili tapetu.
- **Změny profilu konfigurace**: **blok** zabraňuje změnám profilu konfigurace na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit instalovat konfigurační profily.
- **Zámek aktivace**: **Povolit** povolí zámek aktivace na zařízeních s iOS/iPadOS pod dohledem. Zámek aktivace znemožňuje opětovné aktivaci ztraceného nebo odcizeného zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Blokovat odebrání aplikace**: **blok** zabraňuje odebrání aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit odebrat aplikace ze zařízení.
- **Povolí příslušenství USB, když je zařízení zamknuté**: **umožňuje dovolit** , aby data Exchange příslušenství USB byla na zařízeních, která jsou zablokovaná po celou hodinu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém na zařízeních pravděpodobně neaktualizuje režim omezený na USB a příslušenství USB blokuje přenos dat ze zařízení, pokud jsou po dobu po celou hodinu uzamčena.

  Tato funkce platí pro:  
  - iOS/iPadOS 11.4.1 a novější

- **Vynutit automatické datum a čas**: **vyžaduje** , aby zařízení pod dohledem, aby automaticky nastavila datum &ho času. Časové pásmo zařízení se aktualizuje, když má zařízení mobilní připojení nebo má Wi-Fi s povolenými službami zjišťování polohy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Vyžadovat, aby studenti požádali o oprávnění k opuštění kurzu učebnosti**: **vyžadovat** , aby studenti zaregistrovaní v nespravovaném kurzu pomocí aplikace učeben požádali o oprávnění od učitelů k opuštění tohoto kurzu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vynutit, aby student požádal o oprávnění.

  Tato funkce platí pro:  
  - iOS 11,3 a novější
  - iPadOS 13,0 a novější

- **Povolit učebně zamknout aplikaci a uzamknout zařízení bez zobrazení výzvy**: **Povolit** umožní učitelům uzamknout aplikace nebo zamknout zařízení pomocí aplikace učebny bez vyzvání studenta. Uzamykání aplikací znamená, že zařízení mají přístup jenom k aplikacím určeným pro učitele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit učitelům v uzamykání aplikací nebo zařízení pomocí aplikace učebny bez vyzvání studenta.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Automaticky připojovat třídy učeben bez výzvy k zadání**: **Povolit** automaticky umožňuje studentům připojit se ke třídě, která je v aplikaci učebny, bez nutnosti zobrazit dotaz na učitele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém požádat učitele, že studenti chtějí připojit ke třídě, která je v aplikaci učeben.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Blokovat vytvoření sítě VPN**: **blok** zabraňuje uživatelům v vytváření nastavení konfigurace sítě VPN. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožnit uživatelům vytvářet v zařízeních sítě VPN.
- **Úprava nastavení eSIM**: **blok** zabraňuje odebrání nebo přidání plánu mobilního telefonu do eSIM karty na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit tato nastavení změnit.

  Tato funkce platí pro:  
  - iOS 12,1 a novější
  - iPadOS 13,0 a novější

- **Odložení aktualizací softwaru**: **možnost Povolit** umožňuje zpozdit, kdy se na zařízeních zobrazí aktualizace softwaru, od 0-90 dnů. Toto nastavení neřídí, kdy jsou aktualizace nebo nejsou nainstalovány.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém v zařízeních zobrazovat aktualizace softwaru, když je společnost Apple vydává. Například pokud se aktualizace pro iOS/iPadOS uvolní od společnosti Apple k určitému datu, tato aktualizace se přirozeně zobrazuje na zařízeních v datu vydání verze.  

  - **Zpoždění viditelnosti aktualizací softwaru**: zadejte hodnotu od 0-90 dnů. Po vypršení zpoždění se uživatelům zobrazí oznámení o aktualizaci na nejstarší verzi operačního systému, která je k dispozici při aktivaci zpoždění.

    Pokud je například iOS 12. a k dispozici **1. ledna**a je **zpoždění viditelnosti** nastaveno na **5 dní**, pak iOS 12. a není zobrazeno jako dostupná aktualizace na uživatelských zařízeních. Po **šestém dni** od vydání je tato aktualizace dostupná a uživatelé ji můžou nainstalovat.

    Tato funkce platí pro:  
    - iOS 11,3 a novější
    - iPadOS 13,0 a novější

## <a name="password"></a>Heslo

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Heslo**: **vyžaduje** , aby uživatelé zadali heslo pro přístup k zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přístup k zařízením bez zadání hesla.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

> [!IMPORTANT]
> Pokud u zařízení zaregistrovaných uživatelem nakonfigurujete nastavení hesla, budou jednoduchá nastavení **hesla** automaticky nastavená tak, aby se **zablokovala**, a bude vynucený kód PIN s 6 číslicemi.
>
> Například nakonfigurujete nastavení **vypršení platnosti hesla** a tuto zásadu nahrajete do zařízení zaregistrovaných uživatelem. V zařízeních dojde k následujícímu:
>
> - Nastavení **vypršení platnosti hesla** je ignorováno.
> - Jednoduchá hesla, například `1111` nebo `1234` , nejsou povolena.
> - Je vynutil kód PIN pro číslice 6.

- **Jednoduchá hesla**: **blok** vyžaduje složitější hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat jednoduchá hesla, například `0000` a `1234` .

- **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla, kterou vaše organizace vyžaduje. Možnosti:
  - **Výchozí ze zařízení**
  - **Číselná**: heslo musí obsahovat jenom čísla, třeba 123456789.
  - **Alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice.

  > [!NOTE]
  > Výběr alfanumerických může mít vliv na spárované Apple Watch. Další informace najdete v tématu [Nastavení omezení hesla pro Apple Watch](https://support.apple.com/HT204953) (otevře web společnosti Apple).

- **Počet nealfanumerických znaků v hesle**: zadejte počet znaků symbolu, například `#` nebo `@` , které musí heslo obsahovat, od 1-4. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

- **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4-16 znaků. Do zařízení zaregistrovaných uživatelem zadejte délku 4 až 6 znaků.
  
  > [!NOTE]
  > U zařízení, která jsou zaregistrovaná uživatelem, můžou uživatelé nastavit PIN kód o více než 6 číslic. Ale na zařízeních se neuplatní více než 6 číslic. Správce například nastaví minimální délku na `8` . U zařízení zaregistrovaných uživatelem se uživatelům vyžaduje jenom zadání kódu PIN pro 6 číslic. Intune nevynutí na uživatelem zaregistrovaná zařízení kód PIN delší než 6 číslic.

- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet neúspěšných přihlášení, než se zařízení vymaže, od 2-11. Nedoporučuje se tuto hodnotu nastavit na `2` nebo `3` . Je velmi běžné zadat chybné heslo. Vymazání zařízení po dvou nebo třech nesprávných pokusech o zadání hesla se často stává. Doporučuje se nastavit tuto hodnotu aspoň na `4` . 
  
  iOS/iPadOS má integrované zabezpečení, které může mít vliv na toto nastavení. Například iOS/iPadOS může zpozdit spuštění zásady v závislosti na počtu neúspěšných přihlášení. Může také zvážit opakované zadání stejného hesla jako jednoho pokusu. [Příručka zabezpečení iOS/iPadOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) společnosti Apple (Otevírá web společnosti Apple) je dobrým prostředkem a poskytuje konkrétnější údaje o heslech. 
  
- **Maximální počet minut po uzamčení obrazovky, po kterém se vyžaduje zadání hesla**<sup>1</sup>: zadejte, jak dlouho mají zařízení zůstat nečinné, než uživatelé musí znovu zadat heslo. Pokud je čas, který zadáte, delší dobu, než je aktuálně nastaveno na zařízení, zařízení bude ignorovat čas, který zadáte.

  Tato funkce platí pro:  
  - iOS 8.0 +
  - iPadOS 13.0 +

- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**<sup>1</sup>: zadejte maximální počet minut nečinnosti povolený na zařízeních, dokud se obrazovka nezamkne.

  **Možnosti iOS/iPadOS**:  

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Okamžitě**: po 30 sekundách nečinnosti se zamkne obrazovka.
  - **1**: obrazovka se zamkne po 1 minutách nečinnosti.
  - **2**: obrazovka se zamkne po 2 minutách nečinnosti.
  - **3**: obrazovka se zamkne po 3 minutách nečinnosti.
  - **4**: obrazovka se zamkne po 4 minutách nečinnosti.
  - **5**: obrazovka se zamkne po 5 minutách nečinnosti.

  **iPadOS možnosti**:  

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Okamžitě**: po 2 minutách nečinnosti se zamkne obrazovka.
  - **2**: obrazovka se zamkne po 2 minutách nečinnosti.
  - **5**: obrazovka se zamkne po 5 minutách nečinnosti.
  - **10**: po 10 minutách nečinnosti se zamkne obrazovka.
  - **15**: po 15 minutách nečinnosti se zamkne obrazovka.

  Pokud se hodnota nevztahuje na iOS a iPadOS, pak Apple používá nejbližší *nejnižší* hodnotu. Pokud například zadáte `4` minuty, zařízení iPadOS budou používat `2` minuty. Pokud zadáte `10` minuty, zařízení s iOS budou používat `5` minuty. Toto chování je omezení Apple.
  
  > [!NOTE]
  > Uživatelské rozhraní Intune pro toto nastavení nedělí podporované hodnoty pro iOS a iPadOS. Uživatelské rozhraní může být v budoucí verzi aktualizováno.

- **Vypršení platnosti hesla (dny)**: zadejte počet dní, než bude nutné změnit heslo zařízení, od 1-65535.
- **Zakázat opakované použití předchozích hesel**: pomocí tohoto nastavení můžete uživatelům zabránit ve vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Zadejte například hodnotu 5, aby uživatelé nemohli nastavit nové heslo, nebo některá z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Dotykové ID a odemknutí ID obličeje**: **blok** zabraňuje použití otisku prstu nebo obličeje k odemknutí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit odemknout zařízení pomocí biometrika.

  Blokování tohoto nastavení také zabrání použití ověřování FaceID k odemknutí zařízení.

  ID obličeje platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Úprava hesla**: **blok** zabrání změně, přidání nebo odebrání hesla. Po blokování této funkce se změny v omezeních hesla na zařízeních pod dohledem ignorují. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidat, změnit nebo odebrat hesla.

  - **Úprava Touch ID a ID obličeje**: **blok** přestane uživatelům měnit, přidávat nebo odebírat otisky prstů TouchID a ID obličeje. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit aktualizovat otisky prstů TouchID a ID obličeje na zařízeních.

    Blokování tohoto nastavení také zabrání uživatelům v změně, přidávání nebo odebírání ověřování FaceID.

    ID obličeje platí pro:  
    - iOS 11,0 a novější
    - iPadOS 13,0 a novější

- **Blokovat automatické vyplňování hesla**: **blok** zabraňuje použití funkce automatického vyplňování hesel v systému iOS/iPadOS. Výběr **bloku** má také následující dopad:

  - Uživatelům se nezobrazí výzva k použití uloženého hesla v Safari nebo ve všech aplikacích.
  - Automatická silná hesla jsou zakázaná a silná hesla se uživatelům nedoporučují.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto funkce dovolit.

- **Zablokovat žádosti o blízkost k heslům**: **blok** znemožní zařízením vyžadovat hesla z okolních zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto požadavky na heslo způsobit.
- **Blokování sdílení hesel**: **blok** zabraňuje sdílení hesel mezi zařízeními pomocí přetažení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat sdílení hesel.
- **Pro automatické vyplňování informací o heslech nebo informace o kreditních kartách vyžadovat ověření dotykového ID nebo ID obličeje**: **vyžaduje** , aby se uživatelé k ověřování pomocí TouchID nebo FaceID mohli v Safari a dalších aplikacích vyplňovat hesla nebo informace o kreditních kartách. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit tuto funkci řídit v nastavení zařízení.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější
  
<sup>1</sup> když nakonfigurujete **maximální počet minut nečinnosti** , po kterém se zamkne obrazovka a **maximální počet minut po uzamčení obrazovky, když se bude vyžadovat nastavení hesla** , uplatní se v uvedeném pořadí. Pokud například nastavíte hodnotu pro obě nastavení na **5** minut, obrazovka se vypne automaticky po pěti minutách a zařízení se po dalších pět minutách zamkne. Pokud ale uživatelé obrazovku vypnou ručně, druhé nastavení se okamžitě použije. Ve stejném příkladu po vypnutí obrazovky uživatelem zařízení zamkne pět minut později.

## <a name="locked-screen-experience"></a>Prostředí zamknuté obrazovky

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Přístup k řídicímu centru při uzamčeném zařízení**: **blok** zabraňuje přístupu k aplikaci řídicího centra, když je zařízení zamčené. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při zamčení zařízení dovolit přístup k aplikaci řídicího centra.
- **Oznámení, když je zařízení uzamčené**: **blok** zabrání přístupu k oznámením, když jsou zařízení zamčená. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit přístup k oznámením bez odemknutí zařízení.
- **Zobrazení dnes, když je zařízení uzamčené**: **blok** znemožní přístup k zobrazení dnes, když jsou zařízení zamčená. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit zobrazit zobrazení dnes, když jsou zařízení zamčená.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Oznámení kapesního zařízení, když je zařízení uzamčené**: **blok** brání přístupu k aplikaci peněženky, když jsou zařízení zamčená. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při zamčení zařízení dovolit přístup k aplikaci peněženky.

## <a name="app-store-doc-viewing-gaming"></a>App Store, zobrazování dokumentů, hraní her

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Zobrazení firemních dokumentů v nespravovaných aplikacích**: **blok** zabraňuje zobrazení firemních dokumentů v nespravovaných aplikacích. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit podnikové dokumenty v libovolné aplikaci.

  Například chcete zabránit uživatelům v ukládání souborů z aplikace OneDrive do Dropboxu. Nakonfigurujte toto nastavení jako **blok**. Jakmile zařízení dostanou zásadu (například po restartování), už neumožňuje uložení.

  > [!NOTE]
  > Pokud je toto nastavení blokované, zablokují se taky klávesnice třetích stran nainstalované z App Storu.

  - **Povolení čtení nespravovaných aplikací ze spravovaných účtů kontaktů**: **Povolení** umožňuje nespravovaným aplikacím, jako je integrovaná aplikace pro iOS nebo iPadOS, číst a přistupovat k kontaktním informacím ze spravovaných aplikací, včetně mobilní aplikace Outlook. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit čtení, včetně odebrání duplicit, z integrované aplikace kontaktů na zařízeních.  
  
    Toto nastavení povoluje nebo znemožňuje čtení kontaktních informací. Neřídí synchronizaci kontaktů mezi aplikacemi.
  
    Pokud chcete použít toto nastavení, nastavte možnost **zobrazení firemních dokumentů v nespravovaných aplikacích** na **blokovat**.

  Další informace o těchto dvou nastaveních a jejich dopad na Outlook pro iOS/iPadOS kontaktování exportu najdete v tématu [Podpora tipů: použití nastavení vlastního profilu Intune s aplikací pro nativní kontakty iOS/iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- Považovat postupné **přetažení jako nespravovaného cíle**: **vyžadovat** , aby se přetažení považovalo za nespravovaný cíl přetažení. Zastaví spravované aplikace z odesílání dat pomocí přetažení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Zobrazení nefiremních dokumentů v podnikových aplikacích**: **blok** zabraňuje zobrazení nefiremních dokumentů v podnikových aplikacích. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat zobrazení libovolného dokumentu v podnikových spravovaných aplikacích.

  **Blok** také brání synchronizaci exportu kontaktů v Outlooku pro iOS/iPadOS. Další informace najdete v tématu [Podpora tipů: povolení aplikace Outlook pro iOS/IPadOS synchronizace kontaktů s ovládacími prvky](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453)správy mobilních zařízení (MDM) iOS12.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Vyžadovat heslo pro iTunes Store pro všechny nákupy**: **vyžadovat** , aby uživatelé zadali heslo Apple ID pro každý nákup v aplikaci nebo iTunes. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vyžadovat nákupy bez výzvy k zadání hesla pokaždé, když.
- **Nákupy v aplikaci**: **blok** brání nákupům v aplikaci ze Storu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém v rámci spuštěné aplikace dovolit nákupy do Storu.
- **Stáhnout obsah z obchodu iBooks Store označeného jako ' Erotika '**: **Block** znemožní uživatelům stahovat média z obchodu iBooks úložiště, které je označeno jako erotika. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit stahovat knihy s kategorií "Erotika".
- **Povolení spravovaných aplikací pro psaní kontaktů na nespravované účty kontaktů**: **Povolení** umožňuje spravovaným aplikacím, jako je mobilní aplikace Outlook, ukládat nebo synchronizovat kontaktní informace, včetně obchodních a firemních kontaktů, do integrované aplikace pro iOS/iPadOS Contacts. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit tomu, aby spravované aplikace ukládaly nebo synchronizovaly kontaktní informace na vestavěnou aplikaci pro iOS/iPadOS Contacts na zařízeních.
  
  Pokud chcete použít toto nastavení, nastavte možnost **zobrazení firemních dokumentů v nespravovaných aplikacích** na **blokovat**.

- **Oblast hodnocení**: Vyberte oblast hodnocení, kterou chcete použít pro povolené soubory ke stažení. A pak vyberte povolené hodnocení **filmů**, **televizních**pořadů a **aplikací**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **App Store**: **blok** zabrání přístupu k obchodu s aplikacemi na zařízeních pod dohledem. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

  - **Instalace aplikací z App Storu**: **blok** nezobrazuje obchod s aplikacemi na domovské obrazovce zařízení. Uživatelé můžou k instalaci aplikací dál používat iTunes nebo Apple Configuratoru. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na domovské obrazovce dovolit obchod s aplikacemi.
  - **Automatické stahování aplikací**: **blok** znemožňuje automatické stahování aplikací zakoupených na jiných zařízeních a automatické aktualizace nových aplikací. Nemá vliv na aktualizace existujících aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízení nakoupené aplikace na jiných zařízeních s iOS/iPadOS dovolit, aby si stáhli a aktualizovali.

- **Explicitní obsah v hudbě, podcastech nebo zprávách v iTunes**: **blok** zabraňuje explicitnímu obsahu iTunes v hudbě, podcastech nebo zprávách. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení dovolit přístup k obsahu, který je hodnocen jako dospělý ze Storu.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Přidání Game Center přátelé**: **blok** zabraňuje uživatelům v přidávání Game Centerch přátel. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přidat přátele do Game Center.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Game Center**: **zablokujte** pomocí aplikace Game Center. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při použití aplikace Game Center na zařízeních použít.
- **Hry pro více hráčů**: **blok** zabraňuje hraní her s více hráči. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit hraní her pro více hráčů na zařízeních.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Přístup k síťové jednotce v aplikaci soubory**: použití protokolu SMB (Server Message Block), zařízení mají přístup k souborům nebo jiným prostředkům na síťovém serveru. Při **vypnutí** se zabrání přístupu k souborům na síťové jednotce SMB. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="built-in-apps"></a>Integrované aplikace

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Siri**: **Block** znemožní přístup k Siri. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních používat Siri hlasového asistenta.
  - **Siri, když je zařízení uzamčené**: **blok** znemožní přístup k Siri, když jsou zařízení zamčená. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při zamčení na zařízeních používat Siri hlasového pomocníka.

- **Upozornění na podvod v Safari**: **vyžaduje** zobrazení upozornění na podvod ve webovém prohlížeči na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci zakázat.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)


- **Vyhledávání Spotlightu, které vrátí výsledky z Internetu**: **blok** přestane vracet žádné výsledky z internetu hledání. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožnit vyhledávání Spotlightem připojení k Internetu a poskytnout tak výsledky hledání.

  Toto nastavení je duplikováno v uživatelském rozhraní a bude opraveno v nadcházející verzi. V současné době toto nastavení platí pro zařízení pod dohledem. V budoucí verzi toto nastavení platí pro zařízení zaregistrovaná a automatizovaná zaregistrovaná zařízení a nevyžadují dohled.

- **Soubory cookie Safari**: vyberte, jak se soubory cookie zpracovávají na zařízeních. Možnosti:
  - Povolit
  - Blokovat všechny soubory cookie
  - Povolení souborů cookie z navštívených webů
  - Povoluje soubory cookie z aktuálního webu

- **Safari JavaScript**: **blok** zabraňuje spuštění skriptů Java v prohlížeči v zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat skripty Java.

- **Automaticky otevíraná okna Safari**: **blokovat** blokuje všechna automaticky otevíraná okna ve webovém prohlížeči Safari. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém dovolit blokování automaticky otevíraných oken.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Kamera**: **Block** zabrání přístupu k fotoaparátu na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k kameře zařízení.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

  - **FaceTime**: **Block** znemožní přístup k aplikaci FaceTime. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních dovolit přístup k aplikaci FaceTime.

    Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Filtr vulgárních výrazů v Siri**: **vyžadovat, aby** Siri nemohlo diktovat nebo diktovat vulgární jazyk. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Chcete-li použít toto nastavení, nastavte nastavení **Siri** na **blokovat**.

  Tato funkce platí pro:  
  - iOS 11,0 a novější

- **Siri dotazování na uživatelem generovaný obsah z Internetu**: **blok** zabraňuje tomu, aby Siri přístup k webům, aby mohla odpovídat na otázky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat Siri přístupu k obsahu generovanému uživateli z Internetu.

  Chcete-li použít toto nastavení, nastavte nastavení **Siri** na **blokovat**.

- **Apple News**: **blok** brání v přístupu k aplikaci Apple News na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace Apple News.
- **iBooks Store**: **blok** znemožní přístup k úložišti iBooks. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit Procházet a kupovat knihy z iBooks Storu.
- **Aplikace zprávy na zařízení**: **blok** zabraňuje uživatelům v používání aplikace zprávy pro iMessage. Pokud zařízení podporují textové zasílání zpráv, můžou uživatelé dál odesílat a přijímat textové zprávy pomocí SMS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace zprávy k posílání a čtení zpráv přes Internet.
- **Podcasty**: **blokování** brání uživatelům v použití aplikace Podcasty. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace Podcasty.
- **Hudební služba**: **blok** vrátí aplikaci v hudbě do klasického režimu a zakáže hudební službu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace Apple Music.
- **služba iTunes Radio Service**: **blok** zabraňuje použití aplikace iTunes Radio. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace iTunes Radio.
- **iTunes Store**: **blok** zabraňuje použití iTunes na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat iTunes.

  Tato funkce platí pro:  
  - iOS 4,0 a novější
  - iPadOS 13,0 a novější

- **Najít iPhone**: **blok** brání této funkci v aplikaci najít moji. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém pomocí této funkce najít moji aplikaci získat přibližnou polohu zařízení.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

- **Najít přátele**: **blok** brání této funkci v aplikaci najít moji. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém pomocí této funkce najít moji aplikaci najít rodinu a přátele ze zařízení Apple nebo iCloud.com.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

- **Změny v nastavení aplikace Find My Friends**: **Block** zabraňuje změnám v nastavení aplikace Find My Friends. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit měnit nastavení aplikace najít přátele.

- **Vyhledávání Spotlightu, které vrátí výsledky z Internetu**: **blok** přestane vracet žádné výsledky z internetu hledání. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožnit vyhledávání Spotlightem připojení k Internetu a poskytnout tak výsledky hledání.

  Toto nastavení je duplikováno v uživatelském rozhraní a bude opraveno v nadcházející verzi. V současné době toto nastavení platí pro zařízení pod dohledem. V budoucí verzi toto nastavení platí pro zařízení zaregistrovaná a automatizovaná zaregistrovaná zařízení a nevyžadují dohled.

- **Blokovat odebrání systémových aplikací ze zařízení**: **blok** zakáže možnost odebrat systémové aplikace ze zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit odebrat systémové aplikace.

- **Safari**: **zablokujte blokování** pomocí prohlížeče Safari na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit používat prohlížeč Safari.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Automatické vyplňování prohlížeče Safari**: **blok** zakáže funkci automatického vyplňování v prohlížeči Safari na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení automatického dokončování ve webovém prohlížeči.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

## <a name="restricted-apps"></a>Omezené aplikace

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Typ seznamu omezených aplikací**: vytvoří seznam aplikací, které uživatelé nemůžou instalovat ani používat. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém umožňovat přístup k aplikacím, které přiřadíte, a integrovaným aplikacím.
  - **Zakázané aplikace**: seznam aplikací (nespravovaných pomocí Intune), které uživatelé nemůžou instalovat a spouštět. Uživatelům není instalace zakázané aplikace znemožněna. Pokud uživatel z tohoto seznamu nainstaluje aplikaci, zařízení se nahlásí v sestavě **zařízení s omezenými aplikacemi** (zařízení[centra pro správu Správce koncových bodů](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Devices**  >  **monitorují**  >  **zařízení s omezenými aplikacemi**). 
  - **Schválené aplikace**: seznam aplikací, které můžou uživatelé instalovat. Aby bylo možné zachovat dodržování předpisů, uživatelé nesmí instalovat jiné aplikace. Aplikace spravované přes Intune se automaticky povolují, včetně aplikace Portál společnosti. Uživatelům není znemožněna instalace aplikace, která není na seznamu schválených. Pokud tomu tak je, nahlásí se v Intune.

Pokud chcete do těchto seznamů přidat aplikace, můžete:

- **Přidejte** adresu URL obchodu iTunes pro aplikaci, kterou chcete. Pokud například chcete přidat aplikaci Microsoft work folders, zadejte `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` nebo `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` .

  Pokud chcete najít adresu URL aplikace, otevřete aplikaci iTunes App Store a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop` nebo `Microsoft Word` . Vyberte aplikaci a zkopírujte adresu URL.

  K vyhledání aplikace můžete také použít iTunes a potom pomocí úlohy **Kopírovat odkaz** získat adresu URL aplikace.

- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app url>, <app name>, <app publisher>`. Případně **exportujte** existující seznam obsahující seznam aplikací s omezeným přístupem ve stejném formátu.

> [!IMPORTANT]
> Profily zařízení, které používají nastavení aplikací s omezeným přístupem, se musí přiřadit ke skupinám uživatelů.

## <a name="shared-ipad"></a>Sdílený iPad

Tato funkce platí pro:

- iPadOS 13,4 a novější
- Sdílený iPad

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Blokovat sdílené dočasné relace pro iPad**: dočasné relace umožňují uživatelům přihlašovat se jako host a uživatelé nemusejí zadávat spravované Apple ID nebo heslo.

  Při nastavení na **Ano**:

  - Uživatelé iPadu se sdílenými uživateli iPad nemůžou používat dočasné relace.
  - Uživatelé se musí k zařízení přihlásit pomocí spravovaného Apple ID a hesla.
  - Možnost účet hosta není na zařízeních zobrazená na zamykací obrazovce.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém umožňuje sdílenému uživateli iPad přihlásit se k zařízení pomocí účtu Guest. Když se uživatel odhlásí, žádná z dat uživatele se neuloží ani nesynchronizuje do iCloud.

## <a name="show-or-hide-apps"></a>Zobrazit nebo skrýt aplikace

Tato funkce platí pro:

- iOS 9,3 a novější
- iPadOS 13,0 a novější

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Typ seznamu aplikací**: Vytvořte seznam aplikací, které chcete zobrazit nebo skrýt. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094). Možnosti:

  - **Skryté aplikace**: Zadejte seznam aplikací, které jsou pro uživatele skryté. Uživatelé nemůžou tyto aplikace zobrazit ani otevřít.
  
    Apple znemožní skrývání některých nativních aplikací. Nemůžete třeba na zařízení skrýt aplikaci **Nastavení** . [Odstranění integrovaných aplikací Apple](https://support.apple.com/HT208094) zobrazí seznam aplikací, které se dají skrýt.
  
  - **Viditelné aplikace**: Zadejte seznam aplikací, které uživatelé mohou zobrazit a spustit. Žádné jiné aplikace nebude možné zobrazit ani spustit.

- **Adresa URL aplikace**: zadejte adresu URL aplikace pro Store aplikace, kterou chcete zobrazit nebo skrýt. Příklad:

  - Pokud chcete přidat aplikaci Microsoft work folders, zadejte `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` nebo `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` . 

  - Chcete-li přidat aplikaci Microsoft Word, zadejte `https://itunes.apple.com/de/app/microsoft-word/id586447913` nebo `https://apps.apple.com/de/app/microsoft-word/id586447913` .

  Pokud chcete najít adresu URL aplikace, otevřete aplikaci iTunes App Store a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop` nebo `Microsoft Word` . Vyberte aplikaci a zkopírujte adresu URL.

  K vyhledání aplikace můžete také použít iTunes a potom pomocí úlohy **Kopírovat odkaz** získat adresu URL aplikace.

- **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Název aplikace**: zadejte název aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Vydavatel**: zadejte vydavatele aplikace, kterou chcete.

Pokud chcete přidat aplikace, můžete:

- **Přidat**: vyberte, pokud chcete vytvořit seznam aplikací.
- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app url>, <app name>, <app publisher>`. Případně můžete **exportovat** a vytvořit seznam aplikací s omezeným přístupem, které jste přidali, ve stejném formátu.

## <a name="wireless"></a>Bezdrátová síť

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Datový roaming**: **blokovat** znemožní datový roaming v mobilní síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat datový roaming, když je zařízení v mobilní síti.

  > [!IMPORTANT]
  > Toto nastavení se považuje za akci vzdáleného zařízení. Toto nastavení se proto nezobrazí v profilu správy na zařízeních. Pokaždé, když se v zařízení změní stav roamingu dat, služba Intune zablokuje **datový roaming** . Pokud se v Intune zobrazuje stav sestavy úspěch, pak víte, že funguje, i když se toto nastavení nezobrazí v profilu správy na zařízení.

- **Globální načítání na pozadí při roamingu**: při roamingu v mobilní síti znemožní **blokování** použití globální funkce načítání na pozadí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při roamingu v mobilní síti načítat data, jako jsou e-mailová zařízení.
- **Hlasové vytáčení**: **blok** zabraňuje použití funkce hlasového vytáčení na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat hlasové vytáčení na zařízeních.
- **Hlasový roaming**: **blok** zabraňuje hlasovému roamingu přes mobilní síť. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat hlasový roaming, když jsou zařízení v mobilní síti.
- **Osobní hotspot**: **blok** vypne osobní hotspot na zařízeních při každé synchronizaci zařízení. Toto nastavení nemusí být kompatibilní s některými provozovateli. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zachovat konfiguraci osobního hotspotu jako výchozí nastavené uživateli.

  > [!IMPORTANT]
  > Toto nastavení se považuje za akci vzdáleného zařízení. Toto nastavení se proto nezobrazí v profilu správy na zařízeních. Pokaždé, když se změní stav osobního hotspotu na zařízení, služba Intune zablokuje **osobní hotspot** . Pokud se v Intune zobrazuje stav sestavy úspěch, pak víte, že funguje, i když se toto nastavení nezobrazí v profilu správy na zařízení.

- **Pravidla pro mobilní použití (jenom spravované aplikace)**: **umožňuje** definovat datové typy, které spravované aplikace můžou používat při použití v mobilních sítích. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Možnosti:
  - **Zablokovat používání mobilních dat**: blokuje používání mobilních dat pro **všechny spravované aplikace** nebo umožňuje **zvolit konkrétní aplikace**.
  - **Zablokovat používání mobilních dat při roamingu**: při roamingu používejte mobilní data pro **všechny spravované aplikace** nebo **vyberte konkrétní aplikace**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Změny nastavení využití mobilních dat v aplikaci**: **blok** zabraňuje změnám v nastavení využití mobilních dat v aplikaci. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit řídit, které aplikace můžou používat mobilní data.
- **Změny nastavení plánu mobilních telefonů**: **blok** zabraňuje změně nastavení v plánu pro mobilní síť. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit provádění změn.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Změna osobního hotspotu**: **blokování** brání v změně nastavení osobního hotspotu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit povolit nebo zakázat osobní hotspot.

  Pokud zablokujete toto nastavení a zablokujete nastavení **osobní hotspotu** , bude osobní hotspot vypnutý.

  Tato funkce platí pro:  
  - iOS 12,2 a novější
  - iPadOS 13,0 a novější

- **Připojit se k sítím Wi-Fi jenom pomocí konfiguračních profilů**: **vyžaduje** , aby zařízení používala jenom sítě Wi-Fi nastavené prostřednictvím konfiguračních profilů Intune. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém dovolit zařízením používat jiné sítě Wi-Fi.

  Pokud je nastaveno na **vyžadovat**, ujistěte se, že má zařízení profil sítě Wi-Fi. Pokud nepřiřazujete profil sítě Wi-Fi, toto nastavení by mohlo zabránit tomu, aby se zařízení připojovala k Internetu. Jinými slovy, pokud je tento profil omezení zařízení přiřazen před profilem Wi-Fi, zařízení může být zablokované v připojení k Internetu.
  
  Pokud se nemůže připojit, zaregistrujte zařízení a pak ho znovu zaregistrujte pomocí profilu sítě Wi-Fi. Potom nastavte toto nastavení na **vyžadovat** v profilu omezení zařízení a přiřaďte k zařízení profil.

- **Wi-Fi vždycky zapnuté**: **vyžaduje** v aplikaci nastavení zachovat Wi-Fi. Nedá se vypnout v nastavení nebo v řídicím centru, a to ani v případě, že je zařízení v režimu v letadle. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit zapnout nebo vypnout Wi-Fi.

  Konfigurace tohoto nastavení nezabrání uživatelům v výběru sítě Wi-Fi.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="connected-devices"></a>Připojená zařízení

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Detekce zápěstí pro spárovaná Apple Watch**: **vyžaduje** , aby se u spárovaného Apple Watch použilo zjišťování zápěstí. V případě potřeby nebude Apple Watch zobrazovat oznámení, pokud se nepoužívá. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Vyžadovat párovací heslo pro odchozí požadavky AirPlay**: při použití AirPlay ke streamování obsahu do jiných zařízení Apple **vyžadovat** párování hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožňovat streamování obsahu pomocí AirPlay bez zadání hesla.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Přetažení**: **blok** zabraňuje použití přetahování na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít funkci přetažení, která umožňuje výměnu obsahu s okolními zařízeními.
- **Apple Watch párování**: **blok** brání párování s Apple Watch. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit párování zařízení s Apple Watch.
- **Úpravy Bluetooth**: **blok** zabraňuje uživatelům měnit nastavení Bluetooth na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit tato nastavení změnit.
- **Párování hostitelů pro řízení zařízení, se kterými se zařízení s iOS/iPadOS může spárovat**: **blok** zabraňuje párování hostitelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit párování hostitelů, aby správce mohl řídit, se kterými zařízeními se zařízení s iOS/iPadOS můžou spárovat.
- **Blokovat tisk**: **blok** zabraňuje použití funkce pro tisk v zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit použít postupné tisku.
  - **Blokovat úložiště přihlašovacích údajů pro tisk v řetězci klíčů**: **blok** zabraňuje použití úložiště řetězce klíčů pro uživatelské jméno a heslo na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém ukládat uživatelské jméno a heslo pro tisk do aplikace pro řetězce klíčů.
  - **Vyžadovat důvěryhodný certifikát TLS pro spolutisk**: **vyžaduje** , aby zařízení používala důvěryhodné certifikáty pro komunikaci tiskem TLS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Zablokovat blokovat iBeacon u rozpoznávání tiskových tiskáren**: **blok** zabraňuje škodlivým signálům přes útok Bluetooth v přenosu dat v síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních umožňovat reklamní tisk tiskáren.
- **Blokování nastavení nových okolních zařízení**: **blok** zakáže výzvu k nastavení nových zařízení, která jsou v okolí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolovat výzvy uživatelům, aby se připojili k jiným okolním zařízením Apple.

  Tato funkce platí pro:  
  - iOS 11,0 a novější
  - iPadOS 13,0 a novější

- **Přístup k souborům na jednotce USB**: zařízení se můžou připojit a otevírat soubory na USB jednotce. Pokud je zařízení USB připojené k zařízení, **zakažte zakázat** přístup zařízení k jednotce USB v aplikaci soubory. Zakázáním této funkce se taky znemožní uživatelům přenášet soubory na jednotku USB připojenou k iPadu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k jednotce USB v aplikaci Files.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="keyboard-and-dictionary"></a>Klávesnice a slovník

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Vyhledávání definic slov**: **blok** zabraňuje zvýraznění slova a následnému vyhledání jeho definice. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k funkci vyhledávání definic.
- **Prediktivní klávesnice**: **blok** zabraňuje použití prediktivních klávesnic, aby mohli navrhovat slova, která můžou uživatelé chtít. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.
- **Automatické opravy**: **blok** zabraňuje použití automatického opravy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení dovolit, aby automaticky opravila nesprávně napsaná slova.
- Kontrola **pravopisu klávesnice**: **blok** zabraňuje kontrole pravopisu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít kontrolu pravopisu.
- **Klávesové zkratky**: **blok** zabraňuje uživatelům v používání klávesových zkratek. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních používat klávesové zkratky.
- **Diktování**: **blok** zabrání uživatelům v použití hlasového vstupu k zadání textu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit použít vstup diktování.
- **QuickPath**: **blok** zabraňuje uživatelům v používání QuickPath. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit používat QuickPath, což umožňuje průběžný vstup na klávesnici zařízení. Uživatelé můžou k vytváření slov psát přetáhnutím prstem přes tyto klávesy.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

## <a name="cloud-and-storage"></a>Cloud a úložiště

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Šifrované zálohování**: **vyžaduje** , aby bylo zálohování zařízení nutné šifrovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Synchronizace spravovaných aplikací do cloudu**: **blok** brání aplikacím spravovaným v Intune synchronizovat data s uživatelským účtem iCloud. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém iCloud synchronizaci těchto dat.
- **Blokovat zálohování v podnikové knize**: **blok** znemožní zálohování podnikových knih. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit zálohovat tyto knihy.
- **Blokování synchronizace metadat v podnikovém adresáři (poznámky a zvýraznění)**: **blok** zabraňuje synchronizaci poznámek a světel v podnikových knihách. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Synchronizace datových proudů do iCloud**: **blok** zabraňuje synchronizaci streamování fotografií do iCloud. Blokování této funkce může způsobit ztrátu dat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit, **aby na svém zařízení povolil synchronizaci** na iCloud a aby byly na všech zařízeních uživatele dostupné fotky.
- **Knihovna fotografií iCloud**: **blok** zakáže použití knihovny fotografií iCloud k ukládání fotek a videí do cloudu. Ze zařízení se odeberou všechny fotky, které nejsou plně stažené z knihovny fotografií iCloud. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití knihovny fotografií iCloud.
- **Sdílený datový proud fotek**: **blok** zakáže **Sdílení fotek iCloud** na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat sdílené streamování fotografií.
- **Předání**: **Block** znemožní uživatelům spouštět práci na zařízení se systémem iOS/iPadOS a potom pokračovat v práci na jiném zařízení s iOS/iPadOS nebo MacOS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tento odkaz umožňovat.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Backup na iCloud**: **blok** zabrání uživatelům v zálohování zařízení do iCloud. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit zálohovat zařízení na iCloud.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Blokovat synchronizaci dokumentů iCloud**: **blok** zabraňuje tomu, aby iCloud Synchronization Documents and data. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci dokumentu a klíč-hodnota do iCloud prostoru úložiště.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

- **Blokovat synchronizaci řetězce klíčů iCloud**: **blok** zakáže synchronizaci přihlašovacích údajů uložených v řetězci klíčů do iCloud. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožňovat synchronizaci těchto přihlašovacích údajů.

  Od iOS/iPadOS 13,0 Toto nastavení vyžaduje zařízení pod dohledem.

## <a name="autonomous-single-app-mode-asam"></a>Autonomní režim jedné aplikace (ASAM)

Pomocí těchto nastavení můžete nakonfigurovat zařízení s iOS/iPadOS, aby spouštěla konkrétní aplikace v autonomním režimu jedné aplikace (ASAM). Pokud je nakonfigurováno co nejdříve a uživatelé spustí jednu z nakonfigurovaných aplikací, zařízení je v této aplikaci zamčené. Přepínání aplikace nebo úlohy je zakázané, dokud uživatelé neukončí povolenou aplikaci.

Aby se mohla konfigurace ASAM použít, uživatelé musí ručně otevřít konkrétní aplikaci. Tato úloha se vztahuje také na Portál společnosti aplikaci.

- Například ve škole nebo univerzitním prostředí přidejte aplikaci, která umožní uživatelům provést test na zařízení. Nebo zařízení uzamkněte do aplikace Portál společnosti, dokud se uživatel neověří. Pokud jsou akce aplikace dokončené uživateli nebo pokud tuto zásadu odeberete, zařízení se vrátí do normálního stavu.

- Ne všechny aplikace podporují autonomní režim jedné aplikace. Pro vložení aplikace do ASAM se obvykle vyžadují ID sady prostředků nebo dvojice klíčových hodnot poskytované zásadami konfigurace aplikace. Další informace najdete v části [ `autonomousSingleAppModePermittedAppIDs` omezení](https://developer.apple.com/documentation/devicemanagement/restrictions) v dokumentaci k MDM společnosti Apple. Další informace o konkrétním nastavení požadovaném pro aplikaci, kterou konfigurujete, najdete v dokumentaci od dodavatele.

  Pokud třeba chcete nakonfigurovat místnosti lupy v autonomním režimu jedné aplikace, přiblížením říkáte, že se má použít `us.zoom.zpcontroller` ID sady prostředků. V této instanci provedete také změnu webového portálu zoom. Další informace najdete v centru pro [nápovědu lupy](https://support.zoom.us/hc/articles/360021322632-Autonomous-Single-App-Mode-for-Zoom-Rooms-with-a-Third-Party-MDM).

- V zařízeních se systémem iOS/iPadOS podporuje aplikace Portál společnosti ASAM. Když je aplikace Portál společnosti v ASAM, uživatelé musí aplikaci Portál společnosti otevřít ručně. Zařízení je pak uzamčené v aplikaci Portál společnosti, dokud se uživatel neověří. Když se uživatelé přihlásí k aplikaci Portál společnosti, můžou na zařízení používat jiné aplikace a tlačítko na domovské obrazovce. Když se odhlásí z aplikace Portál společnosti, zařízení se vrátí do režimu jedné aplikace a zamkne se v Portál společnosti aplikaci.

  Pokud chcete aplikaci Portál společnosti převést do aplikace pro přihlášení a odhlášení (Povolit ASAM), zadejte do těchto nastavení název Portál společnosti aplikace, jako `Microsoft Intune Company Portal` je, a ID sady ( `com.microsoft.CompanyPortal` ). Po přiřazení tohoto profilu musíte otevřít aplikaci Portál společnosti, abyste aplikaci zamkli, aby se uživatelé mohli přihlašovat a odhlásit. Aby se konfigurace ASAM mohla použít, musí uživatelé aplikaci Portál společnosti otevřít ručně.
  
  Když se odebere konfigurační profil zařízení a uživatel se odhlásí, zařízení není v aplikaci Portál společnosti uzamčené.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Název aplikace**: zadejte název aplikace, kterou chcete.
- **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace, kterou chcete.
- **Přidat**: vyberte, pokud chcete vytvořit seznam aplikací.

Soubor CSV můžete také **naimportovat** se seznamem názvů aplikací a jejich ID sady. Případně **exportujte** existující seznam obsahující aplikace.

## <a name="kiosk"></a>Kiosk

[Režim jedné aplikace](https://support.apple.com/guide/mdm/mdm80a981/web) se v Intune označuje jako celoobrazovkový režim.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- **Aplikace, která se má spustit v celoobrazovkovém režimu**: Vyberte typ aplikací, které chcete spustit v celoobrazovkovém režimu. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení operační systém nemusí použít nastavení veřejného terminálu. Zařízení neběží v celoobrazovkovém režimu.
  - **Aplikace ze Storu**: zadejte adresu URL aplikace v iTunes App Storu.
  - **Spravovaná aplikace**: vyberte aplikaci, kterou jste dříve přidali do Intune.
  - **Vestavěná aplikace**: zadejte [ID sady](bundle-ids-built-in-ios-apps.md) předdefinovaných aplikací.

- **Dotykové ovládání s asistencí**: **vyžaduje** nastavení usnadnění dotykového ovládání v zařízeních. Tato funkce pomáhá uživatelům s gesty na obrazovce, která by pro ně mohla být obtížná. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí spustit nebo povolit tuto funkci v celoobrazovkovém režimu.
- **Invertování barev**: **vyžaduje** nastavení usnadnění invertování barev, aby uživatelé s zrakovým postižením mohli obrazovku pro zobrazení změnit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí spustit nebo povolit tuto funkci v celoobrazovkovém režimu.
- **Mono zvuk**: **vyžaduje** , aby bylo na zařízeních nastaveno nastavení usnadnění Mono zvuk. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí spustit nebo povolit tuto funkci v celoobrazovkovém režimu.
- **Ovládání hlasu**: **vyžaduje** povolení ovládání hlasu na zařízeních a umožňuje uživatelům plně ovládat operační systém pomocí příkazů Siri. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zakázat ovládání hlasu.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější
  
  > [!TIP]
  > Pokud máte ve vaší organizaci k dispozici obchodní aplikace a nejsou v nich k dispozici **hlasové řízení** připravené na den 0 při vydání iOS 13,0, doporučujeme toto nastavení ponechat **nenakonfigurované**.

- **VoiceOver**: **vyžaduje** , aby nastavení usnadnění VoiceOver načetlo text na obrazovce. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí spustit nebo povolit tuto funkci v celoobrazovkovém režimu.
- **Zoom**: **vyžaduje** nastavení přiblížení, aby se uživatelé mohli přiblížit na obrazovku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí spustit nebo povolit tuto funkci v celoobrazovkovém režimu.
- **Auto Lock**: **Block** znemožňuje automatické uzamykání zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.
- **Přepínač vyzvánění**: **blok** zakáže přepínač vyzvánění (ztlumení) na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.
- **Otočení obrazovky**: **blok** zabraňuje změně orientace obrazovky, když uživatelé otáčí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.
- **Tlačítko režimu spánku obrazovky**: **blok** zakáže na zařízeních tlačítko probuzení z režimu spánku obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.
- **Dotyk**: **Block** zakáže dotykovou obrazovku na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit používat dotykovou obrazovku.
- **Tlačítka hlasitosti**: **blok** zabraňuje použití tlačítek hlasitosti na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat tlačítka hlasitosti.
- **Řízení dotykového**ovládání pro usnadnění **: umožňuje** uživatelům používat funkci usnadnění dotykového ovládání. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci zakázat.
- **Invertování barev ovládací prvek**: **Povolit** změnu barev barev, aby uživatelé mohli upravovat funkci invertování barev. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci zakázat.
- **Mluvit na vybraném textu**: **povolí** nastavení usnadnění výběru řeči na zařízeních. Tato funkce přečte text nahlas, který uživatelé vyberou. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci zakázat.
- **Úpravy hlasového ovládacího prvku**: **umožňuje** uživatelům změnit stav ovládacího prvku hlas na svých zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zablokovat uživatelům změnu stavu ovládání hlasu na svých zařízeních.

  Tato funkce platí pro:  
  - iOS 13,0 a novější
  - iPadOS 13,0 a novější

- **Ovládací prvek VoiceOver**: **Povolit** VoiceOver změny, aby uživatelé mohli aktualizovat funkci VoiceOver, jako je například způsob, jakým je rychlé čtení textu na obrazovce. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit VoiceOver změnám.
- **Ovládací prvek Lupa**: **povolí** změny přiblížení uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit změnám přiblížení.

> [!NOTE]
> Než budete moct nakonfigurovat zařízení se systémem iOS/iPadOS pro celoobrazovkový režim, musíte použít nástroj Apple Configuratoru nebo Apple Program registrace zařízení k umístění zařízení do režimu pod dohledem. Podívejte se na téma Příručka Apple na používání nástroje Apple Configuratoru.
> Pokud je aplikace pro iOS/iPadOS, kterou zadáte, nainstalovaná po přiřazení profilu, zařízení nepřejde do celoobrazovkového režimu, dokud se zařízení nerestartuje.

## <a name="domains"></a>Domény

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení, automatický zápis zařízení (pod dohledem)

- **Neoznačené e-mailové domény**  >  **Adresa URL e-mailové domény**: přidejte do seznamu jednu nebo víc adres URL. Když uživatelé dostanou e-mail z jiné domény než z domén, které zadáte, bude tento e-mail v aplikaci pro iOS/iPadOS pošty označený jako nedůvěryhodný.

- **Spravované webové domény**  >  **Adresa URL webové domény**; Přidejte do seznamu jednu nebo více adres URL. Po stažení dokumentů z domén, které zadáte, se považují za spravované. Toto nastavení platí jenom pro dokumenty stažené prostřednictvím prohlížeče Safari.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Nastavení platí pro: automatický zápis zařízení (pod dohledem)

- Domény pro automatické **vyplňování hesel v Safari**  >  **Adresa URL domény**: přidejte do seznamu jednu nebo více adres URL. Uživatelé si mohou uložit jenom webová hesla z adres URL uvedených v tomto seznamu. Toto nastavení platí jenom pro prohlížeč Safari a zařízení v režimu pod dohledem. Pokud nezadáte žádné adresy URL, bude možné ukládat hesla ze všech webů.

  Tato funkce platí pro:  
  - iOS 9,3 a novější
  - iPadOS 13,0 a novější

## <a name="settings-that-require-supervised-mode"></a>Nastavení, které vyžaduje režim pod dohledem

režim iOS/iPadOS pod dohledem se dá povolit jenom při počátečním nastavení zařízení prostřednictvím Program registrace zařízení společnosti Apple nebo pomocí Apple Configuratoru. Po povolení režimu pod dohledem může Intune v zařízení nakonfigurovat následující funkce:

- Celoobrazovkový režim (režim jedné aplikace): v [dokumentaci pro vývojáře Apple](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf)se říká "zámek aplikace".
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
- Novinky 
- Klávesové zkratky 
- Změny hesla 
- Změny názvu zařízení 
- Automatická stahování aplikací 
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
> - Přidat Game Center přátelé
> - Siri

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Na zařízeních [MacOS](device-restrictions-macos.md) můžete také omezit funkce a nastavení zařízení.
