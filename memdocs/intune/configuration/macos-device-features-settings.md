---
title: nastavení funkcí zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na nastavení pro konfiguraci zařízení macOS pro Protisk a přizpůsobení okna přihlášení k zobrazení nebo skrytí tlačítek napájení v Microsoft Intune. Podívejte se na postup, jak získat IP adresu, cestu a nastavení portu tiskového serveru v síti. Pomocí těchto nastavení můžete nakonfigurovat funkce zařízení macOS v profilu konfigurace zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83da63ef78d8b97cad47b811fee0cc3fde8a5502
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907451"
---
# <a name="macos-device-feature-settings-in-intune"></a>nastavení funkcí zařízení macOS v Intune

Intune obsahuje vestavěná nastavení pro přizpůsobení funkcí na zařízeních macOS. Správci můžou například přidat tiskárny pro průchozí tisk, zvolit způsob, jakým se uživatelé přihlásí, konfigurovat řízení spotřeby, používat ověřování pomocí jednotného přihlašování a další.

Pomocí těchto funkcí můžete řídit zařízení macOS jako součást řešení správy mobilních zařízení (MDM).

Tento článek uvádí tato nastavení a popisuje, co jednotlivé nastavení dělá. V této části najdete taky postup pro získání IP adresy, cesty a portu pro tiskárny pro práci na tiskárně pomocí Terminálové aplikace (emulátor). Další informace o funkcích zařízení najdete v pro [Přidání nastavení funkcí zařízení s iOS/iPadOS nebo MacOS](device-features-configure.md).

> [!NOTE]
> Uživatelské rozhraní nemusí odpovídat typům registrace v tomto článku. Informace v tomto článku jsou správné. Uživatelské rozhraní se aktualizuje v nadcházející verzi.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil funkcí zařízení MacOS](device-features-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace s některými nastaveními, která platí pro všechny možnosti registrace. Další informace o různých typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Cílení na tisk**: **přidejte** jednu nebo více tiskových tiskáren, které uživatelé můžou tisknout ze svých zařízení. Dále zadejte:
  - **Port** (iOS 11.0 +, iPadOS 13.0 +): zadejte port naslouchání cíle přenosu. Pokud necháte tuto vlastnost prázdnou, použije se při tisku výchozí port.
  - **IP adresa**: zadejte adresu IPv4 nebo IPv6 tiskárny. Zadejte například `10.0.0.1`. Pokud k identifikaci tiskáren používáte názvy hostitelů, můžete získat IP adresu pomocí příkazového testu tiskárny v aplikaci Terminal. Získat další podrobnosti najdete v [části IP adresa a cesta](#get-the-ip-address-and-path) (v tomto článku).
  - **Cesta**: zadejte cestu prostředku tiskárny. Cesta je typicky `ipp/print` pro tiskárny v síti. Získat další podrobnosti najdete v [části IP adresa a cesta](#get-the-ip-address-and-path) (v tomto článku).
  - **TLS** (iOS 11.0 +, iPadOS 13.0 +): vaše možnosti:
    - **Ne** (výchozí): protokol TLS (Transport Layer Security) se při připojování k tiskárnám tiskárny pro přenos na tiskárně neuplatňuje.
    - **Ano**: zabezpečuje připojení s využitím protokolu TLS (Transport Layer Security).

- **Importujte** textový soubor s oddělovači (. csv), který obsahuje seznam tiskáren pro průchozí tisk. Po přidání tiskáren pro tisk do Intune můžete také **exportovat** tento seznam.

### <a name="get-the-ip-address-and-path"></a>Získat IP adresu a cestu

Chcete-li přidat servery s modulem pro tisk, budete potřebovat IP adresu tiskárny, cestu k prostředku a port. Následující kroky ukazují, jak tyto informace získat.

1. Na Macu, který je připojený ke stejné místní síti (podsíti) jako tiskárny pro Protisk, otevřete **terminál** (z **/aplikace/Utility**).
2. V aplikaci Terminal App zadejte `ippfind` a vyberte Enter.

    Poznamenejte si informace o tiskárně. Například může vracet něco podobného jako `ipp://myprinter.local.:631/ipp/port1` . První část je název tiskárny. Poslední část ( `ipp/port1` ) je cesta prostředku.

3. V terminálu zadejte `ping myprinter.local` a vyberte Enter.

   Poznamenejte si IP adresu. Například může vracet něco podobného jako `PING myprinter.local (10.50.25.21)` .

4. Použijte hodnoty IP adresy a prostředku cesty. V tomto příkladu je IP adresa `10.50.25.21` a cesta k prostředku `/ipp/port1` .

## <a name="associated-domains"></a>Přidružené domény

V Intune můžete:

- Přidejte mnoho přidružení aplikace k doméně.
- Přidružte mnoho domén ke stejné aplikaci.

Tato funkce platí pro:

- macOS 10,15 a novější

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení schválená uživatelem a automatický zápis zařízení

- **Přidružené domény**: **přidejte** přidružení mezi vaší doménou a aplikací. Tato funkce sdílí přihlašovací údaje mezi aplikací contoso a webem společnosti Contoso. Dále zadejte:

  - **ID aplikace**: zadejte identifikátor aplikace, který se má přidružit k webu. Identifikátor aplikace zahrnuje ID týmu a ID sady: `TeamID.BundleID` .

    ID týmu je alfanumerické znaky (písmena a čísla) vygenerované společností Apple pro vývojáře aplikací, jako je například `ABCDE12345` . [Najít ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c)   (otevře web společnosti Apple) obsahuje další informace.

    ID sady prostředků jednoznačně identifikuje aplikaci a obvykle je ve formátu zpětného zápisu názvů domén. Například ID sady Finder je `com.apple.finder` . Pokud chcete najít ID sady, použijte AppleScript v terminálu:

    `osascript -e 'id of app "ExampleApp"'`

  - **Doména**: zadejte doménu webu, kterou chcete přidružit k aplikaci. Doména zahrnuje typ služby a plně kvalifikovaný název hostitele, jako je například `webcredentials:www.contoso.com` .

    Všechny subdomény přidružené domény můžete vyhledat zadáním `*.` (zástupný znak hvězdička a tečka) před začátkem domény. Období je povinné. Přesné domény mají vyšší prioritu než u domén se zástupnými znaky. Modely z nadřazených domén se tedy shodují, *Pokud* se shoda nenajde v plně kvalifikované subdoméně.

    Typ služby může být:

    - **authsrv**: rozšíření aplikace s jednotným přihlašováním
    - **applink**: Universal Link
    - **webcredentials**: Automatické vyplňování hesel

> [!TIP]
> Pokud chcete řešit potíže, otevřete na zařízení MacOS **profily Předvolby systému**  >  **Profiles**. Ověřte, že profil, který jste vytvořili, je v seznamu profily zařízení. Pokud je v seznamu uveden, ujistěte se, že je **Konfigurace přidružených domén** v profilu a obsahuje správné ID aplikace a domény.

## <a name="content-caching"></a>Ukládání obsahu do mezipaměti

Ukládání obsahu do mezipaměti ukládá místní kopii obsahu. Tyto informace mohou být načteny jinými zařízeními Apple bez připojení k Internetu. Toto ukládání do mezipaměti zrychluje stahování uložením aktualizací softwaru, aplikací, fotek a dalšího obsahu při prvním stažení. Vzhledem k tomu, že se aplikace stahují jednou a sdílí se s ostatními zařízeními, školám a organizacím s mnoha zařízeními šetří šířku pásma.

> [!NOTE]
> Pro tato nastavení použijte pouze jeden profil. Pokud s těmito nastaveními přiřadíte více profilů, dojde k chybě.
>
> Další informace o sledování ukládání obsahu do mezipaměti najdete v tématu [zobrazení protokolů a statistik ukládání obsahu do mezipaměti](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (otevření webu společnosti Apple).

Tato funkce platí pro:

- macOS 10.13.4 a novější

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

Další informace o těchto nastaveních najdete v tématu [nastavení datové části mezipaměti obsahu](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (otevření webu společnosti Apple).

**Povolit ukládání obsahu do mezipaměti**: **Ano** zapne ukládání obsahu do mezipaměti a uživatelé ho nemůžou zakázat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vypnout.

- **Typ obsahu, který se má ukládat do mezipaměti**: vaše možnosti:
  - **Veškerý obsah**: ukládá do mezipaměti obsah iCloud a sdílený obsah.
  - **Pouze obsah uživatele**: ukládá do mezipaměti obsah iCloud uživatele, včetně fotek a dokumentů.
  - **Pouze sdílený obsah**: ukládá do mezipaměti aplikace a aktualizace softwaru.

- **Maximální velikost mezipaměti**: zadejte maximální množství místa na disku (v bajtech), které se používá k ukládání obsahu do mezipaměti. Pokud necháte pole prázdné (výchozí), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém nastavit hodnotu nula ( `0` ) bajtů, která poskytuje neomezené místo na disku mezipaměti.

  Ujistěte se, že nepřekračujete prostor, který je k dispozici na zařízeních. Další informace o kapacitě úložiště zařízení najdete v tématu [jak kapacitu úložiště pro iOS a MacOS](https://support.apple.com/HT201402) (se otevírá na webu společnosti Apple).

- **Umístění mezipaměti**: zadejte cestu pro uložení obsahu uloženého v mezipaměti. Výchozí umístění je `/Library/Application Support/Apple/AssetCache/Data` . Doporučuje se, abyste toto umístění nezměnili.

  Pokud toto nastavení změníte, obsah uložený v mezipaměti nebude přesunut do nového umístění. Aby je bylo možné automaticky přesunout, uživatelé musí změnit umístění na zařízení (**Předvolby systému**pro  >  **sdílení**  >  **obsahu do mezipaměti**).

- **Port**: zadejte číslo portu TCP na zařízeních, kde má mezipaměť přijímat požadavky na stažení a nahrání, od 0-65535. Zadáním hodnoty nula ( `0` ) (výchozí) použijte libovolný port, který je k dispozici.
- **Blokovat připojení k Internetu a sdílení obsahu v mezipaměti**: označuje se také jako připojené do mezipaměti. **Ano** zabraňuje sdílení připojení k Internetu a zabraňuje sdílení obsahu uloženého v mezipaměti pomocí zařízení s iOS/iPadOS, která jsou připojená k počítači Mac. Uživatelé tuto funkci nemůžou povolit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

- **Povolit sdílení připojení k Internetu**: taky se označuje jako připojené do mezipaměti. **Ano** , umožňuje sdílení připojení k Internetu a umožňuje sdílení obsahu v mezipaměti pomocí zařízení s iOS/iPadOS, která jsou připojená k počítači Mac. Uživatelé tuto funkci nemůžou zakázat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci vypnout.

  Tato funkce platí pro:

  - macOS 10.15.4 a novější

- **Povolit mezipaměť pro protokolování podrobností klienta**: **Ano** zaznamená IP adresu a číslo portu zařízení, které požaduje obsah.Pokud řešíte problémy se zařízením, může vám tento soubor protokolu pomáhat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí tyto informace zaprotokolovat.

- **Vždycky uchovávat obsah z mezipaměti, i když systém potřebuje místo na disku pro jiné aplikace**: **Ano** uchovává obsah mezipaměti a zajišťuje, že se nic neodstraní, i když je nedostatek místa na disku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vyprázdnit obsah z mezipaměti automaticky, když bude potřebovat prostor úložiště pro ostatní aplikace.

  Tato funkce platí pro:

  - macOS 10,15 a novější

- **Zobrazit upozornění na stav**: **Ano** zobrazuje výstrahy jako systémová oznámení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí tyto výstrahy zobrazit jako systémová oznámení.

  Tato funkce platí pro:

  - macOS 10,15 a novější

- **Zabránit pozastavení zařízení v režimu spánku, když je zapnuté ukládání do mezipaměti**: **Ano** zabraňuje počítači přejít do režimu spánku, pokud je ukládání do mezipaměti zapnuté. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení nechat v režimu spánku.

  Tato funkce platí pro:

  - macOS 10,15 a novější

- **Zařízení do mezipaměti**: Vyberte zařízení, která můžou obsah ukládat do mezipaměti. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. 
  - **Zařízení používající stejnou místní síť**: mezipaměť obsahu nabízí obsah pro zařízení ve stejné bezprostřední místní síti. Zařízení v jiných sítích nenabízí žádný obsah, včetně zařízení, která jsou dostupná pro mezipaměť obsahu.
  - **Zařízení používající stejnou veřejnou IP adresu**: mezipaměť obsahu nabízí obsah pro zařízení, která používají stejnou veřejnou IP adresu. Zařízení v jiných sítích nenabízí žádný obsah, včetně zařízení, která jsou dostupná pro mezipaměť obsahu.
  - **Zařízení využívající vlastní místní sítě**: mezipaměť obsahu poskytuje obsah pro zařízení v rozsahu IP adres, které zadáte.
    - **Rozsahy naslouchání klientů**: zadejte rozsah IP adres, které mohou přijímat mezipaměť obsahu.
  - **Zařízení používající vlastní místní sítě s Fallback**: mezipaměť obsahu poskytuje obsah pro zařízení v oblasti poslechu, rozsahy naslouchání v partnerském prostředí a IP adresy rodičů.
    - **Rozsahy naslouchání klientů**: zadejte rozsah IP adres, které mohou přijímat mezipaměť obsahu.

- **Vlastní veřejné IP adresy**: zadejte rozsah veřejných IP adres. Cloudové servery používají tento rozsah ke spárování klientských zařízení s mezipamětí.

- **Sdílet obsah s jinými mezipamětmi**: Pokud vaše síť obsahuje více než jednu mezipaměť obsahu, mezipaměti obsahu v jiných zařízeních se automaticky stanou partnerskými uzly. Tato zařízení můžou prostudovat a sdílet software uložený v mezipaměti. 

  Když požadovaná položka není dostupná pro jednu mezipaměť obsahu, zkontroluje její partnerské uzly pro danou položku. Pokud je položka k dispozici, je stažena z mezipaměti obsahu na partnerském zařízení. Pokud není stále k dispozici, mezipaměť obsahu stáhne položku z:

  - Nadřazená IP adresa, pokud je nakonfigurovaná
  
    ANI
    
  - Od společnosti Apple přes Internet

  Pokud je k dispozici více než jedna mezipaměť obsahu, zařízení automaticky vyberou správnou mezipaměť obsahu. 

  Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Mezipaměti obsahu pomocí stejných místních sítí**: mezipaměť obsahu se dá použít jenom pro jiné mezipaměti obsahu v stejné bezprostřední místní síti.
  - **Mezipaměti obsahu používající stejnou veřejnou IP adresu**: mezipaměť obsahu se dá použít jenom u ostatních mezipamětí obsahu na stejné veřejné IP adrese.
  - **Mezipaměti obsahu s použitím vlastních místních sítí**: mezipaměť obsahu je v rozsahu naslouchání IP adres, kterou zadáte, jenom Peers s dalšími mezipaměťmi obsahu:

    - **Rozsahy partnerských naslouchání**: Zadejte počáteční a koncové IP adresy IPv4 nebo IPv6 pro váš rozsah. Mezipaměť obsahu reaguje jenom na žádosti sdílené mezipaměti z mezipaměti obsahu v rozsahu IP adres, které zadáte.
    - **Rozsahy rovnocenného filtru**: Zadejte počáteční a koncové IP adresy IPv4 nebo IPv6 pro váš rozsah. Mezipaměť obsahu filtruje svůj seznam partnerských uzlů pomocí rozsahů IP adres, které zadáte.

- **Nadřazené IP adresy**: Zadejte místní IP adresu jiné mezipaměti obsahu, kterou chcete přidat jako nadřazenou mezipaměť. Mezipaměť odesílá a stahuje obsah do těchto mezipamětí a místo toho se nahrává a stahuje přímo pomocí společnosti Apple. Jenom jednu nadřazenou IP adresu přidejte jenom jednou.
- **Zásada nadřazeného výběru**: Pokud existuje mnoho nadřazených mezipamětí, vyberte, jak se vybere nadřazená IP adresa. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Kruhové dotazování**: použijte nadřazené IP adresy v daném pořadí. Tato možnost je vhodná pro scénáře vyrovnávání zatížení.
  - **První k dispozici**: vždy použijte první dostupnou IP adresu v seznamu.
  - **Hash**: vytvoří hodnotu hash pro část cesty požadované adresy URL. Tato možnost zajistí, že stejná nadřazená IP adresa se vždycky používá pro stejnou adresu URL.
  - **Náhodný**: náhodně použijte IP adresu v seznamu. Tato možnost je vhodná pro scénáře vyrovnávání zatížení.
  - **Rychlé dostupnosti**: vždy použijte první IP adresu v seznamu. Pokud není k dispozici, použijte druhou IP adresu v seznamu. Pokračujte v používání druhé IP adresy, dokud není k dispozici, a tak dále.

## <a name="login-items"></a>Přihlašovací položky

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Přidat soubory, složky a vlastní aplikace, které se spustí při přihlášení**: **přidejte** cestu k souboru, složce, vlastní aplikaci nebo systémové aplikaci, která se otevře, když se uživatelé přihlásí ke svým zařízením. Dále zadejte:

  - **Cesta položky**: zadejte cestu k souboru, složce nebo aplikaci. Systémové aplikace nebo aplikace sestavené nebo přizpůsobené pro vaši organizaci jsou obvykle ve `Applications` složce s cestou podobnou `/Applications/AppName.app` .

    Můžete přidat mnoho souborů, složek a aplikací. Zadejte například .  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Při přidávání libovolné aplikace, složky nebo souboru Nezapomeňte zadat správnou cestu. Ne všechny položky jsou ve `Applications` složce. Pokud uživatel přesune položku z jednoho umístění do jiného, pak se cesta změní. Tato přesunutá položka nebude otevřena, když se uživatel přihlásí.

  - **Skrýt**: tuto možnost vyberte, pokud chcete aplikaci zobrazit nebo skrýt. Možnosti:
    - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém zobrazit položky v seznamu uživatelů & skupiny přihlášení s možností skrýt nezaškrtnutou.
    - **Ano**: skryje aplikaci v seznamu Uživatelé & skupiny přihlášení.

## <a name="login-window"></a>Přihlašovací okno

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Zobrazit další informace v řádku nabídek**: když je vybraná časová oblast na řádku nabídek, zobrazí **Ano** název hostitele a verzi MacOS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí tyto informace na řádku nabídek zobrazit.
- **Banner**: zadejte zprávu, která se zobrazí na přihlašovací obrazovce na zařízeních. Zadejte například informace o vaší organizaci, uvítací zprávu, ztracené a zjištěné informace atd.
- **Textové pole vyžadovat uživatelské jméno a heslo**: Vyberte způsob, jakým se uživatelé přihlásí k zařízením. **Ano** – vyžaduje, aby uživatelé zadali uživatelské jméno a heslo. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení operační systém může vyžadovat, aby si uživatelé ze seznamu vybrali své uživatelské jméno a pak zadali jejich heslo.

  Dále zadejte:

  - **Skrýt místní uživatele**: **Ano** nezobrazí místní uživatelské účty v seznamu uživatelů, které mohou zahrnovat účty Standard a admin. Zobrazují se jenom účty uživatelů sítě a systému. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém v seznamu uživatelů zobrazovat místní uživatelské účty.
  - **Skrýt mobilní účty**: **Ano** v seznamu uživatelů nezobrazí mobilní účty. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit mobilní účty v seznamu uživatelů. Některé mobilní účty se můžou zobrazovat jako síťoví uživatelé.
  - **Zobrazit uživatele sítě**: výběrem **Ano** zobrazíte seznam uživatelů sítě v seznamu uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí v seznamu uživatelů zobrazovat síťové uživatelské účty.
  - **Skrýt správce počítače** **: v** seznamu uživatel nezobrazí účty uživatelů správce. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit uživatelské účty správce v seznamu uživatelů.
  - **Zobrazit další uživatele**: vyberte **Ano** , pokud chcete zobrazit seznam **dalších** uživatelů v seznamu uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí v seznamu uživatelů zobrazovat jiné uživatelské účty.

- **Skrýt tlačítko pro vypnutí**: **na** přihlašovací obrazovce se nezobrazí tlačítko vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tlačítko vypnout.
- **Skrýt tlačítko**pro restartování **: na** přihlašovací obrazovce se nezobrazí tlačítko restartovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tlačítko restartovat.
- **Skrýt tlačítko pro režim spánku**: na obrazovce přihlásit **se nezobrazí tlačítko** režimu spánku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tlačítko režimu spánku.
- **Zakázat přihlášení uživatele z konzoly**: **Ano** skryje MacOS příkazový řádek, který se používá pro přihlášení. U typických uživatelů nastavte toto nastavení na **Ano**. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby se přihlásili pomocí příkazového řádku macOS. Chcete-li přejít do režimu konzoly, uživatelé zadají `>console` do pole uživatelské jméno a musí se ověřit v okně konzoly.
- **Zakázat vypnutí při přihlášení**: **Ano** znemožní uživatelům vybrat možnost **vypnutí** po přihlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízeních vybrali položku nabídky pro **vypnutí** .
- **Zakázat restart během přihlášení**: **Ano** zabraňuje uživatelům v výběru možnosti **restartování** po přihlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **restartovat** na zařízeních.
- **Vypnout vypnutí během**přihlašování: **Ano** znemožní uživatelům vybrat možnost **vypnutí** po přihlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **napájení** v zařízeních.
- **Zakázat odhlásit se během přihlášení** (MacOS 10,13 a novější): **Ano** uživatelům zabránit v výběru možnosti **odhlášení** po přihlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **Odhlásit** se na zařízeních.
- **Zakázat zamykací obrazovku, pokud jste přihlášeni** (MacOS 10,13 a novější): **Ano** zabraňuje uživatelům v výběru možnosti **zamykací obrazovky** po přihlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **zamykací obrazovka** na zařízeních.

## <a name="single-sign-on-app-extension"></a>Rozšíření aplikace s jednotným přihlašováním

Tato funkce platí pro:

- macOS 10,15 a novější

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení schválená uživatelem a automatický zápis zařízení

- **Typ rozšíření aplikace jednotného přihlašování**: Vyberte typ rozšíření aplikace jednotného přihlašování. Možnosti:

  - **Nenakonfigurováno**: rozšíření aplikací se nepoužívají. Pokud chcete rozšíření aplikace zakázat, přepněte typ rozšíření aplikace jednotného přihlašování na **Nenakonfigurováno**.
  - **Microsoft Azure AD**: používá modul plug-in Microsoft Enterprise SSO, což je rozšíření aplikace jednotného přihlašování typu přesměrování. Tento modul plug-in poskytuje jednotné přihlašování pro účty služby Active Directory napříč všemi macOS aplikacemi, které podporují funkci [podnikového jednotného přihlašování od společnosti Apple](https://developer.apple.com/documentation/authenticationservices) . Tento typ rozšíření aplikace jednotného přihlašování použijte k povolení jednotného přihlašování v aplikacích Microsoftu, organizačních aplikacích a websites, které se ověřují pomocí Azure AD.

    Modul plug-in jednotného přihlašování funguje jako zprostředkovatel pokročilého ověřování, který nabízí vylepšení zabezpečení a uživatelského prostředí.

    > [!IMPORTANT]
    > K zajištění jednotného přihlašování s typem rozšíření aplikace Microsoft Azure AD jednotného přihlašování, nainstalujte na zařízení aplikaci Portál společnosti macOS. Aplikace Portál společnosti doručuje do zařízení modul plug-in Microsoft Enterprise SSO. Nastavení rozšíření aplikace pro jednotné přihlašování (MDM) aktivuje modul plug-in. Po instalaci aplikace Portál společnosti a profilu rozšíření aplikace jednotného přihlašování na zařízení se uživatelé přihlásí pomocí svých přihlašovacích údajů a vytvoří relaci na jejich zařízeních. Tato relace se používá v různých aplikacích, aniž by bylo nutné znovu ověřovat uživatele.
    >
    > Další informace o aplikaci Portál společnosti najdete v tématu [co se stane, když nainstalujete aplikaci Portál společnosti a zaregistrujete zařízení MacOS v Intune](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md). [Stáhněte](https://go.microsoft.com/fwlink/?linkid=853070) si aplikaci Portál společnosti.

  - **Přesměrování**: k použití jednotného přihlašování s moderními toky ověřování použijte obecné a přizpůsobitelné rozšíření aplikace pro přesměrování. Ujistěte se, že znáte rozšíření a ID týmu pro rozšíření aplikace vaší organizace.
  - **Přihlašovací údaje**: pomocí obecného rozšíření aplikace s přizpůsobitelnou přihlašovacími údaji můžete používat jednotné přihlašování s toky ověřování typu Challenge a Response. Ujistěte se, že znáte ID rozšíření a ID týmu pro rozšíření aplikace jednotného přihlašování ve vaší organizaci.  
  - **Kerberos**: použijte integrované rozšíření protokolu Kerberos společnosti Apple, které je součástí macOS Catalina 10,15 a novějších. Tato možnost je verze rozšíření **přihlašovacích údajů** specifická pro Kerberos.

  > [!TIP]
  > Pomocí typů **přesměrování** a **přihlašovacích údajů** přidáte vlastní hodnoty konfigurace, které budou předávány prostřednictvím rozšíření. Pokud používáte **přihlašovací údaje**, zvažte použití integrovaného nastavení konfigurace poskytovaného společností Apple v typu **Kerberos** .

- **ID rozšíření** (přesměrování, pověření): zadejte identifikátor sady prostředků, který identifikuje vaše rozšíření aplikace jednotného přihlašování, například `com.apple.ssoexample` .
- **ID týmu** (přesměrování, pověření): zadejte identifikátor týmu rozšíření aplikace jednotného přihlašování. Identifikátor týmu je alfanumerický řetězec (čísla a písmena), který vygenerovala společnost Apple, jako je například `ABCDE12345` . 

  [Najděte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře se webová stránka společnosti Apple), kde najdete další informace.

- **Sféra** (přihlašovací údaje, Kerberos): zadejte název sféry ověřování. Název sféry by měl být velkými písmeny, například `CONTOSO.COM` . Název vaší sféry je typicky stejný jako název vaší domény DNS, ale jenom na velká písmena.

- **Domény** (přihlašovací údaje, Kerberos): zadejte doménu nebo názvy hostitelů pro weby, které se dají ověřit pomocí jednotného přihlašování. Například pokud je váš web `mysite.contoso.com` , pak `mysite` je název hostitele a `contoso.com` je název domény. Když se uživatelé připojí k některé z těchto webů, aplikace App Extension zpracuje výzvu ověřování. Toto ověřování umožňuje uživatelům k přihlášení použít ID obličeje, dotykové ID nebo Apple PINCODE/přístupový kód.

  - Všechny domény v profilech služby Intune, které mají rozšíření pro aplikace jednotného přihlašování, musí být jedinečné. Doménu nemůžete opakovat v žádném profilu rozšíření aplikace pro přihlášení, i když používáte různé typy rozšíření aplikace jednotného přihlašování.
  - U těchto domén se nerozlišují velká a malá písmena.

- **Adresy URL** (pouze přesměrované): zadejte PŘEDPONY adresy URL vašich zprostředkovatelů identity, na jejichž základě rozšíření pro přesměrování aplikace používá jednotné přihlašování. Když budou uživatelé přesměrováni na tyto adresy URL, rozšíření aplikace jednotného přihlašování se zasáhne a zobrazí výzvu k přihlášení SSO.

  - Všechny adresy URL v profilech rozšíření aplikace jednotného přihlašování Intune musí být jedinečné. Doménu nejde opakovat v žádném profilu rozšíření aplikace jednotného přihlašování, a to ani v případě, že používáte různé typy rozšíření aplikace jednotného přihlašování.
  - Adresy URL musí začínat na `http://` nebo `https://` .

- **Další konfigurace** (Microsoft Azure AD, přesměrování, pověření): zadejte další data specifická pro rozšíření, která chcete předat rozšíření aplikace jednotného přihlašování:
  - **Klíč**: zadejte název položky, kterou chcete přidat, například `user name` .
  - **Typ**: zadejte typ dat. Možnosti:

    - Řetězec
    - Boolean: v **konfigurační hodnotě**zadejte `True` nebo `False` .
    - Integer: v **hodnotě konfigurace**zadejte číslo.

  - **Hodnota**: zadejte data.
  
  - **Přidat**: vyberte, pokud chcete přidat konfigurační klíče.

- **Použití řetězce klíčů** (jenom Kerberos): vyberte **blok** , aby se zabránilo ukládání a ukládání hesel do řetězce klíčů. Pokud je blokováno, uživatelé nebudou vyzváni k uložení hesla a po vypršení platnosti lístku protokolu Kerberos je nutné znovu zadat heslo. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém ukládat hesla a uložit je do řetězce klíčů. Uživatelům se po vypršení platnosti lístku nezobrazí výzva k zadání hesla.
- **ID obličeje, dotykové ID nebo heslo** (jenom Kerberos): **vyžaduje** , aby uživatelé při aktualizaci lístku Kerberos zadali své ID a dotykové jméno a heslo zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat, aby uživatelé pomocí biometrika nebo hesla zařízení aktualizovali lístek protokolu Kerberos. Pokud je **použití řetězce klíčů** blokované, pak toto nastavení neplatí.
- **Výchozí sféra** (pouze Kerberos): Chcete-li nastavit hodnotu **sféry** , kterou jste zadali jako výchozí sféru, vyberte možnost **Povolit** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí nastavit výchozí sféru.

  > [!TIP]
  > - Toto nastavení **Povolte** , pokud konfigurujete více rozšíření aplikace pro jednotné přihlašování pomocí protokolu Kerberos ve vaší organizaci.
  > - Toto nastavení **Povolte** , pokud používáte více sfér. Nastaví hodnotu **sféry** , kterou jste zadali jako výchozí sféru.
  > - Pokud máte pouze jednu sféru, ponechte ji **nenakonfigurovanou** (výchozí).

- **Automatická konfigurace** (jenom Kerberos): Pokud je nastavená na **blokovat**, nebude rozšíření protokolu Kerberos automaticky používat LDAP a DNS k určení jeho názvu lokality Active Directory. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit, že rozšíření automaticky nalezne název lokality služby Active Directory.
- **Změny hesla** (jenom Kerberos): **blok** znemožní uživatelům měnit hesla, která používají pro přihlášení k doménám, které jste zadali. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit změny hesla.  
- **Synchronizace hesel** (jenom Kerberos): Pokud chcete synchronizovat místní hesla uživatelů do Azure AD, vyberte **Povolit** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zakázat synchronizaci hesel do služby Azure AD. Toto nastavení použijte jako alternativu nebo zálohu k jednotnému přihlašování. Toto nastavení nefunguje, pokud jsou uživatelé přihlášení pomocí mobilního účtu Apple.
- **Složitost hesla služby Active Directory systému Windows Server** (pouze Kerberos): vyberte možnost **vyžadovat** , pokud chcete vynutit uživatelská hesla pro splnění požadavků na složitost hesla služby Active Directory. Další informace najdete v tématu [heslo musí splňovat požadavky na složitost](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat, aby uživatelé splnili požadavky na heslo služby Active Directory.
- **Minimální délka hesla** (jenom Kerberos): zadejte minimální počet znaků, které můžou vytvářet hesla uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí pro uživatele vymáhat minimální délku hesla.
- **Omezení opakovaného použití hesla** (jenom Kerberos): zadejte počet nových hesel, od 1-24, která se použijí, až bude možné znovu použít předchozí heslo v doméně. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vynutilit omezení opakovaného použití hesla.
- **Minimální stáří hesla** (jenom Kerberos): zadejte počet dní, po které se heslo v doméně používá, než je může uživatel změnit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyhovět minimálnímu stáří hesla, aby bylo možné je změnit.
- **Oznámení vypršení platnosti hesla** (jenom Kerberos): zadejte počet dní, než heslo vyprší, uživatelé obdrží oznámení o vypršení platnosti hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém používat `15` dny.
- **Vypršení platnosti hesla** (jenom Kerberos): zadejte počet dní, než se musí změnit heslo zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém nikdy vypršení platnosti hesel.
- **Adresa URL pro změnu hesla** (jenom Kerberos): zadejte adresu URL, která se otevře, když uživatelé spustí změnu hesla protokolu Kerberos.
- **Hlavní název** (jenom Kerberos): zadejte uživatelské jméno objektu zabezpečení protokolu Kerberos. Nemusíte zahrnovat název sféry. Například v `user@contoso.com` , `user` je hlavní název a `contoso.com` je název sféry.

  > [!TIP]
  > - Můžete také použít proměnné v hlavním názvu tak, že zadáte složené závorky `{{ }}` . Pokud například chcete zobrazit uživatelské jméno, zadejte `Username: {{username}}` . 
  > - Buďte ale opatrní s náhradou proměnných, protože proměnné nejsou v uživatelském rozhraní ověřené a rozlišují velká a malá písmena. Nezapomeňte zadat správné informace.
  
- **Kód lokality služby Active Directory** (pouze Kerberos): zadejte název lokality služby Active Directory, kterou má rozšíření protokolu Kerberos použít. Tuto hodnotu pravděpodobně nebudete muset měnit, protože rozšíření protokolu Kerberos může automaticky najít kód lokality služby Active Directory.
- **Název mezipaměti** (jenom Kerberos): zadejte název obecné služby zabezpečení (GSS) mezipaměti protokolu Kerberos. Tuto hodnotu pravděpodobně nemusíte nastavovat.  
- **Zpráva požadavky na heslo** (jenom Kerberos): zadejte textovou verzi požadavků na heslo vaší organizace, které se zobrazují uživatelům. Tato zpráva se zobrazí, pokud nepožadujete požadavky na složitost hesla služby Active Directory nebo nezadáte minimální délku hesla.  
- **Povolit režim sdíleného zařízení** (jenom Microsoft Azure AD): Pokud nasazujete modul plug-in Microsoft Enterprise SSO do zařízení MacOS nakonfigurovaných pro funkci režimu sdíleného zařízení Azure AD, vyberte **Ano** . Zařízení ve sdíleném režimu umožňují mnoha uživatelům globálně přihlašovat se k aplikacím, které podporují režim sdíleného zařízení. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje. 

  Pokud je nastaveno na **Ano**, všechny existující uživatelské účty se ze zařízení vymažou. Aby nedošlo ke ztrátě dat, nebo chcete zabránit obnovení továrního nastavení, ujistěte se, že rozumíte tomu, jak toto nastavení mění vaše zařízení.

  Další informace o režimu sdílených zařízení najdete v tématu [Přehled režimu sdíleného zařízení](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices).

- **ID sady prostředků aplikace** (Microsoft Azure AD, Kerberos): **přidejte** identifikátory sady prostředků aplikace, které by měly na svých zařízeních používat jednotné přihlašování. Těmto aplikacím je udělen přístup k lístku pro udělení lístku protokolu Kerberos a ověřovacímu lístku. Aplikace také ověřují uživatele pro služby, kterým má oprávnění k přístupu.
- **Mapování sféry domény** (jenom Kerberos): **přidejte** přípony DNS domény, které by se měly namapovat do vaší sféry. Toto nastavení použijte, pokud názvy DNS hostitelů neodpovídají názvu sféry. Pravděpodobně nemusíte vytvářet vlastní mapování domén na sféru.
- **PKINIT certifikát** (jenom Kerberos): **Vyberte** certifikát kryptografie s veřejným klíčem pro počáteční ověřování (PKINIT), který se dá použít pro ověřování protokolem Kerberos. Můžete si vybrat z certifikátů [PKCS](../protect/certficates-pfx-configure.md) nebo [SCEP](../protect/certificates-scep-configure.md) , které jste přidali v Intune. Další informace o certifikátech najdete v tématu [použití certifikátů k ověřování v Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Funkce zařízení můžete nakonfigurovat také v systému [iOS/iPadOS](ios-device-features-settings.md).