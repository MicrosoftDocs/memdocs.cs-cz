---
title: Nastavení e-mailu pro Android Enterprise v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte e-mailové profily konfigurace zařízení, které používají Exchange servery, a načtěte atributy z Azure Active Directory. Povolení SSL nebo SMIME, ověřování uživatelů pomocí certifikátů nebo uživatelského jména a hesla a synchronizace e-mailů a plánů na zařízeních s pracovním profilem Androidu pomocí Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: maholdaa
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 316c66e1c03d18ec7ffb85895d254ea8b3cfeb71
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815489"
---
# <a name="android-enterprise-device-settings-to-configure-email-authentication-and-synchronization-in-intune"></a>Nastavení zařízení s Androidem Enterprise pro konfiguraci e-mailu, ověřování a synchronizace v Intune

Tento článek obsahuje seznam a popis různých nastavení e-mailů, která můžete řídit na zařízeních s Androidem Enterprise. V rámci řešení pro správu mobilních zařízení (MDM) použijte Tato nastavení ke konfiguraci e-mailového serveru, k šifrování e-mailů použijte protokol SSL a další informace.

Jako správce Intune můžete v pracovním profilu vytvořit a přiřadit nastavení e-mailu pro zařízení s Androidem Enterprise.

Další informace o e-mailových profilech v Intune najdete v tématu [Konfigurace nastavení e-mailu](email-settings-configure.md).

## <a name="before-you-begin"></a>Než začnete

- Vytvořte pracovní profil pro [profil konfigurace e-mailového zařízení s Androidem Enterprise](email-settings-configure.md)  >  **Work profile**.
- Nebo vytvořte [zásadu konfigurace aplikace](../apps/app-configuration-policies-use-android.md).

## <a name="android-enterprise"></a>Android Enterprise

- **E-mailová aplikace**: vyberte **Gmail** nebo **devět Work**.
- **E-mailový server**: Zadejte název hostitele vašeho Exchange serveru. Zadejte například `outlook.office365.com`.
- **Atribut uživatelského jména z AAD**: Toto jméno je atribut, který Intune získá z Azure Active Directory (Azure AD). Intune dynamicky vygeneruje uživatelské jméno, které tento profil používá. Možnosti:

  - **Hlavní název uživatele**: Získá název, například `user1` nebo `user1@contoso.com` .
  - **Uživatelské jméno**: Získá jenom název, třeba `user1` .

- **Atribut e-mailové adresy z AAD**: Tento název je atribut e-mailu, který Intune získá z Azure AD. Intune dynamicky generuje e-mailovou adresu, kterou používá tento profil. Možnosti:
  - **Hlavní název uživatele**: používá `user1@contoso.com` `user1` jako e-mailovou adresu úplný hlavní název, jako je například nebo.
  - **Primární adresa SMTP**: pomocí primární adresy SMTP, například, se `user1@contoso.com` přihlaste k Exchangi.

- **Metoda ověřování**: jako metodu ověřování používanou e-mailovým profilem vyberte **uživatelské jméno a heslo** nebo **certifikáty** .
  - Pokud vyberete **Certifikát**, vyberte profil certifikátu SCEP nebo PKCS klienta, který jste dříve vytvořili za účelem ověřování připojení Exchange.
- **SSL**: vyberte možnost **Povolit** , pokud chcete při posílání e-mailů, přijímání e-mailů a komunikaci s Exchange serverem používat komunikaci SSL (Secure Sockets Layer) (SSL).
- **Velikost e-mailu, který se má synchronizovat**: vyberte dobu, po kterou se má e-mail synchronizovat. Případně můžete vybrat možnost **neomezeno** a synchronizovat všechny dostupné e-maily.
- **Typ obsahu, který se má synchronizovat** (jenom devět Work): vyberte, která data se mají na zařízeních synchronizovat. Možnosti:
  - **Kontakty**: vyberte **Povolit** , pokud chcete koncovým uživatelům povolit synchronizaci kontaktů s jejich zařízeními.
  - **Kalendář**: vyberte **Povolit** , pokud chcete koncovým uživatelům povolit synchronizaci kalendáře s jejich zařízeními.
  - **Úkoly**: vyberte **Povolit** , pokud chcete koncovým uživatelům povolit synchronizaci všech úloh na jejich zařízeních.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit e-mailové profily pro zařízení se systémem [Android Samsung KNOX](email-settings-android.md), [iOS/iPadOS](email-settings-ios.md)a [Windows 10 a novějším](email-settings-windows-10.md) .
