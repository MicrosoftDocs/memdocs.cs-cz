---
title: Koncové body sítě pro čínská nasazení – Microsoft Intune
titleSuffix: ''
description: Zkontrolujte koncové body Číny pro Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd52b34b70b71874a42486cbdc87cd3d7d2f9037
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994238"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Čínské koncové body pro Microsoft Intune

Tato stránka obsahuje seznam koncových bodů Čína potřebných pro nastavení proxy serveru v nasazeních Intune.

Pokud chcete spravovat zařízení za branami firewall a proxy servery, musíte povolit komunikaci s Intune.

- Proxy server musí podporovat **HTTP (80)** i **HTTPS (443)**, protože klienti Intune používají oba protokoly.
- U některých úloh (například stahování aktualizací softwaru) vyžaduje Intune neověřený proxy server přístup k manage.microsoft.com.

Nastavení proxy server můžete upravit na jednotlivých klientských počítačích. Nastavení Zásady skupiny můžete použít také ke změně nastavení všech klientských počítačů umístěných za zadaným proxy server.

Spravovaná zařízení musí být nakonfigurovaná tak, aby **všichni uživatelé** měli přístup ke službám přes brány firewall.

Další informace o automatické registraci Windows 10 a registraci zařízení pro čínské zákazníky najdete v tématu [Nastavení registrace pro zařízení s Windows](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Následující tabulky obsahují seznam portů a služeb, ke kterým přistupuje klient Intune:

|**Koncový bod**|**IP adresa**|
|---------------------|-----------|
|*. manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Zákazníkem určené koncové body v Číně pro Intune
- Azure Portal: https: \/ /Portal.Azure.cn/
- Microsoft 365: https: \/ /Portal.partner.microsoftonline.cn/
- Portál společnosti Intune: https: \/ /Portal.manage.microsoftonline.cn/
- Centrum pro správu Microsoft Endpoint Manageru: https: \/ /Endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>Koncové body partnerské služby

Intune provozovaný společností 21Vianet závisí na následujících koncových bodech služby partnera:
- Služba Azure AD Sync: https: \/ /SyncService.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS: https: \/ /Login.chinacloudapi.cn/
- Azure AD Graph: https: \/ /Graph.chinacloudapi.us
- MS Graph: https: \/ /microsoftgraph.chinacloudapi.cn
- PRAVIDLA automatického nasazení: https: \/ /enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Další kroky
[Další informace o Intune provozovaném společností 21Vianet v Číně](china.md)

