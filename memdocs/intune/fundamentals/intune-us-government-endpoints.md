---
title: Koncové body sítě pro nasazení státní správy USA – Microsoft Intune
titleSuffix: ''
description: Přečtěte si koncové body státní správy USA pro Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 149a1dba78b32f2d59884fbb5b69ed58f4c0fccd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331379"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Koncové body pro státní správu USA pro Microsoft Intune

Tato stránka obsahuje seznam koncových bodů pro státní správu USA potřebných pro nastavení proxy serveru v nasazeních Intune.

Pokud chcete spravovat zařízení za branami firewall a proxy servery, musíte povolit komunikaci s Intune.

- Proxy server musí podporovat **HTTP (80)** i **HTTPS (443)** , protože klienti Intune používají oba protokoly.
- U některých úloh (například stahování aktualizací softwaru) vyžaduje Intune neověřený proxy server přístup k manage.microsoft.com.

Nastavení proxy server můžete upravit na jednotlivých klientských počítačích. Nastavení Zásady skupiny můžete použít také ke změně nastavení všech klientských počítačů umístěných za zadaným proxy server.

Spravovaná zařízení musí být nakonfigurovaná tak, aby **všichni uživatelé** měli přístup ke službám přes brány firewall.

Další informace o automatické registraci Windows 10 a registraci zařízení pro státní správu USA najdete v tématu [Nastavení registrace pro zařízení s Windows](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Následující tabulky obsahují seznam portů a služeb, ke kterým přistupuje klient Intune:

|**Služba**|**IP adresa**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>Zákazník pro státní správu USA určil koncové body:
- Azure Portal: https:\//portal.azure.us/ 
- Office 365: https:\//portal.office365.us/ 
- Portál společnosti Intune: https:\//portal.manage.microsoft.us/ 

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Koncové body partnerských služeb, na kterých závisí Intune:
- Služba AAD Sync: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Proxy adresář: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- Graf AAD: https:\//directory.microsoftazure.us a https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- PRAVIDLA automatického nasazení: https:\//enterpriseregistration.microsoftonline.us

## <a name="windows-push-notification-services"></a>Služba nabízených oznámení Windows
V zařízeních spravovaných pomocí Intune, která spravuje použití správy mobilních zařízení (MDM), se vyžaduje služba Windows Push Notification Services (WNS) pro akce zařízení a další okamžité aktivity. Další informace najdete v tématu [Konfigurace podnikových bran firewall a proxy serverů pro podporu provozu WNS](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config) .

## <a name="apple-device-network-information"></a>Informace o síti pro zařízení Apple

|**Používá se pro**|**Název hostitele (IP adresa/podsíť)**|**Protokol**|**Přístavní**|
|------------|-----------|------------|-----------|
|Načítání a zobrazování obsahu ze serverů Apple|itunes.apple.com<br>\*. itunes.apple.com<br>\*. mzstatic.com<br>\*. phobos.apple.com<br>\*. phobos.itunes-apple.com.akadns.net|HTTP|80|
|Komunikace se servery APNS|#-courier.push.apple.com<br>' # ' je náhodné číslo od 0 do 50.|TCP|5223 a 443|
|Různé funkce, včetně přístupu k Internetu, obchodu iTunes, macOS App Storu, iCloud, zasílání zpráv atd.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 nebo 443|

Více informací najdete v následujících tématech:

- [Porty TCP a UDP používané softwarovými produkty společnosti Apple](https://support.apple.com/HT202944)
- [O připojeních hostitele serveru macOS, iOS/iPadOS a iTunes a procesech na pozadí iTunes](https://support.apple.com/HT201999)
- [Pokud klienti macOS a iOS/iPadOS nezískávají nabízená oznámení Apple](https://support.apple.com/HT203609)

## <a name="next-steps"></a>Další kroky
[Koncové body sítě pro Microsoft Intune](intune-endpoints.md)
