---
title: Nasazení Windows pomocí samostatného média
titleSuffix: Configuration Manager
description: Použití samostatného média v Configuration Manager k nasazení systému Windows, kde je šířka pásma omezená jako možnost aktualizace, instalace nebo upgradu počítačů.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724220"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Nasazení Windows pomocí samostatného média bez použití sítě

*Platí pro: Configuration Manager (Current Branch)*

Samostatné médium v Configuration Manager obsahuje všechno, co je potřeba k nasazení operačního systému na počítači. To zahrnuje spouštěcí image, image operačního systému a pořadí úkolů pro instalaci operačního systému včetně aplikací, ovladačů a tak dál. Nasazení ze samostatného média umožňuje nasadit operační systém za následujících podmínek:  

-   V prostředích, v nichž není praktické kopírovat bitovou kopii operačního systému nebo další velké balíčky prostřednictvím sítě.  

-   V prostředích bez připojení k síti nebo se síťovým připojením s malou šířkou pásma.  

Samostatné médium můžete použít v následujících scénářích nasazení operačního systému:  

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

- [Upgrade systému Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md)  

  Proveďte kroky v jednom ze scénářů nasazení operačního systému, potom se podle následujících částí připravte na vytvoření samostatného média a nakonec ho vytvořte.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Nepodporované akce pořadí úkolů při použití samostatného média  
 Pokud jste provedli kroky uvedené v jednom z podporovaných scénářů nasazení operačního systému, vytvořilo se pořadí úkolů pro nasazení nebo upgrade operačního systému a všechen přidružený obsah se distribuoval do distribučního bodu. Při použití samostatného média není v pořadí úkolů dostupná podpora následujících akcí:  

-   Krok Automaticky použít ovladače v pořadí úkolů. Automatické použití ovladačů zařízení z katalogu ovladačů se nepodporuje, ale můžete zvolit krok Použít balíček ovladače a zpřístupnit zadanou sadu ovladačů pro instalační program systému Windows.  

-   Instalování aktualizací softwaru.  

-   Instalování softwaru před nasazením operačního systému.  

-   Spojování uživatelů s cílovým počítačem pro podporu spřažení uživatelských zařízení.  

-   Dynamický balíček se nainstaluje prostřednictvím úkolu instalace balíčků.  

-   Dynamická aplikace se instaluje prostřednictvím úkolu instalace aplikace.  

> [!NOTE]  
>  Pokud pořadí úkolů pro nasazení operačního systému zahrnuje krok [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) a vy vytvoříte samostatné médium v lokalitě centrální správy, může dojít k chybě. Lokalita centrální správy nemusí obsahovat zásady konfigurace klienta, které jsou požadovány pro povolení agenta distribuce softwaru při provádění pořadí úloh. V souboru CreateTsMedia.log se může objevit následující chyba:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  U samostatného média, které obsahuje krok **Instalovat balíček** , musíte samostatné médium vytvořit v primární lokalitě s povoleným agentem distribuce softwaru, případně přidat krok [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) za krok [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) a před první krok **Instalovat balíček** v pořadí úkolů. Krok **Spustit příkazový řádek** spustí příkaz WMIC, který povolí agenta distribuce softwaru před prvním spuštěním kroku Instalovat balíček. V kroku pořadí úloh **Spustit příkazový řádek** můžete použít následující zadání:  
>   
>  **Příkazový řádek**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení  
 Když používáte samostatné médium k zahájení procesu nasazení operačního systému, musíte nakonfigurovat nasazení, aby byl operační systém v médiu dostupný. To můžete nakonfigurovat na stránce **Nastavení nasazení** Průvodce nasazením softwaru nebo na kartě **Nastavení nasazení** ve vlastnostech nasazení.  U nastavení **Zpřístupnit pro následující** nakonfigurujte jednu z následujících možností:  

-   **Klienti aplikace Configuration Manager, média a technologie PXE**  

-   **Pouze média a technologie PXE**  

-   **Pouze média a technologie PXE (skryté)**  

## <a name="create-the-stand-alone-media"></a>Vytvoření samostatného média  
 Můžete určit, jestli chcete jako samostatné médium použít USB flash disk nebo sadu disků CD/DVD. Počítač, který médium spustí, musí podporovat možnost, kterou zvolíte jako spouštěcí jednotku. Další informace najdete v tématu [vytvoření samostatného média](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Instalace operačního systému ze samostatného média  
 Vložte samostatné médium do spouštěcí jednotky v počítači a potom počítač zapněte, aby se nainstaloval operační systém.  
