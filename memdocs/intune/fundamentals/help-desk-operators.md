---
title: Portál helpdesku pro řešení potíží
titleSuffix: Microsoft Intune
description: Pracovníci helpdesku používají portál pro řešení potíží, aby pomohli uživatelům s řešením technických problémů.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/11/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: sumitp
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 07aceda512163513632d124d3e17d1041069b229
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80085819"
---
# <a name="use-the-troubleshooting-portal-to-help-users-at-your-company"></a>Použití portálu pro řešení potíží k poskytování pomoci uživatelům ve vaší společnosti

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Portál pro řešení potíží umožňuje operátorům helpdesku a správcům Intune zobrazit informace o uživatelích a použít je k řešení jejich žádostí o pomoc. Organizace, které zahrnují helpdesk, můžou skupině uživatelů přiřadit **operátora helpdesku**. Role operátora helpdesku může používat podokno **Řešení potíží**.

V podokně **Řešení potíží** se zobrazují také problémy s registrací uživatelů. Podrobnosti o problému a navrhované nápravné kroky můžou správcům a pracovníkům technické podpory pomoct problém vyřešit. Některé problémy s registrací nejsou zaznamenané a k některým chybám nemusí návrhy k odstranění problému existovat.

Pokyny k přidání role operátora helpdesku najdete v článku [Řízení správy na základě rolí (RBAC) s Intune](role-based-access-control.md)

Když uživatel kontaktuje podporu ohledně technického problému s Intune, zadá operátor helpdesku jméno uživatele. Intune zobrazí užitečná data, která vám můžou pomoct s řešením řady problémů úrovně 1 včetně těchto:

- Stav uživatele
- Přiřazení
- Problémy se shodou
- Zařízení neodpovídá
- Zařízení nedokáže získat nastavení sítě VPN nebo Wi-Fi
- Instalace aplikace se nezdařila

## <a name="to-review-troubleshooting-details"></a>Kontrola podrobností o řešení potíží

Zvolením možnosti **Vybrat uživatele** v podokně pro řešení potíží zobrazíte informace o uživateli. Informace o uživateli vám mohou pomoci porozumět aktuálnímu stavu uživatelů a jejich zařízení.  

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Řešení potíží**.
4. Klikněte na **Vybrat** a vyberte uživatele, pro kterého chcete řešit potíže.
5. Vyberte uživatele zadáním jména nebo e-mailové adresy. Klikněte na **Vybrat**. Informace o řešení potíží pro uživatele se zobrazí v podokně Řešení potíží. Informace jsou vysvětlené v následující tabulce.

> [!Note]  
> Do podokna **řešení potíží** se dostanete také tak, že v prohlížeči přejdete na adresu: [https://aka.ms/intunetroubleshooting](https://aka.ms/intunetroubleshooting).

## <a name="areas-of-troubleshooting-dashboard"></a>Oblasti řídicího panelu pro řešení potíží

V podokně **Řešení potíží** můžete zkontrolovat informace o uživateli.

![Řídicí panel pro řešení potíží s očíslovanými oblastmi popsanými v následující tabulce](./media/help-desk-operators/troubleshooting-dash.png)

| Oblast | Název | Popis |
| ---  | ---  | ---         |
| 1.   | Stav účtu  | Zobrazuje stav aktuálního tenanta Intune, například **Aktivní** nebo **Neaktivní**.       |
| 2.   | Výběr uživatele  | Jméno aktuálně vybraného uživatele. Kliknutím na **Změnit uživatele** zvolíte nového uživatele.       |
| 3.   | Stav uživatele  | Zobrazuje stav licence Intune uživatele, počet zařízení a dodržování předpisů pro každé zařízení.       |
| 4.   | Údaje uživatele  | Pomocí seznamu můžete vybrat podrobnosti, které chcete v podokně zkontrolovat. <br>Můžete vybrat: <ul><li>Klientské aplikace<li>Compliance zásady<li> Zásady konfigurace<li>Zásady ochrany aplikace <li>Omezení registrace</ul>      |
| 5.   | Členství ve skupině  | Zobrazí aktuální skupiny, ve kterých je vybraný uživatel členem.       |

<!-- this section needs to be updated

## Client apps reference

The apps that are running devices
- managed by Intune and Azure Active Directory (AD) 
- owned by users managed by Intune and Azure Active Directory (AD).

### Properties

The properties of client apps.

| Property      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name          | The name of the application.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| OS            | The operating system installed on the device.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Type          | You can choose an assignment type for each app.  <br> **Available** - Users install the app from the Company Portal app or website.  <br> **Not Applicable** - The app is not installed or shown in the Company Portal. <br> **Uninstall** - The app is uninstalled from devices in the selected groups.  <br> **Available with or without enrollment** - Assign this app to groups of users whose devices are not enrolled with Intune. |
| Last Modified | The name of the type of device.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Description                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device name        | The name of the type of device.                                                                                                     |
| Managed by         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| App install | Denotes whether an app install failure or success has occurred on the individual device. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last check-in      | The name of the type of device.                                                                                                     |

### App protection status

An app protection policy is available to mobile apps that integrate with Enterprise Mobility Solution (EMS) technologies. These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

| Property    | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| Status      | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| App name    | The name of the application                                                           |
| Device name | The name of the type of device.                                                       |
| Device type | The name of the type of device.                                                       |
| Policies    | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| Last sync   | The timestamp of the last time the device synchronized with Intune.                   |

## App protection policies reference

An app protection policy is available to mobile apps that integrate with EMS technologies.These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

### Properties

The table summarizes app protection policies status for devices managed by Intune.

| Property    | Description                                                                                                                                |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Name        | The name of the application.                                                                                                        |
| Deployed    | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Platform    | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Enrollment  | The name of the type of device.                                                                                                     |
| Last Update | The timestamp the policy was modified.                                                                                              |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Text                                                                                                                                |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device Name        | The name of the type of device.                                                                                                     |
| Managed By         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last Check in      | The name of the type of device.                                                                                                     |

## Compliance policies reference

Makes sure that the devices used to access company apps and data, comply with certain rules like using a PIN to access the device, and encryption of data stored on the device.

### Properties

The properties of the compliance policies.

| Property      | Description                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Assignment    | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Name          | The name of the application.                                                                                                        |
| OS            | The operating system installed on the device.                                                                                       |
| Policy Type   | The type of device ownership (**Company**, **Personal**, and **Unknown**).                                               |
| Last Modified | The name of the type of device.                                                                                                     |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Description                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device name        | The name of the type of device.                                                                                                     |
| Managed by         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, and **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last check-in      | The name of the type of device.                                                                                                     |

### App protection policies

An app protection policy is available to mobile apps that integrate with EMS technologies. These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

| Property    | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| Status      | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| App name    | The name of the application                                                           |
| Device name | The name of the type of device.                                                       |
| Device type | The name of the type of device.                                                       |
| Policies    | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| Last sync   | The timestamp of the last time the device synchronized with Intune.                   |

## Configuration policies reference

An app configuration policy is available to mobile apps with vendor-specific configuration. 

### Properties

The properties of the configuration policies.

| Property      | Description                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Assignment    | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Name          | The name of the application.                                                                                                        |
| OS            | The operating system installed on the device.                                                                                       |
| Policy Type   | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Last Modified | The name of the type of device.                                                                                                     |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Description                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device name        | The name of the type of device.                                                                                                     |
| Managed by         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last check-in      | The name of the type of device.                                                                                                     |


### App protection policies

An app protection policy is available to mobile apps that integrate with EMS technologies. These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

| Property    | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| Status      | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| App name    | The name of the application                                                           |
| Device name | The name of the type of device.                                                       |
| Device type | The name of the type of device.                                                       |
| Policies    | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| Last sync   | The timestamp of the last time the device synchronized with Intune.                   |

-->

## <a name="enrollment-failure-reference"></a>Informace o neúspěšných registracích

Tabulka Neúspěšné registrace obsahuje neúspěšné pokusy o registraci. Zařízení uvedená v níže uvedené tabulce se mohla následně během dalšího pokusu úspěšně zaregistrovat. Některé neúspěšné pokusy nemusí být uvedené. Informace o zmírnění dopadů nejsou k dispozici pro všechny chyby.

| Sloupec tabulky | Popis |
|-------------|----------|
| Stav registrace | Počáteční čas, kdy uživatel poprvé zahájil registraci |
| Operační systém | Operační systém zařízení |
| Verze operačního systému | Verze operačního systému zařízení |
| Selhání | Důvod chyby |

### <a name="failure-details"></a>Podrobnosti chyby

Po výběru řádku chyby se zobrazí další podrobnosti.

| Sekce | Popis |
|-------------|----------|
| Podrobnosti chyby | Podrobnější vysvětlení chyby |
| Možná náprava | Navrhovaný postup k vyřešení chyby. Pro některé chyby nemusí být náprava uvedená. |
| Prostředky (volitelné) | Odkazy na další čtení nebo oblasti na portálu |

### <a name="enrollment-errors"></a>Chyby registrace

| Chyba | Podrobnosti |
|-------------|----------|
| Časový limit pro iOS/iPadOS nebo selhání | Došlo k vypršení časového limitu relace mezi zařízením a Intune, protože uživateli trvala registrace moc dlouho. |
| Uživatel se nenašel nebo nemá licenci | Uživatel nemá licenci nebo je ze služby odebraný. |
| Zařízení je už zaregistrované | Někdo se pokusil o registraci zařízení pomocí Portálu společnosti na zařízení, které má zaregistrované jiný uživatel. |
| Nepřipojeno k Intune | Došlo k pokusu o registraci, když nebyla nakonfigurovaná autorita správy mobilních zařízení (MDM) Intune. |
| Ověřování registrace nebylo úspěšné | Došlo k pokusu o registraci pomocí staré verze Portálu společnosti. |
| Zařízení se nepodporuje | Zařízení nesplňuje minimální požadavky pro registraci v Intune. |
| Nesplnila se omezení registrace | Tato registrace se zablokovala kvůli omezení registrace, které nakonfiguroval správce. |
| Verze zařízení je moc nízká. | Správce nakonfiguroval omezení registrace, které vyžaduje vyšší verzi zařízení. |
| Verze zařízení je příliš vysoká. | Správce nakonfiguroval omezení registrace, které vyžaduje nižší verzi zařízení. |
| Zařízení se nedá zaregistrovat jako osobní. | Správce nakonfiguroval omezení registrace k blokování osobních registrací a zařízení, které selhalo, nebylo předdefinované jako firemní. |
| Platforma zařízení je blokovaná. | Správce nakonfiguroval omezení registrace, které blokuje platformu tohoto zařízení. |
| Vypršela platnost hromadných tokenů. | V balíčku pro zřizování vypršela platnost hromadných tokenů. |
| Nepovedlo se najít zařízení nebo podrobnosti o autopilotu. | Při pokusu o registraci se nenašlo zařízení autopilotu. |
| Profil autopilotu se nenašel nebo není přiřazený. | Zařízení nemá aktivní profil autopilotu. |
| Neočekávaná metoda registrace autopilotu | Zařízení se pokusilo o registraci pomocí nepovolené metody. |
| Zařízení Autopilot se odebralo. | Zařízení, které se pokouší zaregistrovat, se odebralo z autopilotního projektu pro tento účet. |
| Dosáhlo se maximálního počtu zařízení | Tato registrace se zablokovala kvůli omezení počtu zařízení, které nakonfiguroval správce. |
| Onboarding Apple | V tuto chvíli se zablokovala registrace všech zařízení s iOS/iPadOS z důvodu chybějícího nebo neplatného certifikátu Apple MDM push Certificate v Intune. |
| Zařízení se nezaregistrovalo předem | Zařízení se nezaregistrovalo předem jako podnikové a správce zablokoval všechny osobní registrace. |
| Funkce se nepodporuje | Uživatel se zřejmě pokusil o registraci prostřednictvím metody, která není kompatibilní s konfigurací Intune. |

## <a name="collect-available-data-from-mobile-device"></a>Shromažďování dostupných dat z mobilních zařízení

Pokud chcete shromažďovat data ze zařízení při řešení potíží se zařízením uživatele, použijte následující zdroje informací:
- [Odeslání chyb registrace iOS/iPadOS správci IT](../user-help/send-errors-to-your-it-admin-ios.md)
- [Pomoc firemní podpoře s řešením problémů zařízení pomocí podrobného protokolování](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md)
- [Odeslání protokolů Androidu firemní podpoře pomocí kabelu USB](../user-help/send-logs-to-your-it-admin-using-cable-android.md)
- [Odeslání protokolů s diagnostickými daty ze zařízení s Androidem správci IT e-mailem](../user-help/send-logs-to-your-it-admin-by-email-android.md)
- [Odeslání chyb registrace zařízení s Androidem správci IT](../user-help/send-logs-to-your-it-admin-by-email-android.md)

## <a name="next-steps"></a>Další kroky

Můžete zjistit další informace o řízení správy na základě rolí (RBAC) k definování rolí v zařízení organizace, správě mobilních aplikací a úlohách ochrany dat. Další informace najdete v článku [Řízení správy na základě rolí (RBAC) s Intune](role-based-access-control.md).

Zjistěte další informace o známých problémech v Microsoft Intune. Ty najdete v článku [Známé problémy v Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).

Zjistěte, jak vytvořit lístek podpory a získat pomoc, když ji potřebujete. [Získejte podporu](get-support.md).
