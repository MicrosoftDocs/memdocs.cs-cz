---
title: Správa nastavení antivirové ochrany pomocí zásad zabezpečení koncových bodů v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady a používejte sestavy pro zařízení, která spravujete pomocí zásad ochrany koncových bodů zabezpečení Endpoint v Microsoft Endpoint Manageru.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431381"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Zásady antivirové ochrany pro zabezpečení koncového bodu v Intune

Zásady ochrany koncových bodů zabezpečení koncového bodu Intune můžou správcům zabezpečení Zaměřte se na správu diskrétní skupiny nastavení antivirové ochrany pro spravovaná zařízení. Pokud chcete používat zásady antivirové ochrany, Integrujte Intune s pokročilou ochranou před internetovými útoky v programu Microsoft Defender jako řešení ochrany před mobilními hrozbami.

Zásady antivirové ochrany obsahují několik profilů. Každý profil obsahuje jenom nastavení, která jsou relevantní pro antivirovou ochranu v programu Defender pro macOS, Windows 10 nebo pro uživatelské prostředí v aplikaci Windows Security na zařízeních s Windows 10.

Zásady antivirové ochrany najdete v části **Správa** v uzlu zabezpečení koncového bodu v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Zásady antivirové ochrany obsahují stejná nastavení, která najdete v části *Endpoint Protection* nebo profily *omezení zařízení* pro zásady [Konfigurace zařízení](../configuration/device-profile-create.md) a jsou podobná nastavení zásad [dodržování předpisů zařízením](../protect/device-compliance-get-started.md) . Tyto typy zásad však obsahují další kategorie nastavení, která nesouvisí s antivirovým programem. Další nastavení může zkomplikovat úlohu konfigurace antivirové ochrany. Kromě toho nastavení nalezená v zásadách antivirové ochrany pro macOS nejsou k dispozici prostřednictvím ostatních typů zásad. MacOS antivirový profil nahrazuje nutnost konfigurace nastavení pomocí `.plist` souborů.

## <a name="prerequisites-for-antivirus-policy"></a>Předpoklady pro zásady antivirové ochrany

- **macOS**
  - Libovolná podporovaná verze macOS
  - Aby mohla Intune spravovat nastavení antivirové ochrany na zařízení, musí být na tomto zařízení nainstalovaná ATP. Si. [ATP – ATP pro MacOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (v dokumentaci k programu Defender ATP)

- **Windows 10 a novější**
  - Aby mohla Intune spravovat nastavení antivirové ochrany na zařízení, musí být na tomto zařízení nainstalovaná ATP. Viz téma [Microsoft Defender ATP pro Windows](../protect/advanced-threat-protection.md)v dokumentaci k Intune.
  - Aplikace zabezpečení systému Windows je nainstalovaná na všech zařízeních, na kterých běží Window 10, a nevyžaduje žádné další požadavky.

## <a name="antivirus-profiles"></a>Profily antivirové ochrany

**MacOS profily**:

- **Antivirová ochrana** – umožňuje spravovat [nastavení zásad antivirové ochrany](../protect/antivirus-microsoft-defender-settings-macos.md) pro MacOS.

  Pokud používáte [Microsoft Defender ATP pro Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), můžete nakonfigurovat a nasadit nastavení antivirového programu do spravovaných zařízení MacOS prostřednictvím Intune namísto konfigurace těchto nastavení pomocí `.plist` souborů.

**Profily Windows 10**:

- **Antivirová ochrana v programu Microsoft Defender** – Správa [nastavení zásad antivirové ochrany](../protect/antivirus-microsoft-defender-settings-windows.md) pro Windows 10

  Antivirová ochrana je součástí nové generace ochrany v programu Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). Ochrana nové generace přináší dohromady strojové učení, analýzu velkých objemů dat, hloubkové zkoumání rezistence proti hrozbám a cloudovou infrastrukturu k ochraně zařízení ve vaší podnikové organizaci.

  *Antivirový profil Microsoft Defenderu* je samostatná instance nastavení antivirové ochrany, která se nachází v *profilu omezení zařízení* pro zásady konfigurace zařízení.
  
  Na rozdíl od nastavení antivirového programu v *profilu omezení zařízení*můžete použít tato nastavení u zařízení, která jsou společně spravovaná. Chcete-li použít tato nastavení, musí být [posuvník úlohy spolusprávy](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) pro Endpoint Protection nastaven na Intune.

- **Prostředí zabezpečení systému Windows** – spravujte [nastavení aplikace zabezpečení systému Windows](../protect/antivirus-security-experience-windows-settings.md) , která koncoví uživatelé mohou zobrazit v centru zabezpečení v programu Microsoft Defender a v oznámeních, která obdrží. Aplikace zabezpečení systému Windows je používána řadou funkcí zabezpečení systému Windows k poskytování oznámení o stavu a zabezpečení počítače. Oznámení aplikací pro zabezpečení zahrnují brány firewall, antivirové produkty, filtr SmartScreen v programu Windows Defender a další.

## <a name="antivirus-policy-reports"></a>Sestavy zásad antivirové ochrany

V sestavách zásad antivirové ochrany se zobrazí podrobnosti o stavu vašich zásad zabezpečení koncového bodu a stavu zařízení. Tyto sestavy jsou k dispozici v uzlu zabezpečení koncového bodu v centru pro správu služby Microsoft Endpoint Manager.

Pokud si chcete zobrazit sestavy, v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), navštivte Endpoint Security a vyberte **antivirová ochrana**. Výběrem antivirového programu otevřete stránku Shrnutí. Další zobrazení sestav a stavů jsou k dispozici jako další stránky.

### <a name="summary"></a>Souhrn

Na stránce **Souhrn** můžete [vytvořit nové zásady](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) a zobrazit seznam dříve vytvořených zásad. Seznam obsahuje podrobné informace o profilu, který zásada zahrnuje (typ zásady), a informace o tom, jestli je zásada přiřazená.

![Stránka s přehledem zásad antivirové ochrany](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Když v seznamu vyberete zásadu, otevře se stránka *Přehled* této instance zásad a zobrazí se další informace. Když v tomto zobrazení vyberete dlaždici, Intune zobrazí další podrobnosti pro tento profil, pokud jsou k dispozici.

![Stránka s přehledem zásad antivirové ochrany](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Koncové body Windows 10 nejsou v pořádku

Na stránce **koncové body ve Windows 10 nesprávného stavu** můžete zobrazit informace o stavu antivirového programu zařízení s Windows 10 spravovaných MDM. Tyto informace se vrátí z antivirové ochrany v programu Windows Defender, která běží na zařízení jako *Stav agenta hrozeb*.

V tomto zobrazení se zobrazí pouze zařízení se zjištěnými problémy. Toto zobrazení nezobrazuje podrobnosti o zařízeních, která jsou označena jako čistá.

![Stránka s přehledem zásad antivirové ochrany](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
