---
title: nastavení zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních macOS k omezení funkcí v Microsoft Intune. Nastavte požadavky na heslo, nastavte si uzamčenou obrazovku, používejte integrované aplikace, přidejte omezené nebo schválené aplikace, zpracujte zařízení Bluetooth, připojte se ke cloudu pro zálohování a úložiště, povolte celoobrazovkový režim, přidejte domény a nastavte, jak uživatelé pracují s webovým prohlížečem Safari.
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
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d762f3729f104bedc992c93f1a445ab00b547841
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813655"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>macOS nastavení zařízení pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popisuje různá nastavení, která můžete řídit na zařízeních macOS. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, nastavit pravidla pro hesla, povolit nebo omezit konkrétní aplikace a další.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí do zařízení macOS.

> [!NOTE]
> Uživatelské rozhraní nemusí odpovídat typům registrace v tomto článku. Informace v tomto článku jsou správné. Uživatelské rozhraní se aktualizuje v nadcházející verzi.

## <a name="before-you-begin"></a>Než začnete

Vytvoří [konfigurační profil omezení zařízení MacOS](device-restrictions-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace. Další informace o různých typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>Integrované aplikace

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Blokovat automatické vyplňování prohlížeče Safari**: **Ano** zakáže funkci automatického vyplňování v Safari na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení automatického dokončování ve webovém prohlížeči.
- **Zablokovat používání kamery**: **Ano** zabraňuje přístupu ke kameře na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k kameře zařízení.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.
  
- **Blokování Apple Music**: **Yes** vrátí aplikaci v hudbě do klasického režimu a zakáže hudební službu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace Apple Music.
- **Zablokovat návrhy Spotlightu**: **Ano** , pokud se vrátí výsledky hledání na internetu, přestane Spotlight. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat připojení Spotlightu k Internetu a získání výsledků hledání.
- **Blokovat přenos souborů pomocí služby Finder nebo iTunes**: **Ano** zakáže služby pro sdílení souborů aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat služby sdílení souborů aplikací.

  Tato funkce platí pro:  
  - macOS 10,13 a novější

## <a name="cloud-and-storage"></a>Cloud a úložiště

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Blokovat synchronizaci řetězce klíčů iCloud**: **Ano** zakáže synchronizaci přihlašovacích údajů uložených v řetězci klíčů do iCloud. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožňovat synchronizaci těchto přihlašovacích údajů.
- **Blokovat synchronizaci stolních počítačů a dokumentů iCloud**: **Ano** zabraňuje iCloud synchronizaci dokumentů a dat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci dokumentu a klíč-hodnota do iCloud prostoru úložiště.
- **Blokovat zálohování pošty iCloud**: **Ano** zabraňuje iCloud synchronizaci do aplikace MacOS mail. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci pošty iCloud.
- **Zablokovat zálohování kontaktů iCloud**: **Ano** zabraňuje iCloud synchronizaci kontaktů zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci kontaktů pomocí iCloud.
- **Zablokovat zálohování kalendáře iCloud**: **Ano** zabraňuje iCloud synchronizaci do aplikace kalendáře MacOS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit synchronizaci kalendáře do iCloud.
- **Zablokovat zálohování připomenutí iCloud**: **Ano** zabraňuje tomu, aby se iCloud synchronizoval do aplikace MacOS s připomenutími. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci připomenutí do iCloud.
- **Zablokovat zálohování záložek iCloud**: **Ano** zabraňuje iCloud synchronizaci záložek zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci záložek do iCloud.
- **Zablokovat zálohování poznámek iCloud**: **Ano** zabraňuje iCloud synchronizaci poznámek zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci poznámek s iCloud.
- **Zablokovat zálohování fotek iCloud**: **Ano** zakáže iCloud knihovnu fotografií a zabraňuje iCloud synchronizaci fotek zařízení. Všechny fotky, které nejsou plně stažené z knihovny fotografií iCloud, se z místního úložiště na zařízeních odeberou. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci fotek mezi zařízením a knihovnou fotek iCloud.
- Zaznamenání **bloku**: Tato funkce umožňuje uživatelům začít pracovat na zařízení MacOS a potom pokračovat v práci, kterou zahájil na jiném zařízení s iOS/IPadOS nebo MacOS. Možnost **Ano** zabrání funkci předání na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci na zařízeních dovolit.

  Tato funkce platí pro:  
  - macOS 10,15 a novější

## <a name="connected-devices"></a>Připojená zařízení

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Blokovat přetažení**: **Ano** zabraňuje použití přetahování na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít funkci přetažení, která umožňuje výměnu obsahu s okolními zařízeními.
- **Blokovat Apple Watch automatické odemknutí**: **Ano** znemožní uživatelům odemknout zařízení MacOS s jejich Apple Watch. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit odemknout zařízení macOS pomocí jejich Apple Watch.

## <a name="domains"></a>Domény

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Neoznačené e-mailové domény**: do seznamu zadejte jednu nebo víc **adres URL e-mailových domén** . Když uživatelé odesílají nebo dostanou e-mail z jiné domény než z domén, které jste přidali, bude tento e-mail v aplikaci macOS mail označen jako nedůvěryhodný.

## <a name="general"></a>Obecné

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Blokování vyhledávání**: **Ano** znemožní uživateli zvýraznit slovo a pak vyhledat jeho definici na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat funkci vyhledávání definic.
- **Vydiktování bloků**: **Ano** zabraňuje uživatelům v zadávání textu pomocí hlasového vstupu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit použít vstup diktování.
- **Blokovat ukládání obsahu do mezipaměti**: **Ano** zabraňuje ukládání obsahu do mezipaměti. Ukládání obsahu do mezipaměti ukládá data aplikací, data webového prohlížeče, soubory ke stažení a další lokálně na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit ukládání obsahu do mezipaměti.

  Další informace o ukládání obsahu do mezipaměti v macOS najdete v tématu [Správa ukládání obsahu do mezipaměti na Macu](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (otevře další web).

  Tato funkce platí pro:  
  - macOS 10,13 a novější

- **Blokovat snímky obrazovky a záznam obrazovky**: zařízení musí být zaregistrované v automatickém zápisu zařízení (DEP) společnosti Apple. Hodnota **Ano** zabraňuje uživatelům ukládat snímky obrazovky obrazovky. Zabraňuje také aplikaci učeben v pozorování vzdálených obrazovek. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit zachytit snímky obrazovky a umožňuje aplikaci učeben zobrazit vzdálené obrazovky.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment-supervised"></a>Nastavení platí pro: registrace zařízení schválená uživatelem, automatický zápis zařízení (pod dohledem)

- **Odložit aktualizace softwaru**: hodnota **Ano** umožňuje zpoždění, pokud se na zařízeních zobrazují aktualizace operačního systému a aktualizace bez OS. Toto nastavení neřídí, kdy jsou aktualizace nebo nejsou nainstalovány. Pokud není nic vybráno, Intune toto nastavení nezmění ani neaktualizuje.

  Ve výchozím nastavení může operační systém na zařízeních zobrazovat aktualizace, když je Apple uvolňuje. Ve výchozím nastavení nejsou aktualizace softwaru zpožděny. Pokud toto nastavení nakonfigurujete, budou se v závislosti na vybraných možnostech zpozdit i aktualizace softwaru v operačních systémech a jiných operačních systémech. Rozevírací seznam přesně vybíráte. Může zpoždění odložit, ani zpozdit ani jedno z nich.

  Pokud se třeba aktualizace macOS uvolní od společnosti Apple po konkrétní datum, pak se tato aktualizace přirozeně zobrazuje na zařízeních v datu vydání verze. Aktualizace sestavení v počátečním nasazení jsou povoleny bez zpoždění.  

  - **Zpoždění viditelnosti aktualizací softwaru**: zadejte hodnotu od 0-90 dnů. Ve výchozím nastavení jsou aktualizace pro dny zpožděny `30` . Tato hodnota se vztahuje na vybrané možnosti pro **odložení aktualizací softwaru** . Pokud vyberete pouze **aktualizace operačního systému**, budou po dobu 30 dnů zpožděny pouze aktualizace operačního systému. Pokud vyberete **aktualizace operačního systému** a **aktualizace, které nejsou v operačním systému**, budou obě služby zpožděné po dobu 30 dnů.

    Po vypršení zpoždění budou uživatelé dostávat oznámení o aktualizaci na nejstarší verzi, která je k dispozici při aktivaci zpoždění.

    Pokud je například macOS aktualizace k dispozici **1. ledna**a je **zpoždění viditelnosti** nastaveno na **5 dní**, aktualizace se nezobrazí jako dostupná aktualizace. Po **šestém dni** od vydání je tato aktualizace dostupná a uživatelé ji můžou nainstalovat.

    Tato funkce platí pro:  
    - macOS 10.13.4 a novější

### <a name="settings-apply-to-automated-device-enrollment"></a>Nastavení platí pro: automatický zápis zařízení

- **Zakázat AirPlay, zobrazit obrazovku podle aplikace učebny a sdílení obrazovky**: **Ano** blokuje AirPlay a zabraňuje sdílení obrazovky jiným zařízením. Také brání učitelům v používání aplikace učebny, aby viděli své obrazovky studentů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém může učitelům dovolit zobrazit své obrazovky studentů.

  Chcete-li použít toto nastavení, nastavte nastavení **blokovat snímky obrazovky a nahrávání obrazovky** na **Nenakonfigurováno** (snímky obrazovky jsou povoleny).

- **Dovolit aplikaci učeben provádět AirPlay a zobrazovat obrazovku bez zobrazení výzvy**: **Ano** umožní učitelům zobrazit obrazovky studentů, aniž by museli souhlasit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při zobrazení obrazovky učitelům vyžadovat, aby studenti mohli souhlasit.

  Chcete-li použít toto nastavení, nastavte nastavení **blokovat snímky obrazovky a nahrávání obrazovky** na **Nenakonfigurováno** (snímky obrazovky jsou povoleny).

- **Vyžadovat oprávnění učitelů k opuštění nespravovaných tříd aplikace učebny**: **Ano** vynutí studenty zaregistrované v nespravovaném kurzu, aby získali schválení učitelů, aby mohl kurz opustit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při každém výběru studenta dovolit kurzu opustit kurz.

- **Povolit učebně zařízení uzamknout bez zobrazení výzvy**: **Ano** umožní učitelům uzamknout zařízení nebo aplikaci studenta bez schválení studenta. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vyžadovat, aby studenti před tím, než si můžou zařízení nebo aplikaci uzamknout, museli souhlasit.

- **Studenti se můžou automaticky připojit ke třídě učeben bez zobrazení výzvy**: **Ano** umožňuje studentům připojit se ke třídě bez vyzvání k učiteli. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vyžadovat schválení učitelů pro připojení ke třídě.

## <a name="password"></a>Heslo

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Vyžadovat heslo**: **Ano** vyžaduje, aby uživatelé zadali heslo pro přístup k zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat heslo. Také nevynucuje žádná omezení, jako je například blokování jednoduchých hesel nebo nastavení minimální délky.
  - **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla, kterou vaše organizace vyžaduje. Pokud je ponecháno prázdné, Intune toto nastavení nezmění ani neaktualizuje. Možnosti:
    - **Nenakonfigurováno**: používá výchozí nastavení zařízení.
    - **Alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice.
    - **Číselná**: heslo musí obsahovat jenom čísla, třeba 123456789.

    Tato funkce platí pro:  
    - macOS 10.10.3 a novější

  - **Počet nealfanumerických znaků v hesle**: zadejte počet složitých znaků vyžadovaných v hesle, od 0-4. Složitý znak je symbol, například `?` . Pokud je ponecháno prázdné nebo nastaveno na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.
  - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4-16 znaků. Pokud je ponecháno prázdné, Intune toto nastavení nezmění ani neaktualizuje.
  - **Blokovat jednoduchá hesla**: hodnota **Ano** zabraňuje použití jednoduchých hesel, jako je například `0000` nebo `1234` . Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje. Ve výchozím nastavení může operační systém umožňovat jednoduchá hesla.
  - **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte dobu, po kterou musí být zařízení nečinné, než se obrazovka automaticky zamkne. Zadejte například, `5` Pokud chcete zařízení zamknout po 5 minutách nečinnosti. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.
  - **Maximální počet minut po uzamčení obrazovky, než se požaduje heslo**: zadejte dobu, po kterou musí být zařízení neaktivní, než bude nutné heslo odemknout. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.
  - **Vypršení platnosti hesla (dny)**: zadejte počet dní, než bude nutné změnit heslo zařízení, od 1-65535. Zadejte například `90` platnost hesla po 90 dnech. Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.
  - **Zakázat opakované použití předchozích hesel**: omezit uživatelům vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Zadejte například hodnotu 5, aby uživatelé nemohli nastavit nové heslo, nebo některá z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.

- **Zablokovat uživateli změnu hesla**: **Ano** zastaví změny, přidání nebo odebrání hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidat, změnit nebo odebrat hesla.

- **Zablokovat dotykové ID pro odemknutí zařízení**: **Ano** zabraňuje použití otisků prstů k odemknutí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby zařízení odemkli pomocí otisku prstu.

- **Zablokovat automatické vyplňování hesel**: **Ano** zabraňuje použití funkce automatického vyplňování hesel na MacOS. Výběr možnosti **Ano** má také následující dopad:

  - Uživatelům se nezobrazí výzva k použití uloženého hesla v Safari nebo ve všech aplikacích.
  - Automatická silná hesla jsou zakázaná a silná hesla se uživatelům nedoporučují.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto funkce dovolit.

- **Zablokovat žádosti o blízkost hesla**: **Ano** znemožní zařízením vyžadovat hesla z blízkých zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto požadavky na heslo způsobit.

- **Blokovat sdílení hesel**: **Ano** zabraňuje sdílení hesel mezi zařízeními pomocí přetažení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat sdílení hesel.

## <a name="privacy-preferences"></a>Předvolby ochrany osobních údajů

V zařízeních macOS se aplikace a procesy často vyzvou uživatele, aby povolili nebo odepřeli přístup k funkcím zařízení, jako je fotoaparát, mikrofon, kalendář, složka dokumentů a další. Tato nastavení umožňují správcům předschvalovat nebo předem odepřít přístup k těmto funkcím zařízení. Při konfiguraci těchto nastavení budete spravovat souhlas s přístupem k datům jménem svých uživatelů. Vaše nastavení potlačí jejich předchozí rozhodnutí.

Cílem těchto nastavení je snížit počet výzev aplikacemi a procesy.

Tato funkce platí pro:

- macOS 10,14 a novější
- Některá nastavení platí pro macOS 10,15 a novější.
- Tato nastavení se vztahují jenom na zařízení, která mají nainstalovaný profil předvolby ochrany osobních údajů před upgradem.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení schválená uživatelem, automatický zápis zařízení

- **Aplikace a procesy**: **přidejte** aplikace nebo procesy pro konfiguraci přístupu. Dále zadejte:
  - **Název**: zadejte název vaší aplikace nebo procesu. Zadejte například `Microsoft Remote Desktop` nebo `Microsoft 365`.
  
  - **Typ identifikátoru**: vaše možnosti:
    - **ID sady**: tuto možnost vyberte pro aplikace.
    - **Cesta**: tuto možnost vyberte pro neseskupené binární soubory, což je proces nebo spustitelný soubor.

    Podpůrné nástroje vložené do sady prostředků aplikace automaticky přebírají oprávnění k jejich ohraničující sadě prostředků aplikace.

  - **Identifikátor**: Zadejte ID sady prostředků aplikace nebo cestu k instalačnímu souboru procesu nebo spustitelného souboru. Zadejte například `com.contoso.appname`.

    Pokud chcete získat ID sady prostředků aplikace, otevřete aplikaci Terminal a spusťte `codesign` příkaz. Tento příkaz identifikuje podpis kódu. Takže můžete získat ID sady a podpis kódu současně.

  - **Požadavek na kód**: zadejte podpis kódu pro aplikaci nebo proces.

    Podpis kódu se vytvoří, když je aplikace nebo binární podepsána certifikátem vývojáře. Pokud chcete zjistit označení, spusťte `codesign` příkaz ručně v aplikaci Terminal: `codesign --display -r - /path/to/app/binary` . Podpis kódu je vše, co se zobrazí po `=>` .

  - **Povolit ověřování statického kódu**: Pokud chcete aplikaci nebo proces staticky ověřit požadavek kódu, vyberte **Ano** . Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

    Toto nastavení povolte pouze v případě, že proces neověřuje svůj dynamický podpis kódu. V opačném případě použijte **nenakonfigurované**.  

  - **Blokovat kameru**: **Ano** zabraňuje aplikaci v přístupu k systémové kameře. Přístup ke kameře nelze udělit. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  - **Blokovat mikrofon**: **Ano** zabraňuje aplikaci v přístupu k mikrofonu systému. Nemůžete povolený přístup k mikrofonu. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  - **Blokovat nahrávání obrazovky**: **Ano** zablokuje aplikaci, aby zachytává obsah zobrazení systému. Nelze zakázat přístup k záznamu obrazovky a snímku obrazovky. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

    Vyžaduje macOS 10,15 a novější.

  - **Blokovat sledování vstupu**: **Ano** znemožní aplikaci používat rozhraní API CoreGraphics a HID k naslouchání událostem CGEvents a HID ze všech procesů. **Ano** taky zakazuje aplikacím a procesům naslouchat a shromažďovat data ze vstupních zařízení, jako jsou myš, klávesnice nebo trackpadu. Nemůžete povolený přístup k rozhraním API CoreGraphics a HID.

    Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

    Vyžaduje macOS 10,15 a novější.

  - **Rozpoznávání řeči**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k rozpoznávání řeči systému a umožňuje posílání dat řeči do Applu.
    - **Blok**: zabraňuje aplikaci v přístupu k rozpoznávání řeči systému a zabraňuje posílání dat řeči do Applu.

    Vyžaduje macOS 10,15 a novější.

  - **Usnadnění**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k aplikaci pro usnadnění přístupu k systému. Tato aplikace obsahuje skryté titulky, text myši a ovládání hlasu.
    - **Blok**: zabraňuje aplikaci v přístupu k aplikaci pro usnadnění přístupu k systému.

  - **Kontakty**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci získat přístup ke kontaktovým informacím spravovaným aplikací pro kontakty systému.  
    - **Blok**: zabraňuje aplikaci v přístupu k těmto kontaktním informacím.

  - **Kalendář**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci získat přístup k informacím z kalendáře, které spravuje systémová aplikace kalendáře.
    - **Blok**: zabrání aplikaci v přístupu k informacím v kalendáři.

  - **Připomenutí**: máte tyto možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k informacím o připomenutí, které spravuje aplikace systémových připomenutí.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto informacím o připomenutí.

  - **Fotky**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k obrázkům spravovaným aplikací pro fotky systému v `~/Pictures/.photoslibrary` .
    - **Blok**: zabraňuje aplikaci v přístupu k těmto obrázkům.

  - **Knihovna médií**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k aktivitě Apple Music, hudbě a videu a knihovně médií.  
    - **Blok**: zabraňuje aplikaci v přístupu k tomuto médiu.

    Vyžaduje macOS 10,15 a novější.

  - **Přítomnost poskytovatele souborů**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k aplikaci poskytovatele souborů a ví, že uživatelé používají soubory spravované poskytovatelem souborů. Aplikace poskytovatele souborů umožňuje ostatním aplikacím poskytovatele souborů přístup k dokumentům a adresářům uloženým a spravovaným pomocí aplikace, kterou obsahuje.
    - **Blok**: znemožní aplikaci přístup k aplikaci poskytovatele souborů.

    Vyžaduje macOS 10,15 a novější.

  - **Úplný přístup k disku**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup ke všem chráněným souborům, včetně souborů pro správu systému. Toto nastavení použijte opatrně.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto chráněným souborům.

  - **Soubory správce systému**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci získat přístup k některým souborům používaným v nástroji Správa systému.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto souborům.

  - **Plocha složka**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k souborům ve složce plochy daného uživatele.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto souborům.

    Vyžaduje macOS 10,15 a novější.

  - **Složka dokumentů**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k souborům ve složce Dokumenty uživatele.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto souborům.

    Vyžaduje macOS 10,15 a novější.

  - **Složka ke stažení**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: povolí aplikaci přístup k souborům ve složce stažené soubory uživatele.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto souborům.

    Vyžaduje macOS 10,15 a novější.

  - **Síťové svazky**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k souborům na svazcích sítě.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto souborům.

    Vyžaduje macOS 10,15 a novější.

  - **Vyměnitelné svazky**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci přístup k souborům na vyměnitelných svazcích, jako je například pevný disk.
    - **Blok**: zabraňuje aplikaci v přístupu k těmto souborům.

    Vyžaduje macOS 10,15 a novější.

  - **Systémové události**: vaše možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Povolit**: umožňuje aplikaci používat rozhraní API CoreGraphics k odesílání CGEvents do datového proudu systémových událostí.
    - **Blok**: zabraňuje aplikaci v použití rozhraní CoreGraphics API k odeslání CGEvents do datového proudu systémových událostí.

  - **Události Apple**: Toto nastavení umožňuje aplikacím odesílat omezené události Apple do jiné aplikace nebo procesu. Vyberte **Přidat** a přidejte přijímající aplikaci nebo proces. Zadejte následující informace o přijímající aplikaci nebo procesu:

    - **Typ identifikátoru**: vyberte **ID sady prostředků** , pokud je přijímací identifikátor aplikace. Vyberte **cestu** , pokud je přijímací identifikátor proces nebo spustitelný soubor.

    - **Identifikátor**: Zadejte ID sady prostředků aplikace nebo instalační cestu procesu, který přijímá událost Apple.  

    - **Požadavek na kód**: zadejte podpis kódu pro přijímající aplikaci nebo proces.

      Podpis kódu se vytvoří, když je aplikace nebo binární podepsána certifikátem vývojáře. Pokud chcete zjistit označení, spusťte `codesign` příkaz ručně v aplikaci Terminal: `codesign --display -r -/path/to/app/binary` . Podpis kódu je vše, co se zobrazí po `=>` .

    - **Přístup**: povolí odeslání události Apple MacOS do přijímající aplikace nebo procesu. Možnosti:
      - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
      - **Povolit**: umožňuje aplikaci nebo procesu odeslat omezenou událost Apple do přijímající aplikace nebo procesu.
      - **Blok**: znemožní aplikaci nebo procesu odeslání omezené události Apple do přijímající aplikace nebo procesu.

  - **Uložte** změny.

## <a name="restricted-apps"></a>Omezené aplikace

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Typ seznamu omezených aplikací**: vytvoří seznam aplikací, které uživatelé nemůžou instalovat ani používat. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení můžou mít uživatelé přístup k aplikacím, které přiřadíte, a k integrovaným aplikacím.
  - **Schválené aplikace**: seznam aplikací, které můžou uživatelé instalovat. Aby bylo možné zachovat dodržování předpisů, uživatelé nesmí instalovat jiné aplikace. Aplikace spravované přes Intune se automaticky povolují, včetně aplikace Portál společnosti. Uživatelům není znemožněna instalace aplikace, která není na seznamu schválených. Pokud tomu tak je, nahlásí se v Intune.
  - **Zakázané aplikace**: seznam aplikací (nespravovaných pomocí Intune), které uživatelé nemůžou instalovat a spouštět. Uživatelům není instalace zakázané aplikace znemožněna. Pokud uživatel z tohoto seznamu nainstaluje aplikaci, nahlásí se v Intune.

- **Seznam aplikací**: **Přidat** aplikace do seznamu:
  - **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace. Můžete přidat integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).

    Pokud chcete najít adresu URL aplikace, otevřete aplikaci iTunes App Store a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop` nebo `Microsoft Word` . Vyberte aplikaci a zkopírujte adresu URL. K vyhledání aplikace můžete také použít iTunes a potom pomocí úlohy **Kopírovat odkaz** získat adresu URL aplikace.

  - **Název aplikace**: Zadejte popisný název, který vám pomůže dané ID sady prostředků identifikovat. Zadejte například `Intune Company Portal app`.
  - **Vydavatel**: zadejte vydavatele aplikace.

- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app bundle ID>, <app name>, <app publisher>`. Případně můžete **exportovat** a vytvořit seznam aplikací, které jste přidali, ve stejném formátu.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Na zařízeních s [iOS/iPadOS](device-restrictions-ios.md) můžete taky omezit funkce a nastavení zařízení.
