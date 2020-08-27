---
title: Konfigurace nastavení proxy serveru pro konektor Intune pro Active Directory
description: Popisuje, jak nakonfigurovat konektor Intune pro službu Active Directory tak, aby fungoval se stávajícími místními proxy servery.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c7300c03ce0ba703f423aa420e9e47534ef2968
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908679"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Práce se stávajícími místními proxy servery

Tento článek vysvětluje, jak nakonfigurovat konektor Intune pro službu Active Directory pro práci s odchozími proxy servery. Je určená pro zákazníky se síťovými prostředími, která mají existující proxy servery.

Ve výchozím nastavení se konektor Intune pro službu Active Directory pokusí automaticky najít proxy server v síti pomocí automatického zjišťování (WPAD) webového proxy serveru. Pokud je tato konfigurace ve vaší síti nakonfigurovaná, nemusí se vyžadovat další konfigurace.  Pokud jsou potřebné změny, následující části popisují, jak přepsat výchozí nastavení, a to s využitím [standardních možností .NET Framework pro konfiguraci nastavení proxy serveru](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  Další možnosti jsou popsány v této dokumentaci.

Další informace o tom, jak fungují konektory, najdete v tématu [vysvětlení konektorů Azure proxy aplikací služby AD](/azure/active-directory/manage-apps/application-proxy-connectors).

## <a name="completely-bypass-outbound-proxies"></a>Zcela obejít odchozí proxy

Konektor můžete nakonfigurovat tak, aby vynechal místní proxy server, aby se zajistilo, že používá přímé připojení ke službám Azure. Doporučujeme tento přístup, pokud to vaše zásada sítě umožňuje, protože to znamená, že máte jednu méně konfigurací, kterou je třeba udržovat.

Pokud chcete pro konektor zakázat použití odchozího proxy serveru, upravte soubor: \Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config a přidejte adresu proxy serveru a port proxy serveru do oddílu v této ukázce kódu:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Chcete-li zajistit, že služba Aktualizátor konektorů obejít proxy server, udělejte podobnou změnu v adresáři C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Nezapomeňte vytvořit kopie původních souborů pro případ, že budete potřebovat vrátit se k souboru Default. config.

Po úpravě konfiguračních souborů budete muset službu Intune Connector restartovat. 

1. Otevřete **Services. msc**.
2. Vyhledejte a vyberte **službu Intune ODJConnector**.
3. Vyberte **restartovat**.

![Snímek obrazovky s restartováním služby](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Určení alternativní proxy server

Pokud se pro službu Intune Connector musí u služby Active Directory použít jiný proxy server (například ta, která obchází ověřování), můžete to určit podobným způsobem. Provedete to tak, že upravíte soubor: \Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config a přidáte adresu proxy serveru a port proxy serveru do oddílu zobrazeného v této ukázce kódu:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Chcete-li zajistit, že služba Aktualizátor konektorů obejít proxy server, udělejte podobnou změnu v adresáři C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Nezapomeňte vytvořit kopie původních souborů pro případ, že budete potřebovat vrátit se k souboru Default. config.

Po úpravě konfiguračních souborů budete muset službu Intune Connector restartovat. 

1. Otevřete **Services. msc**.
2. Vyhledejte a vyberte **službu Intune ODJConnector**.
3. Vyberte **restartovat**.

![Snímek obrazovky s restartováním služby](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Další kroky

[správu zařízení](../remote-actions/device-management.md)