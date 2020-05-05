---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720538"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Určení verze rozhraní .NET

Nejprve určete nainstalované verze rozhraní .NET. Další informace najdete v tématu [jak určit, jaké verze a úrovně aktualizace Service Pack jsou nainstalovány v Microsoft .NET Framework](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Nainstalovat aktualizace .NET

Nainstalujte aktualizace .NET, abyste mohli povolit silné šifrování. Některé verze .NET Framework mohou vyžadovat aktualizace pro povolení silné kryptografie. Použijte tyto pokyny:

- NET Framework 4.6.2 a novější podporuje TLS 1,1 a TLS 1,2. Potvrďte nastavení registru, ale nevyžadují se žádné další změny.

- Aktualizujte rozhraní .NET Framework 4,6 a starší verze na podporu TLS 1,1 a TLS 1,2. Další informace najdete v tématu [.NET Framework verze a závislosti](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Pokud používáte .NET Framework 4.5.1 nebo 4.5.2 v Windows 8.1 nebo Windows Serveru 2012, jsou relevantní aktualizace a podrobnosti dostupné taky z [webu Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Konfigurace pro silné šifrování

Nakonfigurujte .NET Framework pro podporu silné kryptografie. Nastavte nastavení `SchUseStrongCrypto` registru na `DWORD:00000001`. Tato hodnota zakáže šifru datového proudu RC4 a vyžaduje restart. Další informace o tomto nastavení najdete v článku [Microsoft Security advisor 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Nezapomeňte nastavit následující klíče registru v jakémkoli počítači, který komunikuje v síti pomocí systému s povoleným protokolem TLS 1,2. Například Configuration Manager klienti, role vzdálených systémů lokality nejsou nainstalovány na serveru lokality a samotného serveru lokality.

Pro 32 aplikací, které běží na 32 OSs a pro 64-bitové aplikace, které běží 64 na 16bitové službě OSs, aktualizujte následující hodnoty podklíče:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Pro 32 aplikací, které běží na 64 OSs, aktualizujte následující hodnoty podklíče:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto` Nastavení umožňuje rozhraní .NET používat TLS 1,1 a TLS 1,2. `SystemDefaultTlsVersions` Nastavení umožňuje technologii .NET používat konfiguraci operačního systému. Další informace najdete v tématu [osvědčené postupy TLS s .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).
