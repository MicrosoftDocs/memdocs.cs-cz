---
title: Povolení sdílení dat
titleSuffix: Configuration Manager
description: Referenční příručka pro sdílení diagnostických dat s desktopovou analýzou
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7610b0e60f3ea02918c9dd98858a3b2bfd7c712
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723632"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Povolení sdílení dat pro desktopovou analýzu

Aby bylo možné zaregistrovat zařízení do Desktop Analytics, musí posílat diagnostická data společnosti Microsoft. Pokud vaše prostředí používá proxy server, použijte tyto informace k tomu, abyste mohli nakonfigurovat proxy server.

## <a name="diagnostic-data-levels"></a>Úrovně diagnostických dat

![Diagram úrovní diagnostických dat pro desktopovou analýzu](media/diagnostic-data-levels.png)

Když integrujete Configuration Manager s desktopovou analýzou, použijete ji také ke správě úrovně diagnostiky dat v zařízeních. Pro dosažení co nejlepších výsledků použijte Configuration Manager.

> [!Important]  
> Ve většině případů se tato nastavení konfigurují jenom pomocí Configuration Manager. Tato nastavení nepoužívejte také v objektech zásad skupiny domén. Další informace najdete v tématu věnovaném [řešení konfliktů](enroll-devices.md#conflict-resolution).

Základní funkce Desktop Analytics funguje na **základní** [úrovni diagnostických dat](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels). Pokud nenastavíte **rozšířenou (omezenou)** úroveň v Configuration Manager, nebudete dostávat následující funkce Desktop Analytics:

- Použití aplikace
- [Další App Insights](compat-assessment.md#additional-insights)
- Data o stavu nasazení
- Data monitorování stavu

Microsoft doporučuje, abyste povolili **vylepšenou (omezená)** úroveň diagnostických dat s desktopovou analýzou, která vám umožní maximalizovat výhody, které z ní získáte.

> [!Tip]
> **Rozšířené (omezené)** nastavení v Configuration Manager je stejné nastavení jako **omezit rozšířená diagnostická data na minimum vyžadované zásadami Windows Analytics** dostupnými na zařízeních s Windows 10 verze 1709 a novějšími verzemi.
>
> Zařízení s Windows 10, verze 1703 a starší, Windows 8.1 nebo Windows 7 Toto nastavení zásad nemají. Když nakonfigurujete **Rozšířené (omezené)** nastavení v Configuration Manager, tato zařízení se vrátí zpět na úroveň **Basic** .
>
> Nastavení této zásady mají zařízení s Windows 10 verze 1709. Pokud však nakonfigurujete **Rozšířené (omezené)** nastavení v Configuration Manager, tato zařízení se také vrátí zpět na úroveň **Basic** .

Další informace o diagnostických datech, která jsou sdílena s Microsoftem s **rozšířeným (omezeným)**, najdete v tématu [Rozšířené události a pole diagnostických dat Windows 10](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]
> Microsoft má silné závazky na poskytování nástrojů a prostředků, které vám povedou kontrolu nad vaším soukromím. V důsledku toho, zatímco Desktop Analytics podporuje Windows 8.1 zařízení, Microsoft neshromažďuje diagnostická data Windows ze Windows 8.1 zařízení umístěných v zemích Evropské země (EHP a Švýcarsko).

Další informace najdete v tématu [Ochrana osobních údajů Desktop Analytics](privacy.md).

Následující články jsou také dobrými prostředky pro lepší porozumění úrovní diagnostických dat Windows:

- [Windows 10 a GDPR pro tvůrce rozhodnutí IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Klienti s nakonfigurovaným omezením rozšířených diagnostických dat odesílají do cloudu Microsoftu přibližně 2 MB dat při počátečním úplném prohledávání. Denní rozdíl se liší od 250-400 KB za den.
>
> Denní rozdílová kontrola probíhá v 3:00 AM (místní čas zařízení). Některé události jsou odesílány na první dostupný čas v průběhu dne. Tyto časy se nedají konfigurovat.
>
> Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Koncové body

Pokud chcete povolit sdílení dat, nakonfigurujte proxy server tak, aby umožňoval následující internetové koncové body.

> [!Important]  
> V případě ochrany osobních údajů a integrity dat systém Windows při komunikaci s koncovými body diagnostických dat kontroluje certifikát Microsoft SSL (připnutí certifikátů). Zachycení a kontrola SSL nejsou možné. Pokud chcete použít desktopovou analýzu, vylučte tyto koncové body z kontroly SSL.<!-- BUG 4647542 -->

Od verze 2002, pokud se lokalita Configuration Manager nepovede připojit k požadovaným koncovým bodům pro cloudovou službu, vyvolá kritickou stavovou zprávu ID 11488. Když se nemůže připojit ke službě, stav součásti SMS_SERVICE_CONNECTOR se změní na kritický. Zobrazit podrobný stav v uzlu [Stav součásti](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) konzoly Configuration Manager.<!-- 5566763 -->

### <a name="server-connectivity-endpoints"></a>Koncové body připojení serveru

Spojovací bod služby musí komunikovat s následujícími koncovými body:

| Koncový bod  | Funkce  |
|-----------|-----------|
| `https://aka.ms` | Slouží k vyhledání služby. |
| `https://graph.windows.net` | Slouží k automatickému načítání nastavení, jako je CommercialId při připojování hierarchie k Desktop Analytics (na Configuration Manager role serveru). Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Slouží k synchronizaci členství kolekce zařízení, plánů nasazení a stavu připravenosti zařízení s desktopovou analýzou (jenom na Configuration Manager role serveru). Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

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

## <a name="proxy-server-authentication"></a>Ověřování proxy serveru

Pokud vaše organizace používá proxy server ověřování pro přístup k Internetu, ujistěte se, že neblokuje diagnostická data z důvodu ověřování. Pokud váš proxy nepovoluje, aby zařízení odesílala tato data, nebudou se zobrazovat v Desktop Analytics.

### <a name="bypass-recommended"></a>Nepoužívat (doporučeno)

Nakonfigurujte proxy servery tak, aby nevyžadovaly ověřování proxy serveru pro provoz do koncových bodů diagnostických dat. Tato možnost je nejkomplexnější řešení. Funguje pro všechny verze Windows 10.  

### <a name="user-proxy-authentication"></a>Ověřování proxy uživatelů

Nakonfigurovat zařízení tak, aby používala kontext přihlášeného uživatele pro ověřování proxy serveru. Tato metoda vyžaduje následující konfigurace:

- U zařízení je aktuální aktualizace kvality podporovaná pro podporovanou verzi Windows.

- Nakonfigurujte proxy na úrovni uživatele (proxy WinINET) v **nastavení proxy serveru** v síťové & internetovou skupinu nastavení Windows. Můžete použít také starší ovládací panel Možnosti Internetu.

- Ujistěte se, že uživatelé mají oprávnění k přístupu k koncovým bodům diagnostických dat. Tato možnost vyžaduje, aby zařízení měla uživatele konzoly s oprávněními proxy serveru, takže tuto metodu nemůžete použít u zařízení bez periferních zařízení.

> [!IMPORTANT]
> Přístup k ověřování pomocí uživatelského proxy serveru je nekompatibilní s používáním rozšířené ochrany před internetovými útoky v programu Microsoft Defender. Toto chování je způsobeno tím, že toto **DisableEnterpriseAuthProxy** ověřování spoléhá na klíč registru `0`DisableEnterpriseAuthProxy nastavený na, zatímco ATP programu Microsoft Defender vyžaduje, `1`aby byl nastaven na. Další informace najdete v tématu [Konfigurace nastavení připojení počítače a připojení k Internetu v ochraně ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Ověřování proxy zařízení

Tento přístup podporuje následující scénáře:

- Zařízení bez přihlášení, pokud se k Internetu přihlašuje nebo uživatelé zařízení nemají přístup k Internetu

- Ověřené proxy servery, které nepoužívají integrované ověřování systému Windows

- Pokud používáte také rozšířenou ochranu před internetovými útoky v programu Microsoft Defender

Tento přístup je nejsložitější, protože vyžaduje následující konfigurace:

- Ujistěte se, že zařízení mají přístup k proxy server prostřednictvím služby WinHTTP v kontextu místního systému. Pro konfiguraci tohoto chování použijte jednu z následujících možností:

  - Příkazový řádek`netsh winhttp set proxy`

  - Protokol WPAD (Web Proxy Auto-Discovery)

  - Transparentní proxy server

  - Nakonfigurujte proxy server WinINET v rámci zařízení pomocí následujících nastavení zásad skupiny: **nastavení proxy serveru na počítač (nikoli na uživatele)** (ProxySettingsPerUser = `1`).

  - Směrované připojení nebo použití překladu síťových adres (NAT)

- Nakonfigurujte proxy servery tak, aby umožňovaly účtům počítačů ve službě Active Directory přístup k koncovým bodům dat diagnostiky. Tato konfigurace vyžaduje, aby proxy servery podporovaly integrované ověřování systému Windows.  
