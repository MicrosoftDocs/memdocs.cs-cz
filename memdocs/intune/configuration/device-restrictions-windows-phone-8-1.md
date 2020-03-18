---
title: Nastavení omezení pro zařízení s Windows Phone 8.1 v Microsoft Intune
titleSuffix: ''
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete řídit nastavení a funkce na zařízeních s Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3696ebf52ee093befc3b6eadc6d1a5041d5929e9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333127"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Nastavení omezení pro zařízení Windows Phone 8.1 v Microsoft Intune



Tento článek ukazuje nastavení omezení zařízení v Microsoft Intune, která můžete nakonfigurovat pro zařízení s Windows Phone 8.1.


## <a name="general"></a>Obecné

- **Kamera** – Povolí nebo zablokuje fotoaparát zařízení.
- **Kopírování a vložení** – Povolí nebo zablokuje funkci kopírování a vkládání na zařízeních.
- **Vyměnitelné úložiště** – Povolí použití vyměnitelného úložiště v zařízení, třeba SD karty.
- **Zeměpisná poloha** – Umožní zařízení využívat informace o poloze.
- **Účet Microsoft** – Povolí nebo zablokuje možnost, aby uživatel propojil účet Microsoft se zařízením.
- **Snímek obrazovky** – Povolí uživateli zachytit obsah obrazovky jako obrázek.
- **Odeslání diagnostických dat** – Povolí zařízení odesílat diagnostické informace Microsoftu.
- **Synchronizace vlastních e-mailových účtů** – Povolí zařízení připojit se k e-mailovým účtům jiným než Microsoftu.

## <a name="password"></a>Heslo

- **Heslo** – Vyžaduje, aby koncový uživatel zadal heslo pro přístup k zařízení.
  - **Požadovaný typ hesla** – Určuje typ hesla, které se bude vyžadovat, například jenom číslice nebo alfanumerické znaky.
  - **Minimální délka hesla** – Určuje minimální počet znaků, které heslo musí obsahovat.
  - **Jednoduchá hesla** – Umožňuje použití jednoduchých hesel, jako je 0000 nebo 1234.
  - **Počet neúspěšných přihlášení před vymazáním obsahu zařízení** – Určuje, kolikrát může uživatel zadat nesprávné heslo, než se zařízení vymaže.
  - **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka** – Určuje dobu, po kterou musí zařízení zůstat v nečinnosti, než se automaticky zamkne jeho obrazovka.
  - **Konec platnosti hesla (dny)** – Určuje počet dní, než bude nutné změnit heslo zařízení.
  - **Znemožnit opakované použití předchozích hesel** – Určuje, kolik dříve použitých hesel se pamatuje.
- **Šifrování** – Vyžaduje, aby data na podporovaných mobilních zařízeních byla šifrovaná.

## <a name="app-store"></a>App Store

- **App Store** – Umožňuje uživatelům připojit se ze zařízení k obchodu s aplikacemi App Store.

## <a name="restricted-apps"></a>Omezené aplikace

V seznamu omezených aplikací můžete nakonfigurovat jeden z následujících seznamů:

**Blokované aplikace** – Zobrazí seznam aplikací (nespravovaných pomocí Intune), které nemají uživatelé dovolené nainstalovat a spustit.
**Povolené aplikace** – Zobrazí seznam aplikací, které mají uživatelé dovolené instalovat. Aplikace, které spravuje Intune, jsou povolené automaticky.

Pokud chcete seznam nakonfigurovat, klikněte na **Přidat**, zadejte libovolný název, volitelně vydavatele aplikace a nakonec adresu URL aplikace v App Storu.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Jak zadat adresu URL pro aplikaci ve Storu

Pokud chcete zadat adresu URL aplikace do seznamu povolených a blokovaných aplikací, použijte následující formát:

Na stránce [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) najděte aplikaci, kterou chcete použít.

Otevřete stránku aplikace a zkopírujte adresu URL do schránky. Tu teď můžete použít jako adresu URL v seznamu povolených nebo blokovaných aplikací.

Příklad: Vyhledejte v obchodě aplikaci Skype. Použijete tuto adresu URL: `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.



### <a name="additional-options"></a>Další možnosti

Můžete taky kliknout na **importovat** a naplnit seznam ze souboru CSV ve formátu <*URL aplikace*>, <*název aplikace*>, <*vydavatele aplikace*>, nebo kliknout na **exportovat** a vytvořit soubor CSV obsahující obsah seznamu aplikací s omezeným přístupem ve stejném formátu.


## <a name="browser"></a>Prohlížeč

- **Webový prohlížeč** – Povolí nebo zablokuje integrovaný webový prohlížeč v zařízeních.

## <a name="cellular-and-connectivity"></a>Mobilní síť a připojení

- **Wi-Fi** – Povolí nebo zakáže funkce Wi-Fi v zařízení.
- **Wi-Fi tethering** – Povolí sdílení mobilního internetového připojení (tethering) přes Wi-Fi na zařízení.
- **Automaticky se připojovat k Wi-Fi hotspotům** – Povolí zařízení automaticky se připojovat k bezplatným Wi-Fi hotspotům a automaticky přijímat jakékoli podmínky použití.
- **Hlášení Wi-Fi hotspotů** – Umožní posílání informací o připojeních Wi-Fi, aby uživatel mohl nacházet možnosti připojení v okolí.
- **Bezkontaktní komunikace (NFC)** – Povolí nebo zakáže operace, které používají bezkontaktní komunikaci, na zařízeních, která ji podporují.
- **Bluetooth** – Povolí nebo zakáže funkce Bluetooth v zařízení.
