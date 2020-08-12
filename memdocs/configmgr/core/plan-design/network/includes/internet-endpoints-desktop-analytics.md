---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: ca735cde1da5d563b9a7772fdaa55834e307312e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125936"
---
### <a name="server-connectivity-endpoints"></a>Koncové body připojení serveru

Spojovací bod služby musí komunikovat s následujícími koncovými body:

| Koncový bod  | Funkce  |
|-----------|-----------|
| `https://aka.ms` | Slouží k vyhledání služby. |
| `https://graph.windows.net` | Slouží k automatickému načítání nastavení, jako je CommercialId při připojování hierarchie k Desktop Analytics (na Configuration Manager role serveru). Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Slouží k synchronizaci členství kolekce zařízení, plánů nasazení a stavu připravenosti zařízení s desktopovou analýzou (jenom na Configuration Manager role serveru). Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | Pro diagnostická data z konektoru on-premises Service Connector získáte přehled o stavu služeb připojených ke cloudu.<!--7541816--> |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Uživatelské prostředí a koncové body komponenty diagnostiky

Klientská zařízení musí komunikovat s následujícími koncovými body:

| Koncový bod  | Funkce  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Prostředí připojeného uživatele a koncový bod komponenty diagnostiky. Používá se v zařízeních se systémem Windows 10 verze 1809 nebo novějším nebo verze 1803 s nainstalovanou kumulativní aktualizací 2018-09 nebo novější. |
| `https://v10.events.data.microsoft.com` | Prostředí připojeného uživatele a koncový bod komponenty diagnostiky. Používá se v zařízeních se systémem Windows 10 verze 1803 _bez_ nainstalované kumulativní aktualizace 2018-09. |
| `https://v10.vortex-win.data.microsoft.com` | Prostředí připojeného uživatele a koncový bod komponenty diagnostiky. Používá se v zařízeních se systémem Windows 10 verze 1709 nebo starším. |
| `https://vortex-win.data.microsoft.com` | Prostředí připojeného uživatele a koncový bod komponenty diagnostiky. Používá se zařízeními se systémem Windows 7 a Windows 8.1 |

### <a name="client-connectivity-endpoints"></a>Koncové body připojení klienta

Klientská zařízení musí komunikovat s následujícími koncovými body:

| Index | Koncový bod  | Funkce  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Umožňuje aktualizaci kompatibility odeslat data společnosti Microsoft. |
| 2 | `http://adl.windows.com` | Umožňuje aktualizaci kompatibility získat nejnovější data kompatibility od Microsoftu. |
| 3 | `https://watson.telemetry.microsoft.com` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1803 nebo starší. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se pro sestavy stavu zařízení ve Windows 10 verze 1809 nebo novější. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1809 nebo novější. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1809 nebo novější. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1809 nebo novější. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1809 nebo novější. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1809 nebo novější. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Zasílání zpráv o chybách systému Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1809 nebo novější. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Online Crash Analysis (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Vyžaduje se pro sestavy stavu zařízení ve Windows 10 verze 1809 nebo novější. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Online Crash Analysis (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Vyžaduje se ke sledování stavu nasazení ve Windows 10 verze 1803 nebo starší. |
| 13 | `https://login.live.com` | Je potřeba, abyste poskytovali spolehlivější identitu zařízení pro desktopovou analýzu. <br> <br>Pokud chcete zakázat přístup účet Microsoft koncovým uživatelům, místo blokování tohoto koncového bodu použijte nastavení zásad. Další informace najdete v tématu [účet Microsoft v podniku](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Prostředí připojeného uživatele a koncový bod komponenty diagnostiky. |
