---
title: Windows 8.1 nastavení omezení pro zařízení v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete řídit nastavení a funkce na zařízeních s Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 921d0562211d7cd91b28cbafe2edd71fe37af994
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332263"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Nastavení omezení Microsoft Intune Windows 8.1 zařízení

V tomto článku se dozvíte, jak Microsoft Intune nastavení omezení zařízení, která můžete nakonfigurovat pro zařízení s Windows 8.1.

## <a name="general"></a>Obecné

- **Odeslání diagnostických dat** – Povolí zařízení odesílat diagnostické informace Microsoftu.
- **Firewall** – Vyžaduje zapnutí brány Windows Firewall.
- **Řízení uživatelských účtů** – Vyžaduje použití řízení uživatelských účtů (UAC) v zařízeních.

## <a name="password"></a>Heslo
- **Požadovaný typ hesla** – Vyžaduje, aby koncový uživatel zadal heslo k přístupu k zařízení.
- **Minimální délka hesla** – Konfiguruje minimální vyžadovanou délku hesla (ve znacích).
- **Počet neúspěšných přihlášení před vymazáním obsahu zařízení** – Vymaže zařízení, pokud počet pokusů o přihlášení překročí tento počet.
- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka** – Určuje počet minut, po které musí být zařízení nečinné, než bude vyžadované heslo pro odemknutí.
- **Konec platnosti hesla (dny)** – Určuje počet dní, než bude nutné změnit heslo zařízení.
- **Znemožnit opakované použití předchozích hesel** – Určuje, jestli uživatel může konfigurovat dříve použitá hesla.
- **Obrázkové heslo a PIN** – Povolí použití obrázkového hesla a PINu. Obrázkové heslo umožňuje uživateli přihlášení pomocí gesta na obrázku. PIN umožňuje uživatelům rychlé přihlášení pomocí čtyřmístného kódu.
- **Šifrování** – Vyžaduje, aby soubory v zařízení byly šifrované.<br>K vynucení šifrování na zařízeních s Windows 8.1 je potřeba na každé zařízení nainstalovat [aktualizaci MDM klienta pro Windows z prosince 2014](https://support.microsoft.com/kb/3013816).
Pokud toto nastavení povolíte pro zařízení s Windows 8.1, všichni uživatelé zařízení musí mít účet Microsoft.
Šifrování funguje, jenom když zařízení splňuje hardwarové požadavky certifikace [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97).
Pokud vynutíte šifrování na zařízení, je obnovovací klíč přístupný jenom uživatelům s účtem Microsoft, ke kterému přistupují z účtu na Onedrivu. Tento klíč se nedá obnovit jménem uživatele. 

## <a name="browser"></a>Prohlížeč
- **Automatické vyplňování** – Povolí uživatelům změnit nastavení automatického dokončování v prohlížeči.
- **Upozornění na podvody** – Povolí nebo zakáže upozornění na potenciální podvodné weby.
- **Filtr SmartScreen** – Povolí nebo zakáže upozornění na potenciální podvodné weby.
- **JavaScript** – Povolí prohlížeči spouštění skriptů, jako třeba skriptu Java.
- **Automaticky otevíraná okna** – Povolí nebo zakáže blokování automaticky otevíraných oken v prohlížeči.
- **Odesílat hlavičky Do Not Track** – Odesílá v Internet Exploreru hlavičku Do Not Track navštíveným webům.
- **Moduly plug-in** – Umožní uživatelům přidávat do Internet Exploreru moduly plug-in.
- **Jednoslovné zadání na intranetovém webu** – Umožňuje použití jednoho slova pro přesměrování Internet Exploreru na web, jako třeba Bing.
- **Automaticky zjistit intranetový web** – Pomáhá konfigurovat zabezpečení intranetových serverů v Internet Exploreru.
- **Úroveň zabezpečení v internetu** – Nastaví úroveň zabezpečení internetových serverů v Internet Exploreru.
- **Úroveň zabezpečení v intranetu** – Nastaví úroveň zabezpečení intranetových serverů v Internet Exploreru.
- **Úroveň zabezpečení důvěryhodných serverů** – Nakonfiguruje úroveň zabezpečení pro zónu důvěryhodných serverů.
- **Vysoké zabezpečení pro weby s omezeným přístupem** – Nakonfiguruje úroveň zabezpečení pro zónu serverů s omezeným přístupem.
- **Přístup do nabídky Režim rozlehlé sítě** – Umožňuje uživatelům přistupovat k možnostem nabídky podnikového režimu z Internet Exploreru.
Když zapnete toto nastavení můžete také určit **Umístění sestavy protokolování**, které obsahuje adresu URL sestavy, která zobrazuje weby, pro které uživatelé zapnuli přístup v podnikovém režimu.
- **Umístění seznamu webů využívajících Režim rozlehlé sítě** – Určuje umístění seznamu webů, které používají podnikový režim, pokud bude aktivní.

## <a name="cellular"></a>Mobilní služby
- **Datový roaming** – Povolí datový roaming, když je zařízení v mobilní síti.

## <a name="cloud-and-storage"></a>Cloud a úložiště
- **Adresa URL pracovních složek** – Nastaví adresu URL pracovní složky, aby bylo možné synchronizovat dokumenty na všech zařízeních.
- **Přístup k aplikaci Windows Pošta bez účtu Microsoft** – Povolí přístup k aplikaci Windows Pošta bez účtu Microsoft.

## <a name="next-steps"></a>Další kroky

Vytvořte profil omezení zařízení ve [Windows 10 a novějším](device-restrictions-windows-10.md).
