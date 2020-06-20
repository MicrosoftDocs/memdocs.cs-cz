---
title: Konfigurace Endpoint Protection na zařízeních macOS pomocí Microsoft Intune | Microsoft Docs
description: Použití Intune ke konfiguraci zařízení macOS pomocí integrované brány firewall pro povolení nebo blokování určitých aplikací nebo pro použití utajeného režimu pro použití serveru gatekeeper k určení, kde se aplikace instalují, a použití šifrování disku trezoru.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107497"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Nastavení ochrany koncových bodů macOS v Intune

Tento článek ukazuje nastavení ochrany koncových bodů, která můžete nakonfigurovat pro zařízení s macOS. Tato nastavení nakonfigurujete pomocí profilu konfigurace zařízení macOS pro [Endpoint Protection](endpoint-protection-configure.md) v Intune.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil ochrany koncového bodu MacOS](endpoint-protection-configure.md).

## <a name="firewall"></a>Brána firewall

Firewall slouží ke kontrole připojení aplikace, nikoli připojení k portu. Když použijete nastavení pro danou aplikaci, získáte snadno výhody ochrany branou firewall. Nežádoucím aplikacím také znemožníte převzetí kontroly nad síťovými porty otevřenými pro oprávněné aplikace.

- **Povolit bránu firewall**

  Zapněte bránu firewall v macOS a pak nakonfigurujte, jak se budou zpracovávat příchozí připojení ve vašem prostředí.

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

- **Blokovat všechna příchozí připojení**

  Blokuje všechna příchozí připojení s výjimkou připojení požadovaných pro základní internetové služby, jako jsou DHCP, Bonjour a IPSec. Tato funkce také zablokuje všechny služby sdílení, jako je sdílení souborů nebo sdílení obrazovky. Pokud používáte služby sdílení, toto nastavení *nekonfigurujte*.

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

  Když nastavíte *Blokovat všechna příchozí připojení* na *nenakonfigurovaná*, můžete nakonfigurovat, které aplikace můžou nebo nemůžou přijímat příchozí připojení.

  **Povolené aplikace**: umožňuje nakonfigurovat seznam aplikací, u kterých je povolený příjem příchozích připojení.

  - **Přidat aplikace podle ID sady prostředků**: zadejte [ID sady prostředků](../configuration/bundle-ids-built-in-ios-apps.md) aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
  - **Přidat aplikaci pro Store**: vyberte aplikaci ze Storu, kterou jste dříve přidali v Intune. Další informace najdete v článku [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

  **Blokované aplikace**: nakonfigurujte seznam aplikací, které mají blokované příchozí připojení.

  - **Přidat aplikace podle ID sady prostředků**: zadejte [ID sady prostředků](../configuration/bundle-ids-built-in-ios-apps.md) aplikace. Na webu společnosti Apple je seznam [integrovaných aplikací Apple](https://support.apple.com/HT208094).
  - **Přidat aplikaci pro Store**: vyberte aplikaci ze Storu, kterou jste dříve přidali v Intune. Další informace najdete v článku [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

- **Povolit režim utajení**

  Chcete-li zabránit počítači v reakci na požadavky na zjišťování, Povolte režim utajení. Oprávněným aplikacím bude zařízení dále odpovídat na příchozí žádosti. Neočekávané požadavky, jako je ICMP (ping), se ignorují.

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

## <a name="gatekeeper"></a>Gatekeeper

- **Povolí aplikace stažené z těchto umístění.**

  Omezte aplikace, které může zařízení spustit, v závislosti na tom, odkud se aplikace stáhly. Záměrem je chránit zařízení před malwarem a dovolit aplikacím jenom ze zdrojů, kterým důvěřujete.

  - **Nenakonfigurováno** (*výchozí*)
  - **Mac App Store**
  - **Mac App Store a identifikovaní vývojáři**
  - **Kdekoliv**

- **Nepovolit uživateli přepisu serveru gatekeeper**

  Zabrání uživatelům přepsat nastavení serveru gatekeeper a zabránit uživatelům v řízení kliknutí na instalaci aplikace. Pokud tuto možnost povolíte, uživatelé mohou stisknout klávesu Control a kliknutím na libovolnou aplikaci ji nainstalovat.

  - **Nenakonfigurováno** (*výchozí*) – uživatelé můžou instalovat aplikace kliknutím na tlačítko.
  - **Ano** – zabrání uživatelům používat pro instalaci aplikací ovládací prvek – kliknutí.

## <a name="filevault"></a>FileVault

Další informace o nastaveních úložišť Apple najdete v tématu [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) v obsahu pro vývojáře Apple.

> [!IMPORTANT]
> Od macOS 10,15 vyžaduje konfigurace úložiště MDM schválenou uživatelem.

- **Povolit trezor úložiště**  

  Pomocí XTS-AES 128 s trezorem pro zařízení, na kterých běží macOS 10,13 nebo novější, můžete *Povolit* úplné šifrování disku.

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

  Pokud je *možnost Povolit trezoru úložišť* nastavená na *hodnotu Ano*, můžete nakonfigurovat následující nastavení:

  - **Typ obnovovacího klíče**

    Pro zařízení se vytvoří klíče pro obnovení *osobních klíčů* . Pro osobní klíč nakonfigurujte následující nastavení.

  - **Popis umístění v úschově pro osobní obnovovací klíč**

    Zadejte krátkou zprávu pro uživatele, která vysvětluje, jak a kde mohou načíst svůj osobní obnovovací klíč. Tento text se vloží do zprávy, kterou uživatel uvidí na přihlašovací obrazovce, když se zobrazí výzva k zadání osobního obnovovacího klíče, pokud je zapomenuté heslo.

  - **Střídání osobních obnovovacích klíčů**

    Určete, jak často se má otočit osobní obnovovací klíč pro zařízení. Můžete vybrat výchozí nastavení **není nakonfigurováno**nebo hodnota **1** až **12** měsíců.

  - **Skrýt obnovovací klíč**

    Vyberte, pokud chcete skrýt osobní klíč od uživatele zařízení během šifrování trezoru 2.

    - **Nenakonfigurováno** (*výchozí*) – osobní klíč se uživateli zařízení během šifrování zobrazuje.
    - **Ano** – osobní klíč je během šifrování skrytý od uživatele zařízení.

    Po šifrování můžou uživatelé zařízení zobrazit svůj osobní obnovovací klíč pro šifrované zařízení macOS z těchto umístění:
    - aplikace Portál společnosti pro iOS/iPadOS
    - Aplikace Intune
    - Web portál společnosti
    - Aplikace Portál společnosti pro Android

    Pokud chcete klíč zobrazit, v aplikaci nebo na webu přejít na podrobnosti o zařízení šifrovaného zařízení macOS a vyberte *získat obnovovací klíč*.

  - **Zakázat výzvu při odhlášení**

    Zabrání uživateli zobrazit výzvu, aby povolila trezor úložiště při odhlášení.  Pokud je nastavení zakázat, výzva při odhlášení je zakázaná a místo toho se uživateli zobrazí výzva, když se přihlásí.

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zakázat výzvu při odhlášení

  - **Počet povolených pokusů o obejití**

    Nastaví počet pokusů, které uživatel může ignorovat výzvy k povolení trezoru úložišť, aby se uživatel mohl přihlásit.

    - **Není nakonfigurováno** – před povolením dalšího přihlášení je vyžadováno šifrování zařízení.
    - **0** – vyžaduje, aby se zařízení zašifroval při příštím přihlášení uživatele k zařízení.
    - **1** až **10** – povolí uživateli ignorovat výzvu od 1 do 10 před tím, než se v zařízení vyžaduje šifrování.
    - **Bez omezení, vždy** se zobrazí výzva – uživatel bude vyzván k povolení trezoru úložišť, ale šifrování není nikdy vyžadováno.

    Výchozí hodnota pro toto nastavení závisí na konfiguraci služby *Zakázat příkazový řádek při odhlášení*. Pokud je možnost *Zakázat výzvu při odhlášení* nastavena na hodnotu **není nakonfigurováno**, toto nastavení se standardně **nenakonfigurovalo**. Pokud je možnost *Zakázat výzvu při odhlášení* nastavená na **hodnotu Ano**, toto nastavení se nastaví na hodnotu **1** a hodnota **není nakonfigurovaná** .

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](../configuration/device-profile-assign.md) a [monitorujte jeho stav](../configuration/device-profile-monitor.md).

Službu Endpoint Protection můžete také nakonfigurovat na [zařízeních s Windows 10 a novějším](endpoint-protection-windows-10.md).
