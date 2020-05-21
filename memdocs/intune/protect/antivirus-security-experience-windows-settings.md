---
title: Nastavení zásad antivirové ochrany Windows 10 pro prostředí Windows Security pro Intune | Microsoft Docs
description: Nastavení zásad antivirové ochrany Endpoint Security pro aplikaci zabezpečení systému Windows v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431329"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Nastavení profilu Windows Security Experience v Microsoft Intune

Zobrazit nastavení zásad antivirové ochrany, která můžete nakonfigurovat pro profil **Windows Security Experience** pro Windows 10 v Microsoft Intune jako součást [zásady zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

**Zabezpečení systému Windows**

- **Povolení ochrany před neoprávněným zakázáním programu Microsoft Defender**  
  [Zabránit změnám v nastavení zabezpečení pomocí ochrany před zneužitím](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Nenakonfigurováno** (*výchozí*) – Pokud stav *Povolení* nebo *zákaz* existuje v klientovi, nasazení *není nakonfigurované* nemá žádný vliv na toto nastavení. 
  - **Povolit** – povolí omezení ochrany proti falšování. Chcete-li změnit stav z povoleného nebo zakázaného, nasaďte opačné nastavení, aby se projevilo.
  - **Zakázat** – zakáže omezení ochrany proti falšování. Chcete-li změnit stav z povoleného nebo zakázaného, nasaďte opačné nastavení, aby se projevilo.

- **Skrytí oblasti ochrany před viry a hrozbami v aplikaci zabezpečení systému Windows**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast ochrany před viry a hrozbami v aplikaci zabezpečení Windows je pro koncové uživatele skrytá. Oznámení související s ochranou před viry a hrozbami se potlačí.

  - **Skrýt možnost obnovení dat ransomwarem v aplikaci zabezpečení Windows**  
    SLUŽEB[](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast obnovení dat ransomwarem v aplikaci zabezpečení Windows je pro koncové uživatele skrytá. Oznámení související s ransomwarem se potlačí.

- **Skrýt oblast ochrany účtu v aplikaci zabezpečení systému Windows**  
  CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast Ochrana účtu v aplikaci zabezpečení systému Windows je pro koncové uživatele skrytá. Oznámení související s ochranou účtu se potlačí.

- **Skrytí brány firewall a oblasti ochrany sítě v aplikaci zabezpečení systému Windows**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast brána firewall a ochrana sítě v zabezpečení Windows jsou pro koncové uživatele skrytá. Brána firewall a oznámení týkající se ochrany sítě jsou potlačeny.

- **Skrytí oblasti ovládacího prvku aplikace a prohlížeče v aplikaci zabezpečení systému Windows**  
  CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast pro řízení aplikací a prohlížečů v zabezpečení systému Windows je od koncových uživatelů skrytá. Oznámení související s ovládacím prvkem aplikace a prohlížeče se potlačí.

- **Skrýt oblast zabezpečení zařízení v aplikaci zabezpečení systému Windows**  
  CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast hardwarové ochrany v aplikaci zabezpečení systému Windows je pro koncové uživatele skrytá. Budou potlačena oznámení související s hardwarovou ochranou.
  
- **Skrytí oblasti výkonu a stavu zařízení v aplikaci zabezpečení systému Windows**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast výkon a stav zařízení v aplikaci zabezpečení Windows jsou pro koncové uživatele skrytá. U zařízení se neztlačila oznámení týkající se výkonu a stavu zařízení.

- **Skrýt oblast možností řady v aplikaci zabezpečení Windows**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní přístup a oznámení uživateli.
  - **Ano** – oblast možností řady v aplikaci zabezpečení Windows je pro koncové uživatele skrytá. Také se potlačí oznámení týkající se rodinných možností.

- **Oznámení aplikace pro zabezpečení systému Windows**  
  SLUŽEB[](https://go.microsoft.com/fwlink/?linkid=873675)

  Pomocí tohoto nastavení můžete uživatelům zablokovat oznámení zabezpečení systému Windows pro všechna předchozí nastavení funkcí. Alternativně můžete spravovat oznámení aplikací pro zabezpečení systému Windows na funkci pomocí nastavení pro pokračování.

  - **Nenakonfigurováno** (*výchozí*) – všechna oznámení aplikací pro zabezpečení systému Windows, která nejsou kontrolována jiným nastavením, jsou povolena.
  - **Blokuje Nekritická oznámení** – oznámení, jako jsou například dokončování skenování, jsou blokovaná.
  - **Blokování všech oznámení** – kritická a Nekritická oznámení jsou blokovaná pro všechny funkce zabezpečení systému Windows.

- **Skrýt ikonu zabezpečení systému Windows z oznamovací oblasti**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  Aby se toto nastavení projevilo, uživatel se musí odhlásit a znovu přihlásit nebo restartovat počítač.
  - **Nenakonfigurováno** (*výchozí*) – nastavení vrátí klienta k výchozímu zobrazení ikony.
  - **Ano** – skryje ikonu zabezpečení systému Windows z oznamovacího panelu uživatele.
  
- **Zakázání možnosti vymazat čip TPM v aplikaci zabezpečení systému Windows**  
  CSP: [DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožňuje přístup k tlačítku.
  - **Ano** – zakáže přístup k tlačítku vymazat čip TPM v aplikaci zabezpečení systému Windows.

- **Vyzvat uživatele k aktualizaci firmwaru TPM při zjištění ohrožení zabezpečení**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které nevyzve uživatele.
  - **Ano** – povolí systému Windows zobrazovat výzvu koncovým uživatelům, když se v jejich firmwaru TPM najde potenciální ohrožení zabezpečení. Pro vyřešení ohrožení zabezpečení pak doporučujeme spustit aktualizace firmwaru.

- **Kontaktní údaje podpory organizace**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Deklarujete, kde byste chtěli zobrazit informace o vaší organizaci IT v aplikaci zabezpečení systému Windows a oznámeních.
  - **Nenakonfigurováno** (*výchozí*)
  - **Zobrazit v aplikaci a v oznámeních**
  - **Zobrazit jenom v aplikaci**
  - **Zobrazit jenom v oznámeních**