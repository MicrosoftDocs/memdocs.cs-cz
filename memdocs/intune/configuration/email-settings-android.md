---
title: Nastavení e-mailu Androidu v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte e-mailové profily konfigurace zařízení, které používají Exchange servery, a načtěte atributy z Azure Active Directory. Povolte SSL nebo SMIME, ověřte uživatele pomocí certifikátů nebo uživatelského jména a hesla a synchronizujte e-maily a plány na zařízeních se systémem Android Samsung KNOX pomocí Microsoft Intune.
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36e17dc12622b3bb95c35a4472556f1c4f31ccd0
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80087013"
---
# <a name="android-device-settings-to-configure-email-authentication-and-synchronization-in-intune"></a>Nastavení zařízení s Androidem pro konfiguraci e-mailu, ověřování a synchronizace v Intune

Tento článek obsahuje seznam a popis různých nastavení e-mailů, které můžete řídit v zařízeních se systémem Android Samsung KNOX v Intune. V rámci řešení pro správu mobilních zařízení (MDM) použijte Tato nastavení ke konfiguraci e-mailového serveru, k šifrování e-mailů použijte protokol SSL a další informace.

Jako správce Intune můžete vytvořit a přiřadit nastavení e-mailu pro zařízení se systémem Android Samsung KNOX Standard.

Další informace o e-mailových profilech v Intune najdete v tématu [Konfigurace nastavení e-mailu](email-settings-configure.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](email-settings-configure.md).

## <a name="android-samsung-knox"></a>Android (Samsung Knox)

- **E-mailový server**: Zadejte název hostitele vašeho Exchange serveru. Zadejte například `outlook.office365.com`.
- **Název účtu**: Zadejte zobrazovaný název e-mailového účtu. Tento název se zobrazuje uživatelům na jejich zařízeních.
- **Atribut uživatelského jména z AAD**: Toto jméno je atribut, který Intune získá z Azure Active Directory (Azure AD). Intune dynamicky vygeneruje uživatelské jméno, které tento profil používá. Možnosti:
  - **Hlavní název uživatele**: Získá název, například `user1` nebo. `user1@contoso.com`
  - **Uživatelské jméno**: Získá jenom název, třeba `user1`.
  - **Název účtu SAM**: Vyžaduje doménu, například `domain\user1`. název účtu sAM se používá jenom u zařízení s Androidem. Dále zadejte:  
    - **Zdroj názvu domény uživatele**: Zvolte **AAD** (Azure Active Directory) nebo **Vlastní**.

      Pokud se rozhodnete získat atributy ze služby **AAD**, zadejte:
      - **Atribut názvu domény uživatele z AAD**: vyberte, chcete-li získat **úplný název domény** nebo atribut **názvu NetBIOS** pro uživatele.

      Pokud se rozhodnete použít **Vlastní** atributy, zadejte:
      - **Vlastní název domény, který se má použít**: zadejte hodnotu, kterou Intune používá pro název domény, `contoso.com` například `contoso`nebo.

- **Atribut e-mailové adresy z AAD**: Tento název je atribut e-mailu, který Intune získá z Azure AD. Intune dynamicky generuje e-mailovou adresu, kterou používá tento profil. Možnosti:
  - **Hlavní název uživatele**: používá jako e-mailovou adresu úplný `user1@contoso.com` hlavní `user1`název, jako je například nebo.
  - **Primární adresa SMTP**: pomocí primární adresy SMTP, například `user1@contoso.com`, se přihlaste k Exchangi.

- **Metoda ověřování**: Jako metodu ověřování používanou e-mailovým profilem vyberte buď **Uživatelské jméno a heslo**, nebo **Certifikáty**.
  - Pokud vyberete **Certifikát**, vyberte profil certifikátu SCEP nebo PKCS klienta, který jste dříve vytvořili za účelem ověřování připojení Exchange.

### <a name="security-settings"></a>Nastavení zabezpečení

- **SSL**: Při posílání a přijímání e-mailů a komunikaci se serverem Exchange se použije komunikace přes protokol SSL (Secure Sockets Layer).
- **S/MIME**: Odchozí e-maily se budou posílat s využitím šifrování S/MIME.
  - Pokud vyberete **Certifikát**, vyberte profil certifikátu SCEP nebo PKCS klienta, který jste dříve vytvořili za účelem ověřování připojení Exchange.

### <a name="synchronization-settings"></a>Nastavení synchronizace

- **Počet e-mailů k synchronizaci**: Zvolte počet dní, za které se mají e-maily synchronizovat, nebo vyberte **Bez omezení**, pokud chcete synchronizovat všechny dostupné e-maily.
- **Plán synchronizace**: Vyberte plán, podle kterého zařízení synchronizují data z Exchange serveru. Můžete také vybrat **Při doručování zpráv**, aby se data synchronizovala po doručení, nebo **Ruční**, aby musel synchronizaci zahájit uživatel zařízení.

### <a name="content-sync-settings"></a>Nastavení synchronizace obsahu

- **Typ obsahu, který se má synchronizovat**: Vyberte typy obsahu, které se mají na zařízeních synchronizovat. **Není nakonfigurováno** , zakáže toto nastavení. Pokud je nastavení nastaveno na **Nenakonfigurováno**, pak pokud koncový uživatel na zařízení povolí synchronizaci, synchronizace se znovu zakáže, když se zařízení synchronizuje s Intune, protože zásady jsou posílené. 

  Synchronizovat můžete následující obsah:  
  - **Kontakty**: vyberte **Povolit** , pokud chcete koncovým uživatelům povolit synchronizaci kontaktů s jejich zařízeními.
  - **Kalendář**: vyberte **Povolit** , pokud chcete koncovým uživatelům povolit synchronizaci kalendáře s jejich zařízeními.
  - **Úkoly**: vyberte **Povolit** , pokud chcete koncovým uživatelům povolit synchronizaci všech úloh na jejich zařízeních.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit e-mailové profily pro [Android Enterprise – Work Profile](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md), [Windows 10 a novější](email-settings-windows-10.md)a [Windows Phone 8,1](email-settings-windows-phone-8-1.md).
