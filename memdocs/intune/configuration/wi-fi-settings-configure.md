---
title: Vytvoření profilu Wi-Fi pro zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Projděte si postup vytvoření konfiguračního profilu zařízení v Microsoft Intune. Vytvářejte profily pro správce zařízení s Androidem, Android Enterprise, iOS pro Android, iOS, iPadOS, macOS, Windows 10 a novější a Windows Holografick pro firmy. Pomocí těchto profilů můžete vytvořit připojení Wi-Fi pro použití certifikátů, volbu typu protokolu EAP, výběr metody ověřování, povolení proxy a další.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed04114f40ee15a5da2ccfec60abd72999a0c326
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709383"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Přidání a použití nastavení Wi-Fi na zařízeních v Microsoft Intune

Wi-Fi je bezdrátová síť, kterou používá mnoho mobilních zařízení k získání přístupu k síti. Microsoft Intune obsahuje vestavěná nastavení Wi-Fi, která se dají nasadit pro uživatele a zařízení ve vaší organizaci. Tato skupina nastavení se nazývá "profil" a je možné ji přiřadit různým uživatelům a skupinám. Po přiřazení získají vaši uživatelé přístup k síti Wi-Fi vaší organizace bez toho, aby ji nakonfigurovali sami.

Můžete třeba nainstalovat novou Wi-Fi síť nazvanou Contoso Wi-Fi. Pak budete chtít nastavit všechna zařízení se systémem iOS/iPadOS pro připojení k této síti. Postup je následující:

1. Vytvořte profil sítě Wi-Fi, který obsahuje nastavení, která se připojují k bezdrátové síti Contoso Wi-Fi.
2. Přiřaďte profil ke skupině, která obsahuje všechny uživatele zařízení se systémem iOS/iPadOS.
3. Na svých zařízeních uživatelé naleznou novou síť Contoso Wi-Fi v seznamu bezdrátových sítí. Potom se mohou k této síti připojit s využitím metody ověřování, kterou zvolíte.

Tento článek obsahuje seznam kroků pro vytvoření profilu sítě Wi-Fi. Obsahuje také odkazy, které popisují různá nastavení pro jednotlivé platformy.

## <a name="supported-device-platforms"></a>Podporované platformy zařízení

Profily Wi-Fi podporují zařízení s následujícími platformami:

- Android 5 a novější
- Android Enterprise a beznabídkový režim
- iOS 11,0 a novější
- iPadOS 13,0 a novější
- macOS X 10,12 a novější
- Windows 10 a novější, Windows 10 Mobile a Windows Holografick pro firmy

> [!NOTE]
> Pro zařízení s Windows 8.1 můžete importovat konfiguraci Wi-Fi, kterou předtím vyexportujete z jiného zařízení.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte platformu zařízení. Možnosti:

      - **Správce zařízení s Androidem**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 a novější**
      - **Windows 8.1 a vyšší**

    - **Profil**: vyberte **Wi-Fi**.

      > [!TIP]
      >
      > - Pro zařízení s **Androidem Enterprise** spuštěná jako vyhrazené zařízení (beznabídkový režim) vyberte **jenom vlastník zařízení**  >  **Wi-Fi**.
      > - Pro **Windows 8.1 a novější**můžete zvolit **Import Wi-Fi**. Tato možnost umožňuje importovat nastavení Wi-Fi jako soubor XML, který jste předtím vyexportovali z jiného zařízení.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil WiFi pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte svou platformu:

    - [Správce zařízení s Androidem](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), včetně vyhrazených zařízení
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 a novější](wi-fi-settings-windows.md)
    - [Windows 8.1 a novější](wi-fi-settings-import-windows-8-1.md), včetně Windows holografického pro firmy

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

> [!TIP]
> Pokud pro profil sítě Wi-Fi používáte ověřování založené na certifikátech, nasaďte profil sítě Wi-Fi, profil certifikátu a důvěryhodný kořenový profil do stejných skupin, abyste zajistili, že každé zařízení dokáže rozpoznat legitimitu certifikační autority.  Další informace najdete v tématu [Postup konfigurace certifikátů pomocí Microsoft Intune](../protect/certificates-configure.md).


## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Pak [přiřaďte tento profil](device-profile-assign.md) a [sledujte jeho stav.](device-profile-monitor.md)..

[Problémy s profily sítě Wi-Fi v Intune](troubleshoot-wi-fi-profiles.md).
