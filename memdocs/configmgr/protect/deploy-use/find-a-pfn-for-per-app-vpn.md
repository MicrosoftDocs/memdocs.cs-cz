---
title: Vyhledání identity aplikace pro sítě VPN jednotlivých aplikací
titleSuffix: Configuration Manager
description: Přečtěte si o dvou způsobech, jak najít název řady balíčků, abyste mohli nakonfigurovat síť VPN pro jednotlivé aplikace.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 49f9f7972d5e48b0ec646568d85376027bf278c3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906819"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Vyhledání identity aplikace pro sítě VPN jednotlivých aplikací

*Platí pro: Configuration Manager (Current Branch)*


Existují dva způsoby jak najít PFN, abyste mohli konfigurovat síť VPN pro aplikaci.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Hledání PFN pro aplikaci, která je nainstalovaná na počítači s Windows 10

Pokud pracujete s aplikací, která je již nainstalována v počítači s Windows 10, můžete k získání PFN použít rutinu PowerShellu [Get-AppxPackage](https://docs.microsoft.com/powershell/module/appx/get-appxpackage?view=win10-ps).

Syntaxe pro Get-AppxPackage:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Možná bude nutné spustit PowerShell jako správce, aby bylo možné načíst PFN.

Chcete-li například získat informace o všech univerzálních aplikacích nainstalovaných na počítače, použijte `Get-AppxPackage`.

Chcete-li získat informace o aplikaci, jejíž název nebo část názvu znáte, použijte `Get-AppxPackage *<app_name>`. Všimněte si použití zástupného znaku, které je zvláště užitečné, pokud si nejste jisti úplným názvem aplikace. Pokud chcete například získat informace pro aplikaci OneNote, použijte `Get-AppxPackage *OneNote`.


Zde jsou informace načtené pro OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Hledání PFN, pokud aplikace není nainstalovaná na počítači

1. Přejděte na https://www.microsoft.com/store/apps.
2. Zadejte název aplikace v panelu vyhledávání. V našem příkladu hledejte OneNote.
3. Klikněte na odkaz na aplikaci. Všimněte si, že adresa URL, ke které přistupujete, má na konci řadu písmen. V našem příkladu vypadá adresa URL takto:`https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. Na jiné kartě vložte následující adresu URL, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata` nahraďte `<app id>` ID aplikace, kterou jste získali https://www.microsoft.com/store/apps – na konci adresy URL v kroku 3 se zobrazí řada písmen. V našem příkladu (pro OneNote) byste vložili adresu `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

V Edgi se požadované informace zobrazí, v Internet Exploreru je zobrazíte kliknutím na **Otevřít**. Hodnota PFN je uvedena na prvním řádku. Zde jsou uvedené výsledky pro náš příklad:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
