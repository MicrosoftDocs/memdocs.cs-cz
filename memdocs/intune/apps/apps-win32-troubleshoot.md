---
title: Řešení potíží s aplikacemi Win32 v Microsoft Intune
titleSuffix: ''
description: Přečtěte si o nejběžnějších metodách odstraňování potíží s aplikacemi Win32, které se používají s Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aec8ebdd5d91e71c3706df906ce0b18f88edc02
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003441"
---
# <a name="troubleshoot-win32-app-issues"></a>Řešení potíží s aplikacemi Win32

Při řešení potíží s aplikacemi Win32 používanými v Microsoft Intune máte k dispozici řadu metod, které můžete použít. Toto téma poskytuje informace o odstraňování potíží a také další informace, které vám pomůžou vyřešit problémy s aplikacemi Win32.  Prostředky pro [řešení potíží s instalací aplikace Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting) .

> [!NOTE]
> Tato funkce správy aplikací podporuje jak 32, tak 64 architekturu operačního systému pro aplikace Windows.

> [!IMPORTANT]
> Při nasazování aplikací Win32 zvažte výhradně použití přístupu [rozšíření správy Intune](../apps/intune-management-extension.md) , zejména v případě, že máte k dispozici instalační program aplikace pro více souborů Win32. Pokud během registrace automatického pilotního nasazení kombinujete instalaci aplikací Win32 a obchodních aplikací, může instalace aplikace selhat. Rozšíření pro správu Intune se nainstaluje automaticky, když se k uživateli nebo zařízení přiřadí skript prostředí PowerShell nebo aplikace Win32.

## <a name="app-troubleshooting-details"></a>Podrobnosti o řešení potíží s aplikací

Můžete si zobrazit potíže s instalací, například to, kdy byla aplikace vytvořena, upravena, zacílena a dodána do zařízení. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) najdete tyto a další podrobnosti v podokně **Poradce při potížích a podpoře** . Další informace najdete v tématu [informace o řešení potíží s aplikacemi](troubleshoot-app-install.md#app-troubleshooting-details).

## <a name="troubleshoot-app-issues-using-logs"></a>Řešení potíží s aplikacemi pomocí protokolů

Zobrazení podrobností protokolů vám pomůže určit příčinu problému, který vidíte, a pomůže vám ho vyřešit. Můžete se rozhodnout zobrazit [protokoly zobrazené v Intune](apps-win32-troubleshoot.md#logs-displayed-in-intune)nebo zobrazit [protokoly zobrazené pomocí CMTrace](apps-win32-troubleshoot.md#logs-displayed-using-cmtrace). 

### <a name="logs-displayed-in-intune"></a>Protokoly zobrazené v Intune

Když dojde k potížím s instalací aplikace Win32, můžete zvolit možnost **shromáždit protokoly** v podokně podrobností o **instalaci** aplikace v Intune. Další podrobnosti najdete v tématu [řešení potíží s instalací aplikace Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-using-cmtrace"></a>Protokoly zobrazené pomocí CMTrace

Protokoly agenta na klientském počítači se obvykle nachází ve složce `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`. K zobrazení těchto protokolů můžete využít nástroj `CMTrace.exe`. Další informace najdete v tématu [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Snímek obrazovky protokolů agenta v klientském počítači](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> Aby bylo možné správně nainstalovat a spustit aplikace pro obchodní prostředí Win32, nastavení antimalwarového programu by mělo vyloučit následující adresáře, aby byly prohledávány:<p>
> **Na klientských počítačích x64**:<br>
> *C:\Program Files (x86) \Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **Na klientských počítačích x86**:<br>
> *C:\Program Files\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> Další informace najdete v tématu [doporučení pro kontrolu virů pro podnikové počítače, na kterých běží aktuálně podporované verze Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## <a name="detecting-the-win32-app-file-version-using-powershell"></a>Zjištění verze souboru aplikace Win32 pomocí prostředí PowerShell

Pokud máte potíže s detekcí verze souboru aplikace Win32, zvažte použití nebo úpravy následujícího příkazu prostředí PowerShell:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

Ve výše uvedeném příkazu prostředí PowerShell nahraďte `<path to binary file>` řetězec cestou k souboru aplikace Win32. Příklad cesty by byl podobný následujícímu:<br>
`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Nahraďte `<file version of successfully detected file>` řetězec verzí souboru, který je třeba zjistit. Příklad řetězce verze souboru by byl podobný následujícímu:<br>
`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Pokud potřebujete získat informace o verzi vaší aplikace Win32, můžete použít následující příkaz prostředí PowerShell:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

V příkazu prostředí PowerShell nahraďte `<path to binary file>` cestou k souboru.

## <a name="additional-troubleshooting-areas-to-consider"></a>Další oblasti řešení potíží, které je potřeba zvážit
- Zkontroluje cílení, abyste měli jistotu, že je agent nainstalovaný na zařízení – aplikace Win32 zacílená na skupinu nebo powershellový skript zacílený na skupinu vytvoří zásady instalace agenta pro skupinu zabezpečení.
- Zkontrolujte verzi operačního systému – Windows 10 1607 a novější.  
- Zkontrolujte skladovou položku Windows 10 – Windows 10 S nebo verze Windows s povoleným režimem S nepodporují instalaci pomocí instalační služby MSI.

Další informace o řešení potíží s aplikacemi Win32 najdete v tématu [řešení potíží s instalací aplikací Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting). Informace o typech aplikací na zařízeních ARM64 najdete v tématu [typy aplikací podporované na zařízeních ARM64](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## <a name="next-steps"></a>Další kroky

- [Řešení potíží s instalací aplikací](troubleshoot-app-install.md)
