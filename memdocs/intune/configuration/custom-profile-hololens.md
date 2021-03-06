---
title: Použití řízení aplikací v programu Windows Defender na zařízeních HoloLens 2 v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurujte zprostředkovatele CSP pro řízení aplikací (WDAC) v programu Windows Defender tak, aby povoloval nebo blokoval otevírání aplikací na zařízeních HoloLens 2 v Microsoft Intune. Použijte PowerShell a vlastní konfigurační profil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd0d83912a5362225cd49773eda334113d11482e
ms.sourcegitcommit: 84b134594a62ec6df4188cf39f3ea29b0b5f765b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747191"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Použití WDAC a prostředí Windows PowerShell k povolení nebo blokování aplikací na zařízeních HoloLens 2 pomocí Microsoft Intune

Zařízení Microsoft HoloLens 2 podporují [zprostředkovatele CSP pro řízení aplikací (WDAC) v programu Windows Defender](/windows/client-management/mdm/applicationcontrol-csp), který nahrazuje [poskytovatele AppLockeru](/windows/client-management/mdm/applocker-csp).

Pomocí Windows PowerShellu a Microsoft Intune můžete použít CSP WDAC k povolení nebo blokování otevírání určitých aplikací na zařízeních Microsoft HoloLens 2. Například můžete chtít, aby aplikace Cortana ve vaší organizaci otevřela nebo zabránila otevření v zařízeních HoloLens 2.

Tato funkce platí pro:

- Zařízení HoloLens 2 s Windows holografickým pro firmy

WDAC CSP vychází z [funkce řízení aplikací (WDAC) v programu Windows Defender](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). Můžete také [použít více zásad WDAC](/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

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
2. Získat informace o nainstalovaném balíčku aplikace na stolním počítači a HoloLens:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Zadejte například .

    ```powershell
    $package1 = Get-AppxPackage -name Microsoft.MicrosoftEdge
    ```

    Dále ověřte, že balíček obsahuje atributy aplikace:

    ```powershell
    $package1
    ```

    Zobrazí se podobné atributy jako v následujících podrobnostech o aplikaci:

    ```powershell
    Name              : Microsoft.MicrosoftEdge
    Publisher         : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        :
    Version           : 44.20190.1000.0
    PackageFullName   : Microsoft.MicrosoftEdge_44.20190.1000.0_neutral__8wekyb3d8bbwe
    InstallLocation   : C:\Windows\SystemApps\Microsoft.MicrosoftEdge_8wekyb3d8bbwe
    IsFramework       : False
    PackageFamilyName : Microsoft.MicrosoftEdge_8wekyb3d8bbwe
    PublisherId       : 8wekyb3d8bbwe
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

5. Převeďte zásady WDAC na **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Chcete-li cílit na všechny verze aplikace, v newPolicy.xml se ujistěte, že `PackageVersion="65535.65535.65535.65535"` je v uzlu odepřít:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Pro můžete `PackageFamilyNameRules` použít následující verze:

    - **Allow**: ENTER `PackageVersion, 0.0.0.0` , což znamená "povolí tuto verzi a vyšší".
    - **Deny**: zadejte `PackageVersion, 65535.65535.65535.65535` , což znamená "odmítnutí této verze a nižší".

6. Sloučení **newPolicy.xml** s výchozími zásadami, které jsou na stolním počítači. Tento krok vytvoří **mergedPolicy.xml**. Můžete například pro běh použít ovladače podepsané Windows, WHQL a ukládat podepsané aplikace:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Zakáže pravidlo **režimu auditu** v **mergedPolicy.xml**. Při sloučení se režim auditování automaticky zapne:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Povolit **InvalidateEAs pro pravidlo restartování** v **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Další informace o těchto pravidlech najdete v tématu [Principy pravidel zásad WDAC a pravidel souborů](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Převést **mergedPolicy.xml** do binárního formátu. Tento krok vytvoří **compiledPolicy. bin**. Tento binární soubor **compiledPolicy. bin** přidáte do Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Vytvoření vlastního profilu konfigurace zařízení v Intune:

    1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vytvořte vlastní konfigurační profil zařízení s Windows 10.

        Konkrétní postup najdete [v tématu Vytvoření vlastního profilu pomocí OMA-URI v Intune](custom-settings-configure.md).

    2. Když vytváříte profil, zadejte následující nastavení:

      - **OMA-URI:** Zadejte `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>/Policy`. Nahraďte `<PolicyGUID>` uzlem PolicyTypeID v souboru **mergedPolicy.xml** , který jste vytvořili v kroku 6.

        V našem příkladu zadejte `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076/Policy` .

        Identifikátor GUID zásad se **musí shodovat** s uzlem PolicyTypeID v souboru **mergedPolicy.xml** (vytvořený v kroku 6).

        OMA-URI používá [zprostředkovatele CSP pro ApplicationControl](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp). Další informace o uzlech tohoto CSP najdete na webu [APPLICATIONCONTROL CSP](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp).

      - **Datový typ**: nastavte na **soubor Base64**. Soubor automaticky převede z přihrádky na base64.
      - **Soubor certifikátu**: Nahrajte binární soubor **compiledPolicy. bin** (vytvořený v kroku 9).

      Vaše nastavení vypadá podobně jako u následujících nastavení:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Přidejte vlastní OMA-URI pro konfiguraci ApplicationControl CSP v Microsoft Intune.":::

11. Po [přiřazení](device-profile-assign.md) profilu ke skupině HoloLens 2 Ověřte stav profilu. Po úspěšném použití profilu restartujte zařízení HoloLens 2.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

[Přečtěte si další informace o vlastních profilech v Intune](custom-settings-configure.md).
