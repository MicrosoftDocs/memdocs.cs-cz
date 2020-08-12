---
title: Integrace web Windows Update pro firmy
titleSuffix: Configuration Manager
description: Web Windows Update for Business (WUfB) můžete použít k udržování aktuálnosti Windows 10 pro zařízení připojená ke službě web Windows Update.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8ea95a04977038514c00f0199df42c8070e813c3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127650"
---
# <a name="integrate-with-windows-update-for-business"></a>Integrace s web Windows Update pro firmy

*Platí pro: Configuration Manager (Current Branch)*

Web Windows Update for Business (WUfB) umožňuje udržovat zařízení s Windows 10 ve vaší organizaci vždy aktuální s nejnovější ochranou zabezpečení a funkcemi Windows, když se tato zařízení připojují přímo ke službě web Windows Update (WU). Configuration Manager může rozlišovat mezi počítači s Windows 10, které k získávání aktualizací softwaru používají WUfB a WSUS.  

> [!WARNING]
> Pokud pro svá zařízení používáte spolusprávu a přesunuli jste [zásady web Windows Update](../../comanage/workloads.md#windows-update-policies) do Intune, budou vaše zařízení získávat své [zásady web Windows Update pro firmy z Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Pokud je klient Configuration Manager pořád nainstalovaný na spoluspravovaném zařízení, pak se v Intune spravují nastavení pro kumulativní aktualizace a aktualizace funkcí. Opravy, které jsou v [**nastavení klienta**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)povolené, se ale pořád spravují pomocí Configuration Manager.  

 Některé funkce Configuration Manager již nejsou k dispozici, pokud Configuration Manager klienti jsou nakonfigurováni pro příjem aktualizací ze služby WU, což zahrnuje WUfB nebo Windows Insider:  

- Generování sestav o dodržování předpisů služby Windows Update:  
  - Configuration Manager nebude vědět o aktualizacích, které jsou publikovány ve službě WU. U klientů Configuration Manager nakonfigurovaných pro příjem aktualizací ze služby WU se tyto aktualizace zobrazí v konzole Configuration Manager jako **neznámé** .  

  - Řešení potíží s celkovým stavem dodržování předpisů je obtížné, protože **Neznámý** stav byl jenom pro klienty, kteří jste nahlásili stav prohledávání zpátky ze služby WSUS. Teď taky zahrnuje Configuration Manager klienty, kteří získávají aktualizace ze služby WU.  

  - Dodržování předpisů aktualizací definic je součástí generování sestav celkového dodržování předpisů aktualizací a nebude fungovat podle očekávání.

- Celkový Endpoint Protection vytváření sestav pro Defender na základě stavu dodržování předpisů aktualizací nevrátí přesné výsledky, protože chybí data kontroly.  

- Configuration Manager nepůjde nasadit aktualizace Microsoftu, jako jsou aplikace Microsoft 365, IE a Visual Studio, na klienty, kteří jsou připojení k WUfB, aby dostávali aktualizace.  

- Configuration Manager stále můžou nasazovat aktualizace od jiných výrobců, které jsou publikované ve službě WSUS a spravované prostřednictvím Configuration Manager klientům, kteří jsou připojení k WUfB, aby dostávali aktualizace. Pokud nechcete, aby se aktualizace od jiných výrobců nainstalovaly do klientů připojujících se k WUfB, zakažte nastavení klienta s názvem [Povolit aktualizace softwaru na klientech](../../core/clients/deploy/about-client-settings.md#software-updates).

- Configuration Manager úplné nasazení klienta, které používá infrastrukturu aktualizací softwaru, nebude fungovat pro klienty, kteří jsou připojení k WUfB, aby dostávali aktualizace.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifikace klientů, kteří používají WUfB pro aktualizace Windows 10

Pomocí následujícího postupu Identifikujte klienty, kteří používají WUfB k získání aktualizací a upgradů Windows 10. Potom nakonfigurujte tyto klienty tak, aby přestaly používat službu WSUS k získání aktualizací, a nasaďte nastavení agenta klienta, které zakazuje pracovní postup aktualizace softwaru pro tyto klienty.  

### <a name="prerequisites-for-wufb"></a>Předpoklady pro WUfB

- Klienti, kteří používají Windows 10 Desktop Pro nebo Windows 10 Enterprise Edition verze 1511 nebo novější

- Je nasazená služba[Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) a klienti ji používají k získávání aktualizací a upgradů Windows 10.  

### <a name="to-identify-clients-that-use-wufb"></a>Identifikace klientů, kteří používají WUfB  

1. Zajistěte, aby agent web Windows Update nekontroloval službu WSUS, pokud byl dříve povolen. Následující klíč registru lze použít k určení, zda počítač hledá služby WSUS nebo web Windows Update. Pokud klíč registru neexistuje, neprovádí kontrolu na serveru WSUS.
    - **HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. V uzlu **web Windows Update** v Configuration Manager Průzkumník prostředků existuje nový atribut **UseWUServer**.
1. Vytvořte kolekci na základě atributu **UseWUServer** pro všechny počítače, které jsou pro aktualizace a upgrady připojené přes WUfB. Můžete vytvořit kolekci na základě dotazu, který bude vypadat přibližně takto:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Vytvořte nastavení agenta klienta, které zakazuje pracovní postup aktualizace softwaru. Nasaďte nastavení do kolekce počítačů, které jsou připojené přímo k WUfB.
1. Počítače, které jsou spravovány přes WUfB, budou ve stavu dodržování předpisů zobrazovat **Neznámý** a nebudou se počítat jako součást celkového procenta dodržování předpisů.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurace zásad odložení web Windows Update pro firmy
<!-- 1290890 -->
Od verze Configuration Manager 1706 můžete nakonfigurovat zásady odložení pro aktualizace funkcí Windows 10 nebo aktualizace kvality pro zařízení s Windows 10 spravovaná přímo pomocí web Windows Update pro firmy. Zásady odložení můžete spravovat v uzlu nové **zásady web Windows Update pro firmy** v části **softwarová knihovna**  >  **Windows 10 – Údržba**.

> [!NOTE]
> Od verze Configuration Manager 1802 můžete nastavit zásady odložení pro Windows Insider. <!--507201-->  
Další informace o programu Windows Insider najdete v tématu [Začínáme s programem Windows Insider pro firmy](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites-for-deferral-policies"></a>Předpoklady pro zásady odložení

- Windows 10 verze 1703 nebo novější
- Zařízení s Windows 10 spravovaná pomocí web Windows Update pro firmy musí mít připojení k Internetu.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Vytvoření zásady pro odložení web Windows Update pro firmy

1. V **knihovně softwaru**  >  **Windows 10 Údržba**  >  **web Windows Update pro podnikové zásady**
1. Na kartě **Domů** ve skupině **vytvořit** vyberte **vytvořit web Windows Update pro firmy** a otevřete tak Průvodce vytvořením zásad web Windows Update pro firmy.
1. Na stránce **Obecné** zadejte název a popis zásady.
1. Na stránce **zásady odložení** nakonfigurujte, jestli se mají odložit nebo pozastavit aktualizace funkcí. Aktualizace funkcí jsou obecně nové funkce pro Windows. Po konfiguraci nastavení **úrovně připravenosti větve** můžete definovat, jestli a jak dlouho chcete odložit příjem aktualizací funkcí po jejich dostupnosti od Microsoftu.
    - **Úroveň připravenosti větve**: nastavte větev, pro kterou bude zařízení přijímat aktualizace Windows. Vyberte buď půlroční kanál (cílený), půlroční kanál nebo Build Windows Insider.

        > [!NOTE]
        > Nasaďte zásady pro **půlroční kanál (cílený)** na Windows 10 *verze 1903 nebo novější*. Nasaďte zásady pro **půlroční kanál** na Windows 10 *verze 1809 nebo starší*.
        >
        > Pokud nasadíte zásadu pro **půlroční kanál** na Windows 10 verze 1903 nebo novější, nasazení se nezdařilo s chybou **0x8004100C**.<!-- 5593139 -->

    - Doba odkladu **(dny)**: zadejte počet dní, po které budou aktualizace funkcí odloženy. Příjem těchto aktualizací funkcí můžete odložit až o 365 dní od jejich vydání.
    - **Pozastavení funkcí aktualizace od**: Určete, jestli se mají zařízení pozastavit od přijetí aktualizací funkcí po dobu až 35 dnů od doby, kdy jste aktualizace pozastavili. Po uplynutí maximálního počtu dní funkce pozastavení automaticky vyprší a zařízení zkontroluje dostupné aktualizace ve Windows Update. Po této kontrole můžete aktualizace znovu pozastavit. Zaškrtnutím políčka můžete zrušit pozastavení aktualizací funkcí.
1. Vyberte, jestli se mají odložit nebo pozastavit aktualizace kvality. Aktualizace kvality jsou obecně opravy a vylepšení stávajících funkcí Windows a jsou obvykle vydávané první úterý v každém měsíci. Microsoft je ale může vydávat i kdykoli jindy. Můžete definovat, jestli a jak dlouho chcete přijímání aktualizací kvality po jejich vydání odkládat.
    - Doba odkladu **(dny)**: zadejte počet dní, po které se budou aktualizace kvality odvodit. Příjem těchto aktualizací kvality můžete odložit až o 30 dní od jejich vydání.
    - **Spustit aktualizace kvality**od: Určete, jestli se mají zařízení pozastavit od přijetí aktualizací kvality až po 35 dní od okamžiku pozastavení aktualizací. Po uplynutí maximálního počtu dní funkce pozastavení automaticky vyprší a zařízení zkontroluje dostupné aktualizace ve Windows Update. Po této kontrole můžete aktualizace znovu pozastavit. Zaškrtnutím políčka můžete zrušit pozastavení aktualizací kvality.
1. Výběrem možnosti **instalovat aktualizace z dalších produktů společnosti Microsoft** povolte nastavení zásad skupiny, které umožňuje nastavení odložení na Microsoft Update a také aktualizace systému Windows.
1. Chcete-li automaticky aktualizovat ovladače z aktualizací systému Windows, vyberte možnost **zahrnout ovladače s web Windows Update** . Pokud toto nastavení zrušíte, aktualizace ovladačů se nestáhnou z aktualizací Windows.
1. Dokončete průvodce a vytvořte novou zásadu odložení.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Nasazení zásad pro odložení web Windows Update pro firmy

1. V **knihovně softwaru**  >  **Windows 10 Údržba**  >  **web Windows Update pro podnikové zásady**
1. Na kartě **Domů** ve skupině **nasazení** vyberte **nasadit web Windows Update pro podnikové zásady**.
1. Nakonfigurujte tahle nastavení:
    - **Zásady konfigurace, které se mají nasadit**: vyberte zásady web Windows Update pro firmy, které chcete nasadit.
    - **Kolekce**: kliknutím na **Procházet** vyberte kolekci, do které chcete zásady nasadit.
    - **Povolit nápravu mimo okno údržby**: Pokud je pro kolekci, do které nasazujete zásady, nakonfigurované časové období údržby, povolte tuto možnost, aby nastavení zásad mohla napravit hodnotu mimo časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.
    - **Plán**: Určete plán vyhodnocení dodržování předpisů, podle kterého budou nasazené zásady vyhodnoceny na klientských počítačích. Plán může být jednoduchý nebo vlastní.
1. Dokončete Průvodce nasazením zásad.
