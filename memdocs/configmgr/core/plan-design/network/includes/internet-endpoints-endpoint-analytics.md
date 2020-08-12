---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126447"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Koncové body vyžadované pro Configuration Manager spravovaná zařízení

Configuration Manager spravovaná zařízení odesílají data do Intune prostřednictvím konektoru v roli Configuration Manager a nepotřebují přímý přístup k veřejnému cloudu Microsoftu.

| Koncový bod  | Funkce  |
|-----------|-----------|
| `https://graph.windows.net` | Slouží k automatickému načítání nastavení při připojování hierarchie ke službě Endpoint Analytics v Configuration Manager role serveru. Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Slouží k synchronizaci kolekce zařízení a zařízení s nástrojem Endpoint Analytics pouze v roli serveru Configuration Manager. Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="endpoints-required-for-intune-managed-devices"></a>Koncové body vyžadované pro zařízení spravovaná přes Intune

K registraci zařízení do služby Endpoint Analytics je potřeba odesílat požadovaná funkční data do veřejného cloudu Microsoftu. Služba Endpoint Analytics používá ke shromažďování dat ze zařízení spravovaných přes Intune součást prostředí Windows 10 a prostředí Windows serveru připojené k Windows serveru (DiagTrack). Ujistěte se, že je spuštěná služba **prostředí a prostředí pro připojené uživatele** v zařízení.

| Koncový bod  | Funkce  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Používá se zařízením spravovaným v Intune k odesílání [požadovaných funkčních dat](../../../../../analytics/data-collection.md#bkmk_datacollection) do koncového bodu shromažďování dat Intune. |
