---
title: Používání Azure AD pro přístup k rozhraním Intune API v Microsoft Graphu
titleSuffix: Microsoft Intune
description: Popisuje postup nutný pro aplikace, které používají pro přístup k rozhraní Intune API v Microsoft Graphu službu Azure AD.
keywords: intune graphapi c# powershell role oprávnění
author: dougeby
manager: dougeby
ms.author: dougeby
ms.date: 03/08/2018
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 79A67342-C06D-4D20-A447-678A6CB8D70A
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 720328ebe260c967bef4a879bd0ee33ae2f332a0
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915683"
---
# <a name="how-to-use-azure-ad-to-access-the-intune-apis-in-microsoft-graph"></a>Používání Azure AD pro přístup k rozhraním Intune API v Microsoft Graphu

Rozhraní [Microsoft Graph API](https://developer.microsoft.com/graph/) teď podporuje Microsoft Intune pomocí určitých rozhraní API a rolí oprávnění.  Rozhraní Microsoft Graph API používá k ověřování a řízení přístupu službu Azure Active Directory (Azure AD).  
Přístup k rozhraním Intune API v Microsoft Graphu vyžaduje:

- ID aplikace s těmito oprávněními:

  - Oprávnění k volání služby Azure AD a rozhraní Microsoft Graph API
  - Obory oprávnění, které jsou relevantní pro konkrétní úlohy aplikace

- Pověření uživatele s těmito oprávněními:

  - Oprávnění pro přístup k tenantovi Azure AD, který je přidružený k aplikaci
  - Oprávnění rolí, která jsou potřebná k podpoře oborů oprávnění aplikace

- Koncový uživatel musí udělit dané aplikaci oprávnění k provádění úloh aplikací pro jejich tenanta Azure.

Tento článek:

- Postup pro registraci aplikace s přístupem k rozhraní Microsoft Graph API a příslušnými oprávněními rolí

- Popis rolí oprávnění rozhraní Intune API

- Příklady ověřování rozhraní Intune API pro C# a PowerShell

- Popisuje postup pro podporu více tenantů.

Další informace naleznete v tématu:

- [Autorizace přístupu k webovým aplikacím s použitím OAuth 2.0 a Azure Active Directory](/azure/active-directory/develop/active-directory-protocols-oauth-code)
- [Začínáme s ověřováním Azure AD](https://www.visualstudio.com/docs/integrate/get-started/auth/oauth)
- [Integrace aplikací se službou Azure Active Directory](/azure/active-directory/develop/active-directory-integrating-applications)
- [Principy OAuth 2.0](https://oauth.net/2/)

## <a name="register-apps-to-use-the-microsoft-graph-api"></a>Registrace aplikací k používání rozhraní Microsoft Graph API

Postup pro registraci aplikace k používání rozhraní Microsoft Graph API:

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) pomocí přihlašovacích údajů správce.

    Podle potřeby můžete použít:
    - Účet správce tenanta
    - Uživatelský účet tenanta se zapnutou možností **Uživatelé můžou registrovat aplikace**

2. V nabídce zvolte **Azure Active Directory** &gt; **Registrace aplikací**.

    <img src="../media/azure-ad-app-reg.png" width="157" height="170" alt="The App registrations menu command" />

3. Zvolte **Registrace nové aplikace** a vytvořte novou aplikaci, nebo zvolte existující aplikaci.  (Pokud zvolíte existující aplikaci, přeskočte další krok.)

4. V okně **Vytvořit** zadejte následující informace:

    1. **Název** pro aplikaci (zobrazuje se při přihlášení uživatele)

    2. Hodnoty **Typ aplikace** a **Identifikátor URI pro přesměrování**

        Tyto hodnoty se budou lišit podle vašich požadavků. Pokud používáte například Azure AD [Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) (ADAL), nastavte **Typ aplikace** na `Native` a **Identifikátor URI pro přesměrování** na `urn:ietf:wg:oauth:2.0:oob`.

        > [!NOTE]
        > Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).


        <img src="../media/azure-ad-app-new.png" width="209" height="140" alt="New app properties and values" />

        Další informace najdete v tématu [Scénáře ověřování pro Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios).

5. V okně aplikace:

    1. Všimněte si hodnoty **ID aplikace**.

    2. Zvolte **Nastavení** &gt; **Přístup přes rozhraní API** &gt; **Požadovaná oprávnění**.

    <img src="../media/azure-ad-req-perm.png" width="483" height="186" alt="The Required permissions setting" />

6. V okně **Požadovaná oprávnění** zvolte **Přidat** &gt; **Přidat přístup přes rozhraní API** &gt; **Vyberte rozhraní API**.

    <img src="../media/azure-ad-add-graph.png" width="436" height="140" alt="The Microsoft Graph setting" />

7. V okně **Vyberte rozhraní API** zvolte **Microsoft Graph** &gt; **Vybrat**.  Otevře se okno **Povolit přístup**, které obsahuje obory oprávnění dostupné pro aplikaci.

    <img src="../media/azure-ad-perm-scopes.png" width="489" height="248" alt="Intune Graph API permission scopes" />

    Vyberte požadované role pro aplikaci tak, že zaškrtnete políčko nalevo od příslušného názvu.  Další informace o konkrétních oborech oprávnění pro Intune najdete v tématu [Obory oprávnění pro Intune](#intune-permission-scopes).  Další informace o dalších oborech oprávnění pro rozhraní Graph API najdete v tématu [Referenční informace o oprávněních pro Microsoft Graph](/graph/permissions-reference).

    Nejlepších výsledků dosáhnete, když zvolíte co nejméně rolí potřebných k implementaci aplikace.

    Až budete hotoví, zvolte **Vybrat** a **Hotovo**, aby se změny uložily.

V tomto okamžiku můžete udělat také toto:

- Udělení oprávnění všem účtům tenantů, aby mohly používat aplikaci bez zadání pověření  

    Pokud to chcete udělat, zvolte **Udělit oprávnění** a potvrďte výzvu k potvrzení.

    Při prvním spuštění dané aplikace se zobrazí výzva, abyste aplikaci udělili oprávnění k provádění vybraných rolí.

    <img src="../media/azure-ad-grant-perm.png" width="351" height="162" alt="The Grant permissions button" />

- Zpřístupnění aplikace uživatelům mimo vašeho tenanta  (Toto se obvykle vyžaduje jenom u partnerů podporujících více tenantů nebo organizací.)  

    Postupujte následovně:

  1. V okně aplikace zvolte **Manifest**. Otevře se okno **Upravit manifest**.

     <img src="../media/azure-ad-edit-mft.png" width="295" height="114" alt="The Edit manifest blade" />

  2. Změňte hodnotu nastavení `availableToOtherTenants` na `true`.

  3. Uložte provedené změny.

## <a name="intune-permission-scopes"></a>Obory oprávnění pro Intune

Azure AD a Microsoft Graph používají obory oprávnění k řízení přístupu k podnikovým prostředkům.  

Obory oprávnění (označují se také jako _rozsahy OAuth_) řídí přístup ke konkrétním entitám Intune a jejich vlastnostem. Tento oddíl shrnuje obory oprávnění pro funkce rozhraní Intune API.

Další informace najdete v tématech:
- [Ověřování Azure AD](/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication)
- [Obory oprávnění aplikací](/azure/active-directory/develop/active-directory-v2-scopes)

Když udělujete oprávnění pro Microsoft Graph, můžete určit následující obory pro řízení přístupu k funkcím Intune: Následující tabulka shrnuje obory oprávnění rozhraní Intune API.  V prvním sloupci je název funkce, který se zobrazuje na portálu Azure Portal, a ve druhém sloupci je název oboru oprávnění.

Nastavení _Povolit přístup_ | Název oboru
:--|---
__Provádění vzdálených akcí s dopadem na uživatele na zařízeních v Microsoft Intune__ | [DeviceManagementManagedDevices. PrivilegedOperations. All](#mgd-po)
__Čtení a zápis do zařízení v Microsoft Intune__ | [DeviceManagementManagedDevices.. All](#mgd-rw)
__Čtení zařízení v Microsoft Intune__ | [DeviceManagementManagedDevices.Read.All](#mgd-ro)
__Čtení a zápis nastavení RBAC v Microsoft Intune__ | [DeviceManagementRBAC.ReadWrite.All](#rac-rw)
__Čtení nastavení RBAC v Microsoft Intune__ | DeviceManagementRBAC.Read.All
__Čtení a zápis aplikací v Microsoft Intune__ | [DeviceManagementApps.ReadWrite.All](#app-rw)
__Čtení aplikací v Microsoft Intune__ | [DeviceManagementApps.Read.All](#app-ro)
__Čtení a zápis konfigurace a zásad zařízení v Microsoft Intune__ | DeviceManagementConfiguration.ReadWrite.All
__Čtení konfigurace a zásad zařízení v Microsoft Intune__ | [DeviceManagementConfiguration. Read. All](#cfg-ro)
__Čtení a zápis konfigurace v Microsoft Intune__ | [DeviceManagementServiceConfig.ReadWrite.All](#svc-rw)
__Čtení konfigurace v Microsoft Intune__ | DeviceManagementServiceConfig.Read.All

Tabulka uvádí seznam nastavení v pořadí, ve kterém se zobrazují na portálu Azure Portal. Následující oddíly popisují obory v abecedním pořadí.

V současné době všechny obory oprávnění Intune vyžadují přístup správce.  To znamená, že ke spouštění aplikací nebo skriptů přistupujících k prostředkům s rozhraním Intune API se vyžadují odpovídající pověření.

### <a name="devicemanagementappsreadall"></a><a name="app-ro"></a>DeviceManagementApps.Read.All

- Nastavení **Povolit přístup**: __Čtení aplikací v Microsoft Intune__

- Povoluje přístup pro čtení vlastností a stavu následujících entit:
  - Klientské aplikace
  - Kategorie mobilních aplikací
  - Zásady ochrany aplikací
  - Konfigurace aplikací

### <a name="devicemanagementappsreadwriteall"></a><a name="app-rw"></a>DeviceManagementApps.ReadWrite.All

- Nastavení **Povolit přístup**: __Čtení a zápis aplikací v Microsoft Intune__

- Umožňuje stejné operace jako __DeviceManagementApps.Read.All__

- Povoluje také provádění změn následujících entit:

  - Klientské aplikace
  - Kategorie mobilních aplikací
  - Zásady ochrany aplikací
  - Konfigurace aplikací

### <a name="devicemanagementconfigurationreadall"></a><a name="cfg-ro"></a>DeviceManagementConfiguration.Read.All

- Nastavení **Povolit přístup**: __Čtení konfigurace a zásad zařízení v Microsoft Intune__

- Povoluje přístup pro čtení vlastností a stavu následujících entit:
  - Konfigurace zařízení
  - Zásady dodržování předpisů pro zařízení
  - Oznamovací zprávy

### <a name="devicemanagementconfigurationreadwriteall"></a><a name="cfg-ra"></a>DeviceManagementConfiguration.ReadWrite.All

- Nastavení **Povolit přístup**: __Čtení a zápis konfigurace a zásad zařízení v Microsoft Intune__

- Umožňuje stejné operace jako __DeviceManagementConfiguration.Read.All__

- Aplikace můžou také vytvářet, přiřazovat, odstraňovat a měnit následující entity:
  - Konfigurace zařízení
  - Zásady dodržování předpisů pro zařízení
  - Oznamovací zprávy

### <a name="devicemanagementmanageddevicesprivilegedoperationsall"></a><a name="mgd-po"></a>DeviceManagementManagedDevices.PrivilegedOperations.All

- Nastavení **Povolit přístup**: __Provádění vzdálených akcí s dopadem na uživatele na zařízeních v Microsoft Intune__

- Povoluje na spravovaném zařízení následující vzdálené akce:
  - Vyřazení
  - Vymazání
  - Resetování nebo obnovení hesla
  - Vzdálené uzamčení
  - Povolení nebo zakázání režimu ztráty
  - Vyčistění počítače
  - Restartování
  - Odstranění uživatele ze sdíleného zařízení

### <a name="devicemanagementmanageddevicesreadall"></a><a name="mgd-ro"></a>DeviceManagementManagedDevices.Read.All

- Nastavení **Povolit přístup**: __Čtení zařízení v Microsoft Intune__

- Povoluje přístup pro čtení vlastností a stavu následujících entit:
  - Spravované zařízení
  - Kategorie zařízení
  - Zjištěná aplikace
  - Vzdálené akce
  - Informace o malwaru

### <a name="devicemanagementmanageddevicesreadwriteall"></a><a name="mgd-rw"></a>DeviceManagementManagedDevices.ReadWrite.All

- Nastavení **Povolit přístup**: __Čtení a zápis zařízení v Microsoft Intune__

- Umožňuje stejné operace jako __DeviceManagementManagedDevices.Read.All__

- Aplikace můžou také vytvářet, odstraňovat a měnit následující entity:
  - Spravované zařízení
  - Kategorie zařízení

- Povolené jsou i tyto vzdálené akce:
  - Najít zařízení
  - Zakázání zámku aktivace
  - Požádat o vzdálenou pomoc

### <a name="devicemanagementrbacreadall"></a><a name="rac-ro"></a>DeviceManagementRBAC.Read.All

- Nastavení **Povolit přístup**: __Čtení nastavení RBAC v Microsoft Intune__

- Povoluje přístup pro čtení vlastností a stavu následujících entit:
  - Přiřazení rolí
  - Definice rolí
  - Operace prostředků

### <a name="devicemanagementrbacreadwriteall"></a><a name="rac-rw"></a>DeviceManagementRBAC.ReadWrite.All

- Nastavení **Povolit přístup**: __Čtení a zápis nastavení RBAC v Microsoft Intune__

- Umožňuje stejné operace jako __DeviceManagementRBAC.Read.All__

- Aplikace můžou také vytvářet, přiřazovat, odstraňovat a měnit následující entity:
  - Přiřazení rolí
  - Definice rolí

### <a name="devicemanagementserviceconfigreadall"></a><a name="svc-ro"></a>DeviceManagementServiceConfig.Read.All

- Nastavení **Povolit přístup**: __Čtení konfigurace v Microsoft Intune__

- Povoluje přístup pro čtení vlastností a stavu následujících entit:
  - Registrace zařízení
  - Certifikát pro službu Apple Push Notification Service
  - Program Apple Device Enrollment Program
  - Apple Volume Purchase Program
  - Součást Exchange Connector
  - Podmínky a ujednání
  - Služba TEM (Telecom Expense Management)
  - Cloudová infrastruktura veřejných klíčů
  - Značka
  - Mobile Threat Defense

### <a name="devicemanagementserviceconfigreadwriteall"></a><a name="svc-rw"></a>DeviceManagementServiceConfig.ReadWrite.All

- Nastavení **Povolit přístup**: __Čtení a zápis konfigurace v Microsoft Intune__

- Umožňuje stejné operace jako DeviceManagementServiceConfig.Read.All_

- Aplikace můžou také nakonfigurovat následující funkce Intune:
  - Registrace zařízení
  - Certifikát pro službu Apple Push Notification Service
  - Program Apple Device Enrollment Program
  - Apple Volume Purchase Program
  - Součást Exchange Connector
  - Podmínky a ujednání
  - Služba TEM (Telecom Expense Management)
  - Cloudová infrastruktura veřejných klíčů
  - Značka
  - Mobile Threat Defense

## <a name="azure-ad-authentication-examples"></a>Příklady ověřování Azure AD

Tento oddíl ukazuje postup, jak začlenit Azure AD do projektů C# a PowerShellu.

V každém příkladu bude potřeba, abyste zadali ID aplikace, které má obor oprávnění alespoň `DeviceManagementManagedDevices.Read.All` (vysvětlení výše).

Při testování příkladů se vám můžou zobrazovat chyby stavu protokolu HTTP 403 (Zakázáno), které se podobají tomuto:

```json
{
  "error": {
    "code": "Forbidden",
    "message": "Application is not authorized to perform this operation - Operation ID " +
       "(for customer support): 00000000-0000-0000-0000-000000000000 - " +
       "Activity ID: cc7fa3b3-bb25-420b-bfb2-1498e598ba43 - " +
       "Url: https://example.manage.microsoft.com/" +
       "Service/Resource/RESTendpoint?" +
       "api-version=2017-03-06 - CustomApiErrorPhrase: ",
    "innerError": {
      "request-id": "00000000-0000-0000-0000-000000000000",
      "date": "1980-01-0112:00:00"
    }
  }
}
```

Pokud k tomu dojde, ověřte platnost těchto skutečností:

- Aktualizovali jste ID aplikace na takové, které má autorizaci k používání rozhraní Microsoft Graph API a oboru oprávnění `DeviceManagementManagedDevices.Read.All`.

- Pověření tenanta podporují funkce správy.

- Kód se podobá zobrazeným ukázkám.


### <a name="authenticate-azure-ad-in-c"></a>Ověřování služby Azure AD v C\#

Tento příklad ukazuje, jak pomocí C# načíst seznam zařízení přidružených k účtu Intune.

 > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

1. Spusťte Visual Studio a vytvořte nový projekt Konzolová aplikace (.NET Framework) pro Visual C#.

2. Zadejte název projektu a další podrobnosti podle potřeby.

    <img src="../media/aad-auth-cpp-new-console.png" width="624" height="433" alt="Creating a C# console app project in Visual Studio"  />

3. Pomocí Průzkumník řešení přidejte do projektu balíček NuGet Microsoft ADAL:

    1. Klikněte pravým tlačítkem myši na Průzkumníka řešení.
    1. Zvolte **Spravovat balíčky NuGet** &gt;**Procházet**.
    1. Vyberte `Microsoft.IdentityModel.Clients.ActiveDirectory` a pak zvolte **Nainstalovat**.

    <img src="../media/aad-auth-cpp-install-package.png" width="624" height="458" alt="Selecting the Azure AD identity model module" />

4. Přidejte do horní části **Program.cs** následující příkazy:

    ``` csharp
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Net.Http;
    ```

5. Přidejte metodu pro vytvoření autorizační hlavičky:

    ``` csharp
    private static async Task<string> GetAuthorizationHeader()
    {
        string applicationId = "<Your Application ID>";
        string authority = "https://login.microsoftonline.com/common/";
        Uri redirectUri = new Uri("urn:ietf:wg:oauth:2.0:oob");
        AuthenticationContext context = new AuthenticationContext(authority);
        AuthenticationResult result = await context.AcquireTokenAsync(
            "https://graph.microsoft.com",
            applicationId, redirectUri,
            new PlatformParameters(PromptBehavior.Auto));
        return result.CreateAuthorizationHeader();
    ```

    Nezapomeňte změnit hodnotu `application_ID` tak, aby odpovídala položce s uděleným oborem oprávnění aspoň `DeviceManagementManagedDevices.Read.All`, jak je popsáno výše.

6. Přidejte metodu pro načtení seznamu zařízení:

    ``` csharp
    private static async Task<string> GetMyManagedDevices()
    {
        string authHeader = await GetAuthorizationHeader();
        HttpClient graphClient = new HttpClient();
        graphClient.DefaultRequestHeaders.Add("Authorization", authHeader);
        return await graphClient.GetStringAsync(
            "https://graph.microsoft.com/beta/me/managedDevices");
    }
    ```

7. Aktualizujte příkaz **Main**, aby volal funkci **GetMyManagedDevices**:

    ``` csharp
    string devices = GetMyManagedDevices().GetAwaiter().GetResult();
    Console.WriteLine(devices);
    ```

8. Zkompilujte aplikaci a spusťte ji.  

Při prvním spuštění aplikace by se měly zobrazit dvě výzvy.  První požádá o přihlašovací údaje a druhá udělí oprávnění pro žádost `managedDevices`.  

Hotová aplikace pro referenci je zde:

``` csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;
using System.Net.Http;
using System.Threading.Tasks;

namespace IntuneGraphExample
{
    class Program
    {
        static void Main(string[] args)
        {
            string devices = GetMyManagedDevices().GetAwaiter().GetResult();
            Console.WriteLine(devices);
        }

        private static async Task<string> GetAuthorizationHeader()
        {
            string applicationId = "<Your Application ID>";
            string authority = "https://login.microsoftonline.com/common/";
            Uri redirectUri = new Uri("urn:ietf:wg:oauth:2.0:oob");
            AuthenticationContext context = new AuthenticationContext(authority);
            AuthenticationResult result = await context.AcquireTokenAsync("https://graph.microsoft.com", applicationId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
            return result.CreateAuthorizationHeader();
        }

        private static async Task<string> GetMyManagedDevices()
        {
            string authHeader = await GetAuthorizationHeader();
            HttpClient graphClient = new HttpClient();
            graphClient.DefaultRequestHeaders.Add("Authorization", authHeader);
            return await graphClient.GetStringAsync("https://graph.microsoft.com/beta/me/managedDevices");
        }
    }
}
```

### <a name="authenticate-azure-ad-powershell"></a>Ověřování služby Azure AD (PowerShell)

Následující skript PowerShellu používá k ověřování modul AzureAD PowerShell.  Další informace najdete v tématech [Azure Active Directory PowerShell verze 2](/powershell/azure/active-directory/install-adv2) a [Intune PowerShell – příklady](https://github.com/microsoftgraph/powershell-intune-samples).

V tomto příkladu se hodnota `$clientID` aktualizuje tak, aby odpovídala platnému ID aplikace.

``` powershell
function Get-AuthToken {
    [cmdletbinding()]
    param
    (
        [Parameter(Mandatory = $true)]
        $User
    )

    $userUpn = New-Object "System.Net.Mail.MailAddress" -ArgumentList $User
    $tenant = $userUpn.Host

    Write-Host "Checking for AzureAD module..."

    $AadModule = Get-Module -Name "AzureAD" -ListAvailable
    if ($AadModule -eq $null) {
        Write-Host "AzureAD PowerShell module not found, looking for AzureADPreview"
        $AadModule = Get-Module -Name "AzureADPreview" -ListAvailable
    }

    if ($AadModule -eq $null) {
        write-host
        write-host "AzureAD Powershell module not installed..." -f Red
        write-host "Install by running 'Install-Module AzureAD' or 'Install-Module AzureADPreview' from an elevated PowerShell prompt" -f Yellow
        write-host "Script can't continue..." -f Red
        write-host
        exit
    }

    # Getting path to ActiveDirectory Assemblies
    # If the module count is greater than 1 find the latest version

    if ($AadModule.count -gt 1) {
        $Latest_Version = ($AadModule | select version | Sort-Object)[-1]
        $aadModule = $AadModule | ? { $_.version -eq $Latest_Version.version }
        $adal = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.dll"
        $adalforms = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.Platform.dll"
    }

    else {
        $adal = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.dll"
        $adalforms = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.Platform.dll"
    }

    [System.Reflection.Assembly]::LoadFrom($adal) | Out-Null
    [System.Reflection.Assembly]::LoadFrom($adalforms) | Out-Null

    $clientId = "<Your Application ID>"
    $redirectUri = "urn:ietf:wg:oauth:2.0:oob"
    $resourceAppIdURI = "https://graph.microsoft.com"
    $authority = "https://login.microsoftonline.com/$Tenant"

    try {
        $authContext = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext" -ArgumentList $authority
        # https://msdn.microsoft.com/library/azure/microsoft.identitymodel.clients.activedirectory.promptbehavior.aspx
        # Change the prompt behaviour to force credentials each time: Auto, Always, Never, RefreshSession
        $platformParameters = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.PlatformParameters" -ArgumentList "Auto"
        $userId = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.UserIdentifier" -ArgumentList ($User, "OptionalDisplayableId")
        $authResult = $authContext.AcquireTokenAsync($resourceAppIdURI, $clientId, $redirectUri, $platformParameters, $userId).Result
        # If the accesstoken is valid then create the authentication header
        if ($authResult.AccessToken) {
            # Creating header for Authorization token
            $authHeader = @{
                'Content-Type' = 'application/json'
                'Authorization' = "Bearer " + $authResult.AccessToken
                'ExpiresOn' = $authResult.ExpiresOn
            }
            return $authHeader
        }
        else {
            Write-Host
            Write-Host "Authorization Access Token is null, please re-run authentication..." -ForegroundColor Red
            Write-Host
            break
        }
    }
    catch {
        write-host $_.Exception.Message -f Red
        write-host $_.Exception.ItemName -f Red
        write-host
        break
    }   
}

$authToken = Get-AuthToken -User "<Your AAD Username>"

try {
    $uri = "https://graph.microsoft.com/beta/me/managedDevices"
    Write-Verbose $uri
    (Invoke-RestMethod -Uri $uri –Headers $authToken –Method Get).Value
}
catch {
    $ex = $_.Exception
    $errorResponse = $ex.Response.GetResponseStream()
    $reader = New-Object System.IO.StreamReader($errorResponse)
    $reader.BaseStream.Position = 0
    $reader.DiscardBufferedData()
    $responseBody = $reader.ReadToEnd();
    Write-Host "Response content:`n$responseBody" -f Red
    Write-Error "Request to $Uri failed with HTTP Status $($ex.Response.StatusCode) $($ex.Response.StatusDescription)"
    write-host
    break
}
```

## <a name="support-multiple-tenants-and-partners"></a>Podpora více tenantů a partnerů

Pokud vaše organizace podporuje organizace, které mají svoje vlastní tenanty Azure AD, můžete vašim klientům povolit, aby používali vaši aplikaci se svými tenanty.

Postupujte následovně:

1. Ověřte, jestli v cílovém tenantovi Azure AD existuje účet daného klienta.

2. Ověřte, jestli účet vašeho tenanta umožňuje uživatelům registraci aplikací (viz **uživatelská nastavení**).

3. Vytvořte relaci mezi jednotlivými tenanty.  

    Můžete to udělat jedním z těchto způsobů:

    a. K definování relace s klientem a jeho e-mailové adresy použijte [Partnerské centrum Microsoftu](https://partnercenter.microsoft.com/).

    b. Pozvěte uživatele, aby se stal hostem vašeho tenanta.

Pozvání uživatele, aby se stal hostem vašeho tenanta:

1. Na panelu **Rychlé úkoly** zvolte **Přidat uživatele typu host**.

    <img src="../media/azure-ad-add-guest.png" width="448" height="138" alt="Use Quick Tasks to add a guest user" />

2. Zadejte e-mailovou adresu klienta a (volitelně) přidejte individuální zprávu pro pozvánku.

    <img src="../media/azure-ad-guest-invite.png" width="203" height="106" alt="Inviting an external user as a guest" />

3. Zvolte **Pozvat**.

Tím se uživateli odešle pozvánka.

   <img src="../media/aad-multiple-tenant-invitation.png" width="624" height="523" alt="A sample guest invitation" />

   Uživatel musí pozvánku přijmout výběrem odkazu **Začínáme**.

Po vytvoření relace (nebo přijetí pozvánky) přidejte daný uživatelský účet k **roli adresáře**.

Nezapomeňte uživatele přidat podle potřeby k dalším rolím. Například aby uživatel mohl spravovat nastavení Intune, musí mít roli **Globální správce** nebo **Správce služby Intune**.

Navíc:

- Pomocí webu https://admin.microsoft.com přiřaďte licenci pro Intune k vašemu uživatelskému účtu.

- Aktualizujte kód aplikace k ověřování v doméně tenanta služby Azure AD daného klienta, nikoli ve vaší vlastní.

    Předpokládejme například, že vaše doména tenanta je `contosopartner.onmicrosoft.com` a doména tenanta vašeho klienta je `northwind.onmicrosoft.com`. Aktualizovali byste tedy kód pro ověřování v tenantovi vašeho klienta.

    Když to budete dělat v aplikaci C# na základě předchozího příkladu, změníte hodnotu proměnné `authority`:

    ``` csharp
    string authority = "https://login.microsoftonline.com/common/";
    ```

    na

    ``` csharp
    string authority = "https://login.microsoftonline.com/northwind.onmicrosoft.com/";
    ```