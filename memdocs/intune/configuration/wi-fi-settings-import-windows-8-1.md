---
title: Import nastavení Wi-Fi pro zařízení s Windows v Microsoft Intune – Azure | Microsoft Docs
description: Exportujte nastavení Wi-Fi ze zařízení s Windows jako soubor XML pomocí nástroje netsh wlan. Potom importem tohoto souboru do Intune vytvořte profil Wi-Fi pro zařízení s Windows 8.1, Windows 10 a Windows Holographic for Business.
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
ms.openlocfilehash: ef2c4593ad9809614b7e0d497745065fef12df69
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086386"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Import nastavení Wi-Fi pro zařízení s Windows v Intune

Pro zařízení s Windows můžete importovat konfigurační profil Wi-Fi, který jste předtím exportovali do souboru. **Pro zařízení, na kterých běží Windows 10 a vyšší, můžete také [vytvořit profil Wi-Fi](wi-fi-settings-windows.md) přímo v Intune**.

Platí pro:  
- Windows 8.1 a novější
- Windows 10 a novější
- Windows 10 Desktop nebo Mobile
- Windows Holographic for Business

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil zařízení v Microsoft Intune](wi-fi-settings-configure.md). Název profilu **musí** být stejný jako atribut Name v souboru XML profilu Wi-Fi. V opačném případě dojde k chybě.

## <a name="import-the-wi-fi-settings-into-intune"></a>Import nastavení Wi-Fi do Intune

- **Název připojení**: Zadejte název připojení Wi-Fi. Tento název se uživatelům zobrazí, když procházejí dostupné sítě Wi-Fi.
- **XML profilu**: klikněte na tlačítko Procházet a vyberte soubor XML obsahující nastavení profilu sítě Wi-Fi, které chcete importovat.
- **Obsah souboru**: Zobrazuje kód XML vybraného konfiguračního profilu.

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Export nastavení Wi-Fi ze zařízení s Windows

Ve Windows použijte k exportu stávajícího profilu Wi-Fi do souboru XML, který dokáže Intune přečíst, nástroj `netsh wlan`. Aby bylo možné profil úspěšně používat, musí se klíč vyexportovat jako prostý text.

Na počítači s Windows, který už má nainstalovaný požadovaný profil WiFi, použijte tento postup:

1. Vytvořte místní složku pro exportované profily Wi-Fi, například **c:\WiFi**.
2. Otevřete příkazový řádek jako správce.
3. Spusťte příkaz `netsh wlan show profiles`. Poznamenejte si název profilu, který chcete exportovat. V tomto příkladu je název profilu **WiFiNázev**.
4. Spusťte příkaz `netsh wlan export profile name="ProfileName" folder=c:\Wifi`. Tento příkaz vytvoří v cílové složce soubor profilu Wi-Fi s názvem **Wi-Fi-WiFiNázev.xml**.

> [!IMPORTANT]
> - Pokud exportujete profil Wi-Fi s předsdíleným klíčem, **musíte** do příkazu přidat `key=clear`. Zadejte například `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`.
> - Použití předsdíleného klíče se systémem Windows 10 způsobuje chybu opravy v Intune. Když k ní dojde, profil Wi-Fi se správně přiřadí k zařízení a profil bude fungovat podle očekávání.
> - Pokud exportujete profil Wi-Fi s předsdíleným klíčem, ověřte si, že je soubor chráněný. Klíč má formát prostého textu, takže jeho ochranu zajišťujete vy.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nic nedělá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Podívejte se na [Přehled nastavení sítě Wi-Fi](wi-fi-settings-configure.md), včetně dalších dostupných platforem.