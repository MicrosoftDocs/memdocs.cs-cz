---
title: Koncové body sítě pro Microsoft Intune
titleSuffix: ''
description: Zkontrolujte koncové body pro Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0206af58be08130e67907bad18d7afa10e236d44
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912402"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Koncové body sítě pro Microsoft Intune  

Tato stránka obsahuje seznam IP adres a nastavení portů potřebných pro nastavení proxy serveru v nasazeních Intune.

V rámci cloudové služby Intune nevyžaduje místní infrastrukturu, jako jsou servery nebo brány.

## <a name="access-for-managed-devices"></a>Přístup pro spravovaná zařízení  

Pokud chcete spravovat zařízení za branami firewall a proxy servery, musíte povolit komunikaci s Intune.

> [!NOTE]
> Informace v části se vztahují také na Microsoft Intune Certificate Connector. Konektor má stejné požadavky na síť jako spravovaná zařízení.

- Proxy server musí podporovat **protokol HTTP (80)** i **https (443)** , protože klienti Intune používají oba protokoly. Information Protection Windows používá port 444.
- U některých úloh (například stažení aktualizací softwaru pro klasického agenta počítače) Intune vyžaduje neověřený proxy server přístup k manage.microsoft.com.

Nastavení proxy server můžete upravit na jednotlivých klientských počítačích. Nastavení Zásady skupiny můžete použít také ke změně nastavení všech klientských počítačů umístěných za zadaným proxy server.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Spravovaná zařízení musí být nakonfigurovaná tak, aby **všichni uživatelé** měli přístup ke službám přes brány firewall.


Následující tabulky obsahují seznam portů a služeb, ke kterým přistupuje klient Intune:

|Domény    |IP adresa      |
|-----------|----------------|
| login.microsoftonline.com <br> *. officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | Další informace: [Office 365 –adresy URL a rozsahy IP adres](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msub05.manage.microsoft.com|23.97.166.52|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|fef.amsua0102.manage.microsoft.com|52.242.211.0|
|fef.amsua0702.manage.microsoft.com|52.232.225.75|
|fef.amsub0502.manage.microsoft.com|40.67.219.144|
|fef.msud01.manage.microsoft.com|20.40.178.139|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>Požadavky na síť pro skripty prostředí PowerShell a aplikace Win32  

Pokud k nasazení skriptů PowerShellu nebo aplikací Win32 používáte Intune, musíte taky udělit přístup k koncovým bodům, ve kterých se aktuálně nachází váš tenant.

|ASU | Název úložiště | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Služba nabízených oznámení Windows (WNS)  

U zařízení s Windows spravovaných pomocí Intune spravovaných pomocí správy mobilních zařízení (MDM) musí akce zařízení a další okamžité aktivity vyžadovat používání služby nabízených oznámení Windows (WNS). Další informace najdete v tématu [Povolení přenosů oznámení systému Windows prostřednictvím podnikových bran firewall](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).  

## <a name="delivery-optimization-port-requirements"></a>Požadavky na port Optimalizace doručení  

### <a name="port-requirements"></a>Požadavky na porty  

Pro přenosy peer-to-peer používá Optimalizace doručení 7680 pro protokol TCP/IP nebo 3544 pro procházení NAT (volitelně Teredo). Pro komunikaci mezi klientem a službou používá protokol HTTP nebo HTTPS přes port 80/443.

### <a name="proxy-requirements"></a>Požadavky na proxy server  

Chcete-li použít optimalizaci doručování, je nutné, abyste povolili požadavky na rozsah bajtů. Další informace najdete v tématu [požadavky na proxy serveru pro web Windows Update](/windows/deployment/update/windows-update-troubleshooting).

### <a name="firewall-requirements"></a>Požadavky na bránu firewall  

Pro podporu optimalizace doručování Povolte následující názvy hostitelů přes bránu firewall.
Pro komunikaci mezi klienty a cloudovou službou Optimalizace doručení:
- \*. do.dsp.mp.microsoft.com

Pro metadata Optimalizace doručení:
- \*. dl.delivery.mp.microsoft.com
- \*. emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Informace o síti pro zařízení Apple  

|Použití|Název hostitele (IP adresa/podsíť)|Protokol|Port|
|-----|--------|------|-------|
|Načítání a zobrazování obsahu ze serverů Apple|itunes.apple.com<br>\*. itunes.apple.com<br>\*. mzstatic.com<br>\*. phobos.apple.com<br> \*. phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Komunikace se servery APNS|# – courier.push.apple.com<br>' # ' je náhodné číslo od 0 do 50.|    TCP     |  5223 a 443  |
|Různé funkce, včetně přístupu k webu, obchodu iTunes, macOS App Storu, iCloud, zasílání zpráv atd. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 nebo 443   |

Další informace najdete v tématu [porty TCP a UDP společnosti Apple používané softwarovými produkty společnosti Apple](https://support.apple.com/HT202944), [informace o připojeních hostitele MacOS, iOS/iPadOS a iTunes serveru iTunes a o procesech na pozadí iTunes](https://support.apple.com/HT201999)a [v případě, že klienti MacOS a iOS/iPadOS nezískávají nabízená oznámení Apple](https://support.apple.com/HT203609).  

## <a name="android-port-information"></a>Informace o portu Android

V závislosti na tom, jak se rozhodnete spravovat zařízení s Androidem, možná budete muset otevřít porty Google Android Enterprise nebo nabízené oznámení Androidu. Další informace o podporovaných metodách správy Androidu najdete v [dokumentaci k registraci Androidu](../enrollment/android-enroll.md). 

> [!NOTE]
> Protože Google Mobile Services není k dispozici v Číně, zařízení v Číně spravovaná službou Intune nemůžou používat funkce, které vyžadují Google Mobile Services. Mezi tyto funkce patří: Google Play Ochrana zařízení, jako je SafetyNet ověřování zařízení, Správa aplikací z Obchod Google Play funkcí Android Enterprise (viz tato [dokumentace k Google](https://support.google.com/work/android/answer/6270910)). Kromě toho Portál společnosti Intune aplikace pro Android používá Google Mobile Services ke komunikaci se službou Microsoft Intune. Vzhledem k tomu, že služba Google Play Services není k dispozici v Číně, můžou některé úlohy vyžadovat dokončení až 8 hodin. Další informace najdete v tomto [článku](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable).

### <a name="google-android-enterprise"></a>Google Android Enterprise 

Google poskytuje dokumentaci k požadovaným síťovým portům a cílovým názvům hostitelů ve svých [Androidech Bluebook Enterprise](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)v části **Brána firewall** v tomto dokumentu. 

### <a name="android-push-notification"></a>Nabízené oznámení Androidu

Intune využívá pro nabízené oznámení Google Firebase Cloud Messaging (FCM) k aktivaci akcí zařízení a vrácení se změnami. To je vyžadováno pro správce zařízení s Androidem i pro Android Enterprise. Informace o požadavcích na FCM sítě najdete v tématu [FCM porty Google a brána firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall).

## <a name="endpoint-analytics"></a>Analýza koncového bodu

Další informace o požadovaných koncových bodech pro službu Endpoint Analytics najdete v tématu [konfigurace proxy serveru Endpoint Analytics](../../analytics/troubleshoot.md#bkmk_endpoints).