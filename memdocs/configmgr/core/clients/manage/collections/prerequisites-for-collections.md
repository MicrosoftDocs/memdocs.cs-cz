---
title: Předpoklady pro kolekce
titleSuffix: Configuration Manager
description: Získejte předpoklady pro použití kolekcí v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714497"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Předpoklady pro kolekce v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Kolekce v Configuration Manager obsahují pouze závislosti v rámci produktu.  

## <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager  

|Závislost|Další informace|  
|----------------|----------------------|  
|Bod služby Reporting services|Před spuštěním sestav pro kolekce musí být nainstalovaná role systému lokality bodu služby Reporting Services. Další informace najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).|  
|Správa kolekcí vyžadovala udělení specifických oprávnění zabezpečení.|Ke správě nastavení dodržování předpisů je nutné mít následující oprávnění zabezpečení:<br /><br /> – Vytvoření a Správa kolekcí: **vytvořit**, **Odstranit**, **Upravit**, **Upravit složku**, **přesunout objekt**, **číst** a **číst prostředek** pro objekt **kolekce** .<br /><br /> – Pro správu nastavení kolekce: **Upravit nastavení kolekce** pro objekt **kolekce** .<br /><br /> Pro všechny složky kolekcí včetně kořenové složky je vyžadované oprávnění **Upravit složku** .|  
