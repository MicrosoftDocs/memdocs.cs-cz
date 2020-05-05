---
title: Nástroj pro přenos knihovny obsahu
titleSuffix: Configuration Manager
description: Pomocí nástroje pro přenos knihovny obsahu Přeneste obsah z jedné diskové jednotky do jiné na Configuration Manager distribučním bodu.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720083"
---
# <a name="content-library-transfer-tool"></a>Nástroj pro přenos knihovny obsahu

*Platí pro: Configuration Manager (Current Branch)*

Nástroj pro přenos knihovny obsahu je jedním z [Configuration Manager nástrojů](tools.md). Přenáší obsah z jedné diskové jednotky do jiné. Nástroj je navržený tak, aby běžel v systémech lokality distribučního bodu. Podporuje distribuční body společně umístěné v lokalitě nebo vzdálených systémech lokality.  

Tento nástroj je užitečný pro situaci, kdy se disková jednotka hostující knihovnu obsahu zaplní. Nejdřív přidejte nebo Identifikujte jiný pevný disk s dostatkem místa pro hostování knihovny obsahu. Pak pomocí **ContentLibraryTransfer. exe** Přeneste obsah ze starého vyplněného pevného disku do nové, prázdné jednotky.
 
Po dokončení přenosu bude obsah přístupný klientským počítačům z nového umístění.



## <a name="usage"></a>Využití 

Spusťte **ContentLibraryTransfer. exe** jako uživatel s oprávněními správce v distribučním bodě. 

#### <a name="syntax"></a>Syntaxe 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Příklad
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Omezení

- Spusťte nástroj místně na distribučním bodu. Nemůžete ho spustit ze vzdáleného počítače.  

- Tuto položku použijte pouze v případě, že klienti aktivně nezískávají přístup k distribučnímu bodu. Pokud nástroj spustíte v době, kdy klienti přistupují k obsahu, nemusí mít Knihovna obsahu na cílové jednotce úplná data. Přenos dat může zcela selhat, což vede k nepoužitelné knihovně obsahu.  

- Při spuštění nástroje nedistribuujte obsah do distribučního bodu. Pokud nástroj spustíte během zápisu obsahu do distribučního bodu, knihovna obsahu na cílové jednotce pravděpodobně obsahuje Neúplná data. Přenos dat může zcela selhat, což vede k nepoužitelné knihovně obsahu.



## <a name="see-also"></a>Viz také

- [Základní koncepty správy obsahu](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Knihovna obsahu](../plan-design/hierarchy/the-content-library.md)
