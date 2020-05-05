---
title: Kroky pořadí úloh pro správu převodu systému BIOS na UEFI
titleSuffix: Configuration Manager
description: Naučte se přizpůsobit sekvenci úloh nasazení operačního systému pro přípravu oddílu FAT32 pro přechod na rozhraní UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079361"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Kroky pořadí úloh pro správu převodu systému BIOS na UEFI
Windows 10 poskytuje mnoho nových funkcí zabezpečení, které vyžadují zařízení s podporou rozhraní UEFI. Můžete mít moderní počítače s Windows, které podporují rozhraní UEFI, ale používají starší verzi systému BIOS. Převod zařízení na rozhraní UEFI vyžaduje, abyste přešli na každý počítač, znovu rozdělili pevný disk a znovu nakonfigurovali firmware. Pomocí pořadí úkolů v Configuration Manager můžete připravit pevný disk pro systém BIOS na rozhraní UEFI, převést ze systému BIOS na rozhraní UEFI jako součást místního procesu upgradu a shromažďovat informace o rozhraní UEFI jako součást inventáře hardwaru.

## <a name="hardware-inventory-collects-uefi-information"></a>Inventář hardwaru shromažďuje informace o rozhraní UEFI.
Počínaje verzí 1702 jsou k dispozici novou třídu inventáře hardwaru (**SMS_Firmware**) a vlastnost (**UEFI**), která vám pomůže určit, jestli se počítač spustí v režimu UEFI. Pokud je počítač spuštěn v režimu UEFI, vlastnost **UEFI** je nastavena na **hodnotu true**. Tato možnost je ve výchozím nastavení povolená v inventáři hardwaru. Další informace o inventáři hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Vytvoření vlastního pořadí úloh pro přípravu pevného disku pro převod systému BIOS na rozhraní UEFI
Od verze Configuration Manager 1610 teď můžete přizpůsobit pořadí úloh nasazení operačního systému novou proměnnou, TSUEFIDrive, aby krok **restartovat počítač** PŘIPRAVIL oddíl FAT32 na pevném disku pro přechod do rozhraní UEFI. Následující postup popisuje, jak můžete vytvořit kroky pořadí úloh k přípravě pevného disku pro převod systému BIOS na rozhraní UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Příprava oddílu FAT32 na převod na rozhraní UEFI:
V existujícím pořadí úkolů pro instalaci operačního systému přidáte novou skupinu s postupem, který provede převod systému BIOS na rozhraní UEFI.

1. Po krocích k zaznamenání souborů a nastavení a před instalací operačního systému vytvořte novou skupinu pořadí úkolů. Například vytvořte skupinu za skupinou **zachycení souborů a nastavení** s názvem **BIOS-to-UEFI**.
2. Na kartě **Možnosti** nové skupiny přidejte novou proměnnou pořadí úloh jako podmínku, kde **_SMSTSBootUEFI** se **nerovná hodnotě** **true**. Tím se zabrání spuštění kroků ve skupině v případě, že je počítač již v režimu UEFI.

   ![Skupina systému BIOS do rozhraní UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. V části Nová skupina přidejte krok pořadí úkolů **restartovat počítač** . V části **Určete, co se má spustit po restartování**vyberte **spouštěcí bitová kopie přiřazená k tomuto pořadí úkolů slouží** ke spuštění počítače v systému Windows PE.  
4. Na kartě **Možnosti** přidejte proměnnou pořadí úloh jako podmínku, kde **_SMSTSInWinPE rovná hodnotě false**. Tím se zabrání spuštění tohoto kroku, pokud je počítač již v systému Windows PE.

   ![Krok restartování počítače](../../core/get-started/media/restart-in-windows-pe.png)
5. Přidejte krok, který spustí nástroj výrobce OEM, který převede firmware ze systému BIOS na rozhraní UEFI. Obvykle se jedná o krok **Spustit příkazový řádek** pořadí úkolů s příkazovým řádkem pro spuštění nástroje OEM.
6. Přidejte krok pořadí úkolů formátovat a rozdělit disk na oddíly, který bude rozdělit a naformátovat pevný disk. V kroku udělejte toto:
   1. Před instalací operačního systému vytvořte oddíl FAT32, který bude převeden na rozhraní UEFI. Jako **typ disku**vyberte **GPT** .
    ![Krok formátovat a rozdělit disk na oddíly](../media/format-and-partition-disk.png)
   2. Přejít na vlastnosti oddílu FAT32. Do pole **Proměnná** zadejte **TSUEFIDrive** . Když pořadí úkolů tuto proměnnou detekuje, před restartováním počítače se připraví na přechod rozhraní UEFI.
    ![Vlastnosti oddílu](../../core/get-started/media/partition-properties.png)
   3. Vytvořte oddíl NTFS, který modul pořadí úkolů používá k uložení stavu a ukládání souborů protokolu.
7. Přidejte krok pořadí úkolů **restartovat počítač** . V části **Určete, co se má spustit po restartování**vyberte **spouštěcí bitová kopie přiřazená k tomuto pořadí úkolů slouží** ke spuštění počítače v systému Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Převod ze systému BIOS na rozhraní UEFI během místního upgradu
Windows 10 Creators Update zavádí jednoduchý nástroj pro převod, který automatizuje proces opětovného rozdělení pevného disku na hardware s podporou rozhraní UEFI a integruje Nástroj pro převod do místního procesu upgradu Windows 7 na Windows 10. Pokud tento nástroj zkombinujete s pořadím úkolů upgradu operačního systému a nástrojem OEM, který převede firmware ze systému BIOS na rozhraní UEFI, můžete počítače převést na systém BIOS na rozhraní UEFI v rámci místního upgradu na aktualizaci Windows 10 Creators Update.

**Požadavky**:
- Windows 10 Creators Update
- Počítače podporující rozhraní UEFI
- Nástroj OEM, který převede firmware počítače ze systému BIOS na rozhraní UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Převod ze systému BIOS na rozhraní UEFI během místního upgradu
1. Vytvořte pořadí úkolů pro upgrade operačního systému, které provede místní upgrade na Windows 10 Creators Update.
2. Upravte pořadí úkolů. Do **skupiny po zpracování**přidejte následující kroky pořadí úkolů:
   1. Od obecné přidejte krok **Spustit příkazový řádek** . Přidáte příkazový řádek pro nástroj MBR2GPT, který převede disk z MBR do GPT, aniž by bylo potřeba upravovat nebo odstraňovat data z disku. Do příkazového řádku zadejte následující: **MBR2GPT/Convert/disk: 0/AllowFullOS**. Můžete také zvolit, že se má spustit MBR2GPT. Nástroj EXE v systému Windows PE, nikoli v plném operačním systému. To můžete provést tak, že přidáte krok pro restartování počítače do prostředí WinPE před krokem ke spuštění MBR2GPT. Nástroj EXE a z příkazového řádku odeberte možnost/AllowFullOS. Podrobnosti o nástroji a dostupných možnostech najdete v tématu [MBR2GPT. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Přidejte krok, který spustí nástroj výrobce OEM, který převede firmware ze systému BIOS na rozhraní UEFI. Obvykle se jedná o krok spustit příkazový řádek pořadí úkolů s příkazovým řádkem pro spuštění nástroje OEM.
   3. V části Obecné přidejte krok **restartovat počítač** . Pokud chcete určit, co se má spustit po restartování, vyberte **aktuálně nainstalovaný výchozí operační systém**.
3. Nasaďte pořadí úkolů.
