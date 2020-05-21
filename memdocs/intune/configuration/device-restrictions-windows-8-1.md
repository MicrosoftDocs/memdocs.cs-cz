---
title: Windows 8.1 nastavení omezení pro zařízení v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete řídit nastavení a funkce na zařízeních s Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36a74e503f15fe982eeaf1addfed40d0c599cb2c
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556230"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Nastavení omezení Microsoft Intune Windows 8.1 zařízení

V tomto článku se dozvíte, jak Microsoft Intune nastavení omezení zařízení, která můžete nakonfigurovat pro zařízení s Windows 8.1.

## <a name="before-you-begin"></a>Před zahájením

[Vytvoří konfigurační profil omezení zařízení Windows 8.1](device-restrictions-configure.md#create-the-profile).

## <a name="general"></a>Obecné

- **Sdílet data o využití**: **blokovat** zabrání zařízením v odesílání diagnostických informací a informací o využití telemetrie společnosti Microsoft. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Brána firewall**: **vyžaduje** zapnutí brány Windows Firewall. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Řízení uživatelských účtů**: konfiguruje řízení uživatelských účtů (UAC). Vyberte způsob upozorňování uživatelů na změny v zařízeních. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Vždy upozorňovat**
  - **Upozorňovat na změny aplikace**
  - **Upozorňovat na změny aplikace, ale neztlumit plochu**
  - **Nikdy neupozorňovat**

## <a name="password"></a>Heslo

- **Vyžadovaný typ hesla**: Určete, jestli uživatel musí pro přístup k zařízení zadat heslo. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Alfanumerické**: heslo musí být kombinací číslic a písmen.
  - **Číselná**: heslo musí obsahovat pouze čísla.
- **Minimální délka hesla**: zadejte minimální počet požadovaných znaků od 6-16. Zadejte například, pokud `6` chcete pro délku hesla vyžadovat alespoň šest číslic nebo znaků.
- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet chybných hesel povolených před vymazáním zařízení, od 1-14.
- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka (v minutách)**: zadejte dobu, po kterou musí být zařízení nečinné, než se automaticky uzamkne obrazovka, od 1-60 minut. Zadejte například, `5 Minutes` Pokud chcete zařízení uzamknout po 5 minutách nečinnosti. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.
- **Vypršení platnosti hesla (dny)**: zadejte dobu ve dnech, kdy musí být heslo zařízení změněno, od 1-255. Zadejte například `90` platnost hesla po 90 dnech. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Zakázat opakované použití předchozích hesel**: zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Například zadejte, `5` že uživatelé nemůžou nastavit nové heslo na aktuální heslo ani na žádná z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Obrázkové heslo a PIN**: obrázkové heslo umožňuje uživateli přihlašovat se gesty na obrázku. Kód PIN umožňuje uživatelům rychlé přihlášení pomocí čtyřmístného kódu.

  **Blok** zabraňuje použití obrázku nebo PIN kódu jako hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

- **Šifrování**: **vyžaduje** šifrování u zařízení, včetně souborů. Ne všechna zařízení podporují šifrování. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje.

  Pokud chcete nakonfigurovat toto nastavení a správně ohlásit dodržování předpisů, nakonfigurujte taky:

  - **Požadovaný typ hesla**: Nastavte aspoň na **číslo**.
  - **Minimální délka hesla**: Nastavte aspoň na `6` .

  K vynucení šifrování na zařízeních s Windows 8.1 je potřeba na každé zařízení nainstalovat [aktualizaci MDM klienta pro Windows z prosince 2014](https://support.microsoft.com/kb/3013816) .

  Pokud toto nastavení povolíte pro zařízení s Windows 8.1, všichni uživatelé zařízení musí mít účet Microsoft.

  Aby šifrování fungovalo, musí zařízení splňovat požadavky na certifikaci hardwaru [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) .

  Pokud vynutíte šifrování na zařízení, je obnovovací klíč přístupný jenom uživatelům s účtem Microsoft, ke kterému přistupují z účtu na Onedrivu. Tento klíč nemůžete obnovit pro uživatele.

## <a name="browser"></a>Prohlížeč

- Automatické vyplňování: **blok** znemožní uživatelům měnit nastavení automatického dokončování v prohlížeči a automaticky **naplnit**pole formuláře. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automatické vyplňování.
- **Upozornění na podvod**: **vyžaduje, aby** v prohlížeči byla zobrazena upozornění podvodů pro potenciální podvodné weby. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Filtr SmartScreen pro Microsoft Edge**: **blok** vypne filtr SmartScreen v programu Microsoft Defender. Filtr SmartScreen při přístupu k webům a stahování souborů vyhledává potenciální podvodné zprávy a škodlivý software. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout filtr SmartScreen.
- **Allow JavaScript**: **Block** zabrání v prohlížeči spouštění skriptů, jako je například JavaScript. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat jazyk JavaScript.
- **Automaticky otevíraná**okna: **blok** zapne blokování automaticky otevíraných oken, aby se zabránilo automaticky otevíraná okna ve webovém prohlížeči. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Hlavičky do Not Track**: **blok** zabraňuje zařízením v posílání hlaviček do Not Track pro weby požadující informace o sledování. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Moduly plug**-in: **blokovat** znemožní uživatelům přidávat do Internet Exploreru moduly plug-in. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Položka s jedním slovem na intranetovém webu**: jedna položka umožňující uživatelům přejít na intranetový web zadáním jediného slova, například `hr` nebo `benefits` . **Blokování** brání této funkci. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Automatické zjišťování intranetového webu**: **blok** zabraňuje automatickému zjišťování intranetových webů v prohlížeči. Pravidla mapování intranetu jsou blokovaná. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Úroveň zabezpečení v Internetu**: nastaví úroveň zabezpečení internetových serverů. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Maximální**
  - **Střední-vysoká**
  - **Medium**
- **Úroveň zabezpečení intranetu**: nastaví úroveň zabezpečení intranetových serverů. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Nízká**
  - **Středně nízká**
  - **Medium**
  - **Střední-vysoká**
  - **Maximální**
- **Úroveň zabezpečení důvěryhodných serverů**: konfiguruje úroveň zabezpečení pro zónu důvěryhodných lokalit. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Nízká**
  - **Středně nízká**
  - **Medium**
  - **Střední-vysoká**
  - **Maximální**
- **Vysoké zabezpečení pro weby s omezeným přístupem**: konfiguruje úroveň zabezpečení pro zónu lokalit s omezeným přístupem. **Konfigurace** vynutila vysoké zabezpečení pro weby s omezeným přístupem. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Přístup z nabídky podnikového režimu**: **blok** znemožní uživatelům přístup k možnostem nabídky podnikového režimu v Internet Exploreru. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Pokud je nastavena na hodnotu **není nakonfigurováno**, zadejte také:

  - **Adresa URL umístění sestavy protokolování**: zadejte umístění adresy URL, kam chcete získat sestavy, které zobrazují weby s povoleným přístupem v podnikovém režimu.

- **Umístění seznamu webů podnikového režimu (jenom desktopové verze)**: zadejte umístění seznamu webů, které se dají otevřít v podnikovém režimu.

## <a name="cellular"></a>Mobilní služby

- **Datový roaming**: **blok** znemožní datový roaming, když jsou zařízení v mobilní síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="cloud-and-storage"></a>Cloud a úložiště

- **Adresa URL pracovních složek**: zadejte adresu URL pracovní složky, aby bylo možné synchronizovat dokumenty na všech zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí) nebo je ponecháno prázdné, Intune se nezmění ani neaktualizuje toto nastavení.
- **Přístup k aplikaci Windows Mail bez účet Microsoft**: **blok** znemožní přístup k aplikaci Windows Mail bez účet Microsoft. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="next-steps"></a>Další kroky

Vytvořte profil omezení zařízení ve [Windows 10 a novějším](device-restrictions-windows-10.md).
