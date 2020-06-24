---
title: Monitorování stavu připojení
titleSuffix: Configuration Manager
description: Podrobnosti o tom, jak monitorovat stav připojení a stavy zařízení pro analýzu stolních počítačů v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: db70eab54f319197f267173fe857d0fb147a7eba
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746557"
---
# <a name="monitor-connection-health"></a>Monitorování stavu připojení

Pomocí řídicího panelu **stavu připojení** v Configuration Manager přejděte k podrobnostem o kategoriích podle stavu zařízení. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte uzel **Údržba Desktop Analytics** a vyberte řídicí panel **stav připojení** .  

[![Snímek obrazovky řídicího panelu stavu připojení Configuration Manager](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

Při první instalaci Desktop Analytics nemusí tyto grafy zobrazovat kompletní data. Může trvat 2-3 dní, než aktivní zařízení pošle diagnostická data službě Desktop Analytics, služba pro zpracování dat a pak se synchronizuje s vaším Configuration Managerm webem.<!-- 4098037 -->

## <a name="connection-details"></a>Podrobnosti připojení

Tato dlaždice zobrazuje následující základní informace o připojení z Configuration Manager k Desktop Analytics:

- **Název tenanta**: název připojení Desktop Analytics v uzlu **služby Azure** .

- **Cílová kolekce**: stejná *cílová kolekce* , kterou jste zadali při připojování Configuration Manager ke službě Desktop Analytics. Tato kolekce zahrnuje všechna zařízení, která Configuration Manager nakonfigurují s nastavením komerčního ID a nastavení diagnostických dat. Je to celá sada zařízení, která Configuration Manager se připojují ke službě Desktop Analytics.

- **Cílová zařízení**: všechna zařízení v cílové kolekci minus následující typy zařízení:

  - Vyřadit
  - Zastaralé
  - Inactive
  - Nespravovaný
  - Zařízení s verzemi LTSC (Long Term Servicing Channel) systému Windows 10
  - Zařízení se systémem Windows Server

    Další informace o těchto stavech zařízení najdete v tématu [informace o stavu klienta](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager nahrávání do Desktop Analytics všechna zařízení v cílové kolekci minus vyřazené z provozu a zastaralé klienty.

- **Zařízení způsobilá pro da**: počet zařízení cílících na zařízení, která mají nenárokovaná na desktopovou analýzu. Například zařízení v cílové kolekci, která používají Windows Server nebo Windows 10 s kanálem pro dlouhodobé obsluhy (LTSC).

## <a name="last-sync-details"></a>Podrobnosti o poslední synchronizaci

Tato dlaždice zobrazuje, když se Configuration Manager synchronizuje s cloudovou službou Desktop Analytics a kolik zařízení se synchronizuje.

- **Synchronizovaná zařízení**: počet oprávněných zařízení, která Configuration Manager odeslána na Desktop Analytics. Tato služba zahrnuje tato zařízení do aktuálně viditelného snímku.

- **Poslední synchronizace služby**: stejná jako čas **Poslední aktualizace** na portálu pro Desktop Analytics.

- **Příští synchronizace služby**: když můžete očekávat příští denní snímek v rámci analýzy stolních počítačů.

> [!Note]  
> Při prvním zápisu zařízení do služby Desktop Analytics může trvat několik dní, než se data nahrávají a zpracují. Během této doby se dlaždice **Poslední synchronizace** může zdát prázdná.
> Kromě toho se žádná z hodnot v této dlaždici automaticky neaktualizuje, když si vyžádáte snímek na vyžádání. Další informace najdete v tématu [latence dat](troubleshooting.md#data-latency).

Pokud si myslíte, že se některá zařízení nezobrazuje v Desktop Analytics, zajistěte, aby byla zařízení podporovaná desktopovou analýzou. Další informace najdete v tématu [předpoklady](overview.md#prerequisites).

## <a name="connection-health"></a>Stav připojení

Graf **stavu připojení** zobrazuje počet zařízení v následujících stavech:  

- [Správně zaregistrované](#properly-enrolled): zařízení se zobrazuje v Desktop Analytics s kompletním inventářem.
- [Nepovedlo se zaregistrovat](#unable-to-enroll): existuje blokující problém, který brání v registraci zařízení.
- [Výstraha konfigurace](#configuration-alert): zařízení se nezobrazí v části Desktop Analytics nebo se zobrazuje s nekompletním inventářem. Configuration Manager taky zjistili problém s registrací zařízení.
- [Čeká](#awaiting-enrollment)se na registraci: Configuration Manager zařízení nakonfigurovalo, ale zatím se nezobrazuje v Desktop Analytics.
- [Stav čeká na vyřízení](#status-pending): Configuration Manager stále konfiguruje toto zařízení, nebo nemá dostatek dat ze zařízení k určení jeho stavu.
- [Chybějící data](#missing-data): Configuration Manager zařízení nakonfigurovalo, ale Analytics pro stolní počítače má pouze částečná data

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Celkový počet zařízení v tomto grafu by měl být stejný jako **zařízení způsobilá pro hodnotu da** na dlaždici podrobnosti připojení.

Výběrem řezu v grafu přejdete k seznamu zařízení s tímto stavem. Další informace najdete v tématu [seznam zařízení](#device-list).

Vyberte název kategorie v legendě, který chcete odebrat nebo přidat z grafu. Tato akce usnadňuje zvětšení grafu, abyste viděli relativní velikosti menších segmentů.

### <a name="properly-enrolled"></a>Správně zaregistrováno

Zařízení má následující atributy:

- Klient Configuration Manager verze 1902 nebo novější  
- Neexistují žádné chyby konfigurace.  
- Nástroj Desktop Analytics přijal v posledních 28 dnech kompletní diagnostická data z tohoto zařízení.  
- Desktop Analytics má úplný inventář konfigurace a nainstalovaných aplikací pro zařízení.  

### <a name="unable-to-enroll"></a>Nejde provést registraci.

Configuration Manager detekuje jeden nebo více blokujících potíží, které brání v registraci zařízení. Další informace najdete v tématu seznam [vlastností zařízení s Desktop Analytics v Configuration Manager](#bkmk_config-issues).  

Například klient Configuration Manager není minimálně verze 1902 (5.0.8790). Aktualizujte klienta na nejnovější verzi. Zvažte možnost Povolit automatický upgrade klienta pro Configuration Manager Web. Další informace najdete v tématu [upgrade klientů](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

> [!TIP]
> Došlo k známému problému s kumulativní aktualizací zabezpečení z dubna 2020 (EVJ) pro Windows 7, která způsobuje, že zařízení tuto chybu nehlásí. Další informace najdete v [poznámkách k verzi](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

Počínaje verzí 2002 můžete snadněji identifikovat problémy s konfigurací klientského proxy serveru ve dvou oblastech:

- **Kontroly připojení koncových bodů**: Pokud klienti nemůžou kontaktovat požadovaný koncový bod, zobrazí se na řídicím panelu upozornění na konfiguraci. Přejděte k podrobnostem o klientech, které se nemohou zaregistrovat, aby se zobrazily koncové body, ke kterým se klienti nemohou připojit kvůli problémům s konfigurací proxy serveru. Další informace najdete v tématu [kontroly připojení koncových bodů](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Stav připojení**: Pokud vaši klienti používají proxy server pro přístup k Desktop Analytics, Configuration Manager zobrazí problémy s ověřováním proxy serveru od klientů. Přechodem k podrobnostem zobrazíte klienty, kteří se nemohou zaregistrovat kvůli problémům s ověřováním proxy serveru. Další informace najdete v tématu [stav připojení](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Upozornění konfigurace

Zařízení se nezobrazí v části Desktop Analytics nebo se zobrazuje s nekompletním inventářem. Configuration Manager taky zjistili problém s registrací zařízení. Další informace najdete v tématu seznam [vlastností zařízení s Desktop Analytics v Configuration Manager](#bkmk_config-issues).

Například zařízení nemá připojení ke službě. Další informace najdete v tématu [připojení ke koncovému bodu diagnostiky Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Čeká se na registraci

Desktop Analytics neobsahuje diagnostická data pro toto zařízení. K tomuto problému může dojít proto, že jste zařízení nedávno přidali do cílové kolekce a ještě neodeslali data. Může to také znamenat, že zařízení nekomunikuje se službou správně a nejnovější diagnostická data jsou starší než 28 dní.

Ujistěte se, že zařízení může komunikovat se službou. Další informace najdete v tématu [koncové body](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Čeká na stav

Configuration Manager stále konfiguruje toto zařízení, nebo nemá dostatek dat ze zařízení k určení jeho stavu.

### <a name="missing-data"></a>Chybějící data

Zařízení se úspěšně nakonfigurovalo, ale funkce Desktop Analytics nemůže vytvořit vyhodnocení kompatibility. Configuration Manager Nemá kompletní datovou sadu pro konfiguraci zařízení (pro sčítání) nebo nainstalované aplikace (inventarizace).

Tento problém je často vyřešen automaticky při opakovaném pokusu o zařízení. Pokud s tím budou dál problémy, ujistěte se, že zařízení může komunikovat se službou. Další informace najdete v tématu [koncové body](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Seznam zařízení

Pokud chcete zobrazit konkrétní seznam zařízení podle stavu, začněte s řídicím panelem **stavu připojení** . Vyberte jeden z segmentů dlaždice **stav připojení** a přejděte k seznamu zařízení v tomto stavu. Toto vlastní zobrazení zařízení zobrazuje ve výchozím nastavení následující sloupce analýzy plochy:

- Konfigurace komerčního ID
- Minimální aktualizace kompatibility
- Výslovný souhlas s diagnostickými daty Windows
- Výslovný souhlas s komerčními daty pro Windows
- Připojení ke koncovému bodu diagnostiky Windows
- Stav připojení (počínaje verzí 2002)
- Kontroly připojení koncových bodů (počínaje verzí 2002)

Tyto sloupce odpovídají klíčovým [předpokladům](overview.md#prerequisites) pro komunikaci zařízení s desktopovou analýzou.

[![Snímek obrazovky nelze zapsat seznam zařízení](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Výběrem zařízení zobrazíte úplný seznam dostupných vlastností v podokně podrobností. Některé z těchto vlastností můžete přidat také jako sloupce do seznamu zařízení.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a>Vlastnosti zařízení

Jako sloupce v seznamu Configuration Manager zařízení jsou k dispozici následující vlastnosti zařízení Analytics Desktop:

- [Kontroly připojení koncových bodů](#endpoint-connectivity-checks) (počínaje verzí 2002)
- [Stav připojení](#connectivity-status) (počínaje verzí 2002)
- [Konfigurace posouzení](#appraiser-configuration)  
- [Minimální aktualizace kompatibility](#minimum-compatibility-update)  
- [Verze posouzení](#appraiser-version)  
- [Poslední úspěšné úplné spuštění posouzení](#last-successful-full-run-of-appraiser)  
- [Shromažďování dat pro vyhodnocení](#appraiser-data-collection)  
- [Poslední úspěšné úplné spuštění sčítání](#last-successful-full-run-of-census)  
- [Shromažďování dat sčítání](#census-data-collection)  
- [Připojení ke koncovému bodu diagnostiky Windows](#windows-diagnostic-endpoint-connectivity)  
- [Kontrolovat diagnostická data pro koncové uživatele](#check-end-user-diagnostic-data)  
- [Ověřit proxy uživatele](#check-user-proxy)  
- [Konfigurace komerčního ID](#commercial-id-configuration)  
- [Výslovný souhlas s komerčními daty pro Windows](#windows-commercial-data-opt-in)  
- [Kontrolovat název zařízení v diagnostických datech](#check-device-name-in-diagnostic-data)  
- [Konfigurace služby DiagTrack](#diagtrack-service-configuration)  
- [Verze DiagTrack](#diagtrack-version)  
- [Načítání ID SQM](#sqm-id-retrieval)  
- [Jedinečné načtení identifikátoru zařízení](#unique-device-identifier-retrieval)  
- [Výslovný souhlas s diagnostickými daty Windows](#windows-diagnostic-data-opt-in)  

**Nejčastější dlaždice pro blokování registrací a výstrahy konfigurace** na řídicím panelu stavu připojení zobrazují vlastnosti, které zařízení nejčastěji hlásí jako problém.

### <a name="endpoint-connectivity-checks"></a>Kontroly připojení koncových bodů

Počínaje verzí 2002,<!-- 4963230 --> aby klienti zjistili problémy s ověřováním proxy serveru, provádějí kontroly připojení k požadovaným koncovým bodům. Pokud klient nemůže získat přístup k požadovanému koncovému bodu, tato vlastnost zobrazí číslovaný seznam koncových bodů, ke kterým se nemůže připojit kvůli problémům s konfigurací proxy serveru. Porovná tento seznam s publikovaným seznamem [požadovaných koncových bodů](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Stav připojení

Počínaje verzí 2002,<!-- 4963383 --> Pokud klienti používají pro přístup k Desktop Analytics proxy server, zobrazí tato vlastnost problémy s ověřováním proxy serveru. Obsahuje následující podrobnosti týkající se ověřování proxy serveru:

- Stavový kód
- Návratový kód

V souboru protokolu se zobrazí chyby podobné následujícímu:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Kde `%s` je adresa URL požadovaného koncového bodu.

Můžete se také podívat na nedeterministické chybové zprávy, které nevyžadují pozornost, dokud nebudou mít zařízení problémy s registrací. Příklad:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Další informace o konfiguraci proxy serverů pro použití s desktopovou analýzou najdete v tématu [ověřování proxy serveru](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Konfigurace posouzení

<!--20,21-->
Posouzení je součást systému Windows, která odpovídá [aktualizacím kompatibility](enroll-devices.md#update-devices). Posuzuje aplikace a ovladače na zařízení kvůli kompatibilitě s nejnovější verzí Windows.

Pokud je tato kontrolu úspěšná, pak je na zařízení správně nakonfigurovaná součást hodnocení.

V opačném případě se může zobrazit jedna z následujících chyb:

- Nejde nakonfigurovat shromažďování dat kompatibility aplikací zařízení (SetRequestAllAppraiserVersions). Podrobnosti o výjimce najdete v protokolech.  

- Nejde nakonfigurovat shromažďování dat kompatibility aplikací zařízení (SetRequestAllAppraiserVersions). Podrobnosti o výjimce najdete v protokolech.  

- Nelze zapsat RequestAllAppraiserVersions do klíče registru `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Appraiser` . Kontrolovat oprávnění  

Ověřte oprávnění pro tento klíč registru. Ujistěte se, že účet Local System má přístup k tomuto klíči, aby bylo možné nastavit klienta Configuration Manager.  

Další informace najdete v části M365AHandler. log v klientovi.  

### <a name="minimum-compatibility-update"></a>Minimální aktualizace kompatibility

<!--18,19,32-->
Aktualizace kompatibility (appraiser.dll) není na zařízení nainstalovaná nebo je neaktuální. Je starší než minimální požadavek na Desktop Analytics, 10.0.17763.

Nainstalujte nejnovější aktualizaci kompatibility. Další informace najdete v tématu [aktualizace kompatibility](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Verze posouzení

Tato vlastnost zobrazuje aktuální verzi komponenty hodnotící aplikace na zařízení. Zobrazuje verzi souboru na `%windir%\System32\appraiser.dll` , bez desetinných míst. Například verze souboru 10.0.17763 se zobrazí jako 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Poslední úspěšné úplné spuštění posouzení

Tato vlastnost zobrazuje datum a čas, kdy zařízení naposledy úspěšně spustilo hodnocení.

### <a name="appraiser-data-collection"></a>Shromažďování dat pro vyhodnocení

<!--Appraiser run status-->
<!--22,33-->
Tato vlastnost zobrazuje poslední výsledek ze systému Windows, ve kterém je spuštěna komponenta posouzení.

Pokud se to nepodaří, může se zobrazit jedna z následujících chyb:

- Nejde shromáždit data o kompatibilitě aplikací (RunAppraiser). Podrobnosti najdete v protokolech.  

- Shromažďování dat o kompatibilitě aplikací (CompatTelRunner.exe) skončilo s kódem chyby.  

Další informace najdete v části M365AHandler. log v klientovi.

Vyhledejte následující soubor: `%windir%\System32\CompatTelRunner.exe` . Pokud neexistuje, přeinstalujte požadované [aktualizace kompatibility](enroll-devices.md#update-devices). Zajistěte, aby tento soubor neodebrala žádná jiná systémová součást, například zásady skupiny nebo antimalwarovou službu.

Pokud soubor M365AHandler. log v klientovi obsahuje jednu z následujících chyb:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Chcete-li tyto chyby vyřešit, spusťte následující příkazy z konzoly Windows PowerShell se zvýšenými oprávněními na ovlivněném klientovi:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Poslední úspěšné úplné spuštění sčítání

Tato vlastnost zobrazuje datum a čas, kdy zařízení naposledy úspěšně spustilo sčítání.

### <a name="census-data-collection"></a>Shromažďování dat sčítání

<!-- Census run status -->
<!--51,52-->
Sčítání je součást systému Windows, která v inventáři zařízení. Tato data inventáře se používají k pochopení zařízení a jeho konfigurace.

Tato vlastnost zobrazuje poslední výsledek ze systému Windows, ve kterém je spuštěná součást sčítání.

Pokud se to nepodaří, může se zobrazit jedna z následujících chyb:

- Nejde shromáždit data o zařízení a jeho konfiguraci (RunCensus). Podrobnosti o výjimce najdete v protokolech.  

- Nástroj pro shromažďování dat zařízení a konfigurace (devicecensus.exe) se nenašel.  

Další informace najdete v části M365AHandler. log v klientovi.

Vyhledejte následující soubor: `%windir%\System32\DeviceCensus.exe` . Pokud neexistuje, přeinstalujte požadované [aktualizace kompatibility](enroll-devices.md#update-devices). Zajistěte, aby tento soubor neodebrala žádná jiná systémová součást, například zásady skupiny nebo antimalwarovou službu.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Připojení ke koncovému bodu diagnostiky Windows

<!--12,15-->
Pokud je tato kontrolu úspěšná, může se zařízení připojit k prostředí připojenému uživateli a koncovému bodu telemetrie (Vortex).

V opačném případě se může zobrazit jedna z následujících chyb:  

- Nejde se připojit k prostředí s připojeným uživatelem a koncovým bodem telemetrie (Vortex). Ověření nastavení sítě nebo proxy serveru  

- Nelze kontrolovat připojení k prostředí připojenému uživateli a koncovému bodu telemetrie (CheckVortexConnectivity). Podrobnosti o výjimce najdete v protokolech.  

Zařízení ověřují připojení pomocí požadavku GET k následujícímu koncovému bodu na základě verze operačního systému:

| Verze operačního systému | Koncový bod |
|------------|----------|
| – Windows 10, verze 1809 nebo novější<br/>– Windows 10, verze 1803 s kumulativní aktualizací 2018-09 nebo novější | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10 verze 1803 *bez* kumulativní aktualizace 2018-09 nebo novější | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, verze 1709 nebo starší | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 nebo Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Ujistěte se, že zařízení může komunikovat se službou. Tato kontrola ověřuje některé, ale ne všechny požadované koncové body. Další informace najdete v tématu [koncové body](enable-data-sharing.md#endpoints).  

Další informace najdete v části M365AHandler. log v klientovi.  

### <a name="check-end-user-diagnostic-data"></a>Kontrolovat diagnostická data pro koncové uživatele

<!--1004-->
Pokud tato kontrolu neproběhne úspěšně, uživatel na zařízení vybral nižší diagnostická data Windows. Může to být také způsobeno konfliktním objektem zásad skupiny. Další informace najdete v tématu [nastavení systému Windows](enroll-devices.md#windows-settings).

V závislosti na vašich obchodních požadavcích můžete zakázat volbu uživatele prostřednictvím zásad skupiny. Použijte nastavení pro **konfiguraci nastavení výslovných přihlášení k telemetrie v uživatelském rozhraní**. Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Ověřit proxy uživatele

<!--30,35-->
Nastavení DisableEnterpriseAuthProxy je ve výchozím nastavení povoleno pro systém Windows 7. Pro Windows 8.1 počítače Configuration Manager nastaví nastavení DisableEnterpriseAuthProxy na hodnotu 0 (není zakázané).

Tato vlastnost může zobrazit následující chyby:

- Je povolený proxy server pro ověřování. Nastavit DisableEnterpriseAuthProxy na 0 v`HKLM:\Software\Policies\Microsoft\Windows\DataCollection`

- Nejde zjistit stav proxy serveru pro ověřování. Podrobnosti o výjimce najdete v protokolech.

Další informace najdete v části M365AHandler. log v klientovi.  

Ověřte oprávnění pro tento klíč registru. Ujistěte se, že účet Local System má přístup k tomuto klíči, aby bylo možné nastavit klienta Configuration Manager. Může to být také způsobeno konfliktním objektem zásad skupiny. Další informace najdete v tématu [nastavení systému Windows](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Konfigurace komerčního ID

<!--9, 11, 53-->
Microsoft používá jedinečné komerční ID k mapování informací ze zařízení do vašeho pracovního prostoru Desktop Analytics. Když integrujete Configuration Manager s desktopovou analýzou, služba se automaticky dotáže na toto ID. Configuration Manager by měl toto ID automaticky použít na klienty, na které jste zacíleni na nastavení analýzy plochy.

Pokud je tato kontrolu úspěšná, zařízení je správně nakonfigurované s komerčním ID.

V opačném případě se může zobrazit jedna z následujících chyb:

- Nelze zapsat CommercialId do klíče registru `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Kontrolovat oprávnění  

- Nelze aktualizovat CommercialId v klíči registru `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Podrobnosti o výjimce najdete v protokolech.  

- Zadejte správnou hodnotu CommercialId na`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Další informace najdete v části M365AHandler. log v klientovi.  

Ověřte oprávnění pro tento klíč registru. Ujistěte se, že účet Local System má přístup k tomuto klíči, aby bylo možné nastavit klienta Configuration Manager. Může to být také způsobeno konfliktním objektem zásad skupiny. Další informace najdete v tématu [nastavení systému Windows](enroll-devices.md#windows-settings).  

Pro zařízení existuje jiné ID. Tento klíč registru se používá v zásadách skupiny. Má přednost před ID poskytnutým Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a>Pokud si chcete zobrazit komerční ID na portálu Desktop Analytics, použijte následující postup:

1. Přejít na portál Desktop Analytics a vyberte **připojené služby** ve skupině globální nastavení.  

2. V podokně **připojené služby** je ve výchozím nastavení vybráno podokno **registrace zařízení** . V podokně zaregistrovat zařízení se v části informace zobrazuje váš kód komerčního ID.  

[![Snímek obrazovky komerčního ID na portálu pro Desktop Analytics](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Pokud nemůžete použít stávající **klíč ID, Získejte** ho jenom vy. Pokud znovu vygenerujete komerční ID, [znovu zaregistrujte svoje zařízení s novým ID](enroll-devices.md#device-enrollment). Tento proces může způsobit ztrátu diagnostických dat během přechodu.  

### <a name="windows-commercial-data-opt-in"></a>Výslovný souhlas s komerčními daty pro Windows

<!--64-->
Tato vlastnost je specifická pro zařízení s Windows 7 nebo Windows 8.1. Spouští podobné testy, jako je například [výslovný souhlas s diagnostickými daty Windows](#windows-diagnostic-data-opt-in), s výjimkou hodnoty CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Kontrolovat název zařízení v diagnostických datech

<!--56,58-->
Pokud je tato kontrolu úspěšná, zařízení je správně nakonfigurované tak, aby sdílelo název zařízení.

V opačném případě se může zobrazit jedna z následujících chyb:

- Nejde ověřit, jestli se má název zařízení odeslat Microsoftu jako součást diagnostických dat Windows. Podrobnosti o výjimce najdete v protokolech.  

- Nejde zapisovat AllowDeviceNameInTelemetry do klíče registru `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` . Kontrolovat oprávnění  

Další informace najdete v části M365AHandler. log v klientovi.  

Ověřte oprávnění pro tento klíč registru. Ujistěte se, že účet Local System má přístup k tomuto klíči, aby bylo možné nastavit klienta Configuration Manager. Může to být také způsobeno konfliktním objektem zásad skupiny. Další informace najdete v tématu [nastavení systému Windows](enroll-devices.md#windows-settings).  

Ujistěte se, že nastavení jiného mechanismu zásad, jako je třeba zásady skupiny, nezakáže.

### <a name="diagtrack-service-configuration"></a>Konfigurace služby DiagTrack

<!--44,45,50-->
Pokud je tato kontrolu úspěšná, komponenta DiagTrack je na zařízení správně nakonfigurovaná. Minimální verze požadovaná desktopovou analýzou je 10010586 (10.0.10586).

V opačném případě se může zobrazit jedna z následujících chyb:

- Součást prostředí připojené uživatele a telemetrie (diagtrack.dll) je zastaralá. Ověřit požadavky  

    > [!TIP]
    > Došlo k známému problému s kumulativní aktualizací zabezpečení z dubna 2020 (EVJ) pro Windows 7, která způsobuje, že zařízení tuto chybu nehlásí. Další informace najdete v [poznámkách k verzi](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

- Nelze najít součást prostředí připojené uživatele a telemetrie (diagtrack.dll). Ověřit požadavky  

- Povolit a spustit službu prostředí a telemetrie připojené uživatele pro odesílání dat společnosti Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Nainstalujte nejnovější aktualizace. Další informace najdete v tématu [aktualizace zařízení](enroll-devices.md#update-devices).

Ujistěte se, že je spuštěná služba **prostředí a prostředí pro připojené uživatele** v zařízení.

### <a name="diagtrack-version"></a>Verze DiagTrack

Tato vlastnost zobrazuje aktuální verzi součásti prostředí připojené uživatele a telemetrie v zařízení. Zobrazuje verzi souboru na `%windir%\System32\diagtrack.dll` , bez desetinných míst. Například verze souboru 10.0.10586 se zobrazí jako 10010586.

### <a name="sqm-id-retrieval"></a>Načítání ID SQM

<!--38-->
Tato vlastnost je primárně určena pro zařízení s Windows 7. Dá se použít v novějších verzích operačního systému jako záložní identifikátor zařízení.

Pokud se to nepodaří, může se zobrazit následující chyba:

- Nejde načíst identifikátor telemetrie staršího zařízení (ID SQM).

Další informace najdete v části M365AHandler. log v klientovi.  

Ujistěte se, že ve vašem prostředí nemáte duplicitní ID. Například pokud byla zařízení nasazena s bitovou kopií operačního systému, která nebyla zobecněna.

### <a name="unique-device-identifier-retrieval"></a>Jedinečné načtení identifikátoru zařízení

<!--54-->
Desktop Analytics používá službu účtu Microsoft pro spolehlivější identitu zařízení.

Ujistěte se, že služba **Pomocník pro přihlášení k účtu Microsoft** není zakázaná. Typ spuštění by měl být **Ruční (aktivační událost spustit)**.

Pokud chcete zakázat přístup účet Microsoft koncovým uživatelům, místo blokování tohoto koncového bodu použijte nastavení zásad. Další informace najdete v tématu [účet Microsoft v podniku](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Výslovný souhlas s diagnostickými daty Windows

<!--8,40,55,62-->
Tato vlastnost kontroluje, jestli je systém Windows správně nakonfigurovaný tak, aby povoloval diagnostická data. Zkontroluje hodnotu AllowTelemetry v následujících klíčích registru:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Ověřte oprávnění u těchto klíčů registru. Ujistěte se, že účet Local System má přístup k těmto klíčům, aby mohl klient Configuration Manager nastavit. Může to být také způsobeno konfliktním objektem zásad skupiny. Další informace najdete v tématu [nastavení systému Windows](enroll-devices.md#windows-settings).  

Další informace najdete v části M365AHandler. log v klientovi.  

## <a name="see-also"></a>Viz také

[Řešení potíží s Desktop Analytics](troubleshooting.md)
