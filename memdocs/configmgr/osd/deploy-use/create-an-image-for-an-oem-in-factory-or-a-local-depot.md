---
title: Vytvoření image pro výrobce OEM v továrně nebo místním úložišti
titleSuffix: Configuration Manager
description: Nasazení předzpracovaného média můžete použít ke snížení síťového provozu při nasazení operačního systému do počítače, který není úplně zřízený.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125436"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Vytvoření image pro výrobce OEM v továrně nebo místním skladu pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení předzpracovaného média v Configuration Manager umožňuje nasadit operační systém na počítač, který není úplně zřízený. Předzpracované médium je soubor bitové kopie systému Windows (WIM). Výrobce (OEM) ho může nainstalovat do holého počítače, nebo ho můžete použít v přípravném centru, které je oddělené od produkčního prostředí.

Tato metoda nasazení může snížit síťový provoz, protože Bitová spouštěcí kopie a image operačního systému jsou již v cílovém počítači. Můžete určit aplikace, balíčky a balíčky ovladačů, které se mají zahrnout do předzpracovaného média. Po instalaci operačního systému v počítači pořadí úkolů nejprve zkontroluje předzpracovaný mezipaměť pro aplikace, balíčky nebo balíčky ovladačů. Pokud se nedaří najít potřebný obsah nebo je k dispozici novější revize online, pořadí úkolů stáhne obsah z distribučního bodu.

Předzpracovaná média můžete použít v následujících scénářích nasazení operačního systému:

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)

- [Nahrazení existujícího počítače a nastavení přenosu](replace-an-existing-computer-and-transfer-settings.md)

Proveďte kroky v jednom z těchto scénářů nasazení operačního systému. Pak použijte následující části k přípravě a vytvoření předzpracovaného média.

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení

Na stránce **nastavení nasazení** v nasazení vyberte u položky **zpřístupnit pro následující** nastavení jednu z následujících možností:

- Configuration Manager klienty, média a technologie PXE

- Pouze média a technologie PXE

- Pouze média a technologie PXE (skryté)

## <a name="create-the-prestaged-media"></a>Vytvoření předzpracovaného média

Vytvořte soubor předzpracovaného média, který chcete odeslat výrobci OEM nebo do místního skladu. Další informace najdete v tématu [Vytvoření předzpracovaného média pomocí Configuration Manager](create-prestaged-media.md).

## <a name="send-the-prestaged-media-file"></a>Odeslání souboru předzpracovaného média

Odešlete médium do výrobce OEM nebo do místního skladu, aby bylo možné je připravit na počítačích. Aplikují soubor obrázku na formátovaný pevný disk v počítači.

## <a name="deliver-the-computer"></a>Doručovat počítač

Když počítač doručíte uživateli a poprvé ho zapnete:

1. Počítač začíná předzpracovanými spouštěcími bitovými kopiemi.

1. Kontroluje hodnotu hash předzpracovaného média, aby se zajistilo, že je platný.

1. Počítač se připojí k bodu správy, aby měl k dispozici pořadí úkolů k dokončení tohoto procesu.

## <a name="next-steps"></a>Další kroky

[Uživatelská prostředí pro nasazení operačního systému](../understand/user-experience.md)
