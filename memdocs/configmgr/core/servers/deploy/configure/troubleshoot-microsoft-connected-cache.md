---
title: Řešení potíží s připojenou mezipamětí
titleSuffix: Configuration Manager
description: Technické podrobnosti o mezipaměti připojené k Microsoftu, které vám pomůžou při řešení problémů.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a8c975798c506339a981e8648003387dc1e9838
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878101"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Řešení potíží s propojenou mezipamětí Microsoft v Configuration Manager

Tento článek poskytuje technické podrobnosti o mezipaměti připojené k Microsoftu v Configuration Manager. Použijte ho k řešení potíží, které můžete mít ve vašem prostředí. Další informace o tom, jak funguje a jak ho používat, najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> Počínaje verzí 1910 je tato funkce nyní označována jako **propojená s mezipamětí Microsoft**. Dříve byla známá jako Optimalizace doručení v síťové mezipaměti.

## <a name="verify"></a>Ověřit

Když nainstalujete správně server mezipaměti pro optimalizaci doručení a správně nakonfigurujete klienty, stahují se ze serveru mezipaměti nainstalovaného v distribučním bodě místo z Internetu.

Ověřte toto chování [na klientovi](#bkmk_verify-client) nebo [na serveru](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a>Ověřit u klienta

1. V klientovi se systémem Windows 10 verze 1809 nebo novější si stáhněte obsah spravovaný přes Cloud. Další informace o typech obsahu, který podporuje připojená mezipaměť, najdete v tématu [ověření připojené mezipaměti](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Otevřete PowerShell a spusťte následující příkaz:`Get-DeliveryOptimizationStatus`

Příklad:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Všimněte si, že `BytesFromCacheServer` atribut není nula.

Pokud klient není správně nakonfigurovaný nebo server mezipaměti není nainstalovaný správně, vrátí se klientovi Optimalizace doručení do původního cloudového zdroje. Pak bude mít atribut BytesFromCacheServer hodnotu nula.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a>Ověřit na serveru

Nejprve ověřte, zda jsou správně nakonfigurovány vlastnosti registru: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache` . Například umístění mezipaměti jednotky je `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294` , kde `PrimaryDrivesInput` může být více jednotek, například `C,D,E` .

Dále použijte následující metodu pro simulaci požadavku na stažení klienta na server s povinnými záhlavími.

1. Otevřete 64 okno PowerShellu jako správce.
2. Spusťte následující příkaz a nahraďte název nebo IP adresu vašeho serveru pro `<DoincServer>` :

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

Výstup bude vypadat podobně jako v následujícím příkladu:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Následující atributy označují úspěch:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Soubory protokolů

- Protokol nastavení ARR:`%temp%\arr_setup.log`

- Do protokolu instalace serveru mezipaměti: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` v distribučním bodě a `DistMgr.log` na serveru lokality

- Provozní protokoly služby IIS: ve výchozím nastavení`%SystemDrive%\inetpub\logs\LogFiles`

- Provozovat provozní protokol serveru cache:`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Kromě jiných použití vám tento protokol může pomáhat identifikovat problémy s připojením ke cloudu Microsoftu.

## <a name="setup-error-codes"></a>Kódy chyb instalace

Když Configuration Manager nainstaluje součást připojené mezipaměti do distribučního bodu, v následující tabulce jsou uvedeny možné kódy chyb, které mohou nastat:

| Kód chyby | Popis chyby |
|------------|-------------------|
| 0x00000000 | Úspěch |
| 0x00000BC2 | Úspěch, vyžadováno restartování |
| 0x00000643 | Obecná chyba instalace |
| 0x00D00001 | Nastavení připojené mezipaměti se dá spustit jenom v případě, že je nainstalovaná služba Internetová informační služba (IIS). |
| 0x00D00002 | Nastavení připojené mezipaměti lze spustit pouze v případě, že na serveru existuje výchozí web. |
| 0x00D00003 | Nemůžete nainstalovat připojenou mezipaměť, pokud je už služba Směrování žádostí na aplikace (ARR) nainstalovaná. |
| 0x00D00004 | Nastavení připojené mezipaměti se dá spustit jenom v případě, že se do skriptu install. ps1 nainstalovalo směrování žádostí na aplikace (ARR). |
| 0x00D00005 | Nastavení připojené mezipaměti vyžaduje relaci PowerShellu spuštěnou jako správce. |
| 0x00D00006 | Nastavení připojené mezipaměti se dá spustit jenom z 64 prostředí PowerShellu. |
| 0x00D00007 | Nastavení připojené mezipaměti se dá spustit jenom na Windows serveru. |
| 0x00D00008 | Chyba: počet zadaných jednotek mezipaměti musí odpovídat počtu zadaných procent velikosti jednotky mezipaměti. |
| 0x00D00009 | Chyba: je třeba zadat platné ID uzlu mezipaměti. |
| 0x00D0000A | Chyba: je třeba zadat platnou sadu jednotek mezipaměti. |
| 0x00D0000B | Chyba: musí být zadána platná procentuální sada velikosti jednotky mezipaměti. |
| 0x00D0000C | Chyba: je potřeba zadat platnou procentuální hodnotu velikosti jednotky mezipaměti nebo velikost jednotky mezipaměti v GB. |
| 0x00D0000D | Chyba: není možné zadat platnou hodnotu velikosti jednotky mezipaměti a velikost jednotky mezipaměti v GB. |
| 0x00D0000E | Chyba: počet zadaných jednotek mezipaměti se musí shodovat s počtem velikostí jednotky mezipaměti v GB určených. |
| 0x00D0000F | Chyba: soubor ApplicationHost. config se nepovedlo zálohovat z $AppHostConfig na $AppHostConfigDestinationName |
| 0x00D00010 | Chyba: nepovedlo se zálohovat výchozí webový soubor Web. config z $WebsiteConfigFilePath na $WebConfigDestinationName |
| 0x00D00011 | Chyba: v SetupARRWebFarm. ps1 došlo k výjimce. |
| 0x00D00012 | Chyba: v SetupARRWebFarmRewriteRules. ps1 došlo k výjimce. |
| 0x00D00013 | Chyba: v SetupARRWebFarmProperties. ps1 došlo k výjimce. |
| 0x00D00014 | Chyba: v SetupAllowableServerVariables. ps1 došlo k výjimce. |
| 0x00D00015 | Chyba: v SetupFirewallRules. ps1 došlo k výjimce. |
| 0x00D00016 | Chyba: v SetupAppPoolProperties. ps1 došlo k výjimce. |
| 0x00D00017 | Chyba: v SetupARROutboundRules. ps1 došlo k výjimce. |
| 0x00D00018 | Chyba: v SetupARRDiskCache. ps1 došlo k výjimce. |
| 0x00D00019 | Chyba: v SetupARRProperties. ps1 došlo k výjimce. |
| 0x00D0001A | Chyba: v SetupARRHealthProbes. ps1 došlo k výjimce. |
| 0x00D0001B | Chyba: v VerifyIISSItesStarted. ps1 došlo k výjimce. |
| 0x00D0001C | Chyba: v SetDrivesToHealthy. ps1 došlo k výjimce. |
| 0x00D0001D | Chyba: v VerifyCacheNodeSetup. ps1 došlo k výjimce. |
| 0x00D0001E | Připojenou mezipaměť nejde nainstalovat, pokud výchozí web není na portu 80. |
| 0x00D0001F | Chyba: přidělení jednotky mezipaměti v procentech nemůže překročit 100. |
| 0x00D00020 | Selhání: přidělení jednotky mezipaměti v GB nemůže přesáhnout volné místo na jednotce. |
| 0x00D00021 | Selhání: přidělená jednotka mezipaměti v procentech musí být větší než 0. |
| 0x00D00022 | Chyba: alokace jednotky mezipaměti v GB musí být větší než 0. |
| 0x00D00023 | Chyba: v RegisterScheduledTask_CacheNodeKeepAlive došlo k výjimce. |
| 0x00D00024 | Chyba: v RegisterScheduledTask_Maintenance došlo k výjimce. |
| 0x00D00025 | Chyba: při nastavování pravidel přepisu pro farmu HTTPS došlo k výjimce: $FarmName |
| 0x00D00026 | Chyba: při nastavování pravidel přepisu pro farmu HTTP došlo k výjimce: $FarmName |
| 0x00D00027 | Nejde nainstalovat připojenou mezipaměť, protože se nepovedlo nainstalovat závislý software pro směrování žádostí o aplikace (ARR). Podívejte se na soubor protokolu umístěný v% TEMP% \ arr_setup. log. |

## <a name="iis-configurations"></a>Konfigurace služby IIS

Instalace serveru do mezipaměti provede několik úprav konfigurace služby IIS v distribučním bodě.

### <a name="application-request-routing"></a>Směrování žádostí o aplikace

Server mezipaměti nainstaluje a nakonfiguruje [směrování požadavků aplikace IIS (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing). Aby se předešlo možným konfliktům, nemůže distribuční bod tuto součást již mít nainstalovanou.

### <a name="allowed-server-variables"></a>Povolené proměnné serveru

Po instalaci serveru do mezipaměti má výchozí web následující proměnné *místního* serveru:

- HTTP_HOST
- QUERY_STRING
- X – CCC
- X-CID
- X-DOINC – ODCHOZÍ

### <a name="rewrite-rules"></a>Pravidla přepisu

Server do mezipaměti přidá následující pravidla přepisu:

#### <a name="inbound-rewrite-rules"></a>Příchozí pravidla přepisu

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Odchozí pravidla přepsání

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Správa prostředků serveru

Požadované místo na disku pro každý server mezipaměti se může lišit v závislosti na požadavcích na aktualizace vaší organizace. 100 GB by mělo být dostatek místa pro ukládání následujícího obsahu do mezipaměti:

- Aktualizace funkcí
- Od 2 do tří měsíců z hlediska kvality a aktualizací Office
- Microsoft Intune aplikace a aplikace pro doručenou poštu Windows

Server do mezipaměti by neměl spotřebovat mnoho systémové paměti nebo času procesoru. Pokud si po instalaci serveru do mezipaměti všimnete významné spotřeby prostředků procesu nebo paměti, analyzujte soubory protokolu IIS a ARR.

Pokud soubory protokolu IIS a ARR zabírají příliš mnoho místa na serveru, můžete ke správě souborů protokolu použít několik metod. Další informace najdete v tématu [správa File Storage protokolu IIS](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Viz také

[Mezipaměť propojená Microsoftem v Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
