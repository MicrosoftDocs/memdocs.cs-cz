---
title: Získání dat z rozhraní API datového skladu pomocí klienta REST
titleSuffix: Microsoft Intune
description: Toto téma popisuje, jak načíst data z datového skladu Microsoft Intune pomocí rozhraní RESTful API.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: D6D15039-4036-446C-A58F-A5E18175720A
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e036e139e97ce033b3269ba0b8d5cf202fad773
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331767"
---
# <a name="get-data-from-the-intune-data-warehouse-api-with-a-rest-client"></a>Získání dat z rozhraní API datového skladu Intune pomocí klienta REST

Datový model datového skladu Intune můžete zpřístupnit přes koncové body RESTful. Aby váš klient získal přístup k datům, musí se vůči službě Microsoft Azure Active Directory (Azure AD) autorizovat protokolem OAuth 2.0. Přístup umožníte tak, že nejprve nastavíte nativní aplikaci v Azure a udělíte oprávnění rozhraní API Microsoft Intune. Jakmile váš místní klient získá autorizaci, může komunikovat s koncovými body datového skladu přes tuto nativní aplikaci.

Při nastavování klienta, který má získat data z rozhraní API datového skladu, budete muset:

1. Vytvořit klientskou aplikaci jako nativní aplikaci v Azure
3. Udělit této klientské aplikaci přístup k rozhraní API Microsoft Intune
3. Vytvořit místního klienta REST pro získání dat

V následujícím postupu se dozvíte, jak autorizovat rozhraní API a přistupovat k němu pomocí klienta REST. Nejprve se podíváte na používání obecného klienta REST s využitím nástroje Postman. Postman je nástroj často používaný k řešení problémů a vývoji klientů REST pracujících s rozhraními API. Další informace o tomto nástroji najdete na webu [Postman](https://www.getpostman.com). Pak se můžete podívat na ukázku kódu C#. Tento vzorový kód ukazuje příklad autorizace klienta a získání dat z rozhraní API.

## <a name="create-a-client-app-as-a-native-app-in-azure"></a>Vytvořit klientskou aplikaci jako nativní aplikaci v Azure

Vytvořte nativní aplikaci v Azure. Tato nativní aplikace představuje klientskou aplikaci. Klient běžící na místním počítači odkazuje na rozhraní API datového skladu Intune, když si místní klient vyžádá přihlašovací údaje.

1. Přihlaste se k Azure Portalu svého tenanta. Zvolením možnosti **Azure Active Directory** > **Registrace aplikací** otevřete podokno **Registrace aplikací** .
2. Vyberte **Registrace nové aplikace**.
3. Zadejte podrobnosti této aplikace.
    1. Do pole **Název** zadejte nějaký popisný název, například Intune Data Warehouse Client.
    2. Jako **Typ aplikace** vyberte **Nativní**.
    3. Do pole **Přihlašovací adresa URL** zadejte adresu URL. Přihlašovací adresa URL bude záviset na konkrétní situaci, pokud ale hodláte použít nástroj Postman, zadejte `https://www.getpostman.com/oauth2/callback`. Při ověřování vůči službě Azure AD použijete v kroku ověřování klienta zpětné volání.
4. Vyberte **Vytvořit**.

     ![Klientská aplikace datového skladu Intune](./media/reports-proc-data-rest/reports-get_rest_data_client_overview.png)

5. Poznačte si **ID aplikace** této aplikace. Toto ID použijete v další části.

## <a name="grant-the-client-app-access-to-the-microsoft-intune-api"></a>Udělit této klientské aplikaci přístup k rozhraní API Microsoft Intune

Teď máte v Azure definovanou aplikaci. Udělte z této nativní aplikace přístup k rozhraní API Microsoft Intune.

1. Vyberte nativní aplikaci. Aplikaci jste pojmenovali jako **klienta datového skladu Intune**.
2. V podokně **Nastavení** vyberte **Požadovaná oprávnění**.
3. V podokně **Požadovaná oprávnění** vyberte **Přidat**.
4. Vyberte **Výběr rozhraní API**.
5. Vyhledejte název webové aplikace. Její název je **Rozhraní API Microsoft Intune**.
6. Vyberte v seznamu tuto aplikaci.
7. Vyberte **Vybrat**.
8. Zaškrtnutím políčka **Delegovaná oprávnění** přidejte možnost **Získat informace datového skladu z Microsoft Intune**.

    ![Povolení přístupu – rozhraní API Microsot Intune](./media/reports-proc-data-rest/reports-get_rest_data_client_access.png)

9. Vyberte **Vybrat**.
10. Vyberte **Done** (Hotovo).
11. V podokně Požadovaná oprávnění můžete volitelně vybrat **Udělit oprávnění**. Tím udělíte přístup všem účtům v aktuálním adresáři. Zabráníte tím tomu, aby se dialogové okno souhlasu zobrazilo pro každého uživatele v tenantovi. Další informace najdete v článku [Integrace aplikací s Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).
12. Vyberte **Ano**.

## <a name="get-data-from-the-microsoft-intune-api-with-postman"></a>Získání dat z rozhraní API Microsoft Intune pomocí nástroje Postman

S rozhraním API datového skladu Intune můžete pracovat pomocí obecného klienta REST, jako je Postman. Postman dokáže využívat funkce tohoto rozhraní API, podkladový datový model OData a řešit problémy s připojením k prostředkům rozhraní API. V této části najdete informace o vygenerování tokenu OAuth 2.0 pro místního klienta. Klient bude tento token potřebovat k ověření vůči službě Azure AD a přístupu k prostředkům rozhraní API.

### <a name="information-you-will-need-to-make-the-call"></a>Informace, které budete potřebovat k uskutečnění volání

Abyste mohli nástrojem Postman uskutečnit volání REST, budete potřebovat následující informace:

| Atribut        | Popis                                                                                                                                                                          | Příklad                                                                                       |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Adresa URL zpětného volání     | Tento atribut nastavte stejně jako adresu URL zpětného volání na stránce s nastavením aplikace.                                                                                                                              | https://www.getpostman.com/oauth2/callback                                                    |
| Název tokenu       | Řetězec sloužící k předání přihlašovacích údajů aplikaci Azure. Tento proces vám token vygeneruje, takže můžete uskutečnit volání rozhraní API datového skladu.                          | Bearer                                                                                        |
| Ověřovací adresa URL         | Toto je adresa URL sloužící k ověření. | https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com/ |
| Adresa URL přístupového tokenu | Toto je adresa URL sloužící k udělení tokenu.                                                                                                                                              | https://login.microsoftonline.com/common/oauth2/token |
| ID klienta        | Tento atribut jste vytvořili a poznačili si při vytváření nativní aplikace v Azure.                                                                                               | 4184c61a-e324-4f51-83d7-022b6a81b991                                                          |
| Rozsah (nepovinné) | Funkce Blank                                                                                                                                                                               | Toto pole můžete nechat prázdné.                                                                     |
| Typ udělení       | Tento token představuje autorizační kód.                                                                                                                                                  | Autorizační kód                                                                            |

### <a name="odata-endpoint"></a>Koncový bod OData

Potřebujete také koncový bod. K získání koncového bodu datového skladu budete potřebovat adresu URL vlastního kanálu. Koncový bod OData můžete získat v podokně datového skladu.

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. Otevřete podokno **datový sklad Intune** tak, že v části **Další úkoly** na pravé straně okna **Microsoft Intune-přehled** vyberete odkaz datový sklad.
4. V části **Použít služby generování sestav třetích stran** zkopírujte adresu URL vlastního kanálu. Měla by vypadat přibližně takto: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0`

Koncový bod má následující formát:`https://fef.{yourtenant}.manage.microsoft.com/ReportingService/DataWarehouseFEService/{entity}?api-version={verson-number}`

Například entita **dates** vypadá takto: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`

Další informace najdete v tématu [Koncový bod rozhraní API datového skladu Intune](reports-api-url.md).

### <a name="make-the-rest-call"></a>Uskutečnění volání REST

Abyste získali nový přístupový token pro nástroj Postman, musíte přidat autorizační adresu služby Azure AD, ID klienta a tajný klíč klienta. Postman načte autorizační stránku, na kterou zadáte přihlašovací údaje.

#### <a name="add-the-information-used-to-request-the-token"></a>Přidání informací sloužících k vyžádání tokenu

1. Stáhněte si nástroj Postman, pokud ho už nemáte nainstalovaný. Ke stažení tohoto nástroje použijte adresu [www.getpostman](https://www.getpostman.com).
2. Otevřete nástroj Postman. Zvolte operaci HTTP typu **GET**.
3. Vložte do adresy adresu URL koncového bodu. Výsledek by měl vypadat přibližně takto:  

    `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`
4. Zvolte kartu **Authorization** (Autorizace) a v seznamu **Type** (Typ) vyberte **OAuth 2.0**.
5. Vyberte **Get New Access Token** (Získat nový přístupový token).
6. Ověřte, že jste do své aplikace v Azure už přidali adresu URL zpětného volání. Adresa URL zpětného volání je `https://www.getpostman.com/oauth2/callback`.
7. Do pole **Token Name** (Název tokenu) zadejte Bearer.
8. Přidejte **Auth URL** (Ověřovací adresa URL). Výsledek by měl vypadat přibližně takto:  

    `https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com/`
9. Přidejte **Access Token URL** (Adresa URL přístupového tokenu). Výsledek by měl vypadat přibližně takto:  

     `https://login.microsoftonline.com/common/oauth2/token`

10. Přidejte **Client ID** (ID klienta) z nativní aplikace, které jste vytvořili v Azure a pojmenovali jako `Intune Data Warehouse Client`. Výsledek by měl vypadat přibližně takto:  

     `88C8527B-59CB-4679-A9C8-324941748BB4`

11. Vyberte **Authorization Code** (Autorizační kód) a místně si vyžádejte přístupový token.

12. Vyberte **Request Token** (Vyžádat token).

    ![Informace o přístupovém tokenu](./media/reports-proc-data-rest/reports-postman_getnewtoken.png)

13. Na autorizační stránku služby Azure AD zadejte svoje přihlašovací údaje. Seznam tokenů v nástroji Postman teď obsahuje token s názvem `Bearer`.
14. Vyberte **Use Token** (Použít token). Seznam hlaviček obsahuje novou hodnotu klíče pro autorizaci a hodnotu `Bearer <your-authorization-token>`.

#### <a name="send-the-call-to-the-endpoint-using-postman"></a>Odeslání volání koncovému bodu pomocí nástroje Postman

1. Vyberte **Poslat**.
2. V textu odpovědi nástroje Postman se zobrazí návratová data.

    ![Stav klienta pro dodatečnou hodnotu 200 OK](./media/reports-proc-data-rest/reports-postman_200OK.png)

## <a name="create-a-rest-client-c-to-get-data-from-the-intune-data-warehouse"></a>Vytvoření klienta REST (v jazyce C#), který získá data z datového skladu Intune

Následující vzorový kód obsahuje jednoduchého klienta REST. V kódu se používá třída **httpClient** z knihovny .Net. Jakmile klient získá přihlašovací údaje ke službě Azure AD, sestaví volání GET REST, které načte entitu dates z rozhraní API datového skladu.

> [!Note]  
> Následující vzorový kód můžete [zpřístupnit na GitHubu](https://github.com/Microsoft/Intune-Data-Warehouse/blob/master/Samples/CSharp/Program.cs). V tomto úložišti GitHubu najdete jeho nejnovější změny a aktualizace.

1. Otevřete **Microsoft Visual Studio**.
2. Vyberte **soubor** > **Nový projekt**. Rozbalte **Visual C#** a zvolte **Konzolová aplikace (.Net Framework)**.
3. Dejte projektu název `IntuneDataWarehouseSamples`, přejděte do místa, kam chcete projekt uložit, a vyberte **OK**.
4. V Průzkumníkovi řešení klikněte na toto řešení pravým tlačítkem a vyberte **Spravovat balíčky NuGet pro řešení**. Vyberte **Procházet** a pak do vyhledávacího pole zadejte `Microsoft.IdentityModel.Clients.ActiveDirectory`.
5. Zvolte tento balíček, v oblasti Spravovat balíčky pro vaše řešení vyberte projekt **IntuneDataWarehouseSamples** a pak vyberte **Nainstalovat**.
6. Výběrem možnosti **Přijímám** přijměte licenci na tento balíček NuGet.
7. Otevřete `Program.cs` v Průzkumníkovi řešení.

    ![Program.cs a Průzkumník řešení v aplikaci Visual Studio](./media/reports-proc-data-rest/reports-get_rest_data_in.png)

8. Nahraďte kód v *program.cs* následujícím kódem:  

   ```csharp
   namespace IntuneDataWarehouseSamples
   {
   using System;
   using System.Net.Http;
   using System.Net.Http.Headers;
   using Microsoft.IdentityModel.Clients.ActiveDirectory;

   class Program
   {
    static void Main(string[] args)
   {
   /**
   * TODO: Replace the below values with your own.
   * emailAddress - The email address of the user that you will authenticate as.
   *
   * password  - The password for the above email address.
   *    This is inline only for simplicity in this sample. We do not
   *    recommend storing passwords in plaintext.
   *
   * applicationId - The application ID of the native app that was created in AAD.
   *
   * warehouseUrl   - The data warehouse URL for your tenant. This can be found in
   *      the Azure portal.
   *
   * collectionName - The name of the warehouse entity collection you would like to
   *      access.
   */
   var emailAddress = "intuneadmin@yourcompany.com";
   var password = "password_of(intuneadmin@yourcompany.com)";
   var applicationId = "<Application ID>";
   var warehouseUrl = "https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0";
   var collectionName = "dates";

   var adalContext = new AuthenticationContext("https://login.windows.net/common/oauth2/token");
   AuthenticationResult authResult = adalContext.AcquireTokenAsync(
   resource: "https://api.manage.microsoft.com/",
   clientId: applicationId,
   userCredential: new UserPasswordCredential(emailAddress, password)).Result;

   var httpClient = new HttpClient();
   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);

   var uriBuilder = new UriBuilder(warehouseUrl);
   uriBuilder.Path += "/" + collectionName;

   HttpResponseMessage response = httpClient.GetAsync(uriBuilder.Uri).Result;

   Console.Write(response.Content.ReadAsStringAsync().Result);
   Console.ReadKey();
   }
   }
   ```

9. Aktualizujte `TODO` ve vzorovém kódu.
10. Stisknutím kláves **Ctrl+F5** sestavte a spusťte klienta Intune.DataWarehouseAPIClient v režimu ladění.

    ![Entita dates načtená ve formátu JSON](./media/reports-proc-data-rest/reports-get_rest_data_output.png)

11. Prohlédněte si výstup konzoly. Výstup obsahuje data ve formátu JSON přetažená z entity **dates** ve vašem tenantovi Intune.

## <a name="next-steps"></a>Další kroky

Podrobnosti k autorizaci, struktuře adresy URL rozhraní API a koncovým bodům OData najdete v článku [Použití rozhraní API datového skladu Intune](reports-api-url.md).

Datové entity obsažené v tomto rozhraní API jsou rovněž uvedené v datovém modelu datového skladu Intune. Další informace najdete v článku [Datový model rozhraní API datového skladu Intune](reports-ref-data-model.md).
