---
title: Zabezpečení a ochrana osobních údajů při řízení spotřeby
titleSuffix: Configuration Manager
description: Získejte informace o zabezpečení a ochraně osobních údajů pro řízení spotřeby v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715176"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tato část obsahuje informace o zabezpečení a ochraně osobních údajů pro řízení spotřeby v nástroji Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Osvědčené postupy pro zabezpečení řízení spotřeby  
 Nejsou žádné osvědčené postupy související se zabezpečením v souvislosti se řízením spotřeby.  

## <a name="privacy-information-for-power-management"></a>Ochrana osobních údajů při řízení spotřeby  
 Řízení spotřeby používá funkce vestavěné v systému Windows ke sledování spotřeby energie a k nastavení řízení spotřeby počítače během pracovní doby a mimo ni. Configuration Manager shromažďuje informace o spotřebě z počítačů, včetně dat o tom, kdy uživatel počítač používá. I když Configuration Manager monitoruje spotřebu energie pro kolekci, nikoli pro každý počítač, kolekce může obsahovat jenom jeden počítač. Řízení spotřeby není ve výchozím nastavení povolené a musí být nakonfigurované správcem.  

 Informace o spotřebě jsou uložené v databázi nástroje Configuration Manager a neodesílají se do Microsoftu. Podrobné informace se uchovávají v databázi 31 dnů a souhrnné informace 13 měsíců. Interval odstraňování nejde změnit.  

 Před konfigurací řízení spotřeby zvažte své požadavky na ochranu osobních údajů.  
