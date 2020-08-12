---
title: Povolení sdílení dat
titleSuffix: Configuration Manager
description: Referenční příručka pro sdílení diagnostických dat s desktopovou analýzou
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 40ebeabaaf236377388660a2a1a328e308a708ab
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125937"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Povolení sdílení dat pro desktopovou analýzu

Aby bylo možné zaregistrovat zařízení do Desktop Analytics, musí posílat diagnostická data společnosti Microsoft. Pokud vaše prostředí používá proxy server, použijte tyto informace k tomu, abyste mohli nakonfigurovat proxy server.

## <a name="diagnostic-data-levels"></a>Úrovně diagnostických dat

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagram úrovní diagnostických dat pro desktopovou analýzu":::

Když integrujete Configuration Manager s desktopovou analýzou, použijete ji také ke správě úrovně diagnostiky dat v zařízeních. Pro dosažení co nejlepších výsledků použijte Configuration Manager.

> [!IMPORTANT]
> Ve většině případů se tato nastavení konfigurují jenom pomocí Configuration Manager. Tato nastavení nepoužívejte také v objektech zásad skupiny domén. Další informace najdete v tématu věnovaném [řešení konfliktů](enroll-devices.md#conflict-resolution).

Základní funkce Desktop Analytics funguje na **požadované** [úrovni diagnostických dat](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels). Pokud nenastavíte **volitelnou (omezenou)** úroveň v Configuration Manager, nebudete dostávat následující funkce Desktop Analytics:

- Použití aplikace
- [Další App Insights](compat-assessment.md#additional-insights)
- [Data o stavu nasazení](deploy-prod.md#address-deployment-alerts)
- [Data monitorování stavu](health-status-monitoring.md)

Microsoft doporučuje, abyste povolili **volitelnou (omezená)** úroveň diagnostických dat s desktopovou analýzou, která vám umožní maximalizovat výhody, které z ní získáte.

> [!TIP]
> **Volitelné (omezené)** nastavení v Configuration Manager je stejné nastavení jako **omezit rozšířená diagnostická data na minimum vyžadované zásadami Windows Analytics** dostupnými na zařízeních s Windows 10 verze 1709 a novějšími verzemi.
>
> Zařízení s Windows 10, verze 1703 a starší, Windows 8.1 nebo Windows 7 Toto nastavení zásad nemají. Když nakonfigurujete **volitelné (omezené)** nastavení v Configuration Manager, přejdou tato zařízení na **požadovanou** úroveň.
>
> Nastavení této zásady mají zařízení s Windows 10 verze 1709. Když ale v Configuration Manager nakonfigurujete **volitelné (omezené)** nastavení, tato zařízení se také vrátí na **požadovanou** úroveň.
>
> V Configuration Manager verze 2002 a starší mají nastavení jiné názvy:<!-- 7363467 -->
>
> | Verze 2006 a novější | Verze 2002 a starší |
> |---------|---------|
> | Vyžadováno | Základní |
> | Volitelné (omezené) | Rozšířené (omezené) |
> | – | Rozšířené |
> | Volitelné | Do bloku |
>
> Pokud jste dříve nakonfigurovali všechna zařízení na **vyšší** úrovni při upgradu na verzi 2006, vrátí se k **volitelnému (omezenému)**. Pak budou do Microsoftu posílat méně dat. Tato změna by neměla mít vliv na to, co vidíte v Desktop Analytics.

Další informace o diagnostických datech, která jsou sdílena s Microsoftem, s **volitelnou (omezená)**, najdete v tématu [Rozšířené události a pole diagnostických dat Windows 10](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Microsoft má silné závazky na poskytování nástrojů a prostředků, které vám povedou kontrolu nad vaším soukromím. V důsledku toho, zatímco Desktop Analytics podporuje Windows 8.1 zařízení, Microsoft neshromažďuje diagnostická data Windows ze Windows 8.1 zařízení umístěných v zemích Evropské země (EHP a Švýcarsko).

Další informace najdete v tématu [Ochrana osobních údajů Desktop Analytics](privacy.md).

Následující články jsou také dobrými prostředky pro lepší porozumění úrovní diagnostických dat Windows:

- [Windows 10 a GDPR pro tvůrce rozhodnutí IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> Klienti, kteří jsou nakonfigurováni k odesílání **nepovinných (omezených)** diagnostických dat, budou do cloudu Microsoftu při počátečním úplném prohledávání posílat přibližně 2 MB dat. Denní rozdíl se liší od 250-400 KB za den.
>
> Denní rozdílová kontrola probíhá v 3:00 AM (místní čas zařízení). Některé události jsou odesílány na první dostupný čas v průběhu dne. Tyto časy se nedají konfigurovat.
>
> Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Koncové body

Pokud chcete povolit sdílení dat, nakonfigurujte proxy server tak, aby umožňoval následující internetové koncové body.

> [!IMPORTANT]
> V případě ochrany osobních údajů a integrity dat systém Windows při komunikaci s koncovými body diagnostických dat kontroluje certifikát Microsoft SSL (připnutí certifikátů). Zachycení a kontrola SSL nejsou možné. Pokud chcete použít desktopovou analýzu, vylučte tyto koncové body z kontroly SSL.<!-- BUG 4647542 -->

Od verze 2002, pokud se lokalita Configuration Manager nepovede připojit k požadovaným koncovým bodům pro cloudovou službu, vyvolá kritickou stavovou zprávu ID 11488. Když se nemůže připojit ke službě, stav součásti SMS_SERVICE_CONNECTOR se změní na kritický. Zobrazit podrobný stav v uzlu [Stav součásti](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) konzoly Configuration Manager.<!-- 5566763 -->

> [!NOTE]
> Další informace o rozsahu IP adres společnosti Microsoft najdete v tématu věnovaném [veřejné IP adrese Microsoftu](https://www.microsoft.com/download/details.aspx?id=53602). Tyto adresy se pravidelně aktualizují. Služba nenabízí žádnou členitost, proto by mohla být použita jakákoli IP adresa v těchto rozsahech.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

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
> Přístup k ověřování pomocí uživatelského proxy serveru je nekompatibilní s používáním rozšířené ochrany před internetovými útoky v programu Microsoft Defender. Toto chování je způsobeno tím, že toto ověřování spoléhá na klíč registru **DisableEnterpriseAuthProxy** nastavený na `0` , zatímco ATP programu Microsoft Defender vyžaduje, aby byl nastaven na `1` . Další informace najdete v tématu [Konfigurace nastavení připojení počítače a připojení k Internetu v ochraně ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

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

  - Nakonfigurujte proxy server WinINET v rámci zařízení pomocí následujících nastavení zásad skupiny: **nastavení proxy serveru na počítač (nikoli na uživatele)** (ProxySettingsPerUser = `1` ).

  - Směrované připojení nebo použití překladu síťových adres (NAT)

- Nakonfigurujte proxy servery tak, aby umožňovaly účtům počítačů ve službě Active Directory přístup k koncovým bodům dat diagnostiky. Tato konfigurace vyžaduje, aby proxy servery podporovaly integrované ověřování systému Windows.  
