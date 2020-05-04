---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716114"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a>Pořadí úloh nejsou k dispozici pro technologie PXE ani pro médium

<!--5578298-->
Pokud nasadíte pořadí úloh pro PXE nebo médium (USB nebo DVD), klient tyto zásady neobdrží. V **protokolu souboru Smsts. log**je tato zpráva:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Alternativní řešení

Spusťte pořadí úloh z centra softwaru.
