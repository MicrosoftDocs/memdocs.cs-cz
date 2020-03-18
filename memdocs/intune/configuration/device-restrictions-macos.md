---
title: nastavení zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních macOS, abyste omezili funkce, včetně nastavení požadavků na heslo, řízení uzamčené obrazovky, používání integrovaných aplikací, přidávání omezených nebo schválených aplikací, zpracování zařízení Bluetooth, připojení ke cloudu pro zálohování a úložiště, povolit celoobrazovkový režim, přidat domény a řídit, jak uživatelé pracují s webovým prohlížečem Safari v Microsoft Intune.
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
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c4ffe68585d58b4bc61d6302d7772fd2e19855c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332295"
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

- **Vyhledávání definic**: **blok** znemožní uživateli zvýraznit slovo a pak vyhledat jeho definici na zařízení. **Nenakonfigurováno** (výchozí) umožňuje přístup k funkci vyhledávání definic.
- **Diktování**: **blok** zabrání uživateli v použití hlasového vstupu k zadání textu. **Nenakonfigurováno** (výchozí) umožňuje uživateli používat vstup diktování.
- **Ukládání obsahu do mezipaměti**: Pokud chcete povolit ukládání obsahu do mezipaměti, vyberte **nenakonfigurované** (výchozí). Ukládání obsahu do mezipaměti ukládá data aplikací, data webového prohlížeče, soubory ke stažení a další místně na zařízení. Vyberte možnost **blokovat** , pokud chcete zabránit ukládání těchto dat do mezipaměti.

  Další informace o ukládání obsahu do mezipaměti v macOS najdete v tématu [Správa ukládání obsahu do mezipaměti na Macu](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (otevře další web).

  Tato funkce platí pro:  
  - macOS 10,13 a novější

- **Odložit aktualizace softwaru**: Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), v zařízení se zobrazí aktualizace softwaru, které Apple uvolňuje. Pokud se třeba aktualizace macOS uvolní od společnosti Apple k určitému datu, tato aktualizace se přirozeně zobrazuje na zařízení v datu vydání verze. Aktualizace sestavení v počátečním nasazení jsou povoleny bez zpoždění.

  **Možnost Povolit** umožňuje prodlevu při zobrazení aktualizací softwaru na zařízeních, od 0-90 dnů. Toto nastavení neřídí, kdy jsou aktualizace nebo nejsou nainstalovány. 

  - **Zpoždění viditelnosti aktualizací softwaru**: zadejte hodnotu od 0-90 dnů. Po vypršení zpoždění budou uživatelé dostávat oznámení o aktualizaci na nejstarší verzi operačního systému, která je k dispozici při spuštění zpoždění.

    Pokud je například macOS aktualizace k dispozici **1. ledna**a je **zpoždění viditelnosti** nastaveno na **5 dní**, aktualizace se nezobrazí jako dostupná aktualizace. Po **šestém dni** od vydání je tato aktualizace dostupná a koncoví uživatelé ji můžou nainstalovat.

    Tato funkce platí pro:  
    - macOS 10.13.4 a novější

- **Snímky obrazovky**: zařízení musí být zaregistrované v automatickém zápisu zařízení (DEP) společnosti Apple. Když se nastaví **blokování**, uživatelé nemůžou Uložit snímek obrazovky obrazovky. Zabraňuje také aplikaci učeben v pozorování vzdálených obrazovek. **Nenakonfigurováno** (výchozí) umožňuje uživatelům zachytit snímky obrazovky a povolit aplikaci učeben zobrazovat vzdálené obrazovky.

### <a name="settings-apply-to-automated-device-enrollment"></a>Nastavení platí pro: automatický zápis zařízení

- **Sledování vzdálené obrazovky prostřednictvím aplikace učeben**: možnost **Zakázat** brání učitelům v používání aplikace učebny, aby viděli své obrazovky studentů. **Nenakonfigurováno** (výchozí) umožňuje učitelům zobrazit obrazovky studentů.

  Chcete-li použít toto nastavení, nastavte nastavení **snímky obrazovky** na **Nenakonfigurováno** (snímky obrazovky jsou povoleny).

- **Sledování obrazovky s nezodpovězenými obrazovkami podle aplikace učebny**: **umožňuje dovolit** učitelům zobrazit obrazovky studentů, aniž by museli studenta souhlasit. **Nenakonfigurováno** (výchozí) vyžaduje, aby student souhlasil, než uvidí obrazovky učitel.

  Chcete-li použít toto nastavení, nastavte nastavení **snímky obrazovky** na **Nenakonfigurováno** (snímky obrazovky jsou povoleny).

- **Studenti musí požádat o oprávnění k opuštění třídy učebny**: **vyžadovat** u studentů zaregistrovaných v nespravované učebně studia získat schválení učitelů, aby mohl kurz opustit. **Nenakonfigurováno** (výchozí) umožňuje studentům opustit kurz pokaždé, když student zvolí.

- **Učitelé můžou automaticky uzamknout zařízení nebo aplikace v aplikaci učebny**: **Povolit** umožní učitelům uzamknout zařízení nebo aplikaci studenta bez schválení studenta. **Nenakonfigurováno** (výchozí) vyžaduje, aby student souhlasil před tím, než učitel může zařízení nebo aplikaci uzamknout.

- **Studenti můžou automaticky připojit třídu učeben**: **Allow** umožňuje studentům připojit se ke třídě bez výzvy učitelům. **Není nakonfigurováno** (výchozí) vyžaduje schválení učitelů pro připojení ke třídě.

## <a name="password"></a>Heslo

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Heslo**: **vyžaduje** , aby koncový uživatel zadal heslo pro přístup k zařízení. **Nenakonfigurováno** (výchozí) nevyžaduje heslo. Také nevynucuje žádná omezení, jako je například blokování jednoduchých hesel nebo nastavení minimální délky.
  - **Vyžadovaný typ hesla**: Určuje, jestli může být jenom číselné heslo nebo jestli musí být alfanumerické (obsahovat písmena a číslice).

    Tato funkce platí pro:  
    - macOS 10.10.3 a novější

  - **Počet nealfanumerických znaků v hesle**: zadejte počet složitých znaků vyžadovaných v hesle (**0** až **4**).<br>Složitý znak je symbol, například **?** .
  - **Minimální délka hesla**: zadejte minimální délku hesla, které uživatel musí nakonfigurovat (mezi **4** a **16** znaky).
  - **Jednoduchá hesla**: povolí použití jednoduchých hesel, jako je **0000** nebo **1234**.
  - **Maximální počet minut po uzamčení obrazovky, než se požaduje heslo**: Určete, jak dlouho musí být počítač neaktivní, než bude nutné heslo odemknout.
  - **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte dobu, po kterou musí být počítač nečinný, než se zamkne obrazovka.
  - **Vypršení platnosti hesla (dny)** : zadejte počet dnů, po jejichž uplynutí musí uživatel změnit heslo (**1** až **255** dní).
  - **Zakázat opakované použití předchozích hesel**: zadejte počet dříve použitých hesel, která se nesmí znovu použít, od **1** do **24**.

- **Zablokovat uživateli změnu hesla**: vyberte **blok** pro zastavení změny, přidání nebo odebrání hesla. **Nenakonfigurováno** (výchozí) umožňuje přidávat, měnit a odebírat hesla.
- **Blokovat odemknutí otiskem prstu**: vyberte **blok** , abyste zabránili použití otisku prstu k odemknutí zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživateli odemknout zařízení pomocí otisku prstu.

- **Blokovat automatické vyplňování hesel**: Pokud chcete zabránit použití funkce automatického vyplňování hesel na MacOS, vyberte **blokovat** . Výběr **bloku** má také následující dopad:

  - Uživatelům se nezobrazí výzva k použití uloženého hesla v Safari nebo ve všech aplikacích.
  - Automatická silná hesla jsou zakázaná a silná hesla se uživatelům nedoporučují.

  **Není nakonfigurováno** (výchozí) tyto funkce povolují.

- **Zablokovat žádosti o blízkost hesla**: zvolit **blok** , aby zařízení uživatele nepožadovalo hesla z blízkých zařízení. **Nenakonfigurováno** (výchozí) povoluje tyto požadavky na heslo.

- **Blokování sdílení hesel**: **blok** zabraňuje sdílení hesel mezi zařízeními pomocí přetažení. **Nenakonfigurováno** (výchozí) umožňuje sdílet hesla.

## <a name="built-in-apps"></a>Integrované aplikace

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Blokovat automatické vyplňování prohlížeče Safari**: **blok** zakáže funkci automatického vyplňování v prohlížeči Safari na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům změnit nastavení automatického dokončování ve webovém prohlížeči.
- **Blokovat kameru**: vyberte možnost **blokovat** , pokud chcete zabránit přístupu k fotoaparátu na zařízení. **Nenakonfigurováno** (výchozí) umožňuje přístup k kameře zařízení.
- **Block Apple Music**: **Block** vrátí aplikaci v hudbě do klasického režimu a zakáže hudební službu. **Nenakonfigurováno** (výchozí) umožňuje použití aplikace Apple Music.
- **Zablokovat výsledky hledání na internetu**: **blok** zastaví vracení všech výsledků z Internetu hledáním. **Nenakonfigurováno** (výchozí) umožňuje vyhledávání Spotlightu připojit se k Internetu a poskytnout tak výsledky hledání.
- **Blokovat přenos souborů pomocí iTunes**: **blokování** zakáže služby pro sdílení souborů aplikací. **Nenakonfigurováno** (výchozí) povolí služby pro sdílení souborů aplikací.

  Tato funkce platí pro:  
  - macOS 10,13 a novější

## <a name="restricted-apps"></a>Omezené aplikace

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Typ seznamu omezených aplikací**: vytvoří seznam aplikací, které uživatelé nemůžou instalovat ani používat. Možnosti:

  - **Nenakonfigurováno** (výchozí): neexistují žádná omezení z Intune. Uživatelé mají přístup k aplikacím, které přiřadíte, a k integrovaným aplikacím.
  - **Zakázané aplikace**: aplikace nespravované přes Intune, které nechcete v zařízení nainstalovat. Uživatelům není instalace zakázané aplikace znemožněna. Pokud ale uživatel z tohoto seznamu nainstaluje aplikaci, nahlásí se v Intune.
  - **Schválené aplikace**: aplikace, které můžou uživatelé instalovat. Uživatelé nesmí instalovat aplikace, které nejsou uvedené. Aplikace, které spravuje Intune, jsou povolené automaticky. Uživatelům není znemožněna instalace aplikace, která není na seznamu schválených. Pokud tomu tak je, nahlásí se v Intune.
- **ID sady prostředků aplikace**: zadejte [ID sady prostředků](bundle-ids-built-in-ios-apps.md) aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Název aplikace**: zadejte název aplikace, kterou chcete. Můžete zobrazit nebo skrýt integrované aplikace a obchodní aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
- **Vydavatel**: zadejte vydavatele aplikace, kterou chcete.

Pokud chcete do těchto seznamů přidat aplikace, můžete:

- **Přidat**: vyberte, pokud chcete vytvořit seznam aplikací.
- **Importujte** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte formát `<app bundle ID>, <app name>, <app publisher>`. Případně můžete **exportovat** a vytvořit seznam aplikací, které jste přidali, ve stejném formátu.

## <a name="connected-devices"></a>Připojená zařízení

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Blokovat přetažení**: **blok** zabraňuje použití přetahování na zařízení. **Nenakonfigurováno** (výchozí) umožňuje použití funkce prohodit pro výměnu obsahu s blízkými zařízeními.
- **Blokovat Apple Watch automatické odemknutí**: **blok** zabraňuje uživatelům v odemknutí zařízení MacOS pomocí jejich Apple Watch. **Nenakonfigurováno** (výchozí) umožňuje uživatelům odemknout zařízení MacOS pomocí jejich Apple Watch.

## <a name="cloud-and-storage"></a>Cloud a úložiště

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Blokovat synchronizaci řetězce klíčů iCloud**: Pokud chcete zakázat synchronizaci přihlašovacích údajů uložených v řetězci klíčů do iCloud, vyberte **blok** . **Nenakonfigurováno** (výchozí) umožňuje uživatelům synchronizovat tyto přihlašovací údaje.
- **Blokovat synchronizaci dokumentů iCloud**: **blok** zabraňuje tomu, aby iCloud Synchronization Documents and data. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci dokumentu a klíč-hodnota do iCloud prostoru úložiště.
- **Zablokovat zálohování pošty iCloud**: **blok** brání v synchronizaci iCloud do aplikace MacOS mail. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci pošty do iCloud.
- **Blokovat zálohování kontaktů iCloud**: **blok** zabraňuje iCloud synchronizaci kontaktů zařízení. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci kontaktů pomocí iCloud.
- **Zablokovat zálohování kalendáře iCloud**: **blok** brání v synchronizaci iCloud do aplikace kalendáře MacOS. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci kalendáře do iCloud.
- **Zablokovat zálohování připomenutí iCloud**: **blok** brání v synchronizaci iCloud do aplikace MacOS s připomenutími. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci připomenutí do iCloud.
- **Zablokovat zálohování záložek iCloud**: **blok** zabraňuje iCloud synchronizaci záložek zařízení. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci záložek iCloud.
- **Zablokovat zálohování poznámek iCloud**: **blok** zabraňuje iCloud synchronizaci poznámek zařízení. **Nenakonfigurováno** (výchozí) umožňuje synchronizaci poznámek s iCloud.
- **Blokovat knihovnu fotografií iCloud**: **Block** zakáže knihovnu fotografií iCloud a zabrání iCloud synchronizaci fotek zařízení. Všechny fotky, které nejsou plně stažené z knihovny fotografií iCloud, se z místního úložiště na zařízení odeberou. **Nenakonfigurováno** (výchozí) umožňuje synchronizovat fotky mezi zařízením a knihovnou fotek iCloud.
- **Předání**: **Nenakonfigurováno** (výchozí) umožňuje uživatelům začít pracovat na zařízení MacOS a potom pokračovat v práci, kterou zahájil na jiném zařízení s iOS/iPadOS nebo MacOS. **Blok** zabraňuje funkci předání na zařízení. 

  Tato funkce platí pro:  
  - macOS 10,15 a novější

## <a name="domains"></a>Domény

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **Adresa URL e-mailové domény**: **přidejte** do seznamu jednu nebo víc adres URL. Když uživatelé dostanou e-mail z jiné domény než z toho, kterou jste nakonfigurovali, označí se v aplikaci macOS mail e-mail jako nedůvěryhodný.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Na zařízeních s [iOS/iPadOS](device-restrictions-ios.md) můžete taky omezit funkce a nastavení zařízení.
