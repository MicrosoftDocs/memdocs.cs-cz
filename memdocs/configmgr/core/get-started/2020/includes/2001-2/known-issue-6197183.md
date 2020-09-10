---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644117"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Některé kolekce nelze vytvořit ani upravit

<!--6197183-->
V této verzi větve Technical Preview nemůžete vytvořit novou kolekci. Nemůžete také upravovat vlastnosti existující kolekce uživatelů.

Pokud chcete tento problém obejít, pomocí rutin Configuration Manager PowerShellu vytvořte nové kolekce a upravte existující kolekce uživatelů. Mezi dostupné rutiny pro správu kolekcí patří:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)