---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704597"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Některé kolekce nelze vytvořit ani upravit

<!--6197183-->
V této verzi větve Technical Preview nemůžete vytvořit novou kolekci. Nemůžete také upravovat vlastnosti existující kolekce uživatelů.

Pokud chcete tento problém obejít, pomocí rutin Configuration Manager PowerShellu vytvořte nové kolekce a upravte existující kolekce uživatelů. Mezi dostupné rutiny pro správu kolekcí patří:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)