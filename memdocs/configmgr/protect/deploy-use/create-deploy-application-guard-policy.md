---
title: Spravovat zásady ochrany Application Guard
titleSuffix: Configuration Manager
description: Naučte se vytvářet a nasazovat zásady ochrany Application Guard v programu Microsoft Defender.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1189f8c89215bc228c533a88f38f5ae59b6855ee
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454932"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Vytvoření a nasazení zásad ochrany Application Guard v programu Microsoft Defender

*Platí pro: Configuration Manager (Current Branch)*
<!-- 1351960 -->  
Zásady ochrany Application [Guard (Application Guard) programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview) můžete vytvořit a nasadit pomocí Configuration Manager Endpoint Protection. Tyto zásady chrání uživatele otevřením nedůvěryhodných webů v zabezpečeném izolovaném kontejneru, který není přístupný jiným součástem operačního systému.

## <a name="prerequisites"></a>Požadavky

Chcete-li vytvořit a nasadit zásady ochrany Application Guard v programu Microsoft Defender, je nutné použít aktualizaci Windows 10 Updates Creator (1709). U zařízení s Windows 10, na které zásadu nasazujete, se musí nakonfigurovat [zásada izolace sítě](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings). Další informace najdete v tématu [Přehled ochrany Application Guard v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Vytvoření zásady a procházení dostupných nastavení

1. V konzole Configuration Manager vyberte **prostředky a kompatibilita**.
2. V pracovním prostoru **prostředky a kompatibilita** vyberte **Přehled**  >  **Endpoint Protection**  >  **ochrana Application Guard v programu Windows Defender**.
3. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit zásadu Application Guard v programu Windows Defender**.
4. Pomocí [článku](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard) jako reference můžete procházet a konfigurovat dostupná nastavení. Configuration Manager vám umožní nastavit určitá nastavení zásad:
   - [Nastavení interakce hostitele](#bkmk_HIS)
   - [Chování aplikace](#bkmk_ABS)
   - [Správa souborů](#bkmk_FM)
5. Na stránce **definice sítě** zadejte podnikovou identitu a definujte hranici vaší podnikové sítě.

    > [!NOTE]
    > Počítače s Windows 10 ukládají na klientovi jenom jeden seznam izolace sítě. Můžete vytvořit dva různé druhy seznamů izolace sítě a nasadit je do klienta:
    >
    >  - jedna z Information Protection Windows
    >  - jedna z ochrany Application Guard v programu Microsoft Defender
    >
    > Pokud nasadíte obě zásady, musí tyto seznamy izolace sítě odpovídat. Pokud nasadíte seznamy, které se neshodují se stejným klientem, nasazení se nezdaří. Další informace najdete v dokumentaci k [Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Až skončíte, dokončete průvodce a Nasaďte zásadu na jedno nebo více zařízení s Windows 10 1709.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a>Nastavení interakce hostitele

Konfiguruje interakce mezi hostitelskými zařízeními a kontejnerem ochrany Application Guard. Před Configuration Manager verze 1802 se na kartě **Nastavení** používala chování aplikace i interakce hostitele.

- **Schránka** v nastavení před Configuration Manager 1802
  - Povolený typ obsahu
    - Text
    - Image
- **Komerční**
  - Povolit tisk do XPS
  - Povolit tisk do PDF
  - Povolit tisk na místních tiskárnách
  - Povolit tisk na síťových tiskárnách
- **Graphics:** (počínaje Configuration Manager verze 1802)
  - Přístup k virtuálnímu grafickému procesoru
- **Soubory:** (počínaje verzí 1802 Configuration Manager)
  - Uložit stažené soubory na hostitele

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a>Nastavení chování aplikace

Nakonfiguruje chování aplikace v relaci ochrany Application Guard. Před Configuration Manager verze 1802 se na kartě **Nastavení** používala chování aplikace i interakce hostitele.

- **Sušin**
  - Podnikové weby můžou načítat nefiremní obsah, například moduly plug-in třetích stran.
- **Jiná**
  - Zachovat uživatelem generovaná data prohlížeče
  - Auditovat události zabezpečení v izolované relaci ochrany Application Guard

### <a name="file-management"></a><a name="bkmk_FM"></a>Správa souborů
<!--3555858-->
Od verze Configuration Manager 1906 existuje nastavení zásad, které uživatelům umožňuje důvěřovat souborům, které se normálně otevřou v ochraně Application Guard. Po úspěšném dokončení se soubory otevřou na hostitelském zařízení, nikoli v ochraně Application Guard. Další informace o zásadách ochrany Application Guard najdete v tématu [Konfigurace nastavení zásad ochrany Application Guard v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard).

- **Povolit uživatelům důvěřovat souborům, které se otevřou v ochraně Application Guard v programu Windows Defender** – umožní uživateli označovat soubory jako důvěryhodné. Když je soubor důvěryhodný, otevře se na hostiteli, nikoli v ochraně Application Guard. Platí pro klienty Windows 10 verze 1809 nebo vyšší.
  - **Zakázáno:** Nedovolte uživatelům označovat soubory jako důvěryhodné (výchozí).
  - **Soubor zkontrolovaný antivirovým programem:** Umožní uživatelům označit soubory jako důvěryhodné po kontrole antivirové ochrany.
  - **Všechny soubory:** Umožní uživatelům označit kterýkoli soubor jako důvěryhodný.

Pokud povolíte správu souborů, může dojít k chybám zaznamenaným v DCMReporting. log klienta. Následující chyby se obvykle neprojevují: <!--4619457-->

- Na kompatibilních zařízeních:
  - FileTrustCriteria_condition se nenašel.
- Na nekompatibilních zařízeních:
  - FileTrustCriteria_condition se nenašel.
  - FileTrustCriteria_condition se nepovedlo najít na mapě.
  - V algoritmu Digest nebyl nalezen FileTrustCriteria_condition.

Chcete-li upravit nastavení ochrany Application Guard, rozbalte položku **Endpoint Protection** v pracovním prostoru **prostředky a kompatibilita** a pak klikněte na uzel **ochrana Application Guard v programu Windows Defender** . Klikněte pravým tlačítkem na zásadu, kterou chcete upravit, a pak vyberte **vlastnosti**.

## <a name="known-issues"></a>Známé problémy

Zařízení s Windows 10 verze 2004 budou zobrazovat chyby v sestavách dodržování předpisů pro kritéria důvěryhodnosti souborů ochrany Application Guard v programu Microsoft Defender. K tomuto problému dochází, protože některé podtřídy se odebraly z třídy WMI `MDM_WindowsDefenderApplicationGuard_Settings01` ve Windows 10 verze 2004. Všechna ostatní nastavení ochrany Application Guard v programu Microsoft Defender budou stále platit, ale selžou pouze kritéria pro vztah důvěryhodnosti souborů. V současné době neexistují žádná alternativní řešení pro obejít chybu. <!--7099444,5946790-->

## <a name="next-steps"></a>Další kroky

Další informace o ochraně Application Guard v programu Microsoft Defender najdete v části
 - [Přehled ochrany Application Guard v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)
- [Nejčastější dotazy k ochraně Application Guard v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard).
