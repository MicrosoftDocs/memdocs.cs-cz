---
title: Import nastavení Wi-Fi pro zařízení s Windows v Microsoft Intune – Azure | Microsoft Docs
description: Exportujte nastavení Wi-Fi ze zařízení s Windows jako soubor XML pomocí nástroje netsh wlan. Potom importem tohoto souboru do Intune vytvořte profil Wi-Fi pro zařízení s Windows 8.1, Windows 10 a Windows Holographic for Business.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8cd8deb04dc939ed3dc742c9066c6dbfd4f51f3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332931"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Import nastavení Wi-Fi pro zařízení s Windows v Intune

Pro zařízení s Windows můžete importovat konfigurační profil Wi-Fi, který jste předtím exportovali do souboru. **Pro zařízení, na kterých běží Windows 10 a vyšší, můžete také [vytvořit profil Wi-Fi](wi-fi-settings-windows.md) přímo v Intune**.

Platí pro:  
- Windows 8.1 a novější
- Windows 10 a novější
- Windows 10 Desktop nebo Mobile
- Windows Holographic for Business

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Export nastavení Wi-Fi ze zařízení s Windows

Ve Windows použijte k exportu stávajícího profilu Wi-Fi do souboru XML, který dokáže Intune přečíst, nástroj `netsh wlan`. Aby bylo možné profil úspěšně používat, musí se klíč vyexportovat jako prostý text.

Na počítači s Windows, který už má nainstalovaný požadovaný profil WiFi, použijte tento postup:

1. Vytvořte místní složku pro exportované profily Wi-Fi, například **c:\WiFi**.
2. Otevřete příkazový řádek jako správce.
3. Spusťte příkaz `netsh wlan show profiles`. Poznamenejte si název profilu, který chcete exportovat. V tomto příkladu je název profilu **WiFiNázev**.
4. Spusťte příkaz `netsh wlan export profile name="ProfileName" folder=c:\Wifi`. Tento příkaz vytvoří v cílové složce soubor profilu Wi-Fi s názvem **Wi-Fi-WiFiNázev.xml**.

## <a name="import-the-wi-fi-settings-into-intune"></a>Import nastavení Wi-Fi do Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Název **musí** být stejný jako atribut name v souboru XML profilu Wi-Fi. V opačném případě dojde k chybě.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **Platforma**: vyberte **Windows 8.1 a novější**.
    - **Typ profilu**: vyberte **Import Wi-Fi**.

    > [!IMPORTANT]
    > - Pokud exportujete profil Wi-Fi s předsdíleným klíčem, **musíte** do příkazu přidat `key=clear`. Zadejte například `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`.
    > - Použití předsdíleného klíče se systémem Windows 10 způsobuje chybu opravy v Intune. Když k ní dojde, profil Wi-Fi se správně přiřadí k zařízení a profil bude fungovat podle očekávání.
    > - Pokud exportujete profil Wi-Fi s předsdíleným klíčem, ověřte si, že je soubor chráněný. Klíč má formát prostého textu, takže jeho ochranu zajišťujete vy.

4. Zadejte následující nastavení:

    - **Název připojení**: Zadejte název připojení Wi-Fi. Tento název se uživatelům zobrazí, když procházejí dostupné sítě Wi-Fi.
    - **XML profilu**: klikněte na tlačítko Procházet a vyberte soubor XML obsahující nastavení profilu sítě Wi-Fi, které chcete importovat.
    - **Obsah souboru**: Zobrazuje kód XML vybraného konfiguračního profilu.

5. Výběrem **OK** uložte změny.
6. Po dokončení vyberte **OK** > **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Podívejte se na [Přehled nastavení sítě Wi-Fi](wi-fi-settings-configure.md), včetně dalších dostupných platforem.
