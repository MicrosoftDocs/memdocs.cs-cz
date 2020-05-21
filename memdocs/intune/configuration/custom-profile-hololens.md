---
title: Použití řízení aplikací v programu Windows Defender na zařízeních HoloLens 2 v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurujte zprostředkovatele CSP pro řízení aplikací (WDAC) v programu Windows Defender tak, aby povoloval nebo blokoval otevírání aplikací na zařízeních HoloLens 2 v Microsoft Intune. Použijte PowerShell a vlastní konfigurační profil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee388cf15eceb52d17e204a76f4aac1ccf6529e9
ms.sourcegitcommit: d8dc05476ecd5db7ecb36dc649b566b349ba263d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2020
ms.locfileid: "83733638"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Použití WDAC a prostředí Windows PowerShell k povolení nebo blokování aplikací na zařízeních HoloLens 2 pomocí Microsoft Intune

Zařízení Microsoft HoloLens 2 podporují [zprostředkovatele CSP pro řízení aplikací (WDAC) v programu Windows Defender](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp), který nahrazuje [poskytovatele AppLockeru](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).

Pomocí Windows PowerShellu a Microsoft Intune můžete použít CSP WDAC k povolení nebo blokování otevírání určitých aplikací na zařízeních Microsoft HoloLens 2. Například můžete chtít, aby aplikace Cortana ve vaší organizaci otevřela nebo zabránila otevření v zařízeních HoloLens 2.

Tato funkce platí pro:

- Zařízení HoloLens 2 s Windows holografickým pro firmy

WDAC CSP vychází z [funkce řízení aplikací (WDAC) v programu Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). Můžete také [použít více zásad WDAC](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

V tomto článku se dozvíte, jak:

1. K vytváření zásad WDAC použijte Windows PowerShell.
2. Pomocí prostředí Windows PowerShell převeďte pravidla zásad WDAC na XML, aktualizujte XML a pak soubor XML převeďte na binární soubor.
3. V Microsoft Intune vytvořte [vlastní konfigurační profil zařízení](custom-settings-windows-holographic.md), přidejte tento binární soubor zásad WDAC a zásadu použijte na vaše zařízení HoloLens 2.

V Intune je potřeba vytvořit vlastní konfigurační profil pro použití zprostředkovatele CSP pro řízení aplikací v programu Windows Defender (WDAC). 

Kroky v tomto článku použijte jako šablonu a umožněte nebo zamítnout otevírání určitých aplikací na zařízeních HoloLens 2.

## <a name="prerequisites"></a>Požadavky

- Seznámení s prostředím Windows PowerShell.
- Přihlaste se k Intune jako člen:

  - **Zásada a Správce profilů** nebo role **Intune správce role** Intune

    NEBO

  - Role **globálního správce** nebo **Správce služby Intune** v Azure AD

  [Řízení přístupu na základě role (RBAC) s Intune](../fundamentals/role-based-access-control.md) obsahuje další informace.

- Vytvořte skupinu uživatelů nebo zařízení pomocí zařízení HoloLens 2. Další informace najdete v tématu [skupiny uživatelů a skupiny zařízení](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Příklad

V tomto příkladu se pomocí Windows PowerShellu vytvoří zásada řízení aplikací (WDAC) v programu Windows Defender. Zásada zabraňuje otevření konkrétní aplikace. Pak pomocí Intune Nasaďte zásadu na zařízení HoloLens 2.

1. Na stolním počítači otevřete aplikaci **Windows PowerShell** .
2. Získat informace o nainstalovaném balíčku aplikace na stolním počítači:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Zadejte například .

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Dále ověřte, že balíček obsahuje atributy aplikace:

    ```powershell
    $package1
    ```

    Zobrazí se podobné atributy jako v následujících podrobnostech o aplikaci:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Vytvořte zásady WDAC a přidejte balíček aplikace do pravidla ODEPŘENí:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Opakujte kroky 2 a 3 pro všechny ostatní aplikace, které chcete odepřít:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Zadejte například .

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Převeďte zásady WDAC na **newPolicy. XML**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Chcete-li cílit na všechny verze aplikace, v newPolicy. XML se ujistěte, že `PackageVersion="65535.65535.65535.65535"` je v uzlu odepřít:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Pro můžete `PackageFamilyNameRules` použít následující verze:

    - **Allow**: ENTER `PackageVersion, 0.0.0.0` , což znamená "povolí tuto verzi a vyšší".
    - **Deny**: zadejte `PackageVersion, 65535.65535.65535.65535` , což znamená "odmítnutí této verze a nižší".

6. Slučte **newPolicy. XML** výchozími zásadami, které jsou na stolním počítači. Tento krok vytvoří **soubor mergedPolicy. XML**. Můžete například pro běh použít ovladače podepsané Windows, WHQL a ukládat podepsané aplikace:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Zakažte pravidlo **režimu auditu** v **souboru mergedPolicy. XML**. Při sloučení se režim auditování automaticky zapne:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. V **souboru mergedPolicy. XML**povolte **InvalidateEAs na pravidlo restartování** :

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Další informace o těchto pravidlech najdete v tématu [Principy pravidel zásad WDAC a pravidel souborů](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Převede **mergedPolicy. XML** do binárního formátu. Tento krok vytvoří **compiledPolicy. bin**. Tento binární soubor **compiledPolicy. bin** přidáte do Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Vytvoření vlastního profilu konfigurace zařízení v Intune:

    1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vytvořte vlastní konfigurační profil zařízení s Windows 10.

        Konkrétní postup najdete [v tématu Vytvoření vlastního profilu pomocí OMA-URI v Intune](custom-settings-configure.md).

    2. Když vytváříte profil, zadejte následující nastavení:

      - **OMA-URI:** Zadejte `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. Nahraďte `<PolicyGUID>` uzlem PolicyTypeID v souboru **mergedPolicy. XML** , který jste vytvořili v kroku 6.

        V našem příkladu zadejte `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076` .

        Identifikátor GUID zásad se **musí shodovat** s uzlem PolicyTypeID v souboru **mergedPolicy. XML** (vytvořeným v kroku 6).

      - **Datový typ**: nastavte na **soubor Base64**. Soubor automaticky převede z přihrádky na base64.
      - **Soubor certifikátu**: Nahrajte binární soubor **compiledPolicy. bin** (vytvořený v kroku 9).

      Vaše nastavení vypadá podobně jako u následujících nastavení:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Přidejte vlastní OMA-URI pro konfiguraci ApplicationControl CSP v Microsoft Intune.":::

11. Po [přiřazení](device-profile-assign.md) profilu ke skupině HoloLens 2 Ověřte stav profilu. Po úspěšném použití profilu restartujte zařízení HoloLens 2.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

[Přečtěte si další informace o vlastních profilech v Intune](custom-settings-configure.md).
