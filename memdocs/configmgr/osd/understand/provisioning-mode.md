---
title: Režim zřizování
titleSuffix: Configuration Manager
description: Přečtěte si o režimu zřizování klientů během Configuration Manager pořadí úkolů.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0039648c6f444efdbbaeb16f55d29b630ee7f16
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124266"
---
# <a name="provisioning-mode"></a>Režim zřizování

*Platí pro: Configuration Manager (Current Branch)*

Během pořadí úloh nasazení operačního systému Configuration Manager umístí klienta do režimu zřizování. (Pořadí úloh nasazení operačního systému zahrnuje místní upgrade na Windows 10.) V tomto stavu klient nezpracovává zásady z lokality. Toto chování umožňuje, aby pořadí úkolů běželo bez rizika dalších nasazení spuštěných v klientovi. Po úspěšném nebo neúspěšném zpracování pořadí úkolů ukončí režim zřizování klientů.

Pokud se pořadí úkolů neočekávaně nezdařilo, může být klient ponechán v režimu zřizování. Například pokud se zařízení restartuje uprostřed zpracování pořadí úkolů a nedá se obnovit. Správce musí ručně identifikovat a opravit klienty v tomto stavu.


## <a name="manually-remove-provisioning-mode"></a>Ruční odebrání režimu zřizování

Pokud je klient v režimu zřizování, pomocí tohoto ručního procesu vraťte klienta do normálního provozu.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Jedna z změn provedených touto metodou WMI nastavuje hodnotu registru, ale provádí i další změny. Pouhým změnou hodnoty registru nebude klient úplně převzít z režimu zřizování. Pokud registr ručně upravíte, může klient projevit neočekávané chování.  


## <a name="client-provisioning-mode-timeout"></a>Časový limit režimu zřizování klientů

Počínaje verzí 1902 pořadí úkolů nastaví časové razítko, když klient umístí do režimu zřizování. Každých 60 minut klient v režimu zřizování kontroluje dobu trvání od časového razítka. Pokud je v režimu zřizování více než 48 hodin, klient automaticky ukončí režim zřizování a restartuje jeho proces.

48 hodin je výchozí hodnota časového limitu pro režim zřizování. Tento časovač můžete na zařízení upravit nastavením hodnoty **ProvisioningMaxMinutes** v následujícím klíči registru: `HKLM\Software\Microsoft\CCM\CcmExec` . Pokud tato hodnota neexistuje nebo je `0` , klient použije výchozí 48 hodin.

Časové razítko **ProvisioningEnabledTime** se nachází v následujícím klíči registru: `HKLM\Software\Microsoft\CCM\CcmExec` . Časové razítko má hodnotu poslední čas, kdy počítač zadal režim zřizování. Formát je epocha (časové razítko v systému UNIX) a je v čase UTC.

Toto časové razítko se také resetuje na aktuální čas při ručním umístění počítače do režimu zřizování pomocí následujícího příkazu:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Vývojové diagramy procesů

Tyto diagramy znázorňují tok procesu pro pořadí úloh a klienta.

### <a name="task-sequence"></a>Pořadí úkolů

Následující diagram znázorňuje, jak pořadí úkolů nastavuje režim zřizování:

![Vývojový diagram nastavení režimu zřizování pořadí úloh](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Náprava klienta

Následující diagram ukazuje, jak klient ukončí režim zřizování:

![Vývojový diagram klienta, který ukončuje režim zřizování](media/3197824-client-flow.png)


## <a name="see-also"></a>Viz také

[Nastavit systém Windows a nástroj ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Upgradovat operační systém](task-sequence-steps.md#BKMK_UpgradeOS)
