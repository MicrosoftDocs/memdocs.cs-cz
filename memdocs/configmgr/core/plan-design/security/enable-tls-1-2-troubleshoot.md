---
title: Běžné problémy při povolování TLS (Transport Layer Security) 1,2
titleSuffix: Configuration Manager
description: Popisuje běžné problémy při povolování TLS (Transport Layer Security) 1,2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 316387bc42ed51dd9b581a25208091ed93cad1d1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699751"
---
# <a name="common-issues-when-enabling-tls-12"></a>Běžné problémy při povolování protokolu TLS 1.2

Tento článek poskytuje rady pro běžné problémy, ke kterým dochází, když v Configuration Manager povolíte podporu TLS 1,2.

## <a name="unsupported-platforms"></a>Nepodporované platformy

Následující klientské platformy jsou podporovány nástrojem Configuration Manager, ale nejsou podporovány v prostředí TLS 1,2:

- Windows CE
- Apple OS X
- Zařízení s Windows 10 spravovaná pomocí místní správy MDM

## <a name="reports-dont-show-in-the-console"></a>Sestavy se nezobrazují v konzole nástroje.

Pokud se sestavy nezobrazují v konzole Configuration Manager, nezapomeňte aktualizovat počítač, na kterém spouštíte konzolu. [Aktualizujte .NET Framework](enable-tls-1-2-client.md#bkmk_net)a povolte silné šifrování.

## <a name="fips-security-policy-enabled"></a>Zásada zabezpečení FIPS povolena

Pokud u klienta nebo serveru povolíte nastavení zásad zabezpečení FIPS, může vyjednávání zabezpečeného kanálu (Schannel) způsobit, že budou používat protokol TLS 1,0. K tomuto chování dochází i v případě, že protokol zakážete v registru.

K prozkoumání, povolení protokolování událostí zabezpečeného kanálu a následné kontrole událostí Schannel v systémovém protokolu. Další informace najdete v tématu [jak omezit použití určitých kryptografických algoritmů a protokolů v Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>SQL Server Chyba komunikace

Pokud SQL Server komunikace selže a vrátí chybu **SslSecurityError** , ověřte následující nastavení:

- [Aktualizace .NET Framework](enable-tls-1-2-server.md#bkmk_net)a povolení silné kryptografie na každém počítači
- [Aktualizace SQL Server](enable-tls-1-2-server.md#bkmk_sql) na hostitelském serveru
- [Aktualizujte součásti klienta SQL](enable-tls-1-2-server.md#bkmk_sql-client) ve všech systémech, které komunikují s SQL. Například servery lokality, poskytovatel serveru SMS a servery role lokality.

## <a name="configuration-manager-client-communication-failures"></a>Configuration Manager selhání komunikace klienta

Pokud klient Configuration Manager nekomunikuje s rolemi lokality, ověřte, zda je [systém Windows aktualizován](enable-tls-1-2-client.md#bkmk_winhttp) tak, aby PODPOROVAL protokol TLS 1,2 pro komunikaci klienta se serverem pomocí protokolu WinHTTP. Mezi běžné role lokality patří distribuční body, body správy a body migrace stavu.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Bod služby Reporting Services selhává a vrátí očekávanou chybu

Pokud bod služby Reporting Services nekonfiguruje sestavy, vyhledejte následující položku chyby v **protokolu soubor Srsrp. log** :

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Pokud chcete tento problém vyřešit, postupujte následovně:

1. [Aktualizujte .NET Framework](enable-tls-1-2-client.md#bkmk_net)a povolte silnou kryptografii na všech relevantních počítačích.

1. Po instalaci aktualizací restartujte službu SMS_Executive.

## <a name="application-catalog-doesnt-initialize"></a>Katalog aplikací se neinicializuje

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Pokud se katalog aplikací neinicializuje, v souboru **ServicePortalWebSite. svclog** vyhledejte následující položku chyby:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Pokud chcete tento problém vyřešit, postupujte následovně:

1. [Aktualizujte .NET Framework](enable-tls-1-2-client.md#bkmk_net)a povolte silnou kryptografii na všech relevantních počítačích.

1. Ve `%WinDir%\System32\InetSrv` složce serveru Application Catalog vytvořte **W2SP.exe.config** soubor s následujícím obsahem:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Tento soubor je výchozím souborem, který se vytvoří, pokud byla aplikace sestavená pomocí .NET Framework 4.6.3.

1. Pro role katalogu aplikací použijte zabezpečení přenosu HTTPS.

    > [!Important]
    > Pokud používáte zabezpečení zpráv protokolu HTTP pro role katalogu aplikací, je WCF pevně zakódováno, aby používalo pouze SSL 3,0 a TLS 1,0. To brání použití TLS 1,2.

1. Pokud jste provedli nějaké změny, restartujte počítač.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Centrum softwaru nebo prohlížeč nekomunikuje s katalogem aplikací.

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Nejlepším způsobem, jak zajistit fungování centra softwaru pro aplikace dostupné pro uživatele v lokalitě s povoleným protokolem TLS 1,2, odeberte roli katalogu aplikací. Pak umožněte centru softwaru komunikovat přímo s bodem správy. Další informace najdete v tématu [Odebrání katalogu aplikací](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Pokud potřebujete vyřešit selhání komunikace mezi katalogem aplikací a centrem softwaru, ověřte následující podmínky:

- [Aktualizujte .NET Framework](enable-tls-1-2-client.md#bkmk_net)a povolte na každém počítači silný kryptografii.

- Po provedení změn restartujte všechny ovlivněné počítače.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Selhání nahrávání spojovacího bodu služby

Pokud spojovací bod služby neodesílá data do SCCMConnectedService, [aktualizujte .NET Framework](enable-tls-1-2-server.md#bkmk_net)a povolte na každém počítači silný kryptografii. Po provedení změn nezapomeňte restartovat počítače.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager konzoly se zobrazí dialogové okno Intune pro registraci.

Pokud se v dialogovém okně připojování k Intune zobrazí, když se konzola pokusí připojit k portálu Intune, [aktualizujte .NET Framework](enable-tls-1-2-client.md#bkmk_net)a povolte na každém počítači silný kryptografii. Po provedení změn nezapomeňte restartovat počítače.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>V konzole Configuration Manager se zobrazí chyba přihlášení k Azure

Pokud se pokusíte vytvořit aplikace v Azure Active Directory (Azure AD), pokud se v dialogovém okně zprovoznění služeb Azure okamžitě po výběru **Přihlásit**, [aktualizujte .NET Framework](enable-tls-1-2-server.md#bkmk_net)a povolíte silnou kryptografii. Po provedení změn nezapomeňte restartovat počítače.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager Cloud Services a TLS 1,2

Virtuální počítače Azure používané bránou pro správu cloudu a distribučními body cloudu podporují protokol TLS 1,2. Podporované verze klientů automaticky používají protokol TLS 1,2.

**SMSAdminui. log** může obsahovat chybu podobnou následujícímu příkladu:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

V systémových protokolech událostí může být SChannel ID události 36874 zaznamenán s následujícím popisem: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Další zdroje

- [Osvědčené postupy TLS (Transport Layer Security) s .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: podpora TLS 1,2 pro Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Technické informace o kryptografických ovládacích prvcích](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Další kroky

- [Povolení protokolu TLS 1.2 na klientech](enable-tls-1-2-client.md)
- [Povolit TLS 1,2 na serverech lokality a vzdálených systémech lokality](enable-tls-1-2-server.md)