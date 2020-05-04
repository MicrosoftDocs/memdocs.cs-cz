---
title: Pracovní postup ověřování v Azure AD
titleSuffix: Configuration Manager
description: Podrobnosti o procesu instalace klienta Configuration Manager v zařízení s Windows 10 s ověřováním Azure Active Directory
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714119"
---
# <a name="azure-ad-authentication-workflow"></a>Pracovní postup ověřování v Azure AD

*Platí pro: Configuration Manager (Current Branch)*

Tento článek je technickou referencí pro Configuration Manager procesu instalace klienta na zařízení s Windows 10, které je připojené k Azure Active Directory (Azure AD). Popisuje proces pracovního postupu pro ověřování zařízení a instalaci klienta.  
 

## <a name="azure-ad-token-request-workflow"></a>Pracovní postup žádosti o tokeny Azure AD

![Diagram pracovního postupu služby Azure AD CCMSetup](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. žádost o token Azure AD

Klient připojený k doméně Azure AD s Windows 10 používá k vyžádání tokenu parametry Azure AD. Do souboru **CCMSetup. log**se zaznamenávají následující záznamy:

- Požádat o token zařízení Azure AD:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Pokud nemůže získat token zařízení, vyžádá si uživatelský token Azure AD:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Klient by měl získat certifikát připojení k síti (WPJ), když se připojí k Azure AD. Pokud se nenalezne certifikát připojení k síti na pracovišti, klient se nepokusí vytvořit požadavek pomocí komunikačního kanálu služby tokenu zabezpečení (CCM_STS). Důvodem je to, že klient nemůže do žádosti přidat token Azure AD. Zařízení obvykle nemá tento certifikát, pokud klient není správně připojený ke službě Azure AD.
>
> Kromě toho, pokud token není platný, brána pro správu cloudu (CMG) nepředává požadavek do interních rolí lokality. Token může být neplatný, pokud není tenant zaregistrován jako cloudová služba pro správu v Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Configuration Manager žádost o token klienta

Jakmile klient obdrží token Azure AD, vyžádá si token Configuration Manager klienta (CCM).

Do souboru **CCMSetup. log** virtuálního počítače CMG se zaprotokolují následující záznamy:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2,1 CMG dostane požadavek

Do **protokolu IIS. log**se zaznamenávají tyto záznamy:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2,2 CMG požadavek přepošle na bod připojení CMG

Do **protokolu CMGService. log**se zaznamenávají tyto záznamy:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2,3 bod připojení CMG – CMG požadavek klienta na požadavek klienta bodu správy

**SMS_CLOUD_PROXYCONNECTOR. log**se přihlásí následující záznamy:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>bod správy 2,4 ověřuje token uživatele v databázi lokality

**CCM_STS. log**se přihlásí následující záznamy:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Požadavek na umístění obsahu

Jakmile klient získá odpověď s tokenem CCM, uloží ho do mezipaměti a použije ho k vyžádání informací o lokalitě a umístění obsahu prostřednictvím CMG. Do souboru **CCMSetup. log**se zaznamenávají následující záznamy:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Instalace klienta

Zařízení stáhne obsah klienta a spustí instalaci.

### <a name="communication-validation"></a>Ověřování komunikace

- CMG ověřuje token klienta prostřednictvím CMG, bodu připojení CMG a žádosti databáze bodu správy.
- Klient ověří certifikát služby CMG nebo certifikát správy.
- PKI pro certifikát služby CMG: klient vyžaduje kořenovou certifikační autoritu (CA) certifikátu CMG v místním úložišti.
- Certifikát služby CMG třetích stran: klienti automaticky ověřují certifikát s jeho kořenovou certifikační autoritou publikovanou na internetu.


## <a name="common-issues"></a>Běžné problémy

- Kořenová certifikační autorita není k dispozici.
- Povolení kontroly CRL: publikování seznamu odvolaných certifikátů na internetu nebo použití možnosti **/NoCRLcheck** v příkazovém řádku
- Nenašel se certifikát WPJ: klient je zaregistrovaný ve službě Azure AD, ale nepřipojený k Azure AD.

Použití/NoCRLCheck je vhodné jenom pro Bootstrap v programu CCMSetup. Aby klienti byli plně funkční, měli byste seznam odvolaných certifikátů publikovat na internetu. Jako alternativní řešení můžete zakázat kontrolu seznamu odvolaných certifikátů v konfiguraci komunikace klienta v lokalitě. V opačném případě po aktualizaci nastavení zabezpečení službou Location klienti přestanou komunikovat se serverem.


## <a name="client-registration"></a>Registrace klienta

![Diagram pracovního postupu registrace Azure AD](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Configuration Manager registraci žádosti klienta

Do **protokolu ClientIDManagerStartup. log**se zaznamenávají tyto záznamy:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Configuration Manager požádat o registraci klienta token Azure AD

Do **protokolu ADALOperationProvider. log**se zaznamenávají tyto záznamy:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>klient 2,1 Configuration Manager je zaregistrován.  

Do **protokolu ClientIDManagerStartup. log**se zaznamenávají tyto záznamy:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Během registrace klienta se ověřování certifikátů spouští vždy. K tomuto procesu dochází i v případě, že k registraci klienta používáte metodu ověřování Azure AD.


### <a name="3-configuration-manager-client-token-request"></a>3. Configuration Manager žádost o token klienta

Jakmile lokalita zaregistruje klienta, klient vyžádá token CCM. Token CCM je zašifrovaný pro účet Local System (S-1-5-18) a ukládá se do mezipaměti po dobu osmi hodin. Po osmi hodinách vyprší platnost tokenu a klient si vyžádá obnovení tokenu.

Do **protokolu ClientIDManagerStartup. log**se zaznamenávají tyto záznamy:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3,1 CMG dostane požadavek

Do **protokolu IIS. log**se zaznamenávají tyto záznamy:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3,2 CMG požadavek přepošle na bod připojení CMG

Do **protokolu CMGService. log**se zaznamenávají tyto záznamy:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3,3 bod připojení CMG – CMG požadavek klienta na požadavek klienta bodu správy

**SMS_CLOUD_PROXYCONNECTOR. log**se přihlásí následující záznamy:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>bod správy 3,4 ověřuje token uživatele v databázi lokality

**CCM_STS. log**se přihlásí následující záznamy:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
