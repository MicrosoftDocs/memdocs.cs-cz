---
title: Nasazení Windows pomocí samostatného média
titleSuffix: Configuration Manager
description: Použít samostatná média v Configuration Manager k nasazení systému Windows, kde je šířka pásma omezená jako možnost aktualizace, instalace nebo upgradu počítačů.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124648"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Použití samostatného média k nasazení Windows bez použití sítě

*Platí pro: Configuration Manager (Current Branch)*

Samostatné médium v Configuration Manager obsahuje vše potřebné k nasazení operačního systému v počítači. Médium obsahuje spouštěcí bitovou kopii, image operačního systému, zásady pořadí úkolů, aplikace, ovladače a další. Nasazení samostatného média umožňuje nasadit operační systémy v následujících podmínkách:

- V prostředích, kde není praktické kopírovat bitovou kopii operačního systému nebo další velké balíčky přes síť.

- V prostředích bez připojení k síti nebo s nízkou šířkou pásma.

Samostatné médium můžete použít v následujících scénářích nasazení operačního systému:

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)

- [Upgrade systému Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md)

Proveďte kroky v jednom z těchto scénářů nasazení operačního systému. Pak použijte následující části k přípravě a vytvoření samostatného média.

## <a name="unsupported-task-sequence-actions"></a>Nepodporované akce pořadí úkolů

Pokud používáte samostatná média, Configuration Manager v pořadí úkolů nepodporuje následující akce:

- Krok [automaticky použít ovladače](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) Automatické použití ovladačů zařízení z katalogu ovladačů se nepodporuje. K zpřístupnění konkrétní sady ovladačů pro instalační program systému Windows použijte krok [použít balíček ovladače](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) .

- Instalování aktualizací softwaru.

- Instalace softwaru před nasazením operačního systému.

- Přidružování uživatelů k cílovému počítači pro spřažení uživatelských zařízení.

- Dynamický balíček se nainstaluje pomocí kroku [instalovat balíček](../understand/task-sequence-steps.md#BKMK_InstallPackage) .

- Dynamická aplikace se instaluje s krokem [instalovat aplikaci](../understand/task-sequence-steps.md#BKMK_InstallApplication) .

> [!NOTE]
> Pokud pořadí úkolů pro nasazení operačního systému zahrnuje krok **instalovat balíček** a Vy vytvoříte samostatné médium v lokalitě centrální správy (CAS), může dojít k chybě. Certifikační autorita nemá potřebné zásady konfigurace klienta, aby povolila agenta distribuce softwaru při spuštění pořadí úkolů. V souboru **CreateTSMedia. log** se může zobrazit následující chyba:
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> U samostatného média, které obsahuje krok **instalovat balíček** , vytvořte samostatné médium v primární lokalitě s povoleným agentem distribuce softwaru.
>
> Případně můžete upravit pořadí úkolů a přidat krok [Spustit příkazový řádek](../understand/task-sequence-steps.md#BKMK_RunCommandLine) za krok [nastavit systém Windows a nástroj ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) . Tento krok **spuštění příkazového řádku** spustí následující příkaz WMI, který povolí agenta distribuce softwaru před prvním spuštěním kroku **instalace balíčku** :
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení

Když použijete samostatné médium k zahájení procesu nasazení operačního systému, nakonfigurujte nasazení tak, aby byl operační systém dostupný pro média. Na stránce **nastavení nasazení** v nasazení vyberte u položky **zpřístupnit pro následující** nastavení jednu z následujících možností:

- Configuration Manager klienty, média a technologie PXE

- Pouze média a technologie PXE

- Pouze média a technologie PXE (skryté)

## <a name="create-the-standalone-media"></a>Vytvoření samostatného média

Můžete určit, jestli je samostatné médium jednotka USB flash nebo sada disků CD/DVD. Počítač, který spustí médium, musí podporovat možnost, kterou zvolíte jako spouštěcí jednotku. Další informace najdete v tématu [vytvoření samostatného média](create-stand-alone-media.md).

## <a name="install-the-os-from-standalone-media"></a>Instalace operačního systému ze samostatného média

Pokud chcete nainstalovat operační systém, vložte do počítače samostatné médium a pak ho zapněte.

## <a name="next-steps"></a>Další kroky

[Uživatelská prostředí pro nasazení operačního systému](../understand/user-experience.md#task-sequence-wizard)
