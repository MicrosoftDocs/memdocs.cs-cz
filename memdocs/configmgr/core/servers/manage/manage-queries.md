---
title: Správa dotazů
titleSuffix: Configuration Manager
description: Naučte se spravovat dotazy. Obsahuje tabulku pro podrobný odkaz.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713748"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Správa dotazů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek vám může pomáhat při správě dotazů v Configuration Manager.  

 Informace o tom, jak vytvářet dotazy, najdete v tématu [Vytvoření dotazů](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Správa dotazů
 V pracovním prostoru **Monitorování** vyberte **Dotazy**, vyberte spravovaný dotaz a pak vyberte úlohu správy.  

 Následující tabulka poskytuje informace o úlohách správy.  

|Úloha správy|Podrobnosti| 
|---------------------|-------------|
|**Spouštěl**|Spustí vybraný dotaz a zobrazí výsledky v konzole Configuration Manager.|
|**Instalovat klienta**|Otevře **Průvodce instalací klienta**, který umožňuje nainstalovat klienta Configuration Manager v počítačích vrácených vybraným dotazem.<br /><br /> Tato možnost není dostupná pro dotazy, které vracejí mobilní zařízení, uživatele nebo skupiny uživatelů. <br /><br /> Další informace o instalaci Configuration Manager klientů pomocí klientské nabízené instalace najdete v tématu [nasazení klientů do počítačů se systémem Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Export**|Otevře **Průvodce exportem objektů**. Tento průvodce vám umožní exportovat dotaz do souboru formát MOF (Managed Object Format) (MOF), který pak můžete importovat v jiné lokalitě.
|**Přesunout**|Otevře dialogové okno **přesunout vybrané položky** . Toto dialogové okno umožňuje přesunout vybraný dotaz do složky, kterou jste předtím vytvořili pod uzlem **dotazy** .|

## <a name="next-steps"></a>Další kroky 
 [Vytváření dotazů](../../../core/servers/manage/create-queries.md)
