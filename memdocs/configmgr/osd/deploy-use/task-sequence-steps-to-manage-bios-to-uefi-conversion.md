---
title: Převést systém BIOS na rozhraní UEFI
titleSuffix: Configuration Manager
description: Naučte se přizpůsobit sekvenci úloh nasazení operačního systému pro přípravu oddílu FAT32 pro přechod na rozhraní UEFI.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0118dd448520a6f0c21bfeea5f8509bd8e49fd46
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429392"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Kroky pořadí úloh pro správu převodu systému BIOS na UEFI

Windows 10 poskytuje mnoho nových funkcí zabezpečení, které vyžadují zařízení s podporou rozhraní UEFI. Je možné, že máte novější zařízení s Windows, která podporují rozhraní UEFI, ale používají starší verzi systému BIOS. Dříve se převedlo převod zařízení na rozhraní UEFI, které vyžaduje přechod na každé zařízení, přerozdělení pevného disku a překonfigurování firmwaru.

Pomocí Configuration Manager můžete automatizovat následující akce:

- Příprava pevného disku na převod ze systému BIOS na rozhraní UEFI
- Převod ze systému BIOS na rozhraní UEFI jako součást místního procesu upgradu
- Shromažďovat informace o rozhraní UEFI jako součást inventáře hardwaru

## <a name="hardware-inventory-collects-uefi-information"></a>Inventář hardwaru shromažďuje informace o rozhraní UEFI.

K dispozici je třída inventáře hardwaru (**SMS_Firmware**) a vlastnost (**UEFI**), která vám pomůže určit, jestli se počítač spustí v režimu UEFI. Pokud je počítač spuštěn v režimu UEFI, vlastnost **UEFI** je nastavena na **hodnotu true**. Inventář hardwaru tuto třídu standardně povoluje. Další informace o inventáři hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Vytvoření vlastního pořadí úloh pro přípravu pevného disku

Pořadí úloh nasazení operačního systému můžete přizpůsobit pomocí proměnné **TSUEFIDrive** . Krok **restartovat počítač** připraví oddíl FAT32 na pevném disku pro přechod na rozhraní UEFI. Následující postup popisuje, jak můžete vytvořit kroky pořadí úkolů k provedení této akce.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Příprava oddílu FAT32 pro převod na rozhraní UEFI

V existujícím pořadí úkolů pro instalaci operačního systému přidejte novou skupinu s postupem pro převod systému BIOS na rozhraní UEFI.

1. Po krocích k zaznamenání souborů a nastavení a před instalací operačního systému vytvořte novou skupinu pořadí úkolů. Například vytvořte skupinu za skupinou **zachycení souborů a nastavení** s názvem **BIOS-to-UEFI**.

1. Na kartě **Možnosti** nové skupiny přidejte jako podmínku novou proměnnou pořadí úloh. Nastavte **_SMSTSBootUEFI nerovná se true**. V tomto stavu pořadí úkolů spouští pouze tyto kroky na zařízeních se systémem BIOS.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Podmínka v systému BIOS na skupinu UEFI":::

1. V části Nová skupina přidejte krok pořadí úkolů **restartovat počítač** . V části **Určete, co se má spustit po restartování**vyberte **spouštěcí bitová kopie přiřazená k tomuto pořadí úkolů je vybraná**. Tato akce restartuje počítač v systému Windows PE.

1. Na kartě **Možnosti** přidejte jako podmínku proměnnou pořadí úloh. Nastavení **_SMSTSInWinPE rovno hodnotě false**. V tomto stavu pořadí úkolů nespustí tento krok, pokud je počítač již v systému Windows PE.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Podmínka při restartování kroku počítače":::

1. Přidejte krok, který spustí nástroj OEM a převede firmware ze systému BIOS na rozhraní UEFI. Tento krok je obvykle **spouštěn z příkazového řádku**s příkazem pro spuštění nástroje OEM.

1. Přidejte krok pořadí úkolů **Formátovat a rozdělit disk na oddíly** . V tomto kroku nakonfigurujte následující možnosti:

    1. Před instalací operačního systému vytvořte oddíl FAT32 pro převod na rozhraní UEFI. Jako **typ disku**vyberte **GPT**.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Konfigurace kroku formátovat a rozdělit disk na oddíly":::

    1. Přejít na vlastnosti oddílu FAT32. Do pole **Proměnná** zadejte `TSUEFIDrive` . Když pořadí úkolů detekuje tuto proměnnou, připraví oddíl pro přechod rozhraní UEFI před restartováním počítače.

        :::image type="content" source="media/partition-properties.png" alt-text="Konfigurace vlastností oddílu FAT32":::

    1. Vytvořte oddíl NTFS, který pořadí úkolů používá k uložení stavu a ukládání souborů protokolu.

1. Přidejte další krok pořadí úkolů **restartovat počítač** . V části **Určete, co se má spustit po restartování**vyberte **spouštěcí bitová kopie přiřazená k tomuto pořadí úkolů slouží** ke spuštění počítače v systému Windows PE.

    > [!TIP]
    > Ve výchozím nastavení je velikost oddílu EFI 500 MB. V některých prostředích je spouštěcí bitová kopie pro uložení na tomto oddílu příliš velká. Pokud chcete tento problém obejít, zvětšete velikost oddílu EFI. Nastavte ho například na 1 GB.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a>Převod ze systému BIOS na rozhraní UEFI během místního upgradu

Windows 10 obsahuje jednoduchý nástroj pro převod, **MBR2GPT**. Automatizuje proces opětovného rozdělení pevného disku na hardware s podporou rozhraní UEFI. Nástroj pro převod můžete integrovat do místního procesu upgradu na Windows 10. Zkombinujte tento nástroj s pořadím úkolů upgradu a nástrojem výrobce OEM, který převede firmware ze systému BIOS na rozhraní UEFI.

### <a name="requirements"></a>Požadavky

- Podporovaná verze Windows 10
- Počítače podporující rozhraní UEFI
- Nástroj OEM, který převede firmware počítače ze systému BIOS na rozhraní UEFI

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Proces převodu ze systému BIOS na rozhraní UEFI během pořadí úkolů místního upgradu

1. [Vytvoření pořadí úkolů pro upgrade operačního systému](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Upravte pořadí úkolů. Ve skupině **po zpracování** proveďte následující změny:

    1. Přidejte krok **Spustit příkazový řádek** . Zadejte příkazový řádek pro nástroj MBR2GPT. Při spuštění v úplném operačním systému ho nakonfigurujte tak, aby se disk přetajnal z MBR na GPT, aniž by bylo potřeba upravovat nebo odstraňovat data. Do **příkazového řádku**zadejte následující příkaz:`MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > Můžete také zvolit, že se má spustit MBR2GPT. Nástroj EXE v systému Windows PE, nikoli v plném operačním systému. Přidejte krok pro restartování počítače v prostředí Windows PE před krokem ke spuštění MBR2GPT. Nástroj EXE. Pak z příkazového řádku odeberte možnost **/AllowFullOS** .

    Další informace o nástroji a dostupných možnostech najdete v tématu [MBR2GPT. EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt).

    1. Přidejte krok ke spuštění nástroje výrobce OEM, který převede firmware ze systému BIOS na rozhraní UEFI. Tento krok je obvykle **spouštěn z příkazového řádku**s příkazovým řádkem pro spuštění nástroje OEM.

    1. Přidejte krok **restartovat počítač** a vyberte **aktuálně nainstalovaný výchozí operační systém**.

1. Nasaďte pořadí úkolů.
