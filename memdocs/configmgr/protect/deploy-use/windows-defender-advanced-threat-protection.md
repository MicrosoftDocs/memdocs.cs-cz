---
title: Rozšířená ochrana před internetovými útoky v programu Microsoft Defender
titleSuffix: Configuration Manager
description: Naučte se spravovat a monitorovat rozšířenou ochranu před internetovými útoky v programu Microsoft Defender, novou službu, která pomáhá podnikům reagovat na pokročilé útoky.
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a635ae36875984537c18c4850a3526d57ffceb31
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210141"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Rozšířená ochrana před internetovými útoky v programu Microsoft Defender

*Platí pro: Configuration Manager (Current Branch)*

Endpoint Protection může pomáhat spravovat a monitorovat [rozšířenou ochranu před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (dříve označované jako ATP v programu Windows Defender). ATP v programu Microsoft Defender pomáhá podnikům zjišťovat, zkoumat a reagovat na pokročilé útoky v jejich sítích. Zásady Configuration Manager vám můžou pomáhat s připojováním a monitorováním klientů s Windows 10.

Microsoft Defender ATP je služba v [Security Center programu Windows Defender](https://securitycenter.windows.com). Když přidáte a nasadíte konfigurační soubor klienta, Configuration Manager může monitorovat stav nasazení a stav agenta ATP v programu Microsoft Defender. Ochrana ATP v programu Microsoft Defender je podporovaná na počítačích, na kterých běží klient Configuration Manager nebo [které spravuje Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Požadavky

- Předplatné služby Microsoft Defender Advanced Threat Protection online  
- Klienti počítačů s Configuration Manager klientem
- Klienti používající operační systém uvedený níže v části [Podporované klientské operační systémy](#bkmk_os) .

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a>Podporované klientské operační systémy
Na základě verze Configuration Manager, kterou používáte, se dají připojit následující klientské operační systémy:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager verze 1910 a předchozí

- Klienti počítačů se systémem Windows 10 verze 1607 a novějším

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager verze 2002 a novější
<!--5229962-->
- Windows 7 SP1
- Windows 8.1
- Windows 10 verze 1607 nebo novější
- Windows Server 2008 R2 SP1
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, verze 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Vytvoření konfiguračního souboru připojování

1. Přejít na [online službu Microsoft Defender ATP](https://securitycenter.windows.com/) a přihlaste se.
1. V části **Nastavení**vyberte **Správa počítače** a pak vyberte **připojování**.
1. Vyberte operační systémy, které chcete zařadit ze seznamu.
   - Pokud se připojujete k Windows 10, Windows serveru 1803 a Windows Server 2019:
      1. Vyberte **Configuration Manager (aktuální větev) verze 1606** a vyberte **Stáhnout balíček**.
      1. Stáhněte komprimovaný soubor archivu (. zip) a extrahujte obsah.
   - Pokud se připojujete k jinému operačnímu systému Windows: 
      1. Vyberte operační systémy, které chcete zařadit ze seznamu. Například vyberte buď **Windows 7 a 8,1** nebo **Windows Server 2008 R2 SP1, 2012 R2 a 2016**.
      1. Po dokončení procesu zkopírujte hodnoty pro **klíč** a **ID pracovního** prostoru v části **Konfigurace připojení** .

> [!IMPORTANT]
> - Konfigurační soubor ATP v programu Microsoft Defender obsahuje citlivé informace, které by měly být zachovány v bezpečí.

## <a name="onboard-devices"></a>Připojení zařízení

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita** > **Endpoint Protection** > **Zásady ochrany ATP v programu Windows Defender** a vyberte **vytvořit zásadu ochrany ATP v programu Windows Defender**. Otevře se Průvodce zásadami ochrany ATP v programu Microsoft Defender.  
1. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender a vyberte **připojování**.
1. **Přejděte** ke konfiguračnímu souboru, který poskytl tenant cloudové služby Microsoft Defender ATP pro vaši organizaci.
   - V případě **systémů Windows 7 a 8,1** nebo **Windows Server 2008 R2 SP1, 2012 R2 a 2016**zadejte **klíč pracovního prostoru** a **ID pracovního prostoru**.
   - Pro Configuration Manager verze 2002 budete potřebovat **klíč** a **ID pracovního** prostoru a to i v případě, že se připojujete jenom s Windows serverem 2019 a Windows Server 1803 nebo novějšími zařízeními. Tyto hodnoty získáte tak, že vyberete **Nastavení** > **Onboarding** > připojování**Windows 7 a 8,1** od [online služby Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188-->
1. Zadejte ukázky souborů, které se shromažďují a sdílejí ze spravovaných zařízení pro účely analýzy.  

   - **Žádné**

   - **Všechny typy souborů**  
1. Projděte si souhrn a dokončete průvodce.  

Vyberte **nasadit** a Zaměřte se na zásady ATP v programu Microsoft Defender na klienty.

## <a name="monitor"></a>Monitorování

1. V konzole Configuration Manager přejděte na **sledování** > **zabezpečení** a pak vyberte ochrana **ATP v programu Windows Defender**.  

1. Projděte si řídicí panel rozšířené ochrany před internetovými útoky v programu Microsoft Defender.  

    - **Stav nasazení agenta v programu Windows Defender**: počet a procento oprávněných spravovaných klientských počítačů s aktivními zásadami ochrany ATP společnosti Microsoft Defender  

    - **Agent Health ATP v programu Windows Defender**: procento klientských počítačů hlásících stav pro svého agenta ATP v programu Microsoft Defender  

        - **V pořádku** – funguje správně  

        - **Neaktivní** – během časového období se neodesílají žádná data do služby.  

        - **Stav agenta** – systémová služba pro agenta ve Windows není spuštěná.  

        - **Není** připojené – zásady se použily, ale agent neohlásil připojení zásad.  

## <a name="create-an-offboarding-configuration-file"></a>Vytvoření konfiguračního souboru pro zrušení  

1. Přihlaste se k [online službě Microsoft Defender ATP](https://securitycenter.windows.com/).

1. V části **Nastavení**vyberte **Správa počítače** a pak vyberte **připojování**.  

1. Vyberte **Configuration Manager (aktuální větev) verze 1606** a vyberte možnost odložit **koncový bod**.  

1. Stáhněte komprimovaný soubor archivu (. zip) a extrahujte obsah. Soubory pro odpojování jsou platné po dobu 30 dnů.

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita** > **Endpoint Protection** > **Zásady ochrany ATP v programu Windows Defender** a vyberte **vytvořit zásadu ochrany ATP v programu Windows Defender**. Otevře se Průvodce zásadami ochrany ATP v programu Microsoft Defender.  

1. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender **a vyberte možnost**odregistrování.

1. **Přejděte** ke konfiguračnímu souboru, který poskytl tenant cloudové služby Microsoft Defender ATP pro vaši organizaci.

1. Projděte si souhrn a dokončete průvodce.  

Vyberte **nasadit** a Zaměřte se na zásady ATP v programu Microsoft Defender na klienty.  

> [!IMPORTANT]
> Konfigurační soubory ATP v programu Microsoft Defender obsahují citlivé informace, které by měly být zachovány v bezpečí.

## <a name="next-steps"></a>Další kroky

- [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Řešení potíží s připojováním k Rozšířené ochraně před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
