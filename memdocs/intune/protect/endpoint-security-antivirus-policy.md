---
title: Správa nastavení antivirové ochrany pomocí zásad zabezpečení koncových bodů v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady a používejte sestavy pro zařízení, která spravujete pomocí zásad ochrany koncových bodů zabezpečení Endpoint v Microsoft Endpoint Manageru.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 2460a132711fb19d12f33bbada23756fc2344cca
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194242"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Zásady antivirové ochrany pro zabezpečení koncového bodu v Intune

Zásady ochrany koncových bodů zabezpečení služby Intune můžou správcům zabezpečení Zaměřte se na správu diskrétní skupiny nastavení antivirové ochrany pro spravovaná zařízení. Pokud chcete používat zásady antivirové ochrany, Integrujte Intune s rozšířenou ochranou před internetovými útoky v programu Microsoft Defender (Microsoft Defender) jako řešením ochrany před mobilními hrozbami

Zásady antivirové ochrany obsahují několik profilů. Každý profil obsahuje jenom nastavení, která jsou relevantní pro antivirovou ochranu v programu Microsoft Defender ATP pro macOS, Windows 10 nebo pro uživatelské prostředí v aplikaci Windows Security na zařízeních s Windows 10.

Zásady antivirové ochrany najdete v části **Správa** v uzlu zabezpečení koncového bodu v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Zásady antivirové ochrany obsahují stejná nastavení, která se nacházejí v zásadách *ochrany koncových bodů* nebo v profilech *omezení zařízení* pro zásady [Konfigurace zařízení](../configuration/device-profile-create.md) a jsou podobná nastavení zásad [dodržování předpisů zařízením](../protect/device-compliance-get-started.md) . Tyto typy zásad však obsahují další kategorie nastavení, která nesouvisí s antivirovým programem. Další nastavení může zkomplikovat úlohu konfigurace antivirové ochrany. Kromě toho nastavení nalezená v zásadách antivirové ochrany pro macOS nejsou k dispozici prostřednictvím ostatních typů zásad. MacOS antivirový profil nahrazuje nutnost konfigurace nastavení pomocí `.plist` souborů.

## <a name="prerequisites-for-antivirus-policy"></a>Předpoklady pro zásady antivirové ochrany

**Obecné**:

- **macOS**
  - Libovolná podporovaná verze macOS
  - Aby mohla Intune spravovat nastavení antivirové ochrany na zařízení, musí být na tomto zařízení nainstalovaná ochrana ATP programu Microsoft Defender. Si. [Microsoft Defender ATP pro MacOS](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (v dokumentaci ke službě Microsoft Defender ATP)

- **Windows 10 a novější**
  - Nevyžadují se žádné další požadavky.

**Podpora pro klienty Configuration Manager** (*Preview*)

*Tento scénář je ve verzi Preview a vyžaduje použití Configuration Manager aktuální větve verze 2006 nebo novější*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Nastavení připojení tenanta pro zařízení Configuration Manager** – pro podporu nasazení zásad antivirové ochrany do zařízení spravovaných pomocí Configuration Manager nakonfigurujte *připojení tenanta*. Nastavení připojení tenanta zahrnuje konfiguraci Configuration Manager kolekcí zařízení pro podporu zásad zabezpečení koncového bodu služby Intune.

  Pokud chcete nastavit připojení tenanta, přečtěte si téma [Konfigurace připojení tenanta pro podporu zásad Endpoint Protection](../protect/tenant-attach-intune.md).

## <a name="antivirus-profiles"></a>Profily antivirové ochrany

### <a name="devices-managed-by-intune"></a>Zařízení spravovaná přes Intune

Pro zařízení, která spravujete pomocí Intune, jsou podporovány následující profily:

**macOS**:

- Platforma: **MacOS**

  - Profil: **Antivirus** – Správa [nastavení zásad antivirové ochrany](../protect/antivirus-microsoft-defender-settings-macos.md) pro MacOS.

    Pokud používáte [Microsoft Defender ATP pro Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), můžete nakonfigurovat a nasadit nastavení antivirového programu do spravovaných zařízení MacOS prostřednictvím Intune namísto konfigurace těchto nastavení pomocí `.plist` souborů.

**Windows 10**:

- Platforma: **profily Windows 10**

  - Profil: **antivirová ochrana v programu Microsoft Defender** – Správa [nastavení zásad antivirové ochrany](../protect/antivirus-microsoft-defender-settings-windows.md) pro Windows 10

    Antivirová ochrana je součástí nové generace ochrany v programu Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). Ochrana nové generace přináší společně technologie, jako je Machine Learning a cloudová infrastruktura, k ochraně zařízení ve vaší podnikové organizaci.

    *Antivirový profil Microsoft Defenderu* je samostatná instance nastavení antivirové ochrany, která se nachází v *profilu omezení zařízení* pro zásady konfigurace zařízení.
  
    Na rozdíl od nastavení antivirového programu v *profilu omezení zařízení*můžete použít tato nastavení u zařízení, která jsou společně spravovaná. Chcete-li použít tato nastavení, musí být [posuvník úlohy spolusprávy](/configmgr/comanage/how-to-switch-workloads) pro Endpoint Protection nastaven na Intune.

  - Profil: **vyloučení antivirové ochrany v programu Microsoft Defender** – umožňuje spravovat nastavení zásad jenom pro [vyloučení antivirové ochrany](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    Pomocí této zásady můžete spravovat nastavení pro následující poskytovatele kryptografických služeb Microsoft Defenderu (CSP), kteří definují vyloučení antivirové ochrany:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Tito zprostředkovatelé cloudu pro vyloučení antivirové ochrany se spravují taky pomocí zásad *antivirové ochrany v Microsoft Defenderu* , která zahrnuje identická nastavení pro vyloučení. Nastavení z obou typů zásad (*antivirová* a *vyloučení antivirové ochrany*) se vztahují na [sloučení zásad](#policy-merge-for-settings)a vytvářejí množinu vyloučení pro platná zařízení a uživatele.

  - Profil: **Možnosti zabezpečení systému Windows**– Správa [nastavení aplikace zabezpečení systému Windows](../protect/antivirus-security-experience-windows-settings.md) , která koncoví uživatelé mohou zobrazit v centru zabezpečení v programu Microsoft Defender a v oznámeních, která obdrží.

    Aplikace zabezpečení systému Windows je používána řadou funkcí zabezpečení systému Windows k poskytování oznámení o stavu a zabezpečení počítače. Oznámení aplikací pro zabezpečení zahrnují brány firewall, antivirové produkty, filtr SmartScreen v programu Windows Defender a další.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Zařízení spravovaná pomocí Configuration Manager *(ve verzi Preview)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Sloučení zásad pro nastavení

Některá nastavení zásad antivirové ochrany podporují *sloučení zásad*. Sloučení zásad pomáhá předcházet konfliktům při použití více zásad pro stejná zařízení a konfiguraci stejného nastavení. Intune vyhodnocuje nastavení, které sloučení zásad podporuje, a pro každého uživatele nebo zařízení, které se provádí ze všech platných zásad. Tato nastavení se pak sloučí do jedné nadmnožiny zásad.

Můžete například vytvořit tři samostatné zásady antivirové ochrany, které definují různé výjimky pro antivirová umístění souborů. Ke stejnému uživateli se nakonec přiřazují všechny tři zásady. Vzhledem k tomu, že zprostředkovatel vyloučení souborů v programu Microsoft Defender podporuje sloučení zásad, Intune vyhodnocuje a kombinuje vyloučení souborů ze všech platných zásad pro uživatele. Vyloučení se přidají do nadmnožiny a do zařízení uživatelů se doručí jeden seznam vyloučení.

Pokud není pro nastavení podporováno sloučení zásad, může dojít ke konfliktu. Konflikty můžou vést k tomu, že uživatel nebo zařízení neobdrží žádné zásady pro toto nastavení. Například sloučení zásad nepodporuje zprostředkovatele CSP, aby se zabránilo instalaci vyhovujících ID zařízení (*PreventInstallationOfMatchingDeviceIDs*). Konfigurace pro tohoto zprostředkovatele CSP se nesloučí a zpracovávají se samostatně.

Při samostatném zpracování jsou konflikty zásad vyřešeny takto:

1. Zásady se vztahují na nejbezpečnější.
2. Pokud jsou dvě zásady stejně bezpečné, platí poslední upravená zásada.
3. Pokud poslední upravená zásada nedokáže konflikt vyřešit, do zařízení se doručí žádná zásada.

### <a name="settings-and-csps-that-support-policy-merge"></a>Nastavení a zprostředkovatelé CSP podporující sloučení zásad

Sloučení zásad podporuje následující nastavení:

[Zásady antivirové ochrany v programu Microsoft Defender](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Procesy Defenderu k vyloučení** – CSP: [Defender/ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Přípony souborů, které se mají vyloučit z kontrol a ochrany v reálném čase** – CSP: [Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Soubory a složky Defenderu k vyloučení** – CSP: [Defender/ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Sestavy zásad antivirové ochrany

V sestavách zásad antivirové ochrany se zobrazí podrobnosti o stavu vašich zásad zabezpečení koncového bodu a stavu zařízení. Tyto sestavy jsou k dispozici v uzlu zabezpečení koncového bodu v centru pro správu služby Microsoft Endpoint Manager.

Pokud si chcete zobrazit sestavy, v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), navštivte Endpoint Security a vyberte **antivirová ochrana**. Výběrem antivirového programu otevřete stránku Shrnutí. Další zobrazení sestav a stavů jsou k dispozici jako další stránky.

### <a name="summary"></a>Souhrn

Na stránce **Souhrn** můžete [vytvořit nové zásady](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) a zobrazit seznam dříve vytvořených zásad. Seznam obsahuje podrobné informace o profilu, který zásada zahrnuje (typ zásady), a informace o tom, jestli je zásada přiřazená.

![Stránka souhrnu zásad antivirové ochrany](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Když v seznamu vyberete zásadu, otevře se stránka *Přehled* této instance zásad a zobrazí se další informace. Po výběru dlaždice z tohoto zobrazení Intune zobrazí další podrobnosti pro tento profil, pokud jsou k dispozici.

![Stránka s přehledem zásad antivirové ochrany](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Koncové body Windows 10 nejsou v pořádku

Na stránce **koncové body ve Windows 10 nesprávného stavu** můžete zobrazit informace o stavu antivirového programu zařízení s Windows 10 spravovaných MDM. Tyto informace se vrátí z antivirové ochrany v programu Windows Defender, která běží na zařízení jako *Stav agenta hrozeb*.

V tomto zobrazení se zobrazí pouze zařízení se zjištěnými problémy. Toto zobrazení nezobrazuje podrobnosti o zařízeních, která jsou označena jako čistá.

![Stránka nestavové koncové body zásady antivirové ochrany](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)