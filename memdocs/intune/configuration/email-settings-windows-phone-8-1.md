---
title: Nastavení e-mailu pro Windows Phone 8.1 v Microsoft Intune
titleSuffix: ''
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete nakonfigurovat připojení e-mailu na zařízeních s Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5bd00f12ab0f015c6408e2bbc934e1320c7540e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146133"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Nastavení e-mailového profilu v Microsoft Intune pro zařízení s Windows Phone 8.1

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Tento článek ukazuje nastavení e-mailového profilu, která můžete konfigurovat pro zařízení s Windows Phone 8.1.

>[!IMPORTANT]
>Pro zařízení s Windows 10 se taky používají e-mailové profily Windows Phone 8,1.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte e-mailový profil Windows Phone 8,1](email-settings-configure.md).

## <a name="email-settings"></a>Nastavení e-mailu

- **E-mailový server**: Zadejte název hostitele vašeho Exchange serveru. Zadejte například `outlook.office365.com`.
- **Název účtu**: Zadejte zobrazovaný název e-mailového účtu. Tento název se zobrazuje uživatelům na jejich zařízeních.
- **Atribut uživatelského jména z AAD**: Toto jméno je atribut, který Intune získá od služby Azure Active Directory (AAD). Intune dynamicky vygeneruje uživatelské jméno, které tento profil používá. Možnosti:
  - **Hlavní název uživatele**: Získá název, například `user1` nebo `user1@contoso.com` .
  - **Primární adresa SMTP**: Získá název ve formátu e-mailové adresy, například `user1@contoso.com` .
  - **Název účtu SAM**: Vyžaduje doménu, například `domain\user1`. Dále zadejte:
    - **Zdroj názvu domény uživatele**: vaše možnosti:
      - **AAD** (Azure Active Directory): zadejte **atribut názvu domény uživatele z AAD**. Vyberte, chcete-li získat **úplný název domény** nebo atribut **názvu rozhraní NetBIOS** uživatele.
      - **Vlastní**: zadejte **název vlastní domény, který se má použít**. Zadejte hodnotu, kterou Intune používá pro název domény, například `contoso.com` nebo `contoso` .

- **Atribut e-mailové adresy z AAD**: Intune získá tento atribut z Azure Active Directory (AAD). Vyberte způsob generování e-mailové adresy uživatele. Možnosti:
  - **Hlavní název uživatele**: jako e-mailová adresa používá úplný hlavní název, jako je například `user1@contoso.com` nebo `user1` .
  - **Primární adresa SMTP**: používá primární adresu SMTP pro přihlášení k Exchangi, jako je například `user1@contoso.com` .

## <a name="security-settings"></a>Nastavení zabezpečení

- **SSL**: Při volbě **Povolit** se při posílání a přijímání e-mailů a komunikaci se serverem Exchange používá komunikace SSL (Secure Sockets Layer). **Disable** NEPOTŘEBUJE protokol SSL.

## <a name="synchronization-settings"></a>Nastavení synchronizace

- **Počet e-mailů k synchronizaci**: Zvolte počet dní, za které se mají e-maily synchronizovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud chcete synchronizovat všechny dostupné e-maily, vyberte **neomezeno** .
- **Plán synchronizace**: Vyberte plán, podle kterého zařízení synchronizují data z Exchange serveru. Můžete také vybrat možnost **při doručování zpráv**, která synchronizuje data hned po doručení. Případně vyberte možnost **ručně** , aby uživatel zařízení spustil synchronizaci.

## <a name="content-sync-settings"></a>Nastavení synchronizace obsahu

- **Typ obsahu, který se má synchronizovat**: Vyberte typy obsahu, které chcete synchronizovat do zařízení:
  - **Kontakty**: **v** synchronizaci kontaktů. **Off** nesynchronizuje automaticky kontakty. Uživatelé se ručně synchronizují.
  - **Kalendář**: **v** synchronizaci kalendáře. **Off** nesynchronizuje automaticky kontakty. Uživatelé se ručně synchronizují.
  - **Úkoly**: **v** synchronizaci úloh. **Vypnuto** automaticky nesynchronizuje úlohy. Uživatelé se ručně synchronizují.

## <a name="next-steps"></a>Další kroky

Můžete také nakonfigurovat nastavení e-mailu pro [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md)a [Windows 10](email-settings-windows-10.md).

[Nakonfigurujte nastavení e-mailu v Intune](email-settings-configure.md).
