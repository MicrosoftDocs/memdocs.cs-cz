---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712089"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a>Některé kolekce nelze vytvořit ani upravit

<!--6197183-->
V této verzi větve Technical Preview nemůžete vytvořit novou kolekci. Nemůžete také upravovat vlastnosti existující kolekce uživatelů.

Pokud chcete tento problém obejít, pomocí rutin Configuration Manager PowerShellu vytvořte nové kolekce a upravte existující kolekce uživatelů. Mezi dostupné rutiny pro správu kolekcí patří:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
