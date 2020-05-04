---
title: Úvod do dotazů
titleSuffix: Configuration Manager
description: Vytvořte a spusťte dotazy pro vyhledání objektů v hierarchii Configuration Manager, které odpovídají kritériím dotazu.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713818"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Seznámení s dotazy v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete vytvářet a spouštět dotazy pro vyhledání objektů v hierarchii Configuration Manager, které odpovídají kritériím dotazu. Mezi tyto objekty patří položky, jako jsou určité typy počítačů nebo skupiny uživatelů. Dotazy mohou vracet většinu typů Configuration Manager objektů, které zahrnují weby, kolekce, aplikace a data inventáře.  

## <a name="query-creation-overview"></a>Přehled vytváření dotazů

 Když vytvoříte dotaz, je nutné zadat nejméně dva parametry: kde chcete hledat a co chcete hledat. Chcete-li například zjistit množství místa na pevném disku, které je dostupné na všech počítačích v Configuration Manager lokalitě, můžete vytvořit dotaz pro hledání třídy atributů **logického disku** a atributu **volné místo (MB)** pro volné místo na pevném disku.  

 Po vytvoření počátečního dotazu, můžete zadat další kritéria dotazu. Například můžete zadat, že výsledky dotazu obsahovat jenom počítače, které jsou přiřazené k určité lokalitě. Můžete také změnit způsob zobrazení výsledků, abyste se mohli podívat na výsledky v pořadí, které je pro vás smysluplné. Například můžete určit, že výsledky jsou seřazené podle množství volného místa na pevném disku ve vzestupném nebo sestupném pořadí.  

 Když vytvoříte dotaz, uloží se Configuration Manager a zobrazí se v uzlu **dotazy** v pracovním prostoru **monitorování** . Z tohoto umístění můžete vytvářet nové dotazy a spouštět, aktualizovat a spravovat existující dotazy.  

 Dotaz můžete také importovat do pravidla dotazu v kolekci Configuration Manager. Další informace najdete v tématu [vytváření kolekcí](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Další kroky

 [Vytváření dotazů](../../../core/servers/manage/create-queries.md)
