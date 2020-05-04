---
title: Nastavení e-mailu pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte e-mailový profil konfigurace zařízení, který používá servery Exchange a načítá atributy ze služby Azure Active Directory. Pomocí Microsoft Intune můžete na zařízeních s Windows 10 také povolit protokol SSL a synchronizovat e-maily a plány.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa861a266f89b82fdd2d6e73d30fdc2e58da33b4
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086913"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Nastavení e-mailového profilu pro zařízení s Windows 10 v Microsoft Intune

Pomocí nastavení e-mailového profilu můžete nakonfigurovat aplikaci pošty na zařízeních s Windows 10 a novějším.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil](email-settings-configure.md).

## <a name="email-settings"></a>Nastavení e-mailu

- **E-mailový server**: Zadejte název hostitele vašeho Exchange serveru. Zadejte například `outlook.office365.com`.
- **Název účtu**: Zadejte zobrazovaný název e-mailového účtu. Tento název se zobrazuje uživatelům na jejich zařízeních.
- **Atribut uživatelského jména z AAD**: Toto jméno je atribut, který Intune získá od služby Azure Active Directory (AAD). Intune dynamicky vygeneruje uživatelské jméno, které tento profil používá. Možnosti:
  - **Hlavní název uživatele**: Získá název, například `user1` nebo. `user1@contoso.com`
  - **Primární adresa SMTP**: Získá název ve formátu e-mailové adresy, `user1@contoso.com`například.
  - **Název účtu SAM**: Vyžaduje doménu, například `domain\user1`. Dále zadejte:  
    - **Zdroj názvu domény uživatele**: Zvolte **AAD** (Azure Active Directory) nebo **Vlastní**.

      Pokud se rozhodnete získat atributy ze služby **AAD**, zadejte:
      - **Atribut názvu domény uživatele z AAD**: vyberte, chcete-li získat **úplný název domény** nebo atribut **názvu NetBIOS** pro uživatele.

      Pokud se rozhodnete použít **Vlastní** atributy, zadejte:
      - **Vlastní název domény, který se má použít**: zadejte hodnotu, kterou Intune používá pro název domény, `contoso.com` například `contoso`nebo.

- **Atribut e-mailové adresy z AAD**: Intune získá tento atribut z Azure Active Directory (AAD). Vyberte způsob generování e-mailové adresy uživatele. Možnosti:
  - **Hlavní název uživatele**: jako e-mailová adresa používá úplný hlavní název, jako `user1@contoso.com` je `user1`například nebo.
  - **Primární adresa SMTP**: používá primární adresu SMTP pro přihlášení k Exchangi, jako je například `user1@contoso.com`.

### <a name="security"></a>Zabezpečení

- **SSL**: Při volbě **Povolit** se při posílání a přijímání e-mailů a komunikaci se serverem Exchange používá komunikace SSL (Secure Sockets Layer). **Disable** NEPOTŘEBUJE protokol SSL.

### <a name="synchronization"></a>Synchronizace

- **Počet e-mailů k synchronizaci**: Zvolte počet dní, za které se mají e-maily synchronizovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud chcete synchronizovat všechny dostupné e-maily, vyberte **neomezeno** .
- **Plán synchronizace**: Vyberte plán, podle kterého zařízení synchronizují data z Exchange serveru. Můžete také vybrat možnost **při doručování zpráv**, která synchronizuje data hned po doručení. Případně vyberte možnost **ručně** , aby uživatel zařízení spustil synchronizaci.

### <a name="content-sync"></a>Synchronizace obsahu

- **Typ obsahu, který se má synchronizovat**: Vyberte typy obsahu, které chcete synchronizovat do zařízení:
  - **Kontakty**: **v** synchronizaci kontaktů. **Off** nesynchronizuje automaticky kontakty. Uživatelé se ručně synchronizují.
  - **Kalendář**: **v** synchronizaci kalendáře. **Off** nesynchronizuje automaticky kontakty. Uživatelé se ručně synchronizují.
  - **Úkoly**: **v** synchronizaci úloh. **Vypnuto** automaticky nesynchronizuje úlohy. Uživatelé se ručně synchronizují.

## <a name="next-steps"></a>Další kroky

Můžete také nakonfigurovat nastavení e-mailu v [Androidu](email-settings-android.md), [Androidu Enterprise](email-settings-android-enterprise.md)a [iOS/iPadOS](email-settings-ios.md). 

[Nakonfigurujte nastavení e-mailu v Intune](email-settings-configure.md).
