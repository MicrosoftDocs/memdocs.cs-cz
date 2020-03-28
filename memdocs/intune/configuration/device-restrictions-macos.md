---
title: nastavení zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních macOS, abyste omezili funkce, včetně nastavení požadavků na heslo, řízení uzamčené obrazovky, používání integrovaných aplikací, přidávání omezených nebo schválených aplikací, zpracování zařízení Bluetooth, připojení ke cloudu pro zálohování a úložiště, povolit celoobrazovkový režim, přidat domény a řídit, jak uživatelé pracují s webovým prohlížečem Safari v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7054cb658314d00c3e10388c50c2309038c8a15b
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359126"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>macOS nastavení zařízení pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popisuje různá nastavení, která můžete řídit na zařízeních macOS. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, nastavit pravidla pro hesla, povolit nebo omezit konkrétní aplikace a další.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí do zařízení macOS.

## <a name="before-you-begin"></a>Před zahájením

[Vytvoří konfigurační profil omezení zařízení](device-restrictions-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace. Další informace o různých typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="general"></a>Obecné

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Vyhledávání definic**: **blok** znemožní uživateli zvýraznit slovo a pak vyhledat jeho definici na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat funkci vyhledávání definic.
- **Diktování**: **blok** zabrání uživatelům v použití hlasového vstupu k zadání textu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit použít vstup diktování.
- **Ukládání obsahu do mezipaměti**: **blok** zabraňuje ukládání obsahu do mezipaměti. Ukládání obsahu do mezipaměti ukládá data aplikací, data webového prohlížeče, soubory ke stažení a další lokálně na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit ukládání obsahu do mezipaměti.

  Další informace o ukládání obsahu do mezipaměti v macOS najdete v tématu [Správa ukládání obsahu do mezipaměti na Macu](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (otevře další web).

  Tato funkce platí pro:  
  - macOS 10,13 a novější

- **Odložení aktualizací softwaru**: **možnost Povolit** umožňuje zpozdit, kdy se na zařízeních zobrazí aktualizace softwaru, od 0-90 dnů. Toto nastavení neřídí, kdy jsou aktualizace nebo nejsou nainstalovány. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních zobrazovat aktualizace, když je Apple uvolňuje. Pokud se třeba aktualizace macOS uvolní od společnosti Apple po konkrétní datum, pak se tato aktualizace přirozeně zobrazuje na zařízeních v datu vydání verze. Aktualizace sestavení v počátečním nasazení jsou povoleny bez zpoždění.  

  - **Zpoždění viditelnosti aktualizací softwaru**: zadejte hodnotu od 0-90 dnů. Po vypršení zpoždění budou uživatelé dostávat oznámení o aktualizaci na nejstarší verzi operačního systému, která je k dispozici při spuštění zpoždění.

    Pokud je například macOS aktualizace k dispozici **1. ledna**a je **zpoždění viditelnosti** nastaveno na **5 dní**, aktualizace se nezobrazí jako dostupná aktualizace. Po **šestém dni** od vydání je tato aktualizace dostupná a uživatelé ji můžou nainstalovat.

    Tato funkce platí pro:  
    - macOS 10.13.4 a novější

- **Snímky obrazovky**: zařízení musí být zaregistrované v automatickém zápisu zařízení (DEP) společnosti Apple. **Blok** zabraňuje uživatelům ukládat snímky obrazovky obrazovky. Zabraňuje také aplikaci učeben v pozorování vzdálených obrazovek. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit zachytit snímky obrazovky a umožňuje aplikaci učeben zobrazit vzdálené obrazovky.

### <a name="settings-apply-to-automated-device-enrollment"></a>Nastavení platí pro: automatický zápis zařízení

- **Sledování vzdálené obrazovky prostřednictvím aplikace učeben**: možnost **Zakázat** brání učitelům v používání aplikace učebny, aby viděli své obrazovky studentů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém může učitelům dovolit zobrazit své obrazovky studentů.

  Chcete-li použít toto nastavení, nastavte nastavení **snímky obrazovky** na **Nenakonfigurováno** (snímky obrazovky jsou povoleny).

- **Sledování obrazovky s nezodpovězenými obrazovkami podle aplikace učebny**: **umožňuje dovolit** učitelům zobrazit obrazovky studentů, aniž by se museli dohodnout na studenty. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při zobrazení obrazovky učitelům vyžadovat, aby studenti mohli souhlasit.

  Chcete-li použít toto nastavení, nastavte nastavení **snímky obrazovky** na **Nenakonfigurováno** (snímky obrazovky jsou povoleny).

- **Studenti musí požádat o oprávnění k opuštění třídy učebny**: **vyžadovat** u studentů zaregistrovaných v nespravované učebně studia získat schválení učitelů, aby mohl kurz opustit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při každém výběru studenta dovolit kurzu opustit kurz.

- **Učitelé můžou automaticky uzamknout zařízení nebo aplikace v aplikaci učebny**: **Povolit** umožní učitelům uzamknout zařízení nebo aplikaci studenta bez schválení studenta. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vyžadovat, aby studenti před tím, než si můžou zařízení nebo aplikaci uzamknout, museli souhlasit.

- **Studenti můžou automaticky připojit třídu učeben**: **Allow** umožňuje studentům připojit se ke třídě bez výzvy učitelům. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vyžadovat schválení učitelů pro připojení ke třídě.

## <a name="password"></a>Heslo

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Heslo**: **vyžaduje** , aby uživatelé zadali heslo pro přístup k zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat heslo. Také nevynucuje žádná omezení, jako je například blokování jednoduchých hesel nebo nastavení minimální délky.
  - **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla, kterou vaše organizace vyžaduje. Možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
    - **Číselná**: heslo musí obsahovat jenom čísla, třeba 123456789.
    - **Alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice.

    Tato funkce platí pro:  
    - macOS 10.10.3 a novější

  - **Počet nealfanumerických znaků v hesle**: zadejte počet složitých znaků vyžadovaných v hesle, od 0-4. Složitý znak je symbol, například `?`
  - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4-16 znaků.
  - **Jednoduchá hesla**: umožňuje používat jednoduchá hesla, například `0000` nebo `1234`.
  - **Maximální počet minut po uzamčení obrazovky, než se požaduje heslo**: zadejte dobu, po kterou musí být zařízení neaktivní, než bude nutné heslo odemknout. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.
  - **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte dobu, po kterou musí být zařízení nečinné, než se obrazovka automaticky zamkne. Zadejte například hodnotu 5 pro uzamčení zařízení po 5 minutách nečinnosti. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.
  - **Vypršení platnosti hesla (dny)** : zadejte počet dní, než bude nutné změnit heslo zařízení, od 1-65535. Zadejte například `90` vypršení platnosti hesla po 90 dnech. Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
  - **Zakázat opakované použití předchozích hesel**: pomocí tohoto nastavení můžete uživatelům zabránit ve vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Zadejte například hodnotu 5, aby uživatelé nemohli nastavit nové heslo, nebo některá z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.

- **Zablokovat uživateli změnu hesla**: **blok** zastaví změnu hesla, přidání nebo odebrání hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidat, změnit nebo odebrat hesla.
- **Blokovat odemknutí otiskem prstu**: **blok** zabraňuje použití otisků prstů k odemknutí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby zařízení odemkli pomocí otisku prstu.

- **Blokovat automatické vyplňování hesla**: **blok** zabraňuje použití funkce automatického vyplňování hesel na MacOS. Výběr **bloku** má také následující dopad:

  - Uživatelům se nezobrazí výzva k použití uloženého hesla v Safari nebo ve všech aplikacích.
  - Automatická silná hesla jsou zakázaná a silná hesla se uživatelům nedoporučují.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto funkce dovolit.

- **Zablokovat žádosti o blízkost k heslům**: **blok** znemožní zařízením vyžadovat hesla z okolních zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto požadavky na heslo způsobit.

- **Blokování sdílení hesel**: **blok** zabraňuje sdílení hesel mezi zařízeními pomocí přetažení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat sdílení hesel.

## <a name="built-in-apps"></a>Integrované aplikace

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Blokovat automatické vyplňování prohlížeče Safari**: **blok** zakáže funkci automatického vyplňování v prohlížeči Safari na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení automatického dokončování ve webovém prohlížeči.
- **Block Camera**: **Block** zabrání přístupu ke kameře na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k kameře zařízení.
- **Block Apple Music**: **Block** vrátí aplikaci v hudbě do klasického režimu a zakáže hudební službu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití aplikace Apple Music.
- **Zablokovat výsledky hledání na internetu**: **blok** zastaví vracení všech výsledků z Internetu hledáním. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat připojení Spotlightu k Internetu a získání výsledků hledání.
- **Blokovat přenos souborů pomocí iTunes**: **blokování** zakáže služby pro sdílení souborů aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat služby sdílení souborů aplikací.

  Tato funkce platí pro:  
  - macOS 10,13 a novější

## <a name="restricted-apps"></a>Omezené aplikace

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Typ seznamu omezených aplikací**: vytvoří seznam aplikací, které uživatelé nemůžou instalovat ani používat. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení můžou mít uživatelé přístup k aplikacím, které přiřadíte, a k integrovaným aplikacím.
  - **Zakázané aplikace**: seznam aplikací (nespravovaných pomocí Intune), které uživatelé nemůžou instalovat a spouštět. Uživatelům není instalace zakázané aplikace znemožněna. Pokud uživatel z tohoto seznamu nainstaluje aplikaci, nahlásí se v Intune.
  - **Schválené aplikace**: seznam aplikací, které můžou uživatelé instalovat. Aby bylo možné zachovat dodržování předpisů, uživatelé nesmí instalovat jiné aplikace. Aplikace spravované přes Intune se automaticky povolují, včetně aplikace Portál společnosti. Uživatelům není znemožněna instalace aplikace, která není na seznamu schválených. Pokud tomu tak je, nahlásí se v Intune.

- **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Název aplikace**: zadejte název aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Vydavatel**: zadejte vydavatele aplikace.

Pokud chcete do těchto seznamů přidat aplikace, můžete:

- **Přidat**: vyberte, pokud chcete vytvořit seznam aplikací.
- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app bundle ID>, <app name>, <app publisher>`. Případně můžete **exportovat** a vytvořit seznam aplikací, které jste přidali, ve stejném formátu.

## <a name="connected-devices"></a>Připojená zařízení

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Blokovat přetažení**: **blok** zabraňuje použití přetahování na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít funkci přetažení, která umožňuje výměnu obsahu s okolními zařízeními.
- **Blokovat Apple Watch automatické odemknutí**: **blok** zabraňuje uživatelům v odemknutí zařízení MacOS pomocí jejich Apple Watch. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit odemknout zařízení macOS pomocí jejich Apple Watch.

## <a name="cloud-and-storage"></a>Cloud a úložiště

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Blokovat synchronizaci řetězce klíčů iCloud**: **blok** zakáže synchronizaci přihlašovacích údajů uložených v řetězci klíčů do iCloud. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožňovat synchronizaci těchto přihlašovacích údajů.
- **Blokovat synchronizaci dokumentů iCloud**: **blok** zabraňuje tomu, aby iCloud Synchronization Documents and data. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci dokumentu a klíč-hodnota do iCloud prostoru úložiště.
- **Zablokovat zálohování pošty iCloud**: **blok** brání v synchronizaci iCloud do aplikace MacOS mail. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci pošty iCloud.
- **Zablokovat zálohování kontaktů iCloud**: **blok** brání iCloud v synchronizaci kontaktů zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci kontaktů pomocí iCloud.
- **Zablokovat zálohování kalendáře iCloud**: **blok** brání v synchronizaci iCloud do aplikace kalendáře MacOS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit synchronizaci kalendáře do iCloud.
- **Zablokovat zálohování připomenutí iCloud**: **blok** brání v synchronizaci iCloud do aplikace MacOS s připomenutími. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci připomenutí do iCloud.
- **Zablokovat zálohování záložek iCloud**: **blok** zabraňuje iCloud synchronizaci záložek zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci záložek do iCloud.
- **Zablokovat zálohování poznámek iCloud**: **blok** zabraňuje iCloud synchronizaci poznámek zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci poznámek s iCloud.
- **Blokovat knihovnu fotografií iCloud**: **Block** zakáže knihovnu fotografií iCloud a zabrání iCloud synchronizaci fotek v zařízení. Všechny fotky, které nejsou plně stažené z knihovny fotografií iCloud, se z místního úložiště na zařízeních odeberou. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat synchronizaci fotek mezi zařízením a knihovnou fotek iCloud.
- **Předání**: Tato funkce umožňuje uživatelům začít pracovat na zařízení MacOS a potom pokračovat v práci, kterou zahájil na jiném zařízení s iOS/IPadOS nebo MacOS. **Blok** zabraňuje funkci předání na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci na zařízeních dovolit.

  Tato funkce platí pro:  
  - macOS 10,15 a novější

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Adresa URL e-mailové domény**: **přidejte** do seznamu jednu nebo víc adres URL. Když uživatelé dostanou e-mail z jiné domény než z toho, kterou jste nakonfigurovali, označí se v aplikaci macOS mail e-mail jako nedůvěryhodný.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Na zařízeních s [iOS/iPadOS](device-restrictions-ios.md) můžete taky omezit funkce a nastavení zařízení.
