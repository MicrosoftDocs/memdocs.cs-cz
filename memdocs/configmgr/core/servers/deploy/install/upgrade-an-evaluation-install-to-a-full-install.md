---
title: Instalace zkušební verze
titleSuffix: Configuration Manager
description: Naučte se upgradovat instalaci zkušební verze na plnou instalaci Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717997"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Upgrade instalace Configuration Manager na úplnou instalaci

*Platí pro: Configuration Manager (Current Branch)*

Pokud jste nainstalovali Configuration Manager jako zkušební verzi po 180 dnech, bude konzola Configuration Manager jen pro čtení, dokud neaktivujete produkt ze stránky **Údržba lokality** v instalačním programu. K instalaci zkušební verze na plnou instalaci můžete kdykoli po 180 nebo po uplynutí této doby využít možnost upgradu.  

> [!NOTE]  
>  Když připojíte konzolu Configuration Manager k instalaci zkušební verze Configuration Manager, zobrazí se v záhlaví konzoly počet dnů, po jejichž uplynutí vyprší platnost zkušební instalace. Počet dní se automaticky neaktualizuje a aktualizuje se jenom při vytváření nového připojení k lokalitě.  

 Můžete upgradovat následující weby, na kterých běží zkušební instalace:  

-   Lokalita centrální správy  
-   Primární lokalita  

Vzhledem k tomu, že sekundární lokality nejsou považovány za instalace zkušební verze, nemusíte měnit sekundární lokalitu po upgradu své primární nadřazené lokality na úplnou instalaci.  

Požadavky na upgrade zkušební verze na licencovanou verzi:  

-   K použití během upgradu musíte mít platný produkt.  
-   Váš účet musí mít oprávnění **správce** v počítači, kde je lokalita nainstalována.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Upgrade zkušební verze Configuration Manager na licencovanou verzi  

1.  Na serveru lokality spusťte soubor **Setup. exe** (Configuration Manager instalační program) z instalační složky Configuration Manager (**%path%\BIN\X64**). Musíte spustit kopii instalačního programu, která je umístěna na serveru lokality ve složce Configuration Manager, protože možnosti údržby lokality nejsou k dispozici při spuštění instalačního programu z instalačního média nástroje.  
2.  Na stránce **než začnete** vyberte **Další**.  
3.  Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat lokalitu**a pak vyberte **Další**.  
4.  Na stránce **Údržba lokality** vyberte možnost **upgradovat zkušební edici na licencovanou verzi**, zadejte platný kód Product Key a pak vyberte **Další**.  
5.  Na stránce **licenční podmínky pro software společnosti Microsoft** si přečtěte a přijměte licenční podmínky a pak vyberte **Další**.  
6.  Na stránce **Konfigurace** kliknutím na tlačítko **Zavřít** dokončete průvodce.  

    > [!NOTE]  
    >  Záhlaví konzoly Configuration Manager, která zůstane připojená k upgradovanému webu, může znamenat, že lokalita je stále zkušební verzí, dokud znovu nepřipojíte konzolu k lokalitě nástroje.  
