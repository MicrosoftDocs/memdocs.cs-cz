---
title: Import a export aplikací
titleSuffix: Configuration Manager
description: Naučte se importovat a exportovat aplikace v Configuration Manager ke sdílení mezi samostatnými hierarchiemi.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3db127deb353f30566a1f03cbc6ac0eef666cb37
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695252"
---
# <a name="import-and-export-applications"></a>Import a export aplikací

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager můžete importovat a exportovat aplikace mezi dvěma hierarchiemi. Například zkopírujte aplikaci z testovacího prostředí do produkčního prostředí.

## <a name="export"></a>Export

1. V konzole Configuration Manager vyberte uzel **aplikace** . Ve skupině vytvořit na pásu karet vyberte **exportovat aplikaci**.
1. Na obrazovce **Obecné** zadejte cestu k novému souboru zip, do kterého chcete exportovat. Volitelně můžete určit, jestli se mají exportovat *závislosti, vztahy nahrazení, podmínky a virtuální prostředí*, a taky *obsah pro vybrané aplikace a závislosti*.  V případě potřeby zadejte libovolné komentáře správce a vyberte **Další**.
1. Ověřte, že je aplikace a všechny závislosti uvedené na stránce **související objekty** , a vyberte **Další**.
1. Na stránce Souhrn vyberte **Další**.
1. Po dokončení procesu se vytvoří soubor ZIP a průvodce můžete zavřít.

> [!IMPORTANT]
> Pokud budete chtít kopírovat tuto aplikaci do jiného prostředí, poznamenejte si soubor ZIP i složku, která ho doprovází. Soubor ZIP musí existovat ve stejném adresáři jako vytvořená složka.

## <a name="import"></a>Import

> [!NOTE]
> Můžete importovat jenom aplikace z cest UNC, takže nemůžete přímo importovat z místního disku.

1. V konzole Configuration Manager vyberte uzel **aplikace** . Ve skupině vytvořit na pásu karet vyberte možnost **importovat aplikaci**.
1. Zvolte soubor ZIP, který chcete importovat, a vyberte **Další**.
1. V okně obsah souboru se zobrazí informace o tom, co se stane, když aplikaci naimportujete. Vyberte **Další**.
1. Zkontrolujte obrazovku souhrn a vyberte **Další**.
1. Zavřete průvodce. Aplikace je nyní k dispozici v lokalitě.

## <a name="see-also"></a>Viz také:
 
Automatizujte import a export aplikací pomocí PowerShellu.

* [Import – CMApplication](/powershell/module/configurationmanager/import-cmapplication)
* [Export – CMApplication](/powershell/module/configurationmanager/export-cmapplication)