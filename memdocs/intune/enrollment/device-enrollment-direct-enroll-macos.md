---
title: Použití přímé registrace pro zařízení macOS
titleSuffix: Microsoft Intune
description: Naučte se registrovat zařízení macOS pomocí přímé registrace.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819951"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>Použití přímé registrace pro zařízení macOS

Intune podporuje registraci zařízení macOS pomocí přímé registrace (DE) pro podniková zařízení. Přímá registrace zařízení nevymaže. Zařízení zaregistruje pomocí nastavení macOS. Tato metoda podporuje jenom **zařízení bez přidružení uživatele**.

## <a name="prerequisites"></a>Předpoklady

- Fyzický přístup k zařízením macOS
- [Nastavení autority pro správu mobilních zařízení (MDM)](../fundamentals/mdm-authority-set.md)
- [Certifikát Apple MDM push certificate](apple-mdm-push-certificate-get.md)
 - Práva správce na registrovaných zařízeních macOS

## <a name="create-an-apple-configurator-profile-for-devices"></a>Vytvoření profilu Apple Configuratoru pro zařízení

Profil registrace zařízení definuje nastavení, která se během registrace použijí. Tato nastavení se použijí jenom jednou. Pomocí těchto kroků můžete vytvořit registrační profil pro registraci zařízení macOS pomocí přímé registrace.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Registrovat zařízení**  >  **registrace**Apple  >  **Apple Configuratoru**.

2. Vyberte **profily**  >  **vytvořit**.

3. V části **Vytvořit registrační profil** zadejte **Název** a **Popis** profilu pro účely správy. Uživatelům se tyto údaje nezobrazí. Pole Název můžete využít k vytvoření dynamické skupiny v Azure Active Directory. Název profilu použijte k definování parametru enrollmentProfileName pro přiřazení zařízení s tímto registračním profilem. Přečtěte si další informace o dynamických skupinách Azure Active Directory.

4. V případě **spřažení uživatele**vyberte možnost **Registrovat bez přidružení uživatele** – tuto možnost vyberte, pokud chcete zařízení nepřidružená k jednomu uživateli. Použijte ji pro zařízení určená k plnění úkolů, u kterých není potřeba přístup k místním uživatelským datům. Aplikace, které vyžadují přidružení uživatele (včetně aplikace Portál společnosti používané pro instalaci obchodních aplikací), nebudou fungovat. Vyžaduje se pro přímou registraci.

     > [!NOTE]
     > **Registrace s přidružením uživatele** není podporována v MacOS při použití přímé registrace. Pro zařízení, která potřebují přidružení uživatele, použijte automatický zápis zařízení.

6. Uložte profil pomocí tlačítka **Vytvořit**.

## <a name="direct-enrollment"></a>Přímá registrace
Protože Přímá registrace podporuje jenom registraci bez přidružení uživatele, portál společnosti se nedá použít k instalaci dostupných aplikací.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Exportovat profil a nainstalovat na zařízení macOS

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Registrovat zařízení**  >  **Apple registrace**  >  **Apple Configuratoru**  >  **Profiles** > vyberte profil pro export > **exportovat profil**.
2. V části **Přímá registrace** zvolte **Stáhnout profil** a soubor uložte. 

     > [!NOTE]
     > Stažený registrační profil je platný po dobu dvou týdnů po stažení. Pomocí tohoto odkazu si můžete stáhnout tolik profilů zápisu, kolik potřebujete. Stažení nového profilu nezobrazuje předchozí neplatnou hodnotu, ale zároveň nerozšiřuje dobu vypršení dříve staženého souboru.
         
3. Přeneste soubor do počítače s macOS a nainstalujte ho přímo.
4. Dvojím kliknutím na uložený soubor **. mobileconfig** otevřete soubor v části profily.
5. Po zobrazení výzvy k instalaci profilu správy vyberte **instalovat**.
6. Potvrďte další výzvu, kterou chcete nainstalovat profil pro správu, výběrem možnosti **nainstalovat**.
7. Zadejte přihlašovací údaje pro účet správce na zařízení macOS a klikněte na **OK**.
8. Zařízení macOS je teď zaregistrované v Intune a spravované, cílené profily se začnou stahovat.

## <a name="next-steps"></a>Další kroky

Po zaregistrování zařízení macOS můžete začít [Spravovat](../remote-actions/device-management.md).