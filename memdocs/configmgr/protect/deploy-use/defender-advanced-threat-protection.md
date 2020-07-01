---
title: Rozšířená ochrana před internetovými útoky v programu Microsoft Defender
titleSuffix: Configuration Manager
description: Naučte se spravovat a monitorovat rozšířenou ochranu před internetovými útoky v programu Microsoft Defender, novou službu, která pomáhá podnikům reagovat na pokročilé útoky.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613487"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Rozšířená ochrana před internetovými útoky v programu Microsoft Defender

*Platí pro: Configuration Manager (Current Branch)*

Endpoint Protection může pomáhat spravovat a monitorovat [rozšířenou ochranu před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (dříve označované jako ATP v programu Windows Defender). ATP v programu Microsoft Defender pomáhá podnikům zjišťovat, zkoumat a reagovat na pokročilé útoky v jejich sítích. Zásady Configuration Manager vám můžou pomáhat s připojováním a monitorováním klientů s Windows 10.

Microsoft Defender ATP je služba v [Security Center programu Microsoft Defender](https://securitycenter.windows.com). Když přidáte a nasadíte konfigurační soubor klienta, Configuration Manager může monitorovat stav nasazení a stav agenta ATP v programu Microsoft Defender. Ochrana ATP v programu Microsoft Defender je podporovaná na počítačích, na kterých běží klient Configuration Manager nebo [které spravuje Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

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
Počínaje verzí 2002 Configuration Manager můžete připojit následující operační systémy:

- Windows 8.1
- Windows 10 verze 1607 nebo novější
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, verze 1803 nebo novější
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>O připojování k ATP pomocí Configuration Manager

Různé operační systémy mají různé požadavky na registraci do ATP. Windows 8.1 a jiná zařízení s operačním systémem nižší úrovně potřebují ke zprovoznění **klíč pracovního prostoru** a **ID pracovního prostoru** . Zařízení, jako je třeba Windows Server verze 1803, vyžadují konfigurační soubor připojování. Configuration Manager také nainstaluje Microsoft Monitoring Agent (MMA), pokud to vyžaduje zařízení připojená, ale neaktualizuje agenta automaticky.

Mezi operační systémy nejvyšší úrovně patří:
- Windows 10 verze 1607 a novější
- Windows Server 2016, verze 1803 nebo novější
- Windows Server 2019

Mezi operační systémy nižší úrovně patří:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, verze 1709 a starší

Když připojíte zařízení k ATP pomocí Configuration Manager, nasadíte zásady ATP do cílové kolekce nebo do více kolekcí. V některých případech cílová kolekce obsahuje zařízení s libovolným počtem podporovaných operačních systémů. Pokyny k připojování těchto zařízení se liší v závislosti na tom, jestli cílíte na kolekci obsahující zařízení s operačními systémy, které jsou na úrovni služby, nižší úrovně nebo obojí.

- Pokud vaše cílová kolekce obsahuje zařízení na nejvyšší úrovni i na nižší úrovni, použijte pokyny k připojení [zařízení s jakýmkoli podporovaným operačním systémem](#bkmk_any_os) (doporučeno).
- Pokud vaše kolekce obsahuje jenom zařízení na úrovni služby, můžete použít [pokyny k registraci na úrovni](#bkmk_uplevel).
- Pokud vaše kolekce obsahuje jenom zařízení nižší úrovně, můžete použít pokyny k registraci na [nižší úrovni](#bkmk_downlevel).

> [!Warning]
> - Pokud vaše cílová kolekce obsahuje zařízení na úrovni a použijete pokyny pro zařízení nižší úrovně, zařízení na nejvyšší úrovni nebudou připojená.
> - Pokud vaše cílová kolekce obsahuje zařízení nižší úrovně a použijete pokyny pro zařízení se škálováním na úrovni služby, zařízení nižší úrovně nebudou připojená.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a>Připojit zařízení s jakýmkoli podporovaným operačním systémem do ATP (doporučeno)
 Můžete připojit zařízení s některým z [podporovaných operačních systémů](#bkmk_os) k ATP tím, že poskytnete konfigurační soubor, **klíč pracovního prostoru**a **ID pracovního prostoru** , které chcete Configuration Manager.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Získá konfigurační soubor, ID pracovního prostoru a klíč pracovního prostoru.

1. Přejít na [online službu Microsoft Defender ATP](https://securitycenter.windows.com/) a přihlaste se.
1. Vyberte **Nastavení**a potom v záhlaví **Správa zařízení** vyberte **připojování** .
1. V části operační systém vyberte **Windows 10**.
1. Pro metodu nasazení vyberte možnost **Microsoft Endpoint Configuration Manager Current Branch a novější** .
1. Klikněte na **Stáhnout balíček**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Stažení konfiguračního souboru pro registraci" lightbox="media/5229962-onboarding-configuration.png":::
1. Stáhněte komprimovaný soubor archivu (. zip) a extrahujte obsah.
1. Vyberte **Nastavení**a potom v záhlaví **Správa zařízení** vyberte **připojování** .
1. V případě operačního systému vyberte ze seznamu buď **Windows 7 SP1 a 8,1** nebo **Windows Server 2008 R2 SP1, 2012 R2 a 2016** .
   - **Klíč pracovního prostoru** a **ID pracovního prostoru** budou stejné bez ohledu na to, kterou možnost zvolíte.
1. Zkopírujte hodnoty **klíče pracovního prostoru** a **ID pracovního prostoru** z části **Konfigurace připojení** .

   > [!IMPORTANT]
   > Konfigurační soubor ATP v programu Microsoft Defender obsahuje citlivé informace, které by měly být zachovány v bezpečí.


### <a name="onboard-the-devices"></a>Připojení zařízení

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita**  >  **Endpoint Protection**  >  **Zásady ochrany ATP v programu Microsoft Defender**.
1. Vyberte **vytvořit zásadu ochrany ATP v programu Microsoft Defender** a otevřete Průvodce zásadami ochrany ATP v programu Microsoft Defender. 
1. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender a vyberte **připojování**.
1. **Přejděte** ke konfiguračnímu souboru, který jste extrahovali ze staženého souboru. zip.
1. Zadejte **klíč pracovního prostoru** a **ID pracovního prostoru** a potom klikněte na **Další**.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Průvodce vytvořením zásad ATP v programu Microsoft Defender" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Zadejte ukázky souborů, které se shromažďují a sdílejí ze spravovaných zařízení pro účely analýzy.  
   - **Žádné**
   - **Všechny typy souborů**  
1. Projděte si souhrn a dokončete průvodce.  
1. Klikněte pravým tlačítkem na zásadu, kterou jste vytvořili, a pak vyberte **nasadit** a Zaměřte se na zásady ATP v programu Microsoft Defender na klienty.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a>Připojení zařízení s operačními systémy na úrovni ATP

Klienti nejvyšší úrovně vyžadují konfigurační soubor připojování pro připojování k ATP. Mezi operační systémy nejvyšší úrovně patří:
- Windows 10 verze 1607 a novější 
- Windows Server 2016, verze 1803 a novější
- Windows Server 2019

Pokud vaše cílová kolekce obsahuje zařízení na nejvyšší úrovni i nižší úrovně, nebo pokud si nejste jistí, použijte pokyny k připojení [zařízení s jakýmkoli podporovaným operačním systémem (doporučeno)](#bkmk_any_os).

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Získání konfiguračního souboru připojování pro zařízení na úrovni služby

1. Přejít na [online službu Microsoft Defender ATP](https://securitycenter.windows.com/) a přihlaste se.
1. Vyberte **Nastavení**a potom v záhlaví **Správa zařízení** vyberte **připojování** .
1. V části operační systém vyberte **Windows 10**.
1. Pro metodu nasazení vyberte možnost **Microsoft Endpoint Configuration Manager Current Branch a novější** .
1. Klikněte na **Stáhnout balíček**.
1. Stáhněte komprimovaný soubor archivu (. zip) a extrahujte obsah.

> [!IMPORTANT]
> Konfigurační soubor ATP v programu Microsoft Defender obsahuje citlivé informace, které by měly být zachovány v bezpečí.


### <a name="onboard-the-up-level-devices"></a>Připojení zařízení na nejvyšší úrovni

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita**  >  **Endpoint Protection**  >  **Zásady ochrany ATP v programu Microsoft Defender** a vyberte **vytvořit zásadu ochrany ATP v programu Microsoft Defender**. Otevře se Průvodce zásadami ochrany ATP v programu Microsoft Defender.  
1. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender a vyberte **připojování**.
1. **Přejděte** ke konfiguračnímu souboru, který jste extrahovali ze staženého souboru. zip.
   > [!Note]
   > Pro Configuration Manager verze 2002 budete potřebovat **klíč** a **ID pracovního** prostoru a to i v případě, že zaměříte jenom zařízení na nejvyšší úrovni. Tyto hodnoty získáte tak, že vyberete **Nastavení**  >  **připojování**  >  **Windows 7 a 8,1** od [online služby Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188-->
1. Zadejte ukázky souborů, které se shromažďují a sdílejí ze spravovaných zařízení pro účely analýzy.  
   - **Žádné**
   - **Všechny typy souborů**  
1. Projděte si souhrn a dokončete průvodce.  
1. Klikněte pravým tlačítkem na zásadu, kterou jste vytvořili, a pak vyberte **nasadit** a Zaměřte se na zásady ATP v programu Microsoft Defender na klienty.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a>Připojení zařízení s operačními systémy nižší úrovně k ATP

Klienti nižší úrovně vyžadují **klíč pracovního prostoru** a **ID pracovního prostoru** pro připojování atp. Mezi operační systémy nižší úrovně patří:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, verze 1709 a starší

Pokud vaše cílová kolekce obsahuje zařízení na nejvyšší úrovni i nižší úrovně, nebo pokud si nejste jistí, použijte pokyny k připojení [zařízení s jakýmkoli podporovaným operačním systémem (doporučeno)](#bkmk_any_os).

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>Získat ID a klíč pracovního prostoru pro zařízení nižší úrovně

1. Přejít na [online službu Microsoft Defender ATP](https://securitycenter.windows.com/) a přihlaste se.
1. Vyberte **Nastavení**a potom v záhlaví **Správa zařízení** vyberte **připojování** .
1. V případě operačního systému vyberte ze seznamu buď **Windows 7 SP1 a 8,1** nebo **Windows Server 2008 R2 SP1, 2012 R2 a 2016** .
   - **Klíč pracovního prostoru** a **ID pracovního prostoru** budou stejné bez ohledu na to, kterou možnost zvolíte.
1. Zkopírujte hodnoty **klíče pracovního prostoru** a **ID pracovního prostoru** z části **Konfigurace připojení** .

### <a name="onboard-the-down-level-devices"></a>Připojení zařízení na nižší úrovni

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita**  >  **Endpoint Protection**  >  **Zásady ochrany ATP v programu Microsoft Defender** a vyberte **vytvořit zásadu ochrany ATP v programu Microsoft Defender**. Otevře se Průvodce zásadami ochrany ATP v programu Microsoft Defender.  
1. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender a vyberte **připojování**.
1. Zadejte **klíč pracovního prostoru** a **ID pracovního prostoru**.
   > [!Note]
   > - Pro Configuration Manager verze 2002 budete potřebovat konfigurační soubor, i když připojujete jenom zařízení nižší úrovně. Tyto hodnoty získáte tak, že vyberete **Nastavení**  >  **připojování**  >  **Windows 10** od [online služby Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188--> 
   > - Konfigurační soubor ATP v programu Microsoft Defender obsahuje citlivé informace, které by měly být zachovány v bezpečí.
1. Zadejte ukázky souborů, které se shromažďují a sdílejí ze spravovaných zařízení pro účely analýzy.  
   - **Žádné**
   - **Všechny typy souborů**  
1. Projděte si souhrn a dokončete průvodce.  
1. Klikněte pravým tlačítkem na zásadu, kterou jste vytvořili, a pak vyberte **nasadit** a Zaměřte se na zásady ATP v programu Microsoft Defender na klienty.


## <a name="monitor"></a>Monitorování

1. V konzole Configuration Manager přejděte na **monitorování**  >  **zabezpečení** a pak vyberte **ATP Microsoft Defender**.  

1. Projděte si řídicí panel rozšířené ochrany před internetovými útoky v programu Microsoft Defender.  

    - **Stav registrace agenta ATP v programu Microsoft Defender**: počet a procento oprávněných spravovaných klientských počítačů s aktivními zásadami ochrany ATP společnosti Microsoft Defender  

    - **Agent Health ATP v programu Microsoft Defender**: procento klientských počítačů hlásících stav pro svého agenta ochrany ATP v programu Microsoft Defender  

        - **V pořádku** – funguje správně  

        - **Neaktivní** – během časového období se neodesílají žádná data do služby.  

        - **Stav agenta** – systémová služba pro agenta ve Windows není spuštěná.  

        - **Není** připojené – zásady se použily, ale agent neohlásil připojení zásad.  

## <a name="create-an-offboarding-configuration-file"></a>Vytvoření konfiguračního souboru pro zrušení  

1. Přihlaste se k [online službě Microsoft Defender ATP](https://securitycenter.windows.com/).
1. Vyberte **Nastavení**a potom v záhlaví **Správa zařízení** **Vyberte položku** oddálení.
1. Pro operační systém a **Microsoft Endpoint Configuration Manager Current Branch a novějších** pro metodu nasazení vyberte **Windows 10** .
   - Když použijete možnost **Windows 10** , zajistíte, že všechna zařízení v kolekci budou offboarded a v případě potřeby se odinstaluje MMA.
1. Stáhněte komprimovaný soubor archivu (. zip) a extrahujte obsah. Soubory pro odpojování jsou platné po dobu 30 dnů.

1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita**  >  **Endpoint Protection**  >  **Zásady ochrany ATP v programu Microsoft Defender** a vyberte **vytvořit zásadu ochrany ATP v programu Microsoft Defender**. Otevře se Průvodce zásadami ochrany ATP v programu Microsoft Defender.  

1. Zadejte **název** a **Popis** zásad ATP v programu Microsoft Defender **a vyberte možnost**odregistrování.

1. **Přejděte** ke konfiguračnímu souboru, který jste extrahovali ze staženého souboru. zip.

1. Projděte si souhrn a dokončete průvodce.  

Vyberte **nasadit** a Zaměřte se na zásady ATP v programu Microsoft Defender na klienty.  

> [!IMPORTANT]
> Konfigurační soubory ATP v programu Microsoft Defender obsahují citlivé informace, které by měly být zachovány v bezpečí.

## <a name="next-steps"></a>Další kroky

- [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Řešení potíží s připojováním k Rozšířené ochraně před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
