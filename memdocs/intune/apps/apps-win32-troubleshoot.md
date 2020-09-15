---
title: Řešení potíží s aplikacemi Win32 v Microsoft Intune
titleSuffix: ''
description: Přečtěte si o nejběžnějších metodách odstraňování potíží s aplikacemi Win32 pomocí Microsoft Intune.
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
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083909"
---
# <a name="troubleshoot-win32-app-issues"></a>Řešení potíží s aplikacemi Win32

Při řešení potíží s aplikacemi Win32 používanými v Microsoft Intune můžete použít několik metod. Tento článek poskytuje informace o odstraňování potíží a informace, které vám pomůžou vyřešit problémy s aplikacemi Win32. Další informace najdete v tématu materiály k [řešení potíží s instalací aplikace Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting) .

> [!NOTE]
> Tato funkce správy aplikací podporuje jak 32, tak 64 architektury operačních systémů pro aplikace pro Windows.

> [!IMPORTANT]
> Když nasazujete aplikace Win32, zvažte výhradně použití [rozšíření pro správu služby Intune](../apps/intune-management-extension.md) , zejména v případě, že máte k dispozici instalační program Win32 aplikace s více soubory. Pokud během registrace autopilotu kombinujete instalaci aplikací Win32 a obchodních aplikací (LOB), může instalace aplikace selhat. Rozšíření pro správu Intune se nainstaluje automaticky, když se k uživateli nebo zařízení přiřadí skript prostředí PowerShell nebo aplikace Win32.

## <a name="app-troubleshooting-details"></a>Podrobnosti o řešení potíží s aplikací

Můžete si zobrazit potíže s instalací, například to, kdy byla aplikace vytvořena, upravena, zacílena a dodána do zařízení. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) najdete tyto a další podrobnosti v podokně **Poradce při potížích a podpoře** . Další informace najdete v tématu [informace o řešení potíží s aplikacemi](troubleshoot-app-install.md#app-troubleshooting-details).

## <a name="troubleshooting-app-issues-by-using-logs"></a>Řešení potíží s aplikacemi pomocí protokolů

Zobrazení podrobností protokolů vám pomůže určit příčinu problémů, které vidíte, a pomohou vám je vyřešit. Můžete se rozhodnout zobrazit [protokoly zobrazené v Intune](apps-win32-troubleshoot.md#logs-displayed-in-intune)nebo zobrazit [protokoly zobrazené prostřednictvím CMTrace](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace). 

### <a name="logs-displayed-in-intune"></a>Protokoly zobrazené v Intune

Když dojde k potížím s instalací aplikace Win32, můžete zvolit možnost **shromáždit protokoly** v podokně podrobností o **instalaci** aplikace v Intune. Další podrobnosti najdete v tématu [řešení potíží s instalací aplikace Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-through-cmtrace"></a>Protokoly zobrazené prostřednictvím CMTrace

Protokoly agenta v klientském počítači jsou běžně v *C:\ProgramData\Microsoft\IntuneManagementExtension\Logs*. K zobrazení těchto souborů protokolu můžete použít *CMTrace.exe* . Další informace najdete v tématu [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Snímek obrazovky protokolů agenta v klientském počítači.](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> Aby bylo možné zajistit správnou instalaci a spouštění aplikací pro podnikovou aplikaci Win32, by antimalwarové nastavení mělo vyloučit, že se prohledají následující adresáře:<p>
> **Na klientských počítačích x64**:<br>
> *C:\Program Files (x86) \Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **Na klientských počítačích x86**:<br>
> *C:\Program Files\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> Další informace najdete v tématu [doporučení pro kontrolu virů pro podnikové počítače, na kterých běží aktuálně podporované verze Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>Zjištění verze souboru aplikace Win32 pomocí prostředí PowerShell

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

V předchozím příkazu PowerShellu nahraďte `<path to binary file>` řetězec cestou k souboru aplikace Win32. Příklad cesty by byl podobný následujícímu:

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Nahraďte `<file version of successfully detected file>` řetězec verzí souboru, který je třeba zjistit. Příklad řetězce verze souboru by byl podobný následujícímu:

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Pokud potřebujete získat informace o verzi vaší aplikace Win32, můžete použít následující příkaz prostředí PowerShell:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

V předchozím příkazu PowerShellu nahraďte `<path to binary file>` cestu k souboru.

## <a name="additional-troubleshooting-areas-to-consider"></a>Další oblasti řešení potíží, které je potřeba zvážit
- Zkontrolujte cíle a ujistěte se, že je na zařízení nainstalovaný agent. Aplikace Win32, která je cílem skupiny nebo skriptu prostředí PowerShell zaměřeného na skupinu, vytvoří zásady instalace agenta pro skupinu zabezpečení.
- Podívejte se na verzi operačního systému: Windows 10 1607 a novější.  
- Ověřte SKU Windows 10. Verze Windows 10 S nebo Windows spuštěné s povoleným režimem S podporují instalaci MSI.

Další informace o řešení potíží s aplikacemi Win32 najdete v tématu [řešení potíží s instalací aplikací Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting). Informace o typech aplikací na zařízeních ARM64 najdete v tématu [typy aplikací podporované na zařízeních ARM64](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## <a name="next-steps"></a>Další kroky

- [Řešení problémů s instalací aplikací](troubleshoot-app-install.md)
