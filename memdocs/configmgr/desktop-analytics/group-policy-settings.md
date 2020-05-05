---
title: Nastavení zásad skupiny
titleSuffix: Configuration Manager
description: Seznamte se s místními a skupinovými nastaveními zásad skupiny ve Windows používaných Configuration Manager a Desktop Analytics.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0224d9faecb9ff17afc2af3a57ba222023b5a3d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718893"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Nastavení zásad skupiny pro desktopovou analýzu

*Platí pro: Configuration Manager (Current Branch)*

Tento článek podrobně popisuje místní a nastavení zásad skupiny ve Windows, které Configuration Manager a Desktop Analytics používá.

Když Configuration Manager zaregistruje zařízení do Desktop Analytics, nastaví zásady Windows pro konfiguraci zařízení. Ve většině případů se tato nastavení konfigurují jenom pomocí Configuration Manager.

## <a name="windows-settings"></a>Nastavení Windows

Configuration Manager nastavuje zásady systému Windows v jednom nebo obou následujících klíčích registru:

- Objekt zásad skupiny (**GPO**):`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Preference **místních** zásad:`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Zásada | Cesta | Platí pro | Hodnota |
|--------|------|------------|-------|
| **CommercialId** | Local | Všechny verze systému Windows | Aby se zařízení zobrazilo v Desktop Analytics, nakonfigurujte ho pomocí komerčního ID vaší organizace. |
| **AllowTelemetry**  | GPO | Windows 10 | Nastaveno `1` pro **základní**, `2` **Rozšířené**nebo `3` pro **Úplná** diagnostická data. Desktop Analytics vyžaduje aspoň základní diagnostická data. Microsoft doporučuje použití rozšířené (omezené) úrovně s desktopovou analýzou. Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10 verze 1803 a novější | Toto nastavení platí pouze v případě, že je `2`nastavení AllowTelemetry. Omezuje rozšířené události diagnostických dat odeslané společnosti Microsoft jenom na takové události, které potřebuje Desktop Analytics. Další informace najdete v tématu [události diagnostických dat Windows 10 a pole shromážděná prostřednictvím omezení rozšířených diagnostických dat](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10 verze 1803 a novější | Povolit zařízením odesílat název zařízení. Ve výchozím nastavení se název zařízení neposílá společnosti Microsoft. Pokud název zařízení neodešlete, zobrazí se v nástroji Desktop Analytics jako "Neznámý". Další informace najdete v tématu [název zařízení](enroll-devices.md#device-name). |
| **CommercialDataOptIn** | Local | Windows 8.1 a starší | Desktop Analytics vyžaduje hodnotu `1`. Další informace najdete v tématu věnovaném [obchodním údajům v systému Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Obojí | Windows 8.1 a starší | `1` Pro správné fungování shromažďování dat potřebuje aplikace Desktop Analytics hodnotu. |
| **DisableEnterpriseAuthProxy** | GPO | Všechny verze systému Windows | Pokud vaše prostředí vyžaduje uživatelem ověřený proxy server s integrovaným ověřováním Windows pro přístup k Internetu, potřebuje Desktop Analytics hodnotu `0` pro správné fungování shromažďování dat. Další informace najdete v tématu [ověřování proxy serveru](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> Ve většině případů se tato nastavení konfigurují jenom pomocí Configuration Manager. Tato nastavení nepoužívejte také v objektech zásad skupiny domén. Další informace najdete v tématu věnovaném [řešení konfliktů](enroll-devices.md#conflict-resolution).

### <a name="settings-from-upgrade-readiness"></a>Nastavení z Upgrade Readiness

Windows Analytics taky prostřednictvím skriptu Upgrade Readiness nastavit tyto zásady:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

Pokud jste spustili skript Upgrade Readiness připojování na zařízení, tato nastavení zásad můžou pořád existovat. Nepoužívejte starší verzi skriptu. Před registrací zařízení do nástroje Desktop Analytics odeberte tato předchozí nastavení zásad.

## <a name="group-policy-settings"></a>Nastavení zásad skupiny

Obecně platí, že pomocí kolekce Configuration Manager můžete cílit na nastavení a registraci Desktop Analytics. Použijte přímé členství nebo dotazy pro zahrnutí nebo vyloučení zařízení z kolekce. Další informace najdete v tématu [vytváření kolekcí](../core/clients/manage/collections/create-collections.md).

Configuration Manager konfiguruje nastavení komerčního ID a diagnostických dat v cílové kolekci. Pokud potřebujete nakonfigurovat různá nastavení diagnostických dat pro různé skupiny zařízení, přepište nastavení Configuration Manager pomocí nastavení zásad skupiny. Například potřebujete nastavit **rozšířenou (omezená)** úroveň pro některá zařízení a **Basic** pro jiné. Některá zařízení můžou mít různá nastavení [ověřování proxy server](enable-data-sharing.md#proxy-server-authentication) .

Příslušné nastavení zásad skupiny najdete v následujících umístěních: **Konfigurace** > **šablony pro správu** > kolekce dat**součásti** > systému Windows**a buildy Preview**.

Nastavení zásad skupiny upravují pouze nastavení registru v následujícím klíči:`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Když použijete nastavení zásad skupiny k povolení složitých scénářů, věnujte zvláštní pozornost nastavení zásad, která můžou způsobit konflikty konfigurace. Configuration Manager nakonfiguruje [nastavení systému Windows](#windows-settings) pouze *v případě, že hodnota ještě neexistuje*. Nastavení zásad skupiny mají přednost před nastaveními Configuration Manager, takže některé konfigurace zásad skupiny můžou způsobovat problémy s desktopovou analýzou.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Nastavení zásad skupiny, která by mohla být v konfliktu s nastavením Configuration Manager pro desktopovou analýzu

Nastavení zásad skupiny v následující tabulce má největší potenciál v konfliktu s nastavením Windows, které Configuration Manager sady na zařízeních, která se zapisují do Desktop Analytics:

| Zobrazované jméno | Hodnota registru | Vliv na zařízení zaregistrovaná v Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Konfigurace komerčního ID** | CommercialId | Pokud nastavíte tuto zásadu na jinou hodnotu, přepíše komerční ID nastavené Configuration Manager. Pokud se nejedná o stejné ID, nakonfigurované zařízení se nemusí zobrazit v Desktop Analytics. |
| **Povolení telemetrie** | AllowTelemetry | Pokud nastavíte tuto zásadu na jinou hodnotu, přepíše globální úroveň diagnostických dat, kterou jste nastavili v Configuration Manager pro cílovou kolekci. |
| **Omezit rozšířená diagnostická data na minimum vyžadované službou Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | Tato zásada je závislá na předchozím nastavení AllowTelemetry. V závislosti na úrovni, kterou jste nastavili v Configuration Manager nebo se zásadami skupiny, může tato zásada změnit úroveň diagnostických dat v zařízení na hodnotu **Rozšířené** nebo **Rozšířené (s omezením)**. Tato zásada platí jenom v případě, že je `2` AllowTelemetry nastavené na (**Rozšířené**). |
| **Povolí odeslání názvu zařízení v diagnostických datech Windows.** | AllowDeviceNameInTelemetry | Pokud se přihlásíte k odesílání názvů zařízení v Configuration Manager, můžete ji přepsat b konfigurací této zásady na zakázáno. Když toto nastavení zakážete, v části Desktop Analytics se názvy zařízení zobrazí jako neznámé. Další informace najdete v tématu [název zařízení](enroll-devices.md#device-name). |
| **Konfigurace použití ověřeného proxy serveru pro prostředí a službu telemetrie připojené uživatele** | DisableEnterpriseAuthProxy | Pokud nakonfigurujete Configuration Manager zařízení na používání uživatelem ověřeného proxy`0`serveru (), pokud pak tuto zásadu nakonfigurujete tak, aby`1`se **zakázalo použití ověřeného serveru proxy** (), odešle zařízení diagnostická data v kontextu systému místo kontextu uživatele. Pokud zařízení nekonfigurujete na proxy serveru v kontextu systému nebo pokud se zařízení nedokáže ověřit na proxy serveru, Windows nemůže odeslat diagnostická data do nástroje Desktop Analytics. |

> [!NOTE]
> Starší zásady **konfigurující prostředí a telemetrii připojené uživatele** (TelemetryProxy) umožňují systému Windows přeposílání diagnostických dat na vyhrazené proxy místo pomocí proxy uživatele (WinInet) nebo zařízení (WinHTTP). Některé součásti systému Windows tyto zásady nepodporují. Pokud použijete tuto zásadu, může to způsobit problémy s kvalitou dat v Desktop Analytics.

#### <a name="behavior-of-disabled-settings"></a>Chování zakázaných nastavení

Pokud tato nastavení zásad skupiny nakonfigurujete na **zakázáno**, má jiné účinky na chování systému.

- Když zásady **CommercialId** zakážete, Windows odebere hodnotu registru. Nastavení Configuration Manager pro komerční ID, které je nastaveno v cestě registru místních zásad, se pak vztahuje na zařízení.

- Pokud v případě zásad, které Configuration Manager sady ve stejném umístění registru jako zásady skupiny, zakážete nastavení v zásadách skupiny, systém Windows hodnotu registru odstraní. Configuration Manager se znovu nastaví na příští cyklus zpracování zásad a pak ho Windows odebere při další aktualizaci zásad skupiny. Tato konstantní změna v konfiguraci může způsobit nežádoucí chování s desktopovou analýzou.

  - Pokud tato nastavení zásad skupiny nastavíte na **není nakonfigurované**, systém Windows tuto hodnotu jednou odebere, ale nepokračuje v jejím odebrání. Tato konfigurace umožňuje Configuration Manager použít hodnoty podle očekávání.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Nastavení zásad skupiny pro přizpůsobení prostředí pro uživatele

Tato nastavení zásad skupiny nevyžadují Configuration Manager nebo Desktop Analytics. Můžete je nakonfigurovat v zásadách skupiny a nakonfigurovat tak možnosti uživatelů pomocí diagnostických dat Windows.

| Zobrazované jméno | Hodnota registru | Vliv na zařízení zaregistrovaná v Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Konfigurovat oznámení o změnách pro telemetrii** | DisableTelemetryOptInChangeNotification | Počínaje verzí 1803 Windows 10 upozorní uživatele, když se změní úroveň diagnostických dat. Pomocí této zásady můžete zakázat oznámení. |
| **Konfigurovat nastavení výslovných přihlášení k telemetrie v uživatelském rozhraní** | DisableTelemetryOptInSettingsUx | Při konfiguraci úrovně diagnostiky dat nastavíte horní hranici zařízení. Od verze 1803 Windows 10 můžou uživatelé nastavit nižší úroveň. Pomocí této zásady můžete uživatelům zabránit ve změně úrovně diagnostiky. Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Zakázat odstraňování diagnostických dat** | DisableDeviceDelete | Počínaje systémem Windows 10 verze 1809 mohou uživatelé odstranit diagnostická data ze stránky nastavení **zpětné vazby & diagnostiky** . Pomocí této zásady můžete zabránit odstranění diagnostických dat, která Microsoft shromažďuje ze zařízení. |
| **Zakázat prohlížeč diagnostických dat** | DisableDiagnosticDataViewer | Počínaje systémem Windows 10 verze 1809 mohou uživatelé povolit a otevřít prohlížeč diagnostických dat ze stránky nastavení **zpětné vazby pro diagnostiku &** . Pomocí této zásady můžete zakázat prohlížeč diagnostických dat v nastavení Windows a zabránit tomu, aby se zobrazila diagnostická data, která Microsoft shromažďuje ze zařízení.|
