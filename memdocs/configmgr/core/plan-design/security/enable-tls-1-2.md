---
title: Povolení přehledu TLS (Transport Layer Security) 1,2
titleSuffix: Configuration Manager
description: Přehled, jak povolit TLS 1,2 pro Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e1334603bcf60ea3eb8c3d18b73d511570cdc5d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699734"
---
# <a name="how-to-enable-tls-12"></a>Jak povolit TLS 1,2

*Platí pro: Configuration Manager (Current Branch)*

Protokol TLS (Transport Layer Security), jako je například SSL (Secure Sockets Layer) (SSL), je šifrovací protokol určený k zajištění zabezpečení dat při přenosu přes síť. Tyto články popisují kroky potřebné k tomu, aby Configuration Manager zabezpečená komunikace používala protokol TLS 1,2. Tyto články také popisují požadavky na aktualizace pro běžně používané komponenty a odstraňování běžných problémů.

## <a name="enabling-tls-12"></a>Povolení protokolu TLS 1.2

Configuration Manager spoléhá na řadu různých komponent pro zabezpečenou komunikaci. Protokol použitý pro dané připojení závisí na schopnostech relevantních součástí na straně klienta i serveru. Pokud je nějaká součást neaktuální nebo není správně nakonfigurovaná, může komunikace používat starší, méně zabezpečený protokol. Aby bylo možné správně povolit Configuration Manager pro podporu TLS 1,2 pro veškerou zabezpečenou komunikaci, je nutné povolit TLS 1,2 pro všechny požadované součásti. Požadované komponenty závisí na vašem prostředí a Configuration Managerch funkcích, které používáte.

> [!IMPORTANT]
> Tento proces spusťte s klienty, zejména s předchozími verzemi Windows. Než povolíte protokol TLS 1,2 a zakážete starší protokoly na serverech Configuration Manager, ujistěte se, že všichni klienti podporují protokol TLS 1,2. V opačném případě klienti nemůžou komunikovat se servery a můžou být osamocení.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Úlohy pro klienty Configuration Manager, servery lokality a vzdálené systémy lokality

Pokud chcete povolit TLS 1,2 pro součásti, na kterých Configuration Manager závisí na zabezpečené komunikaci, budete muset provést několik úloh na klientech i serverech lokality.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Povolit TLS 1,2 pro klienty Configuration Manager

- [Aktualizace Windows a WinHTTP v systému Windows 8,0, Windows Server 2012 (ne R2) a starší](enable-tls-1-2-client.md#bkmk_winhttp)
- [Ujistěte se, že je protokol TLS 1,2 povolený jako protokol pro zprostředkovatele SChannel na úrovni operačního systému.](enable-tls-1-2-client.md#bkmk_protocol)
- [Aktualizace a konfigurace .NET Framework pro podporu TLS 1,2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Povolit TLS 1,2 pro Configuration Manager servery lokality a systémy vzdálené lokality

- [Ujistěte se, že je protokol TLS 1,2 povolený jako protokol pro zprostředkovatele SChannel na úrovni operačního systému.](enable-tls-1-2-server.md#bkmk_protocol)
- [Aktualizace a konfigurace .NET Framework pro podporu TLS 1,2](enable-tls-1-2-server.md#bkmk_net)
- [Aktualizace SQL Server a SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Aktualizace Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Závislosti funkcí a scénářů

Tato část popisuje závislosti pro konkrétní Configuration Manager funkce a scénáře. Chcete-li určit další kroky, vyhledejte položky, které se vztahují k vašemu prostředí.

|Funkce nebo scénář|Aktualizovat úkoly|
|--- |--- |
|Servery lokality (střední, primární nebo sekundární)| - [Aktualizovat .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> -Ověřit nastavení silné kryptografie|
|Server databáze lokality|[Aktualizace SQL Server a jejích klientských komponent](enable-tls-1-2-server.md#bkmk_sql)|
|Servery sekundární lokality|[Aktualizace SQL Server a jejích klientských komponent](enable-tls-1-2-server.md#bkmk_sql) na odpovídající verzi SQL Express|
|Role systému lokality| - [Aktualizovat .NET Framework](enable-tls-1-2-server.md#bkmk_net) a ověřit nastavení silné kryptografie <br/> - [Aktualizujte SQL Server a její součásti klienta](enable-tls-1-2-server.md#bkmk_sql) v rolích, které to vyžadují, včetně [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Bod služby Reporting services|- [Aktualizace .NET Framework](enable-tls-1-2-server.md#bkmk_net) na serveru lokality, na serverech SQL Reporting Services a na jakémkoli počítači s konzolou<br/> – Restartujte službu SMS_Executive podle potřeby.|
|Bod aktualizace softwaru|[Aktualizace služby WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|Brána pro správu cloudu|[Vynucení protokolu TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Konzola nástroje Configuration Manager| - [Aktualizovat .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> -Ověřit nastavení silné kryptografie|
|Configuration Manager klienta s rolemi systému lokality HTTPS|[Aktualizace Windows pro podporu TLS 1,2 pro komunikaci mezi klientem a serverem pomocí WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Centrum softwaru| - [Aktualizovat .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> -Ověřit nastavení silné kryptografie|
|Klienti se systémem Windows 7| *Než* povolíte protokol TLS 1,2 na všech součástech serveru, [aktualizujte systém Windows tak, aby podporoval TLS 1,2 pro komunikaci mezi klientem a serverem pomocí protokolu WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). Pokud zapnete protokol TLS 1,2 na součástech serveru jako první, můžete starší verze klientů osamocení.|

## <a name="frequently-asked-questions"></a>Nejčastější dotazy

### <a name="why-use-tls-12-with-configuration-manager"></a>Proč používat TLS 1,2 s Configuration Manager?

TLS 1,2 je bezpečnější než u předchozích kryptografických protokolů, jako jsou SSL 2,0, SSL 3,0, TLS 1,0 a TLS 1,1. TLS 1,2 v podstatě udržuje data přenášená přes síť bezpečnější.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Kde Configuration Manager používat šifrovací protokoly jako TLS 1,2?

K dispozici jsou v podstatě pět oblastí, které Configuration Manager používá šifrovací protokoly jako TLS 1,2:

- Komunikace klientů s rolemi serveru lokality založené na službě IIS, je-li role nakonfigurována pro použití protokolu HTTPS. Mezi tyto role patří distribuční body, body aktualizace softwaru a body správy.
- Komunikace s SQL bodem správy, SMS Executive a poskytovatele SMS. Configuration Manager vždy šifruje komunikaci SQL.
- Komunikace mezi serverem lokality WSUS, pokud je služba WSUS nakonfigurovaná na používání protokolu HTTPS.
- Konzola Configuration Manager do služby SQL Reporting Services (SSRS), pokud je služba SSRS nakonfigurovaná tak, aby používala protokol HTTPS.
- Veškerá připojení k internetovým službám. Mezi příklady patří brána pro správu cloudu (CMG), spojovací bod služby a synchronizace metadat aktualizace z Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Co určuje, který šifrovací protokol se používá?

Protokol HTTPS bude vždy vyjednávat nejvyšší verzi protokolu, která je podporována klientem i serverem v zašifrované konverzaci. Po navázání připojení pošle klient zprávu serveru s nejvyšším dostupným protokolem. Pokud server podporuje stejnou verzi, pošle zprávu pomocí této verze. Tato dohodnutá verze je ta, která se používá pro připojení. Pokud server nepodporuje verzi, kterou prezentuje klient, bude serverová zpráva určovat nejvyšší verzi, kterou může použít. Další informace o protokolu TLS handshake najdete v tématu [Vytvoření zabezpečené relace pomocí protokolu TLS](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>Co určuje, kterou verzi protokolu může klient a server použít?

Obecně platí, že následující položky mohou určit, která verze protokolu se používá:

- Aplikace může určit, které konkrétní verze protokolu budou vyjednány.
  - Osvědčeným postupem je vyhýbat se tomu, aby na úrovni aplikace byly závislé verze protokolu specifické pro hardwarové kódování a aby následovala konfigurace definovaná na úrovni protokolu součásti a operačního systému.
  - Configuration Manager tímto osvědčeným postupem.
- Pro aplikace napsané pomocí .NET Framework jsou výchozí verze protokolů závislé na verzi rozhraní .NET Framework, na které byly zkompilovány.  
  - Verze .NET před 4.6.3 nezahrnovaly TLS 1,1 a 1,2 v seznamu protokolů pro vyjednávání ve výchozím nastavení.
- Aplikace, které používají protokol WinHTTP pro komunikaci pomocí protokolu HTTPS, jako je například klient Configuration Manager, závisí na verzi operačního systému, na úrovni oprav a konfiguraci pro podporu verze protokolu.


## <a name="additional-resources"></a>Další zdroje

- [Technické informace o kryptografických ovládacích prvcích](cryptographic-controls-technical-reference.md)
- [Osvědčené postupy TLS (Transport Layer Security) s .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: podpora TLS 1,2 pro Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Další kroky

- [Povolení protokolu TLS 1.2 na klientech](enable-tls-1-2-client.md)
- [Povolit TLS 1,2 na serverech lokality](enable-tls-1-2-server.md)