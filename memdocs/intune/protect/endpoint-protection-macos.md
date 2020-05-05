---
title: Přidání ochrany koncových bodů s macOS v Microsoft Intune – Azure | Microsoft Docs
description: Na zařízeních s macOS můžete použít Gatekeeper k určení aplikací, které se smí instalovat, včetně aplikací z Mac App Storu. V Microsoft Intune také můžete určitým aplikacím povolit nebo nakonfigurovat průchod bránou firewall nebo můžete určité aplikace zablokovat, použít neviditelný režim utajení, případně blokovat určité typy příchozích připojení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/29/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 337f7608b4c75a5a2ce2c85774d2090d549ae1fe
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587259"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Nastavení ochrany koncových bodů macOS v Intune  

Tento článek ukazuje nastavení ochrany koncových bodů, která můžete nakonfigurovat pro zařízení s macOS. Tato nastavení nakonfigurujete pomocí profilu konfigurace zařízení macOS pro [Endpoint Protection](endpoint-protection-configure.md) v Intune.  

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil ochrany koncového bodu MacOS](endpoint-protection-configure.md).

## <a name="gatekeeper"></a>Gatekeeper  

- **Povolí aplikace stažené z těchto umístění.**  
  Omezte aplikace, které může zařízení spustit, v závislosti na tom, odkud se aplikace stáhly. Záměrem je chránit zařízení před malwarem a dovolit aplikacím jenom ze zdrojů, kterým důvěřujete.  

  - **Není nakonfigurováno**  
  - **Mac App Store**  
  - **Mac App Store a identifikovaní vývojáři**  
  - **Kdekoliv**  

  **Výchozí**: Nenakonfigurováno  

- **Uživatel může přepsat server gatekeeper**  
  Zabrání uživatelům přepsat nastavení serveru gatekeeper a zabránit uživatelům v řízení kliknutí na instalaci aplikace. Pokud tuto možnost povolíte, uživatelé mohou stisknout klávesu Control a kliknutím na libovolnou aplikaci ji nainstalovat.  
 
  - **Nenakonfigurováno** – uživatelé můžou instalovat aplikace kliknutím na tlačítko.  
  - **Blok** – zabraňuje uživatelům v použití řízení – kliknutím instalovat aplikace.  

  **Výchozí**: Nenakonfigurováno  

## <a name="firewall"></a>Brána firewall  

Firewall slouží ke kontrole připojení aplikace, nikoli připojení k portu. Když použijete nastavení pro danou aplikaci, získáte snadno výhody ochrany branou firewall. Nežádoucím aplikacím také znemožníte převzetí kontroly nad síťovými porty otevřenými pro oprávněné aplikace.  

**Obecné**
- **Brána firewall**  
  Povolte bránu firewall ke konfiguraci způsobu zpracování příchozích připojení ve vašem prostředí.  
  - **Není nakonfigurováno**  
  - **Povolení**  

  **Výchozí**: Nenakonfigurováno  

- **Příchozí připojení**  
  Blokuje všechna příchozí připojení s výjimkou připojení požadovaných pro základní internetové služby, jako jsou DHCP, Bonjour a IPSec. Tato funkce také zablokuje všechny služby sdílení, jako je sdílení souborů nebo sdílení obrazovky. Pokud používáte služby sdílení, toto nastavení *nekonfigurujte*.  
  - **Není nakonfigurováno**  
  - **Blokované**  

  **Výchozí**: Nenakonfigurováno  

**Povolí nebo zablokuje příchozí připojení pro konkrétní aplikace.**  

  - **Povolené aplikace**  
    Vyberte aplikace, které mají explicitně povolený příjem příchozích připojení.  

  - **Blokované aplikace**  
    Vyberte aplikace, které by měly blokovat příchozí připojení.  

  - **Neviditelný režim**  
    Chcete-li zabránit počítači v reakci na požadavky na zjišťování, Povolte režim utajení. Oprávněným aplikacím bude zařízení dále odpovídat na příchozí žádosti. Neočekávané požadavky, jako je ICMP (ping), se ignorují.  
    - **Není nakonfigurováno**  
    - **Povolení**  

    **Výchozí**: Nenakonfigurováno  

## <a name="filevault"></a>FileVault  
Další informace o nastaveních úložišť Apple najdete v tématu [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) v obsahu pro vývojáře Apple. 

> [!IMPORTANT]  
> Od macOS 10,15 vyžaduje konfigurace úložiště MDM schválenou uživatelem. 

- **FileVault**  
  Pomocí XTS-AES 128 s trezorem pro zařízení, na kterých běží macOS 10,13 nebo novější, můžete *Povolit* úplné šifrování disku.  
  - **Není nakonfigurováno**  
  - **Povolení**  

  **Výchozí**: Nenakonfigurováno  

  - **Typ obnovovacího klíče**  
    Pro zařízení se vytvoří klíče pro obnovení *osobních klíčů* . Pro osobní klíč nakonfigurujte následující nastavení.  

    - **Umístění klíče pro osobní obnovení** – zadejte krátkou zprávu pro uživatele, která vysvětluje, jak a kde mohou načíst svůj osobní obnovovací klíč. Tento text se vloží do zprávy, kterou uživatel uvidí na přihlašovací obrazovce, když se zobrazí výzva k zadání osobního obnovovacího klíče, pokud je zapomenuté heslo.  

    - **Střídání osobních obnovovacích klíčů** – určete, jak často se má otočit osobní obnovovací klíč pro zařízení. Můžete vybrat výchozí nastavení **není nakonfigurováno**nebo hodnota **1** až **12** měsíců.  

  - **Zakázat výzvu při odhlášení**  
    Zabrání uživateli zobrazit výzvu, aby povolila trezor úložiště při odhlášení.  Pokud je nastavení zakázat, výzva při odhlášení je zakázaná a místo toho se uživateli zobrazí výzva, když se přihlásí.  
    - **Není nakonfigurováno**  
    - **Zakázat** – zakáže výzvu při odhlášení.

    **Výchozí**: Nenakonfigurováno  

  - **Počet povolených pokusů o obejití**  
  Nastaví počet pokusů, které uživatel může ignorovat výzvy k povolení trezoru úložišť, aby se uživatel mohl přihlásit. 

    > [!IMPORTANT]
    >
    > Existuje známý problém s hodnotou **bez omezení, vždy se zobrazí dotaz**. Místo toho, aby uživatel mohl při přihlášení obejít šifrování, vyžaduje toto nastavení šifrování zařízení při příštím přihlášení. Očekává se, že tento problém bude opravený v pozdní červeně a nahlásí se v MC210922.
    >
    > V případě potřeby bude mít toto nastavení novou možnost nula (**0**), která bude vyžadovat, aby zařízení při příštím přihlášení do zařízení zašifroval. Kromě toho, když Intune aktualizuje tuto opravu, všechny zásady, které jsou nastavené na **bez omezení, se vždycky** aktualizují, aby používaly novou hodnotu **0**, která zachovává aktuální chování při vyžadování šifrování.
    >
    > Po vyřešení tohoto problému můžete použít možnost obejít nutnost šifrování tím, že znovu nakonfigurujete toto nastavení pro nastavení **bez omezení, vždy** se zobrazí výzva, že nastavení bude fungovat podle původního očekávání a umožní uživatelům, aby zařízení zašifroval.
    >
    > Pokud máte zaregistrovaná zařízení MacOS, můžete zobrazit další informace, když se přihlásíte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), přejdete na > **stav tenanta** **Správa tenanta**, vyberete stav **služby a Centrum zpráv**a vyhledáte ID zprávy **MC210922**.

    <br> 

    - **Není nakonfigurováno** – před povolením dalšího přihlášení je vyžadováno šifrování zařízení.  
    - **1** až **10** – povolí uživateli ignorovat výzvu od 1 do 10 před tím, než se v zařízení vyžaduje šifrování.  
    - **Bez omezení, vždy** se zobrazí výzva – uživatel bude vyzván k povolení trezoru úložišť, ale šifrování není nikdy vyžadováno.  
 
    **Výchozí**: se *liší* – když je nastavení *Zakázat výzvu při odhlášení* nastavené na **Nenakonfigurováno**, toto nastavení se standardně **nenakonfigurovalo**. Když je možnost *Zakázat výzvu při odhlášení* nastavená na **disabled**, toto nastavení se nastaví na hodnotu **1** a hodnota **není nakonfigurovaná** .

Další informace o trezoru s Intune najdete v tématu [klíče pro obnovení trezoru](encryption-monitor.md#filevault-recovery-keys).

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](../configuration/device-profile-assign.md) a [monitorujte jeho stav](../configuration/device-profile-monitor.md).

Službu Endpoint Protection můžete také nakonfigurovat na [zařízeních s Windows 10 a novějším](endpoint-protection-windows-10.md).
