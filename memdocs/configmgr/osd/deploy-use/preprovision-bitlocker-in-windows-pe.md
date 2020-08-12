---
title: Předběžné zřízení nástroje BitLocker ve Windows PE
titleSuffix: Configuration Manager
description: Předzřízení úlohy nástroje BitLocker v nástroji Configuration Manager povolí nástroj BitLocker z Windows Preinstallation Environment před nasazením operačního systému.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124939"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Předzřízení nástroje BitLocker v prostředí Windows PE s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Krok pořadí úkolů **Předzřídit nástroj BitLocker** v Configuration Manager umožňuje povolit nástroj BitLocker z Windows Preinstallation Environment (Windows PE) před nasazením operačního systému. Šifrováno je pouze použité místo na disku, takže šifrování je mnohem rychlejší. Dosahuje se toho použitím náhodně generované nezašifrované ochrany pro formátovaný svazek a šifrováním svazku před spuštěním procesu instalace Windows. Schopnost předběžného přidělení přístupových práv nástroje BitLocker byla zavedena v systémech Windows 8 a Windows Server 2012. Nicméně můžete předběžně přidělit přístupová práva nástroje BitLocker na pevném disku a nainstalovat systém Windows 7, pokud dodržíte určité kroky. Po dokončení instalace systému Windows 7 musíte nastavit ochranné zařízení klíče nástroje BitLocker, protože ovládací panel nástroje BitLocker systému Windows 7 nepodporuje nástroj BitLocker s výmazovým ochranným zařízením. Ochranné zařízení klíče musíte přidat pomocí kroku **Povolit BitLocker** nebo pomocí nástroje příkazového řádku manage-bde.exe.  

 K úspěšnému předběžnému přidělení přístupových práv nástroje BitLocker na počítači, na který bude instalován systém Windows 7, musíte obecně provést následující akce:  

- Restartovat počítač se systémem Windows PE  

  > [!IMPORTANT]  
  >  Musíte použít spouštěcí bitovou kopii se systémem Windows PE 4 nebo novějším k předběžnému přidělení přístupových práv nástroje BitLocker. Další informace o podporovaných verzích systému Windows PE v nástroji Configuration Manager najdete v tématu [závislosti vnější a Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Rozdělit a naformátovat pevný disk  

- Předběžné přidělení přístupových práv nástroje BitLocker  

- Nainstalovat systém Windows 7 se specifikovaným operačním systémem a nastavením sítě  

- Přidat ochranné zařízení klíče k nástroji BitLocker  

  V Configuration Manager doporučený způsob předběžného přidělení nástroje BitLocker na pevném disku a instalace systému Windows 7 je vytvoření nové sekvence úloh a vybrání možnosti **instalovat existující balíček bitové kopie** ze stránky **vytvořit novou sekvenci úloh** v **Průvodci vytvořením pořadí úloh**. Průvodce vytváří kroky sekvence úloh uvedené v následující tabulce.  

> [!NOTE]  
>  Sekvence úloh může mít další kroky v závislosti na tom, jak jste nakonfigurovali nastavení v průvodci. Například můžete mít krok **Zachytit nastavení systému Windows** , pokud jste vybrali nastavení **Zachycené nastavení systému Microsoft Windows** v průvodci na stránce **Migrace stavu** .  

|Krok pořadí úloh|Podrobnosti|  
|------------------------|-------------|  
|Zakázat nástroj BitLocker|Tento krok zakazuje šifrování nástroje BitLocker, pokud je aktuálně povoleno. Další informace naleznete v části [Disable BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Restartovat počítač se systémem Windows PE|Tento krok restartuje počítač se systémem Windows PE spuštěním spouštěcí bitové kopie přiřazené sekvenci úloh. Musíte použít spouštěcí bitovou kopii se systémem Windows PE 4 nebo novějším k předběžnému přidělení přístupových práv nástroje BitLocker. Další informace najdete v části [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Rozdělit disk 0 – BIOS<br /><br /> Rozdělit disk 0 – UEFI|Tyto kroky formátují a rozdělují určený disk na cílovém počítači pomocí BIOS nebo UEFI. Sekvence úloh používá UEFI, když zjistí, že cílový počítač je v režimu UEFI. Další informace najdete v části [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Předběžné přidělení přístupových práv nástroje BitLocker|Tento krok povoluje nástroj BitLocker na disku se systémem Windows PE. Šifrováno je pouze použité místo na disku. Protože jste rozdělili a naformátovali pevný disk v předchozím kroku, neexistují žádná data a šifrování je dokončeno velmi rychle. Další informace naleznete v části [Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Použít operační systém|Tento krok připravuje odpovídací soubor, který se používá k instalaci operačního systému na cílový počítač a nastavuje proměnnou sekvence úloh OSDTargetSystemDrive k písmenu diskové jednotky oddílu, který obsahuje soubory operačního systému. Odpovídací soubor a proměnná jsou používány krokem Nastavit systém Windows a nástroj ConfigMgr k instalaci operačního systému. Další informace najdete v oddílu [Použít bitovou kopii operačního systému](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Použít nastavení systému Windows|Tento krok přidává nastavení systému Windows do odpovídacího souboru. Odpovídací soubor je používán krokem Nastavit systém Windows a nástroj ConfigMgr k instalaci operačního systému. Další informace naleznete v části [Apply Windows Settings](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Použít nastavení sítě|Tento krok přidává nastavení sítě do odpovídacího souboru. Odpovídací soubor je používán krokem Nastavit systém Windows a nástroj ConfigMgr k instalaci operačního systému. Další informace naleznete v části [Apply Network Settings Step](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Použít ovladače zařízení|Tento krok kontroluje kompatibilitu a instaluje ovladače jako součást nasazení operačního systému. Další informace najdete v části [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Nastavit systém Windows a nástroj ConfigMgr|Tento krok provádí přechod ze systému Windows PE na nový operační systém. Tento krok sekvence úloh je požadovanou součástí nasazení operačního systému. Nainstaluje klienta Configuration Manager do nového operačního systému a připraví pořadí úkolů, aby pokračoval v provádění v novém operačním systému. Další informace najdete v části [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Povolit nástroj BitLocker|Tento krok povoluje šifrování nástroje BitLocker na pevném disku a nastavuje ochranná zařízení klíče. Protože pevnému disku byla přidělena přístupová práva nástroje BitLocker, tento krok je dokončen velmi rychle. Systém Windows 7 požaduje přidání ochranného zařízení klíče. Pokud nepoužijete tento krok, můžete pro nastavení ochranného zařízení klíče spustit nástroj příkazového řádku manage-bde.exe. Další informace naleznete v části [Enable BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
