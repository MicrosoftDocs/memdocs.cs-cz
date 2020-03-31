---
title: Nastavení omezení pro zařízení s Windows Phone 8.1 v Microsoft Intune
titleSuffix: ''
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete řídit nastavení a funkce na zařízeních s Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 285144e42f2a029bf2d24b96493c54922727d6dc
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407642"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Nastavení omezení pro zařízení Windows Phone 8.1 v Microsoft Intune

Tento článek ukazuje nastavení omezení zařízení v Microsoft Intune, která můžete nakonfigurovat pro zařízení s Windows Phone 8.1.

## <a name="general"></a>Obecné

- **Kamera**: **Block** zabrání přístupu k fotoaparátu zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.

- **Kopírování a vkládání**: **blok** zabraňuje použití kopírování a vkládání mezi aplikacemi na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Vyměnitelné úložiště**: **blok** zabraňuje použití externích úložných zařízení v zařízeních, jako jsou SD karty. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Zeměpisná poloha**: **blok** zabraňuje zapnutí služby zjišťování polohy na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Účet Microsoft**: **blok** zabraňuje uživatelům v přidružení účet Microsoft k zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Snímek obrazovky**: **zablokování** znemožňuje získání snímků obrazovky na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Odeslání diagnostických dat**: **bloková** zařízení brání odesílání diagnostických dat a využití telemetrie do Microsoftu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Vlastní e-mailové účty synchronizace**: **blokovat** brání zařízením v připojení k e-mailovým účtům jiným než Microsoftu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="password"></a>Heslo

- **Heslo**: **vyžaduje** , aby uživatelé zadali heslo pro přístup k zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Platí jenom pro místní účty. Hesla doménového účtu zůstávají nakonfigurovaná službou Active Directory (AD) a službou Azure AD.
  - **Vyžadovaný typ hesla**: Vyberte typ hesla. Možnosti:
    - **Výchozí nastavení zařízení**: heslo může obsahovat číslice a písmena.
    - **Alfanumerické**: heslo musí být kombinací číslic a písmen.
    - **Číselná**: heslo musí obsahovat pouze čísla.
  - **Minimální délka hesla**: zadejte minimální počet požadovaných znaků od 4-16. Zadejte například `6` pro vyžadování aspoň šesti znaků v délce hesla.
  - **Jednoduchá hesla**: **blok** znemožní uživatelům vytvářet jednoduchá hesla, například `1234` nebo `1111`. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet chybných hesel povolených před vymazáním zařízení.
  - **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte dobu, po kterou musí být zařízení nečinné, než se automaticky uzamkne obrazovka. Zadejte například `5` pro uzamčení zařízení po 5 minutách nečinnosti. Pokud je tato možnost nastavená na hodnotu **není nakonfigurované** nebo je ponecháno prázdné, Intune se nezmění ani neaktualizuje.
  - **Vypršení platnosti hesla (dny)** : zadejte dobu ve dnech, kdy musí být heslo zařízení změněno, od 1-255. Zadejte například `90` vypršení platnosti hesla po 90 dnech. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
  - **Zakázat opakované použití předchozích hesel**: zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Zadejte například `5`, takže uživatelé nemůžou nastavit nové heslo nebo některá z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Šifrování**: **vyžadovat** šifrování u zařízení, včetně souborů. Ne všechna zařízení podporují šifrování. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud chcete nakonfigurovat toto nastavení a správně ohlásit dodržování předpisů, nakonfigurujte taky:
  - **Vyžadovat heslo**: nastavte na **vyžadovat**.
  - **Požadovaný typ hesla**: Nastavte aspoň na **číslo**.
  - **Minimální délka hesla**: nastavte aspoň `4`.

## <a name="app-store"></a>App Store

- **App Storu**: **blok** zabraňuje uživatelům v přístupu k obchodu s aplikacemi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="restricted-apps"></a>Omezené aplikace

V seznamu omezených aplikací můžete nakonfigurovat jeden z následujících seznamů:

- **Blokované aplikace**: seznam aplikací (nespravovaných pomocí Intune), které nemají uživatelé dovolené nainstalovat a spustit.
- **Povolené aplikace**: seznam aplikací, které můžou uživatelé instalovat. Aplikace, které spravuje Intune, jsou povolené automaticky.

Pokud chcete seznam nakonfigurovat, klikněte na **Přidat**, zadejte libovolný název, volitelně vydavatele aplikace a nakonec adresu URL aplikace v App Storu.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Jak zadat adresu URL pro aplikaci ve Storu

Pokud chcete zadat adresu URL aplikace do seznamu povolených a blokovaných aplikací, použijte následující formát:

Na stránce [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) najděte aplikaci, kterou chcete použít.

Otevřete stránku aplikace a zkopírujte adresu URL do schránky. Tuto adresu URL teď můžete použít jako adresu URL v seznamu povolených nebo blokovaných aplikací.

Příklad: Vyhledání aplikace Skype ve Storu. Použijete tuto adresu URL: `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Další možnosti

Můžete taky kliknout na **importovat** a naplnit seznam ze souboru CSV ve formátu <*URL aplikace*>, <*název aplikace*>, <*vydavatele aplikace*>, nebo kliknout na **exportovat** a vytvořit soubor CSV obsahující obsah seznamu aplikací s omezeným přístupem ve stejném formátu.

## <a name="browser"></a>Prohlížeč

- **Webový prohlížeč**: **blokování** vypne integrovaný webový prohlížeč na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="cellular-and-connectivity"></a>Mobilní síť a připojení

- **Wi-Fi**: **Block** zakáže funkce Wi-Fi na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Sdílení internetového připojení přes Wi-Fi**: **blok** zabraňuje použití internetového připojení Wi-Fi na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Automaticky se připojovat k Wi-Fi hotspotům**: umožňuje zařízením automaticky se připojovat k bezplatným Wi-Fi hotspotům a automaticky přijímat jakékoli podmínky použití.
- **Vytváření sestav Wi-Fi hotspotů**: **blokování** brání zařízením v odesílání informací o připojení hotspotů Wi-Fi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **NFC**: **Block** zakáže operace, které na zařízeních, které ji podporují, používají technologii NFC (The-Field Communication). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Bluetooth**: **blok** znemožní uživatelům povolit Bluetooth. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="next-steps"></a>Další kroky

Obecný přehled profilu omezení zařízení najdete v tématu [Konfigurace nastavení omezení zařízení v Microsoft Intune](device-restrictions-configure.md).
