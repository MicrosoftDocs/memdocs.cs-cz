---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: d887f842b789b41260a49b149b61f28741937613
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703657"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> Nejde odstranit kolekce.

<!--6245446-->
V této verzi větve Technical Preview nemůžete odstranit kolekce.

Pokud chcete tento problém obejít, odstraňte kolekce pomocí následujícího Configuration Manager rutiny PowerShellu:

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)