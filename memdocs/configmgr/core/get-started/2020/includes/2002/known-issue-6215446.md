---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 979760d1ebdd9d8f91993361921ae437ed5b81b1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644337"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> Nejde odstranit kolekce.

<!--6245446-->
V této verzi větve Technical Preview nemůžete odstranit kolekce.

Pokud chcete tento problém obejít, odstraňte kolekce pomocí následujícího Configuration Manager rutiny PowerShellu:

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)