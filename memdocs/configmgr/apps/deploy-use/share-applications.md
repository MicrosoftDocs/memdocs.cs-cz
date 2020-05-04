---
title: Sdílení aplikací v centru softwaru
titleSuffix: Configuration Manager
description: Sdílejte odkaz na aplikaci v centru softwaru v Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710073"
---
# <a name="share-an-application-from-software-center"></a>Sdílení aplikace z centra softwaru

*Platí pro: Configuration Manager (Current Branch)* <!-- 1706 -->

Hypertextový odkaz na aplikaci v centru softwaru můžete zkopírovat pomocí tlačítka ![sdílet](media/share15.png)**sdílení** v zobrazení podrobností o aplikaci.   Hypertextové odkazy můžete sdílet jenom pro aplikace. Pokud aplikace nebude k dispozici, hypertextový odkaz otevře okno s nedostupnou zprávou aplikace.

1. Zvolte **aplikace**a pak vyberte aplikaci.
2. Klikněte na ![tlačítko](media/share15.png) sdílet **sdílenou složku** .
3. V okně klikněte na tlačítko **Kopírovat** .
4. Vložte adresu URL do e-mailu, aby bylo možné aplikaci sdílet.  

> [!TIP]  
>  Chcete-li vytvořit odkaz v e-mailu Outlooku, stiskněte klávesu **CTRL** + **K** a vložte adresu URL.  
>  
> Ve výchozím nastavení zobrazí aplikace Outlook výstrahu zabezpečení pro protokol softwaru software Center, když příjemce klikne na odkaz. Zabraňte tomu ve vašem prostředí přidáním důvěryhodného klíče protokolu do registru. Například `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`.  
