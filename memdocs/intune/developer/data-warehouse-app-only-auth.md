---
title: Ověřování v Intune Data Warehouse pouze na úrovni aplikace
titleSuffix: Microsoft Intune
description: Toto téma popisuje ověřování pouze aplikace datového skladu pro Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: d7166563-6bb5-4624-b8c8-6b300a997c3a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: daa4d079d60dc7474e5ba6a140e07a77e25b347d
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165970"
---
# <a name="intune-data-warehouse-application-only-authentication"></a>Ověřování v Intune Data Warehouse pouze na úrovni aplikace

Můžete nastavit aplikaci pomocí Azure Active Directory (Azure AD) a ověřit ji přes Intune Data Warehouse. Tento proces je užitečný pro weby, aplikace a procesy na pozadí, kde by aplikace neměla mít přístup k přihlašovacím údajům uživatelů. Pomocí následujících kroků autorizujete aplikaci v Azure AD pomocí OAuth 2.0.

## <a name="authorization"></a>Autorizace

Azure Active Directory (Azure AD) používá standard OAuth 2.0 za účelem umožnění autorizace přístupu k webovým aplikacím a webovým rozhraním API v tenantovi Azure AD. Tento průvodce vám ukáže, jak ověřit aplikaci pomocí jazyka C#. Tok autorizačního kódu OAuth 2.0 je popsaný v oddíle 4.1 specifikace standardu OAuth 2.0. Další informace najdete v tématu [Autorizace přístupu k webovým aplikacím pomocí OAuth 2.0 a Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code).


## <a name="azure-keyvault"></a>Azure KeyVault

Následující proces používá ke zpracování a převodu klíče aplikace privátní metodu. Tato privátní metoda se jmenuje SecureString. Jako alternativu můžete k uložení klíče aplikace použít Azure KeyVault. Další informace najdete v tématu [Key Vault](https://azure.microsoft.com/services/key-vault/).

## <a name="create-a-web-app"></a>Vytvoření webové aplikace

V této části zadáte podrobnosti o webové aplikaci, na kterou byste chtěli ukázat v Intune. Webová aplikace představuje aplikaci klient-server. Server poskytuje webovou aplikaci, která zahrnuje uživatelské rozhraní, obsah a funkce. Tento typ aplikace se samostatně udržuje na webu. Přístup do Intune můžete webové aplikaci udělit pomocí Intune. Tok dat iniciuje webová aplikace. 

1. Přihlaste se k [portálu Azure Portal](https://portal.azure.com).
2. Pomocí pole **Hledat prostředky, služby a dokumenty** v horní části portálu Azure vyhledejte **Azure Active Directory**.
3. V rozevírací nabídce vyberte **Azure Active Directory** pod položkou **Služby**.
4. Vyberte **Registrace aplikací**.
5. Klikněte na možnost **Registrace nové aplikace**, která zobrazí okno **Vytvořit**.
6. V okně **Vytvořit** přidejte podrobnosti o aplikaci:

    - Název aplikace, jako například *Ověřování v Intune pro aplikace*.
    - **Typ aplikace**. Zvolte **Webová aplikace / webové rozhraní API** a přidejte aplikaci, která představuje webovou aplikaci, webové rozhraní API nebo obojí.
    - **Přihlašovací adresa URL** aplikace. Je to umístění, na které uživatelé automaticky přejdou během procesu ověřování. Budou požádáni, aby prokázali svoji totožnost. Další informace najdete v článku [Co je přístup k aplikaci a jednotné přihlašování s Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

7. Klikněte na **Vytvořit** v dolní části okna **Vytvořit**.

    >[!NOTE] 
    > Zkopírujte **ID aplikace** z okna **Registrovaná aplikace** pro pozdější použití.

## <a name="create-a-key"></a>Vytvoření klíče

V této části Azure AD vygeneruje hodnotu klíče pro vaši aplikaci.

1. V okně **Registrace aplikací** vyberte nově vytvořenou aplikaci, aby se zobrazilo okno aplikace.
2. V horní části okna vyberte **Nastavení**, aby se zobrazilo okno **Nastavení**.
3. V okně **Nastavení** vyberte **Klíče**.
4. Přidejte **popis** klíče, **konec platnosti** a **hodnotu** klíče.
5. Kliknutím na **Uložit** uložte a aktualizujte klíče aplikace.
6. Je nutné zkopírovat vygenerovanou hodnotu klíče (v kódování base64).

    >[!NOTE] 
    > Hodnota klíče po opuštění okna **klíče** zmizí. Klíč nemůžete z tohoto okna načíst později. Zkopírujte si ho pro pozdější použití.

## <a name="grant-application-permissions"></a>Udělení oprávnění aplikacím

V této části udělíte aplikacím oprávnění.

1. V okně **Nastavení** vyberte **Požadovaná oprávnění**.
2. Klikněte na tlačítko **Add** (Přidat).
3. Vyberte **Přidat rozhraní API**, aby se zobrazilo okno **Vyberte rozhraní API**.
4. Vyberte **Microsoft Intune API (MicrosoftIntuneAPI)** a pak v okně **Vyberte rozhraní API** klikněte na **Vybrat**. Je vybraný krok **Vybrat oprávnění** a zobrazené okno **Povolit přístup**.
5. Zvolte možnost **Získat informace o datovém skladu z Microsoft Intune** z části **Oprávnění aplikace**.
6. Klikněte na **Vybrat** v okně **Povolit přístup**.
7. Klikněte na **Hotovo** v okně **Přidat přístup přes rozhraní API**.
8. Klikněte na **Udělit oprávnění** v okně **Požadovaná oprávnění** a klikněte na **Ano**, pokud se zobrazí výzva k aktualizaci stávajících oprávnění, která tato aplikace už má.

## <a name="generate-token"></a>Vygenerování tokenu

Pomocí sady Visual Studio vytvořte projekt Konzolová aplikace (.NET Framework), který podporuje .NET Framework a používá C# jako kódovací jazyk.

1. Vyberte **soubor**  >  **Nový**  >  **projekt** , chcete-li zobrazit dialogové okno **Nový projekt** .
2. Na levé straně vyberte **Visual C#**, aby se zobrazily všechny projekty rozhraní .NET Framework.
3. Vyberte **Konzolová aplikace (.NET Framework)**, přidejte název aplikace a pak kliknutím na **OK** aplikaci vytvořte.
4. V **Průzkumníku řešení** vyberte **Program.cs**, aby se zobrazil kód.
5. V Průzkumník řešení přidejte odkaz na sestavení `System.Configuration` .
6. V místní nabídce vyberte možnost **Přidat**  >  **novou položku**. Zobrazí se dialogové okno **Přidat novou položku**.
7. Na levé straně v části **Visual C#** vyberte **Kód**.
8. Vyberte **Třída**, změňte název třídy na *IntuneDataWarehouseClass.cs* a klikněte na **Přidat**.
9. V rámci metody <code>Main</code> přidejte následující kód:

    ``` csharp
         var applicationId = ConfigurationManager.AppSettings["appId"].ToString();
         SecureString applicationSecret = ConvertToSecureStr(ConfigurationManager.AppSettings["appKey"].ToString()); // Load as SecureString from configuration file or secret store (i.e. Azure KeyVault)
         var tenantDomain = ConfigurationManager.AppSettings["tenantDomain"].ToString();
         var adalContext = new AuthenticationContext($"https://login.windows.net/" + tenantDomain + "/oauth2/token");
    
         AuthenticationResult authResult = adalContext.AcquireTokenAsync(
             resource: "https://api.manage.microsoft.com/",
             clientCredential: new ClientCredential(
                 applicationId,
                 new SecureClientSecret(applicationSecret))).Result;
    ``` 

10. Přidejte další obory názvů přidáním následujícího kódu v horní části souboru kódu:

    ``` csharp
     using System.Security;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     using System.Configuration;
    ``` 

11. Za metodu <code>Main</code> přidejte ke zpracování a převodu klíče aplikace následující privátní metodu:

    ``` csharp
    private static SecureString ConvertToSecureStr(string appkey)
    {
        if (appkey == null)
            throw new ArgumentNullException("AppKey must not be null.");
    
        var secureAppKey = new SecureString();
    
        foreach (char c in appkey)
            secureAppKey.AppendChar(c);
    
        secureAppKey.MakeReadOnly();
        return secureAppKey;
    }
    ```

12. V **Průzkumníku řešení** klikněte pravým tlačítkem myši na **Odkazy** a pak vyberte **Spravovat balíčky NuGet**.
13. Vyhledejte *Microsoft.IdentityModel.Clients.ActiveDirectory* a nainstalujte související balíček Microsoft NuGet.
14. V **Průzkumníku řešení** vyberte a otevřete soubor *App.config*.
15. Přidejte oddíl <code>appSettings</code> tak, aby se kód xml zobrazil následujícím způsobem:

    ``` xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup> 
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
        </startup>
        <appSettings>
          <add key="appId" value="App ID created from 'Create a Web App' procedure"/>
          <add key="appKey" value="Key created from 'Create a key' procedure" />
          <add key="tenantDomain" value="contoso.onmicrosoft.com"/>
        </appSettings>
    </configuration>
    ``` 

16. Aktualizujte hodnoty <code>appId</code>, <code>appKey</code> a <code>tenantDomain</code> tak, aby odpovídaly vašim jedinečným hodnotám souvisejícím s aplikací.
17. Sestavte aplikaci.

    >[!NOTE] 
    > Pokud se chcete podívat na další implementační kód, otevřete si článek s [příkladem kódu Intune-Data-Warehouse](https://github.com/Microsoft/Intune-Data-Warehouse/tree/master/Samples/CSharp ).

## <a name="next-steps"></a>Další kroky
Další informace o Azure Key Vault zjistíte v článku [Co je Azure Key Vault?](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)

